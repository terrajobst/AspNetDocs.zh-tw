---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: 教學課程：使用 ASP.NET MVC 應用程式產生 EF Database First 的視圖
description: 本教學課程著重于使用 ASP.NET 的架構來產生控制器和 views。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: e71e13e22d8a72e1699cfc70d4d93af603edba5b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616204"
---
# <a name="tutorial-generate-views-for-ef-database-first-with-aspnet-mvc-app"></a>教學課程：使用 ASP.NET MVC 應用程式產生 EF Database First 的視圖

使用 MVC、Entity Framework 和 ASP.NET 的樣板，您可以建立 web 應用程式，以提供介面給現有的資料庫。 本教學課程系列會示範如何自動產生程式碼，讓使用者可以顯示、編輯、建立和刪除位於資料庫資料表中的資料。 產生的程式碼會對應至資料庫資料表中的資料行。

本教學課程著重于使用 ASP.NET 的架構來產生控制器和 views。

在本教學課程中，您已：

> [!div class="checklist"]
> * 新增 scaffold
> * 將連結新增至新的視圖
> * 顯示學生的視圖
> * 顯示註冊視圖

## <a name="prerequisite"></a>必要條件

* [建立 web 應用程式和資料模型](creating-the-web-application.md)

## <a name="add-scaffold"></a>新增 scaffold

您已準備好產生可為模型類別提供標準資料作業的程式碼。 您可以藉由新增 scaffold 專案來加入程式碼。 您可以新增的架構類型有許多選項;在本教學課程中，scaffold 會包含與您在上一節中建立的學生和註冊模型對應的控制器和 views。

為了維持專案的一致性，您會將新的控制器新增至 [現有的**控制器**] 資料夾。 以滑鼠右鍵按一下 [**控制器**] 資料夾，**然後選取 [** 新增 > **新的 scaffold 專案**]。

使用 [ **Entity Framework] 選項，選取具有 views 的 MVC 5 控制器**。 此選項會產生控制器和視圖，以更新、刪除、建立和顯示模型中的資料。

![新增 mvc 控制器](generating-views/_static/image2.png)

針對 [模型] 類別選取 [**學生（ContosoSite）** ]，然後選取內容類別的**ContosoUniversityDataEntities （ContosoSite）** 。 將控制器名稱保留為**studentscontroller.cs**。

按一下 [新增]。

如果您收到錯誤，可能是因為您未在上一節中建立專案。 若是如此，請嘗試建立專案，然後再次加入 scaffold 專案。

程式碼產生程式完成之後，您會在專案的 [**控制器**和**views** ] > [**學生**] 資料夾中看到新的控制器和 views。

再次執行相同的步驟，但新增**註冊**類別的 scaffold。 完成時，您會有一個**EnrollmentsController.cs**檔案，以及**一個名為** **註冊** 的資料夾，其中包含 建立、刪除、詳細資料、編輯 和 索引

## <a name="add-links-to-new-views"></a>將連結新增至新的視圖

為了讓您更輕鬆地流覽至新的視圖，您可以將幾個超連結新增至學生和註冊的索引視圖。 在 > **Home** > 的**Views**資料夾中開啟檔案，這是您網站的*首頁。* 在 jumbotron 下方新增下列程式碼。

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

對於 Html.actionlink 方法，第一個參數是要顯示在連結中的文字。 第二個參數是動作，而第三個參數是控制器的名稱。 例如，第一個連結會指向 Studentscontroller.cs 中的索引動作。 實際的超連結是由這些值所構成。 第一個連結最後會將使用者帶到**Views/** student 資料夾中的**Index. cshtml**檔案。

## <a name="display-student-views"></a>顯示學生的視圖

您會驗證新增至專案的程式碼是否正確地顯示學生清單，並可讓使用者編輯、建立或刪除資料庫中的學生記錄。

以滑鼠右鍵按一下 > **Home** * > 的* **Views**檔案，然後選取 [**在瀏覽器中查看**]。 在應用程式首頁上，選取 [**學生清單**]。

![](generating-views/_static/image6.png)

在 [**索引**] 頁面上，請注意要修改此資料的學生和連結清單。 選取 [**新建] 連結，並**為新的學生提供一些值。 按一下 [**建立**]，並注意新的 student 已新增至您的清單。

回到 [**索引**] 頁面，選取 [**編輯**] 連結，然後變更學生的一些值。 按一下 [**儲存**]，並注意學生記錄已經變更。

最後，選取 [**刪除**] 連結，然後按一下 [**刪除**] 按鈕，確認您想要刪除記錄。

在不撰寫任何程式碼的情況下，您已新增可對 Student 資料表中的資料執行一般作業的視圖。

您可能已經注意到，欄位的文字標籤是以資料庫屬性為基礎（例如**LastName**），這不一定是您想要顯示在網頁上的內容。 例如，您可能會偏好將標籤**命名為姓氏**。 您稍後會在本教學課程中修正此顯示問題。

## <a name="display-enrollment-views"></a>顯示註冊視圖

您的資料庫包含 Student 與註冊資料表之間的一對多關聯性，以及課程和註冊資料表之間的一對多關聯性。 註冊的視圖會正確地處理這些關聯性。 流覽至您網站的首頁，然後選取 [註冊] 連結**清單**，再選取 [**建立新**的] 連結。

此視圖會顯示一個表單，用來建立新的註冊記錄。 特別要注意的是，表單包含 [ **CourseID** ] 下拉式清單和 [ **StudentID** ] 下拉式清單。 這兩者都會以相關資料表中的值填入。

此外，系統會根據欄位的資料類型，自動套用所提供值的驗證。 **等級**需要數位，因此如果您嘗試提供不相容的值，就會顯示錯誤訊息：*欄位等級必須是數位。*

您已確認自動產生的視圖可讓使用者使用資料庫中的資料。 在此系列的下一個教學課程中，您將會更新資料庫，並在 web 應用程式中進行對應的變更。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已：

> [!div class="checklist"]
> * 已新增 scaffold
> * 已將連結新增至新的視圖
> * 顯示的學生視圖
> * 顯示的註冊視圖

請前進到下一個教學課程，以瞭解如何變更資料庫。
> [!div class="nextstepaction"]
> [變更資料庫](changing-the-database.md)