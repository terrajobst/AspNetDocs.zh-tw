---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
title: 瞭解 ASP.NET AJAX 驗證和設定檔應用程式服務 |Microsoft Docs
author: scottcate
description: 驗證服務可讓使用者提供認證，以接收驗證 cookie，而閘道服務則允許自訂使用者 。
ms.author: riande
ms.date: 03/14/2008
ms.assetid: 6ab4efb6-aab6-45ac-ad2c-bdec5848ef9e
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
msc.type: authoredcontent
ms.openlocfilehash: cab9acb1ffd75cca87f6c575a6abdd000235828e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640529"
---
# <a name="understanding-aspnet-ajax-authentication-and-profile-application-services"></a>了解 ASP.NET AJAX 驗證與設定檔應用程式服務

由[Scott Cate](https://github.com/scottcate)

[下載 PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial03_MSAjax_ASP.NET_Services_cs.pdf)

> 驗證服務可讓使用者提供認證，以接收驗證 cookie，而是閘道服務，允許 ASP.NET 所提供的自訂使用者設定檔。 使用 ASP.NET AJAX authentication 服務與標準 ASP.NET 表單驗證相容，因此目前使用表單驗證的應用程式（例如使用登入控制項）不會因為升級至 AJAX 驗證服務而中斷。

## <a name="introduction"></a>簡介

作為 .NET Framework 3.5 的一部分，Microsoft 提供了可調整規模的環境升級;不僅提供新的開發環境，還推出了新的語言整合式查詢（LINQ）功能和其他語言增強功能。 此外，其他工具組的一些熟悉功能（尤其是 ASP.NET AJAX 延伸模組）會包含為 .NET Framework 基類庫的第一類成員。 這些延伸模組可啟用許多新的豐富用戶端功能，包括部分呈現頁面，而不需要完整的頁面重新整理、透過用戶端腳本存取 Web 服務的能力（包括 ASP.NET 分析 API），以及廣泛的用戶端 API設計來鏡像 ASP.NET 伺服器端控制項集中所見的許多控制項配置。

本白皮書探討 ASP.NET 分析和表單驗證服務的執行方式，因為它們是由 Microsoft ASP.NET AJAX ExtensionsThe AJAX Extensions 所公開，讓表單驗證非常容易支援，也就是分析服務）是透過 Web 服務 proxy 腳本公開。 AJAX 延伸模組也支援透過 AuthenticationServiceManager 類別的自訂驗證。

本白皮書是以 Visual Studio 2008 和 .NET Framework 3.5 的 Beta 2 版為基礎。 本白皮書也假設您將使用 Visual Studio 2008 Beta 2，而不是 Visual Web Developer Express，並將根據 Visual Studio 的使用者介面提供逐步解說。 有些程式碼範例可能會利用 Visual Web Developer Express 中無法使用的專案範本。

## <a name="profiles-and-authentication"></a>*設定檔和驗證*

Microsoft ASP.NET 設定檔和驗證服務是由 ASP.NET 表單驗證系統提供，而且是 ASP.NET 的標準元件。 ASP.NET AJAX 延伸模組透過腳本 proxy 提供這些服務的腳本存取，其方式是在用戶端 AJAX 程式庫的 Sys.databases 命名空間下相當簡單的模型。

驗證服務可讓使用者提供認證，以接收驗證 cookie，而是閘道服務，允許 ASP.NET 所提供的自訂使用者設定檔。 使用 ASP.NET AJAX authentication 服務與標準 ASP.NET 表單驗證相容，因此目前使用表單驗證的應用程式（例如使用登入控制項）不會因為升級至 AJAX 驗證服務而中斷。

設定檔服務可讓您根據驗證服務所提供的成員資格，自動整合和儲存使用者資料。 儲存的資料是由 web.config 檔案所指定，而各種分析服務提供者會處理資料管理。 就像驗證服務一樣，AJAX 設定檔服務與標準的 ASP.NET 設定檔服務相容，因此包含 AJAX 支援的情況不應中斷目前納入 ASP.NET 設定檔服務功能的頁面。

將 ASP.NET Authentication 和分析服務本身合併到應用程式中，不在此白皮書的範圍內。 如需主題的詳細資訊，請參閱 MSDN Library 參考文章使用[https://msdn.microsoft.com/library/tw292whz.aspx](https://msdn.microsoft.com/library/tw292whz.aspx)的成員資格來管理使用者。 ASP.NET 也包含一個公用程式，可自動設定 SQL Server 的成員資格，這是 ASP.NET 成員資格的預設驗證服務提供者。 如需詳細資訊，請參閱[https://msdn.microsoft.com/library/ms229862(vs.80).aspx](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)的 ASP.NET SQL Server 註冊工具（Aspnet\_regsql 一文）。

## <a name="using-the-aspnet-ajax-authentication-service"></a>*使用 ASP.NET AJAX Authentication 服務*

ASP.NET AJAX Authentication 服務必須在 web.config 檔案中啟用：

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample1.xml)]

