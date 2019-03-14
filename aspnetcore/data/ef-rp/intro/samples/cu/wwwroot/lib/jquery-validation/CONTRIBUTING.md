---
ms.openlocfilehash: 1f36b95063094e891c1e6b44fbf4ee7546853d89
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050455"
---
# <a name="contributing-to-the-jquery-validation-plugin"></a><span data-ttu-id="05320-101">參與 jQuery 驗證外掛程式</span><span class="sxs-lookup"><span data-stu-id="05320-101">Contributing to the jQuery Validation Plugin</span></span>

## <a name="reporting-an-issue"></a><span data-ttu-id="05320-102">回報問題</span><span class="sxs-lookup"><span data-stu-id="05320-102">Reporting an Issue</span></span>

1. <span data-ttu-id="05320-103">確定您正在處理的問題是可重現的。</span><span class="sxs-lookup"><span data-stu-id="05320-103">Make sure the problem you're addressing is reproducible.</span></span>
2. <span data-ttu-id="05320-104">使用 http://jsbin.com 或 http://jsfiddle.net 提供測試頁。</span><span class="sxs-lookup"><span data-stu-id="05320-104">Use http://jsbin.com or http://jsfiddle.net to provide a test page.</span></span>
3. <span data-ttu-id="05320-105">指出可在哪些瀏覽器中重現此問題。</span><span class="sxs-lookup"><span data-stu-id="05320-105">Indicate what browsers the issue can be reproduced in.</span></span> <span data-ttu-id="05320-106">**注意：將不會解決 IE 相容性模式的問題。確定您是在真正的瀏覽器中進行測試！**</span><span class="sxs-lookup"><span data-stu-id="05320-106">**Note: IE Compatibilty mode issues will not be addressed. Make sure you test in a real browser!**</span></span>
4. <span data-ttu-id="05320-107">問題可在哪個外掛程式版本中重現。</span><span class="sxs-lookup"><span data-stu-id="05320-107">What version of the plug-in is the issue reproducible in.</span></span> <span data-ttu-id="05320-108">當您更新到最新版本之後是否可重現問題。</span><span class="sxs-lookup"><span data-stu-id="05320-108">Is it reproducible after updating to the latest version.</span></span>

