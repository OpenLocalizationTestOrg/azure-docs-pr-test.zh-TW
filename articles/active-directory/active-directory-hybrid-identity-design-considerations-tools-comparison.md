---
title: "混合式身分識別：目錄整合工具比較 | Microsoft Docs"
description: "這是頁面會提供完整的資料表，比較 hello 各種可用的目錄整合的目錄整合工具。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 1e62a4bd-4d55-4609-895e-70131dedbf52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 18ac0a0f58726eceb85510df516e8db71429b313
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-identity-directory-integration-tools-comparison"></a>混合式身分識別目錄整合工具比較
Hello 多年 hello 目錄整合工具有成長，而且，進而發展。  這份文件是 toohelp 提供合併的檢視，這些工具和中每個可用的 hello 功能的比較。

<!-- hello hardcoded link is a workaround for campaign ids not working in acom links-->

> [!NOTE]
> Azure AD Connect 會併入 hello 元件和先前發行為 Dirsync 和 AAD Sync 的功能。這些工具不會再個別發行和所有未來的改良功能將會包含在更新 tooAzure AD 連接，好讓您一定會知道其中 tooget hello 最新的功能。
> 
> DirSync 和 Azure AD Sync 已被取代。 如需詳細資訊，請參閱 [這裡](active-directory-aadconnect-dirsync-deprecated.md)。
> 
> 

使用下列 hello 資料表的每個索引鍵的 hello。

●  = 目前已可供使用  
FR = 未來的版本  
PP = 公開預覽  

## <a name="on-premises-toocloud-synchronization"></a>在內部部署 tooCloud 同步處理
| 功能 | Azure Active Directory Connect | Azure Active Directory 同步處理服務 (AAD Sync) | Azure Active Directory 同步處理工具 (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| 連接 toosingle 在內部部署 AD 樹系 |● |● |● |● |● |
| 連接 toomultiple 內部部署 AD 樹系 |● |● | |● |● |
| 連接 toomultiple 內部部署 Exchange 入 |● | | | | |
| 連接 toosingle 在內部部署 LDAP 目錄 |FR | | |● |● |
| 連接 toomultiple 在內部部署 LDAP 目錄 |FR | | |● |● |
| 連接 tooon 內部部署 AD 和內部部署 LDAP 目錄 |FR | | |● |● |
| 連接 toocustom 系統 （也就是 SQL、 Oracle、 MySQL 等） |FR | | |● |● |
| 同步處理客戶定義的屬性 (目錄擴充功能) |● | | | | |
| 連線內部部署 tooon HR (亦即，SAP、 Oracle eBusiness，PeopleSoft) |FR | | |● |● |
| 支援 FIM 同步處理規則和連接器的佈建 tooon 內部部署系統。 | | | |● |● |

## <a name="cloud-tooon-premises-synchronization"></a>雲端 tooOn 內部部署同步處理
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
| 系統管理員 UX tooWindows 伺服器語言的當地語系化 |● |● |● | |
| 終端使用者 UX tooWindows 伺服器語言的當地語系化 | | | |● |
| Windows Server 2008 和 Windows Server 2008 R2 的支援 |● 用於同步，不用於同盟 |● |● |● |
| Windows Server 2012 和 Windows Server 2012 R2 的支援 |● |● |● |● |

## <a name="filtering-and-configuration"></a>篩選和組態
| 功能 | Azure Active Directory Connect | Azure Active Directory 同步處理服務 | Azure Active Directory 同步處理工具 (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| 針對網域及組織單位篩選 |● |● |● |● |● |
| 針對物件的屬性值篩選 |● |● |● |● |● |
| 允許的最小集合屬性 toobe 同步處理 (MinSync) |● |● | | | |
| 允許屬性流程套用不同的服務範本 toobe |● |● | | | |
| 允許從 AD tooAzure AD 流程中移除屬性 |● |● | | | |
| 允許屬性流程的進階自訂 |● |● | |● |● |

## <a name="next-steps"></a>後續步驟
深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。

