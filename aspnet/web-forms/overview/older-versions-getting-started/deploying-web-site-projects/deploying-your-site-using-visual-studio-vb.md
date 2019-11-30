---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-visual-studio-vb
title: 使用 Visual Studio 部署您的網站（VB） |Microsoft Docs
author: rick-anderson
description: Visual Studio 包含用來部署網站的工具。 在本教學課程中深入瞭解這些工具。
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 977105f3-7987-4e50-8be7-afb53b4ca28a
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-visual-studio-vb
msc.type: authoredcontent
ms.openlocfilehash: 6c71e36a8a434947882cc767cd2f903ff6e8d422
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74582411"
---
# <a name="deploying-your-site-using-visual-studio-vb"></a>使用 Visual Studio 部署您的網站 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_04_VB.zip)或[下載 PDF](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial04_DeployingViaVS_vb.pdf)

> Visual Studio 包含用來部署網站的工具。 在本教學課程中深入瞭解這些工具。

## <a name="introduction"></a>簡介

先前的教學課程探討了如何將簡單的 ASP.NET web 應用程式部署到 web 主機提供者。 具體來說，本教學課程示範了如何使用 FileZilla 之類的 FTP 用戶端，將必要的檔案從開發環境轉移到生產環境。 Visual Studio 也提供內建工具，可協助您部署至 web 主機提供者。 本教學課程會檢查其中兩項工具：複製網站工具，可讓您使用 FTP 或 FrontPage Server Extensions 在遠端 Web 服務器之間移動檔案;而發佈工具會將整個網站複製到指定的位置。

