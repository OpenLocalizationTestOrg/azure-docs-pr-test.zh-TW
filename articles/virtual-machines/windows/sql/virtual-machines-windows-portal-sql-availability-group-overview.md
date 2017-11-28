---
title: "aaaSQL Server 可用性群組-Azure 虛擬機器-概觀 |Microsoft 文件"
description: "本文介紹 Azure 虛擬機器上的「SQL Server 可用性群組」。"
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 601eebb1-fc2c-4f5b-9c05-0e6ffd0e5334
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/13/2017
ms.author: mikeray
ms.openlocfilehash: ecac8b8c5073021af2aa22a05490bb8c4c20ed17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a><span data-ttu-id="d031f-103">Azure 虛擬機器上的 SQL Server Always On 可用性群組簡介</span><span class="sxs-lookup"><span data-stu-id="d031f-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span> #

<span data-ttu-id="d031f-104">本文介紹 Azure 虛擬機器上的 SQL Server 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="d031f-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span></span> 

<span data-ttu-id="d031f-105">Always On 可用性群組在 Azure 虛擬機器都類似 tooAlways 在內部部署可用性群組。</span><span class="sxs-lookup"><span data-stu-id="d031f-105">Always On availability groups on Azure Virtual Machines are similar tooAlways On availability groups on premises.</span></span> <span data-ttu-id="d031f-106">如需詳細資訊，請參閱 [Always On 可用性群組 (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d031f-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span> 

<span data-ttu-id="d031f-107">hello 圖表說明完成 SQL Server 可用性群組的 Azure 虛擬機器中的 hello 組件。</span><span class="sxs-lookup"><span data-stu-id="d031f-107">hello diagram illustrates hello parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span></span>

![可用性群組](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

<span data-ttu-id="d031f-109">hello 主要差異為可用性群組在 Azure 虛擬機器中的 hello Azure 虛擬機器，需要[負載平衡器](../../../load-balancer/load-balancer-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d031f-109">hello key difference for an Availability Group in Azure Virtual Machines is that hello Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="d031f-110">hello 負載平衡器會保存 hello hello 可用性群組接聽程式的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d031f-110">hello load balancer holds hello IP addresses for hello availability group listener.</span></span> <span data-ttu-id="d031f-111">如果您有多個可用性群組，則每個群組都需要一個接聽程式。</span><span class="sxs-lookup"><span data-stu-id="d031f-111">If you have more than one availability group each group requires a listener.</span></span> <span data-ttu-id="d031f-112">一個負載平衡器可以支援多個接聽程式。</span><span class="sxs-lookup"><span data-stu-id="d031f-112">One load balancer can support multiple listeners.</span></span>

<span data-ttu-id="d031f-113">當您準備好 toobuild SQL Server 可用性 aroup Azure 虛擬機器上，請參閱 toothese 教學課程。</span><span class="sxs-lookup"><span data-stu-id="d031f-113">When you are ready toobuild a SQL Server availability aroup on Azure Virtual Machines, refer toothese tutorials.</span></span>

## <a name="automatically-create-an-availability-group-from-a-template"></a><span data-ttu-id="d031f-114">從範本自動建立可用性群組</span><span class="sxs-lookup"><span data-stu-id="d031f-114">Automatically create an availability group from a template</span></span>

[<span data-ttu-id="d031f-115">在 Azure VM 中自動設定 Always On 可用性群組 - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d031f-115">Configure Always On availability group in Azure VM automatically - Resource Manager</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a><span data-ttu-id="d031f-116">在 Azure 入口網站中手動建立可用性群組</span><span class="sxs-lookup"><span data-stu-id="d031f-116">Manually create an availability group in Azure portal</span></span>

<span data-ttu-id="d031f-117">您也可以建立 hello 虛擬機器自行不 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="d031f-117">You can also create hello virtual machines yourself without hello template.</span></span> <span data-ttu-id="d031f-118">請先完成 hello 必要條件，再建立 hello 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="d031f-118">First, complete hello prerequisites, then create hello availability group.</span></span> <span data-ttu-id="d031f-119">請參閱下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="d031f-119">See hello following topics:</span></span> 

- [<span data-ttu-id="d031f-120">設定 Azure 虛擬機器上 SQL Server Always On 可用性群組的必要條件</span><span class="sxs-lookup"><span data-stu-id="d031f-120">Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines</span></span>](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [<span data-ttu-id="d031f-121">建立 Alwayson 可用性群組 tooimprove 可用性和災害復原</span><span class="sxs-lookup"><span data-stu-id="d031f-121">Create Always On Availability Group tooimprove availability and disaster recovery</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a><span data-ttu-id="d031f-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d031f-122">Next steps</span></span>

<span data-ttu-id="d031f-123">[在不同區域中的 Azure 虛擬機器上設定 SQL Server Always On 可用性群組](virtual-machines-windows-portal-sql-availability-group-dr.md)。</span><span class="sxs-lookup"><span data-stu-id="d031f-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span></span>
