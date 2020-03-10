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
ms.openlocfilehash: f48b2be755b84dff9b2672bd348c73107602c6dd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617310"
---
# <a name="unstructured-blob-storage-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="56c13-104">非結構化 Blob 儲存體（使用 Azure 建立真實世界的雲端應用程式）</span><span class="sxs-lookup"><span data-stu-id="56c13-104">Unstructured Blob Storage (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="56c13-105">由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="56c13-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="56c13-106">[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="56c13-106">[Download Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="56c13-107">**使用 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。</span><span class="sxs-lookup"><span data-stu-id="56c13-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="56c13-108">其中說明13種模式和作法，可協助您成功開發雲端 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="56c13-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="56c13-109">如需電子書的相關資訊，請參閱[第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="56c13-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="56c13-110">在上一章中，我們探討了資料分割配置，並說明如何修正 It 應用程式如何將影像儲存在 Azure 儲存體 Blob 服務中，以及 Azure SQL Database 中的其他工作資料。</span><span class="sxs-lookup"><span data-stu-id="56c13-110">In the previous chapter we looked at partitioning schemes and explained how the Fix It app stores images in the Azure Storage Blob service, and other task data in Azure SQL Database.</span></span> <span data-ttu-id="56c13-111">在本章中，我們將更深入探討 Blob 服務，並示範如何在修正 It 專案程式碼中執行。</span><span class="sxs-lookup"><span data-stu-id="56c13-111">In this chapter we go deeper into the Blob service and show how it's implemented in Fix It project code.</span></span>

## <a name="what-is-blob-storage"></a><span data-ttu-id="56c13-112">什麼是 Blob 儲存體？</span><span class="sxs-lookup"><span data-stu-id="56c13-112">What is Blob storage?</span></span>

<span data-ttu-id="56c13-113">Azure 儲存體 Blob 服務會提供在雲端儲存檔案的方式。</span><span class="sxs-lookup"><span data-stu-id="56c13-113">The Azure Storage Blob service provides a way to store files in the cloud.</span></span> <span data-ttu-id="56c13-114">與本機網路檔案系統相比，Blob 服務有許多優點：</span><span class="sxs-lookup"><span data-stu-id="56c13-114">The Blob service has a number of advantages over storing files in a local network file system:</span></span>

