---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: 伺服器控制項 |Microsoft Docs
author: microsoft
description: ASP.NET 2.0 以許多方式增強伺服器控制項。 在此課程模組中，我們將探討 ASP.NET 2.0 和 Visual Studio 200 ... 的一些架構變更。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: c02a633013f061c09141d4f98871848c011a799e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641439"
---
# <a name="server-controls"></a><span data-ttu-id="3da98-104">伺服器控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-104">Server Controls</span></span>

<span data-ttu-id="3da98-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3da98-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="3da98-106">ASP.NET 2.0 以許多方式增強伺服器控制項。</span><span class="sxs-lookup"><span data-stu-id="3da98-106">ASP.NET 2.0 enhances server controls in many ways.</span></span> <span data-ttu-id="3da98-107">在此課程模組中，我們將探討 ASP.NET 2.0 和 Visual Studio 2005 處理伺服器控制項的方式的一些架構變更。</span><span class="sxs-lookup"><span data-stu-id="3da98-107">In this module, we'll cover some of the architectural changes to the way ASP.NET 2.0 and Visual Studio 2005 deals with server controls.</span></span>

<span data-ttu-id="3da98-108">ASP.NET 2.0 以許多方式增強伺服器控制項。</span><span class="sxs-lookup"><span data-stu-id="3da98-108">ASP.NET 2.0 enhances server controls in many ways.</span></span> <span data-ttu-id="3da98-109">在此課程模組中，我們將探討 ASP.NET 2.0 和 Visual Studio 2005 處理伺服器控制項的方式的一些架構變更。</span><span class="sxs-lookup"><span data-stu-id="3da98-109">In this module, we'll cover some of the architectural changes to the way ASP.NET 2.0 and Visual Studio 2005 deals with server controls.</span></span>

## <a name="view-state"></a><span data-ttu-id="3da98-110">檢視狀態</span><span class="sxs-lookup"><span data-stu-id="3da98-110">View state</span></span>

<span data-ttu-id="3da98-111">ASP.NET 2.0 中檢視狀態的主要變更，大小大幅縮減。</span><span class="sxs-lookup"><span data-stu-id="3da98-111">The primary change in view state in ASP.NET 2.0 is a dramatic reduction in size.</span></span> <span data-ttu-id="3da98-112">假設有一個頁面上只有一個行事曆控制項。</span><span class="sxs-lookup"><span data-stu-id="3da98-112">Consider a page with only a Calendar control on it.</span></span> <span data-ttu-id="3da98-113">以下是 ASP.NET 1.1 中的檢視狀態。</span><span class="sxs-lookup"><span data-stu-id="3da98-113">Here is the view state in ASP.NET 1.1.</span></span>

[!code-css[Main](server-controls/samples/sample1.css)]

<span data-ttu-id="3da98-114">這現在是 ASP.NET 2.0 中相同頁面的檢視狀態。</span><span class="sxs-lookup"><span data-stu-id="3da98-114">Now here's the view state on an identical page in ASP.NET 2.0.</span></span>

[!code-css[Main](server-controls/samples/sample2.css)]

<span data-ttu-id="3da98-115">這是相當重要的變更，並考慮到該檢視狀態是透過網路來回執行，這種變更可以讓開發人員大幅提升效能。</span><span class="sxs-lookup"><span data-stu-id="3da98-115">That's a pretty significant change, and considering that view state is carried back and forth over the wire, this change can give developers a significant performance increase.</span></span> <span data-ttu-id="3da98-116">減少檢視狀態的大小，主要是因為我們在內部處理它的方式。</span><span class="sxs-lookup"><span data-stu-id="3da98-116">The reduction in size of view state is largely due to the way that we handle it internally.</span></span> <span data-ttu-id="3da98-117">請記住，檢視狀態是 Base64 編碼的字串。</span><span class="sxs-lookup"><span data-stu-id="3da98-117">Remember that view state is a Base64 encoded string.</span></span> <span data-ttu-id="3da98-118">為了進一步瞭解 ASP.NET 2.0 中 view 狀態的變更，讓我們先看一下上述範例中的解碼值。</span><span class="sxs-lookup"><span data-stu-id="3da98-118">To better understand the change in view state in ASP.NET 2.0, let's have a look at the decoded values from the examples above.</span></span>

<span data-ttu-id="3da98-119">以下是已解碼的 1.1 view 狀態：</span><span class="sxs-lookup"><span data-stu-id="3da98-119">Here is the 1.1 view state decoded:</span></span>

[!code-css[Main](server-controls/samples/sample3.css)]

<span data-ttu-id="3da98-120">這看起來有點像雜亂的內容，但這裡有一個模式。</span><span class="sxs-lookup"><span data-stu-id="3da98-120">This may look a bit like gibberish, but there is a pattern here.</span></span> <span data-ttu-id="3da98-121">在 ASP.NET 1.x 中，我們使用了單一字元來識別資料類型，並使用 &lt;的 &gt; 字元來分隔值。</span><span class="sxs-lookup"><span data-stu-id="3da98-121">In ASP.NET 1.x, we used single characters to identify data-types and delimited values using the &lt;&gt; characters.</span></span> <span data-ttu-id="3da98-122">上述檢視狀態範例中的 "t" 代表三元。</span><span class="sxs-lookup"><span data-stu-id="3da98-122">The "t" in the view state sample above represents a Triplet.</span></span> <span data-ttu-id="3da98-123">三元包含一對 ArrayLists （"l" 代表 ArrayList）。其中一個 ArrayLists 包含 Int32 （"i"），其值為1，另一個則包含另一個三元。</span><span class="sxs-lookup"><span data-stu-id="3da98-123">The Triplet contains a pair of ArrayLists (the "l" represents an ArrayList.) One of those ArrayLists contains an Int32 ("i") with a value of 1 and the other contains another Triplet.</span></span> <span data-ttu-id="3da98-124">三元包含一對 ArrayLists 等等。要記住的重點是，我們使用包含配對的 Triplet，我們會透過字母來識別資料類型，而我們會使用 &lt; 並 &gt; 字元做為分隔符號。</span><span class="sxs-lookup"><span data-stu-id="3da98-124">The Triplet contains a pair of ArrayLists, etc. The important thing to remember is that we use Triplets that contain pairs, we identify the data-types via a letter, and we use the &lt; and &gt; characters as delimiters.</span></span>

<span data-ttu-id="3da98-125">在 ASP.NET 2.0 中，解碼的檢視狀態看起來有點不同。</span><span class="sxs-lookup"><span data-stu-id="3da98-125">In ASP.NET 2.0, the decoded view state looks a bit different.</span></span>

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

<span data-ttu-id="3da98-126">您應該會注意到解碼檢視狀態的外觀有很大的變化。</span><span class="sxs-lookup"><span data-stu-id="3da98-126">You should notice a huge change in the appearance of the decoded view state.</span></span> <span data-ttu-id="3da98-127">這項變更有數個架構結構性支援。</span><span class="sxs-lookup"><span data-stu-id="3da98-127">This change has several architectural underpinnings.</span></span> <span data-ttu-id="3da98-128">ASP.NET 1.x 中的 View 狀態使用 LosFormatter 來序列化資料。</span><span class="sxs-lookup"><span data-stu-id="3da98-128">View state in ASP.NET 1.x used the LosFormatter to serialize data.</span></span> <span data-ttu-id="3da98-129">在2.0 中，我們使用新的 ObjectStateFormatter 類別。</span><span class="sxs-lookup"><span data-stu-id="3da98-129">In 2.0, we use the new ObjectStateFormatter class.</span></span> <span data-ttu-id="3da98-130">這個類別是特別設計來協助序列化和還原序列化檢視狀態和控制項狀態。</span><span class="sxs-lookup"><span data-stu-id="3da98-130">This class was specifically designed to aid in the serialization and deserialization of view state and control state.</span></span> <span data-ttu-id="3da98-131">（下一節將涵蓋控制狀態）。藉由變更序列化和還原序列化進行的方法，可以獲得許多好處。</span><span class="sxs-lookup"><span data-stu-id="3da98-131">(Control state will be covered in the next section.) There are many benefits gained by changing the method by which serialization and deserialization take place.</span></span> <span data-ttu-id="3da98-132">其中一個最顯著的事實是，不同于使用了不正確 LosFormatter，ObjectStateFormatter 會使用 BinaryWriter。</span><span class="sxs-lookup"><span data-stu-id="3da98-132">One of the most dramatic is the fact that unlike the LosFormatter which uses a TextWriter, the ObjectStateFormatter uses a BinaryWriter.</span></span> <span data-ttu-id="3da98-133">這可讓 ASP.NET 2.0 儲存檢視狀態一系列的位元組，而不是字串。</span><span class="sxs-lookup"><span data-stu-id="3da98-133">This allows ASP.NET 2.0 to store view state a series of bytes instead of strings.</span></span> <span data-ttu-id="3da98-134">例如，取得整數。</span><span class="sxs-lookup"><span data-stu-id="3da98-134">Take, for example, an integer.</span></span> <span data-ttu-id="3da98-135">在 ASP.NET 1.1 中，整數需要4個位元組的檢視狀態。</span><span class="sxs-lookup"><span data-stu-id="3da98-135">In ASP.NET 1.1, an integer required 4 bytes of view state.</span></span> <span data-ttu-id="3da98-136">在 ASP.NET 2.0 中，相同的整數只需要1個位元組。</span><span class="sxs-lookup"><span data-stu-id="3da98-136">In ASP.NET 2.0, that same integer only requires 1 byte.</span></span> <span data-ttu-id="3da98-137">已進行其他增強，以減少所儲存的檢視狀態量。</span><span class="sxs-lookup"><span data-stu-id="3da98-137">Other enhancements were made to decrease the amount of view state that is stored.</span></span> <span data-ttu-id="3da98-138">例如，日期時間值現在會使用 TickCount （而非字串）來儲存。</span><span class="sxs-lookup"><span data-stu-id="3da98-138">DateTime values, for example, are now stored using a TickCount instead of a string.</span></span>

