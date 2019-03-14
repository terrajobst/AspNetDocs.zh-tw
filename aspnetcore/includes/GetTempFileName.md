---
ms.openlocfilehash: 2cd201e16cd491d0f468e8ef141b522f1694a257
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57165852"
---
**警告**:下列程式碼會使用`GetTempFileName`，哪些則會擲回`IOException`如果會建立超過 65535 的檔案，而不會刪除先前的暫存檔案。 實際的應用程式應該刪除暫存檔案，或使用 `GetTempPath` 和 `GetRandomFileName` 建立暫存檔案名稱。 65535 為以伺服器為依據的檔案限制數，因此伺服器上的另一個應用程式可以用掉所有 65535 個檔案。 
