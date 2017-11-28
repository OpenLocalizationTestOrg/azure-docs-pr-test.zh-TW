---
title: "安裝行動服務 (VMware 或實體至 Azure) | Microsoft Docs"
description: "了解如何安裝行動服務代理程式來保護您的內部部署電腦。"
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
ms.openlocfilehash: 848284f37ae2470a169d8f8a8c9c0bb5b926abe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="install-mobility-service-vmware-or-physical-to-azure"></a><span data-ttu-id="86493-103">安裝行動服務 (VMware 或實體至 Azure)</span><span class="sxs-lookup"><span data-stu-id="86493-103">Install Mobility Service (VMware or physical to Azure)</span></span>
<span data-ttu-id="86493-104">Azure Site Recovery 行動服務會擷取電腦上的資料寫入，然後將它們轉送至處理伺服器。</span><span class="sxs-lookup"><span data-stu-id="86493-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them to the process server.</span></span> <span data-ttu-id="86493-105">將行動服務部署至您要複寫至 Azure 的每部電腦 (VMware VM 或實體伺服器)。</span><span class="sxs-lookup"><span data-stu-id="86493-105">Deploy Mobility Service to every computer (VMware VM or physical server) that you want to replicate to Azure.</span></span> <span data-ttu-id="86493-106">您可以使用下列方法，將行動服務部署至您要保護的伺服器：</span><span class="sxs-lookup"><span data-stu-id="86493-106">You can deploy Mobility Service to the servers that you want to protect by using the following methods:</span></span>


