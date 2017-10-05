---
title: "<span data-ttu-id=\"29866-101\">群組原則和 MDM 設定 | Microsoft Docs</span><span class=\"sxs-lookup\"><span data-stu-id=\"29866-101\">Group Policy and MDM settings | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"29866-102\">提供應該在公司所擁有的裝置上使用的群組原則和行動裝置管理 (MDM) 設定的相關資訊。</span><span class=\"sxs-lookup\"><span data-stu-id=\"29866-102\">Provides information about group policy and mobile device management (MDM) settings that should be used on corporate-owned devices.</span></span> <span data-ttu-id=\"29866-103\">這些原則會套用至使用者的整個裝置。</span><span class=\"sxs-lookup\"><span data-stu-id=\"29866-103\">These policies are applied to the user’s entire device.</span></span>"
services: active-directory
keywords: "<span data-ttu-id=\"29866-104\">什麼是企業狀態漫遊的群組原則和 MDM 設定, 企業狀態漫遊, windows 雲端</span><span class=\"sxs-lookup\"><span data-stu-id=\"29866-104\">what are group Policy and MDM settings for Enterprise State Roaming, Enterprise State Roaming, windows cloud</span></span>"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 6471a9b3-8dd4-4237-89d1-bfbeca9f8252
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 71dd5281a618fe7367eab3e97daac069f77ab491
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="group-policy-and-mdm-settings"></a><span data-ttu-id="29866-105">群組原則和 MDM 設定</span><span class="sxs-lookup"><span data-stu-id="29866-105">Group Policy and MDM settings</span></span>
<span data-ttu-id="29866-106">只在公司所擁有的裝置上使用這些群組原則和行動裝置管理 (MDM) 設定，因為這些原則會套用到使用者的整個裝置。</span><span class="sxs-lookup"><span data-stu-id="29866-106">Use these group policy and mobile device management (MDM) settings only on corporate-owned devices because these policies are applied to the user’s entire device.</span></span> <span data-ttu-id="29866-107">套用 MDM 原則來停用個人、使用者所擁有的裝置的設定同步處理，會對使用該裝置造成負面影響。</span><span class="sxs-lookup"><span data-stu-id="29866-107">Applying an MDM policy to disable settings sync for a personal, user-owned device will negatively impact the use of that device.</span></span> <span data-ttu-id="29866-108">此外，在裝置上的其他使用者帳戶也會被原則影響。</span><span class="sxs-lookup"><span data-stu-id="29866-108">Additionally, other user accounts on the device will also be affected by the policy.</span></span>

<span data-ttu-id="29866-109">要管理個人 (未受管理) 裝置的漫遊的企業可以使用 Azure 入口網站啟用或停用漫遊，而不是使用群組原則或 MDM</span><span class="sxs-lookup"><span data-stu-id="29866-109">Enterprises that want to manage roaming for personal (unmanaged) devices can use the Azure portal to enable or disable roaming, rather than using Group Policy or MDM.</span></span>
<span data-ttu-id="29866-110">下表描述可用的原則設定。</span><span class="sxs-lookup"><span data-stu-id="29866-110">The following tables describe the policy settings available.</span></span>

## <a name="mdm-settings"></a><span data-ttu-id="29866-111">MDM 設定</span><span class="sxs-lookup"><span data-stu-id="29866-111">MDM settings</span></span>
<span data-ttu-id="29866-112">MDM 原則設定會套用至 Windows 10 及 Windows 10 行動裝置版。</span><span class="sxs-lookup"><span data-stu-id="29866-112">The MDM policy settings apply to both Windows 10 and Windows 10 Mobile.</span></span>  <span data-ttu-id="29866-113">Windows 10 行動裝置版支援僅適用於以 Microsoft 帳戶為基礎且透過使用者的 OneDrive 帳戶進行的漫遊。</span><span class="sxs-lookup"><span data-stu-id="29866-113">Windows 10 Mobile support exists only for Microsoft account based roaming via user’s OneDrive account.</span></span>  <span data-ttu-id="29866-114">如需哪些裝置支援以 Azure AD 為基礎的同步處理的詳細資訊，請參閱＜裝置與端點＞一節。</span><span class="sxs-lookup"><span data-stu-id="29866-114">Please refer to “Devices and endpoints” section for details on what devices are supported for Azure AD based syncing.</span></span>

