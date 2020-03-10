---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
title: 使用 Visual Studio ASP.NET Web 部署：部署額外的檔案 |Microsoft Docs
author: tdykstra
description: 本教學課程系列將示範如何透過互動，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商主機服務提供者。
ms.author: riande
ms.date: 03/23/2015
ms.assetid: 1cd91055-84bc-42c6-9d80-646f41429d4d
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
msc.type: authoredcontent
ms.openlocfilehash: eaa3141c22980f0c816e2f33b5597ac9fe69c23c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78548409"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-extra-files"></a>使用 Visual Studio ASP.NET Web 部署：部署額外的檔案

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本教學課程系列說明如何使用 Visual Studio 2012 或 Visual Studio 2010，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商裝載提供者。 如需有關數列的詳細資訊，請參閱[本系列的第一個教學](introduction.md)課程。

## <a name="overview"></a>概觀

本教學課程示範如何擴充 Visual Studio web 發佈管線，以在部署期間執行其他工作。 工作是將不在專案資料夾中的額外檔案複製到目的地網站。

在本教學課程中，您將複製一個額外的檔案： [*機器人 .txt*]。 您想要將此檔案部署至預備環境，而不是實際執行。 在[部署至生產](deploying-to-production.md)教學課程中，您已將此檔案新增至專案，並已設定生產發行設定檔將其排除。 在本教學課程中，您將會看到處理這種情況的替代方法，其中一種方式適用于您想要部署但不想包含在專案中的任何檔案。

## <a name="move-the-robotstxt-file"></a>移動機器人 .txt 檔案

若要準備其他處理*機器人*的方法，請在本教學課程的這一節中，將檔案移至未包含在專案中的資料夾，並從預備環境中刪除的 [*機器人]。* 您必須從預備環境中刪除檔案，如此一來，您就可以確認將檔案部署至該環境的新方法是否正常運作。

1. 在**方案總管**中，以滑鼠右鍵按一下 [*機器人 .txt* ] 檔案，然後按一下 [**從專案排除**]。
2. 使用 Windows 檔案瀏覽器，在方案資料夾中建立新資料夾，並將其命名為*ExtraFiles*。
3. 將*ContosoUniversity*專案資料夾中的*機器人 .txt*檔案移至*ExtraFiles*資料夾。

    ![ExtraFiles 資料夾](deploying-extra-files/_static/image1.png)
4. 使用您的 FTP 工具，從預備網站刪除*機器人 .txt*檔案。

    或者，您可以在預備發行設定檔的 [**設定**] 索引標籤上，選取 [檔案**發佈選項**] 下的 [**移除目的地的其他**檔案]，然後重新發佈至預備環境。

## <a name="update-the-publish-profile-file"></a>更新發行設定檔

在預備環境中，您只需要有*機器人 .txt* ，因此，您需要更新才能部署的發行設定檔是預備環境。

1. 在 Visual Studio 中，開啟 *.pubxml*。
2. 在檔案結尾的結束 `</Project>` 標記之前，新增下列標記：

    [!code-xml[Main](deploying-extra-files/samples/sample1.xml)]

    此程式碼會建立新的*目標*，以收集要部署的其他檔案。 目標是由一或多個工作所組成，MSBuild 將根據您指定的條件來執行。

    `Include` 屬性指定要在其中尋找檔案的資料夾是*ExtraFiles*，位於與專案資料夾相同的層級。 MSBuild 會收集該資料夾中的所有檔案，並從任何子資料夾以遞迴方式進行（雙星號指定遞迴子資料夾）。 使用此程式碼，您可以將多個檔案和檔案放在*ExtraFiles*資料夾內的子資料夾中，而全部都將會部署。

    `DestinationRelativePath` 專案指定應將資料夾和檔案複製到目的地網站的根資料夾，其檔案和資料夾結構與在*ExtraFiles*資料夾中找到的相同。 如果您想要複製*ExtraFiles*資料夾本身，`DestinationRelativePath` 值會是*ExtraFiles\%（RecursiveDir）% （Filename）% （Extension）* 。
