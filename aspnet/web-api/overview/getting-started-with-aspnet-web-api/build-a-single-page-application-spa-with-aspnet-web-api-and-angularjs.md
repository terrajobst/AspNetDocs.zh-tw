---
uid: web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
title: 實習實驗室：使用 ASP.NET Web API 和 .js 建立單一頁面應用程式（SPA） ASP.NET 4。x
author: rick-anderson
description: 逐步執行程式碼：使用適用于 ASP.NET 4.x 的 ASP.NET Web API 和 .js 建立單一頁面應用程式（SPA）。
ms.author: riande
ms.date: 09/30/2015
ms.custom: seoapril2019
ms.assetid: 719727b7-bef3-45ad-bfe9-ba5bcdb2305f
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
msc.type: authoredcontent
ms.openlocfilehash: 86833a890da759e489dd11dc9afb128a9b7a75e3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557040"
---
# <a name="hands-on-lab-build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs"></a>實習實驗室：使用 ASP.NET Web API 和角度 .js 建立單一頁面應用程式（SPA）

依[Web Camp 團隊](https://twitter.com/webcamps)

[下載 Web Camp 訓練套件](https://aka.ms/webcamps-training-kit)

這堂實習實驗室會示範如何使用 ASP.NET Web API 和 ASP.NET 4.x 的 .js 來建立單一頁面應用程式（SPA）。

在這個實際操作的實驗室中，您將利用這些技術來執行萬能技客測驗，這是以 SPA 概念為基礎的邏輯網站。 您會先使用 ASP.NET Web API 來執行服務層級，以公開所需的端點來取得測驗問題並儲存答案。 然後，您將使用 AngularJS 和 CSS3 轉換效果，建立豐富且回應迅速的 UI。

在傳統的 web 應用程式中，用戶端（瀏覽器）會藉由要求頁面來起始與伺服器的通訊。 接著，伺服器會處理要求，並將網頁的 HTML 傳送給用戶端。 在後續與頁面的互動中–例如，使用者導覽至連結或提交含有資料的表單–會將新的要求傳送至伺服器，然後流程會重新開機：伺服器會處理要求，並將新頁面傳送至瀏覽器以回應新的動作要求ed （由用戶端）。
> 
> 在單頁應用程式（Spa）中，在初始要求之後，會在瀏覽器中載入整個頁面，但後續的互動會透過 Ajax 要求進行。 這表示瀏覽器只需要更新已變更之頁面的部分;不需要重載整頁。 SPA 方法可減少應用程式回應使用者動作所花費的時間，進而產生更流暢的體驗。
> 
> SPA 的架構牽涉到在傳統 web 應用程式中不存在的特定挑戰。 不過，像是 ASP.NET Web API 之類的新興技術，像是 AngularJS 的 JavaScript 架構和 CSS3 提供的新樣式功能，讓設計和建立 Spa 變得非常容易。
> 
> 
> 所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)取得。

## <a name="overview"></a>概觀

<a id="Objectives"></a>
### <a name="objectives"></a>目標

在此實際操作實驗室中，您將瞭解如何：

- 建立用來傳送和接收 JSON 資料的 ASP.NET Web API 服務
- 使用 AngularJS 建立回應式 UI
- 使用 CSS3 轉換來增強 UI 體驗

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Prerequisites

若要完成此實際操作實驗室，需要下列各項：

- [適用于 Web 或更新版本的 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)

<a id="Setup"></a>
### <a name="setup"></a>安裝程式

為了在此實際操作實驗室中執行練習，您必須先設定您的環境。

1. 開啟 Windows Explorer 並流覽至實驗室的 [**源**] 資料夾。
2. 以滑鼠右鍵按一下**setup.exe** ，然後選取 [以**系統管理員身分執行**] 以啟動安裝程式，以設定您的環境並安裝此實驗室的 Visual Studio 程式碼片段。
3. 如果顯示 [使用者帳戶控制] 對話方塊，請確認動作以繼續。

> [!NOTE]
> 執行安裝程式之前，請確定您已檢查過此實驗室的所有相依性。

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>使用程式碼片段

在整個實驗室檔中，系統會指示您插入程式碼區塊。 為了方便起見，大部分的程式碼都是以 Visual Studio Code 程式碼片段的形式提供，您可以從 Visual Studio 2013 內進行存取，以避免必須以手動方式新增。

> [!NOTE]
> 每個練習都附有一個起始解決方案，此方案位於練習的 [**開始**] 資料夾中，可讓您獨立于其他練習之外進行追蹤。 請注意，在練習期間新增的程式碼片段缺少這些起始的解決方案，而且在您完成練習之前可能無法正常執行。 在練習的原始程式碼中，您也會找到一個包含 Visual Studio 解決方案的**結束**資料夾，其中含有完成對應練習中步驟所產生的程式碼。 如果您在進行此實際操作實驗室時需要其他協助，您可以使用這些解決方案做為指導方針。

---

<a id="Exercises"></a>
## <a name="exercises"></a>練習

這個實際操作實驗室包含下列練習：

1. [建立 Web API](#Exercise1)
2. [建立 SPA 介面](#Exercise2)

完成此實驗室的預估時間： **60 分鐘**

> [!NOTE]
> 當您第一次啟動 Visual Studio 時，您必須選取其中一個預先定義的設定集合。 每個預先定義的集合都是設計來符合特定的開發風格，並決定視窗配置、編輯器行為、IntelliSense 程式碼片段和對話方塊選項。 本實驗室中的程式說明在使用 [**一般開發設定**] 集合時，在 Visual Studio 中完成指定工作所需的動作。 如果您針對開發環境選擇不同的 [設定] 集合，您應該考慮的步驟可能會有所差異。

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-web-api"></a>練習1：建立 Web API

SPA 的其中一個重要部分就是服務層。 它負責處理 UI 所傳送的 Ajax 呼叫，並傳回資料以回應該呼叫。 抓取的資料應該以電腦可讀取的格式呈現，才能供用戶端剖析及取用。

Web API 架構是 ASP.NET 堆疊的一部分，其設計旨在讓您輕鬆地執行 HTTP 服務，通常會透過 RESTful API 來傳送和接收 JSON 或 XML 格式的資料。 在此練習中，您將建立網站來裝載萬能技客測驗應用程式，然後使用 ASP.NET Web API 來執行後端服務，以公開並保存測驗資料。

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-the-initial-project-for-geek-quiz"></a>工作1–建立萬能技客測驗的初始專案

在這項工作中，您將根據 Visual Studio 隨附的**一個 ASP.NET**專案類型，開始建立具有 ASP.NET Web API 支援的新 ASP.NET MVC 專案。 **其中一個 ASP.NET**會將所有 ASP.NET 技術合併，並提供您視需要混合使用和比對的選項。 接著，您將加入 Entity Framework 的模型類別和資料庫初始化運算式，以插入測驗問題。

1. 開啟**Web Visual Studio Express 2013** ，然後選取 [檔案] **|新增專案 ...** 以啟動新的解決方案。

    ![建立新專案](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "建立新專案")

    *建立新專案*
2. 在 [**新增專案**] 對話方塊中，選取視覺效果  **C#底下的 [ASP.NET Web 應用程式] |[Web** ] 索引標籤。請確認已選取 **.NET Framework 4.5** ，將其命名為*GeekQuiz*，選擇**位置**，然後按一下 **[確定]** 。

    ![建立新的 ASP.NET Web 應用程式專案](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "建立新的 ASP.NET Web 應用程式專案")

    *建立新的 ASP.NET Web 應用程式專案*
3. 在 [**新增 ASP.NET 專案**] 對話方塊中，選取 [ **MVC** ] 範本，然後選取 [ **Web API** ] 選項。 此外，請確定 [**驗證**] 選項已設為 [**個別使用者帳戶**]。 按一下 [確定] 繼續操作。

    ![使用 MVC 範本建立新的專案，包括 Web API 元件](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image3.png)

    *使用 MVC 範本建立新的專案，包括 Web API 元件*
4. 在**方案總管**中，以滑鼠右鍵按一下**GeekQuiz**專案的 [**模型**] 資料夾，然後選取 [**新增] |現有專案 ...** 。

    ![加入現有的專案](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "加入現有的專案")

    *加入現有的專案*
5. 在 [**加入現有專案**] 對話方塊中，流覽至 [**來源/資產/模型**] 資料夾，然後選取所有檔案。 按一下 [新增]。

    ![新增模型資產](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "新增模型資產")

    *新增模型資產*

    > [!NOTE]
    > 藉由新增這些檔案，您將會新增資料模型、Entity Framework 的資料庫內容，以及萬能技客測驗應用程式的資料庫初始化運算式。
    > 
    > **Entity Framework （EF）** 是物件關聯式對應程式（ORM），可讓您以概念應用程式模型進行程式設計來建立資料存取應用程式，而不需要直接使用關聯式儲存架構進行程式設計。 您可以在[這裡](../../../entity-framework.md)深入瞭解 Entity Framework。
    > 
    > 以下是您剛才新增之類別的描述：
    > 
    > - **TriviaOption：** 代表與測驗問題相關聯的單一選項
    > - **TriviaQuestion：** 代表測驗問題，並透過**options**屬性公開相關聯的選項
    > - **TriviaAnswer：** 代表使用者選取來回應測驗問題的選項
    > - **TriviaCoNtext：** 代表萬能技客測驗應用程式的 Entity Framework 資料庫內容。 這個類別衍生自**DCoNtext** ，並公開代表上述實體集合的**DbSet**屬性。
    > - **TriviaDatabaseInitializer：** 執行繼承自**CreateDatabaseIfNotExists**之**TriviaCoNtext**類別的 Entity Framework 初始化運算式。 這個類別的預設行為是只在不存在時建立資料庫，插入**Seed**方法中指定的實體。
6. 開啟**Global.asax.cs**檔案，並新增下列 using 語句。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample1.cs)]
7. 將下列程式碼新增至**應用程式開頭\_Start**方法，將**TriviaDatabaseInitializer**設定為資料庫初始化運算式。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample2.cs)]
8. 修改**Home**控制器來限制已驗證使用者的存取權。 若要這麼做，請開啟 [**控制器**] 資料夾內的**HomeController.cs**檔案，並將 [**授權**] 屬性新增至**HomeController**類別定義。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample3.cs)]

    > [!NOTE]
    > **授權**篩選準則會檢查使用者是否已通過驗證。 如果使用者未經過驗證，則會傳回 HTTP 狀態碼401（未經授權），而不會叫用動作。 您可以在控制器層級或個別動作層級，全域套用篩選準則。
