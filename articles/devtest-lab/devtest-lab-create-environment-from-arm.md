---
title: "aaaCreate 環境多部 VM 和 PaaS 具有 Azure 資源管理員範本 |Microsoft 文件"
description: "深入了解如何 toocreate 多部 VM 的環境和 Azure Resource Manager 範本從 Azure DevTest Labs PaaS 資源"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: tarcher
ms.openlocfilehash: ab8628f6cb5a666435258efb93921ec69ad3a13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-multi-vm-environments-and-paas-resources-with-azure-resource-manager-templates"></a>使用 Azure Resource Manager 範本建立多個 VM 環境和 PaaS 資源

hello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)可讓您 tooeasily[建立並加入 VM tooa 實驗室](https://docs.microsoft.com/en-us/azure/devtest-lab/devtest-lab-add-vm)。 這適用於一次建立一個 VM。 不過，如果 hello 環境包含多個 Vm，每個 VM 有 toobe 分別建立。 例如多層式 Web 應用程式或 SharePoint 伺服器陣列的情況下，一種機制是需要的 tooallow hello 建立在單一步驟中的多個 Vm。 藉由使用 Azure 資源管理員範本，您可以現在定義 hello 基礎結構和 Azure 方案的組態，並重複地部署多個 Vm 一致的狀態。 這項功能提供下列優點 hello:

- Azure Resource Manager 範本會直接從您的原始檔控制儲存機制 (GitHub 或 Team Services Git) 載入。
- 您的使用者設定之後，才能挑選從 hello 做為其功能與其他類型的 Azure 入口網站的 Azure Resource Manager 範本來建立環境[VM 基底](./devtest-lab-comparing-vm-base-image-types.md)。
- 可以從 Azure Resource Manager 範本加法 tooIaaS Vm 中的環境中佈建 azure PaaS 資源。
- 加法 tooindividual Vm 建立其他類型的基底中的 hello 實驗室中可追蹤環境的 hello 成本。
- PaaS 資源所建立，而且會出現在成本追蹤。不過，VM 自動關機不適用 tooPaaS 資源。
- 使用者擁有 hello 相同 VM 原則控制的環境，因為它們已用於單一實驗室 Vm。

深入了解 hello 許多[使用資源管理員範本的優點](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#the-benefits-of-using-resource-manager)toodeploy、 更新或刪除所有實驗室資源在單一作業中。

> [!NOTE]
> 當您使用資源管理員範本為基礎 toocreate 多個實驗室 Vm 時，有一些差異 tookeep 記住是否建立多個 Vm 或單一 Vm。 使用虛擬機器的 Azure Resource Manager 範本會更詳細地說明這些差異。
>
>

## <a name="configure-azure-resource-manager-template-repositories"></a>設定 Azure Resource Manager 範本儲存機制

做為其中一個 hello 有基礎結構做為程式碼和組態與程式碼，環境範本的最佳作法應管理原始檔控制中。 Azure DevTest Labs 採用這種作法，並直接從您的 GitHub 或 VSTS Git 儲存機制載入所有 Azure Resource Manager 範本。 如此一來，資源管理員範本可跨 hello 整個發行週期，從 hello 測試 toohello 生產環境。

有幾個規則 toofollow tooorganize Azure 資源管理員範本放在儲存機制：

- hello 主要範本檔案必須命名為`azuredeploy.json`。 

    ![金鑰 Azure Resource Manager 範本檔案](./media/devtest-lab-create-environment-from-arm/master-template.png)

- 如果您想 toouse 參數檔案中定義的參數值時，必須為 hello 參數檔案`azuredeploy.parameters.json`。
- 您可以使用 hello 參數`_artifactsLocation`和`_artifactsLocationSasToken`tooconstruct hello parametersLink URI 值，允許 DevTest Labs tooautomatically 管理巢狀範本。 如需詳細資訊，請參閱 [How Azure DevTest Labs makes nested Resource Manager template deployments easier for testing environments](https://blogs.msdn.microsoft.com/devtestlab/2017/05/23/how-azure-devtest-labs-makes-nested-arm-template-deployments-easier-for-testing-environments/) (Azure DevTest Labs 如何簡化測試環境的巢狀 Resource Manager 範本部署)。
- 中繼資料可以是定義的 toospecify hello 範本顯示名稱和描述。 此中繼資料必須在名為 `metadata.json` 的檔案中。 hello 下列中繼資料檔範例將示範如何 toospecify hello 顯示名稱和描述： 

```json
{
 
"itemDisplayName": "<your template name>",
 
"description": "<description of hello template>"
 
}
```

hello 下列步驟將引導您透過加入使用 hello Azure 入口網站的儲存機制 tooyour 實驗室。 

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
1. 選取**更服務**，然後選取**DevTest Labs**從 hello 清單。
1. 從 hello 清單的實驗室中，選取 hello 所需的實驗室。   
1. 在 hello 實驗室刀鋒視窗中，選取 **組態和原則**。

    ![組態和原則](./media/devtest-lab-create-environment-from-arm/configuration-and-policies-menu.png)

1. 從 hello**組態和原則**設定清單中，選取**儲存機制**。 hello**儲存機制**刀鋒視窗會列出已加入 toohello 實驗室 hello 儲存機制。 名為儲存機制`Public Repo`會自動產生的所有實驗室，並連接 toohello [DevTest Labs GitHub 儲存機制](https://github.com/Azure/azure-devtestlab)，其中包含您可以使用數個 VM 成品。

    ![公用儲存機制](./media/devtest-lab-create-environment-from-arm/public-repo.png)

1. 選取**新增 +** tooadd 您的 Azure Resource Manager 範本儲存機制。
1. 當第二個 hello**儲存機制**刀鋒視窗隨即開啟，輸入 hello 的必要資訊，如下所示：
    - **名稱**-輸入 hello 實驗室中的 hello 用的儲存機制名稱。
    - **Git 複製 URL** -從 GitHub 或 Visual Studio Team Services 輸入 hello GIT HTTPS 複製 URL。  
    - **分支**-輸入 hello 分支名稱 tooaccess 您的 Azure Resource Manager 範本定義。 
    - **個人存取權杖**-hello 個人存取權杖用 toosecurely 存取您的儲存機制。 您的權杖，從 Visual Studio Team Services 中，選取 tooget  **&lt;YourName >> 我的設定檔 > 安全性 > 公用存取語彙基元**。 tooget 您的權杖從 GitHub，選取您的顯示圖片後面接著選取**設定 > 公用存取語彙基元**。 
    - **資料夾路徑**-使用其中一種 hello 兩個輸入欄位，輸入 hello 的資料夾路徑開頭是正斜線-/-且相對 tooyour Git 複製 URI tooeither 成品定義 （第一個輸入的欄位） 或您的 Azure Resource Manager 範本定義。   
    
        ![公用儲存機制](./media/devtest-lab-create-environment-from-arm/repo-values.png)

1. Hello 所需的所有欄位輸入，並傳遞 hello 驗證，請選取**儲存**。

hello 下一節將引導您完成從 Azure Resource Manager 範本建立環境。

## <a name="create-an-environment-from-an-azure-resource-manager-template"></a>從 Azure Resource Manager 範本建立環境

Hello 實驗室中設定的 Azure Resource Manager 範本存放庫之後, 您的實驗室使用者可以建立 hello 步驟搭配使用 Azure 入口網站的環境：

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
1. 選取**更服務**，然後選取**DevTest Labs**從 hello 清單。
1. 從 hello 清單的實驗室中，選取 hello 所需的實驗室。   
1. 在 hello 實驗室刀鋒視窗中，選取 **新增 +**。
1. hello**選擇基底**刀鋒視窗會顯示 hello 基底映像，您可以使用列於首位的 hello Azure Resource Manager 範本。 選取 hello 所需的 Azure Resource Manager 範本。

    ![選擇基底](./media/devtest-lab-create-environment-from-arm/choose-a-base.png)
  
1. 在 hello**新增**刀鋒視窗中，輸入 hello**環境名稱**值。 hello 環境名稱是會顯示的 tooyour hello 實驗室中的使用者。 hello 其餘的輸入的欄位會定義在 hello Azure Resource Manager 範本。 如果預設值會定義在 hello 範本或 hello`azuredeploy.parameter.json`檔案是否存在，預設值都會顯示在這些輸入欄位中。 類型參數*安全字串*，您可以使用儲存在 hello 實驗室中的 hello 密碼[個人密碼存放區](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)。

    ![新增刀鋒視窗](./media/devtest-lab-create-environment-from-arm/add.png)

    > [!NOTE]
    > 有幾個參數值 (即使指定) 會顯示為空值。 因此，如果使用者指派 Azure Resource Manager 範本中的這些值 tooparameters，DevTest Labs 不會顯示 hello 值;改為顯示 hello 實驗室使用者必須 tooenter 空白輸入的欄位的值建立 hello 環境。
    > 
    > - GEN-UNIQUE
    > - GEN-UNIQUE-[N]
    > - GEN-SSH-PUB-KEY
    > - GEN-PASSWORD 
 
1. 選取**新增**toocreate hello 環境。 hello 環境啟動佈建立即 hello 狀態顯示在 hello**我的虛擬機器**清單。 新的資源群組會自動建立 hello 實驗室 tooprovision hello Azure Resource Manager 範本中定義的所有 hello 資源。
1. 一旦建立 hello 環境時，選取 hello 環境中 hello**我的虛擬機器**清單 tooopen hello 資源群組 刀鋒視窗並瀏覽所有 hello hello 環境中，佈建的資源。
    
    ![我的虛擬機器清單](./media/devtest-lab-create-environment-from-arm/all-environment-resources.png)
   
   您也可以展開 Vm 佈建 hello 環境中的 hello 環境 tooview 只 hello 的清單。
    
    ![我的虛擬機器清單](./media/devtest-lab-create-environment-from-arm/my-vm-list.png)

1. 按一下任何 hello 環境 tooview hello 可用的動作-例如套用成品，附加資料磁碟、 變更自動關機時間等等。

    ![環境動作](./media/devtest-lab-create-environment-from-arm/environment-actions.png)

## <a name="next-steps"></a>後續步驟
* 一旦建立 VM 之後，您可以藉由選取連接 toohello VM**連接**hello VM 刀鋒視窗上。
* 檢視和管理的環境中的資源中 hello 選取 hello 環境**我的虛擬機器**實驗室中的清單。 
* 瀏覽 hello [Azure 資源管理員範本，從 Azure 快速入門範本庫](https://github.com/Azure/azure-quickstart-templates)
