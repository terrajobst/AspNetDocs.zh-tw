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
# <a name="displaying-maps-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="b7db4-103">在 ASP.NET Web Pages （Razor）網站中顯示地圖</span><span class="sxs-lookup"><span data-stu-id="b7db4-103">Displaying Maps in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="b7db4-104">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="b7db4-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="b7db4-105">本文說明如何根據 Bing、Google、MapQuest 和 Yahoo 提供的對應服務，在 ASP.NET Web Pages （Razor）網站中的頁面上顯示互動式地圖。</span><span class="sxs-lookup"><span data-stu-id="b7db4-105">This article explains how to display interactive maps on pages in an ASP.NET Web Pages (Razor) website based on mapping services provided by Bing, Google, MapQuest, and Yahoo.</span></span>
> 
> <span data-ttu-id="b7db4-106">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="b7db4-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="b7db4-107">如何根據地址產生對應。</span><span class="sxs-lookup"><span data-stu-id="b7db4-107">How to generate a map based on an address.</span></span>
> - <span data-ttu-id="b7db4-108">如何根據緯度和經度座標產生地圖。</span><span class="sxs-lookup"><span data-stu-id="b7db4-108">How to generate a map based on latitude and longitude coordinates.</span></span>
> - <span data-ttu-id="b7db4-109">如何註冊 Bing Maps 開發人員帳戶，並取得金鑰以與 Bing 地圖服務搭配使用。</span><span class="sxs-lookup"><span data-stu-id="b7db4-109">How to register a Bing Maps Developer Account and get a key to use with Bing Maps.</span></span>
> 
> <span data-ttu-id="b7db4-110">這是本文中引進的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="b7db4-110">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="b7db4-111">`Maps` helper。</span><span class="sxs-lookup"><span data-stu-id="b7db4-111">The `Maps` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b7db4-112">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="b7db4-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="b7db4-113">ASP.NET Web Pages （Razor）2</span><span class="sxs-lookup"><span data-stu-id="b7db4-113">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="b7db4-114">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="b7db4-114">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="b7db4-115">本教學課程也適用于 WebMatrix 3。</span><span class="sxs-lookup"><span data-stu-id="b7db4-115">This tutorial also works with WebMatrix 3.</span></span>

<span data-ttu-id="b7db4-116">在網頁中，您可以使用 `Maps` helper，在頁面上顯示地圖。</span><span class="sxs-lookup"><span data-stu-id="b7db4-116">In Web Pages, you can display maps on a page by using `Maps` helper.</span></span> <span data-ttu-id="b7db4-117">您可以根據地址或一組經度和緯度座標來產生對應。</span><span class="sxs-lookup"><span data-stu-id="b7db4-117">You can generate maps based either on an address or on a set of longitude and latitude coordinates.</span></span> <span data-ttu-id="b7db4-118">`Maps` 類別可讓您呼叫熱門的地圖引擎，包括 Bing、Google、MapQuest 和 Yahoo。</span><span class="sxs-lookup"><span data-stu-id="b7db4-118">The `Maps` class lets you call into popular map engines including Bing, Google, MapQuest, and Yahoo.</span></span>

<span data-ttu-id="b7db4-119">無論您呼叫哪一個對應引擎，將對應加入至頁面的步驟都相同。</span><span class="sxs-lookup"><span data-stu-id="b7db4-119">The steps for adding mapping to a page are the same regardless of which of the map engines you call.</span></span> <span data-ttu-id="b7db4-120">您只需要新增 JavaScript 檔案參考，讓可用的方法顯示對應，然後再呼叫 `Maps` helper 的方法。</span><span class="sxs-lookup"><span data-stu-id="b7db4-120">You just add a JavaScript file reference that makes available methods to display the map, and then you call methods of the `Maps` helper.</span></span>

<span data-ttu-id="b7db4-121">您可以根據您使用的 `Maps` helper 方法選擇對應服務。</span><span class="sxs-lookup"><span data-stu-id="b7db4-121">You choose a map service based on which `Maps` helper method you use.</span></span> <span data-ttu-id="b7db4-122">您可以使用下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="b7db4-122">You can use any of these:</span></span>

- `Maps.GetBingHtml`
- `Maps.GetGoogleHtml`
- `Maps.GetYahooHtml`
- `Maps.GetMapQuestHtml`

## <a name="installing-the-pieces-you-need"></a><span data-ttu-id="b7db4-123">安裝您需要的部分</span><span class="sxs-lookup"><span data-stu-id="b7db4-123">Installing the Pieces You Need</span></span>

