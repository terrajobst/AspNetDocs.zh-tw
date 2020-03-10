---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: 第7部分：成員資格和授權 |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第7部分涵蓋成員資格和授權。
ms.author: riande
ms.date: 10/13/2010
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: a6a1a936e0ea29ea36721ba78f35845401f74c01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539197"
---
# <a name="part-7-membership-and-authorization"></a>第7部分：成員資格和授權

依[Jon Galloway](https://github.com/jongalloway)

> MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 web 程式開發的逐步解說。  
>   
> MVC 音樂存放區是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。  
>   
> 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第7部分涵蓋成員資格和授權。

我們的商店經理控制器目前可供任何造訪我們網站的人存取。 讓我們將此變更為限制網站管理員的許可權。

## <a name="adding-the-accountcontroller-and-views"></a>新增 AccountController 和 Views

[完整 ASP.NET MVC 3 Web 應用程式] 範本和 [ASP.NET MVC 3 空白 Web 應用程式] 範本之間有一個差異，就是空白範本不包含帳戶控制器。 我們會透過從完整的 ASP.NET MVC 3 Web 應用程式範本建立的新 ASP.NET MVC 應用程式複製一些檔案，以新增帳戶控制器。

使用完整的 ASP.NET MVC 3 Web 應用程式範本建立新的 ASP.NET MVC 應用程式，並將下列檔案複製到專案中的相同目錄：

1. 複製控制器目錄中的 AccountController.cs
2. 複製模型目錄中的 AccountModels
3. 在 Views 目錄中建立帳戶目錄，並複製中的所有四個視圖

變更控制器和模型類別的命名空間，使其開頭為 MvcMusicStore。 AccountController 類別應該使用 MvcMusicStore 命名空間，而 AccountModels 類別應該使用 MvcMusicStore. 模型命名空間。

*注意：這些檔案也可從我們在本教學課程開頭複製網站設計檔案的 MvcMusicStore-Assets 下載中取得。成員資格檔案位於 Code 目錄中。*

更新後的解決方案看起來應該如下所示：

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a>使用 ASP.NET 設定網站新增系統管理使用者

在我們的網站要求授權之前，我們必須先建立具有存取權的使用者。 建立使用者最簡單的方式是使用內建的 ASP.NET 設定網站。

按一下方案總管中的圖示，啟動 ASP.NET 設定網站。

![](mvc-music-store-part-7/_static/image2.png)

這會啟動設定網站。 按一下 [首頁] 畫面上的 [安全性] 索引標籤，然後按一下畫面中央的 [啟用角色] 連結。

![](mvc-music-store-part-7/_static/image3.png)

按一下 [建立或管理角色] 連結。

![](mvc-music-store-part-7/_static/image4.png)

輸入 "Administrator" 作為角色名稱，然後按 [新增角色] 按鈕。

![](mvc-music-store-part-7/_static/image5.png)

按一下 [上一步] 按鈕，然後按一下左側的 [建立使用者] 連結。

![](mvc-music-store-part-7/_static/image6.png)

使用下列資訊填寫左側的 [使用者資訊] 欄位：

| **欄位** | **值** |
| --- | --- |
| **使用者名稱** | 系統管理員 |
| **密碼** | password123! |
| **確認密碼** | password123! |
| **電子郵件** | （任何電子郵件地址都可使用） |
| **安全性問題** | （任何您喜歡的） |
| **安全性解答** | （任何您喜歡的） |

*注意：當然，您可以使用任何您想要的密碼。預設的密碼安全性設定需要7個字元長的密碼，且包含一個非英數位元。*

選取此使用者的系統管理員角色，然後按一下 [建立使用者] 按鈕。

![](mvc-music-store-part-7/_static/image7.png)

此時，您應該會看到一則訊息，指出已成功建立使用者。

![](mvc-music-store-part-7/_static/image8.png)

您現在可以關閉瀏覽器視窗。

## <a name="role-based-authorization"></a>以角色為基礎的授權

現在我們可以使用 [授權] 屬性來限制對 StoreManagerController 的存取，指定使用者必須是系統管理員角色，才能存取類別中的任何控制器動作。

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

*注意： [授權] 屬性可以放在特定動作方法以及控制器類別層級上。*

現在流覽至/StoreManager 會顯示 [登入] 對話方塊：

![](mvc-music-store-part-7/_static/image9.png)

以新的系統管理員帳戶登入之後，我們就能夠如先前一樣前往專輯編輯畫面。

> [!div class="step-by-step"]
> [上一頁](mvc-music-store-part-6.md)
> [下一頁](mvc-music-store-part-8.md)
