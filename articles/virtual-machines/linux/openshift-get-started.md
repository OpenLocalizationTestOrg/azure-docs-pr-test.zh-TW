---
title: "aaaDeploy OpenShift 原點 tooAzure |Microsoft 文件"
description: "了解 toodeploy OpenShift 原點 tooAzure 虛擬機器。"
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
ms.openlocfilehash: a67450c46da41134a5f6c669a9e54e14773ac5b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a><span data-ttu-id="cb9a0-103">部署 OpenShift 原點 tooAzure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="cb9a0-103">Deploy OpenShift Origin tooAzure Virtual Machines</span></span> 

<span data-ttu-id="cb9a0-104">[OpenShift Origin](https://www.openshift.org/) 是建置在 [Kubernetes](https://kubernetes.io/) 上的開放原始碼容器平台。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-104">[OpenShift Origin](https://www.openshift.org/) is an open source container platform built on [Kubernetes](https://kubernetes.io/).</span></span> <span data-ttu-id="cb9a0-105">它可簡化部署、 調整和操作多租用戶應用程式的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-105">It simplifies hello process of deploying, scaling, and operating multi-tenant applications.</span></span> 

<span data-ttu-id="cb9a0-106">本指南說明如何在 Azure 虛擬機器使用 toodeploy OpenShift 原點 hello Azure CLI 和 Azure 資源管理員範本。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-106">This guide describes how toodeploy OpenShift Origin on Azure Virtual Machines using hello Azure CLI and Azure Resource Manager Templates.</span></span> <span data-ttu-id="cb9a0-107">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="cb9a0-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cb9a0-108">建立 KeyVault toomanage hello OpenShift 叢集的 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-108">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="cb9a0-109">部署 Azure VM 上的 OpenShift 叢集。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-109">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="cb9a0-110">安裝和設定 hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-110">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>
> * <span data-ttu-id="cb9a0-111">自訂 hello OpenShift 部署。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-111">Customize hello OpenShift deployment.</span></span>

<span data-ttu-id="cb9a0-112">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="cb9a0-113">本快速入門需要 hello Azure CLI 版本 2.0.8 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-113">This quick start requires hello Azure CLI version 2.0.8 or later.</span></span> <span data-ttu-id="cb9a0-114">toofind hello 版本，執行`az --version`。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-114">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="cb9a0-115">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="cb9a0-116">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="cb9a0-116">Log in tooAzure</span></span> 
<span data-ttu-id="cb9a0-117">登入 Azure 訂用帳戶以 hello tooyour [az 登入](/cli/azure/#login)命令並遵循螢幕上指示 hello 或按一下**試試**toouse 雲端殼層。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-117">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions or click **Try it** toouse Cloud Shell.</span></span>

```azurecli 
az login
```
## <a name="create-a-resource-group"></a><span data-ttu-id="cb9a0-118">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="cb9a0-118">Create a resource group</span></span>

<span data-ttu-id="cb9a0-119">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-119">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="cb9a0-120">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-120">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="cb9a0-121">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a><span data-ttu-id="cb9a0-122">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="cb9a0-122">Create a Key Vault</span></span>
<span data-ttu-id="cb9a0-123">建立 KeyVault toostore hello hello 叢集的 SSH 金鑰以 hello [az keyvault 建立](/cli/azure/keyvault#create)命令。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-123">Create a KeyVault toostore hello SSH keys for hello cluster with hello [az keyvault create](/cli/azure/keyvault#create) command.</span></span>  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a><span data-ttu-id="cb9a0-124">建立 SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="cb9a0-124">Create an SSH key</span></span> 
<span data-ttu-id="cb9a0-125">SSH 金鑰是需要的 toosecure 存取 toohello OpenShift 原點叢集。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-125">An SSH key is needed toosecure access toohello OpenShift Origin cluster.</span></span> <span data-ttu-id="cb9a0-126">建立 SSH 金鑰組使用 hello`ssh-keygen`命令。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-126">Create an SSH key-pair using hello `ssh-keygen` command.</span></span> 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> <span data-ttu-id="cb9a0-127">SSH 金鑰組建立 hello 絕不能有複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-127">hello SSH key pair you create must not have a passphrase.</span></span>

<span data-ttu-id="cb9a0-128">如需有關在 Windows 中，SSH 金鑰[toocreate SSH Windows 上的索引鍵](/azure/virtual-machines/linux/ssh-from-windows)。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-128">For more information on SSH keys on Windows, [How toocreate SSH keys on Windows](/azure/virtual-machines/linux/ssh-from-windows).</span></span>

## <a name="store-ssh-private-key-in-key-vault"></a><span data-ttu-id="cb9a0-129">將 SSH 私密金鑰儲存在 Key Vault 中</span><span class="sxs-lookup"><span data-stu-id="cb9a0-129">Store SSH private key in Key Vault</span></span>
<span data-ttu-id="cb9a0-130">hello OpenShift 部署會使用您建立 toosecure 存取 toohello OpenShift master hello SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-130">hello OpenShift deployment uses hello SSH key you created toosecure access toohello OpenShift master.</span></span> <span data-ttu-id="cb9a0-131">tooenable hello 部署 toosecurely 擷取 hello SSH 金鑰，請將 hello 金鑰儲存在金鑰保存庫使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-131">tooenable hello deployment toosecurely retrieve hello SSH key, store hello key in Key Vault using hello following command.</span></span>

# <a name="enabled-for-template-deployment"></a><span data-ttu-id="cb9a0-132">已針對範本部署啟用</span><span class="sxs-lookup"><span data-stu-id="cb9a0-132">Enabled for template deployment</span></span>
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a><span data-ttu-id="cb9a0-133">建立服務主體</span><span class="sxs-lookup"><span data-stu-id="cb9a0-133">Create a service principal</span></span> 
<span data-ttu-id="cb9a0-134">OpenShift 會使用使用者名稱與密碼或服務主體與 Azure 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-134">OpenShift communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="cb9a0-135">Azure 服務主體是安全性識別，可供您與應用程式、服務及諸如 OpenShift 等自動化工具搭配使用。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like OpenShift.</span></span> <span data-ttu-id="cb9a0-136">您可以控制和定義 hello 權限，如 toowhat 作業 hello 服務主體可以在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-136">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span> <span data-ttu-id="cb9a0-137">透過提供使用者名稱和密碼的 tooimprove 安全性，這個範例會建立基本的服務主體。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-137">tooimprove security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="cb9a0-138">建立服務主體與[az ad 預存程序建立-如-rbac](/cli/azure/ad/sp#create-for-rbac)和 OpenShift 需要輸出 hello 認證：</span><span class="sxs-lookup"><span data-stu-id="cb9a0-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that OpenShift needs:</span></span>

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
<span data-ttu-id="cb9a0-139">記下 hello hello 命令所傳回的 appId 屬性。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-139">Take note of hello appId property returned from hello command.</span></span>
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
 > <span data-ttu-id="cb9a0-140">請勿建立不安全的密碼。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-140">Don't create an insecure password.</span></span>  <span data-ttu-id="cb9a0-141">請依照 [Azure AD 密碼規則和限制](/azure/active-directory/active-directory-passwords-policy)指引。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-141">Follow the [Azure AD password rules and restrictions](/azure/active-directory/active-directory-passwords-policy) guidance.</span></span>

<span data-ttu-id="cb9a0-142">如需有關服務主體的詳細資訊，請參閱[使用 Azure CLI 2.0 建立 Azure 服務主體](/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="cb9a0-142">For more information on service principals, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

## <a name="deploy-hello-openshift-origin-template"></a><span data-ttu-id="cb9a0-143">部署 hello OpenShift 原始範本</span><span class="sxs-lookup"><span data-stu-id="cb9a0-143">Deploy hello OpenShift Origin template</span></span>
<span data-ttu-id="cb9a0-144">接下來，使用 Azure Resource Manager 範本來部署 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-144">Next deploy OpenShift Origin using an Azure Resource Manager template.</span></span> 

> [!NOTE] 
> <span data-ttu-id="cb9a0-145">hello 下列命令需要 az CLI 2.0.8 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-145">hello following command requires az CLI 2.0.8 or later.</span></span> <span data-ttu-id="cb9a0-146">您可以確認 hello az CLI 版本與 hello`az --version`命令。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-146">You can verify hello az CLI version with hello `az --version` command.</span></span> <span data-ttu-id="cb9a0-147">tooupdate hello CLI 版本，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-147">tooupdate hello CLI version, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="cb9a0-148">使用 hello`appId`值從您稍早建立的 hello hello 服務主體`aadClientId`參數。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-148">Use hello `appId` value from hello service principal you created earlier for hello `aadClientId` parameter.</span></span>

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
<span data-ttu-id="cb9a0-149">hello 部署可能會佔用 too20 分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-149">hello deployment may take up too20 minutes toocomplete.</span></span> <span data-ttu-id="cb9a0-150">hello hello OpenShift 主控台的 URL 和 DNS 名稱的 hello OpenShift 主要被列印 toohello 終端機 hello 部署完成時。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-150">hello URL of hello OpenShift console and DNS name of hello OpenShift master is printed toohello terminal when hello deployment completes.</span></span>

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a><span data-ttu-id="cb9a0-151">Toohello OpenShift 叢集連線</span><span class="sxs-lookup"><span data-stu-id="cb9a0-151">Connect toohello OpenShift cluster</span></span>
<span data-ttu-id="cb9a0-152">Hello 部署完成時，將使用 hello 瀏覽器使用 hello toohello OpenShift 主控台連線`OpenShift Console Uri`。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-152">When hello deployment completes, connect toohello OpenShift console using hello browser using hello `OpenShift Console Uri`.</span></span> <span data-ttu-id="cb9a0-153">或者，您可以連線使用下列命令的 hello toohello OpenShift master。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-153">Alternatively, you can connect toohello OpenShift master using hello following command.</span></span>

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a><span data-ttu-id="cb9a0-154">清除資源</span><span class="sxs-lookup"><span data-stu-id="cb9a0-154">Clean up resources</span></span>
<span data-ttu-id="cb9a0-155">當不再需要您可以使用 hello [az 群組刪除](/cli/azure/group#delete)命令 tooremove hello 資源群組、 OpenShift 叢集，以及所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-155">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, OpenShift cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="cb9a0-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cb9a0-156">Next steps</span></span>

<span data-ttu-id="cb9a0-157">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="cb9a0-157">In this tutorial, learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="cb9a0-158">建立 KeyVault toomanage hello OpenShift 叢集的 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-158">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="cb9a0-159">部署 Azure VM 上的 OpenShift 叢集。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-159">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="cb9a0-160">安裝和設定 hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-160">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>

<span data-ttu-id="cb9a0-161">現在您已部署 OpenShift Origin 叢集。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-161">Now that OpenShift Origin cluster is deployed.</span></span> <span data-ttu-id="cb9a0-162">您可以如何依照 OpenShift 教學課程 toolearn toodeploy 第一個應用程式和使用 hello OpenShift 工具。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-162">You can follow OpenShift tutorials toolearn how toodeploy your first application and use hello OpenShift tools.</span></span> <span data-ttu-id="cb9a0-163">請參閱[入門 OpenShift 原點](https://docs.openshift.org/latest/getting_started/index.html)tooget 啟動。</span><span class="sxs-lookup"><span data-stu-id="cb9a0-163">See [Getting Started with OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html) tooget started.</span></span> 
