---
ms.openlocfilehash: f60f934934ae9e16bbd1174959d99aecdbb5833d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040945"
---
--

<span data-ttu-id="604d9-101">[![Slack](https://bootstrap-slack.herokuapp.com/badge.svg)](https://bootstrap-slack.herokuapp.com)
![Bower 版本](https://img.shields.io/bower/v/bootstrap.svg)
[![npm 版本](https://img.shields.io/npm/v/bootstrap.svg)](https://www.npmjs.com/package/bootstrap)
[![組建狀態](https://img.shields.io/travis/twbs/bootstrap/master.svg)](https://travis-ci.org/twbs/bootstrap)
[![devDependency 狀態](https://img.shields.io/david/dev/twbs/bootstrap.svg)](https://david-dm.org/twbs/bootstrap#info=devDependencies)
[![NuGet](https://img.shields.io/nuget/v/bootstrap.svg)](https://www.nuget.org/packages/Bootstrap)
[![Selenium 測試狀態](https://saucelabs.com/browser-matrix/bootstrap.svg)](https://saucelabs.com/u/bootstrap)</span><span class="sxs-lookup"><span data-stu-id="604d9-101">[![Slack](https://bootstrap-slack.herokuapp.com/badge.svg)](https://bootstrap-slack.herokuapp.com)
![Bower version](https://img.shields.io/bower/v/bootstrap.svg)
[![npm version](https://img.shields.io/npm/v/bootstrap.svg)](https://www.npmjs.com/package/bootstrap)
[![Build Status](https://img.shields.io/travis/twbs/bootstrap/master.svg)](https://travis-ci.org/twbs/bootstrap)
[![devDependency Status](https://img.shields.io/david/dev/twbs/bootstrap.svg)](https://david-dm.org/twbs/bootstrap#info=devDependencies)
[![NuGet](https://img.shields.io/nuget/v/bootstrap.svg)](https://www.nuget.org/packages/Bootstrap)
[![Selenium Test Status](https://saucelabs.com/browser-matrix/bootstrap.svg)](https://saucelabs.com/u/bootstrap)</span></span>

<span data-ttu-id="604d9-102">Bootstrap 是一個簡潔、直覺式且功能強大的前端架構，讓 Web 開發更快速且更簡單，此架構是由 [Mark Otto](https://twitter.com/mdo) \(英文\) 和 [Jacob Thornton](https://twitter.com/fat) \(英文\) 所建立，並由具有社群大量支援和參與的[核心小組](https://github.com/orgs/twbs/people) \(英文\) 來維護。</span><span class="sxs-lookup"><span data-stu-id="604d9-102">Bootstrap is a sleek, intuitive, and powerful front-end framework for faster and easier web development, created by [Mark Otto](https://twitter.com/mdo) and [Jacob Thornton](https://twitter.com/fat), and maintained by the [core team](https://github.com/orgs/twbs/people) with the massive support and involvement of the community.</span></span>

<span data-ttu-id="604d9-103">若要開始使用，請參閱 <http://getbootstrap.com>！</span><span class="sxs-lookup"><span data-stu-id="604d9-103">To get started, check out <http://getbootstrap.com>!</span></span>


## <a name="table-of-contents"></a><span data-ttu-id="604d9-104">目錄</span><span class="sxs-lookup"><span data-stu-id="604d9-104">Table of contents</span></span>

* [<span data-ttu-id="604d9-105">快速入門</span><span class="sxs-lookup"><span data-stu-id="604d9-105">Quick start</span></span>](#quick-start)
* [<span data-ttu-id="604d9-106">Bug 與功能要求</span><span class="sxs-lookup"><span data-stu-id="604d9-106">Bugs and feature requests</span></span>](#bugs-and-feature-requests)
* [<span data-ttu-id="604d9-107">文件</span><span class="sxs-lookup"><span data-stu-id="604d9-107">Documentation</span></span>](#documentation)
* [<span data-ttu-id="604d9-108">貢獻</span><span class="sxs-lookup"><span data-stu-id="604d9-108">Contributing</span></span>](#contributing)
* [<span data-ttu-id="604d9-109">Community</span><span class="sxs-lookup"><span data-stu-id="604d9-109">Community</span></span>](#community)
* [<span data-ttu-id="604d9-110">版本控制</span><span class="sxs-lookup"><span data-stu-id="604d9-110">Versioning</span></span>](#versioning)
* [<span data-ttu-id="604d9-111">建立者</span><span class="sxs-lookup"><span data-stu-id="604d9-111">Creators</span></span>](#creators)
* [<span data-ttu-id="604d9-112">著作權及授權</span><span class="sxs-lookup"><span data-stu-id="604d9-112">Copyright and license</span></span>](#copyright-and-license)


## <a name="quick-start"></a><span data-ttu-id="604d9-113">快速入門</span><span class="sxs-lookup"><span data-stu-id="604d9-113">Quick start</span></span>

<span data-ttu-id="604d9-114">有數個快速入門選項可供使用：</span><span class="sxs-lookup"><span data-stu-id="604d9-114">Several quick start options are available:</span></span>

* <span data-ttu-id="604d9-115">[下載最新版本](https://github.com/twbs/bootstrap/archive/v3.3.7.zip) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="604d9-115">[Download the latest release](https://github.com/twbs/bootstrap/archive/v3.3.7.zip).</span></span>
* <span data-ttu-id="604d9-116">複製存放庫：`git clone https://github.com/twbs/bootstrap.git`。</span><span class="sxs-lookup"><span data-stu-id="604d9-116">Clone the repo: `git clone https://github.com/twbs/bootstrap.git`.</span></span>
* <span data-ttu-id="604d9-117">使用 [Bower](http://bower.io) \(英文\) 安裝：`bower install bootstrap`。</span><span class="sxs-lookup"><span data-stu-id="604d9-117">Install with [Bower](http://bower.io): `bower install bootstrap`.</span></span>
* <span data-ttu-id="604d9-118">使用 [npm](https://www.npmjs.com) \(英文\) 安裝：`npm install bootstrap@3`。</span><span class="sxs-lookup"><span data-stu-id="604d9-118">Install with [npm](https://www.npmjs.com): `npm install bootstrap@3`.</span></span>
* <span data-ttu-id="604d9-119">使用 [Meteor](https://www.meteor.com) \(英文\) 安裝：`meteor add twbs:bootstrap`。</span><span class="sxs-lookup"><span data-stu-id="604d9-119">Install with [Meteor](https://www.meteor.com): `meteor add twbs:bootstrap`.</span></span>
* <span data-ttu-id="604d9-120">使用 [Composer](https://getcomposer.org) \(英文\) 安裝：`composer require twbs/bootstrap`。</span><span class="sxs-lookup"><span data-stu-id="604d9-120">Install with [Composer](https://getcomposer.org): `composer require twbs/bootstrap`.</span></span>

<span data-ttu-id="604d9-121">閱讀[開始使用頁面](http://getbootstrap.com/getting-started/) \(英文\)，以取得架構內容、範本和範例的相關資訊，以及其他更多資訊。</span><span class="sxs-lookup"><span data-stu-id="604d9-121">Read the [Getting started page](http://getbootstrap.com/getting-started/) for information on the framework contents, templates and examples, and more.</span></span>

### <a name="whats-included"></a><span data-ttu-id="604d9-122">包含的內容</span><span class="sxs-lookup"><span data-stu-id="604d9-122">What's included</span></span>

<span data-ttu-id="604d9-123">在下載中，您將會發現下列目錄和檔案，以邏輯方式將常見資產分組，並同時提供已編譯和縮減的變化。</span><span class="sxs-lookup"><span data-stu-id="604d9-123">Within the download you'll find the following directories and files, logically grouping common assets and providing both compiled and minified variations.</span></span> <span data-ttu-id="604d9-124">您將看到類似下面的內容：</span><span class="sxs-lookup"><span data-stu-id="604d9-124">You'll see something like this:</span></span>

```
bootstrap/
├── css/
│   ├── bootstrap.css
│   ├── bootstrap.css.map
│   ├── bootstrap.min.css
│   ├── bootstrap.min.css.map
│   ├── bootstrap-theme.css
│   ├── bootstrap-theme.css.map
│   ├── bootstrap-theme.min.css
│   └── bootstrap-theme.min.css.map
├── js/
│   ├── bootstrap.js
│   └── bootstrap.min.js
└── fonts/
    ├── glyphicons-halflings-regular.eot
    ├── glyphicons-halflings-regular.svg
    ├── glyphicons-halflings-regular.ttf
    ├── glyphicons-halflings-regular.woff
    └── glyphicons-halflings-regular.woff2
```

<span data-ttu-id="604d9-125">我們提供已編譯的 CSS 與 JS (`bootstrap.*`)，以及已編譯且縮減的 CSS 與 JS (`bootstrap.min.*`)。</span><span class="sxs-lookup"><span data-stu-id="604d9-125">We provide compiled CSS and JS (`bootstrap.*`), as well as compiled and minified CSS and JS (`bootstrap.min.*`).</span></span> <span data-ttu-id="604d9-126">CSS [來源對應](https://developer.chrome.com/devtools/docs/css-preprocessors) \(英文\) (`bootstrap.*.map`) 可用來與某些瀏覽器的開發人員工具搭配使用。</span><span class="sxs-lookup"><span data-stu-id="604d9-126">CSS [source maps](https://developer.chrome.com/devtools/docs/css-preprocessors) (`bootstrap.*.map`) are available for use with certain browsers' developer tools.</span></span> <span data-ttu-id="604d9-127">已隨附 Glyphicons 提供的字型，及選用的 Bootstrap 佈景主題。</span><span class="sxs-lookup"><span data-stu-id="604d9-127">Fonts from Glyphicons are included, as is the optional Bootstrap theme.</span></span>


## <a name="bugs-and-feature-requests"></a><span data-ttu-id="604d9-128">Bug 與功能要求</span><span class="sxs-lookup"><span data-stu-id="604d9-128">Bugs and feature requests</span></span>

<span data-ttu-id="604d9-129">有 Bug 或功能要求嗎？</span><span class="sxs-lookup"><span data-stu-id="604d9-129">Have a bug or a feature request?</span></span> <span data-ttu-id="604d9-130">請先閱讀[問題指導方針](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md#using-the-issue-tracker) \(英文\)，並搜尋現有和已結案的問題。</span><span class="sxs-lookup"><span data-stu-id="604d9-130">Please first read the [issue guidelines](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md#using-the-issue-tracker) and search for existing and closed issues.</span></span> <span data-ttu-id="604d9-131">如果您的問題或意見尚未獲得處理，[請開立新的問題](https://github.com/twbs/bootstrap/issues/new)。</span><span class="sxs-lookup"><span data-stu-id="604d9-131">If your problem or idea isn't addressed yet, [please open a new issue](https://github.com/twbs/bootstrap/issues/new).</span></span>

<span data-ttu-id="604d9-132">請注意，**功能要求必須將目標設為 [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev) \(英文\)，** 因為 Bootstrap v3 現已處於維護模式，不會再新增功能。</span><span class="sxs-lookup"><span data-stu-id="604d9-132">Note that **feature requests must target [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev),** because Bootstrap v3 is now in maintenance mode and is closed off to new features.</span></span> <span data-ttu-id="604d9-133">這樣我們就可專注投入 Bootstrap v4。</span><span class="sxs-lookup"><span data-stu-id="604d9-133">This is so that we can focus our efforts on Bootstrap v4.</span></span>


## <a name="documentation"></a><span data-ttu-id="604d9-134">文件</span><span class="sxs-lookup"><span data-stu-id="604d9-134">Documentation</span></span>

<span data-ttu-id="604d9-135">Bootstrap 的文件包含在此存放庫的根目錄中，且使用 [Jekyll](http://jekyllrb.com) 來建置，並公開裝載於 GitHub Pages，網址是 <http://getbootstrap.com>。</span><span class="sxs-lookup"><span data-stu-id="604d9-135">Bootstrap's documentation, included in this repo in the root directory, is built with [Jekyll](http://jekyllrb.com) and publicly hosted on GitHub Pages at <http://getbootstrap.com>.</span></span> <span data-ttu-id="604d9-136">文件也可能會在本機執行。</span><span class="sxs-lookup"><span data-stu-id="604d9-136">The docs may also be run locally.</span></span>

### <a name="running-documentation-locally"></a><span data-ttu-id="604d9-137">在本機執行文件</span><span class="sxs-lookup"><span data-stu-id="604d9-137">Running documentation locally</span></span>

1. <span data-ttu-id="604d9-138">如有必要，請利用 `bundle install` 來[安裝 Jekyll](http://jekyllrb.com/docs/installation) \(英文\) 及其他 Ruby 相依性。</span><span class="sxs-lookup"><span data-stu-id="604d9-138">If necessary, [install Jekyll](http://jekyllrb.com/docs/installation) and other Ruby dependencies with `bundle install`.</span></span>
   <span data-ttu-id="604d9-139">**Windows 使用者的附註：** 讀取[這份非官方指南](http://jekyll-windows.juthilo.com/)以 Jekyll 啟動並執行正常。</span><span class="sxs-lookup"><span data-stu-id="604d9-139">**Note for Windows users:** Read [this unofficial guide](http://jekyll-windows.juthilo.com/) to get Jekyll up and running without problems.</span></span>
2. <span data-ttu-id="604d9-140">從根 `/bootstrap` 目錄，在命令列中執行 `bundle exec jekyll serve`。</span><span class="sxs-lookup"><span data-stu-id="604d9-140">From the root `/bootstrap` directory, run `bundle exec jekyll serve` in the command line.</span></span>
4. <span data-ttu-id="604d9-141">在瀏覽器中開啟 `http://localhost:9001`，就是這麼簡單。</span><span class="sxs-lookup"><span data-stu-id="604d9-141">Open `http://localhost:9001` in your browser, and voilà.</span></span>

<span data-ttu-id="604d9-142">請閱讀 Jekyll 的[文件](http://jekyllrb.com/docs/home/) \(英文\)，以深入了解使用 Jekyll 的方式。</span><span class="sxs-lookup"><span data-stu-id="604d9-142">Learn more about using Jekyll by reading its [documentation](http://jekyllrb.com/docs/home/).</span></span>

### <a name="documentation-for-previous-releases"></a><span data-ttu-id="604d9-143">舊版文件</span><span class="sxs-lookup"><span data-stu-id="604d9-143">Documentation for previous releases</span></span>

<span data-ttu-id="604d9-144">在使用者轉換到 Bootstrap 3 的同時，v2.3.2 的文件會暫時於 <http://getbootstrap.com/2.3.2/> 上提供。</span><span class="sxs-lookup"><span data-stu-id="604d9-144">Documentation for v2.3.2 has been made available for the time being at <http://getbootstrap.com/2.3.2/> while folks transition to Bootstrap 3.</span></span>

<span data-ttu-id="604d9-145">[舊版](https://github.com/twbs/bootstrap/releases) \(英文\) 及其文件也可供下載。</span><span class="sxs-lookup"><span data-stu-id="604d9-145">[Previous releases](https://github.com/twbs/bootstrap/releases) and their documentation are also available for download.</span></span>


## <a name="contributing"></a><span data-ttu-id="604d9-146">貢獻</span><span class="sxs-lookup"><span data-stu-id="604d9-146">Contributing</span></span>

<span data-ttu-id="604d9-147">請閱讀我們的[貢獻方針](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="604d9-147">Please read through our [contributing guidelines](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md).</span></span> <span data-ttu-id="604d9-148">內含的指引適用於開啟問題、程式撰寫標準及開發注意事項。</span><span class="sxs-lookup"><span data-stu-id="604d9-148">Included are directions for opening issues, coding standards, and notes on development.</span></span>

<span data-ttu-id="604d9-149">此外，如果您的提取要求包含 JavaScript 修補檔案或功能，您就必須包含[相關單元測試](https://github.com/twbs/bootstrap/tree/master/js/tests) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="604d9-149">Moreover, if your pull request contains JavaScript patches or features, you must include [relevant unit tests](https://github.com/twbs/bootstrap/tree/master/js/tests).</span></span> <span data-ttu-id="604d9-150">所有 HTML 和 CSS 都應符合由 [Mark Otto](https://github.com/mdo) 所維護的[程式碼指南](https://github.com/mdo/code-guide) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="604d9-150">All HTML and CSS should conform to the [Code Guide](https://github.com/mdo/code-guide), maintained by [Mark Otto](https://github.com/mdo).</span></span>

<span data-ttu-id="604d9-151">**Bootstrap v3 現已不再新增功能。**</span><span class="sxs-lookup"><span data-stu-id="604d9-151">**Bootstrap v3 is now closed off to new features.**</span></span> <span data-ttu-id="604d9-152">它已經進入維護模式，讓我們可專注投入 [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev) \(英文\)，即此架構的未來版本。</span><span class="sxs-lookup"><span data-stu-id="604d9-152">It has gone into maintenance mode so that we can focus our efforts on [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev), the future of the framework.</span></span> <span data-ttu-id="604d9-153">新增功能 (而非修正 Bug) 的提取要求應將目標改設為 [Bootstrap v4 (`v4-dev` Git 分支)](https://github.com/twbs/bootstrap/tree/v4-dev) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="604d9-153">Pull requests which add new features (rather than fix bugs) should target [Bootstrap v4 (the `v4-dev` git branch)](https://github.com/twbs/bootstrap/tree/v4-dev) instead.</span></span>

<span data-ttu-id="604d9-154">您可以在[編輯器設定](https://github.com/twbs/bootstrap/blob/master/.editorconfig) \(英文\) 中取得編輯器喜好設定，以便在常見的文字編輯器中輕鬆使用。</span><span class="sxs-lookup"><span data-stu-id="604d9-154">Editor preferences are available in the [editor config](https://github.com/twbs/bootstrap/blob/master/.editorconfig) for easy use in common text editors.</span></span> <span data-ttu-id="604d9-155">在 <http://editorconfig.org> 深入了解並下載外掛程式。</span><span class="sxs-lookup"><span data-stu-id="604d9-155">Read more and download plugins at <http://editorconfig.org>.</span></span>


## <a name="community"></a><span data-ttu-id="604d9-156">社群</span><span class="sxs-lookup"><span data-stu-id="604d9-156">Community</span></span>

<span data-ttu-id="604d9-157">取得關於 Bootstrap 開發的更新，並與專案維護人員和社群成員交談。</span><span class="sxs-lookup"><span data-stu-id="604d9-157">Get updates on Bootstrap's development and chat with the project maintainers and community members.</span></span>

* <span data-ttu-id="604d9-158">關注 [Twitter 上的 @getbootstrap](https://twitter.com/getbootstrap) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="604d9-158">Follow [@getbootstrap on Twitter](https://twitter.com/getbootstrap).</span></span>
* <span data-ttu-id="604d9-159">閱讀和訂閱[Bootstrap 官方部落格](http://blog.getbootstrap.com) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="604d9-159">Read and subscribe to [The Official Bootstrap Blog](http://blog.getbootstrap.com).</span></span>
* <span data-ttu-id="604d9-160">加入[官方 Slack 聊天室](https://bootstrap-slack.herokuapp.com) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="604d9-160">Join [the official Slack room](https://bootstrap-slack.herokuapp.com).</span></span>
* <span data-ttu-id="604d9-161">在 IRC 中，與 Bootstrap 的夥伴交談。</span><span class="sxs-lookup"><span data-stu-id="604d9-161">Chat with fellow Bootstrappers in IRC.</span></span> <span data-ttu-id="604d9-162">在 `irc.freenode.net` 伺服器上的 `##bootstrap` 通道中。</span><span class="sxs-lookup"><span data-stu-id="604d9-162">On the `irc.freenode.net` server, in the `##bootstrap` channel.</span></span>
* <span data-ttu-id="604d9-163">實作說明可在 Stack Overflow 上找到 (標記為 [`twitter-bootstrap-3`](https://stackoverflow.com/questions/tagged/twitter-bootstrap-3))。</span><span class="sxs-lookup"><span data-stu-id="604d9-163">Implementation help may be found at Stack Overflow (tagged [`twitter-bootstrap-3`](https://stackoverflow.com/questions/tagged/twitter-bootstrap-3)).</span></span>
* <span data-ttu-id="604d9-164">當開發人員透過 [npm](https://www.npmjs.com/browse/keyword/bootstrap) \(英文\) 或類似的傳遞機制來散發已修改的或新增功能的 Bootstrap 封裝時，應在封裝上使用關鍵字 `bootstrap`，使其更容易被發現。</span><span class="sxs-lookup"><span data-stu-id="604d9-164">Developers should use the keyword `bootstrap` on packages which modify or add to the functionality of Bootstrap when distributing through [npm](https://www.npmjs.com/browse/keyword/bootstrap) or similar delivery mechanisms for maximum discoverability.</span></span>


## <a name="versioning"></a><span data-ttu-id="604d9-165">版本控制</span><span class="sxs-lookup"><span data-stu-id="604d9-165">Versioning</span></span>

<span data-ttu-id="604d9-166">為了使我們的發行週期透明化且努力維持回溯相容性，Bootstrap 會按照[語意化版本方針](http://semver.org/) \(英文\) 進行維護。</span><span class="sxs-lookup"><span data-stu-id="604d9-166">For transparency into our release cycle and in striving to maintain backward compatibility, Bootstrap is maintained under [the Semantic Versioning guidelines](http://semver.org/).</span></span> <span data-ttu-id="604d9-167">我們有時會搞砸，但我們將盡可能遵循這些規則。</span><span class="sxs-lookup"><span data-stu-id="604d9-167">Sometimes we screw up, but we'll adhere to those rules whenever possible.</span></span>

<span data-ttu-id="604d9-168">如需每個 Bootstrap 發行版本的變更記錄，請參閱[我們 GitHub 專案的 [Releases] \(版本\) 區段](https://github.com/twbs/bootstrap/releases) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="604d9-168">See [the Releases section of our GitHub project](https://github.com/twbs/bootstrap/releases) for changelogs for each release version of Bootstrap.</span></span> <span data-ttu-id="604d9-169">[Bootstrap 官方部落格](http://blog.getbootstrap.com) \(英文\) 上的版本宣告文章會包含每個版本中所做最值得注意的變更摘要。</span><span class="sxs-lookup"><span data-stu-id="604d9-169">Release announcement posts on [the official Bootstrap blog](http://blog.getbootstrap.com) contain summaries of the most noteworthy changes made in each release.</span></span>


## <a name="creators"></a><span data-ttu-id="604d9-170">建立者</span><span class="sxs-lookup"><span data-stu-id="604d9-170">Creators</span></span>

<span data-ttu-id="604d9-171">**Mark Otto**</span><span class="sxs-lookup"><span data-stu-id="604d9-171">**Mark Otto**</span></span>

* <https://twitter.com/mdo>
* <https://github.com/mdo>

<span data-ttu-id="604d9-172">**Jacob Thornton**</span><span class="sxs-lookup"><span data-stu-id="604d9-172">**Jacob Thornton**</span></span>

* <https://twitter.com/fat>
* <https://github.com/fat>


## <a name="copyright-and-license"></a><span data-ttu-id="604d9-173">著作權及授權</span><span class="sxs-lookup"><span data-stu-id="604d9-173">Copyright and license</span></span>

<span data-ttu-id="604d9-174">程式碼和文件著作權 2011-2016 Twitter, Inc.已根據 [MIT 授權](https://github.com/twbs/bootstrap/blob/master/LICENSE) \(英文\) 發行程式碼。</span><span class="sxs-lookup"><span data-stu-id="604d9-174">Code and documentation copyright 2011-2016 Twitter, Inc. Code released under [the MIT license](https://github.com/twbs/bootstrap/blob/master/LICENSE).</span></span> <span data-ttu-id="604d9-175">已根據 [Creative Commons](https://github.com/twbs/bootstrap/blob/master/docs/LICENSE) \(英文\) 發行文件。</span><span class="sxs-lookup"><span data-stu-id="604d9-175">Docs released under [Creative Commons](https://github.com/twbs/bootstrap/blob/master/docs/LICENSE).</span></span>
