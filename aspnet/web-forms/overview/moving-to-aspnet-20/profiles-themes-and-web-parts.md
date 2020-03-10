---
uid: web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
title: 設定檔、主題和 Web 組件 |Microsoft Docs
author: microsoft
description: ASP.NET 2.0 中的設定和檢測有重大變更。 新的 ASP.NET 設定 API 允許將設定變更為 pr 。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 92df4051-77c6-492c-bd34-23d24189cea4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
msc.type: authoredcontent
ms.openlocfilehash: cf5c45781be6d003d28c6aa27efa08032579a6dd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78587231"
---
# <a name="profiles-themes-and-web-parts"></a>設定檔、佈景主題與 Web 組件

由[Microsoft](https://github.com/microsoft)

> ASP.NET 2.0 中的設定和檢測有重大變更。 新的 ASP.NET 設定 API 可讓您以程式設計方式變更設定。 此外，有許多新的設定會允許新的設定和檢測。

ASP.NET 2.0 代表個人化網站區域的大幅改進。 除了我們已涵蓋的成員資格功能之外，ASP.NET 設定檔、主題和 Web 元件會大幅增強網站的個人化。

## <a name="aspnet-profiles"></a>ASP.NET 設定檔

ASP.NET 設定檔類似于會話。 差別在於設定檔是持續性的，而當瀏覽器關閉時，會話也會遺失。 會話和設定檔之間的另一個重大差異在於，設定檔是強型別，因此在開發過程中會為您提供 IntelliSense。

設定檔定義于應用程式的電腦設定檔或 web.config 檔案中。 （您無法在子資料夾的 web.config 檔案中定義設定檔）。下列程式碼會定義一個設定檔，以儲存網站訪客的名字和姓氏。

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample1.xml)]

配置檔案屬性的預設資料類型為 System.string。 在上述範例中，未指定任何資料類型。 因此 FirstName 和 LastName 屬性都是字串類型。 如先前所述，配置檔案屬性是強型別。 下列程式碼會為 Int32 類型的 age 新增新屬性。

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample2.xml)]

設定檔通常與 ASP.NET 表單驗證搭配使用。 與表單驗證搭配使用時，每個使用者都有與他們的使用者識別碼相關聯的個別設定檔。 不過，您也可以在匿名應用程式中使用設定檔中的 &lt;anonymousIdentification&gt; 專案和**allowAnonymous**屬性，來允許設定檔，如下所示：

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample3.xml)]

當匿名使用者流覽網站時，ASP.NET 會為使用者建立**ProfileCommon**的實例。 此設定檔會使用儲存在瀏覽器 cookie 中的唯一識別碼，將使用者識別為唯一的訪客。 如此一來，您就可以針對以匿名方式流覽的使用者儲存設定檔資訊。

## <a name="profile-groups"></a>設定檔群組

可以將設定檔的屬性分組。 藉由群組屬性，可以模擬特定應用程式的多個設定檔。

下列設定會為兩個群組設定 FirstName 和 LastName 屬性;購買者和潛在客戶。

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample4.xml)]

接著，您可以設定特定群組的屬性，如下所示：

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample5.cs)]

## <a name="storing-complex-objects"></a>儲存複雜物件

到目前為止，我們所討論的範例都已在設定檔中儲存簡單的資料類型。 您也可以使用**serializeAs**屬性指定序列化的方法，將複雜的資料類型儲存在設定檔中，如下所示：

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample6.xml)]

在此情況下，此類型為 PurchaseInvoice。 PurchaseInvoice 類別必須標記為可序列化，而且可以包含任意數目的屬性。 例如，如果 PurchaseInvoice 具有名為**NumItemsPurchased**的屬性，您可以在程式碼中參考該屬性，如下所示：

[!code-css[Main](profiles-themes-and-web-parts/samples/sample7.css)]

## <a name="profile-inheritance"></a>設定檔繼承

您可以建立要在多個應用程式中使用的設定檔。 藉由建立衍生自 ProfileBase 的設定檔類別，您可以使用 [**繼承**] 屬性在數個應用程式中重複使用設定檔，如下所示：

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample8.xml)]

在此情況下，類別**PurchasingProfile**看起來會像這樣：

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample9.cs)]

## <a name="profile-providers"></a>設定檔提供者

ASP.NET 設定檔會使用提供者模型。 預設提供者會使用 SqlProfileProvider 提供者，將資訊儲存在 Web 應用程式之 App\_Data 資料夾中的 SQL Server Express 資料庫中。 如果資料庫不存在，ASP.NET 就會在設定檔嘗試儲存資訊時自動建立它。

不過，在某些情況下，您可能會想要開發自己的設定檔提供者。 ASP.NET 設定檔功能可讓您輕鬆地使用不同的提供者。

在下列情況中，您會建立自訂設定檔提供者：

- 您需要將設定檔資訊儲存在資料來源中，例如在 FoxPro 資料庫或 Oracle 資料庫中，這不是由 .NET Framework 所包含的設定檔提供者所支援。
- 您需要使用與 .NET Framework 隨附的提供者所使用的資料庫架構不同的資料庫架構，來管理設定檔資訊。 常見的範例是您想要將設定檔資訊與現有 SQL Server 資料庫中的使用者資料進行整合。

### <a name="required-classes"></a>必要類別

若要執行設定檔提供者，您可以建立繼承 ProfileProvider 抽象類別的類別。 **ProfileProvider**抽象類別會輪流繼承 SettingsProvider 抽象類別，而此類別會繼承 ProviderBase 抽象類別。 由於此繼承鏈，除了**ProfileProvider**類別的必要成員之外，您還必須執行**SettingsProvider**和**ProviderBase**類別的必要成員。

下表描述您必須從**ProviderBase**、 **SettingsProvider**和**ProfileProvider**抽象類別來執行的屬性和方法。

### <a name="providerbase-members"></a>ProviderBase 成員

| **成員** | **說明** |
| --- | --- |
| Initialize 方法 | 將提供者實例的名稱當做輸入，並使用 NameValueCollection 設定。 用來設定提供者實例的選項和屬性值，包括在電腦設定或 Web.config 檔案中指定的實作為特定值和選項。 |

### <a name="settingsprovider-members"></a>SettingsProvider 成員

