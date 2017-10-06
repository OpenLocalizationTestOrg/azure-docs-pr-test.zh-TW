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
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a>Operations Management Suite (OMS) 管理解決方案中的檢視 (預覽)
> [!NOTE]
> 這是在 OMS 中建立管理解決方案 (目前處於預覽狀態) 的預備文件。 如下所述的任何結構描述是主體 toochange。    
>
>

[在 Operations Management Suite (OMS) 的管理解決方案](operations-management-suite-solutions.md)通常會包含一個或多個檢視 toovisualize 資料。  本文說明如何 tooexport 來建立檢視表 hello[檢視表設計工具](../log-analytics/log-analytics-view-designer.md)並將它包含在管理解決方案中。  

> [!NOTE]
> hello 這篇文章中的範例使用參數和變數，都是必要或常見 toomanagement 解決方案中所述[Operations Management Suite (OMS) 中建立管理方案](operations-management-suite-solutions-creating.md)
>
>

## <a name="prerequisites"></a>必要條件
本文假設您已經熟悉如何太[建立管理方案](operations-management-suite-solutions-creating.md)和方案檔的 hello 結構。

## <a name="overview"></a>概觀
建立 tooinclude 管理解決方案中的檢視，**資源**中 hello[方案檔](operations-management-suite-solutions-creating.md)。  hello JSON 描述 hello 檢視詳細的設定是通常複雜雖然和非，一般解決方案作者可以 toocreate 手動。  hello 最常見方法是使用 hello toocreate hello 檢視[檢視表設計工具](../log-analytics/log-analytics-view-designer.md)、 將它，匯出，然後再將它的詳細的組態 toohello 方案。

hello 基本步驟 tooadd 檢視 tooa 方案如下所示。  在 hello 的以下各節將進一步詳細說明每個步驟。

1. 匯出 hello 檢視 tooa 檔案。
2. Hello 方案中建立 hello 檢視資源。
3. 新增 hello 檢視詳細資料。

## <a name="export-hello-view-tooa-file"></a>匯出 hello 檢視 tooa 檔案
請遵循指示 hello[記錄分析檢視表設計工具](../log-analytics/log-analytics-view-designer.md)tooexport 檢視 tooa 檔案。  hello 匯出的檔案將會以 JSON 格式與 hello 相同[為 hello 方案檔案的項目](operations-management-suite-solutions-solution-file.md)。  

hello**資源**hello 檢視檔案的項目將擁有的資源類型為**Microsoft.OperationalInsights/workspaces**代表 hello OMS 工作區。  這個項目必須具有類型的子元素**檢視**中代表 hello 檢視，且包含詳細的設定。  您將會複製這個項目的 hello 詳細資料，並再將它複製到您的方案。

## <a name="create-hello-view-resource-in-hello-solution"></a>建立 hello 方案中的 hello 檢視資源
新增下列檢視資源 toohello hello**資源**方案檔的項目。  這會使用您也必須新增的下述變數。  請注意該 hello**儀表板**和**OverviewTile**屬性都是預留位置，您將會覆寫與 hello hello 匯出的檢視檔案從對應的屬性。

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

新增 hello 遵循 hello 方案檔的變數 toohello 變數項目，並取代 hello 值 toothose 為您的方案。

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of hello view."
    "ViewName": "Provide a name for hello view here."


請注意，您無法複製 hello 整個檢視資源從匯出的檢視檔案，您必須依照變更 toomake hello toowork 方案中。  

* hello**類型**hello 檢視的資源需要從變更的 toobe**檢視**太**Microsoft.OperationalInsights/workspaces**。
* hello**名稱**hello 檢視資源的屬性必須變更 toobe tooinclude hello 工作區名稱。
* hello hello 工作區上的相依性需要 toobe 移除，因為 hello 方案中未定義 hello 工作區的資源。
* **DisplayName**屬性需求 toobe 加入 toohello 檢視。  hello**識別碼**，**名稱**，和**DisplayName**必須全部都會相符。
* 必須變更參數名稱 toomatch hello 所需的參數集。
* 變數應 hello 方案中定義和 hello 適當的內容中使用。

## <a name="add-hello-view-details"></a>新增 hello 檢視詳細資料
hello 檢視資源 hello 中的匯出檔案會包含兩個項目在 hello 檢視**屬性**名**儀表板**和**OverviewTile**包含 hellohello 檢視的詳細的設定。  這兩個元素和其內容複製到 hello**屬性**hello 檢視資源方案檔中的項目。

## <a name="example"></a>範例
比方說，hello 下列範例會示範檢視的簡單方案檔。  省略符號 （...） 會顯示 hello**儀表板**和**OverviewTile**基於空間考量的內容。

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
