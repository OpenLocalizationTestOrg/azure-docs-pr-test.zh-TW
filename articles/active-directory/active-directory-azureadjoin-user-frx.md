---
title: "安裝程式期間使用 Azure AD 的新裝置 aaaSet |Microsoft 文件"
description: "說明使用者如何在初次執行體驗期間設定 Azure AD Join 的主題。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 6afce4be7f084f1956a6f9dbddaa8def0605956d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a><span data-ttu-id="7b570-103">設定期間使用 Azure AD 設定新裝置</span><span class="sxs-lookup"><span data-stu-id="7b570-103">Set up a new device with Azure AD during Setup</span></span>
<span data-ttu-id="7b570-104">在 Windows 10 中，使用者可以 hello 初次執行體驗 (FRX) 加入其裝置 tooAzure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="7b570-104">In Windows 10, users can join their devices tooAzure Active Directory (Azure AD) in hello first-run experience (FRX).</span></span> <span data-ttu-id="7b570-105">這可讓組織 toodistribute 壓縮包裝的裝置 tootheir 員工或學生，或讓使用者選擇他們自己的裝置 (CYOD)。</span><span class="sxs-lookup"><span data-stu-id="7b570-105">This allows organizations toodistribute shrink-wrapped devices tootheir employees or students, or let them choose their own devices (CYOD).</span></span>
<span data-ttu-id="7b570-106">如果裝置上安裝 Windows 10 專業版或 Windows 10 Enterprise edition，則 hello 遇到公司擁有的裝置的預設值 toohello 安裝程序。</span><span class="sxs-lookup"><span data-stu-id="7b570-106">If either Windows 10 Professional or Windows 10 Enterprise editions is installed on a device, hello experience defaults toohello setup process for company-owned devices.</span></span>

