---
title: "Azure Analysis Services 在 aaaAuthentication 和使用者權限 |Microsoft 文件"
description: "了解 Azure Analysis Services 中的驗證和使用者權限。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: dd49fd59eec1f68dfe8a0fe373fa612ac46de4e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-user-permissions"></a>驗證和使用者權限
Azure Analysis Services 會使用 Azure Active Directory (Azure AD) 進行身分識別管理和使用者驗證。 建立任何使用者，管理，或連接 tooan Azure Analysis Services 伺服器在必須具備有效的使用者識別[Azure AD 租用戶](../active-directory/active-directory-administer.md)hello 中相同的訂用帳戶。

Azure Analysis Services 支援 [Azure AD B2B 共同作業](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md)。 透過 B2B，組織外部的使用者可以受邀成為 Azure AD 目錄中的來賓使用者。 來賓可以來自另一個 Azure AD 租用戶目錄或任何有效的電子郵件地址。 一次受邀和 hello 使用者接受 hello 邀請透過電子郵件傳送從 Azure hello 使用者識別加入 toohello 租用戶目錄。 這些身分識別可以再加入 toosecurity 群組或伺服器管理員或資料庫角色的成員。

![Azure Analysis Services 驗證架構](./media/analysis-services-manage-users/aas-manage-users-arch.png)

## <a name="authentication"></a>驗證
所有用戶端應用程式和工具會使用一或多個 Analysis Services hello[用戶端程式庫](analysis-services-data-providers.md)(MSOLAP，AMO ADOMD) tooconnect tooa 伺服器。 

這三個用戶端程式庫全都支援 Azure AD 互動式流程和非互動式驗證方法。 hello 兩個非互動的方法、 Active Directory 密碼和 Active Directory 整合式驗證方法可以用於應用程式利用 AMOMD 和 MSOLAP。 這兩種方法絕對不會產生快顯對話方塊。

