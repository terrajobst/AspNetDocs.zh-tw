---
uid: whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application
title: 如何：將行動頁面加入至您的 ASP.NET Web Forms/MVC 應用程式 |Microsoft Docs
author: rick-anderson
description: 本 how To 說明各種方式來提供針對 ASP.NET Web Forms/MVC 應用程式中的行動裝置優化的頁面，並建議架構和 。
ms.author: riande
ms.date: 01/20/2011
ms.assetid: 3124f28e-cc32-418a-afe3-519fa56f4c36
msc.legacyurl: /whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application
msc.type: content
ms.openlocfilehash: 63c555358d06a9506bb5c8c993800c3307108192
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78572734"
---
# <a name="how-to-add-mobile-pages-to-your-aspnet-web-forms--mvc-application"></a>如何：將行動頁面新增至您的 ASP.NET Web Forms/MVC 應用程式

> **適用于**
> 
> - ASP.NET Web Forms 版本4。0
> - ASP.NET MVC 版本3。0
> 
> **摘要**
> 
> 本 how To 說明各種方式來提供針對 ASP.NET Web Forms/MVC 應用程式中的行動裝置優化的頁面，並建議在以各種裝置為目標時應考慮的架構和設計問題。 本檔也會說明為什麼從 ASP.NET 2.0 到3.5 的 ASP.NET Mobile 控制項現在已過時，並討論一些現代化的替代方案。

## <a name="contents"></a>內容

- 概觀
- 架構選項
- 瀏覽器和裝置偵測
- ASP.NET Web form 應用程式如何呈現行動特定的頁面
- ASP.NET MVC 應用程式如何呈現行動特定的頁面
- 其他資源

