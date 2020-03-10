---
uid: web-pages/overview/getting-started/11-adding-email-to-your-web-site
title: 從 ASP.NET Web Pages （Razor）網站傳送電子郵件 |Microsoft Docs
author: Rick-Anderson
description: 本章說明如何從網站傳送自動化的電子郵件訊息。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: fc49bcb9-f1a9-4048-8c3f-b60951853200
msc.legacyurl: /web-pages/overview/getting-started/11-adding-email-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 23e9717329525fb5a0ed505c9dc94505d4f9dbbe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634712"
---
# <a name="sending-email-from-an-aspnet-web-pages-razor-site"></a>從 ASP.NET Web Pages （Razor）網站傳送電子郵件

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本文說明當您使用 ASP.NET Web Pages （Razor）時，如何從網站傳送電子郵件訊息。
> 
> 您將學到什麼：
> 
> - 如何從您的網站傳送電子郵件訊息。
> - 如何將檔案附加至電子郵件訊息。
> 
> 這是本文中引進的 ASP.NET 功能：
> 
> - `WebMail` helper。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）3
>   
> 
> 本教學課程也適用于 ASP.NET Web Pages 2。

<a id="Sending_Email_Messages"></a>
## <a name="sending-email-messages-from-your-website"></a>從您的網站傳送電子郵件訊息

您可能需要從您的網站傳送電子郵件的原因有很多種。 您可能會傳送確認訊息給使用者，或者您可能會將通知傳送給自己（例如，新使用者已註冊）。`WebMail` 協助程式可讓您輕鬆地傳送電子郵件。

若要使用 `WebMail` helper，您必須具有 SMTP 伺服器的存取權。 （SMTP 代表*簡單郵件傳輸通訊協定*）。SMTP 伺服器是一種電子郵件伺服器，只會將郵件轉寄給收&#8212;件者的伺服器，它是電子郵件的輸出端。 如果您使用網站的主控提供者，他們可能會設定電子郵件給您，而他們可以告訴您 SMTP 伺服器名稱的內容。 如果您在公司網路內工作，系統管理員或您的 IT 部門通常可以提供您可使用之 SMTP 伺服器的相關資訊。 如果您在家工作，甚至可以使用您一般的電子郵件提供者來進行測試，以告訴您其 SMTP 伺服器的名稱。 您通常需要：

- SMTP 伺服器的名稱。
- 埠號碼。 這幾乎都是25。 不過，您的 ISP 可能會要求您使用埠587。 如果您使用安全通訊端層（SSL）來傳送電子郵件，您可能需要不同的埠。 請洽詢您的電子郵件提供者。
- 認證（使用者名稱、密碼）。

在此程式中，您會建立兩個頁面。 第一頁的表單可讓使用者輸入描述，就像是填入技術支援表單一樣。 第一頁會將其資訊提交至第二頁。 在第二頁中，程式碼會解壓縮使用者的資訊，並傳送電子郵件訊息。 它也會顯示一則訊息，確認已收到問題報告。

![[影像]](11-adding-email-to-your-web-site/_static/image1.jpg)

> [!NOTE]
> 為了讓此範例保持簡單，程式碼會在您使用它的頁面中，初始化 `WebMail` helper。 不過，對於真實的網站而言，將初始化程式碼放在全域檔案中是較好的主意，以便為網站中的所有檔案初始化 `WebMail` helper。 如需詳細資訊，請參閱針對[ASP.NET Web Pages 自訂全網站行為](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers)。

1. 建立新的網站。
2. 新增名為*EmailRequest*的新頁面，並新增下列標記： 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample1.html)]

    請注意，form 元素的 `action` 屬性已設定為*ProcessRequest*。 這表示表單會提交至該頁面，而不是回到目前的頁面。
