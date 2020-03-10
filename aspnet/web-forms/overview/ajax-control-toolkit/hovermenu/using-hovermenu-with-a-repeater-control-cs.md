---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
title: 搭配重複使用 HoverMenu 與重複項C#控制項（） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 HoverMenu 控制項提供簡單的快顯視窗效果：當滑鼠指標停留在專案上方時，快顯視窗會出現在 specifi 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e7700e7b-edc3-4183-a713-70e507cc7490
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 3e38b91d837c65191d4b3797fa31ef6112a1f070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578124"
---
# <a name="using-hovermenu-with-a-repeater-control-c"></a>使用 HoverMenu 與重複項控制項 (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)

> AJAX 控制項工具組中的 HoverMenu 控制項提供簡單的快顯視窗效果：當滑鼠指標停留在專案上時，快顯視窗會出現在指定的位置。 您也可以在中繼器中使用此控制項。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的 `HoverMenu` 控制項提供簡單的快顯視窗效果：當滑鼠指標停留在專案上時，快顯視窗會出現在指定的位置。 您也可以在中繼器中使用此控制項。

## <a name="steps"></a>步驟

首先，需要資料來源。 這個範例會使用 AdventureWorks 資料庫和 Microsoft SQL Server 2005 Express Edition。 資料庫是 Visual Studio 安裝（包含 express edition）的選擇性部分，而且也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下個別下載。 AdventureWorks 資料庫是 SQL Server 2005 範例和範例資料庫的一部分（下載于[https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）。 設定資料庫最簡單的方式，就是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）並附加 `AdventureWorks.mdf` 資料庫檔案。

在此範例中，我們假設 SQL Server 2005 Express Edition 的實例呼叫 `SQLEXPRESS` 並與 web 伺服器位於同一部電腦上;這也是預設設定。 如果您的安裝程式不同，則必須調整資料庫的連接資訊。

若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample1.aspx)]

然後，將資料來源加入至頁面。 為了使用有限數量的資料，我們只會在 AdventureWorks 資料庫的 [廠商] 資料表中選取前五個專案。 如果您使用 [Visual Studio 小幫手] 來建立資料來源，請注意，目前版本中的 bug 不會在資料表名稱（`Vendor`）前面加上 `Purchasing`的前置詞。 下列標記會顯示正確的語法：

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample2.aspx)]

接下來，新增可作為強制回應快顯視窗的面板：

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample3.aspx)]

`HoverMenuExtender` 現在就開始了。 因此，資料來源中的每個專案都會取得自己的快顯視窗，而擴充項必須放在中繼器的 `<ItemTemplate>` 區段內。 標記如下：

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample4.aspx)]

現在，資料來源中的每個專案都會在延遲50毫秒（`PopDelay` 屬性）之後，于右側顯示快顯視窗（`PopupPosition` 屬性）。

[![在重複項中的每個專案旁邊都會出現暫留功能表](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)

[暫留] 功能表會顯示在 [中繼器] 中的每個專案旁邊（[按一下以查看完整大小的影像](using-hovermenu-with-a-repeater-control-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [下一個](using-hovermenu-with-a-repeater-control-vb.md)
