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
# <a name="optimize-build-performance-for-solution"></a>將解決方案的建置效能最佳化

Visual Studio 2017 15.8 或更新版本包含功能表項目： **Build** > **ASP.NET 編譯** > 將**解決方案的組建效能優化**。

![新功能表項目的螢幕擷取畫面](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

ASP.NET 會在執行時間編譯其 views，這表示 ASP.NET 專案會攜帶編譯器的複本。 不過，在開發人員電腦上，當編譯器複本不符合 Visual Studio 的複本時，組建效能會受到每個增量組建1-3 秒的順序影響。 這項功能會更新您專案的編譯器複本，以符合 Visual Studio 的，這通常會加速增量組建。

**這僅適用于 ASP.NET Framework 4.7.1 或更新版本的專案，不適用於 ASP.NET Core。**
