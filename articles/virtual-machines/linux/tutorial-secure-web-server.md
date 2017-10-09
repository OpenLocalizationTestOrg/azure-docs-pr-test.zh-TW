---
title: "SSL 的 web 伺服器憑證在 Azure 中的 aaaSecure |Microsoft 文件"
description: "了解如何 toosecure hello NGINX 網頁伺服器使用 SSL 憑證在 Azure 中的 Linux VM 上"
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
ms.date: 07/17/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: d3a62d77ac05c9aa2a44356b7c8e44cb485b81aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="920c9-103">在 Azure 中的 Linux 虛擬機器上使用 SSL 憑證來保護網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="920c9-103">Secure a web server with SSL certificates on a Linux virtual machine in Azure</span></span>
<span data-ttu-id="920c9-104">toosecure web 伺服器，安全通訊端稍後 (SSL) 憑證可以是使用 tooencrypt 網路流量。</span><span class="sxs-lookup"><span data-stu-id="920c9-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="920c9-105">這些 SSL 憑證可以儲存在 Azure 金鑰保存庫，並在 Azure 中允許的憑證 tooLinux 虛擬機器 (Vm) 的安全部署。</span><span class="sxs-lookup"><span data-stu-id="920c9-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooLinux virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="920c9-106">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="920c9-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="920c9-107">建立 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="920c9-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="920c9-108">產生或上傳憑證 toohello 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="920c9-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="920c9-109">建立 VM，並且安裝 hello NGINX 網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="920c9-109">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="920c9-110">插入 hello VM 中的 hello 憑證，並使用 SSL 繫結設定 NGINX</span><span class="sxs-lookup"><span data-stu-id="920c9-110">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="920c9-111">如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="920c9-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="920c9-112">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="920c9-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="920c9-113">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="920c9-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  


## <a name="overview"></a><span data-ttu-id="920c9-114">概觀</span><span class="sxs-lookup"><span data-stu-id="920c9-114">Overview</span></span>
<span data-ttu-id="920c9-115">Azure Key Vault 會保護密碼編譯金鑰和祕密，這類憑證或密碼。</span><span class="sxs-lookup"><span data-stu-id="920c9-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="920c9-116">金鑰保存庫可協助簡化 hello 憑證管理程序，並讓您存取那些憑證的索引鍵的 toomaintain 控制項。</span><span class="sxs-lookup"><span data-stu-id="920c9-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="920c9-117">您可以在 Key Vault 內建立自我簽署憑證，或上傳您目前已經擁有的受信任憑證。</span><span class="sxs-lookup"><span data-stu-id="920c9-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="920c9-118">您不必使用包含了內建憑證的自訂 VM 映像，而是要將憑證插入執行中的 VM。</span><span class="sxs-lookup"><span data-stu-id="920c9-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="920c9-119">此程序可確保 hello 最新的憑證會在部署期間安裝網頁伺服器上。</span><span class="sxs-lookup"><span data-stu-id="920c9-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="920c9-120">如果您更新或取代憑證時，您還沒有 toocreate 新的自訂 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="920c9-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="920c9-121">當您建立其他的 Vm 會自動插入 hello 最新的憑證。</span><span class="sxs-lookup"><span data-stu-id="920c9-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="920c9-122">Hello 整個程序期間 hello 憑證永遠不會保留 hello Azure 平台，或會公開在指令碼、 命令列的歷程記錄或範本。</span><span class="sxs-lookup"><span data-stu-id="920c9-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="920c9-123">建立 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="920c9-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="920c9-124">建立 Key Vault 和憑證之前，請先使用 [az group create](/cli/azure/group#create) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="920c9-124">Before you can create a Key Vault and certificates, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="920c9-125">hello 下列範例會建立名為的資源群組*myResourceGroupSecureWeb*在 hello *eastus*位置：</span><span class="sxs-lookup"><span data-stu-id="920c9-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

