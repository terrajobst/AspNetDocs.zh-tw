---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
title: '反復專案 #1 –建立應用程式（VB） |Microsoft Docs'
author: microsoft
description: 在第一個反復專案中，我們會以最簡單的方式建立連絡人管理員。 我們新增對基本資料庫作業的支援：建立、讀取、更新和 。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 5b033582-1646-42c2-b20d-7edc8814e970
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
msc.type: authoredcontent
ms.openlocfilehash: c6bf4712fb734cf14420fd62c9eaf190a2c28168
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78602316"
---
# <a name="iteration-1--create-the-application-vb"></a>反復專案 #1 –建立應用程式（VB）

由[Microsoft](https://github.com/microsoft)

[下載程式代碼](iteration-1-create-the-application-vb/_static/contactmanager_1_vb1.zip)

> 在第一個反復專案中，我們會以最簡單的方式建立連絡人管理員。 我們新增對基本資料庫作業的支援：建立、讀取、更新和刪除（CRUD）。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>建立連絡人管理 ASP.NET MVC 應用程式（VB）

在這一系列的教學課程中，我們從一開始就建立了整個連絡人管理應用程式。 連絡人管理員應用程式可讓您儲存連絡人資訊名稱、電話號碼和電子郵件地址，以取得人員清單。

我們會透過多個反復專案來建立應用程式。 在每次反覆運算時，我們會逐漸改善應用程式。 這個多個反復專案方法的目標，是要讓您瞭解每項變更的原因。

- 反復專案 #1-建立應用程式。 在第一個反復專案中，我們會以最簡單的方式建立連絡人管理員。 我們新增對基本資料庫作業的支援：建立、讀取、更新和刪除（CRUD）。

- 反復專案 #2-讓應用程式看起來不錯。 在此反復專案中，我們藉由修改預設的 ASP.NET MVC view 主版頁面和級聯樣式表，來改善應用程式的外觀。

- 反復專案 #3-新增表單驗證。 在第三個反復專案中，我們會新增基本表單驗證。 我們會防止人們提交表單，而不需要完成必要的表單欄位。 我們也會驗證電子郵件地址和電話號碼。

- 反復專案 #4-讓應用程式鬆散結合。 在這第四次的反復專案中，我們會利用數種軟體設計模式，讓您更輕鬆地維護和修改 Contact Manager 應用程式。 例如，我們會重構應用程式，以使用存放庫模式和相依性插入模式。

- 反復專案 #5-建立單元測試。 在第五個反復專案中，我們會藉由新增單元測試，讓應用程式更容易維護和修改。 我們會模擬我們的資料模型類別，並為我們的控制器和驗證邏輯建立單元測試。

- 反復專案 #6-使用以測試為導向的開發。 在此第六個反復專案中，我們會先撰寫單元測試，並針對單元測試撰寫程式碼，以將新功能加入至應用程式。 在此反復專案中，我們會新增連絡人群組。

- 反復專案 #7-新增 Ajax 功能。 在第七次的反復專案中，我們藉由新增 Ajax 的支援來改善應用程式的回應性和效能。

## <a name="this-iteration"></a>這個反復專案

在第一個反復專案中，我們會建立基本應用程式。 目標是以最快速且最簡單的方式建立 Contact Manager。 在後續的反復專案中，我們會改善應用程式的設計。

Contact Manager 應用程式是基本的資料庫導向應用程式。 您可以使用此應用程式來建立新的連絡人、編輯現有的連絡人，以及刪除連絡人。

在此反復專案中，我們會完成下列步驟：

1. ASP.NET MVC 應用程式
2. 建立資料庫來儲存我們的連絡人
3. 使用 Microsoft Entity Framework 為我們的資料庫產生模型類別
4. 建立控制器動作和視圖，讓我們列出資料庫中的所有連絡人
5. 建立控制器動作和可讓我們在資料庫中建立新連絡人的視圖
6. 建立控制器動作，以及讓我們編輯資料庫中現有連絡人的視圖
7. 建立控制器動作，以及可讓我們刪除資料庫中現有連絡人的視圖

## <a name="software-prerequisites"></a>軟體必要條件

在 ASP.NET MVC 應用程式中，您必須在電腦上安裝 Visual Studio 2008 或 Visual Web Developer 2008 （Visual Web Developer 是免費版本的 Visual Studio，其中不包含 Visual Studio 的所有 advanced 功能）。 您可以從下列位址下載試用版的 Visual Studio 2008 或 Visual Web Developer：

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> 若要使用 Visual Web Developer ASP.NET MVC 應用程式，您必須安裝 Visual Web Developer Service Pack 1。 若不含 Service Pack 1，您就無法建立 Web 應用程式專案。

ASP.NET MVC 架構。 您可以從下列位址下載 ASP.NET MVC 架構：

[https://www.asp.net/mvc](../../../index.md)

在本教學課程中，我們會使用 Microsoft Entity Framework 來存取資料庫。 Entity Framework 隨附于 .NET Framework 3.5 Service Pack 1。 您可以從下列位置下載此 Service Pack：

[https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;d isplaylang = en](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

另一種方式是逐一執行每個下載，您可以利用 Web Platform Installer （Web PI）。 您可以從下列位址下載 Web PI：

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a>ASP.NET MVC 專案

ASP.NET MVC Web 應用程式專案。 啟動 Visual Studio 並選取 [功能表選項] [檔案] **、[新增專案**]。 [**新增專案**] 對話方塊隨即出現（請參閱 [圖 1]）。 選取 [ **Web** ] 專案類型和 [ **ASP.NET MVC Web 應用程式**] 範本。 將新專案命名為*ContactManager* ，然後按一下 [確定] 按鈕。

請確定您已從 [**新增專案**] 對話方塊右上角的下拉式清單中選取 [.NET Framework 3.5]。 否則，ASP.NET MVC Web 應用程式範本將不會出現。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image1.jpg)](iteration-1-create-the-application-vb/_static/image1.png)

**圖 01**： [新增專案] 對話方塊（[按一下以查看完整大小的影像](iteration-1-create-the-application-vb/_static/image2.png)）

ASP.NET MVC 應用程式時，會出現 [**建立單元測試專案**] 對話方塊。 當您建立 ASP.NET MVC 應用程式時，可以使用此對話方塊來表示您要建立單元測試專案，並將其新增至方案。 雖然我們不會在此反復專案中建立單元測試，但您應該選取 [**是，建立單元測試專案] 選項，** 因為我們計畫要在稍後的反復專案中加入單元測試。 當您第一次建立新的 ASP.NET MVC 專案時加入測試專案，比在建立 ASP.NET MVC 專案之後加入測試專案來得簡單許多。

> [!NOTE] 
> 
> 由於 Visual Web Developer 不支援測試專案，因此當您使用 Visual Web Developer 時，不會取得 [建立單元測試專案] 對話方塊。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image2.jpg)](iteration-1-create-the-application-vb/_static/image3.png)

