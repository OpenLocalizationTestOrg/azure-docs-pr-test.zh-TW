---
title: "使用 Azure 資源群組專案的 VS Team Services 中的 aaaContinuous 整合 |Microsoft 文件"
description: "描述在 Visual Studio Team Services 中使用 Azure 資源群組部署的連續整合 tooset Visual Studio 中的專案。"
services: visual-studio-online
documentationcenter: na
author: mlearned
manager: erickson-doug
editor: 
ms.assetid: b81c172a-be87-4adc-861e-d20b94be9e38
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: mlearned
ms.openlocfilehash: 0fe4a4b8989ee323e8ef2206fa4ebed503025670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-integration-in-visual-studio-team-services-using-azure-resource-group-deployment-projects"></a>使用 Azure 資源群組部署專案在 Visual Studio Team Services 中進行連續整合
toodeploy Azure 的範本，您在執行工作各個階段： 建置時，測試中，複製 tooAzure （也稱為 「 預備 」），並部署範本。 有兩個不同的方式 toodeploy 範本 tooVisual Studio Team Services (VS Team Services)。 這兩種方法提供 hello 相同的結果，因此請選擇最適合您的工作流程的其中一個 hello。

1. 加入執行包含 hello Azure 資源群組部署專案 (Deploy-azureresourcegroup.ps1) 中的 hello PowerShell 指令碼的單一步驟 tooyour 組建定義。 hello 指令碼複製成品，並將部署 hello 範本。
2. 新增多個 VS Team Services 建置步驟，每個都執行一個階段工作。

本文將示範兩個選項。 hello 第一個選項優點 hello hello 使用相同的指令碼開發人員使用 Visual Studio 中，並提供整個 hello 生命週期的一致性。 hello 第二個選項可提供方便的替代 toohello 內建指令碼。 這兩個程序假設您已經在 VS Team Services 中簽入 Visual Studio 部署專案。

## <a name="copy-artifacts-tooazure"></a>複製成品 tooAzure
不論 hello 案例中，如果您有任何所需的範本部署的成品必須提供 Azure Resource Manager 存取 toothem。 這些構件包括下列檔案：

* 巢狀範本
* 組態指令碼及 DSC 指令碼
* 應用程式二進位檔

