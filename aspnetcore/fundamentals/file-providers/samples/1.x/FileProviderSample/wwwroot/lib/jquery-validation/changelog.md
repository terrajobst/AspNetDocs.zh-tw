---
ms.openlocfilehash: b97b3f95a1ecd1e5802794043f848bda83a2f966
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039425"
---
<a name="1160--2016-12-01"></a>1.16.0 / 2016-12-01
==================

## <a name="additional"></a>其他
  * 精簡 cifES 與 nieES 演算法。 關閉 #1826

## <a name="build"></a>組建
  * 在 NPM 套件中包括已縮小的版本
  * 將開發相依性延伸至最新版本

## <a name="core"></a>核心
  * 為具有按鈕類型的輸入新增繫結。 關閉 #1891
  * 支援 jquery3。 關閉 #1866
  * 將 jQuery 別名 'expr[":"]' 變更為 'expr.pseudos'

## <a name="localisation"></a>當地語系化
  * 新增 Urdu 翻譯。 關閉 #1873。

## <a name="localization"></a>當地語系化
  * 修正 az 翻譯的錯誤副檔名。 關閉 #1890。
  * 在 pt-BR 中新增遺漏的翻譯 (關閉 #1897)
  * 修正阿拉伯文語言檔案中的錯字。

## <a name="tests"></a>測試
  * 將 QUnit 升級到 2.0。

## <a name="umd"></a>UMD
  * CommonJS 的更好支援。

<a name="1151--2016-07-22"></a>1.15.1 / 2016-07-22
==================

## <a name="additional"></a>其他
  * 修正多個 mime 類型驗證
  * IBAN 需要至少 5 個字元 (關閉 #1797、修正 #1674)
  * 正確的 notEqualTo jQuery 參考資料

## <a name="core"></a>核心
  * 已為 #1805 新增失敗的測試
  * 修正具有 3 個欄位或更多欄位的群組驗證
  * 修正 #1644 與 #1657 引進的迴歸 (關閉 #1800)
  * 更新步驟驗證以正確地浮點數
  * 修正在非表單元素上呼叫 $.fn.rules() 的錯誤
  * 在驗證程式範圍中呼叫 `errorPlacement`
  * 修正單一輸入驗證事件會導致例外狀況之表單的內容可編輯元素

## <a name="demo"></a>示範
  * 新增連結到啟動程序與語意 UI 示範到 index.html
  * 使用 `.on()` 來取代 `.validateDelegate()`

## <a name="localization"></a>當地語系化
  * 已新增阿澤里文語言

## <a name="tests"></a>測試
  * 已新增 PR #1760 的迴歸單位測試

<a name="1150--2016-02-24"></a>1.15.0 / 2016-02-24
==================

## <a name="all"></a>全部
  * 已修正程式碼樣式問題

## <a name="core"></a>核心
  * `resetForm` 應該也要將 `valid` 類別從元素移除。
  * 當使用遠端規則時，若已將欄位反白顯示，會將欄位取消反白顯示。
  * 只在 `equalTo` 規則中繫結 `blur` 事件一次
  * 已修正在空白 jquery 集上呼叫 .rules() 的錯誤。
  * 修正輸入群組的錯誤訊息處理。
  * 修正當使用 `groups` 設定時 `showLabel` 中的 TypeError
  * 新增一個方式來將方法名稱傳遞到遠端
  * 當下一個欄位已填寫時，驗證失敗以觸發 (Fixes #1508)
  * 必要規則優先順序高於編號與數字規則
  * 錯誤會被隱藏，但不會移除輸入錯誤類別
  * 遠端驗證使用不正確的錯誤訊息
  * 已修正遠端驗證的欄位反白顯示問題。
  * 已修正多個 select 元素的 `:filled` 選取器。
  * 已新增文件參考到 jQuery.validator.methods
  * 將訊息處理從 `formatAndAdd` 移至 `defaultMessage`
  * ErrorList 只應該包含應該包含的錯誤
  * 在不包含 "C:\fakepath\" 的情況下擷取檔案名稱
  * HTML5 步驟屬性支援。 修正 #1295
  * 已新增對待處理要求上之「擱置中」類別的支援
  * 已新增正規器 (#1602)
  * 分裂出 `creditcard` 方法
  * 將 errorID 逸出以便在規則運算式中使用，不是為了要建置 aria-describedby
  * 將名稱中的單引號逸出以避免擲回 Sizzle 錯誤
  * 使用要求的已序列化資料物件，而不是使用驗證欄位的值來跳過 API 呼叫
  * 加入對 contentEditable 標記的支援

## <a name="additional"></a>其他
  * BIC：在第二個位置允許數字 1-9
  * 接受方法規則運算式應該正確地逸出。
  * BIC 的不區分大小寫檢查
  * 修正 postalCodeCA 以排除無效的 combinations
  * 提高 postalCodeCA 方法的容忍度

## <a name="localization"></a>當地語系化
  * 已新增馬其頓文當地語系化。
  * 已在波蘭文中新增遺漏的模式訊息 (adamwojtkiewicz)
  * 已修正波斯文最小/最大訊息的翻譯。
  * 已更新 messages_sk.js
  * 更新馬來文翻譯
  * 已包括來自其他方法的訊息
  * 改進 pt_BR translation 以及修正 'cifES' 索引鍵上的錯字。

<a name="1140--2015-06-30"></a>1.14.0 / 2015-06-30
==================

## <a name="core"></a>核心
  * 移除未使用的 removeAttrs 方法
  * 針對 url 方法取代 regex
  * 在 $.ajax 中移除錯誤的 url 參數，透過 $.extend 來覆寫
  * 適當地處理巢狀取消提交按鈕
  * 修正縮排
  * 重構 attributeRules 和 dataRules 以共用正規化器
  * 將值轉換成數字以進行數字輸入的 dataRules 方法
  * 更新 url 方法，以允許通訊協定相對的 url
  * 移除已被取代的 $.format 預留位置
  * 使用 jQuery 1.7+ on/off，新增 destroy 方法
  * IE8 相容性已將 .indexOf 變更為 $.inArray
  * 針對 Opera Mini，將 NaN 值屬性轉換為未定義的
  * 停止在 required 方法內修剪值
  * 用法：已停用選取器來比對停用的元素
  * 排除某些鍵盤按鍵，以避免重新驗證欄位
  * 請勿針對選項按鈕/核取方塊元素搜尋整個 DOM
  * 針對錯誤規則方法擲回更好的錯誤
  * 已修正數字驗證錯誤
  * 修正對 whatwg 規格的參考
  * 驗證一組自訂的輸入時將重心放在無效的元素上
  * 使用自訂 highlight 方法時重設元素樣式
  * 逸出錯誤識別碼中的貨幣符號
  * 還原「略過唯讀以及停用的欄位。」
  * 更新 Luhn演算法註解中的連結

## <a name="additionals"></a>補充項目
  * 更新 dateITA 以解決時區問題
  * 將擴充方法修正為僅限方法期間
  * 修正 accept 方法以便只比對期間
  * 更新 time 方法以允許單一數字的小時
  * 卸除 notEqualTo 方法的錯誤測試
  * 新增 notEqualTo 方法
  * 透過 `$` 使用正確的 jQuery 參考
  * 移除 iban 方法中無用的 regex 檢查
  * 巴西文的 CPF 號碼

## <a name="localization"></a>當地語系化
  * 更新 messages_tr.js
  * 更新 messages_sr_lat.js
  * 正在新增秘魯西班牙文 (ES PE)
  * 正在新增喬治亞文 (ქართული, ge)
  * 已修正加泰蘭文翻譯中的錯字
  * 改進芬蘭文 (fi) 的翻譯
  * 新增亞美尼亞文 (hy_AM) 的地區設定
  * 擴充含 currency 方法的義大利文 (it) 翻譯
  * 新增 bn_BD 地區設定
  * 更新 zh 地區設定
  * 移除義大利文訊息結尾處的句號

<a name="1131--2014-10-14"></a>1.13.1 / 2014-10-14
==================

## <a name="core"></a>核心
  * 允許 0 作為 autoCreateRanges 的值
  * 將忽略設定套用至所有 validationTargetFor 元素
  * 請勿修剪 min/max/rangelength 方法中的值
  * 逸出識別碼/名稱，然後用它作為 errorsFor 中的選取器
  * 明確地預設 focusCleanup 選項
  * 針對 describedby 比對器修正不正確的 regexp
  * 略過唯讀以及停用的欄位
  * 改進識別碼逸出，將逸出的識別碼儲存於 describedby
  * 使用 submitHandler 的傳回值以允許或防止表單提交

## <a name="additionals"></a>補充項目
  * 新增 postalcodeBR 方法
  * 修正當參數為字串時的 pattern 方法


<a name="1130--2014-07-01"></a>1.13.0 / 2014-07-01
==================

## <a name="all"></a>全部
* 新增外掛程式 UMD 包裝函式

## <a name="core"></a>核心
* 關於非錯誤的 aria-describedby 和空的隱藏錯誤
* 改進 dateISO RegExp
* 已新增選項按鈕/核取方塊來委派 click 事件
* 對非標籤元素使用 aria-describedby
* 同時也在選項按鈕/核取方塊上註冊 focusin、focusout 和 keyup
* 修正 rangelength 屬性值的正規化
* 更新 elementValue 方法來處理 type="number" 欄位
* 在字串中使用 charAt 而不是陣列標記法來支援 IE8(?)

## <a name="localization"></a>當地語系化
* 修正 rangelength 方法的 sk 翻譯
* 新增芬蘭文方法
* 已修正 GL 數字驗證訊息
* 已修正 ES 數字方法驗證訊息
* 已新增加里斯亞文 (GL)
* 已修正 min 和 max 方法的法文訊息

## <a name="additionals"></a>補充項目
* 新增 statesUS 方法
* 修正 dateITA 方法來處理 DST Bug
* 新增波斯文的 date 方法
* 新增 postalCodeCA 方法
* 新增 postalcodeIT 方法

<a name="1120--2014-04-01"></a>1.12.0 / 2014-04-01
==================

* 新增 ARIA 測試 ([3d5658e](https://github.com/jzaefferer/jquery-validation/commit/3d5658e9e4825fab27198c256beed86f0bd12577) \(英文\))
* 新增 es-AR 當地語系化訊息。 ([7b30beb](https://github.com/jzaefferer/jquery-validation/commit/7b30beb8ebd218c38a55d26a63d529e16035c7a2) \(英文\))
* 將遺漏的點新增至 'es' 和 'es_AR' 訊息。 ([a2a653c](https://github.com/jzaefferer/jquery-validation/commit/a2a653cb68926ca034b4b09d742d275db934d040) \(英文\))
* 已新增印尼文 (ID) 的當地語系化 ([1d348bd](https://github.com/jzaefferer/jquery-validation/commit/1d348bdcb65807c71da8d0bfc13a97663631cd3a) \(英文\))
* 已新增 NIF、NIE 及 CIF 西班牙文文件號碼驗證 ([#830](https://github.com/jzaefferer/jquery-validation/issues/830) \(英文\)、[317c20f](https://github.com/jzaefferer/jquery-validation/commit/317c20fa9bb772770bb9b70d46c7081d7cfc6545) \(英文\))
* 已將目前的表單新增至遠端 ajax 要求的內容 ([0a18ae6](https://github.com/jzaefferer/jquery-validation/commit/0a18ae65b9b6d877e3d15650a5c2617a9d2b11d5) \(英文\))
* 補充項目：更新 IBAN 方法、 修剪尾端空格 ([#970](https://github.com/jzaefferer/jquery-validation/issues/970)， [347b04a](https://github.com/jzaefferer/jquery-validation/commit/347b04a7d4e798227405246a5de3fc57451d52e1))
* BIC 方法：改善的 RegEx，{1}一律會重複。 關閉 gh-744 ([5cad6b4](https://github.com/jzaefferer/jquery-validation/commit/5cad6b493575e8a9a82470d17e0900c881130873) \(英文\))
* Bower:新增 Bower.json 以進行封裝註冊 ([e86ccb0](https://github.com/jzaefferer/jquery-validation/commit/e86ccb06e301613172d472cf15dd4011ff71b398))
* 基於與 jQuery.noConflict 的相容性，將貨幣參考變更為 'jQuery'。 關閉 gh-754 ([2049afe](https://github.com/jzaefferer/jquery-validation/commit/2049afe46c1be7b3b89b1d9f0690f5bebf4fbf68) \(英文\))
* 核心：將 「 方法 」 欄位加入至錯誤清單項目 ([89a15c7](https://github.com/jzaefferer/jquery-validation/commit/89a15c7a4b17fa2caaf4ff817f09b04c094c3884))
* 核心：已新增透過 data-msg 屬性的一般訊息的支援 ([5bebaa5](https://github.com/jzaefferer/jquery-validation/commit/5bebaa5c55c73f457c0e0181ec4e3b0c409e2a9d))
* 核心：允許屬性具有值為零 (例如，min = '0') ([#854](https://github.com/jzaefferer/jquery-validation/issues/854)， [9dc0d1d](https://github.com/jzaefferer/jquery-validation/commit/9dc0d1dd946b2c6178991fb16df0223c76162579))
* 核心：停用已被取代的 $.format ([#755](https://github.com/jzaefferer/jquery-validation/issues/755)， [bf3b350](https://github.com/jzaefferer/jquery-validation/commit/bf3b3509140ea8ab5d83d3ec58fd9f1d7822efc5))
* 核心：修正多個錯誤類別的支援 ([c1f0baf](https://github.com/jzaefferer/jquery-validation/commit/c1f0baf36c21ca175bbc05fb9345e5b44b094821))
* 核心：忽略已忽略的項目上的事件 ([#700](https://github.com/jzaefferer/jquery-validation/issues/700)， [a864211](https://github.com/jzaefferer/jquery-validation/commit/a86421131ea69786ee9e0d23a68a54a7658ccdbf))
* 核心：改進善 elementValue 方法 ([6c041ed](https://github.com/jzaefferer/jquery-validation/commit/6c041edd21af1425d12d06cdd1e6e32a78263e82))
* 核心：適當地讓 element() 忽略的控制代碼的項目。 ([3f464a8](https://github.com/jzaefferer/jquery-validation/commit/3f464a8da49dbb0e4881ada04165668e4a63cecb) \(英文\))
* 核心：切換剖析為 W3C HTML5 規格樣式的 dataRules ([460fd22](https://github.com/jzaefferer/jquery-validation/commit/460fd22b6c84a74c825ce1fa860c0a9da20b56bb))
* 核心：觸發 success 選擇性，但有其他成功的驗證程式 ([#851](https://github.com/jzaefferer/jquery-validation/issues/851)， [f93e1de](https://github.com/jzaefferer/jquery-validation/commit/f93e1deb48ec8b3a8a54e946a37db2de42d3aa2a))
* 核心：使用純元素而不是未包裝的項目 ([03cd4c9](https://github.com/jzaefferer/jquery-validation/commit/03cd4c93069674db5415a0bf174a5870da47e5d2))
* 核心：確定上一次是遠端執行 ([#711](https://github.com/jzaefferer/jquery-validation/issues/711) \(英文\)、[ad91b6f](https://github.com/jzaefferer/jquery-validation/commit/ad91b6f388b7fdfb03b74e78554cbab9fd8fca6f) \(英文\))
* 示範：在 multipart 示範中使用正確的選項。 ([# 1025](https://github.com/jzaefferer/jquery-validation/issues/1025) \(英文\)、[070edc7](https://github.com/jzaefferer/jquery-validation/commit/070edc7be4de564cb74cfa9ee4e3f40b6b70b76f) \(英文\))
* 修正額外方法中的 $/ jQuery 使用方式。 修正 #839 ([#839](https://github.com/jzaefferer/jquery-validation/issues/839) \(英文\)、[59bc899](https://github.com/jzaefferer/jquery-validation/commit/59bc899e4586255a4251903712e813c21d25b3e1) \(英文\))
* 改進中文翻譯 ([1a0bfe3](https://github.com/jzaefferer/jquery-validation/commit/1a0bfe32b16f8912ddb57388882aa880fab04ffe) \(英文\))
* 初始 ARIA 所需的實作 ([bf3cfb2](https://github.com/jzaefferer/jquery-validation/commit/bf3cfb234ede2891d3f7e19df02894797dd7ba5e) \(英文\))
* 當地語系化：變更要擴充的接受值。 修正 #771，關閉 gh-793。 ([#771](https://github.com/jzaefferer/jquery-validation/issues/771) \(英文\)、[12edec6](https://github.com/jzaefferer/jquery-validation/commit/12edec66eb30dc7e86756222d455d49b34016f65) \(英文\))
* 訊息：新增冰島文的當地語系化 ([dc88575](https://github.com/jzaefferer/jquery-validation/commit/dc885753c8872044b0eaa1713cecd94c19d4c73d))
* 訊息：將遺漏的點新增至 'bg'、 'fr' 及 'sr' 訊息中。 ([adbc636](https://github.com/jzaefferer/jquery-validation/commit/adbc6361c377bf6b74c35df9782479b1115fbad7) \(英文\))
* 訊息：建立 messages_sr_lat.js ([f2f9007](https://github.com/jzaefferer/jquery-validation/commit/f2f90076518014d98495c2a9afb9a35d45d184e6))
* 訊息：建立 messages_tj.js ([de830b3](https://github.com/jzaefferer/jquery-validation/commit/de830b3fd8689a7384656c17565ee92c2878d8a5))
* 訊息：修正 sr_lat 翻譯，新增遺漏的空格 ([880ba1c](https://github.com/jzaefferer/jquery-validation/commit/880ba1ca545903a41d8c5332fc4038a7e9a580bd))
* 訊息：更新 messages_sr.js，修正遺漏的空格 ([10313f4](https://github.com/jzaefferer/jquery-validation/commit/10313f418c18ea75f385248468c2d3600f136cfb))
* 方法:新增貨幣的其他方法 ([1a981b4](https://github.com/jzaefferer/jquery-validation/commit/1a981b440346620964c87ebdd0fa03246348390e))
* 方法:將智慧引號新增至 stripHTML 的標點符號移除 ([aa0d624](https://github.com/jzaefferer/jquery-validation/commit/aa0d6241c3ea04663edc1e45ed6e6134630bdd2f))
* 方法:修正 dateITA 方法，避免發生夏令時間錯誤 ([279b932](https://github.com/jzaefferer/jquery-validation/commit/279b932c1267b7238e6652880b7846ba3bbd2084))
* 方法:當地語系化智利文化特性 (ES-CL) 的方法 ([cf36b93](https://github.com/jzaefferer/jquery-validation/commit/cf36b933499e435196d951401221d533a4811810))
* 方法:更新電子郵件以使用 HTML5 regex，移除 email2 方法 ([#828](https://github.com/jzaefferer/jquery-validation/issues/828)， [dd162ae](https://github.com/jzaefferer/jquery-validation/commit/dd162ae360639f73edd2dcf7a256710b2f5a4e64))
* 模式的方法：移除分隔符號，因為 HTML5 實作不包含這其中任一個。 ([37992c1](https://github.com/jzaefferer/jquery-validation/commit/37992c1c9e2e0be8b315ccccc2acb74863439d3e) \(英文\))
* 限制信用卡驗證程式包含長度檢查。 關閉 gh-772 ([f5f47c5](https://github.com/jzaefferer/jquery-validation/commit/f5f47c5c661da5b0c0c6d59d169e82230928a804) \(英文\))
* 更新 messages_ko.js：關閉 gh-715 ([5da3085](https://github.com/jzaefferer/jquery-validation/commit/5da3085ff02e0e6ecc955a8bfc3bb9a8d220581b) \(英文\))
* 更新 messages_pt_BR.js。 關閉 gh-782 ([4bf813b](https://github.com/jzaefferer/jquery-validation/commit/4bf813b751ce34fac3c04eaa2e80f75da3461124) \(英文\))
* 更新 phonesUK 和 mobileUK 以接受新的前置詞。 關閉 gh-750 ([d447b41](https://github.com/jzaefferer/jquery-validation/commit/d447b41b830dee984be21d8281ec7b87a852001d) \(英文\))
* 確認九位數的郵遞區號。 關閉 gh-726 ([165005d](https://github.com/jzaefferer/jquery-validation/commit/165005d4b5780e22d13d13189d107940c622a76f) \(英文\))
* phoneUS:新增 N11 排除項目。 關閉 gh-861 ([519bbc6](https://github.com/jzaefferer/jquery-validation/commit/519bbc656bcb26e8aae5166d7b2e000014e0d12a) \(英文\))
* resetForm 應清除任何 aria-invalid 值 ([4f8a631](https://github.com/jzaefferer/jquery-validation/commit/4f8a631cbe84f496ec66260ada52db2aa0bb3733) \(英文\))
* valid （):請檢查所有項目。 修正 #791：valid() 只會驗證第一個 (無效的) 元素 ([#791](https://github.com/jzaefferer/jquery-validation/issues/791) \(英文\)、[6f26803](https://github.com/jzaefferer/jquery-validation/commit/6f268031afaf4e155424ee74dd11f6c47fbb8553) \(英文\))

<a name="1111--2013-03-22"></a>1.11.1 / 2013-03-22
==================

  * 還原也會將範圍方法的參數轉換成數字。 關閉 gh-702
  * 使用 mockjax 處理常式來取代 PHP 的大部分使用方式。 也會執行一些示範清除，更新至較新的遮罩輸入外掛程式。 在 PHP 中保留 captcha 示範。 修正 #662
  * 從 milk 示範中移除醒目提示的內嵌程式碼。 檢視來源運作正常。
  * 修正 dynamic-totals 示範，方法是先修剪範本內容的空格，然後再傳遞給 jQuery 建構函式
  * 修正 min/max 驗證。 關閉 gh-666。 修正 #648
  * 已修正顯示為規則並在透過 rules("add") 更新之後導致例外狀況的「訊息」。 關閉 gh-670，修正 #624
  * 新增韓文 (ko) 的當地語系化。 關閉 gh-671
  * 已改進英國的 postcode 方法，以篩選出更多無效的郵遞區號。 關閉 #682
  * 更新 messages_sv.js。 關閉 #683
  * 變更專案網站的 Grunt 連結。 關閉 #684
  * 在將其他所有方法套用至欄位之後，在清單中將遠端方法向下移動以便最後一個執行。 修正 #679
  * 更新 plugin.json 描述，應包含 'validate' 這個字
  * 修正錯字
  * 修正 jQuery 載入器以使用它自己的路徑。 修正巢狀示範。
  * 更新 grunt-contrib-qunit，以便在透過節點模組 'phantomjs' 安裝時使用 PhantomJS 1.8
  * 使 valid() 傳回布林值，而不是 0 或 1。 修正 #109：valid() 不會傳回布林值

<a name="1110--2013-02-04"></a>1.11.0 / 2013-02-04
==================

  * 移除按照 `min`、`max` 和 `range` 規則的數字清除。 修正 #455。 關閉 gh-528。
  * 更新預先存在的標籤：修正 #430 關閉 gh-436
  * 修正 $.validator.format 以避免群組內插補點，其中至少 IE8/9 要使用相符項目來取代 -bash。 修正 #614
  * 修正 mimetype regex
  * 新增外掛程式資訊清單，並且只將標頭更新為 MIT 授權，丟棄不必要的雙重授權 (例如 jQuery)。
  * 希伯來文訊息：在修正 gh-568 句子的結尾處移除的點
  * 適用於 Require_from_group 驗證的法文翻譯。 修正 gh-573。
  * 允許群組可以是陣列或字串：修正 #479
  * 已移除具有多種 MIME 類型的空格
  * 修正某些日期驗證，JS 語法錯誤。
  * 移除對於中繼資料外掛程式的支援，使用 data-rule- 和 data-msg- (已在 907467e8 中新增) 屬性來取代。
  * 已新增 sftp 作為有效的 url 模式
  * 新增馬來文 (my) 的當地語系化
  * 更新 localization/messages_hu.js
  * 移除 focusin/focusout polyfill。 修正 #542：在 IE9 中利用 focusin 和 focusout 事件包含 jquery.validate 干擾
  * 當地語系化：已修正芬蘭文翻譯中的錯字
  * 修正 RTM 示範，以便在從有效回到無效時顯示無效的圖示
  * 已修正遠端函式中的過早傳回，萬一輸入太快輸入時，可防止進行 ajax 呼叫。 確保遠端驗證一律會驗證最新的值。
  * 復原 #244 的修正。 修正 #521：電子郵件驗證會在文字存在於欄位中時立即引發。

<a name="1100--2012-09-07"></a>1.10.0 / 2012-09-07
===================

  * 已根據社群意見回應來更正 nowhitespace、phoneUS、phoneUK 和 mobileUK 的法文字串。
  * 依據標準 ISO_3166-1 (http://en.wikipedia.org/wiki/ISO_3166-1) 來將 language_REGION 的檔案重新命名，針對台灣，語言是中文 (zh)，而區域為台灣 (TW)
  * 將 RegEx 模式最佳化，特別是針對英國電話號碼。
  * 為每個檔案新增語言名稱，依據標準 ISO 639 (http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)，針對愛沙尼亞文、喬治亞文、烏克蘭文和中文，將語言代碼重新命名
  * 已新增克羅埃西亞文 (HR) 的當地語系化
  * 已編輯現有的法文翻譯，並已新增額外方法的法文翻譯。
  * 已合併變更以指定資料屬性中的自訂錯誤訊息
  * 已針對新的號碼更新英國行動電話號碼 regex。 修正 #154
  * 新增元素以利用測試進行成功呼叫。 修正 #60
  * 已修正時間額外方法的 regex。 修正 #131
  * resetForm 現在會清除表單元素上的舊 previousValue。 修正 #312
  * 已將核取方塊測試新增至 require_from_group，並已變更 require_from_group 以使用 elementValue。 修正 #359
  * 已修正 jQuery 1.5.2+ 中的 dataFilter 回應問題。 修正 #405
  * 已新增 jQuery Mobile 示範。 修正 #249
  * 基於正確性而取消 findByName 的最佳化。 修正 #82：$.validator.prototype.findByName 會在 IE7 中斷
  * 已新增美國郵遞區號的支援和測試。 修正 #90
  * 已在 keyup 中將 lastElement 變更為 lastActive ，略過索引標籤或空元素上的驗證。 修正 #244
  * 已移除從 stripHtml 中刪除的數字。 修正 #2
  * 已修正無效到有效遠端驗證中的無效計數。 修正 #286
  * 將 file_input 的連結新增至示範索引
  * 已將舊的 accept 方法移至 extension 額外方法，已新增新的 accept 方法來處理標準瀏覽器 mimetype 篩選。 修正 #287 並取代 #369
  * 將 onfocusout 設為 false 時停用 blur 事件。 已新增測試。
  * 已修正選項按鈕和核取方塊的問題。 修正 #363
  * 已新增 rangeWords 的測試，並且已修正方法中的 regex 和界限。 修正 #308
  * 已修正 TinyMCE 示範並已在示範頁面上新增連結。 修正 #382
  * 已變更 min/max 的當地語系化訊息。修正 #273
  * 已新增用於文字輸入類型的虛擬選取器，以修正預設空白類型屬性的問題。 已新增測試和某些測試標記。 修正 #217
  * 已修正 dynamic-totals 示範的委派 bug。 修正 #51
  * 修正英數字元驗證程式的不正確訊息
  * 已移除 required 屬性上不正確的 false 檢查
  * 對於非 html5 瀏覽器的 required 屬性修正。 修正 #301
  * 已新增方法 "require_from_group" 和 "skip_or_fill_minimum"
  * 針對瑞典文使用正確的 iso 代碼
  * 已更新示範 HTML 檔案以使用 HTML5 doctype
  * 已針對沒有以零為開頭的小數位數修正 regex 問題。 已新增新的方法測試。 修正 #41
  * 導入 elementValue 方法，此方法只會將字串值標準化 (不會接觸到多重選取的陣列值)。 修正 #116
  * 支援已動態新增的提交按鈕，以及已更新的測試案例。 使用 validateDelegate。 來自 PR #9 的程式碼
  * 修正測試裝置中不正確的雙引號
  * 修正 maxWords 方法以包括上限，不會將它排除。 修正 #284
  * 已修正德文範圍驗證程式訊息中的文法錯誤。 修正 #315
  * 已針對 errorClass 選項修正多個類別名稱的處理。 依 Max Lynch 進行測試。 修正 #280
  * 修正 jQuery.format 使用方式，應該是 $.validator.format。 修正 #329
  * 適用於「所有」英國電話號碼 + 英國郵遞區號的方法
  * 模式的方法：將字串參數轉換成 RegExp。 修正問題 #223
  * 德文當地語系化檔案中的文法錯誤
  * 已針對訊息新增愛沙尼亞文的當地語系化
  * 改進 themerollered 示範中的工具提示處理
  * 將 type="text" 新增至不具類型屬性的輸入欄位，以滿足 qSA
  * 更新 themerollered 示範，使用工具提示來將錯誤顯示為重疊。
  * 更新 themerollered 示範，以使用最新的 jQuery UI (以及較新的 jQuery 版本)。 四處移動程式碼以加速頁面載入。
  * 已修正日文裡毀損的 min 錯誤訊息。
  * 將表單外掛程式更新為最新版本。 增強 ajaxSubmit 示範。
  * 從 classRuleSettings 卸除 dateDE 和 numberDE 方法，將那些項目移至當地語系化的方法之後所剩餘的項目
  * 將 submit 事件傳遞至 submitHandler 回呼
  * 已修正 #219：利用相依性回呼或相依性運算式來修正元素上的 valid()。
  * 改進組建來移除 dist dir，以確保只會壓縮目前的版本

<a name="190"></a>1.9.0
---
* 已新增巴斯克文 (EU) 的當地語系化
* 已新增斯洛維尼亞文 (SL) 的當地語系化
* 已修正問題 #127：芬蘭文翻譯有一個 : 而不是 ;
* 已修正俄文的當地語系化，次要的語法問題
* 已新增對於 HTML5 輸入類型的支援，修正 #97
* 已藉由在表單中設定 novalidate 屬性，以及讀取類型屬性，來改進 HTML5 支援。
* 已修正從錯誤元素中移除所有類別的 showLabel() 只移除 settings.validClass。 修正 #151。
* 已將 'pattern' 新增至額外方法，以針對任意的規則運算式進行驗證。
* 已改進 email 方法，不允許結尾的句點 (透過 RFC 是有效的，但這裡不需要)。 修正 #143
* 已修正瑞典文和挪威文翻譯，已切換 min/max 訊息。 修正 #181
* 已修正 #184：resetForm：應該取消設定 lastElement
* 已修正 #71：改進現有的 time 方法，並新增適用於 12h am/pm 時間格式的 time12h 方法
* 已修正 #177：修正單一選項按鈕或核取方塊輸入的驗證
* 已修正 #189：現在預設會忽略 :hidden 元素
* 已修正 #194：如果 jQuery>=1.6 而導致屬性失敗時為必要的；使用 .prop 而不是 .attr
* 已修正 #47、#39、#32：已允許信用卡號碼包含空格以及連字號 (空格通常是由使用者輸入)。

<a name="181"></a>1.8.1
---
* 已新增泰文 (TH) 的當地語系化，修正 #85
* 已新增越南文 (VI) 的當地語系化，感謝 Ngoc
* 已修正問題 #78。 錯誤/有效的樣式會套用至需要驗證之相同群組的所有選項按鈕。
* 請勿使用 form.elements，因為 jQuery 1.6 中已不再支援。 無論如何還是有很多設計錯誤 (IE6-8: form.elements === form)。

<a name="180"></a>1.8.0
---
* 已改進 NL 當地語系化 (http://plugins.jquery.com/node/14120)
* 已新增喬治亞文 (GE) 的當地語系化，感謝 Avtandil Kikabidze
* 已新增塞爾維亞文 (SR) 的當地語系化，感謝 Aleksandar Milovac
* 已將 ipv4 和 ipv6 新增至額外方法，感謝 Natal Ngétal
* 已新增日文 (JA) 的當地語系化，感謝 Bryan Meyerovich
* 已新增加泰蘭文 (CA) 的當地語系化，感謝 Xavier de Pedro
* 已修正 for-in 迴圈內遺漏的 var 陳述式
* 修正遠端驗證，其中有格式化的訊息發生問題 (https://github.com/jzaefferer/jquery-validation/issues/11)
* 與 jQuery 1.5.1 之相容性的錯誤修正，同時維持回溯相容性

<a name="17"></a>1.7
---
* 已新增立陶宛文 (LT) 的當地語系化
* 已新增希臘文 (EL) 的當地語系化 (http://plugins.jquery.com/node/12319)
* 已新增拉脫維亞文 (LV) 的當地語系化 (http://plugins.jquery.com/node/12349)
* 已新增希伯來文 (HE) 的當地語系化 (http://plugins.jquery.com/node/12039)
* 已修正西班牙文 (ES) 的當地語系化 (http://plugins.jquery.com/node/12696)
* 已新增 jQuery UI themerolled 示範
* 已移除 cmxform.js
* 已修正四個遺漏分號 (http://plugins.jquery.com/node/12639)
* 已將 additional-methods.js 中的 phone-method 重新命名為 phoneUS
* 已將 phoneUK 和 mobileUK 方法新增至 additional-methods.js (http://plugins.jquery.com/node/12359)
* 深入擴充選項，以避免在單一元素上使用 rules 方法時修改多個表單 (http://plugins.jquery.com/node/12411)
* 與 jQuery 1.4.2 之相容性的錯誤修正，同時維持回溯相容性

<a name="16"></a>1.6
---
* 已新增阿拉伯文 (AR)、葡萄牙文 (PTPT)、波斯文 (FA)、芬蘭文 (FI) 和保加利亞文 (BR) 的當地語系化
* 已更新瑞典文 (SE) 的當地語系化 (某些遺漏的 html iso 字元)
* 已修正 $.validator.addMethod，以針對訊息引數適當地處理空字串與未定義的項目
* 已修正兩個附屬的全域變數
* 已增強 min/max/rangeWords (位於 additional-methods.js) 在計數之前刪除 html；在 richtext 編輯器中計算文字時很有用
* 已新增 DE、NL 及 PT 的當地語系化方法，移除 dateDE 和 numberDE 方法 (改用 messages_de.js 和 methods_de.js 搭配 date 和 number 方法)
* 已修正遠端表單提交同步處理，感謝 Matas Petrikas
* 已改進互動式選取驗證，現在也會在按一下時驗證 (透過選項或選取，瀏覽器之間是不一致的)；無法在 Safari 中運作，其完全不會在 select 元素上觸發 click 事件；修正 http://plugins.jquery.com/node/11520
* 更新為最新的表單外掛程式 (2.36)，將修正 http://plugins.jquery.com/node/11487
* 繫結至 equalTo 目標的 blur 事件，在該目標變更時進行重新驗證，修正 http://plugins.jquery.com/node/11450
* 已簡化選取驗證，委派給 jQuery 的 val() 方法以取得選取值；應該修正 http://plugins.jquery.com/node/11239
* 已修正數字的預設訊息 (http://plugins.jquery.com/node/9853)
* 已修正快取遠端郵件的問題 (http://plugins.jquery.com/node/11029 和 http://plugins.jquery.com/node/9351)
* 已修正 additional-methods.js 中遺漏的分號 (http://plugins.jquery.com/node/9233)
* 已在訊息中新增替代參數的自動偵測，不需提供格式函式 (http://plugins.jquery.com/node/11195)
* 已修正可能因為 Sizzle 而造成 :filled/:blank 的問題 (http://plugins.jquery.com/node/11144)
* 已將 integer 方法新增至 additional-methods.js (http://plugins.jquery.com/node/9612)
* 已修正 errorsFor 方法，其中的 for-attribute 包含需要在選取器內逸出為有效的字元 (http://plugins.jquery.com/node/9611)

<a name="155"></a>1.5.5
---
* 修正 http://plugins.jquery.com/node/8659
* 已修正 messages_cs.js 中的結尾逗號

<a name="154"></a>1.5.4
---
* 已修正遠端方法錯誤 (http://plugins.jquery.com/node/8658)

<a name="153"></a>1.5.3
---
* 已修正與包裝函式選項相關的錯誤，其中選取了所有符合包裝函式選項的上階元素 (http://plugins.jquery.com/node/7624)
* 已更新 multipart 示範，以使用最新的 jQuery UI accordion
* 已將 dateNL 和 time 方法新增至 additionalMethods.js
* 已新增繁體中文 (台灣, tw) 和哈薩克文 (KK) 的當地語系化
* 已將 jQuery.format (先前為 String.format) 移至 jQuery.validator.format，jQuery.format 已被取代，將在 1.6 中移除 (如需詳細資訊，請參閱 http://code.google.com/p/jquery-utils/issues/detail?id=15)
* 已清除 messages_pl.js 和 messages_ptbr.js (仍已定義 max/min/rangeValue 的訊息，其已在 1.4 中移除)
* 已針對多個元素修正有效外掛程式方法中有缺陷的布林邏輯；現在所有元素對於布林值 true 結果而言都必須是有效的 (http://plugins.jquery.com/node/8481)
* 增強 $.validator.addmethod:未定義第三個訊息引數不會覆寫現有的訊息 （ http://plugins.jquery.com/node/8443)
* SubmitHandler 選項的增強功能：使用時，按一下 事件提交按鈕會擷取並送出按鈕是插入表單，然後再呼叫 submitHandler，之後加以移除;保留提交按鈕保持不變 （ http://plugins.jquery.com/node/7183#comment-3585)
* 已新增選項 validClass (預設 "valid")，在驗證之後，將該類別新增至所有有效元素 (http://dev.jquery.com/ticket/2205)
* 已將 creditcardtypes 方法新增至 additionalMethods.js，包括測試 (透過 http://dev.jquery.com/ticket/3635)
* 已改進遠端方法以允許字串形式的伺服器端訊息，或者使用用戶端定義的訊息，有效為 true，無效則為 false (http://dev.jquery.com/ticket/3807)
* 已改進 accept 方法，也會接受 Drupal 樣式且以逗點分隔的值清單 (http://plugins.jquery.com/node/8580)

<a name="152"></a>1.5.2
---
* 已在 additional-methods.js 中針對 maxWords、minWords 和 rangeWords 修正訊息，以包含 $.format 的呼叫
* 已修正傳遞至方法的值，以排除歸位字元 (\r)，與 jQuery 的 val() 所做的一樣
* 已新增斯洛伐克文 (sk) 的當地語系化
* 已新增與 jQuery UI 索引標籤整合的示範
* 已將 selects-grouping 範例新增至 tabs 示範 (請參閱第二個索引標籤，出生日期欄位)

<a name="151"></a>1.5.1
---
* 已更新 marketo 示範，以使用 invalidHandler 選項而不是繫結 invalid-form 事件
* 已新增 TinyMCE 整合範例
* 已新增烏克蘭文 (ua) 的當地語系化
* 已修正長度驗證以使用修剪過的值 (從 1.5 迴歸，其中移除了驗證之前所進行的一般修剪)
* 針對 1.2.6 和 1.3 之相容性的各種小修正

<a name="15"></a>1.5
---
* 已改進基本示範，在變更密碼之後，驗證確認密碼欄位
* 已修正基本驗證，將未修剪的輸入值當作第一個參數傳遞至驗證方法，並據以進行所需的變更；中斷依賴修剪的現有自訂方法
* 已新增挪威文 (no)、義大利文 (it)、匈牙利文 (hu) 和羅馬尼亞文 (ro) 的當地語系化
* 已修正的 # 3195:瑞典文當地語系化中的兩個缺點
* 已修正的 # 3503:擴充 rules 來接受訊息屬性： 使用指定透過規則的項目中加入自訂訊息 ("add"，{訊息: {需要："Required ！ " } });
* 已修正的 # 3356:從 #2908 使用中繼選項時的迴歸
* 已修正的 # 3370:已新增的 ignoreTitle 選項，設定要略過的 title 屬性讀取訊息有助於避免發生問題，Google 工具列;預設值為 false 的相容性
* 已修正的 # 3516:觸發程序 invalid-form 事件，即使牽涉到遠端驗證
* 已將 invalidHandler 選項當作捷徑新增至 bind("invalid-form", function() {})
* 已修正在 ajaxSubmit-integration-demo 中載入指標的 Safari 問題 (先附加至主體，然後隱藏)
* 已新增信用卡驗證的測試，並已改進預設訊息
* 已增強遠端驗證，接受選項以傳遞至 $.ajax 作為參數 (url 字串或選項，包括 url 屬性加上 $.ajax 支援的其他所有項目)

<a name="14"></a>1.4
---
* 已修正 #2931，驗證文件順序中的元素，並忽略 type=image 輸入
* 已修正 $ 和 jQuery 變數的使用方式，現在與 noConflict 使用方式的所有變化完全相容
* 已實作 #2908，啟用透過中繼資料 ala class="{required:true,messages:{required:'required field'}}" 啟用自訂訊息，已新增 demo/custom-messages-metadata-demo.html
* 已移除已被取代的方法 minValue (min)、maxValue (max)、rangeValue (rangevalue)、minLength (minlength)、maxLength (maxlength)、rangeLength (rangelength)
* 已修正的 # 2215年迴歸分析：呼叫 unhighlight，只針對目前的項目，不是所有項目
* 已實作 # 2989，啟用影像按鈕以取消驗證
* 已修正 IE 根據 maxlength=0 進行不正確驗證的問題
* 已新增捷克文 (cs) 的當地語系化
* 重設 validator.resetForm() 上的 validator.submitted，必要時啟用完整重設
* 已修正 #3035，在讀取規則時略過所有假的屬性 (0、未定義的、空字串)，已移除部分的 maxlength 因應措施 (針對 0)
* 已新增荷蘭文 (nl) 的當地語系化 (#3201)

<a name="13"></a>1.3
---
* 已修正 invalid-form 事件，現在只會在表單無效時觸發
* 已新增西班牙文 (es)、俄文 (ru)、葡萄牙文 (巴西) (ptbr)、土耳其文 (tr) 和波蘭文 (pl) 的當地語系化
* 已新增 removeAttrs 外掛程式，以便新增和移除多個屬性
* 已新增 groups 選項，透過 groups: { arbitraryGroupName: "fieldName1 fieldName2[, fieldNameN" } 來顯示多個元素的單一訊息
* 已增強用於新增和移除 (靜態) 規則的 rules()：rules("add", "method1[, methodN]"/{method1:param[, method_n:param]}) and rules("remove"[, "method1[, method_n]")
* 已增強 rules 選項，接受方法的字串清單 (以空格分隔)，例如 {birthdate: "required date"}
* 已修正利用內嵌規則的核取方塊群組驗證：只要在第一個項目上指定的規則，該群組是現在 click 上正確驗證
* 已修正 #2473，略過具有布林值 false 之明確參數的所有規則，例如， required:false 相當於完全未指定 required (到目前為止，會將它當成 required:true 來處理)
* 已修正的 # 2424 具有已修改的修補程式，從 # 2473年:傳回相依性不相符的方法不停止再; 評估其他規則儘管如此，成功不會為選擇性欄位套用
* 已修正 url 和電子郵件驗證，不使用修剪過的值
* 已修正信用卡驗證，只接受數字和連字號 ("asdf"不是有效的信用卡號碼)
* 允許取消按鈕的按鈕和輸入元素 (透過 class="cancel")
* 已修正的 # 2215:已修正的訊息顯示呼叫 unhighlight 一部分顯示和隱藏訊息，沒有更多視覺化副作用檢查元素和已擷取的 validator.checkForm，以驗證沒有 UI 副作用的表單
* 使用函式重寫自訂選取器 (:blank、:filled、:unchecked)，以取得與 AIR 的相容性

<a name="121"></a>1.2.1
-----

* 已將委派外掛程式與驗證外掛程式配套；無論如何，一定要這樣做
* 已改進遠端驗證來包含 ajaxQueue 外掛程式的組件，以便進行適當的同步處理 (不需要其他外掛程式)
* 已修正 stopRequest 以避免 pendingRequest < 0
* 已新增 jQuery.validator.autoCreateRanges 屬性預設為 false，啟用以將 min/max 轉換為 range，並將 minlength/maxlength 轉換為 rangelength；這基本上會修正 1.2 中自動建立範圍所引進的問題
* 已修正選擇性方法，在欄位空白時完全不要反白顯示任何項目，也就是不要觸發 success
* 允許 highlight/unhighlight 選項的 false/null，而不是強制執行 do-nothing 回呼，即使不需要反白顯示任何項目時也一樣
* 已修正未選取任何元素的 validate() 呼叫，傳回 undefined，而不是擲回錯誤
* 已改進示範，使用類別/屬性來取代中繼資料以用來指定規則
* 已修正在未使用任何自訂訊息進行遠端驗證時所發生的問題
* 已修改電子郵件和 url 驗證以要求網域標籤和頂端標籤
* 已修正 url 和電子郵件驗證以要求 TLD (實際上需要網域標籤)；已將 1.2 版 (TLD 是選擇性的) 移至新增項目作為 url2 和 email2
* 已修正 IE6/7 中的 dynamic-totals 示範，並已改進範本，以使用 textarea 來儲存多行範本和字串內插補點
* 已利用「電子郵件密碼」連結新增登入表單範例，其會使密碼欄位成為選擇性的
* 已利用適用於兩個欄位的單一訊息範例來增強 dynamic-totals 示範

<a name="12"></a>1.2
---

* 已新增 AJAX-captcha 驗證範例 (根據 http://psyrens.com/captcha/)
* 已新增 remember-the-milk 示範 (感謝 RTM 小組提供權限！)
* 已新增 marketo 示範 (感謝 Glen Lipka！)
* 已新增對於 ajax 驗證的支援，請參閱方法 "remote"；伺服器端會傳回 JSON，針對有效元素為 true，針對無效元素則為 false 或字串，字串可用來作為訊息
* 已新增 highlight 和 unhighlight 選項，根據預設，會在元素上切換 errorClass，允許自訂反白顯示
* 已新增 valid() 外掛程式方法，以程式設計方式對表單和欄位進行簡單的檢查，而不需使用驗證程式 API
* 已新增 rules() 外掛程式方法來讀取和寫入元素 (目前是唯讀) 的規則
* 已取代 email 方法的 regex，感謝 Scott Gonzalez 的貢獻，請參閱 http://projects.scottsplayground.com/email_address_validation/
* 已重建事件架構以便只依賴委派，同時改進效能，讓開發人員能夠輕鬆使用 (需要 jquery.delegate.js)
* 已將文件從內嵌移至 http://docs.jquery.com/Plugins/Validation - 包括所有方法的互動式範例
* 已移除 validator.refresh()，驗證現在是完全動態的
* 已將 minValue 重新命名為 min、maxValue 為 max，而 rangeValue 為 range，淘汰先前的名稱 (要在 1.3 中移除)
* 已將 minLength 重新命名為 minlength、maxLength 為 maxlength，而 rangeLength 為 rangelength，淘汰先前的名稱 (要在 1.3 中移除)
* 已新增功能以將 min + max 合併到 range，將 minlength + maxlength 合併到 rangelength
* 已新增動態規則參數的支援，允許指定函式作為參數，例如， 針對 minlength，在驗證元素時呼叫
* 允許指定 null 或空字串作為不會顯示任何內容的訊息 (請參閱 marketo 示範)
* 規則檢修：現在支援 rules 選項、 中繼資料、 類別 （新） 及組合屬性 （新），請參閱 rules，如需詳細資訊

<a name="112"></a>1.1.2
---

* 已取代 email 方法的 regex，感謝 Scott Gonzalez 的貢獻，請參閱 http://projects.scottsplayground.com/iri/
* 已改進 email 方法，可更妥善地處理 unicode 字元
* 已修正當所有元素都有效時 (而不是只在表單提交上) 要隱藏的錯誤容器
* 已將 String.format 修正為 jQuery.format (正在移到 jQuery 命名空間)
* 已修正 accept 方法，以接受大寫和小寫的擴充功能
* 已修正 validate() 外掛程式方法，針對指定的表單只建立一個驗證程式執行個體，且一律會傳回該執行個體 (避免多次繫結事件)
* 已將偵錯模式主控台記錄從「錯誤」變更為「警告」層級

<a name="111"></a>1.1.1
-----

* 已修正無效的 XHTML，防止從 jQuery 1.1.4 開始，在 IE 中建立錯誤標籤
* 已修正和改進 String.format:全域搜尋和取代，更妥善地處理陣列引數
* 已修正取消按鈕處理，以使用驗證程式物件來儲存狀態，而不是表單元素
* 已修正名稱選取器來處理「複雜」名稱，例如， 包含方括號 ("list[]")
* 已新增要在驗證時排除的按鈕和已停用元素
* 已移動要重新整理的元素事件處理常式，以便能夠將處理常式新增至新元素
* 已修正電子郵件驗證以允許長名稱的最上層網域 (例如 ".travel")
* 已將 showErrors() 從 valid() 移至 form()
* 已新增 validator.size()：傳回目前的錯誤數目
* 呼叫 submitHandler 並使用驗證程式作為範圍，以便更容易存取它的方法，例如， 使用 errorsFor(Element) 尋找錯誤標籤
* 與 jQuery 1.1.x 和 1.2.x 相容

<a name="11"></a>1.1
---

* 已新增 blur、keyup 及 click 的驗證 (適用於核取方塊和選項按鈕)。 取代事件選項。
* 已修正 resetForm
* 已修正 custom-methods-demo

<a name="10"></a>1.0
---

* 已改進 number 和 numberDE 方法，來檢查具有分隔符號的正確十進位數字
* 只會檢查具有規則的元素 (否則會將 success 選項套用至所有元素)
* 已新增信用卡號碼方法 (感謝 Brian Klug)
* 已新增 ignore 選項，例如 ignore: "[@type=hidden]"，使用該運算式來排除要驗證的元素。 預設值：none，儘管一律會忽略提交和重設按鈕
* 已藉由提供彈性的 String.format 協助程式，大幅增強「函式即訊息」
* 接受「函式即訊息」，提供執行階段自訂訊息
* 已修正從 successList 中排除不具規則的元素
* 已修正 custom-method-demo，使用顯示錯誤數目的訊息來取代警示
* 已修正在使用 submitHandler 時防止提交表單
* 已完全移除元素識別碼上的相依性，儘管仍會使用它們 (如果存在) 來將錯誤標籤連結至輸入。 已藉由針對內部 errorList 搭配 {name, message, element} 使用陣列，而不是具有 id:message 配對的物件來達成。
* 已新增使用簡單字串來指定簡單規則的支援，例如， "required" 相當於 {required: true}
* 已新增的功能：ErrorClass 加入無效的欄位的父項目，輕鬆地設定樣式標籤/欄位容器或欄位的標籤。
* 已新增功能：focusCleanup：如果啟用，就會從無效元素移除 errorClass，每當該元素取得焦點時，就會隱藏所有錯誤訊息。
* 已新增 success 選項，以顯示欄位已成功驗證
* 已修正 Opera 選取問題 (避免發生屬性衝突)
* 已修正 IE 中隱藏元素取得焦點的問題
* 已新增功能，以略過對於類別為 "cancel" 之提交按鈕的驗證
* 已修正 Google 工具列的潛在問題，方法是在 title 屬性上偏好使用外掛程式選項訊息
* 只有在已處理實際的 submit 事件時才會呼叫 submitHandler，validator.form() 只會對無效的表單傳回 false
* 無效的元素現在只會在 submit 上或透過 validator.focusInvalid() 取得焦點，以避免所有模糊焦點的問題
* IE6 錯誤容器版面配置問題已解決
* 透過 errorElement 選項自訂錯誤項目
* 已新增 validator.refresh()，以便在表單中尋找新的輸入
* 已新增接受驗證方法，檢查副檔名
* 已藉由新增兩個自訂運算式，改進了相依性功能：":blank" 會選取具有空白值的項目，而 :filled 會選取已有值的項目，兩者都會不會包含空格
* 加入驗證程式 resetform （） 方法：（如果有的話，請使用表單外掛程式，） 的每個格式項目會重設、 移除無效的項目上的類別，並隱藏所有錯誤訊息
* 已修正 Validator.showErrors() 的文件
* 已修正錯誤標籤建立，一律使用 html() 而不是 text()，允許傳入任意 HTML 作為訊息
* 已修正錯誤標籤建立以使用指定的錯誤類別
* 已新增相依性功能：Requires 方法會接受 String （jQuery 運算式） 和函式作為引數
* 大幅改進錯誤訊息顯示的自訂：使用一般的訊息，顯示/隱藏額外的容器;（同時能夠委派到預設的處理常式; own 機制完全取代訊息顯示自訂產生的標籤 （而不是以下預設的元素） 的放置
* 已修正 IE (錯誤容器) 和 Opera (中繼資料) 中的兩個主要 bug
* 已修正驗證方法，可接受空白欄位為有效項目 (例外狀況：required 及 equalTo 方法)
* 將 "min" 重新命名為 "minLength"、"max" 為 "maxLength"、"length" 為 "rangeLength"
* 已新增 "minValue"、"maxValue" 和 "rangeValue"
* 已簡化 API 來支援不同的事件。 您可以停用預設值 submit。 如果指定了任何事件，就會將其套用至每個元素 (而不是整個表單)。 將 Keyup 驗證與提交驗證相結合，現在非常容易設定
* 已新增在透過外掛程式設定定義訊息時對於每個規則一個訊息的支援
* 已新增在某些父元素中包裝中繼資料的支援。 將中繼資料用於其他外掛程式時也很有用。
* 重構的測試及示範：檔案越少，更好的示範
* 改良的說明文件：方法的其他範例，更多參考文字說明一些基本知識
