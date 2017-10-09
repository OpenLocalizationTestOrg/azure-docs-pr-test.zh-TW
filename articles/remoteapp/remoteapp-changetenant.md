---
title: "在 Azure RemoteApp aaaChange hello Azure Active Directory 租用戶 |Microsoft 文件"
description: "了解 toochange hello Azure Active Directory 租用戶與 Azure RemoteApp 的相關聯"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 20faf169-6e48-428a-8bdd-f231daff19fa
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d0928b099b7fcfb3ab16077e295d7aaf519c3653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-azure-active-directory-tenant-in-azure-remoteapp"></a><span data-ttu-id="87eb9-103">變更 Azure RemoteApp 中的 hello Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="87eb9-103">Change hello Azure Active Directory tenant in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="87eb9-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="87eb9-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="87eb9-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="87eb9-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="87eb9-106">Azure RemoteApp 使用 Azure Active Directory (Azure AD) tooallow 使用者存取權。</span><span class="sxs-lookup"><span data-stu-id="87eb9-106">Azure RemoteApp uses Azure Active Directory (Azure AD) tooallow user access.</span></span> <span data-ttu-id="87eb9-107">您可以使用 Azure RemoteApp 中的 hello 只有 Azure AD 租用戶為 hello 與 hello Azure 訂用帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="87eb9-107">hello only Azure AD tenant that you can use in Azure RemoteApp is hello one associated with hello Azure subscription.</span></span> <span data-ttu-id="87eb9-108">您可以檢視相關聯的 hello 訂用帳戶上 hello**設定**hello 入口網站頁面中的。</span><span class="sxs-lookup"><span data-stu-id="87eb9-108">You can view hello associated subscription on hello **Settings** page in hello portal.</span></span> <span data-ttu-id="87eb9-109">查看 hello**目錄**hello 上的資料行**訂閱** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="87eb9-109">Look at hello **Directory** column on hello **Subscriptions** tab.</span></span>

> [!NOTE]
> <span data-ttu-id="87eb9-110">此變更 toosucceed，如先移除 hello 現有 Azure Active Directory 租用戶中所有的 Azure RemoteApp 集合的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="87eb9-110">For this change toosucceed, first remove all users from hello existing Azure Active Directory tenant from all Azure RemoteApp collections.</span></span> <span data-ttu-id="87eb9-111">toodo 這個，請移 toohello Azure 入口網站中，移 toohello **Azure RemoteApp**索引標籤上，開啟每個 Azure RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="87eb9-111">toodo this, go toohello Azure Portal, go toohello **Azure RemoteApp** tab and open every Azure RemoteApp collection.</span></span> <span data-ttu-id="87eb9-112">移 toohello**使用者**索引標籤，並移除屬於 tooyour 目前的 Azure Active Directory 租用戶的使用者。</span><span class="sxs-lookup"><span data-stu-id="87eb9-112">Go toohello **Users** tab and remove users that belong tooyour current Azure Active Directory tenant.</span></span> <span data-ttu-id="87eb9-113">針對所有現有 Azure RemoteApp 集合重複進行。</span><span class="sxs-lookup"><span data-stu-id="87eb9-113">Repeat for all existing Azure RemoteApp collections.</span></span> <span data-ttu-id="87eb9-114">不這麼做，就能 toocreate 或修補程式集合。</span><span class="sxs-lookup"><span data-stu-id="87eb9-114">Without doing this, you will not be able toocreate or patch collections.</span></span>
> 
> 

<span data-ttu-id="87eb9-115">如果您想 toouse 不同的租用戶時，使用這些步驟 toochange hello 關聯與您的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="87eb9-115">If you want toouse a different tenant, use these steps toochange hello association with your subscription:</span></span>

