---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
title: '反復專案 #6 –使用測試導向的開發（VB） |Microsoft Docs'
author: microsoft
description: 在此第六個反復專案中，我們會先撰寫單元測試，並針對單元測試撰寫程式碼，以將新功能加入至應用程式。 在此反復專案中,。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: e1fd226f-3f8e-4575-a179-5c75b240333d
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
msc.type: authoredcontent
ms.openlocfilehash: b166a1c6af29206d43558fa7de447c3f4da2ddfe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78608301"
---
# <a name="iteration-6--use-test-driven-development-vb"></a><span data-ttu-id="22411-104">反復專案 #6 –使用測試導向的開發（VB）</span><span class="sxs-lookup"><span data-stu-id="22411-104">Iteration #6 – Use test-driven development (VB)</span></span>

<span data-ttu-id="22411-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="22411-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="22411-106">下載程式代碼</span><span class="sxs-lookup"><span data-stu-id="22411-106">Download Code</span></span>](iteration-6-use-test-driven-development-vb/_static/contactmanager_6_vb1.zip)

> <span data-ttu-id="22411-107">在此第六個反復專案中，我們會先撰寫單元測試，並針對單元測試撰寫程式碼，以將新功能加入至應用程式。</span><span class="sxs-lookup"><span data-stu-id="22411-107">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="22411-108">在此反復專案中，我們會新增連絡人群組。</span><span class="sxs-lookup"><span data-stu-id="22411-108">In this iteration, we add contact groups.</span></span>

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="22411-109">建立連絡人管理 ASP.NET MVC 應用程式（VB）</span><span class="sxs-lookup"><span data-stu-id="22411-109">Building a Contact Management ASP.NET MVC Application (VB)</span></span>

<span data-ttu-id="22411-110">在這一系列的教學課程中，我們從一開始就建立了整個連絡人管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="22411-110">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="22411-111">連絡人管理員應用程式可讓您儲存連絡人資訊名稱、電話號碼和電子郵件地址，以取得人員清單。</span><span class="sxs-lookup"><span data-stu-id="22411-111">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="22411-112">我們會透過多個反復專案來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="22411-112">We build the application over multiple iterations.</span></span> <span data-ttu-id="22411-113">在每次反覆運算時，我們會逐漸改善應用程式。</span><span class="sxs-lookup"><span data-stu-id="22411-113">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="22411-114">這個多個反復專案方法的目標，是要讓您瞭解每項變更的原因。</span><span class="sxs-lookup"><span data-stu-id="22411-114">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="22411-115">反復專案 #1-建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="22411-115">Iteration #1 - Create the application.</span></span> <span data-ttu-id="22411-116">在第一個反復專案中，我們會以最簡單的方式建立連絡人管理員。</span><span class="sxs-lookup"><span data-stu-id="22411-116">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="22411-117">我們新增對基本資料庫作業的支援：建立、讀取、更新和刪除（CRUD）。</span><span class="sxs-lookup"><span data-stu-id="22411-117">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="22411-118">反復專案 #2-讓應用程式看起來不錯。</span><span class="sxs-lookup"><span data-stu-id="22411-118">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="22411-119">在此反復專案中，我們藉由修改預設的 ASP.NET MVC view 主版頁面和級聯樣式表，來改善應用程式的外觀。</span><span class="sxs-lookup"><span data-stu-id="22411-119">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="22411-120">反復專案 #3-新增表單驗證。</span><span class="sxs-lookup"><span data-stu-id="22411-120">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="22411-121">在第三個反復專案中，我們會新增基本表單驗證。</span><span class="sxs-lookup"><span data-stu-id="22411-121">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="22411-122">我們會防止人們提交表單，而不需要完成必要的表單欄位。</span><span class="sxs-lookup"><span data-stu-id="22411-122">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="22411-123">我們也會驗證電子郵件地址和電話號碼。</span><span class="sxs-lookup"><span data-stu-id="22411-123">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="22411-124">反復專案 #4-讓應用程式鬆散結合。</span><span class="sxs-lookup"><span data-stu-id="22411-124">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="22411-125">在這第四次的反復專案中，我們會利用數種軟體設計模式，讓您更輕鬆地維護和修改 Contact Manager 應用程式。</span><span class="sxs-lookup"><span data-stu-id="22411-125">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="22411-126">例如，我們會重構應用程式，以使用存放庫模式和相依性插入模式。</span><span class="sxs-lookup"><span data-stu-id="22411-126">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="22411-127">反復專案 #5-建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="22411-127">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="22411-128">在第五個反復專案中，我們會藉由新增單元測試，讓應用程式更容易維護和修改。</span><span class="sxs-lookup"><span data-stu-id="22411-128">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="22411-129">我們會模擬我們的資料模型類別，並為我們的控制器和驗證邏輯建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="22411-129">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="22411-130">反復專案 #6-使用以測試為導向的開發。</span><span class="sxs-lookup"><span data-stu-id="22411-130">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="22411-131">在此第六個反復專案中，我們會先撰寫單元測試，並針對單元測試撰寫程式碼，以將新功能加入至應用程式。</span><span class="sxs-lookup"><span data-stu-id="22411-131">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="22411-132">在此反復專案中，我們會新增連絡人群組。</span><span class="sxs-lookup"><span data-stu-id="22411-132">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="22411-133">反復專案 #7-新增 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="22411-133">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="22411-134">在第七次的反復專案中，我們藉由新增 Ajax 的支援來改善應用程式的回應性和效能。</span><span class="sxs-lookup"><span data-stu-id="22411-134">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="22411-135">這個反復專案</span><span class="sxs-lookup"><span data-stu-id="22411-135">This Iteration</span></span>

<span data-ttu-id="22411-136">在連絡人管理員應用程式的上一個反復專案中，我們建立了單元測試，以提供程式碼的安全網路。</span><span class="sxs-lookup"><span data-stu-id="22411-136">In the previous iteration of the Contact Manager application, we created unit tests to provide a safety net for our code.</span></span> <span data-ttu-id="22411-137">建立單元測試的動機是讓我們的程式碼更有彈性地進行變更。</span><span class="sxs-lookup"><span data-stu-id="22411-137">The motivation for creating the unit tests was to make our code more resilient to change.</span></span> <span data-ttu-id="22411-138">當單元測試就緒時，我們可以對程式碼進行任何變更，並立即知道我們是否已中斷現有的功能。</span><span class="sxs-lookup"><span data-stu-id="22411-138">With unit tests in place, we can happily make any change to our code and immediately know whether we have broken existing functionality.</span></span>

<span data-ttu-id="22411-139">在此反復專案中，我們將單元測試用於完全不同的用途。</span><span class="sxs-lookup"><span data-stu-id="22411-139">In this iteration, we use unit tests for an entirely different purpose.</span></span> <span data-ttu-id="22411-140">在此反復專案中，我們使用單元測試做為應用程式設計原理的一部分，稱為「*測試導向開發*」。</span><span class="sxs-lookup"><span data-stu-id="22411-140">In this iteration, we use unit tests as part of an application design philosophy called *test-driven development*.</span></span> <span data-ttu-id="22411-141">當您練習以測試為導向的開發時，您會先撰寫測試，然後針對測試撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="22411-141">When you practice test-driven development, you write tests first and then write code against the tests.</span></span>

<span data-ttu-id="22411-142">更精確地說，在練習以測試為導向的開發時，您可以在建立程式碼時完成三個步驟（紅色/綠色/重構）：</span><span class="sxs-lookup"><span data-stu-id="22411-142">More precisely, when practicing test-driven development, there are three steps that you complete when creating code (Red/ Green/Refactor):</span></span>

1. <span data-ttu-id="22411-143">撰寫失敗的單元測試（紅色）</span><span class="sxs-lookup"><span data-stu-id="22411-143">Write a unit test that fails (Red)</span></span>
2. <span data-ttu-id="22411-144">撰寫通過單元測試的程式碼（綠色）</span><span class="sxs-lookup"><span data-stu-id="22411-144">Write code that passes the unit test (Green)</span></span>
3. <span data-ttu-id="22411-145">重構您的程式碼（重構）</span><span class="sxs-lookup"><span data-stu-id="22411-145">Refactor your code (Refactor)</span></span>

