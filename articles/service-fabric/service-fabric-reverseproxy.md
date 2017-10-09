---
title: "Service Fabric aaaAzure 反向 proxy |Microsoft 文件"
description: "用於從內部和外部 hello 叢集通訊 toomicroservices Service Fabric 反向 proxy。"
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a>Azure Service Fabric 中的反向 Proxy
內建於 Azure Service Fabric hello 反向 proxy 位址 microservices 公開 HTTP 端點的 hello Service Fabric 叢集中。

## <a name="microservices-communication-model"></a>微服務通訊模型
Service Fabric 中的 Microservices 通常子集 hello 叢集中虛擬機器上執行，並可以從一個虛擬機器 tooanother 移動基於各種原因。 因此，microservices hello 端點可以動態變更。 hello 典型模式 toocommunicate toohello 微服務是 hello 下列解決迴圈：

1. 解決一開始是透過 hello 命名服務的 hello 服務位置。
2. 連接 toohello 服務。
3. 判斷連接失敗的 hello 原因和解決 hello 服務位置，必要時。

此程序通常牽涉到包裝在實作 hello 服務解析和重試原則的重試迴圈中的用戶端通訊程式庫。
如需詳細資訊，請參閱[連線至服務並與其進行通訊](service-fabric-connect-and-communicate-with-services.md)。

### <a name="communicating-by-using-hello-reverse-proxy"></a>使用 hello 反向 proxy 通訊
服務網狀架構中的 hello 反向 proxy 會 hello 叢集中的所有 hello 節點上執行。 它代表用戶端上執行 hello 整個服務解析程序，接著才遞交 hello 用戶端要求。 因此，在 hello 叢集執行的用戶端可以使用任何用戶端 HTTP 通訊程式庫 tootalk toohello 目標服務使用 hello 反向 proxy 上執行的本機 hello 相同的節點。

