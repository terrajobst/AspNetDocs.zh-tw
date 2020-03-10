---
uid: visual-studio/overview/2017/optimize-build-perf
title: 將解決方案的建置效能最佳化
author: AngelosP
description: 將解決方案的建置效能最佳化
ms.author: riande
ms.date: 08/29/2018
msc.type: authoredcontent
ms.openlocfilehash: c1a5cf5e59374b4c0dd7150c5dd62fbde42af555
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622637"
---
# <a name="optimize-build-performance-for-solution"></a><span data-ttu-id="45da6-103">將解決方案的建置效能最佳化</span><span class="sxs-lookup"><span data-stu-id="45da6-103">Optimize build performance for solution</span></span>

<span data-ttu-id="45da6-104">Visual Studio 2017 15.8 或更新版本包含功能表項目： **Build** > **ASP.NET 編譯** > 將**解決方案的組建效能優化**。</span><span class="sxs-lookup"><span data-stu-id="45da6-104">Visual Studio 2017 15.8 or later include a menu item: **Build** > **ASP.NET Compilation** > **Optimize Build Performance for Solution**.</span></span>

![新功能表項目的螢幕擷取畫面](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

<span data-ttu-id="45da6-106">ASP.NET 會在執行時間編譯其 views，這表示 ASP.NET 專案會攜帶編譯器的複本。</span><span class="sxs-lookup"><span data-stu-id="45da6-106">ASP.NET compiles its views at runtime, which means that an ASP.NET project carries with it a copy of the compiler.</span></span> <span data-ttu-id="45da6-107">不過，在開發人員電腦上，當編譯器複本不符合 Visual Studio 的複本時，組建效能會受到每個增量組建1-3 秒的順序影響。</span><span class="sxs-lookup"><span data-stu-id="45da6-107">However on a developer machine when the copy of the compiler doesn't match Visual Studio's copy, build performance is impacted on the order of 1-3 seconds per incremental build.</span></span> <span data-ttu-id="45da6-108">這項功能會更新您專案的編譯器複本，以符合 Visual Studio 的，這通常會加速增量組建。</span><span class="sxs-lookup"><span data-stu-id="45da6-108">This feature updates your project's copy of the compiler to match Visual Studio's, which usually speeds up incremental builds.</span></span>

<span data-ttu-id="45da6-109">**這僅適用于 ASP.NET Framework 4.7.1 或更新版本的專案，不適用於 ASP.NET Core。**</span><span class="sxs-lookup"><span data-stu-id="45da6-109">**This is applicable to ASP.NET Framework 4.7.1 or later projects only, it does not apply to ASP.NET Core.**</span></span>
