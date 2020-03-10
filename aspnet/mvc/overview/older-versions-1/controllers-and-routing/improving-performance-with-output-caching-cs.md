---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
title: 使用輸出快取改善效能C#（） |Microsoft Docs
author: microsoft
description: 在本教學課程中，您將瞭解如何利用輸出快取來大幅提升 ASP.NET MVC web 應用程式的效能。 您 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 521c9117-81cd-4d8d-9d96-0256dc7bf50f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
msc.type: authoredcontent
ms.openlocfilehash: 548c5bea2e9cf26e0574e72d2c0ea204dbd90f9c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601266"
---
# <a name="improving-performance-with-output-caching-c"></a>使用輸出快取改善效能 (C#)

由[Microsoft](https://github.com/microsoft)

> 在本教學課程中，您將瞭解如何利用輸出快取來大幅提升 ASP.NET MVC web 應用程式的效能。 您將瞭解如何快取控制器動作傳回的結果，如此一來，每次新的使用者叫用動作時，都不需要建立相同的內容。

本教學課程的目的是要說明如何利用輸出快取來大幅提升 ASP.NET MVC 應用程式的效能。 輸出快取可讓您快取控制器動作所傳回的內容。 如此一來，每次叫用相同的控制器動作時，都不需要產生相同的內容。

例如，假設您的 ASP.NET MVC 應用程式會在名為 Index 的視圖中顯示資料庫記錄清單。 一般來說，每次使用者叫用傳回索引視圖的控制器動作時，都必須藉由執行資料庫查詢，從資料庫中抓取資料庫記錄集。

另一方面，如果您利用輸出快取，則每次使用者叫用相同的控制器動作時，都可以避免執行資料庫查詢。 您可以從快取中抓取此視圖，而不是從控制器動作重新產生。 快取可讓您避免在伺服器上執行多餘的工作。

## <a name="enabling-output-caching"></a>啟用輸出快取

您可以將 [OutputCache] 屬性新增至個別的控制器動作或整個控制器類別，藉以啟用輸出快取。 例如，[清單 1] 中的控制器會公開名為 Index （）的動作。 索引（）動作的輸出會快取10秒。

**清單1– Controllers\HomeController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample1.cs)]

在 ASP.NET MVC 的 Beta 版中，輸出快取不適用於[http://www.MySite.com/](http://www.mysite.com/)之類的 URL。 相反地，您必須輸入類似[http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index)的 URL。 

在 [清單 1] 中，索引（）動作的輸出會快取10秒。 如果您想要的話，也可以指定較長的快取持續時間。 例如，如果您想要快取一天的控制器動作輸出，您可以指定86400秒的快取持續時間（60秒 \* 60 分鐘 \* 24 小時）。

並不保證會針對您指定的時間長度快取內容。 當記憶體資源變低時，快取會開始自動收回內容。

[清單 1] 中的 Home 控制器會傳回 [清單 2] 中的索引視圖。 這個觀點沒有什麼特殊之處。 [索引] 視圖只會顯示目前的時間（請參閱 [圖 1]）。

**清單2– Views\Home\Index.aspx**

[!code-aspx[Main](improving-performance-with-output-caching-cs/samples/sample2.aspx)]

**圖1–快取的索引視圖**

![clip_image002](improving-performance-with-output-caching-cs/_static/image1.jpg)

如果您藉由在瀏覽器的網址列中輸入 URL/Home/Index 來多次叫用 Index （）動作，並重複地在瀏覽器中按下 [重新整理]/[重載] 按鈕，則索引視圖所顯示的時間不會變更10秒。 會顯示相同的時間，因為已快取此視圖。

請務必瞭解，所有造訪您應用程式的人都會快取相同的觀點。 叫用 Index （）動作的任何人都會取得相同的快取版本的索引視圖。 這表示，web 伺服器必須執行以服務索引視圖的工作量會大幅降低。

[清單 2] 中的觀點剛好是這麼簡單。 此視圖只會顯示目前的時間。 不過，您可以輕鬆快取顯示一組資料庫記錄的視圖。 在這種情況下，每次叫用傳回視圖的控制器動作時，都不需要從資料庫中抓取資料庫記錄集。 快取可以減少 web 伺服器和資料庫伺服器必須執行的工作量。

請勿在 MVC 視圖中使用頁面 &lt;% @ OutputCache%&gt; 指示詞。 這個指示詞會從 Web form 世界中不規則，不應用於 ASP.NET MVC 應用程式中。

## <a name="where-content-is-cached"></a>內容的快取位置

根據預設，當您使用 [OutputCache] 屬性時，會在三個位置快取內容：網頁伺服器、任何 proxy 伺服器，以及網頁瀏覽器。 您可以藉由修改 [OutputCache] 屬性的 Location 屬性，精確地控制內容的快取位置。

您可以將 Location 屬性設定為下列任何一個值：

> ·任何
> 
> ·台
> 
> ·數量
> 
> ·伺服器
> 
> ·無
> 
> ·ServerAndClient

根據預設，Location 屬性的值為 Any。 不過，在某些情況下，您可能只想要在瀏覽器上或只在伺服器上快取。 例如，如果您要快取每個使用者個人化的資訊，則不應該快取伺服器上的資訊。 如果您要向不同的使用者顯示不同的資訊，您應該只在用戶端上快取資訊。

例如，[清單 3] 中的控制器會公開名為 GetName （）的動作，以傳回目前的使用者名稱。 如果「插孔」登入網站並叫用 GetName （）動作，則動作會傳回「Hi 的插座」字串。 之後，如果 Jill 登入網站並叫用 GetName （）動作，她也會取得字串 "Hi"。 在一開始叫用控制器動作之後，所有使用者都會在 web 伺服器上快取字串。

**清單3– Controllers\BadUserController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample3.cs)]

