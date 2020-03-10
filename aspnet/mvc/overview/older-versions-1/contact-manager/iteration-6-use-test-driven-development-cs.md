---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
title: '反復專案 #6 –使用測試導向的開發C#（） |Microsoft Docs'
author: microsoft
description: 在此第六個反復專案中，我們會先撰寫單元測試，並針對單元測試撰寫程式碼，以將新功能加入至應用程式。 在此反復專案中,。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 013c3c26-7dc3-41d1-8064-f233c86008b5
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
msc.type: authoredcontent
ms.openlocfilehash: aee0ff9d8d7f17e8a00dab12467bd3a3457fbe18
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601798"
---
# <a name="iteration-6--use-test-driven-development-c"></a>反復專案 #6 –使用測試導向的開發C#（）

由[Microsoft](https://github.com/microsoft)

[下載程式代碼](iteration-6-use-test-driven-development-cs/_static/contactmanager_6_cs1.zip)

> 在此第六個反復專案中，我們會先撰寫單元測試，並針對單元測試撰寫程式碼，以將新功能加入至應用程式。 在此反復專案中，我們會新增連絡人群組。

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

在連絡人管理員應用程式的上一個反復專案中，我們建立了單元測試，以提供程式碼的安全網路。 建立單元測試的動機是讓我們的程式碼更有彈性地進行變更。 當單元測試就緒時，我們可以對程式碼進行任何變更，並立即知道我們是否已中斷現有的功能。

在此反復專案中，我們將單元測試用於完全不同的用途。 在此反復專案中，我們使用單元測試做為應用程式設計原理的一部分，稱為「*測試導向開發*」。 當您練習以測試為導向的開發時，您會先撰寫測試，然後針對測試撰寫程式碼。

更精確地說，在練習以測試為導向的開發時，您可以在建立程式碼時完成三個步驟（紅色/綠色/重構）：

1. 撰寫失敗的單元測試（紅色）
2. 撰寫通過單元測試的程式碼（綠色）
3. 重構您的程式碼（重構）

首先，您要撰寫單元測試。 單元測試應該表示您希望程式程式碼為的意圖。 當您第一次建立單元測試時，單元測試應該會失敗。 測試應該會失敗，因為您尚未撰寫任何符合測試的應用程式代碼。

接下來，您只需要撰寫足夠的程式碼，單元測試才會通過。 其目標是以 laziest、sloppiest 和最快速的可能方式撰寫程式碼。 您不應該浪費時間思考應用程式的架構。 相反地，您應該專注于撰寫必要的最低程式碼數量，以滿足單元測試所表示的意圖。

最後，在撰寫足夠的程式碼之後，您就可以回溯，並考慮應用程式的整體架構。 在此步驟中，您會利用軟體設計模式（例如存放庫模式）來重寫（重構）程式碼，讓您的程式碼更容易維護。 在此步驟中，您可以 fearlessly 重寫程式碼，因為單元測試涵蓋了您的程式碼。

測試導向的開發會產生許多好處。 首先，以測試為導向的開發會強制您將焦點放在實際需要撰寫的程式碼上。 因為您經常專注于撰寫足夠的程式碼來通過特定測試，所以您無法晃至直搗黃龍，並撰寫您永遠不會使用的大量程式碼。

第二種是「測試優先」設計方法，會強制您從程式碼的使用方式來撰寫程式碼。 換句話說，在練習以測試為導向的開發時，您會經常從使用者的觀點來撰寫您的測試。 因此，以測試為導向的開發可能會產生更清楚且更容易理解的 Api。

最後，以測試為導向的開發會強制您撰寫單元測試，做為撰寫應用程式的一般進程的一部分。 作為專案期限的方法，測試通常是進入視窗的第一件事。 另一方面，當您練習以測試為導向的開發時，您更有可能會良性撰寫單元測試，因為測試導向的開發會使單元測試成為建立應用程式的過程。

> [!NOTE] 
> 
> 若要深入瞭解以測試為導向的開發，建議您閱讀 Michael Feathers 書籍**有效率地使用舊版程式碼**。

在此反復專案中，我們會將新功能新增至我們的 Contact Manager 應用程式。 我們新增了對連絡人群組的支援。 您可以使用連絡人群組，將連絡人組織成像是商務和 Friend 群組的類別。

我們會遵循測試導向開發的程式，將這項新功能新增至我們的應用程式。 我們會先撰寫單元測試，我們會針對這些測試撰寫所有程式碼。

## <a name="what-gets-tested"></a>已測試的內容

如先前的反復專案中所討論，您通常不會針對資料存取邏輯或 view 邏輯撰寫單元測試。 您不會撰寫資料存取邏輯的單元測試，因為存取資料庫是相當緩慢的作業。 您不會針對 view 邏輯撰寫單元測試，因為存取視圖需要加速 web 伺服器，這是相當緩慢的作業。 除非測試可以非常快速地執行，否則您不應該撰寫單元測試

因為測試導向的開發是由單元測試所驅動，所以我們一開始會專注于撰寫控制器和商務邏輯。 我們避免觸及資料庫或 views。 我們不會修改資料庫或建立我們的視圖，直到本教學課程的結尾。 我們先從可測試的內容著手。

## <a name="creating-user-stories"></a>建立使用者故事

在練習以測試為導向的開發時，您一律會開始撰寫測試。 這會立即引發問題：您要如何決定要先撰寫哪一種測試？ 若要回答這個問題，您應該撰寫一組[**使用者故事**](http://en.wikipedia.org/wiki/User_stories)。

使用者故事是軟體需求的簡要說明（通常是一句）。 它應該是從使用者觀點撰寫之需求的非技術性說明。

以下是描述新連絡人群組功能所需功能的一組使用者故事：

1. 使用者可以查看連絡人群組的清單。
2. 使用者可以建立新的連絡人群組。
3. 使用者可以刪除現有的連絡人群組。
4. 使用者可以在建立新的連絡人時選取連絡人群組。
5. 編輯現有的連絡人時，使用者可以選取連絡人群組。
6. 連絡人群組清單會顯示在 [索引] 視圖中。
7. 當使用者按一下連絡人群組時，會顯示相符連絡人的清單。

請注意，客戶可以完全瞭解這份使用者故事清單。 不會提及技術的執行詳細資料。

在建立應用程式的過程中，一組使用者故事可能會變得更加精簡。 您可能會將使用者故事細分為多個案例（需求）。 例如，您可能會決定建立新的連絡人群組應該包含驗證。 提交沒有名稱的連絡人群組時，應該會傳回驗證錯誤。

建立使用者故事清單之後，您就可以開始撰寫第一個單元測試。 首先，我們會建立單元測試來查看連絡人群組的清單。

## <a name="listing-contact-groups"></a>列出連絡人群組

我們的第一個使用者案例是，使用者應該能夠查看連絡人群組的清單。 我們需要使用測試來表達這篇故事。

以滑鼠右鍵按一下 [ContactManager] 專案中的 [控制器] 資料夾，選取 [**加入]、[新增測試**]，然後選取 [**單元測試**] 範本（請參閱 [圖 1]），以建立新的單元測試。 將新的單元測試命名為 GroupControllerTest.cs，然後按一下 [**確定]** 按鈕。

[![新增 GroupControllerTest 單元測試](iteration-6-use-test-driven-development-cs/_static/image1.jpg)](iteration-6-use-test-driven-development-cs/_static/image1.png)

**圖 01**：新增 GroupControllerTest 單元測試（[按一下以觀看完整大小的影像](iteration-6-use-test-driven-development-cs/_static/image2.png)）

第一個單元測試包含在 [清單 1] 中。 這項測試會確認群組控制器的 Index （）方法會傳回一組群組。 此測試會確認群組的集合是否會在 view data 中傳回。

**清單 1-Controllers\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample1.cs)]

