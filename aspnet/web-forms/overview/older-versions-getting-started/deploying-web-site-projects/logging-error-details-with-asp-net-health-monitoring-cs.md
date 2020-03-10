---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs
title: 使用 ASP.NET 健康情況監視（C#）記錄錯誤詳細資料 |Microsoft Docs
author: rick-anderson
description: Microsoft 的健全狀況監視系統提供簡單且可自訂的方式來記錄各種 web 事件，包括未處理的例外狀況。 本教學課程會逐步解說指派 。
ms.author: riande
ms.date: 06/09/2009
ms.assetid: b1abb452-642a-4ff3-8504-37b85590ff79
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs
msc.type: authoredcontent
ms.openlocfilehash: e52ed94f78d053701771690fce432d5a1d465b62
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641327"
---
# <a name="logging-error-details-with-aspnet-health-monitoring-c"></a>使用 ASP.NET 狀況監控記錄錯誤的詳細資料 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_13_CS.zip)或[下載 PDF](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial13_HealthMonitoring_cs.pdf)

> Microsoft 的健全狀況監視系統提供簡單且可自訂的方式來記錄各種 web 事件，包括未處理的例外狀況。 本教學課程將逐步解說如何設定健全狀況監視系統，以將未處理的例外狀況記錄到資料庫，並透過電子郵件訊息通知開發人員。

## <a name="introduction"></a>簡介

記錄是用來監視已部署應用程式的健康情況，以及診斷可能發生之任何問題的公用程式。 特別重要的是，記錄部署的應用程式中所發生的錯誤，使其可以補救。 每當 ASP.NET 應用程式中發生未處理的例外狀況時，就會引發 `Error` 事件;[先前的教學](processing-unhandled-exceptions-cs.md)課程示範如何藉由建立 `Error` 事件的事件處理常式，來通知開發人員錯誤並記錄其詳細資料。 不過，建立 `Error` 事件處理常式來記錄錯誤的詳細資料，並通知開發人員是不必要的，因為這項工作可由 ASP 執行。NET 的*健全狀況監視系統*。

健全狀況監視系統是在 ASP.NET 2.0 引進，其設計目的是記錄在應用程式或要求存留期間發生的事件，以監視已部署之 ASP.NET 應用程式的健康情況。 健全狀況監視系統所記錄的事件稱為「健康情況*監控事件*」或「 *Web 事件*」，其中包括：

- 應用程式存留期事件，例如應用程式啟動或停止時
- 安全性事件，包括失敗的登入嘗試和失敗的 URL 授權要求
- 應用程式錯誤，包括未處理的例外狀況、檢視狀態剖析例外狀況、要求驗證例外狀況和編譯錯誤，還有其他類型的錯誤。

當健全狀況監視事件引發時，可以記錄到任何數目的指定*記錄來源*。 健全狀況監視系統隨附記錄檔來源，可將 Web 事件記錄到 Microsoft SQL Server 資料庫、Windows 事件記錄檔，或透過電子郵件訊息傳送給其他人。 您也可以建立自己的記錄來源。

健全狀況監視系統記錄的事件以及使用的記錄來源會定義在 `Web.config`中。 只要幾行設定標記，您就可以使用健康情況監控，將所有未處理的例外狀況記錄到資料庫，並透過電子郵件通知您例外。

## <a name="exploring-the-health-monitoring-systems-configuration"></a>探索健全狀況監視系統的設定

健全狀況監視系統的行為是由其設定資訊所定義，位於 `Web.config`的[`<healthMonitoring>` 元素](https://msdn.microsoft.com/library/2fwh2ss9.aspx)中。 此設定區段會定義下列三項重要資訊：

1. 應記錄引發時的健全狀況監視事件，
2. 記錄檔來源，以及
3. （1）中所定義的每個健全狀況監視事件，如何對應到（2）中定義的記錄來源。

這項資訊是透過三個子系設定元素所指定：分別是[`<eventMappings>`](https://msdn.microsoft.com/library/yc5yk01w.aspx)、 [`<providers>`](https://msdn.microsoft.com/library/zaa41kz1.aspx)和[`<rules>`](https://msdn.microsoft.com/library/fe5wyxa0.aspx)。

預設的健全狀況監視系統設定資訊可以在 `%WINDIR%\Microsoft.NET\Framework\version\CONFIG` 資料夾的 `Web.config` 檔案中找到。 此預設設定資訊（為了簡潔起見已移除某些標記）如下所示：

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample1.xml)]