**圖 02**： [建立單元測試專案] 對話方塊（[按一下以查看完整大小的影像](iteration-1-create-the-application-vb/_static/image4.png)）

ASP.NET MVC 應用程式會出現在 [Visual Studio 方案總管] 視窗中（請參閱 [圖 3]）。 如果您沒有看到 方案總管 視窗，則可以選取 功能表 選項 **查看，方案總管** 來開啟此視窗。 請注意，解決方案包含兩個專案： ASP.NET MVC 專案和測試專案。 ASP.NET MVC 專案的名稱為 ContactManager，而測試專案的名稱為 ContactManager。測試。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image3.jpg)](iteration-1-create-the-application-vb/_static/image5.png)

**圖 03**： [方案總管] 視窗（[按一下以查看完整大小的影像](iteration-1-create-the-application-vb/_static/image6.png)）

## <a name="deleting-the-project-sample-files"></a>刪除專案範例檔案

ASP.NET MVC 專案範本包含控制器和視圖的範例檔案。 在建立新的 ASP.NET MVC 應用程式之前，您應該先刪除這些檔案。 您可以在 [方案總管] 視窗中，以滑鼠右鍵按一下檔案或資料夾，然後選取 [**刪除**] 功能表選項，以刪除檔案和資料夾。

您必須從 ASP.NET MVC 專案中刪除下列檔案：

