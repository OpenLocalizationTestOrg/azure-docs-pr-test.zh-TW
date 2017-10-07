---
title: "以 hello Azure CLI aaaManage 資源 |Microsoft 文件"
description: "使用 hello Azure 命令列介面 (CLI) toomanage Azure 資源和群組"
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3df70e123d14d3bbf2648c71970bac1db4afc025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a>使用 hello Azure CLI toomanage Azure 資源與資源群組
> [!div class="op_single_selector"]
> * [入口網站](resource-group-portal.md) 
> * [Azure CLI](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [REST API](resource-manager-rest-api.md)
> 
> 

hello Azure 命令列介面 (Azure CLI) 是其中一個的數個工具，您可以使用 toodeploy 和管理資源與資源管理員。 本文介紹常見方式 toomanage Azure 資源與資源群組使用 hello Azure CLI Resource Manager 模式中。 如需使用 hello CLI toodeploy 資源資訊，請參閱[部署資源，資源管理員範本與 Azure CLI](resource-group-template-deploy-cli.md)。 如需 Azure 資源與資源管理員的背景，請瀏覽 hello [Azure 資源管理員概觀](resource-group-overview.md)。

> [!NOTE]
> toomanage Azure hello Azure CLI 資源，您需要太[安裝 hello Azure CLI](../cli-install-nodejs.md)，和[登入 tooAzure](../xplat-cli-connect.md)使用 hello`azure login`命令。 請確定 hello CLI 處於 Resource Manager 模式 (執行`azure config mode arm`)。 如果您已經完成這些工作，您已準備好 toogo。
> 
> 

## <a name="get-resource-groups-and-resources"></a>取得資源群組和資源
### <a name="resource-groups"></a>資源群組
tooget 一份您訂用帳戶和它們的位置中的所有資源群組執行此命令。

    azure group list


### <a name="resources"></a>資源
 toolist 群組，例如使用中的所有資源都名稱*testRG*，使用下列命令的 hello:

    azure resource list testRG

tooview hello 群組，例如，名為的 VM 內的個別資源*MyUbuntuVM*，使用類似 hello 下列命令：

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

請注意 hello **Microsoft.Compute/virtualMachines**參數。 這個參數會指出 hello hello 資源要求的資訊類型。

> [!NOTE]
> 當使用 hello **azure 資源**hello 以外的命令**清單**命令時，您必須指定 hello 資源 hello API 版本以 hello **-o**參數。 如果您懷疑 hello API 版本，請參閱 hello 範本檔案，並找出 hello 資源的 hello api 版本欄位。 如需 Resource Manager 中的 API 版本詳細資訊，請參閱[資源提供者和類型](resource-manager-supported-services.md)。
> 
> 

當資源上檢視詳細資料，通常會很有用的 toouse hello`--json`參數。 這個參數可讓 hello 輸出更容易閱讀，因為有些值會巢狀的結構或集合。 hello 下列範例示範傳回的 hello 結果的 hello**顯示**命令做為 JSON 文件。

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> 如果您想要儲存使用 hello hello JSON 資料 toofile&gt;字元 toodirect hello 輸出 tooa 檔案。 例如：
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a>標記
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a>管理資源
tooadd 資源，例如儲存體帳戶 tooa 資源群組，執行如下命令：

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

此外 toospecifying hello API 版的 hello 資源以 hello **-o**參數、 使用 hello **-p**參數 toopass JSON 格式化字串的任何必要或其他屬性。

toodelete 現有的資源，例如虛擬機器資源使用 hello 下列類似的命令：

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

toomove 現有資源 tooanother 資源群組或訂用帳戶，使用 hello **azure 資源移動**命令。 下列範例會示範如何 hello toomove Redis 快取 tooa 新的資源群組。 在 hello **-i**參數，提供以逗號分隔的 toomove hello 資源識別碼的清單。

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a>控制存取 tooresources
您可以使用 hello Azure CLI toocreate 和管理原則 toocontrol 存取 tooAzure 資源。 如需原則定義和指派原則 tooresources 背景，請參閱[原則 toomanage 資源及控制存取](resource-manager-policy.md)。

例如，定義下列原則 toodeny hello 其中位置不是美國西部或美國中北部，所有要求，並將它儲存 toohello 原則定義檔案 policy.json:

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

然後執行 hello**原則定義建立**命令：

    azure policy definition create MyPolicy -p c:\temp\policy.json

此命令會顯示類似 toohello 下列輸出：

    + Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy

    data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny

 tooassign hello 範圍要請使用 hello 原則**PolicyDefinitionId** hello 前一個命令所傳回。 在下列範例的 hello，此範圍是 hello 訂閱，但您可以為範圍 tooresource 群組或個別的資源：

    azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/

您可以取得、 變更或移除原則定義使用 hello**原則定義顯示**，**原則定義集中**，和**原則定義刪除**命令。

同樣地，您可以取得、 變更或移除原則指派使用 hello**原則指派顯示**，**原則指派集中**，和**原則指派刪除**命令.

## <a name="export-a-resource-group-as-a-template"></a>匯出資源群組作為範本
為現有的資源群組，您可以檢視 hello 資源群組的 hello Resource Manager 範本。 匯出的 hello 範本提供兩個優點：

1. 您可以輕鬆地自動化未來 hello 方案的部署，因為 hello 範本中定義所有 hello 基礎結構。
2. 您先熟悉樣板語法藉由查看 hello JSON 表示您的方案。

使用 Azure CLI hello，您可以匯出範本代表 hello 的目前狀態的資源群組，或下載用於特定部署的 hello 範本。

* **匯出的資源群組的 hello 範本**-當您所做的變更 tooa 資源群組，而需要 tooretrieve hello JSON 字串表示的目前狀態，這會很有幫助。 不過，hello 產生的範本包含最少的參數和任何變數。 大多數 hello 範本中的 hello 值是硬式編碼。 在部署之前產生的 hello 範本，您可能希望 tooconvert hello 值的多個參數中，因此您可以自訂的不同環境的 hello 部署。
  
    資源群組 tooa 本機目錄，執行 hello tooexport hello 範本`azure group export`命令 hello 下列範例所示。 (取代適用於您作業系統環境的本機目錄。)
  
        azure group export testRG ~/azure/templates/
* **下載特定部署的 hello 範本**-當您需要 tooview hello 實際範本已使用的 toodeploy 資源時，這是很有幫助。 hello 範本包含所有參數和 hello 原始部署中所定義的變數。 不過，如果您組織中有人 hello 範本中進行變更 toohello 資源群組 hello 定義之外，此範本不代表 hello hello 資源群組的目前狀態。
  
    使用特定部署 tooa 本機目錄中，執行 hello toodownload hello 樣板`azure group deployment template download`命令。 例如：
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> 範本匯出處於預覽狀態，並非所有的資源類型目前都支援匯出範本。 當嘗試 tooexport 範本，可能會看到錯誤指出未匯出一些資源。 如有需要，下載範本之後，在範本中手動定義這些資源。
> 
> 

## <a name="next-steps"></a>後續步驟
* 部署作業的 tooget 詳細資料和疑難排解部署錯誤，以 hello Azure CLI，請參閱[檢視部署作業](resource-manager-deployment-operations.md)。
* 如果您想 toouse hello CLI tooset 應用程式或指令碼 tooaccess 資源，請參閱[使用 Azure CLI toocreate 服務主體 tooaccess 資源](resource-group-authenticate-service-principal-cli.md)。
* 如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。

