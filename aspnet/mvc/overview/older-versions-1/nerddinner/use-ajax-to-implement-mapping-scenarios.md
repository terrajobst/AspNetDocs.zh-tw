---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: 使用 AJAX 來執行對應案例 |Microsoft Docs
author: microsoft
description: 步驟11顯示如何將 AJAX 對應支援整合到我們的 NerdDinner 應用程式，讓正在建立、編輯或查看 dinners 的使用者查看 l 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: 7fc90f978b9f9eca511feca70a3c0d02ec69b940
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580112"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a><span data-ttu-id="f76fb-103">使用 AJAX 實作對應實例</span><span class="sxs-lookup"><span data-stu-id="f76fb-103">Use AJAX to Implement Mapping Scenarios</span></span>

<span data-ttu-id="f76fb-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f76fb-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="f76fb-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="f76fb-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="f76fb-106">這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟11，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f76fb-106">This is step 11 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="f76fb-107">步驟11顯示如何將 AJAX 對應支援整合到我們的 NerdDinner 應用程式，讓正在建立、編輯或查看 dinners 的使用者以圖形方式查看晚餐的位置。</span><span class="sxs-lookup"><span data-stu-id="f76fb-107">Step 11 shows how to integrate AJAX mapping support into our NerdDinner application, enabling users who are creating, editing or viewing dinners to see the location of the dinner graphically.</span></span>
> 
> <span data-ttu-id="f76fb-108">如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。</span><span class="sxs-lookup"><span data-stu-id="f76fb-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a><span data-ttu-id="f76fb-109">NerdDinner 步驟11：整合 AJAX 地圖</span><span class="sxs-lookup"><span data-stu-id="f76fb-109">NerdDinner Step 11: Integrating an AJAX Map</span></span>

<span data-ttu-id="f76fb-110">我們現在會藉由整合 AJAX 對應支援，讓我們的應用程式更具視覺效果。</span><span class="sxs-lookup"><span data-stu-id="f76fb-110">We'll now make our application a little more visually exciting by integrating AJAX mapping support.</span></span> <span data-ttu-id="f76fb-111">這可讓正在建立、編輯或查看 dinners 的使用者以圖形方式查看晚餐的位置。</span><span class="sxs-lookup"><span data-stu-id="f76fb-111">This will enable users who are creating, editing or viewing dinners to see the location of the dinner graphically.</span></span>

### <a name="creating-a-map-partial-view"></a><span data-ttu-id="f76fb-112">建立地圖部分視圖</span><span class="sxs-lookup"><span data-stu-id="f76fb-112">Creating a Map Partial View</span></span>

<span data-ttu-id="f76fb-113">我們會在應用程式內的數個地方使用對應功能。</span><span class="sxs-lookup"><span data-stu-id="f76fb-113">We are going to use mapping functionality in several places within our application.</span></span> <span data-ttu-id="f76fb-114">為了讓我們的程式碼更好，我們會將一般對應功能封裝在單一部分範本中，以便在多個控制器動作和視圖之間重複使用。</span><span class="sxs-lookup"><span data-stu-id="f76fb-114">To keep our code DRY we'll encapsulate the common map functionality within a single partial template that we can re-use across multiple controller actions and views.</span></span> <span data-ttu-id="f76fb-115">我們會將此部分視圖命名為「對應 .ascx」，並在 \Views\Dinners 目錄中建立它。</span><span class="sxs-lookup"><span data-stu-id="f76fb-115">We'll name this partial view "map.ascx" and create it within the \Views\Dinners directory.</span></span>

<span data-ttu-id="f76fb-116">我們可以用滑鼠右鍵按一下 [\Views\Dinners] 目錄，然後選擇 [新增-&gt;View] 功能表命令來建立對應 .ascx 部分。</span><span class="sxs-lookup"><span data-stu-id="f76fb-116">We can create the map.ascx partial by right-clicking on the \Views\Dinners directory and choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="f76fb-117">我們會將 view 命名為 "node.js"，並將其視為部分視圖，並指出我們即將傳遞強型別「晚餐」模型類別：</span><span class="sxs-lookup"><span data-stu-id="f76fb-117">We'll name the view "Map.ascx", check it as a partial view, and indicate that we are going to pass it a strongly-typed "Dinner" model class:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

