---
title: ASP.NET Core 中的核心加密擴充性
author: rick-anderson
description: 深入了解 IAuthenticatedEncryptor、 IAuthenticatedEncryptorDescriptor、 IAuthenticatedEncryptorDescriptorDeserializer 和最上層的 factory。
ms.author: riande
ms.date: 8/11/2017
uid: security/data-protection/extensibility/core-crypto
ms.openlocfilehash: 47432cfefe0a52c9f815d717f7269ec68fdb6af3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036175"
---
# <a name="core-cryptography-extensibility-in-aspnet-core"></a><span data-ttu-id="98f42-103">ASP.NET Core 中的核心加密擴充性</span><span class="sxs-lookup"><span data-stu-id="98f42-103">Core cryptography extensibility in ASP.NET Core</span></span>

<a name="data-protection-extensibility-core-crypto"></a>

>[!WARNING]
> <span data-ttu-id="98f42-104">會實作下列介面的任何的類型應該是安全執行緒的多個呼叫端。</span><span class="sxs-lookup"><span data-stu-id="98f42-104">Types that implement any of the following interfaces should be thread-safe for multiple callers.</span></span>

<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptor"></a>

## <a name="iauthenticatedencryptor"></a><span data-ttu-id="98f42-105">IAuthenticatedEncryptor</span><span class="sxs-lookup"><span data-stu-id="98f42-105">IAuthenticatedEncryptor</span></span>

<span data-ttu-id="98f42-106">**IAuthenticatedEncryptor**介面是密碼編譯子系統基本建置組塊。</span><span class="sxs-lookup"><span data-stu-id="98f42-106">The **IAuthenticatedEncryptor** interface is the basic building block of the cryptographic subsystem.</span></span> <span data-ttu-id="98f42-107">通常是每個索引鍵，一個 IAuthenticatedEncryptor 和 IAuthenticatedEncryptor 執行個體包裝所有密碼編譯金鑰資料和執行密碼編譯作業所需的演算法資訊。</span><span class="sxs-lookup"><span data-stu-id="98f42-107">There's generally one IAuthenticatedEncryptor per key, and the IAuthenticatedEncryptor instance wraps all cryptographic key material and algorithmic information necessary to perform cryptographic operations.</span></span>

<span data-ttu-id="98f42-108">正如其名，此類型為負責提供已驗證的加密和解密服務。</span><span class="sxs-lookup"><span data-stu-id="98f42-108">As its name suggests, the type is responsible for providing authenticated encryption and decryption services.</span></span> <span data-ttu-id="98f42-109">它會公開下列兩個 Api。</span><span class="sxs-lookup"><span data-stu-id="98f42-109">It exposes the following two APIs.</span></span>

* <span data-ttu-id="98f42-110">Decrypt(ArraySegment<byte> ciphertext, ArraySegment<byte> additionalAuthenticatedData) : byte[]</span><span class="sxs-lookup"><span data-stu-id="98f42-110">Decrypt(ArraySegment<byte> ciphertext, ArraySegment<byte> additionalAuthenticatedData) : byte[]</span></span>

* <span data-ttu-id="98f42-111">Encrypt(ArraySegment<byte> plaintext, ArraySegment<byte> additionalAuthenticatedData) : byte[]</span><span class="sxs-lookup"><span data-stu-id="98f42-111">Encrypt(ArraySegment<byte> plaintext, ArraySegment<byte> additionalAuthenticatedData) : byte[]</span></span>

