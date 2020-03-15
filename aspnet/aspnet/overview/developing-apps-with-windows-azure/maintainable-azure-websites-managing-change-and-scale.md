---
uid: aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
title: 實習實驗室：可維護的 Azure 網站：管理變更和調整規模 |Microsoft Docs
author: rick-anderson
description: 在此實驗室中，您將瞭解 Microsoft Azure 如何讓您輕鬆地建立網站並將其部署到生產環境。
ms.author: riande
ms.date: 07/16/2014
ms.assetid: ecfd0eb4-c4ad-44e6-9db9-a2a66611ff6a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
msc.type: authoredcontent
ms.openlocfilehash: c88bae40a8aa092037c0b359ee391acaf161cf10
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624268"
---
# <a name="hands-on-lab-maintainable-azure-websites-managing-change-and-scale"></a>實習實驗室：可維護的 Azure 網站：管理變更和調整規模

依[Web Camp 團隊](https://twitter.com/webcamps)

[下載 Web Camp 訓練套件](https://aka.ms/webcamps-training-kit)

> Microsoft Azure 可讓您輕鬆地建立網站並將其部署到生產環境。 但是當您的應用程式上線時，您就剛開始著手！ 您需要處理變更的需求、資料庫更新、規模調整等等。 幸運的是，Azure App Service 已涵蓋在內，有許多功能可協助您讓網站順暢執行。
>
> Azure 為任何大小的 web 應用程式提供安全且彈性的開發、部署和調整選項。 運用您的現有工具以建立與部署應用程式，省去管理基礎結構的麻煩。
>
> 輕鬆部署使用您慣用的開發工具所建立的內容，即可在幾分鐘內自行布建生產 web 應用程式。 您可以直接從原始檔控制部署現有的網站，並支援**Git**、 **GitHub**、 **Bitbucket**、 **TFS**，甚至是**DropBox**。 直接從您最愛的 IDE 或在 Windows 中使用**PowerShell**或在任何 OS 上執行的**CLI**工具部署腳本。 一旦部署後，您的網站就可以透過持續部署的支援，保持在最新狀態。
>
> Azure 為任何資料提供可調式、持久的雲端儲存體、備份和復原解決方案，無論是大型或小型。 將應用程式部署至生產環境時，儲存體服務（例如資料表、Blob 和 SQL 資料庫）可協助您在雲端中調整應用程式的規模。
>
> 有了 SQL database，在部署新版本的應用程式時，將您的生產力資料庫保持在最新狀態是很重要的。 感謝**Entity Framework Code First 移轉**，您的資料模型開發和部署已經過簡化，可以在幾分鐘內更新您的環境。 這個實際操作實驗室將會顯示您在 Microsoft Azure 中將 web 應用程式部署至生產環境時，可能會遇到的不同主題。
>
> 所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)取得。
>
> 如需本主題的深入涵蓋範圍，請參閱[使用 Azure 電子書建立真實世界的雲端應用程式](building-real-world-cloud-apps-with-windows-azure/introduction.md)。

<a id="Overview"></a>
## <a name="overview"></a>概觀

<a id="Objectives"></a>
### <a name="objectives"></a>目標

在此實際操作實驗室中，您將瞭解如何：

- 使用現有的模型啟用 Entity Framework 遷移
- 使用 Entity Framework 遷移，據以更新物件模型和資料庫
- 使用 Git 部署至 Azure App Service
- 使用 Azure 管理入口網站復原到先前的部署
- 使用 Azure 儲存體來調整 web 應用程式
- 使用 Azure 管理入口網站為 web 應用程式設定自動調整
- 在 Visual Studio 中建立和設定負載測試專案

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Prerequisites

若要完成此實際操作實驗室，需要下列各項：

- [適用于 Web 或更新版本的 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)
- [Azure SDK for .NET 2。2](https://www.microsoft.com/windowsazure/sdk/)
- [GIT 版本控制系統](http://git-scm.com/download)
- Microsoft Azure 訂用帳戶

    - 註冊[免費試用版](https://aka.ms/watk-freetrial)
    - 如果您是 Visual Studio Professional、Test Professional、Premium 或旗艦版的 MSDN 或 MSDN 平臺訂閱者，請立即啟用您的[msdn 權益](https://aka.ms/watk-msdn)，以開始在 Azure 上進行開發和測試
    - [BizSpark](https://aka.ms/watk-bizspark)成員會透過其 Visual Studio Ultimate 含 MSDN 訂用帳戶自動獲得 Azure 權益
    - [Microsoft 合作夥伴網路](https://aka.ms/watk-mpn)Cloud Essentials 方案的成員免費收到每月 Azure 信用額度

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

1. [使用 Entity Framework 遷移](#Exercise1)
2. [將 Web 應用程式部署至預備環境](#Exercise2)
3. [在生產環境中執行部署復原](#Exercise3)
4. [使用 Azure 儲存體進行調整](#Exercise4)
5. [使用 Web Apps 的自動](#Exercise5)調整（適用于 Visual Studio 2013 旗艦版的選擇性）

完成此實驗室的預估時間： **75 分鐘**

> [!NOTE]
> 當您第一次啟動 Visual Studio 時，您必須選取其中一個預先定義的設定集合。 每個預先定義的集合都是設計來符合特定的開發風格，並決定視窗配置、編輯器行為、IntelliSense 程式碼片段和對話方塊選項。 本實驗室中的程式說明在使用 [**一般開發設定**] 集合時，在 Visual Studio 中完成指定工作所需的動作。 如果您針對開發環境選擇不同的 [設定] 集合，您應該考慮的步驟可能會有所差異。

<a id="Exercise1"></a>
### <a name="exercise-1-using-entity-framework-migrations"></a>練習1：使用 Entity Framework 遷移

當您開發應用程式時，您的資料模型可能會隨著時間而改變。 這些變更可能會影響資料庫中的現有模型（如果您要建立新版本），而且您必須讓資料庫保持在最新狀態，以避免發生錯誤。

為了簡化模型中這些變更的追蹤， **Entity Framework Code First 移轉**會自動偵測與資料庫架構比較模型的變更，並產生特定程式碼來更新您的資料庫，並建立新*版本*的資料庫。

此練習會示範如何為您的應用程式啟用**遷移**，以及如何輕鬆地偵測並產生變更以更新您的資料庫。

<a id="Ex1Task1"></a>
#### <a name="task-1--enabling-migrations"></a>工作1–啟用遷移

在這項工作中，您將逐步完成啟用**萬能技客測驗**資料庫**Entity Framework Code First 移轉**、變更模型及瞭解這些變更反映在資料庫中的步驟。

1. 開啟 Visual Studio，然後從**Source\Ex1-UsingEntityFrameworkMigrations\Begin**開啟**GeekQuiz**方案檔。
2. 建立解決方案，以便下載並安裝**NuGet**套件相依性。 若要這樣做，請以滑鼠右鍵按一下方案，然後按一下 [**建立方案**] 或按**Ctrl + Shift + B**。
3. 從 Visual Studio 的 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後按一下 [**套件管理員主控台**]。
4. 在 [**套件管理員主控台**] 中，輸入下列命令，然後按**enter**。 將會建立以現有模型為基礎的初始遷移。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample1.ps1)]

    ![啟用遷移](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "啟用移轉")

    *啟用遷移*

    > [!NOTE]
    > 此命令會將 [**遷移**] 資料夾新增至萬能技客測驗專案，其中包含名為**Configuration.cs**的檔案。 **Configuration**類別可讓您設定遷移如何針對您的內容運作。
5. 啟用遷移之後，您必須更新**設定類別，** 以在資料庫中填入**萬能技客測驗**所需的初始資料。 在 [**遷移**] 底下，以位於此實驗室的 [ **Source\Assets** ] 資料夾中的檔案取代**Configuration.cs**檔案。

    > [!NOTE]
    > 由於**遷移**將會在每次資料庫更新時呼叫**種子**方法，因此您必須確定資料庫中的記錄不會重複。 **AddOrUpdate**方法將有助於防止重複的資料。
6. 若要新增初始遷移，請輸入下列命令，然後按**enter**。

    > [!NOTE]
    > 請確定您的 LocalDB 實例中沒有名為 &quot;GeekQuizProd&quot; 的資料庫。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample2.ps1)]

    ![新增基底架構遷移](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "新增基底架構遷移")

    *新增基底架構遷移*

    > [!NOTE]
    > 「**新增-遷移**」會根據您在上次建立遷移之後對模型所做的變更，scaffold 下一次遷移。 在此情況下，因為它是第一次的專案遷移，所以它會加入腳本來建立**TriviaCoNtext**類別中定義的所有資料表。
7. 執行下列命令來執行遷移以更新資料庫。 針對此命令，您將指定**Verbose**旗標，以查看要套用至目標資料庫的 SQL 語句。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample3.ps1)]

    ![正在建立初始資料庫](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "正在建立初始資料庫")

    *正在建立初始資料庫*

    > [!NOTE]
    > **更新-資料庫**會將任何暫止的遷移套用至資料庫。 在此情況下，它會使用您的 web.config 檔案中定義的連接字串來建立資料庫。
8. 移至 [**流覽**] 功能表，然後開啟 [ **SQL Server 物件總管**]。

    ![在 SQL Server 物件總管中開啟](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "在 SQL Server 物件總管中開啟")

    *在 SQL Server 物件總管中開啟*
9. 在 [ **SQL Server 物件總管**] 視窗中，以滑鼠右鍵按一下 [ **SQL Server** ] 節點，然後選取 [**新增 SQL Server ...** ] 選項，以連接到您的 LocalDB 實例。

    ![加入 SQL Server 實例](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "加入 SQL Server 實例")

    *將 SQL Server 實例新增至 SQL Server 物件總管*
10. 將 [**伺服器名稱**] 設定為 *（localdb） \v11.0* ，並將 [ **Windows 驗證**] 保留為您的驗證模式。 按一下 [連接] 以繼續。

    ![連接到 LocalDB](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "連接到 LocalDB")

    *連接到 LocalDB*
11. 開啟 [ **GeekQuizProd** ] 資料庫，然後展開 [**資料表]** 節點。 如您所見，**更新資料庫**命令會產生**TriviaCoNtext**類別中定義的所有資料表。 找出**dbo。TriviaQuestions**資料表並開啟 [資料行] 節點。 在下一個工作中，您會在此資料表中加入新的資料行，並使用**遷移**來更新資料庫。

    ![邏輯問題資料行](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "邏輯問題資料行")

    *邏輯問題資料行*

<a id="Ex1Task2"></a>
#### <a name="task-2--updating-database-schema-using-migrations"></a>工作2–使用遷移更新資料庫架構

在這項工作中，您將使用**Entity Framework Code First 移轉**來偵測模型中的變更，並產生必要的程式碼來更新資料庫。 您將會藉由在其中加入新的屬性來更新**TriviaQuestions**實體。 接著，您將執行命令來建立新的遷移，以在資料表中包含新的資料行。

1. 在**方案總管**中，按兩下位於 [**模型**] 資料夾內的**TriviaQuestion.cs**檔案。
2. 新增名為 [**提示**] 的新屬性，如下列程式碼片段所示。

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample4.cs)]
3. 在 [**套件管理員主控台**] 中，輸入下列命令，然後按**enter**。 將會建立新的遷移，反映模型中的變更。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample5.ps1)]

    ![新增-遷移](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "新增-遷移")

    *新增-遷移*

    > [!NOTE]
    > 遷移檔案是由兩個**向上**和**向下**的方法所組成。
    >
    > - **Up**方法將用來指定要將應用程式的目前版本套用至資料庫所需的變更。
    > - **向下鍵**會用來反轉我們已新增至**Up**方法的變更。
    >
    > 當資料庫移轉更新資料庫時，它會以時間戳記循序執行所有的遷移，而且只有自上次更新後尚未使用的所有遷移（\_MigrationHistory 表會持續追蹤已套用的遷移）。 所有遷移的**Up**方法都會被呼叫，並會進行已指定到資料庫的變更。 如果我們決定回到先前的遷移，將會呼叫**向下**方法來以相反順序重做變更。
4. 在 [**套件管理員主控台**] 中，輸入下列命令，然後按**enter**。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample6.ps1)]
5. **更新資料庫**命令的輸出會產生**Alter Table** SQL 語句，以將新的資料行加入至**TriviaQuestions**資料表，如下圖所示。

    ![已產生新增資料行 SQL 語句](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "已產生新增資料行 SQL 語句")

    *已產生新增資料行 SQL 語句*