<span data-ttu-id="22411-146">首先，您要撰寫單元測試。</span><span class="sxs-lookup"><span data-stu-id="22411-146">First, you write the unit test.</span></span> <span data-ttu-id="22411-147">單元測試應該表示您希望程式程式碼為的意圖。</span><span class="sxs-lookup"><span data-stu-id="22411-147">The unit test should express your intention for how you expect your code to behave.</span></span> <span data-ttu-id="22411-148">當您第一次建立單元測試時，單元測試應該會失敗。</span><span class="sxs-lookup"><span data-stu-id="22411-148">When you first create the unit test, the unit test should fail.</span></span> <span data-ttu-id="22411-149">測試應該會失敗，因為您尚未撰寫任何符合測試的應用程式代碼。</span><span class="sxs-lookup"><span data-stu-id="22411-149">The test should fail because you have not yet written any application code that satisfies the test.</span></span>

<span data-ttu-id="22411-150">接下來，您只需要撰寫足夠的程式碼，單元測試才會通過。</span><span class="sxs-lookup"><span data-stu-id="22411-150">Next, you write just enough code in order for the unit test to pass.</span></span> <span data-ttu-id="22411-151">其目標是以 laziest、sloppiest 和最快速的可能方式撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="22411-151">The goal is to write the code in the laziest, sloppiest and fastest possible way.</span></span> <span data-ttu-id="22411-152">您不應該浪費時間思考應用程式的架構。</span><span class="sxs-lookup"><span data-stu-id="22411-152">You should not waste time thinking about the architecture of your application.</span></span> <span data-ttu-id="22411-153">相反地，您應該專注于撰寫必要的最低程式碼數量，以滿足單元測試所表示的意圖。</span><span class="sxs-lookup"><span data-stu-id="22411-153">Instead, you should focus on writing the minimal amount of code necessary to satisfy the intention expressed by the unit test.</span></span>

<span data-ttu-id="22411-154">最後，在撰寫足夠的程式碼之後，您就可以回溯，並考慮應用程式的整體架構。</span><span class="sxs-lookup"><span data-stu-id="22411-154">Finally, after you have written enough code, you can step back and consider the overall architecture of your application.</span></span> <span data-ttu-id="22411-155">在此步驟中，您會利用軟體設計模式（例如存放庫模式）來重寫（重構）程式碼，讓您的程式碼更容易維護。</span><span class="sxs-lookup"><span data-stu-id="22411-155">In this step, you rewrite (refactor) your code by taking advantage of software design patterns -- such as the repository pattern -- so that your code is more maintainable.</span></span> <span data-ttu-id="22411-156">在此步驟中，您可以 fearlessly 重寫程式碼，因為單元測試涵蓋了您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="22411-156">You can fearlessly rewrite your code in this step because your code is covered by unit tests.</span></span>

<span data-ttu-id="22411-157">測試導向的開發會產生許多好處。</span><span class="sxs-lookup"><span data-stu-id="22411-157">There are many benefits that result from practicing test-driven development.</span></span> <span data-ttu-id="22411-158">首先，以測試為導向的開發會強制您將焦點放在實際需要撰寫的程式碼上。</span><span class="sxs-lookup"><span data-stu-id="22411-158">First, test-driven development forces you to focus on code that actually needs to be written.</span></span> <span data-ttu-id="22411-159">因為您經常專注于撰寫足夠的程式碼來通過特定測試，所以您無法晃至直搗黃龍，並撰寫您永遠不會使用的大量程式碼。</span><span class="sxs-lookup"><span data-stu-id="22411-159">Because you are constantly focused on just writing enough code to pass a particular test, you are prevented from wandering into the weeds and writing massive amounts of code that you will never use.</span></span>

<span data-ttu-id="22411-160">第二種是「測試優先」設計方法，會強制您從程式碼的使用方式來撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="22411-160">Second, a "test first" design methodology forces you to write code from the perspective of how your code will be used.</span></span> <span data-ttu-id="22411-161">換句話說，在練習以測試為導向的開發時，您會經常從使用者的觀點來撰寫您的測試。</span><span class="sxs-lookup"><span data-stu-id="22411-161">In other words, when practicing test-driven development, you are constantly writing your tests from a user perspective.</span></span> <span data-ttu-id="22411-162">因此，以測試為導向的開發可能會產生更清楚且更容易理解的 Api。</span><span class="sxs-lookup"><span data-stu-id="22411-162">Therefore, test-driven development can result in cleaner and more understandable APIs.</span></span>

<span data-ttu-id="22411-163">最後，以測試為導向的開發會強制您撰寫單元測試，做為撰寫應用程式的一般進程的一部分。</span><span class="sxs-lookup"><span data-stu-id="22411-163">Finally, test-driven development forces you to write unit tests as part of the normal process of writing an application.</span></span> <span data-ttu-id="22411-164">作為專案期限的方法，測試通常是進入視窗的第一件事。</span><span class="sxs-lookup"><span data-stu-id="22411-164">As a project deadline approaches, testing is typically the first thing that goes out the window.</span></span> <span data-ttu-id="22411-165">另一方面，當您練習以測試為導向的開發時，您更有可能會良性撰寫單元測試，因為測試導向的開發會使單元測試成為建立應用程式的過程。</span><span class="sxs-lookup"><span data-stu-id="22411-165">When practicing test-driven development, on the other hand, you are more likely to be virtuous about writing unit tests because test-driven development makes unit tests central to the process of building an application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="22411-166">若要深入瞭解以測試為導向的開發，建議您閱讀 Michael Feathers 書籍**有效率地使用舊版程式碼**。</span><span class="sxs-lookup"><span data-stu-id="22411-166">To learn more about test-driven development, I recommend that you read Michael Feathers book **Working Effectively with Legacy Code**.</span></span>

<span data-ttu-id="22411-167">在此反復專案中，我們會將新功能新增至我們的 Contact Manager 應用程式。</span><span class="sxs-lookup"><span data-stu-id="22411-167">In this iteration, we add a new feature to our Contact Manager application.</span></span> <span data-ttu-id="22411-168">我們新增了對連絡人群組的支援。</span><span class="sxs-lookup"><span data-stu-id="22411-168">We add support for Contact Groups.</span></span> <span data-ttu-id="22411-169">您可以使用連絡人群組，將連絡人組織成像是商務和 Friend 群組的類別。</span><span class="sxs-lookup"><span data-stu-id="22411-169">You can use Contact Groups to organize your contacts into categories such as Business and Friend groups.</span></span>

<span data-ttu-id="22411-170">我們會遵循測試導向開發的程式，將這項新功能新增至我們的應用程式。</span><span class="sxs-lookup"><span data-stu-id="22411-170">We'll add this new functionality to our application by following a process of test-driven development.</span></span> <span data-ttu-id="22411-171">我們會先撰寫單元測試，我們會針對這些測試撰寫所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="22411-171">We'll write our unit tests first and we'll write all of our code against these tests.</span></span>

## <a name="what-gets-tested"></a><span data-ttu-id="22411-172">已測試的內容</span><span class="sxs-lookup"><span data-stu-id="22411-172">What Gets Tested</span></span>

<span data-ttu-id="22411-173">如先前的反復專案中所討論，您通常不會針對資料存取邏輯或 view 邏輯撰寫單元測試。</span><span class="sxs-lookup"><span data-stu-id="22411-173">As we discussed in the previous iteration, you typically do not write unit tests for data access logic or view logic.</span></span> <span data-ttu-id="22411-174">您不會撰寫資料存取邏輯的單元測試，因為存取資料庫是相當緩慢的作業。</span><span class="sxs-lookup"><span data-stu-id="22411-174">You don t write unit tests for data access logic because accessing a database is a relatively slow operation.</span></span> <span data-ttu-id="22411-175">您不會針對 view 邏輯撰寫單元測試，因為存取視圖需要加速 web 伺服器，這是相當緩慢的作業。</span><span class="sxs-lookup"><span data-stu-id="22411-175">You don t write unit tests for view logic because accessing a view requires spinning up a web server which is a relatively slow operation.</span></span> <span data-ttu-id="22411-176">除非測試可以非常快速地執行，否則您不應該撰寫單元測試</span><span class="sxs-lookup"><span data-stu-id="22411-176">You shouldn't write a unit test unless the test can be executed over and over again very fast</span></span>

