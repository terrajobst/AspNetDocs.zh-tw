---
uid: identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
title: 將成員資格和使用者設定檔的通用提供者資料C#遷移至 ASP.NET Identity （）-ASP.NET 4。x
author: rustd
description: 本教學課程說明遷移使用現有應用程式 Universal Providers 所建立的使用者和角色資料和使用者設定檔資料時，所需執行的步驟。
ms.author: riande
ms.date: 12/13/2013
ms.custom: seoapril2019
ms.assetid: 2e260430-d13c-4658-bd05-e256fc0d63b8
msc.legacyurl: /identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 31f02a0cec3c531c45c37b7aad8456e01e80b5ea
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616568"
---
# <a name="migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity-c"></a>將成員資格和使用者設定檔的通用提供者資料移轉至 ASP.NET Identity (C#)

by [Pranav 請參閱 rastogi](https://github.com/rustd)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Robert McMurray](https://github.com/rmcmurray)、 [Suhas Joshi](https://github.com/suhasj)

> 本教學課程說明將使用現有應用程式 Universal Providers 建立的使用者和角色資料和使用者設定檔資料移轉至 ASP.NET Identity 模型所需的步驟。 這裡所述用來遷移使用者設定檔資料的方法，也可以在具有 SQL 成員資格的應用程式中使用。

隨著 Visual Studio 2013 的發行，ASP.NET 團隊引進了新的 ASP.NET Identity 系統，而您可以在[這裡](../../index.md)閱讀更多有關該版本的資訊。 本文說明如何將 web 應用程式從[SQL 成員資格遷移至新的身分識別系統](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)，這篇文章說明了如何將遵循提供者模型的現有應用程式遷移至新的身分識別模型，以進行使用者和角色管理。 本教學課程的重點主要在於遷移使用者設定檔資料，並將它緊密地連結到新系統。 遷移使用者和角色資訊類似于 SQL 成員資格。 您也可以在具有 SQL 成員資格的應用程式中使用遷移設定檔資料所遵循的方法。

例如，我們將從使用提供者模型的 Visual Studio 2012 建立的 web 應用程式開始。 接著，我們將新增程式碼以進行設定檔管理、註冊使用者、為使用者新增設定檔資料、遷移資料庫架構，然後將應用程式變更為使用身分識別系統進行使用者和角色管理。 作為遷移的測試，使用 Universal Providers 建立的使用者應該能夠登入，而新的使用者應該能夠註冊。

> [!NOTE]
> 您可以在[https://github.com/suhasj/UniversalProviders-Identity-Migrations](https://github.com/suhasj/UniversalProviders-Identity-Migrations)找到完整的範例。

## <a name="profile-data-migration-summary"></a>分析資料遷移摘要

開始進行遷移之前，讓我們看看在提供者模型中儲存設定檔資料的經驗。 應用程式使用者的設定檔資料可透過多種方式儲存，最常見的情況是使用隨附于 Universal Providers 的內建設定檔提供者。 這些步驟包括

1. 加入具有用來儲存設定檔資料之屬性的類別。
2. 加入擴充 ' ProfileBase ' 的類別，並執行方法來取得使用者的上述設定檔資料。
3. 在*web.config 檔案*中啟用使用預設設定檔提供者，並定義在步驟 #2 中宣告的類別，以用來存取設定檔資訊。

設定檔資訊會以序列化 xml 和二進位資料的形式儲存在資料庫的「設定檔」資料表中。

在遷移應用程式以使用新的 ASP.NET Identity 系統之後，會將設定檔資訊還原序列化，並儲存為使用者類別上的屬性。 然後，每個屬性都可以對應到使用者資料表中的資料行。 這裡的優點是，除了每次存取資料資訊時，這些屬性都可以直接使用 user 類別來處理，而不必序列化/還原序列化資料。

## <a name="getting-started"></a>快速入門

1. 在 Visual Studio 2012 中建立新的 ASP.NET 4.5 Web Forms 應用程式。 目前的範例會使用 Web Forms 範本，但是您也可以使用 MVC 應用程式。  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.jpg)
2. 建立新的資料夾「模型」以儲存設定檔資訊  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.png)
3. 例如，讓我們將使用者的出生日期、城市、高度和權數儲存在設定檔中。 高度和權數會儲存為名為 ' PersonalStats ' 的自訂類別。 若要儲存和抓取設定檔，我們需要一個擴充 ' ProfileBase ' 的類別。 讓我們建立新的類別 ' AppProfile '，以取得並儲存設定檔資訊。

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample1.cs)]
4. 啟用*web.config*檔案中的設定檔。 輸入要用來儲存/取出在步驟 #3 中建立之使用者資訊的類別名稱。

    [!code-xml[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample2.xml)]
5. 在 [帳戶] 資料夾中新增 web forms 頁面，以取得使用者的設定檔資料並加以儲存。 以滑鼠右鍵按一下專案，然後選取 [加入新專案]。 加入具有主版頁面 ' AddProfileData ' 的新 webforms 頁面。 複製 [MainContent] 區段中的下列內容：

    [!code-html[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample3.html)]

   在程式碼後置中新增下列程式碼：

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample4.cs)]

   加入用來定義 AppProfile 類別的命名空間，以移除編譯錯誤。
6. 執行應用程式，並建立使用者名稱為 '**olduser '** 的新使用者。 流覽至 [AddProfileData] 頁面，並加入使用者的設定檔資訊。  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.png)

