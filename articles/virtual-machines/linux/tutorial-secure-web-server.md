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
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a>在 Azure 中的 Linux 虛擬機器上使用 SSL 憑證來保護網頁伺服器
toosecure web 伺服器，安全通訊端稍後 (SSL) 憑證可以是使用 tooencrypt 網路流量。 這些 SSL 憑證可以儲存在 Azure 金鑰保存庫，並在 Azure 中允許的憑證 tooLinux 虛擬機器 (Vm) 的安全部署。 在本教學課程中，您了解如何：

> [!div class="checklist"]
> * 建立 Azure Key Vault
> * 產生或上傳憑證 toohello 金鑰保存庫
> * 建立 VM，並且安裝 hello NGINX 網頁伺服器
> * 插入 hello VM 中的 hello 憑證，並使用 SSL 繫結設定 NGINX

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。  


## <a name="overview"></a>概觀
Azure Key Vault 會保護密碼編譯金鑰和祕密，這類憑證或密碼。 金鑰保存庫可協助簡化 hello 憑證管理程序，並讓您存取那些憑證的索引鍵的 toomaintain 控制項。 您可以在 Key Vault 內建立自我簽署憑證，或上傳您目前已經擁有的受信任憑證。

您不必使用包含了內建憑證的自訂 VM 映像，而是要將憑證插入執行中的 VM。 此程序可確保 hello 最新的憑證會在部署期間安裝網頁伺服器上。 如果您更新或取代憑證時，您還沒有 toocreate 新的自訂 VM 映像。 當您建立其他的 Vm 會自動插入 hello 最新的憑證。 Hello 整個程序期間 hello 憑證永遠不會保留 hello Azure 平台，或會公開在指令碼、 命令列的歷程記錄或範本。


## <a name="create-an-azure-key-vault"></a>建立 Azure Key Vault
建立 Key Vault 和憑證之前，請先使用 [az group create](/cli/azure/group#create) 來建立資源群組。 hello 下列範例會建立名為的資源群組*myResourceGroupSecureWeb*在 hello *eastus*位置：

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

接著，使用 [az keyvault create](/cli/azure/keyvault#create) 建立 Key Vault，並加以啟用以供您在部署 VM 時使用。 每個 Key Vault 需要唯一的名稱，而且應該全部小寫。 取代 *<mykeyvault>* 在下列範例使用您自己的唯一金鑰保存庫名稱 hello:

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>產生憑證並儲存於 Key Vault
若要在生產環境中使用，您應該使用 [az keyvault certificate import](/cli/azure/certificate#import) 來匯入由受信任的提供者所簽署的有效憑證。 本教學課程，hello 下列範例示範如何產生自我簽署的憑證與[az keyvault 憑證建立](/cli/azure/certificate#create)使用 hello 預設憑證原則：

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a>準備要與 VM 搭配使用的憑證
toouse hello 憑證期間 hello VM 建立處理程序，取得您的憑證與 hello 識別碼[az keyvault 密碼清單-版本](/cli/azure/keyvault/secret#list-versions)。 Hello 憑證與轉換[az vm 格式密碼](/cli/azure/vm#format-secret)。 下列範例中的 hello 指派 hello 輸出，以便於 hello 中使用這些命令 toovariables 的下一個步驟：

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a>建立雲端 init config toosecure NGINX
[雲端 init](https://cloudinit.readthedocs.io)是廣泛使用的方法 toocustomize Linux VM，因為它開機 hello 第一次。 您可以使用雲端 init tooinstall 封裝，並將寫入檔案或 tooconfigure 使用者和安全性。 當雲端 init hello 首次開機程序期間執行時，有任何額外的步驟或所需的代理程式 tooapply 您的設定。

當您建立 VM 時，憑證和金鑰會儲存在受保護的 hello */var/lib/waagent/*目錄。 tooautomate 新增 hello 憑證 toohello VM，並設定 hello 網頁伺服器，使用雲端 init。 在此範例中，我們可以安裝和設定 hello NGINX 網頁伺服器。 您可以使用 hello 相同處理 tooinstall 及設定 Apache。 

建立名為*雲端 init-web server.txt*和 hello 貼上下列組態：

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

### <a name="create-a-secure-vm"></a>建立安全的 VM
現在，使用 [az vm create](/cli/azure/vm#create) 建立 VM。 hello 憑證資料會插入金鑰保存庫中的 hello 與`--secrets`參數。 您要傳入 hello 雲端 init 組態以 hello`--custom-data`參數：

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

花幾分鐘，讓建立 hello VM toobe hello 封裝 tooinstall 和 hello 應用程式 toostart。 建立 hello VM 後，請記下 hello`publicIpAddress`顯示 hello Azure CLI。 此位址是使用的 tooaccess 您網頁瀏覽器中的站台。

tooallow 保護 web 流量 tooreach VM，開啟連接埠 443 從網際網路 hello 與[az vm 開啟通訊埠](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a>測試 hello 安全的 web 應用程式
現在您可以開啟網頁瀏覽器並輸入*https://<publicIpAddress>*  hello 網址列中。 提供自己的公用 IP 位址從 hello VM 建立處理程序。 如果您使用自我簽署的憑證，請接受 hello 安全性警告：

![接受 Web 瀏覽器安全性警告](./media/tutorial-secure-web-server/browser-warning.png)

受保護的 NGINX 網站接著會顯示如 hello 下列範例所示：

![檢視執行中安全的 NGINX 網站](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a>後續步驟

在本教學課程中，您已使用儲存在 Azure Key Vault 中的 SSL 憑證來保護 NGINX 網頁伺服器。 您已了解如何︰

> [!div class="checklist"]
> * 建立 Azure Key Vault
> * 產生或上傳憑證 toohello 金鑰保存庫
> * 建立 VM，並且安裝 hello NGINX 網頁伺服器
> * 插入 hello VM 中的 hello 憑證，並使用 SSL 繫結設定 NGINX

請依照此連結 toosee，預先建立的虛擬機器指令碼範例。

> [!div class="nextstepaction"]
> [Windows 虛擬機器指令碼範例](./cli-samples.md)