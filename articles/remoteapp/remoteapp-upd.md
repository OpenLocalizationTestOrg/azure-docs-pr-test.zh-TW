---
title: "Azure RemoteApp 如何儲存使用者資料和設定？ | Microsoft Docs"
description: "了解 Azure RemoteApp 如何使用使用者設定檔磁碟來儲存使用者資料。"
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
ms.openlocfilehash: 4993bf507536659d7951e1552559cf0a6061d345
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-azure-remoteapp-save-user-data-and-settings"></a><span data-ttu-id="6b12e-104">Azure RemoteApp 如何儲存使用者資料和設定？</span><span class="sxs-lookup"><span data-stu-id="6b12e-104">How does Azure RemoteApp save user data and settings?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6b12e-105">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="6b12e-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6b12e-106">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="6b12e-106">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="6b12e-107">Azure RemoteApp 跨越裝置和工作階段儲存使用者身分識別和自訂。</span><span class="sxs-lookup"><span data-stu-id="6b12e-107">Azure RemoteApp saves user identity and customizations across devices and sessions.</span></span> <span data-ttu-id="6b12e-108">此使用者資料會依每個使用者和每個集合磁碟 (也稱為使用者設定檔磁碟 (UPD)) 儲存。</span><span class="sxs-lookup"><span data-stu-id="6b12e-108">This user data is stored in a per-user per-collection disk, known as a user profile disk (UPD).</span></span> <span data-ttu-id="6b12e-109">不論使用者登入的位置為何，此磁碟都會追蹤使用者並確保使用者擁有一致的經驗。</span><span class="sxs-lookup"><span data-stu-id="6b12e-109">The disk follows the user and ensures the user has a consistent experience, regardless of where they sign in.</span></span>

<span data-ttu-id="6b12e-110">對使用者而言，使用者設定檔磁碟是完全透明的 — 使用者會將文件儲存至其 Documents 資料夾 (似乎是本機磁碟機) 並如往常般變更其應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="6b12e-110">User profile disks are completely transparent to the user — users save documents to their Documents folder (on what appears to be a local drive) and change their app settings as usual.</span></span> <span data-ttu-id="6b12e-111">同時，從任何裝置連線到 Azure RemoteApp 時會保存所有的個人設定。</span><span class="sxs-lookup"><span data-stu-id="6b12e-111">At the same time, all personal settings persist when connecting to Azure RemoteApp from any device.</span></span> <span data-ttu-id="6b12e-112">使用者會在相同的位置看到其資料。</span><span class="sxs-lookup"><span data-stu-id="6b12e-112">All the user sees is their data in the same place.</span></span>

<span data-ttu-id="6b12e-113">每個 UPD 有 50GB 的永續性儲存體，並包含使用者資料和應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="6b12e-113">Each UPD has 50GB of persistent storage and contains both user data and application settings.</span></span> 

<span data-ttu-id="6b12e-114">請閱讀更多有關使用者設定檔資料的特殊資訊。</span><span class="sxs-lookup"><span data-stu-id="6b12e-114">Read on for specifics on user profile data.</span></span>

> [!NOTE]
> <span data-ttu-id="6b12e-115">必須停用 UPD 嗎？</span><span class="sxs-lookup"><span data-stu-id="6b12e-115">Need to disable the UPD?</span></span> <span data-ttu-id="6b12e-116">現在您可以那麼做了 - 詳細資料請查看 Pavithra 的部落格文章： [在 Azure RemoteApp 停用使用者設定檔磁碟 (UPD)](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/)(英文)。</span><span class="sxs-lookup"><span data-stu-id="6b12e-116">You can do that now - check out Pavithra's blog post, [Disable User Profile Disks (UPDs) in Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/), for details.</span></span>
> 
> 

