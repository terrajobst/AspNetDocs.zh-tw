---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: 主版頁面 |Microsoft Docs
author: microsoft
description: 成功網站的其中一個重要元件是一致的外觀與風格。 在 ASP.NET 1.x 中，開發人員使用使用者控制項來複寫一般頁面 elem 。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: 36f2caf7c2c9bcafd22c8f6681c1d6b19fe5078a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78567330"
---
# <a name="master-pages"></a><span data-ttu-id="e8d3f-104">主版頁面</span><span class="sxs-lookup"><span data-stu-id="e8d3f-104">Master Pages</span></span>

<span data-ttu-id="e8d3f-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e8d3f-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="e8d3f-106">成功網站的其中一個重要元件是一致的外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-106">One of the key components to a successful Web site is a consistent look and feel.</span></span> <span data-ttu-id="e8d3f-107">在 ASP.NET 1.x 中，開發人員使用使用者控制項來複寫 Web 應用程式中的一般頁面元素。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-107">In ASP.NET 1.x, developers used user controls to replicate common page elements across a Web application.</span></span> <span data-ttu-id="e8d3f-108">雖然這當然是可行的解決方案，但使用使用者控制項的確有一些缺點。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-108">While that is certainly a workable solution, using user controls does have some drawbacks.</span></span> <span data-ttu-id="e8d3f-109">例如，使用者控制項的位置變更需要跨網站變更多個頁面。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-109">For example, a change in position of a user control requires a change to multiple pages across a site.</span></span> <span data-ttu-id="e8d3f-110">使用者控制項在插入頁面之後，也不會在設計檢視中呈現。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-110">User controls are also not rendered in Design view after being inserted on a page.</span></span>

<span data-ttu-id="e8d3f-111">成功網站的其中一個重要元件是一致的外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-111">One of the key components to a successful Web site is a consistent look and feel.</span></span> <span data-ttu-id="e8d3f-112">在 ASP.NET 1.x 中，開發人員使用使用者控制項來複寫 Web 應用程式中的一般頁面元素。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-112">In ASP.NET 1.x, developers used user controls to replicate common page elements across a Web application.</span></span> <span data-ttu-id="e8d3f-113">雖然這當然是可行的解決方案，但使用使用者控制項的確有一些缺點。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-113">While that is certainly a workable solution, using user controls does have some drawbacks.</span></span> <span data-ttu-id="e8d3f-114">例如，使用者控制項的位置變更需要跨網站變更多個頁面。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-114">For example, a change in position of a user control requires a change to multiple pages across a site.</span></span> <span data-ttu-id="e8d3f-115">使用者控制項在插入頁面之後，也不會在設計檢視中呈現。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-115">User controls are also not rendered in Design view after being inserted on a page.</span></span>

<span data-ttu-id="e8d3f-116">ASP.NET 2.0 引進主版頁面做為維護一致外觀與風格的方式，而且您很快就會看到，主版頁面代表使用者控制項方法的大幅改善。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-116">ASP.NET 2.0 introduces Master pages as a way of maintaining a consistent look and feel, and as you'll soon see, Master pages represent a significant improvement over the user control method.</span></span>

## <a name="why-master-pages"></a><span data-ttu-id="e8d3f-117">為何選擇主版頁面？</span><span class="sxs-lookup"><span data-stu-id="e8d3f-117">Why Master Pages?</span></span>

<span data-ttu-id="e8d3f-118">您可能想知道為什麼 ASP.NET 2.0 中需要主版頁面。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-118">You may be wondering why master pages were needed in ASP.NET 2.0.</span></span> <span data-ttu-id="e8d3f-119">畢竟，網站開發人員已經使用 ASP.NET 1.x 中的使用者控制項，在頁面之間共用內容區域。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-119">After all, Web site developers are already using user controls in ASP.NET 1.x to share content areas between pages.</span></span> <span data-ttu-id="e8d3f-120">實際上，有幾個原因是使用者控制項是較不理想的方案，無法建立一般版面配置。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-120">There are actually several reasons why user controls are a less-than-optimal solution for creating a common layout.</span></span>

