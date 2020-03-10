---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-1
title: 搭配 Entity Framework 6 使用 Web API 2 |Microsoft Docs
author: MikeWasson
description: 本教學課程將告訴您使用 ASP.NET Web API 後端建立 web 應用程式的基本概念。 本教學課程使用 Entity Framework 6 來進行資料佈局 。
ms.author: riande
ms.date: 01/17/2019
ms.assetid: e879487e-dbcd-4b33-b092-d67c37ae768c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-1
msc.type: authoredcontent
ms.openlocfilehash: 0f5dc960f494af5bd4ce87863a510d1892319908
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622476"
---
# <a name="using-web-api-2-with-entity-framework-6"></a>使用 Web API 2 和 Entity Framework 6

[下載已完成的專案](https://github.com/MikeWasson/BookService)

> 本教學課程會教您使用 ASP.NET Web API 後端建立 web 應用程式的基本概念。 本教學課程使用資料層的 Entity Framework 6，以及用戶端 JavaScript 應用程式的挖式 .js。 本教學課程也會說明如何將應用程式部署至 Azure App Service Web Apps。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
>
> - Web API 2。1
> - Visual Studio 2017 （請[在這裡](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)下載 Visual Studio 2017）
> - Entity Framework 6
> - .NET 4.7
> - [挖的 .js](http://knockoutjs.com/) 3。1

本教學課程使用 ASP.NET Web API 2 與 Entity Framework 6 來建立 Web 應用程式，以操作後端資料庫。 以下是您將建立之應用程式的螢幕擷取畫面。

[![](part-1/_static/image2.png)](part-1/_static/image1.png)

應用程式會使用單一頁面應用程式（SPA）設計。 「單頁應用程式」是 web 應用程式的一般詞彙，它會載入單一 HTML 頁面，然後動態更新頁面，而不是載入新的頁面。 載入初始頁面之後，應用程式會透過 AJAX 要求與伺服器交談。 AJAX 要求會傳回 JSON 資料，應用程式會使用它來更新 UI。

AJAX 並不是新的，但目前有 JavaScript 架構可讓您更輕鬆地建立和維護大型的 SPA 應用程式。 本教學課程使用了[挖的 .js](http://knockoutjs.com/)，但是您可以使用任何 JavaScript 用戶端架構。

以下是此應用程式的主要組建區塊：

- ASP.NET MVC 會建立 HTML 網頁。
- ASP.NET Web API 會處理 AJAX 要求並傳回 JSON 資料。
- 挖式 .js 資料-將 HTML 元素系結至 JSON 資料。
- Entity Framework 與資料庫交談。

## <a name="see-this-app-running-on-azure"></a>請參閱此應用程式在 Azure 上執行

您是否想要查看已完成的網站以即時 web 應用程式的形式執行？ 您可以選取下列按鈕，將完整版的應用程式部署到您的 Azure 帳戶。

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/BookService)

您需要 Azure 帳戶，才能將此解決方案部署至 Azure。 如果您還沒有帳戶，您可以使用下列選項：

- [免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-您將取得可試用付費 azure 服務的額度，且即使在用完後，您仍可保留帳戶，並使用免費的 azure 服務。
- [啟用 msdn 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-您的 msdn 訂用帳戶每月會提供您額度，供您用於付費 Azure 服務。

## <a name="create-the-project"></a>建立專案

開啟 Visual Studio。 從 [**檔案**] 功能表中，選取 [**新增**]，然後選取 [**專案**]。 （或選取 [開始] 頁面上的 [**新增專案**]）。

在 **新增專案** 對話方塊中，選取左窗格中的  **web** ，然後在中間窗格中**ASP.NET web 應用程式（.NET Framework）** 。 將專案命名為**BookService** ，然後選取 **[確定]** 。

[![](part-1/_static/image11.png)](part-1/_static/image11.png)

在 [**新增 ASP.NET 專案**] 對話方塊中，選取 [ **Web API** ] 範本。

[![](part-1/_static/image12.png)](part-1/_static/image12.png)

選取 [確定] 建立專案。

## <a name="configure-azure-settings-optional"></a>設定 Azure 設定（選擇性）

建立專案之後，您可以隨時選擇部署至 Azure App Service Web Apps。 

1. 在方案總管中，以滑鼠右鍵按一下您的專案，然後選取 [**發佈**]。

2. 在出現的視窗中，選取 [**啟動**]。 [**挑選發行目標**] 對話方塊隨即出現。

   [![](part-1/_static/image14.png)](part-1/_static/image14.png)

3. 選取 [建立設定檔]。 [建立 App Service] 對話方塊隨即出現。

   [![](part-1/_static/image15.png)](part-1/_static/image15.png)

   接受預設值，或為應用程式名稱、資源群組、主控方案、Azure 訂用帳戶和地理區域輸入不同的值。 

4. 選取 **[建立 SQL database**]。 [**設定 SQL Server** ] 對話方塊隨即出現。 

   [![](part-1/_static/image16.png)](part-1/_static/image16.png)

   接受預設值，或輸入不同的值。 輸入新資料庫的**系統管理員使用者名稱**和**系統管理員密碼**。 當您完成時，請選取 **[確定]** 。 [**建立 App Service** ] 頁面隨即重新出現。

5. 選取 [**建立**] 以建立您的設定檔。 右下角會出現一則訊息，指出部署正在進行中。 一小段時間之後，[**發行**] 視窗隨即重新出現。

    [![](part-1/_static/image17.png)](part-1/_static/image17.png)
   
    您建立用來部署應用程式的設定檔現已推出。 

> [!div class="step-by-step"]
> [下一個](part-2.md)