## <a name="how-can-an-admin-get-to-the-data"></a><span data-ttu-id="6b12e-117">系統管理員如何取得資料？</span><span class="sxs-lookup"><span data-stu-id="6b12e-117">How can an admin get to the data?</span></span>
<span data-ttu-id="6b12e-118">如果您需要存取您其中一個使用者的資料 (為了災害復原或如果使用者離開公司)，請連絡 Azure 支援服務並提供集合和使用者身分識別的訂用帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="6b12e-118">If you need to access the data for one of your users (for disaster recovery or if the user leaves the company), contact Azure Support and provide the subscription information for the collection and the user identity.</span></span> <span data-ttu-id="6b12e-119">Azure RemoteApp 小組會為您提供 VHD 的 URL。</span><span class="sxs-lookup"><span data-stu-id="6b12e-119">The Azure RemoteApp team will provide you a URL to the VHD.</span></span> <span data-ttu-id="6b12e-120">請下載該 VHD，並擷取您需要的任何文件或檔案。</span><span class="sxs-lookup"><span data-stu-id="6b12e-120">Download that VHD and retrieve any documents or files you need.</span></span> <span data-ttu-id="6b12e-121">請注意，VHD 為 50 GB，因此下載需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="6b12e-121">Note that the VHD is 50GB, so it will take a bit to download it.</span></span>

## <a name="is-the-data-backed-up"></a><span data-ttu-id="6b12e-122">已備份資料嗎？</span><span class="sxs-lookup"><span data-stu-id="6b12e-122">Is the data backed up?</span></span>
<span data-ttu-id="6b12e-123">是，我們依據每個地理位置儲存使用者資料的備份。</span><span class="sxs-lookup"><span data-stu-id="6b12e-123">Yes, we save a backup of the user data per geographic location.</span></span> <span data-ttu-id="6b12e-124">如果主要資料中心已關閉，則資料是唯讀的並可用與存取一般資料相同的方式存取 (連絡 Azure RemoteApp 以取得)。</span><span class="sxs-lookup"><span data-stu-id="6b12e-124">The data is read-only and can be accessed in the same way as the regular data would be (contact Azure RemoteApp to get it), if the primary data center is down.</span></span> <span data-ttu-id="6b12e-125">資料會即時複製到備份位置，而且我們不需要保留不同版本的複本。</span><span class="sxs-lookup"><span data-stu-id="6b12e-125">The data is copied real-time to the backup location and we do not keep copies of different versions.</span></span> <span data-ttu-id="6b12e-126">因此，在資料損毀的情況下，我們不能將它還原到上次已知正確的版本，但如果主要資料中心不能使用時，您將能夠從其他位置取得使用者資料。</span><span class="sxs-lookup"><span data-stu-id="6b12e-126">So, on data corruption, we will not be able to restore it to a previously known good version but if the primary data center is down, you will be able to get user data from the other location.</span></span>

## <a name="how-do-users-see-the-upd-on-the-server-side"></a><span data-ttu-id="6b12e-127">使用者如何在伺服器端查看 UPD？</span><span class="sxs-lookup"><span data-stu-id="6b12e-127">How do users see the UPD on the server side?</span></span>
<span data-ttu-id="6b12e-128">每位使用者在伺服器上都有對應至其 UPD 的專屬目錄：c:\Users\username。</span><span class="sxs-lookup"><span data-stu-id="6b12e-128">Each user will have their own directory on the server that maps to their UPD: c:\Users\username.</span></span>

## <a name="whats-the-best-way-to-use-outlook-and-upd"></a><span data-ttu-id="6b12e-129">使用 Outlook 和 UPD 的最佳方式為何？</span><span class="sxs-lookup"><span data-stu-id="6b12e-129">What's the best way to use Outlook and UPD?</span></span>
<span data-ttu-id="6b12e-130">Azure RemoteApp 會儲存工作階段間的 Outlook 狀態 (信箱、PST)。</span><span class="sxs-lookup"><span data-stu-id="6b12e-130">Azure RemoteApp saves the Outlook state (mailboxes, PSTs) between sessions.</span></span> <span data-ttu-id="6b12e-131">若要啟用此功能，我們需要將 PST 儲存在使用者設定檔資料 (c:\users\<username>) 中。</span><span class="sxs-lookup"><span data-stu-id="6b12e-131">To enable this, we need the PST to be stored in the user profile data (c:\users\<username>).</span></span> <span data-ttu-id="6b12e-132">這是資料的預設位置，只要您不變更位置，資料將會在工作階段之間保存。</span><span class="sxs-lookup"><span data-stu-id="6b12e-132">This is the default location for the data, so as long as you do not change the location, the data will persist between sessions.</span></span>

<span data-ttu-id="6b12e-133">我們也建議您在 Outlook 中使用「快取」模式，並使用「伺服器/線上」模式進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="6b12e-133">We also recommend that you use "cached" mode in Outlook and use "server/online" mode for searching.</span></span>