最有可能的情況是，[清單 3] 中的控制器不會以您想要的方式運作。 您不想要對 Jill 顯示「Hi 插座」訊息。

您絕對不應該快取伺服器快取中的個人化內容。 不過，您可能會想要在瀏覽器快取中快取個人化的內容，以改善效能。 如果您在瀏覽器中快取內容，且使用者多次叫用相同的控制器動作，則可以從瀏覽器快取中抓取內容，而不是從伺服器抓取。

清單4中修改過的控制器會快取 GetName （）動作的輸出。 不過，只會在瀏覽器上快取內容，而不是在伺服器上快取。 如此一來，當多位使用者叫用 GetName （）方法時，每個人都會取得自己的使用者名稱，而不是另一個人的使用者名稱。

**清單4– Controllers\UserController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample4.cs)]

請注意，[清單 4] 中的 [OutputCache] 屬性包含將 Location 屬性設定為值 OutputCacheLocation. Client。 [OutputCache] 屬性也包含 NoStore 屬性。 NoStore 屬性是用來通知 proxy 伺服器和瀏覽器，他們不應該儲存快取內容的永久複本。

## <a name="varying-the-output-cache"></a>改變輸出快取

在某些情況下，您可能會想要有相同內容的不同快取版本。 例如，假設您要建立主要/詳細資料頁面。 主版頁面會顯示電影標題清單。 當您按一下標題時，會取得所選電影的詳細資料。

如果您快取 [詳細資料] 頁面，則無論您按一下哪一部電影，都會顯示相同電影的詳細資料。 第一個使用者選取的第一個電影會顯示給所有未來的使用者。

您可以利用 [OutputCache] 屬性的 VaryByParam 屬性來修正這個問題。 當表單參數或查詢字串參數不同時，這個屬性可讓您建立相同內容的不同快取版本。

例如，[清單 5] 中的控制器會公開名為 Master （）和 Details （）的兩個動作。 主要（）動作會傳回電影標題清單，而 Details （）動作會傳回所選電影的詳細資料。

**清單5– Controllers\MoviesController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample5.cs)]

Master （）動作包含 VaryByParam 屬性，其值為 "none"。 叫用 Master （）動作時，會傳回主視圖的相同快取版本。 系統會忽略任何表單參數或查詢字串參數（請參閱 [圖 2]）。

**圖2–/Movies/Master 視圖**

![clip_image004](improving-performance-with-output-caching-cs/_static/image2.jpg)

**圖3–/Movies/Details 視圖**

![clip_image006](improving-performance-with-output-caching-cs/_static/image3.jpg)

Details （）動作包含 VaryByParam 屬性，其值為 "Id"。 當 Id 參數的不同值傳遞至控制器動作時，會產生不同的快取版本的詳細資料檢視。

請務必瞭解，使用 VaryByParam 屬性會導致更快的快取，而不是較少。 會針對每個不同版本的 Id 參數建立詳細資料檢視的不同快取版本。

您可以將 VaryByParam 屬性設定為下列值：

> \* = 每當表單或查詢字串參數不同時，建立不同的快取版本。
> 
> 無 = 永不建立不同的快取版本
> 
> 參數的分號清單 = 每當清單中的任何表單或查詢字串參數改變時，建立不同的快取版本

## <a name="creating-a-cache-profile"></a>建立快取設定檔

除了藉由修改 [OutputCache] 屬性的屬性來設定輸出快取屬性以外，您也可以在 web 設定（web.config）檔案中建立快取設定檔。 在 web 設定檔中建立快取設定檔可提供幾個重要的優點。

首先，藉由在 web 設定檔中設定輸出快取，您可以控制控制器動作在單一中央位置快取內容的方式。 您可以建立一個快取設定檔，並將設定檔套用至數個控制器或控制器動作。

第二，您可以修改 web 設定檔案，而不需要重新編譯應用程式。 如果您需要停用已部署至生產環境之應用程式的快取，則可以直接修改 web 設定檔中定義的快取設定檔。 將會自動偵測並套用對 web 設定檔進行的任何變更。

例如，[清單 6] 中的 [&lt;快取&gt; web 設定] 區段會定義名為 Cache1Hour 的快取設定檔。 &lt;快取&gt; 區段必須出現在 web 設定檔的 &lt;system.web&gt; 區段中。

**[清單 6]-web.config 的快取區段**

[!code-xml[Main](improving-performance-with-output-caching-cs/samples/sample6.xml)]

[清單 7] 中的控制器會說明如何將 Cache1Hour 設定檔套用至具有 [OutputCache] 屬性的控制器動作。

**清單7– Controllers\ProfileController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample7.cs)]

如果您叫用 [清單 7] 中的控制器所公開的 [索引] （）動作，則會傳回1小時的相同時間。

## <a name="summary"></a>總結

輸出快取提供非常簡單的方法，可大幅提升 ASP.NET MVC 應用程式的效能。 在本教學課程中，您已瞭解如何使用 [OutputCache] 屬性來快取控制器動作的輸出。 您也學到如何修改 [OutputCache] 屬性的屬性（例如 Duration 和 VaryByParam 屬性），以修改快取內容的方式。 最後，您已瞭解如何在 web 設定檔中定義快取設定檔。

> [!div class="step-by-step"]
> [上一頁](understanding-action-filters-cs.md)
> [下一頁](adding-dynamic-content-to-a-cached-page-cs.md)
