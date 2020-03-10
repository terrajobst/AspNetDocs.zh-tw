---
uid: signalr/overview/getting-started/real-time-web-applications-with-signalr
title: 實習實驗室：使用 SignalR 的即時 Web 應用程式 |Microsoft Docs
author: bradygaster
description: 即時 Web 應用程式可讓您即時將伺服器端內容推送至連線的用戶端。 針對 ASP.NET 開發人員，ASP ...。
ms.author: bradyg
ms.date: 07/16/2014
ms.assetid: ba07958c-42e1-4da0-81db-ba6925ed6db0
msc.legacyurl: /signalr/overview/getting-started/real-time-web-applications-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 9e39fd3f2fc9d4e791002450085215096c222fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78537097"
---
# <a name="hands-on-lab-real-time-web-applications-with-signalr"></a>實習實驗室：使用 SignalR 的即時 Web 應用程式

依[Web Camp 團隊](https://twitter.com/webcamps)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[下載 Web Camp 訓練套件，2015年10月版本](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)

> 即時 Web 應用程式可讓您即時將伺服器端內容推送至連線的用戶端。 針對 ASP.NET 開發人員， **ASP.NET SignalR**是一種程式庫，可將即時 web 功能新增至其應用程式。 它會利用數個傳輸，並根據用戶端和伺服器的最佳可用傳輸，自動選取最佳可用的傳輸。 它會利用**WebSocket**，這是可在瀏覽器和伺服器之間進行雙向通訊的 HTML5 API。
> 
> **SignalR**也提供簡單的高階 API，可在您的 ASP.NET 應用程式中執行伺服器到用戶端 RPC （從伺服器端的 .net 程式碼呼叫 JavaScript 函式），以及為連線管理新增有用的勾點，例如連接/中斷線上活動、群組連接和授權。
> 
> **SignalR**是在用戶端與伺服器之間進行即時工作所需的一些傳輸的抽象概念。 **SignalR**連線會以 HTTP 啟動，然後升級至**WebSocket**連線（如果有的話）。 **WebSocket**是**SignalR**的理想傳輸，因為它最有效率地使用伺服器記憶體、具有最低延遲，而且具有最基本的功能（例如用戶端與伺服器之間的全雙工通訊），但它也具有最嚴格的需求： **WebSocket**要求伺服器必須使用**windows server 2012**或**windows 8**，以及 **.NET Framework 4.5**。 如果不符合這些需求， **SignalR**會嘗試使用其他傳輸來建立其連接（例如*Ajax 長輪詢*）。
> 
> **SignalR** API 包含兩個可在用戶端和伺服器之間通訊的模型：**持續**連線和**中樞**。 **連接**代表傳送單一收件者、群組或廣播訊息的簡單端點。 **中樞**是以連線 API 為基礎所建立的高階管線，可讓您的用戶端和伺服器直接對彼此呼叫方法。
> 
> ![SignalR 架構](real-time-web-applications-with-signalr/_static/image1.png)
> 
> 所有範例程式碼和程式碼片段都包含在2015年10月版的 Web Camp 訓練套件中，可在[https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)取得。  請注意，該頁面上的安裝程式連結將無法再運作;請改為使用 [資產] 區段下的其中一個連結。

<a id="Overview"></a>
## <a name="overview"></a>概觀

<a id="Objectives"></a>
### <a name="objectives"></a>目標

在此實際操作實驗室中，您將瞭解如何：

- 使用 SignalR 將通知從伺服器傳送至用戶端。
- 使用**SQL Server**Scale Out SignalR 應用程式。

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Prerequisites

若要完成此實際操作實驗室，需要下列各項：

- [適用于 Web 或更新版本的 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)

<a id="Setup"></a>
### <a name="setup"></a>安裝程式

為了在此實際操作實驗室中執行練習，您必須先設定您的環境。

1. 開啟 Windows Explorer 視窗，並流覽至實驗室的 [**源**] 資料夾。
2. 以滑鼠右鍵按一下 [ **Setup** ]，然後選取 [以**系統管理員身分執行**] 來啟動安裝程式，以設定您的環境並安裝此實驗室的 Visual Studio 程式碼片段。
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

1. [使用 SignalR 處理即時資料](#Exercise1)
2. [使用 SQL Server 相應放大](#Exercise2)

完成此實驗室的預估時間： **60 分鐘**

> [!NOTE]
> 當您第一次啟動 Visual Studio 時，您必須選取其中一個預先定義的設定集合。 每個預先定義的集合都是設計來符合特定的開發風格，並決定視窗配置、編輯器行為、IntelliSense 程式碼片段和對話方塊選項。 本實驗室中的程式說明在使用 [**一般開發設定**] 集合時，在 Visual Studio 中完成指定工作所需的動作。 如果您針對開發環境選擇不同的 [設定] 集合，您應該考慮的步驟可能會有所差異。

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-real-time-data-using-signalr"></a>練習1：使用 SignalR 處理即時資料

雖然對話通常是用來做為範例，但您可以使用即時 Web 功能來完成更多工作。 每當使用者重新整理網頁以查看新資料或頁面執行 Ajax 長期輪詢來取得新資料時，您可以使用 SignalR。

SignalR 支援**伺服器推**播或**廣播**功能;它會自動處理連接管理。 在用戶端-伺服器通訊的傳統 HTTP 連線中，會針對每個要求重新建立連線，但 SignalR 會提供用戶端與伺服器之間的持續連線。 在 SignalR 中，伺服器程式碼會使用遠端程序呼叫（RPC）來呼叫瀏覽器中的用戶端程式代碼，而不是我們今天知道的要求-回應模型。

在此練習中，您會將**萬能技客測驗**應用程式設定為使用 SignalR，以更新的計量顯示統計資料儀表板，而不需要重新整理整個頁面。

<a id="Ex1Task1"></a>
#### <a name="task-1--exploring-the-geek-quiz-statistics-page"></a>工作1–探索萬能技客測驗統計資料頁面

在這項工作中，您將會經歷應用程式，並確認統計資料頁面的顯示方式，以及如何改善資訊的更新方式。

1. 開啟 [ **Visual Studio Express 2013 For Web** ]，然後開啟位於**Source\Ex1-WorkingWithRealTimeData\Begin**資料夾中的 [ **GeekQuiz** ] 解決方案。
2. 按 **F5** 執行方案。 [**登入**] 頁面應該會出現在瀏覽器中。

    ![正在執行解決方案](real-time-web-applications-with-signalr/_static/image2.png "正在執行解決方案")

    *正在執行解決方案*
3. 按一下頁面右上角的 [**註冊**]，在應用程式中建立新的使用者。

    ![註冊連結](real-time-web-applications-with-signalr/_static/image3.png "註冊連結")

    *註冊連結*
4. 在 [**註冊**] 頁面中，輸入**使用者名稱**和**密碼**，然後按一下 [**註冊**]。

    ![註冊使用者](real-time-web-applications-with-signalr/_static/image4.png "註冊使用者")

    *註冊使用者*
5. 應用程式會註冊新帳戶，並驗證使用者並重新導向至顯示第一個測驗問題的首頁。
6. 在新視窗中開啟 [**統計資料]** 頁面，然後並排放置 [**首頁**] 和 [**統計資料]** 頁面。

    ![並存視窗](real-time-web-applications-with-signalr/_static/image5.png "並存視窗")

    *並存視窗*
7. 在首頁**中**，按一下其中一個選項來回答問題。

    ![回答問題](real-time-web-applications-with-signalr/_static/image6.png "回答問題")

    *回答問題*
8. 按一下其中一個按鈕之後，應該會出現答案。

    ![問題解答正確](real-time-web-applications-with-signalr/_static/image7.png "問題解答正確")

    *已正確回答問題*
9. 請注意，統計資料頁面中提供的資訊已過期。 重新整理頁面，以便查看更新的結果。

    ![統計資料頁面](real-time-web-applications-with-signalr/_static/image8.png "統計資料頁面")

    *統計資料頁面*
10. 返回 Visual Studio 並停止調試。

<a id="Ex1Task2"></a>
#### <a name="task-2--adding-signalr-to-geek-quiz-to-show-online-charts"></a>工作2–將 SignalR 新增至萬能技客測驗以顯示線上圖表

在這項工作中，您會將 SignalR 新增至解決方案，並在新的回應傳送至伺服器時，自動將更新傳送至用戶端。

1. 從 Visual Studio 的 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後按一下 [**套件管理員主控台**]。
2. 在 [**套件管理員主控台**] 視窗中，執行下列命令：

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample1.ps1)]

    ![SignalR 套件安裝](real-time-web-applications-with-signalr/_static/image9.png "SignalR 套件安裝")

    *SignalR 套件安裝*

   > [!NOTE]
   > 從全新的 MVC 5 應用程式安裝**SignalR** NuGet 套件版本2.0.2 時，您必須手動將**OWIN**套件更新為2.0.1 版（或更高版本），才能安裝 SignalR。 若要這樣做，您可以在 [**套件管理員主控台**] 中執行下列腳本：
   > 
   > [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample2.ps1)]
   > 
   > 在未來的 SignalR 版本中，將會自動更新 OWIN 相依性。
