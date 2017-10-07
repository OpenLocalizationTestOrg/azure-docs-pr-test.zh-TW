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
# <a name="modify-local-network-gateway-settings-using-powershell"></a>使用 PowerShell 修改區域網路閘道設定

有時候您的本機網路閘道 AddressPrefix 或 GatewayIPAddress hello 設定變更。 本文章將示範如何 toomodify 您區域網路閘道的設定。 您也可以修改這些設定，使用另一個方法從 hello 下列清單中選取不同的選項：

> [!div class="op_single_selector"]
> * [Azure 入口網站](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [Azure CLI](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <a name="before"></a>開始之前

安裝 hello hello Azure 資源管理員的 PowerShell 指令程式最新版本。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)如需安裝 hello PowerShell cmdlet 的詳細資訊。

## <a name="ipaddprefix"></a>修改 IP 位址首碼

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="gwip"></a>修改 hello 閘道 IP 位址

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>後續步驟

您可以驗證閘道連線。 請參閱 [驗證閘道連線](vpn-gateway-verify-connection-resource-manager.md)。