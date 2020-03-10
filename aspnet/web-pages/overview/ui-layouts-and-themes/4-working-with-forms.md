---
uid: web-pages/overview/ui-layouts-and-themes/4-working-with-forms
title: 在 ASP.NET Web Pages （Razor）網站中使用 HTML 表單 |Microsoft Docs
author: Rick-Anderson
description: 表單是 HTML 檔案的一個區段，您可以在其中放置使用者輸入控制項，例如文字方塊、核取方塊、選項按鈕和下拉式清單。 您可以使用表單 wh 。
ms.author: riande
ms.date: 02/10/2014
ms.assetid: f3f4b8c8-e8f6-4474-ad94-69228a6c01ee
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/4-working-with-forms
msc.type: authoredcontent
ms.openlocfilehash: c7d4802063c8610a246afe67bd15eea429f7304a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639703"
---
# <a name="working-with-html-forms-in-aspnet-web-pages-razor-sites"></a>在 ASP.NET Web Pages （Razor）網站中使用 HTML 表單

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明當您在 ASP.NET Web Pages （Razor）網站中工作時，如何處理 HTML 表單（使用文字方塊和按鈕）。
> 
> **您將瞭解的內容：** 
> 
> - 如何建立 HTML 表單。
> - 如何從表單讀取使用者輸入。
> - 如何驗證使用者輸入。
> - 如何在提交頁面之後還原表單值。
> 
> 以下是文章中引進的 ASP.NET 程式設計概念：
> 
> - `Request` 物件。
> - 輸入驗證。
> - HTML 編碼。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）3
>   
> 
> 本教學課程也適用于 ASP.NET Web Pages 2。

## <a name="creating-a-simple-html-form"></a>建立簡單的 HTML 表單

1. 建立新的網站。
2. 在根資料夾中，建立名為*Form. cshtml*的網頁，並輸入下列標記：

    [!code-html[Main](4-working-with-forms/samples/sample1.html)]
3. 在您的瀏覽器中啟動頁面。 （在 WebMatrix 的 [檔案 **] 工作區**中，以滑鼠右鍵按一下檔案，然後選取 [**在瀏覽器中啟動**]。）其中會顯示具有三個輸入欄位和 [**提交**] 按鈕的簡單表單。

    ![具有三個文字方塊的表單螢幕擷取畫面。](4-working-with-forms/_static/image1.png)

    此時，如果您按一下 [**提交**] 按鈕，就不會發生任何事。 若要讓表單有用，您必須新增一些將在伺服器上執行的程式碼。

## <a name="reading-user-input-from-the-form"></a>讀取表單中的使用者輸入

若要處理表單，您可以加入程式碼來讀取已提交的域值，並對它們執行一些作業。 此程式說明如何讀取欄位，並在頁面上顯示使用者輸入。 （在生產應用程式中，您通常會使用使用者輸入來執行更有趣的事情。 您會在有關使用資料庫的文章中執行此動作）。

1. 在*表單 cshtml*檔案的頂端，輸入下列程式碼：

    [!code-cshtml[Main](4-working-with-forms/samples/sample2.cshtml)]

    當使用者第一次要求頁面時，只會顯示空白表單。 使用者（也就是您）填滿表單，然後按一下 [**提交**]。 這會將使用者輸入提交（張貼）到伺服器。 根據預設，要求會移至相同的頁面（也就是*表單. cshtml*）。

    當您這次提交頁面時，您輸入的值會顯示在表單的正上方：

    ![顯示您已輸入的值顯示在頁面上的螢幕擷取畫面。](4-working-with-forms/_static/image2.png)

    查看頁面的程式碼。 您會先使用 `IsPost` 方法來判斷頁面是否正在張貼&#8212; ，也就是使用者是否按下 [**提交**] 按鈕。 如果這是 post，`IsPost` 會傳回 true。 這是 ASP.NET Web Pages 中的標準方式，可決定您是使用初始要求（GET 要求）還是回傳（POST 要求）。 （如需 GET 和 POST 的詳細資訊，請參閱[使用 Razor 語法的 ASP.NET Web Pages 程式設計簡介](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost)中的「HTTP GET 和 Post 和 IsPost 屬性」提要欄位）。

    接下來，您會取得使用者從 `Request.Form` 物件填入的值，並將它們放在變數中以供日後查看。 `Request.Form` 物件包含所有以頁面提交的值，每個都是由索引鍵所識別。 索引鍵等同于您想要讀取之表單欄位的 `name` 屬性。 例如，若要讀取 `companyname` 欄位（文字方塊），您可以使用 `Request.Form["companyname"]`。

    表單值會以字串形式儲存在 `Request.Form` 物件中。 因此，當您必須使用值做為數位或日期或其他類型時，您必須將它從字串轉換為該類型。 在此範例中，`Request.Form` 的 `AsInt` 方法是用來將 employees 欄位的值（包含員工計數）轉換成整數。
2. 在您的瀏覽器中啟動頁面，填寫表單欄位，然後按一下 [**提交**]。 此頁面會顯示您所輸入的值。