- <span data-ttu-id="56c13-115">它具有高擴充性。</span><span class="sxs-lookup"><span data-stu-id="56c13-115">It's highly scalable.</span></span> <span data-ttu-id="56c13-116">單一儲存體帳戶可以儲存[數百 tb](https://msdn.microsoft.com/library/windowsazure/dn249410.aspx)，而且您可以有多個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="56c13-116">A single Storage account can store [hundreds of terabytes](https://msdn.microsoft.com/library/windowsazure/dn249410.aspx), and you can have multiple Storage accounts.</span></span> <span data-ttu-id="56c13-117">其中一些最大的 Azure 客戶會儲存數十萬 pb。</span><span class="sxs-lookup"><span data-stu-id="56c13-117">Some of the biggest Azure customers store hundreds of petabytes.</span></span> <span data-ttu-id="56c13-118">Microsoft SkyDrive 會使用 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="56c13-118">Microsoft SkyDrive uses blob storage.</span></span>
- <span data-ttu-id="56c13-119">它是持久的。</span><span class="sxs-lookup"><span data-stu-id="56c13-119">It's durable.</span></span> <span data-ttu-id="56c13-120">您儲存在 Blob 服務中的每個檔案都會自動備份。</span><span class="sxs-lookup"><span data-stu-id="56c13-120">Every file you store in the Blob service is automatically backed up.</span></span>
- <span data-ttu-id="56c13-121">它提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="56c13-121">It provides high availability.</span></span> <span data-ttu-id="56c13-122">[儲存體的 SLA](https://go.microsoft.com/fwlink/p/?linkid=159705&amp;clcid=0x409)承諾99.9% 或99.99% 的執行時間，視您選擇的異地冗余選項而定。</span><span class="sxs-lookup"><span data-stu-id="56c13-122">The [SLA for Storage](https://go.microsoft.com/fwlink/p/?linkid=159705&amp;clcid=0x409) promises 99.9% or 99.99% uptime, depending on which geo-redundancy option you choose.</span></span>
- <span data-ttu-id="56c13-123">它是 Azure 的平臺即服務（PaaS）功能，這表示您只需要儲存和抓取檔案，只支付您所使用的實際儲存體數量，而 Azure 會自動設定和管理所需的所有 Vm 和磁片磁碟機。維護.</span><span class="sxs-lookup"><span data-stu-id="56c13-123">It's a platform-as-a-service (PaaS) feature of Azure, which means you just store and retrieve files, paying only for the actual amount of storage you use, and Azure automatically takes care of setting up and managing all of the VMs and disk drives required for the service.</span></span>
- <span data-ttu-id="56c13-124">您可以使用 REST API 或使用程式設計語言 API 來存取 Blob 服務。</span><span class="sxs-lookup"><span data-stu-id="56c13-124">You can access the Blob service by using a REST API or by using a programming language API.</span></span> <span data-ttu-id="56c13-125">Sdk 適用于 .NET、JAVA、Ruby 及其他專案。</span><span class="sxs-lookup"><span data-stu-id="56c13-125">SDKs are available for .NET, Java, Ruby, and others.</span></span>
- <span data-ttu-id="56c13-126">當您將檔案儲存在 Blob 服務中時，您可以輕鬆地透過網際網路公開提供。</span><span class="sxs-lookup"><span data-stu-id="56c13-126">When you store a file in the Blob service, you can easily make it publicly available over the Internet.</span></span>
- <span data-ttu-id="56c13-127">您可以保護 Blob 服務中的檔案，使其只能由授權的使用者存取，或者您可以提供暫時的存取權杖，讓使用者只能在有限的時間內使用。</span><span class="sxs-lookup"><span data-stu-id="56c13-127">You can secure files in the Blob service so they can accessed only by authorized users, or you can provide temporary access tokens that makes them available to someone only for a limited period of time.</span></span>

<span data-ttu-id="56c13-128">每當您建立適用于 Azure 的應用程式，而且想要在內部部署環境中儲存大量資料時（例如影像、影片、Pdf、試算表等等），請考慮使用 Blob 服務。</span><span class="sxs-lookup"><span data-stu-id="56c13-128">Anytime you're building an app for Azure and you want to store a lot of data that in an on-premises environment would go in files -- such as images, videos, PDFs, spreadsheets, etc. -- consider the Blob service.</span></span>

## <a name="creating-a-storage-account"></a><span data-ttu-id="56c13-129">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="56c13-129">Creating a Storage account</span></span>

<span data-ttu-id="56c13-130">若要開始使用 Blob 服務您要在 Azure 中建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="56c13-130">To get started with the Blob service you create a Storage account in Azure.</span></span> <span data-ttu-id="56c13-131">在入口網站中，按一下 **新增** -- **資料服務** -- **儲存體** -- **快速建立**，然後輸入 URL 和資料中心位置。</span><span class="sxs-lookup"><span data-stu-id="56c13-131">In the portal, click **New** -- **Data Services** -- **Storage** -- **Quick Create**, and then enter a URL and a data center location.</span></span> <span data-ttu-id="56c13-132">資料中心位置應該與您的 web 應用程式相同。</span><span class="sxs-lookup"><span data-stu-id="56c13-132">The data center location should be the same as your web app.</span></span>

![建立儲存體帳戶](unstructured-blob-storage/_static/image1.png)

<span data-ttu-id="56c13-134">您會挑選要儲存內容的主要區域，如果您選擇 [[異地](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx#_Geo_Redundant_Storage)複寫] 選項，Azure 會在國家/地區另一個區域中的不同資料中心建立所有資料的複本。</span><span class="sxs-lookup"><span data-stu-id="56c13-134">You pick the primary region where you want to store the content, and if you choose the [geo-replication](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx#_Geo_Redundant_Storage) option, Azure creates replicas of all your data in a different data center in another region of the country.</span></span> <span data-ttu-id="56c13-135">例如，如果您選擇「美國西部」資料中心，當您儲存檔案時，它會前往「美國西部」資料中心，但在背景中，Azure 也會將它複製到其他美國資料中心的其中一個。</span><span class="sxs-lookup"><span data-stu-id="56c13-135">For example, if you choose the Western US data center, when you store a file it goes to the Western US data center, but in the background Azure also copies it to one of the other US data centers.</span></span> <span data-ttu-id="56c13-136">如果某個國家/地區的某個區域發生嚴重損壞，您的資料仍然安全。</span><span class="sxs-lookup"><span data-stu-id="56c13-136">If a disaster happens in one region of the country, your data is still safe.</span></span>

<span data-ttu-id="56c13-137">Azure 不會跨地理政治界限複寫資料：如果您的主要位置是美國，則您的檔案只會複寫到美國境內的另一個區域;如果您的主要位置為 [澳大利亞]，則您的檔案只會複寫到澳大利亞的另一個資料中心。</span><span class="sxs-lookup"><span data-stu-id="56c13-137">Azure won't replicate data across geo-political boundaries: if your primary location is in the U.S., your files are only replicated to another region within the U.S.; if your primary location is Australia, your files are only replicated to another data center in Australia.</span></span>

<span data-ttu-id="56c13-138">當然，您也可以從腳本執行命令來建立儲存體帳戶，如前文所述。</span><span class="sxs-lookup"><span data-stu-id="56c13-138">Of course, you can also create a Storage account by executing commands from a script, as we saw earlier.</span></span> <span data-ttu-id="56c13-139">以下是用來建立儲存體帳戶的 Windows PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="56c13-139">Here's a Windows PowerShell command to create a Storage account:</span></span>

[!code-powershell[Main](unstructured-blob-storage/samples/sample1.ps1)]

<span data-ttu-id="56c13-140">一旦有了儲存體帳戶，您就可以立即開始在 Blob 服務中儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="56c13-140">Once you have a Storage account, you can immediately start storing files in the Blob service.</span></span>

## <a name="using-blob-storage-in-the-fix-it-app"></a><span data-ttu-id="56c13-141">在修正 It 應用程式中使用 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="56c13-141">Using Blob storage in the Fix It app</span></span>

<span data-ttu-id="56c13-142">[修正 It] 應用程式可讓您上傳相片。</span><span class="sxs-lookup"><span data-stu-id="56c13-142">The Fix It app enables you to upload photos.</span></span>

![建立 Fix It 工作](unstructured-blob-storage/_static/image2.png)

<span data-ttu-id="56c13-144">當您按一下 [**建立 FixIt**] 時，應用程式會上傳指定的影像檔案，並將它儲存在 Blob 服務中。</span><span class="sxs-lookup"><span data-stu-id="56c13-144">When you click **Create the FixIt**, the application uploads the specified image file and stores it in the Blob service.</span></span>

### <a name="set-up-the-blob-container"></a><span data-ttu-id="56c13-145">設定 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="56c13-145">Set up the Blob container</span></span>

<span data-ttu-id="56c13-146">為了將檔案儲存在 Blob 服務您需要一個*容器*來儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="56c13-146">In order to store a file in the Blob service you need a *container* to store it in.</span></span> <span data-ttu-id="56c13-147">Blob 服務容器會對應至檔系統資料夾。</span><span class="sxs-lookup"><span data-stu-id="56c13-147">A Blob service container corresponds to a file system folder.</span></span> <span data-ttu-id="56c13-148">我們在[自動化所有事項一章](automate-everything.md)中回顧的環境建立腳本會建立儲存體帳戶，但不會建立容器。</span><span class="sxs-lookup"><span data-stu-id="56c13-148">The environment creation scripts that we reviewed in the [Automate Everything chapter](automate-everything.md) create the Storage account, but they don't create a container.</span></span> <span data-ttu-id="56c13-149">因此，`PhotoService` 類別之 `CreateAndConfigure` 方法的目的是要建立容器（如果尚未存在的話）。</span><span class="sxs-lookup"><span data-stu-id="56c13-149">So the purpose of the `CreateAndConfigure` method of the `PhotoService` class is to create a container if it doesn't already exist.</span></span> <span data-ttu-id="56c13-150">這個方法是從*global.asax*中的 `Application_Start` 方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="56c13-150">This method is called from the `Application_Start` method in *Global.asax*.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample2.cs)]

<span data-ttu-id="56c13-151">儲存體帳戶名稱和存取金鑰會儲存在*web.config*檔案的 `appSettings` 集合中，而 `StorageUtils.StorageAccount` 方法中的程式碼會使用這些值來建立連接字串並建立連接：</span><span class="sxs-lookup"><span data-stu-id="56c13-151">The storage account name and access key are stored in the `appSettings` collection of the *Web.config* file, and code in the `StorageUtils.StorageAccount` method uses those values to build a connection string and establish a connection:</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample3.cs)]