3. 在檔案結尾的結尾 `</Project>` 標記之前，新增下列標記以指定執行新目標的時機。

    [!code-xml[Main](deploying-extra-files/samples/sample2.xml)]

    此程式碼會在執行將檔案複製到目的地資料夾的目標時，執行新的 `CustomCollectFiles` 目標。 發行與部署套件建立有一個不同的目標，如果您決定使用部署套件（而不是發佈）來部署，新的目標就會插入兩個目標。

    *.Pubxml*檔案現在看起來如下列範例所示：

    [!code-xml[Main](deploying-extra-files/samples/sample3.xml?highlight=53-71)]
4. 儲存並關閉 *.pubxml*檔案。

## <a name="publish-to-staging"></a>發行至預備環境

使用單鍵發佈或命令列，使用暫存設定檔發行應用程式。

如果您使用單鍵發佈，您可以在**預覽**視窗中確認將會複製*機器人 .txt* 。 否則，請使用您的 FTP 工具來確認在部署之後，會在網站的根資料夾中執行*機器人 .txt*檔案。

## <a name="summary"></a>總結

這會完成這一系列的教學課程，將 ASP.NET web 應用程式部署到協力廠商裝載提供者。 如需這些教學課程中所涵蓋之任何主題的詳細資訊，請參閱[ASP.NET 部署內容對應](https://go.microsoft.com/fwlink/p/?LinkId=282413)。

## <a name="more-information"></a>詳細資訊

如果您知道如何使用 MSBuild 檔案，您可以在 *.pubxml*檔（適用于設定檔特定的工作）或專案的*wpp*檔案（適用于所有設定檔的工作）中撰寫程式碼，以自動化許多其他部署工作。 如需 *.pubxml*和*wpp .targets*檔案的詳細資訊，請參閱[如何：在發行設定檔（. .Pubxml）檔案中編輯部署設定和 Visual Studio Web 專案中的 wpp .targets](https://msdn.microsoft.com/library/ff398069)檔。 如需 MSBuild 程式碼的基本簡介，請參閱企業部署系列中的**專案檔案剖析** [：瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔。 若要瞭解如何使用 MSBuild 檔案在您自己的案例中執行工作，請參閱這本書：在[Microsoft Build Engine：使用 MSBuild 和 Team Foundation Build](http://msbuildbook.com) By Sayed Ibraham Hashimi 和 William Bartholomew。

## <a name="acknowledgements"></a>通知

我想感謝下列人對本教學課程系列的內容做出重大貢獻：

- [Alberto Poblacion，MVP &amp; MCT，西班牙](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- Jarod Ferguson，資料平臺開發 MVP，美國
- Microsoft 的 Mittal
- [Jon Galloway](https://weblogs.asp.net/jgalloway) （twitter： [@jongalloway](http://twitter.com/jongalloway)）
- [Kristina Olson，Microsoft](https://blogs.iis.net/krolson/default.aspx)
- [Mike Pope，Microsoft](http://www.mikepope.com/blog/DisplayBlog.aspx)
- Mohit Srivastava，Microsoft
- [Raffaele Rialdi，義大利](http://www.iamraf.net/)
- [Rick Anderson，Microsoft](https://blogs.msdn.com/b/rickandy/)
- [Sayed Hashimi，Microsoft](http://sedodream.com/default.aspx)（twitter： [@sayedihashimi](http://twitter.com/sayedihashimi)）
- [Scott Hanselman](http://www.hanselman.com/blog/) （twitter： [@shanselman](http://twitter.com/shanselman)）
- [Scott Hunter，Microsoft](https://blogs.msdn.com/b/scothu/) （twitter： [@coolcsh](http://twitter.com/coolcsh)）
- [Srđan Božović，塞爾維亞](http://msforge.net/blogs/zmajcek/)
- [Vishal Joshi，Microsoft](http://vishaljoshi.blogspot.com/) （twitter： [@vishalrjoshi](http://twitter.com/vishalrjoshi)）

> [!div class="step-by-step"]
> [上一頁](command-line-deployment.md)
> [下一頁](troubleshooting.md)
