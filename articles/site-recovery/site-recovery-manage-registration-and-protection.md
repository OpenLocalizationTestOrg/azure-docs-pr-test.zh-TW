---
title: "aaaRemove 伺服器並停用保護 |Microsoft 文件"
description: "本文說明如何 toounregister 伺服器從站台復原保存庫，和 toodisable 保護的虛擬機器和實體伺服器。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a>移除伺服器並停用保護

hello Azure Site Recovery 服務佔 tooyour 業務續航力和災害復原 (BCDR) 策略。 hello 服務會協調複寫、 容錯移轉和復原的虛擬機器和實體伺服器。 電腦可以是複寫的 tooAzure 或 tooa 次要內部部署資料中心。 如需快速概觀，請參閱 [什麼是 Azure Site Recovery？](site-recovery-overview.md)

本文說明如何 toounregister 伺服器，從 復原服務保存庫中 hello Azure 入口網站和 toodisable 保護機器的保護站台復原的方式。

將任何註解或問題張貼在本文中，或在 hello hello 下方[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="unregister-a-connected-configuration-server"></a>將已連線的組態伺服器取消註冊

如果您要複寫的 VMware Vm 或 Windows/Linux 實體伺服器 tooAzure，您可以伺服器取消登錄已連線的設定從保存庫，如下所示：

1. 停用機器保護。 在**受保護項目** > **複寫的項目**，以滑鼠右鍵按一下 hello 機器 >**刪除**。
2. 取消關聯任何原則。 在**Site Recovery 基礎結構** > **的 VMWare 及實體機器** > **複寫原則**，按兩下 hello相關聯的原則。 以滑鼠右鍵按一下 hello 組態伺服器 > **Disassociate**。
3. 移除任何額外的內部部署處理伺服器或主要目標伺服器。 在**Site Recovery 基礎結構** > **的 VMWare 及實體機器** > **設定伺服器**，以滑鼠右鍵按一下 hello 伺服器>**刪除**。
4. 刪除 hello 組態伺服器。
5. 手動解除安裝 hello hello 主要目標伺服器上執行的行動服務 (這會是另一個伺服器或 hello 組態伺服器上執行)。
6. 將任何額外的處理伺服器解除安裝。
7. Hello 組態伺服器解除安裝。
8. 在 hello 組態伺服器上解除安裝 hello 所安裝的站台復原的 MySQL 執行個體。
9. Hello 登錄 hello 組態伺服器中刪除 hello 金鑰``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``。

## <a name="unregister-a-unconnected-configuration-server"></a>將未連線的組態伺服器取消註冊

如果您要複寫的 VMware Vm 或 Windows/Linux 實體伺服器 tooAzure，可取消從保存庫未連接的組態伺服器，如下所示：

1. 停用機器保護。 在**受保護項目** > **複寫的項目**，以滑鼠右鍵按一下 hello 機器 >**刪除**。 選取**停止管理 hello 機器**。
2. 移除任何額外的內部部署處理伺服器或主要目標伺服器。 在**Site Recovery 基礎結構** > **的 VMWare 及實體機器** > **設定伺服器**，以滑鼠右鍵按一下 hello 伺服器>**刪除**。
3. 刪除 hello 組態伺服器。
4. 手動解除安裝 hello hello 主要目標伺服器上執行的行動服務 (這會是另一個伺服器或 hello 組態伺服器上執行)。
5. 將任何額外的處理伺服器解除安裝。
6. Hello 組態伺服器解除安裝。
7. 在 hello 組態伺服器上解除安裝 hello 所安裝的站台復原的 MySQL 執行個體。
8. Hello 登錄 hello 組態伺服器中刪除 hello 金鑰``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``。

## <a name="unregister-a-connected-vmm-server"></a>取消註冊已連線的 VMM 伺服器

最佳做法，建議您已連接 tooAzure 時，取消登錄 hello VMM 伺服器。 這可確保設定 hello VMM 伺服器上 （和其他與配對雲端的 VMM 伺服器上） 會正確清除。 您只應在連線發生永久性問題時，才移除未連線的伺服器。 如果 hello VMM 伺服器未連接，您將需要 toomanually 執行指令碼 tooclean 的設定。

1. 停止複寫 hello 想 tooremove VMM 伺服器上雲端中的 Vm。
2. 刪除任何 hello 想 toodelete VMM 伺服器上雲端所使用的網路對應。 在**Site Recovery 基礎結構** > **System Center VMM** > **網路對應**，以滑鼠右鍵按一下 hello 網路對應 > **刪除**。
3. 取消關聯 hello 想 tooremove VMM 伺服器上雲端的複寫的原則。  在**Site Recovery 基礎結構** > **System Center VMM** >  **複寫原則**，連按兩下 相關聯的 hello 原則。 以滑鼠右鍵按一下 hello 雲端 > **Disassociate**。
4. 刪除 hello VMM 伺服器或作用中 VMM 的節點。 在**Site Recovery 基礎結構** > **System Center VMM** > **VMM 伺服器**，以滑鼠右鍵按一下 hello 伺服器 > **刪除**。
5. 解除安裝 hello VMM 伺服器上手動 hello 提供者。 如果您有叢集，請將它從所有節點中移除。
6. 如果您要複寫 tooAzure，手動移除 hello Microsoft 復原服務代理程式從 hello 刪除雲端中的 HYPER-V 主機。



### <a name="unregister-an-unconnected-vmm-server"></a>取消註冊未連線的 VMM 伺服器

1. 停止複寫 hello 想 tooremove VMM 伺服器上雲端中的 Vm。
2. 刪除任何您想 toodelete hello VMM 伺服器上雲端所使用的網路對應。 在**Site Recovery 基礎結構** > **System Center VMM** > **網路對應**，以滑鼠右鍵按一下 hello 網路對應 > **刪除**。
3. 請注意 hello 識別碼 hello VMM 伺服器。
4. 取消關聯 hello 想 tooremove VMM 伺服器上雲端的複寫的原則。  在**Site Recovery 基礎結構** > **System Center VMM** >  **複寫原則**，連按兩下 相關聯的 hello 原則。 以滑鼠右鍵按一下 hello 雲端 > **Disassociate**。
5. 刪除 hello VMM 伺服器或作用中節點。 在**Site Recovery 基礎結構** > **System Center VMM** > **VMM 伺服器**，以滑鼠右鍵按一下 hello 伺服器 > **刪除**。
6. 下載並執行 hello[清除指令碼](http://aka.ms/asr-cleanup-script-vmm)hello VMM 伺服器上。 開啟 PowerShell 以 hello**系統管理員身分執行**選項，hello 預設 (LocalMachine) 範圍 toochange hello 執行原則。 在 hello 指令碼指定 hello 識別碼 hello 想 tooremove VMM 伺服器。 hello 指令碼會移除登錄與雲端配對 hello 伺服器的資訊。
5. 包含會與 hello 想 tooremove VMM 伺服器上的雲端配對的雲端的其他任何 VMM 伺服器上執行 hello 清除指令碼。
6. 任何其他被動 VMM 叢集節點上已安裝提供者的 hello 執行 hello 清除指令碼。
7. 解除安裝 hello VMM 伺服器上手動 hello 提供者。 如果您有叢集，請將它從所有節點中移除。
8. 如果您複寫 tooAzure，您可以移除 hello Microsoft 復原服務代理程式在 hello 刪除雲端中的 HYPER-V 主機。

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a>取消註冊 Hyper-V 站台中的 Hyper-V 主機

未受 VMM 管理的 Hyper-V 主機會集合成 Hyper-V 站台。 移除 Hyper-V 站台中的主機，方法如下：

1. 停用 HYPER-V Vm 位於 hello 主機上的複寫。
2. 取消關聯 hello HYPER-V 站台的原則。 在**Site Recovery 基礎結構** > **HYPER-V 站台的** >  **複寫原則**，連按兩下 相關聯的 hello 原則。 以滑鼠右鍵按一下 hello 網站 > **Disassociate**。
3. 刪除 Hyper-V 主機。 在**Site Recovery 基礎結構** > **System Center VMM** > **HYPER-V 主機**，以滑鼠右鍵按一下 hello 伺服器 > **刪除**。
4. 從中移除所有主機之後，請刪除 hello HYPER-V 站台。 在**Site Recovery 基礎結構** > **System Center VMM** > **HYPER-V 站台**，以滑鼠右鍵按一下 hello 網站 > **刪除**。
5. 執行下列指令碼，移除每個 HYPER-V 主機上的 hello。 hello 指令碼清除 hello 伺服器上的設定，並從 hello 保存庫取消註冊。


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping hello Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a>停用 VMware VM 或實體伺服器的保護

1. 在**受保護項目** > **複寫的項目**，以滑鼠右鍵按一下 hello 機器 >**刪除**。
2. 在 [移除機器] 中，選取下列其中一個選項：
    - **停用保護 （建議選項） 的 hello 機器**。 使用此選項 toostop，將 hello 機器複寫。 系統會自動清除 Site Recovery 設定。 您只會看到此選項，在下列情況下的 hello:
        - **調整 hello VM 磁碟區**— 當您調整磁碟區 hello 虛擬機器便會進入 「 重大 」 狀態。 選取此選項 toodisables 保護，同時保留在 Azure 中的復原點。 當您啟用 hello 機器的保護功能時，hello hello 調整磁碟區的資料會傳送的 tooAzure。
        - **您最近已執行容錯移轉**— 您已執行容錯移轉 tootest 您的環境之後，請選取此選項 toostart，一次保護內部部署機器。 它會停用每個虛擬機器，然後再 tooenable 保護它們一次。 停用這項設定的 hello 機器不會影響在 Azure 中的 hello 複本虛擬機器。 不要解除安裝 hello 機器 hello 行動服務。
    - **停止管理 hello 機器**。 如果您選取此選項時，只會移除 hello 機器 hello 保存庫中。 Hello 機器的內部部署保護設定不會受到影響。 tooremove hello 電腦及從 hello Azure 訂用帳戶的 tooremove hello 電腦上，您需要設定 tooclean hello 設定解除安裝 hello 行動服務。

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a>停用 VMM 雲端中 Hyper-V VM 的保護

1. 在**受保護項目** > **複寫的項目**，以滑鼠右鍵按一下 hello 機器 >**刪除**。
2. 在 [移除機器] 中，選取下列其中一個選項：

    - **停用保護 （建議選項） 的 hello 機器**。 使用此選項 toostop，將 hello 機器複寫。 系統會自動清除 Site Recovery 設定。
    - **停止管理 hello 機器**。 如果您選取此選項時，只會移除 hello 機器 hello 保存庫中。 Hello 機器的內部部署保護設定不會受到影響。 tooremove hello 電腦及從 hello Azure 訂用帳戶的 tooremove hello 電腦上的設定，您需要 tooclean hello 設定向上以手動方式，使用下列的 hello 指示。 請注意，是否您選取 toodelete hello 虛擬機器和其硬碟，將會移除這些 hello 目標位置。

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a>清理保護設定-複寫 tooa 次要 VMM 站台

如果您選取**停止管理 hello 機器**和複寫 tooa 次要站台，您可以執行這個指令碼在 hello 主要伺服器 tooclean hello hello 主要虛擬機器的設定。 Hello VMM 主控台中按一下 hello PowerShell 按鈕 tooopen hello VMM PowerShell 主控台。 SQLVM1 取代 hello 您的虛擬機器名稱。

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. Hello 次要 VMM 伺服器上執行此指令碼 tooclean，hello 次要虛擬機器的 hello 設定：

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. Hello 次要 VMM 伺服器上，重新整理 hello hello HYPER-V 主機伺服器上的虛擬機器，如此 hello 第二個 VM 取得偵測再次 hello VMM 主控台中。
4. 上述步驟 hello 清除 hello hello VMM 伺服器上的複寫設定。 如果您想 hello 虛擬機器，執行下列指令碼喔 hello toostop 複寫 hello 主要和次要的 Vm。 SQLVM1 取代 hello 您的虛擬機器名稱。

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a>清理保護設定-複寫 tooAzure

1. 如果您選取**停止管理 hello 機器**和您複寫 tooAzure、 hello 來源 VMM 伺服器上，從 hello VMM 主控台中使用 PowerShell 執行這個指令碼。
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. hello 上述步驟，請清除 hello hello VMM 伺服器上的複寫設定。 toostop hello hello HYPER-V 主機伺服器上所執行的虛擬機器的複寫執行這個指令碼。 SQLVM1 hello 名稱取代您的虛擬機器和 host01.contoso.com hello hello HYPER-V 主機伺服器名稱。

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a>停用對 Hyper-V 站台中 Hyper-V VM 的保護

如果您要複寫 HYPER-V Vm tooAzure 沒有 VMM 伺服器，請使用此程序。

1. 在**受保護項目** > **複寫的項目**，以滑鼠右鍵按一下 hello 機器 >**刪除**。
2. 在**移除機器**，您可以選取下列選項的 hello:

   - **停用保護 （建議選項） 的 hello 機器**。 使用此選項 toostop，將 hello 機器複寫。 系統會自動清除 Site Recovery 設定。
   - **停止管理 hello 機器**。 如果您選取此選項將只會從 hello 保存庫移除 hello 機器。 Hello 機器的內部部署保護設定不會受到影響。 tooremove hello 機器和從 hello Azure 訂用帳戶的 tooremove hello 虛擬機器上，您需要設定 tooclean hello 設定總手動。 如果您選取 toodelete hello 虛擬機器和其會移除 hello 目標位置的硬碟。
3. 如果您選取**停止管理 hello 機器**，執行這個 hello 來源 HYPER-V 主機伺服器上的指令碼、 tooremove hello 虛擬機器的複寫。 SQLVM1 取代 hello 您的虛擬機器名稱。

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
