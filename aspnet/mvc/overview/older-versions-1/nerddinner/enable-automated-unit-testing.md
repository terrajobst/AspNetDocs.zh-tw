---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: 啟用自動化單元測試 |Microsoft Docs
author: microsoft
description: 步驟12顯示如何開發一套自動化單元測試，以驗證我們的 NerdDinner 功能，讓我們有信心進行變更 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 09a7aa186605a6cce48ee94028425ded957c00d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541675"
---
# <a name="enable-automated-unit-testing"></a><span data-ttu-id="04128-103">啟用自動化單元測試</span><span class="sxs-lookup"><span data-stu-id="04128-103">Enable Automated Unit Testing</span></span>

<span data-ttu-id="04128-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="04128-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="04128-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="04128-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="04128-106">這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟12，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="04128-106">This is step 12 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="04128-107">步驟12顯示如何開發一套自動化單元測試，以驗證我們的 NerdDinner 功能，讓我們有信心在未來對應用程式進行變更和改進。</span><span class="sxs-lookup"><span data-stu-id="04128-107">Step 12 shows how to develop a suite of automated unit tests that verify our NerdDinner functionality, and which will give us the confidence to make changes and improvements to the application in the future.</span></span>
> 
> <span data-ttu-id="04128-108">如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。</span><span class="sxs-lookup"><span data-stu-id="04128-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-12-unit-testing"></a><span data-ttu-id="04128-109">NerdDinner 步驟12：單元測試</span><span class="sxs-lookup"><span data-stu-id="04128-109">NerdDinner Step 12: Unit Testing</span></span>

<span data-ttu-id="04128-110">讓我們來開發一套自動化單元測試，以驗證我們的 NerdDinner 功能，讓我們有信心在未來對應用程式進行變更和改進。</span><span class="sxs-lookup"><span data-stu-id="04128-110">Let's develop a suite of automated unit tests that verify our NerdDinner functionality, and which will give us the confidence to make changes and improvements to the application in the future.</span></span>

### <a name="why-unit-test"></a><span data-ttu-id="04128-111">為何要進行單元測試？</span><span class="sxs-lookup"><span data-stu-id="04128-111">Why Unit Test?</span></span>

<span data-ttu-id="04128-112">在一早上的磁片磁碟機上，您對正在處理的應用程式有非常快的靈感。</span><span class="sxs-lookup"><span data-stu-id="04128-112">On the drive into work one morning you have a sudden flash of inspiration about an application you are working on.</span></span> <span data-ttu-id="04128-113">您已瞭解您可以執行的變更，讓應用程式大幅提升。</span><span class="sxs-lookup"><span data-stu-id="04128-113">You realize there is a change you can implement that will make the application dramatically better.</span></span> <span data-ttu-id="04128-114">它可能是可清除程式碼、加入新功能或修正 bug 的重構。</span><span class="sxs-lookup"><span data-stu-id="04128-114">It might be a refactoring that cleans up the code, adds a new feature, or fixes a bug.</span></span>

<span data-ttu-id="04128-115">當您抵達電腦時，confronts 您的問題就是：「要如何保障這方面的改進？」</span><span class="sxs-lookup"><span data-stu-id="04128-115">The question that confronts you when you arrive at your computer is – "how safe is it to make this improvement?"</span></span> <span data-ttu-id="04128-116">如果進行變更有副作用或中斷某個專案，該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="04128-116">What if making the change has side effects or breaks something?</span></span> <span data-ttu-id="04128-117">這項變更可能很簡單，只需要幾分鐘的時間才能完成，但如果需要數小時才能手動測試所有應用程式案例，該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="04128-117">The change might be simple and only take a few minutes to implement, but what if it takes hours to manually test out all of the application scenarios?</span></span> <span data-ttu-id="04128-118">如果您忘記涵蓋案例，而中斷的應用程式進入生產階段該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="04128-118">What if you forget to cover a scenario and a broken application goes into production?</span></span> <span data-ttu-id="04128-119">這種改進功能真的值得嗎？</span><span class="sxs-lookup"><span data-stu-id="04128-119">Is making this improvement really worth all the effort?</span></span>

<span data-ttu-id="04128-120">自動化單元測試可以提供安全網路，讓您持續增強應用程式，並避免害怕您正在處理的程式碼。</span><span class="sxs-lookup"><span data-stu-id="04128-120">Automated unit tests can provide a safety net that enables you to continually enhance your applications, and avoid being afraid of the code you are working on.</span></span> <span data-ttu-id="04128-121">擁有可快速驗證功能的自動化測試可讓您安心編寫程式碼，並可讓您在其他情況不熟悉的情況進行改善。</span><span class="sxs-lookup"><span data-stu-id="04128-121">Having automated tests that quickly verify functionality enables you to code with confidence – and empower you to make improvements you might otherwise not have felt comfortable doing.</span></span> <span data-ttu-id="04128-122">它們也有助於建立更能維護的解決方案，並具有較長的存留期，這會導致投資的報酬率更高。</span><span class="sxs-lookup"><span data-stu-id="04128-122">They also help create solutions that are more maintainable and have a longer lifetime - which leads to a much higher return on investment.</span></span>

<span data-ttu-id="04128-123">ASP.NET MVC 架構可讓您輕鬆且自然地進行單元測試應用程式功能。</span><span class="sxs-lookup"><span data-stu-id="04128-123">The ASP.NET MVC Framework makes it easy and natural to unit test application functionality.</span></span> <span data-ttu-id="04128-124">它也會啟用測試導向開發（TDD）工作流程，以進行以測試為基礎的開發。</span><span class="sxs-lookup"><span data-stu-id="04128-124">It also enables a Test Driven Development (TDD) workflow that enables test-first based development.</span></span>

### <a name="nerddinnertests-project"></a><span data-ttu-id="04128-125">NerdDinner 測試專案</span><span class="sxs-lookup"><span data-stu-id="04128-125">NerdDinner.Tests Project</span></span>

<span data-ttu-id="04128-126">當我們在本教學課程一開始建立 NerdDinner 應用程式時，會出現一個對話方塊詢問您是否想要建立單元測試專案來與應用程式專案一起執行：</span><span class="sxs-lookup"><span data-stu-id="04128-126">When we created our NerdDinner application at the beginning of this tutorial, we were prompted with a dialog asking whether we wanted to create a unit test project to go along with the application project:</span></span>

![](enable-automated-unit-testing/_static/image1.png)

<span data-ttu-id="04128-127">我們已選取 [是，建立單元測試專案] 選項按鈕，這會在解決方案中加入「NerdDinner」專案：</span><span class="sxs-lookup"><span data-stu-id="04128-127">We kept the "Yes, create a unit test project" radio button selected – which resulted in a "NerdDinner.Tests" project being added to our solution:</span></span>

![](enable-automated-unit-testing/_static/image2.png)

<span data-ttu-id="04128-128">NerdDinner 專案會參考 NerdDinner 應用程式專案元件，並可讓我們輕鬆地將自動化測試加入其中，以驗證應用程式的功能。</span><span class="sxs-lookup"><span data-stu-id="04128-128">The NerdDinner.Tests project references the NerdDinner application project assembly, and enables us to easily add automated tests to it that verify the application functionality.</span></span>

### <a name="creating-unit-tests-for-our-dinner-model-class"></a><span data-ttu-id="04128-129">建立晚餐模型類別的單元測試</span><span class="sxs-lookup"><span data-stu-id="04128-129">Creating Unit Tests for our Dinner Model Class</span></span>

