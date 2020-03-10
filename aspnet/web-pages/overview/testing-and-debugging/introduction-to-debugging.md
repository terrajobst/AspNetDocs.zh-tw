---
uid: web-pages/overview/testing-and-debugging/introduction-to-debugging
title: 調試 ASP.NET Web Pages （Razor）網站簡介 |Microsoft Docs
author: Rick-Anderson
description: 「偵錯工具」是在您的字碼頁中尋找和修正錯誤的過程。 本章將說明一些您可以用來進行 debug 和分析的工具和技巧 。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 68de4326-7611-4b9b-b5f6-79b7adc3069f
msc.legacyurl: /web-pages/overview/testing-and-debugging/introduction-to-debugging
msc.type: authoredcontent
ms.openlocfilehash: ae7d871e56326610c043dc20fe6e0919e1b4ac89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624366"
---
# <a name="introduction-to-debugging-aspnet-web-pages-razor-sites"></a>調試 ASP.NET Web Pages （Razor）網站簡介

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明在 ASP.NET Web Pages （Razor）網站中，用來進行頁面偵錯工具的各種方式。 「偵錯工具」是在您的字碼頁中尋找和修正錯誤的過程。
>
> **您將瞭解的內容：**
>
> - 如何顯示有助於分析和偵錯工具頁面的資訊。
> - 如何在 Visual Studio 中使用調試工具。
>
>
> 以下是文章中引進的 ASP.NET 功能：
>
> - `ServerInfo` helper。
> - `ObjectInfo` helper。
>
>
> ## <a name="software-versions"></a>軟體版本
>
>
> - ASP.NET Web Pages （Razor）3
> - Visual Studio 2013
>
>
> 本教學課程也適用于 ASP.NET Web Pages 2。 您可以使用 WebMatrix 3，但不支援整合式偵錯工具。

