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
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a>部署 OpenShift 原點 tooAzure 虛擬機器 

[OpenShift Origin](https://www.openshift.org/) 是建置在 [Kubernetes](https://kubernetes.io/) 上的開放原始碼容器平台。 它可簡化部署、 調整和操作多租用戶應用程式的 hello 程序。 

本指南說明如何在 Azure 虛擬機器使用 toodeploy OpenShift 原點 hello Azure CLI 和 Azure 資源管理員範本。 在本教學課程中，您了解如何：

> [!div class="checklist"]
> * 建立 KeyVault toomanage hello OpenShift 叢集的 SSH 金鑰。
> * 部署 Azure VM 上的 OpenShift 叢集。 
> * 安裝和設定 hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello 叢集。
> * 自訂 hello OpenShift 部署。

如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。

本快速入門需要 hello Azure CLI 版本 2.0.8 或更新版本。 toofind hello 版本，執行`az --version`。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a>登入 tooAzure 
登入 Azure 訂用帳戶以 hello tooyour [az 登入](/cli/azure/#login)命令並遵循螢幕上指示 hello 或按一下**試試**toouse 雲端殼層。

```azurecli 
az login
```
## <a name="create-a-resource-group"></a>建立資源群組

建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。 Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。 

hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置。

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a>建立金鑰保存庫
建立 KeyVault toostore hello hello 叢集的 SSH 金鑰以 hello [az keyvault 建立](/cli/azure/keyvault#create)命令。  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a>建立 SSH 金鑰 
SSH 金鑰是需要的 toosecure 存取 toohello OpenShift 原點叢集。 建立 SSH 金鑰組使用 hello`ssh-keygen`命令。 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> SSH 金鑰組建立 hello 絕不能有複雜密碼。

如需有關在 Windows 中，SSH 金鑰[toocreate SSH Windows 上的索引鍵](/azure/virtual-machines/linux/ssh-from-windows)。

## <a name="store-ssh-private-key-in-key-vault"></a>將 SSH 私密金鑰儲存在 Key Vault 中
hello OpenShift 部署會使用您建立 toosecure 存取 toohello OpenShift master hello SSH 金鑰。 tooenable hello 部署 toosecurely 擷取 hello SSH 金鑰，請將 hello 金鑰儲存在金鑰保存庫使用下列命令的 hello。

# <a name="enabled-for-template-deployment"></a>已針對範本部署啟用
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a>建立服務主體 
OpenShift 會使用使用者名稱與密碼或服務主體與 Azure 進行通訊。 Azure 服務主體是安全性識別，可供您與應用程式、服務及諸如 OpenShift 等自動化工具搭配使用。 您可以控制和定義 hello 權限，如 toowhat 作業 hello 服務主體可以在 Azure 中執行。 透過提供使用者名稱和密碼的 tooimprove 安全性，這個範例會建立基本的服務主體。

建立服務主體與[az ad 預存程序建立-如-rbac](/cli/azure/ad/sp#create-for-rbac)和 OpenShift 需要輸出 hello 認證：

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
記下 hello hello 命令所傳回的 appId 屬性。
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
 > 請勿建立不安全的密碼。  請依照 [Azure AD 密碼規則和限制](/azure/active-directory/active-directory-passwords-policy)指引。

如需有關服務主體的詳細資訊，請參閱[使用 Azure CLI 2.0 建立 Azure 服務主體](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="deploy-hello-openshift-origin-template"></a>部署 hello OpenShift 原始範本
接下來，使用 Azure Resource Manager 範本來部署 Web 應用程式。 

> [!NOTE] 
> hello 下列命令需要 az CLI 2.0.8 或更新版本。 您可以確認 hello az CLI 版本與 hello`az --version`命令。 tooupdate hello CLI 版本，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。

使用 hello`appId`值從您稍早建立的 hello hello 服務主體`aadClientId`參數。

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
hello 部署可能會佔用 too20 分鐘 toocomplete。 hello hello OpenShift 主控台的 URL 和 DNS 名稱的 hello OpenShift 主要被列印 toohello 終端機 hello 部署完成時。

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a>Toohello OpenShift 叢集連線
Hello 部署完成時，將使用 hello 瀏覽器使用 hello toohello OpenShift 主控台連線`OpenShift Console Uri`。 或者，您可以連線使用下列命令的 hello toohello OpenShift master。

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a>清除資源
當不再需要您可以使用 hello [az 群組刪除](/cli/azure/group#delete)命令 tooremove hello 資源群組、 OpenShift 叢集，以及所有相關的資源。

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：
> [!div class="checklist"]
> * 建立 KeyVault toomanage hello OpenShift 叢集的 SSH 金鑰。
> * 部署 Azure VM 上的 OpenShift 叢集。 
> * 安裝和設定 hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello 叢集。

現在您已部署 OpenShift Origin 叢集。 您可以如何依照 OpenShift 教學課程 toolearn toodeploy 第一個應用程式和使用 hello OpenShift 工具。 請參閱[入門 OpenShift 原點](https://docs.openshift.org/latest/getting_started/index.html)tooget 啟動。 
