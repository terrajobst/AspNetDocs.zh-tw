---
uid: web-pages/overview/data/7-displaying-data-in-a-chart
title: 使用 ASP.NET Web Pages （Razor）在圖表中顯示資料 |Microsoft Docs
author: microsoft
description: 本章說明如何在圖表中顯示資料。 在上一章中，您已瞭解如何以手動方式在方格中顯示資料。 本章將說明 。
ms.author: riande
ms.date: 05/22/2012
ms.assetid: f889fd46-4dac-4ecb-83d8-60e64c22036e
msc.legacyurl: /web-pages/overview/data/7-displaying-data-in-a-chart
msc.type: authoredcontent
ms.openlocfilehash: 6dad67d4e3d38d57a761c567d937d714a3184ea9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627488"
---
# <a name="displaying-data-in-a-chart-with-aspnet-web-pages-razor"></a>使用 ASP.NET Web Pages （Razor）在圖表中顯示資料

由[Microsoft](https://github.com/microsoft)

> 本文說明如何使用圖表，在 ASP.NET Web Pages （Razor）網站中，使用 `Chart` helper 來顯示資料。
> 
> **您將瞭解的內容**：
> 
> - 如何在圖表中顯示資料。
> - 如何使用內建主題來為圖表樣式。
> - 如何儲存圖表以及如何加以快取，以提升效能。
> 
> 以下是文章中引進的 ASP.NET 程式設計功能：
> 
> - `Chart` helper。
> 
> > [!NOTE]
> > 本文中的資訊適用于 ASP.NET Web Pages 1.0 和 Web Pages 2。

<a id="The_Chart_Helper"></a>
## <a name="the-chart-helper"></a>圖表 Helper

當您想要以圖形形式顯示資料時，可以使用 `Chart` helper。 `Chart` helper 可以轉譯影像，以顯示各種圖表類型的資料。 它支援許多格式設定和標籤的選項。 `Chart` helper 可以轉譯超過30種圖表類型，包括您可能熟悉的 Microsoft Excel 或其他工具&#8212;區域圖、橫條圖、直條圖、折線圖和圓形圖，以及更多特製化圖表，例如股票圖。

| **區域圖**![描述：區域圖類型的圖片](7-displaying-data-in-a-chart/_static/image1.jpg) | **橫條圖**![描述：橫條圖類型的圖片](7-displaying-data-in-a-chart/_static/image2.jpg) |
| --- | --- |
| **直條圖**![描述：直條圖類型的圖片](7-displaying-data-in-a-chart/_static/image3.jpg) | **折線圖**![描述：折線圖類型的圖片](7-displaying-data-in-a-chart/_static/image4.jpg) |
| **圓形圖**![描述：圓形圖類型的圖片](7-displaying-data-in-a-chart/_static/image5.jpg) | **股票圖**![描述：股票圖類型的圖片](7-displaying-data-in-a-chart/_static/image6.jpg) |

### <a name="chart-elements"></a>圖表項目

圖表會顯示資料和其他元素，例如圖例、軸、數列等等。 下圖顯示當您使用 `Chart` helper 時，可以自訂的許多圖表元素。 本文說明如何設定這些元素的部分（而非全部）。

![描述：顯示圖表元素的圖片](7-displaying-data-in-a-chart/_static/image7.jpg)

<a id="Creating_a_Chart"></a>
## <a name="creating-a-chart-from-data"></a>從資料建立圖表

您在圖表中顯示的資料可以來自陣列、從資料庫傳回的結果，或 XML 檔案中的資料。

### <a name="using-an-array"></a>使用陣列

如[使用 Razor 語法進行 ASP.NET Web Pages 程式設計簡介](https://go.microsoft.com/fwlink/?LinkId=202890)中所述，陣列可讓您在單一變數中儲存類似專案的集合。 您可以使用陣列來包含您想要包含在圖表中的資料。

此程式說明如何使用預設圖表類型，從陣列中的資料建立圖表。 它也會顯示如何在頁面中顯示圖表。

1. 建立名為*ChartArrayBasic*的新檔案。
2. 以下列內容取代現有的內容： 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample1.cshtml)]

    程式碼會先建立新的圖表，並設定其寬度和高度。 您可以使用 `AddTitle` 方法來指定圖表標題。 若要加入資料，您可以使用 `AddSeries` 方法。 在此範例中，您會使用 `AddSeries` 方法的 `name`、`xValue`和 `yValues` 參數。 [`name`] 參數會顯示在圖表圖例中。 `xValue` 參數包含沿著圖表水準軸顯示的資料陣列。 `yValues` 參數包含用來繪製圖表垂直點的資料陣列。

    `Write` 方法實際上會呈現圖表。 在此情況下，因為您未指定圖表類型，所以 `Chart` helper 會轉譯其預設圖表，也就是直條圖。
