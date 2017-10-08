---
title: "輸入參數的 aaaRunbook |Microsoft 文件"
description: "Runbook 的輸入的參數可以讓您 toopass 資料 tooa runbook 啟動時增加 hello 彈性的 runbook。 本文說明在 Runbook 中使用輸入參數的不同案例。"
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: f3abaf92382e7d41019616bafb14af23cf98dd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-input-parameters"></a>Runbook 輸入參數
Runbook 的輸入的參數可以讓您 toopass 資料 tooit 啟動時增加 hello 彈性的 runbook。 hello 參數可讓目標為特定案例和環境的 hello runbook 動作 toobe。 在本文中，我們將逐步引導您了解在 Runbook 中使用輸入參數的不同案例。

## <a name="configure-input-parameters"></a>設定輸入參數
輸入參數可以在 PowerShell、PowerShell 工作流程和圖形化 Runbook 中設定。 一個 Runbook 可以使用具有不同資料類型的多個參數，或完全不使用參數。 輸入參數可以是強制性或選擇性的，而且您可以為選擇性參數指派預設值。 您可以將值指派 toohello runbook 的輸入的參數，當您透過 hello 可用方法之一啟動。 這些方法包括從 hello 入口網站或 web 服務正在啟動 runbook。 您也可以啟動一個 Runbook 做為在另一個 Runbook 中以內嵌方式呼叫的子 Runbook。

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a>在 PowerShell 和 PowerShell 工作流程 Runbook 中設定輸入參數
PowerShell 和[PowerShell 工作流程 runbook](automation-first-runbook-textual.md) Azure 自動化中支援透過 hello 下列屬性定義的輸入的參數。  

| **屬性** | **說明** |
|:--- |:--- |
| 類型 |必要。 hello hello 參數值所預期的資料型別。 任何 .NET 類型皆有效。 |
| 名稱 |必要。 hello hello 參數名稱。 這必須 hello runbook 內是唯一的可包含字母、 數字或底線字元。 而且必須以字母開頭。 |
| 強制 |選用。 指定是否必須提供 hello 參數的值。 如果設定太**$true**，然後 hello runbook 啟動時，就必須提供值。 如果設定太**$false**，則為選擇性的值。 |
| 預設值 |選用。  指定如果傳入的值不是 hello runbook 啟動時將用於 hello 參數的值。 預設值可以設定任何參數，以及將自動進行 hello 參數選擇性不論 hello 強制設定。 |

Windows PowerShell 所支援的輸入參數屬性比此處所列的多，例如驗證、別名和參數集。 不過，Azure 自動化目前只支援 hello 輸入的參數上面所列。

在 PowerShell 工作流程 runbook 中的參數定義具有下列一般形式，多個參數會以逗號分隔的 hello。

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> 當您正在定義的參數，如果您未指定 hello**強制**屬性，則會根據預設，hello 參數視為選擇性參數。 此外，如果您在 PowerShell 工作流程 runbook 中設定參數的預設值，它將會被視為 powershell 選擇性參數，不論 hello**強制**屬性值。
> 
> 

例如，讓我們設定 hello 輸出詳細虛擬機器之單一 VM 或資源群組內的所有 Vm 的 PowerShell 工作流程 runbook 的輸入的參數。 此 runbook hello 下列螢幕擷取畫面所示，有兩個參數： hello 的虛擬機器和 hello hello 資源群組名稱的名稱。

