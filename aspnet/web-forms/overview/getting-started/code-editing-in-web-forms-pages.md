---
uid: web-forms/overview/getting-started/code-editing-in-web-forms-pages
title: Visual Studio 2013 中的程式碼編輯 ASP.NET Web Forms |Microsoft Docs
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: 5344b74e-b888-479a-92bc-601a33bd61a2
msc.legacyurl: /web-forms/overview/getting-started/code-editing-in-web-forms-pages
msc.type: authoredcontent
ms.openlocfilehash: 3473ad476fbbebc58e12586334b4600f57cf17ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78632745"
---
# <a name="code-editing-aspnet-web-forms-in-visual-studio-2013"></a>在 Visual Studio 2013 中以程式碼編輯 ASP.NET Web Forms

依[Erik Reitan](https://github.com/Erikre)

在許多 ASP.NET Web Form 頁面中，您可以 Visual Basic、 C#或其他語言撰寫程式碼。 Visual Studio 中的程式碼編輯器可協助您快速撰寫程式碼，同時協助您避免錯誤。 此外，編輯器也提供一些方法，讓您建立可重複使用的程式碼，以協助減少您需要執行的工作量。

本逐步解說說明 Visual Studio 程式碼編輯器的各種功能。

在這個逐步解說期間，您將了解如何：

- 修正內嵌程式碼錯誤。
- 重構和重新命名程式碼。
- 重新命名變數和物件。
- 插入程式碼片段。

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

在逐步解說的這個部分中，您將建立 Web 應用程式專案，並在其中加入新的頁面。

### <a name="to-create-a-web-application-project"></a>若要建立 Web 應用程式專案

1. 開啟 Microsoft Visual Studio。
2. 在 [檔案] 功能表上，選取 [新增專案]。  
    ![檔案 功能表](code-editing-in-web-forms-pages/_static/image1.png)

    [ **新增專案** ] 對話方塊隨即出現。
3. 選取左側的 [&gt; **Visual C#**  -&gt; **Web** templates] 群組 -**範本**。
4. 選擇中間欄的 [ASP.NET Web 應用程式] 範本。
5. 將專案命名為***BasicWebApp*** ，然後按一下 [**確定]** 按鈕。   
![[New Project] \(新增專案\) 對話方塊](code-editing-in-web-forms-pages/_static/image2.png)
6. 接下來，選取 [ **Web** form] 範本，然後按一下 [**確定]** 按鈕以建立專案。  
![[New ASP.NET Project] 對話方塊](code-editing-in-web-forms-pages/_static/image3.png)  

    Visual Studio 會建立新的專案，其中包含根據 Web form 範本預先建立的功能。

## <a name="creating-a-new-aspnet-web-forms-page"></a>建立新的 ASP.NET Web Forms 頁面

當您使用**ASP.NET Web 應用程式**專案範本建立新的 Web form 應用程式時，Visual Studio 會新增名為*default.aspx*的 ASP.NET 網頁（Web form 網頁），以及其他數個檔案和資料夾。 您可以使用*預設的 .aspx*頁面作為 Web 應用程式的首頁。 不過，在此逐步解說中，您將建立並使用新的頁面。

### <a name="to-add-a-page-to-the-web-application"></a>若要將頁面新增至 Web 應用程式

1. 在**方案總管**中，以滑鼠**按右鍵 Web**應用程式名稱（在本教學課程中，應用程式名稱是**BasicWebSite**），然後按一下 [新增 -&gt;**新專案**]。   
隨即顯示 [ 新增項目] 對話方塊。
2. 選取左側的 [ **Visual C#**  -&gt; **Web**範本] 群組。 然後，從中間清單中選取 [ **Web Form** ]，並將它命名為*FirstWebPage .aspx*。   
    ![[加入新項目] 對話方塊](code-editing-in-web-forms-pages/_static/image4.png)
3. 按一下 [**新增**]，將 Web form 頁面加入至您的專案。  
 Visual Studio 會建立新的頁面，並開啟它。
4. 接下來，將此新頁面設定為預設的啟動頁面。 在**方案總管**中，以滑鼠右鍵按一下名為*FirstWebPage*的新頁面，然後選取 [**設定為起始頁**]。 下一次執行此應用程式來測試進度時，您會在瀏覽器中自動看到這個新頁面。

## <a name="correcting-inline-coding-errors"></a>修正內嵌程式碼錯誤

Visual Studio 中的程式碼編輯器可協助您在撰寫程式碼時避免錯誤，而且如果您發生錯誤，則程式碼編輯器會協助您更正錯誤。 在本逐步解說的這個部分中，您將撰寫一行程式碼，以說明編輯器中的錯誤修正功能。

### <a name="to-correct-simple-coding-errors-in-visual-studio"></a>更正 Visual Studio 中的簡單編碼錯誤

1. 在**設計**視圖中，按兩下空白頁面，為頁面的**Load**事件建立處理常式。   
   您只會使用事件處理常式做為撰寫一些程式碼的位置。
2. 在處理常式中，輸入下列包含錯誤的行，然後按**enter**：

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample1.cs)]

   當您按下**enter**時，程式碼編輯器會在發生問題的程式碼區域下，加上綠色和紅色底線（通常會呼叫 &quot;彎曲&quot; 線）。 綠色底線表示警告。 紅色波浪線表示您必須修正的錯誤。 

    將滑鼠指標放在 `myStr` 上方，即可看到工具提示，告訴您有關警告的資訊。 此外，請將滑鼠指標停留在紅色底線上，以查看錯誤訊息。

    下圖顯示具有底線的程式碼。

    ![設計檢視中的歡迎文字](code-editing-in-web-forms-pages/_static/image5.png "設計檢視中的歡迎文字")  
   若要修正此錯誤，您必須在行尾 `;` 加上分號。 警告只會通知您尚未使用 `myStr` 變數。  

    > [!NOTE] 
    > 
    > 在 Visual Studio 中，您可以選取 **工具** -&gt;**選項** -&gt; 字型**和色彩**，來查看目前的程式碼格式設定。

## <a name="refactoring-and-renaming"></a>重構和重新命名

重構是一種軟體方法，其中牽涉到重構您的程式碼，讓您更容易瞭解和維護，同時保留其功能。 簡單的範例可能是您在事件處理常式中撰寫程式碼，以從資料庫取得資料。 當您開發頁面時，您會發現需要從數個不同的處理常式存取資料。 因此，您可以在頁面中建立資料存取方法，並在處理常式中插入方法的呼叫，以重構頁面的程式碼。

[程式碼編輯器] 包含可協助您執行各種重構工作的工具。 在此逐步解說中，您將使用兩種重構技術：重新命名變數和解壓縮方法。 其他重構選項包括封裝欄位、將區域變數升級為方法參數，以及管理方法參數。 這些重構選項的可用性取決於程式碼中的位置。

### <a name="refactoring-code"></a>重構程式碼

常見的重構案例是從另一個成員內的程式碼建立（解壓縮）方法，例如方法。 這會減少原始成員的大小，並讓解壓縮的程式碼可重複使用。

在逐步解說的這個部分中，您將撰寫一些簡單的程式碼，然後從它解壓縮方法。 支援重構C#，因此您將建立使用C#作為其程式設計語言的頁面。

### <a name="to-extract-a-method-in-a-c-page"></a>若要在C#頁面中解壓縮方法

1. 切換至**設計**視圖。
2. 在 [**工具箱**] 的 [**標準**] 索引標籤中，將 [[按鈕](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)] 控制項拖曳至頁面上。
3. 按兩下 [**按鈕**] 控制項，以建立其[click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)事件的處理常式，然後新增下列反白顯示的程式碼：

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample2.cs?highlight=3-16)]

   程式碼會建立**arraylist**物件，並使用迴圈將其載入值，然後使用另一個迴圈來顯示**ArrayList**物件的內容。
