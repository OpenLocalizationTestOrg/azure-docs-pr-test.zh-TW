---
ms.assetid: 
title: "金鑰保存庫節流指引 aaaAzure |Microsoft 文件"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: a75cf96bc6503e51f14378bee598bad57e85be82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="07894-102">Azure Key Vault 節流指導方針</span><span class="sxs-lookup"><span data-stu-id="07894-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="07894-103">節流是限制同時呼叫 toohello Azure 服務 tooprevent 的過度使用資源的 hello 數目的程序初始化。</span><span class="sxs-lookup"><span data-stu-id="07894-103">Throttling is a process you initiate that limits hello number of concurrent calls toohello Azure service tooprevent overuse of resources.</span></span> <span data-ttu-id="07894-104">Azure 金鑰保存庫 (AKV) 是設計的 toohandle 大量的要求。</span><span class="sxs-lookup"><span data-stu-id="07894-104">Azure Key Vault (AKV) is designed toohandle a high volume of requests.</span></span> <span data-ttu-id="07894-105">如果產生大量的要求，就會發生，節流設定您的用戶端要求可協助維護最佳效能和可靠性的 hello AKV 服務。</span><span class="sxs-lookup"><span data-stu-id="07894-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of hello AKV service.</span></span>

<span data-ttu-id="07894-106">節流限制會根據 hello 案例而有所不同。</span><span class="sxs-lookup"><span data-stu-id="07894-106">Throttling limits vary based on hello scenario.</span></span> <span data-ttu-id="07894-107">例如，如果您正在執行大量的寫入，hello 節流可能性高於如果您只執行讀取。</span><span class="sxs-lookup"><span data-stu-id="07894-107">For example, if you are performing a large volume of writes, hello possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="07894-108">Key Vault 如何處理其限制？</span><span class="sxs-lookup"><span data-stu-id="07894-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="07894-109">金鑰保存庫中的服務限制有 tooprevent 不當使用的資源，並確定所有金鑰保存庫的用戶端的服務品質。</span><span class="sxs-lookup"><span data-stu-id="07894-109">Service limits in Key Vault are there tooprevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="07894-110">超過服務閾值時，Key Vault 可以限制一段時間內來自該用戶端的任何進一步要求。</span><span class="sxs-lookup"><span data-stu-id="07894-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="07894-111">發生這種情況，金鑰保存庫會傳回 HTTP 狀態碼 429 (太多要求)，和 hello 要求會失敗。</span><span class="sxs-lookup"><span data-stu-id="07894-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and hello requests fail.</span></span> <span data-ttu-id="07894-112">此外，無法傳回 429 計數朝向 hello 節流閥限制追蹤的金鑰保存庫的要求。</span><span class="sxs-lookup"><span data-stu-id="07894-112">Also, failed requests that return a 429 count towards hello throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="07894-113">如果您有需要更高節流限制的有效商務案例，請與我們連絡。</span><span class="sxs-lookup"><span data-stu-id="07894-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-toothrottle-your-app-in-response-tooservice-limits"></a><span data-ttu-id="07894-114">如何 toothrottle 回應 tooservice 中的應用程式限制</span><span class="sxs-lookup"><span data-stu-id="07894-114">How toothrottle your app in response tooservice limits</span></span>

<span data-ttu-id="07894-115">hello 如下**最佳做法**節流您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="07894-115">hello following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="07894-116">Hello 的減少每個要求的作業。</span><span class="sxs-lookup"><span data-stu-id="07894-116">Reduce hello number of operations per request.</span></span>
- <span data-ttu-id="07894-117">減少 hello 頻率的要求。</span><span class="sxs-lookup"><span data-stu-id="07894-117">Reduce hello frequency of requests.</span></span>
- <span data-ttu-id="07894-118">避免立即重試。</span><span class="sxs-lookup"><span data-stu-id="07894-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="07894-119">所有要求都會讓您的使用量限制累加。</span><span class="sxs-lookup"><span data-stu-id="07894-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="07894-120">當您實作您的應用程式錯誤處理時，使用 hello HTTP 錯誤程式碼 429 toodetect hello 需要用戶端節流。</span><span class="sxs-lookup"><span data-stu-id="07894-120">When you implement your app's error handling, use hello HTTP error code 429 toodetect hello need for client-side throttling.</span></span> <span data-ttu-id="07894-121">如果 hello 要求再次失敗，HTTP 429 錯誤代碼，您仍然遇到 Azure 服務的限制。</span><span class="sxs-lookup"><span data-stu-id="07894-121">If hello request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="07894-122">繼續 toouse hello 建議使用的用戶端節流方法，重試 hello 要求，直到成功為止。</span><span class="sxs-lookup"><span data-stu-id="07894-122">Continue toouse hello recommended client-side throttling method, retrying hello request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="07894-123">建議使用的用戶端節流方法</span><span class="sxs-lookup"><span data-stu-id="07894-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="07894-124">針對 HTTP 錯誤碼 429，使用指數型輪詢方法開始為您的用戶端進行節流處理：</span><span class="sxs-lookup"><span data-stu-id="07894-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="07894-125">等候 1 秒，重試要求</span><span class="sxs-lookup"><span data-stu-id="07894-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="07894-126">如果等候 2 秒仍然進行節流處理，重試要求</span><span class="sxs-lookup"><span data-stu-id="07894-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="07894-127">如果等候 4 秒仍然進行節流處理，重試要求</span><span class="sxs-lookup"><span data-stu-id="07894-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="07894-128">如果等候 8 秒仍然進行節流處理，重試要求</span><span class="sxs-lookup"><span data-stu-id="07894-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="07894-129">如果等候 16 秒仍然進行節流處理，重試要求</span><span class="sxs-lookup"><span data-stu-id="07894-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="07894-130">此時，您應該不會收到 HTTP 429 回應碼。</span><span class="sxs-lookup"><span data-stu-id="07894-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="07894-131">另請參閱</span><span class="sxs-lookup"><span data-stu-id="07894-131">See also</span></span>

<span data-ttu-id="07894-132">節流 hello Microsoft 雲端上的更深入方向，請參閱[節流模式](https://docs.microsoft.com/azure/architecture/patterns/throttling)。</span><span class="sxs-lookup"><span data-stu-id="07894-132">For a deeper orientation of throttling on hello Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

