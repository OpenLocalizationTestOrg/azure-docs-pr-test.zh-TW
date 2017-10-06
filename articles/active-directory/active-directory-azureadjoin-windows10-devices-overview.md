---
title: "Hello 企業版的 Windows 10： 工作的方式 toouse 裝置 |Microsoft 文件"
description: "部署 Windows 10 裝置的企業，以及如何與 Azure Active Directory 的 toointegrate hello Windows 雲端的概觀。 相反的裝置可以佈建，並透過 Azure 入口網站 hello 企業中使用 hello 不同方式。"
keywords: "windows 雲端, Azure Active Directory 上的 Windows, Azure 上的 Windows 10 裝置, Azure Windows 裝置"
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2cb9ab6a-55b6-4658-b7f2-6e05ae015e1b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 95b452bc5ba3937e16de769275a59c77cb821e23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-10-for-hello-enterprise-ways-toouse-devices-for-work"></a><span data-ttu-id="035cb-105">Hello 企業版的 Windows 10： 工作的方式 toouse 裝置</span><span class="sxs-lookup"><span data-stu-id="035cb-105">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>
<span data-ttu-id="035cb-106">Windows 10 提供 hello 能力 tooleverage Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="035cb-106">Windows 10 gives you hello ability tooleverage Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="035cb-107">您可以連接 Windows 10 裝置 tooAzure AD，讓使用者可以登入 tooWindows，使用 Azure AD 帳戶，或加入其 Azure Id toogain 存取 toobusiness 應用程式和資源。</span><span class="sxs-lookup"><span data-stu-id="035cb-107">You can connect Windows 10 devices tooAzure AD so that users can sign in tooWindows by using Azure AD accounts or by adding their Azure IDs toogain access toobusiness apps and resources.</span></span>

![Azure Active Directory 與 Windows 雲端](./media/active-directory-azureadjoin/windows10-overview.png)

## <a name="integrating-windows-10-devices-with-azure-active-directory--a-content-map"></a><span data-ttu-id="035cb-109">整合 Windows 10 裝置與 Azure Active Directory：內容對應</span><span class="sxs-lookup"><span data-stu-id="035cb-109">Integrating Windows 10 devices with Azure Active Directory--a content map</span></span>
<span data-ttu-id="035cb-110">下列主題中的 hello 提供深入了解貴組織中的 Windows 10 裝置的不同功能。</span><span class="sxs-lookup"><span data-stu-id="035cb-110">hello following topics provide insights into different capabilities of Windows 10 devices in your organization.</span></span>

|  | <span data-ttu-id="035cb-111">主題</span><span class="sxs-lookup"><span data-stu-id="035cb-111">Topics</span></span> |
| --- | --- |
| <span data-ttu-id="035cb-112">開始使用</span><span class="sxs-lookup"><span data-stu-id="035cb-112">Getting started</span></span> |[<span data-ttu-id="035cb-113">在您的工作場所中使用 Windows 10 裝置</span><span class="sxs-lookup"><span data-stu-id="035cb-113">Using Windows 10 devices in your workplace</span></span>](active-directory-azureadjoin-windows10-devices.md) <br> <br> [<span data-ttu-id="035cb-114">擴充功能 tooWindows 10 裝置透過 Azure Active Directory 加入雲端</span><span class="sxs-lookup"><span data-stu-id="035cb-114">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-overview.md) <br> <br> [<span data-ttu-id="035cb-115">透過 Microsoft Passport 不需要密碼就能驗證身分識別</span><span class="sxs-lookup"><span data-stu-id="035cb-115">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md) |
| <span data-ttu-id="035cb-116">部署</span><span class="sxs-lookup"><span data-stu-id="035cb-116">Deployment</span></span> |[<span data-ttu-id="035cb-117">適用於 Azure AD Join 的使用案例和部署考量</span><span class="sxs-lookup"><span data-stu-id="035cb-117">Usage scenarios and deployment considerations for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md) <br><br> [<span data-ttu-id="035cb-118">連接已加入網域裝置 tooAzure AD，適用於 Windows 10 體驗</span><span class="sxs-lookup"><span data-stu-id="035cb-118">Connecting domain-joined devices tooAzure AD, for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)<br><br>[<span data-ttu-id="035cb-119">啟用 Microsoft Passport hello 組織中的工作</span><span class="sxs-lookup"><span data-stu-id="035cb-119">Enabling Microsoft Passport for work in hello organization</span></span>](active-directory-azureadjoin-passport-deployment.md)<br><br> [<span data-ttu-id="035cb-120">為 Windows 10 啟用企業狀態漫遊</span><span class="sxs-lookup"><span data-stu-id="035cb-120">Enabling Enterprise State Roaming for Windows 10</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)<br><br> |
| <span data-ttu-id="035cb-121">使用者工作</span><span class="sxs-lookup"><span data-stu-id="035cb-121">User tasks</span></span> |[<span data-ttu-id="035cb-122">設定期間使用 Azure AD 設定新的 Windows 10 裝置</span><span class="sxs-lookup"><span data-stu-id="035cb-122">Setting up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md) <br><br> <span data-ttu-id="035cb-123">[使用 Azure AD hello 設定] 功能表中的 Windows 10 裝置設定](active-directory-azureadjoin-user-upgrade.md)</span><span class="sxs-lookup"><span data-stu-id="035cb-123">[Setting up a Windows 10 device with Azure AD from hello settings menu](active-directory-azureadjoin-user-upgrade.md)</span></span> <br><br> [<span data-ttu-id="035cb-124">加入個人的 Windows 10 裝置 tooyour 公司</span><span class="sxs-lookup"><span data-stu-id="035cb-124">Joining a personal Windows 10 device tooyour organization</span></span>](active-directory-azureadjoin-personal-device.md) |

