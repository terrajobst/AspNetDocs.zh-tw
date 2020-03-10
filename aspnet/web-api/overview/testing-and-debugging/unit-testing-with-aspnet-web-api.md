---
uid: web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
title: 單元測試 ASP.NET Web API 2 |Microsoft Docs
author: Rick-Anderson
description: 本指引和應用程式會示範如何為您的 Web API 2 應用程式建立簡單的單元測試。 本教學課程示範如何包含單元測試的 [proj] 。
ms.author: riande
ms.date: 06/05/2014
ms.assetid: bf20f78d-ff91-48be-abd1-88e23dcc70ba
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: f2d60b977475e048a3a74aabff4adc768ee22baf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554968"
---
# <a name="unit-testing-aspnet-web-api-2"></a>單元測試 ASP.NET Web API 2

由[Tom FitzMacken](https://github.com/tfitzmac)

[下載已完成的專案](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> 本指引和應用程式會示範如何為您的 Web API 2 應用程式建立簡單的單元測試。 本教學課程會示範如何在您的方案中包含單元測試專案，以及撰寫可從控制器方法檢查傳回值的測試方法。
>
> 本教學課程假設您已熟悉 ASP.NET Web API 的基本概念。 如需入門教學課程，請參閱[使用 ASP.NET Web API 2 的消費者入門](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)。
>
> 本主題中的單元測試會刻意限制為簡單的資料案例。 如需單元測試更先進的資料案例，請參閱[當單元測試 ASP.NET Web API 2 時的模擬 Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Web API 2

## <a name="in-this-topic"></a>本主題內容

本主題包含下列各節：

- [必要條件](#prereqs)
- [下載程式代碼](#download)
- [使用單元測試專案建立應用程式](#appwithunittest)
    - [建立應用程式時加入單元測試專案](#whencreate)
    - [將單元測試專案加入至現有的應用程式](#addtoexisting)
- [設定 Web API 2 應用程式](#setupproject)
- [在測試專案中安裝 NuGet 套件](#testpackages)
- [建立測試](#tests)
- [執行測試](#runtests)

<a id="prereqs"></a>
## <a name="prerequisites"></a>Prerequisites

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)社區、Professional 或 Enterprise edition

<a id="download"></a>
## <a name="download-code"></a>下載程式碼

下載[已完成的專案](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)。 可下載的專案包含本主題的單元測試程式碼，以及[單元測試 ASP.NET Web API 主題時的模擬 Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) 。

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a>使用單元測試專案建立應用程式

建立應用程式或將單元測試專案加入至現有的應用程式時，您可以建立單元測試專案。 本教學課程會顯示兩種建立單元測試專案的方法。 若要遵循本教學課程，您可以使用任一種方法。

<a id="whencreate"></a>
### <a name="add-unit-test-project-when-creating-the-application"></a>建立應用程式時加入單元測試專案

建立名為**StoreApp**的新 ASP.NET Web 應用程式。

![建立專案](unit-testing-with-aspnet-web-api/_static/image1.png)

在 [新增 ASP.NET 專案] 視窗中，選取 [**空白**] 範本，並新增 Web API 的 [資料夾] 和 [核心參考]。 選取 [**加入單元測試**] 選項。 單元測試專案會自動命名為**StoreApp**。 您可以保留此名稱。

![建立單元測試專案](unit-testing-with-aspnet-web-api/_static/image2.png)

建立應用程式之後，您會看到它包含兩個專案。

![兩個專案](unit-testing-with-aspnet-web-api/_static/image3.png)

<a id="addtoexisting"></a>
### <a name="add-unit-test-project-to-an-existing-application"></a>將單元測試專案加入至現有的應用程式

如果您在建立應用程式時沒有建立單元測試專案，您可以隨時加入一個。 例如，假設您已經有一個名為 StoreApp 的應用程式，而且您想要加入單元測試。 若要加入單元測試專案，請以滑鼠右鍵按一下您的方案，然後選取 [**加入**] 和 [**新增專案**]。

![將新專案新增至方案](unit-testing-with-aspnet-web-api/_static/image4.png)

在左窗格中選取 [**測試**]，然後選取專案類型的 [**單元測試專案**]。 將專案命名為**StoreApp**。

![加入單元測試專案](unit-testing-with-aspnet-web-api/_static/image5.png)

您會在方案中看到單元測試專案。

在單元測試專案中，將專案參考加入至原始專案。

<a id="setupproject"></a>
## <a name="set-up-the-web-api-2-application"></a>設定 Web API 2 應用程式

在您的 StoreApp 專案中，將類別檔案新增至名為**Product.cs**的 [**模型**] 資料夾。 以下列程式碼取代檔案的內容。

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample1.cs)]

建置方案。

以滑鼠右鍵按一下 [控制器] 資料夾，然後選取 [**加入**] 和 [**新增 scaffold 專案**]。 選取 [ **WEB API 2 控制器-空白**]。

![加入新的控制器](unit-testing-with-aspnet-web-api/_static/image6.png)

將控制器名稱設定為**SimpleProductController**，然後按一下 [**新增**]。

![指定控制器](unit-testing-with-aspnet-web-api/_static/image7.png)

將現有的程式碼取代為下列程式碼。 為了簡化此範例，資料會儲存在清單中，而不是資料庫中。 此類別中定義的清單代表生產資料。 請注意，控制器包含一個可接受產品物件清單做為參數的函式。 這個函數可讓您在單元測試時傳遞測試資料。 控制器也包含兩個**非同步**方法，以說明單元測試的非同步方法。 這些非同步方法的執行方式是呼叫**system.threading.tasks.task.fromresult**來將無關的程式碼降到最低，但通常方法會包含需要大量資源的作業。

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample2.cs)]

GetProduct 方法會傳回**應傳回 iHTTPactionresult**介面的實例。 應傳回 iHTTPactionresult 是 Web API 2 中的其中一項新功能，可簡化單元測試的開發。 實應傳回 iHTTPactionresult 介面的類別可在[system.web. HTTP.sys](https://msdn.microsoft.com/library/system.web.http.results.aspx)命名空間中找到。 這些類別代表動作要求的可能回應，並對應至 HTTP 狀態碼。

建置方案。

您現在已準備好設定測試專案。

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a>在測試專案中安裝 NuGet 套件

當您使用空白範本來建立應用程式時，單元測試專案（StoreApp）不會包含任何已安裝的 NuGet 套件。 其他範本，例如 Web API 範本，則會在單元測試專案中包含一些 NuGet 套件。 在本教學課程中，您必須在測試專案中包含 Microsoft ASP.NET Web API 2 核心套件。

以滑鼠右鍵按一下 [StoreApp] 專案，然後選取 [**管理 NuGet 套件**]。 您必須選取 [StoreApp] 專案，才能將封裝加入至該專案。

![管理封裝](unit-testing-with-aspnet-web-api/_static/image8.png)

尋找並安裝 Microsoft ASP.NET Web API 2 核心套件。

![安裝 web api 核心套件](unit-testing-with-aspnet-web-api/_static/image9.png)

關閉 [管理 NuGet 封裝] 視窗。

<a id="tests"></a>
## <a name="create-tests"></a>建立測試

根據預設，您的測試專案會包含名為 UnitTest1.cs 的空白測試檔案。 此檔案會顯示您用來建立測試方法的屬性。 針對單元測試，您可以使用此檔案，或建立您自己的檔案。

![Unittest1.cpp](unit-testing-with-aspnet-web-api/_static/image10.png)

在本教學課程中，您將建立自己的測試類別。 您可以刪除 UnitTest1.cs 檔案。 新增名為**TestSimpleProductController.cs**的類別，並將程式碼取代為下列程式碼。

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample3.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a>執行測試

您現在已準備好執行測試。 所有以**TestMethod**屬性標記的方法都會進行測試。 從 [**測試**] 功能表項目執行測試。

![執行測試](unit-testing-with-aspnet-web-api/_static/image11.png)

開啟 [**測試瀏覽器**] 視窗，並注意測試的結果。

![測試結果](unit-testing-with-aspnet-web-api/_static/image12.png)

## <a name="summary"></a>總結

您已經完成此教學課程。 本教學課程中的資料已刻意簡化，著重于單元測試條件。 如需單元測試更先進的資料案例，請參閱[當單元測試 ASP.NET Web API 2 時的模擬 Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)。
