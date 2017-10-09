---
title: "aaaAzure managed hello Marketplace 中的應用程式 |Microsoft 文件"
description: "描述 Azure 受管理的應用程式，可透過 hello Marketplace。"
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a>Azure 受管理的 hello Marketplace 中的應用程式

 MSPs、 Isv 和系統整合業者 (Si) 可以使用 Azure 受管理應用程式 toooffer 解決方案 tooall Azure Marketplace 客戶。 這類方案減少 hello 維護與服務的客戶的額外負荷。 發行者可以銷售基礎結構和透過 hello Marketplace 的軟體。 服務和作業支援 toomanaged 應用程式，就可以將它們附加。 如需詳細資訊，請參閱[受管理的應用程式概觀](managed-application-overview.md)。

本文說明如何 MSP、 ISV 或 si 亦然可以發行應用程式 toohello Marketplace 並使其廣泛受到使用 toocustomers。

## <a name="prerequisites-for-publishing-a-managed-application"></a>發行受管理應用程式的必要條件

必要條件 toolisting hello Marketplace 中：

* 技術需求

    *  如需 hello 基本結構和語法的 Azure 資源管理員範本，請參閱[Azure 資源管理員範本](resource-group-authoring-templates.md)。
    *  tooview 完成範本方案比較，請參閱[Azure 快速入門範本](https://azure.microsoft.com/en-us/documentation/templates/)或 hello[快速入門範本儲存機制](https://github.com/azure/azure-quickstart-templates)。
    *  如需如何 toocreate hello 介面透過 hello Marketplace 應用程式部署的客戶資訊，請參閱[建立使用者介面的定義檔](managed-application-createuidefinition-overview.md)。

* 非技術性 (商務需求)

    *   您的公司或其子公司，都必須位於國家/地區銷售其中受到 hello Marketplace。
    *   必須授權產品與支援 hello Marketplace 計費模型相容的方式。
    *   您負責進行技術支援人員可以使用 toocustomers 盡商業上合理的方式。 hello 支援可以免費的付費，或透過社群支援。
    *   您必須負責為您的軟體和任何第三方廠商相依性進行授權。
    *   您必須提供符合準則的供應項目 toobe 的內容列出 hello 和 hello Marketplace 中 Azure 入口網站。
    *   您必須同意 toohello hello Azure Marketplace 參與原則和發行者合約的條款。
    *   您必須同意 toocomply hello 使用條款、 Microsoft 隱私權聲明，與 Microsoft Azure 認證程式合約。

## <a name="create-a-new-azure-application-offer"></a>建立新的 Azure 應用程式供應項目

符合 hello 必要條件之後，您便準備好 toocreate 您受管理的應用程式提供的服務。 讓我們先快速概觀供應項目和 SKU。

### <a name="offer"></a>提供項目

受管理的應用程式的 hello 優惠對應 tooa 類別的供應項目從 「 發行者 」 的產品。 如果您有想 toomake hello Marketplace 中可用的方案/應用程式的新類型時，您可以設定它為新的優惠。 優惠 SKU 的集合。 每個供應項目會顯示為自己 hello Marketplace 中的實體。

### <a name="sku"></a>SKU

SKU 不 hello 最小可單位的提供項目。 您可以使用內 hello SKU 相同產品類別 （優惠） toodifferentiate 之間：

* 所支援的不同功能。
* 是否 hello 供應項目為 managed 或 unmanaged。
* 支援的計費模型。

SKU 之下 hello 父 hello Marketplace 中供應項目。 它會顯示為其本身可實體 hello Azure 入口網站中。

### <a name="set-up-an-offer"></a>設定供應項目

1. 登入 toohello [Cloud Partner 入口網站](https://cloudpartner.azure.com/)。

2. Hello hello 左側瀏覽窗格中選取**+ 新的優惠** > **Azure 應用程式**。

    ![新增供應項目](./media/managed-application-author-marketplace/newOffer.png)

3. 填寫 hello 表單出現在 hello 處於 hello**編輯器**檢視。 必填欄位會標示紅色星號 (*)。

    ![供應項目](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    四種主要形式是使用的 toocreate 受管理的應用程式：

    a. 優惠設定

    b. SKU

    c. Marketplace

    d. 支援

Hello 下列各節將詳細說明這些表單。

## <a name="offer-settings-form"></a>供應項目設定表單
使用這個基本形式 toospecify hello 優惠設定。

1. 填寫 hello**提供設定**表單。 hello 不同欄位如下：

    a. **提供識別碼**： 這個唯一識別碼識別 「 發行者 」 設定檔中的 hello 供應項目。 此識別碼會顯示在產品的 URL，Resource Manager 範本和計費報告中。 此識別碼只能包含小寫英數字元或連字號 (-)。 hello 識別碼結尾不得為破折號。 它是有限的 tooa 最多 50 個字元。 供應項目上架後，此欄位便會鎖住。

    b. **發行者 ID**： 使用這個下拉式清單 toochoose hello 「 發行者 」 設定檔想 toopublish 下的這項優惠。 供應項目上架後，此欄位便會鎖住。

    c. **名稱**： 您的優惠此顯示名稱會出現在 hello Marketplace 和 hello 入口網站中。 它最多不能超過 50 個字元。 包含產品的可辨識品牌名稱。 請勿在此包含您的公司名稱，除非這是行銷方式。 如果您在您自己的網站上行銷這項優惠，請確定 hello 名稱是完全在您的網站上的顯示方式。

2. 選取**儲存**toosave 進度。 

## <a name="skus-form"></a>SKU 表單
hello 下一個步驟是您的優惠的 tooadd Sku。

1. 選取 [SKU] > [新增 SKU]。 

    ![選取新的 SKU](./media/managed-application-author-marketplace/newOffer_skus.png)

2. 輸入 [SKU 識別碼]。 SKU 識別碼是提供項目中的 hello SKU 的唯一識別碼。 此識別碼會顯示在產品的 URL，Resource Manager 範本和計費報告中。 此識別碼只能包含小寫英數字元或連字號 (-)。 hello 識別碼不能結束虛線，且限制的 tooa 最多 50 個字元。 供應項目上架後，此欄位便會鎖住。 您可以在一個優惠內建立多個 SKU。 您需要 SKU 想 toopublish 每個映像。

3. 填寫 hello **SKU 詳細資料**hello 遵循表單上的區段：

    ![提供新的 SKU](./media/managed-application-author-marketplace/newOffer_newsku.png)

    填寫下列欄位的 hello:
    
    a. **標題**：輸入此 SKU 的標題。 此標題會出現在 hello 藝廊，適合於這個項目。

    b. **摘要**：輸入此 SKU 的簡短摘要。 此文字會顯示 hello 標題底下。

    c. **描述**： 輸入 hello SKU 的詳細的描述。

    d. **SKU 類型**: hello 允許的值為**管理的應用程式**和**解決方案範本**。 此案例中，選取 [受管理的應用程式]。

4. 填寫 hello**套件詳細資料**hello 遵循表單上的區段：

    ![Package](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    填寫下列欄位的 hello:

    a. **目前版本**： 輸入您上傳的 hello 封裝版本。 Hello 格式應為`{number}.{number}.{number}{number}`。

    b. **選取封裝檔案**： 此套件包含下列檔案壓縮成.zip 檔 hello:
    * **applianceMainTemplate.json**: hello 用 toodeploy hello 方案/應用程式部署範本檔案。 如需有關資訊 toocreate 部署範本檔案，請參閱[建立第一個 Azure Resource Manager 範本](resource-manager-create-first-template.md)。
    * **appliancecreateUIDefinition.json**: hello Azure 入口網站 toogenerate hello 使用者介面使用 tooprovision 方案/應用程式會使用此檔案。 如需詳細資訊，請參閱[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。
    * **mainTemplate.json**： 這個範本檔案包含 hello Microsoft.Solution/appliances 資源。 hello mainTemplate 檔案包含下列屬性的 hello:

        *  **種類**： 使用**Marketplace** hello Marketplace 中的受管理應用程式。
        *  **ManagedResourceGroupId**: hello 客戶的訂用帳戶中的這個資源群組是 applianceMainTemplate.json 中定義的所有 hello 資源都部署的位置。
        *  **PublisherPackageId**： 這個字串可唯一識別 hello 封裝。 提供的 hello 格式中的 hello 值`{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`。

取得 hello**提供識別碼**和**發行者識別碼**從 hello 發佈入口網站中 hello 下列影像所示：

![優惠識別碼](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
取得 hello **SKU 識別碼**hello 下列影像所示：

![SKU 識別碼](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
取得 hello 套件**版本**hello 下列影像所示：

![套件版本](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  根據前面範例的 hello，hello 值**PublisherPackageId**是`azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`。

  範例 mainTemplate.json：

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

此套件應該包含任何巢狀的範本，或需要的 toosuccessfully 的指令碼佈建此應用程式。 hello mainTemplate.json、 applianceMainTemplate.json 和 applianceCreateUIDefinition.json 檔案必須存在於 hello 根資料夾。

* **授權**： 此屬性會定義誰 toohello 客戶的訂用帳戶中的資源取得存取權與 hello 的存取層級。 hello 發行者可以使用它代表 hello 客戶 toomanage hello 應用程式。
* **PrincipalId**： 這個屬性是使用者、 使用者群組或已授與 hello 客戶的訂用帳戶中的 hello 資源上的特定權限的應用程式的 hello Azure Active Directory (Azure AD) 識別項。 hello 角色定義描述 hello 權限。 
* **角色定義**： 這個屬性是所有 hello 內建角色型存取控制 (RBAC) 角色的 Azure AD 所提供的清單。 您可以選取最適合 toouse toomanage hello 資源是代表 hello 客戶的 hello 角色。

您可以新增多個授權。 建議您建立 AD 使用者群組並且在 **PrincipalId** 中指定其識別碼。 如此一來，您可以加入更多使用者 toohello 使用者群組，但不允許 hello 需要 tooupdate hello SKU。

如需 RBAC 的詳細資訊，請參閱[hello Azure 入口網站中開始使用 RBAC](../active-directory/role-based-access-control-what-is.md)。

## <a name="marketplace-form"></a>Marketplace 表單

hello Marketplace 表單詢問 hello 上顯示的欄位[Azure Marketplace](https://azuremarketplace.microsoft.com)在 hello [Azure 入口網站](https://portal.azure.com/)。

### <a name="preview-subscription-ids"></a>預覽訂用帳戶識別碼

輸入 Azure 訂用帳戶可存取 hello 提供，發行後的識別碼的清單。 您在進行之前，您可以使用這些空白列的訂閱 tootest hello 預覽提供即時。 您可以編譯 too100 訂閱 hello 合作夥伴入口網站中的空白清單。

### <a name="suggested-categories"></a>建議的類別

選取從您提供的服務可以與最相關的 hello 清單 toofive 類別。 這些類別位於 hello 您優惠 toohello 產品類別目錄會使用的 toomap [Azure Marketplace](https://azuremarketplace.microsoft.com)和 hello [Azure 入口網站](https://portal.azure.com/)。

#### <a name="azure-marketplace"></a>Azure Marketplace

managed 應用程式的 hello 摘要會顯示 hello 下列欄位：

![Marketplace 摘要](./media/managed-application-author-marketplace/publishvm10.png)

hello**概觀**索引標籤上，您受管理的應用程式會顯示 hello 下列欄位：

![Marketplace 概觀](./media/managed-application-author-marketplace/publishvm11.png)

hello**計劃 + 定價**索引標籤上，您受管理的應用程式會顯示 hello 下列欄位：

![Marketplace 方案](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a>Azure 入口網站

managed 應用程式的 hello 摘要會顯示 hello 下列欄位：

![入口網站摘要](./media/managed-application-author-marketplace/publishvm12.png)

managed 應用程式的 hello 概觀會顯示 hello 下列欄位：

![入口網站概觀](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a>標誌指導方針

請遵循下列指導方針任何您在 hello Cloud Partner 入口網站中上傳的標誌：

*   hello Azure 設計具有簡單的調色盤。 限制 hello 數目主要和次要色彩上您的標誌。
*   hello hello 入口網站的佈景主題色彩是白色與黑色。 請勿使用這些色彩 hello 背景色彩為您的標誌。 使用色彩，讓您的標誌 hello 入口網站中。 建議您使用簡單的主要色彩。 *如果您使用透明背景，請確定 hello 標誌和文字不是白色的黑色或藍色。*
*   請勿在 hello 標誌上使用漸層的背景。
*   不要將文字放在 hello 標誌，即使貴公司或品牌名稱。 hello 的外觀與您的標誌應該是一般，而且避免漸層。
*   請確定 hello 標誌不會自動縮放。

#### <a name="hero-logo"></a>主圖標誌

hello 英雄標誌是選擇性的。 hello 發行者可以選擇不 tooupload 英雄標誌。 上傳 hello 英雄圖示之後，無法刪除。 在這段時間，hello 夥伴必須遵循英雄圖示的 hello Marketplace 指導方針。

請遵循下列指導方針 hello 英雄標誌圖示：

*   hello 發行者顯示名稱、 hello 計劃，顯示標題與 hello 供應項目完整摘要會以白色。 因此，不是使用淺色背景 hello hello 英雄圖示。 主圖圖示不得使用黑色、白色和透明背景。
*   列出 hello 供應項目之後，hello 發行者顯示名稱、 hello 計劃標題、 hello 供應項目完整摘要和 hello**建立**按鈕將以程式設計的方式內嵌在 hello 英雄標誌。 因此，請勿輸入任何文字時設計 hello 英雄標誌。 保留空白空間上 hello 右因為 hello 文字包含以程式設計方式在該空間。 hello 空白空間的 hello 文字應該是右 hello 415 x 100 像素。 它可經由從 hello 左 370 像素為單位。

    ![主圖標誌範例](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a>支援表單

填寫 hello**支援**貴公司連絡人表單和支援。 此資訊可能是工程連絡人和客戶支援連絡人。

## <a name="publish-an-offer"></a>發佈提供項目

請填寫所有 hello 區段之後，請選取**發行**可讓您提供可用 toocustomers toostart hello 程序。

## <a name="next-steps"></a>後續步驟

* 對於簡介 toomanaged 應用程式，請參閱[受管理應用程式概觀](managed-application-overview.md)。
* 使用來自 hello Marketplace 的受管理應用程式的相關資訊，請參閱[取用 Azure managed hello Marketplace 中的應用程式](managed-application-consume-marketplace.md)。
* 如需發佈 Service Catalog 受管理應用程式的資訊，請參閱[建立和發佈 Service Catalog 受管理的應用程式](managed-application-publishing.md)。
* 如需使用 Service Catalog 受管理應用程式的詳細資訊，請參閱[使用 Service Catalog 受管理的應用程式](managed-application-consumption.md)。
