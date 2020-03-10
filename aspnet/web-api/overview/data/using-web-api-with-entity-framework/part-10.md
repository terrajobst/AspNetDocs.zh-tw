---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: 將應用程式發佈至 Azure Azure App Service |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: a9a7b74a07c71b47253c0af304c7a26ffa4eaae5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622385"
---
# <a name="publish-the-app-to-azure-azure-app-service"></a>將應用程式發佈至 Azure Azure App Service

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://github.com/MikeWasson/BookService)

在最後一個步驟中，您會將應用程式發行至 Azure。 在方案總管中，以滑鼠右鍵按一下專案，然後選取 [**發佈**]。

![](part-10/_static/image1.png)

按一下 [**發佈**] 會叫用 [**發行 Web** ] 對話方塊。 如果您在第一次建立專案時已核取 [**主機在雲端**]，則已設定連接和設定。 在此情況下，只需按一下 [**設定**] 索引標籤，然後檢查 &quot;執行 Code First 移轉&quot;。 （如果您在一開始就沒有檢查**雲端主機**，請遵循[下一節](#new-website)中的步驟。）

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

若要部署應用程式，請按一下 [**發佈**]。 您可以在 [ **Web 發行活動**] 視窗中查看發行進度。 （從 [ **View** ] 功能表選取 [**其他視窗**]，然後選取 [ **Web 發行活動**]）。

![](part-10/_static/image4.png)

當 Visual Studio 完成部署應用程式時，預設瀏覽器會自動開啟至已部署網站的 URL，而您建立的應用程式現在正在雲端中執行。 瀏覽器網址列中的 URL 會顯示正在從網際網路載入網站。

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a>部署至新網站

如果您在第一次建立專案時未檢查**雲端主機**，您可以立即設定新的 web 應用程式。 在方案總管中，以滑鼠右鍵按一下專案，然後選取 [**發佈**]。 選取 [**設定檔**] 索引標籤，然後按一下 [ **Microsoft Azure 網站**]。 如果您目前未登入 Azure，系統會提示您登入。

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

在 [**現有網站**] 對話方塊中，按一下 [**新增**]。

![](part-10/_static/image9.png)

輸入 [網站名稱]。 選取您的 Azure 訂用帳戶和區域。 在 [**資料庫伺服器**] 底下，選取 [**建立新的伺服器**]，或選取現有的伺服器。 按一下 [建立]。

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

按一下 [**設定**] 索引標籤，然後勾選 [&quot;執行 Code First 移轉&quot;]。 然後按一下 [發佈]。

> [!div class="step-by-step"]
> [上一篇](part-9.md)
