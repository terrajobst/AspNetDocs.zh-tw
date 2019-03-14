---
ms.openlocfilehash: 24c36493284988aa45b15c78e2577c0ef96aba56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029985"
---
<a name="jquery-validation-pluginhttpsjqueryvalidationorg---form-validation-made-easy"></a><span data-ttu-id="f2bea-101">[jQuery 驗證外掛程式](https://jqueryvalidation.org/) - 表單驗證變得更容易</span><span class="sxs-lookup"><span data-stu-id="f2bea-101">[jQuery Validation Plugin](https://jqueryvalidation.org/) - Form validation made easy</span></span>
================================

<span data-ttu-id="f2bea-102">[![組建狀態](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![devDependency 狀態](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)</span><span class="sxs-lookup"><span data-stu-id="f2bea-102">[![Build Status](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![devDependency Status](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)</span></span>

<span data-ttu-id="f2bea-103">儘管使所有種類的自訂項目符合您的應用程式真的很簡單，但 jQuery 驗證外掛程式會為您的現有表單提供插入驗證。</span><span class="sxs-lookup"><span data-stu-id="f2bea-103">The jQuery Validation Plugin provides drop-in validation for your existing forms, while making all kinds of customizations to fit your application really easy.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f2bea-104">快速入門</span><span class="sxs-lookup"><span data-stu-id="f2bea-104">Getting Started</span></span>

### <a name="downloading-the-prebuilt-files"></a><span data-ttu-id="f2bea-105">下載預先建置的檔案</span><span class="sxs-lookup"><span data-stu-id="f2bea-105">Downloading the prebuilt files</span></span>

<span data-ttu-id="f2bea-106">預先建置的檔案可從下列位置下載： https://jqueryvalidation.org/</span><span class="sxs-lookup"><span data-stu-id="f2bea-106">Prebuilt files can be downloaded from https://jqueryvalidation.org/</span></span>

### <a name="downloading-the-latest-changes"></a><span data-ttu-id="f2bea-107">下載最新變更</span><span class="sxs-lookup"><span data-stu-id="f2bea-107">Downloading the latest changes</span></span>

<span data-ttu-id="f2bea-108">您可以使用下列方式來取得尚未發行的開發檔案：</span><span class="sxs-lookup"><span data-stu-id="f2bea-108">The unreleased development files can be obtained by:</span></span>

 1. <span data-ttu-id="f2bea-109">[下載](https://github.com/jquery-validation/jquery-validation/archive/master.zip)或派生 (fork) 此存放庫</span><span class="sxs-lookup"><span data-stu-id="f2bea-109">[Downloading](https://github.com/jquery-validation/jquery-validation/archive/master.zip) or Forking this repository</span></span>
 2. [<span data-ttu-id="f2bea-110">設定組建</span><span class="sxs-lookup"><span data-stu-id="f2bea-110">Setup the build</span></span>](CONTRIBUTING.md#build-setup)
 3. <span data-ttu-id="f2bea-111">執行 `grunt`，在 "dist" 目錄中建立組建檔</span><span class="sxs-lookup"><span data-stu-id="f2bea-111">Run `grunt` to create the built files in the "dist" directory</span></span>

### <a name="including-it-on-your-page"></a><span data-ttu-id="f2bea-112">在您的頁面上包括該檔案</span><span class="sxs-lookup"><span data-stu-id="f2bea-112">Including it on your page</span></span>

<span data-ttu-id="f2bea-113">在頁面上包括 jQuery 和外掛程式。</span><span class="sxs-lookup"><span data-stu-id="f2bea-113">Include jQuery and the plugin on a page.</span></span> <span data-ttu-id="f2bea-114">然後選取表單來驗證並呼叫 `validate` 方法。</span><span class="sxs-lookup"><span data-stu-id="f2bea-114">Then select a form to validate and call the `validate` method.</span></span>

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

<span data-ttu-id="f2bea-115">或者，透過模組中的 requirejs 來包括 jQuery 和外掛程式。</span><span class="sxs-lookup"><span data-stu-id="f2bea-115">Alternatively include jQuery and the plugin via requirejs in your module.</span></span>

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

<span data-ttu-id="f2bea-116">如需如何設定規則和自訂項目的詳細資訊，請[參閱文件](https://jqueryvalidation.org/documentation/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="f2bea-116">For more information on how to setup a rules and customizations, [check the documentation](https://jqueryvalidation.org/documentation/).</span></span>

## <a name="reporting-issues-and-contributing-code"></a><span data-ttu-id="f2bea-117">回報問題並貢獻程式碼</span><span class="sxs-lookup"><span data-stu-id="f2bea-117">Reporting issues and contributing code</span></span>

<span data-ttu-id="f2bea-118">如需詳細資訊，請參閱[貢獻方針](CONTRIBUTING.md)。</span><span class="sxs-lookup"><span data-stu-id="f2bea-118">See the [Contributing Guidelines](CONTRIBUTING.md) for details.</span></span>

<span data-ttu-id="f2bea-119">**與電子郵件驗證有關的重要注意事項**。</span><span class="sxs-lookup"><span data-stu-id="f2bea-119">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="f2bea-120">截至 1.12.0 版本，此外掛程式會使用 [HTML5 規格所建議瀏覽器使用](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address) \(英文\) 的同一種規則運算式。</span><span class="sxs-lookup"><span data-stu-id="f2bea-120">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="f2bea-121">我們將跟隨他們的領導並使用相同檢查。</span><span class="sxs-lookup"><span data-stu-id="f2bea-121">We will follow their lead and use the same check.</span></span> <span data-ttu-id="f2bea-122">如果您認為規格有誤，請將問題回報給他們。</span><span class="sxs-lookup"><span data-stu-id="f2bea-122">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="f2bea-123">如果您有不同需求，請考慮[使用自訂方法](https://jqueryvalidation.org/jQuery.validator.addMethod/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="f2bea-123">If you have different requirements, consider [using a custom method](https://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>
<span data-ttu-id="f2bea-124">若需要調整內建的驗證規則運算式模式，請[依照文件](https://jqueryvalidation.org/jQuery.validator.methods/)。</span><span class="sxs-lookup"><span data-stu-id="f2bea-124">In case you need to adjust the built-in validation regular expression patterns, please [follow the documentation](https://jqueryvalidation.org/jQuery.validator.methods/).</span></span>

<span data-ttu-id="f2bea-125">**有關必要方法的重要注意事項**。</span><span class="sxs-lookup"><span data-stu-id="f2bea-125">**IMPORTANT NOTE ABOUT REQUIRED METHOD**.</span></span> <span data-ttu-id="f2bea-126">在 1.14.0 版之後，此外掛程式停止修剪附加元素值中的空格。</span><span class="sxs-lookup"><span data-stu-id="f2bea-126">As of version 1.14.0 this plugin stops trimming white spaces from the value of the attached element.</span></span> <span data-ttu-id="f2bea-127">若要達到相同的結果，您可以使用 [`normalizer`](https://jqueryvalidation.org/normalizer/)，這可以用來在驗證之前轉換元素值。</span><span class="sxs-lookup"><span data-stu-id="f2bea-127">If you want to achieve the same result, you can use the [`normalizer`](https://jqueryvalidation.org/normalizer/) that can be used to transform the value of an element before validation.</span></span> <span data-ttu-id="f2bea-128">此功能從 `v1.15.0` 開始就存在。</span><span class="sxs-lookup"><span data-stu-id="f2bea-128">This feature was available since `v1.15.0`.</span></span> <span data-ttu-id="f2bea-129">換句話說，您可以執行如下動作：</span><span class="sxs-lookup"><span data-stu-id="f2bea-129">In other words, you can do something like this:</span></span>
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

## <a name="license"></a><span data-ttu-id="f2bea-130">使用權</span><span class="sxs-lookup"><span data-stu-id="f2bea-130">License</span></span>
<span data-ttu-id="f2bea-131">著作權 &copy; Jörn Zaefferer</span><span class="sxs-lookup"><span data-stu-id="f2bea-131">Copyright &copy; Jörn Zaefferer</span></span><br>
<span data-ttu-id="f2bea-132">根據 MIT 授權進行授權。</span><span class="sxs-lookup"><span data-stu-id="f2bea-132">Licensed under the MIT license.</span></span>