感興趣的健全狀況監視事件會定義在 `<eventMappings>` 元素中，這會為健全狀況監視事件的類別提供易記的名稱。 在上述標記中，`<eventMappings>` 元素會將人類易記名稱「所有錯誤」指派給類型 `WebBaseErrorEvent` 的健全狀況監視事件，並將「失敗」的名稱指定為類型 `WebFailureAuditEvent`的健全狀況監視事件。

`<providers>` 元素會定義記錄檔來源，為其提供易記名稱，並指定任何記錄檔來源特定的設定資訊。 第一個 `<add>` 元素會定義 "EventLogProvider" 提供者，它會使用 `EventLogWebEventProvider` 類別來記錄指定的健全狀況監視事件。 `EventLogWebEventProvider` 類別會將事件記錄到 Windows 事件記錄檔。 第二個 `<add>` 元素會定義 "SqlWebEventProvider" 提供者，它會透過 `SqlWebEventProvider` 類別，將事件記錄到 Microsoft SQL Server 資料庫。 "SqlWebEventProvider" 設定會在其他設定選項中指定資料庫的連接字串（`connectionStringName`）。

`<rules>` 元素會將 `<eventMappings>` 元素中指定的事件對應到 `<providers>` 元素中的記錄來源。 根據預設，ASP.NET web 應用程式會將所有未處理的例外狀況和 audit 失敗記錄到 Windows 事件記錄檔。

## <a name="logging-events-to-a-database"></a>將事件記錄到資料庫

您可以藉由將 `<healthMonitoring>` 區段新增至應用程式的 `Web.config` 檔，以 web 應用程式為基礎來自訂健全狀況監視系統的預設設定。 您可以使用 `<add>` 專案，在 `<eventMappings>`、`<providers>`和 `<rules>` 區段中包含額外的元素。 若要從預設設定中移除設定，請使用 `<remove>` 元素，或使用 `<clear />` 移除其中一個區段中的所有預設值。 讓我們設定書籍審查 web 應用程式，以使用 `SqlWebEventProvider` 類別將所有未處理的例外狀況記錄到 Microsoft SQL Server 資料庫。

`SqlWebEventProvider` 類別是健全狀況監視系統的一部分，並將狀況監控事件記錄到指定的 SQL Server 資料庫。 `SqlWebEventProvider` 類別預期指定的資料庫包含名為 `aspnet_WebEvent_LogEvent`的預存程式。 這個預存程式會傳遞事件的詳細資料，並且負責儲存事件詳細資料。 好消息是，您不需要建立這個預存程式或資料表來儲存事件詳細資料。 您可以使用 [`aspnet_regsql.exe`] 工具，將這些物件新增至您的資料庫。

> [!NOTE]
> 當我們新增了 ASP 的支援時，會在設定[*使用應用程式服務的網站*教學](configuring-a-website-that-uses-application-services-cs.md)課程中討論 `aspnet_regsql.exe` 工具。NET 的應用程式服務。 因此，書籍審查網站的資料庫已經包含 `aspnet_WebEvent_LogEvent` 預存程式，此程式會將事件資訊儲存到名為 `aspnet_WebEvent_Events`的資料表中。

一旦將必要的預存程式和資料表新增至資料庫之後，剩下的工作就是指示健全狀況監視將所有未處理的例外狀況記錄到資料庫中。 將下列標記新增至您網站的 `Web.config` 檔案，即可完成這項工作：

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample2.xml)]

上述的健全狀況監視設定標記會使用 `<clear />` 元素，從 `<eventMappings>`、`<providers>`和 `<rules>` 區段中抹除預先定義的健全狀況監視設定資訊。 然後，它會在每個區段中新增一個專案。

- `<eventMappings>` 元素會定義名為「所有錯誤」的單一健全狀況監視事件，這會在每次發生未處理的例外狀況時引發。
- `<providers>` 元素會定義名為 "SqlWebEventProvider" 的單一記錄來源，其使用 `SqlWebEventProvider` 類別。 `connectionStringName` 屬性已設定為 "ReviewsConnectionString"，這是 `<connectionStrings>` 區段中所定義的連接字串名稱。
- 最後，&lt;規則&gt; 元素表示當「所有錯誤」事件過大幅簡化應該使用 "SqlWebEventProvider" 提供者來記錄它時。

