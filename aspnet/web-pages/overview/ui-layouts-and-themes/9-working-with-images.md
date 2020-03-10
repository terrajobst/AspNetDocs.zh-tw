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
# <a name="working-with-images-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="903b5-103">使用 ASP.NET Web Pages （Razor）網站中的影像</span><span class="sxs-lookup"><span data-stu-id="903b5-103">Working with Images in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="903b5-104">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="903b5-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="903b5-105">本文說明如何在 ASP.NET Web Pages （Razor）網站中新增、顯示及操作影像（調整大小、翻轉和新增浮水印）。</span><span class="sxs-lookup"><span data-stu-id="903b5-105">This article shows you how to add, display, and manipulate images (resize, flip, and add watermarks) in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="903b5-106">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="903b5-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="903b5-107">如何以動態方式將影像新增至頁面。</span><span class="sxs-lookup"><span data-stu-id="903b5-107">How to add an image to a page dynamically.</span></span>
> - <span data-ttu-id="903b5-108">如何讓使用者上傳影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-108">How to let users upload an image.</span></span>
> - <span data-ttu-id="903b5-109">如何調整影像大小。</span><span class="sxs-lookup"><span data-stu-id="903b5-109">How to resize an image.</span></span>
> - <span data-ttu-id="903b5-110">如何翻轉或旋轉影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-110">How to flip or rotate an image.</span></span>
> - <span data-ttu-id="903b5-111">如何將浮水印新增至影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-111">How to add a watermark to an image.</span></span>
> - <span data-ttu-id="903b5-112">如何使用影像做為浮水印。</span><span class="sxs-lookup"><span data-stu-id="903b5-112">How to use an image as a watermark.</span></span>
> 
> <span data-ttu-id="903b5-113">以下是文章中引進的 ASP.NET 程式設計功能：</span><span class="sxs-lookup"><span data-stu-id="903b5-113">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="903b5-114">`WebImage` helper。</span><span class="sxs-lookup"><span data-stu-id="903b5-114">The `WebImage` helper.</span></span>
> - <span data-ttu-id="903b5-115">`Path` 物件，提供可讓您操作路徑和檔案名的方法。</span><span class="sxs-lookup"><span data-stu-id="903b5-115">The `Path` object, which provides methods that let you manipulate path and file names.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="903b5-116">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="903b5-116">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="903b5-117">ASP.NET Web Pages （Razor）2</span><span class="sxs-lookup"><span data-stu-id="903b5-117">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="903b5-118">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="903b5-118">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="903b5-119">本教學課程也適用于 WebMatrix 3。</span><span class="sxs-lookup"><span data-stu-id="903b5-119">This tutorial also works with WebMatrix 3.</span></span>

<a id="Adding_an_Image"></a>
## <a name="adding-an-image-to-a-web-page-dynamically"></a><span data-ttu-id="903b5-120">以動態方式將影像新增至網頁</span><span class="sxs-lookup"><span data-stu-id="903b5-120">Adding an Image to a Web Page Dynamically</span></span>

<span data-ttu-id="903b5-121">您可以在開發網站時，將影像新增至您的網站和個別頁面。</span><span class="sxs-lookup"><span data-stu-id="903b5-121">You can add images to your website and to individual pages while you're developing the website.</span></span> <span data-ttu-id="903b5-122">您也可以讓使用者上傳影像，這可能適用于讓他們新增設定檔相片等工作。</span><span class="sxs-lookup"><span data-stu-id="903b5-122">You can also let users upload images, which might be useful for tasks like letting them add a profile photo.</span></span>

<span data-ttu-id="903b5-123">如果您的網站上已有影像，而您只想要將它顯示在頁面上，您可以使用 HTML `<img>` 元素，如下所示：</span><span class="sxs-lookup"><span data-stu-id="903b5-123">If an image is already available on your site and you just want to display it on a page, you use an HTML `<img>` element like this:</span></span>

[!code-html[Main](9-working-with-images/samples/sample1.html)]

<span data-ttu-id="903b5-124">不過，有時候您需要能夠動態&#8212;顯示影像，也就是說，在頁面執行之前，您不知道要顯示的影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-124">Sometimes, though, you need to be able to display images dynamically &#8212; that is, you don't know what image to display until the page is running.</span></span>

<span data-ttu-id="903b5-125">本節中的程式示範如何在使用者從影像名稱清單中指定影像檔案名稱的即時顯示影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-125">The procedure in this section shows how to display an image on the fly where users specify the image file name from a list of image names.</span></span> <span data-ttu-id="903b5-126">他們會從下拉式清單中選取影像的名稱，而當他們提交頁面時，就會顯示所選取的影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-126">They select the name of the image from a drop-down list, and when they submit the page, the image they selected is displayed.</span></span>

<span data-ttu-id="903b5-127">![包](9-working-with-images/_static/image1.jpg "ch9images-1 .jpg")</span><span class="sxs-lookup"><span data-stu-id="903b5-127">![[image]](9-working-with-images/_static/image1.jpg "ch9images-1.jpg")</span></span>

