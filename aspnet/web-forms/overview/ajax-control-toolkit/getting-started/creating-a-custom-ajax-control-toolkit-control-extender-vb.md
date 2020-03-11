---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
title: 建立自訂 AJAX 控制項工具組控制項擴充項（VB） |Microsoft Docs
author: microsoft
description: 自訂延伸可讓您自訂和擴充 ASP.NET 控制項的功能，而不需要建立新的類別。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 18b29834-c991-4e0c-b533-44d358fbfc9c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: 0849fa6c13679e0cd01bb20a4067a097acbce298
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578159"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-vb"></a>建立自訂的 AJAX Control Toolkit 控制項擴充項 (VB)

由[Microsoft](https://github.com/microsoft)

> 自訂延伸可讓您自訂和擴充 ASP.NET 控制項的功能，而不需要建立新的類別。

在本教學課程中，您將瞭解如何建立自訂的 AJAX 控制項工具組控制項擴充項。 我們建立了一個簡單但實用的新擴充項，當您在 TextBox 中輸入文字時，會將按鈕的狀態從停用變更為啟用。 閱讀本教學課程之後，您將能夠使用自己的控制項擴充項來延伸 ASP.NET AJAX 工具組。

您可以使用 Visual Studio 或 Visual Web Developer 來建立自訂控制項擴充項（請確定您擁有最新版本的 Visual Web Developer）。

## <a name="overview-of-the-disabledbutton-extender"></a>DisabledButton 擴充項的總覽

我們的新控制項擴充項名為 DisabledButton 擴充項。 這個擴充項會有三個屬性：

- TargetControlID-控制項擴充的文字方塊。
- TargetButtonIID-已停用或啟用的按鈕。
- DisabledText-一開始顯示在按鈕中的文字。 當您開始輸入時，按鈕會顯示 [按鈕文字] 屬性的值。

您會將 DisabledButton 擴充項與 TextBox 和 Button 控制項連結。 在您輸入任何文字之前，按鈕會停用，而且 TextBox 和按鈕看起來像這樣：

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image1.png)

（[按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png)）

當您開始輸入文字之後，按鈕就會啟用，而且 TextBox 和按鈕看起來像這樣：

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image4.png)

（[按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png)）

若要建立控制項擴充項，我們需要建立下列三個檔案：

- DisabledButtonExtender：此檔案是伺服器端控制項類別，會管理建立擴充項，並可讓您在設計階段設定屬性。 它也會定義可在您的擴充項上設定的屬性。 這些屬性可以透過程式碼和在設計階段存取，並符合 DisableButtonBehavior 中定義的屬性。
- DisabledButtonBehavior--此檔案是您將新增所有用戶端腳本邏輯的位置。
- DisabledButtonDesigner .vb-這個類別會啟用設計階段功能。 如果您想要讓控制項擴充項與 Visual Studio/Visual Web Developer Designer 正常搭配運作，您需要此類別。

因此，控制項擴充項包含伺服器端控制項、用戶端行為和伺服器端設計工具類別。 在下列各節中，您將瞭解如何建立這三個檔案。

## <a name="creating-the-custom-extender-website-and-project"></a>建立自訂擴充項網站和專案

第一個步驟是在 Visual Studio/Visual Web Developer 中建立類別庫專案和網站。 我們會在類別庫專案中建立自訂擴充項，並在網站中測試自訂擴充項。

讓我們從網站開始。 請遵循下列步驟來建立網站：

1. 選取功能表選項 [檔案] **、[新增網站**]。
2. 選取 [ **ASP.NET 網站**] 範本。
3. 將新網站命名為*Website1*。
4. 按一下 [確定] 按鈕。

接下來，我們必須建立類別庫專案，其中將包含控制項擴充項的程式碼：

1. 選取功能表選項 [檔案] **、[加入]、[新增專案**]。
2. 選取 [**類別庫**] 範本。
3. 以名稱**CustomExtenders**命名新的類別庫。
4. 按一下 [確定] 按鈕。

完成這些步驟之後，您的方案總管視窗看起來應該像 [圖 1] 所示。

