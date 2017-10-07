---
title: "aaaCreate 和管理 Azure 虛擬機器使用 Java |Microsoft 文件"
description: "使用 Java 和 Azure 資源管理員 toodeploy，虛擬機器和其支援的所有資源。"
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
ms.openlocfilehash: 31ac8d59f92ecff887e64906940933dd6fd50815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a><span data-ttu-id="417c8-103">在 Azure 中使用 JAVA 建立並管理 Windows VM</span><span class="sxs-lookup"><span data-stu-id="417c8-103">Create and manage Windows VMs in Azure using Java</span></span>

<span data-ttu-id="417c8-104">[Azure 虛擬機器](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) 需要數個支援的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="417c8-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="417c8-105">本文涵蓋使用 JAVA 建立、管理和刪除 VM 資源。</span><span class="sxs-lookup"><span data-stu-id="417c8-105">This article covers creating, managing, and deleting VM resources using Java.</span></span> <span data-ttu-id="417c8-106">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="417c8-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="417c8-107">建立 Maven 專案</span><span class="sxs-lookup"><span data-stu-id="417c8-107">Create a Maven project</span></span>
> * <span data-ttu-id="417c8-108">新增相依性</span><span class="sxs-lookup"><span data-stu-id="417c8-108">Add dependencies</span></span>
> * <span data-ttu-id="417c8-109">建立認證</span><span class="sxs-lookup"><span data-stu-id="417c8-109">Create credentials</span></span>
> * <span data-ttu-id="417c8-110">建立資源</span><span class="sxs-lookup"><span data-stu-id="417c8-110">Create resources</span></span>
> * <span data-ttu-id="417c8-111">執行管理工作</span><span class="sxs-lookup"><span data-stu-id="417c8-111">Perform management tasks</span></span>
> * <span data-ttu-id="417c8-112">刪除資源</span><span class="sxs-lookup"><span data-stu-id="417c8-112">Delete resources</span></span>
> * <span data-ttu-id="417c8-113">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="417c8-113">Run hello application</span></span>

<span data-ttu-id="417c8-114">它會採用約 20 分鐘 toodo 這些步驟。</span><span class="sxs-lookup"><span data-stu-id="417c8-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="417c8-115">建立 Maven 專案</span><span class="sxs-lookup"><span data-stu-id="417c8-115">Create a Maven project</span></span>