![內部通訊][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a>到達 microservices 從外部 hello 叢集
microservices hello 預設外部通訊模型是選擇加入的模型，其中每個服務無法存取直接來自外部用戶端。 [Azure 負載平衡器](../load-balancer/load-balancer-overview.md)，這是 microservices 和外部的用戶端之間的網路界限執行網路位址轉譯，以及轉送外部要求 toointernal IP:port 端點。 toomake 微服務端點直接存取 tooexternal 用戶端，您必須先設定負載平衡器 tooforward 流量 tooeach 埠 hello 服務會使用 hello 叢集中。 此外，大部分 microservices，特別是可設定狀態 microservices 生活 hello 叢集的所有節點上。 hello microservices 可以在容錯移轉節點之間移動。 在這種情況下，負載平衡器無法有效地判斷 hello 位置 hello 複本 toowhich hello 目標節點它應該轉送流量。

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a>到達 microservices 透過從外部 hello 叢集 hello 反向 proxy
您不需要設定負載平衡器中的 hello 的個別服務的連接埠，您可以設定只 hello 連接埠 hello 反向 proxy 負載平衡器中。 此設定可讓用戶端 hello 叢集外使用 hello 反向 proxy，而不需要其他設定的連接 hello 叢集內的服務。

![外部通訊][0]

> [!WARNING]
> 當您在負載平衡器設定 hello 反向 proxy 的連接埠時，hello 叢集中的所有 microservices 公開 （expose) 的 HTTP 端點都都可以從 hello 叢集外定址。
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a>URI 格式，以解決服務使用 hello 反向 proxy
hello 反向 proxy 會使用特定的統一資源識別元 (URI) 格式 tooidentify hello 服務磁碟分割 toowhich hello 連入要求應該轉送：

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* **http （s):** hello 反向 proxy 可以設定的 tooaccept HTTP 或 HTTPS 流量。 HTTPS 轉寄，請參閱太[tooa 安全服務連接與 hello 反向 proxy](service-fabric-reverseproxy-configure-secure-communication.md)一旦反向 proxy 安裝 toolisten 程式 HTTPS。
* **叢集的完整的網域名稱 (FQDN) |內部 IP:**外部的用戶端，您可以設定 hello 反向 proxy，因此可以存取透過 hello 叢集網域，例如 mycluster.eastus.cloudapp.azure.com。根據預設，hello 反向 proxy 執行每個節點上。 內部流量，hello 反向 proxy 可以連線到 localhost 或任何內部節點 IP，例如 10.0.0.1。
* **連接埠：**這是 hello 連接埠，例如 19081，已指定為 hello 反向 proxy。
* **ServiceInstanceName:**這是 hello 嘗試 tooreach hello 沒有部署的 hello 服務執行個體的完整限定名稱"fabric: /"配置。 比方說，tooreach hello *fabric: / myapp/myservice/*服務，您會使用*myapp/myservice*。

    hello 服務執行個體名稱是區分大小寫。 Hello URL 中的 hello 服務執行個體名稱中使用不同的大小寫導致 hello 要求 toofail 404 （找不到）。
* **後置詞路徑：**這是 hello 實際的 URL 路徑，例如*myapi/值/新增/3*，針對您想要 tooconnect hello 服務。
* **PartitionKey:**資料分割的服務，這是 hello 資料分割的 tooreach hello 計算的資料分割索引鍵。 請注意，這是*不*hello 資料分割識別碼 GUID。 這個參數不需要使用 hello 單一資料分割配置的服務。
* **PartitionKind:**這是 hello 服務資料分割配置。 這可以是 'Int64Range' 或 'Named'。 這個參數不需要使用 hello 單一資料分割配置的服務。
* **ListenerName** hello hello 服務端點會 hello 表單的 {< 端點 >: {"Listener1":"Endpoint1"、"Listener2":"Endpoint2"}}。 當 hello 服務會公開多個端點時，這會識別 hello 端點應該送給 hello 用戶端要求。 這可以省略如果 hello 服務只能有一個接聽程式。
* **TargetReplicaSelector**這會指定應該如何選取 hello 目標複本或執行個體。
  * Hello 目標服務可設定狀態時，hello TargetReplicaSelector 可以是 hello 下列其中之一: 'PrimaryReplica'、 'RandomSecondaryReplica，' 或 'RandomReplica'。 若未指定這個參數，hello 預設值是 'PrimaryReplica'。
  * Hello 目標服務無狀態時，反向 proxy 會挑選 hello 服務磁碟分割 tooforward hello 要求的隨機執行個體。
* **逾時：**這會指定 hello hello 反向 proxy toohello 服務代表 hello 用戶端要求所建立的 hello HTTP 要求的逾時。 hello 預設值為 60 秒。 這是選擇性參數。

### <a name="example-usage"></a>使用方式範例
例如，讓我們來看 hello *fabric: / MyApp/MyService*開啟下列 URL 的 hello HTTP 接聽程式的服務：

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

以下是 hello 服務的 hello 資源：

* `/index.html`
* `/api/users/<userId>`

如果 hello 服務使用 hello 單一資料分割配置，hello *PartitionKey*和*PartitionKind*查詢字串參數，就不需要與 hello 服務可以達到使用 hello 閘道為：

* 外部： `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`
* 內部： `http://localhost:19081/MyApp/MyService`

如果 hello 服務使用 hello 統一 Int64 資料分割配置，hello *PartitionKey*和*PartitionKind*查詢字串參數必須是使用的 tooreach hello 服務的資料分割：

* 外部： `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`
* 內部： `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`

tooreach hello 資源 hello 服務所公開，只要將 hello hello URL 中的服務名稱之後的 hello 資源路徑：

* 外部： `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`
* 內部： `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`

hello 閘道會將這些要求 toohello 服務 URL:

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a>連接埠共用服務特殊處理
Azure 應用程式閘道嘗試的 tooresolve 服務一次地址，然後重試 hello 要求，無法連絡服務時。 這是應用程式閘道的主要優點，因為用戶端程式碼不需要它自己的服務解析 tooimplement，解決迴圈。

一般而言，當服務無法連線，hello 服務執行個體或複本已被移 tooa 不同的節點，做為其標準的生命週期的一部分。 當發生這種情況時，可能會收到應用程式閘道，網路連線錯誤，指出端點上 hello 沒有長開啟原本解析位址。

不過，複本或服務執行個體可以共用主機處理序，在由以 http.sys 為基礎的 Web 伺服器託管時也可以共用連接埠，這些 Web 伺服器包括︰

* [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [ASP.NET Core WebListener](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [Katana](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

在此情況下，可能是該 hello 網頁伺服器位於 hello 主控件程序和回應 toorequests，但 hello 解決服務執行個體或複本已無法再使用 hello 主機上。 在此情況下，hello 閘道會收到 HTTP 404 回應 hello web 伺服器。 因此，HTTP 404 有兩個不同意義︰

- 案例 1: hello 服務位址是正確的但 hello hello 使用者要求的資源不存在。
- 案例 2: hello 服務位址不正確，並且 hello hello 使用者要求的資源可能存在的不同節點上。

hello 第一種情況是會被視為使用者錯誤標準 HTTP 404。 不過，在 hello 第二個情況下，hello 使用者已要求資源存在。 應用程式閘道已無法 toolocate 它因為 hello 服務本身已移動。 應用程式閘道需求 tooresolve hello 位址一次，再重試 hello 要求。

應用程式閘道，因此必須介於這兩種情況的方式 toodistinguish。 toomake 的區別，從 hello 伺服器則需要提示。

* 根據預設，應用程式閘道會假設案例 #2，並再次嘗試 tooresolve 和問題 hello 要求。
* 第 1 個 tooApplication 閘道 tooindicate，hello 服務應該會傳回下列 HTTP 回應標頭的 hello:

  `X-ServiceFabric : ResourceNotFound`

此 HTTP 回應標頭表示一般 HTTP 404 情況中的 hello 要求的資源不存在，以及應用程式閘道將會再次嘗試 tooresolve hello 服務位址。

## <a name="setup-and-configuration"></a>設定和組態

### <a name="enable-reverse-proxy-via-azure-portal"></a>透過 Azure 入口網站啟用反向 Proxy

Azure 入口網站提供選項 tooenable 反向 proxy，建立新的 Service Fabric 叢集時。
在下**建立 Service Fabric 叢集**，步驟 2： 叢集設定中，節點型別組態，選取 hello 核取方塊太 「 啟用反向 proxy 」。
設定安全的反向 proxy，可以指定 SSL 憑證在步驟 3： 安全性、 設定叢集安全性設定、 選取 hello 核取方塊太"Include 反向 proxy 的 SSL 憑證"，而且輸入 hello 憑證詳細資料。

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a>透過 Azure Resource Manager 範本啟用反向 Proxy

您可以使用 hello [Azure Resource Manager 範本](service-fabric-cluster-creation-via-arm.md)tooenable hello 反向 proxy 服務網狀架構中的 hello 叢集。

請參閱太[設定 HTTPS 反向 Proxy 安全叢集中](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster)Azure 資源管理員的範本範例 tooconfigure 安全反向 proxy 的憑證和處理憑證變換。

首先，您取得 hello 範本 hello 叢集的 toodeploy。 您可以使用 hello 範例範本，或建立自訂的資源管理員範本。 然後，您可以使用下列步驟的 hello 啟用 hello 反向 proxy:

1. 定義在 hello hello 反向 proxy 的連接埠[參數 > 一節](../azure-resource-manager/resource-group-authoring-templates.md)的 hello 範本。

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. 針對每個在 hello hello nodetype 物件指定 hello 連接埠**叢集**[資源類型] 區段中](../azure-resource-manager/resource-group-authoring-templates.md)。

    hello 參數名稱，reverseProxyEndpointPort 識別 hello 連接埠。

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. tooaddress hello 反向 proxy，從外部 hello Azure 叢集上，設定您指定在步驟 1 中的 hello 通訊埠的 hello Azure 負載平衡器規則。

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. tooconfigure hello hello 反向 proxy，連接埠上的 SSL 憑證加入 hello 憑證 toohello ***reverseProxyCertificate***屬性在 hello**叢集**[資源類型] 區段](../resource-group-authoring-templates.md).

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a>支援不同 hello 叢集憑證中的反向 proxy 憑證
 如果與 hello 憑證來保護 hello 叢集不同 hello 反向 proxy 的憑證，然後 hello 先前指定應該 hello 虛擬機器上安裝憑證，並加入 toohello 存取控制清單 (ACL)，如此可以 Service Fabric存取它。 作法是在 hello **virtualMachineScaleSets** [資源類型 區段中](../resource-group-authoring-templates.md)。 進行安裝時，將該憑證 toohello osProfile。 hello 範本的 hello 延伸區段，可以更新 hello ACL 中的 hello 憑證。

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> 當您使用不同於 hello 叢集憑證 tooenable hello 反向 proxy 上現有的叢集中的憑證時，安裝 hello 反向 proxy 的憑證，並更新 hello ACL hello 叢集上的，才能啟用 hello 反向 proxy。 完整的 hello [Azure Resource Manager 範本](service-fabric-cluster-creation-via-arm.md)部署使用所述的 hello 設定先前在開始部署 tooenable hello 反向 proxy 之前在步驟 1-4。

## <a name="next-steps"></a>後續步驟
* 請參閱 [GitHub 上的範例專案](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)中服務之間的 HTTP 通訊範例。
* [與 hello 反向 proxy 轉送 toosecure HTTP 服務](service-fabric-reverseproxy-configure-secure-communication.md)
* [使用 Reliable Services 遠端服務進行遠端程序呼叫](service-fabric-reliable-services-communication-remoting.md)
* [在 Reliable Services 中使用 OWIN 的 Web API](service-fabric-reliable-services-communication-webapi.md)
* [使用 Reliable Services 的 WCF 通訊](service-fabric-reliable-services-communication-wcf.md)
* 如需其他反向 Proxy 組態選項，請參閱[自訂 Service Fabric 叢集設定](service-fabric-cluster-fabric-settings.md)中的ApplicationGateway/Http 一節。

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
