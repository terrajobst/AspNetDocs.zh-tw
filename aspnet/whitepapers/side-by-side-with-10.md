---
uid: whitepapers/side-by-side-with-10
title: ASP.NET .NET Framework 1.0 和1.1 的並存執行 |Microsoft Docs
author: rick-anderson
description: 本白皮書說明如何在您的電腦上安裝 .NET 1.0 和 .NET 1.1，讓 ASP.NET Web 應用程式可在任一版本的 fram 上執行 。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: c123545099013af71569bce4707f2b3eb732c344
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78632969"
---
# <a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a>ASP.NET 並存執行 .NET Framework 1.0 與 1.1

> 本白皮書說明如何在您的電腦上安裝 .NET 1.0 和 .NET 1.1，讓 ASP.NET Web 應用程式可在任一版本的架構上執行。
> 
> 適用于 ASP.NET 1.0 和 ASP.NET 1.1。

在 ASP.NET 中，當應用程式安裝在同一部電腦上，但使用不同版本的 .NET Framework 時，就會被視為並存執行。 下列主題說明如何設定 ASP.NET 應用程式以進行並存執行，並提供詳細的步驟來執行下列動作：

- [在安裝期間維護 Web 應用程式與 .NET Framework 版本1.0 的對應](#1)
- [將 Web 應用程式對應至特定版本的 .NET Framework](#2)
- [找出網站所使用的 .NET Framework 版本](#3)

傳統上，當元件或應用程式在電腦上更新時，會移除較舊的版本，並取代為較新的版本。 如果新版本與先前的版本不相容，這通常會中斷使用元件或應用程式的其他應用程式。 .NET Framework 提供並存執行的支援，允許在同一部電腦上同時安裝多個版本的元件或應用程式。 因為可以同時安裝多個版本，所以受控應用程式可以選擇要使用的版本，而不會影響使用不同版本的應用程式。

根據預設，在安裝 .NET Framework 版本1.1 期間，所有現有的 ASP.NET 應用程式都會自動重新設定為使用最新版本的 .NET Framework。 如果您不想讓 ASP.NET 應用程式預設為 .NET Framework 1.1，請按一下[這裡](#1)以瞭解如何在安裝期間避免這種情況。

如果您將 Web 服務器更新為 .NET Framework 1.1，而且想要在 .NET Framework 1.0 中執行一或多個 Web 應用程式，則需要更新 Internet Information Services （IIS）腳本對應。 腳本對應是將特定 Web 應用程式的 .aspx 副檔名對應至 .NET Framework 版本的機制。 按一下[這裡](#2)以瞭解如何將 Web 應用程式對應至特定版本的 .NET Framework。

您可以使用 Internet Information manager 或 ASP.NET IIS 註冊工具（Aspnet\_regiis）來尋找哪個 .NET Framework 版本正在執行特定的 Web 應用程式。 按一下[這裡](#3)以瞭解如何找出網站所使用的 .NET Framework 版本。

遷移至 .NET Framework 1.1 時，一個匯入考慮是 .NET Framework 的每個版本都使用它自己的 Machine.config 檔案。 因此，如果 Web 管理員對 Machine.config 檔案進行了變更，這些變更就必須遷移到 .NET Framework 1.1 Machine.config 檔案。

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a>在安裝期間維護 Web 應用程式與 .NET Framework 1.0 的對應

根據預設，所有現有的 ASP.NET 應用程式會在安裝期間自動重新設定，以使用較新版本的 .NET Framework。 使用較新版本的 .NET Framework，應用程式可以充分利用新版本中所包含的改良功能和新功能。 同時，若 Web 管理員可能想要更精確地控制哪些應用程式已更新，則在安裝 .NET Framework 時，可能會導致無法自動重新對應所有現有的 ASP.NET 應用程式。

為避免將整個 ASP.NET 應用程式自動重新對應到較新版本的 .NET Framework，Web 管理員可以使用/noaspupgrade 命令列選項搭配 Dotnetfx.exe 安裝程式。

**防止 ASP.NET 應用程式重新對應到較新的版本**

1. 移至 [啟動]。
2. 按一下 [**執行**]。
3. 輸入 **cmd**。
4. 按一下 [確定]。  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. 從命令提示字元輸入下列程式程式碼，以開始安裝 .NET Framework： **dotnetfx.exe/c： "install/noaspupgrade？"** 。  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. 在 Microsoft .NET Framework 1.1 安裝程式中按一下 **[是]** 。 這會啟動 .NET Framework 1.1 的設定程式。  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a>將 Web 應用程式對應至特定版本的 .NET Framework

.NET Framework 的每個版本都包含一個版本的 ASP.NET IIS 註冊工具（Aspnet\_regiis）。 這項工具可讓系統管理員指定在特定版本的 .NET Framework 下執行 Web 應用程式。 這稱為將 Web 應用程式對應至 .NET Framework 的版本。 系統管理員必須選取對應至將與 Web 應用程式相關聯之 .NET Framework 版本的 Aspnet\_regiis。 例如，想要指定網站使用 .NET Framework 1.1 的系統管理員，必須使用 .NET Framework 1.1 隨附的 Aspnet\_regiis。

1\.0 版的 Aspnet\_regiis 位於：

- C:\WINDOWS\Microsoft.NET\Framework\\**v v1.0.3705**\aspnet\_regiis

第1版的 Aspnet\_regiis，1位於：

- C:\WINDOWS\Microsoft.NET\Framework\\**v 1.1.4322**\aspnet\_regiis

Aspnet\_regiis 提供兩個選項來對應 Web 應用程式的腳本：

- **-s**會在路徑和其子目錄中設定腳本對應。
- **-sn**只會在路徑中設定腳本對應。

路徑會定義 Web 應用程式 IIS 中繼資料路徑，其定義格式為 W3SVC/ROOT/{WebSiteNumber}/{應用程式\_名稱}。 例如，對於名為入口網站的 Web 應用程式，位於 [預設的網站] 底下，則元資料庫路徑為 W3SVC/1/ROOT/Portal。

![](side-by-side-with-10/_static/image4.gif)

注意：您也可以使用稱為「元資料庫編輯器」的工具來取得元資料庫路徑。 您可以從 Microsoft 支援服務網站下載此工具，網址為[https://support.microsoft.com/default.aspx?scid=kb; en-us; 232068。](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)

- 執行 Aspnet\_regiis-s W3SVC/1/ROOT/Portal，以更新入口網站 IIS 腳本對應和其 subapplication。  
  
    ![](side-by-side-with-10/_static/image5.gif)

- 執行 Aspnet\_regiis，以更新入口網站 IIS 腳本對應，而不會影響入口網站子目錄中的應用程式。  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a>尋找 Web 應用程式正在使用的 .NET Framework 版本

系統管理員可以使用網際網路 Service Manager 來尋找哪個版本的 .NET Framework 會執行網站。 不同的作業系統版本會以不同的方式啟動網際網路 Service Manager。 若要啟動服務管理員，請遵循下列步驟。

**若要啟動網際網路 Service Manager**

1. 移至 [啟動]。
2. 按一下 [**執行**]。
3. 輸入**inetmgr**。  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. 從 [網際網路] Service Manager 中，選取您想要知道其版本 .NET Framework 的 Web 應用程式。  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. 以滑鼠右鍵按一下 Web 應用程式，然後按一下 [**屬性]。**  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. 從 [屬性] 視窗中，選取 [設定] **。**  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. 從 [應用程式對應] 資料表中，選取 [ **.aspx**]，然後按一下 [**編輯**]。  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. 從 [**可執行檔**] 文字方塊中，藉由滾動來查看版本目錄。 如果版本目錄是1.1.4322，應用程式會對應到 .NET Framework 1.1。 相反地，如果版本目錄是 v v1.0.3705，應用程式會對應到 .NET Framework 1.0。  
  
    ![](side-by-side-with-10/_static/image12.gif)
