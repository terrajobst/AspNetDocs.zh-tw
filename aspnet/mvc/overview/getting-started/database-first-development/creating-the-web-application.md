---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: 教學課程：使用 ASP.NET MVC 建立 EF Database First 的 Web 應用程式和資料模型
description: 本教學課程著重于建立 web 應用程式，並根據您的資料庫資料表產生資料模型。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 30fd42be5677df6fa6ee0630914098c30d21385b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616267"
---
# <a name="tutorial-create-the-web-application-and-data-models-for-ef-database-first-with-aspnet-mvc"></a>教學課程：使用 ASP.NET MVC 建立 EF Database First 的 Web 應用程式和資料模型

 使用 MVC、Entity Framework 和 ASP.NET 的樣板，您可以建立 web 應用程式，以提供介面給現有的資料庫。 本教學課程系列會示範如何自動產生程式碼，讓使用者可以顯示、編輯、建立和刪除位於資料庫資料表中的資料。 產生的程式碼會對應至資料庫資料表中的資料行。

本教學課程著重于建立 web 應用程式，並根據您的資料庫資料表產生資料模型。

在本教學課程中，您已：

> [!div class="checklist"]
> * 建立 ASP.NET Web 應用程式
> * 產生模型

## <a name="prerequisites"></a>Prerequisites

* [使用 MVC 5 開始使用 Entity Framework 6 Database First](setting-up-database.md)

## <a name="create-an-aspnet-web-app"></a>建立 ASP.NET Web 應用程式

在新方案或與資料庫專案相同的方案中，在 Visual Studio 中建立新的專案，然後選取 [ **ASP.NET Web 應用程式**] 範本。 將專案命名為**ContosoSite**。

![建立專案](creating-the-web-application/_static/image1.png)

按一下 [確定]。

在 [新增 ASP.NET 專案] 視窗中，選取 [ **MVC** ] 範本。 您現在可以清除 **[雲端中的主機**] 選項，因為您稍後會將應用程式部署至雲端。 按一下 **[確定]** 以建立應用程式。

專案會使用預設檔案和資料夾來建立。

在本教學課程中，您將使用 Entity Framework 6。 您可以透過 [管理 NuGet 封裝] 視窗，再次檢查項目中的 Entity Framework 版本。 如有必要，請更新您的 Entity Framework 版本。

![顯示版本](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a>產生模型

您現在將從資料庫資料表建立 Entity Framework 模型。 這些模型是您將用來處理資料的類別。 每個模型都會鏡像資料庫中的資料表，並包含對應至資料表中資料行的屬性。

以滑鼠右鍵按一下 [**模型**] 資料夾，然後選取 [**加入**] 和 [**新增專案**]。

在 加入新專案 視窗中，選取左窗格中的 **資料**，然後從中間窗格的選項**ADO.NET 實體資料模型**。 將新的模型檔案命名為**ContosoModel**。

按一下 [新增]。

在實體資料模型 Wizard 中，從 [資料庫] 選取 [ **EF Designer**]。

按 [下一步]。

如果您的開發環境內已定義資料庫連接，您可能會看到其中一個預先選取的連接。 不過，您想要建立與您在本教學課程的第一個部分中所建立之資料庫的新連接。 按一下 [**新增連接**] 按鈕。

在 連線屬性視窗中，提供您的資料庫建立所在之本機伺服器的名稱（在此案例中為 **（localdb） \ProjectsV13**）。 提供伺服器名稱之後，請從可用的資料庫中選取 ContosoUniversityData。

![設定連接屬性](creating-the-web-application/_static/image8.png)

按一下 [確定]。

現在會顯示正確的連接屬性。 在 web.config 檔案中，您可以使用預設名稱來連接。

按 [下一步]。

選取最新版本的 Entity Framework。

按 [下一步]。

選取 [**資料表]** ，為所有三個數據表產生模型。

按一下 [完成] **Walkthrough: Calling Code in an VSTO Add-in from VBA**。

如果您收到安全性警告，請選取 **[確定]** 繼續執行範本。

系統會從資料庫資料表產生模型，並顯示一個圖表，其中顯示資料表之間的屬性和關聯性。

![模型的圖表](creating-the-web-application/_static/image11.png)

[模型] 資料夾現在包含許多與從資料庫產生之模型相關的新檔案。

**ContosoModel.CoNtext.cs**檔案包含衍生自**DbCoNtext**類別的類別，並針對對應至資料庫資料表的每個模型類別提供屬性。 **Course.cs**、 **Enrollment.cs**和**Student.cs**檔案包含代表資料庫資料表的模型類別。 使用樣板時，您將會同時使用內容類別和模型類別。

繼續進行本教學課程之前，請先建立專案。 在下一節中，您將會根據資料模型產生程式碼，但如果尚未建立專案，該區段將無法使用。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已：

> [!div class="checklist"]
> * 建立 ASP.NET web 應用程式
> * 產生模型

前進到下一個教學課程，以瞭解如何建立以資料模型為基礎的產生程式碼。
> [!div class="nextstepaction"]
> [產生視圖](generating-views.md)