1. <span data-ttu-id="903b5-128">在 WebMatrix 中，建立新的網站。</span><span class="sxs-lookup"><span data-stu-id="903b5-128">In WebMatrix, create a new website.</span></span>
2. <span data-ttu-id="903b5-129">新增名為*DynamicImage*的新頁面。</span><span class="sxs-lookup"><span data-stu-id="903b5-129">Add a new page named *DynamicImage.cshtml*.</span></span>
3. <span data-ttu-id="903b5-130">在網站的根資料夾中，加入新的資料夾，並將其命名為*images*。</span><span class="sxs-lookup"><span data-stu-id="903b5-130">In the root folder of the website, add a new folder and name it *images*.</span></span>
4. <span data-ttu-id="903b5-131">將四個影像新增至您剛才建立的*images*資料夾。</span><span class="sxs-lookup"><span data-stu-id="903b5-131">Add four images to the *images* folder you just created.</span></span> <span data-ttu-id="903b5-132">（您可以使用的任何影像都會這麼做，但它們應該會放入頁面上）。重新命名影像*Photo1 .jpg*、 *Photo2 .jpg*、 *Photo3*和*Photo4*。</span><span class="sxs-lookup"><span data-stu-id="903b5-132">(Any images you have handy will do, but they should fit onto a page.) Rename the images *Photo1.jpg*, *Photo2.jpg*, *Photo3.jpg*, and *Photo4.jpg*.</span></span> <span data-ttu-id="903b5-133">（您不會在此程式中使用*Photo4* ，但稍後會在本文中使用它）。</span><span class="sxs-lookup"><span data-stu-id="903b5-133">(You won't use *Photo4.jpg* in this procedure, but you'll use it later in the article.)</span></span>
5. <span data-ttu-id="903b5-134">確認四個影像未標示為唯讀。</span><span class="sxs-lookup"><span data-stu-id="903b5-134">Verify that the four images are not marked as read-only.</span></span>
6. <span data-ttu-id="903b5-135">將頁面中的現有內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="903b5-135">Replace the existing content in the page with the following:</span></span>

    [!code-cshtml[Main](9-working-with-images/samples/sample2.cshtml)]

    <span data-ttu-id="903b5-136">頁面的主體具有一個名為 `photoChoice`的下拉式清單（`<select>` 元素）。</span><span class="sxs-lookup"><span data-stu-id="903b5-136">The body of the page has a drop-down list (a `<select>` element) that's named `photoChoice`.</span></span> <span data-ttu-id="903b5-137">清單有三個選項，而且每個清單選項的 `value` 屬性都有一個您放在*images*資料夾中的影像名稱。</span><span class="sxs-lookup"><span data-stu-id="903b5-137">The list has three options, and the `value` attribute of each list option has the name of one of the images that you put in the *images* folder.</span></span> <span data-ttu-id="903b5-138">基本上，此清單可讓使用者選取易記名稱，例如 &quot;相片 1&quot;，然後在提交頁面時傳遞 *.jpg*檔案名。</span><span class="sxs-lookup"><span data-stu-id="903b5-138">Essentially, the list lets the user select a friendly name like &quot;Photo 1&quot;, and it then passes the *.jpg* file name when the page is submitted.</span></span>

    <span data-ttu-id="903b5-139">在程式碼中，您可以藉由閱讀 `Request["photoChoice"]`，從清單中取得使用者的選取範圍（亦即，影像檔案名稱）。</span><span class="sxs-lookup"><span data-stu-id="903b5-139">In the code, you can get the user's selection (in other words, the image file name) from the list by reading `Request["photoChoice"]`.</span></span> <span data-ttu-id="903b5-140">您會先看到是否有任何選取專案。</span><span class="sxs-lookup"><span data-stu-id="903b5-140">You first see if there's a selection at all.</span></span> <span data-ttu-id="903b5-141">如果有，您可以為映射建立路徑，其中包含影像的資料夾名稱和使用者的影像檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="903b5-141">If there is, you construct a path for the image that consists of the name of the folder for the images and the user's image file name.</span></span> <span data-ttu-id="903b5-142">（如果您嘗試建立路徑，但 `Request["photoChoice"]`中沒有任何內容，就會收到錯誤）。這會產生如下所示的相對路徑：</span><span class="sxs-lookup"><span data-stu-id="903b5-142">(If you tried to construct a path but there was nothing in `Request["photoChoice"]`, you'd get an error.) This results in a relative path like this:</span></span>

    <span data-ttu-id="903b5-143">*images/Photo1 .jpg*</span><span class="sxs-lookup"><span data-stu-id="903b5-143">*images/Photo1.jpg*</span></span>

    <span data-ttu-id="903b5-144">路徑會儲存在名為 `imagePath` 的變數中，您稍後會在頁面中需要此名稱。</span><span class="sxs-lookup"><span data-stu-id="903b5-144">The path is stored in variable named `imagePath` that you'll need later in the page.</span></span>

    <span data-ttu-id="903b5-145">在本文中，還有一個 `<img>` 元素，用來顯示使用者挑選的影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-145">In the body, there's also an `<img>` element that's used to display the image that the user picked.</span></span> <span data-ttu-id="903b5-146">`src` 屬性未設定為檔案名或 URL，就像您要顯示靜態元素一樣。</span><span class="sxs-lookup"><span data-stu-id="903b5-146">The `src` attribute isn't set to a file name or URL, like you'd do to display a static element.</span></span> <span data-ttu-id="903b5-147">相反地，它會設定為 `@imagePath`，這表示它會從您在程式碼中設定的路徑取得其值。</span><span class="sxs-lookup"><span data-stu-id="903b5-147">Instead, it's set to `@imagePath`, meaning that it gets its value from the path you set in code.</span></span>

    <span data-ttu-id="903b5-148">不過，第一次執行頁面時，不會顯示任何影像，因為使用者未選取任何專案。</span><span class="sxs-lookup"><span data-stu-id="903b5-148">The first time that the page runs, though, there's no image to display, because the user hasn't selected anything.</span></span> <span data-ttu-id="903b5-149">這通常表示 `src` 屬性會是空的，而且影像會顯示為紅色 &quot;x&quot; （或當瀏覽器找不到影像時所呈現的任何內容）。</span><span class="sxs-lookup"><span data-stu-id="903b5-149">This would normally mean that the `src` attribute would be empty and the image would show up as a red &quot;x&quot; (or whatever the browser renders when it can't find an image).</span></span> <span data-ttu-id="903b5-150">若要避免這個情況，請將 `<img>` 元素放在測試的 `if` 區塊中，以查看 `imagePath` 變數是否有任何專案。</span><span class="sxs-lookup"><span data-stu-id="903b5-150">To prevent this, you put the `<img>` element in an `if` block that tests to see whether the `imagePath` variable has anything in it.</span></span> <span data-ttu-id="903b5-151">如果使用者進行選取，`imagePath` 包含路徑。</span><span class="sxs-lookup"><span data-stu-id="903b5-151">If the user made a selection, `imagePath` contains the path.</span></span> <span data-ttu-id="903b5-152">如果使用者未選取影像，或這是第一次顯示頁面，則不會轉譯 `<img>` 元素。</span><span class="sxs-lookup"><span data-stu-id="903b5-152">If the user didn't pick an image or if this is the first time the page is displayed, the `<img>` element isn't even rendered.</span></span>
7. <span data-ttu-id="903b5-153">儲存檔案，並在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="903b5-153">Save the file and run the page in a browser.</span></span> <span data-ttu-id="903b5-154">（在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）</span><span class="sxs-lookup"><span data-stu-id="903b5-154">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
8. <span data-ttu-id="903b5-155">從下拉式清單中選取映射，然後按一下 [**範例影像**]。</span><span class="sxs-lookup"><span data-stu-id="903b5-155">Select an image from the drop-down list and then click **Sample Image**.</span></span> <span data-ttu-id="903b5-156">請確定您針對不同的選擇看到不同的映射。</span><span class="sxs-lookup"><span data-stu-id="903b5-156">Make sure that you see different images for different choices.</span></span>

<a id="Uploading_an_Image"></a>
## <a name="uploading-an-image"></a><span data-ttu-id="903b5-157">上傳影像</span><span class="sxs-lookup"><span data-stu-id="903b5-157">Uploading an Image</span></span>

<span data-ttu-id="903b5-158">先前的範例示範如何以動態方式顯示影像，但只能使用已在您網站上的影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-158">The previous example showed you how to display an image dynamically, but it worked only with images that were already on your website.</span></span> <span data-ttu-id="903b5-159">此程式說明如何讓使用者上傳影像，然後顯示在頁面上。</span><span class="sxs-lookup"><span data-stu-id="903b5-159">This procedure shows how to let users upload an image, which is then displayed on the page.</span></span> <span data-ttu-id="903b5-160">在 ASP.NET 中，您可以使用 `WebImage` 協助程式即時操作影像，其中包含可讓您建立、操作和儲存影像的方法。</span><span class="sxs-lookup"><span data-stu-id="903b5-160">In ASP.NET, you can manipulate images on the fly using the `WebImage` helper, which has methods that let you create, manipulate, and save images.</span></span> <span data-ttu-id="903b5-161">`WebImage` helper 支援所有常見的 web 圖像檔案類型，包括 *.jpg*、 *.png*和 *.bmp*。</span><span class="sxs-lookup"><span data-stu-id="903b5-161">The `WebImage` helper supports all the common web image file types, including *.jpg*, *.png*, and *.bmp*.</span></span> <span data-ttu-id="903b5-162">在本文中，您將使用 *.jpg*影像，但是您可以使用任何影像類型。</span><span class="sxs-lookup"><span data-stu-id="903b5-162">Throughout this article, you'll use *.jpg* images, but you can use any of the image types.</span></span>

<span data-ttu-id="903b5-163">![包](9-working-with-images/_static/image2.jpg "ch9images-2 .jpg")</span><span class="sxs-lookup"><span data-stu-id="903b5-163">![[image]](9-working-with-images/_static/image2.jpg "ch9images-2.jpg")</span></span>

1. <span data-ttu-id="903b5-164">新增頁面，並將它命名為*UploadImage*。</span><span class="sxs-lookup"><span data-stu-id="903b5-164">Add a new page and name it *UploadImage.cshtml*.</span></span>
2. <span data-ttu-id="903b5-165">將頁面中的現有內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="903b5-165">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](9-working-with-images/samples/sample3.cshtml)]

    <span data-ttu-id="903b5-166">文字的主體具有 `<input type="file">` 元素，可讓使用者選取要上傳的檔案。</span><span class="sxs-lookup"><span data-stu-id="903b5-166">The body of the text has an `<input type="file">` element, which lets users select a file to upload.</span></span> <span data-ttu-id="903b5-167">當他們按一下 [**提交**] 時，所挑選的檔案會連同表單一起提交。</span><span class="sxs-lookup"><span data-stu-id="903b5-167">When they click **Submit**, the file they picked is submitted along with the form.</span></span>

    <span data-ttu-id="903b5-168">若要取得已上傳的影像，您可以使用 `WebImage` helper，其具有各種使用影像的實用方法。</span><span class="sxs-lookup"><span data-stu-id="903b5-168">To get the uploaded image, you use the `WebImage` helper, which has all sorts of useful methods for working with images.</span></span> <span data-ttu-id="903b5-169">具體而言，您會使用 `WebImage.GetImageFromRequest` 來取得已上傳的影像（如果有的話），並將它儲存在名為 `photo`的變數中。</span><span class="sxs-lookup"><span data-stu-id="903b5-169">Specifically, you use `WebImage.GetImageFromRequest` to get the uploaded image (if any) and store it in a variable named `photo`.</span></span>

    <span data-ttu-id="903b5-170">此範例中有很多工作需要取得和設定檔案和路徑名稱。</span><span class="sxs-lookup"><span data-stu-id="903b5-170">A lot of the work in this example involves getting and setting file and path names.</span></span> <span data-ttu-id="903b5-171">問題在於，您想要取得使用者所上傳影像的名稱（以及名稱），然後為您要儲存映射的位置建立新的路徑。</span><span class="sxs-lookup"><span data-stu-id="903b5-171">The issue is that you want to get the name (and just the name) of the image that the user uploaded, and then create a new path for where you're going to store the image.</span></span> <span data-ttu-id="903b5-172">因為使用者可能會上傳多個具有相同名稱的影像，所以您可以使用一些額外的程式碼來建立唯一的名稱，並確保使用者不會覆寫現有的圖片。</span><span class="sxs-lookup"><span data-stu-id="903b5-172">Because users could potentially upload multiple images that have the same name, you use a bit of extra code to create unique names and make sure that users don't overwrite existing pictures.</span></span>

    <span data-ttu-id="903b5-173">如果已上傳影像（測試 `if (photo != null)`），您會從影像的 `FileName` 屬性取得映射名稱。</span><span class="sxs-lookup"><span data-stu-id="903b5-173">If an image actually has been uploaded (the test `if (photo != null)`), you get the image name from the image's `FileName` property.</span></span> <span data-ttu-id="903b5-174">當使用者上傳影像時，`FileName` 會包含使用者的原始名稱，其中包括使用者電腦的路徑。</span><span class="sxs-lookup"><span data-stu-id="903b5-174">When the user uploads the image, `FileName` contains the user's original name, which includes the path from the user's computer.</span></span> <span data-ttu-id="903b5-175">看起來可能像這樣：</span><span class="sxs-lookup"><span data-stu-id="903b5-175">It might look like this:</span></span>

    <span data-ttu-id="903b5-176">*C:\Users\Joe\Pictures\SamplePhoto1.jpg*</span><span class="sxs-lookup"><span data-stu-id="903b5-176">*C:\Users\Joe\Pictures\SamplePhoto1.jpg*</span></span>

    <span data-ttu-id="903b5-177">雖然您只想要實際的檔案名（ &#8212; *SamplePhoto1 .jpg*），但您不想要所有的路徑資訊。</span><span class="sxs-lookup"><span data-stu-id="903b5-177">You don't want all that path information, though &#8212; you just want the actual file name (*SamplePhoto1.jpg*).</span></span> <span data-ttu-id="903b5-178">您可以使用 `Path.GetFileName` 方法來去除路徑中的檔案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="903b5-178">You can strip out just the file from a path by using the `Path.GetFileName` method, like this:</span></span>

    [!code-csharp[Main](9-working-with-images/samples/sample4.cs)]

    <span data-ttu-id="903b5-179">接著，您可以藉由將 GUID 加入至原始名稱，來建立新的唯一檔案名。</span><span class="sxs-lookup"><span data-stu-id="903b5-179">You then create a new unique file name by adding a GUID to the original name.</span></span> <span data-ttu-id="903b5-180">（如需 Guid 的詳細資訊，請參閱本文稍後的[關於 guid](#SB_AboutGUIDs) ）。然後，您會建立可用來儲存影像的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="903b5-180">(For more about GUIDs, see [About GUIDs](#SB_AboutGUIDs) later in this article.) Then you construct a complete path that you can use to save the image.</span></span> <span data-ttu-id="903b5-181">儲存路徑是由新的檔案名、資料夾（影像）和目前的網站位置所組成。</span><span class="sxs-lookup"><span data-stu-id="903b5-181">The save path is made up of the new file name, the folder (images), and the current website location.</span></span>

    > [!NOTE]
    > <span data-ttu-id="903b5-182">為了讓您的程式碼將檔案儲存在*images*資料夾中，應用程式需要該資料夾的讀寫許可權。</span><span class="sxs-lookup"><span data-stu-id="903b5-182">In order for your code to save files in the *images* folder, the application needs read-write permissions for that folder.</span></span> <span data-ttu-id="903b5-183">在您的開發電腦上，這通常不是問題。</span><span class="sxs-lookup"><span data-stu-id="903b5-183">On your development computer this is not typically an issue.</span></span> <span data-ttu-id="903b5-184">不過，當您將網站發佈至主控提供者的 web 伺服器時，您可能需要明確地設定這些許可權。</span><span class="sxs-lookup"><span data-stu-id="903b5-184">However, when you publish your site to a hosting provider's web server, you might need to explicitly set those permissions.</span></span> <span data-ttu-id="903b5-185">如果您在主控提供者的伺服器上執行此程式碼，並收到錯誤，請洽詢主機服務提供者，以瞭解如何設定這些許可權。</span><span class="sxs-lookup"><span data-stu-id="903b5-185">If you run this code on a hosting provider's server and get errors, check with the hosting provider to find out how to set those permissions.</span></span>

    <span data-ttu-id="903b5-186">最後，您會將儲存路徑傳遞給 `WebImage` helper 的 `Save` 方法。</span><span class="sxs-lookup"><span data-stu-id="903b5-186">Finally, you pass the save path to the `Save` method of the `WebImage` helper.</span></span> <span data-ttu-id="903b5-187">這會將所上傳的影像儲存在其新名稱之下。</span><span class="sxs-lookup"><span data-stu-id="903b5-187">This stores the uploaded image under its new name.</span></span> <span data-ttu-id="903b5-188">Save 方法看起來像這樣： `photo.Save(@"~\" + imagePath)`。</span><span class="sxs-lookup"><span data-stu-id="903b5-188">The save method looks like this: `photo.Save(@"~\" + imagePath)`.</span></span> <span data-ttu-id="903b5-189">完整路徑會附加至 `@"~\"`，也就是目前的網站位置。</span><span class="sxs-lookup"><span data-stu-id="903b5-189">The complete path is appended to `@"~\"`, which is the current website location.</span></span> <span data-ttu-id="903b5-190">（如需 `~` 運算子的詳細資訊，請參閱[使用 Razor 語法 ASP.NET Web 程式設計的簡介](https://go.microsoft.com/fwlink/?LinkId=202890#ID_WorkingWithFileAndFolderPaths)）。</span><span class="sxs-lookup"><span data-stu-id="903b5-190">(For information about the `~` operator, see [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890#ID_WorkingWithFileAndFolderPaths).)</span></span>

    <span data-ttu-id="903b5-191">如先前範例所示，頁面的內文包含一個 `<img>` 元素來顯示影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-191">As in the previous example, the body of the page contains an `<img>` element to display the image.</span></span> <span data-ttu-id="903b5-192">如果已設定 `imagePath`，則會轉譯 `<img>` 元素，且其 `src` 屬性會設定為 `imagePath` 值。</span><span class="sxs-lookup"><span data-stu-id="903b5-192">If `imagePath` has been set, the `<img>` element is rendered and its `src` attribute is set to the `imagePath` value.</span></span>
3. <span data-ttu-id="903b5-193">在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="903b5-193">Run the page in a browser.</span></span>
4. <span data-ttu-id="903b5-194">上傳影像，並確定它顯示在頁面中。</span><span class="sxs-lookup"><span data-stu-id="903b5-194">Upload an image and make sure it's displayed in the page.</span></span>
5. <span data-ttu-id="903b5-195">在您的網站中，開啟 [ *images* ] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="903b5-195">In your site, open the *images* folder.</span></span> <span data-ttu-id="903b5-196">您會看到新的檔案已經加入，其檔案名看起來像這樣：：</span><span class="sxs-lookup"><span data-stu-id="903b5-196">You see that a new file has been added whose file name looks something like this::</span></span> 

    <span data-ttu-id="903b5-197">*45ea4527-7ddd-4965-b9ca-c6444982b342\_MyPhoto .png*</span><span class="sxs-lookup"><span data-stu-id="903b5-197">*45ea4527-7ddd-4965-b9ca-c6444982b342\_MyPhoto.png*</span></span>

    <span data-ttu-id="903b5-198">這是您上傳的映射，其 GUID 前面會加上名稱。</span><span class="sxs-lookup"><span data-stu-id="903b5-198">This is the image that you uploaded with a GUID prefixed to the name.</span></span> <span data-ttu-id="903b5-199">（您自己的檔案將會有不同的 GUID，而且名稱可能會與*MyPhoto*不同）。</span><span class="sxs-lookup"><span data-stu-id="903b5-199">(Your own file will have a different GUID and probably is named something different than *MyPhoto.png*.)</span></span>

> [!TIP] 
> 
> <a id="SB_AboutGUIDs"></a>
> ### <a name="about-guids"></a><span data-ttu-id="903b5-200">關於 Guid</span><span class="sxs-lookup"><span data-stu-id="903b5-200">About GUIDs</span></span>
> 
> <span data-ttu-id="903b5-201">GUID （全域唯一識別碼）是通常以如下格式轉譯的識別碼： `936DA01F-9ABD-4d9d-80C7-02AF85C822A8`。</span><span class="sxs-lookup"><span data-stu-id="903b5-201">A GUID (globally-unique ID) is an identifier that's usually rendered in a format like this: `936DA01F-9ABD-4d9d-80C7-02AF85C822A8`.</span></span> <span data-ttu-id="903b5-202">每個 GUID 的數位和字母（從-F）不同，但全都遵循使用8-4-4-4-12 個字元群組的模式。</span><span class="sxs-lookup"><span data-stu-id="903b5-202">The numbers and letters (from A-F) differ for each GUID, but they all follow the pattern of using groups of 8-4-4-4-12 characters.</span></span> <span data-ttu-id="903b5-203">（就技術上而言，GUID 是16位元組/128 位的數位）。當您需要 GUID 時，您可以呼叫為您產生 GUID 的特製化程式碼。</span><span class="sxs-lookup"><span data-stu-id="903b5-203">(Technically, a GUID is a 16-byte/128-bit number.) When you need a GUID, you can call specialized code that generates a GUID for you.</span></span> <span data-ttu-id="903b5-204">Guid 背後的構想是，在數位的龐大大小（3.4 x 10<sup>38</sup>）和產生它的演算法之間，所產生的數位幾乎都一定是其中一種。</span><span class="sxs-lookup"><span data-stu-id="903b5-204">The idea behind GUIDs is that between the enormous size of the number (3.4 x 10<sup>38</sup>) and the algorithm for generating it, the resulting number is virtually guaranteed to be one of a kind.</span></span> <span data-ttu-id="903b5-205">因此，當您必須保證不會使用相同的名稱兩次時，Guid 就是產生專案名稱的好方法。</span><span class="sxs-lookup"><span data-stu-id="903b5-205">GUIDs therefore are a good way to generate names for things when you must guarantee that you won't use the same name twice.</span></span> <span data-ttu-id="903b5-206">當然，缺點是 Guid 並不特別方便使用者使用，因此當名稱只用于程式碼時，通常會用到。</span><span class="sxs-lookup"><span data-stu-id="903b5-206">The downside, of course, is that GUIDs aren't particularly user friendly, so they tend to be used when the name is used only in code.</span></span>

<a id="Resizing_an_Image"></a>
## <a name="resizing-an-image"></a><span data-ttu-id="903b5-207">調整影像大小</span><span class="sxs-lookup"><span data-stu-id="903b5-207">Resizing an Image</span></span>

<span data-ttu-id="903b5-208">如果您的網站接受來自使用者的影像，您可能會想要在顯示或儲存影像之前調整其大小。</span><span class="sxs-lookup"><span data-stu-id="903b5-208">If your website accepts images from a user, you might want to resize the images before you display or save them.</span></span> <span data-ttu-id="903b5-209">您可以再次使用 `WebImage` helper 來進行此工作。</span><span class="sxs-lookup"><span data-stu-id="903b5-209">You can again use the `WebImage` helper for this.</span></span>

<span data-ttu-id="903b5-210">此程式示範如何調整已上傳影像的大小以建立縮圖，然後將縮圖和原始影像儲存在網站中。</span><span class="sxs-lookup"><span data-stu-id="903b5-210">This procedure shows how to resize an uploaded image to create a thumbnail and then save the thumbnail and original image in the website.</span></span> <span data-ttu-id="903b5-211">您會在頁面上顯示縮圖，並使用超連結將使用者重新導向至完整大小的影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-211">You display the thumbnail on the page and use a hyperlink to redirect users to the full-sized image.</span></span>

<span data-ttu-id="903b5-212">![包](9-working-with-images/_static/image3.jpg "ch9images-3 .jpg")</span><span class="sxs-lookup"><span data-stu-id="903b5-212">![[image]](9-working-with-images/_static/image3.jpg "ch9images-3.jpg")</span></span>

1. <span data-ttu-id="903b5-213">新增名為 [*微縮圖. cshtml*] 的新頁面。</span><span class="sxs-lookup"><span data-stu-id="903b5-213">Add a new page named *Thumbnail.cshtml*.</span></span>
2. <span data-ttu-id="903b5-214">在 [ *images* ] 資料夾中，建立名為*大拇指*的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="903b5-214">In the *images* folder, create a subfolder named *thumbs*.</span></span>
3. <span data-ttu-id="903b5-215">將頁面中的現有內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="903b5-215">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](9-working-with-images/samples/sample5.cshtml)]

    <span data-ttu-id="903b5-216">此程式碼與上一個範例中的程式碼類似。</span><span class="sxs-lookup"><span data-stu-id="903b5-216">This code is similar to the code from the previous example.</span></span> <span data-ttu-id="903b5-217">差別在於，此程式碼會在您建立影像的縮圖複本之後，正常地儲存影像兩次。</span><span class="sxs-lookup"><span data-stu-id="903b5-217">The difference is that this code saves the image twice, once normally and once after you create a thumbnail copy of the image.</span></span> <span data-ttu-id="903b5-218">首先，您會取得已上傳的影像，並將它儲存在*images*資料夾中。</span><span class="sxs-lookup"><span data-stu-id="903b5-218">First you get the uploaded image and save it in the *images* folder.</span></span> <span data-ttu-id="903b5-219">接著，您會為縮圖影像建立新的路徑。</span><span class="sxs-lookup"><span data-stu-id="903b5-219">You then construct a new path for the thumbnail image.</span></span> <span data-ttu-id="903b5-220">若要實際建立縮圖，您可以呼叫 `WebImage` helper 的 `Resize` 方法，以建立60圖元的60圖元影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-220">To actually create the thumbnail, you call the `WebImage` helper's `Resize` method to create a 60-pixel by 60-pixel image.</span></span> <span data-ttu-id="903b5-221">此範例會示範如何保留外觀比例，以及如何防止影像放大（以防新的大小實際會使影像變大）。</span><span class="sxs-lookup"><span data-stu-id="903b5-221">The example shows how you preserve the aspect ratio and how you can prevent the image from being enlarged (in case the new size would actually make the image larger).</span></span> <span data-ttu-id="903b5-222">然後，調整大小的影像會儲存在 [*拇指*] 子資料夾中。</span><span class="sxs-lookup"><span data-stu-id="903b5-222">The resized image is then saved in the *thumbs* subfolder.</span></span>

    <span data-ttu-id="903b5-223">在標記的結尾，您會使用與您在先前範例中看到的動態 `src` 屬性相同的 `<img>` 元素，以有條件地顯示影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-223">At the end of the markup, you use the same `<img>` element with the dynamic `src` attribute that you've seen in the previous examples to conditionally show the image.</span></span> <span data-ttu-id="903b5-224">在此情況下，您會顯示縮圖。</span><span class="sxs-lookup"><span data-stu-id="903b5-224">In this case, you display the thumbnail.</span></span> <span data-ttu-id="903b5-225">您也可以使用 `<a>` 元素，來建立影像的大型版本超連結。</span><span class="sxs-lookup"><span data-stu-id="903b5-225">You also use an `<a>` element to create a hyperlink to the big version of the image.</span></span> <span data-ttu-id="903b5-226">如同 `<img>` 元素的 `src` 屬性，您可以將 `<a>` 專案的 `href` 屬性動態設定為 `imagePath`中的任何一個。</span><span class="sxs-lookup"><span data-stu-id="903b5-226">As with the `src` attribute of the `<img>` element, you set the `href` attribute of the `<a>` element dynamically to whatever is in `imagePath`.</span></span> <span data-ttu-id="903b5-227">為確保路徑可以做為 URL，您可以將 `imagePath` 傳遞至 `Html.AttributeEncode` 方法，這會將路徑中的保留字元轉換為 URL 中的正確字元。</span><span class="sxs-lookup"><span data-stu-id="903b5-227">To make sure that the path can work as a URL, you pass `imagePath` to the `Html.AttributeEncode` method, which converts reserved characters in the path to characters that are ok in a URL.</span></span>
