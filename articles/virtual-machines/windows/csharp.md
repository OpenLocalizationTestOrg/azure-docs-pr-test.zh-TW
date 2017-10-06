---
title: "aaaCreate 和管理 Azure 虛擬機器使用 C# |Microsoft 文件"
description: "使用 C# 和 Azure 資源管理員 toodeploy，虛擬機器和其支援的所有資源。"
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 87524373-5f52-4f4b-94af-50bf7b65c277
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 8beeabde731bbaa25e68d2b9c5abbf71acbe377f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a>在 Azure 中使用 C# 建立並管理 Windows VM #

[Azure 虛擬機器](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) 需要數個支援的 Azure 資源。 本文涵蓋使用 C# 建立、管理和刪除 VM 資源。 您會了解如何：

> [!div class="checklist"]
> * 建立 Visual Studio 專案
> * 安裝 hello 套件
> * 建立認證
> * 建立資源
> * 執行管理工作
> * 刪除資源
> * 執行 hello 應用程式

它會採用約 20 分鐘 toodo 這些步驟。

## <a name="create-a-visual-studio-project"></a>建立 Visual Studio 專案

1. 如果您尚未安裝 [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio)，請進行安裝。 選取**.NET 桌面開發**在 hello 工作負載頁面，然後按一下**安裝**。 在 hello 摘要，您可以看到**開發工具，.NET Framework 4 4.6**會自動為您選擇。 如果您已安裝 Visual Studio，您可以新增使用 Visual Studio 啟動器 hello hello.NET 工作負載。
2. 在 Visual Studio 中，按一下 [檔案] > [新增] > [專案]。
3. 在**範本** > **Visual C#**，選取**主控台應用程式 (.NET Framework)**，輸入*myDotnetProject* hello 名稱hello 專案中，選取 hello hello 專案位置，然後按一下**確定**。

## <a name="install-hello-package"></a>安裝 hello 套件

NuGet 封裝是 hello 最簡單方式 tooinstall hello 程式庫，您需要 toofinish 這些步驟。 tooget hello 程式庫，您需要在 Visual Studio 中，執行下列步驟：

1. 按一下 工具 > NuGet 套件管理員，然後按一下Package Manager Console。
2. Hello 主控台中，輸入下列命令：

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a>建立認證

在開始此步驟之前，請確定您有存取 tooan [Active Directory 服務主體](../../azure-resource-manager/resource-group-create-service-principal-portal.md)。 您也應該在稍後步驟中，記錄 hello 應用程式識別碼、 hello 驗證金鑰，以及您需要的 hello 租用戶識別碼。

### <a name="create-hello-authorization-file"></a>建立 hello 授權檔

