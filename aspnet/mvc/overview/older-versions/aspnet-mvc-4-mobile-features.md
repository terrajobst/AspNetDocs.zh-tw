---
uid: mvc/overview/older-versions/aspnet-mvc-4-mobile-features
title: ASP.NET MVC 4 行動功能 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程現在有一個 MVC 5 版本，其中包含在 Azure 網站上部署 ASP.NET MVC 5 行動 Web 應用程式中的程式碼範例。
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 27dc4fc8-1b51-43b0-933f-fc1b52476523
msc.legacyurl: /mvc/overview/older-versions/aspnet-mvc-4-mobile-features
msc.type: authoredcontent
ms.openlocfilehash: 9716def069ca9f7115af32e16381f41bd4d13342
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457644"
---
# <a name="aspnet-mvc-4-mobile-features"></a>ASP.NET MVC 4 行動功能

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教學課程現在有一個 MVC 5 版本，其中包含在[Azure 網站上部署 ASP.NET MVC 5 行動 Web 應用程式中](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/)的程式碼範例。

本教學課程將告訴您如何在 ASP.NET MVC 4 Web 應用程式中使用行動功能的基本概念。 在本教學課程中，您可以使用[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)或 Visual web Developer 2010 Express Service Pack 1 （&quot;Visual web DEVELOPER 或 VWD&quot;）。 如果您已經有，可以使用 professional 版本的 Visual Studio。

開始之前，請先確定您已安裝下列必要條件。

- [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) （建議）或 Visual Studio Web DEVELOPER Express SP1。 Visual Studio 2012 包含 ASP.NET MVC 4。 如果您使用的是 Visual Web Developer 2010，就必須安裝[ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)。

您還需要一個行動瀏覽器模擬器。 下列任一項目都可使用：