<span data-ttu-id="3da98-139">就像這樣的一切都不夠，因為1.x 的其中一個最大取用者是 DataGrid 和類似的控制項，所以會特別注意。</span><span class="sxs-lookup"><span data-stu-id="3da98-139">As if all of that weren't enough, special attention was paid to the fact that one of the greatest consumers of view state in 1.x was the DataGrid and similar controls.</span></span> <span data-ttu-id="3da98-140">控制項的主要缺點，像是 DataGrid 的檢視狀態，其中通常包含大量重複的資訊。</span><span class="sxs-lookup"><span data-stu-id="3da98-140">A major drawback of controls such as the DataGrid where view state is concerned is that it often contains large amounts of repeated information.</span></span> <span data-ttu-id="3da98-141">在 ASP.NET 1.x 中，重複的資訊會一次直接儲存，而導致膨脹檢視狀態。</span><span class="sxs-lookup"><span data-stu-id="3da98-141">In ASP.NET 1.x, that repeated information was simply stored over and over again resulting in a bloated view state.</span></span> <span data-ttu-id="3da98-142">在 ASP.NET 2.0 中，我們使用新的 IndexedString 類別來儲存這類資料。</span><span class="sxs-lookup"><span data-stu-id="3da98-142">In ASP.NET 2.0, we use the new IndexedString class to store such data.</span></span> <span data-ttu-id="3da98-143">如果字串重複，我們只會將 IndexedString 的 token 和索引儲存在 IndexedString 物件的執行中資料表內。</span><span class="sxs-lookup"><span data-stu-id="3da98-143">If a string repeats, we just store the token for the IndexedString and the index within a running table of IndexedString objects.</span></span>

## <a name="control-state"></a><span data-ttu-id="3da98-144">控制項狀態</span><span class="sxs-lookup"><span data-stu-id="3da98-144">Control State</span></span>

<span data-ttu-id="3da98-145">開發人員具有「視圖」狀態的主要傾聽牢騷之一，就是它加入至 HTTP 承載的大小。</span><span class="sxs-lookup"><span data-stu-id="3da98-145">One of the major gripes that developers had with view state was the size that it added to the HTTP payload.</span></span> <span data-ttu-id="3da98-146">如先前所述，檢視狀態的最大取用者之一就是 DataGrid 控制項。</span><span class="sxs-lookup"><span data-stu-id="3da98-146">As previously mentioned, one of the greatest consumers of view state is the DataGrid control.</span></span> <span data-ttu-id="3da98-147">為了避免 DataGrid 產生大量的檢視狀態，許多開發人員只會停用該控制項的檢視狀態。</span><span class="sxs-lookup"><span data-stu-id="3da98-147">To avoid the huge amounts of view state generated by a DataGrid, many developers simply disabled view state for that control.</span></span> <span data-ttu-id="3da98-148">可惜的是，該解決方案並不一定是一個好用的。</span><span class="sxs-lookup"><span data-stu-id="3da98-148">Unfortunately, that solution wasn't always a good one.</span></span> <span data-ttu-id="3da98-149">ASP.NET 1.x 中的 View 狀態不僅包含控制項的正確功能所需的資料。</span><span class="sxs-lookup"><span data-stu-id="3da98-149">View state in ASP.NET 1.x contains not only data necessary for the correct functionality of the control.</span></span> <span data-ttu-id="3da98-150">其中也包含有關控制項 UI 狀態的資訊。</span><span class="sxs-lookup"><span data-stu-id="3da98-150">It also contains information concerning the state of the control's UI.</span></span> <span data-ttu-id="3da98-151">這表示如果您想要允許在 DataGrid 上進行分頁，即使您不需要所有檢視狀態包含的 UI 資訊，還是必須啟用 view 狀態。</span><span class="sxs-lookup"><span data-stu-id="3da98-151">This means that if you want to allow for pagination on a DataGrid, you must enable view state even if you don't need all of the UI information that view state contains.</span></span> <span data-ttu-id="3da98-152">這是一種全有或全無的案例。</span><span class="sxs-lookup"><span data-stu-id="3da98-152">It's an all-or-nothing scenario.</span></span>

<span data-ttu-id="3da98-153">在 ASP.NET 2.0 中，控制狀態會透過引進控制項狀態來解決此問題。</span><span class="sxs-lookup"><span data-stu-id="3da98-153">In ASP.NET 2.0, control state solves that problem nicely via the introduction of control state.</span></span> <span data-ttu-id="3da98-154">控制項狀態包含控制項適當功能絕對必要的資料。</span><span class="sxs-lookup"><span data-stu-id="3da98-154">Control state contains the data that is absolutely necessary for the proper functionality of a control.</span></span> <span data-ttu-id="3da98-155">不同于 view 狀態，控制項狀態無法停用。</span><span class="sxs-lookup"><span data-stu-id="3da98-155">Unlike view state, control state cannot be disabled.</span></span> <span data-ttu-id="3da98-156">因此，請務必小心地控制儲存在控制狀態中的資料。</span><span class="sxs-lookup"><span data-stu-id="3da98-156">Therefore, it is important that the data being stored in control state is carefully controlled.</span></span>

> [!NOTE]
> <span data-ttu-id="3da98-157">控制項狀態會隨著檢視狀態保存在 [\_\_VIEWSTATE 隱藏的表單] 欄位中。</span><span class="sxs-lookup"><span data-stu-id="3da98-157">Control state is persisted along with the view state in the \_\_VIEWSTATE hidden form field.</span></span>

<span data-ttu-id="3da98-158">這段影片是觀看狀態和控制狀態的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="3da98-158">This video is a walkthrough of view state and control state.</span></span>

![](server-controls/_static/image1.png)

[<span data-ttu-id="3da98-159">開啟全螢幕影片</span><span class="sxs-lookup"><span data-stu-id="3da98-159">Open Full-Screen Video</span></span>](server-controls/_static/state1.wmv)

<span data-ttu-id="3da98-160">為了讓伺服器控制項能夠讀取和寫入控制狀態，您必須執行三個步驟。</span><span class="sxs-lookup"><span data-stu-id="3da98-160">In order for a server control to read and write to control state, you must take three steps.</span></span>

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a><span data-ttu-id="3da98-161">步驟1：呼叫 RegisterRequiresControlState 方法</span><span class="sxs-lookup"><span data-stu-id="3da98-161">Step 1: Call the RegisterRequiresControlState Method</span></span>

<span data-ttu-id="3da98-162">RegisterRequiresControlState 方法會通知 ASP.NET 控制項需要保存控制項狀態。</span><span class="sxs-lookup"><span data-stu-id="3da98-162">The RegisterRequiresControlState method informs ASP.NET that a control needs to persist control state.</span></span> <span data-ttu-id="3da98-163">它接受一個 type 控制項的引數，也就是要註冊的控制項。</span><span class="sxs-lookup"><span data-stu-id="3da98-163">It takes one argument of type Control which is the control that is being registered.</span></span>

