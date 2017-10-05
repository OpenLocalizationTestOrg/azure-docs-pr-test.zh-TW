---
title: "使用 Azure 串流分析工作來避免發生服務中斷 | Microsoft Docs"
description: "提供讓您的「串流分析」工作升級具有彈性的指引。"
services: stream-analytics
documentationCenter: 
authors: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 8dc19e1b37082c87d2990ad910d1af786f8b9280
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a><span data-ttu-id="9c017-103">在服務更新期間確保串流分析工作可靠性</span><span class="sxs-lookup"><span data-stu-id="9c017-103">Guarantee Stream Analytics job reliability during service updates</span></span>

<span data-ttu-id="9c017-104">完全受管理服務的其中一個特性，就是能夠快速導入新的服務功能和改良功能。</span><span class="sxs-lookup"><span data-stu-id="9c017-104">Part of being a fully managed service is the capability to introduce new service functionality and improvements at a rapid pace.</span></span> <span data-ttu-id="9c017-105">因此，「串流分析」可以每週 (或更頻繁地) 進行服務更新部署。</span><span class="sxs-lookup"><span data-stu-id="9c017-105">As a result, Stream Analytics can have a service update deploy on a weekly (or more frequent) basis.</span></span> <span data-ttu-id="9c017-106">不論做了多少測試，現有的執行中工作仍然可能有因引入錯誤而導致中斷的風險。</span><span class="sxs-lookup"><span data-stu-id="9c017-106">No matter how much testing is done there is still a risk that an existing, running job may break due to the introduction of a bug.</span></span> <span data-ttu-id="9c017-107">對於執行重要串流處理工作的客戶來說，必須避免這些風險。</span><span class="sxs-lookup"><span data-stu-id="9c017-107">For customers who run critical streaming processing jobs these risks need to be avoided.</span></span> <span data-ttu-id="9c017-108">有一個可供客戶用來降低此風險的機制，就是 Azure 的**[配對區域](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**模型。</span><span class="sxs-lookup"><span data-stu-id="9c017-108">A mechanism customers can use to reduce this risk is Azure’s **[paired region](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** model.</span></span> 

## <a name="how-do-azure-paired-regions-address-this-concern"></a><span data-ttu-id="9c017-109">Azure 配對區域如何解決這個問題？</span><span class="sxs-lookup"><span data-stu-id="9c017-109">How do Azure paired regions address this concern?</span></span>

<span data-ttu-id="9c017-110">「串流分析」可確保以個別的批次更新在配對區域中的工作。</span><span class="sxs-lookup"><span data-stu-id="9c017-110">Stream Analytics guarantees jobs in paired regions are updated in separate batches.</span></span> <span data-ttu-id="9c017-111">如此一來，在找出潛在重大錯誤與進行補救的更新之間，便有足夠的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="9c017-111">As a result there is a sufficient time gap between the updates to identify potential breaking bugs and remediate them.</span></span>

<span data-ttu-id="9c017-112">「印度中部是一個例外」(其配對區域印度南部並沒有提供「串流分析」服務)，「串流分析」更新部署不會在一組配對區域同時發生。</span><span class="sxs-lookup"><span data-stu-id="9c017-112">_With the exception of Central India_ (whose paired region, South India, does not have Stream Analytics presence), the deployment of an update to Stream Analytics would not occur at the same time in a set of paired regions.</span></span> <span data-ttu-id="9c017-113">**相同群組內**多個區域中的部署可能**同時**發生。</span><span class="sxs-lookup"><span data-stu-id="9c017-113">Deployments in multiple regions **in the same group** may occur **at the same time**.</span></span>

<span data-ttu-id="9c017-114">關於**[可用性與配對區域](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**的文章提供了有關配對區域的最新資訊。</span><span class="sxs-lookup"><span data-stu-id="9c017-114">The article on **[availability and paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** has the most up-to-date information on which regions are paired.</span></span>

<span data-ttu-id="9c017-115">建議客戶在兩個配對區域都部署相同的工作。</span><span class="sxs-lookup"><span data-stu-id="9c017-115">Customers are advised to deploy identical jobs to both paired regions.</span></span> <span data-ttu-id="9c017-116">除了「串流分析」內部監視功能之外，也建議客戶將「兩個」工作都當作生產環境工作來監視。</span><span class="sxs-lookup"><span data-stu-id="9c017-116">In addition to Stream Analytics internal monitoring capabilities, customers are also advised to monitor the jobs as if **both** are production jobs.</span></span> <span data-ttu-id="9c017-117">如果中斷情況經識別是「串流分析」服務更新所造成，請適當地呈報此問題，並將所有下游取用者容錯移轉至狀況良好的工作輸出。</span><span class="sxs-lookup"><span data-stu-id="9c017-117">If a break is identified to be a result of the Stream Analytics service update, escalate appropriately and fail over any downstream consumers to the healthy job output.</span></span> <span data-ttu-id="9c017-118">向支援服務呈報此問題將可防止配對區域受到新部署作業影響，並可維護配對工作的完整性。</span><span class="sxs-lookup"><span data-stu-id="9c017-118">Escalation to support will prevent the paired region from being affected by the new deployment and maintain the integrity of the paired jobs.</span></span>
