---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
title: 檢查 ASP.NET MVC 如何 scaffold DropDownList Helper |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 8921d7f2-21f0-427a-8b27-2df7251174b0
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
msc.type: authoredcontent
ms.openlocfilehash: 275b20ad964b3e8ddc272a7448f0740ed0891eff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614902"
---
# <a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a>檢查 ASP.NET MVC 如何 Scaffold DropDownList 協助程式

依[Rick Anderson](https://twitter.com/RickAndMSFT)

在**方案總管**中，以滑鼠右鍵按一下 [*控制器*] 資料夾，然後選取 [**新增控制器**]。 將控制器命名為**StoreManagerController**。 設定 [**新增控制器**] 對話方塊的選項，如下圖所示。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

編輯 [ *StoreManager\Index.cshtml* ] 視圖，並移除 `AlbumArtUrl`。 移除 `AlbumArtUrl` 會使簡報更容易閱讀。 已完成的程式碼如下所示。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

開啟*Controllers\StoreManagerController.cs*檔案，並尋找 `Index` 方法。 新增 `OrderBy` 子句，讓專輯依價格排序。 完整的程式碼如下所示。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

依價格排序可讓您更輕鬆地測試資料庫的變更。 當您測試編輯和建立方法時，您可以使用低價，讓儲存的資料先出現。

開啟*StoreManager\Edit.cshtml*檔案。 在圖例標記之後加入下面這一行。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

下列程式碼顯示這項變更的內容：

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

需要 `AlbumId` 才能對專輯記錄進行變更。

按 CTRL+F5 執行應用程式。 選取 [系統**管理員**] 連結，然後選取 [**建立新**的] 連結以建立新的專輯。 確認已儲存專輯資訊。 編輯專輯並確認您所做的變更已保存。

### <a name="the-album-schema"></a>專輯架構

MVC 樣板機制所建立的 `StoreManager` 控制器，可以讓 CRUD （建立、讀取、更新、刪除）存取音樂存放區資料庫中的專輯。 專輯資訊的架構如下所示：

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

`Albums` 資料表不會儲存專輯內容類型和描述，它會儲存 `Genres` 資料表的外鍵。 `Genres` 資料表包含內容類型名稱和描述。 同樣地，`Albums` 資料表不會包含專輯演出者名稱，而是 `Artists` 資料表的外鍵。 `Artists` 資料表包含演出者的名稱。 如果您檢查 `Albums` 資料表中的資料，您可以看到每個資料列都包含 `Genres` 資料表的外鍵，以及 `Artists` 資料表的外鍵。 下圖顯示 `Albums` 資料表中的一些資料表資料。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a>HTML 選取標記

HTML `<select>` 專案（由 HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) helper 建立）用來顯示完整的值清單（例如內容清單）。 針對 [編輯表單]，當目前的值為已知時，選取清單可以顯示目前的值。 我們先前在將選取的值設定為**喜劇**時看到這種情況。 選取清單非常適合用來顯示類別或外鍵資料。 [類型] 外鍵的 [`<select>`] 專案會顯示可能的內容類型名稱清單，但當您儲存表單時，[內容類型] 屬性會更新為 [內容類型] 外鍵值，而不是顯示的類型名稱。 在下圖中，選取的內容類型是**Disco** ，而演出者是**Donna 夏季**。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a>檢查 ASP.NET MVC Scaffold 程式碼

開啟*Controllers\StoreManagerController.cs*檔案，並尋找 `HTTP GET Create` 方法。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

