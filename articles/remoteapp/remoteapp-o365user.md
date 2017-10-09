---
title: "Office 365 使用者帳戶的 aaaHow toouse Azure RemoteApp |Microsoft 文件"
description: "深入了解如何與我的 Office 365 使用者帳戶的 Azure RemoteApp toouse"
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: aba70fd3-60b0-4b44-9321-1ab18760ccd5
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d2dbed2a6838adf9bb0f7508eb7dcecb0a74a62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-remoteapp-with-office-365-user-accounts"></a><span data-ttu-id="70b1f-103">如何使用 Office 365 使用者帳戶的 Azure RemoteApp toouse</span><span class="sxs-lookup"><span data-stu-id="70b1f-103">How toouse Azure RemoteApp with Office 365 user accounts</span></span>
> [!IMPORTANT]
> <span data-ttu-id="70b1f-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="70b1f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="70b1f-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="70b1f-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="70b1f-106">如果您有 Office 365 訂閱，您有 Azure Active Directory 儲存使用者名稱和密碼使用 tooaccess Office 365 服務。</span><span class="sxs-lookup"><span data-stu-id="70b1f-106">If you have an Office 365 subscription you have an Azure Active Directory that stores your user names and passwords used tooaccess Office 365 services.</span></span> <span data-ttu-id="70b1f-107">比方說，當您的使用者啟用 Office 365 ProPlus 在驗證對 Azure AD toocheck 授權。</span><span class="sxs-lookup"><span data-stu-id="70b1f-107">For example, when your users activate Office 365 ProPlus they authenticate against Azure AD toocheck for licenses.</span></span> <span data-ttu-id="70b1f-108">大部分的客戶會像 toouse hello 相同目錄與 Azure RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="70b1f-108">Most customers would like toouse hello same directory with Azure RemoteApp.</span></span>

<span data-ttu-id="70b1f-109">如果您正在部署 Azure RemoteApp，您最有可能會使用與不同 Azure AD 相關聯的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="70b1f-109">If you are deploying Azure RemoteApp you are most likely using an Azure subscription that is associated with a different Azure AD.</span></span> <span data-ttu-id="70b1f-110">在排序 toouse Office 365 目錄，您將需要 toomove hello 至該目錄的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="70b1f-110">In order toouse your Office 365 directory, you will need toomove hello Azure subscription into that directory.</span></span>

