---
title: "使用 MSDeploy、主機名稱與 SSL 憑證部署 Web 應用程式"
description: "使用 Azure 資源管理員範本，透過 MSDeploy 及藉由設定自訂主機名稱與 SSL 憑證來部署 Web 應用程式"
services: app-service\web
manager: erikre
documentationcenter: 
author: jodehavi
ms.assetid: 66366a72-cef7-4d75-8779-f4d32ed33cf7
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2016
ms.author: jodehavi
ms.openlocfilehash: a0e944d0d74ecb72a919538d54db330cbbdeef64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a><span data-ttu-id="8bb38-103">使用 MSDeploy、自訂主機名稱與 SSL 憑證部署 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="8bb38-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span></span>
<span data-ttu-id="8bb38-104">本指南將逐步說明如何利用 MSDeploy，以及將自訂主機名稱和 SSL 憑證新增至 ARM 範本，以建立 Azure Web 應用程式的端對端部署。</span><span class="sxs-lookup"><span data-stu-id="8bb38-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate to the ARM template.</span></span>

<span data-ttu-id="8bb38-105">如需關於建立範本的詳細資訊，請參閱 [編寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="8bb38-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

### <a name="create-sample-application"></a><span data-ttu-id="8bb38-106">建立範例應用程式</span><span class="sxs-lookup"><span data-stu-id="8bb38-106">Create Sample Application</span></span>
<span data-ttu-id="8bb38-107">您將部署 ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8bb38-107">You will be deploying an ASP.NET web application.</span></span> <span data-ttu-id="8bb38-108">第一個步驟是建立簡單的 Web 應用程式 (或者，您可以選擇使用現有的應用程式；若是如此，您可以略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="8bb38-108">The first step is to create a simple web application (or you could choose to use an existing one - in which case you can skip this step).</span></span>

<span data-ttu-id="8bb38-109">開啟 Visual Studio 2015，然後選擇 [檔案] > [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="8bb38-109">Open Visual Studio 2015 and choose File > New Project.</span></span> <span data-ttu-id="8bb38-110">在出現的對話方塊上，選擇 [Web] > [ASP.NET Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8bb38-110">On the dialog that appears choose Web > ASP.NET Web Application.</span></span> <span data-ttu-id="8bb38-111">在 [範本] 下選擇 [Web]，然後選擇 MVC 範本。</span><span class="sxs-lookup"><span data-stu-id="8bb38-111">Under Templates choose Web and choose the MVC template.</span></span> <span data-ttu-id="8bb38-112">將 [變更驗證類型] 設定為 [不需要驗證]。</span><span class="sxs-lookup"><span data-stu-id="8bb38-112">Select *Change authentication type* to *No Authentication*.</span></span> <span data-ttu-id="8bb38-113">這是為了讓範例應用程式盡可能簡單。</span><span class="sxs-lookup"><span data-stu-id="8bb38-113">This is just to make the sample application as simple as possible.</span></span>

<span data-ttu-id="8bb38-114">此時，您將會有已備妥而可在部署程序中使用的基本 ASP.Net Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8bb38-114">At this point you will have a basic ASP.Net web app ready to use as part of your deployment process.</span></span>

### <a name="create-msdeploy-package"></a><span data-ttu-id="8bb38-115">建立 MSDeploy 封裝</span><span class="sxs-lookup"><span data-stu-id="8bb38-115">Create MSDeploy package</span></span>
<span data-ttu-id="8bb38-116">下一個步驟是建立用以將 Web 應用程式部署至 Azure 的封裝。</span><span class="sxs-lookup"><span data-stu-id="8bb38-116">Next step is to create the package to deploy the web app to Azure.</span></span> <span data-ttu-id="8bb38-117">若要這樣做，請儲存您的專案，然後從命令列中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="8bb38-117">To do this, save your project and then run the following from the command line:</span></span>

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

<span data-ttu-id="8bb38-118">這將會在 PackageLocation 資料夾下建立壓縮的封裝。</span><span class="sxs-lookup"><span data-stu-id="8bb38-118">This will create a zipped package under the PackageLocation folder.</span></span> <span data-ttu-id="8bb38-119">應用程式現在已可供部署；您現在可以建置 Azure 資源管理員範本來執行此作業。</span><span class="sxs-lookup"><span data-stu-id="8bb38-119">The application is now ready to be deployed, which you can now build out an Azure Resource Manager template to do that.</span></span>

### <a name="create-arm-template"></a><span data-ttu-id="8bb38-120">建立 ARM 範本</span><span class="sxs-lookup"><span data-stu-id="8bb38-120">Create ARM Template</span></span>
<span data-ttu-id="8bb38-121">首先，我們先從會建立 Web 應用程式和主控方案的基本 ARM 範本開始 (請注意，為求簡潔，並不會顯示參數和變數)。</span><span class="sxs-lookup"><span data-stu-id="8bb38-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span></span>

    {
        "name": "[parameters('appServicePlanName')]",
        "type": "Microsoft.Web/serverfarms",
        "location": "[resourceGroup().location]",
        "apiVersion": "2014-06-01",
        "dependsOn": [ ],
        "tags": {
            "displayName": "appServicePlan"
        },
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "sku": "[parameters('appServicePlanSKU')]",
            "workerSize": "[parameters('appServicePlanWorkerSize')]",
            "numberOfWorkers": 1
        }
    },
    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        }
    }

