---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 簡介（VB） |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，也就是 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: a1b3d789-93b4-487f-b90d-80c9c9b4f8fa
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: 24f7de303ef7f5a457bd509ecc6bd0e3be7e3d9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78599894"
---
# <a name="intro-to-aspnet-mvc-3-vb"></a>ASP.NET MVC 3 簡介 (VB)

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，這是 Microsoft Visual Studio 的免費版本。 開始之前，請先確定您已安裝下列必要條件。 您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，您可以使用下列連結個別安裝必要條件：
> 
> - [Visual Studio Web Developer Express SP1 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）
> 
> 如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主題提供具有 VB.NET 原始程式碼的 Visual Web Developer 專案。 [下載 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您想C#要的話，請切換到本教學課程的[ C#版本](../cs/intro-to-aspnet-mvc-3.md)。

本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，這是 Microsoft Visual Studio 的免費版本。 開始之前，請先確定您已安裝下列必要條件。 您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，您可以使用下列連結個別安裝必要條件：

- [Visual Studio Web Developer Express SP1 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）

如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。

本主題提供具有 VB 原始程式碼的 Visual Web Developer 專案。 請[在這裡下載 VB 版本](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824)。 如果您偏好使用 CSharp，請切換到本教學課程的[CSharp 版本](../cs/intro-to-aspnet-mvc-3.md)。

## <a name="what-youll-build"></a>您要建置的內容

您將會執行簡單的電影清單應用程式，以支援從資料庫建立、編輯和列出電影。 以下是您將建立之應用程式的兩個螢幕擷取畫面。 其中包含的頁面會顯示資料庫中的電影清單：

[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)

應用程式也可讓您新增、編輯和刪除電影，以及查看個別資料的詳細資訊。 所有的資料輸入案例都包含驗證，以確保資料庫中儲存的資料是正確的。

[![CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="skills-youll-learn"></a>您要學習的技術

以下是您要學習的內容：

- 如何建立新的 ASP.NET MVC 專案
- 如何使用 Entity Framework 程式碼優先建立新的資料庫
- 如何建立 ASP.NET MVC 控制器和 views
- 如何取出和顯示資料
- 如何編輯資料並啟用資料驗證

## <a name="getting-started"></a>快速入門

一開始先執行 Visual Web Developer 2010 Express （簡稱 "VWD"），然後從 [**開始**] 頁面選取 [**新增專案**]。

Visual Web Developer 是一個 IDE 或一個整合式開發環境。 就像您使用 Microsoft Word 來撰寫檔一樣，您將使用 IDE 來建立應用程式。 在 Visual Web Developer 中，有一個工具列沿著上方顯示各種可用的選項。 另外還有一個功能表，可提供另一種在 IDE 中執行工作的方式。 （例如，您可以使用功能表，然後選取 [檔案] &gt; [**新增專案**]，而不是從 [**開始**]**頁面選取 [** **新增專案**]。）

[![](intro-to-aspnet-mvc-3/_static/image6.png)](intro-to-aspnet-mvc-3/_static/image5.png)

## <a name="creating-your-first-application"></a>建立您的第一個應用程式

您可以使用您選擇的 Visual Basic 或視覺效果C#做為程式設計語言來建立應用程式。 在本教學課程中，請選取左側的 [Visual Basic]，然後選取 [ **ASP.NET MVC 3 Web 應用程式**]。 將專案命名為 "MvcMovie"，然後按一下 **[確定]** 。

![1NewMVCproj_sm](intro-to-aspnet-mvc-3/_static/image7.png)

在 [**新增 ASP.NET MVC 3 專案**] 對話方塊中，選取 [**網際網路應用程式**]。 保留**Razor**做為預設的 view engine。

![1InternetAppRazor_SM](intro-to-aspnet-mvc-3/_static/image8.png)

按一下 [確定]。 Visual Web Developer 已針對您剛才建立的 ASP.NET MVC 專案使用預設範本，因此您現在有一個可運作的應用程式，而不需要執行任何動作！ 這是簡單的「Hello World！」 專案，這是啟動應用程式的好地方。

[![](intro-to-aspnet-mvc-3/_static/image10.png)](intro-to-aspnet-mvc-3/_static/image9.png)

從 [偵錯] 功能表中，選取 [開始偵錯]。

![](intro-to-aspnet-mvc-3/_static/image11.png)

請注意，啟動偵錯工具的鍵盤快速鍵是 F5。

F5 會使 Visual Web Developer 啟動開發 web 伺服器，並執行您的 web 應用程式。 VWD 接著會啟動瀏覽器，並開啟應用程式的首頁。 請注意，瀏覽器的網址列會顯示 `localhost`，而不是類似 `example.com`。 這是因為 `localhost` 一定會指向您自己的本機電腦，在此情況下，它會執行您剛建立的應用程式。 當 VWD 執行 Web 專案時，專案會使用隨機埠。 在下圖中，隨機埠號碼為43246。 您的專案可能會使用不同的埠號碼。

![](intro-to-aspnet-mvc-3/_static/image12.png)

現成的預設範本會提供您兩個要造訪的頁面和一個基本的登入頁面。 讓我們來變更此應用程式的運作方式，並稍微瞭解如何在進程中 ASP.NET MVC。 關閉瀏覽器，讓我們變更一些程式碼。

> [!div class="step-by-step"]
> [下一個](adding-a-controller.md)
