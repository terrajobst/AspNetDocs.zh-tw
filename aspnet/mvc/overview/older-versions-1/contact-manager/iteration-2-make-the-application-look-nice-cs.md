---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
title: '反復專案 #2 –讓應用程式看起來C#不錯（） |Microsoft Docs'
author: microsoft
description: 在此反復專案中，我們藉由修改預設的 ASP.NET MVC view 主版頁面和級聯樣式表，來改善應用程式的外觀。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f1173feb-11ee-4017-8f3f-86599ea6ae13
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
msc.type: authoredcontent
ms.openlocfilehash: 246cb4b4668339cc4b7e4e03ea005102c6a2a5c3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78602015"
---
# <a name="iteration-2--make-the-application-look-nice-c"></a>反復專案 #2 –讓應用程式看起來C#不錯（）

由[Microsoft](https://github.com/microsoft)

[下載程式代碼](iteration-2-make-the-application-look-nice-cs/_static/contactmanager_2_cs1.zip)

> 在此反復專案中，我們藉由修改預設的 ASP.NET MVC view 主版頁面和級聯樣式表，來改善應用程式的外觀。

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>建立連絡人管理 ASP.NET MVC 應用程式（C#）

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

這項反復專案的目標是要改善 Contact Manager 應用程式的外觀。 目前，Contact Manager 會使用預設的 ASP.NET MVC view 主版頁面和級聯樣式表（請參閱 [圖 1]）。 這些外觀看起來不正確，但我不想讓 Contact Manager 看起來像是其他每個 ASP.NET 的 MVC 網站。 我想要以自訂檔案取代這些檔案。

[![[新增專案] 對話方塊](iteration-2-make-the-application-look-nice-cs/_static/image1.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image1.png)

**圖 01**： ASP.NET MVC 應用程式的預設面板（[按一下以查看完整大小的影像](iteration-2-make-the-application-look-nice-cs/_static/image2.png)）

在此反復專案中，我將討論兩種改善應用程式視覺化設計的方法。 首先，我會示範如何利用 ASP.NET MVC 設計資源庫來下載免費的 ASP.NET MVC 設計範本。 ASP.NET MVC 設計資源庫可讓您建立專業 web 應用程式，而不需要執行任何工作。

我決定不要針對 Contact Manager 應用程式使用 ASP.NET MVC 設計資源庫中的範本。 而是由專業設計公司所建立的自訂設計。 在本教學課程的第二個部分中，我將說明如何與專業設計公司合作，以建立最終的 ASP.NET MVC 設計。

## <a name="the-aspnet-mvc-design-gallery"></a>ASP.NET MVC 設計資源庫

ASP.NET MVC 設計元件庫是 Microsoft 所提供的免費資源。 ASP.NET MVC 資源庫位於下列位址：

[https://www.asp.net/mvc/gallery](https://www.asp.net/mvc/gallery)

ASP.NET MVC 設計資源庫所裝載的免費網站設計集合，是特別為了在 ASP.NET MVC 專案中使用而建立的。 設計是由「社區」的成員上傳。 資源庫的訪客可以為其最愛的設計投票（請參閱 [圖 2]）。

[![[新增專案] 對話方塊](iteration-2-make-the-application-look-nice-cs/_static/image2.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image3.png)

**圖 02**： ASP.NET MVC 設計資源庫（[按一下以觀看完整大小的影像](iteration-2-make-the-application-look-nice-cs/_static/image4.png)）

當我撰寫本教學課程時，資源庫中最受歡迎的設計是一個名為10月的設計，David Hauser。 您可以藉由完成下列步驟，將此設計用於 ASP.NET MVC 專案：

1. 按一下 [**下載**] 按鈕，將10月份的 .zip 檔案下載到您的電腦。
2. 以滑鼠右鍵按一下下載的2006年10月 .zip 檔案，然後按一下 [**解除封鎖**] 按鈕（請參閱 [圖 3]）。
3. 將檔案解壓縮至名為十月的資料夾。
4. 從10月資料夾中包含的 DesignTemplate 資料夾選取所有檔案，在檔案上按一下滑鼠右鍵，然後選取功能表選項 [**複製**]。
5. 以滑鼠右鍵按一下 [Visual Studio 方案總管] 視窗中的 [ContactManager] 專案節點，然後選取 [**貼**上] 功能表選項（請參閱 [圖 4]）。
6. 選取 Visual Studio 功能表選項 [**編輯]、[尋找和取代]、[快速取代** *] 和 [將 [MyProjectName]* 取代為*ContactManager* ] （請參閱 [圖 5]）。

[![[新增專案] 對話方塊](iteration-2-make-the-application-look-nice-cs/_static/image3.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image5.png)

**圖 03**：解除封鎖從 web 下載的檔案（[按一下以觀看完整大小的影像](iteration-2-make-the-application-look-nice-cs/_static/image6.png)）

[![[新增專案] 對話方塊](iteration-2-make-the-application-look-nice-cs/_static/image4.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image7.png)

**圖 04**：覆寫方案總管中的檔案（[按一下以查看完整大小的影像](iteration-2-make-the-application-look-nice-cs/_static/image8.png)）

[![[新增專案] 對話方塊](iteration-2-make-the-application-look-nice-cs/_static/image5.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image9.png)

**圖 05**：以 ContactManager 取代 [專案名稱] （[按一下以查看完整大小的影像](iteration-2-make-the-application-look-nice-cs/_static/image10.png)）

完成這些步驟之後，您的 web 應用程式將會使用新的設計。 [圖 6] 中的頁面說明了具有10月份設計的 Contact Manager 應用程式外觀。

[![[新增專案] 對話方塊](iteration-2-make-the-application-look-nice-cs/_static/image6.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image11.png)

**圖 06**：具有10月份範本的 ContactManager （[按一下以觀看完整大小的影像](iteration-2-make-the-application-look-nice-cs/_static/image12.png)）

## <a name="creating-a-custom-aspnet-mvc-design"></a>建立自訂 ASP.NET MVC 設計

ASP.NET MVC 設計資源庫可以選擇不同的設計樣式。 資源庫可讓您輕鬆地自訂 ASP.NET MVC 應用程式的外觀。 當然，資源庫也具有完全免費的強大優勢。

不過，您可能需要為您的網站建立完全獨特的設計。 在這種情況下，與網站設計公司合作是合理的。 我決定採用這種方法來設計 Contact Manager 應用程式。

我從反復專案 #1 中壓縮了連絡人管理員，並將專案傳送給設計公司。 它們並未擁有 Visual Studio （太可惜！），但不會有問題。 他們可以從[https://www.asp.net](https://www.asp.net)網站免費下載 Microsoft Visual Web Developer，並在 Visual Web Developer 中開啟 Contact Manager 應用程式。 在幾天內，他們在 [圖 7] 中產生了設計。

[![[新增專案] 對話方塊](iteration-2-make-the-application-look-nice-cs/_static/image7.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image13.png)

**圖 07**： ASP.NET MVC Contact Manager 設計（[按一下以觀看完整大小的影像](iteration-2-make-the-application-look-nice-cs/_static/image14.png)）

新的設計是由兩個主要的檔案所組成：新的級聯樣式表檔案和新的視圖主版分頁檔。 視圖主版頁面包含 ASP.NET MVC 應用程式中 views 的版面配置和共用內容。 例如，[視圖主版] 頁面包含 [圖 7] 中顯示的標題、導覽索引標籤和頁尾。 我已在 Views\Shared 資料夾中，使用來自設計公司的新網站檔案來覆蓋現有的網站。主視圖主版頁面，

設計公司也會建立新的級聯樣式表和一組影像。 我將這些新檔案放在 Content 資料夾中，並將現有的網站 .css 檔案加以覆蓋。 您應該將所有靜態內容放在 Content 資料夾中。

請注意，連絡人管理員的新設計包含編輯和刪除連絡人的影像。 [編輯] 和 [刪除] 影像會出現在連絡人的 HTML 表格中的每個連絡人旁邊。

原本，這些連結是以 HTML 轉譯。Html.actionlink （） helper，如下所示：

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample1.aspx)]

.Html （）方法不支援影像（基於安全性理由，方法 HTML 會針對連結文字進行編碼）。 因此，我將對 Html.actionlink （）的呼叫取代為對 Url 的呼叫（），如下所示：

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample2.aspx)]

.Html （）方法會呈現整個 HTML 超連結。 另一方面，Url. Action （）方法只會轉譯 URL，而不會 &lt;&gt; 標記。

另外，請注意，新的設計同時包含選取和未選取的索引標籤。 例如，在 [圖 8] 中，已選取 [**建立新的連絡人**] 索引標籤，而且未選取 [**我的連絡人**] 索引標籤。

[![[新增專案] 對話方塊](iteration-2-make-the-application-look-nice-cs/_static/image8.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image15.png)

**圖 08**：選取和未選取的索引標籤（[按一下以查看完整大小的影像](iteration-2-make-the-application-look-nice-cs/_static/image16.png)）

為了支援同時呈現選取和未選取的索引標籤，我建立了一個名為 MenuItemHelper 的自訂 HTML helper。 此 helper 方法會根據目前的控制器和動作是否對應至傳遞給協助程式的控制器和動作名稱，轉譯 &lt;li&gt; 標記或 &lt;li 類別 = "selected"&gt; 標記。 MenuItemHelper 的程式碼包含在 [清單 1] 中。

**清單 1-Helpers\MenuItemHelper.cs**

[!code-csharp[Main](iteration-2-make-the-application-look-nice-cs/samples/sample3.cs)]

MenuItemHelper 會在內部使用 TagBuilder 類別來建立 &lt;li&gt; HTML 標籤。 TagBuilder 類別是非常有用的公用程式類別，您可以在需要建立新的 HTML 標籤時使用。 其中包括新增屬性、新增 CSS 類別、產生識別碼，以及修改標記的內部 HTML 的方法。

## <a name="summary"></a>總結

在此反復專案中，我們改善了 ASP.NET MVC 應用程式的視覺化設計。 首先，您已引進 ASP.NET MVC 設計資源庫。 您已瞭解如何從可在 ASP.NET MVC 應用程式中使用的 ASP.NET MVC 設計資源庫下載免費的設計範本。

接下來，我們討論了如何藉由修改預設的級聯樣式表檔案和主版視圖分頁檔來建立自訂設計。 為了支援新的設計，我們必須對我們的「連絡人管理員」應用程式進行一些微小的變更。 例如，我們新增了名為 MenuItemHelper 的新 HTML 協助程式，以顯示選取和取消選取的索引標籤。

在下一個反復專案中，我們會處理驗證的重要主題。 我們會將驗證程式代碼新增至應用程式，如此一來，使用者就無法建立新的連絡人，而不需要提供必要的值，例如個人姓氏和名字。

> [!div class="step-by-step"]
> [上一頁](iteration-1-create-the-application-cs.md)
> [下一頁](iteration-3-add-form-validation-cs.md)
