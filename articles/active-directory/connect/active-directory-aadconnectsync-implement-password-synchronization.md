---
title: "使用 Azure AD Connect 同步處理實作密碼同步處理 | Microsoft Docs"
description: "提供有關密碼同步處理如何運作以及如何設定的資訊。"
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
ms.openlocfilehash: db9b1578a235be9018fc1985cc75a0a05ee47b3a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="implement-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="7a5ae-103">使用 Azure AD Connect 同步處理實作密碼同步處理</span><span class="sxs-lookup"><span data-stu-id="7a5ae-103">Implement password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="7a5ae-104">本文提供您所需資訊，以讓您將使用者密碼從內部部署 Active Directory 執行個體同步處理至雲端式 Azure Active Directory (Azure AD) 執行個體。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-104">This article provides information that you need to synchronize your user passwords from an on-premises Active Directory instance to a cloud-based Azure Active Directory (Azure AD) instance.</span></span>

## <a name="what-is-password-synchronization"></a><span data-ttu-id="7a5ae-105">什麼是密碼同步處理</span><span class="sxs-lookup"><span data-stu-id="7a5ae-105">What is password synchronization</span></span>
<span data-ttu-id="7a5ae-106">您因為忘記密碼而無法完成工作的機率，與您必須記住的不同密碼數目有關。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-106">The probability that you're blocked from getting your work done due to a forgotten password is related to the number of different passwords you need to remember.</span></span> <span data-ttu-id="7a5ae-107">必須記住的密碼越多，將其中之一遺忘的機率就越高。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-107">The more passwords you need to remember, the higher the probability to forget one.</span></span> <span data-ttu-id="7a5ae-108">關於密碼重設和其他密碼相關問題的疑問和來電，佔據了最多的技術服務資源。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-108">Questions and calls about password resets and other password-related issues demand the most helpdesk resources.</span></span>

<span data-ttu-id="7a5ae-109">密碼同步處理功能可用來將使用者密碼從內部部署 Active Directory 執行個體同步處理至雲端式 Azure AD 執行個體。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-109">Password synchronization is a feature used to synchronize user passwords from an on-premises Active Directory instance to a cloud-based Azure AD instance.</span></span>
<span data-ttu-id="7a5ae-110">使用此功能即可登入 Azure AD 服務，例如 Office 365、Microsoft Intune、CRM Online 和 Azure Active Directory Domain Services (Azure AD DS)。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-110">Use this feature to sign in to Azure AD services like Office 365, Microsoft Intune, CRM Online, and Azure Active Directory Domain Services (Azure AD DS).</span></span> <span data-ttu-id="7a5ae-111">用來登入服務的密碼和您用來登入內部部署 Active Directory 執行個體的密碼相同。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-111">You sign in to the service by using the same password you use to sign in to your on-premises Active Directory instance.</span></span>

![何謂 Azure AD Connect](./media/active-directory-aadconnectsync-implement-password-synchronization/arch1.png)

<span data-ttu-id="7a5ae-113">透過減少密碼數量，讓您的使用者只需要維護一個密碼。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-113">By reducing the number of passwords, your users need to maintain to just one.</span></span> <span data-ttu-id="7a5ae-114">密碼同步處理可協助您︰</span><span class="sxs-lookup"><span data-stu-id="7a5ae-114">Password synchronization helps you to:</span></span>

* <span data-ttu-id="7a5ae-115">提升使用者的生產力。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-115">Improve the productivity of your users.</span></span>
* <span data-ttu-id="7a5ae-116">降低技術支援成本。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-116">Reduce your helpdesk costs.</span></span>  

<span data-ttu-id="7a5ae-117">此外，如果您選擇使用[與 Active Directory Federation Services (AD FS) 同盟](https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect)，則可以選擇性地設定密碼同步處理來作為 AD FS 基礎結構失敗時的備用方式。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-117">Also, if you decide to use [Federation with Active Directory Federation Services (AD FS)](https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect), you can optionally set up password synchronization as a backup in case your AD FS infrastructure fails.</span></span>

