---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
title: 使用具有 reorderlist 的回傳 (C#) |Microsoft Docs
author: wenz
description: 在 AJAX Control Toolkit reorderlist 的回傳控制項提供使用者透過拖放來重新排列的清單。 已重新排列清單，每當 po...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 70d5d106-b547-442c-a7fd-3492b3e3d646
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 6f8f74b74080104980e1db866d695fe7c6d9d5fc
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59393349"
---
# <a name="using-postbacks-with-reorderlist-c"></a><span data-ttu-id="8c297-104">使用具有 ReorderList 的回傳 (C#)</span><span class="sxs-lookup"><span data-stu-id="8c297-104">Using Postbacks with ReorderList (C#)</span></span>

<span data-ttu-id="8c297-105">藉由[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="8c297-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8c297-106">[下載程式碼](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip)或[下載 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="8c297-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)</span></span>

> <span data-ttu-id="8c297-107">在 AJAX Control Toolkit reorderlist 的回傳控制項提供使用者透過拖放來重新排列的清單。</span><span class="sxs-lookup"><span data-stu-id="8c297-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="8c297-108">已重新排列清單，每當回傳會通知變更的伺服器。</span><span class="sxs-lookup"><span data-stu-id="8c297-108">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>


## <a name="overview"></a><span data-ttu-id="8c297-109">總覽</span><span class="sxs-lookup"><span data-stu-id="8c297-109">Overview</span></span>

<span data-ttu-id="8c297-110">`ReorderList` AJAX Control Toolkit 中的控制項提供使用者透過拖放來重新排列的清單。</span><span class="sxs-lookup"><span data-stu-id="8c297-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="8c297-111">已重新排列清單，每當回傳會通知變更的伺服器。</span><span class="sxs-lookup"><span data-stu-id="8c297-111">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="steps"></a><span data-ttu-id="8c297-112">步驟</span><span class="sxs-lookup"><span data-stu-id="8c297-112">Steps</span></span>

<span data-ttu-id="8c297-113">有數個可能的資料來源`ReorderList`控制項。</span><span class="sxs-lookup"><span data-stu-id="8c297-113">There are several possible data sources for the `ReorderList` control.</span></span> <span data-ttu-id="8c297-114">其中一個是使用`XmlDataSource`控制項：</span><span class="sxs-lookup"><span data-stu-id="8c297-114">One is to use an `XmlDataSource` control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample1.aspx)]

<span data-ttu-id="8c297-115">若要繫結至這個 XML`ReorderList`必須設定控制項，並啟用回傳中，下列屬性：</span><span class="sxs-lookup"><span data-stu-id="8c297-115">In order to bind this XML to a `ReorderList` control and enable postbacks, the following attributes must be set:</span></span>

- `DataSourceID`<span data-ttu-id="8c297-116">:資料來源的識別碼</span><span class="sxs-lookup"><span data-stu-id="8c297-116">: The ID of the data source</span></span>
- `SortOrderField`<span data-ttu-id="8c297-117">:要排序的屬性</span><span class="sxs-lookup"><span data-stu-id="8c297-117">: The property to sort by</span></span>
- `AllowReorder`<span data-ttu-id="8c297-118">:是否要允許使用者重新排列清單項目</span><span class="sxs-lookup"><span data-stu-id="8c297-118">: Whether to allow the user to reorder the list elements</span></span>
- `PostBackOnReorder`<span data-ttu-id="8c297-119">:是否要建立回傳，每當重新排列清單</span><span class="sxs-lookup"><span data-stu-id="8c297-119">: Whether to create a postback whenever the list is rearranged</span></span>

<span data-ttu-id="8c297-120">以下是控制項的適當標記：</span><span class="sxs-lookup"><span data-stu-id="8c297-120">Here is the appropriate markup for the control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample2.aspx)]

<span data-ttu-id="8c297-121">內`ReorderList`控制項，從資料來源的特定資料可能會繫結使用`Eval()`方法：</span><span class="sxs-lookup"><span data-stu-id="8c297-121">Within the `ReorderList` control, specific data from the data source may be bound using the `Eval()` method:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample3.aspx)]

<span data-ttu-id="8c297-122">在頁面上的任意位置，標籤會包含的資訊，最後重新調整順序發生：</span><span class="sxs-lookup"><span data-stu-id="8c297-122">At an arbitrary position on the page, a label will hold the information when the last reordering occurred:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample4.aspx)]

<span data-ttu-id="8c297-123">此標籤會填入處理回傳的伺服器端程式碼中的文字：</span><span class="sxs-lookup"><span data-stu-id="8c297-123">This label is filled with text in the server-side code, handling the postback:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample5.aspx)]

<span data-ttu-id="8c297-124">最後，若要啟動的 ASP.NET AJAX Control Toolkit 中，功能`ScriptManager`控制項必須放在頁面上：</span><span class="sxs-lookup"><span data-stu-id="8c297-124">Finally, in order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put on the page:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample6.aspx)]


[![E<span data-ttu-id="8c297-125">除此之外，每個重新排列觸發回傳]</span><span class="sxs-lookup"><span data-stu-id="8c297-125">ach reordering triggers a postback]</span></span>(using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)

<span data-ttu-id="8c297-126">每個重新排列觸發回傳 ([按一下以檢視完整大小的影像](using-postbacks-with-reorderlist-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="8c297-126">Each reordering triggers a postback ([Click to view full-size image](using-postbacks-with-reorderlist-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8c297-127">下一步</span><span class="sxs-lookup"><span data-stu-id="8c297-127">Next</span></span>](drag-and-drop-via-reorderlist-cs.md)
