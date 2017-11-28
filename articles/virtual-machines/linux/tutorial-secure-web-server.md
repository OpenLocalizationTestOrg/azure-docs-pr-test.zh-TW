---
title: "在 Azure 中使用 SSL 憑證來保護網頁伺服器 | Microsoft Docs"
description: "了解如何在 Azure 中的 Linux VM 上使用 SSL 憑證來保護 NGINX 網頁伺服器"
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
ms.openlocfilehash: 181be35aeb61020db3abaeba22aa882848923c31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="94df0-103">在 Azure 中的 Linux 虛擬機器上使用 SSL 憑證來保護網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="94df0-103">Secure a web server with SSL certificates on a Linux virtual machine in Azure</span></span>
<span data-ttu-id="94df0-104">若要保護網頁伺服器，您可以使用安全通訊端層 (SSL) 憑證來將網路流量加密。</span><span class="sxs-lookup"><span data-stu-id="94df0-104">To secure web servers, a Secure Sockets Later (SSL) certificate can be used to encrypt web traffic.</span></span> <span data-ttu-id="94df0-105">這些 SSL 憑證可儲存在 Azure Key Vault，並且能夠讓您將憑證安全地部署到 Azure 中的 Linux 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="94df0-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates to Linux virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="94df0-106">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="94df0-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="94df0-107">建立 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="94df0-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="94df0-108">產生或上傳憑證至 Key Vault</span><span class="sxs-lookup"><span data-stu-id="94df0-108">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="94df0-109">建立 VM 並安裝 NGINX 網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="94df0-109">Create a VM and install the NGINX web server</span></span>
> * <span data-ttu-id="94df0-110">將憑證插入 VM 並使用 SSL 繫結來設定 NGINX</span><span class="sxs-lookup"><span data-stu-id="94df0-110">Inject the certificate into the VM and configure NGINX with an SSL binding</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="94df0-111">如果您選擇在本機安裝和使用 CLI，本教學課程會要求您執行 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="94df0-111">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="94df0-112">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="94df0-112">Run `az --version` to find the version.</span></span> <span data-ttu-id="94df0-113">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="94df0-113">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  


