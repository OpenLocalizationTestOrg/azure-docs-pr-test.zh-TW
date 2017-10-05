---
title: "管理 Azure 中 Linux VM 的可用性 | Microsoft Docs"
description: "了解如何使用多部虛擬機器，確保 Azure 中 Linux 應用程式的高可用性。"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 891c852a-84c0-4940-a61e-ada6e185bf37
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f153a740e4814e2573e53b9c051d24c30ff9088f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-the-availability-of-linux-virtual-machines"></a><span data-ttu-id="0899e-103">管理 Linux 虛擬機器的可用性</span><span class="sxs-lookup"><span data-stu-id="0899e-103">Manage the availability of Linux virtual machines</span></span>

<span data-ttu-id="0899e-104">了解如何設定及管理多部虛擬機器，以確保 Azure 中 Linux 應用程式的高可用性。</span><span class="sxs-lookup"><span data-stu-id="0899e-104">Learn ways to set up and manage multiple virtual machines to ensure high availability for your Linux application in Azure.</span></span> <span data-ttu-id="0899e-105">您也可以[管理 Windows 虛擬機器的可用性](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0899e-105">You can also [manage the availability of Windows virtual machines](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="0899e-106">如需有關使用 CLI 在 Resource Manger 部署模型中建立可用性設定組的指示，請參閱 [azure availset：用來管理可用性設定組的命令](../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets)。</span><span class="sxs-lookup"><span data-stu-id="0899e-106">For instructions on creating an availability set using CLI in the Resource Manager deployment model, see [azure availset: commands to manage your availability sets](../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets).</span></span>

[!INCLUDE [virtual-machines-common-manage-availability](../../../includes/virtual-machines-common-manage-availability.md)]

## <a name="next-steps"></a><span data-ttu-id="0899e-107">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0899e-107">Next steps</span></span>
<span data-ttu-id="0899e-108">若要深入了解如何對虛擬機器進行負載平衡，請參閱 [對虛擬機器進行負載平衡](../virtual-machines-linux-load-balance.md)。</span><span class="sxs-lookup"><span data-stu-id="0899e-108">To learn more about load balancing your virtual machines, see [Load Balancing virtual machines](../virtual-machines-linux-load-balance.md).</span></span>