<span data-ttu-id="920c9-126">接著，使用 [az keyvault create](/cli/azure/keyvault#create) 建立 Key Vault，並加以啟用以供您在部署 VM 時使用。</span><span class="sxs-lookup"><span data-stu-id="920c9-126">Next, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="920c9-127">每個 Key Vault 需要唯一的名稱，而且應該全部小寫。</span><span class="sxs-lookup"><span data-stu-id="920c9-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="920c9-128">取代 *<mykeyvault>* 在下列範例使用您自己的唯一金鑰保存庫名稱 hello:</span><span class="sxs-lookup"><span data-stu-id="920c9-128">Replace *<mykeyvault>* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="920c9-129">產生憑證並儲存於 Key Vault</span><span class="sxs-lookup"><span data-stu-id="920c9-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="920c9-130">若要在生產環境中使用，您應該使用 [az keyvault certificate import](/cli/azure/certificate#import) 來匯入由受信任的提供者所簽署的有效憑證。</span><span class="sxs-lookup"><span data-stu-id="920c9-130">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/certificate#import).</span></span> <span data-ttu-id="920c9-131">本教學課程，hello 下列範例示範如何產生自我簽署的憑證與[az keyvault 憑證建立](/cli/azure/certificate#create)使用 hello 預設憑證原則：</span><span class="sxs-lookup"><span data-stu-id="920c9-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a><span data-ttu-id="920c9-132">準備要與 VM 搭配使用的憑證</span><span class="sxs-lookup"><span data-stu-id="920c9-132">Prepare a certificate for use with a VM</span></span>
<span data-ttu-id="920c9-133">toouse hello 憑證期間 hello VM 建立處理程序，取得您的憑證與 hello 識別碼[az keyvault 密碼清單-版本](/cli/azure/keyvault/secret#list-versions)。</span><span class="sxs-lookup"><span data-stu-id="920c9-133">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="920c9-134">Hello 憑證與轉換[az vm 格式密碼](/cli/azure/vm#format-secret)。</span><span class="sxs-lookup"><span data-stu-id="920c9-134">Convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="920c9-135">下列範例中的 hello 指派 hello 輸出，以便於 hello 中使用這些命令 toovariables 的下一個步驟：</span><span class="sxs-lookup"><span data-stu-id="920c9-135">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="920c9-136">建立雲端 init config toosecure NGINX</span><span class="sxs-lookup"><span data-stu-id="920c9-136">Create a cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="920c9-137">[雲端 init](https://cloudinit.readthedocs.io)是廣泛使用的方法 toocustomize Linux VM，因為它開機 hello 第一次。</span><span class="sxs-lookup"><span data-stu-id="920c9-137">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="920c9-138">您可以使用雲端 init tooinstall 封裝，並將寫入檔案或 tooconfigure 使用者和安全性。</span><span class="sxs-lookup"><span data-stu-id="920c9-138">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="920c9-139">當雲端 init hello 首次開機程序期間執行時，有任何額外的步驟或所需的代理程式 tooapply 您的設定。</span><span class="sxs-lookup"><span data-stu-id="920c9-139">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="920c9-140">當您建立 VM 時，憑證和金鑰會儲存在受保護的 hello */var/lib/waagent/*目錄。</span><span class="sxs-lookup"><span data-stu-id="920c9-140">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="920c9-141">tooautomate 新增 hello 憑證 toohello VM，並設定 hello 網頁伺服器，使用雲端 init。</span><span class="sxs-lookup"><span data-stu-id="920c9-141">tooautomate adding hello certificate toohello VM and configuring hello web server, use cloud-init.</span></span> <span data-ttu-id="920c9-142">在此範例中，我們可以安裝和設定 hello NGINX 網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="920c9-142">In this example, we install and configure hello NGINX web server.</span></span> <span data-ttu-id="920c9-143">您可以使用 hello 相同處理 tooinstall 及設定 Apache。</span><span class="sxs-lookup"><span data-stu-id="920c9-143">You can use hello same process tooinstall and configure Apache.</span></span> 

<span data-ttu-id="920c9-144">建立名為*雲端 init-web server.txt*和 hello 貼上下列組態：</span><span class="sxs-lookup"><span data-stu-id="920c9-144">Create a file named *cloud-init-web-server.txt* and paste hello following configuration:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
      }
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
```

### <a name="create-a-secure-vm"></a><span data-ttu-id="920c9-145">建立安全的 VM</span><span class="sxs-lookup"><span data-stu-id="920c9-145">Create a secure VM</span></span>
<span data-ttu-id="920c9-146">現在，使用 [az vm create](/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="920c9-146">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="920c9-147">hello 憑證資料會插入金鑰保存庫中的 hello 與`--secrets`參數。</span><span class="sxs-lookup"><span data-stu-id="920c9-147">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="920c9-148">您要傳入 hello 雲端 init 組態以 hello`--custom-data`參數：</span><span class="sxs-lookup"><span data-stu-id="920c9-148">You pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-web-server.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="920c9-149">花幾分鐘，讓建立 hello VM toobe hello 封裝 tooinstall 和 hello 應用程式 toostart。</span><span class="sxs-lookup"><span data-stu-id="920c9-149">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="920c9-150">建立 hello VM 後，請記下 hello`publicIpAddress`顯示 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="920c9-150">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="920c9-151">此位址是使用的 tooaccess 您網頁瀏覽器中的站台。</span><span class="sxs-lookup"><span data-stu-id="920c9-151">This address is used tooaccess your site in a web browser.</span></span>

<span data-ttu-id="920c9-152">tooallow 保護 web 流量 tooreach VM，開啟連接埠 443 從網際網路 hello 與[az vm 開啟通訊埠](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="920c9-152">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="920c9-153">測試 hello 安全的 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="920c9-153">Test hello secure web app</span></span>
<span data-ttu-id="920c9-154">現在您可以開啟網頁瀏覽器並輸入*https://<publicIpAddress>*  hello 網址列中。</span><span class="sxs-lookup"><span data-stu-id="920c9-154">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="920c9-155">提供自己的公用 IP 位址從 hello VM 建立處理程序。</span><span class="sxs-lookup"><span data-stu-id="920c9-155">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="920c9-156">如果您使用自我簽署的憑證，請接受 hello 安全性警告：</span><span class="sxs-lookup"><span data-stu-id="920c9-156">Accept hello security warning if you used a self-signed certificate:</span></span>

![接受 Web 瀏覽器安全性警告](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="920c9-158">受保護的 NGINX 網站接著會顯示如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="920c9-158">Your secured NGINX site is then displayed as in hello following example:</span></span>

![檢視執行中安全的 NGINX 網站](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="920c9-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="920c9-160">Next steps</span></span>

<span data-ttu-id="920c9-161">在本教學課程中，您已使用儲存在 Azure Key Vault 中的 SSL 憑證來保護 NGINX 網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="920c9-161">In this tutorial, you secured an NGINX web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="920c9-162">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="920c9-162">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="920c9-163">建立 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="920c9-163">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="920c9-164">產生或上傳憑證 toohello 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="920c9-164">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="920c9-165">建立 VM，並且安裝 hello NGINX 網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="920c9-165">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="920c9-166">插入 hello VM 中的 hello 憑證，並使用 SSL 繫結設定 NGINX</span><span class="sxs-lookup"><span data-stu-id="920c9-166">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

<span data-ttu-id="920c9-167">請依照此連結 toosee，預先建立的虛擬機器指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="920c9-167">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="920c9-168">Windows 虛擬機器指令碼範例</span><span class="sxs-lookup"><span data-stu-id="920c9-168">Windows virtual machine script samples</span></span>](./cli-samples.md)