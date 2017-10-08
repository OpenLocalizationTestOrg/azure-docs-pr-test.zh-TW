---
title: "aaaAzure 資源管理員概觀 |Microsoft 文件"
description: "描述如何 toouse Azure 資源管理員部署、 管理和 Azure 上的存取控制的資源。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 76df7de1-1d3b-436e-9b44-e1b3766b3961
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: tomfitz
ms.openlocfilehash: a44fccd96d722c006224145d71cc44292255debf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-overview"></a>Azure Resource Manager 概觀
許多元件 – 也許虛擬機器、 儲存體帳戶和虛擬網路或 web 應用程式、 資料庫、 資料庫伺服器和第 3 個合作對象服務 hello 基礎結構，您的應用程式通常由所組成。 您看不到這些元件作為個別的實體，而是看到它們作為單一實體相關且彼此相依的組件。 您想 toodeploy、 管理和監視這些群組。 Azure 資源管理員可讓您與您的方案中的 hello 資源 toowork 為群組。 您可以部署、 更新或刪除您的解決方案是單一的協調作業，在 hello 的所有資源。 您會使用部署的範本，且該範本可以用於不同的環境，例如測試、預備和生產環境。 資源管理員提供安全性、 稽核和標記功能 toohelp 部署後管理您的資源。 

## <a name="terminology"></a>術語
如果您是新 tooAzure 資源管理員，有一些您可能不熟悉的一些辭彙。