<span data-ttu-id="04128-130">讓我們將一些測試新增至我們的 NerdDinner。測試專案，以驗證我們在建立模型層時所建立的晚餐類別。</span><span class="sxs-lookup"><span data-stu-id="04128-130">Let's add some tests to our NerdDinner.Tests project that verify the Dinner class we created when we built our model layer.</span></span>

<span data-ttu-id="04128-131">首先，我們會在名為「模型」的測試專案中建立新的資料夾，我們將在其中放置模型相關的測試。</span><span class="sxs-lookup"><span data-stu-id="04128-131">We'll start by creating a new folder within our test project called "Models" where we'll place our model-related tests.</span></span> <span data-ttu-id="04128-132">然後，在資料夾上按一下滑鼠右鍵，然後選擇 [**加入&gt;新增測試**] 功能表命令。</span><span class="sxs-lookup"><span data-stu-id="04128-132">We'll then right-click on the folder and choose the **Add-&gt;New Test** menu command.</span></span> <span data-ttu-id="04128-133">這會顯示 [加入新測試] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="04128-133">This will bring up the "Add New Test" dialog.</span></span>

<span data-ttu-id="04128-134">我們會選擇建立「單元測試」，並將它命名為 "DinnerTest.cs"：</span><span class="sxs-lookup"><span data-stu-id="04128-134">We'll choose to create a "Unit Test" and name it "DinnerTest.cs":</span></span>

![](enable-automated-unit-testing/_static/image3.png)

<span data-ttu-id="04128-135">當我們按一下 [確定] 按鈕時 Visual Studio 會將 DinnerTest.cs 檔案新增（並開啟）至專案：</span><span class="sxs-lookup"><span data-stu-id="04128-135">When we click the "ok" button Visual Studio will add (and open) a DinnerTest.cs file to the project:</span></span>

![](enable-automated-unit-testing/_static/image4.png)

<span data-ttu-id="04128-136">預設 Visual Studio 單元測試範本內有一堆定案板程式碼，我發現有點雜亂。</span><span class="sxs-lookup"><span data-stu-id="04128-136">The default Visual Studio unit test template has a bunch of boiler-plate code within it that I find a little messy.</span></span> <span data-ttu-id="04128-137">讓我們將它清除，只包含下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="04128-137">Let's clean it up to just contain the code below:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

<span data-ttu-id="04128-138">上述 DinnerTest 類別上的 [TestClass] 屬性會將它識別為包含測試的類別，以及選擇性的測試初始化和終止程式碼。</span><span class="sxs-lookup"><span data-stu-id="04128-138">The [TestClass] attribute on the DinnerTest class above identifies it as a class that will contain tests, as well as optional test initialization and teardown code.</span></span> <span data-ttu-id="04128-139">我們可以在其中新增具有 [TestMethod] 屬性的公用方法，以定義其中的測試。</span><span class="sxs-lookup"><span data-stu-id="04128-139">We can define tests within it by adding public methods that have a [TestMethod] attribute on them.</span></span>

<span data-ttu-id="04128-140">以下是我們要加入的兩個測試中的第一個，以練習我們的晚餐課程。</span><span class="sxs-lookup"><span data-stu-id="04128-140">Below are the first of two tests we'll add that exercise our Dinner class.</span></span> <span data-ttu-id="04128-141">第一次測試會確認在建立新晚餐時，我們的晚餐無效，而不會正確設定所有屬性。</span><span class="sxs-lookup"><span data-stu-id="04128-141">The first test verifies that our Dinner is invalid if a new Dinner is created without all properties being set correctly.</span></span> <span data-ttu-id="04128-142">第二個測試會在晚餐將所有屬性設為有效的值時，驗證晚餐是否有效：</span><span class="sxs-lookup"><span data-stu-id="04128-142">The second test verifies that our Dinner is valid when a Dinner has all properties set with valid values:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

<span data-ttu-id="04128-143">您會注意到，我們的測試名稱非常明確（而且有點詳細）。</span><span class="sxs-lookup"><span data-stu-id="04128-143">You'll notice above that our test names are very explicit (and somewhat verbose).</span></span> <span data-ttu-id="04128-144">我們會執行這項作業，因為我們可能會建立數百或數千個小型測試，而我們想要讓快速判斷其中每個的意圖和行為（尤其是當我們在測試執行器中尋找失敗的清單時）。</span><span class="sxs-lookup"><span data-stu-id="04128-144">We are doing this because we might end up creating hundreds or thousands of small tests, and we want to make it easy to quickly determine the intent and behavior of each of them (especially when we are looking through a list of failures in a test runner).</span></span> <span data-ttu-id="04128-145">測試名稱應該以測試的功能命名。</span><span class="sxs-lookup"><span data-stu-id="04128-145">The test names should be named after the functionality they are testing.</span></span> <span data-ttu-id="04128-146">在上述情況中，我們會使用「名詞\_應該\_動詞」命名模式。</span><span class="sxs-lookup"><span data-stu-id="04128-146">Above we are using a "Noun\_Should\_Verb" naming pattern.</span></span>

<span data-ttu-id="04128-147">我們會使用「AAA」測試模式來結構化測試，這代表「安排、Act、判斷提示」：</span><span class="sxs-lookup"><span data-stu-id="04128-147">We are structuring the tests using the "AAA" testing pattern – which stands for "Arrange, Act, Assert":</span></span>

- <span data-ttu-id="04128-148">排列：設定要測試的單元</span><span class="sxs-lookup"><span data-stu-id="04128-148">Arrange: Setup the unit being tested</span></span>
- <span data-ttu-id="04128-149">Act：練習受測單元並捕獲結果</span><span class="sxs-lookup"><span data-stu-id="04128-149">Act: Exercise the unit under test and capture results</span></span>
- <span data-ttu-id="04128-150">Assert：驗證行為</span><span class="sxs-lookup"><span data-stu-id="04128-150">Assert: Verify the behavior</span></span>

<span data-ttu-id="04128-151">當我們撰寫測試時，我們想要避免個別測試執行得太多。</span><span class="sxs-lookup"><span data-stu-id="04128-151">When we write tests we want to avoid having the individual tests do too much.</span></span> <span data-ttu-id="04128-152">相反地，每個測試只應驗證單一概念（這可讓您更容易找出失敗的原因）。</span><span class="sxs-lookup"><span data-stu-id="04128-152">Instead each test should verify only a single concept (which will make it much easier to pinpoint the cause of failures).</span></span> <span data-ttu-id="04128-153">最好的指導方針是針對每項測試只使用單一的 assert 語句。</span><span class="sxs-lookup"><span data-stu-id="04128-153">A good guideline is to try and only have a single assert statement for each test.</span></span> <span data-ttu-id="04128-154">如果您在測試方法中有一個以上的 assert 語句，請確定它們全都用來測試相同的概念。</span><span class="sxs-lookup"><span data-stu-id="04128-154">If you have more than one assert statement in a test method, make sure they are all being used to test the same concept.</span></span> <span data-ttu-id="04128-155">若不確定，請進行另一個測試。</span><span class="sxs-lookup"><span data-stu-id="04128-155">When in doubt, make another test.</span></span>

### <a name="running-tests"></a><span data-ttu-id="04128-156">正在執行測試</span><span class="sxs-lookup"><span data-stu-id="04128-156">Running Tests</span></span>