用戶端應用程式，如 Excel 和 Power BI Desktop，並 SSMS 和 SSDT 等工具安裝 hello 最新版本更新時的 hello 程式庫 toohello 最新版本。 Power BI Desktop、SSMS 和 SSDT 會每月更新。 Excel 會[與 Office 365 一起更新](https://support.office.com/en-us/article/When-do-I-get-the-newest-features-in-Office-2016-for-Office-365-da36192c-58b9-4bc9-8d51-bb6eed468516)。 Office 365 更新較不頻繁，而且某些組織會使用 hello 延後的通道，向上 toothree 幾個月才會延期意義更新。

 根據 hello 用戶端應用程式或您使用的工具，驗證與登入方式 hello 類型可能會不同。 每個應用程式可能支援不同功能 toocloud 服務，例如 Azure Analysis Services 連線。


### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Azure Analysis Services 伺服器使用 Windows 驗證、Active Directory 密碼驗證和 Active Directory 通用驗證，支援來自 [SSMS V17.1](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 和更高版本的連線。 一般而言，建議您使用 Active Directory 通用驗證，因為：

*  支援互動式和非互動式驗證方法。

*  支援 Azure B2B 來賓使用者受邀 hello Azure AS 租用戶。 當 tooa 伺服器連線，來賓使用者必須在連接 toohello 伺服器時選取 Active Directory 通用驗證。

*  支援 Multi-Factor Authentication (MFA)。 Azure MFA 有助於保護存取 toodata 和應用程式利用某個範圍的驗證選項： 通話、 簡訊、 智慧卡 pin，或行動裝置應用程式通知。 搭配 Azure AD 使用互動式 MFA 時，會出現快顯對話方塊以進行驗證。

### <a name="sql-server-data-tools-ssdt"></a>SQL Server 資料工具 (SSDT)
SSDT 會使用 MFA 支援的 Active Directory 通用驗證連接 tooAzure Analysis Services。 使用者都提示的 toosign tooAzure hello 第一個部署中使用其組織識別碼 （電子郵件）。 使用者必須登入 tooAzure 與要部署的 hello 伺服器上伺服器系統管理員權限的帳戶。 當登入 tooAzure hello 第一次，則會指派語彙基元。 SSDT 會快取 hello 語彙基元記憶體中的未來重新。

### <a name="power-bi-desktop"></a>Power BI Desktop
Power BI Desktop 會連接 tooAzure Analysis Services 使用 MFA 支援的 Active Directory 通用驗證。 使用者都提示的 toosign 中 tooAzure hello 第一個連接上使用其組織識別碼 （電子郵件）。 使用者必須登入 tooAzure 隨附於伺服器管理員或資料庫角色的帳戶。

### <a name="excel"></a>Excel
Excel 使用者可以連線 tooa 伺服器使用 Windows 帳戶、 組織識別碼 （電子郵件地址） 或外部的電子郵件地址。 外部電子郵件識別身分必須存在於 hello Azure AD 的來賓使用者身分。

## <a name="user-permissions"></a>使用者權限

**伺服器管理員**特定 tooan Azure Analysis Services 伺服器執行個體。 以連線工具像是 Azure 入口網站中，SSMS 和 SSDT tooperform 工作，例如將資料庫新增和管理使用者角色。 根據預設，建立 hello 伺服器 hello 使用者會自動加入做為 Analysis Services 伺服器管理員。 使用 Azure 入口網站或 SSMS，可以新增其他系統管理員。 伺服器系統管理員必須有在 hello hello Azure AD 租用戶的帳戶相同的訂用帳戶。 詳細資訊，請參閱 toolearn[管理伺服器的系統管理員](analysis-services-server-admins.md)。 


**資料庫使用者**toomodel 資料庫連接使用用戶端應用程式，例如 Excel 或 Power BI。 使用者必須加入 toodatabase 角色。 資料庫角色會定義資料庫的系統管理員、處理或讀取權限。 這是很重要 toounderstand 資料庫使用者，系統管理員權限的角色在不同於伺服器系統管理員。 不過，根據預設，伺服器管理員也是資料庫管理員。 詳細資訊，請參閱 toolearn[管理資料庫角色和使用者](analysis-services-database-users.md)。

**Azure 資源擁有者**。 資源擁有者可管理 Azure 訂用帳戶的資源。 資源擁有者可以將 Azure AD 使用者的身分識別 tooOwner 或參與者角色訂用帳戶內使用**存取控制**在 Azure 入口網站，或使用 Azure Resource Manager 範本。 

![Azure 入口網站中的存取控制](./media/analysis-services-manage-users/aas-manage-users-rbac.png)

在此層級的角色套用 toousers 或需要在 hello 入口網站或使用 Azure 資源管理員範本可完成 tooperform 工作的帳戶。 詳細資訊，請參閱 toolearn[角色型存取控制](../active-directory/role-based-access-control-what-is.md)。 


## <a name="database-roles"></a>資料庫角色

 針對表格式模型定義的角色為資料庫角色。 也就是 hello 角色的成員組成的 Azure AD 使用者和安全性群組，那些成員已經定義 hello 動作的特定權限可在模型資料庫上。 資料庫角色會建立 hello 資料庫中的個別物件，而且適用於建立該角色的唯一 toohello 資料庫。   
  
 根據預設，當您建立新的表格式模型專案，hello 模型專案沒有任何角色。 角色可以使用 hello 在 SSDT 中的 [角色管理員] 對話方塊來定義。 在模型專案的設計期間定義角色，會套用只有 toohello 模型工作空間資料庫。 部署 hello 模型時，hello 相同角色是套用的 toohello 部署模型。 部署模型之後，伺服器和資料庫管理員可以使用 SSMS 來管理角色和成員。 詳細資訊，請參閱 toolearn[管理資料庫角色和使用者](analysis-services-database-users.md)。
  


## <a name="next-steps"></a>後續步驟

[使用 Azure Active Directory 群組管理存取 tooresources](../active-directory/active-directory-manage-groups.md)   
[管理資料庫角色和使用者](analysis-services-database-users.md)  
[管理伺服器管理員](analysis-services-server-admins.md)  
[角色型存取控制](../active-directory/role-based-access-control-what-is.md)  