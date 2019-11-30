---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
title: 對抗 Bot （C#） |Microsoft Docs
author: wenz
description: 自動化機器人會 plaster weblog 和其他具有垃圾郵件的網站，並在沒有任何使用者互動的情況下提交留言表單。 ASP.NET AJAX Con 中的 NoBot 控制項 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0a1917e0-884a-4576-8e93-9ed660faae51
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
msc.type: authoredcontent
ms.openlocfilehash: fef55edf12a024e4dd66e2a18ea371ab4dac861f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606424"
---
# <a name="fighting-bots-c"></a>對抗 Bot (C#)

依[Christian Wenz](https://github.com/wenz)

[下載程式代碼](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip)或[下載 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)

> 自動化機器人會 plaster weblog 和其他具有垃圾郵件的網站，並在沒有任何使用者互動的情況下提交留言表單。 ASP.NET AJAX 控制項工具組中的 NoBot 控制項可協助對抗這些 bot。

## <a name="overview"></a>概觀

自動化機器人會 plaster weblog 和其他具有垃圾郵件的網站，並在沒有任何使用者互動的情況下提交留言表單。 ASP.NET AJAX 控制項工具組中的 NoBot 控制項可協助對抗這些 bot。

## <a name="steps"></a>步驟

擊敗 bot 的一個常見方法是使用 CAPTCHAs 完全自動化的公用 Turing 測試，以告訴電腦和人類的與眾不同之處。 Turing 測試原本就是一種測試，其中有人需要決定通訊夥伴是人或電腦。 在 web 中，CAPTCHA 通常是由影像所組成，其中包含一些失真字母。 其概念是，只有人可以讀取影像上的字母，而 OCR 演算法將會失敗。

這種方法有幾個優點和缺點，但這項討論已超出本教學課程的範圍。 不過，ASP.NET AJAX 控制項工具組中的控制項提供類似的方法： `NoBot`。 比起 CAPTCHA 更容易克服，但是很容易就能使用和車資在類似 blog 的網站上，如果大部分的垃圾郵件嘗試都失效，`NoBot` 控制項就會被視為成功。

如果至少符合下列其中一個條件，`NoBot` 會攔截目前 ASP.NET web 表單的回傳：

- 瀏覽器無法解決 JavaScript 謎題（例如，當 JavaScript 停用時）
- 使用者已將表單提交到快速
- 用戶端 IP 位址在一段時間內提交表單的頻率太高。

若要檢查這些條件，`NoBot` 控制項需要這些屬性（全部都是選擇性的）：

- `ResponseMinimumDelaySeconds` 回傳之間的最小秒數
- `CutoffWindowSeconds` 某個 IP 的回傳為量值的時間間隔長度
- `CutoffMaximumInstances` 每個時間間隔的最大秒數

下列標記要求在回傳之間至少有兩秒鐘的時間，而且30秒間隔內只有五個回傳或小於：

[!code-aspx[Main](fighting-bots-cs/samples/sample1.aspx)]

然後，如同往常一般，請務必將 `ScriptManager` 包含在頁面中，以便載入 ASP.NET AJAX 程式庫，並使用控制項工具組：

[!code-aspx[Main](fighting-bots-cs/samples/sample2.aspx)]

由於大部分的檢查 `NoBot` 是在伺服器端進行，因此您必須檢查這些驗證的結果。 這可以藉由呼叫 `NoBot`的 `IsValid()` 方法來完成。 它有一個 `NoBotState`類型的引數（做為 `out` 參數/`ByRef` 參數）。 其字串標記法包含檢查失敗的原因，否則 `Valid`。 下列程式碼會根據 `NoBot`的結果來輸出訊息：

[!code-aspx[Main](fighting-bots-cs/samples/sample3.aspx)]

最後，您需要提交表單，並使用 label 元素來輸出訊息，而且您已完成！

[!code-aspx[Main](fighting-bots-cs/samples/sample4.aspx)]

當您執行此腳本並停用 JavaScript，或在前兩秒內提交表單，或在三十秒內提交表單七次時，您會收到錯誤訊息。 不過，請謹慎使用此控制項，因為只有大約有90-95% 的使用者已啟用 JavaScript，因此5-10% 的使用者將會失敗 `NoBot`的測試。

[![此錯誤訊息可能是 bot 所造成](fighting-bots-cs/_static/image2.png)](fighting-bots-cs/_static/image1.png)

此錯誤訊息可能是 bot 造成的（[按一下以觀看完整大小的影像](fighting-bots-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [下一步](fighting-bots-vb.md)
