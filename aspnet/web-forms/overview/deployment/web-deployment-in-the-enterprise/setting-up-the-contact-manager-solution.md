---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
title: 設定 Contact Manager 解決方案 |Microsoft Docs
author: jrjlee
description: 本主題說明如何下載並設定 Contact Manager 解決方案，以在開發人員工作站上本機執行。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 200b973c-776b-4a9b-9e82-39fda6120a52
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: d9774ee01cb0515d7e733b24baa661f2648bd7c4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78629854"
---
# <a name="setting-up-the-contact-manager-solution"></a>設定連絡管理員解決方案

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題說明如何下載並設定 Contact Manager 解決方案，以在開發人員工作站上本機執行。

## <a name="system-requirements"></a>系統需求

若要在本機執行 Contact Manager 解決方案，以及執行本教學課程中所述的其他工作，您必須在開發人員工作站上安裝此軟體：

- Visual Studio 2010 Service Pack 1、Premium 或旗艦版
- Internet Information Services (IIS) 7.5 Express
- SQL Server Express 2008 R2
- IIS Web Deployment Tool （Web Deploy）2.1 或更新版本
- ASP.NET 4。0
- ASP.NET MVC 3
- .NET Framework 4
- .NET Framework 3.5 SP1

除了 Visual Studio 2010 以外，您還可以透過[Web Platform Installer](https://go.microsoft.com/?linkid=9805118)下載並安裝所有這些產品和元件的最新版本。

## <a name="download-and-extract-the-solution"></a>下載並解壓縮解決方案

您可以從[這裡](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0)的 MSDN 程式碼庫下載 Contact Manager 範例應用程式。

## <a name="configure-and-run-the-solution"></a>設定及執行解決方案

若要在本機電腦上設定並執行 Contact Manager 解決方案，您必須執行下列高階步驟：

1. 如果您還沒有帳戶，請建立已啟用成員資格和角色管理功能的本機 ASP.NET 應用程式服務資料庫。
2. 編輯*web.config*檔案中的連接字串，以指向您的本機 SQL Server Express 實例。
3. 從 Visual Studio 2010 執行解決方案。

本節的其餘部分提供如何完成這些工作的更多指引。

**若要建立應用程式服務資料庫**

1. 開啟 Visual Studio 2010 命令提示字元。 若要這樣做，請在 [**開始**] 功能表上，指向 [**所有程式**]，按一下 [ **Microsoft Visual Studio 2010**]，按一下 [ **Visual Studio Tools**]，然後按一下 **[Visual Studio 命令提示字元（2010）** ]。
2. 在命令提示字元中，輸入下列命令，然後按 Enter 鍵：

    [!code-console[Main](setting-up-the-contact-manager-solution/samples/sample1.cmd)]

    1. 使用 **– C**參數來指定資料庫伺服器的連接字串。
    2. 使用 **– A**參數來指定您想要新增至資料庫的應用程式服務功能。 在此情況下， **m**表示您想要新增成員資格提供者的支援，而**r**則表示您想要加入角色管理員的支援。
    3. 使用 **– d**參數來指定應用程式服務資料庫的名稱。 如果您省略此參數，公用程式會建立預設名稱為**aspnetdb.mdf**的資料庫。
3. 成功建立資料庫之後，命令提示字元就會顯示確認訊息。

    ![](setting-up-the-contact-manager-solution/_static/image1.png)

> [!NOTE]
> 如需 aspnet\_regsql 公用程式的詳細資訊，請參閱[ASP.NET SQL Server 註冊工具（aspnet\_regsql .exe）](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)。

下一個步驟是確定 Contact Manager 解決方案中的連接字串指向 SQL Server Express 的本機實例。

**若要更新連接字串**

1. 在 Visual Studio 2010 中開啟 Contact Manager 解決方案。
2. 在 [**方案總管**] 視窗中，展開 [ **ContactManager** ] 專案，然後按兩下 **[web.config] 節點。**

    > [!NOTE]
    > ContactManager 專案包含兩個*web.config*檔案。 您需要編輯專案層級檔案。

    ![](setting-up-the-contact-manager-solution/_static/image2.png)
3. 在**connectionStrings**元素中，確認名為**microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception**的連接字串指向您的本機 ASP.NET 應用程式服務資料庫。

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample2.xml)]
4. 在 [**方案總管**] 視窗中，展開 [ **ContactManager** ] 專案，然後按兩下 **[web.config] 節點。**

    ![](setting-up-the-contact-manager-solution/_static/image3.png)
5. 在**connectionStrings**元素中，于名為**contactmanager.models.contactmanagercoNtext**的連接字串中，確認 [**資料來源**] 屬性已設定為 SQL Server Express 的本機實例。 您不需要變更連接字串中的任何其他專案。

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample3.xml)]
6. 儲存所有開啟的檔案。

您現在應該已準備好在本機電腦上執行 Contact Manager 解決方案。

> [!NOTE]
> 如果您在沒有先建立應用程式服務資料庫的情況下執行這些步驟，ASP.NET 會在您第一次嘗試建立使用者時建立資料庫。 不過，手動建立資料庫可讓您更充分掌控您想要支援的應用程式服務功能集。

**執行 Contact Manager 解決方案**

1. 在 Visual Studio 2010 中，按 F5。
2. Internet Explorer 會啟動並要求 Contact Manager ASP.NET MVC 3 應用程式的 URL。 根據預設，應用程式會顯示 [**所有連絡人**] 頁面。

    ![](setting-up-the-contact-manager-solution/_static/image4.png)
3. 新增一些連絡人，然後確認應用程式如預期般運作。

    ![](setting-up-the-contact-manager-solution/_static/image5.png)
4. 流覽至 `http://localhost:50114/Account/Register` （如果您要將應用程式裝載在不同的埠上，請調整 URL）。 新增 [使用者名稱]、[電子郵件地址] 和 [密碼]，並確認您能夠成功註冊帳戶。

    ![](setting-up-the-contact-manager-solution/_static/image6.png)
5. 流覽至 `http://localhost:50114/Account/LogOn` （如果您要將應用程式裝載在不同的埠上，請調整 URL）。 確認您能夠使用剛建立的帳戶登入。

    ![](setting-up-the-contact-manager-solution/_static/image7.png)
6. 關閉 Internet Explorer 以停止調試。

## <a name="conclusion"></a>結論

此時，必須將 Contact Manager 解決方案完整設定為在您的本機電腦上執行。 當您逐步執行本教學課程中的其他主題時，您可以使用此解決方案做為參考。

下一個主題：[瞭解專案](understanding-the-project-file.md)檔，說明如何使用 Contact Manager 方案內的自訂 Microsoft Build Engine （MSBuild）專案檔來控制部署程式。

> [!div class="step-by-step"]
> [上一頁](the-contact-manager-solution.md)
> [下一頁](understanding-the-project-file.md)
