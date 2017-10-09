---
title: "使用 Azure Site Recovery 和 PowerShell （資源管理員） 的 VMM 雲端中的 aaaReplicate HYPER-V 虛擬機器 |Microsoft 文件"
description: "使用 Azure Site Recovery 及 PowerShell 複寫 VMM 雲端中的 HYPER-V 虛擬機器"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a>使用 PowerShell 和 Azure 資源管理員的 VMM 雲端 tooAzure 中的 HYPER-V 虛擬機器，複寫
> [!div class="op_single_selector"]
> * [Azure 入口網站](site-recovery-vmm-to-azure.md)
> * [PowerShell - 資源管理員](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [傳統入口網站](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - 傳統](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a>概觀
Azure Site Recovery 提供 tooyour 業務續航力和災害復原 (BCDR) 策略可藉由協調複寫、 容錯移轉和復原的虛擬機器中部署案例的數目。 如需完整的部署案例請參閱 hello [Azure 站台復原概觀](site-recovery-overview.md)。

本文章將示範如何 toouse PowerShell tooautomate 一般工作時，您需要 tooperform 您設定 Azure Site Recovery tooreplicate HYPER-V 虛擬機器在 System Center VMM 雲端 tooAzure 儲存體中。

hello 發行項包含 hello 案例的先決條件，並示範您

* 如何復原服務保存庫註冊 tooset
* Hello 來源 VMM 伺服器上安裝 Azure Site Recovery Provider hello
* Hello 保存庫中註冊伺服器 hello、 新增 Azure 儲存體帳戶
* HYPER-V 主機伺服器上安裝 hello Azure 復原服務代理程式
* 設定會套用的 tooall 受保護的虛擬機器的 VMM 雲端的保護設定
* 為那些虛擬機器啟用保護。
* 測試容錯移轉 hello toomake，確定一切如預期般運作。

如果您遇到此案例中所設定的問題時，請張貼您的問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

> [!NOTE]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。 本文說明如何使用 hello Resource Manager 部署模型。
>
>

## <a name="before-you-start"></a>開始之前
確認您已備妥這些必要條件：

### <a name="azure-prerequisites"></a>Azure 必要條件
* 您將需要 [Microsoft Azure](https://azure.microsoft.com/) 帳戶。 如果您沒有此帳戶，請先前往 [免費帳戶](https://azure.microsoft.com/free)。 此外，您可以閱讀 hello [Azure Site Recovery Manager 定價](https://azure.microsoft.com/pricing/details/site-recovery/)。
* 如果您嘗試出 hello 複寫 tooa CSP 訂閱案例，您將需要 CSP 訂用帳戶。 深入了解中的 hello CSP 程式[如何在 hello CSP 程式 tooenroll](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx)。
* 您將需要 Azure v2 存放裝置 （資源管理員） 帳戶 toostore 複寫資料 tooAzure。 hello 帳戶必須啟用異地複寫。 在 hello 與 hello Azure Site Recovery 服務相同的區域和 hello 與相關聯，它應該是相同的訂用帳戶或 hello CSP 訂用帳戶。 toolearn 進一步了解設定 Azure 儲存體，請參閱 hello[簡介 tooMicrosoft Azure 儲存體](../storage/common/storage-introduction.md)供參考。
* 您必須確定您想 tooprotect 虛擬機器符合 hello toomake [Azure 虛擬機器必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。

> [!NOTE]
> 目前，只有 VM 層級作業可以通過 Powershell。 即將推出對復原計劃層級作業的支援。  現在，您必須是有限的 tooperforming 容錯移轉只能在 'protected VM' 資料粒度，而不是在復原方案層級。
>
>

### <a name="vmm-prerequisites"></a>VMM 必要條件
* 您將需要在在 System Center 2012 R2 上執行的 VMM 伺服器。
* 您所要的任何包含虛擬機器的 VMM 伺服器 tooprotect 必須執行 hello Azure Site Recovery Provider。 這會在 hello Azure Site Recovery 部署期間安裝。
* 您必須在 hello 想 tooprotect VMM 伺服器上的至少一個雲端。 hello 雲端應包含：
  * 一或多個 VMM 主機群組。
  * 每個主機群組中的一或多個 Hyper-V 主機伺服器或叢集。
  * 一或多個虛擬機器 hello 來源 HYPER-V 伺服器上。
* 深入了解設定 VMM 雲端：
  * 深入了解私人 VMM 雲端中[What's New in 搭配 System Center 2012 R2 VMM 的私人雲端](http://go.microsoft.com/fwlink/?LinkId=324952)和[VMM 2012 和 hello 雲端](http://go.microsoft.com/fwlink/?LinkId=324956)。
  * 深入了解[設定 hello VMM 雲端網狀架構](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)
  * 在您備妥雲端網狀架構元素之後，如需了解如何建立私人雲端，請參閱[在 VMM 中建立私人雲端](http://go.microsoft.com/fwlink/p/?LinkId=324953)及[逐步解說：使用 System Center 2012 SP1 VMM 建立私人雲端](http://go.microsoft.com/fwlink/p/?LinkId=324954)。

### <a name="hyper-v-prerequisites"></a>Hyper-V 的必要條件
* hello HYPER-V 主機伺服器必須執行至少**Windows Server 2012**與 HYPER-V 角色或**Microsoft HYPER-V Server 2012**和擁有 hello 安裝最新的更新。
* 如果您在叢集中執行 Hyper-V，請注意，如果您具有靜態 IP 位址叢集，並不會自動建立叢集代理。 您以手動方式將需要 tooconfigure hello 叢集代理人。 如需
* 如需指示，請參閱[如何 tooConfigure HYPER-V 複本代理人](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx)。
* 必須包含任何 HYPER-V 主機伺服器或叢集，您會想 toomanage 保護 VMM 雲端中。

### <a name="network-mapping-prerequisites"></a>網路對應的必要條件
當您保護 Azure 中虛擬機器時，hello 進行網路對應 hello hello 來源 VMM 伺服器與目標 Azure 網路 tooenable hello 下列上的虛擬機器網路：

* 容錯移轉 hello 相同的所有機器網路可以連接 tooeach 其他，無論它們是在復原計劃。
* 如果網路閘道 hello 目標 Azure 網路上的安裝程式，虛擬機器可以連接 tooother 在內部部署虛擬機器。
* 如果您未設定網路對應，僅 hello 容錯移轉 hello 中相同的虛擬機器容錯移轉 tooAzure 後，即可能 tooconnect tooeach 其他復原方案。

如果您想 toodeploy 網路對應，您將需要下列 hello:

* hello 想 tooprotect hello 來源 VMM 伺服器上的虛擬機器應連接的 tooa VM 網路。 該網路應連結的 tooa hello 雲端相關聯的邏輯網路。
* Azure 網路 toowhich 複寫虛擬機器可以容錯移轉之後連接。 您將在容錯移轉的 hello 階段選取此網路。 hello 網路應位於 hello 與 Azure Site Recovery 訂用帳戶相同的區域。

在下列內容中深入了解網路對應

* [如何在 VMM 中的 tooconfigure 邏輯網路](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [如何 tooconfigure VM 網路和閘道在 VMM 中](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [如何 tooconfigure 和監視 Azure 中的虛擬網路](https://azure.microsoft.com/documentation/services/virtual-network/)

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
1. 在 Azure Resource Manager 中建立一個資源群組 (如果您還沒有資源群組)

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. 建立新的復原服務保存庫並儲存在變數 （會使用更新版本） 中建立 ASR 保存庫物件的 hello。 您也可以擷取 hello ASR 保存庫後建立物件使用 hello Get AzureRMRecoveryServicesVault 指令程式:-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>步驟 3： 設定 hello 復原服務保存庫內容

藉由執行下列命令 hello 設定 hello 保存庫的內容。

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

## <a name="step-5-create-an-azure-storage-account"></a>步驟 5：建立 Azure 儲存體帳戶

如果您沒有 Azure 儲存體帳戶，建立 啟用地理複寫帳戶在 hello 同一地區 hello 保存庫執行 hello 下列命令：

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

請注意，hello 儲存體帳戶必須在 hello 與 hello Azure Site Recovery 服務相同的區域和與其相關聯 hello 相同訂用帳戶。

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>步驟 6： 安裝 Azure Recovery Services Agent hello
1. 下載 hello Azure 復原服務代理程式在[http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) ，而且它位於 hello VMM 每部 HYPER-V 主機伺服器上雲端您安裝想 tooprotect。
2. 執行下列命令，在所有 VMM 主機上的 hello:

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a>步驟 7：設定雲端保護設定
1. 建立複寫原則 tooAzure 藉由執行下列命令的 hello:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. 藉由執行下列命令的 hello 取得保護容器：

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. 收到 hello 原則詳細資料 tooa 變數使用 hello 作業所建立然後提及 hello 原則的易記名稱：

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. 開始 hello 複寫原則中的 hello hello 保護容器的關聯：

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. Hello 工作已完成之後，執行下列命令的 hello:

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. Hello 作業已完成處理之後，執行下列命令的 hello:

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

toocheck hello 完成 hello 作業時，請依照下列中的 hello 步驟[監視活動](#monitor)。

## <a name="step-8-configure-network-mapping"></a>步驟 8：設定網路對應
開始之前請確認網路對應 hello 來源 VMM 伺服器上的虛擬機器會連接的 tooa VM 網路。 此外，請建立一或多個 Azure 虛擬網路。

深入了解如何 toocreate 的虛擬網路中，使用 Azure 資源管理員和 PowerShell，[使用站對站 VPN 連線使用 Azure 資源管理員和 PowerShell 建立虛擬網路](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

請注意，多個虛擬機器網路可以是對應的 tooa 單一 Azure 網路。 如果 hello 目標網路有多個子網路，而且其中一個子網路具有 hello 相同的 hello 來源虛擬機器上的子網路的名稱，則 hello 複本虛擬機器將會連接的 toothat 目標子網路容錯移轉之後。 如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器會連接的 toohello hello 網路中的第一個子網路。

1. hello 第一個命令會取得 hello 目前 Azure Site Recovery 保存庫中的伺服器。 hello 命令儲存 hello Microsoft Azure Site Recovery 伺服器 hello $Servers 陣列變數中。

        $Servers = Get-AzureRmSiteRecoveryServer
2. hello 第二個命令會取得 hello hello 第一部伺服器的站台復原網路 hello $Servers 陣列中。 hello 命令儲存 hello 網路 hello $Networks 變數中。

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. hello 第三個命令會取得 Azure 的虛擬網路，然後該值 hello $AzureVmNetworks 變數中。

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. hello 最終 cmdlet 會建立 hello 主要網路與 hello Azure 虛擬機器網路之間的對應。 hello 指令程式會指定 hello 主要網路作為 $Networks hello 第一個項目。 hello cmdlet 會指定虛擬機器網路為 $AzureVmNetworks hello 第一個項目。

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a>步驟 9：對虛擬機器啟用保護
Hello 伺服器、 雲端和網路已正確設定之後，您可以啟用 hello 雲端中的虛擬機器的保護。

 請注意 hello 下列：

* 虛擬機器必須符合 Azure 需求。 這些簽入[必要條件和支援](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)hello 規劃指南中。
* tooenable 保護、 hello 作業系統以及作業系統磁碟屬性必須設定為 hello 虛擬機器。 當您在 VMM 使用虛擬機器範本中建立虛擬機器時，您可以設定 hello 屬性。 您也可以設定這些屬性的現有虛擬機器上 hello**一般**和**硬體組態**hello 虛擬機器內容 索引標籤。 如果您不需要在 VMM 中設定這些屬性，您將必須能夠 tooconfigure hello Azure Site Recovery 入口網站中。

1. tooenable 保護，執行下列命令 tooget hello 保護容器 hello:

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. 取得 hello 保護實體 (VM) 執行下列命令的 hello:

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. 執行下列命令的 hello 啟用 hello DR hello VM:

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a>測試您的部署
tootest 部署可以在執行測試容錯移轉單一的虛擬機器，或建立包含多個虛擬機器的復原計劃和執行測試容錯移轉 hello 計劃。 測試容錯移轉會在隔離的網路中模擬您的容錯移轉與復原機制。 請注意：

* 如果您想 tooconnect toohello Azure 虛擬機器中使用遠端桌面 hello 容錯移轉之後，請啟用遠端桌面連線 hello 虛擬機器上執行 hello 測試容錯移轉之前。
* 在容錯移轉之後您將使用遠端桌面在 Azure 中使用公用 IP 位址 tooconnect toohello 虛擬機器。 如果您希望 toodo 如此，請確定您沒有任何網域原則，讓您無法使用的公用位址的連接 tooa 虛擬機器。

toocheck hello 完成 hello 作業時，請依照下列中的 hello 步驟[監視活動](#monitor)。

### <a name="run-a-test-failover"></a>執行測試容錯移轉
- 執行下列命令的 hello 啟動 hello 測試容錯移轉：

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a>執行計劃性容錯移轉
- 執行下列命令的 hello 啟動 hello 計劃的容錯移轉：

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a>執行非計劃性容錯移轉
- 開始執行下列命令的 hello hello 規劃的容錯移轉：

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

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
