---
title: "Operations Management Suite (OMS) 的管理解決方案中 aaaViews |Microsoft 文件"
description: "在 Operations Management Suite (OMS) 的管理解決方案通常會包含一個或多個檢視 toovisualize 資料。  本文描述如何 tooexport 來建立檢視表 hello 檢視表設計工具，並將它包含在管理解決方案。 "
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 570b278c-2d47-4e5a-9828-7f01f31ddf8c
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 303861465014a27289f831332b3d95925c0ae66d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a><span data-ttu-id="6a30d-104">Operations Management Suite (OMS) 管理解決方案中的檢視 (預覽)</span><span class="sxs-lookup"><span data-stu-id="6a30d-104">Views in Operations Management Suite (OMS) management solutions (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="6a30d-105">這是在 OMS 中建立管理解決方案 (目前處於預覽狀態) 的預備文件。</span><span class="sxs-lookup"><span data-stu-id="6a30d-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="6a30d-106">如下所述的任何結構描述是主體 toochange。</span><span class="sxs-lookup"><span data-stu-id="6a30d-106">Any schema described below is subject toochange.</span></span>    
>
>

<span data-ttu-id="6a30d-107">[在 Operations Management Suite (OMS) 的管理解決方案](operations-management-suite-solutions.md)通常會包含一個或多個檢視 toovisualize 資料。</span><span class="sxs-lookup"><span data-stu-id="6a30d-107">[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views toovisualize data.</span></span>  <span data-ttu-id="6a30d-108">本文說明如何 tooexport 來建立檢視表 hello[檢視表設計工具](../log-analytics/log-analytics-view-designer.md)並將它包含在管理解決方案中。</span><span class="sxs-lookup"><span data-stu-id="6a30d-108">This article describes how tooexport a view created by hello [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span></span>  

> [!NOTE]
> <span data-ttu-id="6a30d-109">hello 這篇文章中的範例使用參數和變數，都是必要或常見 toomanagement 解決方案中所述[Operations Management Suite (OMS) 中建立管理方案](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="6a30d-109">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="6a30d-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6a30d-110">Prerequisites</span></span>
<span data-ttu-id="6a30d-111">本文假設您已經熟悉如何太[建立管理方案](operations-management-suite-solutions-creating.md)和方案檔的 hello 結構。</span><span class="sxs-lookup"><span data-stu-id="6a30d-111">This article assumes that you're already familiar with how too[create a management solution](operations-management-suite-solutions-creating.md) and hello structure of a solution file.</span></span>

## <a name="overview"></a><span data-ttu-id="6a30d-112">概觀</span><span class="sxs-lookup"><span data-stu-id="6a30d-112">Overview</span></span>
<span data-ttu-id="6a30d-113">建立 tooinclude 管理解決方案中的檢視，**資源**中 hello[方案檔](operations-management-suite-solutions-creating.md)。</span><span class="sxs-lookup"><span data-stu-id="6a30d-113">tooinclude a view in a management solution, you create a **resource** for it in hello [solution file](operations-management-suite-solutions-creating.md).</span></span>  <span data-ttu-id="6a30d-114">hello JSON 描述 hello 檢視詳細的設定是通常複雜雖然和非，一般解決方案作者可以 toocreate 手動。</span><span class="sxs-lookup"><span data-stu-id="6a30d-114">hello JSON that describes hello view's detailed configuration is typically complex though and not something that a typical solution author would be able toocreate manually.</span></span>  <span data-ttu-id="6a30d-115">hello 最常見方法是使用 hello toocreate hello 檢視[檢視表設計工具](../log-analytics/log-analytics-view-designer.md)、 將它，匯出，然後再將它的詳細的組態 toohello 方案。</span><span class="sxs-lookup"><span data-stu-id="6a30d-115">hello most common method is toocreate hello view using hello [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration toohello solution.</span></span>

<span data-ttu-id="6a30d-116">hello 基本步驟 tooadd 檢視 tooa 方案如下所示。</span><span class="sxs-lookup"><span data-stu-id="6a30d-116">hello basic steps tooadd a view tooa solution are as follows.</span></span>  <span data-ttu-id="6a30d-117">在 hello 的以下各節將進一步詳細說明每個步驟。</span><span class="sxs-lookup"><span data-stu-id="6a30d-117">Each step is described in further detail in hello sections below.</span></span>

1. <span data-ttu-id="6a30d-118">匯出 hello 檢視 tooa 檔案。</span><span class="sxs-lookup"><span data-stu-id="6a30d-118">Export hello view tooa file.</span></span>
2. <span data-ttu-id="6a30d-119">Hello 方案中建立 hello 檢視資源。</span><span class="sxs-lookup"><span data-stu-id="6a30d-119">Create hello view resource in hello solution.</span></span>
3. <span data-ttu-id="6a30d-120">新增 hello 檢視詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6a30d-120">Add hello view details.</span></span>

## <a name="export-hello-view-tooa-file"></a><span data-ttu-id="6a30d-121">匯出 hello 檢視 tooa 檔案</span><span class="sxs-lookup"><span data-stu-id="6a30d-121">Export hello view tooa file</span></span>
<span data-ttu-id="6a30d-122">請遵循指示 hello[記錄分析檢視表設計工具](../log-analytics/log-analytics-view-designer.md)tooexport 檢視 tooa 檔案。</span><span class="sxs-lookup"><span data-stu-id="6a30d-122">Follow hello instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) tooexport a view tooa file.</span></span>  <span data-ttu-id="6a30d-123">hello 匯出的檔案將會以 JSON 格式與 hello 相同[為 hello 方案檔案的項目](operations-management-suite-solutions-solution-file.md)。</span><span class="sxs-lookup"><span data-stu-id="6a30d-123">hello exported file will be in JSON format with hello same [elements as hello solution file](operations-management-suite-solutions-solution-file.md).</span></span>  

<span data-ttu-id="6a30d-124">hello**資源**hello 檢視檔案的項目將擁有的資源類型為**Microsoft.OperationalInsights/workspaces**代表 hello OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="6a30d-124">hello **resources** element of hello view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents hello OMS workspace.</span></span>  <span data-ttu-id="6a30d-125">這個項目必須具有類型的子元素**檢視**中代表 hello 檢視，且包含詳細的設定。</span><span class="sxs-lookup"><span data-stu-id="6a30d-125">This element will have a subelement with a type of **views** that represents hello view and contains its detailed configuration.</span></span>  <span data-ttu-id="6a30d-126">您將會複製這個項目的 hello 詳細資料，並再將它複製到您的方案。</span><span class="sxs-lookup"><span data-stu-id="6a30d-126">You will copy hello details of this element and then copy it into your solution.</span></span>

## <a name="create-hello-view-resource-in-hello-solution"></a><span data-ttu-id="6a30d-127">建立 hello 方案中的 hello 檢視資源</span><span class="sxs-lookup"><span data-stu-id="6a30d-127">Create hello view resource in hello solution</span></span>
<span data-ttu-id="6a30d-128">新增下列檢視資源 toohello hello**資源**方案檔的項目。</span><span class="sxs-lookup"><span data-stu-id="6a30d-128">Add hello following view resource toohello **resources** element of your solution file.</span></span>  <span data-ttu-id="6a30d-129">這會使用您也必須新增的下述變數。</span><span class="sxs-lookup"><span data-stu-id="6a30d-129">This uses variables that are described below that you must also add.</span></span>  <span data-ttu-id="6a30d-130">請注意該 hello**儀表板**和**OverviewTile**屬性都是預留位置，您將會覆寫與 hello hello 匯出的檢視檔案從對應的屬性。</span><span class="sxs-lookup"><span data-stu-id="6a30d-130">Note that hello **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with hello corresponding properties from hello exported view file.</span></span>

    {
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
        "type": "Microsoft.OperationalInsights/workspaces/views",
        "location": "[parameters('workspaceregionId')]",
        "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
        "dependson": [
            ],
        "properties": {
            "Id": "[variables('ViewName')]",
            "Name": "[variables('ViewName')]",
            "DisplayName": "[variables('ViewName')]",
            "Description": "",
            "Author": "[variables('ViewAuthor')]",
            "Source": "Local",
            "Dashboard": ,
            "OverviewTile":
        }
    }

<span data-ttu-id="6a30d-131">新增 hello 遵循 hello 方案檔的變數 toohello 變數項目，並取代 hello 值 toothose 為您的方案。</span><span class="sxs-lookup"><span data-stu-id="6a30d-131">Add hello following variables toohello variables element of hello solution file and replace hello values toothose for your solution.</span></span>

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of hello view."
    "ViewName": "Provide a name for hello view here."


<span data-ttu-id="6a30d-132">請注意，您無法複製 hello 整個檢視資源從匯出的檢視檔案，您必須依照變更 toomake hello toowork 方案中。</span><span class="sxs-lookup"><span data-stu-id="6a30d-132">Note that you could copy hello entire view resource from your exported view file, but you would need toomake hello following changes for it toowork in your solution.</span></span>  

* <span data-ttu-id="6a30d-133">hello**類型**hello 檢視的資源需要從變更的 toobe**檢視**太**Microsoft.OperationalInsights/workspaces**。</span><span class="sxs-lookup"><span data-stu-id="6a30d-133">hello **type** for hello view resource needs toobe changed from **views** too**Microsoft.OperationalInsights/workspaces**.</span></span>
* <span data-ttu-id="6a30d-134">hello**名稱**hello 檢視資源的屬性必須變更 toobe tooinclude hello 工作區名稱。</span><span class="sxs-lookup"><span data-stu-id="6a30d-134">hello **name** property for hello view resource needs toobe changed tooinclude hello workspace name.</span></span>
* <span data-ttu-id="6a30d-135">hello hello 工作區上的相依性需要 toobe 移除，因為 hello 方案中未定義 hello 工作區的資源。</span><span class="sxs-lookup"><span data-stu-id="6a30d-135">hello dependency on hello workspace needs toobe removed since hello workspace resource isn't defined in hello solution.</span></span>
* <span data-ttu-id="6a30d-136">**DisplayName**屬性需求 toobe 加入 toohello 檢視。</span><span class="sxs-lookup"><span data-stu-id="6a30d-136">**DisplayName** property needs toobe added toohello view.</span></span>  <span data-ttu-id="6a30d-137">hello**識別碼**，**名稱**，和**DisplayName**必須全部都會相符。</span><span class="sxs-lookup"><span data-stu-id="6a30d-137">hello **Id**, **Name**, and **DisplayName** must all match.</span></span>
* <span data-ttu-id="6a30d-138">必須變更參數名稱 toomatch hello 所需的參數集。</span><span class="sxs-lookup"><span data-stu-id="6a30d-138">Parameter names must be changed toomatch hello required set of parameters.</span></span>
* <span data-ttu-id="6a30d-139">變數應 hello 方案中定義和 hello 適當的內容中使用。</span><span class="sxs-lookup"><span data-stu-id="6a30d-139">Variables should be defined in hello solution and used in hello appropriate properties.</span></span>

## <a name="add-hello-view-details"></a><span data-ttu-id="6a30d-140">新增 hello 檢視詳細資料</span><span class="sxs-lookup"><span data-stu-id="6a30d-140">Add hello view details</span></span>
<span data-ttu-id="6a30d-141">hello 檢視資源 hello 中的匯出檔案會包含兩個項目在 hello 檢視**屬性**名**儀表板**和**OverviewTile**包含 hellohello 檢視的詳細的設定。</span><span class="sxs-lookup"><span data-stu-id="6a30d-141">hello view resource in hello exported view file will contain two elements in hello **properties** element named **Dashboard** and **OverviewTile** which contain hello detailed configuration of hello view.</span></span>  <span data-ttu-id="6a30d-142">這兩個元素和其內容複製到 hello**屬性**hello 檢視資源方案檔中的項目。</span><span class="sxs-lookup"><span data-stu-id="6a30d-142">Copy these two elements and their contents into hello **properties** element of hello view resource in your solution file.</span></span>

## <a name="example"></a><span data-ttu-id="6a30d-143">範例</span><span class="sxs-lookup"><span data-stu-id="6a30d-143">Example</span></span>
<span data-ttu-id="6a30d-144">比方說，hello 下列範例會示範檢視的簡單方案檔。</span><span class="sxs-lookup"><span data-stu-id="6a30d-144">For example, hello following sample shows a simple solution file with a view.</span></span>  <span data-ttu-id="6a30d-145">省略符號 （...） 會顯示 hello**儀表板**和**OverviewTile**基於空間考量的內容。</span><span class="sxs-lookup"><span data-stu-id="6a30d-145">Ellipses (...) are shown for hello **Dashboard** and **OverviewTile** contents for space reasons.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspaceName": {
                "type": "string"
            },
            "accountName": {
                "type": "string"
            },
            "workspaceRegionId": {
                "type": "string"
            },
            "regionId": {
                "type": "string"
            },
            "pricingTier": {
                "type": "string"
            }
        },
        "variables": {
            "SolutionVersion": "1.1",
            "SolutionPublisher": "Contoso",
            "SolutionName": "Contoso Solution",
            "LogAnalyticsApiVersion": "2015-11-01-preview",
            "ViewAuthor":  "user@contoso.com",
            "ViewDescription":  "This is a sample view.",
            "ViewName":  "Contoso View"
        },
        "resources": [
            {
                "name": "[concat(variables('SolutionName'), '(' ,parameters('workspacename'), ')')]",
                "location": "[parameters('workspaceRegionId')]",
                "tags": { },
                "type": "Microsoft.OperationsManagement/solutions",
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "dependsOn": [
                    "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspacename'), '/views/', variables('ViewName'))]"
                ],
                "properties": {
                    "workspaceResourceId": "[concat(resourceGroup().id, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspacename'))]",
                    "referencedResources": [
                    ],
                    "containedResources": [
                        "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/views/', variables('ViewName'))]"
                    ]
                },
                "plan": {
                    "name": "[concat(variables('SolutionName'), '(' ,parameters('workspaceName'), ')')]",
                    "Version": "[variables('SolutionVersion')]",
                    "product": "ContosoSolution",
                    "publisher": "[variables('SolutionPublisher')]",
                    "promotionCode": ""
                }
            },
            {
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
                "type": "Microsoft.OperationalInsights/workspaces/views",
                "location": "[parameters('workspaceregionId')]",
                "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
                "dependson": [
                ],
                "properties": {
                    "Id": "[variables('ViewName')]",
                    "Name": "[variables('ViewName')]",
                    "DisplayName": "[variables('ViewName')]",
                    "Description": "[variables('ViewDescription')]",
                    "Author": "[variables('ViewAuthor')]",
                    "Source": "Local",
                    "Dashboard": ...,
                    "OverviewTile": ...
                }
            }
          ]
    }




## <a name="next-steps"></a><span data-ttu-id="6a30d-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6a30d-146">Next steps</span></span>
* <span data-ttu-id="6a30d-147">了解建立[管理解決方案](operations-management-suite-solutions-creating.md)的完整詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6a30d-147">Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).</span></span>
* <span data-ttu-id="6a30d-148">包含[管理解決方案中的自動化 Runbook](operations-management-suite-solutions-resources-automation.md)。</span><span class="sxs-lookup"><span data-stu-id="6a30d-148">Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).</span></span>
