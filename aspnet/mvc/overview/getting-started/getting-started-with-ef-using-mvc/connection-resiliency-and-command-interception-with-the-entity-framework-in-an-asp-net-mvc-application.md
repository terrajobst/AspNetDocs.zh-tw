---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教學課程：在 ASP.NET MVC 應用程式中搭配使用連接復原和命令攔截與 EF
author: tdykstra
description: 在本教學課程中，您將瞭解如何使用連線恢復功能和命令攔截。 它們是 Entity Framework 6 的兩項重要功能。
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: c89d809f-6c65-4425-a3fa-c9f6e8ac89f2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 276266f8ae9df38529d44742ebe6ac0dc8e79727
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583451"
---
# <a name="tutorial-use-connection-resiliency-and-command-interception-with-entity-framework-in-an-aspnet-mvc-app"></a>教學課程：在 ASP.NET MVC 應用程式中搭配使用連線恢復功能和命令攔截 Entity Framework

到目前為止，應用程式已在您的開發電腦上，于本機執行 IIS Express。 若要讓其他人可以透過網際網路使用實際的應用程式，您必須將它部署到 web 主控提供者，而且您必須將資料庫部署到資料庫伺服器。

在本教學課程中，您將瞭解如何使用連線恢復功能和命令攔截。 這些是 Entity Framework 6 的兩項重要功能，在部署至雲端環境時特別有用：連線復原（暫時性錯誤的自動重試）和命令攔截（攔截所有傳送至資料庫的 SQL 查詢以記錄或變更它們）。

此連接恢復功能和命令攔截教學課程是選擇性的。 如果您略過本教學課程，後續的教學課程中將必須進行幾個次要調整。

在本教學課程中，您已：

> [!div class="checklist"]
> * 啟用連接恢復功能
> * 啟用命令攔截
> * 測試新設定

## <a name="prerequisites"></a>Prerequisites

* [排序、篩選與分頁](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="enable-connection-resiliency"></a>啟用連接恢復功能

當您將應用程式部署至 Windows Azure 時，您會將資料庫部署至 Windows Azure SQL Database 雲端資料庫服務。 當您連線到雲端資料庫服務時，如果您的 web 伺服器和資料庫伺服器在相同的資料中心內直接連接在一起，通常會更常遇到暫時性連接錯誤。 即使雲端 web 伺服器和雲端資料庫服務裝載于相同的資料中心，它們之間還是有更多的網路連線可能會發生問題，例如負載平衡器。

此外，雲端服務通常會由其他使用者共用，這表示其回應性可能會受到影響。 而且您對資料庫的存取權可能會受到節流。 「節流」表示當您嘗試存取時，資料庫服務會擲回例外狀況，而不是服務等級協定（SLA）中允許的頻率。

當您存取雲端服務時，許多或大部分的連線問題都是暫時性的，也就是說，它們會在短時間內自行解決。 因此，當您嘗試資料庫作業並取得通常是暫時性的錯誤類型時，您可以在短暫等候之後再次嘗試操作，而且作業可能會成功。 如果您藉由自動重試來處理暫時性錯誤，您可以為使用者提供更好的體驗，讓客戶無法看到大部分的情況。 Entity Framework 6 中的連接復原功能會將重試失敗 SQL 查詢的程式自動化。

您必須針對特定的資料庫服務，適當地設定連接復原功能：

- 它必須知道可能是暫時性的例外狀況。 例如，您想要重試因網路連線暫時中斷而造成的錯誤，而不是程式 bug 所造成的錯誤。
- 它必須在失敗的作業重試之間等候一段適當的時間。 您可以在批次進程的重試之間等候較長的時間，而不是使用者正在等候回應的線上網頁。
- 它必須先重試適當的次數，才會放棄。 您可能想要在您于線上應用程式中的批次進程中，重試更多次。

您可以針對 Entity Framework 提供者所支援的任何資料庫環境，手動設定這些設定，但通常適用于使用 Windows Azure SQL Database 之線上應用程式的預設值，已經為您設定好了，而且這些是您將為 Contoso 大學應用程式執行的設定。

若要啟用連接恢復功能，您只需要在您的元件中建立衍生自[DbConfiguration](https://msdn.microsoft.com/data/jj680699.aspx)類別的類別，並在該類別中設定 SQL Database*執行策略*，在 EF 是*重試原則*的另一個詞彙。

1. 在 DAL 資料夾中，新增名為*SchoolConfiguration.cs*的類別檔案。
2. 使用下列程式碼取代範本程式碼：

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

    Entity Framework 會自動執行它在衍生自 `DbConfiguration`的類別中找到的程式碼。 您可以使用 `DbConfiguration` 類別來執行程式碼中的設定工作，您會*在 web.config 檔案*中執行此作業。 如需詳細資訊，請參閱[EntityFramework 以程式碼為基礎的](https://msdn.microsoft.com/data/jj680699)設定。
3. 在*StudentController.cs*中，加入 `System.Data.Entity.Infrastructure`的 `using` 語句。

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]
4. 變更攔截 `DataException` 例外狀況的所有 `catch` 區塊，使其改為攔截 `RetryLimitExceededException` 例外狀況。 例如:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=1)]

    您使用 `DataException` 嘗試找出可能是暫時性的錯誤，以提供易記的「再試一次」訊息。 但現在您已開啟重試原則，則唯一可能是暫時性的錯誤已嘗試並失敗數次，而實際傳回的例外狀況將會包裝在 `RetryLimitExceededException` 例外狀況中。

