---
uid: web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
title: 針對 ASP.NET Web Pages （Razor）網站自訂全網站行為 |Microsoft Docs
author: Rick-Anderson
description: 本章說明如何將設定設為整個網站或整個資料夾，而不只是頁面。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: e158bed7-226f-4275-b02e-7553bd58c669
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
msc.type: authoredcontent
ms.openlocfilehash: f05e05f725d9209bce283ce18659ae5efe4de2ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634621"
---
# <a name="customizing-site-wide-behavior-for-aspnet-web-pages-razor-sites"></a>針對 ASP.NET Web Pages （Razor）網站自訂全網站行為

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明如何在 ASP.NET Web Pages （Razor）網站中建立頁面的網站端設定。
> 
> 您將學到什麼：
> 
> - 如何執行程式碼，讓您設定網站中所有頁面的值（全域值或 helper 設定）。
> - 如何執行程式碼，讓您設定資料夾中所有頁面的值。
> - 如何在頁面載入之前和之後執行程式碼。
> - 如何將錯誤傳送至中央錯誤頁面。
> - 如何將驗證新增至資料夾中的所有頁面。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）2
> - WebMatrix 3
> - ASP.NET Web helper 程式庫（NuGet 套件）
>   
> 
> 本教學課程也適用于 ASP.NET Web Pages 3 和 Visual Studio 2013 （或 Visual Studio Express 2013 for Web），不同之處在于您無法使用 ASP.NET Web helper 程式庫。

<a id="Adding_Website_Startup_Code"></a>
## <a name="adding-website-startup-code-for-aspnet-web-pages"></a>新增 ASP.NET Web Pages 的網站啟動程式碼

針對您在 ASP.NET Web Pages 中撰寫的大部分程式碼，個別頁面可以包含該頁面所需的所有程式碼。 例如，如果頁面傳送電子郵件訊息，則可以將該作業的所有程式碼放在單一頁面中。 這可包含程式碼，以初始化傳送電子郵件（也就是 SMTP 伺服器）的設定，以及傳送電子郵件訊息。

不過，在某些情況下，您可能會想要在網站上的任何頁面執行之前執行一些程式碼。 這適用于設定可在網站任何地方使用的值（稱為「*全域值*」）。例如，某些協助程式會要求您提供電子郵件設定或帳戶金鑰之類的值。 將這些設定保留在全域值中是很方便的。

若要這麼做，您可以在網站的根目錄中建立名為 *\_AppStart*的頁面。 如果此頁面存在，則會在第一次要求網站中的任何頁面時執行。 因此，它是執行程式碼以設定全域值的好地方。 （因為 *\_AppStart*的底線前置詞，ASP.NET 不會將頁面傳送至瀏覽器，即使使用者直接要求也一樣）。

下圖顯示 [ *\_AppStart* ] 頁面的運作方式。 當要求傳入頁面時，如果這是網站中任何頁面的第一個要求，ASP.NET 會先檢查是否有 *\_AppStart. cshtml*頁面存在。 若是如此， *\_AppStart*中的任何程式碼都會執行，然後再執行要求的頁面。

![[影像]](18-customizing-site-wide-behavior/_static/image1.jpg)

## <a name="setting-global-values-for-your-website"></a>為您的網站設定全域值

1. 在 WebMatrix 網站的根資料夾中，建立名為 *\_AppStart*的檔案。 檔案必須位於網站的根目錄中。
2. 以下列內容取代現有的內容： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample1.cshtml)]

    此程式碼會將值儲存在 `AppState` 字典中，這會自動提供給網站中的所有頁面。 請注意， *\_AppStart*檔案中沒有任何標記。 頁面將會執行程式碼，然後重新導向至原先要求的頁面。

    > [!NOTE]
    > 當您將程式碼放在 *\_AppStart*檔時，請務必小心。 如果 *\_AppStart*檔的程式碼中發生任何錯誤，網站就不會啟動。
3. 在根資料夾中，建立名為*AppName. cshtml*的新頁面。
4. 將預設標記和程式碼取代為下列內容： 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample2.html)]

    此程式碼會從您在 [ *\_AppStart* ] 頁面中設定的 `AppState` 物件中，提取值。
5. 在瀏覽器中執行*AppName. cshtml*頁面。 （在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）此頁面會顯示全域值。 

    ![[影像]](18-customizing-site-wide-behavior/_static/image2.jpg)

<a id="Setting_Values_For_Helpers"></a>
## <a name="setting-values-for-helpers"></a>設定 helper 的值

*\_AppStart*的好用，就是為您在網站中使用且必須初始化的 helper 設定值。 一般範例包括 `WebMail` helper 的電子郵件設定，以及 `ReCaptcha` 協助程式的私用和公開金鑰。 在這種情況下，您可以在 *\_AppStart*中設定值一次，然後在您的網站中為所有頁面設定它們。

此程式說明如何全域設定 `WebMail` 設定。 （如需有關使用 `WebMail` 協助程式的詳細資訊，請參閱[將電子郵件新增至 ASP.NET Web Pages 網站](../getting-started/11-adding-email-to-your-web-site.md)）。