- [Windows 7 Phone 模擬器](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)。 （這是在本教學課程中大部分螢幕擷取畫面中使用的模擬器）。
- 變更使用者代理程式字串以模擬 iPhone。 請參閱[此](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)blog 專案。
- [Opera Mobile 模擬器](http://www.opera.com/developer/tools/mobile/)
- 將使用者代理程式設定為 iPhone 的[Apple Safari](http://www.apple.com/safari/download/) 。 如需有關如何將 Safari 中的使用者代理程式設定為「iPhone」的指示，請參閱[如何讓 safari](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html)在 David Alison 的 blog 上偽裝為 IE。

此處提供具有 C\# 原始程式碼的 Visual Studio 專案來幫助您完成本主題：

- [入門專案下載](https://go.microsoft.com/fwlink/?linkid=228307&amp;clcid=0x409)
- [已完成專案下載](https://go.microsoft.com/fwlink/?linkid=228306&amp;clcid=0x409)

### <a name="what-youll-build"></a>您要建置的內容

在本教學課程中，您會將行動功能新增至[起始專案](https://go.microsoft.com/fwlink/?LinkId=228307)中提供的簡單會議清單應用程式。 下列螢幕擷取畫面顯示已完成應用程式的 [標記] 頁面，如[Windows 7 Phone 模擬器](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)中所示。 請參閱[Windows Phone 模擬器的鍵盤對應](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx)，以簡化鍵盤輸入。

[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)

您可以藉由設定[使用者代理字串](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)，來使用 Internet Explorer 9 或10、FireFox 或 Chrome 來開發您的行動應用程式。 下圖顯示使用 Internet Explorer 模擬 iPhone 的已完成教學課程。 您可以使用 Internet Explorer F-12 開發人員工具和[Fiddler 工具](http://www.fiddler2.com/fiddler2/)，協助您進行應用程式的偵錯工具。

![](aspnet-mvc-4-mobile-features/_static/image3.png)

### <a name="skills-youll-learn"></a>您要學習的技術

以下是您要學習的內容：

- ASP.NET MVC 4 範本如何使用 HTML5 `viewport` 屬性和適應性轉譯來改善行動裝置上的顯示。
- 如何建立行動裝置特定的視圖。
- 如何建立可讓使用者在行動視圖和應用程式桌面視圖之間切換的視圖切換器。

### <a name="getting-started"></a>開始使用

使用下列連結下載入門專案的會議清單應用程式：[下載](https://go.microsoft.com/fwlink/?LinkId=228307)。 然後在 Windows Explorer 中，以滑鼠右鍵按一下 [ *MvcMobile* ] 檔案，然後選擇 [**屬性**]。 在 [ **MvcMobile 屬性**] 對話方塊中，選擇 [**解除封鎖**] 按鈕。 (取消封鎖後，當您嘗試使用從網路下載的 .zip 檔案時，就不會出現安全性警告。)

![p1_unBlock](aspnet-mvc-4-mobile-features/_static/image4.png)

以滑鼠右鍵按一下 [ *MvcMobile* ] 檔案，然後選取 [**解壓縮全部**] 以解壓縮檔案。 在 Visual Studio 中，開啟 [ *MvcMobile* ] 檔案。

按 CTRL + F5 執行應用程式，這會在您的桌面瀏覽器中顯示它。 啟動行動瀏覽器模擬器，將會議應用程式的 URL 複製到模擬器中，然後按一下 [**依標記流覽]** 連結。 如果您使用 Windows Phone 模擬器，請按一下 URL 列，然後按下 [暫停] 鍵以取得鍵盤存取。 下圖顯示 [ *AllTags* ] 視圖（從選擇 **[依標記流覽]** ）。

[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)

該顯示內容在行動裝置上非常清楚易讀。 選擇 [ASP.NET] 連結。

[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)

ASP.NET 標記視圖非常雜亂。 例如，[**日期] 資料**行非常難以閱讀。 稍後在本教學課程中，您將會建立專為行動瀏覽器提供的*AllTags* view 版本，並讓顯示可讀取。

注意：行動快取引擎目前有一個 bug。 對於生產應用程式，您必須安裝[Fixed DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) nugget 套件。 如需修正的詳細資訊，請參閱 < [ASP.NET MVC 4](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)行動快取錯誤修正。

## <a name="css-media-queries"></a>CSS 媒體查詢

[Css 媒體查詢](http://www.w3.org/TR/css3-mediaqueries/)是適用于媒體類型的 css 延伸模組。 它們可讓您建立規則，以覆寫特定瀏覽器（使用者代理程式）的預設 CSS 規則。 以行動瀏覽器為目標的 CSS 通用規則會定義最大螢幕大小。 當您建立新的 ASP.NET MVC 4 網際網路專案時所建立的*Content\Site.css*檔案包含下列媒體查詢：

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample1.css)]

如果瀏覽器視窗寬或小於850圖元，則會使用此媒體區塊內的 CSS 規則。 您可以使用像這樣的 CSS 媒體查詢，在小型瀏覽器（如行動瀏覽器）上提供更好的 HTML 內容顯示，而不是針對更廣泛的桌面瀏覽器顯示所設計的預設 CSS 規則。

## <a name="the-viewport-meta-tag"></a>視口中繼標記

大部分的行動瀏覽器定義的虛擬瀏覽器視窗寬度（*視口*）遠大於行動裝置的實際寬度。 這可讓行動瀏覽器符合虛擬顯示器內的整個網頁。 然後，使用者可以放大感興趣的內容。 不過，如果您將 [視口寬度] 設定為 [實際裝置寬度]，則不需要縮放，因為內容適合在行動瀏覽器中。

ASP.NET MVC 4 配置檔案中的 [視口] `<meta>` 標記會將此視口設定為裝置寬度。 下一行顯示 ASP.NET MVC 4 版面配置檔案中的 [視口] `<meta>` 標記。

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample2.html)]

## <a name="examining-the-effect-of-css-media-queries-and-the-viewport-meta-tag"></a>檢查 CSS 媒體查詢和視口中繼標記的效果

在編輯器中開啟*Views\Shared\\_Layout. cshtml*檔案，並將 [視口] `<meta>` 標記批註。 下列標記會顯示已加上批註的行。

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample3.cshtml)]

在編輯器中開啟*MvcMobile\Content\Site.css*檔案，並將媒體查詢中的最大寬度變更為零圖元。 這會讓 CSS 規則無法在行動瀏覽器中使用。 下一行顯示已修改的媒體查詢：

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample4.css)]