<span data-ttu-id="05320-109">您也可以在 [jQuery 驗證](https://github.com/jzaefferer/jquery-validation/issues) \(英文\) 問題追蹤程式中追蹤文件問題。</span><span class="sxs-lookup"><span data-stu-id="05320-109">Documentation issues are also tracked at the [jQuery Validation](https://github.com/jzaefferer/jquery-validation/issues) issue tracker.</span></span>
<span data-ttu-id="05320-110">儘管如此，[jQuery 驗證文件](https://github.com/jzaefferer/validation-content) \(英文\) 存放庫中也歡迎改善文件的提取要求。</span><span class="sxs-lookup"><span data-stu-id="05320-110">Pull Requests to improve the docs are welcome at the [jQuery Validation docs](https://github.com/jzaefferer/validation-content) repository, though.</span></span>

<span data-ttu-id="05320-111">**與電子郵件驗證有關的重要注意事項**。</span><span class="sxs-lookup"><span data-stu-id="05320-111">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="05320-112">截至 1.12.0 版本，此外掛程式會使用 [HTML5 規格所建議瀏覽器使用](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address) \(英文\) 的同一種規則運算式。</span><span class="sxs-lookup"><span data-stu-id="05320-112">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="05320-113">我們將跟隨他們的領導並使用相同檢查。</span><span class="sxs-lookup"><span data-stu-id="05320-113">We will follow their lead and use the same check.</span></span> <span data-ttu-id="05320-114">如果您認為規格有誤，請將問題回報給他們。</span><span class="sxs-lookup"><span data-stu-id="05320-114">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="05320-115">如果您有不同需求，請考慮[使用自訂方法](http://jqueryvalidation.org/jQuery.validator.addMethod/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="05320-115">If you have different requirements, consider [using a custom method](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>

## <a name="contributing-code"></a><span data-ttu-id="05320-116">貢獻程式碼</span><span class="sxs-lookup"><span data-stu-id="05320-116">Contributing code</span></span>

<span data-ttu-id="05320-117">感謝您的貢獻！</span><span class="sxs-lookup"><span data-stu-id="05320-117">Thanks for contributing!</span></span> <span data-ttu-id="05320-118">以下是一些可協助提供您的貢獻的方針。</span><span class="sxs-lookup"><span data-stu-id="05320-118">Here's a few guidelines to help your contribution get landed.</span></span>

1. <span data-ttu-id="05320-119">確定您正在處理的問題是可重現的。</span><span class="sxs-lookup"><span data-stu-id="05320-119">Make sure the problem you're addressing is reproducible.</span></span> <span data-ttu-id="05320-120">使用 jsbin.com 或 jsfiddle.net 來提供測試頁。</span><span class="sxs-lookup"><span data-stu-id="05320-120">Use jsbin.com or jsfiddle.net to provide a test page.</span></span>
2. <span data-ttu-id="05320-121">請遵循 [jQuery 樣式指南](http://contribute.jquery.com/style-guides/js) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="05320-121">Follow the [jQuery style guide](http://contribute.jquery.com/style-guides/js)</span></span>
3. <span data-ttu-id="05320-122">隨您的修補檔案新增或更新單元測試。</span><span class="sxs-lookup"><span data-stu-id="05320-122">Add or update unit tests along with your patch.</span></span> <span data-ttu-id="05320-123">在至少一個瀏覽器中執行單元測試 (請參閱下文)。</span><span class="sxs-lookup"><span data-stu-id="05320-123">Run the unit tests in at least one browser (see below).</span></span>
4. <span data-ttu-id="05320-124">執行 `grunt` (請參閱下文) 來進行 Lint 檢查和一些其他問題的檢查。</span><span class="sxs-lookup"><span data-stu-id="05320-124">Run `grunt` (see below) to check for linting and a few other issues.</span></span>
5. <span data-ttu-id="05320-125">描述您的認可訊息中的變更，並參考該票證，像這樣：「 示範：已修正 dynamic-totals 示範的委派 bug。</span><span class="sxs-lookup"><span data-stu-id="05320-125">Describe the change in your commit message and reference the ticket, like this: "Demos: Fixed delegate bug for dynamic-totals demo.</span></span> <span data-ttu-id="05320-126">修正 #51。」</span><span class="sxs-lookup"><span data-stu-id="05320-126">Fixes #51".</span></span> <span data-ttu-id="05320-127">如果您要加入新的當地語系化檔案，請使用類似這樣：「 當地語系化：已新增克羅埃西亞文 (HR) 的當地語系化 」</span><span class="sxs-lookup"><span data-stu-id="05320-127">If you're adding a new localization file, use something like this: "Localization: Added croatian (HR) localization"</span></span>

## <a name="build-setup"></a><span data-ttu-id="05320-128">建置設定</span><span class="sxs-lookup"><span data-stu-id="05320-128">Build setup</span></span>

1. <span data-ttu-id="05320-129">安裝 [NodeJS](http://nodejs.org) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="05320-129">Install [NodeJS](http://nodejs.org).</span></span>
2. <span data-ttu-id="05320-130">安裝 Grunt CLI 執行 `npm install -g grunt-cli` 來安裝。</span><span class="sxs-lookup"><span data-stu-id="05320-130">Install the Grunt CLI To install by running `npm install -g grunt-cli`.</span></span> <span data-ttu-id="05320-131">如需更多詳細資料，請參閱其網站 http://gruntjs.com/getting-started。</span><span class="sxs-lookup"><span data-stu-id="05320-131">More details are available on their website http://gruntjs.com/getting-started.</span></span>
3. <span data-ttu-id="05320-132">執行 `npm install` 來安裝 NPM 相依性。</span><span class="sxs-lookup"><span data-stu-id="05320-132">Install the NPM dependencies by running `npm install`.</span></span>
4. <span data-ttu-id="05320-133">您現在可以執行 `grunt` 來呼叫組建。</span><span class="sxs-lookup"><span data-stu-id="05320-133">The build can now be called by running `grunt`.</span></span>

## <a name="creating-a-new-additional-method"></a><span data-ttu-id="05320-134">建立新的額外方法</span><span class="sxs-lookup"><span data-stu-id="05320-134">Creating a new Additional Method</span></span>

<span data-ttu-id="05320-135">如果您已經撰寫要貢獻到 additional-methods.js 的自訂方法：</span><span class="sxs-lookup"><span data-stu-id="05320-135">If you've wrote custom methods that you'd like to contribute to additional-methods.js:</span></span>

1. <span data-ttu-id="05320-136">建立分支</span><span class="sxs-lookup"><span data-stu-id="05320-136">Create a branch</span></span>
2. <span data-ttu-id="05320-137">將該方法新增為 `src/additional` 中的新檔案</span><span class="sxs-lookup"><span data-stu-id="05320-137">Add the method as a new file in `src/additional`</span></span>
3. <span data-ttu-id="05320-138">(選擇性) 將翻譯新增到 `src/localization`</span><span class="sxs-lookup"><span data-stu-id="05320-138">(Optional) Add translations to `src/localization`</span></span>
4. <span data-ttu-id="05320-139">將提取要求傳送到主要分支。</span><span class="sxs-lookup"><span data-stu-id="05320-139">Send a pull request to the master branch.</span></span>

## <a name="unit-tests"></a><span data-ttu-id="05320-140">單元測試</span><span class="sxs-lookup"><span data-stu-id="05320-140">Unit Tests</span></span>

<span data-ttu-id="05320-141">若要執行單元測試，請在瀏覽器中開啟 `test/index.html`。</span><span class="sxs-lookup"><span data-stu-id="05320-141">To run unit tests, just open `test/index.html` within your browser.</span></span> <span data-ttu-id="05320-142">確定您已先執行 `npm install`，進行測試時才能取得所有必要的相依性。</span><span class="sxs-lookup"><span data-stu-id="05320-142">Make sure you ran `npm install` before so all required dependencies are available.</span></span>
<span data-ttu-id="05320-143">先從某一個瀏覽器著手開發修正程式，接著在其他瀏覽器中執行，然後再提交。</span><span class="sxs-lookup"><span data-stu-id="05320-143">Start with one browser while developing the fix, then run against others before committing.</span></span> <span data-ttu-id="05320-144">通常是最新的 Chrome、Firefox、Safari 和 Opera，以及少數的 IE。</span><span class="sxs-lookup"><span data-stu-id="05320-144">Usually latest Chrome, Firefox, Safari and Opera and a few IEs.</span></span>

## <a name="documentation"></a><span data-ttu-id="05320-145">文件</span><span class="sxs-lookup"><span data-stu-id="05320-145">Documentation</span></span>

<span data-ttu-id="05320-146">請在 [jQuery 驗證](https://github.com/jzaefferer/jquery-validation/issues) \(英文\) 問題追蹤程式中回報文件問題。</span><span class="sxs-lookup"><span data-stu-id="05320-146">Please report documentation issues at the [jQuery Validation](https://github.com/jzaefferer/jquery-validation/issues) issue tracker.</span></span>
<span data-ttu-id="05320-147">萬一您的提取要求會實作或變更公用 API，那麼您還應該對 [jQuery 驗證文件](https://github.com/jzaefferer/validation-content) \(英文\) 存放庫提出提取要求。</span><span class="sxs-lookup"><span data-stu-id="05320-147">In case your pull request implements or changes public API it would be a plus you would provide a pull request against the [jQuery Validation docs](https://github.com/jzaefferer/validation-content) repository.</span></span>

## <a name="linting"></a><span data-ttu-id="05320-148">進行 Lint 檢查</span><span class="sxs-lookup"><span data-stu-id="05320-148">Linting</span></span>

<span data-ttu-id="05320-149">若要執行 JSHint 和其他工具，請使用 `grunt`。</span><span class="sxs-lookup"><span data-stu-id="05320-149">To run JSHint and other tools, use `grunt`.</span></span>
