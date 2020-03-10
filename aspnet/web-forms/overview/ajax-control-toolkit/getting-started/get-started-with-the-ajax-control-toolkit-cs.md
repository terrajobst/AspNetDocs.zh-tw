---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: 開始使用 AJAX 控制項工具組（C#） |Microsoft Docs
author: microsoft
description: 瞭解開始使用 AJAX 控制項工具組所需的一切知識。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: 7478b090ec52778572d70065983de6be8bdb4e6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78621601"
---
# <a name="get-started-with-the-ajax-control-toolkit-c"></a><span data-ttu-id="fc8c3-103">開始使用 AJAX Control Toolkit (C#)</span><span class="sxs-lookup"><span data-stu-id="fc8c3-103">Get Started with the AJAX Control Toolkit (C#)</span></span>

<span data-ttu-id="fc8c3-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="fc8c3-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="fc8c3-105">瞭解開始使用 AJAX 控制項工具組所需的一切知識。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>

<span data-ttu-id="fc8c3-106">AJAX Control 工具組包含30個以上的免費控制項，可供您在 ASP.NET 應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="fc8c3-107">在本教學課程中，您將瞭解如何下載 AJAX 控制項工具組，並將工具組控制項新增至您的 Visual Studio/Visual Web Developer Express 工具箱。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="fc8c3-108">下載 AJAX 控制項工具組</span><span class="sxs-lookup"><span data-stu-id="fc8c3-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="fc8c3-109">[AJAX 控制項工具](http://devexpress.com/act)組是由 ASP.NET 社區成員和 ASP.NET 團隊所開發的開放原始碼專案。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span> 

<span data-ttu-id="fc8c3-110">[![下載 AJAX 控制項工具組](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fc8c3-110">[![Downloading the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span></span>

<span data-ttu-id="fc8c3-111">**圖 01**：下載 AJAX 控制項工具組（[按一下以觀看完整大小的影像](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="fc8c3-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span></span>

<span data-ttu-id="fc8c3-112">下載檔案之後，您必須解除封鎖檔案。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="fc8c3-113">在檔案上按一下滑鼠右鍵，選取 [屬性]，然後按一下 [**解除封鎖**] 按鈕（請參閱 [圖 2]）。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>

<span data-ttu-id="fc8c3-114">[![解除封鎖 AJAX 控制項工具組 ZIP 檔案](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="fc8c3-114">[![Unblocking the AJAX Control Toolkit ZIP file](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span></span>

<span data-ttu-id="fc8c3-115">**圖 02**：解除封鎖 AJAX 控制項工具組 ZIP 檔案（[按一下以查看完整大小的影像](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="fc8c3-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span></span>

<span data-ttu-id="fc8c3-116">解除封鎖檔案之後，您可以解壓縮檔案：以滑鼠右鍵按一下檔案，然後選取 [**全部解壓縮**] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="fc8c3-117">現在，我們已準備好將工具組新增至 Visual Studio/Visual Web Developer 工具箱。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="fc8c3-118">將 AJAX 控制項工具組加入至工具箱</span><span class="sxs-lookup"><span data-stu-id="fc8c3-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="fc8c3-119">使用 AJAX 控制項工具組最簡單的方式，就是將工具組新增至您的 Visual Studio/Visual Web Developer 工具箱（請參閱 [圖 3]）。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="fc8c3-120">如此一來，當您想要使用工具組控制項時，可以直接將它拖曳到頁面上。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>

<span data-ttu-id="fc8c3-121">[![AJAX 控制項工具組會出現在工具箱中](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="fc8c3-121">[![AJAX Control Toolkit appears in toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span></span>

<span data-ttu-id="fc8c3-122">**圖 03**： AJAX 控制項工具組出現在工具箱中（[按一下以觀看完整大小的影像](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="fc8c3-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span></span>

<span data-ttu-id="fc8c3-123">首先，您必須將 [AJAX 控制項工具組] 索引標籤新增至 [工具箱]。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="fc8c3-124">請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-124">Follow these steps.</span></span>

1. <span data-ttu-id="fc8c3-125">選取功能表選項 [檔案]、[新增網站]，以建立新的 ASP.NET 網站。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="fc8c3-126">按兩下 [方案總管] 視窗中的 default.aspx，在編輯器中開啟檔案。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="fc8c3-127">在 [一般] 索引標籤底下的 [工具箱] 上按一下滑鼠右鍵，然後選取 [**新增]** 功能表選項（見 [圖 4]）。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="fc8c3-128">輸入名為 [AJAX 控制項工具組] 的新索引標籤。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-128">Enter a new tab named AJAX Control Toolkit.</span></span>

<span data-ttu-id="fc8c3-129">[![新增索引標籤](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="fc8c3-129">[![Adding a new tab](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span></span>

<span data-ttu-id="fc8c3-130">**圖 04**：加入新的索引標籤（[按一下以觀看完整大小的影像](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="fc8c3-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span></span>

<span data-ttu-id="fc8c3-131">接下來，您需要將 AJAX 控制項工具組控制項新增至新的索引標籤。請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="fc8c3-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="fc8c3-132">以滑鼠右鍵按一下 [AJAX Control 工具組] 索引標籤下方，然後選取功能表選項 **[選擇專案] （請參閱 [圖 5]）** 。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="fc8c3-133">流覽至您解壓縮 AJAX 控制項工具組的位置，然後選取 [AjaxControlToolkit] 元件。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>

<span data-ttu-id="fc8c3-134">[![選擇要加入 [工具箱] 的專案](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="fc8c3-134">[![Choose items to add to the toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span></span>

<span data-ttu-id="fc8c3-135">**圖 05**：選擇要加入 [工具箱] 的專案（[按一下以查看完整大小的影像](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="fc8c3-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span></span>

<span data-ttu-id="fc8c3-136">完成這些步驟之後，所有的工具組控制項都會出現在 [工具箱] 中。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="fc8c3-137">升級至新版本的工具組</span><span class="sxs-lookup"><span data-stu-id="fc8c3-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="fc8c3-138">如果您使用較舊版本的工具組，但現在需要移至更新版本，建議您執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fc8c3-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="fc8c3-139">二進位檔-從網站 Bin 資料夾中刪除舊版本的 AjaxControlToolkit 元件。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="fc8c3-140">工具箱專案-刪除 [AJAX 控制項工具組] 索引標籤，然後遵循上述步驟，以使用新版本的 AjaxControlToolkit 重新建立索引標籤。</span><span class="sxs-lookup"><span data-stu-id="fc8c3-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="fc8c3-141">下一個</span><span class="sxs-lookup"><span data-stu-id="fc8c3-141">Next</span></span>](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
