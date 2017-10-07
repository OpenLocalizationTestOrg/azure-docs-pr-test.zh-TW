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
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a><span data-ttu-id="a7fcc-103">使用 Microsoft Operations Management Suite (OMS) 監視 Azure Container Service 叢集</span><span class="sxs-lookup"><span data-stu-id="a7fcc-103">Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7fcc-104">必要條件</span><span class="sxs-lookup"><span data-stu-id="a7fcc-104">Prerequisites</span></span>
<span data-ttu-id="a7fcc-105">本逐步解說假設您已[使用 Azure Container Service 建立 Kubernetes 叢集](container-service-kubernetes-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="a7fcc-106">它也假設您擁有 hello `az` Azure cli 和`kubectl`安裝工具。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="a7fcc-107">您可以測試是否有 hello`az`安裝執行工具：</span><span class="sxs-lookup"><span data-stu-id="a7fcc-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="a7fcc-108">如果您沒有 hello`az`工具安裝，指示[這裡](https://github.com/azure/azure-cli#installation)。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>  
<span data-ttu-id="a7fcc-109">或者，您可以使用[Azure 雲端殼層](https://docs.microsoft.com/en-us/azure/cloud-shell/overview)，其具有 hello `az` Azure cli 和`kubectl`為您已安裝的工具。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-109">Alternatively, you can use [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), which has hello `az` Azure cli and `kubectl` tools already installed for you.</span></span>  

<span data-ttu-id="a7fcc-110">您可以測試是否有 hello`kubectl`安裝執行工具：</span><span class="sxs-lookup"><span data-stu-id="a7fcc-110">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="a7fcc-111">如果您尚未安裝 `kubectl`，可以執行︰</span><span class="sxs-lookup"><span data-stu-id="a7fcc-111">If you don't have `kubectl` installed, you can run:</span></span>
```console
$ az acs kubernetes install-cli
```

<span data-ttu-id="a7fcc-112">如果您有安裝在您可以執行您 kubectl 工具 kubernetes 金鑰，tootest:</span><span class="sxs-lookup"><span data-stu-id="a7fcc-112">tootest if you have kubernetes keys installed in your kubectl tool you can run:</span></span>
```console
$ kubectl get nodes
```

<span data-ttu-id="a7fcc-113">如果 hello 上述命令錯誤，您需要到 kubectl 工具 tooinstall kubernetes 叢集索引鍵。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-113">If hello above command errors out, you need tooinstall kubernetes cluster keys into your kubectl tool.</span></span> <span data-ttu-id="a7fcc-114">您可以執行，以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="a7fcc-114">You can do that with hello following command:</span></span>
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a><span data-ttu-id="a7fcc-115">使用 Operations Management Suite (OMS) 監視容器</span><span class="sxs-lookup"><span data-stu-id="a7fcc-115">Monitoring Containers with Operations Management Suite (OMS)</span></span>

<span data-ttu-id="a7fcc-116">Microsoft Operations Management (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-116">Microsoft Operations Management (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="a7fcc-117">容器的解決方案是 OMS 記錄分析可協助您檢視 hello 容器清查、 效能和記錄檔中的單一位置中的解決方案。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-117">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="a7fcc-118">您可以稽核、 疑難排解容器檢視 hello 記錄在集中式位置，並尋找雜訊耗用過多的容器主機上。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-118">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="a7fcc-119">如需容器解決方案的詳細資訊，請參閱 toothe[容器方案記錄分析](../../log-analytics/log-analytics-containers.md)。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-119">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="installing-oms-on-kubernetes"></a><span data-ttu-id="a7fcc-120">在 Kubernetes 上安裝 OMS</span><span class="sxs-lookup"><span data-stu-id="a7fcc-120">Installing OMS on Kubernetes</span></span>

### <a name="obtain-your-workspace-id-and-key"></a><span data-ttu-id="a7fcc-121">取得您的工作區識別碼和金鑰</span><span class="sxs-lookup"><span data-stu-id="a7fcc-121">Obtain your workspace ID and key</span></span>
<span data-ttu-id="a7fcc-122">Hello OMS 代理程式 tootalk toohello 服務需要 toobe 設定工作區識別碼及工作區金鑰。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-122">For hello OMS agent tootalk toohello service it needs toobe configured with a workspace id and a workspace key.</span></span> <span data-ttu-id="a7fcc-123">tooget hello 工作區識別碼和金鑰需要 toocreate OMS 帳戶在<https://mms.microsoft.com>。請遵循 hello 步驟 toocreate 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-123">tooget hello workspace id and key you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="a7fcc-124">一旦您完成建立 hello 帳戶之後，您需要 tooobtain 識別碼及金鑰即可**設定**，然後**連線來源**，然後**Linux 伺服器**，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-124">Once you are done creating hello account, you need tooobtain your id and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a><span data-ttu-id="a7fcc-125">安裝使用 DaemonSet hello OMS 代理程式</span><span class="sxs-lookup"><span data-stu-id="a7fcc-125">Install hello OMS agent using a DaemonSet</span></span>
<span data-ttu-id="a7fcc-126">DaemonSets 所使用的 Kubernetes toorun hello 叢集中各主機上的容器的單一執行個體。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-126">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="a7fcc-127">它們非常適合用來執行監視代理程式。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-127">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="a7fcc-128">以下是 hello [DaemonSet YAML 檔案](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-128">Here is hello [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span></span> <span data-ttu-id="a7fcc-129">將其儲存 tooa 檔案命名為`oms-daemonset.yaml`hello 預留位置值取代和`WSID`和`KEY`與您的工作區識別碼 hello 檔案中的金鑰。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-129">Save it tooa file named `oms-daemonset.yaml` and replace hello place-holder values for `WSID` and `KEY` with your workspace id and key in hello file.</span></span>

<span data-ttu-id="a7fcc-130">一旦您加入工作區識別碼和金鑰 toohello DaemonSet 組態，您可以在 hello 與叢集上安裝 hello OMS 代理程式`kubectl`命令列工具：</span><span class="sxs-lookup"><span data-stu-id="a7fcc-130">Once you have added your workspace ID and key toohello DaemonSet configuration, you can install hello OMS agent on your cluster with hello `kubectl` command line tool:</span></span>

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a><span data-ttu-id="a7fcc-131">安裝使用 Kubernetes 密碼 hello OMS 代理程式</span><span class="sxs-lookup"><span data-stu-id="a7fcc-131">Installing hello OMS agent using a Kubernetes Secret</span></span>
<span data-ttu-id="a7fcc-132">tooprotect 您的 OMS 工作區識別碼和金鑰，您可以使用 Kubernetes 密碼 DaemonSet YAML 檔案的一部分。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-132">tooprotect your OMS workspace ID and key you can use Kubernetes Secret as a part of DaemonSet YAML file.</span></span>

 - <span data-ttu-id="a7fcc-133">複製 hello 指令碼、 密碼的範本檔案和 hello DaemonSet YAML 檔案 (從[儲存機制](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes))，並確定它們是在 hello 相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-133">Copy hello script, secret template file and hello DaemonSet YAML file (from [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) and make sure they are on hello same directory.</span></span> 
      - <span data-ttu-id="a7fcc-134">秘密產生指令碼 - secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="a7fcc-134">secret generating script - secret-gen.sh</span></span>
      - <span data-ttu-id="a7fcc-135">秘密範本 - secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="a7fcc-135">secret template - secret-template.yaml</span></span>
   - <span data-ttu-id="a7fcc-136">DaemonSet YAML 檔案 - omsagent-ds-secrets.yaml</span><span class="sxs-lookup"><span data-stu-id="a7fcc-136">DaemonSet YAML file - omsagent-ds-secrets.yaml</span></span>
 - <span data-ttu-id="a7fcc-137">執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-137">Run hello script.</span></span> <span data-ttu-id="a7fcc-138">hello 指令碼會要求 hello OMS 工作區識別碼及主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-138">hello script will ask for hello OMS Workspace ID and Primary Key.</span></span> <span data-ttu-id="a7fcc-139">請插入，並 hello 指令碼會建立密碼 yaml 檔案，因此您可以執行它。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-139">Please insert that and hello script will create a secret yaml file so you can run it.</span></span>   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - <span data-ttu-id="a7fcc-140">建立 hello 密碼 pod 執行 hello 下列：``` kubectl create -f omsagentsecret.yaml ```</span><span class="sxs-lookup"><span data-stu-id="a7fcc-140">Create hello secrets pod by running hello following: ``` kubectl create -f omsagentsecret.yaml ```</span></span>
 
   - <span data-ttu-id="a7fcc-141">toocheck，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="a7fcc-141">toocheck, run hello following:</span></span> 

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
 
  - <span data-ttu-id="a7fcc-142">執行 ``` kubectl create -f omsagent-ds-secrets.yaml ``` 以建立您的 omsagent daemon-set</span><span class="sxs-lookup"><span data-stu-id="a7fcc-142">Create your omsagent daemon-set by running ``` kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

### <a name="conclusion"></a><span data-ttu-id="a7fcc-143">結論</span><span class="sxs-lookup"><span data-stu-id="a7fcc-143">Conclusion</span></span>
<span data-ttu-id="a7fcc-144">就這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="a7fcc-144">That's it!</span></span> <span data-ttu-id="a7fcc-145">請稍候幾分鐘，您應該能夠 toosee 資料流動 tooyour OMS 儀表板。</span><span class="sxs-lookup"><span data-stu-id="a7fcc-145">After a few minutes, you should be able toosee data flowing tooyour OMS dashboard.</span></span>
