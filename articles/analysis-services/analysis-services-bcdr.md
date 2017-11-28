---
title: "Analysis Services 的高可用性 aaaAzure |Microsoft 文件"
description: "確保 Azure Analysis Services 的高可用性。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 6e09536c5bd7dc7f88f9b662e1a9f42d2b8c969b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analysis-services-high-availability"></a><span data-ttu-id="ac85e-103">Analysis Services 的高可用性</span><span class="sxs-lookup"><span data-stu-id="ac85e-103">Analysis Services high availability</span></span>
<span data-ttu-id="ac85e-104">本文說明如何確保 Azure Analysis Services 伺服器的高可用性。</span><span class="sxs-lookup"><span data-stu-id="ac85e-104">This article describes assuring high availability for Azure Analysis Services servers.</span></span> 


## <a name="assuring-high-availability-during-a-service-disruption"></a><span data-ttu-id="ac85e-105">在服務中斷期間確保高可用性</span><span class="sxs-lookup"><span data-stu-id="ac85e-105">Assuring high availability during a service disruption</span></span>
<span data-ttu-id="ac85e-106">雖然很罕見，但 Azure 資料中心也可能會有中斷的時候。</span><span class="sxs-lookup"><span data-stu-id="ac85e-106">While rare, an Azure data center can have an outage.</span></span> <span data-ttu-id="ac85e-107">發生中斷時，業務可能只會中斷幾分鐘，也可能會持續幾小時。</span><span class="sxs-lookup"><span data-stu-id="ac85e-107">When an outage occurs, it causes a business disruption that might last a few minutes or might last for hours.</span></span> <span data-ttu-id="ac85e-108">高可用性最常透過伺服器備援來實現。</span><span class="sxs-lookup"><span data-stu-id="ac85e-108">High availability is most often achieved with server redundancy.</span></span> <span data-ttu-id="ac85e-109">使用 Azure Analysis Services，您就可以藉由在一或多個區域建立其他的次要伺服器來實現備援。</span><span class="sxs-lookup"><span data-stu-id="ac85e-109">With Azure Analysis Services, you can achieve redundancy by creating additional, secondary servers in one or more regions.</span></span> <span data-ttu-id="ac85e-110">當在那些伺服器上建立備援伺服器、 tooassure hello 資料和中繼資料是在同步處理與 hello 伺服器區域中，已離線，您可以：</span><span class="sxs-lookup"><span data-stu-id="ac85e-110">When creating redundant servers, tooassure hello data and metadata on those servers is in-sync with hello server in a region that has gone offline, you can:</span></span>

* <span data-ttu-id="ac85e-111">部署模型 tooredundant 伺服器中的其他區域。</span><span class="sxs-lookup"><span data-stu-id="ac85e-111">Deploy models tooredundant servers in other regions.</span></span> <span data-ttu-id="ac85e-112">此方法需要平行處理主要伺服器和備援伺服器的資料，以確保所有伺服器保持同步。</span><span class="sxs-lookup"><span data-stu-id="ac85e-112">This method requires processing data on both your primary server and redundant servers in-parallel, assuring all servers are in-sync.</span></span>

* <span data-ttu-id="ac85e-113">從主要伺服器備份資料庫並還原到備援伺服器上。</span><span class="sxs-lookup"><span data-stu-id="ac85e-113">Back up databases from your primary server and restore on redundant servers.</span></span> <span data-ttu-id="ac85e-114">比方說，您可以自動化夜間備份 tooAzure 存放裝置，並還原 tooother 備援伺服器的其他區域中。</span><span class="sxs-lookup"><span data-stu-id="ac85e-114">For example, you can automate nightly backups tooAzure storage, and restore tooother redundant servers in other regions.</span></span> 

<span data-ttu-id="ac85e-115">在任一情況下，如果您的主要伺服器發生中斷，您必須變更在報表中不同的地區資料中心的用戶端 tooconnect toohello 伺服器 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="ac85e-115">In either case, if your primary server experiences an outage, you must change hello connection strings in reporting clients tooconnect toohello server in a different regional datacenter.</span></span> <span data-ttu-id="ac85e-116">此變更作業應視為最後手段，只有在發生重大的區域資料中心中斷時才應考慮使用。</span><span class="sxs-lookup"><span data-stu-id="ac85e-116">This change should be considered a last resort and only if a catastrophic regional data center outage occurs.</span></span> <span data-ttu-id="ac85e-117">比較常見的情況是，您可能還未更新所有用戶端上的連線，裝載主要伺服器的資料中心就已從中斷狀態恢復為上線狀態。</span><span class="sxs-lookup"><span data-stu-id="ac85e-117">It's more likely a data center outage hosting your primary server would come back online before you could update connections on all clients.</span></span> 



## <a name="related-information"></a><span data-ttu-id="ac85e-118">相關資訊</span><span class="sxs-lookup"><span data-stu-id="ac85e-118">Related information</span></span>
<span data-ttu-id="ac85e-119">[備份與還原](analysis-services-backup.md) </span><span class="sxs-lookup"><span data-stu-id="ac85e-119">[Backup and restore](analysis-services-backup.md) </span></span>  
[<span data-ttu-id="ac85e-120">管理 Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ac85e-120">Manage Azure Analysis Services</span></span>](analysis-services-manage.md) 

