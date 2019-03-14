---
title: 其他 ASP.NET Core 資料保護 Api
author: rick-anderson
description: 深入了解 ASP.NET Core 資料保護 ISecret 介面。
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/extensibility/misc-apis
ms.openlocfilehash: 114cdd6209970e46b827e403fbe79b95692d0242
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57033155"
---
# <a name="miscellaneous-aspnet-core-data-protection-apis"></a><span data-ttu-id="d5371-103">其他 ASP.NET Core 資料保護 Api</span><span class="sxs-lookup"><span data-stu-id="d5371-103">Miscellaneous ASP.NET Core Data Protection APIs</span></span>

<a name="data-protection-extensibility-mics-apis"></a>

>[!WARNING]
> <span data-ttu-id="d5371-104">會實作下列介面的任何的類型應該是安全執行緒的多個呼叫端。</span><span class="sxs-lookup"><span data-stu-id="d5371-104">Types that implement any of the following interfaces should be thread-safe for multiple callers.</span></span>

## <a name="isecret"></a><span data-ttu-id="d5371-105">ISecret</span><span class="sxs-lookup"><span data-stu-id="d5371-105">ISecret</span></span>

<span data-ttu-id="d5371-106">`ISecret`介面代表祕密的值，例如密碼編譯金鑰的內容。</span><span class="sxs-lookup"><span data-stu-id="d5371-106">The `ISecret` interface represents a secret value, such as cryptographic key material.</span></span> <span data-ttu-id="d5371-107">它包含下列的 API 介面：</span><span class="sxs-lookup"><span data-stu-id="d5371-107">It contains the following API surface:</span></span>

* <span data-ttu-id="d5371-108">`Length`: `int`</span><span class="sxs-lookup"><span data-stu-id="d5371-108">`Length`: `int`</span></span>

* <span data-ttu-id="d5371-109">`Dispose()`: `void`</span><span class="sxs-lookup"><span data-stu-id="d5371-109">`Dispose()`: `void`</span></span>

* <span data-ttu-id="d5371-110">`WriteSecretIntoBuffer(ArraySegment<byte> buffer)`: `void`</span><span class="sxs-lookup"><span data-stu-id="d5371-110">`WriteSecretIntoBuffer(ArraySegment<byte> buffer)`: `void`</span></span>

<span data-ttu-id="d5371-111">`WriteSecretIntoBuffer`方法會填入與原始的祕密值提供的緩衝區。</span><span class="sxs-lookup"><span data-stu-id="d5371-111">The `WriteSecretIntoBuffer` method populates the supplied buffer with the raw secret value.</span></span> <span data-ttu-id="d5371-112">此 API 會做為參數緩衝區的原因而不會傳回`byte[]`直接是這讓呼叫端若要釘選緩衝區物件，限制受管理的記憶體回收行程的祕密曝光機會。</span><span class="sxs-lookup"><span data-stu-id="d5371-112">The reason this API takes the buffer as a parameter rather than returning a `byte[]` directly is that this gives the caller the opportunity to pin the buffer object, limiting secret exposure to the managed garbage collector.</span></span>

<span data-ttu-id="d5371-113">`Secret`類型是具象實作`ISecret`同處理序記憶體中儲存的祕密的值。</span><span class="sxs-lookup"><span data-stu-id="d5371-113">The `Secret` type is a concrete implementation of `ISecret` where the secret value is stored in in-process memory.</span></span> <span data-ttu-id="d5371-114">在 Windows 平台，透過加密祕密值[CryptProtectMemory](https://msdn.microsoft.com/library/windows/desktop/aa380262(v=vs.85).aspx)。</span><span class="sxs-lookup"><span data-stu-id="d5371-114">On Windows platforms, the secret value is encrypted via [CryptProtectMemory](https://msdn.microsoft.com/library/windows/desktop/aa380262(v=vs.85).aspx).</span></span>
