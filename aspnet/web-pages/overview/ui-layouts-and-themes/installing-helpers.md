---
uid: web-pages/overview/ui-layouts-and-themes/installing-helpers
title: 在 ASP.NET Web Pages （Razor）網站中安裝 Helper |Microsoft Docs
author: Rick-Anderson
description: 本文說明如何在 ASP.NET Web Pages （Razor）網站中安裝協助程式。 協助程式是可重複使用的元件，其中包含程式碼和標記為每個 。
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 5e968ead-906a-45ea-ac2a-c70e57e1a9b1
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/installing-helpers
msc.type: authoredcontent
ms.openlocfilehash: 41e33c04a53a6ad257c3937cdadcec767e9217c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638583"
---
# <a name="installing-a-helper-in-an-aspnet-web-pages-razor-site"></a>在 ASP.NET Web Pages （Razor）網站中安裝 Helper

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明如何在 ASP.NET Web Pages （Razor）網站中安裝協助程式。 *Helper*是可重複使用的元件，其中包含程式碼和標記來執行可能單調乏味或複雜的工作。
> 
> 您將學到什麼：
> 
> - 如何在使用 WebMatrix 3 建立的網站中安裝 helper。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - WebMatrix 3

## <a name="overview-of-helpers"></a>協助程式總覽

人們通常會想要在網頁上執行的某些工作需要大量的程式碼，或需要額外的知識。 範例包括顯示資料的圖表;在頁面上放置 Twitter 的 [跟隨] 按鈕;正在從您的網站傳送電子郵件;裁剪或調整影像大小;針對您的網站使用 PayPal。 為了讓您輕鬆執行這類工作，ASP.NET Web Pages 可讓*您使用協助*程式。 協助程式是您為網站安裝的元件，可讓您只使用一行或兩個 Razor 程式碼來執行一般工作。

ASP.NET Web Pages 內建了一些協助程式。 不過，許多協助程式都可以在使用 NuGet 套件管理員所提供的封裝（增益集）中取得。 NuGet 可讓您選取要安裝的套件，然後負責安裝的所有詳細資料。

## <a name="installing-a-helper-in-webmatrix-3"></a>在 WebMatrix 中安裝 Helper 3

1. 在 WebMatrix 3 中，按一下 [ **NuGet** ] 按鈕。

    ![WebMatrix 中的 [NuGet 資源庫] 對話方塊](installing-helpers/_static/image1.png)
2. 這會啟動 NuGet 套件管理員，並顯示可用的套件。 在 [搜尋] 方塊中，為您要安裝的 helper 輸入關鍵字。

    ![WebMatrix 中的 [NuGet 資源庫] 對話方塊](installing-helpers/_static/image2.png)
3. 選取套件，然後按一下 [**安裝**]。 當系統詢問您是否要安裝套件，並指出您接受條款時，請按一下 **[是]** 。

     如果這是您第一次安裝 helper，NuGet 會針對組成協助程式的程式碼，在您的網站中建立資料夾。
4. 若要卸載協助程式，請按一下 [資源**庫**] 按鈕，按一下 [**已安裝**] 索引標籤，然後挑選您要卸載的套件。

## <a name="installing-the-twitter-helper"></a>安裝 Twitter helper

Twitter API 的最新版本與您透過 NuGet 安裝的 Twitter helper 不相容。 相反地，請參閱[Twitter helper With WebMatrix](twitter-helper.md)主題，以取得如何在專案中設定 Twitter 協助程式的相關資訊。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他資源

[簡介 ASP.NET Web Pages 2-程式設計基本概念](../getting-started/introducing-razor-syntax-c.md)

[Twitter Helper 與 WebMatrix](twitter-helper.md)
