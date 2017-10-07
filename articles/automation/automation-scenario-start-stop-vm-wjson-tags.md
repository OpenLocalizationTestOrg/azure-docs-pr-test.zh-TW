---
title: "aaaUse JSON 格式的標記 tooschedule Azure VM 狀態 |Microsoft 文件"
description: "本文示範如何 toouse JSON 字串上標記 tooautomate hello 排程 VM 啟動及關機。"
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6afed5d2-e939-4749-8b2c-9312b4c16fb2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;paulomarquesc
ms.openlocfilehash: f6bbf1dea1c193e5d1010f12f3b1ed63562f9daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a>Azure 自動化案例： 使用 JSON 格式標記 toocreate Azure VM 的啟動和關閉的排程
客戶通常希望 tooschedule hello 啟動和關機的虛擬機器 toohelp 減少訂用成本或支援商務和技術需求。

hello 下列案例可讓您自動的啟動和關機的 Vm tooset 使用稱為排程在資源群組層級或在 Azure 中的虛擬機器層級的標記。 此排程可以設定從星期日 tooSaturday 的啟動時間和關機時間。

我們的確有一些現成可用的選項。 其中包含：

* [虛擬機器擴展集](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)tooscale in 或 out 可讓您的自動調整設定。
* [DevTest Labs](../devtest-lab/devtest-lab-overview.md)服務，其具有 hello 排程啟動及關閉作業的內建的功能。

不過，這些選項只支援特定案例並不能套用的 tooinfrastructure 做為服務 (IaaS) Vm。

套用的 tooa 資源群組 hello 排程標記時，也會套用的 tooall 該資源群組內的虛擬機器。 如果排程也是直接套用的 tooa VM，hello 最後一個排程會優先使用在 hello 順序：

1. 排程套用的 tooa 資源群組
2. 排程套用的 tooa 資源群組和 hello 資源群組中的虛擬機器
3. 排程套用 tooa 虛擬機器

此案例基本上會採用指定格式的 JSON 字串，並將它加入做為 hello 值稱為 「 排程的標記。 Runbook 會列出所有資源群組和虛擬機器，然後識別 hello 排程為每個稍早所列的 hello 案例為基礎的 VM。 接下來它會迴圈 hello 有附加的排程的 Vm，並評估，應該採取什麼動作。 例如，它會判斷 Vm 需要 toobe 停止、 關閉或忽略。

這些 runbook 使用 hello 驗證[Azure 執行身分帳戶](automation-sec-configure-azure-runas-account.md)。

## <a name="download-hello-runbooks-for-hello-scenario"></a>下載 hello runbook hello 案例
此案例包含四個 PowerShell 工作流程 runbook，您可以下載從 hello [TechNet 資源庫](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7)或 hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup)這個專案的儲存機制。

| Runbook | 說明 |
| --- | --- |
| Test-ResourceSchedule |檢查每個虛擬機器排程並執行關機或根據 hello 排程啟動。 |
| Add-ResourceSchedule |新增 hello 排程標記 tooa VM 或資源群組。 |
| Update-ResourceSchedule |修改現有排程標記 hello 取代新建一個。 |
| Remove-ResourceSchedule |從 VM 或資源群組中移除 hello 排程標記。 |

## <a name="install-and-configure-this-scenario"></a>安裝和設定此案例
### <a name="install-and-publish-hello-runbooks"></a>安裝和發佈 runbook hello
下載之後 hello runbook，您可以使用匯入它們中的 hello 程序[建立或匯入 Azure 自動化中的 runbook](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation)。  在每個 Runbook 成功匯入到您的自動化帳戶之後予以發佈。

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a>新增排程 toohello 測試 ResourceSchedule runbook
請遵循這些步驟 tooenable hello 排程的 hello 測試 ResourceSchedule runbook。 這是 hello runbook，用來驗證虛擬機器應該要啟動、 關閉，或者保持原樣。

