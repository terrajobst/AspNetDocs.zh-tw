---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
title: Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第8部分 |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 來建立 ASP.NET Web Forms 應用程式。 範例應用程式為 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: aaadd9bb-5508-448c-ad57-5497dff90e13
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
msc.type: authoredcontent
ms.openlocfilehash: ff6a808dd501df8056c0fb0784a8e42e094d5db7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78585908"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-8"></a>Entity Framework 4.0 Database First 和 ASP.NET 4 Web form 的消費者入門-第8部分

由[Tom 作者: dykstra](https://github.com/tdykstra)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 4.0 和 Visual Studio 2010 來建立 ASP.NET Web Forms 應用程式。 如需教學課程系列的資訊，請參閱本[系列的第一個教學](the-entity-framework-and-aspnet-getting-started-part-1.md)課程

## <a name="using-dynamic-data-functionality-to-format-and-validate-data"></a>使用動態資料功能來格式化和驗證資料

在上一個教學課程中，您已執行預存程式。 本教學課程將說明動態資料功能如何提供下列優點：

- 欄位會根據其資料類型自動格式化以顯示。
- 欄位會根據其資料類型自動進行驗證。
- 您可以將中繼資料加入至資料模型，以自訂格式設定和驗證行為。 當您這麼做時，您可以只在一個位置新增格式和驗證規則，而且它們會自動套用到您使用動態資料控制項存取欄位的任何位置。

若要查看其運作方式，您要變更用來顯示和編輯現有 student *.aspx*頁面中之欄位的控制項，然後將格式和驗證中繼資料加入 `Student` 實體類型的 [名稱] 和 [日期] 欄位中。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)

## <a name="using-dynamicfield-and-dynamiccontrol-controls"></a>使用 DynamicField 和 DynamicControl 控制項

開啟 [student *] 頁面，* 然後在 [`StudentsGridView`] 控制項中，以下列標記取代 [**名稱**] 和 [**註冊日期**] `TemplateField` 元素：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample1.aspx)]

此標記會使用 `DynamicControl` 控制項來取代 [學生名稱] 範本欄位中的 `TextBox` 和 `Label` 控制項，並使用註冊日期的 `DynamicField` 控制項。 未指定格式字串。

將 `ValidationSummary` 控制項加入 `StudentsGridView` 控制項之後。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample2.aspx)]

在 [`SearchGridView`] 控制項中，取代 [**名稱**] 和 [**註冊日期] 資料**行的標記，如同您在 `StudentsGridView` 控制項中所做的一樣，但省略 `EditItemTemplate` 元素除外。 `SearchGridView` 控制項的 `Columns` 元素現在包含下列標記：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample3.aspx)]

開啟*Students.aspx.cs* ，並新增下列 `using` 語句：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample4.cs)]

為頁面的 `Init` 事件新增處理常式：

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample5.cs)]

此程式碼會指定動態資料將在 `Student` 實體欄位的這些資料繫結控制項中提供格式設定和驗證。 如果您在執行頁面時收到類似下列範例的錯誤訊息，通常表示您忘了在 `Page_Init`中呼叫 `EnableDynamicData` 方法：

`Could not determine a MetaTable. A MetaTable could not be determined for the data source 'StudentsEntityDataSource' and one could not be inferred from the request URL.`

執行頁面。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)

在 [**註冊日期] 資料**行中，時間會隨著日期顯示，因為屬性類型是 `DateTime`。 您稍後將會修正此問題。

現在請注意，動態資料會自動提供基本的資料驗證。 例如，按一下 [**編輯**]，清除 [日期] 欄位，按一下 [**更新**]，您會看到動態資料自動將此設為必要欄位，因為資料模型中的值不可為 null。 此頁面會在欄位之後顯示星號，並在 `ValidationSummary` 控制項中顯示錯誤訊息：

[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)

您可能會省略 `ValidationSummary` 控制項，因為您也可以將滑鼠指標放在星號上方，以查看錯誤訊息：

