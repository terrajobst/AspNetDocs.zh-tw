---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: 教學課程：使用 ASP.NET MVC 應用程式增強 EF Database First 的資料驗證
description: 本教學課程著重于將資料批註加入至資料模型，以指定驗證需求和顯示格式。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: 897cd7c6a40445e2a4abede50d81e101372d3233
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616274"
---
# <a name="tutorial-enhance-data-validation-for-ef-database-first-with-aspnet-mvc-app"></a>教學課程：使用 ASP.NET MVC 應用程式增強 EF Database First 的資料驗證

使用 MVC、Entity Framework 和 ASP.NET 的樣板，您可以建立 web 應用程式，以提供介面給現有的資料庫。 本教學課程系列會示範如何自動產生程式碼，讓使用者可以顯示、編輯、建立和刪除位於資料庫資料表中的資料。 產生的程式碼會對應至資料庫資料表中的資料行。

本教學課程著重于將資料批註加入至資料模型，以指定驗證需求和顯示格式。 已根據意見區段中的使用者意見反應來改進。

在本教學課程中，您已：

> [!div class="checklist"]
> * 加入資料批註
> * 加入中繼資料類別

## <a name="prerequisites"></a>Prerequisites

* [自訂視圖](customizing-a-view.md)

## <a name="add-data-annotations"></a>加入資料批註

如您在先前的主題中所見，部分資料驗證規則會自動套用至使用者輸入。 例如，您只能為 [年級] 屬性提供一個數位。 若要指定更多資料驗證規則，您可以將資料批註加入至模型類別。 在您的 web 應用程式中，會針對指定的屬性套用這些批註。 您也可以套用變更屬性顯示方式的格式化屬性;例如，變更文字標籤所使用的值。

在本教學課程中，您將加入資料批註，以限制針對 FirstName、LastName 和 MiddleName 屬性所提供的值長度。 在資料庫中，這些值限制為50個字元;不過，在您的 web 應用程式中，目前不會強制字元限制。 如果使用者為其中一個值提供超過50個字元，當嘗試將值儲存至資料庫時，頁面將會損毀。 您也會將等級限制為0到4之間的值。

選取 [ > **ContosoModel**的**模型**] > **ContosoModel.tt** ，然後開啟*Student.cs*檔案。 將下列反白顯示的程式碼新增至類別。

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

開啟*Enrollment.cs* ，並新增下列反白顯示的程式碼。

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

建置方案。

按一下 [**學生清單**]，然後選取 [**編輯**]。 如果您嘗試輸入超過50個字元，就會顯示錯誤訊息。

![顯示錯誤訊息](enhancing-data-validation/_static/image1.png)

回到首頁。 按一下 [**註冊清單**]，然後選取 [**編輯**]。 嘗試提供高於4的等級。 您會收到此錯誤：*欄位等級必須介於0到4之間。*

## <a name="add-metadata-classes"></a>加入中繼資料類別

當您不希望資料庫變更時，直接將驗證屬性加入至模型類別會運作。不過，如果您的資料庫變更，而您需要重新產生模型類別，您將會遺失已套用至模型類別的所有屬性。 這種方法可能非常沒有效率，而且容易遺失重要的驗證規則。

若要避免這個問題，您可以新增包含屬性的中繼資料類別。 當您將模型類別關聯至中繼資料類別時，這些屬性會套用至模型。 在此方法中，您可以重新產生模型類別，而不會遺失已套用至中繼資料類別的所有屬性。

在 [**模型**] 資料夾中，新增名為*Metadata.cs*的類別。

將*Metadata.cs*中的程式碼取代為下列程式碼。

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

這些中繼資料類別包含您先前套用至模型類別的所有驗證屬性。 **顯示**屬性是用來變更文字標籤所使用的值。

現在，您必須將模型類別關聯至中繼資料類別。

在 [**模型**] 資料夾中，新增名為*PartialClasses.cs*的類別。

以下列程式碼取代檔案的內容。

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

請注意，每個類別都標示為 `partial` 類別，而且每個類別都符合名稱和命名空間，做為自動產生的類別。 藉由將中繼資料屬性套用至部分類別，您可以確保資料驗證屬性會套用至自動產生的類別。 當您重新產生模型類別時，這些屬性將不會遺失，因為中繼資料屬性會套用到不會重新產生的部分類別中。

若要重新產生自動產生的類別，請開啟*ContosoModel .edmx*檔案。 同樣地，以滑鼠右鍵按一下設計介面，然後選取 [**從資料庫更新模型**]。 即使您尚未變更資料庫，此程式還是會重新產生類別。 在 [**重新**整理] 索引標籤中，選取 [**資料表**] 並**完成**。

儲存*ContosoModel .edmx*檔案以套用變更。

開啟*Student.cs*檔案或*Enrollment.cs*檔案，並注意您稍早套用的資料驗證屬性已不再位於檔案中。 不過，請執行應用程式，並請注意，當您輸入資料時，仍然會套用驗證規則。

## <a name="conclusion"></a>結論

此系列提供了簡單的範例，說明如何從現有的資料庫產生程式碼，讓使用者可以編輯、更新、建立和刪除資料。 它使用 ASP.NET MVC 5、Entity Framework 和 ASP.NET 樣板來建立專案。 

如需 Code First 開發的簡介範例，請參閱[使用 ASP.NET MVC 5 消費者入門](../introduction/getting-started.md)。 

如需更先進的範例，請參閱[建立 ASP.NET MVC 4 應用程式的 Entity Framework 資料模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 請注意，您用來處理 Database First 中資料的 DbCoNtext API，與您用來處理 Code First 中資料的 API 相同。 即使您想要使用 Database First，您也可以瞭解如何處理更複雜的案例，例如讀取和更新相關資料、處理並行衝突，以及從 Code First 教學課程。 唯一的差異在於資料庫、內容類別和實體類別的建立方式。

## <a name="additional-resources"></a>其他資源

如需資料驗證注釋的完整清單，您可以將它套用至屬性和類別，請參閱[system.workflow.componentmodel.activity. DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已：

> [!div class="checklist"]
> * 新增的資料批註
> * 已新增中繼資料類別

若要瞭解如何將 web 應用程式和 SQL database 部署到 Azure App Service，請參閱此教學課程：
> [!div class="nextstepaction"]
> [將 .NET 應用程式部署至 Azure App Service](/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase/)
