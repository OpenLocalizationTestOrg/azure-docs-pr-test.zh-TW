---
title: "aaaCustomize Linux VM 在 Azure 中的第一次開機 |Microsoft 文件"
description: "了解如何 toouse 雲端 init 和金鑰保存庫 toocustomze Linux Vm hello 第一次在開機在 Azure 中"
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
ms.openlocfilehash: 280189723ac0205226f9c0068bd605da13249ace
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a><span data-ttu-id="7a373-103">如何 toocustomize Linux 虛擬機器第一次開機</span><span class="sxs-lookup"><span data-stu-id="7a373-103">How toocustomize a Linux virtual machine on first boot</span></span>
<span data-ttu-id="7a373-104">在先前的教學課程中，您學到如何 tooSSH tooa 虛擬機器 (VM) 並手動安裝 NGINX。</span><span class="sxs-lookup"><span data-stu-id="7a373-104">In a previous tutorial, you learned how tooSSH tooa virtual machine (VM) and manually install NGINX.</span></span> <span data-ttu-id="7a373-105">通常需要快速且一致的方式，某種形式的自動化 toocreate Vm。</span><span class="sxs-lookup"><span data-stu-id="7a373-105">toocreate VMs in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="7a373-106">常見的方法 toocustomize 上第一次開機的 VM 是 toouse[雲端 init](https://cloudinit.readthedocs.io)。</span><span class="sxs-lookup"><span data-stu-id="7a373-106">A common approach toocustomize a VM on first boot is toouse [cloud-init](https://cloudinit.readthedocs.io).</span></span> <span data-ttu-id="7a373-107">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="7a373-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7a373-108">建立 Cloud-init 組態檔</span><span class="sxs-lookup"><span data-stu-id="7a373-108">Create a cloud-init config file</span></span>
> * <span data-ttu-id="7a373-109">建立 VM 來使用 Cloud-init 檔案</span><span class="sxs-lookup"><span data-stu-id="7a373-109">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="7a373-110">Hello 建立 VM 之後，檢視執行 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a373-110">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="7a373-111">使用金鑰保存庫 toosecurely 存放區的憑證</span><span class="sxs-lookup"><span data-stu-id="7a373-111">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="7a373-112">使用 Cloud-init 來安全地自動部署 NGINX</span><span class="sxs-lookup"><span data-stu-id="7a373-112">Automate secure deployments of NGINX with cloud-init</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7a373-113">如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="7a373-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="7a373-114">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="7a373-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7a373-115">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="7a373-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  



## <a name="cloud-init-overview"></a><span data-ttu-id="7a373-116">Cloud-Init 概觀</span><span class="sxs-lookup"><span data-stu-id="7a373-116">Cloud-init overview</span></span>
<span data-ttu-id="7a373-117">[雲端 init](https://cloudinit.readthedocs.io)是廣泛使用的方法 toocustomize Linux VM，因為它開機 hello 第一次。</span><span class="sxs-lookup"><span data-stu-id="7a373-117">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="7a373-118">您可以使用雲端 init tooinstall 封裝，並將寫入檔案或 tooconfigure 使用者和安全性。</span><span class="sxs-lookup"><span data-stu-id="7a373-118">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="7a373-119">當雲端 init hello 首次開機程序期間執行時，有任何額外的步驟或所需的代理程式 tooapply 您的設定。</span><span class="sxs-lookup"><span data-stu-id="7a373-119">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="7a373-120">Cloud-init 也適用於散發套件。</span><span class="sxs-lookup"><span data-stu-id="7a373-120">Cloud-init also works across distributions.</span></span> <span data-ttu-id="7a373-121">例如，您不使用**apt get 安裝**或**yum 安裝**tooinstall 封裝。</span><span class="sxs-lookup"><span data-stu-id="7a373-121">For example, you don't use **apt-get install** or **yum install** tooinstall a package.</span></span> <span data-ttu-id="7a373-122">相反地，您可以定義封裝 tooinstall 的清單。</span><span class="sxs-lookup"><span data-stu-id="7a373-122">Instead you can define a list of packages tooinstall.</span></span> <span data-ttu-id="7a373-123">雲端 init 自動使用您選取的 hello distro hello 的原生封裝管理工具。</span><span class="sxs-lookup"><span data-stu-id="7a373-123">Cloud-init automatically uses hello native package management tool for hello distro you select.</span></span>

<span data-ttu-id="7a373-124">我們會使用我們合作夥伴 tooget 雲端 for-init 包含以及他們提供 tooAzure hello 映像中的工作。</span><span class="sxs-lookup"><span data-stu-id="7a373-124">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span> <span data-ttu-id="7a373-125">hello 下表概述在 Azure 平台映像上的 hello 目前雲端 init 可用性：</span><span class="sxs-lookup"><span data-stu-id="7a373-125">hello following table outlines hello current cloud-init availability on Azure platform images:</span></span>

| <span data-ttu-id="7a373-126">Alias</span><span class="sxs-lookup"><span data-stu-id="7a373-126">Alias</span></span> | <span data-ttu-id="7a373-127">發佈者</span><span class="sxs-lookup"><span data-stu-id="7a373-127">Publisher</span></span> | <span data-ttu-id="7a373-128">提供項目</span><span class="sxs-lookup"><span data-stu-id="7a373-128">Offer</span></span> | <span data-ttu-id="7a373-129">SKU</span><span class="sxs-lookup"><span data-stu-id="7a373-129">SKU</span></span> | <span data-ttu-id="7a373-130">版本</span><span class="sxs-lookup"><span data-stu-id="7a373-130">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="7a373-131">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="7a373-131">UbuntuLTS</span></span> |<span data-ttu-id="7a373-132">Canonical</span><span class="sxs-lookup"><span data-stu-id="7a373-132">Canonical</span></span> |<span data-ttu-id="7a373-133">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="7a373-133">UbuntuServer</span></span> |<span data-ttu-id="7a373-134">16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="7a373-134">16.04-LTS</span></span> |<span data-ttu-id="7a373-135">最新</span><span class="sxs-lookup"><span data-stu-id="7a373-135">latest</span></span> |
| <span data-ttu-id="7a373-136">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="7a373-136">UbuntuLTS</span></span> |<span data-ttu-id="7a373-137">Canonical</span><span class="sxs-lookup"><span data-stu-id="7a373-137">Canonical</span></span> |<span data-ttu-id="7a373-138">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="7a373-138">UbuntuServer</span></span> |<span data-ttu-id="7a373-139">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="7a373-139">14.04.5-LTS</span></span> |<span data-ttu-id="7a373-140">最新</span><span class="sxs-lookup"><span data-stu-id="7a373-140">latest</span></span> |
| <span data-ttu-id="7a373-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="7a373-141">CoreOS</span></span> |<span data-ttu-id="7a373-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="7a373-142">CoreOS</span></span> |<span data-ttu-id="7a373-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="7a373-143">CoreOS</span></span> |<span data-ttu-id="7a373-144">Stable</span><span class="sxs-lookup"><span data-stu-id="7a373-144">Stable</span></span> |<span data-ttu-id="7a373-145">最新</span><span class="sxs-lookup"><span data-stu-id="7a373-145">latest</span></span> |


## <a name="create-cloud-init-config-file"></a><span data-ttu-id="7a373-146">建立 Cloud-init 組態檔</span><span class="sxs-lookup"><span data-stu-id="7a373-146">Create cloud-init config file</span></span>
<span data-ttu-id="7a373-147">toosee 雲端初始化在動作中，建立的 VM，安裝 NGINX 並執行簡單的 ' Hello World' Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a373-147">toosee cloud-init in action, create a VM that installs NGINX and runs a simple 'Hello World' Node.js app.</span></span> <span data-ttu-id="7a373-148">下列雲端 init 組態的 hello 安裝所需的 hello 封裝、 建立 Node.js 應用程式，則初始化和啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a373-148">hello following cloud-init configuration installs hello required packages, creates a Node.js app, then initialize and starts hello app.</span></span>

<span data-ttu-id="7a373-149">您目前的殼層中建立名為*雲端 init.txt*和 hello 貼上下列組態。</span><span class="sxs-lookup"><span data-stu-id="7a373-149">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="7a373-150">例如，在 hello 雲端 Shell 不在您本機電腦上建立 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="7a373-150">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="7a373-151">您可以使用任何您想要的編輯器。</span><span class="sxs-lookup"><span data-stu-id="7a373-151">You can use any editor you wish.</span></span> <span data-ttu-id="7a373-152">輸入`sensible-editor cloud-init.txt`toocreate hello 檔案，並查看一份可用的編輯器。</span><span class="sxs-lookup"><span data-stu-id="7a373-152">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="7a373-153">請確定已正確複製該 hello 整個雲端初始化檔案，特別是 hello 第一行：</span><span class="sxs-lookup"><span data-stu-id="7a373-153">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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

<span data-ttu-id="7a373-154">如需 Cloud-init 組態選項的詳細資訊，請參閱 [Cloud-init 組態範例](https://cloudinit.readthedocs.io/en/latest/topics/examples.html) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="7a373-154">For more information about cloud-init configuration options, see [cloud-init config examples](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="7a373-155">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="7a373-155">Create virtual machine</span></span>
<span data-ttu-id="7a373-156">建立 VM 之前，請先使用 [az group create](/cli/azure/group#create) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="7a373-156">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="7a373-157">hello 下列範例會建立名為的資源群組*myResourceGroupAutomate*在 hello *eastus*位置：</span><span class="sxs-lookup"><span data-stu-id="7a373-157">hello following example creates a resource group named *myResourceGroupAutomate* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

<span data-ttu-id="7a373-158">現在，使用 [az vm create](/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="7a373-158">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="7a373-159">使用 hello`--custom-data`參數 toopass 雲端 init 組態檔中的。</span><span class="sxs-lookup"><span data-stu-id="7a373-159">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="7a373-160">提供 hello 完整路徑 toohello*雲端 init.txt*組態如果 hello 檔案儲存目前的工作目錄之外。</span><span class="sxs-lookup"><span data-stu-id="7a373-160">Provide hello full path toohello *cloud-init.txt* config if you saved hello file outside of your present working directory.</span></span> <span data-ttu-id="7a373-161">hello 下列範例會建立名為的 VM *myAutomatedVM*:</span><span class="sxs-lookup"><span data-stu-id="7a373-161">hello following example creates a VM named *myAutomatedVM*:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="7a373-162">花幾分鐘，讓建立 hello VM toobe hello 封裝 tooinstall 和 hello 應用程式 toostart。</span><span class="sxs-lookup"><span data-stu-id="7a373-162">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="7a373-163">有 hello Azure CLI 會傳回 toohello 提示之後，繼續 toorun 的背景工作。</span><span class="sxs-lookup"><span data-stu-id="7a373-163">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="7a373-164">它可能是另一個數分鐘才能存取 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a373-164">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="7a373-165">建立 hello VM 後，請記下 hello`publicIpAddress`顯示 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="7a373-165">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="7a373-166">這個位址是透過 web 瀏覽器使用的 tooaccess hello Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a373-166">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="7a373-167">tooallow web 流量 tooreach VM，開啟的通訊埠 80 hello 網際網路從[az vm 開啟通訊埠](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="7a373-167">tooallow web traffic tooreach your VM, open port 80 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a><span data-ttu-id="7a373-168">測試 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a373-168">Test web app</span></span>
<span data-ttu-id="7a373-169">現在您可以開啟網頁瀏覽器並輸入*http://<publicIpAddress>*  hello 網址列中。</span><span class="sxs-lookup"><span data-stu-id="7a373-169">Now you can open a web browser and enter *http://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="7a373-170">提供自己的公用 IP 位址從 hello VM 建立處理程序。</span><span class="sxs-lookup"><span data-stu-id="7a373-170">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="7a373-171">Node.js 應用程式會顯示如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="7a373-171">Your Node.js app is displayed as in hello following example:</span></span>

![檢視執行中的 NGINX 網站](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a><span data-ttu-id="7a373-173">從 Key Vault 插入憑證</span><span class="sxs-lookup"><span data-stu-id="7a373-173">Inject certificates from Key Vault</span></span>
<span data-ttu-id="7a373-174">此選用小節會示範如何安全地儲存在 Azure 金鑰保存庫中的憑證和 driver 期間 hello VM 部署。</span><span class="sxs-lookup"><span data-stu-id="7a373-174">This optional section shows how you can securely store certificates in Azure Key Vault and inject them during hello VM deployment.</span></span> <span data-ttu-id="7a373-175">而不是使用包含 hello 憑證的自訂映像的法式中，此程序可確保 hello 最新的憑證插入第一次開機 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="7a373-175">Rather than using a custom image that includes hello certificates baked-in, this process ensures that hello most up-to-date certificates are injected tooa VM on first boot.</span></span> <span data-ttu-id="7a373-176">Hello 過程 hello 憑證永遠不會離開 hello Azure 平台，或公開在指令碼、 命令列的歷程記錄或範本。</span><span class="sxs-lookup"><span data-stu-id="7a373-176">During hello process, hello certificate never leaves hello Azure platform or is exposed in a script, command-line history, or template.</span></span>

<span data-ttu-id="7a373-177">Azure Key Vault 會保護密碼編譯金鑰和祕密，像是憑證或密碼。</span><span class="sxs-lookup"><span data-stu-id="7a373-177">Azure Key Vault safeguards cryptographic keys and secrets, such as certificates or passwords.</span></span> <span data-ttu-id="7a373-178">金鑰保存庫可協助簡化 hello 金鑰管理程序，並讓您 toomaintain 控制項的索引鍵，以存取並加密資料。</span><span class="sxs-lookup"><span data-stu-id="7a373-178">Key Vault helps streamline hello key management process and enables you toomaintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="7a373-179">此案例中導入了某些金鑰保存庫概念 toocreate 和使用的憑證，但不是獨占概觀如何 toouse 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="7a373-179">This scenario introduces some Key Vault concepts toocreate and use a certificate, though is not an exhaustive overview on how toouse Key Vault.</span></span>

<span data-ttu-id="7a373-180">hello 下列步驟顯示如何：</span><span class="sxs-lookup"><span data-stu-id="7a373-180">hello following steps show how you can:</span></span>

- <span data-ttu-id="7a373-181">建立 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="7a373-181">Create an Azure Key Vault</span></span>
- <span data-ttu-id="7a373-182">產生或上傳憑證 toohello 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="7a373-182">Generate or upload a certificate toohello Key Vault</span></span>
- <span data-ttu-id="7a373-183">建立從 hello 憑證 tooinject tooa VM 中的密碼</span><span class="sxs-lookup"><span data-stu-id="7a373-183">Create a secret from hello certificate tooinject in tooa VM</span></span>
- <span data-ttu-id="7a373-184">建立 VM，並且插入 hello 憑證</span><span class="sxs-lookup"><span data-stu-id="7a373-184">Create a VM and inject hello certificate</span></span>

### <a name="create-an-azure-key-vault"></a><span data-ttu-id="7a373-185">建立 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="7a373-185">Create an Azure Key Vault</span></span>
<span data-ttu-id="7a373-186">首先，使用 [az keyvault create](/cli/azure/keyvault#create) 建立 Key Vault，並加以啟用以供您在部署 VM 時使用。</span><span class="sxs-lookup"><span data-stu-id="7a373-186">First, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="7a373-187">每個 Key Vault 需要唯一的名稱，而且應該全部小寫。</span><span class="sxs-lookup"><span data-stu-id="7a373-187">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="7a373-188">取代*mykeyvault*在下列範例使用您自己的唯一金鑰保存庫名稱 hello:</span><span class="sxs-lookup"><span data-stu-id="7a373-188">Replace *mykeyvault* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a><span data-ttu-id="7a373-189">產生憑證並儲存於 Key Vault</span><span class="sxs-lookup"><span data-stu-id="7a373-189">Generate certificate and store in Key Vault</span></span>
<span data-ttu-id="7a373-190">若要在生產環境中使用，您應該使用 [az keyvault certificate import](/cli/azure/keyvault/certificate#import) 來匯入由受信任的提供者所簽署的有效憑證。</span><span class="sxs-lookup"><span data-stu-id="7a373-190">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span></span> <span data-ttu-id="7a373-191">本教學課程，hello 下列範例示範如何產生自我簽署的憑證與[az keyvault 憑證建立](/cli/azure/keyvault/certificate#create)使用 hello 預設憑證原則：</span><span class="sxs-lookup"><span data-stu-id="7a373-191">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/keyvault/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a><span data-ttu-id="7a373-192">準備要與 VM 搭配使用的憑證</span><span class="sxs-lookup"><span data-stu-id="7a373-192">Prepare certificate for use with VM</span></span>
<span data-ttu-id="7a373-193">toouse hello 憑證期間 hello VM 建立處理程序，取得您的憑證與 hello 識別碼[az keyvault 密碼清單-版本](/cli/azure/keyvault/secret#list-versions)。</span><span class="sxs-lookup"><span data-stu-id="7a373-193">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="7a373-194">hello VM 需要 hello 憑證在特定格式 tooinject 它在開機，因此將轉換 hello 憑證[az vm 格式密碼](/cli/azure/vm#format-secret)。</span><span class="sxs-lookup"><span data-stu-id="7a373-194">hello VM needs hello certificate in a certain format tooinject it on boot, so convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="7a373-195">下列範例中的 hello 指派 hello 輸出，以便於 hello 中使用這些命令 toovariables 的下一個步驟：</span><span class="sxs-lookup"><span data-stu-id="7a373-195">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="7a373-196">建立雲端 init config toosecure NGINX</span><span class="sxs-lookup"><span data-stu-id="7a373-196">Create cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="7a373-197">當您建立 VM 時，憑證和金鑰會儲存在受保護的 hello */var/lib/waagent/*目錄。</span><span class="sxs-lookup"><span data-stu-id="7a373-197">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="7a373-198">新增 hello 憑證 toohello tooautomate VM 並設定 NGINX，您可以使用 hello 上一個範例更新的雲端初始化組態。</span><span class="sxs-lookup"><span data-stu-id="7a373-198">tooautomate adding hello certificate toohello VM and configuring NGINX, you can use an updated cloud-init config from hello previous example.</span></span>

<span data-ttu-id="7a373-199">建立名為*雲端-init-secured.txt*和 hello 貼上下列組態。</span><span class="sxs-lookup"><span data-stu-id="7a373-199">Create a file named *cloud-init-secured.txt* and paste hello following configuration.</span></span> <span data-ttu-id="7a373-200">同樣地，如果您使用 hello 雲端殼層，建立 hello 雲端 init 組態檔，該處，且不在您本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="7a373-200">Again, if you use hello Cloud Shell, create hello cloud-init config file there and not on your local machine.</span></span> <span data-ttu-id="7a373-201">使用`sensible-editor cloud-init-secured.txt`toocreate hello 檔案，並查看一份可用的編輯器。</span><span class="sxs-lookup"><span data-stu-id="7a373-201">Use `sensible-editor cloud-init-secured.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="7a373-202">請確定已正確複製該 hello 整個雲端初始化檔案，特別是 hello 第一行：</span><span class="sxs-lookup"><span data-stu-id="7a373-202">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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

### <a name="create-secure-vm"></a><span data-ttu-id="7a373-203">建立安全的 VM</span><span class="sxs-lookup"><span data-stu-id="7a373-203">Create secure VM</span></span>
<span data-ttu-id="7a373-204">現在，使用 [az vm create](/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="7a373-204">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="7a373-205">hello 憑證資料會插入金鑰保存庫中的 hello 與`--secrets`參數。</span><span class="sxs-lookup"><span data-stu-id="7a373-205">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="7a373-206">如同 hello 先前的範例，您也要傳入 hello 雲端 init 組態以 hello`--custom-data`參數：</span><span class="sxs-lookup"><span data-stu-id="7a373-206">As in hello previous example, you also pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

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

<span data-ttu-id="7a373-207">花幾分鐘，讓建立 hello VM toobe hello 封裝 tooinstall 和 hello 應用程式 toostart。</span><span class="sxs-lookup"><span data-stu-id="7a373-207">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="7a373-208">有 hello Azure CLI 會傳回 toohello 提示之後，繼續 toorun 的背景工作。</span><span class="sxs-lookup"><span data-stu-id="7a373-208">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="7a373-209">它可能是另一個數分鐘才能存取 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a373-209">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="7a373-210">建立 hello VM 後，請記下 hello`publicIpAddress`顯示 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="7a373-210">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="7a373-211">這個位址是透過 web 瀏覽器使用的 tooaccess hello Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a373-211">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="7a373-212">tooallow 保護 web 流量 tooreach VM，開啟連接埠 443 從網際網路 hello 與[az vm 開啟通訊埠](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="7a373-212">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a><span data-ttu-id="7a373-213">測試安全的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a373-213">Test secure web app</span></span>
<span data-ttu-id="7a373-214">現在您可以開啟網頁瀏覽器並輸入*https://<publicIpAddress>*  hello 網址列中。</span><span class="sxs-lookup"><span data-stu-id="7a373-214">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="7a373-215">提供自己的公用 IP 位址從 hello VM 建立處理程序。</span><span class="sxs-lookup"><span data-stu-id="7a373-215">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="7a373-216">如果您使用自我簽署的憑證，請接受 hello 安全性警告：</span><span class="sxs-lookup"><span data-stu-id="7a373-216">Accept hello security warning if you used a self-signed certificate:</span></span>

![接受 Web 瀏覽器安全性警告](./media/tutorial-automate-vm-deployment/browser-warning.png)

<span data-ttu-id="7a373-218">受保護的 NGINX 站台和 Node.js 應用程式接著會顯示如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="7a373-218">Your secured NGINX site and Node.js app is then displayed as in hello following example:</span></span>

![檢視執行中安全的 NGINX 網站](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="7a373-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a373-220">Next steps</span></span>
<span data-ttu-id="7a373-221">在本教學課程中，您已在初次開機時使用 Cloud-init 來設定 VM。</span><span class="sxs-lookup"><span data-stu-id="7a373-221">In this tutorial, you configured VMs on first boot with cloud-init.</span></span> <span data-ttu-id="7a373-222">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="7a373-222">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7a373-223">建立 Cloud-init 組態檔</span><span class="sxs-lookup"><span data-stu-id="7a373-223">Create a cloud-init config file</span></span>
> * <span data-ttu-id="7a373-224">建立 VM 來使用 Cloud-init 檔案</span><span class="sxs-lookup"><span data-stu-id="7a373-224">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="7a373-225">Hello 建立 VM 之後，檢視執行 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a373-225">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="7a373-226">使用金鑰保存庫 toosecurely 存放區的憑證</span><span class="sxs-lookup"><span data-stu-id="7a373-226">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="7a373-227">使用 Cloud-init 來安全地自動部署 NGINX</span><span class="sxs-lookup"><span data-stu-id="7a373-227">Automate secure deployments of NGINX with cloud-init</span></span>

<span data-ttu-id="7a373-228">如何前進 toohello 下一個教學課程 toolearn toocreate 自訂 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="7a373-228">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7a373-229">建立自訂的 VM 映像</span><span class="sxs-lookup"><span data-stu-id="7a373-229">Create custom VM images</span></span>](./tutorial-custom-images.md)
