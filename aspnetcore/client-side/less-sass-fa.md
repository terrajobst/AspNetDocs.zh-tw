---
title: ASP.NET Core 中的 Less、Sass 與 Font Awesome
author: ardalis
description: 了解如何在 ASP.NET Core 應用程式中使用 Less、Sass 與 Font Awesome。
ms.author: tdykstra
ms.date: 10/14/2016
uid: client-side/less-sass-fa
ms.openlocfilehash: 2229c4e3b0238ff17c15e78f657b9acb10495c72
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57065555"
---
# <a name="less-sass-and-font-awesome-in-aspnet-core"></a><span data-ttu-id="c2c17-103">ASP.NET Core 中的 Less、Sass 與 Font Awesome</span><span class="sxs-lookup"><span data-stu-id="c2c17-103">Less, Sass, and Font Awesome in ASP.NET Core</span></span>

<span data-ttu-id="c2c17-104">作者：[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="c2c17-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="c2c17-105">說到樣式與整體體驗時，Web 應用程式的使用者會有越來越高的期望。</span><span class="sxs-lookup"><span data-stu-id="c2c17-105">Users of web applications have increasingly high expectations when it comes to style and overall experience.</span></span> <span data-ttu-id="c2c17-106">現代化 Web 應用程式經常會運用豐富的工具與架構以一致的方式定義及管理其外觀及操作。</span><span class="sxs-lookup"><span data-stu-id="c2c17-106">Modern web applications frequently leverage rich tools and frameworks for defining and managing their look and feel in a consistent manner.</span></span> <span data-ttu-id="c2c17-107">如 [Bootstrap](http://getbootstrap.com/) 的架構在定義常用樣式集與版面配置選項時可非常成功。</span><span class="sxs-lookup"><span data-stu-id="c2c17-107">Frameworks like [Bootstrap](http://getbootstrap.com/) can go a long way toward defining a common set of styles and layout options for web sites.</span></span> <span data-ttu-id="c2c17-108">不過，大部分的非一般站台也可以從能夠有效地定義及維護樣式與階層式樣式表 (CSS) 檔案，以及輕鬆存取協助讓站台的介面更直覺的非影像圖示。</span><span class="sxs-lookup"><span data-stu-id="c2c17-108">However, most non-trivial sites also benefit from being able to effectively define and maintain styles and cascading style sheet (CSS) files, as well as having easy access to non-image icons that help make the site's interface more intuitive.</span></span> <span data-ttu-id="c2c17-109">這是支援 [Less](http://lesscss.org/) 與 [Sass](http://sass-lang.com/) 以及程式庫 (例如 [Font Awesome](http://fontawesome.io/)) 之語言與工具的存在之處。</span><span class="sxs-lookup"><span data-stu-id="c2c17-109">That's where languages and tools that support [Less](http://lesscss.org/) and [Sass](http://sass-lang.com/), and libraries like [Font Awesome](http://fontawesome.io/), come in.</span></span>

## <a name="css-preprocessor-languages"></a><span data-ttu-id="c2c17-110">CSS 前置處理器的語言</span><span class="sxs-lookup"><span data-stu-id="c2c17-110">CSS preprocessor languages</span></span>

<span data-ttu-id="c2c17-111">編譯為其他語言以改善使用底層語言之體驗的語言稱為前置處理器。</span><span class="sxs-lookup"><span data-stu-id="c2c17-111">Languages that are compiled into other languages, in order to improve the experience of working with the underlying language, are referred to as preprocessors.</span></span> <span data-ttu-id="c2c17-112">有兩個熱門的前置處理器 css:較不和 Sass。</span><span class="sxs-lookup"><span data-stu-id="c2c17-112">There are two popular preprocessors for CSS: Less and Sass.</span></span>  <span data-ttu-id="c2c17-113">這些前置處理器可為 CSS 新增功能，例如對變數與巢狀規則的支援，這可以改善大型、複雜樣式表的可維護性。</span><span class="sxs-lookup"><span data-stu-id="c2c17-113">These preprocessors add features to CSS, such as support for variables and nested rules, which improve the maintainability of large, complex stylesheets.</span></span> <span data-ttu-id="c2c17-114">CSS 做為語言是非常基本，甚至不支援簡單的功能 (例如變數)，而這使得 CSS 檔案重複性高且繁雜。</span><span class="sxs-lookup"><span data-stu-id="c2c17-114">CSS as a language is very basic, lacking support even for something as simple as variables, and this tends to make CSS files repetitive and bloated.</span></span> <span data-ttu-id="c2c17-115">透過前置處理器加入實際程式設計語言功能有助於減少重複項目並提供更好的樣式規則組織方式。</span><span class="sxs-lookup"><span data-stu-id="c2c17-115">Adding real programming language features via preprocessors can help reduce duplication and provide better organization of styling rules.</span></span> <span data-ttu-id="c2c17-116">Visual Studio 原生支援 Less 與 Sass，以及可進一步改善當使用這些語言時可進一步改善開發體驗的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="c2c17-116">Visual Studio provides built-in support for both Less and Sass, as well as extensions that can further improve the development experience when working with these languages.</span></span>

<span data-ttu-id="c2c17-117">做為前置處理器如何改善可讀性和可維護性的樣式資訊的快速範例，請考慮這個 CSS:</span><span class="sxs-lookup"><span data-stu-id="c2c17-117">As a quick example of how preprocessors can improve readability and maintainability of style information, consider this CSS:</span></span>

```css
.header {
    color: black;
    font-weight: bold;
    font-size: 18px;
    font-family: Helvetica, Arial, sans-serif;
}

.small-header {
    color: black;
    font-weight: bold;
    font-size: 14px;
    font-family: Helvetica, Arial, sans-serif;
}
```

<span data-ttu-id="c2c17-118">使用 Less，這可以使用 *mixin* 重寫以排除所有重複項 (如此命名是因為它可讓您將來自一個類別或規則集的屬性 "mix" 到另一個類別或規則集)：</span><span class="sxs-lookup"><span data-stu-id="c2c17-118">Using Less, this can be rewritten to eliminate all of the duplication, using a *mixin* (so named because it allows you to "mix in" properties from one class or rule-set into another):</span></span>

```less
.header {
    color: black;
    font-weight: bold;
    font-size: 18px;
    font-family: Helvetica, Arial, sans-serif;
}

.small-header {
    .header;
    font-size: 14px;
}
```

## <a name="less"></a><span data-ttu-id="c2c17-119">Less</span><span class="sxs-lookup"><span data-stu-id="c2c17-119">Less</span></span>

<span data-ttu-id="c2c17-120">Less CSS 前置處理器會使用 Node.js 來執行。</span><span class="sxs-lookup"><span data-stu-id="c2c17-120">The Less CSS preprocessor runs using Node.js.</span></span> <span data-ttu-id="c2c17-121">若要安裝 Less，請從命令提示字元使用節點套件管理員 (npm) (-g 表示「全域」)：</span><span class="sxs-lookup"><span data-stu-id="c2c17-121">To install Less, use Node Package Manager (npm) from a command prompt (-g means "global"):</span></span>

```console
npm install -g less
```

<span data-ttu-id="c2c17-122">如果您使用 Visual Studio，您可以開始使用 Less，方式是將一或多個 Less 檔案加入到您的專案，然後設定在編譯時期使用 Gulp (或 Grunt) 來處理它們</span><span class="sxs-lookup"><span data-stu-id="c2c17-122">If you're using Visual Studio, you can get started with Less by adding one or more Less files to your project, and then configuring Gulp (or Grunt) to process them at compile-time.</span></span> <span data-ttu-id="c2c17-123">新增 *Style* 資料夾到您的專案，然後加入命名為 *main.less* 的新 Less 檔案到此資料夾。</span><span class="sxs-lookup"><span data-stu-id="c2c17-123">Add a *Styles* folder to your project, and then add a new Less file named *main.less* to this folder.</span></span>

![新增 less 檔案](less-sass-fa/_static/add-less-file.png)

<span data-ttu-id="c2c17-125">新增之後，您的資料夾結構看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="c2c17-125">Once added, your folder structure should look something like this:</span></span>

![資料夾結構](less-sass-fa/_static/folder-structure.png)

<span data-ttu-id="c2c17-127">現在您可以加入一些基本的樣式會編譯成 CSS 並部署到 wwwroot 資料夾 Gulp 的檔案。</span><span class="sxs-lookup"><span data-stu-id="c2c17-127">Now you can add some basic styling to the file, which will be compiled into CSS and deployed to the wwwroot folder by Gulp.</span></span>

<span data-ttu-id="c2c17-128">修改*main.less*包含下列內容，並從單一基底的色彩建立簡單的調色盤。</span><span class="sxs-lookup"><span data-stu-id="c2c17-128">Modify *main.less* to include the following content, which creates a simple color palette from a single base color.</span></span>

```less
@base: #663333;
@background: spin(@base, 180);
@lighter: lighten(spin(@base, 5), 10%);
@lighter2: lighten(spin(@base, 10), 20%);
@darker: darken(spin(@base, -5), 10%);
@darker2: darken(spin(@base, -10), 20%);

body {
    background-color:@background;
}
.baseColor  {color:@base}
.bgLight    {color:@lighter}
.bgLight2   {color:@lighter2}
.bgDark     {color:@darker}
.bgDark2    {color:@darker2}
```

<span data-ttu-id="c2c17-129">`@base` 與其他開頭為 @-prefixed的項目是變數。</span><span class="sxs-lookup"><span data-stu-id="c2c17-129">`@base` and the other @-prefixed items are variables.</span></span> <span data-ttu-id="c2c17-130">每個都代表一個色彩。</span><span class="sxs-lookup"><span data-stu-id="c2c17-130">Each of them represents a color.</span></span> <span data-ttu-id="c2c17-131">除了`@base`，它們準備好使用色彩函式： 淡化、 暗化，和微調。</span><span class="sxs-lookup"><span data-stu-id="c2c17-131">Except for `@base`, they're set using color functions: lighten, darken, and spin.</span></span> <span data-ttu-id="c2c17-132">淡化與暗化可執行您預期的動作，而微調則會依度數 (色彩轉輪上所示) 調整色彩的色調。</span><span class="sxs-lookup"><span data-stu-id="c2c17-132">Lighten and darken do pretty much what you would expect; spin adjusts the hue of a color by a number of degrees (around the color wheel).</span></span> <span data-ttu-id="c2c17-133">Less 處理器夠聰明，可以忽略不使用的變數，因此為了示範這些變數如何運作，我們必須在某處使用它們。</span><span class="sxs-lookup"><span data-stu-id="c2c17-133">The Less processor is smart enough to ignore variables that aren't used, so to demonstrate how these variables work, we need to use them somewhere.</span></span> <span data-ttu-id="c2c17-134">類別`.baseColor`，等會示範每個產生的 CSS 檔中變數的導出的值。</span><span class="sxs-lookup"><span data-stu-id="c2c17-134">The classes `.baseColor`, etc. will demonstrate the calculated values of each of the variables in the CSS file that's produced.</span></span>

### <a name="get-started"></a><span data-ttu-id="c2c17-135">開始使用</span><span class="sxs-lookup"><span data-stu-id="c2c17-135">Get started</span></span>

<span data-ttu-id="c2c17-136">建立**npm 設定檔**(*package.json*) 在您的專案資料夾並加以編輯以參考`gulp`和`gulp-less`:</span><span class="sxs-lookup"><span data-stu-id="c2c17-136">Create an **npm Configuration File** (*package.json*) in your project folder and edit it to reference `gulp` and `gulp-less`:</span></span>

```json
{
  "version": "1.0.0",
  "name": "asp.net",
  "private": true,
  "devDependencies": {
    "gulp": "3.9.1",
    "gulp-less": "3.3.0"
  }
}
```

<span data-ttu-id="c2c17-137">在您的專案資料夾，或在 Visual Studio 中安裝的相依性，請在命令提示字元**方案總管**(**相依性 > npm > 還原套件**)。</span><span class="sxs-lookup"><span data-stu-id="c2c17-137">Install the dependencies either at a command prompt in your project folder, or in Visual Studio **Solution Explorer** (**Dependencies > npm > Restore packages**).</span></span>

```console
npm install
```

![VS 還原套件](less-sass-fa/_static/restore-packages.png)

<span data-ttu-id="c2c17-139">在 [專案] 資料夾中，建立**Gulp 組態檔**(*gulpfile.js*) 來定義自動化的程序。</span><span class="sxs-lookup"><span data-stu-id="c2c17-139">In the project folder, create a **Gulp Configuration File** (*gulpfile.js*) to define the automated process.</span></span>  <span data-ttu-id="c2c17-140">新增變數來代表 Less 檔案以及執行較少工作的頂端：</span><span class="sxs-lookup"><span data-stu-id="c2c17-140">Add a variable at the top of the file to represent Less, and a task to run Less:</span></span>

```javascript
var gulp = require("gulp"),
  fs = require("fs"),
  less = require("gulp-less");

gulp.task("less", function () {
  return gulp.src('Styles/main.less')
    .pipe(less())
    .pipe(gulp.dest('wwwroot/css'));
});
```

<span data-ttu-id="c2c17-141">開啟**Task Runner Explorer** (**檢視 > 其他 Windows > Task Runner Explorer**)。</span><span class="sxs-lookup"><span data-stu-id="c2c17-141">Open the **Task Runner Explorer** (**View > Other Windows > Task Runner Explorer**).</span></span> <span data-ttu-id="c2c17-142">在工作中，您應該會看到名為的新工作`less`。</span><span class="sxs-lookup"><span data-stu-id="c2c17-142">Among the tasks, you should see a new task named `less`.</span></span> <span data-ttu-id="c2c17-143">您可能必須重新整理視窗。</span><span class="sxs-lookup"><span data-stu-id="c2c17-143">You might have to refresh the window.</span></span>

<span data-ttu-id="c2c17-144">執行`less`工作，並會看到類似以下所示：</span><span class="sxs-lookup"><span data-stu-id="c2c17-144">Run the `less` task, and you see output similar to what is shown here:</span></span>

![較少的工作執行器](less-sass-fa/_static/less-task-runner.png)

<span data-ttu-id="c2c17-146">*Wwwroot/css*資料夾現在包含新的檔案*main.css*:</span><span class="sxs-lookup"><span data-stu-id="c2c17-146">The *wwwroot/css* folder now contains a new file, *main.css*:</span></span>

![建立主要的 css](less-sass-fa/_static/main-css-created.png)

<span data-ttu-id="c2c17-148">開啟*main.css* ，您會看到類似下列內容：</span><span class="sxs-lookup"><span data-stu-id="c2c17-148">Open *main.css* and you see something like the following:</span></span>

```css
body {
    background-color: #336666;
}
.baseColor {
    color: #663333;
}
.bgLight {
    color: #884a44;
}
.bgLight2 {
    color: #aa6355;
}
.bgDark {
    color: #442225;
}
.bgDark2 {
    color: #221114;
}
```

<span data-ttu-id="c2c17-149">加入簡單的 HTML 頁面，以便*wwwroot*資料夾，然後參考*main.css*若要查看作用中的色彩調色盤。</span><span class="sxs-lookup"><span data-stu-id="c2c17-149">Add a simple HTML page to the *wwwroot* folder, and reference *main.css* to see the color palette in action.</span></span>

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <link href="css/main.css" rel="stylesheet" />
    <title></title>
</head>
<body>
    <div>
        <div class="baseColor">BaseColor</div>
        <div class="bgLight">Light</div>
        <div class="bgLight2">Light2</div>
        <div class="bgDark">Dark</div>
        <div class="bgDark2">Dark2</div>
    </div>
</body>
</html>
```

<span data-ttu-id="c2c17-150">您可以看到在上旋轉 180 度`@base`用來產生`@background`導致相反的色彩的色彩轉輪`@base`:</span><span class="sxs-lookup"><span data-stu-id="c2c17-150">You can see that the 180 degree spin on `@base` used to produce `@background` resulted in the color wheel opposing color of `@base`:</span></span>

![較低的測試範例](less-sass-fa/_static/less-test-screenshot.png)

<span data-ttu-id="c2c17-152">Less 也提供對巢狀規則與巢狀媒體查詢的支援。</span><span class="sxs-lookup"><span data-stu-id="c2c17-152">Less also provides support for nested rules, as well as nested media queries.</span></span> <span data-ttu-id="c2c17-153">例如，定義如功能表的巢狀階層可能會導致繁複的 CSS 規則，例如這些：</span><span class="sxs-lookup"><span data-stu-id="c2c17-153">For example, defining nested hierarchies like menus can result in verbose CSS rules like these:</span></span>

```css
nav {
    height: 40px;
    width: 100%;
}
nav li {
    height: 38px;
    width: 100px;
}
nav li a:link {
    color: #000;
    text-decoration: none;
}
nav li a:visited {
    text-decoration: none;
    color: #CC3333;
}
nav li a:hover {
    text-decoration: underline;
    font-weight: bold;
}
nav li a:active {
    text-decoration: underline;
}
```

<span data-ttu-id="c2c17-154">在理想情況下的所有相關的樣式規則將會放在一起在 CSS 檔案中，但實際上沒有任何強制執行這項規則，除了慣例和或許區塊註解。</span><span class="sxs-lookup"><span data-stu-id="c2c17-154">Ideally all of the related style rules will be placed together within the CSS file, but in practice there's nothing enforcing this rule except convention and perhaps block comments.</span></span>

<span data-ttu-id="c2c17-155">使用 LESS 定義這些相同規則看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="c2c17-155">Defining these same rules using Less looks like this:</span></span>

```less
nav {
    height: 40px;
    width: 100%;
    li {
        height: 38px;
        width: 100px;
        a {
            color: #000;
            &:link { text-decoration:none}
            &:visited { color: #CC3333; text-decoration:none}
            &:hover { text-decoration:underline; font-weight:bold}
            &:active {text-decoration:underline}
        }
    }
}
```

<span data-ttu-id="c2c17-156">請注意，在此情況下，所有的附屬項目`nav`包含其範圍內。</span><span class="sxs-lookup"><span data-stu-id="c2c17-156">Note that in this case, all of the subordinate elements of `nav` are contained within its scope.</span></span> <span data-ttu-id="c2c17-157">不再有任何重複的父項目 (`nav`， `li`， `a`)，並已一併卸除總計的行數 （雖然有部分是將值放在第二個範例中的同一行上的結果）。</span><span class="sxs-lookup"><span data-stu-id="c2c17-157">There's no longer any repetition of parent elements (`nav`, `li`, `a`), and the total line count has dropped as well (though some of that's a result of putting values on the same lines in the second example).</span></span> <span data-ttu-id="c2c17-158">它可以是很有幫助組織，在此情況下查看所有指定的 UI 項目明確繫結的範圍內的規則檔案的其餘部分所設定大括號。</span><span class="sxs-lookup"><span data-stu-id="c2c17-158">It can be very helpful, organizationally, to see all of the rules for a given UI element within an explicitly bounded scope, in this case set off from the rest of the file by curly braces.</span></span>

<span data-ttu-id="c2c17-159">`&`語法是使用較少的選取器功能，與代表目前的選取器父系。</span><span class="sxs-lookup"><span data-stu-id="c2c17-159">The `&` syntax is a Less selector feature, with & representing the current selector parent.</span></span> <span data-ttu-id="c2c17-160">因此，在 {...}</span><span class="sxs-lookup"><span data-stu-id="c2c17-160">So, within the a {...}</span></span> <span data-ttu-id="c2c17-161">區塊中，`&`代表`a`標記，因此`&:link`相當於`a:link`。</span><span class="sxs-lookup"><span data-stu-id="c2c17-161">block, `&` represents an `a` tag, and thus `&:link` is equivalent to `a:link`.</span></span>

<span data-ttu-id="c2c17-162">在建立回應式設計中非常實用的媒體查詢也可能導致 CSS 中的大量重複項與複雜度。</span><span class="sxs-lookup"><span data-stu-id="c2c17-162">Media queries, extremely useful in creating responsive designs, can also contribute heavily to repetition and complexity in CSS.</span></span> <span data-ttu-id="c2c17-163">Less 允許媒體查詢在類別中放在巢狀結構中，因此整個類別定義不需要在不同的頂層 `@media` 元素中重複。</span><span class="sxs-lookup"><span data-stu-id="c2c17-163">Less allows media queries to be nested within classes, so that the entire class definition doesn't need to be repeated within different top-level `@media` elements.</span></span> <span data-ttu-id="c2c17-164">例如，以下是回應式功能表的 CSS：</span><span class="sxs-lookup"><span data-stu-id="c2c17-164">For example, here is CSS for a responsive menu:</span></span>

```css
.navigation {
    margin-top: 30%;
    width: 100%;
}
@media screen and (min-width: 40em) {
    .navigation {
        margin: 0;
    }
}
@media screen and (min-width: 62em) {
    .navigation {
        width: 960px;
        margin: 0;
    }
}
```

<span data-ttu-id="c2c17-165">這可以在 Less 內進一步定義為：</span><span class="sxs-lookup"><span data-stu-id="c2c17-165">This can be better defined in Less as:</span></span>

```less
.navigation {
    margin-top: 30%;
    width: 100%;
    @media screen and (min-width: 40em) {
        margin: 0;
    }
    @media screen and (min-width: 62em) {
        width: 960px;
        margin: 0;
    }
}
```

<span data-ttu-id="c2c17-166">我們已經看過的另一個 Less 功能是它支援數學運算，允許從預先定義的變數建構樣式屬性。</span><span class="sxs-lookup"><span data-stu-id="c2c17-166">Another feature of Less that we have already seen is its support for mathematical operations, allowing style attributes to be constructed from pre-defined variables.</span></span> <span data-ttu-id="c2c17-167">這使得更新相關的樣式更容易，因為只要修改基底變數就可以讓所有相依值自動變更。</span><span class="sxs-lookup"><span data-stu-id="c2c17-167">This makes updating related styles much easier, since the base variable can be modified and all dependent values change automatically.</span></span>

<span data-ttu-id="c2c17-168">CSS 檔案，特別是針對大型網站  (而且特別是如果使用媒體查詢)，在經過一段時間之後會變得相當大，造成使用上的不便。</span><span class="sxs-lookup"><span data-stu-id="c2c17-168">CSS files, especially for large sites (and especially if media queries are being used), tend to get quite large over time, making working with them unwieldy.</span></span> <span data-ttu-id="c2c17-169">您可以分開定義多個 Less 檔案，然後使用 `@import` 指示詞合併。</span><span class="sxs-lookup"><span data-stu-id="c2c17-169">Less files can be defined separately, then pulled together using `@import` directives.</span></span> <span data-ttu-id="c2c17-170">如果有需要，Less 也可以用來匯入個別 CSS 檔案。</span><span class="sxs-lookup"><span data-stu-id="c2c17-170">Less can also be used to import individual CSS files, as well, if desired.</span></span>

<span data-ttu-id="c2c17-171">*Mixins* 可以接受參數，而且 Less 支援 mixin 成立條件形式的條件式邏輯，這提供宣告式方式來定義特定 mixins 何時生效。</span><span class="sxs-lookup"><span data-stu-id="c2c17-171">*Mixins* can accept parameters, and Less supports conditional logic in the form of mixin guards, which provide a declarative way to define when certain mixins take effect.</span></span> <span data-ttu-id="c2c17-172">mixin 成立條件的常見用途是根據來源色彩的深淺度來調整色彩。</span><span class="sxs-lookup"><span data-stu-id="c2c17-172">A common use for mixin guards is to adjust colors based on how light or dark the source color is.</span></span> <span data-ttu-id="c2c17-173">在給定一個可接受參數之  mixin 的情況下，mixin 成立條件可以用來根據該色彩修改 mixin：</span><span class="sxs-lookup"><span data-stu-id="c2c17-173">Given a mixin that accepts a parameter for color, a mixin guard can be used to modify the mixin based on that color:</span></span>

```less
.box (@color) when (lightness(@color) >= 50%) {
    background-color: #000;
}
.box (@color) when (lightness(@color) < 50%) {
    background-color: #FFF;
}
.box (@color) {
    color: @color;
}

.feature {
    .box (@base);
}
```

<span data-ttu-id="c2c17-174">假設我們目前`@base`的值`#663333`，此較少的指令碼會產生下列 CSS:</span><span class="sxs-lookup"><span data-stu-id="c2c17-174">Given our current `@base` value of `#663333`, this Less script will produce the following CSS:</span></span>

```css
.feature {
    background-color: #FFF;
    color: #663333;
}
```

<span data-ttu-id="c2c17-175">Less 提供一些其他功能，但以上內容應該能讓您了解這個前置處理語言的一些概念。</span><span class="sxs-lookup"><span data-stu-id="c2c17-175">Less provides a number of additional features, but this should give you some idea of the power of this preprocessing language.</span></span>

## <a name="sass"></a><span data-ttu-id="c2c17-176">Sass</span><span class="sxs-lookup"><span data-stu-id="c2c17-176">Sass</span></span>

<span data-ttu-id="c2c17-177">Sass 是類似於以下，提供許多相同的功能，但語法稍有不同的支援。</span><span class="sxs-lookup"><span data-stu-id="c2c17-177">Sass is similar to Less, providing support for many of the same features, but with slightly different syntax.</span></span> <span data-ttu-id="c2c17-178">它建置使用 Ruby，而不是 JavaScript，並因此會有不同的安裝需求。</span><span class="sxs-lookup"><span data-stu-id="c2c17-178">It's built using Ruby, rather than JavaScript, and so has different setup requirements.</span></span> <span data-ttu-id="c2c17-179">原始的 Sass 語言並未使用大括號或分號分隔，而定義使用空白字元和縮排的範圍。</span><span class="sxs-lookup"><span data-stu-id="c2c17-179">The original Sass language didn't use curly braces or semicolons, but instead defined scope using white space and indentation.</span></span> <span data-ttu-id="c2c17-180">Sass 版本 3，引進了一種新語法， **SCSS** ("Sassy CSS")。</span><span class="sxs-lookup"><span data-stu-id="c2c17-180">In version 3 of Sass, a new syntax was introduced, **SCSS** ("Sassy CSS").</span></span> <span data-ttu-id="c2c17-181">SCSS 是類似於 CSS，在於它會忽略縮排層級和空白字元，並改為使用分號和大括號。</span><span class="sxs-lookup"><span data-stu-id="c2c17-181">SCSS is similar to CSS in that it ignores indentation levels and whitespace, and instead uses semicolons and curly braces.</span></span>

<span data-ttu-id="c2c17-182">若要安裝 Sass，通常您會先安裝 Ruby （預先安裝在 macOS 上），，然後執行：</span><span class="sxs-lookup"><span data-stu-id="c2c17-182">To install Sass, typically you would first install Ruby (pre-installed on macOS), and then run:</span></span>

```console
gem install sass
```

<span data-ttu-id="c2c17-183">不過，如果您執行 Visual Studio，開始使用 Sass 大致就像開始使用 Less 一樣。</span><span class="sxs-lookup"><span data-stu-id="c2c17-183">However, if you're running Visual Studio, you can get started with Sass in much the same way as you would with Less.</span></span> <span data-ttu-id="c2c17-184">開啟 *package.json* 並將 "gulp sass" 套件新增到 `devDependencies`：</span><span class="sxs-lookup"><span data-stu-id="c2c17-184">Open *package.json* and add the "gulp-sass" package to `devDependencies`:</span></span>

```json
"devDependencies": {
  "gulp": "3.9.1",
  "gulp-less": "3.3.0",
  "gulp-sass": "3.1.0"
}
```

<span data-ttu-id="c2c17-185">接下來，修改*gulpfile.js*加入 sass 變數和 Sass 檔案編譯，並將結果放在 [wwwroot] 資料夾中的工作：</span><span class="sxs-lookup"><span data-stu-id="c2c17-185">Next, modify *gulpfile.js* to add a sass variable and a task to compile your Sass files and place the results in the wwwroot folder:</span></span>

```javascript
var gulp = require("gulp"),
  fs = require("fs"),
  less = require("gulp-less"),
  sass = require("gulp-sass");

// other content removed

gulp.task("sass", function () {
  return gulp.src('Styles/main2.scss')
    .pipe(sass())
    .pipe(gulp.dest('wwwroot/css'));
});
```

<span data-ttu-id="c2c17-186">現在您可以將 Sass 檔案 *main2.scss* 加入到專案根目錄的 *Style* 資料夾中：</span><span class="sxs-lookup"><span data-stu-id="c2c17-186">Now you can add the Sass file *main2.scss* to the *Styles* folder in the root of the project:</span></span>

![新增 scss 檔案](less-sass-fa/_static/add-scss-file.png)

<span data-ttu-id="c2c17-188">開啟 *main2.scss* 並加入下列內容：</span><span class="sxs-lookup"><span data-stu-id="c2c17-188">Open *main2.scss* and add the following:</span></span>

```sass
$base: #CC0000;
body {
    background-color: $base;
}
```

<span data-ttu-id="c2c17-189">儲存所有檔案。</span><span class="sxs-lookup"><span data-stu-id="c2c17-189">Save all of your files.</span></span> <span data-ttu-id="c2c17-190">現在當您重新整理**Task Runner Explorer**，您會看到`sass`工作。</span><span class="sxs-lookup"><span data-stu-id="c2c17-190">Now when you refresh **Task Runner Explorer**, you see a `sass` task.</span></span> <span data-ttu-id="c2c17-191">執行它，然後查看 */wwwroot/css*資料夾。</span><span class="sxs-lookup"><span data-stu-id="c2c17-191">Run it, and look in the */wwwroot/css* folder.</span></span> <span data-ttu-id="c2c17-192">目前沒有*main2.css*檔案，使用下列內容：</span><span class="sxs-lookup"><span data-stu-id="c2c17-192">There's now a *main2.css* file, with these contents:</span></span>

```css
body {
    background-color: #CC0000;
}
```

<span data-ttu-id="c2c17-193">Sass 對巢狀的支援大致與 Less 相同。</span><span class="sxs-lookup"><span data-stu-id="c2c17-193">Sass supports nesting in much the same was that Less does, providing similar benefits.</span></span> <span data-ttu-id="c2c17-194">檔案可依功能分割，並使用 `@import` 指示詞來包含：</span><span class="sxs-lookup"><span data-stu-id="c2c17-194">Files can be split up by function and included using the `@import` directive:</span></span>

```sass
@import 'anotherfile';
```

<span data-ttu-id="c2c17-195">Sass 支援 mixin，使用`@mixin`加以定義的關鍵字和`@include`來包含它們從如此範例所示[sass lang.com](http://sass-lang.com):</span><span class="sxs-lookup"><span data-stu-id="c2c17-195">Sass supports mixins as well, using the `@mixin` keyword to define them and `@include` to include them, as in this example from [sass-lang.com](http://sass-lang.com):</span></span>

```sass
@mixin border-radius($radius) {
    -webkit-border-radius: $radius;
    -moz-border-radius: $radius;
    -ms-border-radius: $radius;
    border-radius: $radius;
}

.box { @include border-radius(10px); }
```

<span data-ttu-id="c2c17-196">Mixin，除了 Sass 也支援繼承的概念可讓擴充另一個類別。</span><span class="sxs-lookup"><span data-stu-id="c2c17-196">In addition to mixins, Sass also supports the concept of inheritance, allowing one class to extend another.</span></span> <span data-ttu-id="c2c17-197">就概念上類似於 mixin，但在較少的 CSS 程式碼所產生的結果。</span><span class="sxs-lookup"><span data-stu-id="c2c17-197">It's conceptually similar to a mixin, but results in less CSS code.</span></span> <span data-ttu-id="c2c17-198">它會藉由`@extend`關鍵字。</span><span class="sxs-lookup"><span data-stu-id="c2c17-198">It's accomplished using the `@extend` keyword.</span></span> <span data-ttu-id="c2c17-199">若要試用 mixin，將下列內容加入您*main2.scss*檔案：</span><span class="sxs-lookup"><span data-stu-id="c2c17-199">To try out mixins, add the following to your *main2.scss* file:</span></span>

```sass
@mixin alert {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    @include alert;
    border-color: green;
}

.error {
    @include alert;
    color: red;
    border-color: red;
    font-weight:bold;
}
```

<span data-ttu-id="c2c17-200">檢查中的輸出*main2.css*開始執行之後`sass`中的工作**Task Runner Explorer**:</span><span class="sxs-lookup"><span data-stu-id="c2c17-200">Examine the output in *main2.css* after running the `sass` task in **Task Runner Explorer**:</span></span>

```css
.success {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
    border-color: green;
 }

.error {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
    color: red;
    border-color: red;
    font-weight: bold;
}
```

<span data-ttu-id="c2c17-201">請注意，所有警示的 mixin 的通用屬性會重複在每個類別。</span><span class="sxs-lookup"><span data-stu-id="c2c17-201">Notice that all of the common properties of the alert mixin are repeated in each class.</span></span> <span data-ttu-id="c2c17-202">Mixin 很好的協助消除重複資料刪除在開發階段，但它仍在建立 CSS 具有大量重複資料刪除，導致超過所需的 CSS 檔案-潛在的效能問題。</span><span class="sxs-lookup"><span data-stu-id="c2c17-202">The mixin did a good job of helping eliminate duplication at development time, but it's still creating CSS with a lot of duplication in it, resulting in larger than necessary CSS files - a potential performance issue.</span></span>

<span data-ttu-id="c2c17-203">現在將使用警示的 mixin`.alert`類別，並變更`@include`要`@extend`(記住擴充`.alert`，而非`alert`):</span><span class="sxs-lookup"><span data-stu-id="c2c17-203">Now replace the alert mixin with a `.alert` class, and change `@include` to `@extend` (remembering to extend `.alert`, not `alert`):</span></span>

```sass
.alert {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    @extend .alert;
    border-color: green;
}

.error {
    @extend .alert;
    color: red;
    border-color: red;
    font-weight:bold;
}
```

<span data-ttu-id="c2c17-204">同樣地，執行 Sass，並檢查產生的 CSS:</span><span class="sxs-lookup"><span data-stu-id="c2c17-204">Run Sass once more, and examine the resulting CSS:</span></span>

```css
.alert, .success, .error {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    border-color: green;
}

.error {
    color: red;
    border-color: red;
    font-weight: bold;
}
```

<span data-ttu-id="c2c17-205">現在只要視需要多次定義的屬性和 CSS 會產生更好。</span><span class="sxs-lookup"><span data-stu-id="c2c17-205">Now the properties are defined only as many times as needed, and better CSS is generated.</span></span>

<span data-ttu-id="c2c17-206">Sass 也包含函式與條件式邏輯作業，類似於 Less。</span><span class="sxs-lookup"><span data-stu-id="c2c17-206">Sass also includes functions and conditional logic operations, similar to Less.</span></span> <span data-ttu-id="c2c17-207">事實上，這兩種語言的功能非常類似。</span><span class="sxs-lookup"><span data-stu-id="c2c17-207">In fact, the two languages' capabilities are very similar.</span></span>

## <a name="less-or-sass"></a><span data-ttu-id="c2c17-208">Less 或 Sass？</span><span class="sxs-lookup"><span data-stu-id="c2c17-208">Less or Sass?</span></span>

<span data-ttu-id="c2c17-209">使用 Less 或 sass (或甚至是建議使用原始 Sass 嘿 SaaS 內較新的 SCSS 語法) 並無共識。</span><span class="sxs-lookup"><span data-stu-id="c2c17-209">There's still no consensus as to whether it's generally better to use Less or Sass (or even whether to prefer the original Sass or the newer SCSS syntax within Sass).</span></span> <span data-ttu-id="c2c17-210">最重要的決策可能是**使用這些工具的其中一個**，而不是手動撰寫 CSS 檔案程式碼。</span><span class="sxs-lookup"><span data-stu-id="c2c17-210">Probably the most important decision is to **use one of these tools**, as opposed to just hand-coding your CSS files.</span></span> <span data-ttu-id="c2c17-211">一旦您做出該決策，Less 與 Sass 都是很好的選擇。</span><span class="sxs-lookup"><span data-stu-id="c2c17-211">Once you've made that decision, both Less and Sass are good choices.</span></span>

## <a name="font-awesome"></a><span data-ttu-id="c2c17-212">Font Awesome</span><span class="sxs-lookup"><span data-stu-id="c2c17-212">Font Awesome</span></span>

<span data-ttu-id="c2c17-213">除了 CSS 前置處理器，樣式現代化 web 應用程式的另一個絕佳的資源則是 Font Awesome 項目。</span><span class="sxs-lookup"><span data-stu-id="c2c17-213">In addition to CSS preprocessors, another great resource for styling modern web applications is Font Awesome.</span></span> <span data-ttu-id="c2c17-214">字型棒了是可提供 500 多個可縮放向量圖示可以自由使用您的 web 應用程式中的工具組。</span><span class="sxs-lookup"><span data-stu-id="c2c17-214">Font Awesome is a toolkit that provides over 500 scalable vector icons that can be freely used in your web applications.</span></span> <span data-ttu-id="c2c17-215">它原本設計為可使用啟動程序，但是它不相依任何 JavaScript 程式庫或該架構上。</span><span class="sxs-lookup"><span data-stu-id="c2c17-215">It was originally designed to work with Bootstrap, but it has no dependency on that framework or on any JavaScript libraries.</span></span>

<span data-ttu-id="c2c17-216">若要開始使用 Font Awesome 最簡單的方式是加入參考，所以使用其公開金鑰的內容傳遞網路 (CDN) 的位置：</span><span class="sxs-lookup"><span data-stu-id="c2c17-216">The easiest way to get started with Font Awesome is to add a reference to it, using its public content delivery network (CDN) location:</span></span>

```html
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">
```

<span data-ttu-id="c2c17-217">您可以也將它新增至您的 Visual Studio 專案藉由將 「 相依性 」 中*bower.json*:</span><span class="sxs-lookup"><span data-stu-id="c2c17-217">You can also add it to your Visual Studio project by adding it to the "dependencies" in *bower.json*:</span></span>

```json
{
  "name": "ASP.NET",
  "private": true,
  "dependencies": {
    "bootstrap": "3.0.0",
    "jquery": "1.10.2",
    "jquery-validation": "1.11.1",
    "jquery-validation-unobtrusive": "3.2.2",
    "hammer.js": "2.0.4",
    "bootstrap-touch-carousel": "0.8.0",
    "Font-Awesome": "4.3.0"
  }
}
```

<span data-ttu-id="c2c17-218">一旦您有參照 Font Awesome 頁面上的，您可以將圖示加入至您的應用程式藉由套用 Font Awesome 類別，通常是加上"fa-"，以您的內嵌 HTML 項目 (例如`<span>`或`<i>`)。</span><span class="sxs-lookup"><span data-stu-id="c2c17-218">Once you have a reference to Font Awesome on a page, you can add icons to your application by applying Font Awesome classes, typically prefixed with "fa-", to your inline HTML elements (such as `<span>` or `<i>`).</span></span>  <span data-ttu-id="c2c17-219">比方說，您也可以將圖示加入至簡單的清單和類似的程式碼的功能表：</span><span class="sxs-lookup"><span data-stu-id="c2c17-219">For example, you can add icons to simple lists and menus using code like this:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title></title>
    <link href="lib/font-awesome/css/font-awesome.css" rel="stylesheet" />
</head>
<body>
    <ul class="fa-ul">
        <li><i class="fa fa-li fa-home"></i> Home</li>
        <li><i class="fa fa-li fa-cog"></i> Settings</li>
    </ul>
</body>
</html>
```

<span data-ttu-id="c2c17-220">這會產生下列瀏覽器中的-請注意每個項目旁的圖示：</span><span class="sxs-lookup"><span data-stu-id="c2c17-220">This produces the following in the browser - note the icon beside each item:</span></span>

![清單圖示](less-sass-fa/_static/list-icons-screenshot.png)

<span data-ttu-id="c2c17-222">您可以檢視可用的圖示的完整清單：</span><span class="sxs-lookup"><span data-stu-id="c2c17-222">You can view a complete list of the available icons here:</span></span>

http://fontawesome.io/icons/

## <a name="summary"></a><span data-ttu-id="c2c17-223">總結</span><span class="sxs-lookup"><span data-stu-id="c2c17-223">Summary</span></span>

<span data-ttu-id="c2c17-224">現代化 web 應用程式越來越要求回應迅速、 流暢的設計是全新、 直覺式且容易使用各式各樣的裝置。</span><span class="sxs-lookup"><span data-stu-id="c2c17-224">Modern web applications increasingly demand responsive, fluid designs that are clean, intuitive, and easy to use from a variety of devices.</span></span> <span data-ttu-id="c2c17-225">最適合進行管理複雜的達成這些目標所需的 CSS 樣式表，較不使用的前置處理器的按讚或 Sass。</span><span class="sxs-lookup"><span data-stu-id="c2c17-225">Managing the complexity of the CSS stylesheets required to achieve these goals is best done using a preprocessor like Less or Sass.</span></span> <span data-ttu-id="c2c17-226">此外，工具組，例如 Font Awesome 快速提供已知的圖示，以文字巡覽功能表和按鈕，改善整體使用者體驗您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2c17-226">In addition, toolkits like Font Awesome quickly provide well-known icons to textual navigation menus and buttons, improving the overall user experience of your application.</span></span>
