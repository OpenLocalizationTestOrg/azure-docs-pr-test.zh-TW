---
title: "搭配 Azure AD Connect 同步化 aaaTroubleshoot 密碼同步化 |Microsoft 文件"
description: "這篇文章提供有關如何資訊 tootroubleshoot 密碼同步處理問題。"
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
ms.openlocfilehash: 390eafec792cb39251627c14cb754f8bb30035b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="0451a-103">針對使用 Azure AD Connect 同步執行的密碼同步處理進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="0451a-103">Troubleshoot password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="0451a-104">本主題提供如何 tootroubleshoot 發出密碼同步處理步驟。</span><span class="sxs-lookup"><span data-stu-id="0451a-104">This topic provides steps for how tootroubleshoot issues with password synchronization.</span></span> <span data-ttu-id="0451a-105">如果密碼未如預期般同步，可能會影響一部分使用者或所有使用者。</span><span class="sxs-lookup"><span data-stu-id="0451a-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span></span> <span data-ttu-id="0451a-106">Azure Active directory (Azure AD) 連線版本 1.1.524.0 部署，或更新版本中，目前已診斷的指令程式，您可以使用 tootroubleshoot 密碼同步處理的問題：</span><span class="sxs-lookup"><span data-stu-id="0451a-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.524.0 or later, there is now a diagnostic cmdlet that you can use tootroubleshoot password synchronization issues:</span></span>

* <span data-ttu-id="0451a-107">如果您有問題會在同步處理沒有密碼，請參閱 toohello[沒有密碼會同步處理： 使用 hello 診斷的指令程式來進行疑難排解](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet)> 一節。</span><span class="sxs-lookup"><span data-stu-id="0451a-107">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

* <span data-ttu-id="0451a-108">如果您有個別的物件發生問題，請參閱 toohello[一個物件不會同步處理密碼： 使用 hello 診斷的指令程式來進行疑難排解](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet)> 一節。</span><span class="sxs-lookup"><span data-stu-id="0451a-108">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

<span data-ttu-id="0451a-109">舊版的 Azure AD Connect 部署：</span><span class="sxs-lookup"><span data-stu-id="0451a-109">For older versions of Azure AD Connect deployment:</span></span>