<span data-ttu-id="56c13-152">然後，`CreateAndConfigureAsync` 方法會建立代表 Blob 服務的物件，以及代表 Blob 服務中名為 "images" 之容器（資料夾）的物件：</span><span class="sxs-lookup"><span data-stu-id="56c13-152">The `CreateAndConfigureAsync` method then creates an object that represents the Blob service, and an object that represents a container (folder) named "images" in the Blob service:</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample4.cs)]

<span data-ttu-id="56c13-153">如果名為「映射」的容器尚不存在--第一次針對新的儲存體帳戶執行應用程式時，這會是 true--程式碼會建立容器並設定許可權，使其成為公用。</span><span class="sxs-lookup"><span data-stu-id="56c13-153">If a container named "images" doesn't exist yet -- which will be true the first time you run the app against a new storage account -- the code creates the container and sets permissions to make it public.</span></span> <span data-ttu-id="56c13-154">（根據預設，新的 blob 容器是私用的，只有有權存取您儲存體帳戶的使用者才能存取）。</span><span class="sxs-lookup"><span data-stu-id="56c13-154">(By default, new blob containers are private and are accessible only to users who have permission to access your storage account.)</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample5.cs)]

### <a name="store-the-uploaded-photo-in-blob-storage"></a><span data-ttu-id="56c13-155">將上傳的相片儲存在 Blob 儲存體中</span><span class="sxs-lookup"><span data-stu-id="56c13-155">Store the uploaded photo in Blob storage</span></span>

