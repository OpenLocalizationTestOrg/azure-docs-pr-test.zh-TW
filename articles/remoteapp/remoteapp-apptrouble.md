---
title: "aaaAzure 疑難排解 RemoteApp-應用程式啟動和連線失敗 |Microsoft 文件"
description: "了解如何 tootroubleshoot 問題的啟動及連線 tooapplications Azure RemoteApp 中。"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e5cf7171-d1c2-4053-a38b-5af7821305e1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e51d480c9d3fa1f2076f95b63c7a8cd2f6956a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a><span data-ttu-id="25ed6-103">為 Azure RemoteApp 進行疑難排解 - 應用程式啟動和連線失敗</span><span class="sxs-lookup"><span data-stu-id="25ed6-103">Troubleshoot Azure RemoteApp - Application launch and connection failures</span></span>
> [!IMPORTANT]
> <span data-ttu-id="25ed6-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="25ed6-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="25ed6-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="25ed6-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="25ed6-106">裝載於 Azure RemoteApp 中的應用程式可能失敗 toolaunch 的幾個不同的原因。</span><span class="sxs-lookup"><span data-stu-id="25ed6-106">Applications hosted in Azure RemoteApp can fail toolaunch for a few different reasons.</span></span> <span data-ttu-id="25ed6-107">本文說明各種原因和使用者時可能會收到錯誤訊息嘗試 toolaunch 應用程式。</span><span class="sxs-lookup"><span data-stu-id="25ed6-107">This article describes various reasons and error messages users might receive when trying toolaunch applications.</span></span> <span data-ttu-id="25ed6-108">文章中也會討論連線失敗。</span><span class="sxs-lookup"><span data-stu-id="25ed6-108">It also talks about connection failures.</span></span> <span data-ttu-id="25ed6-109">（但此發行項登入 hello Azure RemoteApp 用戶端時不會說明問題）。</span><span class="sxs-lookup"><span data-stu-id="25ed6-109">(But this article does not describe issues when signing into hello Azure RemoteApp client.)</span></span>  

<span data-ttu-id="25ed6-110">讀取上常見的錯誤訊息，因為 tooapp 啟動和連線失敗的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="25ed6-110">Read on for information about common error messages due tooapp launch and connection failures.</span></span>

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a><span data-ttu-id="25ed6-111">我們正在引導您設定...請在 10 分鐘內再試一次。</span><span class="sxs-lookup"><span data-stu-id="25ed6-111">We're getting you set up... Try again in 10 minutes.</span></span>
<span data-ttu-id="25ed6-112">此錯誤表示 Azure RemoteApp 向上 toomeet hello 容量需求的使用者。</span><span class="sxs-lookup"><span data-stu-id="25ed6-112">This error means Azure RemoteApp is scaling up toomeet hello capacity need of your users.</span></span> <span data-ttu-id="25ed6-113">Hello 背景中多個 Azure RemoteApp VM 執行個體正在建立使用者 toohandle hello 容量需求。</span><span class="sxs-lookup"><span data-stu-id="25ed6-113">In hello background more Azure RemoteApp VM instances are being created toohandle hello capacity needs of your users.</span></span> <span data-ttu-id="25ed6-114">通常這會佔用大約五分鐘，但可能會佔用 too10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="25ed6-114">Typically this takes around five minutes but can take up too10 minutes.</span></span> <span data-ttu-id="25ed6-115">有時候此工作完成速度不夠快，但是資源的需求卻是立即性的。</span><span class="sxs-lookup"><span data-stu-id="25ed6-115">Sometimes, this doesn't happen fast enough and resources are needed immediately.</span></span> <span data-ttu-id="25ed6-116">例如，許多使用者會需要 toouse 您的應用程式在 Azure RemoteAppn hello 的上午 9 點案例相同的時間。</span><span class="sxs-lookup"><span data-stu-id="25ed6-116">For example a 9 AM scenario where many users need toouse your app in Azure RemoteAppn at hello same time.</span></span> <span data-ttu-id="25ed6-117">如果發生這種情況 tooyou 我們可以啟用**容量模式**上 hello 後端。</span><span class="sxs-lookup"><span data-stu-id="25ed6-117">If this happens tooyou we can enable **capacity mode** on hello back end.</span></span> <span data-ttu-id="25ed6-118">toodo 此開啟 Azure 支援票證。</span><span class="sxs-lookup"><span data-stu-id="25ed6-118">toodo this open an Azure Support ticket.</span></span> <span data-ttu-id="25ed6-119">為特定 tooinclude hello 要求在您訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="25ed6-119">Be certain tooinclude your subscription ID in hello request.</span></span>  

