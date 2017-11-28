---
title: "Azure AD Connect 同步： 變更 hello Azure AD 連接同步處理服務帳戶 |Microsoft 文件"
description: "此主題說明 hello 加密金鑰和方式 tooabandon hello 密碼之後變更。"
services: active-directory
keywords: "Azure AD 同步處理服務帳戶, 密碼"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 11948ac4662f722e4f684ef6c9b9ccdc6387e60f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-azure-ad-connect-sync-service-account-password"></a><span data-ttu-id="c25d8-104">變更 hello Azure AD Connect 同步處理服務帳戶密碼</span><span class="sxs-lookup"><span data-stu-id="c25d8-104">Changing hello Azure AD Connect sync service account password</span></span>
<span data-ttu-id="c25d8-105">如果您變更 hello Azure AD Connect 同步處理服務帳戶密碼，hello 同步處理服務之前將無法可以開始正常您已在放棄 hello 加密金鑰並重新初始化 hello Azure AD Connect 同步處理服務帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="c25d8-105">If you change hello  Azure AD Connect sync service account password, hello Synchronization Service will not be able start correctly until you have abandoned hello encryption key and reinitialized hello Azure AD Connect sync service account password.</span></span> 

<span data-ttu-id="c25d8-106">Azure AD Connect，hello 同步處理服務的一部分使用加密金鑰 toostore hello 密碼的 hello AD DS 和 Azure AD 服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="c25d8-106">Azure AD Connect, as part of hello Synchronization Services uses an encryption key toostore hello passwords of hello AD DS and Azure AD service accounts.</span></span>  <span data-ttu-id="c25d8-107">這些帳戶會加密，再將它們儲存在 hello 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="c25d8-107">These accounts are encrypted before they are stored in hello database.</span></span> 