| **成員** | **說明** |
| --- | --- |
| ApplicationName 屬性 | 與每個設定檔一起儲存的應用程式名稱。 設定檔提供者會使用應用程式名稱，分別為每個應用程式儲存設定檔資訊。 這可讓多個 ASP.NET 應用程式在不同的應用程式中建立相同的使用者名稱時，使用相同的資料來源而不會發生衝突。 或者，多個 ASP.NET 應用程式可以藉由指定相同的應用程式名稱來共用設定檔資料來源。 |
| System.configuration.settingsprovider.getpropertyvalues 方法 | 接受 SettingsCoNtext 和 SettingsPropertyCollection 物件的輸入。 **SettingsCoNtext**會提供使用者的相關資訊。 您可以使用此資訊做為主要金鑰，以取得使用者的配置檔案屬性資訊。 使用**SettingsCoNtext**物件來取得使用者名稱，以及使用者是否已驗證或匿名。 **SettingsPropertyCollection**包含 SettingsProperty 物件的集合。 每個**SettingsProperty**物件都會提供屬性的名稱和類型，以及其他資訊，例如屬性的預設值，以及屬性是否為唯讀。 **System.configuration.settingsprovider.getpropertyvalues**方法會根據提供做為輸入的**SettingsProperty**物件，以 SettingsPropertyValue 物件的形式填入 SettingsPropertyValueCollection。 指定之使用者的資料來源中的值會指派給每個**SettingsPropertyValue**物件的 PropertyValue 屬性，並傳回整個集合。 呼叫方法也會將指定之使用者設定檔的 LastActivityDate 值更新為目前的日期和時間。 |
| SetPropertyValues 方法 | 接受**SettingsCoNtext**和**SettingsPropertyValueCollection**物件的輸入。 **SettingsCoNtext**會提供使用者的相關資訊。 您可以使用此資訊做為主要金鑰，以取得使用者的配置檔案屬性資訊。 使用**SettingsCoNtext**物件來取得使用者名稱，以及使用者是否已驗證或匿名。 **SettingsPropertyValueCollection**包含**SettingsPropertyValue**物件的集合。 每個**SettingsPropertyValue**物件都會提供屬性的名稱、類型和值，以及其他資訊，例如屬性的預設值，以及屬性是否為唯讀。 **SetPropertyValues**方法會針對指定的使用者更新資料來源中的配置檔案屬性值。 呼叫方法也會將指定之使用者設定檔的**LastActivityDate**和 LastUpdatedDate 值更新為目前的日期和時間。 |

### <a name="profileprovider-members"></a>ProfileProvider 成員

| **成員** | **說明** |
| --- | --- |
| DeleteProfiles 方法 | 接受使用者名稱的字串陣列做為輸入，並從資料來源刪除所有設定檔資訊和指定名稱的屬性值，其中應用程式名稱符合**ApplicationName**屬性值。 如果您的資料來源支援交易，建議您將所有刪除作業包含在交易中，如果有任何刪除操作失敗，則會回復交易並擲回例外狀況。 |
| DeleteProfiles 方法 | 接受 Profileinfo.txt 物件集合的輸入，並從資料來源刪除所有設定檔資訊，以及應用程式名稱符合**ApplicationName**屬性值的每個設定檔的屬性值。 如果您的資料來源支援交易，建議您在交易中包含所有刪除作業並回復交易，並在有任何刪除操作失敗時擲回例外狀況。 |
| DeleteInactiveProfiles 方法 | 接受 ProfileAuthenticationOption 值和 DateTime 物件的輸入，並從資料來源刪除所有設定檔資訊和屬性值，其中最後一個活動日期小於或等於指定的日期和時間，且應用程式名稱與**ApplicationName**屬性值相符。 **ProfileAuthenticationOption**參數會指定是否只會刪除匿名設定檔、僅限驗證的設定檔或所有設定檔。 如果您的資料來源支援交易，建議您在交易中包含所有刪除作業並回復交易，並在有任何刪除操作失敗時擲回例外狀況。 |
| GetAllProfiles 方法 | 接受**ProfileAuthenticationOption**值的輸入、指定頁面索引的整數、指定頁面大小的整數，以及將設定為設定檔總計數的整數參考。 傳回 ProfileInfoCollection，其中包含資料來源中的所有設定檔的**profileinfo.txt**物件，其中應用程式名稱與**ApplicationName**屬性值相符。 **ProfileAuthenticationOption**參數會指定是否只會傳回匿名設定檔、僅限已驗證的設定檔或所有設定檔。 **GetAllProfiles**方法所傳回的結果會受到頁面索引和頁面大小值的限制。 [頁面大小] 值會指定要在**ProfileInfoCollection**中傳回之**profileinfo.txt**物件的最大數目。 頁面索引值指定要傳回的結果頁面，其中1表示第一頁。 總計記錄的參數是 out 參數（您可以在 Visual Basic 中使用**ByRef** ），這會設定為設定檔總數。 例如，如果資料存放區包含應用程式13個設定檔，而頁面索引值是2，頁面大小為5，則傳回的**ProfileInfoCollection**會包含第六到第十個設定檔。 當方法傳回時，[記錄總數] 值會設為13。 |
| GetAllInactiveProfiles 方法 | 會採用**ProfileAuthenticationOption**值、 **DateTime**物件、指定頁面索引的整數、指定頁面大小的整數，以及將設定為設定檔總數的整數參考，做為輸入。 傳回**ProfileInfoCollection** ，其中包含資料來源中的所有設定檔的**profileinfo.txt**物件，其中最後一個活動日期小於或等於指定的**日期時間**，而且應用程式名稱與**ApplicationName**屬性值相符。 **ProfileAuthenticationOption**參數會指定是否只會傳回匿名設定檔、僅限已驗證的設定檔或所有設定檔。 **GetAllInactiveProfiles**方法所傳回的結果會受到頁面索引和頁面大小值的限制。 [頁面大小] 值會指定要在**ProfileInfoCollection**中傳回之**profileinfo.txt**物件的最大數目。 頁面索引值指定要傳回的結果頁面，其中1表示第一頁。 總計記錄的參數是 out 參數（您可以在 Visual Basic 中使用**ByRef** ），這會設定為設定檔總數。 例如，如果資料存放區包含應用程式13個設定檔，而頁面索引值是2，頁面大小為5，則傳回的**ProfileInfoCollection**會包含第六到第十個設定檔。 當方法傳回時，[記錄總數] 值會設為13。 |
| FindProfilesByUserName 方法 | 接受**ProfileAuthenticationOption**值的輸入、包含使用者名稱的字串、指定頁面索引的整數、指定頁面大小的整數，以及將設定為設定檔總計數的整數參考。 傳回**ProfileInfoCollection** ，其中包含資料來源中所有設定檔的**profileinfo.txt**物件，其中的使用者名稱符合指定的使用者名稱，而且應用程式名稱與**ApplicationName**屬性值相符。 **ProfileAuthenticationOption**參數會指定是否只會傳回匿名設定檔、僅限已驗證的設定檔或所有設定檔。 如果您的資料來源支援額外的搜尋功能（例如萬用字元），您可以為使用者名稱提供更廣泛的搜尋功能。 **FindProfilesByUserName**方法所傳回的結果會受到頁面索引和頁面大小值的限制。 [頁面大小] 值會指定要在**ProfileInfoCollection**中傳回之**profileinfo.txt**物件的最大數目。 頁面索引值指定要傳回的結果頁面，其中1表示第一頁。 總計記錄的參數是 out 參數（您可以在 Visual Basic 中使用**ByRef** ），這會設定為設定檔總數。 例如，如果資料存放區包含應用程式13個設定檔，而頁面索引值是2，頁面大小為5，則傳回的**ProfileInfoCollection**會包含第六到第十個設定檔。 當方法傳回時，[記錄總數] 值會設為13。 |
| FindInactiveProfilesByUserName 方法 | 接受**ProfileAuthenticationOption**值的輸入、包含使用者名稱的字串、 **DateTime**物件、指定頁面索引的整數、指定頁面大小的整數，以及將設定為設定檔總計數的整數參考。 傳回**ProfileInfoCollection** ，其中包含資料來源中所有設定檔的**profileinfo.txt**物件，其中的使用者名稱符合指定的使用者名稱，其中最後一個活動日期小於或等於指定的**日期時間**，以及應用程式名稱與**ApplicationName**屬性值相符的位置。 **ProfileAuthenticationOption**參數會指定是否只會傳回匿名設定檔、僅限已驗證的設定檔或所有設定檔。 如果您的資料來源支援額外的搜尋功能（例如萬用字元），您可以為使用者名稱提供更廣泛的搜尋功能。 **FindInactiveProfilesByUserName**方法所傳回的結果會受到頁面索引和頁面大小值的限制。 [頁面大小] 值會指定要在**ProfileInfoCollection**中傳回之**profileinfo.txt**物件的最大數目。 頁面索引值指定要傳回的結果頁面，其中1表示第一頁。 總計記錄的參數是 out 參數（您可以在 Visual Basic 中使用**ByRef** ），這會設定為設定檔總數。 例如，如果資料存放區包含應用程式13個設定檔，而頁面索引值是2，頁面大小為5，則傳回的**ProfileInfoCollection**會包含第六到第十個設定檔。 當方法傳回時，[記錄總數] 值會設為13。 |
| GetNumberOfInActiveProfiles 方法 | 接受**ProfileAuthenticationOption**值和**DateTime**物件的輸入，並傳回資料來源中的所有設定檔計數，其中最後一個活動日期小於或等於指定的**日期時間**，且應用程式名稱與**ApplicationName**屬性值相符。 **ProfileAuthenticationOption**參數指定只會計算匿名設定檔、僅限已驗證的設定檔或所有設定檔。 |

