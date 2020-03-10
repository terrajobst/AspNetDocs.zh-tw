---
uid: web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
title: 在 ASP.NET Web Pages （Razor）網站中建立一致的版面配置 |Microsoft Docs
author: Rick-Anderson
description: 為了讓您更有效率地建立網站的網頁，您可以為網站建立可重複使用的內容區塊（例如頁首和頁尾），而您的 c 。
ms.author: riande
ms.date: 03/10/2014
ms.assetid: d7bd001b-6db2-4422-9b78-f3d08b743b00
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
msc.type: authoredcontent
ms.openlocfilehash: 3f63ce68ae4c13970ac0df196167ace0b22b592c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627446"
---
# <a name="creating-a-consistent-layout-in-aspnet-web-pages-razor-sites"></a>在 ASP.NET Web Pages （Razor）網站中建立一致的版面配置

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明如何使用 ASP.NET Web Pages （Razor）網站中的版面配置頁來建立可重複使用的內容區塊（例如頁首和頁尾），並建立一致的外觀來尋找網站中的所有頁面。
> 
> **您將瞭解的內容：** 
> 
> - 如何建立可重複使用的內容區塊，例如頁首和頁尾。
> - 如何使用版面配置建立網站中所有頁面的一致外觀。
> - 如何在執行時間將資料傳遞至版面配置頁。
> 
> 以下是文章中引進的 ASP.NET 功能：
> 
> - 內容區塊，其為包含要插入多頁之 HTML 格式內容的檔案。
> - 版面配置頁，也就是包含 HTML 格式內容的頁面，可由網站上的網頁共用。
> - `RenderPage`、`RenderBody`和 `RenderSection` 方法，告訴 ASP.NET 要在何處插入頁面元素。
> - `PageData` 字典，可讓您在內容區塊和版面配置頁之間共用資料。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）3
>   
> 
> 本教學課程也適用于 ASP.NET Web Pages 2。

## <a name="about-layout-pages"></a>關於版面配置頁

許多網站都有顯示在每個頁面上的內容，例如頁首和頁尾，或可告知使用者已登入的方塊。 ASP.NET 可讓您建立具有內容區塊的個別檔案，其中包含文字、標記和程式碼，就像一般的網頁一樣。 接著，您可以將內容區塊插入網站上您想要顯示資訊的其他頁面。 如此一來，您就不需要將相同的內容複寫並貼到每個頁面中。 建立這類常見的內容也能讓您更輕鬆地更新您的網站。 如果您需要變更內容，您可以只更新單一檔案，然後變更會反映在插入內容的所有位置。

下圖顯示內容區塊的工作方式。 當瀏覽器向 web 伺服器要求頁面時，ASP.NET 會在主頁面中呼叫 `RenderPage` 方法的位置插入內容區塊。 [完成（已合併）] 頁面接著會傳送至瀏覽器。

![概念圖顯示 RenderPage 方法如何在目前的頁面中插入參考的頁面。](3-creating-a-consistent-look/_static/image1.jpg)

在此程式中，您將建立一個頁面，參考位於不同檔案中的兩個內容區塊（頁首和頁尾）。 您可以在網站的任何頁面中使用這些相同的內容區塊。 當您完成時，您會看到如下的頁面：

![螢幕擷取畫面：顯示瀏覽器中的頁面，其結果是執行包含 RenderPage 方法呼叫的頁面。](3-creating-a-consistent-look/_static/image2.png)

1. 在網站的根資料夾中，建立名為*Index. cshtml*的檔案。
2. 以下列內容取代現有的標記：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample1.html)]
3. 在根資料夾中，建立名為*Shared*的資料夾。

    > [!NOTE]
    > 在名為*shared*的資料夾中，儲存網頁之間共用的檔案是常見的作法。
4. 在*共用*資料夾中，建立名為 *\_標頭 cshtml*的檔案。
5. 將任何現有的內容取代為下列內容：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample2.html)]

    請注意，檔案名是 *\_標頭. cshtml*，加底線（\_）做為前置詞。 如果 ASP.NET 的名稱開頭為底線，則不會將頁面傳送至瀏覽器。 這可防止使用者直接要求（不小心或其他）這些頁面。 使用底線來命名含有內容區塊的頁面，是個不錯的主意，因為您不想讓使用者能夠要求這些頁面&#8212; ，嚴格地插入其他頁面。
