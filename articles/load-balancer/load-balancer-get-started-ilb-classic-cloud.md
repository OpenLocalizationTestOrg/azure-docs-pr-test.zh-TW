---
title: "aaaCreate Azure 雲端服務的內部負載平衡器 |Microsoft 文件"
description: "了解 toocreate 內部負載平衡器在 hello 傳統部署模型中使用 PowerShell 的方式"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 57966056-0f46-4f95-a295-483ca1ad135d
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: fe7975bca7bec3248626b0ad0fad6823e278ade2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a>開始為雲端服務建立內部負載平衡器 (傳統)

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [雲端服務](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。  本文說明如何使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 了解如何太[使用 hello 資源管理員的模型執行這些步驟](load-balancer-get-started-ilb-arm-ps.md)。

## <a name="configure-internal-load-balancer-for-cloud-services"></a>設定雲端服務的內部負載平衡器

虛擬機器和雲端服務都支援內部負載平衡器。 只有在 hello 雲端服務內仍可使用區域虛擬網路外的雲端服務中建立的內部負載平衡器端點。

hello 內部負載平衡器組態有 toobe hello 以下範例所示，hello 建立 hello hello 雲端服務中的第一次部署期間設定。

> [!IMPORTANT]
> 下列必要條件 toorun hello 步驟是 toohave 已經針對 hello 雲端部署建立虛擬網路。 您將需要 hello 虛擬網路名稱和子網路名稱 toocreate hello 內部負載平衡。

### <a name="step-1"></a>步驟 1

為您的雲端部署，Visual Studio 中開啟 hello 服務組態檔 (.cscfg)，然後加入下列區段 toocreate hello 內部負載平衡 hello 下的最後的 hello"`</Role>`"hello 網路組態項目。

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of hello load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

讓我們加入 hello 值 hello 網路組態檔 tooshow 的外觀。 在 hello 範例中，假設您建立 VNet 子網路 10.0.0.0/24 test_subnet 和靜態 ip 位址 10.0.0.4 呼叫以呼叫"test_vnet"。 hello 負載平衡器將會命名為 testLB。

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

如需 hello 負載平衡器組態結構描述的詳細資訊，請參閱[新增負載平衡器](https://msdn.microsoft.com/library/azure/dn722411.aspx)。

### <a name="step-2"></a>步驟 2

變更 hello 服務定義 (.csdef) 檔案 tooadd 端點 toohello 內部負載平衡。 hello 目前建立的角色執行個體時，hello 服務定義檔會加入 hello 角色執行個體 toohello 內部負載平衡。

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

下列 hello 相同 hello 上述範例中的值，讓我們加入 hello 值 toohello 服務定義檔。

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

hello 網路流量將負載平衡使用 hello testLB 負載平衡器連入要求，也在連接埠 80 傳送 tooworker 角色執行個體使用通訊埠 80。

## <a name="next-steps"></a>後續步驟

[使用來源 IP 同質性設定負載平衡器分配模式](load-balancer-distribution-mode.md)

[設定負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)

