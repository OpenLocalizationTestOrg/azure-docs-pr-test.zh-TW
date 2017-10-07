---
title: "設定從 Azure AD 與 Windows 10 裝置的 aaaSet |Microsoft 文件"
description: "說明使用者如何加入 tooAzure AD 透過 hello 設定功能表。"
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
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="895d2-103">從 [設定] 使用 Azure AD 設定 Windows 10 裝置</span><span class="sxs-lookup"><span data-stu-id="895d2-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="895d2-104">如果您已經使用 Windows 7 或 Windows 8 與電腦或裝置已升級的 tooWindows 10，您可以加入 tooAzure Active Directory (Azure AD) 透過 hello 設定功能表。</span><span class="sxs-lookup"><span data-stu-id="895d2-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded tooWindows 10, you can join tooAzure Active Directory (Azure AD) through hello Settings menu.</span></span>

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a><span data-ttu-id="895d2-105">toojoin tooAzure AD hello 設定 功能表</span><span class="sxs-lookup"><span data-stu-id="895d2-105">toojoin tooAzure AD from hello Settings menu</span></span>
1. <span data-ttu-id="895d2-106">從 hello**啟動**功能表上，按一下 hello**設定**常用鍵。</span><span class="sxs-lookup"><span data-stu-id="895d2-106">From hello **Start** menu, click hello **Settings** charm.</span></span>
2. <span data-ttu-id="895d2-107">從 [設定] 中選取 [系統]->[關於]->[加入 Azure AD]。</span><span class="sxs-lookup"><span data-stu-id="895d2-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="895d2-108"><center>
   ![加入 Azure AD 設定 功能表中 hello](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center></span><span class="sxs-lookup"><span data-stu-id="895d2-108"><center>
![Join Azure AD from hello Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="895d2-109">按一下**繼續**hello Azure AD Join 訊息視窗中。</span><span class="sxs-lookup"><span data-stu-id="895d2-109">Click **Continue** in hello Azure AD Join message window.</span></span>
   
   <span data-ttu-id="895d2-110"><center>
   ![加入 Azure AD 訊息視窗](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span><span class="sxs-lookup"><span data-stu-id="895d2-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="895d2-111">提供您的登入認證。</span><span class="sxs-lookup"><span data-stu-id="895d2-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="895d2-112">此登入體驗將會包含所需的 toocomplete 驗證的所有 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="895d2-112">This sign-in experience will include all hello steps that are required toocomplete authentication.</span></span> <span data-ttu-id="895d2-113">如果您是同盟租用戶的一部分，您的系統管理員將提供您組織所裝載的 hello 同盟體驗。</span><span class="sxs-lookup"><span data-stu-id="895d2-113">If you are part of a federated tenant, your administrator will provide you with hello federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="895d2-114"><center>
   ![提供登入認證](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span><span class="sxs-lookup"><span data-stu-id="895d2-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="895d2-115">如果您的組織已加入 tooAzure AD 設定 Azure Multi-factor Authentication Server，提供 hello 第二個因素，才能繼續。</span><span class="sxs-lookup"><span data-stu-id="895d2-115">If your organization has configured Azure Multi-Factor Authentication for joining tooAzure AD, provide hello second factor before proceeding.</span></span>
6. <span data-ttu-id="895d2-116">按一下**接受**上 hello**允許管理此裝置 toobe**螢幕。</span><span class="sxs-lookup"><span data-stu-id="895d2-116">Click **Accept** on hello **Allow this device toobe managed** screen.</span></span>
7. <span data-ttu-id="895d2-117">您應該會看到 「 您的裝置現在是 Azure AD 中的聯結的 tooyour 組織"hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="895d2-117">You should see hello message "Your device is now joined tooyour organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="895d2-118">其他資訊</span><span class="sxs-lookup"><span data-stu-id="895d2-118">Additional information</span></span>
* [<span data-ttu-id="895d2-119">了解適用於 Azure AD Join 的使用案例</span><span class="sxs-lookup"><span data-stu-id="895d2-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="895d2-120">連接已加入網域裝置 tooAzure AD 進行 Windows 10 體驗</span><span class="sxs-lookup"><span data-stu-id="895d2-120">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="895d2-121">設定 Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="895d2-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="895d2-122">透過 Microsoft Passport 不需要密碼就能驗證身分識別</span><span class="sxs-lookup"><span data-stu-id="895d2-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

