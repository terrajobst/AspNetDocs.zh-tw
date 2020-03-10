---
uid: mvc/overview/getting-started/database-first-development/setting-up-database
title: 教學課程：使用 MVC 5 開始使用 EF Database First
description: 本教學課程示範如何從現有的資料庫開始，並快速建立可讓使用者與資料互動的 web 應用程式。
author: Rick-Anderson
ms.author: riande
ms.date: 01/15/2019
ms.topic: tutorial
ms.assetid: 095abad4-3bfe-4f06-b092-ae6a735b7e49
msc.legacyurl: /mvc/overview/getting-started/database-first-development/setting-up-database
msc.type: authoredcontent
ms.openlocfilehash: a760767839a834a9c7e9fe358a3fd806a833261f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583521"
---
# <a name="tutorial-get-started-with-ef-database-first-using-mvc-5"></a>教學課程：使用 MVC 5 開始使用 EF Database First

使用 MVC、Entity Framework 和 ASP.NET 的樣板，您可以建立 web 應用程式，以提供介面給現有的資料庫。 本教學課程系列會示範如何自動產生程式碼，讓使用者可以顯示、編輯、建立和刪除位於資料庫資料表中的資料。 產生的程式碼會對應至資料庫資料表中的資料行。 在此系列的最後一個部分中，您將瞭解如何將資料批註加入至資料模型，以指定驗證需求和顯示格式。 當您完成時，您可以前進到 Azure 文章，以瞭解如何將 .NET 應用程式和 SQL database 部署到 Azure App Service。

本教學課程示範如何從現有的資料庫開始，並快速建立可讓使用者與資料互動的 web 應用程式。 它會使用 Entity Framework 6 和 MVC 5 來建立 web 應用程式。 ASP.NET 的 [樣板] 功能可讓您自動產生程式碼來顯示、更新、建立和刪除資料。 您可以使用 Visual Studio 內的發佈工具，輕鬆地將網站和資料庫部署至 Azure。

這部分的系列內容著重于建立資料庫，並將資料填入其中。

此系列是以 Tom 作者: dykstra 和 Rick Anderson 的貢獻來撰寫。 已根據意見區段中的使用者意見反應來改進。

在本教學課程中，您已：

> [!div class="checklist"]
> * 設定資料庫

## <a name="prerequisites"></a>Prerequisites

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)

## <a name="set-up-the-database"></a>設定資料庫

若要模擬擁有現有資料庫的環境，您必須先使用一些預先填入的資料來建立資料庫，然後建立連接到資料庫的 web 應用程式。

本教學課程是使用 LocalDB 與 Visual Studio 2017 開發的。 您可以使用現有的資料庫伺服器，而不是 LocalDB，但根據您的 Visual Studio 版本和您的資料庫類型而定，可能不支援 Visual Studio 中的所有資料工具。 如果您的資料庫無法使用這些工具，您可能需要在資料庫的管理元件內執行一些資料庫特定步驟。

如果您的 Visual Studio 版本中的資料庫工具發生問題，請確定您已安裝最新版本的資料庫工具。 如需有關更新或安裝資料庫工具的詳細資訊，請參閱[Microsoft SQL Server Data tools](https://msdn.microsoft.com/data/hh297027)。

啟動 Visual Studio 並建立**SQL Server 資料庫專案**。 將專案命名為**ContosoUniversityData**。

![建立資料庫專案](setting-up-database/_static/image1.png)

您現在有一個空的資料庫專案。 為確保您可以將此資料庫部署至 Azure，您會將 Azure SQL Database 設定為專案的目標平臺。 設定目標平臺並不會實際部署資料庫;這只表示資料庫專案會驗證資料庫設計是否與目標平臺相容。 若要設定目標平臺，請開啟專案的**屬性**，然後針對目標平臺選取 [ **Microsoft Azure SQL Database** ]。

您可以藉由加入定義資料表的 SQL 腳本來建立本教學課程所需的資料表。 以滑鼠右鍵按一下您的專案，並加入新的專案。 選取**資料表和 Views** > **資料表**，並將它命名為*Student*。

在資料表檔案中，以下列程式碼取代 T-sql 命令以建立資料表。

[!code-sql[Main](setting-up-database/samples/sample1.sql)]

請注意，[設計] 視窗會自動與程式碼同步處理。 您可以使用程式碼或設計工具。

![顯示程式碼和設計](setting-up-database/_static/image5.png)

新增另一個資料表。 這次請將它命名為「課程」，並使用下列 T-sql 命令。

[!code-sql[Main](setting-up-database/samples/sample2.sql)]

再重複一次，以建立名為註冊的資料表。

[!code-sql[Main](setting-up-database/samples/sample3.sql)]

您可以透過在部署資料庫之後執行的腳本，將資料填入資料庫。 將部署後腳本新增至專案。 以滑鼠右鍵按一下您的專案，並加入新的專案。 選取 [**使用者腳本**] > **部署後腳本**。 您可以使用預設名稱。

將下列 T-sql 程式碼新增至部署後腳本。 當找不到相符的記錄時，此腳本只會將資料新增至資料庫。 它不會覆寫或刪除您可能已在資料庫中輸入的任何資料。

[!code-sql[Main](setting-up-database/samples/sample4.sql)]

請務必注意，部署後腳本會在您每次部署資料庫專案時執行。 因此，撰寫此腳本時，您必須仔細考慮您的需求。 在某些情況下，您可能會想要在每次部署專案時，從一組已知的資料開始。 在其他情況下，您可能不想要以任何方式改變現有的資料。 根據您的需求，您可以決定是否需要部署後腳本，或是您需要在腳本中包含的內容。 如需使用部署後腳本填入資料庫的詳細資訊，請參閱[在 SQL Server 資料庫專案中包含資料](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx)。

現在您有4個 SQL 腳本檔案，但沒有實際的資料表。 您已準備好將資料庫專案部署至 localdb。 在 Visual Studio 中，按一下 [開始] 按鈕（或 F5）來建立及部署您的資料庫專案。 檢查 [**輸出**] 索引標籤，確認組建和部署是否成功。

若要查看是否已建立新的資料庫，請開啟**SQL Server 物件總管**，並在正確的本機資料庫伺服器中尋找專案的名稱（在此案例中為 **（localdb） \ProjectsV13**）。

若要查看資料表是否已填入資料，請以滑鼠右鍵按一下資料表，然後選取 [**查看資料**]。

![顯示資料表資料](setting-up-database/_static/image9.png)

資料表資料的可編輯檢視隨即顯示。 例如，如果您選取 **資料表** > **dbo. 課程** > **視圖資料**，您會看到包含三個數據行的資料表（**課程**、**標題**和**點數**）和四個數據列。

## <a name="additional-resources"></a>其他資源

如需 Code First 開發的簡介範例，請參閱[使用 ASP.NET MVC 5 消費者入門](../introduction/getting-started.md)。 如需更先進的範例，請參閱[建立 ASP.NET MVC 4 應用程式的 Entity Framework 資料模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。

如需有關選取要使用哪一個 Entity Framework 方法的指引，請參閱[Entity Framework 開發方法](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已：

> [!div class="checklist"]
> * 設定資料庫

請前進到下一個教學課程，以瞭解如何建立 web 應用程式和資料模型。
> [!div class="nextstepaction"]
> [建立 web 應用程式和資料模型](creating-the-web-application.md)
