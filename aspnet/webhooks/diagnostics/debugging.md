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
# <a name="aspnet-webhooks-debugging"></a>ASP.NET Webhook 的調試  

## <a name="debugging-in-azure"></a>在 Azure 中進行調試

若要在 Azure 中執行時，對您的 Web 應用程式進行檢查，請參閱教學課程[使用 Visual Studio 在 Azure App Service 中進行 web 應用程式疑難排解](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)。

## <a name="debugging-with-source-and-symbols"></a>使用來源和符號進行調試

除了您自己的程式碼之外，您還可以直接在 Microsoft ASP.NET Webhook 中進行偵錯工具，事實上就是所有 .NET。 無論您是在本機或遠端進行調試，都可以運作。 首先，前往 [ **Debug** ]，然後**選擇 [選項和設定**]，設定 Visual Studio 來尋找來源和符號。 設定如下所示的選項：

![選項和設定](_static/SourceSymbols.png)

然後，新增[symbolsource.org](http://symbolsource.org)的連結以下載來源和符號。 移至上方功能表的 [**符號**] 索引標籤，並將下列內容新增為符號位置：

```
http://srv.symbolsource.org/pdb/Public
```

此外，請確定快取目錄具有簡短名稱;否則檔案名可能會變得太長，而導致無法載入符號。 範例路徑為：

```
C:\SymCache
```

這些設定看起來應該像這樣：

![選項符號檔案位置範例](_static/SymSource.png)