<span data-ttu-id="3da98-164">請務必注意，註冊不會從要求中保存。</span><span class="sxs-lookup"><span data-stu-id="3da98-164">It is important to note that registration does not persist from request to request.</span></span> <span data-ttu-id="3da98-165">因此，如果控制項要保存控制項狀態，就必須在每個要求上呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="3da98-165">Therefore, this method must be called on every request if a control is to persist control state.</span></span> <span data-ttu-id="3da98-166">建議您在 OnInit 中呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="3da98-166">It is recommended that the method be called in OnInit.</span></span>

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a><span data-ttu-id="3da98-167">步驟2：覆寫 SaveControlState</span><span class="sxs-lookup"><span data-stu-id="3da98-167">Step 2: Override SaveControlState</span></span>

<span data-ttu-id="3da98-168">SaveControlState 方法會在最後一次回傳後，儲存控制項的控制項狀態變更。</span><span class="sxs-lookup"><span data-stu-id="3da98-168">The SaveControlState method saves control state changes for a control since the last post back.</span></span> <span data-ttu-id="3da98-169">它會傳回代表控制項狀態的物件。</span><span class="sxs-lookup"><span data-stu-id="3da98-169">It returns an object representing the control's state.</span></span>

## <a name="step-3-override-loadcontrolstate"></a><span data-ttu-id="3da98-170">步驟3：覆寫 LoadControlState</span><span class="sxs-lookup"><span data-stu-id="3da98-170">Step 3: Override LoadControlState</span></span>

<span data-ttu-id="3da98-171">LoadControlState 方法會將儲存的狀態載入控制項。</span><span class="sxs-lookup"><span data-stu-id="3da98-171">The LoadControlState method loads saved state into a control.</span></span> <span data-ttu-id="3da98-172">方法會接受一個型別物件的引數，以保存控制項的儲存狀態。</span><span class="sxs-lookup"><span data-stu-id="3da98-172">The method takes one argument of type Object which holds the saved state for the control.</span></span>

## <a name="full-xhtml-compliance"></a><span data-ttu-id="3da98-173">完整的 XHTML 合規性</span><span class="sxs-lookup"><span data-stu-id="3da98-173">Full XHTML Compliance</span></span>

<span data-ttu-id="3da98-174">任何 Web 開發人員都知道 Web 應用程式中標準的重要性。</span><span class="sxs-lookup"><span data-stu-id="3da98-174">Any Web developer knows the importance of standards in Web applications.</span></span> <span data-ttu-id="3da98-175">為了維護以標準為基礎的開發環境，ASP.NET 2.0 完全符合 XHTML 標準。</span><span class="sxs-lookup"><span data-stu-id="3da98-175">In order to maintain a standards-based development environment, ASP.NET 2.0 is fully XHTML compliant.</span></span> <span data-ttu-id="3da98-176">因此，所有標記都是根據瀏覽器中支援 HTML 4.0 或更高版本的 XHTML 標準來呈現。</span><span class="sxs-lookup"><span data-stu-id="3da98-176">Therefore, all tags are rendered according to XHTML standards in browsers that support HTML 4.0 or greater.</span></span>

<span data-ttu-id="3da98-177">ASP.NET 1.1 中的 DOCTYPE 定義如下所示：</span><span class="sxs-lookup"><span data-stu-id="3da98-177">The DOCTYPE definition in ASP.NET 1.1 was as follows:</span></span>

[!code-html[Main](server-controls/samples/sample6.html)]

<span data-ttu-id="3da98-178">在 ASP.NET 2.0 中，預設的 DOCTYPE 定義如下所示：</span><span class="sxs-lookup"><span data-stu-id="3da98-178">In ASP.NET 2.0, the default DOCTYPE definition is as follows:</span></span>

[!code-html[Main](server-controls/samples/sample7.html)]

<span data-ttu-id="3da98-179">如果您選擇，您可以透過設定檔中的 [xhtmlConformance] 節點來改變預設的 XHTML 合規性。</span><span class="sxs-lookup"><span data-stu-id="3da98-179">If you choose, you can alter the default XHTML compliance via the xhtmlConformance node in the configuration file.</span></span> <span data-ttu-id="3da98-180">例如，web.config 檔案中的下列節點會將 XHTML 符合性變更為 XHTML 1.0 Strict：</span><span class="sxs-lookup"><span data-stu-id="3da98-180">For example, the following node in the web.config file will change XHTML compliance to XHTML 1.0 Strict:</span></span>

[!code-xml[Main](server-controls/samples/sample8.xml)]

<span data-ttu-id="3da98-181">如果您選擇，您也可以將 ASP.NET 設定成使用 ASP.NET 1.x 中使用的舊版設定，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3da98-181">If you choose, you can also configure ASP.NET to use the legacy configuration used in ASP.NET 1.x as follows:</span></span>

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a><span data-ttu-id="3da98-182">使用介面卡的自動調整轉譯</span><span class="sxs-lookup"><span data-stu-id="3da98-182">Adaptive Rendering Using Adapters</span></span>

<span data-ttu-id="3da98-183">在 ASP.NET 1.x 中，設定檔包含已填入 HttpBrowserCapabilities 物件的 &lt;browserCaps&gt; 區段。</span><span class="sxs-lookup"><span data-stu-id="3da98-183">In ASP.NET 1.x, the configuration file contained a &lt;browserCaps&gt; section that populated a HttpBrowserCapabilities object.</span></span> <span data-ttu-id="3da98-184">此物件可讓開發人員判斷哪個裝置正在進行特定的要求，並適當地轉譯程式碼。</span><span class="sxs-lookup"><span data-stu-id="3da98-184">This object allowed a developer to determine what device is making a particular request and render code appropriately.</span></span> <span data-ttu-id="3da98-185">在 ASP.NET 2.0 中，模型已經過改良，現在使用新的 ControlAdapter 類別。</span><span class="sxs-lookup"><span data-stu-id="3da98-185">In ASP.NET 2.0, the model has improved and now uses the new ControlAdapter class.</span></span> <span data-ttu-id="3da98-186">ControlAdapter 類別會覆寫控制項生命週期中的事件，並根據使用者代理程式的功能來控制控制項的呈現。</span><span class="sxs-lookup"><span data-stu-id="3da98-186">The ControlAdapter class overrides events in the control's lifecycle and controls the rendering of controls based upon the user agent's capabilities.</span></span> <span data-ttu-id="3da98-187">特定使用者代理程式的功能是由儲存在 c:\windows\microsoft.net\framework\v2.0. 中的瀏覽器定義檔案（副檔名為. 瀏覽器）所定義\*\*\*\*\CONFIG\Browsers 資料夾。</span><span class="sxs-lookup"><span data-stu-id="3da98-187">The capabilities of a specific user agent are defined by a browser definition file (a file with a .browser file extension) stored in the c:\windows\microsoft.net\framework\v2.0.\*\*\*\*\CONFIG\Browsers folder.</span></span>

> [!NOTE]
> <span data-ttu-id="3da98-188">ControlAdapter 類別是抽象類別。</span><span class="sxs-lookup"><span data-stu-id="3da98-188">The ControlAdapter class is an abstract class.</span></span>

<span data-ttu-id="3da98-189">瀏覽器定義檔與1.x 中的 &lt;browserCaps&gt; 區段非常類似，它會使用正則運算式來剖析使用者代理字串，以識別要求的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="3da98-189">Much like the &lt;browserCaps&gt; section in 1.x, the browser definition file uses a Regular Expression to parse the user agent string in order to identify the requesting browser.</span></span> <span data-ttu-id="3da98-190">其會定義該使用者代理程式的特定功能。</span><span class="sxs-lookup"><span data-stu-id="3da98-190">It them defines particular capabilities for that user agent.</span></span> <span data-ttu-id="3da98-191">ControlAdapter 會透過 Render 方法呈現控制項。</span><span class="sxs-lookup"><span data-stu-id="3da98-191">The ControlAdapter renders the control via the Render method.</span></span> <span data-ttu-id="3da98-192">因此，如果您覆寫 Render 方法，則不應該在基類上呼叫 Render。</span><span class="sxs-lookup"><span data-stu-id="3da98-192">Therefore, if you override the Render method, you should not call Render on the base class.</span></span> <span data-ttu-id="3da98-193">這麼做可能會導致轉譯出現兩次，一次用於介面卡，一次用於控制項本身。</span><span class="sxs-lookup"><span data-stu-id="3da98-193">Doing so may cause rendering to occur twice, once for the adapter and once for the control itself.</span></span>