4. <span data-ttu-id="903b5-228">在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="903b5-228">Run the page in a browser.</span></span>
5. <span data-ttu-id="903b5-229">上傳相片並確認已顯示縮圖。</span><span class="sxs-lookup"><span data-stu-id="903b5-229">Upload a photo and verify that the thumbnail is shown.</span></span>
6. <span data-ttu-id="903b5-230">按一下縮圖以查看完整大小的影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-230">Click the thumbnail to see the full-size image.</span></span>
7. <span data-ttu-id="903b5-231">請注意，在*images*和*images/拇指*中，已新增檔案。</span><span class="sxs-lookup"><span data-stu-id="903b5-231">In the *images* and *images/thumbs*, note that new files have been added.</span></span>

<a id="Rotating_and_Flipping"></a>
## <a name="rotating-and-flipping-an-image"></a><span data-ttu-id="903b5-232">旋轉和翻轉影像</span><span class="sxs-lookup"><span data-stu-id="903b5-232">Rotating and Flipping an Image</span></span>

<span data-ttu-id="903b5-233">`WebImage` 協助程式也可讓您翻轉和旋轉影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-233">The `WebImage` helper also lets you flip and rotate images.</span></span> <span data-ttu-id="903b5-234">此程式顯示如何從伺服器取得影像、反轉影像的倒置（垂直）、儲存，然後在頁面上顯示翻轉的影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-234">This procedure shows how to get an image from the server, flip the image upside down (vertically), save it, and then display the flipped image on the page.</span></span> <span data-ttu-id="903b5-235">在此範例中，您只是使用伺服器上已有的檔案（*Photo2 .jpg*）。</span><span class="sxs-lookup"><span data-stu-id="903b5-235">In this example, you're just using a file you already have on the server (*Photo2.jpg*).</span></span> <span data-ttu-id="903b5-236">在實際的應用程式中，您可能會翻轉以動態方式取得名稱的映射，就像先前範例中所做的一樣。</span><span class="sxs-lookup"><span data-stu-id="903b5-236">In a real application, you'd probably flip an image whose name you get dynamically, like you did in previous examples.</span></span>

