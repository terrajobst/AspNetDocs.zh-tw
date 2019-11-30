---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
title: 非結構化 Blob 儲存體（使用 Azure 建立真實世界的雲端應用程式） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會說明13個模式和實務，
ms.author: riande
ms.date: 03/30/2015
ms.assetid: 9f05ccb1-2004-4661-ad8b-c370e6c09c8e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
msc.type: authoredcontent
ms.openlocfilehash: 2afd4b5cf640eb97080de7e5280409f5e5347731
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74583629"
---
# <a name="unstructured-blob-storage-building-real-world-cloud-apps-with-azure"></a>非結構化 Blob 儲存體（使用 Azure 建立真實世界的雲端應用程式）

由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom 作者: dykstra](https://github.com/tdykstra)

[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。 其中說明13種模式和作法，可協助您成功開發雲端 web 應用程式。 如需電子書的相關資訊，請參閱[第一章](introduction.md)。

在上一章中，我們探討了資料分割配置，並說明如何修正 It 應用程式如何將影像儲存在 Azure 儲存體 Blob 服務中，以及 Azure SQL Database 中的其他工作資料。 在本章中，我們將更深入探討 Blob 服務，並示範如何在修正 It 專案程式碼中執行。

## <a name="what-is-blob-storage"></a>什麼是 Blob 儲存體？

Azure 儲存體 Blob 服務會提供在雲端儲存檔案的方式。 與本機網路檔案系統相比，Blob 服務有許多優點：

- 它具有高擴充性。 單一儲存體帳戶可以儲存[數百 tb](https://msdn.microsoft.com/library/windowsazure/dn249410.aspx)，而且您可以有多個儲存體帳戶。 其中一些最大的 Azure 客戶會儲存數十萬 pb。 Microsoft SkyDrive 會使用 blob 儲存體。
- 它是持久的。 您儲存在 Blob 服務中的每個檔案都會自動備份。
- 它提供高可用性。 [儲存體的 SLA](https://go.microsoft.com/fwlink/p/?linkid=159705&amp;clcid=0x409)承諾99.9% 或99.99% 的執行時間，視您選擇的異地冗余選項而定。
- 它是 Azure 的平臺即服務（PaaS）功能，這表示您只需要儲存和抓取檔案，只支付您所使用的實際儲存體數量，而 Azure 會自動設定和管理所需的所有 Vm 和磁片磁碟機。維護.
- 您可以使用 REST API 或使用程式設計語言 API 來存取 Blob 服務。 Sdk 適用于 .NET、JAVA、Ruby 及其他專案。
- 當您將檔案儲存在 Blob 服務中時，您可以輕鬆地透過網際網路公開提供。
- 您可以保護 Blob 服務中的檔案，使其只能由授權的使用者存取，或者您可以提供暫時的存取權杖，讓使用者只能在有限的時間內使用。

每當您建立適用于 Azure 的應用程式，而且想要在內部部署環境中儲存大量資料時（例如影像、影片、Pdf、試算表等等），請考慮使用 Blob 服務。

## <a name="creating-a-storage-account"></a>建立儲存體帳戶

若要開始使用 Blob 服務您要在 Azure 中建立儲存體帳戶。 在入口網站中，按一下 **新增** -- **資料服務** -- **儲存體** -- **快速建立**，然後輸入 URL 和資料中心位置。 資料中心位置應該與您的 web 應用程式相同。

![建立儲存體帳戶](unstructured-blob-storage/_static/image1.png)

您會挑選要儲存內容的主要區域，如果您選擇 [[異地](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx#_Geo_Redundant_Storage)複寫] 選項，Azure 會在國家/地區另一個區域中的不同資料中心建立所有資料的複本。 例如，如果您選擇「美國西部」資料中心，當您儲存檔案時，它會前往「美國西部」資料中心，但在背景中，Azure 也會將它複製到其他美國資料中心的其中一個。 如果某個國家/地區的某個區域發生嚴重損壞，您的資料仍然安全。

Azure 不會跨地理政治界限複寫資料：如果您的主要位置是美國，則您的檔案只會複寫到美國境內的另一個區域;如果您的主要位置為 [澳大利亞]，則您的檔案只會複寫到澳大利亞的另一個資料中心。

當然，您也可以從腳本執行命令來建立儲存體帳戶，如前文所述。 以下是用來建立儲存體帳戶的 Windows PowerShell 命令：

[!code-powershell[Main](unstructured-blob-storage/samples/sample1.ps1)]

一旦有了儲存體帳戶，您就可以立即開始在 Blob 服務中儲存檔案。

## <a name="using-blob-storage-in-the-fix-it-app"></a>在修正 It 應用程式中使用 Blob 儲存體

[修正 It] 應用程式可讓您上傳相片。

![建立 Fix It 工作](unstructured-blob-storage/_static/image2.png)

當您按一下 [**建立 FixIt**] 時，應用程式會上傳指定的影像檔案，並將它儲存在 Blob 服務中。

### <a name="set-up-the-blob-container"></a>設定 Blob 容器

為了將檔案儲存在 Blob 服務您需要一個*容器*來儲存檔案。 Blob 服務容器會對應至檔系統資料夾。 我們在[自動化所有事項一章](automate-everything.md)中回顧的環境建立腳本會建立儲存體帳戶，但不會建立容器。 因此，`PhotoService` 類別之 `CreateAndConfigure` 方法的目的是要建立容器（如果尚未存在的話）。 這個方法是從*global.asax*中的 `Application_Start` 方法呼叫。

[!code-csharp[Main](unstructured-blob-storage/samples/sample2.cs)]

儲存體帳戶名稱和存取金鑰會儲存在*web.config*檔案的 `appSettings` 集合中，而 `StorageUtils.StorageAccount` 方法中的程式碼會使用這些值來建立連接字串並建立連接：

[!code-csharp[Main](unstructured-blob-storage/samples/sample3.cs)]

然後，`CreateAndConfigureAsync` 方法會建立代表 Blob 服務的物件，以及代表 Blob 服務中名為 "images" 之容器（資料夾）的物件：

[!code-csharp[Main](unstructured-blob-storage/samples/sample4.cs)]

如果名為「映射」的容器尚不存在--第一次針對新的儲存體帳戶執行應用程式時，這會是 true--程式碼會建立容器並設定許可權，使其成為公用。 （根據預設，新的 blob 容器是私用的，只有有權存取您儲存體帳戶的使用者才能存取）。

[!code-csharp[Main](unstructured-blob-storage/samples/sample5.cs)]

### <a name="store-the-uploaded-photo-in-blob-storage"></a>將上傳的相片儲存在 Blob 儲存體中

為了上傳並儲存影像檔案，應用程式會在 `PhotoService` 類別中使用 `IPhotoService` 介面和介面的執行。 *PhotoService.cs*檔案包含 [修正 It] 應用程式中與 Blob 服務通訊的所有程式碼。

當使用者按一下 [**建立 FixIt**] 時，會呼叫下列 MVC 控制器方法。 在此程式碼中，`photoService` 指的是 `PhotoService` 類別的實例，而 `fixittask` 則是指儲存新工作之資料的 `FixItTask` 實體類別實例。

[!code-csharp[Main](unstructured-blob-storage/samples/sample6.cs?highlight=8)]

`PhotoService` 類別中的 `UploadPhotoAsync` 方法會將上傳的檔案儲存在 Blob 服務中，並傳回指向新 Blob 的 URL。

[!code-csharp[Main](unstructured-blob-storage/samples/sample7.cs)]

如同在 `CreateAndConfigure` 方法中，程式碼會連線至儲存體帳戶，並建立代表「映射」 blob 容器的物件，但在此情況下，它會假設容器已存在。

然後藉由串連新的 GUID 值與副檔名，為要上傳的映射建立唯一識別碼：

[!code-csharp[Main](unstructured-blob-storage/samples/sample8.cs)]

然後，此程式碼會使用 blob 容器物件和新的唯一識別碼來建立 blob 物件、在該物件上設定屬性，指出它是哪種檔案，然後使用 blob 物件將檔案儲存在 blob 儲存體中。

[!code-csharp[Main](unstructured-blob-storage/samples/sample9.cs)]

最後，它會取得參考 blob 的 URL。 這個 URL 將會儲存在資料庫中，而且可以用來修正它的網頁，以顯示上傳的影像。

[!code-csharp[Main](unstructured-blob-storage/samples/sample10.cs)]

此 URL 會儲存在資料庫中，做為 FixItTask 資料表的其中一個資料行。

[!code-csharp[Main](unstructured-blob-storage/samples/sample11.cs?highlight=10)]

只有資料庫中的 URL 和 Blob 儲存體中的影像，修正 It 應用程式可讓資料庫保持小型、可擴充且實惠，同時儲存映射的位置不會降低，而且能夠處理 tb 或 pb。 一個儲存體帳戶可以儲存數百 tb 的 Fix It 相片，而您只需為使用的部分付費。 因此，您可以開始針對第一個 gb 付費9分，並為每個額外的 gb 新增更多映射以供刪減。

### <a name="display-the-uploaded-file"></a>顯示上傳的檔案

[修正 It] 應用程式會在顯示工作的詳細資料時，顯示所上傳的影像檔案。

![使用相片修正 It 工作的詳細資料](unstructured-blob-storage/_static/image3.png)

若要顯示影像，所有 MVC view 都必須在傳送至瀏覽器的 HTML 中包含 `PhotoUrl` 值。 Web 服務器和資料庫不會使用迴圈來顯示影像，只會為影像 URL 提供幾個位元組。 在下列 Razor 程式碼中，`Model` 指的是 `FixItTask` 實體類別的實例。

[!code-cshtml[Main](unstructured-blob-storage/samples/sample12.cshtml?highlight=11)]

如果您查看顯示的頁面 HTML，您會看到 URL 直接指向 blob 儲存體中的影像，如下所示：

[!code-cshtml[Main](unstructured-blob-storage/samples/sample13.cshtml?highlight=11)]

## <a name="summary"></a>總結

您已瞭解修正 It 應用程式如何將影像儲存在 Blob 服務中，而且只會在 SQL database 中的影像 Url。 使用 Blob 服務會讓 SQL 資料庫保持比原本更小的值，讓您可以相應增加至幾乎不受限制的工作數目，而不需要撰寫大量的程式碼即可完成。

儲存體帳戶中可以有數百 tb 的資料，儲存成本比 SQL Database 儲存體低，每個月大約每 gb 3 美分，再加上小型交易費用。 請記住，您不需要支付最大容量，而只是實際儲存的數量，因此您的應用程式已準備好進行調整，但您不需要支付所有額外的容量。

在[下一章](design-to-survive-failures.md)中，我們將討論讓雲端應用程式能夠正常處理失敗的重要性。

## <a name="resources"></a>資源

如需詳細資訊，請參閱下列資源：

- [AZURE BLOB 儲存體簡介](https://www.simple-talk.com/cloud/cloud-data/an-introduction-to-windows-azure-blob-storage-/)。 由 Mike 木材撰寫的 Blog。
- [如何在 .net 中使用 Azure Blob 儲存體服務](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)。 MicrosoftAzure.com 網站上的官方檔。 Blob 儲存體簡介，後面接著程式碼範例，示範如何連接到 blob 儲存體、建立容器、上傳和下載 blob 等等。
- [防安全功能：建立可擴充、可復原的雲端服務](https://channel9.msdn.com/Series/FailSafe)。 Ulrich Homann、Marc Mercuri 和 Mark Simm 的九個部分影片系列。 以非常容易存取且有趣的方式呈現高階概念和架構原則，並提供 Microsoft 客戶諮詢小組（CAT）體驗與實際客戶的故事。 如需 Azure 儲存體服務和 blob 的討論，請參閱從35:13 開始的第5集。
- [Microsoft 模式和實務-Azure 指引](https://msdn.microsoft.com/library/dn568099.aspx)。 請參閱 Valet 金鑰模式。

> [!div class="step-by-step"]
> [上一頁](data-partitioning-strategies.md)
> [下一頁](design-to-survive-failures.md)
