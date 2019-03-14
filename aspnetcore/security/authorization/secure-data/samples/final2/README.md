---
ms.openlocfilehash: e40d28e9a7ca12efe45988fabef23dece893d428
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049105"
---
# <a name="how-to-buildrun-secure-user-data-sample"></a><span data-ttu-id="31794-101">如何建置/執行安全的使用者資料範例</span><span class="sxs-lookup"><span data-stu-id="31794-101">How to build/run Secure user data sample</span></span>

* <span data-ttu-id="31794-102">使用 Secret Manager 工具設定密碼：</span><span class="sxs-lookup"><span data-stu-id="31794-102">Set password with the Secret Manager tool:</span></span>

  `dotnet user-secrets set SeedUserPW <pw>`

* <span data-ttu-id="31794-103">更新資料庫：</span><span class="sxs-lookup"><span data-stu-id="31794-103">Update the database:</span></span>

    `dotnet ef database update`

* <span data-ttu-id="31794-104">在專案中啟用 HTTPS</span><span class="sxs-lookup"><span data-stu-id="31794-104">Enable HTTPS in the project</span></span>