6. 在*共用*資料夾中，建立名為 *\_頁尾. cshtml*的檔案，並將內容取代為下列內容：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample3.html)]
7. 在 [ *Index. cshtml* ] 頁面中，新增兩個對 `RenderPage` 方法的呼叫，如下所示：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample4.html)]

    這會顯示如何將內容區塊插入網頁。 您可以呼叫 `RenderPage` 方法，並將您想要在該點插入其內容的檔案名傳遞給它。 在這裡，您要將 *\_標頭. cshtml*和\_頁尾 *. cshtml*檔案的內容插入到*Index.* cshtml 檔案中。
8. 在瀏覽器中執行 [ *Index. cshtml* ] 頁面。 （在 WebMatrix 的 [檔案 **] 工作區**中，以滑鼠右鍵按一下檔案，然後選取 [**在瀏覽器中啟動**]。）
9. 在瀏覽器中，查看頁面來源。 （例如，在 Internet Explorer 中，以滑鼠右鍵按一下頁面，然後按一下 [ **View Source**]）。

    這可讓您查看傳送至瀏覽器的網頁標記，其結合了索引頁標記與內容區塊。 下列範例會顯示針對*Index*所呈現的頁面來源。 您插入到*Index*中的 `RenderPage` 呼叫已被標頭和頁尾檔案的實際內容所取代。

    [!code-html[Main](3-creating-a-consistent-look/samples/sample5.html)]

## <a name="creating-a-consistent-look-using-layout-pages"></a>使用版面配置頁建立一致的外觀

到目前為止，您已經看過在多個頁面上包含相同的內容是很容易的。 建立一致的網站外觀的更結構化方法，就是使用版面配置頁面。 版面配置頁會定義網頁的結構，但不包含任何實際內容。 建立版面配置頁之後，您可以建立包含內容的網頁，然後將其連結至版面配置頁面。 顯示這些頁面時，將會根據版面配置頁面將其格式化。 （在這種情況下，版面配置頁面會作為在其他頁面中定義之內容的範本類型）。

版面配置頁與任何 HTML 網頁一樣，不同之處在于它包含對 `RenderBody` 方法的呼叫。 [版面配置] 頁面中 `RenderBody` 方法的位置，會決定要包含內容頁面中之資訊的位置。

下圖顯示如何在執行時間結合內容頁和版面配置頁，以產生完成的網頁。 瀏覽器要求內容頁面。 [內容] 頁面中有程式碼，可指定要用於頁面結構的版面配置頁。 在 [版面配置] 頁面中，會將內容插入呼叫 `RenderBody` 方法的位置。 內容區塊也可以藉由呼叫 `RenderPage` 方法（以您在上一節中執行的方式），插入至版面配置頁。 網頁完成時，會傳送至瀏覽器。

![螢幕擷取畫面：顯示瀏覽器中的頁面，其結果是執行包含 RenderBody 方法呼叫的頁面。](3-creating-a-consistent-look/_static/image3.jpg)

下列程式示範如何建立版面配置頁，並將內容頁面連結至該頁面。

1. 在您網站的*共用*資料夾中，建立名為 *\_layout1.xml*的檔案。
2. 將任何現有的內容取代為下列內容：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample6.html)]

    您可以使用版面配置頁中的 `RenderPage` 方法來插入內容區塊。 版面配置頁只能包含一個 `RenderBody` 方法的呼叫。
3. 在*共用*資料夾中，建立名為 *\_h 2*的檔案，並將任何現有的內容取代為下列內容：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample7.html)]
4. 在根資料夾中，建立新的資料夾，並將其命名為*樣式*。
5. 在 [*樣式*] 資料夾中，建立名為*Site .css*的檔案，並新增下列樣式定義：

    [!code-css[Main](3-creating-a-consistent-look/samples/sample8.css)]

    這些樣式定義僅供示範如何搭配版面配置頁使用樣式表單。 如有需要，您可以為這些元素定義自己的樣式。
6. 在根資料夾中，建立名為*Content1*的檔案，並將任何現有的內容取代為下列內容：

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample9.cshtml)]

    這是將使用版面配置頁的頁面。 頁面頂端的程式碼區塊會指出要用來格式化此內容的版面配置頁。
