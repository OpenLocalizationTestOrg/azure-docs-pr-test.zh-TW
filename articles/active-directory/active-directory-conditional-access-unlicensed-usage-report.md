---
title: "未經授權的使用報告 | Microsoft Docs"
description: "未經授權的使用報告可協助您識別使用 Azure AD 付費功能的未經授權使用者。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: mtillman
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2018
ms.author: markvi
ms.openlocfilehash: 8bcd814ee7b7bfc158e62ad26e6cc23781f5352d
ms.sourcegitcommit: 384d2ec82214e8af0fc4891f9f840fb7cf89ef59
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2018
---
# <a name="unlicensed-usage-report"></a>未經授權的使用報告
未經授權的使用報告可協助您識別使用 Azure AD 付費功能的未經授權使用者。 這可讓您充分利用您已購買的授權，以及確認您知道何時可能需要額外的授權。 

此報告會顯示過去 30 天內有使用付費功能的情形。 

## <a name="report-structure"></a>報告結構
| 資料行名稱 | 說明 |
|:--- |:--- |
| 未經授權的使用者 |使用者名稱 |
| 功能 |功能名稱。 例如：條件式存取 |
| 存取的應用程式 |使用功能存取的應用程式名稱。 例如︰Office 365 SharePoint Online |

> [!NOTE]
> 如果使用者帳戶已遭刪除，「未經授權的使用者」資料行將會填入識別碼，例如 1003000090D8B285
> 
> 

## <a name="conditional-access-feature"></a>條件式存取功能
未經授權的使用者如果沒有 Azure AD Premium 授權，則會在存取已套用條件式存取原則的服務時遭到標示。 

這適用於 MFA/位置原則以及使用 Intune 的裝置原則。

## <a name="see-also"></a>另請參閱
* [搭配使用條件式存取與 Office 365 和其他 Azure Active Directory 連線應用程式](active-directory-conditional-access-azure-portal.md)
* [開始使用 Azure AD 的條件式存取](active-directory-conditional-access-azure-portal-get-started.md) 

