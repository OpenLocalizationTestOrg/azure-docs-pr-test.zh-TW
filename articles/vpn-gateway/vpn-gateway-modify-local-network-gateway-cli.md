---
title: "修改區域網路閘道 IP 位址首碼和 VPN 閘道 IP 位址| Azure| CLI| Microsoft Docs"
description: "本文逐步解說如何使用 Azure CLI 變更區域網路閘道的 IP 位址首碼。"
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
ms.date: 11/29/2017
ms.author: cherylmc
ms.openlocfilehash: d62fa14ea24a9b62e793ef7022a761897984df32
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="modify-local-network-gateway-settings-using-the-azure-cli"></a>使用 Azure CLI 修改區域網路閘道設定

有時候區域網路閘道位址首碼或閘道 IP 位址的設定會變更。 本文將說明如何修改區域網路閘道設定。 您也可以從下列清單選取不同的選項來使用不同的方法修改這些設定：

> [!div class="op_single_selector"]
> * [Azure 入口網站](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [Azure CLI](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <a name="before"></a>開始之前

安裝 CLI 命令的最新版本 (2.0 版或更新版本)。 如需關於安裝 CLI 命令的資訊，請參閱[安裝 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)。

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <a name="ipaddprefix"></a>修改 IP 位址首碼

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <a name="gwip"></a>修改閘道 IP 位址

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a>後續步驟

您可以驗證閘道連線。 請參閱 [驗證閘道連線](vpn-gateway-verify-connection-resource-manager.md)。

