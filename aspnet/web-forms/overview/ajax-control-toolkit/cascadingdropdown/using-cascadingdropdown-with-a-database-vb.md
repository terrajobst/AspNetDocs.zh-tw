---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-vb
title: 使用 CascadingDropDown 搭配資料庫（VB） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入 anoth 中的相關聯值 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 97a3d33c-c856-43f3-8acb-f1ccbc48221a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-vb
msc.type: authoredcontent
ms.openlocfilehash: 4482aa18c4446ec8f5f160c423008398ea2e1d0d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599502"
---
# <a name="using-cascadingdropdown-with-a-database-vb"></a>使用 CascadingDropDown 搭配資料庫 (VB)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.vb.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1VB.pdf)

> AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入另一個 DropDownList 中的關聯值。 為了讓此作業正常，必須建立特殊的 web 服務。

## <a name="overview"></a>概觀

AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入另一個 DropDownList 中的關聯值。 （例如，一個清單提供美國州的清單，而下一個清單則會填入該州的主要城市）。為了讓此作業正常，必須建立特殊的 web 服務。

## <a name="steps"></a>步驟

首先，需要資料來源。 這個範例會使用 AdventureWorks 資料庫和 Microsoft SQL Server 2005 Express Edition。 資料庫是 Visual Studio 安裝（包含 express edition）的選擇性部分，而且也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下個別下載。 AdventureWorks 資料庫是 SQL Server 2005 範例和範例資料庫的一部分（下載于[https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）。 設定資料庫最簡單的方式，就是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）並附加 `AdventureWorks.mdf` 資料庫檔案。

在此範例中，我們假設 SQL Server 2005 Express Edition 的實例呼叫 `SQLEXPRESS` 並與 web 伺服器位於同一部電腦上;這也是預設設定。 如果您的安裝程式不同，則必須調整資料庫的連接資訊。

若要啟用 ASP.NET AJAX 和控制項工具組的功能，必須將 `ScriptManager` 控制項放在頁面上的任何位置（但在 &lt;`form`&gt; 專案中）：

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample1.aspx)]

在下一個步驟中，需要兩個 DropDownList 控制項。 在此範例中，我們會使用 AdventureWorks 的廠商和連絡人資訊，因此我們會為可用的廠商建立一個清單，並為可用的連絡人建立一個清單：

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample2.aspx)]

然後，必須將兩個 CascadingDropDown 擴充項加入至頁面。 其中一個會填入第一個（廠商）清單，另一個則填滿第二個（連絡人）清單。 必須設定下列屬性：

- `ServicePath`：傳遞清單專案之 web 服務的 URL
- `ServiceMethod`：傳遞清單專案的 Web 方法
- `TargetControlID`：下拉式清單的識別碼
- `Category`：呼叫時提交至 web 方法的類別資訊
- `PromptText`：從伺服器以非同步方式載入清單資料時顯示的文字
- `ParentControlID`：（選擇性）用來觸發載入目前清單的父項下拉式清單

視所使用的程式設計語言而定，有問題的 web 服務名稱會變更，但其他所有屬性值都相同。 以下是第一個下拉式清單的 CascadingDropDown 元素：

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample3.aspx)]

第二個清單的控制項擴充項必須設定 `ParentControlID` 屬性，以便選取廠商清單中的專案時，會觸發載入連絡人清單中相關聯的元素。

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample4.aspx)]

然後，實際的工作會在 web 服務中完成，其設定如下所示。 請注意，會使用 `[ScriptService]` 屬性，否則 ASP.NET AJAX 無法建立 JavaScript proxy 以從用戶端腳本存取 web 方法。

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample5.aspx)]

CascadingDropDown 所呼叫之 web 方法的簽章如下所示：

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample6.vb)]

因此，傳回值必須是由控制項工具組所定義 `CascadingDropDownNameValue` 類型的陣列。 `GetVendors()` 方法相當容易執行：程式碼會連接到 AdventureWorks 資料庫，並查詢前25個廠商。 `CascadingDropDownNameValue` 的函式中的第一個參數是清單專案的標題，第二個是其值（HTML 的 &lt;中的值屬性 `option`&gt; 元素）。 以下是程式碼：

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample7.vb)]

為廠商取得相關聯的連絡人（方法名稱： `GetContactsForVendor()`）會有點棘手。 首先，您必須決定在第一個下拉式清單中選取的廠商。 控制項工具組會定義該工作的 helper 方法： `ParseKnownCategoryValuesString()` 方法會傳回包含下拉式資料的 `StringDictionary` 元素：

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample8.vb)]

基於安全性理由，必須先驗證此資料。 因此，如果有 [廠商] 專案（因為第一個 CascadingDropDown 元素的 [`Category`] 屬性設為 [`"Vendor"`]），則可能會抓取所選廠商的識別碼：

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample9.vb)]

方法的其餘部分相當簡單明瞭，然後。 廠商的識別碼會作為 SQL 查詢的參數，以取得該廠商所有相關聯的連絡人。 同樣地，方法會傳回 `CascadingDropDownNameValue`類型的陣列。

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample10.vb)]

載入 ASP.NET 網頁，在短時間後，廠商清單會填入25個專案。 挑選一個專案，並注意第二個下拉式清單如何填入資料。

[![第一個清單會自動填滿](using-cascadingdropdown-with-a-database-vb/_static/image2.png)](using-cascadingdropdown-with-a-database-vb/_static/image1.png)

第一個清單會自動填滿（[按一下以查看完整大小的影像](using-cascadingdropdown-with-a-database-vb/_static/image3.png)）

[![第二個清單是根據第一個清單中的選取專案來填入](using-cascadingdropdown-with-a-database-vb/_static/image5.png)](using-cascadingdropdown-with-a-database-vb/_static/image4.png)

第二個清單是根據第一個清單中的選取專案來填入（[按一下以查看完整大小的影像](using-cascadingdropdown-with-a-database-vb/_static/image6.png)）

> [!div class="step-by-step"]
> [上一頁](filling-a-list-using-cascadingdropdown-vb.md)
> [下一頁](presetting-list-entries-with-cascadingdropdown-vb.md)
