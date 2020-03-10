---
uid: mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-cs
title: '反復專案 #5 –建立單元測試C#（） |Microsoft Docs'
author: microsoft
description: 在第五個反復專案中，我們會藉由新增單元測試，讓應用程式更容易維護和修改。 我們會模擬我們的資料模型類別，並建立適用于 o 的單元測試 。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 28ad8f80-b8a5-444e-b478-8b15a846060c
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-cs
msc.type: authoredcontent
ms.openlocfilehash: 32e81cce34a0e0b1f6b01934334e1b66dce89651
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544300"
---
# <a name="iteration-5--create-unit-tests-c"></a>反復專案 #5 –建立單元測試C#（）

由[Microsoft](https://github.com/microsoft)

[下載程式代碼](iteration-5-create-unit-tests-cs/_static/contactmanager_5_cs1.zip)

> 在第五個反復專案中，我們會藉由新增單元測試，讓應用程式更容易維護和修改。 我們會模擬我們的資料模型類別，並為我們的控制器和驗證邏輯建立單元測試。

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>建立連絡人管理 ASP.NET MVC 應用程式（C#）

在這一系列的教學課程中，我們從一開始就建立了整個連絡人管理應用程式。 連絡人管理員應用程式可讓您儲存連絡人資訊名稱、電話號碼和電子郵件地址，以取得人員清單。

我們會透過多個反復專案來建立應用程式。 在每次反覆運算時，我們會逐漸改善應用程式。 這個多個反復專案方法的目標，是要讓您瞭解每項變更的原因。

- 反復專案 #1-建立應用程式。 在第一個反復專案中，我們會以最簡單的方式建立連絡人管理員。 我們新增對基本資料庫作業的支援：建立、讀取、更新和刪除（CRUD）。

- 反復專案 #2-讓應用程式看起來不錯。 在此反復專案中，我們藉由修改預設的 ASP.NET MVC view 主版頁面和級聯樣式表，來改善應用程式的外觀。

- 反復專案 #3-新增表單驗證。 在第三個反復專案中，我們會新增基本表單驗證。 我們會防止人們提交表單，而不需要完成必要的表單欄位。 我們也會驗證電子郵件地址和電話號碼。

- 反復專案 #4-讓應用程式鬆散結合。 在這第四次的反復專案中，我們會利用數種軟體設計模式，讓您更輕鬆地維護和修改 Contact Manager 應用程式。 例如，我們會重構應用程式，以使用存放庫模式和相依性插入模式。

- 反復專案 #5-建立單元測試。 在第五個反復專案中，我們會藉由新增單元測試，讓應用程式更容易維護和修改。 我們會模擬我們的資料模型類別，並為我們的控制器和驗證邏輯建立單元測試。

- 反復專案 #6-使用以測試為導向的開發。 在此第六個反復專案中，我們會先撰寫單元測試，並針對單元測試撰寫程式碼，以將新功能加入至應用程式。 在此反復專案中，我們會新增連絡人群組。

- 反復專案 #7-新增 Ajax 功能。 在第七次的反復專案中，我們藉由新增 Ajax 的支援來改善應用程式的回應性和效能。

## <a name="this-iteration"></a>這個反復專案

在連絡人管理員應用程式的上一個反復專案中，我們重構了應用程式，以進行更鬆散的結合。 我們將應用程式分成不同的控制器、服務和儲存機制層。 每一層都會透過介面與其底下的圖層互動。

我們已重構應用程式，讓應用程式更容易維護和修改。 例如，如果我們需要使用新的資料存取技術，我們可以直接變更存放庫層，而不需要觸及控制器或服務層。 藉由讓連絡人管理員鬆散結合，我們讓應用程式更有彈性地進行變更。

但是，當我們需要將新功能加入至 Contact Manager 應用程式時，會發生什麼事？ 或者，當我們修正 bug 時，會發生什麼事？ 不過，只要您接觸程式碼，就會產生新 bug 的風險，但這是一項很好的證明，那就是撰寫程式碼的事實。

例如，您的經理可能會要求您將新功能新增至連絡人管理員。 她想要加入連絡人群組的支援。 她希望您可以讓使用者將他們的連絡人組織成像是朋友、Business 等等的群組。

若要執行這項新功能，您必須修改 Contact Manager 應用程式的全部三個層級。 您必須將新功能新增至控制器、服務層和存放庫。 一旦您開始修改程式碼，就會有風險的重大功能。

將我們的應用程式重構成不同的層級，如同我們在先前的反復專案中所做的，是個好的。 這是件好事，因為它可讓我們對整個階層進行變更，而不需要觸及應用程式的其餘部分。 不過，如果您想要讓某一層中的程式碼更容易維護和修改，您必須建立程式碼的單元測試。

您可以使用單元測試來測試個別的程式碼單位。 這些程式碼單位小於整個應用層。 一般來說，您會使用單元測試來驗證程式代碼中的特定方法是否以您預期的方式運作。 例如，您可以為 ContactManagerService 類別所公開的 CreateContact （）方法建立單元測試。

應用程式的單元測試就像安全的網路一樣。 每當您修改應用程式中的程式碼時，您可以執行一組單元測試，以檢查修改是否會中斷現有的功能。 單元測試可讓您的程式碼安全地進行修改。 單元測試可讓您應用程式中的所有程式碼更有彈性地進行變更。

在此反復專案中，我們會將單元測試新增至連絡人管理員應用程式。 如此一來，在下一個反復專案中，我們可以將連絡人群組新增至應用程式，而不必擔心中斷現有的功能。

> [!NOTE] 
> 
> 有各種單元測試架構，包括 NUnit、xUnit.net 和 MbUnit。 在本教學課程中，我們會使用 Visual Studio 隨附的單元測試架構。 不過，您可以輕鬆地使用其中一個替代架構。

## <a name="what-gets-tested"></a>已測試的內容

在完美的世界中，單元測試會涵蓋所有程式碼。 在完美的世界中，您會有完美的安全網路。 無論變更是否中斷現有的功能，您都可以藉由執行單元測試來修改應用程式中的任何程式程式碼，並立即得知。

不過，我們不會在完美的世界中生活。 實際上，撰寫單元測試時，您會專注于撰寫商務邏輯的測試（例如，驗證邏輯）。 特別的是，您*不會*為數據存取邏輯或您的 view 邏輯撰寫單元測試。

單元測試必須非常快速地執行，才能發揮效用。 您可以輕鬆地累積應用程式的數百個（甚至數千個）單元測試。 如果單元測試需要很長的時間來執行，則您會避免執行它們。 換句話說，長時間執行的單元測試在日常編碼的用途上毫無用處。

因此，您通常不會針對與資料庫互動的程式碼撰寫單元測試。 對即時資料庫執行數百個單元測試的速度太慢。 相反地，您會模擬資料庫，並撰寫與模擬資料庫互動的程式碼（我們會在下面討論模擬資料庫）。

基於類似的理由，您通常不會針對 views 撰寫單元測試。 為了測試檢視，您必須啟動 web 伺服器。 由於啟動網頁伺服器是相當緩慢的程式，因此不建議您為您的視圖建立單元測試。

如果您的視圖包含複雜的邏輯，則您應該考慮將邏輯移至 Helper 方法中。 您可以針對執行的 Helper 方法撰寫單元測試，而不需要啟動 web 伺服器。

> [!NOTE] 
> 
> 在撰寫單元測試時，撰寫資料存取邏輯或 view 邏輯的測試並不是個好主意，而在建立功能或整合測試時，這些測試可能非常有説明。

> [!NOTE] 
> 
> ASP.NET MVC 是 Web Forms View 引擎。 雖然 Web form View 引擎相依于 web 伺服器，但其他視圖引擎可能不是。

## <a name="using-a-mock-object-framework"></a>使用 Mock 物件架構

在建立單元測試時，您幾乎都需要利用 Mock 物件架構。 Mock 物件架構可讓您在應用程式中建立類別的模擬和 stub。

例如，您可以使用 Mock 物件架構來產生存放庫類別的模擬版本。 如此一來，您就可以在單元測試中使用模擬儲存機制類別，而不是實際的儲存機制類別。 使用 mock 存放庫可讓您在執行單元測試時，避免執行資料庫程式碼。

Visual Studio 不包含 Mock 物件架構。 不過，有數個適用于 .NET framework 的商業和開放原始碼模擬物件架構：

1. Moq-此架構適用于開放原始碼 BSD 授權。 您可以從[https://code.google.com/p/moq/](https://code.google.com/p/moq/)下載 Moq。
2. Rhino 模擬-此架構適用于開放原始碼 BSD 授權。 您可以從[http://ayende.com/projects/rhino-mocks.aspx](http://ayende.com/projects/rhino-mocks.aspx)下載 Rhino 模擬。
3. Typemock Isolator-這是商業架構。 您可以從[http://www.typemock.com/](http://www.typemock.com/)下載試用版。

在本教學課程中，我決定使用 Moq。 不過，您可以輕鬆地使用 Rhino 模擬或 Typemock Isolator 來建立 Contact Manager 應用程式的 Mock 物件。

在您可以使用 Moq 之前，您需要完成下列步驟：

1. 。
2. 在解壓縮下載內容之前，請確定您以滑鼠右鍵按一下檔案，然後按一下標示為 [**解除封鎖**] 的按鈕（請參閱 [圖 1]）。
3. 將下載解壓縮。
4. 以滑鼠右鍵按一下 [ContactManager] 專案中的 [參考] 資料夾，然後選取 [**加入參考**]，即可加入 Moq 元件的參考。 在 [流覽] 索引標籤下，流覽至您解壓縮 Moq 的資料夾，然後選取 [Moq] 元件。 按一下 [確定] 按鈕。
5. 完成這些步驟之後，[參考] 資料夾看起來應該如 [圖 2] 所示。

[![解除封鎖 Moq](iteration-5-create-unit-tests-cs/_static/image1.jpg)](iteration-5-create-unit-tests-cs/_static/image1.png)

**圖 01**：解除封鎖 Moq （[按一下以觀看完整大小的影像](iteration-5-create-unit-tests-cs/_static/image2.png)）

[新增 Moq 之後的 ![參考](iteration-5-create-unit-tests-cs/_static/image2.jpg)](iteration-5-create-unit-tests-cs/_static/image3.png)

**圖 02**：新增 Moq 之後的參考（[按一下以查看完整大小的影像](iteration-5-create-unit-tests-cs/_static/image4.png)）

## <a name="creating-unit-tests-for-the-service-layer"></a>建立服務層的單元測試

讓我們從為我們的 Contact Manager 應用程式服務層建立一組單元測試開始。 我們將使用這些測試來驗證我們的驗證邏輯。

在 ContactManager 專案中建立名為 [模型] 的新資料夾。 接下來，以滑鼠右鍵按一下 [模型] 資料夾，然後選取 [**加入]、[新增測試**]。 [圖 3] 所示的 [**加入新測試**] 對話方塊隨即出現。 選取 [**單元測試**] 範本，並為新的測試 ContactManagerServiceTest.cs 命名。 按一下 [**確定]** 按鈕，將新的測試加入至測試專案。

> [!NOTE] 
> 
> 一般來說，您會想要測試專案的資料夾結構，以符合 ASP.NET MVC 專案的資料夾結構。 例如，您將控制器測試放在 [控制器] 資料夾、[模型] 資料夾中的模型測試等等。

[![Models\ContactManagerServiceTest.cs](iteration-5-create-unit-tests-cs/_static/image3.jpg)](iteration-5-create-unit-tests-cs/_static/image5.png)

**圖 03**： Models\ContactManagerServiceTest.cs （[按一下以觀看完整大小的影像](iteration-5-create-unit-tests-cs/_static/image6.png)）

一開始，我們想要測試 ContactManagerService 類別所公開的 CreateContact （）方法。 我們將建立下列五項測試：

- CreateContact （）-當有效的連絡人傳遞至方法時，CreateContact （）的測試會傳回 true 值。
- CreateContactRequiredFirstName （）-當具有遺漏名字的連絡人傳遞至 CreateContact （）方法時，測試是否將錯誤訊息加入至模型狀態。
- CreateContactRequiredLastName （）-測試將遺失姓氏的連絡人傳遞至 CreateContact （）方法時，會將錯誤訊息加入至模型狀態。
- CreateContactInvalidPhone （）-當具有無效電話號碼的連絡人傳遞至 CreateContact （）方法時，測試是否將錯誤訊息新增至模型狀態。
- CreateContactInvalidEmail （）-測試將具有無效電子郵件地址的連絡人傳遞至 CreateContact （）方法時，會將錯誤訊息加入至模型狀態。

第一次測試會確認有效的連絡人不會產生驗證錯誤。 其餘的測試會檢查每個驗證規則。

這些測試的程式碼包含在 [清單 1] 中。

**清單 1-Models\ContactManagerServiceTest.cs**

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample1.cs)]

因為我們使用 [清單 1] 中的 Contact 類別，所以我們需要在測試專案中加入 Microsoft Entity Framework 的參考。 加入 System.object 元件的參考。

[清單 1] 包含名為 Initialize （）的方法，它會以 [TestInitialize] 屬性裝飾。 在執行每個單元測試之前，會自動呼叫這個方法（在每個單元測試之前都會呼叫5次）。 Initialize （）方法會使用下列程式程式碼建立模擬儲存機制：

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample2.cs)]

