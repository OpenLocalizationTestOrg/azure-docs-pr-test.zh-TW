---
title: "aaaMonitor Azure DC/OS 叢集 Operations Management |Microsoft 文件"
description: "使用 Microsoft Operations Management Suite 監視 Azure Container Service DC/OS 叢集。"
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a>使用 Operations Management Suite 監視 Azure Container Service DC/OS 叢集

Microsoft Operations Management Suite (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。 容器的解決方案是 OMS 記錄分析可協助您檢視 hello 容器清查、 效能和記錄檔中的單一位置中的解決方案。 您可以稽核、 疑難排解容器檢視 hello 記錄在集中式位置，並尋找雜訊耗用過多的容器主機上。

![](media/container-service-monitoring-oms/image1.png)

如需容器解決方案的詳細資訊，請參閱 toothe[容器方案記錄分析](../../log-analytics/log-analytics-containers.md)。

## <a name="setting-up-oms-from-hello-dcos-universe"></a>從 hello DC/OS universe 設定 OMS


本文假設您已設定 DC/OS 和已部署的 hello 叢集上的簡單的 web 容器應用程式。

### <a name="pre-requisite"></a>必要條件
- [Microsoft Azure 訂用帳戶](https://azure.microsoft.com/free/) - 您可以免費取得帳戶。  
- Microsoft OMS 工作區設定 - 請參閱下方的「步驟 3」
- 已安裝 [DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/)。

1. Hello DC/OS 儀表板中按一下 Universe，搜尋 'OMS' 如下所示。

![](media/container-service-monitoring-oms/image2.png)

2. 按一下 [Install] 。 您會看到快顯向上 hello OMS 版本資訊和**安裝套件**或**進階安裝** 按鈕。 當您按一下**進階安裝**，這會導致 toohello **OMS 特定組態屬性**頁面。

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. 在這裡，將會要求您 tooenter hello `wsid` (hello OMS 工作區識別碼) 和`wskey`（hello OMS 主索引鍵的 hello 工作區識別碼）。 這兩個 tooget`wsid`和`wskey`OMS 帳戶在需要 toocreate <https://mms.microsoft.com>。請遵循 hello 步驟 toocreate 帳戶。 一旦您完成建立 hello 帳戶之後，您需要 tooobtain 您`wsid`和`wskey`按一下**設定**，然後**連線來源**，然後**Linux 伺服器**，如下所示。

 ![](media/container-service-monitoring-oms/image5.png)

4. 選取 hello 數字您 OMS 執行個體，然後按一下 hello 「 檢閱和安裝 」 按鈕。 一般而言，您會想 toohave hello 數目 OMS 執行個體相等 toohello VM 的您在您代理程式的叢集數目。 適用於 Linux 的 OMS 代理程式是安裝做為其想 toocollect 資訊來監視和記錄資訊的每個 VM 上的個別容器。

## <a name="setting-up-a-simple-oms-dashboard"></a>設定簡單的 OMS 儀表板

一旦您已經安裝 hello OMS Agent for Linux hello Vm 上下, 一個步驟是 tooset hello OMS 儀表板上。 有兩種方式 toodo 這： OMS 入口網站或 Azure 入口網站。

### <a name="oms-portal"></a>OMS 入口網站 

登入 toohello OMS 入口網站 (<https://mms.microsoft.com>)，並移 toohello**解決方案資源庫**。

![](media/container-service-monitoring-oms/image6.png)

當您在 hello**解決方案資源庫**，選取**容器**。

![](media/container-service-monitoring-oms/image7.png)

一旦您已選取 hello 容器解決方案，您會看到 hello hello OMS 概觀儀表板頁面上的磚。 一旦 hello 內嵌的容器資料具有索引，您會看到 hello 磚填入解決方案檢視磚上的資訊。

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a>Azure 入口網站 

登入 tooAzure 入口網站則位於<https://portal.microsoft.com/>。 移至 [Marketplace]，選取 [監視 + 管理]，然後按一下 [查看全部]。 接著在搜尋中輸入 `containers` (容器)。 您會看到 [容器] hello 搜尋結果中。 選取 [Containers]\(容器)，然後按一下 [建立]。

![](media/container-service-monitoring-oms/image9.png)

按一下 [建立] 後，它會要求您提供您的工作區。 選取您的工作區，或是如果您沒有工作區，請建立新的工作區。

![](media/container-service-monitoring-oms/image10.PNG)

選取您的工作區後，按一下 [建立]。

![](media/container-service-monitoring-oms/image11.png)

如需有關 hello 容器項 OMS 解決方案的詳細資訊，請參閱 toothe[容器方案記錄分析](../../log-analytics/log-analytics-containers.md)。

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a>如何 tooscale OMS 代理程式與 ACS DC/OS 中 

如果您需要 toohave 安裝 OMS 代理程式，除非 hello 實際節點計數，或您會藉由新增更多 VM VMSS 向上擴充，您可以藉由調整 hello`msoms`服務。

您可以移 tooMarathon 或 hello DC/OS UI 服務 索引標籤，並向上擴充節點計數。

![](media/container-service-monitoring-oms/image12.PNG)

這會將部署 tooother 節點尚未部署 hello OMS 代理程式。

## <a name="uninstall-ms-oms"></a>解除安裝 MS OMS

toouninstall MS OMS 輸入 hello 下列命令：

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a>請告訴我們！
哪些資訊是有用的？ 缺少哪些資訊？ 還有什麼您需要此 toobe 有用了？ 請透過 <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a> 告訴我們。

## <a name="next-steps"></a>後續步驟

 既然您已設定 OMS toomonitor 您容器[看到儀表板容器](../../log-analytics/log-analytics-containers.md)。
