---
title: "<span data-ttu-id=\"6d8fa-101\">Azure 中 Linux VM 的代理程式和延伸模組 | Microsoft Docs</span><span class=\"sxs-lookup\"><span data-stu-id=\"6d8fa-101\">Linux VM agent and extensions in Azure | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"6d8fa-102\">提供代理程式和擴充功能的概觀，以及如何使用 Linux VM 上的傳統部署模型來安裝代理程式。</span><span class=\"sxs-lookup\"><span data-stu-id=\"6d8fa-102\">Gives an overview of the agent and extensions, and how to install the agent, using the classic deployment model on a Linux VM.</span></span>"
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b41e3b21-9132-4d8d-804d-34920b2d0942
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: rasquill
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06b802c408ea5d1b2b40d05321e1a0014e99ca8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="about-the-virtual-machine-agent-and-extensions-for-linux"></a><span data-ttu-id="6d8fa-103">有關 Linux 的虛擬機器代理程式和擴充功能</span><span class="sxs-lookup"><span data-stu-id="6d8fa-103">About the virtual machine agent and extensions for Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6d8fa-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="6d8fa-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6d8fa-105">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="6d8fa-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="6d8fa-106">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="6d8fa-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="6d8fa-107">如需使用 Resource Manager 的 VM 代理程式和擴充的詳細資訊，請參閱[這裡](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="6d8fa-107">For information about VM agents and extensions using Resource Manager, see [here](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-agents-and-extensions](../../../../includes/virtual-machines-common-classic-agents-and-extensions.md)]