[使用網站和類別庫專案 ![解決方案](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)

**圖 01**：使用網站和類別庫專案的解決方案（[按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png)）

接下來，您必須將所有必要的元件參考加入至類別庫專案：

1. 以滑鼠右鍵按一下 CustomExtenders 專案，然後選取 [**新增參考**] 功能表選項。
2. 選取 [.NET] 索引標籤。
3. 加入下列組件的參考：

    1. System.Web.dll
    2. System.Web.Extensions.dll
    3. System.Design.dll
    4. System.web. 副檔名 .dll
4. 選取 [流覽] 索引標籤。
5. 加入 AjaxControlToolkit 元件的參考。 這個元件位於您下載 AJAX 控制項工具組的資料夾中。

您可以用滑鼠右鍵按一下您的專案，選取 [屬性]，然後按一下 [參考] 索引標籤，來確認您已加入所有正確的參考（請參閱 [圖 2]）。

[具有必要參考的 ![參考資料夾](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)

**圖 02**：具有必要參考的參考資料夾（[按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png)）

## <a name="creating-the-custom-control-extender"></a>建立自訂控制項擴充項

既然我們已經有了類別庫，我們就可以開始建立擴充性控制項。 讓我們從自訂擴充項控制項類別的簡略骨骼開始（請參閱 [清單 1]）。

**清單 1-MyCustomExtender .vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample1.vb)]

在 [清單 1] 中，您會注意到控制項擴充項類別的幾件事。 首先，請注意類別是繼承自基底 ExtenderControlBase 類別。 所有的 AJAX 控制項工具組擴充項控制項都是衍生自這個基類。 例如，基類包含 TargetID 屬性，這是每個控制項擴充項的必要屬性。

接下來，請注意類別包含下列兩個與用戶端腳本相關的屬性：

- WebResource-導致檔案以內嵌資源的形式包含在元件中。
- ClientScriptResource-導致從元件抓取腳本資源。

WebResource 屬性是用來在編譯自訂擴充項時，將 MyControlBehavior JavaScript 檔案內嵌至元件中。 ClientScriptResource 屬性是用來在網頁中使用自訂擴充項時，從元件中取出 MyControlBehavior 腳本。

為了讓 WebResource 和 ClientScriptResource 屬性能夠正常執行，您必須將 JavaScript 檔案編譯為內嵌資源。 在 [方案總管] 視窗中選取檔案，開啟屬性工作表，並將 [*內嵌的資源*] 值指派給 [**組建動作**] 屬性。

請注意，控制項擴充項也包含 TargetControlType 屬性。 這個屬性是用來指定控制項擴充項所延伸的控制項類型。 在 [清單 1] 的案例中，控制項擴充項是用來延伸文字方塊。

最後，請注意，自訂擴充項包含名為 MyProperty 的屬性。 屬性會以 ExtenderControlProperty 屬性標記。 GetPropertyValue （）和 SetPropertyValue （）方法是用來將伺服器端控制擴充項的屬性值傳遞至用戶端行為。

讓我們繼續執行 DisabledButton 擴充項的程式碼。 此擴充項的程式碼可在 [清單 2] 中找到。

**清單 2-DisabledButtonExtender .vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample2.vb)]

[清單 2] 中的 DisabledButton 擴充項有兩個名為 TargetButtonID 和 DisabledText 的屬性。 套用至 TargetButtonID 屬性的 IDReferenceProperty 可防止您將 Button 控制項識別碼以外的任何專案指派給這個屬性。

WebResource 和 ClientScriptResource 屬性會將位於名為 DisabledButtonBehavior 之檔案中的用戶端行為與此擴充項產生關聯。 我們將在下一節討論此 JavaScript 檔案。

## <a name="creating-the-custom-extender-behavior"></a>建立自訂擴充項行為

控制項擴充項的用戶端元件稱為「行為」（behavior）。 停用和啟用按鈕的實際邏輯包含在 DisabledButton 行為中。 行為的 JavaScript 程式碼包含在 [清單 3] 中。

**清單 3-DisabledButton .js**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample3.js)]

[清單 3] 中的 JavaScript 檔案包含名為 DisabledButtonBehavior 的用戶端類別。 這個類別（如其伺服器端對應項）包含兩個名為 TargetButtonID 和 DisabledText 的屬性，您可以使用 get\_TargetButtonID/set\_TargetButtonID，並取得\_DisabledText/set\_DisabledText 來進行存取。

Initialize （）方法會將 keyup 事件處理常式與行為的目標元素產生關聯。 每次您在與此行為相關聯的文字方塊中輸入字母時，就會執行 keyup 處理常式。 Keyup 處理常式會根據與行為關聯的 TextBox 是否包含任何文字，來啟用或停用按鈕。

請記住，您必須將清單3中的 JavaScript 檔案編譯為內嵌資源。 在 [方案總管] 視窗中選取檔案，開啟屬性工作表，並將 [*內嵌的資源*] 值指派給 [**組建動作**] 屬性（請參閱 [圖 3]）。 Visual Studio 和 Visual Web Developer 都提供此選項。