<span data-ttu-id="8bb38-122">接下來，您必須修改 Web 應用程式資源，以取用巢狀 MSDeploy 資源。</span><span class="sxs-lookup"><span data-stu-id="8bb38-122">Next, you will need to modify the web app resource to take a nested MSDeploy resource.</span></span> <span data-ttu-id="8bb38-123">這可讓您參考稍早建立的封裝，並指示 Azure 資源管理員使用 MSDeploy 將封裝部署至 Azure WebApp。</span><span class="sxs-lookup"><span data-stu-id="8bb38-123">This will allow you to reference the package created earlier and tell Azure Resource Manager to use MSDeploy to deploy the package to the Azure WebApp.</span></span> <span data-ttu-id="8bb38-124">以下顯示具有巢狀 MSDeploy 資源的 Microsoft.Web/網站資源：</span><span class="sxs-lookup"><span data-stu-id="8bb38-124">The following shows the Microsoft.Web/sites resource with the nested MSDeploy resource:</span></span>

    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        },
        "resources": [
            {
                "name": "MSDeploy",
                "type": "extensions",
                "location": "[resourceGroup().location]",
                "apiVersion": "2015-08-01",
                "dependsOn": [
                    "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
                ],
                "tags": {
                    "displayName": "webDeploy"
                },
                "properties": {
                    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]",
                    "dbType": "None",
                    "connectionString": "",
                    "setParameters": {
                        "IIS Web Application Name": "[variables('webAppName')]"
                    }
                }
            }
        ]
    }

<span data-ttu-id="8bb38-125">現在您會注意到 MSDeploy 資源取用定義如下的 **packageUri** 屬性：</span><span class="sxs-lookup"><span data-stu-id="8bb38-125">Now you will notice that the MSDeploy resource takes a **packageUri** property which is defined as follows:</span></span>

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

<span data-ttu-id="8bb38-126">此 **packageUri** 會取用一個儲存體帳戶 URI，該 URI 指向您的封裝 zip 所將上傳到的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8bb38-126">This **packageUri** takes the storage account uri which points to the storage account where you will upload your package zip to.</span></span> <span data-ttu-id="8bb38-127">當您部署範本時，Azure 資源管理員會利用 [共用存取簽章](../storage/common/storage-dotnet-shared-access-signature-part-1.md) 從儲存體帳戶將封裝提取到本機。</span><span class="sxs-lookup"><span data-stu-id="8bb38-127">The Azure Resource Manager will leverage [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) to pull the package down locally from the storage account when you deploy the template.</span></span> <span data-ttu-id="8bb38-128">此程序就會透過 PowerShell 指令碼而自動化，將封裝上傳，並呼叫 Azure 管理 API，以建立所需的金鑰，並將其傳入範本中做為參數 (_artifactsLocation 和 _artifactsLocationSasToken)。</span><span class="sxs-lookup"><span data-stu-id="8bb38-128">This process will be automated via a PowerShell script that will upload the package and call the Azure Management API to create the keys required and pass those into the template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span></span> <span data-ttu-id="8bb38-129">您將必須針對封裝在儲存體容器下所將上傳到的資料夾和檔案名稱定義參數。</span><span class="sxs-lookup"><span data-stu-id="8bb38-129">You will need to define parameters for the folder and filename the package is uploaded to under the storage container.</span></span>

