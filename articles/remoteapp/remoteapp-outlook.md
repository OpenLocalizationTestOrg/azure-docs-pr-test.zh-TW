---
title: "Azure RemoteApp 中 Outlook aaaUsing |Microsoft 文件"
description: "深入了解如何 tooconfigure 和 Azure RemoteApp 中使用的 Outlook |Microsoft Azure"
services: remoteapp
documentationcenter: 
author: pavithir
manager: mbaldwin
ms.assetid: cb2a498f-9539-4522-a874-542114926a61
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 119d2629ac47bd8d20d617985a9b488068aa959f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-microsoft-outlook-in-azure-remoteapp"></a><span data-ttu-id="7973e-103">在 Azure RemoteApp 中使用 Microsoft Outlook</span><span class="sxs-lookup"><span data-stu-id="7973e-103">Using Microsoft Outlook in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7973e-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="7973e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7973e-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7973e-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="7973e-106">Azure RemoteApp 支援 Microsoft Outlook O365。</span><span class="sxs-lookup"><span data-stu-id="7973e-106">Azure RemoteApp supports Microsoft Outlook O365.</span></span> <span data-ttu-id="7973e-107">深入了解 [Office 在 Azure RemoteApp 中運作](remoteapp-officesubscription.md)的方式。</span><span class="sxs-lookup"><span data-stu-id="7973e-107">Read more about how [Office works in Azure RemoteApp](remoteapp-officesubscription.md).</span></span> <span data-ttu-id="7973e-108">在 Azure RemoteApp 中使用 Outlook 時，有幾個建議的設定。</span><span class="sxs-lookup"><span data-stu-id="7973e-108">There are a few recommended settings for Outlook when used in Azure RemoteApp.</span></span>

## <a name="cached-mode"></a><span data-ttu-id="7973e-109">快取模式</span><span class="sxs-lookup"><span data-stu-id="7973e-109">Cached mode</span></span>
<span data-ttu-id="7973e-110">在 Azure RemoteApp 中使用 Outlook 時，快取模式是建議的組態。</span><span class="sxs-lookup"><span data-stu-id="7973e-110">Cached mode is a recommended configuration when using Outlook in Azure RemoteApp.</span></span> <span data-ttu-id="7973e-111">當您設定 Outlook 2013 帳戶 toouse 快取 Exchange 模式，Outlook 2013 運作方式與 hello 使用者的 Microsoft Exchange 信箱 hello 使用者在電腦上，搭配 hello 離線通訊錄的離線資料檔案 （OST 檔案） 中所儲存的本機複本(OAB)。</span><span class="sxs-lookup"><span data-stu-id="7973e-111">When you configure an Outlook 2013 account toouse Cached Exchange Mode, Outlook 2013 works from a local copy of hello user's Microsoft Exchange mailbox that is stored in an offline data file (OST file) on hello user's computer, together with hello Offline Address Book (OAB).</span></span> <span data-ttu-id="7973e-112">hello 快取的信箱和 OAB 會定期更新從 hello O365 服務。</span><span class="sxs-lookup"><span data-stu-id="7973e-112">hello cached mailbox and OAB are updated periodically from hello O365 service.</span></span> <span data-ttu-id="7973e-113">深入了解[hello 快取和線上模式之間的差異](https://technet.microsoft.com/library/jj683103.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7973e-113">Read more about [hello differences between cached and online mode](https://technet.microsoft.com/library/jj683103.aspx).</span></span>

<span data-ttu-id="7973e-114">hello 使用者可以選取**快取 Exchange 模式**或**線上模式**帳戶安裝期間或藉由變更 hello 帳戶設定。</span><span class="sxs-lookup"><span data-stu-id="7973e-114">hello user can select **Cached Exchange Mode** or **Online Mode** during account setup or by changing hello account settings.</span></span> <span data-ttu-id="7973e-115">您也可以部署一個模式或其他 hello 使用 hello Office 自訂工具 （10 月） 或群組原則。</span><span class="sxs-lookup"><span data-stu-id="7973e-115">You can also deploy one mode or hello other by using hello Office Customization Tool (OCT) or Group Policy.</span></span>  

<span data-ttu-id="7973e-116">閱讀 [啟用快取模式的逐步指示](https://technet.microsoft.com/library/c6f4cad9-c918-420e-bab3-8b49e1885034#proc)。</span><span class="sxs-lookup"><span data-stu-id="7973e-116">Read [step by step instructions on enabling cached mode](https://technet.microsoft.com/library/c6f4cad9-c918-420e-bab3-8b49e1885034#proc).</span></span>

## <a name="search"></a><span data-ttu-id="7973e-117">搜尋</span><span class="sxs-lookup"><span data-stu-id="7973e-117">Search</span></span>
<span data-ttu-id="7973e-118">在 Azure RemoteApp 中，使用 Outlook 中的搜尋有限制。</span><span class="sxs-lookup"><span data-stu-id="7973e-118">In Azure RemoteApp, using search within Outlook has limitations.</span></span> <span data-ttu-id="7973e-119">Azure RemoteApp 使用管理的集區的 Vm tooaccommodate 使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="7973e-119">Azure RemoteApp uses pooled VMs tooaccommodate user sessions.</span></span> <span data-ttu-id="7973e-120">搜尋索引相依於 hello 機器識別碼不同，不同的 Vm。</span><span class="sxs-lookup"><span data-stu-id="7973e-120">Search indexing depends on hello machine ID, which is different for different VMs.</span></span> <span data-ttu-id="7973e-121">很可能在每次使用者登入 Azure RemoteApp，它們會導向的 tooa 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="7973e-121">It is possible that every time a user logs into Azure RemoteApp, they are directed tooa new VM.</span></span> <span data-ttu-id="7973e-122">這表示，每次 hello 機器 ID 就會變更 （當 hello 使用者在不同的 VM 上），如果我們啟用當地搜尋，會執行 hello 索引子。</span><span class="sxs-lookup"><span data-stu-id="7973e-122">That would mean, if we enable local search, hello indexer will run every time hello machine ID changes (when hello user is on a different VM).</span></span> <span data-ttu-id="7973e-123">根據 hello hello 大小。OST 檔案 hello 索引子可能需要很長的時間 toocomplete，並使用資源所需的其他應用程式。</span><span class="sxs-lookup"><span data-stu-id="7973e-123">Depending on hello size of hello .OST file, hello indexer could take a long time toocomplete and use up resources needed for other apps.</span></span> <span data-ttu-id="7973e-124">搜尋不只很慢，而且可能不會產生結果。</span><span class="sxs-lookup"><span data-stu-id="7973e-124">Search would not only be slow but might not produce results.</span></span> <span data-ttu-id="7973e-125">使用線上模式帳戶設定檔會解決這個問題，但因為 toohello 缺乏本機快取，則會犧牲整體效能 （請參閱上方連結，如需有關快取和線上模式的 hello 差異 hello）。</span><span class="sxs-lookup"><span data-stu-id="7973e-125">Using an Online Mode account profile would work around this, but overall performance would suffer due toohello lack of a local cache (see hello link above for more information about hello difference between cached and online mode).</span></span> <span data-ttu-id="7973e-126">不幸的是，在 Outlook 2013 中無法停用已編製索引/本機搜尋，且預設無法啟用線上搜尋。</span><span class="sxs-lookup"><span data-stu-id="7973e-126">Unfortunately, indexed/local search cannot be disabled and online search cannot be enabled by default in Outlook 2013.</span></span>

