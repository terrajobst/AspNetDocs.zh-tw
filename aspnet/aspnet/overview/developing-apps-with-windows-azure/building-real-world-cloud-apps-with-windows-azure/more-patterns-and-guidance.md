---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/more-patterns-and-guidance
title: 更多模式和指導方針（使用 Azure 建立真實世界的雲端應用程式） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會說明13個模式和實務，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 7e97cfc3-d830-4002-8ff7-5790d1ff49e6
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/more-patterns-and-guidance
msc.type: authoredcontent
ms.openlocfilehash: afade34477d1136883e7543d09e73dfbe435690e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585353"
---
# <a name="more-patterns-and-guidance-building-real-world-cloud-apps-with-azure"></a>更多模式和指導方針（使用 Azure 建立真實世界的雲端應用程式）

由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom 作者: dykstra](https://github.com/tdykstra)

[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。 其中說明13種模式和作法，可協助您成功開發雲端 web 應用程式。 如需電子書的相關資訊，請參閱[第一章](introduction.md)。

您現在已經看過13種模式，可提供如何在雲端運算中成功的指引。 這些只是幾個適用于雲端應用程式的模式。 以下是一些更多雲端運算主題，以及協助它們的資源：

- 將現有的內部部署應用程式遷移至雲端。 

    - 將[應用程式移至雲端](https://msdn.microsoft.com/library/ff728592.aspx)。 依 Microsoft 的模式和實務的電子書。 也可做為[硬式複製的平裝](https://www.amazon.com/dp/1621140202)。
    - 正在[遷移 Microsoft 的 ASP.NET 和 IIS.NET](https://go.microsoft.com/fwlink/?LinkId=400656)。 Robert McMurray 的案例研究。
    - [將第 4 &amp; Mayor 移到 Azure 網站](http://www.jeff.wilcox.name/2013/04/4thandmayor-azure-websites/)。 Jeff Wilcox 的 Blog 文章 chronicling 他的經驗，將 web 應用程式從 Amazon Web Services 移至 Azure App Service 的 Web Apps。
    - [將應用程式移至 Azure：有哪些變更？](https://azure.microsoft.com/documentation/videos/web-sites-internals-and-the-file-system/) Stefan Schackow 的短片說明 Azure App Service 的 Web Apps 中的檔案系統存取。
    - [Azure 混合式雲端](https://www.amazon.com/dp/B00EOP4UQW)。 Danny Garber、Jamal Malik 和 Adam Fazio 的硬拷貝書籍或電子書。
- 雲端應用程式獨有的安全性、驗證和授權問題

    - [Azure 安全性指引](https://azure.microsoft.com/blog/2014/02/10/best-practices-windows-azure-websites-waws/)
    - [Microsoft 模式和實務-Azure 指引](https://msdn.microsoft.com/library/dn568099.aspx)。 請參閱閘道管理員模式，同盟身分識別模式。
    - [Azure 網路安全性](https://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx)。 白皮書： Ashin Palekar。

另請參閱[Microsoft 模式和實務的](https://msdn.microsoft.com/library/dn568099.aspx)其他雲端運算模式和指引-Azure 指引。

<a id="resources"></a>
## <a name="resources"></a>資源

本電子書中的每一章節都會提供資源的連結，以取得該特定主題的詳細資訊。 下列清單提供最佳作法的連結，以及使用 Azure 成功進行雲端開發的建議模式。

Documentation

- [Azure 上大規模服務設計的最佳作法雲端服務](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 以標記 Simm 和 Michael Thomassy 的技術白皮書。
- [損毀修復：具有恢復功能的雲端架構指引](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)。 白皮書： Marc Mercuri、Ulrich Homann 和 Andrew Townhill。 網頁版的防安全影片系列。
- [Azure 指引](https://azure.microsoft.com/develop/net/guidance/)適用于開發 Azure 應用程式相關官方檔的入口網站頁面。

Videos

- [使用 Azure 建立真實世界的雲端應用程式-第1部分](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324)和[第2部分](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)。 Scott Guthrie 的簡報影片，這是本電子書的依據。 提供于2013年9月的 Tech Ed 澳大利亞。 舊版的相同簡報是在2013年6月的挪威開發人員會議（NDC）提供： [NDC 第1部分](http://vimeo.com/68215538)， [NDC 第2部分](http://vimeo.com/68215602)。
- [防安全功能：建立可擴充、可復原的雲端服務](https://channel9.msdn.com/Series/FailSafe)。 Ulrich Homann、Marc Mercuri 和 Mark Simm 的九個部分影片系列。 提供如何架構雲端應用程式的400層級觀點。 此系列著重于建議模式背後的理論和原因;如需詳細的作法詳細資料，請參閱以標記 Simm 建立大數列。
- [打造 Big：從 Azure 客戶學習到的經驗-第1部分](https://channel9.msdn.com/Events/Build/2012/3-029)和[第2部分](https://channel9.msdn.com/Events/Build/2012/3-030)。 Simon Davies 並標記 Simm 的兩部分影片系列，類似于防安全系列，但導向至實際執行。

程式碼範例

- [本電子書所附的修正 It 應用程式](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4?cdn_id=2013-12-03-002)。
- [Azure C#中的雲端服務基礎，適用于 Visual Studio 2012](https://aka.ms/csf)。 Microsoft 程式碼庫網站中可下載的專案，包括 Microsoft 客戶諮詢團隊（CAT）所開發的程式碼和檔。 示範許多在安全的極力提倡中的最佳作法，以及建立絕佳的影片系列和安全的技術白皮書。 [程式碼庫] 頁面也會連結到專案作者所提供的廣泛檔，特別是在專案描述頂端附近的藍色方塊中，尤其是 [[雲端服務基礎 wiki 集合](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx)] 連結。 此專案和其檔集仍在開發中，使其更適合用於許多主題的資訊，而非類似但較舊的白皮書。

硬複製書籍

- [雲端運算 bible 》](https://www.amazon.com/dp/0470903562)。 依 Barrie Sosinsky。
- [發行！設計和部署已準備好用於生產環境的軟體](https://www.amazon.com/Release-It-Production-Ready-Pragmatic-Programmers/dp/0978739213)。 由 Michael T. Nygard。
- [雲端架構模式：使用 Microsoft Azure](http://shop.oreilly.com/product/0636920023777.do)。 依帳單 Wilder。
- [Windows Azure 平臺](https://www.amazon.com/dp/1430235632)。 依 Tejaswi Redkar。
- [適用于啟動的 Windows Azure 程式設計模式](https://www.amazon.com/dp/1849685606)。 依 Riccardo Becker。
- [Microsoft Windows Azure 開發手冊](https://www.amazon.com/dp/1849682224)。 依 Neil Mackenzie。

最後，當您開始建立真實世界的應用程式並在 Azure 中執行時，您可能會需要專家的協助。 您可以在[Azure 論壇或 StackOverflow](https://azure.microsoft.com/support/forums/)之類的社區網站中提出問題，也可以直接與 Microsoft 聯繫以進行 Azure 支援。 Microsoft 提供數個層級的技術支援：如需這些選項的摘要和比較，請參閱[Azure 支援](https://azure.microsoft.com/support/plans/)。

<a id="acknowledgments"></a>
## <a name="acknowledgments"></a>致謝

此內容是由 Tom 作者: dykstra、Rick Anderson 和 Mike Wasson 所撰寫。 大部分的原始內容來自[Scott Guthrie](https://weblogs.asp.net/scottgu/)，而他又從 Mark 和 Microsoft 客戶諮詢團隊（CAT）中的材料中進行繪製。

Microsoft 的許多其他同事已在草稿和程式碼上檢查並加上批註：

- Tim Ammann-已複習自動化章節。
- Christopher Bennage-審查並測試修正程式碼。
- Ryan Berry-審查 CD/CI 章節。
- Vittorio Bertocci-已審查 SSO 章節。
- Chris Clayton-協助解決 PowerShell 腳本中的技術問題。
- Conor Cunningham-審查資料儲存選項一章。
- Carlos Farre-審查並測試修正程式碼的安全性問題。
- Larry Franks-審查遙測和監視一章。
- Jonathan Gao-已審查資料儲存選項章節的 Hadoop 和 MapReduce 區段。
- Sidney Higa-審查所有章節。
- Gordon Hogenson-已審查原始檔控制章節。
- Tamra Myers-已審核的資料儲存體選項、blob 和佇列章節。
- Pranav 請參閱 rastogi-已審查 SSO 章節。
- 6月 Blender Rogers-新增了 PowerShell 自動化腳本的錯誤處理和協助。
- Mani-ramaswamy Subramanian-審查所有章節，並帶領修正 It 程式碼的程式碼審查和測試流程。
- Shaun Tinline-jones-第一章-已複習資料分割章節。
- Selcin Tukarslan 審閱的章節，其中涵蓋 SQL Database 和 SQL Server。
- Edward 適用于 SSO 章節的 Wu 提供範例程式碼。
- Guang 停止的高階-撰寫了 PowerShell 自動化腳本。

[Microsoft 開發人員指導方針諮詢委員會](https://aka.ms/DGAC)（DGAC）的成員也已在草稿上複習並加上批註：

- Jean-L u c Boucho
- Catalin Gheorghiu
- Wouter de Kort
- Carlos dos Santos
- Neil Mackenzie
- Dennis Persson
- Sunil Sabat
- [Aleksey Sinyagin](http://www.linkedin.com/in/sinyagin)
- Bill Wagner
- Michael 木材

DGAC 的其他成員已在初步大綱中審閱並加上批註：

- Damir Arh
- Edward Bakker
- Srdjan Bozovic
- Ming Man Chan
- Gianni Rosa Gallina
- 聖保羅 Morgado
- Jason Oliveira
- Alberto Poblacion
- Ryan Riley
- Perez 的 Tsisah
- Roger Whitehead
- Pawel Wilkosz

> [!div class="step-by-step"]
> [上一頁](queue-centric-work-pattern.md)
> [下一頁](the-fix-it-sample-application.md)