<span data-ttu-id="6b12e-134">如需使用 Outlook 和 Azure RemoteApp 的詳細資訊，請查看 [這篇文章](remoteapp-outlook.md) 。</span><span class="sxs-lookup"><span data-stu-id="6b12e-134">Check out [this article](remoteapp-outlook.md) for more information on using Outlook and Azure RemoteApp.</span></span>

## <a name="what-about-redirection"></a><span data-ttu-id="6b12e-135">重新導向呢？</span><span class="sxs-lookup"><span data-stu-id="6b12e-135">What about redirection?</span></span>
<span data-ttu-id="6b12e-136">您可以設定 Azure RemoteApp，讓使用者藉由設定 [重新導向](remoteapp-redirection.md)來存取本機裝置。</span><span class="sxs-lookup"><span data-stu-id="6b12e-136">You can configure Azure RemoteApp to let users access local devices by setting up [redirection](remoteapp-redirection.md).</span></span> <span data-ttu-id="6b12e-137">然後本機裝置即可存取 UPD 上的資料。</span><span class="sxs-lookup"><span data-stu-id="6b12e-137">Local devices will then be able to access the data on the UPD.</span></span>

## <a name="can-i-use-my-upd-as-a-network-share"></a><span data-ttu-id="6b12e-138">我可以使用 UPD 做為網路共用嗎？</span><span class="sxs-lookup"><span data-stu-id="6b12e-138">Can I use my UPD as a network share?</span></span>
<span data-ttu-id="6b12e-139">不用。</span><span class="sxs-lookup"><span data-stu-id="6b12e-139">No.</span></span> <span data-ttu-id="6b12e-140">UPD 不能做為網路共用。</span><span class="sxs-lookup"><span data-stu-id="6b12e-140">UPDs cannot be used as a network share.</span></span> <span data-ttu-id="6b12e-141">UPD 僅適用於使用者主動連線到 Azure RemoteApp 時。</span><span class="sxs-lookup"><span data-stu-id="6b12e-141">A UPD is only available to the user when the user is actively connected to Azure RemoteApp.</span></span>

## <a name="if-i-delete-a-user-from-a-collection-is-their-upd-deleted"></a><span data-ttu-id="6b12e-142">如果我從集合中刪除使用者，其 UPD 是否也會刪除?</span><span class="sxs-lookup"><span data-stu-id="6b12e-142">If I delete a user from a collection, is their UPD deleted?</span></span>
<span data-ttu-id="6b12e-143">否，當您刪除使用者時，我們不會自動刪除 UPD - 相反地，我們會儲存資料，直到您刪除集合為止。</span><span class="sxs-lookup"><span data-stu-id="6b12e-143">No, when you delete a user, we do not automatically delete the UPD - instead, we store the data until you delete the collection.</span></span> <span data-ttu-id="6b12e-144">刪除集合後 90 天，我們才會刪除所有 UPD。</span><span class="sxs-lookup"><span data-stu-id="6b12e-144">90 days after you delete the collection, we delete all UPDs.</span></span> 

<span data-ttu-id="6b12e-145">如果您需要從集合中刪除 UPD，請連絡 Azure RemoteApp - 我們可以從我們這端刪除 UPD。</span><span class="sxs-lookup"><span data-stu-id="6b12e-145">If you need to delete a UPD from a collection, contact Azure RemoteApp - we can delete UPD from our side.</span></span>

## <a name="can-i-access-my-users-upds-either-current-or-deleted-users"></a><span data-ttu-id="6b12e-146">我可以存取使用者的 UPD (目前或已刪除的使用者) 嗎？</span><span class="sxs-lookup"><span data-stu-id="6b12e-146">Can I access my users' UPDs (either current or deleted users)?</span></span>
<span data-ttu-id="6b12e-147">可以，如果您連絡 [Azure RemoteApp](mailto:remoteappforum@microsoft.com)，我們可以為您設定一個 URL 以存取資料。</span><span class="sxs-lookup"><span data-stu-id="6b12e-147">Yes, if you contact [Azure RemoteApp](mailto:remoteappforum@microsoft.com), we can set you up with a URL to access the data.</span></span> <span data-ttu-id="6b12e-148">在存取到期前，您將有大約 10 小時的時間可從 UPD 下載任何資料或檔案。</span><span class="sxs-lookup"><span data-stu-id="6b12e-148">You'll have about 10 hours to download any data or files from the UPD before the access expires.</span></span>