- \Controllers\HomeController.vb

- \Views\Home\About.aspx

- \Views\Home\Index.aspx

而且，您必須從測試專案中刪除下列檔案：

\Controllers\HomeControllerTest.vb

## <a name="creating-the-database"></a>建立資料庫

Contact Manager 應用程式是資料庫驅動的 web 應用程式。 我們使用資料庫來儲存連絡人資訊。

ASP.NET MVC 架構與任何現代化資料庫，包括 Microsoft SQL Server、Oracle、MySQL 和 IBM DB2 資料庫。 在本教學課程中，我們會使用 Microsoft SQL Server 資料庫。 當您安裝 Visual Studio 時，系統會提供安裝 Microsoft SQL Server Express 的選項，這是 Microsoft SQL Server 資料庫的免費版本。

以滑鼠右鍵按一下 [方案總管] 視窗中的應用程式\_[Data] 資料夾，然後選取功能表選項 [**新增]、[新專案]，** 以建立新的資料庫。 在 [**加入新專案**] 對話方塊中，選取 [**資料**類別目錄] 和 [ **SQL Server 資料庫**] 範本（請參閱 [圖 4]）。 將新的資料庫命名為 ContactManagerDB，然後按一下 [確定] 按鈕。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image4.jpg)](iteration-1-create-the-application-vb/_static/image7.png)

**圖 04**：建立新的 Microsoft SQL Server Express 資料庫（[按一下以查看完整大小的影像](iteration-1-create-the-application-vb/_static/image8.png)）

建立新的資料庫之後，資料庫會出現在 [方案總管] 視窗的 [應用程式\_資料] 資料夾中。 按兩下 [ContactManager] 檔案以開啟 [伺服器總管] 視窗，並連接到資料庫。

> [!NOTE] 
> 
> 在 Microsoft Visual Web Developer 的案例中，[伺服器總管] 視窗稱為 [資料庫總管] 視窗。

您可以使用 [伺服器總管] 視窗來建立新的資料庫物件，例如資料庫資料表、視圖、觸發程式和預存程式。 以滑鼠右鍵按一下 [資料表] 資料夾，然後選取 [**加入新的資料表**] 功能表選項。 資料庫資料表設計工具隨即出現（請參閱 圖 5）。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image5.jpg)](iteration-1-create-the-application-vb/_static/image9.png)

**圖 05**：資料庫資料表設計工具（[按一下以查看完整大小的影像](iteration-1-create-the-application-vb/_static/image10.png)）

我們需要建立包含下列資料行的資料表：

<a id="0.2_table01"></a>

| **資料行名稱** | **資料類型** | **允許 Null** |
| --- | --- | --- |
| ID | int | false |
| FirstName | nvarchar(50) | false |
| LastName | nvarchar(50) | false |
| Phone | nvarchar(50) | false |
| Email | nvarchar(255) | false |

第一個資料行（[識別碼] 資料行）是特殊的。 您必須將識別碼資料行標示為識別欄位和主鍵資料行。 您可以藉由展開 [資料行屬性] （查看 [圖 6] 的底部）並向下滾動至 [識別規格] 屬性，來指出資料行是識別欄位。 將 [ **（Is Identity）** ] 屬性設定為 [**是]** 值。

您可以選取資料行，然後按一下具有索引鍵圖示的按鈕，將資料行標示為主鍵資料行。 將資料行標記為主鍵資料行之後，索引鍵的圖示會出現在資料行的旁邊（請參閱 [圖 6]）。

建立資料表之後，請按一下 [儲存] 按鈕（具有軟碟圖示的按鈕）以儲存新的資料表。 為新資料表命名 [*連絡人*]。

完成建立 Contacts 資料庫資料表之後，您應該在資料表中加入一些記錄。 以滑鼠右鍵按一下 [伺服器總管] 視窗中的 [連絡人] 資料表，然後選取 [**顯示資料表資料**] 功能表選項。 在出現的方格中輸入一或多個連絡人。