<span data-ttu-id="7a5ae-118">密碼同步處理是 Azure AD Connect 同步處理實作的目錄同步作業功能的延伸。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-118">Password synchronization is an extension to the directory synchronization feature implemented by Azure AD Connect sync.</span></span> <span data-ttu-id="7a5ae-119">若要在環境中使用密碼同步處理，您需要︰</span><span class="sxs-lookup"><span data-stu-id="7a5ae-119">To use password synchronization in your environment, you need to:</span></span>

* <span data-ttu-id="7a5ae-120">安裝 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-120">Install Azure AD Connect.</span></span>  
* <span data-ttu-id="7a5ae-121">設定內部部署 Active Directory 執行個體與 Azure Active Directory 執行個體之間的目錄同步作業。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-121">Configure directory synchronization between your on-premises Active Directory instance and your Azure Active Directory instance.</span></span>
* <span data-ttu-id="7a5ae-122">啟用密碼同步處理。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-122">Enable password synchronization.</span></span>

<span data-ttu-id="7a5ae-123">如需詳細資訊，請參閱 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-123">For more details, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7a5ae-124">如需針對 FIPS 和密碼同步處理所設定之 Azure Active Directory Domain Services 的詳細資訊，請參閱本文稍後的＜密碼同步處理和 FIPS＞。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-124">For more details about Azure Active Directory Domain Services configured for FIPS and password synchronization, see "Password synchronization and FIPS" later in this article.</span></span>
>
>

## <a name="how-password-synchronization-works"></a><span data-ttu-id="7a5ae-125">密碼同步處理如何運作</span><span class="sxs-lookup"><span data-stu-id="7a5ae-125">How password synchronization works</span></span>
<span data-ttu-id="7a5ae-126">Active Directory 網域服務是以代表使用者實際密碼的雜湊值格式儲存密碼。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-126">The Active Directory domain service stores passwords in the form of a hash value representation of the actual user password.</span></span> <span data-ttu-id="7a5ae-127">雜湊值是單向數學函式 (「雜湊演算法」) 的計算結果。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-127">A hash value is a result of a one-way mathematical function (the *hashing algorithm*).</span></span> <span data-ttu-id="7a5ae-128">沒有任何方法可將單向函式的結果還原為純文字版本的密碼。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-128">There is no method to revert the result of a one-way function to the plain text version of a password.</span></span> <span data-ttu-id="7a5ae-129">您無法使用密碼雜湊來登入您的內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-129">You cannot use a password hash to sign in to your on-premises network.</span></span>

<span data-ttu-id="7a5ae-130">為了同步密碼，Azure AD Connect 同步處理會從內部部署的 Active Directory 執行個體擷取您的密碼雜湊。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-130">To synchronize your password, Azure AD Connect sync extracts your password hash from the on-premises Active Directory instance.</span></span> <span data-ttu-id="7a5ae-131">在將密碼雜湊與 Azure Active Directory 驗證服務同步之前，會進行額外的安全性處理。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-131">Extra security processing is applied to the password hash before it is synchronized to the Azure Active Directory authentication service.</span></span> <span data-ttu-id="7a5ae-132">密碼會以每個使用者為基礎，依照時間先後順序來進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-132">Passwords are synchronized on a per-user basis and in chronological order.</span></span>

<span data-ttu-id="7a5ae-133">密碼同步處理程序的實際資料流程，就類似同步處理 DisplayName 或電子郵件地址等使用者資料。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-133">The actual data flow of the password synchronization process is similar to the synchronization of user data such as DisplayName or Email Addresses.</span></span> <span data-ttu-id="7a5ae-134">不過，相較於其他屬性的標準目錄同步作業週期，密碼會更頻繁地進行同步。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-134">However, passwords are synchronized more frequently than the standard directory synchronization window for other attributes.</span></span> <span data-ttu-id="7a5ae-135">密碼同步處理程序每 2 分鐘會執行一次。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-135">The password synchronization process runs every 2 minutes.</span></span> <span data-ttu-id="7a5ae-136">您無法修改此程序的執行頻率。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-136">You cannot modify the frequency of this process.</span></span> <span data-ttu-id="7a5ae-137">當您同步處理密碼時，它便會覆寫現有的雲端密碼。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-137">When you synchronize a password, it overwrites the existing cloud password.</span></span>

