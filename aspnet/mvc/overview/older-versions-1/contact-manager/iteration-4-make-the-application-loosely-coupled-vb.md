---
uid: mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-vb
title: '反復專案 #4 –讓應用程式鬆散結合（VB） |Microsoft Docs'
author: microsoft
description: 在這第四次的反復專案中，我們會利用數種軟體設計模式，讓您更輕鬆地維護和修改 Contact Manager 應用程式。 如需...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 92c70297-4430-4e4e-919a-9c2333a8d09a
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-vb
msc.type: authoredcontent
ms.openlocfilehash: 422c75406d9c08279d0c2224ee4b6db3a71eb1b3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582079"
---
# <a name="iteration-4--make-the-application-loosely-coupled-vb"></a>反復專案 #4 –讓應用程式鬆散結合（VB）

由[Microsoft](https://github.com/microsoft)

[下載程式代碼](iteration-4-make-the-application-loosely-coupled-vb/_static/contactmanager_4_vb1.zip)

> 在這第四次的反復專案中，我們會利用數種軟體設計模式，讓您更輕鬆地維護和修改 Contact Manager 應用程式。 例如，我們會重構應用程式，以使用存放庫模式和相依性插入模式。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>建立連絡人管理 ASP.NET MVC 應用程式（VB）

在這一系列的教學課程中，我們從一開始就建立了整個連絡人管理應用程式。 連絡人管理員應用程式可讓您儲存連絡人資訊名稱、電話號碼和電子郵件地址，以取得人員清單。

我們會透過多個反復專案來建立應用程式。 在每次反覆運算時，我們會逐漸改善應用程式。 這個多個反復專案方法的目標，是要讓您瞭解每項變更的原因。

- 反復專案 #1-建立應用程式。 在第一個反復專案中，我們會以最簡單的方式建立連絡人管理員。 我們新增對基本資料庫作業的支援：建立、讀取、更新和刪除（CRUD）。

- 反復專案 #2-讓應用程式看起來不錯。 在此反復專案中，我們藉由修改預設的 ASP.NET MVC view 主版頁面和級聯樣式表，來改善應用程式的外觀。

- 反復專案 #3-新增表單驗證。 在第三個反復專案中，我們會新增基本表單驗證。 我們會防止人們提交表單，而不需要完成必要的表單欄位。 我們也會驗證電子郵件地址和電話號碼。

- 反復專案 #4-讓應用程式鬆散結合。 在這第四次的反復專案中，我們會利用數種軟體設計模式，讓您更輕鬆地維護和修改 Contact Manager 應用程式。 例如，我們會重構應用程式，以使用存放庫模式和相依性插入模式。

- 反復專案 #5-建立單元測試。 在第五個反復專案中，我們會藉由新增單元測試，讓應用程式更容易維護和修改。 我們會模擬我們的資料模型類別，並為我們的控制器和驗證邏輯建立單元測試。

- 反復專案 #6-使用以測試為導向的開發。 在此第六個反復專案中，我們會先撰寫單元測試，並針對單元測試撰寫程式碼，以將新功能加入至應用程式。 在此反復專案中，我們會新增連絡人群組。

- 反復專案 #7-新增 Ajax 功能。 在第七次的反復專案中，我們藉由新增 Ajax 的支援來改善應用程式的回應性和效能。

## <a name="this-iteration"></a>這個反復專案

在 Contact Manager 應用程式的第四個反復專案中，我們會重構應用程式，讓應用程式更鬆散結合。 當應用程式鬆散結合時，您可以在應用程式的某個部分修改程式碼，而不需要修改應用程式的其他部分中的程式碼。 鬆散結合的應用程式會更有彈性地進行變更。

目前，Contact Manager 應用程式所使用的所有資料存取和驗證邏輯都包含在控制器類別中。 這是個不錯的想法。 每當您需要修改應用程式的某個部分時，就會有風險，將 bug 引入應用程式的另一個部分。 例如，如果您修改驗證邏輯，您會面臨將新 bug 引入資料存取或控制器邏輯的風險。

> [!NOTE] 
> 
> （SRP），類別應該永遠不會有一個以上的原因要變更。 混合控制器、驗證和資料庫邏輯會違反單一責任原則。

您可能需要修改應用程式的原因有好幾個。 您可能需要在應用程式中加入新功能，您可能需要修正應用程式中的 bug，或者您可能需要修改應用程式的功能的執行方式。 應用程式很少是靜態的。 它們傾向于一段時間的成長和變動。

例如，假設您決定要變更如何執行資料存取層。 現在，Contact Manager 應用程式會使用 Microsoft Entity Framework 來存取資料庫。 不過，您可能會決定遷移至新的或替代的資料存取技術，例如 ADO.NET 資料服務或 NHibernate。 不過，因為資料存取程式碼不會與驗證和控制器程式碼隔離，所以沒有任何方法可以修改您應用程式中的資料存取碼，而不需要修改與資料存取無關的其他程式碼。

另一方面，當應用程式鬆散結合時，您可以對應用程式的某個部分進行變更，而不需要觸及應用程式的其他部分。 例如，您可以在不修改驗證或控制器邏輯的情況下切換資料存取技術。

在此反復專案中，我們會利用數種軟體設計模式，讓我們將連絡人管理員應用程式重構為更鬆散結合的應用程式。 完成後，「連絡人管理員」就會執行任何未執行的作業。 不過，我們將能夠更輕鬆地在未來變更應用程式。

> [!NOTE] 
> 
> 重構是以不會遺失任何現有功能的方式重寫應用程式的過程。

## <a name="using-the-repository-software-design-pattern"></a>使用存放庫軟體設計模式

我們的第一項變更是利用稱為「存放庫」模式的軟體設計模式。 我們會使用存放庫模式，將我們的資料存取程式碼與我們的其餘部分進行隔離。

執行存放庫模式需要我們完成下列兩個步驟：

1. 建立介面
2. 建立可實作為介面的實體類別

首先，我們需要建立一個介面來描述我們需要執行的所有資料存取方法。 IContactManagerRepository 介面包含在 [清單 1] 中。 此介面描述五種方法： CreateContact （）、DeleteContact （）、EditContact （）、GetContact 和 ListContacts （）。

**清單 1-Models\IContactManagerRepository.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample1.vb)]