## <a name="toojoin-a-device-tooazure-ad"></a><span data-ttu-id="7b570-107">toojoin 裝置 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="7b570-107">toojoin a device tooAzure AD</span></span>
1. <span data-ttu-id="7b570-108">當您開啟新裝置，並啟動 hello 安裝程序時，您應該會看到 hello**準備**訊息。</span><span class="sxs-lookup"><span data-stu-id="7b570-108">When you turn on your new device and start hello setup process, you should see hello  **Getting Ready** message.</span></span> <span data-ttu-id="7b570-109">請遵循您的裝置 hello 提示 tooset。</span><span class="sxs-lookup"><span data-stu-id="7b570-109">Follow hello prompts tooset up your device.</span></span>
2. <span data-ttu-id="7b570-110">首先，自訂您的地區及語言，</span><span class="sxs-lookup"><span data-stu-id="7b570-110">Start by customizing your region and language.</span></span> <span data-ttu-id="7b570-111">接著，接受 hello Microsoft 軟體授權條款。</span><span class="sxs-lookup"><span data-stu-id="7b570-111">Then accept hello Microsoft Software License Terms.</span></span>
   <span data-ttu-id="7b570-112">![自訂您的區域](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span><span class="sxs-lookup"><span data-stu-id="7b570-112">![Customize for your region](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span></span>
3. <span data-ttu-id="7b570-113">選取要用於連接 toohello 網際網路 toouse hello 網路。</span><span class="sxs-lookup"><span data-stu-id="7b570-113">Select hello network you want toouse for connecting toohello Internet.</span></span>
4. <span data-ttu-id="7b570-114">選取您是使用自己的裝置，還是公司擁有的裝置。</span><span class="sxs-lookup"><span data-stu-id="7b570-114">Select whether you're using a personal device or a company-owned device.</span></span> <span data-ttu-id="7b570-115">如果屬公司所擁有，請按一下**此裝置隸屬 toomy 組織**。</span><span class="sxs-lookup"><span data-stu-id="7b570-115">If it's company-owned, click **This device belongs toomy organization**.</span></span> <span data-ttu-id="7b570-116">這樣會啟動 hello 體驗 Azure AD Join。</span><span class="sxs-lookup"><span data-stu-id="7b570-116">This starts hello Azure AD Join experience.</span></span> <span data-ttu-id="7b570-117">如果您使用的是 Windows 10 專業版，就會看到以下畫面。</span><span class="sxs-lookup"><span data-stu-id="7b570-117">Following is a screen that you'll see if you're using Windows 10 Professional.</span></span>
   <span data-ttu-id="7b570-118"><center>
   ![[誰是這部電腦的擁有者] 畫面](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span><span class="sxs-lookup"><span data-stu-id="7b570-118"><center>
![Who owns this PC screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span></span>
5. <span data-ttu-id="7b570-119">輸入由您的組織所提供 tooyou hello 認證。</span><span class="sxs-lookup"><span data-stu-id="7b570-119">Enter hello credentials that were provided tooyou by your organization.</span></span>
   <span data-ttu-id="7b570-120"><center>
   ![登入畫面](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span><span class="sxs-lookup"><span data-stu-id="7b570-120"><center>
![Sign-in screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span></span>
6. <span data-ttu-id="7b570-121">當您輸入使用者名稱之後，系統就會在 Azure AD 中找到相符的租用戶。</span><span class="sxs-lookup"><span data-stu-id="7b570-121">After you have entered your user name, a matching tenant is located in Azure AD.</span></span> <span data-ttu-id="7b570-122">如果您是在同盟網域，您將會重新導向的 tooyour 在內部部署安全權杖服務 (STS) 伺服器--例如，Active Directory Federation Services (AD FS)。</span><span class="sxs-lookup"><span data-stu-id="7b570-122">If you are in a federated domain, you will be redirected tooyour on-premises Secure Token Service (STS) server--for example, Active Directory Federation Services (AD FS).</span></span>
7. <span data-ttu-id="7b570-123">如果您是在非同盟網域的使用者，請直接在 hello Azure AD 主控的頁面上輸入認證。</span><span class="sxs-lookup"><span data-stu-id="7b570-123">If you are a user in a non-federated domain, enter your credentials directly on hello Azure AD-hosted page.</span></span> <span data-ttu-id="7b570-124">如果您的組織之前已設定公司商標，此時您也會看到組織的標誌及支援文字。</span><span class="sxs-lookup"><span data-stu-id="7b570-124">If company branding was configured, you will also see your organization’s logo and support text.</span></span>
8. <span data-ttu-id="7b570-125">系統會提示您進行 Multi-Factor Authentication 查問。</span><span class="sxs-lookup"><span data-stu-id="7b570-125">You're prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="7b570-126">IT 系統管理員可以設定這項查問。</span><span class="sxs-lookup"><span data-stu-id="7b570-126">This challenge is configurable by an IT administrator.</span></span>
9. <span data-ttu-id="7b570-127">Azure AD 會查看該使用者/裝置是否需要在行動裝置管理 (MDM) 中註冊。</span><span class="sxs-lookup"><span data-stu-id="7b570-127">Azure AD checks whether this user/device requires enrollment in mobile device management.</span></span>
10. <span data-ttu-id="7b570-128">Windows Azure AD 中註冊 hello 組織目錄中的 hello 裝置和註冊行動裝置管理 中，如果適當的話。</span><span class="sxs-lookup"><span data-stu-id="7b570-128">Windows registers hello device in hello organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
11. <span data-ttu-id="7b570-129">如果您是受管理的使用者，Windows 會帶領您 toohello 桌面透過 hello 自動登入程序。</span><span class="sxs-lookup"><span data-stu-id="7b570-129">If you are a managed user, Windows takes you toohello desktop through hello automatic sign-in process.</span></span>
12. <span data-ttu-id="7b570-130">如果您是同盟的使用者，您會被導向 toohello Windows 登入畫面 tooenter 您的認證。</span><span class="sxs-lookup"><span data-stu-id="7b570-130">If you are a federated user, you are directed toohello Windows sign-in screen tooenter your credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="7b570-131">若要加入內部部署 Windows Server Active Directory 網域中 hello Windows 不支援全新的體驗。</span><span class="sxs-lookup"><span data-stu-id="7b570-131">Joining an on-premises Windows Server Active Directory domain in hello Windows out-of-box experience is not supported.</span></span> <span data-ttu-id="7b570-132">因此，如果您計劃 toojoin 電腦 tooa 網域，您應該選取 hello 連結**使用本機帳戶設定 windows<**改為。</span><span class="sxs-lookup"><span data-stu-id="7b570-132">Therefore, if you plan toojoin a computer tooa domain, you should select hello link **Set up Windows with a local account** instead.</span></span> <span data-ttu-id="7b570-133">然後您可以在您的電腦上聯結 hello 網域從 hello 設定，為 「 您已經完成之前。</span><span class="sxs-lookup"><span data-stu-id="7b570-133">You can then join hello domain from hello settings on your computer as you’ve done before.</span></span>
> 
> 

## <a name="additional-information"></a><span data-ttu-id="7b570-134">其他資訊</span><span class="sxs-lookup"><span data-stu-id="7b570-134">Additional information</span></span>
* [<span data-ttu-id="7b570-135">Hello 企業版的 Windows 10： 工作的方式 toouse 裝置</span><span class="sxs-lookup"><span data-stu-id="7b570-135">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="7b570-136">擴充功能 tooWindows 10 裝置透過 Azure Active Directory 加入雲端</span><span class="sxs-lookup"><span data-stu-id="7b570-136">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="7b570-137">透過 Microsoft Passport 不需要密碼就能驗證身分識別</span><span class="sxs-lookup"><span data-stu-id="7b570-137">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="7b570-138">了解適用於 Azure AD Join 的使用案例</span><span class="sxs-lookup"><span data-stu-id="7b570-138">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="7b570-139">連接已加入網域裝置 tooAzure AD 進行 Windows 10 體驗</span><span class="sxs-lookup"><span data-stu-id="7b570-139">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="7b570-140">設定 Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="7b570-140">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

