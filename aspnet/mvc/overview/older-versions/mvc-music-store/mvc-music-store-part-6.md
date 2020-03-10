---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
title: 第6部分：使用資料批註進行模型驗證 |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第6部分涵蓋使用模型 V 的資料批註 。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: b3193d33-2d0b-4d98-9712-58bd897c62ec
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
msc.type: authoredcontent
ms.openlocfilehash: bc031dd5be61cc6707c522f85f6af77a420c8b31
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539274"
---
# <a name="part-6-using-data-annotations-for-model-validation"></a><span data-ttu-id="e2242-104">第6部分：使用資料批註進行模型驗證</span><span class="sxs-lookup"><span data-stu-id="e2242-104">Part 6: Using Data Annotations for Model Validation</span></span>

<span data-ttu-id="e2242-105">依[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="e2242-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="e2242-106">MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 web 程式開發的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="e2242-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="e2242-107">MVC 音樂存放區是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。</span><span class="sxs-lookup"><span data-stu-id="e2242-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="e2242-108">本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="e2242-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="e2242-109">第6部分涵蓋使用資料批註進行模型驗證。</span><span class="sxs-lookup"><span data-stu-id="e2242-109">Part 6 covers Using Data Annotations for Model Validation.</span></span>

<span data-ttu-id="e2242-110">我們的建立和編輯表單有一個重大的問題：它們不會進行任何驗證。</span><span class="sxs-lookup"><span data-stu-id="e2242-110">We have a major issue with our Create and Edit forms: they're not doing any validation.</span></span> <span data-ttu-id="e2242-111">我們可以執行一些動作，像是在 Price 欄位中保留必要欄位空白或輸入字母，而我們看到的第一個錯誤是來自資料庫。</span><span class="sxs-lookup"><span data-stu-id="e2242-111">We can do things like leave required fields blank or type letters in the Price field, and the first error we'll see is from the database.</span></span>

<span data-ttu-id="e2242-112">我們可以藉由將資料批註加入至我們的模型類別，輕鬆地將驗證加入至應用程式。</span><span class="sxs-lookup"><span data-stu-id="e2242-112">We can easily add validation to our application by adding Data Annotations to our model classes.</span></span> <span data-ttu-id="e2242-113">資料批註可讓我們描述要套用至模型屬性的規則，而 ASP.NET MVC 會負責強制執行它們，並向使用者顯示適當的訊息。</span><span class="sxs-lookup"><span data-stu-id="e2242-113">Data Annotations allow us to describe the rules we want applied to our model properties, and ASP.NET MVC will take care of enforcing them and displaying appropriate messages to our users.</span></span>

## <a name="adding-validation-to-our-album-forms"></a><span data-ttu-id="e2242-114">將驗證新增至我們的專輯表單</span><span class="sxs-lookup"><span data-stu-id="e2242-114">Adding Validation to our Album Forms</span></span>

<span data-ttu-id="e2242-115">我們將使用下列資料批註屬性：</span><span class="sxs-lookup"><span data-stu-id="e2242-115">We'll use the following Data Annotation attributes:</span></span>

- <span data-ttu-id="e2242-116">**Required** –表示屬性為必要欄位</span><span class="sxs-lookup"><span data-stu-id="e2242-116">**Required** – Indicates that the property is a required field</span></span>
- <span data-ttu-id="e2242-117">**DisplayName** –定義我們想要用於表單欄位和驗證訊息的文字</span><span class="sxs-lookup"><span data-stu-id="e2242-117">**DisplayName** – Defines the text we want used on form fields and validation messages</span></span>
- <span data-ttu-id="e2242-118">**StringLength** –定義字串欄位的最大長度</span><span class="sxs-lookup"><span data-stu-id="e2242-118">**StringLength** – Defines a maximum length for a string field</span></span>
- <span data-ttu-id="e2242-119">**範圍**–提供數值欄位的最大和最小值</span><span class="sxs-lookup"><span data-stu-id="e2242-119">**Range** – Gives a maximum and minimum value for a numeric field</span></span>
- <span data-ttu-id="e2242-120">**Bind** –在將參數或表單值系結至模型屬性時，列出要排除或包含的欄位</span><span class="sxs-lookup"><span data-stu-id="e2242-120">**Bind** – Lists fields to exclude or include when binding parameter or form values to model properties</span></span>
- <span data-ttu-id="e2242-121">**ScaffoldColumn** –允許隱藏編輯表單中的欄位</span><span class="sxs-lookup"><span data-stu-id="e2242-121">**ScaffoldColumn** – Allows hiding fields from editor forms</span></span>

<span data-ttu-id="e2242-122">*注意：如需使用資料批註屬性進行模型驗證的詳細資訊，請參閱 MSDN 檔，網址*為[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span><span class="sxs-lookup"><span data-stu-id="e2242-122">*Note: For more information on Model Validation using Data Annotation attributes, see the MSDN documentation at*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span></span>

<span data-ttu-id="e2242-123">開啟專輯類別，並將下列*using*語句加入至頂端。</span><span class="sxs-lookup"><span data-stu-id="e2242-123">Open the Album class and add the following *using* statements to the top.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample1.cs)]

