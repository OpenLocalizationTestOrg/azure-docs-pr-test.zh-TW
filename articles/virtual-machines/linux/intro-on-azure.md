---
title: "Azure 中的 Linux 簡介 | Microsoft Docs"
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
ms.openlocfilehash: 7bd0c5549a2e1f592681760d5ef464b9570ca4ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-linux-on-azure"></a><span data-ttu-id="71dcd-103">Azure 上的 Linux 簡介</span><span class="sxs-lookup"><span data-stu-id="71dcd-103">Introduction to Linux on Azure</span></span>
<span data-ttu-id="71dcd-104">本主題摘要說明在 Azure 雲端中使用 Linux 虛擬機器的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="71dcd-104">This topic provides an overview of some aspects of using Linux virtual machines in the Azure cloud.</span></span> <span data-ttu-id="71dcd-105">使用組件庫中現存的映像來部署 Linux 虛擬機器會很簡單。</span><span class="sxs-lookup"><span data-stu-id="71dcd-105">Deploying a Linux virtual machine is a straightforward process using an image from the gallery.</span></span>

## <a name="authentication-usernames-passwords-and-ssh-keys"></a><span data-ttu-id="71dcd-106">驗證：使用者名稱、密碼和 SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="71dcd-106">Authentication: Usernames, Passwords and SSH Keys</span></span>
<span data-ttu-id="71dcd-107">使用 Azure 入口網站來建立 Linux 虛擬機器時，系統會要求您提供使用者名稱和密碼或 SSH 公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="71dcd-107">When creating a Linux virtual machine using the Azure portal, you are asked to provide a either username and password or an SSH public key.</span></span> <span data-ttu-id="71dcd-108">在 Azure 上部署 Linux 虛擬機器的使用者名稱選擇受到下列限制：不允許使用已存在於虛擬機器中的系統帳戶名稱 (UID <100)，例如 'root'。</span><span class="sxs-lookup"><span data-stu-id="71dcd-108">The choice of a username for deploying a Linux virtual machine on Azure is subject to the following constraint: names of system accounts (UID <100) already present in the virtual machine are not allowed, 'root' for example.</span></span>