<span data-ttu-id="f76fb-118">當我們按一下 [新增] 按鈕時，將會建立部分範本。</span><span class="sxs-lookup"><span data-stu-id="f76fb-118">When we click the "Add" button our partial template will be created.</span></span> <span data-ttu-id="f76fb-119">接著，我們會將對應的 .ascx 檔案更新為具有下列內容：</span><span class="sxs-lookup"><span data-stu-id="f76fb-119">We'll then update the Map.ascx file to have the following content:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

<span data-ttu-id="f76fb-120">第一個 &lt;腳本&gt; 參考指向 Microsoft 虛擬地球6.2 對應程式庫。</span><span class="sxs-lookup"><span data-stu-id="f76fb-120">The first &lt;script&gt; reference points to the Microsoft Virtual Earth 6.2 mapping library.</span></span> <span data-ttu-id="f76fb-121">第二個 &lt;腳本&gt; 參考指向對應 .js 檔案，我們很快就會建立該檔案，以封裝我們的一般 JAVAscript 對應邏輯。</span><span class="sxs-lookup"><span data-stu-id="f76fb-121">The second &lt;script&gt; reference points to a map.js file that we will shortly create which will encapsulate our common Javascript mapping logic.</span></span> <span data-ttu-id="f76fb-122">&lt;div id = "theMap"&gt; 元素是虛擬地球將用來裝載對應的 HTML 容器。</span><span class="sxs-lookup"><span data-stu-id="f76fb-122">The &lt;div id="theMap"&gt; element is the HTML container that Virtual Earth will use to host the map.</span></span>

<span data-ttu-id="f76fb-123">接著，我們會有內嵌的 &lt;腳本&gt; 區塊，其中包含兩個此視圖特有的 JavaScript 函式。</span><span class="sxs-lookup"><span data-stu-id="f76fb-123">We then have an embedded &lt;script&gt; block that contains two JavaScript functions specific to this view.</span></span> <span data-ttu-id="f76fb-124">第一個函式會使用 jQuery 來連接在頁面準備好要執行用戶端腳本時所執行的函式。</span><span class="sxs-lookup"><span data-stu-id="f76fb-124">The first function uses jQuery to wire-up a function that executes when the page is ready to run client-side script.</span></span> <span data-ttu-id="f76fb-125">它會呼叫 LoadMap （） helper 函式，我們將在我們的對應 .js 腳本檔案中定義，以載入虛擬地球地圖控制項。</span><span class="sxs-lookup"><span data-stu-id="f76fb-125">It calls a LoadMap() helper function that we'll define within our Map.js script file to load the virtual earth map control.</span></span> <span data-ttu-id="f76fb-126">第二個函式是回呼事件處理常式，會將釘選到識別位置的對應。</span><span class="sxs-lookup"><span data-stu-id="f76fb-126">The second function is a callback event handler that adds a pin to the map that identifies a location.</span></span>

<span data-ttu-id="f76fb-127">請注意，我們如何在用戶端腳本區塊內使用伺服器端 &lt;% =%&gt; 區塊，以內嵌我們想要對應至 JavaScript 的晚餐的緯度和經度。</span><span class="sxs-lookup"><span data-stu-id="f76fb-127">Notice how we are using a server-side &lt;%= %&gt; block within the client-side script block to embed the latitude and longitude of the Dinner we want to map into the JavaScript.</span></span> <span data-ttu-id="f76fb-128">這是用來輸出可供用戶端腳本使用之動態值的實用技巧（不需要對伺服器進行個別的 AJAX 呼叫來抓取值，讓它更快速）。</span><span class="sxs-lookup"><span data-stu-id="f76fb-128">This is a useful technique to output dynamic values that can be used by client-side script (without requiring a separate AJAX call back to the server to retrieve the values – which makes it faster).</span></span> <span data-ttu-id="f76fb-129">當此視圖在伺服器上呈現時，&lt;% =%&gt; 區塊會執行，因此 HTML 的輸出最後會有內嵌的 JavaScript 值（例如： var 緯度 = 47.64312;）。</span><span class="sxs-lookup"><span data-stu-id="f76fb-129">The &lt;%= %&gt; blocks will execute when the view is rendering on the server – and so the output of the HTML will just end up with embedded JavaScript values (for example: var latitude = 47.64312;).</span></span>

### <a name="creating-a-mapjs-utility-library"></a><span data-ttu-id="f76fb-130">建立對應 .js 公用程式程式庫</span><span class="sxs-lookup"><span data-stu-id="f76fb-130">Creating a Map.js utility library</span></span>

