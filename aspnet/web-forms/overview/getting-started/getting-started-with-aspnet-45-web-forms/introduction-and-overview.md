---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: ASP.NET 4.7 Web Forms 和 Visual Studio 2017 的消費者入門 |Microsoft Docs
author: Erikre
description: 此逐步教學課程系列將教您使用 ASP.NET 4.7 和 Microsoft Visual Studio 建立 ASP.NET Web Forms 應用程式的基本概念
ms.author: riande
ms.date: 01/09/2019
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: 52d5eb7abe4520ebdf6667d299d055fc7619a635
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615458"
---
# <a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2017"></a>具有 ASP.NET 4.5 Web Forms 和 Visual Studio 2017 的消費者入門

[下載 Wingtip 玩具範例專案（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下載電子書（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

本教學課程系列會說明如何建立具有 ASP.NET 4.5 和 Microsoft Visual Studio 2017 的 ASP.NET Web form 應用程式。 

## <a name="introduction"></a>簡介

本教學課程系列會引導您使用 Visual Studio 2017 和 ASP.NET 4.5 來建立 ASP.NET Web Forms 應用程式。 您將建立一個名為**Wingtip 玩具**的應用程式，這是一個簡化的店面網站，可在線上銷售專案。 在此系列期間，會反白顯示新的 ASP.NET 4.5 功能。

### <a name="target-audience"></a>目標物件

ASP.NET Web form 的新開發人員是本教學課程系列的目標物件。

在下列領域中，您應該有一些知識：

- 物件導向程式設計（OOP）和語言
- Web 開發（HTML、CSS、JavaScript）
- 關係資料庫
- 多層式架構

若要查看這些區域，請考慮研究下列內容：

- [使用視覺效果消費者入門C#](https://msdn.microsoft.com/library/a72418yk.aspx)
- [Web 開發](https://msdn.microsoft.com/beginner/bb308760.aspx)、 [HTML、CSS、JavaScript、SQL、PHP、JQuery](http://w3schools.com/)
- [關係資料庫](http://en.wikipedia.org/wiki/Relational_database)
- [多層式架構](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a>應用程式功能

本系列提供的 ASP.NET Web Form 功能包括：

- Web 應用程式專案（而非網站專案）
- Web Form
- 主版頁面，設定
- 從中
- Entity Framework Code First、LocalDB
- 要求驗證
- 強型別資料控制
- 模型繫結
- 資料註釋
- 值提供者
- SSL 和 OAuth
- ASP.NET Identity、設定和授權
- 不顯眼的驗證
- 路由
- ASP.NET 錯誤處理

### <a name="application-scenarios-and-tasks"></a>應用程式案例和工作

教學課程系列工作包括：

- 建立、查看和執行新專案
- 建立資料庫結構
- 初始化和植入資料庫
- 使用樣式、圖形和主版頁面自訂 UI
- 加入頁面和導覽
- 顯示功能表細節和產品資料
- 建立購物車
- 新增 SSL 和 OAuth 支援
- 新增付款條件
- 包含系統管理員角色和使用者至應用程式
- 限制對特定頁面和資料夾的存取
- 將檔案上傳至 web 應用程式
- 執行輸入驗證
- 註冊 web 應用程式的路由
- 執行錯誤處理和錯誤記錄

## <a name="overview"></a>概觀

本教學課程系列適用于熟悉程式設計概念的人，但 ASP.NET Web form 的新手。 如果您已經熟悉 ASP.NET Web form，此系列仍然可以協助您瞭解新的 ASP.NET 4.5 功能。 對於不熟悉程式設計概念和 ASP.NET Web form 的讀者，請參閱 ASP.NET 網站上[消費者入門](../../../index.md)一節中提供的其他 Web form 教學課程。

本教學課程系列中提供的 ASP.NET 4.5 包含下列功能：

- 用於建立專案的簡單 UI，可提供[許多 ASP.NET](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add)架構（web FORM、MVC 和 web API）的支援。
- [啟動](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap)程式、版面配置、主題和回應式設計架構。
- [ASP.NET Identity](../../../../identity/index.md)，這是一個新的 ASP.NET 成員資格系統，在所有 ASP.NET 架構中的運作方式都相同，並可與 IIS 以外的 web 主控軟體搭配運作。
- [Entity Framework 6](https://msdn.microsoft.com/data/ef.aspx)

  Entity Framework 的更新可讓您：
  - 以強型別物件的形式抓取和運算元據
  - 以非同步方式存取資料
  - 處理暫時性連接錯誤
  - 記錄 SQL 語句

如需完整的 ASP.NET 4.5 功能清單，請參閱[Visual Studio 2013 版本資訊的 ASP.NET 和 Web 工具](../../../../visual-studio/overview/2013/release-notes.md)。

### <a name="the-wingtip-toys-sample-application"></a>Wingtip 玩具範例應用程式

下列螢幕擷取畫面是來自您在本教學課程系列中建立的 ASP.NET Web Forms 應用程式。 當您在 Visual Studio 中執行應用程式時，會出現下列 web 首頁。

![Wingtip 玩具-預設頁面](introduction-and-overview/_static/image1.png)

您可以註冊為新的使用者，或以現有的使用者身分登入。 頂端導覽具有從資料庫到產品類別目錄及其產品的連結。

如果您選取 [**產品**]，則會顯示所有可用的產品。 

![Wingtip 玩具-產品](introduction-and-overview/_static/image2.png)

如果您選取特定產品，則會顯示產品詳細資料。

![Wingtip 玩具-產品詳細資料](introduction-and-overview/_static/image3.png)

身為使用者，您可以使用 Web Forms 範本預設功能進行註冊和登入。 本教學課程也會說明如何使用現有的 Gmail 帳戶進行登入。 此外，您可以用系統管理員身分登入，以便在資料庫中新增和移除產品。

![Wingtip 玩具-登入](introduction-and-overview/_static/image4.png)

以使用者身分登入之後，您可以將產品新增至購物車，並簽出 PayPal。 範例應用程式是設計來在 PayPal 的開發人員沙箱中工作。 不會發生實際的 money 交易。

![Wingtip 玩具-購物車](introduction-and-overview/_static/image5.png)

PayPal 會確認您的帳戶、訂購和付款資訊。

![Wingtip 玩具-PayPal](introduction-and-overview/_static/image6.png)

從 PayPal 傳回之後，您可以檢查並完成您的訂單。

![Wingtip 玩具-訂購評論](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a>必要條件：

開始之前，請確定您的電腦上已安裝下列軟體：

- [Microsoft Visual Studio 2017 或 Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/)。

.NET Framework 會自動安裝。

本教學課程系列使用 Microsoft Visual Studio Community 2017。 您可以使用該方法或 Microsoft Visual Studio 2017 來完成此教學課程系列。

請注意下列關於 Visual Studio 的事項：

* Microsoft Visual Studio 2017 和 Microsoft Visual Studio Community 2017 在本教學課程系列中稱為*Visual Studio* 。

* Visual Studio 2017 會安裝在已安裝的任何舊版本旁邊。 在舊版中建立的網站可以在 Visual Studio 2017 中開啟，並繼續在舊版中開啟。

* 第一次開始 Visual Studio 時，會假設您已選取 [ *Web 開發*] 設定。 如需詳細資訊，請參閱[如何：選取 Web 開發環境設定](https://msdn.microsoft.com/library/ff521558.aspx)。

安裝必要條件之後，您就可以開始建立本教學課程系列中所提供的 Web 專案。

## <a name="download-the-sample-application"></a>下載範例應用程式

 您可以隨時從 MSDN 範例網站下載完整的範例應用程式：

[使用 ASP.NET 4.5 Web Forms 和 Visual Studio 2013 Wingtip 玩具](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)（C#）的消費者入門 

 此下載包含下列專案：

- *WingtipToys*資料夾中的範例應用程式。
- 用來在 [ *WingtipToys* ] 資料夾的 [ *WingtipToys-資產*] 資料夾中建立範例應用程式的資源。

下載為 *.zip*檔案。 若要查看此教學課程系列所建立的已完成專案，請*C#* 尋找並選取 .zip 檔案中的資料夾。 將C#資料夾儲存至您用來處理 Visual Studio 專案的資料夾。 根據預設，Visual Studio 2017 projects 資料夾為：

<strong>C:\Users&#92;</strong>  <strong><em>&lt;username&gt;</em></strong> <strong>\source\repos</strong>

將***C#*** 資料夾重新命名為***WingtipToys***。

> [!NOTE]
> 如果您的 [專案] 資料夾中已經有名為*WingtipToys*的資料夾，請在將*C#* 資料夾重新命名為*WingtipToys*之前，暫時將該現有資料夾重新命名。

若要執行已完成的專案，請開啟 [ *WingtipToys* ] 資料夾，然後按兩下 [ *WingtipToys* ] 檔案。 Visual Studio 2017 會開啟專案。 接下來，在**方案總管**中的*default.aspx*檔案上按一下滑鼠右鍵，然後**在瀏覽器中**選取 [View]。

## <a name="take-a-aspnet-web-forms-quiz-to-review-content"></a>參加 ASP.NET Web Forms 測驗以審查內容

完成本教學課程系列之後，請進行測驗來測試您的知識並強化重要概念。 每個問題都提供其他指引的說明和連結。

* [ASP.NET Web Forms 測驗](https://blogs.msdn.microsoft.com/erikreitan/2016/01/08/asp-net-web-forms-quiz/) 

## <a name="tutorial-support-and-comments"></a>教學課程支援和批註

如有問題和意見，請使用[ASP.NET 4.5 Web Forms 和 Visual Studio 2013 Wingtip 玩具](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)（C#）範例頁面上包含的消費者入門的 Q 和 A 區段。

歡迎使用此教學課程系列的批註。 當此教學課程系列更新時，每次致力於考慮改善的更正或建議。

如果發生錯誤，對應的錯誤訊息可能會造成混淆，而不會有如何修正此問題的絕佳說明。 如需協助，您可以查看[ASP.NET 論壇](https://forums.asp.net/)。 另一個不錯的來源是消費者入門中的 Q 和一節[與 ASP.NET 4.5 Web Forms 和 Visual Studio 2013 Wingtip 玩具](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)（C#）範例頁面。 

> [!div class="step-by-step"]
> [下一步](create-the-project.md)
