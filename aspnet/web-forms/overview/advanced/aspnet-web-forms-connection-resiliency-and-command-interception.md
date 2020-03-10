---
uid: web-forms/overview/advanced/aspnet-web-forms-connection-resiliency-and-command-interception
title: ASP.NET Web Forms 連線恢復功能和命令攔截 |Microsoft Docs
author: Erikre
description: 本教學課程說明如何修改範例應用程式，以支援連接恢復功能和命令攔截。
ms.author: riande
ms.date: 03/31/2014
ms.assetid: 6d497001-fa80-4765-b4cc-181fe90b894e
msc.legacyurl: /web-forms/overview/advanced/aspnet-web-forms-connection-resiliency-and-command-interception
msc.type: authoredcontent
ms.openlocfilehash: 95f0b5635c12d5ef88622e5766c1278c6570dd4d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598424"
---
# <a name="aspnet-web-forms-connection-resiliency-and-command-interception"></a>ASP.NET Web Form 連線恢復功能與命令攔截

依[Erik Reitan](https://github.com/Erikre)

在本教學課程中，您將修改 Wingtip 玩具範例應用程式，以支援連接恢復功能和命令攔截。 藉由啟用連線恢復功能，Wingtip 玩具範例應用程式會在雲端環境的暫時性錯誤發生時，自動重試資料呼叫。 此外，藉由執行命令攔截，Wingtip 玩具範例應用程式會攔截所有傳送至資料庫的 SQL 查詢，以便記錄或變更它們。

> [!NOTE] 
> 
> 這個 Web Forms 教學課程是以 Tom 作者: dykstra 的下列 MVC 教學課程為基礎：  
> [在 ASP.NET MVC 應用程式中使用 Entity Framework 的連接恢復功能和命令攔截](../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="what-youll-learn"></a>您將學到什麼：

- 如何提供連接恢復功能。
- 如何執行命令攔截。

## <a name="prerequisites"></a>Prerequisites

開始之前，請確定您的電腦上已安裝下列軟體：

- [適用于 Web 的](https://www.microsoft.com/visualstudio/11/downloads#express-web) [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)或 Microsoft Visual Studio Express 2013。 .NET Framework 會自動安裝。
- Wingtip 玩具範例專案，讓您可以在 Wingtip 玩具專案中執行本教學課程中所述的功能。 下列連結提供下載詳細資料：

    - [使用 ASP.NET 4.5.1 Web Forms 的消費者入門-Wingtip 玩具](https://go.microsoft.com/fwlink/?LinkID=389434&amp;clcid=0x409)（C#）
- 完成本教學課程之前，請考慮[使用 ASP.NET 4.5 Web form 和 Visual Studio 2013](../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)，來檢查相關的教學課程系列消費者入門。 本教學課程系列將協助您熟悉**WingtipToys**專案和程式碼。

## <a name="connection-resiliency"></a>連線恢復功能

當您考慮將應用程式部署到 Windows Azure 時，其中一個考慮選項是將資料庫部署到**windows** **Azure SQL Database**雲端資料庫服務。 當您連線到雲端資料庫服務時，如果您的 web 伺服器和資料庫伺服器在相同的資料中心內直接連接在一起，通常會更常遇到暫時性連接錯誤。 即使雲端 web 伺服器和雲端資料庫服務裝載于相同的資料中心，它們之間還是有更多的網路連線可能會發生問題，例如負載平衡器。

此外，雲端服務通常會由其他使用者共用，這表示其回應性可能會受到影響。 而且您對資料庫的存取權可能會受到節流。 「節流」表示當您嘗試存取時，資料庫服務會擲回例外狀況，而不是*服務等級協定*（SLA）中允許的頻率。

當您存取雲端服務時所發生的許多或大部分連線問題都是暫時性的，也就是說，它們會在短時間內自行解決。 因此，當您嘗試資料庫作業並取得通常是暫時性的錯誤類型時，您可以在短暫等候之後再次嘗試操作，而且作業可能會成功。 如果您藉由自動重試來處理暫時性錯誤，您可以為使用者提供更好的體驗，讓客戶無法看到大部分的情況。 Entity Framework 6 中的連接復原功能會將重試失敗 SQL 查詢的程式自動化。

您必須針對特定的資料庫服務，適當地設定連接復原功能：

1. 它必須知道可能是暫時性的例外狀況。 例如，您想要重試因網路連線暫時中斷而造成的錯誤，而不是程式 bug 所造成的錯誤。
2. 它必須在失敗的作業重試之間等候一段適當的時間。 您可以在批次進程的重試之間等候較長的時間，而不是使用者正在等候回應的線上網頁。
3. 它必須先重試適當的次數，才會放棄。 您可能想要在您于線上應用程式中的批次進程中，重試更多次。

您可以針對 Entity Framework 提供者所支援的任何資料庫環境，手動設定這些設定。

您只需要在元件中建立衍生自 `DbConfiguration` 類別的類別，並在該類別中設定 SQL Database 執行策略，而在 Entity Framework 是重試原則的另一個詞彙。

### <a name="implementing-connection-resiliency"></a>執行連接復原

1. 下載並開啟 Visual Studio 中的[WingtipToys](https://go.microsoft.com/fwlink/?LinkID=389434&amp;clcid=0x409)範例 Web Forms 應用程式。
2. 在**WingtipToys**應用程式的*邏輯*資料夾中，新增名為*WingtipToysConfiguration.cs*的類別檔案。
3. 將現有的程式碼更換成下列程式碼：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample1.cs)]

Entity Framework 會自動執行它在衍生自 `DbConfiguration`的類別中找到的程式碼。 您可以使用 `DbConfiguration` 類別來執行程式碼中的設定工作，您會*在 web.config 檔案*中執行此作業。 如需詳細資訊，請參閱[EntityFramework 以程式碼為基礎的](https://msdn.microsoft.com/data/jj680699)設定。

1. 在*邏輯*資料夾中，開啟*AddProducts.cs*檔案。
2. 新增 `System.Data.Entity.Infrastructure` 的 `using` 語句，如下所示以黃色反白顯示：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample2.cs?highlight=6)]
3. 將 `catch` 區塊新增至 `AddProduct` 方法，以便將 `RetryLimitExceededException` 記錄為黃色的反白顯示：   

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample3.cs?highlight=14-15,17-22)]