## <a name="developing-a-custom-adapter"></a><span data-ttu-id="3da98-194">開發自訂介面卡</span><span class="sxs-lookup"><span data-stu-id="3da98-194">Developing a Custom Adapter</span></span>

<span data-ttu-id="3da98-195">您可以從 ControlAdapter 繼承，以開發自己的自訂介面卡。</span><span class="sxs-lookup"><span data-stu-id="3da98-195">You can develop your own custom adapter by inheriting from ControlAdapter.</span></span> <span data-ttu-id="3da98-196">此外，您可以在頁面需要介面卡的情況下，從抽象類別 PageAdapter 繼承。</span><span class="sxs-lookup"><span data-stu-id="3da98-196">Additionally, you can inherit from the abstract class PageAdapter in cases where an adapter is needed for a page.</span></span> <span data-ttu-id="3da98-197">將控制項對應至自訂介面卡，是透過瀏覽器定義檔中的 &lt;controlAdapters&gt; 元素來完成。</span><span class="sxs-lookup"><span data-stu-id="3da98-197">Mapping of controls to your custom adapter is accomplished via the &lt;controlAdapters&gt; element in the browser definition file.</span></span> <span data-ttu-id="3da98-198">例如，瀏覽器定義檔案中的下列 XML 會將 Menu 控制項對應至 MenuAdapter 類別：</span><span class="sxs-lookup"><span data-stu-id="3da98-198">For example, the following XML from a browser definition file maps the Menu control to the MenuAdapter class:</span></span>

[!code-html[Main](server-controls/samples/sample10.html)]

<span data-ttu-id="3da98-199">使用此模型，控制項開發人員就會變得相當容易，以特定裝置或瀏覽器為目標。</span><span class="sxs-lookup"><span data-stu-id="3da98-199">Using this model, it becomes quite easy for a control developer to target a particular device or browser.</span></span> <span data-ttu-id="3da98-200">開發人員也可以完全掌控每個裝置上頁面的呈現方式，這也相當簡單。</span><span class="sxs-lookup"><span data-stu-id="3da98-200">It's also quite simple for a developer to have complete control over how pages render on every device.</span></span>

## <a name="per-device-rendering"></a><span data-ttu-id="3da98-201">每一裝置轉譯</span><span class="sxs-lookup"><span data-stu-id="3da98-201">Per-Device Rendering</span></span>

<span data-ttu-id="3da98-202">ASP.NET 2.0 中的伺服器控制項屬性可以使用瀏覽器特定的前置詞來指定給每一裝置。</span><span class="sxs-lookup"><span data-stu-id="3da98-202">Server control properties in ASP.NET 2.0 can be specified per-device using a browser-specific prefix.</span></span> <span data-ttu-id="3da98-203">例如，下列程式碼將會根據用來流覽頁面的裝置，變更標籤的文字。</span><span class="sxs-lookup"><span data-stu-id="3da98-203">For example, the code below will change the Text of a label depending upon which device is being used to browse the page.</span></span>

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

<span data-ttu-id="3da98-204">當包含此標籤的頁面從 Internet Explorer 流覽時，標籤會顯示「您是從 Internet Explorer 流覽」文字。</span><span class="sxs-lookup"><span data-stu-id="3da98-204">When the page containing this label is browsed from Internet Explorer, the label will display text saying "You are browsing from Internet Explorer."</span></span> <span data-ttu-id="3da98-205">從 Firefox 流覽頁面時，標籤會顯示「您正從 Firefox 流覽」的文字。</span><span class="sxs-lookup"><span data-stu-id="3da98-205">When the page is browsed from Firefox, the label will display the text "You are browsing from Firefox."</span></span> <span data-ttu-id="3da98-206">當您從任何其他裝置流覽頁面時，它會顯示「您是從未知的裝置流覽」。</span><span class="sxs-lookup"><span data-stu-id="3da98-206">When the page is browsed from any other device, it will display "You are browsing from an unknown device."</span></span> <span data-ttu-id="3da98-207">您可以使用這個特殊語法來指定任何屬性。</span><span class="sxs-lookup"><span data-stu-id="3da98-207">Any property can be specified using this special syntax.</span></span>

## <a name="setting-focus"></a><span data-ttu-id="3da98-208">設定焦點</span><span class="sxs-lookup"><span data-stu-id="3da98-208">Setting Focus</span></span>

<span data-ttu-id="3da98-209">ASP.NET 1.x 開發人員經常會詢問如何設定特定控制項的初始焦點。</span><span class="sxs-lookup"><span data-stu-id="3da98-209">ASP.NET 1.x developers frequently asked about how to set initial focus on a particular control.</span></span> <span data-ttu-id="3da98-210">例如，在登入頁面上，讓 [使用者識別碼] 文字方塊在頁面第一次載入時取得焦點會很有用。</span><span class="sxs-lookup"><span data-stu-id="3da98-210">For example, on a login page, it's useful to have the User ID textbox get the focus when the page first loads.</span></span> <span data-ttu-id="3da98-211">在 ASP.NET 1.x 中，執行這項作業需要撰寫一些用戶端腳本。</span><span class="sxs-lookup"><span data-stu-id="3da98-211">In ASP.NET 1.x, doing this required writing some client-side script.</span></span> <span data-ttu-id="3da98-212">雖然這類腳本是一項簡單的工作，但由於 SetFocus 方法，因此在 ASP.NET 2.0 中已不再需要。</span><span class="sxs-lookup"><span data-stu-id="3da98-212">Even though such a script is a trivial task, it's no longer necessary in ASP.NET 2.0 thanks to the SetFocus method.</span></span> <span data-ttu-id="3da98-213">SetFocus 方法會採用一個引數，表示應接收焦點的控制項。</span><span class="sxs-lookup"><span data-stu-id="3da98-213">The SetFocus method takes one argument indicating the control that should receive focus.</span></span> <span data-ttu-id="3da98-214">這個引數可以是做為字串的控制項的用戶端識別碼，或是做為控制項物件的伺服器控制項名稱。</span><span class="sxs-lookup"><span data-stu-id="3da98-214">This argument can either be the client ID of the control as a string or the name of the Server control as a Control object.</span></span> <span data-ttu-id="3da98-215">例如，若要在第一次載入頁面時將初始焦點設定為 TextBox 控制項，請將下列程式碼新增至頁面\_載入：</span><span class="sxs-lookup"><span data-stu-id="3da98-215">For example, to set the initial focus to a TextBox control called txtUserID when the page first loads, add the following code to Page\_Load:</span></span>

[!code-csharp[Main](server-controls/samples/sample12.cs)]

<span data-ttu-id="3da98-216">--或</span><span class="sxs-lookup"><span data-stu-id="3da98-216">-- or</span></span>

[!code-csharp[Main](server-controls/samples/sample13.cs)]

<span data-ttu-id="3da98-217">ASP.NET 2.0 使用 Webresource 處理常式（先前討論過）來呈現設定焦點的用戶端函式。</span><span class="sxs-lookup"><span data-stu-id="3da98-217">ASP.NET 2.0 uses the Webresource.axd handler (discussed previously) to render a client-side function that sets the focus.</span></span> <span data-ttu-id="3da98-218">用戶端函式的名稱是 WebForm\_自動對焦，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3da98-218">The name of the client-side function is WebForm\_AutoFocus as shown here:</span></span>

[!code-html[Main](server-controls/samples/sample14.html)]

<span data-ttu-id="3da98-219">或者，您可以使用控制項的焦點方法，將初始焦點設定為該控制項。</span><span class="sxs-lookup"><span data-stu-id="3da98-219">Alternatively, you can use the Focus method for a control to set the initial focus to that control.</span></span> <span data-ttu-id="3da98-220">Focus 方法衍生自控制項類別，並可供所有 ASP.NET 2.0 控制項使用。</span><span class="sxs-lookup"><span data-stu-id="3da98-220">The Focus method derives from the Control class and is available to all ASP.NET 2.0 controls.</span></span> <span data-ttu-id="3da98-221">當發生驗證錯誤時，也可以將焦點設定至特定的控制項。</span><span class="sxs-lookup"><span data-stu-id="3da98-221">It is also possible to set focus to a particular control when a validation error occurs.</span></span> <span data-ttu-id="3da98-222">這將在稍後的課程模組中討論。</span><span class="sxs-lookup"><span data-stu-id="3da98-222">That will be covered in a later module.</span></span>

