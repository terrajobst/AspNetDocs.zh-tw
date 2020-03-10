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
# <a name="custom-mvc-template"></a>自訂的 MVC 範本

依[Jacques Eloff](https://github.com/joeloff)

Visual Studio 2010 的 MVC 3 工具更新版本為 MVC 專案引進了個別的專案 wizard。 這項變更是由兩個因素所驅動。 首先，在 MVC 3 中引進新的範本，並支援其他視圖引擎（例如 Razor 潛在客戶），以便 overcrowding Visual Studio 中的 [新增專案] 對話方塊。 第二，客戶已要求擴充性點，而新的 MVC 專案 wizard 可能會讓我們有機會回應這些要求。

新增自訂範本是一種棘手程式，依賴于使用登錄，讓 MVC 專案 wizard 能夠看到新的範本。 新範本的作者必須將它包裝在 MSI 內，以確保在安裝時會建立所需的登錄專案。 替代方式是建立 ZIP 檔案，其中包含可用的範本，並讓使用者手動建立必要的登錄專案。

上述兩種方法都不理想，因此我們決定利用[VSIX](https://msdn.microsoft.com/library/ff363239.aspx)擴充功能所提供的一些現有基礎結構，讓您更輕鬆地撰寫、散發和安裝自 mvc 4 for Visual Studio 2012 開始的自訂 MVC 範本。 此方法所提供的一些優點包括：

- VSIX 擴充功能可以包含多個支援不同語言（C#和 Visual Basic）和多個視圖引擎（ASPX 和 Razor）的範本。
- VSIX 擴充功能可以將 Visual Studio 的多個 Sku 作為目標，包括 Express Sku。
- [Visual Studio 資源庫](https://visualstudiogallery.msdn.microsoft.com/)可協助將延伸模組散發給廣大的觀眾。
- VSIX 擴充功能可以升級，讓您更輕鬆地撰寫自訂範本的更正和更新。

## <a name="prerequisites"></a>Prerequisites

- 使用者必須熟悉撰寫專案範本，包括 .vstemplate 檔案的必要標記等等。
- 使用者必須安裝 Visual Studio Professional 和更新版本。 Express Sku 不支援建立 VSIX 專案。
- 已安裝[Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668) 。

## <a name="example"></a>範例

第一個步驟是使用C#或 Visual Basic 建立新的 VSIX 專案。 選取 [檔案] **> [新增專案**]，**然後按一下左窗格中的 [** 擴充性]，然後選取**VSIX 專案**。

![新增專案](custom-mvc-templates/_static/image1.jpg)

建立專案之後，將會開啟 VSIX 設計工具。

![專案設計工具中繼資料](custom-mvc-templates/_static/image2.jpg)

設計工具可以用來編輯延伸模組的一些一般屬性，當使用者安裝延伸模組或流覽 Visual Studio 中安裝的擴充功能時，會向他們顯示這些內容（[**工具 > 延伸模組和更新**]）。 完成一般資訊後，請按一下 [**安裝目標]** 索引標籤。

![專案設計工具安裝目標](custom-mvc-templates/_static/image3.jpg)

此索引標籤可用來指定您的擴充功能所支援的 Visual Studio Sku 和版本。 **針對所有使用者，選取 [此 vsix 已安裝**] 核取方塊，以啟用 VSIX 的每一電腦安裝。 按一下右側的 [**新增**] 按鈕，以新增其他 sku，例如 Web Developer EXPRESS （VWD）。

![加入新的安裝目標](custom-mvc-templates/_static/image4.jpg)

如果您想要支援所有 Professional 和更新版本的 Sku （Professional、Premium 和旗艦版），您只需要選取**Microsoft.VisualStudio.Pro**系列中的最低 SKU。 完成安裝目標後，請記得儲存所有變更。

![專案設計工具安裝目標](custom-mvc-templates/_static/image5.jpg)

[**資產**] 索引標籤可用來將您的所有內容檔案新增至 VSIX。 由於 MVC 需要自訂中繼資料，因此您將會編輯 VSIX 資訊清單檔案的原始 XML，而不是使用 [**資產**] 索引標籤來新增內容。 首先，將範本內容新增至 VSIX 專案。 資料夾和內容的結構必須鏡像專案的版面配置，這點很重要。 下列範例包含四個衍生自基本 MVC 專案範本的專案範本。 請確定組成專案範本的所有檔案（位於 ProjectTemplates 資料夾底下的所有檔案）都會加入至 VSIX 專案檔中的**Content** itemgroup，而且每個專案都包含**CopyToOutputDirectory**和**IncludeInVsix**元資料集，如下列範例所示。

&lt;內容包括 =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;

&lt;CopyToOutputDirectory&gt;一律&lt;/CopyToOutputDirectory&gt;

&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;

&lt;/Content&gt;

如果不是，IDE 會在您建立 VSIX 時嘗試編譯範本的內容，而且您可能會看到錯誤。 範本中的程式碼檔案通常包含專案範本具現化時 Visual Studio 所使用的特殊樣板[參數](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx)，因此無法在 IDE 中進行編譯。

![底下提供說明，包括方案總管](custom-mvc-templates/_static/image6.jpg)

關閉 VSIX 設計工具，然後以滑鼠右鍵按一下**方案總管**中的**來源. 副檔名**，並選取 [**開啟方式**]，然後選擇 [ **XML （文字）編輯器**] 選項。

![[開啟方式] 對話方塊](custom-mvc-templates/_static/image7.jpg)

建立 **&lt;資產&gt;** 元素，並為必須包含在 VSIX 中的每個檔案新增 **&lt;資產&gt;** 元素。 每個 **&lt;資產&gt;** 元素的**Type**屬性必須設定為**VisualStudio**。 這是只有 MVC project wizard 瞭解的自訂命名空間。 如需資訊清單檔結構和配置的詳細資訊，請參閱 VSIX 2.0 架構檔。

只要將檔案新增至 VSIX，就無法向 MVC wizard 註冊範本。 您必須將範本名稱、描述、支援的視圖引擎和程式設計語言等資訊提供給 MVC wizard。 這項資訊會包含在與每個 **.vstemplate**檔案的 **&lt;資產&gt;** 元素相關聯的自訂屬性中。

&lt;資產 d:VsixSubPath =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;

Type =&quot;VisualStudio&quot;

d:Source =&quot;檔案&quot;

Path =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;

ProjectType =&quot;MVC&quot;

Language =&quot;C#&quot;

ViewEngine =&quot;Aspx&quot;

TemplateId =&quot;MyMvcApplication&quot;

標題 =&quot;自訂基本 Web 應用程式&quot;

描述 =&quot;從基本 MVC web 應用程式（Razor）衍生的自訂範本&quot;

版本 =&quot;4.0&quot;/&gt;

以下是必須存在的自訂屬性說明：

- **ProjectType**必須設定為 MVC。
- **語言**指定範本所支援的開發語言。 有效值為C#或 VB。
- **ViewEngine**會指定範本所支援的 view engine，例如 Aspx 或 Razor。 您可以指定此欄位的自訂值。
- **TemplateId**是用來將範本分組。 如果值符合現有的範本識別碼，它會覆寫先前向 MVC wizard 註冊的範本。
- **標題**會指定在每個專案範本底下的 MVC wizard 中顯示的簡短描述。
- **描述**會指定更詳細的範本描述。

將所有檔案新增到資訊清單並加以儲存之後，您會注意到設計工具中的 [**資產**] 索引標籤會顯示所有檔案，而不是您新增至 **&lt;資產&gt;** **元素的自**定義屬性。

![專案設計工具資產](custom-mvc-templates/_static/image8.jpg)

現在剩下的就是編譯 VSIX 專案並安裝它。

請確定在您想要測試 VSIX 擴充功能的電腦上，已關閉 Visual Studio 的所有實例。 Visual Studio 會在啟動期間掃描新的延伸模組，因此，如果在安裝 VSIX 時 IDE 已開啟，您將需要重新開機 Visual Studio。 在 Explorer 中，按兩下 VSIX 檔案以啟動**Vsix 安裝程式**，按一下 [**安裝**]，然後啟動 Visual Studio。

![VSIX 安裝程式](custom-mvc-templates/_static/image9.jpg)

從功能表中，選取 [**工具] > [擴充功能和更新**]，確認已安裝您的延伸模組。 如果 VSIX 安裝程式在安裝延伸模組期間回報任何錯誤，您可以查看 VSIX 安裝程式記錄檔以取得詳細資訊。 記錄檔通常是在安裝延伸模組之使用者的 **% temp%** 資料夾中建立的，例如**C:\Users\Bob\AppData\Local\Temp**。

![擴充功能和更新](custom-mvc-templates/_static/image10.jpg)

關閉視窗之後，您可以建立 MVC 4 專案，以查看您的新範本是否顯示在 MVC wizard 中。

![新的 ASP.NET MVC 4 專案](custom-mvc-templates/_static/image11.jpg)

## <a name="limitations"></a>限制

1. MVC wizard 不支援當地語系化的自訂範本。
2. 如果找不到自訂範本，則 wizard 不會報告任何錯誤。 如果有任何必要的自訂屬性不存在，則會直接從 Wizard 排除此範本。
