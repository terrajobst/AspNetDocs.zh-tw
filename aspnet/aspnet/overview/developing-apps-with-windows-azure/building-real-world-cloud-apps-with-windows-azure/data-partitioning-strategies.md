---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
title: 資料分割策略（使用 Azure 建立真實世界的雲端應用程式） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會說明13個模式和實務，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 513837a7-cfea-4568-a4e9-1f5901245d24
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
msc.type: authoredcontent
ms.openlocfilehash: efc3fa0255aa765e515412c5fa4098303a9d9234
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457020"
---
# <a name="data-partitioning-strategies-building-real-world-cloud-apps-with-azure"></a>資料分割策略（使用 Azure 建立真實世界的雲端應用程式）

由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom 作者: dykstra](https://github.com/tdykstra)

[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。 其中說明13種模式和作法，可協助您成功開發雲端 web 應用程式。 如需有關數列的詳細資訊，請參閱[第一章](introduction.md)。

我們稍早看到，藉由新增和移除網頁伺服器，調整雲端應用程式的 web 層有多容易。 但是，如果它們全都到達相同的資料存放區，您應用程式的瓶頸就會從前端移至後端，而資料層則是最難調整的。 在本章中，我們將探討如何藉由將資料分割成多個關係資料庫，或是結合關係資料庫儲存體與其他資料儲存選項，讓您的資料層可擴充。

設定資料分割配置最適合先前所述的相同原因：在應用程式進入生產階段之後，很難以變更您的資料儲存策略。 如果您想要瞭解不同的方法，可以在您重新組織應用程式的資料和資料存取程式碼時，避免在您的應用程式損毀或長時間關閉時出現「Twitter 時刻」。

## <a name="the-three-vs-of-data-storage"></a>資料儲存體的三種與

若要判斷您是否需要資料分割策略及其應有的內容，請考慮您的資料有三個問題：

- 磁片區–您最終會儲存多少資料？ 有幾 gb？ 數百 gb？ Tb? Pt?
- 速度–資料成長的速度為何？ 這是不會產生大量資料的內部應用程式嗎？ 客戶將在其中上傳影像和影片的外部應用程式？
- 各種–您會儲存哪些類型的資料？ 關聯式、影像、索引鍵/值組、社交圖形？

如果您認為您的磁片區、速度或種類很大，您必須仔細考慮哪種資料分割配置可讓您的應用程式在成長時有效率且有效率地進行調整，並確保不會遇到任何瓶頸。

基本上，分割的方法有三種：

- 垂直資料分割
- 水平資料分割
- 混合式資料分割

## <a name="vertical-partitioning"></a>垂直資料分割

垂直 portioning 與依資料行分割資料表：一組資料行會放入一個資料存放區，而另一組資料行則會進入不同的資料存放區。

例如，假設我的應用程式儲存人員的相關資料，包括影像：

![資料表](data-partitioning-strategies/_static/image1.png)

當您以資料表的形式表示此資料並查看不同的資料時，您可以看到左邊的三個數據行具有可有效率地儲存在關係資料庫中的字串資料，而右邊的兩個數據行則是 c 的位元組陣列。從影像檔案 ome。 您可以將影像檔案資料儲存在關係資料庫中，而且有很多人都這麼做，因為他們不想要將資料儲存到檔案系統。 它們可能沒有能夠儲存所需資料量的檔案系統，或不想要管理個別的備份和還原系統。 這種方法適用于內部部署資料庫和雲端資料庫中的少量資料。 在內部部署環境中，只是讓 DBA 處理所有專案，可能比較容易。

但是在雲端資料庫中，儲存體的成本相當高，而大量的映射可能會使資料庫的大小增加超過其可有效率地運作的限制。 若要解決這些問題，您可以垂直分割資料，這表示您會針對資料表中的每個資料行，選擇最適當的資料存放區。 在此範例中，最適合使用的是將字串資料放在關係資料庫和 Blob 儲存體中的影像。

![以垂直方式分割的資料表](data-partitioning-strategies/_static/image2.png)

將影像儲存在 Blob 儲存體中，而不是在內部部署環境中，因為您不需要擔心設定檔案伺服器，或管理儲存在關係資料庫外部之資料的備份與還原，因此在雲端中的工作會更實用。Blob 儲存體服務會自動為您處理。

這是我們在修正 It 應用程式中所實行的分割方式，我們將在[Blob 儲存體一章](unstructured-blob-storage.md)中查看該方法的程式碼。 如果沒有此資料分割配置，而且假設平均映射大小為 3 mb，則修正 It 應用程式只能儲存大約40000個工作，再達到 150 gb 的資料庫大小上限。 移除映射之後，資料庫可以將10倍的工作儲存為許多工作;您可以花更長的時間來思考如何執行水準資料分割配置。 隨著應用程式的調整，您的支出成長會變得更慢，因為您的儲存空間需求將會非常便宜。

## <a name="horizontal-partitioning-sharding"></a>水平資料分割 (分區化)

水準 portioning 就像是依資料列分割資料表：一組資料列會進入一個資料存放區，而另一組資料列會進入不同的資料存放區。

假設有一組相同的資料，另一個選項是在不同的資料庫中儲存不同的客戶名稱範圍。

![資料表格水準分割](data-partitioning-strategies/_static/image3.png)

您想要非常小心分區化配置，以確保資料會平均分散，以避免作用點。 使用姓氏的第一個字母的簡單範例不符合該需求，因為很多人都有一個以特定通用字母開頭的名字。 您所叫用的資料表大小限制早于預期，因為某些資料庫會變得非常大，但大部分的情況下都很小。

水準資料分割的下層在於，在所有資料上執行查詢可能會很困難。 在此範例中，查詢必須從最多26個不同的資料庫中繪製，以取得應用程式所儲存的所有資料。

## <a name="hybrid-partitioning"></a>混合式資料分割

您可以結合垂直和水準資料分割。 例如，在範例資料中，您可以將影像儲存在 Blob 儲存體中，並水準分割字串資料。

![資料表混合式資料分割](data-partitioning-strategies/_static/image4.png)

## <a name="partitioning-a-production-application"></a>分割生產應用程式

在概念上，很容易就能看出資料分割配置的運作方式，但任何資料分割配置都會增加程式碼的複雜度，而且引進了許多您必須處理的新複雜性。 如果您要將映射移至 blob 儲存體，當儲存體服務關閉時該怎麼做？ 如何處理 blob 安全性？ 如果資料庫和 blob 儲存體不同步，會發生什麼事？ 如果您要分區化，您要如何處理所有資料庫的查詢？

如果您在進入生產環境之前進行規劃，就可以管理複雜的問題。 很多人都不願意這麼做。 我們的客戶諮詢團隊（CAT）團隊平均每個月會從應用程式以非常大的方式處理的客戶驚慌失措電話，而不會進行這項規劃。 而他們說的就是：「說明！ 我將所有專案都放在單一資料存放區中，而且在45天內，我的空間將會用盡！」 而且，如果您在存取資料存放區的過程中內建了許多商務邏輯，而且您有使用應用程式的客戶，則在您遷移時，不會有足夠的時間可讓您一天停機。 我們最終會經歷項的努力，協助客戶在不停機的時間即時分割其資料。 它非常令人興奮，而且非常可怕，如果可以避免，也不是您想要加入的東西！ 事先思考並將它整合到您的應用程式，可以讓應用程式在稍後成長時變得更容易。

## <a name="summary"></a>摘要

有效的資料分割配置可讓您的雲端應用程式在雲端中擴充至數以 pb 計的資料，而不會產生瓶頸。 如果您在內部部署資料中心內執行應用程式，就不需要支付大規模機器或廣泛基礎結構的正面。 在雲端中，您可以視需要累加地新增容量，而您只需支付使用時所使用的數量。

在[下一章](unstructured-blob-storage.md)中，我們將瞭解如何藉由將影像儲存在 Blob 儲存體中，來修正 It 應用程式如何執行垂直資料分割。

## <a name="resources"></a>資源

如需資料分割策略的詳細資訊，請參閱下列資源。

文件：

- [Windows Azure 雲端服務上大規模服務設計的最佳作法](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 以標記 Simm 和 Michael Thomassy 的技術白皮書。
- [Microsoft 模式和實務-雲端設計模式](https://msdn.microsoft.com/library/dn568099.aspx)。 請參閱資料分割指引，分區化模式。

影片：

- [防安全功能：建立可擴充、可復原的雲端服務](https://channel9.msdn.com/Series/FailSafe)。 Ulrich Homann、Marc Mercuri 和 Mark Simm 的九部分系列。 以非常容易存取且有趣的方式呈現高階概念和架構原則，並提供 Microsoft 客戶諮詢小組（CAT）體驗與實際客戶的故事。 請參閱第7集的資料分割討論。
- [打造 Big：從 Windows Azure 客戶學習到的經驗-第一部分](https://channel9.msdn.com/Events/Build/2012/3-029)。Mark Simm 討論資料分割配置、分區化策略、如何執行分區化，以及 SQL Database 同盟，從19:49 開始。 類似于防故障的系列，並深入探討如何詳細說明。

程式碼範例：

- [Windows Azure 中的雲端服務基本](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)概念。 包含分區化資料庫的範例應用程式。 如需所實分區化配置的說明，請參閱 Windows Azure blog 上的[DAL – RDBMS 分區化](https://blogs.msdn.com/b/windowsazure/archive/2013/09/05/dal-sharding-of-rdbms.aspx)。

> [!div class="step-by-step"]
> [上一頁](data-storage-options.md)
> [下一頁](unstructured-blob-storage.md)
