---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: ASP.NET Web Pages 簡介-HTML 表單基本概念 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程說明如何建立輸入表單，以及如何在使用 ASP.NET Web Pages （Razor）時處理使用者輸入的基本概念。 現在您已經 。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: f57661077ec3bb13f3d4ec41b130bda4d2fb9070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574281"
---
# <a name="introducing-aspnet-web-pages---html-form-basics"></a><span data-ttu-id="3d237-104">ASP.NET Web Pages 簡介-HTML 表單基本概念</span><span class="sxs-lookup"><span data-stu-id="3d237-104">Introducing ASP.NET Web Pages - HTML Form Basics</span></span>

<span data-ttu-id="3d237-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3d237-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3d237-106">本教學課程說明如何建立輸入表單，以及如何在使用 ASP.NET Web Pages （Razor）時處理使用者輸入的基本概念。</span><span class="sxs-lookup"><span data-stu-id="3d237-106">This tutorial shows you the basics of how to create an input form and how to handle the user's input when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="3d237-107">現在您已經有資料庫，您將會使用表單技能，讓使用者能夠在資料庫中尋找特定電影。</span><span class="sxs-lookup"><span data-stu-id="3d237-107">And now that you've got a database, you'll use your form skills to let users find specific movies in the database.</span></span> <span data-ttu-id="3d237-108">它假設您已透過[使用 ASP.NET Web Pages 來顯示資料的簡介來](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data)完成此系列。</span><span class="sxs-lookup"><span data-stu-id="3d237-108">It assumes you have completed the series through [Introduction to Displaying Data Using ASP.NET Web Pages](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data).</span></span>
> 
> <span data-ttu-id="3d237-109">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="3d237-109">What you'll learn:</span></span>
> 
> - <span data-ttu-id="3d237-110">如何使用標準 HTML 元素建立表單。</span><span class="sxs-lookup"><span data-stu-id="3d237-110">How to create a form by using standard HTML elements.</span></span>
> - <span data-ttu-id="3d237-111">如何讀取表單中的使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="3d237-111">How to read the user's input in a form.</span></span>
> - <span data-ttu-id="3d237-112">如何使用使用者所提供的搜尋詞彙，建立選擇性地取得資料的 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="3d237-112">How to create a SQL query that selectively gets data by using a search term that the user supplies.</span></span>
> - <span data-ttu-id="3d237-113">如何讓頁面中的欄位「記住」使用者輸入的內容。</span><span class="sxs-lookup"><span data-stu-id="3d237-113">How to have fields in the page "remember" what the user entered.</span></span>
>   
> 
> <span data-ttu-id="3d237-114">討論的功能/技術：</span><span class="sxs-lookup"><span data-stu-id="3d237-114">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="3d237-115">`Request` 物件。</span><span class="sxs-lookup"><span data-stu-id="3d237-115">The `Request` object.</span></span>
> - <span data-ttu-id="3d237-116">SQL `Where` 子句。</span><span class="sxs-lookup"><span data-stu-id="3d237-116">The SQL `Where` clause.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="3d237-117">您要建置的內容</span><span class="sxs-lookup"><span data-stu-id="3d237-117">What You'll Build</span></span>

<span data-ttu-id="3d237-118">在上一個教學課程中，您已建立資料庫，並在其中加入資料，然後使用 `WebGrid` helper 來顯示資料。</span><span class="sxs-lookup"><span data-stu-id="3d237-118">In the previous tutorial, you created a database, added data to it, and then used the `WebGrid` helper to display the data.</span></span> <span data-ttu-id="3d237-119">在本教學課程中，您將新增搜尋方塊，讓您尋找特定類型的電影，或其標題包含您輸入的任何文字。</span><span class="sxs-lookup"><span data-stu-id="3d237-119">In this tutorial, you'll add a search box that lets you find movies of a specific genre or whose title contains whatever word you enter.</span></span> <span data-ttu-id="3d237-120">（例如，您可以找到內容類型為「動作」或其標題包含「Harry」或「艾德」）的所有電影。</span><span class="sxs-lookup"><span data-stu-id="3d237-120">(For example, you'll be able to find all movies whose genre is "Action" or whose title contains "Harry" or "Adventure.")</span></span>

<span data-ttu-id="3d237-121">當您完成本教學課程時，您將會有如下的頁面：</span><span class="sxs-lookup"><span data-stu-id="3d237-121">When you're done with this tutorial, you'll have a page like this one:</span></span>

![具有內容類型和標題搜尋的電影頁面](form-basics/_static/image1.png)

<span data-ttu-id="3d237-123">頁面的清單部分與上一個教學課程 &mdash; 方格中的相同。</span><span class="sxs-lookup"><span data-stu-id="3d237-123">The listing part of the page is the same as in the last tutorial &mdash; a grid.</span></span> <span data-ttu-id="3d237-124">差別在於方格只會顯示您搜尋的電影。</span><span class="sxs-lookup"><span data-stu-id="3d237-124">The difference will be that the grid will show only the movies that you searched for.</span></span>

## <a name="about-html-forms"></a><span data-ttu-id="3d237-125">關於 HTML 表單</span><span class="sxs-lookup"><span data-stu-id="3d237-125">About HTML Forms</span></span>

