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
# <a name="working-with-files-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="a1994-103">使用 ASP.NET Web Pages （Razor）網站中的檔案</span><span class="sxs-lookup"><span data-stu-id="a1994-103">Working with Files in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="a1994-104">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a1994-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="a1994-105">本文說明如何在 ASP.NET Web Pages （Razor）網站中讀取、寫入、附加、刪除和上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-105">This article explains how to read, write, append, delete, and upload files in an ASP.NET Web Pages (Razor) site.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="a1994-106">如果您想要上傳影像並操作它們（例如，對其進行翻轉或調整大小），請參閱[使用 ASP.NET Web Pages 網站中的影像](/aspnet/web-pages/overview/ui-layouts-and-themes/9-working-with-images)。</span><span class="sxs-lookup"><span data-stu-id="a1994-106">If you want to upload images and manipulate them (for example, flip or resize them), see [Working with Images in an ASP.NET Web Pages Site](/aspnet/web-pages/overview/ui-layouts-and-themes/9-working-with-images).</span></span>
> 
> 
> <span data-ttu-id="a1994-107">**您將瞭解的內容：**</span><span class="sxs-lookup"><span data-stu-id="a1994-107">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="a1994-108">如何建立文字檔，並將資料寫入其中。</span><span class="sxs-lookup"><span data-stu-id="a1994-108">How to create a text file and write data to it.</span></span>
> - <span data-ttu-id="a1994-109">如何將資料附加至現有的檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-109">How to append data to an existing file.</span></span>
> - <span data-ttu-id="a1994-110">如何讀取檔案並從中顯示。</span><span class="sxs-lookup"><span data-stu-id="a1994-110">How to read a file and display from it.</span></span>
> - <span data-ttu-id="a1994-111">如何刪除網站中的檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-111">How to delete files from a website.</span></span>
> - <span data-ttu-id="a1994-112">如何讓使用者上傳一個檔案或多個檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-112">How to let users upload one file or multiple files.</span></span>
> 
> <span data-ttu-id="a1994-113">以下是文章中引進的 ASP.NET 程式設計功能：</span><span class="sxs-lookup"><span data-stu-id="a1994-113">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="a1994-114">`File` 物件，可提供管理檔案的方式。</span><span class="sxs-lookup"><span data-stu-id="a1994-114">The `File` object, which provides a way to manage files.</span></span>
> - <span data-ttu-id="a1994-115">`FileUpload` helper。</span><span class="sxs-lookup"><span data-stu-id="a1994-115">The `FileUpload` helper.</span></span>
> - <span data-ttu-id="a1994-116">`Path` 物件，提供可讓您操作路徑和檔案名的方法。</span><span class="sxs-lookup"><span data-stu-id="a1994-116">The `Path` object, which provides methods that let you manipulate path and file names.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a1994-117">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="a1994-117">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="a1994-118">ASP.NET Web Pages （Razor）2</span><span class="sxs-lookup"><span data-stu-id="a1994-118">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="a1994-119">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="a1994-119">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="a1994-120">本教學課程也適用于 WebMatrix 3。</span><span class="sxs-lookup"><span data-stu-id="a1994-120">This tutorial also works with WebMatrix 3.</span></span>

<a id="Creating_a_Text_File"></a>
## <a name="creating-a-text-file-and-writing-data-to-it"></a><span data-ttu-id="a1994-121">建立文字檔，並將資料寫入其中</span><span class="sxs-lookup"><span data-stu-id="a1994-121">Creating a Text File and Writing Data to It</span></span>

<span data-ttu-id="a1994-122">除了在您的網站中使用資料庫之外，您還可以使用檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-122">In addition to using a database in your website, you might work with files.</span></span> <span data-ttu-id="a1994-123">例如，您可以使用文字檔做為儲存網站資料的簡單方式。</span><span class="sxs-lookup"><span data-stu-id="a1994-123">For example, you might use text files as a simple way to store data for the site.</span></span> <span data-ttu-id="a1994-124">（用來儲存資料的文字檔，有時稱為一般檔案 *）。* 文字檔可以採用不同的格式，例如 *.txt*、 *.xml*或 *.csv* （以逗號分隔的值）。</span><span class="sxs-lookup"><span data-stu-id="a1994-124">(A text file that's used to store data is sometimes called a *flat file*.) Text files can be in different formats, like *.txt*, *.xml*, or *.csv* (comma-delimited values).</span></span>

<span data-ttu-id="a1994-125">如果您想要將資料儲存在文字檔中，您可以使用 `File.WriteAllText` 方法來指定要建立的檔案，以及要寫入資料的檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-125">If you want to store data in a text file, you can use the `File.WriteAllText` method to specify the file to create and the data to write to it.</span></span> <span data-ttu-id="a1994-126">在此程式中，您將建立一個頁面，其中包含具有三個 `input` 元素（名字、姓氏和電子郵件地址）和**提交**按鈕的簡單表單。</span><span class="sxs-lookup"><span data-stu-id="a1994-126">In this procedure, you'll create a page that contains a simple form with three `input` elements (first name, last name, and email address) and a **Submit** button.</span></span> <span data-ttu-id="a1994-127">當使用者提交表單時，您會將使用者的輸入儲存在文字檔中。</span><span class="sxs-lookup"><span data-stu-id="a1994-127">When the user submits the form, you'll store the user's input in a text file.</span></span>

