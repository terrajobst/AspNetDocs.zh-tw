---
uid: identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
title: ASP.NET Identity：搭配 EntityFramework MySQL 提供者（C#）使用 mysql 儲存體-ASP.NET 4。x
author: maumar
description: 本教學課程說明如何使用 EntityFramework （SQL 用戶端提供者）搭配 MySQL 往往低於，來取代 ASP.NET Identity 的預設資料儲存機制。
ms.author: riande
ms.date: 12/10/2013
ms.assetid: 15253312-a92c-43ba-908e-b5dacd3d08b8
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
msc.type: authoredcontent
ms.openlocfilehash: e89ed139657c5ce9ddcc56879946c62038919483
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584004"
---
# <a name="aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider-c"></a>ASP.NET Identity：使用 MySQL 儲存體搭配 EntityFramework MySQL 提供者（C#）

by [Maurycy Markowski](https://github.com/maumar)、 [Raquel Soares De Almeida](https://github.com/raquelsa)、 [Robert McMurray](https://github.com/rmcmurray)

> 本教學課程說明如何使用 EntityFramework （SQL 用戶端提供者）搭配 MySQL 提供者來取代[**ASP.NET Identity**](introduction-to-aspnet-identity.md)的預設資料儲存機制。

本教學課程將涵蓋下列主題：

- 在 Azure 上建立 MySQL 資料庫
- 使用 Visual Studio 2013 MVC 範本建立 MVC 應用程式
- 設定 EntityFramework 以使用 MySQL 資料庫提供者
- 執行應用程式以驗證結果

在本教學課程結束時，您將會有一個 MVC 應用程式，其中包含的 ASP.NET Identity 存放區會使用裝載于 Azure 中的 MySQL 資料庫。

## <a name="creating-a-mysql-database-instance-on-azure"></a>在 Azure 上建立 MySQL 資料庫實例

1. 登入 [Azure 入口網站](https://go.microsoft.com/fwlink/?linkid=529715&amp;clcid=0x409)。
2. 按一下頁面底部的 [**新增**]，然後選取 [**儲存**]：

    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.png)
3. 在 [**選擇和附加**元件] 中，選取 [ **ClearDB MySQL 資料庫**]，然後按一下框架底部的 [**下一步]** 箭號：

   [按一下下列影像將它展開。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.png)
4. 保留預設的 [**免費**方案]，將**名稱**變更為**IdentityMySQLDatabase**，選取最接近您的區域，然後按一下框架底部的**下一個**箭號：

   [按一下下列影像將它展開。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.png)
5. 按一下 [**購買**] 核取記號，以完成資料庫建立。

   [按一下下列影像將它展開。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.png)
6. 建立資料庫之後，您可以從管理入口網站的 [附加元件] 索引標籤加以管理。 若要取得資料庫的連線資訊，請按一下頁面底部的 [**連接資訊**]：

   [按一下下列影像將它展開。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image10.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image9.png)
7. 按一下 [ **CONNECTIONSTRING** ] 欄位的 [複製] 按鈕並加以儲存，以複製連接字串。您稍後會在本教學課程中針對 MVC 應用程式使用此資訊：

   [按一下下列影像將它展開。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image12.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image11.png)

## <a name="creating-an-mvc-application-project"></a>建立 MVC 應用程式專案

若要完成本教學課程的這一節中的步驟，您必須先安裝 Web 或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[的 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 。 安裝 Visual Studio 之後，請使用下列步驟來建立新的 MVC 應用程式專案：

1. 開啟 Visual Studio 2103。
2. 按一下 [**開始**] 頁面中的 [**新增專案**]，或按一下 [檔案 **] 功能表，** 然後按一下 [**新增專案**]：

   [按一下下列影像將它展開。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.jpg)
3. 當 [**新增專案**] 對話方塊顯示時，在範本清單中展開 [**視覺C#效果**]，然後按一下 [ **web**]，再選取 [ **ASP.NET web 應用程式**]。 將專案命名為**IdentityMySQLDemo** ，然後按一下 **[確定]** ：

   [按一下下列影像將它展開。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image14.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image13.png)
4. 在 [**新增 ASP.NET 專案**] 對話方塊中，選取 [ **MVC** templatewith] 預設選項;這會將**個別使用者帳戶**設定為驗證方法。 按一下 [確定]：

   [按一下下列影像將它展開。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image16.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image15.png)

## <a name="configure-entityframework-to-work-with-a-mysql-database"></a>設定 EntityFramework 以使用 MySQL 資料庫

### <a name="update-the-entity-framework-assembly-for-your-project"></a>更新專案的 Entity Framework 元件

從 Visual Studio 2013 範本建立的 MVC 應用程式包含[EntityFramework 6.0.0](http://www.nuget.org/packages/EntityFramework)套件的參考，但自其發行以來已經更新該元件，其中包含顯著的效能改進。 若要在您的應用程式中使用這些最新的更新，請使用下列步驟。

1. 在 Visual Studio 中開啟您的 MVC 專案。
2. 按一下 [**工具**]，然後按一下 [ **NuGet 套件管理員**]，再按一下 [**套件管理員主控台**]：

   [按一下下列影像將它展開。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image18.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image17.png)
3. [**套件管理員主控台**] 將會出現在 Visual Studio 的底部區段中。 輸入 &quot;**更新-封裝 EntityFramework**&quot;，然後按 enter：

   [按一下下列影像將它展開。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image20.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image19.png)

### <a name="install-the-mysql-provider-for-entityframework"></a>安裝適用于 EntityFramework 的 MySQL 提供者

為了讓 EntityFramework 連線到 MySQL 資料庫，您需要安裝 MySQL 提供者。 若要這麼做，請開啟 [**套件管理員主控台**]，然後輸入 &quot;**Install-Package MySql. Data. 實體-Pre**&quot;，然後按 enter 鍵。

> [!NOTE]
> 這是元件的發行前版本，因此可能會包含 bug。 您不應該在生產環境中使用提供者的發行前版本。

[按一下下列影像將它展開。]

[![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image22.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image21.png)

### <a name="making-project-configuration-changes-to-the-webconfig-file-for-your-application"></a>對應用程式的 web.config 檔案進行專案設定變更

在本節中，您會將 Entity Framework 設定為使用您剛安裝的 MySQL 提供者、註冊 MySQL 提供者 factory，以及從 Azure 新增您的連接字串。

> [!NOTE]
> 下列範例包含 MySql. Data .dll 的特定元件版本。 如果元件版本變更，您將需要以正確的版本修改適當的設定。

1. 在 Visual Studio 2013 中，開啟專案的 web.config 檔案。
2. 找出下列設定，以定義 Entity Framework 的預設資料庫提供者和 factory：

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample1.xml)]
3. 以下列內容取代這些設定，將 Entity Framework 設定為使用 MySQL 提供者：

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample2.xml)]
4. 找出 [&lt;connectionStrings&gt;] 區段，並以下列程式碼取代它，這會定義裝載于 Azure 上的 MySQL 資料庫的連接字串（請注意，providerName 值也已從原始變更）：

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample3.xml?highlight=3-4)]

