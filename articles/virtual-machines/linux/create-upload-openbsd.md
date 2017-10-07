---
title: "aaaCreate 和上傳 OpenBSD VM 映像 tooAzure |Microsoft 文件"
description: "了解 toocreate 和上傳虛擬硬碟 (VHD)，其中包含 hello OpenBSD 作業系統 toocreate Azure CLI 透過 Azure 虛擬機器"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: kyliel
ms.openlocfilehash: 0524f45ea1ecec37e55cbe9d54438a571a831de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a>建立及上傳 OpenBSD 磁碟映像 tooAzure
本文章將示範如何 toocreate 和上傳虛擬硬碟 (VHD)，其中包含 hello OpenBSD 作業系統。 將它上傳之後，您可以為您自己的映像 toocreate Azure CLI 透過 Azure 中的虛擬機器 (VM) 使用它。


## <a name="prerequisites"></a>必要條件
本文假設您有下列項目 hello:

* **Azure 訂用帳戶** - 如果您沒有，只需要幾分鐘的時間就可以建立帳戶。 如果您有 MSDN 訂用帳戶，請參閱 [Visual Studio 訂閱者的每月 Azure 點數](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)。 否則，了解如何太[建立免費的試用帳戶](https://azure.microsoft.com/pricing/free-trial/)。  
* **Azure CLI 2.0** -請確定您有最新的 hello [Azure CLI 2.0](/cli/azure/install-azure-cli)安裝並登入 tooyour Azure 帳戶[az 登入](/cli/azure/#login)。
* **安裝中的.vhd 檔案的 OpenBSD 作業系統**-支援的 OpenBSD 作業系統 （6.1 版） 必須是已安裝的 tooa 虛擬硬碟。 多個工具存在 toocreate.vhd 檔案。 例如，您可以使用的虛擬化解決方案，例如 HYPER-V toocreate hello.vhd 檔案，並安裝 hello 作業系統。 如需有關如何 tooinstall 並使用 HYPER-V，請參閱指示[安裝 HYPER-V 並建立虛擬機器](http://technet.microsoft.com/library/hh846766.aspx)。


## <a name="prepare-openbsd-image-for-azure"></a>為 Azure 準備 OpenBSD 映像
Hello 安裝 hello OpenBSD 作業系統 6.1，加入 HYPER-V 支援，這些 VM 上完成下列程序的 hello:

1. 如果在安裝期間未啟用 DHCP，啟用 hello 服務，如下所示：

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. 設定序列主控台，如下所示：

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. 設定套件安裝，如下所示：

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. 根據預設，hello`root`在 Azure 中的虛擬機器上停用使用者。 使用者可以執行使用更高權限命令使用 hello `doas` OpenBSD VM 上的命令。 Doas 預設為啟用狀態。 如需詳細資訊，請參閱 [doas.conf](http://man.openbsd.org/doas.conf.5)。 

5. 安裝和設定 hello Azure 代理程式的必要條件，如下所示：

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. hello 的 hello Azure 代理程式的最新版本能找到上[Github](https://github.com/Azure/WALinuxAgent/releases)。 Hello 代理程式安裝，如下所示：

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > 安裝 Azure 代理程式之後，它是個不錯的主意 tooverify 執行，如下所示：
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. 取消佈建 hello 系統 tooclean，並讓它適用於重新佈建。 hello 下列命令也會刪除 hello 最後一個佈建的使用者帳戶和相關聯的 hello 資料：

    ```sh
    waagent -deprovision+user -force
    ```

現在您可以關閉您的 VM。


## <a name="prepare-hello-vhd"></a>準備 hello VHD
hello VHDX 格式不支援在 Azure 中，只有**固定 VHD**。 您可以將轉換使用 HYPER-V 管理員的 hello 磁碟 toofixed VHD 格式或 hello Powershell[轉換-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet。 範例如下。

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a>建立儲存體資源並上傳
首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。 hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：

```azurecli
az group create --name myResourceGroup --location eastus
```

tooupload 您的 VHD 建立的儲存體帳戶[az 儲存體帳戶建立](/cli/azure/storage/account#create)。 儲存體帳戶名稱必須是唯一的，因此請提供您自己的名稱。 hello 下列範例會建立名為的儲存體帳戶*mystorageaccount*:

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

toocontrol 存取 toohello 儲存體帳戶，取得與 hello 儲存體金鑰[az 儲存體帳戶金鑰清單](/cli/azure/storage/account/keys#list)，如下所示：

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

toologically 個別 hello Vhd 上傳，建立 hello 儲存體帳戶內的容器[az 儲存體容器建立](/cli/azure/storage/container#create):

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

最後，使用 [az storage blob upload](/cli/azure/storage/blob#upload) 上傳 VHD，如下所示：

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a>從 VHD 建立 VM
您可以使用[範例指令碼](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) 或直接使用 [az vm create](/cli/azure/vm#create) 建立 VM。 toospecify hello OpenBSD VHD 您上傳，使用 hello`--image`參數，如下所示：

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

取得 hello IP 位址與 OpenBSD vm [az vm 清單 ip 位址](/cli/azure/vm#list-ip-addresses)，如下所示：

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

現在您可以像平常一樣 SSH tooyour OpenBSD VM:
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a>後續步驟
如果您想的 tooknow 支援 OpenBSD6.1 的 HYPER-V 有關的詳細資訊，請閱讀[OpenBSD 6.1](https://www.openbsd.org/61.html)和[hyperv.4](http://man.openbsd.org/hyperv.4)。

如果您想 toocreate 從受管理磁碟 VM，請閱讀[az 磁碟](/cli/azure/disk)。 