<span data-ttu-id="f76fb-131">現在讓我們建立 Map .js 檔案，我們可以用它來封裝 map 的 JavaScript 功能（並執行上述的 LoadMap 和 LoadPin 方法）。</span><span class="sxs-lookup"><span data-stu-id="f76fb-131">Let's now create the Map.js file that we can use to encapsulate the JavaScript functionality for our map (and implement the LoadMap and LoadPin methods above).</span></span> <span data-ttu-id="f76fb-132">若要這麼做，請以滑鼠右鍵按一下專案內的 \Scripts 目錄，然後選擇 [加入&gt;新專案] 功能表命令，選取 [JScript] 專案，並將其命名為「對應 .js」。</span><span class="sxs-lookup"><span data-stu-id="f76fb-132">We can do this by right-clicking on the \Scripts directory within our project, and then choose the "Add-&gt;New Item" menu command, select the JScript item, and name it "Map.js".</span></span>

<span data-ttu-id="f76fb-133">以下是我們將新增至對應 .js 檔案的 JavaScript 程式碼，該檔案會與虛擬地球互動，以顯示地圖，並為我們的 dinners 新增位置圖釘：</span><span class="sxs-lookup"><span data-stu-id="f76fb-133">Below is the JavaScript code we'll add to the Map.js file that will interact with Virtual Earth to display our map and add locations pins to it for our dinners:</span></span>

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a><span data-ttu-id="f76fb-134">整合地圖與建立和編輯表單</span><span class="sxs-lookup"><span data-stu-id="f76fb-134">Integrating the Map with Create and Edit Forms</span></span>

<span data-ttu-id="f76fb-135">我們現在會將地圖支援與現有的建立和編輯案例進行整合。</span><span class="sxs-lookup"><span data-stu-id="f76fb-135">We'll now integrate the Map support with our existing Create and Edit scenarios.</span></span> <span data-ttu-id="f76fb-136">好消息是，這很簡單，而且不需要我們變更我們的任何控制器程式碼。</span><span class="sxs-lookup"><span data-stu-id="f76fb-136">The good news is that this is pretty easy to-do, and doesn't require us to change any of our Controller code.</span></span> <span data-ttu-id="f76fb-137">因為我們的建立和編輯檢視會共用通用的「DinnerForm」部分視圖來執行晚餐表單 UI，所以我們可以在一處新增地圖，並同時使用「建立」和「編輯」案例。</span><span class="sxs-lookup"><span data-stu-id="f76fb-137">Because our Create and Edit views share a common "DinnerForm" partial view to implement the dinner form UI, we can add the map in one place and have both our Create and Edit scenarios use it.</span></span>

<span data-ttu-id="f76fb-138">我們只需要開啟 \Views\Dinners\DinnerForm.ascx 部分視圖並加以更新，以包含新的地圖部分。</span><span class="sxs-lookup"><span data-stu-id="f76fb-138">All we need to-do is to open the \Views\Dinners\DinnerForm.ascx partial view and update it to include our new map partial.</span></span> <span data-ttu-id="f76fb-139">以下是新增對應之後，更新的 DinnerForm 會顯示的樣子（注意：下列程式碼片段會省略 HTML 表單元素以求簡潔）：</span><span class="sxs-lookup"><span data-stu-id="f76fb-139">Below is what the updated DinnerForm will look like once the map is added (note: the HTML form elements are omitted from the code snippet below for brevity):</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

<span data-ttu-id="f76fb-140">上述的 DinnerForm 部分會將 "DinnerFormViewModel" 類型的物件當做其模型類型（因為它需要晚餐物件，以及用來填入國家/地區 dropdownlist 的 SelectList）。</span><span class="sxs-lookup"><span data-stu-id="f76fb-140">The DinnerForm partial above takes an object of type "DinnerFormViewModel" as its model type (because it needs both a Dinner object, as well as a SelectList to populate the dropdownlist of countries).</span></span> <span data-ttu-id="f76fb-141">我們的 Map 部分只需要「晚餐」類型的物件做為其模型類型，因此當我們轉譯 Map 部分時，我們只會將 DinnerFormViewModel 的晚餐子屬性傳遞給它：</span><span class="sxs-lookup"><span data-stu-id="f76fb-141">Our Map partial just needs an object of type "Dinner" as its model type, and so when we render the map partial we are passing just the Dinner sub-property of DinnerFormViewModel to it:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

