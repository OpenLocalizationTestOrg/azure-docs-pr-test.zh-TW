---
title: "Azure AD Connect：傳遞驗證 - 將預覽驗證代理程式升級 | Microsoft Docs"
description: "本文說明如何 tooupgrade 您的 Azure Active Directory (Azure AD) 的傳遞驗證設定。"
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
ms.openlocfilehash: 1695326b182278944e9f1584da72b18862b6ef27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-upgrade-preview-authentication-agents"></a><span data-ttu-id="8b18b-104">Azure Active Directory 傳遞驗證：將預覽驗證代理程式升級</span><span class="sxs-lookup"><span data-stu-id="8b18b-104">Azure Active Directory Pass-through Authentication: Upgrade preview Authentication Agents</span></span>

## <a name="overview"></a><span data-ttu-id="8b18b-105">概觀</span><span class="sxs-lookup"><span data-stu-id="8b18b-105">Overview</span></span>

<span data-ttu-id="8b18b-106">本文適用於透過預覽版使用 Azure AD 傳遞驗證的客戶。</span><span class="sxs-lookup"><span data-stu-id="8b18b-106">This article is for customers using Azure AD Pass-through Authentication through preview.</span></span> <span data-ttu-id="8b18b-107">我們最近已升級 （並重新命名） hello 驗證代理程式 」 軟體。</span><span class="sxs-lookup"><span data-stu-id="8b18b-107">We recently upgraded (and rebranded) hello Authentication Agent software.</span></span> <span data-ttu-id="8b18b-108">您需要 too_manually_ 升級預覽您的內部部署伺服器上安裝代理程式的驗證。</span><span class="sxs-lookup"><span data-stu-id="8b18b-108">You need too_manually_ upgrade preview Authentication Agents installed on your on-premises servers.</span></span> <span data-ttu-id="8b18b-109">此手動升級只是一次性動作。</span><span class="sxs-lookup"><span data-stu-id="8b18b-109">This manual upgrade is a one-time action only.</span></span> <span data-ttu-id="8b18b-110">所有未來的更新 tooAuthentication 代理程式是自動的。</span><span class="sxs-lookup"><span data-stu-id="8b18b-110">All future updates tooAuthentication Agents are automatic.</span></span> <span data-ttu-id="8b18b-111">hello 原因 tooupgrade 如下所示：</span><span class="sxs-lookup"><span data-stu-id="8b18b-111">hello reasons tooupgrade are as follows:</span></span>

- <span data-ttu-id="8b18b-112">任何進一步的安全性或 bug 修正，不會收到 hello 預覽版本驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="8b18b-112">hello preview versions of Authentication Agents will not receive any further security or bug fixes.</span></span>
-   <span data-ttu-id="8b18b-113">hello 預覽版本驗證代理程式無法安裝在其他伺服器，以進行高可用性。</span><span class="sxs-lookup"><span data-stu-id="8b18b-113">hello preview versions of Authentication Agents can't be installed on additional servers, for high availability.</span></span>

## <a name="check-versions-of-your-authentication-agents"></a><span data-ttu-id="8b18b-114">檢查驗證代理程式的版本</span><span class="sxs-lookup"><span data-stu-id="8b18b-114">Check versions of your Authentication Agents</span></span>

### <a name="step-1-check-where-your-authentication-agents-are-installed"></a><span data-ttu-id="8b18b-115">步驟 1：檢查驗證代理程式的安裝位置</span><span class="sxs-lookup"><span data-stu-id="8b18b-115">Step 1: Check where your Authentication Agents are installed</span></span>

<span data-ttu-id="8b18b-116">請遵循這些步驟 toocheck 驗證代理程式的安裝位置：</span><span class="sxs-lookup"><span data-stu-id="8b18b-116">Follow these steps toocheck where your Authentication Agents are installed:</span></span>

1. <span data-ttu-id="8b18b-117">登入 toohello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)hello 租用戶的全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="8b18b-117">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with hello Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="8b18b-118">選取**Azure Active Directory** hello 左側導覽上。</span><span class="sxs-lookup"><span data-stu-id="8b18b-118">Select **Azure Active Directory** on hello left-hand navigation.</span></span>
3. <span data-ttu-id="8b18b-119">選取 [Azure AD Connect]。</span><span class="sxs-lookup"><span data-stu-id="8b18b-119">Select **Azure AD Connect**.</span></span> 
4. <span data-ttu-id="8b18b-120">選取 [傳遞驗證]。</span><span class="sxs-lookup"><span data-stu-id="8b18b-120">Select **Pass-through Authentication**.</span></span> <span data-ttu-id="8b18b-121">此刀鋒視窗會列出 hello 伺服器驗證代理程式的安裝位置。</span><span class="sxs-lookup"><span data-stu-id="8b18b-121">This blade lists hello servers where your Authentication Agents are installed.</span></span>