您可以使用 [伺服器總管] 視窗，確認資料是以序列化 xml 的形式儲存在「設定檔」資料表中。 在 Visual Studio 中，從 [View] 功能表選擇 [伺服器總管]。 在*web.config 檔案*中定義的資料庫應該會有資料連線。 按一下資料連線會顯示不同的子類別。 展開 [資料表] 以顯示資料庫中的不同資料表，然後以滑鼠右鍵按一下 [設定檔]，再選擇 [顯示資料表資料] 來查看設定檔資料表中所儲存的設定檔資料。

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.png)

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image4.png)

## <a name="migrating-database-schema"></a>正在遷移資料庫架構

若要讓現有的資料庫與身分識別系統搭配使用，我們需要更新身分識別資料庫中的架構，以支援我們新增至原始資料庫的欄位。 這可以使用 SQL 腳本來建立新的資料表，並複製現有的資訊來完成。 在 [伺服器總管] 視窗中，展開 [DefaultConnection] 以顯示資料表。 以滑鼠右鍵按一下 [資料表]，然後選取 [新增查詢]

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image5.png)

從[https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt](https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt)貼上 SQL 腳本並加以執行。 如果重新整理 ' DefaultConnection '，我們可以看到新的資料表已加入。 您可以檢查資料表內的資料，以查看該資訊是否已遷移。

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image6.png)

## <a name="migrating-the-application-to-use-aspnet-identity"></a>將應用程式遷移到使用 ASP.NET Identity

1. 安裝 ASP.NET Identity 所需的 Nuget 套件：

    - Microsoft.AspNet.Identity.EntityFramework
    - Microsoft.AspNet.Identity.Owin
    - Microsoft.Owin.Host.SystemWeb
    - Owin. 安全性 Facebook
    - Owin。 Google
    - Owin. Security. MicrosoftAccount
    - Owin. Security. Twitter

   如需有關管理 Nuget 套件的詳細資訊，請參閱[這裡](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog)
2. 若要使用資料表中的現有資料，我們必須建立對應回資料表的模型類別，並在身分識別系統中連結它們。 在身分識別合約中，模型類別應執行在 Identity. Core dll 中定義的介面，或可以擴充 EntityFramework 中的現有介面。 我們將針對角色、使用者登入和使用者宣告使用現有的類別。 我們需要在我們的範例中使用自訂使用者。 以滑鼠右鍵按一下專案，然後建立新資料夾 ' IdentityModels '。 加入新的「使用者」類別，如下所示：

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample5.cs)]

   請注意，' Profileinfo.txt ' 現在是 user 類別上的屬性。 因此，我們可以使用 user 類別直接處理設定檔資料。

從下載來源（ [https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations](https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations) ）複製**IdentityModels**和**IdentityAccount**資料夾中的檔案。 這些包含其餘的模型類別，以及使用 ASP.NET Identity Api 進行使用者和角色管理所需的新頁面。 使用的方法類似 SQL 成員資格，而詳細的說明可以在[這裡](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)找到。

[!INCLUDE[](../../../includes/identity/alter-command-exception.md)]

## <a name="copying-profile-data-to-the-new-tables"></a>將設定檔資料複製到新的資料表

如先前所述，我們需要將設定檔資料表中的 xml 資料還原序列化，並將它儲存在 AspNetUsers 資料表的資料行中。 新的資料行是在上一個步驟的 [使用者] 資料表中建立的，因此，剩下的工作就是將所需的資料填入這些資料行。 若要這樣做，我們將使用主控台應用程式，它會執行一次，以填入 [使用者] 資料表中新建立的資料行。

1. 在現有的解決方案中建立新的主控台應用程式。  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.jpg)
2. 安裝最新版的 Entity Framework 套件。
3. 將上述建立的 web 應用程式新增為主控台應用程式的參考。 若要執行此動作，請以滑鼠右鍵按一下 [專案]，然後按一下 [加入參考]、[方案]、專案，然後按一下 [確定]。
4. 複製 Program.cs 類別中的下列程式碼。 此邏輯會讀取每個使用者的設定檔資料，並將其序列化為 ' Profileinfo.txt ' 物件，並將其儲存回資料庫。

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample6.cs)]

   某些使用的模型是在 web 應用程式專案的 ' IdentityModels ' 資料夾中定義，因此您必須包含對應的命名空間。
5. 上述程式碼適用于在上一個步驟中建立之 web 應用程式專案的 App\_Data 資料夾中的資料庫檔案。 若要參考該檔案，請在主控台應用程式的 app.config 檔案中，使用 web 應用程式的 web.config 中的連接字串來更新連接字串。 也請在 ' AttachDbFilename ' 屬性中提供完整的實體路徑。
6. 開啟命令提示字元，並流覽至上述主控台應用程式的 bin 資料夾。 執行可執行檔，並檢查記錄輸出，如下圖所示。  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.jpg)
7. 在伺服器總管中開啟 ' AspNetUsers ' 資料表，並確認保留屬性的新資料行中的資料。 您應該使用對應的屬性值來更新它們。

## <a name="verify-functionality"></a>驗證功能

使用新加入的成員資格頁面（使用 ASP.NET Identity 來執行），以從舊的資料庫登入使用者。 使用者應該能夠使用相同的認證登入。 嘗試其他功能，例如新增 OAuth、建立新使用者、變更密碼、新增角色、將使用者新增至角色等。

應抓取舊使用者和新使用者的設定檔資料，並將其儲存在使用者資料表中。 不應再參考舊的資料表。

## <a name="conclusion"></a>結論

本文描述的是將使用提供者模型的 web 應用程式遷移至 ASP.NET Identity 成員資格的程式。 本文另外也概述了遷移設定檔資料，讓使用者連結到身分識別系統。 請針對遷移應用程式時所遇到的問題和問題留下意見。

*感謝 Rick Anderson 和 Robert McMurray 來審查文章。*
