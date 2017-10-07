---
title: "aaaHow tooperform 存取檢閱 |Microsoft 文件"
description: "了解如何檢閱的 tooperform hello Azure Privileged 的 Identity Management 的應用程式。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 301a5e9f97b68fedfbf4954e0bd7dadb7f0fc510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-an-access-review-in-azure-ad-privileged-identity-management"></a>如何 tooperform 存取檢閱在 Azure AD Privileged Identity Management
Azure Active Directory (AD) 的權限身分管理可簡化企業如何管理 Azure AD 中的特殊權限的存取 tooresources 和 Office 365 或 Microsoft Intune 等其他 Microsoft online services。  

如果您指派 tooan 系統管理角色，您組織的特殊權限的角色系統管理員可能會要求您 tooregularly 確認適用於您作業仍然需要該角色。 您可能會收到電子郵件，其中包含的連結，或者您可以移直線 toohello [Azure 入口網站](https://portal.azure.com)。 請遵循自我檢閱您已指派的角色，此文章 tooperform hello 步驟。

如果您想要存取檢閱的特殊權限的角色系統管理員，取得更多詳細資料，在[如何 toostart 存取檢閱](active-directory-privileged-identity-management-how-to-start-security-review.md)。

## <a name="add-hello-privileged-identity-management-application"></a>新增 hello Privileged Identity Management 的應用程式
您可以使用 hello Azure AD Privileged Identity Management (PIM) 的應用程式中 hello [Azure 入口網站](https://portal.azure.com/)tooperform 您進行檢閱。  如果您的入口網站上沒有 hello Azure AD Privileged Identity Management 的應用程式，請遵循啟動這些步驟 tooget。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 選取您在 hello 右上角的 hello Azure 入口網站，與您將您的選取 hello 目錄中的使用者名稱進行操作。
3. 選取**更多服務**並用的 hello 篩選文字方塊中 toosearch **Azure AD Privileged Identity Management**。
4. 請檢查**Pin toodashboard** ，然後按一下**建立**。 hello Privileged Identity Management 的應用程式將會開啟。

## <a name="approve-or-deny-access"></a>核准或拒絕存取
當您核准或拒絕存取時，您只要告訴 hello 檢閱者您仍要使用此角色或不。 選擇**核准**如果您想在 hello 角色 toostay 或**拒絕**如果您不需要再 hello 存取。 Hello 檢閱者套用 hello 結果之前，不會立即，變更您的狀態。
請依照這些步驟 toofind 並完成 hello 存取檢閱：

1. 在 hello PIM 應用程式中，選取 **檢閱特殊權限存取**。 如果您有任何暫止存取檢閱，它們會出現在 hello Azure AD 存取檢閱 刀鋒視窗。
2. 選取您想要 toocomplete hello 檢閱。
3. 除非您建立 hello 檢閱時，您可以顯示為 hello 只有 hello 檢閱中的使用者。 選取 hello 核取記號和 tooyour 名稱下一步。
4. 選擇 [核准] 或 [拒絕]。 您可能需要在 hello 決策的原因 tooinclude**提供原因**文字方塊。  
5. 關閉 hello**檢閱 Azure AD 角色**刀鋒視窗。

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>後續步驟
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