<span data-ttu-id="56c13-156">為了上傳並儲存影像檔案，應用程式會在 `PhotoService` 類別中使用 `IPhotoService` 介面和介面的執行。</span><span class="sxs-lookup"><span data-stu-id="56c13-156">To upload and save the image file, the app uses an `IPhotoService` interface and an implementation of the interface in the `PhotoService` class.</span></span> <span data-ttu-id="56c13-157">*PhotoService.cs*檔案包含 [修正 It] 應用程式中與 Blob 服務通訊的所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="56c13-157">The *PhotoService.cs* file contains all of the code in the Fix It app that communicates with the Blob service.</span></span>

<span data-ttu-id="56c13-158">當使用者按一下 [**建立 FixIt**] 時，會呼叫下列 MVC 控制器方法。</span><span class="sxs-lookup"><span data-stu-id="56c13-158">The following MVC controller method is called when the user clicks **Create the FixIt**.</span></span> <span data-ttu-id="56c13-159">在此程式碼中，`photoService` 指的是 `PhotoService` 類別的實例，而 `fixittask` 則是指儲存新工作之資料的 `FixItTask` 實體類別實例。</span><span class="sxs-lookup"><span data-stu-id="56c13-159">In this code, `photoService` refers to an instance of the `PhotoService` class, and `fixittask` refers to an instance of the `FixItTask` entity class that stores data for a new task.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample6.cs?highlight=8)]