## <a name="are-upds-available-offline"></a><span data-ttu-id="6b12e-149">UPD 可離線使用嗎？</span><span class="sxs-lookup"><span data-stu-id="6b12e-149">Are UPDs available offline?</span></span>
<span data-ttu-id="6b12e-150">除了上述 10 小時的存取時段以外，我們現在並不提供 UPD 的離線存取。</span><span class="sxs-lookup"><span data-stu-id="6b12e-150">Right now we do not provide offline access to UPDs, beyond the 10 hour access window described above.</span></span> <span data-ttu-id="6b12e-151">這表示我們目前沒辦法讓您長時間存取以完成更複雜的工作，像是在 UPD 上執行防毒軟體或存取資料進行稽核。</span><span class="sxs-lookup"><span data-stu-id="6b12e-151">This means that we do not currently have a way to provide you with access for long enough to complete more complicated tasks, like running anti-virus software on the UPDs or accessing data for an audit.</span></span>

## <a name="do-registry-key-settings-persist"></a><span data-ttu-id="6b12e-152">登錄機碼設定可以保存嗎？</span><span class="sxs-lookup"><span data-stu-id="6b12e-152">Do registry key settings persist?</span></span>
<span data-ttu-id="6b12e-153">可以，寫入 HKEY_Current_User 的任何項目都是 UPD 的一部分。</span><span class="sxs-lookup"><span data-stu-id="6b12e-153">Yes, anything written to HKEY_Current_User is part of the UPD.</span></span>

## <a name="can-i-disable-upds-for-a-collection"></a><span data-ttu-id="6b12e-154">我可以停用 集合的 UPD 嗎？</span><span class="sxs-lookup"><span data-stu-id="6b12e-154">Can I disable UPDs for a collection?</span></span>
<span data-ttu-id="6b12e-155">可以，您可以要求 Azure RemoteApp 停用訂用帳戶的 UPD，但無法自己執行該作業。</span><span class="sxs-lookup"><span data-stu-id="6b12e-155">Yes, you can ask Azure RemoteApp to disable UPDs for a subscription, but you cannot do that yourself.</span></span> <span data-ttu-id="6b12e-156">這表示將會針對訂用帳戶中的所有集合停用 UPD。</span><span class="sxs-lookup"><span data-stu-id="6b12e-156">This means that UPDs will be disabled for all collections in the subscription.</span></span>

<span data-ttu-id="6b12e-157">遇到下列情況時，建議您停用 UPD：</span><span class="sxs-lookup"><span data-stu-id="6b12e-157">You might want to disable UPDs in any of the following situations:</span></span> 

* <span data-ttu-id="6b12e-158">您需要使用者資料的完整存取權限和控制 (針對稽核和檢閱之目的，例如金融機構)。</span><span class="sxs-lookup"><span data-stu-id="6b12e-158">You need complete access and control of user data (for audit and review purposes such as financial institutions).</span></span>
* <span data-ttu-id="6b12e-159">您有內部部署的第三方使用者設定檔管理解決方案，並想要加入網域的 Azure RemoteApp 部署繼續使用它們。</span><span class="sxs-lookup"><span data-stu-id="6b12e-159">You have 3rd-party user profile management solutions on-premises and want to continue using them in your domain-joined Azure RemoteApp deployment.</span></span> <span data-ttu-id="6b12e-160">這會需要將設定檔代理程式載入主要映像。</span><span class="sxs-lookup"><span data-stu-id="6b12e-160">This would require the profile agent to be loaded into the gold image.</span></span> 
* <span data-ttu-id="6b12e-161">您不需要任何本機資料儲存空間，或者您的所有資料都在雲端或檔案共用，並且想要使用 Azure RemoteApp 控制在本機的檔案儲存。</span><span class="sxs-lookup"><span data-stu-id="6b12e-161">You don’t need any local data storage or you have all data in the cloud or file share and would like to control saving of data locally using Azure RemoteApp.</span></span>

