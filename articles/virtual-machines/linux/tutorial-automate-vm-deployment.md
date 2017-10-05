---
title: "在 Azure 中初次開機時自訂 Linux VM | Microsoft Docs"
description: "了解如何使用 cloud-init 和 Key Vault，以便在 Linux VM 初次於 Azure 中開機時加以自訂"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 6adf4e43aa80c28c6f5f8d8a071966323ba85723
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-customize-a-linux-virtual-machine-on-first-boot"></a><span data-ttu-id="aa019-103">如何在初次開機時自訂 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="aa019-103">How to customize a Linux virtual machine on first boot</span></span>
<span data-ttu-id="aa019-104">在先前的教學課程中，您學到了如何以 SSH 連線到虛擬機器 (VM) 並手動安裝 NGINX。</span><span class="sxs-lookup"><span data-stu-id="aa019-104">In a previous tutorial, you learned how to SSH to a virtual machine (VM) and manually install NGINX.</span></span> <span data-ttu-id="aa019-105">若要以快速且一致的方式建立 VM，您通常需要借助某種形式的自動化。</span><span class="sxs-lookup"><span data-stu-id="aa019-105">To create VMs in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="aa019-106">在初次開機時自訂 VM 的常見方法是使用 [cloud-init (英文)](https://cloudinit.readthedocs.io)。</span><span class="sxs-lookup"><span data-stu-id="aa019-106">A common approach to customize a VM on first boot is to use [cloud-init](https://cloudinit.readthedocs.io).</span></span> <span data-ttu-id="aa019-107">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="aa019-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aa019-108">建立 Cloud-init 組態檔</span><span class="sxs-lookup"><span data-stu-id="aa019-108">Create a cloud-init config file</span></span>
> * <span data-ttu-id="aa019-109">建立 VM 來使用 Cloud-init 檔案</span><span class="sxs-lookup"><span data-stu-id="aa019-109">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="aa019-110">在建立 VM 之後，檢視執行中的 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="aa019-110">View a running Node.js app after the VM is created</span></span>
> * <span data-ttu-id="aa019-111">使用 Key Vault 安全地儲存憑證</span><span class="sxs-lookup"><span data-stu-id="aa019-111">Use Key Vault to securely store certificates</span></span>
> * <span data-ttu-id="aa019-112">使用 Cloud-init 來安全地自動部署 NGINX</span><span class="sxs-lookup"><span data-stu-id="aa019-112">Automate secure deployments of NGINX with cloud-init</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="aa019-113">如果您選擇在本機安裝和使用 CLI，本教學課程會要求您執行 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="aa019-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="aa019-114">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="aa019-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="aa019-115">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="aa019-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  



## <a name="cloud-init-overview"></a><span data-ttu-id="aa019-116">Cloud-Init 概觀</span><span class="sxs-lookup"><span data-stu-id="aa019-116">Cloud-init overview</span></span>
<span data-ttu-id="aa019-117">[Cloud-init (英文)](https://cloudinit.readthedocs.io) 是在 Linux VM 初次開機時，廣泛用來自訂它們的方法。</span><span class="sxs-lookup"><span data-stu-id="aa019-117">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach to customize a Linux VM as it boots for the first time.</span></span> <span data-ttu-id="aa019-118">您可以使用 cloud-init 來安裝封裝和寫入檔案，或者設定使用者和安全性。</span><span class="sxs-lookup"><span data-stu-id="aa019-118">You can use cloud-init to install packages and write files, or to configure users and security.</span></span> <span data-ttu-id="aa019-119">當 cloud-init 在初次開機程序期間執行時，不需要使用任何額外的步驟或必要的代理程式來套用您的組態。</span><span class="sxs-lookup"><span data-stu-id="aa019-119">As cloud-init runs during the initial boot process, there are no additional steps or required agents to apply your configuration.</span></span>

<span data-ttu-id="aa019-120">Cloud-init 也適用於散發套件。</span><span class="sxs-lookup"><span data-stu-id="aa019-120">Cloud-init also works across distributions.</span></span> <span data-ttu-id="aa019-121">例如，您不使用 **apt-get install** 或 **yum install** 來安裝套件。</span><span class="sxs-lookup"><span data-stu-id="aa019-121">For example, you don't use **apt-get install** or **yum install** to install a package.</span></span> <span data-ttu-id="aa019-122">您可以改為定義要安裝的套件清單。</span><span class="sxs-lookup"><span data-stu-id="aa019-122">Instead you can define a list of packages to install.</span></span> <span data-ttu-id="aa019-123">Cloud-init 會針對您選取的散發套件自動使用原生的套件管理工具。</span><span class="sxs-lookup"><span data-stu-id="aa019-123">Cloud-init automatically uses the native package management tool for the distro you select.</span></span>

<span data-ttu-id="aa019-124">我們正在與合作夥伴合作，以期在他們提供給 Azure 的映像中包含和使用 cloud-init。</span><span class="sxs-lookup"><span data-stu-id="aa019-124">We are working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span> <span data-ttu-id="aa019-125">下表概述 cloud-init 目前在 Azure 平台映像上的可用性：</span><span class="sxs-lookup"><span data-stu-id="aa019-125">The following table outlines the current cloud-init availability on Azure platform images:</span></span>

| <span data-ttu-id="aa019-126">Alias</span><span class="sxs-lookup"><span data-stu-id="aa019-126">Alias</span></span> | <span data-ttu-id="aa019-127">發佈者</span><span class="sxs-lookup"><span data-stu-id="aa019-127">Publisher</span></span> | <span data-ttu-id="aa019-128">提供項目</span><span class="sxs-lookup"><span data-stu-id="aa019-128">Offer</span></span> | <span data-ttu-id="aa019-129">SKU</span><span class="sxs-lookup"><span data-stu-id="aa019-129">SKU</span></span> | <span data-ttu-id="aa019-130">版本</span><span class="sxs-lookup"><span data-stu-id="aa019-130">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="aa019-131">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="aa019-131">UbuntuLTS</span></span> |<span data-ttu-id="aa019-132">Canonical</span><span class="sxs-lookup"><span data-stu-id="aa019-132">Canonical</span></span> |<span data-ttu-id="aa019-133">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="aa019-133">UbuntuServer</span></span> |<span data-ttu-id="aa019-134">16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="aa019-134">16.04-LTS</span></span> |<span data-ttu-id="aa019-135">最新</span><span class="sxs-lookup"><span data-stu-id="aa019-135">latest</span></span> |
| <span data-ttu-id="aa019-136">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="aa019-136">UbuntuLTS</span></span> |<span data-ttu-id="aa019-137">Canonical</span><span class="sxs-lookup"><span data-stu-id="aa019-137">Canonical</span></span> |<span data-ttu-id="aa019-138">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="aa019-138">UbuntuServer</span></span> |<span data-ttu-id="aa019-139">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="aa019-139">14.04.5-LTS</span></span> |<span data-ttu-id="aa019-140">最新</span><span class="sxs-lookup"><span data-stu-id="aa019-140">latest</span></span> |
| <span data-ttu-id="aa019-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="aa019-141">CoreOS</span></span> |<span data-ttu-id="aa019-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="aa019-142">CoreOS</span></span> |<span data-ttu-id="aa019-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="aa019-143">CoreOS</span></span> |<span data-ttu-id="aa019-144">Stable</span><span class="sxs-lookup"><span data-stu-id="aa019-144">Stable</span></span> |<span data-ttu-id="aa019-145">最新</span><span class="sxs-lookup"><span data-stu-id="aa019-145">latest</span></span> |


## <a name="create-cloud-init-config-file"></a><span data-ttu-id="aa019-146">建立 Cloud-init 組態檔</span><span class="sxs-lookup"><span data-stu-id="aa019-146">Create cloud-init config file</span></span>
<span data-ttu-id="aa019-147">若要查看作用中的 cloud-init，請建立 VM 來安裝 NGINX 並執行簡單 'Hello World' Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa019-147">To see cloud-init in action, create a VM that installs NGINX and runs a simple 'Hello World' Node.js app.</span></span> <span data-ttu-id="aa019-148">下列 cloud-init 組態會安裝必要的封裝、建立 Node.js 應用程式，然後初始化並啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa019-148">The following cloud-init configuration installs the required packages, creates a Node.js app, then initialize and starts the app.</span></span>

<span data-ttu-id="aa019-149">您目前的殼層中，建立名為 cloud-init.txt 的檔案，並貼上下列組態。</span><span class="sxs-lookup"><span data-stu-id="aa019-149">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="aa019-150">例如，在 Cloud Shell 中建立不在本機電腦上的檔案。</span><span class="sxs-lookup"><span data-stu-id="aa019-150">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="aa019-151">您可以使用任何您想要的編輯器。</span><span class="sxs-lookup"><span data-stu-id="aa019-151">You can use any editor you wish.</span></span> <span data-ttu-id="aa019-152">輸入 `sensible-editor cloud-init.txt` 可建立檔案，並查看可用的編輯器清單。</span><span class="sxs-lookup"><span data-stu-id="aa019-152">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="aa019-153">請確定已正確複製整個 cloud-init 檔案，特別是第一行：</span><span class="sxs-lookup"><span data-stu-id="aa019-153">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

<span data-ttu-id="aa019-154">如需 Cloud-init 組態選項的詳細資訊，請參閱 [Cloud-init 組態範例](https://cloudinit.readthedocs.io/en/latest/topics/examples.html) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="aa019-154">For more information about cloud-init configuration options, see [cloud-init config examples](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="aa019-155">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="aa019-155">Create virtual machine</span></span>
<span data-ttu-id="aa019-156">建立 VM 之前，請先使用 [az group create](/cli/azure/group#create) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="aa019-156">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="aa019-157">下列範例會在 eastus 位置建立名為 myResourceGroupAutomate 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="aa019-157">The following example creates a resource group named *myResourceGroupAutomate* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

<span data-ttu-id="aa019-158">現在，使用 [az vm create](/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="aa019-158">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="aa019-159">使用 `--custom-data` 參數以傳入 cloud-init 組態檔。</span><span class="sxs-lookup"><span data-stu-id="aa019-159">Use the `--custom-data` parameter to pass in your cloud-init config file.</span></span> <span data-ttu-id="aa019-160">如果您將檔案儲存於目前工作目錄之外的位置，請提供 cloud-init.txt 組態的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="aa019-160">Provide the full path to the *cloud-init.txt* config if you saved the file outside of your present working directory.</span></span> <span data-ttu-id="aa019-161">下列範例會建立名為 myAutomatedVM 的 VM：</span><span class="sxs-lookup"><span data-stu-id="aa019-161">The following example creates a VM named *myAutomatedVM*:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="aa019-162">系統需要花幾分鐘的時間來建立 VM、安裝封裝和啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa019-162">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="aa019-163">在 Azure CLI 將您返回提示字元之後，背景工作會繼續執行。</span><span class="sxs-lookup"><span data-stu-id="aa019-163">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="aa019-164">可能需要再等候幾分鐘，才能存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa019-164">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="aa019-165">建立 VM 之後，請注意 Azure CLI 所顯示的 `publicIpAddress`。</span><span class="sxs-lookup"><span data-stu-id="aa019-165">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="aa019-166">此位址是用來透過 Web 瀏覽器存取 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa019-166">This address is used to access the Node.js app via a web browser.</span></span>

<span data-ttu-id="aa019-167">若要讓 Web 流量到達您的 VM，請使用 [az vm open-port](/cli/azure/vm#open-port) 從網際網路開啟通訊埠 80：</span><span class="sxs-lookup"><span data-stu-id="aa019-167">To allow web traffic to reach your VM, open port 80 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a><span data-ttu-id="aa019-168">測試 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="aa019-168">Test web app</span></span>
<span data-ttu-id="aa019-169">現在，您可以開啟 Web 瀏覽器，並在網址列輸入 *http://<publicIpAddress>*。</span><span class="sxs-lookup"><span data-stu-id="aa019-169">Now you can open a web browser and enter *http://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="aa019-170">提供您自己從 VM 建立程序中取得的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="aa019-170">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="aa019-171">您的 Node.js 應用程式即會顯示，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="aa019-171">Your Node.js app is displayed as in the following example:</span></span>

![檢視執行中的 NGINX 網站](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a><span data-ttu-id="aa019-173">從 Key Vault 插入憑證</span><span class="sxs-lookup"><span data-stu-id="aa019-173">Inject certificates from Key Vault</span></span>
<span data-ttu-id="aa019-174">您可以選擇性閱讀這一節，其中示範如何安全地將憑證儲存在 Azure Key Vault 中，並在 VM 部署期間插入它們。</span><span class="sxs-lookup"><span data-stu-id="aa019-174">This optional section shows how you can securely store certificates in Azure Key Vault and inject them during the VM deployment.</span></span> <span data-ttu-id="aa019-175">不需使用包含憑證的自訂映像內建中，此程序可確保會在初次開機時將最新憑證插入至 VM。</span><span class="sxs-lookup"><span data-stu-id="aa019-175">Rather than using a custom image that includes the certificates baked-in, this process ensures that the most up-to-date certificates are injected to a VM on first boot.</span></span> <span data-ttu-id="aa019-176">過程中，憑證絕對不會離開 Azure 平台，或在指令碼、命令列記錄或範本中公開。</span><span class="sxs-lookup"><span data-stu-id="aa019-176">During the process, the certificate never leaves the Azure platform or is exposed in a script, command-line history, or template.</span></span>

<span data-ttu-id="aa019-177">Azure Key Vault 會保護密碼編譯金鑰和祕密，像是憑證或密碼。</span><span class="sxs-lookup"><span data-stu-id="aa019-177">Azure Key Vault safeguards cryptographic keys and secrets, such as certificates or passwords.</span></span> <span data-ttu-id="aa019-178">Key Vault 有助於簡化金鑰管理程序，並可讓您控管存取和加密資料的金鑰。</span><span class="sxs-lookup"><span data-stu-id="aa019-178">Key Vault helps streamline the key management process and enables you to maintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="aa019-179">此案例會引進一些 Key Vault 概念來建立和使用憑證，但並不是如何使用 Key Vault 的詳盡概觀。</span><span class="sxs-lookup"><span data-stu-id="aa019-179">This scenario introduces some Key Vault concepts to create and use a certificate, though is not an exhaustive overview on how to use Key Vault.</span></span>

<span data-ttu-id="aa019-180">下列步驟將示範如何：</span><span class="sxs-lookup"><span data-stu-id="aa019-180">The following steps show how you can:</span></span>

- <span data-ttu-id="aa019-181">建立 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="aa019-181">Create an Azure Key Vault</span></span>
- <span data-ttu-id="aa019-182">產生或上傳憑證至 Key Vault</span><span class="sxs-lookup"><span data-stu-id="aa019-182">Generate or upload a certificate to the Key Vault</span></span>
- <span data-ttu-id="aa019-183">從憑證建立祕密以插入至 VM</span><span class="sxs-lookup"><span data-stu-id="aa019-183">Create a secret from the certificate to inject in to a VM</span></span>
- <span data-ttu-id="aa019-184">建立 VM 並插入憑證</span><span class="sxs-lookup"><span data-stu-id="aa019-184">Create a VM and inject the certificate</span></span>

### <a name="create-an-azure-key-vault"></a><span data-ttu-id="aa019-185">建立 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="aa019-185">Create an Azure Key Vault</span></span>
<span data-ttu-id="aa019-186">首先，使用 [az keyvault create](/cli/azure/keyvault#create) 建立 Key Vault，並加以啟用以供您在部署 VM 時使用。</span><span class="sxs-lookup"><span data-stu-id="aa019-186">First, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="aa019-187">每個 Key Vault 需要唯一的名稱，而且應該全部小寫。</span><span class="sxs-lookup"><span data-stu-id="aa019-187">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="aa019-188">使用您自己唯一的 Key Vault 名稱來取代下列範例中的 mykeyvault：</span><span class="sxs-lookup"><span data-stu-id="aa019-188">Replace *mykeyvault* in the following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a><span data-ttu-id="aa019-189">產生憑證並儲存於 Key Vault</span><span class="sxs-lookup"><span data-stu-id="aa019-189">Generate certificate and store in Key Vault</span></span>
<span data-ttu-id="aa019-190">若要在生產環境中使用，您應該使用 [az keyvault certificate import](/cli/azure/keyvault/certificate#import) 來匯入由受信任的提供者所簽署的有效憑證。</span><span class="sxs-lookup"><span data-stu-id="aa019-190">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span></span> <span data-ttu-id="aa019-191">在本教學課程中，下列範例示範如何透過使用預設憑證原則的 [az keyvault certificate create](/cli/azure/keyvault/certificate#create) 來產生自我簽署憑證：</span><span class="sxs-lookup"><span data-stu-id="aa019-191">For this tutorial, the following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/keyvault/certificate#create) that uses the default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a><span data-ttu-id="aa019-192">準備要與 VM 搭配使用的憑證</span><span class="sxs-lookup"><span data-stu-id="aa019-192">Prepare certificate for use with VM</span></span>
<span data-ttu-id="aa019-193">若要在 VM 建立程序期間使用憑證，使用 [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions) 來取得憑證的識別碼。</span><span class="sxs-lookup"><span data-stu-id="aa019-193">To use the certificate during the VM create process, obtain the ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="aa019-194">VM 需要特定格式的憑證，才能在開機時將其插入，因此請將憑證轉換為 [az vm format-secret](/cli/azure/vm#format-secret)。</span><span class="sxs-lookup"><span data-stu-id="aa019-194">The VM needs the certificate in a certain format to inject it on boot, so convert the certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="aa019-195">下列範例會將這些命令的輸出指派給變數，以方便在後續步驟中使用：</span><span class="sxs-lookup"><span data-stu-id="aa019-195">The following example assigns the output of these commands to variables for ease of use in the next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-to-secure-nginx"></a><span data-ttu-id="aa019-196">建立 Cloud-init 組態來保護 NGINX</span><span class="sxs-lookup"><span data-stu-id="aa019-196">Create cloud-init config to secure NGINX</span></span>
<span data-ttu-id="aa019-197">當您建立 VM 時，憑證和金鑰會儲存在受保護的 /var/lib/waagent/ 目錄中。</span><span class="sxs-lookup"><span data-stu-id="aa019-197">When you create a VM, certificates and keys are stored in the protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="aa019-198">若要將憑證自動新增至 VM 並設定 NGINX，您可以從上一個範例中使用更新的 cloud-init 組態。</span><span class="sxs-lookup"><span data-stu-id="aa019-198">To automate adding the certificate to the VM and configuring NGINX, you can use an updated cloud-init config from the previous example.</span></span>

<span data-ttu-id="aa019-199">建立名為 cloud-init-secured.txt 的檔案，並貼上下列組態。</span><span class="sxs-lookup"><span data-stu-id="aa019-199">Create a file named *cloud-init-secured.txt* and paste the following configuration.</span></span> <span data-ttu-id="aa019-200">同樣地，如果您使用 Cloud Shell，請在該處而非在本機電腦上建立 cloud-init 組態檔。</span><span class="sxs-lookup"><span data-stu-id="aa019-200">Again, if you use the Cloud Shell, create the cloud-init config file there and not on your local machine.</span></span> <span data-ttu-id="aa019-201">使用 `sensible-editor cloud-init-secured.txt` 可建立檔案，並查看可用的編輯器清單。</span><span class="sxs-lookup"><span data-stu-id="aa019-201">Use `sensible-editor cloud-init-secured.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="aa019-202">請確定已正確複製整個 cloud-init 檔案，特別是第一行：</span><span class="sxs-lookup"><span data-stu-id="aa019-202">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-secure-vm"></a><span data-ttu-id="aa019-203">建立安全的 VM</span><span class="sxs-lookup"><span data-stu-id="aa019-203">Create secure VM</span></span>
<span data-ttu-id="aa019-204">現在，使用 [az vm create](/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="aa019-204">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="aa019-205">使用 `--secrets` 參數，從 Key Vault 插入憑證資料。</span><span class="sxs-lookup"><span data-stu-id="aa019-205">The certificate data is injected from Key Vault with the `--secrets` parameter.</span></span> <span data-ttu-id="aa019-206">如同先前範例，您也要使用 `--custom-data` 參數來傳入 cloud-init 組態：</span><span class="sxs-lookup"><span data-stu-id="aa019-206">As in the previous example, you also pass in the cloud-init config with the `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-secured.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="aa019-207">系統需要花幾分鐘的時間來建立 VM、安裝封裝和啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa019-207">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="aa019-208">在 Azure CLI 將您返回提示字元之後，背景工作會繼續執行。</span><span class="sxs-lookup"><span data-stu-id="aa019-208">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="aa019-209">可能需要再等候幾分鐘，才能存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa019-209">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="aa019-210">建立 VM 之後，請注意 Azure CLI 所顯示的 `publicIpAddress`。</span><span class="sxs-lookup"><span data-stu-id="aa019-210">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="aa019-211">此位址是用來透過 Web 瀏覽器存取 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa019-211">This address is used to access the Node.js app via a web browser.</span></span>

<span data-ttu-id="aa019-212">若要讓 Web 流量安全到達您的 VM，請使用 [az vm open-port](/cli/azure/vm#open-port) 從網際網路開啟通訊埠 443：</span><span class="sxs-lookup"><span data-stu-id="aa019-212">To allow secure web traffic to reach your VM, open port 443 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a><span data-ttu-id="aa019-213">測試安全的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="aa019-213">Test secure web app</span></span>
<span data-ttu-id="aa019-214">現在，您可以開啟 Web 瀏覽器，並在網址列輸入 *https://<publicIpAddress>*。</span><span class="sxs-lookup"><span data-stu-id="aa019-214">Now you can open a web browser and enter *https://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="aa019-215">提供您自己從 VM 建立程序中取得的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="aa019-215">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="aa019-216">如果您使用自我簽署憑證，請接受安全性警告：</span><span class="sxs-lookup"><span data-stu-id="aa019-216">Accept the security warning if you used a self-signed certificate:</span></span>

![接受 Web 瀏覽器安全性警告](./media/tutorial-automate-vm-deployment/browser-warning.png)

<span data-ttu-id="aa019-218">接著會顯示受保護的 NGINX 網站和 Node.js 應用程式，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="aa019-218">Your secured NGINX site and Node.js app is then displayed as in the following example:</span></span>

![檢視執行中安全的 NGINX 網站](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="aa019-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa019-220">Next steps</span></span>
<span data-ttu-id="aa019-221">在本教學課程中，您已在初次開機時使用 Cloud-init 來設定 VM。</span><span class="sxs-lookup"><span data-stu-id="aa019-221">In this tutorial, you configured VMs on first boot with cloud-init.</span></span> <span data-ttu-id="aa019-222">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="aa019-222">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aa019-223">建立 Cloud-init 組態檔</span><span class="sxs-lookup"><span data-stu-id="aa019-223">Create a cloud-init config file</span></span>
> * <span data-ttu-id="aa019-224">建立 VM 來使用 Cloud-init 檔案</span><span class="sxs-lookup"><span data-stu-id="aa019-224">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="aa019-225">在建立 VM 之後，檢視執行中的 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="aa019-225">View a running Node.js app after the VM is created</span></span>
> * <span data-ttu-id="aa019-226">使用 Key Vault 安全地儲存憑證</span><span class="sxs-lookup"><span data-stu-id="aa019-226">Use Key Vault to securely store certificates</span></span>
> * <span data-ttu-id="aa019-227">使用 Cloud-init 來安全地自動部署 NGINX</span><span class="sxs-lookup"><span data-stu-id="aa019-227">Automate secure deployments of NGINX with cloud-init</span></span>

<span data-ttu-id="aa019-228">前進至下一個教學課程，以了解如何建立自訂的 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="aa019-228">Advance to the next tutorial to learn how to create custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aa019-229">建立自訂的 VM 映像</span><span class="sxs-lookup"><span data-stu-id="aa019-229">Create custom VM images</span></span>](./tutorial-custom-images.md)
