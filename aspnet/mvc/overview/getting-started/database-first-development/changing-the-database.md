---
uid: mvc/overview/getting-started/database-first-development/changing-the-database
title: 教學課程：使用 ASP.NET MVC 應用程式變更 EF Database First 的資料庫
description: 本教學課程著重于對資料庫結構進行更新，並將該變更傳播到整個 web 應用程式。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: cfd5c083-a319-482e-8f25-5b38caa93954
msc.legacyurl: /mvc/overview/getting-started/database-first-development/changing-the-database
msc.type: authoredcontent
ms.openlocfilehash: 52cad1120908cf0d4f85770f8e2690f9415c5f56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616260"
---
# <a name="tutorial-change-the-database-for-ef-database-first-with-aspnet-mvc-app"></a>教學課程：使用 ASP.NET MVC 應用程式變更 EF Database First 的資料庫

使用 MVC、Entity Framework 和 ASP.NET 的樣板，您可以建立 web 應用程式，以提供介面給現有的資料庫。 本教學課程系列會示範如何自動產生程式碼，讓使用者可以顯示、編輯、建立和刪除位於資料庫資料表中的資料。 產生的程式碼會對應至資料庫資料表中的資料行。

本教學課程著重于對資料庫結構進行更新，並將該變更傳播到整個 web 應用程式。

在本教學課程中，您已：

> [!div class="checklist"]
> * 加入資料行
> * 將屬性加入至 views

## <a name="prerequisites"></a>Prerequisites

* [產生視圖](generating-views.md)

## <a name="add-a-column"></a>加入資料行

如果您在資料庫中更新資料表的結構，則必須確定您的變更會傳播至資料模型、views 和控制器。

在本教學課程中，您會將新的資料行加入至 Student 資料表，以記錄學生的中間名。 若要加入此資料行，請開啟資料庫專案，然後開啟 Student 檔案。 透過設計工具或 T-sql 程式碼，加入名為**MiddleName**的資料行，其為 NVARCHAR （50），並允許 Null 值。

啟動您的資料庫專案（或 F5），將這項變更部署至本機資料庫。 新的欄位就會加入至資料表。 如果您在 SQL Server 物件總管中看不到它，請按一下窗格中的 重新整理 按鈕。

![顯示新資料行](changing-the-database/_static/image2.png)

新資料行存在於資料庫資料表中，但它目前不存在於資料模型類別中。 您必須更新模型以包含新的資料行。 在 [**模型**] 資料夾中，開啟 [ **ContosoModel** ] 檔案以顯示模型圖表。 請注意，Student 模型不包含 MiddleName 屬性。 以滑鼠右鍵按一下設計介面上的任何位置，然後選取 [**從資料庫更新模型**]。

在 更新**嚮導 中**，選取 重新整理 索引標籤，然後選取 **資料表** > **dbo** > **Student**。 按一下 [完成] **Walkthrough: Calling Code in an VSTO Add-in from VBA**。

更新程式完成之後，資料庫關係圖會包含新的**MiddleName**屬性。 儲存**ContosoModel .edmx**檔案。 您必須儲存這個檔案，新的屬性才會傳播到**Student.cs**類別。 您現在已更新資料庫和模型。

建置方案。

## <a name="add-the-property-to-the-views"></a>將屬性加入至 views

可惜的是，views 仍然不會包含新的屬性。 若要更新這些視圖，您有兩個選項：您可以重新產生視圖，方法是再次新增 Student 類別的樣板，或手動將新屬性新增至現有的視圖。 在本教學課程中，您將再次加入此樣板，因為您尚未對自動產生的視圖進行任何自訂變更。 當您對視圖進行變更，而不想要遺失這些變更時，可以考慮手動新增屬性。

為確保重新建立視圖，請刪除 [ **views**] 底下的 [**學生**] 資料夾，並刪除**studentscontroller.cs**。 然後，以滑鼠右鍵按一下 [**控制器**] 資料夾，並新增**學生**模型的 [樣板]。 同樣地，將控制器命名為**studentscontroller.cs**。 選取 [新增]。

再次建置解決方案。 Views 現在包含 MiddleName 屬性。

![顯示中間名](changing-the-database/_static/image5.png)

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已：

> [!div class="checklist"]
> * 已新增資料行
> * 已將屬性新增至 views

請前進到下一個教學課程，以瞭解如何自訂視圖以顯示學生記錄的詳細資料。
> [!div class="nextstepaction"]
> [自訂視圖](customizing-a-view.md)