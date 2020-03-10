---
uid: visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
title: 實習實驗室：一個 ASP.NET：整合 ASP.NET Web Forms、MVC 和 Web API |Microsoft Docs
author: rick-anderson
description: ASP.NET 是一種架構，可讓您使用 MVC、Web API 等特殊技術來建立網站、應用程式和服務。 擴充 ASP.NET h 。
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 4fe2558d-67cc-4d12-a5c1-6fb9f6f16137
msc.legacyurl: /visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
msc.type: authoredcontent
ms.openlocfilehash: 165d104b5d3ef3281af449cc8673ad96f531d628
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623197"
---
# <a name="hands-on-lab-one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api"></a>實習實驗室：一 ASP.NET：整合 ASP.NET Web Forms、MVC 和 Web API

依[Web Camp 團隊](https://twitter.com/webcamps)

[下載 Web Camp 訓練套件](https://aka.ms/webcamps-training-kit)

> ASP.NET 是一種架構，可讓您使用 MVC、Web API 等特殊技術來建立網站、應用程式和服務。 隨著擴充 ASP.NET 的建立和表示需要整合這些技術，最近致力於進行**一項 ASP.NET**。
> 
> Visual Studio 2013 引進了新的整合專案系統，可讓您建立應用程式，並在一個專案中使用所有 ASP.NET 技術。 這項功能可讓您不需要在專案開始時挑選一項技術，而是要鼓勵在一個專案中使用多個 ASP.NET 架構。
> 
> 所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)取得。

<a id="Overview"></a>
## <a name="overview"></a>概觀

<a id="Objectives"></a>
### <a name="objectives"></a>目標

在此實際操作實驗室中，您將瞭解如何：

- 根據**一個 ASP.NET**專案類型建立網站
- 在相同專案中使用不同的**ASP.NET**架構，例如**MVC**和**Web API**
- 識別**ASP.NET**應用程式的主要元件
- 利用**ASP.NET**的框架架構，自動建立控制器和視圖，以根據您的模型類別來執行 CRUD 作業
- 使用適用于每個工作的適當工具，公開電腦和人類可讀格式的同一組資訊

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Prerequisites

若要完成此實際操作實驗室，需要下列各項：

- [適用于 Web 或更新版本的 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)
- [Visual Studio 2013 Update 1](https://go.microsoft.com/fwlink/?LinkId=301714)

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

1. [建立新的 Web Forms 專案](#Exercise1)
2. [使用樣板建立 MVC 控制器](#Exercise2)
3. [使用樣板建立 Web API 控制器](#Exercise3)

完成此實驗室的預估時間： **60 分鐘**

> [!NOTE]
> 當您第一次啟動 Visual Studio 時，您必須選取其中一個預先定義的設定集合。 每個預先定義的集合都是設計來符合特定的開發風格，並決定視窗配置、編輯器行為、IntelliSense 程式碼片段和對話方塊選項。 本實驗室中的程式說明在使用 [**一般開發設定**] 集合時，在 Visual Studio 中完成指定工作所需的動作。 如果您針對開發環境選擇不同的 [設定] 集合，您應該考慮的步驟可能會有所差異。

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-new-web-forms-project"></a>練習1：建立新的 Web form 專案

在此練習中，您將使用**ASP.NET**整合專案體驗，在 Visual Studio 2013 中建立新的 Web form 網站，這可讓您輕鬆地在相同的應用程式中整合 web FORMS、MVC 和 web API 元件。 接著，您將探索所產生的解決方案並識別其元件，最後您會看到網站的運作方式。

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-a-new-site-using-the-one-aspnet-experience"></a>工作1–使用一 ASP.NET 體驗建立新網站

在這項工作中，您將根據**ASP.NET**專案類型，開始在 Visual Studio 中建立新的網站。 **其中一個 ASP.NET**會將所有 ASP.NET 技術合併，並提供您視需要混合使用和比對的選項。 接著，您將會辨識應用程式中即時的 Web form、MVC 和 Web API 的不同元件。

1. 開啟**Web Visual Studio Express 2013** ，然後選取 [檔案] **|新增專案 ...** 以啟動新的解決方案。

    ![建立新專案](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image1.png)

    *建立新專案*
2. 在 [**新增專案**] 對話方塊中，選取視覺效果  **C#底下的 [ASP.NET Web 應用程式] |[Web** ] 索引標籤，並確認已選取 [ **.NET Framework 4.5** ]。 將專案命名為*MyHybridSite*，選擇 [**位置**]，然後按一下 **[確定]** 。

    ![新增 ASP.NET Web 應用程式專案](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image2.png)

    *建立新的 ASP.NET Web 應用程式專案*
3. 在 [**新增 ASP.NET 專案**] 對話方塊中，選取 [ **Web** form] 範本，然後選取 [ **MVC**和**Web API** ] 選項。 此外，請確定 [**驗證**] 選項已設為 [**個別使用者帳戶**]。 按一下 [確定] 繼續操作。

    ![使用 Web Forms 範本建立新的專案，包括 Web API 和 MVC 元件](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image3.png)

    *使用 Web Forms 範本建立新的專案，包括 Web API 和 MVC 元件*
4. 您現在可以探索所產生解決方案的結構。

    ![探索產生的解決方案](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image4.png)

    *探索產生的解決方案*

    1. **帳戶：** 此資料夾包含要註冊的 Web 表單頁面、登入及管理應用程式的使用者帳戶。 在設定 Web form 專案範本期間選取 [**個別使用者帳戶**] 驗證選項時，會加入此資料夾。
    2. **模型：** 此資料夾將包含代表您的應用程式資料的類別。
    3. **控制器**和**VIEWS**： **ASP.NET MVC**和**ASP.NET Web API**元件都需要這些資料夾。 在下一個練習中，您將會探索 MVC 和 Web API 技術。
    4. Default.aspx **、** **Contact .aspx**和**關於 .aspx**檔案是預先定義的 Web Form 頁面，可供您用來做為建立應用程式特定頁面的起點。 這些檔案的程式設計邏輯位於稱為 &quot;程式碼後置&quot; 檔案的個別檔案中，該檔案具有 &quot;.aspx .vb&quot; 或 &quot;aspx.cs&quot; 延伸模組（視使用的語言而定）。 程式碼後置邏輯會在伺服器上執行，並以動態方式產生頁面的 HTML 輸出。
    5. [**網站**] 和 [**網站**] 頁面會定義應用程式中所有頁面的外觀與風格，以及標準行為。
5. 按兩下**default.aspx**檔案以流覽頁面的內容。

    ![探索 default.aspx 頁面](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image5.png)

    *探索 default.aspx 頁面*

    > [!NOTE]
    > 檔案頂端的**Page**指示詞會定義 Web Forms 頁面的屬性。 例如， **MasterPageFile**屬性會指定主版頁面的路徑，在此案例中為 [*網站. 主版*] 頁面，而 [**繼承**] 屬性則會定義要繼承之頁面的程式碼後置類別。 這個類別位於程式碼後**置屬性所決定的檔案**中。
    > 
    > **Asp： Content**控制項會保存網頁的實際內容（文字、標記和控制項），並對應至主版頁面上的**asp： ContentPlaceHolder**控制項。 在此情況下，頁面內容會呈現在 [*網站*] 頁面中定義的*MainContent*控制項內。
6. 展開**應用程式\_[開始**] 資料夾，並注意**WebApiConfig.cs**檔案。 Visual Studio 將該檔案包含在產生的解決方案中，因為您在使用一個 ASP.NET 範本設定專案時包含 Web API。
7. 開啟**WebApiConfig.cs**檔案。 在*WebApiConfig*類別中，您會找到與 web api 相關聯的設定，其會將 HTTP 路由對應至**web api 控制器**。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample1.cs)]
8. 開啟**RouteConfig.cs**檔案。 在*RegisterRoutes*方法中，您會發現與 mvc 相關聯的設定，其會將 HTTP 路由對應至**mvc 控制器**。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample2.cs)]

<a id="Ex1Task2"></a>
#### <a name="task-2--running-the-solution"></a>工作2–執行解決方案

在這項工作中，您將執行所產生的解決方案、探索應用程式及其部分功能，例如 URL 重寫和內建驗證。

1. 若要執行方案，請按**F5**或按一下位於工具列上的 [**開始**] 按鈕。 應用程式首頁應該會在瀏覽器中開啟。

    ![正在執行解決方案](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image6.png)
2. 確認正在叫用 Web form 頁面。 若要這麼做，請將 **/contact.aspx**附加至網址列中的 URL，然後按**enter**鍵。

    ![易記的 URL](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image7.png)

    *易記 Url*

    > [!NOTE]
    > 如您所見，URL 會變更為 **/contact**。 從**ASP.NET 4**開始，URL 路由功能已新增至 Web 表單，因此您可以撰寫類似 *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* 的 url，而不是 *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)* 。 如需詳細資訊，請參閱[URL 路由](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md)。
