---
title: "在 Azure 中的 aaaIntroduction tooLinux |Microsoft 文件"
description: "了解如何使用 Azure 上的 Linux 虛擬機器"
services: virtual-machines-linux
documentationcenter: python
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: b13bf305-87bf-4df3-815e-e8f6337aa6ea
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: szark
ms.openlocfilehash: 3a931447ee23ce7000174ca314c3e10abc6b8e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toolinux-on-azure"></a><span data-ttu-id="67417-103">在 Azure 上的簡介 tooLinux</span><span class="sxs-lookup"><span data-stu-id="67417-103">Introduction tooLinux on Azure</span></span>
<span data-ttu-id="67417-104">本主題提供在 hello Azure 雲端中使用的 Linux 虛擬機器的某些層面的概觀。</span><span class="sxs-lookup"><span data-stu-id="67417-104">This topic provides an overview of some aspects of using Linux virtual machines in hello Azure cloud.</span></span> <span data-ttu-id="67417-105">部署 Linux 虛擬機器是簡單的程序，使用從 hello 組件庫的映像。</span><span class="sxs-lookup"><span data-stu-id="67417-105">Deploying a Linux virtual machine is a straightforward process using an image from hello gallery.</span></span>

## <a name="authentication-usernames-passwords-and-ssh-keys"></a><span data-ttu-id="67417-106">驗證：使用者名稱、密碼和 SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="67417-106">Authentication: Usernames, Passwords and SSH Keys</span></span>
<span data-ttu-id="67417-107">當建立 Linux 虛擬機器使用 hello Azure 入口網站，系統會要求您 tooprovide 任一使用者名稱和密碼或 SSH 公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="67417-107">When creating a Linux virtual machine using hello Azure portal, you are asked tooprovide a either username and password or an SSH public key.</span></span> <span data-ttu-id="67417-108">hello 選擇部署在 Azure 上的 Linux 虛擬機器的使用者名稱是主體 toohello 遵循條件約束： 系統帳戶的名稱 (UID < 100) hello 中已有虛擬機器不允許，'root' 例如。</span><span class="sxs-lookup"><span data-stu-id="67417-108">hello choice of a username for deploying a Linux virtual machine on Azure is subject toohello following constraint: names of system accounts (UID <100) already present in hello virtual machine are not allowed, 'root' for example.</span></span>

