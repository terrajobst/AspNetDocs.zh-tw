---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: 啟用自動化單元測試 |Microsoft Docs
author: microsoft
description: 步驟12顯示如何開發一套自動化單元測試，以驗證我們的 NerdDinner 功能，讓我們有信心進行變更 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 09a7aa186605a6cce48ee94028425ded957c00d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541675"
---
# <a name="enable-automated-unit-testing"></a>啟用自動化單元測試

由[Microsoft](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟12，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。
> 
> 步驟12顯示如何開發一套自動化單元測試，以驗證我們的 NerdDinner 功能，讓我們有信心在未來對應用程式進行變更和改進。
> 
> 如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。

## <a name="nerddinner-step-12-unit-testing"></a>NerdDinner 步驟12：單元測試

讓我們來開發一套自動化單元測試，以驗證我們的 NerdDinner 功能，讓我們有信心在未來對應用程式進行變更和改進。

### <a name="why-unit-test"></a>為何要進行單元測試？

在一早上的磁片磁碟機上，您對正在處理的應用程式有非常快的靈感。 您已瞭解您可以執行的變更，讓應用程式大幅提升。 它可能是可清除程式碼、加入新功能或修正 bug 的重構。

當您抵達電腦時，confronts 您的問題就是：「要如何保障這方面的改進？」 如果進行變更有副作用或中斷某個專案，該怎麼辦？ 這項變更可能很簡單，只需要幾分鐘的時間才能完成，但如果需要數小時才能手動測試所有應用程式案例，該怎麼辦？ 如果您忘記涵蓋案例，而中斷的應用程式進入生產階段該怎麼辦？ 這種改進功能真的值得嗎？

自動化單元測試可以提供安全網路，讓您持續增強應用程式，並避免害怕您正在處理的程式碼。 擁有可快速驗證功能的自動化測試可讓您安心編寫程式碼，並可讓您在其他情況不熟悉的情況進行改善。 它們也有助於建立更能維護的解決方案，並具有較長的存留期，這會導致投資的報酬率更高。

ASP.NET MVC 架構可讓您輕鬆且自然地進行單元測試應用程式功能。 它也會啟用測試導向開發（TDD）工作流程，以進行以測試為基礎的開發。

### <a name="nerddinnertests-project"></a>NerdDinner 測試專案

當我們在本教學課程一開始建立 NerdDinner 應用程式時，會出現一個對話方塊詢問您是否想要建立單元測試專案來與應用程式專案一起執行：

![](enable-automated-unit-testing/_static/image1.png)

我們已選取 [是，建立單元測試專案] 選項按鈕，這會在解決方案中加入「NerdDinner」專案：

![](enable-automated-unit-testing/_static/image2.png)

NerdDinner 專案會參考 NerdDinner 應用程式專案元件，並可讓我們輕鬆地將自動化測試加入其中，以驗證應用程式的功能。

### <a name="creating-unit-tests-for-our-dinner-model-class"></a>建立晚餐模型類別的單元測試

讓我們將一些測試新增至我們的 NerdDinner。測試專案，以驗證我們在建立模型層時所建立的晚餐類別。

首先，我們會在名為「模型」的測試專案中建立新的資料夾，我們將在其中放置模型相關的測試。 然後，在資料夾上按一下滑鼠右鍵，然後選擇 [**加入&gt;新增測試**] 功能表命令。 這會顯示 [加入新測試] 對話方塊。

我們會選擇建立「單元測試」，並將它命名為 "DinnerTest.cs"：

![](enable-automated-unit-testing/_static/image3.png)

當我們按一下 [確定] 按鈕時 Visual Studio 會將 DinnerTest.cs 檔案新增（並開啟）至專案：

![](enable-automated-unit-testing/_static/image4.png)

預設 Visual Studio 單元測試範本內有一堆定案板程式碼，我發現有點雜亂。 讓我們將它清除，只包含下列程式碼：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

上述 DinnerTest 類別上的 [TestClass] 屬性會將它識別為包含測試的類別，以及選擇性的測試初始化和終止程式碼。 我們可以在其中新增具有 [TestMethod] 屬性的公用方法，以定義其中的測試。

以下是我們要加入的兩個測試中的第一個，以練習我們的晚餐課程。 第一次測試會確認在建立新晚餐時，我們的晚餐無效，而不會正確設定所有屬性。 第二個測試會在晚餐將所有屬性設為有效的值時，驗證晚餐是否有效：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

您會注意到，我們的測試名稱非常明確（而且有點詳細）。 我們會執行這項作業，因為我們可能會建立數百或數千個小型測試，而我們想要讓快速判斷其中每個的意圖和行為（尤其是當我們在測試執行器中尋找失敗的清單時）。 測試名稱應該以測試的功能命名。 在上述情況中，我們會使用「名詞\_應該\_動詞」命名模式。

我們會使用「AAA」測試模式來結構化測試，這代表「安排、Act、判斷提示」：

- 排列：設定要測試的單元
- Act：練習受測單元並捕獲結果
- Assert：驗證行為

當我們撰寫測試時，我們想要避免個別測試執行得太多。 相反地，每個測試只應驗證單一概念（這可讓您更容易找出失敗的原因）。 最好的指導方針是針對每項測試只使用單一的 assert 語句。 如果您在測試方法中有一個以上的 assert 語句，請確定它們全都用來測試相同的概念。 若不確定，請進行另一個測試。

### <a name="running-tests"></a>正在執行測試

Visual Studio 2008 Professional （及更新版本）包含內建的測試執行器，可用來在 IDE 中執行 Visual Studio 單元測試專案。 我們可以在 [方案] 功能表命令**中選取測試&gt;的執行&gt;所有測試**（或輸入 Ctrl R、A）來執行我們所有的單元測試。 或者，我們可以將游標放在特定測試類別或測試方法中，然後使用**測試&gt;的執行&gt;測試（在目前的內容**功能表命令中，或輸入 Ctrl R、t）來執行單元測試的子集。

讓我們將游標放在 DinnerTest 類別內，然後輸入 "Ctrl R，T" 來執行我們剛才定義的兩個測試。 當我們這麼做時，[測試結果] 視窗會出現在 Visual Studio 內，而我們會看到測試回合的結果列在其中：

![](enable-automated-unit-testing/_static/image5.png)

*注意： [VS test 結果] 視窗預設不會顯示 [類別名稱] 資料行。您可以在 [測試結果] 視窗內按一下滑鼠右鍵，然後使用 [新增/移除資料行] 功能表命令來加入這個。*

我們的兩個測試只需要一小部分的時間來執行，您就可以看到兩者都通過了。 我們現在可以藉由建立可驗證特定規則驗證的其他測試，並涵蓋我們已新增至晚餐類別的兩個 helper 方法（IsUserHost （）和 IsUserRegistered （）），來增強它們。 將所有這些測試都用於晚餐課程，可讓您更輕鬆且更安全地在未來加入新的商務規則和驗證。 我們可以將新的規則邏輯新增至晚餐，然後在幾秒內確認它尚未中斷先前所有的邏輯功能。

請注意，使用描述性測試名稱可讓您輕鬆快速地瞭解每個測試的驗證。 我建議您使用 [**工具-&gt;選項**] 功能表命令，開啟 [測試控管-&gt;測試執行設定] 畫面，然後勾選 [按兩下失敗或不明的單元測試結果] 核取方塊中的 [失敗點]。 這可讓您在 [測試結果] 視窗中按兩下失敗，並立即跳到判斷提示失敗。

### <a name="creating-dinnerscontroller-unit-tests"></a>建立 DinnersController 單元測試

現在讓我們建立一些單元測試，以驗證我們的 DinnersController 功能。 首先，以滑鼠右鍵按一下測試專案中的 [控制器] 資料夾，然後選擇 [**加入-&gt;新增測試**] 功能表命令。 我們會建立「單元測試」，並將它命名為 "DinnersControllerTest.cs"。

我們將建立兩個測試方法，以確認 DinnersController 上的 Details （）動作方法。 第一個會驗證當要求現有晚餐時，會傳回一個視圖。 第二個驗證會在要求不存在的晚餐時，確認傳回「NotFound」視圖：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

上述程式碼會編譯乾淨的。 不過，當我們執行測試時，它們會失敗：

![](enable-automated-unit-testing/_static/image6.png)

如果我們查看錯誤訊息，我們會看到測試失敗的原因是因為我們的 DinnersRepository 類別無法連接到資料庫。 我們的 NerdDinner 應用程式會使用本機 SQL Server Express 檔案的連接字串，此檔案位於 NerdDinner 應用程式專案的 \App\_Data 目錄底下。 因為我們的 NerdDinner 會在不同的目錄中編譯並執行，所以在應用程式專案中，連接字串的相對路徑位置不正確。

我們*可以*藉由將 SQL Express 資料庫檔案複製到測試專案，然後在測試專案的 app.config 中為其新增適當的測試連接字串，來修正此問題。 這會讓上述測試解除封鎖且正在執行。

不過，使用實際資料庫的單元測試程式碼會帶來許多挑戰。 尤其是：

- 它會大幅降低單元測試的執行時間。 執行測試所花費的時間愈長，通常執行的可能性就越低。 在理想的情況下，您會想要讓單元測試能夠在幾秒鐘內執行，並以自然的方式來編譯專案。
- 它會使測試中的設定和清除邏輯變得複雜。 您想要讓每個單元測試獨立，並與其他人獨立（不會有副作用或相依性）。 在處理實際的資料庫時，您必須留意狀態，並在測試之間重設它。

讓我們看一下稱為「相依性插入」的設計模式，可協助我們解決這些問題，並避免需要在測試中使用實際的資料庫。

### <a name="dependency-injection"></a>相依性插入

現在 DinnersController 已緊密地「結合」至 DinnerRepository 類別。 「結合」指的是類別明確依賴另一個類別才能正常執行的情況：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

由於 DinnerRepository 類別需要存取資料庫，因此 DinnersController 類別在 DinnerRepository 上具有緊密結合的相依性，最後需要我們擁有資料庫，才能測試 DinnersController 動作方法。

我們可以藉由採用稱為「相依性插入」的設計模式來解決此問題，這種方法會在使用它們的類別內不再以隱含方式建立相依性（例如提供資料存取的儲存機制類別）。 相反地，您可以使用函式引數，將相依性明確傳遞給使用它們的類別。 如果使用介面來定義相依性，我們就可以彈性地針對單元測試案例傳入「假」相依性執行。 這可讓我們建立不需要存取資料庫的測試特定相依性。

若要查看其實際運作情況，讓我們使用 DinnersController 來執行相依性插入。

#### <a name="extracting-an-idinnerrepository-interface"></a>解壓縮 IDinnerRepository 介面

我們的第一個步驟是建立新的 IDinnerRepository 介面，以封裝我們的控制器需要取得和更新 Dinners 的儲存機制合約。

我們可以用滑鼠右鍵按一下 [\Models] 資料夾，然後選擇 [**加入-&gt;新專案**] 功能表命令，並建立名為 IDinnerRepository.cs 的新介面，以手動方式定義此介面合約。

或者，我們可以使用內建 Visual Studio Professional （和更新版本）的重構工具，從現有的 DinnerRepository 類別自動為我們解壓縮並建立介面。 若要使用 VS 來解壓縮此介面，只要將游標放在 [DinnerRepository] 類別的文字編輯器中，然後以滑鼠右鍵按一下並選擇 [**重構-&gt;解壓縮介面**] 功能表命令：

![](enable-automated-unit-testing/_static/image7.png)

這會啟動 [解壓縮介面] 對話方塊，並提示我們輸入要建立之介面的名稱。 它會預設為 IDinnerRepository，並在現有的 DinnerRepository 類別上自動選取要新增至介面的所有公用方法：

![](enable-automated-unit-testing/_static/image8.png)

當我們按一下 [確定] 按鈕時，Visual Studio 會將新的 IDinnerRepository 介面新增至我們的應用程式：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

而我們現有的 DinnerRepository 類別將會更新，使其能夠執行介面：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a>更新 DinnersController 以支援函數插入

我們現在會更新 DinnersController 類別，以使用新的介面。

目前 DinnersController 是硬式編碼，因此它的 "dinnerRepository" 欄位一律是 DinnerRepository 類別：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

我們會將它變更，讓 "dinnerRepository" 欄位的類型是 IDinnerRepository，而不是 DinnerRepository。 接著，我們會新增兩個公用 DinnersController 的函式。 其中一個函式允許將 IDinnerRepository 當做引數傳遞。 另一個則是使用現有 DinnerRepository 執行的預設函式：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

由於 ASP.NET MVC 預設會使用預設的函式建立控制器類別，因此我們在執行時間的 DinnersController 會繼續使用 DinnerRepository 類別來執行資料存取。

不過，我們現在可以使用參數的函式，更新我們的單元測試，以傳入「假」晚餐存放庫的實施。 此「假」晚餐存放庫將不需要存取實際的資料庫，而是會使用記憶體中的範例資料。

#### <a name="creating-the-fakedinnerrepository-class"></a>建立 FakeDinnerRepository 類別

讓我們來建立 FakeDinnerRepository 類別。

我們會先在 NerdDinner 中建立 "Fakes" 目錄，然後在其中新增 FakeDinnerRepository 類別（以滑鼠右鍵按一下該資料夾，然後選擇 [新增 **-&gt;新類別**]）：

![](enable-automated-unit-testing/_static/image9.png)

我們將更新程式碼，讓 FakeDinnerRepository 類別能夠執行 IDinnerRepository 介面。 然後，我們可以在其上按一下滑鼠右鍵，然後選擇 [執行介面 IDinnerRepository] 內容功能表命令：

![](enable-automated-unit-testing/_static/image10.png)

這會導致 Visual Studio 自動將所有 IDinnerRepository 介面成員新增至我們的 FakeDinnerRepository 類別，其具有預設「存根 out」的實作為：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

然後，我們可以更新 FakeDinnerRepository 的執行，以從記憶體中清單中取出&lt;晚餐&gt; 集合做為「函式引數」傳遞給它：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

我們現在有一個不需要資料庫的假 IDinnerRepository，而可以改為處理晚餐物件的記憶體中清單。

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a>搭配單元測試使用 FakeDinnerRepository

讓我們回到先前失敗的 DinnersController 單元測試，因為資料庫無法使用。 我們可以使用下列程式碼，將測試方法更新為使用已填入範例記憶體中晚餐資料的 FakeDinnerRepository 至 DinnersController：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

現在，當我們執行這些測試時，它們都會通過：

![](enable-automated-unit-testing/_static/image11.png)

最棒的是，它們只需要一小部分的時間來執行，而且不需要任何複雜的設定/清除邏輯。 我們現在可以對所有 DinnersController 動作方法程式碼（包括清單、分頁、詳細資料、建立、更新和刪除）進行單元測試，而不需要連接到實際的資料庫。

| **側邊主題：相依性插入架構** |
| --- |
| 執行手動相依性插入（如上所示）可以正常運作，但隨著應用程式中的相依性和元件數目增加而變得更難維護。 有數個適用于 .NET 的相依性插入架構，可協助提供更多相依性管理的彈性。 這些架構（有時也稱為「控制反轉」（IoC）容器）提供了一種機制，可讓您在執行時間指定和傳遞相依性給物件（最常使用的是函式插入）). .NET 中一些較受歡迎的 OSS 相依性插入/IOC 架構包括： AutoFac、Ninject、Spring.NET、StructureMap 和 Windsor。 ASP.NET MVC 會公開擴充性 Api，讓開發人員可以參與控制器的解析和具現化，讓相依性插入/IoC 架構在此程式內完全整合。 使用 DI/IOC 架構也可讓我們從我們的 DinnersController 移除預設的處理函式，這會完全移除其與 DinnerRepository 之間的結合。 我們不會將相依性插入/IOC 架構與我們的 NerdDinner 應用程式搭配使用。 但是，如果 NerdDinner 的程式碼基底和功能成長，我們就可以考慮這一點。 |

