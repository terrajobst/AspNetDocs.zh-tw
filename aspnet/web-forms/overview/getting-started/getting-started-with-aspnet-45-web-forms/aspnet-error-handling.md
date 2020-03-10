---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
title: ASP.NET 錯誤處理 |Microsoft Docs
author: Erikre
description: 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 為我們建立 ASP.NET Web Forms 應用程式的基本概念 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 423498f7-1a4b-44a1-b342-5f39d0bcf94f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 9514142ca50b33470a3f4c033e4f8e319a9ee09b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78566679"
---
# <a name="aspnet-error-handling"></a>ASP.NET 錯誤處理

依[Erik Reitan](https://github.com/Erikre)

[下載 Wingtip 玩具範例專案（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下載電子書（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 建立 ASP.NET Web Forms 應用程式的基本概念。 本教學課程系列隨附有[ C#原始程式碼](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 專案。

在本教學課程中，您將修改 Wingtip 玩具範例應用程式，以包含錯誤處理和錯誤記錄。 錯誤處理會讓應用程式正常處理錯誤，並據以顯示錯誤訊息。 錯誤記錄可讓您尋找並修正已發生的錯誤。 本教學課程是以先前的「URL 路由」教學課程為基礎，而且是 Wingtip 玩具教學課程系列的一部分。

## <a name="what-youll-learn"></a>您將學到什麼：

- 如何將全域錯誤處理新增至應用程式的設定。
- 如何在應用程式、頁面和程式碼層級加入錯誤處理。
- 如何記錄錯誤以供日後審查。
- 如何顯示不會危及安全性的錯誤訊息。
- 如何執行錯誤記錄模組和處理常式（ELMAH）錯誤記錄。

## <a name="overview"></a>概觀

ASP.NET 應用程式必須能夠以一致的方式處理執行期間所發生的錯誤。 ASP.NET 使用 common language runtime （CLR），這種方式可讓您以一致的方式來通知應用程式的錯誤。 發生錯誤時，會擲回例外狀況。 例外狀況是應用程式遇到的任何錯誤、條件或非預期的行為。

在 .NET Framework 中，例外狀況是從 `System.Exception` 類別繼承的物件。 從發生問題的程式碼區域擲回例外狀況。 例外狀況會在呼叫堆疊中向上傳遞至一個位置，應用程式會在此處提供可處理例外狀況的程式碼。 如果應用程式未處理例外狀況，則會強制瀏覽器顯示錯誤詳細資料。

最佳做法是，在程式碼層級中處理 `Try`/`Catch`/`Finally` 區塊內的錯誤。 請嘗試放置這些區塊，讓使用者能夠更正其發生所在內容中的問題。 如果錯誤處理區塊與錯誤發生的位置太遠，則為使用者提供修正問題所需的資訊會變得更難。

### <a name="exception-class"></a>Exception 類別

例外狀況類別是例外狀況繼承來源的基類。 大部分的例外狀況物件都是例外狀況類別之某些衍生類別的實例，例如 `SystemException` 類別、`IndexOutOfRangeException` 類別或 `ArgumentNullException` 類別。 Exception 類別具有屬性，例如 `StackTrace` 屬性、`InnerException` 屬性和 `Message` 屬性，可提供有關所發生錯誤的特定資訊。

### <a name="exception-inheritance-hierarchy"></a>例外狀況繼承階層架構

執行時間具有一組基底例外狀況，衍生自在遇到例外狀況時，執行時間擲回的 `SystemException` 類別。 大部分繼承自例外狀況類別（例如 `IndexOutOfRangeException` 類別和 `ArgumentNullException` 類別）的類別，都不會執行其他成員。 因此，例外狀況的最重要資訊可以在例外狀況階層、例外狀況名稱和例外狀況中包含的資訊中找到。

### <a name="exception-handling-hierarchy"></a>例外狀況處理階層架構

在 ASP.NET Web Forms 應用程式中，可以根據特定的處理階層來處理例外狀況。 例外狀況可以在下列層級處理：

- 應用程式層級
- 分頁層級
- 程式碼層級

當應用程式處理例外狀況時，通常會抓取並向使用者顯示繼承自例外狀況類別的例外狀況的其他資訊。 除了應用程式、頁面和程式碼層級之外，您也可以使用 IIS 自訂處理常式來處理 HTTP 模組層級的例外狀況。

### <a name="application-level-error-handling"></a>應用層級錯誤處理

您可以藉由修改應用程式的設定，或在應用程式的*global.asax*檔案中新增 `Application_Error` 處理常式，在應用層級處理預設錯誤。

您可以藉由將 `customErrors` 區段加入至*web.config*檔案，來處理預設錯誤和 HTTP 錯誤。 [`customErrors`] 區段可讓您指定在發生錯誤時，使用者將被重新導向至的預設頁面。 它也可讓您指定特定狀態碼錯誤的個別頁面。

[!code-xml[Main](aspnet-error-handling/samples/sample1.xml?highlight=3-5)]

可惜的是，當您使用設定將使用者重新導向至不同的頁面時，您沒有發生之錯誤的詳細資料。

不過，您可以藉由將程式碼加入至*global.asax*檔案中的 `Application_Error` 處理常式，來將發生在應用程式任何位置的錯誤設為陷阱。

[!code-csharp[Main](aspnet-error-handling/samples/sample2.cs)]

### <a name="page-level-error-event-handling"></a>頁面層級錯誤事件處理

頁面層級處理常式會將使用者傳回發生錯誤的頁面，但因為不會維護控制項的實例，所以頁面上不會再有任何專案。 若要將錯誤詳細資料提供給應用程式的使用者，您必須特別將錯誤詳細資料寫入至頁面。

您通常會使用頁面層級錯誤處理常式來記錄未處理的錯誤，或將使用者帶到可以顯示有用資訊的頁面。

這個程式碼範例會顯示 ASP.NET 網頁中錯誤事件的處理常式。 這個處理常式會在頁面中的 `try`/`catch` 區塊內，捕捉所有尚未處理的例外狀況。

[!code-csharp[Main](aspnet-error-handling/samples/sample3.cs)]

處理錯誤之後，您必須藉由呼叫伺服器物件的 `ClearError` 方法（`HttpServerUtility` 類別）來清除它，否則會看到先前發生的錯誤。

### <a name="code-level-error-handling"></a>程式碼層級錯誤處理

Try-catch 語句是由 try 區塊後面接著一個或多個 catch 子句所組成，這會指定不同例外狀況的處理常式。 當擲回例外狀況時，common language runtime （CLR）會尋找處理此例外狀況的 catch 語句。 如果目前執行的方法不包含 catch 區塊，則 CLR 會查看呼叫目前方法的方法，依此類推，然後再向上呼叫堆疊。 如果找不到任何 catch 區塊，則 CLR 會向使用者顯示未處理的例外狀況訊息，並停止執行程式。

下列程式碼範例顯示使用 `try`/`catch`/`finally` 來處理錯誤的常見方式。

[!code-csharp[Main](aspnet-error-handling/samples/sample4.cs)]

在上述程式碼中，try 區塊包含需要針對可能的例外狀況進行防護的程式碼。 會執行區塊，直到擲回例外狀況或成功完成區塊為止。 如果發生 `FileNotFoundException` 例外狀況或 `IOException` 例外狀況，則會將執行轉移至不同的頁面。 然後，就會執行包含在 finally 區塊中的程式碼，不論是否發生錯誤。

## <a name="adding-error-logging-support"></a>新增錯誤記錄支援

將錯誤處理新增至 Wingtip 玩具範例應用程式之前，您會將 `ExceptionUtility` 類別新增至*邏輯*資料夾，以新增錯誤記錄支援。 如此一來，每次應用程式處理錯誤時，錯誤詳細資料就會新增至錯誤記錄檔。

1. 以滑鼠右鍵按一下*邏輯*資料夾，**然後選取 [** 新增 -&gt;**新專案**]。   
   隨即顯示 [ 新增項目] 對話方塊。
2. 選取左側的 [ **Visual C#**  -&gt; 程式**代碼**範本] 群組。 然後，從中間清單中選取 [**類別**]，並將其命名為**ExceptionUtility.cs**。
3. 選擇 [新增]。 隨即顯示新的類別檔案。
4. 將現有的程式碼取代為下列程式碼：  

    [!code-csharp[Main](aspnet-error-handling/samples/sample5.cs)]

發生例外狀況時，可以藉由呼叫 `LogException` 方法，將例外狀況寫入例外狀況記錄檔。 這個方法會採用兩個參數，也就是 exception 物件和包含例外狀況來源之詳細資料的字串。 例外狀況記錄檔會寫入*應用程式\_Data*資料夾中的錯誤記錄檔 *.txt*檔案。

### <a name="adding-an-error-page"></a>新增錯誤頁面

在 Wingtip 玩具範例應用程式中，會使用一個頁面來顯示錯誤。 錯誤頁面的設計，是為了向網站的使用者顯示安全錯誤訊息。 不過，如果使用者是發出 HTTP 要求的開發人員，而該服務是在程式碼所在的電腦上進行本機處理，則錯誤頁面上會顯示其他錯誤詳細資料。

1. 以滑鼠右鍵按一下**方案總管**中的專案名稱（**Wingtip 玩具**），**然後選取 [** 新增 -&gt;**新專案**]。   
   隨即顯示 [ 新增項目] 對話方塊。
2. 選取左側的 [ **Visual C#**  -&gt; **Web**範本] 群組。 從中間清單中，選取 [**使用主版頁面的 Web 表單**]，並將它命名為**ErrorPage .aspx**。
3. 按一下 [新增]。
4. 選取*網站*檔案作為主版頁面，然後選擇 **[確定]** 。
5. 以下列內容取代現有的標記：   

    [!code-aspx[Main](aspnet-error-handling/samples/sample6.aspx)]
6. 取代程式碼後置（*ErrorPage.aspx.cs*）的現有程式碼，使其看起來如下所示：   

    [!code-csharp[Main](aspnet-error-handling/samples/sample7.cs)]

顯示錯誤頁面時，會執行 `Page_Load` 事件處理常式。 在 `Page_Load` 處理常式中，會決定第一次處理錯誤的位置。 然後，最後發生的錯誤是藉由呼叫伺服器物件的 `GetLastError` 方法來決定。 如果例外狀況已不存在，則會建立一般例外狀況。 然後，如果 HTTP 要求是在本機提出，則會顯示所有錯誤詳細資料。 在此情況下，只有執行 web 應用程式的本機電腦會看到這些錯誤詳細資料。 顯示錯誤資訊之後，會將錯誤新增至記錄檔，並從伺服器中清除錯誤。

### <a name="displaying-unhandled-error-messages-for-the-application"></a>顯示應用程式的未處理錯誤訊息

藉由將 `customErrors` 區段新增至*web.config 檔案*，您可以快速處理整個應用程式中發生的簡單錯誤。 您也可以根據狀態碼值來指定如何處理錯誤，例如 404-找不到檔案。

#### <a name="update-the-configuration"></a>更新設定

將 `customErrors` 區段新增*至 web.config 檔案*，以更新設定。

1. 在**方案總管**中，尋找並開啟位於 Wingtip 玩具範例應用程式根目錄的*web.config*檔案。
2. 將 `customErrors` 區段新增至 [`<system.web>`] 節點*內的 web.config*檔案，如下所示：   

    [!code-xml[Main](aspnet-error-handling/samples/sample8.xml?highlight=3-5)]
3. 儲存 *Web.config* 檔案。

`customErrors` 區段會指定模式，其設定為 "On"。 它也會指定 `defaultRedirect`，這會告訴應用程式在發生錯誤時要流覽的頁面。 此外，您還加入了特定的錯誤元素，指定當找不到頁面時，如何處理404錯誤。 稍後在本教學課程中，您將會新增其他錯誤處理，以在應用層級上捕捉錯誤的詳細資料。

#### <a name="running-the-application"></a>執行應用程式

您可以立即執行應用程式，以查看更新的路由。

1. 按**F5**執行 Wingtip 玩具範例應用程式。  
 瀏覽器會開啟並顯示*default.aspx*頁面。
2. 在瀏覽器中輸入下列 URL （請務必使用**您**的埠號碼）：  
    `https://localhost:44300/NoPage.aspx`
3. 檢查瀏覽器中顯示的*ErrorPage* 。 

    ![ASP.NET 錯誤處理-找不到分頁錯誤](aspnet-error-handling/_static/image1.png)

當您要求的*NoPage*不存在時，錯誤頁面會顯示簡單的錯誤訊息，以及詳細的錯誤資訊（如果有其他詳細資料可用）。 不過，如果使用者從遠端位置要求不存在的頁面，則錯誤頁面只會以紅色顯示錯誤訊息。

### <a name="including-an-exception-for-testing-purposes"></a>包含測試用途的例外狀況

若要驗證您的應用程式在發生錯誤時的運作方式，您可以故意在 ASP.NET 中建立錯誤狀況。 在 Wingtip 玩具範例應用程式中，當預設頁面載入時，您將會擲回測試例外狀況，以查看發生什麼情況。

1. 在 Visual Studio 中開啟*default.aspx*頁面的程式碼後置。   
   *Default.aspx.cs*程式碼後置頁面隨即顯示。
2. 在 `Page_Load` 處理常式中，新增程式碼，讓處理常式看起來如下：   

    [!code-csharp[Main](aspnet-error-handling/samples/sample9.cs?highlight=3-4)]

您可以建立各種不同類型的例外狀況。 在上述程式碼中，您會在載入*default.aspx*頁面時建立 `InvalidOperationException`。

#### <a name="running-the-application"></a>執行應用程式

您可以執行應用程式，以查看應用程式處理例外狀況的方式。

1. 按**CTRL + F5**執行 Wingtip 玩具範例應用程式。  
 應用程式會擲回 InvalidOperationException。 

    > [!NOTE] 
    > 
    > 您必須按**CTRL + F5**以顯示頁面，而不會中斷程式碼，以在 Visual Studio 中查看錯誤的來源。
2. 檢查瀏覽器中顯示的*ErrorPage* 。 

    ![ASP.NET 錯誤處理-錯誤頁面](aspnet-error-handling/_static/image2.png)

如您在錯誤詳細資料中所見， *web.config*檔案中的 `customError` 區段會攔截例外狀況。

### <a name="adding-application-level-error-handling"></a>加入應用層級的錯誤處理

不是*使用 web.config 檔案*中的 `customErrors` 區段來攔截例外狀況，您可以在其中取得例外狀況的少量資訊，並在應用層級攔截錯誤並取得錯誤詳細資料。

1. 在**方案總管**中，尋找並開啟*Global.asax.cs*檔案。
2. 新增**應用程式\_錯誤**處理常式，使其看起來如下所示：   

    [!code-csharp[Main](aspnet-error-handling/samples/sample10.cs)]

當應用程式中發生錯誤時，會呼叫 `Application_Error` 處理常式。 在此處理程式中，會抓取並審核最後一個例外狀況。 如果例外狀況未處理，且例外狀況包含內部例外狀況詳細資料（也就是 `InnerException` 不是 null），應用程式就會將執行轉移至顯示例外狀況詳細資料的錯誤頁面。

#### <a name="running-the-application"></a>執行應用程式

您可以執行應用程式，以查看在應用層級處理例外狀況所提供的其他錯誤詳細資料。

1. 按**CTRL + F5**執行 Wingtip 玩具範例應用程式。  
 應用程式會擲回 `InvalidOperationException`。
2. 檢查瀏覽器中顯示的*ErrorPage* 。 

    ![ASP.NET 錯誤處理-應用層級錯誤](aspnet-error-handling/_static/image3.png)

### <a name="adding-page-level-error-handling"></a>加入頁面層級錯誤處理

您可以將頁面層級錯誤處理加入頁面中，方法是使用將 `ErrorPage` 屬性加入至頁面的 `@Page` 指示詞，或將 `Page_Error` 事件處理常式加入至頁面的程式碼後置。 在本節中，您將會新增 `Page_Error` 事件處理常式，以將執行傳送至*ErrorPage .aspx*頁面。

1. 在**方案總管**中，尋找並開啟*Default.aspx.cs*檔案。
2. 新增 `Page_Error` 處理常式，讓程式碼後置顯示如下：   

    [!code-csharp[Main](aspnet-error-handling/samples/sample11.cs?highlight=18-30)]

當頁面上發生錯誤時，會呼叫 `Page_Error` 事件處理常式。 在此處理程式中，會抓取並審核最後一個例外狀況。 如果發生 `InvalidOperationException`，`Page_Error` 事件處理常式會將執行傳送至顯示例外狀況詳細資料的錯誤頁面。

#### <a name="running-the-application"></a>執行應用程式

您可以立即執行應用程式，以查看更新的路由。

1. 按**CTRL + F5**執行 Wingtip 玩具範例應用程式。  
 應用程式會擲回 `InvalidOperationException`。
2. 檢查瀏覽器中顯示的*ErrorPage* 。 

    ![ASP.NET 錯誤處理-頁面層級錯誤](aspnet-error-handling/_static/image4.png)
3. 關閉瀏覽器視窗。

### <a name="removing-the-exception-used-for-testing"></a>移除用於測試的例外狀況

若要允許 Wingtip 玩具範例應用程式正常運作，而不擲回您稍早在本教學課程中新增的例外狀況，請移除例外狀況。

1. 開啟*default.aspx*頁面的程式碼後置。
2. 在 `Page_Load` 處理常式中，移除擲回例外狀況的程式碼，讓處理常式看起來如下：   

    [!code-csharp[Main](aspnet-error-handling/samples/sample12.cs)]

### <a name="adding-code-level-error-logging"></a>加入程式碼層級錯誤記錄

如本教學課程稍早所述，您可以加入 try/catch 語句來嘗試執行程式碼區段，並處理第一個發生的錯誤。 在此範例中，您只會將錯誤詳細資料寫入錯誤記錄檔中，以便稍後可以檢查錯誤。

1. 在**方案總管**的*邏輯*資料夾中，尋找並開啟*PayPalFunctions.cs*檔案。
2. 更新 `HttpCall` 方法，讓程式碼看起來如下所示：   

    [!code-csharp[Main](aspnet-error-handling/samples/sample13.cs?highlight=20,22-23)]

上述程式碼會呼叫包含在 `ExceptionUtility` 類別中的 `LogException` 方法。 您已將*ExceptionUtility.cs*類別檔案新增至本教學課程稍早的*邏輯*資料夾。 `LogException` 方法會接受兩個參數。 第一個參數是例外狀況物件。 第二個參數是用來辨識錯誤來源的字串。

### <a name="inspecting-the-error-logging-information"></a>檢查錯誤記錄資訊

如先前所述，您可以使用錯誤記錄檔來判斷應該先修正應用程式中的哪些錯誤。 當然，只會記錄已被攔截並寫入錯誤記錄檔的錯誤。

1. 在**方案總管**中，尋找並開啟*應用程式\_Data*資料夾中的錯誤記錄檔 *.txt*檔案。   
 您可能需要從 [**方案總管**] 頂端選取 [**顯示所有**檔案] 選項或 [重新**整理] 選項**，才能查看錯誤記錄檔 *.txt*檔案。
2. 檢查 Visual Studio 中顯示的錯誤記錄檔： 

    ![ASP.NET 錯誤處理-錯誤記錄檔 .txt](aspnet-error-handling/_static/image5.png)

### <a name="safe-error-messages"></a>安全錯誤訊息

**請務必注意**，當您的應用程式顯示錯誤訊息時，應該不會提供惡意使用者在攻擊您的應用程式時可能會有説明的資訊。 例如，如果您的應用程式未成功地嘗試寫入資料庫，則不應該顯示包含所使用之使用者名稱的錯誤訊息。 因此，使用者會看到紅色的一般錯誤訊息。 所有其他錯誤詳細資料只會對本機電腦上的開發人員顯示。

## <a name="using-elmah"></a>使用 ELMAH

ELMAH （錯誤記錄模組和處理常式）是一種錯誤記錄工具，您可以將 ASP.NET 應用程式插入為 NuGet 套件。 ELMAH 提供下列功能：

- 記錄未處理的例外狀況。
- 用來查看重新編碼未處理之例外狀況之完整記錄的網頁。
- 用來查看每個已記錄例外狀況之完整詳細資料的網頁。
- 每次發生錯誤時的電子郵件通知。
- 記錄檔最後15個錯誤的 RSS 摘要。

在您可以使用 ELMAH 之前，您必須先安裝它。 使用*NuGet*套件安裝程式很容易。 如稍早在本教學課程系列中所述，NuGet 是 Visual Studio 延伸模組，可讓您輕鬆地安裝和更新 Visual Studio 中的開放原始碼程式庫和工具。

1. 在 Visual Studio 中，從 **工具** 功能表選取  **nuget 套件管理員**， > **管理解決方案的 nuget 套件**。 

    ![ASP.NET 錯誤處理-管理解決方案的 NuGet 套件](aspnet-error-handling/_static/image6.png)
2. [**管理 NuGet 封裝**] 對話方塊會顯示在 Visual Studio 中。
3. 在 [**管理 NuGet 封裝**] 對話方塊中，展開左側的 [**線上**]，然後選取 [ **nuget.org**]。然後，在線上可用的套件清單中，尋找並安裝**ELMAH**套件。 

    ![ASP.NET 錯誤處理-ELMA NuGet 套件](aspnet-error-handling/_static/image7.png)
4. 您將需要有網際網路連線才能下載套件。
5. 在 [**選取專案**] 對話方塊中，確認已選取**WingtipToys**選項，然後按一下 **[確定]** 。 

    ![ASP.NET 錯誤處理-[選取專案] 對話方塊](aspnet-error-handling/_static/image8.png)
6. 如有需要，請按一下 [**管理 NuGet 套件**] 對話方塊中的 [**關閉**]。
7. 如果 Visual Studio 要求您重載任何開啟的檔案，請選取 [**全部皆是**]。
8. ELMAH 封裝會在專案*根目錄的 web.config*檔案中，新增其本身的專案。 如果 Visual Studio 詢問您是否要重載已修改的*web.config*檔案，請按一下 **[是]** 。

ELMAH 現在已準備好儲存任何發生的未處理錯誤。

### <a name="viewing-the-elmah-log"></a>查看 ELMAH 記錄檔

查看 ELMAH 記錄檔很簡單，但首先您會建立一個未處理的例外狀況，並將記錄在 ELMAH 記錄檔中。

1. 按**CTRL + F5**執行 Wingtip 玩具範例應用程式。
2. 若要將未處理的例外狀況寫入 ELMAH 記錄檔，請在瀏覽器中流覽至下列 URL （使用您的埠號碼）：  
    將會顯示 [錯誤] 頁面 `https://localhost:44300/NoPage.aspx`。
3. 若要顯示 ELMAH 記錄檔，請在瀏覽器中流覽至下列 URL （使用您的埠號碼）：  
    `https://localhost:44300/elmah.axd`

    ![ASP.NET 錯誤處理-ELMAH 錯誤記錄檔](aspnet-error-handling/_static/image9.png)

## <a name="summary"></a>總結

在本教學課程中，您已瞭解如何在應用層級、頁面層級和程式碼層級處理錯誤。 您也已瞭解如何記錄已處理和未處理的錯誤，以供日後審查。 您已新增 ELMAH 公用程式，以使用 NuGet 為您的應用程式提供例外狀況記錄和通知。 此外，您也已經瞭解安全錯誤訊息的重要性。

## <a name="tutorial-series-conclusion"></a>教學課程系列結論

感謝您的關注。 我希望這組教學課程協助您更熟悉 ASP.NET Web form。 如果您需要 ASP.NET 4.5 和 Visual Studio 2013 中可用 Web form 功能的詳細資訊，請參閱[ASP.NET 和 Web 工具以取得 Visual Studio 2013 版本](../../../../visual-studio/overview/2013/release-notes.md)資訊。 此外，請務必查看**後續步驟**一節中所述的教學課程，並 defintely 試用[免費的 Azure 試用版](https://azure.microsoft.com/pricing/free-trial/)。

![感謝-Erik](aspnet-error-handling/_static/image10.png)  

## <a name="next-steps"></a>後續步驟

若要深入瞭解如何將 web 應用程式部署至 Microsoft Azure，請參閱[使用成員資格、OAuth 和 SQL Database 將安全的 ASP.NET Web Forms 應用程式部署到 Azure 網站](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)。

## <a name="free-trial"></a>免費試用

[Microsoft Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)  
 將您的網站發佈到 Microsoft Azure 可以節省您的時間、維護和費用。 這是將您的 web 應用程式部署至 Azure 的快速流程。 當您需要維護及監視 web 應用程式時，Azure 會提供各種不同的工具和服務。 管理 Azure 中的資料、流量、身分識別、備份、訊息、媒體和效能。 而且這一切都是以非常符合成本效益的方式提供。

## <a name="additional-resources"></a>其他資源

[使用 ASP.NET 健全狀況監視記錄錯誤詳細資料](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md)   
[ELMAH](https://code.google.com/p/elmah/)

## <a name="acknowledgements"></a>通知

我想感謝下列人對本教學課程系列的內容做出重大貢獻：

- [Alberto Poblacion，MVP &amp; MCT，西班牙](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- [Alex Thissen，荷蘭](http://blog.alexthissen.nl/)（twitter： [@alexthissen](http://twitter.com/alexthissen)）
- [美國 Andre Tournier](http://andret503.wordpress.com/)
- Apurva Joshi，Microsoft
- [Bojan Vrhovnik，斯洛維尼亞](http://twitter.com/bvrhovnik)
- [Bruno sonnino 此將，巴西](http://msmvps.com/blogs/bsonnino)（twitter： [@bsonnino](http://twitter.com/bsonnino)）
- [Carlos dos Santos，巴西](http://www.carloscds.net/)
- [美國 Dave Campbell](http://www.wynapse.com/) （twitter： [@windowsdevnews](http://twitter.com/windowsdevnews)）
- [Jon Galloway，Microsoft](https://weblogs.asp.net/jgalloway) （twitter： [@jongalloway](http://twitter.com/jongalloway)）
- 美國（twitter： [@mrsharps](http://twitter.com/mrsharps)） [Michael Sharps](http://www.930solutions.com/)
- Mike Pope
- [美國 Mitchel 賣方](http://www.mitchelsellers.com/)（twitter： [@MitchelSellers](http://twitter.com/MitchelSellers)）
- [Paul Cociuba，Microsoft](http://linqto.me/Links/pcociuba)
- [聖保羅 Morgado，葡萄牙](http://paulomorgado.net/)
- [Pranav 請參閱 rastogi，Microsoft](https://blogs.msdn.com/b/pranav_rastogi)
- [Tim Ammann，Microsoft](https://blogs.iis.net/timamm/default.aspx)
- [Tom 作者: dykstra，Microsoft](https://blogs.msdn.com/aspnetue)

## <a name="community-contributions"></a>社群貢獻

- Graham Mendick （[@grahammendick](http://twitter.com/grahammendick)）  
  MSDN 上 Visual Studio 2012 相關程式碼範例：[導覽 Wingtip 玩具](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)
- James Chaney （[jchaney@agvance.net](mailto:jchaney@agvance.net)）  
  MSDN 上的 Visual Studio 2012 相關程式碼範例： [Visual Basic 中的 ASP.NET 4.5 Web Forms 教學課程系列](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)
- Andrielle Azevedo-Microsoft 技術物件參與者（twitter： @driazevedo）  
  Visual Studio 2012 轉譯： [Iniciando com ASP.NET Web Forms 4.5-Parte 1-Introdução e Visão Geral](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)

> [!div class="step-by-step"]
> [上一篇](url-routing.md)
