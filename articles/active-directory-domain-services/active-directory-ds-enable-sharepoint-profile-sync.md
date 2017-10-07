---
title: "Azure Active Directory Domain Services：啟用對 SharePoint User Profile Service 的支援 | Microsoft Docs"
description: "設定 Azure Active Directory 網域服務受管理的網域 toosupport 設定檔同步處理 SharePoint 伺服器"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9de4f810380309e8f6436fc24412701645978f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a>設定 SharePoint 伺服器的受管理的網域 toosupport 設定檔同步處理
SharePoint Server 包含用來同步處理使用者設定檔的 User Profile Service。 註冊使用者設定檔服務的 hello tooset，適當的權限需要 toobe 授與 Active Directory 網域。 如需詳細資訊，請參閱[授與 Active Directory Domain Services 權限以供 SharePoint Server 2013 中的設定檔同步處理使用](https://technet.microsoft.com/library/hh296982.aspx)。

本文說明如何設定 Azure AD 網域服務受管理的網域 toodeploy hello SharePoint 伺服器使用者設定檔同步處理服務。

## <a name="hello-aad-dc-service-accounts-group"></a>hello ' AAD DC Service Accounts' 群組
安全性群組呼叫 '**AAD DC 的服務帳戶**' hello '的使用者 」 組織單位上受管理的網域內可供使用。 您可以看到這個群組中 hello **Active Directory 使用者和電腦**MMC 嵌入式管理單元在受管理的網域上。

![AAD DC Service Accounts 安全性群組](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

此安全性群組的成員會委派下列權限的 hello:
- hello 根目錄 DSE 的 hello 上 hello 複寫目錄變更權限管理的網域。
- hello hello 設定命名內容上的複寫目錄變更權限 (cn = configuration 容器) 的 hello 受管理網域。

此安全性群組也是 hello 內建群組成員**Pre-Windows 2000 Compatible Access**。

![AAD DC Service Accounts 安全性群組](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a>啟用您的受管理的網域 toosupport SharePoint 伺服器使用者設定檔同步處理
您可以新增 hello 服務帳戶使用的 SharePoint 使用者設定檔同步處理 toohello **AAD DC 的服務帳戶**群組。 如此一來，hello 同步處理帳戶取得足夠的權限 tooreplicate 變更 toohello 目錄。 此組態步驟可讓 SharePoint 伺服器的使用者設定檔同步 toowork 正確。

![AAD DC Service Accounts - 新增成員](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![AAD DC Service Accounts - 新增成員](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a>相關內容
* [技術參考 - 授與 Active Directory Domain Services 權限以供 SharePoint Server 2013 中的設定檔同步處理使用](https://technet.microsoft.com/library/hh296982.aspx)
