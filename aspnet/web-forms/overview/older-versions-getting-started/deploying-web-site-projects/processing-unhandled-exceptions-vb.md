---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-vb
title: 處理未處理的例外狀況（VB） |Microsoft Docs
author: rick-anderson
description: 當生產環境中的 web 應用程式發生執行階段錯誤時，請務必通知開發人員並記錄錯誤，讓它可以在 la 中進行診斷 。
ms.author: riande
ms.date: 06/09/2009
ms.assetid: 051296f0-9519-4e78-835c-d868da13b0a0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-vb
msc.type: authoredcontent
ms.openlocfilehash: 8d2e12af29bd95ce9898fa6a5e81be8b7a761f76
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586062"
---
# <a name="processing-unhandled-exceptions-vb"></a>處理未處理的例外狀況 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[檢視或下載範例程式碼](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-vb/samples) \(英文\) ([如何下載](/aspnet/core/tutorials/index#how-to-download-a-sample))

> 當生產環境中的 web 應用程式發生執行階段錯誤時，請務必通知開發人員並記錄錯誤，以便在稍後的時間點進行診斷。 本教學課程概述 ASP.NET 如何處理執行時間錯誤，並查看在未處理的例外狀況反升至 ASP.NET 執行時間時執行自訂程式碼的一種方式。

## <a name="introduction"></a>簡介

當 ASP.NET 應用程式中發生未處理的例外狀況時，它會向上冒泡至 ASP.NET 執行時間，這會引發 `Error` 事件並顯示適當的錯誤頁面。 有三種不同類型的錯誤頁面：執行階段錯誤的黃色畫面（YSOD）;例外狀況詳細資料 YSOD;和自訂錯誤網頁。 在[先前的教學](displaying-a-custom-error-page-vb.md)課程中，我們已將應用程式設定為使用遠端使用者的自訂錯誤頁面，並針對使用者造訪本機的例外狀況詳細資料 YSOD。

慣用的自訂錯誤頁面若符合網站的外觀與風格，會偏好使用預設的執行階段錯誤 YSOD，但是顯示自訂錯誤頁面只是完整錯誤處理解決方案的一部分。 當應用程式在生產環境中發生錯誤時，請務必讓開發人員收到錯誤的通知，以便他們可以發現例外狀況的原因並加以解決。 此外，也應該記錄錯誤的詳細資料，以便在稍後的時間點檢查並診斷錯誤。

本教學課程會示範如何存取未處理之例外狀況的詳細資料，以便記錄它們和開發人員通知。 之後的兩個教學課程會探索錯誤記錄程式庫，在設定之後，會自動通知開發人員發生執行階段錯誤，並記錄其詳細資料。

> [!NOTE]
> 如果您需要以一些獨特或自訂的方式處理未處理的例外狀況，本教學課程中所檢查的資訊最有用。 在您只需要記錄例外狀況並通知開發人員的情況下，使用錯誤記錄程式庫是一種方式。 接下來的兩個教學課程提供兩個這類程式庫的總覽。

## <a name="executing-code-when-theerrorevent-is-raised"></a>在引發`Error`事件時執行程式碼

事件為物件提供了一種機制，可表示有問題發生，以及另一個物件在回應中執行程式碼。 身為 ASP.NET 的開發人員，您習慣以事件的角度思考。 如果您想要在訪客按一下特定按鈕時執行一些程式碼，您可以為該按鈕的 `Click` 事件建立事件處理常式，並將您的程式碼放在該處。 假設 ASP.NET 執行時間會在發生未處理的例外狀況時引發它的[`Error` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx)，它會遵循記錄錯誤詳細資料的程式碼會進入事件處理常式。 但是，您要如何建立 `Error` 事件的事件處理常式？