### <a name="nested-templates-and-configuration-scripts"></a>巢狀範本和組態指令碼
當您使用 Visual Studio 所提供的 hello 範本 （或使用 Visual Studio 程式碼片段建置），hello PowerShell 指令碼不僅會設置 hello 成品，如需不同部署的 hello 資源 hello URI 也會參數化。 hello 指令碼，然後複製在 Azure 中的 hello 成品 tooa 安全容器、 建立 SaS 權杖，該容器，並接著會將 toohello 範本部署上的該資訊傳遞。 請參閱[建立範本部署](https://msdn.microsoft.com/library/azure/dn790564.aspx)toolearn 深入了解巢狀範本。  當 VS Team Services 中使用的工作，您必須選取針對範本部署的 hello 適當工作，並如有必要，請從預備環境步驟 toohello 範本部署的 hello 傳遞參數值。

## <a name="set-up-continuous-deployment-in-vs-team-services"></a>在 VS Team Services 中設定連續部署
您需要 tooupdate toocall VS Team Services 中的 hello PowerShell 指令碼，您的組建定義。 簡單地說，hello 步驟如下： 

1. 編輯 hello 組建定義。
2. 在 VS Team Services 中設定 Azure 授權。
3. 新增參考 hello hello Azure 資源群組部署專案中的 PowerShell 指令碼的 Azure PowerShell 建置步驟。
4. 設定 hello hello 值*-ArtifactsStagingDirectory*參數 toowork 與 VS Team Services 中所建置的專案。

### <a name="detailed-walkthrough-for-option-1"></a>選項 1 的詳細逐步解說
hello 下列程序引導您完成使用單一工作執行 hello PowerShell 指令碼專案中的 VS Team Services 中的 hello 步驟需要 tooconfigure 連續部署。 

1. 編輯您的 VS Team Services 組建定義並新增 Azure PowerShell 建置步驟。 選擇在 hello hello 組建定義**組建定義**類別目錄，然後選擇 hello**編輯**連結。
   
   ![編輯組建定義][0]
2. 加入新**Azure PowerShell**建置步驟 toohello 組建定義，然後選擇 hello**加入建置步驟...** 按鈕。
   
   ![新增組建步驟][1]
3. 選擇 hello**部署工作**類別目錄中，選取 hello **Azure PowerShell**工作，並再選擇其**新增** 按鈕。
   
   ![新增工作][2]
4. 選擇 hello **Azure PowerShell**建置步驟，然後填入其值。
   
   1. 如果您已經有 Azure 服務端點加入 tooVS Team Services 中，選擇 hello 訂閱 hello **Azure 訂用帳戶**下拉式清單方塊，然後略過 toohello 下一節。 
      
      如果您還沒有 Azure 服務端點在 VS Team Services 中，您會需要 tooadd 其中一個。 本小節會帶領您完成 hello 程序。 如果您的 Azure 帳戶使用 Microsoft 帳戶 （例如 Hotmail)，您必須採取下列步驟 tooget hello 服務主體驗證。
   2. 選擇 hello**管理**連結下一步 toohello **Azure 訂用帳戶**下拉式清單方塊。
      
      ![管理 Azure 訂用帳戶][3]
   3. 選擇**Azure**在 hello**新的服務端點**下拉式清單方塊。
      
      ![新增服務端點][4]
   4. 在 hello**新增 Azure 訂用帳戶**對話方塊中，選取 hello**服務主體**選項。
      
      ![服務主體選項][5]
   5. 加入您的 Azure 訂用帳戶資訊 toohello**新增 Azure 訂用帳戶** 對話方塊。 您需要下列項目 tooprovide hello:
      
      * 訂用帳戶識別碼
      * 訂用帳戶名稱
      * 服務主體識別碼
      * 服務主體金鑰
      * 租用戶識別碼
   6. 新增您選擇 toohello 名稱**訂用帳戶**名稱 方塊中。 這個值會出現在 hello 稍後**Azure 訂用帳戶**VS Team Services 中的下拉式清單。 
   7. 如果您不知道您的 Azure 訂用帳戶 ID，您可以使用下列命令 tooretrieve hello 的其中一個它。
      
      對於 Azure PowerShell 指令碼，請使用：
      
      `Get-AzureRmSubscription`
      
      對於 Azure CLI，請使用：
      
      `azure account show`
   8. tooget 服務主體識別碼、 服務主要金鑰和租用戶識別碼，請依照下列中的 hello 程序[建立 Active Directory 應用程式和服務主體使用入口網站](resource-group-create-service-principal-portal.md)或[驗證的服務主體Azure 資源管理員](resource-group-authenticate-service-principal.md)。
   9. 新增 hello 服務主體識別碼、 服務主要金鑰，以及租用戶識別碼值 toohello**新增 Azure 訂用帳戶**對話方塊方塊，然後選擇 [hello**確定**] 按鈕。
      
      您現在有有效的服務主體 toouse toorun hello Azure PowerShell 指令碼。
5. 編輯 hello 組建定義，並選擇 hello **Azure PowerShell**建置步驟。 選取 hello 訂用帳戶中 hello **Azure 訂用帳戶**下拉式清單方塊。 (如果 hello 訂用帳戶未出現，請選擇 hello**重新整理**按鈕的下一個 hello**管理**連結。) 
   
   ![安裝並設定 Azure PowerShell 建置工作][8]
6. 提供路徑 toohello Deploy-azureresourcegroup.ps1 PowerShell 指令碼。 toodo，選擇 hello 省略符號 （...） 按鈕的下一個 toohello**指令碼路徑**方塊中，瀏覽 toohello Deploy-azureresourcegroup.ps1 PowerShell 指令碼，在 hello**指令碼**您的專案的資料夾，選取它，然後選擇 [hello**確定**] 按鈕。    
   
   ![選取路徑 tooscript][9]
7. 您選取 hello 指令碼之後，更新 hello 路徑 toohello 指令碼，讓它會執行從 hello Build.StagingDirectory (hello 相同的目錄， *ArtifactsLocation*設)。 您可以藉由新增"$（Build.StagingDirectory)/"toohello 開頭 hello 指令碼路徑。
   
    ![編輯路徑 tooscript][10]
8. 在 hello**指令碼引數**方塊中，輸入下列參數 （在單一行） 中的 hello。 當您執行 Visual Studio 中的 hello 指令碼時，您可以查看如何與使用 hello 參數在 hello**輸出**視窗。 您可以使用它做為起點建置步驟中設定 hello 參數值。
   
   | 參數 | 說明 |
   | --- | --- |
   | -ResourceGroupLocation |hello hello 資源群組的位置，例如地理位置值**eastus**或**'美國東部'**。 （新增方以單引號包住如果 hello 名稱中有空格。）如需詳細資訊，請參閱 [Azure 區域](https://azure.microsoft.com/en-us/regions/)。 |
   | -ResourceGroupName |hello 用於這個部署的 hello 資源群組名稱。 |
   | -UploadArtifacts |此參數存在時，會指定需要 toobe 的成品上傳 tooAzure 從 hello 本機系統。 您只需要 tooset 此交換器如果範本部署需要額外的 toostage 使用 hello PowerShell 指令碼 （例如設定指令碼或巢狀的範本） 的成品。 |
   | -StorageAccountName |hello hello 儲存體帳戶名稱會用於此部署 toostage 成品。 僅在您執行部署的成品時才會使用這個參數。 如果沒有提供這個參數，如果 hello 指令碼已不會建立在先前的部署期間建立新的儲存體帳戶。 如果指定了 hello 參數，hello 儲存體帳戶必須已經存在。 |
   | -StorageAccountResourceGroupName |hello hello hello 儲存體帳戶相關聯的資源群組名稱。 Hello StorageAccountName 參數中提供的值時，才需要此參數。 |
   | -TemplateFile |hello 路徑 toohello 範本檔案 hello Azure 資源群組部署專案中。 使用這個參數，這是 hello PowerShell 指令碼，而不是絕對路徑的相對 toohello 位置路徑 tooenhance 彈性。 |
   | -TemplateParametersFile |hello 路徑 toohello 參數檔案 hello Azure 資源群組部署專案中。 使用這個參數，這是 hello PowerShell 指令碼，而不是絕對路徑的相對 toohello 位置路徑 tooenhance 彈性。 |
   | -ArtifactStagingDirectory |這個參數可讓您知道 hello 資料夾從 hello 專案的二進位檔案應該複製其中的 hello PowerShell 指令碼。 這個值會覆寫 hello hello PowerShell 指令碼所使用的預設值。 如需使用 VS Team Services，則將 hello 值設定為:-ArtifactStagingDirectory $(Build.StagingDirectory) |
   
   以下是指令碼引數的範例 (斷行以方便閱讀)：
   
   ```    
   -ResourceGroupName 'MyGroup' -ResourceGroupLocation 'eastus' -TemplateFile '..\templates\azuredeploy.json' 
   -TemplateParametersFile '..\templates\azuredeploy.parameters.json' -UploadArtifacts -StorageAccountName 'mystorageacct' 
   –StorageAccountResourceGroupName 'Default-Storage-EastUS' -ArtifactStagingDirectory '$(Build.StagingDirectory)'    
   ```
   
   當您完成時，hello**指令碼引數**方塊應該類似下列清單中的 hello:
   
   ![指令碼引數][11]
9. 您已新增所有 hello Azure PowerShell 建置步驟的必要項目 toohello 之後，請選擇 hello**佇列**建置按鈕 toobuild hello 專案。 hello**建置**螢幕會顯示 hello hello PowerShell 指令碼的輸出。

### <a name="detailed-walkthrough-for-option-2"></a>選項 2 的詳細逐步解說
hello 下列程序引導您完成使用 hello 內建工作 VS Team Services 中的 hello 步驟需要 tooconfigure 連續部署。

1. 編輯您 VS Team Services 組建定義 tooadd 兩個新組建的步驟。 選擇在 hello hello 組建定義**組建定義**類別目錄，然後選擇 hello**編輯**連結。
   
   ![編輯組建定義][12]
2. 加入新的 hello 建置步驟 toohello 組建定義使用 hello**加入建置步驟...** 按鈕。
   
   ![新增組建步驟][13]
3. 選擇 hello**部署**工作分類中，選取 hello **Azure File Copy**工作，並再選擇其**新增** 按鈕。
   
   ![新增 Azure 檔案複製工作][14]
4. 選擇 hello **Azure 資源群組部署**工作，然後選擇其**新增** 按鈕，然後**關閉**hello**工作目錄**。
   
   ![新增 [Azure 資源群組部署] 工作][15]
5. 選擇 hello **Azure File Copy**工作，並填入其值。
   
   如果您已經有 Azure 服務端點加入 tooVS Team Services 中，選擇 hello 訂閱 hello **Azure 訂用帳戶**下拉式清單方塊。 如果您沒有訂用帳戶，請參閱[選項 1](#detailed-walkthrough-for-option-1)，以查看在 VS Team Services 中設定訂用帳戶的指示。
   
   * 來源 - 輸入 **$(Build.StagingDirectory)**
   * Azure 連線類型 - 選取 **Azure Resource Manager**
   * Azure RM 訂用帳戶-您想要在 hello toouse hello 儲存體帳戶的訂用帳戶選取 hello **Azure 訂用帳戶**下拉式清單方塊。 如果 hello 訂用帳戶未出現，請選擇 hello**重新整理**按鈕的下一個 hello**管理**連結。
   * 目的地類型 - 選取 **Azure Blob**
   * 希望臨時成品 toouse RM 儲存體帳戶-選取您 hello 儲存體帳戶。
   * 容器名稱-輸入 hello 名稱的 hello 容器中，您想要 toouse 供暫存。它可以是任何有效的容器名稱，但使用一個專用的 toothis 組建定義
   
   Hello 輸出值：
   
   * 儲存體容器 URI - 輸入 **artifactsLocation**
   * 儲存體容器 SAS - 輸入 **artifactsLocationSasToken**
   
   ![設定 Azure 檔案複製工作][16]
6. 選擇 hello **Azure 資源群組部署**建置步驟，然後填入其值。
   
   * Azure 連線類型 - 選取 **Azure Resource Manager**
   * Azure RM 訂閱 hello 中部署的訂用帳戶選取 hello **Azure 訂用帳戶**下拉式清單方塊。 這通常會是相同的訂用帳戶使用的 hello hello 上一個步驟中
   * 動作 - 選取 **建立或更新資源群組**
   * 資源群組-選取的資源群組，或輸入 hello 部署新的資源群組的 hello 名稱
   * 位置-選取 hello hello 資源群組位置
   * 範本-輸入 hello 路徑和名稱 hello 範本部署 toobe 前面加上的**$(Build.StagingDirectory)**，例如： **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**
   * 範本參數的輸入 hello 路徑和名稱使用，hello 參數 toobe 前面加上**$(Build.StagingDirectory)**，例如： **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**
   * 覆寫範本參數-輸入或複製並貼上下列程式碼的 hello:
     
     ```    
     -_artifactsLocation $(artifactsLocation) -_artifactsLocationSasToken (ConvertTo-SecureString -String "$(artifactsLocationSasToken)" -AsPlainText -Force)
     ```
     ![設定 [Azure 資源群組部署] 工作][17]
7. 您已新增 hello 所需的所有項目之後，儲存 hello 組建定義，然後選擇**新組建排入佇列**hello 頂端。

## <a name="next-steps"></a>後續步驟
讀取[Azure 資源管理員概觀](azure-resource-manager/resource-group-overview.md)toolearn 深入了解 Azure 資源管理員和 Azure 資源群組。

[0]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough1.png
[1]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough2.png
[2]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough3.png
[3]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough4.png
[4]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough5.png
[5]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough6.png
[8]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough9.png
[9]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough10.png
[10]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough11b.png
[11]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough12.png
[12]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough13.png
[13]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough14.png
[14]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough15.png
[15]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough16.png
[16]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough17.png
[17]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough18.png