<span data-ttu-id="e8d3f-121">使用者控制項實際上不會定義頁面配置。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-121">User controls don't actually define page layout.</span></span> <span data-ttu-id="e8d3f-122">相反地，它們會定義部分頁面的版面配置和功能。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-122">Instead, they define the layout and functionality for a portion of a page.</span></span> <span data-ttu-id="e8d3f-123">這兩者的差異很重要，因為它可讓使用者控制解決方案的管理工作更加棘手。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-123">The distinction between these two is important because it makes manageability of a user control solution much more difficult.</span></span> <span data-ttu-id="e8d3f-124">例如，當您想要變更使用者控制項在頁面上的位置時，您必須編輯顯示使用者控制項的實際頁面。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-124">For example, when you want to change the position of a user control on your page, you must edit the actual page on which the user control appears.</span></span> <span data-ttu-id="e8d3f-125">如果您只有幾頁，但在大型網站中，它很快就會變成網站管理的麻煩！</span><span class="sxs-lookup"><span data-stu-id="e8d3f-125">Thats fine if you have only a few pages, but in large sites, it quickly becomes a site management nightmare!</span></span>

<span data-ttu-id="e8d3f-126">使用使用者控制項來定義一般版面配置的另一個缺點是根 ASP.NET 本身的架構。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-126">Another drawback of using user controls for defining a common layout is rooted in the architecture of ASP.NET itself.</span></span> <span data-ttu-id="e8d3f-127">如果使用者控制項的任何公開成員已變更，您就需要重新編譯所有使用該使用者控制項的頁面。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-127">If any public member of a user control is changed, it requires you to recompile all of the pages that use the user control.</span></span> <span data-ttu-id="e8d3f-128">然後，ASP.NET 會在第一次存取您的頁面時，重新將它們重設為 JIT。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-128">In turn, ASP.NET will then re-JIT your pages when they are first accessed.</span></span> <span data-ttu-id="e8d3f-129">這同樣地，會產生一個無法調整的架構，以及更大的網站的網站管理問題。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-129">This, once again, produces a non-scalable architecture and a site management problem for larger sites.</span></span>

<span data-ttu-id="e8d3f-130">ASP.NET 2.0 中的主版頁面會妥善解決這兩個問題（及其他許多）。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-130">Both of these problems (and many more) are nicely addressed by master pages in ASP.NET 2.0.</span></span>

## <a name="how-master-pages-work"></a><span data-ttu-id="e8d3f-131">主版頁面的工作方式</span><span class="sxs-lookup"><span data-stu-id="e8d3f-131">How Master Pages Work</span></span>

<span data-ttu-id="e8d3f-132">主版頁面類似于其他頁面的範本。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-132">A master page is analogous to a template for other pages.</span></span> <span data-ttu-id="e8d3f-133">應該在主版頁面中加入其他頁面（也就是功能表、框線等）之間共用的頁面元素。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-133">Page elements that should be shared among other pages (i.e. menus, borders, etc.) are added to the master page.</span></span> <span data-ttu-id="e8d3f-134">將新頁面新增至網站時，您可以將它們與主版頁面產生關聯。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-134">When new pages are added to the site, you can associate them with a master page.</span></span> <span data-ttu-id="e8d3f-135">與主版頁面相關聯的頁面稱為**內容頁面**。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-135">A page that is associated with a master page is called a **content page**.</span></span> <span data-ttu-id="e8d3f-136">根據預設，內容頁面會從主版頁面上取得外觀。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-136">By default, a content page takes on the appearance from the master page.</span></span> <span data-ttu-id="e8d3f-137">不過，當您建立主版頁面時，您可以定義內容頁面可以用自己的內容取代的部分頁面。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-137">However, when you create a master page, you can define portions of the page that the content page can replace with its own content.</span></span> <span data-ttu-id="e8d3f-138">這些部分是使用 ASP.NET 2.0 中引進的新控制項所定義;**ContentPlaceHolder**控制項。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-138">These portions are defined using a new control introduced in ASP.NET 2.0; the **ContentPlaceHolder** control.</span></span>

