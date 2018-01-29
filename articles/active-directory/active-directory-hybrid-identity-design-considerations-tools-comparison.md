---
title: "混合式身分識別：目錄整合工具比較 | Microsoft Docs"
description: "本頁面提供完整資料表，供您比較各種可用於目錄整合的目錄整合工具。"
services: active-directory
documentationcenter: 
author: billmath
manager: mtillman
ms.assetid: 1e62a4bd-4d55-4609-895e-70131dedbf52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/09/2018
ms.author: billmath
ms.openlocfilehash: 78ca910b4dfd5a706d2f1df7f70291fb48f096f5
ms.sourcegitcommit: 71fa59e97b01b65f25bcae318d834358fea5224a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/11/2018
---
# <a name="hybrid-identity-directory-integration-tools-comparison"></a>混合式身分識別目錄整合工具比較
目錄整合工具已經經過多年的成長和發展。  本文件是為了整合檢視這些工具，並比較各個工具中所提供的功能。

<!-- The hardcoded link is a workaround for campaign ids not working in acom links-->

> [!NOTE]
> Azure AD Connect 包含先前發行為 Dirsync 和 AAD Sync 的元件和功能。這些工具已不會再個別發行，而且所有未來的增強功能都會包含在 Azure AD Connect 的更新中，因此，您一定會知道可以到哪裡取得最新的功能。
> 
> DirSync 和 Azure AD Sync 已被取代。 如需詳細資訊，請參閱 [這裡](active-directory-aadconnect-dirsync-deprecated.md)。
> 
> 

為每個資料表使用下列機碼。

●  = 目前已可供使用  
FR = 未來的版本  
PP = 公開預覽  

## <a name="on-premises-to-cloud-synchronization"></a>內部部署至雲端同步處理
| 功能 | Azure Active Directory Connect | Azure Active Directory 同步處理服務 (AAD Sync) | Azure Active Directory 同步處理工具 (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| 連接到單一內部部署 AD 樹系 |● |● |● |● |● |
| 連接到多個內部部署 AD 樹系 |● |● | |● |● |
| 連接到多個內部部署 Exchange 組織 |● | | | | |
| 連接到單一內部部署 LDAP 目錄 |●* | | |● |● |
| 連接到多個內部部署 LDAP 目錄 |●*  | | |● |● |
| 連接到內部部署 AD 和內部部署 LDAP 目錄 |●* | | |● |● |
| 連接到自訂系統 (亦即 SQL、Oracle、MySQL 等) |FR | | |● |● |
| 同步處理客戶定義的屬性 (目錄擴充功能) |● | | | | |
| 連接到內部部署人力資源系統 (例如 SAP、Oracle eBusiness、PeopleSoft) |FR | | |● |● |
| 支援 FIM 同步處理規則和連接器，以供佈建到內部部署系統。 | | | |● |● |
&#42; 目前這有兩個支援的選項。  如下：
   1. 您可以使用泛型 LDAP 連接器，並在 Azure AD Connect 之外啟用。  這很複雜，且需要夥伴才能上架，以及頂級支援合約來維護。  此選項可以處理單一和多個 LDAP 目錄。
   2. 您可以開發自己的解決方案，將物件從 LDAP 移至 Active Directory。  然後使用 Azure AD Connect 將物件同步。  MIM 或 FIM 可用來作為移動物件的可能解決方案。

## <a name="cloud-to-on-premises-synchronization"></a>雲端至內部部署同步處理
| 功能 | Azure Active Directory Connect | Azure Active Directory 同步處理服務 | Azure Active Directory 同步處理工具 (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| 裝置的回寫 |● | |● | | |
| 屬性回寫 (用於 Exchange 混合部署) |● |● |● |● |● |
| 群組物件的回寫 |● | | | | |
| 密碼的回寫 (從自助式密碼重設 (SSPR) 和密碼變更) |● |● | | | |

## <a name="authentication-feature-support"></a>驗證功能支援
| 功能 | Azure Active Directory Connect | Azure Active Directory 同步處理服務 | Azure Active Directory 同步處理工具 (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| 單一內部部署 AD 樹系的密碼同步處理 |● |● |● | | |
| 多個內部部署 AD 樹系的密碼同步處理 |● |● | | | |
| 使用同盟進行單一登入 |● |● |● |● |● |
| 密碼的回寫 (從 SSPR 和密碼變更) |● |● | | | |

## <a name="set-up-and-installation"></a>設定與安裝
| 功能 | Azure Active Directory Connect | Azure Active Directory 同步處理服務 | Azure Active Directory 同步處理工具 (DirSync) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|
| 支援在網域控制站上安裝 |● |● |● | |
| 支援使用 SQL Express 安裝 |● |● |● | |
| 從 DirSync 輕鬆升級 |● | | | |
| 系統管理員 UX 至 Windows Server 語言的當地語系化 |● |● |● | |
| 一般使用者 UX 至 Windows Server 語言的當地語系化 | | | |● |
| Windows Server 2008 和 Windows Server 2008 R2 的支援 |● 用於同步，不用於同盟 |● |● |● |
| Windows Server 2012 和 Windows Server 2012 R2 的支援 |● |● |● |● |

## <a name="filtering-and-configuration"></a>篩選和組態
| 功能 | Azure Active Directory Connect | Azure Active Directory 同步處理服務 | Azure Active Directory 同步處理工具 (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| 針對網域及組織單位篩選 |● |● |● |● |● |
| 針對物件的屬性值篩選 |● |● |● |● |● |
| 允許同步處理一組最基本的屬性 (MinSync) |● |● | | | |
| 允許針對屬性流程套用不同的服務範本 |● |● | | | |
| 允許移除從 AD 流向 Azure AD 的屬性 |● |● | | | |
| 允許屬性流程的進階自訂 |● |● | |● |● |

## <a name="next-steps"></a>後續步驟
深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。