<span data-ttu-id="903b5-237">![包](9-working-with-images/_static/image4.jpg "ch9images-4 .jpg")</span><span class="sxs-lookup"><span data-stu-id="903b5-237">![[image]](9-working-with-images/_static/image4.jpg "ch9images-4.jpg")</span></span>

1. <span data-ttu-id="903b5-238">新增名為*FlipImage*的新頁面。</span><span class="sxs-lookup"><span data-stu-id="903b5-238">Add a new page named *FlipImage.cshtml*.</span></span>
2. <span data-ttu-id="903b5-239">將頁面中的現有內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="903b5-239">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](9-working-with-images/samples/sample6.cshtml)]

    <span data-ttu-id="903b5-240">程式碼會使用 `WebImage` helper 來從伺服器取得影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-240">The code uses the `WebImage` helper to get an image from the server.</span></span> <span data-ttu-id="903b5-241">您可以使用先前用來儲存影像的相同技術來建立映射的路徑，並在使用 `WebImage`建立映射時傳遞該路徑：</span><span class="sxs-lookup"><span data-stu-id="903b5-241">You create the path to the image using the same technique you used in earlier examples for saving images, and you pass that path when you create an image using `WebImage`:</span></span>

    [!code-javascript[Main](9-working-with-images/samples/sample7.js)]

    <span data-ttu-id="903b5-242">如果找到影像，您可以建立新的路徑和檔案名，就像您在先前的範例中所做的一樣。</span><span class="sxs-lookup"><span data-stu-id="903b5-242">If an image is found, you construct a new path and file name, like you did in earlier examples.</span></span> <span data-ttu-id="903b5-243">若要翻轉影像，請呼叫 `FlipVertical` 方法，然後再次儲存影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-243">To flip the image, you call the `FlipVertical` method, and then you save the image again.</span></span>

    <span data-ttu-id="903b5-244">使用 `src` 屬性設定為 `imagePath`的 `<img>` 專案，即可再次在頁面上顯示影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-244">The image is again displayed on the page by using the `<img>` element with the `src` attribute set to `imagePath`.</span></span>