驗證服務需要啟用 ASP.NET 表單驗證，而且必須在用戶端瀏覽器上啟用 cookie （因為無 cookie 的會話需要 URL 參數，所以腳本無法啟用無 cookie 的會話）。

一旦啟用並設定 AJAX 驗證服務之後，用戶端腳本就可以立即利用 AuthenticationService 物件。 用戶端腳本主要會想要利用 `login` 方法和 `isLoggedIn` 屬性。 有數個屬性可提供登入方法的預設值，這可以接受大量的參數。

*AuthenticationService 成員*

*登入方法：*

Login （）方法會開始驗證使用者認證的要求。 這個方法是非同步，不會封鎖執行。

*參數：*

| **參數名稱** | **意義** |
| --- | --- |
| userName | 必要。 要驗證的使用者名稱。 |
| 密碼 | 選擇性（預設為 null）。 使用者的密碼。 |
| isPersistent | 選擇性（預設為 false）。 使用者的驗證 cookie 是否應跨會話保存。 若為 false，則使用者會在瀏覽器關閉或會話到期時登出。 |
| redirectUrl | 選擇性（預設為 null）。驗證成功時，要將瀏覽器重新導向至的 URL。 如果此參數為 null 或空字串，則不會進行重新導向。 |
| customInfo | 選擇性（預設為 null）。 此參數目前未使用，保留供未來使用。 |
| loginCompletedCallback | 選擇性（預設為 null）。登入成功完成時所要呼叫的函數。 如果指定，這個參數會覆寫 defaultLoginCompleted 屬性。 |
| failedCallback | 選擇性（預設為 null）。登入失敗時所要呼叫的函數。 如果指定，這個參數會覆寫 defaultFailedCallback 屬性。 |
| userCoNtext | 選擇性（預設為 null）。 應該傳遞至回呼函式的自訂使用者內容資料。 |

*傳回值：*

此函數不包含傳回值。 不過，完成呼叫此函式時，會包含一些行為：

- 如果 `redirectUrl` 參數既不是 null 也不是空字串，則會重新整理或變更目前的頁面。
- 不過，如果參數為 null 或空字串，則會呼叫 `loginCompletedCallback` 參數或 `defaultLoginCompletedCallback` 屬性。
- 如果 web 服務的呼叫失敗，則會呼叫 `defaultFailedCallback` 屬性的 `failedCallback` 參數。

*登出方法：*

登出（）方法會移除認證 cookie，並從 web 應用程式登出目前的使用者。

*參數：*

| **參數名稱** | **意義** |
| --- | --- |
| redirectUrl | 選擇性（預設為 null）。驗證成功時，要將瀏覽器重新導向至的 URL。 如果此參數為 null 或空字串，則不會進行重新導向。 |
| logoutCompletedCallback | 選擇性（預設為 null）。成功完成登出時要呼叫的函式。 如果指定，這個參數會覆寫 defaultLogoutCompleted 屬性。 |
| failedCallback | 選擇性（預設為 null）。登入失敗時所要呼叫的函數。 如果指定，這個參數會覆寫 defaultFailedCallback 屬性。 |
| userCoNtext | 選擇性（預設為 null）。 應該傳遞至回呼函式的自訂使用者內容資料。 |

*傳回值：*

此函數不包含傳回值。 不過，完成呼叫此函式時，會包含一些行為：

- 如果 `redirectUrl` 參數既不是 null 也不是空字串，則會重新整理或變更目前的頁面。
- 不過，如果參數為 null 或空字串，則會呼叫 `logoutCompletedCallback` 參數或 `defaultLogoutCompletedCallback` 屬性。
- 如果 web 服務的呼叫失敗，則會呼叫 `defaultFailedCallback` 屬性的 `failedCallback` 參數。

