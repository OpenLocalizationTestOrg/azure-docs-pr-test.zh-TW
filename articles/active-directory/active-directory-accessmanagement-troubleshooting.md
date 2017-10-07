---
title: "aaaTroubleshooting 群組動態成員資格 |Microsoft 文件"
description: "Azure AD 中群組動態成員資格的疑難排解秘訣。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a>疑難排解群組的動態成員資格
**我在群組上設定的規則，但沒有成員資格取得更新 hello 群組中**<br/>請確認該 hello**啟用委派群組管理**設定為太**是**在 hello**設定** 索引標籤。只有當您登入 Azure Active Directory Premium 授權的使用者 toowhom 是指派，您會看到這項設定。 請確認 hello hello 規則上的使用者屬性的值： 是否有符合 hello 規則的使用者？

**我設定了規則，但現在會移除 hello 的 hello 規則的現有成員**<br/>這是預期行為。 啟用或變更規則時，會移除 hello 群組的現有成員。 傳回從 hello 規則的評估 hello 使用者會新增為成員 toohello 群組。     

**當我新增或變更規則時，沒有立即看到成員資格變更，為什麼？**<br/>專用的成員資格評估會定期在非同步的背景處理序中完成。 Hello 程序會接受時間長度取決於 hello 中您目錄和 hello 大小 hello 群組建立 hello 規則結果的使用者數目。 通常，目錄與小量的使用者會看到 hello 群組成員資格變更小於幾分鐘的時間。 目錄具有大量的使用者可能需要 30 分鐘或更長的 toopopulate。

### <a name="next-steps"></a>後續步驟
這些文章提供有關 Azure Active Directory 的其他資訊。

* [使用 Azure Active Directory 群組來管理存取 tooresources](active-directory-manage-groups.md)
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
* [什麼是 Azure Active Directory？](active-directory-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)