## <a name="new-server-controls-in-aspnet-20"></a><span data-ttu-id="3da98-223">ASP.NET 2.0 中的新伺服器控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-223">New Server Controls in ASP.NET 2.0</span></span>

<span data-ttu-id="3da98-224">以下是 ASP.NET 2.0 中的新伺服器控制項。</span><span class="sxs-lookup"><span data-stu-id="3da98-224">The following are new server controls in ASP.NET 2.0.</span></span> <span data-ttu-id="3da98-225">我們將在稍後的課程模組中深入瞭解其中的部分。</span><span class="sxs-lookup"><span data-stu-id="3da98-225">We will go into more detail on some of them in later modules.</span></span>

## <a name="imagemap-control"></a><span data-ttu-id="3da98-226">ImageMap 控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-226">ImageMap Control</span></span>

<span data-ttu-id="3da98-227">ImageMap 控制項可讓您將作用區新增至可起始回傳或流覽至 URL 的影像。</span><span class="sxs-lookup"><span data-stu-id="3da98-227">The ImageMap control allows you to add hotspots to an image that can initiate a post back or navigate to a URL.</span></span> <span data-ttu-id="3da98-228">有三種可用的熱點類型;[Circlehotspot]、RectangleHotSpot 和 PolygonHotSpot。</span><span class="sxs-lookup"><span data-stu-id="3da98-228">There are three types of hotspots available; CircleHotSpot, RectangleHotSpot, and PolygonHotSpot.</span></span> <span data-ttu-id="3da98-229">在 Visual Studio 中或以程式設計方式，透過程式碼來新增熱點。</span><span class="sxs-lookup"><span data-stu-id="3da98-229">Hotspots are added via a collection editor in Visual Studio or programmatically in code.</span></span> <span data-ttu-id="3da98-230">沒有任何使用者介面可用來在影像上繪製作用區。</span><span class="sxs-lookup"><span data-stu-id="3da98-230">There is no user-interface available for drawing hotspots on an image.</span></span> <span data-ttu-id="3da98-231">作用點的座標和大小或半徑必須以宣告方式指定。</span><span class="sxs-lookup"><span data-stu-id="3da98-231">The coordinates and size or radius of the hotspot must be specified declaratively.</span></span> <span data-ttu-id="3da98-232">在設計工具中，熱點也沒有視覺標記法。</span><span class="sxs-lookup"><span data-stu-id="3da98-232">There is also no visual representation of a hotspot in the designer.</span></span> <span data-ttu-id="3da98-233">如果將作用點設定為流覽至 URL，則會透過作用點的 NavigateUrl 屬性來指定 URL。</span><span class="sxs-lookup"><span data-stu-id="3da98-233">If a hotspot is configured to navigate to a URL, the URL is specified via the NavigateUrl property of the hotspot.</span></span> <span data-ttu-id="3da98-234">在回傳後的熱點案例中，PostBackValue 屬性可讓您傳遞回傳中的字串，以便在伺服器端程式碼中抓取。</span><span class="sxs-lookup"><span data-stu-id="3da98-234">In the case of a post back hotspot, the PostBackValue property allows you to pass a string in the post back that can be retrieved in server-side code.</span></span>

![Visual Studio 中的作用點集合編輯器](server-controls/_static/image1.jpg)

<span data-ttu-id="3da98-236">**圖 1**： Visual Studio 中的作用點集合編輯器</span><span class="sxs-lookup"><span data-stu-id="3da98-236">**Figure 1**: HotSpot Collection Editor in Visual Studio</span></span>

## <a name="bulletedlist-control"></a><span data-ttu-id="3da98-237">BulletedList 控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-237">BulletedList Control</span></span>

<span data-ttu-id="3da98-238">BulletedList 控制項是可輕鬆地系結資料的項目符號清單。</span><span class="sxs-lookup"><span data-stu-id="3da98-238">The BulletedList control is a bulleted list that can easily be data bound.</span></span> <span data-ttu-id="3da98-239">您可以透過 BulletStyle 屬性來排序（編號）或未排序清單。</span><span class="sxs-lookup"><span data-stu-id="3da98-239">The list can be ordered (numbered) or unordered via the BulletStyle property.</span></span> <span data-ttu-id="3da98-240">清單中的每個專案都是以「內容」物件表示。</span><span class="sxs-lookup"><span data-stu-id="3da98-240">Each item in the list is represented by a ListItem object.</span></span>

![Visual Studio 中的 BulletedList 控制項](server-controls/_static/image1.gif)

<span data-ttu-id="3da98-242">**圖 2**： Visual Studio 中的 BulletedList 控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-242">**Figure 2**: BulletedList Control in Visual Studio</span></span>

## <a name="hiddenfield-control"></a><span data-ttu-id="3da98-243">HiddenField 控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-243">HiddenField Control</span></span>

<span data-ttu-id="3da98-244">HiddenField 控制項會將隱藏的表單欄位加入至您的頁面中，其值可在伺服器端程式碼中使用。</span><span class="sxs-lookup"><span data-stu-id="3da98-244">The HiddenField control adds a hidden form field to your page, the value of which is available in server-side code.</span></span> <span data-ttu-id="3da98-245">隱藏的表單欄位值通常會在 post 備份之間保持不變。</span><span class="sxs-lookup"><span data-stu-id="3da98-245">The value of a hidden form field is generally expected to remain unchanged between post backs.</span></span> <span data-ttu-id="3da98-246">不過，惡意使用者可能會在回傳之前變更值。</span><span class="sxs-lookup"><span data-stu-id="3da98-246">However, it is possible for a malicious user to change the value prior to post back.</span></span> <span data-ttu-id="3da98-247">如果發生這種情況，HiddenField 控制項將會引發 ValueChanged 事件。</span><span class="sxs-lookup"><span data-stu-id="3da98-247">If this happens, the HiddenField control will raise the ValueChanged event.</span></span> <span data-ttu-id="3da98-248">如果您在 HiddenField 控制項中有敏感性資訊，而且想要確保它保持不變，您應該在程式碼中處理 ValueChanged 事件。</span><span class="sxs-lookup"><span data-stu-id="3da98-248">If you have sensitive information in the HiddenField control and you want to ensure that it remains unchanged, you should handle the ValueChanged event in your code.</span></span>

## <a name="fileupload-control"></a><span data-ttu-id="3da98-249">FileUpload 控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-249">FileUpload Control</span></span>

<span data-ttu-id="3da98-250">ASP.NET 2.0 中的 FileUpload 控制項可讓您透過 ASP.NET 網頁，將檔案上傳至 Web 服務器。</span><span class="sxs-lookup"><span data-stu-id="3da98-250">The FileUpload control in ASP.NET 2.0 makes it possible to upload files to a Web server via an ASP.NET page.</span></span> <span data-ttu-id="3da98-251">此控制項與 ASP.NET 1.x HtmlInputFile 類別非常類似，但有一些例外狀況。</span><span class="sxs-lookup"><span data-stu-id="3da98-251">This control is quite similar to the ASP.NET 1.x HtmlInputFile class with a few exceptions.</span></span> <span data-ttu-id="3da98-252">在 ASP.NET 1.x 中，建議您檢查 PostedFile 屬性是否為 null，以便判斷您是否有良好的檔案。</span><span class="sxs-lookup"><span data-stu-id="3da98-252">In ASP.NET 1.x, it was recommended that the PostedFile property be checked for null in order to determine if you had a good file.</span></span> <span data-ttu-id="3da98-253">ASP.NET 2.0 中的 FileUpload 控制項加入了新的 HasFile 屬性，可讓您用於相同的目的，而且效率更高。</span><span class="sxs-lookup"><span data-stu-id="3da98-253">The FileUpload control in ASP.NET 2.0 adds a new HasFile property that you can use for the same purpose and it's a bit more efficient.</span></span>

<span data-ttu-id="3da98-254">PostedFile 屬性仍可供存取 HttpPostedFile 物件，但 HttpPostedFile 的某些功能現在已可透過 FileUpload 控制項在本質上使用。</span><span class="sxs-lookup"><span data-stu-id="3da98-254">The PostedFile property is still available for access to an HttpPostedFile object, but some of the functionality of the HttpPostedFile is now available intrinsically with the FileUpload control.</span></span> <span data-ttu-id="3da98-255">例如，若要在 ASP.NET 1.x 中儲存已上傳的檔案，您可以在 HttpPostedFile 物件上呼叫 SaveAs 方法。</span><span class="sxs-lookup"><span data-stu-id="3da98-255">For example, to save an uploaded file in ASP.NET 1.x, you call the SaveAs method on the HttpPostedFile object.</span></span> <span data-ttu-id="3da98-256">使用 ASP.NET 2.0 中的 FileUpload 控制項，您可以在 FileUpload 控制項本身呼叫 SaveAs 方法。</span><span class="sxs-lookup"><span data-stu-id="3da98-256">Using the FileUpload control in ASP.NET 2.0, you would call the SaveAs method on the FileUpload control itself.</span></span>

