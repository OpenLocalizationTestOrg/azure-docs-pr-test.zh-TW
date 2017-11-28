---
title: "在 Azure 中的 VHD Debian Linux aaaPrepare |Microsoft 文件"
description: "了解如何 toocreate Debian 7 和 8 的 VHD 檔案部署在 Azure 中。"
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: a6de7a7c-cc70-44e7-aed0-2ae6884d401a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: e67d126de3db146357a6509aedb5f478576768f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a><span data-ttu-id="5cad3-103">準備適用於 Azure 的 Debian VHD</span><span class="sxs-lookup"><span data-stu-id="5cad3-103">Prepare a Debian VHD for Azure</span></span>
## <a name="prerequisites"></a><span data-ttu-id="5cad3-104">必要條件</span><span class="sxs-lookup"><span data-stu-id="5cad3-104">Prerequisites</span></span>
<span data-ttu-id="5cad3-105">本節假設您已經有安裝 Debian Linux 作業系統從.iso 檔案從 hello 下載[Debian 網站](https://www.debian.org/distrib/)tooa 虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="5cad3-105">This section assumes that you have already installed a Debian Linux operating system from an .iso file downloaded from hello [Debian website](https://www.debian.org/distrib/) tooa virtual hard disk.</span></span> <span data-ttu-id="5cad3-106">多個工具存在 toocreate.vhd 檔案。HYPER-V 是一個範例。</span><span class="sxs-lookup"><span data-stu-id="5cad3-106">Multiple tools exist toocreate .vhd files; Hyper-V is only one example.</span></span> <span data-ttu-id="5cad3-107">使用 HYPER-V 的指示，請參閱[安裝 hello HYPER-V 角色和設定虛擬機器](https://technet.microsoft.com/library/hh846766.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5cad3-107">For instructions using Hyper-V, see [Install hello Hyper-V Role and Configure a Virtual Machine](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

## <a name="installation-notes"></a><span data-ttu-id="5cad3-108">安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="5cad3-108">Installation notes</span></span>
* <span data-ttu-id="5cad3-109">另請參閱[一般 Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes)，了解為 Azure 準備 Linux 的更多祕訣。</span><span class="sxs-lookup"><span data-stu-id="5cad3-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="5cad3-110">在 Azure 中不支援 hello 較新的 VHDX 格式。</span><span class="sxs-lookup"><span data-stu-id="5cad3-110">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="5cad3-111">您可以將轉換 hello 磁碟 tooVHD 格式使用 HYPER-V 管理員] 或 [hello**轉換-vhd** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5cad3-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello **convert-vhd** cmdlet.</span></span>
* <span data-ttu-id="5cad3-112">當安裝 hello Linux 系統建議您使用標準的資料分割，而非 LVM （通常 hello 預設值為許多安裝）。</span><span class="sxs-lookup"><span data-stu-id="5cad3-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="5cad3-113">特別是當作業系統磁碟曾經需要附加 toobe tooanother VM 進行疑難排解，這樣可避免與複製 Vm，LVM 名稱衝突。</span><span class="sxs-lookup"><span data-stu-id="5cad3-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="5cad3-114">如果願意，您可以在資料磁碟上使用 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5cad3-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="5cad3-115">請勿設定 hello OS 磁碟交換資料分割。</span><span class="sxs-lookup"><span data-stu-id="5cad3-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="5cad3-116">hello Azure Linux 代理程式可以設定的 toocreate 交換磁碟上的檔案 hello 暫存資源。</span><span class="sxs-lookup"><span data-stu-id="5cad3-116">hello Azure Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="5cad3-117">相關資訊位於下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="5cad3-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="5cad3-118">所有 hello Vhd 必須是 1 MB 的倍數的大小。</span><span class="sxs-lookup"><span data-stu-id="5cad3-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-azure-manage-toocreate-debian-vhds"></a><span data-ttu-id="5cad3-119">使用 Azure 管理 toocreate Debian Vhd</span><span class="sxs-lookup"><span data-stu-id="5cad3-119">Use Azure-Manage toocreate Debian VHDs</span></span>
<span data-ttu-id="5cad3-120">有工具可用於產生 Debian Vhd azure，例如 hello [azure-管理](https://github.com/credativ/azure-manage)指令碼從[credativ](http://www.credativ.com/)。</span><span class="sxs-lookup"><span data-stu-id="5cad3-120">There are tools available for generating Debian VHDs for Azure, such as hello [azure-manage](https://github.com/credativ/azure-manage) scripts from [credativ](http://www.credativ.com/).</span></span> <span data-ttu-id="5cad3-121">這是建議的方法與從頭開始建立映像的 hello。</span><span class="sxs-lookup"><span data-stu-id="5cad3-121">This is hello recommended approach versus creating an image from scratch.</span></span> <span data-ttu-id="5cad3-122">例如，toocreate Debian 8 VHD 執行 hello 遵循 toodownload azure 管理的命令 （和相依性），然後執行 hello azure_build_image 指令碼：</span><span class="sxs-lookup"><span data-stu-id="5cad3-122">For example, toocreate a Debian 8 VHD run hello following commands toodownload azure-manage (and dependencies) and run hello azure_build_image script:</span></span>

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a><span data-ttu-id="5cad3-123">手動準備 Debian VHD</span><span class="sxs-lookup"><span data-stu-id="5cad3-123">Manually prepare a Debian VHD</span></span>
1. <span data-ttu-id="5cad3-124">在 HYPER-V 管理員 中，選取 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5cad3-124">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="5cad3-125">按一下**連接**tooopen hello 虛擬機器的主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="5cad3-125">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="5cad3-126">註解 hello 列**deb cdrom**中`/etc/apt/source.list`如果您設定 hello VM 根據 ISO 檔案。</span><span class="sxs-lookup"><span data-stu-id="5cad3-126">Comment out hello line for **deb cdrom** in `/etc/apt/source.list` if you set up hello VM against an ISO file.</span></span>
4. <span data-ttu-id="5cad3-127">編輯 hello`/etc/default/grub`檔案，並修改 hello **GRUB_CMDLINE_LINUX**如下 tooinclude 其他核心參數適用於 Azure 的參數。</span><span class="sxs-lookup"><span data-stu-id="5cad3-127">Edit hello `/etc/default/grub` file and modify hello **GRUB_CMDLINE_LINUX** parameter as follows tooinclude additional kernel parameters for Azure.</span></span>
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. <span data-ttu-id="5cad3-128">重建 hello 幼蟲並執行：</span><span class="sxs-lookup"><span data-stu-id="5cad3-128">Rebuild hello grub and run:</span></span>
   
        # sudo update-grub
6. <span data-ttu-id="5cad3-129">新增 Debian 的 Azure 儲存機制 too/etc/apt/sources.list Debian 7 或 8:</span><span class="sxs-lookup"><span data-stu-id="5cad3-129">Add Debian's Azure repositories too/etc/apt/sources.list for either Debian 7 or 8:</span></span>
   
    <span data-ttu-id="5cad3-130">**Debian 7.x "Wheezy"**</span><span class="sxs-lookup"><span data-stu-id="5cad3-130">**Debian 7.x "Wheezy"**</span></span>
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    <span data-ttu-id="5cad3-131">**Debian 8.x "Jessie"**</span><span class="sxs-lookup"><span data-stu-id="5cad3-131">**Debian 8.x "Jessie"**</span></span>

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. <span data-ttu-id="5cad3-132">安裝 hello Azure Linux 代理程式：</span><span class="sxs-lookup"><span data-stu-id="5cad3-132">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. <span data-ttu-id="5cad3-133">Debian 7，則是必要的 toorun hello 3.16 基礎核心 hello wheezy backports 儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="5cad3-133">For Debian 7, it is required toorun hello 3.16-based kernel from hello wheezy-backports repository.</span></span> <span data-ttu-id="5cad3-134">先建立檔案，稱為 /etc/apt/preferences.d/linux.pref 以 hello 下列內容：</span><span class="sxs-lookup"><span data-stu-id="5cad3-134">First create a file called /etc/apt/preferences.d/linux.pref with hello following contents:</span></span>
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    <span data-ttu-id="5cad3-135">然後，執行 sudo apt get 安裝 linux-映像-amd64 」 tooinstall hello 新的核心。</span><span class="sxs-lookup"><span data-stu-id="5cad3-135">Then run "sudo apt-get install linux-image-amd64" tooinstall hello new kernel.</span></span>
3. <span data-ttu-id="5cad3-136">取消佈建 hello 虛擬機器並準備在 Azure 上佈建，然後執行：</span><span class="sxs-lookup"><span data-stu-id="5cad3-136">Deprovision hello virtual machine and prepare it for provisioning on Azure and run:</span></span>
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. <span data-ttu-id="5cad3-137">在 Hyper-V 管理員中，依序按一下 [動作] -> [關閉]。</span><span class="sxs-lookup"><span data-stu-id="5cad3-137">Click **Action** -> Shut Down in Hyper-V Manager.</span></span> <span data-ttu-id="5cad3-138">Linux VHD 是現在準備好 toobe 上傳 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="5cad3-138">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cad3-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5cad3-139">Next steps</span></span>
<span data-ttu-id="5cad3-140">您要現在準備好 toouse Debian 虛擬硬碟 toocreate 新虛擬機器在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="5cad3-140">You're now ready toouse your Debian virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="5cad3-141">如果這是 hello 正在上傳 hello.vhd 檔案 tooAzure 的第一次，請參閱步驟 2 和 3 中的[建立和上傳包含 hello Linux 作業系統的虛擬硬碟](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5cad3-141">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