## <a name="creating-the-data-model"></a>建立資料模型

ASP.NET MVC 應用程式是由模型、視圖和控制器所組成。 我們一開始先建立一個代表我們在上一節中建立之 Contacts 資料表的模型類別。

在本教學課程中，我們會使用 Microsoft Entity Framework 自動從資料庫產生模型類別。

> [!NOTE] 
> 
> ASP.NET MVC 架構不會以任何方式系結至 Microsoft Entity Framework。 您可以使用 ASP.NET MVC 搭配替代的資料庫存取技術，包括 NHibernate、LINQ to SQL 或 ADO.NET。

請遵循下列步驟來建立資料模型類別：

1. 以滑鼠右鍵按一下 [方案總管] 視窗中的 [模型] 資料夾，然後選取 [**加入]、[新增專案**]。 [新增**專案**] 對話方塊隨即出現（請參閱 [圖 6]）。
2. 選取 [**資料**類別] 和 [ **ADO.NET 實體資料模型**] 範本。 將您的資料模型命名為*ContactManagerModel* ，然後按一下 [**新增**] 按鈕。 [實體資料模型 wizard] 隨即出現（請參閱 [圖 7]）。
3. 在 [**選擇模型內容**] 步驟中，選取 [**從資料庫產生**] （請參閱 [圖 7]）。
4. 在 [**選擇您的資料**連線] 步驟中，選取 [ContactManagerDB] 資料庫，並輸入實體連接設定的名稱*ContactManagerDBEntities* （請參閱 [圖 8]）。
5. 在 [**選擇您的資料庫物件**] 步驟中，選取標示為 [資料表] 的核取方塊（見 [圖 9]）。 資料模型會包含資料庫中包含的所有資料表（其中只有一個 [連絡人] 資料表）。 輸入命名空間*模型*。 按一下 [完成] 按鈕以完成嚮導。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image6.jpg)](iteration-1-create-the-application-vb/_static/image11.png)

**圖 06**： [加入新專案] 對話方塊（[按一下以查看完整大小的影像](iteration-1-create-the-application-vb/_static/image12.png)）

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image7.jpg)](iteration-1-create-the-application-vb/_static/image13.png)

**圖 07**：選擇模型內容（[按一下以查看完整大小的影像](iteration-1-create-the-application-vb/_static/image14.png)）

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image8.jpg)](iteration-1-create-the-application-vb/_static/image15.png)

**圖 08**：選擇您的資料連線（[按一下以查看完整大小的影像](iteration-1-create-the-application-vb/_static/image16.png)）

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image9.jpg)](iteration-1-create-the-application-vb/_static/image17.png)

**圖 09**：選擇您的資料庫物件（[按一下以查看完整大小的影像](iteration-1-create-the-application-vb/_static/image18.png)）

完成實體資料模型 Wizard 之後，實體資料模型設計工具隨即出現。 設計工具會顯示對應至每個模型化之資料表的類別。 您應該會看到一個名為 [連絡人] 的類別。

實體資料模型 wizard 會根據資料庫資料表名稱來產生類別名稱。 您幾乎都需要變更 wizard 所產生的類別名稱。 以滑鼠右鍵按一下設計工具中的 [連絡人] 類別，然後選取 [**重新命名**] 功能表選項。 將類別的名稱從 [連絡人（複數）] 變更為 [連絡人（單數）]。 在您變更類別名稱之後，類別應該會如 [圖 10] 所示。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image10.jpg)](iteration-1-create-the-application-vb/_static/image19.png)

**圖 10**： Contact 類別（[按一下以查看完整大小的影像](iteration-1-create-the-application-vb/_static/image20.png)）

此時，我們已建立資料庫模型。 我們可以使用 Contact 類別來代表資料庫中的特定連絡人記錄。

## <a name="creating-the-home-controller"></a>建立主控制器

下一步是建立我們的主控制器。 Home 控制器是在 ASP.NET MVC 應用程式中叫用的預設控制器。

