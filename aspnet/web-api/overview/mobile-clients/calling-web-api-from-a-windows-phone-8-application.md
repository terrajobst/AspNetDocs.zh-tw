---
uid: web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
title: 從 Windows Phone 8 應用程式呼叫 Web API （C#）-ASP.NET 4。x
author: rmcmurray
description: 教學課程與程式碼：在 ASP.NET 4.x 中建立 ASP.NET Web API 應用程式，以提供 Windows Phone 8 應用程式的書籍目錄。
ms.author: riande
ms.date: 10/09/2013
ms.custom: seoapril2019
ms.assetid: b9775f41-352a-4f82-baa6-23e95b342e20
msc.legacyurl: /web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
msc.type: authoredcontent
ms.openlocfilehash: c5da14a6856f551343b6fb14f0aedc659e792f6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614734"
---
# <a name="calling-web-api-from-a-windows-phone-8-application-c"></a>從 Windows Phone 8 應用程式呼叫 Web API (C#)

依[Robert McMurray](https://github.com/rmcmurray)

在本教學課程中，您將瞭解如何建立完整的端對端案例，其中包含 ASP.NET Web API 應用程式，可提供 Windows Phone 8 應用程式的書籍目錄。

### <a name="overview"></a>概觀

RESTful 服務（例如 ASP.NET Web API）藉由抽象化伺服器端和用戶端應用程式的架構，簡化開發人員的 HTTP 型應用程式建立。 Web API 開發人員不會建立用於通訊的專屬通訊端型通訊協定，而是只需要針對其應用程式發佈必要的 HTTP 方法（例如： GET、POST、PUT、DELETE），而用戶端應用程式開發人員只需要使用其應用程式所需的 HTTP 方法。

在此端對端教學課程中，您將瞭解如何使用 Web API 來建立下列專案：

- 在[本教學課程的第一個部分](#STEP1)中，您將建立支援所有建立、讀取、更新和刪除（CRUD）作業的 ASP.NET Web API 應用程式，以管理書籍目錄。 此應用程式將使用 MSDN 的[範例 XML 檔（books.xml）](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) 。
- 在[本教學課程的第二個部分](#STEP2)中，您將建立互動式 Windows Phone 8 應用程式，以從您的 Web API 應用程式抓取資料。

#### <a name="prerequisites"></a>Prerequisites

- 已安裝 Windows Phone 8 SDK 的 Visual Studio 2013
- 安裝 Hyper-v 之64位系統上的 Windows 8 或更新版本
- 如需其他需求的清單，請參閱[WINDOWS PHONE SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471)下載頁面上的*系統需求*一節。

> [!NOTE]
> 如果您要在本機系統上測試 Web API 與 Windows Phone 8 專案之間的連線，您必須遵循將 *[Windows Phone 8 模擬器連線到本機電腦上的 WEB API 應用程式](https://go.microsoft.com/fwlink/?LinkId=324014)* 一文中的指示，以設定您的測試環境。

<a id="STEP1"></a>
### <a name="step-1-creating-the-web-api-bookstore-project"></a>步驟1：建立 Web API 書店專案

本端對端教學課程的第一個步驟，是建立支援所有 CRUD 作業的 Web API 專案;請注意，您會在本教學課程的[步驟 2](#STEP2)中，將 Windows Phone 應用程式專案新增至此方案。

1. 開啟**Visual Studio 2013**。
2. 依**序按一下 [** 檔案]、[**新增**] 和 [**專案**]。
3. 當 [**新增專案**] 對話方塊顯示時，依序展開 [**已安裝**]、[**範本**]、[**視覺C#效果**] 和 [ **Web**]。

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image2.png)](calling-web-api-from-a-windows-phone-8-application/_static/image1.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                按一下影像以展開                                                                |

4. 反白顯示**ASP.NET Web 應用程式**，輸入**書店**作為專案名稱，然後按一下 **[確定]** 。
5. 當 [**新增 ASP.NET 專案**] 對話方塊顯示時，請選取 [ **Web API** ] 範本，然後按一下 **[確定]** 。

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image4.png)](calling-web-api-from-a-windows-phone-8-application/_static/image3.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                按一下影像以展開                                                                |

6. 當 Web API 專案開啟時，從專案中移除範例控制器：

    1. 在 [方案瀏覽器] 中展開 [**控制器**] 資料夾。
    2. 以滑鼠右鍵按一下**ValuesController.cs**檔案，然後按一下 [**刪除**]。
    3. 當系統提示您確認刪除時，請按一下 **[確定]** 。
7. 將 XML 資料檔案新增至 Web API 專案;此檔案包含書店目錄的內容：

   1. 以滑鼠右鍵按一下 [solution explorer] 中的**應用程式\_[Data** ] 資料夾，然後按一下 [新增]，**再按一下 [** **新專案**]。
   2. 當 [**加入新專案**] 對話方塊顯示時，請反白顯示**XML**檔案範本。
   3. 將檔案名命名為**books.xml**，然後按一下 [**新增**]。
   4. 當開啟**books.xml**檔案時，請將檔案中的程式碼取代為 MSDN 上的範例**書籍 .xml**檔案中的 xml： 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample1.xml)]
   5. 儲存並關閉 XML 檔案。

8. 將書店模型新增至 Web API 專案;此模型包含適用于書店應用程式的建立、讀取、更新和刪除（CRUD）邏輯：

   1. 以滑鼠右鍵按一下 [方案瀏覽器] 中的 [**模型**] 資料夾，然後按一下 [**新增**]，再按一下 [**類別**]。
   2. 當 [新增**專案**] 對話方塊顯示時，將類別檔案命名為**BookDetails.cs**，然後按一下 [**新增**]。
   3. 開啟**BookDetails.cs**檔案時，請將檔案中的程式碼取代為下列內容： 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample2.cs)]
   4. 儲存並關閉**BookDetails.cs**檔案。

