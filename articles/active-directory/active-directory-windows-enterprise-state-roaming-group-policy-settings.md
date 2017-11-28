---
title: "aaaGroup 原則和 MDM 設定 |Microsoft 文件"
description: "提供應該在公司所擁有的裝置上使用的群組原則和行動裝置管理 (MDM) 設定的相關資訊。 這些原則會套用的 toohello 使用者整個裝置。"
services: active-directory
keywords: "什麼是企業狀態漫遊的群組原則和 MDM 設定, 企業狀態漫遊, windows 雲端"
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
ms.openlocfilehash: 762419b47014b1fb4d92ac528785e20078afe689
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="group-policy-and-mdm-settings"></a><span data-ttu-id="c2ccd-105">群組原則和 MDM 設定</span><span class="sxs-lookup"><span data-stu-id="c2ccd-105">Group Policy and MDM settings</span></span>
<span data-ttu-id="c2ccd-106">只有在公司擁有的裝置上使用這些群組原則和行動裝置管理 (MDM) 設定，因為這些原則會套用的 toohello 使用者整個裝置。</span><span class="sxs-lookup"><span data-stu-id="c2ccd-106">Use these group policy and mobile device management (MDM) settings only on corporate-owned devices because these policies are applied toohello user’s entire device.</span></span> <span data-ttu-id="c2ccd-107">套用個人 MDM 原則 toodisable 設定同步處理，使用者所擁有的裝置將會產生負面影響 hello 使用該裝置。</span><span class="sxs-lookup"><span data-stu-id="c2ccd-107">Applying an MDM policy toodisable settings sync for a personal, user-owned device will negatively impact hello use of that device.</span></span> <span data-ttu-id="c2ccd-108">此外，hello 裝置上的其他使用者帳戶也將 hello 原則所影響。</span><span class="sxs-lookup"><span data-stu-id="c2ccd-108">Additionally, other user accounts on hello device will also be affected by hello policy.</span></span>

<span data-ttu-id="c2ccd-109">想要 toomanage 漫遊個人 (unmanaged) 的裝置可以使用的企業 hello Azure 入口網站 tooenable 或停用漫遊，而不是使用群組原則或 mdm。</span><span class="sxs-lookup"><span data-stu-id="c2ccd-109">Enterprises that want toomanage roaming for personal (unmanaged) devices can use hello Azure portal tooenable or disable roaming, rather than using Group Policy or MDM.</span></span>
<span data-ttu-id="c2ccd-110">hello 下表描述可用的 hello 原則設定。</span><span class="sxs-lookup"><span data-stu-id="c2ccd-110">hello following tables describe hello policy settings available.</span></span>

## <a name="mdm-settings"></a><span data-ttu-id="c2ccd-111">MDM 設定</span><span class="sxs-lookup"><span data-stu-id="c2ccd-111">MDM settings</span></span>
<span data-ttu-id="c2ccd-112">hello MDM 原則設定會套用 tooboth Windows 10 和 Windows 10 行動裝置。</span><span class="sxs-lookup"><span data-stu-id="c2ccd-112">hello MDM policy settings apply tooboth Windows 10 and Windows 10 Mobile.</span></span>  <span data-ttu-id="c2ccd-113">Windows 10 行動裝置版支援僅適用於以 Microsoft 帳戶為基礎且透過使用者的 OneDrive 帳戶進行的漫遊。</span><span class="sxs-lookup"><span data-stu-id="c2ccd-113">Windows 10 Mobile support exists only for Microsoft account based roaming via user’s OneDrive account.</span></span>  <span data-ttu-id="c2ccd-114">請參閱 「 裝置和端點 > 一節以取得詳細資料，在 Azure ad 支援哪些裝置太基礎同步處理。</span><span class="sxs-lookup"><span data-stu-id="c2ccd-114">Please refer too“Devices and endpoints” section for details on what devices are supported for Azure AD based syncing.</span></span>