<span data-ttu-id="e8d3f-139">主版頁面可以包含任意數目的 ContentPlaceHolder 控制項（或完全無）。在 [內容] 頁面上，ContentPlaceHolder 控制項的內容會出現在**內容**控制項的內部，也就是 ASP.NET 2.0 中的另一個新控制項。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-139">A master page can contain any number of ContentPlaceHolder controls (or none at all.) On the content page, the content from the ContentPlaceHolder controls appears inside of **Content** controls, another new control in ASP.NET 2.0.</span></span> <span data-ttu-id="e8d3f-140">根據預設，內容頁內容控制項是空的，因此您可以提供自己的內容。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-140">By default, the content pages Content controls are empty so that you can provide your own content.</span></span> <span data-ttu-id="e8d3f-141">如果您想要使用內容控制項內主版頁面中的內容，您可以在本課程模組稍後看到。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-141">If you want to use the content from the master page inside of the Content controls, you can do so as you will see later in this module.</span></span> <span data-ttu-id="e8d3f-142">內容控制項透過內容控制項的 ContentPlaceHolderID 屬性對應至 ContentPlaceHolder 控制項。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-142">The Content control is mapped to the ContentPlaceHolder control via the ContentPlaceHolderID attribute of the Content control.</span></span> <span data-ttu-id="e8d3f-143">下列程式碼會將內容控制項對應至主版頁面上名為 mainBody 的 ContentPlaceHolder 控制項。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-143">The code below maps a Content control to a ContentPlaceHolder control called mainBody on a master page.</span></span>

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> <span data-ttu-id="e8d3f-144">您通常會聽到人們將主版頁面描述為其他頁面的基類。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-144">You will often hear people describe master pages as being a base class for other pages.</span></span> <span data-ttu-id="e8d3f-145">其實不是真的。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-145">Thats actually not true.</span></span> <span data-ttu-id="e8d3f-146">主版頁面和內容頁面之間的關聯性不是繼承的其中一個。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-146">The relationship between master pages and content pages is not one of inheritance.</span></span>

<span data-ttu-id="e8d3f-147">[**圖 1** ] 顯示主版頁面和相關聯的內容頁面，出現在 Visual Studio 2005 中。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-147">**Figure 1** shows a master page and an associated content page as they appear in Visual Studio 2005.</span></span> <span data-ttu-id="e8d3f-148">您可以在 [內容] 頁面中的主版頁面和對應的內容控制項中看到 [ContentPlaceHolder] 控制項。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-148">You can see the ContentPlaceHolder control in the master page and the corresponding Content control in the content page.</span></span> <span data-ttu-id="e8d3f-149">請注意，在 [內容] 頁面中會顯示 ContentPlaceHolder 外的主版頁面內容，但會呈現灰色。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-149">Notice that the master pages content that is outside of the ContentPlaceHolder is visible but grayed out in the content page.</span></span> <span data-ttu-id="e8d3f-150">[內容] 頁面只可會 ContentPlaceHolder 內的內容。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-150">Only the content inside of the ContentPlaceHolder can be supplanted by the content page.</span></span> <span data-ttu-id="e8d3f-151">來自主版頁面的所有其他內容都是不可變的。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-151">All other content that comes from the master page is immutable.</span></span>

![主版頁面和其相關聯的內容頁面](master-pages/_static/image1.jpg)

<span data-ttu-id="e8d3f-153">**圖 1**：主版頁面和其相關聯的內容頁面</span><span class="sxs-lookup"><span data-stu-id="e8d3f-153">**Figure 1**: A master page and its associated content page</span></span>

## <a name="creating-a-master-page"></a><span data-ttu-id="e8d3f-154">建立主版頁面</span><span class="sxs-lookup"><span data-stu-id="e8d3f-154">Creating a Master Page</span></span>

<span data-ttu-id="e8d3f-155">若要建立新的主版頁面：</span><span class="sxs-lookup"><span data-stu-id="e8d3f-155">To create a new master page:</span></span>

1. <span data-ttu-id="e8d3f-156">開啟 Visual Studio 2005，並建立新的網站。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-156">Open Visual Studio 2005 and create a new Web site.</span></span>
2. <span data-ttu-id="e8d3f-157">按一下 [檔案]、[新增]、[檔案]。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-157">Click File, New, File.</span></span>
3. <span data-ttu-id="e8d3f-158">從 [新增專案] 對話方塊中選擇 [主要檔案]，如 [**圖 2**] 所示。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-158">Choose Master File from the Add New Item dialog as shown in **figure 2**.</span></span>
4. <span data-ttu-id="e8d3f-159">按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-159">Click Add.</span></span>

![建立新的主版頁面](master-pages/_static/image2.jpg)

<span data-ttu-id="e8d3f-161">**圖 2**：建立新的主版頁面</span><span class="sxs-lookup"><span data-stu-id="e8d3f-161">**Figure 2**: Creating a New Master Page</span></span>

