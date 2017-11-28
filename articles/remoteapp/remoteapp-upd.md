---
title: "aaaHow 未儲存使用者資料和設定的 Azure RemoteApp 嗎？ | Microsoft Docs"
description: "了解 Azure RemoteApp 將使用者資料使用 hello 使用者設定檔磁碟的儲存。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: e125af62-5c1a-4186-a238-52f537f7bb34
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dccebc7861e8a0d87cb3ee174f399a2df7fe023c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-remoteapp-save-user-data-and-settings"></a><span data-ttu-id="ee073-104">Azure RemoteApp 如何儲存使用者資料和設定？</span><span class="sxs-lookup"><span data-stu-id="ee073-104">How does Azure RemoteApp save user data and settings?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ee073-105">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="ee073-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ee073-106">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ee073-106">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ee073-107">Azure RemoteApp 跨越裝置和工作階段儲存使用者身分識別和自訂。</span><span class="sxs-lookup"><span data-stu-id="ee073-107">Azure RemoteApp saves user identity and customizations across devices and sessions.</span></span> <span data-ttu-id="ee073-108">此使用者資料會依每個使用者和每個集合磁碟 (也稱為使用者設定檔磁碟 (UPD)) 儲存。</span><span class="sxs-lookup"><span data-stu-id="ee073-108">This user data is stored in a per-user per-collection disk, known as a user profile disk (UPD).</span></span> <span data-ttu-id="ee073-109">hello 磁碟遵循 hello 使用者，並確保 hello 使用者有一致的經驗，不論他們登入的位置。</span><span class="sxs-lookup"><span data-stu-id="ee073-109">hello disk follows hello user and ensures hello user has a consistent experience, regardless of where they sign in.</span></span>

<span data-ttu-id="ee073-110">使用者設定檔磁碟是完全透明 toohello 使用者-使用者儲存文件 tootheir 文件 資料夾 （在看似 toobe 本機磁碟機） 和變更他們的應用程式設定，如往常般。</span><span class="sxs-lookup"><span data-stu-id="ee073-110">User profile disks are completely transparent toohello user — users save documents tootheir Documents folder (on what appears toobe a local drive) and change their app settings as usual.</span></span> <span data-ttu-id="ee073-111">在 hello 相同連接 tooAzure RemoteApp 從任何裝置時，保存階段，所有個人設定。</span><span class="sxs-lookup"><span data-stu-id="ee073-111">At hello same time, all personal settings persist when connecting tooAzure RemoteApp from any device.</span></span> <span data-ttu-id="ee073-112">所有的 hello 使用者看見他們 hello 中的資料相同的位置。</span><span class="sxs-lookup"><span data-stu-id="ee073-112">All hello user sees is their data in hello same place.</span></span>

<span data-ttu-id="ee073-113">每個 UPD 有 50GB 的永續性儲存體，並包含使用者資料和應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="ee073-113">Each UPD has 50GB of persistent storage and contains both user data and application settings.</span></span> 

<span data-ttu-id="ee073-114">請閱讀更多有關使用者設定檔資料的特殊資訊。</span><span class="sxs-lookup"><span data-stu-id="ee073-114">Read on for specifics on user profile data.</span></span>

> [!NOTE]
> <span data-ttu-id="ee073-115">需要 toodisable hello UPD 嗎？</span><span class="sxs-lookup"><span data-stu-id="ee073-115">Need toodisable hello UPD?</span></span> <span data-ttu-id="ee073-116">現在您可以那麼做了 - 詳細資料請查看 Pavithra 的部落格文章： [在 Azure RemoteApp 停用使用者設定檔磁碟 (UPD)](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/)(英文)。</span><span class="sxs-lookup"><span data-stu-id="ee073-116">You can do that now - check out Pavithra's blog post, [Disable User Profile Disks (UPDs) in Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/), for details.</span></span>
> 
> 

