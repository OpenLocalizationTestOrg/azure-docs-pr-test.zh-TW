---
title: "搭配 Azure AD Connect 同步化 aaaImplement 密碼同步化 |Microsoft 文件"
description: "提供有關的資訊，密碼同步化的運作方式以及 tooset 組成。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 05f16c3e-9d23-45dc-afca-3d0fa9dbf501
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: a0401640f2a4d914419ee4446f923bb3a972389d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="implement-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="985d2-103">使用 Azure AD Connect 同步處理實作密碼同步處理</span><span class="sxs-lookup"><span data-stu-id="985d2-103">Implement password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="985d2-104">本文章提供您需要 toosynchronize 您的使用者密碼從內部部署 Active Directory 執行個體 tooa 雲端型 Azure Active Directory (Azure AD) 執行個體的資訊。</span><span class="sxs-lookup"><span data-stu-id="985d2-104">This article provides information that you need toosynchronize your user passwords from an on-premises Active Directory instance tooa cloud-based Azure Active Directory (Azure AD) instance.</span></span>

## <a name="what-is-password-synchronization"></a><span data-ttu-id="985d2-105">什麼是密碼同步處理</span><span class="sxs-lookup"><span data-stu-id="985d2-105">What is password synchronization</span></span>
<span data-ttu-id="985d2-106">hello 機率封鎖的從 tooa 忘記的密碼到期完成工作相關 toohello 數目的不同的密碼，您需要 tooremember。</span><span class="sxs-lookup"><span data-stu-id="985d2-106">hello probability that you're blocked from getting your work done due tooa forgotten password is related toohello number of different passwords you need tooremember.</span></span> <span data-ttu-id="985d2-107">hello 需要 tooremember，hello 高 hello 機率 tooforget 其中一個更多的密碼。</span><span class="sxs-lookup"><span data-stu-id="985d2-107">hello more passwords you need tooremember, hello higher hello probability tooforget one.</span></span> <span data-ttu-id="985d2-108">問題和密碼重設和其他密碼相關的問題有關的呼叫 hello 最多的技術支援資源。</span><span class="sxs-lookup"><span data-stu-id="985d2-108">Questions and calls about password resets and other password-related issues demand hello most helpdesk resources.</span></span>

<span data-ttu-id="985d2-109">密碼同步處理是一項功能使用 toosynchronize 使用者密碼從內部部署 Active Directory 執行個體 tooa 以雲端為基礎的 Azure AD 執行個體。</span><span class="sxs-lookup"><span data-stu-id="985d2-109">Password synchronization is a feature used toosynchronize user passwords from an on-premises Active Directory instance tooa cloud-based Azure AD instance.</span></span>
<span data-ttu-id="985d2-110">使用此功能 toosign tooAzure AD 服務，例如 Office 365、 Microsoft Intune、 CRM Online 和 Azure Active Directory 網域服務 (Azure AD DS) 中。</span><span class="sxs-lookup"><span data-stu-id="985d2-110">Use this feature toosign in tooAzure AD services like Office 365, Microsoft Intune, CRM Online, and Azure Active Directory Domain Services (Azure AD DS).</span></span> <span data-ttu-id="985d2-111">您登入 toohello 服務使用 hello toosign 用於 tooyour 相同的密碼在內部部署 Active Directory 執行個體。</span><span class="sxs-lookup"><span data-stu-id="985d2-111">You sign in toohello service by using hello same password you use toosign in tooyour on-premises Active Directory instance.</span></span>

![何謂 Azure AD Connect](./media/active-directory-aadconnectsync-implement-password-synchronization/arch1.png)

<span data-ttu-id="985d2-113">透過減少 hello 密碼數目，您的使用者需要 toomaintain toojust 其中一個。</span><span class="sxs-lookup"><span data-stu-id="985d2-113">By reducing hello number of passwords, your users need toomaintain toojust one.</span></span> <span data-ttu-id="985d2-114">密碼同步處理可協助您︰</span><span class="sxs-lookup"><span data-stu-id="985d2-114">Password synchronization helps you to:</span></span>

* <span data-ttu-id="985d2-115">改善使用者的 hello 產能。</span><span class="sxs-lookup"><span data-stu-id="985d2-115">Improve hello productivity of your users.</span></span>
* <span data-ttu-id="985d2-116">降低技術支援成本。</span><span class="sxs-lookup"><span data-stu-id="985d2-116">Reduce your helpdesk costs.</span></span>  

<span data-ttu-id="985d2-117">此外，如果您決定 toouse[與 Active Directory Federation Services (AD FS) 同盟](https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect)，萬一您的 AD FS 基礎結構失敗時，您可以選擇在設定密碼同步作業，以當作備份設定。</span><span class="sxs-lookup"><span data-stu-id="985d2-117">Also, if you decide toouse [Federation with Active Directory Federation Services (AD FS)](https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect), you can optionally set up password synchronization as a backup in case your AD FS infrastructure fails.</span></span>

