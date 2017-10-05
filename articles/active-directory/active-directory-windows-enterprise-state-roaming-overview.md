---
title: "企業狀態漫遊概觀 | Microsoft Docs"
description: "提供 Windows 裝置中企業狀態漫遊設定的相關資訊。 企業狀態漫遊提供使用者跨 Windows 裝置的一致體驗，並且減少設定新的裝置所需的時間。"
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
ms.openlocfilehash: b3c01f8d332d26e92dc3052681a4b2c95142d440
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-state-roaming-overview"></a><span data-ttu-id="9f463-105">企業狀態漫遊概觀</span><span class="sxs-lookup"><span data-stu-id="9f463-105">Enterprise State Roaming overview</span></span>
<span data-ttu-id="9f463-106">使用 Windows 10， [Azure Active Directory (Azure AD)](active-directory-whatis.md) 使用者能夠安全地將其使用者設定和應用程式設定資料同步處理至雲端。</span><span class="sxs-lookup"><span data-stu-id="9f463-106">With Windows 10, [Azure Active Directory (Azure AD)](active-directory-whatis.md) users gain the ability to securely synchronize their user settings and application settings data to the cloud.</span></span> <span data-ttu-id="9f463-107">企業狀態漫遊提供使用者跨 Windows 裝置的一致體驗，並且減少設定新的裝置所需的時間。</span><span class="sxs-lookup"><span data-stu-id="9f463-107">Enterprise State Roaming provides users with a unified experience across their Windows devices and reduces the time needed for configuring a new device.</span></span> <span data-ttu-id="9f463-108">企業狀態漫遊的運作類似於首先在 Windows 8 中引進的標準 [取用者設定同步處理](http://windows.microsoft.com/en-US/windows-8/sync-settings-pcs) 。</span><span class="sxs-lookup"><span data-stu-id="9f463-108">Enterprise State Roaming operates similar to the standard [consumer settings sync](http://windows.microsoft.com/en-US/windows-8/sync-settings-pcs) that was first introduced in Windows 8.</span></span> <span data-ttu-id="9f463-109">此外，企業狀態漫遊提供：</span><span class="sxs-lookup"><span data-stu-id="9f463-109">Additionally, Enterprise State Roaming offers:</span></span>

* <span data-ttu-id="9f463-110">**分隔公司和取用者資料** – 組織可以控制他們的資料，取用者雲端帳戶中不會混合公司資料，企業雲端帳戶中也不會混合取用者資料。</span><span class="sxs-lookup"><span data-stu-id="9f463-110">**Separation of corporate and consumer data** – Organizations are in control of their data, and there is no mixing of corporate data in a consumer cloud account or consumer data in an enterprise cloud account.</span></span>
* <span data-ttu-id="9f463-111">**增強式安全性** – 資料會在離開使用者的 Windows 10 裝置之前自動加密，方法是使用 Azure Rights Management (Azure RMS)，資料在雲端中待用時會保持加密。</span><span class="sxs-lookup"><span data-stu-id="9f463-111">**Enhanced security** – Data is automatically encrypted before leaving the user’s Windows 10 device by using Azure Rights Management (Azure RMS), and data stays encrypted at rest in the cloud.</span></span> <span data-ttu-id="9f463-112">所有內容在雲端中待用時會保持加密，除了命名空間，例如設定名稱和 Windows 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="9f463-112">All content stays encrypted at rest in the cloud, except for the namespaces, like settings names and Windows app names.</span></span>  
* <span data-ttu-id="9f463-113">**更好的管理和監視** – 透過 Azure AD 入口網站整合，對於誰能同步處理組織中的設定以及在哪些裝置上提供更多的控制權和可見性。</span><span class="sxs-lookup"><span data-stu-id="9f463-113">**Better management and monitoring** – Provides control and visibility over who syncs settings in your organization and on which devices through the Azure AD portal integration.</span></span> 

<span data-ttu-id="9f463-114">企業狀態漫遊也可以在多個 Azure 區域中使用。</span><span class="sxs-lookup"><span data-stu-id="9f463-114">Enterprise State Roaming is available in multiple Azure regions.</span></span> <span data-ttu-id="9f463-115">您可以在 Azure Active Directory 下方的 [依區域提供的 Azure 服務](https://azure.microsoft.com/regions/#services) 上找到可用區域的更新清單。</span><span class="sxs-lookup"><span data-stu-id="9f463-115">You can find the updated list of available regions on the [Azure Services by Regions](https://azure.microsoft.com/regions/#services) page under Azure Active Directory.</span></span>

| <span data-ttu-id="9f463-116">文章</span><span class="sxs-lookup"><span data-stu-id="9f463-116">Article</span></span> | <span data-ttu-id="9f463-117">說明</span><span class="sxs-lookup"><span data-stu-id="9f463-117">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="9f463-118">在 Azure Active Directory 中啟用企業狀態漫遊</span><span class="sxs-lookup"><span data-stu-id="9f463-118">Enable Enterprise State Roaming in Azure Active Directory</span></span>](active-directory-windows-enterprise-state-roaming-enable.md) |<span data-ttu-id="9f463-119">企業狀態漫遊適用於具有 Premium Azure Active Directory (Azure AD) 訂用帳戶的任何組織。</span><span class="sxs-lookup"><span data-stu-id="9f463-119">Enterprise State Roaming is available to any organization with a Premium Azure Active Directory (Azure AD) subscription.</span></span> <span data-ttu-id="9f463-120">如需如何取得 Azure AD 訂用帳戶的詳細資訊，請參閱 [Azure AD 產品](https://azure.microsoft.com/services/active-directory) 頁面。</span><span class="sxs-lookup"><span data-stu-id="9f463-120">For more details on how to get an Azure AD subscription, see the [Azure AD product](https://azure.microsoft.com/services/active-directory) page.</span></span> |
| [<span data-ttu-id="9f463-121">設定和資料漫遊常見問題集</span><span class="sxs-lookup"><span data-stu-id="9f463-121">Settings and data roaming FAQ</span></span>](active-directory-windows-enterprise-state-roaming-faqs.md) |<span data-ttu-id="9f463-122">本主題將回答 IT 系統管理員可能會遇到的設定和應用程式資料同步處理的一些問題。</span><span class="sxs-lookup"><span data-stu-id="9f463-122">This topic answers some questions IT administrators might have about settings and app data sync.</span></span> |
| [<span data-ttu-id="9f463-123">設定同步處理的群組原則和 MDM 設定</span><span class="sxs-lookup"><span data-stu-id="9f463-123">Group policy and MDM settings for settings sync</span></span>](active-directory-windows-enterprise-state-roaming-group-policy-settings.md) |<span data-ttu-id="9f463-124">Windows 10 提供群組原則和行動裝置管理 (MDM) 原則設定，以限制設定同步處理。</span><span class="sxs-lookup"><span data-stu-id="9f463-124">Windows 10 provides Group Policy and mobile device management (MDM) policy settings to limit settings sync.</span></span> |
| [<span data-ttu-id="9f463-125">Windows 10 漫遊設定參考</span><span class="sxs-lookup"><span data-stu-id="9f463-125">Windows 10 roaming settings reference</span></span>](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md) |<span data-ttu-id="9f463-126">以下是在 Windows 10 中進行漫遊及/或備份的所有設定的完整清單。</span><span class="sxs-lookup"><span data-stu-id="9f463-126">The following is a complete list of all the settings that will be roamed and/or backed-up in Windows 10.</span></span> |
| [<span data-ttu-id="9f463-127">疑難排解</span><span class="sxs-lookup"><span data-stu-id="9f463-127">Troubleshooting</span></span>](active-directory-windows-enterprise-state-roaming-troubleshooting.md) |<span data-ttu-id="9f463-128">本主題會執行一些疑難排解基本步驟，並且包含一份已知問題清單。</span><span class="sxs-lookup"><span data-stu-id="9f463-128">This topic goes through some basic steps for troubleshooting, and contains a list of known issues.</span></span> |