3. <span data-ttu-id="903b5-245">在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="903b5-245">Run the page in a browser.</span></span> <span data-ttu-id="903b5-246">*Photo2*的影像會以倒置顯示。</span><span class="sxs-lookup"><span data-stu-id="903b5-246">The image for *Photo2.jpg* is shown upside down.</span></span>
4. <span data-ttu-id="903b5-247">重新整理頁面，或再次要求頁面，以查看影像已正確翻轉。</span><span class="sxs-lookup"><span data-stu-id="903b5-247">Refresh the page or request the page again to see the image is flipped right side up again.</span></span>

<span data-ttu-id="903b5-248">若要旋轉影像，您可以使用相同的程式碼，但不會呼叫 `FlipVertical` 或 `FlipHorizontal`，而是呼叫 `RotateLeft` 或 `RotateRight`。</span><span class="sxs-lookup"><span data-stu-id="903b5-248">To rotate an image, you use the same code, except that instead of calling the `FlipVertical` or `FlipHorizontal`, you call `RotateLeft` or `RotateRight`.</span></span>

<a id="Adding_a_Watermark"></a>
## <a name="adding-a-watermark-to-an-image"></a><span data-ttu-id="903b5-249">將浮水印新增至影像</span><span class="sxs-lookup"><span data-stu-id="903b5-249">Adding a Watermark to an Image</span></span>