<span data-ttu-id="98f42-112">加密方法會傳回包含已譯成密碼的純文字，以及驗證標籤的 blob。</span><span class="sxs-lookup"><span data-stu-id="98f42-112">The Encrypt method returns a blob that includes the enciphered plaintext and an authentication tag.</span></span> <span data-ttu-id="98f42-113">驗證標記必須包含額外的驗證的資料 (AAD)，但不是可復原的最後一個裝載從 AAD 自身。</span><span class="sxs-lookup"><span data-stu-id="98f42-113">The authentication tag must encompass the additional authenticated data (AAD), though the AAD itself need not be recoverable from the final payload.</span></span> <span data-ttu-id="98f42-114">解密方法驗證的驗證標籤，並傳回被破解的承載。</span><span class="sxs-lookup"><span data-stu-id="98f42-114">The Decrypt method validates the authentication tag and returns the deciphered payload.</span></span> <span data-ttu-id="98f42-115">所有失敗 （不含 ArgumentNullException 和類似） 應該都 homogenized CryptographicException 到。</span><span class="sxs-lookup"><span data-stu-id="98f42-115">All failures (except ArgumentNullException and similar) should be homogenized to CryptographicException.</span></span>

> [!NOTE]
> <span data-ttu-id="98f42-116">IAuthenticatedEncryptor 執行個體本身實際上並不需要包含金鑰資料。</span><span class="sxs-lookup"><span data-stu-id="98f42-116">The IAuthenticatedEncryptor instance itself doesn't actually need to contain the key material.</span></span> <span data-ttu-id="98f42-117">比方說，實作可以委派給 HSM 的所有作業。</span><span class="sxs-lookup"><span data-stu-id="98f42-117">For example, the implementation could delegate to an HSM for all operations.</span></span>

<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptorfactory"></a>
<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor"></a>

## <a name="how-to-create-an-iauthenticatedencryptor"></a><span data-ttu-id="98f42-118">如何建立 IAuthenticatedEncryptor</span><span class="sxs-lookup"><span data-stu-id="98f42-118">How to create an IAuthenticatedEncryptor</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="98f42-119">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="98f42-119">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="98f42-120">**IAuthenticatedEncryptorFactory**介面代表一種類型，知道如何建立[IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor)執行個體。</span><span class="sxs-lookup"><span data-stu-id="98f42-120">The **IAuthenticatedEncryptorFactory** interface represents a type that knows how to create an [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) instance.</span></span> <span data-ttu-id="98f42-121">它的 API 如下所示。</span><span class="sxs-lookup"><span data-stu-id="98f42-121">Its API is as follows.</span></span>

* <span data-ttu-id="98f42-122">CreateEncryptorInstance （IKey 索引鍵）：IAuthenticatedEncryptor</span><span class="sxs-lookup"><span data-stu-id="98f42-122">CreateEncryptorInstance(IKey key) : IAuthenticatedEncryptor</span></span>

<span data-ttu-id="98f42-123">對於任何給定的 IKey 執行個體，其 CreateEncryptorInstance 方法所建立的任何已驗證的加密程式應視為相等，如下列程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="98f42-123">For any given IKey instance, any authenticated encryptors created by its CreateEncryptorInstance method should be considered equivalent, as in the below code sample.</span></span>

