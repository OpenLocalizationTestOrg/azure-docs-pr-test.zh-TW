---
title: "修改 hello 區域網路閘道 IP 位址前置詞和 hello VPN 閘道 IP 位址 |Azure |PowerShell |Microsoft 文件"
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
ms.openlocfilehash: 1353598b39a97fae9bdb424505a5ae2560482654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a><span data-ttu-id="bb64a-103">使用 PowerShell 修改區域網路閘道設定</span><span class="sxs-lookup"><span data-stu-id="bb64a-103">Modify local network gateway settings using PowerShell</span></span>

<span data-ttu-id="bb64a-104">有時候您的本機網路閘道 AddressPrefix 或 GatewayIPAddress hello 設定變更。</span><span class="sxs-lookup"><span data-stu-id="bb64a-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="bb64a-105">本文章將示範如何 toomodify 您區域網路閘道的設定。</span><span class="sxs-lookup"><span data-stu-id="bb64a-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="bb64a-106">您也可以修改這些設定，使用另一個方法從 hello 下列清單中選取不同的選項：</span><span class="sxs-lookup"><span data-stu-id="bb64a-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bb64a-107">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="bb64a-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="bb64a-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb64a-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="bb64a-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bb64a-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="bb64a-110"><a name="before"></a>開始之前</span><span class="sxs-lookup"><span data-stu-id="bb64a-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="bb64a-111">安裝 hello hello Azure 資源管理員的 PowerShell 指令程式最新版本。</span><span class="sxs-lookup"><span data-stu-id="bb64a-111">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="bb64a-112">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)如需安裝 hello PowerShell cmdlet 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="bb64a-112">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing hello PowerShell cmdlets.</span></span>

## <span data-ttu-id="bb64a-113"><a name="ipaddprefix"></a>修改 IP 位址首碼</span><span class="sxs-lookup"><span data-stu-id="bb64a-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="bb64a-114"><a name="gwip"></a>修改 hello 閘道 IP 位址</span><span class="sxs-lookup"><span data-stu-id="bb64a-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="bb64a-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bb64a-115">Next steps</span></span>

<span data-ttu-id="bb64a-116">您可以驗證閘道連線。</span><span class="sxs-lookup"><span data-stu-id="bb64a-116">You can verify your gateway connection.</span></span> <span data-ttu-id="bb64a-117">請參閱 [驗證閘道連線](vpn-gateway-verify-connection-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="bb64a-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>