9. 您現在將自訂網頁的版面配置和商標。 若要這麼做，請開啟 Views 內的 **\_Layout**檔案 **|共用**資料夾，並將*ASP.NET 應用程式*取代為*萬能技客測驗*，以更新 **&lt;標題&gt;** 元素的內容。

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample4.cshtml)]
10. 在相同的檔案中，移除 [*關於*] 和 [*連絡人*] 連結，並將 [*首頁*] 連結重新命名為 [*播放*]，以更新巡覽列。 此外，將*應用程式名稱*連結重新命名為*萬能技客測驗*。 導覽列的 HTML 看起來應該像下列程式碼。

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample5.cshtml)]
11. 將*我的 ASP.NET 應用程式*取代為*萬能技客測驗*，以更新版面配置頁的頁尾。 若要這麼做，請將&lt;頁尾 **&gt;** 元素的內容取代為下列反白顯示的程式碼。

    [!code-html[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample6.html)]

<a id="Ex1Task2"></a>
#### <a name="task-2--creating-the-triviacontroller-web-api"></a>工作 2-建立 TriviaController Web API

在上一個工作中，您已建立萬能技客測驗 web 應用程式的初始結構。 您現在將建立一個簡單的 Web API 服務，以與測驗資料模型互動並公開下列動作：