9. 將書店控制器新增至 Web API 專案：

   1. 以滑鼠右鍵按一下 [solution explorer] 中的 [**控制器**] 資料夾，然後按一下 [**新增**]，再按一下 [**控制器**]。
   2. 顯示 [**新增 Scaffold** ] 對話方塊時，反白顯示 [ **Web API 2 控制器-空白**]，然後按一下 [**新增**]。
   3. 顯示 [**新增控制器**] 對話方塊時，將控制器命名為**BooksController**，然後按一下 [**新增**]。
   4. 開啟**BooksController.cs**檔案時，請將檔案中的程式碼取代為下列內容： 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample3.cs)]
   5. 儲存並關閉**BooksController.cs**檔案。

10. 建立 Web API 應用程式來檢查是否有錯誤。

<a id="STEP2"></a>
### <a name="step-2-adding-the-windows-phone-8-bookstore-catalog-project"></a>步驟2：新增 Windows Phone 8 書店目錄專案

此端對端案例的下一個步驟是建立 Windows Phone 8 的目錄應用程式。 此應用程式會使用預設使用者介面的*Windows Phone 資料*系結應用程式範本，並使用您在本教學課程的[步驟 1](#STEP1)中建立的 Web API 應用程式做為資料來源。

1. 在 [方案瀏覽器] 中，以滑鼠右鍵按一下 [**書店**] 方案，然後依序按一下 [**加入**] 和 [**新增專案**]。
2. 當 **新增專案** 對話方塊顯示時，依序展開 **已安裝** 和 **視覺效果C#** ，然後**Windows Phone**。
3. 反白顯示 Windows Phone 的資料系結**應用程式**，輸入**BookCatalog**作為 [名稱]，然後按一下 **[確定]** 。
4. 將 Json.NET NuGet 套件新增至**BookCatalog**專案：

    1. 以滑鼠右鍵按一下 [方案瀏覽器] 中**BookCatalog**專案的 [**參考**]，然後按一下 [**管理 NuGet 套件**]。
    2. 顯示 [**管理 NuGet 封裝**] 對話方塊時，展開 [**線上**] 區段，並反白顯示 [ **nuget.org**]。
    3. 在搜尋欄位中輸入**Json.NET** ，然後按一下 [搜尋] 圖示。
    4. 反白顯示搜尋結果中的**Json.NET** ，然後按一下 [**安裝**]。
    5. 當安裝完成時，按一下 [**關閉**]。
5. 將**BookDetails**模型加入至**BookCatalog**專案;這包含書店類別的一般模型：

   1. 以滑鼠右鍵按一下 [方案瀏覽器] 中的**BookCatalog**專案，然後按一下 [**加入**]，再按一下 [**新增資料夾**]。
   2. 將新資料夾命名為**模型**。
   3. 以滑鼠右鍵按一下 [方案瀏覽器] 中的 [**模型**] 資料夾，然後按一下 [**新增**]，再按一下 [**類別**]。
   4. 當 [新增**專案**] 對話方塊顯示時，將類別檔案命名為**BookDetails.cs**，然後按一下 [**新增**]。
   5. 開啟**BookDetails.cs**檔案時，請將檔案中的程式碼取代為下列內容： 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample4.cs)]
   6. 儲存並關閉**BookDetails.cs**檔案。

