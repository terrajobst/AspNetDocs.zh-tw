---
uid: whitepapers/request-validation
title: 要求驗證-防止腳本攻擊 |Microsoft Docs
author: rick-anderson
description: 本檔說明 ASP.NET 的要求驗證功能，根據預設，應用程式無法處理未編碼的 HTML 內容 submitt 。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: fa429113-5f8f-4ef4-97c5-5c04900a19fa
msc.legacyurl: /whitepapers/request-validation
msc.type: content
ms.openlocfilehash: 807cccd6fe1acdd6359b014387abd3878840d4cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640844"
---
# <a name="request-validation---preventing-script-attacks"></a>要求驗證 - 防止指令碼攻擊

> 本檔描述 ASP.NET 的要求驗證功能，其中，應用程式預設會防止處理提交至伺服器的未編碼 HTML 內容。 當應用程式設計成安全地處理 HTML 資料時，可以停用此要求驗證功能。
> 
> 適用于 ASP.NET 1.1 和 ASP.NET 2.0。

要求驗證 (1.1 版後的 ASP.NET 功能) 可防止伺服器接受包含未編碼 HTML 的內容。 這項功能設計用來協助防止某些指令碼資料隱碼攻擊，因此不知不覺地將用戶端指令碼或 HTML 提交至伺服器、加以儲存，而後呈現給其他使用者。 我們仍強烈建議您驗證所有輸入資料，而且適時進行 HTML 編碼。

例如，您建立的網頁會要求使用者的電子郵件地址，然後將該電子郵件地址儲存在資料庫中。 如果使用者輸入 &lt;腳本&gt;警示（"hello from SCRIPT"）&lt;/SCRIPT&gt; 而不是有效的電子郵件地址，則在呈現該資料時，如果未正確編碼內容，則可以執行此腳本。 ASP.NET 的要求驗證功能可防止發生這種情況。

## <a name="why-this-feature-is-useful"></a>這項功能很有用的原因

許多網站並不知道它們已開放給簡單的腳本插入式攻擊。 無論這些攻擊的目的是要藉由顯示 HTML 來 deface 網站，還是可能執行用戶端腳本將使用者重新導向駭客的網站，腳本插入式攻擊就是 Web 開發人員必須對抗的問題。

腳本插入式攻擊是所有 網頁程式開發人員的顧慮，無論是使用 ASP.NET、ASP 或其他 網頁程式開發技術。

ASP.NET 要求驗證功能藉由不允許伺服器處理未編碼的 HTML 內容，而主動預防這些攻擊，除非開發人員決定允許該內容。

## <a name="what-to-expect-error-page"></a>預期的內容：錯誤頁面

下列螢幕擷取畫面顯示一些範例 ASP.NET 程式碼：

![](request-validation/_static/image1.png)

執行此程式碼會產生一個簡單的頁面，讓您在文字方塊中輸入一些文字，按一下按鈕，然後在 [標籤] 控制項中顯示文字：

![](request-validation/_static/image2.png)

不過，是 JavaScript，例如輸入和提交 `<script>alert("hello!")</script>`，我們會收到例外狀況：

![](request-validation/_static/image3.png)

錯誤訊息指出「可能有危險的要求。偵測到表單值」，並在描述中提供更多詳細資料以瞭解發生了什麼事，以及如何變更行為。 例如:

要求驗證偵測到潛在危險的用戶端輸入值，而且要求的處理已中止。 這個值可能表示嘗試危害應用程式的安全性，例如跨網站腳本攻擊。 您可以藉由在頁面指示詞或設定區段中設定 `validateRequest=false`，來停用要求驗證。 不過，強烈建議您的應用程式在此情況下明確檢查所有輸入。

## <a name="disabling-request-validation-on-a-page"></a>停用頁面上的要求驗證

若要停用頁面上的要求驗證，您必須將 Page 指示詞的 `validateRequest` 屬性設定為 `false`：

[!code-aspx[Main](request-validation/samples/sample1.aspx)]

> [!CAUTION]
> 停用要求驗證時，可以將內容提交至頁面;網頁開發人員必須負責確保內容經過正確編碼或處理。

## <a name="disabling-request-validation-for-your-application"></a>停用應用程式的要求驗證

若要停用應用程式的要求驗證，您必須修改或建立應用程式的 web.config 檔案，並將 `<pages />` 區段的 validateRequest 屬性設定為 `false`：

[!code-xml[Main](request-validation/samples/sample2.xml)]

如果您想要停用伺服器上所有應用程式的要求驗證，可以對您的 Machine.config 檔案進行這種修改。

> [!CAUTION]
> 停用要求驗證時，可以將內容提交至您的應用程式;應用程式開發人員必須負責確保正確編碼或處理內容。

下列程式碼已修改為關閉要求驗證：

![](request-validation/_static/image4.png)

現在，如果已在文字方塊中輸入下列 JavaScript `<script>alert("hello!")</script>` 結果會是：

![](request-validation/_static/image5.png)

為了避免發生這種情況，在關閉要求驗證的情況下，我們需要對內容進行 HTML 編碼。

## <a name="how-to-html-encode-content"></a>如何 HTML 編碼內容

如果您已停用要求驗證，則對將儲存供日後使用的內容進行 HTML 編碼是很好的作法。 HTML 編碼會自動將任何 '&lt;' 或 '&gt;' （連同其他數個符號）取代為其對應的 HTML 編碼表示。 例如，'&lt;' 已由 '&amp;lt; ' 取代，而 '&gt;' 已由 '&amp;gt; ' 取代。 瀏覽器會使用這些特殊代碼，在瀏覽器中顯示 '&lt;' 或 '&gt;'。

您可以使用 `Server.HtmlEncode(string)` API，輕鬆地在伺服器上以 HTML 編碼內容。 內容也可以輕易地進行 HTML 解碼，也就是使用 `Server.HtmlDecode(string)` 方法還原為標準 HTML。

![](request-validation/_static/image6.png)

產生的結果：

![](request-validation/_static/image7.png)
