---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
title: 搭配資料庫使用 CascadingDropDown （C#） |Microsoft Docs
author: wenz
description: AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入 anoth 中的相關聯值 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 684f0c28-a490-4e5b-b5e5-5dfb77464b49
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
msc.type: authoredcontent
ms.openlocfilehash: bcf453170d17807b4e3b2d2a8b545cba43139f89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78597857"
---
# <a name="using-cascadingdropdown-with-a-database-c"></a><span data-ttu-id="883df-103">使用 CascadingDropDown 搭配資料庫 (C#)</span><span class="sxs-lookup"><span data-stu-id="883df-103">Using CascadingDropDown with a Database (C#)</span></span>

<span data-ttu-id="883df-104">依[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="883df-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="883df-105">[下載程式代碼](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip)或[下載 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="883df-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)</span></span>

> <span data-ttu-id="883df-106">AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入另一個 DropDownList 中的關聯值。</span><span class="sxs-lookup"><span data-stu-id="883df-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="883df-107">為了讓此作業正常，必須建立特殊的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="883df-107">In order for this to work, a special web service must be created.</span></span>

## <a name="overview"></a><span data-ttu-id="883df-108">概觀</span><span class="sxs-lookup"><span data-stu-id="883df-108">Overview</span></span>

<span data-ttu-id="883df-109">AJAX 控制項工具組中的 CascadingDropDown 控制項會擴充 DropDownList 控制項，讓一個 DropDownList 中的變更載入另一個 DropDownList 中的關聯值。</span><span class="sxs-lookup"><span data-stu-id="883df-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="883df-110">（例如，一個清單提供美國州的清單，而下一個清單則會填入該州的主要城市）。為了讓此作業正常，必須建立特殊的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="883df-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) In order for this to work, a special web service must be created.</span></span>

## <a name="steps"></a><span data-ttu-id="883df-111">步驟</span><span class="sxs-lookup"><span data-stu-id="883df-111">Steps</span></span>

<span data-ttu-id="883df-112">首先，需要資料來源。</span><span class="sxs-lookup"><span data-stu-id="883df-112">First of all, a data source is required.</span></span> <span data-ttu-id="883df-113">這個範例會使用 AdventureWorks 資料庫和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="883df-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="883df-114">資料庫是 Visual Studio 安裝（包含 express edition）的選擇性部分，而且也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下個別下載。</span><span class="sxs-lookup"><span data-stu-id="883df-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="883df-115">AdventureWorks 資料庫是 SQL Server 2005 範例和範例資料庫的一部分（下載于[https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）。</span><span class="sxs-lookup"><span data-stu-id="883df-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="883df-116">設定資料庫最簡單的方式，就是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）並附加 `AdventureWorks.mdf` 資料庫檔案。</span><span class="sxs-lookup"><span data-stu-id="883df-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="883df-117">在此範例中，我們假設 SQL Server 2005 Express Edition 的實例呼叫 `SQLEXPRESS` 並與 web 伺服器位於同一部電腦上;這也是預設設定。</span><span class="sxs-lookup"><span data-stu-id="883df-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="883df-118">如果您的安裝程式不同，則必須調整資料庫的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="883df-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="883df-119">若要啟用 ASP.NET AJAX 和控制項工具組的功能，必須將 `ScriptManager` 控制項放在頁面上的任何位置（但在 &lt;`form`&gt; 專案中）：</span><span class="sxs-lookup"><span data-stu-id="883df-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample1.aspx)]

<span data-ttu-id="883df-120">在下一個步驟中，需要兩個 DropDownList 控制項。</span><span class="sxs-lookup"><span data-stu-id="883df-120">In the next step, two DropDownList controls are required.</span></span> <span data-ttu-id="883df-121">在此範例中，我們會使用 AdventureWorks 的廠商和連絡人資訊，因此我們會為可用的廠商建立一個清單，並為可用的連絡人建立一個清單：</span><span class="sxs-lookup"><span data-stu-id="883df-121">In this sample, we use the vendor and contact information from AdventureWorks, thus we create one list for the available vendors and one for the available contacts:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample2.aspx)]

<span data-ttu-id="883df-122">然後，必須將兩個 CascadingDropDown 擴充項加入至頁面。</span><span class="sxs-lookup"><span data-stu-id="883df-122">Then, two CascadingDropDown extenders must be added to the page.</span></span> <span data-ttu-id="883df-123">其中一個會填入第一個（廠商）清單，另一個則填滿第二個（連絡人）清單。</span><span class="sxs-lookup"><span data-stu-id="883df-123">One fills the first (vendors) list, and the other one fills the second (contacts) list.</span></span> <span data-ttu-id="883df-124">必須設定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="883df-124">The following attributes must be set:</span></span>