<span data-ttu-id="e8d3f-162">請注意，主版頁面的副檔名為 *. master*。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-162">Notice that the file extension for a master page is *.master*.</span></span> <span data-ttu-id="e8d3f-163">這是主版頁面與一般頁面不同的其中一種方式。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-163">This is one of the ways that a master page differs from an ordinary page.</span></span> <span data-ttu-id="e8d3f-164">另一個主要差異在於，在替代 @Page 指示詞的情況下，主版頁面會包含 @Master 的指示詞。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-164">The other primary difference is that in lieu of a @Page directive, the master page contains a @Master directive.</span></span> <span data-ttu-id="e8d3f-165">切換至您剛才建立之主版頁面的原始檔視圖，並查看程式碼。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-165">Switch to Source View for the master page you've just created and review the code.</span></span>

<span data-ttu-id="e8d3f-166">新的主版頁面預設會有一個 ContentPlaceHolder 控制項。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-166">A new master page will have one ContentPlaceHolder control by default.</span></span> <span data-ttu-id="e8d3f-167">在大部分的情況下，先建立一般頁面專案，然後插入需要自訂內容的 ContentPlaceHolder 控制項，會比較合理。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-167">In most cases, it makes more sense to create the common page elements first and then insert ContentPlaceHolder controls where custom content is desired.</span></span> <span data-ttu-id="e8d3f-168">在這些情況下，開發人員會想要刪除預設的 ContentPlaceHolder 控制項，並在開發網頁時插入新的控制項。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-168">In those cases, developers will want to delete the default ContentPlaceHolder control and insert new ones as the page is developed.</span></span> <span data-ttu-id="e8d3f-169">雖然 ContentPlaceHolder 控制項會顯示調整大小控點，但不能調整大小。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-169">ContentPlaceHolder controls are not resizable despite the fact that they do display sizing handles.</span></span> <span data-ttu-id="e8d3f-170">ContentPlaceHolder 控制項會根據其所包含的內容自動進行調整，但有一個例外狀況;如果您將 ContentPlaceHolder 控制項放在區塊專案（例如資料表單元格）內，它會根據專案的大小來調整大小。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-170">The ContentPlaceHolder control sizes automatically based upon the content that it contains with one exception; if you place a ContentPlaceHolder control inside of a block element such as a table cell, it will size according to the size of the element.</span></span>

## <a name="lab-1-working-with-master-pages"></a><span data-ttu-id="e8d3f-171">實驗室1使用主版頁面</span><span class="sxs-lookup"><span data-stu-id="e8d3f-171">Lab 1 Working with Master Pages</span></span>

<span data-ttu-id="e8d3f-172">在此實驗室中，您將建立新的主版頁面，並定義三個 ContentPlaceHolder 控制項。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-172">In this lab, you will create a new master page and define three ContentPlaceHolder controls.</span></span> <span data-ttu-id="e8d3f-173">接著，您會建立新的內容頁面，並從至少一個 ContentPlaceHolder 控制項中取代內容。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-173">You will then create a new Content page and replace the content from at least one of the ContentPlaceHolder controls.</span></span>

1. <span data-ttu-id="e8d3f-174">建立主版頁面並插入 ContentPlaceHolder 控制項。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-174">Create a master page and insert ContentPlaceHolder controls.</span></span> 

    1. <span data-ttu-id="e8d3f-175">如上面所述，建立新的主版頁面。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-175">Create a new master page as described above.</span></span>
    2. <span data-ttu-id="e8d3f-176">刪除預設的 ContentPlaceHolder 控制項。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-176">Delete the default ContentPlaceHolder control.</span></span>
    3. <span data-ttu-id="e8d3f-177">按一下控制項的陰影上方框線來選取 [ContentPlaceHolder] 控制項，然後按下鍵盤上的 DEL 鍵將其刪除。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-177">Select the ContentPlaceHolder control by clicking the shaded top border of the control and then delete it by hitting the DEL key on your keyboard.</span></span>
    4. <span data-ttu-id="e8d3f-178">使用*標頭和側邊*範本插入新的資料表，如 [圖 3] 所示。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-178">Insert a new table using the *Header and side* template as shown in figure 3.</span></span> <span data-ttu-id="e8d3f-179">將 [寬度] 和 [高度] 變更為 [90%]，以便在設計工具中顯示整個資料表。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-179">Change the width and height to 90% each so that the entire table is visible in the designer.</span></span>

