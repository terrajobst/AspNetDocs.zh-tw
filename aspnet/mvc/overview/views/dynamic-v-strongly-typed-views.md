---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: 動態與 強型別視圖 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 3e81c6381b1e280e3b74cb7eb6ea6e6c3224e655
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455641"
---
# <a name="dynamic-v-strongly-typed-views"></a>動態與 強型別檢視

依[Rick Anderson](https://twitter.com/RickAndMSFT)

有三種方式可將控制器的資訊傳遞至 ASP.NET MVC 3 中的 view：

1. 做為強型別模型物件。
2. 當做動態類型（使用 @model 動態）
3. 使用 ViewBag

我撰寫了一個簡單的 MVC 3 熱門 Blog 應用程式來比較和對比動態和強型別的觀點。 控制器一開始會有一份簡單的 blog 清單：

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

在 IndexNotStonglyTyped （）方法中按一下滑鼠右鍵，並新增 Razor view。

[![8475. NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)

請確定未核取 [**建立強型別的視圖**] 方塊。 產生的視圖不會包含太多：

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

由於我們使用的是動態的，而不是強型別視圖，因此 intellisense 並不會協助我們。 完成的程式碼如下所示：

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

[![6646。 NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)

現在我們要加入強型別視圖。 將下列程式碼新增至控制器：

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]

請注意，它完全是相同的傳回視圖（topBlogs）;以非強型別視圖的形式呼叫。 以滑鼠右鍵按一下*StonglyTypedIndex （）* 內部，然後選取 [**新增視圖**]。 這次請選取 [ **Blog**模型] 類別，然後選取 [**清單**] 做為 Scaffold 範本。

[![5658. StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)

在新的 view 範本內，我們取得 intellisense 支援。

[![7002。 IntelliSense [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)

您可以在[這裡](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip)下載 c # 專案。
