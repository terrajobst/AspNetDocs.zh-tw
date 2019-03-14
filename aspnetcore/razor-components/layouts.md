---
title: Razor 元件版面配置
author: guardrex
description: 了解如何建立可重複使用的版面配置 Blazor 和 Razor 元件的應用程式的元件。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/layouts
ms.openlocfilehash: 23d8f441c0b3bbde7a73717f6257013831617ec0
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039035"
---
# <a name="razor-components-layouts"></a>Razor 元件版面配置

藉由[Rainer Stropek](https://www.timecockpit.com)

應用程式通常會包含一個以上的頁面。 版面配置項目，例如功能表、 著作權訊息，以及標誌，必須要有所有頁面。 將這些版面配置元素的程式碼複製到所有的應用程式頁面不是有效的解決方案。 這類重複資料刪除會很難維護，並可能會導致不一致的內容經過一段時間。 *版面配置*解決這個問題。

技術上來說，版面配置是只是另一個元件。 版面配置定義中的 Razor 範本，或在C#程式碼，而且可以包含資料繫結、 相依性插入和其他一般功能的元件。 開啟兩個的其他層面*元件*成*版面配置*:

* 配置元件必須繼承自`BlazorLayoutComponent`。 `BlazorLayoutComponent` 定義`Body`屬性，其中包含要配置內呈現的內容。
* 配置元件會使用`Body`屬性來指定應本文內容呈現使用 Razor 語法`@Body`。 在呈現期間，`@Body`版面配置的內容所取代。

下列程式碼範例顯示的 Razor 範本的配置元件。 請注意，使用`BlazorLayoutComponent`和`@Body`:

```csharp
@inherits BlazorLayoutComponent

<header>
    <h1>ERP Master 3000</h1>
</header>

<nav>
    <a href="master-data">Master Data Management</a>
    <a href="invoicing">Invoicing</a>
    <a href="accounting">Accounting</a>
</nav>

@Body

<footer>
    &copy; by @CopyrightMessage
</footer>

@functions {
    public string CopyrightMessage { get; set; }
    ...
}
```

## <a name="use-a-layout-in-a-component"></a>元件中使用的版面配置

使用 Razor 指示詞`@layout`来套用至元件的版面配置。 編譯器會將轉換成這個指示詞`LayoutAttribute`，套用至元件類別。

下列程式碼範例示範概念。 此元件的內容會插入*MasterLayout*位置的`@Body`:

```csharp
@layout MasterLayout

@page "/master-data"

<h2>Master Data Management</h2>
...
```

## <a name="centralized-layout-selection"></a>集中式的配置選取項目

每個資料夾的應用程式可以選擇性地包含範本檔案，名為 *_ViewImports.cshtml*。 編譯器會包含在相同的資料夾中的 Razor 範本，然後遞迴地在其所有子資料夾中的所有檢視匯入檔案中指定的指示詞。 因此， *_ViewImports.cshtml*檔案，其中`@layout MainLayout`可確保所有資料夾使用中的元件*MainLayout*版面配置。 不需要重複新增`@layout`的所有 *\*.cshtml*檔案。

請注意，預設範本會使用 *_ViewImports.cshtml*版面配置選擇的機制。 新建立的應用程式包含 *_ViewImports.cshtml*中的檔案*頁*資料夾。

## <a name="nested-layouts"></a>巢狀版面配置

應用程式可以包含巢狀版面配置。 元件可以參考會參考另一個版面配置的配置。 例如，巢狀版面配置可用來反映多層級的功能表結構。

下列程式碼範例示範如何使用巢狀的版面配置。 *CustomersComponent.cshtml*檔案是要顯示的元件。 附註的元件參考配置`MasterDataLayout`。

*CustomersComponent.cshtml*:

```csharp
@layout MasterDataLayout

@page "/master-data/customers"

<h1>Customer Maintenance</h1>
...
```

*MasterDataLayout.cshtml*檔案提供`MasterDataLayout`。 版面配置參考另一個版面配置， `MainLayout`，它會內嵌。

*MasterDataLayout.cshtml*:

```csharp
@layout MainLayout
@inherits BlazorLayoutComponent

<nav>
    <!-- Menu structure of master data module -->
    ...
</nav>

@Body
```

最後，`MainLayout`包含最上層的版面配置項目，例如頁首、 頁尾及主功能表。

*MainLayout.cshtml*:

```csharp
@inherits BlazorLayoutComponent

<header>...</header>
<nav>...</nav>

@Body
```
