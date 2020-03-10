---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
title: 第1部分：檔案 > 新專案 |Microsoft Docs
author: JoeStagner
description: 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第1部分涵蓋總覽和檔案/新增專案。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 15d4652b-d5aa-4172-b186-2c7f96ba316d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
msc.type: authoredcontent
ms.openlocfilehash: 05a3ace3d8fef9c1f3593f7948e42b4725d70134
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78636126"
---
# <a name="part-1-file--new-project"></a>第1部分：檔案 > 的新專案

依[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 示範為 .NET 平臺建立功能強大、可擴充的應用程式有多麼簡單。 它會說明如何使用 ASP.NET 4 中的絕佳新功能來建立線上商店，包括購物、結帳和管理。
> 
> 本教學課程系列詳細說明建立 Tailspin Spyworks 範例應用程式所採取的所有步驟。 第1部分涵蓋總覽和檔案/新增專案。

## <a id="_Toc260221666"></a>簡要

本教學課程是 ASP.NET WebForms 的簡介。 我們會開始變慢，因此新手層級的 網頁程式開發體驗也沒關係。

我們將建立的應用程式是簡單的線上商店。

![](tailspin-spyworks-part-1/_static/image1.jpg)

訪客可以依類別流覽產品：

![](tailspin-spyworks-part-1/_static/image2.jpg)

他們可以查看單一產品，並將其新增至其購物車：

![](tailspin-spyworks-part-1/_static/image3.jpg)

他們可以審查其購物車，移除任何不再需要的專案：

![](tailspin-spyworks-part-1/_static/image4.jpg)

繼續簽出將會提示他們

![](tailspin-spyworks-part-1/_static/image5.jpg)

![](tailspin-spyworks-part-1/_static/image6.jpg)

排序之後，他們會看到簡單的確認畫面：

![](tailspin-spyworks-part-1/_static/image7.jpg)

我們將從在 Visual Studio 2010 中建立新的 ASP.NET WebForms 專案開始，並以累加方式新增功能，以建立完整的運作中應用程式。 在此過程中，我們將討論資料庫存取、清單和方格的觀點、資料更新頁面、資料驗證、使用主版頁面進行一致的頁面配置、AJAX、驗證、使用者成員資格等等。

您可以依照步驟進行，也可以從[http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)下載已完成的應用程式。

您可以從[https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/)使用 Visual Studio 2010 或免費的 Visual Web Developer 2010。 若要建立應用程式，您可以使用 SQL Server 或免費 SQL Server Express 來裝載資料庫。

## <a id="_Toc260221667"></a>檔案/新增專案

我們會從 Visual Studio 的 [檔案] 功能表中選取新的專案開始。 這會顯示 [新增專案] 對話方塊。

![](tailspin-spyworks-part-1/_static/image8.jpg)

我們將選取左側的C# [視覺效果/Web 範本] 群組，然後選擇 [中間] 資料行中的 [ASP.NET Web 應用程式] 範本。 將專案命名為 TailspinSpyworks，然後按下 [確定] 按鈕。

![](tailspin-spyworks-part-1/_static/image9.jpg)

這會建立我們的專案。 讓我們來看看應用程式中包含在右側方案總管中的資料夾。

![](tailspin-spyworks-part-1/_static/image10.jpg)

空白解決方案不完全空白–它會新增基本資料夾結構：

![](tailspin-spyworks-part-1/_static/image1.png)

請注意 ASP.NET 4 預設專案範本所執行的慣例。

- 「帳戶」資料夾會為 ASP 實行基本的使用者介面。NET 的成員資格子系統。
- 「腳本」資料夾可作為用戶端 JavaScript 檔案的存放庫，而核心 jQuery .js 檔預設為可用。
- 「樣式」資料夾是用來組織我們的網站視覺效果（CSS 樣式表單）

當我們按 F5 執行應用程式並轉譯 default.aspx 頁面時，我們會看到下列畫面。

![](tailspin-spyworks-part-1/_static/image11.jpg)

我們的第一個應用程式增強功能是將預設 WebForms 範本中的 Style .css 檔案取代成 CSS 類別和相關聯的影像檔案，這些檔案將會轉譯我們的 Tailspin Spyworks 應用程式所需的視覺效果 asthetics。

這麼做之後，default.aspx 頁面就會呈現如下。

![](tailspin-spyworks-part-1/_static/image12.jpg)

請注意頁面右上方的影像連結，以及已新增至主版頁面的功能表項目。 只有「登入」和「帳戶」連結會指向存在的頁面（由預設範本所產生），以及我們在建立應用程式時將會執行的其餘頁面。

我們也要將主版頁面重新放置到 [樣式] 目錄。 雖然這只是偏好的喜好設定，但如果我們決定讓我們的應用程式在未來「skinable」，則可能會變得更容易。

這麼做之後，我們需要變更預設 ASP.NET WebForms 頁面所產生之所有 .aspx 檔案中的主版頁面參考。

> [!div class="step-by-step"]
> [下一個](tailspin-spyworks-part-2.md)