`Create` 方法會在 `ViewBag`中加入兩個[SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx)物件，一個包含內容類型資訊，另一個則包含演出者資訊。 上述使用的[SelectList](https://msdn.microsoft.com/library/dd505286.aspx)函式多載會採用三個引數：

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. *items*： [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) ，其中包含清單中的專案。 在上述範例中，`db.Genres`傳回的內容清單。
2. *dataValueField*： **IEnumerable**清單中包含金鑰值的屬性名稱。 在上述範例中，`GenreId` 和 `ArtistId`。
3. *dataTextField*： **IEnumerable**清單中包含要顯示之資訊的屬性名稱。 在 [演出者] 和 [內容類型] 資料表中，都會使用 [`name`] 欄位。

開啟*Views\StoreManager\Create.cshtml*檔案，並檢查 [內容類型] 欄位的 [`Html.DropDownList` helper 標記]。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

第一行顯示建立視圖會採用 `Album` 模型。 在上面顯示的 `Create` 方法中，未傳遞任何模型，因此此視圖會取得**null** `Album` 模型。 此時，我們會建立新的專輯，所以沒有任何 `Album` 資料。

上面顯示的[DropDownList](https://msdn.microsoft.com/library/dd492948.aspx)多載會採用欄位的名稱來系結至模型。 它也會使用此名稱來尋找包含[SelectList](https://msdn.microsoft.com/library/dd505286.aspx)物件的**ViewBag**物件。 使用此多載時，您必須將**ViewBag SelectList**物件命名為 `GenreId`。 第二個參數（`String.Empty`）是未選取任何專案時所要顯示的文字。 這正是我們在建立新專輯時所要做的。 如果您移除了第二個參數，並使用下列程式碼：

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

選取清單會預設為第一個元素，或在我們的範例中為 [岩石]。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

檢查 `HTTP POST Create` 方法。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

`Create` 方法的這個多載會採用由 ASP.NET MVC 模型系結系統從張貼的表單值所建立的 `album` 物件。 當您提交新的專輯時，如果模型狀態是有效的，而且沒有資料庫錯誤，則會將新的專輯新增至資料庫。 下圖顯示新專輯的建立。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

您可以使用[fiddler 工具](http://www.fiddler2.com/fiddler2/)來檢查 ASP.NET MVC 模型系結用來建立專輯物件的已張貼表單值。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png)

### <a name="refactoring-the-viewbag-selectlist-creation"></a>重構 ViewBag SelectList 建立

`Edit` 方法和 `HTTP POST Create` 方法都有相同的程式碼，可在**ViewBag**中設定**SelectList** 。 在[試](http://en.wikipedia.org/wiki/Don't_repeat_yourself)的精神中，我們會重構這段程式碼。 我們稍後會使用此重構的程式碼。

建立新的方法，將內容類型和演出者**SelectList**新增至**ViewBag**。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

以 `SetGenreArtistViewBag` 方法的呼叫，取代兩行設定每個 `Create` 中的 `ViewBag` 和 `Edit` 方法。 已完成的程式碼如下所示。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

建立新的專輯並編輯專輯，以確認變更可正常執行。

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a>將 SelectList 明確地傳遞至 DropDownList

ASP.NET MVC 樣板所建立的建立和編輯檢視會使用下列**DropDownList**多載：

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

[建立] 視圖的 `DropDownList` 標記如下所示。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

因為 `SelectList` 的 `ViewBag` 屬性會命名為 `GenreId`，所以**DropDownList** helper 會使用**ViewBag**中的 `GenreId`**SelectList** 。 在下列**DropDownList**多載中，會明確傳入 `SelectList`。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

開啟*Views\StoreManager\Edit.cshtml*檔案，並使用上述多載，將**DropDownList**呼叫變更為明確傳入**SelectList**。 針對 [內容類型] 類別執行此動作。 完成的程式碼如下所示：

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

執行應用程式並按一下 [系統**管理**] 連結，然後流覽至 [爵士樂] 專輯並選取 [**編輯**] 連結。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

並不會顯示 [爵士樂] 做為目前選取的內容類型，而是顯示 [岩石]。 當字串引數（要系結的屬性）和**SelectList**物件具有相同的名稱時，不會使用選取的值。 未提供任何選取的值時，瀏覽器會預設為**SelectList**中的第一個元素（在上述範例中為「**岩石**」）。 這是**DropDownList** helper 的已知限制。

開啟*Controllers\StoreManagerController.cs*檔案，並將**SelectList**物件名稱變更為 `Genres` 和 `Artists`。 完成的程式碼如下所示：

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

[名稱] 和 [演出者] 是較好的類別名稱，因為它們包含的不只是每個類別目錄的識別碼。 我們先前已付費的重構。 我們的變更會與 `SetGenreArtistViewBag` 方法隔離，而不是變更四種方法中的**ViewBag** 。

變更 [建立] 和 [編輯] 視圖中的**DropDownList**呼叫，以使用新的**SelectList**名稱。 編輯檢視的新標記如下所示：

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

建立視圖需要空字串，以防止顯示 SelectList 中的第一個專案。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

建立新的專輯並編輯專輯，以確認變更可正常執行。 選取具有 [岩石] 以外類型的專輯來測試編輯程式碼。

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a>搭配 DropDownList Helper 使用視圖模型

在 Viewmodel 資料夾中建立名為 `AlbumSelectListViewModel`的新類別。 將 `AlbumSelectListViewModel` 類別中的程式碼取代為下列內容：

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

`AlbumSelectListViewModel` 的函式會採用專輯、演出者和內容的清單，並建立包含專輯的物件和內容組和演出者的 `SelectList`。

建立專案，以便在下一個步驟中建立視圖時，可以使用 `AlbumSelectListViewModel`。

將 `EditVM` 方法加入至 `StoreManagerController`。 已完成的程式碼如下所示。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

以滑鼠右鍵按一下 `AlbumSelectListViewModel`，選取 [**解析**]，然後**使用 MvcMusicStore. viewmodel;** 。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

或者，您可以新增下列 using 語句：

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

以滑鼠右鍵按一下 `EditVM`，然後選取 [**新增視圖**]。 使用如下所示的選項。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

選取 [**新增**]，然後以下列內容取代*Views\StoreManager\EditVM.cshtml*檔案的內容：

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

`EditVM` 標記與原始的 `Edit` 標記非常類似，但有下列例外狀況。

- [`Edit`] 視圖中的模型屬性的格式為 `model.property`（例如，`model.Title`）。 [`EditVm`] 視圖中的模型屬性的格式為 `model.Album.property`（例如，`model.Album.Title`）。 這是因為 `EditVM` 視圖會傳遞 `Album`的容器，而不是 `Edit` 視圖中的 `Album`。
- **DropDownList**第二個參數來自視圖模型，而不是**ViewBag**。
- `EditVM` view 中的**html.beginform** helper 會明確地回傳至 `Edit` 動作方法。 藉由回傳至 `Edit` 動作，我們不需要撰寫 `HTTP POST EditVM` 動作，而且可以重複使用 `HTTP POST` `Edit` 動作。

執行應用程式並編輯專輯。 將 URL 變更為使用 `EditVM`。 變更欄位並按 [**儲存**] 按鈕，以確認程式碼是否正常運作。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a>您應該使用哪一種方法？

所有顯示的三種方法都是可接受的。 許多開發人員偏好使用 `ViewBag`，將 `SelectList` 明確地傳遞給 `DropDownList`。 這種方法有額外的優點，讓您能夠彈性地使用更適當的集合名稱。 要注意的是，您無法將 `ViewBag SelectList` 物件命名為與模型屬性相同的名稱。

有些開發人員偏好使用 ViewModel 方法。 有些人會考慮更詳細的標記，並產生 ViewModel 方法的 HTML 的缺點。

在本節中，我們已瞭解使用**DropDownList**與類別目錄資料的三種方法。 在下一節中，我們將示範如何加入新的類別。

> [!div class="step-by-step"]
> [上一頁](using-the-dropdownlist-helper-with-aspnet-mvc.md)
> [下一頁](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)
