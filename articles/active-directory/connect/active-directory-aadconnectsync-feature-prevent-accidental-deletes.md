---
title: "Azure AD Connect 同步：防止意外刪除 |Microsoft Docs"
description: "本主題描述 hello 防止被意外刪除 （防止意外刪除） 功能，在 Azure AD Connect。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b852cb4-2850-40a1-8280-8724081601f7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 159597f8354806fcaea1430e0ff84956338592a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-prevent-accidental-deletes"></a><span data-ttu-id="996d5-103">Azure AD Connect 同步處理：防止意外刪除</span><span class="sxs-lookup"><span data-stu-id="996d5-103">Azure AD Connect sync: Prevent accidental deletes</span></span>
<span data-ttu-id="996d5-104">本主題描述 hello 防止被意外刪除 （防止意外刪除） 功能，在 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="996d5-104">This topic describes hello prevent accidental deletes (preventing accidental deletions) feature in Azure AD Connect.</span></span>

<span data-ttu-id="996d5-105">時安裝 Azure AD Connect，防止被意外刪除預設會啟用並設定的 toonot 中允許超過 500 個刪除匯出。</span><span class="sxs-lookup"><span data-stu-id="996d5-105">When installing Azure AD Connect, prevent accidental deletes is enabled by default and configured toonot allow an export with more than 500 deletes.</span></span> <span data-ttu-id="996d5-106">這項功能是設計的 tooprotect 您從意外組態變更，並變更會影響許多使用者和其他物件的 tooyour 在內部部署目錄。</span><span class="sxs-lookup"><span data-stu-id="996d5-106">This feature is designed tooprotect you from accidental configuration changes and changes tooyour on-premises directory that would affect many users and other objects.</span></span>

## <a name="what-is-prevent-accidental-deletes"></a><span data-ttu-id="996d5-107">防止意外刪除是什麼</span><span class="sxs-lookup"><span data-stu-id="996d5-107">What is prevent accidental deletes</span></span>
<span data-ttu-id="996d5-108">會看到多項刪除的常見案例包括：</span><span class="sxs-lookup"><span data-stu-id="996d5-108">Common scenarios when you see many deletes include:</span></span>

* <span data-ttu-id="996d5-109">變更太[篩選](active-directory-aadconnectsync-configure-filtering.md)其中整個[OU](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering)或[網域](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering)會變成未選取。</span><span class="sxs-lookup"><span data-stu-id="996d5-109">Changes too[filtering](active-directory-aadconnectsync-configure-filtering.md) where an entire [OU](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) or [domain](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) is unselected.</span></span>
* <span data-ttu-id="996d5-110">OU 中的所有物件遭到刪除。</span><span class="sxs-lookup"><span data-stu-id="996d5-110">All objects in an OU are deleted.</span></span>
* <span data-ttu-id="996d5-111">OU 已重新命名，以便在它的所有物件都會都視為 toobe 同步處理的範圍。</span><span class="sxs-lookup"><span data-stu-id="996d5-111">An OU is renamed so all objects in it are considered toobe out of scope for synchronization.</span></span>

<span data-ttu-id="996d5-112">可以使用 PowerShell 變更 hello 預設值為 500 個物件使用`Enable-ADSyncExportDeletionThreshold`。</span><span class="sxs-lookup"><span data-stu-id="996d5-112">hello default value of 500 objects can be changed with PowerShell using `Enable-ADSyncExportDeletionThreshold`.</span></span> <span data-ttu-id="996d5-113">您應該設定組織的此值 toofit hello 大小。</span><span class="sxs-lookup"><span data-stu-id="996d5-113">You should configure this value toofit hello size of your organization.</span></span> <span data-ttu-id="996d5-114">因為 hello 同步處理排程器執行每隔 30 分鐘，hello 值會是 hello 30 分鐘內出現的刪除數目。</span><span class="sxs-lookup"><span data-stu-id="996d5-114">Since hello sync scheduler runs every 30 minutes, hello value is hello number of deletes seen within 30 minutes.</span></span>

