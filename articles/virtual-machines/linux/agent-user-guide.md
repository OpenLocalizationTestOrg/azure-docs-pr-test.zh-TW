---
title: "aaaAzure Linux VM 代理程式概觀 |Microsoft 文件"
description: "深入了解如何 tooinstall 及設定 Linux 代理程式 (waagent) toomanage Azure 網狀架構控制器的虛擬機器的互動。"
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
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a><span data-ttu-id="94c92-103">了解與使用 hello Azure Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="94c92-103">Understanding and using hello Azure Linux Agent</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a><span data-ttu-id="94c92-104">簡介</span><span class="sxs-lookup"><span data-stu-id="94c92-104">Introduction</span></span>
<span data-ttu-id="94c92-105">hello Microsoft Azure Linux 代理程式 (waagent) 管理 Linux 和 FreeBSD 佈建、 和 VM 與 hello Azure 網狀架構控制器之間的互動。</span><span class="sxs-lookup"><span data-stu-id="94c92-105">hello Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="94c92-106">它提供下列功能適用於 Linux 和 FreeBSD IaaS 部署的 hello:</span><span class="sxs-lookup"><span data-stu-id="94c92-106">It provides hello following functionality for Linux and FreeBSD IaaS deployments:</span></span>

> [!NOTE]
> <span data-ttu-id="94c92-107">請參閱 hello Azure Linux 代理程式[讀我檔案](https://github.com/Azure/WALinuxAgent/blob/master/README.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="94c92-107">See hello Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span></span>
> 
> 

* <span data-ttu-id="94c92-108">**映像佈建**</span><span class="sxs-lookup"><span data-stu-id="94c92-108">**Image Provisioning**</span></span>
  
  * <span data-ttu-id="94c92-109">建立使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="94c92-109">Creation of a user account</span></span>
  * <span data-ttu-id="94c92-110">設定 SSH 驗證類型</span><span class="sxs-lookup"><span data-stu-id="94c92-110">Configuring SSH authentication types</span></span>
  * <span data-ttu-id="94c92-111">部署 SSH 公開金鑰和金鑰組</span><span class="sxs-lookup"><span data-stu-id="94c92-111">Deployment of SSH public keys and key pairs</span></span>
  * <span data-ttu-id="94c92-112">設定 hello 主機名稱</span><span class="sxs-lookup"><span data-stu-id="94c92-112">Setting hello host name</span></span>
  * <span data-ttu-id="94c92-113">發行 hello 主機名稱 toohello 平台 DNS</span><span class="sxs-lookup"><span data-stu-id="94c92-113">Publishing hello host name toohello platform DNS</span></span>
  * <span data-ttu-id="94c92-114">報告 SSH 主機金鑰指紋 toohello 平台</span><span class="sxs-lookup"><span data-stu-id="94c92-114">Reporting SSH host key fingerprint toohello platform</span></span>
  * <span data-ttu-id="94c92-115">資源磁碟管理</span><span class="sxs-lookup"><span data-stu-id="94c92-115">Resource Disk Management</span></span>
  * <span data-ttu-id="94c92-116">格式化及裝載 hello 資源磁碟</span><span class="sxs-lookup"><span data-stu-id="94c92-116">Formatting and mounting hello resource disk</span></span>
  * <span data-ttu-id="94c92-117">設定交換空間</span><span class="sxs-lookup"><span data-stu-id="94c92-117">Configuring swap space</span></span>
* <span data-ttu-id="94c92-118">**網路功能**</span><span class="sxs-lookup"><span data-stu-id="94c92-118">**Networking**</span></span>
  
  * <span data-ttu-id="94c92-119">管理路由 tooimprove 相容性與平台 DHCP 伺服器</span><span class="sxs-lookup"><span data-stu-id="94c92-119">Manages routes tooimprove compatibility with platform DHCP servers</span></span>
  * <span data-ttu-id="94c92-120">可確保 hello 穩定性的 hello 網路介面名稱</span><span class="sxs-lookup"><span data-stu-id="94c92-120">Ensures hello stability of hello network interface name</span></span>
* <span data-ttu-id="94c92-121">**核心**</span><span class="sxs-lookup"><span data-stu-id="94c92-121">**Kernel**</span></span>
  
  * <span data-ttu-id="94c92-122">設定虛擬 NUMA (核心 < 2.6.37 時停用)</span><span class="sxs-lookup"><span data-stu-id="94c92-122">Configures virtual NUMA (disable for kernel <2.6.37)</span></span>
  * <span data-ttu-id="94c92-123">取用 /dev/random 的 Hyper-V Entropy</span><span class="sxs-lookup"><span data-stu-id="94c92-123">Consumes Hyper-V entropy for /dev/random</span></span>
  * <span data-ttu-id="94c92-124">設定 hello 根裝置 （這可能是遠端） 的 SCSI 逾時</span><span class="sxs-lookup"><span data-stu-id="94c92-124">Configures SCSI timeouts for hello root device (which could be remote)</span></span>
* <span data-ttu-id="94c92-125">**診斷**</span><span class="sxs-lookup"><span data-stu-id="94c92-125">**Diagnostics**</span></span>
  
  * <span data-ttu-id="94c92-126">主控台重新導向 toohello 序列連接埠</span><span class="sxs-lookup"><span data-stu-id="94c92-126">Console redirection toohello serial port</span></span>
* <span data-ttu-id="94c92-127">**SCVMM 部署**</span><span class="sxs-lookup"><span data-stu-id="94c92-127">**SCVMM Deployments**</span></span>
  
  * <span data-ttu-id="94c92-128">偵測到與 System Center Virtual Machine Manager 2012 R2 環境中執行時 bootstraps hello 適用於 Linux 的 VMM 代理程式</span><span class="sxs-lookup"><span data-stu-id="94c92-128">Detects and bootstraps hello VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span></span>
* <span data-ttu-id="94c92-129">**VM 延伸模組**</span><span class="sxs-lookup"><span data-stu-id="94c92-129">**VM Extension**</span></span>
  
  * <span data-ttu-id="94c92-130">插入至 Linux VM (IaaS) tooenable 軟體和設定自動化，由 Microsoft 和協力廠商所撰寫的元件</span><span class="sxs-lookup"><span data-stu-id="94c92-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) tooenable software and configuration automation</span></span>
  * <span data-ttu-id="94c92-131">VM 延伸模組參考實作，網址為 [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span><span class="sxs-lookup"><span data-stu-id="94c92-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span></span>

## <a name="communication"></a><span data-ttu-id="94c92-132">通訊</span><span class="sxs-lookup"><span data-stu-id="94c92-132">Communication</span></span>
<span data-ttu-id="94c92-133">透過兩個通道，就會發生 hello 從 hello 平台 toohello 代理程式的資訊流程：</span><span class="sxs-lookup"><span data-stu-id="94c92-133">hello information flow from hello platform toohello agent occurs via two channels:</span></span>

* <span data-ttu-id="94c92-134">在 IaaS 部署中，開機時連接的 DVD。</span><span class="sxs-lookup"><span data-stu-id="94c92-134">A boot-time attached DVD for IaaS deployments.</span></span> <span data-ttu-id="94c92-135">此 DVD 包含 OVF 相容的組態檔，其中包含實際 SSH 金鑰組 hello 以外的所有佈建資訊。</span><span class="sxs-lookup"><span data-stu-id="94c92-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than hello actual SSH keypairs.</span></span>
* <span data-ttu-id="94c92-136">TCP 端點會公開 REST API 用 tooobtain 部署和拓撲設定。</span><span class="sxs-lookup"><span data-stu-id="94c92-136">A TCP endpoint exposing a REST API used tooobtain deployment and topology configuration.</span></span>

## <a name="requirements"></a><span data-ttu-id="94c92-137">需求</span><span class="sxs-lookup"><span data-stu-id="94c92-137">Requirements</span></span>
<span data-ttu-id="94c92-138">hello 下列系統都已測試過與已知 toowork 以 hello Azure Linux 代理程式：</span><span class="sxs-lookup"><span data-stu-id="94c92-138">hello following systems have been tested and are known toowork with hello Azure Linux Agent:</span></span>

> [!NOTE]
> <span data-ttu-id="94c92-139">這份清單可能會有所不同 hello 官方份支援的系統上 hello Microsoft Azure 平台，如下所述： [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span><span class="sxs-lookup"><span data-stu-id="94c92-139">This list may differ from hello official list of supported systems on hello Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span></span>
> 
> 

* <span data-ttu-id="94c92-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="94c92-140">CoreOS</span></span>
* <span data-ttu-id="94c92-141">CentOS 6.3+</span><span class="sxs-lookup"><span data-stu-id="94c92-141">CentOS 6.3+</span></span>
* <span data-ttu-id="94c92-142">Red Hat Enterprise Linux 6.7+</span><span class="sxs-lookup"><span data-stu-id="94c92-142">Red Hat Enterprise Linux 6.7+</span></span>
* <span data-ttu-id="94c92-143">Debian 7.0+</span><span class="sxs-lookup"><span data-stu-id="94c92-143">Debian 7.0+</span></span>
* <span data-ttu-id="94c92-144">Ubuntu 12.04+</span><span class="sxs-lookup"><span data-stu-id="94c92-144">Ubuntu 12.04+</span></span>
* <span data-ttu-id="94c92-145">openSUSE 12.3+</span><span class="sxs-lookup"><span data-stu-id="94c92-145">openSUSE 12.3+</span></span>
* <span data-ttu-id="94c92-146">SLES 11 SP3+</span><span class="sxs-lookup"><span data-stu-id="94c92-146">SLES 11 SP3+</span></span>
* <span data-ttu-id="94c92-147">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="94c92-147">Oracle Linux 6.4+</span></span>

<span data-ttu-id="94c92-148">其他支援的系統：</span><span class="sxs-lookup"><span data-stu-id="94c92-148">Other Supported Systems:</span></span>

* <span data-ttu-id="94c92-149">FreeBSD 10+ (Azure Linux 代理程式 v2.0.10+)</span><span class="sxs-lookup"><span data-stu-id="94c92-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span></span>

<span data-ttu-id="94c92-150">hello Linux 代理程式取決於某些系統中的封裝順序 toofunction 正確：</span><span class="sxs-lookup"><span data-stu-id="94c92-150">hello Linux agent depends on some system packages in order toofunction properly:</span></span>

* <span data-ttu-id="94c92-151">Python 2.6+</span><span class="sxs-lookup"><span data-stu-id="94c92-151">Python 2.6+</span></span>
* <span data-ttu-id="94c92-152">OpenSSL 1.0+</span><span class="sxs-lookup"><span data-stu-id="94c92-152">OpenSSL 1.0+</span></span>
* <span data-ttu-id="94c92-153">OpenSSH 5.3+</span><span class="sxs-lookup"><span data-stu-id="94c92-153">OpenSSH 5.3+</span></span>
* <span data-ttu-id="94c92-154">檔案系統公用程式：sfdisk、fdisk、mkfs、parted</span><span class="sxs-lookup"><span data-stu-id="94c92-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span></span>
* <span data-ttu-id="94c92-155">密碼工具：chpasswd、sudo</span><span class="sxs-lookup"><span data-stu-id="94c92-155">Password tools: chpasswd, sudo</span></span>
* <span data-ttu-id="94c92-156">文字處理工具：sed、grep</span><span class="sxs-lookup"><span data-stu-id="94c92-156">Text processing tools: sed, grep</span></span>
* <span data-ttu-id="94c92-157">網路工具：ip-route</span><span class="sxs-lookup"><span data-stu-id="94c92-157">Network tools: ip-route</span></span>
* <span data-ttu-id="94c92-158">掛接 UDF 檔案系統的核心支援。</span><span class="sxs-lookup"><span data-stu-id="94c92-158">Kernel support for mounting UDF filesystems.</span></span>

## <a name="installation"></a><span data-ttu-id="94c92-159">安裝</span><span class="sxs-lookup"><span data-stu-id="94c92-159">Installation</span></span>
<span data-ttu-id="94c92-160">從您的發佈封裝儲存機制使用 RPM 或 DEB 套件的安裝是慣用的 hello 方法安裝和升級 hello Azure Linux 代理程式。</span><span class="sxs-lookup"><span data-stu-id="94c92-160">Installation using an RPM or a DEB package from your distribution's package repository is hello preferred method of installing and upgrading hello Azure Linux Agent.</span></span> <span data-ttu-id="94c92-161">所有的 hello[背書發佈提供者](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)整合其映像和儲存機制中的 hello Azure Linux 代理程式套件。</span><span class="sxs-lookup"><span data-stu-id="94c92-161">All hello [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate hello Azure Linux agent package into their images and repositories.</span></span>

<span data-ttu-id="94c92-162">請參閱 toohello 文件以 hello [Azure Linux 代理程式在 GitHub 上的儲存機制](https://github.com/Azure/WALinuxAgent)進階的安裝選項，例如安裝從來源或 toocustom 位置或前置詞。</span><span class="sxs-lookup"><span data-stu-id="94c92-162">Refer toohello documentation in hello [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or toocustom locations or prefixes.</span></span>

## <a name="command-line-options"></a><span data-ttu-id="94c92-163">命令列選項</span><span class="sxs-lookup"><span data-stu-id="94c92-163">Command Line Options</span></span>
### <a name="flags"></a><span data-ttu-id="94c92-164">旗標</span><span class="sxs-lookup"><span data-stu-id="94c92-164">Flags</span></span>
* <span data-ttu-id="94c92-165">verbose：提高指定命令的詳細程度</span><span class="sxs-lookup"><span data-stu-id="94c92-165">verbose: Increase verbosity of specified command</span></span>
* <span data-ttu-id="94c92-166">force：略過某些命令的互動式確認</span><span class="sxs-lookup"><span data-stu-id="94c92-166">force: Skip interactive confirmation for some commands</span></span>

### <a name="commands"></a><span data-ttu-id="94c92-167">命令</span><span class="sxs-lookup"><span data-stu-id="94c92-167">Commands</span></span>
* <span data-ttu-id="94c92-168">說明： 列出支援的 hello 命令和旗標。</span><span class="sxs-lookup"><span data-stu-id="94c92-168">help: Lists hello supported commands and flags.</span></span>
* <span data-ttu-id="94c92-169">取消佈建： 嘗試 tooclean hello 系統，並使其適用於重新佈建。</span><span class="sxs-lookup"><span data-stu-id="94c92-169">deprovision: Attempt tooclean hello system and make it suitable for re-provisioning.</span></span> <span data-ttu-id="94c92-170">這項作業會刪除下列 hello:</span><span class="sxs-lookup"><span data-stu-id="94c92-170">This operation deleted hello following:</span></span>
  
  * <span data-ttu-id="94c92-171">所有 SSH 主機金鑰 （如果 Provisioning.RegenerateSshHostKeyPair 'y' hello 組態檔中）</span><span class="sxs-lookup"><span data-stu-id="94c92-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="94c92-172">/etc/resolv.conf 中的名稱伺服器設定</span><span class="sxs-lookup"><span data-stu-id="94c92-172">Nameserver configuration in /etc/resolv.conf</span></span>
  * <span data-ttu-id="94c92-173">從 /etc/shadow （如果 Provisioning.DeleteRootPassword 'y' hello 組態檔中的） 的根密碼</span><span class="sxs-lookup"><span data-stu-id="94c92-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="94c92-174">快取的 DHCP 用戶端租用</span><span class="sxs-lookup"><span data-stu-id="94c92-174">Cached DHCP client leases</span></span>
  * <span data-ttu-id="94c92-175">重設主機名稱 toolocalhost.localdomain</span><span class="sxs-lookup"><span data-stu-id="94c92-175">Resets host name toolocalhost.localdomain</span></span>

> [!WARNING]
> <span data-ttu-id="94c92-176">取消佈建不保證該 hello 映像時，所有的機密資訊的清除，而且適用於轉散發。</span><span class="sxs-lookup"><span data-stu-id="94c92-176">Deprovisioning does not guarantee that hello image is cleared of all sensitive information and suitable for redistribution.</span></span>
> 
> 

* <span data-ttu-id="94c92-177">取消佈建 + 使用者： 執行下方-取消佈建 （如上） 的所有內容也會刪除 hello （取自 /var/lib/waagent） 最後一個佈建的使用者帳戶和相關聯的資料。</span><span class="sxs-lookup"><span data-stu-id="94c92-177">deprovision+user: Performs everything under -deprovision (above) and also deletes hello last provisioned user account (obtained from /var/lib/waagent) and associated data.</span></span> <span data-ttu-id="94c92-178">此參數是為了取消佈建 Azure 上先前佈建的映像檔，以便擷取並重複使用。</span><span class="sxs-lookup"><span data-stu-id="94c92-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span></span>
* <span data-ttu-id="94c92-179">版本： 顯示 hello waagent 版本</span><span class="sxs-lookup"><span data-stu-id="94c92-179">version: Displays hello version of waagent</span></span>
* <span data-ttu-id="94c92-180">serialconsole： 設定幼蟲 toomark ttyS0 (hello 第一個序列連接埠) 為 hello 啟動主控台。</span><span class="sxs-lookup"><span data-stu-id="94c92-180">serialconsole: Configures GRUB toomark ttyS0 (hello first serial port) as hello boot console.</span></span> <span data-ttu-id="94c92-181">這樣可以確保核心開機記錄會傳送 toothe 序列通訊埠供偵錯。</span><span class="sxs-lookup"><span data-stu-id="94c92-181">This ensures that kernel bootup logs are sent toothe serial port and made available for debugging.</span></span>
* <span data-ttu-id="94c92-182">精靈： hello 平台服務精靈 toomanage 互動以執行 waagent。</span><span class="sxs-lookup"><span data-stu-id="94c92-182">daemon: Run waagent as a daemon toomanage interaction with hello platform.</span></span> <span data-ttu-id="94c92-183">這個引數是指定的 toowaagent hello waagent 初始化指令碼中。</span><span class="sxs-lookup"><span data-stu-id="94c92-183">This argument is specified toowaagent in hello waagent init script.</span></span>
* <span data-ttu-id="94c92-184">開始︰以背景處理序方式執行 waagent</span><span class="sxs-lookup"><span data-stu-id="94c92-184">start: Run waagent as a background process</span></span>

## <a name="configuration"></a><span data-ttu-id="94c92-185">組態</span><span class="sxs-lookup"><span data-stu-id="94c92-185">Configuration</span></span>
<span data-ttu-id="94c92-186">組態檔 (/ etc/waagent.conf) 控制項 hello waagent 的動作。</span><span class="sxs-lookup"><span data-stu-id="94c92-186">A configuration file (/etc/waagent.conf) controls hello actions of waagent.</span></span> <span data-ttu-id="94c92-187">範例組態檔如下所示：</span><span class="sxs-lookup"><span data-stu-id="94c92-187">A sample configuration file is shown below:</span></span>

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

<span data-ttu-id="94c92-188">下面將詳細說明各種組態選項的 hello。</span><span class="sxs-lookup"><span data-stu-id="94c92-188">hello various configuration options are described in detail below.</span></span> <span data-ttu-id="94c92-189">組態選項可分成三種：布林、字串或整數。</span><span class="sxs-lookup"><span data-stu-id="94c92-189">Configuration options are of three types; Boolean, String or Integer.</span></span> <span data-ttu-id="94c92-190">hello 布林組態選項可以指定為"y"或"n"。</span><span class="sxs-lookup"><span data-stu-id="94c92-190">hello Boolean configuration options can be specified as "y" or "n".</span></span> <span data-ttu-id="94c92-191">hello"None"可用於某些字串類型組態項目有詳細說明下列特殊關鍵字。</span><span class="sxs-lookup"><span data-stu-id="94c92-191">hello special keyword "None" may be used for some string type configuration entries as detailed below.</span></span>

<span data-ttu-id="94c92-192">**Provisioning.Enabled：**</span><span class="sxs-lookup"><span data-stu-id="94c92-192">**Provisioning.Enabled:**</span></span>  
<span data-ttu-id="94c92-193">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="94c92-193">Type: Boolean</span></span>  
<span data-ttu-id="94c92-194">預設：y</span><span class="sxs-lookup"><span data-stu-id="94c92-194">Default: y</span></span>

<span data-ttu-id="94c92-195">這可讓 hello 使用者 tooenable 或停用 hello 佈建在 hello 代理程式的功能。</span><span class="sxs-lookup"><span data-stu-id="94c92-195">This allows hello user tooenable or disable hello provisioning functionality in hello agent.</span></span> <span data-ttu-id="94c92-196">有效值為 "y" 或 "n"。</span><span class="sxs-lookup"><span data-stu-id="94c92-196">Valid values are "y" or "n".</span></span> <span data-ttu-id="94c92-197">佈建已停用，SSH hello 映像中的主控件與使用者金鑰會保留，且會忽略 hello Azure 佈建應用程式開發介面中指定的任何設定。</span><span class="sxs-lookup"><span data-stu-id="94c92-197">If provisioning is disabled, SSH host and user keys in hello image are preserved and any configuration specified in hello Azure provisioning API is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="94c92-198">hello`Provisioning.Enabled`太"n"用於佈建雲端 init Ubuntu 雲端映像上的參數預設值。</span><span class="sxs-lookup"><span data-stu-id="94c92-198">hello `Provisioning.Enabled` parameter defaults too"n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span></span>
> 
> 

<span data-ttu-id="94c92-199">**Provisioning.DeleteRootPassword：**</span><span class="sxs-lookup"><span data-stu-id="94c92-199">**Provisioning.DeleteRootPassword:**</span></span>  
<span data-ttu-id="94c92-200">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="94c92-200">Type: Boolean</span></span>  
<span data-ttu-id="94c92-201">預設：n</span><span class="sxs-lookup"><span data-stu-id="94c92-201">Default: n</span></span>

<span data-ttu-id="94c92-202">如果設定，在 hello /etc/hosts 陰影檔案中的 hello 根密碼會清除期間 hello 佈建程序。</span><span class="sxs-lookup"><span data-stu-id="94c92-202">If set, hello root password in hello /etc/shadow file is erased during hello provisioning process.</span></span>

<span data-ttu-id="94c92-203">**Provisioning.RegenerateSshHostKeyPair：**</span><span class="sxs-lookup"><span data-stu-id="94c92-203">**Provisioning.RegenerateSshHostKeyPair:**</span></span>  
<span data-ttu-id="94c92-204">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="94c92-204">Type: Boolean</span></span>  
<span data-ttu-id="94c92-205">預設：y</span><span class="sxs-lookup"><span data-stu-id="94c92-205">Default: y</span></span>

<span data-ttu-id="94c92-206">如果設定，所有 SSH 主機金鑰組 （ecdsa、 dsa 和 rsa） 刪除期間 hello 從 /etc/ssh/佈建程序。</span><span class="sxs-lookup"><span data-stu-id="94c92-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during hello provisioning process from /etc/ssh/.</span></span> <span data-ttu-id="94c92-207">還會產生單一全新的金鑰組。</span><span class="sxs-lookup"><span data-stu-id="94c92-207">And a single fresh key pair is generated.</span></span>

<span data-ttu-id="94c92-208">hello hello 全新的金鑰組的加密類型為可設定由 hello Provisioning.SshHostKeyPairType 項目。</span><span class="sxs-lookup"><span data-stu-id="94c92-208">hello encryption type for hello fresh key pair is configurable by hello Provisioning.SshHostKeyPairType entry.</span></span> <span data-ttu-id="94c92-209">請注意某些會重新建立任何遺失的加密類型的 SSH 金鑰組 hello SSH 服務精靈重新啟動 （例如，在重新開機） 時。</span><span class="sxs-lookup"><span data-stu-id="94c92-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when hello SSH daemon is restarted (for example, upon a reboot).</span></span>

<span data-ttu-id="94c92-210">**Provisioning.SshHostKeyPairType：**</span><span class="sxs-lookup"><span data-stu-id="94c92-210">**Provisioning.SshHostKeyPairType:**</span></span>  
<span data-ttu-id="94c92-211">類型：字串</span><span class="sxs-lookup"><span data-stu-id="94c92-211">Type: String</span></span>  
<span data-ttu-id="94c92-212">預設：rsa</span><span class="sxs-lookup"><span data-stu-id="94c92-212">Default: rsa</span></span>

<span data-ttu-id="94c92-213">這可以設定 tooan 加密演算法支援的型別 hello hello 虛擬機器上的 SSH 服務精靈。</span><span class="sxs-lookup"><span data-stu-id="94c92-213">This can be set tooan encryption algorithm type that is supported by hello SSH daemon on hello virtual machine.</span></span> <span data-ttu-id="94c92-214">hello 通常支援值為"rsa"、"dsa"和"ecdsa"。</span><span class="sxs-lookup"><span data-stu-id="94c92-214">hello typically supported values are "rsa", "dsa" and "ecdsa".</span></span> <span data-ttu-id="94c92-215">請注意，Windows 的 "putty.exe" 不支援 "ecdsa"。</span><span class="sxs-lookup"><span data-stu-id="94c92-215">Note that "putty.exe" on Windows does not support "ecdsa".</span></span> <span data-ttu-id="94c92-216">因此，如果您要 toouse putty.exe Windows tooconnect tooa Linux 部署，請使用"rsa"或"dsa"。</span><span class="sxs-lookup"><span data-stu-id="94c92-216">So, if you intend toouse putty.exe on Windows tooconnect tooa Linux deployment, please use "rsa" or "dsa".</span></span>

<span data-ttu-id="94c92-217">**Provisioning.MonitorHostName：**</span><span class="sxs-lookup"><span data-stu-id="94c92-217">**Provisioning.MonitorHostName:**</span></span>  
<span data-ttu-id="94c92-218">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="94c92-218">Type: Boolean</span></span>  
<span data-ttu-id="94c92-219">預設：y</span><span class="sxs-lookup"><span data-stu-id="94c92-219">Default: y</span></span>

<span data-ttu-id="94c92-220">如果設定，waagent 會監視 hello Linux 虛擬機器的主機名稱變更 （hello"hostname"命令所傳回），並自動更新 hello hello 影像 tooreflect hello 變更中的網路設定。</span><span class="sxs-lookup"><span data-stu-id="94c92-220">If set, waagent will monitor hello Linux virtual machine for hostname changes (as returned by hello "hostname" command) and automatically update hello networking configuration in hello image tooreflect hello change.</span></span> <span data-ttu-id="94c92-221">順序 toopush hello 名稱中變更 toohello DNS 伺服器、 網路功能會以 hello 虛擬機器重新啟動。</span><span class="sxs-lookup"><span data-stu-id="94c92-221">In order toopush hello name change toohello DNS servers, networking will be restarted in hello virtual machine.</span></span> <span data-ttu-id="94c92-222">這會導致網際網路連線短暫中斷。</span><span class="sxs-lookup"><span data-stu-id="94c92-222">This will result in brief loss of Internet connectivity.</span></span>

<span data-ttu-id="94c92-223">**Provisioning.DecodeCustomData**</span><span class="sxs-lookup"><span data-stu-id="94c92-223">**Provisioning.DecodeCustomData**</span></span>  
<span data-ttu-id="94c92-224">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="94c92-224">Type: Boolean</span></span>  
<span data-ttu-id="94c92-225">預設：n</span><span class="sxs-lookup"><span data-stu-id="94c92-225">Default: n</span></span>

<span data-ttu-id="94c92-226">如果設定，waagent 會從 CustomData 將 Base64 解碼。</span><span class="sxs-lookup"><span data-stu-id="94c92-226">If set, waagent will decode CustomData from Base64.</span></span>

<span data-ttu-id="94c92-227">**Provisioning.ExecuteCustomData**</span><span class="sxs-lookup"><span data-stu-id="94c92-227">**Provisioning.ExecuteCustomData**</span></span>  
<span data-ttu-id="94c92-228">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="94c92-228">Type: Boolean</span></span>  
<span data-ttu-id="94c92-229">預設：n</span><span class="sxs-lookup"><span data-stu-id="94c92-229">Default: n</span></span>

<span data-ttu-id="94c92-230">如果設定，waagent 將在佈建之後執行 CustomData。</span><span class="sxs-lookup"><span data-stu-id="94c92-230">If set, waagent will execute CustomData after provisioning.</span></span>

<span data-ttu-id="94c92-231">**Provisioning.PasswordCryptId**</span><span class="sxs-lookup"><span data-stu-id="94c92-231">**Provisioning.PasswordCryptId**</span></span>  
<span data-ttu-id="94c92-232">型別︰字串</span><span class="sxs-lookup"><span data-stu-id="94c92-232">Type:String</span></span>  
<span data-ttu-id="94c92-233">預設︰6</span><span class="sxs-lookup"><span data-stu-id="94c92-233">Default:6</span></span>

<span data-ttu-id="94c92-234">產生密碼雜湊時由 crypt 使用的演算法。</span><span class="sxs-lookup"><span data-stu-id="94c92-234">Algorithm used by crypt when generating password hash.</span></span>  
 <span data-ttu-id="94c92-235">1 - MD5</span><span class="sxs-lookup"><span data-stu-id="94c92-235">1 - MD5</span></span>  
 <span data-ttu-id="94c92-236">2a - Blowfish</span><span class="sxs-lookup"><span data-stu-id="94c92-236">2a - Blowfish</span></span>  
 <span data-ttu-id="94c92-237">5-SHA-256</span><span class="sxs-lookup"><span data-stu-id="94c92-237">5 - SHA-256</span></span>  
 <span data-ttu-id="94c92-238">6 - SHA-512</span><span class="sxs-lookup"><span data-stu-id="94c92-238">6 - SHA-512</span></span>  

<span data-ttu-id="94c92-239">**Provisioning.PasswordCryptSaltLength**</span><span class="sxs-lookup"><span data-stu-id="94c92-239">**Provisioning.PasswordCryptSaltLength**</span></span>  
<span data-ttu-id="94c92-240">型別︰字串</span><span class="sxs-lookup"><span data-stu-id="94c92-240">Type:String</span></span>  
<span data-ttu-id="94c92-241">預設值︰10</span><span class="sxs-lookup"><span data-stu-id="94c92-241">Default:10</span></span>

<span data-ttu-id="94c92-242">產生密碼雜湊時使用的隨機 salt 長度。</span><span class="sxs-lookup"><span data-stu-id="94c92-242">Length of random salt used when generating password hash.</span></span>

<span data-ttu-id="94c92-243">**ResourceDisk.Format：**</span><span class="sxs-lookup"><span data-stu-id="94c92-243">**ResourceDisk.Format:**</span></span>  
<span data-ttu-id="94c92-244">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="94c92-244">Type: Boolean</span></span>  
<span data-ttu-id="94c92-245">預設：y</span><span class="sxs-lookup"><span data-stu-id="94c92-245">Default: y</span></span>

<span data-ttu-id="94c92-246">如果設定，hello hello 平台所提供的資源磁碟會格式化並掛接 waagent"ResourceDisk.Filesystem 」 中的 hello 使用者所要求的 hello filesystem 類型是否"ntfs"以外的任何項目。</span><span class="sxs-lookup"><span data-stu-id="94c92-246">If set, hello resource disk provided by hello platform will be formatted and mounted by waagent if hello filesystem type requested by hello user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span></span> <span data-ttu-id="94c92-247">Linux (83) 類型的單一分割區可供 hello 磁碟上。</span><span class="sxs-lookup"><span data-stu-id="94c92-247">A single partition of type Linux (83) will be made available on hello disk.</span></span> <span data-ttu-id="94c92-248">請注意，如果可順利掛接此磁碟分割，則不會格式化。</span><span class="sxs-lookup"><span data-stu-id="94c92-248">Note that this partition will not be formatted if it can be successfully mounted.</span></span>

<span data-ttu-id="94c92-249">**ResourceDisk.Filesystem：**</span><span class="sxs-lookup"><span data-stu-id="94c92-249">**ResourceDisk.Filesystem:**</span></span>  
<span data-ttu-id="94c92-250">類型：字串</span><span class="sxs-lookup"><span data-stu-id="94c92-250">Type: String</span></span>  
<span data-ttu-id="94c92-251">預設：ext4</span><span class="sxs-lookup"><span data-stu-id="94c92-251">Default: ext4</span></span>

<span data-ttu-id="94c92-252">這會指定 hello hello 資源磁碟的檔案系統類型。</span><span class="sxs-lookup"><span data-stu-id="94c92-252">This specifies hello filesystem type for hello resource disk.</span></span> <span data-ttu-id="94c92-253">支援的值隨 Linux 散發套件而不同。</span><span class="sxs-lookup"><span data-stu-id="94c92-253">Supported values vary by Linux distribution.</span></span> <span data-ttu-id="94c92-254">如果 X，然後 mkfs hello 字串。X 應會出現在 hello Linux 映像上。</span><span class="sxs-lookup"><span data-stu-id="94c92-254">If hello string is X, then mkfs.X should be present on hello Linux image.</span></span> <span data-ttu-id="94c92-255">SLES 11 映像檔通常會使用 'ext3'。</span><span class="sxs-lookup"><span data-stu-id="94c92-255">SLES 11 images should typically use 'ext3'.</span></span> <span data-ttu-id="94c92-256">在此，FreeBSD 映像檔應該是使用 'ufs2'。</span><span class="sxs-lookup"><span data-stu-id="94c92-256">FreeBSD images should use 'ufs2' here.</span></span>

<span data-ttu-id="94c92-257">**ResourceDisk.MountPoint：**</span><span class="sxs-lookup"><span data-stu-id="94c92-257">**ResourceDisk.MountPoint:**</span></span>  
<span data-ttu-id="94c92-258">類型：字串</span><span class="sxs-lookup"><span data-stu-id="94c92-258">Type: String</span></span>  
<span data-ttu-id="94c92-259">預設值：/mnt/resource</span><span class="sxs-lookup"><span data-stu-id="94c92-259">Default: /mnt/resource</span></span> 

<span data-ttu-id="94c92-260">這會指定 hello 掛載 hello 資源磁碟時的路徑。</span><span class="sxs-lookup"><span data-stu-id="94c92-260">This specifies hello path at which hello resource disk is mounted.</span></span> <span data-ttu-id="94c92-261">請注意該 hello 資源磁碟是*暫存*磁碟，以及可能會在取消佈建 hello VM 時清空。</span><span class="sxs-lookup"><span data-stu-id="94c92-261">Note that hello resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span>

<span data-ttu-id="94c92-262">**ResourceDisk.MountOptions**</span><span class="sxs-lookup"><span data-stu-id="94c92-262">**ResourceDisk.MountOptions**</span></span>  
<span data-ttu-id="94c92-263">類型：字串</span><span class="sxs-lookup"><span data-stu-id="94c92-263">Type: String</span></span>  
<span data-ttu-id="94c92-264">預設值︰無</span><span class="sxs-lookup"><span data-stu-id="94c92-264">Default: None</span></span>

<span data-ttu-id="94c92-265">指定磁碟掛接選項傳遞 toobe toohello 掛接-o 命令。</span><span class="sxs-lookup"><span data-stu-id="94c92-265">Specifies disk mount options toobe passed toohello mount -o command.</span></span> <span data-ttu-id="94c92-266">這是以逗號分隔的值清單，例如：</span><span class="sxs-lookup"><span data-stu-id="94c92-266">This is a comma separated list of values, ex.</span></span> <span data-ttu-id="94c92-267">'nodev,nosuid'。</span><span class="sxs-lookup"><span data-stu-id="94c92-267">'nodev,nosuid'.</span></span> <span data-ttu-id="94c92-268">如需詳細資訊，請參閱 Mount(8)。</span><span class="sxs-lookup"><span data-stu-id="94c92-268">See mount(8) for details.</span></span>

<span data-ttu-id="94c92-269">**ResourceDisk.EnableSwap：**</span><span class="sxs-lookup"><span data-stu-id="94c92-269">**ResourceDisk.EnableSwap:**</span></span>  
<span data-ttu-id="94c92-270">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="94c92-270">Type: Boolean</span></span>  
<span data-ttu-id="94c92-271">預設：n</span><span class="sxs-lookup"><span data-stu-id="94c92-271">Default: n</span></span>

<span data-ttu-id="94c92-272">如果設定，成為分頁檔 (/ 交換檔) hello 資源的磁碟上建立和加入 toohello 系統交換空間。</span><span class="sxs-lookup"><span data-stu-id="94c92-272">If set, a swap file (/swapfile) is created on hello resource disk and added toohello system swap space.</span></span>

<span data-ttu-id="94c92-273">**ResourceDisk.SwapSizeMB：**</span><span class="sxs-lookup"><span data-stu-id="94c92-273">**ResourceDisk.SwapSizeMB:**</span></span>  
<span data-ttu-id="94c92-274">型別︰整數</span><span class="sxs-lookup"><span data-stu-id="94c92-274">Type: Integer</span></span>  
<span data-ttu-id="94c92-275">預設值：0</span><span class="sxs-lookup"><span data-stu-id="94c92-275">Default: 0</span></span>

<span data-ttu-id="94c92-276">hello 的 hello 分頁檔，以 mb 為單位的大小。</span><span class="sxs-lookup"><span data-stu-id="94c92-276">hello size of hello swap file in megabytes.</span></span>

<span data-ttu-id="94c92-277">**Logs.Verbose：**</span><span class="sxs-lookup"><span data-stu-id="94c92-277">**Logs.Verbose:**</span></span>  
<span data-ttu-id="94c92-278">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="94c92-278">Type: Boolean</span></span>  
<span data-ttu-id="94c92-279">預設：n</span><span class="sxs-lookup"><span data-stu-id="94c92-279">Default: n</span></span>

<span data-ttu-id="94c92-280">如果設定，則記錄詳細程度會提高。</span><span class="sxs-lookup"><span data-stu-id="94c92-280">If set, log verbosity is boosted.</span></span> <span data-ttu-id="94c92-281">Waagent 記錄 too/var/log/waagent.log，並可運用 hello 系統 logrotate 功能 toorotate 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="94c92-281">Waagent logs too/var/log/waagent.log and leverages hello system logrotate functionality toorotate logs.</span></span>

<span data-ttu-id="94c92-282">**OS.EnableRDMA**</span><span class="sxs-lookup"><span data-stu-id="94c92-282">**OS.EnableRDMA**</span></span>  
<span data-ttu-id="94c92-283">型別︰布林值</span><span class="sxs-lookup"><span data-stu-id="94c92-283">Type: Boolean</span></span>  
<span data-ttu-id="94c92-284">預設：n</span><span class="sxs-lookup"><span data-stu-id="94c92-284">Default: n</span></span>

<span data-ttu-id="94c92-285">如果設定，hello 代理程式會嘗試 tooinstall，然後載入符合 hello 韌體版本的 hello hello 基礎硬體上的 RDMA 核心驅動程式。</span><span class="sxs-lookup"><span data-stu-id="94c92-285">If set, hello agent will attempt tooinstall and then load an RDMA kernel driver that matches hello version of hello firmware on hello underlying hardware.</span></span>

<span data-ttu-id="94c92-286">**OS.RootDeviceScsiTimeout：**</span><span class="sxs-lookup"><span data-stu-id="94c92-286">**OS.RootDeviceScsiTimeout:**</span></span>  
<span data-ttu-id="94c92-287">型別︰整數</span><span class="sxs-lookup"><span data-stu-id="94c92-287">Type: Integer</span></span>  
<span data-ttu-id="94c92-288">預設值︰300</span><span class="sxs-lookup"><span data-stu-id="94c92-288">Default: 300</span></span>

<span data-ttu-id="94c92-289">這會以秒為單位 hello OS 磁碟和資料磁碟機上設定 hello SCSI 逾時。</span><span class="sxs-lookup"><span data-stu-id="94c92-289">This configures hello SCSI timeout in seconds on hello OS disk and data drives.</span></span> <span data-ttu-id="94c92-290">如果沒有設定，hello 系統會使用預設值。</span><span class="sxs-lookup"><span data-stu-id="94c92-290">If not set, hello system defaults are used.</span></span>

<span data-ttu-id="94c92-291">**OS.OpensslPath：**</span><span class="sxs-lookup"><span data-stu-id="94c92-291">**OS.OpensslPath:**</span></span>  
<span data-ttu-id="94c92-292">類型：字串</span><span class="sxs-lookup"><span data-stu-id="94c92-292">Type: String</span></span>  
<span data-ttu-id="94c92-293">預設值︰無</span><span class="sxs-lookup"><span data-stu-id="94c92-293">Default: None</span></span>

<span data-ttu-id="94c92-294">這可以是使用的 toospecify hello openssl 二進位 toouse 密碼編譯作業的替代路徑。</span><span class="sxs-lookup"><span data-stu-id="94c92-294">This can be used toospecify an alternate path for hello openssl binary toouse for cryptographic operations.</span></span>

<span data-ttu-id="94c92-295">**HttpProxy.Host, HttpProxy.Port**</span><span class="sxs-lookup"><span data-stu-id="94c92-295">**HttpProxy.Host, HttpProxy.Port**</span></span>  
<span data-ttu-id="94c92-296">類型：字串</span><span class="sxs-lookup"><span data-stu-id="94c92-296">Type: String</span></span>  
<span data-ttu-id="94c92-297">預設值︰無</span><span class="sxs-lookup"><span data-stu-id="94c92-297">Default: None</span></span>

<span data-ttu-id="94c92-298">如果設定，hello 代理程式將使用此 proxy 伺服器 tooaccess hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="94c92-298">If set, hello agent will use this proxy server tooaccess hello internet.</span></span> 

## <a name="ubuntu-cloud-images"></a><span data-ttu-id="94c92-299">Ubuntu 雲端映像</span><span class="sxs-lookup"><span data-stu-id="94c92-299">Ubuntu Cloud Images</span></span>
<span data-ttu-id="94c92-300">請注意，利用 Ubuntu 雲端映像[雲端 init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform 許多組態工作，否則會由管理 hello Azure Linux 代理程式。</span><span class="sxs-lookup"><span data-stu-id="94c92-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform many configuration tasks that would otherwise be managed by hello Azure Linux Agent.</span></span>  <span data-ttu-id="94c92-301">請注意下列差異 hello:</span><span class="sxs-lookup"><span data-stu-id="94c92-301">Please note hello following differences:</span></span>

* <span data-ttu-id="94c92-302">**Provisioning.Enabled**太"n"使用佈建工作的雲端 init tooperform Ubuntu 雲端映像上的預設值。</span><span class="sxs-lookup"><span data-stu-id="94c92-302">**Provisioning.Enabled** defaults too"n" on Ubuntu Cloud Images that use cloud-init tooperform provisioning tasks.</span></span>
* <span data-ttu-id="94c92-303">下列組態參數的 hello 有不會影響使用雲端 init toomanage hello 資源磁碟和交換空間的 Ubuntu 雲端映像：</span><span class="sxs-lookup"><span data-stu-id="94c92-303">hello following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init toomanage hello resource disk and swap space:</span></span>
  
  * <span data-ttu-id="94c92-304">**ResourceDisk.Format**</span><span class="sxs-lookup"><span data-stu-id="94c92-304">**ResourceDisk.Format**</span></span>
  * <span data-ttu-id="94c92-305">**ResourceDisk.Filesystem**</span><span class="sxs-lookup"><span data-stu-id="94c92-305">**ResourceDisk.Filesystem**</span></span>
  * <span data-ttu-id="94c92-306">**ResourceDisk.MountPoint**</span><span class="sxs-lookup"><span data-stu-id="94c92-306">**ResourceDisk.MountPoint**</span></span>
  * <span data-ttu-id="94c92-307">**ResourceDisk.EnableSwap**</span><span class="sxs-lookup"><span data-stu-id="94c92-307">**ResourceDisk.EnableSwap**</span></span>
  * <span data-ttu-id="94c92-308">**ResourceDisk.SwapSizeMB**</span><span class="sxs-lookup"><span data-stu-id="94c92-308">**ResourceDisk.SwapSizeMB**</span></span>
* <span data-ttu-id="94c92-309">請參閱下列資源 tooconfigure hello 資源磁碟掛接點的 hello 和佈建期間交換 Ubuntu 雲端映像上的空間：</span><span class="sxs-lookup"><span data-stu-id="94c92-309">Please see hello following resources tooconfigure hello resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span></span>
  
  * [<span data-ttu-id="94c92-310">Ubuntu Wiki：設定交換資料分割</span><span class="sxs-lookup"><span data-stu-id="94c92-310">Ubuntu Wiki: Configure Swap Partitions</span></span>](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [<span data-ttu-id="94c92-311">將自訂資料插入 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="94c92-311">Injecting Custom Data into an Azure Virtual Machine</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

