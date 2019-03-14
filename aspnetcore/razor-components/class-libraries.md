---
title: Razor 元件類別庫
author: guardrex
description: 探索如何包含元件，外部元件程式庫中的 Razor 元件應用程式。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/09/2019
uid: razor-components/class-libraries
ms.openlocfilehash: 0e644627178bae2b8880760335860b3e0ebef156
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037405"
---
# <a name="razor-components-class-libraries"></a>Razor 元件類別庫

藉由[Simon Timms](https://github.com/stimms)

> [!NOTE]
> .NET Core 3.0 Preview 2 SDK 不包含 Razor 元件類別程式庫的專案範本，但我們預計在未來的預覽版中新增範本。 同時，在中，您可以使用本主題所說明的 Blazor 元件類別庫範本。

元件可以在專案之間共用元件程式庫中。 元件可以包含：

* 在方案中的另一個專案。
* NuGet 套件。
* 參考的.NET 程式庫。

元件是一般的.NET 型別，如同元件程式庫會是一般的.NET 組件。

若要建立新的元件程式庫，請使用`blazorlib`範本，內含[dotnet 新](/dotnet/core/tools/dotnet-new)命令。 範本是一起安裝的範本的一部分時[設定 Razor 元件](xref:razor-components/get-started)。

```console
dotnet new blazorlib -o MyComponentLib1
```

若要加入現有的專案程式庫，請使用[dotnet sln](/dotnet/core/tools/dotnet-sln)命令：

```console
dotnet sln add .\MyComponentLib1
```

元件程式庫可能包含靜態檔案，例如影像、 JavaScript 和樣式表。 在建置時，靜態檔案內嵌到建置組件檔案 (*.dll*)，可讓元件的耗用量，而不必擔心如何包含其資源。 包含的任何檔案`content`目錄標示為內嵌資源。 

## <a name="consume-a-library-component"></a>使用程式庫元件

若要使用定義在另一個專案中，文件庫中的元件[ @addTagHelper ](/aspnet/core/mvc/views/tag-helpers/intro#add-helper-label)必須使用指示詞。 個別元件可能會依名稱加入。 例如，新增下列指示詞`Component1`的`MyComponentLib1`:

```cshtml
@addTagHelper MyComponentLib1.Component1, MyComponentLib1
```

指示詞一般格式為：

```cshtml
@addTagHelper <namespaced component name>, <assembly name>
```

不過，通常會包含所有的元件，從組件使用萬用字元：

```cshtml
@addTagHelper *, MyComponentLib1
```

`@addTagHelper`指示詞可以包含在 *_ViewImport.cshtml*使元件適用於整個專案或套用至單一頁面或一組資料夾內的頁面。 使用`@addTagHelper`就地指示詞時，元件程式庫的元件可以使用，彷彿應用程式相同的組件中。 

## <a name="build-pack-and-ship-to-nuget"></a>組建、 套件及出貨至 NuGet

因為元件程式庫是標準的.NET 程式庫，並無不同封裝和傳送任何程式庫 nuget 封裝和傳送至 NuGet。 使用執行封裝[dotnet pack](/dotnet/core/tools/dotnet-pack)命令：

```console
dotnet pack
```

使用 NuGet 封裝上傳[dotnet nuget 發行](/dotnet/core/tools/dotnet-nuget-push)命令：

```console
dotnet nuget publish
```

任何包含的靜態資源會納入 NuGet 套件。 程式庫取用者會自動接收指令碼和樣式表，讓取用者不一定要以手動方式安裝的資源。
