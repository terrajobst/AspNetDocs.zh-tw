---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
title: 使用 TagBuilder 類別來建立 HTML 協助程式（VB） |Microsoft Docs
author: StephenWalther
description: Stephen Walther 將為您介紹名為 TagBuilder 類別的 ASP.NET MVC 架構中實用的公用程式類別。 您可以輕鬆地使用 TagBuilder 類別 。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: ec26f264-d0ea-4031-9943-825505a3ac4b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 3b0aa9816209cc326d3dea4b8dfb1b13cf697fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78599999"
---
# <a name="using-the-tagbuilder-class-to-build-html-helpers-vb"></a><span data-ttu-id="44d14-104">使用 TagBuilder 類別來建立 HTML 協助程式（VB）</span><span class="sxs-lookup"><span data-stu-id="44d14-104">Using the TagBuilder Class to Build HTML Helpers (VB)</span></span>

<span data-ttu-id="44d14-105">依[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="44d14-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="44d14-106">Stephen Walther 將為您介紹名為 TagBuilder 類別的 ASP.NET MVC 架構中實用的公用程式類別。</span><span class="sxs-lookup"><span data-stu-id="44d14-106">Stephen Walther introduces you to a useful utility class in the ASP.NET MVC framework named the TagBuilder class.</span></span> <span data-ttu-id="44d14-107">您可以使用 TagBuilder 類別，輕鬆地建立 HTML 標籤。</span><span class="sxs-lookup"><span data-stu-id="44d14-107">You can use the TagBuilder class to easily build HTML tags.</span></span>

<span data-ttu-id="44d14-108">ASP.NET MVC 架構包含一個有用的公用程式類別，名為 TagBuilder 類別，可讓您在建立 HTML helper 時使用。</span><span class="sxs-lookup"><span data-stu-id="44d14-108">The ASP.NET MVC framework includes a useful utility class named the TagBuilder class that you can use when building HTML helpers.</span></span> <span data-ttu-id="44d14-109">TagBuilder 類別，做為類別名稱的建議，可讓您輕鬆地建立 HTML 標籤。</span><span class="sxs-lookup"><span data-stu-id="44d14-109">The TagBuilder class, as the name of the class suggests, enables you to easily build HTML tags.</span></span> <span data-ttu-id="44d14-110">在這個簡短的教學課程中，您會看到 TagBuilder 類別的總覽，並瞭解如何在建立可轉譯 HTML &lt;img&gt; 標記的簡單 HTML helper 時，使用這個類別。</span><span class="sxs-lookup"><span data-stu-id="44d14-110">In this brief tutorial, you are provided with an overview of the TagBuilder class and you learn how to use this class when building a simple HTML helper that renders HTML &lt;img&gt; tags.</span></span>

## <a name="overview-of-the-tagbuilder-class"></a><span data-ttu-id="44d14-111">TagBuilder 類別的總覽</span><span class="sxs-lookup"><span data-stu-id="44d14-111">Overview of the TagBuilder Class</span></span>

<span data-ttu-id="44d14-112">TagBuilder 類別包含在 System.web 命名空間中。</span><span class="sxs-lookup"><span data-stu-id="44d14-112">The TagBuilder class is contained in the System.Web.Mvc namespace.</span></span> <span data-ttu-id="44d14-113">它有五個方法：</span><span class="sxs-lookup"><span data-stu-id="44d14-113">It has five methods:</span></span>

- <span data-ttu-id="44d14-114">AddCssClass （）–可讓您將新的*class = ""* 屬性新增至標記。</span><span class="sxs-lookup"><span data-stu-id="44d14-114">AddCssClass() – Enables you to add a new *class=""* attribute to a tag.</span></span>
- <span data-ttu-id="44d14-115">GenerateId （）–可讓您將 id 屬性新增至標記。</span><span class="sxs-lookup"><span data-stu-id="44d14-115">GenerateId() – Enables you to add an id attribute to a tag.</span></span> <span data-ttu-id="44d14-116">這個方法會自動取代識別碼中的句號（根據預設，句號會以底線取代）</span><span class="sxs-lookup"><span data-stu-id="44d14-116">This method automatically replaces periods in the id (by default, periods are replaced by underscores)</span></span>
- <span data-ttu-id="44d14-117">MergeAttribute （）–可讓您將屬性新增至標記。</span><span class="sxs-lookup"><span data-stu-id="44d14-117">MergeAttribute() – Enables you to add attributes to a tag.</span></span> <span data-ttu-id="44d14-118">這個方法有多個多載。</span><span class="sxs-lookup"><span data-stu-id="44d14-118">There are multiple overloads of this method.</span></span>
- <span data-ttu-id="44d14-119">SetInnerText （）–可讓您設定標記的內部文字。</span><span class="sxs-lookup"><span data-stu-id="44d14-119">SetInnerText() – Enables you to set the inner text of the tag.</span></span> <span data-ttu-id="44d14-120">內部文字會自動進行 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="44d14-120">The inner text is HTML encode automatically.</span></span>
- <span data-ttu-id="44d14-121">ToString （）–可讓您呈現標記。</span><span class="sxs-lookup"><span data-stu-id="44d14-121">ToString() – Enables you to render the tag.</span></span> <span data-ttu-id="44d14-122">您可以指定是否要建立一般標記、開始標記、結束標記或自我結束記號。</span><span class="sxs-lookup"><span data-stu-id="44d14-122">You can specify whether you want to create a normal tag, a start tag, an end tag, or a self-closing tag.</span></span>

<span data-ttu-id="44d14-123">TagBuilder 類別有四個重要的屬性：</span><span class="sxs-lookup"><span data-stu-id="44d14-123">The TagBuilder class has four important properties:</span></span>

- <span data-ttu-id="44d14-124">屬性–代表標記的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="44d14-124">Attributes – Represents all of the attributes of the tag.</span></span>
- <span data-ttu-id="44d14-125">IdAttributeDotReplacement –代表 GenerateId （）方法用來取代句號的字元（預設值為底線）。</span><span class="sxs-lookup"><span data-stu-id="44d14-125">IdAttributeDotReplacement – Represents the character used by the GenerateId() method to replace periods (the default is an underscore).</span></span>
- <span data-ttu-id="44d14-126">InnerHTML –代表標記的內部內容。</span><span class="sxs-lookup"><span data-stu-id="44d14-126">InnerHTML – Represents the inner contents of the tag.</span></span> <span data-ttu-id="44d14-127">將字串指派給這個屬性*並不會*對字串進行 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="44d14-127">Assigning a string to this property *does not* HTML encode the string.</span></span>
- <span data-ttu-id="44d14-128">TagName –代表標記的名稱。</span><span class="sxs-lookup"><span data-stu-id="44d14-128">TagName – Represents the name of the tag.</span></span>

<span data-ttu-id="44d14-129">這些方法和屬性會提供您建立 HTML 標籤所需的所有基本方法和屬性。</span><span class="sxs-lookup"><span data-stu-id="44d14-129">These methods and properties give you all of the basic methods and properties that you need to build up an HTML tag.</span></span> <span data-ttu-id="44d14-130">您實際上不需要使用 TagBuilder 類別。</span><span class="sxs-lookup"><span data-stu-id="44d14-130">You don't really need to use the TagBuilder class.</span></span> <span data-ttu-id="44d14-131">您可以改用 StringBuilder 類別。</span><span class="sxs-lookup"><span data-stu-id="44d14-131">You could use a StringBuilder class instead.</span></span> <span data-ttu-id="44d14-132">不過，TagBuilder 類別讓您的生活變得更簡單。</span><span class="sxs-lookup"><span data-stu-id="44d14-132">However, the TagBuilder class makes your life a little easier.</span></span>

## <a name="creating-an-image-html-helper"></a><span data-ttu-id="44d14-133">建立影像 HTML Helper</span><span class="sxs-lookup"><span data-stu-id="44d14-133">Creating an Image HTML Helper</span></span>

<span data-ttu-id="44d14-134">當您建立 TagBuilder 類別的實例時，會將您要建立的標記名稱傳遞至 TagBuilder 的函式。</span><span class="sxs-lookup"><span data-stu-id="44d14-134">When you create an instance of the TagBuilder class, you pass the name of the tag that you want to build to the TagBuilder constructor.</span></span> <span data-ttu-id="44d14-135">接下來，您可以呼叫方法（例如 AddCssClass 和 MergeAttribute （）方法）來修改標記的屬性。</span><span class="sxs-lookup"><span data-stu-id="44d14-135">Next, you can call methods like the AddCssClass and MergeAttribute() methods to modify the attributes of the tag.</span></span> <span data-ttu-id="44d14-136">最後，您可以呼叫 ToString （）方法來呈現標記。</span><span class="sxs-lookup"><span data-stu-id="44d14-136">Finally, you call the ToString() method to render the tag.</span></span>

<span data-ttu-id="44d14-137">例如，[清單 1] 包含影像 HTML helper。</span><span class="sxs-lookup"><span data-stu-id="44d14-137">For example, Listing 1 contains an Image HTML helper.</span></span> <span data-ttu-id="44d14-138">影像協助程式會在內部實作為 TagBuilder，表示 HTML &lt;img&gt; 標記。</span><span class="sxs-lookup"><span data-stu-id="44d14-138">The Image helper is implemented internally with a TagBuilder that represents an HTML &lt;img&gt; tag.</span></span>

<span data-ttu-id="44d14-139">**清單1– Helpers\ImageHelper.vb**</span><span class="sxs-lookup"><span data-stu-id="44d14-139">**Listing 1 – Helpers\ImageHelper.vb**</span></span>

[!code-vb[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample1.vb)]

<span data-ttu-id="44d14-140">[清單 1] 中的模組包含兩個名為 Image （）的多載方法。</span><span class="sxs-lookup"><span data-stu-id="44d14-140">The module in Listing 1 contains two overloaded methods named Image().</span></span> <span data-ttu-id="44d14-141">當您呼叫 Image （）方法時，可以傳遞代表一組 HTML 屬性的物件。</span><span class="sxs-lookup"><span data-stu-id="44d14-141">When you call the Image() method, you can pass an object which represents a set of HTML attributes or not.</span></span>

<span data-ttu-id="44d14-142">請注意如何使用 TagBuilder. MergeAttribute （）方法，將個別屬性（例如 src 屬性）新增至 TagBuilder。</span><span class="sxs-lookup"><span data-stu-id="44d14-142">Notice how the TagBuilder.MergeAttribute() method is used to add individual attributes such as the src attribute to the TagBuilder.</span></span> <span data-ttu-id="44d14-143">此外，請注意如何使用 TagBuilder. MergeAttributes （）方法，將屬性集合加入至 TagBuilder。</span><span class="sxs-lookup"><span data-stu-id="44d14-143">Notice, furthermore, how the TagBuilder.MergeAttributes() method is used to add a collection of attributes to the TagBuilder.</span></span> <span data-ttu-id="44d14-144">MergeAttributes （）方法會接受字典&lt;字串，物件&gt; 參數。</span><span class="sxs-lookup"><span data-stu-id="44d14-144">The MergeAttributes() method accepts a Dictionary&lt;string,object&gt; parameter.</span></span> <span data-ttu-id="44d14-145">RouteValueDictionary 類別是用來將代表屬性集合的物件，轉換成字典&lt;字串，物件&gt;。</span><span class="sxs-lookup"><span data-stu-id="44d14-145">The RouteValueDictionary class is used to convert the Object representing the collection of attributes into a Dictionary&lt;string,object&gt;.</span></span>

<span data-ttu-id="44d14-146">建立映射協助程式之後，您就可以在 ASP.NET MVC views 中使用 helper，就像任何其他標準 HTML helper 一樣。</span><span class="sxs-lookup"><span data-stu-id="44d14-146">After you create the Image helper, you can use the helper in your ASP.NET MVC views just like any of the other standard HTML helpers.</span></span> <span data-ttu-id="44d14-147">[清單 2] 中的視圖使用影像協助程式顯示 Xbox 的相同影像兩次（請參閱 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="44d14-147">The view in Listing 2 uses the Image helper to display the same image of an Xbox twice (see Figure 1).</span></span> <span data-ttu-id="44d14-148">不論是否有 HTML 屬性集合，都會呼叫 Image （）協助程式。</span><span class="sxs-lookup"><span data-stu-id="44d14-148">The Image() helper is called both with and without an HTML attribute collection.</span></span>

<span data-ttu-id="44d14-149">**清單2– Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="44d14-149">**Listing 2 – Home\Index.aspx**</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample2.aspx)]

