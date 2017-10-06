---
title: "Azure AD Connect 同步：了解及自訂同步處理 | Microsoft Docs"
description: "說明如何在 Azure AD Connect 同步的運作方式以及如何 toocustomize。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ee4bf802-045b-4da0-986e-90aba2de58d6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2016
ms.author: markvi
ms.openlocfilehash: 97e4bd9904b077f2628e5f8dcbaa6f1a76168a12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understand-and-customize-synchronization"></a>Azure AD Connect 同步處理：了解及自訂同步處理
hello Azure Active Directory Connect 同步處理服務 (Azure AD Connect sync) 是 Azure AD Connect 的主要元件。 它會負責所有 hello 作業都在內部部署環境與 Azure AD 之間的相關的 toosynchronize 識別資料。 Azure AD Connect 同步是目錄同步、 Azure AD Sync，和 Forefront Identity Manager 以 hello Azure Active Directory 連接器設定的 hello 後續版本。

本主題為 hello 的家用**Azure AD Connect 同步處理**(也稱為**同步處理引擎**)，並列出連結 tooall 其他主題相關的 tooit。 連結 tooAzure AD Connect，請參閱[整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。

hello 同步服務包含兩個元件，hello 內部**Azure AD Connect 同步處理**在 Azure AD 中的元件和 hello 服務端呼叫**Azure AD Connect 同步處理服務**。 hello 服務是很常見的 DirSync、 Azure AD Sync，與 Azure AD Connect。

## <a name="azure-ad-connect-sync-topics"></a>Azure AD Connect 同步處理主題
| 主題 | 它涵蓋了與時機 tooread |
| --- | --- |
| **Azure AD Connect 同步處理基本概念** | |
| [了解 hello 架構](active-directory-aadconnectsync-understanding-architecture.md) |對於使用者是新 toohello 同步處理引擎，而且想 toolearn hello 架構，以及所用的 hello 詞彙相關。 |
| [技術概念](active-directory-aadconnectsync-technical-concepts.md) |簡短版本，以及 hello 架構 」 主題簡要說明 hello 詞彙。 |
| [Azure AD Connect 的拓撲](active-directory-aadconnect-topologies.md) |描述 hello 不同拓撲和案例 hello 同步處理引擎支援。 |
| **自訂組態** | |
| [執行 hello 安裝精靈一次](active-directory-aadconnectsync-installation-wizard.md) |說明哪些選項您擁有足夠的當您再次執行 hello Azure AD Connect 的安裝精靈。 |
| [了解宣告式佈建](active-directory-aadconnectsync-understanding-declarative-provisioning.md) |描述稱為宣告式佈建的 hello 組態模型。 |
| [了解宣告式佈建運算式](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |描述用於宣告式佈建的 hello 運算式語言的 hello 語法。 |
| [了解 hello 預設組態](active-directory-aadconnectsync-understanding-default-configuration.md) |描述 hello 鶈蜪規則和 hello 預設組態。 同時描述如何 hello 規則一起運作的 hello 鶈蜪案例 toowork。 |
| [了解使用者和連絡人](active-directory-aadconnectsync-understanding-users-and-contacts.md) |會繼續在 hello 前一個主題並描述使用者及連絡人的 hello 組態中的運作方式在一起，尤其是多樹系環境。 |
| [如何變更 toohello toomake 預設組態](active-directory-aadconnectsync-change-the-configuration.md) |引領您完成常見的組態變更 tooattribute toomake 流動的方式。 |
| [變更 hello 預設組態的最佳作法](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) |支援限制和進行變更 toohello 鶈蜪組態。 |
| [設定篩選](active-directory-aadconnectsync-configure-filtering.md) |說明 hello tooAzure AD，以及逐步 toolimit 物件正在進行的同步處理的方式的不同選項 tooconfigure 這些選項。 |
| **功能和案例** | |
| [防止意外刪除](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) |描述 hello*防止被意外刪除*功能及如何 tooconfigure 它。 |
| [排程器](active-directory-aadconnectsync-feature-scheduler.md) |描述 hello 內建排程器，可匯入、 同步處理，及匯出資料。 |
| [實作密碼同步處理](active-directory-aadconnectsync-implement-password-synchronization.md) |描述密碼同步化的運作方式、 如何 tooimplement，以及如何 toooperate 和疑難排解。 |
| [裝置回寫](active-directory-aadconnect-feature-device-writeback.md) |說明在 Azure AD Connect 中，裝置回寫的運作方式。 |
| [目錄擴充](active-directory-aadconnectsync-feature-directory-extensions.md) |描述如何 tooextend hello Azure AD 使用您自己的自訂屬性的結構描述。 |
| **同步處理服務** | |
| [Azure AD Connect 同步處理服務功能](active-directory-aadconnectsyncservice-features.md) |描述 hello 同步處理服務端和 toochange 如何在 Azure AD 同步設定。 |
| [重複屬性恢復功能](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) |描述如何 tooenable 並用**userPrincipalName**和**proxyAddresses**重複的屬性值的恢復功能。 |
| **作業和 UI** | |
| [同步處理服務管理員](active-directory-aadconnectsync-service-manager-ui.md) |描述 hello 同步處理服務管理員 」 UI，包括[作業](active-directory-aadconnectsync-service-manager-ui-operations.md)，[連接器](active-directory-aadconnectsync-service-manager-ui-connectors.md)， [Metaverse 設計工具](active-directory-aadconnectsync-service-manager-ui-mvdesigner.md)，和[Metaverse 搜尋](active-directory-aadconnectsync-service-manager-ui-mvsearch.md)索引標籤。 |
| [作業工作和考量](active-directory-aadconnectsync-operations.md) |說明作業考量，例如災害復原。 |
| **作法...** | |
| [重設 hello Azure AD 帳戶](active-directory-aadconnectsync-howto-azureadaccount.md) |如何 tooreset hello hello 服務帳戶使用認證從 Azure AD Connect 同步處理 tooAzure AD tooconnect。 |
| **詳細資訊和參考** | |
| [連接埠](active-directory-aadconnect-ports.md) |您的連接埠清單需要 tooopen hello 同步處理引擎，並在內部部署目錄與 Azure AD 之間。 |
| [同步處理 tooAzure Active Directory 的屬性](active-directory-aadconnectsync-attributes-synchronized.md) |列出在內部部署 AD 與 Azure AD 之間進行同步處理的所有屬性。 |
| [函式參考](active-directory-aadconnectsync-functions-reference.md) |列出宣告式佈建中可用的所有函式。 |

## <a name="additional-resources"></a>其他資源
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)