* [<span data-ttu-id="86493-107">使用軟體部署工具 (例如 System Center Configuration Manager) 安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="86493-107">Install Mobility Service by using software deployment tools like System Center Configuration Manager</span></span>](site-recovery-install-mobility-service-using-sccm.md)
* [<span data-ttu-id="86493-108">使用 Azure 自動化和預期狀態設定 (Automation DSC) 安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="86493-108">Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)</span></span>](site-recovery-automate-mobility-service-install.md)
* [<span data-ttu-id="86493-109">使用圖形化使用者介面 (GUI) 手動安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="86493-109">Install Mobility Service manually by using the graphical user interface (GUI)</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [<span data-ttu-id="86493-110">在命令提示字元中手動安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="86493-110">Install Mobility Service manually at a command prompt</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [<span data-ttu-id="86493-111">透過推送安裝從 Azure Site Recovery 安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="86493-111">Install Mobility Service by push installation from Azure Site Recovery</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> <span data-ttu-id="86493-112">從版本 9.7.0.0 開始，在 Windows 虛擬機器 (VM) 上，行動服務安裝程式也會安裝最新可用的 [Azure VM 代理程式](../virtual-machines/windows/extensions-features.md#azure-vm-agent)。</span><span class="sxs-lookup"><span data-stu-id="86493-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), the Mobility Service installer also installs the latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span></span> <span data-ttu-id="86493-113">當電腦容錯移轉至 Azure 時，該電腦必須符合代理程式安裝必要條件，才能使用任何 VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="86493-113">When a computer fails over to Azure, the computer meets the agent installation prerequisite for using any VM extension.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86493-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="86493-114">Prerequisites</span></span>
<span data-ttu-id="86493-115">在伺服器上手動安裝行動服務之前，必須先完成下列必要條件步驟：</span><span class="sxs-lookup"><span data-stu-id="86493-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span></span>
1. <span data-ttu-id="86493-116">登入組態伺服器，然後以系統管理員身分開啟 [命令提示字元] 視窗。</span><span class="sxs-lookup"><span data-stu-id="86493-116">Sign in to your configuration server, and then open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="86493-117">將目錄切換至 bin 資料夾，然後建立複雜密碼檔案：</span><span class="sxs-lookup"><span data-stu-id="86493-117">Change the directory to the bin folder, and then create a passphrase file:</span></span>

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. <span data-ttu-id="86493-118">將複雜密碼檔案儲存於安全的位置。</span><span class="sxs-lookup"><span data-stu-id="86493-118">Store the passphrase file in a secure location.</span></span> <span data-ttu-id="86493-119">您會在行動服務安裝期間使用該檔案。</span><span class="sxs-lookup"><span data-stu-id="86493-119">You use the file during the Mobility Service installation.</span></span>
4. <span data-ttu-id="86493-120">針對所有支援作業系統的行動服務安裝程式位於 %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="86493-120">Mobility Service installers for all supported operating systems are in the %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span></span>

### <a name="mobility-service-installer-to-operating-system-mapping"></a><span data-ttu-id="86493-121">行動服務安裝程式與作業系統之間的對應</span><span class="sxs-lookup"><span data-stu-id="86493-121">Mobility Service installer-to-operating system mapping</span></span>

| <span data-ttu-id="86493-122">安裝程式檔案的範本名稱</span><span class="sxs-lookup"><span data-stu-id="86493-122">Installer file template name</span></span>| <span data-ttu-id="86493-123">作業系統</span><span class="sxs-lookup"><span data-stu-id="86493-123">Operating system</span></span> |
|---|--|
|<span data-ttu-id="86493-124">Microsoft-ASR\_UA\*Windows\*release.exe</span><span class="sxs-lookup"><span data-stu-id="86493-124">Microsoft-ASR\_UA\*Windows\*release.exe</span></span> | <span data-ttu-id="86493-125">Windows Server 2008 R2 SP1 (64 位元)</span><span class="sxs-lookup"><span data-stu-id="86493-125">Windows Server 2008 R2 SP1 (64-bit)</span></span> </br> <span data-ttu-id="86493-126">Windows Server 2012 (64 位元)</span><span class="sxs-lookup"><span data-stu-id="86493-126">Windows Server 2012 (64-bit)</span></span> </br> <span data-ttu-id="86493-127">Windows Server 2012 R2 (64 位元)</span><span class="sxs-lookup"><span data-stu-id="86493-127">Windows Server 2012 R2 (64-bit)</span></span> |
|<span data-ttu-id="86493-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="86493-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>| <span data-ttu-id="86493-129">Red Hat Enterprise Linux (RHEL) 6.4、6.5、6.6、6.7、6.8 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="86493-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> </br> <span data-ttu-id="86493-130">CentOS 6.4、6.5、6.6、6.7、6.8 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="86493-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> |
|<span data-ttu-id="86493-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="86493-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span> | <span data-ttu-id="86493-132">Red Hat Enterprise Linux (RHEL) 7.1、7.2 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="86493-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64-bit only)</span></span> </br> <span data-ttu-id="86493-133">CentOS 7.0、7.1、7.2 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="86493-133">CentOS 7.0, 7.1, 7.2 (64-bit only)</span></span></br> <span data-ttu-id="86493-134">CentOs 7.3 (僅限移轉)</span><span class="sxs-lookup"><span data-stu-id="86493-134">CentOs 7.3 (migration only)</span></span> |
|<span data-ttu-id="86493-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="86493-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>| <span data-ttu-id="86493-136">SUSE Linux Enterprise Server 11 SP3 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="86493-136">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span></span>|
|<span data-ttu-id="86493-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="86493-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>| <span data-ttu-id="86493-138">SUSE Linux Enterprise Server 11 SP4 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="86493-138">SUSE Linux Enterprise Server 11 SP4 (64-bit only)</span></span>|
|<span data-ttu-id="86493-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="86493-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span> | <span data-ttu-id="86493-140">Oracle Enterprise Linux 6.4、6.5 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="86493-140">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span></span>|
|<span data-ttu-id="86493-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="86493-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span> | <span data-ttu-id="86493-142">Ubuntu Linux 14.04 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="86493-142">Ubuntu Linux 14.04 (64-bit only)</span></span>|


## <a name="install-mobility-service-manually-by-using-the-gui"></a><span data-ttu-id="86493-143">使用 GUI 手動安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="86493-143">Install Mobility Service manually by using the GUI</span></span>

>[!IMPORTANT]
> <span data-ttu-id="86493-144">如果您是使用**設定伺服器**從一個 Azure 訂用帳戶/區域將 **Azure IaaS 虛擬機器**複寫到另一個 Azure 訂用帳戶/區域，請**使用以命令列為基礎的安裝方法**</span><span class="sxs-lookup"><span data-stu-id="86493-144">If you are using a **Configuration Server** to replicate **Azure IaaS virtual machines** from one Azure Subscription/Region to another then **use the Command-line based installation** method</span></span>

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a><span data-ttu-id="86493-145">在命令提示字元中手動安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="86493-145">Install Mobility Service manually at a command prompt</span></span>

### <a name="command-line-installation-on-a-windows-computer"></a><span data-ttu-id="86493-146">Windows 電腦上的命令列安裝</span><span class="sxs-lookup"><span data-stu-id="86493-146">Command-line installation on a Windows computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a><span data-ttu-id="86493-147">Linux 電腦上的命令列安裝</span><span class="sxs-lookup"><span data-stu-id="86493-147">Command-line installation on a Linux computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a><span data-ttu-id="86493-148">透過推送安裝從 Azure Site Recovery 安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="86493-148">Install Mobility Service by push installation from Azure Site Recovery</span></span>
<span data-ttu-id="86493-149">若要使用 Site Recovery 來執行行動服務安裝推送安裝，所有目標電腦都必須符合下列必要條件。</span><span class="sxs-lookup"><span data-stu-id="86493-149">To do a push installation of Mobility Service by using Site Recovery, all target computers must meet the following prerequisites.</span></span>

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
<span data-ttu-id="86493-150">安裝行動服務之後，選取 Azure 入口網站中的 [複寫] 按鈕以開始保護這些 VM。</span><span class="sxs-lookup"><span data-stu-id="86493-150">After Mobility Service is installed, in the Azure portal, select the **Replicate** button to start protecting these VMs.</span></span>

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a><span data-ttu-id="86493-151">將 Windows Server 電腦上的行動服務解除安裝</span><span class="sxs-lookup"><span data-stu-id="86493-151">Uninstall Mobility Service on a Windows Server computer</span></span>
<span data-ttu-id="86493-152">您可以使用下列其中一種方法將 Windows Server 電腦上的行動服務解除安裝。</span><span class="sxs-lookup"><span data-stu-id="86493-152">Use one of the following methods to uninstall Mobility Service on a Windows Server computer.</span></span>

### <a name="uninstall-by-using-the-gui"></a><span data-ttu-id="86493-153">使用 GUI 來解除安裝</span><span class="sxs-lookup"><span data-stu-id="86493-153">Uninstall by using the GUI</span></span>
1. <span data-ttu-id="86493-154">在 [控制台] 中，選取 [程式]。</span><span class="sxs-lookup"><span data-stu-id="86493-154">In Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="86493-155">選取 [Microsoft Azure Site Recovery Mobility Service/主要目標伺服器]，然後選取 [解除安裝]。</span><span class="sxs-lookup"><span data-stu-id="86493-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="86493-156">在命令提示字元中解除安裝</span><span class="sxs-lookup"><span data-stu-id="86493-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="86493-157">以系統管理員身分開啟 [命令提示字元] 視窗。</span><span class="sxs-lookup"><span data-stu-id="86493-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="86493-158">執行下列命令以將行動服務解除安裝：</span><span class="sxs-lookup"><span data-stu-id="86493-158">To uninstall Mobility Service, run the following command:</span></span>

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a><span data-ttu-id="86493-159">將 Linux 電腦上的行動服務解除安裝</span><span class="sxs-lookup"><span data-stu-id="86493-159">Uninstall Mobility Service on a Linux computer</span></span>
1. <span data-ttu-id="86493-160">在 Linux 伺服器上，以 **root** 使用者登入。</span><span class="sxs-lookup"><span data-stu-id="86493-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="86493-161">在終端機中，移至 /user/local/ASR。</span><span class="sxs-lookup"><span data-stu-id="86493-161">In a terminal, go to /user/local/ASR.</span></span>
3. <span data-ttu-id="86493-162">執行下列命令以將行動服務解除安裝：</span><span class="sxs-lookup"><span data-stu-id="86493-162">To uninstall Mobility Service, run the following command:</span></span>

```
uninstall.sh -Y
```
