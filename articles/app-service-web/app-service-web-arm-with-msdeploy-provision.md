---
title: "aaaDeploy MSDeploy 使用主機名稱與 ssl 憑證的 web 應用程式"
description: "使用 Azure Resource Manager 範本 toodeploy web 應用程式使用 MSDeploy 和設定自訂主機名稱與 SSL 憑證"
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
ms.openlocfilehash: ac13f4a7d14ae182e8e7ced5adff30491422d1e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a><span data-ttu-id="51c2f-103">使用 MSDeploy、自訂主機名稱與 SSL 憑證部署 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="51c2f-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span></span>
<span data-ttu-id="51c2f-104">本指南逐步建立端對端部署為 Azure Web 應用程式、 利用 MSDeploy，以及新增自訂主機名稱與 SSL 憑證 toohello ARM 範本。</span><span class="sxs-lookup"><span data-stu-id="51c2f-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate toohello ARM template.</span></span>

<span data-ttu-id="51c2f-105">如需關於建立範本的詳細資訊，請參閱 [編寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="51c2f-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

### <a name="create-sample-application"></a><span data-ttu-id="51c2f-106">建立範例應用程式</span><span class="sxs-lookup"><span data-stu-id="51c2f-106">Create Sample Application</span></span>
<span data-ttu-id="51c2f-107">您將部署 ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="51c2f-107">You will be deploying an ASP.NET web application.</span></span> <span data-ttu-id="51c2f-108">hello 第一個步驟是 toocreate 簡單 web 應用程式 （或您可以選擇 toouse 現有-在此情況下略過此步驟）。</span><span class="sxs-lookup"><span data-stu-id="51c2f-108">hello first step is toocreate a simple web application (or you could choose toouse an existing one - in which case you can skip this step).</span></span>

<span data-ttu-id="51c2f-109">開啟 Visual Studio 2015，然後選擇 [檔案] > [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="51c2f-109">Open Visual Studio 2015 and choose File > New Project.</span></span> <span data-ttu-id="51c2f-110">在 hello 對話方塊上選擇 Web > ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="51c2f-110">On hello dialog that appears choose Web > ASP.NET Web Application.</span></span> <span data-ttu-id="51c2f-111">在 範本選擇 Web 並選擇 hello MVC 範本。</span><span class="sxs-lookup"><span data-stu-id="51c2f-111">Under Templates choose Web and choose hello MVC template.</span></span> <span data-ttu-id="51c2f-112">選取*變更驗證類型*太*非驗證*。</span><span class="sxs-lookup"><span data-stu-id="51c2f-112">Select *Change authentication type* too*No Authentication*.</span></span> <span data-ttu-id="51c2f-113">這是只 toomake hello 範例應用程式越簡單越好。</span><span class="sxs-lookup"><span data-stu-id="51c2f-113">This is just toomake hello sample application as simple as possible.</span></span>

<span data-ttu-id="51c2f-114">此時您會有基本 ASP.Net web 應用程式準備好 toouse 做為您的部署程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="51c2f-114">At this point you will have a basic ASP.Net web app ready toouse as part of your deployment process.</span></span>

### <a name="create-msdeploy-package"></a><span data-ttu-id="51c2f-115">建立 MSDeploy 封裝</span><span class="sxs-lookup"><span data-stu-id="51c2f-115">Create MSDeploy package</span></span>
<span data-ttu-id="51c2f-116">下一個步驟是 toocreate hello 封裝 toodeploy hello web 應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="51c2f-116">Next step is toocreate hello package toodeploy hello web app tooAzure.</span></span> <span data-ttu-id="51c2f-117">toodo，儲存您的專案，然後從 hello 命令列執行 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="51c2f-117">toodo this, save your project and then run hello following from hello command line:</span></span>

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

<span data-ttu-id="51c2f-118">這會建立壓縮的封裝 hello PackageLocation 資料夾下。</span><span class="sxs-lookup"><span data-stu-id="51c2f-118">This will create a zipped package under hello PackageLocation folder.</span></span> <span data-ttu-id="51c2f-119">hello 應用程式是現在已準備 toobe 部署，您現在可以建置出 Azure Resource Manager 範本 toodo 的。</span><span class="sxs-lookup"><span data-stu-id="51c2f-119">hello application is now ready toobe deployed, which you can now build out an Azure Resource Manager template toodo that.</span></span>

### <a name="create-arm-template"></a><span data-ttu-id="51c2f-120">建立 ARM 範本</span><span class="sxs-lookup"><span data-stu-id="51c2f-120">Create ARM Template</span></span>
<span data-ttu-id="51c2f-121">首先，我們先從會建立 Web 應用程式和主控方案的基本 ARM 範本開始 (請注意，為求簡潔，並不會顯示參數和變數)。</span><span class="sxs-lookup"><span data-stu-id="51c2f-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span></span>

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

<span data-ttu-id="51c2f-122">接下來，您將需要 toomodify hello web 應用程式資源 tootake 巢狀的 MSDeploy 資源。</span><span class="sxs-lookup"><span data-stu-id="51c2f-122">Next, you will need toomodify hello web app resource tootake a nested MSDeploy resource.</span></span> <span data-ttu-id="51c2f-123">這將允許您 tooreference hello 套件之前建立，並告訴 Azure Resource Manager toouse MSDeploy toodeploy hello 封裝 toohello Azure WebApp。</span><span class="sxs-lookup"><span data-stu-id="51c2f-123">This will allow you tooreference hello package created earlier and tell Azure Resource Manager toouse MSDeploy toodeploy hello package toohello Azure WebApp.</span></span> <span data-ttu-id="51c2f-124">hello 下列範例示範使用巢狀的 hello MSDeploy 資源 hello Microsoft.Web/sites 資源：</span><span class="sxs-lookup"><span data-stu-id="51c2f-124">hello following shows hello Microsoft.Web/sites resource with hello nested MSDeploy resource:</span></span>

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

<span data-ttu-id="51c2f-125">現在您會注意到接受該 hello MSDeploy 資源**packageUri**屬性定義，如下所示：</span><span class="sxs-lookup"><span data-stu-id="51c2f-125">Now you will notice that hello MSDeploy resource takes a **packageUri** property which is defined as follows:</span></span>

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

<span data-ttu-id="51c2f-126">這**packageUri**採用 hello toohello 儲存體帳戶，您將上傳至您封裝 zip 指向儲存體帳戶 uri。</span><span class="sxs-lookup"><span data-stu-id="51c2f-126">This **packageUri** takes hello storage account uri which points toohello storage account where you will upload your package zip to.</span></span> <span data-ttu-id="51c2f-127">hello Azure 資源管理員將會利用[共用存取簽章](../storage/common/storage-dotnet-shared-access-signature-part-1.md)toopull hello 封裝向 hello 儲存體帳戶，當您部署的 hello 範本從本機。</span><span class="sxs-lookup"><span data-stu-id="51c2f-127">hello Azure Resource Manager will leverage [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) toopull hello package down locally from hello storage account when you deploy hello template.</span></span> <span data-ttu-id="51c2f-128">此程序將會自動透過 PowerShell 指令碼，將 hello 套件上傳及呼叫所需的 hello Azure 管理 API toocreate hello 金鑰並將那些 hello 範本到當做參數傳遞 (*_artifactsLocation*和*_artifactsLocationSasToken*)。</span><span class="sxs-lookup"><span data-stu-id="51c2f-128">This process will be automated via a PowerShell script that will upload hello package and call hello Azure Management API toocreate hello keys required and pass those into hello template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span></span> <span data-ttu-id="51c2f-129">您將需要 toodefine 參數 hello 資料夾和檔案名稱 hello 封裝是上傳的 toounder hello 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="51c2f-129">You will need toodefine parameters for hello folder and filename hello package is uploaded toounder hello storage container.</span></span>

<span data-ttu-id="51c2f-130">接下來，您必須在另一個巢狀的資源 toosetup hello 主機名稱繫結 tooleverage 自訂網域 tooadd。</span><span class="sxs-lookup"><span data-stu-id="51c2f-130">Next you need tooadd in another nested resource toosetup hello hostname bindings tooleverage a custom domain.</span></span> <span data-ttu-id="51c2f-131">您將第一個需要 tooensure 您擁有 hello 主機名稱，並將它設定 toobe 通過 Azure 的驗證您擁有該-請參閱[Azure App Service 中設定自訂網域名稱](app-service-web-tutorial-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="51c2f-131">You will first need tooensure that you own hello hostname and set it up toobe verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span> <span data-ttu-id="51c2f-132">完成之後，您可以新增下列 tooyour 範本 hello Microsoft.Web/sites 資源區段下的 hello:</span><span class="sxs-lookup"><span data-stu-id="51c2f-132">Once that is done you can add hello following tooyour template under hello Microsoft.Web/sites resource section:</span></span>

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

<span data-ttu-id="51c2f-133">最後您需要 tooadd 另一個最上層資源，Microsoft.Web/certificates。</span><span class="sxs-lookup"><span data-stu-id="51c2f-133">Finally you need tooadd another top level resource, Microsoft.Web/certificates.</span></span> <span data-ttu-id="51c2f-134">此資源將會包含您的 SSL 憑證，並將存在於相同的層級與您的 web 應用程式和主控計劃的 hello。</span><span class="sxs-lookup"><span data-stu-id="51c2f-134">This resource will contain your SSL certificate and will exist at hello same level as your web app and hosting plan.</span></span>

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

<span data-ttu-id="51c2f-135">您將需要 toohave 順序 tooset 此資源的有效 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="51c2f-135">You will need toohave a valid SSL certificate in order tooset up this resource.</span></span> <span data-ttu-id="51c2f-136">一旦您擁有該有效的憑證然後您需要 tooextract hello pfx 位元組做為 base64 字串。</span><span class="sxs-lookup"><span data-stu-id="51c2f-136">Once you have that valid certificate then you need tooextract hello pfx bytes as a base64 string.</span></span> <span data-ttu-id="51c2f-137">其中一個選項 tooextract 這是 toouse hello 下列 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="51c2f-137">One option tooextract this is toouse hello following PowerShell command:</span></span>

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

<span data-ttu-id="51c2f-138">接著，您無法將此做為參數 tooyour ARM 部署範本。</span><span class="sxs-lookup"><span data-stu-id="51c2f-138">You could then pass this as a parameter tooyour ARM deployment template.</span></span>

<span data-ttu-id="51c2f-139">現在已可 hello ARM 範本。</span><span class="sxs-lookup"><span data-stu-id="51c2f-139">At this point hello ARM template is ready.</span></span>

### <a name="deploy-template"></a><span data-ttu-id="51c2f-140">部署範本</span><span class="sxs-lookup"><span data-stu-id="51c2f-140">Deploy Template</span></span>
<span data-ttu-id="51c2f-141">hello 最後一個步驟是 toopiece 這全部整合至完整端對端部署。</span><span class="sxs-lookup"><span data-stu-id="51c2f-141">hello final steps are toopiece this all together into a full end-to-end deployment.</span></span> <span data-ttu-id="51c2f-142">toomake 部署更容易，您可以利用 hello **Deploy-azureresourcegroup.ps1**您建立 Azure 資源群組專案在 Visual Studio toohelp 與上傳所需要的任何成品時所加入的 PowerShell 指令碼hello 範本。</span><span class="sxs-lookup"><span data-stu-id="51c2f-142">toomake deployment easier you can leverage hello **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio toohelp with uploading of any artifacts required in hello template.</span></span> <span data-ttu-id="51c2f-143">它需要您 toohave 建立您想事先 toouse 之儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="51c2f-143">It requires you toohave created a storage account you want toouse ahead of time.</span></span> <span data-ttu-id="51c2f-144">例如，我要建立 hello package.zip toobe 上傳的共用儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="51c2f-144">For this example, I created a shared storage account for hello package.zip toobe uploaded.</span></span> <span data-ttu-id="51c2f-145">hello 指令碼將會利用 AzCopy tooupload hello 封裝 toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="51c2f-145">hello script will leverage AzCopy tooupload hello package toohello storage account.</span></span> <span data-ttu-id="51c2f-146">您傳遞您成品的資料夾位置，然後 hello 指令碼將會自動上傳該目錄 toohello，名為儲存體容器中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="51c2f-146">You pass in your artifact folder location and hello script will automatically upload all files within that directory toohello named storage container.</span></span> <span data-ttu-id="51c2f-147">在呼叫 Deploy-azureresourcegroup.ps1 之後您尚未 toothen 更新 hello SSL 繫結 toomap hello 自訂主機名稱與您的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="51c2f-147">After calling Deploy-AzureResourceGroup.ps1 you have toothen update hello SSL bindings toomap hello custom hostname with your SSL certificate.</span></span>

<span data-ttu-id="51c2f-148">下列 PowerShell 顯示 hello hello 完整部署呼叫 hello 部署-AzureResourceGroup.ps1:</span><span class="sxs-lookup"><span data-stu-id="51c2f-148">hello following PowerShell shows hello complete deployment calling hello Deploy-AzureResourceGroup.ps1:</span></span>

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script toodeploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app toobind ssl certificate toohostname. This has toobe done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

<span data-ttu-id="51c2f-149">此時您的應用程式應該已部署，您應該能夠 toobrowse tooit 透過 https://www.yourcustomdomain.com</span><span class="sxs-lookup"><span data-stu-id="51c2f-149">At this point your application should have been deployed and you should be able toobrowse tooit via https://www.yourcustomdomain.com</span></span>

