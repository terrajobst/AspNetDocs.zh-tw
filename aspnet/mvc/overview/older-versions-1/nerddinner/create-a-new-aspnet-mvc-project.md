---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: 建立新的 ASP.NET MVC 專案 |Microsoft Docs
author: microsoft
description: 步驟1顯示如何將基本 NerdDinner 應用程式結構放在原處。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 189ddc187fc83db14106b2da199ba12a70a32b45
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580931"
---
# <a name="create-a-new-aspnet-mvc-project"></a>建立新的 ASP.NET MVC 專案

由[Microsoft](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟1，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。
> 
> 步驟1顯示如何將基本 NerdDinner 應用程式結構放在原處。
> 
> 如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。

## <a name="nerddinner-step-1-file-gtnew-project"></a>NerdDinner 步驟1：檔案&gt;新專案

我們會在 Visual Studio 2008 或免費的 Visual Web Developer 2008 Express 中選取檔案 **&gt;[新增專案**] 功能表項目，以開始我們的 NerdDinner 應用程式。

這會顯示 [新增專案] 對話方塊。 若要建立新的 ASP.NET MVC 應用程式，我們會選取對話方塊左側的 [Web] 節點，然後選擇右側的 [ASP.NET MVC Web 應用程式] 專案範本：

![](create-a-new-aspnet-mvc-project/_static/image1.png)

*重要事項：請確定您已下載並安裝 ASP.NET MVC，否則它不會顯示在 [新增專案] 對話方塊中。如果您尚未安裝[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) ，您可以使用 V2 （ASP.NET MVC 可在「Web 平臺-&gt;架構和執行時間」一節中取得）。*

我們會將新專案命名為 "NerdDinner"，然後按一下 [確定] 按鈕加以建立。

當我們按下 [Visual Studio 確定] 時，會出現一個額外的對話方塊，提示我們選擇性地為新的應用程式建立單元測試專案。 這個單元測試專案可讓我們建立自動化的測試，以驗證應用程式的功能和行為（我們將在本教學課程稍後討論的內容）。

![](create-a-new-aspnet-mvc-project/_static/image2.png)

上述對話方塊中的 [測試架構] 下拉式清單會填入電腦上安裝的所有可用 ASP.NET MVC 單元測試專案範本。 您可以下載 NUnit、MBUnit 和 XUnit 的版本。 此外，也支援內建的 Visual Studio 單元測試架構。

*注意： Visual Studio 單元測試架構僅適用于 Visual Studio 2008 Professional 和更新版本。如果您使用 VS 2008 Standard Edition 或 Visual Web Developer 2008 Express，您將需要下載並安裝 ASP.NET MVC 的 NUnit、MBUnit 或 XUnit 擴充功能，才能顯示此對話方塊。如果未安裝任何測試架構，則不會顯示對話方塊。*

我們會針對我們所建立的測試專案使用預設的「NerdDinner」名稱，並使用「Visual Studio 單元測試」架構選項。 當我們按一下 [確定] 按鈕時 Visual Studio 會為我們建立一個解決方案，其中包含兩個專案，一個用於我們的 web 應用程式，一個用於我們的單元測試：

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a>檢查 NerdDinner 目錄結構

當您使用 Visual Studio 建立新的 ASP.NET MVC 應用程式時，它會自動將一些檔案和目錄新增至專案：

![](create-a-new-aspnet-mvc-project/_static/image4.png)

ASP.NET MVC 專案預設會有六個最上層目錄：

| **目錄** | **目的** |
| --- | --- |
| **/Controllers** | 放置處理 URL 要求的控制器類別的位置 |
| **/Models** | 在其中放置代表和運算元據的類別 |
| **/Views** | 放置負責轉譯輸出的 UI 範本檔案的位置 |
| **/Scripts** | 放置 JavaScript 程式庫檔案和腳本的位置（.js） |
| **/Content** | 放置 CSS 和影像檔案的位置，以及其他非動態/非 JavaScript 內容 |
| **/App\_資料** | 儲存您想要讀取/寫入的資料檔案的位置。 |

ASP.NET MVC 不需要此結構。 事實上，處理大型應用程式的開發人員通常會在多個專案之間分割應用程式，使其更容易管理（例如：資料模型類別通常會從 web 應用程式移至不同的類別庫專案）。 不過，預設的專案結構的確提供了一個不錯的預設目錄慣例，可讓我們用來將應用程式的顧慮保持乾淨。

當我們展開/Controllers 目錄時，我們會發現 Visual Studio 新增了兩個控制器類別– HomeController 和 AccountController –預設為專案：

![](create-a-new-aspnet-mvc-project/_static/image5.png)

當我們展開/Views 目錄時，我們會發現三個子目錄（/Home、/Account 和/Shared），而且它們內的數個範本檔案也會依預設新增至專案：

![](create-a-new-aspnet-mvc-project/_static/image6.png)

當我們展開/Content 和/Scripts 目錄時，我們會發現一個網站 .css 檔案，該檔案用來為網站上的所有 HTML 樣式，以及可在應用程式內啟用 ASP.NET AJAX 和 jQuery 支援的 JavaScript 程式庫：

![](create-a-new-aspnet-mvc-project/_static/image7.png)

當我們展開 [NerdDinner] 專案時，我們會發現兩個類別，其中包含控制器類別的單元測試：

![](create-a-new-aspnet-mvc-project/_static/image8.png)

Visual Studio 新增的這些預設檔案，會為我們提供一個基本結構，讓應用程式得以完成，其中包含首頁、[關於] 頁面、帳戶登入/登出/註冊頁面，以及未處理的錯誤頁面（所有的有線和作用中）。

### <a name="running-the-nerddinner-application"></a>執行 NerdDinner 應用程式

我們可以藉由選擇 [ **debug-&gt;] [開始調試**程式] 或 [ **Debug-&gt;啟動但不調試**] 功能表項目來執行專案：

![](create-a-new-aspnet-mvc-project/_static/image9.png)

這會啟動 Visual Studio 隨附的內建 ASP.NET Web 服務器，並執行我們的應用程式：

![](create-a-new-aspnet-mvc-project/_static/image10.png)

以下是新專案（URL： "/"）執行時的首頁：

![](create-a-new-aspnet-mvc-project/_static/image11.png)

按一下 [關於] 索引標籤會顯示 [關於] 頁面（URL： "/Home/About"）：

![](create-a-new-aspnet-mvc-project/_static/image12.png)

按一下右上角的 [登入] 連結，會將我們帶到登入頁面（URL： "/Account/LogOn"）

![](create-a-new-aspnet-mvc-project/_static/image13.png)

如果沒有登入帳戶，我們可以按一下 [註冊] 連結（URL： "/Account/Register"）來建立一個：

![](create-a-new-aspnet-mvc-project/_static/image14.png)

當我們建立新專案時，預設會新增執行上述 [首頁]、[關於] 和 [登出/註冊] 功能的程式碼。 我們將使用它做為應用程式的起點。

### <a name="testing-the-nerddinner-application"></a>測試 NerdDinner 應用程式

如果我們使用 Professional Edition 或更高版本的 Visual Studio 2008，我們可以在 Visual Studio 中使用內建的單元測試 IDE 支援來測試專案：

![](create-a-new-aspnet-mvc-project/_static/image15.png)

選擇上述其中一個選項，將會在 IDE 中開啟 [測試結果] 窗格，並在涵蓋內建功能的新專案中所包含的27個單元測試上提供「通過/失敗」狀態：

![](create-a-new-aspnet-mvc-project/_static/image16.png)

稍後在本教學課程中，我們將詳細討論自動化測試，並加入涵蓋我們所實行之應用程式功能的其他單元測試。

### <a name="next-step"></a>後續步驟

我們現在已具備基本的應用程式結構。 現在讓我們[建立資料庫來儲存我們的應用程式資料](create-a-database.md)。

> [!div class="step-by-step"]
> [上一頁](introducing-the-nerddinner-tutorial.md)
> [下一頁](create-a-database.md)
