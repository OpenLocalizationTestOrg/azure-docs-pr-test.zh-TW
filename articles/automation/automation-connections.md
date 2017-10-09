---
title: "在 Azure 自動化中的 aaaConnection 資產 |Microsoft 文件"
description: "在 Azure 自動化連線資產包含 hello 所需的資訊 tooconnect tooan 外部服務或從 runbook 或 DSC 設定的應用程式。 這篇文章說明連線的 hello 詳細資料以及如何與它們的 toowork 文字及圖形化撰寫。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: f0239017-5c66-4165-8cca-5dcb249b8091
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/13/2017
ms.author: magoedte; bwren
ms.openlocfilehash: f0f6b9fb960789b34af7b60eb1069313fdcf071c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connection-assets-in-azure-automation"></a>Azure 自動化中的連接資產

自動化連線資產包含 hello 所需的資訊 tooconnect tooan 外部服務或從 runbook 或 DSC 設定的應用程式。 這可能包括例如使用者名稱和密碼加入 tooconnection 資訊，例如 URL 或連接埠中的驗證所需的資訊。 連線的 hello 值將所有連接 tooa 特定應用程式在一個資產中為相對於 toocreating hello 屬性的多個變數。 hello 使用者可以編輯 hello 值在一個地方，連接和連接 tooa runbook 或 DSC 設定的 hello 名稱傳入的單一參數。 連接可以存取在 hello runbook 或以 hello 的 DSC 組態中的 hello 屬性**Get-automationconnection**活動。