![](master-pages/_static/image3.jpg)

<span data-ttu-id="e8d3f-180">**圖 3**</span><span class="sxs-lookup"><span data-stu-id="e8d3f-180">**Figure 3**</span></span>

1. <span data-ttu-id="e8d3f-181">將游標放入資料表的每個資料格，並將*valign*屬性設定為*top*。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-181">Place the cursor into each cell of the table and set the *valign* property to *top*.</span></span>
2. <span data-ttu-id="e8d3f-182">從 [工具箱] 中，將 ContentPlaceHolder 控制項插入資料表的頂端資料格（標頭儲存格）。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-182">From the Toolbox, insert a ContentPlaceHolder control in the top cell of the table (the header cell.)</span></span>
3. <span data-ttu-id="e8d3f-183">當您插入此 ContentPlaceHolder 控制項時，您會注意到資料列高度會佔用幾乎整個頁面，如 [圖 4] 所示。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-183">When you insert this ContentPlaceHolder control, you will notice that the row height will take up almost the entire page as shown in figure 4.</span></span> <span data-ttu-id="e8d3f-184">此時請不要擔心。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-184">Don't be concerned about that at this point.</span></span>

![空白空間與 ContentPlaceHolder 位於相同的儲存格](master-pages/_static/image1.gif)

<span data-ttu-id="e8d3f-186">**圖 4**：空的空間與 ContentPlaceHolder 位於相同的儲存格</span><span class="sxs-lookup"><span data-stu-id="e8d3f-186">**Figure 4**: The empty space is in the same cell as the ContentPlaceHolder</span></span>

1. <span data-ttu-id="e8d3f-187">將 ContentPlaceHolder 控制項放在其他兩個數據格中。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-187">Place a ContentPlaceHolder control in the other two cells.</span></span> <span data-ttu-id="e8d3f-188">插入其他 ContentPlaceHolder 控制項之後，資料表單元格的大小應該就如同您所預期。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-188">Once the other ContentPlaceHolder controls have been inserted, the size of the table cells should be as you would expect.</span></span> <span data-ttu-id="e8d3f-189">頁面現在看起來應該像 [**圖 5**] 中所示的頁面。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-189">The page should now look like the page shown in **figure 5**.</span></span>

![具有所有 ContentPlaceHolder 控制項的主要複本。](master-pages/_static/image2.gif)

<span data-ttu-id="e8d3f-192">**圖 5**：具有所有 ContentPlaceHolder 控制項的主要複本。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-192">**Figure 5**: The Master with all ContentPlaceHolder controls.</span></span> <span data-ttu-id="e8d3f-193">請注意，標頭儲存格的儲存格高度現在應該是</span><span class="sxs-lookup"><span data-stu-id="e8d3f-193">Notice that the cell height for the header cell is now what it should be</span></span>

1. <span data-ttu-id="e8d3f-194">將您選擇的一些文字輸入至三個 ContentPlaceHolder 控制項中的每一個。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-194">Enter some text of your choice into each of the three ContentPlaceHolder controls.</span></span>
2. <span data-ttu-id="e8d3f-195">將主版頁面儲存為 exercise1。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-195">Save the master page as exercise1.master.</span></span>
3. <span data-ttu-id="e8d3f-196">建立新的 Web 表單，並將它與 exercise1 主版頁面建立關聯。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-196">Create a new Web Form and associate it with the exercise1.master master page.</span></span>
4. <span data-ttu-id="e8d3f-197">選取 [檔案]、[新增]、[檔案于 Visual Studio 2005]。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-197">Select File, New, File in Visual Studio 2005.</span></span>
5. <span data-ttu-id="e8d3f-198">在 [加入新專案] 對話方塊中選取 [ **Web 表單**]。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-198">Select **Web Form** in the Add New Item dialog.</span></span>
6. <span data-ttu-id="e8d3f-199">請確定已核取 [選取主版頁面] 核取方塊，如 [圖 6] 所示。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-199">Make sure that the Select master page checkbox is checked as shown in figure 6.</span></span>

![加入新的內容頁面](master-pages/_static/image3.gif)

<span data-ttu-id="e8d3f-201">**圖 6**：新增內容頁面</span><span class="sxs-lookup"><span data-stu-id="e8d3f-201">**Figure 6**: Adding a new Content Page</span></span>

