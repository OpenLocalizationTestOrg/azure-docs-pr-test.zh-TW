---
title: "Azure AD Connect︰從 DirSync 升級 | Microsoft Docs"
description: "深入了解如何從 DirSync tooAzure AD tooupgrade 連接。 此文章描述 hello 步驟從 DirSync tooAzure 升級 AD Connect。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: baf52da7-76a8-44c9-8e72-33245790001c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 05572af410698deaa1392c8837bfcb749efc69e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-dirsync"></a><span data-ttu-id="aba45-104">Azure AD Connect︰從 DirSync 升級</span><span class="sxs-lookup"><span data-stu-id="aba45-104">Azure AD Connect: Upgrade from DirSync</span></span>
<span data-ttu-id="aba45-105">Azure AD Connect 是 hello 後續 tooDirSync。</span><span class="sxs-lookup"><span data-stu-id="aba45-105">Azure AD Connect is hello successor tooDirSync.</span></span> <span data-ttu-id="aba45-106">您找出您可以升級從 DirSync，本主題中的 hello 方式。</span><span class="sxs-lookup"><span data-stu-id="aba45-106">You find hello ways you can upgrade from DirSync in this topic.</span></span> <span data-ttu-id="aba45-107">這些步驟不適用於從另一個版本的 Azure AD Connect 或從 Azure AD Sync 升級。</span><span class="sxs-lookup"><span data-stu-id="aba45-107">These steps do not work for upgrading from another release of Azure AD Connect or from Azure AD Sync.</span></span>

