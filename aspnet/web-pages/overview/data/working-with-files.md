---
uid: web-pages/overview/data/working-with-files
title: 使用 ASP.NET Web Pages （Razor）網站中的檔案 |Microsoft Docs
author: Rick-Anderson
description: 本章說明如何讀取、寫入、附加、刪除和上傳檔案。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: eee916e4-ba4c-439a-a24e-68df7d45a569
msc.legacyurl: /web-pages/overview/data/working-with-files
msc.type: authoredcontent
ms.openlocfilehash: 684c47a8a8480dc040e5144144577c94c35d39e5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78642363"
---
# <a name="working-with-files-in-an-aspnet-web-pages-razor-site"></a>使用 ASP.NET Web Pages （Razor）網站中的檔案

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明如何在 ASP.NET Web Pages （Razor）網站中讀取、寫入、附加、刪除和上傳檔案。
> 
> > [!NOTE]
> > 如果您想要上傳影像並操作它們（例如，對其進行翻轉或調整大小），請參閱[使用 ASP.NET Web Pages 網站中的影像](/aspnet/web-pages/overview/ui-layouts-and-themes/9-working-with-images)。
> 
> 
> **您將瞭解的內容：** 
> 
> - 如何建立文字檔，並將資料寫入其中。
> - 如何將資料附加至現有的檔案。
> - 如何讀取檔案並從中顯示。
> - 如何刪除網站中的檔案。
> - 如何讓使用者上傳一個檔案或多個檔案。
> 
> 以下是文章中引進的 ASP.NET 程式設計功能：
> 
> - `File` 物件，可提供管理檔案的方式。
> - `FileUpload` helper。
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

<a id="Creating_a_Text_File"></a>
## <a name="creating-a-text-file-and-writing-data-to-it"></a>建立文字檔，並將資料寫入其中

除了在您的網站中使用資料庫之外，您還可以使用檔案。 例如，您可以使用文字檔做為儲存網站資料的簡單方式。 （用來儲存資料的文字檔，有時稱為一般檔案 *）。* 文字檔可以採用不同的格式，例如 *.txt*、 *.xml*或 *.csv* （以逗號分隔的值）。

如果您想要將資料儲存在文字檔中，您可以使用 `File.WriteAllText` 方法來指定要建立的檔案，以及要寫入資料的檔案。 在此程式中，您將建立一個頁面，其中包含具有三個 `input` 元素（名字、姓氏和電子郵件地址）和**提交**按鈕的簡單表單。 當使用者提交表單時，您會將使用者的輸入儲存在文字檔中。

