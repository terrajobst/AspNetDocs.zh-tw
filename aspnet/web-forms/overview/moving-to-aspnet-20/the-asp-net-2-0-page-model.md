---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 頁面模型 |Microsoft Docs
author: microsoft
description: 在 ASP.NET 1.x 中，開發人員可選擇內嵌程式碼模型和程式碼後置程式碼模型。 程式碼後置可以使用 Src attr 。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: bcb71b2b5a484e8756406867e08e8aa699a9024d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547646"
---
# <a name="the-aspnet-20-page-model"></a><span data-ttu-id="f3584-104">ASP.NET 2.0 頁面模型</span><span class="sxs-lookup"><span data-stu-id="f3584-104">The ASP.NET 2.0 Page Model</span></span>

<span data-ttu-id="f3584-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f3584-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="f3584-106">在 ASP.NET 1.x 中，開發人員可選擇內嵌程式碼模型和程式碼後置程式碼模型。</span><span class="sxs-lookup"><span data-stu-id="f3584-106">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="f3584-107">程式碼後置可以使用 Src 屬性或 @Page 指示詞的程式碼後置屬性來執行。</span><span class="sxs-lookup"><span data-stu-id="f3584-107">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="f3584-108">在 ASP.NET 2.0 中，開發人員仍然可以選擇內嵌程式碼和程式碼後置，但已大幅增強程式碼後置模型。</span><span class="sxs-lookup"><span data-stu-id="f3584-108">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

<span data-ttu-id="f3584-109">在 ASP.NET 1.x 中，開發人員可選擇內嵌程式碼模型和程式碼後置程式碼模型。</span><span class="sxs-lookup"><span data-stu-id="f3584-109">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="f3584-110">程式碼後置可以使用 Src 屬性或 @Page 指示詞的程式碼後置屬性來執行。</span><span class="sxs-lookup"><span data-stu-id="f3584-110">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="f3584-111">在 ASP.NET 2.0 中，開發人員仍然可以選擇內嵌程式碼和程式碼後置，但已大幅增強程式碼後置模型。</span><span class="sxs-lookup"><span data-stu-id="f3584-111">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

## <a name="improvements-in-the-code-behind-model"></a><span data-ttu-id="f3584-112">程式碼後置模型中的改良功能</span><span class="sxs-lookup"><span data-stu-id="f3584-112">Improvements in the Code-Behind Model</span></span>

<span data-ttu-id="f3584-113">若要完全瞭解 ASP.NET 2.0 中程式碼後置模型的變更，最好能夠快速地查看 ASP.NET 1.x 中存在的模型。</span><span class="sxs-lookup"><span data-stu-id="f3584-113">In order to fully understand the changes in the code-behind model in ASP.NET 2.0, its best to quickly review the model as it existed in ASP.NET 1.x.</span></span>

## <a name="the-code-behind-model-in-aspnet-1x"></a><span data-ttu-id="f3584-114">ASP.NET 1.x 中的程式碼後置模型</span><span class="sxs-lookup"><span data-stu-id="f3584-114">The Code-Behind Model in ASP.NET 1.x</span></span>

<span data-ttu-id="f3584-115">在 ASP.NET 1.x 中，程式碼後置模型是由一個 ASPX 檔案（Webform）和一個包含程式碼的程式碼後置檔案所組成。</span><span class="sxs-lookup"><span data-stu-id="f3584-115">In ASP.NET 1.x, the code-behind model consisted of an ASPX file (the Webform) and a code-behind file containing programming code.</span></span> <span data-ttu-id="f3584-116">這兩個檔案是使用 ASPX 檔案中的 @Page 指示詞進行連接。</span><span class="sxs-lookup"><span data-stu-id="f3584-116">The two files were connected using the @Page directive in the ASPX file.</span></span> <span data-ttu-id="f3584-117">ASPX 頁面上的每個控制項在程式碼後置檔案中都具有對應的宣告，做為執行個體變數。</span><span class="sxs-lookup"><span data-stu-id="f3584-117">Each control on the ASPX page had a corresponding declaration in the code-behind file as an instance variable.</span></span> <span data-ttu-id="f3584-118">程式碼後置檔案也包含事件系結的程式碼，以及 Visual Studio 設計工具所需的產生程式碼。</span><span class="sxs-lookup"><span data-stu-id="f3584-118">The code-behind file also contained code for event binding and generated code necessary for the Visual Studio designer.</span></span> <span data-ttu-id="f3584-119">此模型的運作良好，但因為 ASPX 頁面中的每個 ASP.NET 元素都需要程式碼後置檔案中的對應程式碼，所以不會真正區分程式碼和內容。</span><span class="sxs-lookup"><span data-stu-id="f3584-119">This model worked fairly well, but because every ASP.NET element in the ASPX page required corresponding code in the code-behind file, there was no true separation of code and content.</span></span> <span data-ttu-id="f3584-120">例如，如果設計工具已將新的伺服器控制項加入至 Visual Studio IDE 外部的 ASPX 檔案，應用程式將會因為不存在程式碼後置檔案中該控制項的宣告而中斷。</span><span class="sxs-lookup"><span data-stu-id="f3584-120">For example, if a designer added a new server control to an ASPX file outside of the Visual Studio IDE, the application would break due to the absence of a declaration for that control in the code-behind file.</span></span>

## <a name="the-code-behind-model-in-aspnet-20"></a><span data-ttu-id="f3584-121">ASP.NET 2.0 中的程式碼後置模型</span><span class="sxs-lookup"><span data-stu-id="f3584-121">The Code-Behind Model in ASP.NET 2.0</span></span>

<span data-ttu-id="f3584-122">ASP.NET 2.0 在此模型上有大幅改善。</span><span class="sxs-lookup"><span data-stu-id="f3584-122">ASP.NET 2.0 greatly improves upon this model.</span></span> <span data-ttu-id="f3584-123">在 ASP.NET 2.0 中，程式碼後置會使用 ASP.NET 2.0 中提供的新*部分類別*來執行。</span><span class="sxs-lookup"><span data-stu-id="f3584-123">In ASP.NET 2.0, code-behind is implemented using the new *partial classes* provided in ASP.NET 2.0.</span></span> <span data-ttu-id="f3584-124">ASP.NET 2.0 中的程式碼後置類別定義為部分類別，這表示它只包含類別定義的一部分。</span><span class="sxs-lookup"><span data-stu-id="f3584-124">The code-behind class in ASP.NET 2.0 is defined as a partial class meaning that it contains only part of the class definition.</span></span> <span data-ttu-id="f3584-125">類別定義的其餘部分是由 ASP.NET 2.0 在執行時間以動態方式產生，或在網站先行編譯時使用。</span><span class="sxs-lookup"><span data-stu-id="f3584-125">The remaining part of the class definition is dynamically generated by ASP.NET 2.0 using the ASPX page at runtime or when the Web site is precompiled.</span></span> <span data-ttu-id="f3584-126">程式碼後置檔案與 ASPX 頁面之間的連結，仍然是使用 @ Page 指示詞來建立的。</span><span class="sxs-lookup"><span data-stu-id="f3584-126">The link between the code-behind file and the ASPX page is still established using the @ Page directive.</span></span> <span data-ttu-id="f3584-127">不過，ASP.NET 2.0 現在會使用 CodeFile 屬性，而不是「後置」或 Src 屬性。</span><span class="sxs-lookup"><span data-stu-id="f3584-127">However, instead of a CodeBehind or Src attribute, ASP.NET 2.0 now uses the CodeFile attribute.</span></span> <span data-ttu-id="f3584-128">Inherits 屬性也用來指定頁面的類別名稱。</span><span class="sxs-lookup"><span data-stu-id="f3584-128">The Inherits attribute is also used to specify the class name for the page.</span></span>

<span data-ttu-id="f3584-129">一般的 @ Page 指示詞可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="f3584-129">A typical @ Page directive might look like this:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

<span data-ttu-id="f3584-130">ASP.NET 2.0 程式碼後置檔案中的一般類別定義看起來可能像這樣：</span><span class="sxs-lookup"><span data-stu-id="f3584-130">A typical class definition in an ASP.NET 2.0 code-behind file might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="f3584-131">C#和 Visual Basic 是目前唯一支援部分類別的 managed 語言。</span><span class="sxs-lookup"><span data-stu-id="f3584-131">C# and Visual Basic are the only managed languages that currently support partial classes.</span></span> <span data-ttu-id="f3584-132">因此，使用 j # 的開發人員將無法使用 ASP.NET 2.0 中的程式碼後置模型。</span><span class="sxs-lookup"><span data-stu-id="f3584-132">Therefore, developers using J# will not be able to use the code-behind model in ASP.NET 2.0.</span></span>

<span data-ttu-id="f3584-133">新模型會增強程式碼後置模型，因為開發人員現在會擁有只包含其所建立之程式碼的程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="f3584-133">The new model enhances the code-behind model because developers will now have code files that contain only the code that they have created.</span></span> <span data-ttu-id="f3584-134">它也提供程式碼和內容的真正分離，因為程式碼後置檔案中沒有任何執行個體變數宣告。</span><span class="sxs-lookup"><span data-stu-id="f3584-134">It also provides for a true separation of code and content because there are no instance variable declarations in the code-behind file.</span></span>

> [!NOTE]
> <span data-ttu-id="f3584-135">因為 ASPX 頁面的部分類別是事件系結髮生的地方，Visual Basic 開發人員可以使用程式碼後置中的 Handles 關鍵字來系結事件，以實現些許的效能提升。</span><span class="sxs-lookup"><span data-stu-id="f3584-135">Because the partial class for the ASPX page is where event binding takes place, Visual Basic developers can realize a slight performance increase by using the Handles keyword in code-behind to bind events.</span></span> <span data-ttu-id="f3584-136">C#沒有對等的關鍵字。</span><span class="sxs-lookup"><span data-stu-id="f3584-136">C# has no equivalent keyword.</span></span>

## <a name="new--page-directive-attributes"></a><span data-ttu-id="f3584-137">新的 @ Page 指示詞屬性</span><span class="sxs-lookup"><span data-stu-id="f3584-137">New @ Page Directive Attributes</span></span>

<span data-ttu-id="f3584-138">ASP.NET 2.0 將許多新的屬性加入 @ Page 指示詞。</span><span class="sxs-lookup"><span data-stu-id="f3584-138">ASP.NET 2.0 adds many new attributes to the @ Page directive.</span></span> <span data-ttu-id="f3584-139">下列是 ASP.NET 2.0 中新增的屬性。</span><span class="sxs-lookup"><span data-stu-id="f3584-139">The following attributes are new in ASP.NET 2.0.</span></span>

## <a name="async"></a><span data-ttu-id="f3584-140">非同步處理</span><span class="sxs-lookup"><span data-stu-id="f3584-140">Async</span></span>

<span data-ttu-id="f3584-141">Async 屬性可讓您將頁面設定為以非同步方式執行。</span><span class="sxs-lookup"><span data-stu-id="f3584-141">The Async attribute allows you to configure page to be executed asynchronously.</span></span> <span data-ttu-id="f3584-142">我們將在此課程模組稍後討論非同步頁面。</span><span class="sxs-lookup"><span data-stu-id="f3584-142">Well cover asynchronous pages later in this module.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="f3584-143">AsyncTimeout</span><span class="sxs-lookup"><span data-stu-id="f3584-143">AsyncTimeout</span></span>

<span data-ttu-id="f3584-144">已指定非同步頁面的超時時間。</span><span class="sxs-lookup"><span data-stu-id="f3584-144">Specified the timeout for asynchronous pages.</span></span> <span data-ttu-id="f3584-145">預設值為45秒。</span><span class="sxs-lookup"><span data-stu-id="f3584-145">The default is 45 seconds.</span></span>

## <a name="codefile"></a><span data-ttu-id="f3584-146">CodeFile</span><span class="sxs-lookup"><span data-stu-id="f3584-146">CodeFile</span></span>

<span data-ttu-id="f3584-147">CodeFile 屬性是取代 Visual Studio 2002/2003 中的程式碼後置屬性。</span><span class="sxs-lookup"><span data-stu-id="f3584-147">The CodeFile attribute is the replacement for the CodeBehind attribute in Visual Studio 2002/2003.</span></span>

### <a name="codefilebaseclass"></a><span data-ttu-id="f3584-148">CodeFileBaseClass</span><span class="sxs-lookup"><span data-stu-id="f3584-148">CodeFileBaseClass</span></span>

<span data-ttu-id="f3584-149">當您想要從單一基類衍生多個頁面時，會使用 CodeFileBaseClass 屬性。</span><span class="sxs-lookup"><span data-stu-id="f3584-149">The CodeFileBaseClass attribute is used in cases where you want multiple pages to derive from a single base class.</span></span> <span data-ttu-id="f3584-150">由於 ASP.NET 中部分類別的執行，若沒有此屬性，使用共用通用欄位來參考 ASPX 頁面中宣告之控制項的基類將無法正常運作，因為 ASP. 神經網路編譯引擎會根據頁面中的控制項自動建立新成員。</span><span class="sxs-lookup"><span data-stu-id="f3584-150">Because of the implementation of partial classes in ASP.NET, without this attribute, a base class that uses shared common fields to reference controls declared in an ASPX page would not work properly because ASP.NETs compilation engine will automatically create new members based on controls in the page.</span></span> <span data-ttu-id="f3584-151">因此，如果您想要在 ASP.NET 中有兩個或多個頁面的通用基類，就必須在 CodeFileBaseClass 屬性中定義指定基類，然後從該基類衍生每個頁面類別。</span><span class="sxs-lookup"><span data-stu-id="f3584-151">Therefore, if you want a common base class for two or more pages in ASP.NET, you will need to define specify your base class in the CodeFileBaseClass attribute and then derive each pages class from that base class.</span></span> <span data-ttu-id="f3584-152">使用此屬性時，也需要 CodeFile 屬性。</span><span class="sxs-lookup"><span data-stu-id="f3584-152">The CodeFile attribute is also required when this attribute is used.</span></span>

