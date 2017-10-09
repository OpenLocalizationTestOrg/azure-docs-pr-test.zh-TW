---
title: "網路安全性群組與 Azure 網路監看員的 aaaIntroduction tooflow 記錄 |Microsoft 文件"
description: "此頁面說明 toouse NSG 流程記錄 Azure 網路監看員的一項功能的方式"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: da85e946147b14717144cb47d1c742057c6dfa24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooflow-logging-for-network-security-groups"></a>網路安全性群組的簡介 tooflow 記錄

網路安全性小組流程記錄檔是 tooview ingress 和 egress IP 流量，透過網路安全性群組相關的資訊可讓您的網路監看員的功能。 這些流程記錄檔會寫入以 json 格式，並顯示輸出和輸入每個規則為基礎的流量，hello NIC hello 流程適用於，5 個 tuple hello 流程 （來源/目的地 IP，來源/目的地連接埠通訊協定） 的資訊，並允許流量，如果 hello 或被拒絕。

![流量記錄概觀][1]

流程記錄目標網路安全性群組，而不會顯示 hello 相同 hello 做其他記錄檔。 流程記錄會儲存在儲存體帳戶和下列 hello 記錄路徑內，hello 下列範例所示：

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

hello 相同套用 tooflow 記錄的其他記錄檔所見的保留原則。 記錄檔具有可設定為 1 天 too365 天的保留原則。 如果未設定保留原則，就會永遠保留 hello 記錄檔。

## <a name="log-file"></a>記錄檔

流量記錄有多個屬性。 hello 下列清單是 hello NSG 流程記錄中傳回的 hello 屬性的清單：

* **時間**-時間時記錄 hello 事件
* **systemId** - 網路安全性群組資源識別碼。
* **類別**-hello 類別 hello 事件，這是永遠是 NetworkSecurityGroupFlowEvent
* **resourceid** -hello hello NSG 的資源 Id
* **operationName** - 一律是 NetworkSecurityGroupFlowEvents
* **屬性**-hello 流程的屬性集合
    * **版本**-hello 流程記錄事件結構描述版本號碼
    * **flows** - 流量的集合。 這個屬性有多個適用於不同規則的項目
        * **規則**-列出哪些 hello 流量的規則
            * **flows** - 流量的集合
                * **mac** -hello hello 收集 hello 流程所在的 VM hello NIC 的 MAC 位址
                * **flowTuples** -包含以逗號分隔格式的 hello 流程 tuple 的多個屬性的字串
                    * **時間戳記**-hello 流程發生 UNIX EPOCH 格式時，這個值會是 hello 時間戳記
                    * **來源 IP** -hello 來源 IP
                    * **目的地 IP** -hello 目的地 IP
                    * **來源連接埠**-hello 來源連接埠
                    * **目的地連接埠**-hello 目的地連接埠
                    * **通訊協定**-hello hello 流量的通訊協定。 有效值為 **T** (若為 TCP) 和 **U** (若為 UDP)
                    * **流量流程**-hello hello 流量的方向。 有效值為 **I** (若為輸入) 和 **O** (若為輸出)。
                    * **流量** - 流量受到允許或拒絕。 有效值為 **A** (若允許) 和 **D** (若拒絕)。


hello 的範例如下的流量記錄檔。 您可以看到有遵循 hello hello 前面一節中所述的屬性清單的多筆記錄。 

> [!NOTE]
> Hello flowTuples 屬性中的值是以逗號分隔清單。
 
```json
{
    "records": 
    [
        
        {
             "time": "2017-02-16T22:00:32.8950000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282421,42.119.146.95,10.1.0.4,51529,5358,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282370,163.28.66.17,10.1.0.4,61771,3389,T,I,A","1487282393,5.39.218.34,10.1.0.4,58596,3389,T,I,A","1487282393,91.224.160.154,10.1.0.4,61540,3389,T,I,A","1487282423,13.76.89.229,10.1.0.4,53163,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:01:32.8960000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282481,195.78.210.194,10.1.0.4,53,1732,U,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282435,61.129.251.68,10.1.0.4,57776,3389,T,I,A","1487282454,84.25.174.170,10.1.0.4,59085,3389,T,I,A","1487282477,77.68.9.50,10.1.0.4,65078,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:02:32.9040000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282492,175.182.69.29,10.1.0.4,28918,5358,T,I,D","1487282505,71.6.216.55,10.1.0.4,8080,8080,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282512,91.224.160.154,10.1.0.4,59046,3389,T,I,A"]}]}]}
        }
        ,
        ...
```

## <a name="next-steps"></a>後續步驟

了解 tooenable 流程造訪的記錄方式[啟用流程記錄](network-watcher-nsg-flow-logging-portal.md)。

瀏覽[網路安全性群組 (NSG) 的 Log Analytics](../virtual-network/virtual-network-nsg-manage-log.md)，以了解 NSG 記錄。

瀏覽[使用 IP 流量驗證來驗證流量](network-watcher-check-ip-flow-verify-portal.md)，以了解流量在 VM 上受到允許或拒絕

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