## <a name="how-can-an-admin-get-toohello-data"></a><span data-ttu-id="ee073-117">系統管理員如何取得 toohello 資料？</span><span class="sxs-lookup"><span data-stu-id="ee073-117">How can an admin get toohello data?</span></span>
<span data-ttu-id="ee073-118">如果您針對您的使用者 （適用於嚴重損壞修復，或如果 hello 使用者離職後 hello 公司） 的其中一個需要 tooaccess hello 資料，請連絡 Azure 支援人員並提供 hello 訂用帳戶資訊 hello 集合和 hello 使用者識別。</span><span class="sxs-lookup"><span data-stu-id="ee073-118">If you need tooaccess hello data for one of your users (for disaster recovery or if hello user leaves hello company), contact Azure Support and provide hello subscription information for hello collection and hello user identity.</span></span> <span data-ttu-id="ee073-119">hello Azure RemoteApp 小組提供 URL toohello VHD。</span><span class="sxs-lookup"><span data-stu-id="ee073-119">hello Azure RemoteApp team will provide you a URL toohello VHD.</span></span> <span data-ttu-id="ee073-120">請下載該 VHD，並擷取您需要的任何文件或檔案。</span><span class="sxs-lookup"><span data-stu-id="ee073-120">Download that VHD and retrieve any documents or files you need.</span></span> <span data-ttu-id="ee073-121">請注意該 hello VHD 50 GB，因此將會花費元 toodownload 它。</span><span class="sxs-lookup"><span data-stu-id="ee073-121">Note that hello VHD is 50GB, so it will take a bit toodownload it.</span></span>

## <a name="is-hello-data-backed-up"></a><span data-ttu-id="ee073-122">Hello 資料備份嗎？</span><span class="sxs-lookup"><span data-stu-id="ee073-122">Is hello data backed up?</span></span>
<span data-ttu-id="ee073-123">是，我們會儲存每個地理位置的 hello 使用者資料的備份。</span><span class="sxs-lookup"><span data-stu-id="ee073-123">Yes, we save a backup of hello user data per geographic location.</span></span> <span data-ttu-id="ee073-124">hello 資料是唯讀的而且可以是存取 hello 相同方式與將 hello 一般資料 (請連絡 Azure RemoteApp tooget 它)，如果 hello 主要資料中心已關閉。</span><span class="sxs-lookup"><span data-stu-id="ee073-124">hello data is read-only and can be accessed in hello same way as hello regular data would be (contact Azure RemoteApp tooget it), if hello primary data center is down.</span></span> <span data-ttu-id="ee073-125">hello 資料複製即時 toohello 備份位置，以及我們不要保留不同版本的複本。</span><span class="sxs-lookup"><span data-stu-id="ee073-125">hello data is copied real-time toohello backup location and we do not keep copies of different versions.</span></span> <span data-ttu-id="ee073-126">因此，資料損毀，我們不會無法 toorestore 它先前已知良好的版本，但是如果 hello 主要資料中心已關機，您將會從能夠 tooget 使用者資料的 tooa hello 其他位置。</span><span class="sxs-lookup"><span data-stu-id="ee073-126">So, on data corruption, we will not be able toorestore it tooa previously known good version but if hello primary data center is down, you will be able tooget user data from hello other location.</span></span>

## <a name="how-do-users-see-hello-upd-on-hello-server-side"></a><span data-ttu-id="ee073-127">如何使用者看見 hello UPD hello 伺服器端上？</span><span class="sxs-lookup"><span data-stu-id="ee073-127">How do users see hello UPD on hello server side?</span></span>
<span data-ttu-id="ee073-128">每個使用者會有自己的目錄對應 tootheir UPD hello 伺服器上： c:\Users\username。</span><span class="sxs-lookup"><span data-stu-id="ee073-128">Each user will have their own directory on hello server that maps tootheir UPD: c:\Users\username.</span></span>

## <a name="whats-hello-best-way-toouse-outlook-and-upd"></a><span data-ttu-id="ee073-129">什麼是最佳方式 toouse hello Outlook 和 UPD？</span><span class="sxs-lookup"><span data-stu-id="ee073-129">What's hello best way toouse Outlook and UPD?</span></span>
<span data-ttu-id="ee073-130">Azure RemoteApp 儲存工作階段之間的 hello Outlook 狀態 （信箱，Pst）。</span><span class="sxs-lookup"><span data-stu-id="ee073-130">Azure RemoteApp saves hello Outlook state (mailboxes, PSTs) between sessions.</span></span> <span data-ttu-id="ee073-131">tooenable，我們需要 hello PST toobe 儲存在 hello 使用者設定檔資料 (c:\users\<使用者名稱 >)。</span><span class="sxs-lookup"><span data-stu-id="ee073-131">tooenable this, we need hello PST toobe stored in hello user profile data (c:\users\<username>).</span></span> <span data-ttu-id="ee073-132">這是 hello hello 資料，因此只要您不要變更 hello 位置的預設位置，hello 資料將會保存工作階段之間。</span><span class="sxs-lookup"><span data-stu-id="ee073-132">This is hello default location for hello data, so as long as you do not change hello location, hello data will persist between sessions.</span></span>