<span data-ttu-id="f76fb-142">我們已新增至部分的 JavaScript 函式會使用 jQuery 將「模糊」事件附加至 [位址] HTML 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="f76fb-142">The JavaScript function we've added to the partial uses jQuery to attach a "blur" event to the "Address" HTML textbox.</span></span> <span data-ttu-id="f76fb-143">您可能聽過「焦點」事件，會在使用者按一下或索引標籤成為文字方塊時引發。</span><span class="sxs-lookup"><span data-stu-id="f76fb-143">You've probably heard of "focus" events that fire when a user clicks or tabs into a textbox.</span></span> <span data-ttu-id="f76fb-144">相反的是當使用者結束文字方塊時，所引發的「模糊」事件。</span><span class="sxs-lookup"><span data-stu-id="f76fb-144">The opposite is a "blur" event that fires when a user exits a textbox.</span></span> <span data-ttu-id="f76fb-145">上述事件處理常式會在發生這種情況時，清除 [緯度] 和 [經度] 文字方塊的值，然後在地圖上繪製新的位址位置。</span><span class="sxs-lookup"><span data-stu-id="f76fb-145">The above event handler clears the latitude and longitude textbox values when this happens, and then plots the new address location on our map.</span></span> <span data-ttu-id="f76fb-146">我們在 map .js 檔案內定義的回呼事件處理常式，會根據我們提供的位址，使用虛擬地球傳回的值，更新表單上的 [經度] 和 [緯度] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="f76fb-146">A callback event handler that we defined within the map.js file will then update the longitude and latitude textboxes on our form using values returned by virtual earth based on the address we gave it.</span></span>

<span data-ttu-id="f76fb-147">現在當我們再次執行應用程式，並按一下 [主機晚餐] 索引標籤時，我們會看到與標準晚餐表單元素一起顯示的預設地圖：</span><span class="sxs-lookup"><span data-stu-id="f76fb-147">And now when we run our application again and click the "Host Dinner" tab we'll see a default map displayed along with our standard Dinner form elements:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

<span data-ttu-id="f76fb-148">當我們輸入位址，然後按 tab 鍵離開時，地圖會動態更新以顯示位置，而我們的事件處理常式將會在 [緯度/經度] 文字方塊中填入位置值：</span><span class="sxs-lookup"><span data-stu-id="f76fb-148">When we type in an address, and then tab away, the map will dynamically update to display the location, and our event handler will populate the latitude/longitude textboxes with the location values:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

<span data-ttu-id="f76fb-149">如果我們儲存新晚餐，然後再次開啟以供編輯，我們會發現對應位置會在頁面載入時顯示：</span><span class="sxs-lookup"><span data-stu-id="f76fb-149">If we save the new dinner and then open it again for editing, we'll find that the map location is displayed when the page loads:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

<span data-ttu-id="f76fb-150">每次變更 [位址] 欄位時，地圖和緯度/經度座標都會更新。</span><span class="sxs-lookup"><span data-stu-id="f76fb-150">Every time the address field is changed, the map and the latitude/longitude coordinates will update.</span></span>

<span data-ttu-id="f76fb-151">現在地圖會顯示晚餐位置，我們也可以將 [緯度] 和 [經度] 表單欄位從可見的文字方塊變更為隱藏的元素（因為地圖會在每次輸入位址時自動更新）。</span><span class="sxs-lookup"><span data-stu-id="f76fb-151">Now that the map displays the Dinner location, we can also change the Latitude and Longitude form fields from being visible textboxes to instead be hidden elements (since the map is automatically updating them each time an address is entered).</span></span> <span data-ttu-id="f76fb-152">為此，我們將使用 Html. TextBox （） HTML helper 來切換，以使用 Html. Hidden （） helper 方法：</span><span class="sxs-lookup"><span data-stu-id="f76fb-152">To-do this we'll switch from using the Html.TextBox() HTML helper to using the Html.Hidden() helper method:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

<span data-ttu-id="f76fb-153">現在，我們的表單更方便使用者使用，並避免顯示未經處理的緯度/經度（但仍會將它們儲存在資料庫中的每個晚餐）：</span><span class="sxs-lookup"><span data-stu-id="f76fb-153">And now our forms are a little more user-friendly and avoid displaying the raw latitude/longitude (while still storing them with each Dinner in the database):</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a><span data-ttu-id="f76fb-154">將地圖與詳細資料檢視整合</span><span class="sxs-lookup"><span data-stu-id="f76fb-154">Integrating the Map with the Details View</span></span>

