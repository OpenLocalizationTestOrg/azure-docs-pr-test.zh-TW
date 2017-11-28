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
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="cb76e-104">Azure Active Directory Identity Protection 偵測到的弱點</span><span class="sxs-lookup"><span data-stu-id="cb76e-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="cb76e-105">弱點是您的環境中攻擊者可以利用的弱點。</span><span class="sxs-lookup"><span data-stu-id="cb76e-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="cb76e-106">我們建議您解決您的組織，這些弱點 tooimprove hello 安全性狀態，並防止攻擊者利用它們。</span><span class="sxs-lookup"><span data-stu-id="cb76e-106">We recommend that you address these vulnerabilities tooimprove hello security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="cb76e-107">![弱點](./media/active-directory-identityprotection-vulnerabilities/101.png "弱點")</span><span class="sxs-lookup"><span data-stu-id="cb76e-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="cb76e-108">hello 下列章節提供您的識別身分保護所報告的 hello 弱點的概觀。</span><span class="sxs-lookup"><span data-stu-id="cb76e-108">hello following sections provide you with an overview of hello vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="cb76e-109">未設定 Multi-Factor Authentication 註冊</span><span class="sxs-lookup"><span data-stu-id="cb76e-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="cb76e-110">這可協助您控制組織中的 hello 部署的 Azure Multi-factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="cb76e-110">This vulnerability helps you control hello deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="cb76e-111">Azure 多因素驗證提供安全性 toouser 驗證的第二層。</span><span class="sxs-lookup"><span data-stu-id="cb76e-111">Azure multi-factor authentication provides a second layer of security toouser authentication.</span></span> <span data-ttu-id="cb76e-112">它可協助保護存取 toodata 和應用程式，同時滿足簡單登入程序的使用者需求。</span><span class="sxs-lookup"><span data-stu-id="cb76e-112">It helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="cb76e-113">它可以透過一些簡單的驗證選項 (例如電話、文字訊息，或行動應用程式通知或驗證代碼，以及第三方 OATH 權杖) 來提供強大的驗證功能。</span><span class="sxs-lookup"><span data-stu-id="cb76e-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="cb76e-114">建議您要求對使用者登入進行 Multi-Factor Authentication。在 Identity Protection 提供的以風險為基礎的條件式存取原則中，Multi-Factor Authentication 扮演關鍵角色。</span><span class="sxs-lookup"><span data-stu-id="cb76e-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins. Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="cb76e-115">如需詳細資訊，請參閱 [什麼是 Azure Multi-Factor Authentication？](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="cb76e-115">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="cb76e-116">未受管理的雲端應用程式</span><span class="sxs-lookup"><span data-stu-id="cb76e-116">Unmanaged cloud apps</span></span>
<span data-ttu-id="cb76e-117">此弱點可協助您識別組織中未受管理的雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="cb76e-117">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="cb76e-118">現代企業 IT 部門通常不知道其組織中的使用者工作使用 toodo 所有 hello 雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="cb76e-118">In modern enterprises, IT departments are often unaware of all hello cloud applications that users in their organization are using toodo their work.</span></span> <span data-ttu-id="cb76e-119">它是簡單 toosee 為什麼系統管理員就必須考慮未經授權的存取 toocorporate 資料、 可能的資料流失和其他安全性風險。</span><span class="sxs-lookup"><span data-stu-id="cb76e-119">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="cb76e-120">我們建議您的組織部署 Cloud App Discovery toodiscover unmanaged 雲端應用程式和 toomanage 這些應用程式使用 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="cb76e-120">We recommend that your organization deploy Cloud App Discovery toodiscover unmanaged cloud applications, and toomanage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="cb76e-121">如需詳細資訊，請參閱 [使用 Cloud App Discovery 尋找未受管理的雲端應用程式](active-directory-cloudappdiscovery-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="cb76e-121">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="cb76e-122">來自 Privileged Identity Management 的安全性警示</span><span class="sxs-lookup"><span data-stu-id="cb76e-122">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="cb76e-123">此弱點可協助您找出並解決有關您組織中特殊權限身分識別的警示。</span><span class="sxs-lookup"><span data-stu-id="cb76e-123">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="cb76e-124">tooenable 特殊權限作業使用者 toocarry，組織需要 toogrant 使用者在 Azure AD 中的暫時或永久特殊權限存取 Azure 或 Office 365 資源或其他 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cb76e-124">tooenable users toocarry out privileged operations, organizations need toogrant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="cb76e-125">每個組織這些權限的使用者會增加 hello 受攻擊面。</span><span class="sxs-lookup"><span data-stu-id="cb76e-125">Each of these privileged users increases hello attack surface of your organization.</span></span> <span data-ttu-id="cb76e-126">這可協助您識別使用者透過不需要特殊權限的存取權，並採取適當的動作 tooreduce 或消除 hello 所造成的風險。</span><span class="sxs-lookup"><span data-stu-id="cb76e-126">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action tooreduce or eliminate hello risk they pose.</span></span> 

<span data-ttu-id="cb76e-127">我們建議您的組織使用 Azure AD Privileged Identity Management toomanage、 控制項，並監視特殊權限身分識別和 Azure AD 中的其存取 tooresources 以及 Office 365 或 Microsoft Intune 等其他 Microsoft online services。</span><span class="sxs-lookup"><span data-stu-id="cb76e-127">We recommend that your organization uses Azure AD Privileged Identity Management toomanage, control, and monitor privileged identities and their access tooresources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="cb76e-128">如需詳細資訊，請參閱 [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="cb76e-128">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="cb76e-129">另請參閱</span><span class="sxs-lookup"><span data-stu-id="cb76e-129">See also</span></span>
* [<span data-ttu-id="cb76e-130">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="cb76e-130">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

