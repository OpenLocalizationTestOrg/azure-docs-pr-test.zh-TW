---
title: "將個人裝置加入至您的組織 | Microsoft Docs"
description: "說明使用者要如何向他們的公司網路註冊其個人的 Windows 10 裝置，同時也提供 BYOD 案例的部署步驟。"
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 9f3d38f5-1cfd-43d4-97da-4fed1255a1ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 9418365ea18b065551448742b21c8b17a1749fc8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-personal-device-to-your-organization"></a><span data-ttu-id="21049-103">將個人裝置加入至您的組織</span><span class="sxs-lookup"><span data-stu-id="21049-103">Join a personal device to your organization</span></span>
## <a name="to-join-a-windows-10-device-to-your-organization"></a><span data-ttu-id="21049-104">將 Windows 10 裝置加入至您的組織</span><span class="sxs-lookup"><span data-stu-id="21049-104">To join a Windows 10 device to your organization</span></span>
1. <span data-ttu-id="21049-105">在 [開始] 功能表中，選取 [設定]。</span><span class="sxs-lookup"><span data-stu-id="21049-105">From the **Start** menu, select **Settings**.</span></span>
2. <span data-ttu-id="21049-106">選取 [帳戶]，然後按一下 [您的帳戶]。</span><span class="sxs-lookup"><span data-stu-id="21049-106">Select **Accounts**, and then click **Your account**.</span></span>
3. <span data-ttu-id="21049-107">按一下 [ **加入工作或學校帳戶**]，然後在您的組織帳戶中進行輸入。</span><span class="sxs-lookup"><span data-stu-id="21049-107">Click **Add Work or School account**, and then type in your organizational account.</span></span>
4. <span data-ttu-id="21049-108">在您組織的登入頁面上，輸入您的使用者名稱和密碼，然後按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="21049-108">On the sign-in page for your organization, enter your user name and password, and then click **OK**.</span></span>
5. <span data-ttu-id="21049-109">接著系統會提示您完成多重要素驗證挑戰。</span><span class="sxs-lookup"><span data-stu-id="21049-109">You will be prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="21049-110">(這項挑戰可由 IT 管理員設定)。</span><span class="sxs-lookup"><span data-stu-id="21049-110">(This challenge is configurable by an IT administrator.)</span></span>
6. <span data-ttu-id="21049-111">Azure Active Directory (Azure AD) 會檢查這個裝置是否需要註冊行動裝置管理。</span><span class="sxs-lookup"><span data-stu-id="21049-111">Azure Active Directory (Azure AD) checks whether the device requires mobile device management enrollment.</span></span>
7. <span data-ttu-id="21049-112">接著 Windows 會在 Azure AD 的組織目錄中註冊裝置，並註冊行動裝置管理 (如果適用)。</span><span class="sxs-lookup"><span data-stu-id="21049-112">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
8. <span data-ttu-id="21049-113">如果您是受管理的使用者，Windows 會透過自動登入將您導向桌面。</span><span class="sxs-lookup"><span data-stu-id="21049-113">If you are a managed user, Windows takes you to the desktop through the automatic sign-in.</span></span>
9. <span data-ttu-id="21049-114">如果您是同盟使用者，便會將您導向 Windows 登入畫面，以輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="21049-114">If you are a federated user, you will be taken to a Windows sign-in screen to enter your credentials.</span></span>

## <a name="additional-information"></a><span data-ttu-id="21049-115">其他資訊</span><span class="sxs-lookup"><span data-stu-id="21049-115">Additional information</span></span>
* [<span data-ttu-id="21049-116">適合企業使用的 Windows 10：使用裝置工作的方式</span><span class="sxs-lookup"><span data-stu-id="21049-116">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="21049-117">透過 Azure Active Directory Join 擴充 Windows 10 裝置的雲端功能</span><span class="sxs-lookup"><span data-stu-id="21049-117">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="21049-118">透過 Microsoft Passport 不需要密碼就能驗證身分識別</span><span class="sxs-lookup"><span data-stu-id="21049-118">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="21049-119">了解適用於 Azure AD Join 的使用案例</span><span class="sxs-lookup"><span data-stu-id="21049-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="21049-120">將已加入網域裝置連接到 Azure AD 以體驗 Windows 10</span><span class="sxs-lookup"><span data-stu-id="21049-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="21049-121">設定 Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="21049-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

