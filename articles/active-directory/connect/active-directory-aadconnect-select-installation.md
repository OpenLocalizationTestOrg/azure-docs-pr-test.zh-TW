---
title: "Azure AD Connect：選取安裝類型 | Microsoft Docs"
description: "本主題引導您 tooselect hello 安裝的 Azure AD Connect 所輸入的 toouse"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a>選取 Azure AD Connect 的安裝類型 toouse
Azure AD Connect 針對新安裝提供兩種安裝類型：快速和自訂。 本主題可協助您在安裝期間選項 toouse toodecide。

## <a name="express"></a>Express
Express 是 hello 最常見的選項，並正由 90%的所有新的安裝。 它是設計的 tooprovide hello 最常見的客戶案例的運作方式的設定。

此選項假設：

- 您有內部部署的單一 Active Directory 樹系。
- 您擁有 hello 安裝，您可以使用企業系統管理員帳戶。
- 您內部部署 Active Directory 中的物件少於 10 萬個。

您會獲得：

- [密碼同步化](active-directory-aadconnectsync-implement-password-synchronization.md)從內部部署 tooAzure AD 進行單一登入。
- 同步處理[使用者、群組、連絡人及 Windows 10 電腦](active-directory-aadconnectsync-understanding-default-configuration.md)的組態。
- 所有網域和所有 OU 中所有合格物件的同步處理。
- [自動升級](active-directory-aadconnect-feature-automatic-upgrade.md)是啟用的 toomake 確定您一律使用 hello 最新可用版本。

在下列情況下，您仍然可以選擇使用 [快速]：

- 如果您不想 toosynchronize 所有 Ou，您仍然可以使用快速並在 hello 最後一個頁面上，取消選取**啟動 hello 同步處理程序...***. 然後再次執行 hello 安裝精靈，並變更中的 hello Ou[組態選項](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options)並啟用排程的同步處理。
- 您想例如密碼回寫 tooenable 其中一項在 Azure AD Premium，hello 功能。 先經過 express tooget hello 初始安裝已完成。 然後再次執行 hello 安裝精靈，並變更 hello[組態選項](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options)。

## <a name="custom"></a>自訂
hello 自訂的路徑可讓您比 express 更多選擇。 它應在所有情況下，快速的上一節中所述的 hello 設定不代表貴組織。

使用時機：

- 您沒有在 Active Directory 中存取 tooan 企業系統管理員帳戶。
- 您有多個樹系，或您計劃 toosynchronize hello 未來中的多個樹系。
- 您無法連線到從 hello 連接伺服器的樹系中有網域。
- 您計劃 toouse 同盟或傳遞驗證的使用者登入。
- 您有 100,000 個以上的物件，而且需要 toouse 完整的 SQL Server。
- 您計劃 toouse 群組為基礎的篩選和不僅網域或組織單位型篩選。

## <a name="upgrade-from-dirsync"></a>從 DirSync 升級
如果您目前使用 DirSync，然後依照中的 hello 步驟[從 DirSync 升級](active-directory-aadconnect-dirsync-upgrade-get-started.md)tooupgrade 您現有的組態。 有兩個不同的升級選項：

- 就地升級 tooinstall 連接上 hello 相同伺服器。
- Hello 現有的 DirSync 伺服器仍可運作時，平行部署 tooinstall 連接新的伺服器上。

## <a name="upgrade-from-azure-ad-sync"></a>從 Azure AD Sync 升級
如果您目前使用 Azure AD Sync，則您可以依照 hello[相同的步驟](active-directory-aadconnect-upgrade-previous-version.md)做為您從一個連接版本 tooa 較新的升級時。 有兩個不同的升級選項：

- 就地升級 tooinstall 連接上 hello 相同伺服器。
- 迴旋移轉 tooinstall 連接新的伺服器時 hello 現有 Azure AD 同步伺服器上時仍可運作。

## <a name="migrate-from-fim2010-or-mim2016"></a>從 FIM2010 或 MIM2016 移轉
如果您目前以 hello Azure AD 連接器使用 Forefront Identity Manager 2010 或 Microsoft Identity Manager 2016，唯一的選項是移轉。 中所述步驟 hello[迴旋移轉](active-directory-aadconnect-upgrade-previous-version.md#swing-migration)。 在 hello 步驟中，取代 FIM2010/MIM2016 中任何提及 Azure AD Sync。

## <a name="next-steps"></a>後續步驟
根據 hello 選項而定，您已選取 toouse，請使用 hello 資料表的內容 toohello 左 toofind 您文件以 hello 詳細步驟。
