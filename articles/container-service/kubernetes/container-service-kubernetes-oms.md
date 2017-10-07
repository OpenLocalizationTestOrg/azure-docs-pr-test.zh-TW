---
title: "aaaMonitor Azure Kubernetes 叢集 Operations Management |Microsoft 文件"
description: "使用 Microsoft Operations Management Suite 監視 Azure Container Service 中的 Kubernetes 叢集"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a>使用 Microsoft Operations Management Suite (OMS) 監視 Azure Container Service 叢集

## <a name="prerequisites"></a>必要條件
本逐步解說假設您已[使用 Azure Container Service 建立 Kubernetes 叢集](container-service-kubernetes-walkthrough.md)。

它也假設您擁有 hello `az` Azure cli 和`kubectl`安裝工具。

您可以測試是否有 hello`az`安裝執行工具：

```console
$ az --version
```

如果您沒有 hello`az`工具安裝，指示[這裡](https://github.com/azure/azure-cli#installation)。  
或者，您可以使用[Azure 雲端殼層](https://docs.microsoft.com/en-us/azure/cloud-shell/overview)，其具有 hello `az` Azure cli 和`kubectl`為您已安裝的工具。  

您可以測試是否有 hello`kubectl`安裝執行工具：

```console
$ kubectl version
```

如果您尚未安裝 `kubectl`，可以執行︰
```console
$ az acs kubernetes install-cli
```

如果您有安裝在您可以執行您 kubectl 工具 kubernetes 金鑰，tootest:
```console
$ kubectl get nodes
```

如果 hello 上述命令錯誤，您需要到 kubectl 工具 tooinstall kubernetes 叢集索引鍵。 您可以執行，以 hello 下列命令：
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a>使用 Operations Management Suite (OMS) 監視容器

Microsoft Operations Management (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。 容器的解決方案是 OMS 記錄分析可協助您檢視 hello 容器清查、 效能和記錄檔中的單一位置中的解決方案。 您可以稽核、 疑難排解容器檢視 hello 記錄在集中式位置，並尋找雜訊耗用過多的容器主機上。

![](media/container-service-monitoring-oms/image1.png)

如需容器解決方案的詳細資訊，請參閱 toothe[容器方案記錄分析](../../log-analytics/log-analytics-containers.md)。

## <a name="installing-oms-on-kubernetes"></a>在 Kubernetes 上安裝 OMS

### <a name="obtain-your-workspace-id-and-key"></a>取得您的工作區識別碼和金鑰
Hello OMS 代理程式 tootalk toohello 服務需要 toobe 設定工作區識別碼及工作區金鑰。 tooget hello 工作區識別碼和金鑰需要 toocreate OMS 帳戶在<https://mms.microsoft.com>。請遵循 hello 步驟 toocreate 帳戶。 一旦您完成建立 hello 帳戶之後，您需要 tooobtain 識別碼及金鑰即可**設定**，然後**連線來源**，然後**Linux 伺服器**，如下所示。

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a>安裝使用 DaemonSet hello OMS 代理程式
DaemonSets 所使用的 Kubernetes toorun hello 叢集中各主機上的容器的單一執行個體。
它們非常適合用來執行監視代理程式。

以下是 hello [DaemonSet YAML 檔案](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)。 將其儲存 tooa 檔案命名為`oms-daemonset.yaml`hello 預留位置值取代和`WSID`和`KEY`與您的工作區識別碼 hello 檔案中的金鑰。

一旦您加入工作區識別碼和金鑰 toohello DaemonSet 組態，您可以在 hello 與叢集上安裝 hello OMS 代理程式`kubectl`命令列工具：

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a>安裝使用 Kubernetes 密碼 hello OMS 代理程式
tooprotect 您的 OMS 工作區識別碼和金鑰，您可以使用 Kubernetes 密碼 DaemonSet YAML 檔案的一部分。

 - 複製 hello 指令碼、 密碼的範本檔案和 hello DaemonSet YAML 檔案 (從[儲存機制](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes))，並確定它們是在 hello 相同的目錄。 
      - 秘密產生指令碼 - secret-gen.sh
      - 秘密範本 - secret-template.yaml
   - DaemonSet YAML 檔案 - omsagent-ds-secrets.yaml
 - 執行 hello 指令碼。 hello 指令碼會要求 hello OMS 工作區識別碼及主要金鑰。 請插入，並 hello 指令碼會建立密碼 yaml 檔案，因此您可以執行它。   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - 建立 hello 密碼 pod 執行 hello 下列：``` kubectl create -f omsagentsecret.yaml ```
 
   - toocheck，執行下列 hello: 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - 執行 ``` kubectl create -f omsagent-ds-secrets.yaml ``` 以建立您的 omsagent daemon-set

### <a name="conclusion"></a>結論
就這麼簡單！ 請稍候幾分鐘，您應該能夠 toosee 資料流動 tooyour OMS 儀表板。