3. 在**方案總管**中，展開 [**腳本**] 資料夾，並注意 SignalR *js*檔案已新增至方案。

    ![SignalR JavaScript 參考](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript 參考")

    *SignalR JavaScript 參考*
4. 在**方案總管**中，以滑鼠右鍵按一下**GeekQuiz**專案，選取 [**新增] | 新資料夾**，並**將**其命名為 [**中樞**]。
5. 以滑鼠右鍵按一下 [**中樞**] 資料夾，然後選取 [**新增] |新專案**。

    ![加入新專案](real-time-web-applications-with-signalr/_static/image11.png "加入新項目")

    *加入新專案*
6. 在 [**加入新專案**] 對話方塊中，選取 **[ C#視覺效果] |Web |** 在左窗格中的 [SignalR] 節點中，從中央窗格中選取 [ **SignalR Hub Class （v2）** ]，將檔案命名為**StatisticsHub.cs** ，然後按一下 [**新增**]。

    ![[加入新專案] 對話方塊](real-time-web-applications-with-signalr/_static/image12.png "[加入新專案] 對話方塊")

    *[加入新專案] 對話方塊*
7. 將**StatisticsHub**類別中的程式碼取代為下列程式碼。

    （程式碼片段- *RealTimeSignalR-Ex1-StatisticsHubClass*）

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample3.cs)]
8. 開啟**Startup.cs** ，**並在設定方法的**結尾新增下列程式程式碼。

    （程式碼片段- *RealTimeSignalR-Ex1-MapSignalR*）

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample4.cs)]
9. 開啟 [**服務**] 資料夾內的 [ **StatisticsService.cs** ] 頁面，並新增下列 using 指示詞。

    （程式碼片段- *RealTimeSignalR-Ex1-UsingDirectives*）

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample5.cs)]
10. 若要通知已連線用戶端的更新，您必須先抓取目前連接的**內容**物件。 **Hub**物件包含將訊息傳送至單一用戶端或廣播至所有已連線用戶端的方法。 將下列方法新增至**StatisticsService**類別，以廣播統計資料。

    （程式碼片段- *RealTimeSignalR-Ex1-NotifyUpdatesMethod*）

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample6.cs)]

    > [!NOTE]
    > 在上述程式碼中，您會使用任意方法名稱來呼叫用戶端上的函式（亦即： *updateStatistics*）。 您指定的方法名稱會被視為動態物件，這表示沒有任何 IntelliSense 或編譯時間驗證。 運算式會在執行時間進行評估。 當方法呼叫執行時，SignalR 會將方法名稱和參數值傳送給用戶端。 如果用戶端具有符合名稱的方法，則會呼叫該方法，並將參數值傳遞給它。 如果在用戶端上找不到相符的方法，則不會引發錯誤。 如需詳細資訊，請參閱[ASP.NET SignalR HUB API Guide](../guide-to-the-api/hubs-api-guide-server.md)。