以滑鼠右鍵按一下 [方案總管] 視窗中的 [控制器] 資料夾，然後選取 [**新增]、[控制器**] 功能表選項（請參閱 [圖 11]），以建立主控制器類別。 請注意，標示**為 [新增]、[更新] 和 [詳細資料] 情節的動作方法**。 請確定已核取此核取方塊，然後再按一下 [**新增**] 按鈕。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image11.jpg)](iteration-1-create-the-application-vb/_static/image21.png)

**圖 11**：新增主控制器（[按一下以觀看完整大小的影像](iteration-1-create-the-application-vb/_static/image22.png)）

當您建立主控制器時，您會取得清單1中的類別。

**清單 1-Controllers\HomeController.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample1.vb)]

## <a name="listing-the-contacts"></a>列出連絡人

為了顯示 [連絡人] 資料庫資料表中的記錄，我們需要建立索引（）動作和索引視圖。

Home 控制器已經包含 Index （）動作。 我們需要修改這個方法，使其看起來像 [清單 2]。

**清單 2-Controllers\HomeController.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample2.vb)]

請注意，[清單 2] 中的 Home 控制器類別包含名為 \_實體的私用欄位。 [\_實體] 欄位代表資料模型中的實體。 我們會使用 [\_實體] 欄位來與資料庫通訊。

Index （）方法會傳回代表連絡人資料庫資料表中所有連絡人的視圖。 運算式 \_的實體。ContactSet. ToList （）會傳回連絡人清單做為泛型清單。

既然我們已建立索引控制器，接下來我們需要建立索引視圖。 建立索引視圖之前，請先選取 [**組建]、[組建方案**] 功能表選項來編譯您的應用程式。 在加入視圖之前，您應該一律編譯專案，以便在 [**加入視圖**] 對話方塊中顯示模型類別清單。

以滑鼠右鍵按一下 [索引] （）方法，然後選取 [**加入視圖**] 功能表選項（請參閱 [圖 12]），即可建立索引視圖。 選取此功能表選項會開啟 [**加入視圖**] 對話方塊（請參閱 [圖 13]）。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image12.jpg)](iteration-1-create-the-application-vb/_static/image23.png)

**圖 12**：新增索引視圖（[按一下以觀看完整大小的影像](iteration-1-create-the-application-vb/_static/image24.png)）

在 [**加入視圖**] 對話方塊中，核取標示為 [**建立強型別的視圖**] 的核取方塊。 選取 [View data class ContactManager. Contact] 和 [View content] 清單。 選取這些選項會產生一個顯示連絡人記錄清單的視圖。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image13.jpg)](iteration-1-create-the-application-vb/_static/image25.png)

**圖 13**： [加入視圖] 對話方塊（[按一下以查看完整大小的影像](iteration-1-create-the-application-vb/_static/image26.png)）

當您按一下 [**新增**] 按鈕時，就會產生 [清單 3] 中的索引視圖。 請注意，出現在檔案頂端的 &lt;% @ Page%&gt; 指示詞。 索引視圖會繼承自 ViewPage&lt;IEnumerable&lt;ContactManager&gt;&gt; 類別。 換句話說，視圖中的 Model 類別代表連絡人實體的清單。

索引視圖的主體包含 foreach 迴圈，可逐一查看模型類別所代表的每個連絡人。 Contact 類別的每個屬性值都會顯示在 HTML 資料表中。

**清單 3-Views\Home\Index.aspx （未修改）**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample3.aspx)]

我們需要對索引視圖進行一次修改。 因為我們不會建立詳細資料檢視，所以我們可以移除 [詳細資料] 連結。 從 [索引] 視圖中尋找並移除下列程式碼：

{. id = item。識別碼}）%&gt;

修改索引視圖之後，您可以執行 Contact Manager 應用程式。 選取功能表選項 [Debug]、[開始調試]，或直接按 F5。 第一次執行應用程式時，您會看到 [圖 14] 中的對話方塊。 選取 [**修改 web.config 檔案以啟用調試**] 選項，然後按一下 [確定] 按鈕。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image14.jpg)](iteration-1-create-the-application-vb/_static/image27.png)

**圖 14**：啟用調試（[按一下以查看完整大小的影像](iteration-1-create-the-application-vb/_static/image28.png)）

