---
title: "使用 JAVA 來建立和管理 Azure 虛擬機器 | Microsoft Docs"
description: "使用 JAVA 和 Azure Resource Manager 來部署虛擬機器及其所有支援的資源。"
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: b9e739a07c5863577285fb3a221b372b385c6762
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a><span data-ttu-id="a933a-103">在 Azure 中使用 JAVA 建立並管理 Windows VM</span><span class="sxs-lookup"><span data-stu-id="a933a-103">Create and manage Windows VMs in Azure using Java</span></span>

<span data-ttu-id="a933a-104">[Azure 虛擬機器](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) 需要數個支援的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="a933a-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="a933a-105">本文涵蓋使用 JAVA 建立、管理和刪除 VM 資源。</span><span class="sxs-lookup"><span data-stu-id="a933a-105">This article covers creating, managing, and deleting VM resources using Java.</span></span> <span data-ttu-id="a933a-106">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="a933a-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a933a-107">建立 Maven 專案</span><span class="sxs-lookup"><span data-stu-id="a933a-107">Create a Maven project</span></span>
> * <span data-ttu-id="a933a-108">新增相依性</span><span class="sxs-lookup"><span data-stu-id="a933a-108">Add dependencies</span></span>
> * <span data-ttu-id="a933a-109">建立認證</span><span class="sxs-lookup"><span data-stu-id="a933a-109">Create credentials</span></span>
> * <span data-ttu-id="a933a-110">建立資源</span><span class="sxs-lookup"><span data-stu-id="a933a-110">Create resources</span></span>
> * <span data-ttu-id="a933a-111">執行管理工作</span><span class="sxs-lookup"><span data-stu-id="a933a-111">Perform management tasks</span></span>
> * <span data-ttu-id="a933a-112">刪除資源</span><span class="sxs-lookup"><span data-stu-id="a933a-112">Delete resources</span></span>
> * <span data-ttu-id="a933a-113">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="a933a-113">Run the application</span></span>

<span data-ttu-id="a933a-114">執行這些步驟大約需要 20 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="a933a-114">It takes about 20 minutes to do these steps.</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="a933a-115">建立 Maven 專案</span><span class="sxs-lookup"><span data-stu-id="a933a-115">Create a Maven project</span></span>