接下來，我們需要建立可實 IContactManagerRepository 介面的實體類別。 因為我們使用 Microsoft Entity Framework 來存取資料庫，所以我們將建立名為 EntityContactManagerRepository 的新類別。 此類別包含在 [清單 2] 中。

**清單 2-Models\EntityContactManagerRepository.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample2.vb)]

請注意，EntityContactManagerRepository 類別會實作為 IContactManagerRepository 介面。 類別會執行該介面所描述的全部五個方法。

您可能會想知道為什麼我們需要使用介面。 為什麼需要同時建立介面和執行它的類別？

有一個例外狀況，我們的應用程式的其餘部分將與介面互動，而不是實體類別。 我們不會呼叫由 EntityContactManagerRepository 類別公開的方法，而是會呼叫 IContactManagerRepository 介面所公開的方法。

如此一來，我們就可以使用新的類別來執行介面，而不需要修改應用程式的其餘部分。 例如，在未來的日期，我們可能會想要實 DataServicesContactManagerRepository 類別來執行 IContactManagerRepository 介面。 DataServicesContactManagerRepository 類別可能會使用 ADO.NET 資料服務來存取資料庫，而不是 Microsoft Entity Framework。

如果我們的應用程式程式碼是以 IContactManagerRepository 介面（而不是具體的 EntityContactManagerRepository 類別）進行設計，則我們可以切換具象類別，而不需要修改程式碼的任何其他部分。 例如，我們可以從 EntityContactManagerRepository 類別切換至 DataServicesContactManagerRepository 類別，而不需要修改我們的資料存取或驗證邏輯。

對介面（抽象）進行程式設計，而不是具象類別，讓我們的應用程式更有彈性地進行變更

> [!NOTE] 
> 
> 您可以藉由選取 [重構、解壓縮介面] 功能表選項，從 Visual Studio 內的實體類別快速建立介面。 例如，您可以先建立 EntityContactManagerRepository 類別，然後使用 [解壓縮介面] 自動產生 IContactManagerRepository 介面。

## <a name="using-the-dependency-injection-software-design-pattern"></a>使用相依性插入軟體設計模式

既然我們已將資料存取程式碼遷移至個別的儲存機制類別，我們需要修改連絡人控制器以使用此類別。 我們將利用稱為相依性插入的軟體設計模式，在我們的控制器中使用存放庫類別。

已修改的連絡人控制器包含在 [清單 3] 中。

**清單 3-Controllers\ContactController.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample3.vb)]

請注意，[清單 3] 中的連絡人控制器有兩個「函式」。 第一個函式會將 IContactManagerRepository 介面的實體實例傳遞給第二個函式。 Contact controller 類別使用的是函數相依性*插入*。

使用 EntityContactManagerRepository 類別的唯一位置就是第一個函式。 類別的其餘部分會使用 IContactManagerRepository 介面，而不是具體的 EntityContactManagerRepository 類別。

這可讓您輕鬆地在未來切換 IContactManagerRepository 類別的實作為。 如果您想要使用 DataServicesContactRepository 類別，而不是 EntityContactManagerRepository 類別，只要修改第一個函式即可。

「函式相依性插入」也會使「連絡人控制器」類別非常容易測試。 在單元測試中，您可以藉由傳遞 IContactManagerRepository 類別的 mock 實作為來具現化 Contact 控制器。 當我們為 Contact Manager 應用程式建立單元測試時，在下一個反復專案中，這項相依性插入的功能將非常重要。

> [!NOTE] 
> 
> 如果您想要完全分離 Contact controller 類別與 IContactManagerRepository 介面的特定執行，則可以利用支援相依性插入的架構，例如 StructureMap 或 MicrosoftEntity Framework （MEF）。 藉由利用相依性插入架構，您就不需要在程式碼中參考具體的類別。

## <a name="creating-a-service-layer"></a>建立服務層級

