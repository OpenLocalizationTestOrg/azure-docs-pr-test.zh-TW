---
title: "aaaReplicate hello 傳統入口網站中使用 PowerShell 的 HYPER-V Vm tooAzure |Microsoft 文件"
description: "自動化 hello hello 傳統入口網站中使用站台復原和 PowerShell 的 VMM 雲端中 HYPER-V 虛擬機器的複寫"
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: tysonn
ms.assetid: 9011f567-e0b4-4306-951a-b30da19f5db6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: d6847b46ac227209e6890de4ab603b23f827360f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-tooazure-with-powershell-in-hello-classic-portal"></a>使用 PowerShell 的 HYPER-V Vm tooAzure hello 傳統入口網站中的複寫
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

hello 文章包含 hello 案例中，並顯示您如何註冊 Site Recovery 保存庫 tooset 安裝 hello hello 來源 VMM 伺服器上的 Azure Site Recovery Provider 的必要條件、 hello 保存庫中註冊伺服器 hello、 新增 Azure 儲存體帳戶、 安裝 hello Azure復原服務代理程式在 HYPER-V 主機伺服器，設定會套用的 tooall 受保護的虛擬機器，並再啟用保護這些虛擬機器的 VMM 雲端的保護設定。 完成的測試 hello 容錯移轉 toomake 確定一切如預期般運作。

如果您遇到此案例中所設定的問題時，請張貼您的問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

> [!NOTE]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。
>
>

## <a name="before-you-start"></a>開始之前
確認您已備妥這些必要條件：

