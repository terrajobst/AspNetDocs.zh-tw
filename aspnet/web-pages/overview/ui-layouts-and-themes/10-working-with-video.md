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
# <a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a>在 ASP.NET Web Pages （Razor）網站中顯示影片

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明如何使用 ASP.NET Web Pages （Razor）網站中的影片（媒體）播放機，讓使用者能夠觀看儲存在網站上的影片。 Razor 語法的 ASP.NET Web Pages 可讓您播放 Flash （*swf*）、媒體播放機（ *.Wmv*）和 Silverlight （ *.xap*）影片。
> 
> 您將學到什麼：
> 
> - 如何選擇影片播放機。
> - 如何將影片新增至網頁。
> - 如何設定影片播放者屬性。
> 
> 以下是文章中引進的 ASP.NET Razor pages 功能：
> 
> - `Video` helper。
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

## <a name="introduction"></a>簡介

您可能想要在您的網站上顯示影片。 其中一種方法是連結至已經有影片的網站，例如 YouTube。 如果您想要直接在自己的頁面中內嵌這些網站的影片，通常可以從網站取得 HTML 標籤，然後將它複製到您的頁面。 例如，下列範例顯示如何內嵌 YouTube 影片：

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

如果您想要播放自己網站上的影片（而不是在公用的影片分享網站），您無法使用像這樣的內嵌標記直接連結到它。 不過，您可以使用 [`Video` 協助程式] 從網站播放影片，這會直接在頁面中轉譯媒體播放機。

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a>選擇影片播放機

影片檔案有許多格式，而且每種格式通常需要不同的播放程式和不同的方式來設定玩家。 在 ASP.NET Razor pages 中，您可以使用 `Video` 協助程式在網頁中播放影片。 `Video` helper 會簡化在網頁中內嵌影片的程式，因為它會自動產生 `object` 和 `embed` 的 HTML 專案，通常用來將影片新增至頁面。

`Video` helper 支援下列媒體播放機：

- Adobe Flash
- Windows MediaPlayer
- Microsoft Silverlight

### <a name="the-flash-player"></a>Flash Player

`Video` 協助程式的 `Flash` 播放程式，可讓您在網頁中播放 Flash 影片（*swf*檔案）。 您至少必須提供影片檔案的路徑。 如果您沒有指定路徑，則播放程式會使用目前版本的 Flash 所設定的預設值。 典型的預設設定為：

- 影片會使用其預設的寬度和高度，而不含背景色彩來顯示。
- 影片會在頁面載入時自動播放。
- 影片會持續迴圈，直到明確停止為止。
- 影片會縮放以顯示所有影片，而不是裁剪影片以符合特定大小。
- 影片會在視窗中播放。

### <a name="the-mediaplayer-player"></a>MediaPlayer Player

`Video` 協助程式的 [`MediaPlayer` 播放程式] 可讓您在網頁中播放 Windows Media 影片（ *.wmv*檔案）、windows media audio （ *.wma*檔案）和 mp3 （*mp3*檔案）。 您必須包含要播放之媒體檔案的路徑;所有其他參數都是選擇性的。 如果您只指定路徑，播放程式會使用目前版本的 MediaPlayer 所設定的預設設定，例如：

- 影片會使用其預設的寬度和高度來顯示。
- 影片會在頁面載入時自動播放。
- 影片會播放一次（它不會迴圈）。
- Media player 會在使用者介面中顯示一組完整的控制項。
- 影片會在視窗中播放。

### <a name="the-silverlight-player"></a>Silverlight Player

`Video` 協助程式的 `Silverlight` 播放程式可讓您播放 Windows Media 視訊（ *.wmv*檔案）、Windows Media 音訊（ *.wma*檔案）和 mp3 （*mp3*檔案）。 您必須設定 path 參數，以指向 Silverlight 應用程式封裝（ *.xap*檔案）。 您也必須設定 width 和 height 參數。 所有其他參數皆為選擇性使用。 當您使用 Silverlight player for video 時，如果您只設定必要的參數，Silverlight 播放程式會顯示沒有背景色彩的影片。

> [!NOTE]
> 如果您還不知道 Silverlight： *.xap*檔案是一個壓縮檔案，其中包含 *.xaml*檔案中的版面配置指示、元件中的 managed 程式碼，以及選擇性的資源。 您可以在 Visual Studio 中建立 *.xap*檔案作為 Silverlight 應用程式專案。