- **取得/api/trivia**：從測驗清單中抓取要由已驗證使用者回答的下一個問題。
- **POST/api/trivia**：儲存已驗證使用者所指定的測驗解答。

您將使用 Visual Studio 所提供的 ASP.NET 架構工具來建立 Web API 控制器類別的基準。

1. 開啟**應用程式\_[開始**] 資料夾內的**WebApiConfig.cs**檔案。 此檔案會定義 Web API 服務的設定，例如路由對應至 Web API 控制器動作的方式。
2. 在檔案開頭處新增下列 using 語句。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample7.cs)]
3. 將下列反白顯示的程式碼新增至**Register**方法，以全域設定 Web API 動作方法所抓取之 JSON 資料的格式器。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample8.cs)]

    > [!NOTE]
    > **CamelCasePropertyNamesContractResolver**會自動將屬性名稱轉換成*camel*大小寫，這是 JavaScript 中屬性名稱的一般慣例。
4. 在**方案總管**中，以滑鼠右鍵按一下**GeekQuiz**專案的 [**控制器**] 資料夾，然後選取 [**新增] |新增 Scaffold 專案 ...** 。

    ![建立新的 scaffold 專案](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "建立新的 scaffold 專案")

    *建立新的 scaffold 專案*
5. 在 [**新增 Scaffold** ] 對話方塊中，確定已在左窗格中選取 [**一般**] 節點。 然後，在中央窗格中選取 [ **WEB API 2 控制器-空白**] 範本，然後按一下 [**新增**]。

    ![選取 [Web API 2 控制器] 空白範本](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "選取 [Web API 2 控制器] 空白範本")

    *選取 [Web API 2 控制器] 空白範本*

    > [!NOTE]
    > **ASP.NET**樣板是用於 ASP.NET Web 應用程式的程式碼產生架構。 Visual Studio 2013 包括適用于 MVC 和 Web API 專案的預先安裝程式碼產生器。 當您想要快速加入與資料模型互動的程式碼，以減少開發標準資料作業所需的時間量時，您應該使用專案中的樣板。
    > 
    > 此樣板程式也可確保專案中已安裝所有必要的相依性。 例如，如果您從空的 ASP.NET 專案開始，然後使用樣板來新增 Web API 控制器，則會自動將必要的 Web API NuGet 套件和參考新增至您的專案。
