---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: 在 ASP.NET Web API 中傳送 HTML 表單資料：檔案上傳和多部分 MIME ASP.NET 4。x
author: MikeWasson
description: 本教學課程說明如何將檔案上傳至 Web API。 它也會說明如何處理多部分 MIME 資料。
ms.author: riande
ms.date: 06/21/2012
ms.custom: seoapril2019
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: f5aaebb96f631dfb6b0da1fbca96cd93a6a7fe2d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557565"
---
# <a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a>在 ASP.NET Web API 中傳送 HTML 表單資料：檔案上傳和多部分 MIME

由[Mike Wasson](https://github.com/MikeWasson)

## <a name="part-2-file-upload-and-multipart-mime"></a>第2部分：檔案上傳和多部分 MIME

本教學課程說明如何將檔案上傳至 Web API。 它也會說明如何處理多部分 MIME 資料。

> [!NOTE]
> [下載已完成的專案](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d)。

以下是用來上傳檔案的 HTML 表單範例：

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

此表單包含文字輸入控制項和檔案輸入控制項。 當表單包含檔案輸入控制項時， **enctype**屬性應該一律為 &quot;多部分/表單資料&quot;，這會指定將表單當做多部分 MIME 訊息來傳送。

藉由查看範例要求，可以更輕鬆地瞭解多部分 MIME 訊息的格式：

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

此訊息分成兩個*部分*，每個表單控制項各一個。 部分界限是以連字號開頭的行來表示。

> [!NOTE]
> 部分界限包含隨機元件（&quot;41184676334&quot;），以確保界限字串不會不慎出現在訊息部分內。

每個訊息部分都包含一或多個標頭，後面接著元件內容。

- 內容配置標頭包含控制項的名稱。 針對檔案，它也包含檔案名。
- Content-type 標頭會描述元件中的資料。 如果省略此標頭，則預設值為 text/純文字。

在上述範例中，使用者上傳了名為 GrandCanyon 的檔案，內容類型為 image/jpeg;而文字輸入的值是 &quot;夏日假期&quot;。

## <a name="file-upload"></a>檔案上傳

現在讓我們看看從多部分 MIME 訊息讀取檔案的 Web API 控制器。 控制器會以非同步方式讀取檔案。 Web API 支援使用以工作為[基礎的程式設計模型](https://msdn.microsoft.com/library/dd460693.aspx)的非同步動作。 首先，如果您的目標為支援**async**和**await**關鍵字的 .NET Framework 4.5，這裡就是程式碼。

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

請注意，控制器動作不會接受任何參數。 這是因為我們會處理動作內的要求本文，而不會叫用媒體類型格式器。

**IsMultipartContent**方法會檢查要求是否包含多部分 MIME 訊息。 如果沒有，控制器會傳回 HTTP 狀態碼415（不支援的媒體類型）。

**MultipartFormDataStreamProvider**類別是一個協助程式物件，它會為上傳的檔案設定檔案串流。 若要讀取多部分 MIME 訊息，請呼叫**ReadAsMultipartAsync**方法。 這個方法會解壓縮所有訊息部分，並將它們寫入**MultipartFormDataStreamProvider**所提供的資料流程。

當方法完成時，您可以從**FileData**屬性取得檔案的相關資訊，這是**MultipartFileData**物件的集合。

- **MultipartFileData**是伺服器上儲存檔案的本機檔案名。
- **MultipartFileData：標頭**包含元件標頭（*而不*是要求標頭）。 您可以使用這個來存取\_配置和內容類型標頭的內容。

顧名思義， **ReadAsMultipartAsync**是非同步方法。 若要在方法完成後執行工作，請使用[接續](https://msdn.microsoft.com/library/ee372288.aspx)工作（.net 4.0）或**await**關鍵字（.net 4.5）。

以下是先前程式碼的 .NET Framework 4.0 版本：

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a>讀取表單控制項資料

我稍早所示的 HTML 表單具有文字輸入控制項。

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

您可以從**MultipartFormDataStreamProvider**的**FormData**屬性取得控制項的值。

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

**FormData**是一個**NameValueCollection** ，其中包含表單控制項的名稱/值組。 集合可以包含重複的索引鍵。 請考慮下列形式：

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

要求主體可能如下所示：

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

在此情況下， **FormData**集合會包含下列索引鍵/值組：

- 旅程：來回
- 選項：持續
- 選項：日期
- 基座：視窗