3. 在瀏覽器中執行頁面。 瀏覽器會顯示圖表。 

    ![](7-displaying-data-in-a-chart/_static/image8.jpg)

### <a name="using-a-database-query-for-chart-data"></a>針對圖表資料使用資料庫查詢

如果您想要建立圖表的資訊是在資料庫中，您可以執行資料庫查詢，然後使用結果中的資料來建立圖表。 此程式說明如何從在[ASP.NET Web Pages 網站中使用資料庫簡介](https://go.microsoft.com/fwlink/?LinkId=202893)中所建立的資料庫中，讀取和顯示資料。

1. 如果資料夾不存在，請將*應用程式\_Data*資料夾新增至網站的根目錄。
2. 在*應用程式\_資料* 資料夾中，新增名為*SmallBakery*的資料庫檔案，其說明請參閱在[ASP.NET Web Pages 網站中使用資料庫簡介](https://go.microsoft.com/fwlink/?LinkId=202893)。
3. 建立名為*ChartDataQuery*的新檔案。
4. 以下列內容取代現有的內容：   

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample2.cshtml)]

    程式碼會先開啟 SmallBakery 資料庫，並將它指派給名為 `db`的變數。 這個變數代表可以用來讀取和寫入資料庫的 `Database` 物件。 接下來，程式碼會執行 SQL 查詢，以取得每個產品的名稱和價格。 此程式碼會建立新的圖表，並藉由呼叫圖表的 `DataBindTable` 方法，將資料庫查詢傳遞給它。 這個方法會採用兩個參數： `dataSource` 參數用於查詢中的資料，而 `xField` 參數可讓您設定要用於圖表 X 軸的資料行。

    除了使用 `DataBindTable` 方法以外，您還可以使用 `Chart` helper 的 `AddSeries` 方法。 `AddSeries` 方法可讓您設定 `xValue` 和 `yValues` 參數。 例如，而不是使用 `DataBindTable` 的方法，如下所示：

    [!code-css[Main](7-displaying-data-in-a-chart/samples/sample3.css)]

    您可以使用 `AddSeries` 方法，如下所示：

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample4.html)]

    兩者都會呈現相同的結果。 `AddSeries` 方法更具彈性，因為您可以更明確地指定圖表類型和資料，但如果您不需要額外的彈性，`DataBindTable` 方法會更容易使用。
5. 在瀏覽器中執行頁面。 

    ![](7-displaying-data-in-a-chart/_static/image9.jpg)

### <a name="using-xml-data"></a>使用 XML 資料

圖表的第三個選項是使用 XML 檔案做為圖表的資料。 這需要 XML 檔案也有描述 XML 結構的架構檔案（ *.xsd*檔案）。 此程式說明如何從 XML 檔案讀取資料。

