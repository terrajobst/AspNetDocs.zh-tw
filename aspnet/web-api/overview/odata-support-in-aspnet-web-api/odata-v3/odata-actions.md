---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
title: 在 ASP.NET Web API 2 中支援 OData 動作 |Microsoft Docs
author: MikeWasson
description: 在 OData 中，動作是一種新增伺服器端行為的方法，不容易定義為實體上的 CRUD 作業。 動作的某些用途包括： [執行]
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 2d7b3aa2-aa47-4e6e-b0ce-3d65a1c6fe02
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
msc.type: authoredcontent
ms.openlocfilehash: ae8b23f0868f992cb2bbbf14ee3f7ac848501515
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600356"
---
# <a name="supporting-odata-actions-in-aspnet-web-api-2"></a>在 ASP.NET Web API 2 中支援 OData 動作

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> 在 OData 中，*動作*是一種新增伺服器端行為的方法，不容易定義為實體上的 CRUD 作業。 某些動作的用途包括：
> 
> - 執行複雜交易。
> - 一次處理數個實體。
> - 僅允許更新實體的特定屬性。
> - 將資訊傳送至未定義于實體中的伺服器。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - Web API 2
> - OData 第3版
> - Entity Framework 6

## <a name="example-rating-a-product"></a>範例：評等產品

在此範例中，我們想要讓使用者對產品進行評分，然後公開每個產品的平均評等。 在資料庫上，我們將會儲存評等的清單，並將其加入產品中。

以下是我們可能用來代表 Entity Framework 中的評等的模型：

[!code-csharp[Main](odata-actions/samples/sample1.cs)]

但是，我們不希望用戶端將 `ProductRating` 物件張貼到「評等」集合。 就直覺而言，評等與 Products 集合相關聯，而且用戶端應該只需要公佈評等值。

因此，我們不會使用一般 CRUD 作業，而是定義用戶端可以在產品上叫用的動作。 在 OData 術語中，*動作會系*結至 Product 實體。

>動作在伺服器上有副作用。 基於這個理由，系統會使用 HTTP POST 要求來叫用它們。 動作可以有參數和傳回型別，如服務中繼資料中所述。 用戶端會在要求主體中傳送參數，而伺服器會在回應本文中傳送傳回值。 為了叫用「速率產品」動作，用戶端會將 POST 傳送至 URI，如下所示：

[!code-console[Main](odata-actions/samples/sample2.cmd)]

POST 要求中的資料只是產品分級：

[!code-console[Main](odata-actions/samples/sample3.cmd)]

## <a name="declare-the-action-in-the-entity-data-model"></a>在實體資料模型中宣告動作

在您的 Web API 設定中，將動作新增至 entity data model （EDM）：

[!code-csharp[Main](odata-actions/samples/sample4.cs)]

此程式碼會將 "RateProduct" 定義為可在產品實體上執行的動作。 它也會宣告動作接受名為「評等」的**int**參數，並傳回**int**值。

## <a name="add-the-action-to-the-controller"></a>將動作新增至控制器

"RateProduct" 動作會系結至 Product 實體。 若要執行此動作，請將名為 `RateProduct` 的方法新增至 Products controller：

[!code-csharp[Main](odata-actions/samples/sample5.cs)]

請注意，方法名稱與 EDM 中的動作名稱相符。 此方法有兩個參數：

- *金鑰*：要分級之產品的金鑰。
- *parameters*：動作參數值的字典。

如果您使用預設路由慣例，則金鑰參數必須命名為 "key"。 也請務必包含 **[FromOdataUri]** 屬性，如下所示。 這個屬性會告知 Web API 在從要求 URI 剖析金鑰時，使用 OData 語法規則。

使用*parameters*字典來取得動作參數：

[!code-csharp[Main](odata-actions/samples/sample6.cs)]

如果用戶端以正確的格式傳送動作參數， **ModelState**的值就是 true。 在這種情況下，您可以使用**ODataActionParameters**字典來取得參數值。 在此範例中，`RateProduct` 動作會接受名為「評等」的單一參數。

## <a name="action-metadata"></a>動作中繼資料

若要查看服務中繼資料，請將 GET 要求傳送至/odata/$metadata。 以下是宣告 `RateProduct` 動作的中繼資料部分：