1. 從 hello Azure 入口網站，開啟您的自動化帳戶，然後按一下hello **Runbook**磚。
2. 在 hello**測試 ResourceSchedule**刀鋒視窗中，按一下 hello**排程**磚。
3. 在 hello**排程**刀鋒視窗中，按一下 **加入排程**。
4. 在 hello**排程**刀鋒視窗中，選取**排程 tooyour runbook 連結**。 然後選取 [建立新的排程] 。
5. 在 hello**新排程**刀鋒視窗中，輸入 hello 名稱的這個排程，例如： *HourlyExecution*。
6. Hello 排程**啟動**，設定 hello 開始時間 tooan 小時增量。
7. 選取 [週期]，然後針對 [重複出現間隔] 選取 [1 小時]。
8. 確認**組是否逾期**設定得**否**，然後按一下**建立**toosave 新的排程。
9. 在 hello**排程 Runbook**選項刀鋒視窗中，選取**參數與回合的設定**。 在 hello 測試 ResourceSchedule**參數**刀鋒視窗中，輸入您的訂閱 hello 名稱 hello**訂用帳戶名稱**欄位。  這是 hello hello runbook 所需的唯一參數。  完成時，請按一下 [確定] 。

hello runbook 排程看起來應該類似下列 hello 完成之後：

