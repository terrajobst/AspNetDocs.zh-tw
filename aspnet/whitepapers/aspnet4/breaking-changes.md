---
uid: whitepapers/aspnet4/breaking-changes
title: ASP.NET 4 重大變更 |Microsoft Docs
author: rick-anderson
description: 本檔說明 .NET Framework 版本4版本所做的變更，可能會影響使用建立的應用程式 。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d601c540-f86b-4feb-890c-20c806b3da6c
msc.legacyurl: /whitepapers/aspnet4/breaking-changes
msc.type: content
ms.openlocfilehash: 8ccad3b40a723c92a3164de082e1f94577141008
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78546246"
---
# <a name="aspnet-4-breaking-changes"></a><span data-ttu-id="f2767-103">ASP.NET 4 重大變更</span><span class="sxs-lookup"><span data-stu-id="f2767-103">ASP.NET 4 Breaking Changes</span></span>

> <span data-ttu-id="f2767-104">本檔說明 .NET Framework 版本4版本所做的變更，可能會影響使用舊版所建立的應用程式，包括 ASP.NET 4 Beta 1 和 Beta 2 版本。</span><span class="sxs-lookup"><span data-stu-id="f2767-104">This document describes changes that have been made for the .NET Framework version 4 release that can potentially affect applications that were created using earlier releases, including the ASP.NET 4 Beta 1 and Beta 2 releases.</span></span>
> 
> [<span data-ttu-id="f2767-105">下載此白皮書</span><span class="sxs-lookup"><span data-stu-id="f2767-105">Download This Whitepaper</span></span>](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_Breaking_Changes.pdf)

<a id="0.1__Toc256768952"></a><a id="0.1__Toc256770056"></a>

## <a name="contents"></a><span data-ttu-id="f2767-106">內容</span><span class="sxs-lookup"><span data-stu-id="f2767-106">Contents</span></span>

