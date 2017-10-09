---
title: "aaaInstall 行動服務 （VMware 或實體 tooAzure） |Microsoft 文件"
description: "了解如何 tooinstall 會 hello 行動服務代理程式 tooprotect 在內部部署電腦。"
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: f7836e6b35d3838bae1eff927838ce4b245b9f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a><span data-ttu-id="c4b0b-103">安裝行動服務 （VMware 或實體 tooAzure）</span><span class="sxs-lookup"><span data-stu-id="c4b0b-103">Install Mobility Service (VMware or physical tooAzure)</span></span>
<span data-ttu-id="c4b0b-104">Azure Site Recovery Mobility 服務擷取的電腦上，資料寫入，並再將它們轉送 toohello 處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="c4b0b-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them toohello process server.</span></span> <span data-ttu-id="c4b0b-105">部署行動服務 tooevery 電腦 （VMware VM 或實體伺服器） 的 tooreplicate tooAzure。</span><span class="sxs-lookup"><span data-stu-id="c4b0b-105">Deploy Mobility Service tooevery computer (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="c4b0b-106">您可以部署您使用下列方法 hello 想 tooprotect 行動服務 toohello 伺服器：</span><span class="sxs-lookup"><span data-stu-id="c4b0b-106">You can deploy Mobility Service toohello servers that you want tooprotect by using hello following methods:</span></span>


