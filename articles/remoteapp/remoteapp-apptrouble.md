---
title: "Azure RemoteApp 疑難排解 - 應用程式啟動和連線失敗 | Microsoft Docs"
description: "瞭解如何疑難排解啟動及連線至 Azure RemoteApp 中之應用程式的問題。"
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
ms.openlocfilehash: fc9d538991adce7fc13e9654b9a7c6d113d03fde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a><span data-ttu-id="026c0-103">為 Azure RemoteApp 進行疑難排解 - 應用程式啟動和連線失敗</span><span class="sxs-lookup"><span data-stu-id="026c0-103">Troubleshoot Azure RemoteApp - Application launch and connection failures</span></span>
> [!IMPORTANT]
> <span data-ttu-id="026c0-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="026c0-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="026c0-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="026c0-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="026c0-106">Azure RemoteApp 中裝載的應用程式可能因幾個不同原因而無法啟動。</span><span class="sxs-lookup"><span data-stu-id="026c0-106">Applications hosted in Azure RemoteApp can fail to launch for a few different reasons.</span></span> <span data-ttu-id="026c0-107">此文章說明使用者嘗試啟動應用程式時可能會收到的各種原因和錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="026c0-107">This article describes various reasons and error messages users might receive when trying to launch applications.</span></span> <span data-ttu-id="026c0-108">文章中也會討論連線失敗。</span><span class="sxs-lookup"><span data-stu-id="026c0-108">It also talks about connection failures.</span></span> <span data-ttu-id="026c0-109">(但此文章不會說明登入 Azure RemoteApp 用戶端時出現的問題。)</span><span class="sxs-lookup"><span data-stu-id="026c0-109">(But this article does not describe issues when signing into the Azure RemoteApp client.)</span></span>  

<span data-ttu-id="026c0-110">請閱讀此文章以瞭解因應用程式啟動和連線失敗而顯示之一般錯誤訊息的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="026c0-110">Read on for information about common error messages due to app launch and connection failures.</span></span>

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a><span data-ttu-id="026c0-111">我們正在引導您設定...請在 10 分鐘內再試一次。</span><span class="sxs-lookup"><span data-stu-id="026c0-111">We're getting you set up... Try again in 10 minutes.</span></span>
<span data-ttu-id="026c0-112">此錯誤表示 Azure RemoteApp 正在向上擴充以滿足您使用者的容量需求。</span><span class="sxs-lookup"><span data-stu-id="026c0-112">This error means Azure RemoteApp is scaling up to meet the capacity need of your users.</span></span> <span data-ttu-id="026c0-113">正在背景建立更多 Azure RemoteApp VM，以處理您使用者的容量需求。</span><span class="sxs-lookup"><span data-stu-id="026c0-113">In the background more Azure RemoteApp VM instances are being created to handle the capacity needs of your users.</span></span> <span data-ttu-id="026c0-114">通常此工作約需要五分鐘來完成，但最多可能需要 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="026c0-114">Typically this takes around five minutes but can take up to 10 minutes.</span></span> <span data-ttu-id="026c0-115">有時候此工作完成速度不夠快，但是資源的需求卻是立即性的。</span><span class="sxs-lookup"><span data-stu-id="026c0-115">Sometimes, this doesn't happen fast enough and resources are needed immediately.</span></span> <span data-ttu-id="026c0-116">例如，9 AM 時許多使用者需要同時使用 Azure RemoteAppn 中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="026c0-116">For example a 9 AM scenario where many users need to use your app in Azure RemoteAppn at the same time.</span></span> <span data-ttu-id="026c0-117">如果您遇到這個問題，我們可以在後端啟用 **容量模式** 。</span><span class="sxs-lookup"><span data-stu-id="026c0-117">If this happens to you we can enable **capacity mode** on the back end.</span></span> <span data-ttu-id="026c0-118">若要這樣做，請開啟一個 Azure 支援票證。</span><span class="sxs-lookup"><span data-stu-id="026c0-118">To do this open an Azure Support ticket.</span></span> <span data-ttu-id="026c0-119">請務必在要求中包含您的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="026c0-119">Be certain to include your subscription ID in the request.</span></span>  

