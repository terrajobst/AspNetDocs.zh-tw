---
uid: webhooks/diagnostics/debugging
title: ASP.NET Webhook 調試 |Microsoft Docs
author: rick-anderson
description: 如何 debug ASP.NET Webhook。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 517d282fc22703b5861b748aea51023fa0a12a26
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640865"
---
# <a name="aspnet-webhooks-debugging"></a><span data-ttu-id="189d9-103">ASP.NET Webhook 的調試</span><span class="sxs-lookup"><span data-stu-id="189d9-103">ASP.NET WebHooks debugging</span></span>  

## <a name="debugging-in-azure"></a><span data-ttu-id="189d9-104">在 Azure 中進行調試</span><span class="sxs-lookup"><span data-stu-id="189d9-104">Debugging in Azure</span></span>

<span data-ttu-id="189d9-105">若要在 Azure 中執行時，對您的 Web 應用程式進行檢查，請參閱教學課程[使用 Visual Studio 在 Azure App Service 中進行 web 應用程式疑難排解](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)。</span><span class="sxs-lookup"><span data-stu-id="189d9-105">To debug your Web Application while running in Azure, please see the tutorial [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="debugging-with-source-and-symbols"></a><span data-ttu-id="189d9-106">使用來源和符號進行調試</span><span class="sxs-lookup"><span data-stu-id="189d9-106">Debugging with Source and Symbols</span></span>

<span data-ttu-id="189d9-107">除了您自己的程式碼之外，您還可以直接在 Microsoft ASP.NET Webhook 中進行偵錯工具，事實上就是所有 .NET。</span><span class="sxs-lookup"><span data-stu-id="189d9-107">In addition to debugging your own code, it is possible to debug directly into Microsoft ASP.NET WebHooks, and in fact all of .NET.</span></span> <span data-ttu-id="189d9-108">無論您是在本機或遠端進行調試，都可以運作。</span><span class="sxs-lookup"><span data-stu-id="189d9-108">This works regardless of whether you debug locally or remotely.</span></span> <span data-ttu-id="189d9-109">首先，前往 [ **Debug** ]，然後**選擇 [選項和設定**]，設定 Visual Studio 來尋找來源和符號。</span><span class="sxs-lookup"><span data-stu-id="189d9-109">First, configure Visual Studio to find the source and symbols by going to **Debug** and then **Options and Settings**.</span></span> <span data-ttu-id="189d9-110">設定如下所示的選項：</span><span class="sxs-lookup"><span data-stu-id="189d9-110">Set the options like this:</span></span>

![選項和設定](_static/SourceSymbols.png)

<span data-ttu-id="189d9-112">然後，新增[symbolsource.org](http://symbolsource.org)的連結以下載來源和符號。</span><span class="sxs-lookup"><span data-stu-id="189d9-112">Then add a link to [symbolsource.org](http://symbolsource.org) for downloading the source and symbols.</span></span> <span data-ttu-id="189d9-113">移至上方功能表的 [**符號**] 索引標籤，並將下列內容新增為符號位置：</span><span class="sxs-lookup"><span data-stu-id="189d9-113">Go to the **Symbols** tab of the menu above and add the following as a symbol location:</span></span>

```
http://srv.symbolsource.org/pdb/Public
```

<span data-ttu-id="189d9-114">此外，請確定快取目錄具有簡短名稱;否則檔案名可能會變得太長，而導致無法載入符號。</span><span class="sxs-lookup"><span data-stu-id="189d9-114">In addition, make sure that the cache directory has a short name; otherwise the file names can get too long which will cause the symbols to not load.</span></span> <span data-ttu-id="189d9-115">範例路徑為：</span><span class="sxs-lookup"><span data-stu-id="189d9-115">A sample path is:</span></span>

```
C:\SymCache
```

<span data-ttu-id="189d9-116">這些設定看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="189d9-116">The settings should look similar to this:</span></span>

![選項符號檔案位置範例](_static/SymSource.png)
