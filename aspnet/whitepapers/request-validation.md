---
uid: whitepapers/request-validation
title: 要求驗證-防止腳本攻擊 |Microsoft Docs
author: rick-anderson
description: 本檔說明 ASP.NET 的要求驗證功能，根據預設，應用程式無法處理未編碼的 HTML 內容 submitt 。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: fa429113-5f8f-4ef4-97c5-5c04900a19fa
msc.legacyurl: /whitepapers/request-validation
msc.type: content
ms.openlocfilehash: 807cccd6fe1acdd6359b014387abd3878840d4cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640844"
---
# <a name="request-validation---preventing-script-attacks"></a><span data-ttu-id="abf98-103">要求驗證 - 防止指令碼攻擊</span><span class="sxs-lookup"><span data-stu-id="abf98-103">Request Validation - Preventing Script Attacks</span></span>

> <span data-ttu-id="abf98-104">本檔描述 ASP.NET 的要求驗證功能，其中，應用程式預設會防止處理提交至伺服器的未編碼 HTML 內容。</span><span class="sxs-lookup"><span data-stu-id="abf98-104">This paper describes the request validation feature of ASP.NET where, by default, the application is prevented from processing unencoded HTML content submitted to the server.</span></span> <span data-ttu-id="abf98-105">當應用程式設計成安全地處理 HTML 資料時，可以停用此要求驗證功能。</span><span class="sxs-lookup"><span data-stu-id="abf98-105">This request validation feature can be disabled when the application has been designed to safely process HTML data.</span></span>
> 
> <span data-ttu-id="abf98-106">適用于 ASP.NET 1.1 和 ASP.NET 2.0。</span><span class="sxs-lookup"><span data-stu-id="abf98-106">Applies to ASP.NET 1.1 and ASP.NET 2.0.</span></span>

<span data-ttu-id="abf98-107">要求驗證 (1.1 版後的 ASP.NET 功能) 可防止伺服器接受包含未編碼 HTML 的內容。</span><span class="sxs-lookup"><span data-stu-id="abf98-107">Request validation, a feature of ASP.NET since version 1.1, prevents the server from accepting content containing un-encoded HTML.</span></span> <span data-ttu-id="abf98-108">這項功能設計用來協助防止某些指令碼資料隱碼攻擊，因此不知不覺地將用戶端指令碼或 HTML 提交至伺服器、加以儲存，而後呈現給其他使用者。</span><span class="sxs-lookup"><span data-stu-id="abf98-108">This feature is designed to help prevent some script-injection attacks whereby client script code or HTML can be unknowingly submitted to a server, stored, and then presented to other users.</span></span> <span data-ttu-id="abf98-109">我們仍強烈建議您驗證所有輸入資料，而且適時進行 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="abf98-109">We still strongly recommend that you validate all input data and HTML encode it when appropriate.</span></span>

<span data-ttu-id="abf98-110">例如，您建立的網頁會要求使用者的電子郵件地址，然後將該電子郵件地址儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="abf98-110">For example, you create a Web page that requests a user's email address and then stores that email address in a database.</span></span> <span data-ttu-id="abf98-111">如果使用者輸入 &lt;腳本&gt;警示（"hello from SCRIPT"）&lt;/SCRIPT&gt; 而不是有效的電子郵件地址，則在呈現該資料時，如果未正確編碼內容，則可以執行此腳本。</span><span class="sxs-lookup"><span data-stu-id="abf98-111">If the user enters &lt;SCRIPT&gt;alert("hello from script")&lt;/SCRIPT&gt; instead of a valid email address, when that data is presented, this script can be executed if the content was not properly encoded.</span></span> <span data-ttu-id="abf98-112">ASP.NET 的要求驗證功能可防止發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="abf98-112">The request validation feature of ASP.NET prevents this from happening.</span></span>

## <a name="why-this-feature-is-useful"></a><span data-ttu-id="abf98-113">這項功能很有用的原因</span><span class="sxs-lookup"><span data-stu-id="abf98-113">Why this feature is useful</span></span>

<span data-ttu-id="abf98-114">許多網站並不知道它們已開放給簡單的腳本插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="abf98-114">Many sites are not aware that they are open to simple script injection attacks.</span></span> <span data-ttu-id="abf98-115">無論這些攻擊的目的是要藉由顯示 HTML 來 deface 網站，還是可能執行用戶端腳本將使用者重新導向駭客的網站，腳本插入式攻擊就是 Web 開發人員必須對抗的問題。</span><span class="sxs-lookup"><span data-stu-id="abf98-115">Whether the purpose of these attacks is to deface the site by displaying HTML, or to potentially execute client script to redirect the user to a hacker's site, script injection attacks are a problem that Web developers must contend with.</span></span>

