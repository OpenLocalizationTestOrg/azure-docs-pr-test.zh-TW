---
title: "從 [設定] 使用 Azure AD 設定 Windows 10 裝置 | Microsoft Docs"
description: "說明使用者要如何透過 [設定] 功能表加入 Azure AD。"
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 5a3963f16b471ad1ca8681b22a1a027935400465
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="6a562-103">從 [設定] 使用 Azure AD 設定 Windows 10 裝置</span><span class="sxs-lookup"><span data-stu-id="6a562-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="6a562-104">如果您已經在使用 Windows 7 或 Windows 8，且您的電腦或裝置已升級為 Windows 10，您可以透過 [設定] 功能表加入 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="6a562-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded to Windows 10, you can join to Azure Active Directory (Azure AD) through the Settings menu.</span></span>

## <a name="to-join-to-azure-ad-from-the-settings-menu"></a><span data-ttu-id="6a562-105">從 [設定] 功能表加入 Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a562-105">To join to Azure AD from the Settings menu</span></span>
1. <span data-ttu-id="6a562-106">從 [開始] 功能表中，按一下 [設定] 常用鍵。</span><span class="sxs-lookup"><span data-stu-id="6a562-106">From the **Start** menu, click the **Settings** charm.</span></span>
2. <span data-ttu-id="6a562-107">從 [設定] 中選取 [系統]->[關於]->[加入 Azure AD]。</span><span class="sxs-lookup"><span data-stu-id="6a562-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="6a562-108"><center>
   ![從設定功能表加入 Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span><span class="sxs-lookup"><span data-stu-id="6a562-108"><center>
![Join Azure AD from the Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="6a562-109">按一下 Azure AD Join 訊息視窗中的 [繼續]  。</span><span class="sxs-lookup"><span data-stu-id="6a562-109">Click **Continue** in the Azure AD Join message window.</span></span>
   
   <span data-ttu-id="6a562-110"><center>
   ![加入 Azure AD 訊息視窗](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span><span class="sxs-lookup"><span data-stu-id="6a562-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="6a562-111">提供您的登入認證。</span><span class="sxs-lookup"><span data-stu-id="6a562-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="6a562-112">此登入體驗將會包含完成驗證所需的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="6a562-112">This sign-in experience will include all the steps that are required to complete authentication.</span></span> <span data-ttu-id="6a562-113">如果您屬於同盟租用戶，您的管理員會提供由您組織託管的同盟體驗。</span><span class="sxs-lookup"><span data-stu-id="6a562-113">If you are part of a federated tenant, your administrator will provide you with the federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="6a562-114"><center>
   ![提供登入認證](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span><span class="sxs-lookup"><span data-stu-id="6a562-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="6a562-115">如果您的組織已針對 Azure AD 的加入程序設定了 Azure Multi-Factor Authentication，則您必須提供第二個要素才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="6a562-115">If your organization has configured Azure Multi-Factor Authentication for joining to Azure AD, provide the second factor before proceeding.</span></span>
6. <span data-ttu-id="6a562-116">按一下 [允許此裝置成為受管理] 畫面中的 [接受]。</span><span class="sxs-lookup"><span data-stu-id="6a562-116">Click **Accept** on the **Allow this device to be managed** screen.</span></span>
7. <span data-ttu-id="6a562-117">您應該會看到此訊息「您的裝置現在已加入位於 Azure AD 中的貴組織」。</span><span class="sxs-lookup"><span data-stu-id="6a562-117">You should see the message "Your device is now joined to your organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="6a562-118">其他資訊</span><span class="sxs-lookup"><span data-stu-id="6a562-118">Additional information</span></span>
* [<span data-ttu-id="6a562-119">了解適用於 Azure AD Join 的使用案例</span><span class="sxs-lookup"><span data-stu-id="6a562-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="6a562-120">將已加入網域裝置連接到 Azure AD 以體驗 Windows 10</span><span class="sxs-lookup"><span data-stu-id="6a562-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="6a562-121">設定 Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="6a562-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="6a562-122">透過 Microsoft Passport 不需要密碼就能驗證身分識別</span><span class="sxs-lookup"><span data-stu-id="6a562-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