這行程式碼會使用 Moq 架構，從 IContactManagerRepository 介面產生 mock 存放庫。 模擬儲存機制會用來取代實際的 EntityContactManagerRepository，以避免在每個單元測試執行時存取資料庫。 Mock 存放庫會實 IContactManagerRepository 介面的方法，但方法不會實際執行任何動作。

> [!NOTE] 
> 
> 使用 Moq 架構時，\_mockRepository 和 \_mockRepository 之間有區別。 前者指的是 Mock&lt;IContactManagerRepository&gt; 類別，其中包含指定模擬儲存機制行為方式的方法。 後者是指實 IContactManagerRepository 介面的實際 mock 存放庫。

建立 ContactManagerService 類別的實例時，會在 Initialize （）方法中使用 mock 存放庫。 所有的個別單元測試都會使用這個 ContactManagerService 類別的實例。

[清單 1] 包含五個對應至每個單元測試的方法。 這些方法都是以 [TestMethod] 屬性裝飾。 當您執行單元測試時，會呼叫具有這個屬性的任何方法。 換句話說，任何以 [TestMethod] 屬性裝飾的方法都是單元測試。

第一個單元測試（名為 CreateContact （））會確認當 Contact 類別的有效實例傳遞給方法時，呼叫 CreateContact （）會傳回 true 值。 此測試會建立 Contact 類別的實例，並呼叫 CreateContact （）方法，並確認 CreateContact （）傳回值 true。