<span data-ttu-id="70b1f-111">如需如何資訊 toodeploy Office 365 用戶端應用程式，請參閱[如何 toouse 您 Office 365 訂用帳戶與 Azure RemoteApp 一起](remoteapp-officesubscription.md)。</span><span class="sxs-lookup"><span data-stu-id="70b1f-111">For info on how toodeploy Office 365 client applications, see [How toouse your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span></span>

## <a name="phase-1-register-your-free-office-365-azure-active-directory-subscription"></a><span data-ttu-id="70b1f-112">階段 1：註冊免費的 Office 365 Azure Active Directory 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="70b1f-112">Phase 1: Register your free Office 365 Azure Active Directory subscription</span></span>
<span data-ttu-id="70b1f-113">如果您使用 hello Azure 傳統入口網站，使用中的 hello 步驟[註冊免費的 Azure Active Directory 訂閱](https://technet.microsoft.com/library/dn832618.aspx)tooget 系統管理存取權 tooyour Azure AD 透過 hello Azure 管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="70b1f-113">If you are using hello Azure classic portal, use hello steps in [Register your free Azure Active Directory subscription](https://technet.microsoft.com/library/dn832618.aspx) tooget administrative access tooyour Azure AD via hello Azure Management Portal.</span></span> <span data-ttu-id="70b1f-114">做為此程序的 hello 結果您也應該能夠 toolog 到 hello Azure 入口網站並請參閱您的目錄那里 – 此時不會看到更因為 hello 您 Azure RemoteApp 搭配使用的完整的 Azure 訂用帳戶是在不同的目錄。</span><span class="sxs-lookup"><span data-stu-id="70b1f-114">As hello result of this process you should be able toolog into hello Azure portal and see your directory there – at this point you won’t see much more since hello full Azure subscription you are using with Azure RemoteApp is in a different directory.</span></span>

<span data-ttu-id="70b1f-115">記住 hello 名稱和您在此步驟中建立的 hello 系統管理員帳戶的密碼 – 第 2 階段會需要它們。</span><span class="sxs-lookup"><span data-stu-id="70b1f-115">Remember hello name and password of hello administrator account you created in this step – they will be needed in Phase 2.</span></span>

<span data-ttu-id="70b1f-116">如果您使用 hello Azure 入口網站，請參閱[如何 tooregister 並啟用免費的 Azure Active Directory 使用 Office 365 入口網站](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/)。</span><span class="sxs-lookup"><span data-stu-id="70b1f-116">If you are using hello Azure portal, check out [How tooregister and activate a free Azure Active Directory using Office 365 portal](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/).</span></span>

## <a name="phase-2-change-hello-azure-ad-associated-with-your-azure-subscription"></a><span data-ttu-id="70b1f-117">階段 2： 變更 hello Azure AD 與 Azure 訂用帳戶關聯。</span><span class="sxs-lookup"><span data-stu-id="70b1f-117">Phase 2: Change hello Azure AD associated with your Azure subscription.</span></span>
<span data-ttu-id="70b1f-118">我們 toochange 您 Azure 訂用帳戶從其目前的目錄到我們與工作階段 1 中的 hello Office 365 目錄。</span><span class="sxs-lookup"><span data-stu-id="70b1f-118">We are going toochange your Azure subscription from its current directory into hello Office 365 directory we worked with in Phase 1.</span></span>

<span data-ttu-id="70b1f-119">請依照下列所述的 hello 指示[Azure RemoteApp 中的變更 hello Azure Active Directory 租用戶](remoteapp-changetenant.md)。</span><span class="sxs-lookup"><span data-stu-id="70b1f-119">Follow hello instructions described in [Change hello Azure Active Directory tenant in Azure RemoteApp](remoteapp-changetenant.md).</span></span> <span data-ttu-id="70b1f-120">請特別注意 toohello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="70b1f-120">Pay particular attention toohello following steps:</span></span>

* <span data-ttu-id="70b1f-121">步驟 1：如果您已在此訂用帳戶中部署 Azure RemoteApp (ARA)，在嘗試執行任何動作之前，請先確定您會從任何 ARA 集合中移除所有的 Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="70b1f-121">Step #1: If you have deployed Azure RemoteApp (ARA) in this subscription, make sure you remove all Azure AD user accounts from any ARA collections first, before trying anything else.</span></span> <span data-ttu-id="70b1f-122">或者，您可以考慮刪除任何現有的集合。</span><span class="sxs-lookup"><span data-stu-id="70b1f-122">Alternatively, you can consider deleting any existing collections.</span></span>
* <span data-ttu-id="70b1f-123">步驟 2：這是一個重要的步驟。</span><span class="sxs-lookup"><span data-stu-id="70b1f-123">Step #2: This is a critical step.</span></span> <span data-ttu-id="70b1f-124">您需要 toouse Microsoft 帳戶 (例如@outlook.com) 做為服務管理員 hello 訂用帳戶; 這是因為我們不能有任何使用者帳戶，從 hello 現有 Azure AD 附加 toohello 訂用帳戶 – 如果我們這樣做，我們將不會無法 toomove 它 tooa不同的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="70b1f-124">You need toouse a Microsoft account (e.g. @outlook.com) as a Service Administrator on hello subscription; this is because we cannot have any user accounts from hello existing Azure AD attached toohello subscription – if we do, we won’t be able toomove it tooa different Azure AD.</span></span>
* <span data-ttu-id="70b1f-125">步驟 #4： 加入時的現有目錄，hello 系統會要求您使用 hello 系統管理員帳戶 toosign 該目錄。</span><span class="sxs-lookup"><span data-stu-id="70b1f-125">Step #4: When adding an existing directory, hello system will ask you toosign in with hello administrator account for that directory.</span></span> <span data-ttu-id="70b1f-126">請確定 toouse hello 系統管理員帳戶，從第 1 階段。</span><span class="sxs-lookup"><span data-stu-id="70b1f-126">Make sure toouse hello administrator account from Phase 1.</span></span>
* <span data-ttu-id="70b1f-127">步驟 5： 變更 hello 訂用帳戶 tooyour Office 365 directory hello 父目錄。</span><span class="sxs-lookup"><span data-stu-id="70b1f-127">Step #5: Change hello parent directory of hello subscription tooyour Office 365 directory.</span></span> <span data-ttu-id="70b1f-128">hello 最後的結果是，在 設定-> 您的訂閱列出 hello Office 365 目錄的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="70b1f-128">hello end result should be that under Settings -> Subscriptions your subscription lists hello Office 365 directory.</span></span> 
  <span data-ttu-id="70b1f-129">![變更 hello 訂閱 hello 父目錄](./media/remoteapp-o365user/settings.png)</span><span class="sxs-lookup"><span data-stu-id="70b1f-129">![Change hello parent directory of hello subscription](./media/remoteapp-o365user/settings.png)</span></span>

<span data-ttu-id="70b1f-130">此時您 Azure RemoteApp 訂用帳戶都與您 Office 365 Azure AD。您可以使用 hello 現有 Office 365 使用者帳戶與 Azure RemoteApp 一起 ！</span><span class="sxs-lookup"><span data-stu-id="70b1f-130">At this point your Azure RemoteApp subscription is associated with your Office 365 Azure AD; you can use hello existing Office 365 user accounts with Azure RemoteApp!</span></span>