預設會傳回索引視圖。 此視圖會列出 [連絡人] 資料庫資料表中的所有資料（請參閱 [圖 15]）。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image15.jpg)](iteration-1-create-the-application-vb/_static/image29.png)

**圖 15**：索引視圖（[按一下以查看完整大小的影像](iteration-1-create-the-application-vb/_static/image30.png)）

請注意，索引視圖包含在視圖底部標示為 [建立新的] 的連結。 在下一節中，您將瞭解如何建立新的連絡人。

## <a name="creating-new-contacts"></a>建立新連絡人

若要讓使用者能夠建立新的連絡人，我們必須將兩個 Create （）動作新增至主控制器。 我們需要建立一個 Create （）動作，以傳回用來建立新連絡人的 HTML 表單。 我們需要建立第二個 Create （）動作，以執行新連絡人的實際資料庫插入。

我們需要新增至主控制器的新 Create （）方法包含在 [清單 4] 中。

**清單 4-Controllers\HomeController.vb （含 Create 方法）**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample4.vb)]

第一個 Create （）方法可以使用 HTTP GET 叫用，而第二個 Create （）方法只能由 HTTP POST 叫用。 換句話說，只有在張貼 HTML 表單時，才可以叫用第二個 Create （）方法。 第一個 Create （）方法只會傳回一個視圖，其中包含用於建立新連絡人的 HTML 表單。 第二個 Create （）方法更為有趣：它會將新的連絡人加入資料庫。

請注意，第二個 Create （）方法已經過修改，可接受 Contact 類別的實例。 從 HTML 表單張貼的表單值會由 ASP.NET MVC 架構自動系結至這個連絡人類別。 HTML 建立表單中的每個表單欄位都會指派給 Contact 參數的屬性。

請注意，Contact 參數是以 [Bind] 屬性裝飾。 [Bind] 屬性是用來從系結中排除 Contact Id 屬性。 因為 Id 屬性代表識別屬性，所以我們不想要設定 Id 屬性。

在 Create （）方法的主體中，Entity Framework 是用來將新的連絡人插入資料庫中。 新的連絡人會加入至現有的連絡人集，並呼叫 SaveChanges （）方法，將這些變更推送回基礎資料庫。

您可以用滑鼠右鍵按一下兩個 Create （）方法，然後選取功能表選項 [**加入視圖**] （請參閱 [圖 16]），產生建立新連絡人的 HTML 表單。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image16.jpg)](iteration-1-create-the-application-vb/_static/image31.png)

**圖 16**：新增 Create View （[按一下以觀看完整大小的影像](iteration-1-create-the-application-vb/_static/image32.png)）

在 [**加入視圖**] 對話方塊中，選取 [ **ContactManager** ] 類別和 [視圖內容] 的 [**建立**] 選項（請參閱 [圖 17]）。 當您按一下 [**新增**] 按鈕時，就會自動產生 Create view。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image17.jpg)](iteration-1-create-the-application-vb/_static/image33.png)

**圖 17**：查看頁面分解（[按一下以觀看完整大小的影像](iteration-1-create-the-application-vb/_static/image34.png)）

[建立] 視圖包含 Contact 類別之每個屬性的表單欄位。 [建立] 視圖的程式碼包含在 [清單 5] 中。

**清單 5-Views\Home\Create.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample5.aspx)]

修改 Create （）方法並新增 Create view 之後，您可以執行 Contact manager 應用程式，並建立新的連絡人。 按一下 [索引] 視圖中出現的 [**建立新**的] 連結，以流覽至 [建立] 視圖。 您應該會在 [圖 18] 看到此視圖。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image18.jpg)](iteration-1-create-the-application-vb/_static/image35.png)

**圖 18**： [建立] 視圖（[按一下以查看完整大小的影像](iteration-1-create-the-application-vb/_static/image36.png)）

## <a name="editing-contacts"></a>編輯連絡人

加入編輯連絡人記錄的功能，與加入建立新連絡人記錄的功能非常類似。 首先，我們需要將兩個新的編輯方法加入至 Home 控制器類別。 這些新的 Edit （）方法包含在 [清單 6] 中。

