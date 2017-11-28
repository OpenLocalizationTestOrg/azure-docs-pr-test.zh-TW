---
title: "如何搭配 Office 365 使用者帳戶使用 Azure RemoteApp | Microsoft Docs"
description: "了解如何搭配 Office 365 使用者帳戶使用 Azure RemoteApp"
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
ms.openlocfilehash: 1bc8949c236afd03415f961cf7a657d4d3926b07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-remoteapp-with-office-365-user-accounts"></a><span data-ttu-id="596d7-103">如何搭配 Office 365 使用者帳戶使用 Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="596d7-103">How to use Azure RemoteApp with Office 365 user accounts</span></span>
> [!IMPORTANT]
> <span data-ttu-id="596d7-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="596d7-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="596d7-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="596d7-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="596d7-106">如果您有 Office 365 訂閱，就會擁有 Azure Active Directory，其會儲存您用來存取 Office 365 服務的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="596d7-106">If you have an Office 365 subscription you have an Azure Active Directory that stores your user names and passwords used to access Office 365 services.</span></span> <span data-ttu-id="596d7-107">例如，當您的使用者啟用 Office 365 ProPlus 時，它們會針對 Azure AD 進行驗證以檢查授權。</span><span class="sxs-lookup"><span data-stu-id="596d7-107">For example, when your users activate Office 365 ProPlus they authenticate against Azure AD to check for licenses.</span></span> <span data-ttu-id="596d7-108">大部分的客戶會想要使用與 Azure RemoteApp 相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="596d7-108">Most customers would like to use the same directory with Azure RemoteApp.</span></span>

<span data-ttu-id="596d7-109">如果您正在部署 Azure RemoteApp，您最有可能會使用與不同 Azure AD 相關聯的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="596d7-109">If you are deploying Azure RemoteApp you are most likely using an Azure subscription that is associated with a different Azure AD.</span></span> <span data-ttu-id="596d7-110">若要使用 Office 365 目錄，您必須將 Azure 訂用帳戶移至該目錄。</span><span class="sxs-lookup"><span data-stu-id="596d7-110">In order to use your Office 365 directory, you will need to move the Azure subscription into that directory.</span></span>