<span data-ttu-id="22411-177">因為測試導向的開發是由單元測試所驅動，所以我們一開始會專注于撰寫控制器和商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="22411-177">Because test-driven development is driven by unit tests, we focus initially on writing controller and business logic.</span></span> <span data-ttu-id="22411-178">我們避免觸及資料庫或 views。</span><span class="sxs-lookup"><span data-stu-id="22411-178">We avoid touching the database or views.</span></span> <span data-ttu-id="22411-179">我們不會修改資料庫或建立我們的視圖，直到本教學課程的結尾。</span><span class="sxs-lookup"><span data-stu-id="22411-179">We won't modify the database or create our views until the very end of this tutorial.</span></span> <span data-ttu-id="22411-180">我們先從可測試的內容著手。</span><span class="sxs-lookup"><span data-stu-id="22411-180">We start with what can be tested.</span></span>

## <a name="creating-user-stories"></a><span data-ttu-id="22411-181">建立使用者故事</span><span class="sxs-lookup"><span data-stu-id="22411-181">Creating User Stories</span></span>

<span data-ttu-id="22411-182">在練習以測試為導向的開發時，您一律會開始撰寫測試。</span><span class="sxs-lookup"><span data-stu-id="22411-182">When practicing test-driven development, you always start by writing a test.</span></span> <span data-ttu-id="22411-183">這會立即引發問題：您要如何決定要先撰寫哪一種測試？</span><span class="sxs-lookup"><span data-stu-id="22411-183">This immediately raises the question: How do you decide what test to write first?</span></span> <span data-ttu-id="22411-184">若要回答這個問題，您應該撰寫一組[*使用者故事*](http://en.wikipedia.org/wiki/User_stories)。</span><span class="sxs-lookup"><span data-stu-id="22411-184">To answer this question, you should write a set of [*user stories*](http://en.wikipedia.org/wiki/User_stories).</span></span>

<span data-ttu-id="22411-185">使用者故事是軟體需求的簡要說明（通常是一句）。</span><span class="sxs-lookup"><span data-stu-id="22411-185">A user story is a very brief (usually one sentence) description of a software requirement.</span></span> <span data-ttu-id="22411-186">它應該是從使用者觀點撰寫之需求的非技術性說明。</span><span class="sxs-lookup"><span data-stu-id="22411-186">It should be a non-technical description of a requirement written from a user perspective.</span></span>

<span data-ttu-id="22411-187">以下是描述新連絡人群組功能所需功能的一組使用者故事：</span><span class="sxs-lookup"><span data-stu-id="22411-187">Here s the set of user stories that describe the features required by the new Contact Group functionality:</span></span>

1. <span data-ttu-id="22411-188">使用者可以查看連絡人群組的清單。</span><span class="sxs-lookup"><span data-stu-id="22411-188">User can view a list of contact groups.</span></span>
2. <span data-ttu-id="22411-189">使用者可以建立新的連絡人群組。</span><span class="sxs-lookup"><span data-stu-id="22411-189">User can create a new contact group.</span></span>
3. <span data-ttu-id="22411-190">使用者可以刪除現有的連絡人群組。</span><span class="sxs-lookup"><span data-stu-id="22411-190">User can delete an existing contact group.</span></span>
4. <span data-ttu-id="22411-191">使用者可以在建立新的連絡人時選取連絡人群組。</span><span class="sxs-lookup"><span data-stu-id="22411-191">User can select a contact group when creating a new contact.</span></span>
5. <span data-ttu-id="22411-192">編輯現有的連絡人時，使用者可以選取連絡人群組。</span><span class="sxs-lookup"><span data-stu-id="22411-192">User can select a contact group when editing an existing contact.</span></span>
6. <span data-ttu-id="22411-193">連絡人群組清單會顯示在 [索引] 視圖中。</span><span class="sxs-lookup"><span data-stu-id="22411-193">A list of contact groups is displayed in the Index view.</span></span>
7. <span data-ttu-id="22411-194">當使用者按一下連絡人群組時，會顯示相符連絡人的清單。</span><span class="sxs-lookup"><span data-stu-id="22411-194">When a user clicks a contact group, a list of matching contacts is displayed.</span></span>

<span data-ttu-id="22411-195">請注意，客戶可以完全瞭解這份使用者故事清單。</span><span class="sxs-lookup"><span data-stu-id="22411-195">Notice that this list of user stories is completely understandable by a customer.</span></span> <span data-ttu-id="22411-196">不會提及技術的執行詳細資料。</span><span class="sxs-lookup"><span data-stu-id="22411-196">There is no mention of technical implementation details.</span></span>

<span data-ttu-id="22411-197">在建立應用程式的過程中，一組使用者故事可能會變得更加精簡。</span><span class="sxs-lookup"><span data-stu-id="22411-197">While in the process of building your application, the set of user stories can become more refined.</span></span> <span data-ttu-id="22411-198">您可能會將使用者故事細分為多個案例（需求）。</span><span class="sxs-lookup"><span data-stu-id="22411-198">You might break a user story into multiple stories (requirements).</span></span> <span data-ttu-id="22411-199">例如，您可能會決定建立新的連絡人群組應該包含驗證。</span><span class="sxs-lookup"><span data-stu-id="22411-199">For example, you might decide that creating a new contact group should involve validation.</span></span> <span data-ttu-id="22411-200">提交沒有名稱的連絡人群組時，應該會傳回驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="22411-200">Submitting a contact group without a name should return a validation error.</span></span>

<span data-ttu-id="22411-201">建立使用者故事清單之後，您就可以開始撰寫第一個單元測試。</span><span class="sxs-lookup"><span data-stu-id="22411-201">After you create a list of user stories, you are ready to write your first unit test.</span></span> <span data-ttu-id="22411-202">首先，我們會建立單元測試來查看連絡人群組的清單。</span><span class="sxs-lookup"><span data-stu-id="22411-202">We'll start by creating a unit test for viewing the list of contact groups.</span></span>

## <a name="listing-contact-groups"></a><span data-ttu-id="22411-203">列出連絡人群組</span><span class="sxs-lookup"><span data-stu-id="22411-203">Listing Contact Groups</span></span>

<span data-ttu-id="22411-204">我們的第一個使用者案例是，使用者應該能夠查看連絡人群組的清單。</span><span class="sxs-lookup"><span data-stu-id="22411-204">Our first user story is that a user should be able to view a list of contact groups.</span></span> <span data-ttu-id="22411-205">我們需要使用測試來表達這篇故事。</span><span class="sxs-lookup"><span data-stu-id="22411-205">We need to express this story with a test.</span></span>

<span data-ttu-id="22411-206">以滑鼠右鍵按一下 [ContactManager] 專案中的 [控制器] 資料夾，選取 [**加入]、[新增測試**]，然後選取 [**單元測試**] 範本（請參閱 [圖 1]），以建立新的單元測試。</span><span class="sxs-lookup"><span data-stu-id="22411-206">Create a new unit test by right-clicking the Controllers folder in the ContactManager.Tests project, selecting **Add, New Test**, and selecting the **Unit Test** template (see Figure 1).</span></span> <span data-ttu-id="22411-207">將新的單元測試命名為 GroupControllerTest，然後按一下 [**確定]** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="22411-207">Name the new unit test GroupControllerTest.vb and click the **OK** button.</span></span>

<span data-ttu-id="22411-208">[![新增 GroupControllerTest 單元測試](iteration-6-use-test-driven-development-vb/_static/image1.jpg)](iteration-6-use-test-driven-development-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="22411-208">[![Adding the GroupControllerTest unit test](iteration-6-use-test-driven-development-vb/_static/image1.jpg)](iteration-6-use-test-driven-development-vb/_static/image1.png)</span></span>

<span data-ttu-id="22411-209">**圖 01**：新增 GroupControllerTest 單元測試（[按一下以觀看完整大小的影像](iteration-6-use-test-driven-development-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="22411-209">**Figure 01**: Adding the GroupControllerTest unit test([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image2.png))</span></span>

<span data-ttu-id="22411-210">第一個單元測試包含在 [清單 1] 中。</span><span class="sxs-lookup"><span data-stu-id="22411-210">Our first unit test is contained in Listing 1.</span></span> <span data-ttu-id="22411-211">這項測試會確認群組控制器的 Index （）方法會傳回一組群組。</span><span class="sxs-lookup"><span data-stu-id="22411-211">This test verifies that the Index() method of the Group controller returns a set of Groups.</span></span> <span data-ttu-id="22411-212">此測試會確認群組的集合是否會在 view data 中傳回。</span><span class="sxs-lookup"><span data-stu-id="22411-212">The test verifies that a collection of Groups is returned in view data.</span></span>

<span data-ttu-id="22411-213">**清單 1-Controllers\GroupControllerTest.vb**</span><span class="sxs-lookup"><span data-stu-id="22411-213">**Listing 1 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample1.vb)]

<span data-ttu-id="22411-214">當您第一次在 Visual Studio 的 [清單 1] 中輸入程式碼時，您將會得到許多紅色的波浪線。</span><span class="sxs-lookup"><span data-stu-id="22411-214">When you first type the code in Listing 1 in Visual Studio, you'll get a lot of red squiggly lines.</span></span> <span data-ttu-id="22411-215">我們尚未建立 GroupController 或 Group 類別。</span><span class="sxs-lookup"><span data-stu-id="22411-215">We have not created the GroupController or Group classes.</span></span>

<span data-ttu-id="22411-216">此時，我們甚至不能建立我們的應用程式，因此無法執行第一次單元測試。</span><span class="sxs-lookup"><span data-stu-id="22411-216">At this point, we can t even build our application so we can t execute our first unit test.</span></span> <span data-ttu-id="22411-217">好了。</span><span class="sxs-lookup"><span data-stu-id="22411-217">That s good.</span></span> <span data-ttu-id="22411-218">這會計算為失敗的測試。</span><span class="sxs-lookup"><span data-stu-id="22411-218">That counts as a failing test.</span></span> <span data-ttu-id="22411-219">因此，我們現在擁有開始撰寫應用程式程式碼的許可權。</span><span class="sxs-lookup"><span data-stu-id="22411-219">Therefore, we now have permission to start writing application code.</span></span> <span data-ttu-id="22411-220">我們需要撰寫足夠的程式碼來執行我們的測試。</span><span class="sxs-lookup"><span data-stu-id="22411-220">We need to write enough code to execute our test.</span></span>

<span data-ttu-id="22411-221">[清單 2] 中的群組控制器類別包含傳遞單元測試所需的最少程式碼。</span><span class="sxs-lookup"><span data-stu-id="22411-221">The Group controller class in Listing 2 contains the bare minimum of code required to pass the unit test.</span></span> <span data-ttu-id="22411-222">Index （）動作會傳回群組的靜態編碼清單（Group 類別定義于 [清單 3] 中）。</span><span class="sxs-lookup"><span data-stu-id="22411-222">The Index() action returns a statically coded list of Groups (the Group class is defined in Listing 3).</span></span>

<span data-ttu-id="22411-223">**清單 2-Controllers\GroupController.vb**</span><span class="sxs-lookup"><span data-stu-id="22411-223">**Listing 2 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample2.vb)]

