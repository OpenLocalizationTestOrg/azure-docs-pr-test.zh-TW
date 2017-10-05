---
title: "針對使用 Azure AD Connect 同步執行的密碼同步處理進行疑難排解 | Microsoft Docs"
description: "本文提供如何針對密碼同步化問題進行疑難排解的相關資訊。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 33fa6a8867764975a57b8727e7705529d1d7506a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="1ee8e-103">針對使用 Azure AD Connect 同步執行的密碼同步處理進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="1ee8e-103">Troubleshoot password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="1ee8e-104">本主題提供如何針對密碼同步處理問題進行疑難排解的步驟。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-104">This topic provides steps for how to troubleshoot issues with password synchronization.</span></span> <span data-ttu-id="1ee8e-105">如果密碼未如預期般同步，可能會影響一部分使用者或所有使用者。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span></span> <span data-ttu-id="1ee8e-106">對於 1.1.524.0 版或更新版本的 Azure Active directory (Azure AD) Connect 部署，現在有一個診斷 Cmdlet 可讓您針對密碼同步化問題進行疑難排解：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.524.0 or later, there is now a diagnostic cmdlet that you can use to troubleshoot password synchronization issues:</span></span>

* <span data-ttu-id="1ee8e-107">如果是未同步任何密碼的問題，請參閱[未同步任何密碼：使用診斷 Cmdlet 進行疑難排解](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet)一節。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-107">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: troubleshoot by using the diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

* <span data-ttu-id="1ee8e-108">如果是個別物件的問題，請參閱[一個物件未同步密碼：使用診斷 Cmdlet 進行疑難排解](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet)一節。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-108">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

<span data-ttu-id="1ee8e-109">舊版的 Azure AD Connect 部署：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-109">For older versions of Azure AD Connect deployment:</span></span>