[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)

動態資料也會驗證在 [**註冊日期**] 欄位中輸入的資料是有效的日期：

[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)

如您所見，這是一般錯誤訊息。 在下一節中，您將瞭解如何自訂訊息，以及驗證和格式化規則。

## <a name="adding-metadata-to-the-data-model"></a>將中繼資料加入至資料模型

一般來說，您會想要自訂動態資料所提供的功能。 例如，您可能會變更資料的顯示方式，以及錯誤訊息的內容。 您通常也會自訂資料驗證規則，以提供比動態資料根據資料類型自動提供更多功能的功能。 若要這樣做，您可以建立對應至實體類型的部分類別。

在**方案總管**中，以滑鼠右鍵按一下**ContosoUniversity**專案，選取 [**新增參考**]，然後加入 `System.ComponentModel.DataAnnotations`的參考。

[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)

在*DAL*資料夾中，建立新的類別檔案，將其命名為*Student.cs*，並將其中的範本程式碼取代為下列程式碼。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample6.cs)]

此程式碼會建立 `Student` 實體的部分類別。 套用至這個部分類別的 `MetadataType` 屬性會識別您用來指定中繼資料的類別。 中繼資料類別可以有任何名稱，但使用機構名稱加上「中繼資料」是常見的作法。

套用至中繼資料類別中屬性的屬性會指定格式、驗證、規則和錯誤訊息。 此處顯示的屬性會有下列結果：

- `EnrollmentDate` 會顯示為日期（不含時間）。
- 這兩個名稱欄位的長度必須少於25個字元，而且提供了自訂的錯誤訊息。
- 這兩個名稱欄位都是必要項，並提供自訂錯誤訊息。

再次執行 [student *.aspx* ] 頁面，您會看到現在顯示的日期沒有時間：

[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)

編輯資料列，並嘗試清除 [名稱] 欄位中的值。 當您離開欄位時，表示欄位錯誤的星號會立即出現，然後再按一下 [**更新**]。 當您按一下 [**更新**] 時，頁面會顯示您指定的錯誤訊息正文。

[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)

請嘗試輸入超過25個字元的名稱，按一下 [**更新**]，頁面就會顯示您指定的錯誤訊息正文。

[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)

既然您已在資料模型中繼資料中設定這些格式和驗證規則，這些規則會自動套用到顯示或允許變更這些欄位的每個頁面，只要您使用 `DynamicControl` 或 `DynamicField` 控制項即可。 這可減少您必須撰寫的多餘程式碼數量，讓程式設計和測試變得更容易，並確保資料格式和驗證在整個應用程式中都是一致的。

## <a name="more-information"></a>詳細資訊

這會在與 Entity Framework 消費者入門的這一系列教學課程結束。 如需可協助您瞭解如何使用 Entity Framework 的更多資源，請繼續進行[下一個 Entity Framework 教學課程系列中的第一個教學](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)課程，或造訪下列網站：

- [Entity Framework 常見問題](http://www.ef-faq.org/introduction.html)
- [Entity Framework 小組的 Blog](https://blogs.msdn.com/b/adonet/)
- [MSDN Library 中的 Entity Framework](https://msdn.microsoft.com/library/bb399572.aspx)
- [MSDN 資料開發人員中心內的 Entity Framework](https://msdn.microsoft.com/data/ef.aspx)
- [MSDN Library 中的 EntityDataSource Web 服務器控制項總覽](https://msdn.microsoft.com/library/cc488502.aspx)
- [MSDN Library 中的 EntityDataSource 控制項 API 參考](https://msdn.microsoft.com/library/system.web.ui.webcontrols.entitydatasource.aspx)
- [MSDN 上的 Entity Framework 論壇](https://social.msdn.microsoft.com/forums/adodotnetentityframework/)
- [Julie Lerman 的 blog](http://thedatafarm.com/blog/)

> [!div class="step-by-step"]
> [上一篇](the-entity-framework-and-aspnet-getting-started-part-7.md)