<span data-ttu-id="22411-224">**清單 3-Models\Group.vb**</span><span class="sxs-lookup"><span data-stu-id="22411-224">**Listing 3 - Models\Group.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample3.vb)]

<span data-ttu-id="22411-225">將 GroupController 和群組類別加入至專案之後，我們的第一個單元測試就會成功完成（請參閱 [圖 2]）。</span><span class="sxs-lookup"><span data-stu-id="22411-225">After we add the GroupController and Group classes to our project, our first unit test completes successfully (see Figure 2).</span></span> <span data-ttu-id="22411-226">我們已完成通過測試所需的最少工作。</span><span class="sxs-lookup"><span data-stu-id="22411-226">We have done the minimum work required to pass the test.</span></span> <span data-ttu-id="22411-227">這是一種慶祝的時機。</span><span class="sxs-lookup"><span data-stu-id="22411-227">It is time to celebrate.</span></span>

<span data-ttu-id="22411-228">[![成功！](iteration-6-use-test-driven-development-vb/_static/image2.jpg)](iteration-6-use-test-driven-development-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="22411-228">[![Success!](iteration-6-use-test-driven-development-vb/_static/image2.jpg)](iteration-6-use-test-driven-development-vb/_static/image3.png)</span></span>

<span data-ttu-id="22411-229">**圖 02**：成功！（[按一下以查看完整大小的影像](iteration-6-use-test-driven-development-vb/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="22411-229">**Figure 02**: Success!([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image4.png))</span></span>

## <a name="creating-contact-groups"></a><span data-ttu-id="22411-230">建立連絡人群組</span><span class="sxs-lookup"><span data-stu-id="22411-230">Creating Contact Groups</span></span>

<span data-ttu-id="22411-231">現在我們可以繼續第二個使用者案例。</span><span class="sxs-lookup"><span data-stu-id="22411-231">Now we can move on to the second user story.</span></span> <span data-ttu-id="22411-232">我們必須能夠建立新的連絡人群組。</span><span class="sxs-lookup"><span data-stu-id="22411-232">We need to be able to create new contact groups.</span></span> <span data-ttu-id="22411-233">我們需要透過測試來表達這種意圖。</span><span class="sxs-lookup"><span data-stu-id="22411-233">We need to express this intention with a test.</span></span>

<span data-ttu-id="22411-234">[清單 4] 中的測試會確認以新群組呼叫 Create （）方法時，會將該群組新增至 Index （）方法所傳回的群組清單中。</span><span class="sxs-lookup"><span data-stu-id="22411-234">The test in Listing 4 verifies that calling the Create() method with a new Group adds the Group to the list of Groups returned by the Index() method.</span></span> <span data-ttu-id="22411-235">換句話說，如果我建立新的群組，則應該能夠從 Index （）方法傳回的群組清單中取得新的群組。</span><span class="sxs-lookup"><span data-stu-id="22411-235">In other words, if I create a new group then I should be able to get the new Group back from the list of Groups returned by the Index() method.</span></span>

<span data-ttu-id="22411-236">**清單 4-Controllers\GroupControllerTest.vb**</span><span class="sxs-lookup"><span data-stu-id="22411-236">**Listing 4 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample4.vb)]

<span data-ttu-id="22411-237">[清單 4] 中的測試會以新的連絡人群組呼叫群組控制器 Create （）方法。</span><span class="sxs-lookup"><span data-stu-id="22411-237">The test in Listing 4 calls the Group controller Create() method with a new contact Group.</span></span> <span data-ttu-id="22411-238">接下來，測試會確認呼叫群組控制器 Index （）方法會傳回 view data 中的新群組。</span><span class="sxs-lookup"><span data-stu-id="22411-238">Next, the test verifies that calling the Group controller Index() method returns the new Group in view data.</span></span>

<span data-ttu-id="22411-239">[清單 5] 中已修改的群組控制器包含傳遞新測試所需的最少變更。</span><span class="sxs-lookup"><span data-stu-id="22411-239">The modified Group controller in Listing 5 contains the bare minimum of changes required to pass the new test.</span></span>

<span data-ttu-id="22411-240">**清單 5-Controllers\GroupController.vb**</span><span class="sxs-lookup"><span data-stu-id="22411-240">**Listing 5 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample5.vb)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a><span data-ttu-id="22411-241">[清單 5] 中的群組控制器有新的 Create （）動作。</span><span class="sxs-lookup"><span data-stu-id="22411-241">The Group controller in Listing 5 has a new Create() action.</span></span> <span data-ttu-id="22411-242">此動作會將群組新增至群組集合。</span><span class="sxs-lookup"><span data-stu-id="22411-242">This action adds a Group to a collection of Groups.</span></span> <span data-ttu-id="22411-243">請注意，索引（）動作已經過修改，可傳回群組集合的內容。</span><span class="sxs-lookup"><span data-stu-id="22411-243">Notice that the Index() action has been modified to return the contents of the collection of Groups.</span></span>

<span data-ttu-id="22411-244">同樣地，我們已執行傳遞單元測試所需的最低工作量。</span><span class="sxs-lookup"><span data-stu-id="22411-244">Once again, we have performed the bare minimum amount of work required to pass the unit test.</span></span> <span data-ttu-id="22411-245">在對群組控制器進行這些變更之後，我們所有的單元測試都會通過。</span><span class="sxs-lookup"><span data-stu-id="22411-245">After we make these changes to the Group controller, all of our unit tests pass.</span></span>

## <a name="adding-validation"></a><span data-ttu-id="22411-246">新增驗證</span><span class="sxs-lookup"><span data-stu-id="22411-246">Adding Validation</span></span>

<span data-ttu-id="22411-247">這項需求並未在使用者案例中明確陳述。</span><span class="sxs-lookup"><span data-stu-id="22411-247">This requirement was not stated explicitly in the user story.</span></span> <span data-ttu-id="22411-248">不過，需要群組具有名稱是合理的。</span><span class="sxs-lookup"><span data-stu-id="22411-248">However, it is reasonable to require that a Group have a name.</span></span> <span data-ttu-id="22411-249">否則，將連絡人組織成群組並不會非常有用。</span><span class="sxs-lookup"><span data-stu-id="22411-249">Otherwise, organizing contacts into Groups would not be very useful.</span></span>

