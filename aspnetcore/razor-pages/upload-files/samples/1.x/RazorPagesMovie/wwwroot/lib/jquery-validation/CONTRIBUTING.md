---
ms.openlocfilehash: 3b33bb9bcab1aa7e5438c6fe3f2d7ba0833e7756
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57054725"
---
--

## <a name="reporting-an-issue"></a>回報問題

1. 確定您正在處理的問題是可重現的。
2. 使用 http://jsbin.com 或 http://jsfiddle.net 提供測試頁。
3. 指出可在哪些瀏覽器中重現此問題。 **注意：不會處理 IE 相容性模式的問題。確定您是在真正的瀏覽器中進行測試！**
4. 問題可在哪個外掛程式版本中重現。 當您更新到最新版本之後是否可重現問題。

您也可以在 [jQuery 驗證](https://github.com/jzaefferer/jquery-validation/issues) \(英文\) 問題追蹤程式中追蹤文件問題。
儘管如此，[jQuery 驗證文件](https://github.com/jzaefferer/validation-content) \(英文\) 存放庫中也歡迎改善文件的提取要求。

**與電子郵件驗證有關的重要注意事項**。 截至 1.12.0 版本，此外掛程式會使用 [HTML5 規格所建議瀏覽器使用](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address) \(英文\) 的同一種規則運算式。 我們將跟隨他們的領導並使用相同檢查。 如果您認為規格有誤，請將問題回報給他們。 如果您有不同需求，請考慮[使用自訂方法](http://jqueryvalidation.org/jQuery.validator.addMethod/) \(英文\)。

## <a name="contributing-code"></a>貢獻程式碼

感謝您的貢獻！ 以下是一些可協助提供您的貢獻的方針。

1. 確定您正在處理的問題是可重現的。 使用 jsbin.com 或 jsfiddle.net 來提供測試頁。
2. 請遵循 [jQuery 樣式指南](http://contribute.jquery.com/style-guides/js) \(英文\)
3. 隨您的修補檔案新增或更新單元測試。 在至少一個瀏覽器中執行單元測試 (請參閱下文)。
4. 執行 `grunt` (請參閱下文) 來進行 Lint 檢查和一些其他問題的檢查。
5. 描述您的認可訊息中的變更，並參考該票證，像這樣：「 示範：已修正 dynamic-totals 示範的委派 bug。 修正 #51。」 如果您要加入新的當地語系化檔案，請使用類似這樣：「 當地語系化：已新增克羅埃西亞文 (HR) 的當地語系化 」

## <a name="build-setup"></a>建置設定

1. 安裝 [NodeJS](http://nodejs.org) \(英文\)。
2. 安裝 Grunt CLI 執行 `npm install -g grunt-cli` 來安裝。 如需更多詳細資料，請參閱其網站 http://gruntjs.com/getting-started。
3. 執行 `npm install` 來安裝 NPM 相依性。
4. 您現在可以執行 `grunt` 來呼叫組建。

## <a name="creating-a-new-additional-method"></a>建立新的額外方法

如果您已經撰寫要貢獻到 additional-methods.js 的自訂方法：

1. 建立分支
2. 將該方法新增為 `src/additional` 中的新檔案
3. (選擇性) 將翻譯新增到 `src/localization`
4. 將提取要求傳送到主要分支。

## <a name="unit-tests"></a>單元測試

若要執行單元測試，請在瀏覽器中開啟 `test/index.html`。 確定您已先執行 `npm install`，進行測試時才能取得所有必要的相依性。
先從某一個瀏覽器著手開發修正程式，接著在其他瀏覽器中執行，然後再提交。 通常是最新的 Chrome、Firefox、Safari 和 Opera，以及少數的 IE。

## <a name="documentation"></a>文件

請在 [jQuery 驗證](https://github.com/jzaefferer/jquery-validation/issues) \(英文\) 問題追蹤程式中回報文件問題。
萬一您的提取要求會實作或變更公用 API，那麼您還應該對 [jQuery 驗證文件](https://github.com/jzaefferer/validation-content) \(英文\) 存放庫提出提取要求。

## <a name="linting"></a>進行 Lint 檢查

若要執行 JSHint 和其他工具，請使用 `grunt`。
