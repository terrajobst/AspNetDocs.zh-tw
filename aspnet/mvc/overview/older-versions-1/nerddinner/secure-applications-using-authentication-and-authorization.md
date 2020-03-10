---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 使用驗證和授權保護應用程式 |Microsoft Docs
author: microsoft
description: 步驟9顯示如何新增驗證和授權來保護我們的 NerdDinner 應用程式，讓使用者必須註冊並登入網站以建立 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8d509c5f15bb4d5014e53b8dc2a736454238e72c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600979"
---
# <a name="secure-applications-using-authentication-and-authorization"></a>保護使用驗證和授權的應用程式

由[Microsoft](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟9，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。
> 
> 步驟9顯示如何新增驗證和授權來保護我們的 NerdDinner 應用程式，讓使用者必須註冊並登入網站以建立新的 dinners，而且只有主控晚餐的使用者可以稍後再編輯。
> 
> 如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。

## <a name="nerddinner-step-9-authentication-and-authorization"></a>NerdDinner 步驟9：驗證和授權

我們的 NerdDinner 應用程式現在會授與網站建立和編輯任何晚餐之詳細資料的能力。 讓我們變更此動作，讓使用者必須註冊並登入網站以建立新的 dinners，並新增限制，如此一來，只有主控晚餐的使用者可以稍後再編輯。

為此，我們將使用驗證和授權來保護應用程式。

### <a name="understanding-authentication-and-authorization"></a>瞭解驗證和授權

*驗證*是識別和驗證存取應用程式之用戶端的身分識別的程式。 更簡單的說，就是識別使用者流覽網站時的「使用者」。 ASP.NET 支援多種方式來驗證瀏覽器使用者。 針對網際網路 web 應用程式，最常見的驗證方法稱為「表單驗證」。 表單驗證可讓開發人員在其應用程式中撰寫 HTML 登入表單，然後驗證使用者針對資料庫或其他密碼認證存放區提交的使用者名稱/密碼。 如果使用者名稱/密碼的組合正確，開發人員就可以要求 ASP.NET 發出加密的 HTTP cookie，以在未來的要求中識別使用者。 我們會使用表單驗證搭配我們的 NerdDinner 應用程式。

「授權」（ *Authorization* ）是判斷已驗證的使用者是否有權存取特定 URL/資源或執行某個動作的程式。 例如，在我們的 NerdDinner 應用程式中，我們會想要授權只有登入的使用者可以存取 */Dinners/Create* URL，並建立新的 Dinners。 我們也會想要新增授權邏輯，讓只有主控晚餐的使用者可以編輯它，並拒絕其他所有使用者的編輯存取。

### <a name="forms-authentication-and-the-accountcontroller"></a>表單驗證和 AccountController

ASP.NET MVC 的預設 Visual Studio 專案範本會在建立新的 ASP.NET MVC 應用程式時，自動啟用表單驗證。 它也會自動將預先建立的帳戶登入頁面執行加入至專案中，這可讓您輕鬆地整合網站內的安全性。

[預設的網站] 主版頁面會在使用者存取時，于網站右上角顯示「登入」連結（未通過驗證）：

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

按一下 [登入] 連結會將使用者帶到 */Account/LogOn* URL：

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

尚未註冊的訪客可以按一下 [註冊] 連結來執行此動作，這會將其帶至 */Account/Register* URL，並允許他們輸入帳戶詳細資料：

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

按一下 [註冊] 按鈕會在 ASP.NET 成員資格系統中建立新的使用者，並使用表單驗證在網站上驗證使用者。

當使用者登入時，網站主要會變更頁面的右上方，以輸出「歡迎 [使用者名稱]！」 訊息並呈現「登出」連結，而不是「登入」。 按一下 [登出] 連結會登出使用者：

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

上述登入、登出和註冊功能會在 AccountController 類別中實作為其建立專案時 Visual Studio 加入至專案中。 AccountController 的 UI 是使用 \Views\Account 目錄內的視圖範本來執行：

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

AccountController 類別會使用 ASP.NET 表單驗證系統來發出加密的驗證 cookie，以及用來儲存和驗證使用者名稱/密碼的 ASP.NET 成員資格 API。 ASP.NET 成員資格 API 是可擴充的，可讓您使用任何密碼認證存放區。 ASP.NET 隨附內建的成員資格提供者，可將使用者名稱/密碼儲存在 SQL 資料庫中，或在 Active Directory 中。

我們可以藉由開啟專案根目錄中的 "web.config" 檔案，並尋找其中的 &lt;成員資格&gt; 區段，設定我們的 NerdDinner 應用程式應使用的成員資格提供者。 建立專案時新增的預設 web.config 會註冊 SQL 成員資格提供者，並將它設定為使用名為 "Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception" 的連接字串來指定資料庫位置。

預設的 "Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception" 連接字串（在 web.config 檔案的 &lt;connectionStrings&gt; 區段中指定）會設定為使用 SQL Express。 它會指向名為 "ASPNETDB.MDF" 的 SQL Express 資料庫。應用程式的 "App\_Data" 目錄底下的 .MDF "。 如果在應用程式中第一次使用成員資格 API 時，此資料庫不存在，則 ASP.NET 會自動建立資料庫，並在其中布建適當的成員資格資料庫架構：

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

如果您想要使用完整的 SQL Server 實例（或連接到遠端資料庫）而不使用 SQL Express，我們只需要更新 web.config 檔案中的 "Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception" 連接字串，並確認適當的成員資格架構已新增至其指向的資料庫。 您可以在 \Windows\Microsoft.NET\Framework\v2.0.50727\ 目錄中執行 "aspnet\_regsql" 公用程式，將成員資格和其他 ASP.NET 應用程式服務的適當架構加入至資料庫。

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a>使用 [授權] 篩選準則授權/Dinners/Create URL

我們不需要撰寫任何程式碼來啟用 NerdDinner 應用程式的安全驗證和帳戶管理。 使用者可以向應用程式註冊新帳戶，以及登入/登出網站。

現在，我們可以將授權邏輯新增至應用程式，並使用訪客的驗證狀態和使用者名稱來控制他們在網站內可以和不能執行的動作。 讓我們從將授權邏輯新增至 DinnersController 類別的「建立」動作方法開始。 具體而言，我們會要求存取 */Dinners/Create* URL 的使用者必須登入。 如果未登入，我們會將它們重新導向至登入頁面，讓他們可以登入。

執行此邏輯相當簡單。 我們只需要將 [授權] 篩選屬性新增至我們的 Create 動作方法，如下所示：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

ASP.NET MVC 支援建立「動作篩選準則」的功能，可用來執行可透過宣告方式套用至動作方法的重複使用邏輯。 [授權] 篩選是 ASP.NET MVC 提供的其中一個內建動作篩選準則，可讓開發人員以宣告方式將授權規則套用至動作方法和控制器類別。

套用時，如果沒有任何參數（如上面所示），[授權] 篩選準則會強制執行動作方法要求的使用者必須登入，而且如果不是，則會自動將瀏覽器重新導向至登入 URL。 執行此重新導向時，原先要求的 URL 會當做 querystring 引數傳遞（例如：/Account/LogOn？ReturnUrl =% 2fDinners% 2fCreate）。 然後，AccountController 會在使用者登入後，將其重新導向回到原始要求的 URL。

[授權] 篩選準則可選擇性地支援指定「使用者」或「角色」內容的能力，此屬性可用來要求使用者必須登入，並在允許的使用者清單中，或是允許的安全性角色的成員。 例如，下列程式碼只允許兩個特定的使用者 "scottgu" 和 "billg" 存取/Dinners/Create URL：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

不過，在程式碼中內嵌特定的使用者名稱，通常是相當不容易維護的。 較好的方法是定義程式碼所檢查的較高層級「角色」，然後使用資料庫或 active directory 系統（讓實際的使用者對應清單從程式碼外部儲存），將使用者對應至角色。 ASP.NET 包含內建角色管理 API，以及一組內建的角色提供者（包括適用于 SQL 和 Active Directory），可協助執行此使用者/角色對應。 然後，我們可以更新程式碼，只允許特定「系統管理員」角色內的使用者存取/Dinners/Create URL：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a>建立 Dinners 時使用 User.Identity.Name 屬性

我們可以使用控制器基類上公開的 User.Identity.Name 屬性，來抓取要求目前登入使用者的使用者名稱。

先前當我們實作為 Create （）動作方法的 HTTP POST 版本時，我們已將晚餐的 "HostedBy" 屬性硬式編碼為靜態字串。 我們現在可以更新此程式碼，改為使用 User.Identity.Name 屬性，並為建立晚餐的主機自動新增一個 RSVP：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

因為我們已將 [授權] 屬性新增至 Create （）方法，所以 ASP.NET MVC 會確保只有在流覽/Dinners/Create URL 的使用者登入網站時，才會執行動作方法。 因此，User.Identity.Name 屬性值一律會包含有效的使用者名稱。

### <a name="using-the-useridentityname-property-when-editing-dinners"></a>編輯 Dinners 時使用 User.Identity.Name 屬性

現在讓我們新增一些授權邏輯，以限制使用者只能編輯其本身所裝載之 dinners 的屬性。

為協助解決此情況，我們會先將「IsHostedBy （使用者名稱）」 helper 方法新增至晚餐物件（在我們稍早建立的 Dinner.cs 部分類別中）。 根據提供的使用者名稱是否與晚餐 HostedBy 屬性相符，此 helper 方法會傳回 true 或 false，並封裝對其執行不區分大小寫字串比較所需的邏輯：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

然後，我們會在 DinnersController 類別內的 Edit （）動作方法中新增 [授權] 屬性。 這可確保使用者必須登入，才能要求 */Dinners/Edit/[id]* URL。

然後，我們可以將程式碼新增至我們的編輯方法，以使用 IsHostedBy （使用者名稱） helper 方法來確認登入的使用者是否符合晚餐主機。 如果使用者不是主機，我們會顯示「InvalidOwner」視圖並結束要求。 執行此動作的程式碼如下所示：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

然後，我們可以在 \Views\Dinners 目錄上按一下滑鼠右鍵，然後選擇 [加入&gt;View] 功能表命令，以建立新的 "InvalidOwner" 視圖。 我們會在其中填入下列錯誤訊息：

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

現在當使用者嘗試編輯他們不擁有的晚餐時，他們會收到錯誤訊息：

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

我們可以對控制器內的 Delete （）動作方法重複相同的步驟，以鎖定刪除 Dinners 的許可權，並確保只有晚餐的主機可以將其刪除。

### <a name="showinghiding-edit-and-delete-links"></a>顯示/隱藏編輯和刪除連結

我們會從詳細資料 URL 連結到 DinnersController 類別的 [編輯] 和 [刪除] 動作方法：

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

目前，我們會顯示 [編輯] 和 [刪除] 動作連結，而不論詳細資料 URL 的訪客是否為晚餐的主機。 讓我們變更此項，如此一來，只有在造訪的使用者是晚餐的擁有者時，才會顯示連結。

DinnersController 內的 Details （）動作方法會抓取晚餐物件，然後將它當做模型物件傳遞至我們的 view 範本：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

我們可以使用 IsHostedBy （）協助程式方法來更新我們的 view 範本，以有條件地顯示/隱藏編輯和刪除連結，如下所示：

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a>後續步驟

現在我們來看一下如何讓已驗證的使用者使用 AJAX 來進行 dinners。

> [!div class="step-by-step"]
> [上一頁](implement-efficient-data-paging.md)
> [下一頁](use-ajax-to-deliver-dynamic-updates.md)