11. 開啟 [**控制器**] 資料夾內的 [ **TriviaController.cs** ] 頁面，並新增下列 using 指示詞。

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample7.cs)]
12. 將下列反白顯示的程式碼新增至**Post**動作方法。

    （程式碼片段- *RealTimeSignalR-Ex1-NotifyUpdatesCall*）

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample8.cs)]
13. 開啟 Views 內的**Statistics. cshtml**頁面 **|主**資料夾。 找出 [**腳本**] 區段，並在區段的開頭新增下列腳本參考。

    （程式碼片段- *RealTimeSignalR-Ex1-SignalRScriptReferences*）

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample9.cshtml)]

    > [!NOTE]
    > 當您將 SignalR 和其他腳本程式庫新增至 Visual Studio 專案時，套件管理員可能會安裝比本主題中所示版本還新的 SignalR 腳本檔案版本。 請確定程式碼中的腳本參考符合您的專案中所安裝的腳本程式庫版本。
14. 新增下列反白顯示的程式碼，將用戶端連接到 SignalR 中樞，並在從中樞收到新訊息時，更新統計資料。

    （程式碼片段- *RealTimeSignalR-Ex1-SignalRClientCode*）

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample10.cshtml)]

    在此程式碼中，您會建立中樞 Proxy，並註冊事件處理常式來接聽伺服器所傳送的訊息。 在此情況下，您會接聽透過*updateStatistics*方法傳送的訊息。

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a>工作3–執行解決方案