> [!TIP] 
> 
> <a id="SB_HTMLEncoding"></a>
> ### <a name="html-encoding-for-appearance-and-security"></a>外觀和安全性的 HTML 編碼方式
> 
> HTML 對 `<`、`>`和 `&`等字元具有特殊用途。 如果這些特殊字元出現在非預期的位置，則可能會破壞網頁的外觀和功能。 例如，瀏覽器會將 `<` 字元（除非後面接著空格）解讀為 HTML 元素的開頭，例如 `<b>` 或 `<input ...>`。 如果瀏覽器無法辨識元素，它就會捨棄開頭為 `<` 的字串，直到到達它可再次辨識的內容。 很明顯地，這可能會導致頁面中出現一些奇怪的呈現。
> 
> HTML 編碼會以瀏覽器解讀為正確符號的程式碼來取代這些保留字元。 例如，`<` 字元會取代為 `&lt;`，而 `>` 字元則會取代為 `&gt;`。 瀏覽器會以您想要查看的字元呈現這些取代字串。
> 
> 當您顯示從使用者所提供的字串（輸入）時，使用 HTML 編碼是個不錯的主意。 如果您沒有這麼做，使用者可以嘗試讓網頁執行惡意腳本，或執行其他動作來危害您的網站安全性，或者這不是您想要的東西。 （這對於您採取使用者輸入、將它儲存在其他地方，然後在稍後&#8212;顯示，例如，作為 blog 批註、使用者評論或像這樣）的情況下特別重要。
> 
> 為協助避免這些問題，ASP.NET Web Pages 會自動對您從程式碼輸出的任何文字內容進行 HTML 編碼。 例如，當您使用 `@MyVar`之類的程式碼顯示變數或運算式的內容時，ASP.NET Web Pages 會自動將輸出編碼。

## <a name="validating-user-input"></a>驗證使用者輸入

使用者犯了錯誤。 您要求他們填寫欄位，並忘了，或要求他們輸入員工人數，並改為鍵入名稱。 若要確定表單在處理之前已正確填入，請驗證使用者的輸入。

此程式示範如何驗證所有三個表單欄位，以確保使用者不會將其保留空白。 您也可以檢查員工計數值是否為數字。 如果發生錯誤，您將會顯示錯誤訊息，告知使用者哪些值未通過驗證。

1. 在*形式的 cshtml*檔案中，以下列程式碼取代第一個程式碼區塊： 

    [!code-cshtml[Main](4-working-with-forms/samples/sample3.cshtml)]

    若要驗證使用者輸入，您可以使用 `Validation` helper。 您可以藉由呼叫 `Validation.RequireField`來註冊所需的欄位。 您可以藉由呼叫 `Validation.Add` 並指定要驗證的欄位以及要執行的驗證類型，來註冊其他類型的驗證。

    當頁面執行時，ASP.NET 會為您執行所有驗證。 您可以藉由呼叫 `Validation.IsValid`來檢查結果，如果通過所有專案，則會傳回 true，如果有任何欄位驗證失敗，則傳回 false。 一般來說，您會在對使用者輸入執行任何處理之前，先呼叫 `Validation.IsValid`。
2. 藉由新增三個對 `Html.ValidationMessage` 方法的呼叫來更新 `<body>` 元素，如下所示：

    [!code-cshtml[Main](4-working-with-forms/samples/sample4.cshtml?highlight=8,13,18)]

    若要顯示驗證錯誤訊息，您可以呼叫 Html。`ValidationMessage` 並將您想要訊息的功能變數名稱傳遞給它。
3. 執行頁面。 將欄位保留空白，然後按一下 [**提交**]。 您會看到錯誤訊息。

    ![螢幕擷取畫面：顯示使用者輸入未通過驗證時所顯示的錯誤訊息。](4-working-with-forms/_static/image3.jpg)
4. 將字串（例如，"ABC"）新增至 [**員工計數**] 欄位，然後再按一下 [**提交**]。 此時您會看到錯誤，指出字串不是正確的格式，也就是整數。

    ![螢幕擷取畫面：顯示使用者輸入 [員工] 欄位的字串時所顯示的錯誤訊息。](4-working-with-forms/_static/image4.jpg)

ASP.NET Web Pages 提供更多選項來驗證使用者輸入，包括能夠使用用戶端腳本自動執行驗證，讓使用者可以在瀏覽器中取得立即的意見反應。 如需詳細資訊，請參閱稍後的[其他資源](#Additional_Resources)一節。

## <a name="restoring-form-values-after-postbacks"></a>回傳後還原表單值

當您測試上一節中的頁面時，您可能已經注意到，如果發生驗證錯誤，您輸入的所有專案（不只是不正確資料）都會消失，而且您必須重新輸入所有欄位的值。 這說明一個重點：當您提交頁面、處理它，然後再次轉譯頁面時，會從頭重新建立頁面。 如您所見，這表示提交的頁面中的任何值都會遺失。

不過，您可以輕鬆地修正此問題。 您可以存取已提交的值（在 `Request.Form` 物件中，因此當呈現頁面時，您可以將這些值填回表單欄位中。

1. 在 *. cshtml*檔案中，使用 `value` 屬性取代 `<input>` 元素的 `value` 屬性： 

    [!code-cshtml[Main](4-working-with-forms/samples/sample5.cshtml?highlight=13,19,25)]

    已設定 `<input>` 元素的 `value` 屬性，以動態方式從 `Request.Form` 物件讀取域值。 第一次要求頁面時，`Request.Form` 物件中的值都是空的。 這沒什麼問題，因為表單是空白的。
2. 在您的瀏覽器中啟動頁面，填寫表單欄位或將其保留空白，然後按一下 [**提交**]。 隨即會顯示顯示已提交值的頁面。

    ![表單-5](4-working-with-forms/_static/image5.jpg)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他資源

- [從 Web 使用者取得輸入的1001方式](https://msdn.microsoft.com/library/ms971057.aspx)
- [使用表單和處理使用者輸入](https://msdn.microsoft.com/library/ms525182(VS.90).aspx)
- [在 ASP.NET Web Pages 網站中驗證使用者輸入](https://go.microsoft.com/fwlink/?LinkId=253002)
- [在 HTML 表單中使用自動完成](https://msdn.microsoft.com/library/ms533032(VS.85).aspx)