如需適用于 ASP.NET Web form 和 MVC 的可下載程式代碼範例，請參閱[使用 ASP.NET Mobile Apps & 網站](https://docs.microsoft.com/aspnet/mobile/overview)。

## <a name="overview"></a>概觀

行動裝置–智慧型手機、功能電話和平板電腦–會繼續在熱門程度上成長，以作為存取網路的途徑。 對於許多 網頁程式開發人員和 web 導向的企業而言，這表示為使用這些裝置的訪客提供絕佳的流覽體驗變得越來越重要。

### <a name="how-earlier-versions-of-aspnet-supported-mobile-browsers"></a>舊版 ASP.NET 支援的行動瀏覽器版本

ASP.NET 版本2.0 至3.5 包含*ASP.NET Mobile 控制項*：一組適用于行動裝置的伺服器控制項，位於*system.web* .dll 元件和*system.web. UI. MobileControls*命名空間中。 元件仍包含在 ASP.NET 4 中，但已被取代。 建議開發人員遷移到更現代化的方法，例如本文所述。

ASP.NET Mobile 控制項已標示為過時的原因，在於其設計是圍繞在2005和更早版本上常見的行動電話。 這些控制項主要是設計來呈現該紀元之 WAP 瀏覽器的 WML 或 cHTML 標籤（而不是一般 HTML）。 但是 WAP、WML 和 cHTML 已不再與大多數專案相關，因為 HTML 現在已成為行動和桌面瀏覽器的普遍標記語言。

### <a name="the-challenges-of-supporting-mobile-devices-today"></a>立即支援行動裝置的挑戰

雖然行動瀏覽器現在幾乎普遍支援 HTML，但當您想要建立絕佳的行動流覽體驗時，仍然會面臨許多挑戰：

- ***螢幕大小***-行動裝置的形式有很大的變化，而且其螢幕通常會比桌面監視器小。 因此，您可能需要為它們設計完全不同的頁面配置。
- ***輸入法***–有些裝置有鍵盤，有些則有 styluses，其他則使用觸控。 您可能需要考慮多個導覽機制和資料輸入方法。
- ***標準合規性***–許多行動瀏覽器不支援最新的 HTML、CSS 或 JavaScript 標準。
- ***頻寬***–行動資料網路的效能會有很高的差異，而某些使用者的關稅會依 mb 收費。

沒有一體適用的解決方案;您的應用程式將必須根據存取它的裝置，以不同的方式來查看和行為。 視您想要的行動支援層級而定，對於 網頁程式開發人員而言，這可能是比桌上型電腦「瀏覽器星際大戰」更大的挑戰。

第一次接近行動瀏覽器支援的開發人員通常會認為只有在支援最新且最複雜的 smartphone （例如，Windows Phone 7、iPhone 或 Android）時，可能是因為開發人員通常是個人擁有的裝置. 不過，較便宜的手機仍然非常受歡迎，而且其擁有者會使用它們來流覽 web，特別是在行動電話比寬頻連線更容易取得的國家/地區。 您的企業必須考慮可能的客戶，以決定要支援哪一系列的裝置。 如果您想要為每個高階的衛生 spa 建立線上手冊，則您可能會決定僅以先進的智慧型手機為目標，而如果您要為電影院建立票證預約系統，您可能需要為具有較不強大功能的訪客進行考慮致電.

## <a name="architectural-options"></a>架構選項

在取得 ASP.NET Web form 或 MVC 的特定技術細節之前，請注意，Web 開發人員一般有三個可能的選項可支援行動瀏覽器：

1. ***不執行任何動作–*** 您可以直接建立標準的桌面導向 web 應用程式，並依賴行動瀏覽器來呈現它可接受。 

    - **優點**：這是執行和維護的最便宜選項–不需額外的工作
    - **缺點**：提供最差的使用者體驗： 

        - 最新的智慧型手機可能會呈現您的 HTML，以及桌面瀏覽器，但是使用者仍然會被強制縮放並以水準和垂直方式滾動，以在小型螢幕上取用您的內容。 這遠低於最佳。
        - 較舊的裝置和功能電話可能無法以滿意的方式轉譯您的標記。
        - 即使是最新的平板電腦裝置（其螢幕可以與筆記本電腦螢幕一樣大），也適用不同的互動規則。 以觸控為基礎的輸入最適用于較大的按鈕和連結，而且沒有任何方法可以將滑鼠游標暫留在飛出功能表上。
2. ***解決用戶端上的問題*–** 使用 CSS 和[漸進增強功能](http://en.wikipedia.org/wiki/Progressive_enhancement)時，您可以建立標記、樣式和腳本，以適應執行它們的任何瀏覽器。 例如，透過[CSS 3 媒體查詢](http://www.w3.org/TR/2010/CR-css3-mediaqueries-20100727/)，您可以建立多重資料行配置，在其螢幕比所選閾值較窄的裝置上轉換成單一資料行版面配置。 

    - **優點**：針對使用中的特定裝置優化轉譯，即使是根據其所擁有的任何螢幕和輸入特性而定，也是未知的未來裝置
    - **優點**：輕鬆讓您跨所有裝置類型共用伺服器端邏輯–最少重複的程式碼或花費
    - **缺點**：行動裝置與桌面裝置不同，您可能會想要讓行動頁面與桌面頁面完全不同，並顯示不同的資訊。 這類變化可能沒有效率，也不可能透過 CSS 單獨達成，特別是考慮較舊的裝置如何解讀 CSS 規則。 這特別適用于 CSS 3 屬性。
    - **缺點**：不支援不同裝置的各種伺服器端邏輯和工作流程。 例如，您無法透過 CSS 來為行動使用者執行簡化的購物車簽出工作流程。
    - **缺點**：頻寬使用效率不佳。 您的伺服器可能必須傳輸適用于所有可能裝置的標記和樣式，即使目標裝置只會使用該資訊的子集也一樣。
3. ***解決伺服器上的問題*–** 如果您的伺服器知道哪些裝置正在存取它（或至少該裝置的特性，例如其螢幕大小和輸入方法），以及它是否為行動裝置–它可以執行不同的邏輯，並輸出不同的 HTML 標籤。 

    - **優點：** 最大彈性。 您可以根據所需的裝置特定版面配置，將您的伺服器端邏輯行動或優化您的標記，而不會有多少限制。
    - **優點：** 有效率的頻寬使用。 您只需要傳輸目標裝置即將使用的標記和樣式資訊。
    - **缺點：** 有時候會強制重複執行工作或程式碼（例如，讓您建立類似但稍微不同的 Web form 頁面或 MVC 視圖複本）。 可能的話，您會將通用邏輯分解成基礎層或服務，但您可能必須複製 UI 程式碼或標記的某些部分，然後以平行方式進行維護。
    - **缺點：** 裝置偵測並不簡單。 它需要已知裝置類型的清單或資料庫及其特性（可能不一定是完美的最新狀態），而且不保證能正確地比對每個傳入的要求。 本檔稍後會說明一些選項及其陷阱。

為了獲得最佳結果，大部分的開發人員都發現他們需要結合選項（2）和（3）。 在使用 CSS 或甚至是 JavaScript 的用戶端上，次要的樣式差異最合適，而資料、工作流程或標記的主要差異最有效地在伺服器端程式碼中執行。

### <a name="this-paper-focuses-on-server-side-techniques"></a>本白皮書著重于伺服器端技術

由於 ASP.NET Web form 和 MVC 主要都是伺服器端技術，這份白皮書將著重于伺服器端技術，讓您為行動瀏覽器產生不同的標記和邏輯。 當然，您也可以將它與任何用戶端技術（例如 CSS 3 媒體查詢、漸進增強 JavaScript）結合，但這比 ASP.NET 開發更是 web 設計。

## <a name="browser-and-device-detection"></a>瀏覽器和裝置偵測

支援行動裝置之所有伺服器端技術的主要必要條件是知道您的訪客所使用的裝置。 事實上，甚至比知道裝置的製造商和型號來知道裝置的*特性*來得好。 特性可能包括：

- 這是行動裝置嗎？
- 輸入法（滑鼠/鍵盤、觸控、鍵盤、搖桿 ...）
- 螢幕大小（實際和以圖元為單位）
- 支援的媒體和資料格式
- 等。

最好是根據特性來做出決策，而不是模型編號，因為如此一來，您就可以更妥善地處理未來的裝置。

### <a name="using-aspnets-built-in-browser-detection-support"></a>使用 ASP。NET 的內建瀏覽器偵測支援

ASP.NET Web form 和 MVC 開發人員可以藉由檢查*要求*的屬性，立即探索造訪瀏覽器的重要特性。 例如，請參閱

- IsMobileDevice
- MobileDeviceManufacturer，要求. 瀏覽器. MobileDeviceModel
- ScreenPixelsWidth
- SupportsXmlHttp
- ...還有許多其他專案

在幕後，ASP.NET 平臺會比對傳入的*使用者代理程式*（UA） HTTP 標頭與一組瀏覽器定義 XML 檔案中的正則運算式。 根據預設，平臺會包含許多一般行動裝置的定義，您可以為想要辨識的其他人新增自訂瀏覽器定義檔案。 如需詳細資訊，請參閱 MSDN 網頁[ASP.NET Web 服務器控制項和瀏覽器功能](https://msdn.microsoft.com/library/x3k2ssx2.aspx)。

### <a name="using-the-wurfl-device-database-via-51degreesmobi-foundation"></a>透過 51Degrees.mobi Foundation 使用 WURFL 裝置資料庫

While ASP。NET 的內建瀏覽器偵測支援對許多應用程式而言都已足夠，但有兩個主要案例可能不夠：

- ***您想要辨識最新的裝置***（不需要手動建立它們的瀏覽器定義檔）。 請注意，.NET 4 的瀏覽器定義檔案不夠新，無法辨識 Windows Phone 7、Android 手機、Opera Mobile 瀏覽器或 Apple Ipad。
- ***您需要更多有關裝置功能的詳細資訊***。 您可能需要知道裝置的輸入法（例如，觸控與鍵盤），或瀏覽器支援的音訊格式。 這項資訊無法在標準瀏覽器定義檔案中使用。

[*無線通用資源檔*（WURFL）專案](http://wurfl.sourceforge.net/)會維護現今使用之行動裝置的最新和詳細資訊。

.NET 開發人員的好消息是 ASP。NET 的瀏覽器偵測功能是可擴充的，因此可以增強它來克服這些問題。 例如，您可以將開放原始碼[*51Degrees.mobi Foundation*](https://github.com/51Degrees/dotNET-Device-Detection)程式庫新增至您的專案。 這是 ASP.NET IHttpModule 或瀏覽器功能提供者（可在 Web form 和 MVC 應用程式上使用），會直接讀取 WURFL 資料並將其連結至 ASP。NET 的內建瀏覽器偵測機制。 當您安裝了模組之後，*要求瀏覽器*會突然包含更精確且詳細的資訊：它會正確辨識先前提到的許多裝置，並列出其功能（包括其他功能，例如輸入法）。 如需詳細資訊，請參閱專案的檔。

## <a name="how-web-forms-applications-can-present-mobile-specific-pages"></a>Web form 應用程式如何顯示行動專用的頁面

根據預設，以下是在常見行動裝置上顯示全新 Web Forms 應用程式的方式：

![](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/_static/image1.png)

很明顯地，版面配置看起來非常方便使用，此頁面是專為大型的橫向式監視器所設計，不適用於較小的直向畫面。 那麼您該怎麼做呢？

如本文稍早所述，有許多方式可為行動裝置量身打造您的頁面。 有些技術是以伺服器為基礎，其他則是在用戶端上執行。

### <a name="creating-a-mobile-specific-master-page"></a>建立行動裝置特定的主版頁面

根據您的需求，您可以針對所有訪客使用相同的 Web 表單，但有兩個不同的主版頁面：一個用於桌面訪客，另一個用於行動訪客。 這可讓您彈性地將 CSS 樣式表單或最上層 HTML 標籤變更為符合行動裝置，而不會強迫您複製任何頁面邏輯。

這很容易執行。 例如，您可以將下列等 PreInit 處理常式新增至 Web 表單：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample1.cs)]

現在，在應用程式的最上層資料夾中，建立名為 Mobile 的主版頁面，並會在偵測到行動裝置時使用。 如有需要，您的行動主版頁面可以參考行動特定的 CSS 樣式表單。 桌面訪客仍然會看到您的預設主版頁面，而不是行動裝置。

### <a name="creating-independent-mobile-specific-web-forms"></a>建立獨立的行動特定 Web 表單

為了達到最大彈性，您可以比只針對不同的裝置類型擁有不同的主版頁面，更進一步。 您可以執行兩組*完全不同的 Web Forms 頁面*，一組用於桌面瀏覽器，另一組用於行動。 如果您想要向行動訪客呈現非常不同的資訊或工作流程，這會是最佳的效果。 本節的其餘部分將詳細說明這種方法。

假設您已經有針對桌面瀏覽器設計的 Web form 應用程式，最簡單的方法就是在您的專案中建立名為 "Mobile" 的子資料夾，並在該處建立您的行動頁面。 您可以使用所有其他 Web Forms 應用程式所使用的相同技術，來建立整個子網站，以及自己的主版頁面、樣式表單和頁面。 您不一定需要針對桌面網站中的*每個*頁面產生對等的行動。您可以選擇適合行動訪客的功能子集。

如果您想要的話，您的行動頁面可以與您的一般頁面共用一般靜態資源（例如影像、JavaScript 或 CSS 檔案）。 由於您的「行動」資料夾在裝載于 IIS 時*不*會被標示為個別的應用程式（它只是 Web form 頁面的簡單子資料夾），因此也會共用所有相同的設定、會話資料和其他基礎結構作為您的桌面網頁。

> [!NOTE]
> 由於這種方法通常牽涉到部分程式碼（行動頁面可能與桌面頁面共用一些相似之處），因此請務必將任何常見的商務邏輯或資料存取程式碼，分解成共用的基礎層或服務。 否則，您將會加倍建立和維護應用程式的工作。

#### <a name="redirecting-mobile-visitors-to-your-mobile-pages"></a>將行動訪客重新導向至您的行動頁面

只有在流覽會話中的*第一個*要求（而不是其會話中的每個要求）將行動訪客重新導向至行動頁面，這通常是很方便的動作，因為：

- 如此一來，您就可以輕鬆地允許行動訪客存取您的桌面頁面，只要在主版頁面上放入「桌上出版本」的連結即可。 訪客不會重新導向回到行動頁面，因為它不再是其會話中的第一個要求。
- 它可以避免干擾您網站的桌面和行動裝置元件間共用之任何動態資源的要求（例如，如果您有共同的 Web 表單，而網站的桌面和行動元件都顯示在 IFRAME 中，或特定 Ajax 處理常式）

若要這樣做，您可以將重新導向邏輯放在**會話中\_Start**方法。 例如，將下列方法新增至您的 Global.asax.cs 檔案：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample2.cs)]

#### <a name="configuring-forms-authentication-to-respect-your-mobile-pages"></a>設定表單驗證以尊重您的行動頁面

請注意，表單驗證會針對在驗證程式期間和之後可將訪客重新導向的位置做出一些假設：

- 當使用者需要驗證時，表單驗證會將他們重新導向至您的桌面登入頁面，不論他們是桌上型電腦或行動使用者（因為它只有*一個*登入 URL 的概念）。 假設您想要以不同的方式為您的行動登入頁面建立樣式，您必須增強桌面登入頁面，使其將行動使用者重新導向至不同的行動登入頁面。 例如，將下列程式碼新增到您的**桌面**登入頁面程式碼後置： 

    [!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample3.cs)]