<span data-ttu-id="ee073-133">我們也建議您在 Outlook 中使用「快取」模式，並使用「伺服器/線上」模式進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="ee073-133">We also recommend that you use "cached" mode in Outlook and use "server/online" mode for searching.</span></span>

<span data-ttu-id="ee073-134">如需使用 Outlook 和 Azure RemoteApp 的詳細資訊，請查看 [這篇文章](remoteapp-outlook.md) 。</span><span class="sxs-lookup"><span data-stu-id="ee073-134">Check out [this article](remoteapp-outlook.md) for more information on using Outlook and Azure RemoteApp.</span></span>

## <a name="what-about-redirection"></a><span data-ttu-id="ee073-135">重新導向呢？</span><span class="sxs-lookup"><span data-stu-id="ee073-135">What about redirection?</span></span>
<span data-ttu-id="ee073-136">您可以設定 toolet 使用者來存取本機裝置設定的 Azure RemoteApp[重新導向](remoteapp-redirection.md)。</span><span class="sxs-lookup"><span data-stu-id="ee073-136">You can configure Azure RemoteApp toolet users access local devices by setting up [redirection](remoteapp-redirection.md).</span></span> <span data-ttu-id="ee073-137">本機裝置，如此便能 tooaccess hello UPD hello 資料。</span><span class="sxs-lookup"><span data-stu-id="ee073-137">Local devices will then be able tooaccess hello data on hello UPD.</span></span>

## <a name="can-i-use-my-upd-as-a-network-share"></a><span data-ttu-id="ee073-138">我可以使用 UPD 做為網路共用嗎？</span><span class="sxs-lookup"><span data-stu-id="ee073-138">Can I use my UPD as a network share?</span></span>
<span data-ttu-id="ee073-139">不用。</span><span class="sxs-lookup"><span data-stu-id="ee073-139">No.</span></span> <span data-ttu-id="ee073-140">UPD 不能做為網路共用。</span><span class="sxs-lookup"><span data-stu-id="ee073-140">UPDs cannot be used as a network share.</span></span> <span data-ttu-id="ee073-141">UPD 是只使用 toohello 時使用者 hello 使用者主動連接 tooAzure RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="ee073-141">A UPD is only available toohello user when hello user is actively connected tooAzure RemoteApp.</span></span>

## <a name="if-i-delete-a-user-from-a-collection-is-their-upd-deleted"></a><span data-ttu-id="ee073-142">如果我從集合中刪除使用者，其 UPD 是否也會刪除?</span><span class="sxs-lookup"><span data-stu-id="ee073-142">If I delete a user from a collection, is their UPD deleted?</span></span>
<span data-ttu-id="ee073-143">否，當您刪除使用者，我們不會自動刪除 hello UPD-相反地，我們會將儲存 hello 資料直到您刪除 hello 集合。</span><span class="sxs-lookup"><span data-stu-id="ee073-143">No, when you delete a user, we do not automatically delete hello UPD - instead, we store hello data until you delete hello collection.</span></span> <span data-ttu-id="ee073-144">90 天後刪除 hello 集合中，我們會刪除所有 Upd。</span><span class="sxs-lookup"><span data-stu-id="ee073-144">90 days after you delete hello collection, we delete all UPDs.</span></span> 

<span data-ttu-id="ee073-145">如果您需要 toodelete UPD 集合中，請連絡 Azure RemoteApp-我們可以從我們這邊刪除 UPD。</span><span class="sxs-lookup"><span data-stu-id="ee073-145">If you need toodelete a UPD from a collection, contact Azure RemoteApp - we can delete UPD from our side.</span></span>