當您第一次在 Visual Studio 的 [清單 1] 中輸入程式碼時，您將會得到許多紅色的波浪線。 我們尚未建立 GroupController 或 Group 類別。

此時，我們甚至不能建立我們的應用程式，因此無法執行第一次單元測試。 好了。 這會計算為失敗的測試。 因此，我們現在擁有開始撰寫應用程式程式碼的許可權。 我們需要撰寫足夠的程式碼來執行我們的測試。

[清單 2] 中的群組控制器類別包含傳遞單元測試所需的最少程式碼。 Index （）動作會傳回群組的靜態編碼清單（Group 類別定義于 [清單 3] 中）。

**清單 2-Controllers\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample2.cs)]

**清單 3-Models\Group.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample3.cs)]

將 GroupController 和群組類別加入至專案之後，我們的第一個單元測試就會成功完成（請參閱 [圖 2]）。 我們已完成通過測試所需的最少工作。 這是一種慶祝的時機。

[![成功！](iteration-6-use-test-driven-development-cs/_static/image2.jpg)](iteration-6-use-test-driven-development-cs/_static/image3.png)

**圖 02**：成功！（[按一下以查看完整大小的影像](iteration-6-use-test-driven-development-cs/_static/image4.png)）

## <a name="creating-contact-groups"></a>建立連絡人群組

