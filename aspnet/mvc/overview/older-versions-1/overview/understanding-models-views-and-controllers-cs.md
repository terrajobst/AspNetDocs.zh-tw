---
uid: mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
title: 瞭解模型、視圖和控制器（C#） |Microsoft Docs
author: StephenWalther
description: 對模型、視圖和控制器感到困惑嗎？ 在本教學課程中，Stephen Walther 會向您介紹 ASP.NET MVC 應用程式的不同部分。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 87313792-0a96-4caf-89fc-1457d54e5c1e
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
msc.type: authoredcontent
ms.openlocfilehash: 57dc82d02d38adc2514aa2c02c6f156ed0fb88a6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600587"
---
# <a name="understanding-models-views-and-controllers-c"></a>了解模型、檢視和控制器 (C#)

依[Stephen Walther](https://github.com/StephenWalther)

> 對模型、視圖和控制器感到困惑嗎？ 在本教學課程中，Stephen Walther 會向您介紹 ASP.NET MVC 應用程式的不同部分。

本教學課程提供 ASP.NET MVC 模型、視圖和控制器的高階總覽。 換句話說，它會說明 ASP.NET MVC 中的 M '、V ' 和 C '。

閱讀本教學課程之後，您應該瞭解 ASP.NET MVC 應用程式的不同部分如何搭配使用。 您也應該瞭解 ASP.NET MVC 應用程式的架構與 ASP.NET Web Forms 應用程式或 Active Server Pages 應用程式有何不同。

## <a name="the-sample-aspnet-mvc-application"></a>範例 ASP.NET MVC 應用程式

建立 ASP.NET MVC Web 應用程式的預設 Visual Studio 範本包含非常簡單的範例應用程式，可用於瞭解 ASP.NET MVC 應用程式的不同部分。 在本教學課程中，我們會利用這個簡單的應用程式。

您可以啟動 Visual Studio 2008，然後選取功能表選項 [檔案] 和 [新增專案] （請參閱 [圖 1]），以建立具有 MVC 範本的新 ASP.NET MVC 應用程式。 在 新增專案 對話方塊的 專案類型 （Visual Basic 或C#）底下，選取您慣用的程式設計語言，並選取 範本 底下的  **ASP.NET MVC Web 應用程式** 按一下 [確定] 按鈕。

[![新增專案 對話方塊](understanding-models-views-and-controllers-cs/_static/image1.jpg)](understanding-models-views-and-controllers-cs/_static/image1.png)

**圖 01**： [新增專案] 對話方塊（[按一下以查看完整大小的影像](understanding-models-views-and-controllers-cs/_static/image2.png)）

當您建立新的 ASP.NET MVC 應用程式時，會出現 [**建立單元測試專案**] 對話方塊（請參閱 [圖 2]）。 這個對話方塊可讓您在方案中建立個別的專案，以測試您的 ASP.NET MVC 應用程式。 選取 [**否，不要建立單元測試專案**] 選項，然後按一下 [**確定]** 按鈕。

[![建立單元測試 對話方塊](understanding-models-views-and-controllers-cs/_static/image2.jpg)](understanding-models-views-and-controllers-cs/_static/image3.png)

**圖 02**： [建立單元測試] 對話方塊（[按一下以查看完整大小的影像](understanding-models-views-and-controllers-cs/_static/image4.png)）

建立新的 ASP.NET MVC 應用程式之後。 您會在 [方案總管] 視窗中看到數個資料夾和檔案。 特別是，您會看到三個名為 [模型]、[Views] 和 [控制器] 的資料夾。 您可能會猜到資料夾名稱，這些資料夾包含用來執行模型、視圖和控制器的檔案。

如果您展開 [控制器] 資料夾，您應該會看到名為 AccountController.cs 的檔案，以及名為 HomeController.cs 的檔案。 如果您展開 [Views] 資料夾，您應該會看到名為 Account、Home 和 Shared 的三個子資料夾。 如果您展開主資料夾，您會看到名為 [關於 .aspx 和 default.aspx] 的兩個其他檔案（請參閱 [圖 3]）。 這些檔案會構成包含在預設 ASP.NET MVC 範本中的範例應用程式。

[![[方案總管] 視窗](understanding-models-views-and-controllers-cs/_static/image3.jpg)](understanding-models-views-and-controllers-cs/_static/image5.png)

**圖 03**： [方案總管] 視窗（[按一下以查看完整大小的影像](understanding-models-views-and-controllers-cs/_static/image6.png)）

若要執行範例應用程式，您可以選取 [ **Debug]、[開始調試**] 功能表選項。 或者，您可以按 F5 鍵。

當您第一次執行 ASP.NET 應用程式時，會出現 [圖 4] 中的對話方塊，建議您啟用 [偵測模式]。 按一下 [確定] 按鈕，應用程式將會執行。

[未啟用 ![的 [偵測] 對話方塊](understanding-models-views-and-controllers-cs/_static/image4.jpg)](understanding-models-views-and-controllers-cs/_static/image7.png)

**圖 04**：未啟用調試功能對話方塊（[按一下以查看完整大小的影像](understanding-models-views-and-controllers-cs/_static/image8.png)）

當您執行 ASP.NET MVC 應用程式時，Visual Studio 會在網頁瀏覽器中啟動應用程式。 範例應用程式只包含兩個頁面： [索引] 頁面和 [關於] 頁面。 當應用程式第一次啟動時，[索引] 頁面會隨即出現（請參閱 [圖 5]）。 您可以按一下應用程式右上方的功能表連結，流覽至 [關於] 頁面。

[![[索引] 頁面](understanding-models-views-and-controllers-cs/_static/image10.png)](understanding-models-views-and-controllers-cs/_static/image9.png)

**圖 05**： [索引] 頁面（[按一下以查看完整大小的影像](understanding-models-views-and-controllers-cs/_static/image11.png)）

請注意瀏覽器網址列中的 Url。 例如，當您按一下 [關於] 功能表連結時，瀏覽器網址列中的 URL 會變更為 **/Home/About**。

如果您關閉瀏覽器視窗並返回 Visual Studio，就無法找到路徑為 Home/About 的檔案。 檔案不存在。 這是怎麼可行的？

## <a name="a-url-does-not-equal-a-page"></a>URL 不等於頁面

當您建立傳統的 ASP.NET Web Forms 應用程式或 Active Server Pages 應用程式時，URL 與頁面之間會有一對一的對應關係。 如果您向伺服器要求名為 SomePage 的頁面，則在名為 SomePage 的磁片上有更好的頁面。 如果 SomePage 不存在，您會看到 [ **404-找不到頁面**] 錯誤。

相較之下，當您建立 ASP.NET MVC 應用程式時，您在瀏覽器的網址列中輸入的 URL 與您在應用程式中找到的檔案之間沒有任何對應。 在 ASP.NET MVC 應用程式中，URL 會對應至控制器動作，而不是磁片上的頁面。

在傳統的 ASP.NET 或 ASP 應用程式中，瀏覽器要求會對應至頁面。 相反地，在 ASP.NET MVC 應用程式中，瀏覽器要求會對應至控制器動作。 ASP.NET Web Forms 應用程式是以內容為中心。 相反地，ASP.NET MVC 應用程式是以應用程式邏輯為中心。

## <a name="understanding-aspnet-routing"></a>瞭解 ASP.NET 路由

瀏覽器要求會透過稱為*ASP.NET 路由*的 ASP.NET 架構功能，對應至控制器動作。 ASP.NET MVC 架構會使用 ASP.NET 路由，將連入要求*路由傳送*至控制器動作。

ASP.NET 路由會使用路由表來處理傳入的要求。 當您的 web 應用程式第一次啟動時，就會建立此路由表。 在 global.asax 檔案中設定路由表。 預設 MVC global.asax 檔案包含在 [清單 1] 中。

**清單 1-global.asax**

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample1.cs)]