其餘的測試會確認使用不正確連絡人呼叫 CreateContact （）方法時，此方法會傳回 false，而預期的驗證錯誤訊息會加入至模型狀態。 例如，CreateContactRequiredFirstName （）測試會使用其 FirstName 屬性的空字串，建立 Contact 類別的實例。 接下來，使用不正確 Contact 呼叫 CreateContact （）方法。 最後，測試會確認 CreateContact （）傳回 false，而且模型狀態包含預期的驗證錯誤訊息「需要名字。」

您可以選取 [**測試]、[執行]、[方案中的所有測試] （CTRL + R、A）** 中的功能表選項，以執行 [清單 1] 中的單元測試。 測試的結果會顯示在 [測試結果] 視窗中（請參閱 [圖 4]）。

[![測試結果](iteration-5-create-unit-tests-cs/_static/image4.jpg)](iteration-5-create-unit-tests-cs/_static/image7.png)

**圖 04**：測試結果（[按一下以觀看完整大小的影像](iteration-5-create-unit-tests-cs/_static/image8.png)）

## <a name="creating-unit-tests-for-controllers"></a>建立控制器的單元測試

NETMVC 應用程式控制使用者互動的流程。 測試控制器時，您會想要測試控制器是否傳回正確的動作結果和查看資料。 您也可能想要測試控制器是否以預期的方式與模型類別互動。

