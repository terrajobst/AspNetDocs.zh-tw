---
ms.openlocfilehash: 610b16b181422978dc143b95f28658bbdf177fdd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028275"
---
# <a name="jquery"></a><span data-ttu-id="08d04-101">jQuery</span><span class="sxs-lookup"><span data-stu-id="08d04-101">jQuery</span></span>

> <span data-ttu-id="08d04-102">jQuery 是快速、小型且功能豐富的 JavaScript 程式庫。</span><span class="sxs-lookup"><span data-stu-id="08d04-102">jQuery is a fast, small, and feature-rich JavaScript library.</span></span>

<span data-ttu-id="08d04-103">如需有關如何開始及如何使用 jQuery 的相關資訊，請參閱 [jQuery 的文件](http://api.jquery.com/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="08d04-103">For information on how to get started and how to use jQuery, please see [jQuery's documentation](http://api.jquery.com/).</span></span>
<span data-ttu-id="08d04-104">如需原始程式檔或有任何問題，請瀏覽 [jQuery 存放庫](https://github.com/jquery/jquery) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="08d04-104">For source files and issues, please visit the [jQuery repo](https://github.com/jquery/jquery).</span></span>

<span data-ttu-id="08d04-105">若要升級，請參閱 [3.3.1 的部落格文章](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="08d04-105">If upgrading, please see the [blog post for 3.3.1](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/).</span></span> <span data-ttu-id="08d04-106">這包括與舊版相比最大的差異，以及可讀性更高的變更記錄。</span><span class="sxs-lookup"><span data-stu-id="08d04-106">This includes notable differences from the previous version and a more readable changelog.</span></span>

## <a name="including-jquery"></a><span data-ttu-id="08d04-107">包括 jQuery</span><span class="sxs-lookup"><span data-stu-id="08d04-107">Including jQuery</span></span>

<span data-ttu-id="08d04-108">以下是包括 jQuery 最常用的一些方式。</span><span class="sxs-lookup"><span data-stu-id="08d04-108">Below are some of the most common ways to include jQuery.</span></span>

### <a name="browser"></a><span data-ttu-id="08d04-109">瀏覽器</span><span class="sxs-lookup"><span data-stu-id="08d04-109">Browser</span></span>

#### <a name="script-tag"></a><span data-ttu-id="08d04-110">指令碼標記</span><span class="sxs-lookup"><span data-stu-id="08d04-110">Script tag</span></span>

```html
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
```

#### <a name="babel"></a><span data-ttu-id="08d04-111">Babel</span><span class="sxs-lookup"><span data-stu-id="08d04-111">Babel</span></span>

<span data-ttu-id="08d04-112">[Babel](http://babeljs.io/) 是新一代的 JavaScript 編譯器。</span><span class="sxs-lookup"><span data-stu-id="08d04-112">[Babel](http://babeljs.io/) is a next generation JavaScript compiler.</span></span> <span data-ttu-id="08d04-113">其中一個功能是現在可以使用 ES6/ES2015 模組，雖然瀏覽器原生還沒支援此功能。</span><span class="sxs-lookup"><span data-stu-id="08d04-113">One of the features is the ability to use ES6/ES2015 modules now, even though browsers do not yet support this feature natively.</span></span>

```js
import $ from "jquery";
```

#### <a name="browserifywebpack"></a><span data-ttu-id="08d04-114">Browserify/Webpack</span><span class="sxs-lookup"><span data-stu-id="08d04-114">Browserify/Webpack</span></span>

<span data-ttu-id="08d04-115">有一些方式可以使用 [Browserify](http://browserify.org/) 與 [Webpack](https://webpack.github.io/)。</span><span class="sxs-lookup"><span data-stu-id="08d04-115">There are several ways to use [Browserify](http://browserify.org/) and [Webpack](https://webpack.github.io/).</span></span> <span data-ttu-id="08d04-116">如需有關如何使用這些工具的詳細資訊，請參閱對應之專案的文件。</span><span class="sxs-lookup"><span data-stu-id="08d04-116">For more information on using these tools, please refer to the corresponding project's documention.</span></span> <span data-ttu-id="08d04-117">在指令碼中，包括 jQuery 通常看起來像這樣...</span><span class="sxs-lookup"><span data-stu-id="08d04-117">In the script, including jQuery will usually look like this...</span></span>

```js
var $ = require("jquery");
```

#### <a name="amd-asynchronous-module-definition"></a><span data-ttu-id="08d04-118">AMD (非同步模組定義)</span><span class="sxs-lookup"><span data-stu-id="08d04-118">AMD (Asynchronous Module Definition)</span></span>

<span data-ttu-id="08d04-119">AMD 是針對瀏覽器建置的模組格式。</span><span class="sxs-lookup"><span data-stu-id="08d04-119">AMD is a module format built for the browser.</span></span> <span data-ttu-id="08d04-120">如需詳細資訊，我們建議您閱讀 [require.js 的文件](http://requirejs.org/docs/whyamd.html) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="08d04-120">For more information, we recommend [require.js' documentation](http://requirejs.org/docs/whyamd.html).</span></span>

```js
define(["jquery"], function($) {

});
```

### <a name="node"></a><span data-ttu-id="08d04-121">節點</span><span class="sxs-lookup"><span data-stu-id="08d04-121">Node</span></span>

<span data-ttu-id="08d04-122">若要將 jQuery 包括在[節點](nodejs.org)中，請先使用 npm 來安裝。</span><span class="sxs-lookup"><span data-stu-id="08d04-122">To include jQuery in [Node](nodejs.org), first install with npm.</span></span>

```sh
npm install jquery
```

<span data-ttu-id="08d04-123">為讓 jQuery 在節點中運作，需要一個具有文件的視窗。</span><span class="sxs-lookup"><span data-stu-id="08d04-123">For jQuery to work in Node, a window with a document is required.</span></span> <span data-ttu-id="08d04-124">因為節點中原生沒有此類視窗存在，您可以使用諸如 [jsdom](https://github.com/tmpvar/jsdom) 的工具來模擬一個視窗。</span><span class="sxs-lookup"><span data-stu-id="08d04-124">Since no such window exists natively in Node, one can be mocked by tools such as [jsdom](https://github.com/tmpvar/jsdom).</span></span> <span data-ttu-id="08d04-125">這對測試用途來講非常實用。</span><span class="sxs-lookup"><span data-stu-id="08d04-125">This can be useful for testing purposes.</span></span>

```js
require("jsdom").env("", function(err, window) {
    if (err) {
        console.error(err);
        return;
    }

    var $ = require("jquery")(window);
});
```