*defaultFailedCallback 屬性（get、set）：*

如果無法與 web 服務通訊，則此屬性會指定應呼叫的函式。 它應該會接收委派（或函數參考）。

這個屬性所指定的函式參考應該具有下列簽章：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample2.js)]

*參數：*

| **參數名稱** | **意義** |
| --- | --- |
| error | 指定錯誤資訊。 |
| userCoNtext | 指定呼叫 login 或登出函數時所提供的使用者內容資訊。 |
| methodName | 呼叫方法的名稱。 |

*defaultLoginCompletedCallback 屬性（get、set）：*

這個屬性會指定當登入 web 服務呼叫完成時，應該呼叫的函式。 它應該會接收委派（或函數參考）。

這個屬性所指定的函式參考應該具有下列簽章：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample3.js)]

*參數：*

| **參數名稱** | **意義** |
| --- | --- |
| validCredentials | 指定使用者是否提供有效的認證。 `true` 如果使用者成功登入，則為，否則 `false`。 |
| userCoNtext | 指定呼叫登入函數時所提供的使用者內容資訊。 |
| methodName | 呼叫方法的名稱。 |

*defaultLogoutCompletedCallback 屬性（get、set）：*

這個屬性會指定當登出 web 服務呼叫完成時應該呼叫的函式。 它應該會接收委派（或函數參考）。

這個屬性所指定的函式參考應該具有下列簽章：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample4.js)]

*參數：*

| **參數名稱** | **意義** |
| --- | --- |
| result | 這個參數一律會 `null`。它會保留供日後使用。 |
| userCoNtext | 指定呼叫登入函數時所提供的使用者內容資訊。 |
| methodName | 呼叫方法的名稱。 |

*isLoggedIn 屬性（get）：*

這個屬性會取得使用者的目前驗證狀態。它是在頁面要求期間由 ScriptManager 物件所設定。

如果使用者目前已登入，此屬性會傳回 `true`;否則，它會傳回 `false`。

*path 屬性（get、set）：*

這個屬性會以程式設計方式決定驗證 web 服務的位置。 它可以用來覆寫預設驗證提供者，以及在 ScriptManager 控制項的 AuthenticationService 子節點的 Path 屬性中以宣告方式設定一個集合（如需詳細資訊，請參閱使用自訂驗證服務提供者主題）。

請注意，預設驗證服務的位置不會變更。 不過，ASP.NET AJAX 可讓您指定 web 服務的位置，以提供與 ASP.NET AJAX authentication 服務 proxy 相同的類別介面。

另請注意，此屬性不應設定為將腳本要求從目前網站導向的值。 因為目前的應用程式不會收到驗證認證，所以不會有任何用處;此外，基礎 AJAX 的技術不應張貼跨網站要求，而且可能會在用戶端瀏覽器中產生安全性例外狀況。

這個屬性是一個 `String` 物件，代表驗證 web 服務的路徑。

*timeout 屬性（get、set）：*

這個屬性會決定在假設登入要求失敗之前，等候驗證服務的時間長度。 如果等候完成呼叫時，超時時間過期，將會呼叫要求失敗的回呼，而且呼叫將不會完成。

這個屬性是一個 `Number` 物件，代表等候驗證服務結果的毫秒數。

*程式碼範例：登入驗證服務*

下列標記是一個範例 ASP.NET 網頁，其中包含對 AuthenticationService 類別的 login 和登出方法進行簡單的腳本呼叫。

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample5.aspx)]

## <a name="accessing-aspnet-profiling-data-via-ajax"></a>透過 AJAX 存取 ASP.NET 分析資料

ASP.NET 分析服務也會透過 ASP.NET AJAX 延伸模組公開。 由於 ASP.NET 分析服務提供豐富、細微的 API 來儲存和抓取使用者資料，因此這可能是絕佳的生產力工具。

必須在 web.config 中啟用設定檔服務;預設值不是。 若要這麼做，請確定 web.config 中的 `profileService` 子專案已啟用 = true，而且您已指定可以讀取或寫入哪些屬性，如下所示：

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample6.xml)]

