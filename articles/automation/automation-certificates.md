---
title: "在 Azure 自動化中的 aaaCertificate 資產 |Microsoft 文件"
description: "讓 runbook 或針對 Azure 和協力廠商資源的 DSC 組態 tooauthenticate 存取，則可以在 Azure 自動化中安全地儲存憑證。  這篇文章說明憑證的 hello 詳細資料以及如何與它們的 toowork 文字及圖形化撰寫。"
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a>Azure 自動化中的憑證資產

憑證可以安全地存放在 Azure 自動化中以便存取 runbook 的 DSC 設定使用 hello **Get AzureRmAutomationRmCertificate** Azure 資源管理員資源的活動。 這可讓您 toocreate runbook 和使用憑證進行驗證的 DSC 設定，或將它們加入 tooAzure 或協力廠商資源。

> [!NOTE] 
> Azure 自動化中的安全資產包括認證、憑證、連接和加密的變數。 這些資產都會經過加密並儲存在 hello 使用產生的唯一索引鍵，每個自動化帳戶的 Azure 自動化中。 這個索引鍵是由主要憑證加密，並且儲存在 Azure 自動化中。 之前儲存安全資產，hello 自動化帳戶的 hello 金鑰會解密使用 hello 主要憑證，並接著使用 tooencrypt hello 資產。
> 

## <a name="windows-powershell-cmdlets"></a>Windows PowerShell Cmdlet

hello 下表中的 hello cmdlet 會使用的 toocreate 和管理使用 Windows PowerShell 的自動化憑證資產。 這些 cmdlet 隨附 hello [Azure PowerShell 模組](../powershell-install-configure.md)可用於自動化 runbook 和 DSC 設定。

|Cmdlet|說明|
|:---|:---|
|[Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx)|擷取憑證 toouse runbook 或 DSC 設定中的相關資訊。 您只能從 Get-automationcertificat 活動擷取 hello 憑證本身。|
|[New-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603604.aspx)|建立新的憑證到 Azure 自動化。|
[Remove-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603529.aspx)|從 Azure 自動化中移除憑證。|建立新的憑證到 Azure 自動化。
|[Set-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603760.aspx)|設定包括 hello 憑證檔案和設定.pfx 的 hello 密碼上傳現有憑證的 hello 屬性。|
|[Add-AzureCertificate](https://msdn.microsoft.com/library/azure/dn495214.aspx)|上傳服務憑證的 hello 指定雲端服務。|


## <a name="creating-a-new-certificate"></a>建立新憑證

當您建立新的憑證時，您上傳.cer 或.pfx 檔案 tooAzure 自動化。 如果您要標示為可匯出的 hello 憑證，則可以將它從 hello Azure 自動化憑證存放區。 如果不是可匯出，然後它只能用於簽章 hello runbook 或 DSC 設定內。


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a>toocreate hello Azure 入口網站的新憑證

1. 從您的自動化帳戶，按一下 hello**資產**磚 tooopen hello**資產**刀鋒視窗。
1. 按一下 hello**憑證**磚 tooopen hello**憑證**刀鋒視窗。
1. 按一下**將憑證加入**在 hello hello 刀鋒視窗最上方。
2. 輸入 hello 憑證的名稱在 hello**名稱**方塊。
2. 按一下**選取檔案**下**憑證檔案上傳**toobrowse.cer 或.pfx 檔案。  如果您選取.pfx 檔案，指定密碼，以及是否應該允許 toobe 匯出。
1. 按一下**建立**toosave hello 新憑證資產。


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a>toocreate Windows PowerShell 的新憑證

hello 下列範例會示範如何 toocreate 新的自動化憑證，並將它標示為可匯出。 這樣會匯入現有的 pfx 檔案。

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a>使用憑證

您必須使用 hello **Get-automationcertificat**活動 toouse 憑證。 您無法使用 hello [Get AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet，因為它會傳回 hello 憑證資產，但不是 hello 憑證本身的相關資訊。

### <a name="textual-runbook-sample"></a>文字式 Runbook 範例

hello，下列程式碼範例顯示如何 tooadd 憑證 tooa 雲端在 runbook 中的服務。 在此範例中，從加密的自動化變數擷取 hello 密碼。

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a>圖形化 Runbook 範例

您將加入**Get-automationcertificat** tooa 圖形化 runbook，以滑鼠右鍵按一下 hello hello 圖形化編輯器和選取的程式庫 窗格中的 hello 憑證**新增 toocanvas**。

![新增憑證 toohello 畫布](media/automation-certificates/automation-certificate-add-to-canvas.png)

hello 下列影像顯示在圖形化 runbook 中使用憑證的範例。  這是 hello 相同憑證 tooa 雲端服務加入從文字的 runbook，如上所示的範例。

![範例圖形化編寫 ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a>後續步驟

- 更多有關連結 toocontrol hello 邏輯流程的活動使用您的 runbook 是的 toolearn 設計 tooperform，請參閱[連結在圖形化撰寫](automation-graphical-authoring-intro.md#links-and-workflow)。 
