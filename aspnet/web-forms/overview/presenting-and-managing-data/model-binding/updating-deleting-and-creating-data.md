---
uid: web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
title: 使用模型系結和 web forms 來更新、刪除和建立資料 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。 模型系結讓資料互動更為直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 602baa94-5a4f-46eb-a717-7a9e539c1db4
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
msc.type: authoredcontent
ms.openlocfilehash: 11dc52ec79ca91119b37ea60e08164eb1b1d0e2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586643"
---
# <a name="updating-deleting-and-creating-data-with-model-binding-and-web-forms"></a>使用模型系結和 web forms 來更新、刪除及建立資料

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。 模型系結可讓資料互動比處理資料來源物件（例如 ObjectDataSource 或 SqlDataSource）更直接。 此系列從簡介材料開始，並在稍後的教學課程中移至更先進的概念。
> 
> 本教學課程說明如何使用模型系結來建立、更新和刪除資料。 您將設定下列屬性：
> 
> - DeleteMethod
> - InsertMethod
> - UpdateMethod
> 
> 這些屬性會接收處理對應作業的方法名稱。 在該方法中，您會提供與資料互動的邏輯。
> 
> 本教學課程是以系列第一個[部分](retrieving-data.md)中所建立的專案為基礎。
> 
> 您可以在或 VB 中 C# [下載](https://go.microsoft.com/fwlink/?LinkId=286116)完整專案。 可下載的程式碼適用于 Visual Studio 2012 或 Visual Studio 2013。 它會使用 Visual Studio 2012 範本，這與本教學課程中所顯示的 Visual Studio 2013 範本稍有不同。

## <a name="what-youll-build"></a>您將建立的內容

在本教學課程中，您將會：

1. 新增動態資料範本
2. 啟用透過模型系結方法來更新和刪除資料
3. 套用資料驗證規則-啟用在資料庫中建立新記錄

## <a name="add-dynamic-data-templates"></a>新增動態資料範本

為了提供最佳的使用者體驗，並將程式碼重複最小化，您將使用動態資料範本。 您可以藉由安裝 NuGet 套件，輕鬆地將預先建立的動態資料範本整合到您現有的網站。

在 [**管理 NuGet 套件**] 中，安裝**DynamicDataTemplatesCS**。

![動態資料範本](updating-deleting-and-creating-data/_static/image1.png)

請注意，您的專案現在包含名為**DynamicData**的資料夾。 在該資料夾中，您會找到自動套用至 web 表單中動態控制項的範本。

![動態資料資料夾](updating-deleting-and-creating-data/_static/image2.png)

## <a name="enable-updating-and-deleting"></a>啟用更新和刪除

讓使用者可以更新和刪除資料庫中的記錄，與抓取資料的程式非常類似。 在 [ **UpdateMethod** ] 和 [ **DeleteMethod** ] 屬性中，您可以指定執行這些作業的方法名稱。 有了 GridView 控制項，您也可以指定自動產生 [編輯] 和 [刪除] 按鈕。 下列反白顯示的程式碼會顯示 GridView 程式碼的新增專案。

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample1.aspx?highlight=4-5)]

在程式碼後置檔案中，為**system.object**新增 using 語句。

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample2.cs)]

然後，新增下列 update 和 delete 方法。

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample3.cs)]

**TryUpdateModel**方法會將相符的資料系結值從 web 表單套用至資料項目。 資料項目目是根據 id 參數的值來抓取。

## <a name="enforce-validation-requirements"></a>強制執行驗證需求

更新資料時，會自動強制執行您套用至 Student 類別中 FirstName、LastName 和 Year 屬性的驗證屬性。 DynamicField 控制項會根據驗證屬性來新增用戶端和伺服器驗證程式。 FirstName 和 LastName 屬性都是必要的。 FirstName 長度不能超過20個字元，而且 LastName 不能超過40個字元。 Year 必須是有效的 AcademicYear 列舉值。

如果使用者違反其中一項驗證需求，就不會繼續更新。 若要查看錯誤訊息，請在 GridView 上方加入 ValidationSummary 控制項。 若要顯示模型系結的驗證錯誤，請將**ShowModelStateErrors**屬性設定為**true**。 

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample4.aspx)]

執行 web 應用程式，並更新和刪除任何記錄。

![更新資料](updating-deleting-and-creating-data/_static/image3.png)

請注意，在編輯模式中，Year 屬性的值會自動轉譯為下拉式清單。 Year 屬性是一個列舉值，而列舉值的動態資料範本會指定一個下拉式清單來進行編輯。 您可以藉由開啟列舉\_在**DynamicData**/**FieldTemplates**資料夾中**編輯 .ascx**檔案，找到該範本。

如果您提供有效的值，則更新會順利完成。 如果您違反其中一項驗證需求，則不會繼續更新，而且格線上方會顯示錯誤訊息。

![錯誤訊息](updating-deleting-and-creating-data/_static/image4.png)

## <a name="add-new-records"></a>加入新記錄

GridView 控制項不包含**InsertMethod**屬性，因此無法用來加入具有模型系結的新記錄。 您可以在 [ **FormView**]、[ **DetailsView**] 或 [ **ListView** ] 控制項中找到 InsertMethod 屬性。 在本教學課程中，您將使用 FormView 控制項來加入新的記錄。

首先，將連結新增至您將建立以加入新記錄的新頁面。 在 ValidationSummary 上方，新增：

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample5.aspx)]

新的連結將會出現在 [學生] 頁面內容的頂端。

![新增連結](updating-deleting-and-creating-data/_static/image5.png)

然後，使用主版頁面新增新的 web 表單，並將其命名為**AddStudent**。 選取 [網站] 作為主版頁面。

您將會使用**DynamicEntity**控制項來轉譯加入新學生的欄位。 DynamicEntity 控制項會在 ItemType 屬性中所指定的類別中轉譯該可編輯的屬性。 StudentID 屬性是以 **[ScaffoldColumn （false）]** 屬性標記，因此不會呈現。 在 [AddStudent] 頁面的 [MainContent] 預留位置中，加入下列程式碼。

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample6.aspx)]

在程式碼後置檔案（AddStudent.aspx.cs）中，為**ContosoUniversityModelBinding**命名空間加入**using**語句。

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample7.cs)]

然後，新增下列方法，以指定如何插入新的記錄和 [取消] 按鈕的事件處理常式。

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample8.cs)]

儲存所有變更。

執行 web 應用程式，並建立新的學生。

![新增學生](updating-deleting-and-creating-data/_static/image6.png)

按一下 [**插入**]，並注意新的 student 已建立。

![顯示新 student](updating-deleting-and-creating-data/_static/image7.png)

## <a name="conclusion"></a>結論

在本教學課程中，您已啟用更新、刪除及建立資料的功能。 當您與資料互動時，會套用驗證規則。

在此系列的下一個[教學](sorting-paging-and-filtering-data.md)課程中，您將啟用排序、分頁及篩選資料。

> [!div class="step-by-step"]
> [上一頁](retrieving-data.md)
> [下一頁](sorting-paging-and-filtering-data.md)
