---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
title: 使用視圖主版頁面建立頁面配置C#（） |Microsoft Docs
author: microsoft
description: 在本教學課程中，您將瞭解如何利用 view 主版頁面，在應用程式中建立多個頁面的一般頁面配置。 您可以使用 。
ms.author: riande
ms.date: 10/16/2008
ms.assetid: dff54fcb-68b1-4488-89a2-ca97532d6a4c
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 026e3efb4ebf84016aa0f6a5fda4af549fdadfcb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594065"
---
# <a name="creating-page-layouts-with-view-master-pages-c"></a><span data-ttu-id="6a0e1-104">使用檢視主版頁面建立頁面配置 (C#)</span><span class="sxs-lookup"><span data-stu-id="6a0e1-104">Creating Page Layouts with View Master Pages (C#)</span></span>

<span data-ttu-id="6a0e1-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="6a0e1-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="6a0e1-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="6a0e1-106">Download PDF</span></span>](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_CS.pdf)

> <span data-ttu-id="6a0e1-107">在本教學課程中，您將瞭解如何利用 view 主版頁面，在應用程式中建立多個頁面的一般頁面配置。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-107">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="6a0e1-108">例如，您可以使用視圖主版頁面來定義兩個數據行的頁面配置，並針對 web 應用程式中的所有頁面使用兩個數據行的版面配置。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-108">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

## <a name="creating-page-layouts-with-view-master-pages"></a><span data-ttu-id="6a0e1-109">使用視圖主版頁面建立頁面配置</span><span class="sxs-lookup"><span data-stu-id="6a0e1-109">Creating Page Layouts with View Master Pages</span></span>

<span data-ttu-id="6a0e1-110">在本教學課程中，您將瞭解如何利用 view 主版頁面，在應用程式中建立多個頁面的一般頁面配置。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-110">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="6a0e1-111">例如，您可以使用視圖主版頁面來定義兩個數據行的頁面配置，並針對 web 應用程式中的所有頁面使用兩個數據行的版面配置。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-111">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

<span data-ttu-id="6a0e1-112">您也可以利用 view 主版頁面，在應用程式的多個頁面之間共用通用內容。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-112">You also can take advantage of view master pages to share common content across multiple pages in your application.</span></span> <span data-ttu-id="6a0e1-113">例如，您可以將網站標誌、導覽連結和橫幅廣告放在視圖主版頁面中。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-113">For example, you can place your website logo, navigation links, and banner advertisements in a view master page.</span></span> <span data-ttu-id="6a0e1-114">如此一來，應用程式中的每個頁面都會自動顯示此內容。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-114">That way, every page in your application would display this content automatically.</span></span>

<span data-ttu-id="6a0e1-115">在本教學課程中，您將瞭解如何建立新的視圖主版頁面，並根據主版頁面建立新的視圖內容頁面。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-115">In this tutorial, you learn how to create a new view master page and create a new view content page based on the master page.</span></span>

### <a name="creating-a-view-master-page"></a><span data-ttu-id="6a0e1-116">建立視圖主版頁面</span><span class="sxs-lookup"><span data-stu-id="6a0e1-116">Creating a View Master Page</span></span>

<span data-ttu-id="6a0e1-117">讓我們從建立定義兩個數據行版面配置的視圖主版頁面開始。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-117">Let's start by creating a view master page that defines a two-column layout.</span></span> <span data-ttu-id="6a0e1-118">以滑鼠右鍵按一下 [Views\Shared] 資料夾，選取功能表選項 [**加入]、[新增專案**]，然後選取 [ **MVC 視圖主版] 頁面**範本（請參閱 [圖 1]），即可將新的視圖主版頁面加入至 MVC 專案。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-118">You add a new view master page to an MVC project by right-clicking the Views\Shared folder, selecting the menu option **Add, New Item**, and selecting the **MVC View Master Page** template (see Figure 1).</span></span>

