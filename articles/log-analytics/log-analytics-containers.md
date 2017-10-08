---
title: "aaaContainer 監控 Azure 記錄分析解決方案 |Microsoft 文件"
description: "hello 容器監視方案中記錄分析可協助您檢視及管理您的 Docker 和 Windows 容器主機的單一位置。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a>Log Analytics 中的容器監視解決方案

![容器符號](./media/log-analytics-containers/containers-symbol.png)

本文說明如何向上 tooset 並用 hello 容器監視方案中記錄分析，可協助您檢視和管理您的 Docker 和 Windows 容器主機的單一位置。 Docker 的軟體虛擬化系統使用 toocreate 容器自動化軟體部署 tootheir IT 基礎結構。

hello 方案顯示哪些容器正在執行，它們正在執行時，哪些容器映像和容器執行的位置。 您可以檢視詳細的稽核資訊，其中顯示搭配容器使用的命令。 此外，您可以透過檢視和搜尋而不需要 tooremotely 檢視 Docker 或 Windows 主機的集中式記錄檔來疑難排解容器。 您可能會找到有雜訊且耗用過多主機資源的容器。 而且，您可以檢視容器的集中式 CPU、記憶體、儲存體以及網路使用量和效能資訊。 您可以在執行 Windows 的電腦上集中管理，並從 Windows Server、HYPER-V 和 Docker 容器比較記錄檔。 hello 解決方案支援下列容器 orchestrators hello:

- Docker Swarm
- DC/OS
- Kubernetes
- Service Fabric
- Red Hat OpenShift


hello 下列圖表顯示 hello 各種容器主機和與 OMS 的代理程式之間的關聯性。

