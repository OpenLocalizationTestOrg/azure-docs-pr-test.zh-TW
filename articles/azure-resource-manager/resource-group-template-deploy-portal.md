---
title: "Azure 入口網站 toodeploy aaaUse Azure 資源 |Microsoft 文件"
description: "使用 Azure 入口網站和 Azure 資源管理 toodeploy 您的資源。"
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a>使用 Resource Manager 範本與 Azure 入口網站來部署資源
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Azure CLI](resource-group-template-deploy-cli.md)
> * [入口網站](resource-group-template-deploy-portal.md)
> * [REST API](resource-group-template-deploy-rest.md)
> 
> 

本主題說明如何 toouse hello [Azure 入口網站](https://portal.azure.com)與[Azure Resource Manager](resource-group-overview.md) toodeploy 您的 Azure 資源。 toolearn 關於管理您的資源，請參閱[透過入口網站管理 Azure 資源](resource-group-portal.md)。

目前不是每次服務支援 hello 入口網站或資源管理員。 針對這些服務，您需要 toouse hello[傳統入口網站](https://manage.windowsazure.com)。 如需每個服務的 hello 狀態，請參閱[Azure 入口網站的可用性圖表](https://azure.microsoft.com/features/azure-portal/availability/)。

## <a name="create-resource-group"></a>建立資源群組
1. toocreate 空的資源群組中，選取**新增** > **管理** > **資源群組**。
   
    ![建立空的資源群組](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. 提供其名稱和位置，再視需要選取訂用帳戶。 因為儲存 hello 資源的相關中繼資料與 hello 資源群組，您需要 hello 資源群組 tooprovide 位置。 基於相容性因素，您可能想的 toospecify 儲存的中繼資料。 一般情況下，我們建議您指定大部分資源所在的位置。 使用 hello 相同位置可簡化您的範本。
   
    ![設定群組值](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a>從 Marketplace 部署資源
建立資源群組之後，您可以部署從 hello Marketplace 的資源 tooit。 hello Marketplace 常見案例提供預先定義的解決方案。

1. toostart 部署中，選取**新增**和 hello 類型的資源，您想要 toodeploy。 然後，尋找 hello hello 資源特定版本，您想要 toodeploy。
   
    ![部署資源](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. 如果看不到您想要 toodeploy hello 特定方案，您可以為其搜尋 hello Marketplace。
   
    ![搜尋 Marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. 根據選取的資源 hello 類型，您會有相關屬性 tooset 之前部署的集合。 這些選項並未在這裡顯示，因為它們會隨著資源類型而有所不同。 對於所有類型，您必須選取目的地資源群組。 hello 以下影像顯示如何 toocreate web 應用程式並將其部署 toohello 您所建立的資源群組。
   
    ![建立資源群組](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    或者，您可以在部署您的資源時，決定 toocreate 資源群組。 選取**建立新**並提供 hello 資源群組名稱。
   
    ![建立新的資源群組](./media/resource-group-template-deploy-portal/select-new-group.png)
4. 您的部署隨即開始。 hello 部署可能需要幾分鐘的時間。 Hello 部署完成時，您會看到通知。
   
    ![檢視通知](./media/resource-group-template-deploy-portal/view-notification.png)
5. 部署後您的資源，您可以加入更多資源 toohello 資源群組使用 hello**新增**hello 資源群組 刀鋒視窗上的命令。
   
    ![新增資源](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a>從自訂範本部署資源
如果您想 tooexecute 部署，但不是使用任何 hello 範本 hello Marketplace 中，您可以建立自訂的範本，定義您方案的 hello 基礎結構。 toolearn 有關建立範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。

1. toodeploy hello 入口網站，透過將自訂的範本選取**新增**，並開始搜尋**範本部署**直到您可以從 hello 選項中選取它。
   
    ![搜尋範本部署](./media/resource-group-template-deploy-portal/search-template.png)
2. 選取**範本部署**從 hello 可用的資源。
   
    ![選取範本部署](./media/resource-group-template-deploy-portal/select-template.png)
3. 在啟動 hello 範本部署之後, 開啟 hello 適用於自訂的空白範本。
   
    ![建立範本](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    在 hello 編輯器中，新增定義您想要 toodeploy hello 資源的 hello JSON 語法。 完成時選取 [儲存]  。 如需撰寫 hello JSON 語法的指引，請參閱[資源管理員範本逐步解說](resource-manager-template-walkthrough.md)。
   
    ![編輯範本](./media/resource-group-template-deploy-portal/edit-template.png)
4. 或者，您可以選取現有的範本從 hello [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)。 這些範本是由 hello 社群貢獻。 這些資料涵蓋許多常見的案例，和其他人可能加入的範本來嘗試 toodeploy 類似 toowhat。 您可以搜尋 hello 範本 toofind 符合您案例的項目。
   
    ![選取快速入門範本](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    您可以在 hello 編輯器中檢視 hello 選取的範本。
5. 提供所有 hello 其他值之後, 選取**建立**toodeploy hello 範本。 
   
    ![部署範本](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a>部署範本儲存 tooyour 帳戶的資源
hello 入口網站可讓您 toosave 範本 tooyour Azure 帳戶，並稍後重新部署它。 如需有關使用這些儲存範本，[開始使用 hello Azure 入口網站上的私用範本](../marketplace-consumer/mytemplates-getstarted.md)。

1. 您已儲存的範本中，選取 toofind**瀏覽** > **範本**。
   
    ![瀏覽範本](./media/resource-group-template-deploy-portal/browse-templates.png)
2. 從 hello 儲存 tooyour 帳戶的範本清單，選取您想 toowork hello。
   
    ![已儲存的範本](./media/resource-group-template-deploy-portal/saved-templates.png)
3. 選取**部署**tooredeploy 這儲存範本。
   
    ![部署已儲存的範本](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a>後續步驟
* tooview 稽核記錄，請參閱 <<c0> [ 稽核與資源管理員作業](resource-group-audit.md)。
* tootroubleshoot 部署錯誤，請參閱[檢視部署作業](resource-manager-deployment-operations.md)。
* tooretrieve 範本部署或資源群組，請參閱[匯出 Azure 資源管理員範本，從現有的資源](resource-manager-export-template.md)。
* 如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。

