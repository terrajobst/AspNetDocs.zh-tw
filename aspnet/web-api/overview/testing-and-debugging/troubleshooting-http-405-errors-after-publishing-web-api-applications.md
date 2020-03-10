---
uid: web-api/overview/testing-and-debugging/troubleshooting-http-405-errors-after-publishing-web-api-applications
title: 針對 Visual Studio 在生產 IIS 伺服器上運作且失敗的 Web API2 應用程式進行疑難排解
author: rmcmurray
description: 針對 Visual Studio 在生產 IIS 伺服器上運作且失敗的 Web API2 應用程式進行疑難排解
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 07ec7d37-023f-43ea-b471-60b08ce338f7
msc.legacyurl: /web-api/overview/testing-and-debugging/troubleshooting-http-405-errors-after-publishing-web-api-applications
msc.type: authoredcontent
ms.openlocfilehash: 1b47f1ade3619cfd010260352f6a96985ab3598b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555017"
---
# <a name="troubleshoot-web-api2-apps-that-work-in-visual-studio-and-fail-on-a-production-iis-server"></a>針對 Visual Studio 在生產 IIS 伺服器上運作且失敗的 Web API2 應用程式進行疑難排解

> 本檔說明如何針對部署至實際執行 IIS 伺服器的 Web API2 應用程式進行疑難排解。 它會解決常見的 HTTP 405 和501錯誤。
> 
> ## <a name="software-used-in-this-tutorial"></a>本教學課程中使用的軟體
> 
> 
> - [Internet Information Services （IIS）](https://www.iis.net/) （7版或更新版本）
> - [Web API](../../index.md) 

Web API 應用程式通常會使用數個 HTTP 動詞命令： GET、POST、PUT、DELETE 和有時 PATCH。 話雖如此，開發人員可能會遇到這些動詞由其生產 IIS 伺服器上的另一個 IIS 模組所執行的情況，這會導致 Web API 控制器在 Visual Studio 或開發伺服器上正常運作的情況。將 HTTP 405 錯誤部署到實際執行的 IIS 伺服器時，會傳回它。

## <a name="what-causes-http-405-errors"></a>導致 HTTP 405 錯誤的原因

學習如何針對 HTTP 405 錯誤進行疑難排解的第一步，就是了解 HTTP 405 錯誤到底是什麼意思。 適用于 HTTP 的主要管理檔是[RFC 2616](http://www.ietf.org/rfc/rfc2616.txt)，其會將 HTTP 405 狀態碼定義為***不允許的方法***，並在要求-URI 所識別的資源不允許 &quot;要求行中指定的方法時，進一步描述此狀態碼。&quot; 換言之，HTTP 用戶端所要求的特定 URL 不允許使用 HTTP 動詞命令。

如需簡短的回顧，以下是 RFC 2616、RFC 4918 和 RFC 5789 中所定義的數個最常使用的 HTTP 方法：

| HTTP 方法 | 說明 |
| --- | --- |
| **GET** | 這個方法是用來從 URI 抓取資料，而且可能是最常使用的 HTTP 方法。 |
| **HEAD** | 這個方法與 GET 方法非常類似，不同之處在于它不會實際從要求 URI 抓取資料，而只會抓取 HTTP 狀態。 |
| **POST** | 這個方法通常用來將新的資料傳送至 URI。POST 通常用來提交表單資料。 |
| **PUT** | 這個方法通常用來將原始資料傳送至 URI;PUT 通常用來將 JSON 或 XML 資料提交至 Web API 應用程式。 |
| **DELETE** | 這個方法是用來移除 URI 中的資料。 |
| **OPTIONS** | 這個方法通常用來抓取 URI 支援的 HTTP 方法清單。 |
| **複製移動** | 這兩種方法與 WebDAV 搭配使用，其用途一目了然。 |
| **MKCOL** | 這個方法會與 WebDAV 搭配使用，並在指定的 URI 上用來建立集合（例如目錄）。 |
| **PROPFIND PROPPATCH** | 這兩種方法會與 WebDAV 搭配使用，並用來查詢或設定 URI 的屬性。 |
| **鎖定解除鎖定** | 這兩種方法會與 WebDAV 搭配使用，並在撰寫時用來鎖定/解除鎖定要求 URI 所識別的資源。 |
| **PATCH** | 這個方法是用來修改現有的 HTTP 資源。 |

當其中一個 HTTP 方法設定為在伺服器上使用時，伺服器將會以 HTTP 狀態和其他適用于該要求的資料來回應。 （例如，GET 方法可能會收到 HTTP 200 ***OK***回應，而 PUT 方法可能會收到 Http 201***建立***的回應）。

如果 HTTP 方法未設定為在伺服器上使用，伺服器將會以 HTTP 501***不會執行***的錯誤來回應。

不過，當 HTTP 方法設定為在伺服器上使用，但已針對指定的 URI 停用時，伺服器將會以「***不允許***的 HTTP 405 方法」錯誤來回應。

## <a name="example-http-405-error"></a>HTTP 405 錯誤範例

下列 HTTP 要求和回應範例說明 HTTP 用戶端嘗試將值放入 web 伺服器上的 Web API 應用程式的情況，而伺服器傳回 HTTP 錯誤，指出不允許 PUT 方法：

HTTP 要求：

[!code-console[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample1.cmd)]

HTTP 回應：

[!code-console[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample2.cmd)]

在此範例中，HTTP 用戶端已將有效的 JSON 要求傳送至 web 伺服器上 Web API 應用程式的 URL，但伺服器傳回 HTTP 405 錯誤訊息，指出 URL 不允許 PUT 方法。 相反地，如果要求 URI 不符合 Web API 應用程式的路由，伺服器就會傳回「***找不到***HTTP 404」錯誤。

## <a name="resolve-http-405-errors"></a>解決 HTTP 405 錯誤

有幾個原因會導致無法允許特定的 HTTP 動詞命令，但有一個主要案例是 IIS 中這個錯誤的最後原因：已針對相同的動詞/方法定義多個處理常式，而其中一個處理常式封鎖了預期的處理常式處理要求。 藉由說明，IIS 會根據*applicationhost.config* *和 web.config*檔案中的連續處理程式專案，從第一次處理處理常式，其中第一個相符的路徑、動詞、資源等組合將用來處理要求。

下列範例是從 IIS 伺服器的*applicationhost.config*檔案摘錄，該檔案在使用 PUT 方法將資料提交至 Web API 應用程式時，會傳回 HTTP 405 錯誤。 在這段摘錄中，會定義數個 HTTP 處理常式，而且每個處理常式都有一組不同的 HTTP 方法，而這是已設定的兩個：清單中的最後一個專案是靜態內容處理常式，也就是在其他處理常式有 chanc 之後所使用的預設處理常式。e 檢查要求：

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample3.xml)]