儲存您的變更，並在行動瀏覽器模擬器中流覽至會議應用程式。 下圖中的小型文字是移除 `<meta>` 標記的視口的結果。 如果沒有 `<meta>` 標記的視口，瀏覽器會縮小為預設的視口寬度（850圖元或更寬，適用于大部分的行動瀏覽器）。

[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)

復原您的變更：將設定檔中的 `<meta>` 標記取消批註，並將媒體查詢還原至*網站 .css*檔案中的850圖元。 儲存您的變更並重新整理行動瀏覽器，以確認是否已還原行動方便的顯示器。

[視口] `<meta>` 標記，而 CSS 媒體查詢不是 ASP.NET MVC 4 特有的，而且您可以在任何 web 應用程式中利用這些功能。 但是，這些檔案現在已內建在您建立新的 ASP.NET MVC 4 專案時所產生的檔案中。

如需有關視口 `<meta>` 標記的詳細資訊，請參閱[兩個數據區的故事-第二部分](http://www.quirksmode.org/mobile/viewports2.html)。

您將在下一節看到如何提供行動瀏覽器專用的檢視。

## <a name="overriding-views-layouts-and-partial-views"></a>覆寫視圖、版面配置和部分視圖

ASP.NET MVC 4 中的重要新功能是一種簡單的機制，可讓您針對一般行動瀏覽器、個別行動瀏覽器或任何特定瀏覽器，覆寫任何視圖（包括版面配置和部分觀點）。 若要提供行動裝置專屬的檢視，您可以複製檢視檔案並將 *.Mobile* 新增至檔案名稱。 例如，若要建立行動*索引*視圖，請將*Views\Home\Index.cshtml*複製到*Views\Home\Index.Mobile.cshtml*。

本節將建立行動裝置專屬的配置檔案。

若要開始，請將*Views\Shared\\_Layout. cshtml*複製到*Views\Shared\\_Layout。* 開啟 *\_Layout* ，並將標題從  **MVC4 會議** 變更為 **會議（** 行動裝置）。

在每個 `Html.ActionLink` 呼叫中，移除每*個連結的*[流覽者]。 下列程式碼顯示行動配置檔案的已完成主體區段。

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample5.cshtml)]

將*Views\Home\AllTags.cshtml*檔案複製到*Views\Home\AllTags.Mobile.cshtml*。 開啟新檔案並將 `<h2>` 元素從 "Tags" 變更為 "Tags (M)"：

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample6.html)]

使用桌面瀏覽器及行動瀏覽器模擬器，瀏覽至標籤頁面。 行動瀏覽器模擬器會顯示您所做的兩個變更。

[![p2m_layoutTags。 mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)

相較之下，桌面顯示器並未改變。

[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)

## <a name="browser-specific-views"></a>瀏覽器特定的視圖

除了行動與桌面專用的檢視之外，您還可以為個別瀏覽器建立檢視。 例如，您可以建立專屬於 iPhone 瀏覽器的視圖。 在本節中，您要建立 iPhone 瀏覽器的配置，以及 iPhone 版的 *AllTags* 檢視。

開啟*global.asax*檔案，並將下列程式碼新增至 `Application_Start` 方法。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample7.cs)]

