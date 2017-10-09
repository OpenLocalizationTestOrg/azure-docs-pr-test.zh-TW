---
title: "aaaManage 馬拉松 UI 叢集 Azure DC/OS |Microsoft 文件"
description: "部署容器 tooan Azure 容器服務的叢集服務使用 hello 馬拉松 web UI。"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker、容器、微服務、Mesos、Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a>管理透過 hello 馬拉松 web UI Azure 容器服務 DC/OS 叢集
DC/OS 會提供一個環境來部署及調整叢集工作負載，同時減少了 hello 基礎硬體。 在 DC/OS 之上有架構會管理排程和執行計算工作負載。

架構可供許多常用的工作負載時，本文件說明 tooget 啟動部署具有馬拉松容器的方式。 


## <a name="prerequisites"></a>必要條件
在練習這些範例之前，您需要 Azure 容器服務中設定的 DC/OS 叢集。 您也需要 toohave 遠端連線 toothis 叢集。 如需有關這些項目詳細資訊，請參閱下列文章的 hello:

* [部署 Azure 容器服務叢集](container-service-deployment.md)
* [Tooan Azure 容器服務叢集連線](../container-service-connect.md)

> [!NOTE]
> 本文假設您透過本機連接埠 80 的通道 toohello DC/OS 叢集。
>

## <a name="explore-hello-dcos-ui"></a>瀏覽 hello DC/OS UI
使用安全殼層 (SSH) 通道[建立](../container-service-connect.md)，瀏覽 toohttp://localhost/。 這會載入 hello DC/OS web UI，並顯示 hello 叢集中，例如使用的資源、 使用中的代理程式，以及執行中的服務的相關資訊。

![DC/OS UI](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a>瀏覽 hello 馬拉松 UI
toosee hello 馬拉松 UI 中，瀏覽 toohttp://localhost/marathon。 在這個畫面上，您可以在 hello Azure 容器服務 DC/OS 叢集上啟動新的容器或另一個應用程式。 您也可以看到有關執行容器和應用程式的資訊。  

![Marathon UI](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a>部署 Docker 格式化容器
按一下新的容器使用馬拉松，toodeploy**建立應用程式**，並輸入下列資訊成 hello 表單索引標籤的 hello:

| 欄位 | 值 |
| --- | --- |
| ID |nginx |
| 記憶體 | 32 |
| 映像 |nginx |
| 網路 |橋接 |
| 主機連接埠 |80 |
| 通訊協定 |TCP |

![新增應用程式 UI--一般](./media/container-service-mesos-marathon-ui/dcos4.png)

![新增應用程式 UI--Docker 容器](./media/container-service-mesos-marathon-ui/dcos5.png)

![新增應用程式 UI--連接埠和服務探索](./media/container-service-mesos-marathon-ui/dcos6.png)

如果您想 toostatically 對應 hello 容器連接埠 tooa port hello 代理程式上的，您會需要 toouse JSON 模式。 toodo，切換 hello 新的應用程式精靈太**JSON 模式**使用 hello 切換。 然後輸入下列設定下 hello hello `portMappings` hello 應用程式定義的區段。 此範例中會繫結 hello 容器 tooport 80 hello DC/OS 代理程式的連接的埠 80。 在進行這項變更之後，您可以將此精靈切換離開 JSON 模式。

```none
"hostPort": 80,
```

![新增應用程式 UI--連接埠 80 範例](./media/container-service-mesos-marathon-ui/dcos13.png)

如果您想 tooenable 健康情況檢查，設定路徑上 hello**健康情況檢查** 索引標籤。

![新的應用程式 UI--健康狀態檢查](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

hello DC/OS 叢集部署的私人和公用的代理程式的設定。 Hello 叢集 toobe 無法 tooaccess 應用程式從 hello 網際網路，您需要 toodeploy hello 應用程式 tooa 公用代理程式。 因此，選取 toodo 的 hello**選擇性**hello 新的應用程式精靈 索引標籤並輸入**slave_public** hello**接受資源角色**。

然後按一下 [建立應用程式]。

![新增應用程式 UI--公用代理程式設定](./media/container-service-mesos-marathon-ui/dcos14.png)

在 hello 馬拉松主要頁面上，您可以看到 hello hello 容器的部署狀態。 一開始您看到的狀態為 [部署中]。 成功部署之後，hello 狀態變更太**執行**。

![Marathon 主頁面 UI--容器部署狀態](./media/container-service-mesos-marathon-ui/dcos7.png)

當您切換後 toohello DC/OS web UI (http://localhost/) 時，您會看到 hello DC/OS 叢集上確認正在執行的工作 （在此情況下，Docker 格式化的容器）。

![DC/OS web UI-hello 叢集上執行的工作](./media/container-service-mesos-marathon-ui/dcos8.png)

hello 工作 toosee hello 叢集節點上執行，請按一下 hello**節點** 索引標籤。

![DC/OS Web UI--工作叢集節點](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a>到達 hello 容器

在此範例中，hello 應用程式公用的代理程式節點上執行。 您到達 hello 應用程式從 hello 網際網路瀏覽 toohello 代理程式 hello 叢集的 FQDN: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`，其中：

* **DNSPREFIX**是您部署 hello 叢集時，您所提供的 hello DNS 前置詞。
* **區域**是資源群組所在的 hello 區域。

    ![來自網際網路的 Nginx](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a>後續步驟
* [使用 DC/OS 和 hello 馬拉松應用程式開發介面](container-service-mesos-marathon-rest.md)

* 深入探討在 hello 與 Mesos Azure 容器服務

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