此設定資訊會指示健全狀況監視系統將所有未處理的例外狀況記錄到書籍評論資料庫。

> [!NOTE]
> 只有在伺服器錯誤時才會引發 `WebBaseErrorEvent` 事件;它不會針對 HTTP 錯誤而引發，例如找不到 ASP.NET 資源的要求。 這與 `HttpApplication` 類別的 `Error` 事件的行為不同，這會針對伺服器和 HTTP 錯誤而引發。

若要查看作用中的健全狀況監視系統，請造訪網站並造訪 `Genre.aspx?ID=foo`產生執行階段錯誤。 您應該會看到適當的錯誤頁面，可能是例外狀況詳細資料的黃色螢幕（當您在本機流覽時）或自訂錯誤網頁（當您造訪生產環境中的網站時）。 在幕後，健全狀況監視系統會將錯誤資訊記錄到資料庫中。 `aspnet_WebEvent_Events` 資料表中應該有一筆記錄（請參閱 [**圖 1**]）。此記錄包含剛發生之執行階段錯誤的相關資訊。

[![](logging-error-details-with-asp-net-health-monitoring-cs/_static/image2.png)](logging-error-details-with-asp-net-health-monitoring-cs/_static/image1.png)

**圖 1**：錯誤詳細資料已記錄到 `aspnet_WebEvent_Events` 資料表  
（[按一下以查看完整大小的影像](logging-error-details-with-asp-net-health-monitoring-cs/_static/image3.png)）

### <a name="displaying-the-error-log-in-a-web-page"></a>在網頁中顯示錯誤記錄檔

在網站的目前設定中，健康狀態監視系統會將所有未處理的例外狀況記錄到資料庫中。 不過，健全狀況監視並不提供任何機制來透過網頁來查看錯誤記錄檔。 不過，您可以建立一個 ASP.NET 網頁，從資料庫中顯示此資訊。 （我們很快就會看到，您可以選擇在電子郵件訊息中，將錯誤詳細資料傳送給您。）

如果您建立這類頁面，請確定您採取的步驟只允許授權的使用者查看錯誤詳細資料。 如果您的網站已經採用使用者帳戶，則您可以使用 URL 授權規則，將頁面的存取限制為特定使用者或角色。 如需有關如何根據登入的使用者來授與或限制網頁存取權的詳細資訊，請參閱我的[網站安全性教學](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)課程。

> [!NOTE]
> 後續的教學課程會探索名為 ELMAH 的替代錯誤記錄和通知系統。 ELMAH 包含內建的機制，可從網頁和 RSS 摘要中同時查看錯誤記錄檔。

## <a name="logging-events-to-email"></a>將事件記錄到電子郵件

健全狀況監視系統包含一個記錄來源提供者，可將事件「記錄」至電子郵件訊息。 記錄來源包含在電子郵件訊息內文中記錄到資料庫的相同資訊。 當發生特定的健全狀況監視事件時，您可以使用此記錄來源來通知開發人員。

讓我們更新書籍審查網站的設定，以便在發生例外狀況時收到電子郵件。 為了完成這項作業，我們需要執行三個工作：

1. 設定 ASP.NET web 應用程式以傳送電子郵件。 這是藉由指定透過 `<system.net>` configuration 專案傳送電子郵件訊息的方式來完成。 如需在 ASP.NET 應用程式中傳送電子郵件訊息的詳細資訊，請參閱[在 ASP.NET 中傳送電子郵件](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)和[系統 .NET. Mail 常見問題](http://systemnetmail.com/)。
2. 在 `<providers>` 元素中註冊電子郵件記錄來源提供者，並
3. 將專案新增至 `<rules>` 元素，將「所有錯誤」事件對應至步驟（2）中新增的記錄來源提供者。

健全狀況監視系統包含兩個電子郵件記錄來源提供者類別： `SimpleMailWebEventProvider` 和 `TemplatedMailWebEventProvider`。 [`SimpleMailWebEventProvider` 類別](https://msdn.microsoft.com/library/system.web.management.simplemailwebeventprovider.aspx)會傳送包含事件詳細資料的純文字電子郵件訊息，並提供小型的電子郵件內文自訂。 使用[`TemplatedMailWebEventProvider` 類別](https://msdn.microsoft.com/library/system.web.management.templatedmailwebeventprovider.aspx)，您可以指定 ASP.NET 網頁，其轉譯的標記會用來做為電子郵件訊息的主體。 [`TemplatedMailWebEventProvider` 類別](https://msdn.microsoft.com/library/system.web.management.templatedmailwebeventprovider.aspx)可讓您更有效地控制電子郵件訊息的內容和格式，但需要更多的前期工作，因為您必須建立 ASP.NET 網頁來產生電子郵件訊息的本文。 本教學課程著重于如何使用 `SimpleMailWebEventProvider` 類別。

更新 `Web.config` 檔案中的健全狀況監視系統 `<providers>` 元素，以包含 `SimpleMailWebEventProvider` 類別的記錄檔來源：

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample3.xml)]