- 在使用者成功登入之後，表單驗證預設會將其重新導向至您的桌面首頁（因為它只有*一個*預設頁面的概念）。 您需要增強行動登入頁面，讓它在成功登入之後重新導向至行動首頁。 例如，將下列程式碼新增至行動登入頁面**的程式碼**後置： 

    [!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample4.cs)]
  
  這段程式碼假設您的頁面具有名為 LoginUser 的登入伺服器控制項，如同預設專案範本中所示。

### <a name="working-with-output-caching"></a>使用輸出快取

如果您使用的是輸出快取，請注意，根據預設，桌面使用者可以流覽特定 URL （導致其輸出快取），接著是行動使用者，接著收到快取的桌面輸出。 無論您是依裝置類型來改變主版頁面，或是針對每個裝置類型執行完全不同的 Web 表單，都適用此警告。

若要避免這個問題，您可以指示 ASP.NET 根據訪客是否使用行動裝置來改變快取專案。 將 VaryByCustom 參數新增至頁面的 OutputCache 宣告，如下所示：

[!code-aspx[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample5.aspx)]

接下來，將下列方法覆寫新增至您的 Global.asax.cs 檔案，以將*isMobileDevice*定義為自訂快取參數：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample6.cs)]

這可確保網頁的行動訪客不會收到先前由桌面訪客放入快取中的輸出。

