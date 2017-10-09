---
title: "aaaUse 與 Azure RemoteApp PowerShell cmdlet |Microsoft 文件"
description: "深入了解如何 toouse Azure RemoteApp 中的 Windows PowerShell cmdlet。"
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a>將 Windows PowerShell Cmdlet 搭配 Azure RemoteApp 使用
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

 您可以使用 hello Azure RemoteApp PowerShell cmdlet tooadminister 及維護您的集合。 使用下列資訊 tooget 啟動 hello。

## <a name="get-hello-cmdlets"></a>取得 hello cmdlet
- - -
第一次下載 hello Azure Powershell cmdlet[這裡](http://go.microsoft.com/?linkid=9811175)，hello RemoteApp 指令程式會包含在內般。 

簽出 hello [Azure RemoteApp 指令程式說明](/powershell/module/azure?view=azuresmps-3.7.0)。

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a>設定 Azure cmdlet toouse 訂用帳戶
- - -
請遵循[本指南](/powershell/azure/overview)因此您可以針對您的 Azure 訂用帳戶使用 hello cmdlet。

您可以使用這些步驟 tooget，快速入門：

1. 下載並安裝 hello [Azure PowerShell cmdlet](http://go.microsoft.com/?linkid=9811175)。
2. 啟動 Microsoft Azure PowerShell。
3. 執行**Add-azureaccount** tooauthenticate tooyour Azure 訂用帳戶。 出現提示時，輸入 hello 相同使用者名稱和密碼，您會使用 toosign tooAzure 入口網站中。  
4. 執行**Get-azuresubscription** toolist hello 訂用帳戶與您的使用者帳戶相關聯。 
5. 執行**Select-azuresubscription SubscriptionName&lt;訂用帳戶名稱&gt;**或**Select-azuresubscription SubscriptionId&lt;訂用帳戶 ID&gt;**  toospecify hello 訂用帳戶 toouse。

恭喜，您的 Azure PowerShell 主控台已設定且已準備 toouse。 請注意，您必須 toorepeate 步驟 2 到 5，每次啟動 hello hello Azure PowerShell 主控台。  


## <a name="list-all-collections"></a>列出所有集合
- - -
     Get-AzureRemoteAppCollection

## <a name="delete-a-collection"></a>刪除集合
- - -
    Remove-AzureRemoteAppCollection <enter collection name>

範例：`Remove-AzureRemoteAppCollection ContosoProduction`。

## <a name="create-a-cloud-collection"></a>建立雲端收藏
- - -
它很簡單，執行下列命令的 hello:

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

hello 上述命令會自動發佈 （Excel、 OneNote、 Outlook、 PowerPoint、 Visio 及 Word） 的 Microsoft Office 365 應用程式。

集合建立作業可能需要 30 分鐘或更長的 toocomplete。 因此，此命令會傳回可使用的追蹤識別碼，如下所示：

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

Hello 收集完成之後，您可以新增使用者 toohello 集合以 hello 下列命令：

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

大功告成！ 該使用者應該能夠 tooconnect toohello 應用程式使用 hello Azure RemoteApp 用戶端找到[這裡](https://www.remoteapp.windowsazure.com/)。

## <a name="available-cmdlets"></a>可用的 Cmdlet
其他命令，我們有很多，將會很快即將 hello 它們的文件：

基本 RemoteApp 集合 Cmdlet： 

* New-AzureRemoteAppCollection
* Get-AzureRemoteAppCollection
* Set-AzureRemoteAppCollection
* Update-AzureRemoteAppCollection
* Remove-AzureRemoteAppCollection
* Add-AzureRemoteAppUser
* Get-AzureRemoteAppUser
* Remove-AzureRemoteAppUser
* Get-AzureRemoteAppSession
* Disconnect-AzureRemoteAppSession
* Invoke-AzureRemoteAppSessionLogoff
* Send-AzureRemoteAppSessionMessage
* Get-AzureRemoteAppProgram
* Get-AzureRemoteAppStartMenuProgram
* Publish-AzureRemoteAppProgram
* Unpublish-AzureRemoteAppProgram
* Get-AzureRemoteAppCollectionUsageDetails
* Get-AzureRemoteAppCollectionUsageSummary
* Get-AzureRemoteAppPlan

RemoteApp virtual network cmdlets:

* New-AzureRemoteAppVNet
* Get-AzureRemoteAppVNet
* Set-AzureRemoteAppVNet
* Remove-AzureRemoteAppVNet
* Get-AzureRemoteAppVpnDevice
* Get-- AzureRemoteAppVpnDeviceConfigScript
* Reset-AzureRemoteAppVpnSharedKey

RemoteApp template image cmdlets:

* New-AzureRemoteAppTemplateImage
* Get-AzureRemoteAppTemplateImage
* Rename-AzureRemoteAppTemplateImage
* Remove-AzureRemoteAppTemplateImage

Other RemoteApp cmdlets:

* Get-AzureRemoteAppLocation
* Get-AzureRemoteAppWorkspace
* Set-AzureRemoteAppWorkspace
* Get-AzureRemoteAppOperationResult

