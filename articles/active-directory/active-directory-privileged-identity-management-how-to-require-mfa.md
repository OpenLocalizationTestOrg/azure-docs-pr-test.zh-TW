---
title: "aaaHow toorequire 多重要素驗證 |Microsoft 文件"
description: "了解如何 toorequire multi-factor authentication (MFA) 特殊權限身分識別與 hello Azure Active Directory Privileged Identity Management 延伸模組。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1e3dc4ad-3a6a-4a52-8417-3ca4f84ae05c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: c08fad9dc80c09a14a4bd7497da4942fa227c3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-mfa-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="31cbb-103">如何在 Azure AD Privileged Identity Management MFA toorequire</span><span class="sxs-lookup"><span data-stu-id="31cbb-103">How toorequire MFA in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="31cbb-104">建議您針對所有系統管理員都要求進行多重要素驗證 (MFA)。</span><span class="sxs-lookup"><span data-stu-id="31cbb-104">We recommend that you require multi-factor authentication (MFA) for all of your administrators.</span></span> <span data-ttu-id="31cbb-105">這可降低攻擊者危害 tooa 密碼到期 hello 風險。</span><span class="sxs-lookup"><span data-stu-id="31cbb-105">This reduces hello risk of an attack due tooa compromised password.</span></span>

<span data-ttu-id="31cbb-106">您可以要求使用者在登入時完成 MFA 挑戰。</span><span class="sxs-lookup"><span data-stu-id="31cbb-106">You can require that users complete an MFA challenge when they sign in.</span></span> <span data-ttu-id="31cbb-107">hello 部落格文章[Office 365 和 azure MFA 的 MFA](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/)比較與 hello hello Microsoft Azure Multi-factor Authentication 供應項目中所包含的功能包含 Office 和 Azure 訂用帳戶的內容。</span><span class="sxs-lookup"><span data-stu-id="31cbb-107">hello blog post [MFA for Office 365 and MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/) compares what is included in Office and Azure subscriptions, with hello features contained in hello Microsoft Azure Multi-Factor Authentication offering.</span></span>

<span data-ttu-id="31cbb-108">您也可以要求使用者在啟用 Azure AD PIM 中的角色時，完成 MFA 挑戰。</span><span class="sxs-lookup"><span data-stu-id="31cbb-108">You can also require that users complete an MFA challenge when they activate a role in Azure AD PIM.</span></span> <span data-ttu-id="31cbb-109">如此一來，如果它們登入時，hello 使用者未完成的 MFA 挑戰，就會提示的 toodo 是由 PIM。</span><span class="sxs-lookup"><span data-stu-id="31cbb-109">This way, if hello user didn't complete an MFA challenge when they signed in, they will be prompted toodo so by PIM.</span></span>

## <a name="requiring-mfa-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="31cbb-110">在 Azure AD Privileged Identity Management 中強制啟用 MFA</span><span class="sxs-lookup"><span data-stu-id="31cbb-110">Requiring MFA in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="31cbb-111">當您以特殊權限角色管理員的身分管理 PIM 中的身分識別時，您可能會看到建議特殊權限帳戶使用 MFA 的警示。</span><span class="sxs-lookup"><span data-stu-id="31cbb-111">When you manage identities in PIM as a privileged role administrator, you may see alerts that recommend MFA for privileged accounts.</span></span> <span data-ttu-id="31cbb-112">按一下 [安全性] hello hello PIM 儀表板和的新刀鋒視窗中的警示將會開啟 hello 應該需要 MFA 的系統管理員帳戶的清單。</span><span class="sxs-lookup"><span data-stu-id="31cbb-112">Click hello security alert in hello PIM dashboard, and a new blade will open with a list of hello administrator accounts that should require MFA.</span></span>  <span data-ttu-id="31cbb-113">您可以選取多個角色，然後按一下hello 要求 MFA**修正**] 按鈕，或者您可以按一下 [hello 省略符號 [下一步 tooindividual 角色，然後按一下hello**修正**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="31cbb-113">You can require MFA by selecting multiple roles and then clicking hello **Fix** button, or you can click hello ellipses next tooindividual roles and then click hello **Fix** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31cbb-114">現在，Azure MFA 只適用於使用工作或學校帳戶，沒有 Microsoft 帳戶 （通常是個人的帳戶中使用過 toosign tooMicrosoft 服務類似 Skype、 Xbox、 Outlook.com 等。），以滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="31cbb-114">Right now, Azure MFA only works with work or school accounts, not Microsoft accounts (usually a personal account that's used toosign in tooMicrosoft services like Skype, Xbox, Outlook.com, etc.).</span></span> <span data-ttu-id="31cbb-115">因為這個緣故，使用 Microsoft 帳戶的任何人都不能合格的系統管理員，因為它們不能使用 MFA tooactivate 及其角色。</span><span class="sxs-lookup"><span data-stu-id="31cbb-115">Because of this, anyone using a Microsoft account can't be an eligible admin because they can't use MFA tooactivate their roles.</span></span> <span data-ttu-id="31cbb-116">如果這些使用者需要 toocontinue 管理使用 Microsoft 帳戶的工作負載，提高其 toopermanent 系統管理員現在。</span><span class="sxs-lookup"><span data-stu-id="31cbb-116">If these users need toocontinue managing workloads using a Microsoft account, elevate them toopermanent administrators for now.</span></span>
> 
> 