1. <span data-ttu-id="e8d3f-202">按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-202">Click Add.</span></span>
2. <span data-ttu-id="e8d3f-203">在 [選取主版頁面] 對話方塊中選取 [exercise1]，如 [圖 7] 所示。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-203">Select exercise1.master in the Select a master page dialog as shown in figure 7.</span></span>
3. <span data-ttu-id="e8d3f-204">按一下 [確定] 以新增 [內容] 頁面。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-204">Click OK to add the new content page.</span></span>

<span data-ttu-id="e8d3f-205">新增內容 頁面會出現在 Visual Studio 中，其中包含主版頁面上每個 ContentPlaceHolder 控制項的一個內容控制項。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-205">The new content page appears in Visual Studio with one Content control for each ContentPlaceHolder control on the master page.</span></span> <span data-ttu-id="e8d3f-206">根據預設，內容控制項是空的，因此您可以新增自己的內容。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-206">By default, the Content controls are empty so that you can add your own content.</span></span> <span data-ttu-id="e8d3f-207">如果您想要讓他們使用主版頁面上 ContentPlaceHolder 控制項的內容，只要按一下智慧標籤符號（控制項右上角的小型黑色箭號），然後選擇 [預設] 從智慧標籤中的 [*主目錄內容*]，如 [**圖 8**] 所示。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-207">If you'd like for them to use the content from the ContentPlaceHolder control on the master page, simply click on the smart tag symbol (the small black arrow in the upper-right corner of the control) and choose *Default to Masters Content* from the smart tag as shown in **figure 8**.</span></span> <span data-ttu-id="e8d3f-208">當您這麼做時，功能表項目會變更以*建立自訂內容*。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-208">When you do so, the menu item changes to *Create Custom Content*.</span></span> <span data-ttu-id="e8d3f-209">按一下該點就會從主版頁面移除內容，讓您定義該特定內容控制項的自訂內容。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-209">Clicking it at that point removes the content from the master page allowing you to define custom content for that particular Content control.</span></span>

![將內容控制項設為預設為主版頁面內容](master-pages/_static/image4.gif)

<span data-ttu-id="e8d3f-211">**圖 7**：將內容控制項設定為預設為主版頁面內容</span><span class="sxs-lookup"><span data-stu-id="e8d3f-211">**Figure 7**: Setting a Content Control to Default to the Master Pages Content</span></span>

## <a name="connecting-master-page-and-content-pages"></a><span data-ttu-id="e8d3f-212">連接主版頁面和內容頁面</span><span class="sxs-lookup"><span data-stu-id="e8d3f-212">Connecting Master Page and Content Pages</span></span>

<span data-ttu-id="e8d3f-213">主版頁面與內容頁面之間的關聯可以透過下列四種不同方式來設定：</span><span class="sxs-lookup"><span data-stu-id="e8d3f-213">The association between a master page and a content page can be configured in one of four different ways:</span></span>

- <span data-ttu-id="e8d3f-214">@Page 指示詞的<strong>MasterPageFile</strong>屬性</span><span class="sxs-lookup"><span data-stu-id="e8d3f-214">The <strong>MasterPageFile</strong> attribute of the @Page directive</span></span>
- <span data-ttu-id="e8d3f-215">在程式碼中設定**MasterPageFile**屬性。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-215">Setting the **Page.MasterPageFile** property in code.</span></span>
- <span data-ttu-id="e8d3f-216">應用程式佈建檔中的 **&lt;頁面&gt;** 元素（應用程式根資料夾中的 web.config）</span><span class="sxs-lookup"><span data-stu-id="e8d3f-216">The **&lt;pages&gt;** element in the applications configuration file (web.config in the root folder of the application)</span></span>
- <span data-ttu-id="e8d3f-217">子資料夾設定檔中的 **&lt;頁面&gt;** 元素（子資料夾中的 web.config）</span><span class="sxs-lookup"><span data-stu-id="e8d3f-217">The **&lt;pages&gt;** element in a subfolders configuration file (web.config in a subfolder)</span></span>

## <a name="masterpagefile-attribute"></a><span data-ttu-id="e8d3f-218">MasterPageFile 屬性</span><span class="sxs-lookup"><span data-stu-id="e8d3f-218">MasterPageFile Attribute</span></span>

