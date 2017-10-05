---
title: "排程器限制及預設值"
description: "排程器限制及預設值"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 88f4a3e9-6dbd-4943-8543-f0649d423061
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: db6b1c196cb468f41c7a7ce34758de346b522abb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-limits-and-defaults"></a><span data-ttu-id="ec1b7-103">排程器限制及預設值</span><span class="sxs-lookup"><span data-stu-id="ec1b7-103">Scheduler Limits and Defaults</span></span>
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a><span data-ttu-id="ec1b7-104">排程器配額、限制、預設值和節流</span><span class="sxs-lookup"><span data-stu-id="ec1b7-104">Scheduler Quotas, Limits, Defaults, and Throttles</span></span>
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="the-x-ms-request-id-header"></a><span data-ttu-id="ec1b7-105">x-ms-request-id 標頭</span><span class="sxs-lookup"><span data-stu-id="ec1b7-105">The x-ms-request-id Header</span></span>
<span data-ttu-id="ec1b7-106">每一個對排程器服務提出的要求都會傳回名為**x-ms-request-id**的回應標頭。</span><span class="sxs-lookup"><span data-stu-id="ec1b7-106">Every request made against the Scheduler service returns a response header named**x-ms-request-id**.</span></span> <span data-ttu-id="ec1b7-107">此標頭包含專門識別要求的不透明值。</span><span class="sxs-lookup"><span data-stu-id="ec1b7-107">This header contains an opaque value that uniquely identifies the request.</span></span>

<span data-ttu-id="ec1b7-108">如果要求一直失敗，而且您已確認要求表達正確，則可以使用此值將錯誤回報給 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="ec1b7-108">If a request is consistently failing and you have verified that the request is properly formulated, you may use this value to report the error to Microsoft.</span></span> <span data-ttu-id="ec1b7-109">在您的報告中，請包括 x-ms-request-id 的值、提出要求的大約時間、訂用帳戶的識別碼、工作集合及/或工作，以及要求所嘗試的作業類型。</span><span class="sxs-lookup"><span data-stu-id="ec1b7-109">In your report, include the value of x-ms-request-id, the approximate time that the request was made, the identifier of the subscription, job collection, and/or job, and the type of operation that the request attempted.</span></span>

## <a name="see-also"></a><span data-ttu-id="ec1b7-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ec1b7-110">See Also</span></span>
 [<span data-ttu-id="ec1b7-111">排程器是什麼？</span><span class="sxs-lookup"><span data-stu-id="ec1b7-111">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="ec1b7-112">Azure 排程器概念、術語及實體階層</span><span class="sxs-lookup"><span data-stu-id="ec1b7-112">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="ec1b7-113">在 Azure 入口網站中開始使用排程器</span><span class="sxs-lookup"><span data-stu-id="ec1b7-113">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="ec1b7-114">Azure 排程器的計劃和計費</span><span class="sxs-lookup"><span data-stu-id="ec1b7-114">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="ec1b7-115">Azure 排程器 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="ec1b7-115">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="ec1b7-116">Azure 排程器 PowerShell Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="ec1b7-116">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="ec1b7-117">Azure 排程器高可用性和可靠性</span><span class="sxs-lookup"><span data-stu-id="ec1b7-117">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="ec1b7-118">Azure 排程器輸出驗證</span><span class="sxs-lookup"><span data-stu-id="ec1b7-118">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