<span data-ttu-id="c25d8-108">hello 加密金鑰用於保護使用[Windows 資料保護 (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c25d8-108">hello encryption key used is secured using [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span></span> <span data-ttu-id="c25d8-109">DPAPI 保護 hello 加密金鑰使用 hello **hello Azure AD Connect 同步處理服務帳戶的密碼**。</span><span class="sxs-lookup"><span data-stu-id="c25d8-109">DPAPI protects hello encryption key using hello **password of hello Azure AD Connect sync service account**.</span></span> 

<span data-ttu-id="c25d8-110">如果您需要 toochange hello 服務帳戶密碼，您就可以使用中的 hello 程序[Abandoning hello Azure AD 連接同步處理加密金鑰](#abandoning-the-azure-ad-connect-sync-encryption-key)tooaccomplish 這。</span><span class="sxs-lookup"><span data-stu-id="c25d8-110">If you need toochange hello service account password you can use hello procedures in [Abandoning hello Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish this.</span></span>  <span data-ttu-id="c25d8-111">如果您因為任何原因需要 tooabandon hello 加密金鑰，也應該使用這些程序。</span><span class="sxs-lookup"><span data-stu-id="c25d8-111">These procedures should also be used if you need tooabandon hello encryption key for any reason.</span></span>

##<a name="issues-that-arise-from-changing-hello-password"></a><span data-ttu-id="c25d8-112">所發生的變更 hello 密碼問題</span><span class="sxs-lookup"><span data-stu-id="c25d8-112">Issues that arise from changing hello password</span></span>
<span data-ttu-id="c25d8-113">有兩件事需要 toobe 完成時變更 hello 服務帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="c25d8-113">There are two things that need toobe done when you change hello service account password.</span></span>

<span data-ttu-id="c25d8-114">首先，您必須在 hello Windows 服務控制管理員 toochange hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="c25d8-114">First, you need toochange hello password under hello Windows Service Control Manager.</span></span>  <span data-ttu-id="c25d8-115">在此問題獲得解決之前，您會看到下列錯誤︰</span><span class="sxs-lookup"><span data-stu-id="c25d8-115">Until this issue is resolved you will see following errors:</span></span>


- <span data-ttu-id="c25d8-116">如果您嘗試 toostart hello 同步處理服務 Windows 服務控制管理員 」 中，您會收到 hello 錯誤 「**Windows 無法啟動本機電腦上的 hello Microsoft Azure AD 同步服務**"。</span><span class="sxs-lookup"><span data-stu-id="c25d8-116">If you try toostart hello Synchronization Service in Windows Service Control Manager, you receive hello error "**Windows could not start hello Microsoft Azure AD Sync service on Local Computer**".</span></span> <span data-ttu-id="c25d8-117">**錯誤 1069年: hello 服務未啟動到期 tooa 登入失敗。**"</span><span class="sxs-lookup"><span data-stu-id="c25d8-117">**Error 1069: hello service did not start due tooa logon failure.**"</span></span>
- <span data-ttu-id="c25d8-118">在 Windows 事件檢視器，hello 系統事件記錄檔包含與錯誤**事件識別碼 7038**和訊息 「**hello ADSync 服務是在無法 toolog 如同 hello 目前已設定密碼到期，toohello 下列錯誤：hello 使用者名稱或密碼不正確。**"</span><span class="sxs-lookup"><span data-stu-id="c25d8-118">Under Windows Event Viewer, hello system event log contains an error with **Event ID 7038** and message “**hello ADSync service was unable toolog on as with hello currently configured password due toohello following error: hello user name or password is incorrect.**"</span></span>

<span data-ttu-id="c25d8-119">第二，在特定情況下更新 hello 密碼時，如果 hello 同步處理服務無法再擷取 hello 透過 DPAPI 的加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="c25d8-119">Second, under specific conditions, if hello password is updated, hello Synchronization Service can no longer retrieve hello encryption key via DPAPI.</span></span> <span data-ttu-id="c25d8-120">沒有 hello 加密金鑰，同步處理服務無法解密，或從 hello 密碼需要的 toosynchronize hello 內部部署 AD 和 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="c25d8-120">Without hello encryption key, hello Synchronization Service cannot decrypt hello passwords required toosynchronize to/from on-premises AD and Azure AD.</span></span>
<span data-ttu-id="c25d8-121">您會看到如下錯誤︰</span><span class="sxs-lookup"><span data-stu-id="c25d8-121">You will see errors such as:</span></span>

- <span data-ttu-id="c25d8-122">在 「 Windows 服務控制管理員 」 中，如果您試過 toostart hello 同步處理服務，它無法擷取 hello 加密金鑰，其錯誤而失敗 」 * * Windows 無法啟動本機電腦上的 Microsoft Azure AD Sync hello。</span><span class="sxs-lookup"><span data-stu-id="c25d8-122">Under Windows Service Control Manager, if you try toostart hello Synchronization Service and it cannot retrieve hello encryption key, it fails with error “**Windows could not start hello Microsoft Azure AD Sync on Local Computer.</span></span> <span data-ttu-id="c25d8-123">如需詳細資訊，檢閱 hello 系統事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c25d8-123">For more information, review hello System Event log.</span></span> <span data-ttu-id="c25d8-124">如果這是非 Microsoft 服務，請連絡 hello 服務廠商，並 tooservice 特有的錯誤程式碼，請參閱 * *-21451857952 * * *。 」</span><span class="sxs-lookup"><span data-stu-id="c25d8-124">If this is a non-Microsoft service, contact hello service vendor, and refer tooservice-specific error code **-21451857952****.”</span></span>
- <span data-ttu-id="c25d8-125">在 Windows 事件檢視器，hello 應用程式事件記錄檔包含與錯誤**事件識別碼 6028**和錯誤訊息*"**hello 伺服器加密金鑰無法存取。**"*</span><span class="sxs-lookup"><span data-stu-id="c25d8-125">Under Windows Event Viewer, hello application event log contains an error with **Event ID 6028** and error message *“**hello server encryption key cannot be accessed.**”*</span></span>

<span data-ttu-id="c25d8-126">tooensure，您不會收到這些錯誤，請依照下列中的 hello 程序[Abandoning hello Azure AD 連接同步處理加密金鑰](#abandoning-the-azure-ad-connect-sync-encryption-key)變更 hello 密碼時。</span><span class="sxs-lookup"><span data-stu-id="c25d8-126">tooensure that you do not receive these errors, follow hello procedures in [Abandoning hello Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) when changing hello password.</span></span>
 
## <a name="abandoning-hello-azure-ad-connect-sync-encryption-key"></a><span data-ttu-id="c25d8-127">放棄 hello Azure AD 連接同步處理加密金鑰</span><span class="sxs-lookup"><span data-stu-id="c25d8-127">Abandoning hello Azure AD Connect Sync encryption key</span></span>
>[!IMPORTANT]
><span data-ttu-id="c25d8-128">hello 下列程序僅適用於 tooAzure AD Connect 組建 1.1.443.0 或更舊版本。</span><span class="sxs-lookup"><span data-stu-id="c25d8-128">hello following procedures only apply tooAzure AD Connect build 1.1.443.0 or older.</span></span>

<span data-ttu-id="c25d8-129">使用下列程序 tooabandon hello 加密金鑰的 hello。</span><span class="sxs-lookup"><span data-stu-id="c25d8-129">Use hello following procedures tooabandon hello encryption key.</span></span>

### <a name="what-toodo-if-you-need-tooabandon-hello-encryption-key"></a><span data-ttu-id="c25d8-130">如果您需要 tooabandon hello 加密金鑰哪些 toodo</span><span class="sxs-lookup"><span data-stu-id="c25d8-130">What toodo if you need tooabandon hello encryption key</span></span>

<span data-ttu-id="c25d8-131">如果您需要 tooabandon hello 加密金鑰，請使用下列程序 tooaccomplish hello 這項。</span><span class="sxs-lookup"><span data-stu-id="c25d8-131">If you need tooabandon hello encryption key, use hello following procedures tooaccomplish this.</span></span>

1. [<span data-ttu-id="c25d8-132">放棄 hello 現有的加密金鑰</span><span class="sxs-lookup"><span data-stu-id="c25d8-132">Abandon hello existing encryption key</span></span>](#abandon-the-existing-encryption-key)

2. [<span data-ttu-id="c25d8-133">提供 hello 的 hello AD DS 帳戶的密碼</span><span class="sxs-lookup"><span data-stu-id="c25d8-133">Provide hello password of hello AD DS account</span></span>](#provide-the-password-of-the-ad-ds-account)

3. [<span data-ttu-id="c25d8-134">重新初始化 hello hello Azure AD 同步處理帳戶密碼</span><span class="sxs-lookup"><span data-stu-id="c25d8-134">Reinitialize hello password of hello Azure AD sync account</span></span>](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [<span data-ttu-id="c25d8-135">啟動 hello 同步處理服務</span><span class="sxs-lookup"><span data-stu-id="c25d8-135">Start hello Synchronization Service</span></span>](#start-the-synchronization-service)

#### <a name="abandon-hello-existing-encryption-key"></a><span data-ttu-id="c25d8-136">放棄 hello 現有的加密金鑰</span><span class="sxs-lookup"><span data-stu-id="c25d8-136">Abandon hello existing encryption key</span></span>
<span data-ttu-id="c25d8-137">因此，可以建立該新的加密金鑰，請放棄 hello 現有的加密金鑰：</span><span class="sxs-lookup"><span data-stu-id="c25d8-137">Abandon hello existing encryption key so that new encryption key can be created:</span></span>

1. <span data-ttu-id="c25d8-138">登入 tooyour Azure AD 連線伺服器系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="c25d8-138">Log in tooyour Azure AD Connect Server as administrator.</span></span>

2. <span data-ttu-id="c25d8-139">啟動新的 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="c25d8-139">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="c25d8-140">瀏覽 toofolder:`$env:Program Files\Microsoft Azure AD Sync\bin\`</span><span class="sxs-lookup"><span data-stu-id="c25d8-140">Navigate toofolder: `$env:Program Files\Microsoft Azure AD Sync\bin\`</span></span>

4. <span data-ttu-id="c25d8-141">執行 hello 命令：`./miiskmu.exe /a`</span><span class="sxs-lookup"><span data-stu-id="c25d8-141">Run hello command: `./miiskmu.exe /a`</span></span>

![Azure AD Connect 同步處理加密金鑰公用程式](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-hello-password-of-hello-ad-ds-account"></a><span data-ttu-id="c25d8-143">提供 hello 的 hello AD DS 帳戶的密碼</span><span class="sxs-lookup"><span data-stu-id="c25d8-143">Provide hello password of hello AD DS account</span></span>
<span data-ttu-id="c25d8-144">無法再解密 hello hello 資料庫內儲存的現有密碼，您必須 tooprovide hello 與 hello 的 hello AD DS 帳戶的密碼同步處理服務。</span><span class="sxs-lookup"><span data-stu-id="c25d8-144">As hello existing passwords stored inside hello database can no longer be decrypted, you need tooprovide hello Synchronization Service with hello password of hello AD DS account.</span></span> <span data-ttu-id="c25d8-145">hello 同步處理服務會加密 hello 使用 hello 新的加密金鑰的密碼：</span><span class="sxs-lookup"><span data-stu-id="c25d8-145">hello Synchronization Service encrypts hello passwords using hello new encryption key:</span></span>

1. <span data-ttu-id="c25d8-146">啟動 hello Synchronization Service Manager （開始 → 同步處理服務）。</span><span class="sxs-lookup"><span data-stu-id="c25d8-146">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="c25d8-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="c25d8-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  
2. <span data-ttu-id="c25d8-148">移 toohello**連接器** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c25d8-148">Go toohello **Connectors** tab.</span></span>
3. <span data-ttu-id="c25d8-149">選取 hello **AD 連接器**對應 tooyour 在內部部署 AD。</span><span class="sxs-lookup"><span data-stu-id="c25d8-149">Select hello **AD Connector** that corresponds tooyour on-premises AD.</span></span> <span data-ttu-id="c25d8-150">如果您有多個 AD 連接器時，重複下列步驟，為每個 hello。</span><span class="sxs-lookup"><span data-stu-id="c25d8-150">If you have more than one AD connector, repeat hello following steps for each of them.</span></span>
4. <span data-ttu-id="c25d8-151">選取 [動作] 下方的 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="c25d8-151">Under **Actions**, select **Properties**.</span></span>
5. <span data-ttu-id="c25d8-152">在 hello 快顯對話方塊中，選取 **連接 tooActive Directory 樹系**:</span><span class="sxs-lookup"><span data-stu-id="c25d8-152">In hello pop-up dialog, select **Connect tooActive Directory Forest**:</span></span>
6. <span data-ttu-id="c25d8-153">輸入 hello hello hello AD DS 帳戶密碼**密碼**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c25d8-153">Enter hello password of hello AD DS account in hello **Password** textbox.</span></span> <span data-ttu-id="c25d8-154">如果您不知道其密碼，您必須設定 tooa 已知值，然後再執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="c25d8-154">If you do not know its password, you must set it tooa known value before performing this step.</span></span>
7. <span data-ttu-id="c25d8-155">按一下**確定**toosave hello 新密碼] 和 [關閉 hello 快顯對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c25d8-155">Click **OK** toosave hello new password and close hello pop-up dialog.</span></span>
<span data-ttu-id="c25d8-156">![Azure AD Connect 同步處理加密金鑰公用程式](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="c25d8-156">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>

#### <a name="reinitialize-hello-password-of-hello-azure-ad-sync-account"></a><span data-ttu-id="c25d8-157">重新初始化 hello hello Azure AD 同步處理帳戶密碼</span><span class="sxs-lookup"><span data-stu-id="c25d8-157">Reinitialize hello password of hello Azure AD sync account</span></span>
<span data-ttu-id="c25d8-158">您無法直接提供 hello hello Azure AD 服務帳戶 toohello 同步處理服務密碼。</span><span class="sxs-lookup"><span data-stu-id="c25d8-158">You cannot directly provide hello password of hello Azure AD service account toohello Synchronization Service.</span></span> <span data-ttu-id="c25d8-159">相反地，您需要 toouse hello cmdlet**新增 ADSyncAADServiceAccount** tooreinitialize hello Azure AD 服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="c25d8-159">Instead, you need toouse hello cmdlet **Add-ADSyncAADServiceAccount** tooreinitialize hello Azure AD service account.</span></span> <span data-ttu-id="c25d8-160">hello cmdlet 會重設 hello 帳戶密碼，並使其成為可用 toohello 同步服務：</span><span class="sxs-lookup"><span data-stu-id="c25d8-160">hello cmdlet resets hello account password and makes it available toohello Synchronization Service:</span></span>

1. <span data-ttu-id="c25d8-161">Hello Azure AD Connect 的伺服器上啟動新的 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="c25d8-161">Start a new PowerShell session on hello Azure AD Connect server.</span></span>
2. <span data-ttu-id="c25d8-162">執行 `Add-ADSyncAADServiceAccount` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c25d8-162">Run cmdlet `Add-ADSyncAADServiceAccount`.</span></span>
3. <span data-ttu-id="c25d8-163">在 hello 快顯對話方塊中，提供 Azure AD 租用戶 hello Azure AD 全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="c25d8-163">In hello pop-up dialog, provide hello Azure AD Global admin credentials for your Azure AD tenant.</span></span>
<span data-ttu-id="c25d8-164">![Azure AD Connect 同步處理加密金鑰公用程式](media/active-directory-aadconnectsync-encryption-key/key7.png)</span><span class="sxs-lookup"><span data-stu-id="c25d8-164">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key7.png)</span></span>
4. <span data-ttu-id="c25d8-165">如果成功，您會看到 hello PowerShell 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="c25d8-165">If it is successful, you will see hello PowerShell command prompt.</span></span>

#### <a name="start-hello-synchronization-service"></a><span data-ttu-id="c25d8-166">啟動 hello 同步處理服務</span><span class="sxs-lookup"><span data-stu-id="c25d8-166">Start hello Synchronization Service</span></span>
<span data-ttu-id="c25d8-167">既然 hello 同步處理服務都有存取 toohello 加密金鑰，且所有 hello 密碼需要您可以重新啟動 Windows 服務控制管理員 hello hello 服務：</span><span class="sxs-lookup"><span data-stu-id="c25d8-167">Now that hello Synchronization Service has access toohello encryption key and all hello passwords it needs, you can restart hello service in hello Windows Service Control Manager:</span></span>


1. <span data-ttu-id="c25d8-168">移 tooWindows 服務控制管理員 （開始 → 服務）。</span><span class="sxs-lookup"><span data-stu-id="c25d8-168">Go tooWindows Service Control Manager (START → Services).</span></span>
2. <span data-ttu-id="c25d8-169">選取 [Microsoft Azure AD 同步處理]，然後按一下 [重新啟動]。</span><span class="sxs-lookup"><span data-stu-id="c25d8-169">Select **Microsoft Azure AD Sync** and click Restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c25d8-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c25d8-170">Next steps</span></span>
<span data-ttu-id="c25d8-171">**概觀主題**</span><span class="sxs-lookup"><span data-stu-id="c25d8-171">**Overview topics**</span></span>

* [<span data-ttu-id="c25d8-172">Azure AD Connect 同步處理：了解及自訂同步處理</span><span class="sxs-lookup"><span data-stu-id="c25d8-172">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="c25d8-173">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c25d8-173">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