### <a name="a-working-example"></a>一個實用的範例

若要查看這些技術的實際運作方式，請下載[此白皮書的程式碼範例](https://docs.microsoft.com/aspnet/mobile/overview)。 Web form 範例應用程式會自動將行動使用者重新導向至子資料夾中名為 Mobile 的一組行動特定頁面。 這些頁面的標記和樣式較適合用於行動瀏覽器，如下列螢幕擷取畫面所示：

![](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/_static/image2.png)

如需有關將行動瀏覽器的標記和 CSS 優化的更多秘訣，請參閱本檔後面的「行動瀏覽器的樣式行動頁面」一節。

## <a name="how-aspnet-mvc-applications-can-present-mobile-specific-pages"></a>ASP.NET MVC 應用程式如何呈現行動特定的頁面

由於模型視圖控制器模式會將應用程式邏輯（在控制器中）與展示邏輯（在 views 中）分離，因此您可以選擇下列任何方法來處理伺服器端程式碼中的行動支援：

1. ***針對桌上型電腦和行動瀏覽器使用相同的控制器和 views，但根據裝置類型 * 來轉譯具有不同 Razor 版面配置的視圖。** 如果您要在所有裝置上顯示相同的資料，但只想要提供不同的 CSS 樣式表單，或變更行動的一些最上層 HTML 元素，這個選項的效果最佳。
2. ***桌面和行動瀏覽器都使用相同的控制器，但根據裝置類型，呈現不同的視圖***。 如果您要顯示大致相同的資料，並為使用者提供相同的工作流程，但想要呈現非常不同的 HTML 標籤以符合所使用的裝置，這個選項的效果最佳。
3. ***為桌面和行動瀏覽器建立個別的區域，並針對每個 * 執行獨立的控制器和 views。** 如果您要顯示非常不同的畫面，其中包含不同的資訊，並讓使用者透過針對其裝置類型優化的不同工作流程，則此選項的效果最佳。 這可能表示某些程式碼重複，但是您可以將通用邏輯分解成基礎層或服務，以將其降至最低。

如果您想要採用**第一個**選項，而且只會改變每一裝置類型的 Razor 版面配置，很容易。 只要修改您的 \_ViewStart. cshtml 檔案，如下所示：

[!code-cshtml[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample7.cshtml)]

現在您可以使用針對行動裝置優化的頁面結構和 CSS 規則，建立稱為 \_LayoutMobile 的行動特定配置。

如果您想要讓**第二個**選項根據造訪者的裝置類型轉譯完全不同的視圖，請參閱[Scott Hanselman 的 blog 文章](http://www.hanselman.com/blog/ABetterASPNETMVCMobileDeviceCapabilitiesViewEngine.aspx)。

本檔的其餘部分著重于**第三個**選項–為行動裝置建立個別的控制器*和*視圖，因此您可以完全控制為行動訪客提供的功能子集。

### <a name="setting-up-a-mobile-area-within-your-aspnet-mvc-application"></a>在您的 ASP.NET MVC 應用程式內設定移動區

您可以用一般方式，將名為 "Mobile" 的區域新增至現有的 ASP.NET MVC 應用程式：以滑鼠右鍵按一下方案總管中的專案名稱，然後選擇 [新增] [à] [區域]。 接著，您可以像在 ASP.NET MVC 應用程式中的任何其他區域一樣，新增控制器和視圖。 例如，將名為 HomeController 的新控制器新增至您的行動區域，以作為 Mobile 訪客的首頁。

### <a name="ensuring-the-url-mobile-reaches-the-mobile-homepage"></a>確保 URL/Mobile 到達 Mobile 首頁

如果您想要讓 URL/Mobile 到達您的行動區域內部 HomeController 的 [索引] 動作，您必須對路由設定進行兩個小的變更。 首先，更新您的 MobileAreaRegistration 類別，讓 HomeController 是您的行動區域中的預設控制器，如下列程式碼所示：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample8.cs)]

