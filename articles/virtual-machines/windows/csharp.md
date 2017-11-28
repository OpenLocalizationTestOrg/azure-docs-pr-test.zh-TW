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
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a><span data-ttu-id="64953-103">在 Azure 中使用 C# 建立並管理 Windows VM</span><span class="sxs-lookup"><span data-stu-id="64953-103">Create and manage Windows VMs in Azure using C#</span></span> #

<span data-ttu-id="64953-104">[Azure 虛擬機器](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) 需要數個支援的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="64953-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="64953-105">本文涵蓋使用 C# 建立、管理和刪除 VM 資源。</span><span class="sxs-lookup"><span data-stu-id="64953-105">This article covers creating, managing, and deleting VM resources using C#.</span></span> <span data-ttu-id="64953-106">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="64953-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="64953-107">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="64953-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="64953-108">安裝 hello 套件</span><span class="sxs-lookup"><span data-stu-id="64953-108">Install hello package</span></span>
> * <span data-ttu-id="64953-109">建立認證</span><span class="sxs-lookup"><span data-stu-id="64953-109">Create credentials</span></span>
> * <span data-ttu-id="64953-110">建立資源</span><span class="sxs-lookup"><span data-stu-id="64953-110">Create resources</span></span>
> * <span data-ttu-id="64953-111">執行管理工作</span><span class="sxs-lookup"><span data-stu-id="64953-111">Perform management tasks</span></span>
> * <span data-ttu-id="64953-112">刪除資源</span><span class="sxs-lookup"><span data-stu-id="64953-112">Delete resources</span></span>
> * <span data-ttu-id="64953-113">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="64953-113">Run hello application</span></span>

<span data-ttu-id="64953-114">它會採用約 20 分鐘 toodo 這些步驟。</span><span class="sxs-lookup"><span data-stu-id="64953-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="64953-115">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="64953-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="64953-116">如果您尚未安裝 [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio)，請進行安裝。</span><span class="sxs-lookup"><span data-stu-id="64953-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="64953-117">選取**.NET 桌面開發**在 hello 工作負載頁面，然後按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="64953-117">Select **.NET desktop development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="64953-118">在 hello 摘要，您可以看到**開發工具，.NET Framework 4 4.6**會自動為您選擇。</span><span class="sxs-lookup"><span data-stu-id="64953-118">In hello summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="64953-119">如果您已安裝 Visual Studio，您可以新增使用 Visual Studio 啟動器 hello hello.NET 工作負載。</span><span class="sxs-lookup"><span data-stu-id="64953-119">If you have already installed Visual Studio, you can add hello .NET workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="64953-120">在 Visual Studio 中，按一下 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="64953-120">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="64953-121">在**範本** > **Visual C#**，選取**主控台應用程式 (.NET Framework)**，輸入*myDotnetProject* hello 名稱hello 專案中，選取 hello hello 專案位置，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="64953-121">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-hello-package"></a><span data-ttu-id="64953-122">安裝 hello 套件</span><span class="sxs-lookup"><span data-stu-id="64953-122">Install hello package</span></span>

<span data-ttu-id="64953-123">NuGet 封裝是 hello 最簡單方式 tooinstall hello 程式庫，您需要 toofinish 這些步驟。</span><span class="sxs-lookup"><span data-stu-id="64953-123">NuGet packages are hello easiest way tooinstall hello libraries that you need toofinish these steps.</span></span> <span data-ttu-id="64953-124">tooget hello 程式庫，您需要在 Visual Studio 中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="64953-124">tooget hello libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="64953-125">按一下 工具 > NuGet 套件管理員，然後按一下Package Manager Console。</span><span class="sxs-lookup"><span data-stu-id="64953-125">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="64953-126">Hello 主控台中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="64953-126">Type this command in hello console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a><span data-ttu-id="64953-127">建立認證</span><span class="sxs-lookup"><span data-stu-id="64953-127">Create credentials</span></span>

