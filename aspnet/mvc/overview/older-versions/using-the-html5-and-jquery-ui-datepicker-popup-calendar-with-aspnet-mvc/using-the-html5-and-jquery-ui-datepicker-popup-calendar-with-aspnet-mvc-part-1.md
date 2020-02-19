---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
title: 搭配 ASP.NET MVC 使用 HTML5 和 jQuery UI Datepicker 快顯行事曆-第1部分 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您如何在 ASP.NET MV 中使用編輯器範本、顯示範本和 jQuery UI datepicker 快顯行事曆的基本概念。
ms.author: riande
ms.date: 08/29/2011
ms.assetid: c23d27f7-b0cf-44f2-8445-fb69e045c674
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
msc.type: authoredcontent
ms.openlocfilehash: c1c2380f24c72f6aabaaacaf975e95288a384ff1
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457618"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-1"></a>搭配 ASP.NET MVC 使用 HTML5 和 jQuery UI Datepicker 快顯行事曆-第1部分

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教學課程將告訴您如何在 ASP.NET MVC Web 應用程式中使用編輯器範本、顯示範本和 jQuery UI datepicker 快顯行事曆的基本概念。

本教學課程將告訴您如何在 ASP.NET MVC Web 應用程式中使用編輯器範本、顯示範本和 jQuery [UI datepicker](http://plugins.jquery.com/project/datepicker)快顯行事曆的基本概念。 在本教學課程中，您可以使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （&quot;Visual Web Developer&quot;），這是 Microsoft Visual Studio 的免費版本，或者您也可以使用 Visual Studio 2010 SP1 （如果您已經有的話）。

開始之前，請先確定您已安裝下列必要條件。 您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，您可以使用下列連結個別安裝所需的軟體：

- [Visual Studio Web Developer Express SP1 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）

如果您使用 Visual Studio 2010，而不是 Visual Web Developer，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。

本教學課程假設您已完成[使用 mvc 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)教學課程的消費者入門，或熟悉 ASP.NET mvc 開發。 本教學課程會從[消費者入門使用 MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)教學課程中的已完成專案開始。

本教學課程會顯示C#中的程式碼。 不過，[[起始專案](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800)] 和 [已完成] 專案也會在 Visual Basic 中提供。

本主題提供具有C#和 Visual Basic 原始程式碼的 Visual Studio 專案：[下載](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800)。

### <a name="what-youll-build"></a>您要建置的內容

您將會在[使用 MVC 3 的消費者入門](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)教學課程中，將範本（具體而言，編輯和顯示範本）新增至簡單的電影清單應用程式。 您也會新增[JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/)快顯行事曆，以簡化輸入日期的程式。 下列螢幕擷取畫面顯示已修改的應用程式，其中顯示了 jQuery UI datepicker 快顯行事曆。

![完成 jQuery](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image1.png)

### <a name="skills-youll-learn"></a>您要學習的技術

以下是您要學習的內容：

- 如何使用[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間中的屬性來控制顯示的資料格式，以及其是否處於編輯模式。
- 如何建立範本（編輯和顯示範本）來控制資料的格式。
- 如何新增[JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/)做為輸入日期欄位的方式。

### <a name="getting-started"></a>開始使用

如果您還沒有來自入門專案的電影清單應用程式，請下載： 

* [下載](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。
* 在 Windows Explorer 中，以滑鼠右鍵按一下*MvcMovie .zip*檔案，然後選取 [**屬性**]。 
* 在 [ **MvcMovie 屬性**] 對話方塊中，選取 [**解除封鎖**]。 (取消封鎖後，當您嘗試使用從網路下載的 .zip 檔案時，就不會出現安全性警告。)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image2.png)

以滑鼠右鍵按一下 [ *MvcMovie* ] 檔案，然後選取 [**解壓縮全部**] 以解壓縮檔案。 在 Visual Web Developer 或 Visual Studio 2010 中，開啟*MvcMovieCS\_TU .sln*檔案。

在**方案總管**中，按兩下*Views\Shared\\_Layout* ，將其開啟。 將 `H1` 標頭從**MVC Movie 應用程式**變更為**Movie jQuery**。 按 CTRL + F5 執行應用程式，然後按一下 [**首頁**] 索引標籤，這會帶您前往電影控制器的 `Index` 方法。 若要試用應用程式，請選取其中一個電影的 [**編輯**] 連結和 [**詳細資料**] 連結。 請注意，在 [索引]、[編輯] 和 [詳細資料] 視圖中，發行日期和價格的格式正確：

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image3.png)

日期和價格的格式是在 `Movie` 類別的屬性上使用[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)屬性的結果。

開啟*Movie.cs*檔案，並將 `ReleaseDate` 上的 `DisplayFormat` 屬性加上批註，並 `Price` 屬性。 產生的 `Movie` 類別看起來像這樣：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample1.cs)]

再按一次 CTRL + F5 執行應用程式，然後選取 [**首頁**] 索引標籤來查看電影清單。 這次發行日期會顯示日期和時間，而 [價格] 欄位則不會再顯示貨幣符號。 您在 `Movie` 類別中的變更已復原您稍早所見的絕佳格式，但很快就會修正此問題。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image4.png)

### <a name="using-the-dataannotations-datatype-attribute-to-specify-the-data-type"></a>使用 DataAnnotations DataType 屬性來指定資料類型

使用 `Date` 列舉，以[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)屬性取代 `ReleaseDate` 屬性的已加批註的 `DisplayFormat` 屬性。 再次以[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)屬性取代 `Price` 屬性的 `DisplayFormat` 屬性，這次使用 `Currency` 列舉。 完成的程式碼如下所示：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample2.cs)]

執行應用程式。 現在發行日期和價格屬性的格式正確（也就是使用適當的日期和貨幣格式）。 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)屬性會提供內建 ASP.NET MVC 範本的類型中繼資料，以正確的格式呈現欄位。 使用 `DataType` 屬性較適合使用原本在程式碼中的 `DisplayFormat` 屬性，因為 `DataType` 屬性可讓模型更清楚且更有彈性地用於國際化之類的用途。

在下一節中，您將瞭解如何建立自訂範本以顯示日期欄位。

> [!div class="step-by-step"]
> [下一個](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
