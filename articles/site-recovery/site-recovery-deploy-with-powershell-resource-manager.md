---
title: "使用 PowerShell 和 Azure 資源管理員的 HYPER-V Vm aaaReplicate |Microsoft 文件"
description: "使用 PowerShell 和 Azure 資源管理員的 Azure Site recovery 自動化 HYPER-V Vm tooAzure hello 的複寫。"
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a>使用 PowerShell 和 Azure Resource Manager 在內部部署 Hyper-V 虛擬機器與 Azure 之間複寫
> [!div class="op_single_selector"]
> * [Azure 入口網站](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell - 資源管理員](site-recovery-deploy-with-powershell-resource-manager.md)
> * [傳統入口網站](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a>概觀
Azure Site Recovery 提供 tooyour 業務續航力和災害復原策略可藉由協調複寫、 容錯移轉，以及一些部署案例中的虛擬機器的復原。 如需部署案例的完整清單，請參閱 hello [Azure 站台復原概觀](site-recovery-overview.md)。

Azure PowerShell 是提供 cmdlet toomanage 透過 Windows PowerShell 的 Azure 模組。 它可以使用兩種類型的模組： hello Azure 設定檔模組或 hello Azure 資源管理員模組。

Azure PowerShell for Azure Resource Manager 提供的 Site Recovery PowerShell Cmdlet 可讓您在 Azure 中保護與復原伺服器。

本文說明如何 toouse Windows PowerShell，以及 Azure 資源管理員，toodeploy Site Recovery tooconfigure 以及協調伺服器保護 tooAzure。 在本文中使用的 hello 範例將示範如何 tooprotect，容錯移轉和復原虛擬機器上的 HYPER-V 主機 tooAzure，使用 Azure PowerShell 的 Azure 資源管理員。

> [!NOTE]
> hello 站台復原 PowerShell cmdlet 目前可讓您遵循 tooconfigure hello： 一個 Virtual Machine Manager 的站台 tooanother、 Virtual Machine Manager 網站 tooAzure 及 HYPER-V 站台 tooAzure。
>
>

您不需要 toobe PowerShell 專家 toouse 本文中，但您需要 toounderstand hello 基本概念，例如模組、 cmdlet 和工作階段。 如需 Windows PowerShell 的詳細資訊，請參閱 [開始使用 Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx)(英文)。

您也可以參閱 [搭配使用 Azure PowerShell 與 Azure Resource Manager](../powershell-azure-resource-manager.md)。

> [!NOTE]
> 屬於 hello 雲端方案提供者 (CSP) 程式的 Microsoft 合作夥伴可以設定及管理其客戶的伺服器的保護個別 CSP 訂閱 tootheir 客戶 （租用戶訂閱）。
>
>

## <a name="before-you-start"></a>開始之前
確認您已備妥這些必要條件：

* [Microsoft Azure](https://azure.microsoft.com/) 帳戶。 您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。 此外，您可以參閱 [Azure Site Recovery 管理員價格](https://azure.microsoft.com/pricing/details/site-recovery/)。
* Azure PowerShell 1.0。 如需有關此版本資訊和如何 tooinstall，請參閱[Azure PowerShell 1.0。](https://azure.microsoft.com/)
* hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/)和[AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/)模組。 您可以從 hello 取得 hello 最新版本，這些模組[PowerShell 資源庫](https://www.powershellgallery.com/)

本文將說明如何使用 Azure Resource Manager tooconfigure toouse Azure Powershell 及管理您伺服器的保護。 在本文中使用的 hello 範例將示範如何為虛擬機器，主機上執行 HYPER-V，tooAzure tooprotect。 hello 下列必要條件是特定 toothis 範例。 一組更完整的需求的 hello 各種站台復原案例，請參閱相關 toothat 案例 toohello 文件。

* 執行 Windows Server 2012 R2 或 Microsoft Hyper-V Server 2012 R2 且包含一或多部虛擬機器的 Hyper-V 主機。
* HYPER-V 伺服器連接網際網路，toohello 直接或透過 proxy。
* hello 想 tooprotect 的虛擬機器都應該符合[虛擬機器必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。

## <a name="step-1-sign-in-tooyour-azure-account"></a>步驟 1： 登入 tooyour Azure 帳戶
1. 開啟 PowerShell 主控台並執行此命令 toosign tooyour Azure 帳戶中。 hello cmdlet 就會開啟一個網頁，會提示您輸入您的帳戶認證。

        Login-AzureRmAccount

    或者，加入您的帳戶認證為參數 toohello `Login-AzureRmAccount` cmdlet，利用 hello`-Credential`參數。

    如果您是使用代表租用戶的 CSP 夥伴時，指定為租用戶，hello 客戶使用其 tenantID 或租用戶的主要網域名稱。

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. 帳戶可以有數個訂閱，所以您應該將您想要與 hello 帳戶 toouse hello 訂用帳戶產生關聯。

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. 請確認您的訂用帳戶註冊的 toouse 復原服務與站台復原 hello Azure 提供者，使用下列命令的 hello:

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   Hello 輸出中的這些命令，如果 hello **RegistrationState**設定得**註冊**，您可以繼續 tooStep 2。 如果沒有，您應該註冊您的訂用帳戶中的 hello 遺漏提供者。

   tooregister hello Azure 提供者站台復原和復原服務，請執行下列命令的 hello:

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   請確認 hello 提供者已成功註冊使用下列命令的 hello:`Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`和`Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`。

## <a name="step-2-set-up-hello-recovery-services-vault"></a>步驟 2： 設定復原服務保存庫的 hello
1. 建立 Azure 資源管理員資源群組中，您將建立 hello 保存庫，或使用現有的資源群組。 您可以使用下列命令的 hello，以建立新的資源群組：

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    hello $ResourceGroupName 變數包含 hello hello 資源群組名稱在您想 toocreate，而且 hello $Geo 變數包含 hello Azure 區域中哪一個 toocreate hello 資源群組 （例如，"巴西南部 」）。

    您也可以使用 hello 您訂用帳戶中取得一份資源群組`Get-AzureRmResourceGroup`cmdlet。
2. 建立新的 Azure 復原服務保存庫，如下所示：

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    您可以擷取一份現有保存庫使用 hello `Get-AzureRmRecoveryServicesVault` cmdlet。

> [!NOTE]
> 如果您想使用 hello 傳統入口網站或 hello Azure Service Management PowerShell 模組所建立的站台復原保存庫 tooperform 作業時，您可以擷取一份這類保存庫使用 hello `Get-AzureRmSiteRecoveryVault` cmdlet。 您應該為所有的新作業建立新的復原服務保存庫。 您稍早建立的 hello Site Recovery 保存庫支援，但是沒有 hello 最新的功能。
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a>步驟 3： 設定 hello 復原服務保存庫內容
1. 執行下列命令的 hello 設定 hello 保存庫的內容：

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a>步驟 4： 建立 HYPER-V 站台，並產生新的保存庫註冊金鑰 hello 站台。
1. 建立新的 Hyper-V 站台，如下所示：

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    此 cmdlet 會啟動站台復原作業 toocreate hello 站台，並傳回站台復原工作物件。 等候 hello 作業 toocomplete，並確認該 hello 工作順利完成。

    您可以擷取 hello 工作物件，並藉此使用 hello Get AzureRmSiteRecoveryJob cmdlet 檢查 hello hello 作業目前狀態。
2. 產生並下載註冊金鑰 hello 網站，如下所示：

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    複製 hello 下載金鑰 toohello HYPER-V 主機。 您需要 hello 金鑰 tooregister hello HYPER-V 主機 toohello 站台。

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a>步驟 5: Hello Azure Site Recovery provider 和 Azure Recovery Services Agent 安裝在 HYPER-V 主機上
1. 下載 hello hello hello 提供者，從最新版本的安裝程式[Microsoft](https://aka.ms/downloaddra)。
2. Hello 執行安裝程式在 HYPER-V 主機上，並在 hello hello 安裝結尾繼續 toohello 註冊的步驟。
3. 出現提示時，提供 hello 下載站台的註冊金鑰，並完成註冊的 hello HYPER-V 主機 toohello 站台。
4. 確認該 hello HYPER-V 主機已註冊的 toohello 站台使用下列命令的 hello:

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a>步驟 6： 建立複寫原則，並將它與 hello 保護容器關聯
1. 建立複寫原則，如下所示︰

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    傳回 hello 複寫原則建立成功的作業 tooensure 核取 hello。

   > [!IMPORTANT]
   > hello 指定儲存體帳戶應在 hello 與您的復原服務保存庫相同的 Azure 區域，而且應啟用地理複寫。
   >
   > * 如果 hello 指定儲存體帳戶屬於型別 Azure 儲存體 （傳統） 的復原，容錯移轉的 hello 受保護機器復原 hello 機器 tooAzure IaaS （傳統）。
   > * 如果 hello 指定復原儲存體帳戶屬於 Azure 儲存體 (Azure Resource Manager) 的型別，hello 的容錯移轉受保護機器復原 hello 機器 tooAzure IaaS (Azure Resource Manager)。
   >
   >
2. 取得 hello 保護容器對應 toohello 站台，如下所示：

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. 開始 hello 關聯 hello 保護容器 hello 複寫原則，如下所示：

     $Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer

   等候 hello 關聯作業 toocomplete，並請確定已成功完成。

## <a name="step-7-enable-protection-for-virtual-machines"></a>步驟 7：對虛擬機器啟用保護
1. 收到 hello 保護實體對應 toohello VM 想 tooprotect，，如下所示：

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. 開始保護 hello 虛擬機器，如下所示：

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > hello 指定儲存體帳戶應在 hello 與您的復原服務保存庫相同的 Azure 區域，而且應啟用地理複寫。
   >
   > * 如果 hello 指定儲存體帳戶屬於型別 Azure 儲存體 （傳統） 的復原，容錯移轉的 hello 受保護機器復原 hello 機器 tooAzure IaaS （傳統）。
   > * 如果 hello 指定復原儲存體帳戶屬於 Azure 儲存體 (Azure Resource Manager) 的型別，hello 的容錯移轉受保護機器復原 hello 機器 tooAzure IaaS (Azure Resource Manager)。
   >
   > 如果您要保護的 VM hello 有多個磁碟附加的 tooit，使用 hello 指定 hello 作業系統磁碟*OSDiskName*參數。
   >
   >
3. 等候 hello 虛擬機器 tooreach 受保護的狀態 hello 初始複寫之後。 這可以使用一段時間，取決於複寫資料 toobe hello 量等因素，並 hello tooAzure 上游的可用頻寬。 hello 工作狀態和 StateDescription，則會在 hello VM 達到受保護的狀態時，如下所示，更新。

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. 更新修復屬性，例如 hello VM 角色大小和 hello Azure 網路 tooattach hello 虛擬機器的網路介面卡 tooupon 容錯移轉。

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update hello virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a>步驟 8：執行測試容錯移轉
1. 執行測試容錯移轉作業，如下所示：

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. 請確認 VM 在 Azure 中建立該 hello 測試。 （hello 測試容錯移轉作業已暫停之後在 Azure 中建立 hello 測試 VM。 hello 作業的完成作業清除已完成時繼續 hello 工作建立 hello artefacts hello 下一個步驟中所示。）
3. 完成 hello 測試容錯移轉的如下所示：

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a>後續步驟
[閱讀更多](https://msdn.microsoft.com/library/azure/mt637930.aspx) 使用 Azure Resource Manager PowerShell Cmdlet 進行 Azure Site Recovery 的相關資訊。