6. 在 [**新增控制器**] 對話方塊中，于 [**控制器名稱**] 文字方塊中輸入*TriviaController* ，然後按一下 [**新增**]。

    ![新增邏輯控制器](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "新增邏輯控制器")

    *新增邏輯控制器*
7. **TriviaController.cs**檔案接著會新增至**GeekQuiz**專案的 [**控制器**] 資料夾，其中包含空的**TriviaController**類別。 在檔案開頭處新增下列 using 語句。

    （程式碼片段- *AspNetWebApiSpa-Ex1-TriviaControllerUsings*）

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample9.cs)]
8. 在**TriviaController**類別的開頭新增下列程式碼，以定義、初始化及處置控制器中的**TriviaCoNtext**實例。

    （程式碼片段- *AspNetWebApiSpa-Ex1-TriviaControllerCoNtext*）

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample10.cs)]

    > [!NOTE]
    > **TriviaController**的**dispose**方法會叫用**TriviaCoNtext**實例的**dispose**方法，以確保在處置或垃圾收集**TriviaCoNtext**實例時，會釋放內容物件所使用的所有資源。 這包括關閉 Entity Framework 開啟的所有資料庫連接。
9. 將下列 helper 方法新增至**TriviaController**類別的結尾。 這個方法會從資料庫中抓取下列測驗問題，以供指定的使用者回答。

    （程式碼片段- *AspNetWebApiSpa-Ex1-TriviaControllerNextQuestion*）

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample11.cs)]
10. 將下列**Get**動作方法新增至**TriviaController**類別。 這個動作方法會呼叫在上一個步驟中定義的**NextQuestionAsync** helper 方法，以取得已驗證使用者的下一個問題。

    （程式碼片段- *AspNetWebApiSpa-Ex1-TriviaControllerGetAction*）

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample12.cs)]
11. 將下列 helper 方法新增至**TriviaController**類別的結尾。 這個方法會將指定的答案儲存在資料庫中，並傳回布林值，指出答案是否正確。

    （程式碼片段- *AspNetWebApiSpa-Ex1-TriviaControllerStoreAsync*）

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample13.cs)]
12. 將下列**Post**動作方法新增至**TriviaController**類別。 此動作方法會將答案與已驗證的使用者建立關聯，並呼叫**StoreAsync** helper 方法。 然後，它會傳送回應，其中包含 helper 方法所傳回的布林值。

    （程式碼片段- *AspNetWebApiSpa-Ex1-TriviaControllerPostAction*）

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample14.cs)]
13. 修改 Web API 控制器，藉由將**授權**屬性新增至**TriviaController**類別定義，來限制已驗證使用者的存取權。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample15.cs)]

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a>工作3–執行解決方案

在此工作中，您將確認您在上一個工作中建立的 Web API 服務是否如預期般運作。 您將使用 Internet Explorer **F12 開發人員工具**來捕獲網路流量，並檢查 Web API 服務的完整回應。

> [!NOTE]
> 請確定已在 [Visual Studio] 工具列上的 [**開始**] 按鈕中選取**Internet Explorer** 。
> 
> ![Internet Explorer 選項](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image9.png)