例如，[清單 2] 包含 Contact controller Create （）方法的兩個單元測試。 第一個單元測試會確認當有效的連絡人傳遞至 Create （）方法時，Create （）方法會重新導向至索引動作。 換句話說，當傳遞有效的連絡人時，Create （）方法應該會傳回代表索引動作的 RedirectToRouteResult。

我們不想在測試控制器層時測試 ContactManager 服務層級。 因此，我們會在 Initialize 方法中，使用下列程式碼來模擬服務層：

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample3.cs)]

在 CreateValidContact （）單元測試中，我們會使用下列程式程式碼來模擬呼叫服務層 CreateContact （）方法的行為：

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample4.cs)]

這行程式碼會在呼叫其 CreateContact （）方法時，讓 mock ContactManager 服務傳回值 true。 藉由模擬服務層級，我們可以測試控制器的行為，而不需要在服務層中執行任何程式碼。

第二個單元測試會在將不正確連絡人傳遞至方法時，確認 Create （）動作是否會傳回 Create view。 我們會讓服務層 CreateContact （）方法以下列程式程式碼傳回 false 值：

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample5.cs)]

如果 Create （）方法如預期般運作，則當服務層傳回 false 值時，應該會傳回 Create view。 如此一來，控制器就可以在 [建立] 視圖中顯示驗證錯誤訊息，而且使用者有機會更正該不正確連絡人屬性。

