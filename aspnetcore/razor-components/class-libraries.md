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
# <a name="razor-components-class-libraries"></a><span data-ttu-id="8b08d-103">Razor 元件類別庫</span><span class="sxs-lookup"><span data-stu-id="8b08d-103">Razor Components Class Libraries</span></span>

<span data-ttu-id="8b08d-104">藉由[Simon Timms](https://github.com/stimms)</span><span class="sxs-lookup"><span data-stu-id="8b08d-104">By [Simon Timms](https://github.com/stimms)</span></span>

> [!NOTE]
> <span data-ttu-id="8b08d-105">.NET Core 3.0 Preview 2 SDK 不包含 Razor 元件類別程式庫的專案範本，但我們預計在未來的預覽版中新增範本。</span><span class="sxs-lookup"><span data-stu-id="8b08d-105">The .NET Core 3.0 Preview 2 SDK doesn't include a project template for Razor Component Class Libraries, but we expect to add a template in a future preview.</span></span> <span data-ttu-id="8b08d-106">同時，在中，您可以使用本主題所說明的 Blazor 元件類別庫範本。</span><span class="sxs-lookup"><span data-stu-id="8b08d-106">In meantime, you can use the Blazor Component Class Library template explained in this topic.</span></span>

<span data-ttu-id="8b08d-107">元件可以在專案之間共用元件程式庫中。</span><span class="sxs-lookup"><span data-stu-id="8b08d-107">Components can be shared in component libraries across projects.</span></span> <span data-ttu-id="8b08d-108">元件可以包含：</span><span class="sxs-lookup"><span data-stu-id="8b08d-108">Components can be included from:</span></span>

* <span data-ttu-id="8b08d-109">在方案中的另一個專案。</span><span class="sxs-lookup"><span data-stu-id="8b08d-109">Another project in the solution.</span></span>
* <span data-ttu-id="8b08d-110">NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="8b08d-110">A NuGet package.</span></span>
* <span data-ttu-id="8b08d-111">參考的.NET 程式庫。</span><span class="sxs-lookup"><span data-stu-id="8b08d-111">A referenced .NET library.</span></span>

<span data-ttu-id="8b08d-112">元件是一般的.NET 型別，如同元件程式庫會是一般的.NET 組件。</span><span class="sxs-lookup"><span data-stu-id="8b08d-112">Just as components are regular .NET types, component libraries are normal .NET assemblies.</span></span>

<span data-ttu-id="8b08d-113">若要建立新的元件程式庫，請使用`blazorlib`範本，內含[dotnet 新](/dotnet/core/tools/dotnet-new)命令。</span><span class="sxs-lookup"><span data-stu-id="8b08d-113">To create a new component library, use the `blazorlib` template with the [dotnet new](/dotnet/core/tools/dotnet-new) command.</span></span> <span data-ttu-id="8b08d-114">範本是一起安裝的範本的一部分時[設定 Razor 元件](xref:razor-components/get-started)。</span><span class="sxs-lookup"><span data-stu-id="8b08d-114">The template is part of the templates installed when [setting up Razor Components](xref:razor-components/get-started).</span></span>

```console
dotnet new blazorlib -o MyComponentLib1
```

<span data-ttu-id="8b08d-115">若要加入現有的專案程式庫，請使用[dotnet sln](/dotnet/core/tools/dotnet-sln)命令：</span><span class="sxs-lookup"><span data-stu-id="8b08d-115">To add the library to an existing project, use the [dotnet sln](/dotnet/core/tools/dotnet-sln) command:</span></span>

```console
dotnet sln add .\MyComponentLib1
```

<span data-ttu-id="8b08d-116">元件程式庫可能包含靜態檔案，例如影像、 JavaScript 和樣式表。</span><span class="sxs-lookup"><span data-stu-id="8b08d-116">Component libraries may contain static files, such as images, JavaScript, and stylesheets.</span></span> <span data-ttu-id="8b08d-117">在建置時，靜態檔案內嵌到建置組件檔案 (*.dll*)，可讓元件的耗用量，而不必擔心如何包含其資源。</span><span class="sxs-lookup"><span data-stu-id="8b08d-117">At build time, static files are embedded into the built assembly file (*.dll*), which allows consumption of the components without having to worry about how to include their resources.</span></span> <span data-ttu-id="8b08d-118">包含的任何檔案`content`目錄標示為內嵌資源。</span><span class="sxs-lookup"><span data-stu-id="8b08d-118">Any files included in the `content` directory are marked as an embedded resource.</span></span> 

## <a name="consume-a-library-component"></a><span data-ttu-id="8b08d-119">使用程式庫元件</span><span class="sxs-lookup"><span data-stu-id="8b08d-119">Consume a library component</span></span>

<span data-ttu-id="8b08d-120">若要使用定義在另一個專案中，文件庫中的元件[ @addTagHelper ](/aspnet/core/mvc/views/tag-helpers/intro#add-helper-label)必須使用指示詞。</span><span class="sxs-lookup"><span data-stu-id="8b08d-120">In order to consume components defined in a library in another project, the [@addTagHelper](/aspnet/core/mvc/views/tag-helpers/intro#add-helper-label) directive must be used.</span></span> <span data-ttu-id="8b08d-121">個別元件可能會依名稱加入。</span><span class="sxs-lookup"><span data-stu-id="8b08d-121">Individual components may be added by name.</span></span> <span data-ttu-id="8b08d-122">例如，新增下列指示詞`Component1`的`MyComponentLib1`:</span><span class="sxs-lookup"><span data-stu-id="8b08d-122">For example, the following directive adds `Component1` of `MyComponentLib1`:</span></span>

```cshtml
@addTagHelper MyComponentLib1.Component1, MyComponentLib1
```

<span data-ttu-id="8b08d-123">指示詞一般格式為：</span><span class="sxs-lookup"><span data-stu-id="8b08d-123">The general format of the directive is:</span></span>

```cshtml
@addTagHelper <namespaced component name>, <assembly name>
```

<span data-ttu-id="8b08d-124">不過，通常會包含所有的元件，從組件使用萬用字元：</span><span class="sxs-lookup"><span data-stu-id="8b08d-124">However, it's common to include all of the components from an assembly using a wildcard:</span></span>

```cshtml
@addTagHelper *, MyComponentLib1
```

<span data-ttu-id="8b08d-125">`@addTagHelper`指示詞可以包含在 *_ViewImport.cshtml*使元件適用於整個專案或套用至單一頁面或一組資料夾內的頁面。</span><span class="sxs-lookup"><span data-stu-id="8b08d-125">The `@addTagHelper` directive can be included in *_ViewImport.cshtml* to make the components available for an entire project or applied to a single page or set of pages within a folder.</span></span> <span data-ttu-id="8b08d-126">使用`@addTagHelper`就地指示詞時，元件程式庫的元件可以使用，彷彿應用程式相同的組件中。</span><span class="sxs-lookup"><span data-stu-id="8b08d-126">With the `@addTagHelper` directive in place, the components of the component library can be consumed as if they were in the same assembly as the app.</span></span> 

## <a name="build-pack-and-ship-to-nuget"></a><span data-ttu-id="8b08d-127">組建、 套件及出貨至 NuGet</span><span class="sxs-lookup"><span data-stu-id="8b08d-127">Build, pack, and ship to NuGet</span></span>

<span data-ttu-id="8b08d-128">因為元件程式庫是標準的.NET 程式庫，並無不同封裝和傳送任何程式庫 nuget 封裝和傳送至 NuGet。</span><span class="sxs-lookup"><span data-stu-id="8b08d-128">Because component libraries are standard .NET libraries, packaging and shipping them to NuGet is no different from packaging and shipping any library to NuGet.</span></span> <span data-ttu-id="8b08d-129">使用執行封裝[dotnet pack](/dotnet/core/tools/dotnet-pack)命令：</span><span class="sxs-lookup"><span data-stu-id="8b08d-129">Packaging is performed using the [dotnet pack](/dotnet/core/tools/dotnet-pack) command:</span></span>

```console
dotnet pack
```

<span data-ttu-id="8b08d-130">使用 NuGet 封裝上傳[dotnet nuget 發行](/dotnet/core/tools/dotnet-nuget-push)命令：</span><span class="sxs-lookup"><span data-stu-id="8b08d-130">Upload the package to NuGet using the [dotnet nuget publish](/dotnet/core/tools/dotnet-nuget-push) command:</span></span>

```console
dotnet nuget publish
```

<span data-ttu-id="8b08d-131">任何包含的靜態資源會納入 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="8b08d-131">Any included static resources are included in the NuGet package.</span></span> <span data-ttu-id="8b08d-132">程式庫取用者會自動接收指令碼和樣式表，讓取用者不一定要以手動方式安裝的資源。</span><span class="sxs-lookup"><span data-stu-id="8b08d-132">Library consumers automatically receive scripts and stylesheets, so consumers aren't required to manually install the resources.</span></span>
