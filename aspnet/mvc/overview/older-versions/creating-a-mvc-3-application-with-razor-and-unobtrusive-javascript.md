---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: 使用 Razor 和不顯眼的 JavaScript 建立 MVC 3 應用程式 |Microsoft Docs
author: microsoft
description: 使用者清單範例 web 應用程式示範使用 Razor view 引擎建立 ASP.NET MVC 3 應用程式有多麼簡單。 範例應用程式 。
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: fb63493ff22c9261fc5746a998a32f2511141f87
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540982"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a>使用 Razor 和低調的 JavaScript 建立 MVC 3 應用程式

由[Microsoft](https://github.com/microsoft)

> 使用者清單範例 web 應用程式示範使用 Razor view 引擎建立 ASP.NET MVC 3 應用程式有多麼簡單。 範例應用程式示範如何使用新的 Razor view 引擎搭配 ASP.NET MVC 第3版和 Visual Studio 2010 來建立虛構的使用者清單網站，其中包含建立、顯示、編輯和刪除使用者等功能。
> 
> 本教學課程說明建立 MVC 3 應用程式的使用者清單範例時，所採取的步驟。 本主題提供具有C#和 VB 原始程式碼的 Visual Studio 專案：[下載](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)。 如果您對本教學課程有任何疑問，請將其張貼至[MVC 論壇](https://forums.asp.net/1146.aspx)。

## <a name="overview"></a>概觀

您將建立的應用程式是簡單的使用者清單網站。 使用者可以輸入、查看及更新使用者資訊。

![範例網站](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

您可以在[這裡](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)下載 VB C#和已完成的專案。

## <a name="creating-the-web-application"></a>建立 Web 應用程式

若要開始本教學課程，請開啟 Visual Studio 2010，並使用*ASP.NET MVC 3 Web 應用程式*範本建立新的專案。 將應用程式命名為 &quot;Mvc3Razor&quot;。

[![新的 MVC 3 專案](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)

在 [**新增 ASP.NET MVC 3 專案**] 對話方塊中，選取 [**網際網路應用程式**]，選取 [Razor 視圖引擎]，然後按一下 **[確定]** 。

![[新增 ASP.NET MVC 3 專案] 對話方塊](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

在本教學課程中，您將不會使用 ASP.NET 成員資格提供者，因此您可以刪除與登入和成員資格相關聯的所有檔案。 在**方案總管**中，移除下列檔案和目錄：

- *Controllers\AccountController*
- *Models\AccountModels*
- *Views\Shared\\_LogOnPartial*
- *Views\Account* （以及此目錄中的所有檔案）

![Soln Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

編輯\_的配置<em>cshtml</em>檔案，並將名為 `logindisplay` 的 `<div>` 元素內的標記取代為停用&quot;的 [登入] <em>&quot;</em>訊息。 下列範例會顯示新的標記：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a>加入模型

在**方案總管**中，以滑鼠右鍵按一下 [*模型*] 資料夾，選取 [**新增**]，然後按一下 [**類別**]。

![新增使用者 Mdl 類別](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

將類別命名為 `UserModel`。 使用下列程式碼取代*UserModel*檔案的內容：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

`UserModel` 類別代表使用者。 類別的每個成員都會使用[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間中的[必要](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)屬性來標注。 [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間中的屬性會為 web 應用程式提供自動用戶端和伺服器端驗證。

開啟 `HomeController` 類別並加入 `using` 指示詞，讓您可以存取 `UserModel` 和 `Users` 類別：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

在 `HomeController` 宣告之後，將下列批註和參考新增至 `Users` 類別：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

`Users` 類別是簡化的記憶體內部資料存放區，您將在本教學課程中使用。 在實際的應用程式中，您會使用資料庫來儲存使用者資訊。 在下列範例中，會顯示 `HomeController` 檔案的前幾行：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

建立應用程式，以便在下一個步驟中將使用者模型提供給 [樣板]。

## <a name="creating-the-default-view"></a>建立預設的視圖

下一個步驟是新增動作方法和 view 來顯示使用者。

刪除現有的*Views\Home\Index*檔案。 您將建立新的*索引*檔案來顯示使用者。

在 `HomeController` 類別中，將 `Index` 方法的內容取代為下列程式碼：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

在 `Index` 方法內按一下滑鼠右鍵，然後按一下 [**加入視圖**]。

![加入視圖](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

選取 [**建立強型別視圖**] 選項。 針對**View data class**，選取**Mvc3Razor UserModel**。 （如果您在 [ **View data class** ] 方塊中看不到 [ **Mvc3Razor** ]，則必須建立專案）。請確定 [view engine] 已設定為 [ **Razor**]。 將 [**視圖內容**] 設定為 [**清單**]，然後按一下 [**新增**]。

![新增索引視圖](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

新的視圖會自動 scaffold 傳遞至 `Index` 視圖的使用者資料。 檢查新產生的*Views\Home\Index*檔案。 [**建立新**的]、[**編輯**]、[**詳細資料**] 和 [**刪除**] 連結無法運作，但頁面的其餘部分則會正常運作。 執行頁面。 您會看到使用者清單。

![[索引] 頁面](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

開啟*Index. cshtml*檔案，並以下列程式碼取代 **[編輯**]、[**詳細資料**] 和 [**刪除**] 的 `ActionLink` 標記：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

使用者名稱會用來作為識別碼，以在 [**編輯**]、[**詳細資料**] 和 [**刪除**] 連結中尋找選取的記錄。

## <a name="creating-the-details-view"></a>建立詳細資料檢視

下一個步驟是新增 `Details` 動作方法和 view，以便顯示使用者詳細資料。

![詳細資料](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

將下列 `Details` 方法加入至主控制器：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

在 `Details` 方法內按一下滑鼠右鍵，然後選取 [<strong>新增視圖</strong>]。 確認 [ <strong>View data class</strong> ] 方塊包含<strong>Mvc3Razor。 UserModel</strong><em>。</em> 將 [<strong>查看內容</strong>] 設定為<strong>詳細資料</strong>，然後按一下 [<strong>新增</strong>]。

![新增詳細資料檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

執行應用程式並選取 [詳細資料] 連結。 自動的範例會顯示模型中的每個屬性。

![詳細資料](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a>建立編輯檢視

將下列 `Edit` 方法新增至 home 控制器。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

如先前的步驟所示新增視圖，但將 [ **view content** ] 設定為 [**編輯**]。

![新增編輯檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

執行應用程式，並編輯其中一個使用者的姓氏和名字。 如果您違反任何已套用至 `UserModel` 類別的 `DataAnnotation` 條件約束，當您提交表單時，您會看到伺服器程式碼所產生的驗證錯誤。 例如，如果您將第一個名稱 &quot;王&quot; 以 &quot;&quot;，則在提交表單時，表單上會顯示下列錯誤：

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

在本教學課程中，您會將使用者名稱視為主要金鑰。 因此，無法變更 [使用者名稱] 屬性。 在*編輯的 cshtml*檔案中，緊接在 `Html.BeginForm` 語句之後，將使用者名稱設定為隱藏欄位。 這會導致屬性在模型中傳遞。 下列程式碼片段顯示 `Hidden` 語句的位置：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

使用 `DisplayFor` 呼叫來取代使用者名稱的 `TextBoxFor` 和 `ValidationMessageFor` 標記。 `DisplayFor` 方法會將屬性顯示為唯讀元素。 下列範例顯示完整的標記。 原始的 `TextBoxFor` 和 `ValidationMessageFor` 呼叫會使用 Razor 開始-批註和結束批註字元（`@* *@`）進行批註化

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a>啟用用戶端驗證

若要在 ASP.NET MVC 3 中啟用用戶端驗證，您必須設定兩個旗標，而且必須包含三個 JavaScript 檔案。

開啟應用程式的*web.config*檔案。 確認 應用程式設定 中的 `that ClientValidationEnabled` 和 `UnobtrusiveJavaScriptEnabled` 設定為 true。 根*web.config*檔案中的下列片段會顯示正確的設定：

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

將 `UnobtrusiveJavaScriptEnabled` 設定為 true 可啟用不顯眼的 Ajax 和不顯眼的用戶端驗證。 當您使用不顯眼的驗證時，驗證規則會變成 HTML5 屬性。 HTML5 屬性名稱只能包含小寫字母、數位和虛線。

將 `ClientValidationEnabled` 設定為 true 會啟用用戶端驗證。 藉由*在應用程式的 web.config 檔案*中設定這些索引鍵，您可以針對整個應用程式啟用用戶端驗證和不顯眼的 JavaScript。 您也可以使用下列程式碼，在個別的 views 或控制器方法中啟用或停用這些設定：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

您也需要在呈現的視圖中包含數個 JavaScript 檔案。 在所有視圖中包含 JavaScript 的簡單方法，就是將它們新增至*Views\Shared\\_Layout. cshtml*檔案。 以下列程式碼取代 *\_Layout*檔案的 `<head>` 元素：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

前兩個 jQuery 腳本是由 Microsoft Ajax 內容傳遞網路（CDN）所主控。 藉由利用 Microsoft Ajax CDN，您可以大幅提升應用程式的第一次點擊效能。

執行應用程式，然後按一下 [編輯] 連結。 在瀏覽器中查看頁面的來源。 瀏覽器來源會顯示多個表單 `data-val` 的屬性（用於資料驗證）。 當啟用用戶端驗證和不顯眼的 JavaScript 時，具有用戶端驗證規則的輸入欄位會包含 `data-val="true"` 屬性，以觸發不顯眼的用戶端驗證。 例如，模型中的 [`City`] 欄位是以[必要](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)的屬性裝飾，這會導致 HTML 顯示在下列範例中：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

針對每個用戶端驗證規則，會加入具有 `data-val-rulename="message"`格式的屬性。 使用稍早所示的 `City` 欄位範例時，必要的用戶端驗證規則會產生 `data-val-required` 屬性和訊息 &quot;[City] 欄位必須&quot;。 執行應用程式、編輯其中一個使用者，然後清除 [`City`] 欄位。 當您按 tab 鍵移出欄位時，您會看到用戶端驗證錯誤訊息。

![需要城市](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

同樣地，針對用戶端驗證規則中的每個參數，會加入具有 `data-val-rulename-paramname=paramvalue`格式的屬性。 例如，`FirstName` 屬性會加上[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)屬性的批註，並指定最小長度3，最大長度為8。 名為 `length` 的資料驗證規則具有參數名稱 `max` 和參數值8。 以下顯示當您編輯其中一個使用者時，為 [`FirstName`] 欄位產生的 HTML：

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

如需不顯眼的用戶端驗證的詳細資訊，請參閱 Brad Wilson 的 blog 中的 ASP.NET MVC 3 中的「不[顯眼的用戶端驗證](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)」專案。

> [!NOTE]
> 在 ASP.NET MVC 3 Beta 中，您有時需要提交表單，才能啟動用戶端驗證。 這可能會在最終版本中變更。

## <a name="creating-the-create-view"></a>建立建立視圖

下一個步驟是新增 `Create` 動作方法和 view，讓使用者能夠建立新的使用者。 將下列 `Create` 方法加入至主控制器：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

如先前的步驟所示新增視圖，但將**view content**設定為 **[建立]。**

![建立檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

執行應用程式，選取 [**建立**] 連結，然後新增新的使用者。 `Create` 方法會自動利用用戶端和伺服器端驗證。 請嘗試輸入包含空白字元的使用者名稱，例如 &quot;Ben X&quot;。 當您使用 tab 鍵移出 [使用者名稱] 欄位時，就會顯示用戶端驗證錯誤（`White space is not allowed`）。

## <a name="add-the-delete-method"></a>新增 Delete 方法

若要完成本教學課程，請將下列 `Delete` 方法加入至主控制器：

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

新增 [`Delete`] 視圖，如同先前的步驟，將 [ **view content** ] 設定為 [**刪除**]。

![刪除檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

您現在有一個簡單但功能完整的 ASP.NET MVC 3 應用程式，具有驗證。
