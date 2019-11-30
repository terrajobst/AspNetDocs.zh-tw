---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
title: 搭配 Reorderlist 回傳（C#）使用回傳 |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 Reorderlist 回傳控制項提供清單，讓使用者可以透過拖放方式重新排序。 每當重新排列清單時，就會有 po 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 70d5d106-b547-442c-a7fd-3492b3e3d646
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: f83201fc6fd458e730b6bb5ffee184d303b52e90
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611410"
---
# <a name="using-postbacks-with-reorderlist-c"></a><span data-ttu-id="71d79-104">使用具有 ReorderList 的回傳 (C#)</span><span class="sxs-lookup"><span data-stu-id="71d79-104">Using Postbacks with ReorderList (C#)</span></span>

<span data-ttu-id="71d79-105">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="71d79-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="71d79-106">[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="71d79-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)</span></span>

> <span data-ttu-id="71d79-107">AJAX 控制項工具組中的 Reorderlist 回傳控制項提供清單，讓使用者可以透過拖放方式重新排序。</span><span class="sxs-lookup"><span data-stu-id="71d79-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="71d79-108">每當重新排序清單時，回傳就會通知伺服器該變更。</span><span class="sxs-lookup"><span data-stu-id="71d79-108">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="overview"></a><span data-ttu-id="71d79-109">概觀</span><span class="sxs-lookup"><span data-stu-id="71d79-109">Overview</span></span>

<span data-ttu-id="71d79-110">AJAX 控制項工具組中的 `ReorderList` 控制項提供一個清單，讓使用者可以透過拖放方式重新排序。</span><span class="sxs-lookup"><span data-stu-id="71d79-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="71d79-111">每當重新排序清單時，回傳就會通知伺服器該變更。</span><span class="sxs-lookup"><span data-stu-id="71d79-111">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="steps"></a><span data-ttu-id="71d79-112">步驟</span><span class="sxs-lookup"><span data-stu-id="71d79-112">Steps</span></span>

<span data-ttu-id="71d79-113">`ReorderList` 控制項有幾個可能的資料來源。</span><span class="sxs-lookup"><span data-stu-id="71d79-113">There are several possible data sources for the `ReorderList` control.</span></span> <span data-ttu-id="71d79-114">其中一種是使用 `XmlDataSource` 控制項：</span><span class="sxs-lookup"><span data-stu-id="71d79-114">One is to use an `XmlDataSource` control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample1.aspx)]

<span data-ttu-id="71d79-115">為了將此 XML 系結至 `ReorderList` 控制項並啟用回傳，必須設定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="71d79-115">In order to bind this XML to a `ReorderList` control and enable postbacks, the following attributes must be set:</span></span>

- <span data-ttu-id="71d79-116">`DataSourceID`：資料來源的識別碼</span><span class="sxs-lookup"><span data-stu-id="71d79-116">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="71d79-117">`SortOrderField`：排序依據的屬性</span><span class="sxs-lookup"><span data-stu-id="71d79-117">`SortOrderField`: The property to sort by</span></span>
- <span data-ttu-id="71d79-118">`AllowReorder`：是否允許使用者重新排序清單元素</span><span class="sxs-lookup"><span data-stu-id="71d79-118">`AllowReorder`: Whether to allow the user to reorder the list elements</span></span>
- <span data-ttu-id="71d79-119">`PostBackOnReorder`：是否要在每次重新排列清單時建立回傳</span><span class="sxs-lookup"><span data-stu-id="71d79-119">`PostBackOnReorder`: Whether to create a postback whenever the list is rearranged</span></span>

<span data-ttu-id="71d79-120">以下是適當的控制項標記：</span><span class="sxs-lookup"><span data-stu-id="71d79-120">Here is the appropriate markup for the control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample2.aspx)]

<span data-ttu-id="71d79-121">在 `ReorderList` 控制項內，可能會使用 `Eval()` 方法來系結資料來源中的特定資料：</span><span class="sxs-lookup"><span data-stu-id="71d79-121">Within the `ReorderList` control, specific data from the data source may be bound using the `Eval()` method:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample3.aspx)]

<span data-ttu-id="71d79-122">在頁面上的任意位置上，標籤會保存最後一次發生重新排序時的資訊：</span><span class="sxs-lookup"><span data-stu-id="71d79-122">At an arbitrary position on the page, a label will hold the information when the last reordering occurred:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample4.aspx)]

<span data-ttu-id="71d79-123">此標籤會以伺服器端程式碼中的文字填入，處理回傳：</span><span class="sxs-lookup"><span data-stu-id="71d79-123">This label is filled with text in the server-side code, handling the postback:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample5.aspx)]

<span data-ttu-id="71d79-124">最後，若要啟用 ASP.NET AJAX 和控制項工具組的功能，必須將 `ScriptManager` 控制項放在網頁上：</span><span class="sxs-lookup"><span data-stu-id="71d79-124">Finally, in order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put on the page:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample6.aspx)]

<span data-ttu-id="71d79-125">[![每個重新排列都會觸發回傳](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="71d79-125">[![Each reordering triggers a postback](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)</span></span>

<span data-ttu-id="71d79-126">每次重新排列都會觸發回傳（[按一下以查看完整大小的影像](using-postbacks-with-reorderlist-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="71d79-126">Each reordering triggers a postback ([Click to view full-size image](using-postbacks-with-reorderlist-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="71d79-127">下一步</span><span class="sxs-lookup"><span data-stu-id="71d79-127">Next</span></span>](drag-and-drop-via-reorderlist-cs.md)
