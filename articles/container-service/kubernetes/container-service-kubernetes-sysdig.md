---
title: "aaaMonitor Azure Kubernetes 叢集 Sysdig |Microsoft 文件"
description: "使用 Sysdig 監視 Azure Container Service 中的 Kubernetes 叢集"
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
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a><span data-ttu-id="a0f49-103">使用 Sysdig 監視 Azure Container Service Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="a0f49-103">Monitor an Azure Container Service Kubernetes cluster using Sysdig</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0f49-104">必要條件</span><span class="sxs-lookup"><span data-stu-id="a0f49-104">Prerequisites</span></span>
<span data-ttu-id="a0f49-105">本逐步解說假設您已[使用 Azure Container Service 建立 Kubernetes 叢集](container-service-kubernetes-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="a0f49-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="a0f49-106">它也假設您已安裝的 hello azure cli 和 kubectl 工具。</span><span class="sxs-lookup"><span data-stu-id="a0f49-106">It also assumes that you have hello azure cli and kubectl tools installed.</span></span>

<span data-ttu-id="a0f49-107">您可以測試是否有 hello`az`安裝執行工具：</span><span class="sxs-lookup"><span data-stu-id="a0f49-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="a0f49-108">如果您沒有 hello`az`工具安裝，指示[這裡](https://github.com/azure/azure-cli#installation)。</span><span class="sxs-lookup"><span data-stu-id="a0f49-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="a0f49-109">您可以測試是否有 hello`kubectl`安裝執行工具：</span><span class="sxs-lookup"><span data-stu-id="a0f49-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="a0f49-110">如果您尚未安裝 `kubectl`，可以執行︰</span><span class="sxs-lookup"><span data-stu-id="a0f49-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a><span data-ttu-id="a0f49-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="a0f49-111">Sysdig</span></span>
<span data-ttu-id="a0f49-112">Sysdig 是一家外部監視即服務公司，可監視您在 Azure 中執行的 Kubernetes 叢集中的容器。</span><span class="sxs-lookup"><span data-stu-id="a0f49-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span></span> <span data-ttu-id="a0f49-113">使用 Sysdig 需要有效的 Sysdig 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a0f49-113">Using Sysdig requires an active Sysdig account.</span></span>
<span data-ttu-id="a0f49-114">您可以在他們的[網站](https://app.sysdigcloud.com)上註冊帳戶。</span><span class="sxs-lookup"><span data-stu-id="a0f49-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span></span>

<span data-ttu-id="a0f49-115">一旦您登入 toohello Sysdig 雲端網站，按一下您的使用者名稱，然後在 hello 頁面上您應該會看到您的 「 存取金鑰 」。</span><span class="sxs-lookup"><span data-stu-id="a0f49-115">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Sysdig API 金鑰](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a><span data-ttu-id="a0f49-117">安裝 hello Sysdig 代理程式 tooKubernetes</span><span class="sxs-lookup"><span data-stu-id="a0f49-117">Installing hello Sysdig agents tooKubernetes</span></span>
<span data-ttu-id="a0f49-118">您的容器 Sysdig 上執行的處理序每個機器使用 Kubernetes toomonitor `DaemonSet`。</span><span class="sxs-lookup"><span data-stu-id="a0f49-118">toomonitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span></span>
<span data-ttu-id="a0f49-119">DaemonSets 是每部機器執行單一容器執行個體的 Kubernetes API 物件。</span><span class="sxs-lookup"><span data-stu-id="a0f49-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span></span>
<span data-ttu-id="a0f49-120">變更就非常適合用以安裝工具 hello Sysdig 的監視代理程式。</span><span class="sxs-lookup"><span data-stu-id="a0f49-120">They're perfect for installing tools like hello Sysdig's monitoring agent.</span></span>

<span data-ttu-id="a0f49-121">tooinstall hello Sysdig daemonset，您應該先下載[hello 範本](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml)從 sysdig。</span><span class="sxs-lookup"><span data-stu-id="a0f49-121">tooinstall hello Sysdig daemonset, you should first download [hello template](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) from sysdig.</span></span> <span data-ttu-id="a0f49-122">將該檔案儲存為 `sysdig-daemonset.yaml`。</span><span class="sxs-lookup"><span data-stu-id="a0f49-122">Save that file as `sysdig-daemonset.yaml`.</span></span>

<span data-ttu-id="a0f49-123">在 Linux 與 OS X 上，您可以執行︰</span><span class="sxs-lookup"><span data-stu-id="a0f49-123">On Linux and OS X you can run:</span></span>

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

<span data-ttu-id="a0f49-124">在 PowerShell 中：</span><span class="sxs-lookup"><span data-stu-id="a0f49-124">In PowerShell:</span></span>

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

<span data-ttu-id="a0f49-125">接下來編輯該檔案 tooinsert 您的存取金鑰，您從 Sysdig 帳戶取得。</span><span class="sxs-lookup"><span data-stu-id="a0f49-125">Next edit that file tooinsert your Access Key, that you obtained from your Sysdig account.</span></span>

<span data-ttu-id="a0f49-126">最後，建立 hello DaemonSet:</span><span class="sxs-lookup"><span data-stu-id="a0f49-126">Finally, create hello DaemonSet:</span></span>

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a><span data-ttu-id="a0f49-127">檢視您的監視</span><span class="sxs-lookup"><span data-stu-id="a0f49-127">View your monitoring</span></span>
<span data-ttu-id="a0f49-128">一旦安裝並正在執行，hello 代理程式應該提取資料回復 tooSysdig。</span><span class="sxs-lookup"><span data-stu-id="a0f49-128">Once installed and running, hello agents should pump data back tooSysdig.</span></span>  <span data-ttu-id="a0f49-129">返回 toothe [sysdig 儀表板](https://app.sysdigcloud.com)，您應該看到的資訊關於您的容器。</span><span class="sxs-lookup"><span data-stu-id="a0f49-129">Go back toothe [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span></span>

<span data-ttu-id="a0f49-130">您也可以透過[新的儀表板精靈](https://app.sysdigcloud.com/#/dashboards/new)來安裝 Kubernetes 專用儀表板。</span><span class="sxs-lookup"><span data-stu-id="a0f49-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