<span data-ttu-id="6a0e1-119">[![加入視圖主版頁面](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6a0e1-119">[![Adding a view master page](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)</span></span>

<span data-ttu-id="6a0e1-120">**圖 01**：加入視圖主版頁面（[按一下以觀看完整大小的影像](creating-page-layouts-with-view-master-pages-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="6a0e1-120">**Figure 01**: Adding a view master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image3.png))</span></span>

<span data-ttu-id="6a0e1-121">您可以在應用程式中建立一個以上的視圖主版頁面。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-121">You can create more than one view master page in an application.</span></span> <span data-ttu-id="6a0e1-122">每個 view 主版頁面都可以定義不同的頁面配置。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-122">Each view master page can define a different page layout.</span></span> <span data-ttu-id="6a0e1-123">例如，您可能想要讓特定頁面具有兩個數據行的配置，而其他頁面具有三個數據行的版面配置。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-123">For example, you might want certain pages to have a two-column layout and other pages to have a three-column layout.</span></span>

<span data-ttu-id="6a0e1-124">視圖主版頁面看起來非常類似標準的 ASP.NET MVC 視圖。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-124">A view master page looks very much like a standard ASP.NET MVC view.</span></span> <span data-ttu-id="6a0e1-125">不過，不同于一般的視圖，視圖主版頁面包含一個或多個 `<asp:ContentPlaceHolder>` 標記。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-125">However, unlike a normal view, a view master page contains one or more `<asp:ContentPlaceHolder>` tags.</span></span> <span data-ttu-id="6a0e1-126">`<contentplaceholder>` 標籤是用來標示可在個別內容頁面中覆寫之主版頁面的區域。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-126">The `<contentplaceholder>` tags are used to mark the areas of the master page that can be overridden in an individual content page.</span></span>

<span data-ttu-id="6a0e1-127">例如，[清單 1] 中的 [視圖主版] 頁面會定義兩個數據行的版面配置。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-127">For example, the view master page in Listing 1 defines a two-column layout.</span></span> <span data-ttu-id="6a0e1-128">其中包含兩個 `<contentplaceholder>` 標記。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-128">It contains two `<contentplaceholder>` tags.</span></span> <span data-ttu-id="6a0e1-129">每個資料行都有一個 `<ContentPlaceHolder>`。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-129">One `<ContentPlaceHolder>` for each column.</span></span>

<span data-ttu-id="6a0e1-130">**清單1– `Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="6a0e1-130">**Listing 1 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample1.aspx)]

<span data-ttu-id="6a0e1-131">[清單 1] 中視圖主版頁面的主體包含兩個對應至兩個數據行的 `<div>` 標記。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-131">The body of the view master page in Listing 1 contains two `<div>` tags that correspond to the two columns.</span></span> <span data-ttu-id="6a0e1-132">級聯樣式表資料行類別會同時套用至 `<div>` 標記。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-132">The Cascading Style Sheet column class is applied to both `<div>` tags.</span></span> <span data-ttu-id="6a0e1-133">這個類別定義于主版頁面頂端所宣告的樣式表單中。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-133">This class is defined in the style sheet declared at the top of the master page.</span></span> <span data-ttu-id="6a0e1-134">您可以藉由切換至設計檢視，來預覽視圖主版頁面的呈現方式。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-134">You can preview how the view master page will be rendered by switching to Design view.</span></span> <span data-ttu-id="6a0e1-135">按一下原始程式碼編輯器左下方的 [設計] 索引標籤（請參閱 [圖 2]）。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-135">Click the Design tab at the bottom-left of the source code editor (see Figure 2).</span></span>

<span data-ttu-id="6a0e1-136">[![預覽設計工具中的主版頁面](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="6a0e1-136">[![Previewing a master page in the designer](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)</span></span>

<span data-ttu-id="6a0e1-137">**圖 02**：在設計工具中預覽主版頁面（[按一下以觀看完整大小的影像](creating-page-layouts-with-view-master-pages-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="6a0e1-137">**Figure 02**: Previewing a master page in the designer ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image6.png))</span></span>

### <a name="creating-a-view-content-page"></a><span data-ttu-id="6a0e1-138">建立視圖內容頁面</span><span class="sxs-lookup"><span data-stu-id="6a0e1-138">Creating a View Content Page</span></span>

<span data-ttu-id="6a0e1-139">建立視圖主版頁面之後，您可以根據 [視圖主版] 頁面建立一或多個 view 內容頁。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-139">After you create a view master page, you can create one or more view content pages based on the view master page.</span></span> <span data-ttu-id="6a0e1-140">例如，您可以在 [Views\Home] 資料夾上按一下滑鼠右鍵，選取 [**加入]、[新增專案**]、選取 [ **MVC 視圖內容] 頁面**範本、輸入名稱為 default.aspx，然後按一下 [**新增**] 按鈕（請參閱 [圖 3]），以建立主控制器的索引視圖內容頁面。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-140">For example, you can create an Index view content page for the Home controller by right-clicking the Views\Home folder, selecting **Add, New Item**, selecting the **MVC View Content Page** template, entering the name Index.aspx, and clicking the **Add** button (see Figure 3).</span></span>

<span data-ttu-id="6a0e1-141">[![加入視圖內容頁面](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="6a0e1-141">[![Adding a view content page](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)</span></span>

<span data-ttu-id="6a0e1-142">**圖 03**：加入視圖內容頁面（[按一下以觀看完整大小的影像](creating-page-layouts-with-view-master-pages-cs/_static/image9.png)）</span><span class="sxs-lookup"><span data-stu-id="6a0e1-142">**Figure 03**: Adding a view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image9.png))</span></span>

<span data-ttu-id="6a0e1-143">按一下 [新增] 按鈕之後，就會出現新的對話方塊，讓您選取要與 [視圖內容] 頁面建立關聯的視圖主版頁面（請參閱 [圖 4]）。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-143">After you click the Add button, a new dialog appears that enables you to select a view master page to associate with the view content page (see Figure 4).</span></span> <span data-ttu-id="6a0e1-144">您可以流覽至我們在上一節中建立的主版視圖主版頁面。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-144">You can navigate to the Site.master view master page that we created in the previous section.</span></span>

<span data-ttu-id="6a0e1-145">[選取主版頁面 ![](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="6a0e1-145">[![Selecting a master page](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)</span></span>

<span data-ttu-id="6a0e1-146">**圖 04**：選取主版頁面（[按一下以觀看完整大小的影像](creating-page-layouts-with-view-master-pages-cs/_static/image12.png)）</span><span class="sxs-lookup"><span data-stu-id="6a0e1-146">**Figure 04**: Selecting a master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image12.png))</span></span>

<span data-ttu-id="6a0e1-147">根據網站主要頁面建立新的 view 內容頁面之後，您會在 [清單 2] 中取得檔案。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-147">After you create a new view content page based on the Site.master master page, you get the file in Listing 2.</span></span>

<span data-ttu-id="6a0e1-148">**清單2– `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="6a0e1-148">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample2.aspx)]