<span data-ttu-id="985d2-118">密碼同步處理是藉由 Azure AD Connect 同步處理延伸模組 toohello 目錄同步作業功能。toouse 密碼同步處理您的環境中，您要：</span><span class="sxs-lookup"><span data-stu-id="985d2-118">Password synchronization is an extension toohello directory synchronization feature implemented by Azure AD Connect sync. toouse password synchronization in your environment, you need to:</span></span>

* <span data-ttu-id="985d2-119">安裝 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="985d2-119">Install Azure AD Connect.</span></span>  
* <span data-ttu-id="985d2-120">設定內部部署 Active Directory 執行個體與 Azure Active Directory 執行個體之間的目錄同步作業。</span><span class="sxs-lookup"><span data-stu-id="985d2-120">Configure directory synchronization between your on-premises Active Directory instance and your Azure Active Directory instance.</span></span>
* <span data-ttu-id="985d2-121">啟用密碼同步處理。</span><span class="sxs-lookup"><span data-stu-id="985d2-121">Enable password synchronization.</span></span>

<span data-ttu-id="985d2-122">如需詳細資訊，請參閱 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="985d2-122">For more details, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="985d2-123">如需針對 FIPS 和密碼同步處理所設定之 Azure Active Directory Domain Services 的詳細資訊，請參閱本文稍後的＜密碼同步處理和 FIPS＞。</span><span class="sxs-lookup"><span data-stu-id="985d2-123">For more details about Azure Active Directory Domain Services configured for FIPS and password synchronization, see "Password synchronization and FIPS" later in this article.</span></span>
>
>

## <a name="how-password-synchronization-works"></a><span data-ttu-id="985d2-124">密碼同步處理如何運作</span><span class="sxs-lookup"><span data-stu-id="985d2-124">How password synchronization works</span></span>
<span data-ttu-id="985d2-125">hello Active Directory 網域服務會將密碼儲存 hello 形式 hello 實際使用者密碼的雜湊值表示法。</span><span class="sxs-lookup"><span data-stu-id="985d2-125">hello Active Directory domain service stores passwords in hello form of a hash value representation of hello actual user password.</span></span> <span data-ttu-id="985d2-126">雜湊值是單向數學函式的結果 (hello*雜湊演算法*)。</span><span class="sxs-lookup"><span data-stu-id="985d2-126">A hash value is a result of a one-way mathematical function (hello *hashing algorithm*).</span></span> <span data-ttu-id="985d2-127">沒有密碼的單向函式 toohello 純文字版的 hello 方法 toorevert 的結果。</span><span class="sxs-lookup"><span data-stu-id="985d2-127">There is no method toorevert hello result of a one-way function toohello plain text version of a password.</span></span> <span data-ttu-id="985d2-128">您無法使用密碼雜湊 toosign tooyour 在內部部署網路中。</span><span class="sxs-lookup"><span data-stu-id="985d2-128">You cannot use a password hash toosign in tooyour on-premises network.</span></span>

<span data-ttu-id="985d2-129">您的密碼，Azure AD Connect 同步處理會擷取您的密碼雜湊，從 toosynchronize hello 在內部部署 Active Directory 執行個體。</span><span class="sxs-lookup"><span data-stu-id="985d2-129">toosynchronize your password, Azure AD Connect sync extracts your password hash from hello on-premises Active Directory instance.</span></span> <span data-ttu-id="985d2-130">套用額外的安全性處理 toohello 密碼雜湊之前同步處理 toohello Azure Active Directory 驗證服務。</span><span class="sxs-lookup"><span data-stu-id="985d2-130">Extra security processing is applied toohello password hash before it is synchronized toohello Azure Active Directory authentication service.</span></span> <span data-ttu-id="985d2-131">密碼會以每個使用者為基礎，依照時間先後順序來進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="985d2-131">Passwords are synchronized on a per-user basis and in chronological order.</span></span>

<span data-ttu-id="985d2-132">hello 實際資料流程 hello 密碼同步處理程序是類似 toohello 同步處理的使用者資料，例如顯示名稱或電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="985d2-132">hello actual data flow of hello password synchronization process is similar toohello synchronization of user data such as DisplayName or Email Addresses.</span></span> <span data-ttu-id="985d2-133">不過，密碼會同步處理頻率會比 hello 標準目錄同步處理期間，其他屬性。</span><span class="sxs-lookup"><span data-stu-id="985d2-133">However, passwords are synchronized more frequently than hello standard directory synchronization window for other attributes.</span></span> <span data-ttu-id="985d2-134">hello 密碼同步處理程序執行每 2 分鐘。</span><span class="sxs-lookup"><span data-stu-id="985d2-134">hello password synchronization process runs every 2 minutes.</span></span> <span data-ttu-id="985d2-135">您無法修改此程序的 hello 頻率。</span><span class="sxs-lookup"><span data-stu-id="985d2-135">You cannot modify hello frequency of this process.</span></span> <span data-ttu-id="985d2-136">當您同步處理密碼時，它會覆寫現有雲端密碼 hello。</span><span class="sxs-lookup"><span data-stu-id="985d2-136">When you synchronize a password, it overwrites hello existing cloud password.</span></span>