1. 按 **F5** 執行方案。 [**登入**] 頁面應該會出現在瀏覽器中。

    > [!NOTE]
    > 當應用程式啟動時，預設的 MVC 路由會觸發，其預設會對應至**HomeController**類別的**索引**動作。 由於**HomeController**僅限於已驗證的使用者（請記住，您已使用練習1中的**授權**屬性來裝飾該類別），而且尚未驗證使用者，因此應用程式會將原始要求重新導向至 [登入] 頁面。

    ![正在執行解決方案](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "正在執行解決方案")

    *正在執行解決方案*
2. 按一下 [**註冊**] 以建立新的使用者。

    ![註冊新的使用者](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "註冊新的使用者")

    *註冊新的使用者*
3. 在 [**註冊**] 頁面中，輸入**使用者名稱**和**密碼**，然後按一下 [**註冊**]。

    ![註冊頁面](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "註冊頁面")

    *註冊頁面*
4. 應用程式會註冊新帳戶，並驗證使用者並重新導向至首頁。

    ![使用者已通過驗證](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "使用者已驗證")

    *使用者已通過驗證*
5. 在瀏覽器中，按**F12**開啟 [**開發人員工具**] 面板。 按**CTRL + 4**或按一下**網路**圖示，然後按一下綠色箭號按鈕以開始捕獲網路流量。

    ![正在起始 Web API 網路捕獲](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "正在起始 Web API 網路捕獲")

    *正在起始 Web API 網路捕獲*
6. 將**api/邏輯**附加至瀏覽器網址列中的 URL。 您現在會從**TriviaController**中的**Get**動作方法，檢查回應的詳細資料。

    ![透過 Web API 抓取下一個問題資料](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "透過 Web API 抓取下一個問題資料")

    *透過 Web API 抓取下一個問題資料*

    > [!NOTE]
    > 下載完成後，系統會提示您對下載的檔案進行動作。 讓對話方塊保持開啟狀態，以便能夠透過 [開發人員] 工具視窗觀看回應內容。
7. 現在，您將會檢查回應的主體。 若要這樣做，請按一下 [**詳細資料**] 索引標籤，然後按一下 [**回應主體**]。 您可以使用屬性**選項**（這是**TriviaOption**物件的清單）、**識別碼**和對應至**TriviaQuestion**類別的**標題**，檢查下載的資料是否為物件。

    ![查看 Web API 回應主體](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "查看 Web API 回應主體")

    *查看 Web API 回應主體*
8. 返回 Visual Studio，然後按**SHIFT + F5**停止調試。

<a id="Exercise2"></a>
### <a name="exercise-2-creating-the-spa-interface"></a>練習2：建立 SPA 介面

在此練習中，您將會先建立萬能技客測驗的 web 前端部分，並將焦點放在使用**AngularJS**的單一頁面應用程式互動。 接著，您將使用 CSS3 來增強使用者體驗，以執行豐富的動畫，並在從一個問題轉換到下一個時，提供內容切換的視覺效果。

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-the-spa-interface-using-angularjs"></a>工作1–使用 AngularJS 建立 SPA 介面

在這項工作中，您將使用**AngularJS**來執行萬能技客測驗應用程式的用戶端。 **AngularJS**是一種開放原始碼 JavaScript 架構，可使用*模型視圖控制器*（MVC）功能來增強瀏覽器型應用程式，同時加速開發和測試。

您會從 Visual Studio 的套件管理員主控台開始安裝 AngularJS。 接著，您將建立控制器來提供萬能技客測驗應用程式的行為，以及使用 AngularJS 範本引擎呈現測驗問題和答案的視圖。

