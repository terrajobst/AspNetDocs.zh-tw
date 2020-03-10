---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: NerdDinner 教學課程簡介 |Microsoft Docs
author: shanselman
description: 學習新架構的最佳方式是使用它來建立一些專案。 本教學課程逐步解說如何使用 ASP.NE 建立一個小型但完整的應用程式 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 154cfe6694cf723c0a1f8e33bfdb42c97594518f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580574"
---
# <a name="introducing-the-nerddinner-tutorial"></a>NerdDinner 教學課程簡介

由[Scott Hanselman](https://github.com/shanselman)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 學習新架構的最佳方式是使用它來建立一些專案。 本教學課程逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的應用程式，並介紹其背後的一些核心概念。
> 
> 如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。

## <a name="nerddinner-tutorial"></a>NerdDinner 教學課程

學習新架構的最佳方式是使用它來建立一些專案。 本教學課程逐步解說如何使用 ASP.NET MVC 建立一個小型但完整的應用程式，並介紹其背後的一些核心概念。

我們即將建立的應用程式稱為「NerdDinner」。 NerdDinner 提供一種簡單的方式，讓人們能夠在線上尋找和組織 dinners：

![](introducing-the-nerddinner-tutorial/_static/image1.png)

NerdDinner 可讓已註冊的使用者建立、編輯和刪除 dinners。 它會在整個應用程式中強制執行一組一致的驗證和商務規則：

![](introducing-the-nerddinner-tutorial/_static/image2.png)

訪客可以使用以 AJAX 為基礎的對應來搜尋即將保留的 dinners：

![](introducing-the-nerddinner-tutorial/_static/image3.png)

按一下晚餐會將他們帶到詳細資料頁面，讓他們深入瞭解：

![](introducing-the-nerddinner-tutorial/_static/image4.png)

如果他們有興趣參加晚餐，他們可以在網站上登入或註冊：

![](introducing-the-nerddinner-tutorial/_static/image5.png)

他們可以按一下以 AJAX 為基礎的 RSVP 連結來參加活動：

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a>執行 NerdDinner

我們即將開始我們的 NerdDinner 應用程式，方法是使用 Visual Studio 內的檔案&gt;[新增專案] 命令，建立全新的 ASP.NET MVC 專案。 然後，我們會以累加方式新增功能和功能。 在本文中，我們將討論：

1. [如何建立新的 ASP.NET MVC 專案](create-a-new-aspnet-mvc-project.md)
2. [如何建立資料庫](create-a-database.md)
3. [如何使用商務規則驗證來建立模型](build-a-model-with-business-rule-validations.md)
4. [如何使用控制器和 views 來執行清單/詳細資料 UI](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [如何提供 CRUD （建立、讀取、更新、刪除）資料表單專案支援](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [如何使用 ViewData 和執行 ViewModel 類別](use-viewdata-and-implement-viewmodel-classes.md)
7. [如何使用主版頁面和部分重新使用 UI](re-use-ui-using-master-pages-and-partials.md)
8. [如何實行有效率的資料分頁](implement-efficient-data-paging.md)
9. [如何使用驗證和授權保護應用程式](secure-applications-using-authentication-and-authorization.md)
10. [如何使用 AJAX 傳遞動態更新](use-ajax-to-deliver-dynamic-updates.md)
11. [如何使用 AJAX 來執行對應案例](use-ajax-to-implement-mapping-scenarios.md)
12. [如何啟用自動化單元測試](enable-automated-unit-testing.md)

您可以完成本章節逐步解說的每個步驟，從頭建立自己的 NerdDinner 複本。 或者，您可以在這裡下載原始程式碼的完整版本： [GitHub 上的 NerdDinner](https://github.com/AspNetMVPSamples/NerdDinner)。 如果您想要離線閱讀本教學課程，您也可以選擇性地[下載本教學課程的免費 PDF 版本](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)。

您可以使用 Visual Studio 2008 或免費的 Visual Web Developer 2008 Express 來建立應用程式。 您可以使用 SQL Server 或資料庫的免費 SQL Server Express。

您可以使用[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)的 V2 安裝 ASP.NET MVC、Visual Web Developer 2008 Express 和 SQL Server Express （所有免費）

### <a name="now-lets-get-started"></a>現在讓我們開始吧 。

既然我們已經討論過什麼 NerdDinner，讓我們來匯總卷起袖子並撰寫一些程式碼。

我們會先使用 Visual Studio 中的檔案&gt;新專案來建立 NerdDinner 應用程式。

> [!div class="step-by-step"]
> [下一個](create-a-new-aspnet-mvc-project.md)
