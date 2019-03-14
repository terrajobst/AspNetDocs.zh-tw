---
ms.openlocfilehash: e40d28e9a7ca12efe45988fabef23dece893d428
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049105"
---
# <a name="how-to-buildrun-secure-user-data-sample"></a>如何建置/執行安全的使用者資料範例

* 使用 Secret Manager 工具設定密碼：

  `dotnet user-secrets set SeedUserPW <pw>`

* 更新資料庫：

    `dotnet ef database update`

* 在專案中啟用 HTTPS
