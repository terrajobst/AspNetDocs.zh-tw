---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
title: 使用 Entity Framework 4.0 和 ObjectDataSource 控制項，第2部分：新增商務邏輯層和單元測試 |Microsoft Docs
author: tdykstra
description: 本教學課程系列是以 Entity Framework 4.0 教學課程系列的消費者入門所建立的 Contoso 大學 web 應用程式為基礎。 I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: efb0e677-10b8-48dc-93d3-9ba3902dd807
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
msc.type: authoredcontent
ms.openlocfilehash: 24344cc33d7c26d7c408db26c0530ef2c708a7d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78546764"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests"></a>使用 Entity Framework 4.0 和 ObjectDataSource 控制項，第2部分：新增商務邏輯層和單元測試

由[Tom 作者: dykstra](https://github.com/tdykstra)

> 本教學課程系列是[以 Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started)教學課程系列的消費者入門所建立的 Contoso 大學 web 應用程式為基礎。 如果您未完成先前的教學課程，做為本教學課程的起點，您可以下載您所建立[的應用程式](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)。 您也可以下載完整的教學課程系列所建立[的應用程式](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)。 如果您有關于教學課程的問題，可以將其張貼到[ASP.NET Entity Framework 論壇](https://forums.asp.net/1227.aspx)。

在上一個教學課程中，您已使用 Entity Framework 和 `ObjectDataSource` 控制項建立了多層式 web 應用程式。 本教學課程說明如何新增商務邏輯，同時保持商業邏輯層（BLL）和資料存取層（DAL）的不同，並示範如何為 BLL 建立自動化的單元測試。

在本教學課程中，您將完成下列工作：

- 建立存放庫介面，以宣告您所需的資料存取方法。
- 在存放庫類別中執行存放庫介面。
- 建立呼叫儲存機制類別的商業邏輯類別，以執行資料存取函數。
- 將 `ObjectDataSource` 控制項連接至商業邏輯類別，而不是儲存機制類別。
- 建立單元測試專案，以及針對其資料存放區使用記憶體內部集合的存放庫類別。
- 針對您想要加入至商業邏輯類別的商務邏輯建立單元測試，然後執行測試並查看失敗。
- 在商業邏輯類別中執行商務邏輯，然後重新執行單元測試並查看其通過。

您將使用在上一個教學課程中建立的*default.aspx*和*DepartmentsAdd .aspx*頁面。

## <a name="creating-a-repository-interface"></a>建立存放庫介面

您將從建立存放庫介面開始。

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image1.png)

在*DAL*資料夾中，建立新的類別檔案，並將其命名為*ISchoolRepository.cs*，並以下列程式碼取代現有的程式碼：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample1.cs)]

介面會針對您在存放庫類別中建立的每個 CRUD （create、read、update、delete）方法定義一個方法。

在*SchoolRepository.cs*的 `SchoolRepository` 類別中，表示此類別會執行 `ISchoolRepository` 介面：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample2.cs)]

## <a name="creating-a-business-logic-class"></a>建立商業邏輯類別

接下來，您將建立商業邏輯類別。 如此一來，您就可以加入 `ObjectDataSource` 控制項將執行的商務邏輯，但您還不會這麼做。 目前，新的商業邏輯類別只會執行存放庫所需的相同 CRUD 作業。

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image3.png)

建立新的資料夾，並將它命名為*BLL*。 （在實際的應用程式中，商業邏輯層通常會實作為類別庫，也就是個別的專案，但為了讓本教學課程保持簡單，BLL 類別將會保留在專案資料夾中）。

在 [ *BLL* ] 資料夾中，建立新的類別檔案，將其命名為*SchoolBL.cs*，並以下列程式碼取代現有的程式碼：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample3.cs)]

這段程式碼會建立您稍早在存放庫類別中看到的相同 CRUD 方法，而不是直接存取 Entity Framework 方法，而是呼叫儲存機制類別方法。

保存存放庫類別參考的類別變數定義為介面類別型，而具現化儲存機制類別的程式碼則包含在兩個函式中。 `ObjectDataSource` 控制項將會使用無參數的函式。 它會建立您稍早建立之 `SchoolRepository` 類別的實例。 另一個函式允許將商業邏輯類別具現化的任何程式碼，傳入任何會執行存放庫介面的物件。

呼叫儲存機制類別和兩個函式的 CRUD 方法，可讓您使用商業邏輯類別搭配您選擇的任何後端資料存放區。 商業邏輯類別不需要知道它所呼叫的類別會如何保存資料。 （這通常稱為*持續性無知*）。這有助於進行單元測試，因為您可以將商業邏輯類別連接到使用類似記憶體內部 `List` 集合來儲存資料的儲存機制。

> [!NOTE]
> 就技術上而言，實體物件仍然不是持續性，因為它們是從繼承自 Entity Framework 之 `EntityObject` 類別的類別具現化。 如需完整的持續性無知，您可以使用*簡單的 CLR 物件*（或*poco*）來取代繼承自 `EntityObject` 類別的物件。 使用 Poco 已超出本教學課程的範圍。 如需詳細資訊，請參閱 MSDN 網站上的可[測試性和 Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx) ）。

