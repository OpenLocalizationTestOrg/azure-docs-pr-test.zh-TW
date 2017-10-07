---
title: "aaaTroubleshoot SSH 連線問題 tooan Azure VM |Microsoft 文件"
description: "如何 tootroubleshoot 發出例如 'SSH 連線失敗' 或 'SSH 連線被拒' 的 Azure vm 執行 Linux。"
keywords: "ssh 連線被拒, ssh 錯誤, azure ssh, ssh 連線失敗"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a>疑難排解 SSH 連線 tooan Azure Linux VM 失敗，錯誤，或被拒
有各種原因發生安全殼層 (SSH) 錯誤，SSH 連線失敗，或當您嘗試 tooconnect tooa Linux 虛擬機器 (VM) 時，就會拒絕 SSH。 這篇文章可協助您尋找和正確的 hello 問題。 您可以用於 Linux tootroubleshoot hello Azure 入口網站，Azure CLI 或 VM 存取擴充功能，並解決連線問題。

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和堆疊溢位論壇](http://azure.microsoft.com/support/forums/)。 或者，您可以提出 Azure 支援事件。 移 toohello [Azure 支援服務網站](http://azure.microsoft.com/support/options/)選取**取得支援**。 使用 Azure 所支援的相關資訊，請參閱 hello [Microsoft Azure 支援常見問題集](http://azure.microsoft.com/support/faq/)。

## <a name="quick-troubleshooting-steps"></a>快速疑難排解步驟
每個疑難排解的步驟之後，嘗試重新連接 toohello VM。

1. 重設 hello SSH 組態。
2. 重設 hello hello 使用者認證。
3. 確認 hello[網路安全性群組](../../virtual-network/virtual-networks-nsg.md)規則允許 SSH 流量。
   * 請確認網路安全性群組規則存在 toopermit SSH 流量 （依預設，TCP 連接埠 22）。
   * 若未使用 Azure 負載平衡器，則無法使用連接埠重新導向 / 對應功能。
4. 檢查 hello [VM 資源健全狀況](../../resource-health/resource-health-overview.md)。 
   * 請確定該 hello VM 為狀況良好的報表。
   * 如果您有開機診斷功能，請確認 hello VM 未回報開機 hello 記錄檔中的錯誤。
5. 重新啟動 hello VM。
6. 重新部署 hello VM。

如需更詳細的疑難排解步驟與說明，請繼續閱讀。

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a>可用的方法 tootroubleshoot SSH 連線問題
您可以重設認證或使用其中一種下列方法 hello 的 SSH 組態：

* [Azure 入口網站](#use-the-azure-portal)-太好了，如果您需要 tooquickly 重設 hello SSH 組態或 SSH 金鑰，並不 hello Azure tools 安裝。
* [Azure CLI 2.0](#use-the-azure-cli-20) -如果您已經在 hello 命令列，快速地重設 hello SSH 組態或認證。 您也可以使用 hello [Azure CLI 1.0](#use-the-azure-cli-10)
* [Azure VMAccessForLinux 延伸模組](#use-the-vmaccess-extension)-建立和重複使用 json 定義檔案 tooreset hello SSH 組態或使用者認證。

每個疑難排解的步驟之後，請再次嘗試連線 tooyour VM。 如果仍然無法連線，請嘗試 hello 下一個步驟。

## <a name="use-hello-azure-portal"></a>使用 hello Azure 入口網站
hello Azure 入口網站提供快速 tooreset hello SSH 組態或使用者認證不會安裝在本機電腦上的任何工具。

選取您的 VM 中的 hello Azure 入口網站。 捲動 toohello**支援 + 疑難排解**區段，然後選取**重設密碼**如 hello 下列範例所示：

![重設 SSH 組態或 hello Azure 入口網站中的認證](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a>重設 hello SSH 設定
第一個步驟中，選取`Reset configuration only`從 hello**模式**下拉式功能表如在 hello 前面螢幕擷取畫面，然後按一下 [hello**重設**] 按鈕。 完成此動作後，tooaccess VM 再試一次。

### <a name="reset-ssh-credentials-for-a-user"></a>重設使用者的 SSH 認證
tooreset hello 認證之現有的使用者，選取 `Reset SSH public key`或`Reset password`從 hello**模式**下拉式選單，如 hello 前面螢幕擷取畫面所示。 指定 hello 使用者名稱和 SSH 金鑰或新的密碼，然後按一下 [hello**重設**] 按鈕。

您也可以建立具有 sudo hello VM 從這個功能表上的權限的使用者。 輸入新的使用者名稱和相關聯的密碼或 SSH 金鑰，然後按一下hello**重設** 按鈕。

## <a name="use-hello-azure-cli-20"></a>使用 Azure CLI 2.0 hello
如果您還沒有這麼做，安裝 hello 最新[Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 帳戶使用登入和[az 登入](/cli/azure/#login)。

如果您建立及上傳自訂 Linux 磁碟映像時，請確定 hello [Microsoft Azure Linux 代理程式](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)版本 2.0.5 安裝或更新。 若為使用資源庫映像建立的 VM，系統已經為您安裝和設定此存取擴充功能。

### <a name="reset-ssh-configuration"></a>重設 SSH 組態
您一開始可以再試一次重設 hello SSH 組態 toodefault 值和 hello VM 上的重新開機 hello SSH 伺服器。 請注意，這不會變更 hello 使用者帳戶名稱、 密碼或 SSH 金鑰。
hello 下列範例會使用[az vm 使用者重設-ssh](/cli/azure/vm/user#reset-ssh) tooreset hello SSH 組態 hello 名為 VM 上的`myVM`中`myResourceGroup`。 使用您自己的值，如下所示︰

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a>重設使用者的 SSH 認證
hello 下列範例會使用[az vm 的使用者更新](/cli/azure/vm/user#update)tooreset hello 認證`myUsername`toohello 值中指定`myPassword`，hello 名為 VM 上`myVM`中`myResourceGroup`。 使用您自己的值，如下所示︰

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

如果使用 SSH 金鑰驗證，您可以重設 hello SSH 金鑰指定的使用者。 hello 下列範例會使用**az vm 存取設定 linux 使用者**tooupdate hello SSH 金鑰儲存在`~/.ssh/id_rsa.pub`hello 使用者名為`myUsername`，hello 名為 VM 上`myVM`中`myResourceGroup`。 使用您自己的值，如下所示︰

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a>使用 hello VMAccess 擴充功能
hello 適用於 Linux VM 存取延伸模組會定義動作 toocarry 出的 json 檔案中讀取。這些動作包括重設 SSHD、重設 SSH 金鑰，或新增使用者。 您仍然可以使用 hello Azure CLI toocall hello VMAccess 擴充功能，但您可以重複 hello json 檔案使用跨多個 Vm，視。 這種方法可讓您 toocreate 便可以呼叫的特定案例的 json 檔案的儲存機制。

### <a name="reset-sshd"></a>重設 SSHD
建立名為`settings.json`以 hello 下列內容：

```json
{  
    "reset_ssh":"True"
}
```

使用 Azure CLI hello，接著您便呼叫 hello`VMAccessForLinux`延伸 tooreset SSHD 連線藉由指定 json 檔案。 hello 下列範例會使用[az vm 延伸模組集](/cli/azure/vm/extension#set)tooreset SSHD hello 名為 VM 上的`myVM`中`myResourceGroup`。 使用您自己的值，如下所示︰

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a>重設使用者的 SSH 認證
如果 SSHD 正確出現 toofunction，您可以重設 hello 酬謝使用者認證。 tooreset hello 密碼的使用者，建立名為`settings.json`。 hello 下列範例會重設 hello 認證`myUsername`toohello 值中指定`myPassword`。 輸入下列行至 hello 您`settings.json`檔案，使用您自己的值：

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

或 tooreset hello SSH 金鑰的使用者，先建立名為`settings.json`。 hello 下列範例會重設 hello 認證`myUsername`toohello 值中指定`myPassword`，hello 名為 VM 上`myVM`中`myResourceGroup`。 輸入下列行至 hello 您`settings.json`檔案，使用您自己的值：

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

建立 json 檔案之後，使用 hello Azure CLI toocall hello`VMAccessForLinux`延伸 tooreset 藉由指定 json 檔案的 SSH 使用者認證。 hello 下列範例會重設 hello 名為 VM 上的認證`myVM`中`myResourceGroup`。 使用您自己的值，如下所示︰

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a>使用 Azure CLI 1.0 hello
如果您還沒有這麼做，[安裝 hello Azure CLI 1.0，而且連接 tooyour Azure 訂用帳戶](../../cli-install-nodejs.md)。 確定您使用的是 Resource Manager 模式，如下所示：

```azurecli
azure config mode arm
```

如果您建立及上傳自訂 Linux 磁碟映像時，請確定 hello [Microsoft Azure Linux 代理程式](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)版本 2.0.5 安裝或更新。 若為使用資源庫映像建立的 VM，系統已經為您安裝和設定此存取擴充功能。

### <a name="reset-ssh-configuration"></a>重設 SSH 組態
hello SSHD 設定本身可能設定錯誤或 hello 服務發生錯誤。 您可以重設 SSHD toomake 確定本身 hello SSH 組態有效。 重設 SSHD 應該是第一個 hello 您需要疑難排解步驟。

hello 下列範例會重設名為的 VM 上 SSHD `myVM` hello 資源群組中名為`myResourceGroup`。 使用您自己的 VM 和資源群組名稱，如下所示︰

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a>重設使用者的 SSH 認證
如果 SSHD 正確出現 toofunction，您可以重設 hello 酬謝使用者的密碼。 hello 下列範例會重設 hello 認證`myUsername`toohello 值中指定`myPassword`，hello 名為 VM 上`myVM`中`myResourceGroup`。 使用您自己的值，如下所示︰

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

如果使用 SSH 金鑰驗證，您可以重設 hello SSH 金鑰指定的使用者。 下列範例會更新 hello hello SSH 金鑰儲存在`~/.ssh/id_rsa.pub`hello 使用者名為`myUsername`，hello 名為 VM 上`myVM`中`myResourceGroup`。 使用您自己的值，如下所示︰

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a>重新啟動 VM
如果您重設 hello SSH 組態和使用者認證，或發生錯誤，在此情況下，您可以嘗試重新啟動 hello VM tooaddress 基礎計算的問題。

### <a name="azure-portal"></a>Azure 入口網站
VM 使用 toorestart hello Azure 入口網站中，選取您的 VM，然後按一下 hello**重新啟動**按鈕如 hello 下列範例所示：

![在 hello Azure 入口網站中重新啟動 VM](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a>Azure CLI 1.0
下列範例會重新啟動的 hello hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`。 使用您自己的值，如下所示︰

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>Azure CLI 2.0
hello 下列範例會使用[az vm 重新啟動](/cli/azure/vm#restart)toorestart hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`。 使用您自己的值，如下所示︰

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a>重新部署 VM
您可以重新部署 VM tooanother 節點在 Azure 中，這可能會修正任何基礎網路問題。 如需重新部署 VM，請參閱[重新部署 Azure 節點的虛擬機器 toonew](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

> [!NOTE]
> 這項作業完成之後，暫時磁碟資料將會遺失，並將更新與 hello 虛擬機器相關聯的動態 IP 位址。
> 
> 

### <a name="azure-portal"></a>Azure 入口網站
VM 使用 tooredeploy hello Azure 入口網站中，選取，您的 VM 和捲動 toohello**支援 + 疑難排解**> 一節。 按一下 hello**重新部署**按鈕如 hello 下列範例所示：

![重新部署 hello Azure 入口網站中的 VM](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a>Azure CLI 1.0
下列範例重新部署的 hello hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`。 使用您自己的值，如下所示︰

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>Azure CLI 2.0
下列範例會使用 hello [az vm 重新部署](/cli/azure/vm#redeploy)tooredeploy hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`。 使用您自己的值，如下所示︰

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a>使用 hello 傳統部署模型所建立的 Vm
對於使用 hello 傳統部署模型所建立的 Vm，請嘗試這些步驟 tooresolve hello 最常見 SSH 連線失敗。 每個步驟之後，嘗試重新連接 toohello VM。

* 重設遠端存取從 hello [Azure 入口網站](https://portal.azure.com)。 在 hello Azure 入口網站，選取您的 VM，然後按一下 hello**重設遠端...**  按鈕。
* 重新啟動 hello VM。 在 [hello [Azure 入口網站](https://portal.azure.com)，選取您的 VM，然後按一下 hello**重新啟動**] 按鈕。
    
* 重新部署 hello VM tooa 新 Azure 節點。 如需有關資訊 tooredeploy VM，請參閱[重新部署 Azure 節點的虛擬機器 toonew](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
  
    這項作業完成之後，暫時磁碟資料將會遺失，並將更新與 hello 虛擬機器相關聯的動態 IP 位址。
* 請依照下列中的 hello 指示[如何 tooreset 密碼或 SSH Linux 型虛擬機器](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)至：
  
  * 重設 hello 密碼或 SSH 金鑰。
  * 建立 *sudo* 使用者帳戶。
  * 重設 hello SSH 組態。
* 檢查有任何平台問題 hello VM 資源健全狀況。<br>
     選取您的虛擬機器並向下捲動 [設定]  >  [檢查健康狀態]。

## <a name="additional-resources"></a>其他資源
* 如果您仍然無法 tooSSH tooyour VM 之後下列 hello 步驟之後，請參閱[更詳細的疑難排解步驟](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)tooreview 額外步驟 tooresolve 您的問題。
* 如需疑難排解應用程式存取的詳細資訊，請參閱[疑難排解存取 tooan 應用程式在 Azure 虛擬機器上執行](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* 如需有關如何疑難排解使用 hello 傳統部署模型所建立的虛擬機器的詳細資訊，請參閱[如何 tooreset 密碼或 SSH Linux 型虛擬機器](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。

