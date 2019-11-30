---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-vb
title: 建立評等控制項（VB） |Microsoft Docs
author: wenz
description: 許多網站（從電子商務到社區網站）提供使用者對文章或專案進行評分。 這通常需要一些編碼工作，但我們有 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6d0d70f4-725e-4258-8ae8-24a6ba1ddbf7
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 08e245edfe73db4e3896db51151e5d7a0fa9697c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611534"
---
# <a name="creating-a-rating-control-vb"></a>建立評等控制項 (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.vb.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0VB.pdf)

> 許多網站（從電子商務到社區網站）提供使用者對文章或專案進行評分。 這通常需要一些程式碼撰寫工作，但我們會將控制工具組提供給我們的處置。

## <a name="overview"></a>概觀

許多網站（從電子商務到社區網站）提供使用者對文章或專案進行評分。 這通常需要一些程式碼撰寫工作，但我們會將控制工具組提供給我們的處置。

## <a name="steps"></a>步驟

首先，您需要（至少）兩種影像：一個用於已填滿的評等專案，另一個則用於空的評等專案。 評等專案通常是星星或笑臉。 在此案例中，您會在本教學課程的原始程式碼下載中找到三個檔案，笑臉和空白 .png 和 smiley-done。

然後，建立新的 ASP.NET 檔案，並開始在其中加入 `ScriptManager` 控制項：

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample1.aspx)]

然後，從 ASP.NET AJAX 控制項工具組加入 `Rating` 控制項。 您必須針對此範例設定下列屬性：

- `CurrentRating` 要使用的初始評等
- `MaxRating` 最大評等
- `EmptyStarCssClass` 在評等專案（星號）為空白時所要使用的 CSS 類別
- `FilledStarCssClass` 填寫評等專案（星星）時要使用的 CSS 類別
- `StarCssClass` 要用於可見狀態的 CSS 類別
- `WaitingStarCssClass` 在將星級評等傳送回伺服器時所要使用的 CSS 類別

以下的標記會建立具有五個專案的評等控制項（smileys），一開始不填寫：

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample2.aspx)]

這三個參考的 CSS 類別現在需要顯示適當的影像檔案，這很容易使用 CSS 來執行：

[!code-css[Main](creating-a-rating-control-vb/samples/sample3.css)]

請確定您提供三個影像的寬度和高度，否則顯示的外觀可能會需要操作。

最後，評等的結果應該會向使用者顯示（或至少儲存在資料庫中）。 因此，請為文字訊息的輸出新增標籤，並使用 [提交] 按鈕將評等表單回傳至伺服器：

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample4.aspx)]

在伺服器端程式碼中，透過其 `ID` 存取評等控制項，然後存取其 `CurrentRating` 屬性，這是所選評等專案的數目，在範例中是介於0和5之間的值。

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample5.aspx)]

儲存頁面，並將它載入瀏覽器。 當您將滑鼠停留在（一開始是空的）評等專案時，就會發生 JavaScript 效果：評等會變更。 當您按一下一組星星時，會保留目前的評等。 最後，當您提交表單時，伺服器端程式碼會輸出選取的評等。

[![以最少的程式碼建立評等系統](creating-a-rating-control-vb/_static/image2.png)](creating-a-rating-control-vb/_static/image1.png)

以最少的程式碼建立分級系統（[按一下以觀看完整大小的影像](creating-a-rating-control-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一篇](creating-a-rating-control-cs.md)