<span data-ttu-id="903b5-250">當您將影像新增至您的網站時，您可能會想要先將浮水印新增至影像，然後將它顯示在頁面上。</span><span class="sxs-lookup"><span data-stu-id="903b5-250">When you add images to your website, you might want to add a watermark to the image before you save it or display it on a page.</span></span> <span data-ttu-id="903b5-251">人們通常會使用浮水印將著作權資訊新增至影像或廣告其商務名稱。</span><span class="sxs-lookup"><span data-stu-id="903b5-251">People often use watermarks to add copyright information to an image or to advertise their business name.</span></span>

<span data-ttu-id="903b5-252">![包](9-working-with-images/_static/image5.jpg "ch9images-5 .jpg")</span><span class="sxs-lookup"><span data-stu-id="903b5-252">![[image]](9-working-with-images/_static/image5.jpg "ch9images-5.jpg")</span></span>

1. <span data-ttu-id="903b5-253">新增名為 [*浮水印*] 的新頁面。</span><span class="sxs-lookup"><span data-stu-id="903b5-253">Add a new page named *Watermark.cshtml*.</span></span>
2. <span data-ttu-id="903b5-254">將頁面中的現有內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="903b5-254">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](9-working-with-images/samples/sample8.cshtml)]

    <span data-ttu-id="903b5-255">這段程式碼就像是稍早的*FlipImage*中的程式碼（雖然這次是使用*Photo3*檔案）。</span><span class="sxs-lookup"><span data-stu-id="903b5-255">This code is like the code in the *FlipImage.cshtml* page from earlier (although this time it uses the *Photo3.jpg* file).</span></span> <span data-ttu-id="903b5-256">若要新增浮水印，您可以先呼叫 `WebImage` helper 的 `AddTextWatermark` 方法，再儲存影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-256">To add the watermark, you call the `WebImage` helper's `AddTextWatermark` method before you save the image.</span></span> <span data-ttu-id="903b5-257">在 `AddTextWatermark`的呼叫中，您會將文字 &quot;[我的浮水印]&quot;，將字型色彩設為黃色，並將字型系列設定為 [Arial]。</span><span class="sxs-lookup"><span data-stu-id="903b5-257">In the call to `AddTextWatermark`, you pass the text &quot;My Watermark&quot;, set the font color to yellow, and set the font family to Arial.</span></span> <span data-ttu-id="903b5-258">（雖然此處未顯示，但 `WebImage` 協助程式也可讓您指定不透明度、字型系列和字型大小，以及浮水印文字的位置）。當您儲存映射時，它不得為唯讀。</span><span class="sxs-lookup"><span data-stu-id="903b5-258">(Although it's not shown here, the `WebImage` helper also lets you specify opacity, font family and font size, and the position of the watermark text.) When you save the image it must not be read-only.</span></span>

    <span data-ttu-id="903b5-259">如先前所見，影像會使用 [src] 屬性設定為 [`@imagePath`] 的 `<img>` 元素顯示在頁面上。</span><span class="sxs-lookup"><span data-stu-id="903b5-259">As you've seen before, the image is displayed on the page by using the `<img>` element with the src attribute set to `@imagePath`.</span></span>
