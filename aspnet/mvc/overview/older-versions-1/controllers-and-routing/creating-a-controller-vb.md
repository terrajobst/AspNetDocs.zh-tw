---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-vb
title: 建立控制器（VB） |Microsoft Docs
author: StephenWalther
description: 在本教學課程中，Stephen Walther 會示範如何將控制器新增至 ASP.NET MVC 應用程式。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 204b7e86-f560-4611-8adb-785b33e777b9
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-vb
msc.type: authoredcontent
ms.openlocfilehash: 60636b79ab5fc06ca904dee90ce74f256e046d12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601455"
---
# <a name="creating-a-controller-vb"></a>建立控制器 (VB)

依[Stephen Walther](https://github.com/StephenWalther)

> 在本教學課程中，Stephen Walther 會示範如何將控制器新增至 ASP.NET MVC 應用程式。

本教學課程的目的是要說明如何建立新的 ASP.NET MVC 控制器。 您將瞭解如何使用 Visual Studio 的 [新增控制器] 功能表選項，以及手動建立類別檔案來建立控制器。

### <a name="using-the-add-controller-menu-option"></a>使用 [新增控制器] 功能表選項

建立新控制器的最簡單方式是以滑鼠右鍵按一下 [Visual Studio 方案總管] 視窗中的 [控制器] 資料夾，然後選取 [**新增]、[控制器**] 功能表選項（請參閱 [圖 1]）。 選取此功能表選項會開啟 [**新增控制器**] 對話方塊（請參閱 [圖 2]）。

[![[新增專案] 對話方塊](creating-a-controller-vb/_static/image1.jpg)](creating-a-controller-vb/_static/image1.png)

**圖 01**：新增控制器（[按一下以觀看完整大小的影像](creating-a-controller-vb/_static/image2.png)）

[![[新增專案] 對話方塊](creating-a-controller-vb/_static/image2.jpg)](creating-a-controller-vb/_static/image3.png)

**圖 02**： [新增控制器] 對話方塊（[按一下以查看完整大小的影像](creating-a-controller-vb/_static/image4.png)）

請注意，控制器名稱的第一個部分會反白顯示在 [**新增控制器**] 對話方塊中。 每個控制器名稱的結尾都必須是尾碼*控制器*。 例如，您可以建立名為*ProductController*的控制器，而不是名為*Product*的控制器。

如果您建立的控制器缺少*控制器*尾碼，則您將無法叫用控制器。 不要這麼做--我在犯此錯誤之後，浪費了無數小時的時間。

**清單 1-Controllers\ProductController.vb**

[!code-vb[Main](creating-a-controller-vb/samples/sample1.vb)]

您應該一律在 [控制器] 資料夾中建立控制器。 否則，您將違反 ASP.NET MVC 的慣例，而其他開發人員將會更容易瞭解您的應用程式。

### <a name="scaffolding-action-methods"></a>樣板動作方法

當您建立控制器時，可以選擇自動產生 [建立]、[更新] 和 [詳細資料] 動作方法（請參閱 [圖 3]）。 如果您選取此選項，則會產生 [清單 2] 中的控制器類別。

[![自動建立動作方法](creating-a-controller-vb/_static/image3.jpg)](creating-a-controller-vb/_static/image5.png)

**圖 03**：自動建立動作方法（[按一下以觀看完整大小的影像](creating-a-controller-vb/_static/image6.png)）

**清單 2-Controllers\CustomerController.vb**

[!code-vb[Main](creating-a-controller-vb/samples/sample2.vb)]

這些產生的方法都是存根方法。 您必須自行加入用來建立、更新和顯示客戶詳細資料的實際邏輯。 但是，存根方法提供了一個不錯的起點。

### <a name="creating-a-controller-class"></a>建立控制器類別

ASP.NET MVC 控制器只是一個類別。 如果您想要的話，可以忽略方便的 Visual Studio 控制器樣板，並手動建立控制器類別。 請依照下列步驟：

1. 以滑鼠右鍵按一下 [控制器] 資料夾，然後選取 [新增] **、[新專案**] 功能表選項，然後選取 [**類別**] 範本（請參閱 [圖 4]）。
2. 將新的類別命名為 PersonController，然後按一下 [**新增**] 按鈕。
3. 修改產生的類別檔案，讓類別繼承自基底 System.web. Controller 類別（請參閱 [清單 3]）。

[建立新類別 ![](creating-a-controller-vb/_static/image4.jpg)](creating-a-controller-vb/_static/image7.png)

**圖 04**：建立新的類別（[按一下以查看完整大小的影像](creating-a-controller-vb/_static/image8.png)）

**清單 3-Controllers\PersonController.vb**

[!code-vb[Main](creating-a-controller-vb/samples/sample3.vb)]

[清單 3] 中的控制器會公開一個名為 Index （）的動作，以傳回字串 "Hello World！"。 您可以藉由執行應用程式並要求如下所示的 URL 來叫用此控制器動作：

`http://localhost:40071/Person`

> [!NOTE]
> 
> ASP.NET 程式開發伺服器使用隨機埠號碼（例如，40071）。 輸入 URL 以叫用控制器時，您必須提供正確的埠號碼。 您可以將滑鼠游標移至 Windows 通知區域（畫面右下方）中的 ASP.NET 程式開發伺服器圖示上，藉以判斷埠號碼。
> 
> [!div class="step-by-step"]
> [上一頁](adding-dynamic-content-to-a-cached-page-vb.md)
> [下一頁](creating-an-action-vb.md)
