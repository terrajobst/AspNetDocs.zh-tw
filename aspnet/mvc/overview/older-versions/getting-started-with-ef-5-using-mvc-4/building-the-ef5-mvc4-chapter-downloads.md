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
ms.openlocfilehash: 0e720b3e4c5d3b8f779afe3a6e2b47baa86eec4c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74592713"
---
# <a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a>建立 EF 5 MVC 4 教學課程的章節下載

依[Rick Anderson]((https://twitter.com/RickAndMSFT))

[下載已完成的專案](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。 如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。

## <a name="building-the-chapter-downloads"></a>建置章節下載

1. 下載並解壓縮 project 範例 zip 檔案。 在解壓縮的下載套件中，您會找到其他 zip 檔案，每一章完成一次。
2. 以滑鼠右鍵按一下所需的 zip 檔案，按一下 [**屬性**]，然後按一下 [**解除封鎖**] 按鈕。  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. 解壓縮檔案。
4. 按兩下 [ *CUx* ] 以啟動 Visual Studio。
5. 從 [**工具**] 功能表中，依序按一下 [ **NuGet 套件管理員**] 和 [**套件管理員主控台**]。  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. 在 [套件管理員主控台] （PMC）中，按一下 [**還原**]。  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. 結束 Visual Studio。
8. 重新開機 Visual Studio，開啟您在上述步驟中關閉的方案檔。
9. 在 [套件管理員主控台] （PMC）中，輸入 `Update-Database` 命令：  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > 如果您收到下列錯誤：  
    >   
    >  *「更新-資料庫」一詞無法辨識為 Cmdlet、函式、指令檔或可運作程式的名稱。請檢查名稱的拼寫，或如果已包含路徑，請確認路徑正確，然後再試一次。*  
    > 結束並重新啟動 Visual Studio。

    每個遷移將會執行，然後將會執行種子方法。 您現在可以執行應用程式。

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> [上一篇](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