| <span data-ttu-id="c2ccd-115">名稱</span><span class="sxs-lookup"><span data-stu-id="c2ccd-115">Name</span></span> | <span data-ttu-id="c2ccd-116">說明</span><span class="sxs-lookup"><span data-stu-id="c2ccd-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c2ccd-117">允許 Microsoft 帳戶連接</span><span class="sxs-lookup"><span data-stu-id="c2ccd-117">Allow Microsoft Account Connection</span></span> |<span data-ttu-id="c2ccd-118">可讓使用者 tooauthenticate hello 裝置上使用 Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="c2ccd-118">Allows users tooauthenticate using a Microsoft account on hello device</span></span> |
| <span data-ttu-id="c2ccd-119">允許同步處理我的設定</span><span class="sxs-lookup"><span data-stu-id="c2ccd-119">Allow Sync My Settings</span></span> |<span data-ttu-id="c2ccd-120">可讓使用者 tooroam Windows 設定和應用程式資料。同步處理，以及行動裝置上的備份時將停用此原則將會停用</span><span class="sxs-lookup"><span data-stu-id="c2ccd-120">Allows users tooroam Windows settings and app data; Disabling this policy will disable sync as well as backups on mobile devices</span></span> |

## <a name="group-policy-settings"></a><span data-ttu-id="c2ccd-121">群組原則設定</span><span class="sxs-lookup"><span data-stu-id="c2ccd-121">Group Policy settings</span></span>
<span data-ttu-id="c2ccd-122">hello 群組原則設定適用於聯結的 tooan Active Directory 網域的 tooWindows 10 裝置。</span><span class="sxs-lookup"><span data-stu-id="c2ccd-122">hello Group Policy settings apply tooWindows 10 devices that are joined tooan Active Directory domain.</span></span> <span data-ttu-id="c2ccd-123">hello 資料表也包含舊設定，會出現 toomanage 同步處理設定，但不適用於企業狀態漫遊適用於 Windows 10，其會利用 '請勿使用' hello 描述中註明。</span><span class="sxs-lookup"><span data-stu-id="c2ccd-123">hello table also includes legacy settings that would appear toomanage sync settings, but that do not work for Enterprise State Roaming for Windows 10, which are noted with ‘Do not use’ in hello description.</span></span>

