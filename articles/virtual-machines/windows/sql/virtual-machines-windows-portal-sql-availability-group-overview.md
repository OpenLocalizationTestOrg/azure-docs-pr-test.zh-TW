---
title: "SQL Server 可用性群組 - Azure 虛擬機器 - 概觀 | Microsoft Docs"
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
ms.openlocfilehash: 2cbb9ff3b2d13996b1b8dc64aa833807c264c877
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a><span data-ttu-id="781e9-103">Azure 虛擬機器上的 SQL Server Always On 可用性群組簡介</span><span class="sxs-lookup"><span data-stu-id="781e9-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span> #

<span data-ttu-id="781e9-104">本文介紹 Azure 虛擬機器上的 SQL Server 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="781e9-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span></span> 

<span data-ttu-id="781e9-105">「Azure 虛擬機器」上的 Always On 可用性群組與內部部署的 Always On 可用性群組類似。</span><span class="sxs-lookup"><span data-stu-id="781e9-105">Always On availability groups on Azure Virtual Machines are similar to Always On availability groups on premises.</span></span> <span data-ttu-id="781e9-106">如需詳細資訊，請參閱 [Always On 可用性群組 (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx)。</span><span class="sxs-lookup"><span data-stu-id="781e9-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span> 

<span data-ttu-id="781e9-107">下圖顯示「Azure 虛擬機器」中完整「SQL Server 可用性群組」的各個部分。</span><span class="sxs-lookup"><span data-stu-id="781e9-107">The diagram illustrates the parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span></span>

![可用性群組](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

<span data-ttu-id="781e9-109">「Azure 虛擬機器」中「可用性群組」的主要差異在於 Azure 虛擬機器需要[負載平衡器](../../../load-balancer/load-balancer-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="781e9-109">The key difference for an Availability Group in Azure Virtual Machines is that the Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="781e9-110">負載平衡器會保有可用性群組接聽程式的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="781e9-110">The load balancer holds the IP addresses for the availability group listener.</span></span> <span data-ttu-id="781e9-111">如果您有多個可用性群組，則每個群組都需要一個接聽程式。</span><span class="sxs-lookup"><span data-stu-id="781e9-111">If you have more than one availability group each group requires a listener.</span></span> <span data-ttu-id="781e9-112">一個負載平衡器可以支援多個接聽程式。</span><span class="sxs-lookup"><span data-stu-id="781e9-112">One load balancer can support multiple listeners.</span></span>

<span data-ttu-id="781e9-113">當您已準備好在「Azure 虛擬機器」上建置 SQL Server 可用性群組時，請參考這些教學課程。</span><span class="sxs-lookup"><span data-stu-id="781e9-113">When you are ready to build a SQL Server availability aroup on Azure Virtual Machines, refer to these tutorials.</span></span>

## <a name="automatically-create-an-availability-group-from-a-template"></a><span data-ttu-id="781e9-114">從範本自動建立可用性群組</span><span class="sxs-lookup"><span data-stu-id="781e9-114">Automatically create an availability group from a template</span></span>

[<span data-ttu-id="781e9-115">在 Azure VM 中自動設定 Always On 可用性群組 - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="781e9-115">Configure Always On availability group in Azure VM automatically - Resource Manager</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a><span data-ttu-id="781e9-116">在 Azure 入口網站中手動建立可用性群組</span><span class="sxs-lookup"><span data-stu-id="781e9-116">Manually create an availability group in Azure portal</span></span>

<span data-ttu-id="781e9-117">您也可以自行建立虛擬機器，而不使用範本。</span><span class="sxs-lookup"><span data-stu-id="781e9-117">You can also create the virtual machines yourself without the template.</span></span> <span data-ttu-id="781e9-118">首先，請完成必要條件，然後再建立可用性群組。</span><span class="sxs-lookup"><span data-stu-id="781e9-118">First, complete the prerequisites, then create the availability group.</span></span> <span data-ttu-id="781e9-119">請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="781e9-119">See the following topics:</span></span> 

- [<span data-ttu-id="781e9-120">設定 Azure 虛擬機器上 SQL Server Always On 可用性群組的必要條件</span><span class="sxs-lookup"><span data-stu-id="781e9-120">Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines</span></span>](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [<span data-ttu-id="781e9-121">建立 Always On 可用性群組以改善可用性和災害復原</span><span class="sxs-lookup"><span data-stu-id="781e9-121">Create Always On Availability Group to improve availability and disaster recovery</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a><span data-ttu-id="781e9-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="781e9-122">Next steps</span></span>

<span data-ttu-id="781e9-123">[在不同區域中的 Azure 虛擬機器上設定 SQL Server Always On 可用性群組](virtual-machines-windows-portal-sql-availability-group-dr.md)。</span><span class="sxs-lookup"><span data-stu-id="781e9-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span></span>
