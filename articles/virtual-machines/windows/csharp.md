---
title: "使用 C# 來建立和管理 Azure 虛擬機器 | Microsoft Docs"
description: "使用 C# 和 Azure Resource Manager 來部署 Azure 虛擬機器及所有支援它的資源。"
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
ms.openlocfilehash: 5d9021c2f65b70e36d5ea82992c9fb9d2d6d394a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a><span data-ttu-id="45162-103">在 Azure 中使用 C# 建立並管理 Windows VM</span><span class="sxs-lookup"><span data-stu-id="45162-103">Create and manage Windows VMs in Azure using C#</span></span> #

<span data-ttu-id="45162-104">[Azure 虛擬機器](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) 需要數個支援的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="45162-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="45162-105">本文涵蓋使用 C# 建立、管理和刪除 VM 資源。</span><span class="sxs-lookup"><span data-stu-id="45162-105">This article covers creating, managing, and deleting VM resources using C#.</span></span> <span data-ttu-id="45162-106">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="45162-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="45162-107">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="45162-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="45162-108">安裝套件</span><span class="sxs-lookup"><span data-stu-id="45162-108">Install the package</span></span>
> * <span data-ttu-id="45162-109">建立認證</span><span class="sxs-lookup"><span data-stu-id="45162-109">Create credentials</span></span>
> * <span data-ttu-id="45162-110">建立資源</span><span class="sxs-lookup"><span data-stu-id="45162-110">Create resources</span></span>
> * <span data-ttu-id="45162-111">執行管理工作</span><span class="sxs-lookup"><span data-stu-id="45162-111">Perform management tasks</span></span>
> * <span data-ttu-id="45162-112">刪除資源</span><span class="sxs-lookup"><span data-stu-id="45162-112">Delete resources</span></span>
> * <span data-ttu-id="45162-113">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="45162-113">Run the application</span></span>