1. <span data-ttu-id="87eb9-116">在 hello 入口網站移除任何 Azure AD 使用者 toowhich 您已獲得存取 tooAzure RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="87eb9-116">In hello portal, remove any Azure AD users toowhich you’ve given access tooAzure RemoteApp collections.</span></span> <span data-ttu-id="87eb9-117">(請參閱上述步驟的 hello 注意事項 toodo 這。)</span><span class="sxs-lookup"><span data-stu-id="87eb9-117">(See hello note above for steps on how toodo this.)</span></span>
2. <span data-ttu-id="87eb9-118">設定 Microsoft 帳戶 （先前稱為 Live ID） hello 服務系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="87eb9-118">Set a Microsoft account (formerly called a Live ID) as hello Service administrator.</span></span> <span data-ttu-id="87eb9-119">（不知道您已經是否 hello 服務系統管理員？</span><span class="sxs-lookup"><span data-stu-id="87eb9-119">(Don't know if you already are hello service admin?</span></span> <span data-ttu-id="87eb9-120">您可以按一下 [設定] -> [系統管理員] 來查看。)接下來，以下是變更的方法：</span><span class="sxs-lookup"><span data-stu-id="87eb9-120">You can find out by clicking **Settings -> Administrators**.) Now, here's how you change that:</span></span>
   
   1. <span data-ttu-id="87eb9-121">按一下 hello 右上角中的 hello 使用者，然後按一下**檢視我的帳單**。</span><span class="sxs-lookup"><span data-stu-id="87eb9-121">Click hello user in hello upper right corner, and then click **View my bill**.</span></span>
   2. <span data-ttu-id="87eb9-122">按一下 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="87eb9-122">Click hello subscription.</span></span> <span data-ttu-id="87eb9-123">然後，在 hello 新頁面上，向下捲動並按一下**編輯訂用帳戶詳細資料**hello 右中。</span><span class="sxs-lookup"><span data-stu-id="87eb9-123">Then, on hello new page, scroll down and click **Edit subscription details** in hello right.</span></span> <span data-ttu-id="87eb9-124">（hello 中間右下方，如果一種可協助您找到它。）</span><span class="sxs-lookup"><span data-stu-id="87eb9-124">(Sort of hello middle bottom right, if that helps you find it.)</span></span>
   3. <span data-ttu-id="87eb9-125">輸入 hello Microsoft 帳戶 hello 使用者應該 hello 服務系統管理員。</span><span class="sxs-lookup"><span data-stu-id="87eb9-125">Type hello Microsoft account for hello user that should be hello service admin.</span></span>
3. <span data-ttu-id="87eb9-126">現在，登出 hello 入口網站，然後傳回以 hello hello 先前步驟中所指定的 Microsoft 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="87eb9-126">Now, sign out of hello portal, and then sign back in with hello Microsoft account you specified in hello previous step.</span></span>
4. <span data-ttu-id="87eb9-127">依序按一下 [新增] > [應用程式服務] > [Active Directory] > [目錄] > [自訂建立]。</span><span class="sxs-lookup"><span data-stu-id="87eb9-127">Click **New -> App Services -> Active Directory -> Directory -> Custom Create**.</span></span>
5. <span data-ttu-id="87eb9-128">在 [目錄] 下方，選擇 [使用現有的目錄]。</span><span class="sxs-lookup"><span data-stu-id="87eb9-128">Under **Directory**, choose **Use existing directory**.</span></span> <span data-ttu-id="87eb9-129">我們會 toohave toosign 超出 hello 入口網站現在，您可以選擇**我已準備好立即登出的 toobe**。</span><span class="sxs-lookup"><span data-stu-id="87eb9-129">We're going toohave toosign you out of hello portal now, so choose **I am ready toobe signed out now**.</span></span>
6. <span data-ttu-id="87eb9-130">簽署回 hello 入口網站的 hello 目錄全域管理員為您想要 tooadd。</span><span class="sxs-lookup"><span data-stu-id="87eb9-130">Sign back into hello portal as a global admin of hello directory you want tooadd.</span></span> <span data-ttu-id="87eb9-131">(如果您還不是全域管理員，您將會經歷一回的登入然後登出。)</span><span class="sxs-lookup"><span data-stu-id="87eb9-131">(If you weren't already a global admin, you will be after a round of sign in and then sign out.)</span></span>
7. <span data-ttu-id="87eb9-132">如果您想要 toouse 您現有的 AD 租用戶與您訂用帳戶登入後會詢問您。</span><span class="sxs-lookup"><span data-stu-id="87eb9-132">You'll be asked when you sign in if you want toouse your existing AD tenant with your subscription.</span></span> <span data-ttu-id="87eb9-133">按一下 繼續，然後按一下立即登出。</span><span class="sxs-lookup"><span data-stu-id="87eb9-133">Click **Continue**, and then click **Sign out now**.</span></span>
8. <span data-ttu-id="87eb9-134">同樣地，登入，並返回太**設定]-> [訂閱**。</span><span class="sxs-lookup"><span data-stu-id="87eb9-134">Sign back in again, and go back too**Settings -> Subscriptions**.</span></span> <span data-ttu-id="87eb9-135">選取您的訂用帳戶，然後按一下編輯目錄 。</span><span class="sxs-lookup"><span data-stu-id="87eb9-135">Select your subscription, and then click **Edit Directory**.</span></span> <span data-ttu-id="87eb9-136">選取您想 toouse hello Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="87eb9-136">Select hello Azure AD tenant that you want toouse.</span></span>

<span data-ttu-id="87eb9-137">您現在可以使用 Azure RemoteApp 中的 hello 新的 Azure AD 租用戶 toocontrol 存取 toohello Azure 訂用帳戶和 tooconfigure 使用者存取權。</span><span class="sxs-lookup"><span data-stu-id="87eb9-137">You can now use hello new Azure AD tenant toocontrol access toohello Azure subscription and tooconfigure user access in Azure RemoteApp.</span></span>

