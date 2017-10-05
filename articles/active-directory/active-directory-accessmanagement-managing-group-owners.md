---
title: "使用群組存取管理的後續步驟 | Microsoft Docs"
description: "管理安全性群組，以及如何使用這些群組管理資源的存取權的進階說明。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 44350a3c-8ea1-4da1-aaac-7fc53933dd21
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 82fbeb379e90add09f7c569111053f6e9b1bc9c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="managing-owners-for-a-group"></a>管理群組的擁有者
一旦資源擁有者將資源的存取權指派給 Azure AD 群組後，群組擁有者就會管理群組的成員資格。 資源擁有者實際上是委派權限給群組的擁有者，以指派使用者存取資源。

> [!IMPORTANT]
> Microsoft 建議您使用 Azure 入口網站中的 [Azure AD 系統管理中心](https://aad.portal.azure.com)來管理 Azure AD，而不要使用本文所提及的 Azure 傳統入口網站。 

## <a name="assigning-group-ownership"></a>指派群組擁有權
**將擁有者新增至群組**

1. 在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，選取 [Active Directory]，然後開啟您組織的目錄。
2. 選取 [群組]  索引標籤，然後開啟您想要在其中新增擁有者的群組。
3. 選取 [新增擁有者] 。
4. 在 [新增擁有者] 頁面上，選取您想要新增為此群組擁有者的使用者，並確定這個名稱新增至 [已選取] 窗格中。

**移除群組中的擁有者**

1. 在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，選取 [Active Directory]，然後開啟您組織的目錄。
2. 選取 [群組]  索引標籤，然後開啟您想要從中移除擁有者的群組。
3. 選取 [擁有者]  索引標籤。
4. 選取您要從這個群組中移除的擁有者，然後選取 [移除] 。

## <a name="additional-information"></a>其他資訊
這些文章提供有關 Azure Active Directory 的其他資訊。

* [使用 Azure Active Directory 群組管理資源的存取權](active-directory-manage-groups.md)
* [設定群組設定的 Azure Active Directory Cmdlet](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
* [什麼是 Azure Active Directory？](active-directory-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)
