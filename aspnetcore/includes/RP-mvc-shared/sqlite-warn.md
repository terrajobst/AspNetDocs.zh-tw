---
ms.openlocfilehash: 2481b10abae9aefce2d5173d8071e4c2236db928
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048215"
---

> [!NOTE]
> EF Core SQLite 提供者不支援許多結構描述變更作業。 例如，其支援新增資料行，但不支援移除資料行。 如果要移除資料行中，建立移轉`ef migrations add`命令執行成功但`ef database update`命令就會失敗。 其中某些限制可以克服手動撰寫資料表重建的移轉程式碼。 重建資料表牽涉到：

>* 重新命名現有的資料表。
>* 建立新的資料表。
>* 舊的資料表資料複製到新的資料表。
>* 卸除舊的資料表。

如需詳細資訊，請參閱下列資源：
> * [SQLite EF Core 資料庫提供者限制](/ef/core/providers/sqlite/limitations)
> * [自訂移轉程式碼](/ef/core/managing-schemas/migrations/#customize-migration-code)
> * [資料植入](/ef/core/modeling/data-seeding)