<span data-ttu-id="996d5-115">如果有太多的接移刪除 toobe 會匯出 tooAzure AD，則 hello 匯出會停止，您會收到一封電子郵件，像這樣：</span><span class="sxs-lookup"><span data-stu-id="996d5-115">If there are too many deletes staged toobe exported tooAzure AD, then hello export stops and you receive an email like this:</span></span>

![防止意外刪除電子郵件](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/email.png)

> <span data-ttu-id="996d5-117">*Hello (技術連絡人)。（時間） 在 hello 身分識別同步處理服務偵測到刪除的 hello 數目超過 hello 刪除設定的臨界值 （組織名稱）。本次執行身分識別同步處理時，共傳送 (數目) 個物件進行刪除。這在達到或超過設定的 hello 刪除臨界值 （數字） 物件。我們需要您 tooprovide 確認刪除動作應該是之前，我們將繼續處理。請 hello 防止意外刪除，如需此電子郵件訊息中所列的 hello 錯誤詳細資訊，參閱。*</span><span class="sxs-lookup"><span data-stu-id="996d5-117">*Hello (technical contact). At (time) hello Identity synchronization service detected that hello number of deletions exceeded hello configured deletion threshold for (organization name). A total of (number) objects were sent for deletion in this Identity synchronization run. This met or exceeded hello configured deletion threshold value of (number) objects. We need you tooprovide confirmation that these deletions should be processed before we will proceed. Please see hello preventing accidental deletions for more information about hello error listed in this email message.*</span></span>
>
> 

<span data-ttu-id="996d5-118">您也可以查看 hello 狀態`stopped-deletion-threshold-exceeded`當您查看 hello**同步處理服務管理員**hello 匯出設定檔的 UI。</span><span class="sxs-lookup"><span data-stu-id="996d5-118">You can also see hello status `stopped-deletion-threshold-exceeded` when you look in hello **Synchronization Service Manager** UI for hello Export profile.</span></span>
<span data-ttu-id="996d5-119">![防止意外刪除 Sync Service Manager UI](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)</span><span class="sxs-lookup"><span data-stu-id="996d5-119">![Prevent Accidental deletes Sync Service Manager UI](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)</span></span>

<span data-ttu-id="996d5-120">如果這是非預期的結果，請進行調查，並採取修正動作。</span><span class="sxs-lookup"><span data-stu-id="996d5-120">If this was unexpected, then investigate and take corrective actions.</span></span> <span data-ttu-id="996d5-121">toosee 哪些物件是關於 toobe 刪除，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="996d5-121">toosee which objects are about toobe deleted, do hello following:</span></span>

1. <span data-ttu-id="996d5-122">啟動**同步處理服務**從 hello 開始] 功能表。</span><span class="sxs-lookup"><span data-stu-id="996d5-122">Start **Synchronization Service** from hello Start Menu.</span></span>
2. <span data-ttu-id="996d5-123">跳過**連接器**。</span><span class="sxs-lookup"><span data-stu-id="996d5-123">Go too**Connectors**.</span></span>
3. <span data-ttu-id="996d5-124">選取 hello 連接器類型**Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="996d5-124">Select hello Connector with type **Azure Active Directory**.</span></span>
4. <span data-ttu-id="996d5-125">在下**動作**toohello 的權限，選取**搜尋連接器空間**。</span><span class="sxs-lookup"><span data-stu-id="996d5-125">Under **Actions** toohello right, select **Search Connector Space**.</span></span>
5. <span data-ttu-id="996d5-126">在 hello 下快顯**範圍**，選取**中斷連線後**hello 過去中挑選一次。</span><span class="sxs-lookup"><span data-stu-id="996d5-126">In hello pop-up under **Scope**, select **Disconnected Since** and pick a time in hello past.</span></span> <span data-ttu-id="996d5-127">按一下 [搜尋] 。</span><span class="sxs-lookup"><span data-stu-id="996d5-127">Click **Search**.</span></span> <span data-ttu-id="996d5-128">此頁面提供有關 toobe 刪除所有物件的檢視。</span><span class="sxs-lookup"><span data-stu-id="996d5-128">This page provides a view of all objects about toobe deleted.</span></span> <span data-ttu-id="996d5-129">按一下每個項目，您可以取得 hello 物件的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="996d5-129">By clicking each item, you can get additional information about hello object.</span></span> <span data-ttu-id="996d5-130">您也可以按一下**資料行設定**tooadd 其他屬性 toobe 在 hello 方格中顯示。</span><span class="sxs-lookup"><span data-stu-id="996d5-130">You can also click **Column Setting** tooadd additional attributes toobe visible in hello grid.</span></span>

