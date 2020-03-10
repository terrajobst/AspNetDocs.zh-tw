---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: 使用 AJAX 來執行對應案例 |Microsoft Docs
author: microsoft
description: 步驟11顯示如何將 AJAX 對應支援整合到我們的 NerdDinner 應用程式，讓正在建立、編輯或查看 dinners 的使用者查看 l 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: 7fc90f978b9f9eca511feca70a3c0d02ec69b940
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580112"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a>使用 AJAX 實作對應實例

由[Microsoft](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟11，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。
> 
> 步驟11顯示如何將 AJAX 對應支援整合到我們的 NerdDinner 應用程式，讓正在建立、編輯或查看 dinners 的使用者以圖形方式查看晚餐的位置。
> 
> 如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a>NerdDinner 步驟11：整合 AJAX 地圖

我們現在會藉由整合 AJAX 對應支援，讓我們的應用程式更具視覺效果。 這可讓正在建立、編輯或查看 dinners 的使用者以圖形方式查看晚餐的位置。

### <a name="creating-a-map-partial-view"></a>建立地圖部分視圖

我們會在應用程式內的數個地方使用對應功能。 為了讓我們的程式碼更好，我們會將一般對應功能封裝在單一部分範本中，以便在多個控制器動作和視圖之間重複使用。 我們會將此部分視圖命名為「對應 .ascx」，並在 \Views\Dinners 目錄中建立它。

我們可以用滑鼠右鍵按一下 [\Views\Dinners] 目錄，然後選擇 [新增-&gt;View] 功能表命令來建立對應 .ascx 部分。 我們會將 view 命名為 "node.js"，並將其視為部分視圖，並指出我們即將傳遞強型別「晚餐」模型類別：

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

當我們按一下 [新增] 按鈕時，將會建立部分範本。 接著，我們會將對應的 .ascx 檔案更新為具有下列內容：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

第一個 &lt;腳本&gt; 參考指向 Microsoft 虛擬地球6.2 對應程式庫。 第二個 &lt;腳本&gt; 參考指向對應 .js 檔案，我們很快就會建立該檔案，以封裝我們的一般 JAVAscript 對應邏輯。 &lt;div id = "theMap"&gt; 元素是虛擬地球將用來裝載對應的 HTML 容器。

接著，我們會有內嵌的 &lt;腳本&gt; 區塊，其中包含兩個此視圖特有的 JavaScript 函式。 第一個函式會使用 jQuery 來連接在頁面準備好要執行用戶端腳本時所執行的函式。 它會呼叫 LoadMap （） helper 函式，我們將在我們的對應 .js 腳本檔案中定義，以載入虛擬地球地圖控制項。 第二個函式是回呼事件處理常式，會將釘選到識別位置的對應。

請注意，我們如何在用戶端腳本區塊內使用伺服器端 &lt;% =%&gt; 區塊，以內嵌我們想要對應至 JavaScript 的晚餐的緯度和經度。 這是用來輸出可供用戶端腳本使用之動態值的實用技巧（不需要對伺服器進行個別的 AJAX 呼叫來抓取值，讓它更快速）。 當此視圖在伺服器上呈現時，&lt;% =%&gt; 區塊會執行，因此 HTML 的輸出最後會有內嵌的 JavaScript 值（例如： var 緯度 = 47.64312;）。

### <a name="creating-a-mapjs-utility-library"></a>建立對應 .js 公用程式程式庫

現在讓我們建立 Map .js 檔案，我們可以用它來封裝 map 的 JavaScript 功能（並執行上述的 LoadMap 和 LoadPin 方法）。 若要這麼做，請以滑鼠右鍵按一下專案內的 \Scripts 目錄，然後選擇 [加入&gt;新專案] 功能表命令，選取 [JScript] 專案，並將其命名為「對應 .js」。

以下是我們將新增至對應 .js 檔案的 JavaScript 程式碼，該檔案會與虛擬地球互動，以顯示地圖，並為我們的 dinners 新增位置圖釘：

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a>整合地圖與建立和編輯表單

我們現在會將地圖支援與現有的建立和編輯案例進行整合。 好消息是，這很簡單，而且不需要我們變更我們的任何控制器程式碼。 因為我們的建立和編輯檢視會共用通用的「DinnerForm」部分視圖來執行晚餐表單 UI，所以我們可以在一處新增地圖，並同時使用「建立」和「編輯」案例。

我們只需要開啟 \Views\Dinners\DinnerForm.ascx 部分視圖並加以更新，以包含新的地圖部分。 以下是新增對應之後，更新的 DinnerForm 會顯示的樣子（注意：下列程式碼片段會省略 HTML 表單元素以求簡潔）：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

上述的 DinnerForm 部分會將 "DinnerFormViewModel" 類型的物件當做其模型類型（因為它需要晚餐物件，以及用來填入國家/地區 dropdownlist 的 SelectList）。 我們的 Map 部分只需要「晚餐」類型的物件做為其模型類型，因此當我們轉譯 Map 部分時，我們只會將 DinnerFormViewModel 的晚餐子屬性傳遞給它：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

我們已新增至部分的 JavaScript 函式會使用 jQuery 將「模糊」事件附加至 [位址] HTML 文字方塊。 您可能聽過「焦點」事件，會在使用者按一下或索引標籤成為文字方塊時引發。 相反的是當使用者結束文字方塊時，所引發的「模糊」事件。 上述事件處理常式會在發生這種情況時，清除 [緯度] 和 [經度] 文字方塊的值，然後在地圖上繪製新的位址位置。 我們在 map .js 檔案內定義的回呼事件處理常式，會根據我們提供的位址，使用虛擬地球傳回的值，更新表單上的 [經度] 和 [緯度] 文字方塊。

現在當我們再次執行應用程式，並按一下 [主機晚餐] 索引標籤時，我們會看到與標準晚餐表單元素一起顯示的預設地圖：

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

當我們輸入位址，然後按 tab 鍵離開時，地圖會動態更新以顯示位置，而我們的事件處理常式將會在 [緯度/經度] 文字方塊中填入位置值：

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

如果我們儲存新晚餐，然後再次開啟以供編輯，我們會發現對應位置會在頁面載入時顯示：

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

每次變更 [位址] 欄位時，地圖和緯度/經度座標都會更新。

現在地圖會顯示晚餐位置，我們也可以將 [緯度] 和 [經度] 表單欄位從可見的文字方塊變更為隱藏的元素（因為地圖會在每次輸入位址時自動更新）。 為此，我們將使用 Html. TextBox （） HTML helper 來切換，以使用 Html. Hidden （） helper 方法：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

現在，我們的表單更方便使用者使用，並避免顯示未經處理的緯度/經度（但仍會將它們儲存在資料庫中的每個晚餐）：

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a>將地圖與詳細資料檢視整合

既然我們已將對應與我們的建立和編輯案例整合，讓我們也將它與我們的詳細資料案例整合。 我們只需要呼叫 &lt;% RenderPartial （"map"）;詳細資料檢視中的%&gt;。

以下是 [完整詳細資料] 視圖的原始程式碼（含對應整合）如下所示：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

現在，當使用者流覽至/Dinners/Details/[id] URL 時，他們會看到晚餐的詳細資料、地圖上晚餐的位置（完成時使用圖釘，當滑鼠停留在上方時，會顯示晚餐的標題和位址），並具有適用于其 RSVP 的 AJAX 連結：

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a>在我們的資料庫和存放庫中執行位置搜尋

為了完成 AJAX 的執行，讓我們將地圖加入應用程式的首頁，以讓使用者以圖形方式搜尋附近的 dinners。

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

我們一開始會先在資料庫和資料存放庫層內實行支援，以有效率地針對 Dinners 執行以位置為基礎的 radius 搜尋。 我們可以使用[sql 2008 的新地理空間功能](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx)來執行這項操作，或者我們也可以使用 sql 函式方法來 Gary Dryden 本文中討論的內容： [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx)和 Conery 網友有關在這裡使用與 LINQ to SQL： [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)

若要執行這項技術，我們將在 Visual Studio 內開啟「伺服器總管」，選取 NerdDinner 資料庫，然後以滑鼠右鍵按一下其底下的 [函數] 子節點，並選擇建立新的「純量值函式」：

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

接著，我們會貼上下列 DistanceBetween 函數：

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

接著，我們會在 SQL Server 中建立新的資料表值函式，我們將會呼叫 "NearestDinners"：

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

這個 "NearestDinners" 資料表函數會使用 DistanceBetween helper 函式，傳回我們提供的緯度和經度100英里內的所有 Dinners：

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

若要呼叫此函式，我們會先按兩下 \Models 目錄中的 NerdDinner 檔案，以開啟 LINQ to SQL 的設計工具：

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

接著，我們會將 NearestDinners 和 DistanceBetween 函式拖曳至 LINQ to SQL 設計工具上，這會將其新增為我們 LINQ to SQL NerdDinnerDataCoNtext 類別上的方法：

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

然後，我們可以在 DinnerRepository 類別上公開 "FindByLocation" 查詢方法，其使用 NearestDinner 函式來傳回在指定位置的100英里內即將發生的 Dinners：

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a>執行以 JSON 為基礎的 AJAX 搜尋動作方法

我們現在將會執行控制器動作方法，利用新的 FindByLocation （）存放庫方法，傳回可用來填入地圖的晚餐資料清單。 我們會將此動作方法傳回 JSON （JavaScript 物件標記法）格式的晚餐資料，讓您可以輕鬆地在用戶端上使用 JavaScript 來進行操作。

若要執行這項操作，我們將建立新的 "SearchController" 類別，方法是以滑鼠右鍵按一下 \Controllers 目錄，然後選擇 [新增-&gt;控制器] 功能表命令。 接著，我們會在新的 SearchController 類別內執行 "SearchByLocation" 動作方法，如下所示：

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

SearchController 的 SearchByLocation 動作方法會在內部呼叫 DinnerRepository 上的 FindByLocation 方法，以取得鄰近 dinners 的清單。 不過，它會改為傳回 JsonDinner 物件，而不是直接將晚餐物件傳回給用戶端。 JsonDinner 類別會公開晚餐屬性的子集（例如，基於安全性理由，它不會洩漏具有晚餐之 RSVP 的人員名稱）。 它也包含不存在晚餐上的 RSVPCount 屬性，而這是透過計算與特定晚餐相關聯的 RSVP 物件數目而動態計算的。

然後，我們會在控制器基類上使用 Json （） helper 方法，以使用以 JSON 為基礎的電傳格式來傳回 dinners 的順序。 JSON 是一種標準文字格式，可表示簡單的資料結構。 以下範例顯示兩個 JsonDinner 物件的 JSON 格式清單在從動作方法傳回時的樣子：

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a>使用 jQuery 呼叫以 JSON 為基礎的 AJAX 方法

我們現在已準備好更新 NerdDinner 應用程式的首頁，以使用 SearchController 的 SearchByLocation 動作方法。 為此，我們會開啟/Views/Home/Index.aspx view 範本並加以更新，使其具有文字方塊、搜尋按鈕、地圖，以及名為 dinnerList 的 &lt;div&gt; 元素：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

然後，我們可以將兩個 JavaScript 函式加入至頁面：

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

第一個 JavaScript 函式會在第一次載入頁面時載入對應。 第二個 JavaScript 函式會在 [搜尋] 按鈕上向上連線 JavaScript click 事件處理常式。 當按下按鈕時，它會呼叫 FindDinnersGivenLocation （） JavaScript 函式，我們會將其新增至我們的對應 .js 檔案：

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

這個 FindDinnersGivenLocation （）函數會呼叫 map。在虛擬地球控制項上尋找（），以將其置入輸入的位置。 當虛擬地球對應服務傳回時，對應。Find （）方法會叫用 callbackUpdateMapDinners 回呼方法，我們傳遞它做為最後的引數。

CallbackUpdateMapDinners （）方法是實際工作的完成位置。 它會使用 jQuery 的 $. post （）協助程式方法，對我們 SearchController 的 SearchByLocation （）動作方法執行 AJAX 呼叫，並將新置中地圖的緯度和經度傳遞給它。 它會定義一個內嵌函式，當 $ post （） helper 方法完成時將會呼叫，而從 SearchByLocation （）動作方法傳回的 JSON 格式的晚餐結果會使用稱為 "dinners" 的變數傳遞給它。 然後，它會對每個傳回的晚餐執行 foreach，並使用晚餐的緯度和經度和其他屬性，在地圖上加入新的 pin。 它也會將晚餐專案新增至地圖右邊的 dinners HTML 清單。 然後，它會將圖釘和 HTML 清單的暫留事件進行線路處理，以便在使用者停留在其上方時顯示晚餐的詳細資料：

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

現在當我們執行應用程式並造訪首頁時，我們會看到一個地圖。 當我們輸入城市的名稱時，地圖會顯示附近的近期 dinners：

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

將滑鼠停留在晚餐上會顯示其相關詳細資料。

按一下 [在反升的] 或 [HTML] 清單右邊的晚餐標題，將會導覽到晚餐，我們可以選擇 RSVP 來進行下列動作：

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a>後續步驟

我們現在已實現 NerdDinner 應用程式的所有應用程式功能。 現在我們來看一下如何啟用它的自動化單元測試。

> [!div class="step-by-step"]
> [上一頁](use-ajax-to-deliver-dynamic-updates.md)
> [下一頁](enable-automated-unit-testing.md)