1. <span data-ttu-id="a1994-128">建立名為 [*應用程式\_資料*] 的新資料夾（如果尚未存在）。</span><span class="sxs-lookup"><span data-stu-id="a1994-128">Create a new folder named *App\_Data*, if it doesn't exist already.</span></span>
2. <span data-ttu-id="a1994-129">在您網站的根目錄中，建立名為*UserData*的新檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-129">At the root of your website, create a new file named *UserData.cshtml*.</span></span>
3. <span data-ttu-id="a1994-130">以下列內容取代現有的內容：</span><span class="sxs-lookup"><span data-stu-id="a1994-130">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample1.cshtml)]

    <span data-ttu-id="a1994-131">HTML 標籤會建立具有三個文字方塊的表單。</span><span class="sxs-lookup"><span data-stu-id="a1994-131">The HTML markup creates the form with the three text boxes.</span></span> <span data-ttu-id="a1994-132">在程式碼中，您可以使用 `IsPost` 屬性來判斷頁面是否已提交，然後再開始處理。</span><span class="sxs-lookup"><span data-stu-id="a1994-132">In the code, you use the `IsPost` property to determine whether the page has been submitted before you start processing.</span></span>

    <span data-ttu-id="a1994-133">第一個工作是取得使用者輸入，並將它指派給變數。</span><span class="sxs-lookup"><span data-stu-id="a1994-133">The first task is to get the user input and assign it to variables.</span></span> <span data-ttu-id="a1994-134">然後，此程式碼會將個別變數的值串連成一個逗號分隔的字串，然後儲存在不同的變數中。</span><span class="sxs-lookup"><span data-stu-id="a1994-134">The code then concatenates the values of the separate variables into one comma-delimited string, which is then stored in a different variable.</span></span> <span data-ttu-id="a1994-135">請注意，逗號分隔符號是包含在引號（"，"）中的字串，因為您實際上是在要建立的大字串中內嵌一個逗號。</span><span class="sxs-lookup"><span data-stu-id="a1994-135">Notice that the comma separator is a string contained in quotation marks (","), because you're literally embedding a comma into the big string that you're creating.</span></span> <span data-ttu-id="a1994-136">在您一起串連的資料結尾處，您會新增 `Environment.NewLine`。</span><span class="sxs-lookup"><span data-stu-id="a1994-136">At the end of the data that you concatenate together, you add `Environment.NewLine`.</span></span> <span data-ttu-id="a1994-137">這會加上分行符號（換行字元）。</span><span class="sxs-lookup"><span data-stu-id="a1994-137">This adds a line break (a newline character).</span></span> <span data-ttu-id="a1994-138">您要使用此串連來建立的內容，就是如下所示的字串：</span><span class="sxs-lookup"><span data-stu-id="a1994-138">What you're creating with all this concatenation is a string that looks like this:</span></span>

    [!code-css[Main](working-with-files/samples/sample2.css)]

    <span data-ttu-id="a1994-139">（結尾處有不可見的分行符號）。</span><span class="sxs-lookup"><span data-stu-id="a1994-139">(With an invisible line break at the end.)</span></span>

    <span data-ttu-id="a1994-140">接著，您要建立一個變數（`dataFile`），其中包含要儲存資料的檔案位置和名稱。</span><span class="sxs-lookup"><span data-stu-id="a1994-140">You then create a variable (`dataFile`) that contains the location and name of the file to store the data in.</span></span> <span data-ttu-id="a1994-141">設定位置需要一些特殊的處理。</span><span class="sxs-lookup"><span data-stu-id="a1994-141">Setting the location requires some special handling.</span></span> <span data-ttu-id="a1994-142">在網站中，將程式碼參考到 web 伺服器上檔案的絕對路徑（例如*C:\Folder\File.txt* ）是不好的作法。</span><span class="sxs-lookup"><span data-stu-id="a1994-142">In websites, it's a bad practice to refer in code to absolute paths like *C:\Folder\File.txt* for files on the web server.</span></span> <span data-ttu-id="a1994-143">如果移動網站，絕對路徑會錯誤。</span><span class="sxs-lookup"><span data-stu-id="a1994-143">If a website is moved, an absolute path will be wrong.</span></span> <span data-ttu-id="a1994-144">此外，對於託管的網站（而不是在您自己的電腦上），您通常甚至不知道撰寫程式碼時的正確路徑。</span><span class="sxs-lookup"><span data-stu-id="a1994-144">Moreover, for a hosted site (as opposed to on your own computer) you typically don't even know what the correct path is when you're writing the code.</span></span>

    <span data-ttu-id="a1994-145">但有時候（像現在是寫入檔案）需要完整的路徑。</span><span class="sxs-lookup"><span data-stu-id="a1994-145">But sometimes (like now, for writing a file) you do need a complete path.</span></span> <span data-ttu-id="a1994-146">解決方案是使用 `Server` 物件的 `MapPath` 方法。</span><span class="sxs-lookup"><span data-stu-id="a1994-146">The solution is to use the `MapPath` method of the `Server` object.</span></span> <span data-ttu-id="a1994-147">這會傳回您網站的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="a1994-147">This returns the complete path to your website.</span></span> <span data-ttu-id="a1994-148">若要取得網站根目錄的路徑，您可以使用者 `~` 操作員（represen 網站的虛擬根目錄）來 `MapPath`。</span><span class="sxs-lookup"><span data-stu-id="a1994-148">To get the path for the website root, you user the `~` operator (to represen the site's virtual root) to `MapPath`.</span></span> <span data-ttu-id="a1994-149">（您也可以將子資料夾名稱傳遞給它，例如 *~/App\_Data/* ）來取得該子資料夾的路徑）。接著，您可以將其他資訊串連到方法傳回的任何內容，以便建立完整的路徑。</span><span class="sxs-lookup"><span data-stu-id="a1994-149">(You can also pass a subfolder name to it, like *~/App\_Data/*, to get the path for that subfolder.) You can then concatenate additional information onto whatever the method returns in order to create a complete path.</span></span> <span data-ttu-id="a1994-150">在此範例中，您會新增一個檔案名。</span><span class="sxs-lookup"><span data-stu-id="a1994-150">In this example, you add a file name.</span></span> <span data-ttu-id="a1994-151">（您可以在[使用 Razor 語法進行 ASP.NET Web Pages 程式設計簡介](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)中，閱讀更多有關如何使用檔案和資料夾路徑的資訊。）</span><span class="sxs-lookup"><span data-stu-id="a1994-151">(You can read more about how to work with file and folder paths in [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span></span>

    <span data-ttu-id="a1994-152">檔案會儲存在*應用程式\_Data*資料夾中。</span><span class="sxs-lookup"><span data-stu-id="a1994-152">The file is saved in the *App\_Data* folder.</span></span> <span data-ttu-id="a1994-153">此資料夾是 ASP.NET 中用來儲存資料檔案的特殊資料夾，如在[ASP.NET Web Pages 網站中使用資料庫簡介](https://go.microsoft.com/fwlink/?LinkId=195209)中所述。</span><span class="sxs-lookup"><span data-stu-id="a1994-153">This folder is a special folder in ASP.NET that's used to store data files, as described in [Introduction to Working with a Database in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=195209).</span></span>

    <span data-ttu-id="a1994-154">`File` 物件的 `WriteAllText` 方法會將資料寫入至檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-154">The `WriteAllText` method of the `File` object writes the data to the file.</span></span> <span data-ttu-id="a1994-155">這個方法會採用兩個參數：要寫入之檔案的名稱（路徑），以及要寫入的實際資料。</span><span class="sxs-lookup"><span data-stu-id="a1994-155">This method takes two parameters: the name (with path) of the file to write to, and the actual data to write.</span></span> <span data-ttu-id="a1994-156">請注意，第一個參數的名稱會以 `@` 字元做為前置詞。</span><span class="sxs-lookup"><span data-stu-id="a1994-156">Notice that the name of the first parameter has an `@` character as a prefix.</span></span> <span data-ttu-id="a1994-157">這會告訴 ASP.NET 您要提供逐字字串常值，而且不應該以特殊方式解讀 "/" 這類的字元。</span><span class="sxs-lookup"><span data-stu-id="a1994-157">This tells ASP.NET that you're providing a verbatim string literal, and that characters like "/" should not be interpreted in special ways.</span></span> <span data-ttu-id="a1994-158">（如需詳細資訊，請參閱[使用 Razor 語法 ASP.NET Web 程式設計的簡介](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)）。</span><span class="sxs-lookup"><span data-stu-id="a1994-158">(For more information, see [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span></span>

    > [!NOTE]
    > <span data-ttu-id="a1994-159">為了讓您的程式碼將檔案儲存在*應用程式\_Data*資料夾中，應用程式需要該資料夾的讀寫許可權。</span><span class="sxs-lookup"><span data-stu-id="a1994-159">In order for your code to save files in the *App\_Data* folder, the application needs read-write permissions for that folder.</span></span> <span data-ttu-id="a1994-160">在您的開發電腦上，這通常不是問題。</span><span class="sxs-lookup"><span data-stu-id="a1994-160">On your development computer this is not typically an issue.</span></span> <span data-ttu-id="a1994-161">不過，當您將網站發佈至主控提供者的 web 伺服器時，您可能需要明確地設定這些許可權。</span><span class="sxs-lookup"><span data-stu-id="a1994-161">However, when you publish your site to a hosting provider's web server, you might need to explicitly set those permissions.</span></span> <span data-ttu-id="a1994-162">如果您在主控提供者的伺服器上執行此程式碼，並收到錯誤，請洽詢主機服務提供者，以瞭解如何設定這些許可權。</span><span class="sxs-lookup"><span data-stu-id="a1994-162">If you run this code on a hosting provider's server and get errors, check with the hosting provider to find out how to set those permissions.</span></span>

- <span data-ttu-id="a1994-163">在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="a1994-163">Run the page in a browser.</span></span> 

    ![](working-with-files/_static/image1.jpg)
- <span data-ttu-id="a1994-164">在欄位中輸入值，然後按一下 [**提交**]。</span><span class="sxs-lookup"><span data-stu-id="a1994-164">Enter values into the fields and then click **Submit**.</span></span>
- <span data-ttu-id="a1994-165">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="a1994-165">Close the browser.</span></span>
- <span data-ttu-id="a1994-166">返回專案並重新整理視圖。</span><span class="sxs-lookup"><span data-stu-id="a1994-166">Return to the project and refresh the view.</span></span>
- <span data-ttu-id="a1994-167">開啟 [*資料 .txt* ] 檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-167">Open the *data.txt* file.</span></span> <span data-ttu-id="a1994-168">您在表單中提交的資料會在檔案中。</span><span class="sxs-lookup"><span data-stu-id="a1994-168">The data you submitted in the form is in the file.</span></span> 

    ![[影像]](working-with-files/_static/image2.jpg)
- <span data-ttu-id="a1994-170">關閉*資料 .txt*檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-170">Close the *data.txt* file.</span></span>

<a id="Appending_Data"></a>
## <a name="appending-data-to-an-existing-file"></a><span data-ttu-id="a1994-171">將資料附加至現有的檔案</span><span class="sxs-lookup"><span data-stu-id="a1994-171">Appending Data to an Existing File</span></span>

<span data-ttu-id="a1994-172">在上一個範例中，您使用 `WriteAllText` 來建立一個文字檔，其中只有一個資料片段。</span><span class="sxs-lookup"><span data-stu-id="a1994-172">In the previous example, you used `WriteAllText` to create a text file that's got just one piece of data in it.</span></span> <span data-ttu-id="a1994-173">如果您再次呼叫方法並傳遞相同的檔案名，則會完全覆寫現有的檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-173">If you call the method again and pass it the same file name, the existing file is completely overwritten.</span></span> <span data-ttu-id="a1994-174">不過，在建立檔案之後，您通常會想要將新的資料加入至檔案結尾。</span><span class="sxs-lookup"><span data-stu-id="a1994-174">However, after you've created a file you often want to add new data to the end of the file.</span></span> <span data-ttu-id="a1994-175">您可以使用 `File` 物件的 `AppendAllText` 方法來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="a1994-175">You can do that using the `AppendAllText` method of the `File` object.</span></span>

1. <span data-ttu-id="a1994-176">在網站中，建立*UserData*檔案的複本，並將複本命名為*UserDataMultiple*。</span><span class="sxs-lookup"><span data-stu-id="a1994-176">In the website, make a copy of the *UserData.cshtml* file and name the copy *UserDataMultiple.cshtml*.</span></span>
2. <span data-ttu-id="a1994-177">使用下列程式碼區塊取代開頭 `<!DOCTYPE html>` 標記之前的程式碼區塊：</span><span class="sxs-lookup"><span data-stu-id="a1994-177">Replace the code block before the opening `<!DOCTYPE html>` tag with the following code block:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample3.cshtml)]

    <span data-ttu-id="a1994-178">此程式碼在上一個範例中有一項變更。</span><span class="sxs-lookup"><span data-stu-id="a1994-178">This code has one change in it from the previous example.</span></span> <span data-ttu-id="a1994-179">它不會使用 `WriteAllText`，而是使用 `the AppendAllText` 方法。</span><span class="sxs-lookup"><span data-stu-id="a1994-179">Instead of using `WriteAllText`, it uses `the AppendAllText` method.</span></span> <span data-ttu-id="a1994-180">方法很類似，不同之處在于 `AppendAllText` 會將資料新增至檔案結尾。</span><span class="sxs-lookup"><span data-stu-id="a1994-180">The methods are similar, except that `AppendAllText` adds the data to the end of the file.</span></span> <span data-ttu-id="a1994-181">如同 `WriteAllText`，`AppendAllText` 會建立檔案（如果尚未存在）。</span><span class="sxs-lookup"><span data-stu-id="a1994-181">As with `WriteAllText`, `AppendAllText` creates the file if it doesn't already exist.</span></span>
