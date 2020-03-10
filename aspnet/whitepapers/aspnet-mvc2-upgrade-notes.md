---
uid: whitepapers/aspnet-mvc2-upgrade-notes
title: 將 ASP.NET MVC 1.0 應用程式升級至 ASP.NET MVC 2 |Microsoft Docs
author: rick-anderson
description: 本檔說明如何以手動方式升級，並透過 wizard 將 ASP.NET MVC 1.0 應用程式 ASP.NET MVC 2。 本檔也適用于 d 。
ms.author: riande
ms.date: 04/08/2010
ms.assetid: f1a01759-d251-4b09-8835-e112e336c6dd
msc.legacyurl: /whitepapers/aspnet-mvc2-upgrade-notes
msc.type: content
ms.openlocfilehash: 27589f1b1c9d5038118e5ff0cc2e7cecae17d5ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637015"
---
# <a name="upgrading-an-aspnet-mvc-10-application-to-aspnet-mvc-2"></a>將 ASP.NET MVC 1.0 應用程式升級至 ASP.NET MVC 2

> 本檔說明如何以手動方式升級，並透過 wizard 將 ASP.NET MVC 1.0 應用程式 ASP.NET MVC 2。 本檔也可供[下載](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf)

## <a name="introduction"></a>簡介

ASP.NET MVC 2 可以與 ASP.NET MVC 1.0 並存安裝在同一部伺服器上。 這讓應用程式開發人員可以彈性選擇何時將 ASP.NET MVC 1.0 應用程式升級為 ASP.NET MVC 2。

Visual Studio 2010 包含一個會將以 Visual Studio 2008 建立的現有 ASP.NET MVC 1.0 專案升級至 ASP.NET MVC 2 的 wizard。 [升級嚮導] 是藉由在 Visual Studio 2010 中開啟 ASP.NET MVC 1.0 專案來起始。

## <a name="upgrade-wizard-for-aspnet-mvc-10-on-visual-studio-2008-sp1"></a>Visual Studio 2008 SP1 上的 ASP.NET MVC 1.0 升級嚮導

若要將 ASP.NET MVC 1.0 應用程式升級至 Visual Studio 2008 SP1 中的 ASP.NET MVC 2，請使用（不支援的） MvcAppConverter 應用程式。 您可以從下列 URL 下載此應用程式：

[https://go.microsoft.com/fwlink/?LinkID=185351](https://go.microsoft.com/fwlink/?LinkID=185351)

## <a name="manually-upgrading-an-aspnet-mvc-10-project"></a>手動升級 ASP.NET MVC 1.0 專案

若要將現有的 ASP.NET MVC 1.0 應用程式手動升級到第2版，請遵循下列步驟：

1. 建立現有專案的備份。
2. 在文字編輯器中，開啟專案檔（副檔名為 .csproj 或. vbproj 的檔案），並尋找 ProjectTypeGuid 元素。 做為該元素的值，請將 GUID {603c0e0b-db56-11dc-be95-000d561079b0} 取代為 {F85E285D-A4E0-4152-9332-AB1D724D3325}。 當您完成時，該元素的值應該如下所示： 

    `{F85E285D-A4E0-4152-9332-AB1D724D3325};{349c5851-65df-11da-9384-00065b846f21};{fae04ec0-301f-11d3-bf4b-00c04f79efbc}`
3. 在 Web 應用程式的根資料夾中，編輯 Web.config 檔案。 搜尋 System.web，Version = 1.0.0.0 並將所有實例取代為 System.web，Version = 2.0.0.0。
4. 針對位於 Views 資料夾中的 Web.config 檔案重複上一個步驟。
5. 使用 Visual Studio 開啟專案，然後在**方案總管**中展開 [**參考**] 節點。 刪除 System.web 的參考（指向版本1.0 元件）。 加入 System.web 的參考（v 2.0.0.0）。
6. 在 configuraton 區段底下的應用程式根目錄中，將下列 bindingRedirect 元素新增至 web.config 檔案：   

    [!code-xml[Main](aspnet-mvc2-upgrade-notes/samples/sample1.xml)]
7. 建立新的空白 ASP.NET MVC 2 應用程式。 將新應用程式的 [腳本] 資料夾中的檔案複製到現有應用程式的 [腳本] 資料夾中。
8. 使用網站 .css 檔案中的 CSS 樣式定義來更新現有的 applicationâ€™ s CSS 檔案。
9. 編譯應用程式並加以執行。 如果發生任何錯誤，請參閱[ASP.NET MVC 2 的新功能頁面中](https://go.microsoft.com/fwlink/?LinkID=185038)的重大變更一節。
