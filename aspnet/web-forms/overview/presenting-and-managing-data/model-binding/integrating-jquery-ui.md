---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: 整合 JQuery UI Datepicker 與模型系結和 web forms |Microsoft Docs
author: Rick-Anderson
description: 本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。 模型系結讓資料互動更為直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: c8d711dd44950116f3a3e09d5d12c507918c543f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78642475"
---
# <a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a>整合 JQuery UI Datepicker 與模型系結和 web 表單

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。 模型系結可讓資料互動比處理資料來源物件（例如 ObjectDataSource 或 SqlDataSource）更直接。 此系列從簡介材料開始，並在稍後的教學課程中移至更先進的概念。
> 
> 本教學課程示範如何將 JQuery UI [Datepicker widget](http://jqueryui.com/datepicker/)新增至 Web 表單，並使用模型系結以選取的值來更新資料庫。
> 
> 本教學課程是以數列的[第一個](retrieving-data.md)和[第二個](updating-deleting-and-creating-data.md)部分中所建立的專案為基礎。
> 
> 您可以[download](https://go.microsoft.com/fwlink/?LinkId=286116)在或 VB 中C#下載完整專案。 可下載的程式碼適用于 Visual Studio 2012 或 Visual Studio 2013。 它會使用 Visual Studio 2012 範本，這與本教學課程中所顯示的 Visual Studio 2013 範本稍有不同。

## <a name="what-youll-build"></a>您將建立的內容

在本教學課程中，您將會：

1. 將屬性新增至您的模型，以記錄學生的註冊日期
2. 讓使用者可以使用 JQuery UI Datepicker widget 來選取註冊日期
3. 強制執行註冊日期的驗證規則

JQuery UI Datepicker 小工具可讓使用者在使用者與欄位互動時，輕鬆地從行事曆選取日期。 對於使用者而言，使用這個小工具會比手動輸入日期更方便。 將 Datepicker widget 整合到使用模型系結來進行資料作業的頁面，只需要少量的額外工作。

## <a name="add-a-new-property-to-the-model"></a>將新屬性新增至模型

首先，您會將**日期時間**屬性加入至您的學生模型，並將該變更遷移至資料庫。 開啟**UniversityModels.cs**，並將反白顯示的程式碼新增至學生模型。

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

包含**RangeAttribute**是為了強制執行屬性的驗證規則。 在本教學課程中，我們會假設 Contoso 大學是在2013年1月1日成立，因此較早的註冊日期是不正確。

在 [套件管理] 視窗中，執行 [**新增-遷移 AddEnrollmentDate**] 命令來新增遷移。 請注意，遷移程式碼會將新的日期時間資料行加入至 Student 資料表。 若要符合您在 RangeAttribute 中指定的值，請為新的資料行加入預設值，如下列反白顯示的程式碼所示。

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

將您的變更儲存至遷移檔案。

您不需要再次植入資料。 因此，請在 [遷移] 資料夾中開啟**Configuration.cs** ，並移除或批註**植入種子**方法中的程式碼。 儲存並關閉檔案。

現在，請執行命令**update-database**。 請注意，資料行現在存在於資料庫中，而且所有現有的記錄都有 EnrollmentDate 的預設值。

## <a name="add-dynamic-controls-for-enrollment-date"></a>新增註冊日期的動態控制項

您現在會加入控制項，以顯示和編輯註冊日期。 此時，值會透過文字方塊進行編輯。 稍後在本教學課程中，您會將文字方塊變更為 JQuery Datepicker widget。

首先，請務必注意，您不需要對**AddStudent .aspx**檔案進行任何變更。 DynamicEntity 控制項會自動轉譯新的屬性。

開啟 **[** student]，並新增下列反白顯示的程式碼。

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

執行應用程式，並注意您可以輸入日期來設定註冊日期的值。 加入新的學生時：

![設定日期](integrating-jquery-ui/_static/image1.png)

或者，編輯現有的值：

![編輯日期](integrating-jquery-ui/_static/image2.png)

輸入日期可以運作，但可能不是您想要提供的客戶體驗。 在下一節中，您將會啟用透過行事曆選取日期。

## <a name="install-nuget-package-to-work-with-jquery-ui"></a>安裝 NuGet 套件以使用 JQuery UI

**JUICE UI** NuGet 套件可讓 JQuery UI widget 輕鬆地整合到您的 web 應用程式中。 若要使用此套件，請透過 NuGet 進行安裝。

![新增 Juice UI](integrating-jquery-ui/_static/image3.png)

您安裝的 Juice UI 版本可能會與應用程式中的 JQuery 版本衝突。 繼續進行本教學課程之前，請先試著執行您的應用程式。 如果您遇到 JavaScript 錯誤，您需要協調 JQuery 版本。 您可以在腳本資料夾中加入預期的 JQuery 版本（在撰寫本教學課程時的版本1.8.2），或在 [網站] 中，指定 JQuery 檔案的路徑。

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a>自訂日期時間範本以包含 Datepicker widget

您會將 Datepicker widget 新增至動態資料範本，以編輯日期時間值。 藉由將 widget 新增至範本，它會自動以用於新增學生的表單，以及在編輯學生的方格視圖中轉譯。 開啟**DateTime\_編輯 .ascx**，並新增下列反白顯示的程式碼。

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

在程式碼後置檔案中，您會設定 DatePicker 的最小和最大日期。 藉由設定這些值，您將可防止使用者流覽至不正確日期。 您將會從日期時間屬性的**RangeAttribute**中取得最小和最大值（如果有提供的話）。 開啟**DateTime\_Edit.ascx.cs**，並將下列反白顯示的程式碼新增至頁面\_載入方法。

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

執行 web 應用程式，並流覽至 [AddStudent] 頁面。 提供欄位的值，並注意當您按一下 [註冊日期] 文字方塊時，會顯示行事曆。

![日期選擇器](integrating-jquery-ui/_static/image4.png)

挑選日期，然後按一下 [**插入**]。 RangeAttribute 會在伺服器上強制執行驗證。 藉由在 Datepicker 上設定 minDate 屬性，您也可以在用戶端上套用驗證。 行事曆不會讓使用者流覽至 minDate 值之前的日期。

當您編輯方格視圖中的記錄時，也會顯示行事曆。

![GridView 中的 Datepicker](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a>結論

在本教學課程中，您已瞭解如何將 JQuery widget 併入使用模型系結的 web 表單。

在下一個[教學](using-query-string-values-to-retrieve-data.md)課程中，您將會在選取資料時使用查詢字串值。

> [!div class="step-by-step"]
> [上一頁](sorting-paging-and-filtering-data.md)
> [下一頁](using-query-string-values-to-retrieve-data.md)
