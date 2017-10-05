---
title: "修改區域網路閘道 IP 位址前置詞和 VPN 閘道 IP 位址| Azure| PowerShell| Microsoft Docs"
description: "本文逐步解說如何使用 PowerShell 來變更區域網路閘道的 IP 位址首碼"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c7db48f-d09a-44e7-836f-1fb6930389df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 2a095b96a8c352abeca72640d37c0d629b447763
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a><span data-ttu-id="44c4c-103">使用 PowerShell 修改區域網路閘道設定</span><span class="sxs-lookup"><span data-stu-id="44c4c-103">Modify local network gateway settings using PowerShell</span></span>

<span data-ttu-id="44c4c-104">有時候區域網路閘道 AddressPrefix 或 GatewayIPAddress 的設定會變更。</span><span class="sxs-lookup"><span data-stu-id="44c4c-104">Sometimes the settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="44c4c-105">本文將說明如何修改區域網路閘道設定。</span><span class="sxs-lookup"><span data-stu-id="44c4c-105">This article shows you how to modify your local network gateway settings.</span></span> <span data-ttu-id="44c4c-106">您也可以從下列清單選取不同的選項來使用不同的方法修改這些設定：</span><span class="sxs-lookup"><span data-stu-id="44c4c-106">You can also modify these settings using a different method by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="44c4c-107">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="44c4c-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="44c4c-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="44c4c-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="44c4c-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="44c4c-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="44c4c-110"><a name="before"></a>開始之前</span><span class="sxs-lookup"><span data-stu-id="44c4c-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="44c4c-111">安裝最新版的 Azure Resource Manager PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="44c4c-111">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="44c4c-112">如需如何安裝 PowerShell Cmdlet 的詳細資訊，請參閱[如何安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。</span><span class="sxs-lookup"><span data-stu-id="44c4c-112">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span></span>

## <span data-ttu-id="44c4c-113"><a name="ipaddprefix"></a>修改 IP 位址首碼</span><span class="sxs-lookup"><span data-stu-id="44c4c-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="44c4c-114"><a name="gwip"></a>修改閘道 IP 位址</span><span class="sxs-lookup"><span data-stu-id="44c4c-114"><a name="gwip"></a>Modify the gateway IP address</span></span>

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="44c4c-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="44c4c-115">Next steps</span></span>

<span data-ttu-id="44c4c-116">您可以驗證閘道連線。</span><span class="sxs-lookup"><span data-stu-id="44c4c-116">You can verify your gateway connection.</span></span> <span data-ttu-id="44c4c-117">請參閱 [驗證閘道連線](vpn-gateway-verify-connection-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="44c4c-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>