<span data-ttu-id="31cbb-117">此外，您可以變更特定角色的 hello MFA 需求 hello hello PIM 儀表板的 [角色] 區段中按一下。</span><span class="sxs-lookup"><span data-stu-id="31cbb-117">Additionally, you can change hello MFA requirement for a specific role by clicking on it in hello Roles section of hello PIM dashboard.</span></span> <span data-ttu-id="31cbb-118">然後按一下 上**設定**hello 角色 刀鋒視窗，然後選取 在**啟用**下多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="31cbb-118">Then, click on **Settings** in hello role blade and then selecting **Enable** under multi-factor authentication.</span></span>

## <a name="how-azure-ad-pim-validates-mfa"></a><span data-ttu-id="31cbb-119">Azure AD PIM 如何驗證 MFA</span><span class="sxs-lookup"><span data-stu-id="31cbb-119">How Azure AD PIM validates MFA</span></span>
<span data-ttu-id="31cbb-120">在使用者啟用角色時有兩個選項可用來驗證 MFA。</span><span class="sxs-lookup"><span data-stu-id="31cbb-120">There are two options for validating MFA when a user activates a role.</span></span>

<span data-ttu-id="31cbb-121">hello 簡單的選項是 toorely 上 Azure MFA 的使用者要啟用特殊權限的角色。</span><span class="sxs-lookup"><span data-stu-id="31cbb-121">hello simplest option is toorely on Azure MFA for users who are activating a privileged role.</span></span> <span data-ttu-id="31cbb-122">toodo，第一次檢查那些使用者授權，如有必要，且已註冊的 Azure MFA。</span><span class="sxs-lookup"><span data-stu-id="31cbb-122">toodo this, first check that those users are licensed, if necessary, and have registered for Azure MFA.</span></span> <span data-ttu-id="31cbb-123">有關如何 toodo 這種[開始使用 Azure Multi-factor Authentication hello 定域機組中](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)。</span><span class="sxs-lookup"><span data-stu-id="31cbb-123">More information on how toodo this is in [Getting started with Azure Multi-Factor Authentication in hello cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span> <span data-ttu-id="31cbb-124">它是建議，但並非必要，登入時，設定這些使用者的 Azure AD tooenforce MFA。</span><span class="sxs-lookup"><span data-stu-id="31cbb-124">It is recommended, but not required, that you configure Azure AD tooenforce MFA for these users when they sign in.</span></span> <span data-ttu-id="31cbb-125">這是因為 hello MFA 檢查將會由 Azure AD PIM 本身。</span><span class="sxs-lookup"><span data-stu-id="31cbb-125">This is because hello MFA checks will be made by Azure AD PIM itself.</span></span>

<span data-ttu-id="31cbb-126">或者，如果使用者驗證內部部署，您可以讓您的身分識別提供者負責進行 MFA。</span><span class="sxs-lookup"><span data-stu-id="31cbb-126">Alternatively, if users authenticate on-premises you can have your identity provider be responsible for MFA.</span></span> <span data-ttu-id="31cbb-127">例如，如果您已設定 AD Federation Services toorequire 智慧卡驗證，才能存取 Azure AD，[與 Azure Multi-factor Authentication Server 和 AD FS 保護雲端資源](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md)包含指示適用於設定 AD FS toosend 宣告 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="31cbb-127">For example, if you have configured AD Federation Services toorequire smartcard-based authentication before accessing Azure AD, [Securing cloud resources with Azure Multi-Factor Authentication and AD FS](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md) includes instructions for configuring AD FS toosend claims tooAzure AD.</span></span> <span data-ttu-id="31cbb-128">當使用者嘗試 tooactivate 角色時，Azure AD PIM 將接受的 MFA 已經過驗證 hello 使用者在收到 hello 適當的宣告。</span><span class="sxs-lookup"><span data-stu-id="31cbb-128">When a user tries tooactivate a role, Azure AD PIM will accept that MFA has already been validated for hello user once it receives hello appropriate claims.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="31cbb-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="31cbb-129">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