1. 在*應用程式\_資料* 資料夾中，建立名為*Data .XML*的新 XML 檔案。
2. 將現有的 XML 取代為下列，這是關於虛構公司員工的一些 XML 資料。 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample5.xml)]
3. 在*應用程式\_資料* 資料夾中，建立名為*Data .XSD*的新 XML 檔案。 （請注意，這次的副檔名是 *.xsd*）。
4. 以下列內容取代現有的 XML： 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample6.xml)]
5. 在網站的根目錄中，建立名為*ChartDataXML*的新檔案。
6. 以下列內容取代現有的內容： 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample7.cshtml)]

    程式碼會先建立 `DataSet` 物件。 這個物件是用來管理從 XML 檔案讀取的資料，並根據架構檔案中的資訊加以組織。 （請注意，程式碼的頂端會包含 `using SystemData`的語句。 若要能夠使用 `DataSet` 物件，這是必要的。 如需詳細資訊，請參閱本文稍後的[使用&quot; 語句和完整限定名稱的&quot;](#SB_UsingStatements) 。）

    接下來，程式碼會根據資料集建立 `DataView` 物件。 資料檢視會提供圖表可以系結&#8212;的物件，也就是 [讀取] 和 [繪製]。 圖表會使用 `AddSeries` 方法系結至資料，如您稍早在建立陣列資料的圖表時所見，但這次 `xValue` 和 `yValues` 參數會設定為 `DataView` 物件。

    這個範例也會示範如何指定特定的圖表類型。 在 `AddSeries` 方法中加入資料時，`chartType` 參數也會設定為顯示圓形圖。
7. 在瀏覽器中執行頁面。 

    ![](7-displaying-data-in-a-chart/_static/image10.jpg)

> [!TIP]
> 
> <a id="SB_UsingStatements"></a>
> ### <a name="using-statements-and-fully-qualified-names"></a>"Using" 語句和完整限定名稱
> 
> 使用 Razor 語法 ASP.NET Web Pages 的 .NET Framework 是由數千個元件（類別）所組成。 為了讓它能夠管理所有的類別，它們會組織成*命名空間*，而這些都有點類似程式庫。 例如，`System.Web` 命名空間包含支援瀏覽器/伺服器通訊的類別，`System.Xml` 命名空間包含用來建立和讀取 XML 檔案的類別，而 `System.Data` 命名空間包含可讓您處理資料的類別。
> 
> 為了在 .NET Framework 中存取任何指定的類別，程式碼必須不只知道類別名稱，也不能知道類別所在的命名空間。 例如，若要使用 `Chart` helper，程式碼必須尋找 `System.Web.Helpers.Chart` 類別，其結合了命名空間（`System.Web.Helpers`）與類別名稱（`Chart`）。 這稱為類別的完整名稱&#8212; ，在 .NET Framework 的 vastness 中，其完整且*明確的位置*。 在程式碼中，這看起來會像下面這樣：
> 
> `var myChart = new System.Web.Helpers.Chart(width: 600, height: 400) // etc.`
> 
> 不過，每次您想要參考類別或協助程式時，都必須使用這些長的完整名稱，這很麻煩（而且容易出錯）。 因此，為了讓您更輕鬆地使用類別名稱，您可以匯*入*您感興趣的命名空間，這通常只是 .NET Framework 的多個命名空間中的少數幾個。 如果您已匯入命名空間，則只能使用類別名稱（`Chart`），而不是完整名稱（`System.Web.Helpers.Chart`）。 當您的程式碼執行並遇到類別名稱時，它只會查看您已匯入以尋找該類別的命名空間。
> 
> 當您使用 ASP.NET Web Pages 搭配 Razor 語法來建立網頁時，通常會每次都使用相同的一組類別，包括 `WebPage` 類別、各種協助程式等等。 若要在每次建立網站時儲存匯入相關命名空間的工作，請設定 ASP.NET，讓它自動匯入每個網站的一組核心命名空間。 這就是為什麼您不需要處理命名空間或匯入到目前為止;您所使用的所有類別都是在已為您匯入的命名空間中。
> 
> 不過，有時候您必須使用不在自動匯入的命名空間中的類別。 在這種情況下，您可以使用該類別的完整名稱，也可以手動匯入包含類別的命名空間。 若要匯入命名空間，您可以使用 `using` 語句（Visual Basic 中的`import`），如您在先前的範例中所見。
> 
> 例如，`DataSet` 類別是在 `System.Data` 命名空間中。 `System.Data` 的命名空間不會自動用於 ASP.NET Razor 頁面。 因此，若要使用其完整名稱來處理 `DataSet` 類別，您可以使用如下的程式碼：
> 
> `var dataSet = new System.Data.DataSet();`
> 
> 如果您必須重複使用 `DataSet` 類別，您可以像這樣匯入命名空間，然後在程式碼中只使用類別名稱：
> 
> [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample8.cshtml)]
> 
> 您可以為任何其他您想要參考的 .NET Framework 命名空間加入 `using` 語句。 不過，如上所述，您不需要經常這麼做，因為您所使用的大部分類別都是在 ASP.NET 自動匯入的命名空間中，以用於 *. cshtml*和*vbhtml*頁面。

<a id="Displaying_Charts"></a>
## <a name="displaying-charts-inside-a-web-page"></a>在網頁內顯示圖表