3. <span data-ttu-id="a1994-182">在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="a1994-182">Run the page in a browser.</span></span>
4. <span data-ttu-id="a1994-183">輸入欄位的值，然後按一下 [**提交**]。</span><span class="sxs-lookup"><span data-stu-id="a1994-183">Enter values for the fields and then click **Submit**.</span></span>
5. <span data-ttu-id="a1994-184">請新增更多資料，然後再次提交表單。</span><span class="sxs-lookup"><span data-stu-id="a1994-184">Add more data and submit the form again.</span></span>
6. <span data-ttu-id="a1994-185">返回您的專案，以滑鼠**按右鍵專案**資料夾，然後按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="a1994-185">Return to your project, right-click the project folder, and then click **Refresh**.</span></span>
7. <span data-ttu-id="a1994-186">開啟 [*資料 .txt* ] 檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-186">Open the *data.txt* file.</span></span> <span data-ttu-id="a1994-187">它現在包含您剛輸入的新資料。</span><span class="sxs-lookup"><span data-stu-id="a1994-187">It now contains the new data that you just entered.</span></span> 

    ![[影像]](working-with-files/_static/image3.jpg)

<a id="Reading_and_Displaying_Data"></a>
## <a name="reading-and-displaying-data-from-a-file"></a><span data-ttu-id="a1994-189">讀取和顯示檔案中的資料</span><span class="sxs-lookup"><span data-stu-id="a1994-189">Reading and Displaying Data from a File</span></span>