<span data-ttu-id="e2242-124">接下來，更新屬性以新增顯示和驗證屬性，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e2242-124">Next, update the properties to add display and validation attributes as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample2.cs)]

<span data-ttu-id="e2242-125">在這裡，我們也將內容類型和演出者變更為虛擬屬性。</span><span class="sxs-lookup"><span data-stu-id="e2242-125">While we're there, we've also changed the Genre and Artist to virtual properties.</span></span> <span data-ttu-id="e2242-126">這可讓 Entity Framework 視需要延遲載入它們。</span><span class="sxs-lookup"><span data-stu-id="e2242-126">This allows Entity Framework to lazy-load them as necessary.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample3.cs)]

<span data-ttu-id="e2242-127">將這些屬性新增至我們的專輯模型之後，我們的 [建立和編輯] 畫面會立即開始驗證欄位，並使用我們選擇的顯示名稱（例如專輯封面 Url，而不是 AlbumArtUrl）。</span><span class="sxs-lookup"><span data-stu-id="e2242-127">After having added these attributes to our Album model, our Create and Edit screen immediately begin validating fields and using the Display Names we've chosen (e.g. Album Art Url instead of AlbumArtUrl).</span></span> <span data-ttu-id="e2242-128">執行應用程式並流覽至/StoreManager/Create。</span><span class="sxs-lookup"><span data-stu-id="e2242-128">Run the application and browse to /StoreManager/Create.</span></span>

![](mvc-music-store-part-6/_static/image1.png)

<span data-ttu-id="e2242-129">接下來，我們會中斷部分驗證規則。</span><span class="sxs-lookup"><span data-stu-id="e2242-129">Next, we'll break some validation rules.</span></span> <span data-ttu-id="e2242-130">輸入0的價格，並將標題保留空白。</span><span class="sxs-lookup"><span data-stu-id="e2242-130">Enter a price of 0 and leave the Title blank.</span></span> <span data-ttu-id="e2242-131">當我們按一下 [建立] 按鈕時，我們會看到表單顯示，其中包含驗證錯誤訊息，顯示哪些欄位不符合我們所定義的驗證規則。</span><span class="sxs-lookup"><span data-stu-id="e2242-131">When we click on the Create button, we will see the form displayed with validation error messages showing which fields did not meet the validation rules we have defined.</span></span>

![](mvc-music-store-part-6/_static/image2.png)

## <a name="testing-the-client-side-validation"></a><span data-ttu-id="e2242-132">測試用戶端驗證</span><span class="sxs-lookup"><span data-stu-id="e2242-132">Testing the Client-Side Validation</span></span>

<span data-ttu-id="e2242-133">從應用程式的觀點來看，伺服器端驗證非常重要，因為使用者可以規避用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="e2242-133">Server-side validation is very important from an application perspective, because users can circumvent client-side validation.</span></span> <span data-ttu-id="e2242-134">不過，只會執行伺服器端驗證的網頁表單呈現了三個重要的問題。</span><span class="sxs-lookup"><span data-stu-id="e2242-134">However, webpage forms which only implement server-side validation exhibit three significant problems.</span></span>

1. <span data-ttu-id="e2242-135">使用者必須等待表單張貼、在伺服器上進行驗證，以及將回應傳送到其瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="e2242-135">The user has to wait for the form to be posted, validated on the server, and for the response to be sent to their browser.</span></span>
2. <span data-ttu-id="e2242-136">當使用者更正欄位，使其立即通過驗證規則時，不會立即收到意見反應。</span><span class="sxs-lookup"><span data-stu-id="e2242-136">The user doesn't get immediate feedback when they correct a field so that it now passes the validation rules.</span></span>
3. <span data-ttu-id="e2242-137">我們會浪費伺服器資源來執行驗證邏輯，而不是利用使用者的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="e2242-137">We are wasting server resources to perform validation logic instead of leveraging the user's browser.</span></span>

<span data-ttu-id="e2242-138">幸好，ASP.NET MVC 3 scaffold 範本已內建用戶端驗證，不需要任何額外的工作。</span><span class="sxs-lookup"><span data-stu-id="e2242-138">Fortunately, the ASP.NET MVC 3 scaffold templates have client-side validation built in, requiring no additional work whatsoever.</span></span>

<span data-ttu-id="e2242-139">在 [標題] 欄位中輸入單一字母可滿足驗證需求，因此會立即移除驗證訊息。</span><span class="sxs-lookup"><span data-stu-id="e2242-139">Typing a single letter in the Title field satisfies the validation requirements, so the validation message is immediately removed.</span></span>

![](mvc-music-store-part-6/_static/image3.png)

> [!div class="step-by-step"]
> <span data-ttu-id="e2242-140">[上一頁](mvc-music-store-part-5.md)
> [下一頁](mvc-music-store-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="e2242-140">[Previous](mvc-music-store-part-5.md)
[Next](mvc-music-store-part-7.md)</span></span>
