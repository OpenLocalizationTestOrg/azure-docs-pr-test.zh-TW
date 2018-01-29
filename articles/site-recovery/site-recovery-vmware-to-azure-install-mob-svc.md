---
title: "安裝行動服務 (VMware 或實體至 Azure) | Microsoft Docs"
description: "了解如何安裝行動服務代理程式來保護您的內部部署電腦。"
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
ms.service: site-recovery
ms.topic: article
ms.date: 01/11/2018
ms.author: anoopkv
ms.openlocfilehash: 939115aedd624dde637f00c02865b1adab47c7c4
ms.sourcegitcommit: 7edfa9fbed0f9e274209cec6456bf4a689a4c1a6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="install-mobility-service-vmware-or-physical-to-azure"></a>安裝行動服務 (VMware 或實體至 Azure)
Azure Site Recovery 行動服務會擷取電腦上的資料寫入，然後將它們轉送至處理伺服器。 將行動服務部署至您要複寫至 Azure 的每部電腦 (VMware VM 或實體伺服器)。 您可以使用下列方法，將行動服務部署至您要保護的伺服器：


* [使用軟體部署工具 (例如 System Center Configuration Manager) 安裝行動服務](site-recovery-install-mobility-service-using-sccm.md)
* [使用 Azure 自動化和預期狀態設定 (Automation DSC) 安裝行動服務](site-recovery-automate-mobility-service-install.md)
* [使用圖形化使用者介面 (GUI) 手動安裝行動服務](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [在命令提示字元中手動安裝行動服務](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [透過推送安裝從 Site Recovery 安裝行動服務](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> 從版本 9.7.0.0 開始，在 Windows 虛擬機器 (VM) 上，行動服務安裝程式也會安裝最新可用的 [Azure VM 代理程式](../virtual-machines/windows/extensions-features.md#azure-vm-agent)。 當電腦容錯移轉至 Azure 時，該電腦必須符合代理程式安裝必要條件，才能使用任何 VM 擴充功能。

## <a name="prerequisites"></a>先決條件
在伺服器上手動安裝行動服務之前，必須先完成下列必要條件步驟：
1. 登入組態伺服器，然後以系統管理員身分開啟 [命令提示字元] 視窗。
2. 將目錄切換至 bin 資料夾，然後建立複雜密碼檔案：

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. 將複雜密碼檔案儲存於安全的位置。 您會在行動服務安裝期間使用該檔案。
4. 針對所有支援作業系統的行動服務安裝程式位於 %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository 資料夾中。

### <a name="mobility-service-installer-to-operating-system-mapping"></a>行動服務安裝程式與作業系統之間的對應

| 安裝程式檔案的範本名稱| 作業系統 |
|---|--|
|Microsoft-ASR\_UA\*Windows\*release.exe | Windows Server 2008 R2 SP1 (64 位元) </br> Windows Server 2012 (64 位元) </br> Windows Server 2012 R2 (64 位元) </br> Windows Server 2016 (64 位元) |
|Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz| Red Hat Enterprise Linux (RHEL) 6.4、6.5、6.6、6.7、6.8、6.9 (僅限 64 位元) </br> CentOS 6.4、6.5、6.6、6.7、6.8、6.9 (僅限 64 位元) |
|Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz | Red Hat Enterprise Linux (RHEL) 7.1、7.2、7.3 (僅限 64 位元) </br> CentOS 7.0、7.1、7.2、7.3 (僅限 64 位元) |
|Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP3 (僅限 64 位元)|
|Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP4 (僅限 64 位元)|
|Microsoft-ASR\_UA\*OL6-64\*release.tar.gz | Oracle Enterprise Linux 6.4、6.5 (僅限 64 位元)|
|Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz | Ubuntu Linux 14.04 (僅限 64 位元)|
|Microsoft-ASR\_UA\*UBUNTU-16.04-64\*release.tar.gz | Ubuntu Linux 16.04 LTS 伺服器 (僅限 64 位元)|
|Microsoft-ASR_UA\*DEBIAN7-64\*release.tar.gz | Debian 7 (僅限 64 位元)|
|Microsoft-ASR_UA\*DEBIAN8-64\*release.tar.gz | Debian 8 (僅限 64 位元)|


## <a name="install-mobility-service-manually-by-using-the-gui"></a>使用 GUI 手動安裝行動服務

>[!IMPORTANT]
> 如果您是使用「設定伺服器」從某個 Azure 訂用帳戶/區域將「Azure IaaS 虛擬機器」複寫到另一個 Azure 訂用帳戶/區域，請「使用以命令列為基礎的安裝方法」

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a>在命令提示字元中手動安裝行動服務

### <a name="command-line-installation-on-a-windows-computer"></a>Windows 電腦上的命令列安裝
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a>Linux 電腦上的命令列安裝
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a>透過推送安裝從 Azure Site Recovery 安裝行動服務
若要使用 Site Recovery 來執行行動服務的推送安裝，所有目標電腦都必須符合下列必要條件：

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
安裝行動服務之後，選取 Azure 入口網站中的 [+複寫] 按鈕以開始保護這些 VM。

## <a name="update-mobility-service"></a>更新行動服務

> [!WARNING]
> 在開始更新受保護伺服器上的行動服務之前，請確保設定伺服器、相應放大處理序伺服器，以及作為部署之一部分的所有主要目標伺服器皆已完成更新。

1. 在 Azure 入口網站上，請瀏覽至 <Your Vault> -> [複寫的項目] 檢視。
2. 如果「設定伺服器」已經更新至最新版本，您應該會看到內容為「有新的 Site Recovery 複寫代理程式更新可用。按一下可安裝」的通知

     ![ReplicatedItems](.\media\site-recovery-vmware-to-azure-install-mob-svc\replicated-item-notif.png)
3. 按一下該通知以開啟虛擬機器選取頁面。
4. 選取要升級行動服務的虛擬機器，然後按一下 [確定] 按鈕。

     ![ReplicatedItemsVMList](.\media\site-recovery-vmware-to-azure-install-mob-svc\update-okpng.png)
5. 這將會針對每個選取的虛擬機器啟動「更新行動服務」作業。

> [!NOTE]
> [深入了解](site-recovery-vmware-to-azure-manage-configuration-server.md)如何更新用來安裝行動服務之帳戶的密碼

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a>將 Windows Server 電腦上的行動服務解除安裝
您可以使用下列其中一種方法將 Windows Server 電腦上的行動服務解除安裝。

### <a name="uninstall-by-using-the-gui"></a>使用 GUI 來解除安裝
1. 在 [控制台] 中，選取 [程式]。
2. 選取 [Microsoft Azure Site Recovery Mobility Service/主要目標伺服器]，然後選取 [解除安裝]。

### <a name="uninstall-at-a-command-prompt"></a>在命令提示字元中解除安裝
1. 以系統管理員身分開啟 [命令提示字元] 視窗。
2. 執行下列命令以將行動服務解除安裝：

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a>將 Linux 電腦上的行動服務解除安裝
1. 在 Linux 伺服器上，以 **root** 使用者登入。
2. 在終端機中，移至 /user/local/ASR。
3. 執行下列命令以將行動服務解除安裝：

```
uninstall.sh -Y
```