```csharp
// we have an IAuthenticatedEncryptorFactory instance and an IKey instance
IAuthenticatedEncryptorFactory factory = ...;
IKey key = ...;

// get an encryptor instance and perform an authenticated encryption operation
ArraySegment<byte> plaintext = new ArraySegment<byte>(Encoding.UTF8.GetBytes("plaintext"));
ArraySegment<byte> aad = new ArraySegment<byte>(Encoding.UTF8.GetBytes("AAD"));
var encryptor1 = factory.CreateEncryptorInstance(key);
byte[] ciphertext = encryptor1.Encrypt(plaintext, aad);

// get another encryptor instance and perform an authenticated decryption operation
var encryptor2 = factory.CreateEncryptorInstance(key);
byte[] roundTripped = encryptor2.Decrypt(new ArraySegment<byte>(ciphertext), aad);


// the 'roundTripped' and 'plaintext' buffers should be equivalent
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="98f42-124">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="98f42-124">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="98f42-125">**IAuthenticatedEncryptorDescriptor**介面代表一種類型，知道如何建立[IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor)執行個體。</span><span class="sxs-lookup"><span data-stu-id="98f42-125">The **IAuthenticatedEncryptorDescriptor** interface represents a type that knows how to create an [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) instance.</span></span> <span data-ttu-id="98f42-126">它的 API 如下所示。</span><span class="sxs-lookup"><span data-stu-id="98f42-126">Its API is as follows.</span></span>

* <span data-ttu-id="98f42-127">CreateEncryptorInstance():IAuthenticatedEncryptor</span><span class="sxs-lookup"><span data-stu-id="98f42-127">CreateEncryptorInstance() : IAuthenticatedEncryptor</span></span>

* <span data-ttu-id="98f42-128">ExportToXml():XmlSerializedDescriptorInfo</span><span class="sxs-lookup"><span data-stu-id="98f42-128">ExportToXml() : XmlSerializedDescriptorInfo</span></span>

<span data-ttu-id="98f42-129">IAuthenticatedEncryptor，例如假設 IAuthenticatedEncryptorDescriptor 的執行個體包裝一個特定的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="98f42-129">Like IAuthenticatedEncryptor, an instance of IAuthenticatedEncryptorDescriptor is assumed to wrap one specific key.</span></span> <span data-ttu-id="98f42-130">這表示，對於任何給定的 IAuthenticatedEncryptorDescriptor 執行個體，其 CreateEncryptorInstance 方法所建立的任何已驗證的加密程式應視為相等，如下列程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="98f42-130">This means that for any given IAuthenticatedEncryptorDescriptor instance, any authenticated encryptors created by its CreateEncryptorInstance method should be considered equivalent, as in the below code sample.</span></span>

```csharp
// we have an IAuthenticatedEncryptorDescriptor instance
IAuthenticatedEncryptorDescriptor descriptor = ...;

// get an encryptor instance and perform an authenticated encryption operation
ArraySegment<byte> plaintext = new ArraySegment<byte>(Encoding.UTF8.GetBytes("plaintext"));
ArraySegment<byte> aad = new ArraySegment<byte>(Encoding.UTF8.GetBytes("AAD"));
var encryptor1 = descriptor.CreateEncryptorInstance();
byte[] ciphertext = encryptor1.Encrypt(plaintext, aad);

// get another encryptor instance and perform an authenticated decryption operation
var encryptor2 = descriptor.CreateEncryptorInstance();
byte[] roundTripped = encryptor2.Decrypt(new ArraySegment<byte>(ciphertext), aad);