<span data-ttu-id="8bb38-130">接著，您必須在其他巢狀資源中新增，以設定主機名稱繫結來利用自訂網域。</span><span class="sxs-lookup"><span data-stu-id="8bb38-130">Next you need to add in another nested resource to setup the hostname bindings to leverage a custom domain.</span></span> <span data-ttu-id="8bb38-131">首先，您必須確定您擁有主機名稱，然後加以設定，使其由 Azure 驗證您具有其所有權 - 請參閱 [在 Azure App Service 中設定自訂網域名稱](app-service-web-tutorial-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="8bb38-131">You will first need to ensure that you own the hostname and set it up to be verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span> <span data-ttu-id="8bb38-132">完成此動作後，您可以在 Microsoft.Web/網站資源區段下新增下列項目：</span><span class="sxs-lookup"><span data-stu-id="8bb38-132">Once that is done you can add the following to your template under the Microsoft.Web/sites resource section:</span></span>

    {
        "apiVersion": "2015-08-01",
        "type": "hostNameBindings",
        "name": "www.yourcustomdomain.com",
        "dependsOn": [
            "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
        ],
        "properties": {
            "domainId": null,
            "hostNameType": "Verified",
            "siteName": "variables('webAppName')"
        }
    }

<span data-ttu-id="8bb38-133">最後，您必須新增另一項最上層資源 Microsoft.Web/憑證。</span><span class="sxs-lookup"><span data-stu-id="8bb38-133">Finally you need to add another top level resource, Microsoft.Web/certificates.</span></span> <span data-ttu-id="8bb38-134">此資源將包含您的 SSL 憑證，且會與 Web 應用程式和主控方案存在於相同的層級。</span><span class="sxs-lookup"><span data-stu-id="8bb38-134">This resource will contain your SSL certificate and will exist at the same level as your web app and hosting plan.</span></span>

    {
        "name": "[parameters('certificateName')]",
        "apiVersion": "2014-04-01",
        "type": "Microsoft.Web/certificates",
        "location": "[resourceGroup().location]",
        "properties": {
            "pfxBlob": "pfx base64 blob",
            "password": "some pass"
        }
    }

<span data-ttu-id="8bb38-135">您必須具備有效的 SSL 憑證，才能設定這項資源。</span><span class="sxs-lookup"><span data-stu-id="8bb38-135">You will need to have a valid SSL certificate in order to set up this resource.</span></span> <span data-ttu-id="8bb38-136">如果您已具備有效憑證，接著必須要以 base64 字串的形式擷取 pfx 位元組。</span><span class="sxs-lookup"><span data-stu-id="8bb38-136">Once you have that valid certificate then you need to extract the pfx bytes as a base64 string.</span></span> <span data-ttu-id="8bb38-137">要擷取此項目，使用下列 PowerShell 命令是選項之一：</span><span class="sxs-lookup"><span data-stu-id="8bb38-137">One option to extract this is to use the following PowerShell command:</span></span>

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

<span data-ttu-id="8bb38-138">接著，您可以將此項目傳遞至 ARM 部署範本做為參數。</span><span class="sxs-lookup"><span data-stu-id="8bb38-138">You could then pass this as a parameter to your ARM deployment template.</span></span>

<span data-ttu-id="8bb38-139">至此，ARM 範本已準備就緒。</span><span class="sxs-lookup"><span data-stu-id="8bb38-139">At this point the ARM template is ready.</span></span>

### <a name="deploy-template"></a><span data-ttu-id="8bb38-140">部署範本</span><span class="sxs-lookup"><span data-stu-id="8bb38-140">Deploy Template</span></span>
<span data-ttu-id="8bb38-141">最後的步驟是將各個項目整合為完整的端對端部署。</span><span class="sxs-lookup"><span data-stu-id="8bb38-141">The final steps are to piece this all together into a full end-to-end deployment.</span></span> <span data-ttu-id="8bb38-142">若要簡化部署，您可以利用您在 Visual Studio 中建立 Azure 資源群組專案時所新增的 **Deploy-AzureResourceGroup.ps1** PowerShell 指令碼，來上傳範本中所需的任何構件。</span><span class="sxs-lookup"><span data-stu-id="8bb38-142">To make deployment easier you can leverage the **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio to help with uploading of any artifacts required in the template.</span></span> <span data-ttu-id="8bb38-143">若要這麼做，您必須事先建立您要使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8bb38-143">It requires you to have created a storage account you want to use ahead of time.</span></span> <span data-ttu-id="8bb38-144">在此範例中，我針對要上傳的 package.zip 建立了共用儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8bb38-144">For this example, I created a shared storage account for the package.zip to be uploaded.</span></span> <span data-ttu-id="8bb38-145">指令碼會利用 AzCopy 將封裝上傳至儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8bb38-145">The script will leverage AzCopy to upload the package to the storage account.</span></span> <span data-ttu-id="8bb38-146">在您傳入構件資料夾位置後，指令碼會自動將該目錄中的所有檔案上傳至指定的儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="8bb38-146">You pass in your artifact folder location and the script will automatically upload all files within that directory to the named storage container.</span></span> <span data-ttu-id="8bb38-147">在呼叫 Deploy-AzureResourceGroup.ps1 之後，您必須更新 SSL 繫結，以對應自訂主機名稱與您的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="8bb38-147">After calling Deploy-AzureResourceGroup.ps1 you have to then update the SSL bindings to map the custom hostname with your SSL certificate.</span></span>

<span data-ttu-id="8bb38-148">下列 PowerShell 顯示呼叫 Deploy-AzureResourceGroup.ps1 的完整部署：</span><span class="sxs-lookup"><span data-stu-id="8bb38-148">The following PowerShell shows the complete deployment calling the Deploy-AzureResourceGroup.ps1:</span></span>

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script to deploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app to bind ssl certificate to hostname. This has to be done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

<span data-ttu-id="8bb38-149">此時，您的應用程式應已部署，且您應能夠透過 https://www.yourcustomdomain.com 加以瀏覽</span><span class="sxs-lookup"><span data-stu-id="8bb38-149">At this point your application should have been deployed and you should be able to browse to it via https://www.yourcustomdomain.com</span></span>

