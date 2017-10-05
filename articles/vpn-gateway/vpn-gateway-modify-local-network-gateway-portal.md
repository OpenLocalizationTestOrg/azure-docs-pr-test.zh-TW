---
title: "修改區域網路閘道 IP 位址首碼和 VPN 閘道 IP 位址| Azure| 入口網站| Microsoft Docs"
description: "本文逐步解說如何使用 Azure 入口網站來變更區域網路閘道的 IP 位址首碼。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: bdd6f90fe97408bd45a72adf58bfdc190207de46
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="modify-local-network-gateway-settings-using-the-azure-portal"></a><span data-ttu-id="f32ec-103">使用 Azure 入口網站修改區域網路閘道設定</span><span class="sxs-lookup"><span data-stu-id="f32ec-103">Modify local network gateway settings using the Azure portal</span></span>

<span data-ttu-id="f32ec-104">有時候區域網路閘道 AddressPrefix 或 GatewayIPAddress 的設定會變更。</span><span class="sxs-lookup"><span data-stu-id="f32ec-104">Sometimes the settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="f32ec-105">本文將說明如何修改區域網路閘道設定。</span><span class="sxs-lookup"><span data-stu-id="f32ec-105">This article shows you how to modify your local network gateway settings.</span></span> <span data-ttu-id="f32ec-106">您也可以從下列清單選取不同的選項來使用不同的方法修改這些設定：</span><span class="sxs-lookup"><span data-stu-id="f32ec-106">You can also modify these settings using a different method by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f32ec-107">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f32ec-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="f32ec-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f32ec-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="f32ec-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f32ec-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <span data-ttu-id="f32ec-110"><a name="ipaddprefix"></a>修改 IP 位址首碼</span><span class="sxs-lookup"><span data-stu-id="f32ec-110"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

<span data-ttu-id="f32ec-111">當您修改 IP 位址首碼時，使用的步驟會依您的區域網路閘道是否有連線而不同。</span><span class="sxs-lookup"><span data-stu-id="f32ec-111">When you modify IP address prefixes, the steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <span data-ttu-id="f32ec-112"><a name="gwip"></a>修改閘道 IP 位址</span><span class="sxs-lookup"><span data-stu-id="f32ec-112"><a name="gwip"></a>Modify the gateway IP address</span></span>

<span data-ttu-id="f32ec-113">如果您想要連線的 VPN 裝置已變更其公用 IP 位址，您需要修改區域網路閘道，以反映該變更。</span><span class="sxs-lookup"><span data-stu-id="f32ec-113">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="f32ec-114">當您變更公用 IP 位址時，使用的步驟會依您的區域網路閘道是否有連線而不同。</span><span class="sxs-lookup"><span data-stu-id="f32ec-114">When you change the public IP address, the steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a><span data-ttu-id="f32ec-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f32ec-115">Next steps</span></span>

<span data-ttu-id="f32ec-116">您可以驗證閘道連線。</span><span class="sxs-lookup"><span data-stu-id="f32ec-116">You can verify your gateway connection.</span></span> <span data-ttu-id="f32ec-117">請參閱 [驗證閘道連線](vpn-gateway-verify-connection-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="f32ec-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>