此程式碼會定義要比對每個連入要求且名為 "iPhone" 的新顯示模式。 若連入的要求符合您定義的條件 (亦即使用者代理程式包含 "iPhone" 字串)，則 ASP.NET MVC 會尋找名稱包含 "iPhone" 字尾的檢視。

以滑鼠右鍵按一下程式碼的 `DefaultDisplayMode`，選擇 [解析]，然後選擇 `using System.Web.WebPages;`。 這麼做會將參考加入定義 `System.Web.WebPages` 和 `DisplayModes` 類型的 `DefaultDisplayMode` 命名空間。

[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)

或者，您可以手動將以下的行加入檔案的 `using` 區段即可。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample8.cs)]

*Global.asax*檔案的完整內容如下所示。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample9.cs)]

儲存變更。 將*MvcMobile\Views\Shared\\_Layout.* *MvcMobile\Views\Shared\\_Layout. iPhone*。 開啟新檔案，然後將 `h1` 標題從 `Conference (Mobile)` 變更為 [`Conference (iPhone)`]。

將*MvcMobile\Views\Home\AllTags.Mobile.cshtml*檔案複製到*MvcMobile\Views\Home\AllTags.iPhone.cshtml*。 在新檔案中，將 `<h2>` 元素從「Tags (M)」變更為「Tags (iPhone)」。

執行應用程式。 執行行動瀏覽器模擬器，請確認其使用者代理程式設為「iPhone」，然後瀏覽至 *AllTags* 檢視。 下列螢幕擷取畫面顯示在[Safari](http://www.apple.com/safari/download/)瀏覽器中呈現的*AllTags*視圖。 您可以在[這裡](https://support.apple.com/kb/DL1531)下載適用于 Windows 的 Safari。

[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)

在本節中，我們已了解如何建立行動配置和檢視，以及如何為特定裝置 (例如 iPhone) 建立配置和檢視。 在下一節中，您將瞭解如何運用 jQuery Mobile 來提供更吸引人的行動裝置。

## <a name="using-jquery-mobile"></a>使用 jQuery Mobile

[JQuery Mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html)程式庫提供一個可在所有主要行動瀏覽器上運作的使用者介面架構。 jQuery Mobile 會對支援 CSS 和 JavaScript 的行動瀏覽器套用*漸進增強功能*。 漸進式增強功能可讓所有瀏覽器顯示網頁的基本內容，同時允許更強大的瀏覽器和裝置具有更豐富的顯示。 JQuery Mobile 樣式的 JavaScript 和 CSS 檔案包含許多元素，以符合行動瀏覽器，而不會進行任何標記變更。

在本節中，您將安裝*Jquery MOBILE MVC* NuGet 封裝，它會安裝 jquery Mobile 和視圖切換器 widget。

若要開始，請先刪除您稍早建立的*共用\\_Layout.* 和*共用\\_Layout iPhone*檔案。

將*Views\Home\AllTags.Mobile.cshtml*和*Views\Home\AllTags.iPhone.cshtml*檔案重新命名為*Views\Home\AllTags.iPhone.cshtml.hide*和*Views\Home\AllTags.Mobile.cshtml.hide*。 因為檔案不再有 *. cshtml*副檔名，所以 ASP.NET MVC 執行時間不會使用這些檔案來轉譯*AllTags*視圖。

執行下列動作以安裝*jQuery* NuGet 套件：

1. 從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。

    [![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)
2. 在 [**套件管理員主控台**] 中，輸入 `Install-Package jQuery.Mobile.MVC -version 1.0.0`

下圖顯示 NuGet jQuery. node.js 封裝新增和變更至 MvcMobile 專案的檔案。 新增的檔案會在檔案名後面附加 [add]。 影像不會顯示新增至*Content\images*資料夾的 GIF 和 PNG 檔案。

![](aspnet-mvc-4-mobile-features/_static/image21.png)

JQuery NuGet 套件會安裝下列各項：

- *應用程式\_Start\BundleMobileConfig.cs*檔，這是參考所新增之 jQuery JAVASCRIPT 和 CSS 檔案所需的檔案。 您必須遵循下列指示，並參考此檔案中定義的行動套件組合。
- jQuery Mobile CSS 檔案。
- `ViewSwitcher` 控制器 widget （*Controllers\ViewSwitcherController.cs*）。
- jQuery Mobile JavaScript 檔案。
- JQuery Mobile 樣式配置檔案（*Views\Shared\\_Layout。*
- 「視圖-切換器部分視圖」 *（MvcMobile\Views\Shared\\_ViewSwitcher. cshtml*），可在每個頁面頂端提供連結，以從 [桌面] 視圖切換至 [mobile view]，反之亦然。
- <em>Content\images</em>資料夾中有數個<em>.png</em>和<em>.gif</em>影像檔案。

開啟*global.asax*檔案，並加入下列程式碼做為 `Application_Start` 方法的最後一行。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample10.cs)]

