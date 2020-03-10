---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: 第3部分：版面配置和分類功能表 |Microsoft Docs
author: JoeStagner
description: 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第3部分涵蓋新增版面配置和分類功能表。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: a223b97fd362ecf73ecde431e141021c1dcc6a6d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639115"
---
# <a name="part-3-layout-and-category-menu"></a><span data-ttu-id="cfa9d-104">第3部分：版面配置和分類功能表</span><span class="sxs-lookup"><span data-stu-id="cfa9d-104">Part 3: Layout and Category Menu</span></span>

<span data-ttu-id="cfa9d-105">依[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="cfa9d-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="cfa9d-106">Tailspin Spyworks 示範為 .NET 平臺建立功能強大、可擴充的應用程式有多麼簡單。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="cfa9d-107">它會說明如何使用 ASP.NET 4 中的絕佳新功能來建立線上商店，包括購物、結帳和管理。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="cfa9d-108">本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="cfa9d-109">第3部分涵蓋新增版面配置和分類功能表。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-109">Part 3 covers adding layout and a category menu.</span></span>

## <a id="_Toc260221669"></a><span data-ttu-id="cfa9d-110">新增一些版面配置和分類功能表</span><span class="sxs-lookup"><span data-stu-id="cfa9d-110">Adding Some Layout and a Category Menu</span></span>

<span data-ttu-id="cfa9d-111">在我們的網站主版頁面中，我們將為左側資料行新增一個 div，其中將包含產品類別目錄功能表。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-111">In our site master page we'll add a div for the left side column that will contain our product category menu.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

<span data-ttu-id="cfa9d-112">請注意，所需的對齊和其他格式會由我們新增至 Style .css 檔案的 CSS 類別提供。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-112">Note that the desired aligning and other formatting will be provided by the CSS class that we added to our Style.css file.</span></span>

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

<span data-ttu-id="cfa9d-113">[產品類別目錄] 功能表將會在執行時間以動態方式建立，方法是查詢商務資料庫中現有的產品類別目錄，並建立功能表項目和對應的連結。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-113">The product category menu will be dynamically created at runtime by querying the Commerce database for existing product categories and creating the menu items and corresponding links.</span></span>

<span data-ttu-id="cfa9d-114">為了達成此目的，我們將使用兩個 ASP。NET 的強大資料控制。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-114">To accomplish this we will use two of ASP.NET's powerful data controls.</span></span> <span data-ttu-id="cfa9d-115">「實體資料來源」控制項和「ListView」控制項。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-115">The "Entity Data Source" control and the "ListView" control.</span></span>

![](tailspin-spyworks-part-3/_static/image1.jpg)

<span data-ttu-id="cfa9d-116">讓我們切換到「設計檢視」，並使用協助程式來設定控制項。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-116">Let's switch to "Design View" and use the helpers to configure our controls.</span></span>

![](tailspin-spyworks-part-3/_static/image2.jpg)

<span data-ttu-id="cfa9d-117">讓我們將 [EntityDataSource ID] 屬性設為 [EDS\_類別目錄\_] 功能表，然後按一下 [設定資料來源]。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-117">Let's set the EntityDataSource ID property to EDS\_Category\_Menu and click on "Configure Data Source".</span></span>

![](tailspin-spyworks-part-3/_static/image3.jpg)

<span data-ttu-id="cfa9d-118">選取為我們建立商務資料庫的實體資料來源模型時所建立的 CommerceEntities 連接，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-118">Select the CommerceEntities Connection that was created for us when we created the Entity Data Source Model for our Commerce Database and click "Next".</span></span>

![](tailspin-spyworks-part-3/_static/image4.jpg)

<span data-ttu-id="cfa9d-119">選取「分類」實體集名稱，並將其餘選項保留為預設值。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-119">Select the "Categories" Entity set name and leave the rest of the options as default.</span></span> <span data-ttu-id="cfa9d-120">按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-120">Click "Finish".</span></span>

<span data-ttu-id="cfa9d-121">現在，讓我們將我們放在頁面上的 ListView 控制項實例的 ID 屬性，設定為 ListView\_ProductsMenu 並啟動其協助程式。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-121">Now let's set the ID property of the ListView control instance that we placed on our page to ListView\_ProductsMenu and activate its helper.</span></span>

![](tailspin-spyworks-part-3/_static/image5.jpg)

<span data-ttu-id="cfa9d-122">雖然我們可以使用控制項選項來格式化資料項目的顯示和格式，但我們的功能表建立只需要簡單的標記，因此我們將在來源視圖中輸入程式碼。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-122">Though we could use control options to format the data item display and formatting, our menu creation will only require simple markup so we will enter the code in the source view.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

<span data-ttu-id="cfa9d-123">請注意 "Eval" 語句： &lt;% # Eval （"類別名稱"）%&gt;</span><span class="sxs-lookup"><span data-stu-id="cfa9d-123">Please note the "Eval" statement : &lt;%# Eval("CategoryName") %&gt;</span></span>

<span data-ttu-id="cfa9d-124">ASP.NET 語法 &lt;% #%&gt; 是一個簡短的慣例，會指示執行時間執行包含在中的任何內容，並將結果輸出「行」。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-124">The ASP.NET syntax &lt;%# %&gt; is a shorthand convention that instructs the runtime to execute whatever is contained within and output the results "in Line".</span></span>

<span data-ttu-id="cfa9d-125">語句 Eval （「類別名稱」）會指示，對於已系結之資料項目集合中的目前專案，會提取實體模型專案名稱「類別目錄」的值。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-125">The statement Eval("CategoryName") instructs that, for the current entry in the bound collection of data items, fetch the value of the Entity Model item names "CategoryName".</span></span> <span data-ttu-id="cfa9d-126">這是非常強大的功能的簡潔語法。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-126">This is concise syntax for a very powerful feature.</span></span>

<span data-ttu-id="cfa9d-127">讓我們立即執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-127">Lets run the application now.</span></span>

![](tailspin-spyworks-part-3/_static/image6.jpg)

<span data-ttu-id="cfa9d-128">請注意，我們的 [產品類別] 功能表現在會顯示，當我們將滑鼠停留在其中一個 [類別] 功能表項目時，就會看到 [功能表項目] 連結指向我們尚未實名為 ProductsList 的頁面，而且我們已建立包含下列專案的動態查詢字串引數： 類別目錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="cfa9d-128">Note that our product category menu is now displayed and when we hover over one of the category menu items we can see the menu item link points to a page we have yet to implement named ProductsList.aspx and that we have built a dynamic query string argument that contains the category id.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cfa9d-129">[上一頁](tailspin-spyworks-part-2.md)
> [下一頁](tailspin-spyworks-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="cfa9d-129">[Previous](tailspin-spyworks-part-2.md)
[Next](tailspin-spyworks-part-4.md)</span></span>