![Azure Active Directory 管理中心 - 傳遞驗證刀鋒視窗](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

### <a name="step-2-check-hello-versions-of-your-authentication-agents"></a><span data-ttu-id="8b18b-123">步驟 2： 檢查 hello 版本驗證代理程式</span><span class="sxs-lookup"><span data-stu-id="8b18b-123">Step 2: Check hello versions of your Authentication Agents</span></span>

<span data-ttu-id="8b18b-124">toocheck hello 版本驗證代理程式，在 hello 前面步驟中，識別每個伺服器上遵循下列指示：</span><span class="sxs-lookup"><span data-stu-id="8b18b-124">toocheck hello versions of your Authentication Agents, on each server identified in hello preceding step, follow these instructions:</span></span>

1. <span data-ttu-id="8b18b-125">跳過**控制台]-> [程式]-> [程式和功能**hello 在內部部署伺服器上。</span><span class="sxs-lookup"><span data-stu-id="8b18b-125">Go too**Control Panel -> Programs -> Programs and Features** on hello on-premises server.</span></span>
2. <span data-ttu-id="8b18b-126">如果沒有的項目 」**Microsoft Azure AD Connect 驗證代理程式**」，您不需要 tootake 這部伺服器上的任何動作。</span><span class="sxs-lookup"><span data-stu-id="8b18b-126">If there is an entry for "**Microsoft Azure AD Connect Authentication Agent**", you don't need tootake any action on this server.</span></span>
3. <span data-ttu-id="8b18b-127">如果沒有的項目 」**Microsoft Azure AD 應用程式 Proxy 連接器**"，版本 1.5.132.0 或更早版本，您需要 toomanually 升級此伺服器上。</span><span class="sxs-lookup"><span data-stu-id="8b18b-127">If there is an entry for "**Microsoft Azure AD Application Proxy Connector**", versions 1.5.132.0 or earlier, you need toomanually upgrade on this server.</span></span>

![驗證代理程式的預覽版本](./media/active-directory-aadconnect-pass-through-authentication/pta6.png)

## <a name="best-practices-toofollow-before-starting-hello-upgrade"></a><span data-ttu-id="8b18b-129">最佳作法 toofollow 開始 hello 升級之前</span><span class="sxs-lookup"><span data-stu-id="8b18b-129">Best practices toofollow before starting hello upgrade</span></span>

<span data-ttu-id="8b18b-130">在升級之前，請確定您有下列項目就地 hello:</span><span class="sxs-lookup"><span data-stu-id="8b18b-130">Before upgrading, ensure that you have hello following items in place:</span></span>

1. <span data-ttu-id="8b18b-131">**建立僅限雲端的全域系統管理員帳戶**： 不升級而不需僅限雲端的全域管理員帳戶 toouse 在緊急情況下，您的傳遞驗證代理程式無法正常運作。</span><span class="sxs-lookup"><span data-stu-id="8b18b-131">**Create cloud-only Global Administrator account**: Don’t upgrade without having a cloud-only Global Administrator account toouse in emergency situations where your Pass-through Authentication Agents are not working properly.</span></span> <span data-ttu-id="8b18b-132">了解如何[新增僅限雲端管理員帳戶 (英文)](../active-directory-users-create-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="8b18b-132">Learn about [adding a cloud-only Global Administrator account](../active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="8b18b-133">這是確保您不會被租用戶封鎖的關鍵步驟。</span><span class="sxs-lookup"><span data-stu-id="8b18b-133">Doing this step is critical and ensures that you don't get locked out of your tenant.</span></span>
2.  <span data-ttu-id="8b18b-134">**確保高可用性**： 如果先前未完成，安裝的第二個獨立的登入要求，使用這些驗證代理程式 」 tooprovide 高可用性[指示](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability)。</span><span class="sxs-lookup"><span data-stu-id="8b18b-134">**Ensure high availability**: If not completed previously, install a second standalone Authentication Agent tooprovide high availability for sign-in requests, using these [instructions](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability).</span></span>

## <a name="upgrading-hello-authentication-agent-on-your-azure-ad-connect-server"></a><span data-ttu-id="8b18b-135">在您 Azure AD Connect 的伺服器上的升級 hello 驗證代理程式</span><span class="sxs-lookup"><span data-stu-id="8b18b-135">Upgrading hello Authentication Agent on your Azure AD Connect server</span></span>

<span data-ttu-id="8b18b-136">您必須升級 Azure AD Connect，才能升級 hello 驗證代理程式 」 在 hello 上的相同的伺服器。</span><span class="sxs-lookup"><span data-stu-id="8b18b-136">You need upgrade Azure AD Connect before upgrading hello Authentication Agent on hello same server.</span></span> <span data-ttu-id="8b18b-137">在主要伺服器和暫存 Azure AD Connect 伺服器上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8b18b-137">Follow these steps on both your primary and staging Azure AD Connect servers:</span></span>

1. <span data-ttu-id="8b18b-138">**升級 Azure AD Connect**： 後面要接著[文章](./active-directory-aadconnect-upgrade-previous-version.md)和 toohello 最新的 Azure AD Connect 版本升級。</span><span class="sxs-lookup"><span data-stu-id="8b18b-138">**Upgrade Azure AD Connect**: Follow this [article](./active-directory-aadconnect-upgrade-previous-version.md) and upgrade toohello latest Azure AD Connect version.</span></span>
2. <span data-ttu-id="8b18b-139">**解除安裝預覽版本，hello hello 驗證代理程式 」**： 下載[這個 PowerShell 指令碼](https://aka.ms/rmpreviewagent)和 hello 伺服器的系統管理員身分執行它。</span><span class="sxs-lookup"><span data-stu-id="8b18b-139">**Uninstall hello preview version of hello Authentication Agent**: Download [this PowerShell script](https://aka.ms/rmpreviewagent) and run it as an Administrator on hello server.</span></span>
3. <span data-ttu-id="8b18b-140">**下載 hello hello 驗證代理程式最新版本 (版本 1.5.193.0 或更新版本)**： 登入 toohello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)與您的租用戶全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="8b18b-140">**Download hello latest version of hello Authentication Agent (versions 1.5.193.0 or later)**: Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with your tenant's Global Administrator credentials.</span></span> <span data-ttu-id="8b18b-141">選取 [Azure Active Directory] -> [Azure AD Connect] -> [傳遞驗證] -> [下載代理程式]。</span><span class="sxs-lookup"><span data-stu-id="8b18b-141">Select **Azure Active Directory -> Azure AD Connect -> Pass-through Authentication -> Download agent**.</span></span> <span data-ttu-id="8b18b-142">接受服務條款 hello 和下載 hello hello 驗證代理程式最新版本。</span><span class="sxs-lookup"><span data-stu-id="8b18b-142">Accept hello terms of service and download hello latest version of hello Authentication Agent.</span></span>
4. <span data-ttu-id="8b18b-143">**Hello 最新版本的 hello 驗證代理程式安裝**： 在步驟 3 中下載的可執行檔執行 hello。</span><span class="sxs-lookup"><span data-stu-id="8b18b-143">**Install hello latest version of hello Authentication Agent**: Run hello executable downloaded in Step 3.</span></span> <span data-ttu-id="8b18b-144">出現提示時，提供您租用戶的全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="8b18b-144">Provide your tenant's Global Administrator credentials when prompted.</span></span>
5. <span data-ttu-id="8b18b-145">**確認是否已安裝，hello 最新版**： 如之前所示，跳過**控制台]-> [程式]-> [程式和功能**，並確認的項目 」**Microsoft Azure AD Connect驗證代理程式 」**"。</span><span class="sxs-lookup"><span data-stu-id="8b18b-145">**Verify that hello latest version has been installed**: As shown before, go too**Control Panel -> Programs -> Programs and Features** and verify that there is an entry for "**Microsoft Azure AD Connect Authentication Agent**".</span></span>

>[!NOTE]
><span data-ttu-id="8b18b-146">如果您核取 hello 傳遞驗證 刀鋒視窗上 hello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)之後完成 hello 先前步驟後，您會看到兩個驗證代理程式 」 項目，每一部伺服器-顯示 hello 的一個項目驗證代理程式 」 為**Active**和其他為 hello**非作用中**。</span><span class="sxs-lookup"><span data-stu-id="8b18b-146">If you check hello Pass-through Authentication blade on hello [Azure Active Directory admin center](https://aad.portal.azure.com) after  completing hello preceding steps, you'll see two Authentication Agent entries per server - one entry showing hello Authentication Agent as **Active** and hello other as **Inactive**.</span></span> <span data-ttu-id="8b18b-147">這是_預期行為_。</span><span class="sxs-lookup"><span data-stu-id="8b18b-147">This is _expected_.</span></span> <span data-ttu-id="8b18b-148">hello **Inactive**幾天後自動卸除項目。</span><span class="sxs-lookup"><span data-stu-id="8b18b-148">hello **Inactive** entry is automatically dropped after a few days.</span></span>

## <a name="upgrading-hello-authentication-agent-on-other-servers"></a><span data-ttu-id="8b18b-149">升級其他伺服器上的 hello 驗證代理程式</span><span class="sxs-lookup"><span data-stu-id="8b18b-149">Upgrading hello Authentication Agent on other servers</span></span>

<span data-ttu-id="8b18b-150">依照這些步驟 tooupgrade 驗證代理程式上的其他伺服器 （Azure AD Connect 但尚未安裝）：</span><span class="sxs-lookup"><span data-stu-id="8b18b-150">Follow these steps tooupgrade Authentication Agents on other servers (where Azure AD Connect is not installed):</span></span>

1. <span data-ttu-id="8b18b-151">**解除安裝預覽版本，hello hello 驗證代理程式 」**： 下載[這個 PowerShell 指令碼](https://aka.ms/rmpreviewagent)和 hello 伺服器的系統管理員身分執行它。</span><span class="sxs-lookup"><span data-stu-id="8b18b-151">**Uninstall hello preview version of hello Authentication Agent**: Download [this PowerShell script](https://aka.ms/rmpreviewagent) and run it as an Administrator on hello server.</span></span>
2. <span data-ttu-id="8b18b-152">**下載 hello hello 驗證代理程式最新版本 (版本 1.5.193.0 或更新版本)**： 登入 toohello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)與您的租用戶全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="8b18b-152">**Download hello latest version of hello Authentication Agent (versions 1.5.193.0 or later)**: Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with your tenant's Global Administrator credentials.</span></span> <span data-ttu-id="8b18b-153">選取 [Azure Active Directory] -> [Azure AD Connect] -> [傳遞驗證] -> [下載代理程式]。</span><span class="sxs-lookup"><span data-stu-id="8b18b-153">Select **Azure Active Directory -> Azure AD Connect -> Pass-through Authentication -> Download agent**.</span></span> <span data-ttu-id="8b18b-154">接受服務條款 hello 和下載 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="8b18b-154">Accept hello terms of service and download hello latest version.</span></span>
3. <span data-ttu-id="8b18b-155">**Hello 最新版本的 hello 驗證代理程式安裝**： 在步驟 2 中的可執行檔執行 hello 下載。</span><span class="sxs-lookup"><span data-stu-id="8b18b-155">**Install hello latest version of hello Authentication Agent**: Run hello executable downloaded in Step 2.</span></span> <span data-ttu-id="8b18b-156">出現提示時，提供您租用戶的全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="8b18b-156">Provide your tenant's Global Administrator credentials when prompted.</span></span>
4. <span data-ttu-id="8b18b-157">**確認是否已安裝，hello 最新版**： 如之前所示，跳過**控制台]-> [程式]-> [程式和功能**，並確認呼叫的項目**Microsoft Azure AD Connect驗證代理程式 」**。</span><span class="sxs-lookup"><span data-stu-id="8b18b-157">**Verify that hello latest version has been installed**: As shown before, go too**Control Panel -> Programs -> Programs and Features** and verify that there is an entry called **Microsoft Azure AD Connect Authentication Agent**.</span></span>

>[!NOTE]
><span data-ttu-id="8b18b-158">如果您核取 hello 傳遞驗證 刀鋒視窗上 hello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)之後完成 hello 先前步驟後，您會看到兩個驗證代理程式 」 項目，每一部伺服器-顯示 hello 的一個項目驗證代理程式 」 為**Active**和其他為 hello**非作用中**。</span><span class="sxs-lookup"><span data-stu-id="8b18b-158">If you check hello Pass-through Authentication blade on hello [Azure Active Directory admin center](https://aad.portal.azure.com) after  completing hello preceding steps, you'll see two Authentication Agent entries per server - one entry showing hello Authentication Agent as **Active** and hello other as **Inactive**.</span></span> <span data-ttu-id="8b18b-159">這是_預期行為_。</span><span class="sxs-lookup"><span data-stu-id="8b18b-159">This is _expected_.</span></span> <span data-ttu-id="8b18b-160">hello **Inactive**幾天後自動卸除項目。</span><span class="sxs-lookup"><span data-stu-id="8b18b-160">hello **Inactive** entry is automatically dropped after a few days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b18b-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8b18b-161">Next steps</span></span>
- <span data-ttu-id="8b18b-162">[**疑難排解**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -了解如何 tooresolve 常見問題與 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="8b18b-162">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