`Error` 事件是[`HttpApplication` 類別](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)中，在要求的存留期期間，于 HTTP 管線的特定階段引發的許多事件之一。 例如，`HttpApplication` 類別的[`BeginRequest` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.beginrequest.aspx)會在每個要求開始時引發;當安全性模組識別出要求者時，就會引發它的[`AuthenticateRequest` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)。 這些 `HttpApplication` 事件可讓網頁開發人員在要求的存留期內，于不同的時間點執行自訂邏輯。

`HttpApplication` 事件的事件處理常式可以放在名為 `Global.asax`的特殊檔案中。 若要在您的網站中建立此檔案，請使用全域應用程式類別範本，將新專案新增至您網站的根目錄，其名稱為 `Global.asax`。

[![](processing-unhandled-exceptions-vb/_static/image2.png)](processing-unhandled-exceptions-vb/_static/image1.png)

**圖 1**：將 `Global.asax` 新增至您的 Web 應用程式  
 （[按一下以查看完整大小的影像](processing-unhandled-exceptions-vb/_static/image3.png)）

根據您使用的是 Web 應用程式專案（WAP）還是網站專案（WSP），Visual Studio 所建立之 `Global.asax` 檔案的內容和結構會稍有不同。 使用 WAP 時，會將 `Global.asax` 實作為兩個不同的檔案，`Global.asax` 和 `Global.asax.vb`。 `Global.asax` 檔案只包含參考 `.vb` 檔案的 `@Application` 指示詞;感興趣的事件處理常式會定義在 `Global.asax.vb` 檔案中。 針對 WSPs，只會建立一個檔案，`Global.asax`，而事件處理常式則定義于 `<script runat="server">` 區塊中。

Visual Studio 的全域應用程式類別範本在 WAP 中建立的 `Global.asax` 檔案包含名為 `Application_BeginRequest`、`Application_AuthenticateRequest`和 `Application_Error`的事件處理常式，分別是 `HttpApplication` 事件 `BeginRequest`、`AuthenticateRequest`和 `Error`的事件處理常式。 還有名為 `Application_Start`、`Session_Start`、`Application_End`和 `Session_End`的事件處理常式，這些事件處理常式會在 web 應用程式啟動、新會話啟動時、應用程式結束時，以及會話結束時引發。 在 WSP 中建立的 `Global.asax` 檔案 Visual Studio 只包含 `Application_Error`、`Application_Start`、`Session_Start`、`Application_End`和 `Session_End` 事件處理常式。

> [!NOTE]
> 部署 ASP.NET 應用程式時，您必須將 `Global.asax` 檔案複製到生產環境。 在 WAP 中建立的 `Global.asax.vb` 檔案不需要複製到生產環境，因為此程式碼會編譯成專案的元件。

Visual Studio 的全域應用程式類別範本所建立的事件處理常式並不完整。 您可以藉由將事件處理常式命名為 `Application_EventName`，為任何 `HttpApplication` 事件加入事件處理常式。 例如，您可以將下列程式碼新增至 `Global.asax` 檔案，以建立[`AuthorizeRequest` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx)的事件處理常式：

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample1.vb)]

同樣地，您可以移除不需要的全域應用程式類別範本所建立的任何事件處理常式。 在本教學課程中，我們只需要 `Error` 事件的事件處理常式;請隨意從 `Global.asax` 檔案移除其他事件處理常式。

