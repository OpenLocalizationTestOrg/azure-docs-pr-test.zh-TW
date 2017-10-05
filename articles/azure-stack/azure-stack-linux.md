---
title: "Azure Stack 上的 Linux 客體 | Microsoft Docs"
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
ms.openlocfilehash: 935cd31c4b38262b7e42271574a8a221377a3cec
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-linux-virtual-machines-on-azure-stack"></a><span data-ttu-id="c7362-103">在 Azure Stack 上部署 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c7362-103">Deploy Linux virtual machines on Azure Stack</span></span>
<span data-ttu-id="c7362-104">您可以透過將 Linux 式映像新增到 Azure Stack Marketplace 中，在 Azure Stack 開發套件上部署 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c7362-104">You can deploy Linux virtual machines on the Azure Stack Development Kit by adding a Linux-based image into the Azure Stack Marketplace.</span></span> <span data-ttu-id="c7362-105">已有數個 Linux 廠商提供可新增到 Azure Stack 開發套件中的映像，您也可以建立自己的映像。</span><span class="sxs-lookup"><span data-stu-id="c7362-105">Several Linux vendors have provided images that can be added into an Azure Stack Development Kit or you can build your own.</span></span>

## <a name="download-an-image"></a><span data-ttu-id="c7362-106">下載映像</span><span class="sxs-lookup"><span data-stu-id="c7362-106">Download an image</span></span>
1. <span data-ttu-id="c7362-107">從下列連結下載並解壓縮與 Azure Stack 相容的映像，或準備您自己的映像：</span><span class="sxs-lookup"><span data-stu-id="c7362-107">Download and extract an Azure Stack-compatible image from the following links, or prepare your own:</span></span>
   
   * [<span data-ttu-id="c7362-108">Bitnami</span><span class="sxs-lookup"><span data-stu-id="c7362-108">Bitnami</span></span>](https://bitnami.com/azure-stack)
   * [<span data-ttu-id="c7362-109">CentOS</span><span class="sxs-lookup"><span data-stu-id="c7362-109">CentOS</span></span>](http://olstacks.cloudapp.net/latest/)
   * [<span data-ttu-id="c7362-110">CoreOS</span><span class="sxs-lookup"><span data-stu-id="c7362-110">CoreOS</span></span>](https://stable.release.core-os.net/amd64-usr/current/coreos_production_azure_image.vhd.bz2)
   * [<span data-ttu-id="c7362-111">SuSE</span><span class="sxs-lookup"><span data-stu-id="c7362-111">SuSE</span></span>](https://download.suse.com/Download?buildid=VCFi7y7MsFQ~)
   * <span data-ttu-id="c7362-112">[Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="c7362-112">[Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
2. <span data-ttu-id="c7362-113">如有必要，請將映像 VHD 解壓縮，並[將影像新增到 Marketplace 中](azure-stack-add-vm-image.md)。</span><span class="sxs-lookup"><span data-stu-id="c7362-113">Extract the image VHD if necessary and [add the image to the Marketplace](azure-stack-add-vm-image.md).</span></span> <span data-ttu-id="c7362-114">請確定已將 `OSType` 參數設定為 `Linux`。</span><span class="sxs-lookup"><span data-stu-id="c7362-114">Make sure that the `OSType` parameter is set to `Linux`.</span></span>
3. <span data-ttu-id="c7362-115">將映像新增到 Marketplace 中之後，便會建立 Marketplace 項目，而您就可以部署 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c7362-115">After you've added the image to the Marketplace, a Marketplace item is created and you can deploy a Linux virtual machine.</span></span>

## <a name="prepare-your-own-image"></a><span data-ttu-id="c7362-116">準備您自己的映像</span><span class="sxs-lookup"><span data-stu-id="c7362-116">Prepare your own image</span></span>
1. <span data-ttu-id="c7362-117">使用下列其中一種指示，準備您自己的 Linux 映像：</span><span class="sxs-lookup"><span data-stu-id="c7362-117">Prepare your own Linux image using one of the following instructions:</span></span>
   
   * [<span data-ttu-id="c7362-118">CentOS 型發行版本</span><span class="sxs-lookup"><span data-stu-id="c7362-118">CentOS-based Distributions</span></span>](../virtual-machines/linux/create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="c7362-119">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="c7362-119">Debian Linux</span></span>](../virtual-machines/linux/debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="c7362-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="c7362-120">Oracle Linux</span></span>](../virtual-machines/linux/oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="c7362-121">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="c7362-121">Red Hat Enterprise Linux</span></span>](../virtual-machines/linux/redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="c7362-122">SLES 和 openSUSE</span><span class="sxs-lookup"><span data-stu-id="c7362-122">SLES & openSUSE</span></span>](../virtual-machines/linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="c7362-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c7362-123">Ubuntu</span></span>](../virtual-machines/linux/create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="c7362-124">下載並安裝 [Azure Linux 代理程式](https://github.com/Azure/WALinuxAgent/)</span><span class="sxs-lookup"><span data-stu-id="c7362-124">Download and install the [Azure Linux Agent](https://github.com/Azure/WALinuxAgent/)</span></span>
   
    <span data-ttu-id="c7362-125">需要 Azure Linux 代理程式版本 2.1.3 或更高版本，才能在 Azure Stack 上佈建 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="c7362-125">The Azure Linux Agent version 2.1.3 or higher is required to provision your Linux VM on Azure Stack.</span></span> <span data-ttu-id="c7362-126">以上所列的許多發佈已在其存放庫中包含此版本的代理程式或更高版本 (通常是稱作 `WALinuxAgent` 或 `walinuxagent` 的套件)。</span><span class="sxs-lookup"><span data-stu-id="c7362-126">Many of the distributions listed above already include this version of the agent or higher as a package in their repositories (typically called `WALinuxAgent` or `walinuxagent`).</span></span> <span data-ttu-id="c7362-127">不過，若 Azure 代理程式套件的版本小於 2.1.3 (亦即 2.0.18 或更低)，則您必須手動安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="c7362-127">However, if the version of the Azure agent package is less than 2.1.3 (i.e. 2.0.18 or lower), then you must install the agent manually.</span></span> <span data-ttu-id="c7362-128">可從套件名稱或執行虛擬機器上的 `/usr/sbin/waagent -version` 來判斷已安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="c7362-128">The installed version can be determined either from the package name or by running `/usr/sbin/waagent -version` on the VM.</span></span>
   
    <span data-ttu-id="c7362-129">請遵循下列指示，手動安裝 Azure Linux 代理程式：</span><span class="sxs-lookup"><span data-stu-id="c7362-129">Follow the instructions below to install the Azure Linux agent manually -</span></span>
   
   * <span data-ttu-id="c7362-130">首先，從 [GitHub](https://github.com/Azure/WALinuxAgent/releases) 下載最新的 Azure Linux 代理程式，例如：</span><span class="sxs-lookup"><span data-stu-id="c7362-130">First, download the latest Azure Linux agent from [GitHub](https://github.com/Azure/WALinuxAgent/releases), example:</span></span>
     
            # wget https://github.com/Azure/WALinuxAgent/archive/v2.2.0.tar.gz
   * <span data-ttu-id="c7362-131">解壓縮 Azure 代理程式：</span><span class="sxs-lookup"><span data-stu-id="c7362-131">Unpack the Azure agent:</span></span>
     
            # tar -vzxf v2.2.0.tar.gz
   * <span data-ttu-id="c7362-132">安裝 python 安裝工具</span><span class="sxs-lookup"><span data-stu-id="c7362-132">Install python-setuptools</span></span>
     
        <span data-ttu-id="c7362-133">**Debian / Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="c7362-133">**Debian / Ubuntu**</span></span>
     
            # sudo apt-get update
            # sudo apt-get install python-setuptools
     
        <span data-ttu-id="c7362-134">**Ubuntu 16.04+**</span><span class="sxs-lookup"><span data-stu-id="c7362-134">**Ubuntu 16.04+**</span></span>
     
            # sudo apt-get install python3-setuptools
     
        <span data-ttu-id="c7362-135">**RHEL / CentOS / Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="c7362-135">**RHEL / CentOS / Oracle Linux**</span></span>
     
            # sudo yum install python-setuptools
   * <span data-ttu-id="c7362-136">安裝 Azure 代理程式：</span><span class="sxs-lookup"><span data-stu-id="c7362-136">Install the Azure agent:</span></span>
     
            # cd WALinuxAgent-2.2.0
            # sudo python setup.py install --register-service
     
     <span data-ttu-id="c7362-137">已並存安裝 Python 2.x 和 Python 3.x 的系統可能會需要執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="c7362-137">Systems with Python 2.x and Python 3.x installed side-by-side may need to run the following command:</span></span>
     
         sudo python3 setup.py install --register-service
     <span data-ttu-id="c7362-138">如需詳細資訊，請參閱 Azure Linux 代理程式[讀我檔案](https://github.com/Azure/WALinuxAgent/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="c7362-138">For more information, see the Azure Linux Agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md).</span></span>
3. <span data-ttu-id="c7362-139">[將映像新增到 Marketplace 中](azure-stack-add-vm-image.md)。</span><span class="sxs-lookup"><span data-stu-id="c7362-139">[Add the image to the Marketplace](azure-stack-add-vm-image.md).</span></span> <span data-ttu-id="c7362-140">請確定已將 `OSType` 參數設定為 `Linux`。</span><span class="sxs-lookup"><span data-stu-id="c7362-140">Make sure that the `OSType` parameter is set to `Linux`.</span></span>
4. <span data-ttu-id="c7362-141">將映像新增到 Marketplace 中之後，便會建立 Marketplace 項目，而您就可以部署 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c7362-141">After you've added the image to the Marketplace, a Marketplace item is created and you can deploy a Linux virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7362-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c7362-142">Next steps</span></span>
[<span data-ttu-id="c7362-143">Azure Stack 的常見問題集</span><span class="sxs-lookup"><span data-stu-id="c7362-143">Frequently asked questions for Azure Stack</span></span>](azure-stack-faq.md)

