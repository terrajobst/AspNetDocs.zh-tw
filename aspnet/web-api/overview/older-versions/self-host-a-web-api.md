---
uid: web-api/overview/older-versions/self-host-a-web-api
title: 自我裝載 ASP.NET Web API 1 （C#）-ASP.NET 4。x
author: MikeWasson
description: 教學課程示範如何在主控台應用程式中裝載 Web API。
ms.author: riande
ms.date: 01/26/2012
ms.custom: seoapril2019
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: bae1737ba5b16bc67fa0ed0474ff04df0add1b3a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525085"
---
# <a name="self-host-aspnet-web-api-1-c"></a>自我裝載 ASP.NET Web API 1 （C#）

由[Mike Wasson](https://github.com/MikeWasson)

> 本教學課程說明如何在主控台應用程式中裝載 Web API。 ASP.NET Web API 不需要 IIS。 您可以在自己的主機進程中自我裝載 Web API。 
> 
> **新的應用程式應該使用 OWIN 來自我裝載 Web API。** 請參閱[使用 OWIN 至自我裝載 ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - Web API 1
> - Visual Studio 2012

## <a name="create-the-console-application-project"></a>建立主控台應用程式專案

啟動 Visual Studio，然後從 [**開始**] 頁面選取 [**新增專案**]。 或者，**從 [檔案**] 功能表選取 [**新增**]，然後選取 [**專案**]。

在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開 **C#視覺效果**節點。 在 **[ C#視覺效果**] 底下，選取 [ **Windows**]。 在專案範本清單中，選取 [**主控台應用程式**]。 將專案命名為 &quot;SelfHost&quot; 然後按一下 **[確定]** 。

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a>設定目標 Framework （Visual Studio 2010）

如果您使用 Visual Studio 2010，請將目標 framework 變更為 .NET Framework 4.0。 （根據預設，專案範本會以[.Net Framework 用戶端設定檔](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile)為目標）。

在方案總管中，以滑鼠右鍵按一下專案，然後選取 [**屬性**]。 在 [**目標 framework** ] 下拉式清單中，將 [目標 framework] 變更為 .NET Framework 4.0。 當系統提示您套用變更時，按一下 **[是]** 。

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a>安裝 NuGet 套件管理員

NuGet 套件管理員是將 Web API 元件新增至 non-ASP.NET 專案的最簡單方式。

若要檢查是否已安裝 NuGet 套件管理員，請按一下 Visual Studio 中的 [**工具**] 功能表。 如果您看到名為 [ **Nuget 套件管理員**] 的功能表項目，則您會有 Nuget 套件管理員。

若要安裝 NuGet 套件管理員：

1. 啟動 Visual Studio。
2. 從 [工具] 功能表中，選取 [擴充功能和更新]。
3. 在 [**擴充功能和更新**] 對話方塊中，選取 [**線上**]。
4. 如果您沒有看到「NuGet 套件管理員」，請在搜尋方塊中輸入「nuget 套件管理員」。
5. 選取 [NuGet 套件管理員]，然後按一下 [**下載**]。
6. 下載完成之後，系統會提示您安裝。
7. 安裝完成之後，系統可能會提示您重新開機 Visual Studio。

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a>新增 Web API NuGet 套件

安裝 NuGet 套件管理員之後，請將 Web API 自我裝載封裝新增至您的專案。

1. 從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]。 *注意*：如果您看不到此功能表項目，請確定已正確安裝 NuGet 套件管理員。
2. 選取 [**管理解決方案的 NuGet 套件**]
3. 在 [**管理 NugGet 封裝**] 對話方塊中，選取 [**線上**]。
4. 在搜尋方塊中，輸入 &quot;WebApi. SelfHost&quot;。
5. 選取 ASP.NET Web API 的自我裝載套件，然後按一下 [**安裝**]。
6. 安裝套件之後，按一下 [**關閉**] 以關閉對話方塊。

> [!NOTE]
> 請務必安裝名為 WebApi. SelfHost，而不是 AspNetWebApi. SelfHost 的套件。

![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a>建立模型和控制器

本教學課程使用與[消費者入門](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)教學課程相同的模型和控制器類別。

新增名為 `Product`的公用類別。

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

新增名為 `ProductsController`的公用類別。 從**ApiController**衍生這個類別。

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

如需此控制器中程式碼的詳細資訊，請參閱[消費者入門](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)教學課程。 此控制器會定義三個 GET 動作：

| URI | 說明 |
| --- | --- |
| /api/products | 取得所有產品的清單。 |
| /api/products/*識別碼* | 依識別碼取得產品。 |
| /api/products/？ category =*category* | 依類別取得產品清單。 |

## <a name="host-the-web-api"></a>裝載 Web API

開啟檔案 Program.cs，並新增下列 using 語句：

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

將下列程式碼新增至**Program**類別。

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a>選擇性新增 HTTP URL 命名空間保留

此應用程式會接聽 `http://localhost:8080/`。 根據預設，接聽特定 HTTP 位址時需要系統管理員許可權。 當您執行本教學課程時，您可能會收到下列錯誤：「HTTP 無法登錄 URL http://+:8080/」，有兩種方式可避免此錯誤：

- 以提升的系統管理員許可權執行 Visual Studio，或
- 使用 Netsh 來授與您的帳戶許可權以保留 URL。

若要使用 Netsh，請使用系統管理員許可權開啟命令提示字元，並輸入下列命令：

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

其中*machine\username*是您的使用者帳戶。

當您完成自我裝載時，請務必刪除保留：

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a>從用戶端應用程式呼叫 Web API （C#）

讓我們撰寫一個簡單的主控台應用程式，以呼叫 Web API。

將新的主控台應用程式專案新增至方案：

- 在方案總管中，以滑鼠右鍵按一下方案，然後選取 [**加入新專案**]。
- 建立名為 &quot;ClientApp&quot;的新主控台應用程式。

![](self-host-a-web-api/_static/image5.png)

使用 NuGet 套件管理員來新增 ASP.NET Web API 核心程式庫套件：

- 從 [工具] 功能表中，選取 [ **NuGet 套件管理員**]。
- 選取 [**管理解決方案的 NuGet 套件**]
- 在 [**管理 NuGet 套件**] 對話方塊中，選取 [**線上**]。
- 在搜尋方塊中，輸入 &quot;WebApi. 用戶端&quot;。
- 選取 [Microsoft ASP.NET Web API 用戶端程式庫] 套件，然後按一下 [**安裝**]。

將 ClientApp 中的參考新增至 SelfHost 專案：

- 在方案總管中，以滑鼠右鍵按一下 [ClientApp] 專案。
- 選取 [新增參考]。
- 在 [**參考管理員**] 對話方塊中，選取 [**方案**] 底下的 [**專案**]。
- 選取 [SelfHost] 專案。
- 按一下 [確定]。

![](self-host-a-web-api/_static/image6.png)

開啟用戶端/程式 .cs 檔案。 加入下列 **using** 陳述式：

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

新增靜態**HttpClient**實例：

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

新增下列方法以列出所有產品、依識別碼列出產品，以及依類別列出產品。

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

所有這些方法都會遵循相同的模式：

1. 呼叫**HttpClient. GetAsync** ，將 GET 要求傳送至適當的 URI。
2. 呼叫**HttpResponseMessage. EnsureSuccessStatusCode**。 如果 HTTP 回應狀態為錯誤碼，這個方法就會擲回例外狀況。
3. 呼叫**ReadAsAsync&lt;t&gt;** ，將 CLR 類型從 HTTP 回應還原序列化。 這個方法是在**HttpContentExtensions**中定義的擴充方法。

**GetAsync**和**ReadAsAsync**方法都是非同步。 它們會傳回代表非同步作業的**Task**物件。 取得**Result**屬性會封鎖執行緒，直到作業完成為止。

如需使用 HttpClient 的詳細資訊，包括如何進行非封鎖式呼叫，請參閱[從 .Net 用戶端呼叫 WEB API](../advanced/calling-a-web-api-from-a-net-client.md)。

在呼叫這些方法之前，請先將 HttpClient 實例上的 BaseAddress 屬性設定為 "`http://localhost:8080`"。 例如:

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

這應該會輸出下列各項。 （請記得先執行 SelfHost 應用程式）。

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