3. <span data-ttu-id="903b5-260">在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="903b5-260">Run the page in a browser.</span></span> <span data-ttu-id="903b5-261">請注意影像右下角的「我的浮水印」文字。</span><span class="sxs-lookup"><span data-stu-id="903b5-261">Notice the text "My Watermark" at the bottom-right corner of the image.</span></span>

<a id="Using_an_Image_as_a_Watermark"></a>
## <a name="using-an-image-as-a-watermark"></a><span data-ttu-id="903b5-262">使用影像做為浮水印</span><span class="sxs-lookup"><span data-stu-id="903b5-262">Using an Image As a Watermark</span></span>

<span data-ttu-id="903b5-263">您可以使用另一個影像，而不是使用浮水印的文字。</span><span class="sxs-lookup"><span data-stu-id="903b5-263">Instead of using text for a watermark, you can use another image.</span></span> <span data-ttu-id="903b5-264">人們有時會使用公司標誌之類的影像做為浮水印，或使用浮水印影像而非文字來取得著作權資訊。</span><span class="sxs-lookup"><span data-stu-id="903b5-264">People sometimes use images like a company logo as a watermark, or they use a watermark image instead of text for copyright information.</span></span>

<span data-ttu-id="903b5-265">![包](9-working-with-images/_static/image6.jpg "ch9images-6 .jpg")</span><span class="sxs-lookup"><span data-stu-id="903b5-265">![[image]](9-working-with-images/_static/image6.jpg "ch9images-6.jpg")</span></span>