<span data-ttu-id="f76fb-155">既然我們已將對應與我們的建立和編輯案例整合，讓我們也將它與我們的詳細資料案例整合。</span><span class="sxs-lookup"><span data-stu-id="f76fb-155">Now that we have the map integrated with our Create and Edit scenarios, let's also integrate it with our Details scenario.</span></span> <span data-ttu-id="f76fb-156">我們只需要呼叫 &lt;% RenderPartial （"map"）;詳細資料檢視中的%&gt;。</span><span class="sxs-lookup"><span data-stu-id="f76fb-156">All we need to-do is to call &lt;% Html.RenderPartial("map"); %&gt; within the Details view.</span></span>

<span data-ttu-id="f76fb-157">以下是 [完整詳細資料] 視圖的原始程式碼（含對應整合）如下所示：</span><span class="sxs-lookup"><span data-stu-id="f76fb-157">Below is what the source code to the complete Details view (with map integration) looks like:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

<span data-ttu-id="f76fb-158">現在，當使用者流覽至/Dinners/Details/[id] URL 時，他們會看到晚餐的詳細資料、地圖上晚餐的位置（完成時使用圖釘，當滑鼠停留在上方時，會顯示晚餐的標題和位址），並具有適用于其 RSVP 的 AJAX 連結：</span><span class="sxs-lookup"><span data-stu-id="f76fb-158">And now when a user navigates to a /Dinners/Details/[id] URL they'll see details about the dinner, the location of the dinner on the map (complete with a push-pin that when hovered over displays the title of the dinner and the address of it), and have an AJAX link to RSVP for it:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a><span data-ttu-id="f76fb-159">在我們的資料庫和存放庫中執行位置搜尋</span><span class="sxs-lookup"><span data-stu-id="f76fb-159">Implementing Location Search in our Database and Repository</span></span>

<span data-ttu-id="f76fb-160">為了完成 AJAX 的執行，讓我們將地圖加入應用程式的首頁，以讓使用者以圖形方式搜尋附近的 dinners。</span><span class="sxs-lookup"><span data-stu-id="f76fb-160">To finish off our AJAX implementation, let's add a Map to the home page of the application that allows users to graphically search for dinners near them.</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

<span data-ttu-id="f76fb-161">我們一開始會先在資料庫和資料存放庫層內實行支援，以有效率地針對 Dinners 執行以位置為基礎的 radius 搜尋。</span><span class="sxs-lookup"><span data-stu-id="f76fb-161">We'll begin by implementing support within our database and data repository layer to efficiently perform a location-based radius search for Dinners.</span></span> <span data-ttu-id="f76fb-162">我們可以使用[sql 2008 的新地理空間功能](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx)來執行這項操作，或者我們也可以使用 sql 函式方法來 Gary Dryden 本文中討論的內容： [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx)和 Conery 網友有關在這裡使用與 LINQ to SQL： [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)</span><span class="sxs-lookup"><span data-stu-id="f76fb-162">We could use the new [geospatial features of SQL 2008](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) to implement this, or alternatively we can use a SQL function approach that Gary Dryden discussed in article here: [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) and Rob Conery blogged about using with LINQ to SQL here: [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)</span></span>

<span data-ttu-id="f76fb-163">若要執行這項技術，我們將在 Visual Studio 內開啟「伺服器總管」，選取 NerdDinner 資料庫，然後以滑鼠右鍵按一下其底下的 [函數] 子節點，並選擇建立新的「純量值函式」：</span><span class="sxs-lookup"><span data-stu-id="f76fb-163">To implement this technique, we will open the "Server Explorer" within Visual Studio, select the NerdDinner database, and then right-click on the "functions" sub-node under it and choose to create a new "Scalar-valued function":</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

<span data-ttu-id="f76fb-164">接著，我們會貼上下列 DistanceBetween 函數：</span><span class="sxs-lookup"><span data-stu-id="f76fb-164">We'll then paste in the following DistanceBetween function:</span></span>

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

<span data-ttu-id="f76fb-165">接著，我們會在 SQL Server 中建立新的資料表值函式，我們將會呼叫 "NearestDinners"：</span><span class="sxs-lookup"><span data-stu-id="f76fb-165">We'll then create a new table-valued function in SQL Server that we'll call "NearestDinners":</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

