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
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a>在 Azure 中使用 JAVA 建立並管理 Windows VM

[Azure 虛擬機器](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) 需要數個支援的 Azure 資源。 本文涵蓋使用 JAVA 建立、管理和刪除 VM 資源。 您會了解如何：

> [!div class="checklist"]
> * 建立 Maven 專案
> * 新增相依性
> * 建立認證
> * 建立資源
> * 執行管理工作
> * 刪除資源
> * 執行 hello 應用程式

它會採用約 20 分鐘 toodo 這些步驟。

## <a name="create-a-maven-project"></a>建立 Maven 專案

1. 如果尚未這麼做，請先安裝 [JAVA](http://www.oracle.com/technetwork/java/javase/downloads/index.html)。
2. 安裝 [Maven](http://maven.apache.org/download.cgi)。
3. 建立新的資料夾和 hello 專案：
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a>新增相依性

1. 在 hello`testAzureApp`資料夾中，開啟 hello`pom.xml`檔案，然後加入 hello 組建組態太&lt;專案&gt;tooenable hello 建置您的應用程式：

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

2. 加入所需的 tooaccess hello Azure Java SDK hello 依存性。

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

3. 儲存 hello 檔案。

## <a name="create-credentials"></a>建立認證

在開始此步驟之前，請確定您有存取 tooan [Active Directory 服務主體](../../azure-resource-manager/resource-group-create-service-principal-portal.md)。 您也應該在稍後步驟中，記錄 hello 應用程式識別碼、 hello 驗證金鑰，以及您需要的 hello 租用戶識別碼。

### <a name="create-hello-authorization-file"></a>建立 hello 授權檔

1. 建立名為`azureauth.properties`並加入這些屬性 tooit:

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

2. 儲存 hello 檔案。
3. 設定環境變數命名您的 shell AZURE_AUTH_LOCATION 與 hello 完整路徑 toohello 驗證檔案。

### <a name="create-hello-management-client"></a>建立 hello 管理用戶端

1. 開啟 hello`App.java`底下`src\main\java\com\fabrikam`，並確定此封裝陳述式是在 hello 最上方：

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. Hello 封裝陳述式，下方加入下列 import 陳述式：
   
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

2. toocreate hello Active Directory 認證，您需要 toomake 要求程式碼 toohello 主要將此方法加入的 hello 應用程式類別：
   
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

## <a name="create-resources"></a>建立資源

### <a name="create-hello-resource-group"></a>建立 hello 資源群組

所有資源都必須包含在[資源群組](../../azure-resource-manager/resource-group-overview.md)中。

toospecify 值 hello 應用程式並建立 hello 資源群組，請在 hello main 方法中加入此程式碼 toohello try 區塊：

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-hello-availability-set"></a>建立 hello 可用性設定組

[可用性設定組](tutorial-availability-sets.md)方便您應用程式所使用的 toomaintain hello 虛擬機器。

toocreate hello 可用性組，請在 hello main 方法中加入此程式碼 toohello try 區塊：

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-hello-public-ip-address"></a>建立 hello 公用 IP 位址

A[公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)是需要的 toocommunicate 與 hello 虛擬機器。

toocreate hello 公用 IP 位址 hello 虛擬機器，加入此程式碼 toohello try 區塊 hello main 方法中：

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-hello-virtual-network"></a>建立 hello 虛擬網路

虛擬機器必須在[虛擬網路](../../virtual-network/virtual-networks-overview.md)的子網路中。

toocreate 的子網路和虛擬網路中，加入此程式碼 toohello try 區塊 hello main 方法中：

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

### <a name="create-hello-network-interface"></a>建立 hello 網路介面

需要網路介面 toocommunicate hello 虛擬網路上的虛擬機器。

toocreate 網路介面，加入此程式碼 toohello try 區塊 hello main 方法中：

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

### <a name="create-hello-virtual-machine"></a>建立 hello 的虛擬機器

現在，您會建立所有 hello 支援的資源，您可以建立虛擬機器。

toocreate hello 虛擬機器、 在 hello main 方法中加入此程式碼 toohello try 區塊：

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
> 本教學課程中建立虛擬機器執行 hello Windows Server 作業系統版本。 toolearn 有關選取其他映像的詳細資訊請參閱[瀏覽並選取 Azure 虛擬機器映像使用 Windows PowerShell 與 hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
> 
>

如果您想 toouse 現有磁碟而非 marketplace 映像，請使用下列程式碼： 

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

## <a name="perform-management-tasks"></a>執行管理工作

在虛擬機器的 hello 生命週期，您可能想 toorun 管理工作，例如啟動、 停止或刪除虛擬機器。 此外，您可能想 toocreate 程式碼 tooautomate 重複或複雜工作。

當您以 hello VM 的任何項目需要 toodo 時，您會需要 tooget 它的執行個體。 加入這個程式碼 toohello 的 try 區塊 hello main 方法：

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-hello-vm"></a>取得 hello VM 的相關資訊

tooget 資訊 hello 虛擬機器，加入此程式碼 toohello try 區塊 hello main 方法中：

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

### <a name="stop-hello-vm"></a>停止 hello VM

您可以停止虛擬機器並保留其所有設定，但繼續 toobe 支付，或您可以停止虛擬機器和解除配置。 當解除配置虛擬機器時，與其相關聯的所有資源也都會解除配置且其計費會結束。

toostop hello 虛擬機器，而不取消配置，加入此程式碼 toohello try 區塊 hello main 方法中：

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

如果您想 toodeallocate hello 虛擬機器，變更 hello 關閉呼叫 toothis 程式碼：

```java
vm.deallocate();
```

### <a name="start-hello-vm"></a>啟動 VM hello

toostart hello 虛擬機器、 在 hello main 方法中加入此程式碼 toohello try 區塊：

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="resize-hello-vm"></a>調整大小 hello VM

決定虛擬機器的大小時，應該考慮部署的許多層面。 如需詳細資訊，請參閱 [VM 大小](sizes.md)。  

hello 虛擬機器，toochange 大小 hello main 方法中新增此程式碼 toohello try 區塊：

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>新增資料磁碟 toohello VM

tooadd 是 2 GB 的大小，資料磁碟 toohello 虛擬機器有 0，且快取類型為 ReadWrite 的 LUN，在 hello main 方法中加入此程式碼 toohello try 區塊：

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter toodelete resources...");
input.nextLine();
```

## <a name="delete-resources"></a>刪除資源

因為您負責 Azure 中使用的資源，但它永遠是很好的作法 toodelete 資源不再需要的。 如果您想 toodelete hello 虛擬機器，而且所有 hello 支援的資源，您都有 toodo 是刪除 hello 資源群組。

1. toodelete hello 資源群組中，加入此程式碼 toohello try 區塊 hello main 方法中：
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. 儲存 hello App.java 檔案。

## <a name="run-hello-application"></a>執行 hello 應用程式

它應該完全從開始 toofinish 此主控台應用程式 toorun 大約五分鐘。

1. toorun hello 應用程式，請使用此 Maven 命令：

    ```
    mvn compile exec:java
    ```

2. 再按**Enter** toostart 刪除資源，您可能需要幾分鐘的時間 tooverify hello 建立 hello 資源 hello Azure 入口網站中。 按一下 hello 部署狀態 toosee hello 部署資訊。


## <a name="next-steps"></a>後續步驟
* 深入了解使用 hello [Azure libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview)。

