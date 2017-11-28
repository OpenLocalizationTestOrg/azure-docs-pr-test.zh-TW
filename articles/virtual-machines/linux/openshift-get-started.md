---
title: "將 OpenShift Origin 部署至 Azure | Microsoft Docs"
description: "了解如何將 OpenShift Origin 部署至 Azure 虛擬機器。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jbinder
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 
ms.author: jbinder
ms.openlocfilehash: e03da05625e440eab29ccc28a2343d3433fc7607
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-openshift-origin-to-azure-virtual-machines"></a><span data-ttu-id="acbf6-103">將 OpenShift Origin 部署至 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="acbf6-103">Deploy OpenShift Origin to Azure Virtual Machines</span></span> 

<span data-ttu-id="acbf6-104">[OpenShift Origin](https://www.openshift.org/) 是建置在 [Kubernetes](https://kubernetes.io/) 上的開放原始碼容器平台。</span><span class="sxs-lookup"><span data-stu-id="acbf6-104">[OpenShift Origin](https://www.openshift.org/) is an open source container platform built on [Kubernetes](https://kubernetes.io/).</span></span> <span data-ttu-id="acbf6-105">它可簡化部署、調整及操作多租用戶應用程式的程序。</span><span class="sxs-lookup"><span data-stu-id="acbf6-105">It simplifies the process of deploying, scaling, and operating multi-tenant applications.</span></span> 

<span data-ttu-id="acbf6-106">本指南說明如何使用 Azure CLI 和 Azure Resource Manager 範本在 Azure 虛擬機器上部署 OpenShift Origin。</span><span class="sxs-lookup"><span data-stu-id="acbf6-106">This guide describes how to deploy OpenShift Origin on Azure Virtual Machines using the Azure CLI and Azure Resource Manager Templates.</span></span> <span data-ttu-id="acbf6-107">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="acbf6-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="acbf6-108">建立 KeyVault 來管理 OpenShift 叢集的 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="acbf6-108">Create a KeyVault to manage SSH keys for the OpenShift cluster.</span></span>
> * <span data-ttu-id="acbf6-109">部署 Azure VM 上的 OpenShift 叢集。</span><span class="sxs-lookup"><span data-stu-id="acbf6-109">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="acbf6-110">安裝和設定 [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) 來管理叢集。</span><span class="sxs-lookup"><span data-stu-id="acbf6-110">Install and configure the [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) to manage the cluster.</span></span>
> * <span data-ttu-id="acbf6-111">自訂 OpenShift 部署。</span><span class="sxs-lookup"><span data-stu-id="acbf6-111">Customize the OpenShift deployment.</span></span>

<span data-ttu-id="acbf6-112">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="acbf6-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="acbf6-113">本快速入門需要 Azure CLI 2.0.8 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="acbf6-113">This quick start requires the Azure CLI version 2.0.8 or later.</span></span> <span data-ttu-id="acbf6-114">若要尋找版本，請執行 `az --version`。</span><span class="sxs-lookup"><span data-stu-id="acbf6-114">To find the version, run `az --version`.</span></span> <span data-ttu-id="acbf6-115">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="acbf6-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-to-azure"></a><span data-ttu-id="acbf6-116">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="acbf6-116">Log in to Azure</span></span> 
<span data-ttu-id="acbf6-117">使用 [az login](/cli/azure/#login) 命令來登入 Azure 訂用帳戶並遵循畫面上的指示進行，或按一下 [試用] 來使用 Cloud Shell。</span><span class="sxs-lookup"><span data-stu-id="acbf6-117">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions or click **Try it** to use Cloud Shell.</span></span>

```azurecli 
az login
```
## <a name="create-a-resource-group"></a><span data-ttu-id="acbf6-118">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="acbf6-118">Create a resource group</span></span>

<span data-ttu-id="acbf6-119">使用 [az group create](/cli/azure/group#create) 命令來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="acbf6-119">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="acbf6-120">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="acbf6-120">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="acbf6-121">下列範例會在 eastus 位置建立名為 myResourceGroup 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="acbf6-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a><span data-ttu-id="acbf6-122">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="acbf6-122">Create a Key Vault</span></span>
<span data-ttu-id="acbf6-123">使用 [az keyvault create](/cli/azure/keyvault#create) 命令來建立要儲存叢集之 SSH 金鑰的 KeyVault。</span><span class="sxs-lookup"><span data-stu-id="acbf6-123">Create a KeyVault to store the SSH keys for the cluster with the [az keyvault create](/cli/azure/keyvault#create) command.</span></span>  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a><span data-ttu-id="acbf6-124">建立 SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="acbf6-124">Create an SSH key</span></span> 
<span data-ttu-id="acbf6-125">需要 SSH 金鑰才能安全存取 OpenShift Origin 叢集。</span><span class="sxs-lookup"><span data-stu-id="acbf6-125">An SSH key is needed to secure access to the OpenShift Origin cluster.</span></span> <span data-ttu-id="acbf6-126">使用 `ssh-keygen` 命令建立 SSH 金鑰組。</span><span class="sxs-lookup"><span data-stu-id="acbf6-126">Create an SSH key-pair using the `ssh-keygen` command.</span></span> 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> <span data-ttu-id="acbf6-127">您所建立的 SSH 金鑰組不能使用複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="acbf6-127">The SSH key pair you create must not have a passphrase.</span></span>

<span data-ttu-id="acbf6-128">如需有關 Windows 上的 SSH 金鑰詳細資訊，請參閱[如何在 Windows 上建立 SSH 金鑰](/azure/virtual-machines/linux/ssh-from-windows)。</span><span class="sxs-lookup"><span data-stu-id="acbf6-128">For more information on SSH keys on Windows, [How to create SSH keys on Windows](/azure/virtual-machines/linux/ssh-from-windows).</span></span>

## <a name="store-ssh-private-key-in-key-vault"></a><span data-ttu-id="acbf6-129">將 SSH 私密金鑰儲存在 Key Vault 中</span><span class="sxs-lookup"><span data-stu-id="acbf6-129">Store SSH private key in Key Vault</span></span>
<span data-ttu-id="acbf6-130">OpenShift 部署會使用您建立的 SSH 金鑰來安全存取 OpenShift 主機。</span><span class="sxs-lookup"><span data-stu-id="acbf6-130">The OpenShift deployment uses the SSH key you created to secure access to the OpenShift master.</span></span> <span data-ttu-id="acbf6-131">若要啟用部署以安全地擷取 SSH 金鑰，請使用下列命令將金鑰儲存在 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="acbf6-131">To enable the deployment to securely retrieve the SSH key, store the key in Key Vault using the following command.</span></span>

# <a name="enabled-for-template-deployment"></a><span data-ttu-id="acbf6-132">已針對範本部署啟用</span><span class="sxs-lookup"><span data-stu-id="acbf6-132">Enabled for template deployment</span></span>
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a><span data-ttu-id="acbf6-133">建立服務主體</span><span class="sxs-lookup"><span data-stu-id="acbf6-133">Create a service principal</span></span> 
<span data-ttu-id="acbf6-134">OpenShift 會使用使用者名稱與密碼或服務主體與 Azure 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="acbf6-134">OpenShift communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="acbf6-135">Azure 服務主體是安全性識別，可供您與應用程式、服務及諸如 OpenShift 等自動化工具搭配使用。</span><span class="sxs-lookup"><span data-stu-id="acbf6-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like OpenShift.</span></span> <span data-ttu-id="acbf6-136">您可以控制和定義對於服務主體可以在 Azure 中執行哪些作業的權限。</span><span class="sxs-lookup"><span data-stu-id="acbf6-136">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span> <span data-ttu-id="acbf6-137">為了提高只提供使用者名稱和密碼的安全性，此範例會建立基本的服務主體。</span><span class="sxs-lookup"><span data-stu-id="acbf6-137">To improve security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="acbf6-138">使用 [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) 建立服務主體，並將 OpenShift 所需的認證輸出：</span><span class="sxs-lookup"><span data-stu-id="acbf6-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output the credentials that OpenShift needs:</span></span>

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
<span data-ttu-id="acbf6-139">記下命令傳回的 appId 屬性。</span><span class="sxs-lookup"><span data-stu-id="acbf6-139">Take note of the appId property returned from the command.</span></span>
```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "openshiftsp",
  "name": "http://openshiftsp",
  "password": {strong password},
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```
 > [!WARNING] 
 > <span data-ttu-id="acbf6-140">請勿建立不安全的密碼。</span><span class="sxs-lookup"><span data-stu-id="acbf6-140">Don't create an insecure password.</span></span>  <span data-ttu-id="acbf6-141">請依照 [Azure AD 密碼規則和限制](/azure/active-directory/active-directory-passwords-policy)指引。</span><span class="sxs-lookup"><span data-stu-id="acbf6-141">Follow the [Azure AD password rules and restrictions](/azure/active-directory/active-directory-passwords-policy) guidance.</span></span>

<span data-ttu-id="acbf6-142">如需有關服務主體的詳細資訊，請參閱[使用 Azure CLI 2.0 建立 Azure 服務主體](/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="acbf6-142">For more information on service principals, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

## <a name="deploy-the-openshift-origin-template"></a><span data-ttu-id="acbf6-143">部署 OpenShift Origin 範本</span><span class="sxs-lookup"><span data-stu-id="acbf6-143">Deploy the OpenShift Origin template</span></span>
<span data-ttu-id="acbf6-144">接下來，使用 Azure Resource Manager 範本來部署 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="acbf6-144">Next deploy OpenShift Origin using an Azure Resource Manager template.</span></span> 

> [!NOTE] 
> <span data-ttu-id="acbf6-145">下列命令需要 az CLI 2.0.8 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="acbf6-145">The following command requires az CLI 2.0.8 or later.</span></span> <span data-ttu-id="acbf6-146">您可以使用 `az --version` 命令來確認 az CLI 版本。</span><span class="sxs-lookup"><span data-stu-id="acbf6-146">You can verify the az CLI version with the `az --version` command.</span></span> <span data-ttu-id="acbf6-147">若要更新 CLI 版本，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="acbf6-147">To update the CLI version, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="acbf6-148">使用您稍早針對 `aadClientId` 參數所建立之服務主體中的 `appId` 值。</span><span class="sxs-lookup"><span data-stu-id="acbf6-148">Use the `appId` value from the service principal you created earlier for the `aadClientId` parameter.</span></span>

```azurecli 
az group deployment create --name myOpenShiftCluster \
      --template-uri https://raw.githubusercontent.com/Microsoft/openshift-origin/master/azuredeploy.json \
      --params \ 
        openshiftMasterPublicIpDnsLabel=myopenshiftmaster \
        infraLbPublicIpDnsLabel=myopenshiftlb \
        openshiftPassword=Pass@word!
        sshPublicKey=~/.ssh/openshift_rsa.pub \
        keyVaultResourceGroup=myResourceGroup \
        keyVaultName=myKeyVault \
        keyVaultSecret=OpenShiftKey \
        aadClientId={appId} \
        aadClientSecret={strong password} 
```
<span data-ttu-id="acbf6-149">完成部署最多可能需要大約 20 分鐘或更久的時間。</span><span class="sxs-lookup"><span data-stu-id="acbf6-149">The deployment may take up to 20 minutes to complete.</span></span> <span data-ttu-id="acbf6-150">當部署完成時，OpenShift 主控台的 URL 和 OpenShift 主機的 DNS 名稱會列印到終端機。</span><span class="sxs-lookup"><span data-stu-id="acbf6-150">The URL of the OpenShift console and DNS name of the OpenShift master is printed to the terminal when the deployment completes.</span></span>

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-to-the-openshift-cluster"></a><span data-ttu-id="acbf6-151">連線到 OpenShift 叢集</span><span class="sxs-lookup"><span data-stu-id="acbf6-151">Connect to the OpenShift cluster</span></span>
<span data-ttu-id="acbf6-152">部署完成時，使用 `OpenShift Console Uri` 可透過瀏覽器連線至 OpenShift 主控台。</span><span class="sxs-lookup"><span data-stu-id="acbf6-152">When the deployment completes, connect to the OpenShift console using the browser using the `OpenShift Console Uri`.</span></span> <span data-ttu-id="acbf6-153">或者，您也可以使用下列命令連線至 OpenShift 主機。</span><span class="sxs-lookup"><span data-stu-id="acbf6-153">Alternatively, you can connect to the OpenShift master using the following command.</span></span>

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a><span data-ttu-id="acbf6-154">清除資源</span><span class="sxs-lookup"><span data-stu-id="acbf6-154">Clean up resources</span></span>
<span data-ttu-id="acbf6-155">若不再需要，您可以使用 [az group delete](/cli/azure/group#delete) 命令將資源群組、OpenShift 叢集和所有相關資源移除。</span><span class="sxs-lookup"><span data-stu-id="acbf6-155">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, OpenShift cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="acbf6-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="acbf6-156">Next steps</span></span>

<span data-ttu-id="acbf6-157">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="acbf6-157">In this tutorial, learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="acbf6-158">建立 KeyVault 來管理 OpenShift 叢集的 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="acbf6-158">Create a KeyVault to manage SSH keys for the OpenShift cluster.</span></span>
> * <span data-ttu-id="acbf6-159">部署 Azure VM 上的 OpenShift 叢集。</span><span class="sxs-lookup"><span data-stu-id="acbf6-159">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="acbf6-160">安裝和設定 [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) 來管理叢集。</span><span class="sxs-lookup"><span data-stu-id="acbf6-160">Install and configure the [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) to manage the cluster.</span></span>

<span data-ttu-id="acbf6-161">現在您已部署 OpenShift Origin 叢集。</span><span class="sxs-lookup"><span data-stu-id="acbf6-161">Now that OpenShift Origin cluster is deployed.</span></span> <span data-ttu-id="acbf6-162">您可以遵循 OpenShift 教學課程，了解如何部署第一個應用程式，以及如何使用 OpenShift 工具。</span><span class="sxs-lookup"><span data-stu-id="acbf6-162">You can follow OpenShift tutorials to learn how to deploy your first application and use the OpenShift tools.</span></span> <span data-ttu-id="acbf6-163">若要開始使用，請參閱[開始使用 OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html)。</span><span class="sxs-lookup"><span data-stu-id="acbf6-163">See [Getting Started with OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html) to get started.</span></span> 