<span data-ttu-id="45162-114">執行這些步驟大約需要 20 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="45162-114">It takes about 20 minutes to do these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="45162-115">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="45162-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="45162-116">如果您尚未安裝 [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio)，請進行安裝。</span><span class="sxs-lookup"><span data-stu-id="45162-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="45162-117">在 [工作負載] 分頁上選取 [.NET 桌面開發]，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="45162-117">Select **.NET desktop development** on the Workloads page, and then click **Install**.</span></span> <span data-ttu-id="45162-118">在摘要中，您可以看到系統自動為您選取 [NET Framework 4 – 4.6 開發工具]。</span><span class="sxs-lookup"><span data-stu-id="45162-118">In the summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="45162-119">如果您已安裝 Visual Studio，您可以使用 Visual Studio Launcher 新增 .NET 工作負載。</span><span class="sxs-lookup"><span data-stu-id="45162-119">If you have already installed Visual Studio, you can add the .NET workload using the Visual Studio Launcher.</span></span>
2. <span data-ttu-id="45162-120">在 Visual Studio 中，按一下 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="45162-120">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="45162-121">在 [範本] > [Visual C#] 中，選取 [主控台應用程式 (.NET Framework)]，針對專案名稱輸入 myDotnetProject，選取專案的位置，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="45162-121">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for the name of the project, select the location of the project, and then click **OK**.</span></span>

## <a name="install-the-package"></a><span data-ttu-id="45162-122">安裝套件</span><span class="sxs-lookup"><span data-stu-id="45162-122">Install the package</span></span>

<span data-ttu-id="45162-123">NuGet 套件是安裝完成這些步驟所需之程式庫的最簡單方式。</span><span class="sxs-lookup"><span data-stu-id="45162-123">NuGet packages are the easiest way to install the libraries that you need to finish these steps.</span></span> <span data-ttu-id="45162-124">若要取得在 Visual Studio 中所需要的程式庫，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="45162-124">To get the libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="45162-125">按一下 [工具] > [NuGet 套件管理員]，然後按一下 [Package Manager Console]。</span><span class="sxs-lookup"><span data-stu-id="45162-125">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="45162-126">在主控台中輸入以下命令：</span><span class="sxs-lookup"><span data-stu-id="45162-126">Type this command in the console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a><span data-ttu-id="45162-127">建立認證</span><span class="sxs-lookup"><span data-stu-id="45162-127">Create credentials</span></span>

<span data-ttu-id="45162-128">在您開始此步驟之前，請確定您可以存取 [Active Directory 服務主體](../../azure-resource-manager/resource-group-create-service-principal-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="45162-128">Before you start this step, make sure that you have access to an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="45162-129">您也應該記錄應用程式識別碼、驗證金鑰以及租用戶識別碼，您在稍後的步驟會需要這些項目。</span><span class="sxs-lookup"><span data-stu-id="45162-129">You should also record the application ID, the authentication key, and the tenant ID that you need in a later step.</span></span>

### <a name="create-the-authorization-file"></a><span data-ttu-id="45162-130">建立授權檔</span><span class="sxs-lookup"><span data-stu-id="45162-130">Create the authorization file</span></span>

1. <span data-ttu-id="45162-131">在 [方案總管] 中，於 [myDotnetProject] 上按一下滑鼠右鍵 > [新增] > [新增項目]，然後選取 [Visual C# 項目] 中的 [文字檔]。</span><span class="sxs-lookup"><span data-stu-id="45162-131">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="45162-132">將檔案命名為 *azureauth.properties*，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="45162-132">Name the file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="45162-133">新增下列授權屬性：</span><span class="sxs-lookup"><span data-stu-id="45162-133">Add these authorization properties:</span></span>

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

    <span data-ttu-id="45162-134">以您的訂用帳戶 ID 取代 **&lt;subscription-id&gt;**、以 Active Directory 應用程式識別碼取代 **&lt;application-id&gt;**、以應用程式金鑰取代 **&lt;authentication-key&gt;**，以及以租用戶識別碼取代 **&lt;tenant-id&gt;**。</span><span class="sxs-lookup"><span data-stu-id="45162-134">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with the Active Directory application identifier, **&lt;authentication-key&gt;** with the application key, and **&lt;tenant-id&gt;** with the tenant identifier.</span></span>

3. <span data-ttu-id="45162-135">儲存 azureauth.properties 檔案。</span><span class="sxs-lookup"><span data-stu-id="45162-135">Save the azureauth.properties file.</span></span> 
4. <span data-ttu-id="45162-136">在 Windows 中名為 AZURE_AUTH_LOCATION 的環境變數上，設定您所建立之授權檔的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="45162-136">Set an environment variable in Windows named AZURE_AUTH_LOCATION with the full path to authorization file that you created.</span></span> <span data-ttu-id="45162-137">例如，可以使用下列 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="45162-137">For example, the following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-the-management-client"></a><span data-ttu-id="45162-138">建立管理用戶端</span><span class="sxs-lookup"><span data-stu-id="45162-138">Create the management client</span></span>

1. <span data-ttu-id="45162-139">開啟您建立之專案的 Program.cs 檔案，然後將這些 using 陳述式新增至檔案頂端的現有陳述式：</span><span class="sxs-lookup"><span data-stu-id="45162-139">Open the Program.cs file for the project that you created, and then add these using statements to the existing statements at top of the file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. <span data-ttu-id="45162-140">若要建立管理用戶端，請將以下程式碼新增到 Main 方法：</span><span class="sxs-lookup"><span data-stu-id="45162-140">To create the management client, add this code to the Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a><span data-ttu-id="45162-141">建立資源</span><span class="sxs-lookup"><span data-stu-id="45162-141">Create resources</span></span>

### <a name="create-the-resource-group"></a><span data-ttu-id="45162-142">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="45162-142">Create the resource group</span></span>

<span data-ttu-id="45162-143">所有資源都必須包含在[資源群組](../../azure-resource-manager/resource-group-overview.md)中。</span><span class="sxs-lookup"><span data-stu-id="45162-143">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="45162-144">若要指定應用程式的值並建立資源群組，請將以下程式碼新增到 Main 方法：</span><span class="sxs-lookup"><span data-stu-id="45162-144">To specify values for the application and create the resource group, add this code to the Main method:</span></span>

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-the-availability-set"></a><span data-ttu-id="45162-145">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="45162-145">Create the availability set</span></span>

<span data-ttu-id="45162-146">維護您應用程式所使用的虛擬機器時，使用[可用性設定組](tutorial-availability-sets.md)可讓您更加輕鬆。</span><span class="sxs-lookup"><span data-stu-id="45162-146">[Availability sets](tutorial-availability-sets.md) make it easier for you to maintain the virtual machines used by your application.</span></span>

<span data-ttu-id="45162-147">若要建立可用性設定組，請將以下程式碼新增到 Main 方法：</span><span class="sxs-lookup"><span data-stu-id="45162-147">To create the availability set, add this code to the Main method:</span></span>

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-the-public-ip-address"></a><span data-ttu-id="45162-148">建立公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="45162-148">Create the public IP address</span></span>

<span data-ttu-id="45162-149">必須要有[公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)才能與虛擬機器進行通訊。</span><span class="sxs-lookup"><span data-stu-id="45162-149">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed to communicate with the virtual machine.</span></span>

<span data-ttu-id="45162-150">若要為虛擬機器建立公用 IP 位址，請將以下程式碼新增到 Main 方法：</span><span class="sxs-lookup"><span data-stu-id="45162-150">To create the public IP address for the virtual machine, add this code to the Main method:</span></span>
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-the-virtual-network"></a><span data-ttu-id="45162-151">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="45162-151">Create the virtual network</span></span>

<span data-ttu-id="45162-152">虛擬機器必須在[虛擬網路](../../virtual-network/virtual-networks-overview.md)的子網路中。</span><span class="sxs-lookup"><span data-stu-id="45162-152">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="45162-153">若要建立子網路和虛擬網路，請將以下程式碼新增到 Main 方法：</span><span class="sxs-lookup"><span data-stu-id="45162-153">To create a subnet and a virtual network, add this code to the Main method:</span></span>

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-the-network-interface"></a><span data-ttu-id="45162-154">建立網路介面</span><span class="sxs-lookup"><span data-stu-id="45162-154">Create the network interface</span></span>

<span data-ttu-id="45162-155">虛擬機器需要網路介面以在虛擬網路上通訊。</span><span class="sxs-lookup"><span data-stu-id="45162-155">A virtual machine needs a network interface to communicate on the virtual network.</span></span>

<span data-ttu-id="45162-156">若要建立網路介面，請將以下程式碼新增到 Main 方法：</span><span class="sxs-lookup"><span data-stu-id="45162-156">To create a network interface, add this code to the Main method:</span></span>

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

### <a name="create-the-virtual-machine"></a><span data-ttu-id="45162-157">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="45162-157">Create the virtual machine</span></span>

<span data-ttu-id="45162-158">既然您已經建立所有支援的資源，您可以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="45162-158">Now that you created all the supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="45162-159">若要建立虛擬機器，請將以下程式碼新增到 Main 方法：</span><span class="sxs-lookup"><span data-stu-id="45162-159">To create the virtual machine, add this code to the Main method:</span></span>

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
> <span data-ttu-id="45162-160">本教學課程中會建立執行 Windows Server 作業系統版本的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="45162-160">This tutorial creates a virtual machine running a version of the Windows Server operating system.</span></span> <span data-ttu-id="45162-161">若要深入了解如何選取其他映像，請參閱 [使用 Windows PowerShell 和 Azure CLI 來瀏覽和選取 Azure 虛擬機器映像](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="45162-161">To learn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and the Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="45162-162">如果您想要使用現有的磁碟而不使用市集映像，請使用以下程式碼：</span><span class="sxs-lookup"><span data-stu-id="45162-162">If you want to use an existing disk instead of a marketplace image, use this code:</span></span>

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

## <a name="perform-management-tasks"></a><span data-ttu-id="45162-163">執行管理工作</span><span class="sxs-lookup"><span data-stu-id="45162-163">Perform management tasks</span></span>

<span data-ttu-id="45162-164">在虛擬機器的生命週期內，您可以執行一些管理工作，例如啟動、停止或刪除虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="45162-164">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="45162-165">此外，您可以建立程式碼來自動執行重複或複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="45162-165">Additionally, you may want to create code to automate repetitive or complex tasks.</span></span>

<span data-ttu-id="45162-166">當您需要使用 VM 來執行任何操作時，就必須取得其執行個體：</span><span class="sxs-lookup"><span data-stu-id="45162-166">When you need to do anything with the VM, you need to get an instance of it:</span></span>

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-the-vm"></a><span data-ttu-id="45162-167">取得 VM 的相關資訊</span><span class="sxs-lookup"><span data-stu-id="45162-167">Get information about the VM</span></span>

<span data-ttu-id="45162-168">若要取得虛擬機器的相關資訊，請將以下程式碼新增到 Main 方法：</span><span class="sxs-lookup"><span data-stu-id="45162-168">To get information about the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Getting information about the virtual machine...");
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
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

### <a name="stop-the-vm"></a><span data-ttu-id="45162-169">停止 VM</span><span class="sxs-lookup"><span data-stu-id="45162-169">Stop the VM</span></span>

<span data-ttu-id="45162-170">您可以停止虛擬機器並保留其所有的設定，但仍繼續計費，或您可以停止虛擬機器並將其解除配置。</span><span class="sxs-lookup"><span data-stu-id="45162-170">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="45162-171">當解除配置虛擬機器時，與其相關聯的所有資源也都會解除配置且其計費會結束。</span><span class="sxs-lookup"><span data-stu-id="45162-171">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="45162-172">若要停止虛擬機器而不解除配置，請將以下程式碼新增到 Main 方法：</span><span class="sxs-lookup"><span data-stu-id="45162-172">To stop the virtual machine without deallocating it, add this code to the Main method:</span></span>

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

<span data-ttu-id="45162-173">如果您想要解除配置虛擬機器，請將 PowerOff 呼叫變更為下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="45162-173">If you want to deallocate the virtual machine, change the PowerOff call to this code:</span></span>

```
vm.Deallocate();
```

### <a name="start-the-vm"></a><span data-ttu-id="45162-174">啟動 VM</span><span class="sxs-lookup"><span data-stu-id="45162-174">Start the VM</span></span>

<span data-ttu-id="45162-175">若要啟動虛擬機器，請將以下程式碼新增到 Main 方法：</span><span class="sxs-lookup"><span data-stu-id="45162-175">To start the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

### <a name="resize-the-vm"></a><span data-ttu-id="45162-176">調整 VM 的大小</span><span class="sxs-lookup"><span data-stu-id="45162-176">Resize the VM</span></span>

<span data-ttu-id="45162-177">決定虛擬機器的大小時，應該考慮部署的許多層面。</span><span class="sxs-lookup"><span data-stu-id="45162-177">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="45162-178">如需詳細資訊，請參閱 [VM 大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="45162-178">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="45162-179">若要變更虛擬機器的大小，請將以下程式碼新增到 Main 方法：</span><span class="sxs-lookup"><span data-stu-id="45162-179">To change size of the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-to-the-vm"></a><span data-ttu-id="45162-180">將資料磁碟新增至 VM</span><span class="sxs-lookup"><span data-stu-id="45162-180">Add a data disk to the VM</span></span>

<span data-ttu-id="45162-181">若要將資料磁碟新增到虛擬機器，請將以下程式碼新增到 Main 方法，以新增一個大小為 2 GB、LUN 為 0 且快取類型為 ReadWrite 的資料磁碟：</span><span class="sxs-lookup"><span data-stu-id="45162-181">To add a data disk to the virtual machine, add this code to the Main method to add a data disk that is 2 GB in size, han a LUN of 0 and a caching type of ReadWrite:</span></span>

```
Console.WriteLine("Adding data disk to vm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter to delete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a><span data-ttu-id="45162-182">刪除資源</span><span class="sxs-lookup"><span data-stu-id="45162-182">Delete resources</span></span>

<span data-ttu-id="45162-183">由於您需要為在 Azure 中使用的資源付費，因此刪除不再需要的資源一律是理想的做法。</span><span class="sxs-lookup"><span data-stu-id="45162-183">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="45162-184">如果您想要刪除虛擬機器及所有支援的資源，您只需要刪除資源群組。</span><span class="sxs-lookup"><span data-stu-id="45162-184">If you want to delete the virtual machines and all the supporting resources, all you have to do is delete the resource group.</span></span>

<span data-ttu-id="45162-185">若要刪除資源群組，請將以下程式碼新增到 Main 方法：</span><span class="sxs-lookup"><span data-stu-id="45162-185">To delete the resource group, add this code to the Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-the-application"></a><span data-ttu-id="45162-186">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="45162-186">Run the application</span></span>

<span data-ttu-id="45162-187">此主控台應用程式從開始到完成的完整執行應該需要五分鐘左右。</span><span class="sxs-lookup"><span data-stu-id="45162-187">It should take about five minutes for this console application to run completely from start to finish.</span></span> 

1. <span data-ttu-id="45162-188">若要執行主控台應用程式，請按一下 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="45162-188">To run the console application, click **Start**.</span></span>

2. <span data-ttu-id="45162-189">在您按 **Enter** 以開始刪除資源之前，可以先花幾分鐘的時間來確認 Azure 入口網站中的資源建立情況。</span><span class="sxs-lookup"><span data-stu-id="45162-189">Before you press **Enter** to start deleting resources, you could take a few minutes to verify the creation of the resources in the Azure portal.</span></span> <span data-ttu-id="45162-190">請按一下部署狀態來查看該項部署的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="45162-190">Click the deployment status to see information about the deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45162-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="45162-191">Next steps</span></span>
* <span data-ttu-id="45162-192">使用 [利用 C# 和 Resource Manager 範本來部署 Azure 虛擬機器](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中的資訊，以利用範本來建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="45162-192">Take advantage of using a template to create a virtual machine by using the information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="45162-193">深入了解關於使用 [Azure Libraries for .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="45162-193">Learn more about using the [Azure libraries for .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span></span>