這表示行動首頁現在會位於/Mobile，而不是/Mobile/Home，因為 "Home" 現在是行動頁面的隱含預設控制器名稱。

接下來，請注意，將第二個 HomeController 新增至您的應用程式（亦即，除了現有的桌上型電腦以外的行動裝置），您將會中斷一般的桌面首頁。 它將會失敗，並出現「*找到與名為 ' Home ' 的控制器相符的多個類型*」錯誤。 若要解決此問題，請更新您的頂層路由設定（在 Global.asax.cs 中），以指定當不明確時，您的桌面 HomeController 應優先考慮：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample9.cs)]

現在，錯誤會消失，且 URL HTTP：\/\/*yoursite*/會到達桌面首頁，而 HTTP：\/\/*yoursite*/mobile/會到達行動首頁。

### <a name="redirecting-mobile-visitors-to-your-mobile-area"></a>將行動訪客重新導向至您的行動區域

ASP.NET MVC 中有許多不同的擴充點，因此有許多可能的方法可以插入重新導向邏輯。 其中一個不錯的選項是建立篩選屬性 [RedirectMobileDevicesToMobileArea]，以在符合下列條件時執行重新導向：

1. 這是使用者會話中的第一個要求（亦即，IsNewSession 等於 true）
2. 要求來自行動瀏覽器（亦即，IsMobileDevice 等於 true）
3. 使用者尚未要求行動區域中的資源（亦即，URL 的*路徑*部分不是以/Mobile 開頭）

