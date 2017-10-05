---
title: "Azure 中 Windows VM 的代理程式和延伸模組 | Microsoft Docs"
description: "提供代理程式和擴充功能的概觀，以及如何使用 Windows VM 上的傳統部署模型來安裝代理程式。"
services: virtual-machines-windows
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 820cdad0-6767-4d9e-9749-6169e76505ad
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: rasquill
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c94332314668dc7e58ed84b20945a548c0443f84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="about-the-virtual-machine-agent-and-extensions-for-windows-vms"></a><span data-ttu-id="74d8e-103">有關 Windows VM 的虛擬機器代理程式和擴充功能</span><span class="sxs-lookup"><span data-stu-id="74d8e-103">About the virtual machine agent and extensions for Windows VMs</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74d8e-104">Azure 建立和處理資源的部署模型有二種： [Resource Manager 和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="74d8e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="74d8e-105">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="74d8e-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="74d8e-106">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="74d8e-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="74d8e-107">如需使用 Resource Manager 的 VM 代理程式和擴充的詳細資訊，請參閱[這裡](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="74d8e-107">For information about VM agents and extensions using Resource Manager, see [here](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-agents-and-extensions](../../../../includes/virtual-machines-common-classic-agents-and-extensions.md)]