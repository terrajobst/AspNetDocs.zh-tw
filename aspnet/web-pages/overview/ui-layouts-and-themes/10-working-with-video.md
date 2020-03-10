---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: 在 ASP.NET Web Pages （Razor）網站中顯示影片 |Microsoft Docs
author: Rick-Anderson
description: 本章說明如何使用 Razor 語法頁面在 ASP.NET Web Pages 中顯示影片。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: 516d46f38ce8910209f4207c474b0404bf012950
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628944"
---
# <a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="7d207-103">在 ASP.NET Web Pages （Razor）網站中顯示影片</span><span class="sxs-lookup"><span data-stu-id="7d207-103">Displaying Video in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="7d207-104">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="7d207-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="7d207-105">本文說明如何使用 ASP.NET Web Pages （Razor）網站中的影片（媒體）播放機，讓使用者能夠觀看儲存在網站上的影片。</span><span class="sxs-lookup"><span data-stu-id="7d207-105">This article explains how to use a video (media) player in an ASP.NET Web Pages (Razor) website to let users view videos that are stored on the site.</span></span> <span data-ttu-id="7d207-106">Razor 語法的 ASP.NET Web Pages 可讓您播放 Flash （*swf*）、媒體播放機（ *.Wmv*）和 Silverlight （ *.xap*）影片。</span><span class="sxs-lookup"><span data-stu-id="7d207-106">ASP.NET Web Pages with Razor syntax lets you play Flash (*.swf*), Media Player (*.wmv*), and Silverlight (*.xap*) videos.</span></span>
> 
> <span data-ttu-id="7d207-107">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="7d207-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="7d207-108">如何選擇影片播放機。</span><span class="sxs-lookup"><span data-stu-id="7d207-108">How to choose a video player.</span></span>
> - <span data-ttu-id="7d207-109">如何將影片新增至網頁。</span><span class="sxs-lookup"><span data-stu-id="7d207-109">How to add video to a web page.</span></span>
> - <span data-ttu-id="7d207-110">如何設定影片播放者屬性。</span><span class="sxs-lookup"><span data-stu-id="7d207-110">How to set video player attributes.</span></span>
> 
> <span data-ttu-id="7d207-111">以下是文章中引進的 ASP.NET Razor pages 功能：</span><span class="sxs-lookup"><span data-stu-id="7d207-111">These are the ASP.NET Razor pages features introduced in the article:</span></span>
> 
> - <span data-ttu-id="7d207-112">`Video` helper。</span><span class="sxs-lookup"><span data-stu-id="7d207-112">The `Video` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="7d207-113">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="7d207-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="7d207-114">ASP.NET Web Pages （Razor）2</span><span class="sxs-lookup"><span data-stu-id="7d207-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="7d207-115">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="7d207-115">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="7d207-116">本教學課程也適用于 WebMatrix 3。</span><span class="sxs-lookup"><span data-stu-id="7d207-116">This tutorial also works with WebMatrix 3.</span></span>

## <a name="introduction"></a><span data-ttu-id="7d207-117">簡介</span><span class="sxs-lookup"><span data-stu-id="7d207-117">Introduction</span></span>

<span data-ttu-id="7d207-118">您可能想要在您的網站上顯示影片。</span><span class="sxs-lookup"><span data-stu-id="7d207-118">You might want to display a video on your site.</span></span> <span data-ttu-id="7d207-119">其中一種方法是連結至已經有影片的網站，例如 YouTube。</span><span class="sxs-lookup"><span data-stu-id="7d207-119">One way to do that is to link to a site that already has the video, like YouTube.</span></span> <span data-ttu-id="7d207-120">如果您想要直接在自己的頁面中內嵌這些網站的影片，通常可以從網站取得 HTML 標籤，然後將它複製到您的頁面。</span><span class="sxs-lookup"><span data-stu-id="7d207-120">If you want to embed a video from these sites directly in your own pages, you can usually get HTML markup from the site and then copy it into your page.</span></span> <span data-ttu-id="7d207-121">例如，下列範例顯示如何內嵌 YouTube 影片：</span><span class="sxs-lookup"><span data-stu-id="7d207-121">For example, the following example shows how to embed a YouTube video:</span></span>

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

