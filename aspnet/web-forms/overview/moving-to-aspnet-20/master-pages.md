---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: 主版頁面 |Microsoft Docs
author: microsoft
description: 成功網站的其中一個重要元件是一致的外觀與風格。 在 ASP.NET 1.x 中，開發人員使用使用者控制項來複寫一般頁面 elem 。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: 36f2caf7c2c9bcafd22c8f6681c1d6b19fe5078a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78567330"
---
# <a name="master-pages"></a>主版頁面

由[Microsoft](https://github.com/microsoft)

> 成功網站的其中一個重要元件是一致的外觀與風格。 在 ASP.NET 1.x 中，開發人員使用使用者控制項來複寫 Web 應用程式中的一般頁面元素。 雖然這當然是可行的解決方案，但使用使用者控制項的確有一些缺點。 例如，使用者控制項的位置變更需要跨網站變更多個頁面。 使用者控制項在插入頁面之後，也不會在設計檢視中呈現。

成功網站的其中一個重要元件是一致的外觀與風格。 在 ASP.NET 1.x 中，開發人員使用使用者控制項來複寫 Web 應用程式中的一般頁面元素。 雖然這當然是可行的解決方案，但使用使用者控制項的確有一些缺點。 例如，使用者控制項的位置變更需要跨網站變更多個頁面。 使用者控制項在插入頁面之後，也不會在設計檢視中呈現。

ASP.NET 2.0 引進主版頁面做為維護一致外觀與風格的方式，而且您很快就會看到，主版頁面代表使用者控制項方法的大幅改善。

## <a name="why-master-pages"></a>為何選擇主版頁面？

您可能想知道為什麼 ASP.NET 2.0 中需要主版頁面。 畢竟，網站開發人員已經使用 ASP.NET 1.x 中的使用者控制項，在頁面之間共用內容區域。 實際上，有幾個原因是使用者控制項是較不理想的方案，無法建立一般版面配置。

使用者控制項實際上不會定義頁面配置。 相反地，它們會定義部分頁面的版面配置和功能。 這兩者的差異很重要，因為它可讓使用者控制解決方案的管理工作更加棘手。 例如，當您想要變更使用者控制項在頁面上的位置時，您必須編輯顯示使用者控制項的實際頁面。 如果您只有幾頁，但在大型網站中，它很快就會變成網站管理的麻煩！

使用使用者控制項來定義一般版面配置的另一個缺點是根 ASP.NET 本身的架構。 如果使用者控制項的任何公開成員已變更，您就需要重新編譯所有使用該使用者控制項的頁面。 然後，ASP.NET 會在第一次存取您的頁面時，重新將它們重設為 JIT。 這同樣地，會產生一個無法調整的架構，以及更大的網站的網站管理問題。

ASP.NET 2.0 中的主版頁面會妥善解決這兩個問題（及其他許多）。

## <a name="how-master-pages-work"></a>主版頁面的工作方式

主版頁面類似于其他頁面的範本。 應該在主版頁面中加入其他頁面（也就是功能表、框線等）之間共用的頁面元素。 將新頁面新增至網站時，您可以將它們與主版頁面產生關聯。 與主版頁面相關聯的頁面稱為**內容頁面**。 根據預設，內容頁面會從主版頁面上取得外觀。 不過，當您建立主版頁面時，您可以定義內容頁面可以用自己的內容取代的部分頁面。 這些部分是使用 ASP.NET 2.0 中引進的新控制項所定義;**ContentPlaceHolder**控制項。

主版頁面可以包含任意數目的 ContentPlaceHolder 控制項（或完全無）。在 [內容] 頁面上，ContentPlaceHolder 控制項的內容會出現在**內容**控制項的內部，也就是 ASP.NET 2.0 中的另一個新控制項。 根據預設，內容頁內容控制項是空的，因此您可以提供自己的內容。 如果您想要使用內容控制項內主版頁面中的內容，您可以在本課程模組稍後看到。 內容控制項透過內容控制項的 ContentPlaceHolderID 屬性對應至 ContentPlaceHolder 控制項。 下列程式碼會將內容控制項對應至主版頁面上名為 mainBody 的 ContentPlaceHolder 控制項。

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> 您通常會聽到人們將主版頁面描述為其他頁面的基類。 其實不是真的。 主版頁面和內容頁面之間的關聯性不是繼承的其中一個。

[**圖 1** ] 顯示主版頁面和相關聯的內容頁面，出現在 Visual Studio 2005 中。 您可以在 [內容] 頁面中的主版頁面和對應的內容控制項中看到 [ContentPlaceHolder] 控制項。 請注意，在 [內容] 頁面中會顯示 ContentPlaceHolder 外的主版頁面內容，但會呈現灰色。 [內容] 頁面只可會 ContentPlaceHolder 內的內容。 來自主版頁面的所有其他內容都是不可變的。

![主版頁面和其相關聯的內容頁面](master-pages/_static/image1.jpg)

**圖 1**：主版頁面和其相關聯的內容頁面

## <a name="creating-a-master-page"></a>建立主版頁面

若要建立新的主版頁面：

1. 開啟 Visual Studio 2005，並建立新的網站。
2. 按一下 [檔案]、[新增]、[檔案]。
3. 從 [新增專案] 對話方塊中選擇 [主要檔案]，如 [**圖 2**] 所示。
4. 按一下 [加入]。

![建立新的主版頁面](master-pages/_static/image2.jpg)

**圖 2**：建立新的主版頁面

請注意，主版頁面的副檔名為 *. master*。 這是主版頁面與一般頁面不同的其中一種方式。 另一個主要差異在於，在替代 @Page 指示詞的情況下，主版頁面會包含 @Master 的指示詞。 切換至您剛才建立之主版頁面的原始檔視圖，並查看程式碼。

新的主版頁面預設會有一個 ContentPlaceHolder 控制項。 在大部分的情況下，先建立一般頁面專案，然後插入需要自訂內容的 ContentPlaceHolder 控制項，會比較合理。 在這些情況下，開發人員會想要刪除預設的 ContentPlaceHolder 控制項，並在開發網頁時插入新的控制項。 雖然 ContentPlaceHolder 控制項會顯示調整大小控點，但不能調整大小。 ContentPlaceHolder 控制項會根據其所包含的內容自動進行調整，但有一個例外狀況;如果您將 ContentPlaceHolder 控制項放在區塊專案（例如資料表單元格）內，它會根據專案的大小來調整大小。

## <a name="lab-1-working-with-master-pages"></a>實驗室1使用主版頁面

在此實驗室中，您將建立新的主版頁面，並定義三個 ContentPlaceHolder 控制項。 接著，您會建立新的內容頁面，並從至少一個 ContentPlaceHolder 控制項中取代內容。

1. 建立主版頁面並插入 ContentPlaceHolder 控制項。 

    1. 如上面所述，建立新的主版頁面。
    2. 刪除預設的 ContentPlaceHolder 控制項。
    3. 按一下控制項的陰影上方框線來選取 [ContentPlaceHolder] 控制項，然後按下鍵盤上的 DEL 鍵將其刪除。
    4. 使用*標頭和側邊*範本插入新的資料表，如 [圖 3] 所示。 將 [寬度] 和 [高度] 變更為 [90%]，以便在設計工具中顯示整個資料表。

![](master-pages/_static/image3.jpg)

**圖 3**

1. 將游標放入資料表的每個資料格，並將*valign*屬性設定為*top*。
2. 從 [工具箱] 中，將 ContentPlaceHolder 控制項插入資料表的頂端資料格（標頭儲存格）。
3. 當您插入此 ContentPlaceHolder 控制項時，您會注意到資料列高度會佔用幾乎整個頁面，如 [圖 4] 所示。 此時請不要擔心。

![空白空間與 ContentPlaceHolder 位於相同的儲存格](master-pages/_static/image1.gif)

**圖 4**：空的空間與 ContentPlaceHolder 位於相同的儲存格

1. 將 ContentPlaceHolder 控制項放在其他兩個數據格中。 插入其他 ContentPlaceHolder 控制項之後，資料表單元格的大小應該就如同您所預期。 頁面現在看起來應該像 [**圖 5**] 中所示的頁面。

![具有所有 ContentPlaceHolder 控制項的主要複本。 請注意，標頭儲存格的儲存格高度現在應該是](master-pages/_static/image2.gif)

**圖 5**：具有所有 ContentPlaceHolder 控制項的主要複本。 請注意，標頭儲存格的儲存格高度現在應該是

1. 將您選擇的一些文字輸入至三個 ContentPlaceHolder 控制項中的每一個。
2. 將主版頁面儲存為 exercise1。
3. 建立新的 Web 表單，並將它與 exercise1 主版頁面建立關聯。
4. 選取 [檔案]、[新增]、[檔案于 Visual Studio 2005]。
5. 在 [加入新專案] 對話方塊中選取 [ **Web 表單**]。
6. 請確定已核取 [選取主版頁面] 核取方塊，如 [圖 6] 所示。

![加入新的內容頁面](master-pages/_static/image3.gif)

**圖 6**：新增內容頁面

1. 按一下 [加入]。
2. 在 [選取主版頁面] 對話方塊中選取 [exercise1]，如 [圖 7] 所示。
3. 按一下 [確定] 以新增 [內容] 頁面。

新增內容 頁面會出現在 Visual Studio 中，其中包含主版頁面上每個 ContentPlaceHolder 控制項的一個內容控制項。 根據預設，內容控制項是空的，因此您可以新增自己的內容。 如果您想要讓他們使用主版頁面上 ContentPlaceHolder 控制項的內容，只要按一下智慧標籤符號（控制項右上角的小型黑色箭號），然後選擇 [預設] 從智慧標籤中的 [*主目錄內容*]，如 [**圖 8**] 所示。 當您這麼做時，功能表項目會變更以*建立自訂內容*。 按一下該點就會從主版頁面移除內容，讓您定義該特定內容控制項的自訂內容。

![將內容控制項設為預設為主版頁面內容](master-pages/_static/image4.gif)

**圖 7**：將內容控制項設定為預設為主版頁面內容

## <a name="connecting-master-page-and-content-pages"></a>連接主版頁面和內容頁面

主版頁面與內容頁面之間的關聯可以透過下列四種不同方式來設定：

- @Page 指示詞的<strong>MasterPageFile</strong>屬性
- 在程式碼中設定**MasterPageFile**屬性。
- 應用程式佈建檔中的 **&lt;頁面&gt;** 元素（應用程式根資料夾中的 web.config）
- 子資料夾設定檔中的 **&lt;頁面&gt;** 元素（子資料夾中的 web.config）

## <a name="masterpagefile-attribute"></a>MasterPageFile 屬性

MasterPageFile 屬性可讓您輕鬆地將主版頁面套用至特定的 ASP.NET 網頁。 當您核取 [**選取主版頁面**] 核取方塊時，它也是用來套用主版頁面的方法，就像在練習1中所做的一樣。

## <a name="setting-pagemasterpagefile-in-code"></a>在程式碼中設定頁面 MasterPageFile

藉由在程式碼中設定 MasterPageFile 屬性，您可以在執行時間將特定的主版頁面套用至內容。 當您可能需要根據使用者角色或其他準則來套用特定的主版頁面時，這會很有用。 MasterPageFile 屬性必須在 PreInit 方法中設定。 如果它是在 PreInit 方法之後設定，則會擲回 InvalidOperationException。 設定此屬性的頁面也必須有內容控制項，做為頁面的最上層控制項。 否則，當設定 MasterPageFile 屬性時，將會擲回 HttpException。

## <a name="using-the-ltpagesgt-element"></a>使用 &lt;頁面&gt; 元素

您可以設定網頁的主版頁面，方法是在 web.config 檔案的 &lt;頁面&gt; 元素中，設定 masterPageFile 屬性。 使用此方法時，請記住，應用程式結構中較低的 web.config 檔案可以覆寫此設定。 在 @Page 指示詞中設定的任何 MasterPageFile 屬性也會覆寫此設定。 使用 &lt;頁面&gt; 專案，可讓您輕鬆地建立*主要*主版頁面，視需要在特定資料夾或檔案中加以覆寫。

## <a name="properties-in-master-pages"></a>主版頁面中的屬性

主版頁面只要在主版頁面中公開這些屬性，就可以公開屬性。 例如，下列程式碼會定義名為 SomeProperty 的屬性：

[!code-csharp[Main](master-pages/samples/sample2.cs)]

若要從 [內容] 頁面存取 [SomeProperty] 屬性，您必須使用 Master 屬性，如下所示：

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a>嵌套主版頁面

主版頁面是確保跨大型 Web 應用程式的常見外觀與風格的絕佳解決方案。 不過，大型網站的某些部分共用通用介面並不常見，而其他部分則共用不同的介面。 若要解決此需求，有多個主版頁面是完美的解決方案。 不過，仍然無法解決大型應用程式可能會有某些元件（例如功能表）在所有頁面和其他只在網站特定區段共用的元件之間共用的事實。 針對這種情況，嵌套主版頁面會適當地填滿需求。 如您所見，一般主版頁面包含主版頁面和內容頁面。 在嵌套主版頁面的情況下，有兩個主版頁面;父主機和子主機。 子主版頁面也是 [內容] 頁面，而其主要頁面是 [父系] 主版頁面。

以下是一般主版頁面的程式碼：

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

在嵌套的主要案例中，這會是父主機。 另一個主版頁面會使用此頁面作為其主版頁面，而該程式碼看起來會像這樣：

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

請注意，在此案例中，子主要複本也是父主機的內容頁面。 所有子主機的內容都會出現在內容控制項的內部，而該控制項會從父系的 ContentPlaceHolder 控制項取得其內容。

> [!NOTE]
> 設計工具支援不適用於嵌套主版頁面。 當您使用「嵌套式主機」進行開發時，您必須使用「來源視圖」。

這段影片會示範如何使用嵌套主版頁面的逐步解說。

![](master-pages/_static/image1.png)

[開啟全螢幕影片](master-pages/_static/nested1.wmv)

![選取主版頁面](master-pages/_static/image4.jpg)

**圖 8**：選取主版頁面