- <span data-ttu-id="883df-125">`ServicePath`：傳遞清單專案之 web 服務的 URL</span><span class="sxs-lookup"><span data-stu-id="883df-125">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="883df-126">`ServiceMethod`：傳遞清單專案的 Web 方法</span><span class="sxs-lookup"><span data-stu-id="883df-126">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="883df-127">`TargetControlID`：下拉式清單的識別碼</span><span class="sxs-lookup"><span data-stu-id="883df-127">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="883df-128">`Category`：呼叫時提交至 web 方法的類別資訊</span><span class="sxs-lookup"><span data-stu-id="883df-128">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="883df-129">`PromptText`：從伺服器以非同步方式載入清單資料時顯示的文字</span><span class="sxs-lookup"><span data-stu-id="883df-129">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>
- <span data-ttu-id="883df-130">`ParentControlID`：（選擇性）用來觸發載入目前清單的父項下拉式清單</span><span class="sxs-lookup"><span data-stu-id="883df-130">`ParentControlID`: (optional) parent dropdown list that triggers loading of the current list</span></span>

<span data-ttu-id="883df-131">視所使用的程式設計語言而定，有問題的 web 服務名稱會變更，但其他所有屬性值都相同。</span><span class="sxs-lookup"><span data-stu-id="883df-131">Depending on the programming language used, the name of the web service in question changes, but all other attribute values are the same.</span></span> <span data-ttu-id="883df-132">以下是第一個下拉式清單的 CascadingDropDown 元素：</span><span class="sxs-lookup"><span data-stu-id="883df-132">Here is the CascadingDropDown element for the first dropdown list:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample3.aspx)]

<span data-ttu-id="883df-133">第二個清單的控制項擴充項必須設定 `ParentControlID` 屬性，以便選取廠商清單中的專案時，會觸發載入連絡人清單中相關聯的元素。</span><span class="sxs-lookup"><span data-stu-id="883df-133">The control extenders for the second list need to set the `ParentControlID` attribute so that selecting an entry in the vendors list triggers loading associated elements in the contacts list.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample4.aspx)]

<span data-ttu-id="883df-134">然後，實際的工作會在 web 服務中完成，其設定如下所示。</span><span class="sxs-lookup"><span data-stu-id="883df-134">The actual work is then done in the web service, which is set up as follows.</span></span> <span data-ttu-id="883df-135">請注意，會使用 `[ScriptService]` 屬性，否則 ASP.NET AJAX 無法建立 JavaScript proxy 以從用戶端腳本存取 web 方法。</span><span class="sxs-lookup"><span data-stu-id="883df-135">Note that the `[ScriptService]` attribute is used, otherwise ASP.NET AJAX cannot create the JavaScript proxy to access the web methods from client-side script code.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample5.aspx)]

<span data-ttu-id="883df-136">CascadingDropDown 所呼叫之 web 方法的簽章如下所示：</span><span class="sxs-lookup"><span data-stu-id="883df-136">The signature of the web methods called by CascadingDropDown is as follows:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample6.cs)]

<span data-ttu-id="883df-137">因此，傳回值必須是由控制項工具組所定義 `CascadingDropDownNameValue` 類型的陣列。</span><span class="sxs-lookup"><span data-stu-id="883df-137">So the return value must be an array of type `CascadingDropDownNameValue` which is defined by the Control Toolkit.</span></span> <span data-ttu-id="883df-138">`GetVendors()` 方法相當容易執行：程式碼會連接到 AdventureWorks 資料庫，並查詢前25個廠商。</span><span class="sxs-lookup"><span data-stu-id="883df-138">The `GetVendors()` method is quite easy to implement: The code connects to the AdventureWorks database and queries the first 25 vendors.</span></span> <span data-ttu-id="883df-139">`CascadingDropDownNameValue` 的函式中的第一個參數是清單專案的標題，第二個是其值（HTML 的 &lt;中的值屬性 `option`&gt; 元素）。</span><span class="sxs-lookup"><span data-stu-id="883df-139">The first parameter in the `CascadingDropDownNameValue` constructor is the caption of the list entry, the second one its value (value attribute in HTML's &lt;`option`&gt; element).</span></span> <span data-ttu-id="883df-140">程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="883df-140">Here is the code:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample7.cs)]

<span data-ttu-id="883df-141">為廠商取得相關聯的連絡人（方法名稱： `GetContactsForVendor()`）會有點棘手。</span><span class="sxs-lookup"><span data-stu-id="883df-141">Getting the associated contacts for a vendor (method name: `GetContactsForVendor()`) is a bit trickier.</span></span> <span data-ttu-id="883df-142">首先，您必須決定在第一個下拉式清單中選取的廠商。</span><span class="sxs-lookup"><span data-stu-id="883df-142">First of all, the vendor which has been selected in the first dropdown list must be determined.</span></span> <span data-ttu-id="883df-143">控制項工具組會定義該工作的 helper 方法： `ParseKnownCategoryValuesString()` 方法會傳回包含下拉式資料的 `StringDictionary` 元素：</span><span class="sxs-lookup"><span data-stu-id="883df-143">The Control Toolkit defines a helper method for that task: The `ParseKnownCategoryValuesString()` method returns a `StringDictionary` element with the dropdown data:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample8.cs)]