如果您打算為控制器建立單元測試，則需要從您的控制器動作傳回明確的視圖名稱。 例如，不會傳回如下所示的視圖：

return View （）;

相反地，會傳回如下所示的視圖：

return View （"Create"）;

如果您在傳回 view 時不是明確的，則 ViewResult. ViewName 屬性會傳回空字串。

**清單 2-Controllers\ContactControllerTest.cs**

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample6.cs)]

## <a name="summary"></a>總結

在此反復專案中，我們為連絡人管理員應用程式建立單元測試。 我們可以隨時執行這些單元測試，以確認我們的應用程式仍然以我們預期的方式運作。 單元測試會作為我們應用程式的安全網路，讓我們能夠在未來安全地修改應用程式。

我們建立了兩組單元測試。 首先，我們會藉由建立服務層的單元測試來測試我們的驗證邏輯。 接下來，我們會藉由建立控制器層的單元測試來測試流程式控制制邏輯。 測試我們的服務層時，我們會模擬我們的存放庫層，將我們的服務層級的測試與我們的存放庫層隔離。 測試控制器層時，我們會藉由模擬服務層級，為控制器層隔離測試。

在下一個反復專案中，我們會修改 Contact Manager 應用程式，使其支援連絡人群組。 我們會使用稱為「測試導向開發」的軟體設計程式，將這種新功能新增至我們的應用程式。

> [!div class="step-by-step"]
> [上一頁](iteration-4-make-the-application-loosely-coupled-cs.md)
> [下一頁](iteration-6-use-test-driven-development-cs.md)