<span data-ttu-id="22411-250">[清單 6] 包含表示此意圖的新測試。</span><span class="sxs-lookup"><span data-stu-id="22411-250">Listing 6 contains a new test that expresses this intention.</span></span> <span data-ttu-id="22411-251">這項測試會確認嘗試在未提供名稱的情況下建立群組，會導致模型狀態中的驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="22411-251">This test verifies that attempting to create a Group without supplying a name results in a validation error message in model state.</span></span>

<span data-ttu-id="22411-252">**清單 6-Controllers\GroupControllerTest.vb**</span><span class="sxs-lookup"><span data-stu-id="22411-252">**Listing 6 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample6.vb)]

<span data-ttu-id="22411-253">為了滿足這項測試的需求，我們必須將 Name 屬性新增至我們的 Group 類別（請參閱 [清單 7]）。</span><span class="sxs-lookup"><span data-stu-id="22411-253">In order to satisfy this test, we need to add a Name property to our Group class (see Listing 7).</span></span> <span data-ttu-id="22411-254">此外，我們還需要在群組控制器的 Create （）動作（請參閱 [清單 8]）中新增一個小的驗證邏輯。</span><span class="sxs-lookup"><span data-stu-id="22411-254">Furthermore, we need to add a tiny bit of validation logic to our Group controller s Create() action (see Listing 8).</span></span>

<span data-ttu-id="22411-255">**清單 7-Models\Group.vb**</span><span class="sxs-lookup"><span data-stu-id="22411-255">**Listing 7 - Models\Group.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample7.vb)]

<span data-ttu-id="22411-256">**清單 8-Controllers\GroupController.vb**</span><span class="sxs-lookup"><span data-stu-id="22411-256">**Listing 8 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample8.vb)]

<span data-ttu-id="22411-257">請注意，[群組控制器建立] （）動作現在同時包含驗證和資料庫邏輯。</span><span class="sxs-lookup"><span data-stu-id="22411-257">Notice that the Group controller Create() action now contains both validation and database logic.</span></span> <span data-ttu-id="22411-258">目前，群組控制器所使用的資料庫只包含記憶體中的集合。</span><span class="sxs-lookup"><span data-stu-id="22411-258">Currently, the database used by the Group controller consists of nothing more than an in-memory collection.</span></span>

## <a name="time-to-refactor"></a><span data-ttu-id="22411-259">重構的時間</span><span class="sxs-lookup"><span data-stu-id="22411-259">Time to Refactor</span></span>

<span data-ttu-id="22411-260">紅色/綠色/重構中的第三個步驟是重構元件。</span><span class="sxs-lookup"><span data-stu-id="22411-260">The third step in Red/Green/Refactor is the Refactor part.</span></span> <span data-ttu-id="22411-261">此時，我們需要從程式碼回頭執行，並考慮如何重構我們的應用程式來改善其設計。</span><span class="sxs-lookup"><span data-stu-id="22411-261">At this point, we need to step back from our code and consider how we can refactor our application to improve its design.</span></span> <span data-ttu-id="22411-262">[重構] 階段是我們認為難以實現軟體設計原則和模式的最佳方式。</span><span class="sxs-lookup"><span data-stu-id="22411-262">The Refactor stage is the stage at which we think hard about the best way of implementing software design principles and patterns.</span></span>

<span data-ttu-id="22411-263">我們可以自由修改程式碼，讓我們選擇改善程式碼的設計。</span><span class="sxs-lookup"><span data-stu-id="22411-263">We are free to modify our code in any way that we choose to improve the design of the code.</span></span> <span data-ttu-id="22411-264">我們有單元測試的安全網路，可防止我們中斷現有的功能。</span><span class="sxs-lookup"><span data-stu-id="22411-264">We have a safety net of unit tests that prevent us from breaking existing functionality.</span></span>

<span data-ttu-id="22411-265">現在，我們的群組控制器從良好的軟體設計觀點來看，是一件令人搞不好的。</span><span class="sxs-lookup"><span data-stu-id="22411-265">Right now, our Group controller is a mess from the perspective of good software design.</span></span> <span data-ttu-id="22411-266">群組控制器包含紊亂的驗證和資料存取程式碼。</span><span class="sxs-lookup"><span data-stu-id="22411-266">The Group controller contains a tangled mess of validation and data access code.</span></span> <span data-ttu-id="22411-267">為了避免違反單一責任原則，我們需要將這些考慮區分為不同的類別。</span><span class="sxs-lookup"><span data-stu-id="22411-267">To avoid violating the Single Responsibility Principle, we need to separate these concerns into different classes.</span></span>

<span data-ttu-id="22411-268">[清單 9] 中包含我們重構的群組控制器類別。</span><span class="sxs-lookup"><span data-stu-id="22411-268">Our refactored Group controller class is contained in Listing 9.</span></span> <span data-ttu-id="22411-269">控制器已修改為使用 ContactManager 服務層。</span><span class="sxs-lookup"><span data-stu-id="22411-269">The controller has been modified to use the ContactManager service layer.</span></span> <span data-ttu-id="22411-270">這是與連絡人控制器搭配使用的相同服務層。</span><span class="sxs-lookup"><span data-stu-id="22411-270">This is the same service layer that we use with the Contact controller.</span></span>

<span data-ttu-id="22411-271">[清單 10] 包含新增至 ContactManager 服務層的方法，以支援驗證、列出及建立群組。</span><span class="sxs-lookup"><span data-stu-id="22411-271">Listing 10 contains the new methods added to the ContactManager service layer to support validating, listing, and creating groups.</span></span> <span data-ttu-id="22411-272">IContactManagerService 介面已更新為包含新的方法。</span><span class="sxs-lookup"><span data-stu-id="22411-272">The IContactManagerService interface was updated to include the new methods.</span></span>

<span data-ttu-id="22411-273">[清單 11] 包含可執行 IContactManagerRepository 介面的新 FakeContactManagerRepository 類別。</span><span class="sxs-lookup"><span data-stu-id="22411-273">Listing 11 contains a new FakeContactManagerRepository class that implements the IContactManagerRepository interface.</span></span> <span data-ttu-id="22411-274">不同于也會執行 IContactManagerRepository 介面的 EntityContactManagerRepository 類別，我們的新 FakeContactManagerRepository 類別不會與資料庫通訊。</span><span class="sxs-lookup"><span data-stu-id="22411-274">Unlike the EntityContactManagerRepository class that also implements the IContactManagerRepository interface, our new FakeContactManagerRepository class does not communicate with the database.</span></span> <span data-ttu-id="22411-275">FakeContactManagerRepository 類別會使用記憶體內部集合做為資料庫的 proxy。</span><span class="sxs-lookup"><span data-stu-id="22411-275">The FakeContactManagerRepository class uses an in-memory collection as a proxy for the database.</span></span> <span data-ttu-id="22411-276">我們會在單元測試中使用此類別做為假的儲存機制層。</span><span class="sxs-lookup"><span data-stu-id="22411-276">We'll use this class in our unit tests as a fake repository layer.</span></span>

<span data-ttu-id="22411-277">**清單 9-Controllers\GroupController.vb**</span><span class="sxs-lookup"><span data-stu-id="22411-277">**Listing 9 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample9.vb)]

<span data-ttu-id="22411-278">**清單 10-Controllers\ContactManagerService.vb**</span><span class="sxs-lookup"><span data-stu-id="22411-278">**Listing 10 - Controllers\ContactManagerService.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample10.vb)]

<span data-ttu-id="22411-279">**清單 11-Controllers\FakeContactManagerRepository.vb**</span><span class="sxs-lookup"><span data-stu-id="22411-279">**Listing 11 - Controllers\FakeContactManagerRepository.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample11.vb)]

<span data-ttu-id="22411-280">修改 IContactManagerRepository 介面需要使用來執行 EntityContactManagerRepository 類別中的 CreateGroup （）和 ListGroups （）方法。</span><span class="sxs-lookup"><span data-stu-id="22411-280">Modifying the IContactManagerRepository interface requires use to implement the CreateGroup() and ListGroups() methods in the EntityContactManagerRepository class.</span></span> <span data-ttu-id="22411-281">執行此動作的 laziest 和最快速方式是新增如下所示的 stub 方法：</span><span class="sxs-lookup"><span data-stu-id="22411-281">The laziest and fastest way to do this is to add stub methods that look like this:</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample12.vb)]

