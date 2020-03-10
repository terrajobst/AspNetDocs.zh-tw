---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
title: 建立資料庫 |Microsoft Docs
author: shanselman
description: 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 建立可從資料庫讀取和寫入的簡單 web 應用程式。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 742df67f-484d-4ef3-af6b-8c791e556b43
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
msc.type: authoredcontent
ms.openlocfilehash: 995db714ce6365415d06dc458aee84a31c7c8fd6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581435"
---
# <a name="creating-a-database"></a>建立資料庫

由[Scott Hanselman](https://github.com/shanselman)

> 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 您將建立可從資料庫讀取和寫入的簡單 web 應用程式。 請造訪[ASP.NET mvc 學習中心](../../../index.md)，以尋找其他 ASP.NET mvc 教學課程和範例。

在本節中，我們將建立新的 SQL Express 資料庫，我們將用它來儲存和抓取電影資料。 從 Visual Web Developer IDE 中，選取 [View] |伺服器總管。 以滑鼠右鍵按一下 [資料連線]，然後按一下 [新增連接 ...]

![AddConnection](getting-started-with-mvc-part4/_static/image1.png)

在 [選擇資料來源] 對話方塊中，選取 Microsoft SQL Server，然後選取 [繼續]。

![](getting-started-with-mvc-part4/_static/image2.png)

在 [新增連線] 對話方塊中，為您的伺服器名稱輸入 ".\SQLEXPRESS"，並輸入「電影」作為新資料庫的名稱。

[![新增連接 對話方塊](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)

按一下 [確定]，系統會詢問您是否要建立該資料庫。 選取 [是]。

[![建立電影嗎？](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)

現在您已在伺服器總管中找到空的資料庫。

![加入新的資料表](getting-started-with-mvc-part4/_static/image7.png)

以滑鼠右鍵按一下 [資料表]，然後按一下 [加入資料表]。 資料表設計工具將會出現。 新增 Id、Title、ReleaseDate、內容類型和價格的資料行。 以滑鼠右鍵按一下 [ID] 資料行，然後按一下 [設定主要金鑰]。 我的設計區域看起來像這樣。

[![資料庫資料表編輯器](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)

此外，請選取 [識別碼] 資料行，然後在 [資料行屬性] 下方，將 [識別規格] 變更為 [是]。

[![IsIdentity-資料行屬性](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)

當您完成時，請按一下工具列中的 [儲存] 圖示，或選取 [檔案] |從功能表中儲存，並將您的資料表命名為「**電影**」（單數）。 我們擁有資料庫和資料表！

[![選擇名稱](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)

返回伺服器總管，以滑鼠右鍵按一下 [電影] 資料表，然後選取 [顯示資料表資料]。 輸入一些電影，讓我們的資料庫有一些資料。

[![資料庫資料表編輯](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)

## <a name="creating-a-model"></a>建立模型

現在，切換回 IDE 右側的 [方案總管]，並以滑鼠右鍵按一下 [模型] 資料夾，然後選取 [新增] |新專案。

[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)

我們即將從新的資料庫建立實體模型。 這會在專案中加入一組類別，讓我們能夠輕鬆地查詢和運算元據庫內的資料。 選取對話方塊左側的 [資料] 節點，然後選取 [ADO.NET 實體資料模型專案] 範本。 將它命名為 [電影 .edmx]。

[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)

按一下 [新增] 按鈕。 這會啟動「實體資料模型 Wizard」。

在彈出的新對話方塊中，選取 [從資料庫產生]。 因為我們剛剛建立了資料庫，所以只需要告訴 Entity Framework 新資料庫及其資料表的相關資訊。 按 [下一步]，在 web 應用程式的設定中儲存我們的資料庫連接。 現在，勾選 [資料表和電影] 核取方塊，然後按一下 [完成]。

[![實體資料模型 Wizard](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)

現在，我們可以在 Entity Framework Designer 中看到新的電影資料表，並從程式碼進行存取。

[![電影-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)

在設計介面上，您可以看到「電影」類別。 這個類別會對應至資料庫中的「電影」資料表，而其中的每個屬性會對應至具有資料表的資料行。 「電影」類別的每個實例都會對應到「電影」資料表中的一個資料列。

如果您不喜歡 Entity Framework 所使用的預設命名和對應慣例，可以使用 Entity Framework 設計工具來變更或自訂它們。 在此應用程式中，我們將使用預設值，並直接依自己的方式儲存檔案。

現在，讓我們來處理一些實際資料！

> [!div class="step-by-step"]
> [上一頁](getting-started-with-mvc-part3.md)
> [下一頁](getting-started-with-mvc-part5.md)