7. 在瀏覽器中執行*Content1。* 呈現的頁面會使用 *\_layout1.xml*中定義的格式和樣式表單，以及*Content1*中定義的文字（content）。

    ![[影像]](3-creating-a-consistent-look/_static/image4.png)

    您可以重複步驟6，建立可共用相同版面配置頁的其他內容頁面。

    > [!NOTE]
    > 您可以設定您的網站，讓您可以針對資料夾中的所有內容頁面自動使用相同的版面配置頁。 如需詳細資訊，請參閱[針對 ASP.NET Web Pages 自訂全網站行為](https://go.microsoft.com/fwlink/?LinkId=202906)。

## <a name="designing-layout-pages-that-have-multiple-content-sections"></a>設計具有多個內容區段的版面配置頁

內容頁面可以有多個區段，如果您想要使用具有可替換內容的多個區域的版面配置，這會很有用。 在 [內容] 頁面中，您可以為每個區段提供唯一的名稱。 （預設區段會保留為未命名）。在 [版面配置] 頁面中，您可以新增 `RenderBody` 方法，以指定應出現未命名（預設）區段的位置。 接著，您會新增個別的 `RenderSection` 方法，以便個別轉譯命名的區段。

下圖顯示 ASP.NET 如何處理劃分成多個區段的內容。 每個命名的區段都包含在 [內容] 頁面的區段區塊中。 （它們的名稱是 `Header`，在範例中 `List`）。架構會在呼叫 `RenderSection` 方法的位置，將內容區段插入至版面配置頁。 未命名的（預設）區段會插入呼叫 `RenderBody` 方法的位置，如先前所見。

![概念圖顯示 RenderSection 方法如何將參考區段插入目前的頁面。](3-creating-a-consistent-look/_static/image5.jpg)

此程式說明如何建立具有多個內容區段的內容頁面，以及如何使用支援多個內容區段的版面配置頁來呈現它。

1. 在*共用*資料夾中，建立名為 *\_Layout2*的檔案。
2. 將任何現有的內容取代為下列內容：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample10.html)]

    您可以使用 `RenderSection` 方法來呈現標頭和清單區段。
3. 在根資料夾中，建立名為*Content2*的檔案，並將任何現有的內容取代為下列內容：

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample11.cshtml)]

    此內容頁面會在頁面頂端包含程式碼區塊。 每個命名的區段都包含在區段區塊中。 頁面的其餘部分包含預設（未命名）內容區段。
4. 在瀏覽器中執行*Content2。*

    ![螢幕擷取畫面：顯示瀏覽器中的頁面，其結果是執行包含 RenderSection 方法呼叫的頁面。](3-creating-a-consistent-look/_static/image6.png)

## <a name="making-content-sections-optional"></a>將內容區段設為選擇性

一般來說，您在內容頁面中建立的區段必須符合版面配置頁面中所定義的區段。 如果發生下列任何一種情況，您可能會收到錯誤：

- [內容] 頁面包含 [版面配置] 頁面中沒有對應區段的區段。
- 版面配置頁包含沒有內容的區段。
- 版面配置頁包含嘗試多次轉譯相同區段的方法呼叫。

不過，您可以藉由在版面配置頁中宣告區段為選擇性，來覆寫已命名區段的這個行為。 這可讓您定義多個可以共用版面配置頁的內容頁，但可能會有或沒有特定區段的內容。

1. 開啟*Content2* ，並移除下列區段：

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample12.cshtml)]
2. 儲存頁面，然後在瀏覽器中執行。 會顯示錯誤訊息，因為 [內容] 頁面不會提供版面配置頁中所定義之區段的內容，也就是標頭區段。

    ![螢幕擷取畫面：顯示當您執行呼叫 RenderSection 方法但未提供對應區段的頁面時，所發生的錯誤。](3-creating-a-consistent-look/_static/image7.png)
