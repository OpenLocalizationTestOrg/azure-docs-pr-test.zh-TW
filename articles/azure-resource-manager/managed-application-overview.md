---
title: "Azure 的 aaaOverview managed 應用程式 |Microsoft 文件"
description: "描述 hello 概念適用於 Azure 受管理應用程式"
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 2fd1844a442515f4492c890c9798073475a66f88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-overview"></a>Azure 受管理的應用程式概觀

使用 Azure 的廠商可以提供解決方案 toocustomers hello 世界各地。 Azure Marketplace 是一個資源庫，包含第一方和第三方廠商的數百個複雜、多資源範本。 客戶可以在幾分鐘內部署及啟動平台即服務 (PaaS) 和軟體即服務 (SaaS) 應用程式。 

Hello Marketplace 提供的絕佳方式，雖然客戶 tooquickly 部署的供應項目，hello 客戶負責維護和更新 hello 方案。 超出 hello 虛擬機器映像計費，供應商無法充電 hello 使用應用程式的客戶。 此外，廠商無法防止客戶修改重要的應用程式資源。 供應商也無法封鎖存取 toointellectual 屬性構成應用程式。 Azure 受管理的應用程式針對這些問題提供了一些解決方案。 

受管理的應用程式是以類似 tooa 方案範本中 hello Marketplace，但有一個主要差異。 在受管理的應用程式，hello 資源是受 hello 廠商 tooa 佈建的資源群組。 hello 資源群組存在於 hello 客戶的訂閱，但 hello 廠商的租用戶中的身分識別存取 toohello 資源群組。

## <a name="advantages-of-managed-applications"></a>受管理應用程式的優點

管理服務提供者 (MSPs)、 Isv 和中央公司的 IT 團隊可以使用受管理的應用程式 toodeliver 解決方案透過 hello Marketplace 或 hello 服務類別目錄。 雖然客戶部署這些受管理的應用程式，其訂用帳戶中，不會擁有 toomaintain、 更新或這些服務。 廠商管理和支援 hello 應用程式，因為客戶不需要 toodevelop 特定應用程式定義域知識 toomanage 這些應用程式。 客戶可以自動取得應用程式更新沒有 hello 需要 tooworry 有關疑難排解及診斷 hello 應用程式的問題。

廠商及提供者，managed 應用程式會建立通道 toosell 基礎結構和透過 hello Marketplace 的軟體。 受管理的應用程式也提供方式 tooattach 服務和作業支援 tooAzure 客戶。 供應商可以結帳客戶使用 hello Azure 計費系統。 他們可以使用已部署應用程式的範本 toomanage hello 生命週期。 這些解決方案是獨立且密封 toohello 客戶，因此廠商可以提供高品質的服務。 這種方式有益於 PaaS 和 SaaS 供應商。 它也可協助公司中央平台小組和系統整合業者 (Si) 的人員想 toopackage 和轉售及其解決方案。

## <a name="managed-application-types"></a>受管理的應用程式類型
Azure 受管理的應用程式以兩種類型提供 - Service Catalog 和 Marketplace。
 
### <a name="service-catalog"></a>Service Catalog  

以 hello 服務類別目錄，客戶可以建立其組織中的人員所使用的 Azure toobe 核准解決方案的目錄。 維護這類解決方案的目錄對於企業的中央 IT 小組很有幫助。 雖然他們為自己組織提供解決方案，他們可以使用與某些組織的標準 hello 目錄 tooensure 相容。 他們可以控制、更新和維護這些應用程式。 員工可以使用 hello 目錄 tooeasily 探索 hello 豐富的建議並由其 IT 部門核准的應用程式。 客戶會看到他們所建立的 hello 受管理的服務類別目錄應用程式。 它們也可以看到 hello managed 應用程式的其他人在與其其組織共用。
 
如需發佈 Service Catalog 受管理應用程式的資訊，請參閱[建立和發佈 Service Catalog 受管理的應用程式](managed-application-publishing.md)。
 
如需使用 Service Catalog 受管理應用程式的詳細資訊，請參閱[使用 Service Catalog 受管理的應用程式](managed-application-consumption.md)。
 