[![新增 JavaScript 檔案做為內嵌資源](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)

**圖 03**：將 JavaScript 檔案新增為內嵌資源（[按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png)）

## <a name="creating-the-custom-extender-designer"></a>建立自訂的擴充項設計工具

有一個我們需要建立的最後一個類別，才能完成我們的擴充項。 我們需要在 [清單 4] 中建立設計工具類別。 必須要有這個類別，才能讓擴充項與 Visual Studio/Visual Web Developer Designer 正確地運作。

**清單 4-DisabledButtonDesigner .vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample4.vb)]

您可以使用設計工具屬性，將 [清單 4] 中的設計工具與 DisabledButton 擴充項產生關聯。您需要將設計工具屬性套用至 DisabledButtonExtender 類別，如下所示：

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample5.vb)]

## <a name="using-the-custom-extender"></a>使用自訂擴充項

既然我們已完成建立 DisabledButton 控制項擴充項，現在可以在我們的 ASP.NET 網站中使用它。 首先，我們需要將自訂擴充項加入 [工具箱] 中。 請依照下列步驟：

1. 按兩下 [方案總管] 視窗中的頁面，即可開啟 ASP.NET 網頁。
2. 以滑鼠右鍵按一下 [工具箱]，然後選取功能表選項 **[選擇專案**]。
3. 在 [選擇工具箱專案] 對話方塊中，流覽至 [CustomExtenders] 元件。
4. 按一下 [**確定**] 按鈕以關閉對話方塊。

完成這些步驟之後，[DisabledButton] 控制項擴充項應該會出現在 [工具箱] 中（請參閱 [圖 4]）。

[在 [工具箱] 中 ![DisabledButton](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)

**圖 04**： [工具箱] 中的 DisabledButton （[按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png)）

接下來，我們需要建立新的 ASP.NET 網頁。 請依照下列步驟：

1. 建立名為 ShowDisabledButton 的新 ASP.NET 網頁。
2. 將 ScriptManager 拖曳至頁面上。
3. 將 TextBox 控制項拖曳至頁面上。
4. 將 [按鈕] 控制項拖曳至頁面上。
5. 在屬性視窗中，將 [按鈕識別碼] 屬性變更為 [值<em>btnSave</em> ]，並將 [Text] 屬性變更為 [*儲存\** ] 值。

我們建立了具有標準 ASP.NET TextBox 和 Button 控制項的頁面。

接下來，我們需要使用 DisabledButton 擴充項來延伸 TextBox 控制項：

1. 選取 [**加入**擴充項工作] 選項，以開啟 [擴充性檢查程式] 對話方塊（請參閱 [圖 5]）。 請注意，此對話方塊包含我們的自訂 DisabledButton 擴充項。
2. 選取 DisabledButton 擴充項，然後按一下 [**確定]** 按鈕。

[![[擴充項嚮導] 對話方塊](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)

**圖 05**： [擴充項嚮導] 對話方塊（[按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png)）

最後，我們可以設定 DisabledButton 擴充項的屬性。 藉由修改 TextBox 控制項的屬性，您可以修改 DisabledButton 擴充項的屬性：

1. 在設計工具中選取文字方塊。
2. 在 屬性視窗中，展開 擴充項 節點（請參閱 圖 6）。
3. 將*儲存*的值指派給 DisabledText 屬性，並將*btnSave*值指定為 TargetButtonID 屬性。

[![設定擴充項屬性](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)

**圖 06**：設定擴充項屬性（[按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png)）

當您執行頁面（藉由按 F5）時，按鈕控制項一開始就會停用。 一旦您開始在文字方塊中輸入文字，就會啟用按鈕控制項（請參閱 [圖 7]）。

[![DisabledButton 擴充項的作用中](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)

**圖 07**：作用中的 DisabledButton 擴充項（[按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png)）

## <a name="summary"></a>總結

本教學課程的目的是要說明如何使用自訂的擴充項控制項來延伸 AJAX 控制項工具組。 在本教學課程中，我們建立了一個簡單的 DisabledButton 控制項擴充項。 我們藉由建立 DisabledButtonExtender 類別、DisabledButtonBehavior JavaScript 行為和 DisabledButtonDesigner 類別來實作為擴充項。 當您建立自訂控制項擴充項時，您會遵循一組類似的步驟。

> [!div class="step-by-step"]
> [上一篇](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
