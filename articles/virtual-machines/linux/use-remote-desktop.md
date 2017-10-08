---
title: "aaaUse 在 Azure 中的 Linux VM 的遠端桌面 tooa |Microsoft 文件"
description: "深入了解如何 tooinstall 並在 Azure 中使用圖形化工具中設定遠端桌面 (xrdp) tooconnect tooa Linux VM"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: iainfou
ms.openlocfilehash: 64d30be101ceeb49fc05bb10293ad63db358efe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a>安裝並在 Azure 中設定遠端桌面 tooconnect tooa Linux VM
在 Azure 中 Linux 虛擬機器 (Vm) 通常是使用安全殼層 (SSH) 連線的 hello 命令列管理。 當新的 tooLinux 或快速疑難排解案例中，遠端桌面的 hello 使用可能會比較容易。 此發行項詳細資料時，如何 tooinstall 及設定使用的桌面環境 ([xfce](https://www.xfce.org)) 和遠端桌面 ([xrdp](http://www.xrdp.org)) Linux vm 使用 hello Resource Manager 部署模型。


## <a name="prerequisites"></a>必要條件
這篇文章需要在 Azure 中有現有的 Linux VM。 如果您需要 toocreate VM，使用下列方法 hello 的其中一個：

- hello [Azure CLI 2.0](quick-create-cli.md)
- hello [Azure 入口網站](quick-create-portal.md)


## <a name="install-a-desktop-environment-on-your-linux-vm"></a>在 Linux VM 上安裝桌面環境
在 Azure 中大多數 Linux VM 預設沒有安裝桌面環境。 Linux VM 通常是使用 SSH 連接來管理，而不是使用桌面環境來管理。 在 Linux 中您有各種不同的桌面環境可以選擇。 根據您選擇的桌面環境中，它可能會取用一個 too2 GB 的磁碟空間，並採取 5 too10 分鐘 tooinstall 和設定所有必要的 hello 封裝。

hello 以下範例會安裝 hello 輕量型[xfce4](https://www.xfce.org/) Ubuntu 虛擬機器上的桌面環境。 針對其他分佈會稍微不同的命令 (使用`yum`tooinstall Red Hat Enterprise Linux 上的並設定適當`selinux`規則或使用`zypper`tooinstall 上 SUSE，例如)。

首先，SSH tooyour VM。 hello 下列範例會連接 toohello 名為 VM *myvm.westus.cloudapp.azure.com*的 hello username *azureuser*:

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

如果您使用 Windows，且需要有關使用 SSH 詳細資訊，請參閱[toouse SSH 與 Windows 的索引鍵](ssh-from-windows.md)。

接下來，使用 `apt` 安裝 xfce，如下所示︰

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a>安裝及設定遠端桌面伺服器
既然您已安裝的桌面環境時，設定連入連線的遠端桌面服務 toolisten。 [xrdp](http://xrdp.org) 是開放原始碼遠端桌面通訊協定 (RDP) 伺服器，適用於大部分的 Linux 散發套件，而且很適合處理 xfce。 在您的 Ubuntu VM 上安裝 xrdp，如下所示：

```bash
sudo apt-get install xrdp
```

當您啟動您的工作階段時告訴 xrdp 哪些桌面環境 toouse。 設定 xrdp toouse xfce 做為您的桌面環境，如下所示：

```bash
echo xfce4-session >~/.xsession
```

重新啟動 hello 變更 tootake 效果 hello xrdp 服務如下：

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a>設定本機使用者帳戶密碼
如果您在建立 VM 時已為您的使用者帳戶建立密碼，請略過此步驟。 如果您只使用 SSH 金鑰驗證，並不需要設定，指定密碼，才能使用 xrdp toolog tooyour VM 中的本機帳戶密碼。 xrdp 無法接受 SSH 金鑰進行驗證。 hello 下列範例會指定 hello 使用者帳戶的密碼*azureuser*:

```bash
sudo passwd azureuser
```

> [!NOTE]
> 如果它目前並不會並指定密碼並不會更新您 SSHD 組態 toopermit 密碼登入。 從安全性觀點來看，您可能想 tooconnect tooyour VM 使用 SSH 通道使用索引鍵為基礎的驗證，並再連接 tooxrdp。 若是如此，請略過下列步驟建立網路安全性群組規則 tooallow 遠端桌面流量 hello。


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a>建立遠端桌面流量的網路安全性群組規則
tooallow 遠端桌面流量 tooreach Linux VM，網路安全性群組規則需要建立 toobe，允許 TCP 連接埠 3389 tooreach 上的 VM。 如需有關網路安全性群組規則的詳細資訊，請參閱[什麼是網路安全性群組？](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 您也可以[使用 hello Azure 入口網站 toocreate 網路安全性群組規則](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

hello 下列範例會建立網路安全性群組規則與[az 網路 nsg 規則建立](/cli/azure/network/nsg/rule#create)名為*myNetworkSecurityGroupRule*太*允許*上的流量*tcp*連接埠*3389*。

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a>連接 Linux VM 與遠端桌面用戶端
開啟您本機的遠端桌面用戶端，並連接 toohello IP 位址或 Linux VM 的 DNS 名稱。 Hello 使用者名稱和密碼 hello 使用者帳戶上輸入您的 VM，如下所示：

![連接 tooxrdp 使用您的遠端桌面用戶端](./media/use-remote-desktop/remote-desktop-client.png)

驗證之後，將會載入 hello xfce 桌面環境，並將其看起來類似下列範例的 toohello 中：

![透過 xrdp 的 xfce 桌面環境](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a>疑難排解
如果您無法連接 tooyour 使用遠端桌面用戶端的 Linux VM，使用`netstat`您 Linux VM tooverify，如下所示接聽 RDP 連線您的 VM 上：

```bash
sudo netstat -plnt | grep rdp
```

下列範例所示的 hello hello 接聽 TCP 連接埠 3389，如預期般的 VM:

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

如果 hello xrdp 服務沒有在接聽，Ubuntu 虛擬機器上重新啟動 hello 服務，如下所示：

```bash
sudo service xrdp restart
```

檢閱記錄檔*/var/記錄*群惡棍為 toowhy hello 服務的指示 Ubuntu VM 上可能沒有回應。 您也可以監視 hello syslog 遠端桌面連線嘗試 tooview 期間的任何錯誤：

```bash
tail -f /var/log/syslog
```

其他 Linux 散發套件，例如 Red Hat Enterprise Linux 和 SUSE 可能會有不同的方式 toorestart 服務和其他記錄檔位置 tooreview。

如果您不在您的遠端桌面用戶端會收到任何回應，並不會看到 hello 系統記錄檔中的任何事件，這種行為表示遠端桌面流量無法連線到 hello VM。 檢閱您所規則 toopermit TCP 連接埠 3389 上您網路安全性群組規則 tooensure。 如需詳細資訊，請參閱[針對應用程式連線能力問題進行疑難排解](../windows/troubleshoot-app-connection.md)。


## <a name="next-steps"></a>後續步驟
如需有關建立和使用 SSH 金鑰與 Linux VM 的詳細資訊，請參閱[在 Azure 中為 Linux VM 建立 SSH 金鑰](mac-create-ssh-keys.md)。

如需從 Windows 使用 SSH 資訊，請參閱[toouse SSH 與 Windows 的索引鍵](ssh-from-windows.md)。