現在您可以將 `ObjectDataSource` 控制項連接到商業邏輯類別，而不是存放庫，並確認所有專案的運作方式與之前相同。

在 [ *default.aspx* ] 和 [ *DepartmentsAdd*] 中，將每個出現的 `TypeName="ContosoUniversity.DAL.SchoolRepository"` 變更為 `TypeName="ContosoUniversity.BLL.SchoolBL`"。 （其中共有四個實例）。

執行 [*部門 .aspx* ] 和 [ *DepartmentsAdd* ] 頁面，確認它們仍然如先前的方式運作。

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image5.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image7.png)

## <a name="creating-a-unit-test-project-and-repository-implementation"></a>建立單元測試專案和存放庫的執行

使用 [**測試專案**] 範本將新專案加入至方案，並將其命名為 `ContosoUniversity.Tests`。

在測試專案中，加入 `System.Data.Entity` 的參考，並將專案參考加入至 `ContosoUniversity` 專案。

您現在可以建立將用於單元測試的儲存機制類別。 此儲存機制的資料存放區將會在類別內。

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image9.png)

在測試專案中，建立新的類別檔案，並將其命名為*MockSchoolRepository.cs*，並以下列程式碼取代現有的程式碼：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample4.cs)]

這個存放庫類別與直接存取 Entity Framework 的 CRUD 方法相同，但是它們會使用記憶體中 `List` 的集合，而不是使用資料庫。 這可讓測試類別更容易設定及驗證商業邏輯類別的單元測試。

## <a name="creating-unit-tests"></a>建立單元測試

**測試**專案範本會為您建立存根單元測試類別，而您的下一個工作是修改這個類別，方法是針對您想要加入至商業邏輯類別的商務邏輯，將單元測試方法加入其中。

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image11.png)

在 Contoso 大學，任何個人講師只能是單一部門的系統管理員，而且您需要新增商務邏輯來強制執行此規則。 首先，您會加入測試並執行測試，以查看它們是否失敗。 接著，您將新增程式碼並重新執行測試，以查看它們是否通過。

開啟*UnitTest1.cs*檔案，並針對您在 ContosoUniversity 專案中建立的商務邏輯和資料存取層，加入 `using` 語句：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample5.cs)]

使用下列方法來取代 `TestMethod1` 方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample6.cs)]

`CreateSchoolBL` 方法會建立您為單元測試專案所建立之儲存機制類別的實例，然後將它傳遞給商業邏輯類別的新實例。 然後，方法會使用商業邏輯類別，插入您可以在測試方法中使用的三個部門。

測試方法會驗證商業邏輯類別是否會在有人嘗試插入具有與現有部門相同系統管理員的新部門，或如果有人嘗試將部門的系統管理員設定為人員的識別碼來更新該部門，而擲回例外狀況。誰已經是另一個部門的系統管理員。

您尚未建立 exception 類別，因此不會編譯此程式碼。 若要進行編譯，請在 `DuplicateAdministratorException` 上按一下滑鼠右鍵，然後依序選取 [**產生**] 和 [**類別**]。

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image13.png)

這會在測試專案中建立一個類別，您可以在建立主要專案中的例外狀況類別之後加以刪除。 和會實作為商務邏輯。

執行測試專案。 如預期般，測試失敗。

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image15.png)

## <a name="adding-business-logic-to-make-a-test-pass"></a>新增商務邏輯以進行測試階段

接下來，您將會實行商務邏輯，使其無法設定為已成為另一個部門之系統管理員的部門系統管理員。 您將會從商業邏輯層擲回例外狀況，如果使用者編輯部門，然後在選取已經是系統管理員的人之後按一下 [**更新**]，則會在展示層中攔截。 （您也可以在轉譯頁面之前，從已被系統管理員的下拉式清單中移除講師，但此處的目的是要使用商業邏輯層）。

首先，建立當使用者嘗試讓講師成為多個部門的系統管理員時，所擲回的例外狀況類別。 在主要專案中，于 [ *BLL* ] 資料夾中建立新的類別檔案，將其命名為*DuplicateAdministratorException.cs*，並以下列程式碼取代現有的程式碼：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample7.cs)]

現在刪除您稍早在測試專案中建立的暫存*DuplicateAdministratorException.cs*檔案，以便進行編譯。

在主要專案中，開啟*SchoolBL.cs*檔案，並新增包含驗證邏輯的下列方法。 （此程式碼會參考稍後將建立的方法）。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample8.cs)]

當您插入或更新 `Department` 實體時，會呼叫此方法，以檢查另一個部門是否已有相同的系統管理員。

程式碼會呼叫方法，在資料庫中搜尋與所插入或更新之實體具有相同 `Administrator` 屬性值的 `Department` 實體。 如果找到其中一個，程式碼就會擲回例外狀況。 如果要插入或更新的實體沒有 `Administrator` 值，則不需要驗證檢查，而且如果在更新期間呼叫方法，且找到的 `Department` 實體符合正在更新的 `Department` 實體，就不會擲回任何例外狀況。