<span data-ttu-id="7d207-122">如果您想要播放自己網站上的影片（而不是在公用的影片分享網站），您無法使用像這樣的內嵌標記直接連結到它。</span><span class="sxs-lookup"><span data-stu-id="7d207-122">If you want to play a video that's on your own website (not on a public video-sharing site), you can't directly link to it using embedded markup like this.</span></span> <span data-ttu-id="7d207-123">不過，您可以使用 [`Video` 協助程式] 從網站播放影片，這會直接在頁面中轉譯媒體播放機。</span><span class="sxs-lookup"><span data-stu-id="7d207-123">However, you can play videos from your site by using the `Video` helper, which renders a media player directly in a page.</span></span>

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a><span data-ttu-id="7d207-124">選擇影片播放機</span><span class="sxs-lookup"><span data-stu-id="7d207-124">Choosing a Video Player</span></span>

<span data-ttu-id="7d207-125">影片檔案有許多格式，而且每種格式通常需要不同的播放程式和不同的方式來設定玩家。</span><span class="sxs-lookup"><span data-stu-id="7d207-125">There are lots of formats for video files, and each format typically requires a different player and a different way to configure the player.</span></span> <span data-ttu-id="7d207-126">在 ASP.NET Razor pages 中，您可以使用 `Video` 協助程式在網頁中播放影片。</span><span class="sxs-lookup"><span data-stu-id="7d207-126">In ASP.NET Razor pages, you can play a video in a web page using the `Video` helper.</span></span> <span data-ttu-id="7d207-127">`Video` helper 會簡化在網頁中內嵌影片的程式，因為它會自動產生 `object` 和 `embed` 的 HTML 專案，通常用來將影片新增至頁面。</span><span class="sxs-lookup"><span data-stu-id="7d207-127">The `Video` helper simplifies the process of embedding videos in a web page because it automatically generates the `object` and `embed` HTML elements that are normally used to add video to the page.</span></span>

<span data-ttu-id="7d207-128">`Video` helper 支援下列媒體播放機：</span><span class="sxs-lookup"><span data-stu-id="7d207-128">The `Video` helper supports the following media players:</span></span>

- <span data-ttu-id="7d207-129">Adobe Flash</span><span class="sxs-lookup"><span data-stu-id="7d207-129">Adobe Flash</span></span>
- <span data-ttu-id="7d207-130">Windows MediaPlayer</span><span class="sxs-lookup"><span data-stu-id="7d207-130">Windows MediaPlayer</span></span>
- <span data-ttu-id="7d207-131">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="7d207-131">Microsoft Silverlight</span></span>

### <a name="the-flash-player"></a><span data-ttu-id="7d207-132">Flash Player</span><span class="sxs-lookup"><span data-stu-id="7d207-132">The Flash Player</span></span>

<span data-ttu-id="7d207-133">`Video` 協助程式的 `Flash` 播放程式，可讓您在網頁中播放 Flash 影片（*swf*檔案）。</span><span class="sxs-lookup"><span data-stu-id="7d207-133">The `Flash` player of the `Video` helper let you play Flash videos (*.swf* files) in a web page.</span></span> <span data-ttu-id="7d207-134">您至少必須提供影片檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="7d207-134">At a minimum, you have to provide a path to the video file.</span></span> <span data-ttu-id="7d207-135">如果您沒有指定路徑，則播放程式會使用目前版本的 Flash 所設定的預設值。</span><span class="sxs-lookup"><span data-stu-id="7d207-135">If you specify nothing but the path, the player uses default values that are set by the current version of Flash.</span></span> <span data-ttu-id="7d207-136">典型的預設設定為：</span><span class="sxs-lookup"><span data-stu-id="7d207-136">Typical default settings are:</span></span>

