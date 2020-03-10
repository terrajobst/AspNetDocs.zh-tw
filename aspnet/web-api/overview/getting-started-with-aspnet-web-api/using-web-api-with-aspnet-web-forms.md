---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: 使用 Web API 搭配 ASP.NET Web Forms-ASP.NET 4。x
author: MikeWasson
description: 使用程式碼逐步解說將 Web API 新增至 ASP.NET 4.x 的 ASP.NET Forms 應用程式的教學課程
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556774"
---
# <a name="using-web-api-with-aspnet-web-forms"></a>使用具有 ASP.NET Web Forms 的 Web API

由[Mike Wasson](https://github.com/MikeWasson)

本教學課程將逐步引導您完成將 Web API 新增至 ASP.NET 4.x 中傳統 ASP.NET Web Forms 應用程式的步驟。 

## <a name="overview"></a>概觀

雖然 ASP.NET Web API 是以 ASP.NET MVC 封裝，但將 Web API 新增至傳統的 ASP.NET Web Forms 應用程式很容易。

若要在 Web Forms 應用程式中使用 Web API，有兩個主要步驟：

- 新增衍生自**ApiController**類別的 Web API 控制器。
- 將路由表新增至**應用程式\_Start**方法。

## <a name="create-a-web-forms-project"></a>建立 Web Forms 專案

啟動 Visual Studio，然後從 [**開始**] 頁面選取 [**新增專案**]。 或者，**從 [檔案**] 功能表選取 [**新增**]，然後選取 [**專案**]。

在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開 **C#視覺效果**節點。 在 **[ C#視覺效果**] 底下，選取 [ **Web**]。 在專案範本清單中，選取 [ **ASP.NET Web Forms 應用程式**]。 輸入專案的名稱，然後按一下 **[確定]** 。

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a>建立模型和控制器

本教學課程使用與[消費者入門](tutorial-your-first-web-api.md)教學課程相同的模型和控制器類別。

首先，新增模型類別。 在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增類別**]。 將類別命名為 Product，並新增下列實作為：

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

接下來，將 Web API 控制器新增至專案。*控制器*是處理 Web API 之 HTTP 要求的物件。

在 [方案總管] 中，以滑鼠右鍵按一下專案。 選取 [**加入新專案**]。

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

展開 **已安裝的範本** 底下**的**   **C#視覺效果**，然後選取 然後，從範本清單中選取 [ **WEB API 控制器類別**]。 將控制器命名為 "Productscontroller.cs"，然後按一下 [**新增**]。

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

[**加入新專案**] wizard 會建立名為 ProductsController.cs 的檔案。 刪除嚮導所包含的方法，並新增下列方法：

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

如需此控制器中程式碼的詳細資訊，請參閱[消費者入門](tutorial-your-first-web-api.md)教學課程。

## <a name="add-routing-information"></a>新增路由資訊

接下來，我們將新增 URI 路由，讓 &quot;/api/products/&quot; 表單的 Uri 路由傳送至控制器。

在**方案總管**中，按兩下 global.asax 以開啟 [程式碼後置檔案 Global.asax.cs]。 新增下列**using**語句。

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

然後，將下列程式碼新增至**應用程式\_Start**方法：

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

如需路由表的詳細資訊，請參閱[ASP.NET Web API 中的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)。

## <a name="add-client-side-ajax"></a>新增用戶端 AJAX

您只需要建立用戶端可以存取的 Web API。 現在讓我們加入一個使用 jQuery 呼叫 API 的 HTML 網頁。

請確定您的主版頁面（例如，*網站*）包含具有 `ID="HeadContent"`的 `ContentPlaceHolder`：

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

開啟檔案 default.aspx。 取代主要內容區段中的重複顯示文字，如下所示：

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

接下來，在 [`HeaderContent`] 區段中新增 jQuery 來源檔案的參考：

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

注意：您可以將檔案從**方案總管**拖放到 [程式碼編輯器] 視窗中，輕鬆地加入腳本參考。

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

在 jQuery script 標記底下，新增下列腳本區塊：

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

當檔載入時，此腳本會發出 AJAX 要求，以 &quot;api/產品&quot;。 要求會傳回 JSON 格式的產品清單。 腳本會將產品資訊新增至 HTML 資料表。

當您執行應用程式時，它看起來應該像這樣：

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
