---
uid: visual-studio/overview/2013/using-browser-link
title: 在 Visual Studio 2013 中使用瀏覽器連結 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/04/2013
ms.assetid: 46cbfe20-b4dc-449b-9016-80657dd44fbe
msc.legacyurl: /visual-studio/overview/2013/using-browser-link
msc.type: authoredcontent
ms.openlocfilehash: 723a38de4569b0bb58817c70aabb84fef8e19591
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622903"
---
# <a name="using-browser-link-in-visual-studio-2013"></a>在 Visual Studio 2013 中使用瀏覽器連結

由[Mike Wasson](https://github.com/MikeWasson)

瀏覽器連結是 Visual Studio 2013 中的一項新功能，可在開發環境與一或多個網頁瀏覽器之間建立通道。 您可以使用瀏覽器連結，一次在數個瀏覽器中重新整理 web 應用程式，這對於跨瀏覽器測試很有用。

- [瀏覽器重新整理](#browser-refresh)
- [查看瀏覽器連結儀表板](#dashboard)
- [啟用靜態 HTML 檔案的瀏覽器連結](#static-html)
- [停用瀏覽器連結](#disabling)
- [它如何運作？](#how-it-works)

<a id="browser-refresh"></a>
## <a name="browser-refresh"></a>瀏覽器重新整理

使用瀏覽器重新整理時，您可以透過瀏覽器連結來重新整理連線到 Visual Studio 的多個瀏覽器。

若要使用瀏覽器重新整理，請先使用任何專案範本來建立 ASP.NET 應用程式。 按 F5 或按一下工具列中的箭號圖示，以對應用程式進行 Debug：

![](using-browser-link/_static/image1.png)

您也可以使用下拉式清單來選取要進行偵錯工具的特定瀏覽器。

![](using-browser-link/_static/image2.png)

若要使用多個瀏覽器進行調試，請選取 **[流覽方式]** 。 在 [**流覽方式**] 對話方塊中，按住 CTRL 鍵以選取一個以上的瀏覽器。 按一下 **[流覽]** ，以選取的瀏覽器進行 debug。 瀏覽器連結也適用于從外部 Visual Studio 啟動瀏覽器，並流覽至應用程式 URL 的情況。

![](using-browser-link/_static/image3.png)

瀏覽器連結控制項位於具有圓形箭號圖示的下拉式清單中。 箭號圖示是 [重新整理 **] 按鈕。**

![](using-browser-link/_static/image4.png)

若要查看哪些瀏覽器已連接，請在進行調試時將滑鼠停留在 [重新整理 **] 按鈕上方**。 [已連接的瀏覽器] 會顯示在工具提示視窗中。

![](using-browser-link/_static/image5.png)

若要重新整理已連線的瀏覽器，請按一下 [重新整理 **] 按鈕，** 或按 CTRL + ALT + ENTER。 例如，下列螢幕擷取畫面顯示我使用 MVC 5 專案範本所建立的 ASP.NET 專案。 您可以在頂端的兩個瀏覽器中看到應用程式正在執行。 在底部，專案會在 Visual Studio 中開啟。

![](using-browser-link/_static/image6.png)

在 Visual Studio 中，我變更了首頁的 &lt;h1&gt; 標題：

![](using-browser-link/_static/image7.png)

當我按一下 [重新整理 **] 按鈕時**，變更會同時出現在這兩個瀏覽器視窗中：

![](using-browser-link/_static/image8.png)

**備註**

- 若要啟用瀏覽器連結，請在專案的 Web.config 檔案中，于[&lt;編譯&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx)元素中設定 `debug=true`。
- 應用程式必須在 localhost 上執行。
- 應用程式必須以 .NET 4.0 或更新版本為目標。

<a id="dashboard"></a>
## <a name="viewing-the-browser-link-dashboard"></a>查看瀏覽器連結儀表板

瀏覽器連結儀表板會顯示瀏覽器連結連接的相關資訊。 若要查看儀表板，請選取瀏覽器連結下拉式功能表（[重新整理 **] 按鈕旁邊的小**箭號）。 然後按一下 [**瀏覽器連結儀表板**]。

![](using-browser-link/_static/image9.png)

儀表板會列出已連線的瀏覽器，以及每個瀏覽器導覽的 URL。

![](using-browser-link/_static/image10.png)

[**必要條件**] 區段會顯示啟用該專案的瀏覽器連結所需的任何步驟。 例如，下列螢幕擷取畫面顯示一個專案，其中 Web.config 檔案中的 "debug" 設定為 false。

![](using-browser-link/_static/image11.png)

<a id="static-html"></a>
## <a name="enabling-browser-link-for-static-html-files"></a>啟用靜態 HTML 檔案的瀏覽器連結

若要啟用靜態 HTML 檔案的瀏覽器連結，請將下列程式新增至您的 web.config 檔案。

[!code-xml[Main](using-browser-link/samples/sample1.xml)]

基於效能考慮，請在發行專案時移除此設定。

<a id="disabling"></a>
## <a name="disabling-browser-link"></a>停用瀏覽器連結

預設會啟用瀏覽器連結。 有幾種方式可以停用它：

- 在 [瀏覽器連結] 下拉式功能表中，取消核取 [**啟用瀏覽器連結**]。 

    ![](using-browser-link/_static/image12.png)
- 在 web.config 檔案中，于 appSettings 區段中新增名為 "vs： EnableBrowserLink" 的索引鍵，其值為 "false"。 

    [!code-xml[Main](using-browser-link/samples/sample2.xml)]
- 在 web.config 檔案中，將 debug 設為 false。 

    [!code-xml[Main](using-browser-link/samples/sample3.xml)]

<a id="how-it-works"></a>
## <a name="how-does-it-work"></a>它如何運作？

瀏覽器連結會使用[SignalR](../../../signalr/index.md)來建立 Visual Studio 與瀏覽器之間的通道。 啟用瀏覽器連結時，Visual Studio 會作為多個用戶端（瀏覽器）可以連接的 SignalR 伺服器。 瀏覽器連結也會向 ASP.NET 註冊 HTTP 模組。 此模組會將特殊的 &lt;腳本&gt; 參考插入伺服器中的每個頁面要求。 您可以在瀏覽器中選取 [View source]，以查看腳本參考。

![](using-browser-link/_static/image13.png)

您的原始程式檔不會遭到修改。 HTTP 模組會動態插入腳本參考。

因為瀏覽器端程式碼是所有的 JavaScript，所以它適用于所有[SignalR 支援](../../../signalr/overview/getting-started/supported-platforms.md)的瀏覽器，而不需要任何瀏覽器外掛程式。