<span data-ttu-id="04128-157">Visual Studio 2008 Professional （及更新版本）包含內建的測試執行器，可用來在 IDE 中執行 Visual Studio 單元測試專案。</span><span class="sxs-lookup"><span data-stu-id="04128-157">Visual Studio 2008 Professional (and higher editions) includes a built-in test runner that can be used to run Visual Studio Unit Test projects within the IDE.</span></span> <span data-ttu-id="04128-158">我們可以在 [方案] 功能表命令**中選取測試&gt;的執行&gt;所有測試**（或輸入 Ctrl R、A）來執行我們所有的單元測試。</span><span class="sxs-lookup"><span data-stu-id="04128-158">We can select the **Test-&gt;Run-&gt;All Tests in Solution** menu command (or type Ctrl R, A) to run all of our unit tests.</span></span> <span data-ttu-id="04128-159">或者，我們可以將游標放在特定測試類別或測試方法中，然後使用**測試&gt;的執行&gt;測試（在目前的內容**功能表命令中，或輸入 Ctrl R、t）來執行單元測試的子集。</span><span class="sxs-lookup"><span data-stu-id="04128-159">Or alternatively we can position our cursor within a specific test class or test method and use the **Test-&gt;Run-&gt;Tests in Current Context** menu command (or type Ctrl R, T) to run a subset of the unit tests.</span></span>

<span data-ttu-id="04128-160">讓我們將游標放在 DinnerTest 類別內，然後輸入 "Ctrl R，T" 來執行我們剛才定義的兩個測試。</span><span class="sxs-lookup"><span data-stu-id="04128-160">Let's position our cursor within the DinnerTest class and type "Ctrl R, T" to run the two tests we just defined.</span></span> <span data-ttu-id="04128-161">當我們這麼做時，[測試結果] 視窗會出現在 Visual Studio 內，而我們會看到測試回合的結果列在其中：</span><span class="sxs-lookup"><span data-stu-id="04128-161">When we do this a "Test Results" window will appear within Visual Studio and we'll see the results of our test run listed within it:</span></span>

![](enable-automated-unit-testing/_static/image5.png)

<span data-ttu-id="04128-162">*注意： [VS test 結果] 視窗預設不會顯示 [類別名稱] 資料行。您可以在 [測試結果] 視窗內按一下滑鼠右鍵，然後使用 [新增/移除資料行] 功能表命令來加入這個。*</span><span class="sxs-lookup"><span data-stu-id="04128-162">*Note: The VS test results window does not show the Class Name column by default. You can add this by right-clicking within the Test Results window and using the Add/Remove Columns menu command.*</span></span>

<span data-ttu-id="04128-163">我們的兩個測試只需要一小部分的時間來執行，您就可以看到兩者都通過了。</span><span class="sxs-lookup"><span data-stu-id="04128-163">Our two tests took only a fraction of a second to run – and as you can see they both passed.</span></span> <span data-ttu-id="04128-164">我們現在可以藉由建立可驗證特定規則驗證的其他測試，並涵蓋我們已新增至晚餐類別的兩個 helper 方法（IsUserHost （）和 IsUserRegistered （）），來增強它們。</span><span class="sxs-lookup"><span data-stu-id="04128-164">We can now go on and augment them by creating additional tests that verify specific rule validations, as well as cover the two helper methods - IsUserHost() and IsUserRegistered() – that we added to the Dinner class.</span></span> <span data-ttu-id="04128-165">將所有這些測試都用於晚餐課程，可讓您更輕鬆且更安全地在未來加入新的商務規則和驗證。</span><span class="sxs-lookup"><span data-stu-id="04128-165">Having all these tests in place for the Dinner class will make it much easier and safer to add new business rules and validations to it in the future.</span></span> <span data-ttu-id="04128-166">我們可以將新的規則邏輯新增至晚餐，然後在幾秒內確認它尚未中斷先前所有的邏輯功能。</span><span class="sxs-lookup"><span data-stu-id="04128-166">We can add our new rule logic to Dinner, and then within seconds verify that it hasn't broken any of our previous logic functionality.</span></span>

<span data-ttu-id="04128-167">請注意，使用描述性測試名稱可讓您輕鬆快速地瞭解每個測試的驗證。</span><span class="sxs-lookup"><span data-stu-id="04128-167">Notice how using a descriptive test name makes it easy to quickly understand what each test is verifying.</span></span> <span data-ttu-id="04128-168">我建議您使用 [**工具-&gt;選項**] 功能表命令，開啟 [測試控管-&gt;測試執行設定] 畫面，然後勾選 [按兩下失敗或不明的單元測試結果] 核取方塊中的 [失敗點]。</span><span class="sxs-lookup"><span data-stu-id="04128-168">I recommend using the **Tools-&gt;Options** menu command, opening the Test Tools-&gt;Test Execution configuration screen, and checking the "Double-clicking a failed or inconclusive unit test result displays the point of failure in the test" checkbox.</span></span> <span data-ttu-id="04128-169">這可讓您在 [測試結果] 視窗中按兩下失敗，並立即跳到判斷提示失敗。</span><span class="sxs-lookup"><span data-stu-id="04128-169">This will allow you to double-click on a failure in the test results window and jump immediately to the assert failure.</span></span>

### <a name="creating-dinnerscontroller-unit-tests"></a><span data-ttu-id="04128-170">建立 DinnersController 單元測試</span><span class="sxs-lookup"><span data-stu-id="04128-170">Creating DinnersController Unit Tests</span></span>

<span data-ttu-id="04128-171">現在讓我們建立一些單元測試，以驗證我們的 DinnersController 功能。</span><span class="sxs-lookup"><span data-stu-id="04128-171">Let's now create some unit tests that verify our DinnersController functionality.</span></span> <span data-ttu-id="04128-172">首先，以滑鼠右鍵按一下測試專案中的 [控制器] 資料夾，然後選擇 [**加入-&gt;新增測試**] 功能表命令。</span><span class="sxs-lookup"><span data-stu-id="04128-172">We'll start by right-clicking on the "Controllers" folder within our Test project and then choose the **Add-&gt;New Test** menu command.</span></span> <span data-ttu-id="04128-173">我們會建立「單元測試」，並將它命名為 "DinnersControllerTest.cs"。</span><span class="sxs-lookup"><span data-stu-id="04128-173">We'll create a "Unit Test" and name it "DinnersControllerTest.cs".</span></span>

<span data-ttu-id="04128-174">我們將建立兩個測試方法，以確認 DinnersController 上的 Details （）動作方法。</span><span class="sxs-lookup"><span data-stu-id="04128-174">We'll create two test methods that verify the Details() action method on the DinnersController.</span></span> <span data-ttu-id="04128-175">第一個會驗證當要求現有晚餐時，會傳回一個視圖。</span><span class="sxs-lookup"><span data-stu-id="04128-175">The first will verify that a View is returned when an existing Dinner is requested.</span></span> <span data-ttu-id="04128-176">第二個驗證會在要求不存在的晚餐時，確認傳回「NotFound」視圖：</span><span class="sxs-lookup"><span data-stu-id="04128-176">The second will verify that a "NotFound" view is returned when a non-existent Dinner is requested:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

<span data-ttu-id="04128-177">上述程式碼會編譯乾淨的。</span><span class="sxs-lookup"><span data-stu-id="04128-177">The above code compiles clean.</span></span> <span data-ttu-id="04128-178">不過，當我們執行測試時，它們會失敗：</span><span class="sxs-lookup"><span data-stu-id="04128-178">When we run the tests, though, they both fail:</span></span>