1. 建立名為 [*應用程式\_資料*] 的新資料夾（如果尚未存在）。
2. 在您網站的根目錄中，建立名為*UserData*的新檔案。
3. 以下列內容取代現有的內容： 

    [!code-cshtml[Main](working-with-files/samples/sample1.cshtml)]

    HTML 標籤會建立具有三個文字方塊的表單。 在程式碼中，您可以使用 `IsPost` 屬性來判斷頁面是否已提交，然後再開始處理。

    第一個工作是取得使用者輸入，並將它指派給變數。 然後，此程式碼會將個別變數的值串連成一個逗號分隔的字串，然後儲存在不同的變數中。 請注意，逗號分隔符號是包含在引號（"，"）中的字串，因為您實際上是在要建立的大字串中內嵌一個逗號。 在您一起串連的資料結尾處，您會新增 `Environment.NewLine`。 這會加上分行符號（換行字元）。 您要使用此串連來建立的內容，就是如下所示的字串：

    [!code-css[Main](working-with-files/samples/sample2.css)]

    （結尾處有不可見的分行符號）。

    接著，您要建立一個變數（`dataFile`），其中包含要儲存資料的檔案位置和名稱。 設定位置需要一些特殊的處理。 在網站中，將程式碼參考到 web 伺服器上檔案的絕對路徑（例如*C:\Folder\File.txt* ）是不好的作法。 如果移動網站，絕對路徑會錯誤。 此外，對於託管的網站（而不是在您自己的電腦上），您通常甚至不知道撰寫程式碼時的正確路徑。

    但有時候（像現在是寫入檔案）需要完整的路徑。 解決方案是使用 `Server` 物件的 `MapPath` 方法。 這會傳回您網站的完整路徑。 若要取得網站根目錄的路徑，您可以使用者 `~` 操作員（represen 網站的虛擬根目錄）來 `MapPath`。 （您也可以將子資料夾名稱傳遞給它，例如 *~/App\_Data/* ）來取得該子資料夾的路徑）。接著，您可以將其他資訊串連到方法傳回的任何內容，以便建立完整的路徑。 在此範例中，您會新增一個檔案名。 （您可以在[使用 Razor 語法進行 ASP.NET Web Pages 程式設計簡介](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)中，閱讀更多有關如何使用檔案和資料夾路徑的資訊。）

    檔案會儲存在*應用程式\_Data*資料夾中。 此資料夾是 ASP.NET 中用來儲存資料檔案的特殊資料夾，如在[ASP.NET Web Pages 網站中使用資料庫簡介](https://go.microsoft.com/fwlink/?LinkId=195209)中所述。

    `File` 物件的 `WriteAllText` 方法會將資料寫入至檔案。 這個方法會採用兩個參數：要寫入之檔案的名稱（路徑），以及要寫入的實際資料。 請注意，第一個參數的名稱會以 `@` 字元做為前置詞。 這會告訴 ASP.NET 您要提供逐字字串常值，而且不應該以特殊方式解讀 "/" 這類的字元。 （如需詳細資訊，請參閱[使用 Razor 語法 ASP.NET Web 程式設計的簡介](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)）。

    > [!NOTE]
    > 為了讓您的程式碼將檔案儲存在*應用程式\_Data*資料夾中，應用程式需要該資料夾的讀寫許可權。 在您的開發電腦上，這通常不是問題。 不過，當您將網站發佈至主控提供者的 web 伺服器時，您可能需要明確地設定這些許可權。 如果您在主控提供者的伺服器上執行此程式碼，並收到錯誤，請洽詢主機服務提供者，以瞭解如何設定這些許可權。

- 在瀏覽器中執行頁面。 

    ![](working-with-files/_static/image1.jpg)
- 在欄位中輸入值，然後按一下 [**提交**]。
- 關閉瀏覽器。
- 返回專案並重新整理視圖。
- 開啟 [*資料 .txt* ] 檔案。 您在表單中提交的資料會在檔案中。 

    ![[影像]](working-with-files/_static/image2.jpg)
- 關閉*資料 .txt*檔案。

<a id="Appending_Data"></a>
## <a name="appending-data-to-an-existing-file"></a>將資料附加至現有的檔案

在上一個範例中，您使用 `WriteAllText` 來建立一個文字檔，其中只有一個資料片段。 如果您再次呼叫方法並傳遞相同的檔案名，則會完全覆寫現有的檔案。 不過，在建立檔案之後，您通常會想要將新的資料加入至檔案結尾。 您可以使用 `File` 物件的 `AppendAllText` 方法來執行此動作。

1. 在網站中，建立*UserData*檔案的複本，並將複本命名為*UserDataMultiple*。
2. 使用下列程式碼區塊取代開頭 `<!DOCTYPE html>` 標記之前的程式碼區塊： 

    [!code-cshtml[Main](working-with-files/samples/sample3.cshtml)]

    此程式碼在上一個範例中有一項變更。 它不會使用 `WriteAllText`，而是使用 `the AppendAllText` 方法。 方法很類似，不同之處在于 `AppendAllText` 會將資料新增至檔案結尾。 如同 `WriteAllText`，`AppendAllText` 會建立檔案（如果尚未存在）。
3. 在瀏覽器中執行頁面。
4. 輸入欄位的值，然後按一下 [**提交**]。
5. 請新增更多資料，然後再次提交表單。
6. 返回您的專案，以滑鼠**按右鍵專案**資料夾，然後按一下 [重新整理]。
7. 開啟 [*資料 .txt* ] 檔案。 它現在包含您剛輸入的新資料。 

    ![[影像]](working-with-files/_static/image3.jpg)

<a id="Reading_and_Displaying_Data"></a>
## <a name="reading-and-displaying-data-from-a-file"></a>讀取和顯示檔案中的資料

即使您不需要將資料寫入文字檔，您有時可能需要讀取其中一個資料。 若要這樣做，您可以再次使用 `File` 物件。 您可以使用 `File` 物件來個別讀取每一行（以分行符號分隔）或讀取個別專案（不論它們的分隔方式為何）。

此程式說明如何讀取和顯示您在上一個範例中建立的資料。

1. 在您網站的根目錄中，建立名為*DisplayData*的新檔案。
2. 以下列內容取代現有的內容： 

    [!code-cshtml[Main](working-with-files/samples/sample4.cshtml)]

    程式碼一開始會先使用這個方法呼叫，將您在上一個範例中建立的檔案讀入名為 `userData`的變數：

    [!code-css[Main](working-with-files/samples/sample5.css)]

    執行此動作的程式碼位於 `if` 語句內。 當您想要讀取檔案時，最好使用 `File.Exists` 方法來判斷檔案是否可用。 程式碼也會檢查檔案是否為空的。

    頁面的內文包含兩個 `foreach` 迴圈，一個是在另一個嵌套的。 外部 `foreach` 迴圈會從資料檔案一次取得一行。 在此情況下，程式程式碼是由檔案中&#8212;的分行符號所定義，每個資料項目都在自己的行上。 外部迴圈會在已排序的清單（`<ol>` 元素）內建立新的專案（`<li>` 元素）。

    內部迴圈會使用逗號做為分隔符號，將每個資料行分割成專案（欄位）。 （根據上一個範例，這表示每一行都包含三個欄位&#8212; ：名字、姓氏和電子郵件地址，每個都以逗號分隔）。內部迴圈也會建立 `<ul>` 清單，並針對資料行中的每個欄位顯示一個清單專案。

    此程式碼說明如何使用兩種資料類型：陣列和 `char` 的資料類型。 陣列是必要的，因為 `File.ReadAllLines` 方法會傳回資料做為陣列。 `char` 的資料類型是必要的，因為 `Split` 方法會傳回 `array`，其中的每個元素都屬於 `char`類型。 （如需陣列的詳細資訊，請參閱[使用 Razor 語法 ASP.NET Web 程式設計的簡介](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects)）。
3. 在瀏覽器中執行頁面。 系統會顯示您為先前範例輸入的資料。 

    ![[影像]](working-with-files/_static/image4.jpg)

> [!TIP] 
> 
> **顯示來自 Microsoft Excel 逗點分隔檔案的資料**
> 
> 您可以使用 Microsoft Excel，將試算表中包含的資料儲存為逗號分隔檔案（ *.csv*檔案）。 當您這麼做時，檔案會以純文字儲存，而不是以 Excel 格式儲存。 試算表中的每個資料列都會以文字檔中的分行符號分隔，而每個資料項目會以逗號分隔。 您可以使用上述範例中所示的程式碼，只要在程式碼中變更資料檔案的名稱，就能讀取 Excel 逗號分隔的檔案。

<a id="Deleting_Files"></a>
## <a name="deleting-files"></a>刪除檔案

若要從您的網站刪除檔案，您可以使用 `File.Delete` 方法。 此程式說明如何讓使用者在知道檔案名稱的情況下，從*images*資料夾中刪除影像（ *.jpg*檔案）。

> [!NOTE] 
> 
> **重要事項**在生產網站中，您通常會限制可對資料進行變更的人員。 如需如何設定成員資格，以及如何授權使用者在網站上執行工作的相關資訊，請參閱[新增 ASP.NET Web Pages 網站的安全性和成員資格](https://go.microsoft.com/fwlink/?LinkId=202904)。

1. 在網站中，建立名為*images*的子資料夾。
2. 將一個或多個 *.jpg*檔案複製到 [ *images* ] 資料夾。
3. 在網站的根目錄中，建立名為*FileDelete*的新檔案。
4. 以下列內容取代現有的內容： 

    [!code-cshtml[Main](working-with-files/samples/sample6.cshtml)]

    此頁面包含一個表單，使用者可以在其中輸入影像檔案的名稱。 它們不會輸入 *.jpg*副檔名;藉由限制此檔案名，您可以協助防止使用者刪除網站上的任意檔案。

    程式碼會讀取使用者所輸入的檔案名，然後再建立完整的路徑。 若要建立路徑，程式碼會使用目前的網站路徑（如 `Server.MapPath` 方法所傳回）、 *images*資料夾名稱、使用者提供的名稱，以及 ".jpg" 做為常值字串。

    若要刪除檔案，程式碼會呼叫 `File.Delete` 方法，並將您剛才所建立的完整路徑傳遞給它。 在標記的結尾，程式碼會顯示已刪除檔案的確認訊息。
5. 在瀏覽器中執行頁面。 

    ![[影像]](working-with-files/_static/image5.jpg)
6. 輸入要刪除的檔案名，然後按一下 [**提交**]。 如果檔案已刪除，則檔案的名稱會顯示在頁面底部。

<a id="Letting_Users_Upload_a_File"></a>
## <a name="letting-users-upload-a-file"></a>讓使用者上傳檔案

`FileUpload` helper 可讓使用者將檔案上傳到您的網站。 下列程式說明如何讓使用者上傳單一檔案。

1. 如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果您先前未新增）。
2. 在*應用程式\_資料* 資料夾中，建立新的資料夾，並將其命名為*UploadedFiles*。
3. 在根目錄中，建立名為*FileUpload*的新檔案。
4. 將頁面中的現有內容取代為下列內容： 

    [!code-cshtml[Main](working-with-files/samples/sample7.cshtml)]

    頁面的內文部分會使用 `FileUpload` helper 來建立您可能熟悉的上傳方塊和按鈕：

    ![[影像]](working-with-files/_static/image6.jpg)

    您為 `FileUpload` helper 設定的屬性會指定您想要上傳檔案的單一方塊，以及要讓 [提交] 按鈕讀取**上傳**。 （您稍後會在文章中新增更多方塊。）

    當使用者按一下 [**上傳**] 時，頁面頂端的程式碼會取得檔案並加以儲存。 通常用來從表單欄位取得值的 `Request` 物件也具有 `Files` 陣列，其中包含已上傳的檔案（或檔案）。 您可以從陣列&#8212;中的特定位置取得個別的檔案，例如，取得第一個上傳的檔案、取得 `Request.Files[0]`、取得第二個檔案、取得 `Request.Files[1]`等等。 （請記住，在程式設計中，計數通常會從零開始）。

    當您提取已上傳的檔案時，您會將它放在變數中（這裡 `uploadedFile`），以便您進行操作。 若要判斷所上傳檔案的名稱，您只需要取得其 `FileName` 屬性。 不過，當使用者上傳檔案時，`FileName` 會包含使用者的原始名稱，其中包括整個路徑。 看起來可能像這樣：

    *C:\Users\Public\Sample.txt*

    不過，您不想要所有的路徑資訊，因為這是使用者電腦上的路徑，而不是您的伺服器。 您只想要實際的檔案名（*Sample .txt*）。 您可以使用 `Path.GetFileName` 方法來去除路徑中的檔案，如下所示：

    [!code-csharp[Main](working-with-files/samples/sample8.cs)]

    `Path` 物件是一種公用程式，其中有一些方法，例如，您可以用來帶狀化路徑、合併路徑等等。

    取得已上傳檔案的名稱之後，您就可以建立新的路徑，以便在網站中儲存已上傳的檔案。 在此情況下，您會將 `Server.MapPath`、資料夾名稱（*應用程式\_Data/UploadedFiles*）和新移除的檔案名結合，以建立新的路徑。 接著，您可以呼叫已上傳檔案的 `SaveAs` 方法，以實際儲存檔案。
5. 在瀏覽器中執行頁面。 

    ![[影像]](working-with-files/_static/image7.jpg)
6. 按一下 **[流覽]** ，然後選取要上傳的檔案。 

    ![[影像]](working-with-files/_static/image8.jpg)

    [**流覽]** 按鈕旁邊的文字方塊會包含路徑和檔案位置。

    ![[影像]](working-with-files/_static/image9.jpg)
7. 按一下 [上傳]。
8. 在網站中，以滑鼠**按右鍵專案**資料夾，然後按一下 [重新整理]。
9. 開啟 [ *UploadedFiles* ] 資料夾。 您上傳的檔案位於資料夾中。 

    ![[影像]](working-with-files/_static/image10.jpg)

<a id="Letting_Users_Upload_Multiple_Files"></a>
## <a name="letting-users-upload-multiple-files"></a>讓使用者上傳多個檔案

在上述範例中，您可以讓使用者上傳一個檔案。 但是，您可以使用 `FileUpload` helper，一次上傳一個以上的檔案。 這適用于上傳相片之類的案例，一次上傳一個檔案相當繁瑣。 （您可以閱讀[使用 ASP.NET Web Pages 網站中的影像](https://go.microsoft.com/fwlink/?LinkId=202897)來上傳相片）。這個範例示範如何讓使用者一次上傳兩個，雖然您可以使用相同的技巧來上傳，而不是這麼做。

1. 如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果尚未這麼做）。
2. 建立名為*FileUploadMultiple*的新頁面。
3. 將頁面中的現有內容取代為下列內容：  

    [!code-cshtml[Main](working-with-files/samples/sample9.cshtml)]

    在此範例中，頁面主體中的 `FileUpload` helper 會設定為讓使用者根據預設上傳兩個檔案。 因為 `allowMoreFilesToBeAdded` 設定為 `true`，協助專家會轉譯一個連結，讓使用者加入更多的上傳方塊：

    ![[影像]](working-with-files/_static/image11.jpg)

    若要處理使用者上傳的檔案，程式碼會使用您在上一個範例&#8212;中所使用的基本技巧，從 `Request.Files` 取得檔案，然後加以儲存。 （包括您需要執行的各種動作，以取得正確的檔案名和路徑）。這次的創新是，使用者可能上傳多個檔案，但您不知道多個檔案。 若要找出，您可以取得 `Request.Files.Count`。

    有了這個數位，您就可以迴圈執行 `Request.Files`、輪流提取每個檔案，然後加以儲存。 當您想要透過集合迴圈執行已知的次數時，您可以使用 `for` 迴圈，如下所示：

    [!code-csharp[Main](working-with-files/samples/sample10.cs)]

    變數 `i` 只是一個暫存計數器，會從零開始到您設定的任何上限。 在此情況下，上限是檔案數目。 但是，由於計數器是從零開始，因此通常是在 ASP.NET 中計算案例，而上限實際上小於檔案計數。 （如果有三個檔案上傳，則計數為零到2）。

    `uploadedCount` 變數會總計已成功上傳並儲存的所有檔案。 這段程式碼可能會導致預期的檔案無法上傳。
4. 在瀏覽器中執行頁面。 瀏覽器會顯示頁面和它的兩個上傳方塊。
5. 選取要上傳的兩個檔案。
6. 按一下 [**新增另一個**檔案]。 此頁面會顯示新的上傳方塊。 

    ![[影像]](working-with-files/_static/image12.jpg)
7. 按一下 [上傳]。
8. 在網站中，以滑鼠**按右鍵專案**資料夾，然後按一下 [重新整理]。
9. 開啟 [ *UploadedFiles* ] 資料夾，以查看成功上傳的檔案。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他資源

[使用 ASP.NET Web Pages 網站中的影像](https://go.microsoft.com/fwlink/?LinkId=202897)

[匯出至 CSV 檔案](https://msdn.microsoft.com/library/ms155919.aspx)