如需詳細資訊，請參閱[Entity Framework 連接恢復/重試邏輯](https://msdn.microsoft.com/data/dn456835)。

## <a name="enable-command-interception"></a>啟用命令攔截

既然您已開啟重試原則，您要如何進行測試以確認它是否如預期般運作？ 不太容易強制發生暫時性錯誤，特別是當您在本機執行時，尤其難以將實際的暫時性錯誤整合到自動化單元測試中。 若要測試連接復原功能，您需要一種方式來攔截 Entity Framework 傳送至 SQL Server 的查詢，並以通常是暫時性的例外狀況類型來取代 SQL Server 回應。

您也可以使用查詢攔截來執行雲端應用程式的最佳作法：記錄對外部服務（例如資料庫服務）[之所有呼叫的延遲、成功或失敗](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log)。 EF6 提供[專用的記錄 API](https://msdn.microsoft.com/data/dn469464) ，可讓您更輕鬆地進行記錄，但在本教學課程的這一節中，您將瞭解如何直接使用 Entity Framework 的[攔截功能](https://msdn.microsoft.com/data/dn469464)，同時用於記錄和模擬暫時性錯誤。

### <a name="create-a-logging-interface-and-class"></a>建立記錄介面和類別

[記錄的最佳做法](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log)是使用介面，而不是對 system.webserver 或記錄類別的硬式編碼呼叫來執行此動作。 這可讓您在稍後需要執行此動作時，更輕鬆地變更您的記錄機制。 所以在本節中，您將建立記錄介面和用來執行它的類別。/p >

1. 在專案中建立資料夾，並將其命名為 [*記錄*]。
2. 在 [*記錄*] 資料夾中，建立名為*ILogger.cs*的類別檔案，並以下列程式碼取代範本程式碼：

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

    介面提供三個追蹤層級來指出記錄的相對重要性，另一個則是設計來為外部服務呼叫（例如資料庫查詢）提供延遲資訊。 記錄方法具有多載，可讓您傳入例外狀況。 如此一來，包含堆疊追蹤和內部例外狀況的例外狀況資訊會由實作為介面的類別來可靠地記錄，而不是依賴整個應用程式的每個記錄方法呼叫中所進行的作業。

    TraceApi 方法可讓您追蹤對外部服務之每個呼叫的延遲，例如 SQL Database。
3. 在 [*記錄*] 資料夾中，建立名為*Logger.cs*的類別檔案，並以下列程式碼取代範本程式碼：

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

    此實作為使用 Diagnostics 來進行追蹤。 這是 .NET 的內建功能，可讓您輕鬆地產生及使用追蹤資訊。 有許多「接聽程式」可用於診斷追蹤、將記錄寫入檔案，或將它們寫入 Azure 中的 blob 儲存體。 如需詳細資訊，請參閱在 Visual Studio 中的[Azure 網站疑難排解](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)中的一些選項，以及其他資源的連結。 在本教學課程中，您只會查看 [Visual Studio**輸出**] 視窗中的記錄。

    在生產應用程式中，您可能想要考慮追蹤 ILogger 以外的封裝，而如果您決定這麼做，則可以讓切換至不同的追蹤機制變得相當容易。

### <a name="create-interceptor-classes"></a>建立攔截器類別

接下來，您將建立每次將查詢傳送至資料庫時，Entity Framework 將呼叫的類別，一個用來模擬暫時性錯誤，另一個用來進行記錄。 這些攔截器類別必須衍生自 `DbCommandInterceptor` 類別。 在中，您可以撰寫在即將執行查詢時自動呼叫的方法覆寫。 在這些方法中，您可以檢查或記錄要傳送到資料庫的查詢，而且您可以在查詢傳送至資料庫之前，先將它變更，或在不傳遞查詢到資料庫的情況下傳回 Entity Framework。

1. 若要建立會記錄傳送至資料庫之每個 SQL 查詢的攔截器類別，請在*DAL*資料夾中建立名為*SchoolInterceptorLogging.cs*的類別檔案，並以下列程式碼取代範本程式碼：

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

    針對成功的查詢或命令，此程式碼會寫入含有延遲資訊的資訊記錄檔。 針對例外狀況，它會建立錯誤記錄檔。
2. 若要建立會在**搜尋**方塊中輸入「擲回」時產生虛擬暫時性錯誤的攔截器類別，請在*DAL*資料夾中建立名為*SchoolInterceptorTransientErrors.cs*的類別檔案，並以下列程式碼取代範本程式碼：

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

    此程式碼只會覆寫 `ReaderExecuting` 方法，這會針對可傳回多個資料列的查詢呼叫。 如果您想要檢查其他類型查詢的連接恢復功能，您也可以覆寫 `NonQueryExecuting` 和 `ScalarExecuting` 方法，如同記錄攔截器所做的一樣。

    當您執行 [學生] 頁面並輸入「擲回」作為搜尋字串時，此程式碼會建立錯誤號碼20的虛擬 SQL Database 例外狀況，這種類型通常是暫時性的。 目前被辨識為暫時性的其他錯誤號碼為64、233、10053、10054、10060、10928、10929、40197、40501和40613，但這些可能在新版本的 SQL Database 中有所變更。

    此程式碼會將例外狀況傳回給 Entity Framework，而不是執行查詢並傳回查詢結果。 暫時性例外狀況會傳回四次，然後程式碼會還原成將查詢傳送至資料庫的一般程式。

    因為所有專案都已記錄，所以您可以看到 Entity Framework 嘗試在最後一次成功之前執行查詢四次，而應用程式的唯一差異在於使用查詢結果轉譯頁面需要較長的時間。

    可以設定 Entity Framework 重試的次數。此程式碼會指定四次，因為這是 SQL Database 執行原則的預設值。 如果您變更執行原則，則也會變更此處的程式碼，以指定產生暫時性錯誤的次數。 您也可以變更程式碼以產生更多例外狀況，讓 Entity Framework 會擲回 `RetryLimitExceededException` 例外狀況。

    您在 [搜尋] 方塊中輸入的值將會是 `command.Parameters[0]` 和 `command.Parameters[1]` （一個用於名字，另一個用於姓氏）。 找到值 "% Throw%" 時，「擲回」會在這些參數中以「a」取代，讓某些學生可以找到並傳回。

    這只是一個便利的方式，可以根據變更應用程式 UI 的某些輸入來測試連接復原。 您也可以撰寫會針對所有查詢或更新產生暫時性錯誤的程式碼，如稍後關於*DbInterception*的批註中所述。
3. 在*global.asax*中，加入下列 `using` 語句：

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]
4. 將反白顯示的行新增至 `Application_Start` 方法：

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=7-8)]

    這幾行程式碼會造成您的攔截器程式碼在 Entity Framework 將查詢傳送至資料庫時執行。 請注意，因為您已針對暫時性錯誤模擬和記錄建立個別的攔截器類別，所以可以獨立啟用和停用它們。

    您可以在程式碼中的任何位置使用 `DbInterception.Add` 方法來新增攔截器;它不一定要在 `Application_Start` 方法中。 另一個選項是將此程式碼放在您稍早建立的 DbConfiguration 類別中，以設定執行原則。

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=6-7)]

    無論您在哪裡放置此程式碼，請小心不要多次執行相同攔截器的 `DbInterception.Add`，或者您會取得其他攔截器實例。 例如，如果您新增記錄攔截器兩次，則會看到每個 SQL 查詢的兩個記錄檔。

    攔截器會依照註冊的循序執行（呼叫 `DbInterception.Add` 方法的順序）。 根據您在攔截器中所執行的動作，順序可能會很重要。 例如，攔截器可能會變更它在 `CommandText` 屬性中取得的 SQL 命令。 如果它確實變更了 SQL 命令，則下一個攔截器會取得變更的 SQL 命令，而不是原始的 SQL 命令。

    您已撰寫暫時性錯誤模擬程式碼，讓您可以在 UI 中輸入不同的值，藉此引發暫時性錯誤。 或者，您可以撰寫攔截器程式碼，一律產生暫時性例外狀況的順序，而不檢查特定的參數值。 然後，只有在您想要產生暫時性錯誤時，才可以新增攔截器。 不過，如果您這樣做，請等到資料庫初始化完成之後，才新增攔截器。 換句話說，在您開始產生暫時性錯誤之前，請至少執行一個資料庫作業，例如在其中一個實體集上進行查詢。 Entity Framework 在資料庫初始化期間執行數個查詢，而且它們不會在交易中執行，因此在初始化期間發生的錯誤可能會導致內容進入不一致的狀態。