![](enable-automated-unit-testing/_static/image6.png)

<span data-ttu-id="04128-179">如果我們查看錯誤訊息，我們會看到測試失敗的原因是因為我們的 DinnersRepository 類別無法連接到資料庫。</span><span class="sxs-lookup"><span data-stu-id="04128-179">If we look at the error messages, we'll see that the reason the tests failed was because our DinnersRepository class was unable to connect to a database.</span></span> <span data-ttu-id="04128-180">我們的 NerdDinner 應用程式會使用本機 SQL Server Express 檔案的連接字串，此檔案位於 NerdDinner 應用程式專案的 \App\_Data 目錄底下。</span><span class="sxs-lookup"><span data-stu-id="04128-180">Our NerdDinner application is using a connection-string to a local SQL Server Express file which lives under the \App\_Data directory of the NerdDinner application project.</span></span> <span data-ttu-id="04128-181">因為我們的 NerdDinner 會在不同的目錄中編譯並執行，所以在應用程式專案中，連接字串的相對路徑位置不正確。</span><span class="sxs-lookup"><span data-stu-id="04128-181">Because our NerdDinner.Tests project compiles and runs in a different directory then the application project, the relative path location of our connection-string is incorrect.</span></span>

<span data-ttu-id="04128-182">我們*可以*藉由將 SQL Express 資料庫檔案複製到測試專案，然後在測試專案的 app.config 中為其新增適當的測試連接字串，來修正此問題。</span><span class="sxs-lookup"><span data-stu-id="04128-182">We *could* fix this by copying the SQL Express database file to our test project, and then add an appropriate test connection-string to it in the App.config of our test project.</span></span> <span data-ttu-id="04128-183">這會讓上述測試解除封鎖且正在執行。</span><span class="sxs-lookup"><span data-stu-id="04128-183">This would get the above tests unblocked and running.</span></span>

<span data-ttu-id="04128-184">不過，使用實際資料庫的單元測試程式碼會帶來許多挑戰。</span><span class="sxs-lookup"><span data-stu-id="04128-184">Unit testing code using a real database, though, brings with it a number of challenges.</span></span> <span data-ttu-id="04128-185">尤其是：</span><span class="sxs-lookup"><span data-stu-id="04128-185">Specifically:</span></span>

- <span data-ttu-id="04128-186">它會大幅降低單元測試的執行時間。</span><span class="sxs-lookup"><span data-stu-id="04128-186">It significantly slows down the execution time of unit tests.</span></span> <span data-ttu-id="04128-187">執行測試所花費的時間愈長，通常執行的可能性就越低。</span><span class="sxs-lookup"><span data-stu-id="04128-187">The longer it takes to run tests, the less likely you are to execute them frequently.</span></span> <span data-ttu-id="04128-188">在理想的情況下，您會想要讓單元測試能夠在幾秒鐘內執行，並以自然的方式來編譯專案。</span><span class="sxs-lookup"><span data-stu-id="04128-188">Ideally you want your unit tests to be able to be run in seconds – and have it be something you do as naturally as compiling the project.</span></span>
- <span data-ttu-id="04128-189">它會使測試中的設定和清除邏輯變得複雜。</span><span class="sxs-lookup"><span data-stu-id="04128-189">It complicates the setup and cleanup logic within tests.</span></span> <span data-ttu-id="04128-190">您想要讓每個單元測試獨立，並與其他人獨立（不會有副作用或相依性）。</span><span class="sxs-lookup"><span data-stu-id="04128-190">You want each unit test to be isolated and independent of others (with no side effects or dependencies).</span></span> <span data-ttu-id="04128-191">在處理實際的資料庫時，您必須留意狀態，並在測試之間重設它。</span><span class="sxs-lookup"><span data-stu-id="04128-191">When working against a real database you have to be mindful of state and reset it between tests.</span></span>

<span data-ttu-id="04128-192">讓我們看一下稱為「相依性插入」的設計模式，可協助我們解決這些問題，並避免需要在測試中使用實際的資料庫。</span><span class="sxs-lookup"><span data-stu-id="04128-192">Let's look at a design pattern called "dependency injection" that can help us work around these issues and avoid the need to use a real database with our tests.</span></span>

### <a name="dependency-injection"></a><span data-ttu-id="04128-193">相依性插入</span><span class="sxs-lookup"><span data-stu-id="04128-193">Dependency Injection</span></span>

<span data-ttu-id="04128-194">現在 DinnersController 已緊密地「結合」至 DinnerRepository 類別。</span><span class="sxs-lookup"><span data-stu-id="04128-194">Right now DinnersController is tightly "coupled" to the DinnerRepository class.</span></span> <span data-ttu-id="04128-195">「結合」指的是類別明確依賴另一個類別才能正常執行的情況：</span><span class="sxs-lookup"><span data-stu-id="04128-195">"Coupling" refers to a situation where a class explicitly relies on another class in order to work:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

<span data-ttu-id="04128-196">由於 DinnerRepository 類別需要存取資料庫，因此 DinnersController 類別在 DinnerRepository 上具有緊密結合的相依性，最後需要我們擁有資料庫，才能測試 DinnersController 動作方法。</span><span class="sxs-lookup"><span data-stu-id="04128-196">Because the DinnerRepository class requires access to a database, the tightly coupled dependency the DinnersController class has on the DinnerRepository ends up requiring us to have a database in order for the DinnersController action methods to be tested.</span></span>

<span data-ttu-id="04128-197">我們可以藉由採用稱為「相依性插入」的設計模式來解決此問題，這種方法會在使用它們的類別內不再以隱含方式建立相依性（例如提供資料存取的儲存機制類別）。</span><span class="sxs-lookup"><span data-stu-id="04128-197">We can get around this by employing a design pattern called "dependency injection" – which is an approach where dependencies (like repository classes that provide data access) are no longer implicitly created within classes that use them.</span></span> <span data-ttu-id="04128-198">相反地，您可以使用函式引數，將相依性明確傳遞給使用它們的類別。</span><span class="sxs-lookup"><span data-stu-id="04128-198">Instead, dependencies can be explicitly passed to the class that uses them using constructor arguments.</span></span> <span data-ttu-id="04128-199">如果使用介面來定義相依性，我們就可以彈性地針對單元測試案例傳入「假」相依性執行。</span><span class="sxs-lookup"><span data-stu-id="04128-199">If the dependencies are defined using interfaces, we then have the flexibility to pass in "fake" dependency implementations for unit test scenarios.</span></span> <span data-ttu-id="04128-200">這可讓我們建立不需要存取資料庫的測試特定相依性。</span><span class="sxs-lookup"><span data-stu-id="04128-200">This enables us to create test-specific dependency implementations that do not actually require access to a database.</span></span>

<span data-ttu-id="04128-201">若要查看其實際運作情況，讓我們使用 DinnersController 來執行相依性插入。</span><span class="sxs-lookup"><span data-stu-id="04128-201">To see this in action, let's implement dependency injection with our DinnersController.</span></span>

#### <a name="extracting-an-idinnerrepository-interface"></a><span data-ttu-id="04128-202">解壓縮 IDinnerRepository 介面</span><span class="sxs-lookup"><span data-stu-id="04128-202">Extracting an IDinnerRepository interface</span></span>

<span data-ttu-id="04128-203">我們的第一個步驟是建立新的 IDinnerRepository 介面，以封裝我們的控制器需要取得和更新 Dinners 的儲存機制合約。</span><span class="sxs-lookup"><span data-stu-id="04128-203">Our first step will be to create a new IDinnerRepository interface that encapsulates the repository contract our controllers require to retrieve and update Dinners.</span></span>

