---
title: "aaaSecuring PaaS web 和行動應用程式使用 Azure 應用程式服務 |Microsoft 文件"
description: " 了解用來保護 PaaS Web 與行動應用程式的 Azure App Service 安全性最佳做法。 "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: terrylan
ms.openlocfilehash: 68a741c668efe2157cff114b649e0e287ef196f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-app-services"></a>使用 Azure App Service 來保護 PaaS Web 與行動應用程式

在本文中，我們將說明用來保護 PaaS Web 與行動應用程式的 [Azure App Service](https://azure.microsoft.com/services/app-service/) 安全性最佳做法。 這些最佳作法從我們的經驗與 Azure 和 hello 經驗的客戶想自己。

## <a name="azure-app-services"></a>Azure App Service
[Azure 應用程式服務](../app-service/app-service-value-prop-what-is.md)是可讓您建立 web 和行動應用程式的任何平台或裝置，以及連接 hello 雲端或內部部署中的任何地方、 toodata PaaS 供應項目。 應用程式服務包含 hello web 和行動先前遞送分別做為 Azure 網站和 Azure 行動服務的功能。 此外，它也包含可用來自動執行商務程序及裝載雲端 API 的新功能。 為單一整合式服務時，應用程式服務會將一組豐富的功能 tooweb、 行動裝置版和整合案例。

toolearn 詳細資訊，請參閱概觀上[行動應用程式](../app-service-mobile/app-service-mobile-value-prop.md)和[Web 應用程式](../app-service-web/app-service-web-overview.md)。

## <a name="best-practices"></a>最佳作法

使用 App Service 時，請依照下列最佳做法操作：

- [透過 Azure Active Directory (AD) 進行驗證](../app-service-web/web-sites-authentication-authorization.md#authenticate-through-azure-active-directory)。 App Service 可為您的身分識別提供者提供 OAuth 2.0 服務。 OAuth 2.0 既將焦點放在為用戶端開發人員提供簡易性，同時又為 Web 應用程式、傳統型應用程式及行動電話提供特定授權流程。 Azure AD 使用 OAuth 2.0 tooenable 您 tooauthorize 存取 toomobile 及 web 應用程式。
- 限制存取權限 hello 需要 tooknow 和最小權限的安全性原則。 限制存取為命令式 tooenforce 安全性原則所需的資料存取的組織。 角色型存取控制 (RBAC) 可以使用的 tooassign 權限 toousers、 群組和應用程式在特定範圍內。 toolearn 進一步了解授與使用者存取 tooapplications，請參閱[開始存取管理](../active-directory/role-based-access-control-what-is.md)。
- 保護您的金鑰。 如果您遺失訂用帳戶金鑰，則安全性措施做得再好也沒有用。 Azure 金鑰保存庫可協助保護雲端應用程式和服務所使用的密碼編譯金鑰和密碼。 使用金鑰保存庫之後，您可以加密金鑰和密碼 (例如驗證金鑰、儲存體帳戶金鑰、資料加密金鑰、.PFX 檔案和密碼)，方法是使用受硬體安全模組 (HSM) 保護的金鑰。 為了加強保證，您可以在 HSM 中匯入或產生金鑰。 請參閱[Azure 金鑰保存庫](../key-vault/key-vault-whatis.md)toolearn 更多。 您也可以使用金鑰保存庫 toomanage TLS 憑證自動更新。
- 限制連入來源 IP 位址。 [應用程式服務環境](../app-service-web/app-service-app-service-environment-intro.md)具有虛擬網路整合功能，可協助您透過網路安全性群組 (NSG) 限制連入來源 IP 位址。 如果您不熟悉 Azure 虛擬網路 (Vnet)，這是一種功能，可讓您 tooplace 許多非網際網路可路由網路中，您可以控制您的 Azure 資源存取權。 詳細資訊，請參閱 toolearn[整合您的應用程式與 Azure 虛擬網路](../app-service-web/web-sites-integrate-with-vnet.md)。

## <a name="next-steps"></a>後續步驟
這篇文章會引進 tooa 集合的應用程式服務的安全性最佳作法來保護您的 PaaS web 與行動應用程式。 toolearn 深入了解保護您的 PaaS 部署，請參閱：

- [保護 PaaS 部署](security-paas-deployments.md)
- [使用 Azure SQL Database 和 SQL 資料倉儲來保護 PaaS Web 與行動應用程式](security-paas-applications-using-sql.md)
