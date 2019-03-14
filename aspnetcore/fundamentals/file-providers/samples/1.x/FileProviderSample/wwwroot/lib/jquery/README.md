---
ms.openlocfilehash: 610b16b181422978dc143b95f28658bbdf177fdd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028275"
---
# <a name="jquery"></a>jQuery

> jQuery 是快速、小型且功能豐富的 JavaScript 程式庫。

如需有關如何開始及如何使用 jQuery 的相關資訊，請參閱 [jQuery 的文件](http://api.jquery.com/) \(英文\)。
如需原始程式檔或有任何問題，請瀏覽 [jQuery 存放庫](https://github.com/jquery/jquery) \(英文\)。

若要升級，請參閱 [3.3.1 的部落格文章](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/) \(英文\)。 這包括與舊版相比最大的差異，以及可讀性更高的變更記錄。

## <a name="including-jquery"></a>包括 jQuery

以下是包括 jQuery 最常用的一些方式。

### <a name="browser"></a>瀏覽器

#### <a name="script-tag"></a>指令碼標記

```html
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
```

#### <a name="babel"></a>Babel

[Babel](http://babeljs.io/) 是新一代的 JavaScript 編譯器。 其中一個功能是現在可以使用 ES6/ES2015 模組，雖然瀏覽器原生還沒支援此功能。

```js
import $ from "jquery";
```

#### <a name="browserifywebpack"></a>Browserify/Webpack

有一些方式可以使用 [Browserify](http://browserify.org/) 與 [Webpack](https://webpack.github.io/)。 如需有關如何使用這些工具的詳細資訊，請參閱對應之專案的文件。 在指令碼中，包括 jQuery 通常看起來像這樣...

```js
var $ = require("jquery");
```

#### <a name="amd-asynchronous-module-definition"></a>AMD (非同步模組定義)

AMD 是針對瀏覽器建置的模組格式。 如需詳細資訊，我們建議您閱讀 [require.js 的文件](http://requirejs.org/docs/whyamd.html) \(英文\)。

```js
define(["jquery"], function($) {

});
```

### <a name="node"></a>節點

若要將 jQuery 包括在[節點](nodejs.org)中，請先使用 npm 來安裝。

```sh
npm install jquery
```

為讓 jQuery 在節點中運作，需要一個具有文件的視窗。 因為節點中原生沒有此類視窗存在，您可以使用諸如 [jsdom](https://github.com/tmpvar/jsdom) 的工具來模擬一個視窗。 這對測試用途來講非常實用。

```js
require("jsdom").env("", function(err, window) {
    if (err) {
        console.error(err);
        return;
    }

    var $ = require("jquery")(window);
});
```