1. 在 [方案總管] 中，於 [myDotnetProject] 上按一下滑鼠右鍵 > [新增] > [新增項目]，然後選取 [Visual C# 項目] 中的 [文字檔]。 名稱 hello 檔*azureauth.properties*，然後按一下**新增**。
2. 新增下列授權屬性：

    ```
    subscription=<subscription-id>
    client=<application-id>
    key=<authentication-key>
    tenant=<tenant-id>
    managementURI=https://management.core.windows.net/
    baseURL=https://management.azure.com/
    authURL=https://login.windows.net/
    graphURL=https://graph.windows.net/
    ```

    取代**&lt;訂用帳戶 id&gt;** 與您的訂用帳戶識別碼**&lt;應用程式識別碼&gt;**以 hello Active Directory 應用程式識別項， **&lt;驗證金鑰&gt;**與 hello 應用程式鍵，和**&lt;租用戶識別碼&gt;**與 hello 租用戶識別項。

3. 儲存 hello azureauth.properties 檔案。 
4. 在名為 AZURE_AUTH_LOCATION hello 完整路徑 tooauthorization 檔案所建立的 Windows 中設定環境變數。 例如，您可以使用下列 PowerShell 命令的 hello:

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a>建立 hello 管理用戶端

1. 開啟您所建立的 hello 專案 hello Program.cs 檔案，然後加入下列陳述式 toohello 現有陳述式，使用在 hello 檔案最上方：

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. toocreate hello 管理用戶端，新增此程式碼 toohello Main 方法：

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a>建立資源

### <a name="create-hello-resource-group"></a>建立 hello 資源群組

所有資源都必須包含在[資源群組](../../azure-resource-manager/resource-group-overview.md)中。

toospecify 值 hello 應用程式並建立 hello 資源群組，請加入這個程式碼 toohello Main 方法：

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a>建立 hello 可用性設定組

[可用性設定組](tutorial-availability-sets.md)方便您應用程式所使用的 toomaintain hello 虛擬機器。

toocreate hello 可用性組，請加入這個程式碼 toohello Main 方法：

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a>建立 hello 公用 IP 位址

A[公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)是需要的 toocommunicate 與 hello 虛擬機器。

toocreate hello 公用 IP 位址 hello 虛擬機器，加入此程式碼 toohello Main 方法：
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a>建立 hello 虛擬網路

虛擬機器必須在[虛擬網路](../../virtual-network/virtual-networks-overview.md)的子網路中。

toocreate 的子網路和虛擬網路，請加入這個程式碼 toohello Main 方法：

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a>建立 hello 網路介面

需要網路介面 toocommunicate hello 虛擬網路上的虛擬機器。

toocreate 網路介面，加入此程式碼 toohello Main 方法：

```
Console.WriteLine("Creating network interface...");
var networkInterface = azure.NetworkInterfaces.Define("myNIC")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetwork(network)
    .WithSubnet("mySubnet")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithExistingPrimaryPublicIPAddress(publicIPAddress)
    .Create();
 ```

### <a name="create-hello-virtual-machine"></a>建立 hello 的虛擬機器

現在，您會建立所有 hello 支援的資源，您可以建立虛擬機器。

toocreate hello 虛擬機器，加入此程式碼 toohello Main 方法：

```
Console.WriteLine("Creating virtual machine...");
azure.VirtualMachines.Define(vmName)
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .WithAdminUsername("azureuser")
    .WithAdminPassword("Azure12345678")
    .WithComputerName(vmName)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

> [!NOTE]
> 本教學課程中建立虛擬機器執行 hello Windows Server 作業系統版本。 toolearn 有關選取其他映像的詳細資訊請參閱[瀏覽並選取 Azure 虛擬機器映像使用 Windows PowerShell 與 hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
> 
>

如果您想 toouse 現有磁碟而非 marketplace 映像，請使用下列程式碼：

```
var managedDisk = azure.Disks.Define("myosdisk")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd")
    .WithSizeInGB(128)
    .WithSku(DiskSkuTypes.PremiumLRS)
    .Create();

azure.VirtualMachines.Define("myVM")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

## <a name="perform-management-tasks"></a>執行管理工作

在虛擬機器的 hello 生命週期，您可能想 toorun 管理工作，例如啟動、 停止或刪除虛擬機器。 此外，您可能想 toocreate 程式碼 tooautomate 重複或複雜工作。

當您以 hello VM 的任何項目需要 toodo 時，您會需要 tooget 它的執行個體：

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a>取得 hello VM 的相關資訊

tooget 資訊 hello 虛擬機器，加入此程式碼 toohello Main 方法：

```
Console.WriteLine("Getting information about hello virtual machine...");
Console.WriteLine("hardwareProfile");
Console.WriteLine("   vmSize: " + vm.Size);
Console.WriteLine("storageProfile");
Console.WriteLine("  imageReference");
Console.WriteLine("    publisher: " + vm.StorageProfile.ImageReference.Publisher);
Console.WriteLine("    offer: " + vm.StorageProfile.ImageReference.Offer);
Console.WriteLine("    sku: " + vm.StorageProfile.ImageReference.Sku);
Console.WriteLine("    version: " + vm.StorageProfile.ImageReference.Version);
Console.WriteLine("  osDisk");
Console.WriteLine("    osType: " + vm.StorageProfile.OsDisk.OsType);
Console.WriteLine("    name: " + vm.StorageProfile.OsDisk.Name);
Console.WriteLine("    createOption: " + vm.StorageProfile.OsDisk.CreateOption);
Console.WriteLine("    caching: " + vm.StorageProfile.OsDisk.Caching);
Console.WriteLine("osProfile");
Console.WriteLine("  computerName: " + vm.OSProfile.ComputerName);
Console.WriteLine("  adminUsername: " + vm.OSProfile.AdminUsername);
Console.WriteLine("  provisionVMAgent: " + vm.OSProfile.WindowsConfiguration.ProvisionVMAgent.Value);
Console.WriteLine("  enableAutomaticUpdates: " + vm.OSProfile.WindowsConfiguration.EnableAutomaticUpdates.Value);
Console.WriteLine("networkProfile");
foreach (string nicId in vm.NetworkInterfaceIds)
{
    Console.WriteLine("  networkInterface id: " + nicId);
}
Console.WriteLine("vmAgent");
Console.WriteLine("  vmAgentVersion" + vm.InstanceView.VmAgent.VmAgentVersion);
Console.WriteLine("    statuses");
foreach (InstanceViewStatus stat in vm.InstanceView.VmAgent.Statuses)
{
    Console.WriteLine("    code: " + stat.Code);
    Console.WriteLine("    level: " + stat.Level);
    Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
    Console.WriteLine("    message: " + stat.Message);
    Console.WriteLine("    time: " + stat.Time);
}
Console.WriteLine("disks");
foreach (DiskInstanceView disk in vm.InstanceView.Disks)
{
    Console.WriteLine("  name: " + disk.Name);
    Console.WriteLine("  statuses");
    foreach (InstanceViewStatus stat in disk.Statuses)
    {
        Console.WriteLine("    code: " + stat.Code);
        Console.WriteLine("    level: " + stat.Level);
        Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
        Console.WriteLine("    time: " + stat.Time);
    }
}
Console.WriteLine("VM general status");
Console.WriteLine("  provisioningStatus: " + vm.ProvisioningState);
Console.WriteLine("  id: " + vm.Id);
Console.WriteLine("  name: " + vm.Name);
Console.WriteLine("  type: " + vm.Type);
Console.WriteLine("  location: " + vm.Region);
Console.WriteLine("VM instance status");
foreach (InstanceViewStatus stat in vm.InstanceView.Statuses)
{
    Console.WriteLine("  code: " + stat.Code);
    Console.WriteLine("  level: " + stat.Level);
    Console.WriteLine("  displayStatus: " + stat.DisplayStatus);
}
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="stop-hello-vm"></a>停止 hello VM

您可以停止虛擬機器並保留其所有設定，但繼續 toobe 支付，或您可以停止虛擬機器和解除配置。 當解除配置虛擬機器時，與其相關聯的所有資源也都會解除配置且其計費會結束。

toostop hello 虛擬機器，而不取消配置，加入此程式碼 toohello Main 方法：

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

如果您想 toodeallocate hello 虛擬機器，變更 hello 關閉呼叫 toothis 程式碼：

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a>啟動 VM hello

toostart hello 虛擬機器，加入此程式碼 toohello Main 方法：

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a>調整大小 hello VM

決定虛擬機器的大小時，應該考慮部署的許多層面。 如需詳細資訊，請參閱 [VM 大小](sizes.md)。  

toochange hello 虛擬機器大小的加入此程式碼 toohello Main 方法：

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>新增資料磁碟 toohello VM

tooadd 資料磁碟 toohello 虛擬機器，加入此程式碼 toohello Main 方法 tooadd 韓文 0 和 ReadWrite 快取類型的 LUN 的大小是 2 GB 的資料磁碟：

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a>刪除資源

因為您負責 Azure 中使用的資源，但它永遠是很好的作法 toodelete 資源不再需要的。 如果您想 toodelete hello 虛擬機器，而且所有 hello 支援的資源，您都有 toodo 是刪除 hello 資源群組。

toodelete hello 資源群組中，加入此程式碼 toohello Main 方法：

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>執行 hello 應用程式

它應該完全從開始 toofinish 此主控台應用程式 toorun 大約五分鐘。 

1. toorun hello 主控台應用程式中，按一下 **啟動**。

2. 再按**Enter** toostart 刪除資源，您可能需要幾分鐘的時間 tooverify hello 建立 hello 資源 hello Azure 入口網站中。 按一下 hello 部署狀態 toosee hello 部署資訊。

## <a name="next-steps"></a>後續步驟
* 使用範本 toocreate 的虛擬機器使用運用中的 hello 資訊[部署 Azure 虛擬機器中使用 C# 和 Resource Manager 範本](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
* 深入了解使用 hello [Azure libraries for.NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet)。