1. 如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果尚未新增）。
2. 如果您還沒有 *\_AppStart. cshtml*檔案，請在網站的根資料夾中建立名為 *\_AppStart*的檔案。
3. 將下列 `WebMail` 設定新增至 *\_AppStart. cshtml*檔案： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample3.cshtml?highlight=2-7)]

    修改程式碼中的下列電子郵件相關設定：

   - 將 `your-SMTP-host` 設定為您可以存取的 SMTP 伺服器名稱。
   - 將 `your-user-name-here` 設定為 SMTP 伺服器帳戶的使用者名稱。
   - 將 `your-account-password` 設定為 SMTP 伺服器帳戶的密碼。
   - 將 `your-email-address-here` 設定為您自己的電子郵件地址。 這是傳送訊息的來源電子郵件地址。 （有些電子郵件提供者不會讓您指定不同的 `From` 位址，而且會使用您的使用者名稱作為 `From` 位址）。

     如需 SMTP 設定的詳細資訊，請參閱在[ASP.NET Web Pages （razor）疑難排解指南](https://go.microsoft.com/fwlink/?LinkId=253001)中[從 ASP.NET Web Pages （razor）網站傳送電子郵件](https://go.microsoft.com/fwlink/?LinkID=202899)和傳送電子郵件的[問題](https://go.microsoft.com/fwlink/?LinkId=253001#email)一文中的[設定電子郵件設定](https://go.microsoft.com/fwlink/?LinkID=202899#configuring_email_settings)。
4. 儲存 *\_AppStart* ，並將它關閉。
5. 在網站的根資料夾中，建立名為*TestEmail*的新頁面。
6. 以下列內容取代現有的內容： 

     [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample4.cshtml)]
7. 在瀏覽器中執行*TestEmail。*
8. 填寫欄位將電子郵件傳送給自己，然後按一下 [**傳送**]。
9. 請檢查您的電子郵件，以確定您已取得該訊息。

這個範例的重要部分是，您通常不會變更的設定（例如 SMTP 伺服器的名稱和電子郵件認證）會在 *\_AppStart. cshtml*檔案中設定。 如此一來，您就不需要在傳送電子郵件的每一頁中重新設定這些專案。 （不過，如果基於某些原因而需要變更這些設定，您可以在頁面中個別加以設定）。在此頁面中，您只會設定通常會每次變更的值，例如收件者和電子郵件訊息的主體。

<a id="Running_Code_Before_and_After"></a>
## <a name="running-code-before-and-after-files-in-a-folder"></a>在資料夾中的檔案前後執行程式碼

就像您可以在網站執行的頁面之前，使用 *\_AppStart*來撰寫程式碼，您可以撰寫在執行特定資料夾中的任何頁面之前（和之後）執行的程式碼。 這適用于針對資料夾中的所有頁面設定相同的版面配置頁，或在執行資料夾中的頁面之前，檢查使用者是否已登入的專案。

針對特定資料夾中的頁面，您可以在名為 *\_PageStart*的檔案中建立程式碼。 下圖顯示 [ *\_PageStart* ] 頁面的運作方式。 當頁面出現要求時，ASP.NET 會先檢查 *\_的 AppStart* ，然後執行該頁面。 然後，ASP.NET 會檢查是否有 *\_PageStart* ，如果是，則會執行該頁面。 然後，它會執行要求的頁面。

在 *\_PageStart*  頁面中，您可以藉由包含 `RunPage` 方法，指定要在處理期間執行要求的頁面。 這可讓您先執行程式碼，然後再執行要求的頁面，然後再進行一次。 如果您未包含 `RunPage`， *\_PageStart*中的所有程式碼都會執行，然後要求的網頁會自動執行。

![[影像]](18-customizing-site-wide-behavior/_static/image3.jpg)

ASP.NET 可讓您建立 *\_PageStart*的階層。 您可以將 *\_PageStart*放在網站根目錄和任何子資料夾中。 當要求頁面時，\_在最上層的位置（最接近網站根目錄）執行的*PageStart*檔案，後面接著下一個子資料夾中的 *\_PageStart*檔，然後關閉子資料夾結構，直到要求到達包含所要求頁面的資料夾為止。 當所有適用的 *\_PageStart*檔案都已執行之後，要求的頁面就會執行。

例如，您可能會有下列 *\_PageStart*的組合，以及*預設的 cshtml*檔案：

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample5.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample6.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample7.cshtml)]

當您執行 */myfolder/default.cshtml*時，您會看到下列內容：

[!code-console[Main](18-customizing-site-wide-behavior/samples/sample8.cmd)]

## <a name="running-initialization-code-for-all-pages-in-a-folder"></a>針對資料夾中的所有頁面執行初始化程式碼

*\_PageStart*的良好用法是針對單一資料夾中的所有檔案，初始化相同的版面配置頁。