* <span data-ttu-id="1ee8e-110">如果是未同步任何密碼的問題，請參閱[未同步任何密碼：手動疑難排解步驟](#no-passwords-are-synchronized-manual-troubleshooting-steps)一節。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-110">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span></span>

* <span data-ttu-id="1ee8e-111">如果是個別物件的問題，請參閱[一個物件未同步密碼：手動疑難排解步驟](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps)一節。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-111">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span></span>

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet"></a><span data-ttu-id="1ee8e-112">未同步任何密碼：使用診斷 Cmdlet 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="1ee8e-112">No passwords are synchronized: troubleshoot by using the diagnostic cmdlet</span></span>
<span data-ttu-id="1ee8e-113">您可以使用 `Invoke-ADSyncDiagnostics` Cmdlet 來查明未同步任何密碼的原因。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-113">You can use the `Invoke-ADSyncDiagnostics` cmdlet to figure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="1ee8e-114">`Invoke-ADSyncDiagnostics` Cmdlet 僅適用於 Azure AD Connect 1.1.524.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-114">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-the-diagnostics-cmdlet"></a><span data-ttu-id="1ee8e-115">執行診斷 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="1ee8e-115">Run the diagnostics cmdlet</span></span>
<span data-ttu-id="1ee8e-116">針對未同步任何密碼的問題進行疑難排解：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-116">To troubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="1ee8e-117">在您的 Azure AD Connect 伺服器上，使用 [以系統管理員身分執行] 選項開啟新的 Windows PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-117">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="1ee8e-118">執行 `Set-ExecutionPolicy RemoteSigned` 或 `Set-ExecutionPolicy Unrestricted`。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-118">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="1ee8e-119">執行 `Import-Module ADSyncDiagnostics`。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-119">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="1ee8e-120">執行 `Invoke-ADSyncDiagnostics -PasswordSync`。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-120">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span></span>

### <a name="understand-the-results-of-the-cmdlet"></a><span data-ttu-id="1ee8e-121">了解 Cmdlet 的結果</span><span class="sxs-lookup"><span data-stu-id="1ee8e-121">Understand the results of the cmdlet</span></span>
<span data-ttu-id="1ee8e-122">診斷 Cmdlet 會執行下列檢查：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-122">The diagnostic cmdlet performs the following checks:</span></span>

* <span data-ttu-id="1ee8e-123">確認您的 Azure AD 租用戶已啟用密碼同步化功能。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-123">Validates that the password synchronization feature is enabled for your Azure AD tenant.</span></span>

* <span data-ttu-id="1ee8e-124">確認 Azure AD Connect 伺服器不是處於預備模式。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-124">Validates that the Azure AD Connect server is not in staging mode.</span></span>

* <span data-ttu-id="1ee8e-125">針對每個現有的內部部署 Active Directory 連接器 (對應至現有的 Active Directory 樹系)：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-125">For each existing on-premises Active Directory connector (which corresponds to an existing Active Directory forest):</span></span>

   * <span data-ttu-id="1ee8e-126">確認密碼同步化功能已啟用。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-126">Validates that the password synchronization feature is enabled.</span></span>
   
   * <span data-ttu-id="1ee8e-127">在 Windows 應用程式事件記錄中搜尋密碼同步化活動訊號事件。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-127">Searches for password synchronization heartbeat events in the Windows Application Event logs.</span></span>

   * <span data-ttu-id="1ee8e-128">針對內部部署 Active Directory 連接器下的每個 Active Directory 網域：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-128">For each Active Directory domain under the on-premises Active Directory connector:</span></span>

      * <span data-ttu-id="1ee8e-129">確認可從 Azure AD Connect 伺服器存取網域。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-129">Validates that the domain is reachable from the Azure AD Connect server.</span></span>

      * <span data-ttu-id="1ee8e-130">確認內部部署 Active Directory 連接器所使用的 Active Directory Domain Services (AD DS) 帳戶，具有密碼同步化所需的正確使用者名稱、密碼和權限。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-130">Validates that the Active Directory Domain Services (AD DS) accounts used by the on-premises Active Directory connector has the correct username, password, and permissions required for password synchronization.</span></span>

<span data-ttu-id="1ee8e-131">下圖說明在單一網域、內部部署 Active Directory 拓撲上，執行此 Cmdlet 的結果：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-131">The following diagram illustrates the results of the cmdlet for a single-domain, on-premises Active Directory topology:</span></span>

![密碼同步化的診斷輸出](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

<span data-ttu-id="1ee8e-133">本節的其餘部分說明 Cmdlet 所傳回的特定結果和對應的問題。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-133">The rest of this section describes specific results that are returned by the cmdlet and corresponding issues.</span></span>

#### <a name="password-synchronization-feature-isnt-enabled"></a><span data-ttu-id="1ee8e-134">密碼同步化功能未啟用</span><span class="sxs-lookup"><span data-stu-id="1ee8e-134">Password synchronization feature isn't enabled</span></span>
<span data-ttu-id="1ee8e-135">如果您尚未使用 Azure AD Connect 精靈來啟用密碼同步化，則會傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-135">If you haven't enabled password synchronization by using the Azure AD Connect wizard, the following error is returned:</span></span>

![密碼同步化未啟用](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a><span data-ttu-id="1ee8e-137">Azure AD Connect 伺服器處於預備模式</span><span class="sxs-lookup"><span data-stu-id="1ee8e-137">Azure AD Connect server is in staging mode</span></span>
<span data-ttu-id="1ee8e-138">如果 Azure AD Connect 伺服器處於預備模式，則會暫時停用密碼同步化，也會傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-138">If the Azure AD Connect server is in staging mode, password synchronization is temporarily disabled, and the following error is returned:</span></span>

![Azure AD Connect 伺服器處於預備模式](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a><span data-ttu-id="1ee8e-140">沒有密碼同步化活動訊號事件</span><span class="sxs-lookup"><span data-stu-id="1ee8e-140">No password synchronization heartbeat events</span></span>
<span data-ttu-id="1ee8e-141">每個內部部署 Active Directory 連接器各有自己的密碼同步化通道。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-141">Each on-premises Active Directory connector has its own password synchronization channel.</span></span> <span data-ttu-id="1ee8e-142">當密碼同步化通道已建立，而且沒有任何密碼變更需要同步時，Windows 應用程式事件記錄下每隔 30 分鐘會產生一次活動訊號事件 (EventId 654)。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-142">When the password synchronization channel is established and there aren't any password changes to be synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under the Windows Application Event Log.</span></span> <span data-ttu-id="1ee8e-143">對於每個內部部署 Active Directory 連接器，此 Cmdlet 會搜尋過去三小時內對應的活動訊號事件。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-143">For each on-premises Active Directory connector, the cmdlet searches for corresponding heartbeat events in the past three hours.</span></span> <span data-ttu-id="1ee8e-144">如果找不到活動訊號事件，則會傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-144">If no heartbeat event is found, the following error is returned:</span></span>

![沒有密碼同步化活動訊號事件](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a><span data-ttu-id="1ee8e-146">AD DS 帳戶沒有正確的權限</span><span class="sxs-lookup"><span data-stu-id="1ee8e-146">AD DS account does not have correct permissions</span></span>
<span data-ttu-id="1ee8e-147">如果內部部署 Active Directory 連接器用來同步密碼雜湊的 AD DS 帳戶沒有適當的權限，則會傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-147">If the AD DS account that's used by the on-premises Active Directory connector to synchronize password hashes does not have the appropriate permissions, the following error is returned:</span></span>

![不正確的認證](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a><span data-ttu-id="1ee8e-149">不正確的 AD DS 帳戶使用者名稱或密碼</span><span class="sxs-lookup"><span data-stu-id="1ee8e-149">Incorrect AD DS account username or password</span></span>
<span data-ttu-id="1ee8e-150">如果內部部署 Active Directory 連接器用來同步密碼雜湊的 AD DS 帳戶有不正確的使用者名稱或密碼，則會傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-150">If the AD DS account used by the on-premises Active Directory connector to synchronize password hashes has an incorrect username or password, the following error is returned:</span></span>

![不正確的認證](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet"></a><span data-ttu-id="1ee8e-152">一個物件未同步密碼：使用診斷 Cmdlet 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="1ee8e-152">One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet</span></span>
<span data-ttu-id="1ee8e-153">您可以使用 `Invoke-ADSyncDiagnostics` Cmdlet 來判斷一個物件未同步密碼的原因。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-153">You can use the `Invoke-ADSyncDiagnostics` cmdlet to determine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="1ee8e-154">`Invoke-ADSyncDiagnostics` Cmdlet 僅適用於 Azure AD Connect 1.1.524.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-154">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-the-diagnostics-cmdlet"></a><span data-ttu-id="1ee8e-155">執行診斷 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="1ee8e-155">Run the diagnostics cmdlet</span></span>
<span data-ttu-id="1ee8e-156">針對未同步任何密碼的問題進行疑難排解：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-156">To troubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="1ee8e-157">在您的 Azure AD Connect 伺服器上，使用 [以系統管理員身分執行] 選項開啟新的 Windows PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-157">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="1ee8e-158">執行 `Set-ExecutionPolicy RemoteSigned` 或 `Set-ExecutionPolicy Unrestricted`。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-158">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="1ee8e-159">執行 `Import-Module ADSyncDiagnostics`。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-159">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="1ee8e-160">執行下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-160">Run the following cmdlet:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   <span data-ttu-id="1ee8e-161">例如：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-161">For example:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-the-results-of-the-cmdlet"></a><span data-ttu-id="1ee8e-162">了解 Cmdlet 的結果</span><span class="sxs-lookup"><span data-stu-id="1ee8e-162">Understand the results of the cmdlet</span></span>
<span data-ttu-id="1ee8e-163">診斷 Cmdlet 會執行下列檢查：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-163">The diagnostic cmdlet performs the following checks:</span></span>

* <span data-ttu-id="1ee8e-164">在 Active Directory 連接器空間、Metaverse 和 Azure AD 連接器空間中，檢查 Active Directory 物件的狀態。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-164">Examines the state of the Active Directory object in the Active Directory connector space, Metaverse, and Azure AD connector space.</span></span>

* <span data-ttu-id="1ee8e-165">確認有已啟用密碼同步化的同步化規則，且已套用至 Active Directory 物件。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-165">Validates that there are synchronization rules with password synchronization enabled and applied to the Active Directory object.</span></span>

* <span data-ttu-id="1ee8e-166">試著擷取並顯示上次嘗試同步物件密碼的結果。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-166">Attempts to retrieve and display the results of the last attempt to synchronize the password for the object.</span></span>

<span data-ttu-id="1ee8e-167">下圖說明針對單一物件的密碼同步化進行疑難排解時，執行此 Cmdlet 的結果：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-167">The following diagram illustrates the results of the cmdlet when troubleshooting password synchronization for a single object:</span></span>

![密碼同步化的診斷輸出 - 單一物件](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

<span data-ttu-id="1ee8e-169">本節的其餘部分說明 Cmdlet 所傳回的特定結果和對應的問題。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-169">The rest of this section describes specific results returned by the cmdlet and corresponding issues.</span></span>

#### <a name="the-active-directory-object-isnt-exported-to-azure-ad"></a><span data-ttu-id="1ee8e-170">Active Directory 物件未匯出至 Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ee8e-170">The Active Directory object isn't exported to Azure AD</span></span>
<span data-ttu-id="1ee8e-171">因為 Azure AD 租用戶中沒有對應的物件，這個內部部署 Active Directory 帳戶的密碼同步化失敗。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-171">Password synchronization for this on-premises Active Directory account fails because there is no corresponding object in the Azure AD tenant.</span></span> <span data-ttu-id="1ee8e-172">傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-172">The following error is returned:</span></span>

![遺漏 Azure AD 物件](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a><span data-ttu-id="1ee8e-174">使用者有暫時密碼</span><span class="sxs-lookup"><span data-stu-id="1ee8e-174">User has a temporary password</span></span>
<span data-ttu-id="1ee8e-175">目前，Azure AD Connect 不支援與 Azure AD 同步暫時密碼。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-175">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span></span> <span data-ttu-id="1ee8e-176">如果對內部部署 Active Directory 使用者設定 [在下次登入時變更密碼] 選項，密碼就視為暫時。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-176">A password is considered to be temporary if the **Change password at next logon** option is set on the on-premises Active Directory user.</span></span> <span data-ttu-id="1ee8e-177">傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-177">The following error is returned:</span></span>

![未匯出暫時密碼](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-to-synchronize-password-arent-available"></a><span data-ttu-id="1ee8e-179">上次嘗試同步密碼沒有結果</span><span class="sxs-lookup"><span data-stu-id="1ee8e-179">Results of last attempt to synchronize password aren't available</span></span>
<span data-ttu-id="1ee8e-180">根據預設，Azure AD Connect 會密碼同步化嘗試的結果保存七天。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-180">By default, Azure AD Connect stores the results of password synchronization attempts for seven days.</span></span> <span data-ttu-id="1ee8e-181">如果選取的 Active Directory 物件沒有可用的結果，則會傳回下列警告：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-181">If there are no results available for the selected Active Directory object, the following warning is returned:</span></span>

![單一物件的診斷輸出 - 沒有密碼同步記錄](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a><span data-ttu-id="1ee8e-183">未同步任何密碼：手動疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="1ee8e-183">No passwords are synchronized: manual troubleshooting steps</span></span>
<span data-ttu-id="1ee8e-184">請依照下列步驟來判斷未同步任何密碼的原因：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-184">Follow these steps to determine why no passwords are synchronized:</span></span>

1. <span data-ttu-id="1ee8e-185">Connect 伺服器是否是處於[預備模式](active-directory-aadconnectsync-operations.md#staging-mode)？</span><span class="sxs-lookup"><span data-stu-id="1ee8e-185">Is the Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="1ee8e-186">處於預備模式的伺服器不會同步處理任何密碼。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-186">A server in staging mode does not synchronize any passwords.</span></span>

2. <span data-ttu-id="1ee8e-187">執行[取得密碼同步設定的狀態](#get-the-status-of-password-sync-settings)一節中的指令碼。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-187">Run the script in the [Get the status of password sync settings](#get-the-status-of-password-sync-settings) section.</span></span> <span data-ttu-id="1ee8e-188">它可讓您大致了解密碼同步設定作業。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-188">It gives you an overview of the password sync configuration.</span></span>  

    ![來自密碼同步設定的 PowerShell 指令碼輸出](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. <span data-ttu-id="1ee8e-190">如果 Azure AD 中未啟用此功能，或未啟用同步通道狀態，請執行 Connect 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-190">If the feature is not enabled in Azure AD or if the sync channel status is not enabled, run the Connect installation wizard.</span></span> <span data-ttu-id="1ee8e-191">選取 [自訂同步處理選項] 並取消選取密碼同步。這項變更會暫時停用此功能。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-191">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables the feature.</span></span> <span data-ttu-id="1ee8e-192">然後再次執行精靈並重新啟用密碼同步處理。再次執行指令碼，確認組態正確無誤。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-192">Then run the wizard again and re-enable password sync. Run the script again to verify that the configuration is correct.</span></span>

4. <span data-ttu-id="1ee8e-193">查看事件記錄中是否有錯誤。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-193">Look in the event log for errors.</span></span> <span data-ttu-id="1ee8e-194">尋找下列事件，這些事件會指出問題所在︰</span><span class="sxs-lookup"><span data-stu-id="1ee8e-194">Look for the following events, which would indicate a problem:</span></span>
    * <span data-ttu-id="1ee8e-195">來源：「目錄同步作業」識別碼：0、611、652、655。如果您看到這些事件，即表示有連線問題。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-195">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span></span> <span data-ttu-id="1ee8e-196">事件記錄訊息包含發生問題的樹系資訊。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-196">The event log message contains forest information where you have a problem.</span></span> <span data-ttu-id="1ee8e-197">如需詳細資訊，請參閱[連線問題](#connectivity problem)。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-197">For more information, see [Connectivity problem](#connectivity problem).</span></span>

5. <span data-ttu-id="1ee8e-198">如果您沒有看到任何活動訊號，或任何其他操作都沒有作用，請執行[觸發所有密碼的完整同步](#trigger-a-full-sync-of-all-passwords)。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-198">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="1ee8e-199">只執行一次指令碼。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-199">Run the script only once.</span></span>

6. <span data-ttu-id="1ee8e-200">請參閱[針對一個未同步密碼的物件進行疑難排解](#one-object-is-not-synchronizing-passwords)一節。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-200">See the [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span></span>

### <a name="connectivity-problems"></a><span data-ttu-id="1ee8e-201">連線問題</span><span class="sxs-lookup"><span data-stu-id="1ee8e-201">Connectivity problems</span></span>

<span data-ttu-id="1ee8e-202">您是否能夠與 Azure AD 連線？</span><span class="sxs-lookup"><span data-stu-id="1ee8e-202">Do you have connectivity with Azure AD?</span></span>

<span data-ttu-id="1ee8e-203">帳戶是否具備可讀取所有網域中密碼雜湊的必要權限？</span><span class="sxs-lookup"><span data-stu-id="1ee8e-203">Does the account have required permissions to read the password hashes in all domains?</span></span> <span data-ttu-id="1ee8e-204">如果您使用 [快速設定] 來安裝 Connect，權限應該已經正確。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-204">If you installed Connect by using Express settings, the permissions should already be correct.</span></span> 

<span data-ttu-id="1ee8e-205">如果您使用自訂安裝，請執行下列動作來手動設定權限：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-205">If you used custom installation, set the permissions manually by doing the following:</span></span>
    
1. <span data-ttu-id="1ee8e-206">若要尋找 Active Directory 連接器所使用的帳戶，請啟動 **Synchronization Service Manager**。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-206">To find the account used by the Active Directory connector, start **Synchronization Service Manager**.</span></span> 
 
2. <span data-ttu-id="1ee8e-207">移至 [連接器]，然後尋找您要進行疑難排解的內部部署 Active Directory 樹系。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-207">Go to **Connectors**, and then search for the on-premises Active Directory forest you are troubleshooting.</span></span> 
 
3. <span data-ttu-id="1ee8e-208">選取 [連接器]，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-208">Select the connector, and then click **Properties**.</span></span> 
 
4. <span data-ttu-id="1ee8e-209">前往 [連線至 Active Directory 樹系] 。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-209">Go to **Connect to Active Directory Forest**.</span></span>  
    
    ![Active Directory 連接器所使用的帳戶](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    <span data-ttu-id="1ee8e-211">記下使用者名稱和帳戶所在的網域。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-211">Note the username and the domain where the account is located.</span></span>
    
5. <span data-ttu-id="1ee8e-212">啟動 **Active Directory 使用者和電腦**，然後確認您稍早發現的帳戶，已在樹系中所有網域的根目錄上設定下列權限：</span><span class="sxs-lookup"><span data-stu-id="1ee8e-212">Start **Active Directory Users and Computers**, and then verify that the account you found earlier has the follow permissions set at the root of all domains in your forest:</span></span>
    * <span data-ttu-id="1ee8e-213">複寫目錄變更</span><span class="sxs-lookup"><span data-stu-id="1ee8e-213">Replicate Directory Changes</span></span>
    * <span data-ttu-id="1ee8e-214">複寫目錄變更 (全部)</span><span class="sxs-lookup"><span data-stu-id="1ee8e-214">Replicate Directory Changes All</span></span>

6. <span data-ttu-id="1ee8e-215">Azure AD Connect 是否可以連線到網域控制站？</span><span class="sxs-lookup"><span data-stu-id="1ee8e-215">Are the domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="1ee8e-216">如果 Connect 伺服器無法連線到所有網域控制站，請設定 [只使用慣用的網域控制站]。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-216">If the Connect server cannot connect to all domain controllers, configure **Only use preferred domain controller**.</span></span>  
    
    ![Active Directory 連接器所使用的網域控制站](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. <span data-ttu-id="1ee8e-218">返回 **Synchronization Service Manager**，並**設定目錄磁碟分割**。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-218">Go back to **Synchronization Service Manager** and **Configure Directory Partition**.</span></span> 
 
8. <span data-ttu-id="1ee8e-219">在 [選取目錄分割] 中選取您的網域，選取 [只使用慣用的網域控制站] 核取方塊，然後按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-219">Select your domain in **Select directory partitions**, select the **Only use preferred domain controllers** check box, and then click **Configure**.</span></span> 

9. <span data-ttu-id="1ee8e-220">在清單中，輸入 Connect 應該用來進行密碼同步的網域控制站。此相同清單也用於匯入和匯出。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-220">In the list, enter the domain controllers that Connect should use for password sync. The same list is used for import and export as well.</span></span> <span data-ttu-id="1ee8e-221">針對您的所有網域執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-221">Do these steps for all your domains.</span></span>

10. <span data-ttu-id="1ee8e-222">如果此指令碼顯示沒有活動訊號，請執行[觸發所有密碼的完整同步](#trigger-a-full-sync-of-all-passwords)中的指令碼。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-222">If the script shows that there is no heartbeat, run the script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a><span data-ttu-id="1ee8e-223">一個物件未同步密碼：手動疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="1ee8e-223">One object is not synchronizing passwords: manual troubleshooting steps</span></span>
<span data-ttu-id="1ee8e-224">您可以藉由檢閱物件的狀態，輕鬆地疑難排解密碼同步處理問題。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-224">You can easily troubleshoot password synchronization issues by reviewing the status of an object.</span></span>

1. <span data-ttu-id="1ee8e-225">在 **Active Directory 使用者和電腦**中，搜尋使用者，然後確認已清除 [使用者必須在下次登入時變更密碼] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-225">In **Active Directory Users and Computers**, search for the user, and then verify that the **User must change password at next logon** check box is cleared.</span></span>  

    ![Active Directory 生產力密碼](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    <span data-ttu-id="1ee8e-227">如果選取此核取方塊，請要求使用者登入並變更密碼。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-227">If the check box is selected, ask the user to sign in and change the password.</span></span> <span data-ttu-id="1ee8e-228">暫時密碼不會與 Azure AD 同步。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-228">Temporary passwords are not synchronized with Azure AD.</span></span>

2. <span data-ttu-id="1ee8e-229">如果 Active Directory 中的密碼看起來正確，請在同步處理引擎中追蹤使用者。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-229">If the password looks correct in Active Directory, follow the user in the sync engine.</span></span> <span data-ttu-id="1ee8e-230">從內部部署 Active Directory 到 Azure AD 追蹤使用者，就能知道物件是否有描述性錯誤。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-230">By following the user from on-premises Active Directory to Azure AD, you can see whether there is a descriptive error on the object.</span></span>

    <span data-ttu-id="1ee8e-231">a.</span><span class="sxs-lookup"><span data-stu-id="1ee8e-231">a.</span></span> <span data-ttu-id="1ee8e-232">啟動 [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md)。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-232">Start the [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

    <span data-ttu-id="1ee8e-233">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-233">b.</span></span> <span data-ttu-id="1ee8e-234">按一下 [連接器] 。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-234">Click **Connectors**.</span></span>

    <span data-ttu-id="1ee8e-235">c.</span><span class="sxs-lookup"><span data-stu-id="1ee8e-235">c.</span></span> <span data-ttu-id="1ee8e-236">選取使用者所在的 **Active Directory 連接器**。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-236">Select the **Active Directory Connector** where the user is located.</span></span>

    <span data-ttu-id="1ee8e-237">d.</span><span class="sxs-lookup"><span data-stu-id="1ee8e-237">d.</span></span> <span data-ttu-id="1ee8e-238">選取 [搜尋連接器空間] 。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-238">Select **Search Connector Space**.</span></span>

    <span data-ttu-id="1ee8e-239">e.</span><span class="sxs-lookup"><span data-stu-id="1ee8e-239">e.</span></span> <span data-ttu-id="1ee8e-240">在 [範圍] 方塊中，選取 [DN 或錨點]，然後輸入您要進行疑難排解之使用者的完整 DN。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-240">In the **Scope** box, select **DN or Anchor**, and then enter the full DN of the user you are troubleshooting.</span></span>

    ![在連接器空間中依 DN 搜尋使用者](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    <span data-ttu-id="1ee8e-242">f.</span><span class="sxs-lookup"><span data-stu-id="1ee8e-242">f.</span></span> <span data-ttu-id="1ee8e-243">找出您要搜尋的使用者，然後按一下 [屬性] 來查看所有屬性。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-243">Locate the user you are looking for, and then click **Properties** to see all the attributes.</span></span> <span data-ttu-id="1ee8e-244">如果該使用者不在搜尋結果中，請確認您的[篩選規則](active-directory-aadconnectsync-configure-filtering.md)，且務必執行[套用並驗證變更](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes)，如此 Connect 中才會顯示該使用者。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-244">If the user is not in the search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for the user to appear in Connect.</span></span>

    <span data-ttu-id="1ee8e-245">g.</span><span class="sxs-lookup"><span data-stu-id="1ee8e-245">g.</span></span> <span data-ttu-id="1ee8e-246">若要查看物件在過去一週的密碼同步詳細資料，請按一下 [記錄]。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-246">To see the password sync details of the object for the past week, click **Log**.</span></span>  

    ![物件記錄詳細資料](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    <span data-ttu-id="1ee8e-248">如果物件記錄是空的，則表示 Azure AD Connect 無法從 Active Directory 讀取密碼雜湊。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-248">If the object log is empty, Azure AD Connect has been unable to read the password hash from Active Directory.</span></span> <span data-ttu-id="1ee8e-249">請繼續進行[連線錯誤](#connectivity-errors)疑難排解。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-249">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="1ee8e-250">如果您看到 [成功] 以外的任何其他值，請參考[密碼同步記錄](#password-sync-log)中的表格。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-250">If you see any other value than **success**, refer to the table in [Password sync log](#password-sync-log).</span></span>

    <span data-ttu-id="1ee8e-251">h.</span><span class="sxs-lookup"><span data-stu-id="1ee8e-251">h.</span></span> <span data-ttu-id="1ee8e-252">選取 [歷程] 索引標籤，並確認至少有一個同步規則的 [PasswordSync] 資料行是 **True**。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-252">Select the **lineage** tab, and make sure that at least one sync rule in the **PasswordSync** column is **True**.</span></span> <span data-ttu-id="1ee8e-253">在預設組態中，同步規則的名稱是 **In from AD - User AccountEnabled**。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-253">In the default configuration, the name of the sync rule is **In from AD - User AccountEnabled**.</span></span>  

    ![使用者的相關歷程資訊](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    <span data-ttu-id="1ee8e-255">i.</span><span class="sxs-lookup"><span data-stu-id="1ee8e-255">i.</span></span> <span data-ttu-id="1ee8e-256">按一下 [Metaverse 物件屬性] 來顯示使用者屬性清單。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-256">Click **Metaverse Object Properties** to display a list of user attributes.</span></span>  

    ![Metaverse 資訊](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    <span data-ttu-id="1ee8e-258">確認沒有任何 **cloudFiltered** 屬性存在。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-258">Verify that there is no **cloudFiltered** attribute present.</span></span> <span data-ttu-id="1ee8e-259">確定網域屬性 (domainFQDN 和 domainNetBios) 具有預期的值。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-259">Make sure that the domain attributes (domainFQDN and domainNetBios) have the expected values.</span></span>

    <span data-ttu-id="1ee8e-260">j.</span><span class="sxs-lookup"><span data-stu-id="1ee8e-260">j.</span></span> <span data-ttu-id="1ee8e-261">按一下 [連接器] 索引標籤。請確定您看到已連線至內部部署 Active Directory 和 Azure AD 的連接器。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-261">Click the **Connectors** tab. Make sure that you see connectors to both on-premises Active Directory and Azure AD.</span></span>

    ![Metaverse 資訊](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    <span data-ttu-id="1ee8e-263">k.</span><span class="sxs-lookup"><span data-stu-id="1ee8e-263">k.</span></span> <span data-ttu-id="1ee8e-264">選取代表 Azure AD 的資料列，按一下 [屬性]，然後按一下 [歷程] 索引標籤。連接器空間物件應該有一個輸出規則的 [PasswordSync] 資料行設為 **True**。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-264">Select the row that represents Azure AD, click **Properties**, and then click the **Lineage** tab. The connector space object should have an outbound rule in the **PasswordSync** column set to **True**.</span></span> <span data-ttu-id="1ee8e-265">在預設組態中，同步規則的名稱是 **Out to AAD - User Join**。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-265">In the default configuration, the name of the sync rule is **Out to AAD - User Join**.</span></span>  

    ![連接器空間物件屬性對話方塊](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a><span data-ttu-id="1ee8e-267">密碼同步記錄</span><span class="sxs-lookup"><span data-stu-id="1ee8e-267">Password sync log</span></span>
<span data-ttu-id="1ee8e-268">[狀態] 欄可以有下列值︰</span><span class="sxs-lookup"><span data-stu-id="1ee8e-268">The status column can have the following values:</span></span>

| <span data-ttu-id="1ee8e-269">狀態</span><span class="sxs-lookup"><span data-stu-id="1ee8e-269">Status</span></span> | <span data-ttu-id="1ee8e-270">說明</span><span class="sxs-lookup"><span data-stu-id="1ee8e-270">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1ee8e-271">成功</span><span class="sxs-lookup"><span data-stu-id="1ee8e-271">Success</span></span> |<span data-ttu-id="1ee8e-272">已成功同步處理密碼。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-272">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="1ee8e-273">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="1ee8e-273">FilteredByTarget</span></span> |<span data-ttu-id="1ee8e-274">密碼會設為 [使用者必須在下次登入時變更密碼] 。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-274">Password is set to **User must change password at next logon**.</span></span> <span data-ttu-id="1ee8e-275">未同步處理密碼。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-275">Password has not been synchronized.</span></span> |
| <span data-ttu-id="1ee8e-276">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="1ee8e-276">NoTargetConnection</span></span> |<span data-ttu-id="1ee8e-277">Metaverse 或 Azure AD 連接器空間中沒有任何物件。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-277">No object in the metaverse or in the Azure AD connector space.</span></span> |
| <span data-ttu-id="1ee8e-278">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="1ee8e-278">SourceConnectorNotPresent</span></span> |<span data-ttu-id="1ee8e-279">在內部部署 Active Directory 連接器空間中找不到任何物件。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-279">No object found in the on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="1ee8e-280">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="1ee8e-280">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="1ee8e-281">尚未匯出 Azure AD 連接器空間中的物件。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-281">The object in the Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="1ee8e-282">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="1ee8e-282">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="1ee8e-283">記錄項目建立於組建 1.0.9125.0 之前，並且以其舊版的狀態顯示。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-283">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |
| <span data-ttu-id="1ee8e-284">錯誤</span><span class="sxs-lookup"><span data-stu-id="1ee8e-284">Error</span></span> |<span data-ttu-id="1ee8e-285">服務傳回未知的錯誤。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-285">Service returned an unknown error.</span></span> |
| <span data-ttu-id="1ee8e-286">不明</span><span class="sxs-lookup"><span data-stu-id="1ee8e-286">Unknown</span></span> |<span data-ttu-id="1ee8e-287">嘗試處理密碼雜湊的批次時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-287">An error occurred while trying to process a batch of password hashes.</span></span>  |
| <span data-ttu-id="1ee8e-288">MissingAttribute</span><span class="sxs-lookup"><span data-stu-id="1ee8e-288">MissingAttribute</span></span> |<span data-ttu-id="1ee8e-289">無法使用 Azure AD Domain Services 所需的特定屬性 (例如，Kerberos 雜湊)。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-289">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span></span> |
| <span data-ttu-id="1ee8e-290">RetryRequestedByTarget</span><span class="sxs-lookup"><span data-stu-id="1ee8e-290">RetryRequestedByTarget</span></span> |<span data-ttu-id="1ee8e-291">先前無法使用 Azure AD Domain Services 所需的特定屬性 (例如，Kerberos 雜湊)。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-291">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span></span> <span data-ttu-id="1ee8e-292">會嘗試重新同步處理使用者的密碼雜湊。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-292">An attempt to resynchronize the user's password hash is made.</span></span> |

## <a name="scripts-to-help-troubleshooting"></a><span data-ttu-id="1ee8e-293">協助疑難排解的指令碼</span><span class="sxs-lookup"><span data-stu-id="1ee8e-293">Scripts to help troubleshooting</span></span>

### <a name="get-the-status-of-password-sync-settings"></a><span data-ttu-id="1ee8e-294">取得密碼同步設定的狀態</span><span class="sxs-lookup"><span data-stu-id="1ee8e-294">Get the status of password sync settings</span></span>
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update the script to use the appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="1ee8e-295">觸發所有密碼的完整同步處理</span><span class="sxs-lookup"><span data-stu-id="1ee8e-295">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="1ee8e-296">只執行一次這個指令碼。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-296">Run this script only once.</span></span> <span data-ttu-id="1ee8e-297">如果需要執行多次，則表示問題出在其他地方。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-297">If you need to run it more than once, something else is the problem.</span></span> <span data-ttu-id="1ee8e-298">若要針對問題進行疑難排解，請連絡 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="1ee8e-298">To troubleshoot the problem, contact Microsoft support.</span></span>

<span data-ttu-id="1ee8e-299">您可以使用下列指令碼來觸發所有密碼的完整同步︰</span><span class="sxs-lookup"><span data-stu-id="1ee8e-299">You can trigger a full sync of all passwords by using the following script:</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a><span data-ttu-id="1ee8e-300">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1ee8e-300">Next steps</span></span>
* [<span data-ttu-id="1ee8e-301">使用 Azure AD Connect 同步處理實作密碼同步處理</span><span class="sxs-lookup"><span data-stu-id="1ee8e-301">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md)
* [<span data-ttu-id="1ee8e-302">Azure AD Connect 同步：自訂同步處理選項</span><span class="sxs-lookup"><span data-stu-id="1ee8e-302">Azure AD Connect Sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="1ee8e-303">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ee8e-303">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
