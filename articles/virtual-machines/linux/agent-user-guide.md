---
title: "Azure Linux VM 代理程式概觀 | Microsoft Docs"
description: "了解如何安裝和設定 Linux 代理程式 (waagent)，來管理虛擬機器與 Azure 網狀架構控制器之間的互動。"
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486ad6bb148583a957fb82b7954ff94f853b12cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="understanding-and-using-the-azure-linux-agent"></a><span data-ttu-id="f034f-103">了解與使用 Azure Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="f034f-103">Understanding and using the Azure Linux Agent</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a><span data-ttu-id="f034f-104">簡介</span><span class="sxs-lookup"><span data-stu-id="f034f-104">Introduction</span></span>
<span data-ttu-id="f034f-105">Microsoft Azure Linux 代理程式 (waagent) 管理 Linux 與 FreeBSD 佈建，以及 VM 與 Azure 網狀架構控制器之間的互動。</span><span class="sxs-lookup"><span data-stu-id="f034f-105">The Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with the Azure Fabric Controller.</span></span> <span data-ttu-id="f034f-106">它為 Linux 和 FreeBSD IaaS 部署提供下列功能：</span><span class="sxs-lookup"><span data-stu-id="f034f-106">It provides the following functionality for Linux and FreeBSD IaaS deployments:</span></span>

