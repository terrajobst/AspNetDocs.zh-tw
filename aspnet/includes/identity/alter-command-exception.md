---
ms.openlocfilehash: b90e7963c5d9e5ef09fb519b72672c63bdffabee
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57188715"
---
> <span data-ttu-id="e0709-101">如果應用程式會使用 SQLite 作為其身分識別資料存放區，不支援某些命令。</span><span class="sxs-lookup"><span data-stu-id="e0709-101">Some commands aren't supported if the app uses SQLite as its Identity data store.</span></span> <span data-ttu-id="e0709-102">由於限制資料庫引擎，`Alter`命令會擲回下列例外狀況：</span><span class="sxs-lookup"><span data-stu-id="e0709-102">Due to limitations in the database engine, `Alter` commands throw the following exception:</span></span>
>
> <span data-ttu-id="e0709-103">「 System.NotSupportedException:SQLite 不支援此移轉作業。 」</span><span class="sxs-lookup"><span data-stu-id="e0709-103">"System.NotSupportedException: SQLite does not support this migration operation."</span></span> 
>
> <span data-ttu-id="e0709-104">因應之道，請變更資料表在資料庫上執行 Code First 移轉。</span><span class="sxs-lookup"><span data-stu-id="e0709-104">As a work around, run Code First migrations on the database to change the tables.</span></span>