現在我們可以繼續第二個使用者案例。 我們必須能夠建立新的連絡人群組。 我們需要透過測試來表達這種意圖。

[清單 4] 中的測試會確認以新群組呼叫 Create （）方法時，會將該群組新增至 Index （）方法所傳回的群組清單中。 換句話說，如果我建立新的群組，則應該能夠從 Index （）方法傳回的群組清單中取得新的群組。

**清單 4-Controllers\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample4.cs)]

[清單 4] 中的測試會以新的連絡人群組呼叫群組控制器 Create （）方法。 接下來，測試會確認呼叫群組控制器 Index （）方法會傳回 view data 中的新群組。

[清單 5] 中已修改的群組控制器包含傳遞新測試所需的最少變更。

**清單 5-Controllers\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample5.cs)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a>[清單 5] 中的群組控制器有新的 Create （）動作。 此動作會將群組新增至群組集合。 請注意，索引（）動作已經過修改，可傳回群組集合的內容。

同樣地，我們已執行傳遞單元測試所需的最低工作量。 在對群組控制器進行這些變更之後，我們所有的單元測試都會通過。

## <a name="adding-validation"></a>新增驗證

這項需求並未在使用者案例中明確陳述。 不過，需要群組具有名稱是合理的。 否則，將連絡人組織成群組並不會非常有用。

[清單 6] 包含表示此意圖的新測試。 這項測試會確認嘗試在未提供名稱的情況下建立群組，會導致模型狀態中的驗證錯誤訊息。

**清單 6-Controllers\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample6.cs)]

為了滿足這項測試的需求，我們必須將 Name 屬性新增至我們的 Group 類別（請參閱 [清單 7]）。 此外，我們還需要在群組控制器的 Create （）動作（請參閱 [清單 8]）中新增一個小的驗證邏輯。

**清單 7-Models\Group.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample7.cs)]

**清單 8-Controllers\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample8.cs)]

請注意，[群組控制器建立] （）動作現在同時包含驗證和資料庫邏輯。 目前，群組控制器所使用的資料庫只包含記憶體中的集合。

## <a name="time-to-refactor"></a>重構的時間

紅色/綠色/重構中的第三個步驟是重構元件。 此時，我們需要從程式碼回頭執行，並考慮如何重構我們的應用程式來改善其設計。 [重構] 階段是我們認為難以實現軟體設計原則和模式的最佳方式。

我們可以自由修改程式碼，讓我們選擇改善程式碼的設計。 我們有單元測試的安全網路，可防止我們中斷現有的功能。

現在，我們的群組控制器從良好的軟體設計觀點來看，是一件令人搞不好的。 群組控制器包含紊亂的驗證和資料存取程式碼。 為了避免違反單一責任原則，我們需要將這些考慮區分為不同的類別。

[清單 9] 中包含我們重構的群組控制器類別。 控制器已修改為使用 ContactManager 服務層。 這是與連絡人控制器搭配使用的相同服務層。

[清單 10] 包含新增至 ContactManager 服務層的方法，以支援驗證、列出及建立群組。 IContactManagerService 介面已更新為包含新的方法。

[清單 11] 包含可執行 IContactManagerRepository 介面的新 FakeContactManagerRepository 類別。 不同于也會執行 IContactManagerRepository 介面的 EntityContactManagerRepository 類別，我們的新 FakeContactManagerRepository 類別不會與資料庫通訊。 FakeContactManagerRepository 類別會使用記憶體內部集合做為資料庫的 proxy。 我們會在單元測試中使用此類別做為假的儲存機制層。

**清單 9-Controllers\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample9.cs)]

**清單 10-Controllers\ContactManagerService.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample10.cs)]

**清單 11-Controllers\FakeContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample11.cs)]

修改 IContactManagerRepository 介面需要使用來執行 EntityContactManagerRepository 類別中的 CreateGroup （）和 ListGroups （）方法。 執行此動作的 laziest 和最快速方式是新增如下所示的 stub 方法：   

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample12.cs)]

最後，應用程式設計的這些變更需要我們對單元測試進行一些修改。 在執行單元測試時，我們現在需要使用 FakeContactManagerRepository。 更新後的 GroupControllerTest 類別包含在 [清單 12] 中。