3. 將名為*ProcessRequest*的新頁面新增至網站，並新增下列程式碼和標記：   

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample2.cshtml)]

    在程式碼中，您會取得已提交至頁面之表單欄位的值。 接著，您可以呼叫 `WebMail` helper 的 `Send` 方法來建立和傳送電子郵件訊息。 在此情況下，要使用的值是由文字所組成，您可以使用從表單提交的值進行串連。

    此頁面的程式碼位於 `try/catch` 區塊內。 如果因任何原因而無法傳送電子郵件（例如設定不正確），則 `catch` 區塊中的程式碼會執行，並將 `errorMessage` 變數設定為已發生的錯誤。 （如需 `try/catch` 區塊或 `<text>` 標記的詳細資訊，請參閱[使用 Razor 語法進行 ASP.NET Web Pages 程式設計的簡介](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors)）。

    在頁面主體中，如果 `errorMessage` 變數是空的（預設值），則使用者會看到電子郵件訊息已傳送的訊息。 如果 `errorMessage` 變數設定為 true，則使用者會看到訊息，指出傳送訊息時發生問題。

    請注意，在顯示錯誤訊息的頁面部分中，有一個額外的測試： `if(debuggingFlag)`。 如果您在傳送電子郵件時遇到問題，您可以將此變數設定為 true。 當 `debuggingFlag` 為 true，且傳送電子郵件時發生問題時，會顯示額外的錯誤訊息，顯示當 ASP.NET 嘗試傳送電子郵件訊息時回報的內容。 公平警告：不過，ASP.NET 在無法傳送電子郵件訊息時回報的錯誤訊息可以是一般的。 例如，如果 ASP.NET 無法連線到 SMTP 伺服器（例如，因為您在伺服器名稱中發生錯誤），則會 `Failure sending mail`錯誤。

    > [!NOTE] 
    > 
    > **重要事項**當您從例外狀況物件（在程式碼中`ex`）收到錯誤訊息時，*請不要定期將*該訊息傳遞給使用者。 例外狀況物件通常會包含使用者不應該看到的資訊，甚至可能是安全性漏洞。 這就是為什麼這段程式碼包含變數 `debuggingFlag`，做為用來顯示錯誤訊息的參數，以及為什麼變數預設會設定為 false。 只有當您在傳送電子郵件時遇到問題，而且需要進行偵錯工具時，*才*應該將該變數設定為 true （因此會顯示錯誤訊息）。 一旦您已修正任何問題，請將 `debuggingFlag` 設回 false。

    修改程式碼中的下列電子郵件相關設定：

   - 將 `your-SMTP-host` 設定為您可以存取的 SMTP 伺服器名稱。
   - 將 `your-user-name-here` 設定為 SMTP 伺服器帳戶的使用者名稱。
   - 將 `your-account-password` 設定為 SMTP 伺服器帳戶的密碼。
   - 將 `your-email-address-here` 設定為您自己的電子郵件地址。 這是傳送訊息的來源電子郵件地址。 （有些電子郵件提供者不會讓您指定不同的 `From` 位址，而且會使用您的使用者名稱作為 `From` 位址）。

     > [!TIP] 
     > 
     > <a id="configuring_email_settings"></a>
     > ### <a name="configuring-email-settings"></a>正在設定電子郵件設定
     > 
     > 有時可能會有一項挑戰，就是確定您有適當的 SMTP 伺服器、埠號碼等等設定。 下列提供幾個秘訣：
     > 
     > - SMTP 伺服器名稱通常類似 `smtp.provider.com` 或 `smtp.provider.net`。 不過，如果您將網站發佈至主機服務提供者，該點的 SMTP 伺服器名稱可能會 `localhost`。 這是因為在您已發佈，且您的網站在提供者的伺服器上執行之後，電子郵件伺服器可能會從您的應用程式觀點來看。 伺服器名稱的這項變更可能表示您必須在發佈程式中變更 SMTP 伺服器名稱。
     > - 埠號碼通常是25。 不過，某些提供者會要求您使用埠587或其他通訊埠。
     > - 請確定您使用正確的認證。 如果您已將您的網站發佈至主控提供者，請使用提供者特別指出的認證做為電子郵件。 這些可能與您用來發佈的認證不同。
     > - 有時候您不需要認證。 如果您是使用個人 ISP 傳送電子郵件，您的電子郵件提供者可能已經知道您的認證。 發行之後，您可能需要使用與在本機電腦上測試時不同的認證。
     > - 如果您的電子郵件提供者使用加密，您必須將 `WebMail.EnableSsl` 設定為 `true`。
4. 在瀏覽器中執行*EmailRequest。* （在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）
5. 輸入您的名稱和問題描述，然後按一下 [**提交**] 按鈕。 系統會將您重新導向至*ProcessRequest* ，以確認您的訊息，並傳送電子郵件訊息給您。 

    ![[影像]](11-adding-email-to-your-web-site/_static/image2.jpg)

<a id="Sending_a_File"></a>
## <a name="sending-a-file-using-email"></a>使用電子郵件傳送檔案

您也可以傳送附加至電子郵件訊息的檔案。 在這個程式中，您會建立一個文字檔和兩個 HTML 頁面。 您將使用文字檔做為電子郵件附件。

1. 在網站中，加入新的文字檔，並將它命名為*myfile.txt .txt*。
2. 複製下列文字並貼到檔案中： 

    `Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.`
3. 建立名為*SendFile*的頁面，並新增下列標記： 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample3.html)]
4. 建立名為*ProcessFile*的頁面，並新增下列標記： 

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample4.cshtml)]
5. 在範例的程式碼中修改下列電子郵件相關設定：

    - 將 `your-SMTP-host` 設定為您可以存取的 SMTP 伺服器名稱。
    - 將 `your-user-name-here` 設定為 SMTP 伺服器帳戶的使用者名稱。
    - 將 `your-email-address-here` 設定為您自己的電子郵件地址。 這是傳送訊息的來源電子郵件地址。
    - 將 `your-account-password` 設定為 SMTP 伺服器帳戶的密碼。
    - 將 `target-email-address-here` 設定為您自己的電子郵件地址。 （如前所述，您通常會將電子郵件傳送給其他人，但若要進行測試，您可以將它傳送給自己。）
6. 在瀏覽器中執行*SendFile。*
7. 輸入您的名稱、主旨行，以及要附加的文字檔名稱（*myfile.txt .txt*）。
8. 按一下 `Submit` 按鈕。 就像之前一樣，您會被重新導向至*ProcessFile* ，以確認您的訊息，並將附加的檔案傳送給您電子郵件訊息。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他資源

- [ASP.NET Web Pages (Razor) 疑難排解指南](https://go.microsoft.com/fwlink/?LinkId=253001)
- [簡易郵件傳送通訊協定](https://msdn.microsoft.com/library/aa480435.aspx)
- [針對 ASP.NET Web Pages 自訂全網站行為](https://go.microsoft.com/fwlink/?LinkId=202906)