> [!NOTE]
> 如需 AngularJS 的詳細資訊，請參閱[[http://angularjs.org/](http://angularjs.org/)](http://angularjs.org/)。

1. 開啟 [ **Visual Studio Express 2013 For Web** ]，然後開啟位於 [**來源/Ex2-CreatingASPAInterface/開始**] 資料夾中的 [ **GeekQuiz** ] 解決方案。 或者，您可以繼續使用您在上一個練習中取得的解決方案。
2. 從 [**工具**] > [ **NuGet 套件管理員**] 開啟 [**套件管理員主控台**]。 輸入下列命令以安裝**AngularJS** NuGet 套件。

    [!code-powershell[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample16.ps1)]
3. 在**方案總管**中，以滑鼠右鍵按一下**GeekQuiz**專案的 [**腳本**] 資料夾，然後選取 [**新增] |新增資料夾**。 將資料夾命名為**應用程式**，然後按**enter**。
4. 以滑鼠右鍵按一下您剛建立的**應用程式**資料夾，然後選取 [**新增] |JavaScript**檔案。

    ![建立新的 JavaScript 檔案](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image17.png)

    *建立新的 JavaScript 檔案*
5. 在 [**指定專案的名稱**] 對話方塊中，于 [**專案名稱**] 文字方塊中輸入 [*測驗-控制器*]，然後按一下 **[確定]** 。

    ![命名新的 JavaScript 檔案](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image18.png)

    *命名新的 JavaScript 檔案*
6. 在**quiz-controller**檔案中，新增下列程式碼以宣告和初始化 AngularJS **QuizCtrl**控制器。

    （程式碼片段- *AspNetWebApiSpa-Ex2-AngularQuizController*）

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample17.js)]

    > [!NOTE]
    > **QuizCtrl**控制器的函式函數需要名為 **$scope**的得以插入參數。 範圍的初始狀態應該在函式函式中設定，方法是將屬性附加至 **$scope**物件。 屬性包含**視圖模型**，而且可以在註冊控制器時，供範本存取。
    > 
    > **QuizCtrl**控制器是在名為**QuizApp**的模組內定義。 模組是工作單位，可讓您將應用程式分成不同的元件。 使用模組的主要優點在於程式碼較容易瞭解，並可協助進行單元測試、重複使用和可維護性。
7. 您現在會將行為新增至範圍，以回應從視圖觸發的事件。 在**QuizCtrl**控制器的結尾新增下列程式碼，以在 **$scope**物件中定義**nextQuestion**函數。

    （程式碼片段- *AspNetWebApiSpa-Ex2-AngularQuizControllerNextQuestion*）

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample18.js)]

    > [!NOTE]
    > 此函式會從上一個練習中建立的**邏輯**Web API 抓取下一個問題，並將問題資料附加至 **$scope**物件。
8. 在**QuizCtrl**控制器的結尾插入下列程式碼，以在 **$scope**物件中定義**sendAnswer**函數。

    （程式碼片段- *AspNetWebApiSpa-Ex2-AngularQuizControllerSendAnswer*）

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample19.js)]

    > [!NOTE]
    > 此函式會將使用者選取的答案傳送至**邏輯**Web API，並將結果（亦即答案是否正確）儲存在 **$scope**物件中。
    > 
    > 上述的**nextQuestion**和**sendAnswer**函式會使用 AngularJS **$HTTP**物件，透過瀏覽器中的 XMLHttpRequest JAVASCRIPT 物件來抽象化與 Web API 的通訊。 AngularJS 支援另一項服務，可透過 RESTful Api，引進更高層級的抽象概念，對資源執行 CRUD 作業。 AngularJS **$resource**物件具有動作方法，可提供高階行為，而不需要與 **$HTTP**物件互動。 請考慮在需要 CRUD 模型的案例中使用 **$resource**物件（前景資訊，請參閱[$resource 檔](https://docs.angularjs.org/api/ngResource/service/$resource)）。
9. 下一步是建立可定義測驗視圖的 AngularJS 範本。 若要這麼做，請開啟 Views 內的**Index. cshtml**檔案 **|主**資料夾，並將內容取代為下列程式碼。

    （程式碼片段- *AspNetWebApiSpa-Ex2-GeekQuizView*）

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample20.cshtml)]

    > [!NOTE]
    > AngularJS 範本是一種宣告式規格，它會使用來自模型的資訊和控制器，將靜態標記轉換成使用者在瀏覽器中看到的動態視圖。 以下是可在範本中使用的 AngularJS 元素和元素屬性範例：
    > 
    > - **Ng 應用**程式指示詞會告訴 AngularJS 代表應用程式之根項目的 DOM 元素。
    > - **Ng 控制器**指示詞會在宣告指示詞的位置，將控制器附加至 DOM。
    > - 大括弧標記法 **{{}}** 代表控制器中定義之範圍屬性的系結。
    > - **Ng click**指示詞是用來叫用範圍中定義的函式，以回應使用者按下的動作。
