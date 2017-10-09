---
title: "aaaTwo 步驟驗證，且 AD FS 的 Azure MFA |Microsoft 文件"
description: "這是描述 tooget 如何開始使用 Azure MFA 和 AD FS 的 hello Azure 多因素驗證頁面。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a>開始使用 Azure Multi-Factor Authentication Server 和 Active Directory Federation Services
<center>![雲端](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center>

如果組織已使用 AD FS 讓內部部署 Active Directory 與 Azure Active Directory 同盟，就會有兩個使用 Azure Multi-Factor Authentication 的選項。

* 使用 Azure Multi-Factor Authentication 或 Active Directory Federation Services 保護雲端資源
* 使用 Azure Multi-Factor Authentication Server 保護雲端和內部部署資源

hello 下表摘要說明 hello 保護與 Azure Multi-factor Authentication Server 和 AD FS 資源之間的驗證體驗

| 驗證體驗 - 瀏覽器型應用程式 | 驗證體驗 - 非瀏覽器型應用程式 |
|:--- |:--- |:--- |
| 使用 Azure Multi-Factor Authentication 保護 Azure AD 資源 |<li>hello 第一個驗證步驟會執行內部部署使用 AD FS。</li> <li>hello 第二個步驟是使用雲端驗證來執行的電話式方法。</li> |
| 使用 Active Directory Federation Services 保護 Azure AD 資源 |<li>hello 第一個驗證步驟會執行內部部署使用 AD FS。</li><li>hello 第二個步驟是內部執行區分 hello 宣告。</li> |

有關同盟使用者之應用程式密碼的警告：

* 應用程式密碼是使用雲端驗證進行驗證，因此會略過同盟。 唯有在設定應用程式密碼時才能主動使用同盟。
* 應用程式密碼不會遵守內部部署用戶端存取控制設定。
* 您會失去應用程式密碼的內部部署驗證記錄功能。
* 帳戶停用/刪除可能需要針對目錄同步作業，因而延遲在 hello 雲端身分識別的應用程式密碼停用/刪除 toothree 小時。

## <a name="next-steps"></a>後續步驟
設定 Azure Multi-factor Authentication 或 hello 與 AD FS 的 Azure Multi-factor Authentication Server 上的資訊，請參閱下列文章 hello:

* [使用 Azure Multi-Factor Authentication 和 AD FS 保護雲端資源](multi-factor-authentication-get-started-adfs-cloud.md)
* [搭配 Windows Server 2012 R2 AD FS 使用 Azure Multi-Factor Authentication Server 保護雲端和內部部署資源](multi-factor-authentication-get-started-adfs-w2k12.md)
* [搭配 AD FS 2.0 使用 Azure Multi-Factor Authentication Server 保護雲端和內部部署資源](multi-factor-authentication-get-started-adfs-adfs2.md)