<span data-ttu-id="596d7-111">如需如何部署 Office 365 用戶端應用程式的相關資訊，請參閱 [如何搭配 Azure RemoteApp 使用 Office 365 訂用帳戶](remoteapp-officesubscription.md)。</span><span class="sxs-lookup"><span data-stu-id="596d7-111">For info on how to deploy Office 365 client applications, see [How to use your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span></span>

## <a name="phase-1-register-your-free-office-365-azure-active-directory-subscription"></a><span data-ttu-id="596d7-112">階段 1：註冊免費的 Office 365 Azure Active Directory 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="596d7-112">Phase 1: Register your free Office 365 Azure Active Directory subscription</span></span>
<span data-ttu-id="596d7-113">如果您正在使用 Azure 傳統入口網站，請使用 [註冊您的免費 Azure Active Directory 訂用帳戶](https://technet.microsoft.com/library/dn832618.aspx) 中的步驟，透過 Azure 管理入口網站取得 Azure AD 的系統管理存取權。</span><span class="sxs-lookup"><span data-stu-id="596d7-113">If you are using the Azure classic portal, use the steps in [Register your free Azure Active Directory subscription](https://technet.microsoft.com/library/dn832618.aspx) to get administrative access to your Azure AD via the Azure Management Portal.</span></span> <span data-ttu-id="596d7-114">完成此程序之後，您應該能夠登入 Azure 入口網站並在此處查看您的目錄 - 此時，您將不會看見更多資訊，因為您搭配 Azure RemoteApp 使用的完整 Azure 訂用帳戶是在不同的目錄中。</span><span class="sxs-lookup"><span data-stu-id="596d7-114">As the result of this process you should be able to log into the Azure portal and see your directory there – at this point you won’t see much more since the full Azure subscription you are using with Azure RemoteApp is in a different directory.</span></span>

<span data-ttu-id="596d7-115">請記下您在此步驟中建立之系統管理員帳戶的名稱和密碼 - 您需要在階段 2 用到它們。</span><span class="sxs-lookup"><span data-stu-id="596d7-115">Remember the name and password of the administrator account you created in this step – they will be needed in Phase 2.</span></span>

<span data-ttu-id="596d7-116">如果您正在使用 Azure 入口網站，請參閱 [如何使用 Office 365 入口網站註冊及啟用免費的 Azure Active Directory](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/)。</span><span class="sxs-lookup"><span data-stu-id="596d7-116">If you are using the Azure portal, check out [How to register and activate a free Azure Active Directory using Office 365 portal](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/).</span></span>

## <a name="phase-2-change-the-azure-ad-associated-with-your-azure-subscription"></a><span data-ttu-id="596d7-117">階段 2：變更與您的 Azure 訂用帳戶相關聯的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="596d7-117">Phase 2: Change the Azure AD associated with your Azure subscription.</span></span>
<span data-ttu-id="596d7-118">我們會將您的 Azure 訂用帳戶從其目前的目錄變更為我們在階段 1 使用的 Office 365 目錄。</span><span class="sxs-lookup"><span data-stu-id="596d7-118">We are going to change your Azure subscription from its current directory into the Office 365 directory we worked with in Phase 1.</span></span>

<span data-ttu-id="596d7-119">請遵循 [變更 Azure RemoteApp 中的 Azure Active Directory 租用戶](remoteapp-changetenant.md)中說明的指示。</span><span class="sxs-lookup"><span data-stu-id="596d7-119">Follow the instructions described in [Change the Azure Active Directory tenant in Azure RemoteApp](remoteapp-changetenant.md).</span></span> <span data-ttu-id="596d7-120">請特別注意下列步驟：</span><span class="sxs-lookup"><span data-stu-id="596d7-120">Pay particular attention to the following steps:</span></span>

* <span data-ttu-id="596d7-121">步驟 1：如果您已在此訂用帳戶中部署 Azure RemoteApp (ARA)，在嘗試執行任何動作之前，請先確定您會從任何 ARA 集合中移除所有的 Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="596d7-121">Step #1: If you have deployed Azure RemoteApp (ARA) in this subscription, make sure you remove all Azure AD user accounts from any ARA collections first, before trying anything else.</span></span> <span data-ttu-id="596d7-122">或者，您可以考慮刪除任何現有的集合。</span><span class="sxs-lookup"><span data-stu-id="596d7-122">Alternatively, you can consider deleting any existing collections.</span></span>
* <span data-ttu-id="596d7-123">步驟 2：這是一個重要的步驟。</span><span class="sxs-lookup"><span data-stu-id="596d7-123">Step #2: This is a critical step.</span></span> <span data-ttu-id="596d7-124">您必須使用 Microsoft 帳戶 (例如 @outlook.com) 做為訂用帳戶上的服務管理員。這是因為我們不能將任何來自現有 Azure AD 的使用者帳戶附加到訂用帳戶，如果這樣做，就無法將它移至不同的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="596d7-124">You need to use a Microsoft account (e.g. @outlook.com) as a Service Administrator on the subscription; this is because we cannot have any user accounts from the existing Azure AD attached to the subscription – if we do, we won’t be able to move it to a different Azure AD.</span></span>
* <span data-ttu-id="596d7-125">步驟 4：加入現有的目錄時，系統將要求您使用該目錄的系統管理員帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="596d7-125">Step #4: When adding an existing directory, the system will ask you to sign in with the administrator account for that directory.</span></span> <span data-ttu-id="596d7-126">請務必使用階段 1 的系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="596d7-126">Make sure to use the administrator account from Phase 1.</span></span>
* <span data-ttu-id="596d7-127">步驟 5：將訂用帳戶的上層目錄變更為 Office 365 目錄。</span><span class="sxs-lookup"><span data-stu-id="596d7-127">Step #5: Change the parent directory of the subscription to your Office 365 directory.</span></span> <span data-ttu-id="596d7-128">最後的結果應該會在 [設定] -> 您的訂用帳戶列出 Office 365 目錄的 [訂用帳戶] 下方。</span><span class="sxs-lookup"><span data-stu-id="596d7-128">The end result should be that under Settings -> Subscriptions your subscription lists the Office 365 directory.</span></span> 
  <span data-ttu-id="596d7-129">![變更訂用帳戶的上層目錄](./media/remoteapp-o365user/settings.png)</span><span class="sxs-lookup"><span data-stu-id="596d7-129">![Change the parent directory of the subscription](./media/remoteapp-o365user/settings.png)</span></span>

<span data-ttu-id="596d7-130">此時您的 Azure RemoteApp 訂用帳戶會與您的 Office 365 Azure AD 產生關聯；您可以搭配 Azure RemoteApp 使用現有的 Office 365 使用者帳戶！</span><span class="sxs-lookup"><span data-stu-id="596d7-130">At this point your Azure RemoteApp subscription is associated with your Office 365 Azure AD; you can use the existing Office 365 user accounts with Azure RemoteApp!</span></span>