<span data-ttu-id="aba45-108">您開始安裝 Azure AD Connect，請確定太[下載 Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)和中的步驟完成 hello 必要條件[Azure AD Connect： 硬體和必要條件](active-directory-aadconnect-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="aba45-108">Before you start installing Azure AD Connect, make sure too[download Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) and complete hello pre-requisite steps in [Azure AD Connect: Hardware and prerequisites](active-directory-aadconnect-prerequisites.md).</span></span> <span data-ttu-id="aba45-109">特別的是，您想 tooread 有關 hello 下列項目，因為這些區域是從 DirSync 不同：</span><span class="sxs-lookup"><span data-stu-id="aba45-109">In particular, you want tooread about hello following, since these areas are different from DirSync:</span></span>

* <span data-ttu-id="aba45-110">hello 的.Net 和 PowerShell 的必要的版本。</span><span class="sxs-lookup"><span data-stu-id="aba45-110">hello required version of .Net and PowerShell.</span></span> <span data-ttu-id="aba45-111">較新版本時需要的 toobe hello 比 DirSync 所需的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="aba45-111">Newer versions are required toobe on hello server than what DirSync needed.</span></span>
* <span data-ttu-id="aba45-112">hello proxy 伺服器設定。</span><span class="sxs-lookup"><span data-stu-id="aba45-112">hello proxy server configuration.</span></span> <span data-ttu-id="aba45-113">如果您使用 proxy 伺服器 tooreach hello 網際網路，則必須設定此設定，然後再升級。</span><span class="sxs-lookup"><span data-stu-id="aba45-113">If you use a proxy server tooreach hello internet, this setting must be configured before you upgrade.</span></span> <span data-ttu-id="aba45-114">DirSync，一律使用 hello proxy 伺服器設定為 hello 使用者安裝，但 Azure AD Connect 使用電腦的設定改為。</span><span class="sxs-lookup"><span data-stu-id="aba45-114">DirSync always used hello proxy server configured for hello user installing it, but Azure AD Connect uses machine settings instead.</span></span>
* <span data-ttu-id="aba45-115">hello Url 需要的 toobe 開啟 hello proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="aba45-115">hello URLs required toobe open in hello proxy server.</span></span> <span data-ttu-id="aba45-116">基本案例中，目錄同步，也支援這些案例 hello 需求是 hello 相同的。</span><span class="sxs-lookup"><span data-stu-id="aba45-116">For basic scenarios, those scenarios also supported by DirSync, hello requirements are hello same.</span></span> <span data-ttu-id="aba45-117">如果您想要 toouse 任何 hello Azure AD Connect 所隨附的新功能，就必須開啟某些新的 Url。</span><span class="sxs-lookup"><span data-stu-id="aba45-117">If you want toouse any of hello new features included with Azure AD Connect, some new URLs must be opened.</span></span>

> [!NOTE]
> <span data-ttu-id="aba45-118">一旦您啟用了您新 Azure AD Connect 伺服器 toostart 同步處理變更 tooAzure AD，您必須復原 toousing DirSync 或 Azure AD Sync。從 Azure AD Connect toolegacy 用戶端，包括 DirSync 和 Azure AD Sync 降級不支援，而且可能會在 Azure AD 中的 tooissues，例如資料遺失。</span><span class="sxs-lookup"><span data-stu-id="aba45-118">Once you have enabled your new Azure AD Connect server toostart synchronizing changes tooAzure AD, you must not roll back toousing DirSync or Azure AD Sync. Downgrading from Azure AD Connect toolegacy clients including DirSync and Azure AD Sync is not supported and can lead tooissues such as data loss in Azure AD.</span></span>

<span data-ttu-id="aba45-119">如果您不是要從 DirSync 升級，請參閱 [相關文件](#related-documentation) 中的其他案例。</span><span class="sxs-lookup"><span data-stu-id="aba45-119">If you are not upgrading from DirSync, see [related documentation](#related-documentation) for other scenarios.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="aba45-120">從 DirSync 升級</span><span class="sxs-lookup"><span data-stu-id="aba45-120">Upgrade from DirSync</span></span>
<span data-ttu-id="aba45-121">根據您目前的目錄同步部署，有不同的 hello 升級選項。</span><span class="sxs-lookup"><span data-stu-id="aba45-121">Depending on your current DirSync deployment, there are different options for hello upgrade.</span></span> <span data-ttu-id="aba45-122">如果 hello 預期升級時是不超過 3 個小時，然後 hello 建議 toodo 就地升級。</span><span class="sxs-lookup"><span data-stu-id="aba45-122">If hello expected upgrade time is less than three hours, then hello recommendation is toodo an in-place upgrade.</span></span> <span data-ttu-id="aba45-123">如果 hello 預期升級的時間會超過三個小時，然後 hello 建議 toodo 平行部署在另一部伺服器上。</span><span class="sxs-lookup"><span data-stu-id="aba45-123">If hello expected upgrade time is more than three hours, then hello recommendation is toodo a parallel deployment on another server.</span></span> <span data-ttu-id="aba45-124">預估，如果您有超過 50,000 個物件需要花費超過三個小時 toodo hello 升級。</span><span class="sxs-lookup"><span data-stu-id="aba45-124">It is estimated that if you have more than 50,000 objects it takes more than three hours toodo hello upgrade.</span></span>

| <span data-ttu-id="aba45-125">案例</span><span class="sxs-lookup"><span data-stu-id="aba45-125">Scenario</span></span> |
| --- | --- |
| [<span data-ttu-id="aba45-126">就地升級</span><span class="sxs-lookup"><span data-stu-id="aba45-126">In-place upgrade</span></span>](#in-place-upgrade) |
| [<span data-ttu-id="aba45-127">平行部署</span><span class="sxs-lookup"><span data-stu-id="aba45-127">Parallel deployment</span></span>](#parallel-deployment) |

> [!NOTE]
> <span data-ttu-id="aba45-128">當您計劃 tooupgrade DirSync tooAzure AD 從連接中，不會解除安裝 DirSync 自行 hello 升級前。</span><span class="sxs-lookup"><span data-stu-id="aba45-128">When you plan tooupgrade from DirSync tooAzure AD Connect, do not uninstall DirSync yourself before hello upgrade.</span></span> <span data-ttu-id="aba45-129">Azure AD Connect 會讀取和從 DirSync 移轉 hello 組態，以及在檢查 hello 伺服器之後解除安裝。</span><span class="sxs-lookup"><span data-stu-id="aba45-129">Azure AD Connect will read and migrate hello configuration from DirSync and uninstall after inspecting hello server.</span></span>

<span data-ttu-id="aba45-130">**就地升級**</span><span class="sxs-lookup"><span data-stu-id="aba45-130">**In-place upgrade**</span></span>  
<span data-ttu-id="aba45-131">hello 預期時間 toocomplete hello 升級由 hello 精靈顯示。</span><span class="sxs-lookup"><span data-stu-id="aba45-131">hello expected time toocomplete hello upgrade is displayed by hello wizard.</span></span> <span data-ttu-id="aba45-132">此預估值根據 hello 假設，需要花費三小時 toocomplete 具有 50,000 個物件 （使用者、 連絡人和群組） 的資料庫升級。</span><span class="sxs-lookup"><span data-stu-id="aba45-132">This estimate is based on hello assumption that it takes three hours toocomplete an upgrade for a database with 50,000 objects (users, contacts, and groups).</span></span> <span data-ttu-id="aba45-133">如果您的資料庫中物件的 hello 數目少於 50,000 個，Azure AD Connect 建議就地升級。</span><span class="sxs-lookup"><span data-stu-id="aba45-133">If hello number of objects in your database is less than 50,000, then Azure AD Connect recommends an in-place upgrade.</span></span> <span data-ttu-id="aba45-134">如果您決定 toocontinue，在升級期間，會自動套用您目前的設定，您的伺服器會自動繼續進行作用中的同步處理。</span><span class="sxs-lookup"><span data-stu-id="aba45-134">If you decide toocontinue, your current settings are automatically applied during upgrade and your server automatically resumes active synchronization.</span></span>

<span data-ttu-id="aba45-135">如果您想 toodo 設定移轉，且執行平行部署，然後您可以覆寫 hello 就地升級的建議。</span><span class="sxs-lookup"><span data-stu-id="aba45-135">If you want toodo a configuration migration and do a parallel deployment, then you can override hello in-place upgrade recommendation.</span></span> <span data-ttu-id="aba45-136">您可能例如 hello 機會 toorefresh hello 硬體和作業系統。</span><span class="sxs-lookup"><span data-stu-id="aba45-136">You might for example take hello opportunity toorefresh hello hardware and operating system.</span></span> <span data-ttu-id="aba45-137">如需詳細資訊，請參閱 hello[平行部署](#parallel-deployment)> 一節。</span><span class="sxs-lookup"><span data-stu-id="aba45-137">For more information, see hello [parallel deployment](#parallel-deployment) section.</span></span>

<span data-ttu-id="aba45-138">**平行部署**</span><span class="sxs-lookup"><span data-stu-id="aba45-138">**Parallel deployment**</span></span>  
<span data-ttu-id="aba45-139">如果您有超過 5 萬個物件，則建議使用平行部署。</span><span class="sxs-lookup"><span data-stu-id="aba45-139">If you have more than 50,000 objects, then a parallel deployment is recommended.</span></span> <span data-ttu-id="aba45-140">此部署可避免您的使用者經歷任何作業延遲。</span><span class="sxs-lookup"><span data-stu-id="aba45-140">This deployment avoids any operational delays experienced by your users.</span></span> <span data-ttu-id="aba45-141">hello Azure AD Connect 的安裝嘗試 hello 升級 tooestimate hello 停機時間，但如果您已在過去的 hello 升級目錄同步，您自己的經驗會可能 toobe hello 最佳指南。</span><span class="sxs-lookup"><span data-stu-id="aba45-141">hello Azure AD Connect installation attempts tooestimate hello downtime for hello upgrade, but if you've upgraded DirSync in hello past, your own experience is likely toobe hello best guide.</span></span>

### <a name="supported-dirsync-configurations-toobe-upgraded"></a><span data-ttu-id="aba45-142">支援的 DirSync 組態 toobe 升級</span><span class="sxs-lookup"><span data-stu-id="aba45-142">Supported DirSync configurations toobe upgraded</span></span>
<span data-ttu-id="aba45-143">升級目錄同步支援 hello 下列組態變更：</span><span class="sxs-lookup"><span data-stu-id="aba45-143">hello following configuration changes are supported with upgraded DirSync:</span></span>

* <span data-ttu-id="aba45-144">網域和 OU 篩選</span><span class="sxs-lookup"><span data-stu-id="aba45-144">Domain and OU filtering</span></span>
* <span data-ttu-id="aba45-145">替代 ID (UPN)</span><span class="sxs-lookup"><span data-stu-id="aba45-145">Alternate ID (UPN)</span></span>
* <span data-ttu-id="aba45-146">密碼同步和 Exchange 混合式設定</span><span class="sxs-lookup"><span data-stu-id="aba45-146">Password sync and Exchange hybrid settings</span></span>
* <span data-ttu-id="aba45-147">您的樹系/網域與 Azure AD 設定</span><span class="sxs-lookup"><span data-stu-id="aba45-147">Your forest/domain and Azure AD settings</span></span>
* <span data-ttu-id="aba45-148">根據使用者屬性進行篩選</span><span class="sxs-lookup"><span data-stu-id="aba45-148">Filtering based on user attributes</span></span>

<span data-ttu-id="aba45-149">無法升級 hello 變更之後。</span><span class="sxs-lookup"><span data-stu-id="aba45-149">hello following change cannot be upgraded.</span></span> <span data-ttu-id="aba45-150">如果您有此設定，將會封鎖 hello 升級：</span><span class="sxs-lookup"><span data-stu-id="aba45-150">If you have this configuration, hello upgrade is blocked:</span></span>

* <span data-ttu-id="aba45-151">不支援的 DirSync 變更，例如移除屬性和使用自訂延伸模組 DLL</span><span class="sxs-lookup"><span data-stu-id="aba45-151">Unsupported DirSync changes, for example removed attributes and using a custom extension DLL</span></span>

![已封鎖升級](./media/active-directory-aadconnect-dirsync-upgrade-get-started/analysisblocked.png)

<span data-ttu-id="aba45-153">在這些情況下，hello 建議 tooinstall 中新的 Azure AD Connect 伺服器[預備模式](active-directory-aadconnectsync-operations.md#staging-mode)並確認 hello 舊 DirSync 和新的 Azure AD Connect 組態。</span><span class="sxs-lookup"><span data-stu-id="aba45-153">In those cases, hello recommendation is tooinstall a new Azure AD Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode) and verify hello old DirSync and new Azure AD Connect configuration.</span></span> <span data-ttu-id="aba45-154">使用自訂組態重新套用任何變更，如 [Azure AD Connect 同步處理自訂組態](active-directory-aadconnectsync-whatis.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="aba45-154">Reapply any changes using custom configuration, as described in [Azure AD Connect Sync custom configuration](active-directory-aadconnectsync-whatis.md).</span></span>

<span data-ttu-id="aba45-155">無法擷取 hello 以 DirSync 用於 hello 服務帳戶的密碼，並不會移轉。</span><span class="sxs-lookup"><span data-stu-id="aba45-155">hello passwords used by DirSync for hello service accounts cannot be retrieved and are not migrated.</span></span> <span data-ttu-id="aba45-156">Hello 升級期間重設這些密碼。</span><span class="sxs-lookup"><span data-stu-id="aba45-156">These passwords are reset during hello upgrade.</span></span>

### <a name="high-level-steps-for-upgrading-from-dirsync-tooazure-ad-connect"></a><span data-ttu-id="aba45-157">從 DirSync tooAzure 升級 AD Connect 的概要步驟</span><span class="sxs-lookup"><span data-stu-id="aba45-157">High-level steps for upgrading from DirSync tooAzure AD Connect</span></span>
1. <span data-ttu-id="aba45-158">歡迎使用 tooAzure AD Connect</span><span class="sxs-lookup"><span data-stu-id="aba45-158">Welcome tooAzure AD Connect</span></span>
2. <span data-ttu-id="aba45-159">目前 DirSync 組態的分析</span><span class="sxs-lookup"><span data-stu-id="aba45-159">Analysis of current DirSync configuration</span></span>
3. <span data-ttu-id="aba45-160">收集 Azure AD 全域管理員密碼</span><span class="sxs-lookup"><span data-stu-id="aba45-160">Collect Azure AD global admin password</span></span>
4. <span data-ttu-id="aba45-161">（僅限用於 Azure AD connect 的 hello 安裝期間），請收集企業系統管理員帳戶的認證</span><span class="sxs-lookup"><span data-stu-id="aba45-161">Collect credentials for an enterprise admin account (only used during hello installation of Azure AD Connect)</span></span>
5. <span data-ttu-id="aba45-162">Azure AD Connect 安裝</span><span class="sxs-lookup"><span data-stu-id="aba45-162">Installation of Azure AD Connect</span></span>
   * <span data-ttu-id="aba45-163">解除安裝 DirSync (或暫時停用)</span><span class="sxs-lookup"><span data-stu-id="aba45-163">Uninstall DirSync (or temporarily disable it)</span></span>
   * <span data-ttu-id="aba45-164">安裝 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="aba45-164">Install Azure AD Connect</span></span>
   * <span data-ttu-id="aba45-165">選擇性地開始同步處理</span><span class="sxs-lookup"><span data-stu-id="aba45-165">Optionally begin synchronization</span></span>

<span data-ttu-id="aba45-166">發生下列情況時，需要其他步驟：</span><span class="sxs-lookup"><span data-stu-id="aba45-166">Additional steps are required when:</span></span>

* <span data-ttu-id="aba45-167">您目前正在使用完整 SQL Server - 本機或遠端</span><span class="sxs-lookup"><span data-stu-id="aba45-167">You're currently using Full SQL Server - local or remote</span></span>
* <span data-ttu-id="aba45-168">您擁有超過 5 萬個物件的規模可進行同步處理</span><span class="sxs-lookup"><span data-stu-id="aba45-168">You have more than 50,000 objects in scope for synchronization</span></span>

## <a name="in-place-upgrade"></a><span data-ttu-id="aba45-169">就地升級</span><span class="sxs-lookup"><span data-stu-id="aba45-169">In-place upgrade</span></span>
1. <span data-ttu-id="aba45-170">啟動 hello Azure AD Connect installer (MSI)。</span><span class="sxs-lookup"><span data-stu-id="aba45-170">Launch hello Azure AD Connect installer (MSI).</span></span>
2. <span data-ttu-id="aba45-171">請先詳閱並同意 toolicense 條款及隱私權注意事項。</span><span class="sxs-lookup"><span data-stu-id="aba45-171">Review and agree toolicense terms and privacy notice.</span></span>  
   ![歡迎使用 tooAzure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Welcome.png)
3. <span data-ttu-id="aba45-173">按一下 下一步 toobegin 分析您現有的 DirSync 安裝。</span><span class="sxs-lookup"><span data-stu-id="aba45-173">Click next toobegin analysis of your existing DirSync installation.</span></span>  
   ![分析現有目錄同步作業安裝](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Analyze.png)
4. <span data-ttu-id="aba45-175">Hello 分析完成時，您會看到 hello 建議如何 tooproceed。</span><span class="sxs-lookup"><span data-stu-id="aba45-175">When hello analysis completes, you see hello recommendations on how tooproceed.</span></span>  
   * <span data-ttu-id="aba45-176">如果您使用 SQL Server Express，並具有少於 50,000 個物件，會顯示下列畫面的 hello:</span><span class="sxs-lookup"><span data-stu-id="aba45-176">If you use SQL Server Express and have less than 50,000 objects, hello following screen is shown:</span></span>  
     ![分析完成準備好從 DirSync tooupgrade](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReady.png)
   * <span data-ttu-id="aba45-178">如果您使用完整的 SQL Server for DirSync 功能，您會看到這個頁面：</span><span class="sxs-lookup"><span data-stu-id="aba45-178">If you use a full SQL Server for DirSync, you see this page instead:</span></span>  
     <span data-ttu-id="aba45-179">![分析完成準備好從 DirSync tooupgrade](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReadyFullSQL.png)</span><span class="sxs-lookup"><span data-stu-id="aba45-179">![Analysis completed ready tooupgrade from DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReadyFullSQL.png)</span></span>  
     <span data-ttu-id="aba45-180">會顯示 hello hello 現有 SQL Server 資料庫伺服器正在使用目錄同步相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="aba45-180">hello information regarding hello existing SQL Server database server being used by DirSync is displayed.</span></span> <span data-ttu-id="aba45-181">如果需要，請進行適當的調整。</span><span class="sxs-lookup"><span data-stu-id="aba45-181">Make appropriate adjustments if needed.</span></span> <span data-ttu-id="aba45-182">按一下**下一步**toocontinue hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="aba45-182">Click **Next** toocontinue hello installation.</span></span>
   * <span data-ttu-id="aba45-183">如果您有超過 5 萬個物件，您會看到這個畫面：</span><span class="sxs-lookup"><span data-stu-id="aba45-183">If you have more than 50,000 objects, you see this screen instead:</span></span>  
     <span data-ttu-id="aba45-184">![分析完成準備好從 DirSync tooupgrade](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)</span><span class="sxs-lookup"><span data-stu-id="aba45-184">![Analysis completed ready tooupgrade from DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)</span></span>  
     <span data-ttu-id="aba45-185">tooproceed 進行就地升級時，按一下 [hello] 核取方塊下一步 toothis 訊息：**繼續在此電腦上升級目錄同步。**</span><span class="sxs-lookup"><span data-stu-id="aba45-185">tooproceed with an in-place upgrade, click hello checkbox next toothis message: **Continue upgrading DirSync on this computer.**</span></span>
     <span data-ttu-id="aba45-186">toodo[平行部署](#parallel-deployment)請匯出 hello DirSync 組態設定，並且移動 hello 組態 toohello 新伺服器。</span><span class="sxs-lookup"><span data-stu-id="aba45-186">toodo a [parallel deployment](#parallel-deployment) instead, you export hello DirSync configuration settings and move hello configuration toohello new server.</span></span>
5. <span data-ttu-id="aba45-187">提供您目前使用 tooconnect tooAzure AD hello 帳戶 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="aba45-187">Provide hello password for hello account you currently use tooconnect tooAzure AD.</span></span> <span data-ttu-id="aba45-188">這必須是目前使用的目錄同步的 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="aba45-188">This must be hello account currently used by DirSync.</span></span>  
   <span data-ttu-id="aba45-189">![輸入您的 Azure AD 認證](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToAzureAD.png)</span><span class="sxs-lookup"><span data-stu-id="aba45-189">![Enter your Azure AD credentials](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToAzureAD.png)</span></span>  
   <span data-ttu-id="aba45-190">如果您收到錯誤訊息，而且有連線問題，請參閱 [針對連線問題進行疑難排解](active-directory-aadconnect-troubleshoot-connectivity.md)。</span><span class="sxs-lookup"><span data-stu-id="aba45-190">If you receive an error and have problems with connectivity, see [Troubleshoot connectivity problems](active-directory-aadconnect-troubleshoot-connectivity.md).</span></span>
6. <span data-ttu-id="aba45-191">提供 Active Directory 的企業系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="aba45-191">Provide an enterprise admin account for Active Directory.</span></span>  
   ![輸入您的 ADDS 認證](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToADDS.png)
7. <span data-ttu-id="aba45-193">您現在準備好 tooconfigure。</span><span class="sxs-lookup"><span data-stu-id="aba45-193">You're now ready tooconfigure.</span></span> <span data-ttu-id="aba45-194">當您按一下 [升級] 時，系統會解除安裝 DirSync，而 Azure AD Connect 會完成設定並開始同步處理。</span><span class="sxs-lookup"><span data-stu-id="aba45-194">When you click **Upgrade**, DirSync is uninstalled and Azure AD Connect is configured and begins synchronizing.</span></span>  
   <span data-ttu-id="aba45-195">![準備好 tooconfigure](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ReadyToConfigure.png)</span><span class="sxs-lookup"><span data-stu-id="aba45-195">![Ready tooconfigure](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ReadyToConfigure.png)</span></span>
8. <span data-ttu-id="aba45-196">Hello 安裝完成後，登出再登入一次 tooWindows 才能使用 [同步處理服務管理員，同步處理規則編輯器] 中，或嘗試 toomake 任何其他組態變更。</span><span class="sxs-lookup"><span data-stu-id="aba45-196">After hello installation has completed, sign out and sign in again tooWindows before you use Synchronization Service Manager, Synchronization Rule Editor, or try toomake any other configuration changes.</span></span>

## <a name="parallel-deployment"></a><span data-ttu-id="aba45-197">平行部署</span><span class="sxs-lookup"><span data-stu-id="aba45-197">Parallel deployment</span></span>
### <a name="export-hello-dirsync-configuration"></a><span data-ttu-id="aba45-198">匯出 hello DirSync 組態</span><span class="sxs-lookup"><span data-stu-id="aba45-198">Export hello DirSync configuration</span></span>
<span data-ttu-id="aba45-199">**平行部署超過 5 萬個物件**</span><span class="sxs-lookup"><span data-stu-id="aba45-199">**Parallel deployment with more than 50,000 objects**</span></span>

<span data-ttu-id="aba45-200">如果您有超過 50,000 個物件，則 hello Azure AD Connect 的安裝將會建議平行部署。</span><span class="sxs-lookup"><span data-stu-id="aba45-200">If you have more than 50,000 objects, then hello Azure AD Connect installation recommends a parallel deployment.</span></span>

<span data-ttu-id="aba45-201">類似 toohello 後的螢幕會顯示：</span><span class="sxs-lookup"><span data-stu-id="aba45-201">A screen similar toohello following is displayed:</span></span>  
![分析完成](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)

<span data-ttu-id="aba45-203">如果您想 tooproceed 平行部署，您需要下列步驟 tooperform hello:</span><span class="sxs-lookup"><span data-stu-id="aba45-203">If you want tooproceed with parallel deployment, you need tooperform hello following steps:</span></span>

* <span data-ttu-id="aba45-204">按一下 hello**匯出設定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="aba45-204">Click hello **Export settings** button.</span></span> <span data-ttu-id="aba45-205">當您安裝 Azure AD Connect 的伺服器上時，從目前目錄同步 tooyour 新 Azure AD Connect 的安裝移轉這些設定。</span><span class="sxs-lookup"><span data-stu-id="aba45-205">When you install Azure AD Connect on a separate server, these settings are migrated from your current DirSync tooyour new Azure AD Connect installation.</span></span>

<span data-ttu-id="aba45-206">一旦成功匯出您的設定，您可以結束 hello hello DirSync 伺服器上的 Azure AD Connect 精靈。</span><span class="sxs-lookup"><span data-stu-id="aba45-206">Once your settings have been successfully exported, you can exit hello Azure AD Connect wizard on hello DirSync server.</span></span> <span data-ttu-id="aba45-207">太繼續進行下一個步驟的 hello[不同的伺服器上安裝 Azure AD Connect](#installation-of-azure-ad-connect-on-separate-server)</span><span class="sxs-lookup"><span data-stu-id="aba45-207">Continue with hello next step too[install Azure AD Connect on a separate server](#installation-of-azure-ad-connect-on-separate-server)</span></span>

<span data-ttu-id="aba45-208">**平行部署少於 5 萬個物件**</span><span class="sxs-lookup"><span data-stu-id="aba45-208">**Parallel deployment with less than 50,000 objects**</span></span>

<span data-ttu-id="aba45-209">如果您具有少於 50,000 個物件，但仍想 toodo 平行部署，然後 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="aba45-209">If you have less than 50,000 objects but still want toodo a parallel deployment, then do hello following:</span></span>

1. <span data-ttu-id="aba45-210">執行 hello Azure AD Connect installer (MSI)。</span><span class="sxs-lookup"><span data-stu-id="aba45-210">Run hello Azure AD Connect installer (MSI).</span></span>
2. <span data-ttu-id="aba45-211">當您看到 hello ** 褖畫惎 tooAzure AD Connect**畫面上，按一下 hello 最上層視窗的右下角 hello hello"X"結束 hello 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="aba45-211">When you see hello **Welcome tooAzure AD Connect** screen, exit hello installation wizard by clicking hello "X" in hello top right corner of hello window.</span></span>
3. <span data-ttu-id="aba45-212">開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="aba45-212">Open a command prompt.</span></span>
4. <span data-ttu-id="aba45-213">從 hello 安裝 Azure AD Connect 的位置 (預設： C:\Program Files\Microsoft Azure Active Directory Connect) 執行下列命令的 hello: `AzureADConnect.exe /ForceExport`。</span><span class="sxs-lookup"><span data-stu-id="aba45-213">From hello install location of Azure AD Connect (Default: C:\Program Files\Microsoft Azure Active Directory Connect) execute hello following command:  `AzureADConnect.exe /ForceExport`.</span></span>
5. <span data-ttu-id="aba45-214">按一下 hello**匯出設定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="aba45-214">Click hello **Export settings** button.</span></span> <span data-ttu-id="aba45-215">當您安裝 Azure AD Connect 的伺服器上時，從目前目錄同步 tooyour 新 Azure AD Connect 的安裝移轉這些設定。</span><span class="sxs-lookup"><span data-stu-id="aba45-215">When you install Azure AD Connect on a separate server, these settings are migrated from your current DirSync tooyour new Azure AD Connect installation.</span></span>

![分析完成](./media/active-directory-aadconnect-dirsync-upgrade-get-started/forceexport.png)

<span data-ttu-id="aba45-217">一旦成功匯出您的設定，您可以結束 hello hello DirSync 伺服器上的 Azure AD Connect 精靈。</span><span class="sxs-lookup"><span data-stu-id="aba45-217">Once your settings have been successfully exported, you can exit hello Azure AD Connect wizard on hello DirSync server.</span></span> <span data-ttu-id="aba45-218">太繼續進行下一個步驟的 hello[不同的伺服器上安裝 Azure AD Connect](#installation-of-azure-ad-connect-on-separate-server)。</span><span class="sxs-lookup"><span data-stu-id="aba45-218">Continue with hello next step too[install Azure AD Connect on a separate server](#installation-of-azure-ad-connect-on-separate-server).</span></span>

### <a name="install-azure-ad-connect-on-separate-server"></a><span data-ttu-id="aba45-219">在不同的伺服器上安裝 Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="aba45-219">Install Azure AD Connect on separate server</span></span>
<span data-ttu-id="aba45-220">當您在新伺服器上安裝 Azure AD Connect 時，hello 假設會是您想 tooperform Azure AD Connect 的全新安裝。</span><span class="sxs-lookup"><span data-stu-id="aba45-220">When you install Azure AD Connect on a new server, hello assumption is that you want tooperform a clean install of Azure AD Connect.</span></span> <span data-ttu-id="aba45-221">由於您希望 toouse hello DirSync 組態，有一些額外的步驟 tootake:</span><span class="sxs-lookup"><span data-stu-id="aba45-221">Since you want toouse hello DirSync configuration, there are some extra steps tootake:</span></span>

1. <span data-ttu-id="aba45-222">執行 hello Azure AD Connect installer (MSI)。</span><span class="sxs-lookup"><span data-stu-id="aba45-222">Run hello Azure AD Connect installer (MSI).</span></span>
2. <span data-ttu-id="aba45-223">當您看到 hello ** 褖畫惎 tooAzure AD Connect**畫面上，按一下 hello 最上層視窗的右下角 hello hello"X"結束 hello 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="aba45-223">When you see hello **Welcome tooAzure AD Connect** screen, exit hello installation wizard by clicking hello "X" in hello top right corner of hello window.</span></span>
3. <span data-ttu-id="aba45-224">開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="aba45-224">Open a command prompt.</span></span>
4. <span data-ttu-id="aba45-225">從 hello 安裝 Azure AD Connect 的位置 (預設： C:\Program Files\Microsoft Azure Active Directory Connect) 執行下列命令的 hello: `AzureADConnect.exe /migrate`。</span><span class="sxs-lookup"><span data-stu-id="aba45-225">From hello install location of Azure AD Connect (Default: C:\Program Files\Microsoft Azure Active Directory Connect) execute hello following command: `AzureADConnect.exe /migrate`.</span></span>
   <span data-ttu-id="aba45-226">hello Azure AD Connect 的安裝精靈會啟動，並會顯示下列畫面 hello:</span><span class="sxs-lookup"><span data-stu-id="aba45-226">hello Azure AD Connect installation wizard starts and presents you with hello following screen:</span></span>  
   <span data-ttu-id="aba45-227">![輸入您的 Azure AD 認證](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ImportSettings.png)</span><span class="sxs-lookup"><span data-stu-id="aba45-227">![Enter your Azure AD credentials](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ImportSettings.png)</span></span>
5. <span data-ttu-id="aba45-228">選取從您的 DirSync 安裝所匯出的 hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="aba45-228">Select hello settings file that exported from your DirSync installation.</span></span>
6. <span data-ttu-id="aba45-229">設定任何進階選項，包括：</span><span class="sxs-lookup"><span data-stu-id="aba45-229">Configure any advanced options including:</span></span>
   * <span data-ttu-id="aba45-230">Azure AD Connect 的自訂安裝位置。</span><span class="sxs-lookup"><span data-stu-id="aba45-230">A custom installation location for Azure AD Connect.</span></span>
   * <span data-ttu-id="aba45-231">現有 SQL Server 執行個體 (預設值：Azure AD Connect 會安裝 SQL Server 2012 Express)。</span><span class="sxs-lookup"><span data-stu-id="aba45-231">An existing instance of SQL Server (Default: Azure AD Connect installs SQL Server 2012 Express).</span></span> <span data-ttu-id="aba45-232">請勿使用 hello 與 DirSync 伺服器相同的資料庫執行個體。</span><span class="sxs-lookup"><span data-stu-id="aba45-232">Do not use hello same database instance as your DirSync server.</span></span>
   * <span data-ttu-id="aba45-233">（如果您的 SQL Server 資料庫位於遠端，則此帳戶必須是網域的服務帳戶） tooconnect tooSQL 伺服器使用的服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="aba45-233">A service account used tooconnect tooSQL Server (If your SQL Server database is remote then this account must be a domain service account).</span></span>
     <span data-ttu-id="aba45-234">您可以在這個畫面上看到下列選項：</span><span class="sxs-lookup"><span data-stu-id="aba45-234">These options can be seen on this screen:</span></span>  
     <span data-ttu-id="aba45-235">![輸入您的 Azure AD 認證](./media/active-directory-aadconnect-dirsync-upgrade-get-started/advancedsettings.png)</span><span class="sxs-lookup"><span data-stu-id="aba45-235">![Enter your Azure AD credentials](./media/active-directory-aadconnect-dirsync-upgrade-get-started/advancedsettings.png)</span></span>
7. <span data-ttu-id="aba45-236">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="aba45-236">Click **Next**.</span></span>
8. <span data-ttu-id="aba45-237">在 hello**準備 tooconfigure**頁面上，保留 hello **hello 組態完成之後儘速開始 hello 同步處理程序**檢查。</span><span class="sxs-lookup"><span data-stu-id="aba45-237">On hello **Ready tooconfigure** page, leave hello **Start hello synchronization process as soon as hello configuration completes** checked.</span></span> <span data-ttu-id="aba45-238">hello 伺服器現在為[預備模式](active-directory-aadconnectsync-operations.md#staging-mode)讓變更不會匯出的 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="aba45-238">hello server is now in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode) so changes are not exported tooAzure AD.</span></span>
9. <span data-ttu-id="aba45-239">按一下 [Install] 。</span><span class="sxs-lookup"><span data-stu-id="aba45-239">Click **Install**.</span></span>
10. <span data-ttu-id="aba45-240">Hello 安裝完成後，登出再登入一次 tooWindows 才能使用 [同步處理服務管理員，同步處理規則編輯器] 中，或嘗試 toomake 任何其他組態變更。</span><span class="sxs-lookup"><span data-stu-id="aba45-240">After hello installation has completed, sign out and sign in again tooWindows before you use Synchronization Service Manager, Synchronization Rule Editor, or try toomake any other configuration changes.</span></span>

> [!NOTE]
> <span data-ttu-id="aba45-241">Windows Server Active Directory 與 Azure Active Directory 之間的同步處理開始，但不不匯出的 tooAzure AD 的任何變更。</span><span class="sxs-lookup"><span data-stu-id="aba45-241">Synchronization between Windows Server Active Directory and Azure Active Directory begins, but no changes are exported tooAzure AD.</span></span> <span data-ttu-id="aba45-242">一次只能有一個作用中的同步處理工具匯出變更。</span><span class="sxs-lookup"><span data-stu-id="aba45-242">Only one synchronization tool can be actively exporting changes at a time.</span></span> <span data-ttu-id="aba45-243">此狀態稱為[預備模式](active-directory-aadconnectsync-operations.md#staging-mode)。</span><span class="sxs-lookup"><span data-stu-id="aba45-243">This state is called [staging mode](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

### <a name="verify-that-azure-ad-connect-is-ready-toobegin-synchronization"></a><span data-ttu-id="aba45-244">驗證 Azure AD Connect 準備好 toobegin 同步處理</span><span class="sxs-lookup"><span data-stu-id="aba45-244">Verify that Azure AD Connect is ready toobegin synchronization</span></span>
<span data-ttu-id="aba45-245">Azure AD Connect 是透過從目錄同步的準備 tootake 的 tooverify，您需要 tooopen**同步處理服務管理員**hello 群組中**Azure AD Connect**從 hello [開始] 功能表。</span><span class="sxs-lookup"><span data-stu-id="aba45-245">tooverify that Azure AD Connect is ready tootake over from DirSync, you need tooopen **Synchronization Service Manager** in hello group **Azure AD Connect** from hello start menu.</span></span>

<span data-ttu-id="aba45-246">在 [hello 應用程式中，移 toohello**作業**] 索引標籤。此索引標籤上，確認已完成下列作業的 hello:</span><span class="sxs-lookup"><span data-stu-id="aba45-246">In hello application, go toohello **Operations** tab. On this tab, confirm that hello following operations have completed:</span></span>

* <span data-ttu-id="aba45-247">在 hello AD 連接器匯入</span><span class="sxs-lookup"><span data-stu-id="aba45-247">Import on hello AD Connector</span></span>
* <span data-ttu-id="aba45-248">在 hello Azure AD 連接器匯入</span><span class="sxs-lookup"><span data-stu-id="aba45-248">Import on hello Azure AD Connector</span></span>
* <span data-ttu-id="aba45-249">Hello AD 連接器上的完整同步處理</span><span class="sxs-lookup"><span data-stu-id="aba45-249">Full Sync on hello AD Connector</span></span>
* <span data-ttu-id="aba45-250">完整同步處理在 hello Azure AD Connector</span><span class="sxs-lookup"><span data-stu-id="aba45-250">Full Sync on hello Azure AD Connector</span></span>

![匯入和同步處理完成](./media/active-directory-aadconnect-dirsync-upgrade-get-started/importsynccompleted.png)

<span data-ttu-id="aba45-252">檢閱 hello 從這些作業的結果，並確定沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="aba45-252">Review hello result from these operations and ensure there are no errors.</span></span>

<span data-ttu-id="aba45-253">如果您想 toosee 並檢查所需 toobe 匯出 tooAzure AD hello 變更，然後讀取方式 tooverify hello 底下設定[預備模式](active-directory-aadconnectsync-operations.md#staging-mode)。</span><span class="sxs-lookup"><span data-stu-id="aba45-253">If you want toosee and inspect hello changes that are about toobe exported tooAzure AD, then read how tooverify hello configuration under [staging mode](active-directory-aadconnectsync-operations.md#staging-mode).</span></span> <span data-ttu-id="aba45-254">進行必要的組態變更，直到看不到非預期的任何項目。</span><span class="sxs-lookup"><span data-stu-id="aba45-254">Make required configuration changes until you do not see anything unexpected.</span></span>

<span data-ttu-id="aba45-255">您已準備好 tooswitch 從 DirSync tooAzure AD，當您完成這些步驟並滿意 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="aba45-255">You are ready tooswitch from DirSync tooAzure AD when you have completed these steps and are happy with hello result.</span></span>

### <a name="uninstall-dirsync-old-server"></a><span data-ttu-id="aba45-256">解除安裝 DirSync (舊伺服器)</span><span class="sxs-lookup"><span data-stu-id="aba45-256">Uninstall DirSync (old server)</span></span>
* <span data-ttu-id="aba45-257">在 [程式和功能] 中，尋找 [Windows Azure Active Directory 同步作業工具]</span><span class="sxs-lookup"><span data-stu-id="aba45-257">In **Programs and features** find **Windows Azure Active Directory sync tool**</span></span>
* <span data-ttu-id="aba45-258">解除安裝 [Windows Azure Active Directory 同步作業工具] </span><span class="sxs-lookup"><span data-stu-id="aba45-258">Uninstall **Windows Azure Active Directory sync tool**</span></span>
* <span data-ttu-id="aba45-259">hello 解除安裝可能會佔用 too15 分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="aba45-259">hello uninstallation might take up too15 minutes toocomplete.</span></span>

<span data-ttu-id="aba45-260">如果您偏好 toouninstall 目錄同步之後，您就可以也會暫時關閉 hello 伺服器，或停用 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="aba45-260">If you prefer toouninstall DirSync later, you can also temporarily shut down hello server or disable hello service.</span></span> <span data-ttu-id="aba45-261">如果發生錯誤，這個方法可讓您 toore 啟用它。</span><span class="sxs-lookup"><span data-stu-id="aba45-261">If something goes wrong, this method allows you toore-enable it.</span></span> <span data-ttu-id="aba45-262">不過，不應該該 hello 下一個步驟將會失敗，因此這應該不需要。</span><span class="sxs-lookup"><span data-stu-id="aba45-262">However, it is not expected that hello next step will fail so this should not be needed.</span></span>

<span data-ttu-id="aba45-263">解除安裝或停用目錄同步，匯出 tooAzure AD 沒有作用中伺服器。</span><span class="sxs-lookup"><span data-stu-id="aba45-263">With DirSync uninstalled or disabled, there is no active server exporting tooAzure AD.</span></span> <span data-ttu-id="aba45-264">您在內部部署 Active Directory 中的任何變更將會繼續執行同步處理的 toobe tooAzure AD，則必須完成下一個步驟 tooenable hello Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="aba45-264">hello next step tooenable Azure AD Connect must be completed before any changes in your on-premises Active Directory will continue toobe synchronized tooAzure AD.</span></span>

### <a name="enable-azure-ad-connect-new-server"></a><span data-ttu-id="aba45-265">啟用 Azure AD Connect (新伺服器)</span><span class="sxs-lookup"><span data-stu-id="aba45-265">Enable Azure AD Connect (new server)</span></span>
<span data-ttu-id="aba45-266">安裝完成後，重新開啟 Azure AD 連接將會讓您 toomake 其他組態變更。</span><span class="sxs-lookup"><span data-stu-id="aba45-266">After installation, reopening Azure AD connect will allow you toomake additional configuration changes.</span></span> <span data-ttu-id="aba45-267">啟動**Azure AD Connect**從 hello [開始] 功能表或從 hello hello 桌面上的捷徑。</span><span class="sxs-lookup"><span data-stu-id="aba45-267">Start **Azure AD Connect** from hello start menu or from hello shortcut on hello desktop.</span></span> <span data-ttu-id="aba45-268">請確定您不會嘗試 toorun hello 安裝 MSI 一次。</span><span class="sxs-lookup"><span data-stu-id="aba45-268">Make sure you do not try toorun hello installation MSI again.</span></span>

<span data-ttu-id="aba45-269">您應該會看到下列 hello:</span><span class="sxs-lookup"><span data-stu-id="aba45-269">You should see hello following:</span></span>  
![其他工作](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AdditionalTasks.png)

* <span data-ttu-id="aba45-271">選取 [設定預備模式] 。</span><span class="sxs-lookup"><span data-stu-id="aba45-271">Select **Configure staging mode**.</span></span>
* <span data-ttu-id="aba45-272">關閉正在取消 hello 臨時**啟用預備模式**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="aba45-272">Turn off staging by unchecking hello **Enabled staging mode** checkbox.</span></span>

![輸入您的 Azure AD 認證](./media/active-directory-aadconnect-dirsync-upgrade-get-started/configurestaging.png)

* <span data-ttu-id="aba45-274">按一下 hello**下一步**按鈕</span><span class="sxs-lookup"><span data-stu-id="aba45-274">Click hello **Next** button</span></span>
* <span data-ttu-id="aba45-275">在 hello 確認頁面上，按一下 [hello**安裝**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="aba45-275">On hello confirmation page, click hello **install** button.</span></span>

<span data-ttu-id="aba45-276">Azure AD Connect 現在是作用中的伺服器，您必須切換後 toousing 現有的 DirSync 伺服器。</span><span class="sxs-lookup"><span data-stu-id="aba45-276">Azure AD Connect is now your active server and you must not switch back toousing your existing DirSync server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aba45-277">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aba45-277">Next steps</span></span>
<span data-ttu-id="aba45-278">既然您已安裝的 Azure AD Connect 可以[確認 hello 安裝並指派授權](active-directory-aadconnect-whats-next.md)。</span><span class="sxs-lookup"><span data-stu-id="aba45-278">Now that you have Azure AD Connect installed you can [verify hello installation and assign licenses](active-directory-aadconnect-whats-next.md).</span></span>

<span data-ttu-id="aba45-279">深入了解這些新功能，與 hello 安裝已啟用：[自動升級](active-directory-aadconnect-feature-automatic-upgrade.md)，[防止被意外刪除](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)，和[Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md)。</span><span class="sxs-lookup"><span data-stu-id="aba45-279">Learn more about these new features, which were enabled with hello installation: [Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md), [Prevent accidental deletes](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), and [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).</span></span>

<span data-ttu-id="aba45-280">深入了解這些常見的主題：[排程器和 tootrigger 的同步處理](active-directory-aadconnectsync-feature-scheduler.md)。</span><span class="sxs-lookup"><span data-stu-id="aba45-280">Learn more about these common topics: [scheduler and how tootrigger sync](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

<span data-ttu-id="aba45-281">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="aba45-281">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