## <a name="can-i-access-my-users-upds-either-current-or-deleted-users"></a><span data-ttu-id="ee073-146">我可以存取使用者的 UPD (目前或已刪除的使用者) 嗎？</span><span class="sxs-lookup"><span data-stu-id="ee073-146">Can I access my users' UPDs (either current or deleted users)?</span></span>
<span data-ttu-id="ee073-147">是，如果您連絡[Azure RemoteApp](mailto:remoteappforum@microsoft.com)，我們可以設定您具有 URL tooaccess hello 資料。</span><span class="sxs-lookup"><span data-stu-id="ee073-147">Yes, if you contact [Azure RemoteApp](mailto:remoteappforum@microsoft.com), we can set you up with a URL tooaccess hello data.</span></span> <span data-ttu-id="ee073-148">您將有 10 小時 toodownload 有關任何資料或檔案從 hello UPD hello 存取到期之前。</span><span class="sxs-lookup"><span data-stu-id="ee073-148">You'll have about 10 hours toodownload any data or files from hello UPD before hello access expires.</span></span>

## <a name="are-upds-available-offline"></a><span data-ttu-id="ee073-149">UPD 可離線使用嗎？</span><span class="sxs-lookup"><span data-stu-id="ee073-149">Are UPDs available offline?</span></span>
<span data-ttu-id="ee073-150">現在我們不提供離線存取 tooUPDs，除了上面所述的 hello 10 個小時存取視窗的權限。</span><span class="sxs-lookup"><span data-stu-id="ee073-150">Right now we do not provide offline access tooUPDs, beyond hello 10 hour access window described above.</span></span> <span data-ttu-id="ee073-151">這表示，我們目前沒有與您的時間夠長，toocomplete 更複雜的工作，像是 hello Upd 上執行防毒軟體或存取的稽核資料存取方式 tooprovide。</span><span class="sxs-lookup"><span data-stu-id="ee073-151">This means that we do not currently have a way tooprovide you with access for long enough toocomplete more complicated tasks, like running anti-virus software on hello UPDs or accessing data for an audit.</span></span>

## <a name="do-registry-key-settings-persist"></a><span data-ttu-id="ee073-152">登錄機碼設定可以保存嗎？</span><span class="sxs-lookup"><span data-stu-id="ee073-152">Do registry key settings persist?</span></span>
<span data-ttu-id="ee073-153">是，撰寫 tooHKEY_Current_User 的任何項目是 hello UPD 的一部分。</span><span class="sxs-lookup"><span data-stu-id="ee073-153">Yes, anything written tooHKEY_Current_User is part of hello UPD.</span></span>

## <a name="can-i-disable-upds-for-a-collection"></a><span data-ttu-id="ee073-154">我可以停用 集合的 UPD 嗎？</span><span class="sxs-lookup"><span data-stu-id="ee073-154">Can I disable UPDs for a collection?</span></span>
<span data-ttu-id="ee073-155">是，您可以要求 Azure RemoteApp toodisable Upd 訂用帳戶，但是您無法自行。</span><span class="sxs-lookup"><span data-stu-id="ee073-155">Yes, you can ask Azure RemoteApp toodisable UPDs for a subscription, but you cannot do that yourself.</span></span> <span data-ttu-id="ee073-156">這表示 Upd 將停用 hello 訂用帳戶中的所有集合。</span><span class="sxs-lookup"><span data-stu-id="ee073-156">This means that UPDs will be disabled for all collections in hello subscription.</span></span>

<span data-ttu-id="ee073-157">您可能想 toodisable Upd 任何 hello 下列情況：</span><span class="sxs-lookup"><span data-stu-id="ee073-157">You might want toodisable UPDs in any of hello following situations:</span></span> 

* <span data-ttu-id="ee073-158">您需要使用者資料的完整存取權限和控制 (針對稽核和檢閱之目的，例如金融機構)。</span><span class="sxs-lookup"><span data-stu-id="ee073-158">You need complete access and control of user data (for audit and review purposes such as financial institutions).</span></span>
* <span data-ttu-id="ee073-159">您已將 3rd 合作對象使用者設定檔管理解決方案的內部，而且想 toocontinue 已加入網域的 Azure RemoteApp 部署中使用它們。</span><span class="sxs-lookup"><span data-stu-id="ee073-159">You have 3rd-party user profile management solutions on-premises and want toocontinue using them in your domain-joined Azure RemoteApp deployment.</span></span> <span data-ttu-id="ee073-160">這會需要 hello 設定檔的代理程式 toobe 載入 hello 黃金映像。</span><span class="sxs-lookup"><span data-stu-id="ee073-160">This would require hello profile agent toobe loaded into hello gold image.</span></span> 
* <span data-ttu-id="ee073-161">您不需要任何本機資料存放區，或您擁有 hello 雲端或檔案共用中的所有資料，而且想要 toocontrol 儲存在本機使用 Azure RemoteApp 的資料。</span><span class="sxs-lookup"><span data-stu-id="ee073-161">You don’t need any local data storage or you have all data in hello cloud or file share and would like toocontrol saving of data locally using Azure RemoteApp.</span></span>

