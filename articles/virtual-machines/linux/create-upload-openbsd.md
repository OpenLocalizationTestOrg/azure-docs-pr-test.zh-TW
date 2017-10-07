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
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a><span data-ttu-id="d31ce-103">建立及上傳 OpenBSD 磁碟映像 tooAzure</span><span class="sxs-lookup"><span data-stu-id="d31ce-103">Create and Upload an OpenBSD disk image tooAzure</span></span>
<span data-ttu-id="d31ce-104">本文章將示範如何 toocreate 和上傳虛擬硬碟 (VHD)，其中包含 hello OpenBSD 作業系統。</span><span class="sxs-lookup"><span data-stu-id="d31ce-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello OpenBSD operating system.</span></span> <span data-ttu-id="d31ce-105">將它上傳之後，您可以為您自己的映像 toocreate Azure CLI 透過 Azure 中的虛擬機器 (VM) 使用它。</span><span class="sxs-lookup"><span data-stu-id="d31ce-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure through Azure CLI.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d31ce-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="d31ce-106">Prerequisites</span></span>
<span data-ttu-id="d31ce-107">本文假設您有下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="d31ce-107">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="d31ce-108">**Azure 訂用帳戶** - 如果您沒有，只需要幾分鐘的時間就可以建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="d31ce-108">**An Azure subscription** - If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="d31ce-109">如果您有 MSDN 訂用帳戶，請參閱 [Visual Studio 訂閱者的每月 Azure 點數](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)。</span><span class="sxs-lookup"><span data-stu-id="d31ce-109">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="d31ce-110">否則，了解如何太[建立免費的試用帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="d31ce-110">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="d31ce-111">**Azure CLI 2.0** -請確定您有最新的 hello [Azure CLI 2.0](/cli/azure/install-azure-cli)安裝並登入 tooyour Azure 帳戶[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="d31ce-111">**Azure CLI 2.0** - Make sure you have hello latest [Azure CLI 2.0](/cli/azure/install-azure-cli) installed and logged in tooyour Azure account with [az login](/cli/azure/#login).</span></span>
* <span data-ttu-id="d31ce-112">**安裝中的.vhd 檔案的 OpenBSD 作業系統**-支援的 OpenBSD 作業系統 （6.1 版） 必須是已安裝的 tooa 虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="d31ce-112">**OpenBSD operating system installed in a .vhd file** - A supported OpenBSD operating system (6.1 version) must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="d31ce-113">多個工具存在 toocreate.vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="d31ce-113">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="d31ce-114">例如，您可以使用的虛擬化解決方案，例如 HYPER-V toocreate hello.vhd 檔案，並安裝 hello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="d31ce-114">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="d31ce-115">如需有關如何 tooinstall 並使用 HYPER-V，請參閱指示[安裝 HYPER-V 並建立虛擬機器](http://technet.microsoft.com/library/hh846766.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d31ce-115">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>


## <a name="prepare-openbsd-image-for-azure"></a><span data-ttu-id="d31ce-116">為 Azure 準備 OpenBSD 映像</span><span class="sxs-lookup"><span data-stu-id="d31ce-116">Prepare OpenBSD image for Azure</span></span>
<span data-ttu-id="d31ce-117">Hello 安裝 hello OpenBSD 作業系統 6.1，加入 HYPER-V 支援，這些 VM 上完成下列程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="d31ce-117">On hello VM where you installed hello OpenBSD operating system 6.1, which added Hyper-V support, complete hello following procedures:</span></span>

1. <span data-ttu-id="d31ce-118">如果在安裝期間未啟用 DHCP，啟用 hello 服務，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d31ce-118">If DHCP is not enabled during installation, enable hello service as follows:</span></span>

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. <span data-ttu-id="d31ce-119">設定序列主控台，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d31ce-119">Set up a serial console as follows:</span></span>

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. <span data-ttu-id="d31ce-120">設定套件安裝，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d31ce-120">Configure Package installation as follows:</span></span>

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. <span data-ttu-id="d31ce-121">根據預設，hello`root`在 Azure 中的虛擬機器上停用使用者。</span><span class="sxs-lookup"><span data-stu-id="d31ce-121">By default, hello `root` user is disabled on virtual machines in Azure.</span></span> <span data-ttu-id="d31ce-122">使用者可以執行使用更高權限命令使用 hello `doas` OpenBSD VM 上的命令。</span><span class="sxs-lookup"><span data-stu-id="d31ce-122">Users can run commands with elevated privileges by using hello `doas` command on OpenBSD VM.</span></span> <span data-ttu-id="d31ce-123">Doas 預設為啟用狀態。</span><span class="sxs-lookup"><span data-stu-id="d31ce-123">Doas is enabled by default.</span></span> <span data-ttu-id="d31ce-124">如需詳細資訊，請參閱 [doas.conf](http://man.openbsd.org/doas.conf.5)。</span><span class="sxs-lookup"><span data-stu-id="d31ce-124">For more information, see [doas.conf](http://man.openbsd.org/doas.conf.5).</span></span> 

5. <span data-ttu-id="d31ce-125">安裝和設定 hello Azure 代理程式的必要條件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d31ce-125">Install and configure prerequisites for hello Azure Agent as follows:</span></span>

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. <span data-ttu-id="d31ce-126">hello 的 hello Azure 代理程式的最新版本能找到上[Github](https://github.com/Azure/WALinuxAgent/releases)。</span><span class="sxs-lookup"><span data-stu-id="d31ce-126">hello latest release of hello Azure agent can always be found on [Github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="d31ce-127">Hello 代理程式安裝，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d31ce-127">Install hello agent as follows:</span></span>

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="d31ce-128">安裝 Azure 代理程式之後，它是個不錯的主意 tooverify 執行，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d31ce-128">After you install Azure Agent, it's a good idea tooverify that it's running as follows:</span></span>
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. <span data-ttu-id="d31ce-129">取消佈建 hello 系統 tooclean，並讓它適用於重新佈建。</span><span class="sxs-lookup"><span data-stu-id="d31ce-129">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="d31ce-130">hello 下列命令也會刪除 hello 最後一個佈建的使用者帳戶和相關聯的 hello 資料：</span><span class="sxs-lookup"><span data-stu-id="d31ce-130">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

    ```sh
    waagent -deprovision+user -force
    ```

<span data-ttu-id="d31ce-131">現在您可以關閉您的 VM。</span><span class="sxs-lookup"><span data-stu-id="d31ce-131">Now you can shut down your VM.</span></span>


## <a name="prepare-hello-vhd"></a><span data-ttu-id="d31ce-132">準備 hello VHD</span><span class="sxs-lookup"><span data-stu-id="d31ce-132">Prepare hello VHD</span></span>
<span data-ttu-id="d31ce-133">hello VHDX 格式不支援在 Azure 中，只有**固定 VHD**。</span><span class="sxs-lookup"><span data-stu-id="d31ce-133">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span> <span data-ttu-id="d31ce-134">您可以將轉換使用 HYPER-V 管理員的 hello 磁碟 toofixed VHD 格式或 hello Powershell[轉換-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d31ce-134">You can convert hello disk toofixed VHD format using Hyper-V Manager or hello Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span></span> <span data-ttu-id="d31ce-135">範例如下。</span><span class="sxs-lookup"><span data-stu-id="d31ce-135">An example is as following.</span></span>

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a><span data-ttu-id="d31ce-136">建立儲存體資源並上傳</span><span class="sxs-lookup"><span data-stu-id="d31ce-136">Create storage resources and upload</span></span>
<span data-ttu-id="d31ce-137">首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="d31ce-137">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="d31ce-138">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：</span><span class="sxs-lookup"><span data-stu-id="d31ce-138">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="d31ce-139">tooupload 您的 VHD 建立的儲存體帳戶[az 儲存體帳戶建立](/cli/azure/storage/account#create)。</span><span class="sxs-lookup"><span data-stu-id="d31ce-139">tooupload your VHD, create a storage account with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="d31ce-140">儲存體帳戶名稱必須是唯一的，因此請提供您自己的名稱。</span><span class="sxs-lookup"><span data-stu-id="d31ce-140">Storage account names must be unique, so provide your own name.</span></span> <span data-ttu-id="d31ce-141">hello 下列範例會建立名為的儲存體帳戶*mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="d31ce-141">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

<span data-ttu-id="d31ce-142">toocontrol 存取 toohello 儲存體帳戶，取得與 hello 儲存體金鑰[az 儲存體帳戶金鑰清單](/cli/azure/storage/account/keys#list)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d31ce-142">toocontrol access toohello storage account, obtain hello storage key with [az storage account keys list](/cli/azure/storage/account/keys#list) as follows:</span></span>

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

<span data-ttu-id="d31ce-143">toologically 個別 hello Vhd 上傳，建立 hello 儲存體帳戶內的容器[az 儲存體容器建立](/cli/azure/storage/container#create):</span><span class="sxs-lookup"><span data-stu-id="d31ce-143">toologically separate hello VHDs you upload, create a container within hello storage account with [az storage container create](/cli/azure/storage/container#create):</span></span>

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

<span data-ttu-id="d31ce-144">最後，使用 [az storage blob upload](/cli/azure/storage/blob#upload) 上傳 VHD，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d31ce-144">Finally, upload your VHD with [az storage blob upload](/cli/azure/storage/blob#upload) as follows:</span></span>

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a><span data-ttu-id="d31ce-145">從 VHD 建立 VM</span><span class="sxs-lookup"><span data-stu-id="d31ce-145">Create VM from your VHD</span></span>
<span data-ttu-id="d31ce-146">您可以使用[範例指令碼](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) 或直接使用 [az vm create](/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="d31ce-146">You can create a VM with a [sample script](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) or directly with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="d31ce-147">toospecify hello OpenBSD VHD 您上傳，使用 hello`--image`參數，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d31ce-147">toospecify hello OpenBSD VHD you uploaded, use hello `--image` parameter as follows:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="d31ce-148">取得 hello IP 位址與 OpenBSD vm [az vm 清單 ip 位址](/cli/azure/vm#list-ip-addresses)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d31ce-148">Obtain hello IP address for your OpenBSD VM with [az vm list-ip-addresses](/cli/azure/vm#list-ip-addresses) as follows:</span></span>

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

<span data-ttu-id="d31ce-149">現在您可以像平常一樣 SSH tooyour OpenBSD VM:</span><span class="sxs-lookup"><span data-stu-id="d31ce-149">Now you can SSH tooyour OpenBSD VM as normal:</span></span>
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a><span data-ttu-id="d31ce-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d31ce-150">Next steps</span></span>
<span data-ttu-id="d31ce-151">如果您想的 tooknow 支援 OpenBSD6.1 的 HYPER-V 有關的詳細資訊，請閱讀[OpenBSD 6.1](https://www.openbsd.org/61.html)和[hyperv.4](http://man.openbsd.org/hyperv.4)。</span><span class="sxs-lookup"><span data-stu-id="d31ce-151">If you want tooknow more about Hyper-V support on OpenBSD6.1, read [OpenBSD 6.1](https://www.openbsd.org/61.html) and [hyperv.4](http://man.openbsd.org/hyperv.4).</span></span>

<span data-ttu-id="d31ce-152">如果您想 toocreate 從受管理磁碟 VM，請閱讀[az 磁碟](/cli/azure/disk)。</span><span class="sxs-lookup"><span data-stu-id="d31ce-152">If you want toocreate a VM from managed disk, read [az disk](/cli/azure/disk).</span></span> 
