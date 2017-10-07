---
title: "Azure 雲端服務的網際網路對向 aaaCreate 負載平衡器 |Microsoft 文件"
description: "了解如何的 toocreate 網際網路向負載平衡器中針對雲端服務的傳統部署模型"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 0bb16f96-56a6-429f-88f5-0de2d0136756
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: d93cf76d417cbfc744cf07ba48c43a63cc14df69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a>開始為雲端服務建立網際網路面向的負載平衡器

> [!div class="op_single_selector"]
> * [Azure 傳統入口網站](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure 雲端服務](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> 您可以使用 Azure 資源之前，它是 Azure 目前有兩種部署模型的重要 toounderstand: Azure 資源管理員] 和 [傳統。 在使用任何 Azure 資源之前，請先確認您了解 [部署模型和工具](../azure-classic-rm.md) 。 您可以按一下上方的這篇文章 hello hello 索引標籤檢視 hello 文件不同的工具。 本文涵蓋 hello 傳統部署模型。 您也可以[toocreate 網際網路向負載平衡器使用 Azure 資源管理員的如何了解](load-balancer-get-started-internet-arm-ps.md)。

雲端服務會自動以負載平衡器設定，而且可以進行自訂透過 hello 服務模型。

## <a name="create-a-load-balancer-using-hello-service-definition-file"></a>建立負載平衡器使用 hello 服務定義檔

您可以利用 hello Azure SDK for.NET 2.5 tooupdate 您的雲端服務。 在 hello 進行雲端服務的端點設定[服務定義](https://msdn.microsoft.com/library/azure/gg557553.aspx).csdef 檔案。

hello 下列範例示範如何設定雲端部署的 servicedefinition.csdef 檔案：

檢查產生的雲端部署的 hello.csdef 檔案 hello 的程式碼片段，您可以看到 hello 設定外部端點 toouse 連接埠 HTTP 通訊埠 10000、 10001 和 10002 上。

```xml
<ServiceDefinition name=“Tenant“>
    <WorkerRole name=“FERole” vmsize=“Small“>
<Endpoints>
    <InputEndpoint name=“FE_External_Http” protocol=“http” port=“10000“ />
    <InputEndpoint name=“FE_External_Tcp“  protocol=“tcp“  port=“10001“ />
    <InputEndpoint name=“FE_External_Udp“  protocol=“udp“  port=“10002“ />

    <InputEndpointname=“HTTP_Probe” protocol=“http” port=“80” loadBalancerProbe=“MyProbe“ />

    <InstanceInputEndpoint name=“InstanceEP” protocol=“tcp” localPort=“80“>
        <AllocatePublicPortFrom>
            <FixedPortRange min=“10110” max=“10120“  />
        </AllocatePublicPortFrom>
    </InstanceInputEndpoint>
    <InternalEndpoint name=“FE_InternalEP_Tcp” protocol=“tcp“ />
</Endpoints>
    </WorkerRole>
</ServiceDefinition>
```

## <a name="check-load-balancer-health-status-for-cloud-services"></a>檢查雲端服務的負載平衡器健全狀態

hello 的範例如下的健全狀況探查：

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

hello 負載平衡器結合 hello hello 端點資訊以及 hello 探查 toocreate hello 資訊 URL 形式的 hello`http://{DIP of VM}:80/Probe.aspx`可以使用的 tooquery hello hello 服務健全狀況。

hello 服務偵測到定期探查 hello 從相同的 IP 位址。 這是來自 hello 節點的 hello 主機 hello 虛擬機器執行所在的 hello 健全狀況探查要求。 hello 服務都有 toorespond 與 hello 負載平衡器 tooassume hello 服務狀況良好的 HTTP 200 狀態碼。 任何其他 HTTP 狀態碼 (例如 503) 直接採用 hello 離輪替循環的虛擬機器。

hello 探查定義也會控制 hello hello 探查頻率。 在上述範例中，hello 負載平衡器會探查 hello 端點每 5 秒。 如果沒有正面回應收到 10 秒 （兩個探查間隔），關機，假設 hello 探查，而 hello 虛擬機器取得離輪替循環。 同樣地，如果 hello 服務離輪替循環，正面回應收到 hello 服務放回 toorotation 以立即開始。 如果 hello 服務有變動之間狀況良好和狀況不良，hello 負載平衡器可以決定 toodelay hello 重新引進的 hello 服務後 toorotation，直到已經過良好的探查數目。

請檢查 hello 的 hello 服務定義結構描述[健全狀況探查](https://msdn.microsoft.com/library/azure/jj151530.aspx)如需詳細資訊。

## <a name="next-steps"></a>後續步驟

[開始設定內部負載平衡器](load-balancer-get-started-ilb-arm-ps.md)

[設定負載平衡器分配模式](load-balancer-distribution-mode.md)

[設定負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)

