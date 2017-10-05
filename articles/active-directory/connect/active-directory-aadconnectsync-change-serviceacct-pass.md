---
title: "Azure AD Connect 同步處理︰變更 Azure AD Connect 同步處理服務帳戶 | Microsoft Docs"
description: "本主題文件說明加密金鑰，以及如何在密碼變更後放棄它。"
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
ms.openlocfilehash: bf6234d0810f870909957ee1c1e33c225a4922b9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="changing-the-azure-ad-connect-sync-service-account-password"></a><span data-ttu-id="ff680-104">變更 Azure AD Connect 同步處理服務帳戶密碼</span><span class="sxs-lookup"><span data-stu-id="ff680-104">Changing the Azure AD Connect sync service account password</span></span>
<span data-ttu-id="ff680-105">如果您變更 Azure AD Connect 同步服務帳戶密碼，「同步處理服務」將會無法正確啟動，直到您放棄加密金鑰並將 Azure AD Connect 同步服務帳戶密碼重新初始化為止。</span><span class="sxs-lookup"><span data-stu-id="ff680-105">If you change the  Azure AD Connect sync service account password, the Synchronization Service will not be able start correctly until you have abandoned the encryption key and reinitialized the Azure AD Connect sync service account password.</span></span> 

<span data-ttu-id="ff680-106">Azure AD Connect 是同步處理服務的一部分，會使用加密金鑰來儲存 AD DS 與 Azure AD 服務帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="ff680-106">Azure AD Connect, as part of the Synchronization Services uses an encryption key to store the passwords of the AD DS and Azure AD service accounts.</span></span>  <span data-ttu-id="ff680-107">這些帳戶會先加密再儲存到資料庫中。</span><span class="sxs-lookup"><span data-stu-id="ff680-107">These accounts are encrypted before they are stored in the database.</span></span> 

