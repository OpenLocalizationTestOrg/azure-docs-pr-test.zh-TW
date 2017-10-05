---
title: "部署連結至 GitHub 儲存機制的 Web 應用程式 | Microsoft Docs"
description: "使用 Azure 資源管理員範本來部署 Web 應用程式，其中包含 GitHub 儲存機制的專案。"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 32739607-85fe-43c8-a4dc-1feb46d93a4d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: 77064802814296d0c21f004534e4264d2f97252e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-web-app-linked-to-a-github-repository"></a><span data-ttu-id="d50a5-103">部署連結至 GitHub 儲存機制的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d50a5-103">Deploy a web app linked to a GitHub repository</span></span>
<span data-ttu-id="d50a5-104">在本主題中，您將學習如何建立 Azure 資源管理員範本，以部署連結至 GitHub 儲存機制中之專案的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d50a5-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys a web app that is linked to a project in a GitHub repository.</span></span> <span data-ttu-id="d50a5-105">您將學習如何定義要部署哪些資源，以及如何定義執行部署時所指定的參數。</span><span class="sxs-lookup"><span data-stu-id="d50a5-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="d50a5-106">您可以直接在自己的部署中使用此範本，或自訂此範本以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="d50a5-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="d50a5-107">如需關於建立範本的詳細資訊，請參閱 [編寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="d50a5-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="d50a5-108">如需完整的範本，請參閱 [連結至 GitHub 的 Web 應用程式範本](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="d50a5-108">For the complete template, see [Web App Linked to GitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="d50a5-109">部署內容</span><span class="sxs-lookup"><span data-stu-id="d50a5-109">What you will deploy</span></span>
<span data-ttu-id="d50a5-110">使用此範本時，您將會部署 Web 應用程式，其中包含 GitHub 中之專案的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d50a5-110">With this template, you will deploy a web app that contains the code from a project in GitHub.</span></span>

<span data-ttu-id="d50a5-111">若要自動執行部署，請按一下下列按鈕：</span><span class="sxs-lookup"><span data-stu-id="d50a5-111">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="d50a5-112">[![部署至 Azure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="d50a5-112">[![Deploy to Azure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="d50a5-113">參數</span><span class="sxs-lookup"><span data-stu-id="d50a5-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="d50a5-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="d50a5-114">repoURL</span></span>
<span data-ttu-id="d50a5-115">包含要部署之專案的 GitHub 儲存機制 URL。</span><span class="sxs-lookup"><span data-stu-id="d50a5-115">The URL for GitHub repository that contains the project to deploy.</span></span> <span data-ttu-id="d50a5-116">此參數包含預設值，但是這個值只用來示範如何提供儲存機制 URL。</span><span class="sxs-lookup"><span data-stu-id="d50a5-116">This parameter contains a default value but this value is only intended to show you how to provide the URL for repository.</span></span> <span data-ttu-id="d50a5-117">測試範本時，您可以使用此值，但您在使用範本時將會想要提供專屬儲存機制的 URL。</span><span class="sxs-lookup"><span data-stu-id="d50a5-117">You can use this value when testing the template but you will want to provide the URL your own repository when working with the template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="d50a5-118">分支</span><span class="sxs-lookup"><span data-stu-id="d50a5-118">branch</span></span>
<span data-ttu-id="d50a5-119">要在部署應用程式時使用之儲存機制的分支。</span><span class="sxs-lookup"><span data-stu-id="d50a5-119">The branch of the repository to use when deploying the application.</span></span> <span data-ttu-id="d50a5-120">預設值是 master，但是您可以提供想要部署之儲存機制中任何分支的名稱。</span><span class="sxs-lookup"><span data-stu-id="d50a5-120">The default value is master, but you can provide the name of any branch in the repository that you wish to deploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="d50a5-121">要部署的資源</span><span class="sxs-lookup"><span data-stu-id="d50a5-121">Resources to deploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="d50a5-122">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d50a5-122">Web app</span></span>
<span data-ttu-id="d50a5-123">建立連結至 GitHub 中之專案的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d50a5-123">Creates the web app that is linked to the project in GitHub.</span></span> 

<span data-ttu-id="d50a5-124">透過 **siteName** 參數指定 Web 應用程式的名稱，透過 **siteLocation** 參數指定 Web 應用程式的位置。</span><span class="sxs-lookup"><span data-stu-id="d50a5-124">You specify the name of the web app through the **siteName** parameter, and the location of the web app through the **siteLocation** parameter.</span></span> <span data-ttu-id="d50a5-125">在 **dependsOn** 元素中，範本會將 Web 應用程式定義為依存於服務主控方案。</span><span class="sxs-lookup"><span data-stu-id="d50a5-125">In the **dependsOn** element, the template defines the web app as dependent on the service hosting plan.</span></span> <span data-ttu-id="d50a5-126">因為它依存於主控方案，所以在建立好主控方案前將不會建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d50a5-126">Because it is dependent on the hosting plan, the web app is not created until the hosting plan has finished being created.</span></span> <span data-ttu-id="d50a5-127">**dependsOn** 元素只能用來指定部署順序。</span><span class="sxs-lookup"><span data-stu-id="d50a5-127">The **dependsOn** element is only used to specify deployment order.</span></span> <span data-ttu-id="d50a5-128">如果您未將 Web 應用程式標示為依存於主控方案，Azure 資源管理員會嘗試同時建立這兩個資源，如果比主控方案早一步建立 Web 應用程式，您可能會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="d50a5-128">If you do not mark the web app as dependent on the hosting plan, Azure Resource Mananger will attempt to create both resources at the same time and you may receive an error if the web app is created before the hosting plan.</span></span>

<span data-ttu-id="d50a5-129">此 Web 應用程式也有子資源，定義在 [資源] 區段下。</span><span class="sxs-lookup"><span data-stu-id="d50a5-129">The web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="d50a5-130">此子資源會定義使用 Web 應用程式部署之專案的原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="d50a5-130">This child resource defines source control for the project deployed with the web app.</span></span> <span data-ttu-id="d50a5-131">在此範本中，原始檔控制會連結到特定的 GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="d50a5-131">In this template, the source control is linked to a particular GitHub repository.</span></span> <span data-ttu-id="d50a5-132">GitHub 儲存機制是以程式碼 **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** 來定義。若您想要以只需最少量參數的方式建立可重複部署單一專案的範本，則可將儲存機制 URL 硬式編碼。</span><span class="sxs-lookup"><span data-stu-id="d50a5-132">The GitHub repository is defined with the code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code the repository URL when you want to create a template that repeatedly deploys a single project while requiring the minimum number of parameters.</span></span>
<span data-ttu-id="d50a5-133">若不想將儲存機制 URL 硬式編碼，您也可以新增儲存機制 URL 的參數，並在 **RepoUrl** 屬性使用該值。</span><span class="sxs-lookup"><span data-stu-id="d50a5-133">Instead of hard-coding the repository URL, you can add a parameter for the repository URL and use that value for the **RepoUrl** property.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
      ],
      "properties": {
        "serverFarmId": "[parameters('hostingPlanName')]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/Sites', parameters('siteName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('repoURL')]",
            "branch": "[parameters('branch')]",
            "IsManualIntegration": true
          }
        }
      ]
    }

## <a name="commands-to-run-deployment"></a><span data-ttu-id="d50a5-134">執行部署的命令</span><span class="sxs-lookup"><span data-stu-id="d50a5-134">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="d50a5-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d50a5-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="d50a5-136">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d50a5-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="d50a5-137">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d50a5-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="d50a5-138">如需參數 JSON 檔案的內容，請參閱 [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json)。</span><span class="sxs-lookup"><span data-stu-id="d50a5-138">For content of the parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>