4. 按**CTRL + F5**執行頁面，然後按一下**按鈕**以確定您看到下列輸出：   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample3.html)]
5. 返回程式碼編輯器，然後在事件處理常式中選取下列幾行。   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample4.html)]
6. 以滑鼠右鍵按一下選取範圍，按一下 [**重構**]，然後選擇 [**解壓縮方法**]。 

    [**解壓縮方法**] 對話方塊隨即出現。
7. 在 [**新方法名稱**] 方塊中，輸入**DisplayArray**，然後按一下 **[確定]** 。 

    [程式碼編輯器] 會建立名為 `DisplayArray`的新方法，然後在迴圈最初的**Click**處理常式中呼叫新的方法。

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample5.cs?highlight=12)]
8. 按**CTRL + F5**再次執行頁面，然後按一下**按鈕**。

    頁面的運作方式與之前相同。 現在可以從 page 類別中的任何位置呼叫 `DisplayArray` 方法。

## <a name="renaming-variables"></a>重新命名變數

當您使用變數和物件時，您可能會想要在程式碼中參考它們之後將它們重新命名。 不過，如果您錯過重新命名其中一個參考，則重新命名變數和物件可能會導致程式碼中斷。 因此，您可以使用重構來執行重新命名。

### <a name="to-use-refactoring-to-rename-a-variable"></a>若要使用重構來重新命名變數