在您到目前為止所看到的範例中，您會建立圖表，然後圖表會以圖形的形式直接轉譯至瀏覽器。 不過，在許多情況下，您會想要將圖表顯示為頁面的一部分，而不只是在瀏覽器中。 若要這麼做，需要兩個步驟的處理常式。 第一個步驟是建立可產生圖表的頁面，如同您已見過的。

第二個步驟是在另一個頁面中顯示產生的影像。 若要顯示影像，請使用 HTML `<img>` 專案，就像顯示任何影像一樣。 不過，`<img>` 專案會參考包含建立圖表之 `Chart` 協助程式的*cshtml*檔案，而不是參考 *.jpg*或 *.png*檔案。 當顯示頁面執行時，`<img>` 元素會取得 `Chart` helper 的輸出，並呈現圖表。

![](7-displaying-data-in-a-chart/_static/image11.jpg)

1. 建立名為*ShowChart*的檔案。
2. 以下列內容取代現有的內容： 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample9.html)]

    程式碼會使用 `<img>` 元素來顯示您稍早在*ChartArrayBasic*中建立的圖表。
3. 在瀏覽器中執行網頁。 *ShowChart*檔會根據*ChartArrayBasic*中包含的程式碼顯示圖表影像。

<a id="Styling_a_Chart"></a>
## <a name="styling-a-chart"></a>設定圖表的樣式

`Chart` helper 支援大量選項，可讓您自訂圖表的外觀。 您可以設定色彩、字型、框線等等。 自訂圖表外觀的簡單方法是使用*主題*。 佈景主題是指定如何使用字型、色彩、標籤、調色盤、框線和效果來呈現圖表的資訊集合。 （請注意，圖表的樣式並不表示圖表的類型）。

下表列出內建主題。

| 佈景主題 | 說明 |
| --- | --- |
| `Vanilla` | 在白色背景上顯示紅色資料行。 |
| `Blue` | 在藍色漸層背景上顯示藍色資料行。 |
| `Green` | 在綠色漸層背景上顯示藍色資料行。 |
| `Yellow` | 在黃色漸層背景上顯示橙色資料行。 |
| `Vanilla3D` | 在白色背景上顯示立體紅色資料行。 |

您可以指定要在建立新圖表時使用的主題。

1. 建立名為*ChartStyleGreen*的新檔案。
2. 將頁面中的現有內容取代為下列內容：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample10.cshtml)]

    這段程式碼與先前使用資料庫來進行資料的範例相同，但會在建立 `Chart` 物件時加入 `theme` 參數。 以下顯示已變更的程式碼：

    [!code-csharp[Main](7-displaying-data-in-a-chart/samples/sample11.cs)]
3. 在瀏覽器中執行頁面。 您會看到與之前相同的資料，但圖表看起來更美觀： 

    ![](7-displaying-data-in-a-chart/_static/image12.jpg)

<a id="Saving_a_Chart"></a>
## <a name="saving-a-chart"></a>儲存圖表

當您使用這篇文章中所見到的 `Chart` helper 時，協助專家會在每次叫用時從頭重新建立圖表。 如有必要，圖表的程式碼也會重新查詢資料庫，或重新讀取 XML 檔案以取得資料。 在某些情況下，執行這項作業可能是一項複雜的作業，例如，如果您查詢的資料庫很大，或 XML 檔案包含大量資料。 即使圖表不包含大量資料，以動態方式建立影像的程式還是會佔用伺服器資源，如果有許多人要求顯示圖表的頁面，可能會影響網站的效能。

為了協助您減少建立圖表的潛在效能影響，您可以在第一次需要時建立圖表，然後加以儲存。 再次需要圖表時，您可以直接提取已儲存的版本，然後再進行轉譯，而不是重新產生。

您可以使用下列方式來儲存圖表：

- 將圖表快取在電腦記憶體中（在伺服器上）。
- 將圖表儲存為影像檔案。
- 將圖表儲存為 XML 檔案。 此選項可讓您在儲存圖表之前先加以修改。

### <a name="caching-a-chart"></a>快取圖表

建立圖表之後，您就可以快取它。 快取圖表表示如果需要再次顯示，則不需要重新建立。 當您將圖表儲存在快取中時，您可以為它提供一個對該圖表而言必須是唯一的索引鍵。