<span data-ttu-id="6a0e1-149">請注意，此視圖包含對應至 [視圖主版] 頁面中每個 `<asp:ContentPlaceHolder>` 標記的 `<asp:Content>` 標記。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-149">Notice that this view contains a `<asp:Content>` tag that corresponds to each of the `<asp:ContentPlaceHolder>` tags in the view master page.</span></span> <span data-ttu-id="6a0e1-150">每個 `<asp:Content>` 標籤都包含 ContentPlaceHolderID 屬性，指向它所覆寫的特定 `<asp:ContentPlaceHolder>`。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-150">Each `<asp:Content>` tag includes a ContentPlaceHolderID attribute that points to the particular `<asp:ContentPlaceHolder>` that it overrides.</span></span>

<span data-ttu-id="6a0e1-151">此外，請注意，[清單 2] 中的 [內容視圖] 頁面不包含任何標準的開頭和結尾 HTML 標籤。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-151">Notice, furthermore, that the content view page in Listing 2 does not contain any of the normal opening and closing HTML tags.</span></span> <span data-ttu-id="6a0e1-152">例如，它不包含開頭和結尾 `<html>` 或 `<head>` 標記。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-152">For example, it does not contain the opening and closing `<html>` or `<head>` tags.</span></span> <span data-ttu-id="6a0e1-153">所有標準的開頭和結束記號都包含在視圖主版頁面中。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-153">All of the normal opening and closing tags are contained in the view master page.</span></span>

<span data-ttu-id="6a0e1-154">您想要顯示在 [視圖內容] 頁面中的任何內容都必須放在 `<asp:Content>` 標籤中。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-154">Any content that you want to display in a view content page must be placed within a `<asp:Content>` tag.</span></span> <span data-ttu-id="6a0e1-155">如果您將任何 HTML 或其他內容放在這些標籤之外，當您嘗試查看頁面時，將會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-155">If you place any HTML or other content outside of these tags, then you will get an error when you attempt to view the page.</span></span>

<span data-ttu-id="6a0e1-156">您不需要從內容視圖頁面中的主版頁面覆寫每個 `<asp:ContentPlaceHolder>` 標記。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-156">You don't need to override every `<asp:ContentPlaceHolder>` tag from a master page in a content view page.</span></span> <span data-ttu-id="6a0e1-157">當您想要將標記取代為特定內容時，您只需要覆寫 `<asp:ContentPlaceHolder>` 標記。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-157">You only need to override a `<asp:ContentPlaceHolder>` tag when you want to replace the tag with particular content.</span></span>