<span data-ttu-id="22411-282">最後，應用程式設計的這些變更需要我們對單元測試進行一些修改。</span><span class="sxs-lookup"><span data-stu-id="22411-282">Finally, these changes to the design of our application require us to make some modifications to our unit tests.</span></span> <span data-ttu-id="22411-283">在執行單元測試時，我們現在需要使用 FakeContactManagerRepository。</span><span class="sxs-lookup"><span data-stu-id="22411-283">We now need to use the FakeContactManagerRepository when performing the unit tests.</span></span> <span data-ttu-id="22411-284">更新後的 GroupControllerTest 類別包含在 [清單 12] 中。</span><span class="sxs-lookup"><span data-stu-id="22411-284">The updated GroupControllerTest class is contained in Listing 12.</span></span>

<span data-ttu-id="22411-285">**清單 12-Controllers\GroupControllerTest.vb**</span><span class="sxs-lookup"><span data-stu-id="22411-285">**Listing 12 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample13.vb)]

<span data-ttu-id="22411-286">完成所有這些變更之後，所有單元測試都會通過。</span><span class="sxs-lookup"><span data-stu-id="22411-286">After we make all of these changes, once again, all of our unit tests pass.</span></span> <span data-ttu-id="22411-287">我們已完成紅色/綠色/重構的整個迴圈。</span><span class="sxs-lookup"><span data-stu-id="22411-287">We have completed the entire cycle of Red/Green/Refactor.</span></span> <span data-ttu-id="22411-288">我們已實現前兩個使用者案例。</span><span class="sxs-lookup"><span data-stu-id="22411-288">We have implemented the first two user stories.</span></span> <span data-ttu-id="22411-289">我們現在已針對使用者故事所表示的需求，支援單元測試。</span><span class="sxs-lookup"><span data-stu-id="22411-289">We now have supporting unit tests for the requirements expressed in the user stories.</span></span> <span data-ttu-id="22411-290">執行其餘的使用者故事牽涉到重複相同的紅色/綠色/重構迴圈。</span><span class="sxs-lookup"><span data-stu-id="22411-290">Implementing the remainder of the user stories involves repeating the same cycle of Red/Green/Refactor.</span></span>

## <a name="modifying-our-database"></a><span data-ttu-id="22411-291">修改資料庫</span><span class="sxs-lookup"><span data-stu-id="22411-291">Modifying our Database</span></span>

<span data-ttu-id="22411-292">可惜的是，即使我們已滿足單元測試所表示的所有需求，我們也不會完成工作。</span><span class="sxs-lookup"><span data-stu-id="22411-292">Unfortunately, even though we have satisfied all of the requirements expressed by our unit tests, our work is not done.</span></span> <span data-ttu-id="22411-293">我們仍然需要修改資料庫。</span><span class="sxs-lookup"><span data-stu-id="22411-293">We still need to modify our database.</span></span>

<span data-ttu-id="22411-294">我們需要建立新的群組資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="22411-294">We need to create a new Group database table.</span></span> <span data-ttu-id="22411-295">請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="22411-295">Follow these steps:</span></span>

1. <span data-ttu-id="22411-296">在 [伺服器總管] 視窗中，以滑鼠右鍵按一下 [資料表] 資料夾，然後選取 [**加入新的資料表**] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="22411-296">In the Server Explorer window, right-click the Tables folder and select the menu option **Add New Table**.</span></span>
2. <span data-ttu-id="22411-297">在資料表設計工具中，輸入下面所述的兩個數據行。</span><span class="sxs-lookup"><span data-stu-id="22411-297">Enter the two columns described below in the Table Designer.</span></span>
3. <span data-ttu-id="22411-298">將 [識別碼] 資料行標示為 [主鍵] 和 [標識] 資料行。</span><span class="sxs-lookup"><span data-stu-id="22411-298">Mark the Id column as a primary key and Identity column.</span></span>
4. <span data-ttu-id="22411-299">按一下該軟碟的圖示，以 [名稱] 群組儲存新的資料表。</span><span class="sxs-lookup"><span data-stu-id="22411-299">Save the new table with the name Groups by clicking the icon of the floppy.</span></span>

<a id="0.12_table01"></a>

| <span data-ttu-id="22411-300">**資料行名稱**</span><span class="sxs-lookup"><span data-stu-id="22411-300">**Column Name**</span></span> | <span data-ttu-id="22411-301">**資料類型**</span><span class="sxs-lookup"><span data-stu-id="22411-301">**Data Type**</span></span> | <span data-ttu-id="22411-302">**允許 Null**</span><span class="sxs-lookup"><span data-stu-id="22411-302">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="22411-303">ID</span><span class="sxs-lookup"><span data-stu-id="22411-303">Id</span></span> | <span data-ttu-id="22411-304">int</span><span class="sxs-lookup"><span data-stu-id="22411-304">int</span></span> | <span data-ttu-id="22411-305">False</span><span class="sxs-lookup"><span data-stu-id="22411-305">False</span></span> |
| <span data-ttu-id="22411-306">名稱</span><span class="sxs-lookup"><span data-stu-id="22411-306">Name</span></span> | <span data-ttu-id="22411-307">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="22411-307">nvarchar(50)</span></span> | <span data-ttu-id="22411-308">False</span><span class="sxs-lookup"><span data-stu-id="22411-308">False</span></span> |