// the 'roundTripped' and 'plaintext' buffers should be equivalent
```

---

<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor"></a>

## <a name="iauthenticatedencryptordescriptor-aspnet-core-2x-only"></a><span data-ttu-id="98f42-131">IAuthenticatedEncryptorDescriptor (ASP.NET Core 僅限 2.x)</span><span class="sxs-lookup"><span data-stu-id="98f42-131">IAuthenticatedEncryptorDescriptor (ASP.NET Core 2.x only)</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="98f42-132">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="98f42-132">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="98f42-133">**IAuthenticatedEncryptorDescriptor**介面代表知道如何將本身匯出到 XML 的型別。</span><span class="sxs-lookup"><span data-stu-id="98f42-133">The **IAuthenticatedEncryptorDescriptor** interface represents a type that knows how to export itself to XML.</span></span> <span data-ttu-id="98f42-134">它的 API 如下所示。</span><span class="sxs-lookup"><span data-stu-id="98f42-134">Its API is as follows.</span></span>

* <span data-ttu-id="98f42-135">ExportToXml():XmlSerializedDescriptorInfo</span><span class="sxs-lookup"><span data-stu-id="98f42-135">ExportToXml() : XmlSerializedDescriptorInfo</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="98f42-136">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="98f42-136">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

---

## <a name="xml-serialization"></a><span data-ttu-id="98f42-137">XML 序列化</span><span class="sxs-lookup"><span data-stu-id="98f42-137">XML Serialization</span></span>

<span data-ttu-id="98f42-138">IAuthenticatedEncryptor 和 IAuthenticatedEncryptorDescriptor 的主要差異在於描述元知道如何建立加密程式，並提供有效的引數。</span><span class="sxs-lookup"><span data-stu-id="98f42-138">The primary difference between IAuthenticatedEncryptor and IAuthenticatedEncryptorDescriptor is that the descriptor knows how to create the encryptor and supply it with valid arguments.</span></span> <span data-ttu-id="98f42-139">請考慮其實作依賴 SymmetricAlgorithm 和 KeyedHashAlgorithm IAuthenticatedEncryptor。</span><span class="sxs-lookup"><span data-stu-id="98f42-139">Consider an IAuthenticatedEncryptor whose implementation relies on SymmetricAlgorithm and KeyedHashAlgorithm.</span></span> <span data-ttu-id="98f42-140">加密程式的工作就是要使用這些類型，但它並不一定知道這些型別來自何處，因此它無法真正會寫出適當描述如何重新建立本身的應用程式重新啟動時。</span><span class="sxs-lookup"><span data-stu-id="98f42-140">The encryptor's job is to consume these types, but it doesn't necessarily know where these types came from, so it can't really write out a proper description of how to recreate itself if the application restarts.</span></span> <span data-ttu-id="98f42-141">描述元做為較高的層級，在這個基礎之上。</span><span class="sxs-lookup"><span data-stu-id="98f42-141">The descriptor acts as a higher level on top of this.</span></span> <span data-ttu-id="98f42-142">由於描述項會知道如何建立加密程式執行個體 （例如，它知道如何建立必要的演算法），以便可以重新建立加密程式執行個體，應用程式重設之後，它可以序列化 XML 表單中的知識。</span><span class="sxs-lookup"><span data-stu-id="98f42-142">Since the descriptor knows how to create the encryptor instance (e.g., it knows how to create the required algorithms), it can serialize that knowledge in XML form so that the encryptor instance can be recreated after an application reset.</span></span>

<a name="data-protection-extensibility-core-crypto-exporttoxml"></a>

<span data-ttu-id="98f42-143">描述元可以透過其 ExportToXml 常式進行序列化。</span><span class="sxs-lookup"><span data-stu-id="98f42-143">The descriptor can be serialized via its ExportToXml routine.</span></span> <span data-ttu-id="98f42-144">此常式會傳回包含兩個屬性 XmlSerializedDescriptorInfo: 描述項和其代表的型別 XElement 表示法[IAuthenticatedEncryptorDescriptorDeserializer](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptordeserializer)可以是用來重新啟動指定對應的 XElement 這個描述元。</span><span class="sxs-lookup"><span data-stu-id="98f42-144">This routine returns an XmlSerializedDescriptorInfo which contains two properties: the XElement representation of the descriptor and the Type which represents an [IAuthenticatedEncryptorDescriptorDeserializer](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptordeserializer) which can be used to resurrect this descriptor given the corresponding XElement.</span></span>

<span data-ttu-id="98f42-145">序列化的描述項可能包含機密資訊，例如密碼編譯金鑰的內容。</span><span class="sxs-lookup"><span data-stu-id="98f42-145">The serialized descriptor may contain sensitive information such as cryptographic key material.</span></span> <span data-ttu-id="98f42-146">資料保護系統的內建支援已保存至儲存體之前加密資訊。</span><span class="sxs-lookup"><span data-stu-id="98f42-146">The data protection system has built-in support for encrypting information before it's persisted to storage.</span></span> <span data-ttu-id="98f42-147">若要利用這個，描述元應該標記包含機密資訊與屬性名稱"requiresEncryption"元素 (xmlns"<http://schemas.asp.net/2015/03/dataProtection>」)，值"true"。</span><span class="sxs-lookup"><span data-stu-id="98f42-147">To take advantage of this, the descriptor should mark the element which contains sensitive information with the attribute name "requiresEncryption" (xmlns "<http://schemas.asp.net/2015/03/dataProtection>"), value "true".</span></span>

>[!TIP]
> <span data-ttu-id="98f42-148">沒有設定這個屬性的協助程式 API。</span><span class="sxs-lookup"><span data-stu-id="98f42-148">There's a helper API for setting this attribute.</span></span> <span data-ttu-id="98f42-149">呼叫 XElement.MarkAsRequiresEncryption() 位於命名空間 Microsoft.AspNetCore.DataProtection.AuthenticatedEncryption.ConfigurationModel; 擴充方法。</span><span class="sxs-lookup"><span data-stu-id="98f42-149">Call the extension method XElement.MarkAsRequiresEncryption() located in namespace Microsoft.AspNetCore.DataProtection.AuthenticatedEncryption.ConfigurationModel.</span></span>

<span data-ttu-id="98f42-150">也可以序列化的描述元其中不包含機密資訊的情況。</span><span class="sxs-lookup"><span data-stu-id="98f42-150">There can also be cases where the serialized descriptor doesn't contain sensitive information.</span></span> <span data-ttu-id="98f42-151">請再次考量 HSM 中所儲存的密碼編譯金鑰的大小寫。</span><span class="sxs-lookup"><span data-stu-id="98f42-151">Consider again the case of a cryptographic key stored in an HSM.</span></span> <span data-ttu-id="98f42-152">序列化本身，因為 HSM 不會公開純文字形式的資料時，無法寫入出金鑰的內容描述元。</span><span class="sxs-lookup"><span data-stu-id="98f42-152">The descriptor cannot write out the key material when serializing itself since the HSM won't expose the material in plaintext form.</span></span> <span data-ttu-id="98f42-153">相反地，描述項可能撰寫出的金鑰包裝版本 （如果 HSM 會允許匯出，以這種方式） 的索引鍵或索引鍵的 HSM 自己的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="98f42-153">Instead, the descriptor might write out the key-wrapped version of the key (if the HSM allows export in this fashion) or the HSM's own unique identifier for the key.</span></span>

<a name="data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptordeserializer"></a>

## <a name="iauthenticatedencryptordescriptordeserializer"></a><span data-ttu-id="98f42-154">IAuthenticatedEncryptorDescriptorDeserializer</span><span class="sxs-lookup"><span data-stu-id="98f42-154">IAuthenticatedEncryptorDescriptorDeserializer</span></span>

<span data-ttu-id="98f42-155">**IAuthenticatedEncryptorDescriptorDeserializer**介面代表知道如何還原序列化從 XElement IAuthenticatedEncryptorDescriptor 執行個體的型別。</span><span class="sxs-lookup"><span data-stu-id="98f42-155">The **IAuthenticatedEncryptorDescriptorDeserializer** interface represents a type that knows how to deserialize an IAuthenticatedEncryptorDescriptor instance from an XElement.</span></span> <span data-ttu-id="98f42-156">它會公開單一方法：</span><span class="sxs-lookup"><span data-stu-id="98f42-156">It exposes a single method:</span></span>

* <span data-ttu-id="98f42-157">ImportFromXml （XElement 項目）：IAuthenticatedEncryptorDescriptor</span><span class="sxs-lookup"><span data-stu-id="98f42-157">ImportFromXml(XElement element) : IAuthenticatedEncryptorDescriptor</span></span>

<span data-ttu-id="98f42-158">ImportFromXml 方法會傳回的 XElement [IAuthenticatedEncryptorDescriptor.ExportToXml](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-exporttoxml)並建立原始 IAuthenticatedEncryptorDescriptor 的對等項目。</span><span class="sxs-lookup"><span data-stu-id="98f42-158">The ImportFromXml method takes the XElement that was returned by [IAuthenticatedEncryptorDescriptor.ExportToXml](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-exporttoxml) and creates an equivalent of the original IAuthenticatedEncryptorDescriptor.</span></span>

<span data-ttu-id="98f42-159">實作 IAuthenticatedEncryptorDescriptorDeserializer 類型應該有下列兩個公用建構函式的其中一個：</span><span class="sxs-lookup"><span data-stu-id="98f42-159">Types which implement IAuthenticatedEncryptorDescriptorDeserializer should have one of the following two public constructors:</span></span>

* <span data-ttu-id="98f42-160">.ctor(IServiceProvider)</span><span class="sxs-lookup"><span data-stu-id="98f42-160">.ctor(IServiceProvider)</span></span>

* <span data-ttu-id="98f42-161">.ctor()</span><span class="sxs-lookup"><span data-stu-id="98f42-161">.ctor()</span></span>

> [!NOTE]
> <span data-ttu-id="98f42-162">傳遞至建構函式的 IServiceProvider 可能是 null。</span><span class="sxs-lookup"><span data-stu-id="98f42-162">The IServiceProvider passed to the constructor may be null.</span></span>

## <a name="the-top-level-factory"></a><span data-ttu-id="98f42-163">最上層的處理站</span><span class="sxs-lookup"><span data-stu-id="98f42-163">The top-level factory</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="98f42-164">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="98f42-164">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="98f42-165">**AlgorithmConfiguration**類別代表知道如何建立的型別[IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor)執行個體。</span><span class="sxs-lookup"><span data-stu-id="98f42-165">The **AlgorithmConfiguration** class represents a type which knows how to create [IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor) instances.</span></span> <span data-ttu-id="98f42-166">它會公開單一的 API。</span><span class="sxs-lookup"><span data-stu-id="98f42-166">It exposes a single API.</span></span>

* <span data-ttu-id="98f42-167">CreateNewDescriptor():IAuthenticatedEncryptorDescriptor</span><span class="sxs-lookup"><span data-stu-id="98f42-167">CreateNewDescriptor() : IAuthenticatedEncryptorDescriptor</span></span>

<span data-ttu-id="98f42-168">您可以將 AlgorithmConfiguration 想像成最上層的 factory。</span><span class="sxs-lookup"><span data-stu-id="98f42-168">Think of AlgorithmConfiguration as the top-level factory.</span></span> <span data-ttu-id="98f42-169">設定做為範本。</span><span class="sxs-lookup"><span data-stu-id="98f42-169">The configuration serves as a template.</span></span> <span data-ttu-id="98f42-170">它會包裝演算法的資訊 （例如，此組態會產生使用 AES-128-GCM 主要金鑰的描述項），但它尚未與特定索引鍵相關聯。</span><span class="sxs-lookup"><span data-stu-id="98f42-170">It wraps algorithmic information (e.g., this configuration produces descriptors with an AES-128-GCM master key), but it's not yet associated with a specific key.</span></span>

<span data-ttu-id="98f42-171">當 CreateNewDescriptor 稱為，全新的金鑰內容會建立僅供此呼叫，而且會產生新的 IAuthenticatedEncryptorDescriptor 包裝此金鑰的資料和取用資料所需的演算法資訊。</span><span class="sxs-lookup"><span data-stu-id="98f42-171">When CreateNewDescriptor is called, fresh key material is created solely for this call, and a new IAuthenticatedEncryptorDescriptor is produced which wraps this key material and the algorithmic information required to consume the material.</span></span> <span data-ttu-id="98f42-172">金鑰的內容可能會在軟體中建立 （和保留在記憶體中），所以無法建立且內含 HSM，依此類推。</span><span class="sxs-lookup"><span data-stu-id="98f42-172">The key material could be created in software (and held in memory), it could be created and held within an HSM, and so on.</span></span> <span data-ttu-id="98f42-173">重點是，CreateNewDescriptor 任何兩個呼叫應該永遠不會建立對等的 IAuthenticatedEncryptorDescriptor 執行個體。</span><span class="sxs-lookup"><span data-stu-id="98f42-173">The crucial point is that any two calls to CreateNewDescriptor should never create equivalent IAuthenticatedEncryptorDescriptor instances.</span></span>

<span data-ttu-id="98f42-174">AlgorithmConfiguration 類型做為索引鍵建立常式的進入點這類[自動金鑰輪換](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling)。</span><span class="sxs-lookup"><span data-stu-id="98f42-174">The AlgorithmConfiguration type serves as the entry point for key creation routines such as [automatic key rolling](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling).</span></span> <span data-ttu-id="98f42-175">若要變更的所有未來的索引鍵的實作，請在 KeyManagementOptions 中設定 AuthenticatedEncryptorConfiguration 屬性。</span><span class="sxs-lookup"><span data-stu-id="98f42-175">To change the implementation for all future keys, set the AuthenticatedEncryptorConfiguration property in KeyManagementOptions.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="98f42-176">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="98f42-176">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="98f42-177">**IAuthenticatedEncryptorConfiguration**介面代表知道如何建立的型別[IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor)執行個體。</span><span class="sxs-lookup"><span data-stu-id="98f42-177">The **IAuthenticatedEncryptorConfiguration** interface represents a type which knows how to create [IAuthenticatedEncryptorDescriptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptordescriptor) instances.</span></span> <span data-ttu-id="98f42-178">它會公開單一的 API。</span><span class="sxs-lookup"><span data-stu-id="98f42-178">It exposes a single API.</span></span>

* <span data-ttu-id="98f42-179">CreateNewDescriptor():IAuthenticatedEncryptorDescriptor</span><span class="sxs-lookup"><span data-stu-id="98f42-179">CreateNewDescriptor() : IAuthenticatedEncryptorDescriptor</span></span>

<span data-ttu-id="98f42-180">您可以將 IAuthenticatedEncryptorConfiguration 想像成最上層的 factory。</span><span class="sxs-lookup"><span data-stu-id="98f42-180">Think of IAuthenticatedEncryptorConfiguration as the top-level factory.</span></span> <span data-ttu-id="98f42-181">設定做為範本。</span><span class="sxs-lookup"><span data-stu-id="98f42-181">The configuration serves as a template.</span></span> <span data-ttu-id="98f42-182">它會包裝演算法的資訊 （例如，此組態會產生使用 AES-128-GCM 主要金鑰的描述項），但它尚未與特定索引鍵相關聯。</span><span class="sxs-lookup"><span data-stu-id="98f42-182">It wraps algorithmic information (e.g., this configuration produces descriptors with an AES-128-GCM master key), but it's not yet associated with a specific key.</span></span>

<span data-ttu-id="98f42-183">當 CreateNewDescriptor 稱為，全新的金鑰內容會建立僅供此呼叫，而且會產生新的 IAuthenticatedEncryptorDescriptor 包裝此金鑰的資料和取用資料所需的演算法資訊。</span><span class="sxs-lookup"><span data-stu-id="98f42-183">When CreateNewDescriptor is called, fresh key material is created solely for this call, and a new IAuthenticatedEncryptorDescriptor is produced which wraps this key material and the algorithmic information required to consume the material.</span></span> <span data-ttu-id="98f42-184">金鑰的內容可能會在軟體中建立 （和保留在記憶體中），所以無法建立且內含 HSM，依此類推。</span><span class="sxs-lookup"><span data-stu-id="98f42-184">The key material could be created in software (and held in memory), it could be created and held within an HSM, and so on.</span></span> <span data-ttu-id="98f42-185">重點是，CreateNewDescriptor 任何兩個呼叫應該永遠不會建立對等的 IAuthenticatedEncryptorDescriptor 執行個體。</span><span class="sxs-lookup"><span data-stu-id="98f42-185">The crucial point is that any two calls to CreateNewDescriptor should never create equivalent IAuthenticatedEncryptorDescriptor instances.</span></span>

<span data-ttu-id="98f42-186">IAuthenticatedEncryptorConfiguration 類型做為索引鍵建立常式的進入點這類[自動金鑰輪換](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling)。</span><span class="sxs-lookup"><span data-stu-id="98f42-186">The IAuthenticatedEncryptorConfiguration type serves as the entry point for key creation routines such as [automatic key rolling](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling).</span></span> <span data-ttu-id="98f42-187">若要變更的所有未來的索引鍵的實作，請在服務容器註冊單一 IAuthenticatedEncryptorConfiguration。</span><span class="sxs-lookup"><span data-stu-id="98f42-187">To change the implementation for all future keys, register a singleton IAuthenticatedEncryptorConfiguration in the service container.</span></span>

---
