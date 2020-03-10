---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
title: 建立 OData v4 用戶端應用程式C#（） |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 47202362-3808-4add-9a69-c9d1f91d5e4e
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
msc.type: authoredcontent
ms.openlocfilehash: a0016cf2cc7bffe6268664395ccb38e140090310
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556291"
---
# <a name="create-an-odata-v4-client-app-c"></a>建立 OData v4 用戶端應用程式 (C#)

由[Mike Wasson](https://github.com/MikeWasson)

在上一個教學課程中，您已建立支援 CRUD 作業的基本 OData 服務。 現在讓我們建立服務的用戶端。

啟動 Visual Studio 的新實例，然後建立新的主控台應用程式專案。 在 [**新增專案**] 對話方塊中，選取 [**已安裝**] &gt; [&gt; **Visual C#**  &gt; **Windows 桌面**的**範本**]，然後選取 [**主控台應用程式**] 範本。 將專案命名為 &quot;ProductsApp&quot;。

![](create-an-odata-v4-client-app/_static/image1.png)

> [!NOTE]
> 您也可以將主控台應用程式新增至包含 OData 服務的相同 Visual Studio 解決方案。

## <a name="install-the-odata-client-code-generator"></a>安裝 OData 用戶端程式代碼產生器

從 [工具] 功能表中，選取 [擴充功能和更新]。 選取 [**線上**&gt; **Visual Studio 資源庫**]。 在搜尋方塊中，搜尋 &quot;OData 用戶端程式代碼產生器&quot;。 按一下 [**下載**] 以安裝 VSIX。 系統可能會提示您重新開機 Visual Studio。

[![](create-an-odata-v4-client-app/_static/image3.png)](create-an-odata-v4-client-app/_static/image2.png)

## <a name="run-the-odata-service-locally"></a>在本機執行 OData 服務

從 Visual Studio 執行 ProductService 專案。 根據預設，Visual Studio 會將瀏覽器啟動至應用程式根目錄。 請記下 URI;在下一個步驟中，您將需要此項。 繼續執行應用程式。

![](create-an-odata-v4-client-app/_static/image4.png)

> [!NOTE]
> 如果您將這兩個專案放在相同的方案中，請務必執行 ProductService 專案而不進行調試。 在下一個步驟中，您將需要在修改主控台應用程式專案時，讓服務保持執行狀態。

## <a name="generate-the-service-proxy"></a>產生服務 Proxy

服務 proxy 是一個 .NET 類別，可定義存取 OData 服務的方法。 Proxy 會將方法呼叫轉譯為 HTTP 要求。 您將藉由執行[T4 範本](https://msdn.microsoft.com/library/bb126445.aspx)來建立 proxy 類別。

以滑鼠右鍵按一下專案。 選取 **[** **新增 &gt; 新專案**]。

![](create-an-odata-v4-client-app/_static/image5.png)

在 [**加入新專案**] 對話方塊中，選取 [&gt; 程式**代碼**&gt; **OData 用戶端**] 的 [**視覺C#專案**]。 將範本命名 &quot;ProductClient.tt&quot;。 按一下 [**新增**]，然後按一下 [安全性警告]。

[![](create-an-odata-v4-client-app/_static/image7.png)](create-an-odata-v4-client-app/_static/image6.png)

此時，您會收到錯誤，您可以忽略它。 Visual Studio 會自動執行範本，但範本需要先進行一些設定。

[![](create-an-odata-v4-client-app/_static/image9.png)](create-an-odata-v4-client-app/_static/image8.png)

開啟檔案 ProductClient。在 `Parameter` 元素中，貼上 ProductService 專案（上一個步驟）中的 URI。 例如:

[!code-xml[Main](create-an-odata-v4-client-app/samples/sample1.xml)]

[![](create-an-odata-v4-client-app/_static/image11.png)](create-an-odata-v4-client-app/_static/image10.png)

再次執行範本。 在方案總管中，以滑鼠右鍵按一下 ProductClient.tt 檔案，然後選取 [**執行自訂工具**]。

此範本會建立名為 ProductClient.cs 的程式碼檔案，以定義 proxy。 當您開發應用程式時，如果您變更 OData 端點，請再次執行範本來更新 proxy。

![](create-an-odata-v4-client-app/_static/image12.png)

## <a name="use-the-service-proxy-to-call-the-odata-service"></a>使用服務 Proxy 呼叫 OData 服務

開啟檔案 Program.cs，並以下列程式碼取代重複使用的程式碼。

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample2.cs)]

將*serviceUri*的值取代為先前的服務 URI。

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample3.cs)]

當您執行應用程式時，它應該會輸出下列內容：

[!code-console[Main](create-an-odata-v4-client-app/samples/sample4.cmd)]