在這項工作中，您將執行解決方案，以確認在回答新問題之後，會使用 SignalR 自動更新統計資料檢視。

1. 按 **F5** 執行方案。

    > [!NOTE]
    > 如果尚未登入應用程式，請使用您在工作1中建立的使用者登入。
2. 在新視窗中開啟 [**統計資料]** 頁面，並將 [**首頁**] 和 [**統計資料]** 頁面並排放在工作1中。
3. 在首頁**中**，按一下其中一個選項來回答問題。

    ![回答另一個問題](real-time-web-applications-with-signalr/_static/image13.png "回答另一個問題")

    *回答另一個問題*
4. 按一下其中一個按鈕之後，應該會出現答案。 請注意，在使用更新的資訊回答問題之後，會自動更新頁面上的統計資料資訊，而不需要重新整理整個頁面。

    ![在解答之後重新整理統計資料頁面](real-time-web-applications-with-signalr/_static/image14.png "在解答之後重新整理統計資料頁面")

    *在解答之後重新整理統計資料頁面*

<a id="Exercise2"></a>
### <a name="exercise-2-scaling-out-using-sql-server"></a>練習2：使用 SQL Server 相應放大

調整 web 應用程式時，您通常可以在相應*增加*和*相應*放大選項之間選擇。 相應*增加*表示使用較大的伺服器，包含更多資源（CPU、RAM 等等），而*相應*放大則表示新增更多伺服器來處理負載。 後者的問題是，用戶端可以路由傳送至不同的伺服器。 連接到一部伺服器的用戶端不會接收從另一部伺服器傳送的訊息。

您可以使用稱為*背板*的元件來解決這些問題，以便在伺服器之間轉送訊息。 啟用背板後，每個應用程式實例會將訊息傳送至後擋板，而背板會將它們轉送至其他應用程式實例。

目前有三種類型的背板可用於 SignalR：

