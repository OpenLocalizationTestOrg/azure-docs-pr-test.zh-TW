---
title: "Azure Active Directory Identity Protection 偵測到的弱點 | Microsoft Docs"
description: "Azure Active Directory Identity Protection 偵測到的弱點概觀。"
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
ms.openlocfilehash: 364873ff54099a6123e40b12e819d1745751f285
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="23557-104">Azure Active Directory Identity Protection 偵測到的弱點</span><span class="sxs-lookup"><span data-stu-id="23557-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="23557-105">弱點是您的環境中攻擊者可以利用的弱點。</span><span class="sxs-lookup"><span data-stu-id="23557-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="23557-106">我們建議您處理這些弱點，以改善組織的安全性狀態，並防止攻擊者利用這些弱點。</span><span class="sxs-lookup"><span data-stu-id="23557-106">We recommend that you address these vulnerabilities to improve the security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="23557-107">![弱點](./media/active-directory-identityprotection-vulnerabilities/101.png "弱點")</span><span class="sxs-lookup"><span data-stu-id="23557-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="23557-108">下列各節概述 Identity Protection 所報告的弱點。</span><span class="sxs-lookup"><span data-stu-id="23557-108">The following sections provide you with an overview of the vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="23557-109">未設定 Multi-Factor Authentication 註冊</span><span class="sxs-lookup"><span data-stu-id="23557-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="23557-110">此弱點可協助您控制組織中部署的 Azure Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="23557-110">This vulnerability helps you control the deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="23557-111">Azure Multi-Factor Authentication 會為使用者驗證提供第二層安全性。</span><span class="sxs-lookup"><span data-stu-id="23557-111">Azure multi-factor authentication provides a second layer of security to user authentication.</span></span> <span data-ttu-id="23557-112">這有助於保護對資料與應用程式的存取，同時可以滿足使用者對簡單登入程序的需求。</span><span class="sxs-lookup"><span data-stu-id="23557-112">It helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="23557-113">它可以透過一些簡單的驗證選項 (例如電話、文字訊息，或行動應用程式通知或驗證代碼，以及第三方 OATH 權杖) 來提供強大的驗證功能。</span><span class="sxs-lookup"><span data-stu-id="23557-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="23557-114">建議您要求對使用者登入進行 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="23557-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins.</span></span> <span data-ttu-id="23557-115">在 Identity Protection 提供的以風險為基礎的條件式存取原則中，Multi-Factor Authentication 扮演關鍵角色。</span><span class="sxs-lookup"><span data-stu-id="23557-115">Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="23557-116">如需詳細資訊，請參閱 [什麼是 Azure Multi-Factor Authentication？](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="23557-116">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="23557-117">未受管理的雲端應用程式</span><span class="sxs-lookup"><span data-stu-id="23557-117">Unmanaged cloud apps</span></span>
<span data-ttu-id="23557-118">此弱點可協助您識別組織中未受管理的雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="23557-118">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="23557-119">在現代企業中，IT 部門通常不會知道組織中的使用者用於進行工作的所有雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="23557-119">In modern enterprises, IT departments are often unaware of all the cloud applications that users in their organization are using to do their work.</span></span> <span data-ttu-id="23557-120">很容易知道為什麼系統管理員必須對未經授權存取公司資料、可能的資料外洩和其他安全性風險有所顧慮。</span><span class="sxs-lookup"><span data-stu-id="23557-120">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="23557-121">我們建議您的組織部署 Cloud App Discovery 來探索未受管理的雲端應用程式，以及管理這些使用 Azure Active Directory 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="23557-121">We recommend that your organization deploy Cloud App Discovery to discover unmanaged cloud applications, and to manage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="23557-122">如需詳細資訊，請參閱 [使用 Cloud App Discovery 尋找未受管理的雲端應用程式](active-directory-cloudappdiscovery-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="23557-122">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="23557-123">來自 Privileged Identity Management 的安全性警示</span><span class="sxs-lookup"><span data-stu-id="23557-123">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="23557-124">此弱點可協助您找出並解決有關您組織中特殊權限身分識別的警示。</span><span class="sxs-lookup"><span data-stu-id="23557-124">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="23557-125">若要讓使用者能夠執行特殊權限作業，組織必須賦予使用者在 Azure AD、Azure 或 Office 365 資源或其他 SaaS 應用程式中的暫時或永久特殊權限存取權。</span><span class="sxs-lookup"><span data-stu-id="23557-125">To enable users to carry out privileged operations, organizations need to grant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="23557-126">這些特殊權限的使用者會增加您組織的受攻擊面。</span><span class="sxs-lookup"><span data-stu-id="23557-126">Each of these privileged users increases the attack surface of your organization.</span></span> <span data-ttu-id="23557-127">此弱點可協助您識別具有非必要特殊權限存取權的使用者，並採取適當的行動來減少或消除其所造成的風險。</span><span class="sxs-lookup"><span data-stu-id="23557-127">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action to reduce or eliminate the risk they pose.</span></span> 

<span data-ttu-id="23557-128">建議您的組織使用 Azure AD Privileged Identity Management 來管理、控制和監視特殊權限身分識別，以及其在 Azure AD 和其他 Microsoft 線上服務 (如 Office 365 或 Microsoft Intune) 中的資源存取權。</span><span class="sxs-lookup"><span data-stu-id="23557-128">We recommend that your organization uses Azure AD Privileged Identity Management to manage, control, and monitor privileged identities and their access to resources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="23557-129">如需詳細資訊，請參閱 [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="23557-129">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="23557-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="23557-130">See also</span></span>
* [<span data-ttu-id="23557-131">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="23557-131">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