如果伺服器的記憶體不足，可能會移除儲存至快取的圖表。 此外，如果您的應用程式因為任何原因而重新開機，則會清除快取。 因此，使用快取圖表的標準方式是一律先檢查它是否可在快取中使用，如果沒有，則建立或重新建立。

1. 在您網站的根目錄中，建立名為*ShowCachedChart*的檔案。
2. 以下列內容取代現有的內容： 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample12.html)]

    `<img>` 標記包含指向*ChartSaveToCache*的 `src` 屬性，並將金鑰當做查詢字串傳遞至頁面。 此索引鍵包含 &quot;myChartKey&quot;的值。 *ChartSaveToCache*檔案包含建立圖表的 `Chart` helper。 您稍後會建立此頁面。

    頁面結尾有一個名為*ClearCache*的頁面連結。 這也是您很快就會建立的頁面。 在此範例中，您只需要使用*ClearCache*來測試快取，這不是您在使用快取圖表時通常會包含的連結或頁面。
3. 在您網站的根目錄中，建立名為*ChartSaveToCache*的新檔案。
4. 以下列內容取代現有的內容：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample13.cshtml)]

    程式碼會先檢查是否已將任何內容當做索引鍵值傳遞至查詢字串中。 若是如此，程式碼就會呼叫 `GetFromCache` 方法並傳遞金鑰給它，以嘗試從快取讀取圖表。 如果快取中沒有該索引鍵下的任何內容（這會在第一次要求圖表時發生），則程式碼會如往常般建立圖表。 當圖表完成時，程式碼會藉由呼叫 `SaveToCache`，將它儲存至快取。 該方法需要金鑰（如此一來，您可以稍後再要求圖表）和圖表儲存在快取中的時間量。 （您快取圖表的確切時間取決於您認為它所代表的資料可能會變更的頻率）。如果這是設定為 true，`SaveToCache` &#8212;方法也需要 `slidingExpiration` 參數，則每次存取圖表時，就會重設 timeout 計數器。 在此情況下，其作用表示圖表的快取專案會在上一次有人存取圖表之後的2分鐘後到期。 （滑動到期的替代方案為絕對到期日，這表示快取專案在放入快取後的2分鐘內就會剛好過期，無論存取的頻率為何）。

    最後，程式碼會使用 `WriteFromCache` 方法，從快取中提取並轉譯圖表。 請注意，這個方法是在檢查快取的 `if` 區塊外，因為它會從快取中取得圖表，無論圖表是從何處開始，還是必須產生並儲存在快取中。

    請注意，在此範例中，`AddTitle` 方法包含時間戳記。 （它會將目前的日期和&#8212;時間&#8212; `DateTime.Now` 新增至標題）。
5. 建立名為*ClearCache*的新頁面，並將其內容取代為下列內容：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample14.cshtml)]

    此頁面會使用 `WebCache` helper 來移除*ChartSaveToCache*中快取的圖表。 如先前所述，您通常不需要像這樣的頁面。 您只需要在這裡建立，就能更輕鬆地測試快取。
6. 在瀏覽器中執行*ShowCachedChart。* 頁面會根據*ChartSaveToCache*中包含的程式碼顯示圖表影像。 記下 [圖表標題] 中的時間戳記。 

    ![描述：圖表標題中包含時間戳記之基本圖表的圖片](7-displaying-data-in-a-chart/_static/image13.jpg)
7. 關閉瀏覽器。
8. 再次執行*ShowCachedChart* 。 請注意，時間戳記與之前相同，這表示圖表並未重新產生，而是改為從快取讀取。
9. 在 [ *ShowCachedChart*] 中，按一下 [**清除**快取] 連結。 這會帶您前往*ClearCache*，這會報告快取已清除。
10. 按一下 [**返回 ShowCachedChart** ] 連結，或從 WebMatrix 重新執行*ShowCachedChart。* 請注意，這次時間戳記已變更，因為快取已清除。 因此，程式碼必須重新產生圖表，並將它放回快取中。

### <a name="saving-a-chart-as-an-image-file"></a>將圖表儲存為影像檔案