> [!NOTE]
> *HTTP 模組*提供另一種方式來定義 `HttpApplication` 事件的事件處理常式。 HTTP 模組會建立為類別檔案，該檔案可以直接放在 web 應用程式專案內，或分成不同的類別庫。 因為它們可以分成一個類別庫，所以 HTTP 模組提供更具彈性且可重複使用的模型，以建立 `HttpApplication` 事件處理常式。 雖然 `Global.asax` 檔案是它所在位置的 web 應用程式所特有，但是 HTTP 模組可以編譯成元件，此時將 HTTP 模組加入至網站，就像在 [`Bin`] 資料夾中卸載元件，然後在 `Web.config`中註冊模組一樣簡單。 本教學課程不會探討如何建立和使用 HTTP 模組，但下列兩個教學課程中使用的兩個錯誤記錄程式庫會實作為 HTTP 模組。 如需 HTTP 模組優點的詳細背景，請參閱[使用 Http 模組和處理常式來建立可插入的 ASP.NET 元件](https://msdn.microsoft.com/library/aa479332.aspx)。

## <a name="retrieving-information-about-the-unhandled-exception"></a>正在抓取未處理之例外狀況的相關資訊

此時，我們有一個具有 `Application_Error` 事件處理常式的 global.asax 檔案。 當此事件處理常式執行時，我們需要通知開發人員錯誤，並記錄其詳細資料。 為了完成這些工作，我們必須先決定所引發之例外狀況的詳細資料。 使用伺服器物件的[`GetLastError` 方法](https://msdn.microsoft.com/library/system.web.httpserverutility.getlasterror.aspx)，來抓取導致引發 `Error` 事件之未處理例外狀況的詳細資料。

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample2.vb)]

`GetLastError` 方法會傳回 `Exception`類型的物件，這是 .NET Framework 中所有例外狀況的基底類型。 不過，在上述程式碼中，我會將 `GetLastError` 所傳回的例外狀況物件，轉換成 `HttpException` 物件。 如果因為 ASP.NET 資源處理期間擲回例外狀況而引發 `Error` 事件，則擲回的例外狀況會包裝在 `HttpException`內。 若要取得促使錯誤事件的實際例外狀況，請使用 `InnerException` 屬性。 如果因為 HTTP 例外狀況而引發 `Error` 事件（例如不存在的頁面要求），則會擲回 `HttpException`，但不會發生內部例外狀況。

下列程式碼會使用 `GetLastErrormessage` 來抓取觸發 `Error` 事件之例外狀況的相關資訊，並將 `HttpException` 儲存在名為 `lastErrorWrapper`的變數中。 然後，它會將原始例外狀況的類型、訊息和堆疊追蹤儲存在三個字串變數中，檢查 `lastErrorWrapper` 是否為觸發 `Error` 事件的實際例外狀況（如果是以 HTTP 為基礎的例外狀況），或者它只是處理要求時所擲回之例外狀況的包裝函式。

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample3.vb)]

此時，您已擁有撰寫程式碼所需的所有資訊，以便將例外狀況的詳細資料記錄到資料庫資料表。 您可以針對每個感利率的錯誤詳細資料，建立具有資料行的資料庫資料表-類型、訊息、堆疊追蹤等等，以及其他有用的資訊片段，例如要求的頁面 URL 和目前登入的使用者名稱。 在 `Application_Error` 事件處理常式中，您接著會連接到資料庫，並將記錄插入資料表中。 同樣地，您可以加入程式碼，透過電子郵件將錯誤的開發人員警示。

接下來兩個教學課程中所檢查的錯誤記錄程式庫，提供現成的功能，因此不需要自行建立此錯誤記錄和通知。 不過，為了說明會引發 `Error` 事件，而且 `Application_Error` 事件處理常式可用來記錄錯誤詳細資料，並通知開發人員，讓我們新增程式碼，以在發生錯誤時通知開發人員。

## <a name="notifying-a-developer-when-an-unhandled-exception-occurs"></a>當發生未處理的例外狀況時通知開發人員

當生產環境中發生未處理的例外狀況時，請務必提醒開發小組，讓他們能夠評估錯誤，並判斷需要採取哪些動作。 例如，如果連線到資料庫時發生錯誤，您將需要再次檢查連接字串，或許可以向您的 web 主控公司開啟支援票證。 如果因程式設計錯誤而發生例外狀況，可能需要新增額外的程式碼或驗證邏輯，以避免未來發生這類錯誤。