- <span data-ttu-id="7d207-137">影片會使用其預設的寬度和高度，而不含背景色彩來顯示。</span><span class="sxs-lookup"><span data-stu-id="7d207-137">The video is displayed using its default width and height and without a background color.</span></span>
- <span data-ttu-id="7d207-138">影片會在頁面載入時自動播放。</span><span class="sxs-lookup"><span data-stu-id="7d207-138">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="7d207-139">影片會持續迴圈，直到明確停止為止。</span><span class="sxs-lookup"><span data-stu-id="7d207-139">The video loops continuously until it's explicitly stopped.</span></span>
- <span data-ttu-id="7d207-140">影片會縮放以顯示所有影片，而不是裁剪影片以符合特定大小。</span><span class="sxs-lookup"><span data-stu-id="7d207-140">The video is scaled to show all of the video, rather than cropping the video to fit a specific size.</span></span>
- <span data-ttu-id="7d207-141">影片會在視窗中播放。</span><span class="sxs-lookup"><span data-stu-id="7d207-141">The video plays in a window.</span></span>

### <a name="the-mediaplayer-player"></a><span data-ttu-id="7d207-142">MediaPlayer Player</span><span class="sxs-lookup"><span data-stu-id="7d207-142">The MediaPlayer Player</span></span>

<span data-ttu-id="7d207-143">`Video` 協助程式的 [`MediaPlayer` 播放程式] 可讓您在網頁中播放 Windows Media 影片（ *.wmv*檔案）、windows media audio （ *.wma*檔案）和 mp3 （*mp3*檔案）。</span><span class="sxs-lookup"><span data-stu-id="7d207-143">The `MediaPlayer` player of the `Video` helper lets you play Windows Media videos (*.wmv* files), Windows Media audio (*.wma* files), and MP3 (*.mp3* files) in a web page.</span></span> <span data-ttu-id="7d207-144">您必須包含要播放之媒體檔案的路徑;所有其他參數都是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="7d207-144">You must include path of the media file to play; all other parameters are optional.</span></span> <span data-ttu-id="7d207-145">如果您只指定路徑，播放程式會使用目前版本的 MediaPlayer 所設定的預設設定，例如：</span><span class="sxs-lookup"><span data-stu-id="7d207-145">If you specify only a path, the player uses default settings set by the current version of MediaPlayer, such as:</span></span>

