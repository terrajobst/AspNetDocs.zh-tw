---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
title: 使用表單驗證驗證使用者（VB） |Microsoft Docs
author: microsoft
description: 瞭解如何使用 [授權] 屬性來保護 MVC 應用程式中的特定頁面。 您也會瞭解如何使用網站管理 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 4341f5b1-6fe5-44c5-8b8a-18fa84f80177
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: a2c2140631d59a7f8b21aa73613a92ea5c7a91d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78615574"
---
# <a name="authenticating-users-with-forms-authentication-vb"></a>使用表單驗證驗證使用者 (VB)

由[Microsoft](https://github.com/microsoft)

> 瞭解如何使用 [授權] 屬性來保護 MVC 應用程式中的特定頁面。 您將瞭解如何使用網站管理工具來建立及管理使用者和角色。 您也會瞭解如何設定儲存使用者帳戶和角色資訊的位置。

本教學課程的目的是要說明如何使用表單驗證來保護 ASP.NET MVC 應用程式中的觀點。 您將瞭解如何使用網站管理工具來建立使用者和角色。 您也將瞭解如何防止未經授權的使用者叫用控制器動作。 最後，您將瞭解如何設定儲存使用者名稱和密碼的位置。

#### <a name="using-the-web-site-administration-tool"></a>使用網站管理工具

在進行其他動作之前，我們應該先建立一些使用者和角色。 建立新使用者和角色最簡單的方式，就是利用 Visual Studio 2008 的網站管理工具。 您可以藉由選取 [專案]、[ **ASP.NET**設定] 功能表選項來啟動此工具。 或者，您也可以藉由按一下 hammer 的（有點令人驚訝的）圖示來啟動網站管理工具，這是出現在 [方案總管] 視窗頂端的世界（請參閱 [圖 1]）。

**圖1–啟動網站管理工具**

![clip_image002 [4]](authenticating-users-with-forms-authentication-vb/_static/image1.jpg)

在網站管理工具中，您可以藉由選取 [安全性] 索引標籤來建立新的使用者和角色。按一下 [**建立使用者**] 連結以建立名為 Stephen 的新使用者（請參閱 [圖 2]）。 為 Stephen 使用者提供您想要的任何密碼（例如，*秘密*）。

**圖2–建立新的使用者**

![clip_image004 [4]](authenticating-users-with-forms-authentication-vb/_static/image2.jpg)

您可以藉由先啟用角色並定義一或多個角色來建立新的角色。 按一下 [**啟用角色**] 連結來啟用角色。 接下來，按一下 [**建立或管理角色**] 連結來建立名為 [系統*管理員*] 的角色（請參閱 [圖 3]）。

**圖3–建立新的角色**

![clip_image006 [4]](authenticating-users-with-forms-authentication-vb/_static/image3.jpg)

最後，建立名為 Sally 的新使用者，並在建立 Sally 時，按一下 [建立使用者] 連結並選取 [系統管理員]，將 Sally 與系統管理員角色建立關聯（請參閱 [圖 4]）。

**圖4–將使用者新增至角色**

![clip_image008 [4]](authenticating-users-with-forms-authentication-vb/_static/image4.jpg)

當所有動作都已完成，您應該有兩個名為 Stephen 和 Sally 的新使用者。 您也應該有一個名為 [系統管理員] 的新角色。 Sally 是 Administrators 角色的成員，而 Stephen 則不是。

#### <a name="requiring-authorization"></a>需要授權

您可以要求使用者在使用者叫用控制器動作之前進行驗證，方法是在動作中新增 [授權] 屬性。 您可以將 [授權] 屬性套用至個別的控制器動作，也可以將此屬性套用至整個控制器類別。

例如，[清單 1] 中的控制器會公開名為 CompanySecrets （）的動作。 由於此動作是以 [授權] 屬性裝飾，因此除非使用者經過驗證，否則無法叫用此動作。

**清單1– Controllers\HomeController.vb**

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample1.vb)]

如果您藉由在瀏覽器的網址列中輸入 URL/Home/CompanySecrets 來叫用 CompanySecrets （）動作，而且您不是已驗證的使用者，則系統會自動將您重新導向至登入視圖（請參閱 [圖 5]）。

**[圖 5] –登入視圖**

![clip_image010 [4]](authenticating-users-with-forms-authentication-vb/_static/image5.jpg)

您可以使用登入視圖來輸入您的使用者名稱和密碼。 如果您不是已註冊的使用者，則可以按一下 [**註冊**] 連結以流覽至 [註冊] 視圖（請參閱 [圖 6]）。 您可以使用 [註冊] 視圖來建立新的使用者帳戶。

**圖6–註冊視圖**

![clip_image012](authenticating-users-with-forms-authentication-vb/_static/image6.jpg)

成功登入之後，您可以看到 [CompanySecrets] 視圖（請參閱 [圖 7]）。 根據預設，您會繼續登入，直到您關閉瀏覽器視窗為止。

**圖7– CompanySecrets 視圖**

![clip_image014](authenticating-users-with-forms-authentication-vb/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a>依使用者名稱或使用者角色授權

您可以使用 [授權] 屬性，將控制器動作的存取限制為一組特定的使用者或一組特定的使用者角色。 例如，[清單 2] 中修改後的主控制器包含兩個名為 StephenSecrets （）和 AdministratorSecrets （）的新動作。

**清單2– Controllers\HomeController.vb**

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample2.vb)]

只有具有使用者名稱 Stephen 的使用者可以叫用 StephenSecrets （）動作。 所有其他使用者都會被重新導向至登入視圖。 Users 屬性會接受以逗號分隔的使用者帳戶名稱清單。

