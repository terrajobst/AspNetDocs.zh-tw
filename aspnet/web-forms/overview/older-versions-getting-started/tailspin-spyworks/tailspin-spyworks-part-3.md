---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: 第3部分：版面配置和分類功能表 |Microsoft Docs
author: JoeStagner
description: 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第3部分涵蓋新增版面配置和分類功能表。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: a223b97fd362ecf73ecde431e141021c1dcc6a6d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639115"
---
# <a name="part-3-layout-and-category-menu"></a>第3部分：版面配置和分類功能表

依[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 示範為 .NET 平臺建立功能強大、可擴充的應用程式有多麼簡單。 它會說明如何使用 ASP.NET 4 中的絕佳新功能來建立線上商店，包括購物、結帳和管理。
> 
> 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第3部分涵蓋新增版面配置和分類功能表。

## <a id="_Toc260221669"></a>新增一些版面配置和分類功能表

在我們的網站主版頁面中，我們將為左側資料行新增一個 div，其中將包含產品類別目錄功能表。

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

請注意，所需的對齊和其他格式會由我們新增至 Style .css 檔案的 CSS 類別提供。

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

[產品類別目錄] 功能表將會在執行時間以動態方式建立，方法是查詢商務資料庫中現有的產品類別目錄，並建立功能表項目和對應的連結。

為了達成此目的，我們將使用兩個 ASP。NET 的強大資料控制。 「實體資料來源」控制項和「ListView」控制項。

![](tailspin-spyworks-part-3/_static/image1.jpg)

讓我們切換到「設計檢視」，並使用協助程式來設定控制項。

![](tailspin-spyworks-part-3/_static/image2.jpg)

讓我們將 [EntityDataSource ID] 屬性設為 [EDS\_類別目錄\_] 功能表，然後按一下 [設定資料來源]。

![](tailspin-spyworks-part-3/_static/image3.jpg)

選取為我們建立商務資料庫的實體資料來源模型時所建立的 CommerceEntities 連接，然後按一下 [下一步]。

![](tailspin-spyworks-part-3/_static/image4.jpg)

選取「分類」實體集名稱，並將其餘選項保留為預設值。 按一下 [完成]。

現在，讓我們將我們放在頁面上的 ListView 控制項實例的 ID 屬性，設定為 ListView\_ProductsMenu 並啟動其協助程式。

![](tailspin-spyworks-part-3/_static/image5.jpg)

雖然我們可以使用控制項選項來格式化資料項目的顯示和格式，但我們的功能表建立只需要簡單的標記，因此我們將在來源視圖中輸入程式碼。

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

請注意 "Eval" 語句： &lt;% # Eval （"類別名稱"）%&gt;

ASP.NET 語法 &lt;% #%&gt; 是一個簡短的慣例，會指示執行時間執行包含在中的任何內容，並將結果輸出「行」。

語句 Eval （「類別名稱」）會指示，對於已系結之資料項目集合中的目前專案，會提取實體模型專案名稱「類別目錄」的值。 這是非常強大的功能的簡潔語法。

讓我們立即執行應用程式。

![](tailspin-spyworks-part-3/_static/image6.jpg)

請注意，我們的 [產品類別] 功能表現在會顯示，當我們將滑鼠停留在其中一個 [類別] 功能表項目時，就會看到 [功能表項目] 連結指向我們尚未實名為 ProductsList 的頁面，而且我們已建立包含下列專案的動態查詢字串引數： 類別目錄識別碼。

> [!div class="step-by-step"]
> [上一頁](tailspin-spyworks-part-2.md)
> [下一頁](tailspin-spyworks-part-4.md)
