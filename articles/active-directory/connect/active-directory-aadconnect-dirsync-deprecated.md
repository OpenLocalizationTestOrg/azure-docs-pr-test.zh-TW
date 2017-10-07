---
title: "從 DirSync 和 Azure AD Sync aaaUpgrade |Microsoft 文件"
description: "描述如何從 DirSync 和 Azure AD Sync tooAzure AD tooupgrade 連接。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: bd68fb88-110b-4d76-978a-233e15590803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d465b137fb54f0c6e28ccf73429c4bd3aafd8698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-windows-azure-active-directory-sync-and-azure-active-directory-sync"></a>升級 Windows Azure Active Directory Sync 和 Azure Active Directory Sync
Azure AD Connect 是 hello 最佳方式 tooconnect 在內部部署目錄與 Azure AD 和 Office 365。 這是很好的時間 tooupgrade tooAzure AD Connect，從 Windows Azure Active Directory 同步作業 (DirSync) 或 Azure AD Sync 因為這些工具現在已被取代，並會到達結束在 2017 年 4 月 13，支援。

已被取代的 hello 兩個身分識別同步處理工具所提供的單一樹系的客戶 (DirSync) 和多樹系和其他進階的客戶 （Azure AD 同步處理）。 這些較舊的工具已經取代為適用於所有案例的單一解決方案︰Azure AD Connect。 它提供新的功能、增強功能和新案例的支援。 toobe 無法 toocontinue toosynchronize 您的內部部署身分識別資料 tooAzure AD 和 Office 365，我們強烈建議您升級 tooAzure AD Connect。

DirSync hello 最後一個版本已於 2014 年 7 月發行和 hello 的 Azure AD Sync 的最後一個版本已於 2015 年發行。

## <a name="what-is-azure-ad-connect"></a>何謂 Azure AD Connect
Azure AD Connect 是 hello 後續 tooDirSync 和 Azure AD Sync。它結合了兩者支援的所有案例。 您可以在 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)中進一步了解。

## <a name="deprecation-schedule"></a>淘汰排程
| Date | 註解 |
| --- | --- |
| 2016 年 4 月 13 日 |Windows Azure Active Directory Sync (“DirSync”) 和 Microsoft Azure Active Directory Sync (“Azure AD Sync”) 已宣布淘汰。 |
| 2017 年 4 月 13 日 |支援結束。 客戶將不再能夠 tooopen 支援案例，而不升級 tooAzure AD 先連線。 |
|2017 年 12 月 31 日|Azure AD 已不再接受來自 Windows Azure Active Directory Sync (“DirSync”) 和 Microsoft Azure Active Directory Sync (“Azure AD Sync”) 的通訊。

## <a name="how-tootransition-tooazure-ad-connect"></a>如何 tootransition tooAzure AD Connect
如果您正在執行 DirSync，有兩種方式可以升級︰就地升級和平行部署。 對大多數的客戶，以及如果您擁有最新的作業系統和少於 50,000 個物件，建議採用就地升級。 在其他情況下，建議您使用 toodo 平行部署，其中是您的 DirSync 組態移動 tooa 執行 Azure AD Connect 的新伺服器。

如果您使用 Azure AD Sync，則建議採用就地升級。 如果您想要它是可能 tooinstall 新的 Azure AD Connect 伺服器，以平行方式，和執行來自您 Azure AD 同步伺服器 tooAzure AD 迴旋移轉連接。

| 方案 | 案例 |
| --- | --- |
| [從 DirSync 升級](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>如果您有已在執行中的現有 DirSync 伺服器。</li> |
| [從 Azure AD Sync 升級](active-directory-aadconnect-upgrade-previous-version.md) |<li>如果您要從 Azure AD Sync 移動。</li> |

如果您想如何 toosee toodo 就地升級 AD Connect 目錄同步 tooAzure 然後看到這個 Channel 9 影片：

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-in-place-upgrade-from-legacy-tools/player]
>
>

## <a name="faq"></a>常見問題集
**問： 我已從 hello Azure 團隊和/或將訊息從 hello Office 365 訊息中心，收到電子郵件通知，但我正在使用連接。**  
hello 通知也會傳送 toocustomers 組建編號 1.0 搭配使用 Azure AD Connect。\*.0 （使用前 1.1 版本）。 Microsoft 建議的客戶使用 Azure AD Connect 目前 toostay 釋放。 hello[自動升級](active-directory-aadconnect-feature-automatic-upgrade.md)1.1 版中引進的功能可讓您輕鬆 tooalways 已安裝的 Azure AD Connect 的最新版本。

**問︰DirSync/Azure AD Sync 會在 2017 年 4 月 13 日停止運作嗎？**  
DirSync/Azure AD 同步處理會繼續 toowork 年 4 月 13 2017年上。  不過，Azure AD 在 2017 年 12 月 31 日將不再接受來自 DirSync/Azure AD Sync 的通訊。

**問：哪些 DirSync 版本可以進行升級？**  
支援的 tooupgrade 從任何目錄同步版本，目前正在使用它。

**問： 該如何 hello Azure AD Connector FIM/MIM？**  
hello 適用於 FIM/MIM Azure AD 連接器具有**不**已被取代。 它目前在 **功能凍結**狀態；不會新增任何功能，而且不會收到任何錯誤修正。 Microsoft 建議客戶使用它從其 tooplan toomove tooAzure AD Connect。 強烈建議 toonot 啟動任何新的部署使用它。 將取代在未來的 hello 公告此連接器。

## <a name="additional-resources"></a>其他資源
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)