![搜尋連接器空間](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/searchcs.png)

<span data-ttu-id="996d5-132">如果需要針對所有 hello 刪除，然後 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="996d5-132">If all hello deletes are desired, then do hello following:</span></span>

1. <span data-ttu-id="996d5-133">tooretrieve hello 目前刪除閾值，執行 hello PowerShell cmdlet `Get-ADSyncExportDeletionThreshold`。</span><span class="sxs-lookup"><span data-stu-id="996d5-133">tooretrieve hello current deletion threshold, run hello PowerShell cmdlet `Get-ADSyncExportDeletionThreshold`.</span></span> <span data-ttu-id="996d5-134">提供 Azure AD 全域系統管理員帳戶與密碼。</span><span class="sxs-lookup"><span data-stu-id="996d5-134">Provide an Azure AD Global Administrator account and password.</span></span> <span data-ttu-id="996d5-135">hello 預設值為 500。</span><span class="sxs-lookup"><span data-stu-id="996d5-135">hello default value is 500.</span></span>
2. <span data-ttu-id="996d5-136">tootemporarily 停用此保護，並讓這些刪除瀏覽，請執行 hello PowerShell cmdlet: `Disable-ADSyncExportDeletionThreshold`。</span><span class="sxs-lookup"><span data-stu-id="996d5-136">tootemporarily disable this protection and let those deletes go through, run hello PowerShell cmdlet: `Disable-ADSyncExportDeletionThreshold`.</span></span> <span data-ttu-id="996d5-137">提供 Azure AD 全域系統管理員帳戶與密碼。</span><span class="sxs-lookup"><span data-stu-id="996d5-137">Provide an Azure AD Global Administrator account and password.</span></span>
   <span data-ttu-id="996d5-138">![認證](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)</span><span class="sxs-lookup"><span data-stu-id="996d5-138">![Credentials](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)</span></span>
3. <span data-ttu-id="996d5-139">以 hello Azure 仍然選取 Active Directory 連接器，選取 [hello 動作**執行**選取**匯出**。</span><span class="sxs-lookup"><span data-stu-id="996d5-139">With hello Azure Active Directory Connector still selected, select hello action **Run** and select **Export**.</span></span>
4. <span data-ttu-id="996d5-140">toore 啟用 hello 保護執行 hello PowerShell cmdlet: `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`。</span><span class="sxs-lookup"><span data-stu-id="996d5-140">toore-enable hello protection, run hello PowerShell cmdlet: `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`.</span></span> <span data-ttu-id="996d5-141">取代您注意到擷取 hello 目前刪除閾值時的 hello 值為 500。</span><span class="sxs-lookup"><span data-stu-id="996d5-141">Replace 500 with hello value you noticed when retrieving hello current deletion threshold.</span></span> <span data-ttu-id="996d5-142">提供 Azure AD 全域系統管理員帳戶與密碼。</span><span class="sxs-lookup"><span data-stu-id="996d5-142">Provide an Azure AD Global Administrator account and password.</span></span>

## <a name="next-steps"></a><span data-ttu-id="996d5-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="996d5-143">Next steps</span></span>
<span data-ttu-id="996d5-144">**概觀主題**</span><span class="sxs-lookup"><span data-stu-id="996d5-144">**Overview topics**</span></span>

* [<span data-ttu-id="996d5-145">Azure AD Connect 同步處理：了解及自訂同步處理</span><span class="sxs-lookup"><span data-stu-id="996d5-145">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="996d5-146">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="996d5-146">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