<span data-ttu-id="985d2-137">hello 第一次啟用 hello 密碼同步功能，它會執行初始同步處理的 hello 的範圍內的所有使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="985d2-137">hello first time you enable hello password synchronization feature, it performs an initial synchronization of hello passwords of all in-scope users.</span></span> <span data-ttu-id="985d2-138">您無法明確地定義您想 toosynchronize 使用者密碼的子集。</span><span class="sxs-lookup"><span data-stu-id="985d2-138">You cannot explicitly define a subset of user passwords that you want toosynchronize.</span></span>

<span data-ttu-id="985d2-139">當您變更在內部部署密碼時，hello 更新密碼會同步處理，通常會在幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="985d2-139">When you change an on-premises password, hello updated password is synchronized, most often in a matter of minutes.</span></span>
<span data-ttu-id="985d2-140">hello 密碼同步功能會自動重試失敗的同步處理嘗試。</span><span class="sxs-lookup"><span data-stu-id="985d2-140">hello password synchronization feature automatically retries failed synchronization attempts.</span></span> <span data-ttu-id="985d2-141">如果嘗試 toosynchronize 密碼時發生錯誤，錯誤會記錄在事件檢視器中。</span><span class="sxs-lookup"><span data-stu-id="985d2-141">If an error occurs during an attempt toosynchronize a password, an error is logged in your event viewer.</span></span>

<span data-ttu-id="985d2-142">hello 同步處理密碼的 hello 使用者目前登入沒有任何影響。</span><span class="sxs-lookup"><span data-stu-id="985d2-142">hello synchronization of a password has no impact on hello user  who is currently signed in.</span></span>
<span data-ttu-id="985d2-143">當您登入 tooa 雲端服務時，就會發生同步處理的密碼變更立即不影響目前的雲端服務工作階段。</span><span class="sxs-lookup"><span data-stu-id="985d2-143">Your current cloud service session is not immediately affected by a synchronized password change that occurs while you are signed in tooa cloud service.</span></span> <span data-ttu-id="985d2-144">不過，當 hello 雲端服務會要求您 tooauthenticate 一次，您需要 tooprovide 新密碼。</span><span class="sxs-lookup"><span data-stu-id="985d2-144">However, when hello cloud service requires you tooauthenticate again, you need tooprovide your new password.</span></span>

<span data-ttu-id="985d2-145">第二個時間 tooauthenticate tooAzure AD，不論它們是否簽署 tootheir 公司網路中時，使用者必須輸入其公司認證。</span><span class="sxs-lookup"><span data-stu-id="985d2-145">A user must enter their corporate credentials a second time tooauthenticate tooAzure AD, regardless of whether they're signed in tootheir corporate network.</span></span> <span data-ttu-id="985d2-146">這些模式可以最小化，不過，如果 hello 使用者在登入時 (KMSI) 核取方塊選取 hello 讓我保持登。</span><span class="sxs-lookup"><span data-stu-id="985d2-146">These pattern can be minimized, however, if hello user selects hello Keep me signed in (KMSI) check box at sign in.</span></span> <span data-ttu-id="985d2-147">此選取動作會設定工作階段 Cookie 在短期間內略過驗證。</span><span class="sxs-lookup"><span data-stu-id="985d2-147">This selection sets a session cookie that bypasses authentication for a short period.</span></span> <span data-ttu-id="985d2-148">KMSI 行為可以啟用或停用 hello Azure AD 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="985d2-148">KMSI behavior can be enabled or disabled by hello Azure AD administrator.</span></span>

> [!NOTE]
> <span data-ttu-id="985d2-149">密碼同步處理才支援 Active Directory 中的 hello 物件類型使用者。</span><span class="sxs-lookup"><span data-stu-id="985d2-149">Password sync is only supported for hello object type user in Active Directory.</span></span> <span data-ttu-id="985d2-150">不支援 hello iNetOrgPerson 物件類型。</span><span class="sxs-lookup"><span data-stu-id="985d2-150">It is not supported for hello iNetOrgPerson object type.</span></span>

### <a name="detailed-description-of-how-password-synchronization-works"></a><span data-ttu-id="985d2-151">密碼同步處理運作方式的詳細描述</span><span class="sxs-lookup"><span data-stu-id="985d2-151">Detailed description of how password synchronization works</span></span>
<span data-ttu-id="985d2-152">hello 以下描述深入了解密碼同步處理 Active Directory 與 Azure AD 之間的運作方式。</span><span class="sxs-lookup"><span data-stu-id="985d2-152">hello following describes in-depth how password synchronization works between Active Directory and Azure AD.</span></span>

![詳細的密碼流程](./media/active-directory-aadconnectsync-implement-password-synchronization/arch3.png)