<span data-ttu-id="ff680-108">所使用的加密金鑰會使用 [Windows 資料保護 (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx) 來提供保護。</span><span class="sxs-lookup"><span data-stu-id="ff680-108">The encryption key used is secured using [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span></span> <span data-ttu-id="ff680-109">DPAPI 為加密金鑰提供保護的方式是使用 **Azure AD Connect 同步處理服務帳戶的密碼**。</span><span class="sxs-lookup"><span data-stu-id="ff680-109">DPAPI protects the encryption key using the **password of the Azure AD Connect sync service account**.</span></span> 

<span data-ttu-id="ff680-110">如果您需要變更服務帳戶的密碼，您可以使用[放棄 Azure AD Connect 同步處理加密金鑰](#abandoning-the-azure-ad-connect-sync-encryption-key)中的程序來完成這項作業。</span><span class="sxs-lookup"><span data-stu-id="ff680-110">If you need to change the service account password you can use the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) to accomplish this.</span></span>  <span data-ttu-id="ff680-111">如果您基於任何原因而需要放棄加密金鑰，您也應該使用這些程序。</span><span class="sxs-lookup"><span data-stu-id="ff680-111">These procedures should also be used if you need to abandon the encryption key for any reason.</span></span>

##<a name="issues-that-arise-from-changing-the-password"></a><span data-ttu-id="ff680-112">變更密碼而引發的問題</span><span class="sxs-lookup"><span data-stu-id="ff680-112">Issues that arise from changing the password</span></span>
<span data-ttu-id="ff680-113">當您在變更服務帳戶的密碼時，有兩件事必須完成。</span><span class="sxs-lookup"><span data-stu-id="ff680-113">There are two things that need to be done when you change the service account password.</span></span>

<span data-ttu-id="ff680-114">第一件事，您必須在 Windows 服務控制管理員底下變更密碼。</span><span class="sxs-lookup"><span data-stu-id="ff680-114">First, you need to change the password under the Windows Service Control Manager.</span></span>  <span data-ttu-id="ff680-115">在此問題獲得解決之前，您會看到下列錯誤︰</span><span class="sxs-lookup"><span data-stu-id="ff680-115">Until this issue is resolved you will see following errors:</span></span>


- <span data-ttu-id="ff680-116">如果您嘗試在 Windows 服務控制管理員中啟動同步處理服務，您會收到錯誤「**Windows 無法在本機電腦上啟動 Microsoft Azure AD 同步處理服務**」。</span><span class="sxs-lookup"><span data-stu-id="ff680-116">If you try to start the Synchronization Service in Windows Service Control Manager, you receive the error "**Windows could not start the Microsoft Azure AD Sync service on Local Computer**".</span></span> <span data-ttu-id="ff680-117">**錯誤 1069︰由於登入失敗，此服務未啟動。**」</span><span class="sxs-lookup"><span data-stu-id="ff680-117">**Error 1069: The service did not start due to a logon failure.**"</span></span>
- <span data-ttu-id="ff680-118">在 Windows 事件檢視器底下，系統事件記錄包含**事件識別碼為 7038** 的錯誤和「**ADSync 服務無法使用目前設定的密碼來登入，因為發生下列錯誤︰使用者名稱或密碼不正確**」的訊息。</span><span class="sxs-lookup"><span data-stu-id="ff680-118">Under Windows Event Viewer, the system event log contains an error with **Event ID 7038** and message “**The ADSync service was unable to log on as with the currently configured password due to the following error: The user name or password is incorrect.**"</span></span>

<span data-ttu-id="ff680-119">第二件事，若密碼在特定狀況下做了更新，同步處理服務將無法再透過 DPAPI 擷取加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="ff680-119">Second, under specific conditions, if the password is updated, the Synchronization Service can no longer retrieve the encryption key via DPAPI.</span></span> <span data-ttu-id="ff680-120">沒有加密金鑰，同步處理服務就無法將密碼解密，以供用來在內部部署 AD 和 Azure AD 進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="ff680-120">Without the encryption key, the Synchronization Service cannot decrypt the passwords required to synchronize to/from on-premises AD and Azure AD.</span></span>
<span data-ttu-id="ff680-121">您會看到如下錯誤︰</span><span class="sxs-lookup"><span data-stu-id="ff680-121">You will see errors such as:</span></span>

- <span data-ttu-id="ff680-122">如果您嘗試在 Windows 服務控制管理員底下啟動同步處理服務，但此服務無法擷取加密金鑰，此啟動作業便會失敗，並出現錯誤「Windows 無法在本機電腦上啟動 Microsoft Azure AD 同步處理。</span><span class="sxs-lookup"><span data-stu-id="ff680-122">Under Windows Service Control Manager, if you try to start the Synchronization Service and it cannot retrieve the encryption key, it fails with error “**Windows could not start the Microsoft Azure AD Sync on Local Computer.</span></span> <span data-ttu-id="ff680-123">如需詳細資訊，請檢閱系統事件記錄。</span><span class="sxs-lookup"><span data-stu-id="ff680-123">For more information, review the System Event log.</span></span> <span data-ttu-id="ff680-124">如果這不是 Microsoft 服務，請連絡服務供應商，並參考服務特有的錯誤碼 **-21451857952****」。</span><span class="sxs-lookup"><span data-stu-id="ff680-124">If this is a non-Microsoft service, contact the service vendor, and refer to service-specific error code **-21451857952****.”</span></span>
- <span data-ttu-id="ff680-125">Windows 事件檢視器底下的應用程式事件記錄包含**事件識別碼為 6028** 的錯誤和錯誤訊息「無法存取伺服器加密金鑰」。</span><span class="sxs-lookup"><span data-stu-id="ff680-125">Under Windows Event Viewer, the application event log contains an error with **Event ID 6028** and error message *“**The server encryption key cannot be accessed.**”*</span></span>

<span data-ttu-id="ff680-126">若要確保不會收到這些錯誤，請在變更密碼時遵循[放棄 Azure AD Connect 同步處理加密金鑰](#abandoning-the-azure-ad-connect-sync-encryption-key)中的程序。</span><span class="sxs-lookup"><span data-stu-id="ff680-126">To ensure that you do not receive these errors, follow the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) when changing the password.</span></span>
 
## <a name="abandoning-the-azure-ad-connect-sync-encryption-key"></a><span data-ttu-id="ff680-127">放棄 Azure AD Connect 同步處理加密金鑰</span><span class="sxs-lookup"><span data-stu-id="ff680-127">Abandoning the Azure AD Connect Sync encryption key</span></span>
>[!IMPORTANT]
><span data-ttu-id="ff680-128">下列程序只適用於 Azure AD Connect 組建 1.1.443.0 或更舊版本。</span><span class="sxs-lookup"><span data-stu-id="ff680-128">The following procedures only apply to Azure AD Connect build 1.1.443.0 or older.</span></span>

<span data-ttu-id="ff680-129">使用下列程序來放棄加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="ff680-129">Use the following procedures to abandon the encryption key.</span></span>

### <a name="what-to-do-if-you-need-to-abandon-the-encryption-key"></a><span data-ttu-id="ff680-130">需要放棄加密金鑰時的作法</span><span class="sxs-lookup"><span data-stu-id="ff680-130">What to do if you need to abandon the encryption key</span></span>

<span data-ttu-id="ff680-131">如果您需要放棄加密金鑰，請使用下列程序來完成這項作業。</span><span class="sxs-lookup"><span data-stu-id="ff680-131">If you need to abandon the encryption key, use the following procedures to accomplish this.</span></span>

1. [<span data-ttu-id="ff680-132">放棄現有的加密金鑰</span><span class="sxs-lookup"><span data-stu-id="ff680-132">Abandon the existing encryption key</span></span>](#abandon-the-existing-encryption-key)

2. [<span data-ttu-id="ff680-133">提供 AD DS 帳戶的密碼</span><span class="sxs-lookup"><span data-stu-id="ff680-133">Provide the password of the AD DS account</span></span>](#provide-the-password-of-the-ad-ds-account)

3. [<span data-ttu-id="ff680-134">重新初始化 Azure AD 同步處理帳戶的密碼</span><span class="sxs-lookup"><span data-stu-id="ff680-134">Reinitialize the password of the Azure AD sync account</span></span>](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [<span data-ttu-id="ff680-135">啟動同步處理服務</span><span class="sxs-lookup"><span data-stu-id="ff680-135">Start the Synchronization Service</span></span>](#start-the-synchronization-service)

#### <a name="abandon-the-existing-encryption-key"></a><span data-ttu-id="ff680-136">放棄現有的加密金鑰</span><span class="sxs-lookup"><span data-stu-id="ff680-136">Abandon the existing encryption key</span></span>
<span data-ttu-id="ff680-137">放棄現有的加密金鑰，以便能夠建立新的加密金鑰︰</span><span class="sxs-lookup"><span data-stu-id="ff680-137">Abandon the existing encryption key so that new encryption key can be created:</span></span>

1. <span data-ttu-id="ff680-138">以系統管理員身分登入您的 Azure AD Connect 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ff680-138">Log in to your Azure AD Connect Server as administrator.</span></span>

2. <span data-ttu-id="ff680-139">啟動新的 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="ff680-139">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="ff680-140">瀏覽至資料夾：`$env:Program Files\Microsoft Azure AD Sync\bin\`</span><span class="sxs-lookup"><span data-stu-id="ff680-140">Navigate to folder: `$env:Program Files\Microsoft Azure AD Sync\bin\`</span></span>

4. <span data-ttu-id="ff680-141">執行命令：`./miiskmu.exe /a`</span><span class="sxs-lookup"><span data-stu-id="ff680-141">Run the command: `./miiskmu.exe /a`</span></span>

![Azure AD Connect 同步處理加密金鑰公用程式](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-the-password-of-the-ad-ds-account"></a><span data-ttu-id="ff680-143">提供 AD DS 帳戶的密碼</span><span class="sxs-lookup"><span data-stu-id="ff680-143">Provide the password of the AD DS account</span></span>
<span data-ttu-id="ff680-144">因為儲存在資料庫內的現有密碼無法再解密，您必須為同步處理服務提供 AD DS 帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="ff680-144">As the existing passwords stored inside the database can no longer be decrypted, you need to provide the Synchronization Service with the password of the AD DS account.</span></span> <span data-ttu-id="ff680-145">同步處理服務會使用新的加密金鑰來將密碼加密︰</span><span class="sxs-lookup"><span data-stu-id="ff680-145">The Synchronization Service encrypts the passwords using the new encryption key:</span></span>

1. <span data-ttu-id="ff680-146">啟動同步處理服務管理員 ([開始] → [同步處理服務])。</span><span class="sxs-lookup"><span data-stu-id="ff680-146">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="ff680-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="ff680-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  
2. <span data-ttu-id="ff680-148">移至 [連接器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ff680-148">Go to the **Connectors** tab.</span></span>
3. <span data-ttu-id="ff680-149">選取與內部部署 AD 對應的 [AD 連接器]。</span><span class="sxs-lookup"><span data-stu-id="ff680-149">Select the **AD Connector** that corresponds to your on-premises AD.</span></span> <span data-ttu-id="ff680-150">如果您有多個 AD 連接器，請為每個連接器重複下列步驟。</span><span class="sxs-lookup"><span data-stu-id="ff680-150">If you have more than one AD connector, repeat the following steps for each of them.</span></span>
4. <span data-ttu-id="ff680-151">選取 [動作] 下方的 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="ff680-151">Under **Actions**, select **Properties**.</span></span>
5. <span data-ttu-id="ff680-152">在快顯對話方塊中，選取 [連線至 Active Directory 樹系]：</span><span class="sxs-lookup"><span data-stu-id="ff680-152">In the pop-up dialog, select **Connect to Active Directory Forest**:</span></span>
6. <span data-ttu-id="ff680-153">在 [密碼] 文字方塊中輸入 AD DS 帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="ff680-153">Enter the password of the AD DS account in the **Password** textbox.</span></span> <span data-ttu-id="ff680-154">如果您不知道該帳戶的密碼，您必須先將密碼設定為您知道的值，再執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="ff680-154">If you do not know its password, you must set it to a known value before performing this step.</span></span>
7. <span data-ttu-id="ff680-155">按一下 [確定] 以儲存新密碼，然後關閉快顯對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ff680-155">Click **OK** to save the new password and close the pop-up dialog.</span></span>
<span data-ttu-id="ff680-156">![Azure AD Connect 同步處理加密金鑰公用程式](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="ff680-156">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>

#### <a name="reinitialize-the-password-of-the-azure-ad-sync-account"></a><span data-ttu-id="ff680-157">重新初始化 Azure AD 同步處理帳戶的密碼</span><span class="sxs-lookup"><span data-stu-id="ff680-157">Reinitialize the password of the Azure AD sync account</span></span>
<span data-ttu-id="ff680-158">您無法將 Azure AD 服務帳戶的密碼直接提供給同步處理服務。</span><span class="sxs-lookup"><span data-stu-id="ff680-158">You cannot directly provide the password of the Azure AD service account to the Synchronization Service.</span></span> <span data-ttu-id="ff680-159">相反地，您必須使用 **Add-ADSyncAADServiceAccount** Cmdlet 來重新初始化 Azure AD 服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="ff680-159">Instead, you need to use the cmdlet **Add-ADSyncAADServiceAccount** to reinitialize the Azure AD service account.</span></span> <span data-ttu-id="ff680-160">此 Cmdlet 會重設帳戶密碼，並將密碼提供給同步處理服務︰</span><span class="sxs-lookup"><span data-stu-id="ff680-160">The cmdlet resets the account password and makes it available to the Synchronization Service:</span></span>

1. <span data-ttu-id="ff680-161">在 Azure AD Connect 伺服器上啟動新的 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="ff680-161">Start a new PowerShell session on the Azure AD Connect server.</span></span>
2. <span data-ttu-id="ff680-162">執行 `Add-ADSyncAADServiceAccount` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ff680-162">Run cmdlet `Add-ADSyncAADServiceAccount`.</span></span>
3. <span data-ttu-id="ff680-163">在快顯對話方塊中，提供 Azure AD 租用戶的 Azure AD 全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="ff680-163">In the pop-up dialog, provide the Azure AD Global admin credentials for your Azure AD tenant.</span></span>
<span data-ttu-id="ff680-164">![Azure AD Connect 同步處理加密金鑰公用程式](media/active-directory-aadconnectsync-encryption-key/key7.png)</span><span class="sxs-lookup"><span data-stu-id="ff680-164">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key7.png)</span></span>
4. <span data-ttu-id="ff680-165">如果成功，您會看到 PowerShell 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="ff680-165">If it is successful, you will see the PowerShell command prompt.</span></span>

#### <a name="start-the-synchronization-service"></a><span data-ttu-id="ff680-166">啟動同步處理服務</span><span class="sxs-lookup"><span data-stu-id="ff680-166">Start the Synchronization Service</span></span>
<span data-ttu-id="ff680-167">由於同步處理服務已可存取所需要的加密金鑰和所有密碼，您可以在 Windows 服務控制管理員中重新啟動該服務︰</span><span class="sxs-lookup"><span data-stu-id="ff680-167">Now that the Synchronization Service has access to the encryption key and all the passwords it needs, you can restart the service in the Windows Service Control Manager:</span></span>


1. <span data-ttu-id="ff680-168">移至 Windows 服務控制管理員 ([開始] → [服務])。</span><span class="sxs-lookup"><span data-stu-id="ff680-168">Go to Windows Service Control Manager (START → Services).</span></span>
2. <span data-ttu-id="ff680-169">選取 [Microsoft Azure AD 同步處理]，然後按一下 [重新啟動]。</span><span class="sxs-lookup"><span data-stu-id="ff680-169">Select **Microsoft Azure AD Sync** and click Restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff680-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ff680-170">Next steps</span></span>
<span data-ttu-id="ff680-171">**概觀主題**</span><span class="sxs-lookup"><span data-stu-id="ff680-171">**Overview topics**</span></span>

* [<span data-ttu-id="ff680-172">Azure AD Connect 同步處理：了解及自訂同步處理</span><span class="sxs-lookup"><span data-stu-id="ff680-172">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="ff680-173">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff680-173">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