> [!NOTE]
> <span data-ttu-id="f034f-107">如需詳細資訊，請參閱 Azure Linux 代理程式[讀我檔案](https://github.com/Azure/WALinuxAgent/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="f034f-107">See the Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span></span>
> 
> 

* <span data-ttu-id="f034f-108">**映像佈建**</span><span class="sxs-lookup"><span data-stu-id="f034f-108">**Image Provisioning**</span></span>
  
  * <span data-ttu-id="f034f-109">建立使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="f034f-109">Creation of a user account</span></span>
  * <span data-ttu-id="f034f-110">設定 SSH 驗證類型</span><span class="sxs-lookup"><span data-stu-id="f034f-110">Configuring SSH authentication types</span></span>
  * <span data-ttu-id="f034f-111">部署 SSH 公開金鑰和金鑰組</span><span class="sxs-lookup"><span data-stu-id="f034f-111">Deployment of SSH public keys and key pairs</span></span>
  * <span data-ttu-id="f034f-112">設定主機名稱</span><span class="sxs-lookup"><span data-stu-id="f034f-112">Setting the host name</span></span>
  * <span data-ttu-id="f034f-113">將主機名稱發佈至平台 DNS</span><span class="sxs-lookup"><span data-stu-id="f034f-113">Publishing the host name to the platform DNS</span></span>
  * <span data-ttu-id="f034f-114">將 SSH 主機金鑰和指紋報告給平台</span><span class="sxs-lookup"><span data-stu-id="f034f-114">Reporting SSH host key fingerprint to the platform</span></span>
  * <span data-ttu-id="f034f-115">資源磁碟管理</span><span class="sxs-lookup"><span data-stu-id="f034f-115">Resource Disk Management</span></span>
  * <span data-ttu-id="f034f-116">格式化和掛接資源磁碟</span><span class="sxs-lookup"><span data-stu-id="f034f-116">Formatting and mounting the resource disk</span></span>
  * <span data-ttu-id="f034f-117">設定交換空間</span><span class="sxs-lookup"><span data-stu-id="f034f-117">Configuring swap space</span></span>
* <span data-ttu-id="f034f-118">**網路功能**</span><span class="sxs-lookup"><span data-stu-id="f034f-118">**Networking**</span></span>
  
  * <span data-ttu-id="f034f-119">管理路由以提高平台 DHCP 伺服器的相容性</span><span class="sxs-lookup"><span data-stu-id="f034f-119">Manages routes to improve compatibility with platform DHCP servers</span></span>
  * <span data-ttu-id="f034f-120">確保網路介面名稱的穩定性</span><span class="sxs-lookup"><span data-stu-id="f034f-120">Ensures the stability of the network interface name</span></span>
* <span data-ttu-id="f034f-121">**核心**</span><span class="sxs-lookup"><span data-stu-id="f034f-121">**Kernel**</span></span>
  
  * <span data-ttu-id="f034f-122">設定虛擬 NUMA (核心 < 2.6.37 時停用)</span><span class="sxs-lookup"><span data-stu-id="f034f-122">Configures virtual NUMA (disable for kernel <2.6.37)</span></span>
  * <span data-ttu-id="f034f-123">取用 /dev/random 的 Hyper-V Entropy</span><span class="sxs-lookup"><span data-stu-id="f034f-123">Consumes Hyper-V entropy for /dev/random</span></span>
  * <span data-ttu-id="f034f-124">設定根裝置 (可能在遠端) 的 SCSI 逾時</span><span class="sxs-lookup"><span data-stu-id="f034f-124">Configures SCSI timeouts for the root device (which could be remote)</span></span>
* <span data-ttu-id="f034f-125">**診斷**</span><span class="sxs-lookup"><span data-stu-id="f034f-125">**Diagnostics**</span></span>
  
  * <span data-ttu-id="f034f-126">將主控台重新導向至序列埠</span><span class="sxs-lookup"><span data-stu-id="f034f-126">Console redirection to the serial port</span></span>
* <span data-ttu-id="f034f-127">**SCVMM 部署**</span><span class="sxs-lookup"><span data-stu-id="f034f-127">**SCVMM Deployments**</span></span>
  
  * <span data-ttu-id="f034f-128">在 System Center Virtual Machine Manager 2012 R2 環境中執行時偵測和啟動 Linux 的 VMM 代理程式</span><span class="sxs-lookup"><span data-stu-id="f034f-128">Detects and bootstraps the VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span></span>
* <span data-ttu-id="f034f-129">**VM 延伸模組**</span><span class="sxs-lookup"><span data-stu-id="f034f-129">**VM Extension**</span></span>
  
  * <span data-ttu-id="f034f-130">將 Microsoft 和合作夥伴所撰寫的元件插入 Linux VM (IaaS)，以啟用軟體和設定自動化 </span><span class="sxs-lookup"><span data-stu-id="f034f-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) to enable software and configuration automation</span></span>
  * <span data-ttu-id="f034f-131">VM 延伸模組參考實作，網址為 [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span><span class="sxs-lookup"><span data-stu-id="f034f-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span></span>

## <a name="communication"></a><span data-ttu-id="f034f-132">通訊</span><span class="sxs-lookup"><span data-stu-id="f034f-132">Communication</span></span>
<span data-ttu-id="f034f-133">資訊經由兩個管道從平台流向代理程式：</span><span class="sxs-lookup"><span data-stu-id="f034f-133">The information flow from the platform to the agent occurs via two channels:</span></span>

* <span data-ttu-id="f034f-134">在 IaaS 部署中，開機時連接的 DVD。</span><span class="sxs-lookup"><span data-stu-id="f034f-134">A boot-time attached DVD for IaaS deployments.</span></span> <span data-ttu-id="f034f-135">此 DVD 包含 OVF 相容組態檔，內含實際 SSH 金鑰組以外的所有佈建資訊。</span><span class="sxs-lookup"><span data-stu-id="f034f-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than the actual SSH keypairs.</span></span>
* <span data-ttu-id="f034f-136">TCP 端點，公開可用來取得部署和拓撲組態的 REST API。</span><span class="sxs-lookup"><span data-stu-id="f034f-136">A TCP endpoint exposing a REST API used to obtain deployment and topology configuration.</span></span>

## <a name="requirements"></a><span data-ttu-id="f034f-137">需求</span><span class="sxs-lookup"><span data-stu-id="f034f-137">Requirements</span></span>
<span data-ttu-id="f034f-138">下列系統已經過測試，且已知可與 Azure Linux 代理程式一同運作：</span><span class="sxs-lookup"><span data-stu-id="f034f-138">The following systems have been tested and are known to work with the Azure Linux Agent:</span></span>

> [!NOTE]
> <span data-ttu-id="f034f-139">這份清單可能與 Microsoft Azure 平台上官方的支援系統清單不同，如下所述：[http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span><span class="sxs-lookup"><span data-stu-id="f034f-139">This list may differ from the official list of supported systems on the Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span></span>
> 
> 

* <span data-ttu-id="f034f-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f034f-140">CoreOS</span></span>
* <span data-ttu-id="f034f-141">CentOS 6.3+</span><span class="sxs-lookup"><span data-stu-id="f034f-141">CentOS 6.3+</span></span>
* <span data-ttu-id="f034f-142">Red Hat Enterprise Linux 6.7+</span><span class="sxs-lookup"><span data-stu-id="f034f-142">Red Hat Enterprise Linux 6.7+</span></span>
* <span data-ttu-id="f034f-143">Debian 7.0+</span><span class="sxs-lookup"><span data-stu-id="f034f-143">Debian 7.0+</span></span>
* <span data-ttu-id="f034f-144">Ubuntu 12.04+</span><span class="sxs-lookup"><span data-stu-id="f034f-144">Ubuntu 12.04+</span></span>
* <span data-ttu-id="f034f-145">openSUSE 12.3+</span><span class="sxs-lookup"><span data-stu-id="f034f-145">openSUSE 12.3+</span></span>
* <span data-ttu-id="f034f-146">SLES 11 SP3+</span><span class="sxs-lookup"><span data-stu-id="f034f-146">SLES 11 SP3+</span></span>
* <span data-ttu-id="f034f-147">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="f034f-147">Oracle Linux 6.4+</span></span>

<span data-ttu-id="f034f-148">其他支援的系統：</span><span class="sxs-lookup"><span data-stu-id="f034f-148">Other Supported Systems:</span></span>

* <span data-ttu-id="f034f-149">FreeBSD 10+ (Azure Linux 代理程式 v2.0.10+)</span><span class="sxs-lookup"><span data-stu-id="f034f-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span></span>

<span data-ttu-id="f034f-150">Linux 代理程式需要一些系統封裝才能正確運作：</span><span class="sxs-lookup"><span data-stu-id="f034f-150">The Linux agent depends on some system packages in order to function properly:</span></span>

* <span data-ttu-id="f034f-151">Python 2.6+</span><span class="sxs-lookup"><span data-stu-id="f034f-151">Python 2.6+</span></span>
* <span data-ttu-id="f034f-152">OpenSSL 1.0+</span><span class="sxs-lookup"><span data-stu-id="f034f-152">OpenSSL 1.0+</span></span>
* <span data-ttu-id="f034f-153">OpenSSH 5.3+</span><span class="sxs-lookup"><span data-stu-id="f034f-153">OpenSSH 5.3+</span></span>
* <span data-ttu-id="f034f-154">檔案系統公用程式：sfdisk、fdisk、mkfs、parted</span><span class="sxs-lookup"><span data-stu-id="f034f-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span></span>
* <span data-ttu-id="f034f-155">密碼工具：chpasswd、sudo</span><span class="sxs-lookup"><span data-stu-id="f034f-155">Password tools: chpasswd, sudo</span></span>
* <span data-ttu-id="f034f-156">文字處理工具：sed、grep</span><span class="sxs-lookup"><span data-stu-id="f034f-156">Text processing tools: sed, grep</span></span>
* <span data-ttu-id="f034f-157">網路工具：ip-route</span><span class="sxs-lookup"><span data-stu-id="f034f-157">Network tools: ip-route</span></span>
* <span data-ttu-id="f034f-158">掛接 UDF 檔案系統的核心支援。</span><span class="sxs-lookup"><span data-stu-id="f034f-158">Kernel support for mounting UDF filesystems.</span></span>

## <a name="installation"></a><span data-ttu-id="f034f-159">安裝</span><span class="sxs-lookup"><span data-stu-id="f034f-159">Installation</span></span>
<span data-ttu-id="f034f-160">安裝和升級 Azure Linux 代理程式時，建議使用散發套件的封裝儲存機制所提供的 RPM 或 DEB 封裝來安裝。</span><span class="sxs-lookup"><span data-stu-id="f034f-160">Installation using an RPM or a DEB package from your distribution's package repository is the preferred method of installing and upgrading the Azure Linux Agent.</span></span> <span data-ttu-id="f034f-161">所有[認可的散發套件提供者](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)都會將 Azure Linux 代理程式套件整合於本身的映像和儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="f034f-161">All the [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate the Azure Linux agent package into their images and repositories.</span></span>

<span data-ttu-id="f034f-162">如需了解進階安裝選項，例如從來源安裝或安裝到自訂的位置或前置詞，請參閱 [GitHub 上 Azure Linux 代理程式存放庫](https://github.com/Azure/WALinuxAgent)中的文件。</span><span class="sxs-lookup"><span data-stu-id="f034f-162">Refer to the documentation in the [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or to custom locations or prefixes.</span></span>

## <a name="command-line-options"></a><span data-ttu-id="f034f-163">命令列選項</span><span class="sxs-lookup"><span data-stu-id="f034f-163">Command Line Options</span></span>
### <a name="flags"></a><span data-ttu-id="f034f-164">旗標</span><span class="sxs-lookup"><span data-stu-id="f034f-164">Flags</span></span>
* <span data-ttu-id="f034f-165">verbose：提高指定命令的詳細程度</span><span class="sxs-lookup"><span data-stu-id="f034f-165">verbose: Increase verbosity of specified command</span></span>
* <span data-ttu-id="f034f-166">force：略過某些命令的互動式確認</span><span class="sxs-lookup"><span data-stu-id="f034f-166">force: Skip interactive confirmation for some commands</span></span>

### <a name="commands"></a><span data-ttu-id="f034f-167">命令</span><span class="sxs-lookup"><span data-stu-id="f034f-167">Commands</span></span>
* <span data-ttu-id="f034f-168">help：列出支援的命令和旗標。</span><span class="sxs-lookup"><span data-stu-id="f034f-168">help: Lists the supported commands and flags.</span></span>
* <span data-ttu-id="f034f-169">deprovision：嘗試清理系統，使之適合重新佈建。</span><span class="sxs-lookup"><span data-stu-id="f034f-169">deprovision: Attempt to clean the system and make it suitable for re-provisioning.</span></span> <span data-ttu-id="f034f-170">此作業會刪除下列項目：</span><span class="sxs-lookup"><span data-stu-id="f034f-170">This operation deleted the following:</span></span>
  
  * <span data-ttu-id="f034f-171">所有 SSH 主機金鑰 (如果組態檔中的 Provisioning.RegenerateSshHostKeyPair 是 'y')</span><span class="sxs-lookup"><span data-stu-id="f034f-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in the configuration file)</span></span>
  * <span data-ttu-id="f034f-172">/etc/resolv.conf 中的名稱伺服器設定</span><span class="sxs-lookup"><span data-stu-id="f034f-172">Nameserver configuration in /etc/resolv.conf</span></span>
  * <span data-ttu-id="f034f-173">/etc/shadow 中的根密碼 (如果組態檔中的 Provisioning.DeleteRootPassword 是 'y')</span><span class="sxs-lookup"><span data-stu-id="f034f-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in the configuration file)</span></span>
  * <span data-ttu-id="f034f-174">快取的 DHCP 用戶端租用</span><span class="sxs-lookup"><span data-stu-id="f034f-174">Cached DHCP client leases</span></span>
  * <span data-ttu-id="f034f-175">將主機名稱重設為 localhost.localdomain</span><span class="sxs-lookup"><span data-stu-id="f034f-175">Resets host name to localhost.localdomain</span></span>

> [!WARNING]
> <span data-ttu-id="f034f-176">取消佈建不能保證映像檔中的所有機密資訊都清除完畢而適合再度散發。</span><span class="sxs-lookup"><span data-stu-id="f034f-176">Deprovisioning does not guarantee that the image is cleared of all sensitive information and suitable for redistribution.</span></span>
> 
> 

* <span data-ttu-id="f034f-177">deprovision+user：執行 -deprovision (上述) 下的一切動作，並刪除最後佈建的使用者帳戶 (取自於 /var/lib/waagent) 和相關聯的資料。</span><span class="sxs-lookup"><span data-stu-id="f034f-177">deprovision+user: Performs everything under -deprovision (above) and also deletes the last provisioned user account (obtained from /var/lib/waagent) and associated data.</span></span> <span data-ttu-id="f034f-178">此參數是為了取消佈建 Azure 上先前佈建的映像檔，以便擷取並重複使用。</span><span class="sxs-lookup"><span data-stu-id="f034f-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span></span>
* <span data-ttu-id="f034f-179">version：顯示 waagent 的版本</span><span class="sxs-lookup"><span data-stu-id="f034f-179">version: Displays the version of waagent</span></span>
* <span data-ttu-id="f034f-180">serialconsole：設定 GRUB，以將 ttyS0 (第一個序列埠) 標示為開機主控台。</span><span class="sxs-lookup"><span data-stu-id="f034f-180">serialconsole: Configures GRUB to mark ttyS0 (the first serial port) as the boot console.</span></span> <span data-ttu-id="f034f-181">這可確保將核心開機記錄傳送至序號埠且可用於偵錯。</span><span class="sxs-lookup"><span data-stu-id="f034f-181">This ensures that kernel bootup logs are sent to the serial port and made available for debugging.</span></span>
* <span data-ttu-id="f034f-182">daemon：以精靈方式執行 waagent 來管理與平台之間的互動。</span><span class="sxs-lookup"><span data-stu-id="f034f-182">daemon: Run waagent as a daemon to manage interaction with the platform.</span></span> <span data-ttu-id="f034f-183">此引數是在 waagent init 指令碼中指定給 waagent。</span><span class="sxs-lookup"><span data-stu-id="f034f-183">This argument is specified to waagent in the waagent init script.</span></span>
* <span data-ttu-id="f034f-184">開始︰以背景處理序方式執行 waagent</span><span class="sxs-lookup"><span data-stu-id="f034f-184">start: Run waagent as a background process</span></span>

## <a name="configuration"></a><span data-ttu-id="f034f-185">組態</span><span class="sxs-lookup"><span data-stu-id="f034f-185">Configuration</span></span>
<span data-ttu-id="f034f-186">組態檔 (/etc/waagent.conf) 控制 waagent 的動作。</span><span class="sxs-lookup"><span data-stu-id="f034f-186">A configuration file (/etc/waagent.conf) controls the actions of waagent.</span></span> <span data-ttu-id="f034f-187">範例組態檔如下所示：</span><span class="sxs-lookup"><span data-stu-id="f034f-187">A sample configuration file is shown below:</span></span>

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

<span data-ttu-id="f034f-188">以下詳細說明各種組態選項。</span><span class="sxs-lookup"><span data-stu-id="f034f-188">The various configuration options are described in detail below.</span></span> <span data-ttu-id="f034f-189">組態選項可分成三種：布林、字串或整數。</span><span class="sxs-lookup"><span data-stu-id="f034f-189">Configuration options are of three types; Boolean, String or Integer.</span></span> <span data-ttu-id="f034f-190">布林組態選項可指定為 "y" 或 "n"。</span><span class="sxs-lookup"><span data-stu-id="f034f-190">The Boolean configuration options can be specified as "y" or "n".</span></span> <span data-ttu-id="f034f-191">特殊關鍵字 "None" 可用於某些字串類型組態項目，詳述如下。</span><span class="sxs-lookup"><span data-stu-id="f034f-191">The special keyword "None" may be used for some string type configuration entries as detailed below.</span></span>

<span data-ttu-id="f034f-192">**Provisioning.Enabled：**</span><span class="sxs-lookup"><span data-stu-id="f034f-192">**Provisioning.Enabled:**</span></span>  
<span data-ttu-id="f034f-193">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="f034f-193">Type: Boolean</span></span>  
<span data-ttu-id="f034f-194">預設：y</span><span class="sxs-lookup"><span data-stu-id="f034f-194">Default: y</span></span>

<span data-ttu-id="f034f-195">這可讓使用者啟用或停用代理程式的佈建功能。</span><span class="sxs-lookup"><span data-stu-id="f034f-195">This allows the user to enable or disable the provisioning functionality in the agent.</span></span> <span data-ttu-id="f034f-196">有效值為 "y" 或 "n"。</span><span class="sxs-lookup"><span data-stu-id="f034f-196">Valid values are "y" or "n".</span></span> <span data-ttu-id="f034f-197">如果停用佈建，則會保留映像檔中的 SSH 主機金鑰和使用者金鑰，並忽略 Azure 佈建 API 中指定的任何組態。</span><span class="sxs-lookup"><span data-stu-id="f034f-197">If provisioning is disabled, SSH host and user keys in the image are preserved and any configuration specified in the Azure provisioning API is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="f034f-198">針對使用 cloud-init 執行佈建工作的 Ubuntu 雲端映像，`Provisioning.Enabled` 參數的預設值為 "n"。</span><span class="sxs-lookup"><span data-stu-id="f034f-198">The `Provisioning.Enabled` parameter defaults to "n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span></span>
> 
> 

<span data-ttu-id="f034f-199">**Provisioning.DeleteRootPassword：**</span><span class="sxs-lookup"><span data-stu-id="f034f-199">**Provisioning.DeleteRootPassword:**</span></span>  
<span data-ttu-id="f034f-200">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="f034f-200">Type: Boolean</span></span>  
<span data-ttu-id="f034f-201">預設：n</span><span class="sxs-lookup"><span data-stu-id="f034f-201">Default: n</span></span>

<span data-ttu-id="f034f-202">如果設定，則佈建過程中會清除 /etc/shadow 檔案中的根密碼。</span><span class="sxs-lookup"><span data-stu-id="f034f-202">If set, the root password in the /etc/shadow file is erased during the provisioning process.</span></span>

<span data-ttu-id="f034f-203">**Provisioning.RegenerateSshHostKeyPair：**</span><span class="sxs-lookup"><span data-stu-id="f034f-203">**Provisioning.RegenerateSshHostKeyPair:**</span></span>  
<span data-ttu-id="f034f-204">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="f034f-204">Type: Boolean</span></span>  
<span data-ttu-id="f034f-205">預設：y</span><span class="sxs-lookup"><span data-stu-id="f034f-205">Default: y</span></span>

<span data-ttu-id="f034f-206">如果設定，則佈建過程會從 /etc/ssh/ 中刪除所有 SSH 主機金鑰組 (ecdsa、dsa 和 rsa)。</span><span class="sxs-lookup"><span data-stu-id="f034f-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during the provisioning process from /etc/ssh/.</span></span> <span data-ttu-id="f034f-207">還會產生單一全新的金鑰組。</span><span class="sxs-lookup"><span data-stu-id="f034f-207">And a single fresh key pair is generated.</span></span>

<span data-ttu-id="f034f-208">全新金鑰組的加密類型可由 Provisioning.SshHostKeyPairType 項目來設定。</span><span class="sxs-lookup"><span data-stu-id="f034f-208">The encryption type for the fresh key pair is configurable by the Provisioning.SshHostKeyPairType entry.</span></span> <span data-ttu-id="f034f-209">請注意，重新啟動 SSH 精靈時 (例如重新開機時)，某些散發套件會針對任何遺失的加密類型而重建 SSH 金鑰組。</span><span class="sxs-lookup"><span data-stu-id="f034f-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when the SSH daemon is restarted (for example, upon a reboot).</span></span>

<span data-ttu-id="f034f-210">**Provisioning.SshHostKeyPairType：**</span><span class="sxs-lookup"><span data-stu-id="f034f-210">**Provisioning.SshHostKeyPairType:**</span></span>  
<span data-ttu-id="f034f-211">類型：字串</span><span class="sxs-lookup"><span data-stu-id="f034f-211">Type: String</span></span>  
<span data-ttu-id="f034f-212">預設：rsa</span><span class="sxs-lookup"><span data-stu-id="f034f-212">Default: rsa</span></span>

<span data-ttu-id="f034f-213">這可設為虛擬機器上的 SSH 精靈所支援的加密演算法類型。</span><span class="sxs-lookup"><span data-stu-id="f034f-213">This can be set to an encryption algorithm type that is supported by the SSH daemon on the virtual machine.</span></span> <span data-ttu-id="f034f-214">支援的值通常為 "rsa"、"dsa" 和 "ecdsa"。</span><span class="sxs-lookup"><span data-stu-id="f034f-214">The typically supported values are "rsa", "dsa" and "ecdsa".</span></span> <span data-ttu-id="f034f-215">請注意，Windows 的 "putty.exe" 不支援 "ecdsa"。</span><span class="sxs-lookup"><span data-stu-id="f034f-215">Note that "putty.exe" on Windows does not support "ecdsa".</span></span> <span data-ttu-id="f034f-216">因此，如果想要在 Windows 上使用 putty.exe 來連線至 Linux 部署，請使用 "rsa" 或 "dsa"。</span><span class="sxs-lookup"><span data-stu-id="f034f-216">So, if you intend to use putty.exe on Windows to connect to a Linux deployment, please use "rsa" or "dsa".</span></span>

<span data-ttu-id="f034f-217">**Provisioning.MonitorHostName：**</span><span class="sxs-lookup"><span data-stu-id="f034f-217">**Provisioning.MonitorHostName:**</span></span>  
<span data-ttu-id="f034f-218">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="f034f-218">Type: Boolean</span></span>  
<span data-ttu-id="f034f-219">預設：y</span><span class="sxs-lookup"><span data-stu-id="f034f-219">Default: y</span></span>

<span data-ttu-id="f034f-220">如果設定，waagent 會監視 Linux 虛擬機器的主機名稱有無變動 (由 "hostname" 命令傳回)，並自動更新映像檔中的網路組態來反映此變動。</span><span class="sxs-lookup"><span data-stu-id="f034f-220">If set, waagent will monitor the Linux virtual machine for hostname changes (as returned by the "hostname" command) and automatically update the networking configuration in the image to reflect the change.</span></span> <span data-ttu-id="f034f-221">為了將名稱變更發送至 DNS 伺服器，虛擬機器中將重新啟動網路功能。</span><span class="sxs-lookup"><span data-stu-id="f034f-221">In order to push the name change to the DNS servers, networking will be restarted in the virtual machine.</span></span> <span data-ttu-id="f034f-222">這會導致網際網路連線短暫中斷。</span><span class="sxs-lookup"><span data-stu-id="f034f-222">This will result in brief loss of Internet connectivity.</span></span>

<span data-ttu-id="f034f-223">**Provisioning.DecodeCustomData**</span><span class="sxs-lookup"><span data-stu-id="f034f-223">**Provisioning.DecodeCustomData**</span></span>  
<span data-ttu-id="f034f-224">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="f034f-224">Type: Boolean</span></span>  
<span data-ttu-id="f034f-225">預設：n</span><span class="sxs-lookup"><span data-stu-id="f034f-225">Default: n</span></span>

<span data-ttu-id="f034f-226">如果設定，waagent 會從 CustomData 將 Base64 解碼。</span><span class="sxs-lookup"><span data-stu-id="f034f-226">If set, waagent will decode CustomData from Base64.</span></span>

<span data-ttu-id="f034f-227">**Provisioning.ExecuteCustomData**</span><span class="sxs-lookup"><span data-stu-id="f034f-227">**Provisioning.ExecuteCustomData**</span></span>  
<span data-ttu-id="f034f-228">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="f034f-228">Type: Boolean</span></span>  
<span data-ttu-id="f034f-229">預設：n</span><span class="sxs-lookup"><span data-stu-id="f034f-229">Default: n</span></span>

<span data-ttu-id="f034f-230">如果設定，waagent 將在佈建之後執行 CustomData。</span><span class="sxs-lookup"><span data-stu-id="f034f-230">If set, waagent will execute CustomData after provisioning.</span></span>

<span data-ttu-id="f034f-231">**Provisioning.PasswordCryptId**</span><span class="sxs-lookup"><span data-stu-id="f034f-231">**Provisioning.PasswordCryptId**</span></span>  
<span data-ttu-id="f034f-232">型別︰字串</span><span class="sxs-lookup"><span data-stu-id="f034f-232">Type:String</span></span>  
<span data-ttu-id="f034f-233">預設︰6</span><span class="sxs-lookup"><span data-stu-id="f034f-233">Default:6</span></span>

<span data-ttu-id="f034f-234">產生密碼雜湊時由 crypt 使用的演算法。</span><span class="sxs-lookup"><span data-stu-id="f034f-234">Algorithm used by crypt when generating password hash.</span></span>  
 <span data-ttu-id="f034f-235">1 - MD5</span><span class="sxs-lookup"><span data-stu-id="f034f-235">1 - MD5</span></span>  
 <span data-ttu-id="f034f-236">2a - Blowfish</span><span class="sxs-lookup"><span data-stu-id="f034f-236">2a - Blowfish</span></span>  
 <span data-ttu-id="f034f-237">5-SHA-256</span><span class="sxs-lookup"><span data-stu-id="f034f-237">5 - SHA-256</span></span>  
 <span data-ttu-id="f034f-238">6 - SHA-512</span><span class="sxs-lookup"><span data-stu-id="f034f-238">6 - SHA-512</span></span>  

<span data-ttu-id="f034f-239">**Provisioning.PasswordCryptSaltLength**</span><span class="sxs-lookup"><span data-stu-id="f034f-239">**Provisioning.PasswordCryptSaltLength**</span></span>  
<span data-ttu-id="f034f-240">型別︰字串</span><span class="sxs-lookup"><span data-stu-id="f034f-240">Type:String</span></span>  
<span data-ttu-id="f034f-241">預設值︰10</span><span class="sxs-lookup"><span data-stu-id="f034f-241">Default:10</span></span>

<span data-ttu-id="f034f-242">產生密碼雜湊時使用的隨機 salt 長度。</span><span class="sxs-lookup"><span data-stu-id="f034f-242">Length of random salt used when generating password hash.</span></span>

<span data-ttu-id="f034f-243">**ResourceDisk.Format：**</span><span class="sxs-lookup"><span data-stu-id="f034f-243">**ResourceDisk.Format:**</span></span>  
<span data-ttu-id="f034f-244">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="f034f-244">Type: Boolean</span></span>  
<span data-ttu-id="f034f-245">預設：y</span><span class="sxs-lookup"><span data-stu-id="f034f-245">Default: y</span></span>

<span data-ttu-id="f034f-246">如果設定，如果使用者在 "ResourceDisk.Filesystem" 中要求的檔案系統類型不是 "ntfs"，則 waagent 會格式化並掛接平台所提供的資源磁碟。</span><span class="sxs-lookup"><span data-stu-id="f034f-246">If set, the resource disk provided by the platform will be formatted and mounted by waagent if the filesystem type requested by the user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span></span> <span data-ttu-id="f034f-247">磁碟上將會有 Linux (83) 類型的單一磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="f034f-247">A single partition of type Linux (83) will be made available on the disk.</span></span> <span data-ttu-id="f034f-248">請注意，如果可順利掛接此磁碟分割，則不會格式化。</span><span class="sxs-lookup"><span data-stu-id="f034f-248">Note that this partition will not be formatted if it can be successfully mounted.</span></span>

<span data-ttu-id="f034f-249">**ResourceDisk.Filesystem：**</span><span class="sxs-lookup"><span data-stu-id="f034f-249">**ResourceDisk.Filesystem:**</span></span>  
<span data-ttu-id="f034f-250">類型：字串</span><span class="sxs-lookup"><span data-stu-id="f034f-250">Type: String</span></span>  
<span data-ttu-id="f034f-251">預設：ext4</span><span class="sxs-lookup"><span data-stu-id="f034f-251">Default: ext4</span></span>

<span data-ttu-id="f034f-252">這指定資源磁碟的檔案系統類型。</span><span class="sxs-lookup"><span data-stu-id="f034f-252">This specifies the filesystem type for the resource disk.</span></span> <span data-ttu-id="f034f-253">支援的值隨 Linux 散發套件而不同。</span><span class="sxs-lookup"><span data-stu-id="f034f-253">Supported values vary by Linux distribution.</span></span> <span data-ttu-id="f034f-254">如果字串為 X，則 Linux 映像檔上應該會出現 mkfs.X。</span><span class="sxs-lookup"><span data-stu-id="f034f-254">If the string is X, then mkfs.X should be present on the Linux image.</span></span> <span data-ttu-id="f034f-255">SLES 11 映像檔通常會使用 'ext3'。</span><span class="sxs-lookup"><span data-stu-id="f034f-255">SLES 11 images should typically use 'ext3'.</span></span> <span data-ttu-id="f034f-256">在此，FreeBSD 映像檔應該是使用 'ufs2'。</span><span class="sxs-lookup"><span data-stu-id="f034f-256">FreeBSD images should use 'ufs2' here.</span></span>

<span data-ttu-id="f034f-257">**ResourceDisk.MountPoint：**</span><span class="sxs-lookup"><span data-stu-id="f034f-257">**ResourceDisk.MountPoint:**</span></span>  
<span data-ttu-id="f034f-258">類型：字串</span><span class="sxs-lookup"><span data-stu-id="f034f-258">Type: String</span></span>  
<span data-ttu-id="f034f-259">預設值：/mnt/resource</span><span class="sxs-lookup"><span data-stu-id="f034f-259">Default: /mnt/resource</span></span> 

<span data-ttu-id="f034f-260">這指定資源磁碟的掛接路徑。</span><span class="sxs-lookup"><span data-stu-id="f034f-260">This specifies the path at which the resource disk is mounted.</span></span> <span data-ttu-id="f034f-261">請注意，資源磁碟是 *暫存* 磁碟，可能會在 VM 取消佈建時清空。</span><span class="sxs-lookup"><span data-stu-id="f034f-261">Note that the resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span>

<span data-ttu-id="f034f-262">**ResourceDisk.MountOptions**</span><span class="sxs-lookup"><span data-stu-id="f034f-262">**ResourceDisk.MountOptions**</span></span>  
<span data-ttu-id="f034f-263">類型：字串</span><span class="sxs-lookup"><span data-stu-id="f034f-263">Type: String</span></span>  
<span data-ttu-id="f034f-264">預設值︰無</span><span class="sxs-lookup"><span data-stu-id="f034f-264">Default: None</span></span>

<span data-ttu-id="f034f-265">指定要傳遞至 mount -o 指令的磁碟掛接選項。</span><span class="sxs-lookup"><span data-stu-id="f034f-265">Specifies disk mount options to be passed to the mount -o command.</span></span> <span data-ttu-id="f034f-266">這是以逗號分隔的值清單，例如：</span><span class="sxs-lookup"><span data-stu-id="f034f-266">This is a comma separated list of values, ex.</span></span> <span data-ttu-id="f034f-267">'nodev,nosuid'。</span><span class="sxs-lookup"><span data-stu-id="f034f-267">'nodev,nosuid'.</span></span> <span data-ttu-id="f034f-268">如需詳細資訊，請參閱 Mount(8)。</span><span class="sxs-lookup"><span data-stu-id="f034f-268">See mount(8) for details.</span></span>

<span data-ttu-id="f034f-269">**ResourceDisk.EnableSwap：**</span><span class="sxs-lookup"><span data-stu-id="f034f-269">**ResourceDisk.EnableSwap:**</span></span>  
<span data-ttu-id="f034f-270">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="f034f-270">Type: Boolean</span></span>  
<span data-ttu-id="f034f-271">預設：n</span><span class="sxs-lookup"><span data-stu-id="f034f-271">Default: n</span></span>

<span data-ttu-id="f034f-272">如果設定，則會在資源磁碟上建立交換檔 (/swapfile) 並加入至系統交換空間。</span><span class="sxs-lookup"><span data-stu-id="f034f-272">If set, a swap file (/swapfile) is created on the resource disk and added to the system swap space.</span></span>

<span data-ttu-id="f034f-273">**ResourceDisk.SwapSizeMB：**</span><span class="sxs-lookup"><span data-stu-id="f034f-273">**ResourceDisk.SwapSizeMB:**</span></span>  
<span data-ttu-id="f034f-274">型別︰整數</span><span class="sxs-lookup"><span data-stu-id="f034f-274">Type: Integer</span></span>  
<span data-ttu-id="f034f-275">預設值：0</span><span class="sxs-lookup"><span data-stu-id="f034f-275">Default: 0</span></span>

<span data-ttu-id="f034f-276">交換檔的大小 (MB)。</span><span class="sxs-lookup"><span data-stu-id="f034f-276">The size of the swap file in megabytes.</span></span>

<span data-ttu-id="f034f-277">**Logs.Verbose：**</span><span class="sxs-lookup"><span data-stu-id="f034f-277">**Logs.Verbose:**</span></span>  
<span data-ttu-id="f034f-278">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="f034f-278">Type: Boolean</span></span>  
<span data-ttu-id="f034f-279">預設：n</span><span class="sxs-lookup"><span data-stu-id="f034f-279">Default: n</span></span>

<span data-ttu-id="f034f-280">如果設定，則記錄詳細程度會提高。</span><span class="sxs-lookup"><span data-stu-id="f034f-280">If set, log verbosity is boosted.</span></span> <span data-ttu-id="f034f-281">Waagent 會記錄到 /var/log/waagent.log，並利用系統 logrotate 功能來輪換記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f034f-281">Waagent logs to /var/log/waagent.log and leverages the system logrotate functionality to rotate logs.</span></span>

<span data-ttu-id="f034f-282">**OS.EnableRDMA**</span><span class="sxs-lookup"><span data-stu-id="f034f-282">**OS.EnableRDMA**</span></span>  
<span data-ttu-id="f034f-283">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="f034f-283">Type: Boolean</span></span>  
<span data-ttu-id="f034f-284">預設：n</span><span class="sxs-lookup"><span data-stu-id="f034f-284">Default: n</span></span>

<span data-ttu-id="f034f-285">如果設定，該代理程式將嘗試安裝並載入 RDMA 核心驅動程式，這個驅動程式與基礎硬體上的軔體版本相符。</span><span class="sxs-lookup"><span data-stu-id="f034f-285">If set, the agent will attempt to install and then load an RDMA kernel driver that matches the version of the firmware on the underlying hardware.</span></span>

<span data-ttu-id="f034f-286">**OS.RootDeviceScsiTimeout：**</span><span class="sxs-lookup"><span data-stu-id="f034f-286">**OS.RootDeviceScsiTimeout:**</span></span>  
<span data-ttu-id="f034f-287">型別︰整數</span><span class="sxs-lookup"><span data-stu-id="f034f-287">Type: Integer</span></span>  
<span data-ttu-id="f034f-288">預設值︰300</span><span class="sxs-lookup"><span data-stu-id="f034f-288">Default: 300</span></span>

<span data-ttu-id="f034f-289">這會在 OS 磁碟和資料磁碟機上設定 SCSI 逾時 (以秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="f034f-289">This configures the SCSI timeout in seconds on the OS disk and data drives.</span></span> <span data-ttu-id="f034f-290">如果未設定，則會使用系統預設值。</span><span class="sxs-lookup"><span data-stu-id="f034f-290">If not set, the system defaults are used.</span></span>

<span data-ttu-id="f034f-291">**OS.OpensslPath：**</span><span class="sxs-lookup"><span data-stu-id="f034f-291">**OS.OpensslPath:**</span></span>  
<span data-ttu-id="f034f-292">類型：字串</span><span class="sxs-lookup"><span data-stu-id="f034f-292">Type: String</span></span>  
<span data-ttu-id="f034f-293">預設值︰無</span><span class="sxs-lookup"><span data-stu-id="f034f-293">Default: None</span></span>

<span data-ttu-id="f034f-294">這可用來指定加密作業使用的 openssl 二進位檔的替代路徑。</span><span class="sxs-lookup"><span data-stu-id="f034f-294">This can be used to specify an alternate path for the openssl binary to use for cryptographic operations.</span></span>

<span data-ttu-id="f034f-295">**HttpProxy.Host, HttpProxy.Port**</span><span class="sxs-lookup"><span data-stu-id="f034f-295">**HttpProxy.Host, HttpProxy.Port**</span></span>  
<span data-ttu-id="f034f-296">類型：字串</span><span class="sxs-lookup"><span data-stu-id="f034f-296">Type: String</span></span>  
<span data-ttu-id="f034f-297">預設值︰無</span><span class="sxs-lookup"><span data-stu-id="f034f-297">Default: None</span></span>

<span data-ttu-id="f034f-298">如果設定，代理程式將使用此 Proxy 伺服器存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="f034f-298">If set, the agent will use this proxy server to access the internet.</span></span> 

## <a name="ubuntu-cloud-images"></a><span data-ttu-id="f034f-299">Ubuntu 雲端映像</span><span class="sxs-lookup"><span data-stu-id="f034f-299">Ubuntu Cloud Images</span></span>
<span data-ttu-id="f034f-300">請注意，Ubuntu 雲端映像會利用 [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) 來執行許多組態工作，否則會由 Azure Linux 代理程式來管理。</span><span class="sxs-lookup"><span data-stu-id="f034f-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) to perform many configuration tasks that would otherwise be managed by the Azure Linux Agent.</span></span>  <span data-ttu-id="f034f-301">請注意下列差異：</span><span class="sxs-lookup"><span data-stu-id="f034f-301">Please note the following differences:</span></span>

* <span data-ttu-id="f034f-302">**Provisioning.Enabled** 會在 Ubuntu 雲端映像上預設為 "n"，其會使用 cloud-init 來執行佈建工作。</span><span class="sxs-lookup"><span data-stu-id="f034f-302">**Provisioning.Enabled** defaults to "n" on Ubuntu Cloud Images that use cloud-init to perform provisioning tasks.</span></span>
* <span data-ttu-id="f034f-303">下列組態參數不會在使用 cloud-init 來管理資源磁碟和交換空間的 Ubuntu 雲端映像上產生任何作用：</span><span class="sxs-lookup"><span data-stu-id="f034f-303">The following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init to manage the resource disk and swap space:</span></span>
  
  * <span data-ttu-id="f034f-304">**ResourceDisk.Format**</span><span class="sxs-lookup"><span data-stu-id="f034f-304">**ResourceDisk.Format**</span></span>
  * <span data-ttu-id="f034f-305">**ResourceDisk.Filesystem**</span><span class="sxs-lookup"><span data-stu-id="f034f-305">**ResourceDisk.Filesystem**</span></span>
  * <span data-ttu-id="f034f-306">**ResourceDisk.MountPoint**</span><span class="sxs-lookup"><span data-stu-id="f034f-306">**ResourceDisk.MountPoint**</span></span>
  * <span data-ttu-id="f034f-307">**ResourceDisk.EnableSwap**</span><span class="sxs-lookup"><span data-stu-id="f034f-307">**ResourceDisk.EnableSwap**</span></span>
  * <span data-ttu-id="f034f-308">**ResourceDisk.SwapSizeMB**</span><span class="sxs-lookup"><span data-stu-id="f034f-308">**ResourceDisk.SwapSizeMB**</span></span>
* <span data-ttu-id="f034f-309">請參閱下列資源，以便在佈建期間，於 Ubuntu 雲端映像上設定資源磁碟掛接和交換空間：</span><span class="sxs-lookup"><span data-stu-id="f034f-309">Please see the following resources to configure the resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span></span>
  
  * [<span data-ttu-id="f034f-310">Ubuntu Wiki：設定交換資料分割</span><span class="sxs-lookup"><span data-stu-id="f034f-310">Ubuntu Wiki: Configure Swap Partitions</span></span>](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [<span data-ttu-id="f034f-311">將自訂資料插入 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="f034f-311">Injecting Custom Data into an Azure Virtual Machine</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