<span data-ttu-id="ee073-162">如需詳細資訊，請參閱[在 Azure RemoteApp 停用使用者設定檔磁碟 (UPD)](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/) (英文)。</span><span class="sxs-lookup"><span data-stu-id="ee073-162">See  [Disable User Profile Disks (UPDs) in Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/) for more information.</span></span>

## <a name="can-i-restrict-users-from-saving-data-toohello-system-drive"></a><span data-ttu-id="ee073-163">可以限制使用者無法儲存資料 toohello 系統磁碟機嗎？</span><span class="sxs-lookup"><span data-stu-id="ee073-163">Can I restrict users from saving data toohello system drive?</span></span>
<span data-ttu-id="ee073-164">是，但您仍需要 tooset 設定中的 hello 範本映像建立 hello 集合之前。</span><span class="sxs-lookup"><span data-stu-id="ee073-164">Yes, but you'll need tooset that up in hello template image before you create hello collection.</span></span> <span data-ttu-id="ee073-165">使用下列步驟 tooblock 存取 toohello 系統磁碟機的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee073-165">Use hello following steps tooblock access toohello system drive:</span></span>

1. <span data-ttu-id="ee073-166">執行**gpedit.msc** hello 範本映像上。</span><span class="sxs-lookup"><span data-stu-id="ee073-166">Run **gpedit.msc** on hello template image.</span></span>
2. <span data-ttu-id="ee073-167">瀏覽過**使用者組態 > 系統管理範本 > Windows 元件 > 總管**。</span><span class="sxs-lookup"><span data-stu-id="ee073-167">Navigate too**User Configuration > Administrative Templates > Windows Components > Explorer**.</span></span>
3. <span data-ttu-id="ee073-168">選取下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee073-168">Select hello following options:</span></span>
   * <span data-ttu-id="ee073-169">**隱藏 [我的電腦] 中這些指定的磁碟機**</span><span class="sxs-lookup"><span data-stu-id="ee073-169">**Hide these specified drives in My Computer**</span></span>
   * <span data-ttu-id="ee073-170">**防止從我的電腦存取 toodrives**</span><span class="sxs-lookup"><span data-stu-id="ee073-170">**Prevent access toodrives from My Computer**</span></span>

## <a name="can-i-seed-upds-i-want-tooput-some-data-in-hello-upd-thats-available-hello-first-time-hello-user-signs-in"></a><span data-ttu-id="ee073-171">我可以植入 UPD 嗎？</span><span class="sxs-lookup"><span data-stu-id="ee073-171">Can I seed UPDs?</span></span> <span data-ttu-id="ee073-172">我想的 tooput hello 是第一個階段 hello 使用者可用的 hello 的 UPD 中的部分資料登入。</span><span class="sxs-lookup"><span data-stu-id="ee073-172">I want tooput some data in hello UPD that's available hello first time hello user signs in.</span></span>
<span data-ttu-id="ee073-173">是，當您建立 hello 範本映像，您可以加入 toohello 預設設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="ee073-173">Yes, when you create hello template image, you can add information toohello default profile.</span></span> <span data-ttu-id="ee073-174">這項資訊接著會加入 toohello UPD。</span><span class="sxs-lookup"><span data-stu-id="ee073-174">That information is then added toohello UPD.</span></span>

## <a name="can-i-change-hello-size-of-hello-upd-depending-on-how-much-data-i-want-toostore"></a><span data-ttu-id="ee073-175">我可以變更 hello UPD hello 大小視資料量而定，我想 toostore 嗎？</span><span class="sxs-lookup"><span data-stu-id="ee073-175">Can I change hello size of hello UPD depending on how much data I want toostore?</span></span>
<span data-ttu-id="ee073-176">否，所有 UPD 都有 50GB 的儲存體。</span><span class="sxs-lookup"><span data-stu-id="ee073-176">No, all UPDs have 50 GB of storage.</span></span> <span data-ttu-id="ee073-177">如果您想 toostore 不同的資料量，請嘗試下列 hello:</span><span class="sxs-lookup"><span data-stu-id="ee073-177">If you want toostore different amounts of data, try hello following:</span></span>