### <a name="applicationname"></a>ApplicationName

因為設定檔提供者會分別針對每個應用程式儲存設定檔資訊，所以您必須確定您的資料結構描述包含應用程式名稱，而且查詢和更新也包含應用程式名稱。 例如，下列命令可用來根據使用者名稱和設定檔是否為匿名，從資料庫中抓取屬性值，並確保**ApplicationName**值包含在查詢中。

[!code-sql[Main](profiles-themes-and-web-parts/samples/sample10.sql)]

## <a name="aspnet-themes"></a>ASP.NET 主題

## <a name="what-are-aspnet-20-themes"></a>什麼是 ASP.NET 2.0 主題？

Web 應用程式最重要的層面之一，是網站上一致的外觀與風格。 ASP.NET 1.x 開發人員通常會使用階層式樣式表（CSS）來執行一致的外觀與風格。 ASP.NET 2.0 主題會在 CSS 上大幅改善，因為它們可讓 ASP.NET 開發人員定義 ASP.NET 伺服器控制項的外觀，以及 HTML 元素。 ASP.NET 主題可以套用至個別控制項、特定網頁，或整個 Web 應用程式。 主題使用 CSS 檔案的組合、選擇性的外觀檔，以及如果需要影像，則為選擇性的 Images 目錄。 外觀檔案控制 ASP.NET 伺服器控制項的視覺外觀。

## <a name="where-are-themes-stored"></a>主題會儲存在哪裡？

儲存主題的位置會依其範圍而有所不同。 可以套用至任何應用程式的主題會儲存于下列資料夾中：

`C:\WINDOWS\Microsoft.NET\Framework\v2.x.xxxxx\ASP.NETClientFiles\Themes\<Theme_Name>`

特定應用程式的特定主題會儲存在網站根目錄的 `App\_Themes\<Theme\_Name>` 目錄中。

> [!NOTE]
> 面板檔案應該只修改會影響外觀的伺服器控制項屬性。

通用主題是可套用至在網頁伺服器上執行之任何應用程式或網站的主題。 根據預設，這些主題會儲存在位於6.x 目錄內的 NETClientfiles\Themes 目錄中。 或者，您也可以將主題檔案移至網站根目錄中的 aspnet\_client/system\_web/[version]/Themes/[主題\_名稱] 資料夾。

應用程式特定的主題只能套用至檔案所在的應用程式。 這些檔案會儲存在網站根目錄的 `App\_Themes/<theme\_name>` 目錄中。

## <a name="the-components-of-a-theme"></a>主題的元件

主題是由一或多個 CSS 檔案、選擇性的外觀檔案和選擇性的 Images 資料夾所組成。 CSS 檔案可以是任何您想要的名稱（例如，預設 .css 或 .css 等等），而且必須位於 [主題] 資料夾的根目錄中。 CSS 檔案是用來定義特定選取器的一般 CSS 類別和屬性。 若要將其中一個 CSS 類別套用至 page 元素，則會使用**CSSClass**屬性。

此面板檔案是一個 XML 檔案，其中包含 ASP.NET 伺服器控制項的屬性定義。 下面所列的程式碼是範例外觀檔案。

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample11.aspx)]

[**圖 1** ] 顯示在未套用主題的情況下流覽的小型 ASP.NET 網頁。 [**圖 2** ] 顯示已套用主題的相同檔案。 背景色彩和文字色彩是透過 CSS 檔案進行設定。 按鈕和文字方塊的外觀是使用上方所列的面板檔案來設定。

![無主題](profiles-themes-and-web-parts/_static/image1.gif)

**圖 1**：沒有主題

![已套用主題](profiles-themes-and-web-parts/_static/image2.gif)

**圖 2**：已套用主題

上方所列的面板檔案會定義所有 TextBox 控制項和按鈕控制項的預設面板。 這表示每個插入網頁的 TextBox 控制項和按鈕控制項都會採用此外觀。 您也可以使用控制項的**SkinID**屬性，定義可以套用至這些控制項之特定實例的面板。

下列程式碼會定義按鈕控制項的外觀。 只有具有**goButton**的**SkinID**屬性的按鈕控制項，才會採用外觀的外觀。

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample12.aspx)]

每個伺服器控制項類型只能有一個預設面板。 如果您需要其他的面板，您應該使用 SkinID 屬性。

