---
title: "Azure AD Connect 同步服務功能與組態 | Microsoft Docs"
description: "描述 Azure AD Connect 同步處理服務的服務端功能。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: c2873510c280a2683c235cfdce3d2617c3b665cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="750c3-103">Azure AD Connect 同步處理服務功能</span><span class="sxs-lookup"><span data-stu-id="750c3-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="750c3-104">Azure AD connect 同步處理功能有兩個元件：</span><span class="sxs-lookup"><span data-stu-id="750c3-104">The synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="750c3-105">名為 **Azure AD Connect 同步處理**的內部部署元件，也稱為**同步處理引擎**。</span><span class="sxs-lookup"><span data-stu-id="750c3-105">The on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="750c3-106">位於 Azure AD 的服務，也稱為 **Azure AD Connect 同步處理服務**</span><span class="sxs-lookup"><span data-stu-id="750c3-106">The service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="750c3-107">本主題說明 **Azure AD Connect 同步處理服務** 的下列功能如何運作，以及如何使用 Windows PowerShell 進行設定。</span><span class="sxs-lookup"><span data-stu-id="750c3-107">This topic explains how the following features of the **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="750c3-108">這些設定是由 [適用於 Windows PowerShell 的 Azure Active Directory 模組](http://aka.ms/aadposh)所設定。</span><span class="sxs-lookup"><span data-stu-id="750c3-108">These settings are configured by the [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="750c3-109">從 Azure AD Connect 個別進行下載和安裝。</span><span class="sxs-lookup"><span data-stu-id="750c3-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="750c3-110">本主題說明的 Cmdlet 已導入 [2016 年 3 月版本 (組建 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1)。</span><span class="sxs-lookup"><span data-stu-id="750c3-110">The cmdlets documented in this topic were introduced in the [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="750c3-111">如果您沒有本主題說明的 Cmdlet，或它們未產生相同的結果，請確認您執行的是最新版本。</span><span class="sxs-lookup"><span data-stu-id="750c3-111">If you do not have the cmdlets documented in this topic or they do not produce the same result, then make sure you run the latest version.</span></span>

<span data-ttu-id="750c3-112">若要查看 Azure AD 目錄中的組態，請執行 `Get-MsolDirSyncFeatures`。</span><span class="sxs-lookup"><span data-stu-id="750c3-112">To see the configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="750c3-113">![Get-MsolDirSyncFeatures 結果](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="750c3-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="750c3-114">其中許多設定只能由 Azure AD Connect 進行變更。</span><span class="sxs-lookup"><span data-stu-id="750c3-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="750c3-115">以下是可在 `Set-MsolDirSyncFeature`中配置的設定：</span><span class="sxs-lookup"><span data-stu-id="750c3-115">The following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="750c3-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="750c3-116">DirSyncFeature</span></span> | <span data-ttu-id="750c3-117">註解</span><span class="sxs-lookup"><span data-stu-id="750c3-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="750c3-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="750c3-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="750c3-119">不只主要 SMTP 位址，還允許物件聯結 userPrincipalName。</span><span class="sxs-lookup"><span data-stu-id="750c3-119">Allows objects to join on userPrincipalName in addition to primary SMTP address.</span></span> |
| [<span data-ttu-id="750c3-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="750c3-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="750c3-121">可讓同步處理引擎更新受管理/授權 (非同盟) 使用者的 userPrincipalName 屬性。</span><span class="sxs-lookup"><span data-stu-id="750c3-121">Allows the sync engine to update the userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="750c3-122">啟用功能後，即無法將其停用。</span><span class="sxs-lookup"><span data-stu-id="750c3-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="750c3-123">從 2016 年 8 月 24 日起，預設會對新的 Azure AD 目錄啟用*重複屬性恢復*功能。</span><span class="sxs-lookup"><span data-stu-id="750c3-123">From August 24, 2016 the feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="750c3-124">這項功能也會在此日期前建立的目錄上推出和啟用。</span><span class="sxs-lookup"><span data-stu-id="750c3-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="750c3-125">當您的目錄即將啟用此功能時，您會收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="750c3-125">You will receive an email notification when your directory is about to get this feature enabled.</span></span>
> 
> 

<span data-ttu-id="750c3-126">下列設定是由 Azure AD Connect 所設定，而且無法由 `Set-MsolDirSyncFeature`修改：</span><span class="sxs-lookup"><span data-stu-id="750c3-126">The following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="750c3-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="750c3-127">DirSyncFeature</span></span> | <span data-ttu-id="750c3-128">註解</span><span class="sxs-lookup"><span data-stu-id="750c3-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="750c3-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="750c3-129">DeviceWriteback</span></span> |[<span data-ttu-id="750c3-130">Azure AD Connect：啟用裝置回寫</span><span class="sxs-lookup"><span data-stu-id="750c3-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="750c3-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="750c3-131">DirectoryExtensions</span></span> |[<span data-ttu-id="750c3-132">Azure AD Connect 同步處理：目錄擴充</span><span class="sxs-lookup"><span data-stu-id="750c3-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="750c3-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="750c3-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="750c3-134">如果屬性是另一個物件的複本，即會將該屬性隔離，而不會在匯出期間導致整個物件失敗。</span><span class="sxs-lookup"><span data-stu-id="750c3-134">Allows an attribute to be quarantined when it is a duplicate of another object rather than failing the entire object during export.</span></span> |
| <span data-ttu-id="750c3-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="750c3-135">PasswordSync</span></span> |[<span data-ttu-id="750c3-136">使用 Azure AD Connect 同步處理實作密碼同步處理</span><span class="sxs-lookup"><span data-stu-id="750c3-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="750c3-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="750c3-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="750c3-138">預覽：群組回寫</span><span class="sxs-lookup"><span data-stu-id="750c3-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="750c3-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="750c3-139">UserWriteback</span></span> |<span data-ttu-id="750c3-140">目前不支援。</span><span class="sxs-lookup"><span data-stu-id="750c3-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="750c3-141">重複屬性恢復功能</span><span class="sxs-lookup"><span data-stu-id="750c3-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="750c3-142">含重複 UPNs / proxyAddresses 的物件，會將該屬性「隔離」，並指派暫時的值，而不會讓佈建物件失敗。</span><span class="sxs-lookup"><span data-stu-id="750c3-142">Instead of failing to provision objects with duplicate UPNs / proxyAddresses, the duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="750c3-143">解決衝突時，會自動將暫時 UPN 變更為適當的值。</span><span class="sxs-lookup"><span data-stu-id="750c3-143">When the conflict is resolved, the temporary UPN is changed to the proper value automatically.</span></span> <span data-ttu-id="750c3-144">如需詳細資訊，請參閱 [身分識別同步處理和重複屬性恢復功能](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)。</span><span class="sxs-lookup"><span data-stu-id="750c3-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="750c3-145">UserPrincipalName 大致比對</span><span class="sxs-lookup"><span data-stu-id="750c3-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="750c3-146">啟用這項功能後，除了一律啟用的 [主要 SMTP 位址](https://support.microsoft.com/kb/2641663)以外，還會對 UPN 套用大致比對。</span><span class="sxs-lookup"><span data-stu-id="750c3-146">When this feature is enabled, soft-match is enabled for UPN in addition to the [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="750c3-147">大致比對功能是用來針對 Azure AD 中現有的雲端使用者與內部部署使用者進行比對。</span><span class="sxs-lookup"><span data-stu-id="750c3-147">Soft-match is used to match existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="750c3-148">如果您需要比對內部部署 AD 帳戶與雲端中建立的現有帳戶，卻不能使用 Exchange Online 時，啟用此功能很有用。</span><span class="sxs-lookup"><span data-stu-id="750c3-148">If you need to match on-premises AD accounts with existing accounts created in the cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="750c3-149">在此案例中，您通常不需要在雲端中設定 SMTP 屬性。</span><span class="sxs-lookup"><span data-stu-id="750c3-149">In this scenario, you generally don’t have a reason to set the SMTP attribute in the cloud.</span></span>

<span data-ttu-id="750c3-150">在新建立的 Azure AD 目錄中，預設會開啟這項功能。</span><span class="sxs-lookup"><span data-stu-id="750c3-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="750c3-151">您可以執行下列項目，查看是否已啟用此功能︰</span><span class="sxs-lookup"><span data-stu-id="750c3-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="750c3-152">如果您的 Azure AD 目錄未啟用這項功能，您可以執行下列項目加以啟用︰</span><span class="sxs-lookup"><span data-stu-id="750c3-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="750c3-153">同步處理 userPrincipalName 更新</span><span class="sxs-lookup"><span data-stu-id="750c3-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="750c3-154">在過去，除非下列兩項條件都成立，否則皆會將透過內部部署使用同步處理服務的 UserPrincipalName 屬性更新封鎖：</span><span class="sxs-lookup"><span data-stu-id="750c3-154">Historically, updates to the UserPrincipalName attribute using the sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="750c3-155">使用者受到管理 (非同盟)。</span><span class="sxs-lookup"><span data-stu-id="750c3-155">The user is managed (non-federated).</span></span>
* <span data-ttu-id="750c3-156">使用者尚未指派授權。</span><span class="sxs-lookup"><span data-stu-id="750c3-156">The user has not been assigned a license.</span></span>

<span data-ttu-id="750c3-157">如需詳細資訊，請參閱 [Office 365、Azure 或 Intune 中的使用者名稱不符合內部部署的 UPN 或替代登入識別碼](https://support.microsoft.com/kb/2523192)。</span><span class="sxs-lookup"><span data-stu-id="750c3-157">For more details, see [User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="750c3-158">當內部部署中的 userPrincipalName 有所變更，且您使用密碼同步處理時，啟用此功能可讓同步處理引擎更新 userPrincipalName。</span><span class="sxs-lookup"><span data-stu-id="750c3-158">Enabling this feature allows the sync engine to update the userPrincipalName when it is changed on-premises and you use password sync.</span></span> <span data-ttu-id="750c3-159">如果您使用同盟，則不支援這項功能。</span><span class="sxs-lookup"><span data-stu-id="750c3-159">If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="750c3-160">在新建立的 Azure AD 目錄中，預設會開啟這項功能。</span><span class="sxs-lookup"><span data-stu-id="750c3-160">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="750c3-161">您可以執行下列項目，查看是否已啟用此功能︰</span><span class="sxs-lookup"><span data-stu-id="750c3-161">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="750c3-162">如果您的 Azure AD 目錄未啟用這項功能，您可以執行下列項目加以啟用︰</span><span class="sxs-lookup"><span data-stu-id="750c3-162">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="750c3-163">啟用這項功能之後，現有的 userPrincipalName 值會保持不變。</span><span class="sxs-lookup"><span data-stu-id="750c3-163">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="750c3-164">下次 userPrincipalName 屬性的內部部署變更時，使用者的一般差異同步處理即會更新 UPN。</span><span class="sxs-lookup"><span data-stu-id="750c3-164">On next change of the userPrincipalName attribute on-premises, the normal delta sync on users will update the UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="750c3-165">另請參閱</span><span class="sxs-lookup"><span data-stu-id="750c3-165">See also</span></span>
* [<span data-ttu-id="750c3-166">Azure AD Connect 同步處理</span><span class="sxs-lookup"><span data-stu-id="750c3-166">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="750c3-167">[整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="750c3-167">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

