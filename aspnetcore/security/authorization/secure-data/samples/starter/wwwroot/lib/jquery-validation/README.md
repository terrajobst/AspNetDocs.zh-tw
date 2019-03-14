---
ms.openlocfilehash: 83a958fe6a8d61becf9f9062e8ad0ff69108b435
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57034985"
---
<a name="jquery-validation-pluginhttpjqueryvalidationorg---form-validation-made-easy"></a>[jQuery 驗證外掛程式](http://jqueryvalidation.org/) - 表單驗證變得更容易
================================

[![組建狀態](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency 狀態](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)

儘管使所有種類的自訂項目符合您的應用程式真的很簡單，但 jQuery 驗證外掛程式會為您的現有表單提供插入驗證。

## <a name="help-the-projecthttppledgiecomcampaigns18159"></a>[為專案提供協助](http://pledgie.com/campaigns/18159) \(英文\)

[![為專案提供協助](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)

這個專案需要協助！ [您可以捐贈給持續進行的 Pledgie 活動](http://pledgie.com/campaigns/18159) \(英文\)，並協助傳播這個訊息。 如果您曾經使用此外掛程式或計劃要使用它，請考慮進行捐贈：任何金額都很有助益。

您可以在 [Pledgie 頁面](http://pledgie.com/campaigns/18159) \(英文\) 上找到關於如何使用這筆費用的計劃。

## <a name="getting-started"></a>快速入門

### <a name="downloading-the-prebuilt-files"></a>下載預先建置的檔案

預先建置的檔案可從下列位置下載： http://jqueryvalidation.org/

### <a name="downloading-the-latest-changes"></a>下載最新變更

您可以使用下列方式來取得尚未發行的開發檔案：

 1. [下載](https://github.com/jzaefferer/jquery-validation/archive/master.zip)或派生 (fork) 此存放庫
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

如需如何設定規則和自訂項目的詳細資訊，請[參閱文件](http://jqueryvalidation.org/documentation/) \(英文\)。

## <a name="reporting-issues-and-contributing-code"></a>回報問題並貢獻程式碼

如需詳細資訊，請參閱[貢獻方針](CONTRIBUTING.md)。

**與電子郵件驗證有關的重要注意事項**。 截至 1.12.0 版本，此外掛程式會使用 [HTML5 規格所建議瀏覽器使用](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address) \(英文\) 的同一種規則運算式。 我們將跟隨他們的領導並使用相同檢查。 如果您認為規格有誤，請將問題回報給他們。 如果您有不同需求，請考慮[使用自訂方法](http://jqueryvalidation.org/jQuery.validator.addMethod/) \(英文\)。

## <a name="license"></a>使用權
著作權 &copy; Jörn Zaefferer<br>
根據 MIT 授權進行授權。
