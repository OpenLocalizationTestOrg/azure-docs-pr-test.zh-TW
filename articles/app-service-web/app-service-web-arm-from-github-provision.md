---
title: "aaaDeploy web 應用程式的連結 tooa GitHub 儲存機制 |Microsoft 文件"
description: "使用 Azure Resource Manager 範本 toodeploy web 應用程式，其中包含從 GitHub 儲存機制的專案。"
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
ms.openlocfilehash: 8b23416c4c06a60991517e6ee4cd82bebc5a9d73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-linked-tooa-github-repository"></a><span data-ttu-id="9790a-103">部署 web 應用程式連結 tooa GitHub 儲存機制</span><span class="sxs-lookup"><span data-stu-id="9790a-103">Deploy a web app linked tooa GitHub repository</span></span>
<span data-ttu-id="9790a-104">本主題中，您將學習如何部署 web 應用程式的 Azure Resource Manager 範本 toocreate 連結 tooa GitHub 儲存機制中的專案。</span><span class="sxs-lookup"><span data-stu-id="9790a-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys a web app that is linked tooa project in a GitHub repository.</span></span> <span data-ttu-id="9790a-105">您將學習如何 toodefine 部署的資源，以及如何 toodefine 參數指定當 hello 執行部署。</span><span class="sxs-lookup"><span data-stu-id="9790a-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="9790a-106">您可以使用此範本為您自己的部署，或自訂它 toomeet 您的需求。</span><span class="sxs-lookup"><span data-stu-id="9790a-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="9790a-107">如需關於建立範本的詳細資訊，請參閱 [編寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="9790a-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="9790a-108">Hello 完成範本，請參閱[Web 應用程式連結 tooGitHub 範本](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="9790a-108">For hello complete template, see [Web App Linked tooGitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="9790a-109">部署內容</span><span class="sxs-lookup"><span data-stu-id="9790a-109">What you will deploy</span></span>
<span data-ttu-id="9790a-110">此範本時，您將部署包含 hello GitHub 中的專案程式碼的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9790a-110">With this template, you will deploy a web app that contains hello code from a project in GitHub.</span></span>

<span data-ttu-id="9790a-111">toorun 自動 hello 部署，請按一下下列按鈕 hello:</span><span class="sxs-lookup"><span data-stu-id="9790a-111">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="9790a-112">[![部署 tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="9790a-112">[![Deploy tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="9790a-113">參數</span><span class="sxs-lookup"><span data-stu-id="9790a-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="9790a-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="9790a-114">repoURL</span></span>
<span data-ttu-id="9790a-115">hello，其中包含 hello 專案 toodeploy GitHub 儲存機制 URL。</span><span class="sxs-lookup"><span data-stu-id="9790a-115">hello URL for GitHub repository that contains hello project toodeploy.</span></span> <span data-ttu-id="9790a-116">這個參數會包含預設值，而這個值只預期的 tooshow 您如何 tooprovide hello 儲存機制的 URL。</span><span class="sxs-lookup"><span data-stu-id="9790a-116">This parameter contains a default value but this value is only intended tooshow you how tooprovide hello URL for repository.</span></span> <span data-ttu-id="9790a-117">當測試 hello 範本，但您會想 tooprovide hello URL 您自己的儲存機制使用 hello 範本時，您可以使用此值。</span><span class="sxs-lookup"><span data-stu-id="9790a-117">You can use this value when testing hello template but you will want tooprovide hello URL your own repository when working with hello template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="9790a-118">分支</span><span class="sxs-lookup"><span data-stu-id="9790a-118">branch</span></span>
<span data-ttu-id="9790a-119">hello 儲存機制 toouse hello 應用程式部署時 hello 分支。</span><span class="sxs-lookup"><span data-stu-id="9790a-119">hello branch of hello repository toouse when deploying hello application.</span></span> <span data-ttu-id="9790a-120">hello 預設值是主要，但是您可以提供 hello hello 儲存機制中的任何分支名稱且想 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="9790a-120">hello default value is master, but you can provide hello name of any branch in hello repository that you wish toodeploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="9790a-121">資源 toodeploy</span><span class="sxs-lookup"><span data-stu-id="9790a-121">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="9790a-122">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9790a-122">Web app</span></span>
<span data-ttu-id="9790a-123">建立連結的 toohello 專案在 GitHub 中的 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9790a-123">Creates hello web app that is linked toohello project in GitHub.</span></span> 

<span data-ttu-id="9790a-124">您指定的 hello web 應用程式透過 hello hello 名稱**siteName**參數，以及透過 hello hello web 應用程式的 hello 位置**siteLocation**參數。</span><span class="sxs-lookup"><span data-stu-id="9790a-124">You specify hello name of hello web app through hello **siteName** parameter, and hello location of hello web app through hello **siteLocation** parameter.</span></span> <span data-ttu-id="9790a-125">在 hello **dependsOn**項目 hello 範本定義 hello web 應用程式做為相依於 hello 服務裝載計劃。</span><span class="sxs-lookup"><span data-stu-id="9790a-125">In hello **dependsOn** element, hello template defines hello web app as dependent on hello service hosting plan.</span></span> <span data-ttu-id="9790a-126">因為它相依於裝載計劃的 hello，hello 裝載計劃已建立完成之前，將不會建立 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9790a-126">Because it is dependent on hello hosting plan, hello web app is not created until hello hosting plan has finished being created.</span></span> <span data-ttu-id="9790a-127">hello **dependsOn**項目是使用的 toospecify 部署順序。</span><span class="sxs-lookup"><span data-stu-id="9790a-127">hello **dependsOn** element is only used toospecify deployment order.</span></span> <span data-ttu-id="9790a-128">如果您不會標示成相依於 hello 主控方案的 hello web 應用程式，Azure 資源管理程式將會嘗試 toocreate 兩個資源 hello 在相同的時間，並可能會收到錯誤如果 hello 裝載計劃之前，建立 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9790a-128">If you do not mark hello web app as dependent on hello hosting plan, Azure Resource Mananger will attempt toocreate both resources at hello same time and you may receive an error if hello web app is created before hello hosting plan.</span></span>

<span data-ttu-id="9790a-129">hello web 應用程式也有定義中的子資源**資源**下一節。</span><span class="sxs-lookup"><span data-stu-id="9790a-129">hello web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="9790a-130">此子資源定義與 hello web 應用程式部署的 hello 專案的原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="9790a-130">This child resource defines source control for hello project deployed with hello web app.</span></span> <span data-ttu-id="9790a-131">在此範本中，便連結的 tooa 特定 GitHub 儲存機制 hello 原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="9790a-131">In this template, hello source control is linked tooa particular GitHub repository.</span></span> <span data-ttu-id="9790a-132">hello GitHub 儲存機制以 hello 程式碼定義**"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"**想 toocreate 重複部署範本時，可能硬式編碼 hello 儲存機制 URL同時需要 hello 最少參數數目的單一專案。</span><span class="sxs-lookup"><span data-stu-id="9790a-132">hello GitHub repository is defined with hello code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code hello repository URL when you want toocreate a template that repeatedly deploys a single project while requiring hello minimum number of parameters.</span></span>
<span data-ttu-id="9790a-133">而不是硬式編碼 hello 儲存機制 URL，您可以將參數加入 hello 儲存機制 url，並使用該值 hello **RepoUrl**屬性。</span><span class="sxs-lookup"><span data-stu-id="9790a-133">Instead of hard-coding hello repository URL, you can add a parameter for hello repository URL and use that value for hello **RepoUrl** property.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="9790a-134">命令 toorun 部署</span><span class="sxs-lookup"><span data-stu-id="9790a-134">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="9790a-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9790a-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="9790a-136">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9790a-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="9790a-137">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9790a-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="9790a-138">如需 hello 參數 JSON 檔案的內容，請參閱[azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json)。</span><span class="sxs-lookup"><span data-stu-id="9790a-138">For content of hello parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>