下列程式碼顯示完整的*global.asax*檔案。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample11.cs?highlight=26)]

> [!NOTE]
> 如果您使用的是 Internet Explorer 9，但未在黃色醒目提示中看到 [`BundleMobileConfig`] 行，請按一下 IE 中![[相容性](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "[相容性檢視] 按鈕的圖片（關閉）")視圖] 按鈕的 [[相容性](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)視圖] 按鈕 [圖片]，讓圖示從![[相容性檢視] 按鈕（關閉）](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "[相容性檢視] 按鈕的圖片（關閉）")的大綱圖片變更為![[相容性檢視] 按鈕的純色圖片（開啟）](https://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "[相容性檢視] 按鈕的圖片（開啟）")。 或者，您可以在 FireFox 或 Chrome 中觀看本教學課程。

開啟*MvcMobile\Views\Shared\\_Layout* ，然後在 `Html.Partial` 呼叫之後，直接新增下列標記：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample12.cshtml)]

完整的*MvcMobile\Views\Shared\\_Layout* ，如下所示：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample13.cshtml)]

建立應用程式，然後在您的行動瀏覽器模擬器中，流覽至 [ *AllTags* ] 視圖。 這時會顯示下列項目：

[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)

> [!NOTE]
> 您可以藉由將 IE 或 Chrome[的使用者代理字串設定](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)為 iPhone，然後使用 F-12 開發人員工具，來對行動裝置的特定程式碼進行偵錯工具。 如果您的行動瀏覽器未將 [**首頁**]、[**說話者**]、[**標記**] 和 [**日期**] 連結顯示為按鈕，則 jQuery mobile 腳本和 CSS 檔案的參考可能會不正確。

除了樣式變更之外，您還會看到 [ **mobile view** ] 和一個連結，可讓您從 [行動視圖] 切換到 [桌面視圖]。 選擇 [**桌面視圖**] 連結，隨即會顯示桌面視圖。

[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)

[桌面] 視圖無法直接流覽回到 [行動] 視圖。 您會立即修正此問題。 開啟*Views\Shared\\_Layout. cshtml*檔案。 在 `body` 專案的頁面下，新增下列程式碼，以轉譯視圖切換器 widget：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample14.cshtml)]

重新整理行動瀏覽器中的*AllTags*視圖。 您現在可以在 [桌面] 和 [行動裝置] 視圖之間流覽。

[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)

> [!NOTE]
> Debug note：您可以將下列程式碼新增至 Views\Shared _ViewSwitcher\\的結尾，以在使用瀏覽器將使用者代理字串設定為行動裝置時，協助偵錯工具。
>
> [!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample15.cs)]
>
> 並將下列標題新增至*Views\Shared\\_Layout. cshtml*檔案。
>
> [!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample16.html)]