在您的程式碼中疑難排解錯誤和問題的重要層面，就是在一開始就予以避免。 若要這麼做，您可以將可能導致錯誤的程式碼區段放入 `try/catch` 區塊中。 如需詳細資訊，請參閱[使用 Razor 語法進行 ASP.NET Web 程式設計簡介](https://go.microsoft.com/fwlink/?LinkId=202890)中的處理錯誤一節。

`ServerInfo` 協助程式是一種診斷工具，可讓您大致瞭解裝載網頁的 web 伺服器環境的相關資訊。 它也會顯示當瀏覽器要求頁面時所傳送的 HTTP 要求資訊。 [`ServerInfo` helper] 會顯示目前的使用者身分識別、提出要求的瀏覽器類型等等。 這類資訊可協助您針對常見的問題進行疑難排解。

1. 建立名為*ServerInfo*的新網頁。
2. 在頁面結尾處，在結束 `</body>` 標記之前，新增 `@ServerInfo.GetHtml()`：

    [!code-cshtml[Main](introduction-to-debugging/samples/sample1.cshtml)]

    您可以在頁面中的任何位置加入 `ServerInfo` 程式碼。 但在結尾新增它，會將其輸出與其他頁面內容分開，讓您更容易閱讀。

    > [!NOTE]
    >
    > **重要事項**將網頁移至實際伺服器之前，您應該先從網頁移除任何診斷程式代碼。 這適用于 `ServerInfo` 協助程式，以及本文中牽涉到將程式碼加入至頁面的其他診斷技術。 您不想讓網站訪客查看伺服器名稱、使用者名稱、伺服器上的路徑，以及類似的詳細資料等資訊，因為這類資訊可能適用于具有惡意意圖的人。
3. 儲存頁面，並在瀏覽器中執行。

    ![調試-1](introduction-to-debugging/_static/image1.jpg)

    `ServerInfo` helper 會在頁面中顯示四個資訊資料表：

   - 伺服器設定。 本節提供主控網頁伺服器的相關資訊，包括電腦名稱稱、您正在執行的 ASP.NET 版本、功能變數名稱和伺服器時間。
   - ASP.NET 伺服器變數。 本節提供許多 HTTP 通訊協定詳細資料（稱為 HTTP 變數）的詳細資料，以及每個網頁要求中的值。
   - HTTP 執行時間資訊。 本節提供有關您的網頁執行所在的 Microsoft .NET Framework 版本、路徑、有關快取的詳細資料等等的詳細資料。 （如您在[使用 Razor 語法 ASP.NET Web 程式設計簡介](https://go.microsoft.com/fwlink/?LinkId=202890)中所學到的內容，使用 Razor 語法的 ASP.NET Web Pages 是以 Microsoft 的 ASP.NET Web 服務器技術為基礎，其本身是建置於廣泛的軟體發展程式庫，稱為 .NET Framework）。
   - 環境變數。 本節提供在 web 伺服器上的所有本機環境變數及其值的清單。

     所有伺服器和要求資訊的完整說明已超出本文的範圍，但您可以看到 `ServerInfo` helper 會傳回許多診斷資訊。 如需 `ServerInfo` 所傳回之值的詳細資訊，請參閱 MSDN 網站上 Microsoft TechNet 網站上的已辨識的[環境變數](https://technet.microsoft.com/library/dd560744(WS.10).aspx)和[IIS 伺服器變數](https://msdn.microsoft.com/library/ms524602(VS.90).aspx)。

## <a name="embedding-output-expressions-to-display-page-values"></a>內嵌輸出運算式以顯示頁面值

另一個查看程式碼發生狀況的方法，就是將輸出運算式內嵌在頁面中。 如您所知，您可以藉由將 `@myVariable` 或 `@(subTotal * 12)` 之類的內容加入頁面中，直接輸出變數的值。 若要進行偵錯工具，您可以將這些輸出運算式放在程式碼的策略性點上。 這可讓您查看索引鍵變數的值，或頁面執行時的計算結果。 當您完成偵錯工具時，可以移除運算式或將它們批註起來。此程式說明使用內嵌運算式來協助 debug 頁面的一般方式。

1. 建立名為*OutputExpression*的新 WebMatrix 頁面。
2. 將頁面內容取代為下列內容：

    [!code-html[Main](introduction-to-debugging/samples/sample2.html)]

    此範例會使用 `switch` 語句來檢查 `weekday` 變數的值，然後根據該星期的哪一天顯示不同的輸出訊息。 在此範例中，第一個程式碼區塊內的 `if` 區塊會將一天新增至目前的工作日值，任意變更一周中的那一天。 這是為了說明而引進的錯誤。
3. 儲存頁面，並在瀏覽器中執行。

    此頁面會顯示一周中錯誤日的訊息。 在一周當中的哪一天，您會在一天后看到訊息。 雖然在此情況下，您知道訊息為何關閉（因為程式碼刻意設定了不正確的日期值），但事實上，通常很難知道程式碼中發生錯誤的位置。 若要進行 debug，您必須找出索引鍵物件和變數的值（例如 `weekday`）發生了什麼事。
4. 藉由插入 `@weekday` （如程式碼中的批註所指示的兩個位置所示）來新增輸出運算式。 這些輸出運算式會在程式碼執行中顯示該時間點的變數值。

    [!code-csharp[Main](introduction-to-debugging/samples/sample3.cs?highlight=2-3,15-16)]
5. 在瀏覽器中儲存並執行頁面。

    此頁面會先顯示一周中的一天，再加上一天的更新日期，然後從 `switch` 語句產生的訊息。 這兩個變數運算式（`@weekday`）的輸出在天數之間沒有空格，因為您未將任何 HTML `<p>` 標記加入至輸出;運算式僅供測試之用。

    ![調試-2](introduction-to-debugging/_static/image2.jpg)

    現在您可以看到錯誤所在的位置。 當您第一次在程式碼中顯示 `weekday` 變數時，它會顯示正確的日期。 當您第二次顯示時，在程式碼中 `if` 區塊之後，一天就會關閉。 所以您知道 weekday 變數的第一個和第二個外觀之間發生了什麼事。 如果這是真正的錯誤，這種方法可協助您縮小造成問題之程式碼的位置。
6. 藉由移除您新增的兩個輸出運算式，並移除變更星期幾的程式碼，修正頁面中的程式碼。 其餘的完整程式碼區塊如下列範例所示：

    [!code-cshtml[Main](introduction-to-debugging/samples/sample4.cshtml)]
7. 在瀏覽器中執行頁面。 此時，您會看到針對一周中的實際日期顯示正確的訊息。

## <a name="using-the-objectinfo-helper-to-display-object-values"></a>使用 ObjectInfo Helper 顯示物件值

`ObjectInfo` helper 會顯示您傳遞給它的每個物件的類型和值。 您可以使用它來查看程式碼中變數和物件的值（如同您在上一個範例中使用的輸出運算式），而且您可以查看物件的資料類型資訊。

1. 開啟您稍早建立的名為*OutputExpression*的檔案。
2. 將頁面中的所有程式碼取代為下列程式碼區塊：

    [!code-html[Main](introduction-to-debugging/samples/sample5.html)]
3. 在瀏覽器中儲存並執行頁面。

    ![調試-4](introduction-to-debugging/_static/image3.jpg)

    在此範例中，`ObjectInfo` helper 會顯示兩個專案：

   - 類型。 針對第一個變數，類型為 `DayOfWeek`。 針對第二個變數，類型為 `String`。
   - 值。 在此情況下，因為您已經在頁面中顯示問候語變數的值，所以當您將變數傳遞給 `ObjectInfo`時，值會再次顯示。

     對於更複雜的物件，`ObjectInfo` helper 可以顯示更多&#8212;的資訊，基本上，它可以顯示物件所有屬性的類型和值。

## <a name="using-debugging-tools-in-visual-studio"></a>在 Visual Studio 中使用調試工具

如需更完整的偵錯工具體驗，請使用[Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。 有了 Visual Studio，您就可以在程式碼中，于想要檢查的那一行設定中斷點。

![設定中斷點](introduction-to-debugging/_static/image1.png)

當您測試網站時，執行中的程式碼會在中斷點暫停。

![到達中斷點](introduction-to-debugging/_static/image2.png)

您可以檢查變數目前的值，並逐行執行程式碼。

![查看值](introduction-to-debugging/_static/image3.png)

如需在 Visual Studio 中使用整合式偵錯工具來 debug ASP.NET Razor 頁面的詳細資訊，請參閱[使用 Visual Studio 的程式設計 ASP.NET Web Pages （Razor）](https://go.microsoft.com/fwlink/?LinkId=205854)。

## <a name="additional-resources"></a>其他資源

- [使用 Visual Studio 的程式設計 ASP.NET Web Pages （Razor）](https://go.microsoft.com/fwlink/?LinkId=205854)
- [IIS 伺服器變數](https://msdn.microsoft.com/library/ms524602(VS.90).aspx)（MSDN）
- 辨識的[環境變數](https://technet.microsoft.com/library/dd560744(WS.10).aspx)（TechNet）