`Silverlight` 影片播放程式會使用您為播放程式提供的設定，以及 *.xap*檔案中提供的設定。

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a>MIME 類型
> 
> 當瀏覽器下載檔案時，瀏覽器會確定檔案類型符合所要轉譯之檔所指定的 MIME 類型。 MIME 類型是檔案的內容類型或媒體類型。 `Video` helper 會使用下列 MIME 類型：
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`

<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a>播放 Flash （swf）影片

此程式說明如何播放名為*sample*的 Flash 影片。 此程式假設您的網站上已有名為*Media*的資料夾，且該資料夾中的 swf 檔案為 *。*

1. 如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果尚未新增）。
2. 在網站中，新增頁面，並將它命名為*FlashVideo*。
3. 將下列標記新增至頁面： 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. 在瀏覽器中執行頁面。 （在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）頁面隨即顯示，且影片會自動播放。 

    ![包](10-working-with-video/_static/image1.jpg "ch08_video-1 .jpg")

您可以將 Flash 影片的 `quality` 參數設定為 `low`、`autolow`、`autohigh`、`medium`、`high`和 `best`：

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

您可以使用 `scale` 參數，將 Flash 影片變更為以特定大小播放，您可以將其設定為下列內容：

- `showall` 這會讓整個影片可見，同時維持原始外觀比例。 不過，您最後可能會在每一端加上框線。
- `noorder` 這會調整影片，同時維持原始外觀比例，但可能會進行裁剪。
- `exactfit` 如此一來，整個影片就會顯示出來，而不會保留原始的外觀比例，但可能會發生失真。

如果您未指定 `scale` 參數，則會顯示整段影片，且不會進行任何裁剪而維持原始外觀比例。 下列範例顯示如何使用 `scale` 參數：

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

Flash player 支援名為 `windowMode`的影片模式設定。 您可以將此設定為 [`window`]、[`opaque`] 和 [`transparent`]。 根據預設，`windowMode` 設定為 [`window`]，這會在網頁的另一個視窗中顯示影片。 [`opaque`] 設定會隱藏網頁上影片背後的所有內容。 [`transparent`] 設定可讓網頁的背景顯示在影片中，假設影片的任何部分都是透明的。

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a>播放 MediaPlayer （*wmv*）影片

下列程式說明如何播放名為*sample*的 Window media 影片，其位於*Media*資料夾中。

1. 如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果尚未這麼做）。
2. 建立名為*MediaPlayerVideo*的新頁面。
3. 將下列標記新增至頁面： 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. 在瀏覽器中執行頁面。 影片會自動載入並播放。 

    ![包](10-working-with-video/_static/image2.jpg "ch08_video-2 .jpg")

您可以將 `playCount` 設定為整數，以指出自動播放影片的次數：

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

`uiMode` 參數可讓您指定要在使用者介面中顯示的控制項。 您可以將 `uiMode` 設定為 [`invisible`]、[`none`]、[`mini`] 或 [`full`]。 如果您未指定 `uiMode` 參數，除了影片視窗之外，影片也會顯示 [狀態] 視窗、[搜尋列]、[控制項] 按鈕和 [音量] 控制項。 如果您使用播放程式播放音訊檔案，也會顯示這些控制項。 以下是如何使用 `uiMode` 參數的範例：

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

根據預設，當影片播放時，音訊就會開啟。 您可以將 `mute` 參數設定為 true，以將音訊靜音：

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

您可以藉由將 `volume` 參數設定為介於0到100之間的值，來控制 MediaPlayer 影片的音訊層級。 預設值為 50。 以下為範例：

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a>播放 Silverlight 影片

此程式說明如何在名為*Media*的資料夾中播放包含在 Silverlight *.xap*頁面中的影片。

1. 如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果尚未這麼做）。
2. 建立名為*SilverlightVideo*的新頁面。
3. 將下列標記新增至頁面： 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. 在瀏覽器中執行頁面。 

    ![包](10-working-with-video/_static/image3.jpg "ch08_video-3 .jpg")

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他資源

[Silverlight 總覽](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)

[Flash 物件和內嵌標記屬性](http://kb2.adobe.com/cps/127/tn_12701.html)

[Windows 媒體播放機 11 SDK 參數標記](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)
