---
title: "Azure AD Connect：傳遞驗證 - 將預覽驗證代理程式升級 | Microsoft Docs"
description: "本文說明如何將 Azure Active Directory (Azure AD) 傳遞驗證組態升級。"
services: active-directory
keywords: "Azure AD Connect 傳遞驗證, 安裝 Active Directory, Azure AD 的必要元件, SSO, 單一登入"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 940cb4466ef5d730c42d04d0107f6901f55eb155
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-upgrade-preview-authentication-agents"></a><span data-ttu-id="5d415-104">Azure Active Directory 傳遞驗證：將預覽驗證代理程式升級</span><span class="sxs-lookup"><span data-stu-id="5d415-104">Azure Active Directory Pass-through Authentication: Upgrade preview Authentication Agents</span></span>

## <a name="overview"></a><span data-ttu-id="5d415-105">概觀</span><span class="sxs-lookup"><span data-stu-id="5d415-105">Overview</span></span>

<span data-ttu-id="5d415-106">本文適用於透過預覽版使用 Azure AD 傳遞驗證的客戶。</span><span class="sxs-lookup"><span data-stu-id="5d415-106">This article is for customers using Azure AD Pass-through Authentication through preview.</span></span> <span data-ttu-id="5d415-107">我們最近已將驗證代理程式軟體升級 (及改版)。</span><span class="sxs-lookup"><span data-stu-id="5d415-107">We recently upgraded (and rebranded) the Authentication Agent software.</span></span> <span data-ttu-id="5d415-108">您需要_手動_升級在內部部署伺服器上安裝的預覽驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="5d415-108">You need to _manually_ upgrade preview Authentication Agents installed on your on-premises servers.</span></span> <span data-ttu-id="5d415-109">此手動升級只是一次性動作。</span><span class="sxs-lookup"><span data-stu-id="5d415-109">This manual upgrade is a one-time action only.</span></span> <span data-ttu-id="5d415-110">驗證代理程式的所有未來更新都是自動的。</span><span class="sxs-lookup"><span data-stu-id="5d415-110">All future updates to Authentication Agents are automatic.</span></span> <span data-ttu-id="5d415-111">升級的原因如下所示：</span><span class="sxs-lookup"><span data-stu-id="5d415-111">The reasons to upgrade are as follows:</span></span>

- <span data-ttu-id="5d415-112">預覽版的驗證代理程式不會收到任何進一步的安全性或錯誤修正。</span><span class="sxs-lookup"><span data-stu-id="5d415-112">The preview versions of Authentication Agents will not receive any further security or bug fixes.</span></span>
-   <span data-ttu-id="5d415-113">預覽版的驗證代理程式無法安裝在其他伺服器上，以獲得高可用性。</span><span class="sxs-lookup"><span data-stu-id="5d415-113">The preview versions of Authentication Agents can't be installed on additional servers, for high availability.</span></span>

## <a name="check-versions-of-your-authentication-agents"></a><span data-ttu-id="5d415-114">檢查驗證代理程式的版本</span><span class="sxs-lookup"><span data-stu-id="5d415-114">Check versions of your Authentication Agents</span></span>

### <a name="step-1-check-where-your-authentication-agents-are-installed"></a><span data-ttu-id="5d415-115">步驟 1：檢查驗證代理程式的安裝位置</span><span class="sxs-lookup"><span data-stu-id="5d415-115">Step 1: Check where your Authentication Agents are installed</span></span>

<span data-ttu-id="5d415-116">遵循下列步驟來檢查驗證代理程式的安裝位置：</span><span class="sxs-lookup"><span data-stu-id="5d415-116">Follow these steps to check where your Authentication Agents are installed:</span></span>