![我們正在引導您設定](./media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-tooyour-applications-please-re-launch-your-application"></a><span data-ttu-id="25ed6-121">無法不自動重新連線 tooyour 應用程式，請重新啟動您的應用程式</span><span class="sxs-lookup"><span data-stu-id="25ed6-121">Could not auto-reconnect tooyour applications, please re-launch your application</span></span>
<span data-ttu-id="25ed6-122">如果您使用 Azure RemoteApp，然後放入您的電腦 toosleep 超過 4 小時並再喚醒您的電腦 hello Azure RemoteApp 用戶端嘗試 tooauto 重新連線且已超過逾時，通常會看到此錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="25ed6-122">This error message is often seen if you were using Azure RemoteApp and then put your PC toosleep longer than 4 hours and then woke your PC up and hello Azure RemoteApp client attempt tooauto reconnect and timeout was exceeded.</span></span>  <span data-ttu-id="25ed6-123">指示使用者 toonavigate 後 toohello 應用程式，並嘗試 tooopen 從 hello Azure RemoteApp 用戶端。</span><span class="sxs-lookup"><span data-stu-id="25ed6-123">Instruct users toonavigate back toohello application and attempt tooopen it from hello Azure RemoteApp client.</span></span>

![無法不自動重新連線 tooyour 應用程式](./media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-hello-temp-profile"></a><span data-ttu-id="25ed6-125">Hello 暫存設定檔的問題</span><span class="sxs-lookup"><span data-stu-id="25ed6-125">Problems with hello temp profile</span></span>
<span data-ttu-id="25ed6-126">您的使用者設定檔 （使用者設定檔磁碟） 無法 toomount 和 hello 使用者收到暫存設定檔時，就會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="25ed6-126">This error occurs when your user profile (User Profile Disk) failed toomount and hello user received a temporary profile.</span></span>  <span data-ttu-id="25ed6-127">系統管理員應該瀏覽 toohello hello Azure 入口網站中的集合，並前往 toohello**工作階段**索引標籤，然後嘗試過**登出**hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="25ed6-127">Administrators should navigate toohello collection in hello Azure portal and then go toohello **Sessions** tab and attempt too**Log Off** hello user.</span></span> <span data-ttu-id="25ed6-128">這會強制完整開 hello 使用者工作階段的記錄，然後再次具有 hello 使用者嘗試 toolaunch 應用程式。</span><span class="sxs-lookup"><span data-stu-id="25ed6-128">This will force a full log off of hello user session - then have hello user attempt toolaunch an app again.</span></span> <span data-ttu-id="25ed6-129">如果失敗，請連絡 Azure 支援服務。</span><span class="sxs-lookup"><span data-stu-id="25ed6-129">If that fails contact Azure support.</span></span>

## <a name="azure-remoteapp-has-stopped-working"></a><span data-ttu-id="25ed6-130">Azure RemoteApp 已停止運作</span><span class="sxs-lookup"><span data-stu-id="25ed6-130">Azure RemoteApp has stopped working</span></span>
<span data-ttu-id="25ed6-131">這則錯誤訊息表示 hello Azure RemoteApp 用戶端有問題，而且需要 toobe 重新啟動。</span><span class="sxs-lookup"><span data-stu-id="25ed6-131">This error message means hello Azure RemoteApp client is having an issue and needs toobe restarted.</span></span> <span data-ttu-id="25ed6-132">指示使用者 tooclose： 選取**關閉程式**，然後再次啟動 hello Azure RemoteApp 用戶端。</span><span class="sxs-lookup"><span data-stu-id="25ed6-132">Instruct users tooclose: select **Close program** and then launch hello Azure RemoteApp client again.</span></span>  <span data-ttu-id="25ed6-133">如果 hello 問題仍繼續開啟與 Azure 支援票證。</span><span class="sxs-lookup"><span data-stu-id="25ed6-133">If hello issue continues open and Azure Support ticket.</span></span>

![Azure RemoteApp 已停止運作](./media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-hello-connection-or-contact-your-system-administrator"></a><span data-ttu-id="25ed6-135">「遠端桌面連線」存取此資源時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="25ed6-135">An error occurred while Remote Desktop Connection was accessing this resource.</span></span> <span data-ttu-id="25ed6-136">重試 hello 連線或連絡您的系統管理員</span><span class="sxs-lookup"><span data-stu-id="25ed6-136">Retry hello connection or contact your system administrator</span></span>
<span data-ttu-id="25ed6-137">這是一般錯誤訊息 - 請連絡 Azure 支援服務，以便我們進行調查。</span><span class="sxs-lookup"><span data-stu-id="25ed6-137">This is a generic error message - contact Azure support so we can investigate.</span></span> 

![一般 Azure RemoteApp 訊息](./media/remoteapp-apptrouble/ra-apptrouble4.png) 