<span data-ttu-id="6b12e-162">如需詳細資訊，請參閱[在 Azure RemoteApp 停用使用者設定檔磁碟 (UPD)](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/) (英文)。</span><span class="sxs-lookup"><span data-stu-id="6b12e-162">See  [Disable User Profile Disks (UPDs) in Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/) for more information.</span></span>

## <a name="can-i-restrict-users-from-saving-data-to-the-system-drive"></a><span data-ttu-id="6b12e-163">我可以限制使用者不要將資料儲存到系統磁碟機嗎？</span><span class="sxs-lookup"><span data-stu-id="6b12e-163">Can I restrict users from saving data to the system drive?</span></span>
<span data-ttu-id="6b12e-164">可以，但您必須在建立集合之前，在範本映像中加以設定。</span><span class="sxs-lookup"><span data-stu-id="6b12e-164">Yes, but you'll need to set that up in the template image before you create the collection.</span></span> <span data-ttu-id="6b12e-165">使用下列步驟來封鎖系統磁碟機的存取：</span><span class="sxs-lookup"><span data-stu-id="6b12e-165">Use the following steps to block access to the system drive:</span></span>

1. <span data-ttu-id="6b12e-166">在範本映像上執行 **gpedit.msc** 。</span><span class="sxs-lookup"><span data-stu-id="6b12e-166">Run **gpedit.msc** on the template image.</span></span>
2. <span data-ttu-id="6b12e-167">瀏覽至 [使用者設定] > [系統管理範本] > [Windows 元件] > [Explorer]。</span><span class="sxs-lookup"><span data-stu-id="6b12e-167">Navigate to **User Configuration > Administrative Templates > Windows Components > Explorer**.</span></span>
3. <span data-ttu-id="6b12e-168">選取下列選項：</span><span class="sxs-lookup"><span data-stu-id="6b12e-168">Select the following options:</span></span>
   * <span data-ttu-id="6b12e-169">**隱藏 [我的電腦] 中這些指定的磁碟機**</span><span class="sxs-lookup"><span data-stu-id="6b12e-169">**Hide these specified drives in My Computer**</span></span>
   * <span data-ttu-id="6b12e-170">**防止從 [我的電腦] 存取磁碟機**</span><span class="sxs-lookup"><span data-stu-id="6b12e-170">**Prevent access to drives from My Computer**</span></span>

## <a name="can-i-seed-upds-i-want-to-put-some-data-in-the-upd-thats-available-the-first-time-the-user-signs-in"></a><span data-ttu-id="6b12e-171">我可以植入 UPD 嗎？</span><span class="sxs-lookup"><span data-stu-id="6b12e-171">Can I seed UPDs?</span></span> <span data-ttu-id="6b12e-172">我想要在使用者第一次登入時可用的 UPD 中放入一些資料。</span><span class="sxs-lookup"><span data-stu-id="6b12e-172">I want to put some data in the UPD that's available the first time the user signs in.</span></span>
<span data-ttu-id="6b12e-173">是，當您建立範本映像時，您可以將資訊加入至預設設定檔。</span><span class="sxs-lookup"><span data-stu-id="6b12e-173">Yes, when you create the template image, you can add information to the default profile.</span></span> <span data-ttu-id="6b12e-174">這項資訊會接著加入至 UPD。</span><span class="sxs-lookup"><span data-stu-id="6b12e-174">That information is then added to the UPD.</span></span>

## <a name="can-i-change-the-size-of-the-upd-depending-on-how-much-data-i-want-to-store"></a><span data-ttu-id="6b12e-175">我可以根據想要儲存的資料量來變更 UPD 的大小嗎？</span><span class="sxs-lookup"><span data-stu-id="6b12e-175">Can I change the size of the UPD depending on how much data I want to store?</span></span>
<span data-ttu-id="6b12e-176">否，所有 UPD 都有 50GB 的儲存體。</span><span class="sxs-lookup"><span data-stu-id="6b12e-176">No, all UPDs have 50 GB of storage.</span></span> <span data-ttu-id="6b12e-177">如果您想要儲存不同的資料量，請嘗試下列方法：</span><span class="sxs-lookup"><span data-stu-id="6b12e-177">If you want to store different amounts of data, try the following:</span></span>