<span data-ttu-id="04128-204">我們可以用滑鼠右鍵按一下 [\Models] 資料夾，然後選擇 [**加入-&gt;新專案**] 功能表命令，並建立名為 IDinnerRepository.cs 的新介面，以手動方式定義此介面合約。</span><span class="sxs-lookup"><span data-stu-id="04128-204">We can define this interface contract manually by right-clicking on the \Models folder, and then choosing the **Add-&gt;New Item** menu command and creating a new interface named IDinnerRepository.cs.</span></span>

<span data-ttu-id="04128-205">或者，我們可以使用內建 Visual Studio Professional （和更新版本）的重構工具，從現有的 DinnerRepository 類別自動為我們解壓縮並建立介面。</span><span class="sxs-lookup"><span data-stu-id="04128-205">Alternatively we can use the refactoring tools built-into Visual Studio Professional (and higher editions) to automatically extract and create an interface for us from our existing DinnerRepository class.</span></span> <span data-ttu-id="04128-206">若要使用 VS 來解壓縮此介面，只要將游標放在 [DinnerRepository] 類別的文字編輯器中，然後以滑鼠右鍵按一下並選擇 [**重構-&gt;解壓縮介面**] 功能表命令：</span><span class="sxs-lookup"><span data-stu-id="04128-206">To extract this interface using VS, simply position the cursor in the text editor on the DinnerRepository class, and then right-click and choose the **Refactor-&gt;Extract Interface** menu command:</span></span>

![](enable-automated-unit-testing/_static/image7.png)

<span data-ttu-id="04128-207">這會啟動 [解壓縮介面] 對話方塊，並提示我們輸入要建立之介面的名稱。</span><span class="sxs-lookup"><span data-stu-id="04128-207">This will launch the "Extract Interface" dialog and prompt us for the name of the interface to create.</span></span> <span data-ttu-id="04128-208">它會預設為 IDinnerRepository，並在現有的 DinnerRepository 類別上自動選取要新增至介面的所有公用方法：</span><span class="sxs-lookup"><span data-stu-id="04128-208">It will default to IDinnerRepository and automatically select all public methods on the existing DinnerRepository class to add to the interface:</span></span>

![](enable-automated-unit-testing/_static/image8.png)

<span data-ttu-id="04128-209">當我們按一下 [確定] 按鈕時，Visual Studio 會將新的 IDinnerRepository 介面新增至我們的應用程式：</span><span class="sxs-lookup"><span data-stu-id="04128-209">When we click the "ok" button, Visual Studio will add a new IDinnerRepository interface to our application:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

<span data-ttu-id="04128-210">而我們現有的 DinnerRepository 類別將會更新，使其能夠執行介面：</span><span class="sxs-lookup"><span data-stu-id="04128-210">And our existing DinnerRepository class will be updated so that it implements the interface:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a><span data-ttu-id="04128-211">更新 DinnersController 以支援函數插入</span><span class="sxs-lookup"><span data-stu-id="04128-211">Updating DinnersController to support constructor injection</span></span>

<span data-ttu-id="04128-212">我們現在會更新 DinnersController 類別，以使用新的介面。</span><span class="sxs-lookup"><span data-stu-id="04128-212">We'll now update the DinnersController class to use the new interface.</span></span>

<span data-ttu-id="04128-213">目前 DinnersController 是硬式編碼，因此它的 "dinnerRepository" 欄位一律是 DinnerRepository 類別：</span><span class="sxs-lookup"><span data-stu-id="04128-213">Currently DinnersController is hard-coded such that its "dinnerRepository" field is always a DinnerRepository class:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

<span data-ttu-id="04128-214">我們會將它變更，讓 "dinnerRepository" 欄位的類型是 IDinnerRepository，而不是 DinnerRepository。</span><span class="sxs-lookup"><span data-stu-id="04128-214">We'll change it so that the "dinnerRepository" field is of type IDinnerRepository instead of DinnerRepository.</span></span> <span data-ttu-id="04128-215">接著，我們會新增兩個公用 DinnersController 的函式。</span><span class="sxs-lookup"><span data-stu-id="04128-215">We'll then add two public DinnersController constructors.</span></span> <span data-ttu-id="04128-216">其中一個函式允許將 IDinnerRepository 當做引數傳遞。</span><span class="sxs-lookup"><span data-stu-id="04128-216">One of the constructors allows an IDinnerRepository to be passed as an argument.</span></span> <span data-ttu-id="04128-217">另一個則是使用現有 DinnerRepository 執行的預設函式：</span><span class="sxs-lookup"><span data-stu-id="04128-217">The other is a default constructor that uses our existing DinnerRepository implementation:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

<span data-ttu-id="04128-218">由於 ASP.NET MVC 預設會使用預設的函式建立控制器類別，因此我們在執行時間的 DinnersController 會繼續使用 DinnerRepository 類別來執行資料存取。</span><span class="sxs-lookup"><span data-stu-id="04128-218">Because ASP.NET MVC by default creates controller classes using default constructors, our DinnersController at runtime will continue to use the DinnerRepository class to perform data access.</span></span>

<span data-ttu-id="04128-219">不過，我們現在可以使用參數的函式，更新我們的單元測試，以傳入「假」晚餐存放庫的實施。</span><span class="sxs-lookup"><span data-stu-id="04128-219">We can now update our unit tests, though, to pass in a "fake" dinner repository implementation using the parameter constructor.</span></span> <span data-ttu-id="04128-220">此「假」晚餐存放庫將不需要存取實際的資料庫，而是會使用記憶體中的範例資料。</span><span class="sxs-lookup"><span data-stu-id="04128-220">This "fake" dinner repository will not require access to a real database, and instead will use in-memory sample data.</span></span>

#### <a name="creating-the-fakedinnerrepository-class"></a><span data-ttu-id="04128-221">建立 FakeDinnerRepository 類別</span><span class="sxs-lookup"><span data-stu-id="04128-221">Creating the FakeDinnerRepository class</span></span>

<span data-ttu-id="04128-222">讓我們來建立 FakeDinnerRepository 類別。</span><span class="sxs-lookup"><span data-stu-id="04128-222">Let's create a FakeDinnerRepository class.</span></span>

<span data-ttu-id="04128-223">我們會先在 NerdDinner 中建立 "Fakes" 目錄，然後在其中新增 FakeDinnerRepository 類別（以滑鼠右鍵按一下該資料夾，然後選擇 [新增 **-&gt;新類別**]）：</span><span class="sxs-lookup"><span data-stu-id="04128-223">We'll begin by creating a "Fakes" directory within our NerdDinner.Tests project and then add a new FakeDinnerRepository class to it (right-click on the folder and choose **Add-&gt;New Class**):</span></span>

![](enable-automated-unit-testing/_static/image9.png)

<span data-ttu-id="04128-224">我們將更新程式碼，讓 FakeDinnerRepository 類別能夠執行 IDinnerRepository 介面。</span><span class="sxs-lookup"><span data-stu-id="04128-224">We'll update the code so that the FakeDinnerRepository class implements the IDinnerRepository interface.</span></span> <span data-ttu-id="04128-225">然後，我們可以在其上按一下滑鼠右鍵，然後選擇 [執行介面 IDinnerRepository] 內容功能表命令：</span><span class="sxs-lookup"><span data-stu-id="04128-225">We can then right-click on it and choose the "Implement interface IDinnerRepository" context menu command:</span></span>

