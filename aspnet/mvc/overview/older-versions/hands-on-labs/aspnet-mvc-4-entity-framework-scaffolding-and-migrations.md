---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
title: ASP.NET MVC 4 Entity Framework 的架構和遷移 |Microsoft Docs
author: rick-anderson
description: 如果您熟悉 ASP.NET MVC 4 控制器方法，或已完成 &quot;協助程式、表單和驗證&quot; 實際操作實驗室，您應該注意 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 093c1362-f10b-407c-a708-be370f4b62b0
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
msc.type: authoredcontent
ms.openlocfilehash: 2b26224390af70e19ca0593abe93a6867140f8ab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598900"
---
# <a name="aspnet-mvc-4-entity-framework-scaffolding-and-migrations"></a>ASP.NET MVC 4 Entity Framework Scaffold 和移轉

依[Web Camp 團隊](https://twitter.com/webcamps)

[下載 Web Camp 訓練套件](https://aka.ms/webcamps-training-kit)

如果您熟悉 ASP.NET MVC 4 控制器方法，或已完成 &quot;協助程式、表單和驗證&quot; 實際操作實驗室，您應該注意到，有許多邏輯可以用來建立、更新、列出和移除任何資料實體，這會在應用程式之間重複。 不提說，如果您的模型有數個要操作的類別，您可能會花費相當長的時間來撰寫每個實體作業的 POST 和 GET 動作方法，以及每個視圖。

在此實驗室中，您將瞭解如何使用 ASP.NET MVC 4 架構，自動產生應用程式 CRUD （建立、讀取、更新和刪除）的基準。 從簡單的模型類別開始，而不需撰寫任何一行程式碼，您將建立一個控制器，其中包含所有 CRUD 作業，以及所有必要的視圖。 建立並執行簡單的方案之後，您將會產生應用程式資料庫，以及用於資料操作的 MVC 邏輯和 views。

此外，您將瞭解在整個應用程式中使用 Entity Framework 遷移來執行模型更新有多麼容易。 Entity Framework 遷移可讓您在使用簡單步驟變更模型之後，修改資料庫。 有了這些概念，您就能夠更有效率地建立及維護 web 應用程式，利用 ASP.NET MVC 4 的最新功能。

> [!NOTE]
> 所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可從[Microsoft web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)取得。 此實驗室的特定專案可在[ASP.NET MVC 4 Entity Framework 的樣板和遷移](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations)中取得。

<a id="Objectives"></a>
### <a name="objectives"></a>目標

在此實際操作實驗室中，您將瞭解如何：

- 在控制器中使用 CRUD 作業的 ASP.NET 架構。
- 使用 Entity Framework 遷移來變更資料庫模型。

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Prerequisites

您必須具有下列專案，才能完成此實驗室：

- 適用于 Web 或上層的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （如需有關如何安裝的指示，請參閱[附錄 A](#AppendixA) ）。

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>安裝程式

**安裝程式碼片段**

為了方便起見，您將在此實驗室中管理的大部分程式碼都是以 Visual Studio 程式碼片段的形式提供。 若要安裝程式碼片段，請執行 **.\Source\Setup\CodeSnippets.vsi**檔案。

如果您不熟悉 Visual Studio Code 程式碼片段，而且想要瞭解如何使用，您可以參閱本檔中的附錄 &quot;[附錄 B：使用程式碼片段](#AppendixB)&quot;。

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>練習

下列練習會組成這個實際操作實驗室：

1. [搭配 Entity Framework 遷移使用 ASP.NET MVC 4 樣板](#Exercise1)

> [!NOTE]
> 此練習會伴隨一個**結束**資料夾，其中包含您在完成練習之後應該取得的結果解決方案。 如果您需要額外的協助來進行練習，您可以使用此解決方案做為指南。

完成此實驗室的預估時間： **30 分鐘**

<a id="Exercise1"></a>

<a id="Exercise_1_Using_ASPNET_MVC_4_Scaffolding_with_Entity_Framework_Migrations"></a>
### <a name="exercise-1-using-aspnet-mvc-4-scaffolding-with-entity-framework-migrations"></a>練習1：搭配 Entity Framework 遷移使用 ASP.NET MVC 4 樣板

ASP.NET MVC 樣板提供快速的方式，以標準化的方式產生 CRUD 作業，建立必要的邏輯，讓您的應用程式與資料庫層互動。

在此練習中，您將瞭解如何搭配使用 ASP.NET MVC 4 樣板與 code first 來建立 CRUD 方法。 然後，您將瞭解如何使用 Entity Framework 遷移來更新您的模型，套用資料庫中的變更。

<a id="Ex1Task1"></a>

<a id="Task_1-_Creating_a_new_ASPNET_MVC_4_project_using_Scaffolding"></a>
#### <a name="task-1--creating-a-new-aspnet-mvc-4-project-using-scaffolding"></a>工作 1-使用樣板建立新的 ASP.NET MVC 4 專案

1. 如果尚未開啟，請啟動**Visual Studio 2012**。
2. 選取檔案 **|新增專案**。 在 [新增專案] 對話方塊中的 **[ C#視覺效果] |Web**區段中，選取 [ **ASP.NET MVC 4 Web 應用程式**]。 將專案命名為**MVC4andEFMigrations** ，並將此實驗室的 [位置] 設定為 [ **Source\Ex1-UsingMVC4ScaffoldingEFMigrations** ] 資料夾。 將 [**方案名稱**] 設定為 [**開始**]，並確定已核取 [**為方案建立目錄**]。 按一下 [確定]。

    ![[新增 ASP.NET MVC 4 專案] 對話方塊](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "[新增 ASP.NET MVC 4 專案] 對話方塊")

    *[新增 ASP.NET MVC 4 專案] 對話方塊*
3. 在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [**網際網路應用程式**] 範本，並確定 [ **Razor** ] 是選取的**視圖引擎**。 按一下 [確定] 建立專案。

    ![新增 ASP.NET MVC 4 網際網路應用程式](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "新增 ASP.NET MVC 4 網際網路應用程式")

    *新增 ASP.NET MVC 4 網際網路應用程式*
4. 在方案總管中，以滑鼠右鍵按一下 [**模型**]，然後選取 [**新增] |** 建立簡單類別 person （POCO）的類別。 為 it**人員**命名，然後按一下 **[確定]** 。
5. 開啟 Person 類別並插入下列屬性。

    （程式碼片段- *ASP.NET MVC 4 和 Entity Framework 遷移-Ex1 Person 屬性*）

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample1.cs)]
6. 按一下 [**組建] |建立方案**以儲存變更並建立專案。

    ![建置應用程式](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "建置應用程式")

    *建置應用程式*
7. 在 方案總管中，以滑鼠右鍵按一下 控制器 資料夾，然後選取 **新增 |控制器**。
8. 將控制器命名為*PersonController* ，並使用下列值完成 [樣板]**選項**。

   1. 在 [**範本**] 下拉式清單中，使用 [Entity Framework] 選項，選取**具有讀取/寫入動作和 views 的 MVC 控制器**。
   2. 在 [**模型類別**] 下拉式清單中，選取 [ **Person** ] 類別。
   3. 在 [**資料內容類別**] 清單中，選取 [ **&lt;新的資料內容 ...]&gt;** 。 選擇任何名稱，然後按一下 **[確定]** 。
   4. 在 [ **Views** ] 下拉式清單中，確認已選取 [ **Razor** ]。

      ![使用樣板新增人員控制器](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "使用樣板新增人員控制器")

      *使用樣板新增人員控制器*
9. 按一下 [**新增**]，為具有樣板的人員建立新的控制器。 您現在已產生控制器動作和 views。

    ![建立具有樣板的人員控制器之後](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "建立具有樣板的人員控制器之後")

    *建立具有樣板的人員控制器之後*
10. 開啟**PersonController**類別。 請注意，已自動產生完整的 CRUD 動作方法。

   ![在人員控制器內](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "在人員控制器內")

   *在人員控制器內*

<a id="Ex1Task2"></a>

<a id="Task_2-_Running_the_application"></a>
#### <a name="task-2--running-the-application"></a>工作 2-正在執行應用程式

此時，尚未建立資料庫。 在這項工作中，您會第一次執行應用程式，並測試 CRUD 作業。 系統會使用 Code First 即時建立資料庫。

1. 按 **F5** 執行應用程式。
2. 在瀏覽器中，將 **/Person**新增至 URL，以開啟 [人員] 頁面。

    ![應用程式首次執行](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "應用程式首次執行")

    *應用程式：第一次執行*
3. 您現在將探索 Person 頁面並測試 CRUD 作業。

    1. 按一下 [**建立新**的] 以加入新人員。 輸入 [名字] 和 [姓氏]，然後按一下 [**建立**]。

        ![加入新人員](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "加入新人員")

        *加入新人員*
    2. 在人員清單中，您可以刪除、編輯或加入專案。

        ![人員清單](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "人員清單")

        *人員清單*
    3. 按一下 [**詳細資料**] 以開啟該人員的詳細資料。

        ![人員的詳細資料](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "人員的詳細資料")

        *人員的詳細資料*
4. 關閉瀏覽器並返回 Visual Studio。 請注意，您已在整個應用程式中建立 person 實體的整個 CRUD-從模型到 views，而不需要撰寫任何一行程式碼！

<a id="Ex1Task3"></a>

<a id="Task_3-_Updating_the_database_using_Entity_Framework_Migrations"></a>
#### <a name="task-3--updating-the-database-using-entity-framework-migrations"></a>工作 3-使用 Entity Framework 遷移來更新資料庫

在這項工作中，您將使用 Entity Framework 遷移來更新資料庫。 您將會發現，使用 Entity Framework 遷移功能來變更模型並反映資料庫中的變更有多簡單。

1. 開啟 [套件管理員主控台]。 選取 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。
2. 在 [套件管理器主控台] 中，輸入下列命令：

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample2.ps1)]

    ![啟用遷移](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "啟用移轉")

    *啟用遷移*

    [啟用-遷移] 命令會建立 [**遷移**] 資料夾，其中包含用來初始化資料庫的腳本。

    ![[遷移] 資料夾](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "[遷移] 資料夾")

    *[遷移] 資料夾*
3. 在 [遷移] 資料夾中開啟**Configuration.cs**檔案。 找出類別的函式，並將**AutomaticMigrationsEnabled**值變更為*true*。

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample3.cs)]
4. 開啟 Person 類別，並為人員的中間名加入屬性。 使用這個新屬性時，您會變更模型。

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample4.cs)]
5. 選取**組建 |建立**應用程式的功能表上的 [組建方案]。

    ![建置應用程式](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "建置應用程式")

    *建置應用程式*