藉由新增 `RetryLimitExceededException` 例外狀況，您可以提供更好的記錄，或向使用者顯示錯誤訊息，他們可以選擇再次嘗試此程式。 藉由攔截 `RetryLimitExceededException` 例外狀況，只會嘗試使用暫時性的錯誤，並失敗數次。 傳回的實際例外狀況會包裝在 `RetryLimitExceededException` 例外狀況中。 此外，您也加入了一般 catch 區塊。 如需 `RetryLimitExceededException` 例外狀況的詳細資訊，請參閱[Entity Framework 連接恢復/重試邏輯](https://msdn.microsoft.com/data/dn456835)。

## <a name="command-interception"></a>命令攔截

既然您已開啟重試原則，您要如何進行測試以確認它是否如預期般運作？ 不太容易強制發生暫時性錯誤，特別是當您在本機執行時，尤其難以將實際的暫時性錯誤整合到自動化單元測試中。 若要測試連接復原功能，您需要一種方式來攔截 Entity Framework 傳送至 SQL Server 的查詢，並以通常是暫時性的例外狀況類型來取代 SQL Server 回應。

您也可以使用查詢攔截來執行雲端應用程式的最佳作法：記錄對外部服務（例如資料庫服務）之所有呼叫的延遲、成功或失敗。

在本教學課程的這一節中，您將使用 Entity Framework 的[*攔截功能*](https://msdn.microsoft.com/data/dn469464)來記錄和模擬暫時性錯誤。

### <a name="create-a-logging-interface-and-class"></a>建立記錄介面和類別

記錄的最佳做法是使用[`interface`](https://msdn.microsoft.com/library/ms173156.aspx) ，而不是對 `System.Diagnostics.Trace` 或記錄類別的硬式編碼呼叫。 這可讓您在稍後需要執行此動作時，更輕鬆地變更您的記錄機制。 因此，在本節中，您將建立記錄介面和用來執行它的類別。

根據上述程式，您已下載並開啟 Visual Studio 中的**WingtipToys**範例應用程式。

1. 在**WingtipToys**專案中建立資料夾，並將其命名為 [*記錄*]。
2. 在 [*記錄*] 資料夾中，建立名為*ILogger.cs*的類別檔案，並以下列程式碼取代預設程式碼：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample4.cs)]

   介面提供三個追蹤層級來指出記錄的相對重要性，另一個則是設計來為外部服務呼叫（例如資料庫查詢）提供延遲資訊。 記錄方法具有多載，可讓您傳入例外狀況。 如此一來，包含堆疊追蹤和內部例外狀況的例外狀況資訊會由實作為介面的類別來可靠地記錄，而不是依賴整個應用程式的每個記錄方法呼叫中所進行的作業。  
  
   `TraceApi` 方法可讓您追蹤對外部服務（例如 SQL Database）之每個呼叫的延遲。
3. 在 [*記錄*] 資料夾中，建立名為*Logger.cs*的類別檔案，並以下列程式碼取代預設程式碼：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample5.cs)]

