---
title: "如何為 Azure 中的 Linux VM 排定計劃性維護 | Microsoft Docs"
description: "了解如何排定在 Azure VM 上的計劃性維護。"
services: virtual-machines-linux
documentationcenter: 
author: igalf
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 619a65ce-f913-4c92-a7ba-2971a839c306
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: igalf
ms.openlocfilehash: 84a61313547e0e7b3715552ab8b20f76eda39db7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-schedule-planned-maintenance-on-azure-vms"></a><span data-ttu-id="3c3cf-103">如何排定在 Azure VM 上的計劃性維護</span><span class="sxs-lookup"><span data-stu-id="3c3cf-103">How to Schedule Planned Maintenance on Azure VMs</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3c3cf-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="3c3cf-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3c3cf-105">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="3c3cf-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="3c3cf-106">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="3c3cf-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="3c3cf-107">如需 Resource Manager 模型中計劃性維護的詳細資訊，請參閱[這裡](../windows/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="3c3cf-107">For information about planned maintenance in the Resource Manager model, see [here](../windows/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
 
[!INCLUDE [virtual-machines-common-planned-maintenance-schedule](../../../includes/virtual-machines-common-planned-maintenance-schedule.md)]