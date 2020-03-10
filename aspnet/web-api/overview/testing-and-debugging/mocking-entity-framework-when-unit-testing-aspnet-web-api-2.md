---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: 當單元測試 ASP.NET Web API 2 時模擬 Entity Framework |Microsoft Docs
author: Rick-Anderson
description: 本指引和應用程式示範如何為使用 Entity Framework 的 Web API 2 應用程式建立單元測試。 它會顯示如何修改 。
ms.author: riande
ms.date: 12/13/2013
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 258450107ee7443c4efd43a3b8e4851249745227
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555087"
---
# <a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a>單元測試 ASP.NET Web API 2 時的模擬 Entity Framework

由[Tom FitzMacken](https://github.com/tfitzmac)

[下載已完成的專案](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> 本指引和應用程式示範如何為使用 Entity Framework 的 Web API 2 應用程式建立單元測試。 它會顯示如何修改 scaffold 控制器，以啟用傳遞內容物件進行測試，以及如何建立可與 Entity Framework 搭配使用的測試物件。
>
> 如需使用 ASP.NET Web API 進行單元測試的簡介，請參閱[使用 ASP.NET Web API 2 進行單元測試](unit-testing-with-aspnet-web-api.md)。
>
> 本教學課程假設您已熟悉 ASP.NET Web API 的基本概念。 如需入門教學課程，請參閱[使用 ASP.NET Web API 2 的消費者入門](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)。
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
- [建立模型類別](#modelclass)
- [新增控制器](#controller)
- [新增相依性插入](#dependency)
- [在測試專案中安裝 NuGet 套件](#testpackages)
- [建立測試內容](#testcontext)
- [建立測試](#tests)
- [執行測試](#runtests)

如果您已完成[使用 ASP.NET Web API 2 進行單元測試](unit-testing-with-aspnet-web-api.md)中的步驟，您可以跳至[新增控制器](#controller)一節。

<a id="prereqs"></a>
## <a name="prerequisites"></a>Prerequisites

Visual Studio 2017 的社區、Professional 或 Enterprise edition

<a id="download"></a>
## <a name="download-code"></a>下載程式碼

下載[已完成的專案](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)。 可下載的專案包含本主題的單元測試程式碼和[單元測試 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)主題。

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a>使用單元測試專案建立應用程式

建立應用程式或將單元測試專案加入至現有的應用程式時，您可以建立單元測試專案。 本教學課程會示範如何在建立應用程式時建立單元測試專案。

建立名為**StoreApp**的新 ASP.NET Web 應用程式。

在 [新增 ASP.NET 專案] 視窗中，選取 [**空白**] 範本，並新增 Web API 的 [資料夾] 和 [核心參考]。 選取 [**加入單元測試**] 選項。 單元測試專案會自動命名為**StoreApp**。 您可以保留此名稱。

![建立單元測試專案](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

建立應用程式之後，您會看到它包含兩個專案- **StoreApp**和**StoreApp。測試**。

<a id="modelclass"></a>
## <a name="create-the-model-class"></a>建立模型類別

在您的 StoreApp 專案中，將類別檔案新增至名為**Product.cs**的 [**模型**] 資料夾。 以下列程式碼取代檔案的內容。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

建置方案。

<a id="controller"></a>
## <a name="add-the-controller"></a>新增控制器

以滑鼠右鍵按一下 [控制器] 資料夾，然後選取 [**加入**] 和 [**新增 scaffold 專案**]。 使用 [Entity Framework] 選取 [具有動作的 Web API 2 控制器]。

![加入新的控制器](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

設定下列的值：

- 控制器名稱： **ProductController**
- 模型類別：**產品**
- 資料內容類別： [選取**新的資料內容**] 按鈕，它會填入下列所示的值。

![指定控制器](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

按一下 [**新增**]，以自動產生的程式碼建立控制器。 此程式碼包含用來建立、抓取、更新及刪除 Product 類別實例的方法。 下列程式碼顯示新增產品的方法。 請注意，方法會傳回**應傳回 iHTTPactionresult**的實例。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

應傳回 iHTTPactionresult 是 Web API 2 中的其中一項新功能，可簡化單元測試的開發。

在下一節中，您將自訂產生的程式碼，以加速將測試物件傳遞至控制器。

<a id="dependency"></a>
## <a name="add-dependency-injection"></a>新增相依性插入

目前，ProductController 類別已硬式編碼，可使用 StoreAppCoNtext 類別的實例。 您將使用稱為「相依性插入」的模式來修改您的應用程式，並移除該硬式編碼的相依性。 藉由中斷此相依性，您可以在測試時傳入 mock 物件。

以滑鼠右鍵按一下 [**模型**] 資料夾，然後新增名為**IStoreAppCoNtext**的新介面。

使用下列程式碼取代程式碼。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

開啟 StoreAppCoNtext.cs 檔案，並進行下列反白顯示的變更。 要注意的重要變更包括：

- StoreAppCoNtext 類別會實 IStoreAppCoNtext 介面
- MarkAsModified 方法已實作為

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

開啟 ProductController.cs 檔案。 變更現有的程式碼，以符合反白顯示的程式碼。 這些變更會中斷對 StoreAppCoNtext 的相依性，並讓其他類別針對內容類別傳入不同的物件。 這項變更可讓您在單元測試期間傳入測試內容。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

您必須在 ProductController 中進行一項變更。 在**PutProduct**方法中，將設定實體狀態的程式程式碼取代為 MarkAsModified 方法的呼叫所修改的。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

建置方案。

您現在已準備好設定測試專案。

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a>在測試專案中安裝 NuGet 套件

當您使用空白範本來建立應用程式時，單元測試專案（StoreApp）不會包含任何已安裝的 NuGet 套件。 其他範本，例如 Web API 範本，則會在單元測試專案中包含一些 NuGet 套件。 在本教學課程中，您必須將 Entity Framework 封裝和 Microsoft ASP.NET Web API 2 核心套件加入至測試專案。

以滑鼠右鍵按一下 [StoreApp] 專案，然後選取 [**管理 NuGet 套件**]。 您必須選取 [StoreApp] 專案，才能將封裝加入至該專案。

![管理封裝](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

從線上套件，尋找並安裝 EntityFramework 套件（6.0 版或更新版本）。 如果已安裝 EntityFramework 封裝，您可能已選取 [StoreApp] 專案，而不是 [StoreApp] 專案。

![新增 Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

尋找並安裝 Microsoft ASP.NET Web API 2 核心套件。

![安裝 web api 核心套件](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

關閉 [管理 NuGet 封裝] 視窗。

<a id="testcontext"></a>
## <a name="create-test-context"></a>建立測試內容

將名為**TestDbSet**的類別加入至測試專案。 這個類別會作為測試資料集的基類。 使用下列程式碼取代程式碼。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

將名為**TestProductDbSet**的類別加入至包含下列程式碼的測試專案。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

新增名為**TestStoreAppCoNtext**的類別，並將現有的程式碼取代為下列程式碼。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a>建立測試

根據預設，您的測試專案會包含名為**UnitTest1.cs**的空白測試檔案。 此檔案會顯示您用來建立測試方法的屬性。 在本教學課程中，您可以刪除此檔案，因為您會加入新的測試類別。

將名為**TestProductController**的類別加入至測試專案。 使用下列程式碼取代程式碼。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a>執行測試

您現在已準備好執行測試。 所有以**TestMethod**屬性標記的方法都會進行測試。 從 [**測試**] 功能表項目執行測試。

![執行測試](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

開啟 [**測試瀏覽器**] 視窗，並注意測試的結果。

![測試結果](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)
