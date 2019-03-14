---
ms.openlocfilehash: 24c36493284988aa45b15c78e2577c0ef96aba56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029985"
---
<a name="jquery-validation-pluginhttpsjqueryvalidationorg---form-validation-made-easy"></a>[jQuery 驗證外掛程式](https://jqueryvalidation.org/) - 表單驗證變得更容易
================================

[![組建狀態](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![devDependency 狀態](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)

儘管使所有種類的自訂項目符合您的應用程式真的很簡單，但 jQuery 驗證外掛程式會為您的現有表單提供插入驗證。

## <a name="getting-started"></a>快速入門

### <a name="downloading-the-prebuilt-files"></a>下載預先建置的檔案

預先建置的檔案可從下列位置下載： https://jqueryvalidation.org/

### <a name="downloading-the-latest-changes"></a>下載最新變更

您可以使用下列方式來取得尚未發行的開發檔案：

 1. [下載](https://github.com/jquery-validation/jquery-validation/archive/master.zip)或派生 (fork) 此存放庫
 2. [設定組建](CONTRIBUTING.md#build-setup)
 3. 執行 `grunt`，在 "dist" 目錄中建立組建檔

### <a name="including-it-on-your-page"></a>在您的頁面上包括該檔案

在頁面上包括 jQuery 和外掛程式。 然後選取表單來驗證並呼叫 `validate` 方法。

```html
<form>
    <input required>
</form>
<script src="jquery.js"></script>
<script src="jquery.validate.js"></script>
<script>
$("form").validate();
</script>
```

或者，透過模組中的 requirejs 來包括 jQuery 和外掛程式。

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

如需如何設定規則和自訂項目的詳細資訊，請[參閱文件](https://jqueryvalidation.org/documentation/) \(英文\)。

## <a name="reporting-issues-and-contributing-code"></a>回報問題並貢獻程式碼

如需詳細資訊，請參閱[貢獻方針](CONTRIBUTING.md)。

**與電子郵件驗證有關的重要注意事項**。 截至 1.12.0 版本，此外掛程式會使用 [HTML5 規格所建議瀏覽器使用](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address) \(英文\) 的同一種規則運算式。 我們將跟隨他們的領導並使用相同檢查。 如果您認為規格有誤，請將問題回報給他們。 如果您有不同需求，請考慮[使用自訂方法](https://jqueryvalidation.org/jQuery.validator.addMethod/) \(英文\)。
若需要調整內建的驗證規則運算式模式，請[依照文件](https://jqueryvalidation.org/jQuery.validator.methods/)。

**有關必要方法的重要注意事項**。 在 1.14.0 版之後，此外掛程式停止修剪附加元素值中的空格。 若要達到相同的結果，您可以使用 [`normalizer`](https://jqueryvalidation.org/normalizer/)，這可以用來在驗證之前轉換元素值。 此功能從 `v1.15.0` 開始就存在。 換句話說，您可以執行如下動作：
``` js
$("#myForm").validate({
    rules: {
        username: {
            required: true,
            // Using the normalizer to trim the value of the element
            // before validating it.
            //
            // The value of `this` inside the `normalizer` is the corresponding
            // DOMElement. In this example, `this` references the `username` element.
            normalizer: function(value) {
                return $.trim(value);
            }
        }
    }
});
```

## <a name="license"></a>使用權
著作權 &copy; Jörn Zaefferer<br>
根據 MIT 授權進行授權。