![](enable-automated-unit-testing/_static/image10.png)

<span data-ttu-id="04128-226">這會導致 Visual Studio 自動將所有 IDinnerRepository 介面成員新增至我們的 FakeDinnerRepository 類別，其具有預設「存根 out」的實作為：</span><span class="sxs-lookup"><span data-stu-id="04128-226">This will cause Visual Studio to automatically add all of the IDinnerRepository interface members to our FakeDinnerRepository class with default "stub out" implementations:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

<span data-ttu-id="04128-227">然後，我們可以更新 FakeDinnerRepository 的執行，以從記憶體中清單中取出&lt;晚餐&gt; 集合做為「函式引數」傳遞給它：</span><span class="sxs-lookup"><span data-stu-id="04128-227">We can then update the FakeDinnerRepository implementation to work off of an in-memory List&lt;Dinner&gt; collection passed to it as a constructor argument:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

<span data-ttu-id="04128-228">我們現在有一個不需要資料庫的假 IDinnerRepository，而可以改為處理晚餐物件的記憶體中清單。</span><span class="sxs-lookup"><span data-stu-id="04128-228">We now have a fake IDinnerRepository implementation that does not require a database, and can instead work off an in-memory list of Dinner objects.</span></span>

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a><span data-ttu-id="04128-229">搭配單元測試使用 FakeDinnerRepository</span><span class="sxs-lookup"><span data-stu-id="04128-229">Using the FakeDinnerRepository with Unit Tests</span></span>

<span data-ttu-id="04128-230">讓我們回到先前失敗的 DinnersController 單元測試，因為資料庫無法使用。</span><span class="sxs-lookup"><span data-stu-id="04128-230">Let's return to the DinnersController unit tests that failed earlier because the database wasn't available.</span></span> <span data-ttu-id="04128-231">我們可以使用下列程式碼，將測試方法更新為使用已填入範例記憶體中晚餐資料的 FakeDinnerRepository 至 DinnersController：</span><span class="sxs-lookup"><span data-stu-id="04128-231">We can update the test methods to use a FakeDinnerRepository populated with sample in-memory Dinner data to the DinnersController using the code below:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

<span data-ttu-id="04128-232">現在，當我們執行這些測試時，它們都會通過：</span><span class="sxs-lookup"><span data-stu-id="04128-232">And now when we run these tests they both pass:</span></span>

![](enable-automated-unit-testing/_static/image11.png)

<span data-ttu-id="04128-233">最棒的是，它們只需要一小部分的時間來執行，而且不需要任何複雜的設定/清除邏輯。</span><span class="sxs-lookup"><span data-stu-id="04128-233">Best of all, they take only a fraction of a second to run, and do not require any complicated setup/cleanup logic.</span></span> <span data-ttu-id="04128-234">我們現在可以對所有 DinnersController 動作方法程式碼（包括清單、分頁、詳細資料、建立、更新和刪除）進行單元測試，而不需要連接到實際的資料庫。</span><span class="sxs-lookup"><span data-stu-id="04128-234">We can now unit test all of our DinnersController action method code (including listing, paging, details, create, update and delete) without ever needing to connect to a real database.</span></span>

| <span data-ttu-id="04128-235">**側邊主題：相依性插入架構**</span><span class="sxs-lookup"><span data-stu-id="04128-235">**Side Topic: Dependency Injection Frameworks**</span></span> |
| --- |
| <span data-ttu-id="04128-236">執行手動相依性插入（如上所示）可以正常運作，但隨著應用程式中的相依性和元件數目增加而變得更難維護。</span><span class="sxs-lookup"><span data-stu-id="04128-236">Performing manual dependency injection (like we are above) works fine, but does become harder to maintain as the number of dependencies and components in an application increases.</span></span> <span data-ttu-id="04128-237">有數個適用于 .NET 的相依性插入架構，可協助提供更多相依性管理的彈性。</span><span class="sxs-lookup"><span data-stu-id="04128-237">Several dependency injection frameworks exist for .NET that can help provide even more dependency management flexibility.</span></span> <span data-ttu-id="04128-238">這些架構（有時也稱為「控制反轉」（IoC）容器）提供了一種機制，可讓您在執行時間指定和傳遞相依性給物件（最常使用的是函式插入）).</span><span class="sxs-lookup"><span data-stu-id="04128-238">These frameworks, also sometimes called "Inversion of Control" (IoC) containers, provide mechanisms that enable an additional level of configuration support for specifying and passing dependencies to objects at runtime (most often using constructor injection).</span></span> <span data-ttu-id="04128-239">.NET 中一些較受歡迎的 OSS 相依性插入/IOC 架構包括： AutoFac、Ninject、Spring.NET、StructureMap 和 Windsor。</span><span class="sxs-lookup"><span data-stu-id="04128-239">Some of the more popular OSS Dependency Injection / IOC frameworks in .NET include: AutoFac, Ninject, Spring.NET, StructureMap, and Windsor.</span></span> <span data-ttu-id="04128-240">ASP.NET MVC 會公開擴充性 Api，讓開發人員可以參與控制器的解析和具現化，讓相依性插入/IoC 架構在此程式內完全整合。</span><span class="sxs-lookup"><span data-stu-id="04128-240">ASP.NET MVC exposes extensibility APIs that enable developers to participate in the resolution and instantiation of controllers, and which enables Dependency Injection / IoC frameworks to be cleanly integrated within this process.</span></span> <span data-ttu-id="04128-241">使用 DI/IOC 架構也可讓我們從我們的 DinnersController 移除預設的處理函式，這會完全移除其與 DinnerRepository 之間的結合。</span><span class="sxs-lookup"><span data-stu-id="04128-241">Using a DI/IOC framework would also enable us to remove the default constructor from our DinnersController – which would completely remove the coupling between it and the DinnerRepository.</span></span> <span data-ttu-id="04128-242">我們不會將相依性插入/IOC 架構與我們的 NerdDinner 應用程式搭配使用。</span><span class="sxs-lookup"><span data-stu-id="04128-242">We won't be using a dependency injection / IOC framework with our NerdDinner application.</span></span> <span data-ttu-id="04128-243">但是，如果 NerdDinner 的程式碼基底和功能成長，我們就可以考慮這一點。</span><span class="sxs-lookup"><span data-stu-id="04128-243">But it is something we could consider for the future if the NerdDinner code-base and capabilities grew.</span></span> |

### <a name="creating-edit-action-unit-tests"></a><span data-ttu-id="04128-244">建立編輯動作單元測試</span><span class="sxs-lookup"><span data-stu-id="04128-244">Creating Edit Action Unit Tests</span></span>

<span data-ttu-id="04128-245">現在讓我們建立一些單元測試，以驗證 DinnersController 的編輯功能。</span><span class="sxs-lookup"><span data-stu-id="04128-245">Let's now create some unit tests that verify the Edit functionality of the DinnersController.</span></span> <span data-ttu-id="04128-246">首先，我們會測試編輯動作的 HTTP GET 版本：</span><span class="sxs-lookup"><span data-stu-id="04128-246">We'll start by testing the HTTP-GET version of our Edit action:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

<span data-ttu-id="04128-247">我們將建立一項測試，以驗證當要求了有效的晚餐時，會將 DinnerFormViewModel 物件所支援的視圖呈現回來：</span><span class="sxs-lookup"><span data-stu-id="04128-247">We'll create a test that verifies that a View backed by a DinnerFormViewModel object is rendered back when a valid dinner is requested:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