1. <span data-ttu-id="5d415-117">使用租用戶的全域管理員認證來登入 [Azure Active Directory 管理中心](https://aad.portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5d415-117">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with the Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="5d415-118">按一下左側導覽上的 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="5d415-118">Select **Azure Active Directory** on the left-hand navigation.</span></span>
3. <span data-ttu-id="5d415-119">選取 [Azure AD Connect]。</span><span class="sxs-lookup"><span data-stu-id="5d415-119">Select **Azure AD Connect**.</span></span> 
4. <span data-ttu-id="5d415-120">選取 [傳遞驗證]。</span><span class="sxs-lookup"><span data-stu-id="5d415-120">Select **Pass-through Authentication**.</span></span> <span data-ttu-id="5d415-121">此刀鋒視窗會列出驗證代理程式的安裝位置。</span><span class="sxs-lookup"><span data-stu-id="5d415-121">This blade lists the servers where your Authentication Agents are installed.</span></span>

![Azure Active Directory 管理中心 - 傳遞驗證刀鋒視窗](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

### <a name="step-2-check-the-versions-of-your-authentication-agents"></a><span data-ttu-id="5d415-123">步驟 2：檢查驗證代理程式的版本</span><span class="sxs-lookup"><span data-stu-id="5d415-123">Step 2: Check the versions of your Authentication Agents</span></span>

<span data-ttu-id="5d415-124">若要檢查驗證代理程式的版本，請在前一個步驟中識別的每部伺服器上，依照下列指示操作：</span><span class="sxs-lookup"><span data-stu-id="5d415-124">To check the versions of your Authentication Agents, on each server identified in the preceding step, follow these instructions:</span></span>

1. <span data-ttu-id="5d415-125">移至內部部署伺服器上的 [控制台]-> [程式]-> [程式和功能]。</span><span class="sxs-lookup"><span data-stu-id="5d415-125">Go to **Control Panel -> Programs -> Programs and Features** on the on-premises server.</span></span>
2. <span data-ttu-id="5d415-126">如果有「Microsoft Azure AD Connect 驗證代理程式」項目，您就不需要在此伺服器上採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="5d415-126">If there is an entry for "**Microsoft Azure AD Connect Authentication Agent**", you don't need to take any action on this server.</span></span>
3. <span data-ttu-id="5d415-127">如果有「Microsoft Azure AD Application Proxy Connector」項目 (版本 1.5.132.0 或更早版本)，您需要在此伺服器上以手動方式進行升級。</span><span class="sxs-lookup"><span data-stu-id="5d415-127">If there is an entry for "**Microsoft Azure AD Application Proxy Connector**", versions 1.5.132.0 or earlier, you need to manually upgrade on this server.</span></span>

![驗證代理程式的預覽版本](./media/active-directory-aadconnect-pass-through-authentication/pta6.png)

## <a name="best-practices-to-follow-before-starting-the-upgrade"></a><span data-ttu-id="5d415-129">開始升級之前所應遵循的最佳做法</span><span class="sxs-lookup"><span data-stu-id="5d415-129">Best practices to follow before starting the upgrade</span></span>

<span data-ttu-id="5d415-130">升級之前，請確定您已備妥下列項目：</span><span class="sxs-lookup"><span data-stu-id="5d415-130">Before upgrading, ensure that you have the following items in place:</span></span>

1. <span data-ttu-id="5d415-131">**建立僅限雲端的全域管理員帳戶**：在傳遞驗證代理程式無法正常運作的緊急情況下，若沒有僅限雲端的全域管理員帳戶可使用，則不要升級。</span><span class="sxs-lookup"><span data-stu-id="5d415-131">**Create cloud-only Global Administrator account**: Don’t upgrade without having a cloud-only Global Administrator account to use in emergency situations where your Pass-through Authentication Agents are not working properly.</span></span> <span data-ttu-id="5d415-132">了解如何[新增僅限雲端管理員帳戶 (英文)](../active-directory-users-create-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="5d415-132">Learn about [adding a cloud-only Global Administrator account](../active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="5d415-133">這是確保您不會被租用戶封鎖的關鍵步驟。</span><span class="sxs-lookup"><span data-stu-id="5d415-133">Doing this step is critical and ensures that you don't get locked out of your tenant.</span></span>
2.  <span data-ttu-id="5d415-134">**確保高可用性**：如果先前未完成，則使用相關[指示](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability)來安裝第二個獨立驗證代理程式，以提供高可用性來滿足登入要求。</span><span class="sxs-lookup"><span data-stu-id="5d415-134">**Ensure high availability**: If not completed previously, install a second standalone Authentication Agent to provide high availability for sign-in requests, using these [instructions](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability).</span></span>

## <a name="upgrading-the-authentication-agent-on-your-azure-ad-connect-server"></a><span data-ttu-id="5d415-135">將 Azure AD Connect 伺服器上的驗證代理程式升級</span><span class="sxs-lookup"><span data-stu-id="5d415-135">Upgrading the Authentication Agent on your Azure AD Connect server</span></span>

<span data-ttu-id="5d415-136">您必須先升級 Azure AD Connect，才能在同一部伺服器上升級驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="5d415-136">You need upgrade Azure AD Connect before upgrading the Authentication Agent on the same server.</span></span> <span data-ttu-id="5d415-137">在主要伺服器和暫存 Azure AD Connect 伺服器上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5d415-137">Follow these steps on both your primary and staging Azure AD Connect servers:</span></span>

1. <span data-ttu-id="5d415-138">**升級 Azure AD Connect**：依照[本文](./active-directory-aadconnect-upgrade-previous-version.md)操作並升級至最新版的 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="5d415-138">**Upgrade Azure AD Connect**: Follow this [article](./active-directory-aadconnect-upgrade-previous-version.md) and upgrade to the latest Azure AD Connect version.</span></span>
2. <span data-ttu-id="5d415-139">**解除預覽版的安裝驗證代理程式**：下載[此 PowerShell 指令碼](https://aka.ms/rmpreviewagent)並在伺服器上以系統管理員身分執行該指令碼。</span><span class="sxs-lookup"><span data-stu-id="5d415-139">**Uninstall the preview version of the Authentication Agent**: Download [this PowerShell script](https://aka.ms/rmpreviewagent) and run it as an Administrator on the server.</span></span>
3. <span data-ttu-id="5d415-140">**下載最新版的驗證代理程式 (1.5.193.0 版或更新版本)**：使用您租用戶的全域管理員認證登入 [Azure Active Directory 管理中心](https://aad.portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5d415-140">**Download the latest version of the Authentication Agent (versions 1.5.193.0 or later)**: Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with your tenant's Global Administrator credentials.</span></span> <span data-ttu-id="5d415-141">選取 [Azure Active Directory] -> [Azure AD Connect] -> [傳遞驗證] -> [下載代理程式]。</span><span class="sxs-lookup"><span data-stu-id="5d415-141">Select **Azure Active Directory -> Azure AD Connect -> Pass-through Authentication -> Download agent**.</span></span> <span data-ttu-id="5d415-142">接受服務條款並下載最新版的驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="5d415-142">Accept the terms of service and download the latest version of the Authentication Agent.</span></span>
4. <span data-ttu-id="5d415-143">**安裝最新版的驗證代理程式**：執行在步驟 3 中下載的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="5d415-143">**Install the latest version of the Authentication Agent**: Run the executable downloaded in Step 3.</span></span> <span data-ttu-id="5d415-144">出現提示時，提供您租用戶的全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="5d415-144">Provide your tenant's Global Administrator credentials when prompted.</span></span>
5. <span data-ttu-id="5d415-145">**已安裝最新版本**：如之前所示，請移至 [控制台]-> [程式]-> [程式和功能]，並確認有 [Microsoft Azure AD Connect 驗證代理程式] 項目。</span><span class="sxs-lookup"><span data-stu-id="5d415-145">**Verify that the latest version has been installed**: As shown before, go to **Control Panel -> Programs -> Programs and Features** and verify that there is an entry for "**Microsoft Azure AD Connect Authentication Agent**".</span></span>

>[!NOTE]
><span data-ttu-id="5d415-146">完成前述步驟後，若到 [Azure Active Directory 管理中心](https://aad.portal.azure.com)查看傳遞驗證刀鋒視窗，將會發現每個伺服器有兩個驗證代理程式項目：一個項目會顯示驗證代理程式為**使用中**，另一個則顯示為**非使用中**。</span><span class="sxs-lookup"><span data-stu-id="5d415-146">If you check the Pass-through Authentication blade on the [Azure Active Directory admin center](https://aad.portal.azure.com) after  completing the preceding steps, you'll see two Authentication Agent entries per server - one entry showing the Authentication Agent as **Active** and the other as **Inactive**.</span></span> <span data-ttu-id="5d415-147">這是_預期行為_。</span><span class="sxs-lookup"><span data-stu-id="5d415-147">This is _expected_.</span></span> <span data-ttu-id="5d415-148">**非使用中**的項目會在幾天後自動卸除。</span><span class="sxs-lookup"><span data-stu-id="5d415-148">The **Inactive** entry is automatically dropped after a few days.</span></span>

## <a name="upgrading-the-authentication-agent-on-other-servers"></a><span data-ttu-id="5d415-149">在其他伺服器上升級驗證代理程式</span><span class="sxs-lookup"><span data-stu-id="5d415-149">Upgrading the Authentication Agent on other servers</span></span>

<span data-ttu-id="5d415-150">在其他伺服器 (未安裝 Azure AD Connect) 上依照下列步驟來升級驗證代理程式：</span><span class="sxs-lookup"><span data-stu-id="5d415-150">Follow these steps to upgrade Authentication Agents on other servers (where Azure AD Connect is not installed):</span></span>

1. <span data-ttu-id="5d415-151">**解除預覽版的安裝驗證代理程式**：下載[此 PowerShell 指令碼](https://aka.ms/rmpreviewagent)並在伺服器上以系統管理員身分執行該指令碼。</span><span class="sxs-lookup"><span data-stu-id="5d415-151">**Uninstall the preview version of the Authentication Agent**: Download [this PowerShell script](https://aka.ms/rmpreviewagent) and run it as an Administrator on the server.</span></span>
2. <span data-ttu-id="5d415-152">**下載最新版的驗證代理程式 (1.5.193.0 版或更新版本)**：使用您租用戶的全域管理員認證登入 [Azure Active Directory 管理中心](https://aad.portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5d415-152">**Download the latest version of the Authentication Agent (versions 1.5.193.0 or later)**: Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with your tenant's Global Administrator credentials.</span></span> <span data-ttu-id="5d415-153">選取 [Azure Active Directory] -> [Azure AD Connect] -> [傳遞驗證] -> [下載代理程式]。</span><span class="sxs-lookup"><span data-stu-id="5d415-153">Select **Azure Active Directory -> Azure AD Connect -> Pass-through Authentication -> Download agent**.</span></span> <span data-ttu-id="5d415-154">接受服務條款並下載最新版本。</span><span class="sxs-lookup"><span data-stu-id="5d415-154">Accept the terms of service and download the latest version.</span></span>
3. <span data-ttu-id="5d415-155">**安裝最新版的驗證代理程式**：執行在步驟 2 中下載的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="5d415-155">**Install the latest version of the Authentication Agent**: Run the executable downloaded in Step 2.</span></span> <span data-ttu-id="5d415-156">出現提示時，提供您租用戶的全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="5d415-156">Provide your tenant's Global Administrator credentials when prompted.</span></span>
4. <span data-ttu-id="5d415-157">**已安裝最新版本**：如之前所示，請移至 [控制台]-> [程式]-> [程式和功能]，並確認有一個叫做 [Microsoft Azure AD Connect 驗證代理程式] 的項目。</span><span class="sxs-lookup"><span data-stu-id="5d415-157">**Verify that the latest version has been installed**: As shown before, go to **Control Panel -> Programs -> Programs and Features** and verify that there is an entry called **Microsoft Azure AD Connect Authentication Agent**.</span></span>

>[!NOTE]
><span data-ttu-id="5d415-158">完成前述步驟後，若到 [Azure Active Directory 管理中心](https://aad.portal.azure.com)查看傳遞驗證刀鋒視窗，將會發現每個伺服器有兩個驗證代理程式項目：一個項目會顯示驗證代理程式為**使用中**，另一個則顯示為**非使用中**。</span><span class="sxs-lookup"><span data-stu-id="5d415-158">If you check the Pass-through Authentication blade on the [Azure Active Directory admin center](https://aad.portal.azure.com) after  completing the preceding steps, you'll see two Authentication Agent entries per server - one entry showing the Authentication Agent as **Active** and the other as **Inactive**.</span></span> <span data-ttu-id="5d415-159">這是_預期行為_。</span><span class="sxs-lookup"><span data-stu-id="5d415-159">This is _expected_.</span></span> <span data-ttu-id="5d415-160">**非使用中**的項目會在幾天後自動卸除。</span><span class="sxs-lookup"><span data-stu-id="5d415-160">The **Inactive** entry is automatically dropped after a few days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d415-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d415-161">Next steps</span></span>
- <span data-ttu-id="5d415-162">[**疑難排解**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - 了解如何解決此功能的常見問題。</span><span class="sxs-lookup"><span data-stu-id="5d415-162">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
