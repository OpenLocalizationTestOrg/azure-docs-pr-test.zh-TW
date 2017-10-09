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
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a>如何 toocustomize Linux 虛擬機器第一次開機
在先前的教學課程中，您學到如何 tooSSH tooa 虛擬機器 (VM) 並手動安裝 NGINX。 通常需要快速且一致的方式，某種形式的自動化 toocreate Vm。 常見的方法 toocustomize 上第一次開機的 VM 是 toouse[雲端 init](https://cloudinit.readthedocs.io)。 在本教學課程中，您了解如何：

> [!div class="checklist"]
> * 建立 Cloud-init 組態檔
> * 建立 VM 來使用 Cloud-init 檔案
> * Hello 建立 VM 之後，檢視執行 Node.js 應用程式
> * 使用金鑰保存庫 toosecurely 存放區的憑證
> * 使用 Cloud-init 來安全地自動部署 NGINX


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。  



## <a name="cloud-init-overview"></a>Cloud-Init 概觀
[雲端 init](https://cloudinit.readthedocs.io)是廣泛使用的方法 toocustomize Linux VM，因為它開機 hello 第一次。 您可以使用雲端 init tooinstall 封裝，並將寫入檔案或 tooconfigure 使用者和安全性。 當雲端 init hello 首次開機程序期間執行時，有任何額外的步驟或所需的代理程式 tooapply 您的設定。

Cloud-init 也適用於散發套件。 例如，您不使用**apt get 安裝**或**yum 安裝**tooinstall 封裝。 相反地，您可以定義封裝 tooinstall 的清單。 雲端 init 自動使用您選取的 hello distro hello 的原生封裝管理工具。

我們會使用我們合作夥伴 tooget 雲端 for-init 包含以及他們提供 tooAzure hello 映像中的工作。 hello 下表概述在 Azure 平台映像上的 hello 目前雲端 init 可用性：

| Alias | 發佈者 | 提供項目 | SKU | 版本 |
|:--- |:--- |:--- |:--- |:--- |:--- |
| UbuntuLTS |Canonical |UbuntuServer |16.04-LTS |最新 |
| UbuntuLTS |Canonical |UbuntuServer |14.04.5-LTS |最新 |
| CoreOS |CoreOS |CoreOS |Stable |最新 |


## <a name="create-cloud-init-config-file"></a>建立 Cloud-init 組態檔
toosee 雲端初始化在動作中，建立的 VM，安裝 NGINX 並執行簡單的 ' Hello World' Node.js 應用程式。 下列雲端 init 組態的 hello 安裝所需的 hello 封裝、 建立 Node.js 應用程式，則初始化和啟動 hello 應用程式。

您目前的殼層中建立名為*雲端 init.txt*和 hello 貼上下列組態。 例如，在 hello 雲端 Shell 不在您本機電腦上建立 hello 檔案。 您可以使用任何您想要的編輯器。 輸入`sensible-editor cloud-init.txt`toocreate hello 檔案，並查看一份可用的編輯器。 請確定已正確複製該 hello 整個雲端初始化檔案，特別是 hello 第一行：

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

如需 Cloud-init 組態選項的詳細資訊，請參閱 [Cloud-init 組態範例](https://cloudinit.readthedocs.io/en/latest/topics/examples.html) \(英文\)。

## <a name="create-virtual-machine"></a>Create virtual machine
建立 VM 之前，請先使用 [az group create](/cli/azure/group#create) 來建立資源群組。 hello 下列範例會建立名為的資源群組*myResourceGroupAutomate*在 hello *eastus*位置：

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

現在，使用 [az vm create](/cli/azure/vm#create) 建立 VM。 使用 hello`--custom-data`參數 toopass 雲端 init 組態檔中的。 提供 hello 完整路徑 toohello*雲端 init.txt*組態如果 hello 檔案儲存目前的工作目錄之外。 hello 下列範例會建立名為的 VM *myAutomatedVM*:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

花幾分鐘，讓建立 hello VM toobe hello 封裝 tooinstall 和 hello 應用程式 toostart。 有 hello Azure CLI 會傳回 toohello 提示之後，繼續 toorun 的背景工作。 它可能是另一個數分鐘才能存取 hello 應用程式。 建立 hello VM 後，請記下 hello`publicIpAddress`顯示 hello Azure CLI。 這個位址是透過 web 瀏覽器使用的 tooaccess hello Node.js 應用程式。

tooallow web 流量 tooreach VM，開啟的通訊埠 80 hello 網際網路從[az vm 開啟通訊埠](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a>測試 Web 應用程式
現在您可以開啟網頁瀏覽器並輸入*http://<publicIpAddress>*  hello 網址列中。 提供自己的公用 IP 位址從 hello VM 建立處理程序。 Node.js 應用程式會顯示如 hello 下列範例所示：

![檢視執行中的 NGINX 網站](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a>從 Key Vault 插入憑證
此選用小節會示範如何安全地儲存在 Azure 金鑰保存庫中的憑證和 driver 期間 hello VM 部署。 而不是使用包含 hello 憑證的自訂映像的法式中，此程序可確保 hello 最新的憑證插入第一次開機 tooa VM。 Hello 過程 hello 憑證永遠不會離開 hello Azure 平台，或公開在指令碼、 命令列的歷程記錄或範本。

Azure Key Vault 會保護密碼編譯金鑰和祕密，像是憑證或密碼。 金鑰保存庫可協助簡化 hello 金鑰管理程序，並讓您 toomaintain 控制項的索引鍵，以存取並加密資料。 此案例中導入了某些金鑰保存庫概念 toocreate 和使用的憑證，但不是獨占概觀如何 toouse 金鑰保存庫。

hello 下列步驟顯示如何：

- 建立 Azure Key Vault
- 產生或上傳憑證 toohello 金鑰保存庫
- 建立從 hello 憑證 tooinject tooa VM 中的密碼
- 建立 VM，並且插入 hello 憑證

### <a name="create-an-azure-key-vault"></a>建立 Azure Key Vault
首先，使用 [az keyvault create](/cli/azure/keyvault#create) 建立 Key Vault，並加以啟用以供您在部署 VM 時使用。 每個 Key Vault 需要唯一的名稱，而且應該全部小寫。 取代*mykeyvault*在下列範例使用您自己的唯一金鑰保存庫名稱 hello:

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a>產生憑證並儲存於 Key Vault
若要在生產環境中使用，您應該使用 [az keyvault certificate import](/cli/azure/keyvault/certificate#import) 來匯入由受信任的提供者所簽署的有效憑證。 本教學課程，hello 下列範例示範如何產生自我簽署的憑證與[az keyvault 憑證建立](/cli/azure/keyvault/certificate#create)使用 hello 預設憑證原則：

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a>準備要與 VM 搭配使用的憑證
toouse hello 憑證期間 hello VM 建立處理程序，取得您的憑證與 hello 識別碼[az keyvault 密碼清單-版本](/cli/azure/keyvault/secret#list-versions)。 hello VM 需要 hello 憑證在特定格式 tooinject 它在開機，因此將轉換 hello 憑證[az vm 格式密碼](/cli/azure/vm#format-secret)。 下列範例中的 hello 指派 hello 輸出，以便於 hello 中使用這些命令 toovariables 的下一個步驟：

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a>建立雲端 init config toosecure NGINX
當您建立 VM 時，憑證和金鑰會儲存在受保護的 hello */var/lib/waagent/*目錄。 新增 hello 憑證 toohello tooautomate VM 並設定 NGINX，您可以使用 hello 上一個範例更新的雲端初始化組態。

建立名為*雲端-init-secured.txt*和 hello 貼上下列組態。 同樣地，如果您使用 hello 雲端殼層，建立 hello 雲端 init 組態檔，該處，且不在您本機電腦上。 使用`sensible-editor cloud-init-secured.txt`toocreate hello 檔案，並查看一份可用的編輯器。 請確定已正確複製該 hello 整個雲端初始化檔案，特別是 hello 第一行：

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

### <a name="create-secure-vm"></a>建立安全的 VM
現在，使用 [az vm create](/cli/azure/vm#create) 建立 VM。 hello 憑證資料會插入金鑰保存庫中的 hello 與`--secrets`參數。 如同 hello 先前的範例，您也要傳入 hello 雲端 init 組態以 hello`--custom-data`參數：

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

花幾分鐘，讓建立 hello VM toobe hello 封裝 tooinstall 和 hello 應用程式 toostart。 有 hello Azure CLI 會傳回 toohello 提示之後，繼續 toorun 的背景工作。 它可能是另一個數分鐘才能存取 hello 應用程式。 建立 hello VM 後，請記下 hello`publicIpAddress`顯示 hello Azure CLI。 這個位址是透過 web 瀏覽器使用的 tooaccess hello Node.js 應用程式。

tooallow 保護 web 流量 tooreach VM，開啟連接埠 443 從網際網路 hello 與[az vm 開啟通訊埠](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a>測試安全的 Web 應用程式
現在您可以開啟網頁瀏覽器並輸入*https://<publicIpAddress>*  hello 網址列中。 提供自己的公用 IP 位址從 hello VM 建立處理程序。 如果您使用自我簽署的憑證，請接受 hello 安全性警告：

![接受 Web 瀏覽器安全性警告](./media/tutorial-automate-vm-deployment/browser-warning.png)

受保護的 NGINX 站台和 Node.js 應用程式接著會顯示如 hello 下列範例所示：

![檢視執行中安全的 NGINX 網站](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a>後續步驟
在本教學課程中，您已在初次開機時使用 Cloud-init 來設定 VM。 您已了解如何︰

> [!div class="checklist"]
> * 建立 Cloud-init 組態檔
> * 建立 VM 來使用 Cloud-init 檔案
> * Hello 建立 VM 之後，檢視執行 Node.js 應用程式
> * 使用金鑰保存庫 toosecurely 存放區的憑證
> * 使用 Cloud-init 來安全地自動部署 NGINX

如何前進 toohello 下一個教學課程 toolearn toocreate 自訂 VM 映像。

> [!div class="nextstepaction"]
> [建立自訂的 VM 映像](./tutorial-custom-images.md)
