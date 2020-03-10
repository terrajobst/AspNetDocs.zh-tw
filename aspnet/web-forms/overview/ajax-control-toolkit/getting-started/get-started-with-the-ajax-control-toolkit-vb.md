---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
title: 開始使用 AJAX 控制項工具組（VB） |Microsoft Docs
author: microsoft
description: 瞭解開始使用 AJAX 控制項工具組所需的一切知識。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 9f8fa166-49a2-402c-b236-20caef0c658f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
msc.type: authoredcontent
ms.openlocfilehash: ff614308555b31710b11f408e12e9a6fadbf98d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613481"
---
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a>開始使用 AJAX Control Toolkit (VB)

由[Microsoft](https://github.com/microsoft)

> 瞭解開始使用 AJAX 控制項工具組所需的一切知識。

AJAX Control 工具組包含30個以上的免費控制項，可供您在 ASP.NET 應用程式中使用。 在本教學課程中，您將瞭解如何下載 AJAX 控制項工具組，並將工具組控制項新增至您的 Visual Studio/Visual Web Developer Express 工具箱。

## <a name="downloading-the-ajax-control-toolkit"></a>下載 AJAX 控制項工具組

[AJAX 控制項工具](http://devexpress.com/act)組是由 ASP.NET 社區成員和 ASP.NET 團隊所開發的開放原始碼專案。

[![下載 AJAX 控制項工具組](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)

**圖 01**：下載 AJAX 控制項工具組（[按一下以觀看完整大小的影像](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png)）

下載檔案之後，您必須解除封鎖檔案。 在檔案上按一下滑鼠右鍵，選取 [屬性]，然後按一下 [**解除封鎖**] 按鈕（請參閱 [圖 2]）。

[![解除封鎖 AJAX 控制項工具組 ZIP 檔案](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)

**圖 02**：解除封鎖 AJAX 控制項工具組 ZIP 檔案（[按一下以查看完整大小的影像](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png)）

解除封鎖檔案之後，您可以解壓縮檔案：以滑鼠右鍵按一下檔案，然後選取 [**全部解壓縮**] 功能表選項。 現在，我們已準備好將工具組新增至 Visual Studio/Visual Web Developer 工具箱。

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>將 AJAX 控制項工具組加入至工具箱

使用 AJAX 控制項工具組最簡單的方式，就是將工具組新增至您的 Visual Studio/Visual Web Developer 工具箱（請參閱 [圖 3]）。 如此一來，當您想要使用工具組控制項時，可以直接將它拖曳到頁面上。

[![AJAX 控制項工具組會出現在工具箱中](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)

**圖 03**： AJAX 控制項工具組出現在工具箱中（[按一下以觀看完整大小的影像](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png)）

首先，您必須將 [AJAX 控制項工具組] 索引標籤新增至 [工具箱]。 請遵循下列步驟。

1. 選取功能表選項 [檔案]、[新增網站]，以建立新的 ASP.NET 網站。 按兩下 [方案總管] 視窗中的 default.aspx，在編輯器中開啟檔案。
2. 在 [一般] 索引標籤底下的 [工具箱] 上按一下滑鼠右鍵，然後選取 [**新增]** 功能表選項（見 [圖 4]）。
3. 輸入名為 [AJAX 控制項工具組] 的新索引標籤。

[![新增索引標籤](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)

**圖 04**：加入新的索引標籤（[按一下以觀看完整大小的影像](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png)）

接下來，您需要將 AJAX 控制項工具組控制項新增至新的索引標籤。請依照下列步驟執行：

- 以滑鼠右鍵按一下 [AJAX Control 工具組] 索引標籤下方，然後選取功能表選項 **[選擇專案] （請參閱 [圖 5]）** 。
- 流覽至您解壓縮 AJAX 控制項工具組的位置，然後選取 [AjaxControlToolkit] 元件。

[![選擇要加入 [工具箱] 的專案](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)

**圖 05**：選擇要加入 [工具箱] 的專案（[按一下以查看完整大小的影像](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png)）

完成這些步驟之後，所有的工具組控制項都會出現在 [工具箱] 中。

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>升級至新版本的工具組

如果您使用較舊版本的工具組，但現在需要移至更新版本，建議您執行下列步驟：

- 二進位檔-從網站 Bin 資料夾中刪除舊版本的 AjaxControlToolkit 元件。
- 工具箱專案-刪除 [AJAX 控制項工具組] 索引標籤，然後遵循上述步驟，以使用新版本的 AjaxControlToolkit 重新建立索引標籤。

> [!div class="step-by-step"]
> [上一頁](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [下一頁](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
