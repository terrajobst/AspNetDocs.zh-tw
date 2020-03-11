---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
title: ASP.NET 4.5 中 Web Forms 的新功能 |Microsoft Docs
author: rick-anderson
description: 新版本的 ASP.NET Web Forms 引進了許多改進，著重于改善使用資料時的使用者體驗。 在舊版中 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 0a1f88bd-97da-4ed1-86f1-605199dc75a4
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: 301af8ed877b58624e419c04f605c41f27dbdd0c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525729"
---
# <a name="whats-new-in-web-forms-in-aspnet-45"></a>ASP.NET 4.5 的 Web Forms 新功能

依[Web Camp 團隊](https://twitter.com/webcamps)

> 新版本的 ASP.NET Web Forms 引進了許多改進，著重于改善使用資料時的使用者體驗。
> 
> 在舊版的 Web form 中，使用資料系結來發出物件成員的值時，您使用的是資料系結運算式 Bind （）或 Eval （）。 在新版本的 ASP.NET 中，您可以使用新的 ItemType 屬性來宣告控制項將要系結的資料類型。 設定這個屬性可讓您使用強型別變數，以獲得 Visual Studio 開發經驗的完整優勢，例如 IntelliSense、成員導覽和編譯時間檢查。
> 
> 使用資料繫結控制項，您現在也可以指定自己的自訂方法來選取、更新、刪除和插入資料，簡化頁面控制項與應用程式邏輯之間的互動。 此外，模型系結功能已新增至 ASP.NET，這表示您可以將頁面中的資料直接對應到方法類型參數。
> 
> 使用最新版的 Web form，驗證使用者輸入也更為容易。 您現在可以使用**system.workflow.componentmodel.activity. DataAnnotations**命名空間中的驗證屬性來標注模型類別，並要求所有的網站控制項都使用該資訊來驗證使用者輸入。 Web form 中的用戶端驗證現在已與 jQuery 整合，提供了更清楚的用戶端程式代碼和不顯眼的 JavaScript 功能。
> 
> 在 [要求驗證] 區域中，已改善，可讓您更輕鬆地關閉應用程式特定部分的要求驗證，或讀取不正確要求資料。
> 
> Web form 伺服器控制項已有一些改進，可利用 HTML5 的新功能：
> 
> - TextBox 控制項的 TextMode 屬性已更新為支援新的 HTML5 輸入類型，例如電子郵件、日期時間等等。
> - FileUpload 控制項現在支援從支援此 HTML5 功能的瀏覽器進行多個檔案上傳。
> - 驗證程式控制項現在支援驗證 HTML5 輸入元素。
> - 具有代表 URL 之屬性的新 HTML5 元素現在支援 runat =&quot;server&quot;。 因此，您可以使用 URL 路徑中的 ASP.NET 慣例，例如 ~ 運算子來代表應用程式根目錄（例如，&lt;video runat =&quot;server&quot; src =&quot;~/myVideo.wmv&quot;&gt;&lt;/video&gt;）。
> - 已修正 UpdatePanel 控制項，以支援張貼 HTML5 輸入欄位。
> 
> 在官方的 ASP.NET 入口網站中，您可以在 ASP.NET WebForms 4.5 中找到更多新功能的範例： [ASP.NET 4.5 和 Visual Studio 2012 中的新](../../../../whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012.md#_Toc318097385)功能
> 
> 所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)取得。

<a id="Objectives"></a>
### <a name="objectives"></a>目標

在此實際操作實驗室中，您將瞭解如何：

- 使用強型別資料系結運算式
- 在 Web Forms 中使用新的模型系結功能
- 使用值提供者將頁面資料對應至程式碼後置方法
- 使用資料批註進行使用者輸入驗證
- 利用 Web Forms 中 jQuery 的不顯眼用戶端驗證
- 執行細微的要求驗證
- 在 Web Forms 中執行非同步網頁處理

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Prerequisites

您必須具有下列專案，才能完成此實驗室：

- 適用于 Web 或上層的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （如需有關如何安裝的指示，請參閱[附錄 A](#AppendixA) ）。

<a id="Setup"></a>
### <a name="setup"></a>安裝程式

**安裝程式碼片段**

為了方便起見，您將在此實驗室中管理的大部分程式碼都是以 Visual Studio 程式碼片段的形式提供。 若要安裝程式碼片段，請執行 **.\Source\Setup\CodeSnippets.vsi**檔案。

如果您不熟悉 Visual Studio Code 程式碼片段，而且想要瞭解如何使用，您可以參閱本檔中的附錄 &quot;[附錄 C：使用程式碼片段](#AppendixC)&quot;。

<a id="Exercises"></a>
## <a name="exercises"></a>練習

這個實際操作實驗室包含下列練習：

1. [練習1： ASP.NET Web Forms 中的模型系結](#Exercise1)
2. [練習2：資料驗證](#Exercise2)
3. [練習3： ASP.NET Web Forms 中的非同步網頁處理](#Exercise3)

> [!NOTE]
> 每個練習都會伴隨一個**結束**資料夾，其中包含您在完成練習之後應該取得的結果解決方案。 如果您需要額外的協助來進行練習，您可以使用此解決方案做為指南。

完成此實驗室的預估時間： **60 分鐘**。

<a id="Exercise1"></a>

<a id="Exercise_1_Model_Binding_in_ASPNET_Web_Forms"></a>
### <a name="exercise-1-model-binding-in-aspnet-web-forms"></a>練習1： ASP.NET Web Forms 中的模型系結

新版本的 ASP.NET Web form 引進了許多增強功能，著重于改善使用資料的經驗。 在此練習中，您將瞭解強型別資料控制和模型系結。

<a id="Task_1_-_Using_Strongly-Typed_Data-Bindings"></a>
#### <a name="task-1---using-strongly-typed-data-bindings"></a>工作 1-使用強型別的資料系結

在這項工作中，您將探索 ASP.NET 4.5 中提供的新強型別系結。

1. 開啟位於**來源/Ex1-ModelBinding/開始/** 資料夾的 [**開始**] 解決方案。

   1. 在繼續之前，您必須先下載一些遺漏的 NuGet 套件。 若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
2. 開啟 [**客戶 .aspx** ] 頁面。 將未編號的清單放在主要控制項中，並在內包含重複項控制項來列出每個客戶。 將中繼器名稱設定為**customersRepeater** ，如下列程式碼所示。

    在舊版的 Web form 中，使用資料系結來發出資料系結之物件的成員值時，您會使用資料系結運算式，以及對 Eval 方法的呼叫，以字串的形式傳入成員的名稱。

    在執行時間，這些 Eval 的呼叫將會針對目前系結的物件使用反映，以讀取具有給定名稱的成員值，並在 HTML 中顯示結果。 這種方法可讓您輕鬆地針對任意的 unshaped 資料進行資料系結。

    可惜的是，您在 Visual Studio 中遺失了許多絕佳的開發時間體驗功能，包括成員名稱的 IntelliSense、導覽的支援（例如 [移至定義]）和編譯時間檢查。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample1.aspx)]
3. 開啟**Customers.aspx.cs**檔案。
4. 新增下列 using 語句。

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample2.cs)]
5. 在 [ **\_載入**方法] 頁面中，新增程式碼，以客戶清單填入中繼器。

    （程式碼片段- *Web Forms 實驗室-Ex01-系結客戶資料來源*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample3.cs)]

    解決方案會搭配使用 EntityFramework 與 CodeFirst 來建立和存取資料庫。 在下列程式碼中，customersRepeater 系結至具體化查詢，它會傳回資料庫中的所有客戶。
6. 按**F5**執行解決方案並移至 [**客戶**] 頁面，以查看操作中的中繼器。 當解決方案使用 CodeFirst 時，在執行應用程式時，資料庫將會建立並填入您的本機 SQL Express 實例。

    ![使用中繼器列出客戶](whats-new-in-web-forms-in-aspnet-45/_static/image1.png "使用中繼器列出客戶")

    *使用中繼器列出客戶*

    > [!NOTE]
    > 在 Visual Studio 2012 中，IIS Express 是預設的 Web 開發伺服器。
7. 關閉瀏覽器，然後返回 Visual Studio。
8. 現在取代此實作為使用強型別系結。 開啟 [ **Customers** ] 頁面，並使用 [中繼器] 中的 [新增**ItemType** ] 屬性，將 [**客戶**類型] 設定為系結類型。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample4.aspx)]

    ItemType 屬性可讓您宣告控制項將要系結的資料類型，並可讓您在資料繫結控制項內使用強型別系結。
9. 將 ItemTemplate 內容取代為下列程式碼。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample5.aspx)]

    上述方法的其中一個缺點是，對 Eval （）和 Bind （）的呼叫是晚期繫結-這表示您會傳遞字串來代表屬性名稱。 這表示您不會取得成員名稱的 Intellisense、程式碼導覽的支援（例如 [移至定義]），也不會支援編譯時間檢查。

    設定 ItemType 屬性會導致在資料系結運算式的範圍中產生兩個新的類型變數： **Item**和**BindItem**。 您可以在資料系結運算式中使用這些強型別變數，並獲得 Visual Studio 開發經驗的完整優勢。

    運算式中使用的 &quot; **：** &quot; 會自動以 HTML 編碼輸出，以避免發生安全性問題（例如跨網站腳本攻擊）。 此標記法自 .NET 4 開始可供回應寫入，但現在也可用於資料系結運算式。

    > [!NOTE]
    > 專案成員適用于單向系結。 如果您想要執行雙向系結，請使用**BindItem**成員。

    ![強型別系結中的 IntelliSense 支援](whats-new-in-web-forms-in-aspnet-45/_static/image2.png "強型別系結中的 IntelliSense 支援")

    *強型別系結中的 IntelliSense 支援*
10. 按**F5**執行方案並移至 [客戶] 頁面，以確定變更如預期般運作。

    ![列出客戶詳細資料](whats-new-in-web-forms-in-aspnet-45/_static/image3.png "列出客戶詳細資料")

    *列出客戶詳細資料*
11. 關閉瀏覽器，然後返回 Visual Studio。

<a id="Task_2_-_Introducing_Model_Binding_in_Web_Forms"></a>
#### <a name="task-2---introducing-model-binding-in-web-forms"></a>工作 2-Web Forms 中的模型系結簡介

在舊版的 ASP.NET Web form 中，當您想要執行雙向資料系結時，若要同時抓取和更新資料，則需要使用資料來源物件。 這可能是物件資料來源、SQL 資料來源、LINQ 資料來源等等。 不過，如果您的案例需要自訂程式碼來處理資料，您需要使用物件資料來源，這樣會帶來一些缺點。 例如，您必須避免複雜類型，而且您需要在執行驗證邏輯時處理例外狀況。

在新版本的 ASP.NET Web Forms 中，資料繫結控制項支援模型系結。 這表示您可以直接在資料繫結控制項中指定 select、update、insert 和 delete 方法，以便從程式碼後置檔案或另一個類別呼叫邏輯。

若要瞭解這一點，您將使用 GridView，利用新的**SelectMethod**屬性來列出產品類別目錄。 這個屬性可讓您指定用來抓取 GridView 資料的方法。

1. 開啟 [ **default.aspx** ] 頁面，並加入**GridView**。 如下所示設定 GridView，以使用強型別系結並啟用排序和分頁。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample6.aspx)]
2. 使用新的**SelectMethod**屬性來設定 GridView，以呼叫**GetCategories**方法來選取資料。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample7.aspx)]
3. 開啟**Products.aspx.cs**程式碼後置檔案，並新增下列 using 語句。

    （程式碼片段- *Web Forms 實驗室-Ex01-命名空間*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample8.cs)]
4. 在**Products**類別中加入私用成員，並指派**ProductsCoNtext**的新實例。 這個屬性會儲存 Entity Framework 的資料內容，讓您可以連接到資料庫。

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample9.cs)]
5. 建立**GetCategories**方法，以使用 LINQ 抓取類別目錄清單。 此查詢將包含**products**屬性，讓 GridView 可以顯示每個類別目錄的產品數量。 請注意，方法會傳回原始 IQueryable 物件，代表要在稍後的頁面生命週期中執行的查詢。

    （程式碼片段- *Web Forms 實驗室-Ex01-GetCategories*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample10.cs)]

    > [!NOTE]
    > 在舊版的 ASP.NET Web Forms 中，使用您自己的存放庫邏輯在物件資料來源內容中啟用排序和分頁，需要撰寫您自己的自訂程式碼並接收所有必要的參數。 現在，當資料系結方法可以傳回 IQueryable，而這代表仍在執行的查詢時，ASP.NET 可以負責修改查詢，以加入適當的排序和分頁參數。
6. 按**F5**開始對網站進行調試，並移至 [產品] 頁面。 您應該會看到 GridView 已填入 GetCategories 方法所傳回的類別。

    ![使用模型系結填入 GridView](whats-new-in-web-forms-in-aspnet-45/_static/image4.png "使用模型系結填入 GridView")

    *使用模型系結填入 GridView*
7. 按**SHIFT**+**F5**停止調試。

<a id="Task_3_-_Value_Providers_in_Model_Binding"></a>
#### <a name="task-3---value-providers-in-model-binding"></a>工作 3-模型系結中的值提供者

模型系結不僅可讓您指定自訂方法，直接在資料繫結控制項中使用您的資料，還可讓您將頁面中的資料對應到這些方法中的參數。 在方法參數上，您可以使用值提供者屬性來指定值的資料來源。 例如:

- 頁面上的控制項
- 查詢字串值
- 檢視資料
- 工作階段狀態
- Cookie
- 張貼的表單資料
- 檢視狀態
- 也支援自訂值提供者

如果您已使用 ASP.NET MVC 4，您會注意到模型系結支援類似。 事實上，這些功能是從 ASP.NET MVC 取得，並移至**system.web**元件，以便在 web Forms 上使用。

在這項工作中，您將會更新 GridView，依據每個類別的產品數量來篩選其結果，並接收具有模型系結的篩選參數。

1. 回到 [ **default.aspx** ] 頁面。
2. 在 GridView 的頂端，新增**標籤**和**ComboBox**來選取每個類別的產品數目，如下所示。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample11.aspx)]
3. 將**EmptyDataTemplate**新增至 GridView，以在沒有所選產品數目的分類時顯示訊息。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample12.aspx)]
4. 開啟**Products.aspx.cs**程式碼後置，並新增下列 using 語句。

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample13.cs)]
5. 修改**GetCategories**方法，以接收整數**minProductsCount**引數並篩選傳回的結果。 若要這麼做，請將方法取代為下列程式碼。

    （程式碼片段- *Web Forms 實驗室-Ex01-GetCategories 2*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample14.cs)]

    **MinProductsCount**引數上的新 **[控制項]** 屬性，可讓 ASP.NET 知道其值必須使用頁面中的控制項填入。 ASP.NET 會尋找符合引數名稱（minProductsCount）的任何控制項，並執行必要的對應和轉換，以控制值來填入參數。

    或者，屬性會提供多載的函式，可讓您指定要從何處取得值的控制項。

    > [!NOTE]
    > 資料系結功能的其中一個目標是減少需要針對頁面互動所撰寫的程式碼數量。 除了 [控制] 值提供者之外，您還可以使用方法參數中的其他模型系結提供者。 其中有部分會列在 [工作簡介] 中。
6. 按**F5**開始對網站進行調試，並移至 [產品] 頁面。 在下拉式清單中選取一些產品，並注意 GridView 現在的更新方式。

    ![使用下拉式清單值篩選 GridView](whats-new-in-web-forms-in-aspnet-45/_static/image5.png "使用下拉式清單值篩選 GridView")

    *使用下拉式清單值篩選 GridView*
7. 停止偵錯。

<a id="Task_4_-_Using_Model_Binding_for_Filtering"></a>
#### <a name="task-4---using-model-binding-for-filtering"></a>工作 4-使用模型系結進行篩選

在這項工作中，您將新增第二個子 GridView，以顯示所選類別中的產品。

1. 開啟 [ **default.aspx** ] 頁面並更新 [類別] GridView，以自動產生 [選取] 按鈕。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample15.aspx)]
2. 在底部新增名為**productsGrid**的第二個**GridView** 。 將  **ItemType**  設定為  **WebFormsLab**、 **DataKeyNames**至  **ProductId**  和 要**GetProducts**的**SelectMethod** 。 將**AutoGenerateColumns**設定為**false** ，並新增 ProductId、ProductName、Description 和單價的資料行。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample16.aspx)]
3. 開啟**Products.aspx.cs**程式碼後置檔案。 執行**GetProducts**方法，以接收來自類別 GridView 的分類識別碼，並篩選產品。 模型系結會使用**categoriesGrid**中所選取的資料列來設定參數值。 由於引數名稱和控制項名稱不相符，因此您應該在控制項值提供者中指定控制項的名稱。

    （程式碼片段- *Web Forms 實驗室-Ex01-GetProducts*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample17.cs)]

    > [!NOTE]
    > 這種方法可讓您更輕鬆地對這些方法進行單元測試。 在未執行 Web form 的單元測試內容中，[Control] 屬性不會執行任何特定動作。
4. 開啟 [ **products** ] 頁面，然後找出 [Products] GridView。 更新產品 GridView 以顯示用來編輯所選產品的連結。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample18.aspx)]
5. 開啟**ProductDetails**程式碼後置，並以下列程式碼取代**SelectProduct**方法。

    （程式碼片段- *Web Forms 實驗室-Ex01-SelectProduct 方法*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample19.cs)]

    > [!NOTE]
    > 請注意， **[QueryString]** 屬性是用來在查詢字串中填入 productId 參數的方法參數。
6. 按**F5**開始對網站進行調試，並移至 [產品] 頁面。 從 [類別] GridView 選取任何類別，並注意 [產品] GridView 已更新。

    ![顯示所選類別中的產品](whats-new-in-web-forms-in-aspnet-45/_static/image6.png "顯示所選類別中的產品")

    *顯示所選類別中的產品*
7. 按一下產品上的 [ **View** ] 連結，以開啟 [ProductDetails] 頁面。

    請注意，此頁面會使用查詢字串中的 productId 參數來抓取具有 SelectMethod 的產品。

    ![查看產品詳細資料](whats-new-in-web-forms-in-aspnet-45/_static/image7.png "查看產品詳細資料")

    *查看產品詳細資料*

    > [!NOTE]
    > 在下一個練習中，將會執行輸入 HTML 描述的功能。

<a id="Task_5_-_Using_Model_Binding_for_Update_Operations"></a>
#### <a name="task-5---using-model-binding-for-update-operations"></a>工作 5-使用更新作業的模型系結

在上一個工作中，您已使用模型系結主要是用來選取資料，在這項工作中，您將瞭解如何在更新作業中使用模型系結。

您將會更新 [類別] GridView，讓使用者更新類別目錄。

1. 開啟 [ **default.aspx** ] 頁面並更新 [類別] GridView，以自動產生 [編輯] 按鈕，並使用新的**UpdateMethod**屬性來指定**UpdateCategory**方法，以更新選取的專案。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample20.aspx)]

    GridView 中的 DataKeyNames 屬性會定義哪些成員是唯一識別模型系結物件，因此是 update 方法至少應接收的參數。
2. 開啟**Products.aspx.cs**程式碼後置檔案，並執行**UpdateCategory**方法。 方法應該會收到分類識別碼以載入目前的分類、填入 GridView 中的值，然後更新類別目錄。

    （程式碼片段- *Web Forms 實驗室-Ex01-UpdateCategory*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample21.cs)]

    Page 類別中的新**TryUpdateModel**方法，會負責使用頁面控制項中的值填入模型物件。 在此情況下，它會將正在編輯的目前 GridView 資料列中的更新值，取代為**category**物件。

    > [!NOTE]
    > 下一個練習將說明 ModelState 的使用方式，以便在編輯物件時驗證使用者所輸入的資料。
3. 執行網站並移至 [產品] 頁面。 編輯分類。 輸入新的名稱，然後按一下 [**更新**] 以保存變更。

    ![編輯分類](whats-new-in-web-forms-in-aspnet-45/_static/image8.png "編輯分類")

    *編輯分類*

<a id="Exercise2"></a>

<a id="Exercise_2_Data_Validation"></a>
### <a name="exercise-2-data-validation"></a>練習2：資料驗證

在此練習中，您將瞭解 ASP.NET 4.5 中的新資料驗證功能。 您將會在 Web Forms 中查看新的不顯眼驗證功能。 您會在應用程式模型類別中使用資料批註來進行使用者輸入驗證，最後，您將瞭解如何開啟或關閉對頁面中個別控制項的要求驗證。

<a id="Task_1_-_Unobtrusive_Validation"></a>
#### <a name="task-1---unobtrusive-validation"></a>工作 1-不顯眼的驗證

具有複雜資料的表單（包括驗證程式）通常會在頁面中產生太多的 JavaScript 程式碼，這可能代表大約60% 的程式碼。 啟用不顯眼的驗證之後，您的 HTML 程式碼看起來會更清楚，而且整齊。

在本節中，您將在 ASP.NET 中啟用不顯眼的驗證，以比較這兩個設定所產生的 HTML 程式碼。

1. 開啟**Visual Studio 2012** ，然後開啟位於此實驗室的**Source\Ex2-Validation\Begin**資料夾中的 [**開始**] 解決方案。 或者，您可以繼續使用上一個練習中的現有解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這麼做，請在 方案總管中，按一下  **WebFormsLab**專案 **管理 NuGet 套件**。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
2. 按**F5**啟動 web 應用程式。 移至 [客戶] 頁面，然後按一下 [**加入新的客戶**] 連結。
3. 以滑鼠右鍵按一下 [瀏覽器] 頁面，然後選取 [ **View Source** ] 選項以開啟應用程式所產生的 HTML 程式碼。

    ![顯示網頁 HTML 程式碼](whats-new-in-web-forms-in-aspnet-45/_static/image9.png "顯示網頁 HTML 程式碼")

    *顯示網頁 HTML 程式碼*
4. 請流覽頁面原始碼，並注意 ASP.NET 已在頁面中插入 JavaScript 程式碼和資料驗證器來執行驗證，並顯示錯誤清單。

    ![CustomerDetails 頁面中的驗證 JavaScript 程式碼](whats-new-in-web-forms-in-aspnet-45/_static/image10.png "CustomerDetails 頁面中的驗證 JavaScript 程式碼")

    *CustomerDetails 頁面中的驗證 JavaScript 程式碼*
5. 關閉瀏覽器，然後返回 Visual Studio。
6. 現在您將啟用不顯眼的驗證。 開啟**web.config** ，並在**AppSettings**區段中找出**ValidationSettings： UnobtrusiveValidationMode**金鑰 **。** 將 [金鑰] 值設定為 [ **WebForms**]。

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample22.xml)]

    > [!NOTE]
    > 您也可以在 [&quot;] 頁面中設定此屬性 **\_載入**&quot; 事件，以防您只想要針對某些網頁啟用不顯眼的驗證。
7. 開啟**CustomerDetails** ，然後按**F5**啟動 Web 應用程式。
8. 按 F12 鍵以開啟 IE 開發人員工具。 開發人員工具開啟之後，請選取 [腳本] 索引標籤。從功能表中選取 [ **CustomerDetails** ]，並記下在頁面上執行 jQuery 所需的腳本已從本機網站載入瀏覽器中。

    ![直接從本機 IIS 伺服器載入 jQuery JavaScript 檔案](whats-new-in-web-forms-in-aspnet-45/_static/image11.png "直接從本機 IIS 伺服器載入 jQuery JavaScript 檔案")

    *直接從本機 IIS 伺服器載入 jQuery JavaScript 檔案*
9. 關閉瀏覽器以返回 Visual Studio。 再次開啟**網站. Master**檔案，然後找出**ScriptManager**。 新增屬性**EnableCdn**屬性，其值**為 True**。 這會強制從線上 URL 載入 jQuery，而不是從本機網站的 URL。
10. 在 Visual Studio 中開啟**CustomerDetails** 。 按 F5 鍵以執行網站。 Internet Explorer 開啟後，按 F12 鍵以開啟開發人員工具。 選取 [**腳本**] 索引標籤，然後查看下拉式清單。 請注意，jQuery JavaScript 檔案不會再從本機網站載入，而是從線上 jQuery CDN。

    ![從 CDN 載入 jQuery JavaScript 檔案](whats-new-in-web-forms-in-aspnet-45/_static/image12.png "從 CDN 載入 jQuery JavaScript 檔案")

    *從 CDN 載入 jQuery JavaScript 檔案*
11. 使用瀏覽器中的 [視圖來源] 選項，再次開啟 HTML 網頁原始程式碼。 請注意，藉由啟用不顯眼的驗證 ASP.NET，已將插入的 JavaScript 程式碼取代為數據 \*屬性。

    ![不顯眼的驗證程式代碼](whats-new-in-web-forms-in-aspnet-45/_static/image13.png "不顯眼的驗證程式代碼")

    *不顯眼的驗證程式代碼*

    > [!NOTE]
    > 在此範例中，您已瞭解如何將含有資料批註的驗證摘要簡化成隻有幾個 HTML 和 JavaScript 行。 在過去，如果沒有不顯眼的驗證，您新增的驗證控制項越多，您的 JavaScript 驗證程式代碼就會變大。

<a id="Task_2_-_Validating_the_Model_with_Data_Annotations"></a>
#### <a name="task-2---validating-the-model-with-data-annotations"></a>工作 2-使用資料批註來驗證模型

ASP.NET 4.5 引進 Web Forms 的資料批註驗證。 您現在可以在模型類別中定義條件約束，並在您的所有 web 應用程式中使用它們，而不需要在每個輸入上都有驗證控制項。 在本節中，您將瞭解如何使用資料批註來驗證新的/編輯客戶表單。

1. 開啟 [ **CustomerDetail** ] 頁面。 請注意， **EditItemTemplate**和**InsertItemTemplate**區段中的客戶名字和第二個名稱會使用 RequiredFieldValidator 控制項進行驗證。 每個驗證程式都會與特定的條件相關聯，因此您需要包含多個驗證器做為要檢查的條件。
2. 加入資料批註以驗證客戶模型類別。 在 [**模型**] 資料夾中開啟**Customer.cs**類別，並使用資料批註屬性來*裝飾*每個屬性。

    （程式碼片段- *Web Forms 實驗室-Ex02-資料批註*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample23.cs)]

    > [!NOTE]
    > .NET Framework 4.5 已擴充現有的資料批註集合。 以下是您可以使用的一些資料批註： [CreditCard]、[Phone]、[EmailAddress]、[Range]、[Compare]、[Url]、[Microsoft.extensions.configuration fileextensions]、[Required]、 [Key]、[RegularExpression]。
    > 
    > 一些使用範例：
    > 
    > [Key]: Specifies that an attribute is the unique identifier
    > 
    > [Range(0.4, 0.5, ErrorMessage=&quot;{Write an error message}&quot;]: Double range
    > 
    > [EmailAddress(ErrorMessage=&quot;Invalid Email&quot;), MaxLength(56)]: Two annotations in the same line.
    > 
    > 您也可以在每個屬性內定義自己的錯誤訊息。
3. 開啟**CustomerDetails** ，並移除 FormView 控制項的 EditItemTemplate 和 InsertItemTemplate 區段中，第一個和最後一個名稱欄位的所有 RequiredFieldValidators。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample24.aspx)]

    > [!NOTE]
    > 使用資料批註的其中一個優點是，應用程式頁面中的驗證邏輯不會重複。 您可以在模型中定義一次，並在運算元據的所有應用程式頁面上使用它。
4. 開啟**CustomerDetails**程式碼後置，並找出 SaveCustomer 方法。 當插入新客戶並從 FormView 控制項值接收 Customer 參數時，會呼叫這個方法。 當頁面控制項與參數物件之間的對應發生時，ASP.NET 將會針對所有資料批註屬性執行模型驗證，並在發生錯誤時填入 ModelState 字典（如果有的話）。

    只有在執行驗證之後，您的模型上的所有欄位都有效時，ModelState 才會傳回 true。

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample25.cs)]
5. 在 CustomerDetails 頁面結尾處新增**ValidationSummary**控制項，以顯示模型錯誤清單。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample26.aspx)]

    **ShowModelStateErrors**是 ValidationSummary 控制項上的新屬性，當設定為**true**時，控制項就會顯示來自 ModelState 字典的錯誤。 這些錯誤來自資料批註驗證。
6. 按**F5**執行 Web 應用程式。 以一些錯誤值完成表單，然後按一下 [**儲存**] 以執行驗證。 請注意底部的錯誤摘要。

    ![使用資料批註進行驗證](whats-new-in-web-forms-in-aspnet-45/_static/image14.png "使用資料批註進行驗證")

    *使用資料批註進行驗證*

<a id="Task_3_-_Handling_Custom_Database_Errors_with_ModelState"></a>
#### <a name="task-3---handling-custom-database-errors-with-modelstate"></a>工作 3-處理 ModelState 的自訂資料庫錯誤

在舊版的 Web form 中，處理資料庫錯誤（例如太長的字串或唯一的索引鍵違規）可能牽涉到在您的存放庫程式碼中擲回例外狀況，然後在程式碼後置中處理例外狀況以顯示錯誤。 需要大量的程式碼才能執行相當簡單的作業。

在 Web form 4.5 中，ModelState 物件可以用來以一致的方式，從您的模型或從資料庫顯示頁面上的錯誤。

在這項工作中，您將新增程式碼來適當處理資料庫例外狀況，並使用 ModelState 物件向使用者顯示適當的訊息。

1. 當應用程式仍在執行時，請嘗試使用重複的值來更新類別目錄的名稱。

    ![以重複的名稱更新分類](whats-new-in-web-forms-in-aspnet-45/_static/image15.png "以重複的名稱更新分類")

    *以重複的名稱更新分類*

    請注意，由於 [**類別名稱**] 資料行的 &quot;唯一&quot; 條件約束，而擲回例外狀況。

    ![重複類別名稱的例外狀況](whats-new-in-web-forms-in-aspnet-45/_static/image16.png "重複類別名稱的例外狀況")

    *重複類別名稱的例外狀況*
2. 停止偵錯。 在**Products.aspx.cs**程式碼後置檔案中，更新**UpdateCategory**方法，以處理 db 所擲回的例外狀況。SaveChanges （）方法呼叫，並將錯誤新增至**ModelState**物件。

    新的**TryUpdateModel**方法會使用使用者所提供的表單資料，來更新從資料庫中抓取的分類物件。

    （程式碼片段- *Web Forms 實驗室-Ex02-UpdateCategory 處理錯誤*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample27.cs)]

    > [!NOTE]
    > 在理想的情況下，您必須找出就 dbupdateexception 的原因，並檢查根本原因是否違反唯一索引鍵條件約束。
3. 開啟 [ **default.aspx** ]，然後在 [類別] GridView 底下新增**ValidationSummary**控制項，以顯示模型錯誤清單。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample28.aspx)]
4. 執行網站並移至 [產品] 頁面。 嘗試使用重複的值來更新類別目錄的名稱。

    請注意，例外狀況已處理，且錯誤訊息會出現在**ValidationSummary**控制項中。

    ![重複的類別錯誤](whats-new-in-web-forms-in-aspnet-45/_static/image17.png "重複的類別錯誤")

    *重複的類別錯誤*

<a id="Task_4_-_Request_Validation_in_ASPNET_Web_Forms_45"></a>
#### <a name="task-4---request-validation-in-aspnet-web-forms-45"></a>工作 4-在 ASP.NET Web Forms 4.5 中要求驗證

ASP.NET 中的要求驗證功能會針對跨網站腳本（XSS）攻擊提供特定層級的預設保護。 在舊版的 ASP.NET 中，預設會啟用要求驗證，而且只能針對整個頁面停用。 使用新版的 ASP.NET Web form 時，您現在可以停用單一控制項的要求驗證、執行延遲要求驗證或存取未驗證的要求資料（如果您這麼做，請務必小心！）。

1. 按**Ctrl + F5**以啟動網站而不進行偵測，並移至 [產品] 頁面。 選取類別，然後按一下任何產品上的 [**編輯**] 連結。
2. 輸入包含潛在危險內容的描述，例如包括 HTML 標籤。 請注意因要求驗證而擲回的例外狀況。

    ![編輯具有潛在危險內容的產品](whats-new-in-web-forms-in-aspnet-45/_static/image18.png "編輯具有潛在危險內容的產品")

    *編輯具有潛在危險內容的產品*

    ![因要求驗證而擲回的例外狀況](whats-new-in-web-forms-in-aspnet-45/_static/image19.png "因要求驗證而擲回的例外狀況")

    *因要求驗證而擲回的例外狀況*
3. 關閉頁面，然後在 Visual Studio 中，按**SHIFT + F5**停止調試。
4. 開啟 [ **ProductDetails** ] 頁面，並找出 [**描述**] 文字方塊。
5. 將新的 [ **ValidateRequestMode** ] 屬性加入文字方塊中，並將其值設定為 [**停用**]。

    新的**ValidateRequestMode**屬性可讓您停用每個控制項的要求驗證。 當您想要使用可能接收 HTML 程式碼的輸入，但想要讓驗證在頁面的其餘部分保持運作時，這會很有用。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample29.aspx)]
6. 按**F5**執行 web 應用程式。 再次開啟 [編輯產品] 頁面，並完成包含 HTML 標籤的產品描述。 請注意，您現在可以將 HTML 內容新增至描述。

    ![已停用產品描述的要求驗證](whats-new-in-web-forms-in-aspnet-45/_static/image20.png "已停用產品描述的要求驗證")

    *已停用產品描述的要求驗證*

    > [!NOTE]
    > 在生產應用程式中，您應該淨化使用者輸入的 HTML 代碼，以確保只輸入安全的 HTML 標籤（例如，沒有 &lt;腳本&gt; 標記）。 若要這樣做，您可以使用[Microsoft Web 保護程式庫](https://www.nuget.org/packages/AntiXSS)。
7. 再次編輯產品。 在 [名稱] 欄位中輸入 HTML 程式碼，然後按一下 [**儲存**]。 請注意，[描述] 欄位只會停用 [要求驗證]，其餘欄位仍然會針對潛在危險的內容進行驗證。

    ![其他欄位中已啟用要求驗證](whats-new-in-web-forms-in-aspnet-45/_static/image21.png "其他欄位中已啟用要求驗證")

    *其他欄位中已啟用要求驗證*

    ASP.NET Web Forms 4.5 包含新的要求驗證模式，以順延強制要求驗證。 當要求驗證模式設定為**4.5**時，如果程式碼部分存取*要求。表單 [&quot;金鑰&quot;]* ，ASP.NET 4.5 的要求驗證只會針對表單集合中的特定元素觸發要求驗證。

    此外，ASP.NET 4.5 現在包含來自 Microsoft 防 XSS 程式庫 v4.0 的核心編碼常式。 反 XSS 編碼常式是由新的**AntiXss**命名空間中的新*AntiXssEncoder*類型所執行。 當**encoderType**參數設定為使用*AntiXssEncoder*時，ASP.NET 內的所有輸出編碼都會自動使用新的編碼常式。
8. ASP.NET 4.5 要求驗證也支援對要求資料進行未經驗證的存取。 ASP.NET 4.5 會將新的集合屬性新增至名為**未驗證**的**HttpRequest**物件。 當您流覽至**HttpRequest**時，您可以存取所有常見的要求資料片段，包括表單、QueryStrings、Cookie、url 等等。

    ![未驗證物件](whats-new-in-web-forms-in-aspnet-45/_static/image22.png "未驗證物件")

    *未驗證物件*

    > [!NOTE]
    > **請小心使用 HttpRequest. 未驗證屬性！** 請確定您仔細對原始要求資料執行自訂驗證，以確保危險的文字不會被往返，並會轉譯回不適合的客戶！

<a id="Exercise3"></a>

<a id="Exercise_3_Asynchronous_Page_Processing_in_ASPNET_Web_Forms"></a>
### <a name="exercise-3-asynchronous-page-processing-in-aspnet-web-forms"></a>練習3： ASP.NET Web Forms 中的非同步網頁處理

在此練習中，您將會在 ASP.NET Web form 中引進新的非同步頁面處理功能。

<a id="Task_1_-_Updating_the_Product_Details_Page_to_Upload_and_Show_Images"></a>
#### <a name="task-1---updating-the-product-details-page-to-upload-and-show-images"></a>工作 1-更新產品詳細資料頁面，以上傳和顯示影像

在這項工作中，您將更新 [產品詳細資料] 頁面，讓使用者指定產品的影像 URL，並將它顯示在唯讀的視圖中。 您將會以同步方式下載指定的映射，以建立其本機複本。 在下一項工作中，您將更新此執行，使其以非同步方式執行。

1. 開啟**Visual Studio 2012** ，並從這個實驗室的資料夾載入位於**Source\Ex3-Async\Begin**的**開始**解決方案。 或者，您可以從先前的練習繼續處理現有的解決方案。

   1. 如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。 若要這樣做，請在 方案總管中，按一下  **WebFormsLab**  專案，然後選取 **管理 NuGet 套件**。
   2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。
   3. 最後，按一下 [**組建**] | [**組建方案**] 來建立方案。

      > [!NOTE]
      > 使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。 使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。 這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。
2. 開啟 [ **ProductDetails** ] 頁面來源，並在 FormView 的 ItemTemplate 中加入欄位以顯示產品影像。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample30.aspx)]
3. 新增欄位以指定 FormView 的 EditTemplate 中的影像 URL。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample31.aspx)]
4. 開啟**ProductDetails.aspx.cs**程式碼後置檔案，並新增下列命名空間指示詞。

    （程式碼片段- *Web Forms 實驗室-Ex03-命名空間*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample32.cs)]
5. 建立**UpdateProductImage**方法，以將遠端影像儲存在 [本機**映射**] 資料夾中，並使用新的 [影像位置] 值來更新 product 實體。

    （程式碼片段- *Web Forms 實驗室-Ex03-UpdateProductImage*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample33.cs)]
6. 更新**UpdateProduct**方法以呼叫**UpdateProductImage**方法。

    （程式碼片段- *Web Forms 實驗室-Ex03-UpdateProductImage 呼叫*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample34.cs)]
7. 執行應用程式，並嘗試上傳產品的影像。 例如，您可以從 Office 美工圖案使用下列影像 URL： [ [http://officeimg.vo.msecnd.net/images/MB900437099.jpg](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)

    ![設定產品的影像](whats-new-in-web-forms-in-aspnet-45/_static/image23.png "設定產品的影像")

    *設定產品的影像*

<a id="Task_2_-_Adding_Asynchronous_Processing_to_the_Product_Details_Page"></a>
#### <a name="task-2---adding-asynchronous-processing-to-the-product-details-page"></a>工作 2-將非同步處理新增至產品詳細資料頁面

在這項工作中，您將更新 [產品詳細資料] 頁面，使其以非同步方式執行。 您將會藉由使用 ASP.NET 4.5 非同步頁面處理，來增強長時間執行的工作，也就是影像下載程式。

Web 應用程式中的非同步方法可以用來優化 ASP.NET 執行緒集區的使用方式。 在 ASP.NET 中，執行緒集區中的執行緒數目有限，可用於出席要求，因此，當所有線程都忙碌時，ASP.NET 會開始拒絕新的要求、傳送應用程式錯誤訊息，並讓您的網站無法使用。

網站上耗時的作業是非同步程式設計的絕佳候選項目，因為它們會佔用指派的執行緒很長一段時間。 這包括長時間執行的要求、有許多不同元素和頁面的頁面需要離線作業，例如查詢資料庫或存取外部 web 伺服器。 其優點是，如果您對這些作業使用非同步方法，當頁面正在處理時，執行緒就會釋出並傳回到執行緒集區，並可用於參與新的頁面要求。 這表示，此頁面會從執行緒集區的一個執行緒開始處理，而且可能會在非同步處理完成之後，在另一個執行緒中完成處理。

1. 開啟 [ **ProductDetails** ] 頁面。 在**Page**元素中新增**Async**屬性，並將它設定為**true**。 這個屬性會告知 ASP.NET，以執行 IHttpAsyncHandler 介面。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample35.aspx)]
2. 在頁面底部新增標籤，以顯示執行頁面之執行緒的詳細資料。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample36.aspx)]
3. 開啟**ProductDetails.aspx.cs** ，並新增下列命名空間指示詞。

    （程式碼片段- *Web Forms 實驗室-Ex03-命名空間 2*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample37.cs)]
4. 修改**UpdateProductImage**方法以下載包含非同步工作的映射。 您將使用**DownloadFileTaskAsync**方法來取代**WebClient** **DownloadFile**方法，並包含**await**關鍵字。

    （程式碼片段- *Web Forms 實驗室-Ex03-UpdateProductImage Async*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample38.cs)]

    RegisterAsyncTask 會註冊新的頁面非同步工作，以在不同的執行緒中執行。 它會接收包含要執行之工作（t）的 lambda 運算式。 **DownloadFileTaskAsync**方法中的**await**關鍵字會將方法的其餘部分，轉換為在**DownloadFileTaskAsync**方法完成後以非同步方式叫用的回呼。 ASP.NET 會自動維護所有 HTTP 要求的原始值，以繼續執行方法。 .NET 4.5 中新的非同步程式設計模型可讓您撰寫看起來非常類似同步程式碼的非同步程式碼，並讓編譯器處理回呼函式或接續程式碼的複雜程度。
    > [!NOTE]
    > 自 .NET 2.0 開始已提供 RegisterAsyncTask 和 PageAsyncTask。 Await 關鍵字是 .NET 4.5 非同步程式設計模型的新方法，可以與 .NET WebClient 物件中的新 TaskAsync 方法搭配使用。
5. 加入程式碼，以顯示程式碼開始和完成執行所在的執行緒。 若要這麼做，請使用下列程式碼更新**UpdateProductImage**方法。

    （程式碼片段- *Web Forms 實驗室-Ex03-顯示執行緒*）

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample39.cs)]
6. 開啟網站的**web.config**檔案。 新增下列 appSetting 變數。

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample40.xml)]
7. 按**F5**執行應用程式，並上傳產品的影像。 請注意，程式碼開始和完成的執行緒識別碼可能不同。 這是因為非同步工作會在與 ASP.NET 執行緒集區不同的執行緒上執行。 當工作完成時，ASP.NET 會將工作放回佇列中，並指派任何可用的執行緒。

    ![非同步下載影像](whats-new-in-web-forms-in-aspnet-45/_static/image24.png "非同步下載影像")

    *非同步下載影像*

> [!NOTE]
> 此外，您可以遵循[附錄 B：使用 Web Deploy 發佈 ASP.NET MVC 4 應用程式](#AppendixB)，將此應用程式部署至 Azure。

---

<a id="Summary"></a>
## <a name="summary"></a>總結

在這個實際操作的實驗室中，已解決並示範下列概念：

- 使用強型別資料系結運算式
- 在 Web Forms 中使用新的模型系結功能
- 使用值提供者將頁面資料對應至程式碼後置方法
- 使用資料批註進行使用者輸入驗證
- 利用 Web Forms 中 jQuery 的不顯眼用戶端驗證
- 執行細微的要求驗證
- 在 Web Forms 中執行非同步網頁處理

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附錄 A：安裝 Web 的 Visual Studio Express 2012

您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。 下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。

1. 移至[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。 或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Azure SDK&quot;搜尋產品 &quot;<em>Visual Studio Express 2012 For Web</em> 。
2. 按一下 [**立即安裝**]。 如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。
3. 開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。

    ![安裝 Visual Studio Express](whats-new-in-web-forms-in-aspnet-45/_static/image25.png "安裝 Visual Studio Express")

    *安裝 Visual Studio Express*
4. 閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。

    ![接受授權條款](whats-new-in-web-forms-in-aspnet-45/_static/image26.png)

    *接受授權條款*
5. 等到下載和安裝程式完成為止。

    ![安裝進度](whats-new-in-web-forms-in-aspnet-45/_static/image27.png)

    *安裝進度*
6. 當安裝完成時，按一下 **[完成]** 。

    ![安裝已完成](whats-new-in-web-forms-in-aspnet-45/_static/image28.png)

    *安裝已完成*
7. 按一下 **[** 結束] 以關閉 Web Platform Installer。
8. 若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。

    ![VS Express for Web 磚](whats-new-in-web-forms-in-aspnet-45/_static/image29.png)

    *VS Express for Web 磚*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>附錄 B：使用 Web Deploy 發行 ASP.NET MVC 4 應用程式

本附錄將說明如何從 Azure 入口網站建立新的網站，併發布您在實驗室之後取得的應用程式，利用 Azure 所提供的 Web Deploy 發佈功能。

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a>工作 1-從 Azure 入口網站建立新的網站

1. 移至[Azure 管理入口網站](https://manage.windowsazure.com/)並使用與您的訂用帳戶相關聯的 Microsoft 認證登入。

    > [!NOTE]
    > 有了 Azure，您可以免費裝載10個 ASP.NET 網站，然後隨著流量成長而調整。 您可以在[這裡](https://aka.ms/aspnet-hol-azure)註冊。

    ![登入 Windows Azure 入口網站](whats-new-in-web-forms-in-aspnet-45/_static/image30.png "登入 Windows Azure 入口網站")

    *登入入口網站*
2. 按一下命令列上的 [**新增**]。

    ![建立新網站](whats-new-in-web-forms-in-aspnet-45/_static/image31.png "建立新網站")

    *建立新網站*
3. 按一下 [**計算** | 的**網站**]。 然後選取 [**快速建立**] 選項。 提供新網站的可用 URL，然後按一下 [**建立網站**]。

    > [!NOTE]
    > Azure 是在雲端中執行之 web 應用程式的主機，您可以控制和管理。 [快速建立] 選項可讓您從入口網站外部，將已完成的 web 應用程式部署至 Azure。 它不包含設定資料庫的步驟。

    ![使用 [快速建立] 建立新的網站](whats-new-in-web-forms-in-aspnet-45/_static/image32.png "使用 [快速建立] 建立新的網站")

    *使用 [快速建立] 建立新的網站*
4. 等到新**網站**建立完畢。
5. 建立網站之後，請按一下 [ **URL** ] 資料行下方的連結。 檢查新網站是否正常運作。

    ![流覽至新網站](whats-new-in-web-forms-in-aspnet-45/_static/image33.png "流覽至新網站")

    *流覽至新網站*

    ![網站正在執行](whats-new-in-web-forms-in-aspnet-45/_static/image34.png "網站正在執行")

    *網站正在執行*
6. 返回入口網站，然後按一下 [**名稱**] 欄底下的網站名稱，以顯示管理頁面。

    ![開啟網站管理頁面](whats-new-in-web-forms-in-aspnet-45/_static/image35.png "開啟網站管理頁面")

    *開啟網站管理頁面*
7. 在 [**儀表板**] 頁面的 [**快速概覽**] 區段下，按一下 [**下載發行設定檔**] 連結。

    > [!NOTE]
    > *發行設定檔*包含將 web 應用程式發佈到 Azure 所需的所有資訊，以供每個已啟用的發行方法使用。 發行設定檔包含 URL、使用者認證和資料庫字串，這些都是用來連接到已啟用發行方法的每個端點並進行驗證的必要資訊。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支援讀取發行設定檔，以將這些程式的設定自動化，以將 Web 應用程式發行至 Azure。

    ![正在下載網站發行設定檔](whats-new-in-web-forms-in-aspnet-45/_static/image36.png "正在下載網站發行設定檔")

    *正在下載網站發行設定檔*
8. 將發行設定檔下載到已知的位置。 在此練習中，您將瞭解如何使用此檔案，將 web 應用程式從 Visual Studio 發行至 Azure。

    ![儲存發行設定檔](whats-new-in-web-forms-in-aspnet-45/_static/image37.png "正在儲存發行設定檔")

    *儲存發行設定檔*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>工作 2-設定資料庫伺服器

如果您的應用程式會使用 SQL Server 資料庫，您必須建立 SQL Database 伺服器。 如果您想要部署不使用 SQL Server 的簡單應用程式，您可能會略過這項工作。

1. 您將需要 SQL Database 伺服器來儲存應用程式資料庫。 您可以在 Azure 管理入口網站的  **SQL 資料庫** | **伺服器** | **伺服器的儀表板**上，從您的訂用帳戶中查看 SQL Database 伺服器。 如果您沒有建立伺服器，可以使用命令列上的 [**新增**] 按鈕建立一個。 記下 [**伺服器名稱] 和 [URL]、[系統管理員登入名稱] 和 [密碼**]，因為您將在後續工作中使用它們。 請不要建立資料庫，因為它會在稍後的階段中建立。

    ![SQL Database Server 儀表板](whats-new-in-web-forms-in-aspnet-45/_static/image38.png "SQL Database Server 儀表板")

    *SQL Database Server 儀表板*
2. 在下一項工作中，您將會從 Visual Studio 測試資料庫連線，因此您必須在伺服器的**允許 IP 位址**清單中包含本機 IP 位址。 若要這麼做，請按一下 **設定**，從**目前的用戶端 IP 位址**中選取 IP 位址，並將它貼入 [**起始 Ip 位址**] 和 [**結束 ip 位址**] 文字方塊，然後按一下 ![新增-用戶端-IP-位址-確定 按鈕](whats-new-in-web-forms-in-aspnet-45/_static/image39.png) 按鈕。

    ![正在新增用戶端 IP 位址](whats-new-in-web-forms-in-aspnet-45/_static/image40.png)

    *正在新增用戶端 IP 位址*
3. 將**用戶端 Ip 位址**新增至 [允許的 ip 位址] 清單之後，按一下 [**儲存**] 以確認變更。

    ![確認變更](whats-new-in-web-forms-in-aspnet-45/_static/image41.png)

    *確認變更*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>工作 3-使用 Web Deploy 發行 ASP.NET MVC 4 應用程式

1. 返回 ASP.NET MVC 4 解決方案。 在 **方案總管**中，以滑鼠右鍵按一下 網站 專案，然後選取 **發佈**。

    ![發行應用程式](whats-new-in-web-forms-in-aspnet-45/_static/image42.png "發行應用程式")

    *發行網站*
2. 匯入您在第一個工作中儲存的發行設定檔。

    ![匯入發行設定檔](whats-new-in-web-forms-in-aspnet-45/_static/image43.png "匯入發行設定檔")

    *正在匯入發行設定檔*
3. 按一下 [**驗證連接**]。 驗證完成後，按 **[下一步]** 。

    > [!NOTE]
    > 當您看到 [驗證連線] 按鈕旁出現綠色核取記號時，驗證就會完成。

    ![正在驗證連接](whats-new-in-web-forms-in-aspnet-45/_static/image44.png "正在驗證連接")

    *正在驗證連接*
4. 在 [**設定**] 頁面的 [**資料庫**] 區段底下，按一下資料庫連接的文字方塊旁邊的按鈕（也就是**DefaultConnection**）。

    ![Web deploy 設定](whats-new-in-web-forms-in-aspnet-45/_static/image45.png "Web deploy 設定")

    *Web deploy 設定*
5. 設定資料庫連接，如下所示：

   - 在 [**伺服器名稱**] 中，使用*tcp：* prefix 輸入您的 SQL Database 伺服器 URL。
   - 在 [**使用者名稱**] 中，輸入您的伺服器管理員登入名稱。
   - 在 [**密碼**] 中輸入您的伺服器管理員登入密碼。
   - 輸入新的資料庫名稱。

     ![正在設定目的地連接字串](whats-new-in-web-forms-in-aspnet-45/_static/image46.png "正在設定目的地連接字串")

     *正在設定目的地連接字串*
6. 然後按一下 [確定]。 當系統提示您建立資料庫時，請按一下 **[是]** 。

    ![建立資料庫](whats-new-in-web-forms-in-aspnet-45/_static/image47.png "建立資料庫字串")

    *建立資料庫*
7. 您將用來連線到 Azure 中 SQL Database 的連接字串會顯示在 [預設連接] 文字方塊中。 然後按一下 [下一步]。

    ![指向 SQL Database 的連接字串](whats-new-in-web-forms-in-aspnet-45/_static/image48.png "指向 SQL Database 的連接字串")

    *指向 SQL Database 的連接字串*
8. 在 [**預覽**] 頁面中，按一下 [**發佈**]。

    ![發行 web 應用程式](whats-new-in-web-forms-in-aspnet-45/_static/image49.png "發行 web 應用程式")

    *發行 web 應用程式*
9. 發佈程式完成後，您的預設瀏覽器會開啟已發行的網站。

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>附錄 C：使用程式碼片段

有了程式碼片段，您就可以輕鬆地擁有所需的所有程式碼。 實驗室檔會告訴您可以使用它們的確切時機，如下圖所示。

![使用 Visual Studio 程式碼片段將程式碼插入您的專案](whats-new-in-web-forms-in-aspnet-45/_static/image50.png "使用 Visual Studio 程式碼片段將程式碼插入您的專案")

*使用 Visual Studio 程式碼片段將程式碼插入您的專案*

***若要使用鍵盤新增程式碼片段（C#僅限）***

1. 將游標放在您想要插入程式碼的位置。
2. 開始鍵入程式碼片段名稱（不含空格或連字號）。
3. 監看 IntelliSense 會顯示相符的程式碼片段名稱。
4. 選取正確的程式碼片段（或繼續輸入，直到選取整個程式碼片段的名稱為止）。
5. 按兩次 Tab 鍵，在游標位置插入程式碼片段。

![開始鍵入程式碼片段名稱](whats-new-in-web-forms-in-aspnet-45/_static/image51.png "開始鍵入程式碼片段名稱")

*開始鍵入程式碼片段名稱*

![按 Tab 鍵以選取反白顯示的程式碼片段](whats-new-in-web-forms-in-aspnet-45/_static/image52.png "按 Tab 鍵以選取反白顯示的程式碼片段")

*按 Tab 鍵以選取反白顯示的程式碼片段*

![再按一次 Tab 鍵，將會展開程式碼片段](whats-new-in-web-forms-in-aspnet-45/_static/image53.png "再按一次 Tab 鍵，將會展開程式碼片段")

*再按一次 Tab 鍵，將會展開程式碼片段*

***若要使用滑鼠C#（、Visual Basic 和 XML）加入程式碼片段***sha-1. 以滑鼠右鍵按一下您要插入程式碼片段的位置。

1. 選取 [**插入程式碼片段**]，後面接著 [ **My Code 程式碼片段**]。
2. 按一下清單中的相關程式碼片段，即可加以選取。

![以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]](whats-new-in-web-forms-in-aspnet-45/_static/image54.png "以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]")

*以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]*

![按一下清單中的相關程式碼片段，即可加以選取](whats-new-in-web-forms-in-aspnet-45/_static/image55.png "按一下清單中的相關程式碼片段，即可加以選取")

*按一下清單中的相關程式碼片段，即可加以選取*