1. <span data-ttu-id="ee073-178">停用 Upd hello 集合。</span><span class="sxs-lookup"><span data-stu-id="ee073-178">Disable UPDs for hello collection.</span></span>
2. <span data-ttu-id="ee073-179">設定使用者 tooaccess 的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="ee073-179">Set up a file share for users tooaccess.</span></span>
3. <span data-ttu-id="ee073-180">使用啟動指令碼的負載 hello 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="ee073-180">Load hello file share by using a startup script.</span></span> <span data-ttu-id="ee073-181">如需 Azure RemoteApp 中啟動指令碼的詳細資訊，請參閱下列內容。</span><span class="sxs-lookup"><span data-stu-id="ee073-181">See below for details on startup scripts in Azure RemoteApp.</span></span>
4. <span data-ttu-id="ee073-182">直接使用者 toosave 所有資料 toohello 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="ee073-182">Direct users toosave all data toohello file share.</span></span>

## <a name="how-do-i-run-a-startup-script-in-azure-remoteapp"></a><span data-ttu-id="ee073-183">如何在 Azure RemoteApp 中執行啟動指令碼？</span><span class="sxs-lookup"><span data-stu-id="ee073-183">How do I run a startup script in Azure RemoteApp?</span></span>
<span data-ttu-id="ee073-184">如果您想 toorun 啟動指令碼時，開始您藉由在 hello 範本映像建立排定的工作將 toouse hello 集合。</span><span class="sxs-lookup"><span data-stu-id="ee073-184">If you want toorun a startup script, start by creating a scheduled task in hello template image you are going toouse for hello collection.</span></span> <span data-ttu-id="ee073-185">(請在執行 sysprep「前」這麼做。)</span><span class="sxs-lookup"><span data-stu-id="ee073-185">(Do this *before* you run sysprep.)</span></span> 

![建立系統工作](./media/remoteapp-upd/upd1.png)

![建立可在使用者登入時執行的系統工作](./media/remoteapp-upd/upd2.png)

<span data-ttu-id="ee073-188">在 [hello**一般**索引標籤上，確定 toochange hello**使用者帳戶**安全性] 之下太"BUILTIN\Users。 」</span><span class="sxs-lookup"><span data-stu-id="ee073-188">On hello **General** tab, be sure toochange hello **User Account** under Security too"BUILTIN\Users."</span></span>

![變更 hello 使用者帳戶 tooa 群組](./media/remoteapp-upd/upd4.png)

<span data-ttu-id="ee073-190">hello 排定的工作將會啟動啟動指令碼，使用 hello 使用者的認證。</span><span class="sxs-lookup"><span data-stu-id="ee073-190">hello scheduled task will launch your startup script, using hello user's credentials.</span></span> <span data-ttu-id="ee073-191">排程 hello 工作 toorun 每次使用者登入。</span><span class="sxs-lookup"><span data-stu-id="ee073-191">Schedule hello task toorun every a time a user logs on.</span></span>

![設定為 在登入 」 的 hello 工作的 hello 觸發程序](./media/remoteapp-upd/upd3.png)