### <a name="marketplace"></a>Marketplace

受管理的應用程式皆可透過 hello Marketplace hello Azure 入口網站中。 Hello 廠商發行這些應用程式之後，它們可供所有人的內部或外部組織 tooconsume。 使用這個方法，MSPs、 Isv 和 SIs 可以提供其解決方案 tooall Azure 客戶。 客戶會取得使用這些複雜的方案沒有 hello 需要 tooinvest 理解和維護 hello 方案中的 hello 優點。 

目前，發行者可以讓其供應項目提供為受管理的應用程式，或是不受管理的解決方案範本。 hello 發佈受管理的應用程式的主要元件包括 hello 範本檔和 hello UI 定義檔。 hello 範本檔案會描述 hello 資源佈建。 hello UI 定義檔案會描述如何 hello 需輸入佈建這些資源會顯示在 hello 入口網站。 hello 必要檔案封裝在.zip 檔案並透過 hello 發佈入口網站上傳。
 
如需發佈受管理的應用程式 toohello Marketplace 資訊，請參閱[Azure 受管理應用程式在 hello Marketplace](managed-application-author-marketplace.md)。

使用來自 hello Marketplace 的受管理應用程式的相關資訊，請參閱[取用 Azure managed hello Marketplace 中的應用程式](managed-application-consume-marketplace.md)。

## <a name="key-concepts"></a>重要概念

### <a name="managed-resource-group"></a>受管理的資源群組
hello 受管理的資源群組是所有 hello Azure，您可以建立 hello 範本中佈建的資源。 例如，如果 hello 應用裝置是使用的 toocreate 儲存體帳戶，此資源群組包含 hello 儲存體帳戶資源。 它並未包含 hello 應用裝置資源。

### <a name="appliance-package"></a>設備套件
hello 發行者建立 hello 樣板檔案和 hello createUIDefinition 檔案所包含的封裝。 具體來說，它包含下列檔案的 hello:

- **applianceMainTemplate.json**： 這個範本檔案會定義所有 hello 應用裝置佈建的 hello 資源。 這個檔案是已使用 toocreate 資源的一般範本檔案。

- **MainTemplate.json**： 這個範本檔案定義 hello 應用裝置資源 (Microsoft.Solutions/appliances)。 此資源中定義的其中一個重要屬性是 ManagedResourceGroupId。 這個屬性會指出哪一個資源群組是使用的 toohost hello 實際資源 applianceMainTemplate.json 中所定義。

- **applianceCreateUIDefinition.json**： 此檔案描述 hello hello 範本中定義的 hello 參數所需的 UI 呈現方式。

### <a name="authorization"></a>Authorization
hello 發行者必須指定 hello 代表 hello 客戶 hello 廠商 toomanage hello 資源所需的權限。 此權限適用於 toohello 受管理的資源群組。 設定下列值的 hello:

- **PrincipalID**: hello 的 hello 使用者、 群組或已使用 toogrant 存取 toohello 受管理的資源群組的應用程式的 Azure Active Directory (Azure AD) 識別項。 這個識別碼所屬 toohello 發行者的租用戶。

- **RoleDefinitionID**: hello Azure AD 的識別項的 hello 指派角色 toohello 前面主體識別碼。 它可以是任何 hello 內建角色型存取控制角色 hello 發行者的租用戶中。 如需詳細資訊，請參閱 [Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md)。

## <a name="next-steps"></a>後續步驟

* 發佈受管理的應用程式 toohello Marketplace 的相關資訊，請參閱[Azure 受管理應用程式在 hello Marketplace](managed-application-author-marketplace.md)。
* 使用來自 hello Marketplace 的受管理應用程式的相關資訊，請參閱[取用 Azure managed hello Marketplace 中的應用程式](managed-application-consume-marketplace.md)。
* 如需發佈 Service Catalog 受管理應用程式的資訊，請參閱[建立和發佈 Service Catalog 受管理的應用程式](managed-application-publishing.md)。
* 如需使用 Service Catalog 受管理應用程式的詳細資訊，請參閱[使用 Service Catalog 受管理的應用程式](managed-application-consumption.md)。
* toocreate UI 定義檔案，請參閱[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。