<span data-ttu-id="abf98-116">腳本插入式攻擊是所有 網頁程式開發人員的顧慮，無論是使用 ASP.NET、ASP 或其他 網頁程式開發技術。</span><span class="sxs-lookup"><span data-stu-id="abf98-116">Script injection attacks are a concern of all web developers, whether they are using ASP.NET, ASP, or other web development technologies.</span></span>

<span data-ttu-id="abf98-117">ASP.NET 要求驗證功能藉由不允許伺服器處理未編碼的 HTML 內容，而主動預防這些攻擊，除非開發人員決定允許該內容。</span><span class="sxs-lookup"><span data-stu-id="abf98-117">The ASP.NET request validation feature proactively prevents these attacks by not allowing unencoded HTML content to be processed by the server unless the developer decides to allow that content.</span></span>

## <a name="what-to-expect-error-page"></a><span data-ttu-id="abf98-118">預期的內容：錯誤頁面</span><span class="sxs-lookup"><span data-stu-id="abf98-118">What to expect: Error Page</span></span>

<span data-ttu-id="abf98-119">下列螢幕擷取畫面顯示一些範例 ASP.NET 程式碼：</span><span class="sxs-lookup"><span data-stu-id="abf98-119">The screen shot below shows some sample ASP.NET code:</span></span>

![](request-validation/_static/image1.png)

<span data-ttu-id="abf98-120">執行此程式碼會產生一個簡單的頁面，讓您在文字方塊中輸入一些文字，按一下按鈕，然後在 [標籤] 控制項中顯示文字：</span><span class="sxs-lookup"><span data-stu-id="abf98-120">Running this code results in a simple page that allows you to enter some text in the textbox, click the button, and display the text in the label control:</span></span>

![](request-validation/_static/image2.png)

<span data-ttu-id="abf98-121">不過，是 JavaScript，例如輸入和提交 `<script>alert("hello!")</script>`，我們會收到例外狀況：</span><span class="sxs-lookup"><span data-stu-id="abf98-121">However, were JavaScript, such as `<script>alert("hello!")</script>` to be entered and submitted we would get an exception:</span></span>

![](request-validation/_static/image3.png)

<span data-ttu-id="abf98-122">錯誤訊息指出「可能有危險的要求。偵測到表單值」，並在描述中提供更多詳細資料以瞭解發生了什麼事，以及如何變更行為。</span><span class="sxs-lookup"><span data-stu-id="abf98-122">The error message states that a 'potentially dangerous Request.Form value was detected' and provides more details in the description as to exactly what occurred and how to change the behavior.</span></span> <span data-ttu-id="abf98-123">例如:</span><span class="sxs-lookup"><span data-stu-id="abf98-123">For example:</span></span>

<span data-ttu-id="abf98-124">要求驗證偵測到潛在危險的用戶端輸入值，而且要求的處理已中止。</span><span class="sxs-lookup"><span data-stu-id="abf98-124">Request validation has detected a potentially dangerous client input value, and processing of the request has been aborted.</span></span> <span data-ttu-id="abf98-125">這個值可能表示嘗試危害應用程式的安全性，例如跨網站腳本攻擊。</span><span class="sxs-lookup"><span data-stu-id="abf98-125">This value may indicate an attempt to compromise the security of your application, such as a cross-site scripting attack.</span></span> <span data-ttu-id="abf98-126">您可以藉由在頁面指示詞或設定區段中設定 `validateRequest=false`，來停用要求驗證。</span><span class="sxs-lookup"><span data-stu-id="abf98-126">You can disable request validation by setting `validateRequest=false` in the Page directive or in the configuration section.</span></span> <span data-ttu-id="abf98-127">不過，強烈建議您的應用程式在此情況下明確檢查所有輸入。</span><span class="sxs-lookup"><span data-stu-id="abf98-127">However, it is strongly recommended that your application explicitly check all inputs in this case.</span></span>

## <a name="disabling-request-validation-on-a-page"></a><span data-ttu-id="abf98-128">停用頁面上的要求驗證</span><span class="sxs-lookup"><span data-stu-id="abf98-128">Disabling request validation on a page</span></span>

<span data-ttu-id="abf98-129">若要停用頁面上的要求驗證，您必須將 Page 指示詞的 `validateRequest` 屬性設定為 `false`：</span><span class="sxs-lookup"><span data-stu-id="abf98-129">To disable request validation on a page you must set the `validateRequest` attribute of the Page directive to `false`:</span></span>

[!code-aspx[Main](request-validation/samples/sample1.aspx)]

> [!CAUTION]
> <span data-ttu-id="abf98-130">停用要求驗證時，可以將內容提交至頁面;網頁開發人員必須負責確保內容經過正確編碼或處理。</span><span class="sxs-lookup"><span data-stu-id="abf98-130">When request validation is disabled, content can be submitted to a page; it is the responsibility of the page developer to ensure that content is properly encoded or processed.</span></span>