## <a name="test-the-new-configuration"></a>測試新設定

1. 按**F5**以在 debug 模式中執行應用程式，然後按一下 [**學生**] 索引標籤。
2. 查看 Visual Studio 的 [**輸出**] 視窗以查看追蹤輸出。 您可能必須在超過一些 JavaScript 錯誤的情況下，才能取得記錄器所寫入的記錄。

    請注意，您可以看到傳送至資料庫的實際 SQL 查詢。 您會看到一些初始查詢和命令，Entity Framework 開始使用、檢查資料庫版本和遷移記錄資料表（您將在下一個教學課程中瞭解如何進行遷移）。 您會看到分頁的查詢，以找出有多少學生，最後您會看到取得學生資料的查詢。

    ![一般查詢的記錄](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. 在 [**學生**] 頁面中，輸入「擲回」作為搜尋字串，然後按一下 [**搜尋**]。

    ![擲回搜尋字串](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

    您會發現瀏覽器似乎會在幾秒後停止回應，而 Entity Framework 會多次重試查詢。 第一次重試會非常快速地執行，然後在每次額外重試之前，會先等待。 這個在每次重試之前等候較久的程式稱為*指數*輪詢。

    當頁面顯示時，顯示名稱中有 "a" 的學生，查看 [輸出] 視窗，您會看到相同的查詢嘗試五次，前四次傳回暫時性的例外狀況。 針對每個暫時性錯誤，您會看到在 `SchoolInterceptorTransientErrors` 類別中產生暫時性錯誤時所撰寫的記錄檔（「傳回命令的暫時性錯誤」），而且當 `SchoolInterceptorLogging` 取得例外狀況時，會看到寫入的記錄檔。

    ![記錄輸出顯示重試](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

    由於您輸入了搜尋字串，因此會參數化傳回 student 資料的查詢：

    [!code-sql[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.sql)]

    您不會記錄參數的值，但您可以這麼做。 如果您想要查看參數值，您可以撰寫記錄程式碼，從您在攔截器方法中取得之 `DbCommand` 物件的 `Parameters` 屬性取得參數值。

    請注意，除非您停止應用程式並重新啟動，否則無法重複此測試。 如果您想要能夠在應用程式的單一執行中多次測試連接恢復功能，您可以在 `SchoolInterceptorTransientErrors`中撰寫程式碼以重設錯誤計數器。
4. 若要查看執行策略（重試原則）的差異，請將*SchoolConfiguration.cs*中的 `SetExecutionStrategy` 行批註，再于 [debug] 模式中再次執行 [學生] 頁面，然後再次搜尋「擲回」。

    這次偵錯工具在第一次嘗試執行查詢時，會立即停止第一個產生的例外狀況。

    ![虛擬例外狀況](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
5. 取消批註*SchoolConfiguration.cs*中的*SetExecutionStrategy*行。

## <a name="get-the-code"></a>取得程式碼

[下載已完成的專案](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他資源

您可以在[ASP.NET 資料存取-建議的資源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已：

> [!div class="checklist"]
> * 已啟用連接恢復功能
> * 已啟用命令攔截
> * 已測試新的設定

前往下一篇文章，以瞭解 Code First 遷移和 Azure 部署的相關資訊。
> [!div class="nextstepaction"]
> [Code First 遷移和 Azure 部署](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)
