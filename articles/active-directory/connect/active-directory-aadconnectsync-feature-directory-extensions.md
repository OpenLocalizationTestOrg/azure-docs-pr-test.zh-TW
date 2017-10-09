---
title: "Azure AD Connect 同步：目錄擴充 | Microsoft Docs"
description: "本主題說明在 Azure AD Connect 的 hello 目錄延伸模組功能。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 31525ae914aa4d9e047ea1515b460a8311d5c815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a>Azure AD Connect 同步處理：目錄擴充
目錄延伸模組可讓您 tooextend hello 結構描述在您自己的屬性從內部部署 Active Directory 與 Azure AD 中。 這項功能可讓您 toobuild LOB 應用程式耗用繼續 toomanage 內部部署的屬性。 透過 [Azure AD Graph 目錄擴充](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)或 [Microsoft Graph](https://graph.microsoft.io/) 即可取用這些屬性。 您可以看到 hello 屬性可以透過[Azure AD Graph 總管](https://graphexplorer.cloudapp.net)和[Microsoft 圖表總管](https://graphexplorer2.azurewebsites.net/)分別。

目前沒有任何 Office 365 工作負載取用這些屬性。

您設定的其他屬性想 toosynchronize hello hello 安裝精靈 中的自訂設定路徑中。
![結構描述擴充精靈](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)  
hello 安裝顯示 hello 下列屬性，也就是有效的候選項目：

* 使用者和群組物件類型
* 單一值屬性︰字串、布林值、整數、二進位檔
* 多值屬性︰字串、二進位檔

hello 份屬性清單會從 Azure AD connect 的安裝期間建立的 hello 結構描述快取讀取。 如果您已延伸 hello Active Directory 架構，與其他屬性，然後 hello[結構描述必須重新整理](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema)會顯示這些新的屬性之前。

Azure AD 中的物件可以有 too100 目錄延伸模組屬性。 hello 長度上限是 250 個字元。 如果屬性值的長度，則會截斷 hello 同步處理引擎。

在 Azure AD Connect 安裝期間，會註冊可提供這些屬性的應用程式。 您可以看到這個 hello Azure 入口網站中的應用程式。  
![結構描述擴充應用程式](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

現在可透過 Graph 提供這些屬性：  
![圖形](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

hello 屬性前面會加上副檔名\_{AppClientId}\_。 hello AppClientId 有的 hello 相同 Azure AD 租用戶中的所有屬性的值。

## <a name="next-steps"></a>後續步驟
深入了解 hello [Azure AD Connect 同步處理](active-directory-aadconnectsync-whatis.md)組態。

深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。