3. 您現在會探索整合到應用程式中的驗證流程。 若要這樣做，請按一下頁面右上角的 [**註冊**]。

    ![註冊新的使用者](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image8.png)

    *註冊新的使用者*
4. 在 [**註冊**] 頁面中，輸入**使用者名稱**和**密碼**，然後按一下 [**註冊**]。

    ![註冊頁面](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image9.png)

    *註冊頁面*
5. 應用程式會註冊新帳戶，並驗證使用者。

    ![使用者已驗證](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image10.png)

    *使用者已驗證*
6. 返回 Visual Studio，然後按**SHIFT + F5**停止調試。

<a id="Exercise2"></a>
### <a name="exercise-2-creating-an-mvc-controller-using-scaffolding"></a>練習2：使用樣板建立 MVC 控制器

在此練習中，您將利用 Visual Studio 所提供的 ASP.NET 樣板架構，建立具有動作和 Razor views 的 ASP.NET MVC 5 控制器來執行 CRUD 作業，而不需要撰寫任何一行程式碼。 此樣板進程會使用 Entity Framework Code First，在 SQL 資料庫中產生資料內容和資料庫架構。

**關於 Entity Framework Code First**

Entity Framework （EF）是物件關聯式對應程式（ORM），可讓您以概念應用程式模型進行程式設計來建立資料存取應用程式，而不需要直接使用關聯式儲存架構進行程式設計。