<span data-ttu-id="7a5ae-138">第一次啟用密碼同步功能時，它會對範圍內的所有使用者執行初次的密碼同步處理。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-138">The first time you enable the password synchronization feature, it performs an initial synchronization of the passwords of all in-scope users.</span></span> <span data-ttu-id="7a5ae-139">您無法明確定義一小組要同步處理的使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-139">You cannot explicitly define a subset of user passwords that you want to synchronize.</span></span>

<span data-ttu-id="7a5ae-140">當您變更內部部署密碼時，更新後的密碼將會進行同步處理，而這個動作大多會在幾分鐘內完成。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-140">When you change an on-premises password, the updated password is synchronized, most often in a matter of minutes.</span></span>
<span data-ttu-id="7a5ae-141">密碼同步處理功能會自動重試失敗的同步處理嘗試。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-141">The password synchronization feature automatically retries failed synchronization attempts.</span></span> <span data-ttu-id="7a5ae-142">若嘗試同步密碼期間發生錯誤，該錯誤會記錄在事件檢視器中。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-142">If an error occurs during an attempt to synchronize a password, an error is logged in your event viewer.</span></span>

<span data-ttu-id="7a5ae-143">密碼同步處理不會影響目前已登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-143">The synchronization of a password has no impact on the user  who is currently signed in.</span></span>
<span data-ttu-id="7a5ae-144">目前的雲端服務工作階段不會立即受到同步處理的密碼變更之影響，會在您登入雲端服務時才會受到影響。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-144">Your current cloud service session is not immediately affected by a synchronized password change that occurs while you are signed in to a cloud service.</span></span> <span data-ttu-id="7a5ae-145">不過，當雲端服務要求您重新驗證時，就需要提供新的密碼。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-145">However, when the cloud service requires you to authenticate again, you need to provide your new password.</span></span>

<span data-ttu-id="7a5ae-146">使用者必須輸入其公司認證第二次對 Azure AD 進行驗證，不論他們是否登入其公司網路。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-146">A user must enter their corporate credentials a second time to authenticate to Azure AD, regardless of whether they're signed in to their corporate network.</span></span> <span data-ttu-id="7a5ae-147">不過，如果使用者在登入時選取 [讓我保持登入 (KMSI)] 核取方塊，這些模式可以最小化。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-147">These pattern can be minimized, however, if the user selects the Keep me signed in (KMSI) check box at sign in.</span></span> <span data-ttu-id="7a5ae-148">此選取動作會設定工作階段 Cookie 在短期間內略過驗證。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-148">This selection sets a session cookie that bypasses authentication for a short period.</span></span> <span data-ttu-id="7a5ae-149">KMSI 行為可以由 Azure AD 系統管理員啟用或停用。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-149">KMSI behavior can be enabled or disabled by the Azure AD administrator.</span></span>

> [!NOTE]
> <span data-ttu-id="7a5ae-150">只有 Active Directory 的物件類型使用者才支援密碼同步。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-150">Password sync is only supported for the object type user in Active Directory.</span></span> <span data-ttu-id="7a5ae-151">不支援 iNetOrgPerson 物件類型。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-151">It is not supported for the iNetOrgPerson object type.</span></span>

### <a name="detailed-description-of-how-password-synchronization-works"></a><span data-ttu-id="7a5ae-152">密碼同步處理運作方式的詳細描述</span><span class="sxs-lookup"><span data-stu-id="7a5ae-152">Detailed description of how password synchronization works</span></span>
<span data-ttu-id="7a5ae-153">以下深入說明 Active Directory 與 Azure AD 之間的密碼同步處理運作方式。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-153">The following describes in-depth how password synchronization works between Active Directory and Azure AD.</span></span>

![詳細的密碼流程](./media/active-directory-aadconnectsync-implement-password-synchronization/arch3.png)