- **Windows Azure 服務匯流排**。 服務匯流排是一種訊息基礎結構，可讓元件傳送鬆散耦合的訊息。
- **SQL Server**。 SQL Server 背板會將訊息寫入至 SQL 資料表。 背板會使用 Service Broker 來提供有效率的訊息。 不過，如果未啟用 Service Broker，它也可以運作。
- **Redis**。 Redis 是記憶體中的索引鍵/值存放區。 Redis 支援發行/訂閱（"pub/sub"）模式來傳送訊息。

每則訊息都會透過訊息匯流排傳送。 訊息匯流排會執行[IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx)介面，以提供發佈/訂閱抽象概念。 背板的工作方式是將預設**IMessageBus**取代為針對該後擋板設計的匯流排。

每個伺服器實例都會透過匯流排連接至後擋板。 當傳送訊息時，它會移至背板，而背板會將它傳送到每一部伺服器。 當伺服器從背板接收訊息時，它會將訊息儲存在其本機快取中。 接著，伺服器會從其本機快取將訊息傳遞給用戶端。

如需 SignalR 背板運作方式的詳細資訊，請閱讀這[篇文章](../performance/scaleout-in-signalr.md)。

> [!NOTE]
> 在某些情況下，背板可能會變成瓶頸。 以下是一些典型的 SignalR 案例：
> 
> - [伺服器廣播](tutorial-server-broadcast-with-signalr.md)（例如股票行情指示器）：背板適用于此案例，因為伺服器會控制傳送訊息的速率。
> - [用戶端對用戶端](tutorial-getting-started-with-signalr.md)（例如聊天）：在此案例中，如果訊息數目隨著用戶端數目調整，則背板可能是瓶頸;也就是說，如果訊息的速率會隨著更多用戶端聯結而按比例成長。
> - [高頻率即時](tutorial-high-frequency-realtime-with-signalr.md)（例如即時遊戲）：在此案例中不建議使用背板。

在此練習中，您將使用**SQL Server**在**萬能技客測驗**應用程式中散發訊息。 您將會在單一測試電腦上執行這些工作，以瞭解如何設定設定，但為了獲得完整的效果，您必須將 SignalR 應用程式部署到兩部以上的伺服器。 您也必須在其中一部伺服器上，或在個別的專用伺服器上安裝 SQL Server。

![使用 SQL Server 圖表 Scale Out](real-time-web-applications-with-signalr/_static/image15.png)

<a id="Ex2Task1"></a>
#### <a name="task-1---understanding-the-scenario"></a>工作 1-瞭解案例

在這項工作中，您將執行2個**萬能技客測驗**實例，在本機電腦上模擬多個 IIS 實例。 在此案例中，當您在某一個應用程式上回答邏輯問題時，不會在第二個實例的 [統計資料] 頁面上通知更新。 此模擬類似于將您的應用程式部署在多個實例上，並使用負載平衡器與其通訊的環境。

1. 開啟位於 [**來源/Ex2-ScalingOutWithSQLServer/開始**] 資料夾中的 [**開始 .sln** ] 解決方案。 載入之後，您會注意到**伺服器總管**解決方案有兩個專案具有相同的結構，但名稱不同。 這會在您的本機電腦上模擬相同應用程式的兩個實例。

    ![開始模擬2個萬能技客測驗實例的解決方案](real-time-web-applications-with-signalr/_static/image16.png "開始模擬2個萬能技客測驗實例的解決方案")

    *開始模擬2個萬能技客測驗實例的解決方案*
2. 以滑鼠右鍵按一下方案節點，然後選取 [**屬性**]，以開啟方案的 [屬性] 頁面。 在 [**啟始專案**] 底下，選取 [**多個啟始專案**]，並將兩個專案的**動作**值變更為 [*啟動*]

    ![啟動多個專案](real-time-web-applications-with-signalr/_static/image17.png "啟動多個專案")

    *啟動多個專案*