![容器圖表](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a>系統需求

開始之前，請檢閱下列符合 hello 必要條件的詳細資料 tooverify hello。

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a>容器監視解決方案支援 Docker Orchestrator 和作業系統平台
hello 表概述 hello Docker 協調流程和監視的容器清查、 效能和記錄檔記錄分析的支援的作業系統。   

| | ACS | Linux | Windows | 容器<br>清查 | 映像<br>清查 | 節點<br>清查 | 容器<br>效能 | 容器<br>Event | Event<br>記錄檔 | 容器<br>記錄檔 |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| Kubernetes | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Mesosphere<br>DC/OS | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; |
| Docker<br>Swarm | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| 服務<br>網狀架構 | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Red Hat 開啟<br>移位 | | &#8226; | | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; | | &#8226; |
| Windows Server<br>(獨立) | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| Linux 伺服器<br>(獨立) | | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |


### <a name="docker-versions-supported-on-linux"></a>在 Linux 上支援的 Docker 版本

- Docker 1.11 too1.13
- Docker CE 和 EE v17.06

### <a name="x64-linux-distributions-supported-as-container-hosts"></a>x64 Linux 散發套件可支援作為容器主機

- Ubuntu 14.04 LTS 和 16.04 LTS
- CoreOS (穩定版)
- Amazon Linux 2016.09.0
- openSUSE 13.2
- openSUSE LEAP 42.2
- CentOS 7.2 和 7.3
- SLES 12
- RHEL 7.2 和 7.3
- Red Hat OpenShift Container Platform (OCP) 3.4 和 3.5
- ACS Mesosphere DC/OS 1.7.3 too1.8.8
- ACS Kubernetes 1.4.5 too1.6
- ACS Docker Swarm

### <a name="supported-windows-operating-system"></a>支援的 Windows 作業系統

- Windows Server 2016
- Windows 10 年度版 (Professional 或 Enterprise)

### <a name="docker-versions-supported-on-windows"></a>在 Windows 上支援 Docker 版本

- Docker 1.12 和 1.13
- Docker 17.03.0 和更新版本

## <a name="installing-and-configuring-hello-solution"></a>安裝和設定 hello 方案
使用下列資訊 tooinstall hello 並設定 hello 方案。

1. 新增 hello 容器監視解決方案 tooyour OMS 工作區從[Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview)或使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。

2. 安裝和使用 Docker 搭配 OMS 代理程式。  根據您的作業系統，您可以選擇從 hello 下列方法：

  * 在支援 Linux 作業系統上安裝和執行 Docker，然後安裝並設定 hello [OMS Agent for Linux](log-analytics-agent-linux.md)。  
  * CoreOS，您無法執行 hello OMS Agent for Linux。 相反地，您可執行容器化的版本的 hello OMS Agent for Linux。 檢閱 [Linux 容器主機，包括 CoreOS](#for-all-linux-container-hosts-including-coreos) 或 [Azure Government Linux 容器主機，包括 CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos)，如果您正在使用 Azure Government Cloud 中的容器。
  * 在 Windows Server 2016 和 Windows 10 中，安裝 hello Docker 引擎與用戶端，然後連接的代理程式 toogather 資訊並傳送它 tooLog 分析。  

### <a name="container-services"></a>容器服務

- 如果您有 Red Hat OpenShift 環境，請檢閱[針對 Red Hat OpenShift 設定 OMS 代理程式](#configure-an-oms-agent-for-red-hat-openshift)。
- 如果您有使用 hello Azure 容器服務的 Kubernetes 叢集，檢閱[監視 Azure 容器服務叢集與 Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md)。
- 如果您擁有 Azure Container Service DC/OS 叢集，請深入了解[使用 Operations Management Suite 監視 Azure Container Service DC/OS 叢集](../container-service/dcos-swarm/container-service-monitoring-oms.md)。
- 如果您有 Docker Swarm 模式環境，詳細資訊請參閱[為 Docker Swarm 設定 OMS 代理程式](#configure-an-oms-agent-for-docker-swarm)。
- 如果您搭配 Service Fabric 使用容器，請參閱 [Azure Service Fabric 概觀](../service-fabric/service-fabric-overview.md)以深入了解。
- 檢閱 hello [Windows 上的 Docker 引擎](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon)發行項，如需有關如何 tooinstall 和執行 Windows 的電腦上設定 Docker 引擎。

> [!IMPORTANT]
> 必須執行 docker**之前**安裝 hello [OMS Agent for Linux](log-analytics-agent-linux.md)容器主機上。 如果您已經安裝 hello 代理程式安裝 Docker 之前，您需要 tooreinstall hello OMS Agent for Linux。 如需有關 Docker 的詳細資訊，請參閱 hello [Docker 網站](https://www.docker.com)。


## <a name="linux-container-hosts"></a>Linux 容器主機

安裝 Docker 之後，使用下列設定容器主機 tooconfigure hello 代理程式用於 Docker 的 hello。 首先您需要您的 OMS 工作區識別碼和金鑰，您可以在 hello Azure 入口網站中找到。 在您的工作區中，按一下**快速入門** > **電腦**tooview 您**工作區識別碼**和**主索引鍵**。  將兩者複製並貼到您最愛的編輯器。

### <a name="for-all-linux-container-hosts-except-coreos"></a>適用於 CoreOS 以外的所有 Linux 容器主機

- 如需詳細資訊和如何 tooinstall hello 適用於 Linux 的 OMS 代理程式上的步驟，請參閱[連接您的 Linux 電腦 tooOperations Management Suite (OMS)](log-analytics-agent-linux.md)。

### <a name="for-all-linux-container-hosts-including-coreos"></a>適用於包含 CoreOS 的所有 Linux 容器主機

啟動您想 toomonitor hello OMS 容器。 修改並使用下列範例中的 hello:

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a>適用於包含 CoreOS 的所有 Azure Government Linux 容器主機

啟動您想 toomonitor hello OMS 容器。 修改並使用下列範例中的 hello:

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a>從使用已安裝的 Linux 代理程式 tooone 容器中切換
如果您先前使用 hello 直接安裝代理程式，而想 tooinstead 使用容器中執行的代理程式，您必須先會移除 hello OMS Agent for Linux。 請參閱[解除安裝 hello OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand toosuccessfully 的解除安裝 hello 代理程式。  

### <a name="configure-an-oms-agent-for-docker-swarm"></a>為 Docker Swarm 設定 OMS 代理程式

您可以執行以全域服務的 hello OMS 代理程式上 Docker Swarm。 使用下列資訊 toocreate OMS 代理程式服務的 hello。 您需要 tooinsert OMS 工作區識別碼及主索引鍵。

- Hello 下列 hello 主要在節點上執行。

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a>為 Red Hat Openshift 設定 OMS 代理程式
有三種方式 tooadd hello OMS Agent tooRed Hat OpenShift toostart 容器監視資料收集。

* [安裝 hello OMS Agent for Linux](log-analytics-agent-linux.md)直接在每個 OpenShift 節點上  
* 在位於 Azure 中的每個 OpenShift 節點上[啟用記錄分析 VM 延伸模組](log-analytics-azure-vm-extension.md)  
* Hello OMS 代理程式安裝為 OpenShift 精靈集  

在本節中，我們會討論 hello 步驟需要的 tooinstall hello OMS 代理程式 OpenShift 精靈設定。  

1. 登入 toohello OpenShift 主節點，然後複製 hello yaml 檔案[ocp omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml)從 GitHub tooyour 主要節點和修改 hello 值與您的 OMS 工作區識別碼和主索引鍵。
2. 執行下列命令 toocreate hello oms 的專案，然後設定 hello 使用者帳戶。

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. toodeploy hello 精靈集執行 hello 下列：

    `oc create -f ocp-omsagent.yaml`

5. tooverify 它已設定且運作正常，hello 下列輸入：

    `oc describe daemonset omsagent`  

    和 hello 輸出應該類似：

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

如果您想 toouse 密碼 toosecure 您的 OMS 工作區識別碼及主要金鑰使用 hello OMS 代理程式協助程式組 yaml 檔案時，，執行下列步驟的 hello。

1. 登入 toohello OpenShift 主節點，然後複製 hello yaml 檔案[ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml)和密碼產生指令碼[ocp secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh)從 GitHub。  此指令碼會產生 OMS 工作區識別碼及主要金鑰 toosecure hello 密碼 yaml 檔案您 secrete 資訊。  
2. 執行下列命令 toocreate hello oms 的專案，然後設定 hello 使用者帳戶。 hello 密碼產生指令碼會要求您的 OMS 工作區識別碼<WSID>和主索引鍵<KEY>和完成時，它會建立 hello ocp secret.yaml 檔案。  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. 執行 hello 下列部署 hello 密碼檔案：

    `oc create -f ocp-secret.yaml`

5. 確認執行 hello 下列部署：

    `oc describe secret omsagent-secret`  

    和 hello 輸出應該類似：  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. 執行 hello 下列部署 hello OMS 代理程式協助程式組 yaml 檔：

    `oc create -f ocp-ds-omsagent.yaml`  

7. 確認執行 hello 下列部署：

    `oc describe ds oms`

    和 hello 輸出應該類似：

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a>保護 Docker Swarm 和 Kubernetes 的密碼資訊

您可以針對 Docker Swarm 和 Kubernetes 容器服務保護密碼 OMS 工作區識別碼與主索引鍵。

#### <a name="secure-secrets-for-docker-swarm"></a>保護 Docker Swarm 的祕密

Docker Swarm，一旦建立工作區識別碼及主要金鑰的 hello 密碼之後，您可以針對執行 hello 建立的 OMSagent hello Docker 服務。 使用下列資訊 toocreate hello 秘密資訊。

1. Hello 下列 hello 主要在節點上執行。

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. 確認已正確建立祕密。

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. 執行下列命令 toomount hello 密碼 toohello 的 hello 容器化 OMS 代理程式。

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a>使用 yaml 檔案保護 Kubernetes 的祕密

Kubernetes，如中，您可以使用指令碼 toogenerate hello 密碼 yaml 檔案的工作區識別碼和主索引鍵。 在 hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)頁面上，您可以使用，不論您的機密資訊的檔案。

- 預設 OMS 代理程式 DaemonSet hello 沒有機密資訊 (omsagent.yaml)
- hello OMS 代理程式 DaemonSet yaml 檔案會使用密碼產生指令碼 toogenerate hello 密碼 yaml (omsagentsecret.yaml) 檔案中的機密資訊 (omsagent-ds-secrets.yaml)。

您可以選擇 toocreate omsagent DaemonSets 含密碼。

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a>沒有祕密的預設 OMSagent DaemonSet yaml 檔案

- Hello 預設 OMS 代理程式 DaemonSet yaml 檔案取代 hello`<WSID>`和`<KEY>`tooyour WSID 和金鑰。 複製 hello 檔案 tooyour 主要節點，然後執行的 hello 下列：

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a>有祕密的預設 OMSagent DaemonSet yaml 檔案

1. toouse 使用機密資訊的 OMS 代理程式 DaemonSet 建立 hello 機密資料第一次。
    1. 複製 hello 指令碼和密碼的範本檔案，並確定它們是在 hello 相同的目錄。
        - 祕密產生指令碼 - secret-gen.sh
        - 祕密範本 - secret-template.yaml
    2. 執行 hello 指令碼，如下列範例中的 hello。 hello 指令碼會要求輸入 hello，OMS 工作區識別碼及主要金鑰，並輸入它們之後，hello 指令碼建立密碼 yaml 檔案，因此您可以在執行。   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. 建立 hello 密碼 pod 執行 hello 下列：
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. tooverify，執行下列 hello:

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        輸出會像下面這樣：

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        輸出會像下面這樣：

        ```
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

    5. 執行 ``` sudo kubectl create -f omsagent-ds-secrets.yaml ``` 以建立您的 omsagent daemon-set

2. 請確認正在執行 OMS Agent DaemonSet，類似下列的 toohello 該 hello:

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


Kubernetes，使用指令碼 toogenerate hello 密碼 yaml 檔案中的工作區識別碼及主要金鑰的內容。 下列範例與 hello 的資訊的使用 hello [omsagent yaml 檔案](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml)toosecure 您的機密資訊。

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
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

## <a name="windows-container-hosts"></a>Windows 容器主機

### <a name="preparation-before-installing-windows-agents"></a>安裝 Windows 代理程式之前的準備動作

您在執行 Windows 的電腦上安裝代理程式之前，您會需要 tooconfigure hello Docker 服務。 hello 組態可讓您 hello Windows 代理程式 」 或 「 hello 記錄分析的虛擬機器擴充功能 toouse hello Docker TCP 通訊端以便 hello 代理程式可以從遠端存取 hello Docker 精靈和 toocapture 資料監視。

#### <a name="toostart-docker-and-verify-its-configuration"></a>toostart Docker 並確認其組態

沒有所需的步驟 tooset 向上 TCP Windows Server 的具名管道：

1. 在 Windows PowerShell 中啟用 TCP 管道和具名的管道。

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. 使用 TCP 管道 hello 組態檔來設定 Docker 及具名管道。 hello 設定檔是位於 C:\ProgramData\docker\config\daemon.json。

    在 hello daemon.json 檔案中，您需要下列 hello:

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

如需搭配 Windows 容器的 hello Docker 精靈設定的詳細資訊，請參閱[Windows 上的 Docker 引擎](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon)。


### <a name="install-windows-agents"></a>安裝 Windows 代理程式

tooenable Windows 和 HYPER-V 容器監視，請容器主機的 Windows 電腦上安裝 hello Microsoft Monitoring Agent (MMA)。 在內部部署環境中執行 Windows 的電腦，請參閱[連接的 Windows 電腦 tooLog 分析](log-analytics-windows-agents.md)。 虛擬機器的執行在 Azure 中，將它們連接 tooLog 分析使用 hello[虛擬機器擴充功能](log-analytics-azure-vm-extension.md)。

您可以監視 Service Fabric 上執行的 Windows 容器。 不過，Service Fabric 目前只支援 [Azure 中執行的虛擬機器](log-analytics-azure-vm-extension.md)和[在內部部署環境中執行 Windows 的電腦](log-analytics-windows-agents.md)。

您可以確認該 hello 容器監視解決方案會針對 Windows 設定正確。 toocheck hello 管理組件正常運作，是下載尋找*ContainerManagement.xxx*。 hello 檔案應該在 hello C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs 資料夾。


## <a name="solution-components"></a>方案元件

如果您使用 Windows 代理程式，然後 hello 下列管理組件是每部電腦上安裝代理程式時將方案加入。 不不需要 hello 管理組件的任何設定或維護。

- C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs 中所安裝的 ContainerManagement.xxx

## <a name="container-data-collection-details"></a>容器資料收集詳細資料
hello 容器監視解決方案會從容器主機和容器，使用您所啟用的代理程式收集各種效能度量和記錄資料。

資料會收集下列代理程式類型的 hello 每隔三分鐘。

- [OMS Agent for Linux](log-analytics-linux-agents.md)
- [Windows 代理程式](log-analytics-windows-agents.md)
- [Log Analytics VM 延伸模組](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a>容器資料列

hello 下表顯示 hello 容器監視解決方案和會出現在記錄搜尋結果中的 hello 資料型別所收集的記錄的範例。

| 資料類型 | 記錄檔搜尋中的資料類型 | 欄位 |
| --- | --- | --- |
| 主機和容器的效能 | `Type=Perf` | Computer、ObjectName、CounterName &#40;%Processor Time、Disk Reads MB、Disk Writes MB、Memory Usage MB、Network Receive Bytes、Network Send Bytes、Processor Usage sec、Network&#41;、CounterValue、TimeGenerated、CounterPath、SourceSystem |
| 容器清查 | `Type=ContainerInventory` | TimeGenerated、Computer、container name、ContainerHostname、Image、ImageTag、ContainerState、ExitCode、EnvironmentVar、Command、CreatedTime、StartedTime、FinishedTime、SourceSystem、ContainerID、ImageID |
| 容器映像清查 | `Type=ContainerImageInventory` | TimeGenerated、Computer、Image、ImageTag、ImageSize、VirtualSize、Running、Paused、Stopped、Failed、SourceSystem、ImageID、TotalContainer |
| 容器記錄檔 | `Type=ContainerLog` | TimeGenerated、Computer、image ID、container name、LogEntrySource、LogEntry、SourceSystem、ContainerID |
| 容器服務記錄檔 | `Type=ContainerServiceLog`  | TimeGenerated、Computer、TimeOfCommand、Image、Command、SourceSystem、ContainerID |
| 容器節點清查 | `Type=ContainerNodeInventory_CL`| TimeGenerated、Computer、ClassName_s、DockerVersion_s、OperatingSystem_s、Volume_s、Network_s、NodeRole_s、OrchestratorType_s、InstanceID_g、SourceSystem|
| Kubernetes 清查 | `Type=KubePodInventory_CL` | TimeGenerated、Computer、PodLabel_deployment_s、PodLabel_deploymentconfig_s、PodLabel_docker_registry_s、Name_s、Namespace_s、PodStatus_s、PodIp_s、PodUid_g、PodCreationTimeStamp_t、SourceSystem |
| 容器流程 | `Type=ContainerProcess_CL` | TimeGenerated、Computer、Pod_s、Namespace_s、ClassName_s、InstanceID_s、Uid_s、PID_s、PPID_s、C_s、STIME_s、Tty_s、TIME_s、Cmd_s、Id_s、Name_s、SourceSystem |
| Kubernetes 事件 | `Type=KubeEvents_CL` | TimeGenerated、Computer、Name_s、ObjectKind_s、Namespace_s、Reason_s、Type_s、SourceComponent_s、SourceSystem、Message |

標籤太附加*PodLabel*資料型別是您自己的自訂標籤。 hello hello 表所示的附加的 PodLabel 標籤是範例。 因此，`PodLabel_deployment_s`、`PodLabel_deploymentconfig_s`、`PodLabel_docker_registry_s` 在環境的資料集中會有所不同，且一般而言會類似 `PodLabel_yourlabel_s`。


## <a name="monitor-containers"></a>監視容器
您已啟用 hello OMS 入口網站中的 hello 方案之後，hello**容器**磚會顯示您的容器主機和 hello 容器主機中執行的摘要資訊。

![容器圖格](./media/log-analytics-containers/containers-title.png)

hello 磚會顯示您有多少容器的概觀 hello 環境中失敗之是否正在執行或已停止。

### <a name="using-hello-containers-dashboard"></a>使用 hello 容器儀表板
按一下 hello**容器**磚。 在這裡，您會看到依下列各項組織的檢視︰

- **容器事件** - 會顯示容器狀態和包含失敗容器的電腦。
- **容器的記錄檔**-顯示以 hello 高數目的記錄檔產生一段時間和的電腦清單的容器記錄檔的圖表。
- **Kubernetes 事件**-顯示 Kubernetes 產生的事件時間和的 hello 原因為何 pod 產生 hello 事件清單的圖表。 只有在 Linux 環境中才會使用此資料集。
- **Kubernetes 命名空間清查**-顯示命名空間和 pod 的 hello 數目，並顯示其階層。 只有在 Linux 環境中才會使用此資料集。
- **容器節點清查**-顯示 hello 數目的容器節點主機上使用的協調流程類型。 節點主機方式 hello 電腦也會列出由 hello 數目的容器。 只有在 Linux 環境中才會使用此資料集。
- **容器映像庫存**-顯示 hello 總數使用容器映像和映像類型數目。 映像的 hello 數目也會列出由 hello 影像標記。
- **容器狀態**-顯示 hello 總數容器具有執行中的容器節點/主機電腦。 由主機執行中的 hello 數目也會列出電腦。
- **容器流程** - 會顯示一段時間執行的容器流程折線圖。 還會依容器內的執行命令/流程列出容器。 只有在 Linux 環境中才會使用此資料集。
- **容器的 CPU 效能**-顯示經過一段時間的電腦節點主控 hello 平均 CPU 使用率的折線圖。 也列出 hello 電腦節點/主控根據平均 CPU 使用率。
- **容器記憶體效能** - 會顯示一段時間的記憶體使用量折線圖。 還會以執行個體名稱作為基礎列出電腦記憶體使用率。
- **電腦效能**-顯示一段時間的一段時間和可用磁碟空間的 mb 記憶體使用量的百分比 hello %的 CPU 效能隨著時間的折線圖。 您可以將滑鼠停留在任何列中圖表 tooview 更多詳細資料。


Hello 儀表板的每個區域是收集的資料執行搜尋的視覺表示法。

![容器儀表板](./media/log-analytics-containers/containers-dash01.png)

![容器儀表板](./media/log-analytics-containers/containers-dash02.png)

在 hello**容器狀態**區域中，按一下 hello 最上層區域中，如下所示。

![容器狀態](./media/log-analytics-containers/containers-status.png)

此時會開啟 記錄搜尋，顯示 hello 狀態，您的容器的相關資訊。

![容器的記錄檔搜尋](./media/log-analytics-containers/containers-log-search.png)

您可以從這裡編輯 hello 搜尋查詢 toomodify 它您感興趣的 toofind hello 特定資訊。 如需記錄檔搜尋的詳細資訊，請參閱 [Log Analytics 中的記錄檔搜尋](log-analytics-log-searches.md)。

## <a name="troubleshoot-by-finding-a-failed-container"></a>尋找失敗的容器以進行疑難排解

如果容器已透過非零結束代碼結束，則 Log Analytics 會將容器標示為 [失敗]。 您可以看到的 hello 錯誤或失敗發生在 hello hello 環境概觀**失敗容器**區域。

### <a name="toofind-failed-containers"></a>失敗的 toofind 容器
1. 按一下 hello**容器狀態**區域。  
   ![容器狀態](./media/log-analytics-containers/containers-status.png)
2. 記錄搜尋會開啟，並顯示 hello 狀態的程式的容器，類似下列的 toohello。  
   ![容器狀態](./media/log-analytics-containers/containers-log-search.png)
3. 接下來，按一下失敗的容器 tooview 更多資訊 hello 的彙總資料值。 展開**顯示更多**tooview hello 映像識別碼。  
   ![失敗的容器](./media/log-analytics-containers/containers-state-failed.png)  
4. 接著，輸入 hello 下列 hello 搜尋查詢中。 `Type=ContainerInventory <ImageID>`toosee 詳細資料 hello 映像，例如停止和失敗的映像的映像大小與數目。  
   ![失敗的容器](./media/log-analytics-containers/containers-failed04.png)

## <a name="search-logs-for-container-data"></a>搜尋容器資料的記錄檔
當您正在排除特定的錯誤時，它可讓的 toosee 發生在您的環境中。 下列記錄類型的 hello 將協助您建立查詢，您想要的 tooreturn hello 資訊。


- **ContainerImageInventory** – 當您嘗試依映像和 tooview 映像資訊，例如映像識別碼或大小 toofind 資訊，請使用此類型。
- **ContainerInventory** – 當您需要有關容器位置、其名稱，以及所執行映像的資訊時，請使用這個類型。
- **ContainerLog** – 當您想 toofind 特定錯誤記錄檔資訊和項目，請使用這個型別。
- **ContainerNodeInventory_CL**此類型要使用 hello/主控件 節點的資訊位於容器的位置。 它會提供 Docker 版本、協調流程類型、儲存體和網路資訊。
- **ContainerProcess_CL**使用這個型別 tooquickly 看到 hello hello 容器內執行的處理程序。
- **ContainerServiceLog** – 當您嘗試 toofind 稽核追蹤資訊的 hello Docker 精靈，例如啟動、 停止、 刪除或提取命令使用這個類型。
- **KubeEvents_CL**使用這個型別 toosee hello Kubernetes 事件。
- **KubePodInventory_CL**當您想 toounderstand hello 叢集階層資訊，請使用這個型別。


### <a name="toosearch-logs-for-container-data"></a>toosearch 記錄檔以取得容器資料
* 選擇的映像，您知道最近失敗，並為其尋找 hello 錯誤記錄檔。 首先，透過 **ContainerInventory** 搜尋來尋找正在執行該映像的容器名稱。 例如，搜尋 `Type=ContainerInventory ubuntu Failed`  
    ![搜尋 Ubuntu 容器](./media/log-analytics-containers/search-ubuntu.png)

  hello hello 容器的名稱旁邊太**名稱**，然後在搜尋這些記錄檔。 在此範例中為 `Type=ContainerLog cranky_stonebreaker`。

**檢視效能資訊**

當您開始 tooconstruct 查詢時，它可以協助 toosee 是什麼可能第一次。 例如，toosee 所有效能資料，再試一次輸入廣泛查詢 hello 下列都搜尋查詢。

```
Type=Perf
```

![容器效能](./media/log-analytics-containers/containers-perf01.png)

您可以為範圍 hello 效能資料，您看見 tooa 特定容器輸入 hello 目的 toohello 查詢的權限。

```
Type=Perf <containerName>
```

顯示 hello 針對個別的容器所收集的效能度量的清單。

![容器效能](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a>範例記錄檔搜尋查詢
它通常很有用 toobuild 開頭範例或兩個，然後修改這些 toofit 查詢您的環境。 做為起點，您可以試驗 hello**查詢範例**區域 toohelp 建置更進階的查詢。

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![容器查詢](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a>儲存記錄檔搜尋查詢
儲存查詢是 Log Analytics 的標準功能。 藉由儲存查詢，您可將您覺得有用的查詢放在容易取得的地方，以便日後使用。

您建立查詢，您有幫助之後，按一下以儲存它**我的最愛**hello 頁面頂端的 hello 記錄搜尋。 然後您可以輕鬆地存取稍後從 hello**我的儀表板**頁面。

## <a name="next-steps"></a>後續步驟
* [搜尋記錄](log-analytics-log-searches.md)tooview 詳細容器資料記錄。
