---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-vb
title: 搭配重複使用 ModalPopup 與重複項控制項（VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。 也可以使用此 contr 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0c8e74f1-b3ba-4ca9-a1c5-f5c4831a359a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 0966770f0218ca91ba7d25e7bf703bf7b005738e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606534"
---
# <a name="using-modalpopup-with-a-repeater-control-vb"></a>使用 ModalPopup 與重複項控制項 (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.vb.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2VB.pdf)

> AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。 您也可以在中繼器中使用此控制項。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的 ModalPopup 控制項提供一個簡單的方式，讓您使用用戶端的方法來建立強制回應快顯視窗。 您也可以在中繼器中使用此控制項。

## <a name="steps"></a>步驟

首先，需要資料來源。 這個範例會使用 AdventureWorks 資料庫和 Microsoft SQL Server 2005 Express Edition。 資料庫是 Visual Studio 安裝（包含 express edition）的選擇性部分，而且也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下個別下載。 AdventureWorks 資料庫是 SQL Server 2005 範例和範例資料庫的一部分（下載于[https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）。 設定資料庫最簡單的方式，就是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）並附加 `AdventureWorks.mdf` 資料庫檔案。 在此範例中，我們假設 SQL Server 2005 Express Edition 的實例呼叫 `SQLEXPRESS` 並與 web 伺服器位於同一部電腦上;這也是預設設定。 如果您的安裝程式不同，則必須調整資料庫的連接資訊。 若要啟用 ASP.NET AJAX 和控制項工具組的功能，`ScriptManager` 控制項必須放在頁面上的任何位置（但在 `<form>` 元素內）：

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample1.aspx)]

然後，將資料來源加入至頁面。 為了使用有限數量的資料，我們只會在 AdventureWorks 資料庫的 [廠商] 資料表中選取前五個專案。 如果您使用 [Visual Studio 小幫手] 來建立資料來源，請注意，目前版本中的 bug 不會在資料表名稱（`Vendor`）前面加上 `Purchasing`的前置詞。 下列標記會顯示正確的語法：

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample2.aspx)]

接下來，新增可作為強制回應快顯視窗的面板。 它包含 `Button` 控制項，可再次關閉快顯視窗：

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample3.aspx)]

若要在中繼器內進行快顯工作，`ModalPopupExtender` 控制項必須放在中繼器的 `<ItemTemplate>` 區段內。 因此，面板會在中繼器外，但擴充項位於內部。 以下是中繼器的標記：

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-vb/samples/sample4.aspx)]

然後會顯示資料來源中的每個專案，並在其旁邊出現一個按鈕，以觸發強制回應快顯視窗。

[![可以為每個資料來源專案觸發強制回應快顯視窗](using-modalpopup-with-a-repeater-control-vb/_static/image2.png)](using-modalpopup-with-a-repeater-control-vb/_static/image1.png)

可以為每個資料來源專案觸發強制回應快顯視窗（[按一下以查看完整大小的影像](using-modalpopup-with-a-repeater-control-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一頁](launching-a-modal-popup-window-from-server-code-vb.md)
> [下一頁](handling-postbacks-from-a-modalpopup-vb.md)
