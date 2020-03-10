---
uid: identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
title: 在 ASP.NET Identity-ASP.NET 4.x 中變更使用者的主要金鑰
author: Rick-Anderson
description: 在 Visual Studio 2013 中，預設 web 應用程式會使用字串值作為使用者帳戶的金鑰。 ASP.NET Identity 可讓您變更的類型 。
ms.author: riande
ms.date: 09/30/2014
ms.assetid: 44925849-5762-4504-a8cd-8f0cd06f6dc3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 0afea8eacfc646f1489b87629fdb2d437815d88c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584459"
---
# <a name="change-primary-key-for-users-in-aspnet-identity"></a>變更 ASP.NET Identity 中的使用者主索引鍵

由[Tom FitzMacken](https://github.com/tfitzmac)

> 在 Visual Studio 2013 中，預設 web 應用程式會使用字串值作為使用者帳戶的金鑰。 ASP.NET Identity 可讓您變更金鑰的類型，以符合您的資料需求。 例如，您可以將索引鍵的類型從字串變更為整數。
> 
> 本主題說明如何從預設 web 應用程式開始，並將使用者帳戶金鑰變更為整數。 您可以使用相同的修改來在您的專案中執行任何類型的金鑰。 它會示範如何在預設 web 應用程式中進行這些變更，但您可以對自訂應用程式套用類似的修改。 它會顯示使用 MVC 或 Web Forms 時所需的變更。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - Update 2 （或更新版本）的 Visual Studio 2013
> - ASP.NET Identity 2.1 或更新版本

若要執行本教學課程中的步驟，您必須擁有 Visual Studio 2013 Update 2 （或更新版本），以及從 ASP.NET Web 應用程式範本建立的 web 應用程式。 在 Update 3 中變更的範本。 本主題說明如何在 Update 2 和 Update 3 中變更範本。

本主題包含下列各節：

- [變更身分識別使用者類別中的金鑰類型](#userclass)
- [新增使用金鑰類型的自訂身分識別類別](#customclass)
- [將內容類別和使用者管理員變更為使用金鑰類型](#context)
- [變更啟動設定以使用金鑰類型](#startup)
- [針對含 Update 2 的 MVC，請將 AccountController 變更為傳遞金鑰類型](#mvcupdate2)
- [針對包含 Update 3 的 MVC，請變更 AccountController 和 ManageController 以傳遞金鑰類型](#mvcupdate3)
- [針對含 Update 2 的 Web form，變更帳戶頁面以傳遞金鑰類型](#webformsupdate2)
- [針對包含 Update 3 的 Web form，變更帳戶頁面以傳遞金鑰類型](#webformsupdate3)
- [執行應用程式](#run)
- [其他資源](#other)

<a id="userclass"></a>
## <a name="change-the-type-of-the-key-in-the-identity-user-class"></a>變更身分識別使用者類別中的金鑰類型

在您從 ASP.NET Web 應用程式範本建立的專案中，指定 ApplicationUser 類別針對使用者帳戶的索引鍵使用整數。 在 IdentityModels.cs 中，變更 ApplicationUser 類別，使其繼承自 TKey 泛型參數類型為**int**的 IdentityUser。 您也會傳遞您尚未實行之三個自訂類別的名稱。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample1.cs?highlight=1-2)]

您已變更金鑰的類型，但根據預設，應用程式的其餘部分仍會假設索引鍵為字串。 您必須在採用字串的程式碼中明確指出金鑰的類型。

在**ApplicationUser**類別中，將**GenerateUserIdentityAsync**方法變更為包含 int，如下列反白顯示的程式碼所示。 具有 Update 3 範本的 Web form 專案不需要進行這種變更。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample2.cs?highlight=2)]

<a id="customclass"></a>
## <a name="add-customized-identity-classes-that-use-the-key-type"></a>新增使用金鑰類型的自訂身分識別類別

其他身分識別類別，例如 IdentityUserRole、IdentityUserClaim、IdentityUserLogin、IdentityRole、UserStore、RoleStore，仍然會設定為使用字串索引鍵。 建立這些類別的新版本，以指定索引鍵的整數。 您不需要在這些類別中提供大量的實作為程式碼，您主要只是將 int 設定為索引鍵。

將下列類別新增至您的 IdentityModels.cs 檔案。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample3.cs)]

<a id="context"></a>
## <a name="change-the-context-class-and-user-manager-to-use-the-key-type"></a>將內容類別和使用者管理員變更為使用金鑰類型

在 IdentityModels.cs 中，變更 **[applicationdbcoNtext]** 類別的定義，以使用新的自訂類別和金鑰的**int** ，如反白顯示的程式碼所示。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample4.cs?highlight=1-2)]

ThrowIfV1Schema 參數在此函式中已不再有效。 變更此函式，使其不會傳遞 ThrowIfV1Schema 值。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample5.cs)]

開啟 IdentityConfig.cs，然後變更**ApplicationUserManger**類別，以使用新的使用者存放區類別來保存資料，並將金鑰設為**int** 。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample6.cs?highlight=1,3,12,14,32,37,48)]