1. <span data-ttu-id="6b12e-178">停用集合的 UPD。</span><span class="sxs-lookup"><span data-stu-id="6b12e-178">Disable UPDs for the collection.</span></span>
2. <span data-ttu-id="6b12e-179">設定檔案共用以供使用者存取。</span><span class="sxs-lookup"><span data-stu-id="6b12e-179">Set up a file share for users to access.</span></span>
3. <span data-ttu-id="6b12e-180">使用啟動指令碼來載入檔案共用。</span><span class="sxs-lookup"><span data-stu-id="6b12e-180">Load the file share by using a startup script.</span></span> <span data-ttu-id="6b12e-181">如需 Azure RemoteApp 中啟動指令碼的詳細資訊，請參閱下列內容。</span><span class="sxs-lookup"><span data-stu-id="6b12e-181">See below for details on startup scripts in Azure RemoteApp.</span></span>
4. <span data-ttu-id="6b12e-182">引導使用者將所有資料儲存至檔案共用。</span><span class="sxs-lookup"><span data-stu-id="6b12e-182">Direct users to save all data to the file share.</span></span>

## <a name="how-do-i-run-a-startup-script-in-azure-remoteapp"></a><span data-ttu-id="6b12e-183">如何在 Azure RemoteApp 中執行啟動指令碼？</span><span class="sxs-lookup"><span data-stu-id="6b12e-183">How do I run a startup script in Azure RemoteApp?</span></span>
<span data-ttu-id="6b12e-184">如果您想要執行啟動指令碼，請從在您即將用於收集的範本映像中建立排定的工作著手。</span><span class="sxs-lookup"><span data-stu-id="6b12e-184">If you want to run a startup script, start by creating a scheduled task in the template image you are going to use for the collection.</span></span> <span data-ttu-id="6b12e-185">(請在執行 sysprep「前」這麼做。)</span><span class="sxs-lookup"><span data-stu-id="6b12e-185">(Do this *before* you run sysprep.)</span></span> 

![建立系統工作](./media/remoteapp-upd/upd1.png)

![建立可在使用者登入時執行的系統工作](./media/remoteapp-upd/upd2.png)

<span data-ttu-id="6b12e-188">在 [一般] 索引標籤上，務必將 [安全性] 底下的 [使用者帳戶] 變更為 BUILTIN\Users。</span><span class="sxs-lookup"><span data-stu-id="6b12e-188">On the **General** tab, be sure to change the **User Account** under Security to "BUILTIN\Users."</span></span>

![變更使用者帳戶為群組](./media/remoteapp-upd/upd4.png)

<span data-ttu-id="6b12e-190">排定的工作將會使用使用者的認證，啟動您的啟動指令碼。</span><span class="sxs-lookup"><span data-stu-id="6b12e-190">The scheduled task will launch your startup script, using the user's credentials.</span></span> <span data-ttu-id="6b12e-191">將此工作安排在使用者每次登入時執行。</span><span class="sxs-lookup"><span data-stu-id="6b12e-191">Schedule the task to run every a time a user logs on.</span></span>

![將工作的觸發程序設定為「登入時」](./media/remoteapp-upd/upd3.png)

