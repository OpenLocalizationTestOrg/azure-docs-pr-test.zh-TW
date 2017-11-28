---
ms.assetid: 
title: "Azure Key Vault 節流指導方針 | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: fe700e22c5323c2a0bdc315e349cd119798bcf40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="97991-102">Azure Key Vault 節流指導方針</span><span class="sxs-lookup"><span data-stu-id="97991-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="97991-103">節流是您起始來限制 Azure 服務並行呼叫數目，以避免過度使用資源的程序。</span><span class="sxs-lookup"><span data-stu-id="97991-103">Throttling is a process you initiate that limits the number of concurrent calls to the Azure service to prevent overuse of resources.</span></span> <span data-ttu-id="97991-104">Azure Key Vault (AKV) 被設計來處理大量的要求。</span><span class="sxs-lookup"><span data-stu-id="97991-104">Azure Key Vault (AKV) is designed to handle a high volume of requests.</span></span> <span data-ttu-id="97991-105">如果產生大量的要求，針對用戶端的要求進行節流有助於維護 AKV 服務的最佳效能和可靠性。</span><span class="sxs-lookup"><span data-stu-id="97991-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of the AKV service.</span></span>

<span data-ttu-id="97991-106">節流限制視情節而異。</span><span class="sxs-lookup"><span data-stu-id="97991-106">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="97991-107">例如，如果您正在執行大量的寫入，則節流的可能性要高於僅執行讀取作業的可能性。</span><span class="sxs-lookup"><span data-stu-id="97991-107">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="97991-108">Key Vault 如何處理其限制？</span><span class="sxs-lookup"><span data-stu-id="97991-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="97991-109">Key Vault 中的服務限制是為了防止濫用資源，並確保所有 Key Vault 用戶端的服務品質。</span><span class="sxs-lookup"><span data-stu-id="97991-109">Service limits in Key Vault are there to prevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="97991-110">超過服務閾值時，Key Vault 可以限制一段時間內來自該用戶端的任何進一步要求。</span><span class="sxs-lookup"><span data-stu-id="97991-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="97991-111">當這種情況發生時，Key Vault 會傳回 HTTP 狀態碼 429 (太多要求)，且要求會失敗。</span><span class="sxs-lookup"><span data-stu-id="97991-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and the requests fail.</span></span> <span data-ttu-id="97991-112">此外，傳回狀態碼 429 的失敗要求會計入 Key Vault 所追蹤的節流限制中。</span><span class="sxs-lookup"><span data-stu-id="97991-112">Also, failed requests that return a 429 count towards the throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="97991-113">如果您有需要更高節流限制的有效商務案例，請與我們連絡。</span><span class="sxs-lookup"><span data-stu-id="97991-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-to-throttle-your-app-in-response-to-service-limits"></a><span data-ttu-id="97991-114">如何為您的應用程式進行節流處理，以回應服務限制</span><span class="sxs-lookup"><span data-stu-id="97991-114">How to throttle your app in response to service limits</span></span>

<span data-ttu-id="97991-115">以下是為您應用程式進行節流處理的**最佳做法**：</span><span class="sxs-lookup"><span data-stu-id="97991-115">The following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="97991-116">減少每個要求的作業數目。</span><span class="sxs-lookup"><span data-stu-id="97991-116">Reduce the number of operations per request.</span></span>
- <span data-ttu-id="97991-117">減少要求的頻率。</span><span class="sxs-lookup"><span data-stu-id="97991-117">Reduce the frequency of requests.</span></span>
- <span data-ttu-id="97991-118">避免立即重試。</span><span class="sxs-lookup"><span data-stu-id="97991-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="97991-119">所有要求都會讓您的使用量限制累加。</span><span class="sxs-lookup"><span data-stu-id="97991-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="97991-120">當您實作應用程式的錯誤處理時，請使用 HTTP 錯誤碼 429 來偵測用戶端節流的需求。</span><span class="sxs-lookup"><span data-stu-id="97991-120">When you implement your app's error handling, use the HTTP error code 429 to detect the need for client-side throttling.</span></span> <span data-ttu-id="97991-121">如果要求再次失敗並傳回 HTTP 429 錯誤碼，您仍然遇到 Azure 服務限制。</span><span class="sxs-lookup"><span data-stu-id="97991-121">If the request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="97991-122">繼續使用建議的用戶端節流方法，重試要求直到成功為止。</span><span class="sxs-lookup"><span data-stu-id="97991-122">Continue to use the recommended client-side throttling method, retrying the request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="97991-123">建議使用的用戶端節流方法</span><span class="sxs-lookup"><span data-stu-id="97991-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="97991-124">針對 HTTP 錯誤碼 429，使用指數型輪詢方法開始為您的用戶端進行節流處理：</span><span class="sxs-lookup"><span data-stu-id="97991-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="97991-125">等候 1 秒，重試要求</span><span class="sxs-lookup"><span data-stu-id="97991-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="97991-126">如果等候 2 秒仍然進行節流處理，重試要求</span><span class="sxs-lookup"><span data-stu-id="97991-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="97991-127">如果等候 4 秒仍然進行節流處理，重試要求</span><span class="sxs-lookup"><span data-stu-id="97991-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="97991-128">如果等候 8 秒仍然進行節流處理，重試要求</span><span class="sxs-lookup"><span data-stu-id="97991-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="97991-129">如果等候 16 秒仍然進行節流處理，重試要求</span><span class="sxs-lookup"><span data-stu-id="97991-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="97991-130">此時，您應該不會收到 HTTP 429 回應碼。</span><span class="sxs-lookup"><span data-stu-id="97991-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="97991-131">另請參閱</span><span class="sxs-lookup"><span data-stu-id="97991-131">See also</span></span>

<span data-ttu-id="97991-132">如需在 Microsoft Cloud 上進行節流處理的詳細資訊，請參閱[節流模式](https://docs.microsoft.com/azure/architecture/patterns/throttling) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="97991-132">For a deeper orientation of throttling on the Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