在 Update 3 範本中，您必須變更 ApplicationSignInManager 類別。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample7.cs?highlight=1)]

<a id="startup"></a>
## <a name="change-start-up-configuration-to-use-the-key-type"></a>變更啟動設定以使用金鑰類型

在 Startup.Auth.cs 中，取代 OnValidateIdentity 程式碼，如下所示。 請注意，getUserIdCallback 定義會將字串值剖析成整數。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample8.cs?highlight=7-12)]

如果您的專案無法辨識**GetUserId**方法的一般執行，您可能需要將 ASP.NET Identity NuGet 套件更新為2.1 版

您對 ASP.NET Identity 所使用的基礎結構類別進行了許多變更。 如果您嘗試編譯專案，您會發現很多錯誤。 幸運的是，其餘的錯誤全都很類似。 識別類別的索引鍵必須是整數，但控制器（或 Web Form）會傳遞字串值。 在每個案例中，您都需要呼叫**GetUserId&lt;int&gt;** ，從字串轉換為和整數。 您可以從編譯完成錯誤清單，或遵循下列變更。

其餘的變更取決於您要建立的專案類型，以及您在 Visual Studio 中安裝的更新。 您可以透過下列連結直接前往相關章節

- [針對含 Update 2 的 MVC，請將 AccountController 變更為傳遞金鑰類型](#mvcupdate2)
- [針對包含 Update 3 的 MVC，請變更 AccountController 和 ManageController 以傳遞金鑰類型](#mvcupdate3)
- [針對含 Update 2 的 Web form，變更帳戶頁面以傳遞金鑰類型](#webformsupdate2)
- [針對包含 Update 3 的 Web form，變更帳戶頁面以傳遞金鑰類型](#webformsupdate3)

<a id="mvcupdate2"></a>
## <a name="for-mvc-with-update-2-change-the-accountcontroller-to-pass-the-key-type"></a>針對含 Update 2 的 MVC，請將 AccountController 變更為傳遞金鑰類型

開啟 AccountController.cs 檔案。 您需要變更下列方法。

**ConfirmEmail**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample9.cs?highlight=1,3)]

取消**關聯**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample10.cs?highlight=5,9)]

**管理（ManageUserViewModel）** 方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample11.cs?highlight=11,17,41)]

**LinkLoginCallback**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample12.cs?highlight=10)]

**RemoveAccountList**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample13.cs?highlight=3)]

**HasPassword**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample14.cs?highlight=3)]

您現在可以[執行應用程式](#run)，並註冊新的使用者。

<a id="mvcupdate3"></a>
## <a name="for-mvc-with-update-3-change-the-accountcontroller-and-managecontroller-to-pass-the-key-type"></a>針對包含 Update 3 的 MVC，請變更 AccountController 和 ManageController 以傳遞金鑰類型

開啟 AccountController.cs 檔案。 您需要變更下列方法。

**ConfirmEmail**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample15.cs?highlight=1,3)]

