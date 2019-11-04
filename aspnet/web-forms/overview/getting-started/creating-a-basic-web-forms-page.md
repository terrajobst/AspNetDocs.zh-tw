---
uid: web-forms/overview/getting-started/creating-a-basic-web-forms-page
title: 使用 Visual Studio 2013 建立基本的 ASP.NET 4.5 Web Forms 網頁
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: a2f1c635-0817-4a9a-8c13-d5b5d29727c0
msc.legacyurl: /web-forms/overview/getting-started/creating-a-basic-web-forms-page
msc.type: authoredcontent
ms.openlocfilehash: 5d13a51128eecd92a82cfd06054448582a348e11
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445682"
---
# <a name="using-visual-studio-2013-to-create-a-basic-aspnet-45-web-forms-page"></a>使用 Visual Studio 2013 建立基本的 ASP.NET 4.5 Web Forms 網頁

依[Erik Reitan](https://github.com/Erikre)

[!INCLUDE[](~/includes/rp.md)]

本逐步解說提供[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)和[web Microsoft Visual Studio Express 2013](https://www.microsoft.com/visualstudio/11/downloads#express-web)中 網頁程式開發環境的簡介。 本逐步解說會引導您建立簡單的 ASP.NET Web form 頁面，並說明建立新頁面、加入控制項和撰寫程式碼的基本技巧。

這個逐步解說中所述的工作包括：

- 建立檔案系統 Web Forms 應用程式專案。
- 使用 Visual Studio 熟悉自己。
- 建立 ASP.NET 網頁。
- 加入控制項。
- 加入事件處理常式。
- 從 Visual Studio 執行和測試頁面。

## <a name="prerequisites"></a>Prerequisites

若要完成這個逐步解說，您將需要：

- [適用于 Web 的](https://www.microsoft.com/visualstudio/11/downloads#express-web) [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)或 Microsoft Visual Studio Express 2013。 .NET Framework 會自動安裝。 

    > [!NOTE] 
    > 
    > Microsoft Visual Studio 2013 和 Microsoft Visual Studio Express 2013 for Web 通常會在本教學課程系列中稱為 Visual Studio。  
    >   
    > 如果您使用 Visual Studio，本逐步解說會假設您在第一次啟動 Visual Studio 時選取了 [ **Web 開發**] 集合。 如需詳細資訊，請參閱[如何：選取 Web 開發環境設定](https://msdn.microsoft.com/library/ff521558.aspx)。

## <a name="creating-a-web-application-project-and-a-page"></a>建立 Web 應用程式專案和頁面

<a id="sectionToggle0"></a>

在逐步解說的這個部分中，您將建立 Web 應用程式專案，並在其中加入新的頁面。 您也會新增 HTML 文字，並在瀏覽器中執行頁面。

### <a name="to-create-a-web-application-project"></a>若要建立 Web 應用程式專案

1. 開啟 Microsoft Visual Studio。
2. 在 [檔案] 功能表上，選取 [新增專案]。  
    ![檔案 功能表](creating-a-basic-web-forms-page/_static/image1.png)

    [ **新增專案** ] 對話方塊隨即出現。
3. 選取左側的 [&gt; **Visual C#**  -&gt; **Web** templates] 群組 -**範本**。
4. 在中間的資料行中選擇 [ **ASP.NET Web 應用程式**] 範本。
5. 將專案命名為***BasicWebApp*** ，然後按一下 [**確定]** 按鈕。   
![[新增專案] 對話方塊](creating-a-basic-web-forms-page/_static/image2.png)
6. 接下來，選取 [ **Web** form] 範本，然後按一下 [**確定]** 按鈕以建立專案。  
![新增 ASP.NET 專案 對話方塊](creating-a-basic-web-forms-page/_static/image3.png)  

    Visual Studio 會建立新的專案，其中包含根據 Web form 範本預先建立的功能。 它不只會提供您一個*首頁 .aspx* *頁面，* 也就是一個*Contact .aspx*頁面，但也包含成員資格功能，可註冊使用者並儲存其認證，讓他們可以登入您的網站。 建立新的頁面時，根據預設，Visual Studio 會在**原始**檔視圖中顯示頁面，您可以在其中看到頁面的 HTML 元素。 下圖顯示當您建立名為*BasicWebApp*的新網頁時，您會在 [**原始**檔視圖] 中看到的內容。  
    ![原始碼檢視](creating-a-basic-web-forms-page/_static/image4.png)

### <a name="a-tour-of-the-visual-studio-web-development-environment"></a>Visual Studio Web 開發環境的導覽

在您繼續修改頁面之前，請先熟悉 Visual Studio 開發環境。 下圖顯示 Visual Studio 和 Web Visual Studio Express 中可用的 windows 和工具。

> [!NOTE] 
> 
> 此圖顯示預設視窗和視窗位置。 [ **View** ] 功能表可讓您顯示其他視窗，以及重新排列和調整視窗大小以符合您的喜好設定。 如果已經對視窗排列進行變更，您看到的內容將不符合圖例。

 Visual Studio 環境

![Visual Studio 環境](creating-a-basic-web-forms-page/_static/image5.png)

### <a name="familiarize-yourself-with-the-web-designer"></a>熟悉 Web 設計工具

檢查上圖，並將文字與下列清單比對，其中描述最常用的 windows 和工具。 （並非所有您看到的視窗和工具都會列在這裡，只有在上圖中標示的）。

- '. 提供用來格式化文字、尋找文字等等的命令。 只有當您在**設計**視圖中工作時，才可以使用某些工具列。
- **方案總管** 視窗。 顯示 Web 應用程式中的檔案和資料夾。
- 文件視窗。 在索引標籤式視窗中顯示您正在處理的檔。 您可以按一下 [索引標籤]，在檔之間切換。
- [**屬性**] 視窗。 可讓您變更頁面、HTML 元素、控制項和其他物件的設定。
- [視圖] 索引標籤。 為您提供相同檔的不同視圖。 **設計**視圖是近 WYSIWYG 的編輯介面。 [**來源**視圖] 是網頁的 HTML 編輯器。 **分割**視圖會同時顯示檔的**設計**視圖和**原始**檔視圖。 稍後在本逐步解說中，您將會使用**設計**和**來源**視圖。 如果您想要在**設計**視圖中開啟網頁，請在 [**工具**] 功能表上，按一下 [**選項**]，選取 [ **HTML 設計**工具] 節點，然後變更 [**起始頁于**] 選項。
- **工具箱**。 提供您可以拖曳至頁面上的控制項和 HTML 元素。 [**工具箱**] 元素是依一般函式分組。
- S **Erver Explorer**。 顯示資料庫連接。 如果看不到伺服器總管，請按一下 [View] 功能表上的 [伺服器總管]。

### <a name="creating-a-new-aspnet-web-forms-page"></a>建立新的 ASP.NET Web Forms 頁面

當您使用**ASP.NET Web 應用程式**專案範本建立新的 Web form 應用程式時，Visual Studio 會新增名為*default.aspx*的 ASP.NET 網頁（Web form 網頁），以及其他數個檔案和資料夾。 您可以使用*預設的 .aspx*頁面作為 Web 應用程式的首頁。 不過，在此逐步解說中，您將建立並使用新的頁面。

### <a name="to-add-a-page-to-the-web-application"></a>若要將頁面新增至 Web 應用程式

1. 關閉*default.aspx*頁面。 若要這麼做，請按一下顯示檔案名的索引標籤，然後按一下 [關閉] 選項。
2. 在**方案總管**中，以滑鼠**按右鍵 Web**應用程式名稱（在本教學課程中，應用程式名稱是**BasicWebSite**），然後按一下 [新增 -&gt;**新專案**]。   
隨即顯示 [ 新增項目] 對話方塊。
3. 選取左側的 [ **Visual C#**  -&gt; **Web**範本] 群組。 然後，從中間清單中選取 [ **Web Form** ]，並將它命名為*FirstWebPage .aspx*。   
    ![加入新專案 對話方塊](creating-a-basic-web-forms-page/_static/image6.png)
4. 按一下 [**新增**]，將網頁新增至您的專案。  
Visual Studio 會建立新的頁面，並開啟它。

### <a name="adding-html-to-the-page"></a>將 HTML 新增至頁面

在本逐步解說的這個部分中，您將會在頁面中新增一些靜態文字。

### <a name="to-add-text-to-the-page"></a>若要將文字加入至頁面

1. 在文件視窗的底部，按一下 [**設計**] 索引標籤以切換至**設計**視圖。

    設計檢視以類似 WYSIWYG 的方式顯示目前的頁面。 此時，您在頁面上沒有任何文字或控制項，因此頁面是空白的，但外框的虛線除外。 此矩形代表頁面上的**div**元素。
2. 在以虛線框住的矩形內部按一下。
3. 輸入**歡迎使用 Visual Web Developer** ，然後按兩次**enter**鍵。

    下圖顯示您在 [**設計**視圖] 中輸入的文字。

    ![設計檢視中的歡迎文字](creating-a-basic-web-forms-page/_static/image7.png "設計檢視中的歡迎文字")
4. 切換至**來源**視圖。

    當您在 [**設計**視圖] 中輸入時，您可以在 [**原始**檔] 視圖中看到您所建立的 HTML。  
    具有靜態文字](creating-a-basic-web-forms-page/_static/image8.png) ![網頁

### <a name="running-the-page"></a>正在執行頁面

將控制項新增至頁面之前，您可以先執行它。

### <a name="to-run-the-page"></a>若要執行頁面

1. 在**方案總管**中，以滑鼠右鍵按一下 [ *FirstWebPage* ]，然後選取 [**設定為起始頁**]。
2. 按**CTRL + F5**執行頁面。

    網頁會顯示在瀏覽器中。 雖然您建立的頁面副檔名為 *.aspx*，但它目前的執行方式就像任何 HTML 網頁一樣。

    若要在瀏覽器中顯示頁面，您也可以在**方案總管**中的頁面上按一下滑鼠右鍵，然後**在瀏覽器中**選取 [View]。
3. 關閉瀏覽器以停止 Web 應用程式。

## <a name="adding-and-programming-controls"></a>加入和程式設計控制項

<a id="sectionToggle1"></a>

您現在會將伺服器控制項加入至頁面。 伺服器控制項（例如按鈕、標籤、文字方塊和其他熟悉的控制項）可為您的 Web form 頁面提供一般表單處理功能。 不過，您可以使用在伺服器上執行的程式碼（而非用戶端）來設計控制項。

您會將[按鈕](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控制項、 [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控制項和[Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控制項加入至頁面，並撰寫程式碼來處理[按鈕](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控制項的[Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件。

### <a name="to-add-controls-to-the-page"></a>若要將控制項加入至頁面

1. 按一下 [**設計**] 索引標籤，切換至 [**設計**視圖]。
2. 將插入點放在 [**歡迎使用 Visual Web Developer** ] 文字的結尾，然後按**enter**五次或多次，以在 [ **div**元素] 方塊中建立一些空間。
3. 在 [**工具箱**] 中，展開 [**標準**] 群組（如果尚未展開）。  
請注意，您可能需要展開左側的 [**工具箱**] 視窗以進行觀看。
4. 將[TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控制項拖曳至頁面上，並將它放在第一行**歡迎使用 Visual Web Developer**的**div**元素方塊中間。
5. 將 [ [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) ] 控制項拖曳至頁面上，並將它放在[TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控制項的右邊。
6. 將 [[標籤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)] 控制項拖曳至頁面上，並將它放在[按鈕](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控制項下方的另一行。
7. 將插入點放在[TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控制項上方，然後輸入**Enter：** 。

    此靜態 HTML 文字是[TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)控制項的標題。 您可以在相同頁面上混合使用靜態 HTML 和伺服器控制項。 下圖顯示三個控制項在**設計**視圖中的顯示方式。

    ![設計檢視中的三個控制項](creating-a-basic-web-forms-page/_static/image9.png "設計檢視中的三個控制項")

### <a name="setting-control-properties"></a>設定控制項屬性

Visual Studio 提供各種方式，讓您在頁面上設定控制項的屬性。 在本逐步解說的這個部分中，您將會在**設計**視圖和**原始**檔視圖中設定屬性。

### <a name="to-set-control-properties"></a>若要設定控制項屬性

1. 首先，從 [**流覽**] 功能表中選取，以顯示 [**屬性**] 視窗-&gt;**其他 Windows** -&gt; [**屬性] 視窗**。 您也可以選取**F4**顯示 [**屬性**] 視窗。
2. 選取 [[按鈕](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)] 控制項，然後在 [**屬性**] 視窗中，將 [**文字**] 的值設定為 [**顯示名稱**]。 您輸入的文字會出現在設計工具中的按鈕上，如下圖所示。

    ![設定按鈕文字](creating-a-basic-web-forms-page/_static/image10.png "設定按鈕文字")
3. 切換至**來源**視圖。

    **來源**視圖會顯示網頁的 HTML，包括 Visual Studio 為伺服器控制項建立的元素。 控制項是使用類似 HTML 的語法來宣告，不同的是，標記會使用前置詞**asp：** ，並包含屬性**runat =&quot;server&quot;** 。

    控制項屬性會宣告為屬性。 例如，當您在步驟1中設定[按鈕](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控制項的[text](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.text.aspx)屬性時，實際上是在控制項的標記中設定**text**屬性。

    > [!NOTE] 
    > 
    > 所有控制項都是在**form**元素內部，也就是屬性**runat =&quot;server&quot;** 。 **Runat =&quot;server&quot;** 屬性，以及控制項標記的**asp：** 前置詞會標記控制項，以便在頁面執行時由伺服器上的 ASP.NET 處理。 &lt;form runat 以外的程式碼 **&quot;server&quot;&gt;** 和 **&lt;script runat =&quot;server&quot;&gt;** 專案會原封不動地傳送至瀏覽器，這就是為什麼 ASP.NET 程式碼必須位於元素內的原因。其開頭標記包含**runat =&quot;server&quot;** 屬性。
4. 接下來，您會將其他屬性新增至[標籤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控制項。 將插入點直接放在 [ **&lt;asp： label]&gt;** 標記中的 [ **asp： label** ] 後面，然後按**空格鍵**。

    此時會出現一個下拉式清單，顯示您可以為[標籤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控制項設定的可用屬性清單。 這項功能稱為**IntelliSense**，可協助您在**原始**檔中，使用伺服器控制項、HTML 元素和頁面上其他專案的語法。 下圖顯示 [[標籤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)] 控制項的 [ **IntelliSense** ] 下拉式清單。

    ![IntelliSense 屬性](creating-a-basic-web-forms-page/_static/image11.png "IntelliSense 屬性")
5. 選取 [**前景**]，然後輸入等號。

    IntelliSense 會顯示色彩清單。

    > [!NOTE] 
    > 
    > 您可以在 [流覽程式碼] 時按下**CTRL + J** ，隨時顯示 [ **IntelliSense** ] 下拉式清單。
6. 選取 **[標籤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)** 控制項文字的色彩。 請確定您選取的色彩夠深，可以針對白色背景閱讀。

    **前景**屬性是以您選取的色彩完成，包括右引號。

### <a name="programming-the-button-control"></a>程式設計按鈕控制項

在此逐步解說中，您將撰寫程式碼，以讀取使用者在文字方塊中輸入的名稱，然後在 [[標籤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)] 控制項中顯示名稱。

### <a name="add-a-default-button-event-handler"></a>新增預設按鈕事件處理常式

1. 切換至**設計**視圖。
2. 按兩下 [[按鈕](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)] 控制項。

    根據預設，Visual Studio 會切換至程式碼後置檔案，並建立[按鈕](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控制項的預設事件（ [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件）的基本架構事件處理常式。 程式碼後置檔案會將您的 UI 標記（例如 HTML）與您的伺服器程式碼C#隔開（例如）。   
   游標會定位於此事件處理常式的加入程式碼。

    > [!NOTE] 
    > 
    > 在 [**設計**視圖] 中按兩下控制項，只是您可以建立事件處理常式的數種方式之一。
3. 在**Button1\_按一下**[事件處理常式]，輸入**Label1** ，後面接著句號（ **.** ）。

    當您在標籤（**Label1**）的**識別碼**之後輸入句點時，Visual Studio 會顯示[標籤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)控制項的可用成員清單，如下圖所示。 成員通常是屬性、方法或事件。

    ![程式碼視圖中的 IntelliSense](creating-a-basic-web-forms-page/_static/image12.png "程式碼檢視中的 IntelliSense")
4. 完成按鈕的**Click**事件處理常式，使其讀取，如下列程式碼範例所示。

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample1.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample2.vb?highlight=2)]
5. 以滑鼠右鍵按一下**方案總管**中的 [ *FirstWebPage* ]，然後選取 [**視圖標記**]，切換回流覽 HTML 標籤的**來源**視圖。
6. 流覽至 [ **&lt;asp：] 按鈕&gt;** 元素。 請注意， **&lt;asp： Button&gt;** 元素現在具有屬性**Onclick =&quot;Button1\_按一下 [&quot;** ]。

    這個屬性會將按鈕的[Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件系結至您在上一個步驟中編碼的處理常式方法。

    事件處理常式方法可以有任何名稱;您看到的名稱是 Visual Studio 所建立的預設名稱。 重點是，HTML 中用於**OnClick**屬性的名稱必須符合程式碼後置中定義之方法的名稱。

### <a name="running-the-page"></a>正在執行頁面

您現在可以在頁面上測試伺服器控制項。

### <a name="to-run-the-page"></a>若要執行頁面

1. 按**CTRL + F5**在瀏覽器中執行頁面。 如果發生錯誤，請重新檢查上述步驟。
2. 在文字方塊中輸入名稱，然後按一下 [**顯示名稱**] 按鈕。

    您輸入的名稱會顯示在 [[標籤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)] 控制項中。 請注意，當您按一下按鈕時，頁面就會張貼到 Web 服務器。 ASP.NET 接著會重新建立頁面，執行您的程式碼（在此案例中，[按鈕](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)控制項的[Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件處理常式會執行），然後將新頁面傳送至瀏覽器。 如果您在瀏覽器中監看狀態列，您可以看到頁面在每次按一下按鈕時，都會往返 Web 服務器。
3. 在瀏覽器中，以滑鼠右鍵按一下頁面，然後選取 [ **view source**]，以查看您正在執行之網頁的來源。

    在頁面原始碼中，您會看到不含任何伺服器程式碼的 HTML。 具體而言，您看不到您在**原始**檔視圖中使用的 **&lt;asp：&gt;** 元素。 當頁面執行時，ASP.NET 會處理伺服器控制項，並將 HTML 專案轉譯成頁面，以執行代表控制項的函式。 例如， **&lt;asp： Button&gt;** 控制項會轉譯為 HTML **&lt;輸入類型 =&quot;提交&quot;&gt;** 元素。
4. 關閉瀏覽器。

## <a name="working-with-additional-controls"></a>使用其他控制項

<a id="sectionToggle2"></a>

在本逐步解說的這個部分中，您將使用[Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制項，這會一次顯示一個月的日期。 行事[曆](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制項比您使用的按鈕、文字方塊和標籤更為複雜，並說明伺服器控制項的一些進一步功能。

在本節中，您會將[WebControls](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)新增至頁面，並將其格式化。

### <a name="to-add-a-calendar-control"></a>若要加入行事曆控制項

1. 在 Visual Studio 中，切換至 [**設計**視圖]。
2. 從 [**工具箱**] 的 [**標準**] 區段中，將行事[曆](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制項拖曳至頁面上，並放在包含其他控制項的**div**元素下方。

    行事曆的智慧標籤面板隨即顯示。 此面板會顯示命令，讓您輕鬆地為選取的控制項執行最常見的工作。 下圖顯示在**設計**視圖中呈現的行事[曆](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制項。

    ![設計檢視中的行事曆控制項](creating-a-basic-web-forms-page/_static/image13.png "設計檢視中的 Calendar 控制項")
3. 在智慧標籤面板中，選擇 [**自動格式化**]。

    [**自動格式化**] 對話方塊隨即顯示，可讓您選取行事曆的格式化配置。 下圖顯示[Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制項的 [**自動格式化**] 對話方塊。

    ![自動格式化對話方塊（Calendar 控制項）](creating-a-basic-web-forms-page/_static/image14.png "自動格式化對話方塊 (Calendar 控制項)")
4. 從 [**選取配置**] 清單中，選取 [**簡單**]，然後按一下 **[確定]** 。
5. 切換至**來源**視圖。

    您可以看到 **&lt;asp： Calendar&gt;** 元素。 這個元素比您稍早建立之簡單控制項的元素長很多。 它也包含子項目，例如 **&lt;WeekEndDayStyle&gt;** ，這代表各種格式設定。 下圖顯示 [**來源**視圖] 中的行事[曆](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制項。 （您在 [**原始**檔視圖] 中看到的確切標記可能與圖例稍有不同）。

    ![來源視圖中的行事曆控制項](creating-a-basic-web-forms-page/_static/image15.png "原始碼檢視中的 Calendar 控制項")

### <a name="programming-the-calendar-control"></a>行事曆控制項程式設計

在本節中，您會將行事[曆](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制項的程式設計為顯示目前選取的日期。

### <a name="to-program-the-calendar-control"></a>若要設計行事曆控制項的程式

1. 在 [**設計**視圖] 中，按兩下 [行事[曆](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)] 控制項。

    新的事件處理常式隨即建立，並顯示在名為*FirstWebPage.aspx.cs*的程式碼後置檔案中。
2. 使用下列程式碼完成[SelectionChanged](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selectionchanged.aspx)事件處理常式。

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample3.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample4.vb?highlight=2)]

    上述程式碼會將 [標籤] 控制項的文字設定為行事曆控制項的選取日期。

### <a name="running-the-page"></a>正在執行頁面

您現在可以測試行事曆。

### <a name="to-run-the-page"></a>若要執行頁面

1. 按**CTRL + F5**在瀏覽器中執行頁面。
2. 按一下行事曆中的日期。

    您所按的日期會顯示在 [[標籤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)] 控制項中。
3. 在瀏覽器中，查看頁面的原始程式碼。

    請注意， [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)控制項已轉譯成**資料表**，每日都是**td**元素。
4. 關閉瀏覽器。

## <a name="next-steps"></a>後續步驟

<a id="nextStepsToggle"></a>

本逐步解說已說明 Visual Studio 頁面設計工具的基本功能。 既然您已瞭解如何在 Visual Studio 中建立和編輯 Web form 頁面，您可能會想要探索其他功能。 例如，您可能會想要執行下列動作：

- 遵循[使用 ASP.NET 4.5 Web Forms 和 Visual Studio 2013 消費者入門](getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)的逐步教學課程系列，深入瞭解如何 ASP.NET Web form。
- 深入瞭解級聯樣式表（CSS）。 如需詳細資訊，請參閱[使用 CSS 總覽](https://msdn.microsoft.com/library/bb398931.aspx)。