* **資源** - 透過 Azure 提供的可管理項目。 部分常見資源有虛擬機器、儲存體帳戶、Web 應用程式、資料庫和虛擬網路，但這只是其中一小部分。
* **資源群組** - 保留 Azure 方案相關資源的容器。 hello 資源群組可包含 hello 方案的所有 hello 資源或您想 toomanage 為群組的資源。 您決定要如何 tooallocate 資源 tooresource 根據錯誤群組構成 hello 最適合您的組織。 請參閱 [資源群組](#resource-groups)。
* **資源提供者**-提供 hello 資源的服務您可以部署及管理透過資源管理員。 每個資源提供者會提供以使用已部署的 hello 資源的作業。 某些共用的資源提供者是 Microsoft.Compute，提供 hello 虛擬機器資源、 Microsoft.Storage，提供 hello 儲存體帳戶資源，以及 Microsoft.Web，提供資源相關的 tooweb 應用程式。 請參閱 [資源提供者](#resource-providers)。
* **資源管理員範本**-A JavaScript Object Notation (JSON) 檔案，定義一個或多個資源 toodeploy tooa 資源群組。 它也會定義 hello hello 部署資源之間的相依性。 一致的方式和重複 hello 範本可以使用的 toodeploy hello 資源。 請參閱 [範本部署](#template-deployment)。
* **宣告式語法**-可讓您的語法狀態 」 以下是 我想要 toocreate"而不需要的程式設計命令 toocreate toowrite hello 順序它。 hello Resource Manager 範本是宣告式語法的範例。 在 hello 檔案中，您可以定義 hello 基礎結構 toodeploy tooAzure hello 屬性。 

## <a name="hello-benefits-of-using-resource-manager"></a>使用資源管理員的 hello 優點
Resource Manager 會提供數個優點：

* 您可以部署、 管理及監視您的方案 hello 的所有資源群組，而非個別處理這些資源。
* 重複，您可以部署整個 hello 開發生命週期方案，並確保一致的狀態以部署您的資源。
* 您可以透過宣告式範本而非指令碼來管理基礎結構。
* 您可以定義 hello 資源，所以它們部署在 hello 正確的順序之間的相依性。
* 因為角色型存取控制 (RBAC) 原生整合至 hello 管理平台，您可以套用存取控制 tooall 服務資源群組中。
* 您可以將標籤套用 tooresources toologically 組織您的訂用帳戶中的所有 hello 資源。
* 您可以藉由檢視群組的資源成本釐清您組織的計費共用 hello 相同的標記。  

資源管理員提供新的方式 toodeploy 和管理您的方案。 如果您使用 hello 舊版部署模型而且想 toolearn 有關 hello 變更，請參閱[了解資源管理員部署和傳統部署](resource-manager-deployment-model.md)。

## <a name="consistent-management-layer"></a>一致的管理層
資源管理員的 hello 執行的工作，透過 Azure PowerShell、 Azure CLI、 Azure 入口網站、 REST API 和開發工具提供一致的管理層。 所有的 hello 工具會使用一組常見的作業。 您使用最適合您，且可以交換使用而不會混淆的 hello 工具。 

hello 下列影像顯示如何與互動的所有 hello 工具 hello 相同的 Azure 資源管理員 API。 hello API 將要求傳遞 toohello 資源管理員服務，以便驗證與授權 hello 要求。 資源管理員然後路由傳送嗨要求 toohello 適當的資源提供者。

![Resource Manager 要求模型](./media/resource-group-overview/consistent-management-layer.png)

## <a name="guidance"></a>指引
hello 下列建議可協助您使用您的方案時，要充分利用的資源管理員。

1. 定義和部署基礎結構透過 hello 資源管理員範本中的宣告式語法，而非透過命令式命令。
2. Hello 範本中定義所有的部署和設定步驟。 您在設定方案時應該沒有手動步驟。
3. 執行您的資源，例如 toostart 命令式命令 toomanage 或停止的應用程式或電腦。
4. 以 hello 排列資源的資源群組中的相同生命週期。 將標記用於資源的所有其他組織方式。

如需範本的建議，請參閱[建立 Azure Resource Manager 範本的最佳做法](resource-manager-template-best-practices.md)。

如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。

## <a name="resource-groups"></a>資源群組
定義您的資源群組時，有一些重要因素 tooconsider:

1. 群組中的所有 hello 資源都應該都共用相同的生命週期的 hello。 您可一起部署、更新和刪除它們。 如果一個資源，例如資料庫伺服器，需要在不同的部署週期 tooexist 應該可以在另一個資源群組中。
2. 每個資源只能存在於一個資源群組中。
3. 您可以新增或移除資源 tooa 資源群組在任何時間。
4. 您可以將資源從一個資源群組 tooanother 群組。 如需詳細資訊，請參閱[移動資源 toonew 資源群組或訂用帳戶](resource-group-move-resources.md)。
5. 資源群組可以包含位於不同區域中的資源。
6. 資源群組可以是用於系統管理動作 tooscope 存取控制。
7. 資源可與其他資源群組中的資源互動。 Hello 兩個資源相關，但不是會共用時，這個互動是很常見 hello 相同生命週期 （例如，web 應用程式連接 tooa 資料庫）。

建立資源群組時，您會需要 tooprovide 位置，該資源群組。 您可能會想：「為什麼資源群組需要位置？ 如果 hello 資源可以有不同的位置比 hello 資源群組，為什麼沒有 hello 資源群組位置重要完全？ 」 hello 資源群組，儲存 hello 資源的相關中繼資料。 因此，當您指定 hello 資源群組的位置，就指定儲存的中繼資料。 基於相容性因素，您可能需要 tooensure 資料儲存在特定區域中。

## <a name="resource-providers"></a>資源提供者
每個資源提供者都會提供一組資源和作業，以便能運用 Azure 服務。 例如，如果您想 toostore 金鑰和密碼，則處理 hello **Microsoft.KeyVault**資源提供者。 這個資源提供者提供的資源類型，稱為**保存庫**建立 hello 金鑰保存庫。 

hello 資源類型名稱的格式 hello: **{資源提供者} / {資源類型}**。 例如，hello 金鑰保存庫類型是**Microsoft.KeyVault/vaults**。

開始與部署您的資源，使用之前，您應該了解 hello 可用資源提供者。 您想 toodeploy tooAzure 知道 hello 名稱的資源提供者和資源可協助您定義的資源。 此外，您可以針對每個資源類型需要 tooknow hello 有效的位置和 API 版本。 如需詳細資訊，請參閱[資源提供者和類型](resource-manager-supported-services.md)。

## <a name="template-deployment"></a>範本部署
使用資源管理員中，您可以建立定義 hello 基礎結構和 Azure 方案的組態 （以 JSON 格式） 的範本。 透過範本，您可以在整個生命週期中重複部署方案，並確信您的資源會以一致的狀態部署。 當您從 hello 入口網站建立一個方案時，hello 方案會自動包含部署範本。 您不需要 toocreate 從頭範本因為您可以從您的方案的開始 hello 範本並進行自訂 toomeet 您的特定需求。 您可以匯出 hello hello 資源群組，目前的狀態或是檢視用於特定部署的 hello 範本來擷取現有的資源群組的範本。 檢視 hello[匯出範本](resource-manager-export-template.md)是很有幫助方式 toolearn hello 範本語法的相關。

toolearn hello 格式的 hello 範本和建構它，請參閱[建立第一個 Azure Resource Manager 範本](resource-manager-create-first-template.md)。 tooview hello JSON 語法資源類型，請參閱[Azure Resource Manager 範本中定義的資源](/azure/templates/)。

資源管理員處理 hello 像任何其他要求的範本 (請參閱 hello 影像[一致的管理層](#consistent-management-layer))。 它會剖析 hello 範本，並將其語法轉換成的 hello 適當的資源提供者 REST API 作業。 例如，當資源管理員收到範本具有下列資源定義的 hello:

```json
"resources": [
  {
    "apiVersion": "2016-01-01",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "mystorageaccount",
    "location": "westus",
    "sku": {
      "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {
    }
  }
]
```

它會將轉換 hello 定義 toohello 下列 REST API 作業，因為它會傳送 toohello Microsoft.Storage 資源提供者：

```HTTP
PUT
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/mystorageaccount?api-version=2016-01-01
REQUEST BODY
{
  "location": "westus",
  "properties": {
  }
  "sku": {
    "name": "Standard_LRS"
  },   
  "kind": "Storage"
}
```

您定義的範本和資源群組已完全啟動 tooyou 和您要如何 toomanage 您的方案。 例如，您可以部署三層應用程式透過單一範本 tooa 單一資源群組。

![三層式範本](./media/resource-group-overview/3-tier-template.png)

但是，如果您沒有 toodefine 整個基礎結構在單一範本。 通常，它可讓意義 toodivide 成一組目標、 目的特定範本部署需求。 您可以輕鬆地將這些份本重複使用於不同的方案。 toodeploy 特定的方案，您會建立主要的範本，用來連結所有必要的 hello 範本。 hello 如下圖所示 toodeploy 三層解決方案透過父範本包含三個巢狀方式範本。

![巢狀階層範本](./media/resource-group-overview/nested-tiers-template.png)

如果您想像您具有獨立的生命週期的層，您可以部署三個層級 tooseparate 資源群組。 請注意 hello 資源仍然可以在其他資源群組中的連結的 tooresources。

![階層範本](./media/resource-group-overview/tier-templates.png)

如需更多有關設計範本的建議，請參閱[設計 Azure Resource Manager 範本的模式](best-practices-resource-manager-design-templates.md)。 如需巢狀範本的相關資訊，請參閱[透過 Azure Resource Manager 使用連結的範本](resource-group-linked-templates.md)。

Azure 資源管理員會分析 hello 正確的順序會建立 tooensure 資源的相依性。 如果某個資源依賴另一個資源的值 (例如需要儲存體帳戶以供磁碟使用的虛擬機器)，您必須設定相依性。 如需詳細資訊，請參閱 [定義 Azure Resource Manager 範本中的相依性](resource-group-define-dependencies.md)。

您也可以使用 hello 範本更新 toohello 基礎結構。 例如，您可以將資源 tooyour 方案，並將已部署的 hello 資源設定規則。 如果 hello 範本會指定建立資源，但該資源已存在，Azure 資源管理員會執行更新，而不是建立新的資產。 Azure 資源管理員更新 hello 現有資產 toohello 相同狀態做為它就是當新的。  

當您需要其他的作業，例如安裝不包含在 hello 安裝程式的特定軟體時，資源管理員會提供擴充功能案例。 如果您已經使用組態管理服務，例如 DSC、Chef 或 Puppet，您可以透過使用擴充功能繼續使用該服務。 如需虛擬機器擴充功能的相關資訊，請參閱[有關虛擬機器擴充功能和功能](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 

最後，hello 範本會變成 hello 原始碼應用程式的一部分。 您可以將它簽入 tooyour 原始程式碼儲存機制，並隨著您的應用程式發展更新。 您可以編輯 hello 範本，透過 Visual Studio。

定義您的範本之後, 您就準備好 toodeploy hello 資源 tooAzure。 如需 hello 命令 toodeploy hello 資源，請參閱：

* [使用 Resource Manager 範本與 Azure PowerShell 來部署資源](resource-group-template-deploy.md)
* [使用 Resource Manager 範本與 Azure CLI 部署資源](resource-group-template-deploy-cli.md)
* [使用 Resource Manager 範本與 Azure 入口網站來部署資源](resource-group-template-deploy-portal.md)
* [使用 Resource Manager 範本和 Resource Manager REST API 部署資源](resource-group-template-deploy-rest.md)

## <a name="tags"></a>標記
資源管理員提供標記的功能可讓您根據管理或帳單的 tooyour 需求 toocategorize 資源。 當您有複雜的資源群組和資源，而且需要 toovisualize 這些資產，可透過 hello 大部分意義 tooyou hello 方式，請使用標記。 例如，您可以標記您的組織中具有類似的角色，或屬於 toohello 資源相同的部門。 沒有標記，您的組織中的使用者可以建立多個資源，可能會難以 toolater 識別及管理。 比方說，您可能需要 toodelete 特定專案的所有 hello 資源。 如果這些資源不會標記為 hello 專案，您必須 toomanually 找到它們。 標記可以是重要的方式，讓您 tooreduce 不必要的成本，您的訂用帳戶中。 

資源不需要在 hello tooreside 相同資源群組 tooshare 標記。 您可以建立您自己標記分類 tooensure 您組織中的所有使用者都使用通用標記，而不是使用者不小心套用稍微不同的標籤 （例如 「 部門 」 而不是 「 部門 」）。

hello 下列範例會顯示套用標籤 tooa 虛擬機器。

```json
"resources": [    
  {
    "type": "Microsoft.Compute/virtualMachines",
    "apiVersion": "2015-06-15",
    "name": "SimpleWindowsVM",
    "location": "[resourceGroup().location]",
    "tags": {
        "costCenter": "Finance"
    },
    ...
  }
]
```

tooretrieve 所有 hello 資源標記值，都使用下列 PowerShell cmdlet 的 hello:

```powershell
Find-AzureRmResource -TagName costCenter -TagValue Finance
```

或者，hello 下列 Azure CLI 2.0 命令：

```azurecli
az resource list --tag costCenter=Finance
```

您也可以檢視透過 hello Azure 入口網站已加上標籤的資源。

hello[使用量報告](../billing/billing-understand-your-bill.md)針對您的訂閱包含標記的名稱和值，這可讓您依標記的 toobreak 出成本。 如需標記的詳細資訊，請參閱[使用標記 tooorganize 您的 Azure 資源](resource-group-using-tags.md)。

## <a name="access-control"></a>存取控制
資源管理員可讓您能夠存取您組織的 toospecific 動作 toocontrol。 原生至 hello 管理平台整合以角色為基礎的存取控制 (RBAC)，以及適用於資源群組中的存取控制 tooall 服務。 

使用角色型存取控制時，有兩個主要概念 toounderstand:

* 角色定義 - 描述一組權限，並可用於許多指派。
* 角色指派 - 為定義與特定範圍 (訂用帳戶、資源群組或資源) 的身分識別 (使用者或群組) 建立關聯。 hello 分派繼承較低範圍。

您可以加入使用者 toopre 定義的平台和資源特定角色。 例如，您可以利用 hello 稱為允許使用者 tooview 資源的讀取器的預先定義角色，但無法變更它們。 您將使用者加入您的組織需要這種類型的存取 toohello 讀取者角色中，並套用 hello 角色 toohello 訂用帳戶、 資源群組或資源。

Azure 提供下列四個平台角色的 hello:

1. 擁有者 - 可以管理所有項目，包括存取
2. 參與者 - 可以管理存取以外的所有內容
3. 讀取者 - 可以檢視所有項目，但是無法進行變更
4. 使用者存取管理員可以管理使用者存取 tooAzure 資源

Azure 也提供數個資源特有的角色。 一些常見的角色有︰

1. 虛擬機器參與者-可以管理虛擬機器，但不是授與存取 toothem，而且不能管理 hello 虛擬網路或存放裝置帳戶 toowhich 連線
2. 網路參與者-可以管理所有的網路資源，但不是授與存取 toothem
3. 儲存體帳戶參與者-可以管理儲存體帳戶，但不是授與存取 toothem
4. SQL Server 參與者 - 可以管理 SQL Server 和資料庫，但是無法管理它們的安全性相關原則
5. 網站參與者-可以管理網站，但不是 hello web 計劃 toowhich 連線

Hello 的角色和允許的動作的完整清單，請參閱[RBAC： 內建的角色](../active-directory/role-based-access-built-in-roles.md)。 如需角色型存取控制的詳細資訊，請參閱 [Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)。 

在某些情況下，您想 toorun 程式碼或指令碼，存取資源，但是不想讓 toorun 在使用者的認證。 相反地，您會想 toocreate hello 應用程式，稱為 「 服務主體的身分識別，以及指派 hello 服務主體的 hello 適當角色。 資源管理員可讓您 toocreate hello 應用程式認證，並且以程式設計方式驗證 hello 應用程式。 toolearn 有關建立服務主體，請參閱下列主題之一：

* [使用 Azure PowerShell toocreate 服務主體 tooaccess 資源](resource-group-authenticate-service-principal.md)
* [使用 Azure CLI toocreate 服務主體 tooaccess 資源](resource-group-authenticate-service-principal-cli.md)
* [使用入口網站 toocreate Azure Active Directory 應用程式和服務主體可存取資源](resource-group-create-service-principal-portal.md)

您可以同時也可以明確鎖定重要的資源 tooprevent 使用者刪除或修改它們。 如需詳細資訊，請參閱[使用 Azure Resource Manager 來鎖定資源](resource-group-lock-resources.md)。

## <a name="activity-logs"></a>活動記錄
Resource Manager 會記錄所有建立、修改或刪除資源的作業。 您可以使用 hello 活動記錄檔 toofind 錯誤進行疑難排解時或 toomonitor 您組織中的使用者如何修改資源。 toosee hello 記錄檔中，選取**活動記錄**在 hello**設定**刀鋒視窗中的資源群組。 您可以由許多不同的值包括哪些使用者起始 hello 作業篩選 hello 記錄檔。 如需有關使用 hello 活動記錄檔資訊，請參閱[檢視活動記錄 toomanage Azure 資源](resource-group-audit.md)。

## <a name="customized-policies"></a>自訂的原則
資源管理員可讓您管理您的資源 toocreate 自訂原則。 hello 您所建立的原則類型可以包含各種不同的案例。 您可以強制執行資源的的命名慣例、限制可以部署的資源類型和執行個體，或限制可以裝載某個資源類型的區域。 您可以依部門要求資源 tooorganize 帳單上的標記值。 您可以建立原則 toohelp 降低成本和維護您的訂用帳戶中的一致性。 

您需要使用 JSON 來定義原則，然後將這些原則套用到您的訂用帳戶或資源群組內。 原則是不同角色型存取控制，因為它們是套用的 tooresource 類型。

下列範例中的 hello 顯示原則，以確保指定的所有資源都包括 costCenter 標記的標記一致性。

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

您還可以建立其他類型的原則。 如需詳細資訊，請參閱[使用原則 toomanage 資源和控制存取](resource-manager-policy.md)。

## <a name="sdks"></a>SDK
Azure SDK 可供多個語言和平台使用。 這些語言實作都是透過其生態系統的套件管理員和 GitHub 提供。

以下是我們的開放原始碼 SDK 存放庫。 歡迎提供意見反應、問題並提取要求。

* [Azure SDK for .NET](https://github.com/Azure/azure-sdk-for-net)
* [適用於 Java 的 Azure 管理程式庫](https://github.com/Azure/azure-sdk-for-java)
* [Azure SDK for Node.js](https://github.com/Azure/azure-sdk-for-node)
* [Azure SDK for PHP](https://github.com/Azure/azure-sdk-for-php)
* [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python)
* [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby)

如需使用這些語言搭配您的資源的相關資訊，請參閱：

* [適用於 .NET 開發人員的 Azure](/dotnet/azure/?view=azure-dotnet)
* [適用於 Java 開發人員的 Azure](/java/azure/)
* [適用於 Node.js 開發人員的 Azure](/nodejs/azure/)
* [適用於 Python 開發人員的 Azure](/python/azure/)

> [!NOTE]
> 如果 hello SDK 並不提供所需的 hello 功能，您也可以呼叫 toohello [Azure REST API](https://docs.microsoft.com/rest/api/resources/)直接。
> 
> 

## <a name="next-steps"></a>後續步驟
* 簡單介紹 tooworking 範本，請參閱[匯出 Azure Resource Manager 範本，從現有的資源](resource-manager-export-template.md)。
* 如需更詳細的建立範本逐步解說，請參閱[建立第一個 Azure Resource Manager 範本](resource-manager-create-first-template.md)。
* toounderstand hello 函式，您可以使用在範本中，請參閱[樣板函式](resource-group-template-functions.md)
* 如需有關如何搭配使用 Visual Studio 與 Resource Manager 的相關資訊，請參閱 [透過 Visual Studio 建立和部署 Azure 資源群組](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)。

以下是此概觀的示範影片。

>[!VIDEO https://channel9.msdn.com/Blogs/Azure-Documentation-Shorts/Azure-Resource-Manager-Overview/player]


[powershellref]: https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/azurerm.resources