1. 在**Click**事件處理常式中，找出下面這一行：

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample6.cs)]
2. 以滑鼠右鍵按一下變數名稱 `alist`，選擇 [**重構**]，然後選擇 [**重新命名**]。

    [**重新命名**] 對話方塊隨即出現。
3. 在 [**新名稱**] 方塊中，輸入**ArrayList1** ，並確認已選取 [**預覽參考變更**] 核取方塊。 然後按一下 [確定]。

    [**預覽變更**] 對話方塊隨即出現，並顯示一個樹狀結構，其中包含您要重新命名之變數的所有參考。
4. 按一下 **[** 套用] 以關閉 [**預覽變更**] 對話方塊。

    明確參考您所選取之實例的變數會重新命名。 不過要注意的是，下面這一行中的變數 `alist` 不會重新命名。

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample7.cs)]

    這一行中的變數 `alist` 不會重新命名，因為它不代表您重新命名之變數 `alist` 的相同值。 `DisplayArray` 宣告中的變數 `alist` 是該方法的本機變數。 這說明使用重構來重新命名變數與直接在編輯器中執行「尋找和取代」動作不同。重構會以其所使用之變數的語義知識來重新命名變數。

## <a name="inserting-snippets"></a>插入程式碼片段

由於 Web Forms 開發人員經常需要執行許多編碼工作，程式碼編輯器會提供程式碼片段的程式庫或預先編寫的程式碼區塊。 您可以將這些程式碼片段插入至您的頁面。

您在 Visual Studio 中使用的每一種語言在插入程式碼片段的方式上有些許差異。 如需插入程式碼片段的詳細資訊，請參閱[Visual Basic IntelliSense 程式碼片段](https://msdn.microsoft.com/library/18yz4be4.aspx)。 如需在視覺效果C#中插入程式碼片段的詳細資訊，請參閱[visual C#程式碼片段](https://msdn.microsoft.com/library/z41h7fat.aspx)。

## <a name="next-steps"></a>後續步驟

本逐步解說已說明了 Visual Studio 2010 程式碼編輯器的基本功能，可用於更正程式碼中的錯誤、重構程式碼、重新命名變數，以及在程式碼中插入程式碼片段。 編輯器中的其他功能可以快速輕鬆地開發應用程式。 例如，您可能要：

- 深入瞭解 IntelliSense 的功能，例如修改 IntelliSense 選項、管理程式碼片段，以及線上搜尋程式碼片段。 如需詳細資訊，請參閱 [Using IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx)。
- 瞭解如何建立您自己的程式碼片段。 如需詳細資訊，請參閱[建立和使用 IntelliSense 程式碼片段](https://msdn.microsoft.com/library/ms165392.aspx)
- 深入瞭解 IntelliSense 程式碼片段的 Visual Basic 特定功能，例如自訂程式碼片段和疑難排解。 如需詳細資訊，請參閱[Visual Basic IntelliSense 程式碼片段](https://msdn.microsoft.com/library/18yz4be4.aspx)
- 深入瞭解 IntelliSense 的C#特定功能，例如重構和程式碼片段。 如需詳細資訊，請參閱[Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx)。