Entity Framework Code First 模型化工作流程可讓您使用自己的網域類別來代表 EF 在執行查詢、變更追蹤和更新函數時所依賴的模型。 使用 Code First 開發工作流程，您不需要藉由建立資料庫或指定架構來開始您的應用程式。 相反地，您可以撰寫標準的 .NET 類別，為您的應用程式定義最適當的領域模型物件，Entity Framework 將會為您建立資料庫。

> [!NOTE]
> 您可以在[這裡](../../../entity-framework.md)深入瞭解 Entity Framework。

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-new-model"></a>工作1–建立新的模型

您現在將定義**Person**類別，這會是由「基類庫」進程用來建立 MVC 控制器和 views 的模型。 您將從建立**Person**模型類別開始，並使用「基類庫」功能自動建立控制器中的 CRUD 作業。

1. 開啟**Web 的 Visual Studio Express 2013**和位於**來源/Ex2-MvcScaffolding/Begin**資料夾中的**MyHybridSite。** 或者，您可以繼續使用您在上一個練習中取得的解決方案。
2. 在**方案總管**中，以滑鼠右鍵按一下**MyHybridSite**專案的 [**模型**] 資料夾，然後選取 [**新增] |類別 ...** 。

    ![新增 Person 模型類別](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image11.png)

    *新增 Person 模型類別*
3. 在 [**加入新專案**] 對話方塊中，將檔案命名為*Person.cs* ，然後按一下 [**新增**]。

    ![建立 Person 模型類別](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image12.png)

    *建立 Person 模型類別*
4. 將**Person.cs**檔案的內容取代為下列程式碼。 按**CTRL + S**儲存變更。

    （程式碼片段- *BringingTogetherOneAspNet-Ex2-PersonClass*）

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample3.cs)]
5. 在**方案總管**中，以滑鼠右鍵按一下**MyHybridSite**專案，然後選取 [**建立**]，或按**CTRL + SHIFT + B**來建立專案。

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-an-mvc-controller"></a>工作2–建立 MVC 控制器

建立**人員**模型之後，您將使用 ASP.NET MVC 樣板搭配 Entity Framework 來建立 CRUD 控制器動作和**人員**的視圖。

1. 在**方案總管**中，以滑鼠右鍵按一下**MyHybridSite**專案的 [**控制器**] 資料夾，然後選取 [**新增] |新增 Scaffold 專案 ...** 。

    ![建立新的 scaffold 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image13.png)

    *建立新的 Scaffold 控制器*
