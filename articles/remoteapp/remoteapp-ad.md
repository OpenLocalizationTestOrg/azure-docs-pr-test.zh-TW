---
title: "aaaAzure AD + 的 Azure RemoteApp 的 Active Directory 需求 |Microsoft 文件"
description: "深入了解如何設定 Active Directory 與 Azure RemoteApp 的 toowork tooset。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a>Azure RemoteApp 的 Azure AD + Active Directory 需求
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

對於您 Azure RemoteApp 的混合式集合，或您想要使用 AD Connect toofederate 雲端集合，您會需要 toodo hello 下列。

### <a name="connect-azure-ad-and-active-directory"></a>連接 Azure AD 和 Active Directory
如果您想要 tooconnect，Azure AD 租用戶和您在內部部署 Active Directory 環境中，使用 AD Connect。 它只會執行[4 按一下](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/)tooconnect hello 兩個目錄。

注意 - 混合式集合需使用目錄同步處理。

### <a name="make-sure-your-domaincom-match"></a>請確定您的 "@domain.com" 是相符的
開始之前，請確定您的 Azure AD 網域您在內部部署樹系相符項目 hello 尾碼該 hello UPN。 

所有使用者登入 Azure RemoteApp hello UPN 網域尾碼設定 Azure AD 中之後，將身分都登入 「 使用者 @<hello suffix you set up>。 」 請確定使用者可以也登入 hello 相同user@suffix到 hello 在內部部署網域。 在某些情況下您可以設定一個網域名稱時指定不同的網域尾碼，如 hello 使用者內部部署的 Azure AD 中 在此情況下，您的使用者會無法 tooconnect tooany 已加入網域的電腦或透過 Azure RemoteApp 的資源。

例如，如果您設定您的 UPN 網域尾碼為 contoso.com，AAD 中，但是有些使用者在內部部署/AD 中使用的設定的 toolog @contoso.uk，這些使用者將不會無法 toocorrectly 記錄，到 hello ARA 集合。 使用者必須是 UPN AAD 和 AD 中的將相同 hello 登入 toobe 可能 hello"

### <a name="create-objects-for-azure-remoteapp"></a>建立 Azure RemoteApp 的物件
您還需要下列內部部署 Active Directory 物件 toocreate hello:

* 服務帳戶 tooprovide 存取 toodomain 資源的 RemoteApp 程式加入 RDSH 結束點 toohello 在內部部署網域。
* 組織單位 (OU) toocontain RemoteApp 的電腦物件。 使用 hello OU 是建議 （但非必要） tooisolate hello 帳戶與您將 RemoteApp 搭配使用的原則。

您會需要這些物件的這兩個當您建立您的 RemoteApp 集合，因此先確定 toodo 這些步驟。

