---
title: "Azure Active Directory Identity Protection 偵測到的 aaaVulnerabilities |Microsoft 文件"
description: "Azure Active Directory Identity Protection 偵測到的 hello 弱點的概觀。"
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, 管理應用程式, 安全性, 風險, 風險層級, 弱點, 安全性原則"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 5e1cb401f8b566a180eb46e3420a090bcfc66767
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a>Azure Active Directory Identity Protection 偵測到的弱點
弱點是您的環境中攻擊者可以利用的弱點。 我們建議您解決您的組織，這些弱點 tooimprove hello 安全性狀態，並防止攻擊者利用它們。


![弱點](./media/active-directory-identityprotection-vulnerabilities/101.png "弱點")



hello 下列章節提供您的識別身分保護所報告的 hello 弱點的概觀。

## <a name="multi-factor-authentication-registration-not-configured"></a>未設定 Multi-Factor Authentication 註冊
這可協助您控制組織中的 hello 部署的 Azure Multi-factor Authentication。 

Azure 多因素驗證提供安全性 toouser 驗證的第二層。 它可協助保護存取 toodata 和應用程式，同時滿足簡單登入程序的使用者需求。 它可以透過一些簡單的驗證選項 (例如電話、文字訊息，或行動應用程式通知或驗證代碼，以及第三方 OATH 權杖) 來提供強大的驗證功能。

建議您要求對使用者登入進行 Multi-Factor Authentication。在 Identity Protection 提供的以風險為基礎的條件式存取原則中，Multi-Factor Authentication 扮演關鍵角色。

如需詳細資訊，請參閱 [什麼是 Azure Multi-Factor Authentication？](../multi-factor-authentication/multi-factor-authentication.md)

## <a name="unmanaged-cloud-apps"></a>未受管理的雲端應用程式
此弱點可協助您識別組織中未受管理的雲端應用程式。

現代企業 IT 部門通常不知道其組織中的使用者工作使用 toodo 所有 hello 雲端應用程式。 它是簡單 toosee 為什麼系統管理員就必須考慮未經授權的存取 toocorporate 資料、 可能的資料流失和其他安全性風險。 

我們建議您的組織部署 Cloud App Discovery toodiscover unmanaged 雲端應用程式和 toomanage 這些應用程式使用 Azure Active Directory。

如需詳細資訊，請參閱 [使用 Cloud App Discovery 尋找未受管理的雲端應用程式](active-directory-cloudappdiscovery-whatis.md)。

## <a name="security-alerts-from-privileged-identity-management"></a>來自 Privileged Identity Management 的安全性警示
此弱點可協助您找出並解決有關您組織中特殊權限身分識別的警示。  

tooenable 特殊權限作業使用者 toocarry，組織需要 toogrant 使用者在 Azure AD 中的暫時或永久特殊權限存取 Azure 或 Office 365 資源或其他 SaaS 應用程式。 每個組織這些權限的使用者會增加 hello 受攻擊面。 這可協助您識別使用者透過不需要特殊權限的存取權，並採取適當的動作 tooreduce 或消除 hello 所造成的風險。 

我們建議您的組織使用 Azure AD Privileged Identity Management toomanage、 控制項，並監視特殊權限身分識別和 Azure AD 中的其存取 tooresources 以及 Office 365 或 Microsoft Intune 等其他 Microsoft online services。

如需詳細資訊，請參閱 [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md)。 

## <a name="see-also"></a>另請參閱
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