**SendCode**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample16.cs?highlight=4)]

開啟 ManageController.cs 檔案。 您需要變更下列方法。

**Index**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample17.cs?highlight=15-17)]

**RemoveLogin**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample18.cs?highlight=3,13,17)]

**AddPhoneNumber**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample19.cs?highlight=9)]

**EnableTwoFactorAuthentication**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample20.cs?highlight=3-4)]

**DisableTwoFactorAuthentication**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample21.cs?highlight=3-4)]

**VerifyPhoneNumber**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample22.cs?highlight=4,18,21)]

**RemovePhoneNumber**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample23.cs?highlight=3,8)]

**ChangePassword**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample24.cs?highlight=10,13)]

**SetPassword**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample25.cs?highlight=5,8)]

**ManageLogins**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample26.cs?highlight=7,12)]

**LinkLoginCallback**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample27.cs?highlight=8)]

**HasPassword**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample28.cs?highlight=3)]

**HasPhoneNumber**方法

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample29.cs?highlight=3)]

您現在可以[執行應用程式](#run)，並註冊新的使用者。

<a id="webformsupdate2"></a>
## <a name="for-web-forms-with-update-2-change-account-pages-to-pass-the-key-type"></a>針對含 Update 2 的 Web form，變更帳戶頁面以傳遞金鑰類型

針對含 Update 2 的 Web form，您必須變更下列頁面。

**Confirm.aspx.cx**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample30.cs?highlight=8)]

**RegisterExternalLogin.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample31.cs?highlight=36)]

**Manage.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample32.cs?highlight=3,22,47,52,69,85,93,98)]

您現在可以[執行應用程式](#run)，並註冊新的使用者。

<a id="webformsupdate3"></a>
## <a name="for-web-forms-with-update-3-change-account-pages-to-pass-the-key-type"></a>針對包含 Update 3 的 Web form，變更帳戶頁面以傳遞金鑰類型

針對具有 Update 3 的 Web form，您必須變更下列頁面。

**Confirm.aspx.cx**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample33.cs?highlight=8)]

**RegisterExternalLogin.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample34.cs?highlight=36)]

**Manage.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample35.cs?highlight=11,27,32,34,82,87,99,108)]

**VerifyPhoneNumber.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample36.cs?highlight=8,23,27)]

**AddPhoneNumber.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample37.cs?highlight=7)]

**ManagePassword.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample38.cs?highlight=11,47,50,68)]

**ManageLogins.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample39.cs?highlight=16,23,32,41,45)]

**TwoFactorAuthenticationSignIn.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample40.cs?highlight=14-15,29,53)]

<a id="run"></a>
## <a name="run-application"></a>執行應用程式

您已完成預設 Web 應用程式範本所需的所有變更。 執行應用程式，並註冊新的使用者。 註冊使用者之後，您會注意到 AspNetUsers 資料表的識別碼資料行是整數。

![新的主要金鑰](change-primary-key-for-users-in-aspnet-identity/_static/image1.png)

如果您先前已使用不同的主鍵建立 ASP.NET Identity 資料表，您需要進行一些額外的變更。 可能的話，只要刪除現有的資料庫即可。 當您執行 web 應用程式並加入新的使用者時，將會使用正確的設計來重新建立資料庫。 如果無法刪除，請執行 code first 遷移來變更資料表。 不過，新的整數主鍵不會設定為資料庫中的 SQL 識別屬性。 您必須以手動方式將 Id 資料行設定為身分識別。

<a id="other"></a>
## <a name="other-resources"></a>其他資源

- [ASP.NET Identity 的自訂儲存體提供者概觀](overview-of-custom-storage-providers-for-aspnet-identity.md)
- [將現有的網站從 SQL 成員資格移轉至 ASP.NET Identity](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [將成員資格和使用者設定檔的通用提供者資料移轉至 ASP.NET Identity](../migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity.md)
- 具有變更之主要金鑰的[範例應用程式](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK)