您也必須設定設定檔服務。 雖然分析服務的設定不在此白皮書的範圍內，但值得注意的是，設定檔設定中所定義的群組，將可作為組名的子屬性來存取。 例如，在指定了下列設定檔區段的情況下：

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample7.xml)]

用戶端腳本可以存取 Name、Address、Line2、Address、City、Address、Address、.Zip 和 BackgroundColor 當做 ProfileService 類別的 properties 欄位屬性。

一旦設定 AJAX 分析服務，它就會立即在頁面中提供;不過，在使用之前，必須載入一次。

*ProfileService 成員*

*屬性欄位：*

[屬性] 欄位會將所有已設定的設定檔資料公開為可由點運算子名稱慣例參考的子屬性。 屬於屬性群組子系的屬性稱為 [PropertyName]。 在上面顯示的範例設定檔設定中，若要取得使用者的狀態，您可以使用下列識別碼：

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample8.cs)]

*載入方法：*

從伺服器載入選取的清單或所有屬性。

*參數：*

| **參數名稱** | **意義** |
| --- | --- |
| 之 propertynames | 選擇性（預設為 null）。 要從伺服器載入的屬性。 |
| loadCompletedCallback | 選擇性（預設為 null）。 載入完成時要呼叫的函式。 |
| failedCallback | 選擇性（預設為 null）。 發生錯誤時所要呼叫的函數。 |
| userCoNtext | 選擇性（預設為 null）。 要傳遞至回呼函式的內容資訊。 |

Load 函數沒有傳回值。 如果呼叫成功完成，它會呼叫 `loadCompletedCallback` 參數或 `defaultLoadCompletedCallback` 屬性。 如果呼叫失敗，或超時時間已過期，則會呼叫 `failedCallback` 參數或 `defaultFailedCallback` 屬性。

如果未提供 `propertyNames` 參數，則會從伺服器中取出所有讀取設定的屬性。

*儲存方法：*

Save （）方法會將指定的屬性清單（或所有屬性）儲存至使用者的 ASP.NET 設定檔。

*參數：*

| **參數名稱** | **意義** |
| --- | --- |
| 之 propertynames | 選擇性（預設為 null）。 要儲存至伺服器的屬性。 |
| saveCompletedCallback | 選擇性（預設為 null）。 完成儲存時要呼叫的函式。 |
| failedCallback | 選擇性（預設為 null）。 發生錯誤時所要呼叫的函數。 |
| userCoNtext | 選擇性（預設為 null）。 要傳遞至回呼函式的內容資訊。 |

Save 函數沒有傳回值。 如果呼叫成功完成，它會呼叫 `saveCompletedCallback` 參數或 `defaultSaveCompletedCallback` 屬性。 如果呼叫失敗，或超時時間已過期，則會呼叫 `failedCallback` 或 `defaultFailedCallback` 屬性。

如果 `propertyNames` 參數是 null，則會將所有配置檔案屬性傳送至伺服器，而伺服器會決定可以儲存哪些屬性，哪些則不能。

*defaultFailedCallback 屬性（get、set）：*

如果無法與 web 服務通訊，則此屬性會指定應呼叫的函式。 它應該會接收委派（或函數參考）。

這個屬性所指定的函式參考應該具有下列簽章：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample9.js)]

*參數：*

| **參數名稱** | **意義** |
| --- | --- |
| 錯誤 | 指定錯誤資訊。 |
| userCoNtext | 指定呼叫 load 或 save 函數時所提供的使用者內容資訊。 |
| methodName | 呼叫方法的名稱。 |

*defaultSaveCompleted 屬性（get、set）：*

這個屬性會指定在儲存使用者的設定檔資料時，應該呼叫的函式。 它應該會接收委派（或函數參考）。

這個屬性所指定的函式參考應該具有下列簽章：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample10.js)]

*參數：*

| **參數名稱** | **意義** |
| --- | --- |
| numPropsSaved | 指定已儲存的屬性數目。 |
| userCoNtext | 指定呼叫 load 或 save 函數時所提供的使用者內容資訊。 |
| methodName | 呼叫方法的名稱。 |

*defaultLoadCompleted 屬性（get、set）：*

這個屬性會指定在使用者的設定檔資料載入完成時呼叫的函式。 它應該會接收委派（或函數參考）。

這個屬性所指定的函式參考應該具有下列簽章：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample11.js)]