![已設定的 Test-ResourceSchedule Runbook](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a>格式 hello JSON 字串
此解決方案會採用 JSON 的指定格式的字串，並將它加入做為標記的 hello 值基本上呼叫排程。 然後 runbook 列出所有資源群組和虛擬機器，並識別每個虛擬機器的 hello 排程。

hello runbook 有附加的排程的 hello 虛擬機器上執行迴圈，並檢查應該採取什麼動作。 hello 以下是如何格式化 hello 解決方案的範例：

```json
{
    "TzId": "Eastern Standard Time",
    "0": {
        "S": "11",
        "E": "17"
    },
    "1": {
        "S": "9",
        "E": "19"
    },
    "2": {
        "S": "9",
        "E": "19"
    },
}
```

以下是此結構的部分詳細資訊︰

1. 此 JSON 結構的 hello 格式為最佳化的 toowork 採用單一標記值，在 Azure 中的 hello 256 個字元限制。
2. *TzId*代表 hello hello 虛擬機器的時區時間。 這個識別碼可透過 PowerShell 工作階段--使用 hello TimeZoneInfo.NET 類別**[System.TimeZoneInfo]:: GetSystemTimeZones()**。

   ![PowerShell 中的 GetSystemTimeZones](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * 工作日會使用零 toosix 的數值表示。 hello 零的值等於星期日。
   * hello 開始時間以表示 hello **S**屬性和其值為 24 小時制格式。
   * hello 結束或關機時間表示以 hello **E**屬性和其值為 24 小時制格式。

     如果 hello **S**和**E**每一個屬性的值為零 (0)、 在 hello 時間評估其目前的狀態將保持 hello 虛擬機器。
3. 如果您想 tooskip 評估 hello 當週的特定日期時，不針對該日 hello 週中的新增區段。 在 hello 遵循範例中，只有星期一會評估並 hello 其他 hello 星期幾都會被忽略：

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a>標記資源群組或 VM
tooshut 關閉 Vm，您需要 tootag hello Vm 或其所處的 hello 資源群組。 沒有「排程」標籤的虛擬機器不會進行評估。 因此，不會加以啟動或關閉。

有兩種方式 tootag 資源群組或 Vm 具有此解決方案。 您可以直接從 hello 入口網站進行。 或者，您可以使用新增 ResourceSchedule hello、 更新 ResourceSchedule 及移除 ResourceSchedule runbook。

### <a name="tag-through-hello-portal"></a>標記透過 hello 入口網站
請遵循這些步驟 tootag 虛擬機器或 hello 入口網站中的資源群組：

1. 壓平合併 hello JSON 字串，並確認沒有任何空格。  您的 JSON 字串應該如下所示︰

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. 選取 hello**標記**圖示的 VM 或資源群組 tooapply 此排程。

   ![VM 標籤選項](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. 標籤會定義於金鑰/值組之後。 型別**排程**在 hello**金鑰**欄位，並將 hello JSON 字串 hello 貼入**值**欄位。 按一下 [儲存] 。 您的新標籤現在應該會出現在 hello 清單中的資源標記。

   ![VM 排程標籤](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a>從 PowerShell 進行標記
所有匯入的 runbook 會包含在 hello 開頭的 hello 指令碼可說明如何 tooexecute hello 直接從 PowerShell runbook 的說明資訊。 您可以從 PowerShell 呼叫 hello 新增 ScheduleResource 和更新 ScheduleResource runbook。 您藉由傳遞必要的參數可讓您 toocreate 或更新 hello 排程標記 hello 入口網站以外的 VM 或資源群組上。

toocreate，新增和刪除透過 PowerShell 的標記，則需要太[設定 azure PowerShell 環境](/powershell/azure/overview)。 Hello 安裝程式完成之後，您可以繼續以 hello 下列步驟。

### <a name="create-a-schedule-tag-with-powershell"></a>使用 PowerShell 建立排程標籤
1. 開啟 PowerShell 工作階段。 接著，使用下列執行身分帳戶與訂用帳戶 toospecify 範例 tooauthenticate hello:

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. 定義排程雜湊表。 以下是其建構方式的範例：

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. 定義所需的 hello runbook hello 參數。 在下列範例的 hello，我們的目標 VM:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    如果您要標記的資源群組，移除 hello *VMName*參數從 hello $params 雜湊資料表，如下所示：

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. 執行 hello 新增 ResourceSchedule runbook 以下列參數 toocreate hello 排程標記 hello:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. 資源群組或虛擬機器標記，tooupdate 執行 hello**更新 ResourceSchedule** runbook 以 hello 下列參數：

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a>使用 PowerShell 移除排程標籤
1. 開啟 PowerShell 工作階段和執行下列執行身分帳戶與 tooselect tooauthenticate hello 和指定的訂用帳戶：

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. 定義所需的 hello runbook hello 參數。 在下列範例的 hello，我們的目標 VM:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    如果您正在從資源群組中移除標記，移除 hello *VMName*參數從 hello $params 雜湊資料表，如下所示：

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. 執行 hello 移除 ResourceSchedule runbook tooremove hello 排程標記：

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. tooupdate 資源群組或虛擬機器標記，執行 hello 移除 ResourceSchedule runbook 以 hello 下列參數：

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> 我們建議您主動監視正在您的虛擬機器的 tooverify 關閉這些 runbook （和 hello 虛擬機器狀態），並據以啟動。
>

hello Azure 入口網站中，選取 hello tooview hello 詳細資料的 hello 測試 ResourceSchedule runbook 作業**作業**hello runbook 的磚。 hello 工作摘要顯示 hello 輸入的參數及 hello 輸出資料流，此外 toogeneral hello 工作的資訊和任何例外狀況發生。

hello**工作摘要**包括從 hello 輸出、 警告和錯誤資料流的訊息。 選取 hello**輸出**磚 tooview 詳細 hello runbook 執行結果。

![Test-ResourceSchedule 輸出](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a>後續步驟
* tooget 開始使用 PowerShell 工作流程 runbook，請參閱[我的第一個 PowerShell 工作流程 runbook](automation-first-runbook-textual.md)。
* toolearn 深入了解 runbook 類型，其優點和限制，請參閱[Azure 自動化 runbook 類型](automation-runbook-types.md)。
* 如需 PowerShell 指令碼支援功能的詳細資訊，請參閱 [Azure 自動化中的原生 PowerShell 指令碼支援](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)。
* toolearn 深入了解 runbook 記錄和輸出，請參閱[Runbook 輸出和在 Azure 自動化中的訊息](automation-runbook-output-and-messages.md)。
* 深入了解 Azure 執行身分帳戶，以及如何 tooauthenticate runbook 使用，請參閱 toolearn[驗證與 Azure 執行身分帳戶的 runbook](automation-sec-configure-azure-runas-account.md)。