## <a name="applying-themes-to-pages"></a>將主題套用至頁面

您可以使用下列任何一種方法來套用主題：

- 在 web.config 檔案的 &lt;頁面&gt; 元素中
- 在頁面的 @Page 指示詞中
- 以程式設計方式

## <a name="applying-a-theme-in-the-configuration-file"></a>在設定檔中套用主題

若要在應用程式佈建檔中套用主題，請使用下列語法：

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample13.xml)]

此處指定的主題名稱必須符合主題資料夾的名稱。 此資料夾可存在於本課程稍早所述的任何一個位置中。 如果您嘗試套用不存在的主題，將會發生設定錯誤。

## <a name="applying-a-theme-in-the-page-directive"></a>在 Page 指示詞中套用主題

您也可以在 @ Page 指示詞中套用主題。 這個方法可讓您針對特定頁面使用主題。

若要在 @Page 指示詞中套用主題，請使用下列語法：

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample14.aspx)]

同樣地，此處指定的主題必須符合先前所述的主題資料夾。 如果您嘗試套用不存在的主題，將會發生組建失敗。 Visual Studio 也會反白顯示內容，並通知您沒有這類主題存在。

## <a name="applying-a-theme-programmatically"></a>以程式設計方式套用主題

若要以程式設計方式套用主題，您必須在**頁面\_PreInit**方法中指定頁面的 [**主題**] 屬性。

若要以程式設計方式套用主題，請使用下列語法：

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample15.cs)]

由於網頁生命週期的緣故，必須在 PreInit 方法中套用主題。 如果您在該時間點之後套用，頁面主題將已由執行時間套用，而且該點的變更會在生命週期中過晚。 如果您套用的主題不存在，就會發生**HttpException** 。 以程式設計方式套用主題時，如果有任何伺服器控制項已指定 SkinID 屬性，就會發生組建警告。 此警告的目的是通知您未以宣告方式套用任何主題，而且可以忽略它。

## <a name="exercise-1--applying-a-theme"></a>練習1：套用主題

在此練習中，您會將 ASP.NET 主題套用至網站。

> [!IMPORTANT]
> 如果您使用 Microsoft Word 將資訊輸入至面板檔案中，請確定您不會以智慧引號取代一般引號。 智慧引號會造成外觀檔案的問題。

1. 建立新的 ASP.NET 網站。
2. 以滑鼠右鍵按一下方案總管中的專案，然後選擇 [加入新專案]。
3. 從檔案清單中選擇 [Web 設定檔]，然後按一下 [新增]。
4. 以滑鼠右鍵按一下方案總管中的專案，然後選擇 [加入新專案]。
5. 選擇 [面板] [檔案]，然後按一下 [新增]。
6. 詢問您是否要將檔案放在應用程式的\_主題資料夾中時，按一下 [是]。
7. 在方案總管中，以滑鼠右鍵按一下應用程式\_[主題] 資料夾內的 [SkinFile] 資料夾，然後選擇 [加入新專案]。
8. 從檔案清單中選擇 [樣式表單]，然後按一下 [新增]。 您現在已擁有所有必要的檔案，可執行您的新主題。 不過，Visual Studio 已將您的主題資料夾命名為 SkinFile。 以滑鼠右鍵按一下該資料夾，然後將名稱變更為 CoolTheme。
9. 開啟 SkinFile 檔案，並在檔案結尾新增下列程式碼： 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample16.aspx)]
10. 儲存 SkinFile 檔案。
11. 開啟樣式表單 .css。
12. 以下列內容取代其中的所有文字： 

    [!code-css[Main](profiles-themes-and-web-parts/samples/sample17.css)]
13. 儲存樣式表單 .css 檔案。
14. 開啟 default.aspx 頁面。
15. 加入 TextBox 控制項和 Button 控制項。
16. 儲存網頁。 現在，流覽 default.aspx 頁面。 它應該會顯示為一般 Web 表單。
17. 開啟 web.config 檔案。
18. 將下列內容直接加入至開頭 `<system.web>` 標籤底下： 

    [!code-xml[Main](profiles-themes-and-web-parts/samples/sample18.xml)]
19. 儲存 web.config 檔案。 現在，流覽 default.aspx 頁面。 它應該會顯示並套用主題。
20. 如果尚未開啟，請開啟 Visual Studio 中的 default.aspx 頁面。
21. 選取 [] 按鈕。
22. 將 [ **SkinID** ] 屬性變更為 [goButton]。 請注意，Visual Studio 提供一個下拉式清單，其中包含按鈕控制項的有效 SkinID 值。
23. 儲存網頁。 現在，請在瀏覽器中再次預覽頁面。 按鈕現在應該會顯示 "go"，且其外觀應該更寬。

使用**SkinID**屬性，您可以輕鬆地為特定類型的伺服器控制項的不同實例設定不同的外觀。

## <a name="the-stylesheettheme-property"></a>StyleSheetTheme 屬性

到目前為止，我們只討論了如何使用主題屬性來套用主題。 使用 [主題] 屬性時，外觀檔案將會覆寫伺服器控制項的任何宣告式設定。 例如，在練習1中，您為按鈕控制項指定了 "goButton" 的 SkinID，並將按鈕的文字變更為 "go"。 您可能已經注意到設計工具中按鈕的 Text 屬性設定為 "Button"，但主題已覆寫了。 主題一律會覆寫設計工具中的任何屬性設定。

如果您想要能夠使用設計工具中指定的屬性來覆寫主題外觀檔案中所定義的屬性，您可以使用**StyleSheetTheme**屬性，而不是 [主題] 屬性。 [StyleSheetTheme] 屬性與 [主題] 屬性相同，不同之處在于它不會覆寫所有的明確屬性設定，例如 [主題] 屬性。

若要查看其實際運作情況，請從練習1中的專案開啟 web.config 檔案，然後將 `<pages>` 元素變更為下列內容：

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample19.xml)]

現在流覽 default.aspx 頁面，您會看到按鈕控制項再次具有 [按鈕] 的 [Text] 屬性。 這是因為設計工具中的明確屬性設定會覆寫 goButton SkinID 所設定的 Text 屬性。

## <a name="overriding-themes"></a>覆寫主題

藉由在應用程式\_主題 資料夾中的相同名稱套用主題，可以覆寫全域主題。 不過，此主題不適用於真正的覆寫案例。 如果執行時間在應用程式中遇到主題檔案\_主題資料夾，則會使用這些檔案套用主題，並忽略全域主題。

StyleSheetTheme 屬性是可覆寫的，而且可以在程式碼中加以覆寫，如下所示：

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample20.cs)]

## <a name="web-parts"></a>Web 組件