2. 在 [**新增 Scaffold** ] 對話方塊中，**使用 Entity Framework 選取 [具有 views 的 MVC 5 控制器**]，然後按一下 [**新增]。**

    ![選取具有 views 和 Entity Framework 的 MVC 5 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image14.png)

    *選取具有 views 和 Entity Framework 的 MVC 5 控制器*
3. 將 [ *MvcPersonController* ] 設定為 [**控制器名稱**]，選取 [**使用非同步控制器動作**] 選項，然後選取 [ **Person （MyHybridSite）** ] 做為**模型類別**。

    ![新增具有樣板的 MVC 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image15.png)

    *新增具有樣板的 MVC 控制器*
4. 在 [**資料內容類別**] 底下，按一下 [**新增資料內容 ...** ]。

    ![建立新的資料內容](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image16.png)

    *建立新的資料內容*
5. 在 [**新增資料內容**] 對話方塊中，將新的資料內容命名為*PersonCoNtext* ，然後按一下 [**加入**]。

    ![建立新的 PersonCoNtext](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image17.png)

    *建立新的 PersonCoNtext 類型*
6. 按一下 [**新增**]，為具有樣板的**人員**建立新的控制器。 Visual Studio 接著會產生控制器動作、人員資料內容和 Razor views。

    ![建立具有樣板的 MVC 控制器之後](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image18.png)

    *建立具有樣板的 MVC 控制器之後*
7. 開啟 [**控制器**] 資料夾中的**MvcPersonController.cs**檔案。 請注意，CRUD 動作方法已自動產生。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample4.cs)]

    > [!NOTE]
    > 藉由在先前步驟的 [樣板] 選項中選取 [**使用非同步控制器動作**] 核取方塊，Visual Studio 會為牽涉到人員資料內容存取權的所有動作產生非同步動作方法。 建議您針對長時間執行的非 CPU 系結要求使用非同步動作方法，以避免在處理要求時封鎖 Web 服務器執行工作。

<a id="Ex2Task3"></a>
#### <a name="task-3--running-the-solution"></a>工作3–執行解決方案

在這項工作中，您將再次執行方案，以確認**人員**的觀點如預期般運作。 您將加入新的人員，以確認它已成功儲存至資料庫。

1. 按 **F5** 執行方案。
2. 流覽至 **/MvcPerson**。 [Scaffold] 視圖會顯示應顯示的人員清單。
3. 按一下 [**建立新**的] 以加入新人員。

    ![流覽至 scaffold MVC views](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image19.png)

    *流覽至 scaffold MVC views*
4. 在 [**建立**] 視圖中，提供人員的**名稱**和**年齡**，然後按一下 [**建立**]。

    ![加入新人員](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image20.png)

    *加入新人員*
5. 新人員會加入清單中。 在 [專案] 清單中，按一下 [**詳細資料**] 以顯示個人的詳細資料檢視。 然後，在**詳細資料**視圖中，按一下 [**返回清單**] 以返回清單視圖。

    ![個人的詳細資料檢視](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image21.png)

    *個人的詳細資料檢視*
6. 按一下 [**刪除**] 連結以刪除人員。 在 [**刪除**] 視圖中，按一下 [**刪除**] 以確認操作。

    ![刪除人員](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image22.png)

    *刪除人員*
7. 返回 Visual Studio，然後按**SHIFT + F5**停止調試。

<a id="Exercise3"></a>
### <a name="exercise-3-creating-a-web-api-controller-using-scaffolding"></a>練習3：使用樣板建立 Web API 控制器

Web API 架構是 ASP.NET 堆疊的一部分，其設計目的是為了讓您更輕鬆地執行 HTTP 服務，通常會透過 RESTful API 傳送和接收 JSON 或 XML 格式的資料。

在此練習中，您將再次使用 ASP.NET 的樣板來產生 Web API 控制器。 您將使用上一個練習中的相同**person**和**PersonCoNtext**類別，以 JSON 格式提供相同的人員資料。 您將瞭解如何在相同的 ASP.NET 應用程式中以不同的方式公開相同的資源。

<a id="Ex3Task1"></a>
#### <a name="task-1--creating-a-web-api-controller"></a>工作1–建立 Web API 控制器

在這項工作中，您將建立新的**WEB API 控制器**，它會以電腦可耗用的格式（例如 JSON）公開人員資料。

