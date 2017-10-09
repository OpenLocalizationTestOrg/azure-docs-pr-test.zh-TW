---
title: "aaaDeploy 和使用 PowerShell 管理通知中樞"
description: "如何 tooCreate 管理通知中樞使用 PowerShell 和自動化"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 7c58f2c8-0399-42bc-9e1e-a7f073426451
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8835bdefa0d360354263eab8040259ad08281771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a>使用 PowerShell 來部署和管理通知中樞
## <a name="overview"></a>概觀
本文章將示範如何 toouse 建立和管理 Azure 通知中心使用 PowerShell。 本主題中，會顯示 hello 遵循一般的自動化工作。

* 建立通知中樞
* 設定認證

如果您也需要 toocreate 新的服務匯流排命名空間的通知中樞，請參閱[使用 PowerShell 管理 Service Bus](../service-bus-messaging/service-bus-powershell-how-to-provision.md)。

不支援直接由 hello cmdlet 隨附於 Azure PowerShell 管理通知中樞。 從 PowerShell hello 最好的方法是 tooreference hello Microsoft.Azure.NotificationHubs.dll 組件。 散發 hello 組件以 hello [Microsoft Azure 通知中樞 NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)。

## <a name="prerequisites"></a>必要條件
在開始這份文件之前，您必須擁有 hello 下列：

* Azure 訂用帳戶。 Azure 是訂閱型平台。 如需取得訂用帳戶的詳細資訊，請參閱[購買選項]、[成員優惠]或[免費試用版]。
* 具備 Azure PowerShell 的電腦。 如需指示，請參閱 [安裝並設定 Azure PowerShell]。
* PowerShell 指令碼及 NuGet 套件 hello.NET Framework 的基本認識。

## <a name="including-a-reference-toohello-net-assembly-for-service-bus"></a>包含服務匯流排的參考 toohello.NET 組件
管理 Azure 通知中心尚未隨附 hello Azure PowerShell 中的 PowerShell cmdlet。 tooprovision 通知中樞，您可以使用 hello.NET 用戶端 hello 中提供[Microsoft Azure 通知中樞 NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)。

首先，請確定您的指令碼就可以找出 hello **Microsoft.Azure.NotificationHubs.dll**組件，它會安裝為 Visual Studio 專案中的 NuGet 封裝。 在訂單 toobe 彈性，hello 指令碼會執行下列步驟：

1. 決定 hello，叫用所在的路徑。
2. 周遊 hello 路徑，直到找到名為的資料夾`packages`。 當您安裝 Visual Studio 專案的 NuGet 封裝時，會建立這個資料夾。
3. 以遞迴方式搜尋 hello`packages`名為組件的資料夾**Microsoft.Azure.NotificationHubs.dll**。
4. 參考 hello 組件，以便 hello 類型可用以供稍後使用。

以下是如何使用 PowerShell 指令碼實作這些步驟的方式：

``` powershell

try
{
    # WARNING: Make sure tooreference hello latest version of Microsoft.Azure.NotificationHubs.dll
    Write-Output "Adding hello [Microsoft.Azure.NotificationHubs.dll] assembly toohello script..."
    $scriptPath = Split-Path (Get-Variable MyInvocation -Scope 0).Value.MyCommand.Path
    $packagesFolder = (Split-Path $scriptPath -Parent) + "\packages"
    $assembly = Get-ChildItem $packagesFolder -Include "Microsoft.Azure.NotificationHubs.dll" -Recurse
    Add-Type -Path $assembly.FullName

    Write-Output "hello [Microsoft.Azure.NotificationHubs.dll] assembly has been successfully added toohello script."
}

catch [System.Exception]
{
    Write-Error("Could not add hello Microsoft.Azure.NotificationHubs.dll assembly toohello script. Make sure you build hello solution before running hello provisioning script.")
}
```

## <a name="create-hello-namespacemanager-class"></a>建立 hello NamespaceManager 類別
tooprovision 通知中樞建立 hello 的執行個體[NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) hello SDK 中的類別。 

