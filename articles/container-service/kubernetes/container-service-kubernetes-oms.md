---
title: "監視 Azure Kubernetes 叢集 - Operations Management | Microsoft Docs"
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
ms.openlocfilehash: bd5c81435c091d25bc14710589b7c043e9f56a25
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a><span data-ttu-id="6a216-103">使用 Microsoft Operations Management Suite (OMS) 監視 Azure Container Service 叢集</span><span class="sxs-lookup"><span data-stu-id="6a216-103">Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a216-104">必要條件</span><span class="sxs-lookup"><span data-stu-id="6a216-104">Prerequisites</span></span>
<span data-ttu-id="6a216-105">本逐步解說假設您已[使用 Azure Container Service 建立 Kubernetes 叢集](container-service-kubernetes-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="6a216-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="6a216-106">同時也假設您已經安裝 `az` Azure cli 和 `kubectl` 工具。</span><span class="sxs-lookup"><span data-stu-id="6a216-106">It also assumes that you have the `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="6a216-107">您可以藉由執行下列操作來測試是否已安裝 `az` 工具：</span><span class="sxs-lookup"><span data-stu-id="6a216-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="6a216-108">如果您尚未安裝 `az` 工具，[這裡](https://github.com/azure/azure-cli#installation)有指示。</span><span class="sxs-lookup"><span data-stu-id="6a216-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>  
<span data-ttu-id="6a216-109">或者，您可以使用 [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview)，它已為您安裝 `az` Azure cli 和 `kubectl` 工具。</span><span class="sxs-lookup"><span data-stu-id="6a216-109">Alternatively, you can use [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), which has the `az` Azure cli and `kubectl` tools already installed for you.</span></span>  

<span data-ttu-id="6a216-110">您可以藉由執行下列操作來測試是否已安裝 `kubectl` 工具：</span><span class="sxs-lookup"><span data-stu-id="6a216-110">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="6a216-111">如果您尚未安裝 `kubectl`，可以執行︰</span><span class="sxs-lookup"><span data-stu-id="6a216-111">If you don't have `kubectl` installed, you can run:</span></span>
```console
$ az acs kubernetes install-cli
```

<span data-ttu-id="6a216-112">若要測試您的 kubectl 工具中是否已安裝 kubernetes 金鑰，您可以執行：</span><span class="sxs-lookup"><span data-stu-id="6a216-112">To test if you have kubernetes keys installed in your kubectl tool you can run:</span></span>
```console
$ kubectl get nodes
```

<span data-ttu-id="6a216-113">如果上述命令發生錯誤，您必須將 kubernetes 叢集金鑰安裝到 kubectl 工具中。</span><span class="sxs-lookup"><span data-stu-id="6a216-113">If the above command errors out, you need to install kubernetes cluster keys into your kubectl tool.</span></span> <span data-ttu-id="6a216-114">您可以使用下列命令來執行此操作：</span><span class="sxs-lookup"><span data-stu-id="6a216-114">You can do that with the following command:</span></span>
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a><span data-ttu-id="6a216-115">使用 Operations Management Suite (OMS) 監視容器</span><span class="sxs-lookup"><span data-stu-id="6a216-115">Monitoring Containers with Operations Management Suite (OMS)</span></span>

<span data-ttu-id="6a216-116">Microsoft Operations Management (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。</span><span class="sxs-lookup"><span data-stu-id="6a216-116">Microsoft Operations Management (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="6a216-117">容器解決方案是 OMS Log Analytics 中的解決方案，可協助您在單一位置檢視容器詳細目錄、效能和記錄檔。</span><span class="sxs-lookup"><span data-stu-id="6a216-117">Container Solution is a solution in OMS Log Analytics, which helps you view the container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="6a216-118">您可以在集中式位置檢視記錄檔以稽核、對容器進行疑難排解，並尋找壟斷及佔用過量主機資源的容器。</span><span class="sxs-lookup"><span data-stu-id="6a216-118">You can audit, troubleshoot containers by viewing the logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="6a216-119">如需容器解決方案的詳細資訊，請參閱[容器解決方案 Log Analytics](../../log-analytics/log-analytics-containers.md)。</span><span class="sxs-lookup"><span data-stu-id="6a216-119">For more information about Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="installing-oms-on-kubernetes"></a><span data-ttu-id="6a216-120">在 Kubernetes 上安裝 OMS</span><span class="sxs-lookup"><span data-stu-id="6a216-120">Installing OMS on Kubernetes</span></span>

### <a name="obtain-your-workspace-id-and-key"></a><span data-ttu-id="6a216-121">取得您的工作區識別碼和金鑰</span><span class="sxs-lookup"><span data-stu-id="6a216-121">Obtain your workspace ID and key</span></span>
<span data-ttu-id="6a216-122">為了使 OMS 代理程式能與服務溝通，必須使用工作區識別碼和工作區金鑰來設定它。</span><span class="sxs-lookup"><span data-stu-id="6a216-122">For the OMS agent to talk to the service it needs to be configured with a workspace id and a workspace key.</span></span> <span data-ttu-id="6a216-123">若要取得工作區識別碼和金鑰，您必須在 <https://mms.microsoft.com> 建立一個 OMS 帳戶。請依步驟指示建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="6a216-123">To get the workspace id and key you need to create an OMS account at <https://mms.microsoft.com>. Please follow the steps to create an account.</span></span> <span data-ttu-id="6a216-124">建立帳戶之後，您必須依序按一下 [設定]、[連接的來源]、[Linux 伺服器]，以取得您的識別碼和金鑰，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6a216-124">Once you are done creating the account, you need to obtain your id and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-the-oms-agent-using-a-daemonset"></a><span data-ttu-id="6a216-125">使用 DaemonSet 安裝 OMS 代理程式</span><span class="sxs-lookup"><span data-stu-id="6a216-125">Install the OMS agent using a DaemonSet</span></span>
<span data-ttu-id="6a216-126">DaemonSet 是 Kubernetes 用來在叢集中每個主機上執行容器的單一執行個體。</span><span class="sxs-lookup"><span data-stu-id="6a216-126">DaemonSets are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="6a216-127">它們非常適合用來執行監視代理程式。</span><span class="sxs-lookup"><span data-stu-id="6a216-127">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="6a216-128">這是 [DaemonSet YAML 檔案](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)。</span><span class="sxs-lookup"><span data-stu-id="6a216-128">Here is the [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span></span> <span data-ttu-id="6a216-129">將它儲存到名為 `oms-daemonset.yaml` 的檔案，並將檔案中的 `WSID` 和 `KEY` 的預留位置值取代為您的工作區識別碼和金鑰。</span><span class="sxs-lookup"><span data-stu-id="6a216-129">Save it to a file named `oms-daemonset.yaml` and replace the place-holder values for `WSID` and `KEY` with your workspace id and key in the file.</span></span>

<span data-ttu-id="6a216-130">當您將工作區識別碼和金鑰新增至 DaemonSet 組態之後，就可以使用 `kubectl` 命令列工具在您的叢集上安裝 OMS：</span><span class="sxs-lookup"><span data-stu-id="6a216-130">Once you have added your workspace ID and key to the DaemonSet configuration, you can install the OMS agent on your cluster with the `kubectl` command line tool:</span></span>

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-the-oms-agent-using-a-kubernetes-secret"></a><span data-ttu-id="6a216-131">使用 Kubernetes 秘密安裝 OMS 代理程式</span><span class="sxs-lookup"><span data-stu-id="6a216-131">Installing the OMS agent using a Kubernetes Secret</span></span>
<span data-ttu-id="6a216-132">若要保護您的 OMS 工作區識別碼和金鑰，您可以使用 Kubernetes 秘密作為 DaemonSet YAML 檔案的一部分。</span><span class="sxs-lookup"><span data-stu-id="6a216-132">To protect your OMS workspace ID and key you can use Kubernetes Secret as a part of DaemonSet YAML file.</span></span>

 - <span data-ttu-id="6a216-133">複製指令碼、秘密範本檔案和 DaemonSet YAML 檔案 (從[存放庫](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes))，並確定它們位於相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="6a216-133">Copy the script, secret template file and the DaemonSet YAML file (from [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) and make sure they are on the same directory.</span></span> 
      - <span data-ttu-id="6a216-134">秘密產生指令碼 - secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="6a216-134">secret generating script - secret-gen.sh</span></span>
      - <span data-ttu-id="6a216-135">秘密範本 - secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="6a216-135">secret template - secret-template.yaml</span></span>
   - <span data-ttu-id="6a216-136">DaemonSet YAML 檔案 - omsagent-ds-secrets.yaml</span><span class="sxs-lookup"><span data-stu-id="6a216-136">DaemonSet YAML file - omsagent-ds-secrets.yaml</span></span>
 - <span data-ttu-id="6a216-137">執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="6a216-137">Run the script.</span></span> <span data-ttu-id="6a216-138">此指令碼會要求提供 OMS 工作區識別碼和主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="6a216-138">The script will ask for the OMS Workspace ID and Primary Key.</span></span> <span data-ttu-id="6a216-139">請插入該資訊，而指令碼會建立秘密 yaml 檔案，以便您執行。</span><span class="sxs-lookup"><span data-stu-id="6a216-139">Please insert that and the script will create a secret yaml file so you can run it.</span></span>   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - <span data-ttu-id="6a216-140">執行以下命令來建立秘密 Pod：``` kubectl create -f omsagentsecret.yaml ```</span><span class="sxs-lookup"><span data-stu-id="6a216-140">Create the secrets pod by running the following: ``` kubectl create -f omsagentsecret.yaml ```</span></span>
 
   - <span data-ttu-id="6a216-141">若要檢查，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="6a216-141">To check, run the following:</span></span> 

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
 
  - <span data-ttu-id="6a216-142">執行 ``` kubectl create -f omsagent-ds-secrets.yaml ``` 以建立您的 omsagent daemon-set</span><span class="sxs-lookup"><span data-stu-id="6a216-142">Create your omsagent daemon-set by running ``` kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

### <a name="conclusion"></a><span data-ttu-id="6a216-143">結論</span><span class="sxs-lookup"><span data-stu-id="6a216-143">Conclusion</span></span>
<span data-ttu-id="6a216-144">就這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="6a216-144">That's it!</span></span> <span data-ttu-id="6a216-145">幾分鐘後，您應該可以看到資料流向您的 OMS 儀表板。</span><span class="sxs-lookup"><span data-stu-id="6a216-145">After a few minutes, you should be able to see data flowing to your OMS dashboard.</span></span>