建立連接時，您必須指定 *連接類型*。 hello 連接類型是定義一組屬性的範本。 hello 連接會定義其連線類型中定義的每一個屬性的值。 連線類型所加入的 tooAzure 自動化在整合模組中，或建立以 hello [Azure 自動化 API](http://msdn.microsoft.com/library/azure/mt163818.aspx)如果 hello 整合模組包含連接類型，並匯入您的自動化帳戶。 否則，您將需要 toocreate 中繼資料檔案 toospecify 自動化連線類型。  如需有關於此的進一步資訊，請參閱[整合模組](automation-integration-modules.md)。  

>[!NOTE] 
>Azure 自動化中的安全資產包括認證、憑證、連接和加密的變數。 這些資產都會經過加密並儲存在 hello 使用產生的唯一索引鍵，每個自動化帳戶的 Azure 自動化中。 這個索引鍵是由主要憑證加密，並且儲存在 Azure 自動化中。 之前儲存安全資產，hello 自動化帳戶的 hello 金鑰會解密使用 hello 主要憑證，並接著使用 tooencrypt hello 資產。

## <a name="windows-powershell-cmdlets"></a>Windows PowerShell Cmdlet

hello 下表中的 hello cmdlet 會使用的 toocreate，而且管理使用 Windows PowerShell 的自動化連線。 這些 cmdlet 隨附 hello [Azure PowerShell 模組](/powershell/azure/overview)可用於自動化 runbook 和 DSC 設定。

|Cmdlet|說明|
|:---|:---|
|[Get-AzureRmAutomationConnection](/powershell/module/azurerm.automation/get-azurermautomationconnection)|擷取連接。 包含與 hello hello 連線的欄位值的雜湊資料表。|
|[New-AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection)|建立新連接。|
|[Remove-AzureRmAutomationConnection](/powershell/module/azurerm.automation/remove-azurermautomationconnection)|移除現有的連接。|
|[Set-AzureRmAutomationConnectionFieldValue](/powershell/module/azurerm.automation/set-azurermautomationconnectionfieldvalue)|設定現有連線的特定欄位的 hello 值。|

## <a name="activities"></a>活動

hello 下表中的 hello 活動是 runbook 或 DSC 設定中的使用的 tooaccess 連線。

|活動|說明|
|---|---|
|[Get-AutomationConnection](/powershell/module/azure/get-azureautomationconnection?view=azuresmps-3.7.0)|取得連線 toouse。 傳回 hello hello 連接屬性的雜湊資料表。|

>[!NOTE] 
>您應該避免使用變數與 hello – Name 參數**Get-AutomationConnection**因為這可以在設計階段使得探索 runbook 或 DSC 設定與連線資產之間的相依性。

## <a name="creating-a-new-connection"></a>建立新連接

### <a name="toocreate-a-new-connection-with-hello-azure-portal"></a>toocreate 與 hello Azure 入口網站的新連線

1. 從您的自動化帳戶，按一下 hello**資產**一部分 tooopen hello**資產**刀鋒視窗。
2. 按一下 hello**連線**一部分 tooopen hello**連線**刀鋒視窗。
3. 按一下**新增連線**在 hello hello 刀鋒視窗最上方。
4. 在 hello**類型**下拉式清單中，選取 hello 類型要連接的 toocreate。 hello 表單將會顯示該特定類型的 hello 屬性。
5. 完成 hello 表單，然後按一下**建立**toosave hello 新的連接。

### <a name="toocreate-a-new-connection-with-hello-azure-classic-portal"></a>toocreate 與 hello Azure 傳統入口網站的新連線

1. 從您的自動化帳戶，按一下 **資產**hello hello 視窗上方。
2. 在 hello hello 視窗底部，按一下 **加入設定**。
3. 按一下 [ **加入連接**]。
4. 在 hello**連線類型**下拉式清單中，選取 hello 類型要連接的 toocreate。  hello 精靈將會顯示該特定類型的 hello 屬性。
5. 完成 hello 精靈，然後按一下 [hello] 核取方塊 toosave hello 新連線。

### <a name="toocreate-a-new-connection-with-windows-powershell"></a>toocreate 與 Windows PowerShell 的新連線

建立新的連接使用 Windows PowerShell 中使用 hello[新增 AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection) cmdlet。 這個 cmdlet 具有名為**ConnectionFieldValues** ，必須要有[雜湊表](http://technet.microsoft.com/library/hh847780.aspx)定義的每一個 hello hello 連線類型所定義的屬性值。

如果您已熟悉 hello 自動化[執行身分帳戶](automation-sec-configure-azure-runas-account.md)tooauthenticate runbook 使用 hello 服務主體，hello PowerShell 指令碼，提供替代 toocreating hello hello hello 入口網站中，從執行身分帳戶建立新的連線資產，使用下列命令範例 hello。  

    $ConnectionAssetName = "AzureRunAsConnection"
    $ConnectionFieldValues = @{"ApplicationId" = $Application.ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Cert.Thumbprint; "SubscriptionId" = $SubscriptionId}
    New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $AutomationAccountName -Name $ConnectionAssetName -ConnectionTypeName AzureServicePrincipal -ConnectionFieldValues $ConnectionFieldValues 

因為當您建立您的自動化帳戶時，會自動包含數個通用的模組以及 hello 連接類型的預設值，都能 toouse hello 指令碼 toocreate hello 連線資產**AzurServicePrincipal**toocreate hello **AzureRunAsConnection**連線資產。  這會是重要 tookeep 納入考量，因為如果您嘗試 toocreate 新的連線資產 tooconnect tooa 服務或應用程式使用不同的驗證方法時，它會失敗，因為 hello 連線類型未定義在您的自動化帳戶。  如需如何 toocreate 您自己的連接類型為您的自訂或模組從 hello 進一步資訊[PowerShell 資源庫](https://www.powershellgallery.com)，請參閱[整合模組](automation-integration-modules.md)
  
## <a name="using-a-connection-in-a-runbook-or-dsc-configuration"></a>在 Runbook 或 DSC 設定中使用連接

擷取 runbook 或 hello DSC 組態中的連接**Get-automationconnection** cmdlet。  您無法使用 hello [Get AzureRmAutomationConnection](https://docs.microsoft.com/powershell/resourcemanager/azurerm.automation/v1.0.12/Get-AzureRmAutomationConnection?redirectedfrom=msdn)活動。  此活動會擷取 hello hello hello 連線中不同的欄位值，並傳回它們作為[雜湊表](http://go.microsoft.com/fwlink/?LinkID=324844)然後可以使用與 hello hello runbook 或 DSC 設定中的適當命令。

### <a name="textual-runbook-sample"></a>文字式 Runbook 範例

hello 下列命令範例示範如何 toouse hello 執行身分帳戶先前所述，與您在 runbook 中的 Azure 資源管理員資源 tooauthenticate。  它會使用 hello 連接代表 hello 執行身分帳戶，即在參考 hello 憑證為基礎的服務主體，資產不認證。  

    $Conn = Get-AutomationConnection -Name AzureRunAsConnection 
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint 

### <a name="graphical-runbook-samples"></a>圖形化 Runbook 範例

您將加入**Get-automationconnection**以滑鼠右鍵按一下 hello 程式庫 窗格中的 hello 連線的 hello 圖形化編輯器，然後選取活動 tooa 圖形化 runbook**新增 toocanvas**。

![](media/automation-connections/connection-add-canvas.png)

hello 下列影像顯示在圖形化 runbook 中使用連接的範例。  這是 hello 如上所示，驗證使用具有文字 runbook hello 執行身分帳戶的相同範例。  這個範例會使用 hello**常數值**hello 的資料集**取得 RunAs 連接**用於驗證的連接物件的活動。  A[管線連結](automation-graphical-authoring-intro.md#links-and-workflow)hello ServicePrincipalCertificate 參數集需要單一物件，因為在此使用。

![](media/automation-connections/automation-get-connection-object.png)

## <a name="next-steps"></a>後續步驟

- 檢閱[連結在圖形化撰寫](automation-graphical-authoring-intro.md#links-and-workflow)toounderstand toodirect 和控制 hello 非固定格式的 runbook 中的邏輯。  

- 請參閱深入了解 Azure 自動化使用 PowerShell 模組和最佳作法 Azure 自動化中的整合模組以建立您自己的 PowerShell 模組 toowork toolearn[整合模組](automation-integration-modules.md)。  
