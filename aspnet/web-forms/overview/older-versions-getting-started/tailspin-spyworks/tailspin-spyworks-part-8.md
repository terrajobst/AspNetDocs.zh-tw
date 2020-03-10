---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: 第8部分：最後的頁面、例外狀況處理和結論 |Microsoft Docs
author: JoeStagner
description: 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第8部分新增連絡人頁面、關於頁面和例外狀況 。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 707dc9d87ae324a7897c971a451e40bc54c96cb3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586881"
---
# <a name="part-8-final-pages-exception-handling-and-conclusion"></a>第8部分：最後的頁面、例外狀況處理和結論

依[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 示範為 .NET 平臺建立功能強大、可擴充的應用程式有多麼簡單。 它會說明如何使用 ASP.NET 4 中的絕佳新功能來建立線上商店，包括購物、結帳和管理。
> 
> 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第8部分新增 [連絡人] 頁面、[關於] 頁面和例外狀況處理。 這就是數列的結論。

## <a id="_Toc260221680"></a>連絡人頁面（從 ASP.NET 傳送電子郵件）

建立名為 ContactUs 的新頁面

使用設計工具建立下列表單，採取特殊的備註，將 ToolkitScriptManager 和編輯器控制項包含在 AjaxControlToolkit 中。 。

![](tailspin-spyworks-part-8/_static/image1.jpg)

按兩下 [提交] 按鈕，以在程式碼後置檔案中產生 click 事件處理常式，並執行方法以電子郵件傳送連絡人資訊。

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

這段程式碼需要您的 web.config 檔案在 configuration 區段中包含一個專案，以指定要用於傳送郵件的 SMTP 伺服器。

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a>關於頁面

建立名為 AboutUs 的頁面，並加入您喜歡的任何內容。

## <a id="_Toc260221682"></a>全域例外狀況處理常式

最後，在整個應用程式中，我們擲回了例外狀況，而在非預期的情況下，冷也會造成 web 應用程式中的未處理例外

我們永遠不希望對網站訪客顯示未處理的例外狀況。

![](tailspin-spyworks-part-8/_static/image2.jpg)

除了是嚴重的使用者體驗未處理的例外狀況之外，也可能會造成安全性問題。

為了解決這個問題，我們將會執行全域例外狀況處理常式。

若要這麼做，請開啟 global.asax 檔案，並記下下列預先產生的事件處理常式。

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

加入程式碼以依照下列方式來執行應用程式\_錯誤處理常式。

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

然後，將名為 Error 的頁面加入至方案，並加入此標記程式碼片段。

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

現在在頁面\_載入事件處理常式會從要求物件中解壓縮錯誤訊息。

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a>結果

我們已瞭解 ASP.NET WebForms 可讓您輕鬆地建立具有資料庫存取權、成員資格、AJAX 等的精密網站。 非常快速。

希望本教學課程提供您開始建立自己的 ASP.NET WebForms 應用程式所需的工具！

> [!div class="step-by-step"]
> [上一篇](tailspin-spyworks-part-7.md)
