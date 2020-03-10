---
uid: web-pages/overview/ui-layouts-and-themes/9-working-with-images
title: 使用 ASP.NET Web Pages （Razor）網站中的影像 |Microsoft Docs
author: Rick-Anderson
description: 本章說明如何在您的網站中新增、顯示及操作影像（調整大小、翻轉和新增浮水印）。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 778c4e58-4372-4d25-bab9-aec4a8d8e38d
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/9-working-with-images
msc.type: authoredcontent
ms.openlocfilehash: 53514b3c314fc182a43c82974ffcfa8158a636a1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78631856"
---
# <a name="working-with-images-in-an-aspnet-web-pages-razor-site"></a>使用 ASP.NET Web Pages （Razor）網站中的影像

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明如何在 ASP.NET Web Pages （Razor）網站中新增、顯示及操作影像（調整大小、翻轉和新增浮水印）。
> 
> 您將學到什麼：
> 
> - 如何以動態方式將影像新增至頁面。
> - 如何讓使用者上傳影像。
> - 如何調整影像大小。
> - 如何翻轉或旋轉影像。
> - 如何將浮水印新增至影像。
> - 如何使用影像做為浮水印。
> 
> 以下是文章中引進的 ASP.NET 程式設計功能：
> 
> - `WebImage` helper。
> - `Path` 物件，提供可讓您操作路徑和檔案名的方法。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）2
> - WebMatrix 2
>   
> 
> 本教學課程也適用于 WebMatrix 3。

<a id="Adding_an_Image"></a>
## <a name="adding-an-image-to-a-web-page-dynamically"></a>以動態方式將影像新增至網頁

您可以在開發網站時，將影像新增至您的網站和個別頁面。 您也可以讓使用者上傳影像，這可能適用于讓他們新增設定檔相片等工作。

如果您的網站上已有影像，而您只想要將它顯示在頁面上，您可以使用 HTML `<img>` 元素，如下所示：

[!code-html[Main](9-working-with-images/samples/sample1.html)]

不過，有時候您需要能夠動態&#8212;顯示影像，也就是說，在頁面執行之前，您不知道要顯示的影像。

本節中的程式示範如何在使用者從影像名稱清單中指定影像檔案名稱的即時顯示影像。 他們會從下拉式清單中選取影像的名稱，而當他們提交頁面時，就會顯示所選取的影像。

![包](9-working-with-images/_static/image1.jpg "ch9images-1 .jpg")

1. 在 WebMatrix 中，建立新的網站。
2. 新增名為*DynamicImage*的新頁面。
3. 在網站的根資料夾中，加入新的資料夾，並將其命名為*images*。
4. 將四個影像新增至您剛才建立的*images*資料夾。 （您可以使用的任何影像都會這麼做，但它們應該會放入頁面上）。重新命名影像*Photo1 .jpg*、 *Photo2 .jpg*、 *Photo3*和*Photo4*。 （您不會在此程式中使用*Photo4* ，但稍後會在本文中使用它）。
5. 確認四個影像未標示為唯讀。
6. 將頁面中的現有內容取代為下列內容：

    [!code-cshtml[Main](9-working-with-images/samples/sample2.cshtml)]

    頁面的主體具有一個名為 `photoChoice`的下拉式清單（`<select>` 元素）。 清單有三個選項，而且每個清單選項的 `value` 屬性都有一個您放在*images*資料夾中的影像名稱。 基本上，此清單可讓使用者選取易記名稱，例如 &quot;相片 1&quot;，然後在提交頁面時傳遞 *.jpg*檔案名。

    在程式碼中，您可以藉由閱讀 `Request["photoChoice"]`，從清單中取得使用者的選取範圍（亦即，影像檔案名稱）。 您會先看到是否有任何選取專案。 如果有，您可以為映射建立路徑，其中包含影像的資料夾名稱和使用者的影像檔案名稱。 （如果您嘗試建立路徑，但 `Request["photoChoice"]`中沒有任何內容，就會收到錯誤）。這會產生如下所示的相對路徑：

    *images/Photo1 .jpg*

    路徑會儲存在名為 `imagePath` 的變數中，您稍後會在頁面中需要此名稱。

    在本文中，還有一個 `<img>` 元素，用來顯示使用者挑選的影像。 `src` 屬性未設定為檔案名或 URL，就像您要顯示靜態元素一樣。 相反地，它會設定為 `@imagePath`，這表示它會從您在程式碼中設定的路徑取得其值。

    不過，第一次執行頁面時，不會顯示任何影像，因為使用者未選取任何專案。 這通常表示 `src` 屬性會是空的，而且影像會顯示為紅色 &quot;x&quot; （或當瀏覽器找不到影像時所呈現的任何內容）。 若要避免這個情況，請將 `<img>` 元素放在測試的 `if` 區塊中，以查看 `imagePath` 變數是否有任何專案。 如果使用者進行選取，`imagePath` 包含路徑。 如果使用者未選取影像，或這是第一次顯示頁面，則不會轉譯 `<img>` 元素。