![我們正在引導您設定](./media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-to-your-applications-please-re-launch-your-application"></a><span data-ttu-id="026c0-121">無法自動重新連線至您的應用程式，請重新啟動您的應用程式</span><span class="sxs-lookup"><span data-stu-id="026c0-121">Could not auto-reconnect to your applications, please re-launch your application</span></span>
<span data-ttu-id="026c0-122">如果您是使用 Azure RemoteApp 接著讓電腦睡眠超過 4 小時，然後喚醒電腦且 Azure RemoteApp 用戶端嘗試自動重新連線且逾時時，您就會常常看到這個錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="026c0-122">This error message is often seen if you were using Azure RemoteApp and then put your PC to sleep longer than 4 hours and then woke your PC up and the Azure RemoteApp client attempt to auto reconnect and timeout was exceeded.</span></span>  <span data-ttu-id="026c0-123">請指示使用者瀏覽回應用程式並嘗試從 Azure RemoteApp 用戶端開啟應用程式。</span><span class="sxs-lookup"><span data-stu-id="026c0-123">Instruct users to navigate back to the application and attempt to open it from the Azure RemoteApp client.</span></span>

![無法自動重新連線至您的應用程式](./media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-the-temp-profile"></a><span data-ttu-id="026c0-125">暫存設定檔的問題</span><span class="sxs-lookup"><span data-stu-id="026c0-125">Problems with the temp profile</span></span>
<span data-ttu-id="026c0-126">當您的使用者設定檔 (使用者設定檔磁碟) 無法掛接且使用者收到暫存設定檔時，就會發生這項錯誤。</span><span class="sxs-lookup"><span data-stu-id="026c0-126">This error occurs when your user profile (User Profile Disk) failed to mount and the user received a temporary profile.</span></span>  <span data-ttu-id="026c0-127">系統管理員應瀏覽至 Azure 入口網站中的集合，然後移到 [工作階段] 索引標籤並嘗試 [登出] 使用者。</span><span class="sxs-lookup"><span data-stu-id="026c0-127">Administrators should navigate to the collection in the Azure portal and then go to the **Sessions** tab and attempt to **Log Off** the user.</span></span> <span data-ttu-id="026c0-128">這會強制完整登出使用者工作階段 - 然後讓使用者嘗試再次啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="026c0-128">This will force a full log off of the user session - then have the user attempt to launch an app again.</span></span> <span data-ttu-id="026c0-129">如果失敗，請連絡 Azure 支援服務。</span><span class="sxs-lookup"><span data-stu-id="026c0-129">If that fails contact Azure support.</span></span>

## <a name="azure-remoteapp-has-stopped-working"></a><span data-ttu-id="026c0-130">Azure RemoteApp 已停止運作</span><span class="sxs-lookup"><span data-stu-id="026c0-130">Azure RemoteApp has stopped working</span></span>
<span data-ttu-id="026c0-131">此錯誤訊息表示 Azure RemoteApp 用戶端發生問題並需要重新啟動。</span><span class="sxs-lookup"><span data-stu-id="026c0-131">This error message means the Azure RemoteApp client is having an issue and needs to be restarted.</span></span> <span data-ttu-id="026c0-132">請指示使用者：選取 [關閉程式]  然後再次啟動 Azure RemoteApp 用戶端。</span><span class="sxs-lookup"><span data-stu-id="026c0-132">Instruct users to close: select **Close program** and then launch the Azure RemoteApp client again.</span></span>  <span data-ttu-id="026c0-133">如果持續發生此問題，請開啟一個 Azure 支援票證。</span><span class="sxs-lookup"><span data-stu-id="026c0-133">If the issue continues open and Azure Support ticket.</span></span>

![Azure RemoteApp 已停止運作](./media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-the-connection-or-contact-your-system-administrator"></a><span data-ttu-id="026c0-135">「遠端桌面連線」存取此資源時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="026c0-135">An error occurred while Remote Desktop Connection was accessing this resource.</span></span> <span data-ttu-id="026c0-136">請嘗試重新連線，或連絡您的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="026c0-136">Retry the connection or contact your system administrator</span></span>
<span data-ttu-id="026c0-137">這是一般錯誤訊息 - 請連絡 Azure 支援服務，以便我們進行調查。</span><span class="sxs-lookup"><span data-stu-id="026c0-137">This is a generic error message - contact Azure support so we can investigate.</span></span> 

![一般 Azure RemoteApp 訊息](./media/remoteapp-apptrouble/ra-apptrouble4.png) 

