---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
title: Contact Manager 解決方案 |Microsoft Docs
author: jrjlee
description: 這一系列的教學課程會使用&#x2014;Contact Manager 解決方案&#x2014;的範例解決方案，來代表具有實際層級的企業規模應用程式 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 4d8c8d19-055b-4b70-9ee1-f748f0db3a01
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: 12ed7827f7392e559e04121386f7cd045de8462b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586265"
---
# <a name="the-contact-manager-solution"></a><span data-ttu-id="7a86a-103">連絡管理員解決方案</span><span class="sxs-lookup"><span data-stu-id="7a86a-103">The Contact Manager Solution</span></span>

<span data-ttu-id="7a86a-104">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="7a86a-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="7a86a-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="7a86a-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="7a86a-106">這一[系列的教學](web-deployment-in-the-enterprise.md)課程會使用&#x2014;Contact Manager 解決方案&#x2014;的範例解決方案，來代表具有實際複雜度層級的企業級應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a86a-106">This [series of tutorials](web-deployment-in-the-enterprise.md) uses a sample solution&#x2014;the Contact Manager solution&#x2014;to represent an enterprise-scale application with a realistic level of complexity.</span></span> <span data-ttu-id="7a86a-107">本主題介紹 Contact Manager 解決方案，說明解決方案的主要元件，並找出在企業環境中將這類應用程式部署至各種目的地平臺的挑戰。</span><span class="sxs-lookup"><span data-stu-id="7a86a-107">This topic introduces the Contact Manager solution, describes the key components of the solution, and identifies the challenges in deploying this kind of application to various destination platforms in an enterprise environment.</span></span>
> 
> <span data-ttu-id="7a86a-108">當您逐步完成這些教學課程中的主題時，您可以使用 Contact Manager 解決方案做為參考，以示範如何滿足企業部署案例中的特定挑戰。</span><span class="sxs-lookup"><span data-stu-id="7a86a-108">As you work through the topics in these tutorials, you can use the Contact Manager solution as a reference implementation that demonstrates how you can meet specific challenges in enterprise deployment scenarios.</span></span> <span data-ttu-id="7a86a-109">下一個主題[設定 Contact Manager 解決方案](setting-up-the-contact-manager-solution.md)，說明如何在開發人員工作站上下載並執行解決方案。</span><span class="sxs-lookup"><span data-stu-id="7a86a-109">The next topic, [Setting Up the Contact Manager Solution](setting-up-the-contact-manager-solution.md), describes how to download and run the solution on your developer workstation.</span></span>

## <a name="solution-overview"></a><span data-ttu-id="7a86a-110">方案概觀</span><span class="sxs-lookup"><span data-stu-id="7a86a-110">Solution Overview</span></span>

<span data-ttu-id="7a86a-111">Contact Manager 解決方案包含四個個別的專案：</span><span class="sxs-lookup"><span data-stu-id="7a86a-111">The Contact Manager solution consists of four individual projects:</span></span>

![](the-contact-manager-solution/_static/image1.png)