流覽至桌面瀏覽器中的 [ *AllTags* ] 頁面。 「視圖切換器」 widget 不會顯示在桌面瀏覽器中，因為它只會新增至行動版面配置頁面。 稍後在本教學課程中，您會看到如何將視圖切換器 widget 新增至桌面視圖。

[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)

## <a name="improving-the-speakers-list"></a>改善喇叭清單

在行動瀏覽器中，選取 [演講者] 連結。 因為沒有 mobile view （*AllSpeakers*），所以會使用行動裝置版面配置視圖（ *\_layout*）來呈現預設的喇叭顯示（*AllSpeakers*）。

[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)

您可以藉由將 `RequireConsistentDisplayMode` 設定為 [ *Views]\\_ViewStart. cshtml*檔案中的 `true`，將預設（非行動）視圖全域停用在行動配置內呈現，如下所示：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample17.cshtml)]

當 `RequireConsistentDisplayMode` 設定為 `true`時，行動裝置版面配置（<em>\_配置. cshtml</em>）只會用於行動裝置視圖。 （也就是說，視圖檔案的格式為<em>* * ViewName</em><em>。</em>`RequireConsistentDisplayMode`，如果您的行動配置不適用於您的非行動裝置的視圖，您可能會想要設定 `true`。 下列螢幕擷取畫面顯示當 `RequireConsistentDisplayMode` 設定為 `true`時，<em>說話</em>者頁面的呈現方式。

[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)

您可以藉由將 `RequireConsistentDisplayMode` 設定為在視圖檔案中 `false`，停用一致的顯示模式。 *Views\Home\AllSpeakers.cshtml*檔案中的下列標記會將 `RequireConsistentDisplayMode` 設定為 `false`：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample18.cshtml)]

## <a name="creating-a-mobile-speakers-view"></a>建立行動喇叭視圖

如您適才所見，行動裝置上的 [ *演講者* ] 檢視已可讀取，但是連結卻非常微小而不容易點選。 在本節中，您將建立與新式行動應用程式類似的行動裝置特定*說話*者，它會顯示大型、易於分的連結，並包含搜尋方塊來快速尋找喇叭。

將*AllSpeakers*複製到*AllSpeakers*。 開啟*AllSpeakers*檔案，並移除 `<h2>` 的標題元素。

在 [`<ul>`] 標籤中，加入 `data-role` 屬性，並將其值設定為 [`listview`]。 就像其他[`data-*` 屬性](http://html5doctor.com/html5-custom-data-attributes/)一樣，`data-role="listview"` 讓大型清單專案變得更容易。 完成的標記如下所示：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample19.cshtml)]

重新整理行動瀏覽器。 更新的檢視如下所示：

[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)

雖然行動視圖已改良，但很難以流覽長的說話者清單。 若要修正此問題，請在 `<ul>` 標記中加入 `data-filter` 屬性，並將它設定為 [`true`]。 下列程式碼顯示 `ul` 標記。

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample20.html)]

下圖顯示 `data-filter` 屬性所產生之頁面頂端的 [搜尋] 篩選方塊。

[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)

當您在 [搜尋] 方塊中輸入每個字母時，jQuery Mobile 會篩選顯示的清單，如下圖所示。

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)

## <a name="improving-the-tags-list"></a>改善標記清單

就像預設*說話*者的觀點一樣，*標記*視圖也是可讀取的，但連結很小，而且很容易在行動裝置上點擊。 在本節中，您將以修正*喇叭*視圖的相同方式來修正*標記*的觀點。

移除 &quot;隱藏&quot; 尾碼至*Views\Home\AllTags.Mobile.cshtml.hide*檔案，使其名稱為*Views\Home\AllTags.Mobile.cshtml*。 開啟重新命名的檔案，並移除 `<h2>` 元素。

將 `data-role` 和 `data-filter` 屬性新增至 `<ul>` 標記，如下所示：

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample21.html)]

下圖顯示字母 `J`的標記頁面篩選。

[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)

