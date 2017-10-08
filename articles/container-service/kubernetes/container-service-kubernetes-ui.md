---
title: "使用 web UI 的 aaaManage Azure Kubernetes 叢集 |Microsoft 文件"
description: "使用 hello Kubernetes web UI 中 Azure 容器服務"
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
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a>使用 hello Kubernetes web UI，使用 Azure 容器服務

## <a name="prerequisites"></a>必要條件
本逐步解說假設您已[使用 Azure Container Service 建立 Kubernetes 叢集](container-service-kubernetes-walkthrough.md)。


它也假設您擁有 hello Azure CLI 2.0 和`kubectl`安裝工具。

您可以測試是否有 hello`az`安裝執行工具：

```console
$ az --version
```

如果您沒有 hello`az`工具安裝，指示[這裡](https://github.com/azure/azure-cli#installation)。

您可以測試是否有 hello`kubectl`安裝執行工具：

```console
$ kubectl version
```

如果您尚未安裝 `kubectl`，可以執行︰

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a>概觀

### <a name="connect-toohello-web-ui"></a>連接 toohello web UI
您可以啟動 hello Kubernetes web UI 執行：

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

這應該會開啟網頁瀏覽器設定 tootalk tooa 安全 proxy 連接您的本機電腦 toohello Kubernetes web UI。

### <a name="create-and-expose-a-service"></a>建立和公開服務
1. 在 hello Kubernetes web UI，按一下 **建立**hello 上方右視窗中的按鈕。

    ![Kubernetes Create UI](./media/container-service-kubernetes-ui/create.png)

    隨即會開啟對話方塊，您可以在其中開始建立應用程式。

2. 提供給它 hello 名稱`hello-nginx`。 使用 hello [ `nginx` Docker 容器](https://hub.docker.com/_/nginx/)及部署此 web 服務的三個複本。

    ![Kubernetes Pod 建立對話方塊](./media/container-service-kubernetes-ui/nginx.png)

3. 在 [服務] 之下，選取 [外部] 並輸入連接埠 80。

    這項設定負載平衡流量 toohello 三個複本。

    ![Kubernetes 服務建立對話方塊](./media/container-service-kubernetes-ui/service.png)

4. 按一下**部署**toodeploy 這些容器和服務。

    ![Kubernetes 部署](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a>檢視您的容器
按一下 之後**部署**，hello UI 顯示的檢視，您的服務部署：

![Kubernetes 狀態](./media/container-service-kubernetes-ui/status.png)

您可以查看左側 hello 的 ui 中，每個 Kubernetes 物件 hello 圓形中有 hello 狀態下**Pod**。 如果是部分完整圓形，正在仍會部署 hello 物件。 完整部署物件時，它會顯示綠色的核取記號︰

![Kubernetes 已部署](./media/container-service-kubernetes-ui/deployed.png)

所有項目開始執行之後，按一下您有關執行 web 服務的 hello 的 pod toosee 詳細資料。

![Kubernetes Pods](./media/container-service-kubernetes-ui/pods.png)

在 hello **Pod**檢視中，您可以看到 hello pod，以及這些容器所使用的 hello CPU 和記憶體資源中的 hello 容器的相關資訊：

![Kubernetes 資源](./media/container-service-kubernetes-ui/resources.png)

如果您沒有看到 hello 資源，您可能需要 toowait 幾分鐘的時間監視資料 toopropagate hello。

toosee hello 記錄檔以取得您的容器，按一下**檢視記錄檔**。

![Kubernetes 記錄檔](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a>檢視您的服務
在加法 toorunning 您容器 hello Kubernetes UI 已經建立外部`Service`的佈建負載平衡器 toobring 流量 toohello 容器在叢集中。

在 hello 左側瀏覽窗格中，按一下 **服務**tooview （應該只有一個） 的所有服務。

![Kubernetes 服務](./media/container-service-kubernetes-ui/service-deployed.png)

在該檢視中，您應該會看到已配置 tooyour 服務的外部端點 （IP 位址）。
如果您按一下該 IP 位址，應該會看到在負載平衡器後方執行的 Nginx 容器。

![nginx 檢視](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a>調整您的服務大小
在加法 tooviewing 物件在 hello UI，您可以編輯並更新 hello Kubernetes 應用程式開發介面的物件。

首先，請按一下**部署**hello 左導覽窗格 toosee hello 部署您的服務中。

一旦您是在該檢視中，按一下 hello 複本集，然後按一下**編輯**hello 上方瀏覽列中：

![Kubernetes 編輯](./media/container-service-kubernetes-ui/edit.png)

編輯 hello`spec.replicas`欄位 toobe `2`，然後按一下**更新**。

這樣 hello 數目複本 toodrop tootwo 刪除您 pod 的其中一個。

 