* [<span data-ttu-id="c4b0b-107">使用軟體部署工具 (例如 System Center Configuration Manager) 安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="c4b0b-107">Install Mobility Service by using software deployment tools like System Center Configuration Manager</span></span>](site-recovery-install-mobility-service-using-sccm.md)
* [<span data-ttu-id="c4b0b-108">使用 Azure 自動化和預期狀態設定 (Automation DSC) 安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="c4b0b-108">Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)</span></span>](site-recovery-automate-mobility-service-install.md)
* [<span data-ttu-id="c4b0b-109">使用 hello 圖形化使用者介面 (GUI)，以手動方式安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="c4b0b-109">Install Mobility Service manually by using hello graphical user interface (GUI)</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [<span data-ttu-id="c4b0b-110">在命令提示字元中手動安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="c4b0b-110">Install Mobility Service manually at a command prompt</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [<span data-ttu-id="c4b0b-111">透過推送安裝從 Azure Site Recovery 安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="c4b0b-111">Install Mobility Service by push installation from Azure Site Recovery</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> <span data-ttu-id="c4b0b-112">開頭為 Windows 虛擬機器 (Vm) 上的版本 9.7.0.0，hello 行動服務安裝程式也會安裝 hello 的最新可用[Azure VM 代理程式](../virtual-machines/windows/extensions-features.md#azure-vm-agent)。</span><span class="sxs-lookup"><span data-stu-id="c4b0b-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), hello Mobility Service installer also installs hello latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span></span> <span data-ttu-id="c4b0b-113">當電腦容錯移轉 tooAzure 時，hello 電腦符合 hello 代理程式安裝使用任何 VM 擴充功能的必要條件。</span><span class="sxs-lookup"><span data-stu-id="c4b0b-113">When a computer fails over tooAzure, hello computer meets hello agent installation prerequisite for using any VM extension.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4b0b-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="c4b0b-114">Prerequisites</span></span>
<span data-ttu-id="c4b0b-115">在伺服器上手動安裝行動服務之前，必須先完成下列必要條件步驟：</span><span class="sxs-lookup"><span data-stu-id="c4b0b-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span></span>
1. <span data-ttu-id="c4b0b-116">登入 tooyour 組態伺服器上，然後開啟 命令提示字元視窗，以系統管理員。</span><span class="sxs-lookup"><span data-stu-id="c4b0b-116">Sign in tooyour configuration server, and then open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="c4b0b-117">變更 hello 目錄 toohello bin 資料夾，然後再建立 複雜密碼檔案：</span><span class="sxs-lookup"><span data-stu-id="c4b0b-117">Change hello directory toohello bin folder, and then create a passphrase file:</span></span>

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. <span data-ttu-id="c4b0b-118">Hello 複雜密碼檔案存放在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="c4b0b-118">Store hello passphrase file in a secure location.</span></span> <span data-ttu-id="c4b0b-119">您在 hello 行動服務安裝期間使用 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="c4b0b-119">You use hello file during hello Mobility Service installation.</span></span>
4. <span data-ttu-id="c4b0b-120">適用於所有支援作業系統的行動服務安裝程式都 hello %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="c4b0b-120">Mobility Service installers for all supported operating systems are in hello %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span></span>

### <a name="mobility-service-installer-to-operating-system-mapping"></a><span data-ttu-id="c4b0b-121">行動服務安裝程式與作業系統之間的對應</span><span class="sxs-lookup"><span data-stu-id="c4b0b-121">Mobility Service installer-to-operating system mapping</span></span>

| <span data-ttu-id="c4b0b-122">安裝程式檔案的範本名稱</span><span class="sxs-lookup"><span data-stu-id="c4b0b-122">Installer file template name</span></span>| <span data-ttu-id="c4b0b-123">作業系統</span><span class="sxs-lookup"><span data-stu-id="c4b0b-123">Operating system</span></span> |
|---|--|
|<span data-ttu-id="c4b0b-124">Microsoft-ASR\_UA\*Windows\*release.exe</span><span class="sxs-lookup"><span data-stu-id="c4b0b-124">Microsoft-ASR\_UA\*Windows\*release.exe</span></span> | <span data-ttu-id="c4b0b-125">Windows Server 2008 R2 SP1 (64 位元)</span><span class="sxs-lookup"><span data-stu-id="c4b0b-125">Windows Server 2008 R2 SP1 (64-bit)</span></span> </br> <span data-ttu-id="c4b0b-126">Windows Server 2012 (64 位元)</span><span class="sxs-lookup"><span data-stu-id="c4b0b-126">Windows Server 2012 (64-bit)</span></span> </br> <span data-ttu-id="c4b0b-127">Windows Server 2012 R2 (64 位元)</span><span class="sxs-lookup"><span data-stu-id="c4b0b-127">Windows Server 2012 R2 (64-bit)</span></span> |
|<span data-ttu-id="c4b0b-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c4b0b-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>| <span data-ttu-id="c4b0b-129">Red Hat Enterprise Linux (RHEL) 6.4、6.5、6.6、6.7、6.8 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="c4b0b-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> </br> <span data-ttu-id="c4b0b-130">CentOS 6.4、6.5、6.6、6.7、6.8 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="c4b0b-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> |
|<span data-ttu-id="c4b0b-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c4b0b-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span> | <span data-ttu-id="c4b0b-132">Red Hat Enterprise Linux (RHEL) 7.1、7.2 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="c4b0b-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64-bit only)</span></span> </br> <span data-ttu-id="c4b0b-133">CentOS 7.0、7.1、7.2 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="c4b0b-133">CentOS 7.0, 7.1, 7.2 (64-bit only)</span></span></br> <span data-ttu-id="c4b0b-134">CentOs 7.3 (僅限移轉)</span><span class="sxs-lookup"><span data-stu-id="c4b0b-134">CentOs 7.3 (migration only)</span></span> |
|<span data-ttu-id="c4b0b-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c4b0b-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>| <span data-ttu-id="c4b0b-136">SUSE Linux Enterprise Server 11 SP3 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="c4b0b-136">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span></span>|
|<span data-ttu-id="c4b0b-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c4b0b-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>| <span data-ttu-id="c4b0b-138">SUSE Linux Enterprise Server 11 SP4 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="c4b0b-138">SUSE Linux Enterprise Server 11 SP4 (64-bit only)</span></span>|
|<span data-ttu-id="c4b0b-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c4b0b-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span> | <span data-ttu-id="c4b0b-140">Oracle Enterprise Linux 6.4、6.5 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="c4b0b-140">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span></span>|
|<span data-ttu-id="c4b0b-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c4b0b-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span> | <span data-ttu-id="c4b0b-142">Ubuntu Linux 14.04 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="c4b0b-142">Ubuntu Linux 14.04 (64-bit only)</span></span>|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a><span data-ttu-id="c4b0b-143">使用 hello GUI 手動安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="c4b0b-143">Install Mobility Service manually by using hello GUI</span></span>

>[!IMPORTANT]
> <span data-ttu-id="c4b0b-144">如果您使用**組態伺服器**tooreplicate **Azure IaaS 虛擬機器**從一個 Azure 訂用帳戶/地區 tooanother 然後**使用 hello 命令列基礎的安裝**方法</span><span class="sxs-lookup"><span data-stu-id="c4b0b-144">If you are using a **Configuration Server** tooreplicate **Azure IaaS virtual machines** from one Azure Subscription/Region tooanother then **use hello Command-line based installation** method</span></span>

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a><span data-ttu-id="c4b0b-145">在命令提示字元中手動安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="c4b0b-145">Install Mobility Service manually at a command prompt</span></span>

### <a name="command-line-installation-on-a-windows-computer"></a><span data-ttu-id="c4b0b-146">Windows 電腦上的命令列安裝</span><span class="sxs-lookup"><span data-stu-id="c4b0b-146">Command-line installation on a Windows computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a><span data-ttu-id="c4b0b-147">Linux 電腦上的命令列安裝</span><span class="sxs-lookup"><span data-stu-id="c4b0b-147">Command-line installation on a Linux computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a><span data-ttu-id="c4b0b-148">透過推送安裝從 Azure Site Recovery 安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="c4b0b-148">Install Mobility Service by push installation from Azure Site Recovery</span></span>
<span data-ttu-id="c4b0b-149">toodo 的行動服務推入安裝使用 Site Recovery，所有目標電腦必須都符合下列必要條件 hello。</span><span class="sxs-lookup"><span data-stu-id="c4b0b-149">toodo a push installation of Mobility Service by using Site Recovery, all target computers must meet hello following prerequisites.</span></span>

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
<span data-ttu-id="c4b0b-150">行動服務安裝在 hello Azure 入口網站後，選取 hello**複寫**按鈕 toostart 保護這些 Vm。</span><span class="sxs-lookup"><span data-stu-id="c4b0b-150">After Mobility Service is installed, in hello Azure portal, select hello **Replicate** button toostart protecting these VMs.</span></span>

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a><span data-ttu-id="c4b0b-151">將 Windows Server 電腦上的行動服務解除安裝</span><span class="sxs-lookup"><span data-stu-id="c4b0b-151">Uninstall Mobility Service on a Windows Server computer</span></span>
<span data-ttu-id="c4b0b-152">使用其中一個 Windows Server 電腦上遵循方法 toouninstall 行動服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="c4b0b-152">Use one of hello following methods toouninstall Mobility Service on a Windows Server computer.</span></span>

### <a name="uninstall-by-using-hello-gui"></a><span data-ttu-id="c4b0b-153">解除安裝使用 hello GUI</span><span class="sxs-lookup"><span data-stu-id="c4b0b-153">Uninstall by using hello GUI</span></span>
1. <span data-ttu-id="c4b0b-154">在 [控制台] 中，選取 [程式]。</span><span class="sxs-lookup"><span data-stu-id="c4b0b-154">In Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="c4b0b-155">選取 [Microsoft Azure Site Recovery Mobility Service/主要目標伺服器]，然後選取 [解除安裝]。</span><span class="sxs-lookup"><span data-stu-id="c4b0b-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="c4b0b-156">在命令提示字元中解除安裝</span><span class="sxs-lookup"><span data-stu-id="c4b0b-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="c4b0b-157">以系統管理員身分開啟 [命令提示字元] 視窗。</span><span class="sxs-lookup"><span data-stu-id="c4b0b-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="c4b0b-158">執行下列命令的 hello toouninstall 行動服務：</span><span class="sxs-lookup"><span data-stu-id="c4b0b-158">toouninstall Mobility Service, run hello following command:</span></span>

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a><span data-ttu-id="c4b0b-159">將 Linux 電腦上的行動服務解除安裝</span><span class="sxs-lookup"><span data-stu-id="c4b0b-159">Uninstall Mobility Service on a Linux computer</span></span>
1. <span data-ttu-id="c4b0b-160">在 Linux 伺服器上，以 **root** 使用者登入。</span><span class="sxs-lookup"><span data-stu-id="c4b0b-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="c4b0b-161">在終端機中，移太/使用者/本機/ASR。</span><span class="sxs-lookup"><span data-stu-id="c4b0b-161">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="c4b0b-162">執行下列命令的 hello toouninstall 行動服務：</span><span class="sxs-lookup"><span data-stu-id="c4b0b-162">toouninstall Mobility Service, run hello following command:</span></span>

```
uninstall.sh -Y
```