3. 在*共用*資料夾中，開啟 [ *\_Layout2* ] 頁面，並取代這一行：

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample13.js)]

    取代為下列程式碼：

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample14.js)]

    或者，您可以使用下列程式碼區塊來取代前一行程式碼，這樣會產生相同的結果：

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample15.cshtml)]
4. 再次執行瀏覽器中的*Content2*頁面。 （如果您仍然在瀏覽器中開啟此頁面，您可以直接重新整理它。）這次會顯示頁面，而不會發生錯誤，即使沒有標頭也一樣。

## <a name="passing-data-to-layout-pages"></a>將資料傳遞至版面配置頁

您可能會在 [內容] 頁面中定義您需要在版面配置頁面中參考的資料。 若是如此，您必須將資料從 [內容] 頁面傳遞至 [版面配置] 頁面。 例如，您可能想要顯示使用者的登入狀態，或者您可能想要根據使用者輸入來顯示或隱藏內容區域。

若要將資料從內容頁面傳遞至版面配置頁，您可以將值放入 [內容] 頁面的 [`PageData`] 屬性中。 `PageData` 屬性是名稱/值組的集合，其中包含您要在頁面之間傳遞的資料。 在 [版面配置] 頁面中，您可以從 [`PageData`] 屬性讀取值。

以下是另一個圖表。 這個範例會示範 ASP.NET 如何使用 `PageData` 屬性，將值從內容頁傳遞至版面配置頁。 當 ASP.NET 開始建立網頁時，它會建立 `PageData` 集合。 在 [內容] 頁面中，您可以撰寫程式碼，將資料放入 `PageData` 集合中。 `PageData` 集合中的值也可以由內容頁面中的其他區段或其他內容區塊來存取。

![概念圖，顯示內容頁面如何填入 PageData 字典，並將該資訊傳遞至版面配置頁。](3-creating-a-consistent-look/_static/image8.jpg)

下列程式顯示如何將資料從內容頁面傳遞至版面配置頁。 當頁面執行時，它會顯示一個按鈕，讓使用者隱藏或顯示在版面配置頁中定義的清單。 當使用者按一下按鈕時，它會在 `PageData` 屬性中設定 true/false （布林值）值。 版面配置頁會讀取該值，如果是 false，則會隱藏清單。 此值也會在 [內容] 頁面中用來判斷是否要顯示 [**隱藏清單**] 按鈕或 [**顯示清單**] 按鈕。

![[影像]](3-creating-a-consistent-look/_static/image9.jpg)

1. 在根資料夾中，建立名為*Content3*的檔案，並將任何現有的內容取代為下列內容：

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample16.cshtml)]

    此程式碼會在 `PageData` 屬性&#8212;中儲存兩個數據片段，此網頁的標題為 true 或 false，以指定是否要顯示清單。

    請注意，ASP.NET 可讓您使用程式碼區塊，有條件地將 HTML 標籤放入頁面。 例如，頁面主體中的 `if/else` 區塊會根據 `PageData["ShowList"]` 是否設定為 true 來決定要顯示的表單。
2. 在*共用*資料夾中，建立名為 *\_Layout3*的檔案，並將任何現有的內容取代為下列內容：

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample17.cshtml)]

    版面配置頁在 `<title>` 元素中包含一個運算式，可從 `PageData` 屬性取得標題值。 它也會使用 `PageData` 屬性的 `ShowList` 值，來判斷是否要顯示清單內容區塊。
3. 在*共用*資料夾中，建立名為 *\_清單*的檔案，並將任何現有的內容取代為下列內容：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample18.html)]
4. 在瀏覽器中執行*Content3。* 頁面會顯示在頁面左側的清單中，並在底部顯示 [**隱藏清單**] 按鈕。

    ![螢幕擷取畫面，其中顯示包含清單的頁面和顯示 [隱藏清單] 的按鈕。](3-creating-a-consistent-look/_static/image10.png)
5. 按一下 [**隱藏清單**]。 清單會消失，且按鈕會變更為 [**顯示清單**]。

    ![螢幕擷取畫面：顯示不包含清單的頁面，以及指出 [顯示清單] 的按鈕。](3-creating-a-consistent-look/_static/image11.png)
6. 按一下 [**顯示清單**] 按鈕，清單就會再次顯示。

## <a name="additional-resources"></a>其他資源

[針對 ASP.NET Web Pages 自訂全網站行為](https://go.microsoft.com/fwlink/?LinkId=202906)
