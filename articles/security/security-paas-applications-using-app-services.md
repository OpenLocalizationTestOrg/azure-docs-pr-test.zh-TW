---
title: "使用 Azure App Service 來保護 PaaS Web 與行動應用程式 | Microsoft Docs"
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
ms.date: 11/21/2017
ms.author: terrylan
ms.openlocfilehash: dec45d91ad1a73306b3e2656dd9bf7fdbe456720
ms.sourcegitcommit: 62eaa376437687de4ef2e325ac3d7e195d158f9f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-app-service"></a>使用 Azure App Service 來保護 PaaS Web 與行動應用程式

在本文中，我們將討論用來保護 PaaS Web 與行動應用程式的 [Azure App Service](https://azure.microsoft.com/services/app-service/) 安全性最佳做法。 這些最佳做法衍生自我們的 Azure 經驗和客戶 (例如您自己) 的經驗。

## <a name="azure-app-service"></a>Azure App Service
[Azure App Service](../app-service/app-service-web-overview.md) 是一個 PaaS 供應項目，可讓您為任何平台或裝置建立 Web 與行動應用程式，以及連線到雲端或內部部署環境中任何位置的資料。 App Service 包含先前以 Azure 網站和 Azure 行動服務形式個別提供的 Web 和行動功能。 此外，它也包含可用來自動執行商務程序及裝載雲端 API 的新功能。 App Service 會以單一整合式服務形式，為 Web、行動及整合案例提供一組豐富的功能。

## <a name="best-practices"></a>最佳作法

使用 App Service 時，請遵循下列最佳做法：

- [透過 Azure Active Directory (AD) 進行驗證](../app-service/app-service-authentication-overview.md)。 App Service 可為您的識別提供者提供 OAuth 2.0 服務。 OAuth 2.0 既將焦點放在為用戶端開發人員提供簡易性，同時又為 Web 應用程式、傳統型應用程式及行動電話提供特定授權流程。 Azure AD 使用 OAuth 2.0 來讓您能夠授與對行動與 Web 應用程式的存取權。
- 根據必要知悉和最低權限安全性原則來限制存取。 對於想要強制執行資料存取安全性原則的組織來說，限制存取是必須做的事。 「角色型存取控制」(RBAC) 可用來將權限指派給特定範圍的使用者、群組及應用程式。 若要深入了解授與使用者的應用程式存取權，請參閱[開始使用存取管理](../active-directory/role-based-access-control-what-is.md)。
- 保護您的金鑰。 如果您遺失訂用帳戶金鑰，則安全性措施做得再好也沒有用。 Azure 金鑰保存庫可協助保護雲端應用程式和服務所使用的密碼編譯金鑰和密碼。 使用金鑰保存庫之後，您可以加密金鑰和密碼 (例如驗證金鑰、儲存體帳戶金鑰、資料加密金鑰、.PFX 檔案和密碼)，方法是使用受硬體安全模組 (HSM) 保護的金鑰。 為了加強保證，您可以在 HSM 中匯入或產生金鑰。 若要深入了解，請參閱 [Azure Key Vault](../key-vault/key-vault-whatis.md)。 您可以使用 Key Vault 藉由自動更新管理 TLS 憑證。
- 限制連入來源 IP 位址。 [App Service 環境](../app-service/environment/intro.md)具有虛擬網路整合功能，可協助您透過網路安全性群組 (NSG) 限制連入來源 IP 位址。 如果您不熟悉「Azure 虛擬網路」(VNET)，這是一種功能，可讓您將許多 Azure 資源放在由您控制存取的非網際網路、可路由網路中。 若要深入了解，請參閱[將您的應用程式與 Azure 虛擬網路整合](../app-service/web-sites-integrate-with-vnet.md)。

## <a name="next-steps"></a>後續步驟
本文介紹了用來保護 PaaS Web 與行動應用程式的一組 App Service 安全性最佳做法。 若要深入了解如何保護您的 PaaS 部署，請參閱︰

- [保護 PaaS 部署](security-paas-deployments.md)
- [使用 Azure SQL Database 和 SQL 資料倉儲來保護 PaaS Web 與行動應用程式](security-paas-applications-using-sql.md)
