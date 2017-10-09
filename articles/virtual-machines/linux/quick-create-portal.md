---
title: "快速入門-aaaAzure 建立 VM 入口網站 |Microsoft 文件"
description: "Azure 快速入門 - 建立 VM 入口網站"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 984a400c976e349a59f873210d6e04bcdea39e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-portal"></a>建立 Linux 虛擬機器以 hello Azure 入口網站

您可以透過 hello Azure 入口網站建立 azure 虛擬機器。 此方法可提供以瀏覽器為基礎的使用者介面，以便建立和設定虛擬機器，以及所有相關的資源。 此快速入門引導您逐步建立虛擬機器和 hello VM 上安裝 web 伺服器。

如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。

## <a name="create-ssh-key-pair"></a>建立 SSH 金鑰組

需要 SSH 金鑰組 toocomplete 本快速入門。 如果現有的 SSH 金鑰組，則可略過此步驟。

從 Bash 殼層中，執行此命令，並遵循螢幕上指示 hello。 hello 命令輸出會包含 hello hello 公開金鑰檔案的檔案名稱。 將複製 hello hello 公開金鑰檔案 toohello 剪貼簿內容。

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="log-in-tooazure"></a>登入 tooAzure 

登入 toohello http://portal.azure.com 在 Azure 入口網站。

## <a name="create-virtual-machine"></a>Create virtual machine

1. 按一下 hello**新增**hello 的左上角 hello Azure 入口網站上找到的按鈕。

2. 選取 [計算]，然後選取 [Ubuntu Server 16.04 LTS]。 

3. 輸入 hello 虛擬機器資訊。 針對 [驗證類型] 選取 [SSH 公開金鑰]。 貼上的 SSH 公開金鑰，格外謹慎 tooremove 任何開頭或尾端泛空白字元。 完成時，按一下 [確定]。

    ![在 hello 入口網站的刀鋒視窗中輸入 VM 的基本資訊](./media/quick-create-portal/create-vm-portal-basic-blade.png)

4. 選取 hello VM 的大小。 多個的大小，選取 toosee**檢視所有**或變更 hello**支援磁碟類型**篩選器。 

    ![顯示 VM 大小的螢幕擷取畫面](./media/quick-create-portal/create-linux-vm-portal-sizes.png)  

5. Hello 設定 刀鋒視窗上保留 hello 預設值，然後按一下**確定**。

6. 在 hello 摘要 頁面上，按一下 **確定**toostart hello 虛擬機器部署。

7. hello VM 將會是已釘選的 toohello Azure 入口網站的儀表板。 Hello 部署完成後，請 hello VM 摘要刀鋒視窗會自動開啟。


## <a name="connect-toovirtual-machine"></a>Toovirtual 機器連線

建立 SSH 連線與 hello 虛擬機器。

1. 按一下 hello**連接**hello 虛擬機器刀鋒視窗上的按鈕。 hello 連接 按鈕會顯示使用的 tooconnect toohello 虛擬機器的 SSH 連接字串。

    ![入口網站 9](./media/quick-create-portal/portal-quick-start-9.png) 

2. Hello 執行的下列命令 toocreate SSH 工作階段。 Hello 以取代連接字串 hello 一個您所複製的 hello Azure 入口網站。

```bash 
ssh azureuser@40.112.21.50
```

## <a name="install-nginx"></a>安裝 NGINX

使用 hello 以下撞指令碼 tooupdate 封裝來源，並安裝最新 NGINX 套件 hello。 

```bash 
#!/bin/bash

# update package source
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

完成之後，結束 hello SSH 工作階段，傳回 hello Azure 入口網站中的 hello VM 屬性。


## <a name="open-port-80-for-web-traffic"></a>針對 Web 流量開啟連接埠 80 

網路安全性群組 (NSG) 可保護輸入和輸出流量。 從 hello Azure 入口網站建立 VM 時，輸入的規則就會建立 SSH 連線的通訊埠 22。 因為此 VM 裝載的網頁伺服器時，NSG 規則需要 toobe 建立的連接埠 80。

1. Hello 虛擬機器上，按一下 hello hello 名稱**資源群組**。
2. 選取 hello**網路安全性群組**。 hello NSG 可以使用來識別 hello**類型**資料行。 
3. 在 hello 左側功能表中，在 設定 上按一下**輸入安全性規則**。
4. 按一下 [新增]。
5. 在 [名稱] 中輸入 **http**。 請確定**連接埠範圍**設定 too80 和**動作**設定得**允許**。 
6. 按一下 [確定] 。


## <a name="view-hello-nginx-welcome-page"></a>檢視 hello NGINX 歡迎使用 頁面

NGINX 安裝，且連接埠 80 開啟 tooyour VM、 hello 網頁伺服器現在可以從 hello 存取網際網路。 開啟網頁瀏覽器，並輸入 hello VM 的 hello 公用 IP 位址。 hello 公用 IP 位址可以找到 hello hello Azure 入口網站中的 VM 刀鋒視窗。

![預設 NGINX 網站](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a>清除資源

當不再需要請刪除 hello 資源群組、 虛擬機器和相關的所有資源。 toodo 因此從 hello 虛擬機器刀鋒視窗中選取 hello 資源群組，然後按一下**刪除**。

## <a name="next-steps"></a>後續步驟

在此快速入門中，您已部署簡單的虛擬機器、網路安全性群組規則，並已安裝 Web 伺服器。 進一步了解 Azure 虛擬機器，toolearn 繼續 toohello 教學課程適用於 Linux Vm。

> [!div class="nextstepaction"]
> [Azure Linux 虛擬機器教學課程](./tutorial-manage-vm.md)