6. 在**SQL Server 物件總管**中，重新整理**dbo。TriviaQuestions**資料表，並檢查是否顯示新的 [**提示**] 資料行。

    ![顯示新的提示資料行](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "顯示新的提示資料行")

    *顯示新的提示資料行*
7. 回到 [ **TriviaQuestion.cs**編輯器] 中，將**StringLength**條件約束加入至 [*提示*] 屬性，如下列程式碼片段所示。

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample7.cs)]
8. 在 [**套件管理員主控台**] 中，輸入下列命令，然後按**enter**。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample8.ps1)]
9. 在 [**套件管理員主控台**] 中，輸入下列命令，然後按**enter**。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample9.ps1)]
10. **更新資料庫**命令的輸出產生了**Alter Table** SQL 語句來更新**TriviaQuestions**資料表的*提示*資料行類型，如下圖所示。

    ![已產生 Alter column SQL 語句](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "已產生 Alter column SQL 語句")

    *已產生 Alter column SQL 語句*
11. 在**SQL Server 物件總管**中，重新整理**dbo。TriviaQuestions**資料表，並檢查 [**提示**] 資料行類型是否為 **[Nvarchar （150）** ]。

    ![顯示新的條件約束](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "顯示新的條件約束")

    *顯示新的條件約束*

<a id="Exercise2"></a>
### <a name="exercise-2-deploying-a-web-app-to-staging"></a>練習2：將 Web 應用程式部署至預備環境

**Azure App Service 中的 Web Apps**可讓您執行分段發行。 預備發行會為每個預設生產網站建立一個預備網站位置，並讓您在不停機時間的情況下交換這些插槽。 這在發行至公用、以累加方式整合網站內容之前驗證變更，以及如果變更未如預期般運作時，這非常有用。

