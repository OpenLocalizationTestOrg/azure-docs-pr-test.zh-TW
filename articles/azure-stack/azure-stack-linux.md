---
title: "Azure 堆疊上的 aaaLinux 遊客 |Microsoft 文件"
description: "了解如何在 Azure Stack 上建立 Linux 式虛擬機器。"
services: azure-stack
documentationcenter: 
author: anjayajodha
manager: byronr
editor: 
ms.assetid: d2155c59-902e-4f63-ac58-d19e6a765380
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: anajod
ms.openlocfilehash: 225bed7d630b676ca760add25731e347516b5bf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-linux-virtual-machines-on-azure-stack"></a><span data-ttu-id="8afa1-103">在 Azure Stack 上部署 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="8afa1-103">Deploy Linux virtual machines on Azure Stack</span></span>
<span data-ttu-id="8afa1-104">您可以將以 Linux 為基礎的映像新增至 hello Marketplace</堆疊部署 Linux 虛擬機器上 hello Azure 堆疊開發套件。</span><span class="sxs-lookup"><span data-stu-id="8afa1-104">You can deploy Linux virtual machines on hello Azure Stack Development Kit by adding a Linux-based image into hello Azure Stack Marketplace.</span></span> <span data-ttu-id="8afa1-105">已有數個 Linux 廠商提供可新增到 Azure Stack 開發套件中的映像，您也可以建立自己的映像。</span><span class="sxs-lookup"><span data-stu-id="8afa1-105">Several Linux vendors have provided images that can be added into an Azure Stack Development Kit or you can build your own.</span></span>

