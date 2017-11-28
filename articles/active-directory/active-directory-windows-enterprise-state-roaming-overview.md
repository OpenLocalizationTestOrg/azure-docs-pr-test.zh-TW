---
title: "aaaEnterprise 狀態漫遊概觀 |Microsoft 文件"
description: "提供 Windows 裝置中企業狀態漫遊設定的相關資訊。 企業狀態漫遊使用者提供一致的方式透過他們的 Windows 裝置，並減少 hello 設定新裝置所需的時間。"
services: active-directory
keywords: "什麼是企業狀態漫遊, 企業同步處理, windows 雲端"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 83b3b58f-94c1-4ab0-be05-20e01f5ae3f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 436076383b70b7cd65a612e3928f62f26ac5fa84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-state-roaming-overview"></a><span data-ttu-id="3beb5-105">企業狀態漫遊概觀</span><span class="sxs-lookup"><span data-stu-id="3beb5-105">Enterprise State Roaming overview</span></span>
<span data-ttu-id="3beb5-106">與 Windows 10 [Azure Active Directory (Azure AD)](active-directory-whatis.md)使用者提升 hello 能力 toosecurely 同步處理其使用者設定和應用程式設定資料 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="3beb5-106">With Windows 10, [Azure Active Directory (Azure AD)](active-directory-whatis.md) users gain hello ability toosecurely synchronize their user settings and application settings data toohello cloud.</span></span> <span data-ttu-id="3beb5-107">企業狀態漫遊使用者提供一致的方式透過他們的 Windows 裝置，並減少 hello 設定新裝置所需的時間。</span><span class="sxs-lookup"><span data-stu-id="3beb5-107">Enterprise State Roaming provides users with a unified experience across their Windows devices and reduces hello time needed for configuring a new device.</span></span> <span data-ttu-id="3beb5-108">企業狀態漫遊的運作類似 toohello 標準[取用者設定同步處理](http://windows.microsoft.com/en-US/windows-8/sync-settings-pcs)，最初在 Windows 8 中導入。</span><span class="sxs-lookup"><span data-stu-id="3beb5-108">Enterprise State Roaming operates similar toohello standard [consumer settings sync](http://windows.microsoft.com/en-US/windows-8/sync-settings-pcs) that was first introduced in Windows 8.</span></span> <span data-ttu-id="3beb5-109">此外，企業狀態漫遊提供：</span><span class="sxs-lookup"><span data-stu-id="3beb5-109">Additionally, Enterprise State Roaming offers:</span></span>

* <span data-ttu-id="3beb5-110">**分隔公司和取用者資料** – 組織可以控制他們的資料，取用者雲端帳戶中不會混合公司資料，企業雲端帳戶中也不會混合取用者資料。</span><span class="sxs-lookup"><span data-stu-id="3beb5-110">**Separation of corporate and consumer data** – Organizations are in control of their data, and there is no mixing of corporate data in a consumer cloud account or consumer data in an enterprise cloud account.</span></span>
* <span data-ttu-id="3beb5-111">**增強式安全性**– 資料會自動加密使用 Azure Rights Management (Azure RMS) 離開 hello 使用者的 Windows 10 裝置之前，資料將會存留在 hello 雲端中的靜止時加密。</span><span class="sxs-lookup"><span data-stu-id="3beb5-111">**Enhanced security** – Data is automatically encrypted before leaving hello user’s Windows 10 device by using Azure Rights Management (Azure RMS), and data stays encrypted at rest in hello cloud.</span></span> <span data-ttu-id="3beb5-112">所有內容都維持在 hello 雲端，除了 hello 命名空間，例如設定名稱和 Windows 應用程式名稱中的靜止時加密。</span><span class="sxs-lookup"><span data-stu-id="3beb5-112">All content stays encrypted at rest in hello cloud, except for hello namespaces, like settings names and Windows app names.</span></span>  
* <span data-ttu-id="3beb5-113">**較佳的管理和監視**– 提供控制項與可見性者同步處理您組織中以及透過 hello Azure AD 入口網站整合哪些裝置上的設定。</span><span class="sxs-lookup"><span data-stu-id="3beb5-113">**Better management and monitoring** – Provides control and visibility over who syncs settings in your organization and on which devices through hello Azure AD portal integration.</span></span> 

<span data-ttu-id="3beb5-114">企業狀態漫遊也可以在多個 Azure 區域中使用。</span><span class="sxs-lookup"><span data-stu-id="3beb5-114">Enterprise State Roaming is available in multiple Azure regions.</span></span> <span data-ttu-id="3beb5-115">您可以找到 hello 更新清單的區域上 hello[依照地區的 Azure 服務](https://azure.microsoft.com/regions/#services)下 Azure Active Directory 頁面。</span><span class="sxs-lookup"><span data-stu-id="3beb5-115">You can find hello updated list of available regions on hello [Azure Services by Regions](https://azure.microsoft.com/regions/#services) page under Azure Active Directory.</span></span>

| <span data-ttu-id="3beb5-116">文章</span><span class="sxs-lookup"><span data-stu-id="3beb5-116">Article</span></span> | <span data-ttu-id="3beb5-117">說明</span><span class="sxs-lookup"><span data-stu-id="3beb5-117">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="3beb5-118">在 Azure Active Directory 中啟用企業狀態漫遊</span><span class="sxs-lookup"><span data-stu-id="3beb5-118">Enable Enterprise State Roaming in Azure Active Directory</span></span>](active-directory-windows-enterprise-state-roaming-enable.md) |<span data-ttu-id="3beb5-119">企業狀態漫遊是可用 tooany 組織與 Premium Azure Active Directory (Azure AD) 的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3beb5-119">Enterprise State Roaming is available tooany organization with a Premium Azure Active Directory (Azure AD) subscription.</span></span> <span data-ttu-id="3beb5-120">如需有關如何 tooget Azure AD 訂用帳戶，請參閱 hello [Azure AD 產品](https://azure.microsoft.com/services/active-directory)頁面。</span><span class="sxs-lookup"><span data-stu-id="3beb5-120">For more details on how tooget an Azure AD subscription, see hello [Azure AD product](https://azure.microsoft.com/services/active-directory) page.</span></span> |
| [<span data-ttu-id="3beb5-121">設定和資料漫遊常見問題集</span><span class="sxs-lookup"><span data-stu-id="3beb5-121">Settings and data roaming FAQ</span></span>](active-directory-windows-enterprise-state-roaming-faqs.md) |<span data-ttu-id="3beb5-122">本主題將回答 IT 系統管理員可能會遇到的設定和應用程式資料同步處理的一些問題。</span><span class="sxs-lookup"><span data-stu-id="3beb5-122">This topic answers some questions IT administrators might have about settings and app data sync.</span></span> |
| [<span data-ttu-id="3beb5-123">設定同步處理的群組原則和 MDM 設定</span><span class="sxs-lookup"><span data-stu-id="3beb5-123">Group policy and MDM settings for settings sync</span></span>](active-directory-windows-enterprise-state-roaming-group-policy-settings.md) |<span data-ttu-id="3beb5-124">Windows 10 提供群組原則和行動裝置管理 (MDM) 原則設定 toolimit 設定同步處理。</span><span class="sxs-lookup"><span data-stu-id="3beb5-124">Windows 10 provides Group Policy and mobile device management (MDM) policy settings toolimit settings sync.</span></span> |
| [<span data-ttu-id="3beb5-125">Windows 10 漫遊設定參考</span><span class="sxs-lookup"><span data-stu-id="3beb5-125">Windows 10 roaming settings reference</span></span>](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md) |<span data-ttu-id="3beb5-126">hello 以下是所有將進行漫遊及/或備份在 Windows 10 中的 hello 設定的完整清單。</span><span class="sxs-lookup"><span data-stu-id="3beb5-126">hello following is a complete list of all hello settings that will be roamed and/or backed-up in Windows 10.</span></span> |
| [<span data-ttu-id="3beb5-127">疑難排解</span><span class="sxs-lookup"><span data-stu-id="3beb5-127">Troubleshooting</span></span>](active-directory-windows-enterprise-state-roaming-troubleshooting.md) |<span data-ttu-id="3beb5-128">本主題會執行一些疑難排解基本步驟，並且包含一份已知問題清單。</span><span class="sxs-lookup"><span data-stu-id="3beb5-128">This topic goes through some basic steps for troubleshooting, and contains a list of known issues.</span></span> |

