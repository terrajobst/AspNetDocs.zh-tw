---
uid: web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
title: 在 ASP.NET Web Pages （Razor）網站中顯示地圖 |Microsoft Docs
author: Rick-Anderson
description: 本文說明如何根據 Bing、Google、Ma 所提供的對應服務，在 ASP.NET Web Pages （Razor）網站中的頁面上顯示互動式地圖。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: b5c268dd-ca6a-4562-b94c-a220fcf01f58
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 36f3b753cf312504892872ff54bef49854588990
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638674"
---
# <a name="displaying-maps-in-an-aspnet-web-pages-razor-site"></a>在 ASP.NET Web Pages （Razor）網站中顯示地圖

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明如何根據 Bing、Google、MapQuest 和 Yahoo 提供的對應服務，在 ASP.NET Web Pages （Razor）網站中的頁面上顯示互動式地圖。
> 
> 您將學到什麼：
> 
> - 如何根據地址產生對應。
> - 如何根據緯度和經度座標產生地圖。
> - 如何註冊 Bing Maps 開發人員帳戶，並取得金鑰以與 Bing 地圖服務搭配使用。
> 
> 這是本文中引進的 ASP.NET 功能：
> 
> - `Maps` helper。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）2
> - WebMatrix 2
>   
> 
> 本教學課程也適用于 WebMatrix 3。

在網頁中，您可以使用 `Maps` helper，在頁面上顯示地圖。 您可以根據地址或一組經度和緯度座標來產生對應。 `Maps` 類別可讓您呼叫熱門的地圖引擎，包括 Bing、Google、MapQuest 和 Yahoo。

無論您呼叫哪一個對應引擎，將對應加入至頁面的步驟都相同。 您只需要新增 JavaScript 檔案參考，讓可用的方法顯示對應，然後再呼叫 `Maps` helper 的方法。

您可以根據您使用的 `Maps` helper 方法選擇對應服務。 您可以使用下列其中一種：

- `Maps.GetBingHtml`
- `Maps.GetGoogleHtml`
- `Maps.GetYahooHtml`
- `Maps.GetMapQuestHtml`

## <a name="installing-the-pieces-you-need"></a>安裝您需要的部分

若要顯示地圖，您需要下列各項：

- `Maps` helper。 此 helper 位於 ASP.NET Web helper 程式庫的第2版。 如果您尚未新增程式庫，您可以將它安裝在您的網站中做為 NuGet 套件。 如需詳細資訊，請參閱[在 ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)。 （在資源庫中，搜尋 `microsoft-web-helpers` 套件）。
- JQuery 程式庫。 其中幾個 WebMatrix 網站範本在其*腳本*資料夾中已經包含 jQuery 程式庫。 如果您沒有這些程式庫，您可以直接從[jQuery.org](http://jQuery.org)網站下載最新的 jQuery 程式庫。 或者，您可以使用範本建立新的網站（例如，**入門網站**範本），然後將 jQuery 檔案從該網站複製到目前的網站。

最後，如果您想要使用 Bing 地圖服務，則必須先建立（免費）帳戶，並取得金鑰。 若要取得金鑰，請遵循下列步驟：

1. 在[Bing Maps 開發人員帳戶](https://www.microsoft.com/maps/developers/web.aspx)上建立帳戶。 您也必須擁有 Microsoft 帳戶（Windows Live ID）。

    您可以指定要使用金鑰進行**評估/測試**。 如果您要使用 WebMatrix 和 IIS Express 在自己的電腦上測試對應功能，請移至 [**網站**] 工作區，並記下網站的 URL （例如，`http://localhost:50408`，雖然您的埠號碼可能會不同）。 當您註冊時，您可以使用此*localhost*位址作為網站。
2. 在您註冊帳戶之後，請前往 Bing Maps 帳戶中心，然後按一下 [**建立或查看金鑰**]：

    ![對應-2](displaying-maps-in-an-aspnet-web-pages-site/_static/image1.png)
3. 記錄 Bing 所建立的金鑰。

## <a name="creating-a-map-based-on-an-address-using-google"></a>根據地址建立對應（使用 Google）

下列範例示範如何建立頁面，以根據地址來呈現地圖。 此範例示範如何使用 Google Maps。

1. 在網站的根目錄中建立名為*MapAddress*的檔案。 此頁面會根據您傳遞給它的位址來產生對應。
2. 將下列程式碼複製到檔案中，並覆寫現有的內容。

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    請注意頁面的下列功能：

    - `<head>` 元素中的 `<script>` 元素。 在範例中，`<script>` 元素會參考*jquery-1.7.2.min.js 1.6.4*檔案，這是 jquery 程式庫（版本1.6.4）的縮減（壓縮）版本。 請注意，此參考會假設 *.js*檔案位於您網站的 [*腳本*] 資料夾中。 

        > [!NOTE]
        > 如果您使用的是不同版本的 jQuery 程式庫，請確定您正確地指向該版本。
    - 呼叫頁面主體中的 `@Maps.GetGoogleHtml`。 若要對應位址，您必須傳遞位址字串。 其他對應引擎的方法會以類似的方式（`@Maps.GetYahooHtml`、`@Maps.GetMapQuestHtml`）來工作。
3. 執行頁面並輸入位址。 此頁面會顯示以 Google Maps 為基礎的地圖，其中會顯示您指定的位置。

     ![對應-1](displaying-maps-in-an-aspnet-web-pages-site/_static/image2.png)

## <a name="creating-a-map-based-on-latitude-and-longitude-coordinates-using-bing"></a>根據緯度和經度座標建立地圖（使用 Bing）

這個範例示範如何根據座標建立地圖。 此範例示範如何使用 Bing 地圖服務，以及如何包含 Bing 金鑰。 （您也可以使用其他地圖引擎來建立以座標為基礎的對應，而不使用 Bing 金鑰）。

1. 在網站的根目錄中建立名為*MapCoordinates*的檔案，並以下列程式碼和標記取代現有的內容：

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample2.cshtml)]
2. 將 `your-key-here` 取代為您稍早產生的 Bing 地圖服務金鑰。
3. 執行 [ *MapCoordinates* ] 頁面，輸入緯度和經度座標，然後按一下**地圖！** 按鈕。 （如果您不知道任何座標，請嘗試下列動作。 這是 Microsoft Redmond 校園的位置）。

   - 緯度：47.6781005859375
   - 經度：-122.158317565918

     頁面會使用您所指定的座標來顯示。

     ![對應-3](displaying-maps-in-an-aspnet-web-pages-site/_static/image3.png)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他資源

[Microsoft Maps API 參考](https://msdn.microsoft.com/library/gg427611.aspx)