ASP.NET Web 組件是一組整合的控制項，可用於建立網站，讓使用者直接從瀏覽器修改網頁的內容、外觀和行為。 修改可以套用至網站上的所有使用者或個別使用者。 當使用者修改頁面和控制項時，可以儲存設定，以保留使用者在未來瀏覽器會話中的個人喜好，這項功能稱為個人化。 這些 Web 組件的功能意味著開發人員可以讓使用者動態個人化 Web 應用程式，而不需要開發人員或系統管理員介入。

您身為開發人員，可以使用 Web 組件控制組，讓使用者能夠：

- 個人化頁面內容。 使用者可以將新的 Web 組件控制項加入至頁面、將其移除、隱藏它們，或將它們最小化，就像一般視窗一樣。
- 個人化頁面配置。 使用者可以將 Web 組件控制項拖曳至頁面上的不同區域，或變更其外觀、屬性和行為。
- 匯出和匯入控制項。 使用者可以匯入或匯出 Web 組件控制項設定，以用於其他頁面或網站，保留屬性、外觀，甚至是控制項中的資料。 這可減少使用者的資料輸入和設定需求。
- 建立連接。 使用者可以在控制項之間建立連接，例如，chart 控制項可以在股票行情指示器控制項中顯示資料的圖形。 使用者不僅可以個人化連線本身，還可將圖表控制項顯示資料的外觀和詳細資訊。
- 管理及個人化網站層級設定。 授權的使用者可以設定網站層級設定、判斷可以存取網站或頁面的人員、設定控制項的角色型存取等等。 例如，系統管理角色中的使用者可以設定要由所有使用者共用的 Web 組件控制項，並防止非系統管理員的使用者個人化共用控制項。

您通常會使用下列三種方式之一來處理 Web 組件：建立使用 Web 組件控制項的頁面、建立個別的 Web 組件控制項，或建立完整、可個人化的 Web 應用程式（例如入口網站）。

## <a name="page-development"></a>頁面開發

網頁開發人員可以使用視覺化設計工具（例如 Microsoft Visual Studio 2005）來建立使用 Web 組件的頁面。 使用工具（例如 Visual Studio）的其中一項優點是，Web 組件控制項集提供了在視覺化設計工具中建立和設定 Web 組件控制項的功能。 例如，您可以使用設計工具將 [Web 組件] 區域或 [Web 組件編輯器] 控制項拖曳至設計介面上，然後使用 Web 組件控制項集提供的 UI，在設計工具中設定控制許可權。 這可以加速開發 Web 組件應用程式，並減少您必須撰寫的程式碼數量。

## <a name="control-development"></a>控制項開發

您可以使用任何現有的 ASP.NET 控制項做為 Web 組件控制項，包括標準的 Web 服務器控制項、自訂伺服器控制項和使用者控制項。 如需您環境的最大程式設計控制，您也可以建立自訂的 Web 組件控制項，以從 WebPart 類別衍生。 針對個別的 Web 組件控制項開發，您通常會建立一個使用者控制項，並使用它做為 Web 組件控制項，或是開發自訂的 Web 組件控制項。

做為開發自訂 Web 組件控制項的範例，您可以建立一個控制項來提供其他 ASP.NET 伺服器控制項所提供的任何功能，這些都可能有助於封裝為可個人化的 Web 組件控制項：行事曆、清單、財務資訊、新聞、計算機、用於更新內容的 rich text 控制項、連接到資料庫的可編輯格線、動態更新其顯示的圖表，或天氣和旅遊資訊。 如果您使用控制項提供視覺化設計工具，則任何使用 Visual Studio 的網頁開發人員都可以直接將控制項拖曳至 Web 組件區域，並在設計階段進行設定，而不需要撰寫額外的程式碼。

個人化是 Web 組件功能的基礎。 它可讓使用者修改（或個人化）頁面上 Web 組件控制項的版面配置、外觀和行為。 個人化設定是長期的：它們不只是在目前的瀏覽器會話期間（如同檢視狀態）保存，也會在長期儲存中保存，讓使用者的設定也會儲存供未來的瀏覽器會話使用。 預設會為 Web 組件頁面啟用個人化。

UI 結構化元件會依賴個人化，並提供所有 Web 組件控制項所需的核心結構和服務。 每個 Web 組件頁面上所需的一個 UI 結構化元件是 WebPartManager 控制項。 雖然永遠不會顯示，但此控制項具有協調頁面上所有 Web 組件控制項的關鍵工作。 例如，它會追蹤所有的個別 Web 組件控制項。 它會管理 Web 組件區域（包含頁面上 Web 組件控制項的區域），以及哪些控制項在哪些區域中。 它也會追蹤並控制頁面可以位於不同的顯示模式，例如 [流覽]、[連接]、[編輯] 或 [目錄] 模式，以及個人化變更適用于所有使用者或個別使用者。 最後，它會起始和追蹤 Web 組件控制項之間的連接和通訊。

第二種 UI 結構化元件是區域。 區域做為 Web 組件頁面上的版面建構管理員。 它們包含和組織衍生自元件類別（元件控制項）的控制項，並提供以水準或垂直方向進行模組化頁面配置的功能。 區域也會針對所包含的每個控制項，提供通用且一致的 UI 元素（例如頁首和頁尾樣式、標題、框線樣式、動作按鈕等等）;這些常見的元素稱為控制項的 chrome。 在不同的顯示模式和各種控制項中，會使用數種特殊類型的區域。 下面的 Web 組件基本控制一節說明不同類型的區域。

Web 組件的 UI 控制項，全都衍生自**元件**類別，其中包含 Web 組件頁面上的主要 UI。 Web 組件控制集具有彈性，而且包含在提供您建立元件控制項的選項中。 除了建立您自己的自訂 Web 組件控制項之外，您還可以使用現有的 ASP.NET 伺服器控制項、使用者控制項或自訂伺服器控制項做為 Web 組件控制項。 下一節將描述最常用來建立 Web 組件頁面的基本控制項。

## <a name="web-parts-essential-controls"></a>Web 組件基本控制項

Web 組件的控制項集很廣泛，但有些控制項是不可或缺的，因為它們是 Web 組件正常工作的必要項，或因為它們是最常用於 Web 組件頁面的控制項。 當您開始使用 Web 組件並建立基本 Web 組件頁面時，熟悉下表所述的基本 Web 組件控制項會很有説明。