<span data-ttu-id="a1994-190">即使您不需要將資料寫入文字檔，您有時可能需要讀取其中一個資料。</span><span class="sxs-lookup"><span data-stu-id="a1994-190">Even if you don't need to write data to a text file, you'll probably sometimes need to read data from one.</span></span> <span data-ttu-id="a1994-191">若要這樣做，您可以再次使用 `File` 物件。</span><span class="sxs-lookup"><span data-stu-id="a1994-191">To do this, you can again use the `File` object.</span></span> <span data-ttu-id="a1994-192">您可以使用 `File` 物件來個別讀取每一行（以分行符號分隔）或讀取個別專案（不論它們的分隔方式為何）。</span><span class="sxs-lookup"><span data-stu-id="a1994-192">You can use the `File` object to read each line individually (separated by line breaks) or to read individual item no matter how they're separated.</span></span>

<span data-ttu-id="a1994-193">此程式說明如何讀取和顯示您在上一個範例中建立的資料。</span><span class="sxs-lookup"><span data-stu-id="a1994-193">This procedure shows you how to read and display the data that you created in the previous example.</span></span>

1. <span data-ttu-id="a1994-194">在您網站的根目錄中，建立名為*DisplayData*的新檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-194">At the root of your website, create a new file named *DisplayData.cshtml*.</span></span>
2. <span data-ttu-id="a1994-195">以下列內容取代現有的內容：</span><span class="sxs-lookup"><span data-stu-id="a1994-195">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample4.cshtml)]

    <span data-ttu-id="a1994-196">程式碼一開始會先使用這個方法呼叫，將您在上一個範例中建立的檔案讀入名為 `userData`的變數：</span><span class="sxs-lookup"><span data-stu-id="a1994-196">The code starts by reading the file that you created in the previous example into a variable named `userData`, using this method call:</span></span>

    [!code-css[Main](working-with-files/samples/sample5.css)]

    <span data-ttu-id="a1994-197">執行此動作的程式碼位於 `if` 語句內。</span><span class="sxs-lookup"><span data-stu-id="a1994-197">The code to do this is inside an `if` statement.</span></span> <span data-ttu-id="a1994-198">當您想要讀取檔案時，最好使用 `File.Exists` 方法來判斷檔案是否可用。</span><span class="sxs-lookup"><span data-stu-id="a1994-198">When you want to read a file, it's a good idea to use the `File.Exists` method to determine first whether the file is available.</span></span> <span data-ttu-id="a1994-199">程式碼也會檢查檔案是否為空的。</span><span class="sxs-lookup"><span data-stu-id="a1994-199">The code also checks whether the file is empty.</span></span>

    <span data-ttu-id="a1994-200">頁面的內文包含兩個 `foreach` 迴圈，一個是在另一個嵌套的。</span><span class="sxs-lookup"><span data-stu-id="a1994-200">The body of the page contains two `foreach` loops, one nested inside the other.</span></span> <span data-ttu-id="a1994-201">外部 `foreach` 迴圈會從資料檔案一次取得一行。</span><span class="sxs-lookup"><span data-stu-id="a1994-201">The outer `foreach` loop gets one line at a time from the data file.</span></span> <span data-ttu-id="a1994-202">在此情況下，程式程式碼是由檔案中&#8212;的分行符號所定義，每個資料項目都在自己的行上。</span><span class="sxs-lookup"><span data-stu-id="a1994-202">In this case, the lines are defined by line breaks in the file &#8212; that is, each data item is on its own line.</span></span> <span data-ttu-id="a1994-203">外部迴圈會在已排序的清單（`<ol>` 元素）內建立新的專案（`<li>` 元素）。</span><span class="sxs-lookup"><span data-stu-id="a1994-203">The outer loop creates a new item (`<li>` element) inside an ordered list (`<ol>` element).</span></span>

    <span data-ttu-id="a1994-204">內部迴圈會使用逗號做為分隔符號，將每個資料行分割成專案（欄位）。</span><span class="sxs-lookup"><span data-stu-id="a1994-204">The inner loop splits each data line into items (fields) using a comma as a delimiter.</span></span> <span data-ttu-id="a1994-205">（根據上一個範例，這表示每一行都包含三個欄位&#8212; ：名字、姓氏和電子郵件地址，每個都以逗號分隔）。內部迴圈也會建立 `<ul>` 清單，並針對資料行中的每個欄位顯示一個清單專案。</span><span class="sxs-lookup"><span data-stu-id="a1994-205">(Based on the previous example, this means that each line contains three fields &#8212; the first name, last name, and email address, each separated by a comma.) The inner loop also creates a `<ul>` list and displays one list item for each field in the data line.</span></span>

    <span data-ttu-id="a1994-206">此程式碼說明如何使用兩種資料類型：陣列和 `char` 的資料類型。</span><span class="sxs-lookup"><span data-stu-id="a1994-206">The code illustrates how to use two data types, an array and the `char` data type.</span></span> <span data-ttu-id="a1994-207">陣列是必要的，因為 `File.ReadAllLines` 方法會傳回資料做為陣列。</span><span class="sxs-lookup"><span data-stu-id="a1994-207">The array is required because the `File.ReadAllLines` method returns data as an array.</span></span> <span data-ttu-id="a1994-208">`char` 的資料類型是必要的，因為 `Split` 方法會傳回 `array`，其中的每個元素都屬於 `char`類型。</span><span class="sxs-lookup"><span data-stu-id="a1994-208">The `char` data type is required because the `Split` method returns an `array` in which each element is of the type `char`.</span></span> <span data-ttu-id="a1994-209">（如需陣列的詳細資訊，請參閱[使用 Razor 語法 ASP.NET Web 程式設計的簡介](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects)）。</span><span class="sxs-lookup"><span data-stu-id="a1994-209">(For information about arrays, see [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects).)</span></span>
