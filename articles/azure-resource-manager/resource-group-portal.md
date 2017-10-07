---
title: "Azure 入口網站 toomanage aaaUse Azure 資源 |Microsoft 文件"
description: "使用 Azure 入口網站和 Azure 資源管理 toomanage 您的資源。 示範如何使用儀表板 toomonitor 資源 toowork。"
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 0c89a197a31c5b6dd03ba457cb4d1fdf9f6d00f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-resources-through-portal"></a>透過入口網站管理 Azure 資源
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Azure CLI](xplat-cli-azure-resource-manager.md)
> * [入口網站](resource-group-portal.md) 
> * [REST API](resource-manager-rest-api.md)
> 
> 

本主題說明如何 toouse hello [Azure 入口網站](https://portal.azure.com)與[Azure Resource Manager](resource-group-overview.md) toomanage 您的 Azure 資源。 toolearn 有關部署資源，透過 hello 入口網站，請參閱[部署具有資源管理員範本和 Azure 入口網站資源](resource-group-template-deploy-portal.md)。

目前不是每次服務支援 hello 入口網站或資源管理員。 針對這些服務，您需要 toouse hello[傳統入口網站](https://manage.windowsazure.com)。 如需每個服務的 hello 狀態，請參閱[Azure 入口網站的可用性圖表](https://azure.microsoft.com/features/azure-portal/availability/)。

## <a name="manage-resource-groups"></a>管理資源群組

資源群組是存放 Azure 方案相關資源的容器。 hello 資源群組可包含 hello 方案的所有 hello 資源或您想 toomanage 為群組的資源。 您決定要如何 tooallocate 資源 tooresource 根據錯誤群組構成 hello 最適合您的組織。 一般而言，加入共用 hello 資源相同的生命週期 toohello 相同資源群組，因此您可以輕鬆地部署、 更新和刪除它們做為群組。 

hello 資源群組，儲存 hello 資源的相關中繼資料。 因此，當您指定 hello 資源群組的位置，就指定儲存的中繼資料。 基於相容性因素，您可能需要 tooensure 資料儲存在特定區域中。

1. 所有的 hello 資源群組，在您的訂用帳戶中，選取 toosee**資源群組**。
   
    ![瀏覽資源群組](./media/resource-group-portal/browse-groups.png)
2. toocreate 空的資源群組中，選取**新增**。
   
    ![新增資源群組](./media/resource-group-portal/add-resource-group.png)
3. 提供的名稱和位置 hello 新資源群組。 選取 [ **建立**]。
   
    ![建立資源群組](./media/resource-group-portal/create-empty-group.png)
4. 您可能需要 tooselect**重新整理**toosee hello 最近已建立資源群組。
   
    ![重新整理資源群組](./media/resource-group-portal/refresh-resource-groups.png)
5. 選取針對您的資源群組，顯示 toocustomize hello 資訊**資料行**。
   
    ![自訂資料行](./media/resource-group-portal/select-columns.png)
6. 選取 hello 資料行 tooadd，，然後選取**更新**。
   
    ![新增資料行](./media/resource-group-portal/add-columns.png)
7. toolearn 有關部署資源 tooyour 新資源群組，請參閱[部署具有資源管理員範本和 Azure 入口網站資源](resource-group-template-deploy-portal.md)。
8. 快速存取 tooa 資源群組，您可以釘選 hello 刀鋒視窗 tooyour 儀表板。
   
    ![釘選資源群組](./media/resource-group-portal/pin-group.png)
9. hello 儀表板會顯示 hello 資源群組和其資源。 您可以選取 hello 資源群組或任何其資源 toonavigate toohello 項目。
   
    ![釘選資源群組](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a>標記資源
您可以套用標籤 tooresource 群組和資源 toologically 組織您的資產。 如需有關使用標記資訊，請參閱[使用標記 tooorganize 您的 Azure 資源](resource-group-using-tags.md)。

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a>監視資源
當您選取的資源時，hello 資源刀鋒視窗會顯示預設圖形和監視該資源類型的資料表。

1. 選取資源，並注意 hello**監視**> 一節。 它包含相關 toohello 資源類型的圖形。 hello 下列影像顯示 hello 預設的監視儲存體帳戶的資料。
   
    ![顯示監視](./media/resource-group-portal/show-monitoring.png)
2. 您可以藉由選取 hello 區段上方 hello 省略符號 （...） 釘選一段 hello 刀鋒視窗 tooyour 儀表板。 您也可以自訂在 hello 刀鋒視窗中的 hello 大小 hello 區段，或將它完全移除。 hello 下列影像顯示 toopin，如何自訂或移除 hello CPU 與記憶體 > 一節。
   
    ![釘選區段](./media/resource-group-portal/pin-cpu-section.png)
3. 釘選 hello 區段 toohello 儀表板，您會看到摘要 hello hello 儀表板上。 此外，立即將它選取會帶您 toomore hello 資料的詳細資料。
   
    ![檢視儀表板](./media/resource-group-portal/view-startboard.png)
4. toocompletely 自訂 hello 資料監視透過 hello 入口網站，瀏覽 tooyour 預設儀表板，並選取**新儀表板**。
   
    ![儀表板](./media/resource-group-portal/dashboard.png)
5. 提供新儀表板名稱，然後拖曳 hello 儀表板的磚。 hello 圖格被篩選的不同選項。
   
    ![儀表板](./media/resource-group-portal/create-dashboard.png)
   
     toolearn 關於使用 儀表板，請參閱[建立和共用 hello Azure 入口網站的儀表板](../azure-portal/azure-portal-dashboards.md)。

## <a name="manage-resources"></a>管理資源
在 hello 刀鋒視窗中的資源，您會看到管理 hello 資源 hello 選項。 hello 入口網站會顯示該特定資源類型的管理選項。 您可以看到 hello 的上方 hello 資源刀鋒視窗和 hello 左邊 hello 管理命令。

![管理資源](./media/resource-group-portal/manage-resources.png)

您可以從這些選項中，執行作業，例如啟動和停止虛擬機器，或是重新設定 hello hello 虛擬機器的屬性。

## <a name="move-resources"></a>移動資源
如果您需要 toomove 資源 tooanother 資源群組或其他訂用帳戶，請參閱[移動資源 toonew 資源群組或訂用帳戶](resource-group-move-resources.md)。

## <a name="lock-resources"></a>鎖定資源
您可以鎖定訂用帳戶、 資源群組或資源 tooprevent 其他使用者不小心刪除或修改重要的資源組織中。 如需詳細資訊，請參閱[使用 Azure Resource Manager 來鎖定資源](resource-group-lock-resources.md)。

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a>檢視訂用帳戶和成本
您可以檢視您的訂用帳戶和 hello 彙總成本的相關資訊的所有資源。 選取**訂閱**和您想要 toosee hello 訂用帳戶。 您可能只有一個訂用帳戶 tooselect。

![訂用帳戶](./media/resource-group-portal/select-subscription.png)

Hello 訂用帳戶 刀鋒視窗中，您會看到完工速率。

![完工速率](./media/resource-group-portal/burn-rate.png)

還有依資源類型的成本分析。

![資源成本](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a>匯出範本
設定好您的資源群組之後，您可能想 tooview hello Resource Manager 範本 hello 資源群組。 匯出的 hello 範本提供兩個優點：

1. 您可以輕鬆地自動化未來 hello 方案的部署，因為 hello 範本包含所有與 hello 完整的基礎結構。
2. 您先熟悉樣板語法藉由查看 hello JavaScript Object Notation (JSON) 表示您的方案。

如需逐步指引，請參閱 [從現有資源匯出 Azure Resource Manager 範本](resource-manager-export-template.md)。

## <a name="delete-resource-group-or-resources"></a>刪除資源群組或資源
刪除資源群組會刪除所有內含的 hello 資源。 您也可以刪除資源群組內的個別資源。 當您刪除資源群組，因為其他資源群組中的連結的 tooit 可能有資源時，您會想 tooexercise 警告。 資源管理員不會刪除連結的資源，但它們可能無法正常運作不含預期的 hello 資源。

![刪除群組](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a>後續步驟
* tooview 活動記錄，請參閱 <<c0> [ 稽核與資源管理員作業](resource-group-audit.md)。
* tooview 部署的詳細資訊，請參閱[檢視部署作業](resource-manager-deployment-operations.md)。
* hello 入口網站，透過 toodeploy 資源，請參閱[部署具有資源管理員範本和 Azure 入口網站資源](resource-group-template-deploy-portal.md)。
* toomanage 存取 tooresources，請參閱[使用角色指派 toomanage 存取 tooyour Azure 訂用帳戶資源](../active-directory/role-based-access-control-configure.md)。
* 如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。