<span data-ttu-id="883df-144">基於安全性理由，必須先驗證此資料。</span><span class="sxs-lookup"><span data-stu-id="883df-144">For security reasons, this data must be validated first.</span></span> <span data-ttu-id="883df-145">因此，如果有 [廠商] 專案（因為第一個 CascadingDropDown 元素的 [`Category`] 屬性設為 [`"Vendor"`]），則可能會抓取所選廠商的識別碼：</span><span class="sxs-lookup"><span data-stu-id="883df-145">So if there is a Vendor entry (because the `Category` property of the first CascadingDropDown element is set to `"Vendor"`), the ID of the selected vendor may be retrieved:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample9.cs)]

<span data-ttu-id="883df-146">方法的其餘部分相當簡單明瞭，然後。</span><span class="sxs-lookup"><span data-stu-id="883df-146">The rest of the method is fairly straight-forward, then.</span></span> <span data-ttu-id="883df-147">廠商的識別碼會作為 SQL 查詢的參數，以取得該廠商所有相關聯的連絡人。</span><span class="sxs-lookup"><span data-stu-id="883df-147">The vendor's ID is used as a parameter for an SQL query that retrieves all associated contacts for that vendor.</span></span> <span data-ttu-id="883df-148">同樣地，方法會傳回 `CascadingDropDownNameValue`類型的陣列。</span><span class="sxs-lookup"><span data-stu-id="883df-148">Once again, the method returns an array of type `CascadingDropDownNameValue`.</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample10.cs)]

<span data-ttu-id="883df-149">載入 ASP.NET 網頁，在短時間後，廠商清單會填入25個專案。</span><span class="sxs-lookup"><span data-stu-id="883df-149">Load the ASP.NET page, and after a short while the vendor list is filled with 25 entries.</span></span> <span data-ttu-id="883df-150">挑選一個專案，並注意第二個下拉式清單如何填入資料。</span><span class="sxs-lookup"><span data-stu-id="883df-150">Pick one entry and notice how the second dropdown list is filled with data.</span></span>

<span data-ttu-id="883df-151">[![第一個清單會自動填滿](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="883df-151">[![The first list is filled automatically](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)</span></span>

<span data-ttu-id="883df-152">第一個清單會自動填滿（[按一下以查看完整大小的影像](using-cascadingdropdown-with-a-database-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="883df-152">The first list is filled automatically ([Click to view full-size image](using-cascadingdropdown-with-a-database-cs/_static/image3.png))</span></span>

<span data-ttu-id="883df-153">[![第二個清單是根據第一個清單中的選取專案來填入](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="883df-153">[![The second list is filled according to the selection in the first list](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)</span></span>

<span data-ttu-id="883df-154">第二個清單是根據第一個清單中的選取專案來填入（[按一下以查看完整大小的影像](using-cascadingdropdown-with-a-database-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="883df-154">The second list is filled according to the selection in the first list ([Click to view full-size image](using-cascadingdropdown-with-a-database-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="883df-155">[上一頁](filling-a-list-using-cascadingdropdown-cs.md)
> [下一頁](presetting-list-entries-with-cascadingdropdown-cs.md)</span><span class="sxs-lookup"><span data-stu-id="883df-155">[Previous](filling-a-list-using-cascadingdropdown-cs.md)
[Next](presetting-list-entries-with-cascadingdropdown-cs.md)</span></span>
