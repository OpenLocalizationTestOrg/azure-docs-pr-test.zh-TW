---
title: "適合企業使用的 Windows 10：使用裝置的工作方式 | Microsoft Docs"
description: "部署適合企業使用的 Windows 10 裝置概觀，以及如何與適合 Windows 雲端的 Azure Active Directory 整合。 對照企業可透過 Azure 入口網站採用之裝置的各式佈建和使用方式。"
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
ms.openlocfilehash: 804156048a7596f9937098e6fe762f424526473c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="windows-10-for-the-enterprise-ways-to-use-devices-for-work"></a><span data-ttu-id="53070-105">適合企業使用的 Windows 10：使用裝置的工作方式</span><span class="sxs-lookup"><span data-stu-id="53070-105">Windows 10 for the enterprise: Ways to use devices for work</span></span>
<span data-ttu-id="53070-106">Windows 10 讓您可以充分利用 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="53070-106">Windows 10 gives you the ability to leverage Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="53070-107">您可以將 Windows 10 裝置連接到 Azure AD，以便使用者使用 Azure AD 帳戶或加入其 Azure 識別碼來登入 Windows，存取商務應用程式和資源。</span><span class="sxs-lookup"><span data-stu-id="53070-107">You can connect Windows 10 devices to Azure AD so that users can sign in to Windows by using Azure AD accounts or by adding their Azure IDs to gain access to business apps and resources.</span></span>

![Azure Active Directory 與 Windows 雲端](./media/active-directory-azureadjoin/windows10-overview.png)

## <a name="integrating-windows-10-devices-with-azure-active-directory--a-content-map"></a><span data-ttu-id="53070-109">整合 Windows 10 裝置與 Azure Active Directory：內容對應</span><span class="sxs-lookup"><span data-stu-id="53070-109">Integrating Windows 10 devices with Azure Active Directory--a content map</span></span>
<span data-ttu-id="53070-110">下列主題提供在組織中發揮 Windows 10 裝置不同功能的深入看法。</span><span class="sxs-lookup"><span data-stu-id="53070-110">The following topics provide insights into different capabilities of Windows 10 devices in your organization.</span></span>

|  | <span data-ttu-id="53070-111">主題</span><span class="sxs-lookup"><span data-stu-id="53070-111">Topics</span></span> |
| --- | --- |
| <span data-ttu-id="53070-112">開始使用</span><span class="sxs-lookup"><span data-stu-id="53070-112">Getting started</span></span> |[<span data-ttu-id="53070-113">在您的工作場所中使用 Windows 10 裝置</span><span class="sxs-lookup"><span data-stu-id="53070-113">Using Windows 10 devices in your workplace</span></span>](active-directory-azureadjoin-windows10-devices.md) <br> <br> [<span data-ttu-id="53070-114">透過 Azure Active Directory Join 擴充 Windows 10 裝置的雲端功能</span><span class="sxs-lookup"><span data-stu-id="53070-114">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-overview.md) <br> <br> [<span data-ttu-id="53070-115">透過 Microsoft Passport 不需要密碼就能驗證身分識別</span><span class="sxs-lookup"><span data-stu-id="53070-115">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md) |
| <span data-ttu-id="53070-116">部署</span><span class="sxs-lookup"><span data-stu-id="53070-116">Deployment</span></span> |[<span data-ttu-id="53070-117">適用於 Azure AD Join 的使用案例和部署考量</span><span class="sxs-lookup"><span data-stu-id="53070-117">Usage scenarios and deployment considerations for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md) <br><br> [<span data-ttu-id="53070-118">將已加入網域裝置連接到 Azure AD 以體驗 Windows 10</span><span class="sxs-lookup"><span data-stu-id="53070-118">Connecting domain-joined devices to Azure AD, for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)<br><br>[<span data-ttu-id="53070-119">啟用 Microsoft Passport 並在組織中運用</span><span class="sxs-lookup"><span data-stu-id="53070-119">Enabling Microsoft Passport for work in the organization</span></span>](active-directory-azureadjoin-passport-deployment.md)<br><br> [<span data-ttu-id="53070-120">為 Windows 10 啟用企業狀態漫遊</span><span class="sxs-lookup"><span data-stu-id="53070-120">Enabling Enterprise State Roaming for Windows 10</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)<br><br> |
| <span data-ttu-id="53070-121">使用者工作</span><span class="sxs-lookup"><span data-stu-id="53070-121">User tasks</span></span> |[<span data-ttu-id="53070-122">設定期間使用 Azure AD 設定新的 Windows 10 裝置</span><span class="sxs-lookup"><span data-stu-id="53070-122">Setting up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md) <br><br> [<span data-ttu-id="53070-123">從設定功能表使用 Azure AD 設定 Windows 10 裝置</span><span class="sxs-lookup"><span data-stu-id="53070-123">Setting up a Windows 10 device with Azure AD from the settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md) <br><br> [<span data-ttu-id="53070-124">聯結個人 Windows 10 裝置到貴組織</span><span class="sxs-lookup"><span data-stu-id="53070-124">Joining a personal Windows 10 device to your organization</span></span>](active-directory-azureadjoin-personal-device.md) |