本白皮書隨附的可下載範例包含此邏輯的執行。 它會實作為授權篩選，衍生自 AuthorizeAttribute，這表示即使您使用輸出快取，它也可以正常運作（否則，如果桌面訪客第一次存取特定的 URL，桌面輸出可能會被快取，然後再提供給後續的行動訪客）。

因為它是一個篩選準則，所以您可以選擇將它套用到特定的控制器和動作，例如

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample10.cs)]

… 或者，您可以將它套用到所有控制器和動作，做為 Global.asax.cs 檔案中的 MVC 3*全域篩選*條件：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample11.cs)]

可下載的範例也會示範如何建立此屬性的子類別，以重新導向至行動區域內的特定位置。 例如，這表示您可以：

- 註冊全域篩選器，如上所示，預設會將行動訪客傳送至行動首頁。
- 此外，也請將特殊的 [RedirectMobileDevicesToMobileProductPage] 篩選準則套用至「觀看產品」動作，以將行動訪客帶到所要求之任何產品頁面的 mobile 版本。
- 也將篩選準則的其他特殊子類別套用至特定動作，並將行動訪客重新導向至對等的行動電話頁面

### <a name="configuring-forms-authentication-to-respect-your-mobile-pages"></a>設定表單驗證以尊重您的行動頁面