<span data-ttu-id="6b12e-193">您也可以使用 [群組原則式啟動指令碼](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6b12e-193">You can also use [Group Policy-based startup scripts](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx).</span></span> 

## <a name="what-about-placing-a-startup-script-in-the-start-menu-would-that-work"></a><span data-ttu-id="6b12e-194">將啟動指令碼置於 [開始] 功能表？</span><span class="sxs-lookup"><span data-stu-id="6b12e-194">What about placing a startup script in the Start menu?</span></span> <span data-ttu-id="6b12e-195">可行嗎？</span><span class="sxs-lookup"><span data-stu-id="6b12e-195">Would that work?</span></span>
<span data-ttu-id="6b12e-196">換句話說，我可以建立一個可執行 config 視窗指令碼的 .bat 檔並將它儲存至 c:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp 資料夾，然後讓該指令碼在使用者每次啟動 RemoteApp 工作階段時執行嗎？</span><span class="sxs-lookup"><span data-stu-id="6b12e-196">In other words, can I create a .bat file that runs a config window script and save it to the c:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp folder, and then have that script run whenever a user starts a RemoteApp session?</span></span>

<span data-ttu-id="6b12e-197">不行，Azure RemoteApp 不支援，會使用 RDSH，也不支援 [開始] 功能表中的啟動指令碼。</span><span class="sxs-lookup"><span data-stu-id="6b12e-197">No, that's not supported with Azure RemoteApp, which uses RDSH, which also does not support startup scripts in the Start menu.</span></span>

## <a name="can-i-use-mstscexe-the-remote-desktop-program-to-configure-logon-scripts"></a><span data-ttu-id="6b12e-198">我可以使用 mstsc.exe (遠端桌面程式) 來設定登入指令碼嗎？</span><span class="sxs-lookup"><span data-stu-id="6b12e-198">Can I use mstsc.exe (the Remote Desktop program) to configure logon scripts?</span></span>
<span data-ttu-id="6b12e-199">不行，Azure RemoteApp 不支援。</span><span class="sxs-lookup"><span data-stu-id="6b12e-199">Nope, not supported by Azure RemoteApp.</span></span>

## <a name="can-i-store-data-on-the-vm-locally"></a><span data-ttu-id="6b12e-200">可以在 VM 本機儲存資料嗎?</span><span class="sxs-lookup"><span data-stu-id="6b12e-200">Can I store data on the VM locally?</span></span>
<span data-ttu-id="6b12e-201">否，資料若不儲存在 UPD 而儲存在 VM 上的任何地方，資料將會遺失。</span><span class="sxs-lookup"><span data-stu-id="6b12e-201">NO, data stored anywhere on the VM other than in the UPD will be lost.</span></span> <span data-ttu-id="6b12e-202">使用者下次登入 Azure RemoteApp 時不會得到同一 VM 的可能性很高。</span><span class="sxs-lookup"><span data-stu-id="6b12e-202">There is a high chance the user will not get the same VM the next time that they sign into Azure RemoteApp.</span></span> <span data-ttu-id="6b12e-203">我們不會維護「使用者-VM」持續性，因此使用者無法登入相同的 VM，故資料會遺失。</span><span class="sxs-lookup"><span data-stu-id="6b12e-203">We do not maintain user-VM persistence, so the user will not sign into the same VM, and the data will be lost.</span></span> <span data-ttu-id="6b12e-204">此外，當我們更新集合時，現有 VM 會被一組新的 VM 取代 - 這表示儲存在 VM 本身的所有資料都會遺失。</span><span class="sxs-lookup"><span data-stu-id="6b12e-204">Additionally, when we update the collection, the existing VMs are replaced with a new set of VMs - that means any data stored on the VM itself is lost.</span></span> <span data-ttu-id="6b12e-205">建議將資料儲存在 UPD、共用儲存體 (如 Azure Files)、VNET 內部的檔案伺服器，或儲存在使用雲端儲存體系統 (如 DropBox) 的雲端上。</span><span class="sxs-lookup"><span data-stu-id="6b12e-205">The recommendation is to store data in the UPD, shared storage like Azure Files, a file server inside a VNET, or on the cloud using a cloud storage system like DropBox.</span></span>

## <a name="how-do-i-mount-an-azure-file-share-on-a-vm-using-powershell"></a><span data-ttu-id="6b12e-206">如何使用 PowerShell 在 VM 上掛接 Azure File 共用?</span><span class="sxs-lookup"><span data-stu-id="6b12e-206">How do I mount an Azure File share on a VM, using PowerShell?</span></span>
<span data-ttu-id="6b12e-207">您可以使用 New-PSDrive Cmdlet 來掛接磁碟機，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="6b12e-207">You can use the Net-PSDrive cmdlet to mount the drive, as follows:</span></span>

    New-PSDrive -Name <drive-name> -PSProvider FileSystem -Root \\<storage-account-name>.file.core.windows.net\<share-name> -Credential :<storage-account-name>


<span data-ttu-id="6b12e-208">您也可以執行下列命令儲存您的認證︰</span><span class="sxs-lookup"><span data-stu-id="6b12e-208">You can also save your credentials by running the following:</span></span>

    cmdkey /add:<storage-account-name>.file.core.windows.net /user:<storage-account-name> /pass:<storage-account-key>


<span data-ttu-id="6b12e-209">這可讓您略過 New-PSDrive Cmdlet 中的 -Credential 參數。</span><span class="sxs-lookup"><span data-stu-id="6b12e-209">That lets you skip the -Credential parameter in the New-PSDrive cmdlet.</span></span>