## <a name="download-an-image"></a><span data-ttu-id="8afa1-106">下載映像</span><span class="sxs-lookup"><span data-stu-id="8afa1-106">Download an image</span></span>
1. <span data-ttu-id="8afa1-107">從下列連結，hello 擷取 Azure 堆疊相容映像或準備您自己和 下載：</span><span class="sxs-lookup"><span data-stu-id="8afa1-107">Download and extract an Azure Stack-compatible image from hello following links, or prepare your own:</span></span>
   
   * [<span data-ttu-id="8afa1-108">Bitnami</span><span class="sxs-lookup"><span data-stu-id="8afa1-108">Bitnami</span></span>](https://bitnami.com/azure-stack)
   * [<span data-ttu-id="8afa1-109">CentOS</span><span class="sxs-lookup"><span data-stu-id="8afa1-109">CentOS</span></span>](http://olstacks.cloudapp.net/latest/)
   * [<span data-ttu-id="8afa1-110">CoreOS</span><span class="sxs-lookup"><span data-stu-id="8afa1-110">CoreOS</span></span>](https://stable.release.core-os.net/amd64-usr/current/coreos_production_azure_image.vhd.bz2)
   * [<span data-ttu-id="8afa1-111">SuSE</span><span class="sxs-lookup"><span data-stu-id="8afa1-111">SuSE</span></span>](https://download.suse.com/Download?buildid=VCFi7y7MsFQ~)
   * <span data-ttu-id="8afa1-112">[Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="8afa1-112">[Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
2. <span data-ttu-id="8afa1-113">如有必要，請解壓縮 hello 映像 VHD 和[新增 hello 映像 toohello Marketplace](azure-stack-add-vm-image.md)。</span><span class="sxs-lookup"><span data-stu-id="8afa1-113">Extract hello image VHD if necessary and [add hello image toohello Marketplace](azure-stack-add-vm-image.md).</span></span> <span data-ttu-id="8afa1-114">請確定該 hello`OSType`參數設定太`Linux`。</span><span class="sxs-lookup"><span data-stu-id="8afa1-114">Make sure that hello `OSType` parameter is set too`Linux`.</span></span>
3. <span data-ttu-id="8afa1-115">您加入 hello 映像 toohello Marketplace 之後，建立 Marketplace 項目，而且您可以部署 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8afa1-115">After you've added hello image toohello Marketplace, a Marketplace item is created and you can deploy a Linux virtual machine.</span></span>

## <a name="prepare-your-own-image"></a><span data-ttu-id="8afa1-116">準備您自己的映像</span><span class="sxs-lookup"><span data-stu-id="8afa1-116">Prepare your own image</span></span>
1. <span data-ttu-id="8afa1-117">準備您自己使用其中一種 hello 下列指示的 Linux 映像：</span><span class="sxs-lookup"><span data-stu-id="8afa1-117">Prepare your own Linux image using one of hello following instructions:</span></span>
   
   * [<span data-ttu-id="8afa1-118">CentOS 型發行版本</span><span class="sxs-lookup"><span data-stu-id="8afa1-118">CentOS-based Distributions</span></span>](../virtual-machines/linux/create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="8afa1-119">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="8afa1-119">Debian Linux</span></span>](../virtual-machines/linux/debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="8afa1-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="8afa1-120">Oracle Linux</span></span>](../virtual-machines/linux/oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="8afa1-121">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="8afa1-121">Red Hat Enterprise Linux</span></span>](../virtual-machines/linux/redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="8afa1-122">SLES 和 openSUSE</span><span class="sxs-lookup"><span data-stu-id="8afa1-122">SLES & openSUSE</span></span>](../virtual-machines/linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="8afa1-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="8afa1-123">Ubuntu</span></span>](../virtual-machines/linux/create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="8afa1-124">下載並安裝 hello [Azure Linux 代理程式](https://github.com/Azure/WALinuxAgent/)</span><span class="sxs-lookup"><span data-stu-id="8afa1-124">Download and install hello [Azure Linux Agent](https://github.com/Azure/WALinuxAgent/)</span></span>
   
    <span data-ttu-id="8afa1-125">hello Azure Linux 代理程式版本 2.1.3 或更高版本需要的 tooprovision 您 Azure 堆疊上的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="8afa1-125">hello Azure Linux Agent version 2.1.3 or higher is required tooprovision your Linux VM on Azure Stack.</span></span> <span data-ttu-id="8afa1-126">許多已上面所列的 hello 分佈在其儲存機制中包含或更高套件 hello 代理程式的這個版本 (通常稱為`WALinuxAgent`或`walinuxagent`)。</span><span class="sxs-lookup"><span data-stu-id="8afa1-126">Many of hello distributions listed above already include this version of hello agent or higher as a package in their repositories (typically called `WALinuxAgent` or `walinuxagent`).</span></span> <span data-ttu-id="8afa1-127">不過，如果 hello hello Azure 代理程式套件的版本將會小於 2.1.3 （也就是 2.0.18 或更低），則您必須手動安裝 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="8afa1-127">However, if hello version of hello Azure agent package is less than 2.1.3 (i.e. 2.0.18 or lower), then you must install hello agent manually.</span></span> <span data-ttu-id="8afa1-128">可以判斷安裝的 hello 版本，從 hello 封裝名稱，或是藉由執行`/usr/sbin/waagent -version`hello VM 上。</span><span class="sxs-lookup"><span data-stu-id="8afa1-128">hello installed version can be determined either from hello package name or by running `/usr/sbin/waagent -version` on hello VM.</span></span>
   
    <span data-ttu-id="8afa1-129">手動-請遵循以下 tooinstall hello Azure Linux 代理程式的 hello 指示</span><span class="sxs-lookup"><span data-stu-id="8afa1-129">Follow hello instructions below tooinstall hello Azure Linux agent manually -</span></span>
   
   * <span data-ttu-id="8afa1-130">首先，下載 hello 最新 Azure Linux 代理程式從[GitHub](https://github.com/Azure/WALinuxAgent/releases)，範例：</span><span class="sxs-lookup"><span data-stu-id="8afa1-130">First, download hello latest Azure Linux agent from [GitHub](https://github.com/Azure/WALinuxAgent/releases), example:</span></span>
     
            # wget https://github.com/Azure/WALinuxAgent/archive/v2.2.0.tar.gz
   * <span data-ttu-id="8afa1-131">解除封裝 hello Azure 代理程式：</span><span class="sxs-lookup"><span data-stu-id="8afa1-131">Unpack hello Azure agent:</span></span>
     
            # tar -vzxf v2.2.0.tar.gz
   * <span data-ttu-id="8afa1-132">安裝 python 安裝工具</span><span class="sxs-lookup"><span data-stu-id="8afa1-132">Install python-setuptools</span></span>
     
        <span data-ttu-id="8afa1-133">**Debian / Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="8afa1-133">**Debian / Ubuntu**</span></span>
     
            # sudo apt-get update
            # sudo apt-get install python-setuptools
     
        <span data-ttu-id="8afa1-134">**Ubuntu 16.04+**</span><span class="sxs-lookup"><span data-stu-id="8afa1-134">**Ubuntu 16.04+**</span></span>
     
            # sudo apt-get install python3-setuptools
     
        <span data-ttu-id="8afa1-135">**RHEL / CentOS / Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="8afa1-135">**RHEL / CentOS / Oracle Linux**</span></span>
     
            # sudo yum install python-setuptools
   * <span data-ttu-id="8afa1-136">安裝 Azure 代理程式 hello:</span><span class="sxs-lookup"><span data-stu-id="8afa1-136">Install hello Azure agent:</span></span>
     
            # cd WALinuxAgent-2.2.0
            # sudo python setup.py install --register-service
     
     <span data-ttu-id="8afa1-137">系統使用 Python 2.x 和 Python 安裝 3.x-並存可能需要 toorun hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="8afa1-137">Systems with Python 2.x and Python 3.x installed side-by-side may need toorun hello following command:</span></span>
     
         sudo python3 setup.py install --register-service
     <span data-ttu-id="8afa1-138">如需詳細資訊，請參閱 hello Azure Linux 代理程式[讀我檔案](https://github.com/Azure/WALinuxAgent/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="8afa1-138">For more information, see hello Azure Linux Agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md).</span></span>
3. <span data-ttu-id="8afa1-139">[新增 hello 映像 toohello Marketplace](azure-stack-add-vm-image.md)。</span><span class="sxs-lookup"><span data-stu-id="8afa1-139">[Add hello image toohello Marketplace](azure-stack-add-vm-image.md).</span></span> <span data-ttu-id="8afa1-140">請確定該 hello`OSType`參數設定太`Linux`。</span><span class="sxs-lookup"><span data-stu-id="8afa1-140">Make sure that hello `OSType` parameter is set too`Linux`.</span></span>
4. <span data-ttu-id="8afa1-141">您加入 hello 映像 toohello Marketplace 之後，建立 Marketplace 項目，而且您可以部署 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8afa1-141">After you've added hello image toohello Marketplace, a Marketplace item is created and you can deploy a Linux virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8afa1-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8afa1-142">Next steps</span></span>
[<span data-ttu-id="8afa1-143">Azure Stack 的常見問題集</span><span class="sxs-lookup"><span data-stu-id="8afa1-143">Frequently asked questions for Azure Stack</span></span>](azure-stack-faq.md)