<span data-ttu-id="f76fb-166">這個 "NearestDinners" 資料表函數會使用 DistanceBetween helper 函式，傳回我們提供的緯度和經度100英里內的所有 Dinners：</span><span class="sxs-lookup"><span data-stu-id="f76fb-166">This "NearestDinners" table function uses the DistanceBetween helper function to return all Dinners within 100 miles of the latitude and longitude we supply it:</span></span>

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

<span data-ttu-id="f76fb-167">若要呼叫此函式，我們會先按兩下 \Models 目錄中的 NerdDinner 檔案，以開啟 LINQ to SQL 的設計工具：</span><span class="sxs-lookup"><span data-stu-id="f76fb-167">To call this function, we'll first open up the LINQ to SQL designer by double-clicking on the NerdDinner.dbml file within our \Models directory:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

<span data-ttu-id="f76fb-168">接著，我們會將 NearestDinners 和 DistanceBetween 函式拖曳至 LINQ to SQL 設計工具上，這會將其新增為我們 LINQ to SQL NerdDinnerDataCoNtext 類別上的方法：</span><span class="sxs-lookup"><span data-stu-id="f76fb-168">We'll then drag the NearestDinners and DistanceBetween functions onto the LINQ to SQL designer, which will cause them to be added as methods on our LINQ to SQL NerdDinnerDataContext class:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

<span data-ttu-id="f76fb-169">然後，我們可以在 DinnerRepository 類別上公開 "FindByLocation" 查詢方法，其使用 NearestDinner 函式來傳回在指定位置的100英里內即將發生的 Dinners：</span><span class="sxs-lookup"><span data-stu-id="f76fb-169">We can then expose a "FindByLocation" query method on our DinnerRepository class that uses the NearestDinner function to return upcoming Dinners that are within 100 miles of the specified location:</span></span>

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a><span data-ttu-id="f76fb-170">執行以 JSON 為基礎的 AJAX 搜尋動作方法</span><span class="sxs-lookup"><span data-stu-id="f76fb-170">Implementing a JSON-based AJAX Search Action Method</span></span>

<span data-ttu-id="f76fb-171">我們現在將會執行控制器動作方法，利用新的 FindByLocation （）存放庫方法，傳回可用來填入地圖的晚餐資料清單。</span><span class="sxs-lookup"><span data-stu-id="f76fb-171">We'll now implement a controller action method that takes advantage of the new FindByLocation() repository method to return back a list of Dinner data that can be used to populate a map.</span></span> <span data-ttu-id="f76fb-172">我們會將此動作方法傳回 JSON （JavaScript 物件標記法）格式的晚餐資料，讓您可以輕鬆地在用戶端上使用 JavaScript 來進行操作。</span><span class="sxs-lookup"><span data-stu-id="f76fb-172">We'll have this action method return back the Dinner data in a JSON (JavaScript Object Notation) format so that it can be easily manipulated using JavaScript on the client.</span></span>

<span data-ttu-id="f76fb-173">若要執行這項操作，我們將建立新的 "SearchController" 類別，方法是以滑鼠右鍵按一下 \Controllers 目錄，然後選擇 [新增-&gt;控制器] 功能表命令。</span><span class="sxs-lookup"><span data-stu-id="f76fb-173">To implement this, we'll create a new "SearchController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span> <span data-ttu-id="f76fb-174">接著，我們會在新的 SearchController 類別內執行 "SearchByLocation" 動作方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f76fb-174">We'll then implement a "SearchByLocation" action method within the new SearchController class like below:</span></span>

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

<span data-ttu-id="f76fb-175">SearchController 的 SearchByLocation 動作方法會在內部呼叫 DinnerRepository 上的 FindByLocation 方法，以取得鄰近 dinners 的清單。</span><span class="sxs-lookup"><span data-stu-id="f76fb-175">The SearchController's SearchByLocation action method internally calls the FindByLocation method on DinnerRepository to get a list of nearby dinners.</span></span> <span data-ttu-id="f76fb-176">不過，它會改為傳回 JsonDinner 物件，而不是直接將晚餐物件傳回給用戶端。</span><span class="sxs-lookup"><span data-stu-id="f76fb-176">Rather than return the Dinner objects directly to the client, though, it instead returns JsonDinner objects.</span></span> <span data-ttu-id="f76fb-177">JsonDinner 類別會公開晚餐屬性的子集（例如，基於安全性理由，它不會洩漏具有晚餐之 RSVP 的人員名稱）。</span><span class="sxs-lookup"><span data-stu-id="f76fb-177">The JsonDinner class exposes a subset of Dinner properties (for example: for security reasons it doesn't disclose the names of the people who have RSVP'd for a dinner).</span></span> <span data-ttu-id="f76fb-178">它也包含不存在晚餐上的 RSVPCount 屬性，而這是透過計算與特定晚餐相關聯的 RSVP 物件數目而動態計算的。</span><span class="sxs-lookup"><span data-stu-id="f76fb-178">It also includes an RSVPCount property that doesn't exist on Dinner– and which is dynamically calculated by counting the number of RSVP objects associated with a particular dinner.</span></span>