<span data-ttu-id="3da98-257">2\.0 行為的另一項重大變更（而且可能是最重要的變更）是不再需要將整個上傳的檔案載入記憶體中，然後再儲存。</span><span class="sxs-lookup"><span data-stu-id="3da98-257">Another significant change in the 2.0 behavior (and likely the most significant change) is that it is no longer necessary to load an entire uploaded file into memory before saving it.</span></span> <span data-ttu-id="3da98-258">在1.x 中，任何已上傳的檔案都會在寫入磁片之前，完全儲存到記憶體中。</span><span class="sxs-lookup"><span data-stu-id="3da98-258">In 1.x, any file that was uploaded is saved entirely into memory prior to being written to disk.</span></span> <span data-ttu-id="3da98-259">此架構會防止上傳大型檔案。</span><span class="sxs-lookup"><span data-stu-id="3da98-259">This architecture prevents the upload of large files.</span></span>

<span data-ttu-id="3da98-260">在 ASP.NET 2.0 中，HTTPRuntime 專案的 requestLengthDiskThreshold 屬性可讓您設定在寫入磁片之前，緩衝區中保留的位元組數。</span><span class="sxs-lookup"><span data-stu-id="3da98-260">In ASP.NET 2.0, the requestLengthDiskThreshold attribute of the httpRuntime element allows you to configure how many Kilobytes are held in a buffer in memory prior to being written to disk.</span></span>

<span data-ttu-id="3da98-261">**重要**事項： MSDN 檔（和其他地方的檔）指定這個值是以位元組為單位（不是 kb），而預設值是256。</span><span class="sxs-lookup"><span data-stu-id="3da98-261">**IMPORTANT**: MSDN documentation (and documentation elsewhere) specifies that this value is in bytes (not Kilobytes) and that the default is 256.</span></span> <span data-ttu-id="3da98-262">這個值實際上是以 Kb 指定，而預設值是80。</span><span class="sxs-lookup"><span data-stu-id="3da98-262">The value is actually specified in Kilobytes and the default value is 80.</span></span> <span data-ttu-id="3da98-263">藉由將預設值設定為80K，我們可以確保緩衝區不會最後出現在大型物件堆積上。</span><span class="sxs-lookup"><span data-stu-id="3da98-263">By having a default value of 80K, we ensure that the buffer does not end up on the large object heap.</span></span>

## <a name="wizard-control"></a><span data-ttu-id="3da98-264">Wizard 控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-264">Wizard Control</span></span>

<span data-ttu-id="3da98-265">當 ASP.NET 的開發人員嘗試使用面板在一系列的「頁面」中收集資訊，或從頁面傳輸到頁面時，這是相當常見的情況。</span><span class="sxs-lookup"><span data-stu-id="3da98-265">It is fairly common to encounter ASP.NET developers struggling with attempting to gather information in a series of "pages" using panels or by transferring from page to page.</span></span> <span data-ttu-id="3da98-266">這項工作通常會令人沮喪，而且非常耗時。</span><span class="sxs-lookup"><span data-stu-id="3da98-266">More often than not, the endeavor is a frustrating one and is time consuming.</span></span> <span data-ttu-id="3da98-267">新的 Wizard 控制項可透過在使用者熟悉的 Wizard 介面中允許線性和非線性步驟來解決問題。</span><span class="sxs-lookup"><span data-stu-id="3da98-267">The new Wizard control solves the problems by allowing for linear and non-linear steps in a wizard interface that users are familiar with.</span></span> <span data-ttu-id="3da98-268">Wizard 控制項會以一系列的步驟呈現輸入表單。</span><span class="sxs-lookup"><span data-stu-id="3da98-268">The Wizard control presents input forms in a series of steps.</span></span> <span data-ttu-id="3da98-269">每個步驟都是由控制項的 StepType 屬性所指定的特定類型。</span><span class="sxs-lookup"><span data-stu-id="3da98-269">Each step is of a particular type specified by the StepType property of the control.</span></span> <span data-ttu-id="3da98-270">可用的步驟類型如下所示：</span><span class="sxs-lookup"><span data-stu-id="3da98-270">The available step types are as follows:</span></span>

| <span data-ttu-id="3da98-271">**步驟類型**</span><span class="sxs-lookup"><span data-stu-id="3da98-271">**Step Type**</span></span> | <span data-ttu-id="3da98-272">**說明**</span><span class="sxs-lookup"><span data-stu-id="3da98-272">**Explanation**</span></span> |
| --- | --- |
| <span data-ttu-id="3da98-273">Auto</span><span class="sxs-lookup"><span data-stu-id="3da98-273">Auto</span></span> | <span data-ttu-id="3da98-274">Wizard 會根據步驟階層中的位置自動判斷步驟的類型。</span><span class="sxs-lookup"><span data-stu-id="3da98-274">The wizard automatically determines the type of step based upon its position within the step hierarchy.</span></span> |
| <span data-ttu-id="3da98-275">開始</span><span class="sxs-lookup"><span data-stu-id="3da98-275">Start</span></span> | <span data-ttu-id="3da98-276">第一個步驟，通常用來呈現簡介語句。</span><span class="sxs-lookup"><span data-stu-id="3da98-276">The first step, often used to present an introductory statement.</span></span> |
| <span data-ttu-id="3da98-277">步驟</span><span class="sxs-lookup"><span data-stu-id="3da98-277">Step</span></span> | <span data-ttu-id="3da98-278">一般步驟。</span><span class="sxs-lookup"><span data-stu-id="3da98-278">A normal step.</span></span> |
| <span data-ttu-id="3da98-279">完成</span><span class="sxs-lookup"><span data-stu-id="3da98-279">Finish</span></span> | <span data-ttu-id="3da98-280">最後一個步驟，通常用來顯示按鈕以完成嚮導。</span><span class="sxs-lookup"><span data-stu-id="3da98-280">The final step, usually used to present a button to finish the wizard.</span></span> |
| <span data-ttu-id="3da98-281">完成</span><span class="sxs-lookup"><span data-stu-id="3da98-281">Complete</span></span> | <span data-ttu-id="3da98-282">顯示訊息成功或失敗。</span><span class="sxs-lookup"><span data-stu-id="3da98-282">Presents a message communicating success or failure.</span></span> |

> [!NOTE]
> <span data-ttu-id="3da98-283">Wizard 控制項會使用 ASP.NET 控制項狀態來追蹤其狀態。</span><span class="sxs-lookup"><span data-stu-id="3da98-283">The Wizard control keeps track of its state using ASP.NET control state.</span></span> <span data-ttu-id="3da98-284">因此，EnableViewState 屬性可以設定為 false，而不需要任何弊。</span><span class="sxs-lookup"><span data-stu-id="3da98-284">Therefore, the EnableViewState property can be set to false without any detriment.</span></span>

<span data-ttu-id="3da98-285">這段影片是 Wizard 控制項的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="3da98-285">This video is a walkthrough of the Wizard control.</span></span>

![](server-controls/_static/image2.png)

[<span data-ttu-id="3da98-286">開啟全螢幕影片</span><span class="sxs-lookup"><span data-stu-id="3da98-286">Open Full-Screen Video</span></span>](server-controls/_static/wizard1.wmv)

## <a name="localize-control"></a><span data-ttu-id="3da98-287">當地語系化控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-287">Localize Control</span></span>

<span data-ttu-id="3da98-288">[當地語系化] 控制項類似于 [常值] 控制項。</span><span class="sxs-lookup"><span data-stu-id="3da98-288">The Localize control is similar to a Literal control.</span></span> <span data-ttu-id="3da98-289">不過，[當地語系化] 控制項具有 [**模式]** 屬性，可控制如何呈現加入至它的標記。</span><span class="sxs-lookup"><span data-stu-id="3da98-289">However, the Localize control has a **Mode** property that controls how markup that is added to it is rendered.</span></span> <span data-ttu-id="3da98-290">Mode 屬性支援下列值：</span><span class="sxs-lookup"><span data-stu-id="3da98-290">The Mode property supports the following values:</span></span>