<span data-ttu-id="56c13-160">`PhotoService` 類別中的 `UploadPhotoAsync` 方法會將上傳的檔案儲存在 Blob 服務中，並傳回指向新 Blob 的 URL。</span><span class="sxs-lookup"><span data-stu-id="56c13-160">The `UploadPhotoAsync` method in the `PhotoService` class stores the uploaded file in the Blob service and returns a URL that points to the new blob.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample7.cs)]

<span data-ttu-id="56c13-161">如同在 `CreateAndConfigure` 方法中，程式碼會連線至儲存體帳戶，並建立代表「映射」 blob 容器的物件，但在此情況下，它會假設容器已存在。</span><span class="sxs-lookup"><span data-stu-id="56c13-161">As in the `CreateAndConfigure` method, the code connects to the storage account and creates an object that represents the "images" blob container, except here it assumes the container already exists.</span></span>

<span data-ttu-id="56c13-162">然後藉由串連新的 GUID 值與副檔名，為要上傳的映射建立唯一識別碼：</span><span class="sxs-lookup"><span data-stu-id="56c13-162">Then it creates a unique identifier for the image about to be uploaded, by concatenating a new GUID value with the file extension:</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample8.cs)]

<span data-ttu-id="56c13-163">然後，此程式碼會使用 blob 容器物件和新的唯一識別碼來建立 blob 物件、在該物件上設定屬性，指出它是哪種檔案，然後使用 blob 物件將檔案儲存在 blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="56c13-163">The code then uses the blob container object and the new unique identifier to create a blob object, sets an attribute on that object indicating what kind of file it is, and then uses the blob object to store the file in blob storage.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample9.cs)]

<span data-ttu-id="56c13-164">最後，它會取得參考 blob 的 URL。</span><span class="sxs-lookup"><span data-stu-id="56c13-164">Finally, it gets a URL that references the blob.</span></span> <span data-ttu-id="56c13-165">這個 URL 將會儲存在資料庫中，而且可以用來修正它的網頁，以顯示上傳的影像。</span><span class="sxs-lookup"><span data-stu-id="56c13-165">This URL will be stored in the database and can be used in Fix It web pages to display the uploaded image.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample10.cs)]

<span data-ttu-id="56c13-166">此 URL 會儲存在資料庫中，做為 FixItTask 資料表的其中一個資料行。</span><span class="sxs-lookup"><span data-stu-id="56c13-166">This URL is stored in the database as one of the columns of the FixItTask table.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample11.cs?highlight=10)]

<span data-ttu-id="56c13-167">只有資料庫中的 URL 和 Blob 儲存體中的影像，修正 It 應用程式可讓資料庫保持小型、可擴充且實惠，同時儲存映射的位置不會降低，而且能夠處理 tb 或 pb。</span><span class="sxs-lookup"><span data-stu-id="56c13-167">With only the URL in the database, and images in Blob storage, the Fix It app keeps the database small, scalable, and inexpensive, while the images are stored where storage is cheap and capable of handling terabytes or petabytes.</span></span> <span data-ttu-id="56c13-168">一個儲存體帳戶可以儲存數百 tb 的 Fix It 相片，而您只需為使用的部分付費。</span><span class="sxs-lookup"><span data-stu-id="56c13-168">One storage account can store hundreds of terabytes of Fix It photos, and you only pay for what you use.</span></span> <span data-ttu-id="56c13-169">因此，您可以開始針對第一個 gb 付費9分，並為每個額外的 gb 新增更多映射以供刪減。</span><span class="sxs-lookup"><span data-stu-id="56c13-169">So you can start off small paying 9 cents for the first gigabyte, and add more images for pennies per additional gigabyte.</span></span>

### <a name="display-the-uploaded-file"></a><span data-ttu-id="56c13-170">顯示上傳的檔案</span><span class="sxs-lookup"><span data-stu-id="56c13-170">Display the uploaded file</span></span>

<span data-ttu-id="56c13-171">[修正 It] 應用程式會在顯示工作的詳細資料時，顯示所上傳的影像檔案。</span><span class="sxs-lookup"><span data-stu-id="56c13-171">The Fix It application displays the uploaded image file when it displays details for a task.</span></span>

