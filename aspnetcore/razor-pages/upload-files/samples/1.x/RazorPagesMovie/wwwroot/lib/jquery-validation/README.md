---
ms.openlocfilehash: 1b563a8c0674d51f893415221ca8fab574b78265
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57046545"
---
<a name="--"></a>--
================================

<span data-ttu-id="d278a-101">[![組建狀態](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency 狀態](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span><span class="sxs-lookup"><span data-stu-id="d278a-101">[![Build Status](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency Status](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span></span>

<span data-ttu-id="d278a-102">儘管使所有種類的自訂項目符合您的應用程式真的很簡單，但 jQuery 驗證外掛程式會為您的現有表單提供插入驗證。</span><span class="sxs-lookup"><span data-stu-id="d278a-102">The jQuery Validation Plugin provides drop-in validation for your existing forms, while making all kinds of customizations to fit your application really easy.</span></span>

## <a name="help-the-projecthttppledgiecomcampaigns18159"></a><span data-ttu-id="d278a-103">[為專案提供協助](http://pledgie.com/campaigns/18159) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="d278a-103">[Help the project](http://pledgie.com/campaigns/18159)</span></span>

<span data-ttu-id="d278a-104">[![為專案提供協助](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span><span class="sxs-lookup"><span data-stu-id="d278a-104">[![Help the project](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span></span>

<span data-ttu-id="d278a-105">這個專案需要協助！</span><span class="sxs-lookup"><span data-stu-id="d278a-105">This project is looking for help!</span></span> <span data-ttu-id="d278a-106">[您可以捐贈給持續進行的 Pledgie 活動](http://pledgie.com/campaigns/18159) \(英文\)，並協助傳播這個訊息。</span><span class="sxs-lookup"><span data-stu-id="d278a-106">[You can donate to the ongoing pledgie campaign](http://pledgie.com/campaigns/18159) and help spread the word.</span></span> <span data-ttu-id="d278a-107">如果您曾經使用此外掛程式或計劃要使用它，請考慮進行捐贈：任何金額都很有助益。</span><span class="sxs-lookup"><span data-stu-id="d278a-107">If you've used the plugin, or plan to use, consider a donation - any amount will help.</span></span>

<span data-ttu-id="d278a-108">您可以在 [Pledgie 頁面](http://pledgie.com/campaigns/18159) \(英文\) 上找到關於如何使用這筆費用的計劃。</span><span class="sxs-lookup"><span data-stu-id="d278a-108">You can find the plan for how to spend the money on the [pledgie page](http://pledgie.com/campaigns/18159).</span></span>

## <a name="get-started"></a><span data-ttu-id="d278a-109">開始使用</span><span class="sxs-lookup"><span data-stu-id="d278a-109">Get Started</span></span>

### <a name="downloading-the-prebuilt-files"></a><span data-ttu-id="d278a-110">下載預先建置的檔案</span><span class="sxs-lookup"><span data-stu-id="d278a-110">Downloading the prebuilt files</span></span>

<span data-ttu-id="d278a-111">預先建置的檔案可從下列位置下載： http://jqueryvalidation.org/</span><span class="sxs-lookup"><span data-stu-id="d278a-111">Prebuilt files can be downloaded from http://jqueryvalidation.org/</span></span>

### <a name="downloading-the-latest-changes"></a><span data-ttu-id="d278a-112">下載最新變更</span><span class="sxs-lookup"><span data-stu-id="d278a-112">Downloading the latest changes</span></span>

<span data-ttu-id="d278a-113">您可以使用下列方式來取得尚未發行的開發檔案：</span><span class="sxs-lookup"><span data-stu-id="d278a-113">The unreleased development files can be obtained by:</span></span>

 1. <span data-ttu-id="d278a-114">[下載](https://github.com/jzaefferer/jquery-validation/archive/master.zip)或派生 (fork) 此存放庫</span><span class="sxs-lookup"><span data-stu-id="d278a-114">[Downloading](https://github.com/jzaefferer/jquery-validation/archive/master.zip) or Forking this repository</span></span>
 2. [<span data-ttu-id="d278a-115">設定組建</span><span class="sxs-lookup"><span data-stu-id="d278a-115">Setup the build</span></span>](CONTRIBUTING.md#build-setup)
 3. <span data-ttu-id="d278a-116">執行 `grunt`，在 "dist" 目錄中建立組建檔</span><span class="sxs-lookup"><span data-stu-id="d278a-116">Run `grunt` to create the built files in the "dist" directory</span></span>

### <a name="including-it-on-your-page"></a><span data-ttu-id="d278a-117">在您的頁面上包括該檔案</span><span class="sxs-lookup"><span data-stu-id="d278a-117">Including it on your page</span></span>

<span data-ttu-id="d278a-118">在頁面上包括 jQuery 和外掛程式。</span><span class="sxs-lookup"><span data-stu-id="d278a-118">Include jQuery and the plugin on a page.</span></span> <span data-ttu-id="d278a-119">然後選取表單來驗證並呼叫 `validate` 方法。</span><span class="sxs-lookup"><span data-stu-id="d278a-119">Then select a form to validate and call the `validate` method.</span></span>

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

<span data-ttu-id="d278a-120">或者，透過模組中的 requirejs 來包括 jQuery 和外掛程式。</span><span class="sxs-lookup"><span data-stu-id="d278a-120">Alternatively include jQuery and the plugin via requirejs in your module.</span></span>

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

<span data-ttu-id="d278a-121">如需如何設定規則和自訂項目的詳細資訊，請[參閱文件](http://jqueryvalidation.org/documentation/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="d278a-121">For more information on how to setup a rules and customizations, [check the documentation](http://jqueryvalidation.org/documentation/).</span></span>

## <a name="reporting-issues-and-contributing-code"></a><span data-ttu-id="d278a-122">回報問題並貢獻程式碼</span><span class="sxs-lookup"><span data-stu-id="d278a-122">Reporting issues and contributing code</span></span>

<span data-ttu-id="d278a-123">如需詳細資訊，請參閱[貢獻方針](CONTRIBUTING.md)。</span><span class="sxs-lookup"><span data-stu-id="d278a-123">See the [Contributing Guidelines](CONTRIBUTING.md) for details.</span></span>

<span data-ttu-id="d278a-124">**與電子郵件驗證有關的重要注意事項**。</span><span class="sxs-lookup"><span data-stu-id="d278a-124">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="d278a-125">截至 1.12.0 版本，此外掛程式會使用 [HTML5 規格所建議瀏覽器使用](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address) \(英文\) 的同一種規則運算式。</span><span class="sxs-lookup"><span data-stu-id="d278a-125">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="d278a-126">我們將跟隨他們的領導並使用相同檢查。</span><span class="sxs-lookup"><span data-stu-id="d278a-126">We will follow their lead and use the same check.</span></span> <span data-ttu-id="d278a-127">如果您認為規格有誤，請將問題回報給他們。</span><span class="sxs-lookup"><span data-stu-id="d278a-127">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="d278a-128">如果您有不同需求，請考慮[使用自訂方法](http://jqueryvalidation.org/jQuery.validator.addMethod/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="d278a-128">If you have different requirements, consider [using a custom method](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>

## <a name="license"></a><span data-ttu-id="d278a-129">使用權</span><span class="sxs-lookup"><span data-stu-id="d278a-129">License</span></span>
<span data-ttu-id="d278a-130">著作權 &copy; Jörn Zaefferer</span><span class="sxs-lookup"><span data-stu-id="d278a-130">Copyright &copy; Jörn Zaefferer</span></span><br>
<span data-ttu-id="d278a-131">根據 MIT 授權進行授權。</span><span class="sxs-lookup"><span data-stu-id="d278a-131">Licensed under the MIT license.</span></span>