[`System.Net.Mail` 命名空間](https://msdn.microsoft.com/library/system.net.mail.aspx)中的 .NET Framework 類別，可讓您輕鬆地傳送電子郵件。 [`MailMessage` 類別](https://msdn.microsoft.com/library/system.net.mail.mailmessage.aspx)代表電子郵件訊息，而且具有 `To`、`From`、`Subject`、`Body`和 `Attachments`等屬性。 `SmtpClass` 可用來傳送使用指定 SMTP 伺服器的 `MailMessage` 物件;SMTP 伺服器設定可以用程式設計方式或在 `Web.config file`的[`<system.net>` 元素](https://msdn.microsoft.com/library/6484zdc1.aspx)中以宣告方式指定。 如需在 ASP.NET 應用程式中傳送電子郵件訊息的詳細資訊，請參閱我的文章：[在 ASP.NET 中傳送電子郵件](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)和[系統 .NET. Mail 常見問題](http://systemnetmail.com/)。

> [!NOTE]
> `<system.net>` 元素包含傳送電子郵件時，`SmtpClient` 類別所使用的 SMTP 伺服器設定。 您的 web 主控公司可能有 SMTP 伺服器，可讓您用來從應用程式傳送電子郵件。 如需您在 web 應用程式中應使用之 SMTP 伺服器設定的詳細資訊，請參閱您的 web 主機支援一節。

將下列程式碼新增至 `Application_Error` 事件處理常式，以在發生錯誤時傳送電子郵件給開發人員：

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample4.vb)]

雖然上述程式碼相當冗長，但大部分的程式會建立在傳送給開發人員的電子郵件中出現的 HTML。 程式碼一開始會參考 `GetLastError` 方法所傳回的 `HttpException` （`lastErrorWrapper`）。 要求所引發的實際例外狀況是透過 `lastErrorWrapper.InnerException` 來抓取，並會指派給變數 `lastError`。 類型、訊息和堆疊追蹤資訊會從 `lastError` 取出，並儲存在三個字串變數中。

