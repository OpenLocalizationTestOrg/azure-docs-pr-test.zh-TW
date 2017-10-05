---
title: "Azure Analysis Services 高可用性 | Microsoft Docs"
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
ms.openlocfilehash: 84b4c59bac1feeb8611b3a8d783d093ba073e532
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="analysis-services-high-availability"></a><span data-ttu-id="2a7c7-103">Analysis Services 的高可用性</span><span class="sxs-lookup"><span data-stu-id="2a7c7-103">Analysis Services high availability</span></span>
<span data-ttu-id="2a7c7-104">本文說明如何確保 Azure Analysis Services 伺服器的高可用性。</span><span class="sxs-lookup"><span data-stu-id="2a7c7-104">This article describes assuring high availability for Azure Analysis Services servers.</span></span> 


## <a name="assuring-high-availability-during-a-service-disruption"></a><span data-ttu-id="2a7c7-105">在服務中斷期間確保高可用性</span><span class="sxs-lookup"><span data-stu-id="2a7c7-105">Assuring high availability during a service disruption</span></span>
<span data-ttu-id="2a7c7-106">雖然很罕見，但 Azure 資料中心也可能會有中斷的時候。</span><span class="sxs-lookup"><span data-stu-id="2a7c7-106">While rare, an Azure data center can have an outage.</span></span> <span data-ttu-id="2a7c7-107">發生中斷時，業務可能只會中斷幾分鐘，也可能會持續幾小時。</span><span class="sxs-lookup"><span data-stu-id="2a7c7-107">When an outage occurs, it causes a business disruption that might last a few minutes or might last for hours.</span></span> <span data-ttu-id="2a7c7-108">高可用性最常透過伺服器備援來實現。</span><span class="sxs-lookup"><span data-stu-id="2a7c7-108">High availability is most often achieved with server redundancy.</span></span> <span data-ttu-id="2a7c7-109">使用 Azure Analysis Services，您就可以藉由在一或多個區域建立其他的次要伺服器來實現備援。</span><span class="sxs-lookup"><span data-stu-id="2a7c7-109">With Azure Analysis Services, you can achieve redundancy by creating additional, secondary servers in one or more regions.</span></span> <span data-ttu-id="2a7c7-110">在建立備援伺服器時，為了確保這些伺服器上的資料和中繼資料會與區域中已離線的伺服器同步，您可以︰</span><span class="sxs-lookup"><span data-stu-id="2a7c7-110">When creating redundant servers, to assure the data and metadata on those servers is in-sync with the server in a region that has gone offline, you can:</span></span>

* <span data-ttu-id="2a7c7-111">將模型部署到其他區域的備援伺服器。</span><span class="sxs-lookup"><span data-stu-id="2a7c7-111">Deploy models to redundant servers in other regions.</span></span> <span data-ttu-id="2a7c7-112">此方法需要平行處理主要伺服器和備援伺服器的資料，以確保所有伺服器保持同步。</span><span class="sxs-lookup"><span data-stu-id="2a7c7-112">This method requires processing data on both your primary server and redundant servers in-parallel, assuring all servers are in-sync.</span></span>

* <span data-ttu-id="2a7c7-113">從主要伺服器備份資料庫並還原到備援伺服器上。</span><span class="sxs-lookup"><span data-stu-id="2a7c7-113">Back up databases from your primary server and restore on redundant servers.</span></span> <span data-ttu-id="2a7c7-114">例如，您可以讓目標為 Azure 儲存體的夜間備份作業自動進行，並還原到其他區域的其他備援伺服器。</span><span class="sxs-lookup"><span data-stu-id="2a7c7-114">For example, you can automate nightly backups to Azure storage, and restore to other redundant servers in other regions.</span></span> 

<span data-ttu-id="2a7c7-115">不論是哪一種情況，如果您的主要伺服器發生中斷，您都必須將報告用戶端中的連接字串，變更為連線到不同區域資料中心的伺服器。</span><span class="sxs-lookup"><span data-stu-id="2a7c7-115">In either case, if your primary server experiences an outage, you must change the connection strings in reporting clients to connect to the server in a different regional datacenter.</span></span> <span data-ttu-id="2a7c7-116">此變更作業應視為最後手段，只有在發生重大的區域資料中心中斷時才應考慮使用。</span><span class="sxs-lookup"><span data-stu-id="2a7c7-116">This change should be considered a last resort and only if a catastrophic regional data center outage occurs.</span></span> <span data-ttu-id="2a7c7-117">比較常見的情況是，您可能還未更新所有用戶端上的連線，裝載主要伺服器的資料中心就已從中斷狀態恢復為上線狀態。</span><span class="sxs-lookup"><span data-stu-id="2a7c7-117">It's more likely a data center outage hosting your primary server would come back online before you could update connections on all clients.</span></span> 



## <a name="related-information"></a><span data-ttu-id="2a7c7-118">相關資訊</span><span class="sxs-lookup"><span data-stu-id="2a7c7-118">Related information</span></span>
<span data-ttu-id="2a7c7-119">[備份與還原](analysis-services-backup.md) </span><span class="sxs-lookup"><span data-stu-id="2a7c7-119">[Backup and restore](analysis-services-backup.md) </span></span>  
[<span data-ttu-id="2a7c7-120">管理 Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="2a7c7-120">Manage Azure Analysis Services</span></span>](analysis-services-manage.md) 

