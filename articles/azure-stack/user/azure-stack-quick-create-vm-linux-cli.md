---
title: "在 Azure Stack 中使用 Azure CLI 來建立 Linux 虛擬機器 | Microsoft Docs"
description: "在 Azure Stack 中使用 CLI 來建立 Linux 虛擬機器。"
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: 21F7D599-1FEC-4827-A5C3-06495C5F53A4
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 09/25/2017
ms.author: mabrigg
ms.custom: mvc
ms.openlocfilehash: ea0bc72c03c7c51f79b838493eb2f6d3efe4f8f7
ms.sourcegitcommit: a5f16c1e2e0573204581c072cf7d237745ff98dc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="create-a-linux-virtual-machine-by-using-azure-cli-in-azure-stack"></a>在 Azure Stack 中使用 Azure CLI 來建立 Linux 虛擬機器

適用於：Azure Stack 整合系統

Azure CLI 可用來從命令列建立和管理 Azure Stack 資源。 本快速入門詳細說明如何使用 Azure CLI 在 Azure Stack 中建立 Linux 虛擬機器。  建立 VM 之後，會安裝 Web 伺服器，並開啟連接埠 80 以允許 Web 流量通過。

## <a name="prerequisites"></a>必要條件 

* 請確定 Azure Stack 操作員已將 “Ubuntu Server 16.04 LTS” 映像新增至 Azure Stack 市集。 

* Azure Stack 需要特定版本的 Azure CLI，才能建立和管理資源。 如果您尚未針對 Azure Stack 設定 Azure CLI，請登入[開發套件](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop)，或登入以 Windows 為基礎的外部用戶端 (如果您[透過 VPN 連線](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)) 並遵循步驟來[安裝和設定 Azure CLI](azure-stack-connect-cli.md)。

* 名稱為 id_rsa.pub 的公開 SSH 金鑰應建立在 Windows 使用者設定檔的 .ssh 目錄中。 如需有關建立 SSH 金鑰的詳細資訊，請參閱[在 Windows 上建立 SSH 金鑰](../../virtual-machines/linux/ssh-from-windows.md)。 

## <a name="create-a-resource-group"></a>建立資源群組

資源群組是在其中部署與管理 Azure Stack 資源的邏輯容器。 從您的開發套件或 Azure Stack 整合系統，執行 [az group create](/cli/azure/group#create) 命令來建立資源群組。 我們已為此文件中的所有變數指派值，您可以使用它們或指派不同的值。 下列範例會在本機位置建立名為 myResourceGroup 的資源群組。

```cli
az group create --name myResourceGroup --location local
```

## <a name="create-a-virtual-machine"></a>建立虛擬機器

使用 [az vm create](/cli/azure/vm#create) 命令來建立 VM。 下列範例會建立名為 myVM 的 VM。 此範例會使用 Demouser 作為系統管理使用者名稱，並使用 Demouser@123 作為密碼。 將這些值更新為適合您環境的值。 連線到虛擬機器連線時需要使用這些值。

```cli
az vm create \
  --resource-group "myResourceGroup" \
  --name "myVM" \
  --image "UbuntuLTS" \
  --admin-username "Demouser" \
  --admin-password "Demouser@123" \
  --use-unmanaged-disk \
  --location local
```

完成之後，命令會輸出您虛擬機器的參數。  請記下 *PublicIPAddress*，因為您將使用此資訊來連線及管理您的虛擬機器。

## <a name="open-port-80-for-web-traffic"></a>針對 Web 流量開啟連接埠 80

依預設只能透過 SSH 連線至 Azure 中部署的 Linux 虛擬機器。 如果此 VM 即將成為 Web 伺服器，您需要從網際網路開啟連接埠 80。 使用 [az vm open-port](/cli/azure/vm#open-port) 命令來開啟所需的連接埠。

```cli
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a>透過 SSH 連線到您的 VM

從已安裝 SSH 的系統，使用下列命令來連線至虛擬機器。 如果使用 Windows，則可使用 [Putty](http://www.putty.org/) 來建立連線。 請務必以虛擬機器的正確公用 IP 位址取代。 在上面的範例中，IP 位址是 192.168.102.36。

```bash
ssh <publicIpAddress>
```

## <a name="install-nginx"></a>安裝 NGINX

使用下列 bash 指令碼來更新套件來源及安裝最新的 NGINX 套件。 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-the-nginx-welcome-page"></a>檢視 NGINX 歡迎使用頁面

安裝 NGINX 後，現在經由網際網路在您的 VM 上開啟連接埠 80 - 您可以使用所選的網頁瀏覽器來檢視預設 NGINX 歡迎使用畫面。 請務必使用您上面記載的 publicIpAddress 來瀏覽預設網頁。 

![預設 NGINX 網站](./media/azure-stack-quick-create-vm-linux-cli/nginx.png) 

## <a name="clean-up-resources"></a>清除資源

若不再需要，您可以使用 [az group delete](/cli/azure/group#delete) 命令來移除資源群組、VM 和所有相關資源。

```cli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>後續步驟

在這個快速入門中，您已部署簡單的 Linux 虛擬機器。 若要深入了解 Azure Stack 虛擬機器，請繼續移至 [Azure Stack 中虛擬機器的考量](azure-stack-vm-considerations.md)。

