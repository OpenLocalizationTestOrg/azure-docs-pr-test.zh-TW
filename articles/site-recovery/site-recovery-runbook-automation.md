---
title: "aaaAdd Azure 自動化 runbook toorecovery 計劃在 Azure Site Recovery |Microsoft 文件"
description: "了解 Azure Site Recovery 如何協助您使用 Azure 自動化來擴充復原方案。 了解期間復原 tooAzure toocomplete 複雜工作的方式。"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a>新增 Azure 自動化 runbook toorecovery 計劃
在本文中，我們說明如何與 Azure 自動化 toohelp 整合 Azure Site Recovery 擴充您的復原方案。 復原方案可以協調使用 Site Recovery 保護的 VM 復原。 復原計劃適用於複寫 tooa 次要雲端，並複寫 tooAzure。 復原計劃也有助於讓 hello 復原**一致精確**， **repeatable**，和**自動化**。 如果您容錯移轉 Vm tooAzure，與 Azure 自動化的整合會擴充您的復原方案。 您可以使用 tooexecute runbook，提供功能強大的自動化工作。

如果您是新 tooAzure 自動化，您可以[註冊](https://azure.microsoft.com/services/automation/)和[下載範例指令碼](https://azure.microsoft.com/documentation/scripts/)。 如需詳細資訊，以及 toolearn 如何使用 tooorchestrate 復原 tooAzure[復原計劃](https://azure.microsoft.com/blog/?p=166264)，請參閱[Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/)。

在本文中，我們說明如何將 Azure 自動化 Runbook 整合至您的復原方案。 我們使用範例 tooautomate 基本工作先前需要手動介入。 我們也會說明如何 tooconvert multi-step 復原 tooa 單鍵復原動作。

## <a name="customize-hello-recovery-plan"></a>自訂 hello 復原計劃
1. 移 toohello **Site Recovery**復原計劃資源刀鋒視窗。 此範例中，hello 復原計劃有兩個 Vm 加入的 tooit，進行復原。 toobegin 加入 runbook，按一下 hello**自訂** 索引標籤。

    ![按一下 hello 自訂按鈕](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. 以滑鼠右鍵按一下 [群組 1: 開始]，然後選取 [新增後續動作]。

    ![以滑鼠右鍵按一下 [群組 1: 開始] 並新增後續動作](media/site-recovery-runbook-automation-new/customize-rp.png)

3. 按一下 [Choose a script] \(選擇指令碼)。

4. 在 hello**更新動作**刀鋒視窗中，名稱 hello 指令碼**Hello World**。

    ![hello 更新動作刀鋒視窗](media/site-recovery-runbook-automation-new/update-rp.png)

5. 輸入自動化帳戶名稱。
    >[!NOTE]
    > hello 自動化帳戶可以是任何 Azure 區域。 hello 自動化帳戶必須在 hello 與 hello Azure Site Recovery 保存庫相同的訂用帳戶。

6. 在您的自動化帳戶中，選取一個 Runbook。 此 runbook 是 hello 復原計劃的 hello 第一個群組的 hello 復原後 hello 執行期間執行的 hello 指令碼。

7. toosave hello 指令碼中，按一下 **確定**。 hello 指令碼會加入太**群組 1： 後續步驟**。

    ![[群組 1: 開始] 的後續動作](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a>新增指令碼的考量

* 如需選項太**刪除步驟**或**更新 hello 指令碼**，以滑鼠右鍵按一下 hello 指令碼。
* 從內部部署機器 tooAzure 指令碼可以在 Azure 上執行容錯移轉期間。 它也可以執行在 Azure 上做為關機之前, 的主要站台指令碼從 Azure tooan 在內部部署機器的容錯回復期間。
* 指令碼執行時會插入復原方案內容。 下列範例中的 hello 顯示內容變數：

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    hello 下表列出 hello 名稱和描述 hello 內容中的每個變數。

    | **變數名稱** | **說明** |
    | --- | --- |
    | RecoveryPlanName |hello 計劃要執行 hello 名稱。 此變數可協助您不同依據採取動作 hello 復原方案名稱。 您也可以重複使用 hello 指令碼。 |
    | FailoverType |指定測試是否 hello 容錯移轉、 規劃或非計劃。 |
    | FailoverDirection |指定是否復原為 tooa 主要或次要站台。 |
    | GroupID |Hello 計劃執行時，識別 hello 群組編號 hello 復原計劃中。 |
    | VmMap |Hello 群組中所有 Vm 的陣列。 |
    | VMMap 索引鍵 |每個 VM 的唯一索引鍵 (GUID)。 它的 hello 與相同 hello Azure Virtual Machine Manager (VMM) 識別碼 hello VM，在適用情況。 |
    | SubscriptionId |建立 VM 中的 hello hello Azure 訂用帳戶識別碼。 |
    | RoleName |hello hello 要復原的 Azure VM 名稱。 |
    | CloudServiceName |已建立的 hello VM hello Azure 雲端服務名稱。 |
    | resourceGroupName|已建立的 hello VM hello Azure 資源群組名稱。 |
    | RecoveryPointId|當復原 hello VM 的 hello 時間戳記。 |

* 請確定該 hello 自動化帳戶能 hello 下列模組：
    * AzureRM.profile
    * AzureRM.Resources
    * AzureRM.Automation
    * AzureRM.Network
    * AzureRM.Compute

所有模組都必須是相容版本。 所有模組都都相容輕鬆 tooensure 是所有 hello 模組 toouse hello 最新版本。

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a>存取 hello VMMap 在迴圈中的所有 Vm
使用下列程式碼 tooloop hello Microsoft VMMap 的所有 Vm 之間的 hello:

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> hello 指令碼時的動作前 tooa 開機群組 hello 資源群組名稱和角色名稱的值是空的。 只有當容錯移轉中的 hello 該群組中的 VM 成功時，會填入 hello 值。 hello 指令碼是 hello 開機群組後續動作。

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a>使用 hello 相同多個復原方案中的 Automation runbook

您可以透過外部變數，在多個復原方案中使用單一指令碼。 您可以使用[Azure 自動化變數](../automation/automation-variables.md)toostore 參數，您可以傳遞的復原計劃執行。 藉由加入 hello 復原方案名稱作為前置詞 toohello 變數，您可以建立個別的變數，針對每個復原方案。 然後，使用 hello 變數做為參數。 您可以變更參數，而不需要變更 hello 指令碼，但仍變更 hello 方式 hello 指令碼。

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a>在 Runbook 指令碼中使用簡單的字串變數

在此範例中，指令碼會使用 hello 輸入的網路安全性群組 (NSG) 並將其套用 toohello Vm 的復原計劃。

Hello 指令碼 toodetect 執行復原計劃，請使用 hello 復原計劃內容：

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

tooapply 現有 NSG，您必須知道 hello NSG 名稱和 hello NSG 資源群組名稱。 使用這些變數作為復原方案指令碼的輸入。 toodo，自動化帳戶資產 hello 中建立兩個變數。 新增 hello hello 復原方案的名稱，您要建立 hello 參數做為前置詞 toohello 變數名稱。

1. 建立變數 toostore hello NSG 名稱。 使用 hello hello 復原方案的名稱，以新增前置詞 toohello 變數名稱。

    ![建立 NSG 名稱變數](media/site-recovery-runbook-automation-new/var1.png)

2. 建立變數 toostore hello NSG 的資源群組名稱。 使用 hello hello 復原方案的名稱，以新增前置詞 toohello 變數名稱。

    ![建立 NSG 資源群組名稱](media/site-recovery-runbook-automation-new/var2.png)


3.  Hello 的指令碼中使用下列參考程式碼 tooget hello 變數值的 hello:

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  使用 hello 變數 hello runbook tooapply hello NSG toohello 網路介面中的 hello 容錯 VM:

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

對於每個復原計劃，請建立獨立變數，以便您可以重複使用 hello 指令碼。 使用 hello 復原方案名稱，以新增前置詞。 如需此案例中完整的端對端指令碼，請參閱[站台復原的復原計劃的測試容錯移轉期間新增公用 IP 與 NSG tooVMs](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee)。


### <a name="use-a-complex-variable-toostore-more-information"></a>使用複雜變數 toostore 的詳細資訊

假設您想要設定特定 Vm 上的公用 IP 上單一指令碼 tooturn。 在其他案例中，您可能想 tooapply （不在所有的 Vm) 上的不同 Vm 上不同的 Nsg。 您可以讓指令碼可重複使用於任何復原方案。 每個復原方案可以有任意數目的 VM。 例如，SharePoint 復原有兩個前端。 基本企業營運 (LOB) 應用程式只有一個前端。 您無法為每個復原方案建立個別變數。 

在下列範例的 hello，我們使用新的技術，並建立[複雜變數](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396)在 hello Azure 自動化帳戶的資產。 您可以藉由指定多個值來執行這項作業。 您必須使用 Azure PowerShell toocomplete hello 下列步驟：

1. 在 PowerShell 中，登入 tooyour Azure 訂用帳戶：

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. toostore hello 參數，會使用 hello hello 復原方案的名稱，以建立 hello 複雜變數：

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. 在此複雜變數， **VMDetails**為 hello VM 識別碼 hello 受保護 VM。 tooget hello VM 識別碼 hello Azure 入口網站中的檢視 hello VM 屬性。 hello 下列螢幕擷取畫面顯示變數以存放的兩個 Vm 的 hello 詳細資料：

    ![Hello GUID 作為 hello VM 識別碼](media/site-recovery-runbook-automation-new/vmguid.png)

4. 在您的 Runbook 中使用此變數。 如果 hello 指示 hello 復原計劃內容中找到 VM GUID，套用 hello NSG hello VM 上：

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. 在您的 runbook，迴圈 hello Vm 的 hello 復原計劃內容。 檢查 hello VM 是否存在於**$VMDetailsObj**。 如果存在的話，存取 hello 變數 tooapply hello NSG hello 屬性：

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

您可以使用相同指令碼的 hello 不同的復原計劃。 儲存對應 tooa 復原計劃在不同的變數中的 hello 值，請輸入不同的參數。

## <a name="sample-scripts"></a>範例指令碼

toodeploy 範例指令碼 tooyour 自動化帳戶中，按一下 hello**部署 tooAzure**  按鈕。

[![部署 tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

如需其他範例，請參閱下列視訊的 hello。 它會示範如何 toorecover 兩層式 WordPress 應用程式 tooAzure:


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a>其他資源
* [Azure 自動化服務執行身分帳戶](../automation/automation-sec-configure-azure-runas-account.md)
* [Azure 自動化概觀](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure 自動化概觀")
* [Azure 自動化範例指令碼](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Azure 自動化範例指令碼")