## <a name="compilationmode"></a><span data-ttu-id="f3584-153">CompilationMode</span><span class="sxs-lookup"><span data-stu-id="f3584-153">CompilationMode</span></span>

<span data-ttu-id="f3584-154">這個屬性可讓您設定 ASPX 頁面的 CompilationMode 屬性。</span><span class="sxs-lookup"><span data-stu-id="f3584-154">This attribute allows you to set the CompilationMode property of the ASPX page.</span></span> <span data-ttu-id="f3584-155">CompilationMode 屬性是包含**Always**、 **Auto**和**Never**值的列舉。</span><span class="sxs-lookup"><span data-stu-id="f3584-155">The CompilationMode property is an enumeration containing the values **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="f3584-156">預設值**一律**為。</span><span class="sxs-lookup"><span data-stu-id="f3584-156">The default is **Always**.</span></span> <span data-ttu-id="f3584-157">**自動**設定會防止 ASP.NET 在可能的情況下動態編譯頁面。</span><span class="sxs-lookup"><span data-stu-id="f3584-157">The **Auto** setting will prevent ASP.NET from dynamically compiling the page if possible.</span></span> <span data-ttu-id="f3584-158">排除動態編譯中的頁面會增加效能。</span><span class="sxs-lookup"><span data-stu-id="f3584-158">Excluding pages from dynamic compilation increases performance.</span></span> <span data-ttu-id="f3584-159">不過，如果排除的頁面包含必須編譯的程式碼，則在流覽網頁時，將會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="f3584-159">However, if a page that is excluded contains that code that must be compiled, an error will be thrown when the page is browsed.</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="f3584-160">EnableEventValidation</span><span class="sxs-lookup"><span data-stu-id="f3584-160">EnableEventValidation</span></span>

<span data-ttu-id="f3584-161">這個屬性會指定是否要驗證回傳和回呼事件。</span><span class="sxs-lookup"><span data-stu-id="f3584-161">This attribute specifies whether or not postback and callback events are validated.</span></span> <span data-ttu-id="f3584-162">啟用此選項時，會檢查回傳或回呼事件的引數，以確保它們源自原先呈現它們的伺服器控制項。</span><span class="sxs-lookup"><span data-stu-id="f3584-162">When this is enabled, arguments to postback or callback events are checked to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="f3584-163">EnableTheming</span><span class="sxs-lookup"><span data-stu-id="f3584-163">EnableTheming</span></span>

<span data-ttu-id="f3584-164">這個屬性會指定是否要在頁面上使用 ASP.NET 主題。</span><span class="sxs-lookup"><span data-stu-id="f3584-164">This attribute specifies whether or not ASP.NET themes are used on a page.</span></span> <span data-ttu-id="f3584-165">預設值為 **false**。</span><span class="sxs-lookup"><span data-stu-id="f3584-165">The default is **false**.</span></span> <span data-ttu-id="f3584-166">[模組 10](profiles-themes-and-web-parts.md)中涵蓋了 ASP.NET 主題。</span><span class="sxs-lookup"><span data-stu-id="f3584-166">ASP.NET themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="linepragmas"></a><span data-ttu-id="f3584-167">LinePragmas</span><span class="sxs-lookup"><span data-stu-id="f3584-167">LinePragmas</span></span>

<span data-ttu-id="f3584-168">這個屬性會指定是否應該在編譯期間加入行 pragma。</span><span class="sxs-lookup"><span data-stu-id="f3584-168">This attribute specifies whether line pragmas should be added during compilation.</span></span> <span data-ttu-id="f3584-169">行 pragma 是偵錯工具用來標示特定代碼區段的選項。</span><span class="sxs-lookup"><span data-stu-id="f3584-169">Line pragmas are options used by debuggers to mark specific sections of code.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="f3584-170">MaintainScrollPositionOnPostback</span><span class="sxs-lookup"><span data-stu-id="f3584-170">MaintainScrollPositionOnPostback</span></span>

<span data-ttu-id="f3584-171">這個屬性會指定是否要將 JavaScript 插入頁面中，以便維護回傳之間的滾動位置。</span><span class="sxs-lookup"><span data-stu-id="f3584-171">This attribute specifies whether or not JavaScript is injected into the page in order to maintain scroll position between postbacks.</span></span> <span data-ttu-id="f3584-172">此屬性預設為**false** 。</span><span class="sxs-lookup"><span data-stu-id="f3584-172">This attribute is **false** by default.</span></span>

<span data-ttu-id="f3584-173">當此屬性為**true**時，ASP.NET 會在回傳時加入 &lt;腳本&gt; 區塊，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f3584-173">When this attribute is **true**, ASP.NET will add a &lt;script&gt; block on postback that looks like this:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

<span data-ttu-id="f3584-174">請注意，此腳本區塊的 src 是 WebResource。</span><span class="sxs-lookup"><span data-stu-id="f3584-174">Note that the src for this script block is WebResource.axd.</span></span> <span data-ttu-id="f3584-175">此資源不是實體路徑。</span><span class="sxs-lookup"><span data-stu-id="f3584-175">This resource is not a physical path.</span></span> <span data-ttu-id="f3584-176">當要求此腳本時，ASP.NET 會以動態方式建立腳本。</span><span class="sxs-lookup"><span data-stu-id="f3584-176">When this script is requested, ASP.NET dynamically builds the script.</span></span>

### <a name="masterpagefile"></a><span data-ttu-id="f3584-177">MasterPageFile</span><span class="sxs-lookup"><span data-stu-id="f3584-177">MasterPageFile</span></span>

<span data-ttu-id="f3584-178">這個屬性會指定目前頁面的主版分頁檔案。</span><span class="sxs-lookup"><span data-stu-id="f3584-178">This attribute specifies the master page file for the current page.</span></span> <span data-ttu-id="f3584-179">路徑可為相對路徑或絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="f3584-179">The path can be relative or absolute.</span></span> <span data-ttu-id="f3584-180">主版頁面涵蓋于[模組 4](master-pages.md)。</span><span class="sxs-lookup"><span data-stu-id="f3584-180">Master pages are covered in [Module 4](master-pages.md).</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="f3584-181">StyleSheetTheme</span><span class="sxs-lookup"><span data-stu-id="f3584-181">StyleSheetTheme</span></span>

<span data-ttu-id="f3584-182">這個屬性可讓您覆寫 ASP.NET 2.0 主題所定義的使用者介面外觀屬性。</span><span class="sxs-lookup"><span data-stu-id="f3584-182">This attribute allows you to override user-interface appearance properties defined by an ASP.NET 2.0 theme.</span></span> <span data-ttu-id="f3584-183">[課程模組 10](profiles-themes-and-web-parts.md)中涵蓋了主題。</span><span class="sxs-lookup"><span data-stu-id="f3584-183">Themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="theme"></a><span data-ttu-id="f3584-184">佈景主題</span><span class="sxs-lookup"><span data-stu-id="f3584-184">Theme</span></span>

<span data-ttu-id="f3584-185">指定頁面的主題。</span><span class="sxs-lookup"><span data-stu-id="f3584-185">Specifies the theme for the page.</span></span> <span data-ttu-id="f3584-186">如果未指定 StyleSheetTheme 屬性的值，主題屬性會覆寫套用至頁面上之控制項的所有樣式。</span><span class="sxs-lookup"><span data-stu-id="f3584-186">If a value is not specified for the StyleSheetTheme attribute, the Theme attribute overrides all styles applied to controls on the page.</span></span>

## <a name="title"></a><span data-ttu-id="f3584-187">標題</span><span class="sxs-lookup"><span data-stu-id="f3584-187">Title</span></span>

<span data-ttu-id="f3584-188">設定頁面的標題。</span><span class="sxs-lookup"><span data-stu-id="f3584-188">Sets the title for the page.</span></span> <span data-ttu-id="f3584-189">此處指定的值將會出現在轉譯頁面的 &lt;標題&gt; 元素中。</span><span class="sxs-lookup"><span data-stu-id="f3584-189">The value specified here will appear in the &lt;title&gt; element of the rendered page.</span></span>

### <a name="viewstateencryptionmode"></a><span data-ttu-id="f3584-190">ViewStateEncryptionMode</span><span class="sxs-lookup"><span data-stu-id="f3584-190">ViewStateEncryptionMode</span></span>

<span data-ttu-id="f3584-191">設定 ViewStateEncryptionMode 列舉的值。</span><span class="sxs-lookup"><span data-stu-id="f3584-191">Sets the value for the ViewStateEncryptionMode enumeration.</span></span> <span data-ttu-id="f3584-192">可用的值**一律**為、 **Auto**和**Never**。</span><span class="sxs-lookup"><span data-stu-id="f3584-192">The available values are **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="f3584-193">預設值為 [**自動**]。當這個屬性設定為**Auto**的值時，viewstate 會進行加密，因為控制項會藉由呼叫**RegisterRequiresViewStateEncryption**方法來要求它。</span><span class="sxs-lookup"><span data-stu-id="f3584-193">The default value is **Auto**. When this attribute is set to a value of **Auto**, viewstate is encrypted is a control requests it by calling the **RegisterRequiresViewStateEncryption** method.</span></span>

## <a name="setting-public-property-values-via-the--page-directive"></a><span data-ttu-id="f3584-194">透過 @ Page 指示詞設定公用屬性值</span><span class="sxs-lookup"><span data-stu-id="f3584-194">Setting Public Property Values via the @ Page Directive</span></span>

<span data-ttu-id="f3584-195">在 ASP.NET 2.0 中，@ Page 指示詞的另一項新功能是能夠設定基類的公用屬性的起始值。</span><span class="sxs-lookup"><span data-stu-id="f3584-195">Another new capability of the @ Page directive in ASP.NET 2.0 is the ability to set the initial value of public properties of a base class.</span></span> <span data-ttu-id="f3584-196">例如，假設您在基類中有一個稱為**SomeText**的公用屬性，而您想要在載入頁面時將它初始化為**Hello** 。</span><span class="sxs-lookup"><span data-stu-id="f3584-196">Suppose, for example, that you have a public property called **SomeText** in your base class and you d like it to be initialized to **Hello** when a page is loaded.</span></span> <span data-ttu-id="f3584-197">您只要在 @ Page 指示詞中設定值，就可以完成這項操作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f3584-197">You can accomplish this by simply setting the value in the @ Page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

<span data-ttu-id="f3584-198">@ Page 指示詞的**SomeText**屬性會將基類中 SomeText 屬性的初始值設定為*Hello！* 。</span><span class="sxs-lookup"><span data-stu-id="f3584-198">The **SomeText** attribute of the @ Page directive sets the initial value of the SomeText property in the base class to *Hello!*.</span></span> <span data-ttu-id="f3584-199">以下影片將逐步解說如何使用 @ Page 指示詞，在基類中設定公用屬性的初始值。</span><span class="sxs-lookup"><span data-stu-id="f3584-199">The video below is a walkthrough of setting the initial value of a public property in a base class using the @ Page directive.</span></span>

![](the-asp-net-2-0-page-model/_static/image1.png)