3. <span data-ttu-id="a1994-210">在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="a1994-210">Run the page in a browser.</span></span> <span data-ttu-id="a1994-211">系統會顯示您為先前範例輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="a1994-211">The data you entered for the previous examples is displayed.</span></span> 

    ![[影像]](working-with-files/_static/image4.jpg)

> [!TIP] 
> 
> <span data-ttu-id="a1994-213">**顯示來自 Microsoft Excel 逗點分隔檔案的資料**</span><span class="sxs-lookup"><span data-stu-id="a1994-213">**Displaying Data from a Microsoft Excel Comma-Delimited File**</span></span>
> 
> <span data-ttu-id="a1994-214">您可以使用 Microsoft Excel，將試算表中包含的資料儲存為逗號分隔檔案（ *.csv*檔案）。</span><span class="sxs-lookup"><span data-stu-id="a1994-214">You can use Microsoft Excel to save the data contained in a spreadsheet as a comma-delimited file (*.csv* file).</span></span> <span data-ttu-id="a1994-215">當您這麼做時，檔案會以純文字儲存，而不是以 Excel 格式儲存。</span><span class="sxs-lookup"><span data-stu-id="a1994-215">When you do, the file is saved in plain text, not in Excel format.</span></span> <span data-ttu-id="a1994-216">試算表中的每個資料列都會以文字檔中的分行符號分隔，而每個資料項目會以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="a1994-216">Each row in the spreadsheet is separated by a line break in the text file, and each data item is separated by a comma.</span></span> <span data-ttu-id="a1994-217">您可以使用上述範例中所示的程式碼，只要在程式碼中變更資料檔案的名稱，就能讀取 Excel 逗號分隔的檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-217">You can use the code shown in the previous example to read an Excel comma-delimited file just by changing the name of the data file in your code.</span></span>

<a id="Deleting_Files"></a>
## <a name="deleting-files"></a><span data-ttu-id="a1994-218">刪除檔案</span><span class="sxs-lookup"><span data-stu-id="a1994-218">Deleting Files</span></span>

<span data-ttu-id="a1994-219">若要從您的網站刪除檔案，您可以使用 `File.Delete` 方法。</span><span class="sxs-lookup"><span data-stu-id="a1994-219">To delete files from your website, you can use the `File.Delete` method.</span></span> <span data-ttu-id="a1994-220">此程式說明如何讓使用者在知道檔案名稱的情況下，從*images*資料夾中刪除影像（ *.jpg*檔案）。</span><span class="sxs-lookup"><span data-stu-id="a1994-220">This procedure shows how to let users delete an image (*.jpg* file) from an *images* folder if they know the name of the file.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="a1994-221">**重要事項**在生產網站中，您通常會限制可對資料進行變更的人員。</span><span class="sxs-lookup"><span data-stu-id="a1994-221">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="a1994-222">如需如何設定成員資格，以及如何授權使用者在網站上執行工作的相關資訊，請參閱[新增 ASP.NET Web Pages 網站的安全性和成員資格](https://go.microsoft.com/fwlink/?LinkId=202904)。</span><span class="sxs-lookup"><span data-stu-id="a1994-222">For information about how to set up membership and about ways to authorize users to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>

1. <span data-ttu-id="a1994-223">在網站中，建立名為*images*的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="a1994-223">In the website, create a subfolder named *images*.</span></span>
2. <span data-ttu-id="a1994-224">將一個或多個 *.jpg*檔案複製到 [ *images* ] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="a1994-224">Copy one or more *.jpg* files into the *images* folder.</span></span>
3. <span data-ttu-id="a1994-225">在網站的根目錄中，建立名為*FileDelete*的新檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-225">In the root of the website, create a new file named *FileDelete.cshtml*.</span></span>
4. <span data-ttu-id="a1994-226">以下列內容取代現有的內容：</span><span class="sxs-lookup"><span data-stu-id="a1994-226">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample6.cshtml)]

    <span data-ttu-id="a1994-227">此頁面包含一個表單，使用者可以在其中輸入影像檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="a1994-227">This page contains a form where users can enter the name of an image file.</span></span> <span data-ttu-id="a1994-228">它們不會輸入 *.jpg*副檔名;藉由限制此檔案名，您可以協助防止使用者刪除網站上的任意檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-228">They don't enter the *.jpg* file-name extension; by restricting the file name like this, you help prevents users from deleting arbitrary files on your site.</span></span>

    <span data-ttu-id="a1994-229">程式碼會讀取使用者所輸入的檔案名，然後再建立完整的路徑。</span><span class="sxs-lookup"><span data-stu-id="a1994-229">The code reads the file name that the user has entered and then constructs a complete path.</span></span> <span data-ttu-id="a1994-230">若要建立路徑，程式碼會使用目前的網站路徑（如 `Server.MapPath` 方法所傳回）、 *images*資料夾名稱、使用者提供的名稱，以及 ".jpg" 做為常值字串。</span><span class="sxs-lookup"><span data-stu-id="a1994-230">To create the path, the code uses the current website path (as returned by the `Server.MapPath` method), the *images* folder name, the name that the user has provided, and ".jpg" as a literal string.</span></span>

    <span data-ttu-id="a1994-231">若要刪除檔案，程式碼會呼叫 `File.Delete` 方法，並將您剛才所建立的完整路徑傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="a1994-231">To delete the file, the code calls the `File.Delete` method, passing it the full path that you just constructed.</span></span> <span data-ttu-id="a1994-232">在標記的結尾，程式碼會顯示已刪除檔案的確認訊息。</span><span class="sxs-lookup"><span data-stu-id="a1994-232">At the end of the markup, code displays a confirmation message that the file was deleted.</span></span>
