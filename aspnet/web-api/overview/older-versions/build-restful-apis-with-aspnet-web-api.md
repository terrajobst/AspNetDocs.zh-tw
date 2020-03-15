---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: 使用 ASP.NET Web API ASP.NET 4.x 建立 RESTful Api
author: rick-anderson
description: 實習實驗室：使用 ASP.NET 4.x 中的 Web API，為連絡人管理員應用程式建立簡單的 REST API。
ms.author: riande
ms.date: 02/18/2013
ms.custom: seoapril2019
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 35b115d6b4f84084e78e429bbb4842670e57bba4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78621811"
---
# <a name="build-restful-apis-with-aspnet-web-api"></a>使用 ASP.NET Web API 建立 RESTful Api

依[Web Camp 團隊](https://twitter.com/webcamps)

> 實習實驗室：使用 ASP.NET 4.x 中的 Web API，為連絡人管理員應用程式建立簡單的 REST API。 您也會建立取用 API 的用戶端。

最近幾年來，它已經很清楚，HTTP 不只是用來提供 HTML 網頁。 它也是一個強大的平臺，可用於建立 Web Api、使用幾個動詞（GET、POST 等等），再加上一些簡單的概念，例如*uri*和*標頭*。 ASP.NET Web API 是一組可簡化 HTTP 程式設計的元件。 因為它是以 ASP.NET MVC 執行時間為基礎，所以 Web API 會自動處理 HTTP 的低層級傳輸詳細資料。 同時，Web API 會自然地公開 HTTP 程式設計模型。 事實上，Web API 的其中一個目標就是*不要*抽象掉 HTTP 的現實。 因此，Web API 既彈性又容易擴充。  REST 架構樣式已證明是利用 HTTP 的有效方法，雖然它肯定不是 HTTP 的唯一有效方法。 連絡人管理員將會公開用來列出、新增和移除連絡人的 RESTful，以及其他人。 

此實驗室需要對 HTTP、REST 的基本瞭解，並假設您具備 HTML、JavaScript 和 jQuery 的基本知識。
> 
> > [!NOTE]
> > ASP.NET 網站有一個專門用於 ASP.NET Web API 架構[https://asp.net/web-api](https://asp.net/web-api)的區域。 此網站將繼續提供與 Web API 相關的最新資訊、範例和新聞，因此如果您想要深入瞭解建立可用於幾乎任何裝置或開發架構的自訂 Web Api，請經常檢查。
> > 
> > ASP.NET Web API （類似于 ASP.NET MVC 4）在分隔服務層與控制器之間有很大的彈性，可讓您輕鬆地使用數個可用的相依性插入架構。 MSDN 中有一個很好的範例，示範如何在 ASP.NET Web API 專案中使用相依性插入的 Ninject，您可以從[這裡](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)下載。
> 
> 
> 所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)取得。

<a id="Objectives"></a>
### <a name="objectives"></a>目標

在此實際操作實驗室中，您將瞭解如何：

- 執行 RESTful Web API
- 從 HTML 用戶端呼叫 API

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Prerequisites

若要完成此實際操作實驗室，需要下列各項：

- 適用于 Web 或上層的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （如需如何安裝的指示，請參閱[附錄 B](#AppendixB) ）。

<a id="Setup"></a>
### <a name="setup"></a>安裝程式

**安裝程式碼片段**

為了方便起見，您將在此實驗室中管理的大部分程式碼都是以 Visual Studio 程式碼片段的形式提供。 若要安裝程式碼片段，請執行 **.\Source\Setup\CodeSnippets.vsi**檔案。

如果您不熟悉 Visual Studio Code 程式碼片段，而且想要瞭解如何使用，您可以參閱本檔中的附錄 &quot;[附錄 A：使用程式碼片段](#AppendixA)&quot;。

<a id="Exercises"></a>
## <a name="exercises"></a>練習

這個實際操作實驗室包含下列練習：

1. [練習1：建立唯讀的 Web API](#Exercise1)
2. [練習2：建立讀取/寫入 Web API](#Exercise2)
3. [練習3：使用 HTML 用戶端的 Web API](#Exercise3)

> [!NOTE]
> 每個練習都會伴隨一個**結束**資料夾，其中包含您在完成練習之後應該取得的結果解決方案。 如果您需要額外的協助來進行練習，您可以使用此解決方案做為指南。

完成此實驗室的預估時間： **60 分鐘**。

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a>練習1：建立唯讀的 Web API

在此練習中，您將為 contact manager 執行唯讀的 GET 方法。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a>工作 1-建立 API 專案

在這項工作中，您將使用新的 ASP.NET Web 專案範本來建立 Web API web 應用程式。

1. 執行**Visual Studio 2012 Express For Web**，若要執行此動作，請移至 [**開始**] 並輸入**VS Express for Web**然後按**enter**。
2. 從 [**檔案**] 功能表中，選取 [**新增專案**]。 選取**視覺效果C# |Web**專案類型從 [專案類型] 樹狀檢視中選取 [ **ASP.NET MVC 4 Web 應用程式**] 專案類型。 將專案的**名稱**設為*ContactManager* ，並將**方案名稱**設定為 [*開始*]，然後按一下 **[確定]** 。

    ![建立新的 ASP.NET MVC 4.0 Web 應用程式專案](build-restful-apis-with-aspnet-web-api/_static/image1.png "建立新的 ASP.NET MVC 4.0 Web 應用程式專案")

    *建立新的 ASP.NET MVC 4.0 Web 應用程式專案*
3. 在 [ASP.NET MVC 4 專案類型] 對話方塊中，選取 [ **WEB API** ] 專案類型。 按一下 [確定]。

    ![指定 Web API 專案類型](build-restful-apis-with-aspnet-web-api/_static/image2.png "指定 Web API 專案類型")

    *指定 Web API 專案類型*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a>工作 2-建立連絡人管理員 API 控制器

在這項工作中，您將會建立 API 方法所在的控制器類別。

1. 從專案刪除 [**控制器**] 資料夾中名為**ValuesController.cs**的檔案。
2. 以滑鼠右鍵按一下專案中的 [**控制器**] 資料夾，然後選取 [**新增] |** 內容功能表中的 [控制器]。

    ![將新的控制器新增至專案](build-restful-apis-with-aspnet-web-api/_static/image3.png "將新的控制器新增至專案")

    *將新的控制器新增至專案*
3. 在出現的 [**新增控制器**] 對話方塊中，從 [範本] 功能表選取 [**空的 API 控制器**]。 將控制器類別命名為**ContactController**。 然後，按一下 [**新增]。**

    ![使用 [新增控制器] 對話方塊來建立新的 Web API 控制器](build-restful-apis-with-aspnet-web-api/_static/image4.png "使用 [新增控制器] 對話方塊來建立新的 Web API 控制器")

    *使用 [新增控制器] 對話方塊來建立新的 Web API 控制器*
4. 將下列程式碼加入至**ContactController**。

    （程式碼片段- *WEB API 實驗室-Ex01-取得 API 方法*）

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. 按 **F5** 鍵來進行應用程式偵錯。 應會出現 Web API 專案的預設首頁。

    ![ASP.NET Web API 應用程式的預設首頁](build-restful-apis-with-aspnet-web-api/_static/image5.png "ASP.NET Web API 應用程式的預設首頁")

    *ASP.NET Web API 應用程式的預設首頁*
6. 在 Internet Explorer 視窗中，按**F12**鍵以開啟 [**開發人員工具**] 視窗。 按一下 [**網路**] 索引標籤，然後按一下 [**開始捕捉**] 按鈕，開始將網路流量捕獲到視窗中。

    ![開啟 [網路] 索引標籤並起始網路捕獲](build-restful-apis-with-aspnet-web-api/_static/image6.png "開啟 [網路] 索引標籤並起始網路捕獲")

    *開啟 [網路] 索引標籤並起始網路捕獲*
7. 使用 **/api/contact**在瀏覽器的網址列中附加 URL，然後按 enter 鍵。 傳輸詳細資料會出現在 [網路捕捉] 視窗中。 請注意，回應的 MIME 類型為**application/json**。 這會示範預設輸出格式為 JSON 的方式。

    ![在網路視圖中查看 Web API 要求的輸出](build-restful-apis-with-aspnet-web-api/_static/image7.png "在網路視圖中查看 Web API 要求的輸出")

    *在網路視圖中查看 Web API 要求的輸出*

    > [!NOTE]
    > 此時，Internet Explorer 10 的預設行為會詢問使用者是否想要儲存或開啟 Web API 呼叫所產生的資料流程。 輸出將會是一個文字檔，其中包含 Web API URL 呼叫的 JSON 結果。 請勿取消對話方塊，以便透過 [開發人員] 工具視窗觀看回應的內容。
8. 按一下 [**移至詳細的視圖**] 按鈕，以查看更多關於此 API 呼叫回應的詳細資料。

    ![切換至詳細的視圖](build-restful-apis-with-aspnet-web-api/_static/image8.png "切換至詳細資料檢視")

    *切換至詳細的視圖*
9. 按一下 [**回應主體**] 索引標籤，以查看實際的 JSON 回應文字。

    ![在網路監視器中查看 JSON 輸出文字](build-restful-apis-with-aspnet-web-api/_static/image9.png "在網路監視器中查看 JSON 輸出文字")

    *在網路監視器中查看 JSON 輸出文字*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a>工作 3-建立連絡人模型並擴大連絡人控制器

在這項工作中，您將會建立 API 方法所在的控制器類別。

1. 以滑鼠右鍵按一下 [**模型**] 資料夾，然後選取 [**新增] |類別 ...** 從內容功能表。

    ![將新模型加入至 web 應用程式](build-restful-apis-with-aspnet-web-api/_static/image10.png "將新模型加入至 web 應用程式")

    *將新模型加入至 web 應用程式*
2. 在 [**加入新專案**] 對話方塊中，將新的檔案命名為**Contact.cs** ，然後按一下 [新增] **。**

    ![建立新的 Contact 類別檔案](build-restful-apis-with-aspnet-web-api/_static/image11.png "建立新的 Contact 類別檔案")

    *建立新的 Contact 類別檔案*
3. 將下列反白顯示的程式碼新增至**Contact**類別。

    （程式碼片段- *WEB API 實驗室-Ex01-Contact 類別*）

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. 在**ContactController**類別中，于**Get**方法的 [方法定義] 中選取 [**字串**]，然後輸入 [ *Contact*] 這個字。 一旦輸入單字，指標就會出現在「**連絡人**」一字的開頭。 按住**Ctrl**鍵，然後按下句點（.）鍵，或按一下圖示來開啟 [程式碼編輯器] 中的 [協助] 對話方塊，以自動填入模型命名空間的**using**指示詞。

    ![針對命名空間宣告使用 Intellisense 協助](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    *針對命名空間宣告使用 Intellisense 協助*
5. 修改**Get**方法的程式碼，使其傳回連絡人模型實例的陣列。

    （程式碼片段- *WEB API 實驗室-Ex01-傳回連絡人清單*）

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. 按**F5** ，在瀏覽器中進行 web 應用程式的偵錯工具。 若要查看對 API 回應輸出所做的變更，請執行下列步驟。

   1. 當瀏覽器開啟時，如果開發人員工具尚未開啟，請按**F12** 。
   2. 按一下 [**網路**] 索引標籤。
   3. 按 [**開始捕捉**] 按鈕。
   4. 將 URL 尾碼 **/api/contact**新增至網址列中的 url，然後按**enter**鍵。
   5. 按 [**移至詳細的視圖**] 按鈕。
   6. 選取 [**回應主體**] 索引標籤。您應該會看到 JSON 字串，代表連絡人實例陣列的序列化形式。

      ![複雜 Web API 方法呼叫的 JSON 序列化輸出](build-restful-apis-with-aspnet-web-api/_static/image13.png "複雜 Web API 方法呼叫的 JSON 序列化輸出")

      *複雜 Web API 方法呼叫的 JSON 序列化輸出*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a>工作 4-將功能解壓縮至服務層

這項工作將示範如何將功能解壓縮至服務層，讓開發人員可以輕鬆地將其服務功能與控制器層隔開，藉此讓實際執行工作的服務得以重複使用。

1. 在方案根目錄中建立新的資料夾，並將其命名為 [it**服務**]。 若要這樣做，請以滑鼠右鍵按一下 [ **ContactManager**專案]，然後選取 [新增] | **新資料夾**，**將**其命名為*服務*

    ![正在建立服務資料夾](build-restful-apis-with-aspnet-web-api/_static/image14.png "正在建立服務資料夾")

    *正在建立服務資料夾*
2. 以滑鼠右鍵按一下 [**服務**] 資料夾，然後選取 [**新增] |類別 ...** 從內容功能表。

    ![將新類別新增至 [服務] 資料夾](build-restful-apis-with-aspnet-web-api/_static/image15.png "將新類別新增至 [服務] 資料夾")

    *將新類別新增至 [服務] 資料夾*
3. 當 [新增**專案**] 對話方塊出現時，將新的類別命名為**contacts.json** ，**然後按一下 [新增]** 。

    ![建立類別檔案以包含 Contact Repository 服務層的程式碼](build-restful-apis-with-aspnet-web-api/_static/image16.png "建立類別檔案以包含 Contact Repository 服務層的程式碼")

    *建立類別檔案以包含 Contact Repository 服務層的程式碼*
4. 將 using 指示詞新增至**ContactRepository.cs**檔案，以包含模型命名空間。

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. 將下列反白顯示的程式碼新增至**ContactRepository.cs**檔案，以執行 GetAllContacts 方法。

    （程式碼片段- *WEB API 實驗室-Ex01-連絡人存放庫*）

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. 如果**ContactController.cs**檔案尚未開啟，請開啟該檔案。
7. 將下列 using 語句新增至檔案的命名空間宣告區段。

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. 將下列反白顯示的程式碼新增至**ContactController.cs**類別，以加入私用欄位來代表存放庫的實例，讓其他類別成員可以利用服務執行。

    （程式碼片段- *WEB API 實驗室-Ex01-連絡人控制器*）

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. 變更**Get**方法，使其使用 contact repository 服務。

    （程式碼片段- *WEB API 實驗室-Ex01-透過存放庫傳回連絡人清單*）

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. 將中斷點放在**ContactController**的**Get**方法定義上。

   ![將中斷點新增至連絡人控制器](build-restful-apis-with-aspnet-web-api/_static/image17.png "將中斷點新增至連絡人控制器")

   *將中斷點新增至連絡人控制器*
11. 按 **F5** 執行應用程式。
12. 當瀏覽器開啟時，請按**F12**開啟開發人員工具。
13. 按一下 [**網路**] 索引標籤。
14. 按一下 [**開始捕捉**] 按鈕。
15. 在網址列中使用尾碼 **/api/contact**附加 URL，然後按**enter**載入 api 控制器。
16. Visual Studio 2012 應該會在**Get**方法開始執行時中斷。

   ![在 Get 方法內中斷](build-restful-apis-with-aspnet-web-api/_static/image18.png "在 Get 方法內中斷")

   *在 Get 方法內中斷*
17. 按 **F5** 繼續。
18. 回到 Internet Explorer （如果尚未處於焦點）。 記下 [網路捕捉] 視窗。

    ![Internet Explorer 中顯示 Web API 呼叫結果的網路視圖](build-restful-apis-with-aspnet-web-api/_static/image19.png "Internet Explorer 中顯示 Web API 呼叫結果的網路視圖")

    *Internet Explorer 中顯示 Web API 呼叫結果的網路視圖*
19. 按一下 [**移至詳細的視圖**] 按鈕。
20. 按一下 [**回應主體**] 索引標籤。請記下 API 呼叫的 JSON 輸出，以及它如何代表服務層所抓取的兩個連絡人。

    ![在 [開發人員工具] 視窗中，從 Web API 查看 JSON 輸出](build-restful-apis-with-aspnet-web-api/_static/image20.png "在 [開發人員工具] 視窗中，從 Web API 查看 JSON 輸出")

    *在 [開發人員工具] 視窗中，從 Web API 查看 JSON 輸出*

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a>練習2：建立讀取/寫入 Web API

在此練習中，您將會針對連絡人管理員實行 POST 和 PUT 方法，以使用資料編輯功能來加以啟用。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a>工作 1-開啟 Web API 專案

在這項工作中，您將準備增強在練習1中建立的 Web API 專案，使其可以接受使用者輸入。

1. 執行**Visual Studio 2012 Express For Web**，若要執行此動作，請移至 [**開始**] 並輸入**VS Express for Web**然後按**enter**。
2. 開啟位於**來源/Ex02-ReadWriteWebAPI/開始/** 資料夾的 [**開始**] 解決方案。 否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
3. 開啟**Services/contacts.json .cs**檔案。

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a>工作 2-將資料持續性功能新增至連絡人存放庫的執行

在這項工作中，您將擴充在練習1中建立之 Web API 專案的 Contacts.json 類別，讓它可以保存並接受使用者輸入和新的連絡人實例。

1. 將下列常數新增至**contacts.json**類別，以代表本練習稍後的 web 伺服器快取專案索引鍵名稱的名稱。

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. 將包含下列程式碼的函式新增至**contacts.json** 。

    （程式碼片段- *WEB API 實驗室-Ex02-連絡人存放庫的構造*函式）

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. 修改**GetAllContacts**方法的程式碼，如下所示。

    （程式碼片段- *WEB API 實驗室-Ex02-取得所有連絡人*）

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > 這個範例是為了示範之用，而且會使用 web 伺服器的快取做為儲存媒體，讓多個用戶端都能使用這些值，而不是使用會話儲存機制或要求儲存體存留期。 您可以使用 Entity Framework、XML 儲存體或任何其他各種不同的 web 伺服器快取來取代它。
4. 將名為**SaveContact**的新方法實作為**contacts.json**類別，以執行儲存連絡人的工作。 **SaveContact**方法應該接受單一**連絡人**參數，並傳回表示成功或失敗的布林值。

    （程式碼片段- *WEB API 實驗室-Ex02-執行 SaveContact 方法*）

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a>練習3：使用 HTML 用戶端的 Web API

在此練習中，您將建立 HTML 用戶端來呼叫 Web API。 此用戶端會使用 JavaScript 來加速使用 Web API 交換資料，並使用 HTML 標籤在網頁瀏覽器中顯示結果。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a>工作 1-修改索引視圖以提供 GUI 來顯示連絡人

在這項工作中，您將修改 web 應用程式的預設 [索引] 視圖，以支援在 HTML 瀏覽器中顯示現有連絡人清單的需求。

1. 開啟 [ **Visual Studio 2012 Express For Web] （** 如果尚未開啟）。
2. 開啟位於**來源/Ex03-ConsumingWebAPI/開始/** 資料夾的 [**開始**] 解決方案。 否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
3. 開啟位於**Views/Home**資料夾的**Index. cshtml**檔案。
4. 將 div 元素內的 HTML 程式碼取代為識別碼**主體**，讓它看起來像下列程式碼。

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. 在檔案底部新增下列 JAVAscript 程式碼，以對 Web API 執行 HTTP 要求。

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. 如果**ContactController.cs**檔案尚未開啟，請開啟該檔案。
7. 將中斷點放在**ContactController**類別的**Get**方法上。

    ![將中斷點放在 API 控制器的 Get 方法上](build-restful-apis-with-aspnet-web-api/_static/image21.png "將中斷點放在 API 控制器的 Get 方法上")

    *將中斷點放在 API 控制器的 Get 方法上*
8. 按 **F5** 執行專案。 瀏覽器將會載入 HTML 檔案。

    > [!NOTE]
    > 請確定您流覽的是應用程式的根 URL。
9. 一旦頁面載入且 JavaScript 執行之後，就會叫用中斷點，而且程式碼執行會在控制器中暫停。

    ![使用 VS Express for Web 進行 Web API 呼叫的調試](build-restful-apis-with-aspnet-web-api/_static/image22.png "使用 VS Express for Web 進行 Web API 呼叫的調試")

    *使用 Visual Studio 2012 Express for Web 進行 Web API 呼叫的偵錯工具*
10. 請移除中斷點，然後按**F5**或偵錯工具工具列的 [**繼續**] 按鈕，繼續在瀏覽器中載入此視圖。 Web API 呼叫完成後，您應該會看到從 Web API 呼叫傳回的連絡人，在瀏覽器中顯示為清單專案。

    ![API 呼叫的結果會顯示在瀏覽器中做為清單專案](build-restful-apis-with-aspnet-web-api/_static/image23.png "API 呼叫的結果會顯示在瀏覽器中做為清單專案")

    *API 呼叫的結果會顯示在瀏覽器中做為清單專案*
11. 停止偵錯。

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a>工作 2-修改索引視圖以提供 GUI 來建立連絡人

在這項工作中，您將繼續修改 MVC 應用程式的索引視圖。 表單將會新增至 HTML 網頁，此頁面將會捕獲使用者輸入，並將其傳送至 Web API 以建立新的連絡人，並建立新的 Web API 控制器方法以從 GUI 收集日期。

1. 開啟**ContactController.cs**檔案。
2. 將新方法新增至名為**Post**的控制器類別，如下列程式碼所示。

    （程式碼片段- *WEB API 實驗室-Ex03-Post 方法*）

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. 如果尚未開啟，請在 Visual Studio 中開啟**Index. cshtml**檔案。
4. 在您于上一個工作中新增的未排序清單之後，將下面的 HTML 程式碼新增至檔案。

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. 在檔底部的腳本專案中，新增下列反白顯示的程式碼以處理按鈕點按事件，這會使用 HTTP POST 呼叫將資料張貼至 Web API。

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. 在**ContactController.cs**中，將中斷點放在**Post**方法上。
7. 按**F5**在瀏覽器中執行應用程式。
8. 在瀏覽器中載入頁面後，輸入新的連絡人名稱和識別碼，然後按一下 [**儲存**] 按鈕。

    ![在瀏覽器中載入的用戶端 HTML 檔案](build-restful-apis-with-aspnet-web-api/_static/image24.png "在瀏覽器中載入的用戶端 HTML 檔案")

    *在瀏覽器中載入的用戶端 HTML 檔案*
9. 當偵錯工具視窗在**Post**方法中中斷時，請查看**contact**參數的屬性。 這些值應符合您在表單中輸入的資料。

    ![要從用戶端傳送至 Web API 的 Contact 物件](build-restful-apis-with-aspnet-web-api/_static/image25.png "要從用戶端傳送至 Web API 的 Contact 物件")

    *要從用戶端傳送至 Web API 的 Contact 物件*
10. 在偵錯工具中逐步執行方法，直到已建立**回應**變數為止。 在偵錯工具的 [**區域變數**] 視窗中進行檢查時，您會看到所有屬性都已設定。

   ![在偵錯工具中建立後的回應](build-restful-apis-with-aspnet-web-api/_static/image26.png "在偵錯工具中建立後的回應")

   *在偵錯工具中建立後的回應*
11. 如果您按下**F5**鍵，或在偵錯工具中按一下 [**繼續**]，則要求會完成。 當您切換回瀏覽器之後，新的連絡人就會新增至**contacts.json**執行所儲存的連絡人清單中。

   ![瀏覽器反映成功建立新的連絡人實例](build-restful-apis-with-aspnet-web-api/_static/image27.png "瀏覽器反映成功建立新的連絡人實例")

   *瀏覽器反映成功建立新的連絡人實例*

> [!NOTE]
> 此外，您可以遵循[附錄 C：使用 Web Deploy 發佈 ASP.NET MVC 4 應用程式](#AppendixC)，將此應用程式部署至 Azure。

---

<a id="Summary"></a>
## <a name="summary"></a>總結

本實驗室為您介紹了新的 ASP.NET Web API 架構，以及如何使用架構來 RESTful Web Api。 從這裡開始，您可以建立新的存放庫，以使用任意數目的機制和連線來加速資料持續性，而不是在此實驗室中提供的範例。 Web API 支援多項額外功能，例如從非 HTML 用戶端，啟用以支援 HTTP 和 JSON 或 XML 的任何語言所撰寫的通訊。 也可以在一般 Web 應用程式之外裝載 Web API 的功能，也能夠建立您自己的序列化格式。

ASP.NET 網站有一個專門用於 ASP.NET Web API 架構[[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api)的區域。 此網站將繼續提供與 Web API 相關的最新資訊、範例和新聞，因此如果您想要深入瞭解建立可用於幾乎任何裝置或開發架構的自訂 Web Api，請經常檢查。

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a>附錄 A：使用程式碼片段

有了程式碼片段，您就可以輕鬆地擁有所需的所有程式碼。 實驗室檔會告訴您可以使用它們的確切時機，如下圖所示。

![使用 Visual Studio 程式碼片段將程式碼插入您的專案](build-restful-apis-with-aspnet-web-api/_static/image28.png "使用 Visual Studio 程式碼片段將程式碼插入您的專案")

*使用 Visual Studio 程式碼片段將程式碼插入您的專案*

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a>若要使用鍵盤新增程式碼片段（C#僅限）

1. 將游標放在您想要插入程式碼的位置。
2. 開始鍵入程式碼片段名稱（不含空格或連字號）。
3. 監看 IntelliSense 會顯示相符的程式碼片段名稱。
4. 選取正確的程式碼片段（或繼續輸入，直到選取整個程式碼片段的名稱為止）。
5. 按兩次 Tab 鍵，在游標位置插入程式碼片段。

    ![開始鍵入程式碼片段名稱](build-restful-apis-with-aspnet-web-api/_static/image29.png "開始鍵入程式碼片段名稱")

    *開始鍵入程式碼片段名稱*

    ![按 Tab 鍵以選取反白顯示的程式碼片段](build-restful-apis-with-aspnet-web-api/_static/image30.png "按 Tab 鍵以選取反白顯示的程式碼片段")

    *按 Tab 鍵以選取反白顯示的程式碼片段*

    ![再按一次 Tab 鍵，將會展開程式碼片段](build-restful-apis-with-aspnet-web-api/_static/image31.png "再按一次 Tab 鍵，將會展開程式碼片段")

    *再按一次 Tab 鍵，將會展開程式碼片段*

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a>若要使用滑鼠（C#、VISUAL BASIC 和 XML）加入程式碼片段

1. 以滑鼠右鍵按一下您要插入程式碼片段的位置。
2. 選取 [**插入程式碼片段**]，後面接著 [ **My Code 程式碼片段**]。
3. 按一下清單中的相關程式碼片段，即可加以選取。

    ![以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]](build-restful-apis-with-aspnet-web-api/_static/image32.png "以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]")

    *以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]*

    ![按一下清單中的相關程式碼片段，即可加以選取](build-restful-apis-with-aspnet-web-api/_static/image33.png "按一下清單中的相關程式碼片段，即可加以選取")

    *按一下清單中的相關程式碼片段，即可加以選取*

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a>附錄 B：安裝 Web 的 Visual Studio Express 2012

您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。 下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。

1. 移至[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。 或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Azure SDK&quot;搜尋產品 &quot;<em>Visual Studio Express 2012 For Web</em> 。
2. 按一下 [**立即安裝**]。 如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。
3. 開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。

    ![安裝 Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "安裝 Visual Studio Express")

    *安裝 Visual Studio Express*
4. 閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。

    ![接受授權條款](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    *接受授權條款*
5. 等到下載和安裝程式完成為止。

    ![安裝進度](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    *安裝進度*
6. 當安裝完成時，按一下 **[完成]** 。

    ![安裝已完成](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    *安裝已完成*
7. 按一下 **[** 結束] 以關閉 Web Platform Installer。
8. 若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。

    ![VS Express for Web 磚](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    *VS Express for Web 磚*

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>附錄 C：使用 Web Deploy 發行 ASP.NET MVC 4 應用程式

本附錄將說明如何從 Azure 入口網站建立新的網站，併發布您在實驗室之後取得的應用程式，利用 Azure 所提供的 Web Deploy 發佈功能。

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a>工作 1-從 Azure 入口網站建立新的網站

1. 移至[Azure 管理入口網站](https://manage.windowsazure.com/)並使用與您的訂用帳戶相關聯的 Microsoft 認證登入。

    > [!NOTE]
    > 有了 Azure，您可以免費裝載10個 ASP.NET 網站，然後隨著流量成長而調整。 您可以在[這裡](https://aka.ms/aspnet-hol-azure)註冊。

    ![登入 Windows Azure 入口網站](build-restful-apis-with-aspnet-web-api/_static/image39.png "登入 Windows Azure 入口網站")

    *登入入口網站*
2. 按一下命令列上的 [**新增**]。

    ![建立新網站](build-restful-apis-with-aspnet-web-api/_static/image40.png "建立新網站")

    *建立新網站*
3. 按一下 [**計算** | 的**網站**]。 然後選取 [**快速建立**] 選項。 提供新網站的可用 URL，然後按一下 [**建立網站**]。

    > [!NOTE]
    > Azure 是在雲端中執行之 web 應用程式的主機，您可以控制和管理。 [快速建立] 選項可讓您從入口網站外部，將已完成的 web 應用程式部署至 Azure。 它不包含設定資料庫的步驟。

    ![使用 [快速建立] 建立新的網站](build-restful-apis-with-aspnet-web-api/_static/image41.png "使用 [快速建立] 建立新的網站")

    *使用 [快速建立] 建立新的網站*
4. 等到新**網站**建立完畢。
5. 建立網站之後，請按一下 [ **URL** ] 資料行下方的連結。 檢查新網站是否正常運作。

    ![流覽至新網站](build-restful-apis-with-aspnet-web-api/_static/image42.png "流覽至新網站")

    *流覽至新網站*

    ![網站正在執行](build-restful-apis-with-aspnet-web-api/_static/image43.png "網站正在執行")

    *網站正在執行*
6. 返回入口網站，然後按一下 [**名稱**] 欄底下的網站名稱，以顯示管理頁面。

    ![開啟網站管理頁面](build-restful-apis-with-aspnet-web-api/_static/image44.png "開啟網站管理頁面")

    *開啟網站管理頁面*
7. 在 [**儀表板**] 頁面的 [**快速概覽**] 區段下，按一下 [**下載發行設定檔**] 連結。

    > [!NOTE]
    > *發行設定檔*包含針對每個啟用的發行方法，將 web 應用程式發佈到 Azure 所需的所有資訊。 發行設定檔包含 URL、使用者認證和資料庫字串，這些都是用來連接到已啟用發行方法的每個端點並進行驗證的必要資訊。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支援讀取發行設定檔，以將這些程式的設定自動化，以將 Web 應用程式發行至 Azure。

    ![正在下載網站發行設定檔](build-restful-apis-with-aspnet-web-api/_static/image45.png "正在下載網站發行設定檔")

    *正在下載網站發行設定檔*
8. 將發行設定檔下載到已知的位置。 在此練習中，您將瞭解如何使用此檔案，將 web 應用程式從 Visual Studio 發行至 Azure。

    ![儲存發行設定檔](build-restful-apis-with-aspnet-web-api/_static/image46.png "正在儲存發行設定檔")

    *儲存發行設定檔*

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>工作 2-設定資料庫伺服器

如果您的應用程式會使用 SQL Server 資料庫，您必須建立 SQL Database 伺服器。 如果您想要部署不使用 SQL Server 的簡單應用程式，您可能會略過這項工作。

1. 您將需要 SQL Database 伺服器來儲存應用程式資料庫。 您可以在 Azure 管理入口網站的  **SQL 資料庫** | **伺服器** | **伺服器的儀表板**上，從您的訂用帳戶中查看 SQL Database 伺服器。 如果您沒有建立伺服器，可以使用命令列上的 [**新增**] 按鈕建立一個。 記下 [**伺服器名稱] 和 [URL]、[系統管理員登入名稱] 和 [密碼**]，因為您將在後續工作中使用它們。 請不要建立資料庫，因為它會在稍後的階段中建立。

    ![SQL Database Server 儀表板](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database Server 儀表板")

    *SQL Database Server 儀表板*
2. 在下一項工作中，您將會從 Visual Studio 測試資料庫連線，因此您必須在伺服器的**允許 IP 位址**清單中包含本機 IP 位址。 若要這麼做，請按一下 **設定**，從**目前的用戶端 IP 位址**中選取 IP 位址，並將它貼入 [**起始 Ip 位址**] 和 [**結束 ip 位址**] 文字方塊，然後按一下 ![新增-用戶端-IP-位址-確定 按鈕](build-restful-apis-with-aspnet-web-api/_static/image48.png) 按鈕。

    ![正在新增用戶端 IP 位址](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    *正在新增用戶端 IP 位址*
3. 將**用戶端 Ip 位址**新增至 [允許的 ip 位址] 清單之後，按一下 [**儲存**] 以確認變更。

    ![確認變更](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    *確認變更*

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>工作 3-使用 Web Deploy 發行 ASP.NET MVC 4 應用程式

1. 返回 ASP.NET MVC 4 解決方案。 在 **方案總管**中，以滑鼠右鍵按一下 網站 專案，然後選取 **發佈**。

    ![發行應用程式](build-restful-apis-with-aspnet-web-api/_static/image51.png "發行應用程式")

    *發行網站*
2. 匯入您在第一個工作中儲存的發行設定檔。

    ![匯入發行設定檔](build-restful-apis-with-aspnet-web-api/_static/image52.png "匯入發行設定檔")

    *正在匯入發行設定檔*
3. 按一下 [**驗證連接**]。 驗證完成後，按 **[下一步]** 。

    > [!NOTE]
    > 當您看到 [驗證連線] 按鈕旁出現綠色核取記號時，驗證就會完成。

    ![正在驗證連接](build-restful-apis-with-aspnet-web-api/_static/image53.png "正在驗證連接")

    *正在驗證連接*
4. 在 [**設定**] 頁面的 [**資料庫**] 區段底下，按一下資料庫連接的文字方塊旁邊的按鈕（也就是**DefaultConnection**）。

    ![Web deploy 設定](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web deploy 設定")

    *Web deploy 設定*
5. 設定資料庫連接，如下所示：

   - 在 [**伺服器名稱**] 中，使用*tcp：* prefix 輸入您的 SQL Database 伺服器 URL。
   - 在 [**使用者名稱**] 中，輸入您的伺服器管理員登入名稱。
   - 在 [**密碼**] 中輸入您的伺服器管理員登入密碼。
   - 輸入新的資料庫名稱，例如： *MVC4SampleDB*。

     ![正在設定目的地連接字串](build-restful-apis-with-aspnet-web-api/_static/image55.png "正在設定目的地連接字串")

     *正在設定目的地連接字串*
6. 然後按一下 [確定]。 當系統提示您建立資料庫時，請按一下 **[是]** 。

    ![建立資料庫](build-restful-apis-with-aspnet-web-api/_static/image56.png "建立資料庫字串")

    *建立資料庫*
7. 您將用來連接到 Windows Azure 中 SQL Database 的連接字串會顯示在 [預設連接] 文字方塊中。 然後按一下 [下一步]。

    ![指向 SQL Database 的連接字串](build-restful-apis-with-aspnet-web-api/_static/image57.png "指向 SQL Database 的連接字串")

    *指向 SQL Database 的連接字串*
8. 在 [**預覽**] 頁面中，按一下 [**發佈**]。

    ![發行 web 應用程式](build-restful-apis-with-aspnet-web-api/_static/image58.png "發行 web 應用程式")

    *發行 web 應用程式*
9. 發佈程式完成後，您的預設瀏覽器會開啟已發行的網站。

    ![發行至 Windows Azure 的應用程式](build-restful-apis-with-aspnet-web-api/_static/image59.png "發行至 Windows Azure 的應用程式")

    *已發佈至 Azure 的應用程式*