<span data-ttu-id="3d237-126">（如果您有建立 HTML 表單的經驗，以及 `GET` 和 `POST`之間的差異，您可以略過本節）。</span><span class="sxs-lookup"><span data-stu-id="3d237-126">(If you've got experience with creating HTML forms and with the difference between `GET` and `POST`, you can skip this section.)</span></span>

<span data-ttu-id="3d237-127">表單具有使用者輸入元素 &mdash; 文字方塊、按鈕、選項按鈕、核取方塊、下拉式清單等。</span><span class="sxs-lookup"><span data-stu-id="3d237-127">A form has user input elements &mdash; text boxes, buttons, radio buttons, check boxes, drop-down lists, and so on.</span></span> <span data-ttu-id="3d237-128">使用者會填入這些控制項或進行選取，然後按一下按鈕來提交表單。</span><span class="sxs-lookup"><span data-stu-id="3d237-128">Users fill in these controls or make selections and then submit the form by clicking a button.</span></span>

<span data-ttu-id="3d237-129">這個範例會說明表單的基本 HTML 語法：</span><span class="sxs-lookup"><span data-stu-id="3d237-129">The basic HTML syntax of a form is illustrated by this example:</span></span>

[!code-html[Main](form-basics/samples/sample1.html)]

<span data-ttu-id="3d237-130">當此標記在頁面中執行時，它會建立一個簡單的表單，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="3d237-130">When this markup runs in a page, it creates a simple form that looks like this illustration:</span></span>

![在瀏覽器中呈現的基本 HTML 表單](form-basics/_static/image2.png)

<span data-ttu-id="3d237-132">`<form>` 元素會括住要提交的 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="3d237-132">The `<form>` element encloses HTML elements to be submitted.</span></span> <span data-ttu-id="3d237-133">（容易犯的錯誤是將專案新增至頁面，但忘了將它們放在 `<form>` 元素中。</span><span class="sxs-lookup"><span data-stu-id="3d237-133">(An easy mistake to make is to add elements to the page but then forget to put them inside a `<form>` element.</span></span> <span data-ttu-id="3d237-134">在此情況下，並不會提交任何內容）。`method` 屬性會告訴瀏覽器如何提交使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="3d237-134">In that case, nothing is submitted.) The `method` attribute tells the browser how to submit the user input.</span></span> <span data-ttu-id="3d237-135">如果您要在伺服器上執行更新，請將此設定為 `post`，如果您只是從伺服器提取資料，則會 `get`。</span><span class="sxs-lookup"><span data-stu-id="3d237-135">You set this to `post` if you're performing an update on the server or to `get` if you're just fetching data from the server.</span></span>

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> <span data-ttu-id="3d237-136">**GET、POST 和 HTTP 動詞安全**</span><span class="sxs-lookup"><span data-stu-id="3d237-136">**GET, POST, and HTTP Verb Safety**</span></span>
> 
> <span data-ttu-id="3d237-137">HTTP 是瀏覽器和伺服器用來交換資訊的通訊協定，在其基本作業中很簡單。</span><span class="sxs-lookup"><span data-stu-id="3d237-137">HTTP, the protocol that browsers and servers use to exchange information, is remarkably simple in its basic operations.</span></span> <span data-ttu-id="3d237-138">瀏覽器只會使用幾個動詞來對伺服器提出要求。</span><span class="sxs-lookup"><span data-stu-id="3d237-138">Browsers use only a few verbs to make requests to servers.</span></span> <span data-ttu-id="3d237-139">當您撰寫 web 的程式碼時，瞭解這些動詞以及瀏覽器和伺服器如何使用它們會很有説明。</span><span class="sxs-lookup"><span data-stu-id="3d237-139">When you write code for the web, it's helpful to understand these verbs and how the browser and server use them.</span></span> <span data-ttu-id="3d237-140">遠低於最常使用的動詞：</span><span class="sxs-lookup"><span data-stu-id="3d237-140">Far and away the most commonly used verbs are these:</span></span>
> 
> - <span data-ttu-id="3d237-141">`GET`</span><span class="sxs-lookup"><span data-stu-id="3d237-141">`GET`.</span></span> <span data-ttu-id="3d237-142">瀏覽器會使用這個動詞命令從伺服器提取內容。</span><span class="sxs-lookup"><span data-stu-id="3d237-142">The browser uses this verb to fetch something from the server.</span></span> <span data-ttu-id="3d237-143">例如，當您在瀏覽器中輸入 URL 時，瀏覽器會執行 `GET` 作業來要求您想要的頁面。</span><span class="sxs-lookup"><span data-stu-id="3d237-143">For example, when you type a URL into your browser, the browser performs a `GET` operation to request the page you want.</span></span> <span data-ttu-id="3d237-144">如果頁面包含圖形，瀏覽器會執行其他 `GET` 作業來取得影像。</span><span class="sxs-lookup"><span data-stu-id="3d237-144">If the page includes graphics, the browser performs additional `GET` operations to get the images.</span></span> <span data-ttu-id="3d237-145">如果 `GET` 作業必須將資訊傳遞給伺服器，則會在查詢字串中將資訊當做 URL 的一部分傳遞。</span><span class="sxs-lookup"><span data-stu-id="3d237-145">If the `GET` operation has to pass information to the server, the information is passed as part of the URL in the query string.</span></span>
> - <span data-ttu-id="3d237-146">`POST`</span><span class="sxs-lookup"><span data-stu-id="3d237-146">`POST`.</span></span> <span data-ttu-id="3d237-147">瀏覽器會傳送 `POST` 要求，以便提交要在伺服器上新增或變更的資料。</span><span class="sxs-lookup"><span data-stu-id="3d237-147">The browser sends a `POST` request in order to submit data to be added or changed on the server.</span></span> <span data-ttu-id="3d237-148">例如，`POST` 指令動詞是用來在資料庫中建立記錄，或變更現有的記錄。</span><span class="sxs-lookup"><span data-stu-id="3d237-148">For example, the `POST` verb is used to create records in a database or change existing ones.</span></span> <span data-ttu-id="3d237-149">在大部分的情況下，當您填寫表單並按一下 [提交] 按鈕時，瀏覽器會執行 `POST` 作業。</span><span class="sxs-lookup"><span data-stu-id="3d237-149">Most of the time, when you fill in a form and click the submit button, the browser performs a `POST` operation.</span></span> <span data-ttu-id="3d237-150">在 `POST` 作業中，傳遞至伺服器的資料會在頁面的主體中。</span><span class="sxs-lookup"><span data-stu-id="3d237-150">In a `POST` operation, the data being passed to the server is in the body of the page.</span></span>
> 
> <span data-ttu-id="3d237-151">這些動詞的重要差異在於，`GET` 作業不應該變更伺服器上的任何專案，或是以稍微更抽象的方式來放置，`GET` 作業不會導致伺服器上的狀態變更。</span><span class="sxs-lookup"><span data-stu-id="3d237-151">An important distinction between these verbs is that a `GET` operation is not supposed to change anything on the server — or to put it in a slightly more abstract way, a `GET` operation does not result in a change in state on the server.</span></span> <span data-ttu-id="3d237-152">您可以視需要在相同的資源上執行 `GET` 作業，而這些資源不會變更。</span><span class="sxs-lookup"><span data-stu-id="3d237-152">You can perform a `GET` operation on the same resources as many times as you like, and those resources don't change.</span></span> <span data-ttu-id="3d237-153">（`GET` 作業通常稱為「安全」，或使用技術術語，其為*等冪*）。相反地，在每次執行作業時，`POST` 要求都會變更伺服器上的某些專案。</span><span class="sxs-lookup"><span data-stu-id="3d237-153">(A `GET` operation is often said to be "safe," or to use a technical term, is *idempotent*.) In contrast, of course, a `POST` request changes something on the server each time you perform the operation.</span></span>
> 
> <span data-ttu-id="3d237-154">有兩個範例將有助於說明這種區別。</span><span class="sxs-lookup"><span data-stu-id="3d237-154">Two examples will help illustrate this distinction.</span></span> <span data-ttu-id="3d237-155">當您使用 Bing 或 Google 之類的引擎執行搜尋時，您會填入包含一個文字方塊的表單，然後按一下 [搜尋] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3d237-155">When you perform a search using an engine like Bing or Google, you fill in a form that consists of one text box, and then you click the search button.</span></span> <span data-ttu-id="3d237-156">瀏覽器會執行 `GET` 作業，並將您輸入的值當做 URL 的一部分來傳遞。</span><span class="sxs-lookup"><span data-stu-id="3d237-156">The browser performs a `GET` operation, with the value you entered into the box passed as part of the URL.</span></span> <span data-ttu-id="3d237-157">針對這種類型的表單使用 `GET` 作業是正常的，因為搜尋作業不會變更伺服器上的任何資源，而只會提取資訊。</span><span class="sxs-lookup"><span data-stu-id="3d237-157">Using a `GET` operation for this type of form is fine, because a search operation doesn't change any resources on the server, it just fetches information.</span></span>
> 
> <span data-ttu-id="3d237-158">現在請考慮在線上排序某個專案的程式。</span><span class="sxs-lookup"><span data-stu-id="3d237-158">Now consider the process of ordering something online.</span></span> <span data-ttu-id="3d237-159">填寫訂單詳細資料，然後按一下 [提交] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3d237-159">You fill in the order details and then click the submit button.</span></span> <span data-ttu-id="3d237-160">這項作業將會是 `POST` 的要求，因為此作業會導致伺服器上的變更，例如新的訂單記錄、帳戶資訊的變更，以及可能有其他許多變更。</span><span class="sxs-lookup"><span data-stu-id="3d237-160">This operation will be a `POST` request, because the operation will result in changes on the server, such as a new order record, a change in your account information, and perhaps many other changes.</span></span> <span data-ttu-id="3d237-161">不同于 `GET` 作業，您無法重複您的 `POST` 要求，如果您這麼做，則每次重新提交要求時，就會在伺服器上產生新的訂單。</span><span class="sxs-lookup"><span data-stu-id="3d237-161">Unlike the `GET` operation, you cannot repeat your `POST` request — if you did, each time you resubmitted the request, you'd generate a new order on the server.</span></span> <span data-ttu-id="3d237-162">（在這種情況下，網站通常會警告您不要再按一次 [提交] 按鈕，或會停用 [提交] 按鈕，讓您不會不小心重新提交表單。）</span><span class="sxs-lookup"><span data-stu-id="3d237-162">(In cases like this, websites will often warn you not to click a submit button more than once, or will disable the submit button so that you don't resubmit the form accidentally.)</span></span>
> 
> <span data-ttu-id="3d237-163">在本教學課程的過程中，您將使用 `GET` 作業和 `POST` 操作，以使用 HTML 表單。</span><span class="sxs-lookup"><span data-stu-id="3d237-163">In the course of this tutorial, you'll use both a `GET` operation and a `POST` operation to work with HTML forms.</span></span> <span data-ttu-id="3d237-164">我們將在每個案例中說明您使用的動詞為何是適當的。</span><span class="sxs-lookup"><span data-stu-id="3d237-164">We'll explain in each case why the verb you use is the appropriate one.</span></span>
> 
> <span data-ttu-id="3d237-165">（若要深入瞭解 HTTP 指令動詞，請參閱 W3C 網站上的[方法定義](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)一文）。</span><span class="sxs-lookup"><span data-stu-id="3d237-165">(To learn more about HTTP verbs, see the [Method Definitions](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) article on the W3C site.)</span></span>

<span data-ttu-id="3d237-166">大部分的使用者輸入元素都是 HTML `<input>` 元素。</span><span class="sxs-lookup"><span data-stu-id="3d237-166">Most user input elements are HTML `<input>` elements.</span></span> <span data-ttu-id="3d237-167">它們看起來像 `<input type="type" name="name">,`，其中*type*表示您想要的使用者輸入控制項類型。</span><span class="sxs-lookup"><span data-stu-id="3d237-167">They look like `<input type="type" name="name">,` where *type* indicates the kind of user input control you want.</span></span> <span data-ttu-id="3d237-168">這些元素是常見的專案：</span><span class="sxs-lookup"><span data-stu-id="3d237-168">These elements are the common ones:</span></span>

- <span data-ttu-id="3d237-169">文字方塊： `<input type="text">`</span><span class="sxs-lookup"><span data-stu-id="3d237-169">Text box: `<input type="text">`</span></span>
- <span data-ttu-id="3d237-170">核取方塊： `<input type="check">`</span><span class="sxs-lookup"><span data-stu-id="3d237-170">Check box: `<input type="check">`</span></span>
- <span data-ttu-id="3d237-171">選項按鈕： `<input type="radio">`</span><span class="sxs-lookup"><span data-stu-id="3d237-171">Radio button: `<input type="radio">`</span></span>
- <span data-ttu-id="3d237-172">按鈕： `<input type="button">`</span><span class="sxs-lookup"><span data-stu-id="3d237-172">Button: `<input type="button">`</span></span>
- <span data-ttu-id="3d237-173">提交按鈕： `<input type="submit">`</span><span class="sxs-lookup"><span data-stu-id="3d237-173">Submit button: `<input type="submit">`</span></span>

<span data-ttu-id="3d237-174">您也可以使用 `<textarea>` 元素來建立多行文字方塊和 `<select>` 元素，以建立下拉式清單或可滾動清單。</span><span class="sxs-lookup"><span data-stu-id="3d237-174">You can also use the `<textarea>` element to create a multiline text box and the `<select>` element to create a drop-down list or scrollable list.</span></span> <span data-ttu-id="3d237-175">（如需 HTML 表單元素的詳細資訊，請參閱 W3Schools 網站上的[Html 表單和輸入](http://www.w3schools.com/html/html_forms.asp)。）</span><span class="sxs-lookup"><span data-stu-id="3d237-175">(For more about HTML form elements, see [HTML Forms and Input](http://www.w3schools.com/html/html_forms.asp) on the W3Schools site.)</span></span>

<span data-ttu-id="3d237-176">`name` 屬性非常重要，因為名稱是您稍後將會取得元素值的方式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="3d237-176">The `name` attribute is very important, because the name is how you'll get the value of the element later, as you'll see shortly.</span></span>

<span data-ttu-id="3d237-177">有趣的是，網頁開發人員對使用者的輸入做了什麼。</span><span class="sxs-lookup"><span data-stu-id="3d237-177">The interesting part is what you, the page developer, do with the user's input.</span></span> <span data-ttu-id="3d237-178">沒有與這些元素相關聯的內建行為。</span><span class="sxs-lookup"><span data-stu-id="3d237-178">There's no built-in behavior associated with these elements.</span></span> <span data-ttu-id="3d237-179">相反地，您必須取得使用者已輸入或選取的值，並對它們執行一些動作。</span><span class="sxs-lookup"><span data-stu-id="3d237-179">Instead, you have to get the values that the user has entered or selected and do something with them.</span></span> <span data-ttu-id="3d237-180">這就是您將在本教學課程中學習到的內容。</span><span class="sxs-lookup"><span data-stu-id="3d237-180">That's what you'll learn in this tutorial.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="3d237-181">**HTML5 和輸入表單**</span><span class="sxs-lookup"><span data-stu-id="3d237-181">**HTML5 and Input Forms**</span></span>
> 
> <span data-ttu-id="3d237-182">如您所知，HTML 正在轉換中，而最新版本（HTML5）包含支援更直覺化的方式，讓使用者輸入資訊。</span><span class="sxs-lookup"><span data-stu-id="3d237-182">As you might know, HTML is in transition and the latest version (HTML5) includes support for more intuitive ways for users to enter information.</span></span> <span data-ttu-id="3d237-183">例如，在 HTML5 中，您（網頁開發人員）可以告訴您要使用者輸入日期的頁面。</span><span class="sxs-lookup"><span data-stu-id="3d237-183">For example, in HTML5, you (the page developer) can tell the page that you want the user to enter a date.</span></span> <span data-ttu-id="3d237-184">然後，瀏覽器可以自動顯示行事曆，而不是要求使用者手動輸入日期。</span><span class="sxs-lookup"><span data-stu-id="3d237-184">The browser can then automatically display a calendar rather than requiring the user to enter a date manually.</span></span> <span data-ttu-id="3d237-185">不過，HTML5 是新的，而且所有的瀏覽器目前都不支援。</span><span class="sxs-lookup"><span data-stu-id="3d237-185">However, HTML5 is new and is not supported in all browsers yet.</span></span>
> 
> <span data-ttu-id="3d237-186">ASP.NET Web Pages 支援 HTML5 輸入至使用者瀏覽器的範圍。</span><span class="sxs-lookup"><span data-stu-id="3d237-186">ASP.NET Web Pages supports HTML5 input to the extent that the user's browser does.</span></span> <span data-ttu-id="3d237-187">如需 HTML5 中 `<input>` 元素的新屬性概念，請參閱 W3Schools 網站上的[HTML &lt;輸入&gt; 類型屬性](http://www.w3schools.com/html/html_form_input_types.asp)。</span><span class="sxs-lookup"><span data-stu-id="3d237-187">For an idea of the new attributes for the `<input>` element in HTML5, see [HTML &lt;input&gt; type Attribute](http://www.w3schools.com/html/html_form_input_types.asp) on the W3Schools site.</span></span>

## <a name="creating-the-form"></a><span data-ttu-id="3d237-188">建立表單</span><span class="sxs-lookup"><span data-stu-id="3d237-188">Creating the Form</span></span>

<span data-ttu-id="3d237-189">在 WebMatrix 的 [檔案 **] 工作區**中，開啟 [*電影. cshtml* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="3d237-189">In WebMatrix, in the **Files** workspace, open the *Movies.cshtml* page.</span></span>

<span data-ttu-id="3d237-190">在結尾 `</h1>` 標記之後，以及 `grid.GetHtml` 呼叫的開啟 `<div>` 標記之前，新增下列標記：</span><span class="sxs-lookup"><span data-stu-id="3d237-190">After the closing `</h1>` tag and before the opening `<div>` tag of the `grid.GetHtml` call, add the following markup:</span></span>

[!code-html[Main](form-basics/samples/sample2.html)]

<span data-ttu-id="3d237-191">此標記會建立一個表單，其中包含名為 `searchGenre` 的文字方塊和 [提交] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3d237-191">This markup creates a form that has a text box named `searchGenre` and a submit button.</span></span> <span data-ttu-id="3d237-192">[文字方塊] 和 [提交] 按鈕會括在 `<form>` 元素中，其 `method` 屬性設為 `get`。</span><span class="sxs-lookup"><span data-stu-id="3d237-192">The text box and submit button are enclosed in a `<form>` element whose `method` attribute is set to `get`.</span></span> <span data-ttu-id="3d237-193">（請記住，如果您未將 [文字方塊] 和 [提交] 按鈕放在 `<form>` 專案內，當您按一下按鈕時，將不會提交任何內容）。您會在這裡使用 `GET` 動詞，因為您所建立的表單不會在伺服器上進行任何變更，而只會產生搜尋。</span><span class="sxs-lookup"><span data-stu-id="3d237-193">(Remember that if you don't put the text box and submit button inside a `<form>` element, nothing will be submitted when you click the button.) You use the `GET` verb here because you're creating a form that does not make any changes on the server — it just results in a search.</span></span> <span data-ttu-id="3d237-194">（在上一個教學課程中，您使用了 `post` 方法，這就是您將變更提交至伺服器的方式。</span><span class="sxs-lookup"><span data-stu-id="3d237-194">(In the previous tutorial, you used a `post` method, which is how you submit changes to the server.</span></span> <span data-ttu-id="3d237-195">您會在下一個教學課程中再次看到）。</span><span class="sxs-lookup"><span data-stu-id="3d237-195">You'll see that in the next tutorial again.)</span></span>

<span data-ttu-id="3d237-196">執行頁面。</span><span class="sxs-lookup"><span data-stu-id="3d237-196">Run the page.</span></span> <span data-ttu-id="3d237-197">雖然您尚未定義表單的任何行為，但是您可以查看它看起來的樣子：</span><span class="sxs-lookup"><span data-stu-id="3d237-197">Although you haven't defined any behavior for the form, you can see what it looks like:</span></span>

![具有內容類型搜尋方塊的電影頁面](form-basics/_static/image3.png)

<span data-ttu-id="3d237-199">在文字方塊中輸入值，例如 "喜劇"。</span><span class="sxs-lookup"><span data-stu-id="3d237-199">Enter a value into the text box, like "Comedy."</span></span> <span data-ttu-id="3d237-200">然後按一下 [**搜尋**內容類型]。</span><span class="sxs-lookup"><span data-stu-id="3d237-200">Then click **Search Genre**.</span></span>

<span data-ttu-id="3d237-201">記下頁面的 URL。</span><span class="sxs-lookup"><span data-stu-id="3d237-201">Take note of the URL of the page.</span></span> <span data-ttu-id="3d237-202">因為您將 `<form>` 專案的 `method` 屬性設定為 [`get`]，所以您輸入的值現在會是 URL 中查詢字串的一部分，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3d237-202">Because you set the `<form>` element's `method` attribute to `get`, the value you entered is now part of the query string in the URL, like this:</span></span>

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a><span data-ttu-id="3d237-203">讀取表單值</span><span class="sxs-lookup"><span data-stu-id="3d237-203">Reading Form Values</span></span>

<span data-ttu-id="3d237-204">此頁面已經包含一些程式碼，可取得資料庫資料並將結果顯示在方格中。</span><span class="sxs-lookup"><span data-stu-id="3d237-204">The page already contains some code that gets database data and displays the results in a grid.</span></span> <span data-ttu-id="3d237-205">現在您必須新增一些程式碼來讀取文字方塊的值，以便執行包含搜尋詞彙的 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="3d237-205">Now you have to add some code that reads the value of the text box so you can run a SQL query that includes the search term.</span></span>

<span data-ttu-id="3d237-206">因為您將表單的方法設定為 `get`，所以您可以使用如下所示的程式碼，來讀取在文字方塊中輸入的值：</span><span class="sxs-lookup"><span data-stu-id="3d237-206">Because you set the form's method to `get`, you can read the value that was entered into the text box by using code like the following:</span></span>

`var searchTerm = Request.QueryString["searchGenre"];`

<span data-ttu-id="3d237-207">`Request.QueryString` 物件（`Request` 物件的 `QueryString` 屬性）包含已提交做為 `GET` 作業一部分的元素值。</span><span class="sxs-lookup"><span data-stu-id="3d237-207">The `Request.QueryString` object (the `QueryString` property of the `Request` object) includes the values of elements that were submitted as part of the `GET` operation.</span></span> <span data-ttu-id="3d237-208">`Request.QueryString` 屬性包含在表單中提交之值的*集合*（清單）。</span><span class="sxs-lookup"><span data-stu-id="3d237-208">The `Request.QueryString` property contains a *collection* (a list) of the values that are submitted in the form.</span></span> <span data-ttu-id="3d237-209">若要取得任何個別值，請指定您想要的元素名稱。</span><span class="sxs-lookup"><span data-stu-id="3d237-209">To get any individual value, you specify the name of the element that you want.</span></span> <span data-ttu-id="3d237-210">這就是為什麼在建立文字方塊的 `<input>` 元素（`searchTerm`）上必須有 `name` 屬性的原因。</span><span class="sxs-lookup"><span data-stu-id="3d237-210">That's why you have to have a `name` attribute on the `<input>` element (`searchTerm`) that creates the text box.</span></span> <span data-ttu-id="3d237-211">（如需 `Request` 物件的詳細資訊，請參閱稍後的[邊欄](#BKMK_TheRequestObject)）。</span><span class="sxs-lookup"><span data-stu-id="3d237-211">(For more about the `Request` object, see the [sidebar](#BKMK_TheRequestObject) later.)</span></span>

<span data-ttu-id="3d237-212">這很簡單，足以讀取文字方塊的值。</span><span class="sxs-lookup"><span data-stu-id="3d237-212">It's simple enough to read the value of the text box.</span></span> <span data-ttu-id="3d237-213">但是，如果使用者沒有在文字方塊中輸入任何內容，但按下 [**搜尋**]，則您可以忽略該點擊，因為沒有任何可搜尋的專案。</span><span class="sxs-lookup"><span data-stu-id="3d237-213">But if the user didn't enter anything at all in the text box but clicked **Search** anyway, you can ignore that click, since there's nothing to search.</span></span>

<span data-ttu-id="3d237-214">下列程式碼範例顯示如何執行這些條件。</span><span class="sxs-lookup"><span data-stu-id="3d237-214">The following code is an example that shows how to implement these conditions.</span></span> <span data-ttu-id="3d237-215">（您還不需要新增此程式碼; 您稍後會這麼做）。</span><span class="sxs-lookup"><span data-stu-id="3d237-215">(You don't have to add this code yet; you'll do that in a moment.)</span></span>

[!code-csharp[Main](form-basics/samples/sample3.cs)]

<span data-ttu-id="3d237-216">此測試會以這種方式細分：</span><span class="sxs-lookup"><span data-stu-id="3d237-216">The test breaks down in this way:</span></span>

- <span data-ttu-id="3d237-217">取得 `Request.QueryString["searchGenre"]`的值，也就是輸入至名為 `searchGenre`之 `<input>` 元素的值。</span><span class="sxs-lookup"><span data-stu-id="3d237-217">Get the value of `Request.QueryString["searchGenre"]`, namely the value that was entered into the `<input>` element named `searchGenre`.</span></span>
- <span data-ttu-id="3d237-218">使用 `IsEmpty` 方法，找出是否為空的。</span><span class="sxs-lookup"><span data-stu-id="3d237-218">Find out if it's empty by using the `IsEmpty` method.</span></span> <span data-ttu-id="3d237-219">這個方法是判斷某個專案（例如，表單元素）是否包含值的標準方式。</span><span class="sxs-lookup"><span data-stu-id="3d237-219">This method is the standard way to determine whether something (for example, a form element) contains a value.</span></span> <span data-ttu-id="3d237-220">但事實上，您只在意它*不*是空的，因此 。</span><span class="sxs-lookup"><span data-stu-id="3d237-220">But really, you care only if it's *not* empty, therefore ...</span></span>
- <span data-ttu-id="3d237-221">將 `!` 運算子加入 `IsEmpty` 測試前面。</span><span class="sxs-lookup"><span data-stu-id="3d237-221">Add the `!` operator in front of the `IsEmpty` test.</span></span> <span data-ttu-id="3d237-222">（`!` 運算子表示邏輯 NOT）。</span><span class="sxs-lookup"><span data-stu-id="3d237-222">(The `!` operator means logical NOT).</span></span>

<span data-ttu-id="3d237-223">在純英文中，整個 `if` 條件會轉譯成下列專案：*如果表單的 searchGenre 元素不是空的，則 ...*</span><span class="sxs-lookup"><span data-stu-id="3d237-223">In plain English, the entire `if` condition translates into the following: *If the form's searchGenre element is not empty, then ...*</span></span>

<span data-ttu-id="3d237-224">此區塊會設定用來建立使用搜尋詞彙之查詢的階段。</span><span class="sxs-lookup"><span data-stu-id="3d237-224">This block sets the stage for creating a query that uses the search term.</span></span> <span data-ttu-id="3d237-225">您將在下一節中執行該動作。</span><span class="sxs-lookup"><span data-stu-id="3d237-225">You'll do that in the next section.</span></span>

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> <span data-ttu-id="3d237-226">**Request 物件**</span><span class="sxs-lookup"><span data-stu-id="3d237-226">**The Request Object**</span></span>
> 
> <span data-ttu-id="3d237-227">`Request` 物件包含當要求或提交頁面時，瀏覽器傳送到您應用程式的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="3d237-227">The `Request` object contains all the information that the browser sends to your application when a page is requested or submitted.</span></span> <span data-ttu-id="3d237-228">此物件包含使用者提供的任何資訊，例如文字方塊值或要上傳的檔案。</span><span class="sxs-lookup"><span data-stu-id="3d237-228">This object includes any information that the user provides, like text box values or a file to upload.</span></span> <span data-ttu-id="3d237-229">它也包括各種額外的資訊，例如 cookie、URL 查詢字串中的值（如果有的話）、正在執行之網頁的檔案路徑、使用者所使用的瀏覽器類型，以及在瀏覽器中設定的語言清單還有更多。</span><span class="sxs-lookup"><span data-stu-id="3d237-229">It also includes all sorts of additional information, like cookies, values in the URL query string (if any), the file path of the page that is running, the type of browser that the user is using, the list of languages that are set in the browser, and much more.</span></span>
> 
> <span data-ttu-id="3d237-230">`Request` 物件是值的*集合*（清單）。</span><span class="sxs-lookup"><span data-stu-id="3d237-230">The `Request` object is a *collection* (list) of values.</span></span> <span data-ttu-id="3d237-231">您可以藉由指定名稱，從集合中取得個別的值：</span><span class="sxs-lookup"><span data-stu-id="3d237-231">You get an individual value out of the collection by specifying its name:</span></span>
> 
> `var someValue = Request["name"];`
> 
> <span data-ttu-id="3d237-232">`Request` 物件實際上會公開數個子集。</span><span class="sxs-lookup"><span data-stu-id="3d237-232">The `Request` object actually exposes several subsets.</span></span> <span data-ttu-id="3d237-233">例如:</span><span class="sxs-lookup"><span data-stu-id="3d237-233">For example:</span></span>
> 
> - <span data-ttu-id="3d237-234">如果要求是 `POST` 要求，`Request.Form` 會從已提交的 `<form>` 元素內的元素提供值。</span><span class="sxs-lookup"><span data-stu-id="3d237-234">`Request.Form` gives you values from elements inside the submitted `<form>` element if the request is a `POST` request.</span></span>
> - <span data-ttu-id="3d237-235">`Request.QueryString` 只會為您提供 URL 的查詢字串中的值。</span><span class="sxs-lookup"><span data-stu-id="3d237-235">`Request.QueryString` gives you just the values in the URL's query string.</span></span> <span data-ttu-id="3d237-236">（在類似 `http://mysite/myapp/page?searchGenre=action&page=2`的 URL 中，URL 的 `?searchGenre=action&page=2` 區段是查詢字串）。</span><span class="sxs-lookup"><span data-stu-id="3d237-236">(In a URL like `http://mysite/myapp/page?searchGenre=action&page=2`, the `?searchGenre=action&page=2` section of the URL is the query string.)</span></span>
> - <span data-ttu-id="3d237-237">`Request.Cookies` 集合可讓您存取瀏覽器已傳送的 cookie。</span><span class="sxs-lookup"><span data-stu-id="3d237-237">`Request.Cookies` collection gives you access to cookies that the browser has sent.</span></span>
> 
> <span data-ttu-id="3d237-238">若要取得您知道在已提交表單中的值，您可以使用 `Request["name"]`。</span><span class="sxs-lookup"><span data-stu-id="3d237-238">To get a value that you know is in the submitted form, you can use `Request["name"]`.</span></span> <span data-ttu-id="3d237-239">或者，您可以使用更具體的版本 `Request.Form["name"]` （適用于 `POST` 要求）或 `Request.QueryString["name"]` （適用于 `GET` 要求）。</span><span class="sxs-lookup"><span data-stu-id="3d237-239">Alternatively, you can use the more specific versions `Request.Form["name"]` (for `POST` requests) or `Request.QueryString["name"]` (for `GET` requests).</span></span> <span data-ttu-id="3d237-240">當然， *name*是要取得的專案名稱。</span><span class="sxs-lookup"><span data-stu-id="3d237-240">Of course, *name* is the name of the item to get.</span></span>
> 
> <span data-ttu-id="3d237-241">您想要取得的專案名稱在您所使用的集合中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="3d237-241">The name of the item you want to get has to be unique within the collection you're using.</span></span> <span data-ttu-id="3d237-242">這就是為什麼 `Request` 物件提供 `Request.Form` 和 `Request.QueryString`這類子集的原因。</span><span class="sxs-lookup"><span data-stu-id="3d237-242">That's why the `Request` object provides the subsets like `Request.Form` and `Request.QueryString`.</span></span> <span data-ttu-id="3d237-243">假設您的頁面包含名為 `userName` 的 form 元素，而且*也*包含名為 `userName`的 cookie。</span><span class="sxs-lookup"><span data-stu-id="3d237-243">Suppose that your page contains a form element named `userName` and *also* contains a cookie named `userName`.</span></span> <span data-ttu-id="3d237-244">如果您取得 `Request["userName"]`，不論您想要表單值或 cookie，都是不明確的。</span><span class="sxs-lookup"><span data-stu-id="3d237-244">If you get `Request["userName"]`, it's ambiguous whether you want the form value or the cookie.</span></span> <span data-ttu-id="3d237-245">不過，如果您取得 `Request.Form["userName"]` 或 `Request.Cookie["userName"]`，您就會明確瞭解要取得哪個值。</span><span class="sxs-lookup"><span data-stu-id="3d237-245">However, if you get `Request.Form["userName"]` or `Request.Cookie["userName"]`, you're being explicit about which value to get.</span></span>
> 
> <span data-ttu-id="3d237-246">最好的作法是使用您感興趣的 `Request` 子集，例如 `Request.Form` 或 `Request.QueryString`。</span><span class="sxs-lookup"><span data-stu-id="3d237-246">It's a good practice to be specific and use the subset of `Request` that you're interested in, like `Request.Form` or `Request.QueryString`.</span></span> <span data-ttu-id="3d237-247">針對您在本教學課程中建立的簡單頁面，它可能不會真正有任何差異。</span><span class="sxs-lookup"><span data-stu-id="3d237-247">For the simple pages that you're creating in this tutorial, it probably doesn't really make any difference.</span></span> <span data-ttu-id="3d237-248">不過，當您建立更複雜的頁面時，使用明確的版本 `Request.Form` 或 `Request.QueryString` 可以協助您避免頁面包含表單（或多個表單）、cookie、查詢字串值等等時可能發生的問題。</span><span class="sxs-lookup"><span data-stu-id="3d237-248">However, as you create more complex pages, using the explicit version `Request.Form` or `Request.QueryString` can help you avoid problems that can arise when the page contains a form (or multiple forms), cookies, query string values, and so on.</span></span>

## <a name="creating-a-query-by-using-a-search-term"></a><span data-ttu-id="3d237-249">使用搜尋詞彙建立查詢</span><span class="sxs-lookup"><span data-stu-id="3d237-249">Creating a Query by Using a Search Term</span></span>

<span data-ttu-id="3d237-250">既然您已經知道如何取得使用者輸入的搜尋字詞，就可以建立使用它的查詢。</span><span class="sxs-lookup"><span data-stu-id="3d237-250">Now that you know how to get the search term that the user entered, you can create a query that uses it.</span></span> <span data-ttu-id="3d237-251">請記住，若要取得資料庫中的所有電影專案，您會使用類似此語句的 SQL 查詢：</span><span class="sxs-lookup"><span data-stu-id="3d237-251">Remember that to get all the movie items out of the database, you're using a SQL query that looks like this statement:</span></span>

`SELECT * FROM Movies`

<span data-ttu-id="3d237-252">若只要取得特定電影，您就必須使用包含 `Where` 子句的查詢。</span><span class="sxs-lookup"><span data-stu-id="3d237-252">To get only certain movies, you have to use a query that includes a `Where` clause.</span></span> <span data-ttu-id="3d237-253">此子句可讓您設定查詢所傳回之資料列的條件。</span><span class="sxs-lookup"><span data-stu-id="3d237-253">This clause lets you set a condition on which rows are returned by the query.</span></span> <span data-ttu-id="3d237-254">以下為範例：</span><span class="sxs-lookup"><span data-stu-id="3d237-254">Here's an example:</span></span>

`SELECT * FROM Movies WHERE Genre = 'Action'`

<span data-ttu-id="3d237-255">基本格式為 `WHERE column = value`。</span><span class="sxs-lookup"><span data-stu-id="3d237-255">The basic format is `WHERE column = value`.</span></span> <span data-ttu-id="3d237-256">除了 `=`以外，您還可以使用不同的運算子，例如 `>` （大於）、`<` （小於）、`<>` （不等於）、`<=` （小於或等於）等，視您要尋找的內容而定。</span><span class="sxs-lookup"><span data-stu-id="3d237-256">You can use different operators besides just `=`, like `>` (greater than), `<` (less than), `<>` (not equal to), `<=` (less than or equal to), etc., depending on what you're looking for.</span></span>

<span data-ttu-id="3d237-257">如果您想知道，SQL 語句並不區分大小寫 &mdash; `SELECT` 與 `Select` （或甚至 `select`）相同。</span><span class="sxs-lookup"><span data-stu-id="3d237-257">In case you're wondering, SQL statements are not case sensitive &mdash; `SELECT` is the same as `Select` (or even `select`).</span></span> <span data-ttu-id="3d237-258">不過，使用者通常會將 SQL 語句中的關鍵字（例如 `SELECT` 和 `WHERE`）大寫，以便更容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="3d237-258">However, people often capitalize keywords in a SQL statement, like `SELECT` and `WHERE`, to make it easier to read.</span></span>

### <a name="passing-the-search-term-as-a-parameter"></a><span data-ttu-id="3d237-259">傳遞搜尋詞彙做為參數</span><span class="sxs-lookup"><span data-stu-id="3d237-259">Passing the search term as a parameter</span></span>

<span data-ttu-id="3d237-260">搜尋特定的內容類型很容易（`WHERE Genre = 'Action'`），但您想要能夠搜尋使用者輸入的任何類型。</span><span class="sxs-lookup"><span data-stu-id="3d237-260">Searching for a specific genre is easy enough (`WHERE Genre = 'Action'`), but you want to be able to search for any genre that the user enters.</span></span> <span data-ttu-id="3d237-261">若要這麼做，您可以建立 SQL 查詢，其中包含要搜尋之值的預留位置。</span><span class="sxs-lookup"><span data-stu-id="3d237-261">To do that, you create as SQL query that includes a placeholder for the value to search.</span></span> <span data-ttu-id="3d237-262">此命令看起來會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="3d237-262">It will look like this command:</span></span>

`SELECT * FROM Movies WHERE Genre = @0`

<span data-ttu-id="3d237-263">預留位置是後面接著零的 `@` 字元。</span><span class="sxs-lookup"><span data-stu-id="3d237-263">The placeholder is the `@` character followed by zero.</span></span> <span data-ttu-id="3d237-264">您可能會猜到，查詢可以包含多個預留位置，而且它們會命名 `@0`、`@1`、`@2`等等。</span><span class="sxs-lookup"><span data-stu-id="3d237-264">As you might guess, a query can contain multiple placeholders, and they'd be named `@0`, `@1`, `@2`, etc.</span></span>

<span data-ttu-id="3d237-265">若要設定查詢，並實際將值傳遞給它，您可以使用如下所示的程式碼：</span><span class="sxs-lookup"><span data-stu-id="3d237-265">To set up the query and actually pass it the value, you use the code like the following:</span></span>

[!code-sql[Main](form-basics/samples/sample4.sql)]

<span data-ttu-id="3d237-266">這段程式碼與您在方格中顯示資料所做的類似。</span><span class="sxs-lookup"><span data-stu-id="3d237-266">This code is similar to what you've already done to display data in the grid.</span></span> <span data-ttu-id="3d237-267">唯一的差異如下：</span><span class="sxs-lookup"><span data-stu-id="3d237-267">The only differences are:</span></span>

- <span data-ttu-id="3d237-268">查詢包含預留位置（`WHERE Genre = @0"`）。</span><span class="sxs-lookup"><span data-stu-id="3d237-268">The query contains a placeholder (`WHERE Genre = @0"`).</span></span>
- <span data-ttu-id="3d237-269">查詢會放入變數（`selectCommand`）;在之前，您會直接將查詢傳遞給 `db.Query` 方法。</span><span class="sxs-lookup"><span data-stu-id="3d237-269">The query is put into a variable (`selectCommand`); before, you passed the query directly to the `db.Query` method.</span></span>
- <span data-ttu-id="3d237-270">當您呼叫 `db.Query` 方法時，您會同時傳遞查詢和用於預留位置的值。</span><span class="sxs-lookup"><span data-stu-id="3d237-270">When you call the `db.Query` method, you pass both the query and the value to use for the placeholder.</span></span> <span data-ttu-id="3d237-271">（如果查詢有多個預留位置，您會將它們全部當做個別值傳遞給方法）。</span><span class="sxs-lookup"><span data-stu-id="3d237-271">(If the query had multiple placeholders, you'd pass them all as separate values to the method.)</span></span>

<span data-ttu-id="3d237-272">如果您將所有這些元素放在一起，您會取得下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="3d237-272">If you put all these elements together, you get the following code:</span></span>

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="3d237-273">**重要！**</span><span class="sxs-lookup"><span data-stu-id="3d237-273">**Important!**</span></span> <span data-ttu-id="3d237-274">使用預留位置（例如 `@0`）將值傳遞至 SQL 命令對於安全性而言*非常重要*。</span><span class="sxs-lookup"><span data-stu-id="3d237-274">Using placeholders (like `@0`) to pass values to a SQL command is *extremely important* for security.</span></span> <span data-ttu-id="3d237-275">您在這裡看到的方式，加上變數資料的預留位置，是您應該用來建立 SQL 命令的唯一方式。</span><span class="sxs-lookup"><span data-stu-id="3d237-275">The way you see it here, with placeholders for variable data, is the only way you should construct SQL commands.</span></span>
> 
> <span data-ttu-id="3d237-276">絕對不要建立 SQL 語句，方法是將常值文字和您從使用者取得的值放在一起（串連）。</span><span class="sxs-lookup"><span data-stu-id="3d237-276">Never construct a SQL statement by putting together (concatenating) literal text and values you get from the user.</span></span> <span data-ttu-id="3d237-277">將使用者輸入串連到 SQL 語句，會開啟您的網站進入*sql 插入式攻擊*，其中惡意使用者會將值提交至您的頁面，以攻擊您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="3d237-277">Concatenating user input into a SQL statement opens your site to a *SQL injection attack* where a malicious user submits values to your page that hack your database.</span></span> <span data-ttu-id="3d237-278">（您可以在[SQL 插入](https://msdn.microsoft.com/library/ms161953.aspx)MSDN 網站一文中深入瞭解）。</span><span class="sxs-lookup"><span data-stu-id="3d237-278">(You can read more in the article [SQL Injection](https://msdn.microsoft.com/library/ms161953.aspx) the MSDN website.)</span></span>

## <a name="updating-the-movies-page-with-search-code"></a><span data-ttu-id="3d237-279">使用搜尋程式碼更新電影頁面</span><span class="sxs-lookup"><span data-stu-id="3d237-279">Updating the Movies Page with Search Code</span></span>

<span data-ttu-id="3d237-280">現在您可以更新 [*電影*] 檔案中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="3d237-280">Now you can update the code in the *Movies.cshtml* file.</span></span> <span data-ttu-id="3d237-281">若要開始，請使用下列程式碼取代頁面頂端程式碼區塊中的程式碼：</span><span class="sxs-lookup"><span data-stu-id="3d237-281">To begin, replace the code in the code block at the top of the page with this code:</span></span>

[!code-csharp[Main](form-basics/samples/sample6.cs)]

<span data-ttu-id="3d237-282">此處的差異在於，您已將查詢放入 `selectCommand` 變數中，而您將在稍後傳遞給 `db.Query`。</span><span class="sxs-lookup"><span data-stu-id="3d237-282">The difference here is that you've put the query into the `selectCommand` variable, which you'll pass to `db.Query` later.</span></span> <span data-ttu-id="3d237-283">將 SQL 語句放入變數中，可讓您變更語句，這就是執行搜尋時所要執行的動作。</span><span class="sxs-lookup"><span data-stu-id="3d237-283">Putting the SQL statement into a variable lets you change the statement, which is what you'll do to perform the search.</span></span>

<span data-ttu-id="3d237-284">您也已移除這兩行，您將在稍後將它們放回：</span><span class="sxs-lookup"><span data-stu-id="3d237-284">You've also removed these two lines, which you'll put back in later:</span></span>

[!code-csharp[Main](form-basics/samples/sample7.cs)]

<span data-ttu-id="3d237-285">您還不想要執行查詢（也就是呼叫 `db.Query`），而且您也不想要初始化 `WebGrid` helper。</span><span class="sxs-lookup"><span data-stu-id="3d237-285">You don't want to run the query yet (that is, call `db.Query`) and you don't want to initialize the `WebGrid` helper yet either.</span></span> <span data-ttu-id="3d237-286">在您瞭解必須執行的 SQL 語句之後，就會執行這些動作。</span><span class="sxs-lookup"><span data-stu-id="3d237-286">You'll do those things after you've figured out which SQL statement has to run.</span></span>

<span data-ttu-id="3d237-287">在此重寫區塊之後，您可以新增用來處理搜尋的邏輯。</span><span class="sxs-lookup"><span data-stu-id="3d237-287">After this rewritten block, you can add the new logic for handling the search.</span></span> <span data-ttu-id="3d237-288">完成後的程式碼看起來會像下面這樣。</span><span class="sxs-lookup"><span data-stu-id="3d237-288">The completed code will look like the following.</span></span> <span data-ttu-id="3d237-289">更新頁面中的程式碼，使其符合此範例：</span><span class="sxs-lookup"><span data-stu-id="3d237-289">Update the code in your page so it matches this example:</span></span>

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

<span data-ttu-id="3d237-290">此頁面現在的運作方式如下所示。</span><span class="sxs-lookup"><span data-stu-id="3d237-290">The page now works like this.</span></span> <span data-ttu-id="3d237-291">每次執行頁面時，程式碼都會開啟資料庫，而 `selectCommand` 變數會設定為從 `Movies` 資料表取得所有記錄的 SQL 語句。</span><span class="sxs-lookup"><span data-stu-id="3d237-291">Every time the page runs, the code opens the database and the `selectCommand` variable is set to the SQL statement that gets all the records from the `Movies` table.</span></span> <span data-ttu-id="3d237-292">程式碼也會初始化 `searchTerm` 變數。</span><span class="sxs-lookup"><span data-stu-id="3d237-292">The code also initializes the `searchTerm` variable.</span></span>

<span data-ttu-id="3d237-293">不過，如果目前的要求包含 `searchGenre` 元素的值，則程式碼會將 `selectCommand` 設定為不同的查詢，也就是包含 `Where` 子句來搜尋內容類型的查詢。</span><span class="sxs-lookup"><span data-stu-id="3d237-293">However, if the current request includes a value for the `searchGenre` element, the code sets `selectCommand` to a different query — namely, to one that includes the `Where` clause to search for a genre.</span></span> <span data-ttu-id="3d237-294">它也會將 `searchTerm` 設定為搜尋方塊所傳遞的內容（這可能不是任何內容）。</span><span class="sxs-lookup"><span data-stu-id="3d237-294">It also sets `searchTerm` to whatever was passed for the search box (which might be nothing).</span></span>

<span data-ttu-id="3d237-295">不論 `selectCommand`的 SQL 語句為何，程式碼會接著呼叫 `db.Query` 來執行查詢，並將它傳遞至 `searchTerm`中的任何內容。</span><span class="sxs-lookup"><span data-stu-id="3d237-295">Regardless of which SQL statement is in `selectCommand`, the code then calls `db.Query` to run the query, passing it whatever is in `searchTerm`.</span></span> <span data-ttu-id="3d237-296">如果 `searchTerm`中沒有任何東西，這並不重要，因為在這種情況下，沒有任何參數可以將值傳遞給 `selectCommand`。</span><span class="sxs-lookup"><span data-stu-id="3d237-296">If there's nothing in `searchTerm`, it doesn't matter, because in that case there's no parameter to pass the value to `selectCommand` anyway.</span></span>

<span data-ttu-id="3d237-297">最後，程式碼會使用查詢結果來初始化 `WebGrid` helper，就像之前一樣。</span><span class="sxs-lookup"><span data-stu-id="3d237-297">Finally, the code initializes the `WebGrid` helper by using the query results, just like before.</span></span>

<span data-ttu-id="3d237-298">您可以藉由將 SQL 語句和搜尋詞彙放入變數中來看出，您已在程式碼中增加彈性。</span><span class="sxs-lookup"><span data-stu-id="3d237-298">You can see that by putting the SQL statement and the search term into variables, you've added flexibility to the code.</span></span> <span data-ttu-id="3d237-299">如您稍後在本教學課程中所見，您可以使用此基本架構，並持續為不同的搜尋類型新增邏輯。</span><span class="sxs-lookup"><span data-stu-id="3d237-299">As you'll see later in this tutorial, you can use this basic framework and keep adding logic for different types of searches.</span></span>

## <a name="testing-the-search-by-genre-feature"></a><span data-ttu-id="3d237-300">測試依風格搜尋的功能</span><span class="sxs-lookup"><span data-stu-id="3d237-300">Testing the Search-by-Genre Feature</span></span>

<span data-ttu-id="3d237-301">在 WebMatrix 中，執行 [*電影. cshtml* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="3d237-301">In WebMatrix, run the *Movies.cshtml* page.</span></span> <span data-ttu-id="3d237-302">您會看到具有文字類型文字方塊的頁面。</span><span class="sxs-lookup"><span data-stu-id="3d237-302">You see the page with the text box for genre.</span></span>

<span data-ttu-id="3d237-303">輸入您為其中一個測試記錄輸入的內容類型，然後按一下 [**搜尋**]。</span><span class="sxs-lookup"><span data-stu-id="3d237-303">Enter a genre that you've entered for one of your test records, then click **Search**.</span></span> <span data-ttu-id="3d237-304">此時，您只會看到符合該內容類型的電影清單：</span><span class="sxs-lookup"><span data-stu-id="3d237-304">This time you see a listing of just the movies that match that genre:</span></span>

![搜尋內容類型 ' Comedies ' 之後的電影頁面清單](form-basics/_static/image4.png)

<span data-ttu-id="3d237-306">輸入不同的內容類型，然後再搜尋一次。</span><span class="sxs-lookup"><span data-stu-id="3d237-306">Enter a different genre and search again.</span></span> <span data-ttu-id="3d237-307">嘗試使用全部小寫或全部大寫來輸入內容類型，讓您可以看到搜尋不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="3d237-307">Try entering the genre by using all lowercase or all uppercase letters so that you can see that the search is not case sensitive.</span></span>

## <a name="remembering-what-the-user-entered"></a><span data-ttu-id="3d237-308">「記住」使用者輸入的內容</span><span class="sxs-lookup"><span data-stu-id="3d237-308">"Remembering" What the User Entered</span></span>

<span data-ttu-id="3d237-309">您可能已經注意到在輸入內容類型，然後按一下 [**搜尋**內容類型] 之後，就會看到該內容類型的清單。</span><span class="sxs-lookup"><span data-stu-id="3d237-309">You might have noticed that after you entered a genre and clicked **Search Genre**, you saw a listing for that genre.</span></span> <span data-ttu-id="3d237-310">不過，[搜尋] 文字方塊是空的 &mdash; 換句話說，這並不記得您輸入的內容。</span><span class="sxs-lookup"><span data-stu-id="3d237-310">However, the search text box was empty &mdash; in other words, it didn't remember what you'd entered.</span></span>

<span data-ttu-id="3d237-311">請務必瞭解為何會發生這種行為。</span><span class="sxs-lookup"><span data-stu-id="3d237-311">It's important to understand why this behavior occurs.</span></span> <span data-ttu-id="3d237-312">當您提交頁面時，瀏覽器會將要求傳送至 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="3d237-312">When you submit a page, the browser sends a request to the web server.</span></span> <span data-ttu-id="3d237-313">當 ASP.NET 取得要求時，它會建立頁面的全新實例、執行其中的程式碼，然後再次將頁面轉譯至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="3d237-313">When ASP.NET gets the request, it creates a brand-new instance of the page, runs the code in it, and then renders the page to the browser again.</span></span> <span data-ttu-id="3d237-314">但實際上，此頁面並不知道您使用的是舊版本身。</span><span class="sxs-lookup"><span data-stu-id="3d237-314">In effect, though, the page doesn't know that you were just working with a previous version of itself.</span></span> <span data-ttu-id="3d237-315">它知道它會得到一個要求，裡面有一些表單資料。</span><span class="sxs-lookup"><span data-stu-id="3d237-315">All it knows is that it got a request that had some form data in it.</span></span>

<span data-ttu-id="3d237-316">每次要求頁面時 &mdash; 是第一次還是提交，&mdash; 您正在取得新的頁面。</span><span class="sxs-lookup"><span data-stu-id="3d237-316">Every time you request a page &mdash; whether for the first time or by submitting it &mdash; you're getting a new page.</span></span> <span data-ttu-id="3d237-317">網頁伺服器沒有您上一個要求的記憶體。</span><span class="sxs-lookup"><span data-stu-id="3d237-317">The web server has no memory of your last request.</span></span> <span data-ttu-id="3d237-318">兩者都不會 ASP.NET，而且瀏覽器都不會執行。</span><span class="sxs-lookup"><span data-stu-id="3d237-318">Neither does ASP.NET, and neither does the browser.</span></span> <span data-ttu-id="3d237-319">這些個別實例之間的唯一連接是您在它們之間傳輸的任何資料。</span><span class="sxs-lookup"><span data-stu-id="3d237-319">The only connection between these separate instances of the page is any data that you transmit between them.</span></span> <span data-ttu-id="3d237-320">例如，如果您提交頁面，新的頁面實例可以取得先前實例所傳送的表單資料。</span><span class="sxs-lookup"><span data-stu-id="3d237-320">If you submit a page, for example, the new page instance can get the form data that was sent by the earlier instance.</span></span> <span data-ttu-id="3d237-321">（在頁面之間傳遞資料的另一種方式是使用 cookie）。</span><span class="sxs-lookup"><span data-stu-id="3d237-321">(Another way to pass data between pages is to use cookies.)</span></span>

<span data-ttu-id="3d237-322">描述這種情況的一種正式方式是說，網頁是*無狀態*的。</span><span class="sxs-lookup"><span data-stu-id="3d237-322">A formal way to describe this situation is to say that web pages are *stateless*.</span></span> <span data-ttu-id="3d237-323">網頁伺服器和頁面本身，以及頁面中的元素不會維護任何有關頁面先前狀態的資訊。</span><span class="sxs-lookup"><span data-stu-id="3d237-323">Web servers and the pages themselves and the elements in the page do not maintain any information about the previous state of a page.</span></span> <span data-ttu-id="3d237-324">Web 是以這種方式設計的，因為維護個別要求的狀態會快速耗盡 web 伺服器的資源，這通常會處理數千個（甚至是每秒數百個要求）。</span><span class="sxs-lookup"><span data-stu-id="3d237-324">The web was designed this way because maintaining state for individual requests would quickly exhaust the resources of web servers, which often handle thousands, maybe even hundreds of thousands, of requests per second.</span></span>

<span data-ttu-id="3d237-325">這就是為什麼文字方塊是空的。</span><span class="sxs-lookup"><span data-stu-id="3d237-325">So that's why the text box was empty.</span></span> <span data-ttu-id="3d237-326">提交頁面之後，ASP.NET 會建立頁面的新實例，並透過程式碼和標記執行。</span><span class="sxs-lookup"><span data-stu-id="3d237-326">After you submitted the page, ASP.NET created a new instance of the page and ran through the code and markup.</span></span> <span data-ttu-id="3d237-327">該程式碼中沒有任何告訴 ASP.NET 將值放入文字方塊中的東西。</span><span class="sxs-lookup"><span data-stu-id="3d237-327">There was nothing in that code that told ASP.NET to put a value into the text box.</span></span> <span data-ttu-id="3d237-328">因此 ASP.NET 不會執行任何動作，而且文字方塊的呈現不含值。</span><span class="sxs-lookup"><span data-stu-id="3d237-328">So ASP.NET didn't do anything, and the text box was rendered without a value in it.</span></span>

<span data-ttu-id="3d237-329">實際上，有一個簡單的方法可以解決此問題。</span><span class="sxs-lookup"><span data-stu-id="3d237-329">There's actually an easy way to get around this issue.</span></span> <span data-ttu-id="3d237-330">您在文字方塊中輸入的內容類型可供您在*程式*代碼中使用，&mdash; 它在 `Request.QueryString["searchGenre"]`中。</span><span class="sxs-lookup"><span data-stu-id="3d237-330">The genre that you entered into the text box *is* available to you in code &mdash; it's in `Request.QueryString["searchGenre"]`.</span></span>

<span data-ttu-id="3d237-331">更新文字方塊的標記，讓 `value` 屬性從 `searchTerm`取得其值，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="3d237-331">Update the markup for the text box so that the `value` attribute gets its value from `searchTerm`, like this example:</span></span>

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

<span data-ttu-id="3d237-332">在此頁面中，您也可以將 `value` 屬性設定為 `searchTerm` 變數，因為該變數也包含您所輸入的內容類型。</span><span class="sxs-lookup"><span data-stu-id="3d237-332">In this page, you could have also set the `value` attribute to the `searchTerm` variable, since that variable also contains the genre you entered.</span></span> <span data-ttu-id="3d237-333">但是，使用 `Request` 物件來設定 `value` 屬性，如下所示，這是完成這項工作的標準方式。</span><span class="sxs-lookup"><span data-stu-id="3d237-333">But using the `Request` object to set the `value` attribute as shown here is the standard way to accomplish this task.</span></span> <span data-ttu-id="3d237-334">（假設您甚至想要在某些情況下執行這項 &mdash;，您可能會想要在欄位中呈現*不含*值的頁面。</span><span class="sxs-lookup"><span data-stu-id="3d237-334">(Assuming you even want to do this &mdash; in some situations, you might want to render the page *without* values in the fields.</span></span> <span data-ttu-id="3d237-335">這一切都取決於應用程式的狀況。）</span><span class="sxs-lookup"><span data-stu-id="3d237-335">It all depends on what's going on with your app.)</span></span>

> [!NOTE]
> <span data-ttu-id="3d237-336">您不能「記住」用於密碼的文字方塊值。</span><span class="sxs-lookup"><span data-stu-id="3d237-336">You can't "remember" the value of a text box that's used for passwords.</span></span> <span data-ttu-id="3d237-337">這會是一個安全性漏洞，讓使用者可以使用程式碼填寫密碼欄位。</span><span class="sxs-lookup"><span data-stu-id="3d237-337">It would be a security hole to allow people to fill in a password field by using code.</span></span>

<span data-ttu-id="3d237-338">再次執行頁面，輸入內容類型，然後按一下 [**搜尋**內容類型]。</span><span class="sxs-lookup"><span data-stu-id="3d237-338">Run the page again, enter a genre, and click **Search Genre**.</span></span> <span data-ttu-id="3d237-339">這次不只會看到搜尋結果，而文字方塊會記住您上一次輸入的內容：</span><span class="sxs-lookup"><span data-stu-id="3d237-339">This time not only do you see the results of the search, but the text box remembers what you entered last time:</span></span>

![頁面，顯示文字方塊已「記住」先前的專案](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a><span data-ttu-id="3d237-341">搜尋標題中的任何單字</span><span class="sxs-lookup"><span data-stu-id="3d237-341">Searching for Any Word in the Title</span></span>

<span data-ttu-id="3d237-342">您現在可以搜尋任何類型內容，但您可能也會想要搜尋標題。</span><span class="sxs-lookup"><span data-stu-id="3d237-342">You can now search for any genre, but you might also want to search for a title.</span></span> <span data-ttu-id="3d237-343">當您搜尋時，很難正確地取得標題，因此您可以搜尋出現在標題中任何位置的單字。</span><span class="sxs-lookup"><span data-stu-id="3d237-343">It's hard to get a title exactly right when you search, so instead you can search for a word that appears anywhere inside a title.</span></span> <span data-ttu-id="3d237-344">若要在 SQL 中執行此動作，請使用 `LIKE` 運算子和語法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3d237-344">To do that in SQL, you use the `LIKE` operator and syntax like the following:</span></span>

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

<span data-ttu-id="3d237-345">此命令會取得標題包含「艾德」的所有電影。</span><span class="sxs-lookup"><span data-stu-id="3d237-345">This command gets all the movies whose titles contain "adventure".</span></span> <span data-ttu-id="3d237-346">當您使用 `LIKE` 運算子時，您會在搜尋字詞中包含萬用字元 `%`。</span><span class="sxs-lookup"><span data-stu-id="3d237-346">When you use the `LIKE` operator, you include the wildcard character `%` as part of the search term.</span></span> <span data-ttu-id="3d237-347">搜尋 `LIKE 'adventure%'` 表示「從 ' 冒險 ' 開始」。</span><span class="sxs-lookup"><span data-stu-id="3d237-347">The search `LIKE 'adventure%'` means "starting with 'adventure'".</span></span> <span data-ttu-id="3d237-348">（技術上來說，這表示「字串 ' 艾德」後面接著任何東西。」）同樣地，搜尋詞彙 `LIKE '%adventure'` 表示「任何後面接著字串 ' 艾德 '」的「專案」，也就是「以 ' 艾德 ' 做為結尾」的另一種方式。</span><span class="sxs-lookup"><span data-stu-id="3d237-348">(Technically, it means "The string 'adventure' followed by anything.") Similarly, the search term `LIKE '%adventure'` means "anything followed by the string 'adventure'", which is another way to say "ending with 'adventure'".</span></span>

<span data-ttu-id="3d237-349">因此，搜尋詞彙 `LIKE '%adventure%'` 因此會在標題中的任何位置表示「具有 ' 艾德」。」</span><span class="sxs-lookup"><span data-stu-id="3d237-349">The search term `LIKE '%adventure%'` therefore means "with 'adventure' anywhere in the title."</span></span> <span data-ttu-id="3d237-350">（技術上來說，「標題中的任何東西」，後面接著「艾德」，再加上任何東西）。</span><span class="sxs-lookup"><span data-stu-id="3d237-350">(Technically, "anything in the title, followed by 'adventure', followed by anything.")</span></span>

<span data-ttu-id="3d237-351">在 `<form>` 專案中，于內容類型搜尋的結尾 `</div>` 標記（緊接在結尾 `</form>` 元素之前）新增下列標記：</span><span class="sxs-lookup"><span data-stu-id="3d237-351">Inside the `<form>` element, add the following markup right under the closing `</div>` tag for the genre search (just before the closing `</form>` element):</span></span>

[!code-html[Main](form-basics/samples/sample10.html)]

<span data-ttu-id="3d237-352">處理此搜尋的程式碼類似于內容類型搜尋的程式碼，不同之處在于您必須組合 `LIKE` 搜尋。</span><span class="sxs-lookup"><span data-stu-id="3d237-352">The code to handle this search is similar to the code for the genre search, except that you have to assemble the `LIKE` search.</span></span> <span data-ttu-id="3d237-353">在頁面頂端的程式碼區塊中，在內容類型搜尋的 `if` 區塊之後，新增此 `if` 組塊：</span><span class="sxs-lookup"><span data-stu-id="3d237-353">Inside the code block at the top of the page, add this `if` block just after the `if` block for the genre search:</span></span>

[!code-csharp[Main](form-basics/samples/sample11.cs)]

<span data-ttu-id="3d237-354">此程式碼會使用您稍早看到的相同邏輯，不同之處在于搜尋會使用 `LIKE` 運算子，而程式碼會將 "`%`" 放在搜尋詞彙的前後。</span><span class="sxs-lookup"><span data-stu-id="3d237-354">This code uses the same logic you saw earlier, except that the search uses a `LIKE` operator and the code puts "`%`" before and after the search term.</span></span>

<span data-ttu-id="3d237-355">請注意，如何輕鬆地將另一個搜尋新增至頁面。</span><span class="sxs-lookup"><span data-stu-id="3d237-355">Notice how it was easy to add another search to the page.</span></span> <span data-ttu-id="3d237-356">您只需要：</span><span class="sxs-lookup"><span data-stu-id="3d237-356">All you had to do was:</span></span>

- <span data-ttu-id="3d237-357">建立測試的 `if` 區塊，以查看相關的搜尋方塊是否具有值。</span><span class="sxs-lookup"><span data-stu-id="3d237-357">Create an `if` block that tested to see whether the relevant search box had a value.</span></span>
- <span data-ttu-id="3d237-358">將 `selectCommand` 變數設定為新的 SQL 語句。</span><span class="sxs-lookup"><span data-stu-id="3d237-358">Set the `selectCommand` variable to a new SQL statement.</span></span>
- <span data-ttu-id="3d237-359">將 `searchTerm` 變數設定為要傳遞給查詢的值。</span><span class="sxs-lookup"><span data-stu-id="3d237-359">Set the `searchTerm` variable to the value to pass to the query.</span></span>

<span data-ttu-id="3d237-360">以下是完整的程式碼區塊，其中包含標題搜尋的新邏輯：</span><span class="sxs-lookup"><span data-stu-id="3d237-360">Here's the complete code block, which contains the new logic for a title search:</span></span>

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

<span data-ttu-id="3d237-361">以下摘要說明此程式碼的作用：</span><span class="sxs-lookup"><span data-stu-id="3d237-361">Here's a summary of what this code does:</span></span>

- <span data-ttu-id="3d237-362">`searchTerm` 和 `selectCommand` 的變數會在頂端初始化。</span><span class="sxs-lookup"><span data-stu-id="3d237-362">The variables `searchTerm` and `selectCommand` are initialized at the top.</span></span> <span data-ttu-id="3d237-363">您將根據使用者在頁面中執行的工作，將這些變數設定為適當的搜尋字詞（如果有的話）和適當的 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="3d237-363">You're going to set these variables to the appropriate search term (if any) and appropriate SQL command based on what the user does in the page.</span></span> <span data-ttu-id="3d237-364">預設搜尋是從資料庫取得所有電影的簡單案例。</span><span class="sxs-lookup"><span data-stu-id="3d237-364">The default search is the simple case of getting all the movies from the database.</span></span>
- <span data-ttu-id="3d237-365">在 `searchGenre` 和 `searchTitle`的測試中，程式碼會將 `searchTerm` 設定為您要搜尋的值。</span><span class="sxs-lookup"><span data-stu-id="3d237-365">In the tests for `searchGenre` and `searchTitle`, the code sets `searchTerm` to the value you want to search for.</span></span> <span data-ttu-id="3d237-366">這些程式碼區塊也會將 `selectCommand` 設定為該搜尋的適當 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="3d237-366">Those code blocks also set `selectCommand` to an appropriate SQL command for that search.</span></span>
- <span data-ttu-id="3d237-367">`db.Query` 方法只會叫用一次，使用 `selectedCommand` 的 SQL 命令，以及 `searchTerm`中的任何值。</span><span class="sxs-lookup"><span data-stu-id="3d237-367">The `db.Query` method is invoked only once, using whatever SQL command is in `selectedCommand` and whatever value is in `searchTerm`.</span></span> <span data-ttu-id="3d237-368">如果沒有搜尋字詞（沒有內容類型，也沒有標題字），`searchTerm` 的值就是空字串。</span><span class="sxs-lookup"><span data-stu-id="3d237-368">If there is no search term (no genre and no title word), the value of `searchTerm` is an empty string.</span></span> <span data-ttu-id="3d237-369">不過，這並不重要，因為在這種情況下，查詢不需要參數。</span><span class="sxs-lookup"><span data-stu-id="3d237-369">However, that doesn't matter, because in that case the query doesn't require a parameter.</span></span>

## <a name="testing-the-title-search-feature"></a><span data-ttu-id="3d237-370">測試標題搜尋功能</span><span class="sxs-lookup"><span data-stu-id="3d237-370">Testing the Title Search Feature</span></span>

<span data-ttu-id="3d237-371">現在您可以測試已完成的搜尋頁面。</span><span class="sxs-lookup"><span data-stu-id="3d237-371">Now you can test your completed search page.</span></span> <span data-ttu-id="3d237-372">執行*電影。 cshtml*。</span><span class="sxs-lookup"><span data-stu-id="3d237-372">Run *Movies.cshtml*.</span></span>

<span data-ttu-id="3d237-373">輸入內容類型，然後按一下 [**搜尋**內容類型]。</span><span class="sxs-lookup"><span data-stu-id="3d237-373">Enter a genre and click **Search Genre**.</span></span> <span data-ttu-id="3d237-374">格線會顯示該內容類型的電影，就像之前一樣。</span><span class="sxs-lookup"><span data-stu-id="3d237-374">The grid displays movies of that genre, like before.</span></span>

<span data-ttu-id="3d237-375">輸入標題文字，然後按一下 [**搜尋標題**]。</span><span class="sxs-lookup"><span data-stu-id="3d237-375">Enter a title word and click **Search Title**.</span></span> <span data-ttu-id="3d237-376">此方格會顯示標題中有該單字的電影。</span><span class="sxs-lookup"><span data-stu-id="3d237-376">The grid displays movies that have that word in the title.</span></span>

![在標題中搜尋 ' the ' 之後的電影頁面清單](form-basics/_static/image6.png)

<span data-ttu-id="3d237-378">將兩個文字方塊保持空白，然後按一下其中一個按鈕。</span><span class="sxs-lookup"><span data-stu-id="3d237-378">Leave both text boxes blank and click either button.</span></span> <span data-ttu-id="3d237-379">方格會顯示所有電影。</span><span class="sxs-lookup"><span data-stu-id="3d237-379">The grid displays all the movies.</span></span>

## <a name="combining-the-queries"></a><span data-ttu-id="3d237-380">結合查詢</span><span class="sxs-lookup"><span data-stu-id="3d237-380">Combining the Queries</span></span>

<span data-ttu-id="3d237-381">您可能會注意到，您可以執行的搜尋是獨佔的。</span><span class="sxs-lookup"><span data-stu-id="3d237-381">You might notice that the searches you can perform are exclusive.</span></span> <span data-ttu-id="3d237-382">您不能同時搜尋標題和內容類型，即使這兩個搜尋方塊中有值也一樣。</span><span class="sxs-lookup"><span data-stu-id="3d237-382">You can't search the title and the genre at the same time, even if both search boxes have values in them.</span></span> <span data-ttu-id="3d237-383">例如，您無法搜尋標題包含 "艾德" 的所有動作電影。</span><span class="sxs-lookup"><span data-stu-id="3d237-383">For example, you can't search for all action movies whose title contains "Adventure".</span></span> <span data-ttu-id="3d237-384">（當頁面已編碼時，如果您同時輸入內容類型和標題的值，則標題搜尋會優先）。若要建立合併條件的搜尋，您必須建立具有如下語法的 SQL 查詢：</span><span class="sxs-lookup"><span data-stu-id="3d237-384">(As the page is coded now, if you enter values for both genre and title, the title search gets precedence.) To create a search that combines the conditions, you would have to create a SQL query that has syntax like the following:</span></span>

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

<span data-ttu-id="3d237-385">而且，您必須使用如下所示的語句來執行查詢（大致說）：</span><span class="sxs-lookup"><span data-stu-id="3d237-385">And you'd have to run the query by using a statement like the following (roughly speaking):</span></span>

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

<span data-ttu-id="3d237-386">建立邏輯來允許許多搜尋條件的排列，可能會有一些相關的情況，如您所見。</span><span class="sxs-lookup"><span data-stu-id="3d237-386">Creating logic to allow many permutations of search criteria can get a bit involved, as you can see.</span></span> <span data-ttu-id="3d237-387">因此，我們將在此停止。</span><span class="sxs-lookup"><span data-stu-id="3d237-387">Therefore, we'll stop here.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="3d237-388">下一步</span><span class="sxs-lookup"><span data-stu-id="3d237-388">Coming Up Next</span></span>

<span data-ttu-id="3d237-389">在下一個教學課程中，您將建立使用表單的頁面，讓使用者將電影新增至資料庫。</span><span class="sxs-lookup"><span data-stu-id="3d237-389">In the next tutorial, you'll create a page that uses a form to let users add movies to the database.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-search"></a><span data-ttu-id="3d237-390">電影頁面的完整清單（使用搜尋更新）</span><span class="sxs-lookup"><span data-stu-id="3d237-390">Complete Listing for Movie Page (Updated with Search)</span></span>

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="3d237-391">其他資源</span><span class="sxs-lookup"><span data-stu-id="3d237-391">Additional Resources</span></span>

- [<span data-ttu-id="3d237-392">使用 Razor 語法 ASP.NET Web 程式設計的簡介</span><span class="sxs-lookup"><span data-stu-id="3d237-392">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)
- <span data-ttu-id="3d237-393">W3Schools 網站上的[SQL WHERE 子句](http://www.w3schools.com/sql/sql_where.asp)</span><span class="sxs-lookup"><span data-stu-id="3d237-393">[SQL WHERE Clause](http://www.w3schools.com/sql/sql_where.asp) on the W3Schools site</span></span>
- <span data-ttu-id="3d237-394">W3C 網站上的[方法定義](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)文章</span><span class="sxs-lookup"><span data-stu-id="3d237-394">[Method Definitions](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) article on the W3C site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3d237-395">[上一頁](displaying-data.md)
> [下一頁](entering-data.md)</span><span class="sxs-lookup"><span data-stu-id="3d237-395">[Previous](displaying-data.md)
[Next](entering-data.md)</span></span>
