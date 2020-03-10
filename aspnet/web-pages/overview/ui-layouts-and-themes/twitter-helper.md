---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: Twitter Helper 與 ASP.NET Web Pages |Microsoft Docs
author: Rick-Anderson
description: 本主題和應用程式會示範如何將 Twitter Helper 新增至您的 WebMatrix 3 專案。 其中包含 Twitter Helper 程式碼，並示範如何呼叫 Helper 。
ms.author: riande
ms.date: 11/26/2018
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 76e32b7c808467a9a87c70017dac02bdb895e1df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638555"
---
# <a name="twitter-helper-with-aspnet-web-pages"></a>Twitter 協助程式與 ASP.NET Web Pages

由[Tom FitzMacken](https://github.com/tfitzmac)

> [!IMPORTANT]
> Twitter 協助程式已過時。 如需 Twitter 最新的適用于網站的 engagement 工具，請參閱[twitter 的網站總覽](https://developer.twitter.com/en/docs/twitter-for-websites/overview)。

> 本主題和應用程式會示範如何將 Twitter Helper 新增至您的 WebMatrix 3 專案。 其中包含 Twitter Helper 程式碼，並示範如何呼叫 Helper 方法。
> 
> 此 Twitter 檔案的程式碼是由 Microsoft 的**Tian Pan**所開發。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）3
>   
> 
> 本教學課程也適用于 ASP.NET Web Pages 2。

## <a name="introduction"></a>簡介

本主題示範如何將 Twitter Helper 新增至您的應用程式，並使用 Razor 語法來呼叫 Helper 方法。 Twitter Helper 可讓您輕鬆地在應用程式中併入 Twitter 按鈕和小工具。 若要使用 Twitter widget （例如使用者的時間軸）或主題標籤的搜尋結果，您必須先[在 Twitter 上建立 widget](https://twitter.com/settings/widgets)。 建立小工具之後，您會收到 widget 識別碼。呼叫顯示 widget 的 helper 方法時，您會傳遞這個 widget id 做為參數。

本主題是針對 Twitter API 1.1 版所撰寫。 藉由直接將 Twitter Helper 程式碼新增至您的專案，您可以在 Twitter API 變更時更新 Helper 程式碼。

如需有關安裝 WebMatrix 的詳細資訊，請參閱[ASP.NET Web Pages 2 消費者入門簡介](../getting-started/introducing-aspnet-web-pages-2/getting-started.md)。

## <a name="add-twitter-helper-to-your-project"></a>將 Twitter Helper 新增至您的專案

若要新增 Twitter 協助程式，請先在您的專案中新增名為**App\_** 的資料夾。 然後，建立名為**Twitter. cshtml**的檔案。

![App_Code 資料夾](twitter-helper/_static/image1.png)

將 Twitter 中的預設程式碼取代為下列程式碼。

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a>從您的網頁呼叫 Twitter 方法

下列範例顯示如何從專案中的頁面使用 Twitter Helper 方法。 在您的專案中，您會想要將參數值取代為與您的需求相關的值。 您可以使用提供的 widget id 來探索方法的使用方式，但您會想要為您的專案產生您自己的小工具。

不需要以下顯示的所有參數。 選擇性參數是用來自訂按鈕或 widget 的顯示方式。 例如，[下一項] 按鈕只需要遵循使用者名稱，但此範例會顯示如何包含關注者的數目，以及如何指定按鈕的大小和語言。

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a>查看結果

上述程式碼會產生下列按鈕和小工具。 這些按鈕和小工具都是功能完整的，而不是螢幕擷取畫面。 [跟隨] 按鈕會以西班牙文顯示，因為 language 參數是設定為**es**。

### <a name="follow-button"></a>追蹤按鈕

[遵循 @aspnet）](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`

### <a name="tweet-button"></a>推文按鈕

[推文](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`

### <a name="user-timeline-profile"></a>使用者時間軸（設定檔）

[@aspnet`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>` 推文](https://twitter.com/aspnet)

### <a name="favorites"></a>我的最愛

[@Microsoft`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>` 的我的最愛推文](https://twitter.com/Microsoft/favorites)

### <a name="list"></a>清單

[從 @Microsoft/MS\_取用者\_的頻帶推文](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="search"></a>搜尋

[&quot;#asp .net&quot;的相關推文](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`
