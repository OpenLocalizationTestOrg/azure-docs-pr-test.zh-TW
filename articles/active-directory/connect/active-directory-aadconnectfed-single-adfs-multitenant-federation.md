---
title: "aaaFederating 與單一 AD FS 的多個 Azure AD |Microsoft 文件"
description: "本文件中，您將學習如何 toofederate 與單一的 AD FS 的多個 Azure AD。"
keywords: "聯盟, ADFS, AD FS, 多個租用戶, 單一 AD FS, 一個 ADFS, 多個租用戶同盟, 多樹系 adfs, aad 連線, 同盟, 跨租用戶同盟"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.openlocfilehash: 442192896b3b13f7bf9388396cd3769e194329d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a>將多個 Azure AD 執行個體和單一 AD FS 執行個體建立同盟

如果樹系之間有雙向信任，單一高可用 AD FS 伺服器陣列就可以聯合多個樹系。 這些多個樹系可能或可能無法對應 toohello 相同的 Azure Active Directory。 這篇文章提供如何 tooconfigure 同盟與單一 AD FS 部署多個樹系，同步處理 toodifferent Azure AD 的指示。

![多租用戶與單一 AD FS 的同盟關係](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> 在此案例中不支援裝置回寫和自動加入裝置。

> [!NOTE]
> Azure AD Connect 不能使用的 tooconfigure 同盟，在此案例中，與 Azure AD Connect 可以在單一的 Azure AD 中設定同盟網域。

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a>將 AD FS 和多個 Azure AD 建立同盟的步驟

請考慮在 Azure Active Directory contoso.onmicrosoft.com 網域 contoso.com 已經同盟與 hello AD FS 內部 contoso.com 在內部部署 Active Directory 環境中安裝。 Fabrikam.com 是 fabrikam.onmicrosoft.com Azure Active Directory 中的網域。

##<a name="step-1-establish-a-two-way-trust"></a>步驟 1︰建立雙向信任
 
中的 AD FS 中 fabrikam.com contoso.com toobe 無法 tooauthenticate 使用者，contoso.com 和 fabrikam.com 之間需要雙向信任關係。請依照下列中的 hello 指導方針[文章](https://technet.microsoft.com/library/cc816590.aspx)toocreate hello 雙向信任關係。
 
##<a name="step-2-modify-contosocom-federation-settings"></a>步驟 2︰修改 contoso.com 同盟設定 
 
hello 預設簽發者為單一網域同盟 tooAD FS"http://ADFSServiceFQDN/adfs/services/trust"，例如，"http://fs.contoso.com/adfs/services/trust 」 設定。 Azure Active Directory 要求每個同盟網域都需要擁有唯一簽發者。 Hello 相同 AD FS 會成為 toofederate 兩個網域，必須修改，使它是唯一的 AD FS 同盟與 Azure Active Directory 的每個網域的 toobe hello 簽發者值。 
 
Hello AD FS 伺服器上，開啟 Azure AD PowerShell 並執行下列步驟的 hello:
 
連接 toohello 包含 hello 網域 contoso.com Connect-msolservice 更新 hello de federación de contoso.com Update-msolfederateddomain-DomainName contoso.com 的 Azure Active Directory – SupportMultipleDomain
 
將變更 hello 網域同盟設定中的簽發者太"http://contoso.com/adfs/services/trust 」 和發行宣告規則將會新增 hello Azure AD 信賴憑證者信任 tooissue hello 正確 issuerId 值根據 hello UPN 尾碼。
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a>步驟 3︰建立 fabrikam.com 與 AD FS 的同盟
 
在 Azure AD powershell 工作階段執行下列步驟的 hello： 連接 tooAzure 包含 hello 網域 fabrikam.com 的 Active Directory

    Connect-MsolService
轉換 hello 管理 fabrikam.com 網域 toofederated:

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
上述操作的 hello 將同盟 hello 網域 fabrikam.com 以 hello 相同 AD FS。 您可以使用這兩個網域 Get-msoldomainfederationsettings 確認 hello 網域設定。

## <a name="next-steps"></a>後續步驟
[使用 Azure Active Directory 與 Active Directory 連線](active-directory-aadconnect.md)
