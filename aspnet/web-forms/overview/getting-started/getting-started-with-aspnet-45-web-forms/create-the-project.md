---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create-the-project
title: 建立專案 |Microsoft Docs
author: Erikre
description: 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 為我們建立 ASP.NET Web Forms 應用程式的基本概念 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 2ce36f78-8ecb-4ab1-b748-6d0ab633ea3f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create-the-project
msc.type: authoredcontent
ms.openlocfilehash: 62918b17f42e54dfe4e45a08927b1039dcbb7012
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74576059"
---
# <a name="create-the-project"></a>建立專案

依[Erik Reitan](https://github.com/Erikre)

[下載 Wingtip 玩具範例專案（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下載電子書（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 建立 ASP.NET Web Forms 應用程式的基本概念。 本教學課程系列隨附有[ C#原始程式碼](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 專案。

在本教學課程中，您將建立、審查和執行 Visual Studio 中的預設專案，這可讓您熟悉 ASP.NET 的功能。 此外，您也會查看 Visual Studio 環境。

## <a name="what-youll-learn"></a>您將瞭解的內容：

- 如何建立新的 Web form 專案。
- Web Forms 專案的檔案結構。
- 如何在 Visual Studio 中執行專案。
- 預設 Web forms 應用程式的不同功能。
- 有關如何使用 Visual Studio 環境的一些基本概念。

## <a name="creating-the-project"></a>建立專案

1. 開啟 Visual Studio。
2. 從**Visual Studio 的 [** 檔案] 功能表中選取 [**新增專案**]。 

    ![建立專案-新增專案功能表項目](create-the-project/_static/image1.png)
3. 選取左側的 [&gt; **Visual C#**  -&gt; **Web** templates] 群組 -**範本**。
4. 在中間的資料行中選擇 [ **ASP.NET Web 應用程式**] 範本。  
 本教學課程系列使用 .NET Framework 4.5.2。
5. 將專案命名為*WingtipToys* ，然後選擇 [**確定]** 按鈕。 

    ![建立專案-新增專案對話方塊](create-the-project/_static/image2.png)

    > [!NOTE]
    > 本教學課程系列中的專案名稱是**WingtipToys**。 建議您使用此專案的*確切*名稱，讓整個教學課程系列中提供的程式碼如預期般運作。

6. 按一下 [**變更驗證**] 按鈕。 選取 [**個別使用者帳戶**]，然後按一下 [**確定]** 按鈕。

7. 選取 [ **Web** form] 範本，然後按一下 [**確定]** 按鈕。

    ![建立專案-新增專案範本](create-the-project/_static/image3.png)

專案需要一些時間才能建立。 準備就緒時，請開啟**default.aspx**頁面。

![建立專案-新增專案範本](create-the-project/_static/image4.png)

您可以選取中央視窗底部的選項，在**設計**視圖和**來源**視圖之間切換。 [**設計**視圖] 會使用接近 WYSIWYG 的視圖，顯示 ASP.NET 的網頁、主版頁面、內容頁面、HTML 網頁和使用者控制項。 [**來源**視圖] 會顯示您網頁的 HTML 標籤，您可以加以編輯。

> [!TIP] 
> 
> **瞭解 ASP.NET 架構**
> 
> ASP.NET Web Forms 可讓您使用類似的拖放、事件導向模型來建置動態網站。 單一設計介面和數百個控制項和元件可讓您快速建置功能強大、可存取資料的 UI 導向網站。 Wingtip 玩具存放區是以 ASP.NET 的 Web 表單為基礎，但您在本教學課程系列中學習到的許多概念都適用于所有 ASP.NET。
> 
> ASP.NET 提供四種主要的開發架構：
> 
> - [ASP.NET Web Forms](../../../index.md)  
>  Web form 架構是以偏好宣告式和以控制項為基礎之程式設計的開發人員為目標，例如 Microsoft Windows Forms （WinForms）和 WPF/XAML/Silverlight。 它提供 WYSIWYG 設計工具驅動的開發模型，讓開發人員在尋找 網頁程式開發的快速應用程式開發（RAD）環境時，也很容易受到歡迎。 如果您是 web 程式設計的新手，並且熟悉傳統的 Microsoft RAD 用戶端開發工具（例如，針對 Visual Basic 和視覺C#效果），您可以快速建立 web 應用程式，而不需要使用 HTML 和 JavaScript 的經驗。
> - [ASP.NET MVC](../../../../mvc/index.md)  
>  ASP.NET MVC 目標開發人員對各種模式和原則感興趣，例如測試導向開發、關注點分離、控制反轉（IoC）和相依性插入（DI）。 此架構鼓勵 web 應用程式的商務邏輯層與展示層分開。
> - [ASP.NET Web Pages](../../../../web-pages/index.md)  
>  ASP.NET Web Pages 以需要簡單 Web 開發案例的開發人員為目標，以及 PHP 的各行。 在網頁模型中，您可以建立 HTML 網頁，然後將以伺服器為基礎的程式碼加入至頁面，以動態方式控制該標記的呈現方式。 網頁是特別設計為輕量架構，對於知道 HTML 但可能不會有廣泛程式設計經驗（例如學生或業餘人士）的人而言，這是最容易 ASP.NET 的進入點。 這也是讓知道 PHP 或類似架構的 網頁程式開發人員開始使用 ASP.NET 的好方法。
> - [ASP.NET 單一頁面應用程式](../../../../single-page-application/index.md)  
>  ASP.NET 單頁應用程式（SPA）可協助您使用 HTML 5、CSS 3 和 JavaScript，建立包含重大用戶端互動的應用程式。 ASP.NET 和 Web 工具2012.2 更新推出了新的範本，可使用挖的 .js 和 ASP.NET Web API 建立單一頁面應用程式。 除了新的 SPA 範本，新的已建立社區的 SPA 範本也可供下載。
> 
> 除了四個主要的開發架構之外，ASP.NET 也提供其他重要的技術，讓您瞭解並熟悉，但不會涵蓋在本教學課程系列中：
> 
> - [ASP.NET Web API](../../../../web-api/index.md) -用來建立可觸及各種用戶端（包括瀏覽器和行動裝置）之 HTTP 服務的架構。
> - [ASP.NET SignalR](../../../../signalr/index.md) -可讓您輕鬆開發即時 web 功能的程式庫。

### <a name="reviewing-the-project"></a>檢查項目

在 Visual Studio 中，[**方案總管**] 視窗可讓您管理專案的檔案。 讓我們看一下**方案總管**中已新增至應用程式的資料夾。 Web 應用程式範本會新增基本資料夾結構：

![建立專案-方案總管](create-the-project/_static/image5.png)

Visual Studio 會為您的專案建立一些初始資料夾和檔案。 您稍後將在本教學課程中使用的第一個檔案如下所示：

| **檔案** | **目的** |
| --- | --- |
| *Default.aspx* | 當應用程式在瀏覽器中執行時，通常會顯示第一頁。 |
| *網站. Master* | 此頁面可讓您建立一致的版面配置，並在應用程式中使用頁面的標準行為。 |
| *Global.asax* | 選擇性的檔案，其中包含回應 ASP.NET 或 HTTP 模組所引發之應用層級和工作階段層級事件的程式碼。 |
| *Web.config* | 應用程式的設定資料。 |

### <a name="running-the-default-web-application"></a>執行預設 Web 應用程式

預設的 Web 應用程式會根據內建功能和支援，提供豐富的體驗。 若沒有預設 Web form 專案的任何變更，應用程式就可以在本機網頁瀏覽器上執行。

1. 在 Visual Studio 中，按***F5***鍵。   
 應用程式將會在您的網頁瀏覽器中建立並顯示。  

    ![建立專案-預設頁面](create-the-project/_static/image6.png)
2. 完成執行的應用程式檢查之後，請關閉瀏覽器視窗。

這個預設 Web 應用程式中有三個主要頁面： *default.aspx* （Home）、 *About .aspx*和*Contact .aspx*。 您可以從上方導覽列中，連線到每個頁面。 帳戶資料夾中也包含兩個額外的頁面： [Register .aspx] 頁面和 [Login .aspx] 頁面。 這兩個頁面可讓您使用 ASP.NET 的成員資格功能來建立、儲存和驗證使用者認證。

## <a name="aspnet-web-forms-background"></a>ASP.NET Web Forms 背景

ASP.NET Web form 是以 Microsoft ASP.NET 技術為基礎的頁面，在伺服器上執行的程式碼會以動態方式將網頁輸出產生至瀏覽器或用戶端裝置。 ASP.NET Web form 頁面會針對樣式、版面配置等功能，自動呈現正確的瀏覽器相容 HTML。 Web form 與 .NET common language runtime 所支援的任何語言（例如 Microsoft Visual Basic 和 Microsoft Visual C#）相容。 此外，Web form 是以[Microsoft .NET Framework](https://msdn.microsoft.com/vstudio/aa496123)為基礎，提供受控環境、型別安全和繼承等優點。

當 ASP.NET Web form 頁面執行時，此頁面會經歷一個生命週期，其會執行一系列的處理步驟。 這些步驟包括初始化、具現化控制項、還原和維護狀態、執行事件處理常式程式碼，以及呈現。 當您更熟悉 ASP.NET Web form 的能力時，請務必瞭解[ASP.NET 網頁生命週期](https://msdn.microsoft.com/library/ms178472(v=vs.100).aspx)，讓您可以在適當的生命週期階段為您想要的效果撰寫程式碼。

當網頁伺服器收到頁面的要求時，它會尋找該頁面，處理它，然後將它傳送至瀏覽器，然後捨棄所有頁面資訊。 如果使用者再次要求相同的頁面，伺服器就會重複整個順序，從頭重新處理頁面。 另一種方式是，伺服器沒有任何已處理頁面的記憶體-頁面是無狀態的。 ASP.NET 網頁架構會自動處理維護頁面和其控制項狀態的工作，並提供明確的方式來維護應用程式特定資訊的狀態。

> [!TIP] 
> 
> **Web Forms 應用程式範本中的 web 應用程式功能**
> 
> ASP.NET Web Forms 應用程式範本提供了一組豐富的內建功能。 它不只會提供您一個*首頁 .aspx* *頁面，* 也就是一個*Contact .aspx*頁面，但也包含成員資格功能，可註冊使用者並儲存其認證，讓他們可以登入您的網站。 本總覽提供 ASP.NET Web Forms 應用程式範本中所含功能的詳細資訊，以及它們在 Wingtip 玩具應用程式中的使用方式。
> 
> **成員資格**
> 
> [ASP.NET](https://msdn.microsoft.com/library/yh26yfzy.aspx)身分識別會將使用者的認證儲存在應用程式所建立的資料庫中。 當您的使用者登入時，應用程式會藉由讀取資料庫來驗證其認證。 您專案的 [*帳戶*] 資料夾包含可執行成員資格各部分的檔案：註冊、登入、變更密碼，以及授權存取。 此外，ASP.NET Web Forms 支援 OAuth 和 OpenID。 這些驗證增強功能可讓使用者使用現有的認證登入您的網站，例如 Facebook、Twitter、Windows Live 和 Google 等帳戶。
> 
> ![建立專案-方案總管（ASP.NET Identity）](create-the-project/_static/image7.png)
> 
> 根據預設，此範本會在 SQL Server Express LocalDB 的實例上使用預設資料庫名稱建立成員資格資料庫，而在 Visual Studio Express 2013 for Web 隨附的開發資料庫伺服器。
> 
> **SQL Server Express LocalDB**
> 
> [SQL Server Express LocalDB](https://technet.microsoft.com/library/hh510202.aspx)是輕量版的 SQL Server，其中有許多 SQL Server 資料庫的可程式性功能。 SQL Server Express LocalDB 會在使用者模式中執行，而且具有快速的零設定安裝，其中包含安裝必要條件的簡短清單。 在 Microsoft SQL Server 中，任何資料庫或 Transact-sql 程式碼都可以從 SQL Server Express LocalDB 移至 SQL Server 和 SQL Azure，而不需要任何升級步驟。 因此，SQL Server Express LocalDB 可以做為以所有 SQL Server 版本為目標之應用程式的開發人員環境。 SQL Server Express LocalDB 可啟用一些功能，例如預存程式、使用者定義函數和匯總、.NET Framework 整合、空間類型，以及 SQL Server Compact 中無法使用的其他專案。
> 
> **主版頁面**
> 
> [ASP.NET 主版頁面](https://msdn.microsoft.com/library/wtxbf3hh.aspx)會針對您應用程式中的所有頁面定義一致的外觀和行為。 主版頁面的配置會與個別內容頁面中的內容合併，以產生使用者看到的最後一頁。 在 Wingtip 玩具應用程式中，您可以修改 [*網站*] 主版頁面，讓 Wingtip 玩具網站中的所有頁面共用相同的獨特標誌和導覽列。
> 
> **HTML5**
> 
> ASP.NET Web Forms 應用程式範本支援[HTML5](http://www.w3schools.com/html/html5_intro.asp)，這是最新版的 HTML 標籤語言。 HTML5 支援新的專案和功能，讓您更輕鬆地建立網站。
> 
> **Modernizr**
> 
> 對於不支援 HTML5 的瀏覽器，您可以使用[Modernizr](http://www.modernizr.com/)。 Modernizr 是開放原始碼 JavaScript 程式庫，可以偵測瀏覽器是否支援 HTML5 功能，如果沒有的話，則啟用。 在 ASP.NET Web Forms 應用程式範本中，Modernizr 會安裝為 NuGet 套件。
> 
> **啟動程序**
> 
> Visual Studio 2013 專案範本會使用[啟動](http://getbootstrap.com/)程式，這是 Twitter 所建立的版面配置和主題架構。 啟動程式會使用 CSS3 來提供回應式設計，這表示版面配置可以動態調整成不同的瀏覽器視窗大小。 您也可以使用啟動程式的主題功能，輕鬆地影響應用程式外觀和風格的變更。 根據預設，Visual Studio 2013 中的 ASP.NET Web 應用程式範本包含以 NuGet 封裝的啟動載入器。
> 
> **NuGet 套件**
> 
> ASP.NET Web Forms 應用程式範本包含一組[NuGet](http://www.nuget.org/)套件。 這些套件以開放原始碼程式庫和工具的形式提供元件化功能。 有各式各樣的套件可協助您建立及測試應用程式。 Visual Studio 可讓您輕鬆地新增、移除和更新 NuGet 套件。 開發人員也可以建立套件並將其新增至 NuGet。
> 
> ![建立專案-NuGet 對話方塊](create-the-project/_static/image8.png)
> 
> 當您安裝套件時，NuGet 會將檔案複製到您的解決方案，並自動進行所需的任何變更，例如新增參考和變更與 Web 應用程式相關聯的設定。 如果您決定移除程式庫，NuGet 會移除檔案，並反轉它在專案中所做的任何變更，因此不會留下雜亂的內容。 您可以從 Visual Studio 中的 [**工具**] 功能表取得 NuGet。
> 
> **jQuery**
> 
> [jQuery](http://jquery.com/)是一種快速且簡潔的 JavaScript 程式庫，可簡化 HTML 檔案的往返、事件處理、動畫和 Ajax 互動，以快速進行 web 程式開發。 JQuery JavaScript 程式庫會以 NuGet 套件的形式包含在 ASP.NET Web Forms 應用程式範本中。
> 
> **不顯眼的驗證**
> 
> 內建的驗證程式控制項已設定為針對用戶端驗證邏輯使用不顯眼的 JavaScript。 這會大幅減少在頁面標記中內嵌呈現的 JavaScript 數量，並減少整體頁面大小。 不顯眼的驗證會根據應用程式根目錄*之 web.config 檔案*的 &lt;appSettings&gt; 元素中的設定，以全域方式加入至 ASP.NET Web Forms 應用程式範本。
> 
> **Entity Framework Code First**
> 
> 除了 ASP.NET Web Forms 應用程式範本中的功能之外，Wingtip 玩具應用程式還會使用[Entity Framework Code First](https://weblogs.asp.net/scottgu/archive/2010/12/08/announcing-entity-framework-code-first-ctp5-release.aspx)，這是 NuGet 程式庫，可在您使用資料時，啟用以程式碼為中心的開發。 簡單地說，它會根據您撰寫的程式碼，為您建立應用程式的資料庫部分。 使用 Entity Framework，您可以將資料當作強型別物件來取得和操作。 這可讓您專注于應用程式中的商務邏輯，而不是資料存取方式的詳細資訊。
> 
> 如需 ASP.NET Web form 範本隨附之已安裝程式庫和套件的詳細資訊，請參閱已安裝的 NuGet 套件清單。 若要這麼做，請在 Visual Studio 建立新的 Web form 專案 中，選取 **工具** >  **NuGet 套件管理員** > **管理方案的 nuget 套件**，然後選取 **管理 Nuget 套件** 對話方塊中的 **已安裝的套件**。

### <a name="touring-visual-studio"></a>旅行 Visual Studio

Visual Studio 中的主視窗包括**方案總管**、**伺服器總管**（**資料庫總管**在 Express 中）、[**屬性] 視窗**、[**工具箱**]、**工具列**和**文件視窗**。

![建立專案-NuGet 對話方塊](create-the-project/_static/image9.png)

如需 Visual Studio 的詳細資訊，請參閱 visual [Web Developer 的視覺效果指南](https://msdn.microsoft.com/library/ee410104.aspx)。

## <a name="summary"></a>總結

在本教學課程中，您已建立、審查及執行預設的 Web form 應用程式。 您已複習過預設 Web forms 應用程式的不同功能，並瞭解如何使用 Visual Studio 環境的一些基本概念。 在下列教學課程中，您將建立資料存取層。

## <a name="additional-resources"></a>其他資源

[選擇正確的程式設計模型](../../../videos/how-do-i/choosing-the-right-programming-model.md)   
[Web 應用程式專案與網站專案](https://msdn.microsoft.com/library/dd547590.aspx)的比較   
[ASP.NET Web Forms 頁面總覽](https://msdn.microsoft.com/library/428509ah.aspx)

> [!div class="step-by-step"]
> [上一頁](introduction-and-overview.md)
> [下一頁](create_the_data_access_layer.md)