| <span data-ttu-id="c2ccd-124">名稱</span><span class="sxs-lookup"><span data-stu-id="c2ccd-124">Name</span></span> | <span data-ttu-id="c2ccd-125">說明</span><span class="sxs-lookup"><span data-stu-id="c2ccd-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c2ccd-126">帳戶：封鎖 Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="c2ccd-126">Accounts: Block Microsoft Accounts</span></span> |<span data-ttu-id="c2ccd-127">此原則設定會防止使用者在這部電腦上新增新的 Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="c2ccd-127">This policy setting prevents users from adding new Microsoft accounts on this computer</span></span> |
| <span data-ttu-id="c2ccd-128">不要同步處理</span><span class="sxs-lookup"><span data-stu-id="c2ccd-128">Do not sync</span></span> |<span data-ttu-id="c2ccd-129">防止使用者 tooroam Windows 設定和應用程式資料</span><span class="sxs-lookup"><span data-stu-id="c2ccd-129">Prevents users tooroam Windows settings and app data</span></span> |
| <span data-ttu-id="c2ccd-130">不要同步處理個人化</span><span class="sxs-lookup"><span data-stu-id="c2ccd-130">Do not sync personalize</span></span> |<span data-ttu-id="c2ccd-131">停用同步 hello 佈景主題的群組</span><span class="sxs-lookup"><span data-stu-id="c2ccd-131">Disables syncing of hello Themes group</span></span> |
| <span data-ttu-id="c2ccd-132">不要同步處理瀏覽器設定</span><span class="sxs-lookup"><span data-stu-id="c2ccd-132">Do not sync browser settings</span></span> |<span data-ttu-id="c2ccd-133">停用同步 hello Internet Explorer 的群組</span><span class="sxs-lookup"><span data-stu-id="c2ccd-133">Disables syncing of hello Internet Explorer group</span></span> |
| <span data-ttu-id="c2ccd-134">不要同步處理密碼</span><span class="sxs-lookup"><span data-stu-id="c2ccd-134">Do not sync passwords</span></span> |<span data-ttu-id="c2ccd-135">停用密碼群組的同步處理</span><span class="sxs-lookup"><span data-stu-id="c2ccd-135">Disables syncing of Passwords group</span></span> |
| <span data-ttu-id="c2ccd-136">不要同步處理其他 Windows 設定</span><span class="sxs-lookup"><span data-stu-id="c2ccd-136">Do not sync other Windows settings</span></span> |<span data-ttu-id="c2ccd-137">停用其他 Windows 設定群組的同步處理</span><span class="sxs-lookup"><span data-stu-id="c2ccd-137">Disables syncing of Other Windows settings group</span></span> |
| <span data-ttu-id="c2ccd-138">不要同步處理桌面個人化</span><span class="sxs-lookup"><span data-stu-id="c2ccd-138">Do not sync desktop personalization</span></span> |<span data-ttu-id="c2ccd-139">不要使用；沒有作用</span><span class="sxs-lookup"><span data-stu-id="c2ccd-139">Do not use; has no effect</span></span> |
| <span data-ttu-id="c2ccd-140">不要同步處理已計量連接</span><span class="sxs-lookup"><span data-stu-id="c2ccd-140">Do not sync on metered connections</span></span> |<span data-ttu-id="c2ccd-141">停用已計量連接的漫遊，例如行動電話 3G</span><span class="sxs-lookup"><span data-stu-id="c2ccd-141">Disables roaming on metered connections, such as cellular 3G</span></span> |
| <span data-ttu-id="c2ccd-142">不要同步處理應用程式</span><span class="sxs-lookup"><span data-stu-id="c2ccd-142">Do not sync apps</span></span> |<span data-ttu-id="c2ccd-143">不要使用；沒有作用</span><span class="sxs-lookup"><span data-stu-id="c2ccd-143">Do not use; has no effect</span></span> |
| <span data-ttu-id="c2ccd-144">不要同步處理應用程式設定</span><span class="sxs-lookup"><span data-stu-id="c2ccd-144">Do not sync app settings</span></span> |<span data-ttu-id="c2ccd-145">停用應用程式資料的漫遊</span><span class="sxs-lookup"><span data-stu-id="c2ccd-145">Disables roaming of app data</span></span> |
| <span data-ttu-id="c2ccd-146">不要同步處理啟動設定</span><span class="sxs-lookup"><span data-stu-id="c2ccd-146">Do not sync start settings</span></span> |<span data-ttu-id="c2ccd-147">不要使用；沒有作用</span><span class="sxs-lookup"><span data-stu-id="c2ccd-147">Do not use; has no effect</span></span> |

## <a name="related-topics"></a><span data-ttu-id="c2ccd-148">相關主題</span><span class="sxs-lookup"><span data-stu-id="c2ccd-148">Related topics</span></span>
* [<span data-ttu-id="c2ccd-149">企業狀態漫遊概觀</span><span class="sxs-lookup"><span data-stu-id="c2ccd-149">Enterprise State Roaming overview</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)
* [<span data-ttu-id="c2ccd-150">在 Azure Active Directory 中啟用企業狀態漫遊</span><span class="sxs-lookup"><span data-stu-id="c2ccd-150">Enable enterprise state roaming in Azure Active Directory</span></span>](active-directory-windows-enterprise-state-roaming-enable.md)
* [<span data-ttu-id="c2ccd-151">設定和資料漫遊常見問題集</span><span class="sxs-lookup"><span data-stu-id="c2ccd-151">Settings and data roaming FAQ</span></span>](active-directory-windows-enterprise-state-roaming-faqs.md)
* [<span data-ttu-id="c2ccd-152">Windows 10 漫遊設定參考</span><span class="sxs-lookup"><span data-stu-id="c2ccd-152">Windows 10 roaming settings reference</span></span>](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [<span data-ttu-id="c2ccd-153">疑難排解</span><span class="sxs-lookup"><span data-stu-id="c2ccd-153">Troubleshooting</span></span>](active-directory-windows-enterprise-state-roaming-troubleshooting.md)