1. 如果尚未開啟，請開啟**Visual Studio Express 2013 For Web** ，然後開啟位於**Source/Ex3-WebAPI/Begin**資料夾中的**MyHybridSite。** 或者，您可以繼續使用您在上一個練習中取得的解決方案。

    > [!NOTE]
    > 如果您從練習3開始使用開始解決方案，請按**CTRL + SHIFT + B**來建立方案。
2. 在**方案總管**中，以滑鼠右鍵按一下**MyHybridSite**專案的 [**控制器**] 資料夾，然後選取 [**新增] |新增 Scaffold 專案 ...** 。

    ![建立新的 scaffold 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image23.png)

    *建立新的 scaffold 控制器*
3. 在 [**新增 Scaffold** ] 對話方塊中，選取左窗格中的 [ **web api** ]，然後在中間窗格中，**使用 Entity Framework** ，然後按一下 [新增] **。**

    ![選取具有動作和 Entity Framework 的 Web API 2 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "選取具有動作和 Entity Framework 的 Web API 2 控制器")

    *選取具有動作和 Entity Framework 的 Web API 2 控制器*
4. 將 [ *ApiPersonController* ] 設定為 [**控制器名稱**]，選取 [**使用非同步控制器動作**] 選項，然後選取 [ **Person] （MyHybridSite）** 和 [ **PersonCoNtext （MyHybridSite）** ] 做為 [**模型**] 和 [**資料內容**類別]。 然後按一下 [加入]。

    ![使用樣板新增 Web API 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "使用樣板新增 Web API 控制器")

    *使用樣板新增 Web API 控制器*
5. Visual Studio 接著會產生具有四個 CRUD 動作的**ApiPersonController**類別，以處理您的資料。

    ![使用樣板建立 Web API 控制器之後](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "使用樣板建立 Web API 控制器之後")

    *使用樣板建立 Web API 控制器之後*
6. 開啟**ApiPersonController.cs**檔案，並檢查*GetPeople*動作方法。 這個方法會查詢**PersonCoNtext**類型的 db 欄位，以便取得人員資料。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample5.cs)]
7. 現在請注意方法定義上方的批註。 它提供的 URI 會公開此動作，而您將在下一個工作中使用。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample6.cs)]

    > [!NOTE]
    > 根據預設，Web API 會設定為攔截 */api*路徑的查詢，以避免與 MVC 控制器發生衝突。 如果您需要變更此設定，請參閱[ASP.NET Web API 中的路由](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md)。

<a id="Ex3Task2"></a>
#### <a name="task-2--running-the-solution"></a>工作2–執行解決方案

在這項工作中，您將使用 Internet Explorer **F12 開發人員工具**來檢查來自 Web API 控制器的完整回應。 您將瞭解如何捕捉網路流量，以深入瞭解您的應用程式資料。

> [!NOTE]
> 請確定已在 [Visual Studio] 工具列上的 [**開始**] 按鈕中選取**Internet Explorer** 。
> 
> ![Internet Explorer 選項](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image27.png)
> 
> **F12 開發人員工具**有一組廣泛的功能，不涵蓋在此實際操作實驗室中。 如果您想要深入瞭解，請參閱[使用 F12 開發人員工具](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85))。

1. 按 **F5** 執行方案。

    > [!NOTE]
    > 為了正確地執行此工作，您的應用程式需要有資料。 如果您的資料庫是空的，您可以回到練習2中的工作3，並遵循如何使用 MVC views 建立新人員的步驟進行。
2. 在瀏覽器中，按**F12**開啟 [**開發人員工具**] 面板。 按**CTRL** + **4**或按一下**網路**圖示，然後按一下綠色箭號按鈕來開始捕獲網路流量。

    ![正在起始 Web API 網路捕獲](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "正在起始 Web API 網路捕獲")

    *正在起始 Web API 網路捕獲*
3. 將**api/ApiPerson**附加至瀏覽器網址列中的 URL。 您現在將會從**ApiPersonController**檢查回應的詳細資料。

    ![透過 Web API 來抓取人員資料](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "透過 Web API 來抓取人員資料")

    *透過 Web API 來抓取人員資料*

    > [!NOTE]
    > 下載完成後，系統會提示您對下載的檔案進行動作。 讓對話方塊保持開啟狀態，以便能夠透過 [開發人員] 工具視窗觀看回應內容。
