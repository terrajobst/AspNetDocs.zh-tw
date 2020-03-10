---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
title: ASP.NET MVC 4 簡介 |Microsoft Docs
author: Rick-Anderson
description: 如果本教學課程可在此使用 Visual Studio 2013，則為更新版本。 新的教學課程使用 ASP.NET MVC 5，它提供了許多透過 t 的改良功能 。
ms.author: riande
ms.date: 08/15/2012
ms.assetid: ed66530a-04d5-49eb-b76a-85be1f57c437
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 51709a9c6ddb39b8fcd1cd94cd08d530a595825a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78599642"
---
# <a name="intro-to-aspnet-mvc-4"></a>ASP.NET MVC 4 簡介

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> 如果本教學[課程](../../getting-started/introduction/getting-started.md)可在此使用[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)，則為更新版本。 新的教學課程會使用 ASP.NET MVC 5，這在此教學課程中提供了許多改進功能。
>
> 本教學課程將告訴您使用 Microsoft [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)或 Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC 4 Web 應用程式的基本概念。 建議使用 Visual Studio 2012，您不需要安裝任何專案，即可完成本教學課程。 如果您使用 Visual Studio 2010，您必須安裝下列元件。 您可以按一下下列連結來安裝所有這些專案：
>
> - [Visual Studio Web Developer Express SP1 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [適用于 ASP.NET MVC 4 的 DOWNLOAD-WPI 安裝程式](https://go.microsoft.com/fwlink/?LinkId=243392)
> - [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)
> - [SSDT](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)
>
> 如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請安裝[適用于 ASP.NET MVC 4 的 download-wpi 安裝程式](https://go.microsoft.com/fwlink/?LinkId=243392)和： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)
>
> 本主題提供具有C#原始程式碼的 Visual Web Developer 專案。 [下載C#版本](https://code.msdn.microsoft.com/Intro-to-ASPNET-MVC-4-61d0219d/file/114480/1/MvcMovie.zip)。
>
> 在教學課程中，您會在 Visual Studio 中執行應用程式。 您也可以將應用程式部署至主機服務提供者，使其可透過網際網路使用。 Microsoft 在[免費的 Windows Azure 試用帳戶](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)中，最多可為10個網站提供免費的 web 主機。 如需如何將 Visual Studio Web 專案部署至 Windows Azure 網站的詳細資訊，請參閱[建立及部署 ASP.NET 網站，並使用 Visual Studio SQL Database](https://docs.microsoft.com/dotnet/azure/)。 該教學課程也會示範如何使用 Entity Framework Code First 移轉將您的 SQL Server 資料庫部署至 Windows Azure SQL Database （先前稱為 SQL Azure）。
>
> 本教學課程是由 Rick Anderson （ [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ）撰寫。

## <a name="what-youll-build"></a>您要建置的內容

> [!NOTE]
> 如果本教學[課程](../../getting-started/introduction/getting-started.md)可在此使用[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)，則為更新版本。 新的教學課程會使用 ASP.NET MVC 5，這在此教學課程中提供了許多改進功能。

您將會執行簡單的電影清單應用程式，以支援從資料庫建立、編輯、搜尋和列出電影。 以下是您將建立之應用程式的兩個螢幕擷取畫面。 其中包含的頁面會顯示資料庫中的電影清單：

![](intro-to-aspnet-mvc-4/_static/image1.png)

應用程式也可讓您新增、編輯和刪除電影，以及查看個別資料的詳細資訊。 所有的資料輸入案例都包含驗證，以確保資料庫中儲存的資料是正確的。

![](intro-to-aspnet-mvc-4/_static/image2.png)

## <a name="getting-started"></a>快速入門

從執行 Visual Studio Express 2012 或 Visual Web Developer 2010 Express 開始。 此系列中的大部分螢幕擷取畫面都會使用 Visual Studio Express 2012，但您可以使用 Visual Studio 2010/SP1、Visual Studio 2012、Visual Studio Express 2012 或 Visual Web Developer 2010 Express 來完成本教學課程。 從 [**開始**] 頁面選取 [**新增專案**]。

Visual Studio 是 IDE 或整合式開發環境。 就像您使用 Microsoft Word 來撰寫檔一樣，您將使用 IDE 來建立應用程式。 在 Visual Studio 上方會有一個工具列，其中顯示您可以使用的各種選項。 另外還有一個功能表，可提供另一種在 IDE 中執行工作的方式。 （例如，您可以使用功能表，然後選取 [檔案] &gt; [**新增專案**]，而不是從 [**開始**]**頁面選取 [** **新增專案**]。）

![](intro-to-aspnet-mvc-4/_static/image3.png)

## <a name="creating-your-first-application"></a>建立您的第一個應用程式

您可以使用 Visual Basic 或 Visual C#作為程式設計語言來建立應用程式。 選取左側C#的 [視覺效果]，然後選取 [ **ASP.NET MVC 4 Web 應用程式**]。 將專案命名為 &quot;MvcMovie&quot; 然後按一下 **[確定]** 。

![](intro-to-aspnet-mvc-4/_static/image4.png)

在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [**網際網路應用程式**]。 保留**Razor**做為預設的 view engine。

![](intro-to-aspnet-mvc-4/_static/image5.png)

按一下 [確定]。 Visual Studio 使用您剛建立的 ASP.NET MVC 專案的預設範本，所以您現在有一個可運作的應用程式，而不需要執行任何動作！ 這是簡單的 &quot;Hello World！&quot; 專案，這是啟動應用程式的好地方。

![](intro-to-aspnet-mvc-4/_static/image6.png)

從 [偵錯] 功能表中，選取 [開始偵錯]。

![](intro-to-aspnet-mvc-4/_static/image7.png)

請注意，啟動偵錯工具的鍵盤快速鍵是 F5。

F5 會使 Visual Studio 開始 IIS Express 並執行您的 web 應用程式。 Visual Studio 接著會啟動瀏覽器，並開啟應用程式的首頁。 請注意，瀏覽器的網址列會顯示 `localhost`，而不是類似 `example.com`。 這是因為 `localhost` 一定會指向您自己的本機電腦，在此情況下，它會執行您剛建立的應用程式。 當 Visual Studio 執行 Web 專案時，會針對網頁伺服器使用隨機埠。 在下圖中，埠號碼為41788。 當您執行應用程式時，可能會看到不同的埠號碼。

![](intro-to-aspnet-mvc-4/_static/image8.png)

現成的預設範本會提供您首頁、連絡人和頁面。 它也提供註冊和登入的支援，以及 Facebook 和 Twitter 的連結。 下一步是變更此應用程式的運作方式，並稍微瞭解 ASP.NET MVC。 關閉瀏覽器，讓我們變更一些程式碼。

> [!div class="step-by-step"]
> [下一個](adding-a-controller.md)