| <span data-ttu-id="29866-115">名稱</span><span class="sxs-lookup"><span data-stu-id="29866-115">Name</span></span> | <span data-ttu-id="29866-116">說明</span><span class="sxs-lookup"><span data-stu-id="29866-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="29866-117">允許 Microsoft 帳戶連接</span><span class="sxs-lookup"><span data-stu-id="29866-117">Allow Microsoft Account Connection</span></span> |<span data-ttu-id="29866-118">允許使用者在裝置上使用 Microsoft 帳戶進行驗證</span><span class="sxs-lookup"><span data-stu-id="29866-118">Allows users to authenticate using a Microsoft account on the device</span></span> |
| <span data-ttu-id="29866-119">允許同步處理我的設定</span><span class="sxs-lookup"><span data-stu-id="29866-119">Allow Sync My Settings</span></span> |<span data-ttu-id="29866-120">讓使用者能夠漫遊 Windows 設定和應用程式資料。停用此原則，將停用行動裝置上的同步處理及備份</span><span class="sxs-lookup"><span data-stu-id="29866-120">Allows users to roam Windows settings and app data; Disabling this policy will disable sync as well as backups on mobile devices</span></span> |

## <a name="group-policy-settings"></a><span data-ttu-id="29866-121">群組原則設定</span><span class="sxs-lookup"><span data-stu-id="29866-121">Group Policy settings</span></span>
<span data-ttu-id="29866-122">群組原則設定會套用至加入 Active Directory 網域的 Windows 10 裝置上。</span><span class="sxs-lookup"><span data-stu-id="29866-122">The Group Policy settings apply to Windows 10 devices that are joined to an Active Directory domain.</span></span> <span data-ttu-id="29866-123">資料表也包含看似可管理同步處理設定的舊版設定，但不適用於 Windows 10 的企業狀態漫遊 (已在其說明中註明「不要使用」)。</span><span class="sxs-lookup"><span data-stu-id="29866-123">The table also includes legacy settings that would appear to manage sync settings, but that do not work for Enterprise State Roaming for Windows 10, which are noted with ‘Do not use’ in the description.</span></span>

