---
title: "aaaAzure AD 連線和同盟 |Microsoft 文件"
description: "此頁面是 hello 中央位置，如需有關使用 Azure AD Connect 的 AD FS 作業的所有文件。"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: f9107cf5-0131-499a-9edf-616bf3afef4d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: anandy
ms.openlocfilehash: dc70206eee2296c2320712ef2ade48ccebcc912d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-and-federation"></a>Azure AD Connect 和同盟
Azure Active Directory (Azure AD) Connect 可讓您使用內部部署 Active Directory 同盟服務 (AD FS) 與 Azure AD 來設定同盟。 同盟登入，您可以啟用使用者 toosign tooAzure AD 為基礎的服務在內部部署密碼-，而在 hello 公司網路上而不需要 tooenter 密碼一次。 藉由使用 AD FS 中的 hello 同盟選項，您可以部署新安裝的 AD FS，或您可以在 Windows Server 2012 R2 的伺服器陣列中指定現有的安裝。

本主題為 hello 家用與同盟相關功能的 Azure AD Connect 的資訊。 它會列出連結 tooall 相關主題。 連結 tooAzure AD Connect，請參閱[整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。

## <a name="azure-ad-connect-federation-topics"></a>Azure AD Connect：同盟主題
| 主題 | 它涵蓋了與時機 tooread 它 |
|:--- |:--- |
| **Azure AD Connect 使用者登入選項** | |
| [了解使用者登入選項](active-directory-aadconnect-user-signin.md) |深入了解各種使用者登入選項，以及它們如何影響 hello Azure 登入的使用者經驗。 |
| **使用 Azure AD Connect 安裝 AD FS** | |
| [必要條件](active-directory-aadconnect-get-started-custom.md#ad-fs-configuration-pre-requisites) |請參閱 AD FS 安裝 Azure AD Connect 透過成功的 hello 必要條件。 |
| [設定 AD FS 伺服器陣列](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs) |使用 Azure AD Connect 安裝新的 AD FS 伺服器陣列。 |
| [使用替代登入識別碼與 Azure AD 建立同盟關係](active-directory-aadconnect-federation-management.md#alternateid) | 使用替代登入識別碼設定同盟  |
| **修改 hello AD FS 設定** | |
| [修復 hello 信任](active-directory-aadconnect-federation-management.md#repairthetrust) |修復 hello 目前信任之間內部部署 AD FS 和 Office 365/Azure。 |
| [新增 AD FS 伺服器](active-directory-aadconnect-federation-management.md#addadfsserver) |在初始安裝之後，增加 AD FS 伺服器來擴充 AD FS 伺服器陣列。 |
| [新增 AD FS WAP 伺服器](active-directory-aadconnect-federation-management.md#addwapserver) |在初始安裝之後，增加 Web 應用程式 Proxy (WAP) 伺服器來擴充 AD FS 伺服器陣列。 |
| [新增新的同盟網域](active-directory-aadconnect-federation-management.md#addfeddomain) |加入另一個網域 toobe 與 Azure AD 建立同盟。 |
| [Hello SSL 憑證更新](active-directory-aadconnectfed-ssl-update.md)| 更新 AD FS 伺服器陣列的 hello SSL 憑證。 |
| **其他同盟組態** | |
| [將多個 Azure AD 執行個體與單一 AD FS 執行個體同盟](active-directory-aadconnectfed-single-adfs-multitenant-federation.md) | 將多個 Azure AD 和單一 AD FS 伺服器陣列建立同盟關係| 
| [新增自訂公司標誌/圖例](active-directory-aadconnect-federation-management.md#customlogo) |藉由指定 hello hello AD FS 登入頁面顯示的自訂標誌，請修改 hello 登入體驗。 |
| [新增登入說明](active-directory-aadconnect-federation-management.md#addsignindescription) |變更 hello 登入描述 hello AD FS 登入頁面上。 |
| [修改 AD FS 宣告規則](active-directory-aadconnect-federation-management.md#modclaims) |修改或新增對應 tooAzure AD Connect 同步處理設定的 AD FS 中的宣告規則。 |


## <a name="additional-resources"></a>其他資源
* [將兩個 Azure AD 和單一 AD FS 建立同盟關係](active-directory-aadconnectfed-single-adfs-multitenant-federation.md)
* [Azure 中的 AD FS 部署](active-directory-aadconnect-azure-adfs.md)
* [使用 Azure 流量管理員在 Azure 中部署高可用性跨地區 AD FS](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)
