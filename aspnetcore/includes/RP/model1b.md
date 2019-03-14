---
ms.openlocfilehash: 025a244812a50709bfd48de9f47a234a547c53e2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047415"
---
<span data-ttu-id="3472a-101"><!-- THIS INCLUDE USED BY MVC AND RP --> 將下列屬性新增至 `Movie` 類別：</span><span class="sxs-lookup"><span data-stu-id="3472a-101"><!-- THIS INCLUDE USED BY MVC AND RP --> Add the following properties to the `Movie` class:</span></span>

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Models/Movie.cs?name=snippet1)]

<span data-ttu-id="3472a-102">`Movie` 類別包含：</span><span class="sxs-lookup"><span data-stu-id="3472a-102">The `Movie` class contains:</span></span>

* <span data-ttu-id="3472a-103">`ID` 欄位是資料庫對於主索引鍵的必要欄位。</span><span class="sxs-lookup"><span data-stu-id="3472a-103">The `ID` field is required by the database for the primary key.</span></span>
* <span data-ttu-id="3472a-104">`[DataType(DataType.Date)]`：[DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) 屬性會指定資料的類型 (日期)。</span><span class="sxs-lookup"><span data-stu-id="3472a-104">`[DataType(DataType.Date)]`:  The [DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) attribute specifies the type of the data (Date).</span></span> <span data-ttu-id="3472a-105">使用此屬性：</span><span class="sxs-lookup"><span data-stu-id="3472a-105">With this attribute:</span></span>

  * <span data-ttu-id="3472a-106">使用者不需要在日期欄位中輸入時間資訊。</span><span class="sxs-lookup"><span data-stu-id="3472a-106">The user is not required to enter time information in the date field.</span></span>
  * <span data-ttu-id="3472a-107">只會顯示日期，不會顯示時間資訊。</span><span class="sxs-lookup"><span data-stu-id="3472a-107">Only the date is displayed, not time information.</span></span>

<span data-ttu-id="3472a-108">稍後的教學課程會涵蓋 [DataAnnotations](/dotnet/api/system.componentmodel.dataannotations)。</span><span class="sxs-lookup"><span data-stu-id="3472a-108">[DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) are covered in a later tutorial.</span></span>