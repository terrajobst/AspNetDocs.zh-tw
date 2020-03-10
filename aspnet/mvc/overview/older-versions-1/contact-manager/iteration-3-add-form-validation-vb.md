---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
title: '反復專案 #3 –新增表單驗證（VB） |Microsoft Docs'
author: microsoft
description: 在第三個反復專案中，我們會新增基本表單驗證。 我們會防止人們提交表單，而不需要完成必要的表單欄位。 我們也會驗證 emai 。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 4805e75a-7911-46e3-b11b-229a6eed245e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 73b307f53875abe84b592c75b1ff614ffd9d8b82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544447"
---
# <a name="iteration-3--add-form-validation-vb"></a>反復專案 #3 –新增表單驗證（VB）

由[Microsoft](https://github.com/microsoft)

[下載程式代碼](iteration-3-add-form-validation-vb/_static/contactmanager_3_vb1.zip)

> 在第三個反復專案中，我們會新增基本表單驗證。 我們會防止人們提交表單，而不需要完成必要的表單欄位。 我們也會驗證電子郵件地址和電話號碼。

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

在 Contact Manager 應用程式的第二個反復專案中，我們新增了基本表單驗證。 我們會防止人們提交連絡人，而不需要輸入必要表單欄位的值。 我們也會驗證電話號碼和電子郵件地址（請參閱 [圖 1]）。

[![[新增專案] 對話方塊](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)

**圖 01**：具有驗證的表單（[按一下以觀看完整大小的影像](iteration-3-add-form-validation-vb/_static/image2.png)）

在此反復專案中，我們會將驗證邏輯直接新增至控制器動作。 一般來說，這不是將驗證新增至 ASP.NET MVC 應用程式的建議方式。 較好的方法是將應用程式的驗證邏輯放在不同的[服務層](http://martinfowler.com/eaaCatalog/serviceLayer.html)中。 在下一個反復專案中，我們會重構 Contact Manager 應用程式，讓應用程式更容易維護。

在此反復專案中，為了簡單起見，我們會以手動方式撰寫所有驗證程式代碼。 我們不會自行撰寫驗證程式代碼，而是可以利用驗證架構。 例如，您可以使用 Microsoft 企業程式庫驗證應用程式區塊（VAB）來執行 ASP.NET MVC 應用程式的驗證邏輯。 若要深入瞭解驗證應用程式區塊，請參閱：

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a>將驗證新增至建立視圖

首先，讓我們先將驗證邏輯加入至 Create view。 幸運的是，因為我們產生了具有 Visual Studio 的 Create view，所以 Create view 已經包含所有必要的使用者介面邏輯來顯示驗證訊息。 [建立] 視圖包含在 [清單 1] 中。

**清單 1-\Views\Contact\Create.aspx**

[!code-aspx[Main](iteration-3-add-form-validation-vb/samples/sample1.aspx)]

欄位驗證-error 類別是用來將 ValidationMessage （） helper 所呈現的輸出樣式。 輸入驗證-error 類別是用來為 Html. TextBox （） helper 所轉譯的 textbox （輸入）樣式。 [驗證-摘要-錯誤] 類別是用來將 ValidationSummary （） helper 所呈現的未排序清單樣式。

> [!NOTE] 
> 
> 您可以修改本節所述的樣式表單類別，以自訂驗證錯誤訊息的外觀。

## <a name="adding-validation-logic-to-the-create-action"></a>將驗證邏輯新增至建立動作

現在，Create view 永遠不會顯示驗證錯誤訊息，因為我們並未撰寫邏輯來產生任何訊息。 若要顯示驗證錯誤訊息，您必須將錯誤訊息新增至 ModelState。

> [!NOTE] 
> 
> 將表單欄位的值指派給屬性時，UpdateModel （）方法會自動將錯誤訊息新增至 ModelState。 例如，如果您嘗試將字串 "apple" 指派給接受 DateTime 值的生日屬性，則 UpdateModel （）方法會將錯誤新增至 ModelState。

[清單 2] 中的 [已修改的 Create （）] 方法包含新的區段，它會先驗證 Contact 類別的屬性，再將新的連絡人插入資料庫。

**清單 2-Controllers\ContactController.vb （使用驗證建立）**

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample2.vb)]

[驗證] 區段會強制執行四個不同的驗證規則：

- FirstName 屬性的長度必須大於零（而且不能只包含空格）
- LastName 屬性的長度必須大於零（而且不能只包含空格）
- 如果 Phone 屬性具有值（長度大於0），則電話屬性必須符合正則運算式。
- 如果 [電子郵件] 屬性具有值（長度大於0），則 [電子郵件] 屬性必須符合正則運算式。

當發生驗證規則違規時，會使用 AddModelError （）方法的協助，將錯誤訊息新增至 ModelState。 當您將訊息新增至 ModelState 時，您會提供屬性的名稱和驗證錯誤訊息的文字。 此錯誤訊息會顯示在 ValidationSummary （）和 ValidationMessage （） helper 方法的視圖中。

執行驗證規則之後，會檢查 ModelState 的 IsValid 屬性。 當有任何驗證錯誤訊息新增至 ModelState 時，IsValid 屬性會傳回 false。 如果驗證失敗，則會重新顯示 [建立] 表單，並顯示錯誤訊息。

> [!NOTE] 
> 
> 我從正則運算式儲存機制取得用來驗證電話號碼和電子郵件地址的正則運算式， [ *http://regexlib.com* ](http://regexlib.com)

## <a name="adding-validation-logic-to-the-edit-action"></a>將驗證邏輯加入至編輯動作

編輯（）動作會更新連絡人。 編輯（）動作必須執行與 Create （）動作完全相同的驗證。 我們應該重構 Contact controller，讓 Create （）和 Edit （）動作都呼叫相同的驗證方法，而不是複製相同的驗證程式代碼。

已修改的連絡人控制器類別包含在 [清單 3] 中。 這個類別具有新的 ValidateContact （）方法，它會在 Create （）和 Edit （）動作中同時呼叫。

**清單 3-Controllers\ContactController.vb**

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample3.vb)]

## <a name="summary"></a>總結

在此反復專案中，我們已將基本表單驗證新增至我們的 Contact Manager 應用程式。 我們的驗證邏輯會防止使用者提交新的連絡人，或編輯現有的連絡人，而不需要提供 FirstName 和 LastName 屬性的值。 此外，使用者必須提供有效的電話號碼和電子郵件地址。

在此反復專案中，我們以最簡單的方式將驗證邏輯新增至連絡人管理員應用程式。 不過，將我們的驗證邏輯混用在控制器邏輯中，將會為我們長期建立問題。 我們的應用程式會更容易維護及修改一段時間。

在下一個反復專案中，我們將會從我們的控制器重構驗證邏輯和資料庫存取邏輯。 我們將利用數個軟體設計原則，讓我們能夠建立更鬆散結合且更容易維護的應用程式。

> [!div class="step-by-step"]
> [上一頁](iteration-2-make-the-application-look-nice-vb.md)
> [下一頁](iteration-4-make-the-application-loosely-coupled-vb.md)
