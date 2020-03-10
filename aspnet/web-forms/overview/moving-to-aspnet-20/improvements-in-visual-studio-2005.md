---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: Visual Studio 2005 中的改進 |Microsoft Docs
author: microsoft
description: Visual Studio 2005 為 Web 應用程式開發人員提供一份很長的 Web 專案改良功能和增強功能。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: 64215d556ded0850537a13856fe69b094116ebca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78575576"
---
# <a name="improvements-in-visual-studio-2005"></a>Visual Studio 2005 中的改善

由[Microsoft](https://github.com/microsoft)

> Visual Studio 2005 為 Web 應用程式開發人員提供一份很長的 Web 專案改良功能和增強功能。

Visual Studio 2005 為 Web 應用程式開發人員提供一份很長的 Web 專案改良功能和增強功能。 就像 Visual Studio .NET 2002 和2003的功能強大，Web 專案的處理方式有很多抱怨。 Visual Studio 2005 加入大量的新功能，以解決這些抱怨。 針對偏好 Visual Studio .NET 2003 處理 Web 應用程式之編譯方式的人員，請參閱[Web 應用程式專案](https://go.microsoft.com/fwlink/?LinkId=57870)。

在此課程模組中，我們將探討 Web 專案建立、管理和開發方面的改進。 在稍後的課程模組中，我們將進一步探討建立 Web 專案和部署它們的功能。

## <a name="frontpage-server-extensions"></a>FrontPage Server Extensions

Visual Studio FrontPage Server Extensions 需要 .NET 2002 和2003，才能建立或建立 Web 專案。 開發人員可以選擇兩種不同的存取模式（FrontPage Server Extensions 或檔案存取模式），這兩者都用 FrontPage Server Extensions 來執行工作，例如在 IIS 中設定應用程式根目錄等等。

Visual Studio 2005 會移除對本機專案的 FrontPage Server Extensions 的依賴。 Visual Studio 2005 現在會直接存取 IIS 元資料庫，而不是使用 FrontPage Server Extensions。 Visual Studio 2005 也新增了 FTP 的支援，允許遠端專案存取，而不需要 FrontPage Server Extensions。

對於想要在專案中使用 FrontPage Server Extensions 的開發人員而言，仍然可以使用此選項。 不過，根據 ASP.NET 開發人員社區的強大意見反應，這不是必要條件。

> [!NOTE]
> 遠端專案建立、開啟等等，仍然需要 FrontPage Server Extensions。

## <a name="aspnet-development-server"></a>ASP.NET 程式開發伺服器

Visual Studio 2005 隨附新的網頁伺服器，稱為 ASP.NET 程式開發伺服器。 （此網頁伺服器先前稱為 Cassini）。

ASP.NET 程式開發伺服器有數個優點。

- 非系統管理員現在可以針對 Web 服務器進行開發和偵錯工具。
- ASP.NET 程式開發伺服器會動態地將虛擬目錄對應至檔案系統中的任何位置，以允許彈性的專案位置。
- Windows XP Professional 上已使用 IIS 的使用者現在可以建立新的 Web 應用程式，而不會影響 IIS 中預設網站的檔案或資料夾結構。

不需要特殊設定即可利用 ASP.NET 程式開發伺服器。 當調試或流覽檔案系統上主控的 Web 專案時，Visual Studio 2005 將會在隨機埠上自動啟動 ASP.NET 程式開發伺服器的實例，以服務要求。

本課程模組稍後的 ASP.NET 程式開發伺服器將涵蓋詳細資訊。

## <a name="improved-file-management"></a>改良的檔案管理

在 Visual Studio 2002 和2003中，專案檔（適用于 VB.NET 的 vbproj 和 .csproj C#）會儲存在 Web 應用程式中所有檔案的資訊。 方案總管顯示是根據專案檔中的檔案資訊。 因此，在使用外部編輯器的情況下，方案總管通常會顯示不正確的資訊。 Visual Studio 2002 和2003通常會覆寫檔案變更，或不會顯示最新版本的檔案。

Visual Studio 2005 與專案檔相同。 相反地，它會直接從磁片讀取檔案和資料夾資訊，以精確顯示專案中的檔案。 因為 Visual Studio 2002 和2003中的 [參考] 資料夾不代表 Web 應用程式中的實際資料夾，Visual Studio 2005 也會從方案總管移除 [參考] 資料夾。 若要存取 Visual Studio 2005 中專案的參考，您應該使用專案的屬性頁。

## <a name="creating-web-projects"></a>建立 Web 專案

Web 開發人員有許多新選項可用於 Visual Studio 2005 中的專案建立。 現在可以在檔案系統中的任何位置建立網站，然後使用新的 ASP.NET 程式開發伺服器來進行調試或流覽。 開發人員也可以使用 FTP 建立新的網站。

按一下這裡以觀看在 Visual Studio 2005 中建立 Web 專案的影片逐步解說。

![](improvements-in-visual-studio-2005/_static/image1.png)

[開啟全螢幕影片](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)

### <a name="file-system-projects"></a>檔案系統專案

如您在影片逐步解說中所見，您可以選擇在檔案系統上，透過檔案共用在本機電腦或遠端位置上建立網站。 在檔案系統上建立的網站會使用 ASP.NET 程式開發伺服器進行流覽和調試。

> [!NOTE]
> ASP.NET 程式開發伺服器可能會對客戶造成一些混淆。 如果在檔案系統上的 IISs 目錄結構中建立 Web 專案（也就是 c：/inetpub/wwwroot），則在從 Visual Studio 2005 內啟動網站時，仍然會透過 ASP.NET 程式開發伺服器來流覽該網站。 因此，任何 IIS 設定（亦即驗證方法）都不適用。

預設的 Web 專案也會藉由只包含 default.aspx 頁面、default.cs 檔和應用程式/_Data 資料夾來移除許多額外負荷。 Web.config 和特殊資料夾（例如應用程式/_code）會視需要新增。 您的 Web 專案只包含您需要的檔案和資料夾。

### <a name="http-projects"></a>HTTP 專案

HTTP 專案可以是在本機 IIS 網站或遠端網站上建立的專案。 預設專案位置為 `http://localhost`。 如果您按一下 [流覽] 按鈕，則會有兩個 HTTP 選項： [本機 IIS] 和 [遠端網站]。 這兩個選項的主要差異在於網站資訊顯示在 [選擇位置] 對話方塊中的方法，以及檔案複製到 Web 服務器的方式。

本機 IIS 選項會從本機電腦上的設定檔讀取網站資訊，並使用檔案系統來複製檔案。 [遠端網站] 選項會使用 FrontPage Server Extensions 並使用 HTTP 和 FrontPage Server Extensions RPC 呼叫來複製網站資訊和檔案。

> [!NOTE]
> 不再使用 vs # # #/_tmp .htm 檔案和 get/_aspx/_ver 來判斷版本資訊。

預設的 HTTP 選項是 [本機 IIS]。 此選項會讀取 IIS 的元資料庫，以判斷可用的網站和要在其中建立內容的位置。 您可以選取不同的資料夾或虛擬目錄，方法是在樹狀檢視中選取它。 您也可以建立新的虛擬目錄、將資料夾標示為應用程式，以及從此對話方塊中刪除現有的虛擬目錄。

![[選擇位置] 對話方塊](improvements-in-visual-studio-2005/_static/image1.gif)

**圖 1**： [選擇位置] 對話方塊

不同于舊版 Visual Studio，如果您核取 [**使用安全通訊端層**] 核取方塊，且 SSL 憑證不符合您要流覽的 URL，您會看到 [安全性警示] 對話方塊，詢問您是否要繼續。 使用 Visual Studio .NET 2003，如果憑證不相符，則建立專案會失敗。

![關於 SSL 憑證的安全性警示](improvements-in-visual-studio-2005/_static/image2.gif)

**圖 2**：關於 SSL 憑證的安全性警示

### <a name="note-on-host-headers"></a>主機標頭上的注意事項

如果您要在系結至特定 IP 的網站上建立 Web 應用程式，您將需要確定已設定主機標頭。 否則，Visual Studio 會在 `http://localhost`建立網站，但在從 IDE 內流覽或調試網站時，IP 位址將無法正確解析。

如果您選取 [遠端網站] 選項，對話方塊會變更為，讓您輸入新網站的目的地 URL。 此 URL 必須位於已啟用 FrontPage Server Extensions 的伺服器上。 如果您想要使用 FrontPage Server Extensions 來處理本機 Web 服務器，可以使用 [遠端網站] 選項，並指定本機 URL。

![在遠端伺服器上建立網站](improvements-in-visual-studio-2005/_static/image1.jpg)

**圖 3**：在遠端伺服器上建立網站

透過 SSL 在遠端網站上建立應用程式時，如果 SSL 憑證不相符，則 [確認] 對話方塊會與使用 [本機 IIS] 選項時所顯示的對話方塊略有不同。

![遠端網站安全性警示](improvements-in-visual-studio-2005/_static/image3.gif)

**圖 4**：遠端網站安全性警示

<a id="_Toc116100243"></a>

#### <a name="ftp"></a>FTP

Visual Studio 2005 引進了透過 FTP 建立網站的選項。 當您使用此選項時，IDE 會在使用者的 temp 資料夾中建立檔案，然後使用 FTP 將檔案移到 FTP 位置。

> [!NOTE]
> 暫存資料夾位置為 c：/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;應用程式名稱&gt;

使用 FTP 選項時，您會看到 [選擇位置] 對話方塊。 您在此對話方塊中輸入必要的 FTP 連接資訊，如下所示。

![FTP 的 [選擇位置] 對話方塊](improvements-in-visual-studio-2005/_static/image2.jpg)

**圖 5**： FTP 的 [選擇位置] 對話方塊

## <a name="lab-setup-ftp-site-and-create-a-project"></a>實驗室：設定 FTP 網站和建立專案

下列步驟會設定 FTP 網站，讓使用者具有只能透過 FTP 上傳至的位置。

### <a name="install-the-ftp-service"></a>安裝 FTP 服務

1. 開啟 [新增] [移除程式]，選取 [新增/移除 Windows 元件]
2. 選取 [Internet Information Services （Windows 2003 上的應用程式伺服器）]，然後按一下 [**詳細資料**]。
3. 檢查**檔案傳輸通訊協定（FTP）服務**，然後按一下 **[確定]** 。
4. 按 **[下一步]** 安裝 FTP 服務。

### <a name="create-a-new-folder-for-content"></a>為內容建立新的資料夾

1. 在 Windows Explorer 中，于 c：/inetpub/wwwroot 內建立名為**User1**的新資料夾。

#### <a name="configure-folders-and-permissions-on-folders"></a>設定資料夾的資料夾和許可權。

1. 從 [系統管理工具] 開啟 [Internet Information Services] 嵌入式管理單元。 您現在會在 [電腦名稱稱] 節點底下有一個 [FTP 網站] 資料夾。
2. 展開 [ **FTP 網站**]。
3. 以滑鼠右鍵按一下**預設的 FTP 網站**，依序選取 [**新增**]、[**虛擬目錄** **] 和 [下一步]** 。
4. 輸入**User1**作為虛擬目錄名稱，然後按 **[下一步]** 。
5. 針對路徑輸入**c：/inetpub/wwwroot/User1** ，然後按 **[下一步]** 。
6. 按 **[下一步**]，然後按一下 **[完成**] 以完成嚮導。
7. 以滑鼠右鍵按一下 [預設 FTP 網站] 底下的**User1**虛擬目錄，然後選取 [**屬性**]。
8. 勾選 [**寫入**] 核取方塊，然後按一下 **[確定**] 以關閉對話方塊。
9. 以滑鼠右鍵按一下 [**預設的 FTP 網站**]，然後選取 [**屬性**]。
10. 在 [**安全性帳戶**] 索引標籤上，取消核取 [**允許匿名連接**]。
11. 在詢問您是否要繼續的對話方塊中按一下 **[是**]。
12. 按一下 **[確定]** 關閉對話方塊。
13. 在 [**網站**] 節點底下，展開 [**預設的網站**]。
14. 以滑鼠右鍵按一下**User1**目錄，然後選取 [**屬性**]
15. 在 [**應用程式設定**] 區段中，按一下 [**建立**]，將資料夾標示為應用程式。
16. 按一下 **[確定]** 關閉對話方塊。
17. 關閉 [Internet Information Services] 嵌入式管理單元。

### <a name="create-web-project"></a>建立 Web 專案

1. 開啟 Visual Studio 2005。
2. 從 [**檔案**] 功能表中，選取 [**新網站**]。
3. 在 [**位置**] 下拉式清單中，選取 [ **FTP**]。
4. 按一下 [瀏覽]。
5. 在 [**伺服器**] 文字方塊中輸入**localhost** 。
6. 在 [目錄] 文字方塊中，輸入**User1** 。
7. 按一下 [開啟]。 FTP 位置會在 [新網站] 對話方塊中輸入。
8. 按一下 [確定]。
9. 取消核取 [FTP 登入] 對話方塊中的 [**匿名登入**]，輸入您的認證，然後按一下 **[確定]** 。
10. 專案的 URL 為何？ （專案的 URL 會顯示在方案總管中）。
11. 從 [**建立**] 功能表中，選取 [**建立網站**] 或 [**組建方案**]。
12. 在方案總管中，以滑鼠右鍵按一下 default.aspx，然後**在瀏覽器中**選取 [View]。
13. 在 [需要網站 URL] 對話方塊中，輸入 URL 的 `http://localhost/user1`，然後按一下 **[確定]** 。

> [!NOTE]
> 如果您收到錯誤，指出無法載入類型/_Default，請確定您在網站上執行的是 ASP.NET 2.0，而不是在較舊的版本上執行。 您可以從 Internet Information Services 的 [ASP.NET] 索引標籤中執行此動作。

## <a name="opening-web-projects"></a>開啟 Web 專案

開啟 Web 專案類似于建立專案。 下列各節會在 IDE 中工作時，呼叫要留意的區域。 它也涵蓋如何使用 HTTP 和 FTP 來處理 Web 專案。

若要開啟 Web 專案，請從 [檔案] 功能表中選取 [開啟網站]。 系統會提示您提供先前所述的相同 [選擇位置] 對話方塊，而且您有相同的四個選項： [檔案系統]、[本機 IIS]、[FTP] 和 [遠端網站]。

<a id="_Toc116100245"></a>

## <a name="file-system"></a>檔案系統

如先前在此課程模組中所述，Visual Studio 不再使用專案檔。 因此，如果您選擇從檔案系統開啟網站，則您實際上可以選擇想要的任何資料夾，即使您選擇的資料夾不是以 Visual Studio 一開始就建立為 Web 專案。 例如，您可以選擇開啟 [我的文件] 資料夾做為網站，Visual Studio 會很高興地開啟它並顯示您的檔案，如下所示。

![我的檔開啟為網站](improvements-in-visual-studio-2005/_static/image3.jpg)

**圖 6**：*我的檔*開啟為網站

因為 Visual Studio 只會在必要時建立額外的檔案和資料夾，所以不會在您開啟的位置新增任何其他檔案或資料夾。 此架構的副作用是它會讓您無法在檔案系統上建立網站的嵌套。 例如，請考慮下列目錄結構。

Web 專案位於 C：/MyWebSite

另一個位於 C：/MyWebSite/Nested 的 Web 專案

當您在 c：/MyWebSite 開啟網站時，此嵌套資料夾會顯示為該應用程式的子資料夾。

<a id="_Toc116100246"></a>

## <a name="http"></a>HTTP

透過 HTTP 開啟網站時，會從 IIS 元資料庫（本機 IIS）或使用 FrontPage Server Extensions （遠端網站）讀取設定。如果有嵌套的 web 應用程式，則會顯示它們，以及將其識別為應用程式的圖示。 如果您熟悉在 FrontPage 中使用 web 應用程式，Visual Studio 2005 中的行為很類似。

即使 Visual Studio 將會顯示應用程式的圖示，而該應用程式位於目前在 IDE 中開啟的應用程式底下，但不允許您將其展開以查看其內容。 不過，您可以按兩下它們來開啟它們。 當您這麼做時，您會看到一個對話方塊，提示您開啟 web 應用程式（並取代目前開啟的方案），或將 Web 應用程式新增至您目前的方案。

![按兩下 [已嵌套的應用程式] 圖示會顯示此對話方塊](improvements-in-visual-studio-2005/_static/image4.jpg)

**圖 7**：按兩下 [已嵌套的應用程式] 圖示會顯示此對話方塊

<a id="_Toc116100247"></a>

## <a name="ftp-site"></a>FTP 站台

當您透過 FTP 開啟網站時，檔案全部都會複製到您的暫存資料夾。 本機儲存位置的完整路徑會顯示在專案的 [屬性] 窗格中，並使用下列格式來建立。

C：/Documents and Settings/&lt;使用者&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;應用程式名稱&gt;

使用 FTP 時，Visual Studio 需要指定專案的基底 URL，讓您可以流覽它，如下所示。 如果您未指定基底 URL，Visual Studio 會在您第一次嘗試流覽網站中的頁面時要求您。

![指定 FTP 網站的基底 URL](improvements-in-visual-studio-2005/_static/image5.jpg)

**圖 8**：指定 FTP 網站的基底 URL

## <a name="improvements-in-compilation"></a>編譯的改良功能

在 Visual Studio 2005 中使用 Web 應用程式的速度，明顯比先前的版本更快。 這在編譯架構的變更中沒有任何小部分。

在 Visual Studio 2002 和2003中，Web 應用程式已編譯成位於/bin 資料夾中的一個主要元件。 在 Visual Studio 2005 中，已新增應用程式/_Code 資料夾。 類別和其他非 UI 程式碼會新增至 App/_Code 資料夾。 當 Visual Studio 建立專案時，會將 App/_Code 資料夾中的所有檔案編譯成單一應用程式/_Code .dll 檔案。 這項變更的結果是，後續組建的速度會比先前的版本快很多。

> [!NOTE]
> MSBuild 命令列公用程式也可以用來建立 ASP.NET Web 應用程式。 模組9將涵蓋該工具。

另一個編譯增強功能是 [建立] 功能表上的 [新增組建頁面] 選項。 這項功能可讓開發人員只重建目前的頁面（當然還有相依性），以便更快速地編譯變更。 由於C#不會針對更新 IntelliSense 等目的提供背景編譯等等，因此從這項功能可以獲益，因為它可讓 IntelliSense 快速地透過重建單一頁面來進行更新。

專案的組建屬性可讓您設定在執行啟動頁面之前所發生的組建類型。 開發人員可以選擇只建立目前的網頁，讓 Visual Studio 可以在程式碼變更之後，更快速地開始偵錯工具。

![組建頁面啟動動作](improvements-in-visual-studio-2005/_static/image6.jpg)

**圖 9**：組建頁面啟動動作

Visual Studio 和 ASP.NET 架構的另一個絕佳增強功能，是在 [編輯後繼續] 區域中。 在 Visual Studio 2005 中，開發人員可以開始對專案進行偵錯工具，並在不中斷偵錯工具的情況下，對專案進行程式碼變更。 事實上，您可以依實際情況開始對專案進行的偵錯工具、新增類別、將程式碼新增至該類別、將程式碼新增至您的頁面，以建立該類別的新實例並執行類別的方法，全都不需要卸離偵錯工具。 執行新的程式碼其實就像重新整理瀏覽器一樣簡單！

按一下這裡以查看 Visual Studio 2005 中 [編輯後繼續] 功能的影片逐步解說。

![](improvements-in-visual-studio-2005/_static/image2.png)

[開啟全螢幕影片](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)

ASP.NET 2.0 和 Visual Studio 2005 中的強大編輯和繼續功能，是因為 ASP.NET 應用程式的架構變更。 在 ASP.NET 1.x 中，Visual Studio 2002/2003 中建立的應用程式會編譯成儲存在/bin 資料夾中的主要元件。 應用程式的所有類別、頁面等等已編譯成該 DLL。 然後在執行時間，ASP.NET 會在頁面中編譯所有的控制項、標記和 ASP.NET 程式碼，並將這些 Dll 複製到 ASP.NET 暫存資料夾中。

在使用 ASP.NET 2.0 的 Visual Studio 2005 中，上述兩種編譯模型（一個適用于 Visual Studio，一個用於執行時間的 ASP.NET）已合併為一個通用的編譯模型。 這表示現在會在開發階段（而不是在執行時間）攔截所有編譯問題。 它也允許設計工具和 IntelliSense 支援的功能，例如使用者控制項和主版頁面。

按一下這裡可查看提供使用者控制項設計工具支援的影片逐步解說。

![](improvements-in-visual-studio-2005/_static/image3.png)

[開啟全螢幕影片](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)

> [!NOTE]
> 從頁面中移除使用者控制項時，@Register 指示詞會保留在標記中，而且應該手動移除，以避免在使用者控制項從網站中刪除時的剖析器錯誤。

Visual Studio 編譯模型的另一項改進是「發行網站」功能。 因為發佈功能會將網站預先編譯，所以開發人員可以享受增加的效能，而不需視需要編譯任何專案。 它也會將 App/_Code 資料夾中的所有原始程式碼都預先編譯成 DLL，因此不需要部署任何原始程式碼。

![[發行網站] 對話方塊](improvements-in-visual-studio-2005/_static/image7.jpg)

**圖 10**： [發行網站] 對話方塊

> [!NOTE]
> Aspnet/_compile .exe 公用程式也可以用來預先編譯 ASP.NET Web 應用程式。 模組9將涵蓋該工具。

當您發行網站時，預先編譯的檔案會儲存在暫存的 ASP.NET Files 資料夾中，如下所示。 副檔名*為 .xml*的檔案為 XML 檔案，可定義特定 dll 的相依性。 任何 Webform 或使用者控制項都會編譯成以*App/_Web/_* 開頭的隨機 dll。

如果您將 [*允許此先行編譯的網站成為可更新*的] 核取方塊保持核取狀態，則 Webforms 和使用者控制項內的標記將不會預先編譯成 DLL，讓您在部署後進行變更。 如果您想要鎖定標記，而不允許變更已部署的內容，請取消核取此方塊。

[*使用固定命名和單一頁面元件*] 核取方塊可讓您停用批次編譯，讓每個頁面都編譯成固定名稱的元件。 未核取此方塊可讓您利用批次編譯。

[在先行*編譯元件上啟用強式命名*] 核取方塊可讓您將先行編譯的元件強式名稱。

> [!NOTE]
> 在 ASP.NET 1.x 中，必須將強式名稱的元件安裝在全域組件快取（GAC）中。 在 ASP.NET 2.0 中，您不需要將強式名稱的元件安裝到 GAC 中。

![ASP.NET 應用程式預先編譯的檔案](improvements-in-visual-studio-2005/_static/image8.jpg)

**圖 11**： ASP.NET 應用程式預先編譯的檔案

> [!NOTE]
> 在上述應用程式中，沒有 web.config 檔案。 如果已經存在，則會在發佈網站進程之後被稱為*PrecompiledApp。*

## <a name="improvements-in-deployment"></a>部署的改良功能

如同 Visual Studio 2002 和2003，Visual Studio 2005 提供複製專案功能。 不過，此功能已在 Visual Studio 2005 中過增強，現在稱為「複製網站」。

[複製網站] 對話方塊會分割成左框架和右框架。 左側的框架稱為「來源網站」，而右邊的框架稱為「遠端網站」。 有些開發人員可能會造成混淆，那就是在右側畫面中顯示的網站不一定是遠端網站。 它可以是本機檔案系統上或 IIS 本機實例上的網站。 此外，在左邊框中顯示的網站不一定是來源網站，因為此對話方塊可讓您從遠端網站發行*至*來源網站。

如果您要將專案複製到遠端網站，該網站上必須安裝 FrontPage Server Extensions。 如果不是，您就必須使用 FTP 進行連接。 另一方面，如果您要將專案複製到本機 IIS 實例，則不需要 FrontPage Server Extensions。

> [!NOTE]
> 如果您嘗試在本機 IIS 實例上建立新的網站，而且已安裝 FrontPage 2002 伺服器延伸模組，您會收到一則錯誤訊息，告訴您 SharePoint 伺服器上不支援建立網站。 在此情況下，您可以選擇安裝 FrontPage 2000 伺服器擴充功能或移除 FrontPage Server Extensions。

按一下這裡以取得複製網站功能的影片逐步解說。

![](improvements-in-visual-studio-2005/_static/image4.png)

[開啟全螢幕影片](improvements-in-visual-studio-2005/_static/copysite1.wmv)

## <a name="improvements-in-debugging"></a>對調試功能的改善

Visual Studio 2005 中的調試功能有四項重要的改良。

- 以非系統管理員的身分在本機進行調試，可能是現成的。
- 編譯專案的 Debug 屬性現在預設為 false。
- 遠端偵錯程式的安裝和設定比以前更容易。
- 您現在可以將透過 FTP 位置開啟的網站進行偵錯工具。

## <a name="debugging-as-a-non-administrator"></a>以非系統管理員的身分進行調試

新增 ASP.NET 程式開發伺服器可讓非系統管理員輕鬆地立即 ASP.NET 現成的應用程式。 在本機檔案系統上執行的 ASP.NET 應用程式進行調試時，Visual Studio 會在登入使用者的內容下啟動 ASP.NET 程式開發伺服器。 之後，該使用者就可以在不進行任何額外設定的情況下，進行應用程式的

## <a name="debug-is-false-by-default"></a>Debug 預設為 False

在 ASP.NET 1.x 中，web.config 檔案之*編譯*元素中的*debug*屬性預設會設定為*true* 。 建議開發人員在將應用程式部署到生產環境之前，將此屬性設定為*false* ，但因為大部分的開發人員都不會完全瞭解將 debug 屬性設定為 true 的結果，所以它們只是保持不存在。

將 debug 屬性設為 true 的最嚴重問題，就是它會停用神經網路批次編譯模型。 因此，每個頁面都會編譯成個別的 DLL。 如果 Web 應用程式是由數千頁組成（不是由任何方法前所未聞），這表示該應用程式會建立數千個小型的 Dll。 雖然這些 Dll 的大小很小，但是它們不會載入記憶體中的任何特定位置。 因此，它們會造成系統記憶體分散，而且可能會導致 OutOfMemoryException 發生。

在 ASP.NET 2.0 中，debug 屬性預設會設定為 false。 如您所見，當開發人員在 Visual Studio 2005 中調試 ASP.NET 應用程式時，系統會提示他們新增已啟用偵測的 web.config 檔案。 這麼做會產生與 ASP.NET 1.x 中相同的缺點，但現在，開發人員會在將應用程式移至生產環境之前，清楚警告屬性應該重設為 false。

## <a name="remote-debugging-setup-and-configuration"></a>遠端偵錯程式安裝和設定

在 Visual Studio 2002/2003 中，遠端偵錯程式依賴機器偵錯工具（mdm）和 vs7jit 處理。 因此，針對遠端偵錯程式問題進行疑難排解通常是客戶的黑色方塊，而對於 PSS 而言，這通常不是那麼好。

Visual Studio 2005 會移除對 wsdl.exe 和 vs7jit 處理的依賴。 相反地，它現在會使用遠端偵錯「監視」服務（msvsmon）。

從遠端在 Visual Studio 2005 中進行調試的需求相當簡單。 您必須先在遠端伺服器上執行 msvsmon，然後再進行調試。 您可以從 Visual Studio CD 安裝遠端偵錯時間監視器，也可以直接從共用執行 msvsmon，而不需要在 Web 服務器上安裝任何專案。

當您執行 msvsmon 時，可能會抱怨封鎖埠以進行遠端偵錯程式。 幸好，您可以輕鬆地在警告對話方塊中直接解除封鎖埠，如下所示。

![Windows 防火牆封鎖遠端偵錯程式的通知](improvements-in-visual-studio-2005/_static/image9.jpg)

**圖 12**： Windows 防火牆封鎖遠端偵錯程式的通知

一旦您解除了偵錯工具所需的通訊埠，就會看到如下所示的遠端偵錯監視。 您可以從這個介面輕鬆地監視連接和變更調試許可權。

![遠端偵錯監視](improvements-in-visual-studio-2005/_static/image10.jpg)

**圖 13**：遠端偵錯監視

您也可以從遠端偵測透過 FTP 開啟的 Web 應用程式。 這些步驟與先前涵蓋的步驟相同。 不過，您必須指定用來流覽 FTP 專案的基底 URL，如本課程模組稍早所述。

## <a name="lab-2"></a>實驗室2

## <a name="remote-debugging-with-visual-studio-2005"></a>使用 Visual Studio 2005 進行遠端偵錯

此實驗室將逐步引導您使用 Visual Studio 2005 進行遠端偵錯。

按一下這裡以取得此實驗室的影片逐步解說。

![](improvements-in-visual-studio-2005/_static/image5.png)

[開啟全螢幕影片](improvements-in-visual-studio-2005/_static/remdebug1.wmv)

此實驗室需要您擁有兩部電腦，一個執行 Visual Studio 2005，另一個執行中的 IIS 5 或更新版本。

1. 開啟 Visual Studio 2005，並在遠端伺服器上建立新的網站。

> [!NOTE]
> 您可以在遠端 IIS 實例上或透過 FTP 來建立網站。

1. 從遠端 Web 服務器，使用 UNC 路徑找出在開發電腦上的 msvsmon，然後加以執行。  
 Msvsmon 的預設位置是//server/c $/Program Files/Microsoft Visual Studio 8/Common7/IDE/Remote 偵錯工具/x86。
2. 如果系統提示您解除封鎖埠以進行遠端偵錯程式，請執行此動作。
3. 在開發電腦上，開啟 default.aspx 的程式碼後置，並在 Page/_Load 方法中設定中斷點。
4. 從開發電腦開始進行調試。

您應該會如預期般到達中斷點。

## <a name="aspnet-development-server"></a>ASP.NET 程式開發伺服器

如先前所討論，Visual Studio 2005 隨附名為 ASP.NET 程式開發伺服器的 Web 服務器。 （ASP.NET 程式開發伺服器有時稱為 Cassini）。這個 Web 服務器是流覽和偵錯工具在檔案系統上執行之 Web 應用程式的便利方法。

ASP.NET 程式開發伺服器是受限制的 Web 服務器。 它不允許遠端連線，它不允許來自啟動 Web 服務器的使用者以外的任何使用者提出任何要求。 它也沒有提供 ASP 網頁的功能。 只會提供 ASP.NET 資源和 HTML 資源（包括影像、CSS 檔案等）。

ASP.NET 程式開發伺服器可以透過命令列來啟動，方法是執行位於 c：/Windows/Microsoft .net/Framework/v2.0./ */* / */* /* 的 webdev.webserver.exe。 下列對話方塊會顯示可用的參數。

![](improvements-in-visual-studio-2005/_static/image11.jpg)

**圖14**

> [!NOTE]
> 透過命令列明確啟動時，不支援 ASP.NET 程式開發伺服器。
