---
uid: web-pages/overview/performance-and-traffic/14-analyzing-traffic
title: 追蹤 ASP.NET Web Pages （Razor）網站的訪客資訊（分析） |Microsoft Docs
author: Rick-Anderson
description: 當您的網站繼續進行之後，您可能會想要分析網站流量。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 360bc6e1-84c5-4b8e-a84c-ea48ab807aa4
msc.legacyurl: /web-pages/overview/performance-and-traffic/14-analyzing-traffic
msc.type: authoredcontent
ms.openlocfilehash: 095a5572c755446e0661c052ca9de82d636429fd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525183"
---
# <a name="tracking-visitor-information-analytics-for-an-aspnet-web-pages-razor-site"></a>追蹤 ASP.NET Web Pages （Razor）網站的訪客資訊（分析）

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明如何使用 helper 將網站分析新增至 ASP.NET Web Pages （Razor）網站中的頁面。
> 
> 您將學到什麼：
> 
> - 如何將網站流量的相關資訊傳送至分析提供者。
> 
> 以下是文章中引進的 ASP.NET 程式設計功能：
> 
> - `Analytics` helper。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）2
> - ASP.NET Web helper 程式庫（NuGet 套件）

分析是技術的一般詞彙，可測量您網站上的流量，讓您可以瞭解使用者使用網站的方式。 有許多分析服務可供使用，包括 Google、Yahoo、StatCounter 和其他服務。

分析的運作方式是註冊具有分析提供者的帳戶，您可以在其中登錄您要追蹤的網站。提供者會傳送 JavaScript 程式碼程式碼片段給您，其中包含您帳戶的識別碼或追蹤程式碼。 您會將 JavaScript 程式碼片段新增至您要追蹤之網站上的網頁。（您通常會將分析程式碼片段新增至頁尾或版面配置頁，或在網站中的每個頁面上顯示的其他 HTML 標籤）。當使用者要求包含其中一個 JavaScript 程式碼片段的頁面時，程式碼片段會將目前頁面的相關資訊傳送給分析提供者，以記錄有關頁面的各種詳細資料。

當您想要查看您的網站統計資料時，請登入分析提供者的網站。 接著，您可以查看網站的各種報告，例如：

- 個別頁面的頁面流覽次數。 這會告訴您（大約）有多少人造訪網站，以及您的網站上最受歡迎的網頁。
- 人們花在特定頁面上的時間。 這可能會告訴您，您的首頁是否會讓人感到滿意。
- 使用者造訪您的網站之前的網站。 這可協助您瞭解流量是否來自連結、搜尋等。
- 當人們造訪您的網站時，以及它們的持續時間。
- 您的訪客所來自的國家/地區。
- 您的訪客所使用的瀏覽器和作業系統。

    ![Ch14traffic-1](14-analyzing-traffic/_static/image1.jpg)

## <a name="using-a-helper-to-add-analytics-to-a-page"></a>使用 Helper 將分析新增至頁面

ASP.NET Web Pages 包含數個分析協助程式（`Analytics.GetGoogleHtml`、`Analytics.GetYahooHtml`和 `Analytics.GetStatCounterHtml`），可讓您輕鬆地管理用於分析的 JavaScript 程式碼片段。 您只需要將 helper 新增至頁面，而不是找出 JavaScript 程式碼的儲存方式和位置。 您需要提供的唯一資訊是您的帳戶名稱、識別碼或追蹤程式碼。 （對於 StatCounter，您也必須提供一些額外的值）。

在這個程式中，您將建立使用 `GetGoogleHtml` helper 的版面配置頁。 如果您已經有一個具有其他其中一個分析提供者的帳戶，您可以改為使用該帳戶，並視需要進行些許調整。

> [!NOTE]
> 當您建立分析帳戶時，您會註冊您想要追蹤之網站的 URL。 如果您要測試本機電腦上的所有專案，則不會追蹤實際的流量（唯一的流量是您），因此您將無法記錄及查看網站統計資料。 但此程式會顯示如何將分析協助程式新增至頁面。 當您發佈網站時，即時網站會將資訊傳送給您的分析提供者。

1. 如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果尚未新增）。
2. 使用 Google Analytics 建立帳戶並記錄帳戶名稱。
3. 建立名為 [*分析*] 的版面配置頁，並新增下列標記：

    [!code-cshtml[Main](14-analyzing-traffic/samples/sample1.cshtml)]

    > [!NOTE]
    > 您必須將呼叫放在網頁主體（在 `</body>` 標記之前）中的 `Analytics` helper。 否則，瀏覽器將不會執行腳本。

    如果您使用不同的分析提供者，請改為使用下列其中一個協助程式：

    - （Yahoo） `@Analytics.GetYahooHtml("myaccount")`
    - （StatCounter） `@Analytics.GetStatCounterHtml("project", "security")`
4. 以您在步驟1中建立的帳戶、識別碼或追蹤程式碼的名稱取代 `myaccount`。
5. 在瀏覽器中執行頁面。 （在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）
6. 在瀏覽器中，查看頁面來源。 您將能夠看到轉譯的分析程式碼：

    [!code-html[Main](14-analyzing-traffic/samples/sample2.html)]
7. 登入 Google Analytics 網站，並檢查您網站的統計資料。 如果您是在即時網站上執行頁面，您會看到一個專案，將造訪記錄到您的頁面。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他資源

- [Google Analytics 網站](https://www.google.com/analytics/)
- [Yahoo！ Web Analytics 網站](http://help.yahoo.com/l/us/yahoo/ywa/)
- [StatCounter 網站](http://statcounter.com/)