10. 開啟**Content**資料夾內的 **.css**檔案，並在檔案結尾新增下列反白顯示的樣式，以提供測驗視圖的外觀與風格。

    （程式碼片段- *AspNetWebApiSpa-Ex2-GeekQuizStyles*）

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample21.css)]

<a id="Ex2Task2"></a>
#### <a name="task-2--running-the-solution"></a>工作2–執行解決方案

在這項工作中，您將使用以 AngularJS 建立的新使用者介面來執行解決方案，以回答一些測驗問題。

1. 按 **F5** 執行方案。
2. 註冊新的使用者帳戶。 若要這麼做，請遵循練習1，工作3中所述的註冊步驟。

    > [!NOTE]
    > 如果您使用上一個練習中的解決方案，您可以使用先前建立的使用者帳戶登入。
3. 首頁**應該**會出現，並顯示測驗的第一個問題。 按一下其中一個選項來回答問題。 這會觸發稍早定義的**sendAnswer**函式，這會將選取的選項傳送至**邏輯**Web API。

    ![回答問題](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "回答問題")

    *回答問題*
4. 按一下其中一個按鈕之後，應該會出現答案。 按一下 **[下一個問題]** 以顯示下列問題。 這會觸發控制器中定義的**nextQuestion**函數。

    ![要求下一個問題](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "要求下一個問題")

    *要求下一個問題*
5. 下一個問題應該會出現。 依照您的需要，繼續回答問題數次。 完成所有問題之後，您應該會回到第一個問題。

    ![另一個問題](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "另一個問題")

    *下一個問題*
6. 返回 Visual Studio，然後按**SHIFT + F5**停止調試。

<a id="Ex2Task3"></a>
#### <a name="task-3--creating-a-flip-animation-using-css3"></a>工作 3-使用 CSS3 建立翻轉動畫

在這項工作中，您將使用 CSS3 屬性來執行豐富的動畫，方法是在問題獲得解答時新增翻轉效果，以及何時抓取下一個問題。

1. 在**方案總管**中，以滑鼠右鍵按一下**GeekQuiz**專案的 [ **Content** ] 資料夾，然後選取 [**新增] |現有專案 ...** 。

    ![將現有的專案加入至 Content 資料夾](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "將現有的專案加入至 Content 資料夾")

    *將現有的專案加入至 Content 資料夾*
2. 在 [**加入現有專案**] 對話方塊中，流覽至 [**來源/資產**] 資料夾，然後選取 [ **Flip .css**]。 按一下 [新增]。

    ![從資產新增 Flip .css 檔案](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "從資產新增 Flip .css 檔案")

    *從資產新增 Flip .css 檔案*
3. 開啟您剛才新增的**Flip .css**檔案，並檢查其內容。
4. 找出**翻轉轉換**批註。 該批註底下的樣式會使用 CSS 的**觀點**和**rotateY**轉換來產生 &quot;卡翻轉&quot; 效果。

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample22.css)]
5. 在翻轉批註期間，找出窗格的 [**隱藏後一步]** 。 此批註底下的樣式會在臉部離開檢視器時，將**背面可見度**CSS 屬性設定為*hidden*，以隱藏其後端。

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample23.css)]
6. 開啟**應用程式\_[開始**] 資料夾中的**BundleConfig.cs**檔案，並將參考新增至 **&quot;~/Content/css&quot;** 樣式組合中的**Flip .css**檔案

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample24.cs)]
7. 按**F5**執行方案，並使用您的認證登入。
8. 按一下其中一個選項來回答問題。 請注意在流覽之間轉換時的翻轉效果。

    ![使用翻轉效果回答問題](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "使用翻轉效果回答問題")

    *使用翻轉效果回答問題*
9. 按一下 **[下一個問題]** 以取得下列問題。 翻轉效果應該會再次出現。

    ![使用 flip 效果抓取下列問題](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "使用 flip 效果抓取下列問題")

    *使用 flip 效果抓取下列問題*

---

<a id="Summary"></a>
## <a name="summary"></a>總結

藉由完成此實際操作實驗室，您已瞭解如何：

- 使用 ASP.NET 的框架建立 ASP.NET Web API 控制器
- 執行 Web API Get 動作以取得下一個測驗問題
- 執行 Web API Post 動作以儲存測驗解答
- 從 Visual Studio 套件管理員主控台安裝 AngularJS
- 執行 AngularJS 範本和控制器
- 使用 CSS3 轉換來執行動畫效果
