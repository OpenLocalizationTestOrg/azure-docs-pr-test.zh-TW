---
title: "aaaHow tooAssign 使用者 tooapplications |Microsoft 文件"
description: "了解使用者如何取得指派 tooan 租用戶中的應用程式"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a>如何 tooassign 使用者 tooapplications

本文將協助您 toounderstand 使用者取得如何指派 tooan 租用戶中的應用程式。

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a>如何使用者取得指派 tooan 在 Azure AD 中的應用程式？

使用者 tooaccess 應用程式，則必須先指派 tooit 以某種方式。 作業只能由系統管理員、 商務委派，或某些情況下，hello 使用者本身。 下面將描述使用者可以指派 tooapplications hello 方式：

1.  系統管理員[指派使用者](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)直接 toohello 應用程式

2.  系統管理員[指派群組](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)hello 使用者所屬 toohello 應用程式，包括：

  * 已從內部部署同步的群組

  * 建立 hello 雲端中的靜態安全性群組

  * A[動態安全性群組](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal)hello 雲端中建立

  * 建立 hello 雲端中的 Office 365 群組

  * hello[所有使用者](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups)群組

3.  系統管理員啟用[自助應用程式存取](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)tooallow 應用程式使用使用者 tooadd hello[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)**新增應用程式**功能**無商務核准**

4.  系統管理員啟用[自助應用程式存取](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)tooallow 應用程式使用使用者 tooadd hello[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)**新增應用程式**功能，但只有 w**ith 先前組選取的公司核准者核准**

5.  系統管理員啟用[自助群組管理](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management)tooallow 使用者 toojoin 太指派應用程式群組**無商務核准**

6.  系統管理員啟用[自助群組管理](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management)tooallow 使用者 toojoin 應用程式，但只能指派一組**與先前組選取的公司核准者核准**

7.  系統管理員指派授權 tooa 使用者直接針對第一個合作對象應用程式，例如[Microsoft Office 365](http://products.office.com/)

8.  Hello 使用者的授權 tooa 群組隸屬的 tooa 第一個合作對象應用程式，例如系統管理員指派[Microsoft Office 365](http://products.office.com/)

9.  [Tooan 應用程式，系統管理員同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)toobe 由所有使用者，而且使用者在登入時 toohello 應用程式

10. 使用者[tooan 應用程式，同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)自行登入 toohello 應用程式

## <a name="next-steps"></a>後續步驟
[使用 Azure Active Directory 管理應用程式](active-directory-enable-sso-scenario.md)