3. 按 **F5** 執行方案。 應用程式會在不同的埠中啟動兩個**萬能技客測驗**實例，模擬相同應用程式的多個實例。 將左側的其中一個瀏覽器釘選到螢幕右側的另一個。 使用您的認證登入，或註冊新的使用者。 登入之後，請將 [邏輯] 頁面保持在左側，並移至右側瀏覽器中的 [**統計資料]** 頁面。

    ![並排萬能技客測驗](real-time-web-applications-with-signalr/_static/image18.png)

    *並排萬能技客測驗*

    ![不同埠中的萬能技客測驗](real-time-web-applications-with-signalr/_static/image19.png)

    *不同埠中的萬能技客測驗*
4. 在左側瀏覽器中開始回答問題，您會注意到右側瀏覽器中的 [**統計資料]** 頁面並未更新。 這是因為**SignalR**會使用本機快取，將訊息散發到其用戶端，而此案例會模擬多個實例，因此不會在兩者之間共用快取。 您可以藉由測試相同的步驟，但使用單一應用程式，來確認**SignalR**是否正常運作。 在下列工作中，您將設定背板來複寫各個實例的訊息。
5. 返回 Visual Studio 並停止調試。

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-sql-server-backplane"></a>工作2–建立 SQL Server 背板

在這項工作中，您將建立一個將作為**萬能技客測驗**應用程式後擋板的資料庫。 您將使用**SQL Server 物件總管**來流覽伺服器並初始化資料庫。 此外，您將會啟用**Service Broker**。

1. 在**Visual Studio**中，開啟功能表**視圖**並選取 [ **SQL Server 物件總管**]。
2. 以滑鼠右鍵按一下 [ **SQL Server** ] 節點，然後選取 [**新增 SQL Server** ] 選項，以連接到您的 LocalDB 實例。

    ![加入 SQL Server 實例](real-time-web-applications-with-signalr/_static/image20.png "加入 SQL Server 實例")

    *將 SQL Server 實例新增至 SQL Server 物件總管*
3. 將 [**伺服器名稱**] 設定為 *（localdb） \v11.0* ，並將 [ **Windows 驗證**] 保留為您的驗證模式。 按一下 [連接] 以繼續。

    ![連接到 LocalDB](real-time-web-applications-with-signalr/_static/image21.png "連接到 LocalDB")

    *連接到 LocalDB*
4. 既然您已連接到 LocalDB 實例，您將需要建立一個資料庫，以代表 SignalR 的 SQL Server 背板。 若要這樣做，請以滑鼠右鍵按一下 [**資料庫**] 節點，然後選取 [**加入新的資料庫**]。

    ![加入新的資料庫](real-time-web-applications-with-signalr/_static/image22.png "加入新的資料庫")

    *加入新的資料庫*
5. 將資料庫名稱設定為*SignalR* ，然後按一下 **[確定]** 加以建立。

    ![建立 SignalR 資料庫](real-time-web-applications-with-signalr/_static/image23.png "建立 SignalR 資料庫")

    *建立 SignalR 資料庫*

    > [!NOTE]
    > 您可以為資料庫選擇任何名稱。
6. 若要從背板更有效率地接收更新，建議您啟用資料庫的 Service Broker。 Service Broker 在 SQL Server 中提供訊息和佇列的原生支援。 背板也可以運作，而不 Service Broker。 以滑鼠右鍵按一下資料庫，然後選取 [追加**查詢**]，以開啟新的查詢。

    ![開啟新的查詢](real-time-web-applications-with-signalr/_static/image24.png "開啟新的查詢")

    *開啟新的查詢*
7. 若要檢查是否已啟用 Service Broker，請查詢**sys.databases**目錄檢視中 **\_Broker\_enabled**資料行。 在最近開啟的查詢視窗中執行下列腳本。

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample11.sql)]

    ![查詢 Service Broker 狀態](real-time-web-applications-with-signalr/_static/image25.png "查詢 Service Broker 狀態")

    *查詢 Service Broker 狀態*
