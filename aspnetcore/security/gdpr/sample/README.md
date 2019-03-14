---
ms.openlocfilehash: 96cd8c78178b02ad3eb4a471540950b4581af583
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57033375"
---
# <a name="gdpr-sample"></a>GDPR 範例

* 在*appsettings.json*，將`CheckNotConsentNeeded`到`false`以要求同意; 否則設定為 true 或 略過。 測試應用程式與`CheckNotConsentNeeded`設定為`false`並將設定為`true`。
* 建立的每個變化的基本和非必要的 cookie`CheckConsentNeeded`和授與同意。
* 註冊的使用者。
* 刪除 cookie。
