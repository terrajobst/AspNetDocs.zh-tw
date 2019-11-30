---
uid: config-builder
title: ASP.NET 的設定構建者
author: rick-anderson
description: 瞭解如何從外部來源的 web.config 值以外的來源取得設定資料。
ms.author: riande
ms.date: 10/29/2018
msc.type: content
ms.openlocfilehash: 5299d9ab057c3096773955a7461e77a80673ebfe
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74586756"
---
# <a name="configuration-builders-for-aspnet"></a><span data-ttu-id="cb0a3-103">ASP.NET 的設定構建者</span><span class="sxs-lookup"><span data-stu-id="cb0a3-103">Configuration builders for ASP.NET</span></span>

<span data-ttu-id="cb0a3-104">By [Stephen Molloy](https://github.com/StephenMolloy)和[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="cb0a3-104">By [Stephen Molloy](https://github.com/StephenMolloy) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="cb0a3-105">設定產生器提供現代化且敏捷的機制，讓 ASP.NET 應用程式從外部來源取得設定值。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-105">Configuration builders provide a modern and agile mechanism for ASP.NET apps to get configuration values from external sources.</span></span>

<span data-ttu-id="cb0a3-106">設定產生器：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-106">Configuration builders:</span></span>

* <span data-ttu-id="cb0a3-107">.NET Framework 4.7.1 和更新版本中都有提供。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-107">Are available in .NET Framework 4.7.1 and later.</span></span>
* <span data-ttu-id="cb0a3-108">提供彈性的機制來讀取設定值。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-108">Provide a flexible mechanism for reading configuration values.</span></span>
* <span data-ttu-id="cb0a3-109">解決應用程式移入容器和雲端焦點環境時的一些基本需求。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-109">Address some of the basic needs of apps as they move into a container and cloud focused environment.</span></span>
* <span data-ttu-id="cb0a3-110">可以用來改善設定資料的保護，方法是從先前無法使用的來源（例如，Azure Key Vault 和環境變數）在 .NET 設定系統中進行繪製。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-110">Can be used to improve protection of configuration data by drawing from sources previously unavailable (for example, Azure Key Vault and environment variables) in the .NET configuration system.</span></span>

## <a name="keyvalue-configuration-builders"></a><span data-ttu-id="cb0a3-111">索引鍵/值設定產生器</span><span class="sxs-lookup"><span data-stu-id="cb0a3-111">Key/value configuration builders</span></span>

<span data-ttu-id="cb0a3-112">設定產生器可以處理的常見案例，是為遵循索引鍵/值模式的設定區段提供基本的索引鍵/值取代機制。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-112">A common scenario that can be handled by configuration builders is to provide a basic key/value replacement mechanism for configuration sections that follow a key/value pattern.</span></span> <span data-ttu-id="cb0a3-113">Configurationbuilders.ignoreloadfailure 的 .NET Framework 概念不限於特定的設定區段或模式。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-113">The .NET Framework concept of ConfigurationBuilders is not limited to specific configuration sections or patterns.</span></span> <span data-ttu-id="cb0a3-114">不過，`Microsoft.Configuration.ConfigurationBuilders` （[github](https://github.com/aspnet/MicrosoftConfigurationBuilders)、 [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)）中的許多設定產生器都是在索引鍵/值模式內工作。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-114">However, many of the configuration builders in `Microsoft.Configuration.ConfigurationBuilders` ([github](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) work within the key/value pattern.</span></span>

## <a name="keyvalue-configuration-builders-settings"></a><span data-ttu-id="cb0a3-115">索引鍵/值設定構建者設定</span><span class="sxs-lookup"><span data-stu-id="cb0a3-115">Key/value configuration builders settings</span></span>

<span data-ttu-id="cb0a3-116">下列設定適用于 `Microsoft.Configuration.ConfigurationBuilders`中的所有索引鍵/值設定產生器。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-116">The following settings apply to all key/value configuration builders in `Microsoft.Configuration.ConfigurationBuilders`.</span></span>

### <a name="mode"></a><span data-ttu-id="cb0a3-117">Mode</span><span class="sxs-lookup"><span data-stu-id="cb0a3-117">Mode</span></span>

<span data-ttu-id="cb0a3-118">設定產生器會使用索引鍵/值資訊的外部來源來填入設定系統的選取索引鍵/值元素。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-118">The configuration builders use an external source of key/value information to populate selected key/value elements of the configuration system.</span></span> <span data-ttu-id="cb0a3-119">具體而言，`<appSettings/>` 和 `<connectionStrings/>` 區段會收到設定產生器的特殊處理。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-119">Specifically, the `<appSettings/>` and `<connectionStrings/>` sections receive special treatment from the configuration builders.</span></span> <span data-ttu-id="cb0a3-120">產生器適用于三種模式：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-120">The builders work in three modes:</span></span>

* <span data-ttu-id="cb0a3-121">`Strict`-預設模式。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-121">`Strict` - The default mode.</span></span> <span data-ttu-id="cb0a3-122">在此模式中，設定產生器只會在知名的索引鍵/值中心設定區段上運作。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-122">In this mode, the configuration builder only operates on well-known key/value-centric configuration sections.</span></span> <span data-ttu-id="cb0a3-123">`Strict` 模式會列舉區段中的每個索引鍵。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-123">`Strict` mode enumerates each key in the section.</span></span> <span data-ttu-id="cb0a3-124">如果在外部來源中找到相符的索引鍵：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-124">If a matching key is found in the external source:</span></span>

   * <span data-ttu-id="cb0a3-125">設定產生器會將結果設定區段中的值取代為來自外部來源的值。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-125">The configuration builders replace the value in the resulting configuration section with the value from the external source.</span></span>
* <span data-ttu-id="cb0a3-126">`Greedy`-此模式與 `Strict` 模式密切相關。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-126">`Greedy` - This mode is closely related to `Strict` mode.</span></span> <span data-ttu-id="cb0a3-127">而不限於原始設定中已存在的金鑰：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-127">Rather than being limited to keys that already exist in the original configuration:</span></span>

  * <span data-ttu-id="cb0a3-128">設定產生器會將外部來源中的所有機碼/值組新增至 [產生的設定] 區段。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-128">The configuration builders adds all key/value pairs from the external source into the resulting configuration section.</span></span>

* <span data-ttu-id="cb0a3-129">`Expand`-在原始 XML 上進行操作，再將它剖析成設定區段物件。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-129">`Expand` - Operates on the raw XML before it's parsed into a configuration section object.</span></span> <span data-ttu-id="cb0a3-130">您可以將它視為字串中的標記擴充。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-130">It can be thought of as an expansion of tokens in a string.</span></span> <span data-ttu-id="cb0a3-131">原始 XML 字串中符合模式 `${token}` 的任何部分都是用於標記擴充的候選項目。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-131">Any part of the raw XML string that matches the pattern `${token}` is a candidate for token expansion.</span></span> <span data-ttu-id="cb0a3-132">如果在外部來源中找不到對應的值，則 token 不會變更。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-132">If no corresponding value is found in the external source, then the token is not changed.</span></span> <span data-ttu-id="cb0a3-133">此模式中的產生器不限於 `<appSettings/>` 和 `<connectionStrings/>` 區段。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-133">Builders in this mode are not limited to the `<appSettings/>` and `<connectionStrings/>` sections.</span></span>

<span data-ttu-id="cb0a3-134">下列*來自 web.config 的標記*會在 `Strict` 模式中啟用[EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) ：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-134">The following markup from *web.config* enables the [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) in `Strict` mode:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

<span data-ttu-id="cb0a3-135">下列程式碼會讀取先前*web.config*檔案中顯示的 `<appSettings/>` 和 `<connectionStrings/>`：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-135">The following code reads the `<appSettings/>` and `<connectionStrings/>` shown in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

<span data-ttu-id="cb0a3-136">上述程式碼會將屬性值設定為：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-136">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="cb0a3-137">如果未在環境變數中設定索引鍵，則*為 web.config 檔案*中的值。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-137">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="cb0a3-138">環境變數的值（如果已設定的話）。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-138">The values of the environment variable, if set.</span></span>

<span data-ttu-id="cb0a3-139">例如，`ServiceID` 將包含：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-139">For example, `ServiceID` will contain:</span></span>

* <span data-ttu-id="cb0a3-140">「如果未設定環境變數 `ServiceID`，則為 web.config 中的 ServiceID 值」。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-140">"ServiceID value from web.config", if the environment variable `ServiceID` is not set.</span></span>
* <span data-ttu-id="cb0a3-141">如果已設定，則為 `ServiceID` 環境變數的值。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-141">The value of the `ServiceID` environment variable, if set.</span></span>

<span data-ttu-id="cb0a3-142">下圖顯示先前在環境編輯器中設定*的 web.config 檔案*中的 `<appSettings/>` 索引鍵/值：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-142">The following image shows the `<appSettings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![環境編輯器](config-builder/static/env.png)

<span data-ttu-id="cb0a3-144">注意：您可能需要結束並重新啟動 Visual Studio，才能看到環境變數的變更。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-144">Note: You might need to exit and restart Visual Studio to see changes in environment variables.</span></span>

### <a name="prefix-handling"></a><span data-ttu-id="cb0a3-145">前置詞處理</span><span class="sxs-lookup"><span data-stu-id="cb0a3-145">Prefix handling</span></span>

<span data-ttu-id="cb0a3-146">金鑰首碼可以簡化設定金鑰，因為：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-146">Key prefixes can simplify setting keys because:</span></span>

* <span data-ttu-id="cb0a3-147">.NET Framework 設定是複雜且嵌套的。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-147">The .NET Framework configuration is complex and nested.</span></span>
* <span data-ttu-id="cb0a3-148">外部索引鍵/值來源通常是基本的，而且本質上是一般的。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-148">External key/value sources are commonly basic and flat by nature.</span></span> <span data-ttu-id="cb0a3-149">例如，環境變數不是嵌套的。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-149">For example, environment variables are not nested.</span></span>

<span data-ttu-id="cb0a3-150">使用下列任何方法，透過環境變數將 `<appSettings/>` 和 `<connectionStrings/>` 插入設定中：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-150">Use any of the following approaches to inject both `<appSettings/>` and `<connectionStrings/>` into the configuration via environment variables:</span></span>

* <span data-ttu-id="cb0a3-151">使用預設 `Strict` 模式中的 `EnvironmentConfigBuilder` 和設定檔中的適當索引鍵名稱。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-151">With the `EnvironmentConfigBuilder` in the default `Strict` mode and the appropriate key names in the configuration file.</span></span> <span data-ttu-id="cb0a3-152">上述程式碼和標記採用這種方法。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-152">The preceding code and markup takes this approach.</span></span> <span data-ttu-id="cb0a3-153">使用這種方法時，`<appSettings/>` 和 `<connectionStrings/>`中都**不**能有相同名稱的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-153">Using this approach you can **not** have identically named keys in both `<appSettings/>` and `<connectionStrings/>`.</span></span>
* <span data-ttu-id="cb0a3-154">在 `Greedy` 模式中使用兩個 `EnvironmentConfigBuilder`s，並使用不同的前置詞和 `stripPrefix`。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-154">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes and `stripPrefix`.</span></span> <span data-ttu-id="cb0a3-155">使用此方法，應用程式可以讀取 `<appSettings/>` 和 `<connectionStrings/>`，而不需要更新設定檔。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-155">With this approach, the app can read `<appSettings/>` and `<connectionStrings/>` without needing to update the configuration file.</span></span> <span data-ttu-id="cb0a3-156">下一節[stripPrefix](#stripprefix)會示範如何執行此動作。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-156">The next section,  [stripPrefix](#stripprefix),  shows how to do this.</span></span>
* <span data-ttu-id="cb0a3-157">在具有不同前置詞的 `Greedy` 模式中使用兩個 `EnvironmentConfigBuilder`s。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-157">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes.</span></span> <span data-ttu-id="cb0a3-158">使用此方法時，您不能有重複的索引鍵名稱，因為索引鍵名稱必須依前置詞而有所不同。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-158">With this approach you can't have duplicate key names as key names must differ by prefix.</span></span>  <span data-ttu-id="cb0a3-159">例如：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-159">For example:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

<span data-ttu-id="cb0a3-160">使用上述標記時，可以使用相同的一般索引鍵/值來源來填入兩個不同區段的設定。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-160">With the preceding markup, the same flat key/value source can be used to populate configuration for two different sections.</span></span>

<span data-ttu-id="cb0a3-161">下圖顯示先前在環境編輯器中設定*的 web.config 檔案*中的 `<appSettings/>` 和 `<connectionStrings/>` 索引鍵/值：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-161">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![環境編輯器](config-builder/static/prefix.png)

<span data-ttu-id="cb0a3-163">下列程式碼會讀取前述*web.config*檔案中包含的 `<appSettings/>` 和 `<connectionStrings/>` 索引鍵/值：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-163">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

<span data-ttu-id="cb0a3-164">上述程式碼會將屬性值設定為：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-164">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="cb0a3-165">如果未在環境變數中設定索引鍵，則*為 web.config 檔案*中的值。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-165">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="cb0a3-166">環境變數的值（如果已設定的話）。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-166">The values of the environment variable, if set.</span></span>

<span data-ttu-id="cb0a3-167">例如，使用先前的*web.config*檔案、先前環境編輯器影像中的索引鍵/值，以及先前的程式碼，會設定下列值：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-167">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="cb0a3-168">索引鍵</span><span class="sxs-lookup"><span data-stu-id="cb0a3-168">Key</span></span>              | <span data-ttu-id="cb0a3-169">{2&gt;值&lt;2}</span><span class="sxs-lookup"><span data-stu-id="cb0a3-169">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="cb0a3-170">AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="cb0a3-170">AppSetting_ServiceID</span></span>           | <span data-ttu-id="cb0a3-171">從 env 變數 AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="cb0a3-171">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="cb0a3-172">AppSetting_default</span><span class="sxs-lookup"><span data-stu-id="cb0a3-172">AppSetting_default</span></span>            | <span data-ttu-id="cb0a3-173">來自 env 的 AppSetting_default 值</span><span class="sxs-lookup"><span data-stu-id="cb0a3-173">AppSetting_default value from env</span></span> |
|       <span data-ttu-id="cb0a3-174">ConnStr_default</span><span class="sxs-lookup"><span data-stu-id="cb0a3-174">ConnStr_default</span></span>         | <span data-ttu-id="cb0a3-175">從 env ConnStr_default val</span><span class="sxs-lookup"><span data-stu-id="cb0a3-175">ConnStr_default val from env</span></span>|

### <a name="stripprefix"></a><span data-ttu-id="cb0a3-176">stripPrefix</span><span class="sxs-lookup"><span data-stu-id="cb0a3-176">stripPrefix</span></span>

<span data-ttu-id="cb0a3-177">`stripPrefix`：布林值，預設為 `false`。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-177">`stripPrefix`: boolean, defaults to `false`.</span></span> 

<span data-ttu-id="cb0a3-178">上述 XML 標記會將應用程式設定與連接字串分開，*但 web.config 檔案*中的所有索引鍵都必須使用指定的前置詞。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-178">The preceding XML markup separates app settings from connection strings but requires all the keys in the *web.config* file to use the specified prefix.</span></span> <span data-ttu-id="cb0a3-179">例如，必須將前置詞 `AppSetting` 新增至 `ServiceID` 機碼（"AppSetting_ServiceID"）。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-179">For example, the prefix `AppSetting` must be added to the `ServiceID` key ("AppSetting_ServiceID").</span></span> <span data-ttu-id="cb0a3-180">使用 `stripPrefix`時，不會*在 web.config 檔案*中使用前置詞。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-180">With `stripPrefix`, the prefix is not used in the *web.config* file.</span></span> <span data-ttu-id="cb0a3-181">設定產生器來源（例如環境中的）中必須有前置詞。我們預期大部分的開發人員都會使用 `stripPrefix`。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-181">The prefix is required in the configuration builder source (for example, in the environment.) We anticipate most developers will use `stripPrefix`.</span></span>

<span data-ttu-id="cb0a3-182">應用程式通常會去除前置詞。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-182">Applications typically strip off the prefix.</span></span> <span data-ttu-id="cb0a3-183">下列 web.config*會去除前置*詞：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-183">The following *web.config* strips the prefix:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

<span data-ttu-id="cb0a3-184">在*前述的 web.config 檔案*中，`default` 鍵同時位於 `<appSettings/>` 和 `<connectionStrings/>`。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-184">In the preceding *web.config* file, the `default` key is in both the `<appSettings/>` and `<connectionStrings/>`.</span></span>

<span data-ttu-id="cb0a3-185">下圖顯示先前在環境編輯器中設定*的 web.config 檔案*中的 `<appSettings/>` 和 `<connectionStrings/>` 索引鍵/值：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-185">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![環境編輯器](config-builder/static/prefix.png)

<span data-ttu-id="cb0a3-187">下列程式碼會讀取前述*web.config*檔案中包含的 `<appSettings/>` 和 `<connectionStrings/>` 索引鍵/值：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-187">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

<span data-ttu-id="cb0a3-188">上述程式碼會將屬性值設定為：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-188">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="cb0a3-189">如果未在環境變數中設定索引鍵，則*為 web.config 檔案*中的值。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-189">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="cb0a3-190">環境變數的值（如果已設定的話）。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-190">The values of the environment variable, if set.</span></span>

<span data-ttu-id="cb0a3-191">例如，使用先前的*web.config*檔案、先前環境編輯器影像中的索引鍵/值，以及先前的程式碼，會設定下列值：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-191">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="cb0a3-192">索引鍵</span><span class="sxs-lookup"><span data-stu-id="cb0a3-192">Key</span></span>              | <span data-ttu-id="cb0a3-193">{2&gt;值&lt;2}</span><span class="sxs-lookup"><span data-stu-id="cb0a3-193">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="cb0a3-194">ServiceID</span><span class="sxs-lookup"><span data-stu-id="cb0a3-194">ServiceID</span></span>           | <span data-ttu-id="cb0a3-195">從 env 變數 AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="cb0a3-195">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="cb0a3-196">預設</span><span class="sxs-lookup"><span data-stu-id="cb0a3-196">default</span></span>            | <span data-ttu-id="cb0a3-197">來自 env 的 AppSetting_default 值</span><span class="sxs-lookup"><span data-stu-id="cb0a3-197">AppSetting_default value from env</span></span> |
|    <span data-ttu-id="cb0a3-198">預設</span><span class="sxs-lookup"><span data-stu-id="cb0a3-198">default</span></span>         | <span data-ttu-id="cb0a3-199">從 env ConnStr_default val</span><span class="sxs-lookup"><span data-stu-id="cb0a3-199">ConnStr_default val from env</span></span>|

### <a name="tokenpattern"></a><span data-ttu-id="cb0a3-200">tokenPattern</span><span class="sxs-lookup"><span data-stu-id="cb0a3-200">tokenPattern</span></span>

<span data-ttu-id="cb0a3-201">`tokenPattern`：字串，預設為 `@"\$\{(\w+)\}"`</span><span class="sxs-lookup"><span data-stu-id="cb0a3-201">`tokenPattern`: String, defaults to `@"\$\{(\w+)\}"`</span></span>

<span data-ttu-id="cb0a3-202">產生器的 `Expand` 行為會在原始 XML 中搜尋看起來像 `${token}`的權杖。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-202">The `Expand` behavior of the builders searches the raw XML for tokens that look like `${token}`.</span></span> <span data-ttu-id="cb0a3-203">使用預設的正則運算式 `@"\$\{(\w+)\}"`來進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-203">Searching is done with the default regular expression `@"\$\{(\w+)\}"`.</span></span> <span data-ttu-id="cb0a3-204">符合 `\w` 的字元組比 XML 更嚴格，而且有許多設定來源允許。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-204">The set of characters that matches `\w` is more strict than XML and many configuration sources allow.</span></span> <span data-ttu-id="cb0a3-205">當令牌名稱中需要比 `@"\$\{(\w+)\}"` 更多的字元時，請使用 `tokenPattern`。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-205">Use `tokenPattern` when more characters than `@"\$\{(\w+)\}"` are required in the token name.</span></span>

<span data-ttu-id="cb0a3-206">`tokenPattern`：字串：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-206">`tokenPattern`: String:</span></span>

* <span data-ttu-id="cb0a3-207">可讓開發人員變更用於標記比對的 RegEx。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-207">Allows developers to change the regex that is used for token matching.</span></span>
* <span data-ttu-id="cb0a3-208">不會進行任何驗證，以確保它是格式正確、不危險的 RegEx。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-208">No validation is done to make sure it is a well-formed, non-dangerous regex.</span></span>
* <span data-ttu-id="cb0a3-209">它必須包含一個「capture 群組」。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-209">It must contain a capture group.</span></span> <span data-ttu-id="cb0a3-210">整個 RegEx 必須符合整個 token。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-210">The entire regex must match the entire token.</span></span> <span data-ttu-id="cb0a3-211">第一個 capture 必須是要在設定來源中查詢的權杖名稱。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-211">The first capture must be the token name to look up in the configuration source.</span></span>

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a><span data-ttu-id="cb0a3-212">Configurationbuilders.ignoreloadfailure 中的設定構建者</span><span class="sxs-lookup"><span data-stu-id="cb0a3-212">Configuration builders in Microsoft.Configuration.ConfigurationBuilders</span></span>

### <a name="environmentconfigbuilder"></a><span data-ttu-id="cb0a3-213">EnvironmentConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="cb0a3-213">EnvironmentConfigBuilder</span></span>

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

<span data-ttu-id="cb0a3-214">[EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/)：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-214">The [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span></span>

* <span data-ttu-id="cb0a3-215">是設定產生器的最簡單。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-215">Is the simplest of the configuration builders.</span></span>
* <span data-ttu-id="cb0a3-216">從環境讀取值。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-216">Reads values from the environment.</span></span>
* <span data-ttu-id="cb0a3-217">沒有任何其他設定選項。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-217">Does not have any additional configuration options.</span></span>
* <span data-ttu-id="cb0a3-218">`name` 屬性值是任意的。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-218">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="cb0a3-219">**注意：** 在 Windows 容器環境中，在執行時間設定的變數只會插入進入點處理環境。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-219">**Note:** In a Windows container environment, variables set at run time are only injected into the EntryPoint process environment.</span></span> <span data-ttu-id="cb0a3-220">執行為服務或非進入點進程的應用程式不會挑選這些變數，除非以其他方式插入容器中的機制。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-220">Apps that run as a service or a non-EntryPoint process do not pick up these variables unless they are otherwise injected through a mechanism in the container.</span></span> <span data-ttu-id="cb0a3-221">針對[IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)為基礎的容器， [ServiceMonitor](https://github.com/Microsoft/iis-docker/pull/41)的目前版本只會在*DefaultAppPool*中處理此項。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-221">For [IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)-based containers, the current version of [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) handles this in the *DefaultAppPool* only.</span></span> <span data-ttu-id="cb0a3-222">其他以 Windows 為基礎的容器變體可能需要針對非進入點進程開發自己的插入式機制。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-222">Other Windows-based container variants may need to develop their own injection mechanism for non-EntryPoint processes.</span></span>

### <a name="usersecretsconfigbuilder"></a><span data-ttu-id="cb0a3-223">UserSecretsConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="cb0a3-223">UserSecretsConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="cb0a3-224">絕對不要在原始程式碼中儲存密碼、敏感性連接字串或其他機密資料。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-224">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="cb0a3-225">生產秘密不應用於開發或測試。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-225">Production secrets should not be used for development or test.</span></span>

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

<span data-ttu-id="cb0a3-226">此設定產生器提供的功能類似于[ASP.NET Core 秘密管理員](/aspnet/core/security/app-secrets)。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-226">This configuration builder provides a feature similar to [ASP.NET Core Secret Manager](/aspnet/core/security/app-secrets).</span></span>

<span data-ttu-id="cb0a3-227">[UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/)可用於 .NET Framework 專案中，但必須指定秘密檔案。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-227">The [UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) can be used in .NET Framework projects, but a secrets file must be specified.</span></span> <span data-ttu-id="cb0a3-228">或者，您可以在專案檔中定義 `UserSecretsId` 屬性，並在正確的位置中建立原始秘密檔案以供讀取。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-228">Alternatively, you can define the `UserSecretsId` property in the project file and create the raw secrets file in the correct location for reading.</span></span> <span data-ttu-id="cb0a3-229">為避免專案中的外部相依性，會將密碼檔案格式化為 XML。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-229">To keep external dependencies out of your project, the secret file is XML formatted.</span></span> <span data-ttu-id="cb0a3-230">XML 格式是一個執行詳細資料，且格式不應依賴。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-230">The XML formatting is an implementation detail, and the format should not be relied upon.</span></span> <span data-ttu-id="cb0a3-231">如果您需要與 .NET Core 專案共用*秘密 json*檔案，請考慮使用[SimpleJsonConfigBuilder](#simplejsonconfigbuilder)。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-231">If you need to share a *secrets.json* file with .NET Core projects, consider using the [SimpleJsonConfigBuilder](#simplejsonconfigbuilder).</span></span> <span data-ttu-id="cb0a3-232">.NET Core 的 `SimpleJsonConfigBuilder` 格式也應該被視為要變更的執行詳細資料。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-232">The `SimpleJsonConfigBuilder` format for .NET Core should also be considered an implementation detail subject to change.</span></span>

<span data-ttu-id="cb0a3-233">`UserSecretsConfigBuilder`的設定屬性：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-233">Configuration attributes for `UserSecretsConfigBuilder`:</span></span>

* <span data-ttu-id="cb0a3-234">`userSecretsId`-這是用來識別 XML 秘密檔案的慣用方法。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-234">`userSecretsId` - This is the preferred method for identifying an XML secrets file.</span></span> <span data-ttu-id="cb0a3-235">其運作方式類似于 .NET Core，它會使用 `UserSecretsId` 專案屬性來儲存此識別碼。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-235">It works similar to .NET Core, which uses a `UserSecretsId` project property to store this identifier.</span></span> <span data-ttu-id="cb0a3-236">此字串必須是唯一的，不需要是 GUID。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-236">The string must be unique, it doesn't need to be a GUID.</span></span> <span data-ttu-id="cb0a3-237">使用此屬性時，`UserSecretsConfigBuilder` 會尋找屬於此識別碼之秘密檔案的知名本機位置（`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`）。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-237">With this attribute, the `UserSecretsConfigBuilder` look in a well-known local location (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`) for a secrets file belonging to this identifier.</span></span>
* <span data-ttu-id="cb0a3-238">`userSecretsFile`-選擇性屬性，指定包含密碼的檔案。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-238">`userSecretsFile` - An optional attribute specifying the file containing the secrets.</span></span> <span data-ttu-id="cb0a3-239">在開始時，可以使用 `~` 字元來參考應用程式根目錄。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-239">The `~` character can be used at the start to reference the application root.</span></span> <span data-ttu-id="cb0a3-240">此屬性或 `userSecretsId` 屬性為必要項。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-240">Either this attribute or the `userSecretsId` attribute is required.</span></span> <span data-ttu-id="cb0a3-241">如果同時指定這兩者，`userSecretsFile` 會優先使用。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-241">If both are specified, `userSecretsFile` takes precedence.</span></span>
* <span data-ttu-id="cb0a3-242">`optional`：布林值，預設值 `true`-如果找不到秘密檔案，就會避免例外狀況。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-242">`optional`: boolean, default value `true` - Prevents an exception if the secrets file cannot be found.</span></span> 
* <span data-ttu-id="cb0a3-243">`name` 屬性值是任意的。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-243">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="cb0a3-244">秘密檔案具有下列格式：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-244">The secrets file has the following format:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a><span data-ttu-id="cb0a3-245">AzureKeyVaultConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="cb0a3-245">AzureKeyVaultConfigBuilder</span></span>

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [connectionString="connection string"]
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

<span data-ttu-id="cb0a3-246">[AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/)會讀取儲存在[Azure Key Vault](/azure/key-vault/key-vault-whatis)中的值。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-246">The [AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) reads values stored in the [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

<span data-ttu-id="cb0a3-247">需要 `vaultName` （保存庫的名稱或保存庫的 URI）。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-247">`vaultName` is required (either the name of the vault or a URI to the vault).</span></span> <span data-ttu-id="cb0a3-248">其他屬性可控制要連接的保存庫，但只有在應用程式不是在與 `Microsoft.Azure.Services.AppAuthentication`搭配運作的環境中執行時才需要。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-248">The other attributes allow control about which vault to connect to, but are only necessary if the application is not running in an environment that works with `Microsoft.Azure.Services.AppAuthentication`.</span></span> <span data-ttu-id="cb0a3-249">Azure 服務驗證程式庫會在可能的情況下，用來自動從執行環境中挑選連線資訊。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-249">The Azure Services Authentication library is used to automatically pick up connection information from the execution environment if possible.</span></span> <span data-ttu-id="cb0a3-250">您可以藉由提供連接字串，覆寫自動挑選連接資訊。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-250">You can override automatically pick up of connection information by providing a connection string.</span></span>

* <span data-ttu-id="cb0a3-251">`vaultName`-如果未提供 `uri` 則為必要項。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-251">`vaultName` - Required if `uri` in not provided.</span></span> <span data-ttu-id="cb0a3-252">在您的 Azure 訂用帳戶中，指定要從中讀取索引鍵/值組的保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-252">Specifies the name of the vault in your Azure subscription from which to read key/value pairs.</span></span>
* <span data-ttu-id="cb0a3-253">`connectionString`- [azureservicetokenprovider 會](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support)可使用的連接字串</span><span class="sxs-lookup"><span data-stu-id="cb0a3-253">`connectionString` - A connection string usable by [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support)</span></span>
* <span data-ttu-id="cb0a3-254">`uri`-使用指定的 `uri` 值連接到其他 Key Vault 提供者。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-254">`uri` - Connects to other Key Vault providers with the specified `uri` value.</span></span> <span data-ttu-id="cb0a3-255">如果未指定，則 Azure （`vaultName`）是保存庫提供者。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-255">If not specified, Azure (`vaultName`) is the vault provider.</span></span>
* <span data-ttu-id="cb0a3-256">`version` Azure Key Vault 提供秘密的版本控制功能。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-256">`version` - Azure Key Vault provides a versioning feature for secrets.</span></span> <span data-ttu-id="cb0a3-257">如果指定了 `version`，產生器只會抓取符合此版本的密碼。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-257">If `version` is specified, the builder only retrieves secrets matching this version.</span></span>
* <span data-ttu-id="cb0a3-258">`preloadSecretNames`-根據預設，此產生器會在金鑰保存庫中 querys**所有**金鑰名稱（當它初始化時）。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-258">`preloadSecretNames` - By default, this builder querys **all** key names in the key vault when it is initialized.</span></span> <span data-ttu-id="cb0a3-259">若要避免讀取所有索引鍵值，請將此屬性設定為 `false`。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-259">To prevent reading all key values, set this attribute to `false`.</span></span> <span data-ttu-id="cb0a3-260">將此項設定為 `false` 一次讀取一個秘密。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-260">Setting this to `false` reads secrets one at a time.</span></span> <span data-ttu-id="cb0a3-261">如果保存庫允許「取得」存取權，而不是「列出」存取權，一次讀取一個秘密會很有用。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-261">Reading secrets one at a time can useful if the vault allows "Get" access but not "List" access.</span></span> <span data-ttu-id="cb0a3-262">**注意：** 使用 `Greedy` 模式時，`preloadSecretNames` 必須 `true` （預設值）。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-262">**Note:** When using `Greedy` mode, `preloadSecretNames` must be `true` (the default.)</span></span>

### <a name="keyperfileconfigbuilder"></a><span data-ttu-id="cb0a3-263">KeyPerFileConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="cb0a3-263">KeyPerFileConfigBuilder</span></span>

```xml
<add name="KeyPerFile"
    [mode|prefix|stripPrefix|tokenPattern]
    (directoryPath="PathToSourceDirectory")
    [ignorePrefix="ignore."]
    [keyDelimiter=":"]
    [optional="false"]
    type="Microsoft.Configuration.ConfigurationBuilders.KeyPerFileConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.KeyPerFile" />
```

<span data-ttu-id="cb0a3-264">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/)是基本的設定產生器，會使用目錄的檔案做為值的來源。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-264">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) is a basic configuration builder that uses a directory's files as a source of values.</span></span> <span data-ttu-id="cb0a3-265">檔案的名稱是索引鍵，而內容則是值。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-265">A file's name is the key, and the contents are the value.</span></span> <span data-ttu-id="cb0a3-266">在協調的容器環境中執行時，此設定產生器可能會很有用。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-266">This configuration builder can be useful when running in an orchestrated container environment.</span></span> <span data-ttu-id="cb0a3-267">Docker Swarm 和 Kubernetes 這類系統會以每個檔案的方式，為其協調的 windows 容器提供 `secrets`。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-267">Systems like Docker Swarm and Kubernetes provide `secrets` to their orchestrated windows containers in this key-per-file manner.</span></span>

<span data-ttu-id="cb0a3-268">屬性詳細資料：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-268">Attribute details:</span></span>

* <span data-ttu-id="cb0a3-269">`directoryPath` - 必要項。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-269">`directoryPath` - Required.</span></span> <span data-ttu-id="cb0a3-270">指定要在其中尋找值的路徑。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-270">Specifies a path to look in for values.</span></span> <span data-ttu-id="cb0a3-271">適用於 Windows 的 Docker 秘密預設會儲存在*C:\ProgramData\Docker\secrets*目錄中。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-271">Docker for Windows secrets are stored in the *C:\ProgramData\Docker\secrets* directory by default.</span></span>
* <span data-ttu-id="cb0a3-272">`ignorePrefix`-排除以這個前置詞開頭的檔案。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-272">`ignorePrefix` - Files that start with this prefix are excluded.</span></span> <span data-ttu-id="cb0a3-273">預設為 "ignore."。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-273">Defaults to "ignore.".</span></span>
* <span data-ttu-id="cb0a3-274">`keyDelimiter`-預設值為 `null`。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-274">`keyDelimiter` - Default value is `null`.</span></span> <span data-ttu-id="cb0a3-275">如果指定，則設定產生器會遍歷目錄的多個層級，並使用此分隔符號來建立索引鍵名稱。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-275">If specified, the configuration builder traverses multiple levels of the directory, building up key names with this delimiter.</span></span> <span data-ttu-id="cb0a3-276">如果此值為 `null`，則設定產生器只會查看目錄的最上層。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-276">If this value is `null`, the configuration builder only looks at the top level of the directory.</span></span>
* <span data-ttu-id="cb0a3-277">`optional`-預設值為 `false`。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-277">`optional` -  Default value is `false`.</span></span> <span data-ttu-id="cb0a3-278">指定如果來原始目錄不存在，設定產生器是否應該造成錯誤。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-278">Specifies whether the configuration builder should cause errors if the source directory doesn't exist.</span></span>

### <a name="simplejsonconfigbuilder"></a><span data-ttu-id="cb0a3-279">SimpleJsonConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="cb0a3-279">SimpleJsonConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="cb0a3-280">絕對不要在原始程式碼中儲存密碼、敏感性連接字串或其他機密資料。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-280">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="cb0a3-281">生產秘密不應用於開發或測試。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-281">Production secrets should not be used for development or test.</span></span>

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

<span data-ttu-id="cb0a3-282">.NET Core 專案經常會使用 JSON 檔案進行設定。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-282">.NET Core projects frequently use JSON files for configuration.</span></span> <span data-ttu-id="cb0a3-283">[SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) builder 允許在 .NET Framework 中使用 .NET Core JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-283">The [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) builder allows .NET Core JSON files to be used in the .NET Framework.</span></span> <span data-ttu-id="cb0a3-284">此設定產生器提供從一般索引鍵/值來源到 .NET Framework 設定的特定索引鍵/值區域的基本對應。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-284">This configuration builder is provides a basic mapping from a flat key/value source into specific key/value areas of .NET Framework configuration.</span></span> <span data-ttu-id="cb0a3-285">此設定產生器**不提供階層**式設定。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-285">This configuration builder does **not** provide for hierarchical configurations.</span></span> <span data-ttu-id="cb0a3-286">JSON 支援檔案類似于字典，而不是複雜的階層式物件。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-286">The JSON backing file is similar to a dictionary, not a complex hierarchical object.</span></span> <span data-ttu-id="cb0a3-287">可以使用多層級的階層式檔案。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-287">A multi-level hierarchical file can be used.</span></span> <span data-ttu-id="cb0a3-288">此提供者 `flatten`的深度，方法是在每個層級附加屬性名稱，並使用 `:` 作為分隔符號。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-288">This provider `flatten`s the depth by appending the property name at each level using `:` as a delimiter.</span></span>

<span data-ttu-id="cb0a3-289">屬性詳細資料：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-289">Attribute details:</span></span>

* <span data-ttu-id="cb0a3-290">`jsonFile` - 必要項。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-290">`jsonFile` - Required.</span></span> <span data-ttu-id="cb0a3-291">指定要從中讀取的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-291">Specifies the JSON file to read from.</span></span> <span data-ttu-id="cb0a3-292">在開始時，可以使用 `~` 字元來參考應用程式根目錄。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-292">The `~` character can be used at the start to reference the app root.</span></span>
* <span data-ttu-id="cb0a3-293">`optional` 布林值，預設值是 `true`。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-293">`optional` - Boolean,  default value is `true`.</span></span> <span data-ttu-id="cb0a3-294">如果找不到 JSON 檔案，則防止擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-294">Prevents throwing exceptions if the JSON file cannot be found.</span></span>
* <span data-ttu-id="cb0a3-295">`jsonMode` - `[Flat|Sectional]`.</span><span class="sxs-lookup"><span data-stu-id="cb0a3-295">`jsonMode` - `[Flat|Sectional]`.</span></span> <span data-ttu-id="cb0a3-296">`Flat` 是預設值。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-296">`Flat` is the default.</span></span> <span data-ttu-id="cb0a3-297">當 `jsonMode` `Flat`時，JSON 檔案是單一的一般索引鍵/值來源。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-297">When `jsonMode` is `Flat`, the JSON file is a single flat key/value source.</span></span> <span data-ttu-id="cb0a3-298">`EnvironmentConfigBuilder` 和 `AzureKeyVaultConfigBuilder` 也是單一的一般索引鍵/值來源。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-298">The `EnvironmentConfigBuilder` and `AzureKeyVaultConfigBuilder` are also single flat key/value sources.</span></span> <span data-ttu-id="cb0a3-299">當 `SimpleJsonConfigBuilder` 設定為 `Sectional` 模式時：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-299">When the `SimpleJsonConfigBuilder` is configured in `Sectional` mode:</span></span>

  * <span data-ttu-id="cb0a3-300">在概念上，JSON 檔案會分成多個字典，而不是在最上層。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-300">The JSON file is conceptually divided just at the top level into multiple dictionaries.</span></span>
  * <span data-ttu-id="cb0a3-301">每個字典只會套用至符合附加至其最上層屬性名稱的設定區段。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-301">Each of the dictionaries is only applied to the configuration section that matches the top-level property name attached to them.</span></span> <span data-ttu-id="cb0a3-302">例如：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-302">For example:</span></span>

```json
    {
        "appSettings" : {
            "setting1" : "value1",
            "setting2" : "value2",
            "complex" : {
                "setting1" : "complex:value1",
                "setting2" : "complex:value2",
            }
        }
    }
```

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a><span data-ttu-id="cb0a3-303">執行自訂索引鍵/值設定產生器</span><span class="sxs-lookup"><span data-stu-id="cb0a3-303">Implementing a custom key/value configuration builder</span></span>

<span data-ttu-id="cb0a3-304">如果設定產生器不符合您的需求，您可以撰寫一個自訂的程式。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-304">If the configuration builders don't meet your needs, you can write a custom one.</span></span> <span data-ttu-id="cb0a3-305">`KeyValueConfigBuilder` 基類會處理替代模式和大部分前置詞的顧慮。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-305">The `KeyValueConfigBuilder` base class handles substitution modes and most prefix concerns.</span></span> <span data-ttu-id="cb0a3-306">執行專案只需要：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-306">An implementing project need only:</span></span>

* <span data-ttu-id="cb0a3-307">繼承自基類，並透過 `GetValue` 和 `GetAllValues`來執行索引鍵/值組的基本來源：</span><span class="sxs-lookup"><span data-stu-id="cb0a3-307">Inherit from the base class and implement a basic source of key/value pairs through the `GetValue` and `GetAllValues`:</span></span>
* <span data-ttu-id="cb0a3-308">將[configurationbuilders.ignoreloadfailure](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/)新增至專案。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-308">Add the [Microsoft.Configuration.ConfigurationBuilders.Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) to the project.</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

<span data-ttu-id="cb0a3-309">`KeyValueConfigBuilder` 基類在索引鍵/值設定產生器中提供許多工作和一致的行為。</span><span class="sxs-lookup"><span data-stu-id="cb0a3-309">The `KeyValueConfigBuilder` base class provides much of the work and consistent behavior across key/value configuration builders.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cb0a3-310">其他資源</span><span class="sxs-lookup"><span data-stu-id="cb0a3-310">Additional resources</span></span>

* [<span data-ttu-id="cb0a3-311">設定構建者 GitHub 存放庫</span><span class="sxs-lookup"><span data-stu-id="cb0a3-311">Configuration Builders GitHub repository</span></span>](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [<span data-ttu-id="cb0a3-312">使用 .NET Azure Key Vault 的服務對服務驗證</span><span class="sxs-lookup"><span data-stu-id="cb0a3-312">Service-to-service authentication to Azure Key Vault using .NET</span></span>](/azure/key-vault/service-to-service-authentication#connection-string-support)
