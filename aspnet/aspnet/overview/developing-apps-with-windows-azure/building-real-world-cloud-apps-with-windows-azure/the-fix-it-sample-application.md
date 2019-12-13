---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: 附錄：修正 It 範例應用程式（使用 Azure 建立真實世界的雲端應用程式） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會說明13個模式和實務，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: e6fda47babd3c2505315f42667c45f09482218c2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74583751"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a>附錄：修正 It 範例應用程式（使用 Azure 建立真實世界的雲端應用程式）

由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom 作者: dykstra](https://github.com/tdykstra)

[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> **使用 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。 其中說明13種模式和作法，可協助您成功開發雲端 web 應用程式。 如需電子書的相關資訊，請參閱[第一章](introduction.md)。

使用 Azure 電子書建立真實世界雲端應用程式的本附錄包含下列各節，其中提供可供您下載之 Fix It 範例應用程式的其他相關資訊：

- [已知問題](#knownissues)
- [最佳作法](#bestpractices)
- [如何從本機電腦上的 Visual Studio 執行應用程式](#run-in-vs)
- [如何使用 Windows PowerShell 腳本將基本應用程式部署至 Azure App Service Web Apps](#deploybase)
- [疑難排解 Windows PowerShell 腳本](#troubleshooting)
- [如何將具有佇列處理的應用程式部署至 Azure App Service Web Apps 和 Azure 雲端服務](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a>已知問題

最初開發的 Fix It 應用程式，是為了說明這種電子書所呈現的一些模式。 不過，由於電子書是關於建立真實世界的應用程式，因此我們會將 Fix It 程式碼與我們針對發行之軟體所做的檢查和測試流程進行比對。 我們發現許多問題，如同任何真實世界的應用程式，我們已修正其中一些問題，而其中一些我們已延遲到較新的版本。

下列清單包含應在實際執行應用程式中解決的問題，但基於其中一個原因或我們決定不在「修正 It」範例應用程式的初始版本中處理。

### <a name="security"></a>安全性

- 請確定您無法將工作指派給不存在的擁有者。
- 請確定您只能查看和修改您所建立或指派給您的工作。
- 對登入頁面和驗證 cookie 使用 HTTPS。
- 指定驗證 cookie 的時間限制。

### <a name="input-validation"></a>輸入驗證

一般來說，生產應用程式會比修正 It 應用程式執行更多的輸入驗證。 例如，允許進行上傳的映射大小/影像檔案大小應該會受到限制。

### <a name="administrator-functionality"></a>系統管理員功能

系統管理員應該能夠變更現有工作的擁有權。 例如，工作的建立者可能會離開公司，除非已啟用系統管理存取權，否則不會有任何人可以維護工作。

### <a name="queue-message-processing"></a>佇列訊息處理

修正 It 應用程式中的佇列訊息處理是設計成簡單的，以便以最少量的程式碼來說明以佇列為中心的工作模式。 這個簡單的程式碼不適合實際的生產應用程式。

- 程式碼不保證每個佇列訊息最多會處理一次。 當您從佇列取得訊息時，會有一個超時期間，在此期間內，其他佇列接聽程式看不到訊息。 如果在刪除訊息之前的超時時間已過期，訊息就會再次顯示。 因此，如果背景工作角色實例花了很長的時間處理訊息，則理論上可能會有相同的訊息處理兩次，導致資料庫發生重複的工作。 如需有關此問題的詳細資訊，請參閱[使用 Azure 儲存體的佇列](https://msdn.microsoft.com/library/ff803365.aspx#sec7)。
- 藉由批次處理訊息抓取，佇列輪詢邏輯可能更符合成本效益。 每次呼叫[CloudQueue](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)時，都有交易成本。 相反地，您可以呼叫[CloudQueue. GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) （請注意複數的 '），這會在單一交易中取得多個訊息。 Azure 儲存體佇列的交易成本非常低，因此在大部分的情況下，對成本所造成的影響並不明顯。
- 佇列訊息處理常式代碼中的緊密迴圈會導致 CPU 親和性，而不會有效率地使用多核心 Vm。 較佳的設計會使用工作平行處理原則，平行執行數個非同步工作。
- 佇列訊息處理只有基本的例外狀況處理。 例如，程式碼不會處理[有害訊息](https://msdn.microsoft.com/library/ms789028.aspx)。 （當訊息處理造成例外狀況時，您必須記錄錯誤並刪除訊息，否則背景工作角色會嘗試再次處理它，迴圈將會無限期地繼續）。

### <a name="sql-queries-are-unbounded"></a>SQL 查詢沒有界限

最新的修正程式碼不會限制索引頁面的查詢可能會傳回多少資料列。 如果在資料庫中輸入大量的工作，收到的結果清單大小可能會造成效能問題。 解決方案是執行分頁。 如需範例，請參閱[使用 ASP.NET MVC 應用程式中的 Entity Framework 排序、篩選和分頁](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)。

### <a name="view-models-recommended"></a>建議的視圖模型

Fix It 應用程式會使用 FixItTask 實體類別，在控制器和視圖之間傳遞資訊。 最佳做法是使用 view 模型。 領域模型（例如，FixItTask 實體類別）是以資料持續性所需的方式來設計，而視圖模型則可以設計來呈現資料。 如需詳細資訊，請參閱[12 ASP.NET MVC 最佳做法](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)。

### <a name="secure-image-blob-recommended"></a>建議使用安全映射 blob

Fix It 應用程式會將已上傳的影像儲存為公用，這表示任何尋找該 URL 的人都可以存取影像。 影像可以受到保護，而不是公用。

### <a name="no-powershell-automation-scripts-for-queues"></a>沒有適用于佇列的 PowerShell 自動化腳本

範例 PowerShell 自動化腳本只是針對修正它的基礎版本而撰寫，它完全在 Azure App Service Web Apps 中執行。 我們尚未提供用來設定和部署至 web 應用程式的腳本，以及佇列處理所需的雲端服務環境。

### <a name="special-handling-for-html-codes-in-user-input"></a>使用者輸入中 HTML 程式碼的特殊處理

ASP.NET 會在使用者輸入文字方塊中輸入腳本，自動防止惡意使用者嘗試跨網站腳本攻擊的許多方式。 以及用來顯示工作標題和附注的 MVC `DisplayFor` helper，會自動將其傳送至瀏覽器的值進行 HTML 編碼。 但是在生產環境應用程式中，您可能會想要採取其他措施。 如需詳細資訊，請參閱[在 ASP.NET 中要求驗證](https://msdn.microsoft.com/library/hh882339.aspx)。

<a id="bestpractices"></a>
## <a name="best-practices"></a>最佳做法

以下是在程式碼審查和測試修正 It 應用程式的原始版本中探索後已修正的一些問題。 有些是因為原始當中不知道特定的最佳作法，而是因為程式碼是快速撰寫，而不是用於發行的軟體。 我們會在這裡列出問題，以防我們從這項審查和測試中學習到的內容，對於同時也在開發 web 應用程式的其他人可能會有説明。

### <a name="dispose-the-database-repository"></a>處置資料庫存放庫

`FixItTaskRepository` 類別必須處置 Entity Framework `DbContext` 實例。 我們藉由在 `FixItTaskRepository` 類別中執行 `IDisposable` 來完成這項操作：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

請注意，AutoFac 會自動處置 `FixItTaskRepository` 實例，因此我們不需要明確地處置它。

另一個選項是從 `FixItTaskRepository`移除 `DbContext` 成員變數，並改為在 `using` 語句內部的每個存放庫方法中建立本機 `DbContext` 變數。 例如:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a>使用 DI 註冊單次個體

由於只需要 `PhotoService` 類別和 `Logger` 類別的一個實例，因此應該在*DependenciesConfig.cs*中將這些類別[註冊為單一實例以進行](https://code.google.com/p/autofac/wiki/InstanceScope)相依性插入：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a>安全性：不要向使用者顯示錯誤詳細資料

原始的修正 It 應用程式沒有一般錯誤頁面，只要讓所有例外狀況反升至 UI，因此某些例外狀況（例如資料庫連接錯誤）可能會導致完整的堆疊追蹤顯示在瀏覽器中。 詳細的錯誤資訊有時可能會協助惡意使用者發動攻擊。 解決方案是記錄例外狀況詳細資料，並向不包含錯誤詳細資料的使用者顯示錯誤頁面。 Fix It 應用程式已在進行記錄，而為了顯示錯誤頁面，我們在 web.config 檔案中加入了 `<customErrors mode=On>`。

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

根據預設，這會顯示錯誤的*Views\Shared\Error.cshtml* 。 您可以自訂*error. cshtml*或建立自己的錯誤網頁檢視，並加入 `defaultRedirect` 屬性。 您也可以針對特定錯誤指定不同的錯誤頁面。

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a>安全性：只允許其建立者編輯工作

[儀表板索引] 頁面只會顯示登入的使用者所建立的工作，但惡意使用者可以建立一個識別碼為另一個使用者工作的 URL。 我們已在*DashboardController.cs*中新增程式碼，以在此情況下傳回404：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a>不要忍受例外狀況

原始的修正 It 應用程式在記錄 SQL 查詢所產生的例外狀況之後，只會傳回 null：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

這會讓使用者看起來像是查詢成功，但是只是未傳回任何資料列。 解決方法是在攔截和記錄之後重新擲回例外狀況：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a>攔截背景工作角色中的所有例外狀況

背景工作角色中任何未處理的例外狀況都會導致回收 VM，因此您會想要將您在 try-catch 區塊中執行的所有專案包裝在一起，並處理所有例外狀況。

### <a name="specify-length-for-string-properties-in-entity-classes"></a>在實體類別中指定字串屬性的長度

為了顯示簡單的程式碼，原始版本的 Fix It 應用程式未指定 FixItTask 實體欄位的長度，因此在資料庫中定義為 Varchar （max）。 因此，UI 幾乎可以接受任何數量的輸入。 指定長度會將套用至 web 網頁中的使用者輸入和資料庫中的資料行大小限制：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a>當私用成員不應該變更時，將其標記為 readonly

例如，在 `DashboardController` 類別中，`FixItTaskRepository` 的實例已建立，而且不應該變更，所以我們將它定義為[readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx)。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a>使用清單。Any （）而不是 list。Count （） &gt; 0

如果您只在意清單中的一個或多個專案是否符合指定的準則，請使用[Any](https://msdn.microsoft.com/library/bb534972.aspx)方法，因為它會在找到條件的專案時立即傳回，而 `Count` 方法一律必須逐一查看每個專案。 儀表板*索引 cshtml*檔案原先具有下列程式碼：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

我們已將它變更為：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a>使用 MVC helper 在 MVC 視圖中產生 Url

若為首頁上的 [**建立 Fix it** ] 按鈕，請修正 it 應用程式硬式編碼錨定元素：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

針對類似的視圖/動作連結，最好是使用[Url。動作](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx)HTML helper，例如：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a>使用工作。延遲而不是執行緒。背景工作角色中的睡眠

新專案範本會將 `Thread.Sleep` 放入背景工作角色的範例程式碼中，但造成執行緒進入睡眠狀態可能會造成執行緒集區產生額外的不必要執行緒。 您可以改為使用 [[延遲](https://msdn.microsoft.com/library/hh139096.aspx)] 來避免這種情況。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a>避免 async void

如果非同步方法不需要傳回值，則會傳回 `Task` 型別，而不是 `void`。

這個範例來自 `FixItQueueManager` 類別：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

您應該只將 `async void` 用於最上層的事件處理常式。 如果您將方法定義為 `async void`，則呼叫端**無法等候**方法，或攔截方法擲回的任何例外狀況。 如需詳細資訊，請參閱[非同步程式設計中的最佳作法](https://msdn.microsoft.com/magazine/jj991977.aspx)。

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a>使用解除標記來中斷背景工作角色迴圈

一般而言，背景工作角色上的**Run**方法包含無限迴圈。 當背景工作角色停止時，會呼叫[RoleEntryPoint](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx)方法。 您應該使用這個方法來取消在**Run**方法內完成的工作，並正常結束。 否則，進程可能會在作業中途終止。

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a>選擇不進行自動 MIME 探查程式

在某些情況下，Internet Explorer 報告的 MIME 類型與 web 伺服器所指定的類型不同。 比方說，如果 Internet Explorer 在以 HTTP 回應標頭 Content-type 提供的檔案中找到 HTML 內容： text/純文字，Internet Explorer 會判斷內容應該轉譯為 HTML。 可惜的是，這種「MIME 探查」也可能導致主控不受信任內容之伺服器的安全性問題。 為了對抗這個問題，Internet Explorer 8 已對 MIME 類型的判斷程式碼進行了一些變更，並可讓應用程式開發人員選擇不使用[mime 探查](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)。 下列程式碼已加入至*web.config*檔案。

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a>啟用捆綁和縮制

當 Visual Studio 建立新的 Web 專案時，預設不會啟用 JavaScript 檔案的組合和縮制。 我們在 BundleConfig.cs 中新增了一行程式碼：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a>設定驗證 cookie 的到期時間

根據預設，驗證 cookie 會在兩周內過期。 較短的時間比較安全。 您可以在*StartupAuth.cs*中變更此設定：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a>如何從本機電腦上的 Visual Studio 執行應用程式

有兩種方式可執行 Fix It 應用程式：

- 執行會將新工作直接寫入 SQL 資料庫的基底應用程式。
- 使用佇列加上後端服務來執行應用程式，以建立工作。 佇列模式會在以[佇列為中心的工作模式](queue-centric-work-pattern.md)一章中加以說明。

<a id="runbase"></a>
### <a name="run-the-base-application"></a>執行基底應用程式

1. 安裝[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。
2. 安裝[適用于 Visual Studio 的 AZURE SDK for .net](https://azure.microsoft.com/downloads/)。
3. 從[MSDN 程式碼庫](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)下載 .zip 檔案。
4. 在 [檔案管理器] 中，以滑鼠右鍵按一下 .zip 檔案，然後按一下 [屬性]，然後在屬性視窗按一下 [解除封鎖]。
5. 解壓縮檔案。
6. 按兩下 .sln 檔案以啟動 Visual Studio。
7. 從 [**工具**] 功能表中，依序按一下 [ **NuGet 套件管理員**] 和 [**套件管理員主控台**]。
8. 在 [套件管理員主控台] （PMC）中，按一下 [還原]。
9. 結束 Visual Studio。
10. 啟動[Azure 儲存體模擬器](/azure/storage/common/storage-use-emulator)。
11. 重新開機 Visual Studio，開啟您在上一個步驟中關閉的方案檔。
12. 請確定 FixIt 專案已設定為啟始專案，然後按 CTRL + F5 執行專案。

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a>執行具有佇列處理的應用程式

1. 遵循執行[基底應用程式](#runbase)的指示，然後關閉瀏覽器並關閉 Visual Studio。
2. 使用系統管理員許可權啟動 Visual Studio。 （您將會使用 Azure 計算模擬器，而這需要系統管理員許可權）。
3. 在*MyFixIt*專案（Web 專案）中的應用程式*web.config*檔案中，將 `appSettings/UseQueues` 的值變更為 "true"：

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. 如果[Azure 儲存體模擬器](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx)仍未執行，請重新開機它。
5. 同時執行 FixIt Web 專案和 MyFixItCloudService 專案。

    使用 Visual Studio：

   1. 按**F5**執行 FixIt 專案。
   2. 在**方案總管**中，以滑鼠右鍵按一下 MyFixItCloudService 專案，然後按一下  **Debug**  > **開始新實例**。

    使用適用于 Web 的 Visual Studio 2013 Express：

   3. 在方案總管中，以滑鼠右鍵按一下 FixIt 方案，然後選取 [**屬性**]。
   4. 選取 [**多個啟始專案**]。
   5. 在 [MyFixIt 和 MyFixItCloudService] 底下的 [**動作**] 下拉式清單中，選取 [**啟動**]。
   6. 按一下 [確定]。
   7. 按**F5**執行這兩個專案。

      當您執行 MyFixItCloudService 專案時，Visual Studio 會啟動 Azure 計算模擬器。 視您的防火牆設定而定，您可能需要允許模擬器通過防火牆。

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a>如何使用 Windows PowerShell 腳本將基本應用程式部署至 Azure App Service Web Apps

為了說明「[自動化所有專案](automate-everything.md)」模式，您可以使用在 Azure 中設定環境並將專案部署到新環境的腳本來提供修正 It 應用程式。 下列指示說明如何使用腳本。

如果您想要在 Azure 中執行而不使用佇列，而且您已將變更設定為使用佇列在本機執行，請務必將 UseQueues appSetting 值設回 false，再繼續進行下列指示。

這些指示假設您已在本機下載並執行 Fix It 解決方案，而且您有 Azure 帳戶，或擁有您有權管理的 Azure 訂用帳戶。

1. 安裝**Azure PowerShell**主控台。 如需指示，請參閱[如何安裝和設定 Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)。

    此自訂的主控台已設定為可與您的 Azure 訂用帳戶搭配使用。 Azure 模組會安裝在*Program Files*目錄中，而且會在每次使用 Azure PowerShell 主控台時自動匯入。

    如果您想要在不同的主機程式（例如 Windows PowerShell ISE）中工作，請務必使用[import-module](https://go.microsoft.com/fwlink/?LinkID=141553) Cmdlet 來匯入 azure 模組，或使用 azure 模組中的命令來觸發模組的自動匯入。
2. 使用 [以**系統管理員身分執行**] 選項啟動 Azure PowerShell。
3. 執行[ExecutionPolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) Cmdlet，將 Azure PowerShell 執行原則設定為 `RemoteSigned`。 輸入**Y** （為 [是]）來完成原則變更。

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    此設定可讓您執行未數位簽署的本機腳本。 （您也可以將執行原則設定為 `Unrestricted`，這樣就不需要在稍後解除封鎖步驟的需求，但基於安全性理由，不建議這樣做）。
4. 執行 `Add-AzureAccount` Cmdlet，使用您帳戶的認證來設定 PowerShell。

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    這些認證會在一段時間後到期，您必須重新執行 `Add-AzureAccount` Cmdlet。 在撰寫此電子書時，認證到期前的時間限制為12小時。
5. 如果您有多個訂用帳戶，請使用 Set-azuresubscription Cmdlet 來指定您想要在其中建立測試環境的訂閱。
6. 使用 `Get-AzurePublishSettingsFile` 和 `Import-AzurePublishSettingsFile` Cmdlet，匯入相同 Azure 訂用帳戶的管理憑證。 這些 Cmdlet 的第一個會下載憑證檔案，而在第二個檔案中，您可以指定該檔案的位置，以便匯入該檔案。 > [!IMPORTANT]
   > 將下載的檔案保留在安全的位置，或在完成時將它刪除，因為它包含可用來管理 Azure 服務的憑證。

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    憑證用於偵測開發電腦的 IP 位址的 REST API 呼叫，以便在 SQL Database 伺服器上設定防火牆規則。
7. 執行[設定位置](https://go.microsoft.com/fwlink/p/?linkid=293912)Cmdlet （別名是 `cd`、`chdir`和 `sl`），以流覽至包含腳本的目錄。 （它們位於 [修正 It] 方案資料夾的 [*自動化*] 資料夾中）。如果有任何目錄名稱包含空格，請以引號括住路徑。 例如，若要流覽至 `c:\Sample Apps\FixIt\Automation` 目錄，您可以輸入下列命令：

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. 若要允許 Windows PowerShell 執行這些腳本，請使用 [[解除封鎖-](https://go.microsoft.com/fwlink/p/?linkid=294021)檔案] Cmdlet。 （腳本會遭到封鎖，因為它們是從網際網路下載）。

    > [!WARNING]
    > 安全性-在任何腳本或可執行檔上執行 `Unblock-File` 之前，請在 [記事本] 中開啟檔案，檢查命令，並確認它們不包含任何惡意程式碼。

    例如，下列命令會在目前目錄中的所有腳本上執行 `Unblock-File` Cmdlet。

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. 若要建立基底的 web 應用程式（沒有佇列處理），請修正 It 應用程式，執行環境建立腳本。

    必要的 `Name` 參數會指定資料庫的名稱，而且也會用於腳本所建立的儲存體帳戶。 此名稱在 azurewebsites.net 網域內必須是全域唯一的。 如果您指定的名稱不是唯一的，例如 Fixit 或 Test （或甚至在範例中為 fixitdemo），則 `New-AzureWebsite` Cmdlet 會失敗，並產生報告衝突的內部錯誤。 腳本會將名稱轉換為所有小寫，以符合 web 應用程式、儲存體帳戶和資料庫的名稱需求。

    必要的 `SqlDatabasePassword` 參數會指定將針對 SQL Database 建立之系統管理員帳戶的密碼。 請勿在密碼中包含特殊的 XML 字元（&amp; &lt; &gt;;)。 這是撰寫腳本的方式限制，而不是 Azure 的限制。

    例如，如果您想要建立名為 "fixitdemo" 的 web 應用程式，並使用 "Passw0rd1" 的 SQL Server 系統管理員密碼，您可以輸入下列命令：

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    此名稱在 azurewebsites.net 網域中必須是唯一的，且密碼必須符合密碼複雜性 SQL Database 需求。 （範例 Passw0rd1 符合需求）。

    請注意，命令的開頭是 "。\"。 為了協助防止惡意執行腳本，Windows PowerShell 會要求您在執行腳本時提供腳本檔案的完整路徑。 您可以使用點來表示目前的目錄（"。\"）或提供完整路徑，例如：

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    如需腳本的詳細資訊，請使用 `Get-Help` Cmdlet。

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    您可以使用 Get-help Cmdlet 的 `Detailed`、`Full`、`Parameters`和 `Examples` 參數來篩選所傳回的說明。

    如果腳本失敗或產生錯誤，例如 "AzureWebsite：呼叫 Set-azuresubscription 並選取-Set-azuresubscription first，「您可能尚未完成 Azure PowerShell 的設定。

    腳本完成之後，您可以使用 Azure 管理入口網站查看已建立的資源，如[自動化所有事項](automate-everything.md)一章所示。
10. 若要將 FixIt 專案部署到新的 Azure 環境，請使用*AzureWebsite*腳本。 例如:

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    部署完成時，瀏覽器會開啟並修正在 Azure 中執行的問題。

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a>疑難排解 Windows PowerShell 腳本

執行這些腳本時最常遇到的錯誤與許可權相關。 請確定 `Add-AzureAccount` 和 `Import-AzurePublishSettingsFile` 成功，而且您已將它們用於相同的 Azure 訂用帳戶。 即使 `Add-AzureAccount` 成功，您可能必須再次執行。 `Add-AzureAccount` 新增的許可權會在12小時內過期。

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a>並未將物件參考設定為物件的執行個體。

如果腳本傳回錯誤，例如「物件參考未設定為物件的實例」，這表示 Windows PowerShell 找不到要處理的物件（這是 null 參考例外狀況），請執行 `Add-AzureAccount` Cmdlet，然後再試一次腳本。

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a>InternalError伺服器發生內部錯誤。

當 azurewebsites.net 網域中的名稱不是唯一時，`New-AzureWebsite` Cmdlet 會傳回內部錯誤。 若要解決此錯誤，請使用不同的名稱值，也就是*New-AzureWebsiteEnv*的 name 參數。

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a>重新開機腳本

如果您需要重新開機*New-AzureWebsiteEnv*腳本，因為它在列印「腳本已完成」訊息之前失敗，您可能會想要刪除腳本停止之前所建立的資源。 例如，如果腳本已經建立 ContosoFixItDemo web 應用程式，而且您以相同的名稱再次執行腳本，腳本將會失敗，因為名稱正在使用中。

若要判斷腳本在停止之前所建立的資源，請使用下列 Cmdlet：

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- `Get-AzureSqlDatabase`：若要執行此 Cmdlet，請以管線將資料庫伺服器名稱傳送至 `Get-AzureSqlDatabase`： `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`

若要刪除這些資源，請使用下列命令。 請注意，如果您刪除資料庫伺服器，就會自動刪除與伺服器相關聯的資料庫。

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a>如何將具有佇列處理的應用程式部署至 Azure App Service Web Apps 和 Azure 雲端服務

若要啟用佇列，請在 MyFixIt\Web.config 檔案中進行下列變更。 在 [`appSettings`] 底下，將 `UseQueues` 的值變更為 "true"：

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

然後在 Azure App Service 中，將 MVC 應用程式部署至 web 應用程式，如[先前](#deploybase)所述。

接下來，建立新的 Azure 雲端服務。 Fix It 應用程式隨附的腳本不會建立或部署雲端服務，因此您必須為此使用 Azure 入口網站。 在入口網站中，按一下 **新增** -- **計算**–**雲端服務** -- **快速建立**，然後輸入 URL 和資料中心位置。 使用您部署 web 應用程式所在的相同資料中心。

![](the-fix-it-sample-application/_static/image1.png)

在您可以部署雲端服務之前，您必須先更新一些設定檔。

在 MyFixIt 中的 `connectionStrings`底下，將 `appdb` 連接字串的值取代為 SQL Database 的實際連接字串。 您可以從入口網站取得連接字串。 在入口網站中，按一下 [ **SQL 資料庫**] - **appdb** - **VIEW SQL Database ADO .net、ODBC、PHP 和 JDBC 的連接字串**。 複製 ADO.NET 連接字串，並將值貼到 app.config 檔案中。 將「{您的\_密碼\_這裡}」取代為您的資料庫密碼。 （假設您使用腳本來部署 MVC 應用程式，您已在 `SqlDatabasePassword` 腳本參數中指定資料庫密碼）。

結果看起來應該如下所示：

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

在相同的 MyFixIt WorkerRole\app.config 檔案中，于 `appSettings`底下，取代 Azure 儲存體帳戶的兩個預留位置值。

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

您可以從入口網站取得存取金鑰。 請參閱[如何管理儲存體帳戶](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)。

在 MyFixItCloudService\ServiceConfiguration.Cloud.cscfg 中，將 Azure 儲存體帳戶的兩個預留位置值取代為相同。

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

現在您已準備好部署雲端服務。 在 [方案探索] 中，以滑鼠右鍵按一下 MyFixItCloudService 專案，然後選取 [**發佈**]。 如需詳細資訊，請參閱[本教學](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)課程的第2部分中的「將[應用程式部署到 Azure](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)」。

> [!div class="step-by-step"]
> [上一步](more-patterns-and-guidance.md)
