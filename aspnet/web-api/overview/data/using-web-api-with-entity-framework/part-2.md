---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: 新增模型和控制器 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: 57dacda421968f341284d89c9a3ad80040c16e25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557537"
---
# <a name="add-models-and-controllers"></a>新增模型與控制器

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://github.com/MikeWasson/BookService)

在本節中，您將加入定義資料庫實體的模型類別。 接著，您將新增 Web API 控制器，在這些實體上執行 CRUD 作業。

## <a name="add-model-classes"></a>新增模型類別

在本教學課程中，我們將使用「Code First」方法來建立資料庫，以 Entity Framework （EF）。 使用 Code First，您可以C#撰寫對應至資料庫資料表的類別，而 EF 會建立資料庫。 （如需詳細資訊，請參閱[Entity Framework 開發方法](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf)）。

我們一開始會將領域物件定義為 Poco （純舊的 CLR 物件）。 我們將建立下列 Poco：

- 作者
- 書籍

在方案總管中，以滑鼠右鍵按一下 [模型] 資料夾。 選取 [**新增**]，然後選取 [**類別**]。 將類別命名為 `Author`。

![](part-2/_static/image1.png)

以下列程式碼取代 Author.cs 中的所有重複使用程式碼。

[!code-csharp[Main](part-2/samples/sample1.cs)]

使用下列程式碼，新增名為 `Book`的另一個類別。

[!code-csharp[Main](part-2/samples/sample2.cs)]

Entity Framework 將會使用這些模型來建立資料庫資料表。 針對每個模型，`Id` 屬性會成為資料庫資料表的主鍵資料行。

在 Book 類別中，`AuthorId` 會在 `Author` 資料表中定義外鍵。 （為了簡單起見，我假設每一本書都有一位作者）。Book 類別也包含相關 `Author`的導覽屬性。 您可以使用導覽屬性來存取程式碼中的相關 `Author`。 我更進一步瞭解第4部分中的導覽屬性，[處理實體](part-4.md)關聯。

## <a name="add-web-api-controllers"></a>新增 Web API 控制器

在本節中，我們將新增支援 CRUD 作業（建立、讀取、更新和刪除）的 Web API 控制器。 控制器會使用 Entity Framework 來與資料庫層通訊。

首先，您可以刪除檔控制器/ValuesController。 此檔案包含範例 Web API 控制器，但在本教學課程中，您不需要用到它。

![](part-2/_static/image2.png)

接下來，建立專案。 Web API 樣板會使用反映來尋找模型類別，因此需要已編譯的元件。

在方案總管中，以滑鼠右鍵按一下 [控制器] 資料夾。 選取 [**新增**]，然後選取 [**控制器**]。

![](part-2/_static/image3.png)

在 [**新增 Scaffold** ] 對話方塊中，選取 [具有動作的 Web API 2 控制器，使用 Entity Framework]。 按一下 [新增]。

![](part-2/_static/image4.png)

在 [**新增控制器**] 對話方塊中，執行下列動作：

1. 在 [**模型類別**] 下拉式清單中，選取 [`Author`] 類別。 （如果您沒有看到它列在下拉式清單中，請確定您已建立專案）。
2. 勾選 [使用非同步控制器動作]。
3. 將控制器名稱保留 &quot;AuthorsController&quot;。
4. 按一下 [**資料內容類別**] 旁邊的加號（+）按鈕。

![](part-2/_static/image5.png)

在 [**新增資料內容**] 對話方塊中，保留預設名稱，然後按一下 [**加入**]。

![](part-2/_static/image6.png)

按一下 [**新增**] 以完成 [**新增控制器**] 對話方塊。 對話方塊會將兩個類別新增至您的專案：

- `AuthorsController` 定義 Web API 控制器。 控制器會執行用戶端用來在作者清單上執行 CRUD 作業的 REST API。
- `BookServiceContext` 在運行時間管理實體物件，其中包括以資料庫的資料填入物件、變更追蹤，以及將資料保存至資料庫。 它繼承自 `DbContext`。

![](part-2/_static/image7.png)

此時，請重新建立專案。 現在，請執行相同的步驟，為 `Book` 實體新增 API 控制器。 這次請選取模型類別的 [`Book`]，然後選取資料內容類別的現有 `BookServiceContext` 類別。 （請勿建立新的資料內容）。按一下 [**新增**] 以新增控制器。

![](part-2/_static/image8.png)

> [!div class="step-by-step"]
> [上一頁](part-1.md)
> [下一頁](part-3.md)