您可以使用 hello [Get AzureSBAuthorizationRule]隨附於 Azure PowerShell tooretrieve 授權規則使用 tooprovide 連接字串的 cmdlet。 我們將會儲存參考 toohello `NamespaceManager` hello 中的執行個體`$NamespaceManager`變數。 我們將使用`$NamespaceManager`tooprovision 通知中樞。

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create hello NamespaceManager object toocreate hello hub
Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a>佈建新的通知中樞
新的通知中樞，tooprovision 使用 hello[通知中樞的.NET API]。

在這個部分中的 hello 指令碼設定四個本機變數。 

1. `$Namespace`： 設定此 toohello hello 命名空間的名稱要 toocreate 通知中樞。
2. `$Path`： 設定此路徑 toohello 的 hello 新通知中樞名稱。  例如，"MyHub"。    
3. `$WnsPackageSid`： 這個 toohello 封裝 SID 為您設定 Windows 應用程式從 hello [Windows 開發人員中心](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409)。
4. `$WnsSecretkey`： 此 toohello 密碼金鑰為您設定 Windows 應用程式從 hello [Windows 開發人員中心](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409)。

這些變數是使用的 tooconnect tooyour 命名空間，並且建立新的設定通知中樞 toohandle Windows 通知服務 (WNS) 通知使用 WNS 認證之 Windows 應用程式。 如需取得 hello 封裝 SID 與秘密金鑰，請參閱 hello[開始使用通知中心](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)教學課程。 

* hello 指令碼的程式碼片段會使用 hello`NamespaceManager`物件所識別的通知中樞 hello toocheck toosee`$Path`存在。
* 如果不存在，將會建立 hello 指令碼`NotificationHubDescription`搭配 WNS 認證，以及傳遞該 toohello`NamespaceManager`類別`CreateNotificationHub`方法。

``` powershell

$Namespace = "<Enter your namespace>"
$Path  = "<Enter a name for your notification hub>"
$WnsPackageSid = "<your package sid>"
$WnsSecretkey = "<enter your secret key>"

$WnsCredential = New-Object -TypeName Microsoft.Azure.NotificationHubs.WnsCredential -ArgumentList $WnsPackageSid,$WnsSecretkey

# Query hello namespace
$CurrentNamespace = Get-AzureSBNamespace -Name $Namespace

# Check if hello namespace already exists
if ($CurrentNamespace)
{
    Write-Output "hello namespace [$Namespace] in hello [$($CurrentNamespace.Region)] region was found."

    # Create hello NamespaceManager object used toocreate a new notification hub
    $sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
    Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
    $NamespaceManager = [Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
    Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."

    # Check toosee if hello Notification Hub already exists
    if ($NamespaceManager.NotificationHubExists($Path))
    {
        Write-Output "hello [$Path] notification hub already exists in hello [$Namespace] namespace."  
    }
    else
    {
        Write-Output "Creating hello [$Path] notification hub in hello [$Namespace] namespace."
        $NHDescription = New-Object -TypeName Microsoft.Azure.NotificationHubs.NotificationHubDescription -ArgumentList $Path;
        $NHDescription.WnsCredential = $WnsCredential;
        $NamespaceManager.CreateNotificationHub($NHDescription);
        Write-Output "hello [$Path] notification hub was created in hello [$Namespace] namespace."
    }
}
else
{
    Write-Host "hello [$Namespace] namespace does not exist."
}
```




## <a name="additional-resources"></a>其他資源
* [使用 PowerShell 管理服務匯流排](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [如何 toocreate 服務匯流排佇列、 主題和訂用帳戶的 PowerShell 指令碼](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [如何為服務匯流排命名空間，並使用 PowerShell 指令碼的事件中樞的 toocreate](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

也有一些現成的指令碼可供下載：

* [服務匯流排 PowerShell 指令碼](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[購買選項]: http://azure.microsoft.com/pricing/purchase-options/
[成員優惠]: http://azure.microsoft.com/pricing/member-offers/
[免費試用版]: http://azure.microsoft.com/pricing/free-trial/
[安裝並設定 Azure PowerShell]: /powershell/azureps-cmdlets-docs
[通知中樞的.NET API]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[Get AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx

