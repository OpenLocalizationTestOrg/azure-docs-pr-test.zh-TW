---
title: "為使用者設定 Azure AD Join| Microsoft Docs"
description: "說明系統管理員如何設定 Azure AD Join 以用於內部部署目錄及裝置註冊。"
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: c37adc2654f7e931fdda22627e4a6ece2789fd86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a><span data-ttu-id="1f38d-103">在組織中設定 Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="1f38d-103">Setting up Azure AD Join in your organization</span></span>
<span data-ttu-id="1f38d-104">設定 Azure Active Directory Join (Azure AD Join) 之前，您需要將使用者的內部部署目錄同步處理至雲端，或在 Azure AD 中手動建立受管理的帳戶。</span><span class="sxs-lookup"><span data-stu-id="1f38d-104">Before you set up Azure Active Directory Join (Azure AD Join), you need to either sync up your on-premises directory of users to the cloud or manually create managed accounts in Azure AD.</span></span>

<span data-ttu-id="1f38d-105">如需將內部部署使用者同步處理至 Azure AD 的詳細指示，請參閱 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="1f38d-105">Detailed instructions for syncing your on-premises users to Azure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="1f38d-106">若要在 Azure AD 中手動建立和管理使用者，請參閱 [Azure AD 中的使用者管理](https://msdn.microsoft.com/library/azure/hh967609.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1f38d-106">To manually create and manage users in Azure AD, refer to [User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span></span>

## <a name="set-up-device-registration"></a><span data-ttu-id="1f38d-107">設定裝置註冊</span><span class="sxs-lookup"><span data-stu-id="1f38d-107">Set up device registration</span></span>
1. <span data-ttu-id="1f38d-108">以系統管理員身分登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="1f38d-108">Log on to the Azure portal as an administrator.</span></span>
2. <span data-ttu-id="1f38d-109">在左窗格中選取 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="1f38d-109">On the left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="1f38d-110">在 [目錄]  索引標籤中，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="1f38d-110">On the **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="1f38d-111">選取 [設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1f38d-111">Select the **Configure** tab.</span></span>
5. <span data-ttu-id="1f38d-112">移至 [裝置]  區段。</span><span class="sxs-lookup"><span data-stu-id="1f38d-112">Go to the **Devices** section.</span></span>
6. <span data-ttu-id="1f38d-113">在 [裝置]  索引標籤上，設定下列內容：</span><span class="sxs-lookup"><span data-stu-id="1f38d-113">On the **devices** tab, set the following:</span></span>  
   * <span data-ttu-id="1f38d-114">**每位使用者的裝置數目上限**：選取使用者可在 Azure AD 中擁有的裝置數目上限。</span><span class="sxs-lookup"><span data-stu-id="1f38d-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select the maximum number of devices that a user can have in Azure AD.</span></span>  <span data-ttu-id="1f38d-115">如果使用者達到此配額限制，則在移除一或多個現有的裝置之前，將無法新增其他裝置。</span><span class="sxs-lookup"><span data-stu-id="1f38d-115">If a user reaches this quota, they will not be able to add additional devices until one or more of their existing devices are removed.</span></span>
   * <span data-ttu-id="1f38d-116">**需要 Multi-factor Auth 才能聯結裝置**：設定使用者是否需要提供第二個驗證要素，才能將其裝置加入 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="1f38d-116">**REQUIRE MULTI-FACTOR AUTH TO JOIN DEVICES**: Set whether users are required to provide a second authentication factor to join their device to Azure AD.</span></span> <span data-ttu-id="1f38d-117">如需 Azure Multi-Factor Authentication 的詳細資訊，請參閱 [開始在雲端中使用 Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)。</span><span class="sxs-lookup"><span data-stu-id="1f38d-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in the cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>
   * <span data-ttu-id="1f38d-118">**使用者可以將裝置加入 Azure AD**：選取允許將裝置加入 Azure AD 的使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="1f38d-118">**USERS MAY AZURE AD JOIN DEVICES**: Select the users and groups that are allowed to join devices to Azure AD.</span></span>
   * <span data-ttu-id="1f38d-119">**加入 Azure AD 之裝置的其他系統管理員**：使用 Azure AD Premium 或 Enterprise Mobility Suite (EMS)，您可以選擇要為哪些使用者授與裝置的本機系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="1f38d-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or the Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights to the device.</span></span> <span data-ttu-id="1f38d-120">全域系統管理員和裝置擁有者預設會授與本機系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="1f38d-120">Global administrators and device owners are granted local administrator rights by default.</span></span>

<span data-ttu-id="1f38d-121"><center>![設定裝置註冊](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span><span class="sxs-lookup"><span data-stu-id="1f38d-121"><center>![Set up device regisration](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span></span>

<span data-ttu-id="1f38d-122">為使用者設定 Azure AD Join 之後，他們就能透過其公司或個人裝置連接到 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="1f38d-122">After you set up Azure AD Join for your users, they can connect to Azure AD through their corporate or personal devices.</span></span>

<span data-ttu-id="1f38d-123">以下是您可以用來讓使用者能夠設定 Azure AD Join 的三種案例：</span><span class="sxs-lookup"><span data-stu-id="1f38d-123">Following are the three scenarios you can use to enable your users to set up Azure AD Join:</span></span>

* <span data-ttu-id="1f38d-124">使用者可將公司擁有的裝置直接加入 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="1f38d-124">Users join a company-owned device directly to Azure AD.</span></span>
* <span data-ttu-id="1f38d-125">使用者可將公司擁有的裝置網域加入內部部署 Active Directory，然後將裝置擴充至 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="1f38d-125">Users domain-join a company-owned device to the on-premises Active Directory and then extend the device to Azure AD.</span></span>
* <span data-ttu-id="1f38d-126">使用者可在個人裝置上將工作或學校帳戶新增至 Windows</span><span class="sxs-lookup"><span data-stu-id="1f38d-126">Users add work or school accounts to Windows on a personal device</span></span>

## <a name="additional-information"></a><span data-ttu-id="1f38d-127">其他資訊</span><span class="sxs-lookup"><span data-stu-id="1f38d-127">Additional information</span></span>
* [<span data-ttu-id="1f38d-128">適合企業使用的 Windows 10：使用裝置工作的方式</span><span class="sxs-lookup"><span data-stu-id="1f38d-128">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="1f38d-129">透過 Azure Active Directory Join 擴充 Windows 10 裝置的雲端功能</span><span class="sxs-lookup"><span data-stu-id="1f38d-129">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="1f38d-130">了解適用於 Azure AD Join 的使用案例</span><span class="sxs-lookup"><span data-stu-id="1f38d-130">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="1f38d-131">將已加入網域裝置連接到 Azure AD 以體驗 Windows 10</span><span class="sxs-lookup"><span data-stu-id="1f38d-131">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="1f38d-132">設定 Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="1f38d-132">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

