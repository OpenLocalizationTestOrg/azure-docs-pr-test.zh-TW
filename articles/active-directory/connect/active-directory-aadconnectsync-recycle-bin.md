---
title: "Azure AD Connect 同步處理︰啟用 AD 資源回收筒 | Microsoft Docs"
description: "本主題建議 hello 使用 Azure AD Connect 與 AD 資源回收筒功能。"
services: active-directory
keywords: "AD 資源回收筒, 意外刪除, 來源錨點"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a>Azure AD Connect 同步處理︰啟用 AD 資源回收筒
建議您針對在內部部署 Active 目錄，也就是已同步處理的 tooAzure AD 啟用 hello AD 資源回收筒功能。 

如果您不小心刪除了內部部署 AD 使用者物件與它使用 hello 功能，Azure AD 會還原 hello 對應的 Azure AD 使用者物件的還原。  Hello AD 資源回收筒功能的相關資訊，請參閱 tooarticle[還原刪除的 Active Directory 物件的案例概觀](https://technet.microsoft.com/library/dd379542.aspx)。

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a>優點啟用 hello AD 資源回收筒
這項功能可協助執行 hello 下列還原 Azure AD 使用者物件：

* 如果您不小心刪除了內部部署 AD 使用者物件、 hello 對應的 Azure AD 使用者物件將會在刪除 hello 下一個同步處理循環。 根據預設，Azure AD 會保留 hello 刪除 Azure AD 使用者物件，處於虛刪除狀態 30 天的時間。

* 如果您有內部啟用的 AD 資源回收筒功能，您可以還原已刪除的 hello 內部部署 AD 使用者物件而不需要變更其來源錨點值。 當 hello 復原在內部部署同步處理 AD 使用者物件 tooAzure AD，Azure AD 將會還原 hello 對應虛刪除 Azure AD 使用者物件。 來源錨點屬性的相關資訊，請參閱 tooarticle [Azure AD Connect： 設計概念](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor)。

* 如果您不需要在內部部署 AD 資源回收筒功能已啟用，您可能需要的 toocreate 的 AD 使用者物件 tooreplace hello 已刪除物件。 如果 Azure AD Connect 同步處理服務設定的 toouse 系統產生 AD 屬性 （例如 ObjectGuid) hello 來源錨點屬性，hello 新建立的 AD 使用者物件將不具有 hello 相同的來源錨點值為 hello 刪除 AD 使用者物件。 當 hello 新建立的 AD 使用者物件同步處理的 tooAzure AD，Azure AD 會建立新的 Azure AD 使用者物件，而不是還原 hello 虛刪除 Azure AD 使用者物件。

> [!NOTE]
> 根據預設，Azure AD 會讓已刪除的 Azure AD 使用者物件保持 30 天的虛刪除狀態，再將其永久刪除。 不過，系統管理員可以加速 hello 刪除這類物件。 一旦 hello 物件會永久刪除，就無法再復原，即使在內部部署 AD 資源回收筒功能已啟用。



## <a name="next-steps"></a>後續步驟
**概觀主題**

* [Azure AD Connect 同步處理：了解及自訂同步處理](active-directory-aadconnectsync-whatis.md)

* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)
