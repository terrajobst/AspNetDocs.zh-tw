---
uid: web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
title: 在 ASP.NET Web Pages （Razor）網站中快取資料以獲得更佳的效能 |Microsoft Docs
author: Rick-Anderson
description: 您可以藉由讓 it 儲存（也就是快取）來加速您的網站，這通常會花很長的時間來抓取或處理 。
ms.author: riande
ms.date: 02/14/2014
ms.assetid: 961e525b-7700-469e-8a68-d7010b6fb68c
msc.legacyurl: /web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
msc.type: authoredcontent
ms.openlocfilehash: 01796d3ca699a6af5d9162b22a926551435c2040
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641516"
---
# <a name="caching-data-in-an-aspnet-web-pages-razor-site-for-better-performance"></a>在 ASP.NET Web Pages （Razor）網站中快取資料以獲得更好的效能

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明如何使用協助程式快取資訊，以在 ASP.NET Web Pages （Razor）網站中取得更快速的效能。 您可以藉由讓 it 儲存&#8212; ，來加速您的網站， &#8212;快取資料的結果，通常需要很長的時間來抓取或處理，而且不常變更。
> 
> **您將瞭解的內容：** 
> 
> - 如何使用快取來改善網站的回應能力。
> 
> 以下是文章中引進的 ASP.NET 功能：
> 
> - `WebCache` helper。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）3
>   
> 
> 本教學課程也適用于 ASP.NET Web Pages 2。

每次有人向您的網站要求頁面時，網頁伺服器都必須執行一些工作，才能完成要求。 對於某些頁面，伺服器可能必須執行花費（相對）長時間的工作，例如從資料庫中抓取資料。 即使這些工作不會花很長的時間，但如果您的網站遇到大量的流量，則導致 web 伺服器執行複雜或緩慢工作的一系列個別要求，可能會增加許多工作。 這最後可能會影響網站的效能。

在這種情況下，若要改善網站效能，其中一種方法就是快取資料。 如果您的網站取得相同資訊的重複要求，而且不需要針對每個人修改該資訊，而且也不會進行時間區分，而是只會提取資料一次，然後儲存結果。 下一次收到該資訊的要求時，您就可以將它從快取中取出。

一般來說，您會快取不常變更的資訊。 當您將資訊放在快取中時，它會儲存在 web 伺服器的記憶體中。 您可以指定應快取的時間長度，從秒到天。 當快取期間到期時，就會自動從快取中移除資訊。

> [!NOTE]
> 可能會移除快取中的專案，原因是其已過期。 例如，網頁伺服器可能會暫時耗盡記憶體，而它可以回收記憶體的方法之一，就是從快取中擲回專案。 如您所見，即使您已將資訊放入快取中，還是必須檢查以確定它在您需要的時候仍然存在。

假設您的網站有一個頁面，其中顯示目前的溫度和氣象預報。 若要取得這種類型的資訊，您可以將要求傳送至外部服務。 由於這項資訊不會變更（例如在兩小時的期間內），而且因為外部呼叫需要時間和頻寬，所以這是快取的理想候選。

## <a name="adding-caching-to-a-page"></a>將快取新增至頁面

ASP.NET 包含 `WebCache` 協助程式，可讓您輕鬆地將快取新增至您的網站，並將資料新增至快取。 在這個程式中，您將建立快取目前時間的頁面。 這不是真實世界的範例，因為目前的時間是經常變更的專案，而且這一點也不太複雜而無法計算。 不過，這是說明快取實際運作的好方法。

1. 將名為*WebCache*的新頁面新增至網站。
2. 將下列程式碼和標記新增至頁面：

    [!code-cshtml[Main](15-caching-to-improve-the-performance-of-your-website/samples/sample1.cshtml)]

    當您快取資料時，您可以使用名稱，將它放入快取中，這在整個網站中都是唯一的。 在此情況下，您將使用名為 `CachedTime`的快取專案。 這是程式碼範例中所顯示的 `cacheItemKey`。

    程式碼會先讀取 `CachedTime` 快取專案。 如果傳回值（亦即，如果快取專案不是 null），則程式碼只會將時間變數的值設定為快取資料。

    不過，如果快取專案不存在（亦即，它是 null），則程式碼會設定時間值、將它新增至快取，並將到期值設定為一分鐘。 一分鐘後，就會捨棄快取專案。 （快取中專案的預設到期值為20分鐘）。命令 `WebCache.Set(cacheItemKey, time, 1, false)` 顯示如何將目前時間值新增至快取，並將其到期日設定為1分鐘。 將*slidingExpiration*參數設定為 `false` 表示每次要求時，不會更新到期時間。 它在最初新增至快取之後，將會剛好在1分鐘後到期。 如果您將此值設定為 `true` 則每次從快取要求值時，就會重設1分鐘的到期時間。

    此程式碼說明當您快取資料時，應該一律使用的模式。 在您取得快取的內容之前，請一律先檢查 `WebCache.Get` 方法是否傳回 null。 請記住，快取專案可能已過期，或因為某些其他原因已移除，因此任何指定的專案永遠都不保證會在快取中。
3. 在瀏覽器中執行*WebCache。* （在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）第一次要求頁面時，時間資料不在快取中，而且程式碼必須將時間值新增至快取。

    ![cache-1](15-caching-to-improve-the-performance-of-your-website/_static/image1.jpg)
4. 在瀏覽器中重新整理*WebCache。* 這次，時間資料會在快取中。 請注意，自從上次查看頁面之後，時間尚未變更。

    ![cache-2](15-caching-to-improve-the-performance-of-your-website/_static/image2.jpg)
5. 等候一分鐘，讓快取清空，然後重新整理頁面。 此頁面會再次指出快取中找不到時間資料，而且更新的時間會新增至快取。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他資源

- [以圖表顯示資料](https://go.microsoft.com/fwlink/?LinkId=202895)
- [WEBCACHE API 參考](https://msdn.microsoft.com/library/system.web.helpers.webcache(v=vs.99).aspx)（MSDN）