- <span data-ttu-id="7d207-146">影片會使用其預設的寬度和高度來顯示。</span><span class="sxs-lookup"><span data-stu-id="7d207-146">The video is displayed using its default width and height.</span></span>
- <span data-ttu-id="7d207-147">影片會在頁面載入時自動播放。</span><span class="sxs-lookup"><span data-stu-id="7d207-147">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="7d207-148">影片會播放一次（它不會迴圈）。</span><span class="sxs-lookup"><span data-stu-id="7d207-148">The video plays once (it doesn't loop).</span></span>
- <span data-ttu-id="7d207-149">Media player 會在使用者介面中顯示一組完整的控制項。</span><span class="sxs-lookup"><span data-stu-id="7d207-149">The player displays the full set of controls in the user interface.</span></span>
- <span data-ttu-id="7d207-150">影片會在視窗中播放。</span><span class="sxs-lookup"><span data-stu-id="7d207-150">The video plays in a window.</span></span>

### <a name="the-silverlight-player"></a><span data-ttu-id="7d207-151">Silverlight Player</span><span class="sxs-lookup"><span data-stu-id="7d207-151">The Silverlight Player</span></span>

<span data-ttu-id="7d207-152">`Video` 協助程式的 `Silverlight` 播放程式可讓您播放 Windows Media 視訊（ *.wmv*檔案）、Windows Media 音訊（ *.wma*檔案）和 mp3 （*mp3*檔案）。</span><span class="sxs-lookup"><span data-stu-id="7d207-152">The `Silverlight` player of the `Video` helper lets you play Windows Media Video (*.wmv* files), Windows Media Audio (*.wma* files), and MP3 (*.mp3* files).</span></span> <span data-ttu-id="7d207-153">您必須設定 path 參數，以指向 Silverlight 應用程式封裝（ *.xap*檔案）。</span><span class="sxs-lookup"><span data-stu-id="7d207-153">You must set the path parameter to point to a Silverlight-based application package (*.xap* file).</span></span> <span data-ttu-id="7d207-154">您也必須設定 width 和 height 參數。</span><span class="sxs-lookup"><span data-stu-id="7d207-154">You also must set the width and height parameters.</span></span> <span data-ttu-id="7d207-155">所有其他參數皆為選擇性使用。</span><span class="sxs-lookup"><span data-stu-id="7d207-155">All other parameters are optional.</span></span> <span data-ttu-id="7d207-156">當您使用 Silverlight player for video 時，如果您只設定必要的參數，Silverlight 播放程式會顯示沒有背景色彩的影片。</span><span class="sxs-lookup"><span data-stu-id="7d207-156">When you use the Silverlight player for video, if you set only the required parameters, the Silverlight player displays the video without a background color.</span></span>

> [!NOTE]
> <span data-ttu-id="7d207-157">如果您還不知道 Silverlight： *.xap*檔案是一個壓縮檔案，其中包含 *.xaml*檔案中的版面配置指示、元件中的 managed 程式碼，以及選擇性的資源。</span><span class="sxs-lookup"><span data-stu-id="7d207-157">In case you don't already know Silverlight: the *.xap* file is a compressed file that contains layout instructions in a *.xaml* file, managed code in assemblies, and optional resources.</span></span> <span data-ttu-id="7d207-158">您可以在 Visual Studio 中建立 *.xap*檔案作為 Silverlight 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="7d207-158">You can create a *.xap* file in Visual Studio as a Silverlight application project.</span></span>

<span data-ttu-id="7d207-159">`Silverlight` 影片播放程式會使用您為播放程式提供的設定，以及 *.xap*檔案中提供的設定。</span><span class="sxs-lookup"><span data-stu-id="7d207-159">The `Silverlight` video player uses both the settings that you provide for the player and the settings that are provided in the *.xap* file.</span></span>

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a><span data-ttu-id="7d207-160">MIME 類型</span><span class="sxs-lookup"><span data-stu-id="7d207-160">MIME Types</span></span>
> 
> <span data-ttu-id="7d207-161">當瀏覽器下載檔案時，瀏覽器會確定檔案類型符合所要轉譯之檔所指定的 MIME 類型。</span><span class="sxs-lookup"><span data-stu-id="7d207-161">When a browser downloads a file, the browser makes sure that the file type matches the MIME type that's specified for the document that's being rendered.</span></span> <span data-ttu-id="7d207-162">MIME 類型是檔案的內容類型或媒體類型。</span><span class="sxs-lookup"><span data-stu-id="7d207-162">The MIME type is the content type or media type of a file.</span></span> <span data-ttu-id="7d207-163">`Video` helper 會使用下列 MIME 類型：</span><span class="sxs-lookup"><span data-stu-id="7d207-163">The `Video` helper uses the following MIME types:</span></span>
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`

<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a><span data-ttu-id="7d207-164">播放 Flash （swf）影片</span><span class="sxs-lookup"><span data-stu-id="7d207-164">Playing Flash (.swf) Videos</span></span>

<span data-ttu-id="7d207-165">此程式說明如何播放名為*sample*的 Flash 影片。</span><span class="sxs-lookup"><span data-stu-id="7d207-165">This procedure shows you how to play a Flash video named *sample.swf*.</span></span> <span data-ttu-id="7d207-166">此程式假設您的網站上已有名為*Media*的資料夾，且該資料夾中的 swf 檔案為 *。*</span><span class="sxs-lookup"><span data-stu-id="7d207-166">The procedure assumes that you've got a folder named *Media* on your site and that the *.swf* file is in that folder.</span></span>

1. <span data-ttu-id="7d207-167">如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果尚未新增）。</span><span class="sxs-lookup"><span data-stu-id="7d207-167">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="7d207-168">在網站中，新增頁面，並將它命名為*FlashVideo*。</span><span class="sxs-lookup"><span data-stu-id="7d207-168">In the website, add a page and name it *FlashVideo.cshtml*.</span></span>
3. <span data-ttu-id="7d207-169">將下列標記新增至頁面：</span><span class="sxs-lookup"><span data-stu-id="7d207-169">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. <span data-ttu-id="7d207-170">在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="7d207-170">Run the page in a browser.</span></span> <span data-ttu-id="7d207-171">（在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）頁面隨即顯示，且影片會自動播放。</span><span class="sxs-lookup"><span data-stu-id="7d207-171">(Make sure the page is selected in the **Files** workspace before you run it.) The page is displayed and the video plays automatically.</span></span> 

    <span data-ttu-id="7d207-172">![包](10-working-with-video/_static/image1.jpg "ch08_video-1 .jpg")</span><span class="sxs-lookup"><span data-stu-id="7d207-172">![[image]](10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")</span></span>

<span data-ttu-id="7d207-173">您可以將 Flash 影片的 `quality` 參數設定為 `low`、`autolow`、`autohigh`、`medium`、`high`和 `best`：</span><span class="sxs-lookup"><span data-stu-id="7d207-173">You can set the `quality` parameter for a Flash video to `low`, `autolow`, `autohigh`, `medium`, `high`, and `best`:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

<span data-ttu-id="7d207-174">您可以使用 `scale` 參數，將 Flash 影片變更為以特定大小播放，您可以將其設定為下列內容：</span><span class="sxs-lookup"><span data-stu-id="7d207-174">You can change the Flash video to play at a specific size using the `scale` parameter, which you can set to the following:</span></span>

- <span data-ttu-id="7d207-175">`showall`</span><span class="sxs-lookup"><span data-stu-id="7d207-175">`showall`.</span></span> <span data-ttu-id="7d207-176">這會讓整個影片可見，同時維持原始外觀比例。</span><span class="sxs-lookup"><span data-stu-id="7d207-176">This makes the entire video visible while maintaining the original aspect ratio.</span></span> <span data-ttu-id="7d207-177">不過，您最後可能會在每一端加上框線。</span><span class="sxs-lookup"><span data-stu-id="7d207-177">However, you might end up with borders on each side.</span></span>
- <span data-ttu-id="7d207-178">`noorder`</span><span class="sxs-lookup"><span data-stu-id="7d207-178">`noorder`.</span></span> <span data-ttu-id="7d207-179">這會調整影片，同時維持原始外觀比例，但可能會進行裁剪。</span><span class="sxs-lookup"><span data-stu-id="7d207-179">This scales the video while maintaining the original aspect ratio, but it might be cropped.</span></span>
- <span data-ttu-id="7d207-180">`exactfit`</span><span class="sxs-lookup"><span data-stu-id="7d207-180">`exactfit`.</span></span> <span data-ttu-id="7d207-181">如此一來，整個影片就會顯示出來，而不會保留原始的外觀比例，但可能會發生失真。</span><span class="sxs-lookup"><span data-stu-id="7d207-181">This makes the entire video visible without preserving the original aspect ratio, but distortion may occur.</span></span>

<span data-ttu-id="7d207-182">如果您未指定 `scale` 參數，則會顯示整段影片，且不會進行任何裁剪而維持原始外觀比例。</span><span class="sxs-lookup"><span data-stu-id="7d207-182">If you don't specify a `scale` parameter, the entire video will be visible and the original aspect ratio will be maintained without any cropping.</span></span> <span data-ttu-id="7d207-183">下列範例顯示如何使用 `scale` 參數：</span><span class="sxs-lookup"><span data-stu-id="7d207-183">The following example shows how to use the `scale` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

<span data-ttu-id="7d207-184">Flash player 支援名為 `windowMode`的影片模式設定。</span><span class="sxs-lookup"><span data-stu-id="7d207-184">The Flash player supports a video mode setting named `windowMode`.</span></span> <span data-ttu-id="7d207-185">您可以將此設定為 [`window`]、[`opaque`] 和 [`transparent`]。</span><span class="sxs-lookup"><span data-stu-id="7d207-185">You can set this to `window`, `opaque`, and `transparent`.</span></span> <span data-ttu-id="7d207-186">根據預設，`windowMode` 設定為 [`window`]，這會在網頁的另一個視窗中顯示影片。</span><span class="sxs-lookup"><span data-stu-id="7d207-186">By default, the `windowMode` is set to `window`, which displays the video in a separate window on the web page.</span></span> <span data-ttu-id="7d207-187">[`opaque`] 設定會隱藏網頁上影片背後的所有內容。</span><span class="sxs-lookup"><span data-stu-id="7d207-187">The `opaque` setting hides everything behind the video on the web page.</span></span> <span data-ttu-id="7d207-188">[`transparent`] 設定可讓網頁的背景顯示在影片中，假設影片的任何部分都是透明的。</span><span class="sxs-lookup"><span data-stu-id="7d207-188">The `transparent` setting lets the background of the web page show through the video, assuming any part of the video is transparent.</span></span>

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a><span data-ttu-id="7d207-189">播放 MediaPlayer （*wmv*）影片</span><span class="sxs-lookup"><span data-stu-id="7d207-189">Playing MediaPlayer (*.wmv*) Videos</span></span>

<span data-ttu-id="7d207-190">下列程式說明如何播放名為*sample*的 Window media 影片，其位於*Media*資料夾中。</span><span class="sxs-lookup"><span data-stu-id="7d207-190">The following procedure shows you how to play a Window Media video named *sample.wmv* that's in the *Media* folder.</span></span>

1. <span data-ttu-id="7d207-191">如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果尚未這麼做）。</span><span class="sxs-lookup"><span data-stu-id="7d207-191">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="7d207-192">建立名為*MediaPlayerVideo*的新頁面。</span><span class="sxs-lookup"><span data-stu-id="7d207-192">Create a new page named *MediaPlayerVideo.cshtml*.</span></span>
3. <span data-ttu-id="7d207-193">將下列標記新增至頁面：</span><span class="sxs-lookup"><span data-stu-id="7d207-193">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. <span data-ttu-id="7d207-194">在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="7d207-194">Run the page in a browser.</span></span> <span data-ttu-id="7d207-195">影片會自動載入並播放。</span><span class="sxs-lookup"><span data-stu-id="7d207-195">The video loads and plays automatically.</span></span> 

    <span data-ttu-id="7d207-196">![包](10-working-with-video/_static/image2.jpg "ch08_video-2 .jpg")</span><span class="sxs-lookup"><span data-stu-id="7d207-196">![[image]](10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")</span></span>

<span data-ttu-id="7d207-197">您可以將 `playCount` 設定為整數，以指出自動播放影片的次數：</span><span class="sxs-lookup"><span data-stu-id="7d207-197">You can set `playCount` to an integer that indicates how many times to play the video automatically:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

<span data-ttu-id="7d207-198">`uiMode` 參數可讓您指定要在使用者介面中顯示的控制項。</span><span class="sxs-lookup"><span data-stu-id="7d207-198">The `uiMode` parameter lets you specify which controls show up in the user interface.</span></span> <span data-ttu-id="7d207-199">您可以將 `uiMode` 設定為 [`invisible`]、[`none`]、[`mini`] 或 [`full`]。</span><span class="sxs-lookup"><span data-stu-id="7d207-199">You can set `uiMode` to `invisible`, `none`, `mini`, or `full`.</span></span> <span data-ttu-id="7d207-200">如果您未指定 `uiMode` 參數，除了影片視窗之外，影片也會顯示 [狀態] 視窗、[搜尋列]、[控制項] 按鈕和 [音量] 控制項。</span><span class="sxs-lookup"><span data-stu-id="7d207-200">If you don't specify a `uiMode` parameter, the video will be displayed with the status window, seek bar, control buttons, and volume controls in addition to the video window.</span></span> <span data-ttu-id="7d207-201">如果您使用播放程式播放音訊檔案，也會顯示這些控制項。</span><span class="sxs-lookup"><span data-stu-id="7d207-201">These controls will also be displayed if you use the player to play an audio file.</span></span> <span data-ttu-id="7d207-202">以下是如何使用 `uiMode` 參數的範例：</span><span class="sxs-lookup"><span data-stu-id="7d207-202">Here's an example of how to use the `uiMode` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

<span data-ttu-id="7d207-203">根據預設，當影片播放時，音訊就會開啟。</span><span class="sxs-lookup"><span data-stu-id="7d207-203">By default, audio is on when the video plays.</span></span> <span data-ttu-id="7d207-204">您可以將 `mute` 參數設定為 true，以將音訊靜音：</span><span class="sxs-lookup"><span data-stu-id="7d207-204">You can mute the audio by setting the `mute` parameter to true:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

<span data-ttu-id="7d207-205">您可以藉由將 `volume` 參數設定為介於0到100之間的值，來控制 MediaPlayer 影片的音訊層級。</span><span class="sxs-lookup"><span data-stu-id="7d207-205">You can control the audio level of the MediaPlayer video by setting the `volume` parameter to a value between 0 and 100.</span></span> <span data-ttu-id="7d207-206">預設值為 50。</span><span class="sxs-lookup"><span data-stu-id="7d207-206">The default value is 50.</span></span> <span data-ttu-id="7d207-207">以下為範例：</span><span class="sxs-lookup"><span data-stu-id="7d207-207">Here's an example:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a><span data-ttu-id="7d207-208">播放 Silverlight 影片</span><span class="sxs-lookup"><span data-stu-id="7d207-208">Playing Silverlight Videos</span></span>

<span data-ttu-id="7d207-209">此程式說明如何在名為*Media*的資料夾中播放包含在 Silverlight *.xap*頁面中的影片。</span><span class="sxs-lookup"><span data-stu-id="7d207-209">This procedure shows you how to play video contained in a Silverlight *.xap* page that's in a folder named *Media*.</span></span>

1. <span data-ttu-id="7d207-210">如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果尚未這麼做）。</span><span class="sxs-lookup"><span data-stu-id="7d207-210">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already .</span></span>
2. <span data-ttu-id="7d207-211">建立名為*SilverlightVideo*的新頁面。</span><span class="sxs-lookup"><span data-stu-id="7d207-211">Create a new page named *SilverlightVideo.cshtml*.</span></span>
3. <span data-ttu-id="7d207-212">將下列標記新增至頁面：</span><span class="sxs-lookup"><span data-stu-id="7d207-212">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. <span data-ttu-id="7d207-213">在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="7d207-213">Run the page in a browser.</span></span> 

    <span data-ttu-id="7d207-214">![包](10-working-with-video/_static/image3.jpg "ch08_video-3 .jpg")</span><span class="sxs-lookup"><span data-stu-id="7d207-214">![[image]](10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="7d207-215">其他資源</span><span class="sxs-lookup"><span data-stu-id="7d207-215">Additional Resources</span></span>

<span data-ttu-id="7d207-216">[Silverlight 總覽](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span><span class="sxs-lookup"><span data-stu-id="7d207-216">[Silverlight Overview](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span></span>

[<span data-ttu-id="7d207-217">Flash 物件和內嵌標記屬性</span><span class="sxs-lookup"><span data-stu-id="7d207-217">Flash OBJECT and EMBED tag attributes</span></span>](http://kb2.adobe.com/cps/127/tn_12701.html)

<span data-ttu-id="7d207-218">[Windows 媒體播放機 11 SDK 參數標記](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="7d207-218">[Windows Media Player 11 SDK PARAM Tags](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span></span>
