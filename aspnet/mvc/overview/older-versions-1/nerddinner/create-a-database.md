---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: 建立資料庫 | Microsoft 文件
author: microsoft
description: 步驟2顯示的步驟可讓您建立資料庫，以保存 NerdDinner 應用程式的所有晚餐和 RSVP 資料。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: b0aa7c8cdf741f44e09ed18e2b2f73fe6bf786ae
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581001"
---
# <a name="create-a-database"></a>建立資料庫

由[Microsoft](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟2，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。
> 
> 步驟2顯示的步驟可讓您建立資料庫，以保存 NerdDinner 應用程式的所有晚餐和 RSVP 資料。
> 
> 如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。

## <a name="nerddinner-step-2-creating-the-database"></a>NerdDinner 步驟2：建立資料庫

我們將使用資料庫來儲存 NerdDinner 應用程式的所有晚餐和 RSVP 資料。

下列步驟顯示如何使用免費的 SQL Server Express edition 來建立資料庫（您可以使用[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)的第2版輕鬆地安裝）。 我們撰寫的所有程式碼都適用于 SQL Server Express 和完整 SQL Server。

### <a name="creating-a-new-sql-server-express-database"></a>建立新的 SQL Server Express 資料庫

首先，在 Web 專案上按一下滑鼠右鍵，然後選取 [**新增-&gt;新專案**] 功能表命令：

![](create-a-database/_static/image1.png)

這會顯示 Visual Studio 的 [新增專案] 對話方塊。 我們會依 [資料] 類別篩選，並選取 [SQL Server 資料庫] 專案範本：

![](create-a-database/_static/image2.png)

我們會將您要建立的 SQL Server Express 資料庫命名為 "NerdDinner"，然後按 [確定]。 Visual Studio 接著會詢問我們是否要將此檔案新增至我們的 \App\_Data 目錄（這是已設定為讀取和寫入安全性 Acl 的目錄）：

![](create-a-database/_static/image3.png)

我們將按一下 [是]，我們將會建立新的資料庫，並將其新增至我們的方案總管：

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a>在我們的資料庫中建立資料表

我們現在有一個新的空白資料庫。 讓我們在其中新增一些資料表。

若要這麼做，我們將流覽至 Visual Studio 內的 [伺服器總管] 索引標籤視窗，讓我們管理資料庫和伺服器。 儲存在應用程式之 \App\_Data 資料夾中的 SQL Server Express 資料庫，會自動顯示在伺服器總管內。 我們可以選擇性地使用 [伺服器總管] 視窗頂端的 [連接到資料庫] 圖示，同時將額外的 SQL Server 資料庫（本機和遠端）新增至清單：

![](create-a-database/_static/image5.png)

我們會將兩個數據表新增至我們的 NerdDinner 資料庫–一個用來儲存我們的 Dinners，另一個用來追蹤對他們的 RSVP 接受。 若要建立新的資料表，請以滑鼠右鍵按一下資料庫內的 [資料表] 資料夾，然後選擇 [加入新的資料表] 功能表命令：

![](create-a-database/_static/image6.png)

這會開啟資料表設計工具，讓我們設定資料表的架構。 針對我們的「Dinners」資料表，我們將新增10個數據行：

![](create-a-database/_static/image7.png)

我們希望 "DinnerID" 資料行是資料表的唯一主鍵。 我們可以用滑鼠右鍵按一下 [DinnerID] 資料行，然後選擇 [設定主要金鑰] 功能表項目來進行設定：

![](create-a-database/_static/image8.png)

除了讓 DinnerID 成為主鍵之外，我們也想要將它設定為「身分識別」資料行，其值會隨著新增至資料表的新資料列而自動遞增（這表示第一個插入的晚餐資料列將 DinnerID 為1，第二個插入的資料列的 DinnerID 為2，依此類推）。

我們可以選取 [DinnerID] 資料行來執行這項操作，然後使用 [資料行屬性] 編輯器，將資料行上的 [（是識別）] 屬性設定為 [是]。 我們將使用標準身分識別預設值（從1開始，並在每個新的晚餐資料列遞增1）：

![](create-a-database/_static/image9.png)

接著，我們會輸入 Ctrl-S 或使用檔案&gt;的 [**儲存**] 功能表命令來儲存資料表。 這會提示我們將資料表命名為。 我們會將它命名為 "Dinners"：

![](create-a-database/_static/image10.png)

我們的新 Dinners 資料表就會顯示在伺服器 explorer 的資料庫中。

接著，我們會重複上述步驟，並建立「RSVP」資料表。 具有3個數據行的這個資料表。 我們會將 RsvpID 資料行設定為主要金鑰，並將它設為識別欄位：

![](create-a-database/_static/image11.png)

我們會儲存它，並將它命名為「RSVP」。

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a>設定資料表之間的外鍵關聯性

我們的資料庫中現在有兩個數據表。 我們的最後一個架構設計步驟是在這兩個數據表之間設定「一對多」關聯性，讓我們可以將每個晚餐資料列與套用至該資料的零或多個 RSVP 資料列產生關聯。 我們會將 RSVP 資料表的「DinnerID」資料行設定為與「Dinners」資料表中的「DinnerID」資料行具有外鍵關聯性，以達到此目的。

若要這麼做，我們要在 [資料表設計工具] 中按兩下 [RSVP] 資料表，方法是在 [伺服器瀏覽器] 中按兩下它。 然後選取其中的 "DinnerID" 資料行，按一下滑鼠右鍵，然後選擇 [關聯性 ...]內容功能表命令：

![](create-a-database/_static/image12.png)

這會出現一個對話方塊，可讓我們用來設定資料表之間的關聯性：

![](create-a-database/_static/image13.png)

我們將按一下 [新增] 按鈕，將新的關聯性新增至對話方塊。 加入關聯性之後，我們會在對話方塊右邊的屬性方格中展開 [資料表和資料行規格] 樹狀檢視節點，然後按一下 [...]按鈕的右邊：

![](create-a-database/_static/image14.png)

按一下 [...]按鈕會顯示另一個對話方塊，讓我們指定關聯性中涉及的資料表和資料行，以及讓我們命名關聯性。

我們會將主鍵資料表變更為 "Dinners"，並選取 Dinners 資料表內的 "DinnerID" 資料行作為主鍵。 我們的「RSVP」資料表會是外鍵資料表和「RSVP」。DinnerID 資料行會與外鍵建立關聯：

![](create-a-database/_static/image15.png)

此時，RSVP 資料表中的每個資料列都會與晚餐表中的資料列相關聯。 SQL Server 會為我們維護參考完整性-如果未指向有效的晚餐資料列，則會防止我們新增新的 RSVP 資料列。 如果仍有 RSVP 資料列參考資料列，也會導致我們無法刪除晚餐資料列。

### <a name="adding-data-to-our-tables"></a>將資料加入我們的資料表

讓我們透過將一些範例資料新增至我們的 Dinners 資料表來完成。 我們可以在 [伺服器總管] 中以滑鼠右鍵按一下資料表，然後選擇 [顯示資料表資料] 命令，將資料新增至資料表：

![](create-a-database/_static/image16.png)

我們會新增幾個資料列，供我們稍後開始執行應用程式時使用：

![](create-a-database/_static/image17.png)

### <a name="next-step"></a>後續步驟

我們已完成資料庫的建立。 現在讓我們建立可用來查詢和更新的模型類別。

> [!div class="step-by-step"]
> [上一頁](create-a-new-aspnet-mvc-project.md)
> [下一頁](build-a-model-with-business-rule-validations.md)