在上述範例中，ASP.NET （用於 Web API）的 WebDAV 處理常式和無副檔名的 URL 處理常式，已清楚地定義為不同的 HTTP 方法清單。 請注意，雖然這種設定不一定會導致錯誤，但所有 HTTP 方法的 ISAPI DLL 處理常式都是如此。 不過，針對 HTTP 405 錯誤進行疑難排解時，需要考慮這類設定。

在上述範例中，ISAPI DLL 處理常式不是問題;事實上，問題並未定義在 IIS 伺服器的*applicationhost.config*檔案中，這是因為在 Visual Studio 中建立 web API 應用程式時 *，web.config 檔案*中所做的專案所造成的問題。 下列來自應用程式*web.config*檔案的摘錄會顯示問題的位置：

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample4.xml)]

在此摘錄中，會重新定義 ASP.NET 的無副檔名 URL 處理常式，以包含將與 Web API 應用程式搭配使用的其他 HTTP 方法。 不過，由於已針對 WebDAV 處理常式定義一組類似的 HTTP 方法，因此會發生衝突。 在此特定情況下，即使已針對包含 Web API 應用程式的網站停用 WebDAV，IIS 還是會定義和載入 WebDAV 處理常式。 在處理 HTTP PUT 要求的過程中，IIS 會呼叫 WebDAV 模組，因為它是針對 PUT 動詞所定義的。 呼叫 WebDAV 模組時，它會檢查其設定併發現它已停用，因此它會針對類似 WebDAV 要求的任何要求傳回 HTTP 405***方法不允許***的錯誤。 若要解決這個問題，您應該從已定義 Web API 應用程式之網站的 HTTP 模組清單中移除 WebDAV。 下列範例會顯示看起來可能像這樣：

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample5.xml)]

在應用程式從開發環境發行至 IIS 生產環境後，通常會發生這種情況，這是因為您的開發與生產環境之間的處理常式/模組清單不同。 例如，如果您使用 Visual Studio 2012 或更新版本來開發 Web API 應用程式，則 IIS Express 是用於測試的預設 Web 服務器。 此開發 web 伺服器是伺服器產品中所附完整 IIS 功能的相應減少版本，而此開發 web 伺服器包含一些針對開發案例所新增的變更。 例如，WebDAV 模組通常會安裝在執行完整版 IIS 的生產 web 伺服器上，但可能不在使用中。 開發版的 IIS （IIS Express）會安裝 WebDAV 模組，但 WebDAV 模組的專案會被刻意標記為批註，因此，除非您特別改變 IIS Express 設定，否則永遠不會在 IIS Express 上載入 WebDAV 模組。將 WebDAV 功能新增至 IIS Express 安裝的設定。 因此，您的 web 應用程式可能會在您的開發電腦上正常運作，但當您將 Web API 應用程式發行至實際執行的 IIS 網頁伺服器時，可能會遇到 HTTP 405 錯誤。

## <a name="http-501-errors"></a>HTTP 501 錯誤

* 指出尚未在伺服器上執行特定功能。
* 通常表示 IIS 設定中未定義符合 HTTP 要求的處理常式：
  * 可能表示未在 IIS 上正確安裝某個專案，或
  * 某些專案已修改您的 IIS 設定，因此不會定義支援特定 HTTP 方法的處理常式。

若要解決這個問題，您必須重新安裝任何嘗試使用 HTTP 方法的應用程式，其沒有對應的模組或處理常式定義。

## <a name="summary"></a>總結

當 web 伺服器的要求 URL 不允許 HTTP 方法時，就會產生 HTTP 405 錯誤。 當特定的動詞命令已定義特定的處理常式，而且該處理常式正在覆寫您預期處理要求的處理常式時，通常會發生這種狀況。
