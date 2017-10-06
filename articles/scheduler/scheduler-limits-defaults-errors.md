---
title: "aaaScheduler 限制及預設值"
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
ms.openlocfilehash: 6fe0600d3ce3249d5aab1b877369b175316b5437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-limits-and-defaults"></a><span data-ttu-id="9f6a2-103">排程器限制及預設值</span><span class="sxs-lookup"><span data-stu-id="9f6a2-103">Scheduler Limits and Defaults</span></span>
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a><span data-ttu-id="9f6a2-104">排程器配額、限制、預設值和節流</span><span class="sxs-lookup"><span data-stu-id="9f6a2-104">Scheduler Quotas, Limits, Defaults, and Throttles</span></span>
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="hello-x-ms-request-id-header"></a><span data-ttu-id="9f6a2-105">hello x ms-要求識別碼標頭</span><span class="sxs-lookup"><span data-stu-id="9f6a2-105">hello x-ms-request-id Header</span></span>
<span data-ttu-id="9f6a2-106">每個對 hello 排程器服務所提出的要求會傳回回應標頭**x ms-要求識別碼**。此標頭包含唯一識別 hello 要求的不透明值。</span><span class="sxs-lookup"><span data-stu-id="9f6a2-106">Every request made against hello Scheduler service returns a response header named**x-ms-request-id**. This header contains an opaque value that uniquely identifies hello request.</span></span>

<span data-ttu-id="9f6a2-107">如果要求不一致的方式失敗，且您有會確認 hello 要求為正確的組成之後，您可以使用此值 tooreport hello 錯誤 tooMicrosoft。</span><span class="sxs-lookup"><span data-stu-id="9f6a2-107">If a request is consistently failing and you have verified that hello request is properly formulated, you may use this value tooreport hello error tooMicrosoft.</span></span> <span data-ttu-id="9f6a2-108">在報表中，加入 x ms-要求識別碼，hello 的大約時間 hello 值該 hello 製作要求之 hello hello 訂用帳戶、 工作集合和/或作業的識別碼和 hello hello 要求嘗試的作業類型。</span><span class="sxs-lookup"><span data-stu-id="9f6a2-108">In your report, include hello value of x-ms-request-id, hello approximate time that hello request was made, hello identifier of hello subscription, job collection, and/or job, and hello type of operation that hello request attempted.</span></span>

## <a name="see-also"></a><span data-ttu-id="9f6a2-109">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9f6a2-109">See Also</span></span>
 [<span data-ttu-id="9f6a2-110">排程器是什麼？</span><span class="sxs-lookup"><span data-stu-id="9f6a2-110">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="9f6a2-111">Azure 排程器概念、術語及實體階層</span><span class="sxs-lookup"><span data-stu-id="9f6a2-111">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="9f6a2-112">開始在 hello Azure 入口網站中使用排程器</span><span class="sxs-lookup"><span data-stu-id="9f6a2-112">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="9f6a2-113">Azure 排程器的計劃和計費</span><span class="sxs-lookup"><span data-stu-id="9f6a2-113">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="9f6a2-114">Azure 排程器 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="9f6a2-114">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="9f6a2-115">Azure 排程器 PowerShell Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="9f6a2-115">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="9f6a2-116">Azure 排程器高可用性和可靠性</span><span class="sxs-lookup"><span data-stu-id="9f6a2-116">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="9f6a2-117">Azure 排程器輸出驗證</span><span class="sxs-lookup"><span data-stu-id="9f6a2-117">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

