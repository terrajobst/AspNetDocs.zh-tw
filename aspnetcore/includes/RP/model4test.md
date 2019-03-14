---
ms.openlocfilehash: 22c540058e0b3b9ae612f1b2612cecc08627ea2b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57063985"
---
<a name="test"></a>
### <a name="test-the-app"></a><span data-ttu-id="77d1a-101">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="77d1a-101">Test the app</span></span>

* <span data-ttu-id="77d1a-102">執行應用程式，並將 `/Movies` 附加至瀏覽器中的 URL (`http://localhost:port/movies`)。</span><span class="sxs-lookup"><span data-stu-id="77d1a-102">Run the app and append `/Movies` to the URL in the browser (`http://localhost:port/movies`).</span></span>
* <span data-ttu-id="77d1a-103">測試 **Create** 連結。</span><span class="sxs-lookup"><span data-stu-id="77d1a-103">Test the **Create** link.</span></span>

  ![建立頁面](../../tutorials/razor-pages/model/_static/conan.png)

<a name="scaffold"></a>

* <span data-ttu-id="77d1a-105">測試 **Edit**、**Details** 和 **Delete** 連結。</span><span class="sxs-lookup"><span data-stu-id="77d1a-105">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="77d1a-106">如果您收到下列錯誤，請確認您已執行移轉並更新資料庫：</span><span class="sxs-lookup"><span data-stu-id="77d1a-106">If you get the following error, verify you have run migrations and updated the database:</span></span>

```
An unhandled exception occurred while processing the request.
SqliteException: SQLite Error 1: 'no such table: Movie'.
Microsoft.Data.Sqlite.SqliteException.ThrowExceptionForRC(int rc, sqlite3 db)
```