- <span data-ttu-id="7a86a-112">**ContactManager。**</span><span class="sxs-lookup"><span data-stu-id="7a86a-112">**ContactManager.Mvc**.</span></span> <span data-ttu-id="7a86a-113">這是 ASP.NET MVC 3 web 應用程式專案，代表解決方案的進入點。</span><span class="sxs-lookup"><span data-stu-id="7a86a-113">This is an ASP.NET MVC 3 web application project that represents the entry point for the solution.</span></span> <span data-ttu-id="7a86a-114">它提供一些基本的 web 應用程式功能，例如提供使用者建立和查看連絡人詳細資料的能力。</span><span class="sxs-lookup"><span data-stu-id="7a86a-114">It offers some basic web application functionality, like providing users with the ability to create and view contact details.</span></span> <span data-ttu-id="7a86a-115">應用程式會依賴 Windows Communication Foundation （WCF）服務來管理連絡人和 ASP.NET 應用程式服務資料庫，以管理驗證和授權。</span><span class="sxs-lookup"><span data-stu-id="7a86a-115">The application relies on a Windows Communication Foundation (WCF) service to manage contacts and an ASP.NET application services database to manage authentication and authorization.</span></span>
- <span data-ttu-id="7a86a-116">**ContactManager. 資料庫**。</span><span class="sxs-lookup"><span data-stu-id="7a86a-116">**ContactManager.Database**.</span></span> <span data-ttu-id="7a86a-117">這是 Visual Studio 資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="7a86a-117">This is a Visual Studio database project.</span></span> <span data-ttu-id="7a86a-118">專案會定義儲存連絡人詳細資料之資料庫的架構。</span><span class="sxs-lookup"><span data-stu-id="7a86a-118">The project defines the schema for a database that stores contact details.</span></span>
- <span data-ttu-id="7a86a-119">**ContactManager. 服務**。</span><span class="sxs-lookup"><span data-stu-id="7a86a-119">**ContactManager.Service**.</span></span> <span data-ttu-id="7a86a-120">這是 WCF web 服務專案。</span><span class="sxs-lookup"><span data-stu-id="7a86a-120">This is a WCF web service project.</span></span> <span data-ttu-id="7a86a-121">WCF 服務會公開一個端點，讓呼叫者可以在**ContactManager**資料庫上執行建立、抓取、更新和刪除（CRUD）作業。</span><span class="sxs-lookup"><span data-stu-id="7a86a-121">The WCF service exposes an endpoint that allows callers to perform create, retrieve, update, and delete (CRUD) operations on the **ContactManager** database.</span></span> <span data-ttu-id="7a86a-122">服務依賴**ContactManager**資料庫和**ContactManager 的 Common .dll**元件。</span><span class="sxs-lookup"><span data-stu-id="7a86a-122">The service relies on the **ContactManager** database and the **ContactManager.Common.dll** assembly.</span></span>
- <span data-ttu-id="7a86a-123">**ContactManager。**</span><span class="sxs-lookup"><span data-stu-id="7a86a-123">**ContactManager.Common**.</span></span> <span data-ttu-id="7a86a-124">這是類別庫專案。</span><span class="sxs-lookup"><span data-stu-id="7a86a-124">This is a class library project.</span></span> <span data-ttu-id="7a86a-125">WCF 服務依賴此元件中定義的類型。</span><span class="sxs-lookup"><span data-stu-id="7a86a-125">The WCF service relies on types defined in this assembly.</span></span>

<span data-ttu-id="7a86a-126">此解決方案也包含名為 Publish 的方案資料夾。</span><span class="sxs-lookup"><span data-stu-id="7a86a-126">The solution also includes a solution folder named Publish.</span></span> <span data-ttu-id="7a86a-127">其中包含各種自訂專案檔和命令檔，可示範如何控制和操作組建和部署程式。</span><span class="sxs-lookup"><span data-stu-id="7a86a-127">This contains various custom project files and command files that demonstrate how you can control and manipulate the build and deployment process.</span></span> <span data-ttu-id="7a86a-128">本教學課程稍後會詳細說明這些功能。</span><span class="sxs-lookup"><span data-stu-id="7a86a-128">These are covered in more detail later in this tutorial.</span></span>

<span data-ttu-id="7a86a-129">在概念層級中，解決方案的元件會與下列內容配合：</span><span class="sxs-lookup"><span data-stu-id="7a86a-129">At a conceptual level, the components of the solution fit together like this:</span></span>

