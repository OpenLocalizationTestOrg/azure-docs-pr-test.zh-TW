---
title: "VM 中使用 C# 和資源管理員範本 aaaDeploy |Microsoft 文件"
description: "了解 toohow toouse C# 和資源管理員範本 toodeploy Azure VM。"
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: bfba66e8-c923-4df2-900a-0c2643b81240
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: davidmu
ms.openlocfilehash: 91d470228cfeed72336b488ffef4dfbb25bc3a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a><span data-ttu-id="aadd1-103">利用 C# 和 Resource Manager 範本來部署 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="aadd1-103">Deploy an Azure Virtual Machine using C# and a Resource Manager template</span></span>
<span data-ttu-id="aadd1-104">本文章將示範如何使用 C# 的 Azure Resource Manager 範本 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="aadd1-104">This article shows you how toodeploy an Azure Resource Manager template using C#.</span></span> <span data-ttu-id="aadd1-105">您所建立的 hello 範本部署單一虛擬機器執行 Windows Server 中具有單一子網路的新虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="aadd1-105">hello template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="aadd1-106">Hello 虛擬機器資源的詳細說明，請參閱[Azure Resource Manager 範本中的虛擬機器](template-description.md)。</span><span class="sxs-lookup"><span data-stu-id="aadd1-106">For a detailed description of hello virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="aadd1-107">如需在範本中的所有 hello 資源的詳細資訊，請參閱[Azure Resource Manager 範本逐步解說](../../azure-resource-manager/resource-manager-template-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="aadd1-107">For more information about all hello resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="aadd1-108">它會採用約 10 分鐘 toodo 這些步驟。</span><span class="sxs-lookup"><span data-stu-id="aadd1-108">It takes about 10 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="aadd1-109">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="aadd1-109">Create a Visual Studio project</span></span>

<span data-ttu-id="aadd1-110">在此步驟中，您確定已安裝 Visual Studio，並建立主控台應用程式使用 toodeploy hello 範本。</span><span class="sxs-lookup"><span data-stu-id="aadd1-110">In this step, you make sure that Visual Studio is installed and you create a console application used toodeploy hello template.</span></span>

1. <span data-ttu-id="aadd1-111">如果您尚未安裝 [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio)，請進行安裝。</span><span class="sxs-lookup"><span data-stu-id="aadd1-111">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="aadd1-112">選取**.NET 桌面開發**在 hello 工作負載頁面，然後按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="aadd1-112">Select **.NET desktop development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="aadd1-113">在 hello 摘要，您可以看到**開發工具，.NET Framework 4 4.6**會自動為您選擇。</span><span class="sxs-lookup"><span data-stu-id="aadd1-113">In hello summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="aadd1-114">如果您已安裝 Visual Studio，您可以新增使用 Visual Studio 啟動器 hello hello.NET 工作負載。</span><span class="sxs-lookup"><span data-stu-id="aadd1-114">If you have already installed Visual Studio, you can add hello .NET workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="aadd1-115">在 Visual Studio 中，按一下 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="aadd1-115">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="aadd1-116">在**範本** > **Visual C#**，選取**主控台應用程式 (.NET Framework)**，輸入*myDotnetProject* hello 名稱hello 專案中，選取 hello hello 專案位置，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="aadd1-116">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-hello-packages"></a><span data-ttu-id="aadd1-117">安裝 hello 封裝</span><span class="sxs-lookup"><span data-stu-id="aadd1-117">Install hello packages</span></span>

<span data-ttu-id="aadd1-118">NuGet 封裝是 hello 最簡單方式 tooinstall hello 程式庫，您需要 toofinish 這些步驟。</span><span class="sxs-lookup"><span data-stu-id="aadd1-118">NuGet packages are hello easiest way tooinstall hello libraries that you need toofinish these steps.</span></span> <span data-ttu-id="aadd1-119">tooget hello 程式庫，您需要在 Visual Studio 中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="aadd1-119">tooget hello libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="aadd1-120">按一下 工具 > NuGet 套件管理員，然後按一下Package Manager Console。</span><span class="sxs-lookup"><span data-stu-id="aadd1-120">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="aadd1-121">Hello 主控台中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="aadd1-121">Type these commands in hello console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-hello-files"></a><span data-ttu-id="aadd1-122">建立 hello 檔案</span><span class="sxs-lookup"><span data-stu-id="aadd1-122">Create hello files</span></span>