您也可以在伺服器上將圖表儲存為影像檔案（例如，做為 *.jpg*檔案）。 接著，您可以用您對任何影像的方式來使用影像檔案。 其優點是儲存檔案，而不是儲存至暫時快取。 您可以在不同的時間儲存新的圖表影像（例如，每小時），然後保留一段時間後所發生變更的永久記錄。 請注意，您必須確定您的 web 應用程式有許可權將檔案儲存至您要放置影像檔的伺服器上的資料夾。

1. 在您網站的根目錄中，建立名為 *\_ChartFiles*的資料夾（如果尚未存在的話）。
2. 在您網站的根目錄中，建立名為*ChartSave*的新檔案。
3. 以下列內容取代現有的內容：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample15.cshtml)]

    程式碼會先藉由呼叫 `File.Exists` 方法，檢查 *.jpg*檔案是否存在。 如果檔案不存在，則程式碼會從陣列建立新的 `Chart`。 此時，程式碼會呼叫 `Save` 方法並傳遞 `path` 參數，以指定要儲存圖表之位置的檔案路徑和檔案名。 在頁面主體中，`<img>` 元素會使用路徑指向要顯示的 *.jpg*檔案。
4. 執行*ChartSave。*
5. 返回 WebMatrix。 請注意，名為*chart01*的影像檔已經儲存在 *\_ChartFiles*資料夾中。

### <a name="saving-a-chart-as-an-xml-file"></a>將圖表儲存為 XML 檔案

最後，您可以將圖表儲存為伺服器上的 XML 檔案。 使用此方法來快取圖表或將圖表儲存至檔案的優點是，您可以在需要時修改 XML，然後才顯示圖表。 您的應用程式必須具有您要放置影像檔之伺服器上資料夾的讀取/寫入權限。

1. 在您網站的根目錄中，建立名為*ChartSaveXml*的新檔案。
2. 以下列內容取代現有的內容：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample16.cshtml)]

    此程式碼類似于您稍早在快取中儲存圖表所看到的程式碼，但它使用 XML 檔案。 程式碼會先藉由呼叫 `File.Exists` 方法，檢查 XML 檔案是否存在。 如果檔案存在，則程式碼會建立新的 `Chart` 物件，並將檔案名當做 `themePath` 參數傳遞。 這會根據 XML 檔案中的任何內容來建立圖表。 如果 XML 檔案尚未存在，則程式碼會建立類似一般的圖表，然後呼叫 `SaveXml` 加以儲存。 圖表是使用 `Write` 方法來呈現，如先前所見。

    如同顯示快取的頁面，此程式碼會在圖表標題中包含時間戳記。
3. 建立名為*ChartDisplayXMLChart*的新頁面，並在其中加入下列標記： 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample17.html)]
4. 執行 [ *ChartDisplayXMLChart* ] 頁面。 圖表隨即顯示。 記下圖表標題中的時間戳記。
5. 關閉瀏覽器。
6. 在 WebMatrix 中，以滑鼠右鍵按一下 [ *\_ChartFiles* ] 資料夾 **，按一下 [** 重新整理]，然後開啟資料夾。 此資料夾中的*XMLChart*是由 `Chart` helper 所建立。 

    ![描述：顯示圖表協助程式所建立之 XMLChart 的 [_ChartFiles] 資料夾。](7-displaying-data-in-a-chart/_static/image14.jpg)
7. 再次執行 [ *ChartDisplayXMLChart* ] 頁面。 圖表會顯示與您第一次執行頁面時相同的時間戳記。 這是因為圖表是從您稍早儲存的 XML 產生的。
8. 在 WebMatrix 中，開啟 [ *\_ChartFiles* ] 資料夾，並刪除*XMLChart*檔案。
9. 再次執行*ChartDisplayXMLChart*一頁。 此時，時間戳記會更新，因為 `Chart` helper 必須重新建立 XML 檔案。 如果您想要的話，請檢查 *\_ChartFiles*資料夾，並注意 XML 檔案已回傳。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他資源

- [在 ASP.NET Web Pages 網站中使用資料庫的簡介](https://go.microsoft.com/fwlink/?LinkId=202893)
- [在 ASP.NET Web Pages 的網站中使用快取來改善效能](https://go.microsoft.com/fwlink/?LinkId=202903)
- [圖表類別](https://msdn.microsoft.com/library/system.web.helpers.chart(v=vs.99))（MSDN 上的 ASP.NET Web Pages API 參考）
