---
uid: web-forms/videos/how-do-i/how-do-i-write-web-events-to-a-sql-server-database-using-the-sqlwebeventprovider
title: '[How Do I：]使用 SqlWebEventProvider 將 Web 事件寫入 SQL Server 資料庫 |Microsoft Docs'
author: rick-anderson
description: 在這段影片中，Chris Pels 示範如何使用 ASP.NET health monitoring SqlWebEventProvider，將網站中的錯誤記錄到 SQL Server 資料庫。 首先，清除 。
ms.author: riande
ms.date: 08/28/2008
ms.assetid: d4c08844-fe1c-4759-9ec7-66263ba678fb
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-write-web-events-to-a-sql-server-database-using-the-sqlwebeventprovider
msc.type: video
ms.openlocfilehash: 601da044c0c9679526eecaa09256e0100e7ad571
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78636742"
---
# <a name="how-do-i-write-web-events-to-a-sql-server-database-using-the-sqlwebeventprovider"></a><span data-ttu-id="34fef-104">[How Do I：]使用 SqlWebEventProvider 將 Web 事件寫入 SQL Server 資料庫</span><span class="sxs-lookup"><span data-stu-id="34fef-104">[How Do I:] Write Web Events to a SQL Server Database Using the SqlWebEventProvider</span></span>

<span data-ttu-id="34fef-105">依[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="34fef-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="34fef-106">在這段影片中，Chris Pels 示範如何使用 ASP.NET health monitoring SqlWebEventProvider，將網站中的錯誤記錄到 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="34fef-106">In this video Chris Pels shows how to use the ASP.NET health monitoring SqlWebEventProvider to log errors in a web site to a SQL Server database.</span></span> <span data-ttu-id="34fef-107">首先，瞭解 ASP.NET 健康狀態監視中提供者和事件的角色。</span><span class="sxs-lookup"><span data-stu-id="34fef-107">First, learn the role of the provider and events in ASP.NET health monitoring.</span></span> <span data-ttu-id="34fef-108">接下來，請參閱如何使用 aspnet\_regiis 公用程式（用來設定 ASP.NET 成員資格的相同公用程式），利用所需的物件來設定 SQL Server 資料庫來記錄健康情況監視事件。</span><span class="sxs-lookup"><span data-stu-id="34fef-108">Next, see how to configure a SQL Server database with the necessary objects for recording health monitoring events using the aspnet\_regiis utility, the same utility used to configure ASP.NET Membership.</span></span> <span data-ttu-id="34fef-109">然後，瞭解如何在 web.config 檔案中設定健全狀況監視，以將 ASP.NET 網站中的事件記錄到新建立的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="34fef-109">Then, learn how to configure health monitoring in the web.config file to record events in an ASP.NET web site to the newly created SQL Server database.</span></span> <span data-ttu-id="34fef-110">在這項設定中，請參閱 .NET Framework 2.0 中的根 web.config 檔案如何同時定義提供者和事件，以便在設定您的健康情況監視時運用。</span><span class="sxs-lookup"><span data-stu-id="34fef-110">As part of this configuration, see how the root web.config file in the .NET Framework 2.0 has both providers and events defined that can be leveraged when configuring your health monitoring.</span></span> <span data-ttu-id="34fef-111">這些基本概念可讓您建立自訂事件，以將您自己的特定資訊記錄到 ASP.NET 網站中的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="34fef-111">These fundamentals are a base upon which custom events can be created that log your own specific information to a SQL Server database in an ASP.NET web site.</span></span>

[<span data-ttu-id="34fef-112">&#9654;觀看影片（31分鐘）</span><span class="sxs-lookup"><span data-stu-id="34fef-112">&#9654; Watch video (31 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-write-web-events-to-a-sql-server-database-using-the-sqlwebeventprovider)