如果您是使用表單驗證，請注意，當使用者需要登入時，它會自動將使用者重新導向至單一特定的「登入」 URL，預設為 **/Account/LogOn**。 這表示行動使用者可能會被重新導向至您的桌面「登入」動作。

若要避免這個問題，請將邏輯新增至您的桌面「登入」動作，使其再次將行動使用者重新導向至 mobile 「登入」動作。 如果您使用的是預設的 ASP.NET MVC 應用程式範本，請更新 AccountController 的登入動作，如下所示：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample12.cs)]

… 然後在您的行動區域中，于名為 AccountController 的控制器上，執行適當的特定行動裝置「登入」動作。

### <a name="working-with-output-caching"></a>使用輸出快取

如果您使用 [OutputCache] 篩選準則，您必須強制快取專案因裝置類型而異。 例如，撰寫：

[!code-javascript[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample13.js)]

然後，將下列方法新增至您的 Global.asax.cs 檔案：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample14.cs)]

這可確保網頁的行動訪客不會收到先前由桌面訪客放入快取中的輸出。

### <a name="a-working-example"></a>一個實用的範例

若要查看這些技術的實際運作方式，請下載[這份白皮書相關的程式碼範例](https://docs.microsoft.com/aspnet/mobile/overview)。 此範例包含已增強的 ASP.NET MVC 3 （候選版）應用程式，可使用上述方法來支援行動裝置。

## <a name="further-guidance-and-suggestions"></a>進一步的指引和建議

下列討論適用于使用本檔所涵蓋之技術的 Web form 和 MVC 開發人員。

### <a name="enhancing-your-redirection-logic-using-51degreesmobi-foundation"></a>使用 51Degrees.mobi Foundation 增強重新導向邏輯

本檔中所顯示的重新導向邏輯對您的應用程式而言可能完全足夠，但如果您需要停用會話，或使用拒絕 cookie 的行動瀏覽器（這些都不能有會話），則無法運作，因為它不會知道指定的要求是否為來自該訪客的第一個。

您已經瞭解開放原始碼 51Degrees.mobi Foundation 如何改善 ASP 的精確度。NET 的瀏覽器偵測。 它也有內建的功能，可將行動訪客重新導向至 web.config 中設定的特定位置。藉由儲存訪客的 HTTP 標頭和 IP 位址之雜湊的暫時記錄，讓它知道每個要求是否是來自指定 vistor 的第一個，就能夠在不依賴 ASP.NET 會話（也就是 cookie）的情況下工作。

在 web.config 檔案的 fiftyOne 區段中新增的下列元素會將第一個要求從偵測到的行動裝置重新導向至頁面 ~/Mobile/Default.aspx。 不論裝置類型為何，行動資料夾底下的任何頁面要求都*不*會重新導向。 如果行動裝置已處於非使用中狀態一段20分鐘以上，則會忘記裝置，並將後續要求視為新的要求，以供重新導向之用。

[!code-xml[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample15.xml)]

如需詳細資訊，請參閱[51Degrees.mobi Foundation 檔](https://github.com/51Degrees/dotNET-Device-Detection)。

> [!NOTE]
> 您*可以*在 ASP.NET MVC 應用程式上使用 51Degrees.mobi Foundation 的重新導向功能，但您必須根據一般 url 定義重新導向設定，而不是在路由參數或將 MVC 篩選準則放在動作上。 這是因為（在撰寫本文時） 51Degrees.mobi Foundation 無法辨識篩選器或路由。

### <a name="disabling-transcoders-and-proxy-servers"></a>停用轉錄器和 Proxy 伺服器

行動網路操作員在行動網際網路的方法中有兩個廣泛的目標：

1. 盡可能提供最多相關內容
2. 最大化可共用有限無線網路頻寬的客戶數目

由於大部分的網頁都是針對大型桌上型電腦大小的螢幕和快速的固定線寬頻連線所設計，因此許多操作員會使用動態改變 web 內容的*轉錄器*或*proxy 伺服器*。 他們可以修改您的 HTML 標籤或 CSS，使其符合較小的螢幕（特別是「功能電話」，缺少處理複雜配置的處理能力），而且它們可能會重新壓縮您的影像（大幅降低其品質）以改善頁面傳遞速度。

但是，如果您已經致力於產生網站的行動優化版本，您可能不希望網路操作員進一步干擾。 您可以將下列這一行新增至頁面，\_ASP.NET Web Form 中的載入事件：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample16.cs)]