1. <span data-ttu-id="985d2-154">每兩分鐘，hello AD 連線伺服器上的 hello 密碼同步處理代理程式要求儲存的密碼雜湊 （hello unicodePwd 屬性） 的 DC，以透過標準的 hello [MS DRSR](https://msdn.microsoft.com/library/cc228086.aspx)使用 toosynchronize 資料複寫通訊協定。之間的 Dc。</span><span class="sxs-lookup"><span data-stu-id="985d2-154">Every two minutes, hello password synchronization agent on hello AD Connect server requests stored password hashes (hello unicodePwd attribute) from a DC via hello standard [MS-DRSR](https://msdn.microsoft.com/library/cc228086.aspx) replication protocol used toosynchronize data between DCs.</span></span> <span data-ttu-id="985d2-155">hello 服務帳戶必須具有複寫目錄變更 」 和 「 複寫目錄變更所有 AD （授與的預設安裝） 的權限 tooobtain hello 密碼雜湊。</span><span class="sxs-lookup"><span data-stu-id="985d2-155">hello service account must have Replicate Directory Changes and Replicate Directory Changes All AD permissions (granted by default on installation) tooobtain hello password hashes.</span></span>
2. <span data-ttu-id="985d2-156">在傳送之前，hello DC hello MD4 密碼雜湊會使用加密的金鑰[MD5](http://www.rfc-editor.org/rfc/rfc1321.txt) hello RPC 工作階段金鑰和 salt 的雜湊。</span><span class="sxs-lookup"><span data-stu-id="985d2-156">Before sending, hello DC encrypts hello MD4 password hash by using a key that is a [MD5](http://www.rfc-editor.org/rfc/rfc1321.txt) hash of hello RPC session key and a salt.</span></span> <span data-ttu-id="985d2-157">接著會透過 RPC 傳送嗨結果 toohello 密碼同步處理代理程式。</span><span class="sxs-lookup"><span data-stu-id="985d2-157">It then sends hello result toohello password synchronization agent over RPC.</span></span> <span data-ttu-id="985d2-158">hello DC 也會傳遞 hello salt toohello 同步代理程式利用 hello DC 複寫通訊協定，因此 hello 代理程式無法 toodecrypt hello 信封。</span><span class="sxs-lookup"><span data-stu-id="985d2-158">hello DC also passes hello salt toohello synchronization agent by using hello DC replication protocol, so hello agent will be able toodecrypt hello envelope.</span></span>
3.  <span data-ttu-id="985d2-159">Hello 密碼同步處理代理程式有 hello 加密的信封之後，就會使用[MD5CryptoServiceProvider](https://msdn.microsoft.com/library/System.Security.Cryptography.MD5CryptoServiceProvider.aspx)和 hello salt toogenerate 金鑰 toodecrypt hello 收到資料後 tooits 原始 MD4 格式。</span><span class="sxs-lookup"><span data-stu-id="985d2-159">After hello password synchronization agent has hello encrypted envelope, it uses [MD5CryptoServiceProvider](https://msdn.microsoft.com/library/System.Security.Cryptography.MD5CryptoServiceProvider.aspx) and hello salt toogenerate a key toodecrypt hello received data back tooits original MD4 format.</span></span> <span data-ttu-id="985d2-160">沒有任何一點 hello 密碼同步處理代理程式沒有存取 toohello 純文字密碼。</span><span class="sxs-lookup"><span data-stu-id="985d2-160">At no point does hello password synchronization agent have access toohello clear text password.</span></span> <span data-ttu-id="985d2-161">hello MD5 使用密碼同步處理代理程式的主要是以 hello DC，複寫通訊協定相容性，它只會用於內部部署 hello DC 與 hello 密碼同步處理代理程式之間。</span><span class="sxs-lookup"><span data-stu-id="985d2-161">hello password synchronization agent’s use of MD5 is strictly for replication protocol compatibility with hello DC, and it is only used on premises between hello DC and hello password synchronization agent.</span></span>
4.  <span data-ttu-id="985d2-162">hello 密碼同步處理代理程式第一個轉換 hello 雜湊 tooa 32 位元組十六進位字串，來展開 hello 16 位元組二進位密碼雜湊 too64 位元組，則此字串轉換成以 utf-16 編碼的二進位檔放回。</span><span class="sxs-lookup"><span data-stu-id="985d2-162">hello password synchronization agent expands hello 16-byte binary password hash too64 bytes by first converting hello hash tooa 32-byte hexadecimal string, then converting this string back into binary with UTF-16 encoding.</span></span>
5.  <span data-ttu-id="985d2-163">hello 密碼同步處理代理程式會加入 salt，組成 10 位元組長度 salt，toohello 64 位元組的二進位 toofurther 保護 hello 原始雜湊。</span><span class="sxs-lookup"><span data-stu-id="985d2-163">hello password synchronization agent adds a salt, consisting of a 10-byte length salt, toohello 64-byte binary toofurther protect hello original hash.</span></span>
6.  <span data-ttu-id="985d2-164">hello 密碼同步處理代理程式結合 hello MD4 雜湊和 salt，然後輸入 hello [PBKDF2](https://www.ietf.org/rfc/rfc2898.txt)函式。</span><span class="sxs-lookup"><span data-stu-id="985d2-164">hello password synchronization agent then combines hello MD4 hash plus salt, and inputs it into hello [PBKDF2](https://www.ietf.org/rfc/rfc2898.txt) function.</span></span> <span data-ttu-id="985d2-165">1000 個反覆運算的 hello [hmac-sha256](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx)會使用索引鍵的雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="985d2-165">1000 iterations of hello [HMAC-SHA256](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) keyed hashing algorithm is used.</span></span> 
7.  <span data-ttu-id="985d2-166">hello 密碼同步處理代理程式會採用 hello 產生 32 位元雜湊，串連這兩個 hello salt hello SHA256 反覆項目 tooit （適用於使用 Azure ad） 的數目再傳輸來自 Azure AD Connect tooAzure AD 透過 SSL 的 hello 字串。</span><span class="sxs-lookup"><span data-stu-id="985d2-166">hello password synchronization agent takes hello resulting 32-byte hash, concatenates both hello salt and hello number of SHA256 iterations tooit (for use by Azure AD), then transmits hello string from Azure AD Connect tooAzure AD over SSL.</span></span></br> 
8.  <span data-ttu-id="985d2-167">當使用者嘗試 toosign tooAzure AD 中的，並輸入其密碼、 hello 密碼透過 hello 執行相同的 MD4 + salt + PBKDF2 + hmac-sha256 程序。</span><span class="sxs-lookup"><span data-stu-id="985d2-167">When a user attempts toosign in tooAzure AD and enters their password, hello password is run through hello same MD4+salt+PBKDF2+HMAC-SHA256 process.</span></span> <span data-ttu-id="985d2-168">如果 hello 產生雜湊符合儲存在 Azure AD 中的 hello 雜湊，hello 使用者已進入 hello 正確的密碼，並驗證。</span><span class="sxs-lookup"><span data-stu-id="985d2-168">If hello resulting hash matches hello hash stored in Azure AD, hello user has entered hello correct password and is authenticated.</span></span> 

>[!Note] 
><span data-ttu-id="985d2-169">hello 原始 MD4 雜湊不是傳輸的 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="985d2-169">hello original MD4 hash is not transmitted tooAzure AD.</span></span> <span data-ttu-id="985d2-170">相反地，會傳送 hello hello 原始的 MD4 雜湊 SHA256 雜湊。</span><span class="sxs-lookup"><span data-stu-id="985d2-170">Instead, hello SHA256 hash of hello original MD4 hash is transmitted.</span></span> <span data-ttu-id="985d2-171">如此一來，取得儲存在 Azure AD 中的 hello 雜湊時，如果它不能在內部部署密碼的雜湊攻擊中。</span><span class="sxs-lookup"><span data-stu-id="985d2-171">As a result, if hello hash stored in Azure AD is obtained, it cannot be used in an on-premises pass-the-hash attack.</span></span>

### <a name="how-password-synchronization-works-with-azure-active-directory-domain-services"></a><span data-ttu-id="985d2-172">密碼同步處理如何與 Azure Active Directory Domain Services 搭配運作</span><span class="sxs-lookup"><span data-stu-id="985d2-172">How password synchronization works with Azure Active Directory Domain Services</span></span>
<span data-ttu-id="985d2-173">您也可以使用 hello 密碼同步處理功能 toosynchronize 在內部部署密碼太[Azure Active Directory 網域服務](../../active-directory-domain-services/active-directory-ds-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="985d2-173">You can also use hello password synchronization feature toosynchronize your on-premises passwords too[Azure Active Directory Domain Services](../../active-directory-domain-services/active-directory-ds-overview.md).</span></span> <span data-ttu-id="985d2-174">在此案例中，hello Azure Active Directory 網域服務執行個體會向使用者在 hello 雲端中的驗證您在內部部署 Active Directory 執行個體中所有 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="985d2-174">In this scenario, hello Azure Active Directory Domain Services instance authenticates your users in hello cloud with all hello methods available in your on-premises Active Directory instance.</span></span> <span data-ttu-id="985d2-175">此案例的 hello 體驗為在內部部署環境中類似的 toousing hello Active Directory 遷移工具 (ADMT)。</span><span class="sxs-lookup"><span data-stu-id="985d2-175">hello experience of this scenario is similar toousing hello Active Directory Migration Tool (ADMT) in an on-premises environment.</span></span>

### <a name="security-considerations"></a><span data-ttu-id="985d2-176">安全性考量</span><span class="sxs-lookup"><span data-stu-id="985d2-176">Security considerations</span></span>
<span data-ttu-id="985d2-177">當同步處理密碼，hello 純文字密碼版本不是公開的 toohello 密碼同步功能、 tooAzure AD，或任何相關聯的 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="985d2-177">When synchronizing passwords, hello plain-text version of your password is not exposed toohello password synchronization feature, tooAzure AD, or any of hello associated services.</span></span>

<span data-ttu-id="985d2-178">使用者的驗證會針對 Azure AD 中，而不是反對 hello 組織自己的 Active Directory 執行個體。</span><span class="sxs-lookup"><span data-stu-id="985d2-178">User authentication takes place against Azure AD rather than against hello organization's own Active Directory instance.</span></span> <span data-ttu-id="985d2-179">如果您的組織有疑慮留下任何形式的密碼資料 hello 內部部署，您可以考慮該 hello SHA256 密碼資料儲存在 Azure AD-hello 事實的原始 MD4 雜湊 hello-雜湊是遠比什麼儲存在 Active Directory 安全。</span><span class="sxs-lookup"><span data-stu-id="985d2-179">If your organization has concerns about password data in any form leaving hello premises, consider hello fact that hello SHA256 password data stored in Azure AD--a hash of hello original MD4 hash--is significantly more secure than what is stored in Active Directory.</span></span> <span data-ttu-id="985d2-180">此外，無法解密此 SHA256 雜湊，因為它無法被帶回 toohello 組織的 Active Directory 環境，呈現為有效的使用者密碼在傳遞的雜湊攻擊中。</span><span class="sxs-lookup"><span data-stu-id="985d2-180">Further, because this SHA256 hash cannot be decrypted, it cannot be brought back toohello organization's Active Directory environment and presented as a valid user password in a pass-the-hash attack.</span></span>





### <a name="password-policy-considerations"></a><span data-ttu-id="985d2-181">密碼原則考量</span><span class="sxs-lookup"><span data-stu-id="985d2-181">Password policy considerations</span></span>
<span data-ttu-id="985d2-182">啟用密碼同步處理會影響兩種類型的密碼原則：</span><span class="sxs-lookup"><span data-stu-id="985d2-182">There are two types of password policies that are affected by enabling password synchronization:</span></span>

* <span data-ttu-id="985d2-183">密碼複雜性原則</span><span class="sxs-lookup"><span data-stu-id="985d2-183">Password complexity policy</span></span>
* <span data-ttu-id="985d2-184">密碼到期原則</span><span class="sxs-lookup"><span data-stu-id="985d2-184">Password expiration policy</span></span>

#### <a name="password-complexity-policy"></a><span data-ttu-id="985d2-185">密碼複雜性原則</span><span class="sxs-lookup"><span data-stu-id="985d2-185">Password complexity policy</span></span>  
<span data-ttu-id="985d2-186">啟用密碼同步處理時，在內部部署 Active Directory 執行個體中的 hello 密碼複雜性原則覆寫已同步處理使用者的 hello 雲端中的複雜性原則。</span><span class="sxs-lookup"><span data-stu-id="985d2-186">When password synchronization is enabled, hello password complexity policies in your on-premises Active Directory instance override complexity policies in hello cloud for synchronized users.</span></span> <span data-ttu-id="985d2-187">您可以使用所有 hello 有效密碼從您在內部部署 Active Directory 執行個體 tooaccess Azure AD 服務。</span><span class="sxs-lookup"><span data-stu-id="985d2-187">You can use all of hello valid passwords from your on-premises Active Directory instance tooaccess Azure AD services.</span></span>

> [!NOTE]
> <span data-ttu-id="985d2-188">直接在 hello 雲端中建立的使用者密碼仍主旨 toopassword 原則 hello 雲端中所定義。</span><span class="sxs-lookup"><span data-stu-id="985d2-188">Passwords for users that are created directly in hello cloud are still subject toopassword policies as defined in hello cloud.</span></span>

#### <a name="password-expiration-policy"></a><span data-ttu-id="985d2-189">密碼到期原則</span><span class="sxs-lookup"><span data-stu-id="985d2-189">Password expiration policy</span></span>  
<span data-ttu-id="985d2-190">如果使用者在 hello 的密碼同步處理的範圍內，hello 雲端帳戶密碼設定得*永遠不過期*。</span><span class="sxs-lookup"><span data-stu-id="985d2-190">If a user is in hello scope of password synchronization, hello cloud account password is set too*Never Expire*.</span></span>

<span data-ttu-id="985d2-191">您可以繼續 toosign tooyour 雲端服務中，使用同步處理內部部署環境中已過期的密碼。</span><span class="sxs-lookup"><span data-stu-id="985d2-191">You can continue toosign in tooyour cloud services by using a synchronized password that is expired in your on-premises environment.</span></span> <span data-ttu-id="985d2-192">更新您的雲端密碼 hello 變更 hello 密碼 hello 在內部部署環境中的下一次。</span><span class="sxs-lookup"><span data-stu-id="985d2-192">Your cloud password is updated hello next time you change hello password in hello on-premises environment.</span></span>

#### <a name="account-expiration"></a><span data-ttu-id="985d2-193">帳戶到期</span><span class="sxs-lookup"><span data-stu-id="985d2-193">Account expiration</span></span>
<span data-ttu-id="985d2-194">如果您的組織使用 hello accountExpires 屬性做為使用者帳戶管理的一部分，請注意這個屬性不是已同步處理的 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="985d2-194">If your organization uses hello accountExpires attribute as part of user account management, be aware that this attribute is not synchronized tooAzure AD.</span></span> <span data-ttu-id="985d2-195">如此一來，針對密碼同步處理設定之環境中到期的 Active Directory 帳戶在 Azure AD 仍然為作用中。</span><span class="sxs-lookup"><span data-stu-id="985d2-195">As a result, an expired Active Directory account in an environment configured for password synchronization will still be active in Azure AD.</span></span> <span data-ttu-id="985d2-196">我們建議如果 hello 帳戶到期，工作流程動作應該觸發停用 hello 使用者的 Azure AD 帳戶的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="985d2-196">We recommend that if hello account is expired, a workflow action should trigger a PowerShell script that disables hello user's Azure AD account.</span></span> <span data-ttu-id="985d2-197">相反地，當開啟 hello 帳戶時，hello Azure AD 執行個體應該會開啟。</span><span class="sxs-lookup"><span data-stu-id="985d2-197">Conversely, when hello account is turned on, hello Azure AD instance should be turned on.</span></span>

### <a name="overwrite-synchronized-passwords"></a><span data-ttu-id="985d2-198">覆寫已同步的密碼</span><span class="sxs-lookup"><span data-stu-id="985d2-198">Overwrite synchronized passwords</span></span>
<span data-ttu-id="985d2-199">系統管理員可以使用 Windows PowerShell 手動重設您的密碼。</span><span class="sxs-lookup"><span data-stu-id="985d2-199">An administrator can manually reset your password by using Windows PowerShell.</span></span>

<span data-ttu-id="985d2-200">在此情況下，hello 新密碼會覆寫已同步處理的密碼，並在 hello 雲端中定義的所有密碼原則都會套用的 toohello 新密碼。</span><span class="sxs-lookup"><span data-stu-id="985d2-200">In this case, hello new password overrides your synchronized password, and all password policies defined in hello cloud are applied toohello new password.</span></span>

<span data-ttu-id="985d2-201">如果您再次變更內部部署密碼，hello 新密碼會同步處理 toohello 雲端，而且它會覆寫 hello 手動更新密碼。</span><span class="sxs-lookup"><span data-stu-id="985d2-201">If you change your on-premises password again, hello new password is synchronized toohello cloud, and it overrides hello manually updated password.</span></span>

<span data-ttu-id="985d2-202">hello 同步處理密碼的 hello Azure 登入的使用者沒有任何影響。</span><span class="sxs-lookup"><span data-stu-id="985d2-202">hello synchronization of a password has no impact on hello Azure user who is signed in.</span></span> <span data-ttu-id="985d2-203">您已登入 tooa 雲端服務時，就會發生同步處理的密碼變更立即不影響目前的雲端服務工作階段。</span><span class="sxs-lookup"><span data-stu-id="985d2-203">Your current cloud service session is not immediately affected by a synchronized password change that occurs while you're signed in tooa cloud service.</span></span> <span data-ttu-id="985d2-204">KMSI 擴充 hello 持續時間，這項差異。</span><span class="sxs-lookup"><span data-stu-id="985d2-204">KMSI extends hello duration of this difference.</span></span> <span data-ttu-id="985d2-205">當 hello 雲端服務會要求您 tooauthenticate 一次時，您需要 tooprovide 新密碼。</span><span class="sxs-lookup"><span data-stu-id="985d2-205">When hello cloud service requires you tooauthenticate again, you need tooprovide your new password.</span></span>

### <a name="additional-advantages"></a><span data-ttu-id="985d2-206">其他優點</span><span class="sxs-lookup"><span data-stu-id="985d2-206">Additional advantages</span></span>

- <span data-ttu-id="985d2-207">一般而言，密碼同步化是簡單 tooimplement 比 federation service。</span><span class="sxs-lookup"><span data-stu-id="985d2-207">Generally, password synchronization is simpler tooimplement than a federation service.</span></span> <span data-ttu-id="985d2-208">它不需要任何額外的伺服器，並排除高可用性的同盟服務 tooauthenticate 使用者相依性。</span><span class="sxs-lookup"><span data-stu-id="985d2-208">It doesn't require any additional servers, and eliminates dependence on a highly available federation service tooauthenticate users.</span></span> 
- <span data-ttu-id="985d2-209">也可以加入 toofederation 中啟用密碼同步處理。</span><span class="sxs-lookup"><span data-stu-id="985d2-209">Password synchronization can also be enabled in addition toofederation.</span></span> <span data-ttu-id="985d2-210">您可以將它作為同盟服務發生中斷時的後援服務。</span><span class="sxs-lookup"><span data-stu-id="985d2-210">It may be used as a fallback if your federation service experiences an outage.</span></span>












## <a name="enable-password-synchronization"></a><span data-ttu-id="985d2-211">啟用密碼同步處理</span><span class="sxs-lookup"><span data-stu-id="985d2-211">Enable password synchronization</span></span>
<span data-ttu-id="985d2-212">當您安裝 Azure AD Connect 使用 hello**快速設定**選項時，密碼同步化會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="985d2-212">When you install Azure AD Connect by using hello **Express Settings** option, password synchronization is automatically enabled.</span></span> <span data-ttu-id="985d2-213">如需詳細資訊，請參閱[使用快速設定開始使用 Azure AD Connect](active-directory-aadconnect-get-started-express.md)。</span><span class="sxs-lookup"><span data-stu-id="985d2-213">For more details, see [Getting started with Azure AD Connect using express settings](active-directory-aadconnect-get-started-express.md).</span></span>

<span data-ttu-id="985d2-214">如果您使用自訂設定，當您安裝 Azure AD Connect，密碼同步功能 hello 使用者登入頁面。</span><span class="sxs-lookup"><span data-stu-id="985d2-214">If you use custom settings when you install Azure AD Connect, password synchronization is available on hello user sign-in page.</span></span> <span data-ttu-id="985d2-215">如需詳細資訊，請參閱[自訂 Azure AD Connect 安裝](active-directory-aadconnect-get-started-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="985d2-215">For more details, see [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

![啟用密碼同步處理](./media/active-directory-aadconnectsync-implement-password-synchronization/usersignin.png)

### <a name="password-synchronization-and-fips"></a><span data-ttu-id="985d2-217">密碼同步處理和 FIPS</span><span class="sxs-lookup"><span data-stu-id="985d2-217">Password synchronization and FIPS</span></span>
<span data-ttu-id="985d2-218">如果您的伺服器已經鎖定，根據 tooFederal 資訊處理標準 (FIPS)，則會停用 MD5。</span><span class="sxs-lookup"><span data-stu-id="985d2-218">If your server has been locked down according tooFederal Information Processing Standard (FIPS), then MD5 is disabled.</span></span>

<span data-ttu-id="985d2-219">**密碼同步化的 tooenable MD5 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="985d2-219">**tooenable MD5 for password synchronization, perform hello following steps:**</span></span>

1. <span data-ttu-id="985d2-220">移 too%programfiles%\Azure AD Sync\Bin。</span><span class="sxs-lookup"><span data-stu-id="985d2-220">Go too%programfiles%\Azure AD Sync\Bin.</span></span>
2. <span data-ttu-id="985d2-221">開啟 miiserver.exe.config。</span><span class="sxs-lookup"><span data-stu-id="985d2-221">Open miiserver.exe.config.</span></span>
3. <span data-ttu-id="985d2-222">請移至在 hello hello 檔案結尾處的 toohello configuration/runtime 節點。</span><span class="sxs-lookup"><span data-stu-id="985d2-222">Go toohello configuration/runtime node at hello end of hello file.</span></span>
4. <span data-ttu-id="985d2-223">新增節點的後的 hello:`<enforceFIPSPolicy enabled="false"/>`</span><span class="sxs-lookup"><span data-stu-id="985d2-223">Add hello following node: `<enforceFIPSPolicy enabled="false"/>`</span></span>
5. <span data-ttu-id="985d2-224">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="985d2-224">Save your changes.</span></span>

<span data-ttu-id="985d2-225">如需參考，此程式碼片段就是其大致樣貌︰</span><span class="sxs-lookup"><span data-stu-id="985d2-225">For reference, this snippet is what it should look like:</span></span>

```
    <configuration>
        <runtime>
            <enforceFIPSPolicy enabled="false"/>
        </runtime>
    </configuration>
```

<span data-ttu-id="985d2-226">如需安全性和 FIPS 的詳細資訊，請參閱 [AAD 密碼同步、加密和 FIPS 合規性](https://blogs.technet.microsoft.com/enterprisemobility/2014/06/28/aad-password-sync-encryption-and-fips-compliance/)。</span><span class="sxs-lookup"><span data-stu-id="985d2-226">For information about security and FIPS, see [AAD Password Sync, encryption and FIPS compliance](https://blogs.technet.microsoft.com/enterprisemobility/2014/06/28/aad-password-sync-encryption-and-fips-compliance/).</span></span>

## <a name="troubleshoot-password-synchronization"></a><span data-ttu-id="985d2-227">對密碼同步處理進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="985d2-227">Troubleshoot password synchronization</span></span>
<span data-ttu-id="985d2-228">如果您在進行密碼同步處理時發生問題，請參閱[針對密碼同步處理進行疑難排解](active-directory-aadconnectsync-troubleshoot-password-synchronization.md)。</span><span class="sxs-lookup"><span data-stu-id="985d2-228">If you have problems with password synchronization, see [Troubleshoot password synchronization](active-directory-aadconnectsync-troubleshoot-password-synchronization.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="985d2-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="985d2-229">Next steps</span></span>
* [<span data-ttu-id="985d2-230">Azure AD Connect 同步處理：自訂同步處理選項</span><span class="sxs-lookup"><span data-stu-id="985d2-230">Azure AD Connect sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="985d2-231">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="985d2-231">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