在此練習中，您會使用 Git 原始檔控制，將**萬能技客測驗**應用程式部署至 web 應用程式的預備環境。 若要這麼做，您將建立 web 應用程式並在管理入口網站布建必要的元件、設定**Git**存放庫，並將應用程式原始程式碼從本機電腦推送至預備位置。 您也會使用您在上一個練習中建立的**Code First 移轉**來更新生產資料庫。 接著，您會在此測試環境中執行應用程式，以確認其作業是否正常。 一旦您滿意它是根據您的預期運作，就會將應用程式升階到生產環境。

> [!NOTE]
> 若要啟用分段發行，web 應用程式必須處於**標準模式**。 請注意，如果您將 web 應用程式變更為標準模式，將會產生額外的費用。 如需價格的詳細資訊，請參閱[App Service 定價](https://azure.microsoft.com/pricing/details/app-service/)。

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-web-app-in-azure-app-service"></a>工作1–在 Azure App Service 中建立 Web 應用程式

在這項工作中，您將會從管理入口網站的**Azure App Service**建立 web 應用程式。 您也會設定**SQL Database**來保存應用程式資料，以及設定原始檔控制的本機 Git 存放庫。

1. 前往[Azure 管理入口網站](https://manage.windowsazure.com)，並使用與您的訂用帳戶相關聯的 Microsoft 帳戶登入。

    ![登入 Azure 管理入口網站](maintainable-azure-websites-managing-change-and-scale/_static/image13.png)

    *登入 Azure 管理入口網站*
2. 在頁面底部的命令列中，按一下 [**新增**]。

    ![建立新的 web 應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "建立新的 web 應用程式")

    *建立新的 web 應用程式*
3. 依序按一下 [**計算**]、[**網站**] 和 [**自訂建立**]。

    ![使用自訂建立建立新的 web 應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "使用自訂建立建立新的 web 應用程式")

    *使用自訂建立建立新的 web 應用程式*
4. 在 [**新增網站-自訂建立**] 對話方塊中，提供可用的**URL** （例如*萬能技客-測驗*），在 [**區域**] 下拉式清單中選取一個位置，然後在 [**資料庫**] 下拉式清單中選取 [**建立新的 SQL database** ]。 最後，選取 [**從原始檔控制發行**] 核取方塊，然後按 **[下一步]** 。

    ![自訂新的 web 應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image16.png)

    *自訂新的 web 應用程式*
5. 指定資料庫設定的下列資訊：

   - 在 [**名稱**] 文字方塊中，輸入資料庫名稱（例如， *geekquiz\_db*）
   - 在 [伺服器]**下拉式**清單中，選取 [**新增 SQL database 伺服器**]。 或者，您也可以選取現有的伺服器。
   - 在 [**資料庫使用者名稱**] 和 [**資料庫密碼**] 方塊中，輸入 SQL Database 伺服器的系統管理員使用者名稱和密碼。 如果您選取已建立的伺服器，系統會提示您輸入密碼。

     ![指定資料庫設定](maintainable-azure-websites-managing-change-and-scale/_static/image17.png)

     *指定資料庫設定*
6. 按 [下一步] 以繼續。
7. 選取要使用之原始檔控制的**本機 Git 存放庫**，然後按 **[下一步]** 。

    > [!NOTE]
    > 系統可能會提示您輸入部署認證（使用者名稱和密碼）。

    ![建立 Git 存放庫](maintainable-azure-websites-managing-change-and-scale/_static/image18.png)

    *建立 Git 存放庫*
8. 等候新的 web 應用程式建立。

    > [!NOTE]
    > 根據預設，Azure 會在*azurewebsites.net*提供網域，但也可讓您使用 Azure 管理入口網站來設定自訂網域。 不過，如果您使用特定的 Azure App Service 模式，則只能管理自訂網域。
    >
    > Azure App Service 在免費、共用、基本、標準和 Premium 版本中都有提供。 在 [免費] 和 [共用] 模式中，所有 web 應用程式會在多租使用者環境中執行，並具有 CPU、記憶體和網路使用量的配額。 免費應用程式的最大數目可能會隨著您的方案而有所不同。 在標準模式中，您可以選擇哪些應用程式會在對應至標準 Azure 計算資源的專用虛擬機器上執行。 您可以在 web 應用程式的 [**調整**] 功能表中找到 web 應用程式模式設定。
    >
    > ![Azure App Service 模式](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service 模式")
    >
    > 如果您使用 [**共用**] 或 [**標準**] 模式，您將可以前往應用程式的 [**設定**] 功能表，然後按一下 [*功能變數名稱*] 底下的 [**管理網域**]，來管理 web 應用程式的自訂網域。
    >
    > ![管理網域](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "管理網域")
    >
    > ![管理自訂網域](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "管理自訂網域")
9. 建立 web 應用程式之後，請按一下 [ **URL** ] 資料行下方的連結，以檢查新的 web 應用程式是否正在執行。

    ![流覽至新的 web 應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image22.png)

    *流覽至新的 web 應用程式*

    ![web 應用程式正在執行](maintainable-azure-websites-managing-change-and-scale/_static/image23.png)

    *web 應用程式正在執行*

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-production-sql-database"></a>工作2–建立生產 SQL Database

在這項工作中，您將使用**Entity Framework Code First 移轉**建立以您在上一個工作中建立的**Azure SQL Database**實例為目標的資料庫。

1. 在 管理入口網站中，流覽至您在上一個工作中建立的 web 應用程式，並移至其**儀表板**。
2. 在 [**儀表板**] 頁面中，按一下 [**快速概覽**] 區段底下的 [**查看連接字串**] 連結。

    ![查看連接字串](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "查看連接字串")

    *查看連接字串*
3. 複製 [**連接字串**] 值，然後關閉對話方塊。

    ![Azure 管理入口網站中的連接字串](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Azure 管理入口網站中的連接字串")

    *Azure 管理入口網站中的連接字串*
4. 按一下 **[Sql 資料庫**] 以查看 Azure 中的 sql 資料庫清單

    ![SQL Database 功能表](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL Database 功能表")

    *SQL Database 功能表*
5. 找出您在上一項工作中建立的資料庫，然後按一下伺服器。

    ![SQL Database 伺服器](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL Database 伺服器")

    *SQL Database 伺服器*
6. 在伺服器的 [**快速入門**] 頁面中，按一下 [**設定**]。

    ![[設定] 功能表](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "[設定] 功能表")

    *[設定] 功能表*
7. 在 [**允許的 ip 位址**] 區段中，按一下 **[新增至允許的 ip 位址**] 連結，讓您的 ip 連線至 SQL Database 伺服器。

    ![允許的 IP 位址](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "允許的 IP 位址")

    *允許的 IP 位址*
8. 按一下頁面底部的 [儲存] 以完成此步驟。
9. 切換回 Visual Studio。
10. 在 [**套件管理員主控台**] 中，執行下列命令，以您從 Azure 複製的連接字串取代 *[您的連接字串]* 預留位置

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample10.ps1)]

    ![更新以 Windows 為目標的資料庫 Azure SQL Database](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "更新以 Windows 為目標的資料庫 Azure SQL Database")

    *更新資料庫目標 Azure SQL Database*

<a id="Ex2Task3"></a>
#### <a name="task-3--deploying-geek-quiz-to-staging-using-git"></a>工作 3-使用 Git 將萬能技客測驗部署至預備環境

在這項工作中，您會在 web 應用程式中啟用分段發行。 然後，您將使用 Git，直接從您的本機電腦將萬能技客測驗應用程式發佈到 web 應用程式的預備環境。

1. 返回入口網站，然後按一下 [**名稱**] 欄底下的 web 應用程式名稱，以顯示管理頁面。

    ![開啟 web 應用程式管理頁面](maintainable-azure-websites-managing-change-and-scale/_static/image31.png)

    *開啟 web 應用程式管理頁面*
2. 流覽至 [**調整**] 頁面。 在 [**一般**] 區段下，針對設定選取 [**標準**]，然後按一下命令列中的 [**儲存**]。

    > [!NOTE]
    > 若要以**標準**模式執行目前區域和訂用帳戶中的所有 web 應用程式，請保留 [**選擇網站**設定] 中的 [**全**選] 核取方塊。 否則，請清除 [**全選**] 核取方塊。

    ![將 web 應用程式升級至標準模式](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "將 web 應用程式升級至標準模式")

    *將 Web 應用程式升級至標準模式*
3. 按一下 **[是]** 以確認變更。

    ![確認變更為標準模式](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "繼續變更 web 應用程式模式")

    *確認變更為標準模式*
4. 移至 [**儀表板**] 頁面，然後按一下 [**快速概覽**] 區段下的 [**啟用分段發行**]。

    ![啟用分段發行](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "啟用分段發行")

    *啟用分段發行*
5. 按一下 **[是]** 啟用分段發行。

    ![確認分段發行](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "按一下 [是] 啟用分段發行")

    *確認分段發行*
6. 在 web 應用程式清單中，展開 web 應用程式名稱左側的標記，以顯示預備網站位置。 它具有您的 web 應用程式名稱，後面接著 ***（暫存）***。 按一下預備網站以移至 [管理] 頁面。

    ![流覽至預備 web 應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "流覽至預備 web 應用程式")

    *流覽至預備應用程式*
7. 請注意，他的管理頁面看起來就像任何其他 web 應用程式的管理頁面。 流覽至 [**部署**] 頁面，並複製 [ **Git URL** ] 值。 稍後在本練習中將會用到它。

    ![複製 Git URL 值](maintainable-azure-websites-managing-change-and-scale/_static/image37.png)

    *複製 Git URL 值*
8. 開啟新的**Git Bash**主控台，並執行下列命令。 以此實驗室的**Source\Ex1-DeployingWebSiteToStaging\Begin**資料夾中**GeekQuiz**解決方案的路徑，更新 *[您的應用程式-路徑]* 預留位置。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample11.cmd)]

    ![Git 初始化和第一次認可](maintainable-azure-websites-managing-change-and-scale/_static/image38.png)

    *Git 初始化和第一次認可*
9. 執行下列命令，將您的 web 應用程式推送至遠端**Git**存放庫。 將預留位置取代為您從管理入口網站取得的 URL。 系統會提示您輸入您的部署密碼。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample12.cmd)]

    ![推送至 Windows Azure](maintainable-azure-websites-managing-change-and-scale/_static/image39.png)

    *推送至 Azure*

    > [!NOTE]
    > 當您將內容部署至 web 應用程式的 FTP 主機或 GIT 存放庫時，必須使用您從 web 應用程式的 [**快速入門**] 或 [**儀表板**] 管理頁面建立的**部署**認證來進行驗證。 如果您不知道您的部署認證，可以使用入口網站輕鬆地將其重設。 開啟 web 應用程式的 [**儀表板**] 頁面，然後按一下 [**重設您的部署認證**] 連結。 提供新密碼，然後按一下 **[確定]** 。 部署認證適用于與您的訂用帳戶相關聯的所有 web 應用程式。
