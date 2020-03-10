---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: ASP.NET Web API 中的 JSON 和 XML 序列化-ASP.NET 4。x
author: MikeWasson
description: 描述 ASP.NET 4.x 的 ASP.NET Web API 中的 JSON 和 XML 格式器。
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: 00fa07f00eabf7e6c883c5e9ceaf9a38a8f49605
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557467"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="7ae77-103">ASP.NET Web API 中的 JSON 和 XML 序列化</span><span class="sxs-lookup"><span data-stu-id="7ae77-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="7ae77-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7ae77-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="7ae77-105">本文說明 ASP.NET Web API 中的 JSON 和 XML 格式器。</span><span class="sxs-lookup"><span data-stu-id="7ae77-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="7ae77-106">在 ASP.NET Web API 中，*媒體類型格式*器是一個物件，可以：</span><span class="sxs-lookup"><span data-stu-id="7ae77-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="7ae77-107">從 HTTP 訊息內文讀取 CLR 物件</span><span class="sxs-lookup"><span data-stu-id="7ae77-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="7ae77-108">將 CLR 物件寫入 HTTP 訊息內文</span><span class="sxs-lookup"><span data-stu-id="7ae77-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="7ae77-109">Web API 提供適用于 JSON 和 XML 的媒體類型格式器。</span><span class="sxs-lookup"><span data-stu-id="7ae77-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="7ae77-110">根據預設，架構會將這些格式器插入管線中。</span><span class="sxs-lookup"><span data-stu-id="7ae77-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="7ae77-111">用戶端可以在 HTTP 要求的 Accept 標頭中要求 JSON 或 XML。</span><span class="sxs-lookup"><span data-stu-id="7ae77-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="7ae77-112">內容</span><span class="sxs-lookup"><span data-stu-id="7ae77-112">Contents</span></span>

