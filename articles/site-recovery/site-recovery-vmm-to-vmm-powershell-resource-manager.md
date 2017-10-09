---
title: "aaaReplicate VMM tooa 次要站台中的 HYPER-V Vm，使用 PowerShell (Azure Resource Manager) |Microsoft 文件"
description: "描述如何 toodeploy Azure Site Recovery tooorchestrate 複寫、 容錯移轉和復原 VMM 中的 HYPER-V Vm 的雲端 tooa 次要部署 VMM 站台使用 PowerShell （資源管理員）"
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a>複寫 HYPER-V 虛擬機器在 VMM 雲端 tooa 次要 VMM 站台使用 PowerShell （資源管理員）
> [!div class="op_single_selector"]
> * [Azure 入口網站](site-recovery-vmm-to-vmm.md)
> * [傳統入口網站](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - 資源管理員](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

歡迎使用 tooAzure Site Recovery ！ 如果您想 tooreplicate 內部管理 System Center Virtual Machine Manager (VMM) 雲端 tooa 次要站台中的 HYPER-V 虛擬機器，請使用這份文件。

本文章將示範如何 toouse PowerShell tooautomate 一般工作時，您需要 tooperform 您在 System Center VMM 雲端 tooSystem Center 次要站台中的 VMM 雲端中設定 Azure Site Recovery tooreplicate HYPER-V 虛擬機器。

hello 發行項包含 hello 案例的先決條件，並示範您

* 如何復原服務保存庫註冊 tooset
* Hello 來源 VMM 伺服器與 hello 目標 VMM 伺服器上安裝 Azure Site Recovery Provider hello
* Hello 保存庫中註冊 hello VMM 伺服器
* 設定 hello VMM 雲端的複寫原則。 會套用的 tooall 受保護的虛擬機器 hello hello 原則中的複寫設定。
* 啟用 hello 虛擬機器的保護。
* Hello 的測試容錯移轉 Vm 個別或做為復原計劃 toomake 確定一切如預期般運作的一部分。
* 執行的已規劃或未規劃的容錯移轉的 Vm，個別或做為復原計劃 toomake 確定一切如預期般運作的一部分。

如果您遇到此案例中所設定的問題時，請張貼您的問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

> [!NOTE]
> Azure 建立和處理資源的 [部署模型](../azure-resource-manager/resource-manager-deployment-model.md) 有二種：Azure Resource Manager 和傳統。 Azure 也有兩個入口網站 – hello Azure 傳統入口網站支援 hello 傳統部署模型，與 hello Azure 入口網站支援這兩種部署模型。 本文涵蓋 hello Resource Manager 部署模型。
>
>

## <a name="on-premises-prerequisites"></a>內部部署必要條件
以下是您將需要在 hello 主要和次要內部部署站台 toodeploy 此案例中：

| **必要條件** | **詳細資料** |
| --- | --- |
| **VMM** |我們建議您部署中的 VMM 伺服器 hello 主要站台和 hello 次要站台之 VMM 伺服器。<br/><br/> 您也可以[在單一 VMM 伺服器上的雲端之間進行複寫](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment)。 toodo 這將需要至少兩個雲端 hello VMM 伺服器上設定。<br/><br/> VMM 伺服器應至少執行 System Center 2012 SP1 含 hello 最新的更新。<br/><br/> 每個 VMM 伺服器必須能夠在其中一個或更多雲端設定，而且所有雲端必須有 hello HYPER-V 容量設定檔集合。 <br/><br/>雲端必須包含一或多個 VMM 主機群組。<br/><br/>深入了解設定 VMM 雲端中[設定 hello VMM 雲端網狀架構](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)，和[逐步解說： 使用 System Center 2012 SP1 VMM 建立私人雲端](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx)。<br/><br/> VMM 伺服器必須能夠存取網際網路。 |
| **Hyper-V** |HYPER-V 的伺服器必須至少執行 Windows Server 2012 與 hello HYPER-V 角色和擁有 hello 安裝最新的更新。<br/><br/> Hyper-V 伺服器應該包含一或多部 VM。<br/><br/>  HYPER-V 主機伺服器應該位於 hello 主要和次要 VMM 雲端中的主機群組。<br/><br/> 如果您是在 Windows Server 2012 R2 上的叢集中執行 Hyper-V，則應該安裝[更新 2961977](https://support.microsoft.com/kb/2961977)。<br/><br/> 如果您是在 Windows Server 2012 上的叢集中執行 Hyper-V，請注意，當您的叢集是靜態 IP 位址型叢集時，並不會自動建立叢集代理。 您以手動方式將需要 tooconfigure hello 叢集代理人。 [閱讀更多資訊](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx)。 |
| **提供者** |Site Recovery 部署期間，請在 VMM 伺服器上安裝 hello Azure Site Recovery Provider。 透過 HTTPS 443 tooorchestrate 複寫，hello 提供者進行通訊與站台復原。 透過 hello LAN hello 主要和次要 HYPER-V 伺服器或 VPN 連線之間，進行資料複寫。<br/><br/> hello hello VMM 伺服器上執行的提供者需要存取 toothese Url: *。.hypervrecoverymanager.windowsazure.com;*。 accesscontrol.windows.net;*。 backup.windowsazure.com;*。 account>.blob.core.windows.net;*。 store.core.windows.net。<br/><br/> 此外，則允許從 hello VMM 伺服器 toohello 防火牆通訊[Azure 資料中心 IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)並允許 hello HTTPS (443) 通訊協定。 |

### <a name="network-mapping-prerequisites"></a>網路對應的必要條件
Hello 主要和次要 VMM 伺服器上的 VMM VM 網路之間的網路對應會：

* 容錯移轉之後，選擇性地在次要 Hyper-V 主機上放置複本 VM。
* 複本 Vm tooappropriate VM 網路連線。
* 如果您未設定網路對應複本 Vm 不是連接的 tooany 網路容錯移轉之後。
* 如果您想 tooset 網路站台復原期間將對應部署以下是您將需要：

  * 請確定 hello 來源 HYPER-V 主機伺服器上的 Vm 的連線的 tooa VMM VM 網路。 該網路應連結的 tooa hello 雲端相關聯的邏輯網路。
  * 請確認 hello 您將用於復原的次要雲端已設定的對應 VM 網路。 該 VM 網路應連結的 tooa hello 次要雲端相關聯的邏輯網路。

深入了解在 hello 以下文章中設定 VMM 網路

* [如何在 VMM 中的 tooconfigure 邏輯網路](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [如何 tooconfigure VM 網路和閘道在 VMM 中](http://go.microsoft.com/fwlink/p/?LinkId=386308)

[深入了解](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) 網路對應的運作方式。

### <a name="powershell-prerequisites"></a>PowerShell 必要條件
請確定您具有 Azure PowerShell 準備 toogo。 如果您已經使用 PowerShell，您將需要 tooupgrade tooversion 0.8.10 或更新版本。 PowerShell 設定的詳細資訊，請參閱 hello[引導 tooinstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。 一旦您已安裝並設定 PowerShell，您可以檢視所有 hello 可用的 hello 服務 cmdlet[這裡](/powershell/azure/overview)。

toolearn 的相關技巧，可協助您使用 hello cmdlet，例如如何參數值、 輸入和輸出通常處理 Azure PowerShell，請參閱 hello[引導 tooget 開始使用 Azure Cmdlet](/powershell/azure/get-started-azureps)。

## <a name="step-1-set-hello-subscription"></a>步驟 1： 設定 hello 訂用帳戶
1. 從 Azure powershell、 Azure 帳戶的登入 tooyour： 使用下列 cmdlet 的 hello

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. 取得您的訂用帳戶清單。 這也會列出 hello 訂用帳戶每一個 hello 訂用帳戶。 記下您想在其中 toocreate hello 復原服務保存庫的 hello 訂用帳戶的 hello subscriptionID    

        Get-AzureRmSubscription
3. 設定中的 hello 復原服務保存庫是由一提 hello 訂用帳戶 ID 的 toobe hello 訂用帳戶

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a>步驟 2：建立復原服務保存庫
1. 如果您還沒有 Azure Resource Manager 資源群組，請建立一個

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. 建立新的復原服務保存庫並儲存在變數 （會使用更新版本） 中建立 ASR 保存庫物件的 hello。 您也可以擷取 hello ASR 保存庫後建立物件使用 hello Get AzureRMRecoveryServicesVault 指令程式:-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>步驟 3： 設定 hello 復原服務保存庫內容
1. 如果您已經建立的保存庫，執行下列命令 tooget hello 保存庫的 hello。

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. 藉由執行下列命令 hello 設定 hello 保存庫的內容。

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>步驟 4： 安裝 hello Azure Site Recovery Provider
1. Hello VMM 在電腦上，執行下列命令的 hello 建立目錄：

       New-Item c:\ASR -type directory
2. 擷取使用 hello 下載提供者藉由執行下列命令的 hello hello 檔案

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. 安裝 hello 提供者使用 hello 下列命令：

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   等候 hello 安裝 toofinish。
4. 使用下列命令的 hello hello 保存庫中註冊伺服器 hello:

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a>步驟 5︰建立複寫原則並建立關聯
1. 建立 HYPER-V 2012 R2 複寫原則，藉由執行下列命令的 hello:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > hello VMM 雲端中可包含 HYPER-V 主機執行不同版本的 Windows Server （如 hello HYPER-V 必要條件中所述），但 hello 複寫原則是特定的作業系統版本。 如果您有執行不同作業系統版本的主機，則請針對每一種作業系統版本建立不同的複寫原則。 例如︰如果您有五部主機在 Windows Server 2012 上執行，有三部在 Windows Server 2012 R2 上執行，則請建立兩個複寫原則 – 每一種作業系統版本使用一個。

1. 收到 hello 主要的保護容器 （主要 VMM 雲端） 和復原保護容器 （復原的 VMM 雲端），藉由執行下列命令的 hello:

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. 擷取您在步驟 1 所使用的 hello 原則 hello hello 原則的好記的名稱

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. 開始 hello 複寫原則中的 hello hello 保護容器 （VMM 雲端） 的關聯：

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. 等候 hello 原則關聯工作 toocomplete。 您可以檢查 hello 作業已使用下列 PowerShell 程式碼片段的 hello 來完成。

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   Hello 作業已完成處理之後，執行下列命令的 hello:

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

toocheck hello 完成 hello 作業時，請依照下列中的 hello 步驟[監視活動](#monitor)。

## <a name="step-6-configure-network-mapping"></a>步驟 6：設定網路對應
1. hello 第一個命令會取得 hello 目前 Azure Site Recovery 保存庫中的伺服器。 hello 命令儲存 hello Microsoft Azure Site Recovery 伺服器 hello $Servers 陣列變數中。

        $Servers = Get-AzureRmSiteRecoveryServer
2. hello，下列命令會取得 hello 站台復原 hello 來源 VMM 伺服器和網路 hello 目標 VMM 伺服器。

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > 第一個或 hello 第二個一個在 hello 伺服器陣列，可以 hello hello 來源 VMM 伺服器。 請檢查 hello hello VMM 伺服器名稱，並適當地取得 hello 網路


1. hello 最終 cmdlet 會建立 hello 主要網路與 hello 復原網路之間的對應。 hello 指令程式會指定 hello 主要網路作為 hello $PrimaryNetworks 和 hello $RecoveryNetworks hello 第一個項目與復原網路的第一個項目。

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a>步驟 7：設定儲存體對應
1. hello，下列命令會取得 hello 到 $storageclassifications 變數的儲存體分類清單。

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. hello，下列命令取得 hello 來源分類到 $SourceClassificaion 變數和目標分類到 $TargetClassification 變數。

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > hello 來源與目標分類可以 hello 陣列中的任何項目。 請參閱下面命令 toofigure hello 索引，來源與目標分類 $storageclassifications 陣列中的 hello toohello 輸出。

    > Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table


1. hello 以下指令程式會建立 hello 來源分類與 hello 目標分類之間的對應。

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a>步驟 8：對虛擬機器啟用保護
Hello 伺服器、 雲端和網路已正確設定之後，您可以啟用 hello 雲端中的虛擬機器的保護。

1. tooenable 保護，執行下列命令 tooget hello 保護容器 hello:

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. 取得 hello 保護實體 (VM) 執行下列命令的 hello:

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. 執行下列命令的 hello 啟用 hello VM 的複寫：

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a>測試您的部署
tootest 規劃您的部署，您可以執行測試容錯移轉的單一虛擬機器，或建立復原方案包含多個虛擬機器並執行測試容錯移轉的 hello。 測試容錯移轉會在隔離的網路中模擬您的容錯移轉與復原機制。

> [!NOTE]
> 您可以在 Azure 入口網站中為應用程式建立復原方案。
>
>

toocheck hello 完成 hello 作業時，請依照下列中的 hello 步驟[監視活動](#monitor)。

### <a name="run-a-test-failover"></a>執行測試容錯移轉
1. 執行以下 cmdlet tooget hello VM 網路 toowhich hello 想 tootest 容錯移轉 Vm。

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. 執行測試容錯移轉的 VM 執行 hello 下列動作：

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. 藉由 hello 下列執行復原計劃的測試容錯移轉：

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a>執行計劃性容錯移轉
1. 執行規劃的容錯移轉的 VM 執行 hello 下列動作：

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. 執行規劃的容錯移轉復原方案執行 hello 下列：

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a>執行非計劃性容錯移轉
1. 執行規劃的容錯移轉的 VM 執行 hello 下列：

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

2.執行規劃的容錯移轉復原方案執行 hello 下列：

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <a name=monitor></a>監視活動
使用下列命令 toomonitor hello 活動 hello。 請注意，您 toowait 之間 hello 處理 toofinish 的作業。

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a>後續步驟
[閱讀更多](/powershell/module/azurerm.recoveryservices.backup/#recovery) 使用 Azure Resource Manager PowerShell Cmdlet 進行 Azure Site Recovery 的相關資訊。
