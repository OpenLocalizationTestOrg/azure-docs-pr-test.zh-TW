---
title: "aaaExport Azure Resource Manager 範本 |Microsoft 文件"
description: "使用 Azure 資源管理 tooexport 現有的資源群組中的範本。"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a>從現有資源匯出 Azure Resource Manager 範本
在本文中，您將學習如何 tooexport Resource Manager 範本使用從您的訂用帳戶中現有的資源。 您可以使用該產生的範本 toogain 進一步了解樣板語法。

有兩種方式 tooexport 範本：

* 您可以匯出 hello**用於部署的實際範本**。 hello 匯出的範本包含所有 hello 參數和變數，如同它們是出現在 hello 原始範本。 此方法時，很有幫助您部署的 hello 入口網站，透過資源，並想 toosee hello 範本 toocreate 那些資源。 此範本立即可用。 
* 您可以匯出**產生代表 hello hello 資源群組的目前狀態的範本**。 hello 匯出的範本不根據您用於部署的任何範本。 相反地，它會建立 hello 資源群組的快照集的範本。 hello 匯出的範本有許多的硬式編碼值，可能不一樣多的參數，因為您通常會定義。 當您在部署後修改了 hello 資源群組，則這個方法會很有用。 此範本通常需要修改才能使用。

本主題說明這兩種方法，透過 hello 入口網站。

## <a name="deploy-resources"></a>部署資源
讓我們開始部署，您可以使用匯出為範本的資源 tooAzure。 如果您已經有資源群組訂閱您想要 tooexport tooa 範本中，您可以略過本節。 hello 本文其餘部分會假設您已部署 hello web 應用程式和本節中所顯示的 SQL 資料庫解決方案。 如果您使用不同的解決方案，您的體驗可能會稍有不同，但 hello 步驟 tooexport 範本是 hello 相同。 

