---
title: "Operations Management Suite (OMS) 管理解決方案中的檢視 | Microsoft Docs"
description: "Operations Management Suite (OMS) 中的管理解決方案通常包含一或多個檢視，以將資料視覺化。  本文說明如何匯出檢視設計工具所建立的檢視並將它納入管理解決方案中。 "
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
ms.openlocfilehash: 533b5564a805e0b41f2b1a4ad92e12b133220952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a><span data-ttu-id="869c2-104">Operations Management Suite (OMS) 管理解決方案中的檢視 (預覽)</span><span class="sxs-lookup"><span data-stu-id="869c2-104">Views in Operations Management Suite (OMS) management solutions (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="869c2-105">這是在 OMS 中建立管理解決方案 (目前處於預覽狀態) 的預備文件。</span><span class="sxs-lookup"><span data-stu-id="869c2-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="869c2-106">以下所述的任何結構描述可能會有所變更。</span><span class="sxs-lookup"><span data-stu-id="869c2-106">Any schema described below is subject to change.</span></span>    
>
>

<span data-ttu-id="869c2-107">[Operations Management Suite (OMS) 中的管理解決方案](operations-management-suite-solutions.md)通常包含一或多個檢視，以將資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="869c2-107">[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views to visualize data.</span></span>  <span data-ttu-id="869c2-108">本文說明如何匯出[檢視設計工具](../log-analytics/log-analytics-view-designer.md)所建立的檢視並將它納入管理解決方案中。</span><span class="sxs-lookup"><span data-stu-id="869c2-108">This article describes how to export a view created by the [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span></span>  

> [!NOTE]
> <span data-ttu-id="869c2-109">本文中的範例使用管理解決方案所必要或通用的參數和變數，如[在 Operations Management Suite (OMS) 中建立管理解決方案](operations-management-suite-solutions-creating.md)所述。</span><span class="sxs-lookup"><span data-stu-id="869c2-109">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="869c2-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="869c2-110">Prerequisites</span></span>
<span data-ttu-id="869c2-111">本文假設您已經熟悉如何[建立管理解決方案](operations-management-suite-solutions-creating.md)和方案檔的結構。</span><span class="sxs-lookup"><span data-stu-id="869c2-111">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of a solution file.</span></span>

## <a name="overview"></a><span data-ttu-id="869c2-112">Overview</span><span class="sxs-lookup"><span data-stu-id="869c2-112">Overview</span></span>
<span data-ttu-id="869c2-113">若要在管理解決方案中納入檢視，您可在[方案檔](operations-management-suite-solutions-creating.md)中建立其**資源**。</span><span class="sxs-lookup"><span data-stu-id="869c2-113">To include a view in a management solution, you create a **resource** for it in the [solution file](operations-management-suite-solutions-creating.md).</span></span>  <span data-ttu-id="869c2-114">說明檢視詳細組態的 JSON 通常很複雜，典型方案作者無法以手動方式建立。</span><span class="sxs-lookup"><span data-stu-id="869c2-114">The JSON that describes the view's detailed configuration is typically complex though and not something that a typical solution author would be able to create manually.</span></span>  <span data-ttu-id="869c2-115">最常見的方法是使用[檢視設計工具](../log-analytics/log-analytics-view-designer.md)建立檢視、加以匯出，然後將其詳細組態新增至方案。</span><span class="sxs-lookup"><span data-stu-id="869c2-115">The most common method is to create the view using the [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration to the solution.</span></span>

<span data-ttu-id="869c2-116">將檢視新增至方案的基本步驟如下所示。</span><span class="sxs-lookup"><span data-stu-id="869c2-116">The basic steps to add a view to a solution are as follows.</span></span>  <span data-ttu-id="869c2-117">下列各節會進一步詳細說明每個步驟。</span><span class="sxs-lookup"><span data-stu-id="869c2-117">Each step is described in further detail in the sections below.</span></span>

1. <span data-ttu-id="869c2-118">將檢視匯出至檔案。</span><span class="sxs-lookup"><span data-stu-id="869c2-118">Export the view to a file.</span></span>
2. <span data-ttu-id="869c2-119">在方案中建立檢視資源。</span><span class="sxs-lookup"><span data-stu-id="869c2-119">Create the view resource in the solution.</span></span>
3. <span data-ttu-id="869c2-120">新增檢視詳細資料。</span><span class="sxs-lookup"><span data-stu-id="869c2-120">Add the view details.</span></span>

## <a name="export-the-view-to-a-file"></a><span data-ttu-id="869c2-121">將檢視匯出至檔案</span><span class="sxs-lookup"><span data-stu-id="869c2-121">Export the view to a file</span></span>
<span data-ttu-id="869c2-122">請依照 [Log Analytics 檢視設計工具](../log-analytics/log-analytics-view-designer.md)的指示將檢視匯出至檔案。</span><span class="sxs-lookup"><span data-stu-id="869c2-122">Follow the instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) to export a view to a file.</span></span>  <span data-ttu-id="869c2-123">匯出的檔案會是 JSON 格式，具有與[方案檔相同的元素](operations-management-suite-solutions-solution-file.md)。</span><span class="sxs-lookup"><span data-stu-id="869c2-123">The exported file will be in JSON format with the same [elements as the solution file](operations-management-suite-solutions-solution-file.md).</span></span>  

<span data-ttu-id="869c2-124">檢視檔的 **resources** 元素會有 **Microsoft.OperationalInsights/workspaces** 類型的資源，其代表 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="869c2-124">The **resources** element of the view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents the OMS workspace.</span></span>  <span data-ttu-id="869c2-125">此元素會有 **views** 類型的子元素，其代表檢視且包含詳細的組態。</span><span class="sxs-lookup"><span data-stu-id="869c2-125">This element will have a subelement with a type of **views** that represents the view and contains its detailed configuration.</span></span>  <span data-ttu-id="869c2-126">您將複製此元素的詳細資料，然後將它複製到您的方案。</span><span class="sxs-lookup"><span data-stu-id="869c2-126">You will copy the details of this element and then copy it into your solution.</span></span>

## <a name="create-the-view-resource-in-the-solution"></a><span data-ttu-id="869c2-127">在方案中建立檢視資源</span><span class="sxs-lookup"><span data-stu-id="869c2-127">Create the view resource in the solution</span></span>
<span data-ttu-id="869c2-128">將下列檢視資源新增至方案檔的 **resources** 元素。</span><span class="sxs-lookup"><span data-stu-id="869c2-128">Add the following view resource to the **resources** element of your solution file.</span></span>  <span data-ttu-id="869c2-129">這會使用您也必須新增的下述變數。</span><span class="sxs-lookup"><span data-stu-id="869c2-129">This uses variables that are described below that you must also add.</span></span>  <span data-ttu-id="869c2-130">請注意，**Dashboard** 和 **OverviewTile** 屬性是您將以所匯出檢視檔中的對應屬性覆寫的預留位置。</span><span class="sxs-lookup"><span data-stu-id="869c2-130">Note that the **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with the corresponding properties from the exported view file.</span></span>

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

<span data-ttu-id="869c2-131">將下列變數加入至解決方案檔的 variables 元素，並以您的解決方案值取代。</span><span class="sxs-lookup"><span data-stu-id="869c2-131">Add the following variables to the variables element of the solution file and replace the values to those for your solution.</span></span>

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of the view."
    "ViewName": "Provide a name for the view here."


<span data-ttu-id="869c2-132">請注意，您無法從匯出的檢視檔複製整個檢視資源，但您必須進行下列變更，該資源才能您的方案中正常運作。</span><span class="sxs-lookup"><span data-stu-id="869c2-132">Note that you could copy the entire view resource from your exported view file, but you would need to make the following changes for it to work in your solution.</span></span>  

* <span data-ttu-id="869c2-133">檢視資源的 **type** 必須從 **views** 變更為 **Microsoft.OperationalInsights/workspaces**。</span><span class="sxs-lookup"><span data-stu-id="869c2-133">The **type** for the view resource needs to be changed from **views** to **Microsoft.OperationalInsights/workspaces**.</span></span>
* <span data-ttu-id="869c2-134">檢視資源的 **name** 屬性必須變更以包含工作區名稱。</span><span class="sxs-lookup"><span data-stu-id="869c2-134">The **name** property for the view resource needs to be changed to include the workspace name.</span></span>
* <span data-ttu-id="869c2-135">必須移除工作區的相依性，因為方案中未定義此工作區資源。</span><span class="sxs-lookup"><span data-stu-id="869c2-135">The dependency on the workspace needs to be removed since the workspace resource isn't defined in the solution.</span></span>
* <span data-ttu-id="869c2-136">**DisplayName** 屬性必須新增至檢視。</span><span class="sxs-lookup"><span data-stu-id="869c2-136">**DisplayName** property needs to be added to the view.</span></span>  <span data-ttu-id="869c2-137">**Id**、**Name** 和 **DisplayName** 必須完全相符。</span><span class="sxs-lookup"><span data-stu-id="869c2-137">The **Id**, **Name**, and **DisplayName** must all match.</span></span>
* <span data-ttu-id="869c2-138">參數名稱必須變更以符合必要的參數集。</span><span class="sxs-lookup"><span data-stu-id="869c2-138">Parameter names must be changed to match the required set of parameters.</span></span>
* <span data-ttu-id="869c2-139">變數應定義於方案中並使用於適當的屬性中。</span><span class="sxs-lookup"><span data-stu-id="869c2-139">Variables should be defined in the solution and used in the appropriate properties.</span></span>

## <a name="add-the-view-details"></a><span data-ttu-id="869c2-140">新增檢視詳細資料</span><span class="sxs-lookup"><span data-stu-id="869c2-140">Add the view details</span></span>
<span data-ttu-id="869c2-141">所匯出檢視檔中的檢視資源會在 **properties** 元素中包含兩個名為 **Dashboard** 和 **OverviewTile** 的元素，而這兩個元素包含檢視的詳細組態。</span><span class="sxs-lookup"><span data-stu-id="869c2-141">The view resource in the exported view file will contain two elements in the **properties** element named **Dashboard** and **OverviewTile** which contain the detailed configuration of the view.</span></span>  <span data-ttu-id="869c2-142">將這兩個元素及其內容複製到方案檔中檢視資源的 **properties** 元素中。</span><span class="sxs-lookup"><span data-stu-id="869c2-142">Copy these two elements and their contents into the **properties** element of the view resource in your solution file.</span></span>

## <a name="example"></a><span data-ttu-id="869c2-143">範例</span><span class="sxs-lookup"><span data-stu-id="869c2-143">Example</span></span>
<span data-ttu-id="869c2-144">例如，下列範例顯示包含一個檢視的簡單方案檔。</span><span class="sxs-lookup"><span data-stu-id="869c2-144">For example, the following sample shows a simple solution file with a view.</span></span>  <span data-ttu-id="869c2-145">基於空間考量，**Dashboard** 和 **OverviewTile** 內容會顯示省略符號 (...)。</span><span class="sxs-lookup"><span data-stu-id="869c2-145">Ellipses (...) are shown for the **Dashboard** and **OverviewTile** contents for space reasons.</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="869c2-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="869c2-146">Next steps</span></span>
* <span data-ttu-id="869c2-147">了解建立[管理解決方案](operations-management-suite-solutions-creating.md)的完整詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="869c2-147">Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).</span></span>
* <span data-ttu-id="869c2-148">包含[管理解決方案中的自動化 Runbook](operations-management-suite-solutions-resources-automation.md)。</span><span class="sxs-lookup"><span data-stu-id="869c2-148">Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).</span></span>