<span data-ttu-id="f76fb-179">然後，我們會在控制器基類上使用 Json （） helper 方法，以使用以 JSON 為基礎的電傳格式來傳回 dinners 的順序。</span><span class="sxs-lookup"><span data-stu-id="f76fb-179">We are then using the Json() helper method on the Controller base class to return the sequence of dinners using a JSON-based wire format.</span></span> <span data-ttu-id="f76fb-180">JSON 是一種標準文字格式，可表示簡單的資料結構。</span><span class="sxs-lookup"><span data-stu-id="f76fb-180">JSON is a standard text format for representing simple data-structures.</span></span> <span data-ttu-id="f76fb-181">以下範例顯示兩個 JsonDinner 物件的 JSON 格式清單在從動作方法傳回時的樣子：</span><span class="sxs-lookup"><span data-stu-id="f76fb-181">Below is an example of what a JSON-formatted list of two JsonDinner objects looks like when returned from our action method:</span></span>

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a><span data-ttu-id="f76fb-182">使用 jQuery 呼叫以 JSON 為基礎的 AJAX 方法</span><span class="sxs-lookup"><span data-stu-id="f76fb-182">Calling the JSON-based AJAX method using jQuery</span></span>

<span data-ttu-id="f76fb-183">我們現在已準備好更新 NerdDinner 應用程式的首頁，以使用 SearchController 的 SearchByLocation 動作方法。</span><span class="sxs-lookup"><span data-stu-id="f76fb-183">We are now ready to update the home page of the NerdDinner application to use the SearchController's SearchByLocation action method.</span></span> <span data-ttu-id="f76fb-184">為此，我們會開啟/Views/Home/Index.aspx view 範本並加以更新，使其具有文字方塊、搜尋按鈕、地圖，以及名為 dinnerList 的 &lt;div&gt; 元素：</span><span class="sxs-lookup"><span data-stu-id="f76fb-184">To-do this, we'll open the /Views/Home/Index.aspx view template and update it to have a textbox, search button, our map, and a &lt;div&gt; element named dinnerList:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

<span data-ttu-id="f76fb-185">然後，我們可以將兩個 JavaScript 函式加入至頁面：</span><span class="sxs-lookup"><span data-stu-id="f76fb-185">We can then add two JavaScript functions to the page:</span></span>

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

<span data-ttu-id="f76fb-186">第一個 JavaScript 函式會在第一次載入頁面時載入對應。</span><span class="sxs-lookup"><span data-stu-id="f76fb-186">The first JavaScript function loads the map when the page first loads.</span></span> <span data-ttu-id="f76fb-187">第二個 JavaScript 函式會在 [搜尋] 按鈕上向上連線 JavaScript click 事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="f76fb-187">The second JavaScript function wires up a JavaScript click event handler on the search button.</span></span> <span data-ttu-id="f76fb-188">當按下按鈕時，它會呼叫 FindDinnersGivenLocation （） JavaScript 函式，我們會將其新增至我們的對應 .js 檔案：</span><span class="sxs-lookup"><span data-stu-id="f76fb-188">When the button is pressed it calls the FindDinnersGivenLocation() JavaScript function which we'll add to our Map.js file:</span></span>

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

<span data-ttu-id="f76fb-189">這個 FindDinnersGivenLocation （）函數會呼叫 map。在虛擬地球控制項上尋找（），以將其置入輸入的位置。</span><span class="sxs-lookup"><span data-stu-id="f76fb-189">This FindDinnersGivenLocation() function calls map.Find() on the Virtual Earth Control to center it on the entered location.</span></span> <span data-ttu-id="f76fb-190">當虛擬地球對應服務傳回時，對應。Find （）方法會叫用 callbackUpdateMapDinners 回呼方法，我們傳遞它做為最後的引數。</span><span class="sxs-lookup"><span data-stu-id="f76fb-190">When the virtual earth map service returns, the map.Find() method invokes the callbackUpdateMapDinners callback method we passed it as the final argument.</span></span>