![自動化 PowerShell 工作流程](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

在此參數定義中，hello 參數**$VMName**和**$resourceGroupName**是簡單字串類型的參數。 不過，PowerShell 和 PowerShell 工作流程 Runbook 支援所有簡單類型和複雜類型，例如輸入參數的 **object** 或 **PSCredential**。

如果您的 runbook 具有物件類型的輸入的參數，然後使用 PowerShell 雜湊表 （名稱、 值） 與組 toopass 值中。 例如，如果您有下列參數在 runbook 中的 hello:

     [Parameter (Mandatory = $true)]
     [object] $FullName

然後您可以傳遞值 toohello 參數後面的 hello:

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a>在圖形化 Runbook 中設定輸入參數
太[設定圖形化 runbook](automation-first-runbook-graphical.md)具有輸入參數，讓我們來建立圖形化 runbook 會輸出可能是虛擬機器的相關詳細資料之單一 VM 或資源群組內的所有 Vm。 設定 Runbook 包含兩個主要活動，如下所述。

[**向 Azure 執行身分帳戶的 Runbook** ](automation-sec-configure-azure-runas-account.md) tooauthenticate 與 Azure。

[**Get AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) tooget hello 屬性的虛擬機器。

您可以使用 hello [ **Write-output** ](https://technet.microsoft.com/library/hh849921.aspx)活動 toooutput hello 虛擬機器的名稱。 hello 活動**Get AzureRmVm**接受兩個參數，hello**虛擬機器名稱**和 hello**資源群組名稱**。 由於每次啟動 hello runbook 時，這些參數可能需要不同的值，您可以加入輸入的參數 tooyour runbook。 以下是 hello 步驟 tooadd 輸入的參數：

1. 選取 hello hello 從圖形化 runbook **Runbook**刀鋒視窗，然後按一下[**編輯**](automation-graphical-authoring-intro.md)它。
2. 從 hello runbook 編輯器中，按一下 **輸入和輸出**tooopen hello**輸入和輸出**刀鋒視窗。
   
    ![自動化圖形化 Runbook](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. hello**輸入和輸出**刀鋒視窗會顯示 hello runbook 所定義的輸入參數的清單。 在這個刀鋒視窗中，您可以加入新的輸入的參數，或編輯現有輸入參數的 hello 組態。 按一下 tooadd hello runbook 的新參數**加入輸入**tooopen hello **Runbook 輸入的參數**刀鋒視窗。 您可以設定下列參數的 hello:
   
   | **屬性** | **說明** |
   |:--- |:--- |
   | 名稱 |必要。  hello hello 參數名稱。 這必須 hello runbook 內是唯一的可包含字母、 數字或底線字元。 而且必須以字母開頭。 |
   | 說明 |選用。 關於 hello 目的輸入參數的描述。 |
   | 類型 |選用。 hello 應有 hello 參數值的資料類型。 支援的參數類型有：**String**、**Int32**、**Int64**、**Decimal**、**Boolean**、**DateTime**、**Object**。 如果未選取的資料類型，則預設太**字串**。 |
   | 強制 |選用。 指定是否必須提供 hello 參數的值。 如果您選擇**是**，然後 hello runbook 啟動時，就必須提供值。 如果您選擇**沒有**，然後 hello runbook 已啟動，且可能會設定預設值時，不需要值。 |
   | 預設值 |選用。 指定如果傳入的值不是 hello runbook 啟動時將用於 hello 參數的值。 不是強制性的參數可以設定預設值。 預設值，tooset 選擇**自訂**。 除非另一個值中有提供 hello runbook 啟動時，會使用此值。 選擇**無**如果您不想 tooprovide 任何預設值。 |
   
    ![加入新的輸入](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. 建立兩個參數具有下列屬性，將由 hello hello **Get AzureRmVm**活動：
   
   * **參數1：**
     
     * Name - VMName
     * Type - String
     * Mandatory - No
   * **參數 2：**
     
     * Name - resourceGroupName
     * Type - String
     * Mandatory - No
     * Default value - Custom
     * 自訂的預設值- \<hello 包含 hello 虛擬機器的資源群組名稱 >
5. 一旦您加入 hello 參數，請按一下**確定**。  您現在可以檢視它們在 hello**輸入和輸出刀鋒視窗**。 再按一下 確定，然後按一下儲存 並 發佈 您的 Runbook。

## <a name="assign-values-tooinput-parameters-in-runbooks"></a>在 runbook 中的 tooinput 參數指派值
您可以在 hello 下列案例中的 runbook 中傳遞值 tooinput 參數。

### <a name="start-a-runbook-and-assign-parameters"></a>啟動 Runbook 並指派參數
Runbook 可以啟動許多方法： 透過 Azure 入口網站，使用 webhook、 PowerShell cmdlet，以 hello REST API 或 hello SDK hello。 以下我們將討論啟動 Runbook 並指派參數的不同方法。

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a>開始使用 hello Azure 入口網站已發佈的 runbook 和指派的參數
當您[啟動 hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal)，hello**啟動 Runbook**刀鋒視窗隨即開啟，而且您可以設定您剛才建立的 hello 參數的值。

![開始使用 hello 入口網站](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

在 hello hello 輸入方塊下方的標籤，您可以看到 hello hello 參數已設定的屬性。 這些屬性包括強制或選擇性、類型和預設值。 在 hello 說明提示氣球下一步 toohello 參數名稱，您可以看到所有您需要 toomake 參數輸入值來判斷 hello 金鑰資訊。 此資訊包括參數為強制或選擇性。 它也包含 hello 類型和預設值 （如果有的話） 和其他有用的資訊。

![說明提示氣球](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> 字串類型參數支援 **空** 字串值。  輸入**[EmptyString]**在 hello 輸入參數 方塊中會傳遞空字串 toohello 參數。 此外，字串類型參數不支援傳遞 **Null** 值。 如果您沒有傳遞任何值 toohello 字串參數，然後 PowerShell 會解譯為 null。
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a>使用 PowerShell Cmdlet 啟動已發佈的 Runbook，並指派參數
* **Azure Resource Manager Cmdlet：** 您可以使用 [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx)啟動在資源群組中建立的自動化 Runbook。
  
  **範例：**
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* **Azure 服務管理 Cmdlet：** 您可以使用 [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx)啟動在預設資源群組中建立的自動化 Runbook。
  
  **範例：**
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> 當您使用 PowerShell cmdlet，預設參數，來啟動 runbook **MicrosoftApplicationManagementStartedBy**使用 hello 值建立**PowerShell**。 您可以檢視此參數在 hello**作業詳細資料**刀鋒視窗。  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a>使用 SDK 啟動 Runbook，並指派參數
* **Azure 資源管理員的方法：**您可以使用 hello SDK 的程式設計語言來啟動 runbook。 以下 C# 程式碼片段用於在您的自動化帳戶中啟動 Runbook。 您可以檢視所有 hello 程式碼，在我們[GitHub 儲存機制](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs)。  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* **Azure 服務管理方法：**您可以使用 hello SDK 的程式設計語言來啟動 runbook。 以下 C# 程式碼片段用於在您的自動化帳戶中啟動 Runbook。 您可以檢視所有 hello 程式碼，在我們[GitHub 儲存機制](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs)。
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  toostart 這種方法，建立 runbook 參數的字典 toostore hello **VMName**和**resourceGroupName**，和它們的值。 然後啟動 hello runbook。 以下是呼叫 hello 方法，定義於上方的 hello C# 程式碼片段。
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a>啟動 runbook 使用 hello REST API 和指派的參數
Runbook 作業可建立及啟動以 hello Azure 自動化 REST API 使用 hello**放**以 hello 遵循方法要求 URI。

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

Hello 要求 URI 中取代 hello 下列參數：

* **subscription-id：** 您的 Azure 訂用帳戶識別碼。  
* **雲端服務名稱：**應該傳送嗨雲端服務 toowhich hello 要求 hello 名稱。  
* **自動化帳戶名稱：** hello 您裝載於 hello 的自動化帳戶名稱指定雲端服務。  
* **作業識別碼：** hello hello 工作的 GUID。 在 PowerShell 中的 Guid 可以建立使用 hello **[GUID]::NewGuid()。Tostring （)**命令。

在訂單 toopass 參數 toohello runbook 工作，使用 hello 要求主體。 它會採用下列 JSON 格式中提供的兩個屬性的 hello:

* **Runbook 名稱：** 必要。 hello 作業 toostart hello hello runbook 的名稱。  
* **Runbook 參數：** 選擇性。 字典 （名稱、 值） 中的 hello 參數清單的格式，其中名稱必須是字串型別和值可以是任何有效的 JSON 值。

如果您想 toostart hello **Get AzureVMTextual**稍早建立的 runbook **VMName**和**resourceGroupName**做為參數，使用下列 JSON 格式的 hellohello 要求主體。

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

如果 hello 工作成功建立，則會傳回 HTTP 狀態碼 「 201。 如需有關回應標頭和 hello 回應主體的詳細資訊，請參閱有關 toohello 文章太[使用 hello REST API 來建立 runbook 作業。](https://msdn.microsoft.com/library/azure/mt163849.aspx)

### <a name="test-a-runbook-and-assign-parameters"></a>測試 Runbook 並指派參數
當您[測試 hello 草稿版本，您的 runbook 的](automation-testing-runbook.md)使用 hello 測試選項，hello**測試**刀鋒視窗隨即開啟，而且您可以設定您剛才建立的 hello 參數的值。

![測試並指派參數](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a>排程 tooa runbook 連結和指派的參數
您可以[將排程連結](automation-schedules.md)tooyour runbook 讓該 hello runbook 在特定時間啟動。 當您建立 hello 排程並 hello runbook 將會使用這些值，hello 排程啟動時，您會指定輸入的參數。 提供所有必要的參數值之前，您無法儲存 hello 排程。

![排程並指派參數](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a>建立 Runbook 的 Webhook，並指派參數
您可以為您的 Runbook 建立 [Webhook](automation-webhooks.md) ，並設定 Runbook 輸入參數。 提供所有必要的參數值之前，您無法儲存 hello webhook。

![建立 Webhook 並指派參數](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

當您使用 webhook 執行 runbook 時，hello 預先定義的輸入的參數 **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** 傳送，以及您定義的 hello 輸入參數。 您可以按一下 tooexpand hello **WebhookData**參數，如需詳細資訊。

![WebhookData 參數](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a>後續步驟
* 如需關於 Runbook 輸入和輸出的詳細資訊，請參閱 [Azure 自動化：Runbook 輸入、輸出和巢狀 Runbook](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/)。
* 如需不同的方式 toostart runbook 的詳細資訊，請參閱[啟動 runbook](automation-starting-a-runbook.md)。
* tooedit 文字的 runbook，請參閱太[編輯文字的 runbook](automation-edit-textual-runbook.md)。
* tooedit 圖形化 runbook，請參閱太[Azure 自動化中的圖形化撰寫](automation-graphical-authoring-intro.md)。