**清單 6-Controllers\HomeController.vb （含編輯方法）**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample6.vb)]

第一個 Edit （）方法是由 HTTP GET 作業叫用。 識別碼參數會傳遞給這個方法，代表正在編輯之連絡人記錄的識別碼。 Entity Framework 是用來抓取符合識別碼的連絡人。會傳回包含編輯記錄之 HTML 表單的視圖。

第二個 Edit （）方法會對資料庫執行實際的更新。 這個方法會接受 Contact 類別的實例做為參數。 ASP.NET MVC 架構會自動將表單欄位從編輯表單系結到這個類別。 請注意，當您編輯連絡人時，不會包含 [Bind] 屬性（我們需要 Id 屬性的值）。

Entity Framework 可用來將修改過的連絡人儲存至資料庫。 原始連絡人必須先從資料庫中抓取。 接下來，會呼叫 Entity Framework ApplyPropertyChanges （）方法來記錄連絡人的變更。 最後，會呼叫 Entity Framework SaveChanges （）方法，將變更保存至基礎資料庫。

以滑鼠右鍵按一下 [編輯] （）方法，然後選取 [新增視圖] 功能表選項，即可產生包含編輯表單的視圖。 在 [加入視圖] 對話方塊中，選取 [ **ContactManager** ] 類別和 [**編輯**視圖] 內容（請參閱 [圖 19]）。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image19.jpg)](iteration-1-create-the-application-vb/_static/image37.png)

**圖 19**：新增編輯檢視（[按一下以觀看完整大小的影像](iteration-1-create-the-application-vb/_static/image38.png)）

當您按一下 [新增] 按鈕時，就會自動產生新的編輯檢視。 產生的 HTML 表單包含對應至 Contact 類別之每個屬性的欄位（請參閱 [清單 7]）。

**清單 7-Views\Home\Edit.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample7.aspx)]

## <a name="deleting-contacts"></a>刪除連絡人

如果您想要刪除連絡人，則需要將兩個 Delete （）動作新增至 Home 控制器類別。 第一個 Delete （）動作會顯示刪除確認表單。 第二個 Delete （）動作會執行實際的刪除。

> [!NOTE] 
> 
> 之後，在反復專案 #7 中，我們會修改 Contact Manager，使其支援一個步驟 Ajax delete。

[清單 8] 中包含兩個新的 Delete （）方法。

**清單 8-Controllers\HomeController.vb （Delete 方法）**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample8.vb)]

第一個 Delete （）方法會傳回確認表單，以便從資料庫中刪除連絡人記錄（請參閱 Figure20）。 第二個 Delete （）方法會對資料庫執行實際的刪除作業。 從資料庫抓取原始連絡人之後，會呼叫 Entity Framework DeleteObject （）和 SaveChanges （）方法來執行資料庫刪除。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image20.jpg)](iteration-1-create-the-application-vb/_static/image39.png)

**圖 20**：刪除確認視圖（[按一下以查看完整大小的影像](iteration-1-create-the-application-vb/_static/image40.png)）

我們需要修改索引視圖，使其包含刪除連絡人記錄的連結（請參閱 [圖 21]）。 您必須將下列程式碼加入至包含編輯連結的相同資料表資料格：

{. id = item。識別碼}）%&gt;

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image21.jpg)](iteration-1-create-the-application-vb/_static/image41.png)

**圖 21**：具有編輯連結的索引視圖（[按一下以查看完整大小的影像](iteration-1-create-the-application-vb/_static/image42.png)）

接下來，我們需要建立刪除確認視圖。 以滑鼠右鍵按一下 Home 控制器類別中的 Delete （）方法，然後選取 [新增視圖] 功能表選項。 [加入視圖] 對話方塊隨即出現（請參閱 [圖 22]）。

不同于清單的案例、建立和編輯檢視，[加入視圖] 對話方塊不會包含建立刪除視圖的選項。 相反地，請選取 [ **ContactManager** ] 資料類別和 [**空白**視圖內容]。 選取 [空白視圖內容] 選項將需要我們自己建立視圖。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image22.jpg)](iteration-1-create-the-application-vb/_static/image43.png)