*參數：*

| **參數名稱** | **意義** |
| --- | --- |
| numPropsLoaded | 指定已載入的屬性數目。 |
| userCoNtext | 指定呼叫 load 或 save 函數時所提供的使用者內容資訊。 |
| methodName | 呼叫方法的名稱。 |

*path 屬性（get、set）：*

這個屬性會以程式設計方式決定設定檔 web 服務的位置。 它可以用來覆寫預設的設定檔服務提供者，以及在 ScriptManager 控制項的 ProfileService 子節點的 Path 屬性中以宣告方式設定一個集合。

請注意，預設設定檔服務的位置不會變更。 不過，ASP.NET AJAX 可讓您指定 web 服務的位置，以提供與 ASP.NET AJAX authentication 服務 proxy 相同的類別介面。

另請注意，此屬性不應設定為將腳本要求從目前網站導向的值。 基礎 AJAX 的技術不應張貼跨網站要求，而且可能會在用戶端瀏覽器中產生安全性例外狀況。

這個屬性是一個 `String` 物件，代表設定檔 web 服務的路徑。

*timeout 屬性（get、set）：*

這個屬性會決定在假設載入或儲存要求失敗之前，等候設定檔服務的時間長度。 如果等候完成呼叫時，超時時間過期，將會呼叫要求失敗的回呼，而且呼叫將不會完成。

此屬性是一個 `Number` 物件，代表等候來自設定檔服務之結果的毫秒數。

*程式碼範例：在頁面載入時載入設定檔資料*

下列程式碼會檢查使用者是否已驗證，如果是，將會載入使用者慣用的背景色彩做為網頁的。

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample12.js)]

## <a name="using-a-custom-authentication-service-provider"></a>*使用自訂驗證服務提供者*

ASP.NET AJAX Extensions 可讓您透過自訂的 web 服務公開您的功能，以建立自訂腳本驗證服務提供者。 為了要使用，您的 web 服務必須公開兩個方法，`Login` 和 `Logout`;而且，您必須使用與預設 ASP.NET AJAX Authentication web 服務相同的方法簽章來指定這些方法。

建立自訂 web 服務之後，您必須以宣告方式在頁面上、程式碼中或透過用戶端腳本來指定它的路徑。

*若要以宣告方式設定路徑：*

若要以宣告方式設定路徑，請在 ASP.NET 網頁上包含 ScriptManager 物件的 AuthenticationService 子系：

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample13.aspx)]

*若要在程式碼中設定路徑：*

若要以程式設計方式設定路徑，請透過腳本管理員的實例指定路徑：

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample14.cs)]

*若要在腳本中設定路徑：*

若要在腳本中以程式設計方式設定路徑，請利用 AuthenticationService 類別的 `path` 屬性：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample15.js)]

*自訂驗證的範例 Web 服務*

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample16.aspx)]

## <a name="summary"></a>總結

ASP.NET 服務-特別是程式碼剖析、成員資格和驗證服務-可輕鬆地公開給用戶端瀏覽器上的 JavaScript。 這可讓開發人員順暢地將其用戶端程式代碼與驗證機制整合，而不需視 Updatepanel 之類的控制項來執行繁重的工作。 您也可以利用 web 設定值，從用戶端保護分析資料。預設不提供任何資料，而開發人員必須加入宣告配置檔案屬性。

此外，藉由建立具有對等方法簽章的簡化 web 服務，開發人員可以為這些內部 ASP.NET 服務建立自訂腳本提供者。 這些技術的支援簡化了豐富型用戶端應用程式的開發，同時為開發人員提供各種彈性來符合特定需求。

## <a name="bio"></a>*生物*

Scott Cate 自1997起開始使用 Microsoft Web 技術，而這是 myKB.com （[www.myKB.com](http://www.myKB.com)）的總裁，他專門撰寫以 ASP.NET 為基礎的應用程式，著重于知識庫軟體解決方案。 Scott 可以透過電子郵件聯絡，位於[scott.cate@myKB.com](mailto:scott.cate@myKB.com)或他的[ScottCate.com](http://ScottCate.com)的 blog

> [!div class="step-by-step"]
> [上一頁](understanding-asp-net-ajax-updatepanel-triggers.md)
> [下一頁](understanding-asp-net-ajax-localization.md)
