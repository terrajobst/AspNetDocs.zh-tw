---
uid: aspnet/overview/owin-and-katana/owin-startup-class-detection
title: OWIN 啟動類別偵測 |Microsoft Docs
author: Praburaj
description: 本教學課程說明如何設定要載入的 OWIN startup 類別。 如需 OWIN 的詳細資訊，請參閱專案 Katana 的總覽。 本教學課程是 。
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 08257f55-36f4-4e39-9c88-2a5602838c79
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-startup-class-detection
msc.type: authoredcontent
ms.openlocfilehash: e1670c32049ec33dd4d1941a091a429d3929c452
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617044"
---
# <a name="owin-startup-class-detection"></a>OWIN 啟動類別偵測

> 本教學課程說明如何設定要載入的 OWIN startup 類別。 如需 OWIN 的詳細資訊，請參閱[專案 Katana 的總覽](an-overview-of-project-katana.md)。 本教學課程是由 Rick Anderson （ [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ）、Praburaj Thiagarajan 和 Howard Dierking （ [@howard\_Dierking](https://twitter.com/howard_dierking) ）撰寫。
>
> ## <a name="prerequisites"></a>Prerequisites
>
> [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)

## <a name="owin-startup-class-detection"></a>OWIN 啟動類別偵測

 每個 OWIN 應用程式都有一個啟動類別，您可以在其中指定應用程式管線的元件。 有不同的方式可讓您連接啟動類別與執行時間，視您選擇的裝載模型而定（OwinHost、IIS 和 IIS Express）。 本教學課程中所顯示的 startup 類別可以在每個裝載應用程式中使用。 您可以使用下列其中一種方法，將啟動類別與主控執行時間連接：

1. **命名慣例**： Katana 會在符合元件名稱或全域命名空間的命名空間中，尋找名為 `Startup` 的類別。
2. **OwinStartup 屬性**：這是大部分開發人員用來指定啟動類別的方法。 下列屬性會將 startup 類別設定為 `StartupDemo` 命名空間中的 `TestStartup` 類別。

    [!code-csharp[Main](owin-startup-class-detection/samples/sample1.cs)]

   `OwinStartup` 屬性會覆寫命名慣例。 您也可以指定具有此屬性的易記名稱，不過，使用易記名稱時，您也必須使用設定檔中的 `appSetting` 元素。
3. **設定檔中的 appSetting 元素**： `appSetting` 元素會覆寫 `OwinStartup` 屬性和命名慣例。 您可以有多個啟動類別（每個都使用 `OwinStartup` 屬性），並使用類似下列的標記來設定要在設定檔案中載入的啟動類別：

    [!code-xml[Main](owin-startup-class-detection/samples/sample2.xml)]

   您也可以使用下列索引鍵，明確指定啟動類別和元件：

    [!code-xml[Main](owin-startup-class-detection/samples/sample3.xml)]

   設定檔中的下列 XML 會指定 `ProductionConfiguration`的易記啟動類別名稱。

    [!code-xml[Main](owin-startup-class-detection/samples/sample4.xml)]

   上述標記必須與下列 `OwinStartup` 屬性搭配使用，以指定易記名稱並導致 `ProductionStartup2` 類別執行。

    [!code-csharp[Main](owin-startup-class-detection/samples/sample5.cs?highlight=1,16)]
4. 若要停用 OWIN 啟動探索，請在 web.config 檔案中新增具有 `"false"` 值的 `appSetting owin:AutomaticAppStartup`。

    [!code-xml[Main](owin-startup-class-detection/samples/sample6.xml)]

## <a name="create-an-aspnet-web-app-using-owin-startup"></a>使用 OWIN 啟動建立 ASP.NET Web 應用程式

1. 建立空的 Asp.Net web 應用程式，並將其命名為**StartupDemo**。 -使用 NuGet 套件管理員安裝 `Microsoft.Owin.Host.SystemWeb`。 從 [**工具**] 功能表中，依序選取 [ **NuGet 套件管理員**] 和 [**套件管理員主控台**]。 輸入下列命令：

    [!code-powershell[Main](owin-startup-class-detection/samples/sample7.ps1)]
2. 新增 OWIN startup 類別。 在 Visual Studio 2017 中以滑鼠右鍵按一下專案，然後選取 [新增**類別**]。在 [**加入新專案**] 對話方塊的 [搜尋] 欄位中輸入*OWIN* ，並將名稱變更為 Startup.cs，然後選取 [**新增**]。

     ![](owin-startup-class-detection/_static/image1.png)

   下次您想要新增*Owin 啟動類別*時，它會出現在 [**新增**] 功能表中。

     ![](owin-startup-class-detection/_static/image2.png)

   或者，您也可以用滑鼠右鍵按一下專案，然後依**序選取 [** 新增] 和 [**新專案**]，然後選取 [ **Owin] 啟動類別**。

     ![](owin-startup-class-detection/_static/image3.png)

- 將*Startup.cs*檔案中產生的程式碼取代為下列內容：

    [!code-csharp[Main](owin-startup-class-detection/samples/sample8.cs?highlight=5,7,15-28,31-34)]

  `app.Use` lambda 運算式是用來將指定的中介軟體元件註冊至 OWIN 管線。 在此情況下，我們會先設定傳入要求的記錄，再回應傳入的要求。 `next` 參數是管線中下一個元件的委派（ [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) [&lt; 工作](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx)&gt;）。 `app.Run` lambda 運算式會將管線連結到傳入的要求，並提供回應機制。
     > [!NOTE]
     > 在上述程式碼中，我們已將 `OwinStartup` 屬性標記為批註，而我們將依賴執行名為 `Startup` 的類別。-按***F5***執行應用程式。 按幾次 [重新整理]。

    ![](owin-startup-class-detection/_static/image4.png) 注意：本教學課程中的影像所顯示的數位不會符合您看到的數位。 當您重新整理頁面時，會使用毫秒字串來顯示新的回應。
  您可以在 [**輸出**] 視窗中看到追蹤資訊。

    ![](owin-startup-class-detection/_static/image5.png)

## <a name="add-more-startup-classes"></a>新增更多啟動類別

在本節中，我們將新增另一個 Startup 類別。 您可以將多個 OWIN 啟動類別新增至您的應用程式。 例如，您可能會想要建立用於開發、測試和生產環境的啟動類別。

1. 建立新的 OWIN 啟動類別，並將其命名為 `ProductionStartup`。
2. 使用下列程式碼取代產生的程式碼：

    [!code-csharp[Main](owin-startup-class-detection/samples/sample9.cs?highlight=14-18)]
3. 按下 Control F5 以執行應用程式。 `OwinStartup` 屬性會指定執行生產啟動類別。

    ![](owin-startup-class-detection/_static/image6.png)
4. 建立另一個 OWIN 啟動類別，並將其命名為 `TestStartup`。
5. 使用下列程式碼取代產生的程式碼：

    [!code-csharp[Main](owin-startup-class-detection/samples/sample10.cs?highlight=6,14-18)]

   上述 `OwinStartup` 屬性多載會將 `TestingConfiguration` 指定為啟動類別的*易記*名稱。
6. 開啟*web.config*檔案，並新增 OWIN 應用程式啟動金鑰，它會指定啟動類別的易記名稱：

    [!code-xml[Main](owin-startup-class-detection/samples/sample11.xml?highlight=3-5)]
7. 按下 Control F5 以執行應用程式。 應用程式設定元素會採用上述專案，並執行測試設定。

    ![](owin-startup-class-detection/_static/image7.png)
8. 從 `TestStartup` 類別中的 `OwinStartup` 屬性移除*易記*名稱。

    [!code-csharp[Main](owin-startup-class-detection/samples/sample12.cs)]
9. 以下列內容取代*web.config*檔案中的 OWIN 應用程式啟動金鑰：

    [!code-xml[Main](owin-startup-class-detection/samples/sample13.xml)]
10. 將每個類別中的 `OwinStartup` 屬性還原為 Visual Studio 所產生的預設屬性代碼：

    [!code-csharp[Main](owin-startup-class-detection/samples/sample14.cs)]

    下列每個 OWIN 應用程式啟動金鑰都會導致生產環境類別執行。

    [!code-xml[Main](owin-startup-class-detection/samples/sample15.xml)]

    最後一個啟動金鑰會指定啟動設定方法。 下列 OWIN 應用程式啟動金鑰可讓您將 configuration 類別的名稱變更為 `MyConfiguration`。

    [!code-xml[Main](owin-startup-class-detection/samples/sample16.xml)]

## <a name="using-owinhostexe"></a>使用 Owinhost

1. 以下列標記取代 Web.config 檔案：

    [!code-xml[Main](owin-startup-class-detection/samples/sample17.xml?highlight=3-6)]

   最後一個索引鍵是，因此在此情況下會指定 `TestStartup`。
2. 從 PMC 安裝 Owinhost：

    [!code-console[Main](owin-startup-class-detection/samples/sample18.cmd)]
3. 流覽至應用程式資料夾（*包含 web.config 檔案*的資料夾），然後在命令提示字元中輸入：

    [!code-console[Main](owin-startup-class-detection/samples/sample19.cmd)]

   命令視窗會顯示：

    [!code-console[Main](owin-startup-class-detection/samples/sample20.cmd)]
4. 以 `http://localhost:5000/`的 URL 啟動瀏覽器。

    ![](owin-startup-class-detection/_static/image8.png)

   OwinHost 遵守上述的啟動慣例。
5. 在命令視窗中，按 Enter 鍵結束 OwinHost。
6. 在 `ProductionStartup` 類別中，新增下列 OwinStartup 屬性，以指定易記名稱*ProductionConfiguration*。

    [!code-csharp[Main](owin-startup-class-detection/samples/sample21.cs)]
7. 在命令提示字元中輸入：

    [!code-console[Main](owin-startup-class-detection/samples/sample22.cmd)]

   已載入生產啟動類別。
    ![](owin-startup-class-detection/_static/image9.png)

   我們的應用程式有多個啟動類別，在此範例中，我們已延後要載入的啟動類別，直到執行時間為止。
8. 測試下列執行時間啟動選項：

    [!code-console[Main](owin-startup-class-detection/samples/sample23.cmd)]
