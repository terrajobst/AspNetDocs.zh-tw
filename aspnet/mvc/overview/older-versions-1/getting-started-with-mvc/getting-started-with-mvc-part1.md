---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: ASP.NET MVC 簡介 |Microsoft Docs
author: shanselman
description: 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 建立可從資料庫讀取和寫入的簡單 web 應用程式。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: f8f0014776ba1313119e8c39c63a216b0fc864e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581582"
---
# <a name="intro-to-aspnet-mvc"></a>ASP.NET MVC 簡介

由[Scott Hanselman](https://github.com/shanselman)

> > [!NOTE]
> > 如果本教學[課程](../../getting-started/introduction/getting-started.md)可在此使用[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)，則為更新版本。 新的教學課程會使用 ASP.NET MVC 5，這在此教學課程中提供了許多改進功能。
>
>
> 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 您將建立可從資料庫讀取和寫入的簡單 web 應用程式。 請造訪[ASP.NET mvc 學習中心](../../../index.md)，以尋找其他 ASP.NET mvc 教學課程和範例。

讓我們使用[Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/)來製作第一個 ASP.NET MVC Web 應用程式。 我們將製作一個小電影清單的應用程式，讓我們建立和列出電影。

## <a name="what-youll-build"></a>您要建置的內容

以下是您將建立之應用程式的兩個螢幕擷取畫面。 您將會有一個具有各種資料行的簡單電影資料表。

[![電影清單-Windows Internet Explorer （12）](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)

您將會有一個建立表單，讓我們可以將電影加入清單中。

[![建立電影-Windows Internet Explorer （2）](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)

## <a name="skills-youll-learn"></a>您要學習的技術

本教學課程將告訴您使用 Visual Studio 建立 ASP.NET MVC Web 應用程式的基本概念。 您將了解：

- 如何建立新的 ASP.NET MVC 專案
- 如何使用 SQL Server 建立新的資料庫
- 如何建立 ASP.NET MVC 控制器和 Views
- 如何取出和顯示資料
- 如何編輯資料並啟用資料驗證
- 如何更新資料庫架構

## <a name="get-started"></a>開始使用

一開始先執行 Visual Web Developer 2010 Express （我會從現在稱為「VWD」），然後從 [開始] 畫面選取 [新增專案]。

Visual Web Developer 是一個 IDE，也是整合式開發人員環境。 就像您使用 Microsoft Word 來撰寫檔一樣，您將使用 IDE 來建立應用程式。 頂端還有一個工具列，其中顯示您可以使用的各種選項，以及您也可以用來選取檔案的功能表 |新增專案。

[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)

## <a name="creating-your-first-application"></a>建立您的第一個應用程式

您可以使用 Visual Basic 或視覺效果C#來建立應用程式。 現在，選取左側的C# [視覺效果]，然後挑選 [ASP.NET MVC 2 Web 應用程式]。 將您的專案命名為「電影」，然後按一下 [確定]。

[![新增專案](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)

右側是顯示應用程式中所有檔案和資料夾的方案總管。 中間的大視窗是您編輯程式碼，並花費大多數時間的地方。 Visual Studio 使用您剛建立的 ASP.NET MVC 專案的預設範本，所以您現在有一個可運作的應用程式，而不需要執行任何動作！ 這是簡單的「Hello World！ 專案，這是我們應用程式的好起點。

[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)

選取工具列上的 [播放] 按鈕。

![[偵錯]](getting-started-with-mvc-part1/_static/image11.png)

它是指向右側的綠色箭號，它會編譯您的程式，並在網頁瀏覽器中啟動您的應用程式。

*注意：您可以改為在鍵盤上按 F5，或從 [Debug] 功能表中選取 [Debug-&gt;開始偵錯工具]。*

這會導致 Visual Web Developer 啟動開發 web 伺服器，並執行 web 應用程式（不需要進行任何設定或手動步驟即可啟用）。 接著，它會啟動瀏覽器，並將它設定為流覽應用程式的首頁。 請注意，瀏覽器的網址列會顯示 "localhost"，而不是類似 example.com 的專案。 這是因為 localhost 一律會指向您自己的本機電腦，在此情況下，會執行我們剛才建立的應用程式。

[![首頁](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)

現成的預設範本會提供您兩個要造訪的頁面和一個基本的登入頁面。 讓我們來變更此應用程式的運作方式，並稍微瞭解如何在進程中 ASP.NET MVC。 關閉您的瀏覽器，並讓變更一些程式碼。

> [!div class="step-by-step"]
> [下一個](getting-started-with-mvc-part2.md)
