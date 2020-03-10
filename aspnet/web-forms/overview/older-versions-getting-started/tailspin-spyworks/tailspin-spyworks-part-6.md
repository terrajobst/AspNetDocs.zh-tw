---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: 第6部分： ASP.NET 成員資格 |Microsoft Docs
author: JoeStagner
description: 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第6部分新增 ASP.NET 成員資格。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: b0caa89dc9ffb5bb7451fa2d9d346c7db2bf1466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78564180"
---
# <a name="part-6-aspnet-membership"></a>第6部分： ASP.NET 成員資格

依[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 示範為 .NET 平臺建立功能強大、可擴充的應用程式有多麼簡單。 它會說明如何使用 ASP.NET 4 中的絕佳新功能來建立線上商店，包括購物、結帳和管理。
> 
> 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第6部分新增 ASP.NET 成員資格。

## <a id="_Toc260221672"></a>使用 ASP.NET 成員資格

![](tailspin-spyworks-part-6/_static/image1.png)

按一下 [安全性]

![](tailspin-spyworks-part-6/_static/image1.jpg)

請確定我們使用的是表單驗證。

![](tailspin-spyworks-part-6/_static/image2.jpg)

使用 [建立使用者] 連結來建立幾個使用者。

![](tailspin-spyworks-part-6/_static/image3.jpg)

完成時，請參閱 [方案總管] 視窗，並重新整理此視圖。

![](tailspin-spyworks-part-6/_static/image2.png)

請注意，ASPNETDB.MDF。MDF 已建立良好。 此檔案包含支援核心 ASP.NET 服務（例如成員資格）的資料表。

現在我們可以開始執行結帳程式。

一開始先建立一個 [CheckOut] 頁面。

只有登入的使用者才能使用 [CheckOut] 頁面，因此我們會限制登入使用者的存取權，並將未登入的使用者重新導向至登入頁面。

為此，我們會將下列內容新增至 web.config 檔案的 [設定] 區段。

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

ASP.NET Web Forms 應用程式的範本會自動將驗證區段新增至我們的 web.config 檔案，並建立預設登入頁面。

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

當使用者登入時，我們必須修改登入 .aspx 程式碼後置檔案，以遷移匿名購物車。 變更頁面\_載入事件，如下所示。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

然後，新增 "LoggedIn" 事件處理常式（如下所示），將會話名稱設定為新登入的使用者，並藉由呼叫 MyShoppingCart 類別中的 MigrateCart 方法，將購物車中的暫時會話識別碼變更為使用者。 （實作為 .cs 檔案）

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

執行 MigrateCart （）方法，如下所示。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

在 checkout 中，我們將使用 [簽出] 頁面中的 EntityDataSource 和 GridView，與我們在 [購物車] 頁面中所做的一樣。

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

請注意，GridView 控制項會指定名為 MyList\_RowDataBound 的 "ondatabound" 事件處理常式，讓我們來執行此事件處理常式，如下所示。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

此方法會在每個資料列被系結時，保留購物車的執行總計，並更新 GridView 的底部資料列。

在這個階段，我們已針對要放置的訂單，執行「評論」簡報。

讓我們藉由將幾行程式碼新增至頁面\_載入事件來處理空的購物車案例：

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

當使用者按一下 [Submit （提交）] 按鈕時，我們會在 [提交] 按鈕的 Click 事件處理常式中執行下列程式碼。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

訂單提交程式的「肉」是在我們的 MyShoppingCart 類別的 SubmitOrder （）方法中執行。

SubmitOrder 將會：

- 接受購物車中的所有明細專案，並使用它們來建立新的訂單記錄和相關聯的 OrderDetails 記錄。
- 計算出貨日期。
- 清除 [購物車]。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

基於此範例應用程式的目的，我們將計算出貨日期，只要在目前日期加上兩天。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

現在執行應用程式可讓我們從開始到結束測試購物流程。

> [!div class="step-by-step"]
> [上一頁](tailspin-spyworks-part-5.md)
> [下一頁](tailspin-spyworks-part-7.md)