* <span data-ttu-id="71dcd-109">請參閱[建立執行 Linux 的虛擬機器](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="71dcd-109">See [Create a Virtual Machine Running Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="71dcd-110">請參閱[如何對 Azure 上的 Linux 使用 SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="71dcd-110">See [How to Use SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="obtaining-superuser-privileges-using-sudo"></a><span data-ttu-id="71dcd-111">使用 `sudo`</span><span class="sxs-lookup"><span data-stu-id="71dcd-111">Obtaining Superuser Privileges Using `sudo`</span></span>
<span data-ttu-id="71dcd-112">在 Azure 上部署虛擬機器執行個體時所指定的使用者帳戶是特殊權限帳戶。</span><span class="sxs-lookup"><span data-stu-id="71dcd-112">The user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="71dcd-113">此帳戶由 Azure Linux 代理程式設定，可使用 `sudo` 公用程式將權限提升至 root (超級使用者帳戶)。</span><span class="sxs-lookup"><span data-stu-id="71dcd-113">This account is configured by the Azure Linux Agent to be able to elevate privileges to root (superuser account) using the `sudo` utility.</span></span> <span data-ttu-id="71dcd-114">使用此使用者帳戶登入之後，您就能夠以 root 的身分使用命令語法來執行命令：</span><span class="sxs-lookup"><span data-stu-id="71dcd-114">Once logged in using this user account, you will be able to run commands as root using the command syntax:</span></span>

    # sudo <COMMAND>

<span data-ttu-id="71dcd-115">您可以選擇使用 **sudo -s**來取得 root shell。</span><span class="sxs-lookup"><span data-stu-id="71dcd-115">You can optionally obtain a root shell using **sudo -s**.</span></span>

* <span data-ttu-id="71dcd-116">請參閱[在 Azure 中的 Linux 虛擬機器上使用根權限](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="71dcd-116">See [Using root privileges on Linux virtual machines in Azure](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="firewall-configuration"></a><span data-ttu-id="71dcd-117">防火牆設定</span><span class="sxs-lookup"><span data-stu-id="71dcd-117">Firewall Configuration</span></span>
<span data-ttu-id="71dcd-118">Azure 提供輸入封包篩選器，可限制只能連線至 Azure 入口網站中指定的連接埠。</span><span class="sxs-lookup"><span data-stu-id="71dcd-118">Azure provides an inbound packet filter that restricts connectivity to ports specified in the Azure portal.</span></span> <span data-ttu-id="71dcd-119">預設允許的連接埠只有 SSH。</span><span class="sxs-lookup"><span data-stu-id="71dcd-119">By default, the only allowed port is SSH.</span></span> <span data-ttu-id="71dcd-120">您可以在 Azure 入口網站中設定端點，以開放存取 Linux 虛擬機器上的其他連接埠：</span><span class="sxs-lookup"><span data-stu-id="71dcd-120">You may open up access to additional ports on your Linux virtual machine by configuring endpoints in the Azure portal:</span></span>

* <span data-ttu-id="71dcd-121">請參閱：[如何設定虛擬機器的端點](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="71dcd-121">See: [How to Set Up Endpoints to a Virtual Machine](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="71dcd-122">Azure 映像庫中的 Linux 映像依預設不會啟用 *iptables* 防火牆。</span><span class="sxs-lookup"><span data-stu-id="71dcd-122">The Linux images in the Azure Gallery do not enable the *iptables* firewall by default.</span></span> <span data-ttu-id="71dcd-123">如有需要，可設定防火牆來提供其他篩選。</span><span class="sxs-lookup"><span data-stu-id="71dcd-123">If desired, the firewall may be configured to provide additional filtering.</span></span>

## <a name="hostname-changes"></a><span data-ttu-id="71dcd-124">主機名稱變更</span><span class="sxs-lookup"><span data-stu-id="71dcd-124">Hostname Changes</span></span>
<span data-ttu-id="71dcd-125">初次部署 Linux 映像的執行個體時，您必須提供虛擬機器的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="71dcd-125">When you initially deploy an instance of a Linux image, you are required to provide a host name for the virtual machine.</span></span> <span data-ttu-id="71dcd-126">當虛擬機器執行時，此主機名稱會發佈至平台 DNS 伺服器，讓彼此相連的多個虛擬機器可利用主機名稱來執行 IP 位址查閱。</span><span class="sxs-lookup"><span data-stu-id="71dcd-126">Once the virtual machine is running, this hostname is published to the platform DNS servers so that multiple virtual machines connected to each other can perform IP address lookups using hostnames.</span></span>

<span data-ttu-id="71dcd-127">如果在部署虛擬機器之後需要變更主機名稱，請使用命令</span><span class="sxs-lookup"><span data-stu-id="71dcd-127">If hostname changes are desired after a virtual machine has been deployed, please use the command</span></span>

    # sudo hostname <newname>

<span data-ttu-id="71dcd-128">Azure Linux 代理程式包括可自動偵測此名稱變更、適當地設定虛擬機器來保存此變更，以及將此變更發佈至平台 DNS 伺服器等功能。</span><span class="sxs-lookup"><span data-stu-id="71dcd-128">The Azure Linux Agent includes functionality to automatically detect this name change and appropriately configure the virtual machine to persist this change and publish this change to the platform DNS servers.</span></span>

* [<span data-ttu-id="71dcd-129">Azure Linux 代理程式使用者指南</span><span class="sxs-lookup"><span data-stu-id="71dcd-129">Azure Linux Agent User Guide</span></span>](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="cloud-init"></a><span data-ttu-id="71dcd-130">Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="71dcd-130">Cloud-Init</span></span>
<span data-ttu-id="71dcd-131">**Ubuntu** 和 **CoreOS** 映像會在 Azure 上利用 Cloud-Init，這可提供用來啟動虛擬機器的額外功能。</span><span class="sxs-lookup"><span data-stu-id="71dcd-131">**Ubuntu** and **CoreOS** images utilize cloud-init on Azure, which provides additional capabilities for bootstrapping a virtual machine.</span></span>

* [<span data-ttu-id="71dcd-132">如何插入自訂資料</span><span class="sxs-lookup"><span data-stu-id="71dcd-132">How to Inject Custom Data</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="71dcd-133">Microsoft Azure 上的自訂資料和 Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="71dcd-133">Custom Data and Cloud-Init on Microsoft Azure</span></span>](https://azure.microsoft.com/blog/2014/04/21/custom-data-and-cloud-init-on-windows-azure/)
* [<span data-ttu-id="71dcd-134">使用 Cloud-Init 建立 Azure Swap 磁碟分割</span><span class="sxs-lookup"><span data-stu-id="71dcd-134">Create Azure Swap Partitions Using Cloud-Init</span></span>](https://wiki.ubuntu.com/AzureSwapPartitions)
* [<span data-ttu-id="71dcd-135">如何在 Azure 上使用 CoreOS</span><span class="sxs-lookup"><span data-stu-id="71dcd-135">How to Use CoreOS on Azure</span></span>](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="virtual-machine-image-capture"></a><span data-ttu-id="71dcd-136">擷取虛擬機器映像</span><span class="sxs-lookup"><span data-stu-id="71dcd-136">Virtual Machine Image Capture</span></span>
<span data-ttu-id="71dcd-137">Azure 可將現有虛擬機器的狀態擷取到映像中，供以後用來部署其他虛擬機器執行個體。</span><span class="sxs-lookup"><span data-stu-id="71dcd-137">Azure provides the ability to capture the state of an existing virtual machine into an image that can subsequently be used to deploy additional virtual machine instances.</span></span> <span data-ttu-id="71dcd-138">Azure Linux 代理程式可用來回復佈建過程中執行的一些自訂。</span><span class="sxs-lookup"><span data-stu-id="71dcd-138">The Azure Linux Agent may be used to rollback some of the customization that was performed during the provisioning process.</span></span> <span data-ttu-id="71dcd-139">您可以依照下列步驟將虛擬機器擷取為映像：</span><span class="sxs-lookup"><span data-stu-id="71dcd-139">You may follow the steps below to capture a virtual machine as an image:</span></span>

1. <span data-ttu-id="71dcd-140">執行 **waagent -deprovision** 來還原佈建自訂。</span><span class="sxs-lookup"><span data-stu-id="71dcd-140">Run **waagent -deprovision** to undo provisioning customization.</span></span> <span data-ttu-id="71dcd-141">或是 **waagent -deprovision+user**，選擇性地將佈建期間指定的使用者帳戶及所有相關資料刪除。</span><span class="sxs-lookup"><span data-stu-id="71dcd-141">Or **waagent -deprovision+user** to optionally delete the user account specified during provisioning and all associated data.</span></span>
2. <span data-ttu-id="71dcd-142">關閉虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="71dcd-142">Shut down/power off the virtual machine.</span></span>
3. <span data-ttu-id="71dcd-143">按一下 Azure 入口網站中的 [擷取] 或使用 PowerShell 或 CLI 工具，將虛擬機器擷取為映像。</span><span class="sxs-lookup"><span data-stu-id="71dcd-143">Click **Capture** in the Azure portal or use the PowerShell or CLI tools to capture the virtual machine as an image.</span></span>
   
   * <span data-ttu-id="71dcd-144">請參閱：[如何擷取 Linux 虛擬機器作為範本使用](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="71dcd-144">See: [How to Capture a Linux Virtual Machine to Use as a Template](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

## <a name="attaching-disks"></a><span data-ttu-id="71dcd-145">連接磁碟</span><span class="sxs-lookup"><span data-stu-id="71dcd-145">Attaching Disks</span></span>
<span data-ttu-id="71dcd-146">每個虛擬機器都會連接一個暫時性的本機 *資源磁碟* 。</span><span class="sxs-lookup"><span data-stu-id="71dcd-146">Each virtual machine has a temporary, local *resource disk* attached.</span></span> <span data-ttu-id="71dcd-147">因為資源磁碟上的資料在重新開機之後就會消失，通常供虛擬機器中執行的應用程式和處理程序 **暫時** 儲存資料。</span><span class="sxs-lookup"><span data-stu-id="71dcd-147">Because data on a resource disk may not be durable across reboots, it is often used by applications and processes running in the virtual machine for transient and **temporary** storage of data.</span></span> <span data-ttu-id="71dcd-148">也用來儲存作業系統的分頁檔或交換檔。</span><span class="sxs-lookup"><span data-stu-id="71dcd-148">It is also used to store the page or swap files for the operating system.</span></span>

<span data-ttu-id="71dcd-149">在 Linux 上，資源磁碟通常由 Azure Linux 代理程式管理，並自動掛接到 **/mnt/resource** (或 Ubuntu 映像中的 **/mnt**)。</span><span class="sxs-lookup"><span data-stu-id="71dcd-149">On Linux, the resource disk is typically managed by the Azure Linux Agent and automatically mounted to **/mnt/resource** (or **/mnt** on Ubuntu images).</span></span>

> [!NOTE]
> <span data-ttu-id="71dcd-150">請注意，資源磁碟是 **暫存** 磁碟，可能會在 VM 重新開機時遭到刪除及重新格式化。</span><span class="sxs-lookup"><span data-stu-id="71dcd-150">Note that the resource disk is a **temporary** disk, and might be deleted and reformatted when the VM is rebooted.</span></span>
> 
> 

<span data-ttu-id="71dcd-151">在 Linux 上，核心可能會將資料磁碟命名為 `/dev/sdc`，而使用者必須分割、格式化及掛接該資源。</span><span class="sxs-lookup"><span data-stu-id="71dcd-151">On Linux the data disk might be named by the kernel as `/dev/sdc`, and users will need to partition, format and mount that resource.</span></span> <span data-ttu-id="71dcd-152">[如何將資料磁碟連接至虛擬機器](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)的教學課程中涵蓋這部分的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="71dcd-152">This is covered step-by-step in the tutorial: [How to Attach a Data Disk to a Virtual Machine](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

* <span data-ttu-id="71dcd-153">**另請參閱︰**[Linux 上設定軟體 RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)  &  [設定 Azure 中 Linux VM 的 LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="71dcd-153">**See also:** [Configure Software RAID on Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [Configure LVM on a Linux VM in Azure](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