* <span data-ttu-id="0451a-110">如果您有問題會在同步處理沒有密碼，請參閱 toohello[沒有密碼會同步處理： 疑難排解步驟的手動](#no-passwords-are-synchronized-manual-troubleshooting-steps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="0451a-110">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span></span>

* <span data-ttu-id="0451a-111">如果您有個別的物件發生問題，請參閱 toohello[一個物件不會同步處理密碼： 疑難排解步驟的手動](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="0451a-111">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span></span>

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="0451a-112">不會將密碼同步處理： 使用 hello 診斷的指令程式來進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="0451a-112">No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="0451a-113">您可以使用 hello `Invoke-ADSyncDiagnostics` cmdlet toofigure 出為什麼沒有密碼會同步處理。</span><span class="sxs-lookup"><span data-stu-id="0451a-113">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toofigure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="0451a-114">hello `Invoke-ADSyncDiagnostics` cmdlet 是僅適用於 Azure AD Connect 版本 1.1.524.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="0451a-114">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="0451a-115">執行 hello 診斷 cmdlet</span><span class="sxs-lookup"><span data-stu-id="0451a-115">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="0451a-116">會在同步處理不會將密碼 tootroubleshoot 問題：</span><span class="sxs-lookup"><span data-stu-id="0451a-116">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="0451a-117">開啟新的 Windows PowerShell 工作階段，在您 Azure AD Connect 的伺服器上以 hello**系統管理員身分執行**選項。</span><span class="sxs-lookup"><span data-stu-id="0451a-117">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="0451a-118">執行 `Set-ExecutionPolicy RemoteSigned` 或 `Set-ExecutionPolicy Unrestricted`。</span><span class="sxs-lookup"><span data-stu-id="0451a-118">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="0451a-119">執行 `Import-Module ADSyncDiagnostics`。</span><span class="sxs-lookup"><span data-stu-id="0451a-119">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="0451a-120">執行 `Invoke-ADSyncDiagnostics -PasswordSync`。</span><span class="sxs-lookup"><span data-stu-id="0451a-120">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span></span>

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="0451a-121">了解 hello cmdlet 的 hello 結果</span><span class="sxs-lookup"><span data-stu-id="0451a-121">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="0451a-122">hello 診斷 cmdlet 會執行下列檢查 hello:</span><span class="sxs-lookup"><span data-stu-id="0451a-122">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="0451a-123">會驗證該 hello Azure AD 租用戶啟用密碼同步處理功能。</span><span class="sxs-lookup"><span data-stu-id="0451a-123">Validates that hello password synchronization feature is enabled for your Azure AD tenant.</span></span>

* <span data-ttu-id="0451a-124">會驗證該 hello Azure AD Connect 伺服器不是預備模式。</span><span class="sxs-lookup"><span data-stu-id="0451a-124">Validates that hello Azure AD Connect server is not in staging mode.</span></span>

* <span data-ttu-id="0451a-125">針對每個現有的內部部署 Active Directory 連接器 （其對應 tooan 現有 Active Directory 樹系）：</span><span class="sxs-lookup"><span data-stu-id="0451a-125">For each existing on-premises Active Directory connector (which corresponds tooan existing Active Directory forest):</span></span>

   * <span data-ttu-id="0451a-126">會驗證該 hello 啟用密碼同步處理功能。</span><span class="sxs-lookup"><span data-stu-id="0451a-126">Validates that hello password synchronization feature is enabled.</span></span>
   
   * <span data-ttu-id="0451a-127">密碼同步處理活動訊號中的事件 hello 搜尋 Windows 應用程式事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0451a-127">Searches for password synchronization heartbeat events in hello Windows Application Event logs.</span></span>

   * <span data-ttu-id="0451a-128">每個 Active Directory 網域下 hello 在內部部署 Active Directory 連接器：</span><span class="sxs-lookup"><span data-stu-id="0451a-128">For each Active Directory domain under hello on-premises Active Directory connector:</span></span>

      * <span data-ttu-id="0451a-129">會驗證該 hello 網域可從 hello Azure AD Connect 的伺服器連線。</span><span class="sxs-lookup"><span data-stu-id="0451a-129">Validates that hello domain is reachable from hello Azure AD Connect server.</span></span>

      * <span data-ttu-id="0451a-130">驗證 hello hello 在內部部署 Active Directory 連接器所使用的 Active Directory 網域服務 (AD DS) 帳戶具有 hello 正確的使用者名稱、 密碼和密碼同步處理所需的權限。</span><span class="sxs-lookup"><span data-stu-id="0451a-130">Validates that hello Active Directory Domain Services (AD DS) accounts used by hello on-premises Active Directory connector has hello correct username, password, and permissions required for password synchronization.</span></span>

<span data-ttu-id="0451a-131">hello 下列圖表說明單一網域，在內部部署 Active Directory 拓樸的 hello cmdlet 的 hello 的結果：</span><span class="sxs-lookup"><span data-stu-id="0451a-131">hello following diagram illustrates hello results of hello cmdlet for a single-domain, on-premises Active Directory topology:</span></span>

![密碼同步化的診斷輸出](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

<span data-ttu-id="0451a-133">hello 本節其餘部分將說明特定 hello cmdlet 所傳回的結果和對應的問題。</span><span class="sxs-lookup"><span data-stu-id="0451a-133">hello rest of this section describes specific results that are returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="password-synchronization-feature-isnt-enabled"></a><span data-ttu-id="0451a-134">密碼同步化功能未啟用</span><span class="sxs-lookup"><span data-stu-id="0451a-134">Password synchronization feature isn't enabled</span></span>
<span data-ttu-id="0451a-135">如果您尚未使用 hello Azure AD Connect 精靈啟用密碼同步處理，會傳回下列錯誤 hello:</span><span class="sxs-lookup"><span data-stu-id="0451a-135">If you haven't enabled password synchronization by using hello Azure AD Connect wizard, hello following error is returned:</span></span>

![密碼同步化未啟用](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a><span data-ttu-id="0451a-137">Azure AD Connect 伺服器處於預備模式</span><span class="sxs-lookup"><span data-stu-id="0451a-137">Azure AD Connect server is in staging mode</span></span>
<span data-ttu-id="0451a-138">如果正在預備模式 hello Azure AD Connect 的伺服器，暫時停用密碼同步處理，並 hello 會傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="0451a-138">If hello Azure AD Connect server is in staging mode, password synchronization is temporarily disabled, and hello following error is returned:</span></span>

![Azure AD Connect 伺服器處於預備模式](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a><span data-ttu-id="0451a-140">沒有密碼同步化活動訊號事件</span><span class="sxs-lookup"><span data-stu-id="0451a-140">No password synchronization heartbeat events</span></span>
<span data-ttu-id="0451a-141">每個內部部署 Active Directory 連接器各有自己的密碼同步化通道。</span><span class="sxs-lookup"><span data-stu-id="0451a-141">Each on-premises Active Directory connector has its own password synchronization channel.</span></span> <span data-ttu-id="0451a-142">當建立 hello 密碼同步處理通道，而且沒有任何同步處理的密碼變更 toobe 時，活動訊號事件 (EventId 654) 會產生一次每隔 30 分鐘在 hello Windows 應用程式事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0451a-142">When hello password synchronization channel is established and there aren't any password changes toobe synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under hello Windows Application Event Log.</span></span> <span data-ttu-id="0451a-143">每個內部部署 Active Directory 連接器 hello 指令程式會搜尋 hello 中對應的活動訊號事件過去三小時內。</span><span class="sxs-lookup"><span data-stu-id="0451a-143">For each on-premises Active Directory connector, hello cmdlet searches for corresponding heartbeat events in hello past three hours.</span></span> <span data-ttu-id="0451a-144">如果不找到任何活動訊號的事件，hello 會傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="0451a-144">If no heartbeat event is found, hello following error is returned:</span></span>

![沒有密碼同步化活動訊號事件](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a><span data-ttu-id="0451a-146">AD DS 帳戶沒有正確的權限</span><span class="sxs-lookup"><span data-stu-id="0451a-146">AD DS account does not have correct permissions</span></span>
<span data-ttu-id="0451a-147">如果使用 hello hello AD DS 帳戶內部部署 Active Directory 連接器 toosynchronize 密碼雜湊並沒有 hello 適當的權限，hello 會傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="0451a-147">If hello AD DS account that's used by hello on-premises Active Directory connector toosynchronize password hashes does not have hello appropriate permissions, hello following error is returned:</span></span>

![不正確的認證](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a><span data-ttu-id="0451a-149">不正確的 AD DS 帳戶使用者名稱或密碼</span><span class="sxs-lookup"><span data-stu-id="0451a-149">Incorrect AD DS account username or password</span></span>
<span data-ttu-id="0451a-150">如果 hello AD DS 帳戶由 hello 在內部部署 Active Directory 連接器 toosynchronize 密碼雜湊不正確的使用者名稱或密碼，hello 會傳回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="0451a-150">If hello AD DS account used by hello on-premises Active Directory connector toosynchronize password hashes has an incorrect username or password, hello following error is returned:</span></span>

![不正確的認證](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="0451a-152">一個物件不會同步處理密碼： 使用 hello 診斷的指令程式來進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="0451a-152">One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="0451a-153">您可以使用 hello `Invoke-ADSyncDiagnostics` cmdlet toodetermine 為什麼一個物件並未同步處理密碼。</span><span class="sxs-lookup"><span data-stu-id="0451a-153">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toodetermine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="0451a-154">hello `Invoke-ADSyncDiagnostics` cmdlet 是僅適用於 Azure AD Connect 版本 1.1.524.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="0451a-154">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="0451a-155">執行 hello 診斷 cmdlet</span><span class="sxs-lookup"><span data-stu-id="0451a-155">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="0451a-156">會在同步處理不會將密碼 tootroubleshoot 問題：</span><span class="sxs-lookup"><span data-stu-id="0451a-156">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="0451a-157">開啟新的 Windows PowerShell 工作階段，在您 Azure AD Connect 的伺服器上以 hello**系統管理員身分執行**選項。</span><span class="sxs-lookup"><span data-stu-id="0451a-157">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="0451a-158">執行 `Set-ExecutionPolicy RemoteSigned` 或 `Set-ExecutionPolicy Unrestricted`。</span><span class="sxs-lookup"><span data-stu-id="0451a-158">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="0451a-159">執行 `Import-Module ADSyncDiagnostics`。</span><span class="sxs-lookup"><span data-stu-id="0451a-159">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="0451a-160">執行下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="0451a-160">Run hello following cmdlet:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   <span data-ttu-id="0451a-161">例如：</span><span class="sxs-lookup"><span data-stu-id="0451a-161">For example:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="0451a-162">了解 hello cmdlet 的 hello 結果</span><span class="sxs-lookup"><span data-stu-id="0451a-162">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="0451a-163">hello 診斷 cmdlet 會執行下列檢查 hello:</span><span class="sxs-lookup"><span data-stu-id="0451a-163">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="0451a-164">Hello hello Active Directory 連接器空間、 Metaverse 和 Azure 中的 hello Active Directory 物件狀態會檢查 AD 連接器空間。</span><span class="sxs-lookup"><span data-stu-id="0451a-164">Examines hello state of hello Active Directory object in hello Active Directory connector space, Metaverse, and Azure AD connector space.</span></span>

* <span data-ttu-id="0451a-165">驗證已啟用密碼同步處理的同步處理規則，並套用 toohello Active Directory 物件。</span><span class="sxs-lookup"><span data-stu-id="0451a-165">Validates that there are synchronization rules with password synchronization enabled and applied toohello Active Directory object.</span></span>

* <span data-ttu-id="0451a-166">嘗試 tooretrieve 並顯示 hello 的結果 hello 最後嘗試 toosynchronize hello 密碼 hello 物件。</span><span class="sxs-lookup"><span data-stu-id="0451a-166">Attempts tooretrieve and display hello results of hello last attempt toosynchronize hello password for hello object.</span></span>

<span data-ttu-id="0451a-167">疑難排解密碼同步化單一物件時，hello 下列圖表說明 hello cmdlet 的 hello 結果：</span><span class="sxs-lookup"><span data-stu-id="0451a-167">hello following diagram illustrates hello results of hello cmdlet when troubleshooting password synchronization for a single object:</span></span>

![密碼同步化的診斷輸出 - 單一物件](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

<span data-ttu-id="0451a-169">hello 本節其餘部分將說明特定 hello cmdlet 所傳回的結果和對應的問題。</span><span class="sxs-lookup"><span data-stu-id="0451a-169">hello rest of this section describes specific results returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a><span data-ttu-id="0451a-170">hello Active Directory 物件不是匯出的 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="0451a-170">hello Active Directory object isn't exported tooAzure AD</span></span>
<span data-ttu-id="0451a-171">這在內部部署 Active Directory 帳戶的密碼同步處理失敗，因為在 hello Azure AD 租用戶中沒有對應的物件。</span><span class="sxs-lookup"><span data-stu-id="0451a-171">Password synchronization for this on-premises Active Directory account fails because there is no corresponding object in hello Azure AD tenant.</span></span> <span data-ttu-id="0451a-172">會傳回下列錯誤 hello:</span><span class="sxs-lookup"><span data-stu-id="0451a-172">hello following error is returned:</span></span>

![遺漏 Azure AD 物件](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a><span data-ttu-id="0451a-174">使用者有暫時密碼</span><span class="sxs-lookup"><span data-stu-id="0451a-174">User has a temporary password</span></span>
<span data-ttu-id="0451a-175">目前，Azure AD Connect 不支援與 Azure AD 同步暫時密碼。</span><span class="sxs-lookup"><span data-stu-id="0451a-175">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span></span> <span data-ttu-id="0451a-176">密碼會被視為 toobe 暫存如果 hello**在下次登入時變更密碼**hello 在內部部署 Active Directory 使用者上設定選項。</span><span class="sxs-lookup"><span data-stu-id="0451a-176">A password is considered toobe temporary if hello **Change password at next logon** option is set on hello on-premises Active Directory user.</span></span> <span data-ttu-id="0451a-177">會傳回下列錯誤 hello:</span><span class="sxs-lookup"><span data-stu-id="0451a-177">hello following error is returned:</span></span>

![未匯出暫時密碼](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a><span data-ttu-id="0451a-179">上次嘗試 toosynchronize 密碼的結果，就無法使用</span><span class="sxs-lookup"><span data-stu-id="0451a-179">Results of last attempt toosynchronize password aren't available</span></span>
<span data-ttu-id="0451a-180">根據預設，Azure AD Connect 儲存 hello 的有效期是七天的密碼同步處理嘗試的結果。</span><span class="sxs-lookup"><span data-stu-id="0451a-180">By default, Azure AD Connect stores hello results of password synchronization attempts for seven days.</span></span> <span data-ttu-id="0451a-181">如果沒有可用的 hello 選取 Active Directory 物件的結果，則會傳回下列警告 hello:</span><span class="sxs-lookup"><span data-stu-id="0451a-181">If there are no results available for hello selected Active Directory object, hello following warning is returned:</span></span>

![單一物件的診斷輸出 - 沒有密碼同步記錄](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a><span data-ttu-id="0451a-183">未同步任何密碼：手動疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="0451a-183">No passwords are synchronized: manual troubleshooting steps</span></span>
<span data-ttu-id="0451a-184">請遵循這些步驟 toodetermine，不會將密碼同步處理的原因：</span><span class="sxs-lookup"><span data-stu-id="0451a-184">Follow these steps toodetermine why no passwords are synchronized:</span></span>

1. <span data-ttu-id="0451a-185">中的 hello 連接伺服器[預備模式](active-directory-aadconnectsync-operations.md#staging-mode)嗎？</span><span class="sxs-lookup"><span data-stu-id="0451a-185">Is hello Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="0451a-186">處於預備模式的伺服器不會同步處理任何密碼。</span><span class="sxs-lookup"><span data-stu-id="0451a-186">A server in staging mode does not synchronize any passwords.</span></span>

2. <span data-ttu-id="0451a-187">執行 hello hello 指令碼[取得的密碼同步處理設定 hello 狀態](#get-the-status-of-password-sync-settings)> 一節。</span><span class="sxs-lookup"><span data-stu-id="0451a-187">Run hello script in hello [Get hello status of password sync settings](#get-the-status-of-password-sync-settings) section.</span></span> <span data-ttu-id="0451a-188">它可讓您 hello 密碼同步處理組態的概觀。</span><span class="sxs-lookup"><span data-stu-id="0451a-188">It gives you an overview of hello password sync configuration.</span></span>  

    ![來自密碼同步設定的 PowerShell 指令碼輸出](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. <span data-ttu-id="0451a-190">如果 hello 功能未啟用 Azure AD 中，或未啟用 hello 同步通道狀態，執行 hello 連線安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="0451a-190">If hello feature is not enabled in Azure AD or if hello sync channel status is not enabled, run hello Connect installation wizard.</span></span> <span data-ttu-id="0451a-191">選取 [自訂同步處理選項] 並取消選取密碼同步。這項變更暫時停用 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="0451a-191">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables hello feature.</span></span> <span data-ttu-id="0451a-192">然後再次執行 hello 精靈並重新啟用密碼同步。執行 hello 指令碼一次 hello 組態的 tooverify 是否正確。</span><span class="sxs-lookup"><span data-stu-id="0451a-192">Then run hello wizard again and re-enable password sync. Run hello script again tooverify that hello configuration is correct.</span></span>

4. <span data-ttu-id="0451a-193">查看有錯誤的 hello 事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0451a-193">Look in hello event log for errors.</span></span> <span data-ttu-id="0451a-194">尋找下列事件，則表示問題 hello:</span><span class="sxs-lookup"><span data-stu-id="0451a-194">Look for hello following events, which would indicate a problem:</span></span>
    * <span data-ttu-id="0451a-195">來源：「目錄同步作業」識別碼：0、611、652、655。如果您看到這些事件，即表示有連線問題。</span><span class="sxs-lookup"><span data-stu-id="0451a-195">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span></span> <span data-ttu-id="0451a-196">hello 事件記錄檔訊息包含您有問題的所在的樹系資訊。</span><span class="sxs-lookup"><span data-stu-id="0451a-196">hello event log message contains forest information where you have a problem.</span></span> <span data-ttu-id="0451a-197">如需詳細資訊，請參閱[連線問題](#connectivity problem)。</span><span class="sxs-lookup"><span data-stu-id="0451a-197">For more information, see [Connectivity problem](#connectivity problem).</span></span>

5. <span data-ttu-id="0451a-198">如果您沒有看到任何活動訊號，或任何其他操作都沒有作用，請執行[觸發所有密碼的完整同步](#trigger-a-full-sync-of-all-passwords)。</span><span class="sxs-lookup"><span data-stu-id="0451a-198">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="0451a-199">Hello 指令碼只執行一次。</span><span class="sxs-lookup"><span data-stu-id="0451a-199">Run hello script only once.</span></span>

6. <span data-ttu-id="0451a-200">請參閱 hello[疑難排解不同步處理密碼的一個物件](#one-object-is-not-synchronizing-passwords)> 一節。</span><span class="sxs-lookup"><span data-stu-id="0451a-200">See hello [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span></span>

### <a name="connectivity-problems"></a><span data-ttu-id="0451a-201">連線問題</span><span class="sxs-lookup"><span data-stu-id="0451a-201">Connectivity problems</span></span>

<span data-ttu-id="0451a-202">您是否能夠與 Azure AD 連線？</span><span class="sxs-lookup"><span data-stu-id="0451a-202">Do you have connectivity with Azure AD?</span></span>

<span data-ttu-id="0451a-203">沒有 hello 帳戶具有必要的權限 tooread hello 密碼雜湊中的所有網域？</span><span class="sxs-lookup"><span data-stu-id="0451a-203">Does hello account have required permissions tooread hello password hashes in all domains?</span></span> <span data-ttu-id="0451a-204">如果您安裝連接使用 Express 設定時，應該已經正確 hello 權限。</span><span class="sxs-lookup"><span data-stu-id="0451a-204">If you installed Connect by using Express settings, hello permissions should already be correct.</span></span> 

<span data-ttu-id="0451a-205">如果您使用自訂安裝，hello 手動設定權限執行 hello 下列動作：</span><span class="sxs-lookup"><span data-stu-id="0451a-205">If you used custom installation, set hello permissions manually by doing hello following:</span></span>
    
1. <span data-ttu-id="0451a-206">hello Active Directory 連接器，開始使用 toofind hello 帳戶**同步處理服務管理員**。</span><span class="sxs-lookup"><span data-stu-id="0451a-206">toofind hello account used by hello Active Directory connector, start **Synchronization Service Manager**.</span></span> 
 
2. <span data-ttu-id="0451a-207">跳過**連接器**，然後搜尋您正在疑難排解的 hello 在內部部署 Active Directory 樹系。</span><span class="sxs-lookup"><span data-stu-id="0451a-207">Go too**Connectors**, and then search for hello on-premises Active Directory forest you are troubleshooting.</span></span> 
 
3. <span data-ttu-id="0451a-208">選取 hello 連接器，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="0451a-208">Select hello connector, and then click **Properties**.</span></span> 
 
4. <span data-ttu-id="0451a-209">跳過**連接 tooActive Directory 樹系**。</span><span class="sxs-lookup"><span data-stu-id="0451a-209">Go too**Connect tooActive Directory Forest**.</span></span>  
    
    ![Active Directory 連接器所使用的帳戶](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    <span data-ttu-id="0451a-211">請注意 hello 使用者名稱和 hello hello 帳戶所在的網域。</span><span class="sxs-lookup"><span data-stu-id="0451a-211">Note hello username and hello domain where hello account is located.</span></span>
    
5. <span data-ttu-id="0451a-212">啟動**Active Directory 使用者和電腦**，然後確認您稍早發現的 hello 帳戶具有設定所有的網域樹系中的 hello 根目錄的 hello 後續權限：</span><span class="sxs-lookup"><span data-stu-id="0451a-212">Start **Active Directory Users and Computers**, and then verify that hello account you found earlier has hello follow permissions set at hello root of all domains in your forest:</span></span>
    * <span data-ttu-id="0451a-213">複寫目錄變更</span><span class="sxs-lookup"><span data-stu-id="0451a-213">Replicate Directory Changes</span></span>
    * <span data-ttu-id="0451a-214">複寫目錄變更 (全部)</span><span class="sxs-lookup"><span data-stu-id="0451a-214">Replicate Directory Changes All</span></span>

6. <span data-ttu-id="0451a-215">為 hello 網域控制站連線到 Azure AD connect 嗎？</span><span class="sxs-lookup"><span data-stu-id="0451a-215">Are hello domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="0451a-216">如果 hello 連接伺服器無法連線 tooall 網域控制站，設定**只使用慣用的網域控制站**。</span><span class="sxs-lookup"><span data-stu-id="0451a-216">If hello Connect server cannot connect tooall domain controllers, configure **Only use preferred domain controller**.</span></span>  
    
    ![Active Directory 連接器所使用的網域控制站](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. <span data-ttu-id="0451a-218">請返回太**同步處理服務管理員**和**設定目錄分割**。</span><span class="sxs-lookup"><span data-stu-id="0451a-218">Go back too**Synchronization Service Manager** and **Configure Directory Partition**.</span></span> 
 
8. <span data-ttu-id="0451a-219">選取您的網域中**選取目錄分割**，選取 hello**只使用慣用的網域控制站**核取方塊，然後**設定**。</span><span class="sxs-lookup"><span data-stu-id="0451a-219">Select your domain in **Select directory partitions**, select hello **Only use preferred domain controllers** check box, and then click **Configure**.</span></span> 

9. <span data-ttu-id="0451a-220">在 [hello] 清單中，輸入 hello 網域控制站連接應該用於密碼同步處理。hello 匯入和匯出也使用相同的清單。</span><span class="sxs-lookup"><span data-stu-id="0451a-220">In hello list, enter hello domain controllers that Connect should use for password sync. hello same list is used for import and export as well.</span></span> <span data-ttu-id="0451a-221">針對您的所有網域執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="0451a-221">Do these steps for all your domains.</span></span>

10. <span data-ttu-id="0451a-222">如果 hello 指令碼會顯示沒有任何活動訊號，請執行 hello 指令碼[觸發完整同步處理所有密碼](#trigger-a-full-sync-of-all-passwords)。</span><span class="sxs-lookup"><span data-stu-id="0451a-222">If hello script shows that there is no heartbeat, run hello script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a><span data-ttu-id="0451a-223">一個物件未同步密碼：手動疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="0451a-223">One object is not synchronizing passwords: manual troubleshooting steps</span></span>
<span data-ttu-id="0451a-224">您可以輕鬆地疑難排解密碼同步處理的問題，藉由檢閱 hello 物件狀態。</span><span class="sxs-lookup"><span data-stu-id="0451a-224">You can easily troubleshoot password synchronization issues by reviewing hello status of an object.</span></span>

1. <span data-ttu-id="0451a-225">在**Active Directory 使用者和電腦**搜尋 hello 使用者，然後確認該 hello**使用者必須變更密碼，在下次登入時**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="0451a-225">In **Active Directory Users and Computers**, search for hello user, and then verify that hello **User must change password at next logon** check box is cleared.</span></span>  

    ![Active Directory 生產力密碼](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    <span data-ttu-id="0451a-227">如果選取 [hello] 核取方塊，詢問 hello 使用者 toosign 中的，並變更 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="0451a-227">If hello check box is selected, ask hello user toosign in and change hello password.</span></span> <span data-ttu-id="0451a-228">暫時密碼不會與 Azure AD 同步。</span><span class="sxs-lookup"><span data-stu-id="0451a-228">Temporary passwords are not synchronized with Azure AD.</span></span>

2. <span data-ttu-id="0451a-229">如果在 Active Directory 中 hello 密碼正確無誤，請遵循 hello hello 同步處理引擎中的使用者。</span><span class="sxs-lookup"><span data-stu-id="0451a-229">If hello password looks correct in Active Directory, follow hello user in hello sync engine.</span></span> <span data-ttu-id="0451a-230">由下列 hello 使用者從內部部署 Active Directory tooAzure AD，您可以看到 hello 物件上是否具描述性的錯誤。</span><span class="sxs-lookup"><span data-stu-id="0451a-230">By following hello user from on-premises Active Directory tooAzure AD, you can see whether there is a descriptive error on hello object.</span></span>

    <span data-ttu-id="0451a-231">a.</span><span class="sxs-lookup"><span data-stu-id="0451a-231">a.</span></span> <span data-ttu-id="0451a-232">啟動 hello[同步處理服務管理員](active-directory-aadconnectsync-service-manager-ui.md)。</span><span class="sxs-lookup"><span data-stu-id="0451a-232">Start hello [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

    <span data-ttu-id="0451a-233">b.</span><span class="sxs-lookup"><span data-stu-id="0451a-233">b.</span></span> <span data-ttu-id="0451a-234">按一下 [連接器] 。</span><span class="sxs-lookup"><span data-stu-id="0451a-234">Click **Connectors**.</span></span>

    <span data-ttu-id="0451a-235">c.</span><span class="sxs-lookup"><span data-stu-id="0451a-235">c.</span></span> <span data-ttu-id="0451a-236">選取 hello **Active Directory 連接器**hello 使用者所在的位置。</span><span class="sxs-lookup"><span data-stu-id="0451a-236">Select hello **Active Directory Connector** where hello user is located.</span></span>

    <span data-ttu-id="0451a-237">d.</span><span class="sxs-lookup"><span data-stu-id="0451a-237">d.</span></span> <span data-ttu-id="0451a-238">選取 [搜尋連接器空間] 。</span><span class="sxs-lookup"><span data-stu-id="0451a-238">Select **Search Connector Space**.</span></span>

    <span data-ttu-id="0451a-239">e.</span><span class="sxs-lookup"><span data-stu-id="0451a-239">e.</span></span> <span data-ttu-id="0451a-240">在 hello**範圍**方塊中，選取**DN 或錨點**，然後輸入 hello 完整 DN hello 使用者您正在疑難排解。</span><span class="sxs-lookup"><span data-stu-id="0451a-240">In hello **Scope** box, select **DN or Anchor**, and then enter hello full DN of hello user you are troubleshooting.</span></span>

    ![在連接器空間中依 DN 搜尋使用者](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    <span data-ttu-id="0451a-242">f.</span><span class="sxs-lookup"><span data-stu-id="0451a-242">f.</span></span> <span data-ttu-id="0451a-243">找出您要尋找，然後按一下 hello 使用者**屬性**toosee 所有 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="0451a-243">Locate hello user you are looking for, and then click **Properties** toosee all hello attributes.</span></span> <span data-ttu-id="0451a-244">如果 hello 使用者不是在 hello 搜尋結果，請確認您[篩選規則](active-directory-aadconnectsync-configure-filtering.md)，並確定您執行[套用並驗證變更](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes)的 hello 使用者 tooappear 連線中。</span><span class="sxs-lookup"><span data-stu-id="0451a-244">If hello user is not in hello search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for hello user tooappear in Connect.</span></span>

    <span data-ttu-id="0451a-245">g.</span><span class="sxs-lookup"><span data-stu-id="0451a-245">g.</span></span> <span data-ttu-id="0451a-246">過去一週中，按一下 toosee hello 密碼同步處理物件的詳細資料 hello hello**記錄**。</span><span class="sxs-lookup"><span data-stu-id="0451a-246">toosee hello password sync details of hello object for hello past week, click **Log**.</span></span>  

    ![物件記錄詳細資料](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    <span data-ttu-id="0451a-248">如果 hello 物件記錄是空的 Azure AD Connect 已從 Active Directory 無法 tooread hello 密碼雜湊。</span><span class="sxs-lookup"><span data-stu-id="0451a-248">If hello object log is empty, Azure AD Connect has been unable tooread hello password hash from Active Directory.</span></span> <span data-ttu-id="0451a-249">請繼續進行[連線錯誤](#connectivity-errors)疑難排解。</span><span class="sxs-lookup"><span data-stu-id="0451a-249">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="0451a-250">如果您看到任何其他值比**成功**，toohello 資料表中的，請參閱[密碼同步處理記錄](#password-sync-log)。</span><span class="sxs-lookup"><span data-stu-id="0451a-250">If you see any other value than **success**, refer toohello table in [Password sync log](#password-sync-log).</span></span>

    <span data-ttu-id="0451a-251">h.</span><span class="sxs-lookup"><span data-stu-id="0451a-251">h.</span></span> <span data-ttu-id="0451a-252">選取 hello**歷程**索引標籤，然後確認該至少一個同步處理規則中 hello **PasswordSync**資料行是**True**。</span><span class="sxs-lookup"><span data-stu-id="0451a-252">Select hello **lineage** tab, and make sure that at least one sync rule in hello **PasswordSync** column is **True**.</span></span> <span data-ttu-id="0451a-253">Hello 預設組態中，在 hello hello 同步處理規則名稱是**中 from AD-User AccountEnabled**。</span><span class="sxs-lookup"><span data-stu-id="0451a-253">In hello default configuration, hello name of hello sync rule is **In from AD - User AccountEnabled**.</span></span>  

    ![使用者的相關歷程資訊](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    <span data-ttu-id="0451a-255">i.</span><span class="sxs-lookup"><span data-stu-id="0451a-255">i.</span></span> <span data-ttu-id="0451a-256">按一下**Metaverse 物件屬性**toodisplay 的使用者屬性清單。</span><span class="sxs-lookup"><span data-stu-id="0451a-256">Click **Metaverse Object Properties** toodisplay a list of user attributes.</span></span>  

    ![Metaverse 資訊](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    <span data-ttu-id="0451a-258">確認沒有任何 **cloudFiltered** 屬性存在。</span><span class="sxs-lookup"><span data-stu-id="0451a-258">Verify that there is no **cloudFiltered** attribute present.</span></span> <span data-ttu-id="0451a-259">請確定 hello 網域屬性 （domainFQDN 和 domainNetBios） 具有 hello 預期的值。</span><span class="sxs-lookup"><span data-stu-id="0451a-259">Make sure that hello domain attributes (domainFQDN and domainNetBios) have hello expected values.</span></span>

    <span data-ttu-id="0451a-260">j.</span><span class="sxs-lookup"><span data-stu-id="0451a-260">j.</span></span> <span data-ttu-id="0451a-261">按一下 hello**連接器** 索引標籤。請確定您看到連接器 tooboth 內部部署 Active Directory 與 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="0451a-261">Click hello **Connectors** tab. Make sure that you see connectors tooboth on-premises Active Directory and Azure AD.</span></span>

    ![Metaverse 資訊](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    <span data-ttu-id="0451a-263">k.</span><span class="sxs-lookup"><span data-stu-id="0451a-263">k.</span></span> <span data-ttu-id="0451a-264">選取 hello 資料列代表 Azure AD 中，按一下**屬性**，然後按一下hello**歷程** 索引標籤 hello 連接器空間物件中應該會有輸出規則 hello **PasswordSync**資料行集太**True**。</span><span class="sxs-lookup"><span data-stu-id="0451a-264">Select hello row that represents Azure AD, click **Properties**, and then click hello **Lineage** tab. hello connector space object should have an outbound rule in hello **PasswordSync** column set too**True**.</span></span> <span data-ttu-id="0451a-265">Hello 預設組態中，在 hello hello 同步處理規則名稱是**出 tooAAD-User Join**。</span><span class="sxs-lookup"><span data-stu-id="0451a-265">In hello default configuration, hello name of hello sync rule is **Out tooAAD - User Join**.</span></span>  

    ![連接器空間物件屬性對話方塊](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a><span data-ttu-id="0451a-267">密碼同步記錄</span><span class="sxs-lookup"><span data-stu-id="0451a-267">Password sync log</span></span>
<span data-ttu-id="0451a-268">hello 狀態資料行可以有下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="0451a-268">hello status column can have hello following values:</span></span>

| <span data-ttu-id="0451a-269">狀態</span><span class="sxs-lookup"><span data-stu-id="0451a-269">Status</span></span> | <span data-ttu-id="0451a-270">說明</span><span class="sxs-lookup"><span data-stu-id="0451a-270">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0451a-271">成功</span><span class="sxs-lookup"><span data-stu-id="0451a-271">Success</span></span> |<span data-ttu-id="0451a-272">已成功同步處理密碼。</span><span class="sxs-lookup"><span data-stu-id="0451a-272">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="0451a-273">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="0451a-273">FilteredByTarget</span></span> |<span data-ttu-id="0451a-274">密碼設定得**使用者必須變更密碼，在下次登入時**。</span><span class="sxs-lookup"><span data-stu-id="0451a-274">Password is set too**User must change password at next logon**.</span></span> <span data-ttu-id="0451a-275">未同步處理密碼。</span><span class="sxs-lookup"><span data-stu-id="0451a-275">Password has not been synchronized.</span></span> |
| <span data-ttu-id="0451a-276">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="0451a-276">NoTargetConnection</span></span> |<span data-ttu-id="0451a-277">Hello metaverse 或 hello Azure AD 連接器空間中任何物件。</span><span class="sxs-lookup"><span data-stu-id="0451a-277">No object in hello metaverse or in hello Azure AD connector space.</span></span> |
| <span data-ttu-id="0451a-278">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="0451a-278">SourceConnectorNotPresent</span></span> |<span data-ttu-id="0451a-279">Hello 在內部部署 Active Directory 連接器空間中找不到物件。</span><span class="sxs-lookup"><span data-stu-id="0451a-279">No object found in hello on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="0451a-280">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="0451a-280">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="0451a-281">hello Azure AD 連接器空間中的 hello 物件尚未匯出。</span><span class="sxs-lookup"><span data-stu-id="0451a-281">hello object in hello Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="0451a-282">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="0451a-282">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="0451a-283">記錄項目建立於組建 1.0.9125.0 之前，並且以其舊版的狀態顯示。</span><span class="sxs-lookup"><span data-stu-id="0451a-283">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |
| <span data-ttu-id="0451a-284">錯誤</span><span class="sxs-lookup"><span data-stu-id="0451a-284">Error</span></span> |<span data-ttu-id="0451a-285">服務傳回未知的錯誤。</span><span class="sxs-lookup"><span data-stu-id="0451a-285">Service returned an unknown error.</span></span> |
| <span data-ttu-id="0451a-286">不明</span><span class="sxs-lookup"><span data-stu-id="0451a-286">Unknown</span></span> |<span data-ttu-id="0451a-287">嘗試 tooprocess 密碼雜湊的批次時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="0451a-287">An error occurred while trying tooprocess a batch of password hashes.</span></span>  |
| <span data-ttu-id="0451a-288">MissingAttribute</span><span class="sxs-lookup"><span data-stu-id="0451a-288">MissingAttribute</span></span> |<span data-ttu-id="0451a-289">無法使用 Azure AD Domain Services 所需的特定屬性 (例如，Kerberos 雜湊)。</span><span class="sxs-lookup"><span data-stu-id="0451a-289">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span></span> |
| <span data-ttu-id="0451a-290">RetryRequestedByTarget</span><span class="sxs-lookup"><span data-stu-id="0451a-290">RetryRequestedByTarget</span></span> |<span data-ttu-id="0451a-291">先前無法使用 Azure AD Domain Services 所需的特定屬性 (例如，Kerberos 雜湊)。</span><span class="sxs-lookup"><span data-stu-id="0451a-291">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span></span> <span data-ttu-id="0451a-292">會嘗試 tooresynchronize hello 使用者密碼雜湊。</span><span class="sxs-lookup"><span data-stu-id="0451a-292">An attempt tooresynchronize hello user's password hash is made.</span></span> |

## <a name="scripts-toohelp-troubleshooting"></a><span data-ttu-id="0451a-293">指令碼 toohelp 疑難排解</span><span class="sxs-lookup"><span data-stu-id="0451a-293">Scripts toohelp troubleshooting</span></span>

### <a name="get-hello-status-of-password-sync-settings"></a><span data-ttu-id="0451a-294">取得密碼同步處理設定 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="0451a-294">Get hello status of password sync settings</span></span>
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
        Write-Warning "More than one Azure AD Connectors found. Please update hello script toouse hello appropriate Connector."
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

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="0451a-295">觸發所有密碼的完整同步處理</span><span class="sxs-lookup"><span data-stu-id="0451a-295">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="0451a-296">只執行一次這個指令碼。</span><span class="sxs-lookup"><span data-stu-id="0451a-296">Run this script only once.</span></span> <span data-ttu-id="0451a-297">如果您需要 toorun，它一次以上，其他項目是 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="0451a-297">If you need toorun it more than once, something else is hello problem.</span></span> <span data-ttu-id="0451a-298">tootroubleshoot hello 問題，請連絡 Microsoft 支援。</span><span class="sxs-lookup"><span data-stu-id="0451a-298">tootroubleshoot hello problem, contact Microsoft support.</span></span>

<span data-ttu-id="0451a-299">您可以使用下列指令碼的 hello 觸發完整同步處理所有密碼：</span><span class="sxs-lookup"><span data-stu-id="0451a-299">You can trigger a full sync of all passwords by using hello following script:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0451a-300">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0451a-300">Next steps</span></span>
* [<span data-ttu-id="0451a-301">使用 Azure AD Connect 同步處理實作密碼同步處理</span><span class="sxs-lookup"><span data-stu-id="0451a-301">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md)
* [<span data-ttu-id="0451a-302">Azure AD Connect 同步：自訂同步處理選項</span><span class="sxs-lookup"><span data-stu-id="0451a-302">Azure AD Connect Sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="0451a-303">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0451a-303">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