| <span data-ttu-id="3da98-291">**模式**</span><span class="sxs-lookup"><span data-stu-id="3da98-291">**Mode**</span></span> | <span data-ttu-id="3da98-292">**說明**</span><span class="sxs-lookup"><span data-stu-id="3da98-292">**Explanation**</span></span> |
| --- | --- |
| <span data-ttu-id="3da98-293">轉換</span><span class="sxs-lookup"><span data-stu-id="3da98-293">Transform</span></span> | <span data-ttu-id="3da98-294">標記會根據提出要求之瀏覽器的通訊協定進行轉換。</span><span class="sxs-lookup"><span data-stu-id="3da98-294">Markup is transformed according to the protocol of the browser making the request.</span></span> |
| <span data-ttu-id="3da98-295">Ssh</span><span class="sxs-lookup"><span data-stu-id="3da98-295">PassThrough</span></span> | <span data-ttu-id="3da98-296">標記會以-is 呈現。</span><span class="sxs-lookup"><span data-stu-id="3da98-296">Markup is rendered as-is.</span></span> |
| <span data-ttu-id="3da98-297">編碼</span><span class="sxs-lookup"><span data-stu-id="3da98-297">Encode</span></span> | <span data-ttu-id="3da98-298">加入至控制項的標記會使用 HtmlEncode 進行編碼。</span><span class="sxs-lookup"><span data-stu-id="3da98-298">Markup that is added to the control is encoded using HtmlEncode.</span></span> |

## <a name="multiview-and-view-controls"></a><span data-ttu-id="3da98-299">[查看] 和 [視圖] 控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-299">MultiView and View Controls</span></span>

<span data-ttu-id="3da98-300">多型多型控制項的作用是 View 控制項的容器，而 View 控制項則是做為其他控制項的容器（與面板控制項非常類似）。</span><span class="sxs-lookup"><span data-stu-id="3da98-300">The MultiView control acts as a container for View controls, and the View control acts as a container (much like a Panel control) for other controls.</span></span> <span data-ttu-id="3da98-301">同一個視圖控制項中的每個視圖都是由單一 View 控制項表示。</span><span class="sxs-lookup"><span data-stu-id="3da98-301">Each view in a MultiView control is represented by a single View control.</span></span> <span data-ttu-id="3da98-302">同位查看中的第一個 View 控制項是 view 0，第二個是 view 1 等等。您可以藉由指定 [檢視器] 控制項的 ActiveViewIndex 來切換 views。</span><span class="sxs-lookup"><span data-stu-id="3da98-302">The first View control in the MultiView is view 0, the second is view 1, etc. You can switch views by specifying the ActiveViewIndex of the MultiView control.</span></span>

## <a name="substitution-control"></a><span data-ttu-id="3da98-303">替代控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-303">Substitution Control</span></span>

<span data-ttu-id="3da98-304">替代控制項會與 ASP.NET 快取搭配使用。</span><span class="sxs-lookup"><span data-stu-id="3da98-304">The Substitution control is used in conjunction with ASP.NET caching.</span></span> <span data-ttu-id="3da98-305">在您想要利用快取的情況下，您有部分頁面必須在每個要求上更新（換句話說，非快取的頁面部分），替代元件會提供絕佳的解決方案。</span><span class="sxs-lookup"><span data-stu-id="3da98-305">In cases where you want to take advantage of caching, but you have portions of a page that must be updated on each request (in other words, portions of a page that are exempt from caching), the Substitution component provides a great solution.</span></span> <span data-ttu-id="3da98-306">控制項實際上不會自行呈現任何輸出。</span><span class="sxs-lookup"><span data-stu-id="3da98-306">The control doesn't actually render any output on its own.</span></span> <span data-ttu-id="3da98-307">相反地，它會系結至伺服器端程式碼中的方法。</span><span class="sxs-lookup"><span data-stu-id="3da98-307">Instead, it is bound to a method in server-side code.</span></span> <span data-ttu-id="3da98-308">當要求頁面時，會呼叫方法，並呈現傳回的標記來取代替代控制項。</span><span class="sxs-lookup"><span data-stu-id="3da98-308">When the page is requested, the method is called and the returned markup is rendered in place of the substitution control.</span></span>

<span data-ttu-id="3da98-309">替代控制項所系結的方法是透過 [**方法名稱**] 屬性來指定。</span><span class="sxs-lookup"><span data-stu-id="3da98-309">The method to which the Substitution control is bound is specified via the **MethodName** property.</span></span> <span data-ttu-id="3da98-310">該方法必須符合下列準則：</span><span class="sxs-lookup"><span data-stu-id="3da98-310">That method must meet the following criteria:</span></span>

- <span data-ttu-id="3da98-311">它必須是靜態（在 VB 中為 shared）方法。</span><span class="sxs-lookup"><span data-stu-id="3da98-311">It must be a static (shared in VB) method.</span></span>
- <span data-ttu-id="3da98-312">它接受一個類型為 HttpCoNtext 的參數。</span><span class="sxs-lookup"><span data-stu-id="3da98-312">It accepts one parameter of type HttpContext.</span></span>
- <span data-ttu-id="3da98-313">它會傳回代表標記的字串，該標記應取代頁面上的控制項。</span><span class="sxs-lookup"><span data-stu-id="3da98-313">It returns a string representing the markup that should replace the control on the page.</span></span>

<span data-ttu-id="3da98-314">替代控制項無法修改頁面上的任何其他控制項，但它可以透過其參數存取目前的 HttpCoNtext。</span><span class="sxs-lookup"><span data-stu-id="3da98-314">The Substitution control does not have the ability to modify any other control on the page, but it does have access to the current HttpContext via its parameter.</span></span>

## <a name="gridview-control"></a><span data-ttu-id="3da98-315">GridView 控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-315">GridView Control</span></span>

<span data-ttu-id="3da98-316">GridView 控制項是 DataGrid 控制項的取代。</span><span class="sxs-lookup"><span data-stu-id="3da98-316">The GridView control is the replacement for the DataGrid control.</span></span> <span data-ttu-id="3da98-317">在稍後的課程模組中，將會更詳細地討論此控制項。</span><span class="sxs-lookup"><span data-stu-id="3da98-317">This control will be covered in more detail in a later module.</span></span>

## <a name="detailsview-control"></a><span data-ttu-id="3da98-318">DetailsView 控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-318">DetailsView Control</span></span>

<span data-ttu-id="3da98-319">DetailsView 控制項可讓您從資料來源顯示單一記錄，並加以編輯或刪除。</span><span class="sxs-lookup"><span data-stu-id="3da98-319">The DetailsView control allows you to display a single record from a data source and to edit or delete it.</span></span> <span data-ttu-id="3da98-320">稍後的課程模組會更詳細地說明。</span><span class="sxs-lookup"><span data-stu-id="3da98-320">It is covered in more detail in a later module.</span></span>

## <a name="formview-control"></a><span data-ttu-id="3da98-321">FormView 控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-321">FormView Control</span></span>

<span data-ttu-id="3da98-322">FormView 控制項是用來在可設定的介面中顯示資料來源中的單一記錄。</span><span class="sxs-lookup"><span data-stu-id="3da98-322">The FormView control is used to display a single record from a datasource in a configurable interface.</span></span> <span data-ttu-id="3da98-323">稍後的課程模組會更詳細地說明。</span><span class="sxs-lookup"><span data-stu-id="3da98-323">It is covered in more detail in a later module.</span></span>

## <a name="accessdatasource-control"></a><span data-ttu-id="3da98-324">AccessDataSource 控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-324">AccessDataSource Control</span></span>

<span data-ttu-id="3da98-325">AccessDataSource 控制項是用來系結 Access 資料庫的資料。</span><span class="sxs-lookup"><span data-stu-id="3da98-325">The AccessDataSource control is used to data bind an Access database.</span></span> <span data-ttu-id="3da98-326">稍後的課程模組會更詳細地說明。</span><span class="sxs-lookup"><span data-stu-id="3da98-326">It is covered in more detail in a later module.</span></span>

## <a name="objectdatasource-control"></a><span data-ttu-id="3da98-327">ObjectDataSource 控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-327">ObjectDataSource Control</span></span>