10. 若要確認 web 應用程式已成功推送至 Azure，請回到入口網站，然後按一下 [**網站**]。
11. 找出您的 web 應用程式，並展開該專案以顯示預備網站位置。 按一下其**名稱**，以移至 [管理] 頁面。
12. 按一下 [**部署**] 以查看**部署歷程記錄**。 確認有使用中的**部署**與您的 *&quot;初始認可&quot;* 。

    ![作用中的部署](maintainable-azure-websites-managing-change-and-scale/_static/image40.png)

    *作用中的部署*
13. 最後，按一下命令列中的 **[流覽]** 以移至 web 應用程式。

    ![流覽 web 應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image41.png)

    *流覽 web 應用程式*
14. 如果已成功部署應用程式，您會看到萬能技客測驗登入頁面。

    > [!NOTE]
    > 已部署應用程式的位址 URL 包含您的 web 應用程式名稱，後面接著 *-預備*。

    ![在預備環境中執行的應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image42.png)

    *在預備環境中執行的應用程式*
15. 如果您想要探索應用程式，請按一下 [**註冊**] 來註冊新的使用者。 輸入使用者名稱、電子郵件地址和密碼，以完成帳戶詳細資料。 接下來，應用程式會顯示測驗的第一個問題。 請回答幾個問題，確定它如預期般運作。

    ![已備妥可供使用的應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image43.png)

    *已備妥可供使用的應用程式*

<a id="Ex2Task4"></a>
#### <a name="task-4--promoting-the-web-app-to-production"></a>工作 4-將 Web 應用程式升級至生產環境

現在您已確認 web 應用程式在預備環境中正常運作，您已準備好將它升級至生產環境。 在這項工作中，您會將預備網站位置與生產網站位置交換。

1. 返回入口網站，然後選取 [預備網站] 位置。 按一下命令列中的 [**交換**]。

    ![交換至生產環境](maintainable-azure-websites-managing-change-and-scale/_static/image44.png)

    *交換至生產環境*
2. 在確認對話方塊中按一下 **[是]** ，繼續進行交換操作。 Azure 會立即將生產網站的內容與預備網站的內容交換。

    > [!NOTE]
    > 預備版本的某些設定會自動複製到實際執行版本（例如連接字串覆寫、處理常式對應等），但其他設定不會變更（例如 DNS 端點、SSL 系結等）。

    ![正在確認交換操作](maintainable-azure-websites-managing-change-and-scale/_static/image45.png)

    *正在確認交換操作*
3. 一旦交換完成，請選取生產位置，然後按一下命令列中的 **[流覽]** 以開啟生產網站。 請注意網址列中的 URL。

    > [!NOTE]
    > 您可能需要重新整理瀏覽器以清除快取。 在 Internet Explorer 中，您可以按下**CTRL + R**來執行此動作。

    ![在生產環境中執行的 Web 應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image46.png)