[!code-xml[Main](odata-actions/samples/sample7.xml)]

**FunctionImport**元素會宣告動作。 大部分的欄位都是一目了然的，但有兩個值得注意的：

- **Isbindable 時**表示可在目標實體上叫用此動作，至少必須有一些時間。
- **IsAlwaysBindable**表示動作一律可在目標實體上叫用。

差別在於某些動作一律可供用戶端使用，但其他動作則可能取決於實體的狀態。 例如，假設您定義了「購買」動作。 您只能購買庫存中的專案。 如果專案已脫銷，用戶端就無法叫用該動作。

當您定義 EDM 時，**動作**方法會建立永遠可系結的動作：

[!code-csharp[Main](odata-actions/samples/sample8.cs?highlight=1)]

我將在本主題稍後討論不一定可系結的動作（也稱為*暫時性*動作）。

## <a name="invoking-the-action"></a>叫用動作

現在讓我們來看看用戶端叫用此動作的方式。 假設用戶端想要為識別碼為4的產品提供2的評等。 以下是範例要求訊息，其中使用 JSON 格式的要求本文：

[!code-console[Main](odata-actions/samples/sample9.cmd)]

以下是回應訊息：

[!code-console[Main](odata-actions/samples/sample10.cmd)]

## <a name="binding-an-action-to-an-entity-set"></a>將動作系結至實體集

在上述範例中，動作會系結至單一實體：用戶端會對單一產品進行速率。 您也可以將動作系結至實體的集合。 只要進行下列變更：

在 EDM 中，將動作加入至實體的**集合**屬性。

[!code-csharp[Main](odata-actions/samples/sample11.cs?highlight=1)]

在控制器方法中，省略*key*參數。

[!code-csharp[Main](odata-actions/samples/sample12.cs)]

現在，用戶端會叫用 Products 實體集上的動作：

[!code-console[Main](odata-actions/samples/sample13.cmd)]

## <a name="actions-with-collection-parameters"></a>具有集合參數的動作

動作可以具有接受值集合的參數。 在 EDM 中，使用**CollectionParameter&lt;t&gt;** 來宣告參數。

[!code-csharp[Main](odata-actions/samples/sample14.cs)]

這會宣告名為「評等」的參數，其接受**int**值的集合。 在控制器方法中，您仍然會從**ODataActionParameters**物件取得參數值，但現在的值是**ICollection&lt;int&gt;** 值：

[!code-csharp[Main](odata-actions/samples/sample15.cs)]

## <a name="transient-actions"></a>暫時性動作

在 "RateProduct" 範例中，使用者一律可以對產品進行評分，因此此動作一律可供使用。 但某些動作取決於實體的狀態。 例如，在影片出租服務中，「結帳」動作不一定可供使用。 （這取決於該影片的複本是否可供使用。）這種類型的動作稱為「*暫時性*動作」。

在服務中繼資料中，暫時性動作的**IsAlwaysBindable**等於 false。 這實際上是預設值，因此中繼資料看起來會像這樣：

[!code-xml[Main](odata-actions/samples/sample16.xml)]

這就是為什麼這是很重要的原因：如果某個動作是暫時性的，伺服器就必須在有動作可用時告訴用戶端。 其方式是在實體中包含動作的連結。 以下是 Movie 實體的範例：

[!code-console[Main](odata-actions/samples/sample17.cmd)]

"#CheckOut" 屬性包含 [簽出] 動作的連結。 如果動作無法使用，伺服器就會省略連結。

若要在 EDM 中宣告暫時性動作，請呼叫**TransientAction**方法：

[!code-csharp[Main](odata-actions/samples/sample18.cs)]

此外，您還必須提供函式，以傳回指定實體的動作連結。 藉由呼叫**HasActionLink**來設定此函式。 您可以撰寫函式做為 lambda 運算式：

[!code-csharp[Main](odata-actions/samples/sample19.cs)]

如果動作可供使用，lambda 運算式會傳回動作的連結。 OData 序列化程式會在序列化實體時包含此連結。 當動作無法使用時，函數會傳回 `null`。

## <a name="additional-resources"></a>其他資源

[OData 動作範例](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v3/ODataActionsSample/)