接下來，會建立名為 `mm` 的 `MailMessage` 物件。 電子郵件內文的格式為 HTML，並顯示要求頁面的 URL、目前登入之使用者的名稱，以及例外狀況的相關資訊（類型、訊息和堆疊追蹤）。 `HttpException` 類別的其中一項很酷的事，就是您可以藉由呼叫[GetHtmlErrorMessage 方法](https://msdn.microsoft.com/library/system.web.httpexception.gethtmlerrormessage.aspx)，產生用來建立例外狀況詳細資料（YSOD）的 HTML。 這裡會使用這個方法來抓取例外狀況詳細資料 YSOD 標記，並將它新增至電子郵件作為附件。 請注意：如果觸發 `Error` 事件的例外狀況是以 HTTP 為基礎的例外狀況（例如不存在的頁面要求），則 `GetHtmlErrorMessage` 方法會傳回 `null`。

最後一個步驟是傳送 `MailMessage`。 這是藉由建立新的 `SmtpClient` 方法並呼叫其 `Send` 方法來完成。

> [!NOTE]
> 在您的 web 應用程式中使用此程式碼之前，您會想要將 `ToAddress` 中的值和 `FromAddress` 常數從 support@example.com 變更為傳送錯誤通知電子郵件的來源電子郵件地址。 您也必須在 `Web.config`的 [`<system.net>`] 區段中指定 SMTP 伺服器設定。 請洽詢您的 web 主機提供者，以判斷要使用的 SMTP 伺服器設定。

當此程式碼隨時都在發生錯誤時，開發人員會傳送一封電子郵件訊息，摘要說明錯誤並包含 YSOD。 在先前的教學課程中，我們示範了執行時間錯誤，方法是造訪內容類型 .aspx，並透過 querystring （例如 `Genre.aspx?ID=foo`）傳入不正確 `ID` 值。 流覽含有 `Global.asax` 檔案的頁面，會產生與上一個教學課程相同的使用者體驗-在開發環境中，您將會繼續看到例外狀況詳細資料的黃色畫面，而在生產環境中，您會看到 [自訂錯誤] 頁面。 除了此現有的行為之外，開發人員也會傳送電子郵件。

[**圖 2** ] 顯示造訪 `Genre.aspx?ID=foo`時收到的電子郵件。 [電子郵件內文] 會匯總例外狀況資訊，而 [`YSOD.htm` 附件] 會顯示 [例外狀況詳細資料] YSOD 中顯示的內容（請參閱 [**圖 3**]）。

[![](processing-unhandled-exceptions-vb/_static/image5.png)](processing-unhandled-exceptions-vb/_static/image4.png)

**圖 2**：每當有未處理的例外狀況時，就會傳送電子郵件通知給開發人員  
 （[按一下以查看完整大小的影像](processing-unhandled-exceptions-vb/_static/image6.png)）

[![](processing-unhandled-exceptions-vb/_static/image8.png)](processing-unhandled-exceptions-vb/_static/image7.png)

**圖 3**：電子郵件通知包含例外狀況詳細資料 YSOD 作為附件  
 （[按一下以查看完整大小的影像](processing-unhandled-exceptions-vb/_static/image9.png)）

## <a name="what-about-using-the-custom-error-page"></a>使用自訂錯誤網頁呢？

本教學課程示範如何使用 `Global.asax` 和 `Application_Error` 事件處理常式，在發生未處理的例外狀況時執行程式碼。 具體而言，我們使用這個事件處理常式來通知開發人員發生錯誤;我們可以將它延伸，以便在資料庫中記錄錯誤詳細資料。 `Application_Error` 事件處理常式的存在並不會影響使用者的體驗。 他們仍然會看到 [設定的錯誤] 頁面，也就是 [錯誤詳細資料] YSOD、[執行時間錯誤] YSOD 或 [自訂錯誤] 頁面。

使用自訂錯誤頁面時，請務必知道 `Global.asax` 檔案和 `Application_Error` 事件是否必要。 發生錯誤時，使用者會顯示在 [自訂錯誤] 頁面上，因此為什麼無法讓程式碼通知開發人員，並將錯誤詳細資料記錄到自訂錯誤頁面的程式碼後置類別中？ 雖然您可以在自訂錯誤頁面的程式碼後置類別中加入程式碼，但在使用我們在先前的教學課程中所探討的技巧時，您無法存取觸發 `Error` 事件之例外狀況的詳細資料。 從自訂錯誤頁面呼叫 `GetLastError` 方法會傳回 `Nothing`。

這種行為的原因是因為透過重新導向來到達自訂錯誤網頁。 當未處理的例外狀況到達 ASP.NET 執行時間時，ASP.NET 引擎會引發它的 `Error` 事件（這會執行 `Application_Error` 事件處理常式），然後藉由發出 `Response.Redirect(customErrorPageUrl)`，將使用者重新*導向*至自訂錯誤網頁。 `Response.Redirect` 方法會將回應傳送至具有 HTTP 302 狀態碼的用戶端，指示瀏覽器要求新的 URL，也就是自訂錯誤網頁。 然後，瀏覽器會自動要求這個新頁面。 您可以告訴，自訂錯誤頁面是從發生錯誤的頁面分開要求，因為瀏覽器的網址列會變更為自訂錯誤網頁 URL （請參閱 [**圖 4**]）。

[![](processing-unhandled-exceptions-vb/_static/image11.png)](processing-unhandled-exceptions-vb/_static/image10.png)

**圖 4**：當發生錯誤時，瀏覽器會重新導向至自訂錯誤網頁 URL  
 （[按一下以查看完整大小的影像](processing-unhandled-exceptions-vb/_static/image12.png)）

最後的結果是，當伺服器回應 HTTP 302 重新導向時，發生未處理的例外狀況的要求就會結束。 後續對自訂錯誤頁面提出的要求是全新的要求;此時，ASP.NET 引擎已捨棄錯誤資訊，而且也無法將前一個要求中未處理的例外狀況與自訂錯誤網頁的新要求產生關聯。 這就是為什麼當從自訂錯誤頁面呼叫時，`GetLastError` 傳回 `null` 的原因。

不過，在導致錯誤的相同要求期間，可能會執行自訂錯誤頁面。 [`Server.Transfer(url)`](https://msdn.microsoft.com/library/system.web.httpserverutility.transfer.aspx)方法會將執行傳輸到指定的 URL，並在相同的要求中進行處理。 您可以將 `Application_Error` 事件處理常式中的程式碼移至自訂錯誤頁面的程式碼後置類別，並以下列程式碼取代 `Global.asax`：

[!code-vb[Main](processing-unhandled-exceptions-vb/samples/sample5.vb)]

現在，當發生未處理的例外狀況時，`Application_Error` 事件處理常式會根據 HTTP 狀態碼，將控制項傳輸至適當的自訂錯誤頁面。 因為已傳輸控制項，所以自訂錯誤頁面可以透過 `Server.GetLastError` 存取未處理的例外狀況資訊，並可通知開發人員錯誤並記錄其詳細資料。 `Server.Transfer` 呼叫會阻止 ASP.NET 引擎將使用者重新導向至自訂錯誤網頁。 相反地，會傳回自訂錯誤頁面的內容做為產生錯誤之頁面的回應。

## <a name="summary"></a>總結

當 ASP.NET web 應用程式中發生未處理的例外狀況時，ASP.NET 執行時間會引發 `Error` 事件，並顯示已設定的錯誤頁面。 我們可以藉由建立錯誤事件的事件處理常式，來通知開發人員錯誤、記錄其詳細資料，或以其他方式處理它。 有兩種方式可以建立事件處理常式，以便在 `Global.asax` 檔案或 HTTP 模組中 `HttpApplication` 事件（例如 `Error`：）。 本教學課程示範如何在 `Global.asax` 檔案中建立 `Error` 事件處理常式，以透過電子郵件訊息通知開發人員發生錯誤。

如果您需要以一些獨特或自訂的方式處理未處理的例外狀況，建立 `Error` 事件處理常式會很有用。 不過，建立您自己的 `Error` 事件處理常式來記錄例外狀況或通知開發人員，並不是最有效率的使用時間，因為已有可用的錯誤記錄程式庫，而且可以在幾分鐘內進行設定。 接下來的兩個教學課程會檢查兩個這類程式庫。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [ASP.NET HTTP 模組和 HTTP 處理常式總覽](https://support.microsoft.com/kb/307985)
- [正常回應未處理的例外狀況-處理未處理的例外狀況](http://aspnet.4guysfromrolla.com/articles/091306-1.aspx)
- [`HttpApplication` 類別和 ASP.NET 應用程式物件](http://www.eggheadcafe.com/articles/20030211.asp)
- [ASP.NET 中的 HTTP 處理常式和 HTTP 模組](http://www.15seconds.com/Issue/020417.htm)
- [在 ASP.NET 中傳送電子郵件](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)
- [瞭解 `Global.asax` 檔案](http://aspalliance.com/1114_Understanding_the_Globalasax_file.all)
- [使用 HTTP 模組和處理常式建立可插入的 ASP.NET 元件](https://msdn.microsoft.com/library/aa479332.aspx)
- [使用 ASP.NET `Global.asax` 檔案](http://articles.techrepublic.com.com/5100-10878_11-5771721.html)
- [使用 `HttpApplication` 實例](https://msdn.microsoft.com/library/a0xez8f2.aspx)

> [!div class="step-by-step"]
> [上一頁](displaying-a-custom-error-page-vb.md)
> [下一頁](logging-error-details-with-asp-net-health-monitoring-vb.md)