<span data-ttu-id="e8d3f-219">MasterPageFile 屬性可讓您輕鬆地將主版頁面套用至特定的 ASP.NET 網頁。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-219">The MasterPageFile attribute makes it easy to apply a master page to a particular ASP.NET page.</span></span> <span data-ttu-id="e8d3f-220">當您核取 [**選取主版頁面**] 核取方塊時，它也是用來套用主版頁面的方法，就像在練習1中所做的一樣。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-220">It is also the method used to apply the master page when you check the **Select Master Page** checkbox as you did in Exercise 1.</span></span>

## <a name="setting-pagemasterpagefile-in-code"></a><span data-ttu-id="e8d3f-221">在程式碼中設定頁面 MasterPageFile</span><span class="sxs-lookup"><span data-stu-id="e8d3f-221">Setting Page.MasterPageFile in Code</span></span>

<span data-ttu-id="e8d3f-222">藉由在程式碼中設定 MasterPageFile 屬性，您可以在執行時間將特定的主版頁面套用至內容。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-222">By setting the MasterPageFile property in code, you can apply a particular master page to your content at runtime.</span></span> <span data-ttu-id="e8d3f-223">當您可能需要根據使用者角色或其他準則來套用特定的主版頁面時，這會很有用。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-223">This is useful in cases where you may need to apply a specific master page based upon a users role or some other criteria.</span></span> <span data-ttu-id="e8d3f-224">MasterPageFile 屬性必須在 PreInit 方法中設定。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-224">The MasterPageFile property must be set in the PreInit method.</span></span> <span data-ttu-id="e8d3f-225">如果它是在 PreInit 方法之後設定，則會擲回 InvalidOperationException。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-225">If it is set after the PreInit method, an InvalidOperationException will be thrown.</span></span> <span data-ttu-id="e8d3f-226">設定此屬性的頁面也必須有內容控制項，做為頁面的最上層控制項。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-226">The page on which this property is being set must also have a Content control as the top-level control for the page.</span></span> <span data-ttu-id="e8d3f-227">否則，當設定 MasterPageFile 屬性時，將會擲回 HttpException。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-227">Otherwise an HttpException will be thrown when the MasterPageFile property is set.</span></span>

## <a name="using-the-ltpagesgt-element"></a><span data-ttu-id="e8d3f-228">使用 &lt;頁面&gt; 元素</span><span class="sxs-lookup"><span data-stu-id="e8d3f-228">Using the &lt;pages&gt; Element</span></span>

<span data-ttu-id="e8d3f-229">您可以設定網頁的主版頁面，方法是在 web.config 檔案的 &lt;頁面&gt; 元素中，設定 masterPageFile 屬性。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-229">You can configure a master page for your pages by setting the masterPageFile attribute in the &lt;pages&gt; element of the web.config file.</span></span> <span data-ttu-id="e8d3f-230">使用此方法時，請記住，應用程式結構中較低的 web.config 檔案可以覆寫此設定。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-230">When using this method, keep in mind that web.config files lower in the application structure can override this setting.</span></span> <span data-ttu-id="e8d3f-231">在 @Page 指示詞中設定的任何 MasterPageFile 屬性也會覆寫此設定。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-231">Any MasterPageFile attribute set in a @Page directive will also override this setting.</span></span> <span data-ttu-id="e8d3f-232">使用 &lt;頁面&gt; 專案，可讓您輕鬆地建立*主要*主版頁面，視需要在特定資料夾或檔案中加以覆寫。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-232">Using the &lt;pages&gt; element makes it simple to create a *master* master page that can be overridden if necessary in particular folders or files.</span></span>

## <a name="properties-in-master-pages"></a><span data-ttu-id="e8d3f-233">主版頁面中的屬性</span><span class="sxs-lookup"><span data-stu-id="e8d3f-233">Properties in Master Pages</span></span>

<span data-ttu-id="e8d3f-234">主版頁面只要在主版頁面中公開這些屬性，就可以公開屬性。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-234">A master page can expose properties by simply making those properties public within the master page.</span></span> <span data-ttu-id="e8d3f-235">例如，下列程式碼會定義名為 SomeProperty 的屬性：</span><span class="sxs-lookup"><span data-stu-id="e8d3f-235">For example, the following code defines a property called SomeProperty:</span></span>

[!code-csharp[Main](master-pages/samples/sample2.cs)]

