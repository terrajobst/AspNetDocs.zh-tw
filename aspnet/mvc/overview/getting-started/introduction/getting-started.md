---
uid: mvc/overview/getting-started/introduction/getting-started
title: ASP.NET MVC 5 的消費者入門 |Microsoft Docs
author: Rick-Anderson
ms.author: riande
ms.date: 10/04/2018
ms.assetid: f3d8adbe-55e7-4fd4-84a8-7155bc45c676
msc.legacyurl: /mvc/overview/getting-started/introduction/getting-started
msc.type: authoredcontent
ms.openlocfilehash: ca39bc37c757c0452cf56624c8e37c04df4b41f2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78602764"
---
# <a name="getting-started-with-aspnet-mvc-5"></a>開始使用 ASP.NET MVC 5

依[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](../../../../includes/razor.md)]

本教學課程會教您使用[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)建立 ASP.NET MVC 5 web 應用程式的基本概念。 本教學課程的最終原始程式碼位於[GitHub](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie)。

本教學課程是由[Scott Guthrie](https://weblogs.asp.net/scottgu/) （twitter[@scottgu](https://twitter.com/scottgu) ）、 [scott Hanselman](http://www.hanselman.com/blog/) （Twitter： [@shanselman](https://twitter.com/shanselman) ）和[Rick Anderson](https://twitter.com/RickAndMSFT) （ [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ）所撰寫

您需要 Azure 帳戶，才能將此應用程式部署至 Azure：

- 您可以[免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-您將取得可試用付費 azure 服務的額度，且即使在用完後，您仍可保留帳戶，並使用免費的 azure 服務。
- 您可以 [啟用 MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - 您的 MSDN 訂閱每月會提供您額度，您可以用在 Azure 付費服務。

## <a name="get-started"></a>開始使用

一開始請先[安裝 Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。 然後，開啟 Visual Studio。

Visual Studio 是 IDE 或整合式開發環境。 就像您使用 Microsoft Word 來撰寫檔一樣，您將使用 IDE 來建立應用程式。 在 Visual Studio 中，底部會有一個清單，顯示您可以使用的各種選項。 另外還有一個功能表，可提供另一種在 IDE 中執行工作的方式。 例如，您可以使用功能表列，然後選取 [檔案] > [**新增專案**]，而不**是選取 [** **開始] 頁面**上的 [**新增專案**]。

![](getting-started/_static/image1.png)

## <a name="create-your-first-app"></a>建立您的第一個應用程式

在 [**開始] 頁面**上，選取 [**新增專案**]。 在 [**新增專案**] 對話方塊中，依序選取左側的 [**視覺效果C#**  ] 類別目錄和 [ **web**]，然後選取 [ **ASP.NET Web 應用程式（.NET Framework）** ] 專案範本。 將專案命名為 "MvcMovie"，然後選擇 **[確定]** 。

![](getting-started/_static/image2.png)

在 [**新增 ASP.NET Web 應用程式**] 對話方塊中，選擇 [ **MVC** ]，然後選擇 **[確定]** 。

![](getting-started/_static/image3.png)

Visual Studio 使用您剛建立的 ASP.NET MVC 專案的預設範本，所以您現在有一個可運作的應用程式，而不需要執行任何動作！ 這是簡單的「Hello World！」 專案，這是啟動應用程式的好地方。

![](getting-started/_static/image4.png)

按 **F5** 開始偵錯作業。 當您按下**F5**時，Visual Studio 會開始[IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)並執行您的 web 應用程式。 Visual Studio 接著會啟動瀏覽器，並開啟應用程式的首頁。 請注意，瀏覽器的網址列會顯示 `localhost:port#`，而不是類似 `example.com`。 這是因為 `localhost` 一定會指向您自己的本機電腦，在此情況下，它會執行您剛建立的應用程式。 當 Visual Studio 執行 Web 專案時，會針對網頁伺服器使用隨機埠。 在下圖中，埠號碼為1234。 當您執行應用程式時，您會看到不同的埠號碼。

![](getting-started/_static/image5.png)

現成的預設範本會提供您 `Home`、`Contact`和 `About` 頁面的許可權。 下圖不會顯示 [**首頁**]、[**關於**] 和 [**連絡人**] 連結。 視瀏覽器視窗的大小而定，您可能需要按一下流覽圖示才能看到這些連結。

![](getting-started/_static/image6.png)

應用程式也會提供註冊和登入的支援。 下一步是變更此應用程式的運作方式，並稍微瞭解 ASP.NET MVC。 關閉 ASP.NET MVC 應用程式，讓我們變更一些程式碼。

如需目前教學課程的清單，請參閱[MVC 建議的文章](../mvc-learning-sequence.md)。

## <a name="see-this-app-running-on-azure"></a>請參閱此應用程式在 Azure 上執行

您是否想要查看已完成的網站以即時 web 應用程式的形式執行？ 只要按一下下列按鈕，您就可以將應用程式的完整版本部署至您的 Azure 帳戶。

[![](https://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?repository=https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie&amp;WT.mc_id=deploy_azure_aspnet)

您需要 Azure 帳戶，才能將此解決方案部署至 Azure。 如果您還沒有帳戶，請使用下列其中一個選項建立一個：

- [免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-您將取得可試用付費 azure 服務的額度，且即使在用完後，您仍可保留帳戶，並使用免費的 azure 服務。
- [啟用 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers)-您的 Visual Studio 訂用帳戶每月會提供您額度，供您用於付費 Azure 服務。

> [!div class="step-by-step"]
> [下一個](adding-a-controller.md)