<span data-ttu-id="6a0e1-158">例如，[清單 3] 中修改過的索引視圖只包含兩個 `<asp:Content>` 標記。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-158">For example, the modified Index view in Listing 3 contains only two `<asp:Content>` tags.</span></span> <span data-ttu-id="6a0e1-159">每個 `<asp:Content>` 標記都包含一些文字。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-159">Each of the `<asp:Content>` tags includes some text.</span></span>

<span data-ttu-id="6a0e1-160">**清單3– `Views\Home\Index.aspx (modified)`**</span><span class="sxs-lookup"><span data-stu-id="6a0e1-160">**Listing 3 – `Views\Home\Index.aspx (modified)`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample3.aspx)]

<span data-ttu-id="6a0e1-161">當要求 [清單 3] 中的視圖時，它會呈現 [圖 5] 中的頁面。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-161">When the view in Listing 3 is requested, it renders the page in Figure 5.</span></span> <span data-ttu-id="6a0e1-162">請注意，此視圖會呈現包含兩個數據行的頁面。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-162">Notice that the view renders a page with two columns.</span></span> <span data-ttu-id="6a0e1-163">此外，也請注意，[view content] 頁面中的內容會與 [視圖主版] 頁面中的內容合併</span><span class="sxs-lookup"><span data-stu-id="6a0e1-163">Notice, furthermore, that the content from the view content page is merged with the content from the view master page</span></span>

<span data-ttu-id="6a0e1-164">[![[索引視圖內容] 頁面](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="6a0e1-164">[![The Index view content page](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)</span></span>

<span data-ttu-id="6a0e1-165">**圖 05**： [索引視圖內容] 頁面（[按一下以查看完整大小的影像](creating-page-layouts-with-view-master-pages-cs/_static/image15.png)）</span><span class="sxs-lookup"><span data-stu-id="6a0e1-165">**Figure 05**: The Index view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image15.png))</span></span>

### <a name="modifying-view-master-page-content"></a><span data-ttu-id="6a0e1-166">修改視圖主版頁面內容</span><span class="sxs-lookup"><span data-stu-id="6a0e1-166">Modifying View Master Page Content</span></span>

<span data-ttu-id="6a0e1-167">當您使用 view 主版頁面時，幾乎會立即遇到的問題之一，就是在要求不同的視圖內容頁面時，修改視圖主版頁面內容的問題。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-167">One issue that you encounter almost immediately when working with view master pages is the problem of modifying view master page content when different view content pages are requested.</span></span> <span data-ttu-id="6a0e1-168">例如，您希望 web 應用程式中的每個頁面都有唯一的標題。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-168">For example, you want each page in your web application to have a unique title.</span></span> <span data-ttu-id="6a0e1-169">不過，標題是在視圖主版頁面中宣告，而不是在 [視圖內容] 頁面中宣告。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-169">However, the title is declared in the view master page and not in the view content page.</span></span> <span data-ttu-id="6a0e1-170">那麼，您要如何自訂每個視圖內容頁面的頁面標題呢？</span><span class="sxs-lookup"><span data-stu-id="6a0e1-170">So, how do you customize the page title for each view content page?</span></span>

<span data-ttu-id="6a0e1-171">有兩種方式可讓您修改 [視圖內容] 頁面所顯示的標題。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-171">There are two ways that you can modify the title displayed by a view content page.</span></span> <span data-ttu-id="6a0e1-172">首先，您可以將頁面標題指派給在 [視圖內容] 頁面頂端宣告之 `<%@ page %>` 指示詞的 [標題] 屬性。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-172">First, you can assign a page title to the title attribute of the `<%@ page %>` directive declared at the top of a view content page.</span></span> <span data-ttu-id="6a0e1-173">例如，如果您想要將頁面標題「超級絕佳網站」指派給索引視圖，您可以在索引視圖的頂端加入下列指示詞：</span><span class="sxs-lookup"><span data-stu-id="6a0e1-173">For example, if you want to assign the page title "Super Great Website" to the Index view, then you can include the following directive at the top of the Index view:</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample4.aspx)]

<span data-ttu-id="6a0e1-174">當索引視圖呈現到瀏覽器時，所需的標題會出現在瀏覽器標題列中：</span><span class="sxs-lookup"><span data-stu-id="6a0e1-174">When the Index view is rendered to the browser, the desired title appears in the browser title bar:</span></span>