1. <span data-ttu-id="7a5ae-155">每隔兩分鐘，AD Connect 伺服器上的密碼同步處理代理程式會透過標準 [MS-DRSR](https://msdn.microsoft.com/library/cc228086.aspx) 複寫通訊協定，從 DC 要求儲存的密碼雜湊 (unicodePwd 屬性)，以同步處理 DC 之間的資料。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-155">Every two minutes, the password synchronization agent on the AD Connect server requests stored password hashes (the unicodePwd attribute) from a DC via the standard [MS-DRSR](https://msdn.microsoft.com/library/cc228086.aspx) replication protocol used to synchronize data between DCs.</span></span> <span data-ttu-id="7a5ae-156">服務帳戶必須具有複寫目錄變更和複寫目錄變更所有 AD 權限 (預設在安裝時授與)，以取得密碼雜湊。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-156">The service account must have Replicate Directory Changes and Replicate Directory Changes All AD permissions (granted by default on installation) to obtain the password hashes.</span></span>
2. <span data-ttu-id="7a5ae-157">在傳送之前，DC 會使用金鑰 (它是 RPC 工作階段金鑰和 salt 的 [MD5](http://www.rfc-editor.org/rfc/rfc1321.txt) 雜湊)，來加密 MD4 密碼雜湊。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-157">Before sending, the DC encrypts the MD4 password hash by using a key that is a [MD5](http://www.rfc-editor.org/rfc/rfc1321.txt) hash of the RPC session key and a salt.</span></span> <span data-ttu-id="7a5ae-158">然後它會透過 RPC 將結果傳送至密碼同步處理代理程式。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-158">It then sends the result to the password synchronization agent over RPC.</span></span> <span data-ttu-id="7a5ae-159">DC 也會使用 DC 複寫通訊協定將 salt 傳送至同步處理代理程式，讓代理程式可以解密信封。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-159">The DC also passes the salt to the synchronization agent by using the DC replication protocol, so the agent will be able to decrypt the envelope.</span></span>
3.  <span data-ttu-id="7a5ae-160">在密碼同步處理代理程式將信封加密後，它會使用 [MD5CryptoServiceProvider](https://msdn.microsoft.com/library/System.Security.Cryptography.MD5CryptoServiceProvider.aspx) 和 salt 來產生金鑰，以將接收的資料解密回其原始 MD4 格式。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-160">After the password synchronization agent has the encrypted envelope, it uses [MD5CryptoServiceProvider](https://msdn.microsoft.com/library/System.Security.Cryptography.MD5CryptoServiceProvider.aspx) and the salt to generate a key to decrypt the received data back to its original MD4 format.</span></span> <span data-ttu-id="7a5ae-161">密碼同步處理代理程式完全無法存取純文字密碼。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-161">At no point does the password synchronization agent have access to the clear text password.</span></span> <span data-ttu-id="7a5ae-162">密碼同步處理代理程式使用 MD5 純粹是為了與 DC 的複寫通訊協定相容性，並且只會在 DC 和密碼同步處理代理程式之間的內部部署上使用。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-162">The password synchronization agent’s use of MD5 is strictly for replication protocol compatibility with the DC, and it is only used on premises between the DC and the password synchronization agent.</span></span>
4.  <span data-ttu-id="7a5ae-163">密碼同步處理代理程式將 16 位元組二進位密碼雜湊擴展至 64 位元組的方法是首先將該雜湊轉換為 32 位元組十六進位字串，然後將此字串轉換回具有 UTF-16 編碼的二進位。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-163">The password synchronization agent expands the 16-byte binary password hash to 64 bytes by first converting the hash to a 32-byte hexadecimal string, then converting this string back into binary with UTF-16 encoding.</span></span>
5.  <span data-ttu-id="7a5ae-164">密碼同步處理代理程式會新增 salt，其中包含 10 位元組長度 salt，64 位元組二進位檔，以進一步保護原始雜湊。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-164">The password synchronization agent adds a salt, consisting of a 10-byte length salt, to the 64-byte binary to further protect the original hash.</span></span>
6.  <span data-ttu-id="7a5ae-165">然後密碼同步處理代理程式會結合 MD4 雜湊加上 salt，並且將它輸入 [PBKDF2](https://www.ietf.org/rfc/rfc2898.txt) 函式。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-165">The password synchronization agent then combines the MD4 hash plus salt, and inputs it into the [PBKDF2](https://www.ietf.org/rfc/rfc2898.txt) function.</span></span> <span data-ttu-id="7a5ae-166">系統會使用 [HMAC-SHA256](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) 索引雜湊演算法的 1000 次反覆運算。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-166">1000 iterations of the [HMAC-SHA256](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) keyed hashing algorithm is used.</span></span> 
7.  <span data-ttu-id="7a5ae-167">密碼同步處理代理程式會產生 32 位元組的雜湊，串連 salt 和 SHA256 反覆運算數 (以供 Azure AD 使用)，然後透過 SSL 將字串從 Azure AD Connect 傳輸至 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-167">The password synchronization agent takes the resulting 32-byte hash, concatenates both the salt and the number of SHA256 iterations to it (for use by Azure AD), then transmits the string from Azure AD Connect to Azure AD over SSL.</span></span></br> 
8.  <span data-ttu-id="7a5ae-168">當使用者嘗試登入 Azure AD 並且輸入其密碼時，密碼會執行相同的 MD4+salt+PBKDF2+HMAC-SHA256 程序。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-168">When a user attempts to sign in to Azure AD and enters their password, the password is run through the same MD4+salt+PBKDF2+HMAC-SHA256 process.</span></span> <span data-ttu-id="7a5ae-169">如果產生的雜湊符合 Azure AD 中儲存的雜湊，使用者輸入的密碼正確並且通過驗證。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-169">If the resulting hash matches the hash stored in Azure AD, the user has entered the correct password and is authenticated.</span></span> 

>[!Note] 
><span data-ttu-id="7a5ae-170">系統不會將原始的 MD4 雜湊傳輸至 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-170">The original MD4 hash is not transmitted to Azure AD.</span></span> <span data-ttu-id="7a5ae-171">而是會傳輸原始 MD4 雜湊的 SHA256 雜湊。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-171">Instead, the SHA256 hash of the original MD4 hash is transmitted.</span></span> <span data-ttu-id="7a5ae-172">如此一來，如果取得儲存在 Azure AD 的雜湊，它不能在內部部署傳遞雜湊攻擊中使用。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-172">As a result, if the hash stored in Azure AD is obtained, it cannot be used in an on-premises pass-the-hash attack.</span></span>

### <a name="how-password-synchronization-works-with-azure-active-directory-domain-services"></a><span data-ttu-id="7a5ae-173">密碼同步處理如何與 Azure Active Directory Domain Services 搭配運作</span><span class="sxs-lookup"><span data-stu-id="7a5ae-173">How password synchronization works with Azure Active Directory Domain Services</span></span>
<span data-ttu-id="7a5ae-174">您也可以使用密碼同步處理功能，將內部部署密碼同步處理到 [Azure Active Directory Domain Services](../../active-directory-domain-services/active-directory-ds-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-174">You can also use the password synchronization feature to synchronize your on-premises passwords to [Azure Active Directory Domain Services](../../active-directory-domain-services/active-directory-ds-overview.md).</span></span> <span data-ttu-id="7a5ae-175">在此案例中，Azure Active Directory Domain Services 執行個體會以內部部署 Active Directory 執行個體中所有可用的方法，來對您在雲端中的使用者進行驗證。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-175">In this scenario, the Azure Active Directory Domain Services instance authenticates your users in the cloud with all the methods available in your on-premises Active Directory instance.</span></span> <span data-ttu-id="7a5ae-176">此案例的體驗類似於在內部部署環境中使用 Active Directory 遷移工具 (ADMT)。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-176">The experience of this scenario is similar to using the Active Directory Migration Tool (ADMT) in an on-premises environment.</span></span>

### <a name="security-considerations"></a><span data-ttu-id="7a5ae-177">安全性考量</span><span class="sxs-lookup"><span data-stu-id="7a5ae-177">Security considerations</span></span>
<span data-ttu-id="7a5ae-178">同步密碼的時候，純文字版本的密碼不會向密碼同步處理功能、Azure AD 或任何相關服務公開。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-178">When synchronizing passwords, the plain-text version of your password is not exposed to the password synchronization feature, to Azure AD, or any of the associated services.</span></span>

<span data-ttu-id="7a5ae-179">使用者驗證是針對 Azure AD 進行，而不是針對組織自己的 Active Directory 執行個體進行。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-179">User authentication takes place against Azure AD rather than against the organization's own Active Directory instance.</span></span> <span data-ttu-id="7a5ae-180">如果您的組織對於離開內部部署之任何表單中的密碼資料有疑慮，請考量事實上儲存在 Azure AD 中的 SHA256 資料密碼 (原始 MD4 雜湊的雜湊) 比起儲存在 Active Directory 中的安全許多。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-180">If your organization has concerns about password data in any form leaving the premises, consider the fact that the SHA256 password data stored in Azure AD--a hash of the original MD4 hash--is significantly more secure than what is stored in Active Directory.</span></span> <span data-ttu-id="7a5ae-181">此外，因為此 SHA256 雜湊無法解密，所以無法帶回組織的 Active Directory 環境，並且在傳遞雜湊攻擊中顯示為有效的使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-181">Further, because this SHA256 hash cannot be decrypted, it cannot be brought back to the organization's Active Directory environment and presented as a valid user password in a pass-the-hash attack.</span></span>





### <a name="password-policy-considerations"></a><span data-ttu-id="7a5ae-182">密碼原則考量</span><span class="sxs-lookup"><span data-stu-id="7a5ae-182">Password policy considerations</span></span>
<span data-ttu-id="7a5ae-183">啟用密碼同步處理會影響兩種類型的密碼原則：</span><span class="sxs-lookup"><span data-stu-id="7a5ae-183">There are two types of password policies that are affected by enabling password synchronization:</span></span>

* <span data-ttu-id="7a5ae-184">密碼複雜性原則</span><span class="sxs-lookup"><span data-stu-id="7a5ae-184">Password complexity policy</span></span>
* <span data-ttu-id="7a5ae-185">密碼到期原則</span><span class="sxs-lookup"><span data-stu-id="7a5ae-185">Password expiration policy</span></span>

#### <a name="password-complexity-policy"></a><span data-ttu-id="7a5ae-186">密碼複雜性原則</span><span class="sxs-lookup"><span data-stu-id="7a5ae-186">Password complexity policy</span></span>  
<span data-ttu-id="7a5ae-187">當您啟用密碼同步處理時，在內部部署 Active Directory 執行個體中的密碼複雜性原則，會覆寫已同步處理的使用者在雲端中的複雜性原則。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-187">When password synchronization is enabled, the password complexity policies in your on-premises Active Directory instance override complexity policies in the cloud for synchronized users.</span></span> <span data-ttu-id="7a5ae-188">您可以使用內部部署 Active Directory 執行個體的所有有效密碼，來存取 Azure AD 服務。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-188">You can use all of the valid passwords from your on-premises Active Directory instance to access Azure AD services.</span></span>

> [!NOTE]
> <span data-ttu-id="7a5ae-189">直接在雲端建立的使用者的密碼仍受制於在雲端定義的密碼原則。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-189">Passwords for users that are created directly in the cloud are still subject to password policies as defined in the cloud.</span></span>

#### <a name="password-expiration-policy"></a><span data-ttu-id="7a5ae-190">密碼到期原則</span><span class="sxs-lookup"><span data-stu-id="7a5ae-190">Password expiration policy</span></span>  
<span data-ttu-id="7a5ae-191">如果使用者位於密碼同步處理範圍內，則雲端帳戶的密碼會設為「永不到期」。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-191">If a user is in the scope of password synchronization, the cloud account password is set to *Never Expire*.</span></span>

<span data-ttu-id="7a5ae-192">您可以使用內部部署環境中已過期的同步處理密碼，繼續登入雲端服務。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-192">You can continue to sign in to your cloud services by using a synchronized password that is expired in your on-premises environment.</span></span> <span data-ttu-id="7a5ae-193">您的雲端密碼會於下一次您在內部部署環境中變更密碼時更新。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-193">Your cloud password is updated the next time you change the password in the on-premises environment.</span></span>

#### <a name="account-expiration"></a><span data-ttu-id="7a5ae-194">帳戶到期</span><span class="sxs-lookup"><span data-stu-id="7a5ae-194">Account expiration</span></span>
<span data-ttu-id="7a5ae-195">如果您的組織使用 accountExpires 屬性作為使用者帳戶管理的一部分，請注意這個屬性不會同步處理至 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-195">If your organization uses the accountExpires attribute as part of user account management, be aware that this attribute is not synchronized to Azure AD.</span></span> <span data-ttu-id="7a5ae-196">如此一來，針對密碼同步處理設定之環境中到期的 Active Directory 帳戶在 Azure AD 仍然為作用中。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-196">As a result, an expired Active Directory account in an environment configured for password synchronization will still be active in Azure AD.</span></span> <span data-ttu-id="7a5ae-197">我們的建議是，如果帳戶已到期，工作流程動作就應該觸發 PowerShell 指令碼，以停用使用者的 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-197">We recommend that if the account is expired, a workflow action should trigger a PowerShell script that disables the user's Azure AD account.</span></span> <span data-ttu-id="7a5ae-198">相反地，當帳戶開啟時，Azure AD 執行個體也應開啟。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-198">Conversely, when the account is turned on, the Azure AD instance should be turned on.</span></span>

### <a name="overwrite-synchronized-passwords"></a><span data-ttu-id="7a5ae-199">覆寫已同步的密碼</span><span class="sxs-lookup"><span data-stu-id="7a5ae-199">Overwrite synchronized passwords</span></span>
<span data-ttu-id="7a5ae-200">系統管理員可以使用 Windows PowerShell 手動重設您的密碼。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-200">An administrator can manually reset your password by using Windows PowerShell.</span></span>

<span data-ttu-id="7a5ae-201">在此情況下，新的密碼會覆寫您已同步處理的密碼，且雲端中定義的所有密碼原則都會套用到新的密碼。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-201">In this case, the new password overrides your synchronized password, and all password policies defined in the cloud are applied to the new password.</span></span>

<span data-ttu-id="7a5ae-202">如果您再次變更內部部署密碼，則新密碼會同步到雲端並覆寫手動更新的密碼。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-202">If you change your on-premises password again, the new password is synchronized to the cloud, and it overrides the manually updated password.</span></span>

<span data-ttu-id="7a5ae-203">密碼同步處理不會影響已登入的 Azure 使用者。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-203">The synchronization of a password has no impact on the Azure user who is signed in.</span></span> <span data-ttu-id="7a5ae-204">目前的雲端服務工作階段不會立即受到同步處理的密碼變更之影響，會在您登入雲端服務時才會受到影響。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-204">Your current cloud service session is not immediately affected by a synchronized password change that occurs while you're signed in to a cloud service.</span></span> <span data-ttu-id="7a5ae-205">KMSI 會延伸此差異的持續時間。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-205">KMSI extends the duration of this difference.</span></span> <span data-ttu-id="7a5ae-206">當雲端服務要求您重新驗證時，就需要提供新的密碼。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-206">When the cloud service requires you to authenticate again, you need to provide your new password.</span></span>

### <a name="additional-advantages"></a><span data-ttu-id="7a5ae-207">其他優點</span><span class="sxs-lookup"><span data-stu-id="7a5ae-207">Additional advantages</span></span>

- <span data-ttu-id="7a5ae-208">一般而言，密碼同步處理比同盟服務更容易實作。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-208">Generally, password synchronization is simpler to implement than a federation service.</span></span> <span data-ttu-id="7a5ae-209">它不需要任何額外的伺服器，並且會排除高可用性同盟服務的相依性以驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-209">It doesn't require any additional servers, and eliminates dependence on a highly available federation service to authenticate users.</span></span> 
- <span data-ttu-id="7a5ae-210">除了同盟服務，您也可以啟用密碼同步處理服務。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-210">Password synchronization can also be enabled in addition to federation.</span></span> <span data-ttu-id="7a5ae-211">您可以將它作為同盟服務發生中斷時的後援服務。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-211">It may be used as a fallback if your federation service experiences an outage.</span></span>












## <a name="enable-password-synchronization"></a><span data-ttu-id="7a5ae-212">啟用密碼同步處理</span><span class="sxs-lookup"><span data-stu-id="7a5ae-212">Enable password synchronization</span></span>
<span data-ttu-id="7a5ae-213">當您使用 [快速設定] 選項來安裝 Azure AD Connect 時，系統會自動啟用密碼同步處理服務。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-213">When you install Azure AD Connect by using the **Express Settings** option, password synchronization is automatically enabled.</span></span> <span data-ttu-id="7a5ae-214">如需詳細資訊，請參閱[使用快速設定開始使用 Azure AD Connect](active-directory-aadconnect-get-started-express.md)。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-214">For more details, see [Getting started with Azure AD Connect using express settings](active-directory-aadconnect-get-started-express.md).</span></span>

<span data-ttu-id="7a5ae-215">如果您在安裝 Azure AD Connect 時使用自訂設定，則可以在使用者登入頁面上使用密碼同步處理服務。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-215">If you use custom settings when you install Azure AD Connect, password synchronization is available on the user sign-in page.</span></span> <span data-ttu-id="7a5ae-216">如需詳細資訊，請參閱[自訂 Azure AD Connect 安裝](active-directory-aadconnect-get-started-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-216">For more details, see [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

![啟用密碼同步處理](./media/active-directory-aadconnectsync-implement-password-synchronization/usersignin.png)

### <a name="password-synchronization-and-fips"></a><span data-ttu-id="7a5ae-218">密碼同步處理和 FIPS</span><span class="sxs-lookup"><span data-stu-id="7a5ae-218">Password synchronization and FIPS</span></span>
<span data-ttu-id="7a5ae-219">如果我們已經根據美國聯邦資訊處理標準 (FIPS) 鎖定您的伺服器，則 MD5 會停用。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-219">If your server has been locked down according to Federal Information Processing Standard (FIPS), then MD5 is disabled.</span></span>

<span data-ttu-id="7a5ae-220">**若要針對密碼同步處理啟用 MD5，請執行下列步驟︰**</span><span class="sxs-lookup"><span data-stu-id="7a5ae-220">**To enable MD5 for password synchronization, perform the following steps:**</span></span>

1. <span data-ttu-id="7a5ae-221">移至 %programfiles%\Azure AD Sync\Bin。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-221">Go to %programfiles%\Azure AD Sync\Bin.</span></span>
2. <span data-ttu-id="7a5ae-222">開啟 miiserver.exe.config。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-222">Open miiserver.exe.config.</span></span>
3. <span data-ttu-id="7a5ae-223">移至檔案結尾處的 configuration/runtime 節點。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-223">Go to the configuration/runtime node at the end of the file.</span></span>
4. <span data-ttu-id="7a5ae-224">新增下列節點︰ `<enforceFIPSPolicy enabled="false"/>`</span><span class="sxs-lookup"><span data-stu-id="7a5ae-224">Add the following node: `<enforceFIPSPolicy enabled="false"/>`</span></span>
5. <span data-ttu-id="7a5ae-225">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-225">Save your changes.</span></span>

<span data-ttu-id="7a5ae-226">如需參考，此程式碼片段就是其大致樣貌︰</span><span class="sxs-lookup"><span data-stu-id="7a5ae-226">For reference, this snippet is what it should look like:</span></span>

```
    <configuration>
        <runtime>
            <enforceFIPSPolicy enabled="false"/>
        </runtime>
    </configuration>
```

<span data-ttu-id="7a5ae-227">如需安全性和 FIPS 的詳細資訊，請參閱 [AAD 密碼同步、加密和 FIPS 合規性](https://blogs.technet.microsoft.com/enterprisemobility/2014/06/28/aad-password-sync-encryption-and-fips-compliance/)。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-227">For information about security and FIPS, see [AAD Password Sync, encryption and FIPS compliance](https://blogs.technet.microsoft.com/enterprisemobility/2014/06/28/aad-password-sync-encryption-and-fips-compliance/).</span></span>

## <a name="troubleshoot-password-synchronization"></a><span data-ttu-id="7a5ae-228">對密碼同步處理進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="7a5ae-228">Troubleshoot password synchronization</span></span>
<span data-ttu-id="7a5ae-229">如果您在進行密碼同步處理時發生問題，請參閱[針對密碼同步處理進行疑難排解](active-directory-aadconnectsync-troubleshoot-password-synchronization.md)。</span><span class="sxs-lookup"><span data-stu-id="7a5ae-229">If you have problems with password synchronization, see [Troubleshoot password synchronization](active-directory-aadconnectsync-troubleshoot-password-synchronization.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a5ae-230">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a5ae-230">Next steps</span></span>
* [<span data-ttu-id="7a5ae-231">Azure AD Connect 同步處理：自訂同步處理選項</span><span class="sxs-lookup"><span data-stu-id="7a5ae-231">Azure AD Connect sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="7a5ae-232">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a5ae-232">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