此執行會使用 `System.Diagnostics` 來進行追蹤。 這是 .NET 的內建功能，可讓您輕鬆地產生及使用追蹤資訊。 有許多 &quot;接聽程式&quot; 您可以搭配使用 `System.Diagnostics` 追蹤、將記錄寫入檔案，或將它們寫入 Windows Azure 中的 blob 儲存體。 如需詳細資訊，請參閱在 Visual Studio 中的[Windows Azure 網站疑難排解](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)中的一些選項，以及其他資源的連結。 在本教學課程中，您只會在 [Visual Studio**輸出**] 視窗中查看記錄。

在生產應用程式中，您可能想要考慮使用 `System.Diagnostics`以外的追蹤架構，如果您決定這麼做，則 `ILogger` 介面可以讓切換至不同的追蹤機制變得相當容易。

### <a name="create-interceptor-classes"></a>建立攔截器類別

接下來，您將建立每次將查詢傳送至資料庫時，Entity Framework 將呼叫的類別，一個用來模擬暫時性錯誤，另一個用來進行記錄。 這些攔截器類別必須衍生自 `DbCommandInterceptor` 類別。 在其中，您會撰寫要在執行查詢時自動呼叫的方法覆寫。 在這些方法中，您可以檢查或記錄要傳送到資料庫的查詢，而且您可以在查詢傳送至資料庫之前，先將它變更，或在不傳遞查詢到資料庫的情況下傳回 Entity Framework。

1. 若要建立會在將每個 SQL 查詢傳送至資料庫之前先記錄的攔截器類別，請在*邏輯*資料夾中建立名為*InterceptorLogging.cs*的類別檔案，並以下列程式碼取代預設程式碼：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample6.cs)]

   針對成功的查詢或命令，此程式碼會寫入含有延遲資訊的資訊記錄檔。 針對例外狀況，它會建立錯誤記錄檔。
2. 若要建立攔截器類別，當您在名為*AdminPage*的頁面上 &quot;輸入 [**名稱**] 文字方塊中的&quot; 時，會產生虛擬暫時性錯誤，請在*邏輯*資料夾中建立名為*InterceptorTransientErrors.cs*的類別檔案，並以下列程式碼取代預設程式碼：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample7.cs)]

    此程式碼只會覆寫 `ReaderExecuting` 方法，這會針對可傳回多個資料列的查詢呼叫。 如果您想要檢查其他類型查詢的連接恢復功能，您也可以覆寫 `NonQueryExecuting` 和 `ScalarExecuting` 方法，如同記錄攔截器所做的一樣。  
  
   稍後，您將以「系統管理員」身分登入，並選取頂端導覽列上的 [**管理**] 連結。 然後，在 [ *AdminPage* ] 頁面上，您將新增名為 &quot;擲回&quot;的產品。 此程式碼會建立錯誤號碼20的虛擬 SQL Database 例外狀況，這種類型通常是暫時性的。 目前被辨識為暫時性的其他錯誤號碼為64、233、10053、10054、10060、10928、10929、40197、40501和40613，但這些可能在新版本的 SQL Database 中有所變更。 產品將會重新命名為 "TransientErrorExample"，您可以在*InterceptorTransientErrors.cs*檔案的程式碼中遵循。  
  
   此程式碼會將例外狀況傳回給 Entity Framework，而不是執行查詢並傳回結果。 暫時性例外狀況會傳回*四*次，然後程式碼會還原成將查詢傳送至資料庫的一般程式。

    因為所有專案都已記錄，所以您可以看到 Entity Framework 嘗試在最後一次成功之前執行查詢四次，而應用程式的唯一差異在於使用查詢結果轉譯頁面需要較長的時間。  
  
   可以設定 Entity Framework 重試的次數。此程式碼會指定四次，因為這是 SQL Database 執行原則的預設值。 如果您變更執行原則，則也會變更此處的程式碼，以指定產生暫時性錯誤的次數。 您也可以變更程式碼以產生更多例外狀況，讓 Entity Framework 會擲回 `RetryLimitExceededException` 例外狀況。
3. 在*global.asax*中，加入下列 using 語句：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample8.cs)]
4. 然後，將反白顯示的行新增至 `Application_Start` 方法：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample9.cs?highlight=17-20)]

這幾行程式碼會造成您的攔截器程式碼在 Entity Framework 將查詢傳送至資料庫時執行。 請注意，因為您已針對暫時性錯誤模擬和記錄建立個別的攔截器類別，所以可以獨立啟用和停用它們。   
  
 您可以在程式碼中的任何位置使用 `DbInterception.Add` 方法來新增攔截器;它不一定要在 `Application_Start` 方法中。 另一個選項是，如果您未在 `Application_Start` 方法中加入攔截器，則會更新或新增名為*WingtipToysConfiguration.cs*的類別，並將上述程式碼放在 `WingtipToysConfiguration` 類別之函式的結尾。

