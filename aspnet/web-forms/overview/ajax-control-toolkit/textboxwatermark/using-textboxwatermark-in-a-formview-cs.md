---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-cs
title: 在 FormView 中使用 TextBoxWatermark （C#） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 TextBoxWatermark 控制項會擴充一個文字方塊，讓文字顯示在方塊中。 當使用者按一下方塊時，我 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e6ee90bf-32a5-4987-a384-15cc7dd30c8a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-cs
msc.type: authoredcontent
ms.openlocfilehash: 13ac0da5ca53756aa7c660cdc47c96f0c865b006
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611334"
---
# <a name="using-textboxwatermark-in-a-formview-c"></a>在 FormView 中使用 TextBoxWatermark (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1CS.pdf)

> AJAX 控制項工具組中的 TextBoxWatermark 控制項會擴充一個文字方塊，讓文字顯示在方塊中。 當使用者按一下方塊時，就會清空。 如果使用者離開方塊而不輸入文字，預先填入的文字就會重新出現。 這也可以在 FormView 控制項內使用。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的 `TextBoxWatermark` 控制項會擴充一個文字方塊，讓文字顯示在方塊中。 當使用者按一下方塊時，就會清空。 如果使用者離開方塊而不輸入文字，預先填入的文字就會重新出現。 這也可以在 `FormView` 控制項內進行。

## <a name="steps"></a>步驟

首先，需要資料來源。 這個範例會使用 AdventureWorks 資料庫和 Microsoft SQL Server 2005 Express Edition。 資料庫是 Visual Studio 安裝（包含 express edition）的選擇性部分，而且也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下個別下載。 AdventureWorks 資料庫是 SQL Server 2005 範例和範例資料庫的一部分（下載于[https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）。 設定資料庫最簡單的方式，就是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）並附加 `AdventureWorks.mdf` 資料庫檔案。

在此範例中，我們假設 SQL Server 2005 Express Edition 的實例呼叫 `SQLEXPRESS` 並與 web 伺服器位於同一部電腦上;這也是預設設定。 如果您的安裝程式不同，則必須調整資料庫的連接資訊。

若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：

[!code-aspx[Main](using-textboxwatermark-in-a-formview-cs/samples/sample1.aspx)]

然後，將資料來源加入至支援 `DELETE`、`INSERT` 和 `UPDATE` SQL 語句的頁面。 如果您使用 [Visual Studio 小幫手] 來建立資料來源，請注意，目前版本中的 bug 不會在資料表名稱（`Vendor`）前面加上 `Purchasing`的前置詞。 下列標記會顯示正確的語法：

[!code-aspx[Main](using-textboxwatermark-in-a-formview-cs/samples/sample2.aspx)]

請記住資料來源的名稱（`ID`），因為它將在 `FormView` 控制項的 `DataSourceID` 屬性中使用。 `FormView` 的 [`<InsertItemTemplate>`] 區段包含 [`TextBoxWatermarkExtender`] 控制項所延伸的文字方塊。 請確定擴充項位於範本中，而不在其外部。

[!code-aspx[Main](using-textboxwatermark-in-a-formview-cs/samples/sample3.aspx)]

現在當使用者變更為 `FormView` 控制項的插入模式時，新廠商的文字欄位會預先填入 `TextBoxWatermarkExtender` 控制項。 在文字方塊內按一下可讓填充文字消失。

[![欄位中的浮水印來自于擴充項](using-textboxwatermark-in-a-formview-cs/_static/image2.png)](using-textboxwatermark-in-a-formview-cs/_static/image1.png)

欄位中的浮水印來自于擴充項（[按一下以查看完整大小的影像](using-textboxwatermark-in-a-formview-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [下一步](using-textboxwatermark-with-validation-controls-cs.md)
