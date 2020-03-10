---
uid: mvc/overview/advanced/custom-mvc-templates
title: 自訂 MVC 範本 |Microsoft Docs
author: joeloff
description: 建立範本做為 VSIX 擴充功能。
ms.author: riande
ms.date: 12/10/2012
ms.assetid: b0a214c7-2f38-4dbc-b47f-bd7bd9df97bd
msc.legacyurl: /mvc/overview/advanced/custom-mvc-templates
msc.type: authoredcontent
ms.openlocfilehash: 0603bc24e070e223551813f66a75889a2e46fd35
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616351"
---
# <a name="custom-mvc-template"></a><span data-ttu-id="34b8d-103">自訂的 MVC 範本</span><span class="sxs-lookup"><span data-stu-id="34b8d-103">Custom MVC Template</span></span>

<span data-ttu-id="34b8d-104">依[Jacques Eloff](https://github.com/joeloff)</span><span class="sxs-lookup"><span data-stu-id="34b8d-104">by [Jacques Eloff](https://github.com/joeloff)</span></span>

<span data-ttu-id="34b8d-105">Visual Studio 2010 的 MVC 3 工具更新版本為 MVC 專案引進了個別的專案 wizard。</span><span class="sxs-lookup"><span data-stu-id="34b8d-105">The release of MVC 3 Tools Update for Visual Studio 2010 introduced a separate project wizard for MVC projects.</span></span> <span data-ttu-id="34b8d-106">這項變更是由兩個因素所驅動。</span><span class="sxs-lookup"><span data-stu-id="34b8d-106">The change was driven by two factors.</span></span> <span data-ttu-id="34b8d-107">首先，在 MVC 3 中引進新的範本，並支援其他視圖引擎（例如 Razor 潛在客戶），以便 overcrowding Visual Studio 中的 [新增專案] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="34b8d-107">First, the introduction of new templates in MVC 3 and support for additional view engines such as Razor lead to overcrowding the New Project dialog in Visual Studio.</span></span> <span data-ttu-id="34b8d-108">第二，客戶已要求擴充性點，而新的 MVC 專案 wizard 可能會讓我們有機會回應這些要求。</span><span class="sxs-lookup"><span data-stu-id="34b8d-108">Second, customers had been asking for extensibility points and the new MVC project wizard would afford us the opportunity to respond to these requests.</span></span>

<span data-ttu-id="34b8d-109">新增自訂範本是一種棘手程式，依賴于使用登錄，讓 MVC 專案 wizard 能夠看到新的範本。</span><span class="sxs-lookup"><span data-stu-id="34b8d-109">Adding custom templates was an arduous process that relied on using the registry to make new templates visible to the MVC project wizard.</span></span> <span data-ttu-id="34b8d-110">新範本的作者必須將它包裝在 MSI 內，以確保在安裝時會建立所需的登錄專案。</span><span class="sxs-lookup"><span data-stu-id="34b8d-110">The author of a new template had to wrap it inside an MSI to ensure that the necessary registry entries would be created at install time.</span></span> <span data-ttu-id="34b8d-111">替代方式是建立 ZIP 檔案，其中包含可用的範本，並讓使用者手動建立必要的登錄專案。</span><span class="sxs-lookup"><span data-stu-id="34b8d-111">The alternative was to make a ZIP file containing the template available and have the end-user create the required registry entries by hand.</span></span>

<span data-ttu-id="34b8d-112">上述兩種方法都不理想，因此我們決定利用[VSIX](https://msdn.microsoft.com/library/ff363239.aspx)擴充功能所提供的一些現有基礎結構，讓您更輕鬆地撰寫、散發和安裝自 mvc 4 for Visual Studio 2012 開始的自訂 MVC 範本。</span><span class="sxs-lookup"><span data-stu-id="34b8d-112">Neither of the aforementioned approaches is ideal so we decided to leverage some of the existing infrastructure provided by [VSIX](https://msdn.microsoft.com/library/ff363239.aspx) extensions to make it easier to author, distribute and install custom MVC templates starting with MVC 4 for Visual Studio 2012.</span></span> <span data-ttu-id="34b8d-113">此方法所提供的一些優點包括：</span><span class="sxs-lookup"><span data-stu-id="34b8d-113">Some of the benefits provided by this approach are:</span></span>

- <span data-ttu-id="34b8d-114">VSIX 擴充功能可以包含多個支援不同語言（C#和 Visual Basic）和多個視圖引擎（ASPX 和 Razor）的範本。</span><span class="sxs-lookup"><span data-stu-id="34b8d-114">A VSIX extension can contain multiple templates that support different languages (C# and Visual Basic) and multiple view engines (ASPX and Razor).</span></span>
- <span data-ttu-id="34b8d-115">VSIX 擴充功能可以將 Visual Studio 的多個 Sku 作為目標，包括 Express Sku。</span><span class="sxs-lookup"><span data-stu-id="34b8d-115">A VSIX extension can target multiple SKUs of Visual Studio including Express SKUs.</span></span>
- <span data-ttu-id="34b8d-116">[Visual Studio 資源庫](https://visualstudiogallery.msdn.microsoft.com/)可協助將延伸模組散發給廣大的觀眾。</span><span class="sxs-lookup"><span data-stu-id="34b8d-116">The [Visual Studio Gallery](https://visualstudiogallery.msdn.microsoft.com/) facilitates distributing the extension to a wide audience.</span></span>
- <span data-ttu-id="34b8d-117">VSIX 擴充功能可以升級，讓您更輕鬆地撰寫自訂範本的更正和更新。</span><span class="sxs-lookup"><span data-stu-id="34b8d-117">VSIX extensions can be upgraded making it easier to author corrections and updates to your custom templates.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34b8d-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="34b8d-118">Prerequisites</span></span>

- <span data-ttu-id="34b8d-119">使用者必須熟悉撰寫專案範本，包括 .vstemplate 檔案的必要標記等等。</span><span class="sxs-lookup"><span data-stu-id="34b8d-119">Users need to be familiar with authoring project templates, including the required markup for vstemplate files, etc.</span></span>
- <span data-ttu-id="34b8d-120">使用者必須安裝 Visual Studio Professional 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="34b8d-120">Users will need to have Visual Studio Professional and higher installed.</span></span> <span data-ttu-id="34b8d-121">Express Sku 不支援建立 VSIX 專案。</span><span class="sxs-lookup"><span data-stu-id="34b8d-121">Express SKUs do not support creating VSIX projects.</span></span>
- <span data-ttu-id="34b8d-122">已安裝[Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668) 。</span><span class="sxs-lookup"><span data-stu-id="34b8d-122">[Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668) installed.</span></span>

## <a name="example"></a><span data-ttu-id="34b8d-123">範例</span><span class="sxs-lookup"><span data-stu-id="34b8d-123">Example</span></span>

<span data-ttu-id="34b8d-124">第一個步驟是使用C#或 Visual Basic 建立新的 VSIX 專案。</span><span class="sxs-lookup"><span data-stu-id="34b8d-124">The first step is to create a new VSIX project using either C# or Visual Basic.</span></span> <span data-ttu-id="34b8d-125">選取 [檔案] **> [新增專案**]，**然後按一下左窗格中的 [** 擴充性]，然後選取**VSIX 專案**。</span><span class="sxs-lookup"><span data-stu-id="34b8d-125">Select **File > New Project**, then click **Extensibility** in the left pane and select the **VSIX Project**.</span></span>

![新增專案](custom-mvc-templates/_static/image1.jpg)

<span data-ttu-id="34b8d-127">建立專案之後，將會開啟 VSIX 設計工具。</span><span class="sxs-lookup"><span data-stu-id="34b8d-127">After the project is created, the VSIX designer will be opened.</span></span>

![專案設計工具中繼資料](custom-mvc-templates/_static/image2.jpg)

<span data-ttu-id="34b8d-129">設計工具可以用來編輯延伸模組的一些一般屬性，當使用者安裝延伸模組或流覽 Visual Studio 中安裝的擴充功能時，會向他們顯示這些內容（[**工具 > 延伸模組和更新**]）。</span><span class="sxs-lookup"><span data-stu-id="34b8d-129">The designer can be used to edit some of the general properties of the extension that will be shown to users when they install the extension or browse the installed extensions in Visual Studio (**Tools > Extensions and Updates**).</span></span> <span data-ttu-id="34b8d-130">完成一般資訊後，請按一下 [**安裝目標]** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="34b8d-130">Once you have completed the general information click on the **Install Targets tab**.</span></span>

![專案設計工具安裝目標](custom-mvc-templates/_static/image3.jpg)

<span data-ttu-id="34b8d-132">此索引標籤可用來指定您的擴充功能所支援的 Visual Studio Sku 和版本。</span><span class="sxs-lookup"><span data-stu-id="34b8d-132">This tab is used to specify the SKUs and versions of Visual Studio that are supported by your extension.</span></span> <span data-ttu-id="34b8d-133">**針對所有使用者，選取 [此 vsix 已安裝**] 核取方塊，以啟用 VSIX 的每一電腦安裝。</span><span class="sxs-lookup"><span data-stu-id="34b8d-133">Select the checkbox for **This VSIX is installed for all users** to enable per-machine installs of the VSIX.</span></span> <span data-ttu-id="34b8d-134">按一下右側的 [**新增**] 按鈕，以新增其他 sku，例如 Web Developer EXPRESS （VWD）。</span><span class="sxs-lookup"><span data-stu-id="34b8d-134">Click on the **New** button on the right to add additional SKUs such as Web Developer Express (VWD).</span></span>

![加入新的安裝目標](custom-mvc-templates/_static/image4.jpg)

<span data-ttu-id="34b8d-136">如果您想要支援所有 Professional 和更新版本的 Sku （Professional、Premium 和旗艦版），您只需要選取**Microsoft.VisualStudio.Pro**系列中的最低 SKU。</span><span class="sxs-lookup"><span data-stu-id="34b8d-136">If you intend to support all the Professional and higher SKUs (Professional, Premium and Ultimate) you only need to select the minimum SKU in the family, **Microsoft.VisualStudio.Pro**.</span></span> <span data-ttu-id="34b8d-137">完成安裝目標後，請記得儲存所有變更。</span><span class="sxs-lookup"><span data-stu-id="34b8d-137">Remember to save all your changes once you have completed the Install Targets.</span></span>

![專案設計工具安裝目標](custom-mvc-templates/_static/image5.jpg)

<span data-ttu-id="34b8d-139">[**資產**] 索引標籤可用來將您的所有內容檔案新增至 VSIX。</span><span class="sxs-lookup"><span data-stu-id="34b8d-139">The **Assets** tab is used to add all your content files to the VSIX.</span></span> <span data-ttu-id="34b8d-140">由於 MVC 需要自訂中繼資料，因此您將會編輯 VSIX 資訊清單檔案的原始 XML，而不是使用 [**資產**] 索引標籤來新增內容。</span><span class="sxs-lookup"><span data-stu-id="34b8d-140">Since MVC requires custom metadata you will be editing the raw XML of the VSIX manifest file instead of using the **Assets** tab to add content.</span></span> <span data-ttu-id="34b8d-141">首先，將範本內容新增至 VSIX 專案。</span><span class="sxs-lookup"><span data-stu-id="34b8d-141">Start by adding the template contents to the VSIX project.</span></span> <span data-ttu-id="34b8d-142">資料夾和內容的結構必須鏡像專案的版面配置，這點很重要。</span><span class="sxs-lookup"><span data-stu-id="34b8d-142">It is important that the structure of the folder and the contents mirror the layout of the project.</span></span> <span data-ttu-id="34b8d-143">下列範例包含四個衍生自基本 MVC 專案範本的專案範本。</span><span class="sxs-lookup"><span data-stu-id="34b8d-143">The example below contains four project templates that were derived from the Basic MVC project template.</span></span> <span data-ttu-id="34b8d-144">請確定組成專案範本的所有檔案（位於 ProjectTemplates 資料夾底下的所有檔案）都會加入至 VSIX 專案檔中的**Content** itemgroup，而且每個專案都包含**CopyToOutputDirectory**和**IncludeInVsix**元資料集，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="34b8d-144">Make sure that all the files that comprise your project template (everything underneath the ProjectTemplates folder) are added to the **Content** itemgroup in the VSIX project file and that each item contains the **CopyToOutputDirectory** and **IncludeInVsix** metadata set as shown in the example below.</span></span>

<span data-ttu-id="34b8d-145">&lt;內容包括 =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;</span><span class="sxs-lookup"><span data-stu-id="34b8d-145">&lt;Content Include=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;</span></span>

<span data-ttu-id="34b8d-146">&lt;CopyToOutputDirectory&gt;一律&lt;/CopyToOutputDirectory&gt;</span><span class="sxs-lookup"><span data-stu-id="34b8d-146">&lt;CopyToOutputDirectory&gt;Always&lt;/CopyToOutputDirectory&gt;</span></span>

<span data-ttu-id="34b8d-147">&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;</span><span class="sxs-lookup"><span data-stu-id="34b8d-147">&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;</span></span>

<span data-ttu-id="34b8d-148">&lt;/Content&gt;</span><span class="sxs-lookup"><span data-stu-id="34b8d-148">&lt;/Content&gt;</span></span>

<span data-ttu-id="34b8d-149">如果不是，IDE 會在您建立 VSIX 時嘗試編譯範本的內容，而且您可能會看到錯誤。</span><span class="sxs-lookup"><span data-stu-id="34b8d-149">If not, the IDE will try to compile the contents of the template when you build the VSIX and you will likely see an error.</span></span> <span data-ttu-id="34b8d-150">範本中的程式碼檔案通常包含專案範本具現化時 Visual Studio 所使用的特殊樣板[參數](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx)，因此無法在 IDE 中進行編譯。</span><span class="sxs-lookup"><span data-stu-id="34b8d-150">Code files in templates often contain special [template parameters](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx) used by Visual Studio when the project template is instantiated and therefore cannot be compiled in the IDE.</span></span>

![底下提供說明，包括方案總管](custom-mvc-templates/_static/image6.jpg)

<span data-ttu-id="34b8d-152">關閉 VSIX 設計工具，然後以滑鼠右鍵按一下**方案總管**中的**來源. 副檔名**，並選取 [**開啟方式**]，然後選擇 [ **XML （文字）編輯器**] 選項。</span><span class="sxs-lookup"><span data-stu-id="34b8d-152">Close the VSIX designer, then right click on the **source.extension.manifest** file in **Solution Explorer** and select **Open With** and choose the **XML (Text) Editor** option.</span></span>

![[開啟方式] 對話方塊](custom-mvc-templates/_static/image7.jpg)

<span data-ttu-id="34b8d-154">建立 **&lt;資產&gt;** 元素，並為必須包含在 VSIX 中的每個檔案新增 **&lt;資產&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="34b8d-154">Create an **&lt;Assets&gt;** element and add an **&lt;Asset&gt;** element for each file that must be included in the VSIX.</span></span> <span data-ttu-id="34b8d-155">每個 **&lt;資產&gt;** 元素的**Type**屬性必須設定為**VisualStudio**。</span><span class="sxs-lookup"><span data-stu-id="34b8d-155">The **Type** attribute of each **&lt;Asset&gt;** element must be set to **Microsoft.VisualStudio.Mvc.Template**.</span></span> <span data-ttu-id="34b8d-156">這是只有 MVC project wizard 瞭解的自訂命名空間。</span><span class="sxs-lookup"><span data-stu-id="34b8d-156">This is a custom namespace that only the MVC project wizard understands.</span></span> <span data-ttu-id="34b8d-157">如需資訊清單檔結構和配置的詳細資訊，請參閱 VSIX 2.0 架構檔。</span><span class="sxs-lookup"><span data-stu-id="34b8d-157">Refer to the VSIX 2.0 Schema documentation for additional information on the structure and layout of the manifest file.</span></span>

<span data-ttu-id="34b8d-158">只要將檔案新增至 VSIX，就無法向 MVC wizard 註冊範本。</span><span class="sxs-lookup"><span data-stu-id="34b8d-158">Just adding the files to the VSIX is not sufficient to register the templates with the MVC wizard.</span></span> <span data-ttu-id="34b8d-159">您必須將範本名稱、描述、支援的視圖引擎和程式設計語言等資訊提供給 MVC wizard。</span><span class="sxs-lookup"><span data-stu-id="34b8d-159">You need to provide information such as the template name, description, supported view engines and programming language to the MVC wizard.</span></span> <span data-ttu-id="34b8d-160">這項資訊會包含在與每個 **.vstemplate**檔案的 **&lt;資產&gt;** 元素相關聯的自訂屬性中。</span><span class="sxs-lookup"><span data-stu-id="34b8d-160">This information is carried in custom attributes associated with the **&lt;Asset&gt;** element for each **vstemplate** file.</span></span>

<span data-ttu-id="34b8d-161">&lt;資產 d:VsixSubPath =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;</span><span class="sxs-lookup"><span data-stu-id="34b8d-161">&lt;Asset d:VsixSubPath=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;</span></span>

<span data-ttu-id="34b8d-162">Type =&quot;VisualStudio&quot;</span><span class="sxs-lookup"><span data-stu-id="34b8d-162">Type=&quot;Microsoft.VisualStudio.Mvc.Template&quot;</span></span>

<span data-ttu-id="34b8d-163">d:Source =&quot;檔案&quot;</span><span class="sxs-lookup"><span data-stu-id="34b8d-163">d:Source=&quot;File&quot;</span></span>

<span data-ttu-id="34b8d-164">Path =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;</span><span class="sxs-lookup"><span data-stu-id="34b8d-164">Path=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;</span></span>

<span data-ttu-id="34b8d-165">ProjectType =&quot;MVC&quot;</span><span class="sxs-lookup"><span data-stu-id="34b8d-165">ProjectType=&quot;MVC&quot;</span></span>

<span data-ttu-id="34b8d-166">Language =&quot;C#&quot;</span><span class="sxs-lookup"><span data-stu-id="34b8d-166">Language=&quot;C#&quot;</span></span>

<span data-ttu-id="34b8d-167">ViewEngine =&quot;Aspx&quot;</span><span class="sxs-lookup"><span data-stu-id="34b8d-167">ViewEngine=&quot;Aspx&quot;</span></span>

<span data-ttu-id="34b8d-168">TemplateId =&quot;MyMvcApplication&quot;</span><span class="sxs-lookup"><span data-stu-id="34b8d-168">TemplateId=&quot;MyMvcApplication&quot;</span></span>

<span data-ttu-id="34b8d-169">標題 =&quot;自訂基本 Web 應用程式&quot;</span><span class="sxs-lookup"><span data-stu-id="34b8d-169">Title=&quot;Custom Basic Web Application&quot;</span></span>

<span data-ttu-id="34b8d-170">描述 =&quot;從基本 MVC web 應用程式（Razor）衍生的自訂範本&quot;</span><span class="sxs-lookup"><span data-stu-id="34b8d-170">Description=&quot;A custom template derived from a Basic MVC web application (Razor)&quot;</span></span>

<span data-ttu-id="34b8d-171">版本 =&quot;4.0&quot;/&gt;</span><span class="sxs-lookup"><span data-stu-id="34b8d-171">Version=&quot;4.0&quot;/&gt;</span></span>

<span data-ttu-id="34b8d-172">以下是必須存在的自訂屬性說明：</span><span class="sxs-lookup"><span data-stu-id="34b8d-172">Below is an explanation of the custom attributes that must be present:</span></span>

- <span data-ttu-id="34b8d-173">**ProjectType**必須設定為 MVC。</span><span class="sxs-lookup"><span data-stu-id="34b8d-173">**ProjectType** must be set to MVC.</span></span>
- <span data-ttu-id="34b8d-174">**語言**指定範本所支援的開發語言。</span><span class="sxs-lookup"><span data-stu-id="34b8d-174">**Language** designates the development language supported by the template.</span></span> <span data-ttu-id="34b8d-175">有效值為C#或 VB。</span><span class="sxs-lookup"><span data-stu-id="34b8d-175">Valid values are either C# or VB.</span></span>
- <span data-ttu-id="34b8d-176">**ViewEngine**會指定範本所支援的 view engine，例如 Aspx 或 Razor。</span><span class="sxs-lookup"><span data-stu-id="34b8d-176">**ViewEngine** designates the view engine supported by the template such as Aspx or Razor.</span></span> <span data-ttu-id="34b8d-177">您可以指定此欄位的自訂值。</span><span class="sxs-lookup"><span data-stu-id="34b8d-177">You can specify a custom value for this field.</span></span>
- <span data-ttu-id="34b8d-178">**TemplateId**是用來將範本分組。</span><span class="sxs-lookup"><span data-stu-id="34b8d-178">**TemplateId** is used for grouping the templates.</span></span> <span data-ttu-id="34b8d-179">如果值符合現有的範本識別碼，它會覆寫先前向 MVC wizard 註冊的範本。</span><span class="sxs-lookup"><span data-stu-id="34b8d-179">If the value matches an existing template ID it will be override templates previously registered with the MVC wizard.</span></span>
- <span data-ttu-id="34b8d-180">**標題**會指定在每個專案範本底下的 MVC wizard 中顯示的簡短描述。</span><span class="sxs-lookup"><span data-stu-id="34b8d-180">**Title** designates the short description displayed in the MVC wizard beneath each project template.</span></span>
- <span data-ttu-id="34b8d-181">**描述**會指定更詳細的範本描述。</span><span class="sxs-lookup"><span data-stu-id="34b8d-181">**Description** designates a more verbose description of the template.</span></span>

<span data-ttu-id="34b8d-182">將所有檔案新增到資訊清單並加以儲存之後，您會注意到設計工具中的 [**資產**] 索引標籤會顯示所有檔案，而不是您新增至 **&lt;資產&gt;** **元素的自**定義屬性。</span><span class="sxs-lookup"><span data-stu-id="34b8d-182">After you have added all the files to the manifest and saved it, you will notice that the **Assets** tab in the designer will display all the files, but not the custom attributes you added to the **&lt;Asset&gt;** elements for the **vstemplate** files.</span></span>

![專案設計工具資產](custom-mvc-templates/_static/image8.jpg)

<span data-ttu-id="34b8d-184">現在剩下的就是編譯 VSIX 專案並安裝它。</span><span class="sxs-lookup"><span data-stu-id="34b8d-184">All that remains now is to compile the VSIX project and install it.</span></span>

<span data-ttu-id="34b8d-185">請確定在您想要測試 VSIX 擴充功能的電腦上，已關閉 Visual Studio 的所有實例。</span><span class="sxs-lookup"><span data-stu-id="34b8d-185">Make sure that all instances of Visual Studio are closed on the machine where you intend to test the VSIX extension.</span></span> <span data-ttu-id="34b8d-186">Visual Studio 會在啟動期間掃描新的延伸模組，因此，如果在安裝 VSIX 時 IDE 已開啟，您將需要重新開機 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="34b8d-186">Visual Studio scans for new extensions during startup, so if the IDE is open while installing a VSIX you will need to restart Visual Studio.</span></span> <span data-ttu-id="34b8d-187">在 Explorer 中，按兩下 VSIX 檔案以啟動**Vsix 安裝程式**，按一下 [**安裝**]，然後啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="34b8d-187">In Explorer, double click on the VSIX file to launch the **VSIX Installer**, click **Install** and then launch Visual Studio.</span></span>

![VSIX 安裝程式](custom-mvc-templates/_static/image9.jpg)

<span data-ttu-id="34b8d-189">從功能表中，選取 [**工具] > [擴充功能和更新**]，確認已安裝您的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="34b8d-189">From the menu, select **Tools > Extensions and Updates** to confirm that your extension was installed.</span></span> <span data-ttu-id="34b8d-190">如果 VSIX 安裝程式在安裝延伸模組期間回報任何錯誤，您可以查看 VSIX 安裝程式記錄檔以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="34b8d-190">If the VSIX Installer reported any errors during the installation of the extension you can view the VSIX Installer log for more information.</span></span> <span data-ttu-id="34b8d-191">記錄檔通常是在安裝延伸模組之使用者的 **% temp%** 資料夾中建立的，例如**C:\Users\Bob\AppData\Local\Temp**。</span><span class="sxs-lookup"><span data-stu-id="34b8d-191">The log is usually created in the **%temp%** folder of the user that installed the extension, for example **C:\Users\Bob\AppData\Local\Temp**.</span></span>

![擴充功能和更新](custom-mvc-templates/_static/image10.jpg)

<span data-ttu-id="34b8d-193">關閉視窗之後，您可以建立 MVC 4 專案，以查看您的新範本是否顯示在 MVC wizard 中。</span><span class="sxs-lookup"><span data-stu-id="34b8d-193">After closing the window you can create an MVC 4 project to see whether your new templates are shown in the MVC wizard.</span></span>

![新的 ASP.NET MVC 4 專案](custom-mvc-templates/_static/image11.jpg)

## <a name="limitations"></a><span data-ttu-id="34b8d-195">限制</span><span class="sxs-lookup"><span data-stu-id="34b8d-195">Limitations</span></span>

1. <span data-ttu-id="34b8d-196">MVC wizard 不支援當地語系化的自訂範本。</span><span class="sxs-lookup"><span data-stu-id="34b8d-196">The MVC wizard does not support localized custom templates.</span></span>
2. <span data-ttu-id="34b8d-197">如果找不到自訂範本，則 wizard 不會報告任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="34b8d-197">The wizard will not report any errors if it fails to locate custom templates.</span></span> <span data-ttu-id="34b8d-198">如果有任何必要的自訂屬性不存在，則會直接從 Wizard 排除此範本。</span><span class="sxs-lookup"><span data-stu-id="34b8d-198">If any of the required custom attributes are absent, the template would simply be excluded from the Wizard.</span></span>
