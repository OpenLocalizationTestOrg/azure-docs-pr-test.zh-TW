---
title: "aaaAzure AD SAML 通訊協定參考 |Microsoft 文件"
description: "本文章提供在 Azure Active Directory hello 單一登入和單一登出 SAML 設定檔的概觀。"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 88125cfc-45c1-448b-9903-a629d8f31b01
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: priyamo
ms.custom: aaddev
ms.reviewer: dastrock
ms.openlocfilehash: d712289b16dc40a6b43a96fadef729c55cdaac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# Azure Active Directory 的 hello SAML 通訊協定的使用方式
Azure Active Directory (Azure AD) 採用 hello SAML 2.0 通訊協定 tooenable 應用程式單一登入 tooprovide 經驗 tootheir 使用者。 hello[單一登入](active-directory-single-sign-on-protocol-reference.md)和[單一登出](active-directory-single-sign-out-protocol-reference.md)SAML 設定檔的 Azure AD 說明如何在 hello 身分識別提供者服務中使用 SAML 判斷提示、 通訊協定和繫結。

SAML 通訊協定需要 hello 身分識別提供者 (Azure AD) 和 hello 服務提供者 （hello 應用程式） tooexchange 本身的資訊。

當應用程式已向 Azure AD 時，hello 應用程式開發人員會註冊與同盟相關的資訊與 Azure AD。 這包括 hello**重新導向 URI**和**中繼資料 URI** hello 應用程式。

Azure AD 使用 hello**中繼資料 URI**的 hello 雲端服務 tooretrieve hello 簽署金鑰和 hello 登出 hello 雲端服務的 URI。 如果 hello 應用程式不支援中繼資料 URI，hello 開發人員必須連絡 Microsoft 支援 tooprovide hello 登出 URI 和簽署金鑰。

Azure Active Directory 會公開租用戶專屬和一般 (租用戶獨立) 單一登入和單一登出端點。 這些 Url 代表可定址的位置--它們不只是識別碼-讓您可以移 toohello 端點 tooread hello 中繼資料。

* hello 租用戶專用端點位於`https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`。  hello<TenantDomainName>預留位置代表註冊的網域名稱或 Azure AD 租用戶的 TenantID GUID。 比方說，hello hello contoso.com 租用戶同盟中繼資料位於： https://login.microsoftonline.com/contoso.com/FederationMetadata/2007-06/FederationMetadata.xml

* hello 租用戶獨立端點位於`https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml`。在此端點位址、**常見**隨即出現，而不是租用戶網域名稱或識別碼。

Azure AD 會發行的 hello 同盟中繼資料文件的相關資訊，請參閱[同盟中繼資料](active-directory-federation-metadata.md)。