**圖 22**：新增刪除確認視圖（[按一下以觀看完整大小的影像](iteration-1-create-the-application-vb/_static/image44.png)）

[刪除] 視圖的內容包含在 [清單 9] 中。 此視圖包含一個表單，可確認是否應刪除特定的連絡人（請參閱 [圖 21]）。

**清單 9-Views\Home\Delete.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a>變更預設控制器的名稱

這可能會讓您想要讓使用連絡人的控制器類別名稱命名為 HomeController 類別。 控制器不應該命名為 ContactController 嗎？

這個問題很容易修正。 首先，我們需要重構主控制器的名稱。 在 Visual Studio Code 編輯器中開啟 HomeController 類別，以滑鼠右鍵按一下類別的名稱，然後選取 [**重新命名**] 功能表選項。 選取此功能表選項會開啟 [重新命名] 對話方塊。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image23.jpg)](iteration-1-create-the-application-vb/_static/image45.png)

**圖 23**：重構控制器名稱（[按一下以查看完整大小的影像](iteration-1-create-the-application-vb/_static/image46.png)）

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image24.jpg)](iteration-1-create-the-application-vb/_static/image47.png)

**圖 24**：使用 [重新命名] 對話方塊（[按一下以查看完整大小的影像](iteration-1-create-the-application-vb/_static/image48.png)）

如果您將控制器類別重新命名，Visual Studio 也會在 [Views] 資料夾中更新資料夾的名稱。 Visual Studio 會將 \Views\Home 資料夾重新命名為 \Views\Contact 資料夾。

進行這種變更之後，您的應用程式將不再有主控制器。 當您執行應用程式時，您會看到 [圖 25] 中的錯誤頁面。

[![[新增專案] 對話方塊](iteration-1-create-the-application-vb/_static/image25.jpg)](iteration-1-create-the-application-vb/_static/image49.png)

**圖 25**：沒有預設控制器（[按一下以觀看完整大小的影像](iteration-1-create-the-application-vb/_static/image50.png)）

我們必須更新 global.asax 檔案中的預設路由，才能使用連絡人控制器，而不是主控制器。 開啟 global.asax 檔案，並修改預設路由所使用的預設控制器（請參閱 [清單 10]）。

**清單 10-global.asax .vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample10.vb)]

在您進行這些變更之後，Contact Manager 就會正確執行。 現在，它會使用 Contact controller 類別做為預設控制器。

## <a name="summary"></a>總結

在第一次的反復專案中，我們以最快速的方式建立了基本的 Contact Manager 應用程式。 我們利用 Visual Studio 來自動產生控制器和 views 的初始程式碼。 我們也利用 Entity Framework 來自動產生我們的資料庫模型類別。

目前，我們可以使用 Contact Manager 應用程式來列出、建立、編輯和刪除連絡人記錄。 換句話說，我們可以執行資料庫驅動 web 應用程式所需的所有基本資料庫作業。

可惜的是，我們的應用程式有一些問題。 首先，我想承認這一點，Contact Manager 應用程式並不是最吸引人的應用程式。 它需要一些設計工作。 在下一個反復專案中，我們將探討如何變更預設的視圖主版頁面和級聯樣式表，以改善應用程式的外觀。

第二，我們尚未實行任何表單驗證。 例如，沒有任何內容可以防止您提交建立連絡人表單，而不需要輸入任何表單欄位的值。 此外，您可以輸入不正確電話號碼和電子郵件地址。 我們開始在反復專案 #3 中解決表單驗證的問題。

最後，最重要的是，無法輕鬆地修改或維護連絡人管理員應用程式的目前反復專案。 例如，資料庫存取邏輯會直接內建至控制器動作。 這表示我們無法修改我們的資料存取程式碼，而不需要修改控制器。 在稍後的反復專案中，我們會探索可執行檔軟體設計模式，讓 Contact Manager 更有彈性地進行變更。

> [!div class="step-by-step"]
> [上一頁](iteration-7-add-ajax-functionality-cs.md)
> [下一頁](iteration-2-make-the-application-look-nice-vb.md)
