---
title: "aaaJoin RedHat Linux VM tooan Azure Active Directory DS |Microsoft 文件"
description: "如何 toojoin 現有 RedHat Enterprise Linux 7 VM tooan Azure Active Directory 網域服務。"
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
ms.openlocfilehash: f3ba3c764e253191753f1cc5fc8c3b85c53818af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a><span data-ttu-id="ae736-103">加入 RedHat Linux VM tooan Azure Active Directory 網域服務</span><span class="sxs-lookup"><span data-stu-id="ae736-103">Join a RedHat Linux VM tooan Azure Active Directory Domain Service</span></span>

<span data-ttu-id="ae736-104">本文章將示範如何 toojoin Red Hat Enterprise Linux (RHEL) 7 虛擬機器 tooan Azure Active Directory 網域服務 (AADDS) 管理網域。</span><span class="sxs-lookup"><span data-stu-id="ae736-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure Active Directory Domain Services (AADDS) managed domain.</span></span>  <span data-ttu-id="ae736-105">hello 需求如下：</span><span class="sxs-lookup"><span data-stu-id="ae736-105">hello requirements are:</span></span>

- [<span data-ttu-id="ae736-106">一個 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="ae736-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)

- [<span data-ttu-id="ae736-107">SSH 公開金鑰和私密金鑰檔案</span><span class="sxs-lookup"><span data-stu-id="ae736-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

- [<span data-ttu-id="ae736-108">Azure Active Directory Domain Services DC</span><span class="sxs-lookup"><span data-stu-id="ae736-108">an Azure Active Directory Domain Services DC</span></span>](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="ae736-109">快速命令</span><span class="sxs-lookup"><span data-stu-id="ae736-109">Quick Commands</span></span>

<span data-ttu-id="ae736-110">_將任何範例換成您自己的設定。_</span><span class="sxs-lookup"><span data-stu-id="ae736-110">_Replace any examples with your own settings._</span></span>

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a><span data-ttu-id="ae736-111">切換 hello azure cli tooclassic 部署模式</span><span class="sxs-lookup"><span data-stu-id="ae736-111">Switch hello azure-cli tooclassic deployment mode</span></span>

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a><span data-ttu-id="ae736-112">搜尋 RHEL 版本和映像</span><span class="sxs-lookup"><span data-stu-id="ae736-112">Search for a RHEL version and image</span></span>

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a><span data-ttu-id="ae736-113">建立 Redhat Linux VM</span><span class="sxs-lookup"><span data-stu-id="ae736-113">Create a Redhat Linux VM</span></span>

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

### <a name="ssh-toohello-vm"></a><span data-ttu-id="ae736-114">SSH toohello VM</span><span class="sxs-lookup"><span data-stu-id="ae736-114">SSH toohello VM</span></span>

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a><span data-ttu-id="ae736-115">更新 YUM 套件</span><span class="sxs-lookup"><span data-stu-id="ae736-115">Update YUM packages</span></span>

```bash
sudo yum update
```

### <a name="install-packages-needed"></a><span data-ttu-id="ae736-116">安裝需要的套件</span><span class="sxs-lookup"><span data-stu-id="ae736-116">Install packages needed</span></span>

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

<span data-ttu-id="ae736-117">現在，hello Linux 虛擬機器上安裝所需的 hello 封裝，hello 下一項工作就會是 toojoin hello 虛擬機器 toohello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="ae736-117">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

### <a name="discover-hello-aad-domain-services-managed-domain"></a><span data-ttu-id="ae736-118">探索 hello AAD 網域服務受管理的網域</span><span class="sxs-lookup"><span data-stu-id="ae736-118">Discover hello AAD Domain Services managed domain</span></span>

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a><span data-ttu-id="ae736-119">初始化 kerberos</span><span class="sxs-lookup"><span data-stu-id="ae736-119">Initialize kerberos</span></span>

<span data-ttu-id="ae736-120">請確認您指定隸屬 toohello ' AAD DC Administrators' 群組的使用者身分。</span><span class="sxs-lookup"><span data-stu-id="ae736-120">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="ae736-121">只有這些使用者可以加入電腦 toohello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="ae736-121">Only these users can join computers toohello managed domain.</span></span>

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a><span data-ttu-id="ae736-122">加入 hello 機器 toohello 網域</span><span class="sxs-lookup"><span data-stu-id="ae736-122">Join hello machine toohello domain</span></span>

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a><span data-ttu-id="ae736-123">請確認 hello 電腦聯結的 toohello 網域</span><span class="sxs-lookup"><span data-stu-id="ae736-123">Verify hello machine is joined toohello domain</span></span>

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="ae736-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ae736-124">Next Steps</span></span>

* [<span data-ttu-id="ae736-125">適用於 Azure 中隨選 Red Hat Enterprise Linux VM 的 Red Hat Update Infrastructure (RHUI)</span><span class="sxs-lookup"><span data-stu-id="ae736-125">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="ae736-126">為 Azure Resource Manager 中的虛擬機器設定金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="ae736-126">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="ae736-127">部署及管理虛擬機器使用的 Azure 資源管理員範本和 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ae736-127">Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI</span></span>](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