無論您在哪裡放置此程式碼，請小心不要多次執行相同攔截器的 `DbInterception.Add`，或者您會取得其他攔截器實例。 例如，如果您新增記錄攔截器兩次，則會看到每個 SQL 查詢的兩個記錄檔。

攔截器會依照註冊的循序執行（呼叫 `DbInterception.Add` 方法的順序）。 根據您在攔截器中所執行的動作，順序可能會很重要。 例如，攔截器可能會變更它在 `CommandText` 屬性中取得的 SQL 命令。 如果它確實變更了 SQL 命令，則下一個攔截器會取得變更的 SQL 命令，而不是原始的 SQL 命令。

您已撰寫暫時性錯誤模擬程式碼，讓您可以在 UI 中輸入不同的值，藉此引發暫時性錯誤。 或者，您可以撰寫攔截器程式碼，一律產生暫時性例外狀況的順序，而不檢查特定的參數值。 然後，只有在您想要產生暫時性錯誤時，才可以新增攔截器。 不過，如果您這樣做，請等到資料庫初始化完成之後，才新增攔截器。 換句話說，在您開始產生暫時性錯誤之前，請至少執行一個資料庫作業，例如在其中一個實體集上進行查詢。 Entity Framework 在資料庫初始化期間執行數個查詢，而且它們不會在交易中執行，因此在初始化期間發生的錯誤可能會導致內容進入不一致的狀態。

## <a name="test-logging-and-connection-resiliency"></a>測試記錄和連接復原

1. 在 Visual Studio 中，按**F5**以在「偵測模式」中執行應用程式，然後使用「Pa $ $word」作為密碼來登入為「系統管理員」。
2. 從頂端的導覽列選取 [**管理員**]。
3. 輸入名為「擲回」的新產品，其中包含適當的描述、價格和影像檔案。
4. 按下 [**新增產品**] 按鈕。  
   您會發現瀏覽器似乎會在幾秒後停止回應，而 Entity Framework 會多次重試查詢。 第一次重試會非常快速地執行，然後在每次重試之前都會增加等待時間。 這個在每次重試之前等候較久的程式稱為*指數*輪詢。
5. 等到頁面不再嘗試載入。
6. 停止專案並查看 [Visual Studio**輸出**] 視窗，以查看追蹤輸出。 您可以在 [&gt; **Windows** -&gt;**輸出**] 中選取 [ **Debug** -] 來尋找 [**輸出**] 視窗。 您可能必須滾動到記錄器所撰寫的數個其他記錄。  
  
   請注意，您可以看到傳送至資料庫的實際 SQL 查詢。 您會看到 Entity Framework 開始使用的一些初始查詢和命令，檢查資料庫版本和遷移記錄資料表。   
    ![輸出視窗](aspnet-web-forms-connection-resiliency-and-command-interception/_static/image1.png)   
   請注意，除非您停止應用程式並重新啟動，否則無法重複此測試。 如果您想要能夠在應用程式的單一執行中多次測試連接恢復功能，您可以在 `InterceptorTransientErrors` 中撰寫程式碼以重設錯誤計數器。
7. 若要查看執行策略（重試原則）的差異，請批註*邏輯*資料夾中*WingtipToysConfiguration.cs*檔案中的 `SetExecutionStrategy` 行，再于 [檢查模式] 中再次執行 [系統**管理**] 頁面，然後新增名為 &quot;的產品，然後再次擲回&quot;。  
  
   這次偵錯工具在第一次嘗試執行查詢時，會立即停止第一個產生的例外狀況。  
    ![調試層-查看詳細資料](aspnet-web-forms-connection-resiliency-and-command-interception/_static/image2.png)
8. 取消批註*WingtipToysConfiguration.cs*檔案中的 `SetExecutionStrategy` 行。

## <a name="summary"></a>總結

在本教學課程中，您已瞭解如何修改 Web form 範例應用程式，以支援連接恢復功能和命令攔截。

## <a name="next-steps"></a>後續步驟

在您已複習 ASP.NET Web Forms 中的連線恢復功能和命令攔截之後，請參閱[ASP.NET 4.5 中](../performance-and-caching/using-asynchronous-methods-in-aspnet-45.md)的 ASP.NET Web Forms 主題非同步方法。 本主題將教您使用 Visual Studio 建立異步 ASP.NET Web Forms 應用程式的基本概念。
