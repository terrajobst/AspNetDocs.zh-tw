---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
title: 建立 EF 5 MVC 4 教學課程的章節下載 |Microsoft Docs
author: Rick-Anderson
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio ... 來建立 ASP.NET MVC 4 應用程式。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: d0a89089-eed8-4f61-a478-c5ffa30186f5
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
msc.type: authoredcontent
ms.openlocfilehash: 10237af40e3914b65e5181f17555697e86adea4b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457852"
---
# <a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a><span data-ttu-id="92e26-103">建立 EF 5 MVC 4 教學課程的章節下載</span><span class="sxs-lookup"><span data-stu-id="92e26-103">Building the Chapter Downloads for the EF 5 MVC 4 Tutorials</span></span>

<span data-ttu-id="92e26-104">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="92e26-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[<span data-ttu-id="92e26-105">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="92e26-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="92e26-106">Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。</span><span class="sxs-lookup"><span data-stu-id="92e26-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="92e26-107">如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="92e26-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

## <a name="building-the-chapter-downloads"></a><span data-ttu-id="92e26-108">建置章節下載</span><span class="sxs-lookup"><span data-stu-id="92e26-108">Building the Chapter Downloads</span></span>

1. <span data-ttu-id="92e26-109">下載並解壓縮 project 範例 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="92e26-109">Download and unzip the  project sample zip file.</span></span> <span data-ttu-id="92e26-110">在解壓縮的下載套件中，您會找到其他 zip 檔案，每一章完成一次。</span><span class="sxs-lookup"><span data-stu-id="92e26-110">In the unzipped download package, you will find additional zip files, one for the completion of each chapter.</span></span>
2. <span data-ttu-id="92e26-111">以滑鼠右鍵按一下所需的 zip 檔案，按一下 [**屬性**]，然後按一下 [**解除封鎖**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="92e26-111">Right click on the desired zip file, click **Properties**, and click the **Unblock** button.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. <span data-ttu-id="92e26-112">解壓縮檔案。</span><span class="sxs-lookup"><span data-stu-id="92e26-112">Unzip the file.</span></span>
4. <span data-ttu-id="92e26-113">按兩下 [ *CUx* ] 以啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="92e26-113">Double-click the *CUx.sln* file to launch Visual Studio.</span></span>
5. <span data-ttu-id="92e26-114">從 [**工具**] 功能表中，依序按一下 [ **NuGet 套件管理員**] 和 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="92e26-114">From the **Tools** menu, click **NuGet Package Manager**, then **Package Manager Console**.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. <span data-ttu-id="92e26-115">在 [套件管理員主控台] （PMC）中，按一下 [**還原**]。</span><span class="sxs-lookup"><span data-stu-id="92e26-115">In the Package Manager Console (PMC), click **Restore**.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. <span data-ttu-id="92e26-116">結束 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="92e26-116">Exit Visual Studio.</span></span>
8. <span data-ttu-id="92e26-117">重新開機 Visual Studio，開啟您在上述步驟中關閉的方案檔。</span><span class="sxs-lookup"><span data-stu-id="92e26-117">Restart Visual Studio, opening the solution file you closed in the step above.</span></span>
9. <span data-ttu-id="92e26-118">在 [套件管理員主控台] （PMC）中，輸入 `Update-Database` 命令：</span><span class="sxs-lookup"><span data-stu-id="92e26-118">In the Package Manager Console (PMC), enter the `Update-Database` command:</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > <span data-ttu-id="92e26-119">如果您收到下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="92e26-119">If you get the following error:</span></span>  
    >   
    >  <span data-ttu-id="92e26-120">*「更新-資料庫」一詞無法辨識為 Cmdlet、函式、指令檔或可運作程式的名稱。請檢查名稱的拼寫，或如果已包含路徑，請確認路徑正確，然後再試一次。*</span><span class="sxs-lookup"><span data-stu-id="92e26-120">*The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.*</span></span>  
    > <span data-ttu-id="92e26-121">結束並重新啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="92e26-121">Exit and restart Visual Studio.</span></span>

    <span data-ttu-id="92e26-122">每個遷移將會執行，然後將會執行種子方法。</span><span class="sxs-lookup"><span data-stu-id="92e26-122">Each migration will run, then the seed method will run.</span></span> <span data-ttu-id="92e26-123">您現在可以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="92e26-123">You can now run the app.</span></span>

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> <span data-ttu-id="92e26-124">[[上一步]](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="92e26-124">[Previous](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span></span>