<span data-ttu-id="44d14-150">[![[新增專案] 對話方塊](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="44d14-150">[![The New Project dialog box](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)</span></span>

<span data-ttu-id="44d14-151">**圖 01**：使用影像協助程式（[按一下以觀看完整大小的影像](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="44d14-151">**Figure 01**: Using the Image helper([Click to view full-size image](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png))</span></span>

<span data-ttu-id="44d14-152">請注意，您必須在 [default.aspx] 視圖的頂端匯入與影像協助程式關聯的命名空間。</span><span class="sxs-lookup"><span data-stu-id="44d14-152">Notice that you must import the namespace associated with the Image helper at the top of the Index.aspx view.</span></span> <span data-ttu-id="44d14-153">Helper 會以下列指示詞彙入：</span><span class="sxs-lookup"><span data-stu-id="44d14-153">The helper is imported with the following directive:</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample3.aspx)]

<span data-ttu-id="44d14-154">在 Visual Basic 應用程式中，預設命名空間與應用程式的名稱相同。</span><span class="sxs-lookup"><span data-stu-id="44d14-154">In a Visual Basic application, the default namespace is the same as the name of the application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="44d14-155">[上一頁](creating-custom-html-helpers-vb.md)
> [下一頁](creating-page-layouts-with-view-master-pages-vb.md)</span><span class="sxs-lookup"><span data-stu-id="44d14-155">[Previous](creating-custom-html-helpers-vb.md)
[Next](creating-page-layouts-with-view-master-pages-vb.md)</span></span>
