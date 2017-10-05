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
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a>Operations Management Suite (OMS) 管理解決方案中的檢視 (預覽)
> [!NOTE]
> 這是在 OMS 中建立管理解決方案 (目前處於預覽狀態) 的預備文件。 以下所述的任何結構描述可能會有所變更。    
>
>

[Operations Management Suite (OMS) 中的管理解決方案](operations-management-suite-solutions.md)通常包含一或多個檢視，以將資料視覺化。  本文說明如何匯出[檢視設計工具](../log-analytics/log-analytics-view-designer.md)所建立的檢視並將它納入管理解決方案中。  

> [!NOTE]
> 本文中的範例使用管理解決方案所必要或通用的參數和變數，如[在 Operations Management Suite (OMS) 中建立管理解決方案](operations-management-suite-solutions-creating.md)所述。
>
>

## <a name="prerequisites"></a>必要條件
本文假設您已經熟悉如何[建立管理解決方案](operations-management-suite-solutions-creating.md)和方案檔的結構。

## <a name="overview"></a>Overview
若要在管理解決方案中納入檢視，您可在[方案檔](operations-management-suite-solutions-creating.md)中建立其**資源**。  說明檢視詳細組態的 JSON 通常很複雜，典型方案作者無法以手動方式建立。  最常見的方法是使用[檢視設計工具](../log-analytics/log-analytics-view-designer.md)建立檢視、加以匯出，然後將其詳細組態新增至方案。

將檢視新增至方案的基本步驟如下所示。  下列各節會進一步詳細說明每個步驟。

1. 將檢視匯出至檔案。
2. 在方案中建立檢視資源。
3. 新增檢視詳細資料。

## <a name="export-the-view-to-a-file"></a>將檢視匯出至檔案
請依照 [Log Analytics 檢視設計工具](../log-analytics/log-analytics-view-designer.md)的指示將檢視匯出至檔案。  匯出的檔案會是 JSON 格式，具有與[方案檔相同的元素](operations-management-suite-solutions-solution-file.md)。  

檢視檔的 **resources** 元素會有 **Microsoft.OperationalInsights/workspaces** 類型的資源，其代表 OMS 工作區。  此元素會有 **views** 類型的子元素，其代表檢視且包含詳細的組態。  您將複製此元素的詳細資料，然後將它複製到您的方案。

## <a name="create-the-view-resource-in-the-solution"></a>在方案中建立檢視資源
將下列檢視資源新增至方案檔的 **resources** 元素。  這會使用您也必須新增的下述變數。  請注意，**Dashboard** 和 **OverviewTile** 屬性是您將以所匯出檢視檔中的對應屬性覆寫的預留位置。

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

將下列變數加入至解決方案檔的 variables 元素，並以您的解決方案值取代。

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of the view."
    "ViewName": "Provide a name for the view here."


請注意，您無法從匯出的檢視檔複製整個檢視資源，但您必須進行下列變更，該資源才能您的方案中正常運作。  

* 檢視資源的 **type** 必須從 **views** 變更為 **Microsoft.OperationalInsights/workspaces**。
* 檢視資源的 **name** 屬性必須變更以包含工作區名稱。
* 必須移除工作區的相依性，因為方案中未定義此工作區資源。
* **DisplayName** 屬性必須新增至檢視。  **Id**、**Name** 和 **DisplayName** 必須完全相符。
* 參數名稱必須變更以符合必要的參數集。
* 變數應定義於方案中並使用於適當的屬性中。

## <a name="add-the-view-details"></a>新增檢視詳細資料
所匯出檢視檔中的檢視資源會在 **properties** 元素中包含兩個名為 **Dashboard** 和 **OverviewTile** 的元素，而這兩個元素包含檢視的詳細組態。  將這兩個元素及其內容複製到方案檔中檢視資源的 **properties** 元素中。

## <a name="example"></a>範例
例如，下列範例顯示包含一個檢視的簡單方案檔。  基於空間考量，**Dashboard** 和 **OverviewTile** 內容會顯示省略符號 (...)。

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




## <a name="next-steps"></a>後續步驟
* 了解建立[管理解決方案](operations-management-suite-solutions-creating.md)的完整詳細資訊。
* 包含[管理解決方案中的自動化 Runbook](operations-management-suite-solutions-resources-automation.md)。