5. <span data-ttu-id="a1994-233">在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="a1994-233">Run the page in a browser.</span></span> 

    ![[影像]](working-with-files/_static/image5.jpg)
6. <span data-ttu-id="a1994-235">輸入要刪除的檔案名，然後按一下 [**提交**]。</span><span class="sxs-lookup"><span data-stu-id="a1994-235">Enter the name of the file to delete and then click **Submit**.</span></span> <span data-ttu-id="a1994-236">如果檔案已刪除，則檔案的名稱會顯示在頁面底部。</span><span class="sxs-lookup"><span data-stu-id="a1994-236">If the file was deleted, the name of the file is displayed at the bottom of the page.</span></span>

<a id="Letting_Users_Upload_a_File"></a>
## <a name="letting-users-upload-a-file"></a><span data-ttu-id="a1994-237">讓使用者上傳檔案</span><span class="sxs-lookup"><span data-stu-id="a1994-237">Letting Users Upload a File</span></span>

<span data-ttu-id="a1994-238">`FileUpload` helper 可讓使用者將檔案上傳到您的網站。</span><span class="sxs-lookup"><span data-stu-id="a1994-238">The `FileUpload` helper lets users upload files to your website.</span></span> <span data-ttu-id="a1994-239">下列程式說明如何讓使用者上傳單一檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-239">The procedure below shows you how to let users upload a single file.</span></span>