<span data-ttu-id="b7db4-124">若要顯示地圖，您需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="b7db4-124">To display maps, you need these pieces:</span></span>

- <span data-ttu-id="b7db4-125">`Maps` helper。</span><span class="sxs-lookup"><span data-stu-id="b7db4-125">The `Maps` helper.</span></span> <span data-ttu-id="b7db4-126">此 helper 位於 ASP.NET Web helper 程式庫的第2版。</span><span class="sxs-lookup"><span data-stu-id="b7db4-126">This helper is in version 2 of the ASP.NET Web Helpers Library.</span></span> <span data-ttu-id="b7db4-127">如果您尚未新增程式庫，您可以將它安裝在您的網站中做為 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="b7db4-127">If you haven't already added the library, you can install it in your site as a NuGet package.</span></span> <span data-ttu-id="b7db4-128">如需詳細資訊，請參閱[在 ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)。</span><span class="sxs-lookup"><span data-stu-id="b7db4-128">For details, see [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372).</span></span> <span data-ttu-id="b7db4-129">（在資源庫中，搜尋 `microsoft-web-helpers` 套件）。</span><span class="sxs-lookup"><span data-stu-id="b7db4-129">(In the Gallery, search for the `microsoft-web-helpers` package.)</span></span>
- <span data-ttu-id="b7db4-130">JQuery 程式庫。</span><span class="sxs-lookup"><span data-stu-id="b7db4-130">The jQuery library.</span></span> <span data-ttu-id="b7db4-131">其中幾個 WebMatrix 網站範本在其*腳本*資料夾中已經包含 jQuery 程式庫。</span><span class="sxs-lookup"><span data-stu-id="b7db4-131">Several of the WebMatrix site templates already include jQuery libraries in their *Script* folders.</span></span> <span data-ttu-id="b7db4-132">如果您沒有這些程式庫，您可以直接從[jQuery.org](http://jQuery.org)網站下載最新的 jQuery 程式庫。</span><span class="sxs-lookup"><span data-stu-id="b7db4-132">If you do not have these libraries, you can download the latest jQuery library directly from the [jQuery.org](http://jQuery.org) site.</span></span> <span data-ttu-id="b7db4-133">或者，您可以使用範本建立新的網站（例如，**入門網站**範本），然後將 jQuery 檔案從該網站複製到目前的網站。</span><span class="sxs-lookup"><span data-stu-id="b7db4-133">Or you can create a new site using a template (for example, the **Starter Site** template) and then copy the jQuery files from that site to your current site.</span></span>

<span data-ttu-id="b7db4-134">最後，如果您想要使用 Bing 地圖服務，則必須先建立（免費）帳戶，並取得金鑰。</span><span class="sxs-lookup"><span data-stu-id="b7db4-134">Finally, if you want to use Bing maps, you must first create a (free) account and get a key.</span></span> <span data-ttu-id="b7db4-135">若要取得金鑰，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b7db4-135">To get a key, follow these steps:</span></span>

1. <span data-ttu-id="b7db4-136">在[Bing Maps 開發人員帳戶](https://www.microsoft.com/maps/developers/web.aspx)上建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7db4-136">Create an account on the [Bing Maps Developer Account](https://www.microsoft.com/maps/developers/web.aspx).</span></span> <span data-ttu-id="b7db4-137">您也必須擁有 Microsoft 帳戶（Windows Live ID）。</span><span class="sxs-lookup"><span data-stu-id="b7db4-137">You must have a Microsoft account (Windows Live ID) as well.</span></span>

    <span data-ttu-id="b7db4-138">您可以指定要使用金鑰進行**評估/測試**。</span><span class="sxs-lookup"><span data-stu-id="b7db4-138">You can specify that you want to use the key for **Evaluation/Test**.</span></span> <span data-ttu-id="b7db4-139">如果您要使用 WebMatrix 和 IIS Express 在自己的電腦上測試對應功能，請移至 [**網站**] 工作區，並記下網站的 URL （例如，`http://localhost:50408`，雖然您的埠號碼可能會不同）。</span><span class="sxs-lookup"><span data-stu-id="b7db4-139">If you are testing the mapping function on your own computer using WebMatrix and IIS Express, go the **Site** workspace and note the URL of your site (for example, `http://localhost:50408`, although your port number will probably be different).</span></span> <span data-ttu-id="b7db4-140">當您註冊時，您可以使用此*localhost*位址作為網站。</span><span class="sxs-lookup"><span data-stu-id="b7db4-140">You can use this *localhost* address as the site when you register.</span></span>
2. <span data-ttu-id="b7db4-141">在您註冊帳戶之後，請前往 Bing Maps 帳戶中心，然後按一下 [**建立或查看金鑰**]：</span><span class="sxs-lookup"><span data-stu-id="b7db4-141">After you have registered for an account, go to the Bing Maps Account Center and click **Create or view keys**:</span></span>

    ![對應-2](displaying-maps-in-an-aspnet-web-pages-site/_static/image1.png)
3. <span data-ttu-id="b7db4-143">記錄 Bing 所建立的金鑰。</span><span class="sxs-lookup"><span data-stu-id="b7db4-143">Record the key that Bing creates.</span></span>

## <a name="creating-a-map-based-on-an-address-using-google"></a><span data-ttu-id="b7db4-144">根據地址建立對應（使用 Google）</span><span class="sxs-lookup"><span data-stu-id="b7db4-144">Creating a Map Based on an Address (Using Google)</span></span>

<span data-ttu-id="b7db4-145">下列範例示範如何建立頁面，以根據地址來呈現地圖。</span><span class="sxs-lookup"><span data-stu-id="b7db4-145">The following example shows how to create a page that renders a map based on an address.</span></span> <span data-ttu-id="b7db4-146">此範例示範如何使用 Google Maps。</span><span class="sxs-lookup"><span data-stu-id="b7db4-146">This example shows how to use Google Maps.</span></span>

1. <span data-ttu-id="b7db4-147">在網站的根目錄中建立名為*MapAddress*的檔案。</span><span class="sxs-lookup"><span data-stu-id="b7db4-147">Create a file named *MapAddress.cshtml* in the root of the site.</span></span> <span data-ttu-id="b7db4-148">此頁面會根據您傳遞給它的位址來產生對應。</span><span class="sxs-lookup"><span data-stu-id="b7db4-148">This page will generate a map based on an address that you pass to it.</span></span>
2. <span data-ttu-id="b7db4-149">將下列程式碼複製到檔案中，並覆寫現有的內容。</span><span class="sxs-lookup"><span data-stu-id="b7db4-149">Copy the following code into the file, overwriting the existing content.</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="b7db4-150">請注意頁面的下列功能：</span><span class="sxs-lookup"><span data-stu-id="b7db4-150">Notice the following features of the page:</span></span>

    - <span data-ttu-id="b7db4-151">`<head>` 元素中的 `<script>` 元素。</span><span class="sxs-lookup"><span data-stu-id="b7db4-151">The `<script>` element in the `<head>` element.</span></span> <span data-ttu-id="b7db4-152">在範例中，`<script>` 元素會參考*jquery-1.7.2.min.js 1.6.4*檔案，這是 jquery 程式庫（版本1.6.4）的縮減（壓縮）版本。</span><span class="sxs-lookup"><span data-stu-id="b7db4-152">In the example, the `<script>` element references the *jquery-1.6.4.min.js* file, which is a minified (compressed) version of the jQuery library, version 1.6.4.</span></span> <span data-ttu-id="b7db4-153">請注意，此參考會假設 *.js*檔案位於您網站的 [*腳本*] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="b7db4-153">Note that the reference assumes that the *.js* file is in the *Scripts* folder of your site.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="b7db4-154">如果您使用的是不同版本的 jQuery 程式庫，請確定您正確地指向該版本。</span><span class="sxs-lookup"><span data-stu-id="b7db4-154">If you're using a different version of the jQuery library, just make sure that you're pointing to that version correctly.</span></span>
    - <span data-ttu-id="b7db4-155">呼叫頁面主體中的 `@Maps.GetGoogleHtml`。</span><span class="sxs-lookup"><span data-stu-id="b7db4-155">The call to the `@Maps.GetGoogleHtml` in the body of the page.</span></span> <span data-ttu-id="b7db4-156">若要對應位址，您必須傳遞位址字串。</span><span class="sxs-lookup"><span data-stu-id="b7db4-156">To map an address, you must pass an address string.</span></span> <span data-ttu-id="b7db4-157">其他對應引擎的方法會以類似的方式（`@Maps.GetYahooHtml`、`@Maps.GetMapQuestHtml`）來工作。</span><span class="sxs-lookup"><span data-stu-id="b7db4-157">The methods for the other map engines work in a similar way (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).</span></span>
3. <span data-ttu-id="b7db4-158">執行頁面並輸入位址。</span><span class="sxs-lookup"><span data-stu-id="b7db4-158">Run the page and enter an address.</span></span> <span data-ttu-id="b7db4-159">此頁面會顯示以 Google Maps 為基礎的地圖，其中會顯示您指定的位置。</span><span class="sxs-lookup"><span data-stu-id="b7db4-159">The page displays a map, based on Google Maps, that shows the location that you specified.</span></span>

     ![對應-1](displaying-maps-in-an-aspnet-web-pages-site/_static/image2.png)

## <a name="creating-a-map-based-on-latitude-and-longitude-coordinates-using-bing"></a><span data-ttu-id="b7db4-161">根據緯度和經度座標建立地圖（使用 Bing）</span><span class="sxs-lookup"><span data-stu-id="b7db4-161">Creating a Map Based on Latitude and Longitude Coordinates (Using Bing)</span></span>

<span data-ttu-id="b7db4-162">這個範例示範如何根據座標建立地圖。</span><span class="sxs-lookup"><span data-stu-id="b7db4-162">This example shows how to create a map based on coordinates.</span></span> <span data-ttu-id="b7db4-163">此範例示範如何使用 Bing 地圖服務，以及如何包含 Bing 金鑰。</span><span class="sxs-lookup"><span data-stu-id="b7db4-163">This example shows how to use Bing maps and how to include your Bing key.</span></span> <span data-ttu-id="b7db4-164">（您也可以使用其他地圖引擎來建立以座標為基礎的對應，而不使用 Bing 金鑰）。</span><span class="sxs-lookup"><span data-stu-id="b7db4-164">(You can create a map based on coordinates using the other map engines also, without using a Bing key.)</span></span>

1. <span data-ttu-id="b7db4-165">在網站的根目錄中建立名為*MapCoordinates*的檔案，並以下列程式碼和標記取代現有的內容：</span><span class="sxs-lookup"><span data-stu-id="b7db4-165">Create a file named *MapCoordinates.cshtml* in the root of the site and replace the existing content with the following code and markup:</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample2.cshtml)]
2. <span data-ttu-id="b7db4-166">將 `your-key-here` 取代為您稍早產生的 Bing 地圖服務金鑰。</span><span class="sxs-lookup"><span data-stu-id="b7db4-166">Replace `your-key-here` with the Bing Maps key that you generated earlier.</span></span>
3. <span data-ttu-id="b7db4-167">執行 [ *MapCoordinates* ] 頁面，輸入緯度和經度座標，然後按一下**地圖！**</span><span class="sxs-lookup"><span data-stu-id="b7db4-167">Run the *MapCoordinates.cshtml* page, enter latitude and longitude coordinates, and then click the **Map It!**</span></span> <span data-ttu-id="b7db4-168">按鈕。</span><span class="sxs-lookup"><span data-stu-id="b7db4-168">button.</span></span> <span data-ttu-id="b7db4-169">（如果您不知道任何座標，請嘗試下列動作。</span><span class="sxs-lookup"><span data-stu-id="b7db4-169">(If you don't know any coordinates, try the following.</span></span> <span data-ttu-id="b7db4-170">這是 Microsoft Redmond 校園的位置）。</span><span class="sxs-lookup"><span data-stu-id="b7db4-170">This is a location on the Microsoft Redmond campus.)</span></span>

   - <span data-ttu-id="b7db4-171">緯度：47.6781005859375</span><span class="sxs-lookup"><span data-stu-id="b7db4-171">Latitude: 47.6781005859375</span></span>
   - <span data-ttu-id="b7db4-172">經度：-122.158317565918</span><span class="sxs-lookup"><span data-stu-id="b7db4-172">Longitude: -122.158317565918</span></span>

     <span data-ttu-id="b7db4-173">頁面會使用您所指定的座標來顯示。</span><span class="sxs-lookup"><span data-stu-id="b7db4-173">The page is displayed using the coordinates that you specified.</span></span>

     ![對應-3](displaying-maps-in-an-aspnet-web-pages-site/_static/image3.png)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="b7db4-175">其他資源</span><span class="sxs-lookup"><span data-stu-id="b7db4-175">Additional Resources</span></span>

[<span data-ttu-id="b7db4-176">Microsoft Maps API 參考</span><span class="sxs-lookup"><span data-stu-id="b7db4-176">Microsoft.Maps API Reference</span></span>](https://msdn.microsoft.com/library/gg427611.aspx)
