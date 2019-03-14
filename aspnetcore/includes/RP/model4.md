---
ms.openlocfilehash: 5ed24cd8a7e880a496d0c0295f7c1fb07f0e1032
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57035985"
---
<span data-ttu-id="59679-101">下表詳細列出 ASP.NET Core 程式碼產生器參數：</span><span class="sxs-lookup"><span data-stu-id="59679-101">The following table details the ASP.NET Core code generator parameters:</span></span>

| <span data-ttu-id="59679-102">參數</span><span class="sxs-lookup"><span data-stu-id="59679-102">Parameter</span></span>               | <span data-ttu-id="59679-103">描述</span><span class="sxs-lookup"><span data-stu-id="59679-103">Description</span></span>|
| ----------------- | ------------ |
| <span data-ttu-id="59679-104">-m</span><span class="sxs-lookup"><span data-stu-id="59679-104">-m</span></span>  | <span data-ttu-id="59679-105">模型的名稱。</span><span class="sxs-lookup"><span data-stu-id="59679-105">The name of the model.</span></span> |
| <span data-ttu-id="59679-106">-dc</span><span class="sxs-lookup"><span data-stu-id="59679-106">-dc</span></span>  | <span data-ttu-id="59679-107">要使用的 `DbContext` 類別。</span><span class="sxs-lookup"><span data-stu-id="59679-107">The `DbContext` class to use.</span></span> |
| <span data-ttu-id="59679-108">-udl</span><span class="sxs-lookup"><span data-stu-id="59679-108">-udl</span></span> | <span data-ttu-id="59679-109">使用預設的配置。</span><span class="sxs-lookup"><span data-stu-id="59679-109">Use the default layout.</span></span> |
| <span data-ttu-id="59679-110">-outDir</span><span class="sxs-lookup"><span data-stu-id="59679-110">-outDir</span></span> | <span data-ttu-id="59679-111">要建立檢視的相對輸出資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="59679-111">The relative output folder path to create the views.</span></span> |
| <span data-ttu-id="59679-112">--referenceScriptLibraries</span><span class="sxs-lookup"><span data-stu-id="59679-112">--referenceScriptLibraries</span></span> | <span data-ttu-id="59679-113">將 `_ValidationScriptsPartial` 新增至 Edit 和 Create 頁面</span><span class="sxs-lookup"><span data-stu-id="59679-113">Adds `_ValidationScriptsPartial` to Edit and Create pages</span></span> |

<span data-ttu-id="59679-114">使用 `h` 參數取得 `aspnet-codegenerator razorpage` 命令的說明：</span><span class="sxs-lookup"><span data-stu-id="59679-114">Use the `h` switch to get help on the `aspnet-codegenerator razorpage` command:</span></span>

```console
dotnet aspnet-codegenerator razorpage -h
```