<span data-ttu-id="64953-128">在開始此步驟之前，請確定您有存取 tooan [Active Directory 服務主體](../../azure-resource-manager/resource-group-create-service-principal-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="64953-128">Before you start this step, make sure that you have access tooan [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="64953-129">您也應該在稍後步驟中，記錄 hello 應用程式識別碼、 hello 驗證金鑰，以及您需要的 hello 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="64953-129">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="64953-130">建立 hello 授權檔</span><span class="sxs-lookup"><span data-stu-id="64953-130">Create hello authorization file</span></span>

1. <span data-ttu-id="64953-131">在 [方案總管] 中，於 [myDotnetProject] 上按一下滑鼠右鍵 > [新增] > [新增項目]，然後選取 [Visual C# 項目] 中的 [文字檔]。</span><span class="sxs-lookup"><span data-stu-id="64953-131">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="64953-132">名稱 hello 檔*azureauth.properties*，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="64953-132">Name hello file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="64953-133">新增下列授權屬性：</span><span class="sxs-lookup"><span data-stu-id="64953-133">Add these authorization properties:</span></span>

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

    <span data-ttu-id="64953-134">取代**&lt;訂用帳戶 id&gt;** 與您的訂用帳戶識別碼**&lt;應用程式識別碼&gt;**以 hello Active Directory 應用程式識別項， **&lt;驗證金鑰&gt;**與 hello 應用程式鍵，和**&lt;租用戶識別碼&gt;**與 hello 租用戶識別項。</span><span class="sxs-lookup"><span data-stu-id="64953-134">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

3. <span data-ttu-id="64953-135">儲存 hello azureauth.properties 檔案。</span><span class="sxs-lookup"><span data-stu-id="64953-135">Save hello azureauth.properties file.</span></span> 
4. <span data-ttu-id="64953-136">在名為 AZURE_AUTH_LOCATION hello 完整路徑 tooauthorization 檔案所建立的 Windows 中設定環境變數。</span><span class="sxs-lookup"><span data-stu-id="64953-136">Set an environment variable in Windows named AZURE_AUTH_LOCATION with hello full path tooauthorization file that you created.</span></span> <span data-ttu-id="64953-137">例如，您可以使用下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="64953-137">For example, hello following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a><span data-ttu-id="64953-138">建立 hello 管理用戶端</span><span class="sxs-lookup"><span data-stu-id="64953-138">Create hello management client</span></span>

1. <span data-ttu-id="64953-139">開啟您所建立的 hello 專案 hello Program.cs 檔案，然後加入下列陳述式 toohello 現有陳述式，使用在 hello 檔案最上方：</span><span class="sxs-lookup"><span data-stu-id="64953-139">Open hello Program.cs file for hello project that you created, and then add these using statements toohello existing statements at top of hello file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. <span data-ttu-id="64953-140">toocreate hello 管理用戶端，新增此程式碼 toohello Main 方法：</span><span class="sxs-lookup"><span data-stu-id="64953-140">toocreate hello management client, add this code toohello Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a><span data-ttu-id="64953-141">建立資源</span><span class="sxs-lookup"><span data-stu-id="64953-141">Create resources</span></span>

### <a name="create-hello-resource-group"></a><span data-ttu-id="64953-142">建立 hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="64953-142">Create hello resource group</span></span>

<span data-ttu-id="64953-143">所有資源都必須包含在[資源群組](../../azure-resource-manager/resource-group-overview.md)中。</span><span class="sxs-lookup"><span data-stu-id="64953-143">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="64953-144">toospecify 值 hello 應用程式並建立 hello 資源群組，請加入這個程式碼 toohello Main 方法：</span><span class="sxs-lookup"><span data-stu-id="64953-144">toospecify values for hello application and create hello resource group, add this code toohello Main method:</span></span>

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a><span data-ttu-id="64953-145">建立 hello 可用性設定組</span><span class="sxs-lookup"><span data-stu-id="64953-145">Create hello availability set</span></span>

<span data-ttu-id="64953-146">[可用性設定組](tutorial-availability-sets.md)方便您應用程式所使用的 toomaintain hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="64953-146">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

<span data-ttu-id="64953-147">toocreate hello 可用性組，請加入這個程式碼 toohello Main 方法：</span><span class="sxs-lookup"><span data-stu-id="64953-147">toocreate hello availability set, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="64953-148">建立 hello 公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="64953-148">Create hello public IP address</span></span>

<span data-ttu-id="64953-149">A[公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)是需要的 toocommunicate 與 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="64953-149">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

<span data-ttu-id="64953-150">toocreate hello 公用 IP 位址 hello 虛擬機器，加入此程式碼 toohello Main 方法：</span><span class="sxs-lookup"><span data-stu-id="64953-150">toocreate hello public IP address for hello virtual machine, add this code toohello Main method:</span></span>
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a><span data-ttu-id="64953-151">建立 hello 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="64953-151">Create hello virtual network</span></span>

<span data-ttu-id="64953-152">虛擬機器必須在[虛擬網路](../../virtual-network/virtual-networks-overview.md)的子網路中。</span><span class="sxs-lookup"><span data-stu-id="64953-152">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="64953-153">toocreate 的子網路和虛擬網路，請加入這個程式碼 toohello Main 方法：</span><span class="sxs-lookup"><span data-stu-id="64953-153">toocreate a subnet and a virtual network, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a><span data-ttu-id="64953-154">建立 hello 網路介面</span><span class="sxs-lookup"><span data-stu-id="64953-154">Create hello network interface</span></span>

<span data-ttu-id="64953-155">需要網路介面 toocommunicate hello 虛擬網路上的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="64953-155">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

<span data-ttu-id="64953-156">toocreate 網路介面，加入此程式碼 toohello Main 方法：</span><span class="sxs-lookup"><span data-stu-id="64953-156">toocreate a network interface, add this code toohello Main method:</span></span>

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

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="64953-157">建立 hello 的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="64953-157">Create hello virtual machine</span></span>

<span data-ttu-id="64953-158">現在，您會建立所有 hello 支援的資源，您可以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="64953-158">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="64953-159">toocreate hello 虛擬機器，加入此程式碼 toohello Main 方法：</span><span class="sxs-lookup"><span data-stu-id="64953-159">toocreate hello virtual machine, add this code toohello Main method:</span></span>

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
> <span data-ttu-id="64953-160">本教學課程中建立虛擬機器執行 hello Windows Server 作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="64953-160">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="64953-161">toolearn 有關選取其他映像的詳細資訊請參閱[瀏覽並選取 Azure 虛擬機器映像使用 Windows PowerShell 與 hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="64953-161">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="64953-162">如果您想 toouse 現有磁碟而非 marketplace 映像，請使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="64953-162">If you want toouse an existing disk instead of a marketplace image, use this code:</span></span>

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

## <a name="perform-management-tasks"></a><span data-ttu-id="64953-163">執行管理工作</span><span class="sxs-lookup"><span data-stu-id="64953-163">Perform management tasks</span></span>

<span data-ttu-id="64953-164">在虛擬機器的 hello 生命週期，您可能想 toorun 管理工作，例如啟動、 停止或刪除虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="64953-164">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="64953-165">此外，您可能想 toocreate 程式碼 tooautomate 重複或複雜工作。</span><span class="sxs-lookup"><span data-stu-id="64953-165">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

<span data-ttu-id="64953-166">當您以 hello VM 的任何項目需要 toodo 時，您會需要 tooget 它的執行個體：</span><span class="sxs-lookup"><span data-stu-id="64953-166">When you need toodo anything with hello VM, you need tooget an instance of it:</span></span>

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="64953-167">取得 hello VM 的相關資訊</span><span class="sxs-lookup"><span data-stu-id="64953-167">Get information about hello VM</span></span>

<span data-ttu-id="64953-168">tooget 資訊 hello 虛擬機器，加入此程式碼 toohello Main 方法：</span><span class="sxs-lookup"><span data-stu-id="64953-168">tooget information about hello virtual machine, add this code toohello Main method:</span></span>

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

### <a name="stop-hello-vm"></a><span data-ttu-id="64953-169">停止 hello VM</span><span class="sxs-lookup"><span data-stu-id="64953-169">Stop hello VM</span></span>

<span data-ttu-id="64953-170">您可以停止虛擬機器並保留其所有設定，但繼續 toobe 支付，或您可以停止虛擬機器和解除配置。</span><span class="sxs-lookup"><span data-stu-id="64953-170">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="64953-171">當解除配置虛擬機器時，與其相關聯的所有資源也都會解除配置且其計費會結束。</span><span class="sxs-lookup"><span data-stu-id="64953-171">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="64953-172">toostop hello 虛擬機器，而不取消配置，加入此程式碼 toohello Main 方法：</span><span class="sxs-lookup"><span data-stu-id="64953-172">toostop hello virtual machine without deallocating it, add this code toohello Main method:</span></span>

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

<span data-ttu-id="64953-173">如果您想 toodeallocate hello 虛擬機器，變更 hello 關閉呼叫 toothis 程式碼：</span><span class="sxs-lookup"><span data-stu-id="64953-173">If you want toodeallocate hello virtual machine, change hello PowerOff call toothis code:</span></span>

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a><span data-ttu-id="64953-174">啟動 VM hello</span><span class="sxs-lookup"><span data-stu-id="64953-174">Start hello VM</span></span>

<span data-ttu-id="64953-175">toostart hello 虛擬機器，加入此程式碼 toohello Main 方法：</span><span class="sxs-lookup"><span data-stu-id="64953-175">toostart hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a><span data-ttu-id="64953-176">調整大小 hello VM</span><span class="sxs-lookup"><span data-stu-id="64953-176">Resize hello VM</span></span>

<span data-ttu-id="64953-177">決定虛擬機器的大小時，應該考慮部署的許多層面。</span><span class="sxs-lookup"><span data-stu-id="64953-177">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="64953-178">如需詳細資訊，請參閱 [VM 大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="64953-178">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="64953-179">toochange hello 虛擬機器大小的加入此程式碼 toohello Main 方法：</span><span class="sxs-lookup"><span data-stu-id="64953-179">toochange size of hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="64953-180">新增資料磁碟 toohello VM</span><span class="sxs-lookup"><span data-stu-id="64953-180">Add a data disk toohello VM</span></span>

<span data-ttu-id="64953-181">tooadd 資料磁碟 toohello 虛擬機器，加入此程式碼 toohello Main 方法 tooadd 韓文 0 和 ReadWrite 快取類型的 LUN 的大小是 2 GB 的資料磁碟：</span><span class="sxs-lookup"><span data-stu-id="64953-181">tooadd a data disk toohello virtual machine, add this code toohello Main method tooadd a data disk that is 2 GB in size, han a LUN of 0 and a caching type of ReadWrite:</span></span>

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a><span data-ttu-id="64953-182">刪除資源</span><span class="sxs-lookup"><span data-stu-id="64953-182">Delete resources</span></span>

<span data-ttu-id="64953-183">因為您負責 Azure 中使用的資源，但它永遠是很好的作法 toodelete 資源不再需要的。</span><span class="sxs-lookup"><span data-stu-id="64953-183">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="64953-184">如果您想 toodelete hello 虛擬機器，而且所有 hello 支援的資源，您都有 toodo 是刪除 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="64953-184">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

<span data-ttu-id="64953-185">toodelete hello 資源群組中，加入此程式碼 toohello Main 方法：</span><span class="sxs-lookup"><span data-stu-id="64953-185">toodelete hello resource group, add this code toohello Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a><span data-ttu-id="64953-186">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="64953-186">Run hello application</span></span>

<span data-ttu-id="64953-187">它應該完全從開始 toofinish 此主控台應用程式 toorun 大約五分鐘。</span><span class="sxs-lookup"><span data-stu-id="64953-187">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> 

1. <span data-ttu-id="64953-188">toorun hello 主控台應用程式中，按一下 **啟動**。</span><span class="sxs-lookup"><span data-stu-id="64953-188">toorun hello console application, click **Start**.</span></span>

2. <span data-ttu-id="64953-189">再按**Enter** toostart 刪除資源，您可能需要幾分鐘的時間 tooverify hello 建立 hello 資源 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="64953-189">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="64953-190">按一下 hello 部署狀態 toosee hello 部署資訊。</span><span class="sxs-lookup"><span data-stu-id="64953-190">Click hello deployment status toosee information about hello deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64953-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64953-191">Next steps</span></span>
* <span data-ttu-id="64953-192">使用範本 toocreate 的虛擬機器使用運用中的 hello 資訊[部署 Azure 虛擬機器中使用 C# 和 Resource Manager 範本](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="64953-192">Take advantage of using a template toocreate a virtual machine by using hello information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="64953-193">深入了解使用 hello [Azure libraries for.NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="64953-193">Learn more about using hello [Azure libraries for .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span></span>