1. <span data-ttu-id="903b5-266">新增名為*ImageWatermark*的新頁面。</span><span class="sxs-lookup"><span data-stu-id="903b5-266">Add a new page named *ImageWatermark.cshtml*.</span></span>
2. <span data-ttu-id="903b5-267">將影像新增至 [ *images* ] 資料夾，您可以使用它做為標誌，並重新命名影像*MyCompanyLogo*。</span><span class="sxs-lookup"><span data-stu-id="903b5-267">Add an image to the *images* folder that you can use as a logo, and rename the image *MyCompanyLogo.jpg*.</span></span> <span data-ttu-id="903b5-268">此影像應該是當其設定為80圖元寬和20圖元高時，可以清楚看出的影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-268">This image should be an image that you can see clearly when it's set to 80 pixels wide and 20 pixels high.</span></span>
3. <span data-ttu-id="903b5-269">將頁面中的現有內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="903b5-269">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](9-working-with-images/samples/sample9.cshtml)]

    <span data-ttu-id="903b5-270">這是先前範例中程式碼的另一種變化。</span><span class="sxs-lookup"><span data-stu-id="903b5-270">This is another variation on the code from earlier examples.</span></span> <span data-ttu-id="903b5-271">在此情況下，您可以呼叫 `AddImageWatermark`，將浮水印影像新增至目標影像（*Photo3 .jpg*），然後再儲存影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-271">In this case, you call `AddImageWatermark` to add the watermark image to the target image (*Photo3.jpg*) before you save the image.</span></span> <span data-ttu-id="903b5-272">當您呼叫 `AddImageWatermark`時，會將其寬度設定為80圖元，並將高度設為20圖元。</span><span class="sxs-lookup"><span data-stu-id="903b5-272">When you call `AddImageWatermark`, you set its width to 80 pixels and the height to 20 pixels.</span></span> <span data-ttu-id="903b5-273">*MyCompanyLogo*會水準對齊，並在目標影像底部以垂直方式對齊。</span><span class="sxs-lookup"><span data-stu-id="903b5-273">The *MyCompanyLogo.jpg* image is horizontally aligned in the center and vertically aligned at the bottom of the target image.</span></span> <span data-ttu-id="903b5-274">不透明度設定為100%，而填補設定為10圖元。</span><span class="sxs-lookup"><span data-stu-id="903b5-274">The opacity is set to 100% and the padding is set to 10 pixels.</span></span> <span data-ttu-id="903b5-275">如果浮水印影像大於目標影像，則不會發生任何事。</span><span class="sxs-lookup"><span data-stu-id="903b5-275">If the watermark image is bigger than the target image, nothing will happen.</span></span> <span data-ttu-id="903b5-276">如果浮水印影像大於目標影像，而且您將影像浮水印的填補設定為零，則會忽略浮水印。</span><span class="sxs-lookup"><span data-stu-id="903b5-276">If the watermark image is bigger than the target image and you set the padding for the image watermark to zero, the watermark is ignored.</span></span>

    <span data-ttu-id="903b5-277">如先前所示，您可以使用 `<img>` 元素和動態 `src` 屬性來顯示影像。</span><span class="sxs-lookup"><span data-stu-id="903b5-277">As before, you display the image using the `<img>` element and a dynamic `src` attribute.</span></span>
4. <span data-ttu-id="903b5-278">在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="903b5-278">Run the page in a browser.</span></span> <span data-ttu-id="903b5-279">請注意，浮水印影像會出現在主要影像的底部。</span><span class="sxs-lookup"><span data-stu-id="903b5-279">Notice that the watermark image appears at the bottom of the main image.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="903b5-280">其他資源</span><span class="sxs-lookup"><span data-stu-id="903b5-280">Additional Resources</span></span>

[<span data-ttu-id="903b5-281">使用 ASP.NET Web Pages 網站中的檔案</span><span class="sxs-lookup"><span data-stu-id="903b5-281">Working with Files in an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkId=202896)

[<span data-ttu-id="903b5-282">使用 Razor 語法進行 ASP.NET Web Pages 程式設計的簡介</span><span class="sxs-lookup"><span data-stu-id="903b5-282">Introduction to ASP.NET Web Pages Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=251587)
