---
ms.openlocfilehash: 2481b10abae9aefce2d5173d8071e4c2236db928
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048215"
---

> [!NOTE]
> <span data-ttu-id="3559f-101">EF Core SQLite 提供者不支援許多結構描述變更作業。</span><span class="sxs-lookup"><span data-stu-id="3559f-101">Many schema change operations are not supported by the EF Core SQLite provider.</span></span> <span data-ttu-id="3559f-102">例如，其支援新增資料行，但不支援移除資料行。</span><span class="sxs-lookup"><span data-stu-id="3559f-102">For example, adding a column is supported, but removing a column is not supported.</span></span> <span data-ttu-id="3559f-103">如果要移除資料行中，建立移轉`ef migrations add`命令執行成功但`ef database update`命令就會失敗。</span><span class="sxs-lookup"><span data-stu-id="3559f-103">If a migration is created to remove a column, the `ef migrations add` command succeeds but the `ef database update` command fails.</span></span> <span data-ttu-id="3559f-104">其中某些限制可以克服手動撰寫資料表重建的移轉程式碼。</span><span class="sxs-lookup"><span data-stu-id="3559f-104">Some of these limitations can be overcome by manually writing migrations code to perform a table rebuild.</span></span> <span data-ttu-id="3559f-105">重建資料表牽涉到：</span><span class="sxs-lookup"><span data-stu-id="3559f-105">A table rebuild involves:</span></span>

>* <span data-ttu-id="3559f-106">重新命名現有的資料表。</span><span class="sxs-lookup"><span data-stu-id="3559f-106">Renaming the existing table.</span></span>
>* <span data-ttu-id="3559f-107">建立新的資料表。</span><span class="sxs-lookup"><span data-stu-id="3559f-107">Creating a new table.</span></span>
>* <span data-ttu-id="3559f-108">舊的資料表資料複製到新的資料表。</span><span class="sxs-lookup"><span data-stu-id="3559f-108">Copying data from the old table to the new table.</span></span>
>* <span data-ttu-id="3559f-109">卸除舊的資料表。</span><span class="sxs-lookup"><span data-stu-id="3559f-109">Dropping the old table.</span></span>

<span data-ttu-id="3559f-110">如需詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="3559f-110">For more information, see the following resources:</span></span>
> * [<span data-ttu-id="3559f-111">SQLite EF Core 資料庫提供者限制</span><span class="sxs-lookup"><span data-stu-id="3559f-111">SQLite EF Core Database Provider Limitations</span></span>](/ef/core/providers/sqlite/limitations)
> * [<span data-ttu-id="3559f-112">自訂移轉程式碼</span><span class="sxs-lookup"><span data-stu-id="3559f-112">Customize migration code</span></span>](/ef/core/managing-schemas/migrations/#customize-migration-code)
> * [<span data-ttu-id="3559f-113">資料植入</span><span class="sxs-lookup"><span data-stu-id="3559f-113">Data seeding</span></span>](/ef/core/modeling/data-seeding)