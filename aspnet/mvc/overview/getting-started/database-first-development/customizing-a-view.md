---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: 教學課程：使用 ASP.NET MVC 應用程式自訂 EF Database First 的 view
description: 本教學課程著重于變更自動產生的視圖，以增強簡報。
author: Rick-Anderson
ms.author: riande
ms.date: 01/24/2019
ms.topic: tutorial
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: 89b8a0eb84b6e287c45bc141c68a2c76e63b0e41
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583591"
---
# <a name="tutorial-customize-view-for-ef-database-first-with-aspnet-mvc-app"></a>教學課程：使用 ASP.NET MVC 應用程式自訂 EF Database First 的 view

使用 MVC、Entity Framework 和 ASP.NET 的樣板，您可以建立 web 應用程式，以提供介面給現有的資料庫。 本教學課程系列會示範如何自動產生程式碼，讓使用者可以顯示、編輯、建立和刪除位於資料庫資料表中的資料。 產生的程式碼會對應至資料庫資料表中的資料行。

本教學課程著重于變更自動產生的視圖，以增強簡報。

在本教學課程中，您已：

> [!div class="checklist"]
> * 將課程新增至學生詳細資料頁面
> * 確認課程已新增至頁面

## <a name="prerequisites"></a>Prerequisites

* [變更資料庫](changing-the-database.md)

## <a name="add-courses-to-student-detail"></a>新增課程到學生的詳細資料

產生的程式碼會為您的應用程式提供良好的起點，但不一定要提供應用程式中所需的所有功能。 您可以自訂程式碼，以符合應用程式的特定需求。 目前，您的應用程式不會顯示所選學生的已註冊課程。 在本節中，您會將每個學生註冊的課程新增至學生的**詳細資料**視圖。

 > **學生** > *詳細資料中*開啟**Views** 。 cshtml。 在最後一個 &lt;/dl&gt; 標記，但在關閉 &lt;/div&gt; 標記之前，新增下列程式碼。

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

這段程式碼會建立一個資料表，針對所選學生在註冊資料表中的每筆記錄，顯示一個資料列。 **顯示**方法會針對表示運算式的物件（modelItem）呈現 HTML。 您可以使用顯示方法（而不只是在程式碼中內嵌屬性值），以確定該值的格式是否正確，取決於其型別和該型別的範本。 在此範例中，每個運算式會從迴圈中的目前記錄傳回單一屬性，而這些值是轉譯成文字的基本類型。

## <a name="confirm-courses-are-added"></a>確認課程已新增

執行方案。 按一下 [**學生清單**]，然後選取其中一個學生的 [**詳細資料**]。 您會看到已註冊的課程已包含在此視圖中。

![註冊的學生](customizing-a-view/_static/image1.png)

## <a name="next-steps"></a>後續步驟
在本教學課程中，您已：

> [!div class="checklist"]
> * 將課程新增至學生詳細資料頁面
> * 確認課程已新增至頁面

請前進到下一個教學課程，以瞭解如何新增資料批註來指定驗證需求和顯示格式。
> [!div class="nextstepaction"]
> [增強資料驗證](enhancing-data-validation.md)