<span data-ttu-id="e8d3f-236">若要從 [內容] 頁面存取 [SomeProperty] 屬性，您必須使用 Master 屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e8d3f-236">To access the SomeProperty property from the Content page, you will need to use the Master property like so:</span></span>

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a><span data-ttu-id="e8d3f-237">嵌套主版頁面</span><span class="sxs-lookup"><span data-stu-id="e8d3f-237">Nesting Master Pages</span></span>

<span data-ttu-id="e8d3f-238">主版頁面是確保跨大型 Web 應用程式的常見外觀與風格的絕佳解決方案。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-238">Master pages are the perfect solution for ensuring a common look and feel across a large Web application.</span></span> <span data-ttu-id="e8d3f-239">不過，大型網站的某些部分共用通用介面並不常見，而其他部分則共用不同的介面。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-239">However, it's not uncommon to have certain parts of a large site share a common interface while other parts share a different interface.</span></span> <span data-ttu-id="e8d3f-240">若要解決此需求，有多個主版頁面是完美的解決方案。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-240">To address that need, multiple master pages are the perfect solution.</span></span> <span data-ttu-id="e8d3f-241">不過，仍然無法解決大型應用程式可能會有某些元件（例如功能表）在所有頁面和其他只在網站特定區段共用的元件之間共用的事實。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-241">However, that still doesn't address the fact that a large application may have certain components (such as a menu, for example) that are shared among all pages and other components that are shared only among certain sections of the site.</span></span> <span data-ttu-id="e8d3f-242">針對這種情況，嵌套主版頁面會適當地填滿需求。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-242">For that type of situation, nested master pages fill the need nicely.</span></span> <span data-ttu-id="e8d3f-243">如您所見，一般主版頁面包含主版頁面和內容頁面。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-243">As you've seen, a normal master page consists of a master page and a content page.</span></span> <span data-ttu-id="e8d3f-244">在嵌套主版頁面的情況下，有兩個主版頁面;父主機和子主機。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-244">In a nested master page situation, there are two master pages; a parent master and a child master.</span></span> <span data-ttu-id="e8d3f-245">子主版頁面也是 [內容] 頁面，而其主要頁面是 [父系] 主版頁面。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-245">The child master page is also a content page and its master is the parent master page.</span></span>

<span data-ttu-id="e8d3f-246">以下是一般主版頁面的程式碼：</span><span class="sxs-lookup"><span data-stu-id="e8d3f-246">Here is the code for a typical master page:</span></span>

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

<span data-ttu-id="e8d3f-247">在嵌套的主要案例中，這會是父主機。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-247">In a nested master scenario, this would be the parent master.</span></span> <span data-ttu-id="e8d3f-248">另一個主版頁面會使用此頁面作為其主版頁面，而該程式碼看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="e8d3f-248">Another master page would use this page as its master page, and that code would look like this:</span></span>

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

<span data-ttu-id="e8d3f-249">請注意，在此案例中，子主要複本也是父主機的內容頁面。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-249">Note that in this scenario, the child master is also a content page for the parent master.</span></span> <span data-ttu-id="e8d3f-250">所有子主機的內容都會出現在內容控制項的內部，而該控制項會從父系的 ContentPlaceHolder 控制項取得其內容。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-250">All of the child master's content appears inside of a Content control that gets its content from the parent's ContentPlaceHolder control.</span></span>

> [!NOTE]
> <span data-ttu-id="e8d3f-251">設計工具支援不適用於嵌套主版頁面。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-251">Designer support is not available for nested master pages.</span></span> <span data-ttu-id="e8d3f-252">當您使用「嵌套式主機」進行開發時，您必須使用「來源視圖」。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-252">When you are developing using nested masters, you will need to use source view.</span></span>

<span data-ttu-id="e8d3f-253">這段影片會示範如何使用嵌套主版頁面的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="e8d3f-253">This video shows a walkthrough of using nested master pages.</span></span>

![](master-pages/_static/image1.png)

[<span data-ttu-id="e8d3f-254">開啟全螢幕影片</span><span class="sxs-lookup"><span data-stu-id="e8d3f-254">Open Full-Screen Video</span></span>](master-pages/_static/nested1.wmv)

![選取主版頁面](master-pages/_static/image4.jpg)

<span data-ttu-id="e8d3f-256">**圖 8**：選取主版頁面</span><span class="sxs-lookup"><span data-stu-id="e8d3f-256">**Figure 8**: Selecting a Master Page</span></span>
