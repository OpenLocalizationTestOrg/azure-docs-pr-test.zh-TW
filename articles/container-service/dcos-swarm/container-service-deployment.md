---
title: "在 Azure 中部署 Docker 容器叢集 | Microsoft Docs"
description: "在 Azure Container Service 中使用 Azure 入口網站或 Resource Manager 範本部署 Kubernetes、DC/OS，或 Docker Swarm 解決方案。"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure, dcos, swarm, kubernetes, azure container service, acs
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 0ef256537bf095e2a5d582bd345a9c8dcede2095
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-the-azure-portal"></a><span data-ttu-id="d27e8-104">使用 Azure 入口網站部署 Docker 容器主控解決方案</span><span class="sxs-lookup"><span data-stu-id="d27e8-104">Deploy a Docker container hosting solution using the Azure portal</span></span>



<span data-ttu-id="d27e8-105">Azure Container Service 支援快速部署常用的開放原始碼容器叢集和協調流程解決方案。</span><span class="sxs-lookup"><span data-stu-id="d27e8-105">Azure Container Service provides rapid deployment of popular open-source container clustering and orchestration solutions.</span></span> <span data-ttu-id="d27e8-106">本文件會逐步引導您使用 Azure 入口網站或Azure Resource Manager 快速入門範本來部署 Azure Container Service 叢集。</span><span class="sxs-lookup"><span data-stu-id="d27e8-106">This document walks you through deploying an Azure Container Service cluster by using the Azure portal or an Azure Resource Manager quickstart template.</span></span> 

<span data-ttu-id="d27e8-107">您也可以使用 [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) 或 Azure Container Service API 來部署 Azure Container Service 叢集。</span><span class="sxs-lookup"><span data-stu-id="d27e8-107">You can also deploy an Azure Container Service cluster by using the [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) or the Azure Container Service APIs.</span></span>