<span data-ttu-id="ee073-193">您也可以使用 [群組原則式啟動指令碼](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ee073-193">You can also use [Group Policy-based startup scripts](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx).</span></span> 

## <a name="what-about-placing-a-startup-script-in-hello-start-menu-would-that-work"></a><span data-ttu-id="ee073-194">如何將啟動指令碼置於 hello 開始功能表？</span><span class="sxs-lookup"><span data-stu-id="ee073-194">What about placing a startup script in hello Start menu?</span></span> <span data-ttu-id="ee073-195">可行嗎？</span><span class="sxs-lookup"><span data-stu-id="ee073-195">Would that work?</span></span>
<span data-ttu-id="ee073-196">換句話說，建立.bat 檔案，執行組態視窗指令碼並將它儲存 toohello c:\ProgramData\Microsoft\Windows\Start 登錄資料夾，和後，每當使用者啟動 RemoteApp 工作階段時執行該指令碼？</span><span class="sxs-lookup"><span data-stu-id="ee073-196">In other words, can I create a .bat file that runs a config window script and save it toohello c:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp folder, and then have that script run whenever a user starts a RemoteApp session?</span></span>

<span data-ttu-id="ee073-197">否，不支援使用 Azure RemoteApp，會使用 RDSH，也不支援啟動指令碼中的 hello [開始] 功能表。</span><span class="sxs-lookup"><span data-stu-id="ee073-197">No, that's not supported with Azure RemoteApp, which uses RDSH, which also does not support startup scripts in hello Start menu.</span></span>

## <a name="can-i-use-mstscexe-hello-remote-desktop-program-tooconfigure-logon-scripts"></a><span data-ttu-id="ee073-198">可以使用 mstsc.exe （hello 遠端桌面程式） tooconfigure 登入指令碼嗎？</span><span class="sxs-lookup"><span data-stu-id="ee073-198">Can I use mstsc.exe (hello Remote Desktop program) tooconfigure logon scripts?</span></span>
<span data-ttu-id="ee073-199">不行，Azure RemoteApp 不支援。</span><span class="sxs-lookup"><span data-stu-id="ee073-199">Nope, not supported by Azure RemoteApp.</span></span>

## <a name="can-i-store-data-on-hello-vm-locally"></a><span data-ttu-id="ee073-200">可以在 hello VM 在本機上儲存資料？</span><span class="sxs-lookup"><span data-stu-id="ee073-200">Can I store data on hello VM locally?</span></span>
<span data-ttu-id="ee073-201">否，儲存在 hello UPD 中的 hello 以外的 VM 上的資料將會遺失。</span><span class="sxs-lookup"><span data-stu-id="ee073-201">NO, data stored anywhere on hello VM other than in hello UPD will be lost.</span></span> <span data-ttu-id="ee073-202">沒有高機率 hello 使用者不會收到 hello 相同 VM hello 他們登入 Azure RemoteApp 的下一次。</span><span class="sxs-lookup"><span data-stu-id="ee073-202">There is a high chance hello user will not get hello same VM hello next time that they sign into Azure RemoteApp.</span></span> <span data-ttu-id="ee073-203">我們不會維護使用者 VM 持續性，因此 hello 使用者將無法登入 hello 相同的 VM 與 hello 資料將遺失。</span><span class="sxs-lookup"><span data-stu-id="ee073-203">We do not maintain user-VM persistence, so hello user will not sign into hello same VM, and hello data will be lost.</span></span> <span data-ttu-id="ee073-204">此外，當我們更新 hello 集合，以一組新的 Vm-這表示任何 hello VM 本身上儲存的資料取代現有的 Vm 的 hello 會遺失。</span><span class="sxs-lookup"><span data-stu-id="ee073-204">Additionally, when we update hello collection, hello existing VMs are replaced with a new set of VMs - that means any data stored on hello VM itself is lost.</span></span> <span data-ttu-id="ee073-205">hello 建議 toostore hello UPD，就像 Azure 檔案，檔案伺服器的內部 VNET，或使用 DropBox 等雲端儲存體系統 hello 雲端上的共用存放裝置中的資料。</span><span class="sxs-lookup"><span data-stu-id="ee073-205">hello recommendation is toostore data in hello UPD, shared storage like Azure Files, a file server inside a VNET, or on hello cloud using a cloud storage system like DropBox.</span></span>

## <a name="how-do-i-mount-an-azure-file-share-on-a-vm-using-powershell"></a><span data-ttu-id="ee073-206">如何使用 PowerShell 在 VM 上掛接 Azure File 共用?</span><span class="sxs-lookup"><span data-stu-id="ee073-206">How do I mount an Azure File share on a VM, using PowerShell?</span></span>
<span data-ttu-id="ee073-207">您可以使用 hello Net PSDrive cmdlet toomount hello 磁碟機，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ee073-207">You can use hello Net-PSDrive cmdlet toomount hello drive, as follows:</span></span>

    New-PSDrive -Name <drive-name> -PSProvider FileSystem -Root \\<storage-account-name>.file.core.windows.net\<share-name> -Credential :<storage-account-name>


<span data-ttu-id="ee073-208">您也可以藉由執行 hello 下列儲存您的認證：</span><span class="sxs-lookup"><span data-stu-id="ee073-208">You can also save your credentials by running hello following:</span></span>

    cmdkey /add:<storage-account-name>.file.core.windows.net /user:<storage-account-name> /pass:<storage-account-key>


<span data-ttu-id="ee073-209">可讓您略過 hello-Credential 參數 hello New-psdrive cmdlet 中的。</span><span class="sxs-lookup"><span data-stu-id="ee073-209">That lets you skip hello -Credential parameter in hello New-PSDrive cmdlet.</span></span>