6. 更新**MainViewModel.cs**類別，以包含與書店 Web API 應用程式通訊的功能：

   1. 展開 [方案瀏覽器] 中的 [ **viewmodel** ] 資料夾，然後按兩下 [ **MainViewModel.cs** ] 檔案。
   2. 開啟**MainViewModel.cs**檔案時，請將檔案中的程式碼取代為下列程式碼：請注意，您將需要使用 Web API 的實際 URL 來更新 `apiUrl` 常數的值： 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample5.cs)]
   3. 儲存並關閉**MainViewModel.cs**檔案。

7. 更新**MainPage** ，以自訂應用程式名稱：

   1. 按兩下 [方案 MainPage] 中的 [ **xaml** ] 檔案。
   2. 當**MainPage 開啟 xaml**檔案時，請找出下列幾行程式碼： 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample6.xml)]
   3. 以下列內容取代這幾行： 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample7.xml)]
   4. 儲存並關閉**MainPage. xaml**檔案。

8. 更新**DetailsPage**檔案，以自訂顯示的專案：

   1. 按兩下 [方案 DetailsPage] 中的 [ **xaml** ] 檔案。
   2. 當**DetailsPage 開啟 xaml**檔案時，請找出下列幾行程式碼： 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample8.xml)]
   3. 以下列內容取代這幾行： 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample9.xml)]
   4. 儲存並關閉**DetailsPage. xaml**檔案。

9. 建立 Windows Phone 應用程式，以檢查是否有錯誤。

### <a name="step-3-testing-the-end-to-end-solution"></a>步驟3：測試端對端解決方案

如本教學*課程的必要條件*一節中所述，當您在本機系統上測試 Web API 與 Windows Phone 8 專案之間的連線時，必須遵循將 *[Windows Phone 8 模擬器連線到本機電腦上的 Web API 應用程式](https://go.microsoft.com/fwlink/?LinkId=324014)* 一文中的指示，以設定您的測試環境。

設定測試環境之後，您必須將 Windows Phone 應用程式設為啟始專案。 若要這樣做，請在 [方案瀏覽器] 中反白顯示**BookCatalog**應用程式，然後按一下 [**設定為啟始專案**]：

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image6.png)](calling-web-api-from-a-windows-phone-8-application/_static/image5.png) |
| --- |
| 按一下影像以展開 |

當您按下 F5 時，Visual Studio 會同時啟動 Windows Phone 模擬器，這會在從您的 Web API 抓取應用程式資料時，顯示 &quot;請等候&quot; 訊息：

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image8.png)](calling-web-api-from-a-windows-phone-8-application/_static/image7.png) |
| --- |
| 按一下影像以展開 |

如果所有專案都成功，您應該會看到顯示的類別目錄：

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image10.png)](calling-web-api-from-a-windows-phone-8-application/_static/image9.png) |
| --- |
| 按一下影像以展開 |

如果您在任何書籍標題上按一下，應用程式將會顯示書籍描述：

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image12.png)](calling-web-api-from-a-windows-phone-8-application/_static/image11.png) |
| --- |
| 按一下影像以展開 |

如果應用程式無法與您的 Web API 通訊，將會顯示錯誤訊息：

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image14.png)](calling-web-api-from-a-windows-phone-8-application/_static/image13.png) |
| --- |
| 按一下影像以展開 |

如果您按一下錯誤訊息，將會顯示有關錯誤的任何其他詳細資料：

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image16.png)](calling-web-api-from-a-windows-phone-8-application/_static/image15.png) |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                 按一下影像以展開                                                                 |
