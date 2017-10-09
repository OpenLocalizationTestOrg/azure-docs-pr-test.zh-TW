---
title: "aaaTroubleshooting Linux VM 配置失敗 |Microsoft 文件"
description: "在 Azure 中建立、重新啟動或調整 Linux VM 大小時，對配置失敗進行疑難排解"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resourece-manager,azure-service-management
ms.assetid: 1ef41144-6dd6-4a56-b180-9d8b3d05eae7
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cjiang
ms.openlocfilehash: 502fbb406b0b4acf086c2586795f69a44cc1a004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-linux-vms-in-azure"></a><span data-ttu-id="0acd0-103">在 Azure 中建立、重新啟動或調整 Linux VM 大小時，對配置失敗進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="0acd0-103">Troubleshoot allocation failures when you create, restart, or resize Linux VMs in Azure</span></span>
<span data-ttu-id="0acd0-104">當您建立 VM、 重新啟動已停止 （取消配置） Vm，或調整 VM 的大小時，Microsoft Azure 配置計算資源 tooyour 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0acd0-104">When you create a VM, restart stopped (deallocated) VMs, or resize a VM, Microsoft Azure allocates compute resources tooyour subscription.</span></span> <span data-ttu-id="0acd0-105">執行這些作業-之前到達 hello Azure 訂用帳戶限制時，您偶爾可能會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="0acd0-105">You may occasionally receive errors when performing these operations -- even before you reach hello Azure subscription limits.</span></span> <span data-ttu-id="0acd0-106">本文說明 hello 一些 hello 的一般配置失敗的原因，並建議可能的補救措施。</span><span class="sxs-lookup"><span data-stu-id="0acd0-106">This article explains hello causes of some of hello common allocation failures and suggests possible remediation.</span></span> <span data-ttu-id="0acd0-107">當您計劃 hello 部署您的服務，hello 資訊可能也很有用。</span><span class="sxs-lookup"><span data-stu-id="0acd0-107">hello information may also be useful when you plan hello deployment of your services.</span></span> <span data-ttu-id="0acd0-108">[當您在 Azure 中建立、重新啟動或調整 Windows VM 大小時，也可以對配置失敗進行疑難排解](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0acd0-108">You can also [troubleshoot allocation failures when you create, restart, or resize Windows VMs in Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