<span data-ttu-id="22411-309">接下來，我們需要刪除 [Contacts] 資料表中的所有資料（否則，我們無法建立 [連絡人] 和 [群組] 資料表之間的關聯性）。</span><span class="sxs-lookup"><span data-stu-id="22411-309">Next, we need to delete all of the data from the Contacts table (otherwise, we won't be able to create a relationship between the Contacts and Groups tables).</span></span> <span data-ttu-id="22411-310">請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="22411-310">Follow these steps:</span></span>

1. <span data-ttu-id="22411-311">以滑鼠右鍵按一下 [連絡人] 資料表，然後選取 [**顯示資料表資料**] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="22411-311">Right-click the Contacts table and select the menu option **Show Table Data**.</span></span>
2. <span data-ttu-id="22411-312">刪除所有資料列。</span><span class="sxs-lookup"><span data-stu-id="22411-312">Delete all of the rows.</span></span>

<span data-ttu-id="22411-313">接下來，我們需要定義群組資料庫資料表與現有 [連絡人] 資料庫資料表之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="22411-313">Next, we need to define a relationship between the Groups database table and the existing Contacts database table.</span></span> <span data-ttu-id="22411-314">請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="22411-314">Follow these steps:</span></span>

1. <span data-ttu-id="22411-315">按兩下 [伺服器總管] 視窗中的 [連絡人] 資料表以開啟資料表設計工具。</span><span class="sxs-lookup"><span data-stu-id="22411-315">Double-click the Contacts table in the Server Explorer window to open the Table Designer.</span></span>
2. <span data-ttu-id="22411-316">將新的整數資料行加入至名為 GroupId 的連絡人資料表。</span><span class="sxs-lookup"><span data-stu-id="22411-316">Add a new integer column to the Contacts table named GroupId.</span></span>
3. <span data-ttu-id="22411-317">按一下 [關聯性] 按鈕以開啟 [外鍵關聯性] 對話方塊（請參閱 [圖 3]）。</span><span class="sxs-lookup"><span data-stu-id="22411-317">Click the Relationship button to open the Foreign Key Relationships dialog (see Figure 3).</span></span>
4. <span data-ttu-id="22411-318">按一下 [加入] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="22411-318">Click the Add button.</span></span>
5. <span data-ttu-id="22411-319">按一下出現在 [資料表和資料行規格] 按鈕旁邊的省略號按鈕。</span><span class="sxs-lookup"><span data-stu-id="22411-319">Click the ellipsis button that appears next to the Table and Columns Specification button.</span></span>
6. <span data-ttu-id="22411-320">在 [資料表和資料行] 對話方塊中，選取 [群組] 做為主鍵資料表和識別碼做為 [主鍵] 資料行。</span><span class="sxs-lookup"><span data-stu-id="22411-320">In the Tables and Columns dialog, select Groups as the primary key table and Id as the primary key column.</span></span> <span data-ttu-id="22411-321">選取 [連絡人] 做為外鍵資料表和 [GroupId] 做為外鍵資料行（請參閱 [圖 4]）。</span><span class="sxs-lookup"><span data-stu-id="22411-321">Select Contacts as the foreign key table and GroupId as the foreign key column (see Figure 4).</span></span> <span data-ttu-id="22411-322">按一下 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="22411-322">Click the OK button.</span></span>
7. <span data-ttu-id="22411-323">在 [**插入和更新規格**] 底下，選取 [**刪除規則**的**Cascade** ] 值。</span><span class="sxs-lookup"><span data-stu-id="22411-323">Under **INSERT and UPDATE Specification**, select the value **Cascade** for **Delete Rule**.</span></span>
8. <span data-ttu-id="22411-324">按一下 [關閉] 按鈕，關閉 [外鍵關聯性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="22411-324">Click the Close button to close the Foreign Key Relationships dialog.</span></span>
9. <span data-ttu-id="22411-325">按一下 [儲存] 按鈕，將變更儲存至 [連絡人] 資料表。</span><span class="sxs-lookup"><span data-stu-id="22411-325">Click the Save button to save the changes to the Contacts table.</span></span>

<span data-ttu-id="22411-326">[建立資料庫資料表關聯性 ![](iteration-6-use-test-driven-development-vb/_static/image3.jpg)](iteration-6-use-test-driven-development-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="22411-326">[![Creating a database table relationship](iteration-6-use-test-driven-development-vb/_static/image3.jpg)](iteration-6-use-test-driven-development-vb/_static/image5.png)</span></span>

<span data-ttu-id="22411-327">**圖 03**：建立資料庫資料表關聯性（[按一下以查看完整大小的影像](iteration-6-use-test-driven-development-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="22411-327">**Figure 03**: Creating a database table relationship ([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image6.png))</span></span>

<span data-ttu-id="22411-328">[指定資料表關聯性 ![](iteration-6-use-test-driven-development-vb/_static/image4.jpg)](iteration-6-use-test-driven-development-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="22411-328">[![Specifying table relationships](iteration-6-use-test-driven-development-vb/_static/image4.jpg)](iteration-6-use-test-driven-development-vb/_static/image7.png)</span></span>

<span data-ttu-id="22411-329">**圖 04**：指定資料表關聯性（[按一下以查看完整大小的影像](iteration-6-use-test-driven-development-vb/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="22411-329">**Figure 04**: Specifying table relationships([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image8.png))</span></span>

### <a name="updating-our-data-model"></a><span data-ttu-id="22411-330">正在更新我們的資料模型</span><span class="sxs-lookup"><span data-stu-id="22411-330">Updating our Data Model</span></span>

<span data-ttu-id="22411-331">接下來，我們需要更新我們的資料模型，以代表新的資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="22411-331">Next, we need to update our data model to represent the new database table.</span></span> <span data-ttu-id="22411-332">請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="22411-332">Follow these steps:</span></span>

1. <span data-ttu-id="22411-333">按兩下 [模型] 資料夾中的 [ContactManagerModel] 檔案，開啟 [Entity Designer]。</span><span class="sxs-lookup"><span data-stu-id="22411-333">Double-click the ContactManagerModel.edmx file in the Models folder to open the Entity Designer.</span></span>
2. <span data-ttu-id="22411-334">以滑鼠右鍵按一下設計工具介面，然後選取 [**從資料庫更新模型**] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="22411-334">Right-click the Designer surface and select the menu option **Update Model from Database**.</span></span>
3. <span data-ttu-id="22411-335">在 [更新嚮導] 中，選取 [群組] 資料表，然後按一下 [完成] 按鈕（請參閱 [圖 5]）。</span><span class="sxs-lookup"><span data-stu-id="22411-335">In the Update Wizard, select the Groups table and click the Finish button (see Figure 5).</span></span>
4. <span data-ttu-id="22411-336">以滑鼠右鍵按一下 [群組] 實體，然後選取 [**重新命名**] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="22411-336">Right-click the Groups entity and select the menu option **Rename**.</span></span> <span data-ttu-id="22411-337">將 [*群組*] 實體的名稱變更為 [*群組*（單數）]。</span><span class="sxs-lookup"><span data-stu-id="22411-337">Change the name of the *Groups* entity to *Group* (singular).</span></span>
5. <span data-ttu-id="22411-338">以滑鼠右鍵按一下 [Contact] 實體底部的 [群組] 導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="22411-338">Right-click the Groups navigation property that appears at the bottom of the Contact entity.</span></span> <span data-ttu-id="22411-339">將 [*群組*] 導覽屬性的名稱變更為 [*群組*（單數）]。</span><span class="sxs-lookup"><span data-stu-id="22411-339">Change the name of the *Groups* navigation property to *Group* (singular).</span></span>

<span data-ttu-id="22411-340">[![從資料庫更新 Entity Framework 模型](iteration-6-use-test-driven-development-vb/_static/image5.jpg)](iteration-6-use-test-driven-development-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="22411-340">[![Updating an Entity Framework model from the database](iteration-6-use-test-driven-development-vb/_static/image5.jpg)](iteration-6-use-test-driven-development-vb/_static/image9.png)</span></span>

<span data-ttu-id="22411-341">**圖 05**：從資料庫更新 Entity Framework 模型（[按一下以查看完整大小的影像](iteration-6-use-test-driven-development-vb/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="22411-341">**Figure 05**: Updating an Entity Framework model from the database([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image10.png))</span></span>

<span data-ttu-id="22411-342">完成這些步驟之後，您的資料模型會同時代表 [連絡人] 和 [群組] 資料表。</span><span class="sxs-lookup"><span data-stu-id="22411-342">After you complete these steps, your data model will represent both the Contacts and Groups tables.</span></span> <span data-ttu-id="22411-343">Entity Designer 應該會顯示這兩個實體（請參閱 [圖 6]）。</span><span class="sxs-lookup"><span data-stu-id="22411-343">The Entity Designer should show both entities (see Figure 6).</span></span>

<span data-ttu-id="22411-344">[顯示群組和連絡人 ![Entity Designer](iteration-6-use-test-driven-development-vb/_static/image6.jpg)](iteration-6-use-test-driven-development-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="22411-344">[![Entity Designer displaying Group and Contact](iteration-6-use-test-driven-development-vb/_static/image6.jpg)](iteration-6-use-test-driven-development-vb/_static/image11.png)</span></span>

<span data-ttu-id="22411-345">**圖 06**：顯示群組和連絡人的 Entity Designer （[按一下以觀看完整大小的影像](iteration-6-use-test-driven-development-vb/_static/image12.png)）</span><span class="sxs-lookup"><span data-stu-id="22411-345">**Figure 06**: Entity Designer displaying Group and Contact([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image12.png))</span></span>

### <a name="creating-our-repository-classes"></a><span data-ttu-id="22411-346">建立我們的存放庫類別</span><span class="sxs-lookup"><span data-stu-id="22411-346">Creating our Repository Classes</span></span>

<span data-ttu-id="22411-347">接下來，我們需要執行我們的存放庫類別。</span><span class="sxs-lookup"><span data-stu-id="22411-347">Next, we need to implement our repository class.</span></span> <span data-ttu-id="22411-348">在此反復專案的過程中，我們在撰寫程式碼以滿足我們的單元測試時，將數個新方法新增至 IContactManagerRepository 介面。</span><span class="sxs-lookup"><span data-stu-id="22411-348">Over the course of this iteration, we added several new methods to the IContactManagerRepository interface while writing code to satisfy our unit tests.</span></span> <span data-ttu-id="22411-349">IContactManagerRepository 介面的最終版本包含在 [清單 14] 中。</span><span class="sxs-lookup"><span data-stu-id="22411-349">The final version of the IContactManagerRepository interface is contained in Listing 14.</span></span>

<span data-ttu-id="22411-350">**清單 14-Models\IContactManagerRepository.vb**</span><span class="sxs-lookup"><span data-stu-id="22411-350">**Listing 14 - Models\IContactManagerRepository.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample14.vb)]

<span data-ttu-id="22411-351">我們實際上尚未在實際的 EntityContactManagerRepository 類別中，使用與連絡人群組相關的任何方法。</span><span class="sxs-lookup"><span data-stu-id="22411-351">We haven't actually implemented any of the methods related to working with contact groups in our real EntityContactManagerRepository class.</span></span> <span data-ttu-id="22411-352">目前，EntityContactManagerRepository 類別具有 IContactManagerRepository 介面中列出的每個連絡人群組方法的 stub 方法。</span><span class="sxs-lookup"><span data-stu-id="22411-352">Currently, the EntityContactManagerRepository class has stub methods for each of the contact group methods listed in the IContactManagerRepository interface.</span></span> <span data-ttu-id="22411-353">例如，ListGroups （）方法目前看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="22411-353">For example, the ListGroups() method currently looks like this:</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample15.vb)]

<span data-ttu-id="22411-354">Stub 方法可讓我們編譯應用程式並通過單元測試。</span><span class="sxs-lookup"><span data-stu-id="22411-354">The stub methods enabled us to compile our application and pass the unit tests.</span></span> <span data-ttu-id="22411-355">不過，現在是時候實際執行這些方法。</span><span class="sxs-lookup"><span data-stu-id="22411-355">However, now it is time to actually implement these methods.</span></span> <span data-ttu-id="22411-356">EntityContactManagerRepository 類別的最終版本包含在 [清單 13] 中。</span><span class="sxs-lookup"><span data-stu-id="22411-356">The final version of the EntityContactManagerRepository class is contained in Listing 13.</span></span>

<span data-ttu-id="22411-357">**清單 13-Models\EntityContactManagerRepository.vb**</span><span class="sxs-lookup"><span data-stu-id="22411-357">**Listing 13 - Models\EntityContactManagerRepository.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample16.vb)]

### <a name="creating-the-views"></a><span data-ttu-id="22411-358">建立視圖</span><span class="sxs-lookup"><span data-stu-id="22411-358">Creating the Views</span></span>

<span data-ttu-id="22411-359">當您使用預設的 ASP.NET view engine 時，請 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="22411-359">ASP.NET MVC application when you use the default ASP.NET view engine.</span></span> <span data-ttu-id="22411-360">因此，您不會建立 views 來回應特定的單元測試。</span><span class="sxs-lookup"><span data-stu-id="22411-360">So, you don t create views in response to a particular unit test.</span></span> <span data-ttu-id="22411-361">不過，因為應用程式不會有任何視圖，所以無法完成此反復專案，而不需要建立及修改 Contact Manager 應用程式中所包含的視圖。</span><span class="sxs-lookup"><span data-stu-id="22411-361">However, because an application would be useless without views, we can t complete this iteration without creating and modifying the views contained in the Contact Manager application.</span></span>

<span data-ttu-id="22411-362">我們需要建立下列新的視圖來管理連絡人群組（請參閱 [圖 7]）：</span><span class="sxs-lookup"><span data-stu-id="22411-362">We need to create the following new views for managing contact groups (see Figure 7):</span></span>

- <span data-ttu-id="22411-363">Views\Group\Index.aspx-顯示連絡人群組的清單</span><span class="sxs-lookup"><span data-stu-id="22411-363">Views\Group\Index.aspx - Displays list of contact groups</span></span>
- <span data-ttu-id="22411-364">Views\Group\Delete.aspx-顯示刪除連絡人群組的確認表單</span><span class="sxs-lookup"><span data-stu-id="22411-364">Views\Group\Delete.aspx - Displays confirmation form for deleting a contact group</span></span>

<span data-ttu-id="22411-365">[![[群組索引] 視圖](iteration-6-use-test-driven-development-vb/_static/image7.jpg)](iteration-6-use-test-driven-development-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="22411-365">[![The Group Index view](iteration-6-use-test-driven-development-vb/_static/image7.jpg)](iteration-6-use-test-driven-development-vb/_static/image13.png)</span></span>

<span data-ttu-id="22411-366">**圖 07**： [群組索引] 視圖（[按一下以查看完整大小的影像](iteration-6-use-test-driven-development-vb/_static/image14.png)）</span><span class="sxs-lookup"><span data-stu-id="22411-366">**Figure 07**: The Group Index view([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image14.png))</span></span>

<span data-ttu-id="22411-367">我們需要修改下列現有的視圖，使其包含連絡人群組：</span><span class="sxs-lookup"><span data-stu-id="22411-367">We need to modify the following existing views so that they include contact groups:</span></span>

- <span data-ttu-id="22411-368">Views\Home\Create.aspx</span><span class="sxs-lookup"><span data-stu-id="22411-368">Views\Home\Create.aspx</span></span>
- <span data-ttu-id="22411-369">Views\Home\Edit.aspx</span><span class="sxs-lookup"><span data-stu-id="22411-369">Views\Home\Edit.aspx</span></span>
- <span data-ttu-id="22411-370">Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="22411-370">Views\Home\Index.aspx</span></span>

<span data-ttu-id="22411-371">藉由查看本教學課程隨附的 Visual Studio 應用程式，您可以看到修改過的觀點。</span><span class="sxs-lookup"><span data-stu-id="22411-371">You can see the modified views by looking at the Visual Studio application that accompanies this tutorial.</span></span> <span data-ttu-id="22411-372">例如，[圖 8] 說明連絡人索引視圖。</span><span class="sxs-lookup"><span data-stu-id="22411-372">For example, Figure 8 illustrates the Contact Index view.</span></span>

<span data-ttu-id="22411-373">[![連絡人索引視圖](iteration-6-use-test-driven-development-vb/_static/image8.jpg)](iteration-6-use-test-driven-development-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="22411-373">[![The Contact Index view](iteration-6-use-test-driven-development-vb/_static/image8.jpg)](iteration-6-use-test-driven-development-vb/_static/image15.png)</span></span>

<span data-ttu-id="22411-374">**圖 08**：連絡人索引視圖（[按一下以查看完整大小的影像](iteration-6-use-test-driven-development-vb/_static/image16.png)）</span><span class="sxs-lookup"><span data-stu-id="22411-374">**Figure 08**: The Contact Index view([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image16.png))</span></span>

## <a name="summary"></a><span data-ttu-id="22411-375">總結</span><span class="sxs-lookup"><span data-stu-id="22411-375">Summary</span></span>

<span data-ttu-id="22411-376">在此反復專案中，我們會遵循測試導向的開發應用程式設計方法，將新功能新增至我們的 Contact Manager 應用程式。</span><span class="sxs-lookup"><span data-stu-id="22411-376">In this iteration, we added new functionality to our Contact Manager application by following a test-driven development application design methodology.</span></span> <span data-ttu-id="22411-377">我們從建立一組使用者故事開始。</span><span class="sxs-lookup"><span data-stu-id="22411-377">We started by creating a set of user stories.</span></span> <span data-ttu-id="22411-378">我們已建立一組單元測試，其對應于使用者故事所表示的需求。</span><span class="sxs-lookup"><span data-stu-id="22411-378">We created a set of unit tests that corresponds to the requirements expressed by the user stories.</span></span> <span data-ttu-id="22411-379">最後，我們撰寫的程式碼剛好足以滿足單元測試所表示的需求。</span><span class="sxs-lookup"><span data-stu-id="22411-379">Finally, we wrote just enough code to satisfy the requirements expressed by the unit tests.</span></span>

<span data-ttu-id="22411-380">完成撰寫足夠的程式碼以滿足單元測試所表示的需求之後，我們更新了資料庫和 views。</span><span class="sxs-lookup"><span data-stu-id="22411-380">After we finished writing enough code to satisfy the requirements expressed by the unit tests, we updated our database and views.</span></span> <span data-ttu-id="22411-381">我們已在資料庫中新增 [群組] 資料表，並更新 Entity Framework 資料模型。</span><span class="sxs-lookup"><span data-stu-id="22411-381">We added a new Groups table to our database and updated our Entity Framework Data Model.</span></span> <span data-ttu-id="22411-382">我們也建立了一組視圖並加以修改。</span><span class="sxs-lookup"><span data-stu-id="22411-382">We also created and modified a set of views.</span></span>

<span data-ttu-id="22411-383">在下一個反復專案中--最後一個反復專案--我們會重寫應用程式以利用 Ajax。</span><span class="sxs-lookup"><span data-stu-id="22411-383">In the next iteration -- the final iteration -- we rewrite our application to take advantage of Ajax.</span></span> <span data-ttu-id="22411-384">藉由利用 Ajax，我們將改善 Contact Manager 應用程式的回應性和效能。</span><span class="sxs-lookup"><span data-stu-id="22411-384">By taking advantage of Ajax, we'll improve the responsiveness and performance of the Contact Manager application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="22411-385">[上一頁](iteration-5-create-unit-tests-vb.md)
> [下一頁](iteration-7-add-ajax-functionality-vb.md)</span><span class="sxs-lookup"><span data-stu-id="22411-385">[Previous](iteration-5-create-unit-tests-vb.md)
[Next](iteration-7-add-ajax-functionality-vb.md)</span></span>