7. 儲存檔案，並在瀏覽器中執行頁面。 （在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）
8. 從下拉式清單中選取映射，然後按一下 [**範例影像**]。 請確定您針對不同的選擇看到不同的映射。

<a id="Uploading_an_Image"></a>
## <a name="uploading-an-image"></a>上傳影像

先前的範例示範如何以動態方式顯示影像，但只能使用已在您網站上的影像。 此程式說明如何讓使用者上傳影像，然後顯示在頁面上。 在 ASP.NET 中，您可以使用 `WebImage` 協助程式即時操作影像，其中包含可讓您建立、操作和儲存影像的方法。 `WebImage` helper 支援所有常見的 web 圖像檔案類型，包括 *.jpg*、 *.png*和 *.bmp*。 在本文中，您將使用 *.jpg*影像，但是您可以使用任何影像類型。

![包](9-working-with-images/_static/image2.jpg "ch9images-2 .jpg")

1. 新增頁面，並將它命名為*UploadImage*。
2. 將頁面中的現有內容取代為下列內容： 

    [!code-cshtml[Main](9-working-with-images/samples/sample3.cshtml)]

    文字的主體具有 `<input type="file">` 元素，可讓使用者選取要上傳的檔案。 當他們按一下 [**提交**] 時，所挑選的檔案會連同表單一起提交。

    若要取得已上傳的影像，您可以使用 `WebImage` helper，其具有各種使用影像的實用方法。 具體而言，您會使用 `WebImage.GetImageFromRequest` 來取得已上傳的影像（如果有的話），並將它儲存在名為 `photo`的變數中。

    此範例中有很多工作需要取得和設定檔案和路徑名稱。 問題在於，您想要取得使用者所上傳影像的名稱（以及名稱），然後為您要儲存映射的位置建立新的路徑。 因為使用者可能會上傳多個具有相同名稱的影像，所以您可以使用一些額外的程式碼來建立唯一的名稱，並確保使用者不會覆寫現有的圖片。

    如果已上傳影像（測試 `if (photo != null)`），您會從影像的 `FileName` 屬性取得映射名稱。 當使用者上傳影像時，`FileName` 會包含使用者的原始名稱，其中包括使用者電腦的路徑。 看起來可能像這樣：

    *C:\Users\Joe\Pictures\SamplePhoto1.jpg*

    雖然您只想要實際的檔案名（ &#8212; *SamplePhoto1 .jpg*），但您不想要所有的路徑資訊。 您可以使用 `Path.GetFileName` 方法來去除路徑中的檔案，如下所示：

    [!code-csharp[Main](9-working-with-images/samples/sample4.cs)]

    接著，您可以藉由將 GUID 加入至原始名稱，來建立新的唯一檔案名。 （如需 Guid 的詳細資訊，請參閱本文稍後的[關於 guid](#SB_AboutGUIDs) ）。然後，您會建立可用來儲存影像的完整路徑。 儲存路徑是由新的檔案名、資料夾（影像）和目前的網站位置所組成。

    > [!NOTE]
    > 為了讓您的程式碼將檔案儲存在*images*資料夾中，應用程式需要該資料夾的讀寫許可權。 在您的開發電腦上，這通常不是問題。 不過，當您將網站發佈至主控提供者的 web 伺服器時，您可能需要明確地設定這些許可權。 如果您在主控提供者的伺服器上執行此程式碼，並收到錯誤，請洽詢主機服務提供者，以瞭解如何設定這些許可權。

    最後，您會將儲存路徑傳遞給 `WebImage` helper 的 `Save` 方法。 這會將所上傳的影像儲存在其新名稱之下。 Save 方法看起來像這樣： `photo.Save(@"~\" + imagePath)`。 完整路徑會附加至 `@"~\"`，也就是目前的網站位置。 （如需 `~` 運算子的詳細資訊，請參閱[使用 Razor 語法 ASP.NET Web 程式設計的簡介](https://go.microsoft.com/fwlink/?LinkId=202890#ID_WorkingWithFileAndFolderPaths)）。

    如先前範例所示，頁面的內文包含一個 `<img>` 元素來顯示影像。 如果已設定 `imagePath`，則會轉譯 `<img>` 元素，且其 `src` 屬性會設定為 `imagePath` 值。
3. 在瀏覽器中執行頁面。
4. 上傳影像，並確定它顯示在頁面中。
5. 在您的網站中，開啟 [ *images* ] 資料夾。 您會看到新的檔案已經加入，其檔案名看起來像這樣：： 

    *45ea4527-7ddd-4965-b9ca-c6444982b342\_MyPhoto .png*

    這是您上傳的映射，其 GUID 前面會加上名稱。 （您自己的檔案將會有不同的 GUID，而且名稱可能會與*MyPhoto*不同）。

> [!TIP] 
> 
> <a id="SB_AboutGUIDs"></a>
> ### <a name="about-guids"></a>關於 Guid
> 
> GUID （全域唯一識別碼）是通常以如下格式轉譯的識別碼： `936DA01F-9ABD-4d9d-80C7-02AF85C822A8`。 每個 GUID 的數位和字母（從-F）不同，但全都遵循使用8-4-4-4-12 個字元群組的模式。 （就技術上而言，GUID 是16位元組/128 位的數位）。當您需要 GUID 時，您可以呼叫為您產生 GUID 的特製化程式碼。 Guid 背後的構想是，在數位的龐大大小（3.4 x 10<sup>38</sup>）和產生它的演算法之間，所產生的數位幾乎都一定是其中一種。 因此，當您必須保證不會使用相同的名稱兩次時，Guid 就是產生專案名稱的好方法。 當然，缺點是 Guid 並不特別方便使用者使用，因此當名稱只用于程式碼時，通常會用到。

<a id="Resizing_an_Image"></a>
## <a name="resizing-an-image"></a>調整影像大小

如果您的網站接受來自使用者的影像，您可能會想要在顯示或儲存影像之前調整其大小。 您可以再次使用 `WebImage` helper 來進行此工作。

此程式示範如何調整已上傳影像的大小以建立縮圖，然後將縮圖和原始影像儲存在網站中。 您會在頁面上顯示縮圖，並使用超連結將使用者重新導向至完整大小的影像。

![包](9-working-with-images/_static/image3.jpg "ch9images-3 .jpg")

1. 新增名為 [*微縮圖. cshtml*] 的新頁面。
2. 在 [ *images* ] 資料夾中，建立名為*大拇指*的子資料夾。
3. 將頁面中的現有內容取代為下列內容： 

    [!code-cshtml[Main](9-working-with-images/samples/sample5.cshtml)]

    此程式碼與上一個範例中的程式碼類似。 差別在於，此程式碼會在您建立影像的縮圖複本之後，正常地儲存影像兩次。 首先，您會取得已上傳的影像，並將它儲存在*images*資料夾中。 接著，您會為縮圖影像建立新的路徑。 若要實際建立縮圖，您可以呼叫 `WebImage` helper 的 `Resize` 方法，以建立60圖元的60圖元影像。 此範例會示範如何保留外觀比例，以及如何防止影像放大（以防新的大小實際會使影像變大）。 然後，調整大小的影像會儲存在 [*拇指*] 子資料夾中。

    在標記的結尾，您會使用與您在先前範例中看到的動態 `src` 屬性相同的 `<img>` 元素，以有條件地顯示影像。 在此情況下，您會顯示縮圖。 您也可以使用 `<a>` 元素，來建立影像的大型版本超連結。 如同 `<img>` 元素的 `src` 屬性，您可以將 `<a>` 專案的 `href` 屬性動態設定為 `imagePath`中的任何一個。 為確保路徑可以做為 URL，您可以將 `imagePath` 傳遞至 `Html.AttributeEncode` 方法，這會將路徑中的保留字元轉換為 URL 中的正確字元。
4. 在瀏覽器中執行頁面。
5. 上傳相片並確認已顯示縮圖。
6. 按一下縮圖以查看完整大小的影像。
7. 請注意，在*images*和*images/拇指*中，已新增檔案。

<a id="Rotating_and_Flipping"></a>
## <a name="rotating-and-flipping-an-image"></a>旋轉和翻轉影像

`WebImage` 協助程式也可讓您翻轉和旋轉影像。 此程式顯示如何從伺服器取得影像、反轉影像的倒置（垂直）、儲存，然後在頁面上顯示翻轉的影像。 在此範例中，您只是使用伺服器上已有的檔案（*Photo2 .jpg*）。 在實際的應用程式中，您可能會翻轉以動態方式取得名稱的映射，就像先前範例中所做的一樣。

![包](9-working-with-images/_static/image4.jpg "ch9images-4 .jpg")

1. 新增名為*FlipImage*的新頁面。
2. 將頁面中的現有內容取代為下列內容： 

    [!code-cshtml[Main](9-working-with-images/samples/sample6.cshtml)]

    程式碼會使用 `WebImage` helper 來從伺服器取得影像。 您可以使用先前用來儲存影像的相同技術來建立映射的路徑，並在使用 `WebImage`建立映射時傳遞該路徑：

    [!code-javascript[Main](9-working-with-images/samples/sample7.js)]

    如果找到影像，您可以建立新的路徑和檔案名，就像您在先前的範例中所做的一樣。 若要翻轉影像，請呼叫 `FlipVertical` 方法，然後再次儲存影像。

    使用 `src` 屬性設定為 `imagePath`的 `<img>` 專案，即可再次在頁面上顯示影像。
3. 在瀏覽器中執行頁面。 *Photo2*的影像會以倒置顯示。
4. 重新整理頁面，或再次要求頁面，以查看影像已正確翻轉。

若要旋轉影像，您可以使用相同的程式碼，但不會呼叫 `FlipVertical` 或 `FlipHorizontal`，而是呼叫 `RotateLeft` 或 `RotateRight`。

<a id="Adding_a_Watermark"></a>
## <a name="adding-a-watermark-to-an-image"></a>將浮水印新增至影像

當您將影像新增至您的網站時，您可能會想要先將浮水印新增至影像，然後將它顯示在頁面上。 人們通常會使用浮水印將著作權資訊新增至影像或廣告其商務名稱。

![包](9-working-with-images/_static/image5.jpg "ch9images-5 .jpg")

1. 新增名為 [*浮水印*] 的新頁面。
2. 將頁面中的現有內容取代為下列內容： 

    [!code-cshtml[Main](9-working-with-images/samples/sample8.cshtml)]

    這段程式碼就像是稍早的*FlipImage*中的程式碼（雖然這次是使用*Photo3*檔案）。 若要新增浮水印，您可以先呼叫 `WebImage` helper 的 `AddTextWatermark` 方法，再儲存影像。 在 `AddTextWatermark`的呼叫中，您會將文字 &quot;[我的浮水印]&quot;，將字型色彩設為黃色，並將字型系列設定為 [Arial]。 （雖然此處未顯示，但 `WebImage` 協助程式也可讓您指定不透明度、字型系列和字型大小，以及浮水印文字的位置）。當您儲存映射時，它不得為唯讀。

    如先前所見，影像會使用 [src] 屬性設定為 [`@imagePath`] 的 `<img>` 元素顯示在頁面上。
3. 在瀏覽器中執行頁面。 請注意影像右下角的「我的浮水印」文字。

<a id="Using_an_Image_as_a_Watermark"></a>
## <a name="using-an-image-as-a-watermark"></a>使用影像做為浮水印

您可以使用另一個影像，而不是使用浮水印的文字。 人們有時會使用公司標誌之類的影像做為浮水印，或使用浮水印影像而非文字來取得著作權資訊。

![包](9-working-with-images/_static/image6.jpg "ch9images-6 .jpg")

1. 新增名為*ImageWatermark*的新頁面。
2. 將影像新增至 [ *images* ] 資料夾，您可以使用它做為標誌，並重新命名影像*MyCompanyLogo*。 此影像應該是當其設定為80圖元寬和20圖元高時，可以清楚看出的影像。
3. 將頁面中的現有內容取代為下列內容： 

    [!code-cshtml[Main](9-working-with-images/samples/sample9.cshtml)]

    這是先前範例中程式碼的另一種變化。 在此情況下，您可以呼叫 `AddImageWatermark`，將浮水印影像新增至目標影像（*Photo3 .jpg*），然後再儲存影像。 當您呼叫 `AddImageWatermark`時，會將其寬度設定為80圖元，並將高度設為20圖元。 *MyCompanyLogo*會水準對齊，並在目標影像底部以垂直方式對齊。 不透明度設定為100%，而填補設定為10圖元。 如果浮水印影像大於目標影像，則不會發生任何事。 如果浮水印影像大於目標影像，而且您將影像浮水印的填補設定為零，則會忽略浮水印。

    如先前所示，您可以使用 `<img>` 元素和動態 `src` 屬性來顯示影像。
4. 在瀏覽器中執行頁面。 請注意，浮水印影像會出現在主要影像的底部。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他資源

[使用 ASP.NET Web Pages 網站中的檔案](https://go.microsoft.com/fwlink/?LinkId=202896)

[使用 Razor 語法進行 ASP.NET Web Pages 程式設計的簡介](https://go.microsoft.com/fwlink/?LinkID=251587)
