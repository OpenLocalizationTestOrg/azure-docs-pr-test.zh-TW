---
title: "aaaAdd Azure 自動化 runbook toorecovery 計劃在 hello 傳統入口網站 |Microsoft 文件"
description: "本文說明如何 Azure Site Recovery 現在可讓您使用 Azure 自動化 toocomplete 複雜的工作期間復原 tooAzure tooextend 復原計劃"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a>在 hello 傳統入口網站中加入 Azure 自動化 runbook toorecovery 計劃
本教學課程說明如何與 Azure 自動化 tooprovide 擴充性 toorecovery 計劃整合 Azure Site Recovery。 復原計劃，便可調整的虛擬機器複寫 toosecondary 雲端和複寫 tooAzure 案例使用 Azure Site Recovery 保護的復原。 它們也可以協助進行 hello 復原**一致精確**， **repeatable**，和**自動化**。 如果您容錯移轉虛擬機器 tooAzure，整合 Azure 自動化與擴充的復原計劃，並提供功能 tooexecute runbook，如此可讓功能強大的自動化工作。

如果您還沒聽過「Azure 自動化」，請在[這裡](https://azure.microsoft.com/services/automation/)註冊，然後從[這裡](https://azure.microsoft.com/documentation/scripts/)下載其範例指令碼。 深入了解[Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/)和 tooorchestrate 復原 tooAzure 使用復原的計劃[這裡](https://azure.microsoft.com/blog/?p=166264)。

在本簡短教學課程中，我們將會探討如何將 Azure 自動化 Runbook 整合到復原計畫。 我們將自動化先前需要手動介入的簡單工作，請參閱如何 tooconvert 多逐步執行單鍵復原動作的復原。 我們也將探討簡單的指令碼發生錯誤時如何進行疑難排解。

## <a name="protect-hello-application-tooazure"></a>保護 hello 應用程式 tooAzure
讓我們從兩部虛擬機器所組成的簡單應用程式開始。 在這裡，我們有 Fabrikam 的 HRweb 應用程式。 Fabrikam-HRweb-前端和後 Hrweb Fabrikam 端是 hello 兩部虛擬機器保護 tooAzure 使用 Azure Site Recovery。 tooprotect hello 虛擬機器使用 Azure Site Recovery，請遵循下列 hello 步驟。

1. 對虛擬機器啟用保護。
2. 請 hello 虛擬機器已完成初始複寫，且會複寫。
3. 等候直到 hello 初始複寫完成，並 hello 複寫狀態會顯示受保護。

## ![](media/site-recovery-runbook-automation/01.png)
在本教學課程中，我們將建立 Fabrikam HRweb 應用程式 toofailover hello 應用程式 tooAzure hello 的復原計劃。 然後我們會將它整合與 runbook 會在容錯移轉連接埠 80 的 Azure 虛擬機器 tooserve web 網頁的 hello 上建立端點。

首先，讓我們為應用程式建立一個復原計畫。

## <a name="create-hello-recovery-plan"></a>建立 hello 復原計劃
toorecover hello 應用程式 tooAzure，您需要 toocreate 復原計劃。
使用 復原方案，您可以指定復原的虛擬機器的 hello 順序。 hello 放置在群組 1 中的虛擬機器會復原並啟動第一個，並會遵照 hello 群組 2 中的虛擬機器。

建立一個如下的復原計畫。

![](media/site-recovery-runbook-automation/12.png)

深入了解復原計劃，請閱讀文件 tooread[這裡](https://msdn.microsoft.com/library/azure/dn788799.aspx "這裡")。

接下來，讓我們來建立必要的成品 hello Azure 自動化中。

## <a name="create-hello-automation-account-and-its-assets"></a>建立 hello 自動化帳戶和其資產
您需要 Azure 自動化帳戶 toocreate runbook。 如果您沒有帳戶，請瀏覽 tooAzure 自動化索引標籤，以表示![](media/site-recovery-runbook-automation/02.png)並建立新的帳戶。

1. 授與 hello 帳戶與名稱 tooidentify。
2. 指定要讓 tooplace hello 帳戶的地理區域。

建議您在 hello tooplace hello 帳戶與 hello ASR 保存庫相同的區域。

![](media/site-recovery-runbook-automation/03.png)

接下來，建立 hello 遵循 hello 帳戶中的資產。

### <a name="add-a-subscription-name-as-asset"></a>將訂用帳戶名稱新增為資產
1. 加入新的設定![](media/site-recovery-runbook-automation/04.png)在 hello Azure 自動化資產，並選取 太![](media/site-recovery-runbook-automation/05.png)
2. 選取 hello 變數類型為**字串**
3. 將變數名稱指定為 **AzureSubscriptionName**

   ![](media/site-recovery-runbook-automation/06.png)
4. 您實際的 Azure 訂用帳戶名稱指定為 hello 變數值。

   ![](media/site-recovery-runbook-automation/07_1.png)

您可以識別您的訂用帳戶，從您的帳戶在 hello Azure 入口網站上的 hello 設定頁面 hello 名稱。

### <a name="add-an-azure-login-credential-as-asset"></a>將 Azure 登入認證新增為資產
Azure 自動化會使用 Azure PowerShell tooconnect toothe 訂用帳戶，並那里 hello 成品上運作。 因此，您必須使用您的 Microsoft 帳戶或工作或學校帳戶進行驗證。
您可以安全地使用 hello runbook 資產 toobe 儲存 hello 帳戶認證。

1. 加入新的設定![](media/site-recovery-runbook-automation/04.png)在 hello Azure 自動化資產，並選取![](media/site-recovery-runbook-automation/09.png)
2. 選取 hello 認證類型為**Windows PowerShell 認證**
3. Hello 名稱指定為**AzureCredential**

   ![](media/site-recovery-runbook-automation/10.png)
4. 指定 hello 使用者名稱和 toosign 入與密碼。

現在，這兩個設定都可以在您的資產中使用。

![](media/site-recovery-runbook-automation/11.png)

如何指定透過 PowerShell tooconnect tooyour 訂用帳戶的詳細資訊[這裡](/powershell/azure/overview)。

接下來，您將可以新增 hello 前端的虛擬機器的端點容錯移轉後的 Azure 自動化中建立 runbook。

## <a name="azure-automation-context"></a>Azure 自動化內容
ASR 將傳遞內容變數 toohello runbook toohelp 您撰寫具有決定性的指令碼。 其中一個可以說 hello 雲端服務和虛擬機器 hello hello 名稱，可預測，但是發生，它不一定與 toocertain 案例，例如其中一個位置 hello 虛擬機器名稱 hello 名稱可能已變更到期 hello hello 案例在 Azure 中的 toounsupported 字元。 因此這項資訊會傳遞 toohello ASR 復原方案一部分 hello*內容*。

以下是範例的 hello 內容變數的外觀。

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


hello 表包含 hello 內容中的每個變數的名稱和描述。

| **變數名稱** | **說明** |
| --- | --- |
| RecoveryPlanName |正在執行的計劃名稱。 可協助您根據採取動作名稱使用 hello 相同指令碼 |
| FailoverType |指定是否 hello 容錯移轉是測試、 已規劃或非計劃。 |
| FailoverDirection |指定復原 tooprimary 或次要資料庫 |
| GroupID |Hello 計劃執行時，找出 hello hello 復原計劃中的群組編號 |
| VmMap |Hello 群組中的所有 hello 虛擬機器的陣列 |
| VMMap 索引鍵 |每個 VM 的唯一索引鍵 (GUID)。 具有 hello 與適用的 hello VMM hello 虛擬機器識別碼相同。 |
| RoleName |Hello 要復原的 Azure VM 的名稱 |
| CloudServiceName |哪些 hello 下建立虛擬機器的 azure 雲端服務名稱。 |

您也可以移至 ASR toohello VM 屬性頁面，並查看 hello VM GUID 屬性的 hello 內容中 tooidentify hello VmMap 索引鍵。

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a>撰寫自動化 Runbook
現在 hello 前端的虛擬機器上建立 hello runbook tooopen 連接埠 80。

1. 在 hello hello 名稱 Azure 自動化帳戶中建立新的 runbook **OpenPort80**

   ![](media/site-recovery-runbook-automation/14.png)
2. 瀏覽 toohello hello runbook 作者檢視，然後輸入 hello 草稿模式。
3. 先指定 hello 變數 toouse hello 復原計劃內容

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. 接下來連接 toohello 訂用帳戶使用 hello 認證和訂用帳戶名稱

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   請注意，您會使用 hello Azure 資產 – **AzureCredential**和**AzureSubscriptionName**這裡。
5. 現在指定 hello 端點詳細資料，然後 hello hello 想 tooexpose hello 端點的虛擬機器的 GUID。 在此案例的 hello 前端虛擬機器。

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   這會指定 hello Azure 端點通訊協定、 hello VM 上的本機連接埠和其對應的公用連接埠。 這些變數是參數的所需的 hello Azure 加入端點 tooVMs 的命令。 hello VMGUID 保存 hello hello 需要 toooperate 的虛擬機器的 GUID。
6. hello 指令碼現在會擷取指定的 VM GUID hello hello 內容，並被它參考的 hello 虛擬機器上建立端點。

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. 一旦完成，叫用發佈![](media/site-recovery-runbook-automation/20.png)tooallow 您指令碼 toobe 可供執行。

下面提供 hello 完整的指令碼供您參考

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a>加入 hello 指令碼 toohello 復原計劃
Hello 指令碼準備就緒之後，您可以將它加入 toohello 您稍早建立的復原方案。

1. 在您建立 hello 復原計劃，群組 2 之後指令碼選擇 tooadd。 ![](media/site-recovery-runbook-automation/15.png)
2. 指定指令碼名稱。 這是只顯示 hello 復原計劃中的此指令碼的好記名稱。
3. 在 hello 容錯移轉 tooAzure 指令碼 – 選取 hello Azure 自動化帳戶名稱。
4. 在 hello Azure Runbook，選取您所撰寫的 hello runbook。

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a>主要端指令碼
當您執行容錯移轉 tooAzure 時，您也可以選擇 tooexecute 主要端指令碼。 這些指令碼會在容錯移轉期間 hello VMM 伺服器上執行。
主要端指令碼僅適用於關機前及關機後階段。 這是因為我們希望在 hello 主要站台 toobe 通常無法使用時所發生的災害事件。
期間發生未規劃的容錯移轉，只有當您選擇的主要站台作業，它會嘗試 toorun hello 主要端指令碼。 如果它們不是可連線，或逾時，將會繼續 hello 容錯移轉 toorecover hello 虛擬機器。
未使用的 VMware/實體/hyper-v 站台不受保護的 VMM tooAzure-時容錯移轉 tooAzure 主要端指令碼。
不過，當您回復從 Azure tooon 內部部署主要端指令碼 (Runbook) 可以用於 VMware 以外的所有目標。

## <a name="test-hello-recovery-plan"></a>測試 hello 復原計劃
一旦您加入 hello runbook toohello 計劃，您可以起始測試容錯移轉和觀看實作示範。 它一定會是建議的測試容錯移轉 tootest toorun 您應用程式和 hello 復原計劃 tooensure 沒有任何錯誤。

1. 選取 hello 復原計劃，並起始測試容錯移轉。
2. Hello 計劃在執行期間，您可以查看是否 hello runbook 已執行或不是透過其狀態。

   ![](media/site-recovery-runbook-automation/17.png)
3. 您也可以查看 hello 詳細 hello runbook hello Azure 自動化作業 頁面上的 runbook 執行狀態。

   ![](media/site-recovery-runbook-automation/18.png)
4. Hello 容錯移轉完成時，除了 hello runbook 執行結果之後, 您可以查看 hello 執行是否成功或不是前往 hello Azure 的虛擬機器 頁面上，查看 hello 端點。

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a>範例指令碼
雖然我們逐步進行作業自動化一個通常用在本教學課程中新增端點 tooan Azure 虛擬機器的工作，您可以執行其他使用 Azure 自動化的強大的自動化工作的數目。 Microsoft 與 hello Azure 自動化社群提供範例 runbook 可協助您開始建立您自己的方案和公用程式 runbook，您可以使用較大的自動化工作做為建置組塊。 開始使用它們從 hello 組件庫，並建置應用程式使用 Azure Site Recovery 強大的一種單鍵復原計劃。

## <a name="additional-resources"></a>其他資源
[Azure 自動化概觀](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure 自動化概觀")

[Azure 自動化範例指令碼](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Azure 自動化範例指令碼")