從 `Insert` 和 `Update` 方法呼叫新的方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample9.cs)]

在*ISchoolRepository.cs*中，為新的資料存取方法新增下列宣告：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample10.cs)]

在*SchoolRepository.cs*中，新增下列 `using` 語句：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample11.cs)]

在*SchoolRepository.cs*中，新增下列新的資料存取方法：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample12.cs)]

此程式碼會抓取具有指定之系統管理員 `Department` 實體。 只能找到一個部門（如果有的話）。 不過，由於資料庫中沒有內建的條件約束，因此如果找到多個部門，則傳回型別會是集合。

根據預設，當物件內容從資料庫抓取實體時，它會在其物件狀態管理員中持續追蹤它們。 `MergeOption.NoTracking` 參數指定不會針對此查詢執行此追蹤。 這是必要的，因為查詢可能會傳回您嘗試更新的確切實體，然後您就無法附加該實體。 例如，如果您編輯 [*部門 .aspx* ] 頁面中的 [歷程記錄] 部門，並將系統管理員保持不變，此查詢將會傳回曆程記錄部門。 如果未設定 `NoTracking`，則物件內容在其物件狀態管理員中可能已經有歷程記錄部門實體。 然後，當您附加從 view 狀態重新建立的歷程記錄部門實體時，物件內容會擲回例外狀況，指出 `"An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key"`。

（另一個方法是指定 `MergeOption.NoTracking`，您可以只針對此查詢建立新的物件內容。 因為新的物件內容會有自己的物件狀態管理員，所以當您呼叫 `Attach` 方法時，就不會發生衝突。 新的物件內容會與原始物件內容共用中繼資料和資料庫連接，因此，此替代方法的效能影響會降到最低。 不過，這裡所示的方法會介紹 `NoTracking` 選項，您會在其他內容中找到這項功能。 本系列稍後的教學課程會進一步討論 `NoTracking` 選項）。

在測試專案中，將新的資料存取方法加入至*MockSchoolRepository.cs*：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample13.cs)]

這段程式碼會使用 LINQ 來執行相同的資料選取，`ContosoUniversity` 專案存放庫使用 LINQ to Entities 的。

再次執行測試專案。 測試這一次會成功。

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image17.png)

## <a name="handling-objectdatasource-exceptions"></a>處理 ObjectDataSource 例外狀況

在 `ContosoUniversity` 專案中，執行 [*部門 .aspx* ] 頁面，然後嘗試將部門的系統管理員變更為已經是另一個部門之系統管理員的使用者。 （請記住，您只能編輯您在本教學課程中新增的部門，因為資料庫已預先載入了不正確資料）。您會收到下列伺服器錯誤頁面：

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image19.png)

您不想讓使用者看到這種錯誤頁面，因此您需要新增錯誤處理常式代碼。 開啟 [*部門 .aspx* ]，並指定 `DepartmentsObjectDataSource`之 `OnUpdated` 事件的處理常式。 `ObjectDataSource` 開頭標記現在與下列範例類似。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample14.aspx)]

在*Departments.aspx.cs*中，新增下列 `using` 語句：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample15.cs)]

為 `Updated` 事件新增下列處理常式：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample16.cs)]

如果 `ObjectDataSource` 控制項在嘗試執行更新時攔截到例外狀況，它會將事件引數（`e`）中的例外狀況傳遞給這個處理常式。 處理常式中的程式碼會檢查例外狀況是否為重複的系統管理員例外狀況。 如果是，則程式碼會建立一個驗證程式控制項，其中包含要顯示 `ValidationSummary` 控制項的錯誤訊息。

執行頁面，並嘗試讓某人再次成為兩個部門的系統管理員。 此時，`ValidationSummary` 控制項會顯示錯誤訊息。

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image21.png)

對 [ *DepartmentsAdd* ] 頁面進行類似的變更。 在*DepartmentsAdd*中，指定 `DepartmentsObjectDataSource`之 `OnInserted` 事件的處理常式。 產生的標記會如下列範例所示。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample17.aspx)]

在*DepartmentsAdd.aspx.cs*中，新增相同的 `using` 語句：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample18.cs)]

新增下列事件處理常式：

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample19.cs)]

您現在可以測試 [ *DepartmentsAdd.aspx.cs* ] 頁面，以確認它也會正確地處理讓一個人成為多個部門之系統管理員的嘗試。

這會完成使用 `ObjectDataSource` 控制項搭配 Entity Framework 來執行存放庫模式的簡介。 如需有關存放庫模式和可測試性的詳細資訊，請參閱 MSDN 白皮書的可[測試性和 Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx)。

在下列教學課程中，您將瞭解如何將排序和篩選功能新增至應用程式。

> [!div class="step-by-step"]
> [上一頁](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)
> [下一頁](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)
