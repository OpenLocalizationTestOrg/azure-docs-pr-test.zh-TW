---
title: "修改 hello 區域網路閘道 IP 位址前置詞和 hello VPN 閘道 IP 位址 |Azure |CLI |Microsoft 文件"
description: "這篇文章會引導您使用 Azure CLI hello 您區域網路閘道的 IP 位址首碼的變更。"
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
ms.openlocfilehash: 4b8bbf3e9d3d42ac2d12f87360fa0a4134c57a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-cli"></a><span data-ttu-id="d7b4f-103">修改區域網路閘道設定使用 Azure CLI hello</span><span class="sxs-lookup"><span data-stu-id="d7b4f-103">Modify local network gateway settings using hello Azure CLI</span></span>

<span data-ttu-id="d7b4f-104">有時候您的閘道 IP 位址或位址首碼的區域網路閘道的 hello 設定變更。</span><span class="sxs-lookup"><span data-stu-id="d7b4f-104">Sometimes hello settings for your local network gateway Address Prefix or Gateway IP Address change.</span></span> <span data-ttu-id="d7b4f-105">本文章將示範如何 toomodify 您區域網路閘道的設定。</span><span class="sxs-lookup"><span data-stu-id="d7b4f-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="d7b4f-106">您也可以修改這些設定，使用另一個方法從 hello 下列清單中選取不同的選項：</span><span class="sxs-lookup"><span data-stu-id="d7b4f-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d7b4f-107">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d7b4f-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="d7b4f-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7b4f-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="d7b4f-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d7b4f-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="d7b4f-110"><a name="before"></a>開始之前</span><span class="sxs-lookup"><span data-stu-id="d7b4f-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="d7b4f-111">安裝 hello 最新版本 （2.0 或更新版本） 的 hello CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="d7b4f-111">Install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="d7b4f-112">如需安裝 hello CLI 命令的資訊，請參閱[安裝 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="d7b4f-112">For information about installing hello CLI commands, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="d7b4f-113"><a name="ipaddprefix"></a>修改 IP 位址首碼</span><span class="sxs-lookup"><span data-stu-id="d7b4f-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <span data-ttu-id="d7b4f-114"><a name="gwip"></a>修改 hello 閘道 IP 位址</span><span class="sxs-lookup"><span data-stu-id="d7b4f-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="d7b4f-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d7b4f-115">Next steps</span></span>

<span data-ttu-id="d7b4f-116">您可以驗證閘道連線。</span><span class="sxs-lookup"><span data-stu-id="d7b4f-116">You can verify your gateway connection.</span></span> <span data-ttu-id="d7b4f-117">請參閱 [驗證閘道連線](vpn-gateway-verify-connection-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="d7b4f-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

