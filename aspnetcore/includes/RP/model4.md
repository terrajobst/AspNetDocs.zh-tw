---
ms.openlocfilehash: 5ed24cd8a7e880a496d0c0295f7c1fb07f0e1032
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57035985"
---
下表詳細列出 ASP.NET Core 程式碼產生器參數：

| 參數               | 描述|
| ----------------- | ------------ |
| -m  | 模型的名稱。 |
| -dc  | 要使用的 `DbContext` 類別。 |
| -udl | 使用預設的配置。 |
| -outDir | 要建立檢視的相對輸出資料夾路徑。 |
| --referenceScriptLibraries | 將 `_ValidationScriptsPartial` 新增至 Edit 和 Create 頁面 |

使用 `h` 參數取得 `aspnet-codegenerator razorpage` 命令的說明：

```console
dotnet aspnet-codegenerator razorpage -h
```
