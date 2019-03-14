---
ms.openlocfilehash: f323482d6f8bfaebf7bf6673d5fb91608430760a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044075"
---
## <a name="add-initial-migration-and-update-the-database"></a>新增初始移轉並更新資料庫

* 開啟命令提示字元並巡覽至專案目錄。 (目錄包含*Startup.cs*檔案)。

* 在命令提示字元中執行下列命令：

  ```console
  dotnet restore
  dotnet ef migrations add Initial
  dotnet ef database update
  ```
  
  [.NET core](/dotnet/core/tools/index)是.NET 的跨平台實作。 以下是這些命令所執行的動作：

  * [dotnet 還原](/dotnet/core/tools/dotnet-restore):下載 NuGet 套件中指定 *.csproj*檔案。
  * `dotnet ef migrations add Initial` 執行 Entity Framework 的.NET Core CLI 移轉命令，並建立初始移轉。 您指派給移轉名稱參數之後 [新增]。 這裡您命名移轉 「 初始 」 因為它是初始資料庫移轉。 此作業會建立*Data/Migrations/\<日期時間 > _Initial.cs*檔案，其中包含要新增的移轉命令*電影*到資料庫的資料表。
  * `dotnet ef database update`  使用我們剛才建立的移轉更新資料庫。

在下一個教學課程中，您將了解的資料庫和連接字串。 您將了解中的資料模型變更[將欄位加入](xref:tutorials/first-mvc-app/new-field)教學課程。