1. 在 hello [Azure 入口網站](https://portal.azure.com)，選取**新增**。
   
      ![選取 [新增]](./media/resource-manager-export-template/new.png)
2. 搜尋**web 應用程式 + SQL**和選取從 hello 可用的選項。
   
      ![搜尋 Web 應用程式和 SQL](./media/resource-manager-export-template/webapp-sql.png)

3. 選取 [ **建立**]。

      ![選取 [建立]](./media/resource-manager-export-template/create.png)

4. 提供所需的 hello 值 hello web 應用程式和 SQL database。 選取 [ **建立**]。

      ![提供 Web 和 SQL 值](./media/resource-manager-export-template/provide-web-values.png)

hello 部署可能會花一分鐘。 Hello 部署完成之後，您的訂用帳戶包含 hello 方案。

## <a name="view-template-from-deployment-history"></a>從部署記錄中檢視範本
1. 移 toohello 資源群組刀鋒視窗，新的資源群組。 請注意該 hello 刀鋒視窗會顯示 hello 最後一個部署的 hello 結果。 選取此連結。
   
      ![資源群組刀鋒視窗](./media/resource-manager-export-template/select-deployment.png)
2. 您會看到 hello 群組部署的歷程記錄。 在您的情況下，hello 刀鋒視窗可能會列出只能有一個部署。 選取此部署。
   
     ![上次部署](./media/resource-manager-export-template/select-history.png)
3. hello 刀鋒視窗會顯示 hello 部署的摘要。 hello 摘要包含 hello 部署的 hello 狀態及作業以及您為參數提供的 hello 值。 您用於 hello 部署中，選取 toosee hello 範本**檢視範本**。
   
     ![檢視部署摘要](./media/resource-manager-export-template/view-template.png)
4. 下列為您的七個檔案的資源管理員擷取 hello:
   
   1. **範本**-hello 範本可定義您方案的 hello 基礎結構。 當您建立 hello 透過 hello 入口網站的儲存體帳戶時，資源管理員會使用範本 toodeploy 它並儲存供日後參考該範本。
   2. **參數**-參數檔案，您可以在部署期間在值中使用 toopass。 它包含您在第一次部署的 hello 期間提供的 hello 值。 當您重新部署的 hello 範本時，您可以變更這些值。
   3. **CLI** -Azure 命令列介面 (CLI) 指令碼檔案，您可以使用 toodeploy hello 範本。
   3. **CLI 2.0** -Azure 命令列介面 (CLI) 指令碼檔案，您可以使用 toodeploy hello 範本。
   4. **PowerShell** -您可以使用 toodeploy hello 範本的 Azure PowerShell 指令碼檔案。
   5. **.NET** -您可以使用 toodeploy hello 範本的.NET 類別。
   6. **Ruby** -A Ruby 類別，您可以使用 toodeploy hello 範本。
      
      hello 檔可透過連結跨 hello 刀鋒視窗。 根據預設，hello 刀鋒視窗會顯示 hello 範本。
      
       ![檢視範本](./media/resource-manager-export-template/see-template.png)
      
此範本是使用 toocreate hello 實際範本您 web 應用程式和 SQL database。 請注意它包含可讓您 tooprovide 不同的值在部署期間的參數。 toolearn 進一步了解 hello 結構的範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。

## <a name="export-hello-template-from-resource-group"></a>從資源群組匯出 hello 範本
如果您手動變更您的資源或將資源加入多個部署中，從 hello 部署歷程記錄中擷取範本並不會反映 hello hello 資源群組的目前狀態。 本節說明如何 tooexport 範本，以反映 hello hello 資源群組的目前狀態。 

> [!NOTE]
> 您無法針對具有超過 200 個資源的資源群組匯出範本。
> 
> 

1. 資源群組中，選取 tooview hello 範本**自動化指令碼**。
   
      ![匯出資源群組](./media/resource-manager-export-template/select-automation.png)
   
     資源管理員會評估 hello hello 資源群組中的資源，並產生這些資源的範本。 並非所有的資源類型都支援 hello 匯出樣板函式。 您可能會看到錯誤指出 hello 匯出問題。 您了解如何 toohandle 那些問題 hello[修正匯出問題](#fix-export-issues)> 一節。
2. 同樣地，您會看到 hello 六個檔案中，您可以使用 tooredeploy hello 方案。 不過，此時間 hello 範本是稍有不同。 請注意，hello 產生的範本包含比上一節中的 hello 範本較少的參數。 此外，許多 hello 值 （如位置和 SKU 值） 是硬式編碼這個範本，而不會接受參數值。 重複使用此範本之前, 您可能想 tooedit hello 範本 toomake 更妥善運用參數。 
   
3. 您有幾個選項用於接續 toowork 與此範本。 您可以下載 hello 範本，並使用它在本機 JSON 編輯器。 或者，您可以儲存 hello 範本庫 tooyour 並處理它，透過 hello 入口網站。
   
     如果您想要使用 JSON 編輯器，例如[VS Code](https://code.visualstudio.com/)或[Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)，您可能會偏好下載本機 hello 範本並使用該編輯器。 toowork 的在本機上，選取**下載**。
   
      ![下載範本](./media/resource-manager-export-template/download-template.png)
   
     如果您未設定使用 JSON 編輯器，您可能會偏好編輯 hello 透過 hello 入口網站的範本。 hello 本主題其餘部分會假設您已儲存 hello 範本庫 tooyour hello 入口網站中。 不過，您可以建立 hello 相同語法變更 toohello 範本是否在本機使用 JSON 編輯器，或透過 hello 入口網站。 toowork 透過 hello 入口網站中，選取**新增 toolibrary**。
   
      ![新增 toolibrary](./media/resource-manager-export-template/add-to-library.png)
   
     加入時範本庫 toohello，讓 hello 範本的名稱和描述。 然後選取 [儲存]。
   
     ![設定範本值](./media/resource-manager-export-template/save-library-template.png)
4. tooview 範本儲存在您的程式庫中，選取**更多服務**，型別**範本**toofilter 結果中，選取**範本**。
   
      ![尋找範本](./media/resource-manager-export-template/find-templates.png)
5. 選取具有您所儲存的 hello 名稱 hello 範本。
   
      ![選取範本](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a>自訂 hello 範本
匯出的 hello 範本運作良好，如果您想 toocreate hello 相同 web 應用程式和每個部署的 SQL 資料庫。 但 Resource Manager 提供了一些選項，以便您可以更有彈性地部署範本。 本文章將示範如何 hello tooadd 參數資料庫管理員名稱和密碼。 您可以使用這個相同的方法 tooadd 更大的彈性，其他 hello 範本中的值。

1. toocustomize hello 範本中，選取**編輯**。
   
     ![顯示範本](./media/resource-manager-export-template/select-edit.png)
2. 選取 hello 範本。
   
     ![編輯範本](./media/resource-manager-export-template/select-added-template.png)
3. toobe 無法 toopass hello 值，您可能會想 toospecify 在部署期間，加入下列兩個參數 toohello hello**參數**hello 範本中的區段：

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. toouse hello 新參數取代 hello 中的 hello SQL 伺服器定義**資源**> 一節。 請注意，**administratorLogin** 和 **administratorLoginPassword** 現在使用參數值。

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. 選取**確定**當您完成編輯 hello 範本。
7. 選取**儲存**toosave hello 變更 toohello 範本。
   
     ![儲存範本](./media/resource-manager-export-template/save-template.png)
8. tooredeploy hello 更新範本中，選取**部署**。
   
     ![部署範本](./media/resource-manager-export-template/redeploy-template.png)
9. 提供參數值，並選取資源群組 toodeploy hello 資源。


## <a name="fix-export-issues"></a>修正匯出問題
並非所有的資源類型都支援 hello 匯出樣板函式。 這個問題，請以手動方式 tooresolve hello 遺失資源，將重新加入至您的範本。 hello 錯誤訊息包含無法匯出的 hello 資源類型。 在[範本參考](/azure/templates/)中尋找該資源類型。 例如，toomanually 加入虛擬網路閘道，請參閱[Microsoft.Network/virtualNetworkGateways 範本參考](/azure/templates/microsoft.network/virtualnetworkgateways)。

> [!NOTE]
> 從資源群組 (而非部署歷程記錄) 匯出時，您只會遇到匯出問題。 如果您的最後一個部署準確地呈現 hello hello 資源群組的目前狀態，您應該將 hello 範本匯出從 hello 部署歷程記錄，而不是從 hello 資源群組。 您所做的變更 toohello 資源群組的單一範本中未定義時，只能匯出從資源群組。
> 
> 

## <a name="next-steps"></a>後續步驟
您已經學會如何 tooexport 範本，以從您在 hello 入口網站中建立的資源。

* 您可以透過 [PowerShell](resource-group-template-deploy.md)、[Azure CLI](resource-group-template-deploy-cli.md) 或 [REST API](resource-group-template-deploy-rest.md) 部署範本。
* 如何 tooexport 範本，以透過 PowerShell，請參閱的 toosee[使用 Azure PowerShell 的 Azure Resource Manager](powershell-azure-resource-manager.md)。
* 如何 tooexport 範本，以透過 Azure CLI，請參閱的 toosee[使用 hello for Mac、 Linux 及 Windows Azure 資源管理員使用 Azure CLI](xplat-cli-azure-resource-manager.md)。