1. <span data-ttu-id="a1994-240">如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果您先前未新增）。</span><span class="sxs-lookup"><span data-stu-id="a1994-240">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you didn't add it previously.</span></span>
2. <span data-ttu-id="a1994-241">在*應用程式\_資料* 資料夾中，建立新的資料夾，並將其命名為*UploadedFiles*。</span><span class="sxs-lookup"><span data-stu-id="a1994-241">In the *App\_Data* folder, create a new a folder and name it *UploadedFiles*.</span></span>
3. <span data-ttu-id="a1994-242">在根目錄中，建立名為*FileUpload*的新檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-242">In the root, create a new file named *FileUpload.cshtml*.</span></span>
4. <span data-ttu-id="a1994-243">將頁面中的現有內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="a1994-243">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample7.cshtml)]

    <span data-ttu-id="a1994-244">頁面的內文部分會使用 `FileUpload` helper 來建立您可能熟悉的上傳方塊和按鈕：</span><span class="sxs-lookup"><span data-stu-id="a1994-244">The body portion of the page uses the `FileUpload` helper to create the upload box and buttons that you're probably familiar with:</span></span>

    ![[影像]](working-with-files/_static/image6.jpg)

    <span data-ttu-id="a1994-246">您為 `FileUpload` helper 設定的屬性會指定您想要上傳檔案的單一方塊，以及要讓 [提交] 按鈕讀取**上傳**。</span><span class="sxs-lookup"><span data-stu-id="a1994-246">The properties that you set for the `FileUpload` helper specify that you want a single box for the file to upload and that you want the submit button to read **Upload**.</span></span> <span data-ttu-id="a1994-247">（您稍後會在文章中新增更多方塊。）</span><span class="sxs-lookup"><span data-stu-id="a1994-247">(You'll add more boxes later in the article.)</span></span>

    <span data-ttu-id="a1994-248">當使用者按一下 [**上傳**] 時，頁面頂端的程式碼會取得檔案並加以儲存。</span><span class="sxs-lookup"><span data-stu-id="a1994-248">When the user clicks **Upload**, the code at the top of the page gets the file and saves it.</span></span> <span data-ttu-id="a1994-249">通常用來從表單欄位取得值的 `Request` 物件也具有 `Files` 陣列，其中包含已上傳的檔案（或檔案）。</span><span class="sxs-lookup"><span data-stu-id="a1994-249">The `Request` object that you normally use to get values from form fields also has a `Files` array that contains the file (or files) that have been uploaded.</span></span> <span data-ttu-id="a1994-250">您可以從陣列&#8212;中的特定位置取得個別的檔案，例如，取得第一個上傳的檔案、取得 `Request.Files[0]`、取得第二個檔案、取得 `Request.Files[1]`等等。</span><span class="sxs-lookup"><span data-stu-id="a1994-250">You can get individual files out of specific positions in the array &#8212; for example, to get the first uploaded file, you get `Request.Files[0]`, to get the second file, you get `Request.Files[1]`, and so on.</span></span> <span data-ttu-id="a1994-251">（請記住，在程式設計中，計數通常會從零開始）。</span><span class="sxs-lookup"><span data-stu-id="a1994-251">(Remember that in programming, counting usually starts at zero.)</span></span>

    <span data-ttu-id="a1994-252">當您提取已上傳的檔案時，您會將它放在變數中（這裡 `uploadedFile`），以便您進行操作。</span><span class="sxs-lookup"><span data-stu-id="a1994-252">When you fetch an uploaded file, you put it in a variable (here, `uploadedFile`) so that you can manipulate it.</span></span> <span data-ttu-id="a1994-253">若要判斷所上傳檔案的名稱，您只需要取得其 `FileName` 屬性。</span><span class="sxs-lookup"><span data-stu-id="a1994-253">To determine the name of the uploaded file, you just get its `FileName` property.</span></span> <span data-ttu-id="a1994-254">不過，當使用者上傳檔案時，`FileName` 會包含使用者的原始名稱，其中包括整個路徑。</span><span class="sxs-lookup"><span data-stu-id="a1994-254">However, when the user uploads a file, `FileName` contains the user's original name, which includes the entire path.</span></span> <span data-ttu-id="a1994-255">看起來可能像這樣：</span><span class="sxs-lookup"><span data-stu-id="a1994-255">It might look like this:</span></span>

    <span data-ttu-id="a1994-256">*C:\Users\Public\Sample.txt*</span><span class="sxs-lookup"><span data-stu-id="a1994-256">*C:\Users\Public\Sample.txt*</span></span>

    <span data-ttu-id="a1994-257">不過，您不想要所有的路徑資訊，因為這是使用者電腦上的路徑，而不是您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="a1994-257">You don't want all that path information, though, because that's the path on the user's computer, not for your server.</span></span> <span data-ttu-id="a1994-258">您只想要實際的檔案名（*Sample .txt*）。</span><span class="sxs-lookup"><span data-stu-id="a1994-258">You just want the actual file name (*Sample.txt*).</span></span> <span data-ttu-id="a1994-259">您可以使用 `Path.GetFileName` 方法來去除路徑中的檔案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a1994-259">You can strip out just the file from a path by using the `Path.GetFileName` method, like this:</span></span>

    [!code-csharp[Main](working-with-files/samples/sample8.cs)]

    <span data-ttu-id="a1994-260">`Path` 物件是一種公用程式，其中有一些方法，例如，您可以用來帶狀化路徑、合併路徑等等。</span><span class="sxs-lookup"><span data-stu-id="a1994-260">The `Path` object is a utility that has a number of methods like this that you can use to strip paths, combine paths, and so on.</span></span>

    <span data-ttu-id="a1994-261">取得已上傳檔案的名稱之後，您就可以建立新的路徑，以便在網站中儲存已上傳的檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-261">Once you've gotten the name of the uploaded file, you can build a new path for where you want to store the uploaded file in your website.</span></span> <span data-ttu-id="a1994-262">在此情況下，您會將 `Server.MapPath`、資料夾名稱（*應用程式\_Data/UploadedFiles*）和新移除的檔案名結合，以建立新的路徑。</span><span class="sxs-lookup"><span data-stu-id="a1994-262">In this case, you combine `Server.MapPath`, the folder names (*App\_Data/UploadedFiles*), and the newly stripped file name to create a new path.</span></span> <span data-ttu-id="a1994-263">接著，您可以呼叫已上傳檔案的 `SaveAs` 方法，以實際儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-263">You can then call the uploaded file's `SaveAs` method to actually save the file.</span></span>
5. <span data-ttu-id="a1994-264">在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="a1994-264">Run the page in a browser.</span></span> 

    ![[影像]](working-with-files/_static/image7.jpg)
6. <span data-ttu-id="a1994-266">按一下 **[流覽]** ，然後選取要上傳的檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-266">Click **Browse** and then select a file to upload.</span></span> 

    ![[影像]](working-with-files/_static/image8.jpg)

    <span data-ttu-id="a1994-268">[**流覽]** 按鈕旁邊的文字方塊會包含路徑和檔案位置。</span><span class="sxs-lookup"><span data-stu-id="a1994-268">The text box next to the **Browse** button will contain the path and file location.</span></span>

    ![[影像]](working-with-files/_static/image9.jpg)
7. <span data-ttu-id="a1994-270">按一下 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="a1994-270">Click **Upload**.</span></span>
8. <span data-ttu-id="a1994-271">在網站中，以滑鼠**按右鍵專案**資料夾，然後按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="a1994-271">In the website, right-click the project folder and then click **Refresh**.</span></span>
9. <span data-ttu-id="a1994-272">開啟 [ *UploadedFiles* ] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="a1994-272">Open the *UploadedFiles* folder.</span></span> <span data-ttu-id="a1994-273">您上傳的檔案位於資料夾中。</span><span class="sxs-lookup"><span data-stu-id="a1994-273">The file that you uploaded is in the folder.</span></span> 

    ![[影像]](working-with-files/_static/image10.jpg)

<a id="Letting_Users_Upload_Multiple_Files"></a>
## <a name="letting-users-upload-multiple-files"></a><span data-ttu-id="a1994-275">讓使用者上傳多個檔案</span><span class="sxs-lookup"><span data-stu-id="a1994-275">Letting Users Upload Multiple Files</span></span>

<span data-ttu-id="a1994-276">在上述範例中，您可以讓使用者上傳一個檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-276">In the previous example, you let users upload one file.</span></span> <span data-ttu-id="a1994-277">但是，您可以使用 `FileUpload` helper，一次上傳一個以上的檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-277">But you can use the `FileUpload` helper to upload more than one file at a time.</span></span> <span data-ttu-id="a1994-278">這適用于上傳相片之類的案例，一次上傳一個檔案相當繁瑣。</span><span class="sxs-lookup"><span data-stu-id="a1994-278">This is handy for scenarios like uploading photos, where uploading one file at a time is tedious.</span></span> <span data-ttu-id="a1994-279">（您可以閱讀[使用 ASP.NET Web Pages 網站中的影像](https://go.microsoft.com/fwlink/?LinkId=202897)來上傳相片）。這個範例示範如何讓使用者一次上傳兩個，雖然您可以使用相同的技巧來上傳，而不是這麼做。</span><span class="sxs-lookup"><span data-stu-id="a1994-279">(You can read about uploading photos in [Working with Images in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202897).) This example shows how to let users upload two at a time, although you can use the same technique to upload more than that.</span></span>

1. <span data-ttu-id="a1994-280">如在[ASP.NET Web Pages 網站中安裝協助程式](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，將 ASP.NET Web Helper 程式庫新增至您的網站（如果尚未這麼做）。</span><span class="sxs-lookup"><span data-stu-id="a1994-280">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="a1994-281">建立名為*FileUploadMultiple*的新頁面。</span><span class="sxs-lookup"><span data-stu-id="a1994-281">Create a new page named *FileUploadMultiple.cshtml*.</span></span>
3. <span data-ttu-id="a1994-282">將頁面中的現有內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="a1994-282">Replace the existing content in the page with the following:</span></span>  

    [!code-cshtml[Main](working-with-files/samples/sample9.cshtml)]

    <span data-ttu-id="a1994-283">在此範例中，頁面主體中的 `FileUpload` helper 會設定為讓使用者根據預設上傳兩個檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-283">In this example, the `FileUpload` helper in the body of the page is configured to let users upload two files by default.</span></span> <span data-ttu-id="a1994-284">因為 `allowMoreFilesToBeAdded` 設定為 `true`，協助專家會轉譯一個連結，讓使用者加入更多的上傳方塊：</span><span class="sxs-lookup"><span data-stu-id="a1994-284">Because `allowMoreFilesToBeAdded` is set to `true`, the helper renders a link that lets user add more upload boxes:</span></span>

    ![[影像]](working-with-files/_static/image11.jpg)

    <span data-ttu-id="a1994-286">若要處理使用者上傳的檔案，程式碼會使用您在上一個範例&#8212;中所使用的基本技巧，從 `Request.Files` 取得檔案，然後加以儲存。</span><span class="sxs-lookup"><span data-stu-id="a1994-286">To process the files that the user uploads, the code uses the same basic technique that you used in the previous example &#8212; get a file from `Request.Files` and then save it.</span></span> <span data-ttu-id="a1994-287">（包括您需要執行的各種動作，以取得正確的檔案名和路徑）。這次的創新是，使用者可能上傳多個檔案，但您不知道多個檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-287">(Including the various things you need to do to get the right file name and path.) The innovation this time is that the user might be uploading multiple files and you don't know many.</span></span> <span data-ttu-id="a1994-288">若要找出，您可以取得 `Request.Files.Count`。</span><span class="sxs-lookup"><span data-stu-id="a1994-288">To find out, you can get `Request.Files.Count`.</span></span>

    <span data-ttu-id="a1994-289">有了這個數位，您就可以迴圈執行 `Request.Files`、輪流提取每個檔案，然後加以儲存。</span><span class="sxs-lookup"><span data-stu-id="a1994-289">With this number in hand, you can loop through `Request.Files`, fetch each file in turn, and save it.</span></span> <span data-ttu-id="a1994-290">當您想要透過集合迴圈執行已知的次數時，您可以使用 `for` 迴圈，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a1994-290">When you want to loop a known number of times through a collection, you can use a `for` loop, like this:</span></span>

    [!code-csharp[Main](working-with-files/samples/sample10.cs)]

    <span data-ttu-id="a1994-291">變數 `i` 只是一個暫存計數器，會從零開始到您設定的任何上限。</span><span class="sxs-lookup"><span data-stu-id="a1994-291">The variable `i` is just a temporary counter that will go from zero to whatever upper limit you set.</span></span> <span data-ttu-id="a1994-292">在此情況下，上限是檔案數目。</span><span class="sxs-lookup"><span data-stu-id="a1994-292">In this case, the upper limit is the number of files.</span></span> <span data-ttu-id="a1994-293">但是，由於計數器是從零開始，因此通常是在 ASP.NET 中計算案例，而上限實際上小於檔案計數。</span><span class="sxs-lookup"><span data-stu-id="a1994-293">But because the counter starts at zero, as is typical for counting scenarios in ASP.NET, the upper limit is actually one less than the file count.</span></span> <span data-ttu-id="a1994-294">（如果有三個檔案上傳，則計數為零到2）。</span><span class="sxs-lookup"><span data-stu-id="a1994-294">(If three files are uploaded, the count is zero to 2.)</span></span>

    <span data-ttu-id="a1994-295">`uploadedCount` 變數會總計已成功上傳並儲存的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-295">The `uploadedCount` variable totals all the files that are successfully uploaded and saved.</span></span> <span data-ttu-id="a1994-296">這段程式碼可能會導致預期的檔案無法上傳。</span><span class="sxs-lookup"><span data-stu-id="a1994-296">This code accounts for the possibility that an expected file may not be able to be uploaded.</span></span>
4. <span data-ttu-id="a1994-297">在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="a1994-297">Run the page in a browser.</span></span> <span data-ttu-id="a1994-298">瀏覽器會顯示頁面和它的兩個上傳方塊。</span><span class="sxs-lookup"><span data-stu-id="a1994-298">The browser displays the page and its two upload boxes.</span></span>
5. <span data-ttu-id="a1994-299">選取要上傳的兩個檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-299">Select two files to upload.</span></span>
6. <span data-ttu-id="a1994-300">按一下 [**新增另一個**檔案]。</span><span class="sxs-lookup"><span data-stu-id="a1994-300">Click **Add another file**.</span></span> <span data-ttu-id="a1994-301">此頁面會顯示新的上傳方塊。</span><span class="sxs-lookup"><span data-stu-id="a1994-301">The page displays a new upload box.</span></span> 

    ![[影像]](working-with-files/_static/image12.jpg)
7. <span data-ttu-id="a1994-303">按一下 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="a1994-303">Click **Upload**.</span></span>
8. <span data-ttu-id="a1994-304">在網站中，以滑鼠**按右鍵專案**資料夾，然後按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="a1994-304">In the website, right-click the project folder and then click **Refresh**.</span></span>
9. <span data-ttu-id="a1994-305">開啟 [ *UploadedFiles* ] 資料夾，以查看成功上傳的檔案。</span><span class="sxs-lookup"><span data-stu-id="a1994-305">Open the *UploadedFiles* folder to see the successfully uploaded files.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="a1994-306">其他資源</span><span class="sxs-lookup"><span data-stu-id="a1994-306">Additional Resources</span></span>

[<span data-ttu-id="a1994-307">使用 ASP.NET Web Pages 網站中的影像</span><span class="sxs-lookup"><span data-stu-id="a1994-307">Working with Images in an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkId=202897)

[<span data-ttu-id="a1994-308">匯出至 CSV 檔案</span><span class="sxs-lookup"><span data-stu-id="a1994-308">Exporting to a CSV File</span></span>](https://msdn.microsoft.com/library/ms155919.aspx)