1. 在根資料夾中，建立名為*InitPages*的新資料夾。
2. 在網站的 [ *InitPages* ] 資料夾中，建立名為 *\_PageStart*的檔案，並將預設標記和程式碼取代為下列內容： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample9.cshtml)]
3. 在網站的根目錄中，建立名為*Shared*的資料夾。
4. 在*共用*資料夾中，建立名為 *\_layout1.xml*的檔案，並將預設標記和程式碼取代為下列內容： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample10.cshtml)]
5. 在*InitPages*資料夾中，建立名為*Content1*的檔案，並以下列內容取代現有的內容： 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample11.html)]
6. 在*InitPages*資料夾中，建立另一個名為*Content2*的檔案，並將預設標記取代為下列內容： 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample12.html)]
7. 在瀏覽器中執行*Content1。* 

    ![[影像]](18-customizing-site-wide-behavior/_static/image4.jpg)

    當*Content1*在執行時，會 `Layout` 設定 *\_的 PageStart* ，同時將 `PageData["MyBackground"]` 設定為色彩。 在*Content1*中，會套用版面配置和色彩。
8. 在瀏覽器中顯示*Content2* 。 

    版面配置相同，因為這兩個頁面都會使用與 *\_PageStart*中初始化的相同版面配置頁和色彩。

## <a name="using-_pagestartcshtml-to-handle-errors"></a>使用 \_PageStart 來處理錯誤

*\_PageStart*的另一個好用方法，就是建立一個方式來處理資料夾中任何 *. cshtml*頁面可能發生的程式設計錯誤（例外狀況）。 這個範例會示範一種執行此動作的方式。

1. 在根資料夾中，建立名為*InitCatch*的資料夾。
2. 在網站的*InitCatch*資料夾中，建立名為 *\_PageStart*的檔案，並將現有的標記和程式碼取代為下列內容： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample13.cshtml)]

    在此程式碼中，您會藉由呼叫 `try` 區塊內的 `RunPage` 方法，來嘗試明確執行要求的頁面。 如果要求的頁面中發生任何程式設計錯誤，`catch` 區塊內的程式碼就會執行。 在此情況下，程式碼會重新導向至頁面（*錯誤. cshtml*），並將發生錯誤的檔案名傳遞為 URL 的一部分。 （您很快就會建立此頁面）。
3. 在您網站的*InitCatch*資料夾中，建立名為*Exception. cshtml*的檔案，並將現有的標記和程式碼取代為下列內容： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample14.cshtml)]

    基於此範例的目的，您在此頁面中執行的動作，是藉由嘗試開啟不存在的資料庫檔案，而故意建立錯誤。
4. 在根資料夾中，建立名為*Error*的檔案，並將現有的標記和程式碼取代為下列內容： 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample15.html)]

    在此頁面中，運算式 `@Request["source"]` 會從 URL 取得值，並加以顯示。
5. 在工具列中，按一下 [**儲存**]。
6. 在瀏覽器中執行*Exception. cshtml* 。 

    ![[影像]](18-customizing-site-wide-behavior/_static/image5.jpg)

    因為在*Exception. cshtml*中發生錯誤， *\_PageStart*會重新導向至*錯誤的 cshtml*檔案，該檔案會顯示訊息。

    如需例外狀況的詳細資訊，請參閱[使用 Razor 語法進行 ASP.NET Web Pages 程式設計的簡介](https://go.microsoft.com/fwlink/?LinkID=251587)。

<a id="Using__PageStart.cshtml_to_Restrict_Folder_Access"></a>
## <a name="using-_pagestartcshtml-to-restrict-folder-access"></a>使用 \_PageStart 來限制資料夾存取

您也可以使用 *\_PageStart*檔來限制資料夾中所有檔案的存取權。

1. 在 WebMatrix 中，使用 [**來自範本的網站**] 選項建立新的網站。
2. 從可用的範本中，選取 [**入門網站**]。
3. 在根資料夾中，建立名為*AuthenticatedContent*的資料夾。
4. 在*AuthenticatedContent*資料夾中，建立名為 *\_PageStart*的檔案，並將現有的標記和程式碼取代為下列內容： 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample16.cshtml)]

    程式碼一開始會防止快取資料夾中的所有檔案。 （這是公用電腦等案例的必要項，您不想讓使用者的快取頁面供下一位使用者使用）。接下來，程式碼會判斷使用者是否已登入網站，然後才能查看資料夾中的任何頁面。 如果使用者未登入，則程式碼會重新導向至登入頁面。 如果您包含名為 `ReturnUrl`的查詢字串值，登入頁面可以將使用者傳回原先要求的頁面。
5. 在*AuthenticatedContent*資料夾中建立名為*page. cshtml*的新頁面。
6. 將預設標記取代為下列內容：  

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample17.cshtml)]
7. 在瀏覽器中執行 *. cshtml* 。 此程式碼會將您重新導向至登入頁面。 在登入之前，您必須先註冊。 註冊並登入之後，您可以流覽至頁面並查看其內容。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他資源

[使用 Razor 語法進行 ASP.NET Web Pages 程式設計的簡介](https://go.microsoft.com/fwlink/?LinkID=251587)
