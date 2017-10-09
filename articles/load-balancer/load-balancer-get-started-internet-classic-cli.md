---
title: "aaaCreate 網際網路對向負載平衡器-Azure CLI 傳統 |Microsoft 文件"
description: "了解如何在模型中使用傳統部署使用網際網路對向負載平衡器 toocreate hello Azure CLI"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: e433a824-4a8a-44d2-8765-a74f52d4e584
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e6070cbc574f74bca0cccb960ff192847d6511bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-cli"></a>開始建立網際網路對向 hello Azure CLI 中的負載平衡器 （傳統）

> [!div class="op_single_selector"]
> * [Azure 傳統入口網站](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure 雲端服務](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> 您可以使用 Azure 資源之前，它是 Azure 目前有兩種部署模型的重要 toounderstand: Azure 資源管理員] 和 [傳統。 在使用任何 Azure 資源之前，請先確認您了解 [部署模型和工具](../azure-classic-rm.md) 。 您可以按一下上方的這篇文章 hello hello 索引標籤檢視 hello 文件不同的工具。 本文涵蓋 hello 傳統部署模型。 您也可以[toocreate 網際網路向負載平衡器使用 Azure 資源管理員的如何了解](load-balancer-get-started-internet-arm-ps.md)。

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a>使用 CLI 逐步建立網際網路面向的負載平衡器

本指南也說明如何 toocreate 網際網路負載平衡器根據上面的 hello 案例。

1. 如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。
2. 執行 hello **azure 組態模式**命令 tooswitch tooclassic 模式，如下所示。

    ```azurecli
    azure config mode asm
    ```

    預期的輸出：

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a>建立端點與負載平衡器集

hello 案例假設 hello 虛擬機器 」 web1"和"web2 」 所建立。
本指南將使用連接埠 80 作為公用連接埠，以及 80 作為本機連接埠，建立負載平衡器集。 探查連接埠也會設定連接埠 80 和具名的 hello 負載平衡器設定 「 lbset"。

### <a name="step-1"></a>步驟 1

建立 hello 第一個端點和負載平衡器設定使用`azure network vm endpoint create`虛擬機器 」 web1"。

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a>步驟 2

新增第二個虛擬機器 」 web2"toohello 負載平衡器集。

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a>步驟 3

確認 hello 負載平衡器組態使用`azure vm show`。

```azurecli
azure vm show web1
```

hello 輸出將會：

    data:    DNSName "contoso.cloudapp.net"
    data:    Location "East US"
    data:    VMName "web1"
    data:    IPAddress "10.0.0.5"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-2015
    6-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "joaoma-1-web1-0-201509251804250879"
    data:    OSDisk mediaLink "https://XXXXXXXXXXXXXXX.blob.core.windows.
    /vhds/joaomatest-web1-2015-09-25.vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Se
    r-2012-R2-20150916-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "XXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 name "XXXXXXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    Network Endpoints 0 loadBalancedEndpointSetName "lbset"
    data:    Network Endpoints 0 localPort 80
    data:    Network Endpoints 0 name "tcp-80-80"
    data:    Network Endpoints 0 port 80
    data:    Network Endpoints 0 loadBalancerProbe port 80
    data:    Network Endpoints 0 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 0 loadBalancerProbe intervalInSeconds 15
    data:    Network Endpoints 0 loadBalancerProbe timeoutInSeconds 31
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 5986
    data:    Network Endpoints 1 name "PowerShell"
    data:    Network Endpoints 1 port 5986
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 3389
    data:    Network Endpoints 2 name "Remote Desktop"
    data:    Network Endpoints 2 port 58081
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a>為虛擬機器建立遠端桌面端點

您可以從公用連接埠 tooa 本機連接埠的特定虛擬機器使用建立遠端桌面端點 tooforward 網路流量`azure vm endpoint create`。

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a>從負載平衡器移除虛擬機器

您必須從 hello 虛擬機器負載平衡器集 toodelete hello 關聯端點 toohello。 一旦移除 hello 端點時，hello 虛擬機器不屬於 toohello 負載平衡器不再設定。

使用 hello 上述範例中，您可以移除虛擬機器 」 web1"建立 hello 端點從負載平衡器使用 hello 命令"lbset" `azure vm endpoint delete`。

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> 您可以瀏覽選項 toomanage 端點使用 hello 命令`azure vm endpoint --help`

## <a name="next-steps"></a>後續步驟

[開始設定內部負載平衡器](load-balancer-get-started-ilb-arm-ps.md)

[設定負載平衡器分配模式](load-balancer-distribution-mode.md)

[設定負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)