1. <span data-ttu-id="a933a-116">如果尚未這麼做，請先安裝 [JAVA](http://www.oracle.com/technetwork/java/javase/downloads/index.html)。</span><span class="sxs-lookup"><span data-stu-id="a933a-116">If you haven't already done so, install [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
2. <span data-ttu-id="a933a-117">安裝 [Maven](http://maven.apache.org/download.cgi)。</span><span class="sxs-lookup"><span data-stu-id="a933a-117">Install [Maven](http://maven.apache.org/download.cgi).</span></span>
3. <span data-ttu-id="a933a-118">建立新的資料夾和專案：</span><span class="sxs-lookup"><span data-stu-id="a933a-118">Create a new folder and the project:</span></span>
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a><span data-ttu-id="a933a-119">新增相依性</span><span class="sxs-lookup"><span data-stu-id="a933a-119">Add dependencies</span></span>

1. <span data-ttu-id="a933a-120">在 `testAzureApp` 資料夾下，開啟 `pom.xml` 檔案，然後將組建設定新增至&lt;專案&gt;，以啟用您的應用程式的建置：</span><span class="sxs-lookup"><span data-stu-id="a933a-120">Under the `testAzureApp` folder, open the `pom.xml` file and add the build configuration to &lt;project&gt; to enable the building of your application:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <configuration>
                <mainClass>com.fabrikam.testAzureApp.App</mainClass>
            </configuration>
        </plugin>
      </plugins>
    </build>
    ```

2. <span data-ttu-id="a933a-121">新增存取 Azure Java SDK 所需的相依性。</span><span class="sxs-lookup"><span data-stu-id="a933a-121">Add the dependencies that are needed to access the Azure Java SDK.</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-compute</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-resources</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-network</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.squareup.okio</groupId>
      <artifactId>okio</artifactId>
      <version>1.13.0</version>
    </dependency>
    <dependency> 
      <groupId>com.nimbusds</groupId>
      <artifactId>nimbus-jose-jwt</artifactId>
      <version>3.6</version>
    </dependency>
    <dependency>
      <groupId>net.minidev</groupId>
      <artifactId>json-smart</artifactId>
      <version>1.0.6.3</version>
    </dependency>
    <dependency>
      <groupId>javax.mail</groupId>
      <artifactId>mail</artifactId>
      <version>1.4.5</version>
    </dependency>
    ```

3. <span data-ttu-id="a933a-122">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="a933a-122">Save the file.</span></span>

## <a name="create-credentials"></a><span data-ttu-id="a933a-123">建立認證</span><span class="sxs-lookup"><span data-stu-id="a933a-123">Create credentials</span></span>

<span data-ttu-id="a933a-124">在您開始此步驟之前，請確定您可以存取 [Active Directory 服務主體](../../azure-resource-manager/resource-group-create-service-principal-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="a933a-124">Before you start this step, make sure that you have access to an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="a933a-125">您也應該記錄應用程式識別碼、驗證金鑰以及租用戶識別碼，您在稍後的步驟會需要這些項目。</span><span class="sxs-lookup"><span data-stu-id="a933a-125">You should also record the application ID, the authentication key, and the tenant ID that you need in a later step.</span></span>

### <a name="create-the-authorization-file"></a><span data-ttu-id="a933a-126">建立授權檔</span><span class="sxs-lookup"><span data-stu-id="a933a-126">Create the authorization file</span></span>

1. <span data-ttu-id="a933a-127">建立名為 `azureauth.properties` 的檔案名稱，並加入下列屬性：</span><span class="sxs-lookup"><span data-stu-id="a933a-127">Create a file named `azureauth.properties` and add these properties to it:</span></span>

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

    <span data-ttu-id="a933a-128">以您的訂用帳戶 ID 取代 **&lt;subscription-id&gt;**、以 Active Directory 應用程式識別碼取代 **&lt;application-id&gt;**、以應用程式金鑰取代 **&lt;authentication-key&gt;**，以及以租用戶識別碼取代 **&lt;tenant-id&gt;**。</span><span class="sxs-lookup"><span data-stu-id="a933a-128">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with the Active Directory application identifier, **&lt;authentication-key&gt;** with the application key, and **&lt;tenant-id&gt;** with the tenant identifier.</span></span>

2. <span data-ttu-id="a933a-129">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="a933a-129">Save the file.</span></span>
3. <span data-ttu-id="a933a-130">使用驗證檔案的完整路徑，在殼層中設定名稱為 AZURE_AUTH_LOCATION 的環境變數。</span><span class="sxs-lookup"><span data-stu-id="a933a-130">Set an environment variable named AZURE_AUTH_LOCATION in your shell with the full path to the authentication file.</span></span>

### <a name="create-the-management-client"></a><span data-ttu-id="a933a-131">建立管理用戶端</span><span class="sxs-lookup"><span data-stu-id="a933a-131">Create the management client</span></span>

1. <span data-ttu-id="a933a-132">在 `src\main\java\com\fabrikam` 下開啟 `App.java` 檔案，並確定此 package 陳述式位於最上方：</span><span class="sxs-lookup"><span data-stu-id="a933a-132">Open the `App.java` file under `src\main\java\com\fabrikam` and make sure this package statement is at the top:</span></span>

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. <span data-ttu-id="a933a-133">在 package 陳述式下，新增下列 import 陳述式：</span><span class="sxs-lookup"><span data-stu-id="a933a-133">Under the package statement, add these import statements:</span></span>
   
    ```java
    import com.microsoft.azure.management.Azure;
    import com.microsoft.azure.management.compute.AvailabilitySet;
    import com.microsoft.azure.management.compute.AvailabilitySetSkuTypes;
    import com.microsoft.azure.management.compute.CachingTypes;
    import com.microsoft.azure.management.compute.InstanceViewStatus;
    import com.microsoft.azure.management.compute.DiskInstanceView;
    import com.microsoft.azure.management.compute.VirtualMachine;
    import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
    import com.microsoft.azure.management.network.PublicIPAddress;
    import com.microsoft.azure.management.network.Network;
    import com.microsoft.azure.management.network.NetworkInterface;
    import com.microsoft.azure.management.resources.ResourceGroup;
    import com.microsoft.azure.management.resources.fluentcore.arm.Region;
    import com.microsoft.azure.management.resources.fluentcore.model.Creatable;
    import com.microsoft.rest.LogLevel;
    import java.io.File;
    import java.util.Scanner;
    ```

2. <span data-ttu-id="a933a-134">若要建立您提出要求所需的 Active Directory 認證，請將此程式碼新增至 App 類別的 Main 方法：</span><span class="sxs-lookup"><span data-stu-id="a933a-134">To create the Active Directory credentials that you need to make requests, add this code to the main method of the App class:</span></span>
   
    ```java
    try {    
        final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
        Azure azure = Azure.configure()
            .withLogLevel(LogLevel.BASIC)
            .authenticate(credFile)
            .withDefaultSubscription();
    } catch (Exception e) {
        System.out.println(e.getMessage());
        e.printStackTrace();
    }

    ```

## <a name="create-resources"></a><span data-ttu-id="a933a-135">建立資源</span><span class="sxs-lookup"><span data-stu-id="a933a-135">Create resources</span></span>

### <a name="create-the-resource-group"></a><span data-ttu-id="a933a-136">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="a933a-136">Create the resource group</span></span>

<span data-ttu-id="a933a-137">所有資源都必須包含在[資源群組](../../azure-resource-manager/resource-group-overview.md)中。</span><span class="sxs-lookup"><span data-stu-id="a933a-137">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="a933a-138">若要指定應用程式的值並建立資源群組，請將以下程式碼新增到 Main 方法中的 try 區塊：</span><span class="sxs-lookup"><span data-stu-id="a933a-138">To specify values for the application and create the resource group, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-the-availability-set"></a><span data-ttu-id="a933a-139">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="a933a-139">Create the availability set</span></span>

<span data-ttu-id="a933a-140">維護您應用程式所使用的虛擬機器時，使用[可用性設定組](tutorial-availability-sets.md)可讓您更加輕鬆。</span><span class="sxs-lookup"><span data-stu-id="a933a-140">[Availability sets](tutorial-availability-sets.md) make it easier for you to maintain the virtual machines used by your application.</span></span>

<span data-ttu-id="a933a-141">若要建立可用性設定組，請將以下程式碼新增到 Main 方法中的 try 區塊：</span><span class="sxs-lookup"><span data-stu-id="a933a-141">To create the availability set, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-the-public-ip-address"></a><span data-ttu-id="a933a-142">建立公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="a933a-142">Create the public IP address</span></span>

<span data-ttu-id="a933a-143">必須要有[公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)才能與虛擬機器進行通訊。</span><span class="sxs-lookup"><span data-stu-id="a933a-143">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed to communicate with the virtual machine.</span></span>

<span data-ttu-id="a933a-144">若要為虛擬機器建立公用 IP 位址，請將以下程式碼新增到 Main 方法中的 try 區塊：</span><span class="sxs-lookup"><span data-stu-id="a933a-144">To create the public IP address for the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-the-virtual-network"></a><span data-ttu-id="a933a-145">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="a933a-145">Create the virtual network</span></span>

<span data-ttu-id="a933a-146">虛擬機器必須在[虛擬網路](../../virtual-network/virtual-networks-overview.md)的子網路中。</span><span class="sxs-lookup"><span data-stu-id="a933a-146">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="a933a-147">若要建立子網路和虛擬網路，請將以下程式碼新增到 Main 方法中的 try 區塊：</span><span class="sxs-lookup"><span data-stu-id="a933a-147">To create a subnet and a virtual network, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating virtual network...");
Network network = azure.networks()
    .define("myVN")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withAddressSpace("10.0.0.0/16")
    .withSubnet("mySubnet","10.0.0.0/24")
    .create();
```

### <a name="create-the-network-interface"></a><span data-ttu-id="a933a-148">建立網路介面</span><span class="sxs-lookup"><span data-stu-id="a933a-148">Create the network interface</span></span>

<span data-ttu-id="a933a-149">虛擬機器需要網路介面以在虛擬網路上通訊。</span><span class="sxs-lookup"><span data-stu-id="a933a-149">A virtual machine needs a network interface to communicate on the virtual network.</span></span>

<span data-ttu-id="a933a-150">若要建立網路介面，請將以下程式碼新增到 Main 方法中的 try 區塊：</span><span class="sxs-lookup"><span data-stu-id="a933a-150">To create a network interface, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating network interface...");
NetworkInterface networkInterface = azure.networkInterfaces()
    .define("myNIC")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetwork(network)
    .withSubnet("mySubnet")
    .withPrimaryPrivateIPAddressDynamic()
    .withExistingPrimaryPublicIPAddress(publicIPAddress)
    .create();
```

### <a name="create-the-virtual-machine"></a><span data-ttu-id="a933a-151">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a933a-151">Create the virtual machine</span></span>

<span data-ttu-id="a933a-152">既然您已經建立所有支援的資源，您可以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a933a-152">Now that you created all the supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="a933a-153">若要建立虛擬機器，請將以下程式碼新增到 Main 方法中的 try 區塊：</span><span class="sxs-lookup"><span data-stu-id="a933a-153">To create the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating virtual machine...");
VirtualMachine virtualMachine = azure.virtualMachines()
    .define("myVM")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetworkInterface(networkInterface)
    .withLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .withAdminUsername("azureuser")
    .withAdminPassword("Azure12345678")
    .withComputerName("myVM")
    .withExistingAvailabilitySet(availabilitySet)
    .withSize("Standard_DS1")
    .create();
Scanner input = new Scanner(System.in);
System.out.println("Press enter to get information about the VM...");
input.nextLine();
```

> [!NOTE]
> <span data-ttu-id="a933a-154">本教學課程中會建立執行 Windows Server 作業系統版本的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a933a-154">This tutorial creates a virtual machine running a version of the Windows Server operating system.</span></span> <span data-ttu-id="a933a-155">若要深入了解如何選取其他映像，請參閱 [使用 Windows PowerShell 和 Azure CLI 來瀏覽和選取 Azure 虛擬機器映像](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a933a-155">To learn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and the Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="a933a-156">如果您想要使用現有的磁碟而不使用市集映像，請使用以下程式碼：</span><span class="sxs-lookup"><span data-stu-id="a933a-156">If you want to use an existing disk instead of a marketplace image, use this code:</span></span> 

```java
ManagedDisk managedDisk = azure.disks.define("myosdisk") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd") 
    .withSizeInGB(128) 
    .withSku(DiskSkuTypes.PremiumLRS) 
    .create(); 

azure.virtualMachines.define("myVM") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withExistingPrimaryNetworkInterface(networkInterface) 
    .withSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows) 
    .withExistingAvailabilitySet(availabilitySet) 
    .withSize(VirtualMachineSizeTypes.StandardDS1) 
    .create(); 
``` 

## <a name="perform-management-tasks"></a><span data-ttu-id="a933a-157">執行管理工作</span><span class="sxs-lookup"><span data-stu-id="a933a-157">Perform management tasks</span></span>

<span data-ttu-id="a933a-158">在虛擬機器的生命週期內，您可以執行一些管理工作，例如啟動、停止或刪除虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a933a-158">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="a933a-159">此外，您可以建立程式碼來自動執行重複或複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="a933a-159">Additionally, you may want to create code to automate repetitive or complex tasks.</span></span>

<span data-ttu-id="a933a-160">當您需要使用 VM 來執行任何操作時，必須取得其執行個體。</span><span class="sxs-lookup"><span data-stu-id="a933a-160">When you need to do anything with the VM, you need to get an instance of it.</span></span> <span data-ttu-id="a933a-161">將此程式碼新增到 Main 方法的 try 區塊：</span><span class="sxs-lookup"><span data-stu-id="a933a-161">Add this code to the try block of the main method:</span></span>

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-the-vm"></a><span data-ttu-id="a933a-162">取得 VM 的相關資訊</span><span class="sxs-lookup"><span data-stu-id="a933a-162">Get information about the VM</span></span>

<span data-ttu-id="a933a-163">若要取得虛擬機器的相關資訊，請將以下程式碼新增到 Main 方法中的 try 區塊：</span><span class="sxs-lookup"><span data-stu-id="a933a-163">To get information about the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("hardwareProfile");
System.out.println("    vmSize: " + vm.size());
System.out.println("storageProfile");
System.out.println("  imageReference");
System.out.println("    publisher: " + vm.storageProfile().imageReference().publisher());
System.out.println("    offer: " + vm.storageProfile().imageReference().offer());
System.out.println("    sku: " + vm.storageProfile().imageReference().sku());
System.out.println("    version: " + vm.storageProfile().imageReference().version());
System.out.println("  osDisk");
System.out.println("    osType: " + vm.storageProfile().osDisk().osType());
System.out.println("    name: " + vm.storageProfile().osDisk().name());
System.out.println("    createOption: " + vm.storageProfile().osDisk().createOption());
System.out.println("    caching: " + vm.storageProfile().osDisk().caching());
System.out.println("osProfile");
System.out.println("    computerName: " + vm.osProfile().computerName());
System.out.println("    adminUserName: " + vm.osProfile().adminUsername());
System.out.println("    provisionVMAgent: " + vm.osProfile().windowsConfiguration().provisionVMAgent());
System.out.println("    enableAutomaticUpdates: " + vm.osProfile().windowsConfiguration().enableAutomaticUpdates());
System.out.println("networkProfile");
System.out.println("    networkInterface: " + vm.primaryNetworkInterfaceId());
System.out.println("vmAgent");
System.out.println("  vmAgentVersion: " + vm.instanceView().vmAgent().vmAgentVersion());
System.out.println("    statuses");
for(InstanceViewStatus status : vm.instanceView().vmAgent().statuses()) {
    System.out.println("    code: " + status.code());
    System.out.println("    displayStatus: " + status.displayStatus());
    System.out.println("    message: " + status.message());
    System.out.println("    time: " + status.time());
}
System.out.println("disks");
for(DiskInstanceView disk : vm.instanceView().disks()) {
    System.out.println("  name: " + disk.name());
    System.out.println("  statuses");
    for(InstanceViewStatus status : disk.statuses()) {
        System.out.println("    code: " + status.code());
        System.out.println("    displayStatus: " + status.displayStatus());
        System.out.println("    time: " + status.time());
    }
}
System.out.println("VM general status");
System.out.println("  provisioningStatus: " + vm.provisioningState());
System.out.println("  id: " + vm.id());
System.out.println("  name: " + vm.name());
System.out.println("  type: " + vm.type());
System.out.println("VM instance status");
for(InstanceViewStatus status : vm.instanceView().statuses()) {
    System.out.println("  code: " + status.code());
    System.out.println("  displayStatus: " + status.displayStatus());
}
System.out.println("Press enter to continue...");
input.nextLine();   
```

### <a name="stop-the-vm"></a><span data-ttu-id="a933a-164">停止 VM</span><span class="sxs-lookup"><span data-stu-id="a933a-164">Stop the VM</span></span>

<span data-ttu-id="a933a-165">您可以停止虛擬機器並保留其所有的設定，但仍繼續計費，或您可以停止虛擬機器並將其解除配置。</span><span class="sxs-lookup"><span data-stu-id="a933a-165">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="a933a-166">當解除配置虛擬機器時，與其相關聯的所有資源也都會解除配置且其計費會結束。</span><span class="sxs-lookup"><span data-stu-id="a933a-166">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="a933a-167">若要停止虛擬機器而不解除配置，請將以下程式碼新增到 Main 方法中的 try 區塊：</span><span class="sxs-lookup"><span data-stu-id="a933a-167">To stop the virtual machine without deallocating it, add this code to the try block in the main method:</span></span>

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter to continue...");
input.nextLine();
```

<span data-ttu-id="a933a-168">如果您想要解除配置虛擬機器，請將 PowerOff 呼叫變更為下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="a933a-168">If you want to deallocate the virtual machine, change the PowerOff call to this code:</span></span>

```java
vm.deallocate();
```

### <a name="start-the-vm"></a><span data-ttu-id="a933a-169">啟動 VM</span><span class="sxs-lookup"><span data-stu-id="a933a-169">Start the VM</span></span>

<span data-ttu-id="a933a-170">若要啟動虛擬機器，請將以下程式碼新增到 Main 方法中的 try 區塊：</span><span class="sxs-lookup"><span data-stu-id="a933a-170">To start the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter to continue...");
input.nextLine();
```

### <a name="resize-the-vm"></a><span data-ttu-id="a933a-171">調整 VM 的大小</span><span class="sxs-lookup"><span data-stu-id="a933a-171">Resize the VM</span></span>

<span data-ttu-id="a933a-172">決定虛擬機器的大小時，應該考慮部署的許多層面。</span><span class="sxs-lookup"><span data-stu-id="a933a-172">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="a933a-173">如需詳細資訊，請參閱 [VM 大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="a933a-173">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="a933a-174">若要變更虛擬機器的大小，請將以下程式碼新增到 Main 方法中的 try 區塊：</span><span class="sxs-lookup"><span data-stu-id="a933a-174">To change size of the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter to continue...");
input.nextLine();
```

### <a name="add-a-data-disk-to-the-vm"></a><span data-ttu-id="a933a-175">將資料磁碟新增至 VM</span><span class="sxs-lookup"><span data-stu-id="a933a-175">Add a data disk to the VM</span></span>

<span data-ttu-id="a933a-176">若要將資料磁碟新增到大小為 2 GB、LUN 為 0 且快取類型為 ReadWrite 的虛擬機器，請將以下程式碼新增到 Main 方法中的 try 區塊：</span><span class="sxs-lookup"><span data-stu-id="a933a-176">To add a data disk to the virtual machine that is 2 GB in size, has a LUN of 0, and a caching type of ReadWrite, add this code to the try block in the main method:</span></span>

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter to delete resources...");
input.nextLine();
```

## <a name="delete-resources"></a><span data-ttu-id="a933a-177">刪除資源</span><span class="sxs-lookup"><span data-stu-id="a933a-177">Delete resources</span></span>

<span data-ttu-id="a933a-178">由於您需要為在 Azure 中使用的資源付費，因此刪除不再需要的資源一律是理想的做法。</span><span class="sxs-lookup"><span data-stu-id="a933a-178">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="a933a-179">如果您想要刪除虛擬機器及所有支援的資源，您只需要刪除資源群組。</span><span class="sxs-lookup"><span data-stu-id="a933a-179">If you want to delete the virtual machines and all the supporting resources, all you have to do is delete the resource group.</span></span>

1. <span data-ttu-id="a933a-180">若要刪除資源群組，請將以下程式碼新增到 Main 方法中的 try 區塊：</span><span class="sxs-lookup"><span data-stu-id="a933a-180">To delete the resource group, add this code to the try block in the main method:</span></span>
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. <span data-ttu-id="a933a-181">儲存 App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="a933a-181">Save the App.java file.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="a933a-182">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="a933a-182">Run the application</span></span>

<span data-ttu-id="a933a-183">此主控台應用程式從開始到完成的完整執行應該需要五分鐘左右。</span><span class="sxs-lookup"><span data-stu-id="a933a-183">It should take about five minutes for this console application to run completely from start to finish.</span></span>

1. <span data-ttu-id="a933a-184">若要執行應用程式，請使用此 Maven 命令：</span><span class="sxs-lookup"><span data-stu-id="a933a-184">To run the application, use this Maven command:</span></span>

    ```
    mvn compile exec:java
    ```

2. <span data-ttu-id="a933a-185">在您按 **Enter** 以開始刪除資源之前，可以先花幾分鐘的時間來確認 Azure 入口網站中的資源建立情況。</span><span class="sxs-lookup"><span data-stu-id="a933a-185">Before you press **Enter** to start deleting resources, you could take a few minutes to verify the creation of the resources in the Azure portal.</span></span> <span data-ttu-id="a933a-186">請按一下部署狀態來查看該項部署的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a933a-186">Click the deployment status to see information about the deployment.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a933a-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a933a-187">Next steps</span></span>
* <span data-ttu-id="a933a-188">深入了解關於使用[適用於 JAVA 的 Azure 程式庫](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview)。</span><span class="sxs-lookup"><span data-stu-id="a933a-188">Learn more about using the [Azure libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span></span>