8. 如果您資料庫中 **\_broker\_已啟用**資料行的值為 &quot;0&quot;，請使用下列命令來啟用它。 使用您在建立資料庫時所設定的名稱（例如： SignalR），取代**您的資料庫&gt;&lt;** 。

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample12.sql)]

    ![啟用 Service Broker](real-time-web-applications-with-signalr/_static/image26.png "啟用 Service Broker")

    *啟用 Service Broker*

    > [!NOTE]
    > 如果此查詢出現鎖死，請確定沒有任何應用程式連接到資料庫。

<a id="Ex2Task3"></a>
#### <a name="task-3--configuring-the-signalr-application"></a>工作 3-設定 SignalR 應用程式

在這項工作中，您將設定**萬能技客測驗**以連接到 SQL Server 背板。 您會先新增**SignalR** NuGet 套件，並將連接字串設定為您的背板資料庫。

1. 從 [**工具**] > [ **NuGet 套件管理員**] 開啟 [**套件管理員主控台**]。 請確定已在 [**預設專案**] 下拉式清單中選取 [ **GeekQuiz**專案]。 輸入下列命令以安裝**SignalR** NuGet 套件。

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample13.ps1)]
2. 重複上一個步驟，但這次是針對 [專案**GeekQuiz2**]。
3. 若要設定 SQL Server 背板，請開啟**GeekQuiz**專案的**Startup.cs**檔案，並將下列程式碼新增至**configure**方法。 以您在建立 SQL Server 後擋板時所使用的資料庫名稱取代**您的資料庫&gt;&lt;** 。 針對**GeekQuiz2**專案重複此步驟。

    （程式碼片段- *RealTimeSignalR-Ex2-StartupConfiguration*）

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample14.cs)]
4. 現在這兩個專案都設定為使用 SQL Server 背板，請按**F5**同時執行它們。
5. 同樣地， **Visual Studio**會在不同的埠中啟動兩個**萬能技客測驗**實例。 將左側的其中一個瀏覽器釘選在畫面右側，然後使用您的認證登入。 保持左側的 [邏輯] 頁面，並移至 [**統計資料]** pagein 正確的瀏覽器。
6. 在左側瀏覽器中開始回答問題。 這次，**統計資料**頁面會因為背板而更新。 在應用程式之間切換（**統計資料**現在位於左側，而**邏輯**位於右邊）並重複測試，以驗證這兩個實例都能正常運作。 背板會作為每個連線伺服器的*共用*訊息快取，而每部伺服器會將訊息儲存在自己的本機快取中，以散發給已連線的用戶端。
7. 返回 Visual Studio 並停止調試。
8. SQL Server 的背板元件會在指定的資料庫上自動產生必要的資料表。 在 [ **SQL Server 物件總管**] 面板中，開啟您為背板建立的資料庫（例如： SignalR），並展開其資料表。 您應該會看到下列資料表：

    ![背板產生的資料表](real-time-web-applications-with-signalr/_static/image27.png)

    *背板產生的資料表*
9. 以滑鼠右鍵按一下  **SignalR\_0**  資料表，然後選取 **查看資料**。

    ![View SignalR 背板訊息資料表](real-time-web-applications-with-signalr/_static/image28.png)

    *View SignalR 背板訊息資料表*
10. 回答邏輯問題時，您可以看到傳送至**中樞**的不同訊息。 背板會將這些訊息散發到任何已連接的實例。

    ![背板訊息資料表](real-time-web-applications-with-signalr/_static/image29.png)

    *背板訊息資料表*

---

<a id="Summary"></a>
## <a name="summary"></a>總結

在此實際操作實驗室中，您已瞭解如何將**SignalR**新增至您的應用程式，並使用**中樞**將通知從伺服器傳送到已連線的用戶端。 此外，當您的應用程式部署在多個 IIS 實例時，您已瞭解如何使用*背板*元件來相應放大應用程式。
