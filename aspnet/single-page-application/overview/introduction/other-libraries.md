---
uid: single-page-application/overview/introduction/other-libraries
title: 是否認識 Knockout 以外的程式庫？ | Microsoft Docs
author: madskristensen
description: 是否認識 Knockout 以外的程式庫？
ms.author: riande
ms.date: 02/05/2013
ms.assetid: a8367c6d-ef94-4dff-a010-5eff9e6eea96
msc.legacyurl: /single-page-application/overview/introduction/other-libraries
msc.type: authoredcontent
ms.openlocfilehash: 64a4ad1fb411f7291a5cba634afdf4d2fdb16d55
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578544"
---
# <a name="know-a-library-other-than-knockout"></a>是否認識 Knockout 以外的程式庫？

依[Mads Kristensen](https://github.com/madskristensen)

[單頁應用程式（SPA）範本](knockoutjs-template.md)是開始撰寫單一頁面應用程式的絕佳方式。 此範本會使用[KnockoutJS](http://knockoutjs.com/)將應用程式資料系結至 DOM 元素。

但是，挖不是用來建立豐富型用戶端應用程式的唯一 JavaScript 程式庫。 其他程式庫會以不同的方式解決類似的挑戰。 您可能偏好使用一個程式庫，因此我們建立了數個以社區建立的範本供您下載。 這些範本各自使用不同的用戶端 JavaScript 程式庫混合。

若要安裝已建立社區的範本，請造訪下面所列的其中一個範本頁面，然後按一下 [下載] 按鈕。 範本會以 VSIX 檔案的形式提供。

## <a name="backbonejs"></a>BackboneJS

[骨幹 SPA 範本](../templates/backbonejs-template.md)。 此範本提供在 ASP.NET MVC 中開發[骨幹](http://backbonejs.org/)應用程式的初始基本架構。 它提供基本的使用者登入功能，包括使用者註冊、登入、密碼重設，以及使用基本電子郵件範本的使用者確認。

## <a name="breezejs"></a>BreezeJS

[BreezeJS](http://www.breezejs.com/?utm_source=ms-spa)是一個開放原始碼程式庫，可用於管理 JavaScript 用戶端中的豐富資料。 輕鬆處理查詢、快取、變更追蹤、驗證等。 有兩個範本功能輕鬆：

- 「簡單」 [/「挖](../templates/breezeknockout-template.md)後」範本會延伸「挖式 SPA」範本，顯示您可以輕鬆地建立單一頁面應用程式，方便資料管理及 KnockoutJS 資料系結。
- 「簡單」 [/「角度](../templates/breezeangular-template.md)」範本也會輕鬆擴充挖式 SPA 範本，但使用[AngularJS](http://angularjs.org)程式庫來進行資料系結、相依性插入和螢幕管理。

此外，「[熱門紙巾 SPA」範本](../templates/hottowel-template.md)會使用 BreezeJS。

## <a name="emberjs"></a>EmberJS

[EMBERJS SPA 範本](../templates/emberjs-template.md)。 此範本使用[ember.js](http://emberjs.com/)，這是功能強大的 MVC JavaScript 程式庫，可解決建立豐富型用戶端應用程式的各種挑戰。

Ember.js SPA 範本是使用 EmberJS 和 Handlebars 範本化的「挖後 SPA」範本重新執行。

## <a name="hot-towel"></a>熱門紙巾

[熱門紙巾 SPA 範本](../templates/hottowel-template.md)。 此範本引進數個 JavaScript 程式庫，包括輕鬆、挖的、RequireJS 和 Twitter 啟動程式。

相較于此處所列的其他範本，「熱門的紙巾」範本提供了更完整的應用程式，讓您可以從中建立。 還有更多要注意的概念，但一旦您瞭解，此範本可能只是您要尋找的專案。 如果您想要建立 SPA，但無法決定要從何處開始，請使用「熱門的紙巾」，並在幾秒內建立您需要的 SPA 和所有工具。

## <a name="feature-table"></a>功能資料表

以下是每個 SPA 範本所提供的功能：

|                        | ASP.NET SPA | 骨幹 | 輕而易舉/角度 | 輕鬆/KO |  Ember.js   | 熱門紙巾 |
|------------------------|-------------|----------|----------------|-----------|----------|-----------|
|      ToDo 範例       |  &#10003;   |          |    &#10003;    | &#10003;  | &#10003; |           |
|     裸機範本      |             | &#10003; |                |           |          | &#10003;  |
| 導覽和歷程記錄 |             | &#10003; |    &#10003;    |           | &#10003; | &#10003;  |
|        程式庫       |             |          |                |           |          |           |
|        Angular         |             |          |    &#10003;    |           |          |           |
|    &#8195;骨幹     |             | &#10003; |                |           |          |           |
|         輕而易舉         |             |          |    &#10003;    | &#10003;  |          | &#10003;  |
|        durandal 等架構        |             |          |                |           |          | &#10003;  |
|         Ember.js          |             |          |                |           | &#10003; |           |
|        Knockout        |  &#10003;   |          |                | &#10003;  |          | &#10003;  |
