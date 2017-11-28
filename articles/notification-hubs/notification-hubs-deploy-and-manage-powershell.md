---
title: "使用 PowerShell 來部署和管理通知中樞"
description: "如何使用 PowerShell 來進行自動化的通知中樞建立和管理"
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
ms.openlocfilehash: 4db058e4bd91dc287b14e887abc6c378c65c4a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a><span data-ttu-id="f19aa-103">使用 PowerShell 來部署和管理通知中樞</span><span class="sxs-lookup"><span data-stu-id="f19aa-103">Deploy and Manage Notification Hubs using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="f19aa-104">概觀</span><span class="sxs-lookup"><span data-stu-id="f19aa-104">Overview</span></span>
<span data-ttu-id="f19aa-105">本文將說明如何使用 PowerShell 來建立和管理 Azure 通知中樞。</span><span class="sxs-lookup"><span data-stu-id="f19aa-105">This article shows you how to use Create and Manage Azure Notification Hubs using PowerShell.</span></span> <span data-ttu-id="f19aa-106">本主題示範下列一般自動化工作。</span><span class="sxs-lookup"><span data-stu-id="f19aa-106">The following common automation tasks are shown in this topic.</span></span>

* <span data-ttu-id="f19aa-107">建立通知中樞</span><span class="sxs-lookup"><span data-stu-id="f19aa-107">Create a Notification Hub</span></span>
* <span data-ttu-id="f19aa-108">設定認證</span><span class="sxs-lookup"><span data-stu-id="f19aa-108">Set Credentials</span></span>