### <a name="creating-edit-action-unit-tests"></a>建立編輯動作單元測試

現在讓我們建立一些單元測試，以驗證 DinnersController 的編輯功能。 首先，我們會測試編輯動作的 HTTP GET 版本：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

我們將建立一項測試，以驗證當要求了有效的晚餐時，會將 DinnerFormViewModel 物件所支援的視圖呈現回來：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

不過，當我們執行測試時，我們會發現它會失敗，因為當編輯方法存取 User.Identity.Name 屬性來執行 IsHostedBy （）檢查時，會擲回 null 參考例外狀況。

控制器基類上的 User 物件會封裝已登入使用者的詳細資料，並在執行時間建立控制器時，藉由 ASP.NET MVC 來填入。 因為我們要在 web 伺服器環境外測試 DinnersController，所以不會設定 User 物件（因此是 null 參考例外狀況）。

### <a name="mocking-the-useridentityname-property"></a>模擬 User.Identity.Name 屬性

模擬架構可讓我們以動態方式建立支援測試的假版本相依物件，使測試變得更容易。 例如，我們可以使用編輯動作測試中的模擬架構，以動態方式建立一個使用者物件，讓我們的 DinnersController 可用來查閱模擬的使用者名稱。 這可避免在執行測試時擲回 null 參考。

有許多 .NET 模擬架構可以搭配 ASP.NET MVC 使用（您可以在這裡看到其清單： [http://www.mockframeworks.com/](http://www.mockframeworks.com/)）。 若要測試我們的 NerdDinner 應用程式，我們將使用名為 "Moq" 的開放原始碼模擬架構，可從[http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq)免費下載。

下載之後，我們會將 NerdDinner 中的參考新增至 Moq 元件：

![](enable-automated-unit-testing/_static/image12.png)

接著，我們會將 "CreateDinnersControllerAs （username）" 協助程式方法新增至我們的測試類別，並採用使用者名稱做為參數，然後在 DinnersController 實例上「模擬」 User.Identity.Name 屬性：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

在上述情況下，我們會使用 Moq 來建立模擬物件，以 fakes ControllerCoNtext 物件（這是 ASP.NET MVC 傳遞至控制器類別以公開執行時間物件（例如 User、Request、Response 和 Session）的模型。 我們會在 Mock 上呼叫 "SetupGet" 方法，以指出 ControllerCoNtext 上的 HttpCoNtext.User.Identity.Name 屬性應傳回我們傳遞至 helper 方法的使用者名稱字串。

我們可以模擬任意數目的 ControllerCoNtext 屬性和方法。 為了說明這一點，我也新增了 IsAuthenticated 屬性的 SetupGet （）呼叫（下面的測試實際上不需要這麼做），但這有助於說明您可以如何模擬要求屬性。 當我們完成時，我們會將 ControllerCoNtext mock 的實例指派給我們的 helper 方法所傳回的 DinnersController。

我們現在可以撰寫單元測試，使用此 helper 方法來測試牽涉到不同使用者的編輯案例：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

現在，當我們執行其通過的測試時：

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a>測試 UpdateModel （）案例

我們已建立涵蓋編輯動作之 HTTP GET 版本的測試。 現在讓我們建立一些測試，以驗證編輯動作的 HTTP POST 版本：

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

我們使用這個動作方法來支援有趣的新測試案例，就是在控制器基類上使用 UpdateModel （） helper 方法。 我們會使用此 helper 方法，將表單張貼值系結至晚餐物件實例。

以下兩個測試示範如何提供表單張貼值，讓 UpdateModel （） helper 方法可供使用。 我們的作法是建立和填入 FormCollection 物件，然後將它指派給控制器上的 "ValueProvider" 屬性。

第一個測試會確認在成功儲存時，瀏覽器會重新導向至 [詳細資料] 動作。 第二個測試會確認在張貼不正確輸入時，動作會再次重新顯示編輯檢視，並顯示錯誤訊息。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a>測試總結

我們已討論過單元測試控制器類別所牽涉到的核心概念。 我們可以使用這些技術來輕鬆建立數百個簡單的測試，以驗證應用程式的行為。

因為我們的控制器和模型測試並不需要實際的資料庫，所以非常快速且容易執行。 我們可以在幾秒鐘內執行數百個自動化測試，並立即取得對我們所做的變更是否中斷的意見反應。 這將有助於讓我們安心地持續改進、重構和精簡應用程式。

我們在本章的最後一個主題中討論過測試，但不是因為測試是您應該在開發流程結束時執行的作業！ 相反地，您應該在開發過程中儘早撰寫自動化測試。 這麼做可讓您在開發時立即取得意見反應，協助您思考 thoughtfully 應用程式使用案例的相關資訊，並引導您在設計應用程式時，使用乾淨的分層和結合。

本書稍後的章節將討論「測試導向開發」（TDD），以及如何搭配 ASP.NET MVC 來使用它。 TDD 是一種反復的編碼做法，您可以在其中先撰寫所產生之程式碼所能滿足的測試。 有了 TDD，您就可以藉由建立測試來驗證您即將執行的功能，以開始每項功能。 第一次撰寫單元測試有助於確保您清楚瞭解此功能，以及應該如何使用它。 只有在撰寫測試之後（而且您已驗證失敗）之後，才會執行測試所驗證的實際功能。 因為您已經花時間思考此功能應如何運用的使用案例，所以您將會進一步瞭解需求和其最佳執行方式。 完成執行時，您可以重新執行測試，並立即取得此功能是否正常運作的意見反應。 我們將在第10章討論 TDD。

### <a name="next-step"></a>後續步驟

最後總結批註。

> [!div class="step-by-step"]
> [上一頁](use-ajax-to-implement-mapping-scenarios.md)
> [下一頁](nerddinner-wrap-up.md)
