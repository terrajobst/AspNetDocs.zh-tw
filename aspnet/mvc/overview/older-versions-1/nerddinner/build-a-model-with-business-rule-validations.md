---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: 使用商務規則驗證建立模型 |Microsoft Docs
author: microsoft
description: 步驟3顯示如何建立可用於查詢和更新 NerdDinner 應用程式資料庫的模型。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 6ebf1b71c089229ba9139ff7dc788b8978724046
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541661"
---
# <a name="build-a-model-with-business-rule-validations"></a>使用商務規則驗證建置模型

由[Microsoft](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟3，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。
> 
> 步驟3顯示如何建立可用於查詢和更新 NerdDinner 應用程式資料庫的模型。
> 
> 如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。

## <a name="nerddinner-step-3-building-the-model"></a>NerdDinner 步驟3：建立模型

在模型視圖控制器架構中，「模型」一詞指的是代表應用程式資料的物件，以及整合驗證和商務規則的對應領域邏輯。 此模型的方式很多，以 MVC 為基礎之應用程式的「核心」，我們將在稍後以根本上驅動它的行為。

ASP.NET MVC 架構支援使用任何資料存取技術，而開發人員可以從各種豐富的 .NET 資料選項中進行選擇，以執行其模型，包括： LINQ to Entities、LINQ to SQL、NHibernate、LLBLGen Pro、SubSonic、WilsonORM，或只是原始 ADO。NET Datareader 或資料集。

針對我們的 NerdDinner 應用程式，我們將使用 LINQ to SQL 來建立簡單的模型，使其相當於我們的資料庫設計，並加入一些自訂驗證邏輯和商務規則。 接著，我們將會執行存放庫類別，協助從應用程式的其餘部分來抽象化資料持續性的執行，並讓我們輕鬆地對其進行單元測試。

### <a name="linq-to-sql"></a>LINQ to SQL

LINQ to SQL 是在 .NET 3.5 中隨附的 ORM （物件關聯式對應程式）。

LINQ to SQL 提供簡單的方法，將資料庫資料表對應至我們可以撰寫程式碼的 .NET 類別。 針對我們的 NerdDinner 應用程式，我們將使用它，將資料庫內的 Dinners 和 RSVP 資料表對應至晚餐和 RSVP 類別。 Dinners 和 RSVP 資料表的資料行將會對應至晚餐和 RSVP 類別的屬性。 每個晚餐和 RSVP 物件將代表資料庫中 Dinners 或 RSVP 資料表內的個別資料列。

LINQ to SQL 可讓我們避免必須手動建立 SQL 語句，以使用資料庫資料來抓取和更新晚餐和 RSVP 物件。 相反地，我們會定義晚餐和 RSVP 類別、它們如何對應到資料庫，以及它們之間的關聯性。 然後 LINQ to SQL 會負責產生適當的 SQL 執行邏輯，以便在我們互動和使用時于執行時間使用。

我們可以使用 VB 和C#中的 LINQ 語言支援，撰寫表達查詢，從資料庫中取出晚餐和 RSVP 物件。 這會減少我們需要撰寫的資料程式碼數量，並可讓我們建立真正整潔的應用程式。

### <a name="adding-linq-to-sql-classes-to-our-project"></a>將 LINQ to SQL 類別加入至專案

首先，以滑鼠右鍵按一下專案中的 [模型] 資料夾，然後選取 [新增 **-&gt;新專案**] 功能表命令：

![](build-a-model-with-business-rule-validations/_static/image1.png)

這會顯示 [加入新專案] 對話方塊。 我們會依「資料」分類進行篩選，並選取其中的「LINQ to SQL 類別」範本：

![](build-a-model-with-business-rule-validations/_static/image2.png)

我們會將專案命名為 "NerdDinner"，然後按一下 [新增] 按鈕。 Visual Studio 會在 \Models 目錄下新增 NerdDinner，然後開啟 [LINQ to SQL 物件關聯式設計工具]：

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a>使用 LINQ to SQL 建立資料模型類別

LINQ to SQL 可以讓我們從現有的資料庫架構快速建立資料模型類別。 為此，我們會在伺服器總管中開啟 NerdDinner 資料庫，並選取我們想要在其中建立模型的資料表：

![](build-a-model-with-business-rule-validations/_static/image4.png)

然後，我們可以將資料表拖曳到 LINQ to SQL 設計工具介面上。 當我們這麼做時 LINQ to SQL 會使用資料表的架構（具有對應至資料庫資料表資料行的類別屬性），自動建立晚餐和 RSVP 類別：

![](build-a-model-with-business-rule-validations/_static/image5.png)

根據預設，LINQ to SQL 設計工具會在根據資料庫架構建立類別時，自動「pluralizes」資料表和資料行名稱。 例如：上述範例中的 "Dinners" 資料表會產生「晚餐」類別。 此類別命名可協助讓我們的模型與 .NET 命名慣例保持一致，而且通常會發現設計工具的修正很方便（尤其是在加入許多資料表時）。 不過，如果您不喜歡設計工具所產生之類別或屬性的名稱，您可以一律覆寫它，並將它變更為您想要的任何名稱。 若要這麼做，您可以在設計工具內以內嵌方式編輯實體/屬性名稱，或透過屬性方格加以修改。

根據預設，LINQ to SQL 設計工具也會檢查資料表的主鍵/外鍵關聯性，而且根據它們會在其建立的不同模型類別之間自動建立預設的「關聯性關聯」。 例如，當我們將 [Dinners] 和 [RSVP] 資料表拖曳至 LINQ to SQL 設計工具時，這兩個之間的一對多關聯性關聯是根據 RSVP 資料表具有 Dinners 資料表的外鍵的事實所推斷（這是由設計工具）：

![](build-a-model-with-business-rule-validations/_static/image6.png)

上述關聯會導致 LINQ to SQL 將強型別「晚餐」屬性新增至 RSVP 類別，讓開發人員用來存取與指定之 RSVP 相關聯的晚餐。 它也會導致晚餐類別具有 "RSVPs" 集合屬性，讓開發人員能夠抓取和更新與特定晚餐相關聯的 RSVP 物件。

當我們建立新的 RSVP 物件，並將它新增至晚餐的 RSVPs 集合時，您可以在下方查看 Visual Studio 內的 intellisense 範例。 請注意，LINQ to SQL 如何在晚餐物件上自動新增 "RSVPs" 集合：

![](build-a-model-with-business-rule-validations/_static/image7.png)

藉由將「RSVP」物件新增至晚餐的 RSVPs 集合，我們會告訴 LINQ to SQL 在資料庫中建立晚餐和「RSVP」資料列之間的外鍵關聯性：

![](build-a-model-with-business-rule-validations/_static/image8.png)

如果您不喜歡設計工具模型化或命名為數據表關聯的方式，您可以覆寫它。 只要在設計工具中按一下 [關聯] 箭號，然後透過屬性方格存取其屬性，即可重新命名、刪除或修改它。 不過，針對我們的 NerdDinner 應用程式，預設關聯規則適用于我們所建立的資料模型類別，而我們只會使用預設行為。

### <a name="nerddinnerdatacontext-class"></a>NerdDinnerDataCoNtext 類別

Visual Studio 會自動建立 .NET 類別，以代表使用 LINQ to SQL 設計工具所定義的模型和資料庫關聯性。 針對加入至方案中的每個 LINQ to SQL 設計工具檔案，也會產生 LINQ to SQL DataCoNtext 類別。 因為我們將 LINQ to SQL 類別專案命名為 "NerdDinner"，所以所建立的 DataCoNtext 類別將稱為 "NerdDinnerDataCoNtext"。 這個 NerdDinnerDataCoNtext 類別是我們將與資料庫互動的主要方式。

我們的 NerdDinnerDataCoNtext 類別會公開兩個屬性： "Dinners" 和 "RSVPs"，代表我們在資料庫中建立模型的兩個數據表。 我們可以使用C# ，針對這些屬性撰寫 LINQ 查詢，從資料庫查詢和取出晚餐和 RSVP 物件。

下列程式碼示範如何具現化 NerdDinnerDataCoNtext 物件，並對其執行 LINQ 查詢，以取得未來發生的 Dinners 序列。 Visual Studio 在撰寫 LINQ 查詢時提供完整的 intellisense，而從它傳回的物件則是強型別，也支援 intellisense：

![](build-a-model-with-business-rule-validations/_static/image9.png)

除了可讓我們查詢晚餐和 RSVP 物件之外，NerdDinnerDataCoNtext 也會自動追蹤我們後續對我們透過它取得的晚餐和 RSVP 物件所做的任何變更。 我們可以使用這種功能，輕鬆地將變更儲存回資料庫，而不需要撰寫任何明確的 SQL 更新程式碼。

例如，下列程式碼示範如何使用 LINQ 查詢來抓取資料庫中的單一晚餐物件、更新兩個晚餐屬性，然後將變更儲存回資料庫：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

上述程式碼中的 NerdDinnerDataCoNtext 物件會自動追蹤我們從中取得的晚餐物件所做的屬性變更。 當我們呼叫 "SubmitChanges （）" 方法時，它會對資料庫執行適當的 SQL "UPDATE" 語句，以保存更新後的值。

### <a name="creating-a-dinnerrepository-class"></a>建立 DinnerRepository 類別

針對小型應用程式，有時可以讓控制器直接針對 LINQ to SQL DataCoNtext 類別進行處理，並在控制器內內嵌 LINQ 查詢。 不過隨著應用程式變得更大，這種方法會變得很麻煩，而無法進行維護和測試。 它也會導致我們將相同的 LINQ 查詢複製到多個位置。

可以讓應用程式更容易維護和測試的方法之一，就是使用「存放庫」模式。 儲存機制類別可協助封裝資料查詢和持續性邏輯，並抽象化應用程式中資料持續性的執行細節。 除了讓應用程式程式碼更簡潔，使用儲存機制模式可讓您更輕鬆地在未來變更資料儲存區，而且它可以協助對應用程式進行單元測試，而不需要實際的資料庫。

針對我們的 NerdDinner 應用程式，我們將定義具有下列簽章的 DinnerRepository 類別：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

*注意：在本章稍後，我們將從這個類別解壓縮 IDinnerRepository 介面，並在我們的控制器上啟用相依性插入。從開始，我們將開始簡單明瞭，只是直接使用 DinnerRepository 類別。*

若要執行這個類別，我們要以滑鼠右鍵按一下 [模型] 資料夾，然後選擇 [**加入-&gt;新專案**] 功能表命令。 在 [新增專案] 對話方塊中，我們將選取 "Class" 範本，並將檔案命名為 "DinnerRepository.cs"：

![](build-a-model-with-business-rule-validations/_static/image10.png)

然後，我們可以使用下列程式碼來執行我們的 DinnerRepository 類別：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a>使用 DinnerRepository 類別來抓取、更新、插入及刪除

既然我們已經建立了 DinnerRepository 類別，接下來就讓我們來看幾個程式碼範例，示範我們可以用它來執行的一般工作：

#### <a name="querying-examples"></a>查詢範例

下列程式碼會使用 DinnerID 值來抓取單一晚餐：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

下列程式碼會抓取所有即將推出的 dinners 和迴圈：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a>插入和更新範例

下列程式碼示範如何新增兩個新的 dinners。 儲存機制的新增/修改不會認可到資料庫，直到在其上呼叫 "Save （）" 方法為止。 LINQ to SQL 會自動包裝資料庫交易中的所有變更–因此，所有變更都會發生，或在存放庫儲存時都不會這麼做：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

下列程式碼會抓取現有的晚餐物件，並修改其上的兩個屬性。 在我們的存放庫中呼叫 "Save （）" 方法時，會將變更認可回資料庫：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

下列程式碼會抓取晚餐，然後在其中加上一個 RSVP。 它會使用 LINQ to SQL 為我們建立的晚餐物件上的 RSVPs 集合來執行這項操作（因為資料庫中的兩個之間有主鍵/外鍵關聯性）。 在存放庫上呼叫 "Save （）" 方法時，此變更會保存回資料庫，做為新的 RSVP 資料表資料列：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a>刪除範例

下列程式碼會抓取現有的晚餐物件，然後將其標示為已刪除。 在存放庫上呼叫 "Save （）" 方法時，它會將刪除認可回資料庫：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a>整合驗證和商務規則邏輯與模型類別

整合驗證和商務規則邏輯是任何可搭配資料使用之應用程式的重要部分。

#### <a name="schema-validation"></a>結構描述驗證

當模型類別是使用 LINQ to SQL 設計工具來定義時，資料模型類別中屬性（property）的資料類型會對應至資料庫資料表的資料類型。 例如：如果 Dinners 資料表中的 "EventDate" 資料行是 "datetime"，則 LINQ to SQL 所建立的資料模型類別會是 "DateTime" 類型（內建的 .NET 資料類型）。 這表示如果您嘗試從程式碼指派整數或布林值給它，就會發生編譯錯誤，如果您嘗試在執行時間將不正確字串型別隱含轉換成它，就會自動引發錯誤。

當您使用字串時，LINQ to SQL 也會自動為您處理已植入的 SQL 值，這可在使用時協助保護您免于遭受 SQL 插入式攻擊。

#### <a name="validation-and-business-rule-logic"></a>驗證和商務規則邏輯

架構驗證非常適合做為第一個步驟，但很少會用到。 大部分的真實案例都需要能夠指定更豐富的驗證邏輯，以跨越多個屬性、執行程式碼，而且通常會知道模型的狀態（例如，它是在/updated/deleted 中建立，還是在網域特定的狀態（例如「封存」）內。 您可以使用各種不同的模式和架構來定義和套用驗證規則至模型類別，而且有數個 .NET 架構的架構，可以用來協助進行這項工作。 您幾乎可以在 ASP.NET MVC 應用程式中使用其中任何一個。

基於我們的 NerdDinner 應用程式的目的，我們將使用相當簡單且直接向前的模式，在我們的晚餐模型物件上公開 IsValid 屬性和 GetRuleViolations （）方法。 [IsValid] 屬性會根據驗證和商務規則是否有效而傳回 true 或 false。 GetRuleViolations （）方法會傳回任何規則錯誤的清單。

我們會在專案中加入「部分類別」，為晚餐模型實行 IsValid 和 GetRuleViolations （）。 部分類別可以用來將方法/屬性/事件新增至 VS 設計工具所維護的類別（例如，LINQ to SQL 設計工具所產生的晚餐類別），並協助避免使用我們的程式碼因為各家工具。 我們可以在 [\Models] 資料夾上按一下滑鼠右鍵，然後選取 [加入新專案] 功能表命令，將新的部分類別加入至專案中。 然後，我們可以選擇 [新增專案] 對話方塊中的「類別」範本，並將其命名為 Dinner.cs。

![](build-a-model-with-business-rule-validations/_static/image11.png)

按一下 [新增] 按鈕會將 Dinner.cs 檔案加入至專案，並在 IDE 中開啟它。 然後，我們可以使用下列程式碼來執行基本的規則/驗證強制架構：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

關於上述程式碼的一些注意事項：

- 晚餐類別前面會加上 "partial" 關鍵字，這表示包含在其中的程式碼將會與 LINQ to SQL 設計工具所產生/維護的類別結合，並編譯成單一類別。
- RuleViolation 類別是我們將加入至專案的協助程式類別，可讓我們提供有關規則違規的更多詳細資料。
- GetRuleViolations （）方法會使我們的驗證和商務規則進行評估（我們將在稍後加以執行）。 然後，它會傳回一系列的 RuleViolation 物件，以提供有關任何規則錯誤的詳細資料。
- 晚餐. IsValid 屬性提供便利的 helper 屬性，指出晚餐物件是否有任何作用中的 RuleViolations。 開發人員可以隨時使用晚餐物件主動檢查它（而且不會引發例外狀況）。
- OnValidate （）部分方法是 LINQ to SQL 提供的勾點，可讓我們在晚餐物件即將保存在資料庫中時收到通知。 上述的 OnValidate （）執行可確保晚餐在儲存前不會 RuleViolations。 如果它處於無效狀態，會引發例外狀況，這會導致 LINQ to SQL 中止交易。

這種方法提供了簡單的架構，讓我們可以將驗證和商務規則整合到其中。 現在，讓我們將下列規則新增至我們的 GetRuleViolations （）方法：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

我們使用的「yield return」功能C#來傳回任何 RuleViolations 的序列。 前六個規則檢查，只是在晚餐上強制字串屬性不能是 null 或空白。 最後一個規則比較有趣，而且會呼叫 PhoneValidator IsValidNumber （） helper 方法，我們可以將其新增至專案，以確認 ContactPhone 數位格式符合晚餐的國家/地區。

我們可以使用。NET 的正則運算式支援，可實現這種電話驗證支援。 以下是一個簡單的 PhoneValidator 實作為，我們可以新增至我們的專案，讓我們新增國家特定的 Regex 模式檢查：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a>處理驗證和商務邏輯違規

既然我們已新增上述驗證和商務規則程式碼，每當我們嘗試建立或更新晚餐時，就會評估並強制執行我們的驗證邏輯規則。

開發人員可以撰寫如下的程式碼，以主動判斷晚餐物件是否有效，並抓取其中的所有違規清單，而不引發任何例外狀況：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

如果我們嘗試以不正確狀態儲存晚餐，當我們在 DinnerRepository 上呼叫 Save （）方法時，就會引發例外狀況。 這是因為 LINQ to SQL 會在儲存晚餐的變更之前，自動呼叫 OnValidate （）部分方法，而且我們已將程式碼新增至 OnValidate （），以在晚餐中存在任何規則違規時引發例外狀況。 我們可以攔截這個例外狀況，並被動抓取要修正的違規清單：

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

因為我們的驗證和商務規則是在模型層內執行，而不是在 UI 層內，所以會套用到應用程式內的所有案例並加以使用。 我們稍後可以變更或新增商務規則，並讓所有與晚餐物件搭配使用的程式碼都能接受它們。

有彈性可以在一處變更商務規則，而不需要在整個應用程式和 UI 邏輯中進行這些變更，而是撰寫完善的應用程式，以及 MVC 架構有助於鼓勵的優點。

### <a name="next-step"></a>後續步驟

我們現在有一個模型，可以用來查詢和更新我們的資料庫。

現在讓我們在專案中新增一些控制器和視圖，供我們用來建立其周圍的 HTML UI 體驗。

> [!div class="step-by-step"]
> [上一頁](create-a-database.md)
> [下一頁](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