- [<span data-ttu-id="7ae77-113">JSON 媒體類型格式器</span><span class="sxs-lookup"><span data-stu-id="7ae77-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="7ae77-114">唯讀屬性</span><span class="sxs-lookup"><span data-stu-id="7ae77-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="7ae77-115">時間</span><span class="sxs-lookup"><span data-stu-id="7ae77-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="7ae77-116">進來</span><span class="sxs-lookup"><span data-stu-id="7ae77-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="7ae77-117">Camel 大小寫</span><span class="sxs-lookup"><span data-stu-id="7ae77-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="7ae77-118">匿名和弱式類型物件</span><span class="sxs-lookup"><span data-stu-id="7ae77-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="7ae77-119">XML 媒體類型格式器</span><span class="sxs-lookup"><span data-stu-id="7ae77-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="7ae77-120">唯讀屬性</span><span class="sxs-lookup"><span data-stu-id="7ae77-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="7ae77-121">時間</span><span class="sxs-lookup"><span data-stu-id="7ae77-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="7ae77-122">進來</span><span class="sxs-lookup"><span data-stu-id="7ae77-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="7ae77-123">設定每一類型的 XML 序列化程式</span><span class="sxs-lookup"><span data-stu-id="7ae77-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="7ae77-124">移除 JSON 或 XML 格式器</span><span class="sxs-lookup"><span data-stu-id="7ae77-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="7ae77-125">處理迴圈物件參考</span><span class="sxs-lookup"><span data-stu-id="7ae77-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="7ae77-126">測試物件序列化</span><span class="sxs-lookup"><span data-stu-id="7ae77-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="7ae77-127">JSON 媒體類型格式器</span><span class="sxs-lookup"><span data-stu-id="7ae77-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="7ae77-128">JSON 格式是由**JsonMediaTypeFormatter**類別所提供。</span><span class="sxs-lookup"><span data-stu-id="7ae77-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="7ae77-129">根據預設， **JsonMediaTypeFormatter**會使用[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)程式庫來執行序列化。</span><span class="sxs-lookup"><span data-stu-id="7ae77-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="7ae77-130">Json.NET 是協力廠商的開放原始碼專案。</span><span class="sxs-lookup"><span data-stu-id="7ae77-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="7ae77-131">如果您想要的話，可以將**JsonMediaTypeFormatter**類別設定為使用**DataContractJsonSerializer** ，而不是 Json.NET。</span><span class="sxs-lookup"><span data-stu-id="7ae77-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="7ae77-132">若要這麼做，請將**UseDataContractJsonSerializer**屬性設定為**true**：</span><span class="sxs-lookup"><span data-stu-id="7ae77-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="7ae77-133">JSON 序列化</span><span class="sxs-lookup"><span data-stu-id="7ae77-133">JSON Serialization</span></span>

<span data-ttu-id="7ae77-134">本節說明 JSON 格式器的某些特定行為，並使用預設的[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)序列化程式。</span><span class="sxs-lookup"><span data-stu-id="7ae77-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="7ae77-135">這不是 Json.NET 程式庫的完整檔，如需詳細資訊，請參閱[Json.NET 檔](http://james.newtonking.com/projects/json/help/)。</span><span class="sxs-lookup"><span data-stu-id="7ae77-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="7ae77-136">會序列化哪些專案？</span><span class="sxs-lookup"><span data-stu-id="7ae77-136">What Gets Serialized?</span></span>

<span data-ttu-id="7ae77-137">根據預設，所有公用屬性和欄位都包含在序列化 JSON 中。</span><span class="sxs-lookup"><span data-stu-id="7ae77-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="7ae77-138">若要省略屬性或欄位，請使用**JsonIgnore**屬性加以裝飾。</span><span class="sxs-lookup"><span data-stu-id="7ae77-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="7ae77-139">如果您偏好 &quot;加入宣告&quot; 方法，請使用**DataContract**屬性來裝飾類別。</span><span class="sxs-lookup"><span data-stu-id="7ae77-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="7ae77-140">如果有這個屬性，除非成員具有**DataMember**，否則會忽略它們。</span><span class="sxs-lookup"><span data-stu-id="7ae77-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="7ae77-141">您也可以使用**DataMember**來序列化私用成員。</span><span class="sxs-lookup"><span data-stu-id="7ae77-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="7ae77-142">唯讀屬性</span><span class="sxs-lookup"><span data-stu-id="7ae77-142">Read-Only Properties</span></span>

<span data-ttu-id="7ae77-143">預設會序列化唯讀屬性。</span><span class="sxs-lookup"><span data-stu-id="7ae77-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="7ae77-144">日期</span><span class="sxs-lookup"><span data-stu-id="7ae77-144">Dates</span></span>

<span data-ttu-id="7ae77-145">根據預設，Json.NET 會以[ISO 8601](http://www.w3.org/TR/NOTE-datetime)格式寫入日期。</span><span class="sxs-lookup"><span data-stu-id="7ae77-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="7ae77-146">UTC 格式的日期（國際標準時間）是以 "Z" 後置字元撰寫。</span><span class="sxs-lookup"><span data-stu-id="7ae77-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="7ae77-147">當地時間的日期包含一個時區時差。</span><span class="sxs-lookup"><span data-stu-id="7ae77-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="7ae77-148">例如:</span><span class="sxs-lookup"><span data-stu-id="7ae77-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="7ae77-149">根據預設，Json.NET 會保留時區。</span><span class="sxs-lookup"><span data-stu-id="7ae77-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="7ae77-150">您可以藉由設定 DateTimeZoneHandling 屬性來覆寫此值：</span><span class="sxs-lookup"><span data-stu-id="7ae77-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="7ae77-151">如果您想要使用[MICROSOFT JSON 日期格式](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb)（`"\/Date(ticks)\/"`），而不是 ISO 8601，請設定序列化程式設定上的**DateFormatHandling**屬性：</span><span class="sxs-lookup"><span data-stu-id="7ae77-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="7ae77-152">縮排</span><span class="sxs-lookup"><span data-stu-id="7ae77-152">Indenting</span></span>

<span data-ttu-id="7ae77-153">若要寫入縮排的 JSON，請將**格式**設定設定為 [**格式化]。縮排**：</span><span class="sxs-lookup"><span data-stu-id="7ae77-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="7ae77-154">Camel 大小寫</span><span class="sxs-lookup"><span data-stu-id="7ae77-154">Camel Casing</span></span>

<span data-ttu-id="7ae77-155">若要以 camel 大小寫來撰寫 JSON 屬性名稱，而不變更您的資料模型，請在序列化程式上設定**CamelCasePropertyNamesContractResolver** ：</span><span class="sxs-lookup"><span data-stu-id="7ae77-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="7ae77-156">匿名和弱式類型物件</span><span class="sxs-lookup"><span data-stu-id="7ae77-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="7ae77-157">動作方法可以傳回匿名物件，並將它序列化為 JSON。</span><span class="sxs-lookup"><span data-stu-id="7ae77-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="7ae77-158">例如:</span><span class="sxs-lookup"><span data-stu-id="7ae77-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="7ae77-159">回應訊息主體會包含下列 JSON：</span><span class="sxs-lookup"><span data-stu-id="7ae77-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="7ae77-160">如果您的 Web API 從用戶端接收鬆散結構化的 JSON 物件，您可以將要求主體還原序列化為**Newtonsoft**類型。</span><span class="sxs-lookup"><span data-stu-id="7ae77-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="7ae77-161">不過，使用強型別資料物件通常是比較好的做法。</span><span class="sxs-lookup"><span data-stu-id="7ae77-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="7ae77-162">然後您不需要自行剖析資料，並獲得模型驗證的優點。</span><span class="sxs-lookup"><span data-stu-id="7ae77-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="7ae77-163">XML 序列化程式不支援匿名型別或**JObject**實例。</span><span class="sxs-lookup"><span data-stu-id="7ae77-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="7ae77-164">如果您針對 JSON 資料使用這些功能，您應該從管線中移除 XML 格式器，如本文稍後所述。</span><span class="sxs-lookup"><span data-stu-id="7ae77-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="7ae77-165">XML 媒體類型格式器</span><span class="sxs-lookup"><span data-stu-id="7ae77-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="7ae77-166">XML 格式是由**XmlMediaTypeFormatter**類別所提供。</span><span class="sxs-lookup"><span data-stu-id="7ae77-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="7ae77-167">根據預設， **XmlMediaTypeFormatter**會使用**DataContractSerializer**類別來執行序列化。</span><span class="sxs-lookup"><span data-stu-id="7ae77-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="7ae77-168">如果您想要的話，可以將**XmlMediaTypeFormatter**設定為使用**XmlSerializer** ，而不是**DataContractSerializer**。</span><span class="sxs-lookup"><span data-stu-id="7ae77-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="7ae77-169">若要這麼做，請將**UseXmlSerializer**屬性設定為**true**：</span><span class="sxs-lookup"><span data-stu-id="7ae77-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="7ae77-170">**XmlSerializer**類別支援比**DataContractSerializer**更窄的類型集合，但對產生的 XML 提供更多的控制權。</span><span class="sxs-lookup"><span data-stu-id="7ae77-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="7ae77-171">如果您需要符合現有的 XML 架構，請考慮使用**XmlSerializer** 。</span><span class="sxs-lookup"><span data-stu-id="7ae77-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="7ae77-172">XML 序列化</span><span class="sxs-lookup"><span data-stu-id="7ae77-172">XML Serialization</span></span>

<span data-ttu-id="7ae77-173">本節使用預設**DataContractSerializer**來描述 XML 格式器的某些特定行為。</span><span class="sxs-lookup"><span data-stu-id="7ae77-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="7ae77-174">根據預設，DataContractSerializer 的行為如下所示：</span><span class="sxs-lookup"><span data-stu-id="7ae77-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="7ae77-175">所有公用讀取/寫入屬性和欄位都會進行序列化。</span><span class="sxs-lookup"><span data-stu-id="7ae77-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="7ae77-176">若要省略屬性或欄位，請使用**IgnoreDataMember**屬性加以裝飾。</span><span class="sxs-lookup"><span data-stu-id="7ae77-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="7ae77-177">私用和受保護成員不會序列化。</span><span class="sxs-lookup"><span data-stu-id="7ae77-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="7ae77-178">唯讀屬性不會序列化。</span><span class="sxs-lookup"><span data-stu-id="7ae77-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="7ae77-179">（不過，唯讀集合屬性的內容會序列化）。</span><span class="sxs-lookup"><span data-stu-id="7ae77-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="7ae77-180">類別和成員名稱會以 XML 中的形式，與在類別宣告中所顯示的內容完全相同。</span><span class="sxs-lookup"><span data-stu-id="7ae77-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="7ae77-181">會使用預設的 XML 命名空間。</span><span class="sxs-lookup"><span data-stu-id="7ae77-181">A default XML namespace is used.</span></span>

<span data-ttu-id="7ae77-182">如果您需要更充分掌控序列化，您可以使用**DataContract**屬性來裝飾類別。</span><span class="sxs-lookup"><span data-stu-id="7ae77-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="7ae77-183">當這個屬性存在時，類別會序列化如下：</span><span class="sxs-lookup"><span data-stu-id="7ae77-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="7ae77-184">&quot;加入宣告&quot; 方法：預設不會序列化屬性和欄位。</span><span class="sxs-lookup"><span data-stu-id="7ae77-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="7ae77-185">若要序列化屬性或欄位，請使用**DataMember**屬性來裝飾它。</span><span class="sxs-lookup"><span data-stu-id="7ae77-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="7ae77-186">若要序列化私用或受保護的成員，請使用**DataMember**屬性來裝飾它。</span><span class="sxs-lookup"><span data-stu-id="7ae77-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="7ae77-187">唯讀屬性不會序列化。</span><span class="sxs-lookup"><span data-stu-id="7ae77-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="7ae77-188">若要變更類別名稱在 XML 中的顯示方式，請在**DataContract**屬性中設定*name*參數。</span><span class="sxs-lookup"><span data-stu-id="7ae77-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="7ae77-189">若要變更成員名稱在 XML 中的顯示方式，請在**DataMember**屬性中設定*name*參數。</span><span class="sxs-lookup"><span data-stu-id="7ae77-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="7ae77-190">若要變更 XML 命名空間，請在**DataContract**類別中設定*namespace*參數。</span><span class="sxs-lookup"><span data-stu-id="7ae77-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="7ae77-191">唯讀屬性</span><span class="sxs-lookup"><span data-stu-id="7ae77-191">Read-Only Properties</span></span>

<span data-ttu-id="7ae77-192">唯讀屬性不會序列化。</span><span class="sxs-lookup"><span data-stu-id="7ae77-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="7ae77-193">如果唯讀屬性具有支援的私用欄位，您可以使用**DataMember**屬性來標記私用欄位。</span><span class="sxs-lookup"><span data-stu-id="7ae77-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="7ae77-194">這個方法需要類別上的**DataContract**屬性。</span><span class="sxs-lookup"><span data-stu-id="7ae77-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="7ae77-195">日期</span><span class="sxs-lookup"><span data-stu-id="7ae77-195">Dates</span></span>

<span data-ttu-id="7ae77-196">日期是以 ISO 8601 格式撰寫。</span><span class="sxs-lookup"><span data-stu-id="7ae77-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="7ae77-197">例如，&quot;2012-05-23T20：21： 37.9116538 Z&quot;。</span><span class="sxs-lookup"><span data-stu-id="7ae77-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="7ae77-198">縮排</span><span class="sxs-lookup"><span data-stu-id="7ae77-198">Indenting</span></span>

<span data-ttu-id="7ae77-199">若要寫入縮排的 XML，請將 [**縮排**] 屬性設定為**true**：</span><span class="sxs-lookup"><span data-stu-id="7ae77-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="7ae77-200">設定每一類型的 XML 序列化程式</span><span class="sxs-lookup"><span data-stu-id="7ae77-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="7ae77-201">您可以針對不同的 CLR 類型設定不同的 XML 序列化程式。</span><span class="sxs-lookup"><span data-stu-id="7ae77-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="7ae77-202">例如，您可能有需要**XmlSerializer**以提供回溯相容性的特定資料物件。</span><span class="sxs-lookup"><span data-stu-id="7ae77-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="7ae77-203">您可以針對此物件使用**XmlSerializer** ，並繼續使用其他類型的**DataContractSerializer** 。</span><span class="sxs-lookup"><span data-stu-id="7ae77-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="7ae77-204">若要設定特定類型的 XML 序列化程式，請呼叫**SetSerializer**。</span><span class="sxs-lookup"><span data-stu-id="7ae77-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="7ae77-205">您可以指定**XmlSerializer**或任何衍生自**XmlObjectSerializer**的物件。</span><span class="sxs-lookup"><span data-stu-id="7ae77-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="7ae77-206">移除 JSON 或 XML 格式器</span><span class="sxs-lookup"><span data-stu-id="7ae77-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="7ae77-207">如果您不想要使用，您可以從格式器清單中移除 JSON 格式器或 XML 格式器。</span><span class="sxs-lookup"><span data-stu-id="7ae77-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="7ae77-208">執行此動作的主要原因包括：</span><span class="sxs-lookup"><span data-stu-id="7ae77-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="7ae77-209">將您的 Web API 回應限制為特定的媒體類型。</span><span class="sxs-lookup"><span data-stu-id="7ae77-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="7ae77-210">例如，您可能會決定僅支援 JSON 回應，並移除 XML 格式器。</span><span class="sxs-lookup"><span data-stu-id="7ae77-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="7ae77-211">以自訂格式器取代預設格式器。</span><span class="sxs-lookup"><span data-stu-id="7ae77-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="7ae77-212">例如，您可以使用 JSON 格式器的自訂執行來取代 JSON 格式器。</span><span class="sxs-lookup"><span data-stu-id="7ae77-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="7ae77-213">下列程式碼顯示如何移除預設的格式器。</span><span class="sxs-lookup"><span data-stu-id="7ae77-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="7ae77-214">從您的應用程式呼叫此項， **\_啟動**方法（定義于 global.asax 中）。</span><span class="sxs-lookup"><span data-stu-id="7ae77-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="7ae77-215">處理迴圈物件參考</span><span class="sxs-lookup"><span data-stu-id="7ae77-215">Handling Circular Object References</span></span>

<span data-ttu-id="7ae77-216">根據預設，JSON 和 XML 格式器會將所有物件寫入為值。</span><span class="sxs-lookup"><span data-stu-id="7ae77-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="7ae77-217">如果兩個屬性都參考相同的物件，或如果相同的物件在集合中出現兩次，則格式器會將物件序列化兩次。</span><span class="sxs-lookup"><span data-stu-id="7ae77-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="7ae77-218">如果您的物件圖形包含迴圈，這是一個特別的問題，因為當序列化程式在圖形中偵測到迴圈時，將會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7ae77-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="7ae77-219">請考慮下列物件模型和控制器。</span><span class="sxs-lookup"><span data-stu-id="7ae77-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="7ae77-220">叫用此動作會導致格式器擲回例外狀況，這會轉譯為用戶端的狀態碼500（內部伺服器錯誤）回應。</span><span class="sxs-lookup"><span data-stu-id="7ae77-220">Invoking this action will cause the formatter to thrown an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="7ae77-221">若要保留 JSON 中的物件參考，請將下列程式碼新增至 global.asax 檔案中的**Application\_Start**方法：</span><span class="sxs-lookup"><span data-stu-id="7ae77-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="7ae77-222">現在控制器動作會傳回 JSON，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7ae77-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="7ae77-223">請注意，序列化程式會將 &quot;$id&quot; 屬性新增至這兩個物件。</span><span class="sxs-lookup"><span data-stu-id="7ae77-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="7ae77-224">此外，它會偵測 Employee. 部門屬性會建立迴圈，因此它會將值取代為物件參考： {&quot;$ref&quot;：&quot;1&quot;}。</span><span class="sxs-lookup"><span data-stu-id="7ae77-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="7ae77-225">物件參考在 JSON 中不是標準。</span><span class="sxs-lookup"><span data-stu-id="7ae77-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="7ae77-226">使用這項功能之前，請考慮您的用戶端是否能夠剖析結果。</span><span class="sxs-lookup"><span data-stu-id="7ae77-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="7ae77-227">最好是從圖表中移除迴圈。</span><span class="sxs-lookup"><span data-stu-id="7ae77-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="7ae77-228">例如，在此範例中，從員工到部門的連結並不是真的必要的。</span><span class="sxs-lookup"><span data-stu-id="7ae77-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>

<span data-ttu-id="7ae77-229">若要在 XML 中保留物件參考，您有兩個選項。</span><span class="sxs-lookup"><span data-stu-id="7ae77-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="7ae77-230">較簡單的選項是將 `[DataContract(IsReference=true)]` 新增至您的模型類別。</span><span class="sxs-lookup"><span data-stu-id="7ae77-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="7ae77-231">*IsReference*參數會啟用物件參考。</span><span class="sxs-lookup"><span data-stu-id="7ae77-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="7ae77-232">請記住， **DataContract**會加入宣告序列化，因此您也需要將**DataMember**屬性新增至屬性：</span><span class="sxs-lookup"><span data-stu-id="7ae77-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="7ae77-233">現在，格式器會產生類似下列的 XML：</span><span class="sxs-lookup"><span data-stu-id="7ae77-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="7ae77-234">如果您想要避免模型類別上的屬性，還有另一個選項：建立新的類型特定**DataContractSerializer**實例，並在此函式中將*帶有 preserveobjectreferences*設定為**true** 。</span><span class="sxs-lookup"><span data-stu-id="7ae77-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="7ae77-235">然後，將此實例設定為 XML 媒體類型格式器上的每個類型序列化程式。</span><span class="sxs-lookup"><span data-stu-id="7ae77-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="7ae77-236">下列程式碼示範如何執行這項操作：</span><span class="sxs-lookup"><span data-stu-id="7ae77-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="7ae77-237">測試物件序列化</span><span class="sxs-lookup"><span data-stu-id="7ae77-237">Testing Object Serialization</span></span>

<span data-ttu-id="7ae77-238">當您設計 Web API 時，測試資料物件的序列化方式會很有説明。</span><span class="sxs-lookup"><span data-stu-id="7ae77-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="7ae77-239">您不需要建立控制器或叫用控制器動作，就可以這樣做。</span><span class="sxs-lookup"><span data-stu-id="7ae77-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