只有系統管理員（Administrators）角色中的使用者可以叫用 AdministratorSecrets （）動作。 例如，因為 Sally 是 Administrators 群組的成員，所以她可以叫用 AdministratorSecrets （）動作。 所有其他使用者都會被重新導向至登入視圖。 [角色] 屬性會接受以逗號分隔的角色名稱清單。

#### <a name="configuring-authentication"></a>設定驗證

此時，您可能會想知道使用者帳戶和角色資訊的儲存位置。 根據預設，資訊會儲存在位於 MVC 應用程式之應用程式\_Data 資料夾中名為 ASPNETDB.MDF 的（RANU） SQL Express 資料庫中。 當您開始使用成員資格時，ASP.NET 架構會自動產生此資料庫。

若要在 [方案總管] 視窗中看到 ASPNETDB.MDF .mdf 資料庫，您必須先選取 [功能表選項] [專案]、[顯示所有檔案]。

在開發應用程式時，使用預設的 SQL Express 資料庫是正常的。 不過，最有可能的情況是，您不會想要針對生產應用程式使用預設的 ASPNETDB.MDF .mdf 資料庫。 在這種情況下，您可以藉由完成下列兩個步驟來變更儲存使用者帳戶資訊的位置：

1. 將應用程式服務資料庫物件新增至您的生產環境資料庫-變更應用程式連接字串以指向您的實際執行資料庫

第一個步驟是將所有必要的資料庫物件（資料表和預存程式）新增至您的生產環境資料庫。 將這些物件新增至新資料庫的最簡單方式，就是利用 ASP.NET SQL Server 安裝程式 Wizard （請參閱 [圖 8]）。 您可以從 Microsoft Visual Studio 2008 程式群組開啟 Visual Studio 2008 命令提示字元，並從命令提示字元執行下列命令，以啟動此工具：

aspnet\_regsql

**圖8– ASP.NET SQL Server 安裝程式 Wizard**

![clip_image016](authenticating-users-with-forms-authentication-vb/_static/image8.jpg)

[ASP.NET SQL Server 安裝程式] 會讓您選取網路上的 SQL Server 資料庫，並安裝 ASP.NET 應用程式服務所需的所有資料庫物件。 資料庫伺服器不一定要位於您的本機電腦上。

> [!NOTE]
> 如果您不想使用 [ASP.NET SQL Server 安裝程式]，您可以在下列資料夾中找到用於新增應用程式服務資料庫物件的 SQL 腳本：
> 
> 
> C：\Windows\Microsoft.NET\Framework\v2.0.50727

建立必要的資料庫物件之後，您必須修改 MVC 應用程式所使用的資料庫連接。 修改 web 設定（web.config）檔案中的 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 連接字串，使其指向實際執行的資料庫。 例如，清單3中的已修改連接會指向名為 MyProductionDB 的資料庫（原始 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 連接字串已標記為批註）。

**[清單 3] – web.config**

[!code-xml[Main](authenticating-users-with-forms-authentication-vb/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a>設定資料庫許可權

如果您使用整合式安全性來連接到您的資料庫，則必須將正確的 Windows 使用者帳戶新增為您資料庫的登入。 正確的帳戶取決於您使用的是 ASP.NET 程式開發伺服器還是 Internet Information Services 作為 web 伺服器。 正確的使用者帳戶也取決於您的作業系統。

如果您使用 ASP.NET 程式開發伺服器（Visual Studio 所使用的預設 web 伺服器），則您的應用程式會在 Windows 使用者帳戶的內容中執行。 在此情況下，您必須將您的 Windows 使用者帳戶新增為資料庫伺服器登入。

或者，如果您使用 Internet Information Services，則必須將 ASPNET 帳戶或 NT 授權單位/網路服務帳戶新增為資料庫伺服器登入。 如果您使用的是 Windows XP，請將 ASPNET 帳戶新增為您資料庫的登入。 如果您使用的是較新的作業系統（例如 Windows Vista 或 Windows Server 2008），請新增 NT 授權單位/網路服務帳戶作為資料庫登入。

您可以使用 Microsoft SQL Server Management Studio，將新的使用者帳戶新增至您的資料庫（請參閱 [圖 9]）。

**圖9–建立新的 Microsoft SQL Server 登入**

![clip_image018](authenticating-users-with-forms-authentication-vb/_static/image9.jpg)

建立必要的登入之後，您必須將登入對應至具有正確資料庫角色的資料庫使用者。 按兩下登入，然後選取 [使用者對應] 索引標籤。選取一個或多個應用程式服務資料庫角色。 例如，為了驗證使用者，您必須啟用 aspnet\_成員資格\_BasicAccess 資料庫角色。 若要建立新的使用者，您必須啟用 aspnet\_成員資格\_FullAccess 資料庫角色（請參閱 [圖 10]）。

**圖10–新增應用程式服務資料庫角色**

![clip_image020](authenticating-users-with-forms-authentication-vb/_static/image10.jpg)

#### <a name="summary"></a>總結

在本教學課程中，您已瞭解如何在建立 ASP.NET MVC 應用程式時，使用表單驗證。 首先，您已瞭解如何利用網站管理工具來建立新的使用者和角色。 接下來，您已瞭解如何使用 [授權] 屬性來防止未經授權的使用者叫用控制器動作。 最後，您已瞭解如何設定 MVC 應用程式，以將使用者和角色資訊儲存在生產資料庫中。

> [!div class="step-by-step"]
> [上一頁](preventing-javascript-injection-attacks-cs.md)
> [下一頁](authenticating-users-with-windows-authentication-vb.md)
