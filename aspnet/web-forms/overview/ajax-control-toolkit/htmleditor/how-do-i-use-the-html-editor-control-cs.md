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
# <a name="how-do-i-use-the-html-editor-control-c"></a>如何? 使用 HTML 編輯器控制項嗎？ (C#)

由[Microsoft](https://github.com/microsoft)

> HTMLEditor 是一種 ASP.NET 的 AJAX 控制項，可讓您透過工具列中的按鈕輕鬆建立和編輯 HTML 內容。

本教學課程的目的是要提供 AJAX 控制項工具組所包含的 HTML 編輯器控制項的總覽。 HTML 編輯器包含變更字型大小、選取字型、變更背景色彩、修改前景色彩、加入連結、加入影像、變更文字對齊，以及執行剪下、複製和貼上作業的選項（請參閱 [圖 1]）。

[![HTML 編輯器](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)

**圖 01**： HTML 編輯器（[按一下以查看完整大小的影像](how-do-i-use-the-html-editor-control-cs/_static/image2.png)）

HTML 編輯器可讓您使用設計模式輸入內容，也可以直接輸入 HTML。 您也可以使用預覽 HTML 內容的選項來提供（請參閱 [圖 2]）。

[![[設計]、[HTML] 和 [預覽] 按鈕](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)

**圖 02**： [設計]、[HTML] 和 [預覽] 按鈕（[按一下以查看完整大小的影像](how-do-i-use-the-html-editor-control-cs/_static/image4.png)）

在本教學課程中，您將瞭解如何顯示 HTML 編輯器、如何自訂出現在 HTML 編輯器中的工具列按鈕，以及如何避免跨網站腳本攻擊。

## <a name="displaying-the-html-editor"></a>顯示 HTML 編輯器

在 ASP.NET 網頁中使用 HTML 編輯器之前，您必須先將 ScriptManager 控制項加入至頁面。 ScriptManager 控制項位於 Visual Studio/Visual Web Developer Express 工具箱的 [AJAX 擴充功能] 索引標籤底下。

您應該將 ScriptManager 控制項放在頁面頂端，然後再將頁面上的任何其他控制項。 例如，您可以將它放在開啟伺服器端 &lt;表單&gt; 標記的正下方。

HTML 編輯器控制項位於 [工具箱] 中，其中包含其餘的 AJAX 控制項工具組控制項。 它會命名為編輯器控制項（請參閱 [圖 3]）。

[![HTML 編輯器控制項](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)

**圖 03**： HTML 編輯器控制項（[按一下以查看完整大小的影像](how-do-i-use-the-html-editor-control-cs/_static/image6.png)）

將 HTML 編輯器拖曳至頁面之後，您可以在屬性工作表中設定其屬性。 例如，您通常會想要設定 [寬度] 和 [高度] 屬性。 [清單 1] 包含包含 HTML 編輯器的 ASP.NET 網頁來源。

**清單 1-SimpleEditor .aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample1.aspx)]

[清單 1] 中的頁面包含 HTML 編輯器控制項、按鈕控制項和常值控制項。 當您按一下按鈕時，HTML 編輯器的內容就會出現在常值控制項中（請參閱 [圖 4]）。

[![使用 HTML 編輯器提交表單](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)

**圖 04**：使用 HTML 編輯器提交表單（[按一下以觀看完整大小的影像](how-do-i-use-the-html-editor-control-cs/_static/image8.png)）

HTML 編輯器的 [內容] 屬性是用來取出輸入 HTML 編輯器的 HTML 內容。 請注意，此 HTML 內容可以包含 JavaScript。 在下一節中，我們會討論如何防止 JavaScript 插入式攻擊。

## <a name="customizing-the-html-editor-toolbar"></a>自訂 HTML 編輯器工具列

您可以完全自訂編輯器中顯示的按鈕。 例如，您可能會想要移除 [HTML] 索引標籤，以防止使用者將 HTML 編輯器切換成 HTML 模式。 或者，您可能會想要移除 [字型大小] 下拉式清單，以防止使用者在論壇訊息貼文中建立過大的文字（請參閱 [圖 5]）。

[![自訂的 HTML 編輯器](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)

**圖 05**：自訂的 HTML 編輯器（[按一下以觀看完整大小的影像](how-do-i-use-the-html-editor-control-cs/_static/image10.png)）

您可以從基底編輯器類別衍生新的 HTML 編輯器，以自訂工具列按鈕。 例如，[清單 2] 中的自訂編輯器只包含粗體和斜體的工具列按鈕。 所有其他工具列按鈕都已移除。 此外，[HTML] 索引標籤已經從編輯器的底部移除（但是 [設計] 和 [預覽] 索引標籤仍然存在）。

**清單 2-應用程式\_Code\CustomEditor.cs**

[!code-csharp[Main](how-do-i-use-the-html-editor-control-cs/samples/sample2.cs)]

您必須將清單2中的類別新增至您的應用程式\_Code 資料夾，才能自動編譯類別。 如果應用程式\_Code 資料夾不存在於您的網站中，則您可以直接新增資料夾。

建立自訂編輯器之後，您可以使用與新增一般 HTML 編輯器相同的方式，將它加入至 ASP.NET 網頁（請參閱 [清單 3]）。

**清單 3-ShowCustomEditor .aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a>避免跨網站腳本（XSS）攻擊

每當您接受使用者輸入，並在您的網站上重新顯示該輸入時，您可能會開啟您的網站來進行跨網站腳本（XSS）攻擊。 理論上，惡意駭客可以提交在重新顯示輸入時所執行的 JavaScript 程式碼。 JavaScript 可用來竊取使用者密碼或其他機密資訊。

一般來說，您可以藉由 HTML 編碼從使用者抓取的任何輸入，然後在網頁中顯示，來對抗 XSS 攻擊。 但是 html 編碼的 html 編輯器輸出不只會編碼 &lt;腳本&gt; 標記，它也會對所有 HTML 標籤進行編碼。 換句話說，您會遺失所有的格式，例如字型類型、字型大小和背景色彩。

如果您要收集使用者的機密資訊（例如密碼、信用卡號碼和身分證號碼），則不應該顯示您使用 HTML 編輯器從使用者抓取的未編碼內容。 只有當您不重新提供 HTML 內容，或 HTML 內容正由受信任的合作物件提交至您的網站時，您才應該使用 HTML 編輯器。

例如，假設您要建立一個 blog 應用程式。 在這種情況下，在撰寫 blog 文章時使用 HTML 編輯器是合理的。 您是唯一提交 blog 文章的人，而且您可能會信任自己不要提交惡意的 JavaScript。 不過，在允許匿名使用者張貼留言時，使用 HTML 編輯器並不合理。 在使用者提交機密資訊（例如密碼）的情況下，您應該特別小心。 惡意使用者可能會張貼包含正確 JavaScript 的批註來竊取密碼。

## <a name="summary"></a>總結

在本教學課程中，您已提供 AJAX 控制項工具組中所包含的 HTML 編輯器控制項的簡要總覽。 您已瞭解如何使用 HTML 編輯器來接受使用者的豐富內容，並將內容提交至伺服器。 我們也會討論如何自訂 HTML 編輯器所顯示的工具列按鈕。 最後，您已瞭解如何在使用 HTML 編輯器來接受潛在的惡意輸入時，避免跨網站腳本攻擊。

> [!div class="step-by-step"]
> [下一個](how-do-i-use-the-html-editor-control-vb.md)
