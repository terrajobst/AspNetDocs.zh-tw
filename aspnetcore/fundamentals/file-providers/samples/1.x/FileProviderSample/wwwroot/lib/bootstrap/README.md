---
ms.openlocfilehash: 3be420696add54094f24424285a905e7e7963bad
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028825"
---
# <a name="bootstraphttpgetbootstrapcom"></a>[啟動程序](http://getbootstrap.com)

[![Slack](https://bootstrap-slack.herokuapp.com/badge.svg)](https://bootstrap-slack.herokuapp.com)
![Bower 版本](https://img.shields.io/bower/v/bootstrap.svg)
[![npm 版本](https://img.shields.io/npm/v/bootstrap.svg)](https://www.npmjs.com/package/bootstrap)
[![組建狀態](https://img.shields.io/travis/twbs/bootstrap/master.svg)](https://travis-ci.org/twbs/bootstrap)
[![devDependency 狀態](https://img.shields.io/david/dev/twbs/bootstrap.svg)](https://david-dm.org/twbs/bootstrap#info=devDependencies)
[![NuGet](https://img.shields.io/nuget/v/bootstrap.svg)](https://www.nuget.org/packages/Bootstrap)
[![Selenium 測試狀態](https://saucelabs.com/browser-matrix/bootstrap.svg)](https://saucelabs.com/u/bootstrap)

Bootstrap 是一個簡潔、直覺式且功能強大的前端架構，讓 Web 開發更快速且更簡單，此架構是由 [Mark Otto](https://twitter.com/mdo) \(英文\) 和 [Jacob Thornton](https://twitter.com/fat) \(英文\) 所建立，並由具有社群大量支援和參與的[核心小組](https://github.com/orgs/twbs/people) \(英文\) 來維護。

若要開始使用，請參閱 <http://getbootstrap.com>！


## <a name="table-of-contents"></a>目錄

* [快速入門](#quick-start)
* [Bug 與功能要求](#bugs-and-feature-requests)
* [文件](#documentation)
* [貢獻](#contributing)
* [Community](#community)
* [版本控制](#versioning)
* [建立者](#creators)
* [著作權及授權](#copyright-and-license)


## <a name="quick-start"></a>快速入門

有數個快速入門選項可供使用：

* [下載最新版本](https://github.com/twbs/bootstrap/archive/v3.3.7.zip) \(英文\)。
* 複製存放庫：`git clone https://github.com/twbs/bootstrap.git`。
* 使用 [Bower](http://bower.io) \(英文\) 安裝：`bower install bootstrap`。
* 使用 [npm](https://www.npmjs.com) \(英文\) 安裝：`npm install bootstrap@3`。
* 使用 [Meteor](https://www.meteor.com) \(英文\) 安裝：`meteor add twbs:bootstrap`。
* 使用 [Composer](https://getcomposer.org) \(英文\) 安裝：`composer require twbs/bootstrap`。

閱讀[開始使用頁面](http://getbootstrap.com/getting-started/) \(英文\)，以取得架構內容、範本和範例的相關資訊，以及其他更多資訊。

### <a name="whats-included"></a>包含的內容

在下載中，您將會發現下列目錄和檔案，以邏輯方式將常見資產分組，並同時提供已編譯和縮減的變化。 您將看到類似下面的內容：

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

我們提供已編譯的 CSS 與 JS (`bootstrap.*`)，以及已編譯且縮減的 CSS 與 JS (`bootstrap.min.*`)。 CSS [來源對應](https://developer.chrome.com/devtools/docs/css-preprocessors) \(英文\) (`bootstrap.*.map`) 可用來與某些瀏覽器的開發人員工具搭配使用。 已隨附 Glyphicons 提供的字型，及選用的 Bootstrap 佈景主題。


## <a name="bugs-and-feature-requests"></a>Bug 與功能要求

有 Bug 或功能要求嗎？ 請先閱讀[問題指導方針](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md#using-the-issue-tracker) \(英文\)，並搜尋現有和已結案的問題。 如果您的問題或意見尚未獲得解決，[請開啟新問題](https://github.com/twbs/bootstrap/issues/new) \(英文\)。

請注意，**功能要求必須將目標設為 [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev) \(英文\)，** 因為 Bootstrap v3 現已處於維護模式，不會再新增功能。 這樣我們就可專注投入 Bootstrap v4。


## <a name="documentation"></a>文件

Bootstrap 的文件包含在此存放庫的根目錄中，且使用 [Jekyll](http://jekyllrb.com) 來建置，並公開裝載於 GitHub Pages，網址是 <http://getbootstrap.com>。 文件也可能會在本機執行。

### <a name="running-documentation-locally"></a>在本機執行文件

1. 如有必要，請利用 `bundle install` 來[安裝 Jekyll](http://jekyllrb.com/docs/installation) \(英文\) 及其他 Ruby 相依性。
   **Windows 使用者的附註：** 讀取[這份非官方指南](http://jekyll-windows.juthilo.com/)以 Jekyll 啟動並執行正常。
2. 從根 `/bootstrap` 目錄，在命令列中執行 `bundle exec jekyll serve`。
4. 在瀏覽器中開啟 `http://localhost:9001`，就是這麼簡單。

請閱讀 Jekyll 的[文件](http://jekyllrb.com/docs/home/) \(英文\)，以深入了解使用 Jekyll 的方式。

### <a name="documentation-for-previous-releases"></a>舊版文件

在使用者轉換到 Bootstrap 3 的同時，v2.3.2 的文件會暫時於 <http://getbootstrap.com/2.3.2/> 上提供。

[舊版](https://github.com/twbs/bootstrap/releases) \(英文\) 及其文件也可供下載。


## <a name="contributing"></a>貢獻

請閱讀我們的[貢獻方針](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md) \(英文\)。 內含的指引適用於開啟問題、程式撰寫標準及開發注意事項。

此外，如果您的提取要求包含 JavaScript 修補檔案或功能，您就必須包含[相關單元測試](https://github.com/twbs/bootstrap/tree/master/js/tests) \(英文\)。 所有 HTML 和 CSS 都應符合由 [Mark Otto](https://github.com/mdo) 所維護的[程式碼指南](https://github.com/mdo/code-guide) \(英文\)。

**Bootstrap v3 現已不再新增功能。** 它已經進入維護模式，讓我們可專注投入 [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev) \(英文\)，即此架構的未來版本。 新增功能 (而非修正 Bug) 的提取要求應將目標改設為 [Bootstrap v4 (`v4-dev` Git 分支)](https://github.com/twbs/bootstrap/tree/v4-dev) \(英文\)。

您可以在[編輯器設定](https://github.com/twbs/bootstrap/blob/master/.editorconfig) \(英文\) 中取得編輯器喜好設定，以便在常見的文字編輯器中輕鬆使用。 在 <http://editorconfig.org> 深入了解並下載外掛程式。


## <a name="community"></a>社群

取得關於 Bootstrap 開發的更新，並與專案維護人員和社群成員交談。

* 關注 [Twitter 上的 @getbootstrap](https://twitter.com/getbootstrap) \(英文\)。
* 閱讀和訂閱[Bootstrap 官方部落格](http://blog.getbootstrap.com) \(英文\)。
* 加入[官方 Slack 聊天室](https://bootstrap-slack.herokuapp.com) \(英文\)。
* 在 IRC 中，與 Bootstrap 的夥伴交談。 在 `irc.freenode.net` 伺服器上的 `##bootstrap` 通道中。
* 實作說明可在 Stack Overflow 上找到 (標記為 [`twitter-bootstrap-3`](https://stackoverflow.com/questions/tagged/twitter-bootstrap-3))。
* 當開發人員透過 [npm](https://www.npmjs.com/browse/keyword/bootstrap) \(英文\) 或類似的傳遞機制來散發已修改的或新增功能的 Bootstrap 封裝時，應在封裝上使用關鍵字 `bootstrap`，使其更容易被發現。


## <a name="versioning"></a>版本控制

為了使我們的發行週期透明化且努力維持回溯相容性，Bootstrap 會按照[語意化版本方針](http://semver.org/) \(英文\) 進行維護。 我們有時會搞砸，但我們將盡可能遵循這些規則。

如需每個 Bootstrap 發行版本的變更記錄，請參閱[我們 GitHub 專案的 [Releases] \(版本\) 區段](https://github.com/twbs/bootstrap/releases) \(英文\)。 [Bootstrap 官方部落格](http://blog.getbootstrap.com) \(英文\) 上的版本宣告文章會包含每個版本中所做最值得注意的變更摘要。


## <a name="creators"></a>建立者

**Mark Otto**

* <https://twitter.com/mdo>
* <https://github.com/mdo>

**Jacob Thornton**

* <https://twitter.com/fat>
* <https://github.com/fat>


## <a name="copyright-and-license"></a>著作權及授權

程式碼和文件著作權 2011-2016 Twitter, Inc.已根據 [MIT 授權](https://github.com/twbs/bootstrap/blob/master/LICENSE) \(英文\) 發行程式碼。 已根據 [Creative Commons](https://github.com/twbs/bootstrap/blob/master/docs/LICENSE) \(英文\) 發行文件。