* <span data-ttu-id="67417-109">請參閱[建立執行 Linux 的虛擬機器](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="67417-109">See [Create a Virtual Machine Running Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="67417-110">請參閱[如何透過在 Azure 上的 Linux SSH tooUse](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="67417-110">See [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="obtaining-superuser-privileges-using-sudo"></a><span data-ttu-id="67417-111">使用 `sudo`</span><span class="sxs-lookup"><span data-stu-id="67417-111">Obtaining Superuser Privileges Using `sudo`</span></span>
<span data-ttu-id="67417-112">hello 在 Azure 上的虛擬機器執行個體部署期間指定的使用者帳戶是特殊權限的帳戶。</span><span class="sxs-lookup"><span data-stu-id="67417-112">hello user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="67417-113">此帳戶蒻謔 hello Azure Linux 代理程式 toobe 無法 tooelevate 權限 tooroot （superuser 帳戶） 使用 hello`sudo`公用程式。</span><span class="sxs-lookup"><span data-stu-id="67417-113">This account is configured by hello Azure Linux Agent toobe able tooelevate privileges tooroot (superuser account) using hello `sudo` utility.</span></span> <span data-ttu-id="67417-114">登入使用此使用者帳戶之後，您將無法 toorun 命令根使用 hello 命令語法為：</span><span class="sxs-lookup"><span data-stu-id="67417-114">Once logged in using this user account, you will be able toorun commands as root using hello command syntax:</span></span>

    # sudo <COMMAND>

<span data-ttu-id="67417-115">您可以選擇使用 **sudo -s**來取得 root shell。</span><span class="sxs-lookup"><span data-stu-id="67417-115">You can optionally obtain a root shell using **sudo -s**.</span></span>

* <span data-ttu-id="67417-116">請參閱[在 Azure 中的 Linux 虛擬機器上使用根權限](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="67417-116">See [Using root privileges on Linux virtual machines in Azure](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="firewall-configuration"></a><span data-ttu-id="67417-117">防火牆設定</span><span class="sxs-lookup"><span data-stu-id="67417-117">Firewall Configuration</span></span>
<span data-ttu-id="67417-118">Azure 提供限制連線 tooports hello Azure 入口網站中指定的輸入封包篩選器。</span><span class="sxs-lookup"><span data-stu-id="67417-118">Azure provides an inbound packet filter that restricts connectivity tooports specified in hello Azure portal.</span></span> <span data-ttu-id="67417-119">根據預設，hello 只允許連接埠是 SSH。</span><span class="sxs-lookup"><span data-stu-id="67417-119">By default, hello only allowed port is SSH.</span></span> <span data-ttu-id="67417-120">可能存取 tooadditional 連接埠上開啟您的 Linux 虛擬機器在 hello Azure 入口網站中設定的端點：</span><span class="sxs-lookup"><span data-stu-id="67417-120">You may open up access tooadditional ports on your Linux virtual machine by configuring endpoints in hello Azure portal:</span></span>

* <span data-ttu-id="67417-121">請參閱：[如何 tooSet 端點 tooa 虛擬機器](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="67417-121">See: [How tooSet Up Endpoints tooa Virtual Machine](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="67417-122">在 hello Azure 組件庫中的 hello Linux 映像不會啟用 hello *iptables*預設的防火牆。</span><span class="sxs-lookup"><span data-stu-id="67417-122">hello Linux images in hello Azure Gallery do not enable hello *iptables* firewall by default.</span></span> <span data-ttu-id="67417-123">如果需要的話，可能會設定 hello 防火牆 tooprovide 額外的篩選。</span><span class="sxs-lookup"><span data-stu-id="67417-123">If desired, hello firewall may be configured tooprovide additional filtering.</span></span>

## <a name="hostname-changes"></a><span data-ttu-id="67417-124">主機名稱變更</span><span class="sxs-lookup"><span data-stu-id="67417-124">Hostname Changes</span></span>
<span data-ttu-id="67417-125">當您一開始會部署 Linux 映像的執行個體時，您就需要的 tooprovide hello 虛擬機器的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="67417-125">When you initially deploy an instance of a Linux image, you are required tooprovide a host name for hello virtual machine.</span></span> <span data-ttu-id="67417-126">一旦 hello 虛擬機器正在執行，此主機名稱會是已發行的 toohello 平台 DNS 伺服器，讓多個連接的虛擬機器 tooeach 其他可以執行使用主機名稱的 IP 位址搜尋。</span><span class="sxs-lookup"><span data-stu-id="67417-126">Once hello virtual machine is running, this hostname is published toohello platform DNS servers so that multiple virtual machines connected tooeach other can perform IP address lookups using hostnames.</span></span>

<span data-ttu-id="67417-127">如果虛擬機器部署之後，需要主機名稱變更，請使用 hello 命令</span><span class="sxs-lookup"><span data-stu-id="67417-127">If hostname changes are desired after a virtual machine has been deployed, please use hello command</span></span>

    # sudo hostname <newname>

<span data-ttu-id="67417-128">hello Azure Linux 代理程式包含功能 tooautomatically 偵測到此名稱的變更和適當地設定 hello 虛擬機器 toopersist 這項變更，並發佈此變更 toohello 平台 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="67417-128">hello Azure Linux Agent includes functionality tooautomatically detect this name change and appropriately configure hello virtual machine toopersist this change and publish this change toohello platform DNS servers.</span></span>

* [<span data-ttu-id="67417-129">Azure Linux 代理程式使用者指南</span><span class="sxs-lookup"><span data-stu-id="67417-129">Azure Linux Agent User Guide</span></span>](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="cloud-init"></a><span data-ttu-id="67417-130">Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="67417-130">Cloud-Init</span></span>
<span data-ttu-id="67417-131">**Ubuntu** 和 **CoreOS** 映像會在 Azure 上利用 Cloud-Init，這可提供用來啟動虛擬機器的額外功能。</span><span class="sxs-lookup"><span data-stu-id="67417-131">**Ubuntu** and **CoreOS** images utilize cloud-init on Azure, which provides additional capabilities for bootstrapping a virtual machine.</span></span>

* [<span data-ttu-id="67417-132">如何 tooInject 自訂資料</span><span class="sxs-lookup"><span data-stu-id="67417-132">How tooInject Custom Data</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="67417-133">Microsoft Azure 上的自訂資料和 Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="67417-133">Custom Data and Cloud-Init on Microsoft Azure</span></span>](https://azure.microsoft.com/blog/2014/04/21/custom-data-and-cloud-init-on-windows-azure/)
* [<span data-ttu-id="67417-134">使用 Cloud-Init 建立 Azure Swap 磁碟分割</span><span class="sxs-lookup"><span data-stu-id="67417-134">Create Azure Swap Partitions Using Cloud-Init</span></span>](https://wiki.ubuntu.com/AzureSwapPartitions)
* [<span data-ttu-id="67417-135">如何在 Azure 上 CoreOS tooUse</span><span class="sxs-lookup"><span data-stu-id="67417-135">How tooUse CoreOS on Azure</span></span>](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="virtual-machine-image-capture"></a><span data-ttu-id="67417-136">擷取虛擬機器映像</span><span class="sxs-lookup"><span data-stu-id="67417-136">Virtual Machine Image Capture</span></span>
<span data-ttu-id="67417-137">Azure 提供現有的虛擬機器的 hello 能力 toocapture hello 狀態納入接下來可以使用的 toodeploy 額外的虛擬機器執行個體的映像。</span><span class="sxs-lookup"><span data-stu-id="67417-137">Azure provides hello ability toocapture hello state of an existing virtual machine into an image that can subsequently be used toodeploy additional virtual machine instances.</span></span> <span data-ttu-id="67417-138">hello Azure Linux 代理程式可能使用的 toorollback 部分 hello hello 佈建程序期間執行的自訂。</span><span class="sxs-lookup"><span data-stu-id="67417-138">hello Azure Linux Agent may be used toorollback some of hello customization that was performed during hello provisioning process.</span></span> <span data-ttu-id="67417-139">您可以依照下列 toocapture 虛擬機器的 hello 步驟，做為映像：</span><span class="sxs-lookup"><span data-stu-id="67417-139">You may follow hello steps below toocapture a virtual machine as an image:</span></span>

1. <span data-ttu-id="67417-140">執行**waagent-取消佈建**tooundo 佈建的自訂。</span><span class="sxs-lookup"><span data-stu-id="67417-140">Run **waagent -deprovision** tooundo provisioning customization.</span></span> <span data-ttu-id="67417-141">或者**waagent-取消佈建 + 使用者**toooptionally 刪除 hello 佈建和所有相關聯的資料期間所指定的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="67417-141">Or **waagent -deprovision+user** toooptionally delete hello user account specified during provisioning and all associated data.</span></span>
2. <span data-ttu-id="67417-142">關閉清單/hello 虛擬機器關機。</span><span class="sxs-lookup"><span data-stu-id="67417-142">Shut down/power off hello virtual machine.</span></span>
3. <span data-ttu-id="67417-143">按一下**擷取**hello Azure 入口網站或使用 hello PowerShell 或 CLI 工具 toocapture hello 虛擬機器做為映像。</span><span class="sxs-lookup"><span data-stu-id="67417-143">Click **Capture** in hello Azure portal or use hello PowerShell or CLI tools toocapture hello virtual machine as an image.</span></span>
   
   * <span data-ttu-id="67417-144">請參閱：[如何 tooCapture Linux 虛擬機器 tooUse 做為範本](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="67417-144">See: [How tooCapture a Linux Virtual Machine tooUse as a Template](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

## <a name="attaching-disks"></a><span data-ttu-id="67417-145">連接磁碟</span><span class="sxs-lookup"><span data-stu-id="67417-145">Attaching Disks</span></span>
<span data-ttu-id="67417-146">每個虛擬機器都會連接一個暫時性的本機 *資源磁碟* 。</span><span class="sxs-lookup"><span data-stu-id="67417-146">Each virtual machine has a temporary, local *resource disk* attached.</span></span> <span data-ttu-id="67417-147">在重新啟動期間的資源磁碟上的資料可能不會持久，因為它常用的應用程式和暫時性的 hello 虛擬機器中執行的處理序和**暫存**資料的儲存體。</span><span class="sxs-lookup"><span data-stu-id="67417-147">Because data on a resource disk may not be durable across reboots, it is often used by applications and processes running in hello virtual machine for transient and **temporary** storage of data.</span></span> <span data-ttu-id="67417-148">它也是使用的 toostore hello 分頁 hello 作業系統檔案。</span><span class="sxs-lookup"><span data-stu-id="67417-148">It is also used toostore hello page or swap files for hello operating system.</span></span>

<span data-ttu-id="67417-149">在 Linux 上 hello 資源磁碟通常是由管理 hello Azure Linux 代理程式，且自動掛接太**/mnt/retention/ 資源**(或**/mnt** Ubuntu 映像上)。</span><span class="sxs-lookup"><span data-stu-id="67417-149">On Linux, hello resource disk is typically managed by hello Azure Linux Agent and automatically mounted too**/mnt/resource** (or **/mnt** on Ubuntu images).</span></span>

> [!NOTE]
> <span data-ttu-id="67417-150">請注意該 hello 資源磁碟是**暫存**磁碟，並可能會刪除並重新格式化 hello VM 重新開機時。</span><span class="sxs-lookup"><span data-stu-id="67417-150">Note that hello resource disk is a **temporary** disk, and might be deleted and reformatted when hello VM is rebooted.</span></span>
> 
> 

<span data-ttu-id="67417-151">在 Linux 上 hello 資料磁碟可能名為 hello 核心`/dev/sdc`，而且使用者需要 toopartition、 格式化及裝載該資源。</span><span class="sxs-lookup"><span data-stu-id="67417-151">On Linux hello data disk might be named by hello kernel as `/dev/sdc`, and users will need toopartition, format and mount that resource.</span></span> <span data-ttu-id="67417-152">這會涵蓋在 hello 教學課程逐步：[如何 tooAttach 虛擬機器的資料磁碟 tooa](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="67417-152">This is covered step-by-step in hello tutorial: [How tooAttach a Data Disk tooa Virtual Machine](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

* <span data-ttu-id="67417-153">**另請參閱︰**[Linux 上設定軟體 RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)  &  [設定 Azure 中 Linux VM 的 LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="67417-153">**See also:** [Configure Software RAID on Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [Configure LVM on a Linux VM in Azure](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

