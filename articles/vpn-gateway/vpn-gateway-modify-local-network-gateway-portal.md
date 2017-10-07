---
title: "修改 hello 區域網路閘道 IP 位址前置詞和 hello VPN 閘道 IP 位址 |Azure |入口網站 |Microsoft 文件"
description: "這篇文章會引導您變更您使用 hello Azure 入口網站的本機網路閘道的 IP 位址首碼。"
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
ms.openlocfilehash: 001df7b748ccc234d87aab3501a4f0e4ddfe60f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-portal"></a>修改使用 hello Azure 入口網站的區域網路閘道設定

有時候您的本機網路閘道 AddressPrefix 或 GatewayIPAddress hello 設定變更。 本文章將示範如何 toomodify 您區域網路閘道的設定。 您也可以修改這些設定，使用另一個方法從 hello 下列清單中選取不同的選項：

> [!div class="op_single_selector"]
> * [Azure 入口網站](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [Azure CLI](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <a name="ipaddprefix"></a>修改 IP 位址首碼

當您修改 IP 位址前置詞時，hello 所遵循的步驟會取決於您的本機網路閘道是否有連線。

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <a name="gwip"></a>修改 hello 閘道 IP 位址

如果您想 tooconnect toohas hello VPN 裝置變更其公用 IP 位址，您會需要 toomodify hello 區域網路閘道 tooreflect 變更。 當您變更 hello 公用 IP 位址時，hello 所遵循的步驟會取決於您的本機網路閘道是否有連線。

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a>後續步驟

您可以驗證閘道連線。 請參閱 [驗證閘道連線](vpn-gateway-verify-connection-resource-manager.md)。