<span data-ttu-id="04128-248">不過，當我們執行測試時，我們會發現它會失敗，因為當編輯方法存取 User.Identity.Name 屬性來執行 IsHostedBy （）檢查時，會擲回 null 參考例外狀況。</span><span class="sxs-lookup"><span data-stu-id="04128-248">When we run the test, though, we'll find that it fails because a null reference exception is thrown when the Edit method accesses the User.Identity.Name property to perform the Dinner.IsHostedBy() check.</span></span>

<span data-ttu-id="04128-249">控制器基類上的 User 物件會封裝已登入使用者的詳細資料，並在執行時間建立控制器時，藉由 ASP.NET MVC 來填入。</span><span class="sxs-lookup"><span data-stu-id="04128-249">The User object on the Controller base class encapsulates details about the logged-in user, and is populated by ASP.NET MVC when it creates the controller at runtime.</span></span> <span data-ttu-id="04128-250">因為我們要在 web 伺服器環境外測試 DinnersController，所以不會設定 User 物件（因此是 null 參考例外狀況）。</span><span class="sxs-lookup"><span data-stu-id="04128-250">Because we are testing the DinnersController outside of a web-server environment, the User object isn't set (hence the null reference exception).</span></span>

### <a name="mocking-the-useridentityname-property"></a><span data-ttu-id="04128-251">模擬 User.Identity.Name 屬性</span><span class="sxs-lookup"><span data-stu-id="04128-251">Mocking the User.Identity.Name property</span></span>

<span data-ttu-id="04128-252">模擬架構可讓我們以動態方式建立支援測試的假版本相依物件，使測試變得更容易。</span><span class="sxs-lookup"><span data-stu-id="04128-252">Mocking frameworks make testing easier by enabling us to dynamically create fake versions of dependent objects that support our tests.</span></span> <span data-ttu-id="04128-253">例如，我們可以使用編輯動作測試中的模擬架構，以動態方式建立一個使用者物件，讓我們的 DinnersController 可用來查閱模擬的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="04128-253">For example, we can use a mocking framework in our Edit action test to dynamically create a User object that our DinnersController can use to lookup a simulated username.</span></span> <span data-ttu-id="04128-254">這可避免在執行測試時擲回 null 參考。</span><span class="sxs-lookup"><span data-stu-id="04128-254">This will avoid a null reference from being thrown when we run our test.</span></span>

<span data-ttu-id="04128-255">有許多 .NET 模擬架構可以搭配 ASP.NET MVC 使用（您可以在這裡看到其清單： [http://www.mockframeworks.com/](http://www.mockframeworks.com/)）。</span><span class="sxs-lookup"><span data-stu-id="04128-255">There are many .NET mocking frameworks that can be used with ASP.NET MVC (you can see a list of them here: [http://www.mockframeworks.com/](http://www.mockframeworks.com/)).</span></span> <span data-ttu-id="04128-256">若要測試我們的 NerdDinner 應用程式，我們將使用名為 "Moq" 的開放原始碼模擬架構，可從[http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq)免費下載。</span><span class="sxs-lookup"><span data-stu-id="04128-256">For testing our NerdDinner application we'll use an open source mocking framework called "Moq", which can be downloaded for free from [http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq).</span></span>

<span data-ttu-id="04128-257">下載之後，我們會將 NerdDinner 中的參考新增至 Moq 元件：</span><span class="sxs-lookup"><span data-stu-id="04128-257">Once downloaded, we'll add a reference in our NerdDinner.Tests project to the Moq.dll assembly:</span></span>

![](enable-automated-unit-testing/_static/image12.png)

<span data-ttu-id="04128-258">接著，我們會將 "CreateDinnersControllerAs （username）" 協助程式方法新增至我們的測試類別，並採用使用者名稱做為參數，然後在 DinnersController 實例上「模擬」 User.Identity.Name 屬性：</span><span class="sxs-lookup"><span data-stu-id="04128-258">We'll then add a "CreateDinnersControllerAs(username)" helper method to our test class that takes a username as a parameter, and which then "mocks" the User.Identity.Name property on the DinnersController instance:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

<span data-ttu-id="04128-259">在上述情況下，我們會使用 Moq 來建立模擬物件，以 fakes ControllerCoNtext 物件（這是 ASP.NET MVC 傳遞至控制器類別以公開執行時間物件（例如 User、Request、Response 和 Session）的模型。</span><span class="sxs-lookup"><span data-stu-id="04128-259">Above we are using Moq to create a Mock object that fakes a ControllerContext object (which is what ASP.NET MVC passes to Controller classes to expose runtime objects like User, Request, Response, and Session).</span></span> <span data-ttu-id="04128-260">我們會在 Mock 上呼叫 "SetupGet" 方法，以指出 ControllerCoNtext 上的 HttpCoNtext.User.Identity.Name 屬性應傳回我們傳遞至 helper 方法的使用者名稱字串。</span><span class="sxs-lookup"><span data-stu-id="04128-260">We are calling the "SetupGet" method on the Mock to indicate that the HttpContext.User.Identity.Name property on ControllerContext should return the username string we passed to the helper method.</span></span>

<span data-ttu-id="04128-261">我們可以模擬任意數目的 ControllerCoNtext 屬性和方法。</span><span class="sxs-lookup"><span data-stu-id="04128-261">We can mock any number of ControllerContext properties and methods.</span></span> <span data-ttu-id="04128-262">為了說明這一點，我也新增了 IsAuthenticated 屬性的 SetupGet （）呼叫（下面的測試實際上不需要這麼做），但這有助於說明您可以如何模擬要求屬性。</span><span class="sxs-lookup"><span data-stu-id="04128-262">To illustrate this I've also added a SetupGet() call for the Request.IsAuthenticated property (which isn't actually needed for the tests below – but which helps illustrate how you can mock Request properties).</span></span> <span data-ttu-id="04128-263">當我們完成時，我們會將 ControllerCoNtext mock 的實例指派給我們的 helper 方法所傳回的 DinnersController。</span><span class="sxs-lookup"><span data-stu-id="04128-263">When we are done we assign an instance of the ControllerContext mock to the DinnersController our helper method returns.</span></span>

<span data-ttu-id="04128-264">我們現在可以撰寫單元測試，使用此 helper 方法來測試牽涉到不同使用者的編輯案例：</span><span class="sxs-lookup"><span data-stu-id="04128-264">We can now write unit tests that use this helper method to test Edit scenarios involving different users:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

<span data-ttu-id="04128-265">現在，當我們執行其通過的測試時：</span><span class="sxs-lookup"><span data-stu-id="04128-265">And now when we run the tests they pass:</span></span>

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a><span data-ttu-id="04128-266">測試 UpdateModel （）案例</span><span class="sxs-lookup"><span data-stu-id="04128-266">Testing UpdateModel() scenarios</span></span>

<span data-ttu-id="04128-267">我們已建立涵蓋編輯動作之 HTTP GET 版本的測試。</span><span class="sxs-lookup"><span data-stu-id="04128-267">We've created tests that cover the HTTP-GET version of the Edit action.</span></span> <span data-ttu-id="04128-268">現在讓我們建立一些測試，以驗證編輯動作的 HTTP POST 版本：</span><span class="sxs-lookup"><span data-stu-id="04128-268">Let's now create some tests that verify the HTTP-POST version of the Edit action:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

