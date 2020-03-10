---
uid: whitepapers/ms03-32-issue
title: 套用 IE 的安全性更新之後，修正「伺服器應用程式無法使用」錯誤Microsoft Docs
author: rick-anderson
description: 本文說明的修補程式可修正 Internet Explorer 的 MS03-32 安全性更新問題，這會影響在 Wi-fi 上執行的 ASP.NET 1.0 應用程式。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 1365eebb-bdf7-4a05-8d18-7f200531be55
msc.legacyurl: /whitepapers/ms03-32-issue
msc.type: content
ms.openlocfilehash: e0b6776cbfe22e341ac7105f03daac5074b480fc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574183"
---
# <a name="fix-for-server-application-unavailable-error-after-applying-security-update-for-ie"></a>套用 IE 的安全性更新之後，修正「無法使用伺服器應用程式」錯誤

> 本文說明的修補程式可修正 Internet Explorer 的 MS03-32 安全性更新問題，這會影響在 Windows XP Professional 上執行的 ASP.NET 1.0 應用程式。
> 
> 適用于 ASP.NET 1.0 和 Windows XP Professional。

Microsoft 發現 Windows XP 上執行的 Internet Explorer 安全性修補程式和 ASP.NET 1.0 的 MS03-32 安全性更新發生問題。 您可以手動安裝此修補程式，或從 Windows Update 網站取得最近的重大更新。

這個問題的徵兆是，在 Windows XP 電腦上安裝修補程式之後，ASP.NET 在本機 IIS 5.1 web 伺服器上執行之應用程式的所有要求都會產生一則錯誤訊息，指出「伺服器應用程式無法使用」。 對遠端網頁伺服器的要求不會受到影響。

這個問題只會影響在 Windows XP 上執行 ASP.NET 1.0 的安裝。 它不會影響執行 Windows 2000 或 Windows Server 2003 的機器。 它也不會影響執行 Windows XP 且已安裝 ASP.NET 1.1 的機器。

請注意，此問題**不是**ASP.NET 的安全性錯誤。 它不**會**開啟或允許對 ASP.NET 應用程式或伺服器進行任何惡意的攻擊。 相反地，它只是由修補程式本身所造成的功能性 bug。

我們正在努力解決此問題的永久性解決方案。 在此同時，您可以執行下列批次檔，做為問題的因應措施。 批次檔會執行下列動作：

1. 停止 IIS 和 ASP.NET 狀態服務
2. 刪除並重新建立具有已知暫時密碼的 ASPNET 帳戶
3. 使用 Windows `runas` 命令來啟動可執行檔，以建立 ASPNET 使用者設定檔
4. 重新註冊 ASP.NET。 這會為帳戶建立新的隨機密碼，並為其套用預設的 ASP.NET 存取控制設定
5. 重新開機 IIS 服務

批次檔包含「<strong>1pass\@word</strong>」的硬式編碼暫時密碼，當批次檔執行時，系統會提示您輸入 runas 命令。 Runas 命令完成之後，會使用強式隨機值重新建立 ASPNET 帳戶密碼。 請注意，如果硬式編碼的密碼不符合環境中的密碼複雜性需求，批次檔可能會失敗。 如果是這種情況，您可以將它變更為適用于您環境的另一個值。

*> [!IMPORTANT]* 如果您已新增 ASPNET 帳戶的自訂存取控制設定或資料庫帳戶許可權，則必須在此批次檔完成之後重新建立。 這是因為重新建立帳戶時，將會取得新的安全識別碼（SID）。

*> [!IMPORTANT]* 如果您使用 ASPNET 帳戶以外的自訂帳戶來執行 ASP.NET 背景工作進程，則不應該執行此批次檔。 相反地，您應該以互動方式登入，或使用 runas 命令搭配該帳戶，這會建立該帳戶的使用者設定檔。

批次檔包含在下面的自我解壓縮封存中。 使用方式：

1. 您必須以具有系統管理員許可權的帳戶身分執行
2. [下載並開啟自動解壓縮的可執行檔](ms03-32-issue/_static/fixup1.exe)
3. 將內容解壓縮至 c：\
4. 選取 [執行 ...]從 [開始] 功能表，然後輸入 `cmd.exe`
5. 在 [開啟命令] 視窗中，輸入 `c:\fixup.cmd`。
6. 出現提示時，輸入<strong>1pass\@word</strong>  做為密碼。
7. 如果您先前已有 ASPNET 帳戶的自訂存取控制設定或資料庫帳戶許可權，就必須立即重新套用這些設定。

許多讀者表達歉意會造成這種情況引起的不便。 我們會在其他資訊可供使用時張貼。

下方的矩陣詳述受此問題影響的平臺和版本。

| .NET Framework | Platform | 會 |
| --- | --- | --- |
| 版本1。0 | Windows 2000 Professional | 否 |
| 版本1。0 | Windows 2000 Server | 否 |
| 版本1。0 | Windows XP Professional | [是] |
| 版本1。0 | Windows Server 2003 | 否 |
| 版本1。0 | Windows XP Home with Cassini | 否 |
| 1\.1 版 | Windows 2000 Professional | 否 |
| 1\.1 版 | Windows 2000 Server | 否 |
| 1\.1 版 | Windows XP Professional | 否 |
| 1\.1 版 | Windows Server 2003 | 否 |
| 1\.1 版 | Windows XP Home with Cassini | 否 |

謹此，   
 ASP.NET 小組