4. 在**GitBash**主控台中，將本機 Git 存放庫的遠端 URL 更新為目標為生產位置。 若要執行這項操作，請執行下列命令，將預留位置取代為您的部署使用者名稱和 web 應用程式的名稱。

    > [!NOTE]
    > 在下列練習中，您會將變更推送至生產網站，而不是暫存，只是為了實驗室的簡單性。 在真實世界的案例中，建議您先確認預備環境中的變更，再升級至生產環境。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample13.cmd)]

<a id="Exercise3"></a>
### <a name="exercise-3-performing-deployment-rollback-in-production"></a>練習3：在生產環境中執行部署復原

在某些情況下，您沒有預備位置可在預備與生產環境之間執行熱交換，例如，如果您使用的是**免費**或**共用**模式。 在這些情況下，您應該在測試環境（本機或遠端網站）中測試您的應用程式，然後再部署到生產環境。 不過，在測試階段期間未偵測到的問題可能會在生產網站中發生。 在此情況下，請務必讓機制輕鬆地儘快切換至先前和更穩定的應用程式版本。

在**Azure App Service**中，從原始檔控制進行連續部署，可能會因為管理入口網站中提供的重新**部署**動作而產生這種情況。 Azure 會持續追蹤與推送至存放庫的認可相關聯的部署，並提供選項讓您隨時使用任何先前的部署重新部署應用程式。

在此練習中，您將對**萬能技客測驗**應用程式中刻意插入*bug*的程式碼進行變更。 您會將應用程式部署至生產環境以查看錯誤，然後您將會利用重新部署功能來回到先前的狀態。

<a id="Ex3Task1"></a>
#### <a name="task-1--updating-the-geek-quiz-application"></a>工作1–更新萬能技客測驗應用程式

在這項工作中，您將重構**TriviaController**類別的一小段程式碼，將從資料庫中取出所選測驗選項的部分，解壓縮到新的方法中。

1. 使用上一個練習中的**GeekQuiz**解決方案，切換到 Visual Studio 實例。
2. 在**方案總管**中，開啟 [**控制器**] 資料夾內的**TriviaController.cs**檔案。
3. 找出**StoreAsync**方法，並選取下圖中反白顯示的程式碼。

    ![選取程式碼](maintainable-azure-websites-managing-change-and-scale/_static/image47.png)

    *選取程式碼*
4. 以滑鼠右鍵按一下選取的程式碼，展開 [**重構**] 功能表，然後選取 [**解壓縮方法**...]。

    ![將程式碼解壓縮為新方法](maintainable-azure-websites-managing-change-and-scale/_static/image48.png)

    *選取 [解壓縮方法]*
5. 在 [**解壓縮方法**] 對話方塊中，將新的方法命名為*MatchesOption* ，然後按一下 **[確定]** 。

    ![指定方法名稱](maintainable-azure-websites-managing-change-and-scale/_static/image49.png)

    *指定已解壓縮方法的名稱*
6. 然後會將選取的程式碼解壓縮至**MatchesOption**方法。 產生的程式碼會顯示在下列程式碼片段中。

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample14.cs)]
7. 按**CTRL + S**儲存變更。

<a id="Ex3Task2"></a>
#### <a name="task-2--redeploying-the-geek-quiz-application"></a>工作 2-重新部署萬能技客測驗應用程式

您現在會將您在上一個工作中所做的變更推送至存放庫，這會觸發生產環境的新部署。 接著，您將使用 Internet Explorer 提供的**F12 開發工具**來疑難排解問題，然後從 Azure 管理入口網站執行復原至先前的部署。

1. 開啟新的**Git Bash**主控台，將更新過的應用程式部署至 Azure App Service。
2. 執行下列命令，將變更推送至 Azure。 以**GeekQuiz**方案的路徑更新 *[您的應用程式-路徑]* 預留位置。 系統會提示您輸入您的部署密碼。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample15.cmd)]

    ![將重構的程式碼推送至 Azure](maintainable-azure-websites-managing-change-and-scale/_static/image50.png)

    *將重構的程式碼推送至 Azure*
3. 開啟 Internet Explorer 並流覽至您的 web 應用程式（例如 `http://<your-web-site>.azurewebsites.net`）。 使用先前建立的認證登入。
4. 按**F12**啟動開發工具，選取 [**網路**] 索引標籤，然後按一下 [**播放**] 按鈕以開始錄製。

    ![正在啟動網路錄製](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "正在啟動網路錄製")

    *正在啟動網路錄製*
5. 選取測驗的任何選項。 您會看到不會發生任何事。
6. 在**F12**視窗中，與 POST HTTP 要求對應的專案會顯示 HTTP **500**結果。

    ![HTTP 500 錯誤](maintainable-azure-websites-managing-change-and-scale/_static/image52.png)

    *HTTP 500 錯誤*
7. 選取 [**主控台**] 索引標籤。會記錄錯誤的詳細資料。

    ![記錄的錯誤](maintainable-azure-websites-managing-change-and-scale/_static/image53.png)

    *記錄的錯誤*
8. 找出錯誤的詳細資料部分。 很明顯地，此錯誤是由您在先前步驟中認可的程式碼重構所造成。

    `Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`
9. 請勿關閉瀏覽器。
10. 在新的瀏覽器實例中，流覽至[Azure 管理入口網站](https://manage.windowsazure.com)，然後使用與您的訂用帳戶相關聯的 Microsoft 帳戶登入。
11. 選取 [**網站**]，然後按一下您在練習2中建立的 web 應用程式。
12. 流覽至 [**部署**] 頁面。 請注意，所有執行的認可都會列在部署歷程記錄中。

    ![現有部署的清單](maintainable-azure-websites-managing-change-and-scale/_static/image54.png)

    *現有部署的清單*
13. 選取先前的認可，然後按一下命令列上的 [重新**部署**]。

    ![重新部署先前的認可](maintainable-azure-websites-managing-change-and-scale/_static/image55.png)

    *重新部署先前的認可*
14. 在系統提示您確認時，按一下 [Yes](是)。

    ![確認重新部署](maintainable-azure-websites-managing-change-and-scale/_static/image56.png)
15. 當部署完成時，使用您的 web 應用程式切換回瀏覽器實例，然後按下**CTRL + F5**。
16. 按一下任何一個選項。 現在會進行翻轉動畫，並顯示結果（*正確/不正確*）。
17. 選擇性切換至**Git Bash**主控台並執行下列命令，以還原為先前的認可。

    > [!NOTE]
    > 這些命令會建立新的認可，以復原在錯誤認可中所做的 Git 儲存機制中的所有變更。 然後，Azure 會使用新的認可來重新部署應用程式。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample16.cmd)]

<a id="Exercise4"></a>
### <a name="exercise-4-scaling-using-azure-storage"></a>練習4：使用 Azure 儲存體進行調整

**Blob**是儲存大量非結構化文字或二進位資料（例如影片、音訊和影像）的最簡單方式。 將應用程式的靜態內容移至儲存體，可透過將影像或檔直接提供給瀏覽器，協助調整您的應用程式。

在此練習中，您會將應用程式的靜態內容移至 Blob 容器。 然後，您會將應用程式設定為**在 web.config 中**新增**ASP.NET URL 重寫規則**，以將您的內容重新導向至 Blob 容器。