<span data-ttu-id="f76fb-191">CallbackUpdateMapDinners （）方法是實際工作的完成位置。</span><span class="sxs-lookup"><span data-stu-id="f76fb-191">The callbackUpdateMapDinners() method is where the real work is done.</span></span> <span data-ttu-id="f76fb-192">它會使用 jQuery 的 $. post （）協助程式方法，對我們 SearchController 的 SearchByLocation （）動作方法執行 AJAX 呼叫，並將新置中地圖的緯度和經度傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="f76fb-192">It uses jQuery's $.post() helper method to perform an AJAX call to our SearchController's SearchByLocation() action method – passing it the latitude and longitude of the newly centered map.</span></span> <span data-ttu-id="f76fb-193">它會定義一個內嵌函式，當 $ post （） helper 方法完成時將會呼叫，而從 SearchByLocation （）動作方法傳回的 JSON 格式的晚餐結果會使用稱為 "dinners" 的變數傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="f76fb-193">It defines an inline function that will be called when the $.post() helper method completes, and the JSON-formatted dinner results returned from the SearchByLocation() action method will be passed it using a variable called "dinners".</span></span> <span data-ttu-id="f76fb-194">然後，它會對每個傳回的晚餐執行 foreach，並使用晚餐的緯度和經度和其他屬性，在地圖上加入新的 pin。</span><span class="sxs-lookup"><span data-stu-id="f76fb-194">It then does a foreach over each returned dinner, and uses the dinner's latitude and longitude and other properties to add a new pin on the map.</span></span> <span data-ttu-id="f76fb-195">它也會將晚餐專案新增至地圖右邊的 dinners HTML 清單。</span><span class="sxs-lookup"><span data-stu-id="f76fb-195">It also adds a dinner entry to the HTML list of dinners to the right of the map.</span></span> <span data-ttu-id="f76fb-196">然後，它會將圖釘和 HTML 清單的暫留事件進行線路處理，以便在使用者停留在其上方時顯示晚餐的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="f76fb-196">It then wires-up a hover event for both the pushpins and the HTML list so that details about the dinner are displayed when a user hovers over them:</span></span>

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

<span data-ttu-id="f76fb-197">現在當我們執行應用程式並造訪首頁時，我們會看到一個地圖。</span><span class="sxs-lookup"><span data-stu-id="f76fb-197">And now when we run the application and visit the home-page we'll be presented with a map.</span></span> <span data-ttu-id="f76fb-198">當我們輸入城市的名稱時，地圖會顯示附近的近期 dinners：</span><span class="sxs-lookup"><span data-stu-id="f76fb-198">When we enter the name of a city the map will display the upcoming dinners near it:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

<span data-ttu-id="f76fb-199">將滑鼠停留在晚餐上會顯示其相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f76fb-199">Hovering over a dinner will display details about it.</span></span>

<span data-ttu-id="f76fb-200">按一下 [在反升的] 或 [HTML] 清單右邊的晚餐標題，將會導覽到晚餐，我們可以選擇 RSVP 來進行下列動作：</span><span class="sxs-lookup"><span data-stu-id="f76fb-200">Clicking the Dinner title either in the bubble or on the right-hand side in the HTML list will navigate us to the dinner – which we can then optionally RSVP for:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a><span data-ttu-id="f76fb-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f76fb-201">Next Step</span></span>

<span data-ttu-id="f76fb-202">我們現在已實現 NerdDinner 應用程式的所有應用程式功能。</span><span class="sxs-lookup"><span data-stu-id="f76fb-202">We've now implemented all the application functionality of our NerdDinner application.</span></span> <span data-ttu-id="f76fb-203">現在我們來看一下如何啟用它的自動化單元測試。</span><span class="sxs-lookup"><span data-stu-id="f76fb-203">Let's now look at how we can enable automated unit testing of it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f76fb-204">[上一頁](use-ajax-to-deliver-dynamic-updates.md)
> [下一頁](enable-automated-unit-testing.md)</span><span class="sxs-lookup"><span data-stu-id="f76fb-204">[Previous](use-ajax-to-deliver-dynamic-updates.md)
[Next](enable-automated-unit-testing.md)</span></span>
