---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
title: 第1部分：總覽和檔案 > 新專案 |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第1部分涵蓋總覽和檔案 > 的新專案。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: bd356ca3-5bdb-4067-9dac-c9e9923a86e8
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
msc.type: authoredcontent
ms.openlocfilehash: 48428ff4ab5888253ed93ac41e79006eec823ad2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559980"
---
# <a name="part-1-overview-and-file-new-project"></a>第1部分：總覽和檔案 > 的新專案

依[Jon Galloway](https://github.com/jongalloway)

> MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 web 程式開發的逐步解說。  
>   
> MVC 音樂存放區是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。  
>   
> 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第1部分涵蓋總覽和檔案&gt;的新專案。

## <a name="overview"></a>概觀

MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Web Developer 進行網頁程式開發的逐步解說。 我們會開始變慢，因此新手層級的 網頁程式開發體驗也沒關係。

我們將建立的應用程式是簡單的音樂商店。 應用程式有三個主要部分： [購物]、[結帳] 和 [系統管理]。

![](mvc-music-store-part-1/_static/image1.jpg)

訪客可以依內容類型流覽專輯：

![](mvc-music-store-part-1/_static/image2.jpg)

他們可以查看單一專輯，並將其新增至購物車：

![](mvc-music-store-part-1/_static/image3.jpg)

他們可以審查其購物車，移除任何不再需要的專案：

![](mvc-music-store-part-1/_static/image4.jpg)

繼續簽出將會提示他們登入或註冊使用者帳戶。

![](mvc-music-store-part-1/_static/image1.png)

![](mvc-music-store-part-1/_static/image2.png)

建立帳戶之後，他們可以填寫出貨和付款資訊來完成訂單。 為了簡單起見，我們會執行一項絕佳的促銷活動：如果您輸入促銷代碼「免費」，一切都免費！

![](mvc-music-store-part-1/_static/image5.jpg)

排序之後，他們會看到簡單的確認畫面：

![](mvc-music-store-part-1/_static/image6.jpg)

除了客戶面向的頁面之外，我們也會建立 [系統管理員] 區段，其中會顯示系統管理員可以建立、編輯和刪除專輯的專輯清單：

![](mvc-music-store-part-1/_static/image7.jpg)

## <a name="1-file--gt-new-project"></a>1. 檔案&gt; 的新專案

### <a name="installing-the-software"></a>安裝軟體

本教學課程一開始會使用免費的 Visual Web Developer 2010 Express （這是免費的）來建立新的 ASP.NET MVC 3 專案，然後我們會以累加方式新增功能，以建立完整的運作中應用程式。 在此過程中，我們將討論資料庫存取、表單張貼案例、資料驗證、使用主版頁面進行一致的頁面配置、使用 AJAX 進行頁面更新和驗證、使用者登入等等。

您可以依照步驟進行，也可以從[MVC-音樂存放區](https://github.com/evilDave/MVC-Music-Store)下載已完成的應用程式。

您可以使用 Visual Studio 2010 SP1 或 Visual Web Developer 2010 Express SP1 （免費版的 Visual Studio 2010）來建立應用程式。 我們將使用 SQL Server Compact （也免費）來裝載資料庫。 開始之前，請先確定您已安裝下列必要條件。

- [Visual Studio Web Developer Express SP1 必要條件]
- [ASP.NET MVC 3 工具更新]
- [SQL Server Compact 4.0]-包含執行時間和工具支援

### <a name="creating-a-new-aspnet-mvc-3-project"></a>建立新的 ASP.NET MVC 3 專案

我們會先從 Visual Web Developer 的 [檔案] 功能表中選取 [新增專案]。 這會顯示 [新增專案] 對話方塊。

![](mvc-music-store-part-1/_static/image5.png)

我們將選取左側的C# [Visual&gt; Web Templates] 群組，然後選擇 [中間] 資料行中的 [ASP.NET MVC 3 Web 應用程式] 範本。 將專案命名為 MvcMusicStore，然後按下 [確定] 按鈕。

![](mvc-music-store-part-1/_static/image8.jpg)

這會顯示次要對話，讓我們為專案進行一些 MVC 特定設定。 選取下列各項：

專案範本-選取 [空白]

視圖引擎-選取 Razor

使用 HTML5 語義標記-已核取

確認您的設定如下所示，然後按下 [確定] 按鈕。

![](mvc-music-store-part-1/_static/image9.jpg)

這會建立我們的專案。 讓我們來看一下在右邊的方案總管中，已新增至應用程式的資料夾。

![](mvc-music-store-part-1/_static/image10.jpg)

空白 MVC 3 範本不是完全空白，它會新增基本資料夾結構：

![](mvc-music-store-part-1/_static/image6.png)

ASP.NET MVC 會針對資料夾名稱使用一些基本的命名慣例：

| [資料夾] | **目的** |
| --- | --- |
| **/Controllers** | 控制器會回應來自瀏覽器的輸入、決定該如何處理，以及將回應傳回給使用者。 |
| **/Views** | Views 包含 UI 範本 |
| **/Models** | 模型保存和運算元據 |
| **/Content** | 此資料夾包含我們的影像、CSS 和任何其他靜態內容 |
| **/Scripts** | 此資料夾包含我們的 JavaScript 檔案 |

這些資料夾甚至會包含在空白的 ASP.NET MVC 應用程式中，因為 ASP.NET MVC 架構預設會使用「慣例 over 設定」方法，並根據資料夾命名慣例做出一些預設假設。 例如，控制器預設會在 [Views] 資料夾中尋找 views，而您不需要在程式碼中明確指定。 堅持使用預設慣例可減少您需要撰寫的程式碼數量，也能讓其他開發人員更輕鬆地瞭解您的專案。 我們會在建立應用程式時，更清楚地說明這些慣例。

> [!div class="step-by-step"]
> [下一個](mvc-music-store-part-2.md)