[<span data-ttu-id="f3584-200">開啟全螢幕影片</span><span class="sxs-lookup"><span data-stu-id="f3584-200">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a><span data-ttu-id="f3584-201">頁面類別的新公用屬性</span><span class="sxs-lookup"><span data-stu-id="f3584-201">New Public Properties of the Page Class</span></span>

<span data-ttu-id="f3584-202">下列公用屬性是 ASP.NET 2.0 中的新功能。</span><span class="sxs-lookup"><span data-stu-id="f3584-202">The following public properties are new in ASP.NET 2.0.</span></span>

## <a name="apprelativetemplatesourcedirectory"></a><span data-ttu-id="f3584-203">AppRelativeTemplateSourceDirectory</span><span class="sxs-lookup"><span data-stu-id="f3584-203">AppRelativeTemplateSourceDirectory</span></span>

<span data-ttu-id="f3584-204">傳回頁面或控制項的應用程式相對路徑。</span><span class="sxs-lookup"><span data-stu-id="f3584-204">Returns the application-relative path to the page or control.</span></span> <span data-ttu-id="f3584-205">例如，針對位於 http://app/folder/page.aspx的頁面，屬性會傳回 ~/folder/。</span><span class="sxs-lookup"><span data-stu-id="f3584-205">For example, for a page located at http://app/folder/page.aspx, the property returns ~/folder/.</span></span>

## <a name="apprelativevirtualpath"></a><span data-ttu-id="f3584-206">AppRelativeVirtualPath</span><span class="sxs-lookup"><span data-stu-id="f3584-206">AppRelativeVirtualPath</span></span>

<span data-ttu-id="f3584-207">傳回頁面或控制項的相對虛擬目錄路徑。</span><span class="sxs-lookup"><span data-stu-id="f3584-207">Returns the relative virtual directory path to the page or control.</span></span> <span data-ttu-id="f3584-208">例如，針對位於 http://app/folder/page.aspx的頁面，屬性會傳回 ~/folder/page.aspx。</span><span class="sxs-lookup"><span data-stu-id="f3584-208">For example for a page located at http://app/folder/page.aspx, the property returns ~/folder/page.aspx.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="f3584-209">AsyncTimeout</span><span class="sxs-lookup"><span data-stu-id="f3584-209">AsyncTimeout</span></span>

<span data-ttu-id="f3584-210">取得或設定非同步網頁處理所使用的超時時間。</span><span class="sxs-lookup"><span data-stu-id="f3584-210">Gets or sets the timeout used for asynchronous page handling.</span></span> <span data-ttu-id="f3584-211">（此課程模組稍後會涵蓋非同步頁面。）</span><span class="sxs-lookup"><span data-stu-id="f3584-211">(Asynchronous pages will be covered later in this module.)</span></span>

## <a name="clientquerystring"></a><span data-ttu-id="f3584-212">ClientQueryString</span><span class="sxs-lookup"><span data-stu-id="f3584-212">ClientQueryString</span></span>

<span data-ttu-id="f3584-213">唯讀屬性，會傳回所要求 URL 的查詢字串部分。</span><span class="sxs-lookup"><span data-stu-id="f3584-213">A read-only property that returns the query string portion of the requested URL.</span></span> <span data-ttu-id="f3584-214">此值為 URL 編碼。</span><span class="sxs-lookup"><span data-stu-id="f3584-214">This value is URL encoded.</span></span> <span data-ttu-id="f3584-215">您可以使用 HttpServerUtility 類別的 UrlDecode 方法來對它進行解碼。</span><span class="sxs-lookup"><span data-stu-id="f3584-215">You can use the UrlDecode method of the HttpServerUtility class to decode it.</span></span>

## <a name="clientscript"></a><span data-ttu-id="f3584-216">Page.clientscript</span><span class="sxs-lookup"><span data-stu-id="f3584-216">ClientScript</span></span>

<span data-ttu-id="f3584-217">這個屬性會傳回 ClientScriptManager 物件，可用來管理 ASP。神經網路發出用戶端腳本。</span><span class="sxs-lookup"><span data-stu-id="f3584-217">This property returns a ClientScriptManager object that can be used to manage ASP.NETs emission of client-side script.</span></span> <span data-ttu-id="f3584-218">（此課程模組稍後會涵蓋 ClientScriptManager 類別）。</span><span class="sxs-lookup"><span data-stu-id="f3584-218">(The ClientScriptManager class is covered later in this module.)</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="f3584-219">EnableEventValidation</span><span class="sxs-lookup"><span data-stu-id="f3584-219">EnableEventValidation</span></span>

<span data-ttu-id="f3584-220">此屬性控制是否啟用回傳和回呼事件的事件驗證。</span><span class="sxs-lookup"><span data-stu-id="f3584-220">This property controls whether or not event validation is enabled for postback and callback events.</span></span> <span data-ttu-id="f3584-221">啟用時，回傳或回呼事件的引數會經過驗證，以確保它們源自原先呈現它們的伺服器控制項。</span><span class="sxs-lookup"><span data-stu-id="f3584-221">When enabled, arguments to postback or callback events are verified to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="f3584-222">EnableTheming</span><span class="sxs-lookup"><span data-stu-id="f3584-222">EnableTheming</span></span>

<span data-ttu-id="f3584-223">這個屬性會取得或設定布林值，指定 ASP.NET 2.0 主題是否要套用至頁面。</span><span class="sxs-lookup"><span data-stu-id="f3584-223">This property gets or sets a Boolean that specifies whether or not an ASP.NET 2.0 theme applies to the page.</span></span>

## <a name="form"></a><span data-ttu-id="f3584-224">表單</span><span class="sxs-lookup"><span data-stu-id="f3584-224">Form</span></span>

<span data-ttu-id="f3584-225">這個屬性會以 HtmlForm 物件的形式傳回 ASPX 頁面上的 HTML 表單。</span><span class="sxs-lookup"><span data-stu-id="f3584-225">This property returns the HTML form on the ASPX page as an HtmlForm object.</span></span>

## <a name="header"></a><span data-ttu-id="f3584-226">頁首</span><span class="sxs-lookup"><span data-stu-id="f3584-226">Header</span></span>

<span data-ttu-id="f3584-227">這個屬性會傳回包含頁首之 HtmlHead 物件的參考。</span><span class="sxs-lookup"><span data-stu-id="f3584-227">This property returns a reference to an HtmlHead object that contains the page header.</span></span> <span data-ttu-id="f3584-228">您可以使用傳回的 HtmlHead 物件來取得/設定樣式表單、中繼標記等。</span><span class="sxs-lookup"><span data-stu-id="f3584-228">You can use the returned HtmlHead object to get/set style sheets, Meta tags, etc.</span></span>

## <a name="idseparator"></a><span data-ttu-id="f3584-229">IdSeparator</span><span class="sxs-lookup"><span data-stu-id="f3584-229">IdSeparator</span></span>

<span data-ttu-id="f3584-230">當 ASP.NET 為頁面上的控制項建立唯一識別碼時，這個唯讀屬性會取得用來分隔控制項識別碼的字元。</span><span class="sxs-lookup"><span data-stu-id="f3584-230">This read-only property gets the character that is used to separate control identifiers when ASP.NET is building a unique ID for controls on a page.</span></span> <span data-ttu-id="f3584-231">但並不是針對直接從程式碼使用而設計。</span><span class="sxs-lookup"><span data-stu-id="f3584-231">It is not intended to be used directly from your code.</span></span>

## <a name="isasync"></a><span data-ttu-id="f3584-232">IsAsync</span><span class="sxs-lookup"><span data-stu-id="f3584-232">IsAsync</span></span>

<span data-ttu-id="f3584-233">這個屬性允許非同步頁面。</span><span class="sxs-lookup"><span data-stu-id="f3584-233">This property allows for asynchronous pages.</span></span> <span data-ttu-id="f3584-234">本課程模組稍後會討論非同步網頁。</span><span class="sxs-lookup"><span data-stu-id="f3584-234">Asynchronous pages are discussed later in this module.</span></span>

## <a name="iscallback"></a><span data-ttu-id="f3584-235">IsCallback</span><span class="sxs-lookup"><span data-stu-id="f3584-235">IsCallback</span></span>

<span data-ttu-id="f3584-236">如果頁面是回呼的結果，此唯讀屬性會傳回**true** 。</span><span class="sxs-lookup"><span data-stu-id="f3584-236">This read-only property returns **true** if the page is the result of a call back.</span></span> <span data-ttu-id="f3584-237">稍後會在此課程模組中討論電話支援。</span><span class="sxs-lookup"><span data-stu-id="f3584-237">Call backs are discussed later in this module.</span></span>

## <a name="iscrosspagepostback"></a><span data-ttu-id="f3584-238">IsCrossPagePostBack</span><span class="sxs-lookup"><span data-stu-id="f3584-238">IsCrossPagePostBack</span></span>

<span data-ttu-id="f3584-239">如果頁面是跨頁面回傳的一部分，此唯讀屬性會傳回**true** 。</span><span class="sxs-lookup"><span data-stu-id="f3584-239">This read-only property returns **true** if the page is part of a cross-page postback.</span></span> <span data-ttu-id="f3584-240">本課程模組稍後會涵蓋跨頁面回傳。</span><span class="sxs-lookup"><span data-stu-id="f3584-240">Cross-page postbacks are covered later in this module.</span></span>

## <a name="items"></a><span data-ttu-id="f3584-241">項目</span><span class="sxs-lookup"><span data-stu-id="f3584-241">Items</span></span>

<span data-ttu-id="f3584-242">傳回 IDictionary 實例的參考，其中包含儲存在頁面內容中的所有物件。</span><span class="sxs-lookup"><span data-stu-id="f3584-242">Returns a reference to an IDictionary instance that contains all objects stored in the pages context.</span></span> <span data-ttu-id="f3584-243">您可以將專案新增至此 IDictionary 物件，而且在內容的整個存留期間都可以使用它們。</span><span class="sxs-lookup"><span data-stu-id="f3584-243">You can add items to this IDictionary object and they will be available to you throughout the lifetime of the context.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="f3584-244">MaintainScrollPositionOnPostBack</span><span class="sxs-lookup"><span data-stu-id="f3584-244">MaintainScrollPositionOnPostBack</span></span>

<span data-ttu-id="f3584-245">此屬性控制 ASP.NET 是否會發出 JavaScript，以在回傳之後，維護瀏覽器中的頁面滾動位置。</span><span class="sxs-lookup"><span data-stu-id="f3584-245">This property controls whether or not ASP.NET emits JavaScript that maintains the pages scroll position in the browser after a postback occurs.</span></span> <span data-ttu-id="f3584-246">（本課程模組稍早已討論過此屬性的詳細資料）。</span><span class="sxs-lookup"><span data-stu-id="f3584-246">(Details of this property were discussed earlier in this module.)</span></span>

## <a name="master"></a><span data-ttu-id="f3584-247">Master</span><span class="sxs-lookup"><span data-stu-id="f3584-247">Master</span></span>

<span data-ttu-id="f3584-248">這個唯讀屬性會針對已套用主版頁面的頁面，傳回 MasterPage 實例的參考。</span><span class="sxs-lookup"><span data-stu-id="f3584-248">This read-only property returns a reference to the MasterPage instance for a page to which a master page has been applied.</span></span>

## <a name="masterpagefile"></a><span data-ttu-id="f3584-249">MasterPageFile</span><span class="sxs-lookup"><span data-stu-id="f3584-249">MasterPageFile</span></span>

<span data-ttu-id="f3584-250">取得或設定頁面的主版分頁檔名。</span><span class="sxs-lookup"><span data-stu-id="f3584-250">Gets or sets the master page filename for the page.</span></span> <span data-ttu-id="f3584-251">這個屬性只能在 PreInit 方法中設定。</span><span class="sxs-lookup"><span data-stu-id="f3584-251">This property can only be set in the PreInit method.</span></span>

## <a name="maxpagestatefieldlength"></a><span data-ttu-id="f3584-252">MaxPageStateFieldLength</span><span class="sxs-lookup"><span data-stu-id="f3584-252">MaxPageStateFieldLength</span></span>

<span data-ttu-id="f3584-253">這個屬性會取得或設定頁面狀態的最大長度（以位元組為單位）。</span><span class="sxs-lookup"><span data-stu-id="f3584-253">This property gets or sets the maximum length for the pages state in bytes.</span></span> <span data-ttu-id="f3584-254">如果屬性設定為正數，網頁檢視狀態將會分成多個隱藏欄位，使其不會超過指定的位元組數。</span><span class="sxs-lookup"><span data-stu-id="f3584-254">If the property is set to a positive number, the pages view state will be broken up into multiple hidden fields so that it doesnt exceed the number of bytes specified.</span></span> <span data-ttu-id="f3584-255">如果屬性為負數，則檢視狀態將不會分成多個區塊。</span><span class="sxs-lookup"><span data-stu-id="f3584-255">If the property is a negative number, the view state will not be broken into chunks.</span></span>

## <a name="pageadapter"></a><span data-ttu-id="f3584-256">PageAdapter</span><span class="sxs-lookup"><span data-stu-id="f3584-256">PageAdapter</span></span>

<span data-ttu-id="f3584-257">傳回對要求的瀏覽器修改頁面的 PageAdapter 物件參考。</span><span class="sxs-lookup"><span data-stu-id="f3584-257">Returns a reference to the PageAdapter object that modifies the page for the requesting browser.</span></span>

## <a name="previouspage"></a><span data-ttu-id="f3584-258">PreviousPage</span><span class="sxs-lookup"><span data-stu-id="f3584-258">PreviousPage</span></span>

<span data-ttu-id="f3584-259">當伺服器. 傳輸或跨頁面回傳時，傳回前一頁的參考。</span><span class="sxs-lookup"><span data-stu-id="f3584-259">Returns a reference to the previous page in cases of a Server.Transfer or a cross-page postback.</span></span>

## <a name="skinid"></a><span data-ttu-id="f3584-260">SkinID</span><span class="sxs-lookup"><span data-stu-id="f3584-260">SkinID</span></span>

<span data-ttu-id="f3584-261">指定要套用至頁面的 ASP.NET 2.0 面板。</span><span class="sxs-lookup"><span data-stu-id="f3584-261">Specifies the ASP.NET 2.0 skin to apply to the page.</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="f3584-262">StyleSheetTheme</span><span class="sxs-lookup"><span data-stu-id="f3584-262">StyleSheetTheme</span></span>

<span data-ttu-id="f3584-263">這個屬性會取得或設定套用至頁面的樣式表單。</span><span class="sxs-lookup"><span data-stu-id="f3584-263">This property gets or sets the style sheet that is applied to a page.</span></span>

## <a name="templatecontrol"></a><span data-ttu-id="f3584-264">TemplateControl</span><span class="sxs-lookup"><span data-stu-id="f3584-264">TemplateControl</span></span>

<span data-ttu-id="f3584-265">傳回頁面之包含控制項的參考。</span><span class="sxs-lookup"><span data-stu-id="f3584-265">Returns a reference to the containing control for the page.</span></span>

## <a name="theme"></a><span data-ttu-id="f3584-266">佈景主題</span><span class="sxs-lookup"><span data-stu-id="f3584-266">Theme</span></span>

<span data-ttu-id="f3584-267">取得或設定套用至頁面的 ASP.NET 2.0 主題名稱。</span><span class="sxs-lookup"><span data-stu-id="f3584-267">Gets or sets the name of the ASP.NET 2.0 theme applied to the page.</span></span> <span data-ttu-id="f3584-268">在 PreInit 方法之前，必須先設定此值。</span><span class="sxs-lookup"><span data-stu-id="f3584-268">This value must be set prior to the PreInit method.</span></span>

## <a name="title"></a><span data-ttu-id="f3584-269">標題</span><span class="sxs-lookup"><span data-stu-id="f3584-269">Title</span></span>

<span data-ttu-id="f3584-270">這個屬性會取得或設定頁面標頭中所取得之網頁的標題。</span><span class="sxs-lookup"><span data-stu-id="f3584-270">This property gets or sets the title for the page as obtained from the pages header.</span></span>

## <a name="viewstateencryptionmode"></a><span data-ttu-id="f3584-271">ViewStateEncryptionMode</span><span class="sxs-lookup"><span data-stu-id="f3584-271">ViewStateEncryptionMode</span></span>

<span data-ttu-id="f3584-272">取得或設定頁面的 ViewStateEncryptionMode。</span><span class="sxs-lookup"><span data-stu-id="f3584-272">Gets or sets the ViewStateEncryptionMode of the page.</span></span> <span data-ttu-id="f3584-273">請參閱此課程模組稍早的此屬性的詳細討論。</span><span class="sxs-lookup"><span data-stu-id="f3584-273">See a detailed discussion of this property earlier in this module.</span></span>

## <a name="new-protected-properties-of-the-page-class"></a><span data-ttu-id="f3584-274">頁面類別的新受保護屬性</span><span class="sxs-lookup"><span data-stu-id="f3584-274">New Protected Properties of the Page Class</span></span>

<span data-ttu-id="f3584-275">以下是 ASP.NET 2.0 中頁面類別的新受保護屬性。</span><span class="sxs-lookup"><span data-stu-id="f3584-275">The following are the new protected properties of the Page class in ASP.NET 2.0.</span></span>

## <a name="adapter"></a><span data-ttu-id="f3584-276">配接器</span><span class="sxs-lookup"><span data-stu-id="f3584-276">Adapter</span></span>

<span data-ttu-id="f3584-277">傳回 ControlAdapter 的參考，它會在要求的裝置上呈現頁面。</span><span class="sxs-lookup"><span data-stu-id="f3584-277">Returns a reference to the ControlAdapter that renders the page on the device that requested it.</span></span>

## <a name="asyncmode"></a><span data-ttu-id="f3584-278">AsyncMode</span><span class="sxs-lookup"><span data-stu-id="f3584-278">AsyncMode</span></span>

<span data-ttu-id="f3584-279">這個屬性會指出是否要以非同步方式處理頁面。</span><span class="sxs-lookup"><span data-stu-id="f3584-279">This property indicates whether or not the page is processed asynchronously.</span></span> <span data-ttu-id="f3584-280">它適用于執行時間，而不是直接在程式碼中使用。</span><span class="sxs-lookup"><span data-stu-id="f3584-280">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="clientidseparator"></a><span data-ttu-id="f3584-281">ClientIDSeparator</span><span class="sxs-lookup"><span data-stu-id="f3584-281">ClientIDSeparator</span></span>

<span data-ttu-id="f3584-282">這個屬性會傳回建立控制項的唯一用戶端識別碼時，用來做為分隔符號的字元。</span><span class="sxs-lookup"><span data-stu-id="f3584-282">This property returns the character used as a separator when creating unique client IDs for controls.</span></span> <span data-ttu-id="f3584-283">它適用于執行時間，而不是直接在程式碼中使用。</span><span class="sxs-lookup"><span data-stu-id="f3584-283">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="pagestatepersister"></a><span data-ttu-id="f3584-284">PageStatePersister</span><span class="sxs-lookup"><span data-stu-id="f3584-284">PageStatePersister</span></span>

<span data-ttu-id="f3584-285">這個屬性會傳回頁面的 PageStatePersister 物件。</span><span class="sxs-lookup"><span data-stu-id="f3584-285">This property returns the PageStatePersister object for the page.</span></span> <span data-ttu-id="f3584-286">這個屬性主要是由 ASP.NET 控制項開發人員使用。</span><span class="sxs-lookup"><span data-stu-id="f3584-286">This property is primarily used by ASP.NET control developers.</span></span>

## <a name="uniquefilepathsuffix"></a><span data-ttu-id="f3584-287">UniqueFilePathSuffix</span><span class="sxs-lookup"><span data-stu-id="f3584-287">UniqueFilePathSuffix</span></span>

<span data-ttu-id="f3584-288">這個屬性會傳回附加至快取瀏覽器之檔案路徑的唯一尾碼。</span><span class="sxs-lookup"><span data-stu-id="f3584-288">This property returns a unique suffix that is appended to the file path for caching browsers.</span></span> <span data-ttu-id="f3584-289">預設值為 \_\_ufps = 和6位數的數位。</span><span class="sxs-lookup"><span data-stu-id="f3584-289">The default value is \_\_ufps= and a 6-digit number.</span></span>

## <a name="new-public-methods-for-the-page-class"></a><span data-ttu-id="f3584-290">Page 類別的新公用方法</span><span class="sxs-lookup"><span data-stu-id="f3584-290">New Public Methods for the Page Class</span></span>

<span data-ttu-id="f3584-291">下列公用方法是 ASP.NET 2.0 中 Page 類別的新功能。</span><span class="sxs-lookup"><span data-stu-id="f3584-291">The following public methods are new to the Page class in ASP.NET 2.0.</span></span>

## <a name="addonprerendercompleteasync"></a><span data-ttu-id="f3584-292">AddOnPreRenderCompleteAsync</span><span class="sxs-lookup"><span data-stu-id="f3584-292">AddOnPreRenderCompleteAsync</span></span>

<span data-ttu-id="f3584-293">這個方法會註冊非同步頁面執行的事件處理常式委派。</span><span class="sxs-lookup"><span data-stu-id="f3584-293">This method registers event handler delegates for asynchronous page execution.</span></span> <span data-ttu-id="f3584-294">本課程模組稍後會討論非同步網頁。</span><span class="sxs-lookup"><span data-stu-id="f3584-294">Asynchronous pages are discussed later in this module.</span></span>

## <a name="applystylesheetskin"></a><span data-ttu-id="f3584-295">ApplyStyleSheetSkin</span><span class="sxs-lookup"><span data-stu-id="f3584-295">ApplyStyleSheetSkin</span></span>

<span data-ttu-id="f3584-296">將頁面樣式表單中的屬性套用至頁面。</span><span class="sxs-lookup"><span data-stu-id="f3584-296">Applies the properties in a pages style sheet to the page.</span></span>

## <a name="executeregisteredasynctasks"></a><span data-ttu-id="f3584-297">ExecuteRegisteredAsyncTasks</span><span class="sxs-lookup"><span data-stu-id="f3584-297">ExecuteRegisteredAsyncTasks</span></span>

<span data-ttu-id="f3584-298">這個方法是非同步工作。</span><span class="sxs-lookup"><span data-stu-id="f3584-298">This method beings an asynchronous task.</span></span>

### <a name="getvalidators"></a><span data-ttu-id="f3584-299">GetValidators</span><span class="sxs-lookup"><span data-stu-id="f3584-299">GetValidators</span></span>

<span data-ttu-id="f3584-300">傳回指定之驗證群組的驗證程式集合，如果未指定，則傳回預設的驗證群組。</span><span class="sxs-lookup"><span data-stu-id="f3584-300">Returns a collection of validators for the specified validation group or the default validation group if none is specified.</span></span>

## <a name="registerasynctask"></a><span data-ttu-id="f3584-301">RegisterAsyncTask</span><span class="sxs-lookup"><span data-stu-id="f3584-301">RegisterAsyncTask</span></span>

<span data-ttu-id="f3584-302">這個方法會註冊新的非同步工作。</span><span class="sxs-lookup"><span data-stu-id="f3584-302">This method registers a new async task.</span></span> <span data-ttu-id="f3584-303">此課程模組稍後會涵蓋非同步頁面。</span><span class="sxs-lookup"><span data-stu-id="f3584-303">Asynchronous pages are covered later in this module.</span></span>

## <a name="registerrequirescontrolstate"></a><span data-ttu-id="f3584-304">RegisterRequiresControlState</span><span class="sxs-lookup"><span data-stu-id="f3584-304">RegisterRequiresControlState</span></span>

<span data-ttu-id="f3584-305">這個方法會告訴 ASP.NET，必須保存頁面控制項狀態。</span><span class="sxs-lookup"><span data-stu-id="f3584-305">This method tells ASP.NET that the pages control state must be persisted.</span></span>

## <a name="registerrequiresviewstateencryption"></a><span data-ttu-id="f3584-306">RegisterRequiresViewStateEncryption</span><span class="sxs-lookup"><span data-stu-id="f3584-306">RegisterRequiresViewStateEncryption</span></span>

<span data-ttu-id="f3584-307">這個方法會告訴 ASP.NET 網頁 viewstate 需要加密。</span><span class="sxs-lookup"><span data-stu-id="f3584-307">This method tells ASP.NET that the pages viewstate requires encryption.</span></span>

## <a name="resolveclienturl"></a><span data-ttu-id="f3584-308">ResolveClientUrl</span><span class="sxs-lookup"><span data-stu-id="f3584-308">ResolveClientUrl</span></span>

<span data-ttu-id="f3584-309">傳回可用於用戶端要求影像等的相對 URL。</span><span class="sxs-lookup"><span data-stu-id="f3584-309">Returns a relative URL that can be used for client requests for images, etc.</span></span>

## <a name="setfocus"></a><span data-ttu-id="f3584-310">SetFocus</span><span class="sxs-lookup"><span data-stu-id="f3584-310">SetFocus</span></span>

<span data-ttu-id="f3584-311">這個方法會將焦點設定為一開始載入頁面時所指定的控制項。</span><span class="sxs-lookup"><span data-stu-id="f3584-311">This method will set the focus to the control that is specified when the page is initially loaded.</span></span>

## <a name="unregisterrequirescontrolstate"></a><span data-ttu-id="f3584-312">UnregisterRequiresControlState</span><span class="sxs-lookup"><span data-stu-id="f3584-312">UnregisterRequiresControlState</span></span>

<span data-ttu-id="f3584-313">這個方法會取消註冊傳遞給它的控制項，因為不再需要控制項狀態持續性。</span><span class="sxs-lookup"><span data-stu-id="f3584-313">This method will unregister the control that is passed to it as no longer requiring control state persistence.</span></span>

## <a name="changes-to-the-page-lifecycle"></a><span data-ttu-id="f3584-314">頁面生命週期的變更</span><span class="sxs-lookup"><span data-stu-id="f3584-314">Changes to the Page Lifecycle</span></span>

<span data-ttu-id="f3584-315">ASP.NET 2.0 中的頁面生命週期並未大幅變更，但有一些您應該注意的新方法。</span><span class="sxs-lookup"><span data-stu-id="f3584-315">The page lifecycle in ASP.NET 2.0 hasn't changed dramatically, but there are some new methods that you should be aware of.</span></span> <span data-ttu-id="f3584-316">ASP.NET 2.0 頁面生命週期如下所述。</span><span class="sxs-lookup"><span data-stu-id="f3584-316">The ASP.NET 2.0 page lifecycle is outlined below.</span></span>

## <a name="preinit-new-in-aspnet-20"></a><span data-ttu-id="f3584-317">PreInit （ASP.NET 2.0 中的新功能）</span><span class="sxs-lookup"><span data-stu-id="f3584-317">PreInit (New in ASP.NET 2.0)</span></span>

<span data-ttu-id="f3584-318">PreInit 事件是開發人員可以存取之生命週期中的最早階段。</span><span class="sxs-lookup"><span data-stu-id="f3584-318">The PreInit event is the earliest stage in the lifecycle that a developer can access.</span></span> <span data-ttu-id="f3584-319">新增此事件可讓您以程式設計方式變更 ASP.NET 2.0 主題、主版頁面、ASP.NET 2.0 設定檔的存取屬性等等。如果您處於回傳狀態，請務必瞭解 Viewstate 在生命週期的這個階段尚未套用到控制項。</span><span class="sxs-lookup"><span data-stu-id="f3584-319">The addition of this event makes it possible to programmatically change ASP.NET 2.0 themes, master pages, access properties for an ASP.NET 2.0 profile, etc. If you are in a postback state, its important to realize that Viewstate has not yet been applied to controls at this point in the lifecycle.</span></span> <span data-ttu-id="f3584-320">因此，如果開發人員在這個階段變更控制項的屬性，稍後在頁面生命週期中可能會遭到覆寫。</span><span class="sxs-lookup"><span data-stu-id="f3584-320">Therefore, if a developer changes a property of a control at this stage, it will likely be overwritten later in the pages lifecycle.</span></span>

## <a name="init"></a><span data-ttu-id="f3584-321">Init</span><span class="sxs-lookup"><span data-stu-id="f3584-321">Init</span></span>

<span data-ttu-id="f3584-322">Init 事件尚未從 ASP.NET 1.x 變更。</span><span class="sxs-lookup"><span data-stu-id="f3584-322">The Init event has not changed from ASP.NET 1.x.</span></span> <span data-ttu-id="f3584-323">這是您想要在頁面上讀取或初始化控制項屬性的位置。</span><span class="sxs-lookup"><span data-stu-id="f3584-323">This is where you would want to read or initialize properties of controls on your page.</span></span> <span data-ttu-id="f3584-324">在這個階段，主版頁面、主題等已套用至頁面。</span><span class="sxs-lookup"><span data-stu-id="f3584-324">At this stage, master pages, themes, etc. are already applied to the page.</span></span>

## <a name="initcomplete-new-in-20"></a><span data-ttu-id="f3584-325">InitComplete （2.0 中的新功能）</span><span class="sxs-lookup"><span data-stu-id="f3584-325">InitComplete (New in 2.0)</span></span>

<span data-ttu-id="f3584-326">InitComplete 事件會在頁面初始化階段結束時呼叫。</span><span class="sxs-lookup"><span data-stu-id="f3584-326">The InitComplete event is called at the end of the pages initialization stage.</span></span> <span data-ttu-id="f3584-327">在生命週期的這個階段中，您可以存取頁面上的控制項，但尚未填入其狀態。</span><span class="sxs-lookup"><span data-stu-id="f3584-327">At this point in the lifecycle, you can access controls on the page, but their state has not yet been populated.</span></span>

## <a name="preload-new-in-20"></a><span data-ttu-id="f3584-328">預先載入（2.0 中的新功能）</span><span class="sxs-lookup"><span data-stu-id="f3584-328">PreLoad (New in 2.0)</span></span>

<span data-ttu-id="f3584-329">在套用所有回傳資料之後，以及在頁面\_載入之前，會呼叫此事件。</span><span class="sxs-lookup"><span data-stu-id="f3584-329">This event is called after all postback data has been applied and just prior to Page\_Load.</span></span>

## <a name="load"></a><span data-ttu-id="f3584-330">載入</span><span class="sxs-lookup"><span data-stu-id="f3584-330">Load</span></span>

<span data-ttu-id="f3584-331">Load 事件尚未從 ASP.NET 1.x 變更。</span><span class="sxs-lookup"><span data-stu-id="f3584-331">The Load event has not changed from ASP.NET 1.x.</span></span>

## <a name="loadcomplete-new-in-20"></a><span data-ttu-id="f3584-332">System.web.ui.page.loadcomplete （2.0 中的新功能）</span><span class="sxs-lookup"><span data-stu-id="f3584-332">LoadComplete (New in 2.0)</span></span>

<span data-ttu-id="f3584-333">System.web.ui.page.loadcomplete 事件是頁面載入階段中的最後一個事件。</span><span class="sxs-lookup"><span data-stu-id="f3584-333">The LoadComplete event is the last event in the pages load stage.</span></span> <span data-ttu-id="f3584-334">在這個階段，所有回傳和 viewstate 資料都已套用至頁面。</span><span class="sxs-lookup"><span data-stu-id="f3584-334">At this stage, all postback and viewstate data has been applied to the page.</span></span>

## <a name="prerender"></a><span data-ttu-id="f3584-335">預</span><span class="sxs-lookup"><span data-stu-id="f3584-335">PreRender</span></span>

<span data-ttu-id="f3584-336">如果您想要針對以動態方式新增至頁面的控制項適當地維護 viewstate，則可呈現的事件是最後一個加入它們的機會。</span><span class="sxs-lookup"><span data-stu-id="f3584-336">If you would like for viewstate to be properly maintained for controls that are added to the page dynamically, the PreRender event is the last opportunity to add them.</span></span>

## <a name="prerendercomplete-new-in-20"></a><span data-ttu-id="f3584-337">PreRenderComplete （2.0 中的新功能）</span><span class="sxs-lookup"><span data-stu-id="f3584-337">PreRenderComplete (New in 2.0)</span></span>

<span data-ttu-id="f3584-338">在 PreRenderComplete 階段，所有控制項都已加入至頁面，而且該頁面已準備好呈現。</span><span class="sxs-lookup"><span data-stu-id="f3584-338">At the PreRenderComplete stage, all controls have been added to the page and the page is ready to be rendered.</span></span> <span data-ttu-id="f3584-339">PreRenderComplete 事件是儲存頁面 viewstate 之前引發的最後一個事件。</span><span class="sxs-lookup"><span data-stu-id="f3584-339">The PreRenderComplete event is the last event raised before the pages viewstate is saved.</span></span>

## <a name="savestatecomplete-new-in-20"></a><span data-ttu-id="f3584-340">SaveStateComplete （2.0 中的新功能）</span><span class="sxs-lookup"><span data-stu-id="f3584-340">SaveStateComplete (New in 2.0)</span></span>

<span data-ttu-id="f3584-341">儲存所有頁面 viewstate 和控制項狀態之後，就會立即呼叫 SaveStateComplete 事件。</span><span class="sxs-lookup"><span data-stu-id="f3584-341">The SaveStateComplete event is called immediately after all page viewstate and control state has been saved.</span></span> <span data-ttu-id="f3584-342">這是頁面實際轉譯至瀏覽器前的最後一個事件。</span><span class="sxs-lookup"><span data-stu-id="f3584-342">This is the last event before the page is actually rendered to the browser.</span></span>

## <a name="render"></a><span data-ttu-id="f3584-343">轉譯</span><span class="sxs-lookup"><span data-stu-id="f3584-343">Render</span></span>

<span data-ttu-id="f3584-344">Render 方法自 ASP.NET 1.x 以來並未變更。</span><span class="sxs-lookup"><span data-stu-id="f3584-344">The Render method has not changed since ASP.NET 1.x.</span></span> <span data-ttu-id="f3584-345">這就是 HtmlTextWriter 初始化的位置，而且頁面會轉譯至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="f3584-345">This is where the HtmlTextWriter is initialized and the page is rendered to the browser.</span></span>

## <a name="cross-page-postback-in-aspnet-20"></a><span data-ttu-id="f3584-346">ASP.NET 2.0 中的跨頁面回傳</span><span class="sxs-lookup"><span data-stu-id="f3584-346">Cross-Page Postback in ASP.NET 2.0</span></span>

<span data-ttu-id="f3584-347">在 ASP.NET 1.x 中，回傳必須張貼到相同的頁面。</span><span class="sxs-lookup"><span data-stu-id="f3584-347">In ASP.NET 1.x, postbacks were required to post to the same page.</span></span> <span data-ttu-id="f3584-348">不允許跨頁面回傳。</span><span class="sxs-lookup"><span data-stu-id="f3584-348">Cross-page postbacks were not allowed.</span></span> <span data-ttu-id="f3584-349">ASP.NET 2.0 新增了透過 IButtonControl 介面回傳至不同頁面的功能。</span><span class="sxs-lookup"><span data-stu-id="f3584-349">ASP.NET 2.0 adds the ability to post back to a different page via the IButtonControl interface.</span></span> <span data-ttu-id="f3584-350">除了協力廠商自訂控制項以外，任何會執行新 IButtonControl 介面（Button、LinkButton 和 ImageButton）的控制項，都可以透過使用 PostBackUrl 屬性來利用這項新功能。</span><span class="sxs-lookup"><span data-stu-id="f3584-350">Any control that implements the new IButtonControl interface (Button, LinkButton, and ImageButton in addition to third-party custom controls) can take advantage of this new functionality via the use of the PostBackUrl attribute.</span></span> <span data-ttu-id="f3584-351">下列程式碼顯示會回傳至第二頁的按鈕控制項。</span><span class="sxs-lookup"><span data-stu-id="f3584-351">The following code shows a Button control that posts back to a second page.</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

<span data-ttu-id="f3584-352">當頁面回傳時，可以透過第二頁上的 PreviousPage 屬性來存取起始回傳的網頁。</span><span class="sxs-lookup"><span data-stu-id="f3584-352">When the page is posted back, the Page that initiates the postback is accessible via the PreviousPage property on the second page.</span></span> <span data-ttu-id="f3584-353">此功能是透過新的 WebForm\_DoPostBackWithOptions 用戶端函式來執行，當控制項回傳至不同的頁面時，ASP.NET 2.0 會轉譯至頁面。</span><span class="sxs-lookup"><span data-stu-id="f3584-353">This functionality is implemented via the new WebForm\_DoPostBackWithOptions client-side function that ASP.NET 2.0 renders to the page when a control posts back to a different page.</span></span> <span data-ttu-id="f3584-354">這個 JavaScript 函數是由向用戶端發出腳本的新 WebResource 處理常式所提供。</span><span class="sxs-lookup"><span data-stu-id="f3584-354">This JavaScript function is provided by the new WebResource.axd handler which emits script to the client.</span></span>

<span data-ttu-id="f3584-355">以下影片是跨頁面回傳的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="f3584-355">The video below is a walkthrough of a cross-page postback.</span></span>

![](the-asp-net-2-0-page-model/_static/image2.png)

[<span data-ttu-id="f3584-356">開啟全螢幕影片</span><span class="sxs-lookup"><span data-stu-id="f3584-356">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a><span data-ttu-id="f3584-357">跨頁面回傳的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="f3584-357">More Details on Cross-Page Postbacks</span></span>

### <a name="viewstate"></a><span data-ttu-id="f3584-358">狀態</span><span class="sxs-lookup"><span data-stu-id="f3584-358">Viewstate</span></span>

<span data-ttu-id="f3584-359">您可能已經問自己，您已經在跨頁面回傳案例中，從第一頁看到 viewstate 會發生什麼情況。</span><span class="sxs-lookup"><span data-stu-id="f3584-359">You may have asked yourself already about what happens to the viewstate from the first page in a cross-page postback scenario.</span></span> <span data-ttu-id="f3584-360">畢竟，任何未執行 IPostBackDataHandler 的控制項都會透過 viewstate 保存其狀態，因此若要在跨頁面回傳的第二頁上存取該控制項的屬性，您必須能夠存取該頁面的 viewstate。</span><span class="sxs-lookup"><span data-stu-id="f3584-360">After all, any control that does not implement IPostBackDataHandler will persist its state via viewstate, so to have access to the properties of that control on the second page of a cross-page postback, you must have access to the viewstate for the page.</span></span> <span data-ttu-id="f3584-361">ASP.NET 2.0 會在第二頁中使用新的隱藏欄位（稱為 \_\_PREVIOUSPAGE）來處理此案例。</span><span class="sxs-lookup"><span data-stu-id="f3584-361">ASP.NET 2.0 takes care of this scenario using a new hidden field in the second page called \_\_PREVIOUSPAGE.</span></span> <span data-ttu-id="f3584-362">[\_\_PREVIOUSPAGE 表單] 欄位包含第一個頁面的 viewstate，讓您可以存取第二頁中所有控制項的屬性。</span><span class="sxs-lookup"><span data-stu-id="f3584-362">The \_\_PREVIOUSPAGE form field contains the viewstate for the first page so that you can have access to the properties of all controls in the second page.</span></span>

### <a name="circumventing-findcontrol"></a><span data-ttu-id="f3584-363">規避 FindControl</span><span class="sxs-lookup"><span data-stu-id="f3584-363">Circumventing FindControl</span></span>

<span data-ttu-id="f3584-364">在跨頁面回傳的影片逐步解說中，我使用 FindControl 方法來取得第一個頁面上 TextBox 控制項的參考。</span><span class="sxs-lookup"><span data-stu-id="f3584-364">In the video walkthrough of a cross-page postback, I used the FindControl method to get a reference to the TextBox control on the first page.</span></span> <span data-ttu-id="f3584-365">該方法適用于該用途，但 FindControl 的成本很高，而且需要撰寫額外的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f3584-365">That method works well for that purpose, but FindControl is expensive and it requires writing additional code.</span></span> <span data-ttu-id="f3584-366">幸好，ASP.NET 2.0 針對此用途提供了 FindControl 的替代方案，可在許多案例中使用。</span><span class="sxs-lookup"><span data-stu-id="f3584-366">Fortunately, ASP.NET 2.0 provides an alternative to FindControl for this purpose that will work in many scenarios.</span></span> <span data-ttu-id="f3584-367">PreviousPageType 指示詞可讓您使用 TypeName 或 VirtualPath 屬性，來擁有上一頁的強型別參考。</span><span class="sxs-lookup"><span data-stu-id="f3584-367">The PreviousPageType directive allows you to have a strongly-typed reference to the previous page by using either the TypeName or the VirtualPath attribute.</span></span> <span data-ttu-id="f3584-368">TypeName 屬性可讓您指定前一頁的類型，而 VirtualPath 屬性則可讓您使用虛擬路徑來參考前一頁。</span><span class="sxs-lookup"><span data-stu-id="f3584-368">The TypeName attribute allows you to specify the type of the previous page while the VirtualPath attribute allows you to refer to the previous page using a virtual path.</span></span> <span data-ttu-id="f3584-369">設定 PreviousPageType 指示詞之後，您必須接著使用公用屬性來公開控制項等，以允許存取。</span><span class="sxs-lookup"><span data-stu-id="f3584-369">After you've set the PreviousPageType directive, you must then expose the controls, etc. to which you want to allow access using public properties.</span></span>

## <a name="lab-1-cross-page-postback"></a><span data-ttu-id="f3584-370">實驗室1跨頁面回傳</span><span class="sxs-lookup"><span data-stu-id="f3584-370">Lab 1 Cross-Page Postback</span></span>

<span data-ttu-id="f3584-371">在此實驗室中，您將建立使用 ASP.NET 2.0 新跨頁面回傳功能的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3584-371">In this lab, you will create an application that uses the new cross-page postback functionality of ASP.NET 2.0.</span></span>

1. <span data-ttu-id="f3584-372">開啟 Visual Studio 2005，並建立新的 ASP.NET 網站。</span><span class="sxs-lookup"><span data-stu-id="f3584-372">Open Visual Studio 2005 and create a new ASP.NET Web site.</span></span>
2. <span data-ttu-id="f3584-373">加入名為 page2 的新 Webform。</span><span class="sxs-lookup"><span data-stu-id="f3584-373">Add a new Webform called page2.aspx.</span></span>
3. <span data-ttu-id="f3584-374">在設計檢視中開啟 default.aspx，並新增 [按鈕] 控制項和 [TextBox] 控制項。</span><span class="sxs-lookup"><span data-stu-id="f3584-374">Open the Default.aspx in Design view and add a Button control and a TextBox control.</span></span> 

    1. <span data-ttu-id="f3584-375">為按鈕控制項提供**SubmitButton**的識別碼，並將 TextBox 控制項命名為**UserName**。</span><span class="sxs-lookup"><span data-stu-id="f3584-375">Give the Button control an ID of **SubmitButton** and the TextBox control an ID of **UserName**.</span></span>
    2. <span data-ttu-id="f3584-376">將按鈕的 PostBackUrl 屬性設定為 page2。</span><span class="sxs-lookup"><span data-stu-id="f3584-376">Set the PostBackUrl property of the Button to page2.aspx.</span></span>
4. <span data-ttu-id="f3584-377">在原始檔視圖中開啟 page2。</span><span class="sxs-lookup"><span data-stu-id="f3584-377">Open page2.aspx in Source view.</span></span>
5. <span data-ttu-id="f3584-378">新增 @ PreviousPageType 指示詞，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f3584-378">Add a @ PreviousPageType directive as shown below:</span></span>
6. <span data-ttu-id="f3584-379">將下列程式碼新增至頁面\_載入 page2 的程式碼後置：</span><span class="sxs-lookup"><span data-stu-id="f3584-379">Add the following code to the Page\_Load of page2.aspx's code-behind:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. <span data-ttu-id="f3584-380">按一下 [建立] 功能表上的 [建立] 來建立專案。</span><span class="sxs-lookup"><span data-stu-id="f3584-380">Build the project by clicking on Build on the Build menu.</span></span>
8. <span data-ttu-id="f3584-381">將下列程式碼加入至 default.aspx 的程式碼後置：</span><span class="sxs-lookup"><span data-stu-id="f3584-381">Add the following code to the code-behind for Default.aspx:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. <span data-ttu-id="f3584-382">將 page2 中的頁面\_載入變更為下列內容：</span><span class="sxs-lookup"><span data-stu-id="f3584-382">Change the Page\_Load in page2.aspx to the following:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. <span data-ttu-id="f3584-383">建置專案。</span><span class="sxs-lookup"><span data-stu-id="f3584-383">Build the project.</span></span>
11. <span data-ttu-id="f3584-384">執行專案。</span><span class="sxs-lookup"><span data-stu-id="f3584-384">Run the project.</span></span>
12. <span data-ttu-id="f3584-385">在文字方塊中輸入您的名稱，然後按一下按鈕。</span><span class="sxs-lookup"><span data-stu-id="f3584-385">Enter your name in the TextBox and click the button.</span></span>
13. <span data-ttu-id="f3584-386">結果是什麼？</span><span class="sxs-lookup"><span data-stu-id="f3584-386">What is the result?</span></span>

## <a name="asynchronous-pages-in-aspnet-20"></a><span data-ttu-id="f3584-387">ASP.NET 2.0 中的非同步頁面</span><span class="sxs-lookup"><span data-stu-id="f3584-387">Asynchronous Pages in ASP.NET 2.0</span></span>

<span data-ttu-id="f3584-388">ASP.NET 中的許多爭用問題是因外部呼叫延遲（例如 Web 服務或資料庫呼叫）、檔案 IO 延遲等所造成。針對 ASP.NET 應用程式提出要求時，ASP.NET 會使用其中一個背景工作執行緒來服務該要求。</span><span class="sxs-lookup"><span data-stu-id="f3584-388">Many contention problems in ASP.NET are caused by latency of external calls (such as Web service or database calls), file IO latency, etc. When a request is made against an ASP.NET application, ASP.NET uses one of its worker threads to service that request.</span></span> <span data-ttu-id="f3584-389">該要求會擁有該執行緒，直到要求完成並已傳送回應為止。</span><span class="sxs-lookup"><span data-stu-id="f3584-389">That request owns that thread until the request is complete and the response has been sent.</span></span> <span data-ttu-id="f3584-390">ASP.NET 2.0 藉由新增以非同步方式執行頁面的功能，尋求解決這些類型問題的延遲問題。</span><span class="sxs-lookup"><span data-stu-id="f3584-390">ASP.NET 2.0 seeks to resolve latency issues with these types of issues by adding the capability to execute pages asynchronously.</span></span> <span data-ttu-id="f3584-391">這表示工作者執行緒可以啟動要求，然後將額外的執行交給另一個執行緒，藉此快速返回可用的執行緒集區。</span><span class="sxs-lookup"><span data-stu-id="f3584-391">That means that a worker thread can start the request and then hand off additional execution to another thread, thereby returning to the available thread pool quickly.</span></span> <span data-ttu-id="f3584-392">當檔案 IO、資料庫呼叫等完成時，就會從執行緒集區取得新的執行緒以完成要求。</span><span class="sxs-lookup"><span data-stu-id="f3584-392">When the file IO, database call, etc. has completed, a new thread is obtained from the thread pool to finish the request.</span></span>

<span data-ttu-id="f3584-393">讓頁面以非同步方式執行的第一個步驟，是設定 page 指示詞的**Async**屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f3584-393">The first step in making a page execute asynchronously is to set the **Async** attribute of the page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

<span data-ttu-id="f3584-394">這個屬性會告知 ASP.NET，以執行頁面的 IHttpAsyncHandler。</span><span class="sxs-lookup"><span data-stu-id="f3584-394">This attribute tells ASP.NET to implement the IHttpAsyncHandler for the page.</span></span>

<span data-ttu-id="f3584-395">下一步是在預先呈現之前，在頁面生命週期中的某個點呼叫 AddOnPreRenderCompleteAsync 方法。</span><span class="sxs-lookup"><span data-stu-id="f3584-395">The next step is to call the AddOnPreRenderCompleteAsync method at a point in the lifecycle of the page prior to PreRender.</span></span> <span data-ttu-id="f3584-396">（這個方法通常會在頁面\_載入）中呼叫）。AddOnPreRenderCompleteAsync 方法會採用兩個參數：BeginEventHandler 和 EndEventHandler。</span><span class="sxs-lookup"><span data-stu-id="f3584-396">(This method is typically called in Page\_Load.) The AddOnPreRenderCompleteAsync method takes two parameters; a BeginEventHandler and an EndEventHandler.</span></span> <span data-ttu-id="f3584-397">BeginEventHandler 會傳回 IAsyncResult，然後將它當做參數傳遞給 EndEventHandler。</span><span class="sxs-lookup"><span data-stu-id="f3584-397">The BeginEventHandler returns an IAsyncResult which is then passed as a parameter to the EndEventHandler.</span></span>

<span data-ttu-id="f3584-398">以下影片是非同步網頁要求的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="f3584-398">The video below is a walkthrough of an asynchronous page request.</span></span>

![](the-asp-net-2-0-page-model/_static/image3.png)

[<span data-ttu-id="f3584-399">開啟全螢幕影片</span><span class="sxs-lookup"><span data-stu-id="f3584-399">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> <span data-ttu-id="f3584-400">在 EndEventHandler 完成之前，非同步網頁不會轉譯至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="f3584-400">An async page does not render to the browser until the EndEventHandler has completed.</span></span> <span data-ttu-id="f3584-401">不確定，有些開發人員會將非同步要求視為類似非同步回呼。</span><span class="sxs-lookup"><span data-stu-id="f3584-401">No doubt but that some developers will think of async requests as being similar to async callbacks.</span></span> <span data-ttu-id="f3584-402">請務必瞭解它們不是。</span><span class="sxs-lookup"><span data-stu-id="f3584-402">It's important to realize that they are not.</span></span> <span data-ttu-id="f3584-403">非同步要求的優點是第一個工作者執行緒可以傳回到執行緒集區來服務新的要求，藉此減少因 IO 系結等而造成的爭用。</span><span class="sxs-lookup"><span data-stu-id="f3584-403">The benefit to asynchronous requests is that the first worker thread can be returned to the thread pool to service new requests, thereby reducing contention due to being IO bound, etc.</span></span>

## <a name="script-callbacks-in-aspnet-20"></a><span data-ttu-id="f3584-404">ASP.NET 2.0 中的腳本回呼</span><span class="sxs-lookup"><span data-stu-id="f3584-404">Script Callbacks in ASP.NET 2.0</span></span>

<span data-ttu-id="f3584-405">Web 開發人員一直都在尋求避免與回呼相關聯之閃爍的方式。</span><span class="sxs-lookup"><span data-stu-id="f3584-405">Web developers have always looked for ways to prevent the flickering associated with a callback.</span></span> <span data-ttu-id="f3584-406">在 ASP.NET 1.x 中，SmartNavigation 是避免閃爍的最常見方法，但是 SmartNavigation 會因其在用戶端上的執行複雜度而造成某些開發人員的問題。</span><span class="sxs-lookup"><span data-stu-id="f3584-406">In ASP.NET 1.x, SmartNavigation was the most common method for avoiding flickering, but SmartNavigation caused problems for some developers because of the complexity of its implementation on the client.</span></span> <span data-ttu-id="f3584-407">ASP.NET 2.0 使用腳本回呼解決了這個問題。</span><span class="sxs-lookup"><span data-stu-id="f3584-407">ASP.NET 2.0 addresses this issue with script callbacks.</span></span> <span data-ttu-id="f3584-408">腳本回呼會利用 XMLHttp，透過 JavaScript 對 Web 服務器提出要求。</span><span class="sxs-lookup"><span data-stu-id="f3584-408">Script callbacks utilize XMLHttp to make requests against the Web server via JavaScript.</span></span> <span data-ttu-id="f3584-409">XMLHttp 要求會傳回可透過瀏覽器的 DOM 操作的 XML 資料。</span><span class="sxs-lookup"><span data-stu-id="f3584-409">The XMLHttp request returns XML data that can then be manipulated via the browser's DOM.</span></span> <span data-ttu-id="f3584-410">新的 WebResource 處理常式會向使用者隱藏 XMLHttp 程式碼。</span><span class="sxs-lookup"><span data-stu-id="f3584-410">XMLHttp code is hidden from the user by the new WebResource.axd handler.</span></span>

<span data-ttu-id="f3584-411">若要在 ASP.NET 2.0 中設定腳本回呼，必須執行幾個步驟。</span><span class="sxs-lookup"><span data-stu-id="f3584-411">There are several steps that are necessary in order to configure a script callback in ASP.NET 2.0.</span></span>

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a><span data-ttu-id="f3584-412">步驟1：執行 ICallbackEventHandler 介面</span><span class="sxs-lookup"><span data-stu-id="f3584-412">Step 1 : Implement the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="f3584-413">為了讓 ASP.NET 能夠將您的頁面辨識為參與腳本回呼，您必須執行 ICallbackEventHandler 介面。</span><span class="sxs-lookup"><span data-stu-id="f3584-413">In order for ASP.NET to recognize your page as participating in a script callback, you must implement the ICallbackEventHandler interface.</span></span> <span data-ttu-id="f3584-414">您可以在程式碼後置檔案中執行此動作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f3584-414">You can do this in your code-behind file like so:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

<span data-ttu-id="f3584-415">您也可以使用 @ Implements 指示詞來執行此動作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f3584-415">You can also do this using the @ Implements directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

<span data-ttu-id="f3584-416">使用內嵌 ASP.NET 程式碼時，您通常會使用 @ Implements 指示詞。</span><span class="sxs-lookup"><span data-stu-id="f3584-416">You would typically use the @ Implements directive when using inline ASP.NET code.</span></span>

## <a name="step-2--call-getcallbackeventreference"></a><span data-ttu-id="f3584-417">步驟2：呼叫 GetCallbackEventReference</span><span class="sxs-lookup"><span data-stu-id="f3584-417">Step 2 : Call GetCallbackEventReference</span></span>

<span data-ttu-id="f3584-418">如先前所述，XMLHttp 呼叫會封裝在 WebResource 處理常式中。</span><span class="sxs-lookup"><span data-stu-id="f3584-418">As mentioned previously, the XMLHttp call is encapsulated in the WebResource.axd handler.</span></span> <span data-ttu-id="f3584-419">當您的頁面呈現時，ASP.NET 會將呼叫新增至 WebForm\_DoCallback，這是 WebResource 所提供的用戶端腳本。</span><span class="sxs-lookup"><span data-stu-id="f3584-419">When your page is rendered, ASP.NET will add a call to WebForm\_DoCallback, a client script that is provided by WebResource.axd.</span></span> <span data-ttu-id="f3584-420">WebForm\_DoCallback 函數會取代回呼的 \_\_doPostBack 函式。</span><span class="sxs-lookup"><span data-stu-id="f3584-420">The WebForm\_DoCallback function replaces the \_\_doPostBack function for a callback.</span></span> <span data-ttu-id="f3584-421">請記住，\_\_doPostBack 以程式設計方式在頁面上提交表單。</span><span class="sxs-lookup"><span data-stu-id="f3584-421">Remember that \_\_doPostBack programmatically submits the form on the page.</span></span> <span data-ttu-id="f3584-422">在回呼案例中，您想要避免回傳，因此 \_\_doPostBack 將不會足夠。</span><span class="sxs-lookup"><span data-stu-id="f3584-422">In a callback scenario, you want to prevent a postback, so \_\_doPostBack will not suffice.</span></span>

> [!NOTE]
> <span data-ttu-id="f3584-423">在用戶端腳本回呼案例中，\_\_doPostBack 仍會轉譯至頁面。</span><span class="sxs-lookup"><span data-stu-id="f3584-423">\_\_doPostBack is still rendered to the page in a client script callback scenario.</span></span> <span data-ttu-id="f3584-424">不過，它不會用於回呼。</span><span class="sxs-lookup"><span data-stu-id="f3584-424">However, it's not used for the callback.</span></span>

<span data-ttu-id="f3584-425">WebForm\_DoCallback 用戶端函式的引數是透過伺服器端函數 GetCallbackEventReference 提供，通常會在頁面\_載入中呼叫。</span><span class="sxs-lookup"><span data-stu-id="f3584-425">The arguments for the WebForm\_DoCallback client-side function are provided via the server-side function GetCallbackEventReference which would normally be called in Page\_Load.</span></span> <span data-ttu-id="f3584-426">典型的 GetCallbackEventReference 呼叫可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="f3584-426">A typical call to GetCallbackEventReference might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="f3584-427">在此情況下，cm 是 ClientScriptManager 的實例。</span><span class="sxs-lookup"><span data-stu-id="f3584-427">In this case, cm is an instance of ClientScriptManager.</span></span> <span data-ttu-id="f3584-428">本課程模組稍後會涵蓋 ClientScriptManager 類別。</span><span class="sxs-lookup"><span data-stu-id="f3584-428">The ClientScriptManager class will be covered later in this module.</span></span>

<span data-ttu-id="f3584-429">GetCallbackEventReference 有數個多載版本。</span><span class="sxs-lookup"><span data-stu-id="f3584-429">There are several overloaded versions of GetCallbackEventReference.</span></span> <span data-ttu-id="f3584-430">在此情況下，引數如下所示：</span><span class="sxs-lookup"><span data-stu-id="f3584-430">In this case, the arguments are as follows:</span></span>

`this`

<span data-ttu-id="f3584-431">呼叫 GetCallbackEventReference 之控制項的參考。</span><span class="sxs-lookup"><span data-stu-id="f3584-431">A reference to the control where GetCallbackEventReference is being called.</span></span> <span data-ttu-id="f3584-432">在此情況下，它是頁面本身。</span><span class="sxs-lookup"><span data-stu-id="f3584-432">In this case, it's the page itself.</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

<span data-ttu-id="f3584-433">將從用戶端程式代碼傳遞至伺服器端事件的字串引數。</span><span class="sxs-lookup"><span data-stu-id="f3584-433">A string argument that will be passed from the client-side code to the server-side event.</span></span> <span data-ttu-id="f3584-434">在此情況下，Im 會傳遞名為 ddlCompany 之下拉式清單的值。</span><span class="sxs-lookup"><span data-stu-id="f3584-434">In this case, Im passing the value of a dropdown called ddlCompany.</span></span>

`ShowCompanyName`

<span data-ttu-id="f3584-435">用戶端函式的名稱，將接受來自伺服器端回呼事件的傳回值（字串形式）。</span><span class="sxs-lookup"><span data-stu-id="f3584-435">The name of the client-side function that will accept the return value (as string) from the server-side callback event.</span></span> <span data-ttu-id="f3584-436">只有當伺服器端回呼成功時，才會呼叫這個函式。</span><span class="sxs-lookup"><span data-stu-id="f3584-436">This function will only be called when the server-side callback is successful.</span></span> <span data-ttu-id="f3584-437">因此，為了加強可靠性，通常建議使用 GetCallbackEventReference 的多載版本，它會採用額外的 string 引數來指定在發生錯誤時要執行的用戶端函數名稱。</span><span class="sxs-lookup"><span data-stu-id="f3584-437">Therefore, for the sake of robustness, it is generally recommended to use the overloaded version of GetCallbackEventReference that takes an additional string argument specifying the name of a client-side function to execute in the event of an error.</span></span>

`null`

<span data-ttu-id="f3584-438">代表用戶端函式的字串，該函數會在回呼至伺服器之前起始。</span><span class="sxs-lookup"><span data-stu-id="f3584-438">A string representing a client-side function that it initiated before the callback to the server.</span></span> <span data-ttu-id="f3584-439">在此情況下，沒有這類腳本，因此引數為 null。</span><span class="sxs-lookup"><span data-stu-id="f3584-439">In this case, there is no such script, so the argument is null.</span></span>

`true`

<span data-ttu-id="f3584-440">布林值，指定是否要以非同步方式執行回呼。</span><span class="sxs-lookup"><span data-stu-id="f3584-440">A Boolean specifying whether or not to conduct the callback asynchronously.</span></span>

<span data-ttu-id="f3584-441">在用戶端上對 WebForm\_DoCallback 的呼叫將會傳遞這些引數。</span><span class="sxs-lookup"><span data-stu-id="f3584-441">The call to WebForm\_DoCallback on the client will pass these arguments.</span></span> <span data-ttu-id="f3584-442">因此，當此頁面在用戶端上呈現時，該程式碼看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="f3584-442">Therefore, when this page is rendered on the client, that code will look like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

<span data-ttu-id="f3584-443">請注意，用戶端上的函數簽章有點不同。</span><span class="sxs-lookup"><span data-stu-id="f3584-443">Notice that the signature of the function on the client is a bit different.</span></span> <span data-ttu-id="f3584-444">用戶端函式會傳遞5個字串和一個布林值。</span><span class="sxs-lookup"><span data-stu-id="f3584-444">The client-side function passes 5 strings and a Boolean.</span></span> <span data-ttu-id="f3584-445">其他字串（在上述範例中為 null）包含用戶端函式，會處理來自伺服器端回呼的任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="f3584-445">The additional string (which is null in the above example) contains the client-side function that will handle any errors from the server-side callback.</span></span>

## <a name="step-3--hook-the-client-side-control-event"></a><span data-ttu-id="f3584-446">步驟3：掛上用戶端控制項事件</span><span class="sxs-lookup"><span data-stu-id="f3584-446">Step 3 : Hook the Client-Side Control Event</span></span>

<span data-ttu-id="f3584-447">請注意，上述 GetCallbackEventReference 的傳回值已指派給字串變數。</span><span class="sxs-lookup"><span data-stu-id="f3584-447">Notice that the return value of GetCallbackEventReference above was assigned to a string variable.</span></span> <span data-ttu-id="f3584-448">該字串是用來攔截起始回呼之控制項的用戶端事件。</span><span class="sxs-lookup"><span data-stu-id="f3584-448">That string is used to hook a client-side event for the control that initiates the callback.</span></span> <span data-ttu-id="f3584-449">在此範例中，回呼是由頁面上的下拉式清單起始，所以我想要攔截*OnChange*事件。</span><span class="sxs-lookup"><span data-stu-id="f3584-449">In this example, the callback is initiated by a dropdown on the page, so I want to hook the *OnChange* event.</span></span>

<span data-ttu-id="f3584-450">若要攔截用戶端事件，只需要將處理常式新增至用戶端標記，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f3584-450">To hook the client-side event, simply add a handler to the client-side markup as follows:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

<span data-ttu-id="f3584-451">回想一下， *cbRef*是呼叫 GetCallbackEventReference 的傳回值。</span><span class="sxs-lookup"><span data-stu-id="f3584-451">Recall that *cbRef* is the return value from the call to GetCallbackEventReference.</span></span> <span data-ttu-id="f3584-452">它包含對 WebForm\_DoCallback 的呼叫，如上所示。</span><span class="sxs-lookup"><span data-stu-id="f3584-452">It contains the call to WebForm\_DoCallback that was shown above.</span></span>

## <a name="step-4--register-the-client-side-script"></a><span data-ttu-id="f3584-453">步驟4：註冊用戶端腳本</span><span class="sxs-lookup"><span data-stu-id="f3584-453">Step 4 : Register the Client-Side Script</span></span>

<span data-ttu-id="f3584-454">回想一下，GetCallbackEventReference 的呼叫指定當伺服器端回呼成功時，會執行名為**ShowCompanyName**的用戶端腳本。</span><span class="sxs-lookup"><span data-stu-id="f3584-454">Recall that the call to GetCallbackEventReference specified that a client-side script called **ShowCompanyName** would be executed when the server-side callback succeeds.</span></span> <span data-ttu-id="f3584-455">該腳本必須使用 ClientScriptManager 實例加入至頁面。</span><span class="sxs-lookup"><span data-stu-id="f3584-455">That script needs to be added to the page using a ClientScriptManager instance.</span></span> <span data-ttu-id="f3584-456">（稍後將在此課程模組中討論 ClientScriptManager 類別）。您可以這樣做，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f3584-456">(The ClientScriptManager class will be discussed later in this module.) You do that like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a><span data-ttu-id="f3584-457">步驟5：呼叫 ICallbackEventHandler 介面的方法</span><span class="sxs-lookup"><span data-stu-id="f3584-457">Step 5 : Call the Methods of the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="f3584-458">ICallbackEventHandler 包含兩個您需要在程式碼中執行的方法。</span><span class="sxs-lookup"><span data-stu-id="f3584-458">The ICallbackEventHandler contains two methods that you need to implement in your code.</span></span> <span data-ttu-id="f3584-459">它們是**RaiseCallbackEvent**和**GetCallbackEvent**。</span><span class="sxs-lookup"><span data-stu-id="f3584-459">They are **RaiseCallbackEvent** and **GetCallbackEvent**.</span></span>

<span data-ttu-id="f3584-460">**RaiseCallbackEvent**接受字串做為引數，並不會傳回任何內容。</span><span class="sxs-lookup"><span data-stu-id="f3584-460">**RaiseCallbackEvent** takes a string as an argument and returns nothing.</span></span> <span data-ttu-id="f3584-461">字串引數會從用戶端呼叫傳遞至 WebForm\_DoCallback。</span><span class="sxs-lookup"><span data-stu-id="f3584-461">The string argument is passed from the client-side call to WebForm\_DoCallback.</span></span> <span data-ttu-id="f3584-462">在此情況下，該值是下拉式清單的*value*屬性，稱為 ddlCompany。</span><span class="sxs-lookup"><span data-stu-id="f3584-462">In this case, that value is the *value* attribute of the dropdown called ddlCompany.</span></span> <span data-ttu-id="f3584-463">您的伺服器端程式碼應該放在 RaiseCallbackEvent 方法中。</span><span class="sxs-lookup"><span data-stu-id="f3584-463">Your server-side code should be placed in the RaiseCallbackEvent method.</span></span> <span data-ttu-id="f3584-464">例如，如果您的回呼是對外部資源進行 WebRequest，則該程式碼應該放在 RaiseCallbackEvent 中。</span><span class="sxs-lookup"><span data-stu-id="f3584-464">For example, if your callback is making a WebRequest against an external resource, that code should be placed in RaiseCallbackEvent.</span></span>

<span data-ttu-id="f3584-465">**GetCallbackEvent**負責處理傳回用戶端的回呼。</span><span class="sxs-lookup"><span data-stu-id="f3584-465">**GetCallbackEvent** is responsible for processing the return of the callback to the client.</span></span> <span data-ttu-id="f3584-466">它不接受任何引數，而且會傳回字串。</span><span class="sxs-lookup"><span data-stu-id="f3584-466">It takes no arguments and returns a string.</span></span> <span data-ttu-id="f3584-467">其傳回的字串將會當做引數傳遞至用戶端函式，在此案例中為*ShowCompanyName*。</span><span class="sxs-lookup"><span data-stu-id="f3584-467">The string that it returns will be passed as an argument to the client-side function, in this case *ShowCompanyName*.</span></span>

<span data-ttu-id="f3584-468">完成上述步驟之後，您就可以開始在 ASP.NET 2.0 中執行腳本回呼。</span><span class="sxs-lookup"><span data-stu-id="f3584-468">Once you have completed the above steps, you are ready to perform a script callback in ASP.NET 2.0.</span></span>

![](the-asp-net-2-0-page-model/_static/image4.png)

[<span data-ttu-id="f3584-469">開啟全螢幕影片</span><span class="sxs-lookup"><span data-stu-id="f3584-469">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/callback1.wmv)

<span data-ttu-id="f3584-470">支援進行 XMLHttp 呼叫的任何瀏覽器都支援 ASP.NET 中的腳本回呼。</span><span class="sxs-lookup"><span data-stu-id="f3584-470">Script callbacks in ASP.NET are supported in any browser that supports making XMLHttp calls.</span></span> <span data-ttu-id="f3584-471">這包括現今使用的所有新式瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="f3584-471">That includes all of the modern browsers in use today.</span></span> <span data-ttu-id="f3584-472">Internet Explorer 會使用 XMLHttp ActiveX 物件，而其他現代化的瀏覽器（包括即將推出的 IE 7）則使用內部 XMLHttp 物件。</span><span class="sxs-lookup"><span data-stu-id="f3584-472">Internet Explorer uses the XMLHttp ActiveX object while other modern browsers (including the upcoming IE 7) use an intrinsic XMLHttp object.</span></span> <span data-ttu-id="f3584-473">若要以程式設計方式判斷瀏覽器是否支援回呼，您可以使用**SupportCallback**屬性。</span><span class="sxs-lookup"><span data-stu-id="f3584-473">To programmatically determine if a browser supports callbacks, you can use the **Request.Browser.SupportCallback** property.</span></span> <span data-ttu-id="f3584-474">如果要求的用戶端支援腳本回呼，這個屬性會傳回**true** 。</span><span class="sxs-lookup"><span data-stu-id="f3584-474">This property will return **true** if the requesting client supports script callbacks.</span></span>

## <a name="working-with-client-script-in-aspnet-20"></a><span data-ttu-id="f3584-475">在 ASP.NET 2.0 中使用用戶端腳本</span><span class="sxs-lookup"><span data-stu-id="f3584-475">Working with Client Script in ASP.NET 2.0</span></span>

<span data-ttu-id="f3584-476">ASP.NET 2.0 中的用戶端腳本是透過使用 ClientScriptManager 類別來管理。</span><span class="sxs-lookup"><span data-stu-id="f3584-476">Client scripts in ASP.NET 2.0 are managed via the use of the ClientScriptManager class.</span></span> <span data-ttu-id="f3584-477">ClientScriptManager 類別會使用類型和名稱來追蹤用戶端腳本。</span><span class="sxs-lookup"><span data-stu-id="f3584-477">The ClientScriptManager class keeps track of client scripts using a type and a name.</span></span> <span data-ttu-id="f3584-478">這可防止相同的腳本以程式設計方式在頁面上多次插入。</span><span class="sxs-lookup"><span data-stu-id="f3584-478">This prevents the same script from being programmatically inserted on a page more than once.</span></span>

> [!NOTE]
> <span data-ttu-id="f3584-479">在網頁上成功註冊腳本之後，任何後續嘗試註冊相同的腳本，都只會導致腳本不會第二次註冊。</span><span class="sxs-lookup"><span data-stu-id="f3584-479">After a script has been successfully registered on a page, any subsequent attempt to register the same script will simply result in the script not being registered a second time.</span></span> <span data-ttu-id="f3584-480">不會新增重複的腳本，也不會發生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f3584-480">No duplicate scripts are added and no exception occurs.</span></span> <span data-ttu-id="f3584-481">若要避免不必要的計算，您可以使用一些方法來判斷是否已註冊腳本，讓您不會嘗試多次註冊。</span><span class="sxs-lookup"><span data-stu-id="f3584-481">To avoid unnecessary computation, there are methods that you can use to determine if a script is already registered so that you do not attempt to register it more than once.</span></span>

<span data-ttu-id="f3584-482">所有目前的 ASP.NET 開發人員都應該熟悉 ClientScriptManager 的方法：</span><span class="sxs-lookup"><span data-stu-id="f3584-482">The methods of the ClientScriptManager should be familiar to all current ASP.NET developers:</span></span>

## <a name="registerclientscriptblock"></a><span data-ttu-id="f3584-483">RegisterClientScriptBlock</span><span class="sxs-lookup"><span data-stu-id="f3584-483">RegisterClientScriptBlock</span></span>

<span data-ttu-id="f3584-484">這個方法會將腳本加入轉譯頁面的頂端。</span><span class="sxs-lookup"><span data-stu-id="f3584-484">This method adds a script to the top of the rendered page.</span></span> <span data-ttu-id="f3584-485">這適用于新增將在用戶端上明確呼叫的函式。</span><span class="sxs-lookup"><span data-stu-id="f3584-485">This is useful for adding functions that will be explicitly called on the client.</span></span>

<span data-ttu-id="f3584-486">這個方法有兩個多載版本。</span><span class="sxs-lookup"><span data-stu-id="f3584-486">There are two overloaded versions of this method.</span></span> <span data-ttu-id="f3584-487">四個引數中有三個是常見的。</span><span class="sxs-lookup"><span data-stu-id="f3584-487">Three of four arguments are common among them.</span></span> <span data-ttu-id="f3584-488">包括：</span><span class="sxs-lookup"><span data-stu-id="f3584-488">They are:</span></span>

`type (string)`

<span data-ttu-id="f3584-489">***型***別引數可識別腳本的型別。</span><span class="sxs-lookup"><span data-stu-id="f3584-489">The ***type*** argument identifies a type for the script.</span></span> <span data-ttu-id="f3584-490">通常最好是使用頁面的類型（這個）。類型的 GetType （））。</span><span class="sxs-lookup"><span data-stu-id="f3584-490">It is generally a good idea to use the page's type (this.GetType()) for the type.</span></span>

`key (string)`

<span data-ttu-id="f3584-491">***Key***引數是腳本的使用者定義索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f3584-491">The ***key*** argument is a user-defined key for the script.</span></span> <span data-ttu-id="f3584-492">這對於每個腳本而言都是唯一的。</span><span class="sxs-lookup"><span data-stu-id="f3584-492">This should be unique for each script.</span></span> <span data-ttu-id="f3584-493">如果您嘗試加入的腳本具有與已加入之腳本相同的索引鍵和類型，則不會新增它。</span><span class="sxs-lookup"><span data-stu-id="f3584-493">If you attempt to add a script with the same key and type of an already added script, it will not be added.</span></span>

`script (string)`

<span data-ttu-id="f3584-494">***腳本***引數是一個字串，其中包含要加入的實際腳本。</span><span class="sxs-lookup"><span data-stu-id="f3584-494">The ***script*** argument is a string containing the actual script to add.</span></span> <span data-ttu-id="f3584-495">建議您使用 StringBuilder 來建立腳本，然後在 StringBuilder 上使用 ToString （）方法來指派***腳本***引數。</span><span class="sxs-lookup"><span data-stu-id="f3584-495">It's recommended that you use a StringBuilder to create the script and then use the ToString() method on the StringBuilder to assign the ***script*** argument.</span></span>

<span data-ttu-id="f3584-496">如果您使用只接受三個引數的多載 RegisterClientScriptBlock，您必須在腳本中包含 script 元素（&lt;腳本&gt; 和 &lt;/script&gt;）。</span><span class="sxs-lookup"><span data-stu-id="f3584-496">If you use the overloaded RegisterClientScriptBlock that only takes three arguments, you must include script elements (&lt;script&gt; and &lt;/script&gt;) in your script.</span></span>

<span data-ttu-id="f3584-497">您可以選擇使用採用第四個引數的 RegisterClientScriptBlock 多載。</span><span class="sxs-lookup"><span data-stu-id="f3584-497">You may choose to use the overload of RegisterClientScriptBlock that takes a fourth argument.</span></span> <span data-ttu-id="f3584-498">第四個引數是布林值，指定 ASP.NET 是否應該為您加入腳本元素。</span><span class="sxs-lookup"><span data-stu-id="f3584-498">The fourth argument is a Boolean that specifies whether or not ASP.NET should add script elements for you.</span></span> <span data-ttu-id="f3584-499">如果這個引數為**true**，則您的腳本不應明確包含腳本元素。</span><span class="sxs-lookup"><span data-stu-id="f3584-499">If this argument is **true**, your script should not include the script elements explicitly.</span></span>

<span data-ttu-id="f3584-500">使用 IsClientScriptBlockRegistered 方法來判斷腳本是否已註冊。</span><span class="sxs-lookup"><span data-stu-id="f3584-500">Use the IsClientScriptBlockRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="f3584-501">這可讓您避免嘗試重新註冊已註冊的腳本。</span><span class="sxs-lookup"><span data-stu-id="f3584-501">This allows you to avoid an attempt to re-register a script that has already been registered.</span></span>

### <a name="registerclientscriptinclude-new-in-20"></a><span data-ttu-id="f3584-502">RegisterClientScriptInclude （2.0 中的新功能）</span><span class="sxs-lookup"><span data-stu-id="f3584-502">RegisterClientScriptInclude (New in 2.0)</span></span>

<span data-ttu-id="f3584-503">RegisterClientScriptInclude 標記會建立連結至外部腳本檔案的腳本區塊。</span><span class="sxs-lookup"><span data-stu-id="f3584-503">The RegisterClientScriptInclude tag creates a script block that links to an external script file.</span></span> <span data-ttu-id="f3584-504">它有兩個多載。</span><span class="sxs-lookup"><span data-stu-id="f3584-504">It has two overloads.</span></span> <span data-ttu-id="f3584-505">其中一個會接受一個金鑰和一個 URL。</span><span class="sxs-lookup"><span data-stu-id="f3584-505">One takes a key and a URL.</span></span> <span data-ttu-id="f3584-506">第二個會加入指定類型的第三個引數。</span><span class="sxs-lookup"><span data-stu-id="f3584-506">The second adds a third argument specifying the type.</span></span>

<span data-ttu-id="f3584-507">例如，下列程式碼會產生一個腳本區塊，它會連結至應用程式之 scripts 資料夾根目錄中的 jsfunctions：</span><span class="sxs-lookup"><span data-stu-id="f3584-507">For example, the following code generates a script block that links to jsfunctions.js in the root of the scripts folder of the application:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

<span data-ttu-id="f3584-508">此程式碼會在呈現的頁面中產生下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="f3584-508">This code produces the following code in the rendered page:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> <span data-ttu-id="f3584-509">腳本區塊會呈現在頁面底部。</span><span class="sxs-lookup"><span data-stu-id="f3584-509">The script block is rendered at the bottom of the page.</span></span>

<span data-ttu-id="f3584-510">使用 IsClientScriptIncludeRegistered 方法來判斷腳本是否已註冊。</span><span class="sxs-lookup"><span data-stu-id="f3584-510">Use the IsClientScriptIncludeRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="f3584-511">這可讓您避免嘗試重新註冊腳本。</span><span class="sxs-lookup"><span data-stu-id="f3584-511">This allows you to avoid an attempt to re-register a script.</span></span>

## <a name="registerstartupscript"></a><span data-ttu-id="f3584-512">RegisterStartupScript</span><span class="sxs-lookup"><span data-stu-id="f3584-512">RegisterStartupScript</span></span>

<span data-ttu-id="f3584-513">RegisterStartupScript 方法會採用與 RegisterClientScriptBlock 方法相同的引數。</span><span class="sxs-lookup"><span data-stu-id="f3584-513">The RegisterStartupScript method takes the same arguments as the RegisterClientScriptBlock method.</span></span> <span data-ttu-id="f3584-514">向 RegisterStartupScript 註冊的腳本會在頁面載入之後，但在 OnLoad 用戶端事件之前執行。</span><span class="sxs-lookup"><span data-stu-id="f3584-514">A script registered with RegisterStartupScript executes after the page loads but before the OnLoad client-side event.</span></span> <span data-ttu-id="f3584-515">在1.x 中，使用 RegisterStartupScript 註冊的腳本會放在結尾 &lt;/form&gt; 標記之前，而向 RegisterClientScriptBlock 註冊的腳本會緊接在開頭 &lt;表單&gt; 標記之後。</span><span class="sxs-lookup"><span data-stu-id="f3584-515">In 1.X, scripts registered with RegisterStartupScript were placed just before the closing &lt;/form&gt; tag while scripts registered with RegisterClientScriptBlock were placed immediately after the opening &lt;form&gt; tag.</span></span> <span data-ttu-id="f3584-516">在 ASP.NET 2.0 中，這兩個都會緊接在結尾 &lt;/form&gt; 標記之前。</span><span class="sxs-lookup"><span data-stu-id="f3584-516">In ASP.NET 2.0, both are placed immediately before the closing &lt;/form&gt; tag.</span></span>

> [!NOTE]
> <span data-ttu-id="f3584-517">如果您向 RegisterStartupScript 註冊函式，該函式將不會執行，直到您在用戶端程式代碼中明確呼叫它為止。</span><span class="sxs-lookup"><span data-stu-id="f3584-517">If you register a function with RegisterStartupScript, that function will not execute until you explicitly call it in client-side code.</span></span>

<span data-ttu-id="f3584-518">使用 IsStartupScriptRegistered 方法來判斷腳本是否已註冊，並避免嘗試重新註冊腳本。</span><span class="sxs-lookup"><span data-stu-id="f3584-518">Use the IsStartupScriptRegistered method to determine if a script has already been registered and avoid an attempt to re-register a script.</span></span>

## <a name="other-clientscriptmanager-methods"></a><span data-ttu-id="f3584-519">其他 ClientScriptManager 方法</span><span class="sxs-lookup"><span data-stu-id="f3584-519">Other ClientScriptManager Methods</span></span>

<span data-ttu-id="f3584-520">以下是 ClientScriptManager 類別的一些其他實用方法。</span><span class="sxs-lookup"><span data-stu-id="f3584-520">Here are some of the other useful methods of the ClientScriptManager class.</span></span>

|  <span data-ttu-id="f3584-521"><strong>GetCallbackEventReference</strong></span><span class="sxs-lookup"><span data-stu-id="f3584-521"><strong>GetCallbackEventReference</strong></span></span>   |                                                 <span data-ttu-id="f3584-522">請參閱稍早在此課程模組中的腳本回呼。</span><span class="sxs-lookup"><span data-stu-id="f3584-522">See script callbacks earlier in this module.</span></span>                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <span data-ttu-id="f3584-523"><strong>GetPostBackClientHyperlink</strong></span><span class="sxs-lookup"><span data-stu-id="f3584-523"><strong>GetPostBackClientHyperlink</strong></span></span>  |                <span data-ttu-id="f3584-524">取得 JavaScript 參考（javascript：&lt;呼叫&gt;），可以用來從用戶端事件回傳。</span><span class="sxs-lookup"><span data-stu-id="f3584-524">Gets a JavaScript reference (javascript:&lt;call&gt;) that can be used to post back from a client-side event.</span></span>                 |
|  <span data-ttu-id="f3584-525"><strong>GetPostBackEventReference</strong></span><span class="sxs-lookup"><span data-stu-id="f3584-525"><strong>GetPostBackEventReference</strong></span></span>   |                                   <span data-ttu-id="f3584-526">取得可用於從用戶端起始回傳的字串。</span><span class="sxs-lookup"><span data-stu-id="f3584-526">Gets a string that can be used to initiate a post back from the client.</span></span>                                    |
|      <span data-ttu-id="f3584-527"><strong>GetWebResourceUrl</strong></span><span class="sxs-lookup"><span data-stu-id="f3584-527"><strong>GetWebResourceUrl</strong></span></span>       | <span data-ttu-id="f3584-528">傳回內嵌于元件中之資源的 URL。</span><span class="sxs-lookup"><span data-stu-id="f3584-528">Returns a URL to a resource that is embedded in an assembly.</span></span> <span data-ttu-id="f3584-529">必須與<strong>RegisterClientScriptResource</strong>搭配使用。</span><span class="sxs-lookup"><span data-stu-id="f3584-529">Must be used in conjunction with <strong>RegisterClientScriptResource</strong>.</span></span> |
| <span data-ttu-id="f3584-530"><strong>RegisterClientScriptResource</strong></span><span class="sxs-lookup"><span data-stu-id="f3584-530"><strong>RegisterClientScriptResource</strong></span></span> |     <span data-ttu-id="f3584-531">向頁面註冊 Web 資源。</span><span class="sxs-lookup"><span data-stu-id="f3584-531">Registers a Web resource with the page.</span></span> <span data-ttu-id="f3584-532">這些是內嵌在元件中，並由新的 WebResource 處理常式所處理的資源。</span><span class="sxs-lookup"><span data-stu-id="f3584-532">These are resources embedded in an assembly and handled by the new WebResource.axd handler.</span></span>      |
|     <span data-ttu-id="f3584-533"><strong>RegisterHiddenField</strong></span><span class="sxs-lookup"><span data-stu-id="f3584-533"><strong>RegisterHiddenField</strong></span></span>      |                                                 <span data-ttu-id="f3584-534">向頁面註冊隱藏的表單欄位。</span><span class="sxs-lookup"><span data-stu-id="f3584-534">Registers a hidden form field with the page.</span></span>                                                 |
|  <span data-ttu-id="f3584-535"><strong>RegisterOnSubmitStatement</strong></span><span class="sxs-lookup"><span data-stu-id="f3584-535"><strong>RegisterOnSubmitStatement</strong></span></span>   |                                  <span data-ttu-id="f3584-536">註冊在提交 HTML 表單時執行的用戶端程式代碼。</span><span class="sxs-lookup"><span data-stu-id="f3584-536">Registers client-side code that executes when the HTML form is submitted.</span></span>                                   |