<span data-ttu-id="f19aa-109">如果您也需要為通知中樞建立新服務匯流排命名空間，請參閱 [使用 PowerShell 管理服務匯流排](../service-bus-messaging/service-bus-powershell-how-to-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="f19aa-109">If you also need to create a new service bus namespace for your notification hubs, see [Manage Service Bus with PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span></span>

<span data-ttu-id="f19aa-110">Azure PowerShell 隨附的 Cmdlet 無法直接支援「管理通知中樞」。</span><span class="sxs-lookup"><span data-stu-id="f19aa-110">Managing Notifications Hubs is not supported directly by the cmdlets included with Azure PowerShell.</span></span> <span data-ttu-id="f19aa-111">從 PowerShell 進行的最佳方法，是參考 Microsoft.Azure.NotificationHubs.dll 組件。</span><span class="sxs-lookup"><span data-stu-id="f19aa-111">The best approach from PowerShell is to reference the Microsoft.Azure.NotificationHubs.dll assembly.</span></span> <span data-ttu-id="f19aa-112">組件隨附於 [Microsoft Azure 通知中樞 NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)。</span><span class="sxs-lookup"><span data-stu-id="f19aa-112">The assembly is distributed with the [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f19aa-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="f19aa-113">Prerequisites</span></span>
<span data-ttu-id="f19aa-114">開始閱讀本文之前，您必須符合下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="f19aa-114">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="f19aa-115">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f19aa-115">An Azure subscription.</span></span> <span data-ttu-id="f19aa-116">Azure 是訂閱型平台。</span><span class="sxs-lookup"><span data-stu-id="f19aa-116">Azure is a subscription-based platform.</span></span> <span data-ttu-id="f19aa-117">如需取得訂用帳戶的詳細資訊，請參閱[購買選項]、[成員優惠]或[免費試用版]。</span><span class="sxs-lookup"><span data-stu-id="f19aa-117">For more information about obtaining a subscription, see [Purchase Options], [Member Offers], or [Free Trial].</span></span>
* <span data-ttu-id="f19aa-118">具備 Azure PowerShell 的電腦。</span><span class="sxs-lookup"><span data-stu-id="f19aa-118">A computer with Azure PowerShell.</span></span> <span data-ttu-id="f19aa-119">如需指示，請參閱 [安裝並設定 Azure PowerShell]。</span><span class="sxs-lookup"><span data-stu-id="f19aa-119">For instructions, see [Install and configure Azure PowerShell].</span></span>
* <span data-ttu-id="f19aa-120">大致了解 PowerShell 指令碼、NuGet 封裝和 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="f19aa-120">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="including-a-reference-to-the-net-assembly-for-service-bus"></a><span data-ttu-id="f19aa-121">包括對服務匯流排之 .NET 組件的參考</span><span class="sxs-lookup"><span data-stu-id="f19aa-121">Including a reference to the .NET assembly for Service Bus</span></span>
<span data-ttu-id="f19aa-122">Azure PowerShell 中的 PowerShell Cmdlet 尚未提供「管理 Azure 通知中樞」。</span><span class="sxs-lookup"><span data-stu-id="f19aa-122">Managing Azure Notification Hubs is not yet included with the PowerShell cmdlets in Azure PowerShell.</span></span> <span data-ttu-id="f19aa-123">若要佈建通知中樞，可以使用 [Microsoft Azure 通知中樞 NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)中所提供的 .NET 用戶端。</span><span class="sxs-lookup"><span data-stu-id="f19aa-123">To provision notification hubs, you can use the .NET client provided in the [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="f19aa-124">首先，請確定指令碼可以找到 **Microsoft.Azure.NotificationHubs.dll** 組件，其在 Visual Studio 專案中會以 NuGet 套件的形式安裝。</span><span class="sxs-lookup"><span data-stu-id="f19aa-124">First, make sure your script can locate the **Microsoft.Azure.NotificationHubs.dll** assembly, which is installed as a NuGet package in a Visual Studio project.</span></span> <span data-ttu-id="f19aa-125">為了要有使用彈性，指令碼會執行這些步驟：</span><span class="sxs-lookup"><span data-stu-id="f19aa-125">In order to be flexible, the script performs these steps:</span></span>

1. <span data-ttu-id="f19aa-126">判斷叫用的路徑。</span><span class="sxs-lookup"><span data-stu-id="f19aa-126">Determines the path at which it was invoked.</span></span>
2. <span data-ttu-id="f19aa-127">周遊路徑，直到找到名為 `packages`的資料夾為止。</span><span class="sxs-lookup"><span data-stu-id="f19aa-127">Traverses the path until it finds a folder named `packages`.</span></span> <span data-ttu-id="f19aa-128">當您安裝 Visual Studio 專案的 NuGet 封裝時，會建立這個資料夾。</span><span class="sxs-lookup"><span data-stu-id="f19aa-128">This folder is created when you install NuGet packages for Visual Studio projects.</span></span>
3. <span data-ttu-id="f19aa-129">以遞迴方式搜尋 `packages` 資料夾中是否有名稱為 **Microsoft.Azure.NotificationHubs.dll**的組件。</span><span class="sxs-lookup"><span data-stu-id="f19aa-129">Recursively searches the `packages` folder for an assembly named **Microsoft.Azure.NotificationHubs.dll**.</span></span>
4. <span data-ttu-id="f19aa-130">參考組件，以供稍後使用這些類型。</span><span class="sxs-lookup"><span data-stu-id="f19aa-130">References the assembly so that the types are available for later use.</span></span>

<span data-ttu-id="f19aa-131">以下是如何使用 PowerShell 指令碼實作這些步驟的方式：</span><span class="sxs-lookup"><span data-stu-id="f19aa-131">Here's how these steps are implemented in a PowerShell script:</span></span>

``` powershell

try
{
    # WARNING: Make sure to reference the latest version of Microsoft.Azure.NotificationHubs.dll
    Write-Output "Adding the [Microsoft.Azure.NotificationHubs.dll] assembly to the script..."
    $scriptPath = Split-Path (Get-Variable MyInvocation -Scope 0).Value.MyCommand.Path
    $packagesFolder = (Split-Path $scriptPath -Parent) + "\packages"
    $assembly = Get-ChildItem $packagesFolder -Include "Microsoft.Azure.NotificationHubs.dll" -Recurse
    Add-Type -Path $assembly.FullName

    Write-Output "The [Microsoft.Azure.NotificationHubs.dll] assembly has been successfully added to the script."
}

catch [System.Exception]
{
    Write-Error("Could not add the Microsoft.Azure.NotificationHubs.dll assembly to the script. Make sure you build the solution before running the provisioning script.")
}
```

## <a name="create-the-namespacemanager-class"></a><span data-ttu-id="f19aa-132">建立 NamespaceManager 類別</span><span class="sxs-lookup"><span data-stu-id="f19aa-132">Create the NamespaceManager class</span></span>
<span data-ttu-id="f19aa-133">若要佈建通知中樞，請從 SDK 建立 [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="f19aa-133">To provision Notification Hubs, create an instance of the [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) class from the SDK.</span></span> 

<span data-ttu-id="f19aa-134">您可以使用 Azure PowerShell 隨附的 [Get-AzureSBAuthorizationRule] Cmdlet 來擷取用來提供連接字串的授權規則。</span><span class="sxs-lookup"><span data-stu-id="f19aa-134">You can use the [Get-AzureSBAuthorizationRule] cmdlet included with Azure PowerShell to retrieve an authorization rule that's used to provide a connection string.</span></span> <span data-ttu-id="f19aa-135">我們將會在 `$NamespaceManager` 變數中儲存對 `NamespaceManager` 執行個體的參照。</span><span class="sxs-lookup"><span data-stu-id="f19aa-135">We'll store a reference to the `NamespaceManager` instance in the `$NamespaceManager` variable.</span></span> <span data-ttu-id="f19aa-136">我們將使用 `$NamespaceManager` 佈建通知中樞。</span><span class="sxs-lookup"><span data-stu-id="f19aa-136">We will use `$NamespaceManager` to provision a notification hub.</span></span>

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create the NamespaceManager object to create the hub
Write-Output "Creating a NamespaceManager object for the [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for the [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a><span data-ttu-id="f19aa-137">佈建新的通知中樞</span><span class="sxs-lookup"><span data-stu-id="f19aa-137">Provisioning a new Notification Hub</span></span>
<span data-ttu-id="f19aa-138">若要佈建新的通知中樞，請使用 [通知中樞的 .NET API]。</span><span class="sxs-lookup"><span data-stu-id="f19aa-138">To provision a new notification hub, use the [.NET API for Notification Hubs].</span></span>

<span data-ttu-id="f19aa-139">您會在指令碼的這個部分設定四個本機變數。</span><span class="sxs-lookup"><span data-stu-id="f19aa-139">In this part of the script you set up four local variables.</span></span> 

1. <span data-ttu-id="f19aa-140">`$Namespace` ：將此變數設定為要建立通知中樞之命名空間的名稱。</span><span class="sxs-lookup"><span data-stu-id="f19aa-140">`$Namespace` : Set this to the name of the namespace where you want to create a notification hub.</span></span>
2. <span data-ttu-id="f19aa-141">`$Path` ：將此路徑設定為新的通知中樞之名稱。</span><span class="sxs-lookup"><span data-stu-id="f19aa-141">`$Path` : Set this path to the name of the new notification hub.</span></span>  <span data-ttu-id="f19aa-142">例如，"MyHub"。</span><span class="sxs-lookup"><span data-stu-id="f19aa-142">For example, "MyHub".</span></span>    
3. <span data-ttu-id="f19aa-143">`$WnsPackageSid` ：從 [Windows 開發人員中心](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409)將此變數設定為 Windows 應用程式的封裝 SID。</span><span class="sxs-lookup"><span data-stu-id="f19aa-143">`$WnsPackageSid` : Set this to the package SID for you Windows App from the [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>
4. <span data-ttu-id="f19aa-144">`$WnsSecretkey`：從 [Windows 開發人員中心](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409)將此變數設定為 Windows 應用程式的祕密金鑰。</span><span class="sxs-lookup"><span data-stu-id="f19aa-144">`$WnsSecretkey`: Set this to the secret key for you Windows App from the [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>

<span data-ttu-id="f19aa-145">這些變數可用以連接命名空間，以及建立新的通知中樞，並將其設定為利用 WNS 認證，為 Windows 應用程式處理 Windows Notification Services (WNS) 通知。</span><span class="sxs-lookup"><span data-stu-id="f19aa-145">These variables are used to connect to your namespace and create a new Notification Hub configured to handle Windows Notification Services (WNS) notifications with WNS credentials for a Windows App.</span></span> <span data-ttu-id="f19aa-146">如需取得封裝 SID 與祕密金鑰的相關資訊，請參閱 [開始使用通知中樞](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) 教學課程。</span><span class="sxs-lookup"><span data-stu-id="f19aa-146">For information on obtaining the package SID and secret key see, the [Getting Started with Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span> 

* <span data-ttu-id="f19aa-147">指令碼片段使用 `NamespaceManager` 物件來查看 `$Path` 所識別的通知中樞是否存在。</span><span class="sxs-lookup"><span data-stu-id="f19aa-147">The script snippet uses the `NamespaceManager` object to check to see if the Notification Hub identified by `$Path` exists.</span></span>
* <span data-ttu-id="f19aa-148">如果不存在，指令碼會使用 WNS 認證建立 `NotificationHubDescription`，並將其傳遞至 `NamespaceManager` 類別 `CreateNotificationHub` 方法。</span><span class="sxs-lookup"><span data-stu-id="f19aa-148">If it does not exist, the script will create an `NotificationHubDescription` with WNS credentials and pass that to the `NamespaceManager` class `CreateNotificationHub` method.</span></span>

``` powershell

$Namespace = "<Enter your namespace>"
$Path  = "<Enter a name for your notification hub>"
$WnsPackageSid = "<your package sid>"
$WnsSecretkey = "<enter your secret key>"

$WnsCredential = New-Object -TypeName Microsoft.Azure.NotificationHubs.WnsCredential -ArgumentList $WnsPackageSid,$WnsSecretkey

# Query the namespace
$CurrentNamespace = Get-AzureSBNamespace -Name $Namespace

# Check if the namespace already exists
if ($CurrentNamespace)
{
    Write-Output "The namespace [$Namespace] in the [$($CurrentNamespace.Region)] region was found."

    # Create the NamespaceManager object used to create a new notification hub
    $sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
    Write-Output "Creating a NamespaceManager object for the [$Namespace] namespace..."
    $NamespaceManager = [Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
    Write-Output "NamespaceManager object for the [$Namespace] namespace has been successfully created."

    # Check to see if the Notification Hub already exists
    if ($NamespaceManager.NotificationHubExists($Path))
    {
        Write-Output "The [$Path] notification hub already exists in the [$Namespace] namespace."  
    }
    else
    {
        Write-Output "Creating the [$Path] notification hub in the [$Namespace] namespace."
        $NHDescription = New-Object -TypeName Microsoft.Azure.NotificationHubs.NotificationHubDescription -ArgumentList $Path;
        $NHDescription.WnsCredential = $WnsCredential;
        $NamespaceManager.CreateNotificationHub($NHDescription);
        Write-Output "The [$Path] notification hub was created in the [$Namespace] namespace."
    }
}
else
{
    Write-Host "The [$Namespace] namespace does not exist."
}
```




## <a name="additional-resources"></a><span data-ttu-id="f19aa-149">其他資源</span><span class="sxs-lookup"><span data-stu-id="f19aa-149">Additional Resources</span></span>
* [<span data-ttu-id="f19aa-150">使用 PowerShell 管理服務匯流排</span><span class="sxs-lookup"><span data-stu-id="f19aa-150">Manage Service Bus with PowerShell</span></span>](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="f19aa-151">如何使用 PowerShell 指令碼來建立服務匯流排佇列、主題及訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f19aa-151">How to create Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="f19aa-152">如何使用 PowerShell 指令碼來建立服務匯流排命名空間與事件中樞</span><span class="sxs-lookup"><span data-stu-id="f19aa-152">How to create a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

<span data-ttu-id="f19aa-153">也有一些現成的指令碼可供下載：</span><span class="sxs-lookup"><span data-stu-id="f19aa-153">Some ready-made scripts are also available for download:</span></span>

* [<span data-ttu-id="f19aa-154">服務匯流排 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="f19aa-154">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

<span data-ttu-id="f19aa-155">[購買選項]: http://azure.microsoft.com/pricing/purchase-options/</span><span class="sxs-lookup"><span data-stu-id="f19aa-155">[Purchase Options]: http://azure.microsoft.com/pricing/purchase-options/</span></span>
<span data-ttu-id="f19aa-156">[成員優惠]: http://azure.microsoft.com/pricing/member-offers/</span><span class="sxs-lookup"><span data-stu-id="f19aa-156">[Member Offers]: http://azure.microsoft.com/pricing/member-offers/</span></span>
<span data-ttu-id="f19aa-157">[免費試用版]: http://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="f19aa-157">[Free Trial]: http://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="f19aa-158">[安裝並設定 Azure PowerShell]: /powershell/azureps-cmdlets-docs</span><span class="sxs-lookup"><span data-stu-id="f19aa-158">[Install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs</span></span>
<span data-ttu-id="f19aa-159">[通知中樞的 .NET API]: https://msdn.microsoft.com/library/azure/mt414893.aspx</span><span class="sxs-lookup"><span data-stu-id="f19aa-159">[.NET API for Notification Hubs]: https://msdn.microsoft.com/library/azure/mt414893.aspx</span></span>
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
<span data-ttu-id="f19aa-160">[Get-AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx</span><span class="sxs-lookup"><span data-stu-id="f19aa-160">[Get-AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx</span></span>