6. 在 [套件管理器主控台] 中，輸入下列命令：

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample5.ps1)]

    此命令會尋找資料物件中的變更，然後再加入必要的命令，以便據以修改資料庫。

    ![加入中間名](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "加入中間名")

    *加入中間名*
7. 選擇性您可以執行下列命令，以差異更新產生 SQL 腳本。 這可讓您以手動方式更新資料庫（在此情況下不需要），或套用其他資料庫中的變更：

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample6.ps1)]

    ![產生 SQL 腳本](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "產生 SQL 指令碼")

    *產生 SQL 腳本*

    ![SQL 腳本更新](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL 腳本更新")

    *SQL 腳本更新*
8. 在 [套件管理員主控台] 中，輸入下列命令以更新資料庫：

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample7.ps1)]

    ![正在更新資料庫](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "更新資料庫")

    *正在更新資料庫*

    這會在 [**人員**] 資料表中加入**MiddleName**資料行，以符合**Person**類別的目前定義。
9. 更新資料庫之後，以滑鼠右鍵按一下 [控制器] 資料夾，然後選取 [**新增] |** 要再次新增人員控制器的控制器（以相同的值完成）。 這會更新現有的方法，並加入新的屬性。

    ![新增控制器更新](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "新增控制器更新")

    *正在更新控制器*
10. 按一下 [新增]。 然後，選取 [**覆寫 PersonController.cs** ] 和 [**覆寫關聯的視圖**] 的值，然後按一下 **[確定]** 。

   ![新增控制器覆寫](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image19.png)

   *正在更新控制器*

<a id="Ex1Task4"></a>

<a id="Task4-_Running_the_application"></a>
#### <a name="task4--running-the-application"></a>Task4-執行應用程式

1. 按 **F5** 執行應用程式。
2. 開啟 **/Person**。 請注意，資料已保留，但已加入「中間名」資料行。

    ![已新增中間名](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "已新增中間名")

    *已新增中間名*
3. 如果您按一下 [**編輯**]，就可以將中間名加入至目前的人員。

    ![中間名版本](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "中間名版本")

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>總結

在這個實際操作的實驗室中，您已學到使用任何模型類別來建立 CRUD 作業與 ASP.NET MVC 4 架構的簡單步驟。 然後，您已瞭解如何在應用程式中執行端對端更新-從資料庫到 views-使用 Entity Framework 遷移。

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附錄 A：安裝 Web 的 Visual Studio Express 2012

您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。 下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。

1. 移至 [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)。 或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Windows Azure SDK&quot;來搜尋產品 &quot;<em>Visual Studio Express 2012 For Web</em> 。
2. 按一下 [**立即安裝**]。 如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。
3. 開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。

    ![安裝 Visual Studio Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "安裝 Visual Studio Express")

    *安裝 Visual Studio Express*
4. 閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。

    ![接受授權條款](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image23.png)

    *接受授權條款*
5. 等到下載和安裝程式完成為止。

    ![安裝進度](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image24.png)

    *安裝進度*
6. 當安裝完成時，按一下 **[完成]** 。

    ![安裝已完成](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image25.png)

    *安裝已完成*
7. 按一下 **[** 結束] 以關閉 Web Platform Installer。
8. 若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。

    ![VS Express for Web 磚](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image26.png)

    *VS Express for Web 磚*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>附錄 B：使用程式碼片段

有了程式碼片段，您就可以輕鬆地擁有所需的所有程式碼。 實驗室檔會告訴您可以使用它們的確切時機，如下圖所示。

![使用 Visual Studio 程式碼片段將程式碼插入您的專案](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "使用 Visual Studio 程式碼片段將程式碼插入您的專案")

*使用 Visual Studio 程式碼片段將程式碼插入您的專案*

***若要使用鍵盤新增程式碼片段（C#僅限）***

1. 將游標放在您想要插入程式碼的位置。
2. 開始鍵入程式碼片段名稱（不含空格或連字號）。
3. 監看 IntelliSense 會顯示相符的程式碼片段名稱。
4. 選取正確的程式碼片段（或繼續輸入，直到選取整個程式碼片段的名稱為止）。
5. 按兩次 Tab 鍵，在游標位置插入程式碼片段。

![開始鍵入程式碼片段名稱](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "開始鍵入程式碼片段名稱")

*開始鍵入程式碼片段名稱*

![按 Tab 鍵以選取反白顯示的程式碼片段](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "按 Tab 鍵以選取反白顯示的程式碼片段")

*按 Tab 鍵以選取反白顯示的程式碼片段*

![再按一次 Tab 鍵，將會展開程式碼片段](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "再按一次 Tab 鍵，將會展開程式碼片段")

*再按一次 Tab 鍵，將會展開程式碼片段*

***若要使用滑鼠C#（、Visual Basic 和 XML）加入程式碼片段***sha-1. 以滑鼠右鍵按一下您要插入程式碼片段的位置。

1. 選取 [**插入程式碼片段**]，後面接著 [ **My Code 程式碼片段**]。
2. 按一下清單中的相關程式碼片段，即可加以選取。

![以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]")

*以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]*

![按一下清單中的相關程式碼片段，即可加以選取](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "按一下清單中的相關程式碼片段，即可加以選取")

*按一下清單中的相關程式碼片段，即可加以選取*