## <a name="overview"></a><span data-ttu-id="94df0-114">概觀</span><span class="sxs-lookup"><span data-stu-id="94df0-114">Overview</span></span>
<span data-ttu-id="94df0-115">Azure Key Vault 會保護密碼編譯金鑰和祕密，這類憑證或密碼。</span><span class="sxs-lookup"><span data-stu-id="94df0-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="94df0-116">Key Vault 有助於簡化憑證管理程序，並可讓您掌控用來存取這些憑證的金鑰。</span><span class="sxs-lookup"><span data-stu-id="94df0-116">Key Vault helps streamline the certificate management process and enables you to maintain control of keys that access those certificates.</span></span> <span data-ttu-id="94df0-117">您可以在 Key Vault 內建立自我簽署憑證，或上傳您目前已經擁有的受信任憑證。</span><span class="sxs-lookup"><span data-stu-id="94df0-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="94df0-118">您不必使用包含了內建憑證的自訂 VM 映像，而是要將憑證插入執行中的 VM。</span><span class="sxs-lookup"><span data-stu-id="94df0-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="94df0-119">此程序可確保您在部署期間安裝在網頁伺服器上的憑證會是最新的。</span><span class="sxs-lookup"><span data-stu-id="94df0-119">This process ensures that the most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="94df0-120">如果您更新或取代憑證，您就不必另外再建立新的自訂 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="94df0-120">If you renew or replace a certificate, you don't also have to create a new custom VM image.</span></span> <span data-ttu-id="94df0-121">當您建立其他 VM 時，系統會自動插入最新的憑證。</span><span class="sxs-lookup"><span data-stu-id="94df0-121">The latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="94df0-122">在整個過程中，憑證絕對不會離開 Azure 平台，或在指令碼、命令列記錄或範本中公開。</span><span class="sxs-lookup"><span data-stu-id="94df0-122">During the whole process, the certificates never leave the Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="94df0-123">建立 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="94df0-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="94df0-124">建立 Key Vault 和憑證之前，請先使用 [az group create](/cli/azure/group#create) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="94df0-124">Before you can create a Key Vault and certificates, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="94df0-125">下列範例會在 eastus 位置建立名為 myResourceGroupSecureWeb 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="94df0-125">The following example creates a resource group named *myResourceGroupSecureWeb* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

<span data-ttu-id="94df0-126">接著，使用 [az keyvault create](/cli/azure/keyvault#create) 建立 Key Vault，並加以啟用以供您在部署 VM 時使用。</span><span class="sxs-lookup"><span data-stu-id="94df0-126">Next, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="94df0-127">每個 Key Vault 需要唯一的名稱，而且應該全部小寫。</span><span class="sxs-lookup"><span data-stu-id="94df0-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="94df0-128">使用您自己唯一的 Key Vault 名稱來取代下列範例中的 *<mykeyvault>*：</span><span class="sxs-lookup"><span data-stu-id="94df0-128">Replace *<mykeyvault>* in the following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="94df0-129">產生憑證並儲存於 Key Vault</span><span class="sxs-lookup"><span data-stu-id="94df0-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="94df0-130">若要在生產環境中使用，您應該使用 [az keyvault certificate import](/cli/azure/certificate#import) 來匯入由受信任的提供者所簽署的有效憑證。</span><span class="sxs-lookup"><span data-stu-id="94df0-130">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/certificate#import).</span></span> <span data-ttu-id="94df0-131">在本教學課程中，下列範例示範如何透過使用預設憑證原則的 [az keyvault certificate create](/cli/azure/certificate#create) 來產生自我簽署憑證：</span><span class="sxs-lookup"><span data-stu-id="94df0-131">For this tutorial, the following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/certificate#create) that uses the default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a><span data-ttu-id="94df0-132">準備要與 VM 搭配使用的憑證</span><span class="sxs-lookup"><span data-stu-id="94df0-132">Prepare a certificate for use with a VM</span></span>
<span data-ttu-id="94df0-133">若要在 VM 建立程序期間使用憑證，使用 [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions) 來取得憑證的識別碼。</span><span class="sxs-lookup"><span data-stu-id="94df0-133">To use the certificate during the VM create process, obtain the ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="94df0-134">使用 [az vm format-secret](/cli/azure/vm#format-secret) 轉換憑證。</span><span class="sxs-lookup"><span data-stu-id="94df0-134">Convert the certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="94df0-135">下列範例會將這些命令的輸出指派給變數，以方便在後續步驟中使用：</span><span class="sxs-lookup"><span data-stu-id="94df0-135">The following example assigns the output of these commands to variables for ease of use in the next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-to-secure-nginx"></a><span data-ttu-id="94df0-136">建立 Cloud-init 組態來保護 NGINX</span><span class="sxs-lookup"><span data-stu-id="94df0-136">Create a cloud-init config to secure NGINX</span></span>
<span data-ttu-id="94df0-137">[Cloud-init (英文)](https://cloudinit.readthedocs.io) 是在 Linux VM 初次開機時，廣泛用來自訂它們的方法。</span><span class="sxs-lookup"><span data-stu-id="94df0-137">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach to customize a Linux VM as it boots for the first time.</span></span> <span data-ttu-id="94df0-138">您可以使用 cloud-init 來安裝封裝和寫入檔案，或者設定使用者和安全性。</span><span class="sxs-lookup"><span data-stu-id="94df0-138">You can use cloud-init to install packages and write files, or to configure users and security.</span></span> <span data-ttu-id="94df0-139">當 cloud-init 在初次開機程序期間執行時，不需要使用任何額外的步驟或必要的代理程式來套用您的組態。</span><span class="sxs-lookup"><span data-stu-id="94df0-139">As cloud-init runs during the initial boot process, there are no additional steps or required agents to apply your configuration.</span></span>

<span data-ttu-id="94df0-140">當您建立 VM 時，憑證和金鑰會儲存在受保護的 /var/lib/waagent/ 目錄中。</span><span class="sxs-lookup"><span data-stu-id="94df0-140">When you create a VM, certificates and keys are stored in the protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="94df0-141">若要自動將憑證新增至 VM 並設定網頁伺服器，請使用 cloud-init。</span><span class="sxs-lookup"><span data-stu-id="94df0-141">To automate adding the certificate to the VM and configuring the web server, use cloud-init.</span></span> <span data-ttu-id="94df0-142">在此範例中，我們會安裝和設定 NGINX 網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="94df0-142">In this example, we install and configure the NGINX web server.</span></span> <span data-ttu-id="94df0-143">您可以使用相同的程序來安裝和設定 Apache。</span><span class="sxs-lookup"><span data-stu-id="94df0-143">You can use the same process to install and configure Apache.</span></span> 

<span data-ttu-id="94df0-144">建立名為 cloud-init-web-server.txt 的檔案，並貼上下列組態：</span><span class="sxs-lookup"><span data-stu-id="94df0-144">Create a file named *cloud-init-web-server.txt* and paste the following configuration:</span></span>

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

### <a name="create-a-secure-vm"></a><span data-ttu-id="94df0-145">建立安全的 VM</span><span class="sxs-lookup"><span data-stu-id="94df0-145">Create a secure VM</span></span>
<span data-ttu-id="94df0-146">現在，使用 [az vm create](/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="94df0-146">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="94df0-147">使用 `--secrets` 參數，從 Key Vault 插入憑證資料。</span><span class="sxs-lookup"><span data-stu-id="94df0-147">The certificate data is injected from Key Vault with the `--secrets` parameter.</span></span> <span data-ttu-id="94df0-148">使用 `--custom-data` 參數傳入 cloud-init 組態：</span><span class="sxs-lookup"><span data-stu-id="94df0-148">You pass in the cloud-init config with the `--custom-data` parameter:</span></span>

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

<span data-ttu-id="94df0-149">系統需要花幾分鐘的時間來建立 VM、安裝封裝和啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="94df0-149">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="94df0-150">建立 VM 之後，請注意 Azure CLI 所顯示的 `publicIpAddress`。</span><span class="sxs-lookup"><span data-stu-id="94df0-150">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="94df0-151">您可以使用此位址在網頁瀏覽器中存取您的網站。</span><span class="sxs-lookup"><span data-stu-id="94df0-151">This address is used to access your site in a web browser.</span></span>

<span data-ttu-id="94df0-152">若要讓 Web 流量安全到達您的 VM，請使用 [az vm open-port](/cli/azure/vm#open-port) 從網際網路開啟通訊埠 443：</span><span class="sxs-lookup"><span data-stu-id="94df0-152">To allow secure web traffic to reach your VM, open port 443 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-the-secure-web-app"></a><span data-ttu-id="94df0-153">測試安全的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="94df0-153">Test the secure web app</span></span>
<span data-ttu-id="94df0-154">現在，您可以開啟 Web 瀏覽器，並在網址列輸入 *https://<publicIpAddress>*。</span><span class="sxs-lookup"><span data-stu-id="94df0-154">Now you can open a web browser and enter *https://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="94df0-155">提供您自己從 VM 建立程序中取得的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="94df0-155">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="94df0-156">如果您使用自我簽署憑證，請接受安全性警告：</span><span class="sxs-lookup"><span data-stu-id="94df0-156">Accept the security warning if you used a self-signed certificate:</span></span>

![接受 Web 瀏覽器安全性警告](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="94df0-158">接著會顯示受保護的 NGINX 網站，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="94df0-158">Your secured NGINX site is then displayed as in the following example:</span></span>

![檢視執行中安全的 NGINX 網站](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="94df0-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="94df0-160">Next steps</span></span>

<span data-ttu-id="94df0-161">在本教學課程中，您已使用儲存在 Azure Key Vault 中的 SSL 憑證來保護 NGINX 網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="94df0-161">In this tutorial, you secured an NGINX web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="94df0-162">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="94df0-162">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="94df0-163">建立 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="94df0-163">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="94df0-164">產生或上傳憑證至 Key Vault</span><span class="sxs-lookup"><span data-stu-id="94df0-164">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="94df0-165">建立 VM 並安裝 NGINX 網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="94df0-165">Create a VM and install the NGINX web server</span></span>
> * <span data-ttu-id="94df0-166">將憑證插入 VM 並使用 SSL 繫結來設定 NGINX</span><span class="sxs-lookup"><span data-stu-id="94df0-166">Inject the certificate into the VM and configure NGINX with an SSL binding</span></span>

<span data-ttu-id="94df0-167">用以下連結查看預先建立的虛擬機器指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="94df0-167">Follow this link to see pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="94df0-168">Windows 虛擬機器指令碼範例</span><span class="sxs-lookup"><span data-stu-id="94df0-168">Windows virtual machine script samples</span></span>](./cli-samples.md)