<a id="Ex4Task1"></a>
#### <a name="task-1--creating-an-azure-storage-account"></a>工作1–建立 Azure 儲存體帳戶

在這項工作中，您將瞭解如何使用入口網站來建立新的儲存體帳戶。

1. 流覽至[Azure 管理入口網站](https://manage.windowsazure.com)，並使用與您的訂用帳戶相關聯的 Microsoft 帳戶進行登入。
2. 選取 [**新增] |資料服務 |儲存體 |[快速建立**] 以開始建立新的儲存體帳戶。 輸入帳戶的唯一名稱，並從清單中選取一個**區域**。 按一下 [**建立儲存體帳戶**] 以繼續。

    ![建立新的儲存體帳戶](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "建立新的儲存體帳戶")

    *建立新的儲存體帳戶*
3. 在 [**儲存體**] 區段中，等候新儲存體帳戶的狀態變更為 [*線上*]，才能繼續進行下列步驟。

    ![已建立儲存體帳戶](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "已建立儲存體帳戶")

    *已建立儲存體帳戶*
4. 按一下儲存體帳戶名稱，然後按一下頁面頂端的 [**儀表板**] 連結。 [**儀表板**] 頁面會提供帳戶狀態的相關資訊，以及可在應用程式中使用的服務端點。

    ![顯示儲存體帳戶儀表板](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "顯示儲存體帳戶儀表板")

    *顯示儲存體帳戶儀表板*
5. 按一下巡覽列中的 [**管理存取金鑰**] 按鈕。

    ![[管理存取金鑰] 按鈕](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "[管理存取金鑰] 按鈕")

    *[管理存取金鑰] 按鈕*
6. 在 [**管理存取金鑰**] 對話方塊中，複製 [**儲存體帳戶名稱**] 和 [**主要存取金鑰**]，因為您在下列練習中將會用到它們。 然後關閉對話方塊。

    ![[管理存取金鑰] 對話方塊](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "[管理存取金鑰] 對話方塊")

    *[管理存取金鑰] 對話方塊*

<a id="Ex4Task2"></a>
#### <a name="task-2--uploading-an-asset-to-azure-blob-storage"></a>工作 2-將資產上傳至 Azure Blob 儲存體

在這項工作中，您將使用 Visual Studio 的 [伺服器總管] 視窗連接到您的儲存體帳戶。 接著，您將建立 blob 容器，並將具有萬能技客測驗標誌的檔案上傳至容器。

1. 使用上一個練習中的**GeekQuiz**解決方案，切換到 Visual Studio 實例。
2. 從功能表列中選取 [ **View** ]，然後按一下 [**伺服器總管**]。
3. 在**伺服器總管**中，以滑鼠右鍵按一下 [ **Azure** ] 節點，然後選取 **[連線到 azure ...]** 。使用與您的訂用帳戶相關聯的 Microsoft 帳戶進行登入。

    ![連接至 Windows Azure](maintainable-azure-websites-managing-change-and-scale/_static/image62.png)

    *連接到 Azure*
4. 展開 [ **Azure** ] 節點，以滑鼠右鍵按一下 [**儲存體**]，然後選取 [**附加外部儲存體**]。
5. 在 [**加入新的儲存體帳戶**] 對話方塊中，輸入您在上一個工作中取得的**帳戶名稱**和**帳戶金鑰**，然後按一下 **[確定]** 。

    ![[新增儲存體帳戶] 對話方塊](maintainable-azure-websites-managing-change-and-scale/_static/image63.png)

    *[新增儲存體帳戶] 對話方塊*
6. 您的儲存體帳戶應該會出現在 [**儲存體**] 節點底下。 展開您的儲存體帳戶，以滑鼠右鍵按一下 [ **blob** ]，然後選取 [**建立 Blob 容器**]。

    ![建立 Blob 容器](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "建立 Blob 容器")

    *建立 Blob 容器*
7. 在 [**建立 Blob 容器**] 對話方塊中，輸入 Blob 容器的名稱，然後按一下 **[確定]** 。

    ![[建立 Blob 容器] 對話方塊](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "[建立 Blob 容器] 對話方塊")

    *[建立 Blob 容器] 對話方塊*
8. 新的 blob 容器應新增至 [ **blob** ] 節點。 變更容器中的存取權限，使容器成為公用。 若要這麼做，請以滑鼠右鍵按一下 [ **images** ] 容器，然後選取 [**屬性**]。

    ![images 容器屬性](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "images 容器屬性")

    *Images 容器屬性*
9. 在 [**屬性**] 視窗中，將 [**公用讀取權限**] 設定為 [**容器**]。

    ![變更公用讀取權限屬性](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "變更公用讀取權限屬性")

    *變更公用讀取權限屬性*
10. 當系統提示您是否確定要變更 [公用存取] 屬性時，請按一下 **[是]** 。

    ![Microsoft Visual Studio 警告](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio 警告")

    *Microsoft Visual Studio 警告*
11. 在**伺服器總管**中，以滑鼠右鍵按一下**images** blob 容器，然後選取 [ **View blob container**]。

    ![View Blob 容器](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "View Blob 容器")

    *View Blob 容器*
12. [Images] 容器應該會在新視窗中開啟，而且應該不會顯示任何專案的圖例。 按一下 [**上傳**] 圖示，將檔案上傳至 blob 容器。

    ![沒有專案的 Images 容器](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "沒有專案的 Images 容器")

    *沒有專案的 Images 容器*
13. 在 [**上傳 Blob** ] 對話方塊中，流覽至實驗室的 [**資產**] 資料夾。 選取 [ **logo-big** ] 檔案，然後按一下 [**開啟**]。
14. 等候檔案上傳。 當上傳完成時，檔案應該會列在 images 容器中。 以滑鼠右鍵按一下檔案專案，然後選取 [**複製 URL**]。

    ![複製 blob URL](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "複製 blob 檔案 URL")

    *複製 blob URL*
15. 開啟 Internet Explorer 並貼上 URL。 下列影像應該會顯示在瀏覽器中。

    ![從 Windows Blob 儲存體 logo-big .png 影像](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "從儲存體 logo-big .png 影像")

    *從 Azure Blob 儲存體 logo-big .png 影像*

<a id="Ex4Task3"></a>
#### <a name="task-3--updating-the-solution-to-consume-static-content-from-azure-blob-storage"></a>工作 3-更新解決方案以取用 Azure Blob 儲存體的靜態內容

在這項工作中，您會在**web.config**檔案中新增 ASP.NET URL 重寫規則，以將**GeekQuiz**解決方案設定為使用上傳至 Azure Blob 儲存體（而不是位於 web 應用程式中的影像）。

1. 在 Visual Studio 中，開啟**GeekQuiz**專案**內的 web.config**檔案，並找出 **&lt;system.webserver&gt;** 元素。
2. 新增下列程式碼，以新增 URL 重寫規則，並使用您的儲存體帳戶名稱來更新預留位置。

    （程式碼片段- *WebSitesInProduction-Ex4-UrlRewriteRule*）

    [!code-xml[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample17.xml)]

    > [!NOTE]
    > URL 重寫程式會攔截傳入的 Web 要求，並將要求重新導向至不同的資源。 URL 重寫規則會在要求需要重新導向時，告訴重寫引擎，以及應重新導向的位置。 重寫規則是由兩個字串所組成：在要求的 URL 中尋找的模式（通常是使用正則運算式），以及用來取代模式的字串（如果找到的話）。 如需詳細資訊，請參閱[ASP.NET 中的 URL 重寫](https://msdn.microsoft.com/library/ms972974.aspx)。
3. 按**CTRL + S**儲存變更。
4. 開啟新的**Git Bash**主控台，將更新過的應用程式部署至 Azure App Service。
5. 執行下列命令，將變更推送至 Azure。 以**GeekQuiz**方案的路徑更新 *[您的應用程式-路徑]* 預留位置。 系統會提示您輸入您的部署密碼。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample18.cmd)]

    ![將更新部署至 Azure](maintainable-azure-websites-managing-change-and-scale/_static/image73.png)

    *將更新部署至 Azure*

<a id="Ex4Task4"></a>
#### <a name="task-4--verification"></a>工作4–驗證

在這項工作中，您將使用**Internet Explorer**流覽**萬能技客測驗**應用程式，並檢查影像的 URL 重寫規則是否正常運作，並將您重新導向至**Azure Blob 儲存體**上主控的映射。

1. 開啟 Internet Explorer 並流覽至您的 web 應用程式（例如 `http://<your-web-site>.azurewebsites.net`）。 使用先前建立的認證登入。

    ![以影像顯示萬能技客測驗 web 應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "以影像顯示萬能技客測驗 web 應用程式")

    *以影像顯示萬能技客測驗 web 應用程式*
2. 按**F12**啟動開發工具，選取 [**網路**] 索引標籤，然後開始錄製。

    ![正在啟動網路錄製](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "正在啟動網路錄製")

    *正在啟動網路錄製*
3. 按**CTRL + F5**以重新整理網頁。
4. 網頁完成載入之後，您應該會看到 **/Img/logo-big.png** URL 的 HTTP 要求，其中包含 HTTP **301**結果（重新導向），以及另一個 `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` URL 的要求與 HTTP **200**結果。

    ![驗證 URL 重新導向](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "在開發人員工具中顯示重新導向")

    *驗證 URL 重新導向*

<a id="Exercise5"></a>
### <a name="exercise-5-using-autoscale-for-web-apps"></a>練習5：針對 Web Apps 使用自動調整

> [!NOTE]
> 此練習是選擇性的，因為它需要支援 Web 負載 &amp; 效能測試，這僅適用于**Visual Studio 2013 旗艦版**。 如需特定 Visual Studio 2013 功能的詳細資訊，請比較[這裡](https://www.microsoft.com/visualstudio/eng/products/compare)的版本。

**Azure App Service Web Apps**會針對以**標準模式**執行的 Web 應用程式提供自動調整功能。 自動調整可讓 Azure 根據負載，自動調整 web 應用程式的實例計數。 啟用自動調整時，Azure 每隔五分鐘會檢查一次 web 應用程式的 CPU，並視需要在該時間點新增實例。 如果 CPU 使用率很低，Azure 會每隔兩個小時移除實例一次，以確保 web 應用程式的效能不會降低。

在此練習中，您將逐步完成為**萬能技客測驗**web 應用程式設定**自動**調整功能所需的步驟。 您將執行 Visual Studio 負載測試，以在應用程式上產生足夠的 CPU 負載來觸發實例升級，以驗證這項功能。

<a id="Ex5Task1"></a>
#### <a name="task-1--configuring-autoscale-based-on-the-cpu-metric"></a>工作1–根據 CPU 度量設定自動調整

在這項工作中，您將使用 Azure 管理入口網站，為您在練習2中建立的 web 應用程式啟用自動調整功能。

1. 在[Azure 管理入口網站](https://manage.windowsazure.com/)中，選取 [**網站**]，然後按一下您在練習2中建立的 web 應用程式。
2. 流覽至 [**調整**] 頁面。 在 [**容量**] 區段下，選取 [**依度量調整規模**] 設定的 [ **CPU** ]。

    > [!NOTE]
    > 依 CPU 進行調整時，Azure 會在 CPU 使用量變更時，動態調整應用程式所使用的實例數目。

    ![選取以根據 CPU 調整規模](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "選取自動調整的 CPU 度量")

    *選取以根據 CPU 調整規模*
3. 將**目標 CPU 設定**變更為**20**-**40** %。

    > [!NOTE]
    > 此範圍代表 web 應用程式的平均 CPU 使用量。 Azure 將會新增或移除實例，以將您的 web 應用程式保留在此範圍內。 用於調整的實例數目下限和上限是在 [**實例計數**] 設定中指定。 Azure 永遠不會超出該限制。
    >
    > 預設的**目標 CPU**值只會針對此實驗室的目的而修改。 藉由將 CPU 範圍設定為較小的值，您會增加在應用程式上放置中等負載時觸發自動調整的機會。

    ![將目標 CPU 變更為介於20到40% 之間](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "將目標 CPU 變更為介於20到40% 之間")

    *將目標 CPU 變更為介於20到40% 之間*
4. 按一下命令列中的 [**儲存**] 以儲存變更。

<a id="Ex5Task2"></a>
#### <a name="task-2--load-testing-with-visual-studio"></a>工作2–使用 Visual Studio 進行負載測試

現在已設定**自動**調整，您將在 Visual Studio 中建立**Web 效能和負載測試專案**，以在您的 Web 應用程式上產生一些 CPU 負載。

1. 開啟**Visual Studio Ultimate 2013**並選取 [檔案] **|新增 |專案 ...** 以啟動新的解決方案。

    ![建立新專案](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "建立新專案")

    *建立新專案*
2. 在 [**新增專案**] 對話方塊中，選取視覺效果  **C#底下的 [Web 效能和負載測試專案] |[測試**] 索引標籤。請確定已選取 **.NET Framework 4.5** ，將專案命名為*WebAndLoadTestProject*，選擇**位置**，然後按一下 **[確定]** 。

    ![建立新的 Web 和負載測試專案](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "建立新的 Web 和負載測試專案")

    *建立新的 Web 和負載測試專案*
3. 在 [ **webtest1.webtest] webtest**中，以滑鼠右鍵按一下**webtest1.webtest**節點，然後按一下 [**新增要求**]。

    ![將要求新增至 Webtest1.webtest](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "將要求新增至 Webtest1.webtest")

    *將要求新增至 Webtest1.webtest*
4. 在 [新增要求] 節點的 [**屬性**] 視窗中，更新 [ **url** ] 屬性以指向 WEB 應用程式的 url （例如 *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)* ）。

    ![變更 Url 屬性](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "變更 Url 屬性")

    *變更 Url 屬性*
5. 在 [ **webtest1.webtest webtest** ] 視窗中，以滑鼠右鍵按一下**webtest1.webtest** ，然後按一下 [**新增迴圈**]。

    ![將迴圈新增至 Webtest1.webtest](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "將迴圈新增至 Webtest1.webtest")

    *將迴圈新增至 Webtest1.webtest*
6. 在 [**加入條件式規則和要迴圈的專案**] 對話方塊中，選取 [ **For 迴圈**] 規則，並修改下列屬性。

   1. **終止值：** 1000
   2. **內容參數名稱：** 定位
   3. **遞增值：** 1

      ![選取「For 迴圈」規則並更新屬性](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "選取「For 迴圈」規則並更新屬性")

      *選取「For 迴圈」規則並更新屬性*
7. 在 [**迴圈中的專案**] 區段下，選取您先前建立的要求做為迴圈的第一個和最後一個專案。 按一下 [確定] 繼續操作。

    ![選取迴圈的第一個和最後一個專案](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "選取迴圈的第一個和最後一個專案")

    *選取迴圈的第一個和最後一個專案*
8. 在**方案總管**中，以滑鼠右鍵按一下**WebAndLoadTestProject**專案，展開 [**新增**] 功能表，然後選取 [**負載測試 ...** ]。

    ![將負載測試加入至 WebAndLoadTestProject 專案](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "將負載測試加入至 WebAndLoadTestProject 專案")

    *將負載測試加入至 WebAndLoadTestProject 專案*
9. 在 [**新增負載測試精靈**] 對話方塊中，按 **[下一步**]。

    ![新增負載測試精靈](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "新增負載測試精靈")

    *新增負載測試精靈*
10. 在 [**案例**] 頁面中，選取 [不**使用考慮時間**]，然後按 **[下一步]** 。

    ![選取不使用考慮時間](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "選取不使用考慮時間")

    *選取不使用考慮時間*
11. 在 [**負載模式**] 頁面中，確認已選取 [**常數載入**] 選項。 將 [**使用者計數**] 設定變更為**250**個使用者，然後按 **[下一步]** 。

    ![將使用者計數變更為250](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "將使用者計數變更為250")

    *將使用者計數變更為250*
12. 在 [**測試混合模型**] 頁面中，選取 [**根據順序測試順序**]，然後按 **[下一步]** 。

    ![選取測試混合模型](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "選取測試混合模型")

    *選取測試混合模型*
13. 在 [**測試混合模型**] 頁面中，按一下 [**加入**]，將測試加入至混合。

    ![將測試加入至測試混合](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "將測試加入至測試混合")

    *將測試加入至測試混合*
14. 在 [**加入測試**] 對話方塊中，按兩下 [ **webtest1.webtest** ]，將測試加入至 [**選取的測試**] 清單。 按一下 [確定] 繼續操作。

    ![新增 Webtest1.webtest 測試](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "新增 Webtest1.webtest 測試")

    *新增 Webtest1.webtest 測試*
15. 回到 [**測試混合**] 頁面，按 **[下一步]** 。

    ![正在完成測試混合頁面](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "正在完成測試混合頁面")

    *正在完成測試混合頁面*
16. 在 [**網路混合**] 頁面上，按 **[下一步]** 。

    ![在 [網路混合] 頁面中按一下 [下一步]](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "在 [網路混合] 頁面中按一下 [下一步]")

    *在 [網路混合] 頁面中按一下 [下一步]*
17. 在 [**瀏覽器混合**] 頁面中，選取**Internet Explorer 10.0**作為瀏覽器類型，然後按 **[下一步]** 。

    ![選取瀏覽器類型](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "選取瀏覽器類型")

    *選取瀏覽器類型*
18. 在 [**計數器集合**] 頁面上，按 **[下一步]** 。

    ![按一下 [計數器集合] 頁面中的 [下一步]](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "按一下 [計數器集合] 頁面中的 [下一步]")

    *按一下 [計數器集合] 頁面中的 [下一步]*
19. 在 [回合**設定**] 頁面上，將**負載測試持續時間**設定為**5 分鐘**，然後按一下 **[完成]** 。

    ![將負載測試持續時間設定為5分鐘](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "將負載測試持續時間設定為5分鐘")

    *將負載測試持續時間設定為5分鐘*
20. 在**方案總管**中，按兩下本機的**配置**檔案，以流覽測試設定。 根據預設，Visual Studio 會使用您的本機電腦來執行測試。

    > [!NOTE]
    > 或者，您可以使用**Azure Test Plans**，將您的測試專案設定為在雲端中執行負載測試。 Azure Test Plans 提供以雲端為基礎的負載測試服務，可模擬更實際的負載，避免像是 CPU 容量、可用記憶體和網路頻寬等本機環境的條件約束。 如需使用 Azure Test Plans 執行負載測試的詳細資訊，請參閱[負載測試案例](/azure/devops/test/load-test/overview?view=vsts)。

    ![測試設定](maintainable-azure-websites-managing-change-and-scale/_static/image98.png)

<a id="Ex5Task3"></a>
#### <a name="task-3--autoscale-verification"></a>工作 3-自動調整驗證

您現在會執行您在上一項工作中建立的負載測試，並查看您的 web 應用程式在負載下的行為。

1. 在**方案總管**中，按兩下**loadtest1.loadtest loadtest**以開啟負載測試。

    ![開啟 Loadtest1.loadtest。 loadtest](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "開啟 Loadtest1.loadtest。 loadtest")

    *開啟 Loadtest1.loadtest。 loadtest*
2. 在 [ **loadtest1.loadtest loadtest** ] 視窗中，按一下 [工具箱] 中的第一個按鈕以執行負載測試。

    ![執行負載測試](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "執行負載測試")

    *執行負載測試*
3. 等待負載測試完成。

    > [!NOTE]
    > 負載測試會模擬多個將要求同時傳送至 web 應用程式的使用者。 當測試正在執行時，您可以監視可用的計數器，以偵測任何與負載測試回合相關的錯誤、警告或其他資訊。

    ![負載測試正在執行](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "等待負載測試完成")

    *負載測試正在執行*
4. 測試完成之後，請回到入口網站，並流覽至 web 應用程式的 [**調整規模**] 頁面。 在 [**容量**] 區段下，您應該會在圖表中看到新實例已自動部署。

    ![已自動部署新的實例](maintainable-azure-websites-managing-change-and-scale/_static/image102.png)

    *已自動部署新的實例*

    > [!NOTE]
    > 可能需要幾分鐘的時間，變更才會出現在圖形中（請定期按**CTRL + F5**以重新整理頁面）。 如果您看不到任何變更，可以嘗試下列動作：
    >
    > - 增加負載測試的持續時間（例如**10 分鐘**）
    > - 在 web 應用程式的自動調整規模設定中，減少**目標 CPU**範圍的最大值和最小值
    > - 使用**Azure Test Plans**在雲端中執行負載測試。 如需詳細資訊，請參閱[這裡](/azure/devops/test/load-test/index?view=vsts)。

---

<a id="Summary"></a>
## <a name="summary"></a>總結

在此實際操作實驗室中，您已瞭解如何在 Azure 中設定應用程式，並將其部署至生產 web 應用程式。 您一開始會使用**Entity Framework Code First 移轉**來偵測及更新您的資料庫，然後繼續使用**Git**部署新版本的網站，並執行復原至網站的最新穩定版本。 此外，您已瞭解如何使用儲存體來調整您的應用程式，以將您的靜態內容移至 Blob 容器。
