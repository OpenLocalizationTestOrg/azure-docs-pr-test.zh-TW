---
title: "aaaVerify VPN 閘道連線 |Microsoft 文件"
description: "本文章將示範如何 tooverify 的虛擬網路 VPN 閘道連線。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 7e3d1043-caa9-4472-96d3-832f4e2c91ee
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2017
ms.author: cherylmc
ms.openlocfilehash: 0d3da94a76b36251d629f82b1575328c7ac10b26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="verify-a-vpn-gateway-connection"></a><span data-ttu-id="82b78-103">確認 VPN 閘道連線</span><span class="sxs-lookup"><span data-stu-id="82b78-103">Verify a VPN Gateway connection</span></span>

<span data-ttu-id="82b78-104">本文章將示範如何 tooverify 傳統 hello 和資源管理員部署模型的 VPN 閘道連線。</span><span class="sxs-lookup"><span data-stu-id="82b78-104">This article shows you how tooverify a VPN gateway connection for both hello classic and Resource Manager deployment models.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="82b78-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="82b78-105">Azure portal</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a><span data-ttu-id="82b78-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="82b78-106">PowerShell</span></span>

<span data-ttu-id="82b78-107">tooverify hello 資源管理員部署的 VPN 閘道連線模型使用 PowerShell，請安裝 hello 最新版 hello [Azure 資源管理員 PowerShell cmdlet](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="82b78-107">tooverify a VPN gateway connection for hello Resource Manager deployment model using PowerShell, install hello latest version of hello [Azure Resource Manager PowerShell cmdlets](/powershell/azure/overview).</span></span>

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a><span data-ttu-id="82b78-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="82b78-108">Azure CLI</span></span>

<span data-ttu-id="82b78-109">tooverify hello 資源管理員部署的 VPN 閘道連線模型使用 Azure CLI，請安裝 hello 最新版 hello [CLI 命令](https://docs.microsoft.com/cli/azure/install-azure-cli)（2.0 或更新版本）。</span><span class="sxs-lookup"><span data-stu-id="82b78-109">tooverify a VPN gateway connection for hello Resource Manager deployment model using Azure CLI, install hello latest version of hello [CLI commands](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 or later).</span></span>

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a><span data-ttu-id="82b78-110">Azure 入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="82b78-110">Azure portal (classic)</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a><span data-ttu-id="82b78-111">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="82b78-111">PowerShell (classic)</span></span>

<span data-ttu-id="82b78-112">您的 VPN 閘道連線的 hello 傳統部署模型使用 PowerShell、 tooverify 安裝 hello Azure PowerShell cmdlet hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="82b78-112">tooverify your VPN gateway connection for hello classic deployment model using PowerShell, install hello latest versions of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="82b78-113">要確定 toodownload 並安裝 hello[服務管理](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0)模組。</span><span class="sxs-lookup"><span data-stu-id="82b78-113">Be sure toodownload and install hello [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module.</span></span> <span data-ttu-id="82b78-114">使用 'Add-azureaccount' toolog toohello 傳統部署模型中。</span><span class="sxs-lookup"><span data-stu-id="82b78-114">Use 'Add-AzureAccount' toolog in toohello classic deployment model.</span></span>

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a><span data-ttu-id="82b78-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="82b78-115">Next steps</span></span>

* <span data-ttu-id="82b78-116">您可以將虛擬機器 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="82b78-116">You can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="82b78-117">請參閱 [建立網站的虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 以取得相關步驟。</span><span class="sxs-lookup"><span data-stu-id="82b78-117">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