您可能已經注意到，我們的驗證邏輯仍然與 [清單 3] 中修改過的控制器類別中的控制器邏輯混合在一起。 基於相同的理由，若要隔離我們的資料存取邏輯，最好先找出我們的驗證邏輯。

若要修正此問題，我們可以建立不同的[服務層](http://martinfowler.com/eaaCatalog/serviceLayer.html)級。 服務層是可在控制器和存放庫類別之間插入的個別圖層。 服務層包含我們的商務邏輯，包括所有的驗證邏輯。

ContactManagerService 包含在 [清單 4] 中。 它包含來自 Contact controller 類別的驗證邏輯。

**清單 4-Models\ContactManagerService.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample4.vb)]

請注意，ContactManagerService 的構造函式需要 ValidationDictionary。 服務層會透過此 ValidationDictionary 與控制器層通訊。 當我們討論裝飾專案模式時，我們會在下一節中詳細討論 ValidationDictionary。

此外，請注意，ContactManagerService 會執行 IContactManagerService 介面。 您應該一律致力於針對介面（而非具體類別）進行程式設計。 連絡人管理員應用程式中的其他類別不會直接與 ContactManagerService 類別互動。 相反地，有一個例外狀況，Contact Manager 應用程式的其餘部分會針對 IContactManagerService 介面進行程式設計。

IContactManagerService 介面包含在 [清單 5] 中。

**清單 5-Models\IContactManagerService.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample5.vb)]

已修改的連絡人控制器類別包含在 [清單 6] 中。 請注意，Contact controller 不會再與 ContactManager 存放庫互動。 相反地，Contact 控制器會與 ContactManager 服務互動。 每個圖層會盡可能地與其他層隔離。

**清單 6-Controllers\ContactController.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample6.vb)]

我們的應用程式不再執行單一責任原則（SRP）的 afoul。 清單6中的連絡人控制器已移除每個責任，而不是控制應用程式執行的流程。 所有驗證邏輯都已從連絡人控制器移除，並推送至服務層。 所有的資料庫邏輯都已推送至儲存機制層。

## <a name="using-the-decorator-pattern"></a>使用裝飾專案模式

我們想要能夠完全將我們的服務層與控制器層分離。 就原則而言，我們應該能夠在控制器層的不同元件中編譯我們的服務層，而不需要新增對 MVC 應用程式的參考。

不過，我們的服務層必須能夠將驗證錯誤訊息傳回控制器層。 如何讓服務層能夠傳達驗證錯誤訊息，而不需要結合控制器和服務層級？ 我們可以利用名為裝飾項[模式](http://en.wikipedia.org/wiki/Decorator_pattern)的軟體設計模式。

控制器會使用名為 ModelState 的 ModelStateDictionary 來表示驗證錯誤。 因此，您可能會想要將 ModelState 從控制器層傳遞至服務層。 不過，在服務層中使用 ModelState 會讓您的服務層相依于 ASP.NET MVC 架構的功能。 這會是錯誤的，因為在未來，您可能會想要將服務層與 WPF 應用程式搭配使用，而不是 ASP.NET MVC 應用程式。 在這種情況下，您不想要參考 ASP.NET MVC 架構來使用 ModelStateDictionary 類別。

裝飾專案模式可讓您在新的類別中包裝現有的類別，以便執行介面。 我們的 Contact Manager 專案包含 [清單 7] 中所包含的 ModelStateWrapper 類別。 ModelStateWrapper 類別會執行 [清單 8] 中的介面。

**清單 7-Models\Validation\ModelStateWrapper.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample7.vb)]

**清單 8-Models\Validation\IValidationDictionary.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample8.vb)]

如果您仔細查看清單5，則會看到 ContactManager 服務層以獨佔方式使用 IValidationDictionary 介面。 ContactManager 服務不相依于 ModelStateDictionary 類別。 當 Contact controller 建立 ContactManager 服務時，控制器會包裝其 ModelState，如下所示：

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample9.vb)]

## <a name="summary"></a>總結

在此反復專案中，我們不會將任何新的功能加入至 Contact Manager 應用程式。 這項反復專案的目標是要重構 Contact Manager 應用程式，以便更容易維護和修改。

首先，我們實行了存放庫軟體設計模式。 我們已將所有資料存取程式碼遷移至個別的 ContactManager 存放庫類別。

我們也會將我們的驗證邏輯與我們的控制器邏輯隔離。 我們建立了個別的服務層，其中包含我們所有的驗證程式代碼。 控制器層會與服務層互動，而服務層會與存放庫層互動。

當我們建立服務層時，我們會利用裝飾項模式來隔離服務層的 ModelState。 在我們的服務層中，我們會針對 IValidationDictionary 介面（而不是 ModelState）進行設計。

最後，我們利用名為相依性插入模式的軟體設計模式。 此模式可讓我們針對介面（抽象）而不是實體類別進行程式設計。 執行相依性插入設計模式也可以讓我們的程式碼更容易測試。 在下一個反復專案中，我們會將單元測試新增至我們的專案。

> [!div class="step-by-step"]
> [上一頁](iteration-3-add-form-validation-vb.md)
> [下一頁](iteration-5-create-unit-tests-vb.md)