**清單 12-Controllers\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample13.cs)]

完成所有這些變更之後，所有單元測試都會通過。 我們已完成紅色/綠色/重構的整個迴圈。 我們已實現前兩個使用者案例。 我們現在已針對使用者故事所表示的需求，支援單元測試。 執行其餘的使用者故事牽涉到重複相同的紅色/綠色/重構迴圈。

## <a name="modifying-our-database"></a>修改資料庫

可惜的是，即使我們已滿足單元測試所表示的所有需求，我們也不會完成工作。 我們仍然需要修改資料庫。

我們需要建立新的群組資料庫資料表。 請依照下列步驟：

1. 在 [伺服器總管] 視窗中，以滑鼠右鍵按一下 [資料表] 資料夾，然後選取 [**加入新的資料表**] 功能表選項。
2. 在資料表設計工具中，輸入下面所述的兩個數據行。
3. 將 [識別碼] 資料行標示為 [主鍵] 和 [標識] 資料行。
4. 按一下該軟碟的圖示，以 [名稱] 群組儲存新的資料表。

<a id="0.11_table01"></a>

| **資料行名稱** | **資料類型** | **允許 Null** |
| --- | --- | --- |
| ID | int | False |
| 名稱 | nvarchar(50) | False |

接下來，我們需要刪除 [Contacts] 資料表中的所有資料（否則，我們無法建立 [連絡人] 和 [群組] 資料表之間的關聯性）。 請依照下列步驟：

1. 以滑鼠右鍵按一下 [連絡人] 資料表，然後選取 [**顯示資料表資料**] 功能表選項。
2. 刪除所有資料列。

接下來，我們需要定義群組資料庫資料表與現有 [連絡人] 資料庫資料表之間的關聯性。 請依照下列步驟：

1. 按兩下 [伺服器總管] 視窗中的 [連絡人] 資料表以開啟資料表設計工具。
2. 將新的整數資料行加入至名為 GroupId 的連絡人資料表。
3. 按一下 [關聯性] 按鈕以開啟 [外鍵關聯性] 對話方塊（請參閱 [圖 3]）。
4. 按一下 [加入] 按鈕。
5. 按一下出現在 [資料表和資料行規格] 按鈕旁邊的省略號按鈕。
6. 在 [資料表和資料行] 對話方塊中，選取 [群組] 做為主鍵資料表和識別碼做為 [主鍵] 資料行。 選取 [連絡人] 做為外鍵資料表和 [GroupId] 做為外鍵資料行（請參閱 [圖 4]）。 按一下 [確定] 按鈕。
7. 在 [**插入和更新規格**] 底下，選取 [**刪除規則**的**Cascade** ] 值。
8. 按一下 [關閉] 按鈕，關閉 [外鍵關聯性] 對話方塊。
9. 按一下 [儲存] 按鈕，將變更儲存至 [連絡人] 資料表。

[建立資料庫資料表關聯性 ![](iteration-6-use-test-driven-development-cs/_static/image3.jpg)](iteration-6-use-test-driven-development-cs/_static/image5.png)

**圖 03**：建立資料庫資料表關聯性（[按一下以查看完整大小的影像](iteration-6-use-test-driven-development-cs/_static/image6.png)）

[指定資料表關聯性 ![](iteration-6-use-test-driven-development-cs/_static/image4.jpg)](iteration-6-use-test-driven-development-cs/_static/image7.png)

**圖 04**：指定資料表關聯性（[按一下以查看完整大小的影像](iteration-6-use-test-driven-development-cs/_static/image8.png)）

### <a name="updating-our-data-model"></a>正在更新我們的資料模型

接下來，我們需要更新我們的資料模型，以代表新的資料庫資料表。 請依照下列步驟：

1. 按兩下 [模型] 資料夾中的 [ContactManagerModel] 檔案，開啟 [Entity Designer]。
2. 以滑鼠右鍵按一下設計工具介面，然後選取 [**從資料庫更新模型**] 功能表選項。
3. 在 [更新嚮導] 中，選取 [群組] 資料表，然後按一下 [完成] 按鈕（請參閱 [圖 5]）。
4. 以滑鼠右鍵按一下 [群組] 實體，然後選取 [**重新命名**] 功能表選項。 將 [*群組*] 實體的名稱變更為 [*群組*（單數）]。
5. 以滑鼠右鍵按一下 [Contact] 實體底部的 [群組] 導覽屬性。 將 [*群組*] 導覽屬性的名稱變更為 [*群組*（單數）]。