4. 現在，您將會檢查回應的主體。 若要這樣做，請按一下 [**詳細資料**] 索引標籤，然後按一下 [**回應主體**]。 您可以檢查下載的資料是否為具有與**Person**類別對應之屬性**識別碼**、**名稱**和**年齡**的物件清單。

    ![查看 Web API 回應主體](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "查看 Web API 回應主體")

    *查看 Web API 回應主體*

<a id="Ex3Task3"></a>
#### <a name="task-3--adding-web-api-help-pages"></a>工作 3-新增 Web API 說明頁面

當您建立 Web API 時，建立說明頁會很有説明，讓其他開發人員知道如何呼叫您的 API。 您可以手動建立和更新檔頁面，但最好是自動產生它們，以避免必須執行維護工作。 在這項工作中，您將使用 Nuget 套件，自動產生 Web API 說明頁面至解決方案。

1. 從 Visual Studio 的 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後按一下 [**套件管理員主控台**]。
2. 在 [**套件管理員主控台**] 視窗中，執行下列命令：

    [!code-powershell[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample7.ps1)]

    > [!NOTE]
    > **WebApi. HelpPage**套件會安裝必要的元件，並將 [說明] 頁面的 MVC 視圖加入 [**區域/HelpPage** ] 資料夾底下。

    ![HelpPage 區域](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage 區域")

    *HelpPage 區域*
3. 根據預設，說明頁面會有檔的預留位置字串。 您可以使用 XML 檔批註來建立檔。 若要啟用此功能，請開啟位於 [**區域/HelpPage/應用程式]\_[開始**] 資料夾中的**HelpPageConfig.cs**檔案，並取消批註下列程式程式碼：

    [!code-javascript[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample8.js)]
4. 在**方案總管**中，以滑鼠右鍵按一下專案**MyHybridSite**，選取 [**屬性**]，然後按一下 [**組建**] 索引標籤。

    ![[組建] 索引標籤](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "組建區段")

    *[組建] 索引標籤*
5. 在 [**輸出**] 底下，選取 [ **XML**檔檔]。 在 [編輯] 方塊中，輸入**應用程式\_Data/xml**。

    ![[組建] 索引標籤中的輸出區段](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "[組建] 索引標籤中的輸出區段")

    *[組建] 索引標籤中的輸出區段*
6. 按**CTRL** + **S**以儲存變更。
7. 從 [**控制器**] 資料夾中開啟**ApiPersonController.cs**檔案。
8. 在*GetPeople*方法簽章和 *//GET api/ApiPerson*批註之間輸入新的一行，然後輸入三個正斜線。

    > [!NOTE]
    > Visual Studio 會自動插入定義方法檔的 XML 元素。
9. 加入摘要文字和*GetPeople*方法的傳回值。 看起來應該如下所示。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample9.cs)]
10. 按 **F5** 執行方案。
11. 將 **/help**附加至網址列中的 URL，以流覽至 [說明] 頁面。

    ![ASP.NET Web API 說明頁面](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API 說明頁面")

    *ASP.NET Web API 說明頁面*

    > [!NOTE]
    > 頁面的主要內容是以控制器分組的 Api 資料表。 系統會使用**IApiExplorer**介面，以動態方式產生資料表專案。 如果您新增或更新 API 控制器，下一次建立應用程式時，資料表會自動更新。
    > 
    > [ **API** ] 欄會列出 HTTP 方法和相對 URI。 [**描述**] 資料行包含已從方法的檔中解壓縮的資訊。
12. 請注意，您在方法定義上方新增的描述會顯示在 [描述] 欄中。

    ![API 方法描述](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API 方法描述")

    *API 方法描述*
13. 按一下其中一個 API 方法，流覽至包含詳細資訊的頁面，包括範例回應主體。

    ![詳細資訊頁面](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "詳細資訊頁面")

    *詳細資訊頁面*

---

<a id="Summary"></a>
## <a name="summary"></a>總結

藉由完成此實際操作實驗室，您已瞭解如何：

- 使用 Visual Studio 2013 中的一個 ASP.NET 體驗建立新的 Web 應用程式
- 將多個 ASP.NET 技術整合成一個單一專案
- 使用 ASP.NET 的架構，從您的模型類別產生 MVC 控制器和 views
- 產生 Web API 控制器，其使用非同步程式設計和透過 Entity Framework 的資料存取等功能
- 自動為您的控制器產生 Web API 說明頁面