### <a name="azure-prerequisites"></a>Azure 必要條件
* 您將需要 [Microsoft Azure](https://azure.microsoft.com/) 帳戶。 您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。
* 您將需要 Azure 儲存體帳戶 toostore 複寫資料。 hello 帳戶必須啟用異地複寫。 它應該會在 hello 與 hello Azure Site Recovery 保存庫相同的區域，並且與相關聯 hello 相同訂用帳戶。 [深入了解 Azure 儲存體](../storage/common/storage-introduction.md)。
* 您必須確定您想 tooprotect 虛擬機器符合 toomake [Azure 虛擬機器必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。

### <a name="vmm-prerequisites"></a>VMM 必要條件
* 您將需要在 System Center 2012 R2 上執行的 VMM 伺服器。
* 您必須在 hello 想 tooprotect VMM 伺服器上的至少一個雲端。 hello 雲端應包含：
  * 一或多個 VMM 主機群組。
  * 每個主機群組中的一或多個 Hyper-V 主機伺服器或叢集。
  * 一或多個虛擬機器 hello 來源 HYPER-V 伺服器上。

### <a name="hyper-v-prerequisites"></a>Hyper-V 的必要條件
* hello HYPER-V 主機伺服器必須執行至少**Windows Server 2012**與 HYPER-V 角色或**Microsoft HYPER-V Server 2012**和擁有 hello 安裝最新的更新。
* 如果您在叢集中執行 Hyper-V，請注意，如果您具有靜態 IP 位址叢集，並不會自動建立叢集代理。 您以手動方式將需要 tooconfigure hello 叢集代理人。 toodo 這在 伺服器管理員 > 連接 toohello 叢集容錯移轉叢集管理員 中，按一下**設定角色**選取**HYPER-V 複本代理人**在 hello**選取角色**hello 高可用性精靈 的螢幕。
* 必須包含任何 HYPER-V 主機伺服器或叢集，您會想 toomanage 保護 VMM 雲端中。

### <a name="network-mapping-prerequisites"></a>網路對應的必要條件
當您保護 Azure 網路對應中的虛擬機器 hello 來源 VMM 伺服器上的 VM 網路和目標 Azure 網路 tooenable hello 下列之間進行對應：

* 容錯移轉 hello 相同的所有機器網路可以連接 tooeach 其他，無論它們是在復原計劃。
* 如果網路閘道 hello 目標 Azure 網路上的安裝程式，虛擬機器可以連接 tooother 在內部部署虛擬機器。
* 如果您未設定網路對應，只有容錯移轉 hello 中相同的虛擬機器容錯移轉 tooAzure 後，即可能 tooconnect tooeach 其他復原方案。

如果您想 toodeploy 網路對應，您將需要下列 hello:

* hello 想 tooprotect hello 來源 VMM 伺服器上的虛擬機器應連接的 tooa VM 網路。 該網路應連結的 tooa hello 雲端相關聯的邏輯網路。
* Azure 網路 toowhich 複寫虛擬機器可以容錯移轉之後連接。 在 hello 容錯移轉期間，會選取此網路。 hello 網路應位於 hello 與 Azure Site Recovery 訂用帳戶相同的區域。

### <a name="powershell-prerequisites"></a>PowerShell 必要條件
請確定您具有 Azure PowerShell 準備 toogo。 如果您已經使用 PowerShell，您將需要 tooupgrade tooversion 0.8.10 或更新版本。 PowerShell 設定的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。 一旦您已安裝並設定 PowerShell，您可以檢視所有 hello 可用的 hello 服務 cmdlet[這裡](/powershell/azure/overview)。

toolearn 的相關技巧，可協助您使用 hello cmdlet，例如如何參數值、 輸入和輸出通常處理 Azure PowerShell，請參閱[開始使用 Azure Cmdlet](/powershell/azure/get-started-azureps)。

## <a name="step-1-set-hello-subscription"></a>步驟 1： 設定 hello 訂用帳戶
在 PowerShell 中，執行這些 Cmdlet：

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

Hello hello"< > 」 中的項目取代為您的專屬資訊。

## <a name="step-2-create-a-site-recovery-vault"></a>步驟 2：建立 Site Recovery 保存庫
在 PowerShell 中，您的專屬資訊，以取代 hello hello"< > 」 中的項目，並執行下列命令：

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a>步驟 3：產生保存庫註冊金鑰
Hello 保存庫中產生註冊金鑰。 您下載 hello Azure Site Recovery Provider，並將它安裝在 hello VMM 伺服器之後，您將使用此索引鍵 tooregister hello VMM 伺服器 hello 保存庫中。

1. 取得 hello 保存庫設定檔，並設定 hello 內容：

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. 執行下列命令的 hello 設定 hello 保存庫的內容：

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>步驟 4： 安裝 hello Azure Site Recovery Provider
1. Hello VMM 在電腦上，執行下列命令的 hello 建立目錄：

   ```

   pushd C:\ASR\

   ```
2. 擷取使用 hello 下載提供者藉由執行下列命令的 hello hello 檔案

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. 安裝 hello 提供者使用 hello 下列命令：

   ```

   .\SetupDr.exe /i

   ```

   ```

   $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
   do
   {
     $isNotInstalled = $true;
     if(Test-Path $installationRegPath)
     {
         $isNotInstalled = $false;
     }
   }While($isNotInstalled)

   ```

   等候 hello 安裝 toofinish。
4. 使用下列命令的 hello hello 保存庫中註冊伺服器 hello:

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a>步驟 5：建立 Azure 儲存體帳戶
如果您沒有 Azure 儲存體帳戶，請執行下列命令的 hello 建立啟用地理複寫帳戶：

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

請注意，hello 儲存體帳戶必須在 hello 與 hello Azure Site Recovery 服務相同的區域和與其相關聯 hello 相同訂用帳戶。

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>步驟 6： 安裝 Azure Recovery Services Agent hello
Hello Azure 入口網站位於 hello VMM 雲端中每部 HYPER-V 主機伺服器上安裝 hello Azure 復原服務代理程式從您想 tooprotect。

執行下列命令，在所有 VMM 主機上的 hello:

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a>步驟 7：設定雲端保護設定
1. 建立雲端保護設定檔 tooAzure 藉由執行下列命令的 hello:

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. 藉由執行下列命令的 hello 取得保護容器：

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. 開始 hello 雲端中的 hello hello 保護容器的關聯：

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. Hello 工作已完成之後，執行下列命令的 hello:

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. Hello 作業已完成處理之後，執行下列命令的 hello:

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



toocheck hello 完成 hello 作業時，請依照下列中的 hello 步驟[監視活動](#monitor)。

## <a name="step-8-configure-network-mapping"></a>步驟 8：設定網路對應
開始之前請確認網路對應 hello 來源 VMM 伺服器上的虛擬機器會連接的 tooa VM 網路。 此外，請建立一或多個 Azure 虛擬網路。 請注意，多個 VM 網路可以是對應的 tooa 單一 Azure 網路。

附註是否 hello 目標網路有多個子網路，而且其中一個子網路具有 hello 是相同的 hello 來源虛擬機器上的子網路的名稱，則 hello 複本虛擬機器將會連接的 toothat 目標子網路容錯移轉之後。 如果沒有具有相符名稱的目標子網路，hello 虛擬機器將會連接的 toohello hello 網路中的第一個子網路。

hello 第一個命令會取得 hello 目前 Azure Site Recovery 保存庫中的伺服器。 hello 命令儲存 hello Microsoft Azure Site Recovery 伺服器 hello $Servers 陣列變數中。

    $Servers = Get-AzureSiteRecoveryServer


hello 第二個命令會取得 hello hello 第一部伺服器的站台復原網路 hello $Servers 陣列中。 hello 命令儲存 hello 網路 hello $Networks 變數中。

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

hello 第三個命令會取得您的 Azure 訂用帳戶使用 hello Get-azuresubscription cmdlet，然後將該值儲存 hello $Subscriptions 變數。

    $Subscriptions = Get-AzureSubscription



hello 第四個命令會取得 Azure 虛擬網路使用 hello Get AzureVNetSite cmdlet，然後該值 hello $AzureVmNetworks 變數中。

    $AzureVmNetworks = Get-AzureVNetSite



hello 最終 cmdlet 會建立 hello 主要網路與 hello Azure 虛擬機器網路之間的對應。 hello 指令程式會指定 hello 主要網路作為 $Networks hello 第一個項目。 hello cmdlet 指定 $AzureVmNetworks hello 第一個項目為虛擬機器網路，使用其識別碼。 hello 命令包含您的 Azure 訂用帳戶 id。

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a>步驟 9：對虛擬機器啟用保護
伺服器、 雲端和網路已正確設定之後，您可以啟用 hello 雲端中的虛擬機器的保護。 請注意 hello 下列：

虛擬機器必須符合 [Azure 虛擬機器必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。

tooenable 保護 hello 作業系統和作業系統磁碟屬性必須設定為 hello 虛擬機器。 當您在 VMM 使用虛擬機器範本中建立虛擬機器時，您可以設定 hello 屬性。 您也可以設定這些屬性的現有虛擬機器上 hello**一般**和**硬體組態**hello 虛擬機器內容 索引標籤。 如果您不需要在 VMM 中設定這些屬性，您將必須能夠 tooconfigure hello Azure Site Recovery 入口網站中。

1. tooenable 保護，執行下列命令 tooget hello 保護容器 hello:

     $ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName
2. 取得 hello 保護實體 (VM) 執行下列命令的 hello:

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. 執行下列命令的 hello 啟用 hello DR hello VM:

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a>測試您的部署
tootest 規劃您的部署，您可以執行測試容錯移轉的單一虛擬機器，或建立復原方案包含多個虛擬機器並執行測試容錯移轉的 hello。 測試容錯移轉會在隔離的網路中模擬您的容錯移轉與復原機制。 請注意：

* 如果您想 tooconnect toohello Azure 虛擬機器中使用遠端桌面 hello 容錯移轉之後，請啟用遠端桌面連線 hello 虛擬機器上執行 hello 測試容錯移轉之前。
* 容錯移轉之後，您將使用遠端桌面在 Azure 中使用公用 IP 位址 tooconnect toohello 虛擬機器。 如果您希望 toodo 如此，請確定您沒有任何網域原則，讓您無法使用的公用位址的連接 tooa 虛擬機器。

toocheck hello 完成 hello 作業時，請依照下列中的 hello 步驟[監視活動](#monitor)。

### <a name="create-a-recovery-plan"></a>建立復原計畫
1. 做為範本使用 hello 資料，復原方案中建立的.xml 檔，然後將它儲存為"C:\RPTemplatePath.xml"。
2. Hello RecoveryPlan 節點識別碼、 名稱、 PrimaryServerId 和 SecondaryServerId 變更。
3. Hello ProtectionEntity 節點 PrimaryProtectionEntityId （vmid，可從 VMM） 的變更。
4. 您可以新增更多 ProtectionEntity 節點來新增更多 VM。

        <#
        <?xml version="1.0" encoding="utf-16"?>
        <RecoveryPlan Id="d0323b26-5be2-471b-addc-0a8742796610" Name="rp-test"     PrimaryServerId="9350a530-d5af-435b-9f2b-b941b5d9fcd5"     SecondaryServerId="21a9403c-6ec1-44f2-b744-b4e50b792387" Description=""     Version="V2014_07">
          <Actions />
          <ActionGroups>
            <ShutdownAllActionGroup Id="ShutdownAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </ShutdownAllActionGroup>
            <FailoverAllActionGroup Id="FailoverAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </FailoverAllActionGroup>
            <BootActionGroup Id="DefaultActionGroup">
              <PreActionSequence />
              <PostActionSequence />
              <ProtectionEntity PrimaryProtectionEntityId="d4c8ce92-a613-4c63-9b03-    cf163cc36ef8" />
            </BootActionGroup>
          </ActionGroups>
          <ActionGroupSequence>
            <ActionGroup Id="ShutdownAllActionGroup" ActionId="ShutdownAllActionGroup"     Before="FailoverAllActionGroup" />
            <ActionGroup Id="FailoverAllActionGroup" ActionId="FailoverAllActionGroup"     After="ShutdownAllActionGroup" Before="DefaultActionGroup" />
            <ActionGroup Id="DefaultActionGroup" ActionId="DefaultActionGroup" After="FailoverAllActionGroup"/>
          </ActionGroupSequence>
        </RecoveryPlan>
        #>



1. 填入 hello hello 範本中的資料：

        $TemplatePath = "C:\RPTemplatePath.xml";



1. 建立 hello RecoveryPlan:

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a>執行測試容錯移轉
1. 藉由執行下列命令的 hello 收到 hello RecoveryPlan 物件：

     $RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;
2. 執行下列命令的 hello 啟動 hello 測試容錯移轉：

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


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
[閱讀更多](/powershell/azure/overview) Azure Site Recovery PowerShell Cmdlet 的相關資訊。 </a>。