<span data-ttu-id="d27e8-108">若為背景，請參閱 [Azure Container Service 簡介](../container-service-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="d27e8-108">For background, see [Azure Container Service introduction](../container-service-intro.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d27e8-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="d27e8-109">Prerequisites</span></span>

* <span data-ttu-id="d27e8-110">**Azure 訂用帳戶**：如果您沒有帳戶，請註冊[免費試用](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935)。</span><span class="sxs-lookup"><span data-stu-id="d27e8-110">**Azure subscription**: If you don't have one, sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> <span data-ttu-id="d27e8-111">針對較大的叢集，請考慮隨用隨付訂用帳戶或其他購買選項。</span><span class="sxs-lookup"><span data-stu-id="d27e8-111">For a larger cluster, consider a pay-as-you go subscription or other purchase options.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d27e8-112">您的 Azure 訂用帳戶使用量和[資源配額](../../azure-subscription-service-limits.md)(例如核心配額) 可以限制您部署的叢集大小。</span><span class="sxs-lookup"><span data-stu-id="d27e8-112">Your Azure subscription usage and [resource quotas](../../azure-subscription-service-limits.md), such as cores quotas, can limit the size of the cluster you deploy.</span></span> <span data-ttu-id="d27e8-113">若要要求增加配額，可免費[開啟線上客戶支援要求](../../azure-supportability/how-to-create-azure-support-request.md)。</span><span class="sxs-lookup"><span data-stu-id="d27e8-113">To request a quota increase, open an [online customer support request](../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
    >

* <span data-ttu-id="d27e8-114">**SSH RSA 公開金鑰**︰透過入口網站或其中一個 Azure 快速入門範本部署時，您必須提供公開金鑰，以便對 Azure Container Service 虛擬機器進行驗證。</span><span class="sxs-lookup"><span data-stu-id="d27e8-114">**SSH RSA public key**: When deploying through the portal or one of the Azure quickstart templates, you need to provide the public key for authentication against Azure Container Service virtual machines.</span></span> <span data-ttu-id="d27e8-115">若要建立安全殼層 (SSH) RSA 金鑰，請參閱 [OS X 和 Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) 和 [Windows](../../virtual-machines/linux/ssh-from-windows.md)指引。</span><span class="sxs-lookup"><span data-stu-id="d27e8-115">To create Secure Shell (SSH) RSA keys, see the [OS X and Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../../virtual-machines/linux/ssh-from-windows.md) guidance.</span></span> 

* <span data-ttu-id="d27e8-116">**服務主體用戶端識別碼和密碼** (僅限 Kubernetes)：如需建立 Azure Active Directory 服務主體的詳細資訊和指引，請參閱[關於 Kubernetes 叢集的服務主體](../kubernetes/container-service-kubernetes-service-principal.md)。</span><span class="sxs-lookup"><span data-stu-id="d27e8-116">**Service principal client ID and secret** (Kubernetes only): For more information and guidance to create an Azure Active Directory service principal, see [About the service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>



## <a name="create-a-cluster-by-using-the-azure-portal"></a><span data-ttu-id="d27e8-117">使用 Azure 入口網站建立叢集</span><span class="sxs-lookup"><span data-stu-id="d27e8-117">Create a cluster by using the Azure portal</span></span>
1. <span data-ttu-id="d27e8-118">登入 Azure 入口網站、選取[新增]，並在 Azure Marketplace 中搜尋 [Azure Container Service]。</span><span class="sxs-lookup"><span data-stu-id="d27e8-118">Sign in to the Azure portal, select **New**, and search the Azure Marketplace for **Azure Container Service**.</span></span>

    ![Marketplace 中的 Azure Container Service](./media/container-service-deployment/acs-portal1.png)  <br />

2. <span data-ttu-id="d27e8-120">按一下 [Azure Container Service]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="d27e8-120">Click **Azure Container Service**, and click **Create**.</span></span>

3. <span data-ttu-id="d27e8-121">在 [基本概念] 刀鋒視窗中，輸入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="d27e8-121">On the **Basics** blade, enter the following information:</span></span>

    * <span data-ttu-id="d27e8-122">**Orchestrator**︰ 選取其中一個容器 Orchestrators 以在叢集上部署。</span><span class="sxs-lookup"><span data-stu-id="d27e8-122">**Orchestrator**: Select one of the container orchestrators to deploy on the cluster.</span></span>
        * <span data-ttu-id="d27e8-123">**DC/OS**：部署 DC/OS 叢集。</span><span class="sxs-lookup"><span data-stu-id="d27e8-123">**DC/OS**: Deploys a DC/OS cluster.</span></span>
        * <span data-ttu-id="d27e8-124">**Swarm**：部署 Docker Swarm 叢集。</span><span class="sxs-lookup"><span data-stu-id="d27e8-124">**Swarm**: Deploys a Docker Swarm cluster.</span></span>
        * <span data-ttu-id="d27e8-125">**Kubernetes**：部署 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="d27e8-125">**Kubernetes**: Deploys a Kubernetes cluster.</span></span>
    * <span data-ttu-id="d27e8-126">**訂用帳戶**：選取 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d27e8-126">**Subscription**: Select an Azure subscription.</span></span>
    * <span data-ttu-id="d27e8-127">**資源群組**：輸入部署的新資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="d27e8-127">**Resource group**: Enter the name of a new resource group for the deployment.</span></span>
    * <span data-ttu-id="d27e8-128">**位置**：選取 Azure Container Service 部署的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="d27e8-128">**Location**: Select an Azure region for the Azure Container Service deployment.</span></span> <span data-ttu-id="d27e8-129">如需可用性，請查看[依區域提供的產品](https://azure.microsoft.com/regions/services/)。</span><span class="sxs-lookup"><span data-stu-id="d27e8-129">For availability, check [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
    
    ![基本設定](./media/container-service-deployment/acs-portal3.png)  <br />
    
    <span data-ttu-id="d27e8-131">準備好繼續時請按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="d27e8-131">Click **OK** when you're ready to proceed.</span></span>

4. <span data-ttu-id="d27e8-132">在 [主機組態] 刀鋒視窗中，針對叢集中的 Linux 主要節點輸入下列設定 (有些是每個 Orchestrator 的特定設定)︰</span><span class="sxs-lookup"><span data-stu-id="d27e8-132">On the **Master configuration** blade, enter the following settings for the Linux master node or nodes in the cluster (some settings are specific to each orchestrator):</span></span>

    * <span data-ttu-id="d27e8-133">**主要 DNS 名稱**︰用來為主要節點建立唯一完整網域名稱 (FQDN) 的前置詞。</span><span class="sxs-lookup"><span data-stu-id="d27e8-133">**Master DNS name**: The prefix used to create a unique fully qualified domain name (FQDN) for the master.</span></span> <span data-ttu-id="d27e8-134">主要 FQDN 的格式是 *prefix*mgmt.*location*.cloudapp.azure.com。</span><span class="sxs-lookup"><span data-stu-id="d27e8-134">The master FQDN is of the form *prefix*mgmt.*location*.cloudapp.azure.com.</span></span>
    * <span data-ttu-id="d27e8-135">**使用者名稱**︰在叢集中每個 Linux 虛擬機器上帳戶的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="d27e8-135">**User name**: The user name for an account on each of the Linux virtual machines in the cluster.</span></span>
    * <span data-ttu-id="d27e8-136">**SSH RSA 公開金鑰**：新增要用於對 Linux 虛擬機器進行驗證的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="d27e8-136">**SSH RSA public key**: Add the public key to be used for authentication against the Linux virtual machines.</span></span> <span data-ttu-id="d27e8-137">請務必不要讓此金鑰包含分行符號，而讓它包含 `ssh-rsa` 前置詞。</span><span class="sxs-lookup"><span data-stu-id="d27e8-137">It is important that this key contains no line breaks, and it includes the `ssh-rsa` prefix.</span></span> <span data-ttu-id="d27e8-138">`username@domain` 後置詞是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="d27e8-138">The `username@domain` postfix is optional.</span></span> <span data-ttu-id="d27e8-139">金鑰應如下所示：**ssh-rsa AAAAB3Nz...<...>...UcyupgH azureuser@linuxvm**。</span><span class="sxs-lookup"><span data-stu-id="d27e8-139">The key should look something like the following: **ssh-rsa AAAAB3Nz...<...>...UcyupgH azureuser@linuxvm**.</span></span> 
    * <span data-ttu-id="d27e8-140">**服務主體**︰如果您選取 Kubernetes Orchestrator，請輸入 Azure Active Directory 「服務主體用戶端識別碼」(也稱為 appId) 和「服務主體用戶端密碼」。</span><span class="sxs-lookup"><span data-stu-id="d27e8-140">**Service principal**: If you selected the Kubernetes orchestrator, enter an Azure Active Directory **Service principal client ID** (also called the appId) and **Service principal client secret** (password).</span></span> <span data-ttu-id="d27e8-141">如需詳細資訊，請參閱[關於 Kubernetes 叢集的服務主體](../kubernetes/container-service-kubernetes-service-principal.md)。</span><span class="sxs-lookup"><span data-stu-id="d27e8-141">For more information, see [About the service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>
    * <span data-ttu-id="d27e8-142">**主要主機計數**：叢集中主要主機的數目。</span><span class="sxs-lookup"><span data-stu-id="d27e8-142">**Master count**: The number of masters in the cluster.</span></span>
    * <span data-ttu-id="d27e8-143">**VM 診斷**︰對於某些 Orchestrator，您可以啟用主要節點上的 VM 診斷。</span><span class="sxs-lookup"><span data-stu-id="d27e8-143">**VM diagnostics**: For some orchestrators, you can enable VM diagnostics on the masters.</span></span>

    ![主要組態](./media/container-service-deployment/acs-portal4.png)  <br />

    <span data-ttu-id="d27e8-145">準備好繼續時請按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="d27e8-145">Click **OK** when you're ready to proceed.</span></span>

5. <span data-ttu-id="d27e8-146">在 [代理程式組態] 刀鋒視窗中，輸入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="d27e8-146">On the **Agent configuration** blade, enter the following information:</span></span>

    * <span data-ttu-id="d27e8-147">**代理程式計數**：若為 Docker Swarm 和 Kubernetes，此值是代理程式擴展集內的初始代理程式數目。</span><span class="sxs-lookup"><span data-stu-id="d27e8-147">**Agent count**: For Docker Swarm and Kubernetes, this value is the initial number of agents in the agent scale set.</span></span> <span data-ttu-id="d27e8-148">若為 DC/OS，此值是私人擴展集內的初始代理程式數目。</span><span class="sxs-lookup"><span data-stu-id="d27e8-148">For DC/OS, it is the initial number of agents in a private scale set.</span></span> <span data-ttu-id="d27e8-149">此外，也會建立 DC/OS 的公用擴展集，其中包含預先決定的代理程式數目。</span><span class="sxs-lookup"><span data-stu-id="d27e8-149">Additionally, a public scale set is created for DC/OS, which contains a predetermined number of agents.</span></span> <span data-ttu-id="d27e8-150">此公用擴展集內的代理程式數目是由叢集中的主要節點數目來決定：一個主要節點需要一個公用代理程式，而三或五個主要節點則需要兩個公用代理程式。</span><span class="sxs-lookup"><span data-stu-id="d27e8-150">The number of agents in this public scale set is determined by the number of masters in the cluster: one public agent for one master, and two public agents for three or five masters.</span></span>
    * <span data-ttu-id="d27e8-151">**代理程式虛擬機器大小**：代理程式虛擬機器的大小。</span><span class="sxs-lookup"><span data-stu-id="d27e8-151">**Agent virtual machine size**: The size of the agent virtual machines.</span></span>
    * <span data-ttu-id="d27e8-152">**作業系統**︰這個設定只有在您選取 Kubernetes Orchestrator 時才可以使用。</span><span class="sxs-lookup"><span data-stu-id="d27e8-152">**Operating system**: This setting is currently available only if you selected the Kubernetes orchestrator.</span></span> <span data-ttu-id="d27e8-153">選擇要在代理程式上執行 Linux 散發套件或 Windows Server 作業系統。</span><span class="sxs-lookup"><span data-stu-id="d27e8-153">Choose either a Linux distribution or a Windows Server operating system to run on the agents.</span></span> <span data-ttu-id="d27e8-154">此設定會決定您的叢集可以執行 Linux 或 Windows 容器應用程式。</span><span class="sxs-lookup"><span data-stu-id="d27e8-154">This setting determines whether your cluster can run Linux or Windows container apps.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="d27e8-155">對於 Kubernetes 叢集，Windows 容器支援處於預覽階段。</span><span class="sxs-lookup"><span data-stu-id="d27e8-155">Windows container support is in preview for Kubernetes clusters.</span></span> <span data-ttu-id="d27e8-156">在 DC/OS 和 Swarm 叢集上，Azure Container Service 中目前只支援 Linux 代理程式。</span><span class="sxs-lookup"><span data-stu-id="d27e8-156">On DC/OS and Swarm clusters, only Linux agents are currently supported in Azure Container Service.</span></span>

    * <span data-ttu-id="d27e8-157">**代理程式認證**︰如果您選取 Windows 作業系統，請輸入代理程式 VM 的系統管理員「使用者名稱」和「密碼」。</span><span class="sxs-lookup"><span data-stu-id="d27e8-157">**Agent credentials**: If you selected the Windows operating system, enter an administrator **User name** and **Password** for the agent VMs.</span></span> 

    ![代理程式組態](./media/container-service-deployment/acs-portal5.png)  <br />

    <span data-ttu-id="d27e8-159">準備好繼續時請按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="d27e8-159">Click **OK** when you're ready to proceed.</span></span>

6. <span data-ttu-id="d27e8-160">服務驗證完成後請按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="d27e8-160">After service validation finishes, click **OK**.</span></span>

    ![驗證](./media/container-service-deployment/acs-portal6.png)  <br />

7. <span data-ttu-id="d27e8-162">檢閱條款。</span><span class="sxs-lookup"><span data-stu-id="d27e8-162">Review the terms.</span></span> <span data-ttu-id="d27e8-163">若要啟動部署程序，請按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="d27e8-163">To start the deployment process, click **Create**.</span></span>

    <span data-ttu-id="d27e8-164">如果您已選擇將部署釘選到 Azure 入口網站，您就可以看到部署狀態。</span><span class="sxs-lookup"><span data-stu-id="d27e8-164">If you've elected to pin the deployment to the Azure portal, you can see the deployment status.</span></span>

    ![部署狀態](./media/container-service-deployment/acs-portal8.png)  <br />

<span data-ttu-id="d27e8-166">部署需要數分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="d27e8-166">The deployment takes several minutes to complete.</span></span> <span data-ttu-id="d27e8-167">然後，Azure Container Service 叢集便可供使用。</span><span class="sxs-lookup"><span data-stu-id="d27e8-167">Then, the Azure Container Service cluster is ready for use.</span></span>


## <a name="create-a-cluster-by-using-a-quickstart-template"></a><span data-ttu-id="d27e8-168">使用快速入門範本建立叢集</span><span class="sxs-lookup"><span data-stu-id="d27e8-168">Create a cluster by using a quickstart template</span></span>
<span data-ttu-id="d27e8-169">Azure 快速入門範本可供在 Azure Container Service 中部署叢集。</span><span class="sxs-lookup"><span data-stu-id="d27e8-169">Azure quickstart templates are available to deploy a cluster in Azure Container Service.</span></span> <span data-ttu-id="d27e8-170">提供的快速入門範本可以修改為包含其他或進階 Azure 組態。</span><span class="sxs-lookup"><span data-stu-id="d27e8-170">The provided quickstart templates can be modified to include additional or advanced Azure configuration.</span></span> <span data-ttu-id="d27e8-171">若要使用 Azure 快速入門範本建立 Azure Container Service 叢集，您需要 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d27e8-171">To create an Azure Container Service cluster by using an Azure quickstart template, you need an Azure subscription.</span></span> <span data-ttu-id="d27e8-172">如果您沒有訂用帳戶，請註冊[免費試用](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935)。</span><span class="sxs-lookup"><span data-stu-id="d27e8-172">If you don't have one, then sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> 

<span data-ttu-id="d27e8-173">請使用範本和 Azure CLI 2.0 並遵循下列步驟來部署叢集 (請參閱[安裝和設定指示](/cli/azure/install-az-cli2))。</span><span class="sxs-lookup"><span data-stu-id="d27e8-173">Follow these steps to deploy a cluster using a template and the Azure CLI 2.0 (see [installation and setup instructions](/cli/azure/install-az-cli2)).</span></span>

> [!NOTE] 
> <span data-ttu-id="d27e8-174">如果您在 Windows 系統上，可以使用 Azure PowerShell 並以類似的步驟來部署範本。</span><span class="sxs-lookup"><span data-stu-id="d27e8-174">If you're on a Windows system, you can use similar steps to deploy a template using Azure PowerShell.</span></span> <span data-ttu-id="d27e8-175">請參閱本節稍後的步驟。</span><span class="sxs-lookup"><span data-stu-id="d27e8-175">See steps later in this section.</span></span> <span data-ttu-id="d27e8-176">您也可以透過[入口網站](../../azure-resource-manager/resource-group-template-deploy-portal.md)或其他方法來部署範本。</span><span class="sxs-lookup"><span data-stu-id="d27e8-176">You can also deploy a template through the [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) or other methods.</span></span>

1. <span data-ttu-id="d27e8-177">若要部署 DC/OS、Docker Swarm 或 Kubernetes 叢集，請從 GitHub 選取其中一個可用的快速入門範本。</span><span class="sxs-lookup"><span data-stu-id="d27e8-177">To deploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of the available quickstart templates from GitHub.</span></span> <span data-ttu-id="d27e8-178">部分清單如下。</span><span class="sxs-lookup"><span data-stu-id="d27e8-178">A partial list follows.</span></span> <span data-ttu-id="d27e8-179">除了預設的 Orchestrator 選項有所不同外，DC/OS 和 Swarm 範本完全相同。</span><span class="sxs-lookup"><span data-stu-id="d27e8-179">The DC/OS and Swarm templates are the same, except for the default orchestrator selection.</span></span>

    * [<span data-ttu-id="d27e8-180">DC/OS 範本</span><span class="sxs-lookup"><span data-stu-id="d27e8-180">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="d27e8-181">Swarm 範本</span><span class="sxs-lookup"><span data-stu-id="d27e8-181">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="d27e8-182">Kubernetes 範本</span><span class="sxs-lookup"><span data-stu-id="d27e8-182">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="d27e8-183">登入您的 Azure 帳戶 (`az login`)，並確定 Azure CLI 已連接至 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d27e8-183">Log in to your Azure account (`az login`), and make sure that the Azure CLI is connected to your Azure subscription.</span></span> <span data-ttu-id="d27e8-184">您可以使用下列命令來查看預設訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="d27e8-184">You can see the default subscription by using the following command:</span></span>

    ```azurecli
    az account show
    ```
    
    <span data-ttu-id="d27e8-185">如果您有多個訂用帳戶，而且需要設定不同的預設訂用帳戶，請執行 `az account set --subscription` 並指定訂用帳戶識別碼或名稱。</span><span class="sxs-lookup"><span data-stu-id="d27e8-185">If you have more than one subscription and need to set a different default subscription, run `az account set --subscription` and specify the subscription ID or name.</span></span>

3. <span data-ttu-id="d27e8-186">最佳作法是使用新的資源群組進行部署。</span><span class="sxs-lookup"><span data-stu-id="d27e8-186">As a best practice, use a new resource group for the deployment.</span></span> <span data-ttu-id="d27e8-187">若要建立資源群組，請使用 `az group create` 命令指定資源群組名稱和位置：</span><span class="sxs-lookup"><span data-stu-id="d27e8-187">To create a resource group, use the `az group create` command specify a resource group name and location:</span></span> 

    ```azurecli
    az group create --name "RESOURCE_GROUP" --location "LOCATION"
    ```

4. <span data-ttu-id="d27e8-188">建立包含必要範本參數的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="d27e8-188">Create a JSON file containing the required template parameters.</span></span> <span data-ttu-id="d27e8-189">下載名為 `azuredeploy.parameters.json` 的參數檔，其隨附於 GitHub 中的 Azure Container Service 範本 `azuredeploy.json`。</span><span class="sxs-lookup"><span data-stu-id="d27e8-189">Download the parameters file named `azuredeploy.parameters.json` that accompanies the Azure Container Service template `azuredeploy.json` in GitHub.</span></span> <span data-ttu-id="d27e8-190">輸入您叢集所需的參數值。</span><span class="sxs-lookup"><span data-stu-id="d27e8-190">Enter required parameter values for your cluster.</span></span> 

    <span data-ttu-id="d27e8-191">例如，若要使用 [DC/OS 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)，請提供 `dnsNamePrefix` 和 `sshRSAPublicKey` 的參數值。</span><span class="sxs-lookup"><span data-stu-id="d27e8-191">For example, to use the [DC/OS template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), supply parameter values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="d27e8-192">請參閱 `azuredeploy.json` 中的說明和其他參數的選項。</span><span class="sxs-lookup"><span data-stu-id="d27e8-192">See the descriptions in `azuredeploy.json` and options for other parameters.</span></span>  
 

5. <span data-ttu-id="d27e8-193">藉由下列命令傳遞部署參數檔，以建立 Container Service 叢集，其中︰</span><span class="sxs-lookup"><span data-stu-id="d27e8-193">Create a Container Service cluster by passing the deployment parameters file with the following command, where:</span></span>

    * <span data-ttu-id="d27e8-194">**RESOURCE_GROUP** 是您在上一個步驟中建立的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="d27e8-194">**RESOURCE_GROUP** is the name of the resource group that you created in the previous step.</span></span>
    * <span data-ttu-id="d27e8-195">**DEPLOYMENT_NAME** (選用) 是您提供的部署名稱。</span><span class="sxs-lookup"><span data-stu-id="d27e8-195">**DEPLOYMENT_NAME** (optional) is a name you give to the deployment.</span></span>
    * <span data-ttu-id="d27e8-196">**TEMPLATE_URI** 是部署檔案 `azuredeploy.json` 的位置。</span><span class="sxs-lookup"><span data-stu-id="d27e8-196">**TEMPLATE_URI** is the location of the deployment file `azuredeploy.json`.</span></span> <span data-ttu-id="d27e8-197">此 URI 必須是 Raw 檔案，而不是 GitHub UI 的指標。</span><span class="sxs-lookup"><span data-stu-id="d27e8-197">This URI must be the Raw file, not a pointer to the GitHub UI.</span></span> <span data-ttu-id="d27e8-198">若要尋找這個 URI，請在 GitHub 中選取 `azuredeploy.json` 檔案，然後按一下 [Raw] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d27e8-198">To find this URI, select the `azuredeploy.json` file in GitHub, and click the **Raw** button.</span></span>  

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters @azuredeploy.parameters.json
    ```

    <span data-ttu-id="d27e8-199">您也可以在命令列上以 JSON 格式字串提供參數。</span><span class="sxs-lookup"><span data-stu-id="d27e8-199">You can also provide parameters as a JSON-formatted string on the command line.</span></span> <span data-ttu-id="d27e8-200">使用類似下列的命令：</span><span class="sxs-lookup"><span data-stu-id="d27e8-200">Use a command similar to the following:</span></span>

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters "{ \"param1\": {\"value1\"} … }"
    ```

    > [!NOTE]
    > <span data-ttu-id="d27e8-201">部署需要數分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="d27e8-201">The deployment takes several minutes to complete.</span></span>
    > 

### <a name="equivalent-powershell-commands"></a><span data-ttu-id="d27e8-202">對等的 PowerShell 命令</span><span class="sxs-lookup"><span data-stu-id="d27e8-202">Equivalent PowerShell commands</span></span>
<span data-ttu-id="d27e8-203">您也可以使用 PowerShell 部署 Azure Container Service 叢集範本。</span><span class="sxs-lookup"><span data-stu-id="d27e8-203">You can also deploy an Azure Container Service cluster template with PowerShell.</span></span> <span data-ttu-id="d27e8-204">這份文件以 1.0 版的 [Azure PowerShell 模組](https://azure.microsoft.com/blog/azps-1-0/)為基礎。</span><span class="sxs-lookup"><span data-stu-id="d27e8-204">This document is based on the version 1.0 [Azure PowerShell module](https://azure.microsoft.com/blog/azps-1-0/).</span></span>

1. <span data-ttu-id="d27e8-205">若要部署 DC/OS、Docker Swarm 或 Kubernetes 叢集，請從 GitHub 選取其中一個可用的快速入門範本。</span><span class="sxs-lookup"><span data-stu-id="d27e8-205">To deploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of the available quickstart templates from GitHub.</span></span> <span data-ttu-id="d27e8-206">部分清單如下。</span><span class="sxs-lookup"><span data-stu-id="d27e8-206">A partial list follows.</span></span> <span data-ttu-id="d27e8-207">請注意，除了預設的 Orchestrator 選項有所不同外，DC/OS 和 Swarm 範本完全相同。</span><span class="sxs-lookup"><span data-stu-id="d27e8-207">Note that the DC/OS and Swarm templates are the same, with the exception of the default orchestrator selection.</span></span>

    * [<span data-ttu-id="d27e8-208">DC/OS 範本</span><span class="sxs-lookup"><span data-stu-id="d27e8-208">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="d27e8-209">Swarm 範本</span><span class="sxs-lookup"><span data-stu-id="d27e8-209">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="d27e8-210">Kubernetes 範本</span><span class="sxs-lookup"><span data-stu-id="d27e8-210">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="d27e8-211">在 Azure 訂用帳戶中建立叢集之前，請確認您的 PowerShell 工作階段已登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="d27e8-211">Before creating a cluster in your Azure subscription, verify that your PowerShell session has been signed in to Azure.</span></span> <span data-ttu-id="d27e8-212">您若要這麼做，可透過 `Get-AzureRMSubscription` 命令：</span><span class="sxs-lookup"><span data-stu-id="d27e8-212">You can do this with the `Get-AzureRMSubscription` command:</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="d27e8-213">如果您需要登入 Azure，請使用 `Login-AzureRMAccount` 命令：</span><span class="sxs-lookup"><span data-stu-id="d27e8-213">If you need to sign in to Azure, use the `Login-AzureRMAccount` command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

4. <span data-ttu-id="d27e8-214">最佳作法是使用新的資源群組進行部署。</span><span class="sxs-lookup"><span data-stu-id="d27e8-214">As a best practice, use a new resource group for the deployment.</span></span> <span data-ttu-id="d27e8-215">若要建立資源群組，請使用 `New-AzureRmResourceGroup` 命令，並指定資源群組名稱和目的地區域：</span><span class="sxs-lookup"><span data-stu-id="d27e8-215">To create a resource group, use the `New-AzureRmResourceGroup` command, and specify a resource group name and destination region:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name GROUP_NAME -Location REGION
    ```

5. <span data-ttu-id="d27e8-216">建立資源群組後，您就可以使用下列命令來建立叢集。</span><span class="sxs-lookup"><span data-stu-id="d27e8-216">After you create a resource group, you can create your cluster with the following command.</span></span> <span data-ttu-id="d27e8-217">使用 `-TemplateUri` 參數指定所需範本的 URI。</span><span class="sxs-lookup"><span data-stu-id="d27e8-217">The URI of the desired template is specified with the `-TemplateUri` parameter.</span></span> <span data-ttu-id="d27e8-218">當您執行此命令時，PowerShell 會提示您輸入部署參數值。</span><span class="sxs-lookup"><span data-stu-id="d27e8-218">When you run this command, PowerShell prompts you for deployment parameter values.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DEPLOYMENT_NAME -ResourceGroupName RESOURCE_GROUP_NAME -TemplateUri TEMPLATE_URI
    ```

#### <a name="provide-template-parameters"></a><span data-ttu-id="d27e8-219">提供範本參數</span><span class="sxs-lookup"><span data-stu-id="d27e8-219">Provide template parameters</span></span>
<span data-ttu-id="d27e8-220">如果您熟悉 PowerShell，您知道您可以輸入減號 (-) 然後按下 TAB 鍵，循環 Cmdlet 的可用參數。</span><span class="sxs-lookup"><span data-stu-id="d27e8-220">If you're familiar with PowerShell, you know that you can cycle through the available parameters for a cmdlet by typing a minus sign (-) and then pressing the TAB key.</span></span> <span data-ttu-id="d27e8-221">相同的功能也適用於您在範本中定義的參數。</span><span class="sxs-lookup"><span data-stu-id="d27e8-221">This same functionality also works with parameters that you define in your template.</span></span> <span data-ttu-id="d27e8-222">在您輸入範本名稱之後，Cmdlet 便會立即擷取範本、剖析參數，並將範本參數動態新增至命令。</span><span class="sxs-lookup"><span data-stu-id="d27e8-222">As soon as you type the template name, the cmdlet fetches the template, parses the parameters, and adds the template parameters to the command dynamically.</span></span> <span data-ttu-id="d27e8-223">這可讓您輕鬆指定範本參數值。</span><span class="sxs-lookup"><span data-stu-id="d27e8-223">This makes it easy to specify the template parameter values.</span></span> <span data-ttu-id="d27e8-224">另外，如果您忘記必要參數值，則 PowerShell 會出現此值的提示。</span><span class="sxs-lookup"><span data-stu-id="d27e8-224">And, if you forget a required parameter value, PowerShell prompts you for the value.</span></span>

<span data-ttu-id="d27e8-225">以下是包含參數的完整命令。</span><span class="sxs-lookup"><span data-stu-id="d27e8-225">Here is the full command, with parameters included.</span></span> <span data-ttu-id="d27e8-226">請對資源名稱提供您自己的值。</span><span class="sxs-lookup"><span data-stu-id="d27e8-226">Provide your own values for the names of the resources.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName RESOURCE_GROUP_NAME-TemplateURI TEMPLATE_URI -adminuser value1 -adminpassword value2 ....
```

## <a name="next-steps"></a><span data-ttu-id="d27e8-227">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d27e8-227">Next steps</span></span>
<span data-ttu-id="d27e8-228">既然您有一個可運作的叢集，請參閱這些文件來了解連接和管理的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="d27e8-228">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="d27e8-229">連接到 Azure Container Service 叢集</span><span class="sxs-lookup"><span data-stu-id="d27e8-229">Connect to an Azure Container Service cluster</span></span>](../container-service-connect.md)
* [<span data-ttu-id="d27e8-230">使用 Azure Container Service 和 DC/OS</span><span class="sxs-lookup"><span data-stu-id="d27e8-230">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="d27e8-231">使用 Azure Container Service 和 Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="d27e8-231">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="d27e8-232">使用 Azure Container Service 和 Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d27e8-232">Work with Azure Container Service and Kubernetes</span></span>](../kubernetes/container-service-kubernetes-walkthrough.md)