| <span data-ttu-id="29866-124">名稱</span><span class="sxs-lookup"><span data-stu-id="29866-124">Name</span></span> | <span data-ttu-id="29866-125">說明</span><span class="sxs-lookup"><span data-stu-id="29866-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="29866-126">帳戶：封鎖 Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="29866-126">Accounts: Block Microsoft Accounts</span></span> |<span data-ttu-id="29866-127">此原則設定會防止使用者在這部電腦上新增新的 Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="29866-127">This policy setting prevents users from adding new Microsoft accounts on this computer</span></span> |
| <span data-ttu-id="29866-128">不要同步處理</span><span class="sxs-lookup"><span data-stu-id="29866-128">Do not sync</span></span> |<span data-ttu-id="29866-129">防止使用者漫遊 Windows 設定和應用程式資料</span><span class="sxs-lookup"><span data-stu-id="29866-129">Prevents users to roam Windows settings and app data</span></span> |
| <span data-ttu-id="29866-130">不要同步處理個人化</span><span class="sxs-lookup"><span data-stu-id="29866-130">Do not sync personalize</span></span> |<span data-ttu-id="29866-131">停用主題群組的同步處理</span><span class="sxs-lookup"><span data-stu-id="29866-131">Disables syncing of the Themes group</span></span> |
| <span data-ttu-id="29866-132">不要同步處理瀏覽器設定</span><span class="sxs-lookup"><span data-stu-id="29866-132">Do not sync browser settings</span></span> |<span data-ttu-id="29866-133">停用 Internet Explorer 群組的同步處理</span><span class="sxs-lookup"><span data-stu-id="29866-133">Disables syncing of the Internet Explorer group</span></span> |
| <span data-ttu-id="29866-134">不要同步處理密碼</span><span class="sxs-lookup"><span data-stu-id="29866-134">Do not sync passwords</span></span> |<span data-ttu-id="29866-135">停用密碼群組的同步處理</span><span class="sxs-lookup"><span data-stu-id="29866-135">Disables syncing of Passwords group</span></span> |
| <span data-ttu-id="29866-136">不要同步處理其他 Windows 設定</span><span class="sxs-lookup"><span data-stu-id="29866-136">Do not sync other Windows settings</span></span> |<span data-ttu-id="29866-137">停用其他 Windows 設定群組的同步處理</span><span class="sxs-lookup"><span data-stu-id="29866-137">Disables syncing of Other Windows settings group</span></span> |
| <span data-ttu-id="29866-138">不要同步處理桌面個人化</span><span class="sxs-lookup"><span data-stu-id="29866-138">Do not sync desktop personalization</span></span> |<span data-ttu-id="29866-139">不要使用；沒有作用</span><span class="sxs-lookup"><span data-stu-id="29866-139">Do not use; has no effect</span></span> |
| <span data-ttu-id="29866-140">不要同步處理已計量連接</span><span class="sxs-lookup"><span data-stu-id="29866-140">Do not sync on metered connections</span></span> |<span data-ttu-id="29866-141">停用已計量連接的漫遊，例如行動電話 3G</span><span class="sxs-lookup"><span data-stu-id="29866-141">Disables roaming on metered connections, such as cellular 3G</span></span> |
| <span data-ttu-id="29866-142">不要同步處理應用程式</span><span class="sxs-lookup"><span data-stu-id="29866-142">Do not sync apps</span></span> |<span data-ttu-id="29866-143">不要使用；沒有作用</span><span class="sxs-lookup"><span data-stu-id="29866-143">Do not use; has no effect</span></span> |
| <span data-ttu-id="29866-144">不要同步處理應用程式設定</span><span class="sxs-lookup"><span data-stu-id="29866-144">Do not sync app settings</span></span> |<span data-ttu-id="29866-145">停用應用程式資料的漫遊</span><span class="sxs-lookup"><span data-stu-id="29866-145">Disables roaming of app data</span></span> |
| <span data-ttu-id="29866-146">不要同步處理啟動設定</span><span class="sxs-lookup"><span data-stu-id="29866-146">Do not sync start settings</span></span> |<span data-ttu-id="29866-147">不要使用；沒有作用</span><span class="sxs-lookup"><span data-stu-id="29866-147">Do not use; has no effect</span></span> |

## <a name="related-topics"></a><span data-ttu-id="29866-148">相關主題</span><span class="sxs-lookup"><span data-stu-id="29866-148">Related topics</span></span>
* [<span data-ttu-id="29866-149">企業狀態漫遊概觀</span><span class="sxs-lookup"><span data-stu-id="29866-149">Enterprise State Roaming overview</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)
* [<span data-ttu-id="29866-150">在 Azure Active Directory 中啟用企業狀態漫遊</span><span class="sxs-lookup"><span data-stu-id="29866-150">Enable enterprise state roaming in Azure Active Directory</span></span>](active-directory-windows-enterprise-state-roaming-enable.md)
* [<span data-ttu-id="29866-151">設定和資料漫遊常見問題集</span><span class="sxs-lookup"><span data-stu-id="29866-151">Settings and data roaming FAQ</span></span>](active-directory-windows-enterprise-state-roaming-faqs.md)
* [<span data-ttu-id="29866-152">Windows 10 漫遊設定參考</span><span class="sxs-lookup"><span data-stu-id="29866-152">Windows 10 roaming settings reference</span></span>](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [<span data-ttu-id="29866-153">疑難排解</span><span class="sxs-lookup"><span data-stu-id="29866-153">Troubleshooting</span></span>](active-directory-windows-enterprise-state-roaming-troubleshooting.md)

