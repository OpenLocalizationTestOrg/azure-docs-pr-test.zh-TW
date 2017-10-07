---
title: "aaaWhat 是以群組為基礎來授權 Azure Active Directory 中？ | Microsoft Docs"
description: "描述 Azure Active Directory 群組型授權、如何運作以及最佳做法"
services: active-directory
keywords: "Azure AD 授權"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/29/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 11647de6b76022cd2393751fcafc67ce671aeba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="group-based-licensing-basics-in-azure-active-directory"></a>Azure Active Directory 中以群組為基礎的授權基本概念

使用 Microsoft 付費雲端服務 (例如 Office 365、Enterprise Mobility + Security、Dynamics CRM 及其他類似的產品) 需要授權。 這些授權指派給需要存取 toothese 服務 tooeach 使用者。 toomanage 授權，系統管理員使用其中一個 hello 管理入口網站 （Office 或 Azure） 和 PowerShell 指令程式。 Azure Active Directory (Azure AD) 是 hello 支援所有的 Microsoft 雲端服務的身分識別管理的基礎結構。 Azure AD 會儲存使用者授權指派狀態的相關資訊。

到目前為止，授權只能在 hello 個別使用者層級，它可能會造成大規模管理困難指派。 例如，根據組織的變更，例如使用者加入或離開 hello 組織或部門的 tooadd 或移除使用者授權，系統管理員通常必須撰寫複雜的 PowerShell 指令碼。 此指令碼可讓個別呼叫 toohello 雲端服務。

tooaddress 所面臨的挑戰，Azure AD 現在包含群組為基礎的授權。 您可以指派一或多個產品授權 tooa 群組。 Azure AD 可確保 hello 授權指派 tooall hello 群組成員。 加入 hello 群組的任何新成員指派 hello 適當授權。 當它們離開 hello 群組時，會移除這些授權。 這樣會排除 hello 需要自動化透過 PowerShell tooreflect 變更 hello 組織與部門的結構，每個使用者為基礎的授權管理。

## <a name="features"></a>特性

以下是以群組為基礎授權的 hello 主要功能：

- 授權可以 tooany 安全性群組指派 Azure AD 中。 內部部署可以使用 Azure AD Connect 來同步處理安全性群組。 直接在 Azure AD （也稱為僅限雲端的群組），或自動透過 hello Azure AD 動態群組功能，您也可以建立安全性群組。

- 當產品的授權指派 tooa 群組時，hello 系統管理員可以停用 hello 產品中的一個或多個服務方案。 一般而言，這是當尚未使用的產品中納入服務準備好 toostart hello 組織。 例如，hello 系統管理員可能會指派 Office 365 tooa 部門，但暫時停用 hello Yammer 服務。

- 支援所有需要使用者層級授權的 Microsoft 雲端服務。 這包括所有 Office 365 產品、Enterprise Mobility + Security 和 Dynamics CRM。

- 群組為基礎的授權其目前只能透過[hello Azure 入口網站](https://portal.azure.com)。 如果您主要是使用其他管理入口網站為使用者與群組管理，例如 hello Office 365 入口網站中，您可以繼續 toodo 因此。 但是，您應該使用 hello Azure 入口網站 toomanage 授權在群組層級。

- Azure AD 會自動管理因群組成員資格變更而產生的授權修改。 一般而言，在成員資格變更後的幾分鐘內，授權修改就會生效。

- 一個使用者可以屬於多個已指定授權原則的群組。 使用者也可以有一些直接從任何群組之外指派的授權。 產生使用者狀態的 hello 是所有指派的產品和服務授權的組合。

- 在某些情況下，授權不能指派 tooa 使用者。 例如，在 hello 租用戶不可能有足夠的可用授權或衝突的服務可能已指派給 hello 在相同的時間。 系統管理員具有存取 tooinformation 有關針對 Azure AD 無法完整處理群組授權的使用者。 然後，他們可以根據該資訊採取更正動作。

- 公用預覽期間，Azure AD Basic 或 Premium edition 的付費或試用訂用帳戶需要在 hello 租用戶 toouse 群組為基礎的授權管理。

## <a name="next-steps"></a>後續步驟

toolearn 有關透過群組為基礎授權的授權管理的其他案例的詳細資訊，請參閱：

* [在 Azure Active Directory 中開始使用授權](active-directory-licensing-get-started-azure-portal.md)
* [Azure Active Directory 中指派的授權 tooa 群組](active-directory-licensing-group-assignment-azure-portal.md)
* [識別及解決 Azure Active Directory 中群組的授權問題](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [如何 toomigrate 個別授權 toogroup 型授權 Azure Active Directory 中的使用者](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory 群組型授權其他案例 (英文)](active-directory-licensing-group-advanced.md)