<span data-ttu-id="aadd1-123">在此步驟中，您會建立部署 hello 資源範本檔，以及提供參數值 toohello 範本參數檔案。</span><span class="sxs-lookup"><span data-stu-id="aadd1-123">In this step, you create a template file that deploys hello resources and a parameters file that supplies parameter values toohello template.</span></span> <span data-ttu-id="aadd1-124">您也可以建立使用的 tooperform Azure Resource Manager 作業的授權檔案。</span><span class="sxs-lookup"><span data-stu-id="aadd1-124">You also create an authorization file that is used tooperform Azure Resource Manager operations.</span></span>

### <a name="create-hello-template-file"></a><span data-ttu-id="aadd1-125">建立 hello 範本檔案</span><span class="sxs-lookup"><span data-stu-id="aadd1-125">Create hello template file</span></span>

1. <span data-ttu-id="aadd1-126">在 [方案總管] 中，於 [myDotnetProject] 上按一下滑鼠右鍵 > [新增] > [新增項目]，然後選取 [Visual C# 項目] 中的 [文字檔]。</span><span class="sxs-lookup"><span data-stu-id="aadd1-126">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="aadd1-127">名稱 hello 檔*CreateVMTemplate.json*，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="aadd1-127">Name hello file *CreateVMTemplate.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="aadd1-128">加入您建立此 JSON 程式碼 toohello 檔案：</span><span class="sxs-lookup"><span data-stu-id="aadd1-128">Add this JSON code toohello file that you created:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

3. <span data-ttu-id="aadd1-129">儲存 hello CreateVMTemplate.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="aadd1-129">Save hello CreateVMTemplate.json file.</span></span>

### <a name="create-hello-parameters-file"></a><span data-ttu-id="aadd1-130">建立 hello 參數檔案</span><span class="sxs-lookup"><span data-stu-id="aadd1-130">Create hello parameters file</span></span>

<span data-ttu-id="aadd1-131">toospecify hello hello 範本中所定義的資源參數的值，您會建立包含 hello 值的參數檔案。</span><span class="sxs-lookup"><span data-stu-id="aadd1-131">toospecify values for hello resource parameters that are defined in hello template, you create a parameters file that contains hello values.</span></span>

1. <span data-ttu-id="aadd1-132">在 [方案總管] 中，於 [myDotnetProject] 上按一下滑鼠右鍵 > [新增] > [新增項目]，然後選取 [Visual C# 項目] 中的 [文字檔]。</span><span class="sxs-lookup"><span data-stu-id="aadd1-132">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="aadd1-133">名稱 hello 檔*Parameters.json*，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="aadd1-133">Name hello file *Parameters.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="aadd1-134">加入您建立此 JSON 程式碼 toohello 檔案：</span><span class="sxs-lookup"><span data-stu-id="aadd1-134">Add this JSON code toohello file that you created:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

4. <span data-ttu-id="aadd1-135">儲存 hello Parameters.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="aadd1-135">Save hello Parameters.json file.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="aadd1-136">建立 hello 授權檔</span><span class="sxs-lookup"><span data-stu-id="aadd1-136">Create hello authorization file</span></span>

<span data-ttu-id="aadd1-137">您可以將範本部署之前，請確定您有存取 tooan [Active Directory 服務主體](../../resource-group-authenticate-service-principal.md)。</span><span class="sxs-lookup"><span data-stu-id="aadd1-137">Before you can deploy a template, make sure that you have access tooan [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span></span> <span data-ttu-id="aadd1-138">從 hello 服務主體時，您可以取得 token 來驗證要求 tooAzure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="aadd1-138">From hello service principal, you acquire a token for authenticating requests tooAzure Resource Manager.</span></span> <span data-ttu-id="aadd1-139">您也應該記錄 hello 應用程式識別碼、 hello 驗證金鑰，以及您需要在 hello 授權檔案中的 hello 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="aadd1-139">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in hello authorization file.</span></span>

1. <span data-ttu-id="aadd1-140">在 [方案總管] 中，於 [myDotnetProject] 上按一下滑鼠右鍵 > [新增] > [新增項目]，然後選取 [Visual C# 項目] 中的 [文字檔]。</span><span class="sxs-lookup"><span data-stu-id="aadd1-140">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="aadd1-141">名稱 hello 檔*azureauth.properties*，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="aadd1-141">Name hello file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="aadd1-142">新增下列授權屬性：</span><span class="sxs-lookup"><span data-stu-id="aadd1-142">Add these authorization properties:</span></span>

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

    <span data-ttu-id="aadd1-143">取代**&lt;訂用帳戶 id&gt;** 與您的訂用帳戶識別碼**&lt;應用程式識別碼&gt;**以 hello Active Directory 應用程式識別項， **&lt;驗證金鑰&gt;**與 hello 應用程式鍵，和**&lt;租用戶識別碼&gt;**與 hello 租用戶識別項。</span><span class="sxs-lookup"><span data-stu-id="aadd1-143">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

3. <span data-ttu-id="aadd1-144">儲存 hello azureauth.properties 檔案。</span><span class="sxs-lookup"><span data-stu-id="aadd1-144">Save hello azureauth.properties file.</span></span>
4. <span data-ttu-id="aadd1-145">在名為 AZURE_AUTH_LOCATION hello 完整路徑 tooauthorization 檔案所建立的 Windows 中設定環境變數，例如 hello 下列的 PowerShell 命令可以用：</span><span class="sxs-lookup"><span data-stu-id="aadd1-145">Set an environment variable in Windows named AZURE_AUTH_LOCATION with hello full path tooauthorization file that you created, for example hello following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-hello-management-client"></a><span data-ttu-id="aadd1-146">建立 hello 管理用戶端</span><span class="sxs-lookup"><span data-stu-id="aadd1-146">Create hello management client</span></span>

1. <span data-ttu-id="aadd1-147">開啟您所建立的 hello 專案 hello Program.cs 檔案，然後加入下列陳述式 toohello 現有陳述式，使用在 hello 檔案最上方：</span><span class="sxs-lookup"><span data-stu-id="aadd1-147">Open hello Program.cs file for hello project that you created, and then add these using statements toohello existing statements at top of hello file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

2. <span data-ttu-id="aadd1-148">toocreate hello 管理用戶端，新增此程式碼 toohello Main 方法：</span><span class="sxs-lookup"><span data-stu-id="aadd1-148">toocreate hello management client, add this code toohello Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="aadd1-149">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="aadd1-149">Create a resource group</span></span>

<span data-ttu-id="aadd1-150">toospecify 值 hello 應用程式中，加入程式碼 toohello Main 方法：</span><span class="sxs-lookup"><span data-stu-id="aadd1-150">toospecify values for hello application, add code toohello Main method:</span></span>

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a><span data-ttu-id="aadd1-151">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="aadd1-151">Create a storage account</span></span>

<span data-ttu-id="aadd1-152">從儲存體帳戶在 Azure 中部署 hello 範本和參數。</span><span class="sxs-lookup"><span data-stu-id="aadd1-152">hello template and parameters are deployed from a storage account in Azure.</span></span> <span data-ttu-id="aadd1-153">在此步驟中，您可以建立 hello 帳戶和 hello 檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="aadd1-153">In this step, you create hello account and upload hello files.</span></span> 

<span data-ttu-id="aadd1-154">toocreate hello 帳戶，加入此程式碼 toohello Main 方法：</span><span class="sxs-lookup"><span data-stu-id="aadd1-154">toocreate hello account, add this code toohello Main method:</span></span>

```
string storageAccountName = SdkContext.RandomResourceName("st", 10);

Console.WriteLine("Creating storage account...");
var storage = azure.StorageAccounts.Define(storageAccountName)
    .WithRegion(Region.USWest)
    .WithExistingResourceGroup(resourceGroup)
    .Create();

var storageKeys = storage.GetKeys();
string storageConnectionString = "DefaultEndpointsProtocol=https;"
    + "AccountName=" + storage.Name
    + ";AccountKey=" + storageKeys[0].Value
    + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
var serviceClient = account.CreateCloudBlobClient();

Console.WriteLine("Creating container...");
var container = serviceClient.GetContainerReference("templates");
container.CreateIfNotExistsAsync().Wait();
var containerPermissions = new BlobContainerPermissions()
    { PublicAccess = BlobContainerPublicAccessType.Container };
container.SetPermissionsAsync(containerPermissions).Wait();

Console.WriteLine("Uploading template file...");
var templateblob = container.GetBlockBlobReference("CreateVMTemplate.json");
templateblob.UploadFromFile("..\\..\\CreateVMTemplate.json");

Console.WriteLine("Uploading parameters file...");
var paramblob = container.GetBlockBlobReference("Parameters.json");
paramblob.UploadFromFile("..\\..\\Parameters.json");
```

## <a name="deploy-hello-template"></a><span data-ttu-id="aadd1-155">部署 hello 範本</span><span class="sxs-lookup"><span data-stu-id="aadd1-155">Deploy hello template</span></span>

<span data-ttu-id="aadd1-156">部署 hello 範本和參數從 hello 所建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="aadd1-156">Deploy hello template and parameters from hello storage account that was created.</span></span> 

<span data-ttu-id="aadd1-157">toodeploy hello 範本，加入此程式碼 toohello Main 方法：</span><span class="sxs-lookup"><span data-stu-id="aadd1-157">toodeploy hello template, add this code toohello Main method:</span></span>

```
var templatePath = "https://" + storageAccountName + ".blob.core.windows.net/templates/CreateVMTemplate.json";
var paramPath = "https://" + storageAccountName + ".blob.core.windows.net/templates/Parameters.json";
var deployment = azure.Deployments.Define("myDeployment")
    .WithExistingResourceGroup(groupName)
    .WithTemplateLink(templatePath, "1.0.0.0")
    .WithParametersLink(paramPath, "1.0.0.0")
    .WithMode(Microsoft.Azure.Management.ResourceManager.Fluent.Models.DeploymentMode.Incremental)
    .Create();
Console.WriteLine("Press enter toodelete hello resource group...");
Console.ReadLine();
```

## <a name="delete-hello-resources"></a><span data-ttu-id="aadd1-158">刪除 hello 資源</span><span class="sxs-lookup"><span data-stu-id="aadd1-158">Delete hello resources</span></span>

<span data-ttu-id="aadd1-159">因為您負責 Azure 中使用的資源，但它永遠是很好的作法 toodelete 資源不再需要的。</span><span class="sxs-lookup"><span data-stu-id="aadd1-159">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="aadd1-160">您不需要 toodelete 分開資源群組的每個資源。</span><span class="sxs-lookup"><span data-stu-id="aadd1-160">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="aadd1-161">刪除 hello 資源群組和其所有資源都將會自動刪除。</span><span class="sxs-lookup"><span data-stu-id="aadd1-161">Delete hello resource group and all its resources are automatically deleted.</span></span> 

<span data-ttu-id="aadd1-162">toodelete hello 資源群組中，加入此程式碼 toohello Main 方法：</span><span class="sxs-lookup"><span data-stu-id="aadd1-162">toodelete hello resource group, add this code toohello Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a><span data-ttu-id="aadd1-163">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="aadd1-163">Run hello application</span></span>

<span data-ttu-id="aadd1-164">它應該完全從開始 toofinish 此主控台應用程式 toorun 大約五分鐘。</span><span class="sxs-lookup"><span data-stu-id="aadd1-164">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> 

1. <span data-ttu-id="aadd1-165">toorun hello 主控台應用程式中，按一下 **啟動**。</span><span class="sxs-lookup"><span data-stu-id="aadd1-165">toorun hello console application, click **Start**.</span></span>

2. <span data-ttu-id="aadd1-166">再按**Enter** toostart 刪除資源，您可能需要幾分鐘的時間 tooverify hello 建立 hello 資源 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="aadd1-166">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="aadd1-167">按一下 hello 部署狀態 toosee hello 部署資訊。</span><span class="sxs-lookup"><span data-stu-id="aadd1-167">Click hello deployment status toosee information about hello deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aadd1-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aadd1-168">Next steps</span></span>
* <span data-ttu-id="aadd1-169">如果有一些與 hello 部署的問題下, 一個步驟會在 toolook[疑難排解常見的 Azure 部署錯誤與 Azure 資源管理員](../../resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="aadd1-169">If there were issues with hello deployment, a next step would be toolook at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="aadd1-170">深入了解如何 toodeploy 虛擬機器和其支援的資源，藉由檢閱[部署 Azure 虛擬機器使用 C#](csharp.md)。</span><span class="sxs-lookup"><span data-stu-id="aadd1-170">Learn how toodeploy a virtual machine and its supporting resources by reviewing [Deploy an Azure Virtual Machine Using C#](csharp.md).</span></span>