## <a name="improving-the-dates-list"></a>改善日期清單

您可以改善 [*說話*者 *] 和 [* 標籤] 視圖，讓您更輕鬆地在行動裝置上使用 [*日期*]。

將*Views\Home\AllDates.cshtml*檔案複製到*Views\Home\AllDates.Mobile.cshtml*。 開啟新檔案，並移除 `<h2>` 元素。

將 `data-role="listview"` 新增至 `<ul>` 標記，如下所示：

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample22.html)]

下圖顯示 [**日期**] 頁面在 [`data-role`] 屬性備妥的樣子。

[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png)使用下列程式碼取代*Views\Home\AllDates.Mobile.cshtml*檔案的內容：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample23.cshtml)]

此程式碼會以天為單位來分組所有會話。 它會為每個新的日期建立清單分隔線，並列出分隔線下每一天的所有會話。 以下是此程式碼執行時的樣子：

[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)

## <a name="improving-the-sessionstable-view"></a>改善 SessionsTable 視圖

在本節中，您將建立會話的行動特定視圖。 我們所做的變更會比我們所建立的其他視圖更廣泛。

在行動瀏覽器中，按一下 [**喇叭**] 按鈕，然後在搜尋方塊中輸入 `Sc`。

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)

請按**Scott Hanselman**連結。

[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)

如您所見，在行動瀏覽器上顯示的畫面很容易閱讀。 [日期] 資料行難以閱讀，而且 [標記] 資料行不在視圖中。 若要修正此問題，請將*Views\Home\SessionsTable.cshtml*複製到*Views\Home\SessionsTable.Mobile.cshtml*，然後將檔案的內容取代為下列程式碼：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample24.cshtml)]

程式碼會移除 [會議室] 和 [標籤] 資料行，並以垂直方式格式化標題、說話者和日期，以便在行動瀏覽器上閱讀所有資訊。 下圖反映了程式碼變更。

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)

## <a name="improving-the-sessionbycode-view"></a>改善 SessionByCode 視圖

最後，您將建立*SessionByCode* view 的行動特定視圖。 在行動瀏覽器中，按一下 [**喇叭**] 按鈕，然後在搜尋方塊中輸入 `Sc`。

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)

請按**Scott Hanselman**連結。 會顯示 Scott Hanselman 的會話。

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)

選擇 [ **MS Web Stack 的愛**] 連結的總覽。

[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)

預設桌面視圖是正常的，但您可以加以改善。

將*Views\Home\SessionByCode.cshtml*複製到*Views\Home\SessionByCode.Mobile.cshtml* ，並以下列標記取代*Views\Home\SessionByCode.Mobile.cshtml*檔案的內容：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample25.cshtml)]

新的標記會使用 `data-role` 屬性來改善視圖的版面配置。

重新整理行動瀏覽器。 下圖反映您剛做的程式碼變更：

[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)

## <a name="wrapup-and-review"></a>Wrapup 與審查

本教學課程引進了 ASP.NET MVC 4 Developer Preview 的新行動功能。 行動功能包括：

- 覆寫版面配置、視圖和部分視圖的能力，全域和個別視圖皆可。
- 使用 `RequireConsistentDisplayMode` 屬性來控制版面配置和部分覆寫的強制執行。
- 行動裝置視圖的視圖切換器 widget 也可以在桌面視圖中顯示。
- 支援支援特定的瀏覽器，例如 iPhone 瀏覽器。

## <a name="see-also"></a>另請參閱

- [JQuery mobile](http://jquerymobile.com)網站。
- [jQuery Mobile 總覽](http://jquerymobile.com/demos/1.0b3/docs/about/intro.html)
- [W3C 推薦的行動 Web 應用程式最佳做法](http://www.w3.org/TR/mwabp/)
- [W3C 針對媒體查詢的候選推薦做法](http://www.w3.org/TR/css3-mediaqueries/)
