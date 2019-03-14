---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
title: 使用 TagBuilder 類別可建置 HTML 協助程式 (C#) |Microsoft Docs
author: StephenWalther
description: Stephen Walther 會向您介紹在 ASP.NET MVC framework 將 TagBuilder 類別命名為實用的公用程式類別。 您可以輕鬆地使用 TagBuilder 類別可...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 3975a52f-bd15-4edd-8f3d-1df93672515b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 9759ea9b05ba5eba268901d3d2d1a15b2afe6202
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57055925"
---
<a name="using-the-tagbuilder-class-to-build-html-helpers-c"></a><span data-ttu-id="1a9a2-104">使用 TagBuilder 類別可建置 HTML 協助程式 (C#)</span><span class="sxs-lookup"><span data-stu-id="1a9a2-104">Using the TagBuilder Class to Build HTML Helpers (C#)</span></span>
====================
<span data-ttu-id="1a9a2-105">藉由[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="1a9a2-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="1a9a2-106">Stephen Walther 會向您介紹在 ASP.NET MVC framework 將 TagBuilder 類別命名為實用的公用程式類別。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-106">Stephen Walther introduces you to a useful utility class in the ASP.NET MVC framework named the TagBuilder class.</span></span> <span data-ttu-id="1a9a2-107">您可以使用 TagBuilder 類別，輕鬆地建置 HTML 標記。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-107">You can use the TagBuilder class to easily build HTML tags.</span></span>


<span data-ttu-id="1a9a2-108">ASP.NET MVC 架構包括名為 TagBuilder 類別可建置 HTML 協助程式時，您可以使用的實用的公用程式類別。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-108">The ASP.NET MVC framework includes a useful utility class named the TagBuilder class that you can use when building HTML helpers.</span></span> <span data-ttu-id="1a9a2-109">TagBuilder 類別名所示的類別，可讓您輕鬆地建置 HTML 標記。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-109">The TagBuilder class, as the name of the class suggests, enables you to easily build HTML tags.</span></span> <span data-ttu-id="1a9a2-110">在這個簡短的教學課程中，為您提供 TagBuilder 類別的概觀和您將了解如何使用這個類別，當建置簡單的 HTML helper 來呈現 HTML &lt;img&gt;標記。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-110">In this brief tutorial, you are provided with an overview of the TagBuilder class and you learn how to use this class when building a simple HTML helper that renders HTML &lt;img&gt; tags.</span></span>

## <a name="overview-of-the-tagbuilder-class"></a><span data-ttu-id="1a9a2-111">TagBuilder 類別的概觀</span><span class="sxs-lookup"><span data-stu-id="1a9a2-111">Overview of the TagBuilder Class</span></span>

<span data-ttu-id="1a9a2-112">TagBuilder 類別包含在 System.Web.Mvc 命名空間中。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-112">The TagBuilder class is contained in the System.Web.Mvc namespace.</span></span> <span data-ttu-id="1a9a2-113">它有五個方法：</span><span class="sxs-lookup"><span data-stu-id="1a9a2-113">It has five methods:</span></span>

- <span data-ttu-id="1a9a2-114">AddCssClass()-可讓您新增的新*類別 =""* 屬性標記。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-114">AddCssClass() - Enables you to add a new *class=""* attribute to a tag.</span></span>
- <span data-ttu-id="1a9a2-115">GenerateId()-可讓您將識別碼屬性新增至標記。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-115">GenerateId() - Enables you to add an id attribute to a tag.</span></span> <span data-ttu-id="1a9a2-116">這個方法會自動取代識別碼中的句點 （根據預設，週期會以底線取代）</span><span class="sxs-lookup"><span data-stu-id="1a9a2-116">This method automatically replaces periods in the id (by default, periods are replaced by underscores)</span></span>
- <span data-ttu-id="1a9a2-117">MergeAttribute()-可讓您將屬性加入至標記。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-117">MergeAttribute() - Enables you to add attributes to a tag.</span></span> <span data-ttu-id="1a9a2-118">有多個多載，這個方法。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-118">There are multiple overloads of this method.</span></span>
- <span data-ttu-id="1a9a2-119">SetInnerText()-可讓您設定標記的內部文字。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-119">SetInnerText() - Enables you to set the inner text of the tag.</span></span> <span data-ttu-id="1a9a2-120">內部文字會自動對 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-120">The inner text is HTML encode automatically.</span></span>
- <span data-ttu-id="1a9a2-121">Tostring （）-可讓您呈現標記。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-121">ToString() - Enables you to render the tag.</span></span> <span data-ttu-id="1a9a2-122">您可以指定是否要建立的標準標記、 開始標記、 結束標記或自我結尾標記。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-122">You can specify whether you want to create a normal tag, a start tag, an end tag, or a self-closing tag.</span></span>
  

<span data-ttu-id="1a9a2-123">TagBuilder 類別有四個重要的屬性：</span><span class="sxs-lookup"><span data-stu-id="1a9a2-123">The TagBuilder class has four important properties:</span></span>

- <span data-ttu-id="1a9a2-124">屬性-代表所有標記的屬性。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-124">Attributes - Represents all of the attributes of the tag.</span></span>
- <span data-ttu-id="1a9a2-125">IdAttributeDotReplacement-表示 GenerateId() 方法用來取代的期間 （預設值為底線） 的字元。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-125">IdAttributeDotReplacement - Represents the character used by the GenerateId() method to replace periods (the default is an underscore).</span></span>
- <span data-ttu-id="1a9a2-126">InnerHTML-表示標記的內部的內容。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-126">InnerHTML - Represents the inner contents of the tag.</span></span> <span data-ttu-id="1a9a2-127">將字串指派給這個屬性*則否*HTML 編碼字串。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-127">Assigning a string to this property *does not* HTML encode the string.</span></span>
- <span data-ttu-id="1a9a2-128">TagName-表示標記的名稱。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-128">TagName - Represents the name of the tag.</span></span>

<span data-ttu-id="1a9a2-129">這些方法和屬性提供給您所有的基本的方法和您要建置的 HTML 標記的屬性。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-129">These methods and properties give you all of the basic methods and properties that you need to build up an HTML tag.</span></span> <span data-ttu-id="1a9a2-130">您真的不需要使用 TagBuilder 類別。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-130">You don't really need to use the TagBuilder class.</span></span> <span data-ttu-id="1a9a2-131">您可以改為使用 StringBuilder 類別。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-131">You could use a StringBuilder class instead.</span></span> <span data-ttu-id="1a9a2-132">不過，TagBuilder 類別可讓您的生活更輕鬆。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-132">However, the TagBuilder class makes your life a little easier.</span></span>

## <a name="creating-an-image-html-helper"></a><span data-ttu-id="1a9a2-133">建立映像 HTML 協助程式</span><span class="sxs-lookup"><span data-stu-id="1a9a2-133">Creating an Image HTML Helper</span></span>

<span data-ttu-id="1a9a2-134">當您建立 TagBuilder 類別的執行個體時，您會傳遞您想要建置 TagBuilder 建構函式的標記名稱。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-134">When you create an instance of the TagBuilder class, you pass the name of the tag that you want to build to the TagBuilder constructor.</span></span> <span data-ttu-id="1a9a2-135">接下來，您可以呼叫方法，例如 AddCssClass 和 MergeAttribute() 方法修改標記的屬性。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-135">Next, you can call methods like the AddCssClass and MergeAttribute() methods to modify the attributes of the tag.</span></span> <span data-ttu-id="1a9a2-136">最後，您會呼叫 tostring （） 方法，來呈現標記。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-136">Finally, you call the ToString() method to render the tag.</span></span>

<span data-ttu-id="1a9a2-137">例如，列表 1 包含的映像 HTML 協助程式。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-137">For example, Listing 1 contains an Image HTML helper.</span></span> <span data-ttu-id="1a9a2-138">影像協助程式在內部實作代表 HTML TagBuilder &lt;img&gt;標記。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-138">The Image helper is implemented internally with a TagBuilder that represents an HTML &lt;img&gt; tag.</span></span>

<span data-ttu-id="1a9a2-139">**列表 1-Helpers\ImageHelper.cs**</span><span class="sxs-lookup"><span data-stu-id="1a9a2-139">**Listing 1 - Helpers\ImageHelper.cs**</span></span>

[!code-csharp[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample1.cs)]

<span data-ttu-id="1a9a2-140">列表 1 中的類別包含兩個靜態的多載的方法，名為映像。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-140">The class in Listing 1 contains two static overloaded methods named Image.</span></span> <span data-ttu-id="1a9a2-141">當您呼叫 Image() 方法時，您可以傳遞或不代表一組 HTML 屬性的物件。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-141">When you call the Image() method, you can pass an object which represents a set of HTML attributes or not.</span></span>

<span data-ttu-id="1a9a2-142">請注意 TagBuilder.MergeAttribute() 方法用來將個別的屬性，例如 src 屬性新增至 TagBuilder 的方式。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-142">Notice how the TagBuilder.MergeAttribute() method is used to add individual attributes such as the src attribute to the TagBuilder.</span></span> <span data-ttu-id="1a9a2-143">請注意，此外，將屬性的集合新增至 TagBuilder 用法 TagBuilder.MergeAttributes() 方法。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-143">Notice, furthermore, how the TagBuilder.MergeAttributes() method is used to add a collection of attributes to the TagBuilder.</span></span> <span data-ttu-id="1a9a2-144">MergeAttributes() 方法接受字典&lt;string，object&gt;參數。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-144">The MergeAttributes() method accepts a Dictionary&lt;string,object&gt; parameter.</span></span> <span data-ttu-id="1a9a2-145">RouteValueDictionary 類別用來轉換物件，表示為字典的屬性集合&lt;string，object&gt;。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-145">The RouteValueDictionary class is used to convert the Object representing the collection of attributes into a Dictionary&lt;string,object&gt;.</span></span>

<span data-ttu-id="1a9a2-146">建立影像協助程式之後，您可以使用協助程式，在您的 ASP.NET MVC 檢視就像任何其他標準的 HTML 協助程式。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-146">After you create the Image helper, you can use the helper in your ASP.NET MVC views just like any of the other standard HTML helpers.</span></span> <span data-ttu-id="1a9a2-147">列表 2 中的檢視使用影像協助程式兩次顯示 Xbox 的相同映像 （請參閱 圖 1）。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-147">The view in Listing 2 uses the Image helper to display the same image of an Xbox twice (see Figure 1).</span></span> <span data-ttu-id="1a9a2-148">Image() 協助程式會呼叫具有和沒有 HTML 屬性集合。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-148">The Image() helper is called both with and without an HTML attribute collection.</span></span>

<span data-ttu-id="1a9a2-149">**列表 2-Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="1a9a2-149">**Listing 2 - Home\Index.aspx**</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample2.aspx)]


<span data-ttu-id="1a9a2-150">[![[新增專案] 對話方塊](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1a9a2-150">[![The New Project dialog box](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="1a9a2-151">**圖 01**:使用影像協助程式 ([按一下以檢視完整大小的影像](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="1a9a2-151">**Figure 01**: Using the Image helper([Click to view full-size image](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png))</span></span>


<span data-ttu-id="1a9a2-152">請注意，您必須匯入影像協助程式頂端的 Index.aspx 檢視相關聯的命名空間。</span><span class="sxs-lookup"><span data-stu-id="1a9a2-152">Notice that you must import the namespace associated with the Image helper at the top of the Index.aspx view.</span></span> <span data-ttu-id="1a9a2-153">使用下列指示詞，匯入協助程式：</span><span class="sxs-lookup"><span data-stu-id="1a9a2-153">The helper is imported with the following directive:</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample3.aspx)]

> [!div class="step-by-step"]
> <span data-ttu-id="1a9a2-154">[上一頁](creating-custom-html-helpers-cs.md)
> [下一頁](creating-page-layouts-with-view-master-pages-cs.md)</span><span class="sxs-lookup"><span data-stu-id="1a9a2-154">[Previous](creating-custom-html-helpers-cs.md)
[Next](creating-page-layouts-with-view-master-pages-cs.md)</span></span>