> [!NOTE]
> Visual Studio 提供的其他部署相關工具組括[Web 安裝專案](https://msdn.microsoft.com/library/wx3b589t.aspx)和[web 部署專案](https://www.microsoft.com/downloads/details.aspx?FamilyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&amp;displaylang=en)增益集。 Web 安裝專案會將網站的內容和設定資訊封裝成單一 MSI 檔案。 此選項最適用于部署在內部網路內的網站，或銷售預先封裝的 web 應用程式（客戶在自己的網頁伺服器上安裝）的公司。 Web 部署專案增益集是一個 Visual Studio 增益集，可協助您指定開發環境和生產環境的組建之間的設定差異。 本教學課程系列不討論 Web 安裝專案;Web 部署專案會在[*開發與生產*](common-configuration-differences-between-development-and-production-vb.md)教學課程的一般設定差異中摘要說明。

## <a name="deploying-your-site-using-the-copy-web-site-tool"></a>使用複製網站工具部署您的網站

Visual Studio 的複製網站工具與獨立 FTP 用戶端的功能類似。 簡言之，「複製網站」工具可讓您透過 FTP 或 FrontPage Server Extensions 連接到遠端網站。 類似于 FileZilla 的使用者介面，「複製網站」使用者介面包含兩個窗格：左窗格會列出本機檔案，而右窗格則會列出目的地伺服器上的這些檔案。

> [!NOTE]
> 「複製網站」工具僅適用于網站專案。 當您使用 Web 應用程式專案時，Visual Studio 會提供這種工具。

讓我們看一下如何使用「複製網站」工具，將書籍審查應用程式發佈到生產環境。 由於「複製網站」工具僅適用于使用網站專案模型的專案，因此我們只能檢查使用此工具與 BookReviewsWSP 專案。 開啟該專案。

按一下 方案總管中的 複製網站 圖示，以啟動 複製網站 工具專案（在 圖 1 中將此圖示圈起來）;或者，您可以從 網站 功能表中選取 複製網站 選項。 任一種方法都會啟動複製網站使用者介面，如 [圖 1] 所示。只有 [圖 1] 中的左窗格會填入，因為我們尚未連接到遠端伺服器。

[![複製網站工具的使用者介面分成兩個窗格](deploying-your-site-using-visual-studio-vb/_static/image2.png)](deploying-your-site-using-visual-studio-vb/_static/image1.png)

**圖 1**：複製網站工具的使用者介面分成兩個窗格（[按一下以觀看完整大小的影像](deploying-your-site-using-visual-studio-vb/_static/image3.png)）

為了部署我們的網站，我們必須先連接到 web 主機提供者。 按一下 [複製網站] 使用者介面頂端的 [連接] 按鈕。 這會顯示 [圖 2] 所示的 [開啟網站] 對話方塊。

您可以從左側選取四個選項的其中一個，以連接到目的地網站：

- **檔案系統**-選取此功能，將您的網站部署到可從您的電腦存取的資料夾或網路共用。
- **本機 IIS** -使用此選項可將網站部署到安裝在您電腦上的 IIS web 伺服器。
- **Ftp 網站**-使用 ftp 連接到遠端網站。
- **遠端網站**-使用 FrontPage Server Extensions 連接到遠端網站。

大部分的 web 主機提供者都支援 FTP，但較少的提供 FrontPage 伺服器擴充功能支援。 基於這個理由，我選取了 [FTP 網站] 選項，然後輸入連接資訊，如 [圖 2] 所示。

[![指定目的地網站](deploying-your-site-using-visual-studio-vb/_static/image5.png)](deploying-your-site-using-visual-studio-vb/_static/image4.png)

**圖 2**：指定目的地網站（[按一下以查看完整大小的影像](deploying-your-site-using-visual-studio-vb/_static/image6.png)）

連接之後，[複製網站] 工具會將檔案載入右窗格中的遠端網站，並指出每個檔案的狀態： [新增]、[已刪除]、[已變更] 或 [未變更]。 您可以從本機網站將檔案複製到遠端網站，反之亦然。

讓我們將新頁面新增至 BookReviewsWSP 專案，然後加以部署，讓我們可以看到「複製網站」工具的實際運作。 在名為 `Privacy.aspx`的根目錄中，于 Visual Studio 建立新的 ASP.NET 網頁。 讓頁面使用主版頁面 `Site.master`，並將您網站的隱私權原則加入此頁面。 [圖 3] 顯示在建立此頁面之後 Visual Studio。

[![將名為 &lt;code&gt;default.aspx&lt;/code&gt; 的新頁面新增至網站的根資料夾](deploying-your-site-using-visual-studio-vb/_static/image8.png)](deploying-your-site-using-visual-studio-vb/_static/image7.png)

**圖 3**：將名為 `Privacy.aspx` 的新頁面新增至網站的根資料夾（[按一下以查看完整大小的影像](deploying-your-site-using-visual-studio-vb/_static/image9.png)）

接下來，返回「複製網站」使用者介面。 如 [圖 4] 所示，左窗格現在包含新的檔案-`Policy.aspx` 和 `Policy.aspx.vb`。 還有什麼，這些檔案會以箭號圖示和 [新增] 狀態標示，表示它們存在於本機網站，而不是在遠端網站上。

[![複製網站工具在左窗格中包含新的 &lt;程式碼&gt;default.aspx&lt;/code&gt; 頁面](deploying-your-site-using-visual-studio-vb/_static/image11.png)](deploying-your-site-using-visual-studio-vb/_static/image10.png)

**圖 4**：複製網站工具在左窗格中包含新的 `Privacy.aspx` 頁面（[按一下以觀看完整大小的影像](deploying-your-site-using-visual-studio-vb/_static/image12.png)）

若要部署新檔案，請選取它們，然後按一下箭號圖示，將其傳送至遠端網站。 在傳送完成之後，本機和遠端網站上的 `Policy.aspx` 和 `Policy.aspx.vb` 檔案都存在，而且狀態不會變更。

除了列出新的檔案，「複製網站」工具也會反白顯示本機和遠端網站之間的任何不同檔案。 若要查看其實際運作情況，請回到 [`Privacy.aspx`] 頁面，再將幾個字新增至隱私權原則。 儲存頁面，然後返回 [複製網站] 工具。 如 [圖 5] 所示，左窗格中的 [`Privacy.aspx`] 頁面狀態為 [已變更]，表示它與遠端網站不同步。

[![[複製網站] 工具表示 &lt;程式碼&gt;隱私權&lt;/code&gt; 頁面已變更](deploying-your-site-using-visual-studio-vb/_static/image14.png)](deploying-your-site-using-visual-studio-vb/_static/image13.png)

[**圖 5**]：複製網站工具指出 [`Privacy.aspx`] 頁面已變更（[按一下以觀看完整大小的影像](deploying-your-site-using-visual-studio-vb/_static/image15.png)）

複製網站工具也會指出自從上次複製作業之後是否已刪除檔案。 從本機專案中刪除 `Privacy.aspx`，然後重新整理 [複製網站] 工具。 `Privacy.aspx` 和 `Privacy.aspx.vb` 檔案仍會列在左窗格中，但會有 [已刪除] 狀態，指出自上次複製作業後已將其移除。

## <a name="publishing-a-web-application"></a>發行 Web 應用程式

從 Visual Studio 中部署 web 應用程式的另一種方式是使用 [發行] 選項，您可以透過 [建立] 功能表存取此選項。 [發行] 選項會明確編譯應用程式，然後將所有必要的檔案複製到指定的遠端網站。 如我們稍後所見，[發行] 選項比 [複製網站] 工具更為鈍。 雖然複製網站工具可讓您檢查本機和遠端網站上的檔案，並允許您視需要上傳或下載個別檔案，但 [發行] 選項會部署整個 Web 應用程式。

除了將所有必要的檔案複製到指定的遠端網站以外，[發佈] 選項也會明確地編譯應用程式。 假設 Web 應用程式專案需要進行明確編譯，則 Web 應用程式專案的 [發行] 選項就不會有任何驚訝。 有點令人驚訝的是，[發行] 選項也適用于網站專案。 如[*判斷需要部署哪些*](determining-what-files-need-to-be-deployed-vb.md)檔案教學課程中所述，您可以透過稱為*預先編譯*的進程來明確編譯網站專案。 本教學課程著重于搭配 Web 應用程式專案使用 Publish 選項;未來的教學課程將探索預先編譯，此時我們會回頭查看如何搭配網站專案使用 [發行] 選項。

> [!NOTE]
> 雖然 [發行] 選項同時適用于網站專案和 Web 應用程式專案的 Visual Studio，但 Visual Web Developer 只提供 Web 應用程式專案的 [發行] 選項。

讓我們看看使用 [發行] 選項部署書籍審查應用程式。 一開始請開啟 Visual Studio 中的 BookReviewsWAP （Web 應用程式專案）。 從 [發佈] 功能表選擇 [組建 BookReviewsWAP] 專案。 這會出現一個對話方塊，提示您輸入目標位置，還有其他設定選項（請參閱 [圖 6]）。 與複製網站工具很類似，您可以輸入指向本機資料夾的位置、IIS 上的本機網站、支援 FrontPage Server Extensions 的遠端網站，或 FTP 伺服器位址。 您可以選擇是否要使用已部署的檔案來取代遠端 web 伺服器上的檔案，或是在發佈之前刪除遠端網站上的所有內容。 您也可以指定是否要複製：

- 只有專案中執行應用程式所需的檔案，這會省略不必要的原始程式碼和專案相關檔案。
- 所有專案檔，包括原始程式碼檔案和 Visual Studio 專案檔，例如方案檔。
- 來源專案資料夾中的所有檔案，會複製來源專案資料夾中的所有檔案，不論它們是否包含在專案中。

您也可以選擇上傳 `App_Data` 資料夾的內容。

[![指定目的地網站](deploying-your-site-using-visual-studio-vb/_static/image17.png)](deploying-your-site-using-visual-studio-vb/_static/image16.png)

**圖 6**：指定目的地網站（[按一下以查看完整大小的影像](deploying-your-site-using-visual-studio-vb/_static/image18.png)）

在書籍審查應用程式中，遠端網站包含透過複製網站工具複製 BookReviewsWSP 專案時所部署的檔案。 因此，讓我們先從刪除所有現有的內容開始發行選項。 此外，讓我們只複製必要的檔案，而不是使用不必要的原始程式碼和專案檔來塞滿生產環境。 指定這些選項之後，請按一下 [發行] 按鈕。 在接下來的幾秒內 Visual Studio 會將必要的檔案部署到目的地網站，並在 [輸出] 視窗中顯示其進度。

[圖 7] 顯示在發行作業完成後，FTP 網站上的檔案。 請注意，只有標記頁面和必要的伺服器和用戶端支援檔案已上傳。

[只 ![所需的檔案已發佈到生產環境](deploying-your-site-using-visual-studio-vb/_static/image20.png)](deploying-your-site-using-visual-studio-vb/_static/image19.png)

**圖 7**：只有所需的檔案已發佈至生產環境（[按一下以觀看完整大小的影像](deploying-your-site-using-visual-studio-vb/_static/image21.png)）

[發行] 選項比 [複製網站] 工具的差別細微工具少。 雖然「複製網站」工具可讓您檢查本機和遠端網站上的檔案，並瞭解它們有何不同，但 [發行] 選項不會提供這類介面。 此外，「複製網站」工具可讓您進行一次性變更、上傳或刪除個別檔案。 [發行] 選項不允許這樣的精細控制;相反地，它會發佈*整個*應用程式。 這種行為有其優缺點。 在加號上，當您使用 [發佈] 選項時，就不會忘了上傳重要的檔案。 但是，如果您對非常大的網站進行了少許變更，請考慮使用 [發佈] 選項，您無法更新該頁面或已修改的兩個，而必須等到 Visual Studio 部署整個網站時，才會發生什麼情況。

有些檔案的內容在生產和開發環境之間有所不同，並不罕見。 主要的範例是應用程式的設定檔，`Web.config`。 由於 Publish 選項會盲目複製 web 應用程式檔，因此它會以開發環境中的版本覆寫生產環境的自訂設定檔。 後續的教學課程會進一步探索此主題，並提供部署 web 應用程式的秘訣（當有這類差異時）。

## <a name="summary"></a>總結

部署網站牽涉到從開發環境將必要的檔案複製到生產環境。 先前的教學課程示範了如何使用 FTP 用戶端（例如 FileZilla）來傳輸檔案。 本教學課程在 Visual Studio 中檢查了兩種部署工具：複製網站工具和發佈選項。 複製網站工具類似于 FTP 用戶端，因為它有兩個窗格的介面，列出本機電腦上的檔案和指定的遠端電腦，可讓您輕鬆地在兩部電腦之間上傳或下載檔案。 [發行] 選項是更鈍的工具，可明確地編譯專案，然後將整個應用程式部署到指定的目的地。

快樂的程式設計！

### <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [使用複製網站工具複製網站](https://msdn.microsoft.com/library/1cc82atw.aspx)
- [如何：使用複製網站工具來部署網站](../../../videos/how-do-i/how-do-i-deploy-a-web-site-using-the-copy-web-site-tool.md)（影片）
- [如何：發行 Web 應用程式專案](https://msdn.microsoft.com/library/aa983453.aspx)
- [How To：發行網站](https://msdn.microsoft.com/library/20yh9f1b.aspx)
- [Visual Studio 中的安裝程式和部署專案](https://msdn.microsoft.com/library/wx3b589t.aspx)

> [!div class="step-by-step"]
> [上一頁](deploying-your-site-using-an-ftp-client-vb.md)
> [下一頁](common-configuration-differences-between-development-and-production-vb.md)
