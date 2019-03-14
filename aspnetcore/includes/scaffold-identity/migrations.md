---
ms.openlocfilehash: 4d6b6309e6e15c364542b5d3ae296d53c6ea4358
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037395"
---
<span data-ttu-id="787f0-101">產生的識別資料庫程式碼需要[Entity Framework Core 移轉](/ef/core/managing-schemas/migrations/)。</span><span class="sxs-lookup"><span data-stu-id="787f0-101">The generated Identity database code requires [Entity Framework Core Migrations](/ef/core/managing-schemas/migrations/).</span></span> <span data-ttu-id="787f0-102">建立移轉並更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="787f0-102">Create a migration and update the database.</span></span> <span data-ttu-id="787f0-103">例如，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="787f0-103">For example, run the following commands:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="787f0-104">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="787f0-104">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="787f0-105">在 Visual Studio **Package Manager Console**:</span><span class="sxs-lookup"><span data-stu-id="787f0-105">In the Visual Studio **Package Manager Console**:</span></span>

```PMC
Add-Migration CreateIdentitySchema
Update-Database
```

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="787f0-106">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="787f0-106">.NET Core CLI</span></span>](#tab/netcore-cli)

```cli
dotnet ef migrations add CreateIdentitySchema
dotnet ef database update
```

------

<span data-ttu-id="787f0-107">「 CreateIdentitySchema"name 參數，如`Add-Migration`是任意的命令。</span><span class="sxs-lookup"><span data-stu-id="787f0-107">The "CreateIdentitySchema" name parameter for the `Add-Migration` command is arbitrary.</span></span> <span data-ttu-id="787f0-108">`"CreateIdentitySchema"` 描述如何移轉。</span><span class="sxs-lookup"><span data-stu-id="787f0-108">`"CreateIdentitySchema"` describes the migration.</span></span>