[![從資料庫更新 Entity Framework 模型](iteration-6-use-test-driven-development-cs/_static/image5.jpg)](iteration-6-use-test-driven-development-cs/_static/image9.png)

**圖 05**：從資料庫更新 Entity Framework 模型（[按一下以查看完整大小的影像](iteration-6-use-test-driven-development-cs/_static/image10.png)）

完成這些步驟之後，您的資料模型會同時代表 [連絡人] 和 [群組] 資料表。 Entity Designer 應該會顯示這兩個實體（請參閱 [圖 6]）。

[顯示群組和連絡人 ![Entity Designer](iteration-6-use-test-driven-development-cs/_static/image6.jpg)](iteration-6-use-test-driven-development-cs/_static/image11.png)

**圖 06**：顯示群組和連絡人的 Entity Designer （[按一下以觀看完整大小的影像](iteration-6-use-test-driven-development-cs/_static/image12.png)）

### <a name="creating-our-repository-classes"></a>建立我們的存放庫類別

接下來，我們需要執行我們的存放庫類別。 在此反復專案的過程中，我們在撰寫程式碼以滿足我們的單元測試時，將數個新方法新增至 IContactManagerRepository 介面。 IContactManagerRepository 介面的最終版本包含在 [清單 14] 中。

**清單 14-Models\IContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample14.cs)]

我們實際上尚未實行任何與使用連絡人群組相關的方法。 目前，EntityContactManagerRepository 類別具有 IContactManagerRepository 介面中列出的每個連絡人群組方法的 stub 方法。 例如，ListGroups （）方法目前看起來像這樣：

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample15.cs)]

Stub 方法可讓我們編譯應用程式並通過單元測試。 不過，現在是時候實際執行這些方法。 EntityContactManagerRepository 類別的最終版本包含在 [清單 13] 中。

**清單 13-Models\EntityContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample16.cs)]

### <a name="creating-the-views"></a>建立視圖

當您使用預設的 ASP.NET view engine 時，請 ASP.NET MVC 應用程式。 因此，您不會建立 views 來回應特定的單元測試。 不過，因為應用程式不會有任何視圖，所以無法完成此反復專案，而不需要建立及修改 Contact Manager 應用程式中所包含的視圖。

我們需要建立下列新的視圖來管理連絡人群組（請參閱 [圖 7]）：

- Views\Group\Index.aspx-顯示連絡人群組的清單
- Views\Group\Delete.aspx-顯示刪除連絡人群組的確認表單

[![[群組索引] 視圖](iteration-6-use-test-driven-development-cs/_static/image7.jpg)](iteration-6-use-test-driven-development-cs/_static/image13.png)

**圖 07**： [群組索引] 視圖（[按一下以查看完整大小的影像](iteration-6-use-test-driven-development-cs/_static/image14.png)）

我們需要修改下列現有的視圖，使其包含連絡人群組：

- Views\Home\Create.aspx
- Views\Home\Edit.aspx
- Views\Home\Index.aspx

藉由查看本教學課程隨附的 Visual Studio 應用程式，您可以看到修改過的觀點。 例如，[圖 8] 說明連絡人索引視圖。

[![連絡人索引視圖](iteration-6-use-test-driven-development-cs/_static/image8.jpg)](iteration-6-use-test-driven-development-cs/_static/image15.png)

**圖 08**：連絡人索引視圖（[按一下以查看完整大小的影像](iteration-6-use-test-driven-development-cs/_static/image16.png)）

## <a name="summary"></a>總結

在此反復專案中，我們會遵循測試導向的開發應用程式設計方法，將新功能新增至我們的 Contact Manager 應用程式。 我們從建立一組使用者故事開始。 我們已建立一組單元測試，其對應于使用者故事所表示的需求。 最後，我們撰寫的程式碼剛好足以滿足單元測試所表示的需求。

完成撰寫足夠的程式碼以滿足單元測試所表示的需求之後，我們更新了資料庫和 views。 我們已在資料庫中新增 [群組] 資料表，並更新 Entity Framework 資料模型。 我們也建立了一組視圖並加以修改。

在下一個反復專案中--最後一個反復專案--我們會重寫應用程式以利用 Ajax。 藉由利用 Ajax，我們將改善 Contact Manager 應用程式的回應性和效能。

> [!div class="step-by-step"]
> [上一頁](iteration-5-create-unit-tests-cs.md)
> [下一頁](iteration-7-add-ajax-functionality-cs.md)