或者，對於 ASP.NET 的 MVC 控制器，您可以新增下列方法覆寫，以便套用至該控制器上的所有動作：

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample17.cs)]

產生的 HTTP 訊息會通知符合 W3C 規範的轉錄器和 proxy，而不是更改內容。 當然，並不保證行動網路操作員會遵循此訊息。

### <a name="styling-mobile-pages-for-mobile-browsers"></a>為行動瀏覽器設定行動頁面的樣式

這不在本檔的討論範圍內，非常詳細地說明哪些類型的 HTML 標籤可正確運作，或哪些 web 設計技術可將特定裝置上的可用性最大化。 您可以找出非常簡單的版面配置，針對行動大小的螢幕進行優化，而不需使用不可靠的 HTML 或 CSS 定位技巧。 不過，有一項重要的技術值得一提，那就是「*區中繼」標記*。

某些現代化行動瀏覽器的工作會顯示適用于桌面監視器的網頁、在虛擬畫布上轉譯頁面，也稱為「視口」（例如，虛擬區在 iPhone 上是980圖元寬，而在預設的 Opera Mobile 上為850圖元寬），然後將結果相應縮小，以符合螢幕的實體圖元。 然後，使用者可以放大和移動該區。 這有一個優點，就是讓瀏覽器在其預期的版面配置中顯示頁面，但它也具有強制縮放和移動的缺點，這對使用者而言並不方便。 如果您要針對行動裝置進行設計，最好是針對縮小畫面進行設計，這樣就不需要縮放或水準滾動。

一種方法，告訴行動瀏覽器，視口的寬度應透過非標準的*視口*中繼標記。 例如，如果您將下列內容新增至頁面的標頭區段，

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample18.html)]

… 然後支援 smartphone 瀏覽器會在 480-圖元寬的虛擬畫布上配置頁面。 這表示如果您的 HTML 專案定義其寬度（以百分比表示），則會根據這個480圖元寬度來解讀百分比，而不是預設的視窗素寬度。 因此，使用者較不可能必須水準縮放和移動–大幅改善行動流覽體驗。

如果您想要讓視口寬度符合裝置的實體圖元，您可以指定下列各項：

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample19.html)]

若要讓此作業正常運作，您不能明確地強制元素超過該寬度（例如，使用*width*屬性或 CSS 屬性），否則瀏覽器將被迫使用較大的區，而不論。 另請參閱：[有關非標準的視口標記的更多詳細資料](https://developer.apple.com/library/safari/#documentation/AppleApplications/Reference/SafariHTMLRef/Articles/MetaTags.html)。

大部分的新式 smartphone 都支援*雙重方向*：它們可以用直向或橫向模式來保留。 因此，請務必不要假設畫面寬度是以圖元為單位。 甚至不會假設螢幕寬度是固定的，因為使用者可以在您的頁面上重新調整其裝置的方向。

較舊的 Windows Mobile 和 Blackberry 裝置也可以接受頁首中的下列中繼標記，以通知其內容已針對行動裝置進行優化，因此不應進行轉換。

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample20.html)]

## <a name="additional-resources"></a>其他資源

如需您可以用來測試行動 ASP.NET web 應用程式的行動裝置模擬器和模擬器清單，請參閱[模擬熱門的行動裝置進行測試](../mobile/device-simulators.md)一頁。

## <a name="credits"></a>學分

- 主要作者： Steven Sanderson
- 審核者/其他內容作者： James Rosewell、Mikael Söderström、Scott Hanselman、Scott Hunter