<span data-ttu-id="6a0e1-175">[![瀏覽器標題列](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="6a0e1-175">[![Browser title bar](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)</span></span>

<span data-ttu-id="6a0e1-176">主要視圖頁面必須滿足其中一項重要的需求，title 屬性才能正常執行。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-176">There is one important requirement that a master view page must satisfy in order for the title attribute to work.</span></span> <span data-ttu-id="6a0e1-177">視圖主版頁面必須包含 `<head runat="server">` 標記，而不是其標頭的一般 `<head>` 標記。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-177">The view master page must contain a `<head runat="server">` tag instead of a normal `<head>` tag for its header.</span></span> <span data-ttu-id="6a0e1-178">如果 `<head>` 標記不包含 runat = "server" 屬性，則不會出現標題。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-178">If the `<head>` tag does not include the runat="server" attribute then the title won't appear.</span></span> <span data-ttu-id="6a0e1-179">預設的視圖主版頁面包含必要的 `<head runat="server">` 標記。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-179">The default view master page includes the required `<head runat="server">` tag.</span></span>

<span data-ttu-id="6a0e1-180">從個別視圖內容頁面修改主版頁面內容的替代方法是將您想要在 `<asp:ContentPlaceHolder>` 標籤中修改的區域換行。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-180">An alternative approach to modifying master page content from an individual view content page is to wrap the region that you want to modify in a `<asp:ContentPlaceHolder>` tag.</span></span> <span data-ttu-id="6a0e1-181">例如，假設您想要變更主要視圖頁面所轉譯的標題，而不只是中繼標記。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-181">For example, imagine that you want to change not only the title, but also the meta tags, rendered by a master view page.</span></span> <span data-ttu-id="6a0e1-182">[清單 4] 中的 [主要視圖] 頁面包含其 `<head>` 標記內的 `<asp:ContentPlaceHolder>` 標記。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-182">The master view page in Listing 4 contains a `<asp:ContentPlaceHolder>` tag within its `<head>` tag.</span></span>

<span data-ttu-id="6a0e1-183">**清單4– `Views\Shared\Site2.master`**</span><span class="sxs-lookup"><span data-stu-id="6a0e1-183">**Listing 4 – `Views\Shared\Site2.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample5.aspx)]

<span data-ttu-id="6a0e1-184">請注意，[清單 4] 中的 `<asp:ContentPlaceHolder>` 標籤包含預設的內容：預設標題和預設的中繼標記。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-184">Notice that the `<asp:ContentPlaceHolder>` tag in Listing 4 includes default content: a default title and default meta tags.</span></span> <span data-ttu-id="6a0e1-185">如果您未覆寫個別 [內容] 頁面中的此 `<asp:ContentPlaceHolder>` 標記，則會顯示預設內容。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-185">If you don't override this `<asp:ContentPlaceHolder>` tag in an individual view content page, then the default content will be displayed.</span></span>

<span data-ttu-id="6a0e1-186">[清單 5] 中的 [內容視圖] 頁面會覆寫 `<asp:ContentPlaceHolder>` 標記，以顯示自訂標題和自訂中繼標記。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-186">The content view page in Listing 5 overrides the `<asp:ContentPlaceHolder>` tag in order to display a custom title and custom meta tags.</span></span>

<span data-ttu-id="6a0e1-187">**清單5– `Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="6a0e1-187">**Listing 5 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample6.aspx)]

### <a name="summary"></a><span data-ttu-id="6a0e1-188">總結</span><span class="sxs-lookup"><span data-stu-id="6a0e1-188">Summary</span></span>

<span data-ttu-id="6a0e1-189">本教學課程提供您「觀看主版頁面」和「觀看內容頁面」的基本簡介。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-189">This tutorial provided you with a basic introduction to view master pages and view content pages.</span></span> <span data-ttu-id="6a0e1-190">您已瞭解如何建立新的視圖主版頁面，並根據它們建立視圖內容頁面。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-190">You learned how to create new view master pages and create view content pages based on them.</span></span> <span data-ttu-id="6a0e1-191">我們也探討了如何從特定的視圖內容頁面修改視圖主版頁面的內容。</span><span class="sxs-lookup"><span data-stu-id="6a0e1-191">We also examined how you can modify the content of a view master page from a particular view content page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6a0e1-192">[上一頁](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
> [下一頁](passing-data-to-view-master-pages-cs.md)</span><span class="sxs-lookup"><span data-stu-id="6a0e1-192">[Previous](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
[Next](passing-data-to-view-master-pages-cs.md)</span></span>