[<span data-ttu-id="f2767-107">Web.config 檔案中的 ControlRenderingCompatibilityVersion 設定</span><span class="sxs-lookup"><span data-stu-id="f2767-107">ControlRenderingCompatibilityVersion Setting in the Web.config File</span></span>](#0.1__Toc256770141 "_Toc256770141")  
[<span data-ttu-id="f2767-108">ClientIDMode 變更</span><span class="sxs-lookup"><span data-stu-id="f2767-108">ClientIDMode Changes</span></span>](#0.1__Toc256770142 "_Toc256770142")  
[<span data-ttu-id="f2767-109">HtmlEncode 和 UrlEncode 現在會將單引號編碼</span><span class="sxs-lookup"><span data-stu-id="f2767-109">HtmlEncode and UrlEncode Now Encode Single Quotation Marks</span></span>](#0.1__Toc256770143 "_Toc256770143")  
[<span data-ttu-id="f2767-110">ASP.NET Page （.aspx）剖析器較嚴格</span><span class="sxs-lookup"><span data-stu-id="f2767-110">ASP.NET Page (.aspx) Parser is Stricter</span></span>](#0.1__Toc256770144 "_Toc256770144")  
[<span data-ttu-id="f2767-111">已更新瀏覽器定義檔案</span><span class="sxs-lookup"><span data-stu-id="f2767-111">Browser Definition Files Updated</span></span>](#0.1__Toc256770145 "_Toc256770145")  
[<span data-ttu-id="f2767-112">從根 Web 設定檔案移除的 system.web. .dll</span><span class="sxs-lookup"><span data-stu-id="f2767-112">System.Web.Mobile.dll Removed from Root Web Configuration File</span></span>](#0.1__Toc256770146 "_Toc256770146")  
[<span data-ttu-id="f2767-113">ASP.NET 要求驗證</span><span class="sxs-lookup"><span data-stu-id="f2767-113">ASP.NET Request Validation</span></span>](#0.1__Toc256770147 "_Toc256770147")  
[<span data-ttu-id="f2767-114">預設雜湊演算法現已 HMACSHA256</span><span class="sxs-lookup"><span data-stu-id="f2767-114">Default Hashing Algorithm Is Now HMACSHA256</span></span>](#0.1__Toc256770148 "_Toc256770148")  
[<span data-ttu-id="f2767-115">與新的 ASP.NET 4 根設定相關的設定錯誤</span><span class="sxs-lookup"><span data-stu-id="f2767-115">Configuration Errors Related to New ASP.NET 4 Root Configuration</span></span>](#0.1__Toc256770149 "_Toc256770149")  
[<span data-ttu-id="f2767-116">ASP.NET 4 子應用程式在 ASP.NET 2.0 或 ASP.NET 3.5 應用程式下無法啟動</span><span class="sxs-lookup"><span data-stu-id="f2767-116">ASP.NET 4 Child Applications Fail to Start When Under ASP.NET 2.0 or ASP.NET 3.5 Applications</span></span>](#0.1__Toc256770150 "_Toc256770150")  
[<span data-ttu-id="f2767-117">ASP.NET 4 網站在安裝 SharePoint 的電腦上無法啟動</span><span class="sxs-lookup"><span data-stu-id="f2767-117">ASP.NET 4 Web Sites Fail to Start on Computers Where SharePoint Is Installed</span></span>](#0.1__Toc256770151 "_Toc256770151")  
[<span data-ttu-id="f2767-118">HttpRequest 的屬性不再包含 PathInfo 值</span><span class="sxs-lookup"><span data-stu-id="f2767-118">The HttpRequest.FilePath Property No Longer Includes PathInfo Values</span></span>](#0.1__Toc256770152 "_Toc256770152")  
[<span data-ttu-id="f2767-119">ASP.NET 2.0 應用程式可能會產生參考 eurl 的 HttpException 錯誤</span><span class="sxs-lookup"><span data-stu-id="f2767-119">ASP.NET 2.0 Applications Might Generate HttpException Errors that Reference eurl.axd</span></span>](#0.1__Toc256770153 "_Toc256770153")  
[<span data-ttu-id="f2767-120">事件處理常式可能不會在 IIS 7 或 IIS 7.5 整合模式的預設檔中引發</span><span class="sxs-lookup"><span data-stu-id="f2767-120">Event Handlers Might Not Be Not Raised in a Default Document in IIS 7 or IIS 7.5 Integrated Mode</span></span>](#0.1__Toc256770154 "_Toc256770154")  
[<span data-ttu-id="f2767-121">對 ASP.NET 代碼啟用安全性（CAS）實行的變更</span><span class="sxs-lookup"><span data-stu-id="f2767-121">Changes to the ASP.NET Code Access Security (CAS) Implementation</span></span>](#0.1__Toc256770155 "_Toc256770155")  
[<span data-ttu-id="f2767-122">MembershipUser 和 System.web. Security 命名空間中的其他類型已移動</span><span class="sxs-lookup"><span data-stu-id="f2767-122">MembershipUser and Other Types in the System.Web.Security Namespace Have Been Moved</span></span>](#0.1__Toc256770156 "_Toc256770156")  
[<span data-ttu-id="f2767-123">輸出快取變更為不同的 \* HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="f2767-123">Output Caching Changes to Vary \* HTTP Header</span></span>](#0.1__Toc256770157 "_Toc256770157")  
[<span data-ttu-id="f2767-124">Passport 的安全性類型已過時</span><span class="sxs-lookup"><span data-stu-id="f2767-124">System.Web.Security Types for Passport are Obsolete</span></span>](#0.1__Toc256770158 "_Toc256770158")  
[<span data-ttu-id="f2767-125">PopOutImageUrl 屬性無法轉譯 ASP.NET 4 中的影像</span><span class="sxs-lookup"><span data-stu-id="f2767-125">The MenuItem.PopOutImageUrl Property Fails to Render an Image in ASP.NET 4</span></span>](#0.1__Toc256770159 "_Toc256770159")  
[<span data-ttu-id="f2767-126">StaticPopOutImageUrl 和 Menu. DynamicPopOutImageUrl 無法在路徑包含反斜線時呈現影像</span><span class="sxs-lookup"><span data-stu-id="f2767-126">Menu.StaticPopOutImageUrl and Menu.DynamicPopOutImageUrl Fail to Render Images When Paths Contain Backslashes</span></span>](#0.1__Toc256770160 "_Toc256770160")  
[<span data-ttu-id="f2767-127">免責聲明</span><span class="sxs-lookup"><span data-stu-id="f2767-127">Disclaimer</span></span>](#0.1__Toc256770161 "_Toc256770161")

<a id="0.1__ControlRenderingCompatibilityVersio"></a><a id="0.1__Toc245724853"></a><a id="0.1__Toc255587630"></a><a id="0.1__Toc256770141"></a>

## <a name="controlrenderingcompatibilityversion-setting-in-the-webconfig-file"></a><span data-ttu-id="f2767-128">Web.config 檔案中的 ControlRenderingCompatibilityVersion 設定</span><span class="sxs-lookup"><span data-stu-id="f2767-128">ControlRenderingCompatibilityVersion Setting in the Web.config File</span></span>

<span data-ttu-id="f2767-129">ASP.NET 控制項在 .NET Framework 第4版中已經過修改，可讓您更精確地指定它們呈現標記的方式。</span><span class="sxs-lookup"><span data-stu-id="f2767-129">ASP.NET controls have been modified in the .NET Framework version 4 in order to let you specify more precisely how they render markup.</span></span> <span data-ttu-id="f2767-130">在舊版的 .NET Framework 中，有些控制項發出的標記是您無法停用的。</span><span class="sxs-lookup"><span data-stu-id="f2767-130">In previous versions of the .NET Framework, some controls emitted markup that you had no way to disable.</span></span> <span data-ttu-id="f2767-131">根據預設，ASP.NET 4 不會再產生這種類型的標記。</span><span class="sxs-lookup"><span data-stu-id="f2767-131">By default, ASP.NET 4 this type of markup is no longer generated.</span></span>

<span data-ttu-id="f2767-132">如果您使用 Visual Studio 2010 從 ASP.NET 2.0 或 ASP.NET 3.5 升級您的應用程式，此工具會自動將設定新增至保留舊版轉譯的 `Web.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="f2767-132">If you use Visual Studio 2010 to upgrade your application from ASP.NET 2.0 or ASP.NET 3.5, the tool automatically adds a setting to the `Web.config` file that preserves legacy rendering.</span></span> <span data-ttu-id="f2767-133">不過，如果您將 IIS 中的應用程式集區變更成以.NET Framework 4 為目標來升級應用程式，則 ASP.NET 預設會使用新轉譯模式。</span><span class="sxs-lookup"><span data-stu-id="f2767-133">However, if you upgrade an application by changing the application pool in IIS to target the .NET Framework 4, ASP.NET uses the new rendering mode by default.</span></span> <span data-ttu-id="f2767-134">若要停用新的轉譯模式，請在 `Web.config` 檔案中新增下列設定：</span><span class="sxs-lookup"><span data-stu-id="f2767-134">To disable the new rendering mode, add the following setting in the `Web.config` file:</span></span>

[!code-xml[Main](breaking-changes/samples/sample1.xml)]

<span data-ttu-id="f2767-135">新行為所帶入的主要呈現變更如下所示：</span><span class="sxs-lookup"><span data-stu-id="f2767-135">The major rendering changes that the new behavior brings are as follows:</span></span>

- <span data-ttu-id="f2767-136">**影像**和**ImageButton**控制項不再呈現 `border="0"` 屬性。</span><span class="sxs-lookup"><span data-stu-id="f2767-136">The **Image** and **ImageButton** controls no longer render a `border="0"` attribute.</span></span>
- <span data-ttu-id="f2767-137">根據預設，衍生自它的**BaseValidator**類別和驗證控制項不會再轉譯紅色文字。</span><span class="sxs-lookup"><span data-stu-id="f2767-137">The **BaseValidator** class and validation controls that derive from it no longer render red text by default.</span></span>
- <span data-ttu-id="f2767-138">**HtmlForm**控制項不會呈現**name**屬性。</span><span class="sxs-lookup"><span data-stu-id="f2767-138">The **HtmlForm** control does not render a **name** attribute.</span></span>
- <span data-ttu-id="f2767-139">**資料表**控制項不再呈現 `border="0"` 屬性。</span><span class="sxs-lookup"><span data-stu-id="f2767-139">The **Table** control no longer renders a `border="0"` attribute.</span></span>
- <span data-ttu-id="f2767-140">如果控制項的 [ **Enabled** ] 屬性設定為**false** （或從容器控制項繼承此設定），則不是針對使用者輸入（例如， **Label**控制項）所設計的控制項就不會再轉譯 `disabled="disabled"` 屬性。</span><span class="sxs-lookup"><span data-stu-id="f2767-140">Controls that are not designed for user input (for example, the **Label** control) no longer render the `disabled="disabled"` attribute if their **Enabled** property is set to **false** (or if they inherit this setting from a container control).</span></span>

<a id="0.1__Toc245724854"></a><a id="0.1__Toc255587631"></a><a id="0.1__Toc256770142"></a>

## <a name="clientidmode-changes"></a><span data-ttu-id="f2767-141">ClientIDMode 變更</span><span class="sxs-lookup"><span data-stu-id="f2767-141">ClientIDMode Changes</span></span>

<span data-ttu-id="f2767-142">ASP.NET 4 中的**ClientIDMode**設定可讓您指定 ASP.NET 如何產生 HTML 元素的**id**屬性。</span><span class="sxs-lookup"><span data-stu-id="f2767-142">The **ClientIDMode** setting in ASP.NET 4 lets you specify how ASP.NET generates the **id** attribute for HTML elements.</span></span> <span data-ttu-id="f2767-143">在舊版的 ASP.NET 中，預設行為相當於**ClientIDMode**的**autoid predictable**設定。</span><span class="sxs-lookup"><span data-stu-id="f2767-143">In previous versions of ASP.NET, the default behavior was equivalent to the **AutoID** setting of **ClientIDMode**.</span></span> <span data-ttu-id="f2767-144">不過，預設設定現在是**可預測**的。</span><span class="sxs-lookup"><span data-stu-id="f2767-144">However, the default setting is now **Predictable**.</span></span>

<span data-ttu-id="f2767-145">如果您使用 Visual Studio 2010 從 ASP.NET 2.0 或 ASP.NET 3.5 升級您的應用程式，此工具會自動將設定新增至 `Web.config` 檔案，以保留舊版 .NET Framework 的行為。</span><span class="sxs-lookup"><span data-stu-id="f2767-145">If you use Visual Studio 2010 to upgrade your application from ASP.NET 2.0 or ASP.NET 3.5, the tool automatically adds a setting to the `Web.config` file that preserves the behavior of earlier versions of the .NET Framework.</span></span> <span data-ttu-id="f2767-146">不過，如果您將 IIS 中的應用程式集區變更成以.NET Framework 4 為目標來升級應用程式，則 ASP.NET 預設會使用新模式。</span><span class="sxs-lookup"><span data-stu-id="f2767-146">However, if you upgrade an application by changing the application pool in IIS to target the .NET Framework 4, ASP.NET uses the new mode by default.</span></span> <span data-ttu-id="f2767-147">若要停用新的用戶端識別碼模式，請在 `Web.config` 檔案中新增下列設定：</span><span class="sxs-lookup"><span data-stu-id="f2767-147">To disable the new client ID mode, add the following setting in the `Web.config` file:</span></span>

[!code-xml[Main](breaking-changes/samples/sample2.xml)]

<a id="0.1__Toc245724855"></a><a id="0.1__Toc255587632"></a><a id="0.1__Toc256770143"></a>

## <a name="htmlencode-and-urlencode-now-encode-single-quotation-marks"></a><span data-ttu-id="f2767-148">HtmlEncode 和 UrlEncode 現在會將單引號編碼</span><span class="sxs-lookup"><span data-stu-id="f2767-148">HtmlEncode and UrlEncode Now Encode Single Quotation Marks</span></span>

<span data-ttu-id="f2767-149">在 ASP.NET 4 中， **HTTPutility.htmlencode**和**HttpServerUtility**類別的**HtmlEncode**和**UrlEncode**方法已更新為將單引號字元（'）編碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f2767-149">In ASP.NET 4, the **HtmlEncode** and **UrlEncode** methods of the **HttpUtility** and **HttpServerUtility** classes have been updated to encode the single quotation mark character (') as follows:</span></span>

- <span data-ttu-id="f2767-150">**HtmlEncode**方法會將單引號的實例編碼為 '。</span><span class="sxs-lookup"><span data-stu-id="f2767-150">The **HtmlEncode** method encodes instances of the single quotation mark as ' .</span></span>
- <span data-ttu-id="f2767-151">**UrlEncode**方法會將單引號的實例編碼為 %27。</span><span class="sxs-lookup"><span data-stu-id="f2767-151">The **UrlEncode** method encodes instances of the single quotation mark as %27.</span></span>

<a id="0.1__Toc255587633"></a><a id="0.1__Toc256770144"></a><a id="0.1__Toc245724856"></a>

## <a name="aspnet-page-aspx-parser-is-stricter"></a><span data-ttu-id="f2767-152">ASP.NET Page （.aspx）剖析器較嚴格</span><span class="sxs-lookup"><span data-stu-id="f2767-152">ASP.NET Page (.aspx) Parser is Stricter</span></span>

<span data-ttu-id="f2767-153">ASP.NET 網頁（`.aspx` 檔案）和使用者控制項（`.ascx` 檔案）的頁面剖析器在 ASP.NET 4 中更嚴格，而且將會拒絕無效標記的更多實例。</span><span class="sxs-lookup"><span data-stu-id="f2767-153">The page parser for ASP.NET pages (`.aspx` files) and user controls (`.ascx` files) is stricter in ASP.NET 4 and will reject more instances of invalid markup.</span></span> <span data-ttu-id="f2767-154">例如，下列兩個程式碼片段會在舊版的 ASP.NET 中成功剖析，但現在會在 ASP.NET 4 中引發剖析器錯誤。</span><span class="sxs-lookup"><span data-stu-id="f2767-154">For example, the following two snippets would successfully parse in earlier releases of ASP.NET, but will now raise parser errors in ASP.NET 4.</span></span>

[!code-aspx[Main](breaking-changes/samples/sample3.aspx)]

<span data-ttu-id="f2767-155">請注意**HiddenField**標記結尾的無效分號。</span><span class="sxs-lookup"><span data-stu-id="f2767-155">Notice the invalid semicolon at the end of the **HiddenField** tag.</span></span>

[!code-aspx[Main](breaking-changes/samples/sample4.aspx)]

<span data-ttu-id="f2767-156">請注意，在**CssClass**屬性中執行的未封閉**樣式**屬性。</span><span class="sxs-lookup"><span data-stu-id="f2767-156">Notice the unclosed **style** attribute that runs into the **CssClass** attribute.</span></span>

<a id="0.1__Toc255587634"></a><a id="0.1__Toc256770145"></a>

## <a name="browser-definition-files-updated"></a><span data-ttu-id="f2767-157">已更新瀏覽器定義檔案</span><span class="sxs-lookup"><span data-stu-id="f2767-157">Browser Definition Files Updated</span></span>

<span data-ttu-id="f2767-158">瀏覽器定義檔已更新成包含新增和已更新瀏覽器及裝置的資訊。</span><span class="sxs-lookup"><span data-stu-id="f2767-158">The browser definition files have been updated to include information about new and updated browsers and devices.</span></span> <span data-ttu-id="f2767-159">已移除 Netscape Navigator 這類較舊的瀏覽器和裝置，並已新增 Google Chrome 和 Apple iPhone 這類較新的瀏覽器和裝置。</span><span class="sxs-lookup"><span data-stu-id="f2767-159">Older browsers and devices such as Netscape Navigator have been removed, and newer browsers and devices such as Google Chrome and Apple iPhone have been added.</span></span>

<span data-ttu-id="f2767-160">如果您的應用程式包含繼承自其中一個已移除瀏覽器定義的自訂瀏覽器定義，則您會看到錯誤。</span><span class="sxs-lookup"><span data-stu-id="f2767-160">If your application contains custom browser definitions that inherit from one of the browser definitions that have been removed, you will see an error.</span></span> <span data-ttu-id="f2767-161">例如，如果 [`App_Browsers`] 資料夾包含繼承自 IE2 瀏覽器定義的瀏覽器定義，您將會收到下列設定錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="f2767-161">For example, if the `App_Browsers` folder contains a browser definition that inherits from the IE2 browser definition, you will receive the following configuration error message:</span></span>

- <span data-ttu-id="f2767-162">找不到識別碼為 ' IE2 ' 的瀏覽器或閘道元素。</span><span class="sxs-lookup"><span data-stu-id="f2767-162">The browser or gateway element with ID 'IE2' cannot be found.</span></span>

> [!NOTE]
> <span data-ttu-id="f2767-163">**HttpBrowserCapabilities**物件（由頁面的 [**要求流覽**] 屬性公開）是由瀏覽器定義檔案所驅動。</span><span class="sxs-lookup"><span data-stu-id="f2767-163">The **HttpBrowserCapabilities** object (which is exposed by the page's **Request.Browser** property) is driven by the browser definitions files.</span></span> <span data-ttu-id="f2767-164">因此，在 ASP.NET 4 中存取此物件的屬性所傳回的資訊，可能會與舊版 ASP.NET 中傳回的資訊不同。</span><span class="sxs-lookup"><span data-stu-id="f2767-164">Therefore, the information returned by accessing a property of this object in ASP.NET 4 might be different than the information returned in an earlier version of ASP.NET.</span></span>

<span data-ttu-id="f2767-165">您可以從下列資料夾複製瀏覽器定義檔案，以還原成舊的瀏覽器定義檔案：</span><span class="sxs-lookup"><span data-stu-id="f2767-165">You can revert to the old browser definition files by copying the browser definition files from the following folder:</span></span>

[!code-console[Main](breaking-changes/samples/sample5.cmd)]

<span data-ttu-id="f2767-166">將檔案複製到 ASP.NET 4 的對應 `\CONFIG\Browsers` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f2767-166">Copy the files into the corresponding `\CONFIG\Browsers` folder for ASP.NET 4.</span></span> <span data-ttu-id="f2767-167">複製檔案之後，請執行 Aspnet\_regbrowsers 命令列工具。</span><span class="sxs-lookup"><span data-stu-id="f2767-167">After you copy the files, run the Aspnet\_regbrowsers.exe command-line tool.</span></span>

<a id="0.1__Toc255587635"></a><a id="0.1__Toc256770146"></a>

## <a name="systemwebmobiledll-removed-from-root-web-configuration-file"></a><span data-ttu-id="f2767-168">從根 Web 設定檔案移除的 system.web. .dll</span><span class="sxs-lookup"><span data-stu-id="f2767-168">System.Web.Mobile.dll Removed from Root Web Configuration File</span></span>

<span data-ttu-id="f2767-169">在舊版的 ASP.NET 中，在底下的**元件**區段中，根 `Web.config` 檔案中會包含 system.web. .dll 元件的參考。</span><span class="sxs-lookup"><span data-stu-id="f2767-169">In previous versions of ASP.NET, a reference to the System.Web.Mobile.dll assembly was included in the root `Web.config` file in the **assemblies** section under.</span></span> <span data-ttu-id="f2767-170">為了改善效能，已移除此元件的參考。</span><span class="sxs-lookup"><span data-stu-id="f2767-170">In order to improve performance, the reference to this assembly was removed.</span></span>

<span data-ttu-id="f2767-171">ASP.NET 4 包含 system.servicemodel 元件，但它已被取代。</span><span class="sxs-lookup"><span data-stu-id="f2767-171">The System.Web.Mobile.dll assembly is included in ASP.NET 4, but it is deprecated.</span></span> <span data-ttu-id="f2767-172">如果您想要使用 system.servicemodel 元件中的類型，請將此元件的參考新增至根 `Web.config` 檔案或應用程式 `Web.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="f2767-172">If you want to use types from the System.Web.Mobile.dll assembly, add a reference to this assembly to either the root `Web.config` file or to an application `Web.config` file.</span></span> <span data-ttu-id="f2767-173">例如，如果您想要使用任何（已淘汰）的 ASP.NET mobile 控制項，則必須將 System.web 元件的參考加入至 `Web.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="f2767-173">For example, if you want to use any of the (deprecated) ASP.NET mobile controls, you must add a reference to the System.Web.Mobile.dll assembly to the `Web.config` file.</span></span>

<a id="0.1__Toc245724857"></a><a id="0.1__Toc255587636"></a><a id="0.1__Toc256770147"></a>

## <a name="aspnet-request-validation"></a><span data-ttu-id="f2767-174">ASP.NET 要求驗證</span><span class="sxs-lookup"><span data-stu-id="f2767-174">ASP.NET Request Validation</span></span>

<span data-ttu-id="f2767-175">ASP.NET 中的要求驗證功能會針對跨網站腳本（XSS）攻擊提供特定層級的預設保護。</span><span class="sxs-lookup"><span data-stu-id="f2767-175">The request validation feature in ASP.NET provides a certain level of default protection against cross-site scripting (XSS) attacks.</span></span> <span data-ttu-id="f2767-176">在舊版的 ASP.NET 中，預設會啟用要求驗證。</span><span class="sxs-lookup"><span data-stu-id="f2767-176">In previous versions of ASP.NET, request validation was enabled by default.</span></span> <span data-ttu-id="f2767-177">不過，它只會套用至 ASP.NET 網頁（`.aspx` 檔案及其類別檔案），而且只會套用至這些頁面執行時。</span><span class="sxs-lookup"><span data-stu-id="f2767-177">However, it applied only to ASP.NET pages (`.aspx` files and their class files) and only when those pages were executing.</span></span>

<span data-ttu-id="f2767-178">在 ASP.NET 4 中，預設會針對所有要求啟用要求驗證，因為它是在 HTTP 要求的**BeginRequest**階段之前啟用。</span><span class="sxs-lookup"><span data-stu-id="f2767-178">In ASP.NET 4, by default, request validation is enabled for all requests, because it is enabled before the **BeginRequest** phase of an HTTP request.</span></span> <span data-ttu-id="f2767-179">因此，要求驗證會套用至所有 ASP.NET 資源的要求，而不只是 .aspx 頁面要求。</span><span class="sxs-lookup"><span data-stu-id="f2767-179">As a result, request validation applies to requests for all ASP.NET resources, not just .aspx page requests.</span></span> <span data-ttu-id="f2767-180">這包括像是 Web 服務呼叫和自訂 HTTP 處理常式之類的要求。</span><span class="sxs-lookup"><span data-stu-id="f2767-180">This includes requests such as Web service calls and custom HTTP handlers.</span></span> <span data-ttu-id="f2767-181">當自訂 HTTP 模組讀取 HTTP 要求的內容時，要求驗證也是作用中。</span><span class="sxs-lookup"><span data-stu-id="f2767-181">Request validation is also active when custom HTTP modules are reading the contents of an HTTP request.</span></span>

<span data-ttu-id="f2767-182">因此，先前未觸發錯誤的要求，現在可能會發生要求驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="f2767-182">As a result, request validation errors might now occur for requests that previously did not trigger errors.</span></span> <span data-ttu-id="f2767-183">若要還原為 ASP.NET 2.0 要求驗證功能的行為，請在 `Web.config` 檔案中新增下列設定：</span><span class="sxs-lookup"><span data-stu-id="f2767-183">To revert to the behavior of the ASP.NET 2.0 request validation feature, add the following setting in the `Web.config` file:</span></span>

[!code-xml[Main](breaking-changes/samples/sample6.xml)]

<span data-ttu-id="f2767-184">不過，我們建議您分析任何要求驗證錯誤，以判斷現有處理常式、模組或其他自訂程式碼是否會存取可能為 XSS 攻擊媒介的潛在不安全 HTTP 輸入。</span><span class="sxs-lookup"><span data-stu-id="f2767-184">However, we recommend that you analyze any request validation errors to determine whether existing handlers, modules, or other custom code accesses potentially unsafe HTTP inputs that could be XSS attack vectors.</span></span>

<a id="0.1__Toc245724858"></a><a id="0.1__Toc255587637"></a><a id="0.1__Toc256770148"></a>

## <a name="default-hashing-algorithm-is-now-hmacsha256"></a><span data-ttu-id="f2767-185">預設雜湊演算法現已 HMACSHA256</span><span class="sxs-lookup"><span data-stu-id="f2767-185">Default Hashing Algorithm Is Now HMACSHA256</span></span>

<span data-ttu-id="f2767-186">ASP.NET 使用加密和雜湊演算法來協助保護資料，例如表單驗證 Cookie 和檢視狀態。</span><span class="sxs-lookup"><span data-stu-id="f2767-186">ASP.NET uses both encryption and hashing algorithms to help secure data such as forms authentication cookies and view state.</span></span> <span data-ttu-id="f2767-187">根據預設，ASP.NET 4 現在會針對 cookie 和 view 狀態的雜湊作業使用 HMACSHA256 演算法。</span><span class="sxs-lookup"><span data-stu-id="f2767-187">By default, ASP.NET 4 now uses the HMACSHA256 algorithm for hash operations on cookies and view state.</span></span> <span data-ttu-id="f2767-188">較早版本的 ASP.NET 使用較舊的 HMACSHA1 演算法。</span><span class="sxs-lookup"><span data-stu-id="f2767-188">Earlier versions of ASP.NET used the older HMACSHA1 algorithm.</span></span>

<span data-ttu-id="f2767-189">如果您執行混合 ASP.NET 2.0/ASP. NET 4 環境，例如表單驗證 cookie 的資料必須使用 across.NET Framework 版本，您的應用程式可能會受到影響。</span><span class="sxs-lookup"><span data-stu-id="f2767-189">Your applications might be affected if you run mixed ASP.NET 2.0/ASP.NET 4 environments where data such as forms authentication cookies must work across.NET Framework versions.</span></span> <span data-ttu-id="f2767-190">若要將 ASP.NET 4 Web 應用程式設定為使用較舊的 HMACSHA1 演算法，請在 `Web.config` 檔案中新增下列設定：</span><span class="sxs-lookup"><span data-stu-id="f2767-190">To configure an ASP.NET 4 Web application to use the older HMACSHA1 algorithm, add the following setting in the `Web.config` file:</span></span>

[!code-xml[Main](breaking-changes/samples/sample7.xml)]

<a id="0.1__Toc245724859"></a><a id="0.1__Toc255587638"></a><a id="0.1__Toc256770149"></a>

## <a name="configuration-errors-related-to-new-aspnet-4-root-configuration"></a><span data-ttu-id="f2767-191">與新的 ASP.NET 4 根設定相關的設定錯誤</span><span class="sxs-lookup"><span data-stu-id="f2767-191">Configuration Errors Related to New ASP.NET 4 Root Configuration</span></span>

<span data-ttu-id="f2767-192">.NET Framework 4 （因此 ASP.NET 4）的根設定檔案（`machine.config` 檔案和根 `Web.config` 檔案）已經更新，以包含在應用程式 `Web.config` 檔案中找到的大部分 ASP.NET 3.5 中的重複使用設定資訊。</span><span class="sxs-lookup"><span data-stu-id="f2767-192">The root configuration files (the `machine.config` file and the root `Web.config` file) for the .NET Framework 4 (and therefore ASP.NET 4) have been updated to include most of the boilerplate configuration information that in ASP.NET 3.5 was found in the application `Web.config` files.</span></span> <span data-ttu-id="f2767-193">由於受管理的 IIS 7 和 IIS 7.5 設定系統的複雜性，在 ASP.NET 4 和 iis 7 和 IIS 7.5 下執行 ASP.NET 3.5 應用程式可能會導致 ASP.NET 或 IIS 設定錯誤。</span><span class="sxs-lookup"><span data-stu-id="f2767-193">Because of the complexity of the managed IIS 7 and IIS 7.5 configuration systems, running ASP.NET 3.5 applications under ASP.NET 4 and under IIS 7 and IIS 7.5 can result in either ASP.NET or IIS configuration errors.</span></span>

<span data-ttu-id="f2767-194">我們建議您在實際情況下，使用 Visual Studio 2010 中的專案升級工具，將 ASP.NET 3.5 應用程式升級至 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="f2767-194">We recommend that you upgrade ASP.NET 3.5 applications to ASP.NET 4 by using the project upgrade tools in Visual Studio 2010, if practical.</span></span> <span data-ttu-id="f2767-195">Visual Studio 2010 會自動修改 ASP.NET 3.5 應用程式的 `Web.config` 檔，使其包含 ASP.NET 4 的適當設定。</span><span class="sxs-lookup"><span data-stu-id="f2767-195">Visual Studio 2010 automatically modifies the ASP.NET 3.5 application's `Web.config` file to contain the appropriate settings for ASP.NET 4.</span></span>

<span data-ttu-id="f2767-196">不過，使用 .NET Framework 4 來執行 ASP.NET 3.5 應用程式不需要重新編譯，這是支援的案例。</span><span class="sxs-lookup"><span data-stu-id="f2767-196">However, it is a supported scenario to run ASP.NET 3.5 applications using the .NET Framework 4 without recompilation.</span></span> <span data-ttu-id="f2767-197">在這種情況下，您可能必須先手動修改應用程式的 `Web.config` 檔，然後才能在 .NET Framework 4 和 IIS 7 或 IIS 7.5 下執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2767-197">In that case, you might have to manually modify the application's `Web.config` file before you run the application under the .NET Framework 4 and under IIS 7 or IIS 7.5.</span></span>

<span data-ttu-id="f2767-198">接下來的兩節說明您可能需要針對不同的軟體組合進行的變更。</span><span class="sxs-lookup"><span data-stu-id="f2767-198">The next two sections describe changes that you might need to make for different combinations of software.</span></span>

<span data-ttu-id="f2767-199">**Windows Vista SP1 或 Windows Server 2008 SP1，其中不會安裝任何修補程式 KB958854 或 SP2。**</span><span class="sxs-lookup"><span data-stu-id="f2767-199">**Windows Vista SP1 or Windows Server 2008 SP1, where neither hotfix KB958854 nor SP2 are installed.**</span></span> <span data-ttu-id="f2767-200">在此設定中，IIS 7 設定系統會藉由比較應用層級的 `Web.config` 檔案與 ASP.NET 2.0 `machine.config` 檔，來不正確地合併應用程式的受管理設定。</span><span class="sxs-lookup"><span data-stu-id="f2767-200">In this configuration, the IIS 7 configuration system incorrectly merges an application's managed configuration by comparing the application-level `Web.config` file to the ASP.NET 2.0 `machine.config` files.</span></span> <span data-ttu-id="f2767-201">因此，來自 .NET Framework 3.5 或更新版本的應用層級 `Web.config` 檔案必須有**system.web 副檔名**設定區段定義（元素），才不會導致 IIS 7 驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="f2767-201">Because of this, application-level `Web.config` files from the .NET Framework 3.5 or later must have a **system.web.extensions** configuration section definition (the element) in order not to cause an IIS 7 validation failure.</span></span>

<span data-ttu-id="f2767-202">不過，手動修改的應用層級 `Web.config` 檔案專案若未精確符合 Visual Studio 2008 引進的原始樣板設定區段定義，則會導致 ASP.NET 設定錯誤。</span><span class="sxs-lookup"><span data-stu-id="f2767-202">However, manually modified application-level `Web.config` file entries that do not precisely match the original boilerplate configuration section definitions that were introduced with Visual Studio 2008 will cause ASP.NET configuration errors.</span></span> <span data-ttu-id="f2767-203">（Visual Studio 2008 產生的預設設定專案會正常運作）。常見的問題是，手動修改 `Web.config` 檔案會省略在各種設定區段定義上找到的**allowDefinition**和**requirePermission**設定屬性。</span><span class="sxs-lookup"><span data-stu-id="f2767-203">(The default configuration entries that are generated by Visual Studio 2008 work correctly.) A common problem is that manually modified `Web.config` files leave out the **allowDefinition** and **requirePermission** configuration attributes that are found on various configuration section definitions.</span></span> <span data-ttu-id="f2767-204">這會導致應用層級 `Web.config` 檔案中的縮寫設定區段與 ASP.NET 4 `machine.config` 檔案中的完整定義不相符。</span><span class="sxs-lookup"><span data-stu-id="f2767-204">This causes a mismatch between the abbreviated configuration section in application-level `Web.config` files and the complete definition in the ASP.NET 4 `machine.config` file.</span></span> <span data-ttu-id="f2767-205">因此，在執行時間，ASP.NET 4 設定系統會擲回設定錯誤。</span><span class="sxs-lookup"><span data-stu-id="f2767-205">As a result, at run time, the ASP.NET 4 configuration system throws a configuration error.</span></span>

<span data-ttu-id="f2767-206">**Windows Vista SP2、Windows Server 2008 SP2、Windows 7、Windows Server 2008 R2 以及 Windows Vista SP1 和 Windows Server 2008 SP1，其中安裝了「修正程式 KB958854。**</span><span class="sxs-lookup"><span data-stu-id="f2767-206">**Windows Vista SP2, Windows Server 2008 SP2, Windows 7, Windows Server 2008 R2, and also Windows Vista SP1 and Windows Server 2008 SP1 where hotfix KB958854 is installed.**</span></span>

<span data-ttu-id="f2767-207">在此案例中，IIS 7 和 IIS 7.5 原生設定系統會傳回設定錯誤，因為它會對針對 managed 設定區段處理常式所定義的**類型**屬性執行文字比較。</span><span class="sxs-lookup"><span data-stu-id="f2767-207">In this scenario, the IIS 7 and IIS 7.5 native configuration system returns a configuration error because it performs a text comparison on the **type** attribute that is defined for a managed configuration section handler.</span></span> <span data-ttu-id="f2767-208">因為 Visual Studio 2008 和 Visual Studio 2008 SP1 所產生的所有 `Web.config` 檔案在系統的類型字串中都有 "3.5" **。網頁副檔名**（和相關）設定區段處理常式，而且由於 ASP.NET 4 `machine.config` 檔案在相同設定區段處理常式的**type**屬性中具有 "4.0"，所以在 Visual Studio 2008 或 Visual Studio 2008 SP1 中產生的應用程式一律會在 iis 7 和 iis 7.5 中失敗設定驗證。</span><span class="sxs-lookup"><span data-stu-id="f2767-208">Because all `Web.config` files that are generated by Visual Studio 2008 and Visual Studio 2008 SP1 have "3.5" in the type string for the **system.web.extensions** (and related) configuration section handlers, and because the ASP.NET 4 `machine.config` file has "4.0" in the **type** attribute for the same configuration section handlers, applications that are generated in Visual Studio 2008 or Visual Studio 2008 SP1 always fail configuration validation in IIS 7 and IIS 7.5.</span></span>

<a id="0.1__Toc251910248"></a>

### <a name="resolving-these-issues"></a><span data-ttu-id="f2767-209">解決這些問題</span><span class="sxs-lookup"><span data-stu-id="f2767-209">Resolving These Issues</span></span>

<span data-ttu-id="f2767-210">第一個案例的因應措施是藉由在 Visual Studio 2008 自動產生的 `Web.config` 檔案中包含未定案設定文字，以更新應用層級 `Web.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="f2767-210">The workaround for the first scenario is to update the application-level `Web.config` file by including the boilerplate configuration text from a `Web.config` file that was generated automatically by Visual Studio 2008.</span></span>

<span data-ttu-id="f2767-211">第一個案例的替代因應措施是在您的電腦上安裝適用于 Vista 或 Windows Server 2008 的 Service Pack 2，或安裝 fix KB958854 （[https://support.microsoft.com/kb/958854](https://support.microsoft.com/kb/958854)），以修正 IIS 設定系統的不正確設定合併行為。</span><span class="sxs-lookup"><span data-stu-id="f2767-211">An alternative workaround for the first scenario is to install Service Pack 2 for Vista or Windows Server 2008 on your computer or to install hotfix KB958854 ([https://support.microsoft.com/kb/958854](https://support.microsoft.com/kb/958854)) to fix the incorrect configuration-merge behavior of the IIS configuration system.</span></span> <span data-ttu-id="f2767-212">不過，在您執行上述任一動作之後，您的應用程式可能會因為第二個案例所述的問題而遇到設定錯誤。</span><span class="sxs-lookup"><span data-stu-id="f2767-212">However, after you perform either of these actions, your application will likely encounter a configuration error due to the issue described for the second scenario.</span></span>

<span data-ttu-id="f2767-213">第二個案例的因應措施是從應用層級的 `Web.config` 檔中，刪除或批註所有的**system.web. extensions**設定區段定義和 configuration 區段群組定義。</span><span class="sxs-lookup"><span data-stu-id="f2767-213">The workaround for the second scenario is to delete or comment out all the **system.web.extensions** configuration section definitions and configuration section group definitions from the application-level `Web.config` file.</span></span> <span data-ttu-id="f2767-214">這些定義通常位於應用層級 `Web.config` 檔案的頂端，而且可以由**configSections**元素和其子系加以識別。</span><span class="sxs-lookup"><span data-stu-id="f2767-214">These definitions are usually at the top of the application-level `Web.config` file and can be identified by the **configSections** element and its children.</span></span>

<span data-ttu-id="f2767-215">在這兩種情況下，建議您也手動刪除**system.object**區段，雖然這不是必要的。</span><span class="sxs-lookup"><span data-stu-id="f2767-215">For both scenarios, it is recommended that you also manually delete the **system.codedom** section, although this is not required.</span></span>

<a id="0.1__Toc252995490"></a><a id="0.1__Toc255587639"></a><a id="0.1__Toc256770150"></a><a id="0.1__Toc245724860"></a>

## <a name="aspnet-4-child-applications-fail-to-start-when-under-aspnet-20-or-aspnet-35-applications"></a><span data-ttu-id="f2767-216">ASP.NET 4 子應用程式在 ASP.NET 2.0 或 ASP.NET 3.5 應用程式下無法啟動</span><span class="sxs-lookup"><span data-stu-id="f2767-216">ASP.NET 4 Child Applications Fail to Start When Under ASP.NET 2.0 or ASP.NET 3.5 Applications</span></span>

<span data-ttu-id="f2767-217">因為發生組態或編譯錯誤，所以可能無法啟動設定為執行舊版 ASP.NET 之應用程式子系的 ASP.NET 4 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2767-217">ASP.NET 4 applications that are configured as children of applications that run earlier versions of ASP.NET might fail to start because of configuration or compilation errors.</span></span> <span data-ttu-id="f2767-218">下列範例顯示受影響應用程式的目錄結構。</span><span class="sxs-lookup"><span data-stu-id="f2767-218">The following example shows a directory structure for an affected application.</span></span>

<span data-ttu-id="f2767-219">`/parentwebapp` （設定為使用 ASP.NET 2.0 或 ASP.NET 3.5）</span><span class="sxs-lookup"><span data-stu-id="f2767-219">`/parentwebapp` (configured to use ASP.NET 2.0 or ASP.NET 3.5)</span></span>  
<span data-ttu-id="f2767-220">`/childwebapp` （設定為使用 ASP.NET 4）</span><span class="sxs-lookup"><span data-stu-id="f2767-220">`/childwebapp` (configured to use ASP.NET 4)</span></span>

<span data-ttu-id="f2767-221">[`childwebapp`] 資料夾中的應用程式將無法在 IIS 7 或 IIS 7.5 上啟動，並且會報告設定錯誤。</span><span class="sxs-lookup"><span data-stu-id="f2767-221">The application in the `childwebapp` folder will fail to start on IIS 7 or IIS 7.5 and will report a configuration error.</span></span> <span data-ttu-id="f2767-222">錯誤文字將包含類似下面的訊息：</span><span class="sxs-lookup"><span data-stu-id="f2767-222">The error text will include a message similar to the following:</span></span>

- `The requested page cannot be accessed because the related configuration data for the page is invalid.`

- `The configuration section 'configSections' cannot be read because it is missing a section declaration.`

<span data-ttu-id="f2767-223">在 IIS 6 上，[`childwebapp`] 資料夾中的應用程式也將無法啟動，但它會報告不同的錯誤。</span><span class="sxs-lookup"><span data-stu-id="f2767-223">On IIS 6, the application in the `childwebapp` folder will also fail to start, but it will report a different error.</span></span> <span data-ttu-id="f2767-224">例如，錯誤文字可能會陳述下列內容：</span><span class="sxs-lookup"><span data-stu-id="f2767-224">For example, the error text might state the following:</span></span>

- `The value for the 'compilerVersion' attribute in the provider options must be 'v4.0' or later if you are compiling for version 4.0 or later of the .NET Framework. To compile this Web application for version 3.5 or earlier of the .NET Framework, remove the 'targetFramework' attribute from the element of the Web.config file`

<span data-ttu-id="f2767-225">發生這些狀況的原因是，來自 [`parentwebapp`] 資料夾中父應用程式的設定資訊是設定資訊階層的一部分，可決定 [`childwebapp`] 資料夾中子 web 應用程式所使用的最終合併設定。</span><span class="sxs-lookup"><span data-stu-id="f2767-225">These scenarios occur because the configuration information from the parent application in the `parentwebapp` folder is part of the hierarchy of configuration information that determines the final merged configuration settings that are used by the child web application in the `childwebapp` folder.</span></span> <span data-ttu-id="f2767-226">根據 ASP.NET 4 Web 應用程式是在 IIS 7 （或 IIS 7.5）還是在 IIS 6 上執行，IIS 設定系統或 ASP.NET 4 編譯系統會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="f2767-226">Depending on whether the ASP.NET 4 Web application is running on IIS 7 (or IIS 7.5) or on IIS 6, either the IIS configuration system or the ASP.NET 4 compilation system will return an error.</span></span>

<span data-ttu-id="f2767-227">您必須遵循這些步驟來解決此問題，並讓子 ASP.NET 4 應用程式運作，取決於 ASP.NET 4 應用程式是在 IIS 6 或 IIS 7 （或 IIS 7.5）上執行。</span><span class="sxs-lookup"><span data-stu-id="f2767-227">The steps that you must follow to resolve this issue and to get the child ASP.NET 4 application to work depend on whether the ASP.NET 4 application runs on IIS 6 or on IIS 7 (or IIS 7.5).</span></span>

### <a name="step-1-iis-7-or-iis-75-only"></a><span data-ttu-id="f2767-228">步驟1（僅限 IIS 7 或 IIS 7.5）</span><span class="sxs-lookup"><span data-stu-id="f2767-228">Step 1 (IIS 7 or IIS 7.5 only)</span></span>

<span data-ttu-id="f2767-229">只有執行 IIS 7 或 IIS 7.5 的作業系統（包括 Windows Vista、Windows Server 2008、Windows 7 和 Windows Server 2008 R2），才需要執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="f2767-229">This step is necessary only on operating systems that run IIS 7 or IIS 7.5, which includes Windows Vista, Windows Server 2008, Windows 7, and Windows Server 2008 R2.</span></span>

<span data-ttu-id="f2767-230">將父應用程式的 `Web.config` 檔案中的**configSections**定義（執行 ASP.NET 2.0 或 ASP.NET 3.5 的應用程式）移至 the.NET Framework 2.0 的根 `Web.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="f2767-230">Move the **configSections** definition in the `Web.config` file of the parent application (the application that runs ASP.NET 2.0 or ASP.NET 3.5) into the root `Web.config` file for the.NET Framework 2.0.</span></span> <span data-ttu-id="f2767-231">IIS 7 和 IIS 7.5 原生設定系統會在合併設定檔階層時掃描**configSections**元素。</span><span class="sxs-lookup"><span data-stu-id="f2767-231">The IIS 7 and IIS 7.5 native configuration system scans the **configSections** element when it merges the hierarchy of configuration files.</span></span> <span data-ttu-id="f2767-232">將**configSections**定義從父系 Web 應用程式的 `Web.config` 檔案移至根 `Web.config` 檔案，可有效地隱藏子 ASP.NET 4 應用程式所發生之設定合併處理的元素。</span><span class="sxs-lookup"><span data-stu-id="f2767-232">Moving the **configSections** definition from the parent Web application's `Web.config` file to the root `Web.config` file effectively hides the element from the configuration merge process that occurs for the child ASP.NET 4 application.</span></span>

<span data-ttu-id="f2767-233">在32位作業系統或32位應用程式集區中，ASP.NET 2.0 和 ASP.NET 3.5 的根 `Web.config` 檔案通常位於下列資料夾：</span><span class="sxs-lookup"><span data-stu-id="f2767-233">On a 32-bit operating system or for 32-bit application pools, the root `Web.config` file for ASP.NET 2.0 and ASP.NET 3.5 is normally located in the following folder:</span></span>

`C:\Windows\Microsoft.NET\Framework\v2.0.50727\CONFIG`

<span data-ttu-id="f2767-234">在64位作業系統或64位應用程式集區中，ASP.NET 2.0 和 ASP.NET 3.5 的根 `Web.config` 檔案通常位於下列資料夾：</span><span class="sxs-lookup"><span data-stu-id="f2767-234">On a 64-bit operating system or for 64-bit application pools, the root `Web.config` file for ASP.NET 2.0 and ASP.NET 3.5 is normally located in the following folder:</span></span>

`C:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG`

<span data-ttu-id="f2767-235">如果您在64位電腦上執行32位和64位的 Web 應用程式，您必須將**configSections**元素移到根 `Web.config` 檔案中，以供32位和64位系統使用。</span><span class="sxs-lookup"><span data-stu-id="f2767-235">If you run both 32-bit and 64-bit Web applications on a 64-bit computer, you must move the **configSections** element up into root `Web.config` files for both the 32-bit and the 64-bit systems.</span></span>

<span data-ttu-id="f2767-236">當您將**configSections**元素放在根 `Web.config` 檔案時，請將該區段貼到**configuration**元素之後的後面。</span><span class="sxs-lookup"><span data-stu-id="f2767-236">When you put the **configSections** element in the root `Web.config` file, paste the section immediately after the **configuration** element.</span></span> <span data-ttu-id="f2767-237">下列範例顯示當您完成移動元素時，根 `Web.config` 檔案的上半部應該看起來的樣子。</span><span class="sxs-lookup"><span data-stu-id="f2767-237">The following example shows what the top portion of the root `Web.config` file should look like when you have finished moving the elements.</span></span>

> [!NOTE]
> <span data-ttu-id="f2767-238">在下列範例中，已包裝行以方便閱讀。</span><span class="sxs-lookup"><span data-stu-id="f2767-238">In the following example, lines have been wrapped for readability.</span></span>

[!code-xml[Main](breaking-changes/samples/sample8.xml)]

### <a name="step-2-all-versions-of-iis"></a><span data-ttu-id="f2767-239">步驟2（所有版本的 IIS）</span><span class="sxs-lookup"><span data-stu-id="f2767-239">Step 2 (all versions of IIS)</span></span>

<span data-ttu-id="f2767-240">無論 ASP.NET 4 子 Web 應用程式是在 IIS 6 或 IIS 7 （或 IIS 7.5）上執行，都需要這個步驟。</span><span class="sxs-lookup"><span data-stu-id="f2767-240">This step is required whether the ASP.NET 4 child Web application is running on IIS 6 or on IIS 7 (or IIS 7.5).</span></span>

<span data-ttu-id="f2767-241">在執行 ASP.NET 2 或 ASP.NET 3.5 之父 Web 應用程式的 `Web.config` 檔案中，新增一個**位置**標籤，此標記會明確指定（適用于 IIS 和 ASP.NET 設定系統），而設定專案只會套用至父 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2767-241">In the `Web.config` file of the parent Web application that is running ASP.NET 2 or ASP.NET 3.5, add a **location** tag that explicitly specifies (for both the IIS and ASP.NET configuration systems) that the configuration entries only apply to the parent Web application.</span></span> <span data-ttu-id="f2767-242">下列範例顯示要加入之**location**元素的語法：</span><span class="sxs-lookup"><span data-stu-id="f2767-242">The following example shows the syntax of the **location** element to add:</span></span>

[!code-xml[Main](breaking-changes/samples/sample9.xml)]

<span data-ttu-id="f2767-243">下列範例顯示如何使用**location**標記來包裝所有設定區段，從**appSettings**區段開始，並以**system.webserver**區段結束。</span><span class="sxs-lookup"><span data-stu-id="f2767-243">The following example shows how the **location** tag is used to wrap all configuration sections starting with the **appSettings** section and ending with **system.webServer** section.</span></span>

[!code-xml[Main](breaking-changes/samples/sample10.xml)]

<span data-ttu-id="f2767-244">當您完成步驟1和2時，子 ASP.NET 4 Web 應用程式將會啟動而不會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="f2767-244">When you have completed steps 1 and 2, child ASP.NET 4 Web applications will start without errors.</span></span>

<a id="0.1__Toc252995491"></a><a id="0.1__Toc255587640"></a><a id="0.1__Toc256770151"></a>

## <a name="aspnet-4-web-sites-fail-to-start-on-computers-where-sharepoint-is-installed"></a><span data-ttu-id="f2767-245">ASP.NET 4 網站在安裝 SharePoint 的電腦上無法啟動</span><span class="sxs-lookup"><span data-stu-id="f2767-245">ASP.NET 4 Web Sites Fail to Start on Computers Where SharePoint Is Installed</span></span>

<span data-ttu-id="f2767-246">執行 SharePoint 的 Web 服務器具有部署在 SharePoint 網站根目錄的 `Web.config` 檔案（例如，`c:\inetpub\wwwroot\web.config` 用於預設的網站）。</span><span class="sxs-lookup"><span data-stu-id="f2767-246">Web servers that run SharePoint have a `Web.config` file that is deployed at the root of a SharePoint Web site (for example, `c:\inetpub\wwwroot\web.config` for Default Web Site).</span></span> <span data-ttu-id="f2767-247">在此 `Web.config` 檔案中，SharePoint 會將名為 WSS\_的自訂部分信任層級設定為最少。</span><span class="sxs-lookup"><span data-stu-id="f2767-247">In this `Web.config` file, SharePoint sets a custom partial-trust level named WSS\_Minimal.</span></span>

<span data-ttu-id="f2767-248">如果您嘗試執行的 ASP.NET 4 網站是部署為此類型 SharePoint 網站的子系，您將會看到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="f2767-248">If you try to run an ASP.NET 4 Web site that is deployed as a child of this type of SharePoint Web site, you will see the following error:</span></span>

`Could not find permission set named 'ASP.NET'.`

<span data-ttu-id="f2767-249">之所以發生此錯誤，是因為 ASP.NET 4 代碼啟用安全性（CAS）基礎結構會尋找名為 ASP.NET 的許可權集合。</span><span class="sxs-lookup"><span data-stu-id="f2767-249">This error occurs because the ASP.NET 4 code access security (CAS) infrastructure looks for a permission set named ASP.NET.</span></span> <span data-ttu-id="f2767-250">不過，WSS\_所參考的部分信任設定檔案，並不包含任何具有該名稱的許可權集合。</span><span class="sxs-lookup"><span data-stu-id="f2767-250">However, the partial trust configuration file that is referenced by WSS\_Minimal does not contain any permission sets with that name.</span></span>

<span data-ttu-id="f2767-251">目前沒有可與 ASP.NET 相容的 SharePoint 版本。</span><span class="sxs-lookup"><span data-stu-id="f2767-251">Currently there is not a version of SharePoint available that is compatible with ASP.NET.</span></span> <span data-ttu-id="f2767-252">因此，您不應該嘗試在 SharePoint 網站底下，將 ASP.NET 4 網站當做子網站執行。</span><span class="sxs-lookup"><span data-stu-id="f2767-252">As a result, you should not attempt to run an ASP.NET 4 Web site as a child site underneath SharePoint Web sites.</span></span>

<a id="0.1__Toc255587641"></a><a id="0.1__Toc256770152"></a>

## <a name="the-httprequestfilepath-property-no-longer-includes-pathinfo-values"></a><span data-ttu-id="f2767-253">HttpRequest 的屬性不再包含 PathInfo 值</span><span class="sxs-lookup"><span data-stu-id="f2767-253">The HttpRequest.FilePath Property No Longer Includes PathInfo Values</span></span>

<span data-ttu-id="f2767-254">舊版的 ASP.NET 在不同檔案路徑相關屬性（包括**HttpRequest**、 **HttpRequest、AppRelativeCurrentExecutionFilePath**和**HttpRequest**）所傳回的值中，包含了**PathInfo**值。</span><span class="sxs-lookup"><span data-stu-id="f2767-254">Previous versions of ASP.NET included a **PathInfo** value in the value returned from various file path-related properties, including **HttpRequest.FilePath**, **HttpRequest.AppRelativeCurrentExecutionFilePath**, and **HttpRequest.CurrentExecutionFilePath**.</span></span> <span data-ttu-id="f2767-255">ASP.NET 4 不再包含這些屬性的傳回值中的**PathInfo**值。</span><span class="sxs-lookup"><span data-stu-id="f2767-255">ASP.NET 4 no longer includes the **PathInfo** value in the return values from these properties.</span></span> <span data-ttu-id="f2767-256">相反地， **PathInfo**資訊可在**HttpRequest. PathInfo**中取得。</span><span class="sxs-lookup"><span data-stu-id="f2767-256">Instead, the **PathInfo** information is available in **HttpRequest.PathInfo**.</span></span> <span data-ttu-id="f2767-257">例如，假設有下列 URL 片段：</span><span class="sxs-lookup"><span data-stu-id="f2767-257">For example, imagine the following URL fragment:</span></span>

`/testapp/Action.mvc/SomeAction`

<span data-ttu-id="f2767-258">在舊版的 ASP.NET 中， **HttpRequest**屬性具有下列值：</span><span class="sxs-lookup"><span data-stu-id="f2767-258">In earlier versions of ASP.NET, **HttpRequest** properties have the following values:</span></span>

<span data-ttu-id="f2767-259">**HttpRequest FilePath**： `/testapp/Action.mvc/SomeAction`</span><span class="sxs-lookup"><span data-stu-id="f2767-259">**HttpRequest.FilePath**: `/testapp/Action.mvc/SomeAction`</span></span>

<span data-ttu-id="f2767-260">**HttpRequest. PathInfo**：（空白）</span><span class="sxs-lookup"><span data-stu-id="f2767-260">**HttpRequest.PathInfo**: (empty)</span></span>

<span data-ttu-id="f2767-261">在 ASP.NET 4 中， **HttpRequest**屬性會改為具有下列值：</span><span class="sxs-lookup"><span data-stu-id="f2767-261">In ASP.NET 4, **HttpRequest** properties instead have the following values:</span></span>

<span data-ttu-id="f2767-262">**HttpRequest FilePath**： `/testapp/Action.mvc`</span><span class="sxs-lookup"><span data-stu-id="f2767-262">**HttpRequest.FilePath**: `/testapp/Action.mvc`</span></span>

<span data-ttu-id="f2767-263">**HttpRequest. PathInfo**： `SomeAction`</span><span class="sxs-lookup"><span data-stu-id="f2767-263">**HttpRequest.PathInfo**: `SomeAction`</span></span>

<a id="0.1__Toc252995493"></a><a id="0.1__Toc255587642"></a><a id="0.1__Toc256770153"></a><a id="0.1__Toc245724861"></a>

## <a name="aspnet-20-applications-might-generate-httpexception-errors-that-reference-eurlaxd"></a><span data-ttu-id="f2767-264">ASP.NET 2.0 應用程式可能會產生參考 eurl 的 HttpException 錯誤</span><span class="sxs-lookup"><span data-stu-id="f2767-264">ASP.NET 2.0 Applications Might Generate HttpException Errors that Reference eurl.axd</span></span>

<span data-ttu-id="f2767-265">在 IIS 6 上啟用 ASP.NET 4 之後，IIS 6 上執行的 ASP.NET 2.0 應用程式 (在 Windows Server 2003 或 Windows Server 2003 R2 中) 可能會產生下列這類錯誤：</span><span class="sxs-lookup"><span data-stu-id="f2767-265">After ASP.NET 4 has been enabled on IIS 6, ASP.NET 2.0 applications that run on IIS 6 (in either Windows Server 2003 or Windows Server 2003 R2) might generate errors such as the following:</span></span>

`System.Web.HttpException: Path '/[yourApplicationRoot]/eurl.axd/[Value]' was not found.`

<span data-ttu-id="f2767-266">發生此錯誤的原因是當 ASP.NET 偵測到某個網站已設定為使用 ASP.NET 4 時，ASP.NET 4 的原生元件會將無副檔名 URL 傳遞至 ASP.NET 的 managed 部分，以供進一步處理。</span><span class="sxs-lookup"><span data-stu-id="f2767-266">This error occurs because when ASP.NET detects that a Web site is configured to use ASP.NET 4, a native component of ASP.NET 4 passes an extensionless URL to the managed portion of ASP.NET for further processing.</span></span> <span data-ttu-id="f2767-267">不過，如果 ASP.NET 4 網站底下的虛擬目錄設定為使用 ASP.NET 2.0，以這種方式處理無副檔名 URL 會產生包含字串 "eurl" 的修改 URL。</span><span class="sxs-lookup"><span data-stu-id="f2767-267">However, if virtual directories that are below an ASP.NET 4 Web site are configured to use ASP.NET 2.0, processing the extensionless URL in this way results in a modified URL that contains the string "eurl.axd".</span></span> <span data-ttu-id="f2767-268">這個修改後的 URL 會傳送至 ASP.NET 2.0 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2767-268">This modified URL is then sent to the ASP.NET 2.0 application.</span></span> <span data-ttu-id="f2767-269">ASP.NET 2.0 無法辨識 "eurl" 格式。</span><span class="sxs-lookup"><span data-stu-id="f2767-269">ASP.NET 2.0 cannot recognize the "eurl.axd" format.</span></span> <span data-ttu-id="f2767-270">因此，ASP.NET 2.0 會嘗試尋找名為 `eurl.axd` 的檔案，並加以執行。</span><span class="sxs-lookup"><span data-stu-id="f2767-270">Therefore, ASP.NET 2.0 tries to find a file named `eurl.axd` and execute it.</span></span> <span data-ttu-id="f2767-271">因為沒有這類檔案存在，要求會失敗並出現**HttpException**例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f2767-271">Because no such file exists, the request fails with an **HttpException** exception.</span></span>

<span data-ttu-id="f2767-272">您可以使用下列其中一個選項來解決此問題。</span><span class="sxs-lookup"><span data-stu-id="f2767-272">You can work around this issue using one of the following options.</span></span>

### <a name="option-1"></a><span data-ttu-id="f2767-273">選項 1</span><span class="sxs-lookup"><span data-stu-id="f2767-273">Option 1</span></span>

<span data-ttu-id="f2767-274">如果執行網站時不需要 ASP.NET 4，請重新對應網站，改為使用 ASP.NET 2.0。</span><span class="sxs-lookup"><span data-stu-id="f2767-274">If ASP.NET 4 is not required in order to run the Web site, remap the site to use ASP.NET 2.0 instead.</span></span>

### <a name="option-2"></a><span data-ttu-id="f2767-275">選項 2</span><span class="sxs-lookup"><span data-stu-id="f2767-275">Option 2</span></span>

<span data-ttu-id="f2767-276">如果需要 ASP.NET 4 才能執行網站，請將任何子 ASP.NET 2.0 虛擬目錄移到另一個對應至 ASP.NET 2.0 的網站。</span><span class="sxs-lookup"><span data-stu-id="f2767-276">If ASP.NET 4 is required in order to run the Web site, move any child ASP.NET 2.0 virtual directories to a different Web site that is mapped to ASP.NET 2.0.</span></span>

### <a name="option-3"></a><span data-ttu-id="f2767-277">選項3</span><span class="sxs-lookup"><span data-stu-id="f2767-277">Option 3</span></span>

<span data-ttu-id="f2767-278">如果將網站重新對應至 ASP.NET 2.0 或變更虛擬目錄的位置並不實用，請明確停用 ASP.NET 4 中的無副檔名 URL 處理。</span><span class="sxs-lookup"><span data-stu-id="f2767-278">If it is not practical to remap the Web site to ASP.NET 2.0 or to change the location of a virtual directory, explicitly disable extensionless URL processing in ASP.NET 4.</span></span> <span data-ttu-id="f2767-279">請使用下列程序：</span><span class="sxs-lookup"><span data-stu-id="f2767-279">Use the following procedure:</span></span>

1. <span data-ttu-id="f2767-280">在 Windows 登錄中，開啟下列節點：</span><span class="sxs-lookup"><span data-stu-id="f2767-280">In the Windows registry, open the following node:</span></span>

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\4.0.30319.0`

1. <span data-ttu-id="f2767-281">建立名為**EnableExtensionlessUrls**的新**DWORD**值。</span><span class="sxs-lookup"><span data-stu-id="f2767-281">Create a new **DWORD** value named **EnableExtensionlessUrls**.</span></span>
2. <span data-ttu-id="f2767-282">將**EnableExtensionlessUrls**設定為0。</span><span class="sxs-lookup"><span data-stu-id="f2767-282">Set **EnableExtensionlessUrls** to 0.</span></span> <span data-ttu-id="f2767-283">這會停用無副檔名 URL 行為。</span><span class="sxs-lookup"><span data-stu-id="f2767-283">This disables extensionless URL behavior.</span></span>
3. <span data-ttu-id="f2767-284">儲存登錄值，然後關閉 [登錄編輯程式]。</span><span class="sxs-lookup"><span data-stu-id="f2767-284">Save the registry value and close the registry editor.</span></span>
4. <span data-ttu-id="f2767-285">執行**iisreset**命令列工具，這會導致 IIS 讀取新的登錄值。</span><span class="sxs-lookup"><span data-stu-id="f2767-285">Run the **iisreset** command-line tool, which causes IIS to read the new registry value.</span></span>

> [!NOTE]
> <span data-ttu-id="f2767-286">將**EnableExtensionlessUrls**設定為1可啟用無副檔名 URL 行為。</span><span class="sxs-lookup"><span data-stu-id="f2767-286">Setting **EnableExtensionlessUrls** to 1 enables extensionless URL behavior.</span></span> <span data-ttu-id="f2767-287">如果未指定任何值，這就是預設設定。</span><span class="sxs-lookup"><span data-stu-id="f2767-287">This is the default setting if no value is specified.</span></span>

<a id="0.1__Toc252995494"></a><a id="0.1__Toc255587643"></a><a id="0.1__Toc256770154"></a><a id="0.1__Toc245724862"></a>

## <a name="event-handlers-might-not-be-not-raised-in-a-default-document-in-iis-7-or-iis-75-integrated-mode"></a><span data-ttu-id="f2767-288">事件處理常式可能不會在 IIS 7 或 IIS 7.5 整合模式的預設檔中引發</span><span class="sxs-lookup"><span data-stu-id="f2767-288">Event Handlers Might Not Be Not Raised in a Default Document in IIS 7 or IIS 7.5 Integrated Mode</span></span>

<span data-ttu-id="f2767-289">ASP.NET 4 包含修改，可變更當無副檔名 URL 解析為預設檔時，如何呈現 HTML**表單**元素的**action**屬性。</span><span class="sxs-lookup"><span data-stu-id="f2767-289">ASP.NET 4 includes modifications that change how the **action** attribute of the HTML **form** element is rendered when an extensionless URL resolves to a default document.</span></span> <span data-ttu-id="f2767-290">無副檔名 URL 解析為預設檔的範例會[http://contoso.com/](http://contoso.com/)，因而導致[http://contoso.com/Default.aspx](http://contoso.com/Default.aspx)的要求。</span><span class="sxs-lookup"><span data-stu-id="f2767-290">An example of an extensionless URL resolving to a default document would be [http://contoso.com/](http://contoso.com/), resulting in a request to [http://contoso.com/Default.aspx](http://contoso.com/Default.aspx).</span></span>

<span data-ttu-id="f2767-291">ASP.NET 4 現在會在對具有對應預設檔的無副檔名 URL 提出要求時，將 HTML**表單**元素的**動作**屬性值呈現為空字串。</span><span class="sxs-lookup"><span data-stu-id="f2767-291">ASP.NET 4 now renders the HTML **form** element's **action** attribute value as an empty string when a request is made to an extensionless URL that has a default document mapped to it.</span></span> <span data-ttu-id="f2767-292">例如，在舊版的 ASP.NET 中， [http://contoso.com](http://contoso.com)的要求會導致 `Default.aspx`的要求。</span><span class="sxs-lookup"><span data-stu-id="f2767-292">For example, in earlier releases of ASP.NET, a request to [http://contoso.com](http://contoso.com) would result in a request to `Default.aspx`.</span></span> <span data-ttu-id="f2767-293">在該檔中，開啟**表單**標記會如下列範例所示呈現：</span><span class="sxs-lookup"><span data-stu-id="f2767-293">In that document, the opening **form** tag would be rendered as in the following example:</span></span>

`<form action="Default.aspx" />`

<span data-ttu-id="f2767-294">在 ASP.NET 4 中， [http://contoso.com](http://contoso.com)的要求也會導致 `Default.aspx`的要求。</span><span class="sxs-lookup"><span data-stu-id="f2767-294">In ASP.NET 4, a request to [http://contoso.com](http://contoso.com) also results in a request to `Default.aspx`.</span></span> <span data-ttu-id="f2767-295">不過，ASP.NET 現在會轉譯 HTML 開啟**表單**標記，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f2767-295">However, ASP.NET now renders the HTML opening **form** tag as in the following example:</span></span>

`<form action="" />`

<span data-ttu-id="f2767-296">如何轉譯**動作**屬性的這項差異，可能會導致 IIS 和 ASP.NET 處理表單張貼時的細微變更。</span><span class="sxs-lookup"><span data-stu-id="f2767-296">This difference in how the **action** attribute is rendered can cause subtle changes in how a form post is processed by IIS and ASP.NET.</span></span> <span data-ttu-id="f2767-297">當**action**屬性是空字串時，IIS **DefaultDocumentModule**物件將會建立 `Default.aspx`的子要求。</span><span class="sxs-lookup"><span data-stu-id="f2767-297">When the **action** attribute is an empty string, the IIS **DefaultDocumentModule** object will create a child request to `Default.aspx`.</span></span> <span data-ttu-id="f2767-298">在大部分的情況下，此子要求對應用程式代碼而言是透明的，而且 [`Default.aspx`] 頁面會正常執行。</span><span class="sxs-lookup"><span data-stu-id="f2767-298">Under most conditions, this child request is transparent to application code, and the `Default.aspx` page runs normally.</span></span>

<span data-ttu-id="f2767-299">不過，Managed 程式碼與 IIS 7 或 IIS 7.5 整合模式之間的可能互動可能會在子要求期間讓受管理 .aspx 頁面適當地停止運作。</span><span class="sxs-lookup"><span data-stu-id="f2767-299">However, a potential interaction between managed code and IIS 7 or IIS 7.5 Integrated mode can cause managed .aspx pages to stop working properly during the child request.</span></span> <span data-ttu-id="f2767-300">如果發生下列情況，對 `Default.aspx` 檔的子要求將會導致錯誤或非預期的行為：</span><span class="sxs-lookup"><span data-stu-id="f2767-300">If the following conditions occur, the child request to a `Default.aspx` document will result in an error or in unexpected behavior:</span></span>

1. <span data-ttu-id="f2767-301">.Aspx 頁面會傳送至瀏覽器，並將**form**元素的**action**屬性設定為 ""。</span><span class="sxs-lookup"><span data-stu-id="f2767-301">An .aspx page is sent to the browser with the **form** element's **action** attribute set to "".</span></span>
2. <span data-ttu-id="f2767-302">表單會回傳給 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="f2767-302">The form is posted back to ASP.NET.</span></span>
3. <span data-ttu-id="f2767-303">Managed HTTP 模組會讀取實體主體的某個部分。</span><span class="sxs-lookup"><span data-stu-id="f2767-303">A managed HTTP module reads some part of the entity body.</span></span> <span data-ttu-id="f2767-304">例如，模組會讀取**Request. Form**或**request. Params**。</span><span class="sxs-lookup"><span data-stu-id="f2767-304">For example, a module reads **Request.Form** or **Request.Params**.</span></span> <span data-ttu-id="f2767-305">這會將 POST 要求的實體主體讀入受管理記憶體中。</span><span class="sxs-lookup"><span data-stu-id="f2767-305">This causes the entity body of the POST request to be read into managed memory.</span></span> <span data-ttu-id="f2767-306">因此，任何以 IIS 7 或 IIS 7.5 整合模式執行的機器碼模組都無法再使用實體主體。</span><span class="sxs-lookup"><span data-stu-id="f2767-306">As a result, the entity body is no longer available to any native code modules that are running in IIS 7 or IIS 7.5 Integrated mode.</span></span>
4. <span data-ttu-id="f2767-307">IIS **DefaultDocumentModule**物件最後會執行，並建立 `Default.aspx` 檔的子要求。</span><span class="sxs-lookup"><span data-stu-id="f2767-307">The IIS **DefaultDocumentModule** object eventually runs and creates a child request to the `Default.aspx` document.</span></span> <span data-ttu-id="f2767-308">不過，因為 Managed 程式碼的某個部分已經讀取實體主體，所以沒有實體主體可用來傳送至子要求。</span><span class="sxs-lookup"><span data-stu-id="f2767-308">However, because the entity body has already been read by a piece of managed code, there is no entity body available to send to the child request.</span></span>
5. <span data-ttu-id="f2767-309">當 HTTP 管線針對子要求執行時，`.aspx` 檔案的處理常式會在處理常式執行階段執行。</span><span class="sxs-lookup"><span data-stu-id="f2767-309">When the HTTP pipeline runs for the child request, the handler for `.aspx` files runs during the handler-execute phase.</span></span>
6. <span data-ttu-id="f2767-310">因為沒有實體主體，所以沒有任何表單變數和 view 狀態，因此 .aspx 頁面處理常式不會提供任何資訊來判斷應該引發的事件（如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="f2767-310">Because there is no entity body, there are no form variables and no view state, and therefore no information is available for the .aspx page handler to determine what event (if any) is supposed to be raised.</span></span> <span data-ttu-id="f2767-311">因此，未執行受影響 .aspx 頁面的回傳事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="f2767-311">As a result, none of the postback event handlers for the affected .aspx page run.</span></span>

<span data-ttu-id="f2767-312">您可以透過下列方式來解決這個行為：</span><span class="sxs-lookup"><span data-stu-id="f2767-312">You can work around this behavior in the following ways:</span></span>

- <span data-ttu-id="f2767-313">識別在預設檔要求期間存取要求之實體主體的 HTTP 模組，並判斷是否可以將它設定為僅針對受控要求執行。</span><span class="sxs-lookup"><span data-stu-id="f2767-313">Identify the HTTP module that is accessing the request's entity body during default document requests and determine whether it can be configured to run only for managed requests.</span></span> <span data-ttu-id="f2767-314">在 IIS 7 和 IIS 7.5 的整合模式中，HTTP 模組可以標記為僅針對受控要求執行，方法是將下列屬性新增至模組的 system.webserver **/模組**專案：</span><span class="sxs-lookup"><span data-stu-id="f2767-314">In Integrated mode for both IIS 7 and IIS 7.5, HTTP modules can be marked to run only for managed requests by adding the following attribute to the module's **system.webServer/modules** entry:</span></span>

- `precondition="managedHandler"`

- <span data-ttu-id="f2767-315">此設定會針對 IIS 7 和 IIS 7.5 判斷為不受管理要求的要求停用模組。</span><span class="sxs-lookup"><span data-stu-id="f2767-315">This setting disables the module for requests that IIS 7 and IIS 7.5 determine as not being managed requests.</span></span> <span data-ttu-id="f2767-316">對於預設檔要求，第一個要求是無副檔名 URL。</span><span class="sxs-lookup"><span data-stu-id="f2767-316">For default document requests, the first request is to an extensionless URL.</span></span> <span data-ttu-id="f2767-317">因此，在初始要求處理期間，IIS 不會執行任何標記為受管理處理程式前置條件的受管理模組。</span><span class="sxs-lookup"><span data-stu-id="f2767-317">Therefore, IIS does not run any managed modules that are marked with a precondition of managed Handler during initial request processing.</span></span> <span data-ttu-id="f2767-318">因此，受控模組不會不慎讀取實體主體，因此實體主體仍然可以使用，並傳遞至子要求和預設檔。</span><span class="sxs-lookup"><span data-stu-id="f2767-318">As a result, managed modules will not accidentally read the entity body and thus the entity body is still available and is passed along to the child request and to the default document.</span></span>

- <span data-ttu-id="f2767-319">如果有問題的 HTTP 模組必須針對所有要求執行（針對靜態檔案、針對解析為**DefaultDocumentModule**物件的無副檔名 url、針對 managed 要求等），請明確地將網頁的**microsoft.visualstudio.testtools.uitesting.htmlcontrols> HtmlForm**控制項的**Action**屬性設定為非空白字串，以修改受影響的 .aspx 頁面。</span><span class="sxs-lookup"><span data-stu-id="f2767-319">If the problematic HTTP modules have to run for all requests (for static files, for extensionless URLs that resolve to the **DefaultDocumentModule** object, for managed requests, etc.), modify the affected .aspx pages by explicitly setting the **Action** property of the page's **System.Web.UI.HtmlControls.HtmlForm** control to a non-empty string.</span></span> <span data-ttu-id="f2767-320">例如，如果預設檔是 `Default.aspx`，請修改頁面的程式碼，將**HtmlForm**控制項的**Action**屬性明確設定為 "default.aspx"。</span><span class="sxs-lookup"><span data-stu-id="f2767-320">For example, if the default document is `Default.aspx`, modify the page's code to explicitly set the **HtmlForm** control's **Action** property to "Default.aspx".</span></span>

<a id="0.1__Toc255587644"></a><a id="0.1__Toc256770155"></a>

## <a name="changes-to-the-aspnet-code-access-security-cas-implementation"></a><span data-ttu-id="f2767-321">對 ASP.NET 代碼啟用安全性（CAS）實行的變更</span><span class="sxs-lookup"><span data-stu-id="f2767-321">Changes to the ASP.NET Code Access Security (CAS) Implementation</span></span>

<span data-ttu-id="f2767-322">ASP.NET 2.0，並擴充3.5 中新增的 ASP.NET 功能，請使用 .NET Framework 1.1 和2.0 代碼啟用安全性（CAS）模型。</span><span class="sxs-lookup"><span data-stu-id="f2767-322">ASP.NET 2.0, and by extension the ASP.NET features that were added in 3.5, use the .NET Framework 1.1 and 2.0 code access security (CAS) model.</span></span> <span data-ttu-id="f2767-323">不過，已大幅全面檢查 ASP.NET 4 中 CAS 的實作。</span><span class="sxs-lookup"><span data-stu-id="f2767-323">However, the implementation of CAS in ASP.NET 4 has been substantially overhauled.</span></span> <span data-ttu-id="f2767-324">因此，依賴全域組件快取（GAC）中執行之受信任程式碼的部分信任 ASP.NET 應用程式可能會失敗，並出現各種安全性例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f2767-324">As a result, partial-trust ASP.NET applications that rely on trusted code running in the global assembly cache (GAC) might fail with various security exceptions.</span></span> <span data-ttu-id="f2767-325">依賴大量修改機器 CAS 原則的部分信任應用程式也可能會因為安全性例外狀況而失敗。</span><span class="sxs-lookup"><span data-stu-id="f2767-325">Partial-trust applications that rely on extensive modifications to machine CAS policy might also fail with security exceptions.</span></span>

<span data-ttu-id="f2767-326">您可以使用**信任**設定元素中的新**legacyCasModel**屬性，將部分信任 ASP.NET 4 應用程式還原為 ASP.NET 1.1 和2.0 的行為，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f2767-326">You can revert partial-trust ASP.NET 4 applications to the behavior of ASP.NET 1.1 and 2.0 using the new **legacyCasModel** attribute in the **trust** configuration element, as shown in the following example:</span></span>

`<trust level= "Medium" legacyCasModel="true" />`

<span data-ttu-id="f2767-327">當您還原為舊版 CAS 模型時，會啟用下列舊的 CAS 行為：</span><span class="sxs-lookup"><span data-stu-id="f2767-327">When you revert to the legacy CAS model, the following old CAS behaviors are enabled:</span></span>

- <span data-ttu-id="f2767-328">遵守機器 CAS 原則。</span><span class="sxs-lookup"><span data-stu-id="f2767-328">Machine CAS policy is honored.</span></span>
- <span data-ttu-id="f2767-329">允許單一應用程式域中有多個不同的許可權集合。</span><span class="sxs-lookup"><span data-stu-id="f2767-329">Multiple different permission sets in a single application domain are allowed.</span></span>
- <span data-ttu-id="f2767-330">當只有 ASP.NET 或其他 .NET Framework 程式碼位於堆疊上時，GAC 中的元件不需要明確許可權判斷提示。</span><span class="sxs-lookup"><span data-stu-id="f2767-330">Explicit permission assertions are not required for assemblies in the GAC that are invoked when only ASP.NET or other .NET Framework code is on the stack.</span></span>

<span data-ttu-id="f2767-331">其中一個案例無法在 .NET Framework 4 中還原：非 Web 部分信任應用程式無法再呼叫 System.web 和 System.web 中的特定 Api。</span><span class="sxs-lookup"><span data-stu-id="f2767-331">One scenario cannot be reverted in the .NET Framework 4: non-Web partial-trust applications can no longer call certain APIs in System.Web.dll and System.Web.Extensions.dll.</span></span> <span data-ttu-id="f2767-332">在舊版的 .NET Framework 中，非 Web 部分信任應用程式可能會明確授與**內所 aspnethostingpermission**許可權。</span><span class="sxs-lookup"><span data-stu-id="f2767-332">In previous versions of the .NET Framework, it was possible for non-Web partial-trust applications to be explicitly granted **AspNetHostingPermission** permissions.</span></span> <span data-ttu-id="f2767-333">然後，這些應用程式就可以使用**HTTPutility.htmlencode**、ClientServices 中的型別 **\*** 命名空間，以及與成員資格、角色和設定檔相關的類型。</span><span class="sxs-lookup"><span data-stu-id="f2767-333">These applications could then use **System.Web.HttpUtility**, types in the **System.Web.ClientServices.\*** namespaces, and types related to membership, roles, and profiles.</span></span> <span data-ttu-id="f2767-334">.NET Framework 4 中不再支援從非 Web 部分信任應用程式呼叫這些類型。</span><span class="sxs-lookup"><span data-stu-id="f2767-334">Calling these types from non-Web partial trust applications is no longer supported in the .NET Framework 4.</span></span>

> [!NOTE]
> <span data-ttu-id="f2767-335">**Httputility.htmlencode**類別的**HtmlEncode**和**system.net.webutility.htmldecode**功能已移至新的 .NET Framework 4**系統 .net. webutility.htmldecode**類別。</span><span class="sxs-lookup"><span data-stu-id="f2767-335">The **HtmlEncode** and **HtmlDecode** functionality of the **System.Web.HttpUtility** class was moved to the new .NET Framework 4 **System.Net.WebUtility** class.</span></span> <span data-ttu-id="f2767-336">如果這是唯一使用的 ASP.NET 功能，請修改應用程式的程式碼，改為使用新的**webutility.htmldecode**類別。</span><span class="sxs-lookup"><span data-stu-id="f2767-336">If that was the only ASP.NET functionality that was being used, modify the application's code to use the new **WebUtility** class instead.</span></span>

<span data-ttu-id="f2767-337">以下是 ASP.NET 4 中預設 CAS 執行變更的高階摘要：</span><span class="sxs-lookup"><span data-stu-id="f2767-337">The following is a high-level summary of the changes to the default CAS implementation in ASP.NET 4:</span></span>

- <span data-ttu-id="f2767-338">ASP.NET 應用程式域現在是同質應用程式域。</span><span class="sxs-lookup"><span data-stu-id="f2767-338">ASP.NET application domains are now homogeneous application domains.</span></span> <span data-ttu-id="f2767-339">只有部分信任和完全信任的授與集可在應用程式域中使用。</span><span class="sxs-lookup"><span data-stu-id="f2767-339">Only partial-trust and full-trust grant sets are available in an application domain.</span></span>
- <span data-ttu-id="f2767-340">ASP.NET 部分信任的授與集與任何企業層級、電腦層級或使用者層級的 CAS 原則無關。</span><span class="sxs-lookup"><span data-stu-id="f2767-340">ASP.NET partial-trust grant sets are independent from any enterprise-level, machine-level, or user-level CAS policy.</span></span>
- <span data-ttu-id="f2767-341">已將3.5 和 3.5 SP1 隨附的 ASP.NET 元件轉換成使用 .NET Framework 4 透明度模型。</span><span class="sxs-lookup"><span data-stu-id="f2767-341">ASP.NET assemblies that shipped in 3.5 and 3.5 SP1 have been converted to use the .NET Framework 4 transparency model.</span></span>
- <span data-ttu-id="f2767-342">ASP.NET**內所 aspnethostingpermission**屬性的使用已大幅降低。</span><span class="sxs-lookup"><span data-stu-id="f2767-342">Use of the ASP.NET **AspNetHostingPermission** attribute has been substantially reduced.</span></span> <span data-ttu-id="f2767-343">已從公用 ASP.NET Api 中移除此屬性的大多數實例。</span><span class="sxs-lookup"><span data-stu-id="f2767-343">Most instances of this attribute have been removed from the public ASP.NET APIs.</span></span>
- <span data-ttu-id="f2767-344">ASP.NET 組建提供者所建立的動態編譯元件已更新，以明確地將元件標記為透明。</span><span class="sxs-lookup"><span data-stu-id="f2767-344">Dynamically compiled assemblies that are created by ASP.NET build providers have been updated to explicitly mark assemblies as transparent.</span></span>
- <span data-ttu-id="f2767-345">所有的 ASP.NET 元件現在都會標示為僅在 Web 主控環境中接受 APTCA 屬性。</span><span class="sxs-lookup"><span data-stu-id="f2767-345">All ASP.NET assemblies are now marked in such a way that the APTCA attribute is honored only in Web hosting environments.</span></span> <span data-ttu-id="f2767-346">部分信任的非 Web 裝載環境（例如 ClickOnce）無法呼叫 ASP.NET 元件。</span><span class="sxs-lookup"><span data-stu-id="f2767-346">Partially trusted non-Web hosting environments like ClickOnce will not be able to call into ASP.NET assemblies.</span></span>

<span data-ttu-id="f2767-347">如需新的 ASP.NET 4 代碼啟用安全性模型的詳細資訊，請參閱 MSDN 網站上的在[ASP.NET 應用程式中使用代碼啟用安全性](https://msdn.microsoft.com/library/dd984947%28VS.100%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f2767-347">For more information about the new ASP.NET 4 code access security model, see [Using Code Access Security in ASP.NET Applications](https://msdn.microsoft.com/library/dd984947%28VS.100%29.aspx) on the MSDN Web site.</span></span>

<a id="0.1__Toc256770156"></a><a id="0.1__Toc245724863"></a><a id="0.1__Toc252995496"></a><a id="0.1__Toc255587645"></a><a id="0.1__Toc245724864"></a>

## <a name="membershipuser-and-other-types-in-the-systemwebsecurity-namespace-have-been-moved"></a><span data-ttu-id="f2767-348">MembershipUser 和 System.web. Security 命名空間中的其他類型已移動</span><span class="sxs-lookup"><span data-stu-id="f2767-348">MembershipUser and Other Types in the System.Web.Security Namespace Have Been Moved</span></span>

<span data-ttu-id="f2767-349">某些用於 ASP.NET 成員資格的類型已從 `System.Web.dll` 移至新的 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception .dll 元件。</span><span class="sxs-lookup"><span data-stu-id="f2767-349">Some types that are used in ASP.NET membership have been moved from `System.Web.dll` to the new System.Web.ApplicationServices.dll assembly.</span></span> <span data-ttu-id="f2767-350">已移動類型，以解析用戶端和擴充 .NET Framework SKU 中類型之間的架構層相依性。</span><span class="sxs-lookup"><span data-stu-id="f2767-350">The types were moved in order to resolve architectural layering dependencies between types in the client and in extended .NET Framework SKUs.</span></span>

<span data-ttu-id="f2767-351">由於 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 已新增至 ASP.NET 編譯系統預設使用的參考元件清單中，因此網站專案不會因為移動這些類型而產生任何問題。</span><span class="sxs-lookup"><span data-stu-id="f2767-351">Web site projects do not have problems as a result of moving these types, because System.Web.ApplicationServices.dll was added to the list of referenced assemblies that is used by default by the ASP.NET compilation system.</span></span> <span data-ttu-id="f2767-352">如果您將使用舊版 ASP.NET 建立的網站專案升級為 ASP.NET 4，方法是在 Visual Studio 2010 中開啟它，專案就會編譯而不會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="f2767-352">If you upgrade a Web site project that was created using an earlier version of ASP.NET to ASP.NET 4 by opening it in Visual Studio 2010, the project will compile without errors.</span></span>

<span data-ttu-id="f2767-353">同樣地，如果您在 Visual Studio 2010 中開啟以舊版 ASP.NET 建立的 Web 應用程式專案到 ASP.NET 4，升級程式就會將 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 的參考加入至專案。</span><span class="sxs-lookup"><span data-stu-id="f2767-353">Similarly, if you upgrade a Web application project that was created in an earlier version of ASP.NET to ASP.NET 4 by opening it in Visual Studio 2010, the upgrade process adds a reference to System.Web.ApplicationServices.dll to the project.</span></span> <span data-ttu-id="f2767-354">因此，升級的 Web 應用程式專案也會編譯而不會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="f2767-354">Therefore, upgraded Web application projects will also compile without errors.</span></span>

<span data-ttu-id="f2767-355">使用舊版 ASP.NET 所建立的已編譯（二進位）檔案也會在 ASP.NET 4 上執行，而不會發生錯誤，即使成員資格類型已移至不同的元件也一樣。</span><span class="sxs-lookup"><span data-stu-id="f2767-355">Compiled (binary) files that were created using earlier versions of ASP.NET will also run without errors on ASP.NET 4, even though the membership types were moved to a different assembly.</span></span> <span data-ttu-id="f2767-356">類型轉送資訊已新增至 ASP.NET 4 版的 `System.Web.dll`，會自動將這些類型的執行時間參考路由至類型的新位置。</span><span class="sxs-lookup"><span data-stu-id="f2767-356">Type forwarding information has been added to the ASP.NET 4 version of `System.Web.dll` that automatically routes run-time references for these types to the new location for the types.</span></span>

<span data-ttu-id="f2767-357">不過，使用特定成員資格類型，而且已從舊版 ASP.NET 升級的類別庫，在 ASP.NET 4 專案中使用時，將無法進行編譯。</span><span class="sxs-lookup"><span data-stu-id="f2767-357">However, class libraries that use specific membership types and that have been upgraded from earlier versions of ASP.NET will fail to compile when used in an ASP.NET 4 project.</span></span> <span data-ttu-id="f2767-358">例如，類別庫專案可能無法編譯和報告錯誤，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f2767-358">For example, a class library project might fail to compile and report an error such as the following:</span></span>

- `The type 'System.Web.Security.MembershipUser' is defined in an assembly that is not referenced. You must add a reference to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`

- `The type name 'MembershipUser' could not be found. This type has been forwarded to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'. Consider adding a reference to that assembly.`

<span data-ttu-id="f2767-359">若要解決這個問題，您可以在類別庫專案中加入 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 的參考。</span><span class="sxs-lookup"><span data-stu-id="f2767-359">You can work around this problem by adding a reference in your class library project to System.Web.ApplicationServices.dll.</span></span>

<span data-ttu-id="f2767-360">下列清單顯示已從 `System.Web.dll` 移至 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 的*system.web. Security*型別：</span><span class="sxs-lookup"><span data-stu-id="f2767-360">The following list shows the *System.Web.Security* types that were moved from `System.Web.dll` to System.Web.ApplicationServices.dll:</span></span>

- <span data-ttu-id="f2767-361">*System.web. Security. MembershipCreateStatus*</span><span class="sxs-lookup"><span data-stu-id="f2767-361">*System.Web.Security.MembershipCreateStatus*</span></span>
- <span data-ttu-id="f2767-362">*CreateUserException 的成員。*</span><span class="sxs-lookup"><span data-stu-id="f2767-362">*System.Web.Security.Membership.CreateUserException*</span></span>
- <span data-ttu-id="f2767-363">*System.web. Security. System.web.security.membershippasswordexception*</span><span class="sxs-lookup"><span data-stu-id="f2767-363">*System.Web.Security.MembershipPasswordException*</span></span>
- <span data-ttu-id="f2767-364">*System.web. Security. MembershipPasswordFormat*</span><span class="sxs-lookup"><span data-stu-id="f2767-364">*System.Web.Security.MembershipPasswordFormat*</span></span>
- <span data-ttu-id="f2767-365">*System.web. MembershipProvider*</span><span class="sxs-lookup"><span data-stu-id="f2767-365">*System.Web.Security.MembershipProvider*</span></span>
- <span data-ttu-id="f2767-366">*System.web. Security. MembershipProviderCollection*</span><span class="sxs-lookup"><span data-stu-id="f2767-366">*System.Web.Security.MembershipProviderCollection*</span></span>
- <span data-ttu-id="f2767-367">*System.web. Security. MembershipUser*</span><span class="sxs-lookup"><span data-stu-id="f2767-367">*System.Web.Security.MembershipUser*</span></span>
- <span data-ttu-id="f2767-368">*System.web. Security. MembershipUserCollection*</span><span class="sxs-lookup"><span data-stu-id="f2767-368">*System.Web.Security.MembershipUserCollection*</span></span>
- <span data-ttu-id="f2767-369">*System.web. Security. MembershipValidatePasswordEventHandler*</span><span class="sxs-lookup"><span data-stu-id="f2767-369">*System.Web.Security.MembershipValidatePasswordEventHandler*</span></span>
- <span data-ttu-id="f2767-370">*System.web. Security. ValidatePasswordEventArgs*</span><span class="sxs-lookup"><span data-stu-id="f2767-370">*System.Web.Security.ValidatePasswordEventArgs*</span></span>
- <span data-ttu-id="f2767-371">*System.web. Security. RoleProvider*</span><span class="sxs-lookup"><span data-stu-id="f2767-371">*System.Web.Security.RoleProvider*</span></span>
- <a id="0.1_a"></a><span data-ttu-id="f2767-372">*System.web. MembershipPasswordCompatibilityMode*</span><span class="sxs-lookup"><span data-stu-id="f2767-372">*System.Web.Configuration.MembershipPasswordCompatibilityMode*</span></span>

<a id="0.1__Toc256770157"></a>

## <a name="output-caching-changes-to-vary--http-header"></a><span data-ttu-id="f2767-373">輸出快取變更為不同的 \* HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="f2767-373">Output Caching Changes to Vary \* HTTP Header</span></span>

<span data-ttu-id="f2767-374">在 ASP.NET 1.0 中，bug 導致指定 `Location="ServerAndClient"` 的快取頁面做為輸出–快取設定，以在回應中發出 `Vary:*` HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="f2767-374">In ASP.NET 1.0, a bug caused cached pages that specified `Location="ServerAndClient"` as an output–cache setting to emit a `Vary:*` HTTP header in the response.</span></span> <span data-ttu-id="f2767-375">這會影響如何告知用戶端瀏覽器永遠不要在本機快取頁面。</span><span class="sxs-lookup"><span data-stu-id="f2767-375">This had the effect of telling client browsers to never cache the page locally.</span></span>

<span data-ttu-id="f2767-376">在 ASP.NET 1.1 中，已新增**HttpCachePolicy. SetOmitVaryStar**方法，您可以呼叫它來隱藏 `Vary:*` 標頭。</span><span class="sxs-lookup"><span data-stu-id="f2767-376">In ASP.NET 1.1, the **System.Web.HttpCachePolicy.SetOmitVaryStar** method was added, which you could call to suppress the `Vary:*` header.</span></span> <span data-ttu-id="f2767-377">已選擇這個方法，因為變更發出的 HTTP 標頭在當時已被視為可能的重大變更。</span><span class="sxs-lookup"><span data-stu-id="f2767-377">This method was chosen because changing the emitted HTTP header was considered a potentially breaking change at the time.</span></span> <span data-ttu-id="f2767-378">不過，開發人員已被 ASP.NET 中的行為搞混，而 bug 報告則建議開發人員不知道現有的**SetOmitVaryStar**行為。</span><span class="sxs-lookup"><span data-stu-id="f2767-378">However, developers have been confused by the behavior in ASP.NET, and bug reports suggest that developers are unaware of the existing **SetOmitVaryStar** behavior.</span></span>

<span data-ttu-id="f2767-379">在 ASP.NET 4 中，決策是為了修正根本問題而做出的。</span><span class="sxs-lookup"><span data-stu-id="f2767-379">In ASP.NET 4, the decision was made to fix the root problem.</span></span> <span data-ttu-id="f2767-380">不會再從指定下列指示詞的回應發出 `Vary:*` HTTP 標頭：</span><span class="sxs-lookup"><span data-stu-id="f2767-380">The `Vary:*` HTTP header is no longer emitted from responses that specify the following directive:</span></span>

`<%@OutputCache Location="ServerAndClient" %>`

<span data-ttu-id="f2767-381">因此，不需要**SetOmitVaryStar**就能隱藏 `Vary:*` 標頭。</span><span class="sxs-lookup"><span data-stu-id="f2767-381">As a result, **SetOmitVaryStar** is no longer needed in order to suppress the `Vary:*` header.</span></span>

<span data-ttu-id="f2767-382">在在頁面上的 **@ OutputCache**指示詞中指定 `Location="ServerAndClient"` 的應用程式中，您現在會看到**Location**屬性的值所隱含的行為，也就是可以在瀏覽器中快取頁面，而不需要呼叫**SetOmitVaryStar**方法。</span><span class="sxs-lookup"><span data-stu-id="f2767-382">In applications that specify `Location="ServerAndClient"` in the **@ OutputCache** directive on a page, you will now see the behavior implied by the name of the **Location** attribute's value – that is, pages will be cacheable in the browser without requiring that you call the **SetOmitVaryStar** method.</span></span>

<span data-ttu-id="f2767-383">如果您應用程式中的頁面必須發出 `Vary:*`，請呼叫**AppendHeader**方法，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f2767-383">If pages in your application must emit `Vary:*`, call the **AppendHeader** method, as in the following example:</span></span>

`HttpResponse.AppendHeader("Vary","*");`

<span data-ttu-id="f2767-384">或者，您可以將 [輸出快取**位置**] 屬性的值變更為 [伺服器]。</span><span class="sxs-lookup"><span data-stu-id="f2767-384">Alternatively, you can change the value of the output caching **Location** attribute to "Server".</span></span>

<a id="0.1__Toc255587646"></a><a id="0.1__Toc256770158"></a>

## <a name="systemwebsecurity-types-for-passport-are-obsolete"></a><span data-ttu-id="f2767-385">Passport 的安全性類型已過時</span><span class="sxs-lookup"><span data-stu-id="f2767-385">System.Web.Security Types for Passport are Obsolete</span></span>

<span data-ttu-id="f2767-386">ASP.NET 2.0 內建的 Passport 支援已經過時，而且因為 Passport 的變更（現在是 LiveID）而不支援幾年。</span><span class="sxs-lookup"><span data-stu-id="f2767-386">The Passport support built into ASP.NET 2.0 has been obsolete and unsupported for a few years due to changes in Passport (now LiveID).</span></span> <span data-ttu-id="f2767-387">因此，與**system.web**中的 Passport 相關的五種類型現在會以**ObsoleteAttribute**屬性標記。</span><span class="sxs-lookup"><span data-stu-id="f2767-387">As a result, the five types related to Passport in **System.Web.Security** are now marked with the **ObsoleteAttribute** attribute.</span></span>

<a id="0.1__The_MenuItem.PopOutImageUrl_Propert"></a><a id="0.1__Toc256770159"></a>

## <a name="the-menuitempopoutimageurl-property-fails-to-render-an-image-in-aspnet-4"></a><span data-ttu-id="f2767-388">PopOutImageUrl 屬性無法轉譯 ASP.NET 4 中的影像</span><span class="sxs-lookup"><span data-stu-id="f2767-388">The MenuItem.PopOutImageUrl Property Fails to Render an Image in ASP.NET 4</span></span>

<span data-ttu-id="f2767-389">在 ASP.NET 3.5 中， *PopOutImageUrl*屬性可讓您指定功能表項目中顯示之影像的 URL，以指出功能表項目具有動態子功能表。</span><span class="sxs-lookup"><span data-stu-id="f2767-389">In ASP.NET 3.5, the *MenuItem.PopOutImageUrl* property lets you specify the URL for an image that is displayed in a menu item to indicate that the menu item has a dynamic submenu.</span></span> <span data-ttu-id="f2767-390">下列範例顯示如何在 ASP.NET 3.5 的標記中指定此屬性。</span><span class="sxs-lookup"><span data-stu-id="f2767-390">The following example shows how to specify this property in markup in ASP.NET 3.5.</span></span>

[!code-aspx[Main](breaking-changes/samples/sample11.aspx)]

<span data-ttu-id="f2767-391">由於 ASP.NET 4 中的設計變更，如果為*MenuItem*類別設定了屬性，則不會呈現*PopOutImageUrl*的輸出。</span><span class="sxs-lookup"><span data-stu-id="f2767-391">As a result of a design change in ASP.NET 4, no output is rendered for the *PopOutImageUrl* if the property is set for the *MenuItem* class.</span></span> <span data-ttu-id="f2767-392">您必須改為使用*StaticPopOutImageUrl*屬性或*DynamicPopOutImageUrl*屬性，直接在*MENU*控制項中指定影像 URL。</span><span class="sxs-lookup"><span data-stu-id="f2767-392">Instead, you must specify an image URL directly in the *Menu* control using either the *StaticPopOutImageUrl* property or the *DynamicPopOutImageUrl* property.</span></span> <span data-ttu-id="f2767-393">當您使用靜態功能表時， *StaticPopOutImageUrl*屬性會指定要顯示之影像的 URL，以指出靜態功能表項目具有子功能表，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f2767-393">When you work with a static menu, the *Menu.StaticPopOutImageUrl* property specifies the URL for an image that is displayed in order to indicate that the static menu item has a submenu, as shown in the following example:</span></span>

[!code-aspx[Main](breaking-changes/samples/sample12.aspx)]

<span data-ttu-id="f2767-394">如果您要使用動態功能表，請使用*DynamicPopOutImageUrl*屬性來指定影像的 URL，表示動態功能表項目具有子功能表。</span><span class="sxs-lookup"><span data-stu-id="f2767-394">If you are working with a dynamic menu, you use the *Menu.DynamicPopOutImageUrl* property to specify the URL for an image that indicates that a dynamic menu item has a submenu.</span></span> <span data-ttu-id="f2767-395">下列範例與上一個範例類似，但會顯示如何設定動態功能表的*DynamicPopOutImageUrl*屬性。</span><span class="sxs-lookup"><span data-stu-id="f2767-395">The following example is similar to the previous one, but shows how to set the *DynamicPopOutImageUrl* property for a dynamic menu.</span></span>

[!code-aspx[Main](breaking-changes/samples/sample13.aspx)]

<span data-ttu-id="f2767-396">如果未設定*DynamicPopOutImageUrl*屬性，而且*DynamicEnableDefaultPopOutImage*屬性設定為*false*，則不會顯示任何影像。</span><span class="sxs-lookup"><span data-stu-id="f2767-396">If the *Menu.DynamicPopOutImageUrl* property is not set and the *Menu.DynamicEnableDefaultPopOutImage* property is set to *false*, no image is displayed.</span></span> <span data-ttu-id="f2767-397">同樣地，如果未設定*StaticPopOutImageUrl*屬性，而且*StaticEnableDefaultPopOutImage*屬性設定為*false*，則不會顯示任何影像。</span><span class="sxs-lookup"><span data-stu-id="f2767-397">Similarly, if the *StaticPopOutImageUrl* property is not set and the *StaticEnableDefaultPopOutImage* property is set to *false*, no image is displayed.</span></span>

<span data-ttu-id="f2767-398">當您設定這些屬性的路徑時，請使用正斜線（/），而不是反斜線（\)。</span><span class="sxs-lookup"><span data-stu-id="f2767-398">When you set the paths for these properties, use a forward slash (/) instead of a backslash (\).</span></span> <span data-ttu-id="f2767-399">如需詳細資訊，請參閱[StaticPopOutImageUrl 和 menu。當路徑包含](#0.1__Menu.StaticPopOutImageUrl_and_Menu. "_Menu。 StaticPopOutImageUrl_and_Menu。")本檔中其他位置的反斜線時，DynamicPopOutImageUrl 無法轉譯影像。</span><span class="sxs-lookup"><span data-stu-id="f2767-399">For more information, see [Menu.StaticPopOutImageUrl and Menu.DynamicPopOutImageUrl Fail to Render Images When Paths Contain Backslashes](#0.1__Menu.StaticPopOutImageUrl_and_Menu. "_Menu.StaticPopOutImageUrl_and_Menu.") elsewhere in this document.</span></span>

<a id="0.1__Menu.StaticPopOutImageUrl_and_Menu."></a><a id="0.1__Toc256770160"></a>

## <a name="menustaticpopoutimageurl-and-menudynamicpopoutimageurl-fail-to-render-images-when-paths-contain-backslashes"></a><span data-ttu-id="f2767-400">StaticPopOutImageUrl 和 Menu. DynamicPopOutImageUrl 無法在路徑包含反斜線時呈現影像</span><span class="sxs-lookup"><span data-stu-id="f2767-400">Menu.StaticPopOutImageUrl and Menu.DynamicPopOutImageUrl Fail to Render Images When Paths Contain Backslashes</span></span>

<span data-ttu-id="f2767-401">在 ASP.NET 4 中，如果路徑包含 backlashes （\)，則使用*StaticPopOutImageUrl*和*menu. DynamicPopOutImageUrl*屬性所指定的影像將不會呈現。</span><span class="sxs-lookup"><span data-stu-id="f2767-401">In ASP.NET 4, the images that you specify using the *Menu.StaticPopOutImageUrl* and *Menu.DynamicPopOutImageUrl* properties will not render if the path contains backlashes (\).</span></span> <span data-ttu-id="f2767-402">這是舊版 ASP.NET 的變更。</span><span class="sxs-lookup"><span data-stu-id="f2767-402">This is a change from earlier versions of ASP.NET.</span></span>

<span data-ttu-id="f2767-403">下列*Menu*控制項標記範例顯示使用包含反斜線的路徑所設定的*StaticPopOutImageUrl*屬性。</span><span class="sxs-lookup"><span data-stu-id="f2767-403">The following example of *Menu* control markup shows the *StaticPopOutImageUrl* property set using a path that contains a backslash.</span></span> <span data-ttu-id="f2767-404">在 ASP.NET 4 中，屬性中指定的影像將不會呈現。</span><span class="sxs-lookup"><span data-stu-id="f2767-404">In ASP.NET 4, the image specified in the property will not render.</span></span>

[!code-aspx[Main](breaking-changes/samples/sample14.aspx)]

<span data-ttu-id="f2767-405">若要更正此問題，請將*StaticPopOutImageUrl*和*DynamicPopOutImageUrl*屬性中指定的路徑值變更為使用正斜線（/）。</span><span class="sxs-lookup"><span data-stu-id="f2767-405">To correct this issue, change path values that are specified in the *StaticPopOutImageUrl* and *DynamicPopOutImageUrl* properties to use forward slashes (/).</span></span> <span data-ttu-id="f2767-406">下列範例會顯示這項變更：</span><span class="sxs-lookup"><span data-stu-id="f2767-406">The following example shows this change:</span></span>

[!code-aspx[Main](breaking-changes/samples/sample15.aspx)]

<span data-ttu-id="f2767-407">請注意，從舊版 ASP.NET 遷移至 ASP.NET 4 的應用程式可能也會受到影響，因為*PopOutImageUrl*屬性已經變更。</span><span class="sxs-lookup"><span data-stu-id="f2767-407">Note that applications that were migrated from earlier versions of ASP.NET to ASP.NET 4 might also be affected, because the *MenuItem.PopOutImageUrl* property has been changed.</span></span> <span data-ttu-id="f2767-408">如需詳細資訊，請參閱本檔中其他位置[的 PopOutImageUrl 屬性無法轉譯 ASP.NET 4 中的影像](#0.1__The_MenuItem.PopOutImageUrl_Propert "_The_MenuItem。 PopOutImageUrl_Propert")。</span><span class="sxs-lookup"><span data-stu-id="f2767-408">For more information, see [The MenuItem.PopOutImageUrl Property Fails to Render an Image in ASP.NET 4](#0.1__The_MenuItem.PopOutImageUrl_Propert "_The_MenuItem.PopOutImageUrl_Propert") elsewhere in this document.</span></span>

<a id="0.1__Toc224729061"></a><a id="0.1__Toc255587647"></a><a id="0.1__Toc256770161"></a>

## <a name="disclaimer"></a><span data-ttu-id="f2767-409">免責聲明</span><span class="sxs-lookup"><span data-stu-id="f2767-409">Disclaimer</span></span>

<span data-ttu-id="f2767-410">這是一份初稿，內容在本文所述的軟體於正式商業發行前都可能有所更動。</span><span class="sxs-lookup"><span data-stu-id="f2767-410">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="f2767-411">本文件中的資訊表示直到文件發行日前 Microsoft Corporation 針對問題的看法。</span><span class="sxs-lookup"><span data-stu-id="f2767-411">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="f2767-412">Microsoft 必須因應不斷變化的市場狀況，因此本文件不代表 Microsoft 的保證，且 Microsoft 不保證這些資訊在文件發行後的正確性。</span><span class="sxs-lookup"><span data-stu-id="f2767-412">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="f2767-413">本技術白皮書僅供參考。</span><span class="sxs-lookup"><span data-stu-id="f2767-413">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="f2767-414">MICROSOFT 對本文件中的資訊不提供任何明示、暗示或法定擔保。</span><span class="sxs-lookup"><span data-stu-id="f2767-414">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="f2767-415">承諾遵守所有適用的著作權法是使用者的責任。</span><span class="sxs-lookup"><span data-stu-id="f2767-415">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="f2767-416">著作權法沒有針對某種權利加以限制，但在未獲得 Microsoft Corporation 書面同意的情況下，本文件的任何部分不得複製、以檢索系統存放或擷取、以任何形式或方法傳送 (電子、機械、影像複製、錄音或其他任何方法)、或基於任何其他不良意圖。</span><span class="sxs-lookup"><span data-stu-id="f2767-416">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="f2767-417">本文件所提及的主要事務，Microsoft 得擁有專利、專利應用程式、商標、著作權或其他智慧財產權。</span><span class="sxs-lookup"><span data-stu-id="f2767-417">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="f2767-418">除了 Microsoft 於授權合約書中書面提供的之外，本文件所述內容並未賦予您這些專利、商標、著作權、或其他智慧財產的任何授權或使用權利。</span><span class="sxs-lookup"><span data-stu-id="f2767-418">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="f2767-419">除非另有說明，否則此處所描述的範例公司、組織、產品、功能變數名稱、電子郵件地址、商標、人員、地點及事件均屬虛構，而且不會與任何真實的公司、組織、產品、功能變數名稱、電子郵件相關。位址、標誌、人員、地點或事件的預定或應加以推斷。</span><span class="sxs-lookup"><span data-stu-id="f2767-419">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="f2767-420">© 2010 Microsoft Corporation。</span><span class="sxs-lookup"><span data-stu-id="f2767-420">© 2010 Microsoft Corporation.</span></span> <span data-ttu-id="f2767-421">著作權所有，並保留一切權利。</span><span class="sxs-lookup"><span data-stu-id="f2767-421">All rights reserved.</span></span>

<span data-ttu-id="f2767-422">Microsoft 和 Windows 是 Microsoft Corporation 在美國及/或其他國家/地區的註冊商標或商標。</span><span class="sxs-lookup"><span data-stu-id="f2767-422">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="f2767-423">本文件中所提實際公司和產品，可能為各所有人所有之商標。</span><span class="sxs-lookup"><span data-stu-id="f2767-423">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