| **Web 組件控制項** | **說明** |
| --- | --- |
| WebPartManager | 管理頁面上的所有 Web 組件控制項。 每個 Web 組件頁面都需要一個（且只有一個） **WebPartManager**控制項。 |
| CatalogZone | 包含 CatalogPart 控制項。 使用此區域來建立 Web 組件控制項的目錄，使用者可以從中選取要加入至頁面的控制項。 |
| EditorZone | 包含 EditorPart 控制項。 使用此區域可讓使用者編輯頁面上的 Web 組件控制項並個人化。 |
| WebPartZone | 包含，並提供構成頁面主要 UI 之 WebPart 控制項的整體版面配置。 每當您建立具有 Web 組件控制項的頁面時，請使用此區域。 頁面可以包含一或多個區域。 |
| ConnectionsZone | 包含 WebPartConnection 控制項，並提供用來管理連接的 UI。 |
| WebPart （GenericWebPart） | 呈現主要 UI;大部分的 Web 組件 UI 控制項都屬於此分類。 如需最大的程式設計控制項，您可以建立衍生自基底**WebPart**控制項的自訂 Web 組件控制項。 您也可以使用現有的伺服器控制項、使用者控制項或自訂控制項做為 Web 組件控制項。 只要這些控制項放在區域中， **WebPartManager**控制項就會在執行時間自動將它們包裝在**GenericWebPart**控制項中，讓您可以將它們與 Web 組件功能搭配使用。 |
| CatalogPart | 包含使用者可以加入至頁面的可用 Web 組件控制項清單。 |
| WebPartConnection | 在頁面上的兩個 Web 組件控制項之間建立連接。 連接會將其中一個 Web 組件控制項定義為提供者（資料），而另一個做為取用者。 |
| EditorPart | 作為特製化編輯器控制項的基類。 |
| EditorPart 控制項（AppearanceEditorPart、LayoutEditorPart、BehaviorEditorPart 和 PropertyGridEditorPart） | 允許使用者在頁面上個人化 Web 組件 UI 控制項的各個層面 |

## <a name="lab-create-a-web-part-page"></a>實驗室：建立 Web 元件頁面

在此實驗室中，您將建立會透過 ASP.NET 設定檔保存資訊的網頁元件頁面。

### <a name="creating-a-simple-page-with-web-parts"></a>建立具有 Web 組件的簡單頁面

在逐步解說的這個部分中，您會建立使用 Web 組件控制項來顯示靜態內容的頁面。 使用 Web 組件的第一個步驟是建立包含兩個必要結構元素的頁面。 首先，Web 元件頁面需要一個 WebPartManager 控制項來追蹤和協調所有的 Web 組件控制項。 第二，Web 組件頁需要一或多個區域，這些區域是包含 WebPart 或其他伺服器控制項並佔用頁面指定區域的複合控制項。

> [!NOTE]
> 您不需要執行任何動作來啟用 Web 組件個人化;預設會針對 [Web 組件] 控制項集啟用此功能。 當您第一次在網站上執行 Web 組件頁面時，ASP.NET 會設定預設個人化提供者來儲存使用者個人化設定。 如需個人化的詳細資訊，請參閱 Web 組件個人化總覽。

### <a name="to-create-a-page-for-containing-web-parts-controls"></a>若要建立包含 Web 組件控制項的頁面

1. 關閉預設頁面，並將新頁面新增至名為 WebPartsDemo 的網站。
2. 切換至**設計**視圖。
3. 在 [ **View** ] 功能表中，確定已選取 [**非視覺效果控制項**] 和 [**詳細資料**] 選項，讓您可以看到不具有 UI 的版面配置標記和控制項。
4. 將插入點放在設計介面上的 `<div>` 標記之前，然後按 ENTER 以加入新的行。 將插入點放在新行字元之前，按一下功能表上的 [**封鎖格式**] 下拉式清單控制項，然後選取 [**標題 1** ] 選項。 在標題中，將 [文字] **Web 組件 [示範] 頁面**。
5. 從 [工具箱] 的 [ **webpart** ] 索引標籤中，將 [ **WebPartManager** ] 控制項拖曳至頁面上，將它放在新行字元後面，然後在 `<div>`標記之前。   
  
   **WebPartManager**控制項不會轉譯任何輸出，因此它會在設計工具介面上顯示為灰色方塊。
6. 將插入點放在 `<div>` 標記內。
7. 在 [**版面**配置] 功能表中，按一下 [**插入資料表**]，然後建立有一個資料列和三個數據行的新資料表。 按一下 [資料**格屬性**] 按鈕，從 [**垂直對齊**] 下拉式清單中選取 [**上**一步]，按一下 **[確定]** ，然後再按一下 **[確定]** 以建立資料表。
8. 將 [WebPartZone] 控制項拖曳至 [左資料表] 資料行。 以滑鼠右鍵按一下 [ **WebPartZone** ] 控制項，選擇 [**屬性**]，然後設定下列屬性：   
  
   識別碼： SidebarZone   
  
   HeaderText：提要欄位
9. 將第二個 [ **WebPartZone** ] 控制項拖曳至 [中間資料表] 資料行，並設定下列屬性：   
  
   識別碼： MainZone   
  
   HeaderText： Main
10. 儲存檔案。

您的頁面現在有兩個不同的區域，您可以分別進行控制。 不過，這兩個區域都沒有任何內容，因此下一個步驟是建立內容。 在此逐步解說中，您會使用只顯示靜態內容 Web 組件控制項。

Web 組件區域的配置是由 &lt;zonetemplate&gt; 元素所指定。 在區域範本內，您可以加入任何 ASP.NET 控制項，不論它是自訂的 Web 組件控制項、使用者控制項或現有的伺服器控制項。 請注意，這裡您使用的是標籤控制項，而您只是加入靜態文字。 當您將一般伺服器控制項放在**WebPartZone**區域時，ASP.NET 會在執行時間將控制項視為 Web 組件控制項，這會在控制項上啟用 Web 組件功能。

**建立主要區域的內容**

1. 在**設計**視圖中，從 [工具箱] 的 [**標準**] 索引**標籤**將 [Label] 控制項拖曳至 [**識別碼**] 屬性設為 [MainZone] 之區域的 [內容] 區域中。
2. 切換至**來源**視圖。 請注意，已新增 &lt;zonetemplate&gt; 元素，以包裝 MainZone 中的**標籤**控制項。
3. 將名為**title**的屬性新增至 &lt;asp： label&gt; 元素，並將其值設定為 Content。 從 &lt;asp： label&gt; 元素中移除 Text = "Label" 屬性。 在 &lt;asp： label&gt; 元素的開頭和結束記號之間，新增一些文字，例如 [**歡迎使用我**的首頁]，在一對 &lt;h2&gt; 元素標記中。 您的程式碼看起來應該如下所示。 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample21.aspx)]
4. 儲存檔案。

接下來，建立一個使用者控制項，它也可以當做 Web 組件控制項加入至頁面。

### <a name="to-create-a-user-control"></a>建立使用者控制項

1. 將新的 Web 使用者控制項加入至您的網站，以作為搜尋控制項。 取消選取此選項，將**原始程式碼放在不同**的檔案中。 將它新增到與 WebPartsDemo 相同的目錄中，並將它命名為 SearchUserControl。   
  
    > [!NOTE]
    > 此逐步解說的使用者控制項不會執行實際的搜尋功能;它只能用來示範 Web 組件功能。