![使用相片修正 It 工作的詳細資料](unstructured-blob-storage/_static/image3.png)

<span data-ttu-id="56c13-173">若要顯示影像，所有 MVC view 都必須在傳送至瀏覽器的 HTML 中包含 `PhotoUrl` 值。</span><span class="sxs-lookup"><span data-stu-id="56c13-173">To display the image, all the MVC view has to do is include the `PhotoUrl` value in the HTML sent to the browser.</span></span> <span data-ttu-id="56c13-174">Web 服務器和資料庫不會使用迴圈來顯示影像，只會為影像 URL 提供幾個位元組。</span><span class="sxs-lookup"><span data-stu-id="56c13-174">The web server and the database are not using cycles to display the image, they are only serving up a few bytes to the image URL.</span></span> <span data-ttu-id="56c13-175">在下列 Razor 程式碼中，`Model` 指的是 `FixItTask` 實體類別的實例。</span><span class="sxs-lookup"><span data-stu-id="56c13-175">In the following Razor code, `Model` refers to an instance of the `FixItTask` entity class.</span></span>

[!code-cshtml[Main](unstructured-blob-storage/samples/sample12.cshtml?highlight=11)]

<span data-ttu-id="56c13-176">如果您查看顯示的頁面 HTML，您會看到 URL 直接指向 blob 儲存體中的影像，如下所示：</span><span class="sxs-lookup"><span data-stu-id="56c13-176">If you look at the HTML of the page that displays, you see the URL pointing directly to the image in blob storage, something like this:</span></span>

[!code-cshtml[Main](unstructured-blob-storage/samples/sample13.cshtml?highlight=11)]

## <a name="summary"></a><span data-ttu-id="56c13-177">總結</span><span class="sxs-lookup"><span data-stu-id="56c13-177">Summary</span></span>

<span data-ttu-id="56c13-178">您已瞭解修正 It 應用程式如何將影像儲存在 Blob 服務中，而且只會在 SQL database 中的影像 Url。</span><span class="sxs-lookup"><span data-stu-id="56c13-178">You've seen how the Fix It app stores images in the Blob service and only image URLs in the SQL database.</span></span> <span data-ttu-id="56c13-179">使用 Blob 服務會讓 SQL 資料庫保持比原本更小的值，讓您可以相應增加至幾乎不受限制的工作數目，而不需要撰寫大量的程式碼即可完成。</span><span class="sxs-lookup"><span data-stu-id="56c13-179">Using the Blob service keeps the SQL database much smaller than it otherwise would be, makes it possible to scale up to an almost unlimited number of tasks, and can be done without writing a lot of code.</span></span>

<span data-ttu-id="56c13-180">儲存體帳戶中可以有數百 tb 的資料，儲存成本比 SQL Database 儲存體低，每個月大約每 gb 3 美分，再加上小型交易費用。</span><span class="sxs-lookup"><span data-stu-id="56c13-180">You can have hundreds of terabytes in a storage account, and the storage cost is much less expensive than SQL Database storage, starting at about 3 cents per gigabyte per month plus a small transaction charge.</span></span> <span data-ttu-id="56c13-181">請記住，您不需要支付最大容量，而只是實際儲存的數量，因此您的應用程式已準備好進行調整，但您不需要支付所有額外的容量。</span><span class="sxs-lookup"><span data-stu-id="56c13-181">And keep in mind that you're not paying for the maximum capacity but only for the amount you actually store, so your app is ready to scale but you're not paying for all that extra capacity.</span></span>

<span data-ttu-id="56c13-182">在[下一章](design-to-survive-failures.md)中，我們將討論讓雲端應用程式能夠正常處理失敗的重要性。</span><span class="sxs-lookup"><span data-stu-id="56c13-182">In the [next chapter](design-to-survive-failures.md) we'll talk about the importance of making a cloud app capable of gracefully handling failures.</span></span>

