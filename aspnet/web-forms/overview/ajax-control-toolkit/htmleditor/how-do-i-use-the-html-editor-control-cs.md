---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
title: 如何? 使用 HTML 編輯器控制項嗎？ (C#) |Microsoft Docs
author: microsoft
description: HTMLEditor 是一種 ASP.NET 的 AJAX 控制項，可讓您透過工具列中的按鈕輕鬆建立和編輯 HTML 內容。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: f47e6224-c2e5-4472-b069-b6c7b6115200
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
msc.type: authoredcontent
ms.openlocfilehash: cb7d75b59b1361abeb6d3c38ad6e42e34d6e3f7b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78577858"
---
# <a name="how-do-i-use-the-html-editor-control-c"></a><span data-ttu-id="80de6-104">如何? 使用 HTML 編輯器控制項嗎？</span><span class="sxs-lookup"><span data-stu-id="80de6-104">How do I use the HTML Editor Control?</span></span> <span data-ttu-id="80de6-105">(C#)</span><span class="sxs-lookup"><span data-stu-id="80de6-105">(C#)</span></span>

<span data-ttu-id="80de6-106">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="80de6-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="80de6-107">HTMLEditor 是一種 ASP.NET 的 AJAX 控制項，可讓您透過工具列中的按鈕輕鬆建立和編輯 HTML 內容。</span><span class="sxs-lookup"><span data-stu-id="80de6-107">HTMLEditor is an ASP.NET AJAX Control that allows you to easily create and edit HTML content via buttons in a toolbar.</span></span>

<span data-ttu-id="80de6-108">本教學課程的目的是要提供 AJAX 控制項工具組所包含的 HTML 編輯器控制項的總覽。</span><span class="sxs-lookup"><span data-stu-id="80de6-108">The goal of this tutorial is to provide you with an overview of the HTML Editor control included with the AJAX Control Toolkit.</span></span> <span data-ttu-id="80de6-109">HTML 編輯器包含變更字型大小、選取字型、變更背景色彩、修改前景色彩、加入連結、加入影像、變更文字對齊，以及執行剪下、複製和貼上作業的選項（請參閱 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="80de6-109">The HTML Editor includes options for changing font size, selecting a font, changing background color, modifying the foreground color, adding links, adding images, changing text alignment, and performing cut, copy, and paste operations (see Figure 1).</span></span>

<span data-ttu-id="80de6-110">[![HTML 編輯器](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="80de6-110">[![The HTML Editor](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="80de6-111">**圖 01**： HTML 編輯器（[按一下以查看完整大小的影像](how-do-i-use-the-html-editor-control-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="80de6-111">**Figure 01**: The HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image2.png))</span></span>

<span data-ttu-id="80de6-112">HTML 編輯器可讓您使用設計模式輸入內容，也可以直接輸入 HTML。</span><span class="sxs-lookup"><span data-stu-id="80de6-112">The HTML editor enables you to enter content using a design mode or you can enter HTML directly.</span></span> <span data-ttu-id="80de6-113">您也可以使用預覽 HTML 內容的選項來提供（請參閱 [圖 2]）。</span><span class="sxs-lookup"><span data-stu-id="80de6-113">You also are provided with the option to preview your HTML content (see Figure 2).</span></span>

<span data-ttu-id="80de6-114">[![[設計]、[HTML] 和 [預覽] 按鈕](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="80de6-114">[![Design, HTML, and Preview buttons](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)</span></span>

<span data-ttu-id="80de6-115">**圖 02**： [設計]、[HTML] 和 [預覽] 按鈕（[按一下以查看完整大小的影像](how-do-i-use-the-html-editor-control-cs/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="80de6-115">**Figure 02**: Design, HTML, and Preview buttons([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image4.png))</span></span>

<span data-ttu-id="80de6-116">在本教學課程中，您將瞭解如何顯示 HTML 編輯器、如何自訂出現在 HTML 編輯器中的工具列按鈕，以及如何避免跨網站腳本攻擊。</span><span class="sxs-lookup"><span data-stu-id="80de6-116">In this tutorial, you learn how to display the HTML Editor, how to customize the toolbar buttons that appear in the HTML Editor, and how to avoid Cross-Site Scripting Attacks.</span></span>

## <a name="displaying-the-html-editor"></a><span data-ttu-id="80de6-117">顯示 HTML 編輯器</span><span class="sxs-lookup"><span data-stu-id="80de6-117">Displaying the HTML Editor</span></span>

<span data-ttu-id="80de6-118">在 ASP.NET 網頁中使用 HTML 編輯器之前，您必須先將 ScriptManager 控制項加入至頁面。</span><span class="sxs-lookup"><span data-stu-id="80de6-118">Before you can use the HTML Editor in an ASP.NET page, you must first add a ScriptManager control to the page.</span></span> <span data-ttu-id="80de6-119">ScriptManager 控制項位於 Visual Studio/Visual Web Developer Express 工具箱的 [AJAX 擴充功能] 索引標籤底下。</span><span class="sxs-lookup"><span data-stu-id="80de6-119">The ScriptManager control is located beneath the AJAX Extensions tab in the Visual Studio/Visual Web Developer Express toolbox.</span></span>

<span data-ttu-id="80de6-120">您應該將 ScriptManager 控制項放在頁面頂端，然後再將頁面上的任何其他控制項。</span><span class="sxs-lookup"><span data-stu-id="80de6-120">You should place the ScriptManager control at the top of the page before any other controls on the page.</span></span> <span data-ttu-id="80de6-121">例如，您可以將它放在開啟伺服器端 &lt;表單&gt; 標記的正下方。</span><span class="sxs-lookup"><span data-stu-id="80de6-121">For example, you can place it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="80de6-122">HTML 編輯器控制項位於 [工具箱] 中，其中包含其餘的 AJAX 控制項工具組控制項。</span><span class="sxs-lookup"><span data-stu-id="80de6-122">The HTML Editor control is located in the toolbox with the rest of the AJAX Control Toolkit controls.</span></span> <span data-ttu-id="80de6-123">它會命名為編輯器控制項（請參閱 [圖 3]）。</span><span class="sxs-lookup"><span data-stu-id="80de6-123">It is named the Editor control (see Figure 3).</span></span>

<span data-ttu-id="80de6-124">[![HTML 編輯器控制項](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="80de6-124">[![The HTML Editor control](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)</span></span>

<span data-ttu-id="80de6-125">**圖 03**： HTML 編輯器控制項（[按一下以查看完整大小的影像](how-do-i-use-the-html-editor-control-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="80de6-125">**Figure 03**: The HTML Editor control([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image6.png))</span></span>

<span data-ttu-id="80de6-126">將 HTML 編輯器拖曳至頁面之後，您可以在屬性工作表中設定其屬性。</span><span class="sxs-lookup"><span data-stu-id="80de6-126">After you drag the HTML Editor onto a page, you can set its properties in the property sheet.</span></span> <span data-ttu-id="80de6-127">例如，您通常會想要設定 [寬度] 和 [高度] 屬性。</span><span class="sxs-lookup"><span data-stu-id="80de6-127">For example, you normally want to set the Width and Height properties.</span></span> <span data-ttu-id="80de6-128">[清單 1] 包含包含 HTML 編輯器的 ASP.NET 網頁來源。</span><span class="sxs-lookup"><span data-stu-id="80de6-128">Listing 1 contains the source for an ASP.NET page that contains an HTML editor.</span></span>

<span data-ttu-id="80de6-129">**清單 1-SimpleEditor .aspx**</span><span class="sxs-lookup"><span data-stu-id="80de6-129">**Listing 1 - SimpleEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample1.aspx)]

<span data-ttu-id="80de6-130">[清單 1] 中的頁面包含 HTML 編輯器控制項、按鈕控制項和常值控制項。</span><span class="sxs-lookup"><span data-stu-id="80de6-130">The page in Listing 1 contains an HTML Editor control, a Button control, and a Literal control.</span></span> <span data-ttu-id="80de6-131">當您按一下按鈕時，HTML 編輯器的內容就會出現在常值控制項中（請參閱 [圖 4]）。</span><span class="sxs-lookup"><span data-stu-id="80de6-131">When you click the button, the contents of the HTML Editor appear in the Literal control (see Figure 4).</span></span>

<span data-ttu-id="80de6-132">[![使用 HTML 編輯器提交表單](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="80de6-132">[![Submitting a form with an HTML Editor](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)</span></span>

<span data-ttu-id="80de6-133">**圖 04**：使用 HTML 編輯器提交表單（[按一下以觀看完整大小的影像](how-do-i-use-the-html-editor-control-cs/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="80de6-133">**Figure 04**: Submitting a form with an HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image8.png))</span></span>

<span data-ttu-id="80de6-134">HTML 編輯器的 [內容] 屬性是用來取出輸入 HTML 編輯器的 HTML 內容。</span><span class="sxs-lookup"><span data-stu-id="80de6-134">The HTML Editor Content property is used to retrieve the HTML content entered into the HTML Editor.</span></span> <span data-ttu-id="80de6-135">請注意，此 HTML 內容可以包含 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="80de6-135">Be aware that this HTML content can contain JavaScript.</span></span> <span data-ttu-id="80de6-136">在下一節中，我們會討論如何防止 JavaScript 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="80de6-136">In the next section, we discuss how you can prevent JavaScript Injection Attacks.</span></span>

## <a name="customizing-the-html-editor-toolbar"></a><span data-ttu-id="80de6-137">自訂 HTML 編輯器工具列</span><span class="sxs-lookup"><span data-stu-id="80de6-137">Customizing the HTML Editor Toolbar</span></span>

<span data-ttu-id="80de6-138">您可以完全自訂編輯器中顯示的按鈕。</span><span class="sxs-lookup"><span data-stu-id="80de6-138">You can customize exactly which buttons appear in the editor.</span></span> <span data-ttu-id="80de6-139">例如，您可能會想要移除 [HTML] 索引標籤，以防止使用者將 HTML 編輯器切換成 HTML 模式。</span><span class="sxs-lookup"><span data-stu-id="80de6-139">For example, you might want to remove the HTML tab to prevent users from switching the HTML Editor into HTML mode.</span></span> <span data-ttu-id="80de6-140">或者，您可能會想要移除 [字型大小] 下拉式清單，以防止使用者在論壇訊息貼文中建立過大的文字（請參閱 [圖 5]）。</span><span class="sxs-lookup"><span data-stu-id="80de6-140">Or, you might want to remove the font size dropdown list to prevent users from creating overly large text in a forum message post (see Figure 5).</span></span>

<span data-ttu-id="80de6-141">[![自訂的 HTML 編輯器](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="80de6-141">[![A customized HTML Editor](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)</span></span>

<span data-ttu-id="80de6-142">**圖 05**：自訂的 HTML 編輯器（[按一下以觀看完整大小的影像](how-do-i-use-the-html-editor-control-cs/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="80de6-142">**Figure 05**: A customized HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image10.png))</span></span>

<span data-ttu-id="80de6-143">您可以從基底編輯器類別衍生新的 HTML 編輯器，以自訂工具列按鈕。</span><span class="sxs-lookup"><span data-stu-id="80de6-143">You customize the toolbar buttons by deriving a new HTML Editor from the base Editor class.</span></span> <span data-ttu-id="80de6-144">例如，[清單 2] 中的自訂編輯器只包含粗體和斜體的工具列按鈕。</span><span class="sxs-lookup"><span data-stu-id="80de6-144">For example, the custom editor in Listing 2 only contains toolbar buttons for bold and italic.</span></span> <span data-ttu-id="80de6-145">所有其他工具列按鈕都已移除。</span><span class="sxs-lookup"><span data-stu-id="80de6-145">All other toolbar buttons have been removed.</span></span> <span data-ttu-id="80de6-146">此外，[HTML] 索引標籤已經從編輯器的底部移除（但是 [設計] 和 [預覽] 索引標籤仍然存在）。</span><span class="sxs-lookup"><span data-stu-id="80de6-146">Furthermore, the HTML tab has been removed from the bottom of the editor (but the Design and Preview tabs are still there).</span></span>

<span data-ttu-id="80de6-147">**清單 2-應用程式\_Code\CustomEditor.cs**</span><span class="sxs-lookup"><span data-stu-id="80de6-147">**Listing 2 - App\_Code\CustomEditor.cs**</span></span>

[!code-csharp[Main](how-do-i-use-the-html-editor-control-cs/samples/sample2.cs)]

<span data-ttu-id="80de6-148">您必須將清單2中的類別新增至您的應用程式\_Code 資料夾，才能自動編譯類別。</span><span class="sxs-lookup"><span data-stu-id="80de6-148">You must add the class in Listing 2 to your App\_Code folder so that the class will be compiled automatically.</span></span> <span data-ttu-id="80de6-149">如果應用程式\_Code 資料夾不存在於您的網站中，則您可以直接新增資料夾。</span><span class="sxs-lookup"><span data-stu-id="80de6-149">If the App\_Code folder does not exist in your website then you can simply add the folder.</span></span>

<span data-ttu-id="80de6-150">建立自訂編輯器之後，您可以使用與新增一般 HTML 編輯器相同的方式，將它加入至 ASP.NET 網頁（請參閱 [清單 3]）。</span><span class="sxs-lookup"><span data-stu-id="80de6-150">After you create a custom editor, you can add it to an ASP.NET page in the same way as you add the normal HTML Editor (see Listing 3).</span></span>

<span data-ttu-id="80de6-151">**清單 3-ShowCustomEditor .aspx**</span><span class="sxs-lookup"><span data-stu-id="80de6-151">**Listing 3 - ShowCustomEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a><span data-ttu-id="80de6-152">避免跨網站腳本（XSS）攻擊</span><span class="sxs-lookup"><span data-stu-id="80de6-152">Avoiding Cross-Site Scripting (XSS) Attacks</span></span>

<span data-ttu-id="80de6-153">每當您接受使用者輸入，並在您的網站上重新顯示該輸入時，您可能會開啟您的網站來進行跨網站腳本（XSS）攻擊。</span><span class="sxs-lookup"><span data-stu-id="80de6-153">Whenever you accept input from a user, and redisplay that input on your website, you potentially open your website to Cross-Site Scripting (XSS) Attacks.</span></span> <span data-ttu-id="80de6-154">理論上，惡意駭客可以提交在重新顯示輸入時所執行的 JavaScript 程式碼。</span><span class="sxs-lookup"><span data-stu-id="80de6-154">In theory, a malicious hacker could submit JavaScript code that gets executed when the input is redisplayed.</span></span> <span data-ttu-id="80de6-155">JavaScript 可用來竊取使用者密碼或其他機密資訊。</span><span class="sxs-lookup"><span data-stu-id="80de6-155">The JavaScript could be used to steal user passwords or other sensitive information.</span></span>

<span data-ttu-id="80de6-156">一般來說，您可以藉由 HTML 編碼從使用者抓取的任何輸入，然後在網頁中顯示，來對抗 XSS 攻擊。</span><span class="sxs-lookup"><span data-stu-id="80de6-156">Normally, you can defeat XSS attacks by HTML encoding whatever input you retrieve from a user before displaying it in a web page.</span></span> <span data-ttu-id="80de6-157">但是 html 編碼的 html 編輯器輸出不只會編碼 &lt;腳本&gt; 標記，它也會對所有 HTML 標籤進行編碼。</span><span class="sxs-lookup"><span data-stu-id="80de6-157">However, HTML encoding the output of the HTML Editor would not only encode &lt;script&gt; tags, it would also encode all HTML tags.</span></span> <span data-ttu-id="80de6-158">換句話說，您會遺失所有的格式，例如字型類型、字型大小和背景色彩。</span><span class="sxs-lookup"><span data-stu-id="80de6-158">In other words, you would lose all of the formatting such as the font type, font size, and background color.</span></span>

<span data-ttu-id="80de6-159">如果您要收集使用者的機密資訊（例如密碼、信用卡號碼和身分證號碼），則不應該顯示您使用 HTML 編輯器從使用者抓取的未編碼內容。</span><span class="sxs-lookup"><span data-stu-id="80de6-159">If you are collecting sensitive information from your users -- such as passwords, credit-card numbers, and social security numbers - then you should not display un-encoded content that you retrieve from a user with the HTML Editor.</span></span> <span data-ttu-id="80de6-160">只有當您不重新提供 HTML 內容，或 HTML 內容正由受信任的合作物件提交至您的網站時，您才應該使用 HTML 編輯器。</span><span class="sxs-lookup"><span data-stu-id="80de6-160">You should use the HTML Editor only in situations in which you are not redisplaying the HTML content, or the HTML content is being submitted to your website by a trusted party.</span></span>

<span data-ttu-id="80de6-161">例如，假設您要建立一個 blog 應用程式。</span><span class="sxs-lookup"><span data-stu-id="80de6-161">Imagine, for example, that you are creating a blog application.</span></span> <span data-ttu-id="80de6-162">在這種情況下，在撰寫 blog 文章時使用 HTML 編輯器是合理的。</span><span class="sxs-lookup"><span data-stu-id="80de6-162">In this situation, it makes sense to use the HTML Editor when composing blog posts.</span></span> <span data-ttu-id="80de6-163">您是唯一提交 blog 文章的人，而且您可能會信任自己不要提交惡意的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="80de6-163">You are the only one who submits a blog post and, presumably, you can trust yourself not to submit malicious JavaScript.</span></span> <span data-ttu-id="80de6-164">不過，在允許匿名使用者張貼留言時，使用 HTML 編輯器並不合理。</span><span class="sxs-lookup"><span data-stu-id="80de6-164">However, it does not make sense to use the HTML Editor when allowing anonymous users to post comments.</span></span> <span data-ttu-id="80de6-165">在使用者提交機密資訊（例如密碼）的情況下，您應該特別小心。</span><span class="sxs-lookup"><span data-stu-id="80de6-165">You should be especially careful in situations in which users submit sensitive information such as passwords.</span></span> <span data-ttu-id="80de6-166">惡意使用者可能會張貼包含正確 JavaScript 的批註來竊取密碼。</span><span class="sxs-lookup"><span data-stu-id="80de6-166">Potentially, a malicious user could post a comment that contains the right JavaScript for stealing a password.</span></span>

## <a name="summary"></a><span data-ttu-id="80de6-167">總結</span><span class="sxs-lookup"><span data-stu-id="80de6-167">Summary</span></span>

<span data-ttu-id="80de6-168">在本教學課程中，您已提供 AJAX 控制項工具組中所包含的 HTML 編輯器控制項的簡要總覽。</span><span class="sxs-lookup"><span data-stu-id="80de6-168">In this tutorial, you were provided with a brief overview of the HTML Editor control included in the AJAX Control Toolkit.</span></span> <span data-ttu-id="80de6-169">您已瞭解如何使用 HTML 編輯器來接受使用者的豐富內容，並將內容提交至伺服器。</span><span class="sxs-lookup"><span data-stu-id="80de6-169">You learned how to use the HTML Editor to accept rich content from a user and submit the content to the server.</span></span> <span data-ttu-id="80de6-170">我們也會討論如何自訂 HTML 編輯器所顯示的工具列按鈕。</span><span class="sxs-lookup"><span data-stu-id="80de6-170">We also discussed how you can customize the toolbar buttons that are displayed by the HTML Editor.</span></span> <span data-ttu-id="80de6-171">最後，您已瞭解如何在使用 HTML 編輯器來接受潛在的惡意輸入時，避免跨網站腳本攻擊。</span><span class="sxs-lookup"><span data-stu-id="80de6-171">Finally, you learned how to avoid Cross-Site Scripting Attacks when using the HTML Editor to accept potentially malicious input.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="80de6-172">下一個</span><span class="sxs-lookup"><span data-stu-id="80de6-172">Next</span></span>](how-do-i-use-the-html-editor-control-vb.md)
