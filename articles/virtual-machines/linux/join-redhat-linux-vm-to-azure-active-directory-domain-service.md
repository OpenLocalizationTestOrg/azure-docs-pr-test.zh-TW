---
title: "將 RedHat Linux VM 加入 Azure Active Directory DS | Microsoft Docs"
description: "如何將現有 RedHat Enterprise Linux 7 VM 加入 Azure Active Directory 網域服務。"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/14/2016
ms.author: v-livech
ms.openlocfilehash: 2e46a0f3c9bdbe267d121b4bf62e25d5d411fcc2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="join-a-redhat-linux-vm-to-an-azure-active-directory-domain-service"></a><span data-ttu-id="713b3-103">將 RedHat Linux VM 加入 Azure Active Directory 網域服務</span><span class="sxs-lookup"><span data-stu-id="713b3-103">Join a RedHat Linux VM to an Azure Active Directory Domain Service</span></span>

<span data-ttu-id="713b3-104">本文說明如何將 Red Hat Enterprise Linux (RHEL) 7 虛擬機器加入 Azure Active Directory Domain Services (AADDS) 管理的網域。</span><span class="sxs-lookup"><span data-stu-id="713b3-104">This article shows you how to join a Red Hat Enterprise Linux (RHEL) 7 virtual machine to an Azure Active Directory Domain Services (AADDS) managed domain.</span></span>  <span data-ttu-id="713b3-105">這些需求包括：</span><span class="sxs-lookup"><span data-stu-id="713b3-105">The requirements are:</span></span>

- [<span data-ttu-id="713b3-106">一個 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="713b3-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)

- [<span data-ttu-id="713b3-107">SSH 公開金鑰和私密金鑰檔案</span><span class="sxs-lookup"><span data-stu-id="713b3-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

- [<span data-ttu-id="713b3-108">Azure Active Directory Domain Services DC</span><span class="sxs-lookup"><span data-stu-id="713b3-108">an Azure Active Directory Domain Services DC</span></span>](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="713b3-109">快速命令</span><span class="sxs-lookup"><span data-stu-id="713b3-109">Quick Commands</span></span>

<span data-ttu-id="713b3-110">_將任何範例換成您自己的設定。_</span><span class="sxs-lookup"><span data-stu-id="713b3-110">_Replace any examples with your own settings._</span></span>

### <a name="switch-the-azure-cli-to-classic-deployment-mode"></a><span data-ttu-id="713b3-111">將 azure-cli 切換至傳統部署模式</span><span class="sxs-lookup"><span data-stu-id="713b3-111">Switch the azure-cli to classic deployment mode</span></span>

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a><span data-ttu-id="713b3-112">搜尋 RHEL 版本和映像</span><span class="sxs-lookup"><span data-stu-id="713b3-112">Search for a RHEL version and image</span></span>

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a><span data-ttu-id="713b3-113">建立 Redhat Linux VM</span><span class="sxs-lookup"><span data-stu-id="713b3-113">Create a Redhat Linux VM</span></span>

```azurecli
azure vm create myVM \
-o a879bbefc56a43abb0ce65052aac09f3__RHEL_7_2_Standard_Azure_RHUI-20161026220742 \
-g ahmet \
-p myPassword \
-e 22 \
-t "~/.ssh/id_rsa.pub" \
-z "Small" \
-l "West US"
```

### <a name="ssh-to-the-vm"></a><span data-ttu-id="713b3-114">透過 SSH 連接到 VM</span><span class="sxs-lookup"><span data-stu-id="713b3-114">SSH to the VM</span></span>

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a><span data-ttu-id="713b3-115">更新 YUM 套件</span><span class="sxs-lookup"><span data-stu-id="713b3-115">Update YUM packages</span></span>

```bash
sudo yum update
```

### <a name="install-packages-needed"></a><span data-ttu-id="713b3-116">安裝需要的套件</span><span class="sxs-lookup"><span data-stu-id="713b3-116">Install packages needed</span></span>

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

<span data-ttu-id="713b3-117">既然 Linux 虛擬機器上已安裝必要的封裝，下一個工作是將虛擬機器加入受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="713b3-117">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span></span>

### <a name="discover-the-aad-domain-services-managed-domain"></a><span data-ttu-id="713b3-118">探索 AAD Domain Services 管理的網域</span><span class="sxs-lookup"><span data-stu-id="713b3-118">Discover the AAD Domain Services managed domain</span></span>

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a><span data-ttu-id="713b3-119">初始化 kerberos</span><span class="sxs-lookup"><span data-stu-id="713b3-119">Initialize kerberos</span></span>

<span data-ttu-id="713b3-120">請確定您是指定屬於 'AAD DC Administrators' 群組的使用者。</span><span class="sxs-lookup"><span data-stu-id="713b3-120">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="713b3-121">只有這些使用者可以將電腦加入受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="713b3-121">Only these users can join computers to the managed domain.</span></span>

```bash
kinit ahmet@mydomain.com
```

### <a name="join-the-machine-to-the-domain"></a><span data-ttu-id="713b3-122">將電腦加入網域</span><span class="sxs-lookup"><span data-stu-id="713b3-122">Join the machine to the domain</span></span>

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-the-machine-is-joined-to-the-domain"></a><span data-ttu-id="713b3-123">確認電腦已加入網域</span><span class="sxs-lookup"><span data-stu-id="713b3-123">Verify the machine is joined to the domain</span></span>

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="713b3-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="713b3-124">Next Steps</span></span>

* [<span data-ttu-id="713b3-125">適用於 Azure 中隨選 Red Hat Enterprise Linux VM 的 Red Hat Update Infrastructure (RHUI)</span><span class="sxs-lookup"><span data-stu-id="713b3-125">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="713b3-126">為 Azure Resource Manager 中的虛擬機器設定金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="713b3-126">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="713b3-127">使用 Azure Resource Manager 範本和 Azure CLI 部署和管理虛擬機器</span><span class="sxs-lookup"><span data-stu-id="713b3-127">Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI</span></span>](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