2. 切換至**設計**視圖。 從 [工具箱] 的 [**標準**] 索引標籤，將 TextBox 控制項拖曳至頁面上。
3. 將插入點放在您剛才加入的文字方塊之後，然後按下 ENTER 以加入新的行。
4. 將 [按鈕] 控制項拖曳至您剛才加入之文字方塊下方的新行上的頁面。
5. 切換至**來源**視圖。 請確定使用者控制項的原始程式碼看起來如下列範例所示。 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample22.aspx)]
6. 儲存並關閉檔案。

現在您可以將 Web 組件控制項加入至邊欄區域。 您要將兩個控制項加入至提要欄位，一個包含連結的清單，另一個則是您在上一個程式中建立的使用者控制項。 連結會新增為標準**標籤**伺服器控制項，類似于您為主要區域建立靜態文字的方式。 不過，雖然使用者控制項中包含的個別伺服器控制項可以直接包含在區域中（例如標籤控制項），但在此情況下，它們並不是。 相反地，它們是您在上一個程式中建立的使用者控制項的一部分。 這會示範在使用者控制項中封裝您想要的任何控制項和額外功能的常見方式，然後在區域中將該控制項當做 Web 組件控制項來參考。

在執行時間，Web 組件控制項集會使用 GenericWebPart 控制項來包裝這兩個控制項。 當**GenericWebPart**控制項包裝 Web 服務器控制項時，泛型元件控制項是父控制項，而您可以透過父控制項的 ChildControl 屬性來存取伺服器控制項。 使用泛型元件控制項可讓標準 Web 服務器控制項具有與衍生自**WebPart**類別 Web 組件控制項相同的基本行為和屬性。

### <a name="to-add-web-parts-controls-to-the-sidebar-zone"></a>將 Web 組件控制項新增至提要欄位區域

1. 開啟 [WebPartsDemo] 頁面。
2. 切換至**設計**視圖。
3. 將您建立的 [使用者控制項] 頁面從**方案總管**拖曳至 [**識別碼**] 屬性設為 [SidebarZone] 的區域，然後將它拖放到該處。
4. 儲存 WebPartsDemo .aspx 頁面。
5. 切換至**來源**視圖。
6. 在適用于 SidebarZone 的 &lt;asp： webpartzone&gt; 元素中，在使用者控制項的參考正上方，新增 &lt;asp： label&gt; 專案與包含的連結，如下列範例所示。 此外，使用 [**搜尋**] 的值，將 [**標題**] 屬性新增至 [使用者] 控制項標記，如下所示。 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample23.aspx)]
7. 儲存並關閉檔案。

現在您可以在瀏覽器中流覽以測試您的頁面。 此頁面會顯示兩個區域。 下列螢幕擷取畫面顯示頁面。

**具有兩個區域的 Web 組件示範頁面**

![Web 組件 VS 逐步解說1螢幕擷取畫面](profiles-themes-and-web-parts/_static/image3.gif)

**圖 3**： Web 組件 VS 逐步解說1螢幕擷取畫面

在每個控制項的標題列中，會有向下箭號，可讓您存取可以在控制項上執行之動作的動詞功能表。 按一下其中一個控制項的 [動詞] 功能表，然後按一下 [**最小化**] 動詞，並注意控制項已最小化。 從 [動詞] 功能表中，按一下 [**還原**]，控制項會回到其一般大小。

### <a name="enabling-users-to-edit-pages-and-change-layout"></a>讓使用者可以編輯頁面和變更版面配置

Web 組件提供功能，讓使用者將 Web 組件控制項的配置從一個區域拖曳到另一個區域，以變更其版面配置。 除了允許使用者將**WebPart**控制項從一個區域移至另一個區域之外，您還可以讓使用者編輯控制項的各種特性，包括其外觀、版面配置和行為。 Web 組件控制項集提供了**WebPart**控制項的基本編輯功能。 雖然您在此逐步解說中不會這麼做，但您也可以建立自訂編輯器控制項，讓使用者編輯**WebPart**控制項的功能。 就像變更**WebPart**控制項的位置一樣，編輯控制項的屬性會依賴 ASP.NET 個人化，以儲存使用者所做的變更。

在本逐步解說的這個部分中，您可以新增使用者編輯頁面上任何**WebPart**控制項之基本特性的功能。 若要啟用這些功能，您可以將另一個自訂使用者控制項加入至頁面，以及 &lt;asp： editorzone&gt; 元素和兩個編輯控制項。

### <a name="to-create-a-user-control-that-enables-changing-page-layout"></a>若要建立可讓您變更頁面配置的使用者控制項

1. 在 Visual Studio 的 [檔案 **] 功能表上，選取 [** **新增**] 子功能表，然後按一下 [檔案 **] 選項。**
2. 在 [**加入新專案**] 對話方塊中，選取 [ **Web 使用者控制項**]。 將新檔案命名為 DisplayModeMenu。 取消選取 [**將原始程式碼放在不同**的檔案中] 選項。
3. 按一下 [新增] 以建立新的控制項。
4. 切換至**來源**視圖。
5. 移除新檔案中的所有現有程式碼，並貼上下列程式碼。 這個使用者控制項程式碼會使用 Web 組件控制項集的功能，讓頁面變更其視圖或顯示模式，同時也可讓您在特定顯示模式中變更頁面的實體外觀和版面配置。 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample24.aspx)]
6. 按一下工具列上的 [儲存] 圖示，或選取 [檔案 **] 功能表上的 [** **儲存**]，以儲存檔案。

### <a name="to-enable-users-to-change-the-layout"></a>若要讓使用者變更版面配置

1. 開啟 [WebPartsDemo] 頁面，然後切換至 [**設計**視圖]。
2. 在**設計**視圖中，將插入點放在您稍早新增的**WebPartManager**控制項之後。 在文字後面加入強制換行，讓**WebPartManager**控制項之後有一個空白行。 將插入點放置在空白行上。
3. 將您剛才建立的使用者控制項（名為 DisplayModeMenu 的檔案）拖曳至 [WebPartsDemo] 頁面，並將它放在空白行。
4. 從 [工具箱] 的 [ **webpart** ] 區段，將 [EditorZone] 控制項拖曳至 [WebPartsDemo] 頁面中的 [其他開啟的資料表] 資料格。
5. 從 [工具箱] 的 [ **webpart** ] 區段中，將 AppearanceEditorPart 控制項和 LayoutEditorPart 控制項拖曳至**EditorZone**控制項。
6. 切換至**來源**視圖。 資料表單元格中產生的程式碼看起來應該類似下列程式碼。 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample25.aspx)]
7. 儲存 WebPartsDemo .aspx 檔案。 您已建立可讓您變更顯示模式和變更頁面配置的使用者控制項，而且您已在主要網頁上參考該控制項。

