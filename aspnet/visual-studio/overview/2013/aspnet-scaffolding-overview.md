---
uid: visual-studio/overview/2013/aspnet-scaffolding-overview
title: Visual Studio 2013 中的 ASP.NET 架構 |Microsoft Docs
author: Rick-Anderson
description: ASP.NET 的樣板是包含在 Visual Studio 2013 中的新功能。
ms.author: riande
ms.date: 04/09/2014
ms.assetid: a41ec9d4-8287-4f31-9e2a-460e7b7f04be
msc.legacyurl: /visual-studio/overview/2013/aspnet-scaffolding-overview
msc.type: authoredcontent
ms.openlocfilehash: cf4669b769cee28475e2dd6a6ddf07ea1434d04d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557978"
---
# <a name="aspnet-scaffolding-in-visual-studio-2013"></a>Visual Studio 2013 中的 ASP.NET Scaffold

由[Tom FitzMacken](https://github.com/tfitzmac)

> ASP.NET 的樣板是包含在 Visual Studio 2013 中的新功能。

## <a name="overview"></a>概觀

ASP.NET 樣板是用於 ASP.NET Web 應用程式的程式碼產生架構。 Visual Studio 2013 包括適用于 MVC 和 Web API 專案的預先安裝程式碼產生器。 當您想要快速加入與資料模型互動的程式碼時，您可以將樣板加入至專案。 使用樣板可以減少在專案中開發標準資料作業的時間量。

根據預設，Visual Studio 2013 不支援產生 Web form 專案的程式碼，但您可以透過將 MVC 相依性新增至專案或安裝延伸模組，將樣板與 Web form 搭配使用。 這兩種方法如下所示。

Visual Studio 2013 Update 2 （目前為 RC）可讓您擴充 ASP.NET 的架構，以符合您的案例需求。 透過這種功能，您可以建立自訂的樣板範本，並將其新增至 [加入新的 Scaffold] 對話方塊。 在自訂範本內，您可以指定加入 scaffold 專案時所產生的程式碼。 如需詳細資訊，請參閱[建立 Visual Studio 的自訂 Scaffolder](https://go.microsoft.com/fwlink/p/?LinkId=395029)。

## <a name="prerequisites"></a>Prerequisites

若要使用 ASP.NET 的架構，您必須具有：

- Microsoft Visual Studio 2013
- Web 開發人員工具（預設 Visual Studio 2013 安裝的一部分）
- ASP.NET Web 架構和工具2013（預設 Visual Studio 2013 安裝的一部分）

## <a name="add-a-scaffolded-item-to-mvc-or-web-api"></a>將 scaffold 專案新增至 MVC 或 Web API

若要加入 scaffold，請以滑鼠右鍵按一下專案中的專案或資料夾，**然後選取 [** 新增]-[**新的 scaffold 專案**]，如下圖所示。

![新增 scaffold 專案](aspnet-scaffolding-overview/_static/image1.png)

從 [**新增 Scaffold** ] 視窗中，選取要新增的 Scaffold 類型。

![選取 scaffold 類型](aspnet-scaffolding-overview/_static/image2.png)

[**新增控制器**] 視窗可讓您選擇產生控制器的選項，包括是否要使用 Entity Framework 6 的新異步功能。

![新增控制器](aspnet-scaffolding-overview/_static/image3.png)

系統會為您的案例建立相關的類別和頁面。 例如，下圖顯示透過名為「電影」之模型類別的樣板所建立的 MVC 控制器和 views。

![建立的檔案](aspnet-scaffolding-overview/_static/image4.png)

## <a name="add-a-scaffolded-item-to-web-forms"></a>將 scaffold 專案新增至 Web Forms

若要加入產生 Web form 程式碼的樣板，您必須安裝延伸模組以 Visual Studio 或加入 MVC 相依性。 這兩種方法如下所示，但您只需要執行其中一種方法。

### <a name="web-forms-scaffolding-extension"></a>Web Forms 樣板延伸模組

您可以安裝 Visual Studio 延伸模組，讓您使用具有 Web form 專案的樣板。 在 Visual Studio 中，依序選取 [**工具**] 和 [**擴充功能和更新**]。 從這個對話方塊中，搜尋**Web**form 樣板的 Visual Studio 資源庫。

![安裝 web forms 樣板](aspnet-scaffolding-overview/_static/image5.png)

如需詳細資訊，請參閱[Web Forms](https://go.microsoft.com/fwlink/p/?LinkId=396478)樣板。

### <a name="mvc-dependencies"></a>MVC 相依性

若**要新增 MVC**相依性，請選取 [新增 - 新的**scaffold 專案**]。 在 [新增 Scaffold] 視窗中，選取 [ **MVC**相依性]，如下所示。

![新增 MVC 相依性](aspnet-scaffolding-overview/_static/image6.png)

有兩個適用于樣板 MVC 的選項;最小和完整。 如果您選取 [最低]，則只會將 ASP.NET MVC 的 NuGet 套件和參考新增至您的專案。 如果您選取 [完整] 選項，則會加入最少的相依性，以及 MVC 專案所需的內容檔案。 若要輕鬆使用樣板，請選取 [完整相依性]。

![選取 [完整相依性]](aspnet-scaffolding-overview/_static/image7.png)

新增相依性之後，您會**看到 readme.txt 檔案**。 請仔細遵循此檔案中的指示，以確保您的專案能正常運作。

當您完成了 readme.txt 檔案中的步驟時，您可以新增 scaffold 專案，如上一節中的 MVC 和 Web API 所示。 自動產生的視圖和控制器將會在您的專案中正常運作。

## <a name="tutorials"></a>教學課程

若要建立自訂 scaffolder，請參閱[建立 Visual Studio 的自訂 scaffolder](https://go.microsoft.com/fwlink/p/?LinkId=395029)。

若要自訂產生的檔案，請參閱[如何從新的 Scaffold 專案自訂產生的檔案對話方塊](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx)。

如需搭配**Database First 開發**使用架構的範例，請參閱[使用 ASP.NET MVC 的 EF Database First](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md)。

如需在**mvc**專案中使用樣板的範例，請參閱[使用 ASP.NET mvc 5 的消費者入門](../../../mvc/overview/getting-started/introduction/getting-started.md)。

如需在**WEB api**專案中使用樣板的範例，請參閱使用[web api 2 中的屬性路由建立 REST API](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md)。