<span data-ttu-id="04128-269">我們使用這個動作方法來支援有趣的新測試案例，就是在控制器基類上使用 UpdateModel （） helper 方法。</span><span class="sxs-lookup"><span data-stu-id="04128-269">The interesting new testing scenario for us to support with this action method is its usage of the UpdateModel() helper method on the Controller base class.</span></span> <span data-ttu-id="04128-270">我們會使用此 helper 方法，將表單張貼值系結至晚餐物件實例。</span><span class="sxs-lookup"><span data-stu-id="04128-270">We are using this helper method to bind form-post values to our Dinner object instance.</span></span>

<span data-ttu-id="04128-271">以下兩個測試示範如何提供表單張貼值，讓 UpdateModel （） helper 方法可供使用。</span><span class="sxs-lookup"><span data-stu-id="04128-271">Below are two tests that demonstrates how we can supply form posted values for the UpdateModel() helper method to use.</span></span> <span data-ttu-id="04128-272">我們的作法是建立和填入 FormCollection 物件，然後將它指派給控制器上的 "ValueProvider" 屬性。</span><span class="sxs-lookup"><span data-stu-id="04128-272">We'll do this by creating and populating a FormCollection object, and then assign it to the "ValueProvider" property on the Controller.</span></span>

<span data-ttu-id="04128-273">第一個測試會確認在成功儲存時，瀏覽器會重新導向至 [詳細資料] 動作。</span><span class="sxs-lookup"><span data-stu-id="04128-273">The first test verifies that on a successful save the browser is redirected to the details action.</span></span> <span data-ttu-id="04128-274">第二個測試會確認在張貼不正確輸入時，動作會再次重新顯示編輯檢視，並顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="04128-274">The second test verifies that when invalid input is posted the action redisplays the edit view again with an error message.</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a><span data-ttu-id="04128-275">測試總結</span><span class="sxs-lookup"><span data-stu-id="04128-275">Testing Wrap-Up</span></span>

<span data-ttu-id="04128-276">我們已討論過單元測試控制器類別所牽涉到的核心概念。</span><span class="sxs-lookup"><span data-stu-id="04128-276">We've covered the core concepts involved in unit testing controller classes.</span></span> <span data-ttu-id="04128-277">我們可以使用這些技術來輕鬆建立數百個簡單的測試，以驗證應用程式的行為。</span><span class="sxs-lookup"><span data-stu-id="04128-277">We can use these techniques to easily create hundreds of simple tests that verify the behavior of our application.</span></span>

<span data-ttu-id="04128-278">因為我們的控制器和模型測試並不需要實際的資料庫，所以非常快速且容易執行。</span><span class="sxs-lookup"><span data-stu-id="04128-278">Because our controller and model tests do not require a real database, they are extremely fast and easy to run.</span></span> <span data-ttu-id="04128-279">我們可以在幾秒鐘內執行數百個自動化測試，並立即取得對我們所做的變更是否中斷的意見反應。</span><span class="sxs-lookup"><span data-stu-id="04128-279">We'll be able to execute hundreds of automated tests in seconds, and immediately get feedback as to whether a change we made broke something.</span></span> <span data-ttu-id="04128-280">這將有助於讓我們安心地持續改進、重構和精簡應用程式。</span><span class="sxs-lookup"><span data-stu-id="04128-280">This will help provide us the confidence to continually improve, refactor, and refine our application.</span></span>

<span data-ttu-id="04128-281">我們在本章的最後一個主題中討論過測試，但不是因為測試是您應該在開發流程結束時執行的作業！</span><span class="sxs-lookup"><span data-stu-id="04128-281">We covered testing as the last topic in this chapter – but not because testing is something you should do at the end of a development process!</span></span> <span data-ttu-id="04128-282">相反地，您應該在開發過程中儘早撰寫自動化測試。</span><span class="sxs-lookup"><span data-stu-id="04128-282">On the contrary, you should write automated tests as early as possible in your development process.</span></span> <span data-ttu-id="04128-283">這麼做可讓您在開發時立即取得意見反應，協助您思考 thoughtfully 應用程式使用案例的相關資訊，並引導您在設計應用程式時，使用乾淨的分層和結合。</span><span class="sxs-lookup"><span data-stu-id="04128-283">Doing so enables you to get immediate feedback as you develop, helps you think thoughtfully about your application's use case scenarios, and guides you to design your application with clean layering and coupling in mind.</span></span>

<span data-ttu-id="04128-284">本書稍後的章節將討論「測試導向開發」（TDD），以及如何搭配 ASP.NET MVC 來使用它。</span><span class="sxs-lookup"><span data-stu-id="04128-284">A later chapter in the book will discuss Test Driven Development (TDD), and how to use it with ASP.NET MVC.</span></span> <span data-ttu-id="04128-285">TDD 是一種反復的編碼做法，您可以在其中先撰寫所產生之程式碼所能滿足的測試。</span><span class="sxs-lookup"><span data-stu-id="04128-285">TDD is an iterative coding practice where you first write the tests that your resulting code will satisfy.</span></span> <span data-ttu-id="04128-286">有了 TDD，您就可以藉由建立測試來驗證您即將執行的功能，以開始每項功能。</span><span class="sxs-lookup"><span data-stu-id="04128-286">With TDD you begin each feature by creating a test that verifies the functionality you are about to implement.</span></span> <span data-ttu-id="04128-287">第一次撰寫單元測試有助於確保您清楚瞭解此功能，以及應該如何使用它。</span><span class="sxs-lookup"><span data-stu-id="04128-287">Writing the unit test first helps ensure that you clearly understand the feature and how it is supposed to work.</span></span> <span data-ttu-id="04128-288">只有在撰寫測試之後（而且您已驗證失敗）之後，才會執行測試所驗證的實際功能。</span><span class="sxs-lookup"><span data-stu-id="04128-288">Only after the test is written (and you have verified that it fails) do you then implement the actual functionality the test verifies.</span></span> <span data-ttu-id="04128-289">因為您已經花時間思考此功能應如何運用的使用案例，所以您將會進一步瞭解需求和其最佳執行方式。</span><span class="sxs-lookup"><span data-stu-id="04128-289">Because you've already spent time thinking about the use case of how the feature is supposed to work, you will have a better understanding of the requirements and how best to implement them.</span></span> <span data-ttu-id="04128-290">完成執行時，您可以重新執行測試，並立即取得此功能是否正常運作的意見反應。</span><span class="sxs-lookup"><span data-stu-id="04128-290">When you are done with the implementation you can re-run the test – and get immediate feedback as to whether the feature works correctly.</span></span> <span data-ttu-id="04128-291">我們將在第10章討論 TDD。</span><span class="sxs-lookup"><span data-stu-id="04128-291">We'll cover TDD more in Chapter 10.</span></span>

### <a name="next-step"></a><span data-ttu-id="04128-292">後續步驟</span><span class="sxs-lookup"><span data-stu-id="04128-292">Next Step</span></span>

<span data-ttu-id="04128-293">最後總結批註。</span><span class="sxs-lookup"><span data-stu-id="04128-293">Some final wrap up comments.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="04128-294">[上一頁](use-ajax-to-implement-mapping-scenarios.md)
> [下一頁](nerddinner-wrap-up.md)</span><span class="sxs-lookup"><span data-stu-id="04128-294">[Previous](use-ajax-to-implement-mapping-scenarios.md)
[Next](nerddinner-wrap-up.md)</span></span>