您現在可以測試編輯頁面和變更版面配置的功能。

### <a name="to-test-layout-changes"></a>測試版面配置變更

1. 在瀏覽器中載入頁面。
2. 按一下 [**顯示模式]** 下拉式功能表，然後選取 [**編輯**]。 區域標題隨即顯示。
3. 將 [**我的連結**] 控制項從提要欄位的標題列拖曳到主要區域底部。 您的頁面看起來應該如下列螢幕擷取畫面所示。

### <a name="web-parts-demo-page-with-my-links-control-moved"></a>已移動 [我的連結] 控制項的 Web 組件示範頁面

![Web 組件 VS 逐步解說2螢幕擷取畫面](profiles-themes-and-web-parts/_static/image4.gif)

**圖 4**： Web 組件 VS 逐步解說2螢幕擷取畫面

1. 按一下 [**顯示模式**] 下拉式功能表，然後選取 **[流覽]** 。 頁面會重新整理，區功能變數名稱稱會消失，而 [**我的連結**] 控制項則保留在您放置它的位置。
2. 若要示範個人化的運作情況，請關閉瀏覽器，然後再次載入頁面。 您所做的變更會儲存在未來的瀏覽器會話中。
3. 從 [**顯示模式]** 功能表中，選取 [**編輯**]。   
  
   頁面上的每個控制項現在都會在其標題列中顯示向下箭號，其中包含 [動詞] 下拉式功能表。
4. 按一下箭號，即可在 [**我的連結**] 控制項上顯示動詞功能表。 按一下 [**編輯**] 動詞。   
  
   **EditorZone**控制項會隨即出現，並顯示您所新增的 EditorPart 控制項。
5. 在編輯控制項的 [**外觀**] 區段中，將 **[標題**] 變更為 [我的最愛]，使用 [ **Chrome 類型**] 下拉式清單選取 [**僅限標題**]，**然後按一下 [** 套用]。 下列螢幕擷取畫面顯示 [編輯] 模式中的頁面。

### <a name="web-parts-demo-page-in-edit-mode"></a>編輯模式中的 Web 組件示範頁面

![Web 組件 VS 逐步解說3螢幕擷取畫面](profiles-themes-and-web-parts/_static/image5.gif)

**圖 5**： Web 組件 VS 逐步解說3螢幕擷取畫面

1. 按一下 [**顯示模式**] 功能表，然後選取 **[流覽]** 以返回瀏覽模式。
2. 控制項現在具有更新的標題，而且沒有框線，如下列螢幕擷取畫面所示。

### <a name="edited-web-parts-demo-page"></a>已編輯 Web 組件示範頁面

![Web 組件 VS 逐步解說4螢幕擷取畫面](profiles-themes-and-web-parts/_static/image6.gif)

**圖 4**： Web 組件 VS 逐步解說4螢幕擷取畫面

### <a name="adding-web-parts-at-run-time"></a>在執行時間加入 Web 組件

您也可以讓使用者在執行時間，將 Web 組件控制項加入至其頁面。 若要這麼做，請使用 Web 組件目錄來設定頁面，其中包含您想要提供給使用者的 Web 組件控制項清單。

**允許使用者在執行時間加入 Web 組件**

1. 開啟 [WebPartsDemo] 頁面，然後切換至 [**設計**視圖]。
2. 從 [工具箱] 的 [ **webpart** ] 索引標籤中，將 [CatalogZone] 控制項拖曳至資料表的右欄中， **EditorZone**控制項下方。   
  
   這兩個控制項都可以位於相同的資料表資料格中，因為它們不會同時顯示。
3. 在 [屬性] 窗格中，將字串**Add Web 組件**指派給**CatalogZone**控制項的 HeaderText 屬性。
4. 從 [工具箱] 的 [ **webpart** ] 區段中，將 [DeclarativeCatalogPart] 控制項拖曳至 [ **CatalogZone** ] 控制項的 [內容] 區域中。
5. 按一下**DeclarativeCatalogPart**控制項右上角的箭號，以公開其 [工作] 功能表，然後選取 [**編輯範本**]。
6. 從 [工具箱] 的 [**標準**] 區段中，將 [ **FileUpload** ] 控制項和 [行事**曆**] 控制項拖曳至**DeclarativeCatalogPart**控制項的 [ **WebPartsTemplate** ] 區段中。
7. 切換至**來源**視圖。 檢查 &lt;asp： catalogzone&gt; 元素的原始程式碼。 請注意， **DeclarativeCatalogPart**控制項包含一個 &lt;webpartstemplate&gt; 元素，其中含有兩個括住的伺服器控制項，您可以從目錄新增至您的頁面。
8. 使用下列程式碼範例中每個標題所顯示的字串值，將**Title**屬性新增至您新增至目錄的每個控制項。 雖然標題不是您通常可以在設計階段于這兩個伺服器控制項上設定的屬性，但當使用者將這些控制項從類別目錄中的**WebPartZone**區域加入至執行時間時，就會以**GenericWebPart**控制項來包裝它們。 這可讓它們作為 Web 組件控制項，讓他們能夠顯示標題。   
  
   **DeclarativeCatalogPart**控制項中包含的兩個控制項的程式碼看起來應該如下所示。 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample26.aspx)]
9. 儲存網頁。

您現在可以測試目錄。

### <a name="to-test-the-web-parts-catalog"></a>測試 Web 組件目錄

1. 在瀏覽器中載入頁面。
2. 按一下 [**顯示模式]** 下拉式功能表，然後選取 [**目錄**]。   
  
   隨即顯示標題為 [**新增 Web 組件**] 的目錄。
3. 將 [**我**的最愛] 控制項從主要區域拖曳回提要欄位區域的頂端，然後將它拖放到該處。
4. 在 [**新增 Web 組件**目錄] 中，選取這兩個核取方塊，然後從包含可用區域的下拉式清單中選取 [ **Main** ]。
5. 按一下目錄中的 [**新增**]。 控制項會新增至主要區域。 如果您想要的話，可以將類別目錄中的多個控制項實例新增至您的頁面。   
  
   下列螢幕擷取畫面顯示具有 [檔案上傳] 控制項的頁面，以及主要區域中的行事曆。 

![從目錄新增至主要區域的控制項](profiles-themes-and-web-parts/_static/image7.gif)

    **Figure 5**: Controls added to Main zone from the catalog
6. 按一下 [**顯示模式**] 下拉式功能表，然後選取 **[流覽]** 。 類別目錄會消失，並重新整理頁面。
7. 關閉瀏覽器。 再次載入頁面。 您所做的變更會保存下來。