### <a name="adding-custom-migrationhistory-context"></a>新增自訂 MigrationHistory 內容

Entity Framework Code First 會使用**MigrationHistory**資料表來追蹤模型變更，並確保資料庫架構與概念架構之間的一致性。 不過，根據預設，此資料表不適用於 MySQL，因為主要金鑰太大。 若要解決這種情況，您必須壓縮該資料表的金鑰大小。 若要這樣做，請使用下列步驟：

1. 此資料表的架構資訊是在**HistoryCoNtext**中捕捉，可以修改為任何其他**DbCoNtext**。 若要這麼做，請將名為**MySqlHistoryCoNtext.cs**的新類別檔案新增至專案，並將其內容取代為下列程式碼：

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample4.cs)]
2. 接下來，您必須將 Entity Framework 設定為使用修改過的**HistoryCoNtext**，而不是預設值。 這可以藉由運用以程式碼為基礎的設定功能來完成。 若要這麼做，請將名為**MySqlConfiguration.cs**的新類別檔案新增至您的專案，並將其內容取代為：

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample5.cs)]

### <a name="creating-a-custom-entityframework-initializer-for-applicationdbcontext"></a>建立 [ApplicationdbcoNtext] 的自訂 EntityFramework 初始化運算式

本教學課程中所述的 MySQL 提供者目前不支援 Entity Framework 遷移，因此您必須使用模型初始化運算式，才能連接到資料庫。 由於本教學課程使用 Azure 上的 MySQL 實例，因此您必須建立自訂的 Entity Framework 初始化運算式。

> [!NOTE]
> 如果您要連接到 Azure 上的 SQL Server 實例，或使用裝載于內部部署環境的資料庫，則不需要執行此步驟。

若要建立 MySQL 的自訂 Entity Framework 初始化運算式，請使用下列步驟：

1. 將名為**MySqlInitializer.cs**的新類別檔案新增至專案，並以下列程式碼取代其內容：

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample6.cs?highlight=23)]
2. 開啟專案的**IdentityModels.cs**檔案（位於 [**模型**] 目錄中），並將其內容取代為下列內容：

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample7.cs)]

## <a name="running-the-application-and-verifying-the-database"></a>執行應用程式並驗證資料庫

完成上述各節中的步驟之後，您應該測試您的資料庫。 若要這樣做，請使用下列步驟：

1. 按**Ctrl + F5**以建立並執行 web 應用程式。
2. 按一下頁面頂端的 [**註冊**] 索引標籤：

   [按一下下列影像將它展開。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.jpg)
3. 輸入新的 [使用者名稱] 和 [密碼]，然後按一下 [**註冊**]：

   [按一下下列影像將它展開。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image24.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image23.png)
4. 此時，會在 MySQL 資料庫上建立 ASP.NET Identity 的資料表，並將使用者註冊並登入應用程式：

   [按一下下列影像將它展開。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.jpg)

### <a name="installing-mysql-workbench-tool-to-verify-the-data"></a>安裝 MySQL 工作臺工具來驗證資料

1. 從[mysql 下載頁面](http://dev.mysql.com/downloads/windows/installer/)安裝**mysql 工作臺**工具
2. 在安裝精靈中： [**特徵選取**] 索引標籤上，選取 [**應用程式**區段下的**MySQL 工作臺**]。
3. 啟動應用程式，並使用您在本教學課程乞求所建立的 Azure MySQL 資料庫中的連接字串資料，來新增連接。
4. 建立連接之後，請檢查 IdentityMySQLDatabase 上建立的**ASP.NET Identity**資料表 **。**
5. 您會看到所有 ASP.NET Identity 必要的資料表都已建立，如下圖所示：

   [按一下下列影像將它展開。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.jpg)
6. 檢查**aspnetusers**資料表中的實例，以在您註冊新的使用者時檢查項目。

   [按一下下列影像將它展開。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image26.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image25.png)