## <a name="disabling-request-validation-for-your-application"></a><span data-ttu-id="abf98-131">停用應用程式的要求驗證</span><span class="sxs-lookup"><span data-stu-id="abf98-131">Disabling request validation for your application</span></span>

<span data-ttu-id="abf98-132">若要停用應用程式的要求驗證，您必須修改或建立應用程式的 web.config 檔案，並將 `<pages />` 區段的 validateRequest 屬性設定為 `false`：</span><span class="sxs-lookup"><span data-stu-id="abf98-132">To disable request validation for your application, you must modify or create a Web.config file for your application and set the validateRequest attribute of the `<pages />` section to `false`:</span></span>

[!code-xml[Main](request-validation/samples/sample2.xml)]

<span data-ttu-id="abf98-133">如果您想要停用伺服器上所有應用程式的要求驗證，可以對您的 Machine.config 檔案進行這種修改。</span><span class="sxs-lookup"><span data-stu-id="abf98-133">If you wish to disable request validation for all applications on your server, you can make this modification to your Machine.config file.</span></span>

> [!CAUTION]
> <span data-ttu-id="abf98-134">停用要求驗證時，可以將內容提交至您的應用程式;應用程式開發人員必須負責確保正確編碼或處理內容。</span><span class="sxs-lookup"><span data-stu-id="abf98-134">When request validation is disabled, content can be submitted to your application; it is the responsibility of the application developer to ensure that content is properly encoded or processed.</span></span>

<span data-ttu-id="abf98-135">下列程式碼已修改為關閉要求驗證：</span><span class="sxs-lookup"><span data-stu-id="abf98-135">The code below is modified to turn off request validation:</span></span>

![](request-validation/_static/image4.png)

<span data-ttu-id="abf98-136">現在，如果已在文字方塊中輸入下列 JavaScript `<script>alert("hello!")</script>` 結果會是：</span><span class="sxs-lookup"><span data-stu-id="abf98-136">Now if the following JavaScript was entered into the textbox `<script>alert("hello!")</script>` the result would be:</span></span>

![](request-validation/_static/image5.png)

<span data-ttu-id="abf98-137">為了避免發生這種情況，在關閉要求驗證的情況下，我們需要對內容進行 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="abf98-137">To prevent this from happening, with request validation turned off, we need to HTML encode the content.</span></span>

## <a name="how-to-html-encode-content"></a><span data-ttu-id="abf98-138">如何 HTML 編碼內容</span><span class="sxs-lookup"><span data-stu-id="abf98-138">How to HTML encode content</span></span>

<span data-ttu-id="abf98-139">如果您已停用要求驗證，則對將儲存供日後使用的內容進行 HTML 編碼是很好的作法。</span><span class="sxs-lookup"><span data-stu-id="abf98-139">If you have disabled request validation, it is good practice to HTML-encode content that will be stored for future use.</span></span> <span data-ttu-id="abf98-140">HTML 編碼會自動將任何 '&lt;' 或 '&gt;' （連同其他數個符號）取代為其對應的 HTML 編碼表示。</span><span class="sxs-lookup"><span data-stu-id="abf98-140">HTML encoding will automatically replace any ‘&lt;' or ‘&gt;' (together with several other symbols) with their corresponding HTML encoded representation.</span></span> <span data-ttu-id="abf98-141">例如，'&lt;' 已由 '&amp;lt; ' 取代，而 '&gt;' 已由 '&amp;gt; ' 取代。</span><span class="sxs-lookup"><span data-stu-id="abf98-141">For example, ‘&lt;' is replaced by ‘&amp;lt;' and ‘&gt;' is replaced by ‘&amp;gt;'.</span></span> <span data-ttu-id="abf98-142">瀏覽器會使用這些特殊代碼，在瀏覽器中顯示 '&lt;' 或 '&gt;'。</span><span class="sxs-lookup"><span data-stu-id="abf98-142">Browsers use these special codes to display the ‘&lt;' or ‘&gt;' in the browser.</span></span>

<span data-ttu-id="abf98-143">您可以使用 `Server.HtmlEncode(string)` API，輕鬆地在伺服器上以 HTML 編碼內容。</span><span class="sxs-lookup"><span data-stu-id="abf98-143">Content can be easily HTML-encoded on the server using the `Server.HtmlEncode(string)` API.</span></span> <span data-ttu-id="abf98-144">內容也可以輕易地進行 HTML 解碼，也就是使用 `Server.HtmlDecode(string)` 方法還原為標準 HTML。</span><span class="sxs-lookup"><span data-stu-id="abf98-144">Content can also be easily HTML-decoded, that is, reverted back to standard HTML using the `Server.HtmlDecode(string)` method.</span></span>

![](request-validation/_static/image6.png)

<span data-ttu-id="abf98-145">產生的結果：</span><span class="sxs-lookup"><span data-stu-id="abf98-145">Resulting in:</span></span>

![](request-validation/_static/image7.png)