## <a name="resources"></a><span data-ttu-id="56c13-183">資源</span><span class="sxs-lookup"><span data-stu-id="56c13-183">Resources</span></span>

<span data-ttu-id="56c13-184">如需詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="56c13-184">For more information see the following resources:</span></span>

- <span data-ttu-id="56c13-185">[AZURE BLOB 儲存體簡介](https://www.simple-talk.com/cloud/cloud-data/an-introduction-to-windows-azure-blob-storage-/)。</span><span class="sxs-lookup"><span data-stu-id="56c13-185">[An Introduction to Azure BLOB Storage](https://www.simple-talk.com/cloud/cloud-data/an-introduction-to-windows-azure-blob-storage-/).</span></span> <span data-ttu-id="56c13-186">由 Mike 木材撰寫的 Blog。</span><span class="sxs-lookup"><span data-stu-id="56c13-186">Blog by Mike Wood.</span></span>
- <span data-ttu-id="56c13-187">[如何在 .net 中使用 Azure Blob 儲存體服務](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)。</span><span class="sxs-lookup"><span data-stu-id="56c13-187">[How to use the Azure Blob Storage Service in .NET](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs).</span></span> <span data-ttu-id="56c13-188">MicrosoftAzure.com 網站上的官方檔。</span><span class="sxs-lookup"><span data-stu-id="56c13-188">Official documentation on the MicrosoftAzure.com site.</span></span> <span data-ttu-id="56c13-189">Blob 儲存體簡介，後面接著程式碼範例，示範如何連接到 blob 儲存體、建立容器、上傳和下載 blob 等等。</span><span class="sxs-lookup"><span data-stu-id="56c13-189">A brief introduction to blob storage followed by code examples showing how to connect to blob storage, create containers, upload and download blobs, etc.</span></span>
- <span data-ttu-id="56c13-190">[防安全功能：建立可擴充、可復原的雲端服務](https://channel9.msdn.com/Series/FailSafe)。</span><span class="sxs-lookup"><span data-stu-id="56c13-190">[FailSafe: Building Scalable, Resilient Cloud Services](https://channel9.msdn.com/Series/FailSafe).</span></span> <span data-ttu-id="56c13-191">Ulrich Homann、Marc Mercuri 和 Mark Simm 的九個部分影片系列。</span><span class="sxs-lookup"><span data-stu-id="56c13-191">Nine-part video series by Ulrich Homann, Marc Mercuri, and Mark Simms.</span></span> <span data-ttu-id="56c13-192">以非常容易存取且有趣的方式呈現高階概念和架構原則，並提供 Microsoft 客戶諮詢小組（CAT）體驗與實際客戶的故事。</span><span class="sxs-lookup"><span data-stu-id="56c13-192">Presents high-level concepts and architectural principles in a very accessible and interesting way, with stories drawn from Microsoft Customer Advisory Team (CAT) experience with actual customers.</span></span> <span data-ttu-id="56c13-193">如需 Azure 儲存體服務和 blob 的討論，請參閱從35:13 開始的第5集。</span><span class="sxs-lookup"><span data-stu-id="56c13-193">For a discussion of Azure Storage service and blobs, see episode 5 starting at 35:13.</span></span>
- <span data-ttu-id="56c13-194">[Microsoft 模式和實務-Azure 指引](https://msdn.microsoft.com/library/dn568099.aspx)。</span><span class="sxs-lookup"><span data-stu-id="56c13-194">[Microsoft Patterns and Practices - Azure Guidance](https://msdn.microsoft.com/library/dn568099.aspx).</span></span> <span data-ttu-id="56c13-195">請參閱 Valet 金鑰模式。</span><span class="sxs-lookup"><span data-stu-id="56c13-195">See Valet Key pattern.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="56c13-196">[上一頁](data-partitioning-strategies.md)
> [下一頁](design-to-survive-failures.md)</span><span class="sxs-lookup"><span data-stu-id="56c13-196">[Previous](data-partitioning-strategies.md)
[Next](design-to-survive-failures.md)</span></span>
