---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
title: 使用 Windows 驗證驗證使用者（VB） |Microsoft Docs
author: microsoft
description: 瞭解如何在 MVC 應用程式的內容中使用 Windows 驗證。 您將瞭解如何在應用程式的 web co 中啟用 Windows 驗證 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 532fa051-7d5c-4d6d-87f6-339ce4b84c44
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: aa64b1f9ef6461a81611ca066310dca2d545baa3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624114"
---
# <a name="authenticating-users-with-windows-authentication-vb"></a>使用Windows 驗證驗證使用者 (VB)

由[Microsoft](https://github.com/microsoft)

> 瞭解如何在 MVC 應用程式的內容中使用 Windows 驗證。 您將瞭解如何在應用程式的 web 設定檔中啟用 Windows 驗證，以及如何使用 IIS 設定驗證。 最後，您將瞭解如何使用 [授權] 屬性來限制對特定 Windows 使用者或群組的控制器動作存取。

本教學課程的目的是要說明如何利用內建在 Internet Information Services 中的安全性功能，來保護 MVC 應用程式中的 views。 您將瞭解如何允許只有特定 Windows 使用者或特定 Windows 群組成員的使用者，才可以叫用控制器動作。

當您要建立內部公司網站（內部網路網站），而且想要讓使用者能夠在存取網站時使用其標準 Windows 使用者名稱和密碼時，使用 Windows 驗證就很有意義。 如果您要建立向外面向網站（網際網路網站），請考慮改用表單驗證。

#### <a name="enabling-windows-authentication"></a>啟用 Windows 驗證

當您建立新的 ASP.NET MVC 應用程式時，預設不會啟用 Windows 驗證。 表單驗證是針對 MVC 應用程式啟用的預設驗證類型。 您必須藉由修改 MVC 應用程式的 web 設定（web.config）檔案來啟用 Windows 驗證。 尋找 &lt;authentication&gt; 區段，並將它修改為使用 Windows，而不是像這樣的表單驗證：

[!code-xml[Main](authenticating-users-with-windows-authentication-vb/samples/sample1.xml)]

當您啟用 Windows 驗證時，您的網頁伺服器會負責驗證使用者。 一般來說，您在建立和部署 ASP.NET MVC 應用程式時，會使用兩種不同類型的 web 伺服器。

首先，在開發 MVC 應用程式時，您會使用 Visual Studio 隨附的 ASP.NET 開發 Web 服務器。 根據預設，ASP.NET 開發 Web 服務器會執行目前 Windows 帳戶（您用來登入 Windows 的任何帳戶）內容中的所有頁面。

ASP.NET 開發網頁伺服器也支援 NTLM 驗證。 以滑鼠右鍵按一下 [方案總管] 視窗中的專案名稱，然後選取 [屬性]，即可啟用 NTLM 驗證。 接下來，選取 [Web] 索引標籤並勾選 [NTLM] 核取方塊（請參閱 [圖 1]）。

**圖1–為 ASP.NET 開發 Web 服務器啟用 NTLM 驗證**

![clip_image002](authenticating-users-with-windows-authentication-vb/_static/image1.jpg)

對於生產 web 應用程式，您可以使用 IIS 做為 web 伺服器。 IIS 支援數種類型的驗證，包括：

- 基本驗證–定義為 HTTP 1.0 通訊協定的一部分。 以純文字（Base64 編碼）傳送網際網路上的使用者名稱和密碼。 -摘要式驗證–透過網際網路傳送密碼雜湊，而不是密碼本身。 -整合式 Windows （NTLM）驗證–使用 Windows 在內部網路環境中使用的最佳驗證類型。 -憑證驗證–使用用戶端憑證來啟用驗證。 憑證會對應至 Windows 使用者帳戶。

> [!NOTE] 
> 
> 如需這些不同驗證類型的詳細總覽，請參閱[https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)。

您可以使用 Internet Information Services 管理員來啟用特定類型的驗證。 請注意，所有類型的驗證在每個作業系統的情況下都不適用。 此外，如果您將 IIS 7.0 與 Windows Vista 搭配使用，您必須先啟用不同類型的 Windows 驗證，才會出現在 Internet Information Services 管理員中。 開啟 [**控制台]、[程式]、[程式和功能]、[開啟或關閉 Windows 功能**]，然後展開 [Internet Information Services] 節點（請參閱 [圖 2]）。

**[圖 2]-啟用 Windows IIS 功能**

![clip_image004](authenticating-users-with-windows-authentication-vb/_static/image2.jpg)

使用 Internet Information Services，您可以啟用或停用不同類型的驗證。 例如，[圖 3] 說明如何停用匿名驗證，並在使用 IIS 7.0 時啟用整合式 Windows （NTLM）驗證。

**[圖 3]-啟用整合式 Windows 驗證**

![clip_image006](authenticating-users-with-windows-authentication-vb/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a>授權 Windows 使用者和群組

啟用 Windows 驗證之後，您可以使用 &lt;授權&gt; 屬性來控制控制器或控制器動作的存取權。 這個屬性可以套用至整個 MVC 控制器或特定的控制器動作。

例如，[清單 1] 中的 Home 控制器會公開名為 Index （）、CompanySecrets （）和 StephenSecrets （）的三個動作。 任何人都可以叫用 Index （）動作。 不過，只有 Windows 本機管理員群組的成員可以叫用 CompanySecrets （）動作。 最後，只有名為 Stephen （位於 Redmond 網域）的 Windows 網域使用者，才能夠叫用 StephenSecrets （）動作。

**清單1– Controllers\HomeController.vb**

[!code-vb[Main](authenticating-users-with-windows-authentication-vb/samples/sample2.vb)]

> [!NOTE]
> 由於 Windows 使用者帳戶控制（UAC），在使用 Windows Vista 或 Windows Server 2008 時，本機系統管理員群組的行為會與其他群組不同。 除非您修改電腦的 UAC 設定，否則 &lt;授權&gt; 屬性將無法正確辨識本機 Administrators 群組的成員。

當您嘗試叫用控制器動作而不是正確的許可權時，會發生什麼事，視啟用的驗證類型而定。 根據預設，使用 ASP.NET 程式開發伺服器時，您只會看到空白頁面。 此頁面提供**401 未授權**的 HTTP 回應狀態。

另一方面，如果您使用的 IIS 已停用匿名驗證，且已啟用基本驗證，則每次要求受保護的頁面時，都會持續取得登入對話方塊提示（請參閱 [圖 4]）。

**[圖 4]-基本驗證登入對話方塊**

![clip_image008](authenticating-users-with-windows-authentication-vb/_static/image4.jpg)

#### <a name="summary"></a>總結

本教學課程會說明如何在 ASP.NET MVC 應用程式的內容中使用 Windows 驗證。 您已瞭解如何在應用程式的 web 設定檔中啟用 Windows 驗證，以及如何使用 IIS 設定驗證。 最後，您已瞭解如何使用 &lt;授權&gt; 屬性來限制對特定 Windows 使用者或群組的控制器動作存取。

> [!div class="step-by-step"]
> [上一頁](authenticating-users-with-forms-authentication-vb.md)
> [下一頁](preventing-javascript-injection-attacks-vb.md)