上述標記會使用 `SimpleMailWebEventProvider` 類別做為記錄來源提供者，並為其指派易記名稱 "EmailWebEventProvider"。 此外，`<add>` 屬性還包含其他設定選項，例如電子郵件訊息的 [寄件者] 和 [從] 位址。

定義電子郵件記錄來源之後，剩下的工作就是指示健康狀態監視系統使用此來源「記錄」未處理的例外狀況。 這是藉由在 `<rules>` 區段中新增規則來完成：

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample4.xml)]

`<rules>` 區段現在包含兩個規則。 第一個名稱為「電子郵件的所有錯誤」，會將所有未處理的例外狀況傳送至 "EmailWebEventProvider" 記錄來源。 此規則的效果是將網站上錯誤的詳細資料傳送至指定的位址。 「所有錯誤到資料庫」規則會將錯誤詳細資料記錄到網站的資料庫。 因此，每當網站發生未處理的例外狀況時，其詳細資料都會記錄到資料庫，並傳送到指定的電子郵件地址。

[**圖 2** ] 顯示當造訪 `Genre.aspx?ID=foo`時，`SimpleMailWebEventProvider` 類別所產生的電子郵件。

[![](logging-error-details-with-asp-net-health-monitoring-cs/_static/image5.png)](logging-error-details-with-asp-net-health-monitoring-cs/_static/image4.png)

**圖 2**：錯誤詳細資料會在電子郵件訊息中傳送  
（[按一下以查看完整大小的影像](logging-error-details-with-asp-net-health-monitoring-cs/_static/image6.png)）

## <a name="summary"></a>總結

ASP.NET 健全狀況監視系統的設計，是要允許系統管理員監視已部署之 web 應用程式的健全狀況。 當某些動作展開時（例如當應用程式停止時、使用者成功登入網站時，或發生未處理的例外狀況）時，就會引發健康情況監控事件。 這些事件可以記錄到任何數目的記錄來源。 本教學課程示範如何將未處理之例外狀況的詳細資料記錄到資料庫，以及透過電子郵件訊息。

本教學課程著重于使用健全狀況監視來記錄未處理的例外狀況，但請記住，健康情況監視是設計來測量已部署之 ASP.NET 應用程式的整體健全狀況，並包含豐富的健全狀況監視事件和記錄來源在此探索。 還有什麼，您可以在需要時建立自己的健全狀況監視事件和記錄來源。 如果您想要深入瞭解健康情況監視，最好的第一個步驟是閱讀[Erik Reitan](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)的健康情況[監視常見問題](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)。 之後，請參閱[如何：在 ASP.NET 2.0 中使用健全狀況監視](https://msdn.microsoft.com/library/ms998306.aspx)。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [ASP.NET 健康狀態監視總覽](https://msdn.microsoft.com/library/bb398933.aspx)
- [設定和自訂 ASP.NET 的健康情況監視系統](http://dotnetslackers.com/articles/aspnet/ConfiguringAndCustomizingTheHealthMonitoringSystemOfASPNET.aspx)
- [常見問題-ASP.NET 2.0 中的健全狀況監視](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)
- [如何：傳送健全狀況監視通知的電子郵件](https://msdn.microsoft.com/library/ms227553.aspx)
- [如何：在 ASP.NET 中使用健全狀況監視](https://msdn.microsoft.com/library/ms998306.aspx)
- [ASP.NET 中的健康狀態監視](http://aspnet.4guysfromrolla.com/articles/031407-1.aspx)

> [!div class="step-by-step"]
> [上一頁](processing-unhandled-exceptions-cs.md)
> [下一頁](logging-error-details-with-elmah-cs.md)
