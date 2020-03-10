---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: 第1部分：總覽和建立專案 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: a76a18f2bd95969358452085ef342fdca8a386e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556074"
---
# <a name="part-1-overview-and-creating-the-project"></a>第1部分：總覽和建立專案

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

Entity Framework 是物件/關聯式對應架構。 它會將程式碼中的網域物件對應至關係資料庫中的實體。 在大部分的情況下，您不需要擔心資料庫層，因為 Entity Framework 會為您處理。 您的程式碼會操控物件，而變更會保存在資料庫中。

## <a name="about-the-tutorial"></a>關於教學課程

在本教學課程中，您將建立簡單的存放區應用程式。 應用程式有兩個主要部分。 一般使用者可以查看產品並建立訂單：

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

系統管理員可以建立、刪除或編輯產品：

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a>您要學習的技術

以下是您要學習的內容：

- 如何搭配 ASP.NET Web API 使用 Entity Framework。
- 如何使用挖的 .js 建立動態用戶端 UI。
- 如何使用 Web API 的表單驗證來驗證使用者。

雖然本教學課程是獨立的，但您可能會想要先閱讀下列教學課程：

- [您的第一個 ASP.NET Web API](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [建立支援 CRUD 作業的 Web API](../creating-a-web-api-that-supports-crud-operations.md)

[ASP.NET MVC](../../../../mvc/index.md)的某些知識也很有説明。

## <a name="overview"></a>概觀

概括而言，以下是應用程式的架構：

- ASP.NET MVC 會產生用戶端的 HTML 頁面。
- ASP.NET Web API 會對資料（產品和訂單）公開 CRUD 作業。
- Entity Framework 會將C# Web API 所使用的模型轉譯成資料庫實體。

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

下圖顯示網域物件在應用程式的各個層級中的呈現方式：資料庫層、物件模型，最後是電傳格式，這是用來透過 HTTP 將資料傳輸至用戶端。

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a>建立 Visual Studio 專案

您可以使用 Visual Web Developer Express 或完整版的 Visual Studio 來建立教學課程專案。

在 [**開始**] 頁面上，按一下 [**新增專案**]。

在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開 **C#視覺效果**節點。 在 **[ C#視覺效果**] 底下，選取 [ **Web**]。 在專案範本清單中，選取 [ **ASP.NET MVC 4 Web 應用程式**]。 將專案命名為 "ProductStore"，然後按一下 **[確定]** 。

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [**網際網路應用程式**]，然後按一下 **[確定]** 。

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

「網際網路應用程式」範本會建立支援表單驗證的 ASP.NET MVC 應用程式。 如果您現在執行應用程式，它已經有一些功能：

- 新使用者可以按一下右上角的 [註冊] 連結進行註冊。
- 已註冊的使用者可以按一下 [登入] 連結來進行登入。

成員資格資訊會保存在自動建立的資料庫中。 如需 ASP.NET MVC 中表單驗證的詳細資訊，請參閱[逐步解說：在 ASP.NET mvc 中使用表單驗](https://msdn.microsoft.com/library/ff398049(VS.98).aspx)證。

## <a name="update-the-css-file"></a>更新 CSS 檔案

此步驟是表面的，但它會使頁面呈現起來像先前的螢幕擷取畫面。

在方案總管中，展開 [內容] 資料夾，然後開啟名為 [網站 .css] 的檔案。 新增下列 CSS 樣式：

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [下一個](using-web-api-with-entity-framework-part-2.md)
