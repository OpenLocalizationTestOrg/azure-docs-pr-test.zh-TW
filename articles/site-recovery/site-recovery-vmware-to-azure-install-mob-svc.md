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
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a>安裝行動服務 （VMware 或實體 tooAzure）
Azure Site Recovery Mobility 服務擷取的電腦上，資料寫入，並再將它們轉送 toohello 處理序伺服器。 部署行動服務 tooevery 電腦 （VMware VM 或實體伺服器） 的 tooreplicate tooAzure。 您可以部署您使用下列方法 hello 想 tooprotect 行動服務 toohello 伺服器：


* [使用軟體部署工具 (例如 System Center Configuration Manager) 安裝行動服務](site-recovery-install-mobility-service-using-sccm.md)
* [使用 Azure 自動化和預期狀態設定 (Automation DSC) 安裝行動服務](site-recovery-automate-mobility-service-install.md)
* [使用 hello 圖形化使用者介面 (GUI)，以手動方式安裝行動服務](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [在命令提示字元中手動安裝行動服務](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [透過推送安裝從 Azure Site Recovery 安裝行動服務](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> 開頭為 Windows 虛擬機器 (Vm) 上的版本 9.7.0.0，hello 行動服務安裝程式也會安裝 hello 的最新可用[Azure VM 代理程式](../virtual-machines/windows/extensions-features.md#azure-vm-agent)。 當電腦容錯移轉 tooAzure 時，hello 電腦符合 hello 代理程式安裝使用任何 VM 擴充功能的必要條件。

## <a name="prerequisites"></a>必要條件
在伺服器上手動安裝行動服務之前，必須先完成下列必要條件步驟：
1. 登入 tooyour 組態伺服器上，然後開啟 命令提示字元視窗，以系統管理員。
2. 變更 hello 目錄 toohello bin 資料夾，然後再建立 複雜密碼檔案：

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. Hello 複雜密碼檔案存放在安全的位置。 您在 hello 行動服務安裝期間使用 hello 檔案。
4. 適用於所有支援作業系統的行動服務安裝程式都 hello %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository 資料夾中。

### <a name="mobility-service-installer-to-operating-system-mapping"></a>行動服務安裝程式與作業系統之間的對應

| 安裝程式檔案的範本名稱| 作業系統 |
|---|--|
|Microsoft-ASR\_UA\*Windows\*release.exe | Windows Server 2008 R2 SP1 (64 位元) </br> Windows Server 2012 (64 位元) </br> Windows Server 2012 R2 (64 位元) |
|Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz| Red Hat Enterprise Linux (RHEL) 6.4、6.5、6.6、6.7、6.8 (僅限 64 位元) </br> CentOS 6.4、6.5、6.6、6.7、6.8 (僅限 64 位元) |
|Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz | Red Hat Enterprise Linux (RHEL) 7.1、7.2 (僅限 64 位元) </br> CentOS 7.0、7.1、7.2 (僅限 64 位元)</br> CentOs 7.3 (僅限移轉) |
|Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP3 (僅限 64 位元)|
|Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP4 (僅限 64 位元)|
|Microsoft-ASR\_UA\*OL6-64\*release.tar.gz | Oracle Enterprise Linux 6.4、6.5 (僅限 64 位元)|
|Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz | Ubuntu Linux 14.04 (僅限 64 位元)|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a>使用 hello GUI 手動安裝行動服務

>[!IMPORTANT]
> 如果您使用**組態伺服器**tooreplicate **Azure IaaS 虛擬機器**從一個 Azure 訂用帳戶/地區 tooanother 然後**使用 hello 命令列基礎的安裝**方法

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a>在命令提示字元中手動安裝行動服務

### <a name="command-line-installation-on-a-windows-computer"></a>Windows 電腦上的命令列安裝
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a>Linux 電腦上的命令列安裝
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a>透過推送安裝從 Azure Site Recovery 安裝行動服務
toodo 的行動服務推入安裝使用 Site Recovery，所有目標電腦必須都符合下列必要條件 hello。

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
行動服務安裝在 hello Azure 入口網站後，選取 hello**複寫**按鈕 toostart 保護這些 Vm。

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a>將 Windows Server 電腦上的行動服務解除安裝
使用其中一個 Windows Server 電腦上遵循方法 toouninstall 行動服務的 hello。

### <a name="uninstall-by-using-hello-gui"></a>解除安裝使用 hello GUI
1. 在 [控制台] 中，選取 [程式]。
2. 選取 [Microsoft Azure Site Recovery Mobility Service/主要目標伺服器]，然後選取 [解除安裝]。

### <a name="uninstall-at-a-command-prompt"></a>在命令提示字元中解除安裝
1. 以系統管理員身分開啟 [命令提示字元] 視窗。
2. 執行下列命令的 hello toouninstall 行動服務：

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a>將 Linux 電腦上的行動服務解除安裝
1. 在 Linux 伺服器上，以 **root** 使用者登入。
2. 在終端機中，移太/使用者/本機/ASR。
3. 執行下列命令的 hello toouninstall 行動服務：

```
uninstall.sh -Y
```