![](the-contact-manager-solution/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="7a86a-130">雖然 ASP.NET MVC 3 web 應用程式使用 ASP.NET 成員資格提供者，但 web 應用程式中的所有頁面都允許匿名存取。</span><span class="sxs-lookup"><span data-stu-id="7a86a-130">While the ASP.NET MVC 3 web application uses the ASP.NET membership provider, all the pages within the web application allow anonymous access.</span></span> <span data-ttu-id="7a86a-131">這顯然不是實際的設定。</span><span class="sxs-lookup"><span data-stu-id="7a86a-131">This is clearly not a realistic configuration.</span></span> <span data-ttu-id="7a86a-132">不過，此解決方案是以這種方式設定，讓您可以更輕鬆地部署及測試解決方案，而不需要設定使用者帳戶和角色。</span><span class="sxs-lookup"><span data-stu-id="7a86a-132">However, the solution is set up in this way to make it easier for you to deploy and test the solution without configuring user accounts and roles.</span></span>

## <a name="deployment-challenges"></a><span data-ttu-id="7a86a-133">部署挑戰</span><span class="sxs-lookup"><span data-stu-id="7a86a-133">Deployment Challenges</span></span>

<span data-ttu-id="7a86a-134">Contact Manager 解決方案說明許多企業部署案例常見的幾種部署挑戰：</span><span class="sxs-lookup"><span data-stu-id="7a86a-134">The Contact Manager solution illustrates several deployment challenges that are common to lots of enterprise deployment scenarios:</span></span>

- <span data-ttu-id="7a86a-135">解決方案包含多個相依專案。</span><span class="sxs-lookup"><span data-stu-id="7a86a-135">The solution consists of multiple dependent projects.</span></span> <span data-ttu-id="7a86a-136">您需要同時部署這些專案。</span><span class="sxs-lookup"><span data-stu-id="7a86a-136">You need to deploy these projects simultaneously.</span></span>
- <span data-ttu-id="7a86a-137">您必須針對每個環境更新連接字串和服務端點，而且在許多情況下，這項資訊將無法供開發人員使用。</span><span class="sxs-lookup"><span data-stu-id="7a86a-137">Connection strings and service endpoints need to be updated for each environment, and in a lot of cases this information will not be available to the developer.</span></span>
- <span data-ttu-id="7a86a-138">當您將**ContactManager**資料庫部署至預備和生產環境時，您需要在後續部署中保留現有的資料。</span><span class="sxs-lookup"><span data-stu-id="7a86a-138">When you deploy the **ContactManager** database to staging and production environments, you need to preserve existing data on subsequent deployments.</span></span>
- <span data-ttu-id="7a86a-139">當您部署 ASP.NET 應用程式服務資料庫時，您需要部署一些設定資料，但省略任何使用者帳戶資料。</span><span class="sxs-lookup"><span data-stu-id="7a86a-139">When you deploy the ASP.NET application services database, you need to deploy some configuration data but omit any user account data.</span></span>
- <span data-ttu-id="7a86a-140">專案包含一些不應部署的檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="7a86a-140">The projects include some files and folders that should not be deployed.</span></span> <span data-ttu-id="7a86a-141">您必須從部署程式中排除這些檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="7a86a-141">You need to exclude these files and folders from the deployment process.</span></span>
- <span data-ttu-id="7a86a-142">解決方案需要支援從 Team Foundation Server （TFS）組建伺服器進行自動化部署。</span><span class="sxs-lookup"><span data-stu-id="7a86a-142">The solution needs to support automated deployment from a Team Foundation Server (TFS) build server.</span></span>

## <a name="conclusion"></a><span data-ttu-id="7a86a-143">結論</span><span class="sxs-lookup"><span data-stu-id="7a86a-143">Conclusion</span></span>

<span data-ttu-id="7a86a-144">本主題提供了 Contact Manager 解決方案的高階總覽，並找出許多企業部署案例通用的一些固有部署挑戰。</span><span class="sxs-lookup"><span data-stu-id="7a86a-144">This topic provided a high-level overview of the Contact Manager solution and identified some of the inherent deployment challenges that are common to lots of enterprise deployment scenarios.</span></span> <span data-ttu-id="7a86a-145">本教學課程中的其餘主題將說明您可以用來滿足這些挑戰的一些技巧。</span><span class="sxs-lookup"><span data-stu-id="7a86a-145">The remaining topics in this tutorial describe some of the techniques you can use to meet these challenges.</span></span>

<span data-ttu-id="7a86a-146">下一個主題[設定 Contact Manager 解決方案](setting-up-the-contact-manager-solution.md)，說明如何在開發人員工作站上下載並執行解決方案。</span><span class="sxs-lookup"><span data-stu-id="7a86a-146">The next topic, [Setting Up the Contact Manager Solution](setting-up-the-contact-manager-solution.md), describes how to download and run the solution on your developer workstation.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7a86a-147">[上一頁](web-deployment-in-the-enterprise.md)
> [下一頁](setting-up-the-contact-manager-solution.md)</span><span class="sxs-lookup"><span data-stu-id="7a86a-147">[Previous](web-deployment-in-the-enterprise.md)
[Next](setting-up-the-contact-manager-solution.md)</span></span>
