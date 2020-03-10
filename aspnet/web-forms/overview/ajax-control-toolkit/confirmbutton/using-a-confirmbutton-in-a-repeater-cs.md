---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-cs
title: 使用中繼器中的項 confirmbutton （C#） |Microsoft Docs
author: wenz
description: 當使用者按一下按鈕（包括 LinkButton 控制項）時，AJAX 控制項工具組中的項 confirmbutton 擴充項會建立 [是/否] 快顯視窗。 只有在是 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a973ed3e-400c-4925-ace2-0b086b479301
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-cs
msc.type: authoredcontent
ms.openlocfilehash: 468a830f01c48dc39b22bc5d826f80533df65c1a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554282"
---
# <a name="using-a-confirmbutton-in-a-repeater-c"></a>在重複項中使用 ConfirmButton (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1CS.pdf)

> 當使用者按一下按鈕（包括 LinkButton 控制項）時，AJAX 控制項工具組中的項 confirmbutton 擴充項會建立 [是/否] 快顯視窗。 只有當您按一下 [是] 時，才會執行按鈕的動作，否則會取消。 這也可以在中繼器中進行。

## <a name="overview"></a>概觀

當使用者按一下按鈕（包括 LinkButton 控制項）時，AJAX 控制項工具組中的項 confirmbutton 擴充項會建立 [是/否] 快顯視窗。 只有當您按一下 [是] 時，才會執行按鈕的動作，否則會取消。 這也可以在中繼器中進行。

## <a name="steps"></a>步驟

首先，需要資料來源。 這個範例會使用 AdventureWorks 資料庫和 Microsoft SQL Server 2005 Express Edition。 資料庫是 Visual Studio 安裝（包含 express edition）的選擇性部分，而且也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下個別下載。 AdventureWorks 資料庫是 SQL Server 2005 範例和範例資料庫的一部分（下載于[https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）。 設定資料庫最簡單的方式，就是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）並附加 `AdventureWorks.mdf` 資料庫檔案。

在此範例中，我們假設 SQL Server 2005 Express Edition 的實例呼叫 `SQLEXPRESS` 並與 web 伺服器位於同一部電腦上;這也是預設設定。 如果您的安裝程式不同，則必須調整資料庫的連接資訊。

若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample1.aspx)]

然後，需要資料來源。 為了簡單起見，只會抓取 AdventureWorks 「廠商」資料表中的前五個專案。 請注意，使用 [Visual Studio wizard] 建立資料來源時，資料表名稱（`Vendors`）目前不會正確地加上 `Purchasing`的前置詞。 下列標記是正確的：

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample2.aspx)]

然後，可以在中繼器內使用此資料來源。 如同往常，`DataBinder.Eval()` 方法會從資料來源抓取資料。 然後，`ConfirmButtonExtender` 控制項必須放在重複項的 [`<ItemTemplate>`] 區段內，才會顯示在資料來源中的每個專案。

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample3.aspx)]

[![[確認] 按鈕會出現在資料來源中的每個專案旁邊](using-a-confirmbutton-in-a-repeater-cs/_static/image2.png)](using-a-confirmbutton-in-a-repeater-cs/_static/image1.png)

[確認] 按鈕會出現在資料來源中的每個專案旁邊（[按一下以查看完整大小的影像](using-a-confirmbutton-in-a-repeater-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [下一個](using-a-confirmbutton-in-a-repeater-vb.md)
