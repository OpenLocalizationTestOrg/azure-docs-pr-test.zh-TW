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
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a>使用 MSDeploy、自訂主機名稱與 SSL 憑證部署 Web 應用程式
本指南逐步建立端對端部署為 Azure Web 應用程式、 利用 MSDeploy，以及新增自訂主機名稱與 SSL 憑證 toohello ARM 範本。

如需關於建立範本的詳細資訊，請參閱 [編寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。

### <a name="create-sample-application"></a>建立範例應用程式
您將部署 ASP.NET Web 應用程式。 hello 第一個步驟是 toocreate 簡單 web 應用程式 （或您可以選擇 toouse 現有-在此情況下略過此步驟）。

開啟 Visual Studio 2015，然後選擇 [檔案] > [新增專案]。 在 hello 對話方塊上選擇 Web > ASP.NET Web 應用程式。 在 範本選擇 Web 並選擇 hello MVC 範本。 選取*變更驗證類型*太*非驗證*。 這是只 toomake hello 範例應用程式越簡單越好。

此時您會有基本 ASP.Net web 應用程式準備好 toouse 做為您的部署程序的一部分。

### <a name="create-msdeploy-package"></a>建立 MSDeploy 封裝
下一個步驟是 toocreate hello 封裝 toodeploy hello web 應用程式 tooAzure。 toodo，儲存您的專案，然後從 hello 命令列執行 hello 下列：

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

這會建立壓縮的封裝 hello PackageLocation 資料夾下。 hello 應用程式是現在已準備 toobe 部署，您現在可以建置出 Azure Resource Manager 範本 toodo 的。

### <a name="create-arm-template"></a>建立 ARM 範本
首先，我們先從會建立 Web 應用程式和主控方案的基本 ARM 範本開始 (請注意，為求簡潔，並不會顯示參數和變數)。

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

接下來，您將需要 toomodify hello web 應用程式資源 tootake 巢狀的 MSDeploy 資源。 這將允許您 tooreference hello 套件之前建立，並告訴 Azure Resource Manager toouse MSDeploy toodeploy hello 封裝 toohello Azure WebApp。 hello 下列範例示範使用巢狀的 hello MSDeploy 資源 hello Microsoft.Web/sites 資源：

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

現在您會注意到接受該 hello MSDeploy 資源**packageUri**屬性定義，如下所示：

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

這**packageUri**採用 hello toohello 儲存體帳戶，您將上傳至您封裝 zip 指向儲存體帳戶 uri。 hello Azure 資源管理員將會利用[共用存取簽章](../storage/common/storage-dotnet-shared-access-signature-part-1.md)toopull hello 封裝向 hello 儲存體帳戶，當您部署的 hello 範本從本機。 此程序將會自動透過 PowerShell 指令碼，將 hello 套件上傳及呼叫所需的 hello Azure 管理 API toocreate hello 金鑰並將那些 hello 範本到當做參數傳遞 (*_artifactsLocation*和*_artifactsLocationSasToken*)。 您將需要 toodefine 參數 hello 資料夾和檔案名稱 hello 封裝是上傳的 toounder hello 儲存體容器。

接下來，您必須在另一個巢狀的資源 toosetup hello 主機名稱繫結 tooleverage 自訂網域 tooadd。 您將第一個需要 tooensure 您擁有 hello 主機名稱，並將它設定 toobe 通過 Azure 的驗證您擁有該-請參閱[Azure App Service 中設定自訂網域名稱](app-service-web-tutorial-custom-domain.md)。 完成之後，您可以新增下列 tooyour 範本 hello Microsoft.Web/sites 資源區段下的 hello:

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

最後您需要 tooadd 另一個最上層資源，Microsoft.Web/certificates。 此資源將會包含您的 SSL 憑證，並將存在於相同的層級與您的 web 應用程式和主控計劃的 hello。

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

您將需要 toohave 順序 tooset 此資源的有效 SSL 憑證。 一旦您擁有該有效的憑證然後您需要 tooextract hello pfx 位元組做為 base64 字串。 其中一個選項 tooextract 這是 toouse hello 下列 PowerShell 命令：

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

接著，您無法將此做為參數 tooyour ARM 部署範本。

現在已可 hello ARM 範本。

### <a name="deploy-template"></a>部署範本
hello 最後一個步驟是 toopiece 這全部整合至完整端對端部署。 toomake 部署更容易，您可以利用 hello **Deploy-azureresourcegroup.ps1**您建立 Azure 資源群組專案在 Visual Studio toohelp 與上傳所需要的任何成品時所加入的 PowerShell 指令碼hello 範本。 它需要您 toohave 建立您想事先 toouse 之儲存體帳戶。 例如，我要建立 hello package.zip toobe 上傳的共用儲存體帳戶。 hello 指令碼將會利用 AzCopy tooupload hello 封裝 toohello 儲存體帳戶。 您傳遞您成品的資料夾位置，然後 hello 指令碼將會自動上傳該目錄 toohello，名為儲存體容器中的所有檔案。 在呼叫 Deploy-azureresourcegroup.ps1 之後您尚未 toothen 更新 hello SSL 繫結 toomap hello 自訂主機名稱與您的 SSL 憑證。

下列 PowerShell 顯示 hello hello 完整部署呼叫 hello 部署-AzureResourceGroup.ps1:

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

此時您的應用程式應該已部署，您應該能夠 toobrowse tooit 透過 https://www.yourcustomdomain.com