當 ASP.NET 應用程式第一次啟動時，會呼叫應用程式\_Start （）方法。 在 [清單 1] 中，這個方法會呼叫 RegisterRoutes （）方法，而 RegisterRoutes （）方法會建立預設的路由表。

預設路由表包含一個路由。 此預設路由會將所有連入要求分成三個區段（一個 URL 區段是正斜線之間的任何專案）。 第一個區段會對應到一個控制器名稱，第二個區段會對應到動作名稱，而最後一個區段會對應至傳遞給名為 Id 之動作的參數。

例如，請考慮下列 URL：

/Product/Details/3

此 URL 會剖析成三個參數，如下所示：

控制器 = 產品

動作 = 詳細資料

識別碼 = 3

Global.asax 檔案中定義的預設路由包含所有三個參數的預設值。 預設的控制器為 Home，預設動作為 Index，而預設識別碼為空字串。 記住這些預設值之後，請考慮如何剖析下列 URL：

/Employee

此 URL 會剖析成三個參數，如下所示：

控制器 = 員工

action = 索引

識別碼 =

最後，如果您開啟 ASP.NET MVC 應用程式，但未提供任何 URL （例如 `http://localhost`），則會剖析 URL，如下所示：

控制器 = 首頁

action = 索引

識別碼 =