<span data-ttu-id="3da98-328">ObjectDataSource 控制項是用來支援三層式架構，因此控制項可以資料系結至中介層商務物件，而不是直接系結至資料來源的兩層式模型。</span><span class="sxs-lookup"><span data-stu-id="3da98-328">The ObjectDataSource control is used to support a three-tier architecture so that controls can be data-bound to a middle-tier business object as opposed to a two-tiered model where controls are bound directly to the data source.</span></span> <span data-ttu-id="3da98-329">稍後的課程模組中將會更詳細地討論。</span><span class="sxs-lookup"><span data-stu-id="3da98-329">It will be discussed in more detail in a later module.</span></span>

## <a name="xmldatasource-control"></a><span data-ttu-id="3da98-330">XmlDataSource 控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-330">XmlDataSource Control</span></span>

<span data-ttu-id="3da98-331">XmlDataSource 控制項是用來將資料系結至 XML 資料來源。</span><span class="sxs-lookup"><span data-stu-id="3da98-331">The XmlDataSource control is used to data bind to an XML data source.</span></span> <span data-ttu-id="3da98-332">稍後的課程模組會更詳細地說明。</span><span class="sxs-lookup"><span data-stu-id="3da98-332">It is covered in more detail in a later module.</span></span>

## <a name="sitemapdatasource-control"></a><span data-ttu-id="3da98-333">SiteMapDataSource 控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-333">SiteMapDataSource Control</span></span>

<span data-ttu-id="3da98-334">SiteMapDataSource 控制項會根據網站地圖提供網站導覽控制項的資料系結。</span><span class="sxs-lookup"><span data-stu-id="3da98-334">The SiteMapDataSource control provides data binding for site navigation controls based on a site map.</span></span> <span data-ttu-id="3da98-335">稍後的課程模組中將會更詳細地討論。</span><span class="sxs-lookup"><span data-stu-id="3da98-335">It will be discussed in more detail in a later module.</span></span>

## <a name="sitemappath-control"></a><span data-ttu-id="3da98-336">SiteMapPath 控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-336">SiteMapPath Control</span></span>

<span data-ttu-id="3da98-337">SiteMapPath 控制項會顯示一系列的導覽連結，通常稱為「階層連結」。</span><span class="sxs-lookup"><span data-stu-id="3da98-337">The SiteMapPath control displays a series of navigation links commonly referred to as breadcrumbs.</span></span> <span data-ttu-id="3da98-338">稍後的課程模組會更詳細地說明。</span><span class="sxs-lookup"><span data-stu-id="3da98-338">It is covered in more detail in a later module.</span></span>

## <a name="menu-control"></a><span data-ttu-id="3da98-339">功能表控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-339">Menu Control</span></span>

<span data-ttu-id="3da98-340">功能表控制項會使用 DHTML 顯示動態功能表。</span><span class="sxs-lookup"><span data-stu-id="3da98-340">The Menu control displays dynamic menus using DHTML.</span></span> <span data-ttu-id="3da98-341">稍後的課程模組會更詳細地說明。</span><span class="sxs-lookup"><span data-stu-id="3da98-341">It is covered in more detail in a later module.</span></span>

## <a name="treeview-control"></a><span data-ttu-id="3da98-342">TreeView 控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-342">TreeView Control</span></span>

<span data-ttu-id="3da98-343">TreeView 控制項是用來顯示資料的階層式樹狀檢視。</span><span class="sxs-lookup"><span data-stu-id="3da98-343">The TreeView control is used to display a hierarchical tree view of data.</span></span> <span data-ttu-id="3da98-344">稍後的課程模組會更詳細地說明。</span><span class="sxs-lookup"><span data-stu-id="3da98-344">It is covered in more detail in a later module.</span></span>

## <a name="login-control"></a><span data-ttu-id="3da98-345">Login 控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-345">Login Control</span></span>

<span data-ttu-id="3da98-346">Login 控制項提供登入網站的機制。</span><span class="sxs-lookup"><span data-stu-id="3da98-346">The Login control provides for a mechanism to log into a Web site.</span></span> <span data-ttu-id="3da98-347">稍後的課程模組會更詳細地說明。</span><span class="sxs-lookup"><span data-stu-id="3da98-347">It is covered in more detail in a later module.</span></span>

## <a name="loginview-control"></a><span data-ttu-id="3da98-348">LoginView 控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-348">LoginView Control</span></span>

<span data-ttu-id="3da98-349">LoginView 控制項可讓您根據使用者的登入狀態來顯示不同的範本。</span><span class="sxs-lookup"><span data-stu-id="3da98-349">The LoginView control allows for the display of different templates based upon a user's login status.</span></span> <span data-ttu-id="3da98-350">稍後的課程模組會更詳細地說明。</span><span class="sxs-lookup"><span data-stu-id="3da98-350">It is covered in more detail in a later module.</span></span>

## <a name="passwordrecovery-control"></a><span data-ttu-id="3da98-351">PasswordRecovery 控制項</span><span class="sxs-lookup"><span data-stu-id="3da98-351">PasswordRecovery Control</span></span>

<span data-ttu-id="3da98-352">PasswordRecovery 控制項是用來抓取 ASP.NET 應用程式的使用者所遺忘的密碼。</span><span class="sxs-lookup"><span data-stu-id="3da98-352">The PasswordRecovery control is used to retrieve forgotten passwords by users of an ASP.NET application.</span></span> <span data-ttu-id="3da98-353">稍後的課程模組會更詳細地說明。</span><span class="sxs-lookup"><span data-stu-id="3da98-353">It is covered in more detail in a later module.</span></span>

## <a name="loginstatus"></a><span data-ttu-id="3da98-354">LoginStatus</span><span class="sxs-lookup"><span data-stu-id="3da98-354">LoginStatus</span></span>

<span data-ttu-id="3da98-355">LoginStatus 控制項會顯示使用者的登入狀態。</span><span class="sxs-lookup"><span data-stu-id="3da98-355">The LoginStatus control displays a user's login status.</span></span> <span data-ttu-id="3da98-356">稍後的課程模組會更詳細地說明。</span><span class="sxs-lookup"><span data-stu-id="3da98-356">It is covered in more detail in a later module.</span></span>

## <a name="loginname"></a><span data-ttu-id="3da98-357">LoginName</span><span class="sxs-lookup"><span data-stu-id="3da98-357">LoginName</span></span>

<span data-ttu-id="3da98-358">LoginName 控制項會在登入 ASP.NET 應用程式後顯示使用者的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="3da98-358">The LoginName control displays a user's username after being logged into an ASP.NET application.</span></span> <span data-ttu-id="3da98-359">稍後的課程模組會更詳細地說明。</span><span class="sxs-lookup"><span data-stu-id="3da98-359">It is covered in more detail in a later module.</span></span>

## <a name="createuserwizard"></a><span data-ttu-id="3da98-360">CreateUserWizard</span><span class="sxs-lookup"><span data-stu-id="3da98-360">CreateUserWizard</span></span>

<span data-ttu-id="3da98-361">CreateUserWizard 是可設定的 wizard，讓使用者能夠建立 ASP.NET 成員資格帳戶，以便在 ASP.NET 應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="3da98-361">The CreateUserWizard is a configurable wizard which gives users the ability to create an ASP.NET Membership account for use in an ASP.NET application.</span></span> <span data-ttu-id="3da98-362">稍後的課程模組會更詳細地說明。</span><span class="sxs-lookup"><span data-stu-id="3da98-362">It is covered in more detail in a later module.</span></span>

## <a name="changepassword"></a><span data-ttu-id="3da98-363">ChangePassword</span><span class="sxs-lookup"><span data-stu-id="3da98-363">ChangePassword</span></span>

<span data-ttu-id="3da98-364">ChangePassword 控制項可讓使用者變更 ASP.NET 應用程式的密碼。</span><span class="sxs-lookup"><span data-stu-id="3da98-364">The ChangePassword control allows users to change their password for an ASP.NET application.</span></span> <span data-ttu-id="3da98-365">稍後的課程模組會更詳細地說明。</span><span class="sxs-lookup"><span data-stu-id="3da98-365">It is covered in more detail in a later module.</span></span>

## <a name="various-webparts"></a><span data-ttu-id="3da98-366">各種 Webpart</span><span class="sxs-lookup"><span data-stu-id="3da98-366">Various WebParts</span></span>

<span data-ttu-id="3da98-367">ASP.NET 2.0 隨附各種 Web 組件。</span><span class="sxs-lookup"><span data-stu-id="3da98-367">ASP.NET 2.0 ships with various Web Parts.</span></span> <span data-ttu-id="3da98-368">稍後的課程模組中將會詳細說明這些功能。</span><span class="sxs-lookup"><span data-stu-id="3da98-368">These will be covered in detail in a later module.</span></span>