1. <span data-ttu-id="417c8-116">如果尚未這麼做，請先安裝 [JAVA](http://www.oracle.com/technetwork/java/javase/downloads/index.html)。</span><span class="sxs-lookup"><span data-stu-id="417c8-116">If you haven't already done so, install [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
2. <span data-ttu-id="417c8-117">安裝 [Maven](http://maven.apache.org/download.cgi)。</span><span class="sxs-lookup"><span data-stu-id="417c8-117">Install [Maven](http://maven.apache.org/download.cgi).</span></span>
3. <span data-ttu-id="417c8-118">建立新的資料夾和 hello 專案：</span><span class="sxs-lookup"><span data-stu-id="417c8-118">Create a new folder and hello project:</span></span>
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a><span data-ttu-id="417c8-119">新增相依性</span><span class="sxs-lookup"><span data-stu-id="417c8-119">Add dependencies</span></span>

1. <span data-ttu-id="417c8-120">在 hello`testAzureApp`資料夾中，開啟 hello`pom.xml`檔案，然後加入 hello 組建組態太&lt;專案&gt;tooenable hello 建置您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="417c8-120">Under hello `testAzureApp` folder, open hello `pom.xml` file and add hello build configuration too&lt;project&gt; tooenable hello building of your application:</span></span>

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

2. <span data-ttu-id="417c8-121">加入所需的 tooaccess hello Azure Java SDK hello 依存性。</span><span class="sxs-lookup"><span data-stu-id="417c8-121">Add hello dependencies that are needed tooaccess hello Azure Java SDK.</span></span>

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

3. <span data-ttu-id="417c8-122">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="417c8-122">Save hello file.</span></span>

## <a name="create-credentials"></a><span data-ttu-id="417c8-123">建立認證</span><span class="sxs-lookup"><span data-stu-id="417c8-123">Create credentials</span></span>

<span data-ttu-id="417c8-124">在開始此步驟之前，請確定您有存取 tooan [Active Directory 服務主體](../../azure-resource-manager/resource-group-create-service-principal-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="417c8-124">Before you start this step, make sure that you have access tooan [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="417c8-125">您也應該在稍後步驟中，記錄 hello 應用程式識別碼、 hello 驗證金鑰，以及您需要的 hello 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="417c8-125">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="417c8-126">建立 hello 授權檔</span><span class="sxs-lookup"><span data-stu-id="417c8-126">Create hello authorization file</span></span>

1. <span data-ttu-id="417c8-127">建立名為`azureauth.properties`並加入這些屬性 tooit:</span><span class="sxs-lookup"><span data-stu-id="417c8-127">Create a file named `azureauth.properties` and add these properties tooit:</span></span>

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

    <span data-ttu-id="417c8-128">取代**&lt;訂用帳戶 id&gt;** 與您的訂用帳戶識別碼**&lt;應用程式識別碼&gt;**以 hello Active Directory 應用程式識別項， **&lt;驗證金鑰&gt;**與 hello 應用程式鍵，和**&lt;租用戶識別碼&gt;**與 hello 租用戶識別項。</span><span class="sxs-lookup"><span data-stu-id="417c8-128">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

2. <span data-ttu-id="417c8-129">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="417c8-129">Save hello file.</span></span>
3. <span data-ttu-id="417c8-130">設定環境變數命名您的 shell AZURE_AUTH_LOCATION 與 hello 完整路徑 toohello 驗證檔案。</span><span class="sxs-lookup"><span data-stu-id="417c8-130">Set an environment variable named AZURE_AUTH_LOCATION in your shell with hello full path toohello authentication file.</span></span>

### <a name="create-hello-management-client"></a><span data-ttu-id="417c8-131">建立 hello 管理用戶端</span><span class="sxs-lookup"><span data-stu-id="417c8-131">Create hello management client</span></span>

1. <span data-ttu-id="417c8-132">開啟 hello`App.java`底下`src\main\java\com\fabrikam`，並確定此封裝陳述式是在 hello 最上方：</span><span class="sxs-lookup"><span data-stu-id="417c8-132">Open hello `App.java` file under `src\main\java\com\fabrikam` and make sure this package statement is at hello top:</span></span>

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. <span data-ttu-id="417c8-133">Hello 封裝陳述式，下方加入下列 import 陳述式：</span><span class="sxs-lookup"><span data-stu-id="417c8-133">Under hello package statement, add these import statements:</span></span>
   
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

2. <span data-ttu-id="417c8-134">toocreate hello Active Directory 認證，您需要 toomake 要求程式碼 toohello 主要將此方法加入的 hello 應用程式類別：</span><span class="sxs-lookup"><span data-stu-id="417c8-134">toocreate hello Active Directory credentials that you need toomake requests, add this code toohello main method of hello App class:</span></span>
   
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

## <a name="create-resources"></a><span data-ttu-id="417c8-135">建立資源</span><span class="sxs-lookup"><span data-stu-id="417c8-135">Create resources</span></span>

### <a name="create-hello-resource-group"></a><span data-ttu-id="417c8-136">建立 hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="417c8-136">Create hello resource group</span></span>

<span data-ttu-id="417c8-137">所有資源都必須包含在[資源群組](../../azure-resource-manager/resource-group-overview.md)中。</span><span class="sxs-lookup"><span data-stu-id="417c8-137">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="417c8-138">toospecify 值 hello 應用程式並建立 hello 資源群組，請在 hello main 方法中加入此程式碼 toohello try 區塊：</span><span class="sxs-lookup"><span data-stu-id="417c8-138">toospecify values for hello application and create hello resource group, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-hello-availability-set"></a><span data-ttu-id="417c8-139">建立 hello 可用性設定組</span><span class="sxs-lookup"><span data-stu-id="417c8-139">Create hello availability set</span></span>

<span data-ttu-id="417c8-140">[可用性設定組](tutorial-availability-sets.md)方便您應用程式所使用的 toomaintain hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="417c8-140">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

<span data-ttu-id="417c8-141">toocreate hello 可用性組，請在 hello main 方法中加入此程式碼 toohello try 區塊：</span><span class="sxs-lookup"><span data-stu-id="417c8-141">toocreate hello availability set, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-hello-public-ip-address"></a><span data-ttu-id="417c8-142">建立 hello 公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="417c8-142">Create hello public IP address</span></span>

<span data-ttu-id="417c8-143">A[公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)是需要的 toocommunicate 與 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="417c8-143">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

<span data-ttu-id="417c8-144">toocreate hello 公用 IP 位址 hello 虛擬機器，加入此程式碼 toohello try 區塊 hello main 方法中：</span><span class="sxs-lookup"><span data-stu-id="417c8-144">toocreate hello public IP address for hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-hello-virtual-network"></a><span data-ttu-id="417c8-145">建立 hello 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="417c8-145">Create hello virtual network</span></span>

<span data-ttu-id="417c8-146">虛擬機器必須在[虛擬網路](../../virtual-network/virtual-networks-overview.md)的子網路中。</span><span class="sxs-lookup"><span data-stu-id="417c8-146">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="417c8-147">toocreate 的子網路和虛擬網路中，加入此程式碼 toohello try 區塊 hello main 方法中：</span><span class="sxs-lookup"><span data-stu-id="417c8-147">toocreate a subnet and a virtual network, add this code toohello try block in hello main method:</span></span>

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

### <a name="create-hello-network-interface"></a><span data-ttu-id="417c8-148">建立 hello 網路介面</span><span class="sxs-lookup"><span data-stu-id="417c8-148">Create hello network interface</span></span>

<span data-ttu-id="417c8-149">需要網路介面 toocommunicate hello 虛擬網路上的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="417c8-149">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

<span data-ttu-id="417c8-150">toocreate 網路介面，加入此程式碼 toohello try 區塊 hello main 方法中：</span><span class="sxs-lookup"><span data-stu-id="417c8-150">toocreate a network interface, add this code toohello try block in hello main method:</span></span>

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

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="417c8-151">建立 hello 的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="417c8-151">Create hello virtual machine</span></span>

<span data-ttu-id="417c8-152">現在，您會建立所有 hello 支援的資源，您可以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="417c8-152">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="417c8-153">toocreate hello 虛擬機器、 在 hello main 方法中加入此程式碼 toohello try 區塊：</span><span class="sxs-lookup"><span data-stu-id="417c8-153">toocreate hello virtual machine, add this code toohello try block in hello main method:</span></span>

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
System.out.println("Press enter tooget information about hello VM...");
input.nextLine();
```

> [!NOTE]
> <span data-ttu-id="417c8-154">本教學課程中建立虛擬機器執行 hello Windows Server 作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="417c8-154">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="417c8-155">toolearn 有關選取其他映像的詳細資訊請參閱[瀏覽並選取 Azure 虛擬機器映像使用 Windows PowerShell 與 hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="417c8-155">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="417c8-156">如果您想 toouse 現有磁碟而非 marketplace 映像，請使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="417c8-156">If you want toouse an existing disk instead of a marketplace image, use this code:</span></span> 

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

## <a name="perform-management-tasks"></a><span data-ttu-id="417c8-157">執行管理工作</span><span class="sxs-lookup"><span data-stu-id="417c8-157">Perform management tasks</span></span>

<span data-ttu-id="417c8-158">在虛擬機器的 hello 生命週期，您可能想 toorun 管理工作，例如啟動、 停止或刪除虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="417c8-158">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="417c8-159">此外，您可能想 toocreate 程式碼 tooautomate 重複或複雜工作。</span><span class="sxs-lookup"><span data-stu-id="417c8-159">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

<span data-ttu-id="417c8-160">當您以 hello VM 的任何項目需要 toodo 時，您會需要 tooget 它的執行個體。</span><span class="sxs-lookup"><span data-stu-id="417c8-160">When you need toodo anything with hello VM, you need tooget an instance of it.</span></span> <span data-ttu-id="417c8-161">加入這個程式碼 toohello 的 try 區塊 hello main 方法：</span><span class="sxs-lookup"><span data-stu-id="417c8-161">Add this code toohello try block of hello main method:</span></span>

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="417c8-162">取得 hello VM 的相關資訊</span><span class="sxs-lookup"><span data-stu-id="417c8-162">Get information about hello VM</span></span>

<span data-ttu-id="417c8-163">tooget 資訊 hello 虛擬機器，加入此程式碼 toohello try 區塊 hello main 方法中：</span><span class="sxs-lookup"><span data-stu-id="417c8-163">tooget information about hello virtual machine, add this code toohello try block in hello main method:</span></span>

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
System.out.println("Press enter toocontinue...");
input.nextLine();   
```

### <a name="stop-hello-vm"></a><span data-ttu-id="417c8-164">停止 hello VM</span><span class="sxs-lookup"><span data-stu-id="417c8-164">Stop hello VM</span></span>

<span data-ttu-id="417c8-165">您可以停止虛擬機器並保留其所有設定，但繼續 toobe 支付，或您可以停止虛擬機器和解除配置。</span><span class="sxs-lookup"><span data-stu-id="417c8-165">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="417c8-166">當解除配置虛擬機器時，與其相關聯的所有資源也都會解除配置且其計費會結束。</span><span class="sxs-lookup"><span data-stu-id="417c8-166">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="417c8-167">toostop hello 虛擬機器，而不取消配置，加入此程式碼 toohello try 區塊 hello main 方法中：</span><span class="sxs-lookup"><span data-stu-id="417c8-167">toostop hello virtual machine without deallocating it, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

<span data-ttu-id="417c8-168">如果您想 toodeallocate hello 虛擬機器，變更 hello 關閉呼叫 toothis 程式碼：</span><span class="sxs-lookup"><span data-stu-id="417c8-168">If you want toodeallocate hello virtual machine, change hello PowerOff call toothis code:</span></span>

```java
vm.deallocate();
```

### <a name="start-hello-vm"></a><span data-ttu-id="417c8-169">啟動 VM hello</span><span class="sxs-lookup"><span data-stu-id="417c8-169">Start hello VM</span></span>

<span data-ttu-id="417c8-170">toostart hello 虛擬機器、 在 hello main 方法中加入此程式碼 toohello try 區塊：</span><span class="sxs-lookup"><span data-stu-id="417c8-170">toostart hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="resize-hello-vm"></a><span data-ttu-id="417c8-171">調整大小 hello VM</span><span class="sxs-lookup"><span data-stu-id="417c8-171">Resize hello VM</span></span>

<span data-ttu-id="417c8-172">決定虛擬機器的大小時，應該考慮部署的許多層面。</span><span class="sxs-lookup"><span data-stu-id="417c8-172">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="417c8-173">如需詳細資訊，請參閱 [VM 大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="417c8-173">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="417c8-174">hello 虛擬機器，toochange 大小 hello main 方法中新增此程式碼 toohello try 區塊：</span><span class="sxs-lookup"><span data-stu-id="417c8-174">toochange size of hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="417c8-175">新增資料磁碟 toohello VM</span><span class="sxs-lookup"><span data-stu-id="417c8-175">Add a data disk toohello VM</span></span>

<span data-ttu-id="417c8-176">tooadd 是 2 GB 的大小，資料磁碟 toohello 虛擬機器有 0，且快取類型為 ReadWrite 的 LUN，在 hello main 方法中加入此程式碼 toohello try 區塊：</span><span class="sxs-lookup"><span data-stu-id="417c8-176">tooadd a data disk toohello virtual machine that is 2 GB in size, has a LUN of 0, and a caching type of ReadWrite, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter toodelete resources...");
input.nextLine();
```

## <a name="delete-resources"></a><span data-ttu-id="417c8-177">刪除資源</span><span class="sxs-lookup"><span data-stu-id="417c8-177">Delete resources</span></span>

<span data-ttu-id="417c8-178">因為您負責 Azure 中使用的資源，但它永遠是很好的作法 toodelete 資源不再需要的。</span><span class="sxs-lookup"><span data-stu-id="417c8-178">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="417c8-179">如果您想 toodelete hello 虛擬機器，而且所有 hello 支援的資源，您都有 toodo 是刪除 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="417c8-179">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

1. <span data-ttu-id="417c8-180">toodelete hello 資源群組中，加入此程式碼 toohello try 區塊 hello main 方法中：</span><span class="sxs-lookup"><span data-stu-id="417c8-180">toodelete hello resource group, add this code toohello try block in hello main method:</span></span>
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. <span data-ttu-id="417c8-181">儲存 hello App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="417c8-181">Save hello App.java file.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="417c8-182">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="417c8-182">Run hello application</span></span>

<span data-ttu-id="417c8-183">它應該完全從開始 toofinish 此主控台應用程式 toorun 大約五分鐘。</span><span class="sxs-lookup"><span data-stu-id="417c8-183">It should take about five minutes for this console application toorun completely from start toofinish.</span></span>

1. <span data-ttu-id="417c8-184">toorun hello 應用程式，請使用此 Maven 命令：</span><span class="sxs-lookup"><span data-stu-id="417c8-184">toorun hello application, use this Maven command:</span></span>

    ```
    mvn compile exec:java
    ```

2. <span data-ttu-id="417c8-185">再按**Enter** toostart 刪除資源，您可能需要幾分鐘的時間 tooverify hello 建立 hello 資源 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="417c8-185">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="417c8-186">按一下 hello 部署狀態 toosee hello 部署資訊。</span><span class="sxs-lookup"><span data-stu-id="417c8-186">Click hello deployment status toosee information about hello deployment.</span></span>


## <a name="next-steps"></a><span data-ttu-id="417c8-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="417c8-187">Next steps</span></span>
* <span data-ttu-id="417c8-188">深入了解使用 hello [Azure libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview)。</span><span class="sxs-lookup"><span data-stu-id="417c8-188">Learn more about using hello [Azure libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span></span>

