---
title: "Azure DC/OS 叢集中的 aaaLoad 平衡容器 |Microsoft 文件"
description: "Azure Container Service DC/OS 叢集中多個容器的負載平衡。"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "容器, 微服務, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a>Azure Container Service DC/OS 叢集中容器的負載平衡
在本文中，我們會探討 toocreate DC/OS 中使用內部負載平衡器管理使用馬拉松 LB Azure 容器服務的方式。 此設定可讓您 tooscale 應用程式以水平方式。 它也可讓您利用 tootake hello 公用和私用的代理程式的叢集將您的負載平衡器放置在 hello 公用叢集和您的應用程式容器 hello 私用的叢集上。 在本教學課程中，您：

> [!div class="checklist"]
> * 設定 Marathon 負載平衡器
> * 部署應用程式使用 hello 負載平衡器
> * 設定 Azure 負載平衡器

您必須在本教學課程步驟的叢集 toocomplete hello ACS DC/OS。 如有需要，[此指令碼範例](./../kubernetes/scripts/container-service-cli-deploy-dcos.md)可為您建立一個叢集。

本教學課程需要 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooupgrade，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a>負載平衡概觀

在 Azure Container Service DC/OS 叢集中有兩個負載平衡層： 

**Azure 負載平衡器**提供公用進入點 (是該使用者存取的 hello)。 Azure LB Azure 容器服務會自動提供，而是，預設為設定的 tooexpose 連接埠 80、 443 和 8080。

**hello 馬拉松負載平衡器 (lb 馬拉松)**路由輸入這些要求提供服務的要求 toocontainer 執行個體。 因為我們縮放 hello 容器提供 web 服務，hello 馬拉松 lb 動態調整。 預設會在您的容器服務未提供此負載平衡器，但它是簡單 tooinstall。

## <a name="configure-marathon-load-balancer"></a>設定 Marathon 負載平衡器

馬拉松負載平衡器以動態方式重新設定根據您已部署的 hello 容器本身。 它也是彈性 toohello 遺失的容器或代理程式-如果發生這種情況，會重新啟動的其他地方 hello 容器 Apache Mesos 馬拉松 lb 會調整。

執行下列命令 tooinstall hello 馬拉松負載平衡器 hello 公用代理程式的叢集上的 hello。

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a>部署負載平衡應用程式

現在，我們已經 hello 馬拉松 lb 封裝時，我們可以部署，我們希望 tooload 平衡的應用程式容器。 

首先，取得 hello hello 公開屬性，代理程式的 FQDN。

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

接下來，建立名為*hello web.json*和 hello 中的複製下列內容。 hello`HAPROXY_0_VHOST`標籤需要 toobe hello FQDN hello DC/OS 代理程式的更新。 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

使用 hello DC/OS CLI toorun hello 應用程式。 根據預設馬拉松部署 hello hello 應用程式 toohello 私人叢集。 這表示在上面部署 hello 才可存取您的負載平衡器，透過這通常是 hello 預期的行為。

```azurecli-interactive
dcos marathon app add hello-web.json
```

一旦部署的 hello 應用程式，瀏覽 toohello hello 代理程式叢集 tooview 負載平衡應用程式的 FQDN。

![負載平衡應用程式的影像](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a>設定 Azure 負載平衡器

根據預設，Azure Load Balancer 會公開連接埠 80、8080 和 443。 如果您使用這三個的其中一個連接埠 （像是我們在上述範例中的 hello），則沒有需要 toodo 的項目。 您應該能夠 toohit 代理程式負載平衡器的 FQDN，以及每次您重新整理，您將會叫用其中三個 web 伺服器以循環配置資源方式。 

如果您使用不同的通訊埠，您需要 tooadd 循環配置資源的規則，並在 hello 負載平衡器探查的 hello 所使用的連接埠。 您可以從 hello [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md)，與 hello 命令`azure network lb rule create`和`azure network lb probe create`。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解有關負載平衡 acs hello 馬拉松和 Azure 負載平衡器包括 hello 下列動作：

> [!div class="checklist"]
> * 設定 Marathon 負載平衡器
> * 部署應用程式使用 hello 負載平衡器
> * 設定 Azure 負載平衡器

前進 toohello 下一個教學課程的 toolearn 需將 Azure 儲存體與 Azure 中的 DC/OS 的整合。

> [!div class="nextstepaction"]
> [在 DC/OS 叢集中裝載 Azure 檔案共用](container-service-dcos-fileshare.md)