要求會路由傳送至 HomeController 類別上的 Index （）動作。

## <a name="understanding-controllers"></a>瞭解控制器

控制器負責控制使用者與 MVC 應用程式互動的方式。 控制器包含 ASP.NET MVC 應用程式的流程式控制制邏輯。 當使用者提出瀏覽器要求時，控制器會決定要將哪些回應傳回給使用者。

控制器只是一個類別（例如，Visual Basic 或C#類別）。 範例 ASP.NET MVC 應用程式包含一個位於 [控制器] 資料夾中名為 HomeController.cs 的控制器。 HomeController.cs 檔案的內容會在 [清單 2] 中重現。

**清單 2-HomeController.cs**

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample2.cs)]

請注意，HomeController 有兩個名為 Index （）和 About （）的方法。 這兩種方法對應到控制器所公開的兩個動作。 URL/Home/Index 會叫用 HomeController （）方法，而 URL/Home/About 會叫用 HomeController. About （）方法。

控制器中的任何公用方法都會公開為控制器動作。 您必須特別注意這一點。 這表示可以透過在瀏覽器中輸入正確的 URL，讓具有網際網路存取權的任何人叫用控制器中包含的任何公用方法。

## <a name="understanding-views"></a>了解檢視

HomeController 類別、Index （）和 About （）公開的兩個控制器動作都會傳回一個視圖。 View 包含 HTML 標籤和傳送至瀏覽器的內容。 當您使用 ASP.NET MVC 應用程式時，view 就相當於頁面。

您必須在正確的位置建立您的 views。 HomeController （）動作會傳回位於下列路徑的 view：

\Views\Home\Index.aspx

HomeController （）動作會傳回位於下列路徑的 view：

\Views\Home\About.aspx

一般來說，如果您想要傳回控制器動作的視圖，則需要在 Views 資料夾中建立一個與您的控制器名稱相同的子資料夾。 在子資料夾中，您必須使用與控制器動作相同的名稱來建立 .aspx 檔案。

[清單 3] 中的檔案包含 About .aspx view。

**清單 3-關於 .aspx**

[!code-aspx[Main](understanding-models-views-and-controllers-cs/samples/sample3.aspx)]

如果您忽略 [清單 3] 中的第一行，則此視圖的其餘部分會包含標準 HTML。 您可以在這裡輸入您想要的任何 HTML 來修改視圖的內容。

View 與 Active Server Pages 或 ASP.NET Web Forms 中的頁面非常類似。 一個視圖可以包含 HTML 內容和腳本。 您可以用您最愛的 .NET 程式設計語言（例如， C#或 Visual Basic .net）撰寫腳本。 您可以使用腳本來顯示動態內容，例如資料庫資料。

## <a name="understanding-models"></a>瞭解模型

我們已討論過控制器，而且我們已討論過 views。 我們需要討論的最後一個主題是模型。 什麼是 MVC 模型？

MVC 模型包含所有未包含在視圖或控制器中的應用程式邏輯。 此模型應該包含您的所有應用程式商務邏輯、驗證邏輯和資料庫存取邏輯。 例如，如果您使用 Microsoft Entity Framework 來存取您的資料庫，則您會在 [模型] 資料夾中建立您的 Entity Framework 類別（您的 .edmx 檔案）。

視圖應該只包含與產生使用者介面相關的邏輯。 控制器應該只包含傳回正確視圖或將使用者重新導向至另一個動作（流量控制）所需的最低邏輯。 所有其他專案都應該包含在模型中。

一般來說，您應該針對 fat 模型和訣竅控制器進行。 您的控制器方法應該只包含幾行程式碼。 如果控制器動作的功能過大，則您應該考慮將邏輯移出至 [模型] 資料夾中的新類別。

## <a name="summary"></a>總結

本教學課程提供您 ASP.NET MVC web 應用程式不同部分的高階總覽。 您已瞭解 ASP.NET 路由如何將傳入瀏覽器要求對應至特定控制器動作。 您已瞭解控制器如何協調如何將視圖傳回給瀏覽器。 最後，您已瞭解模型如何包含應用程式商務、驗證和資料庫存取邏輯。
