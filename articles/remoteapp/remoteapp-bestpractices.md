---
title: "Azure RemoteApp 最佳做法 | Microsoft Docs"
description: "設定和使用 Azure RemoteApp 的最佳做法。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b851865b-bec4-4f29-82c0-7b9770c1a520
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ab9c2dafc622e9b6f3bcd2767218cdc03e844847
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a><span data-ttu-id="ec825-103">設定和使用 Azure RemoteApp 的最佳做法</span><span class="sxs-lookup"><span data-stu-id="ec825-103">Best practices for configuring and using Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ec825-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="ec825-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ec825-105">如需詳細資訊，請參閱 [公告](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) 。</span><span class="sxs-lookup"><span data-stu-id="ec825-105">Read the [announcement](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) for details.</span></span>
> 
> 

<span data-ttu-id="ec825-106">下列資訊可協助您有效率地設定和使用 Azure RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="ec825-106">The following information can help you configure and use Azure RemoteApp productively.</span></span>

## <a name="connectivity"></a><span data-ttu-id="ec825-107">連線能力</span><span class="sxs-lookup"><span data-stu-id="ec825-107">Connectivity</span></span>
* <span data-ttu-id="ec825-108">請始終使用最新的用戶端版本。</span><span class="sxs-lookup"><span data-stu-id="ec825-108">Always use the latest client version.</span></span> <span data-ttu-id="ec825-109">使用舊版的用戶端可能會造成連線問題和其他降級的體驗。</span><span class="sxs-lookup"><span data-stu-id="ec825-109">Using older clients might result in connectivity issues and other degraded experiences.</span></span> <span data-ttu-id="ec825-110">為您的裝置啟用自動應用程式更新將可確保安裝的永遠是最新的用戶端。</span><span class="sxs-lookup"><span data-stu-id="ec825-110">Enabling automatic application updates for your device will ensure that the latest client is always installed.</span></span>
* <span data-ttu-id="ec825-111">請始終使用最穩定和最可靠的網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="ec825-111">Always use the most stable and reliable internet connection available to you.</span></span>  
* <span data-ttu-id="ec825-112">請使用支援的 Proxy 連線以獲得最佳連線效能。</span><span class="sxs-lookup"><span data-stu-id="ec825-112">Use only supported proxy connections for optimal connectivity performance.</span></span>  <span data-ttu-id="ec825-113">不支援 SOCKS Proxy。</span><span class="sxs-lookup"><span data-stu-id="ec825-113">The SOCKS proxy is not supported.</span></span>

## <a name="applications"></a><span data-ttu-id="ec825-114">應用程式</span><span class="sxs-lookup"><span data-stu-id="ec825-114">Applications</span></span>
* <span data-ttu-id="ec825-115">當您結束應用程式後，請儲存並關閉 RemoteApp 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec825-115">Save and close RemoteApp applications when you are done with the application.</span></span> <span data-ttu-id="ec825-116">未關閉應用程式可能會導致資料遺失。</span><span class="sxs-lookup"><span data-stu-id="ec825-116">Not closing the application might result in data loss.</span></span>
* <span data-ttu-id="ec825-117">在 Azure RemoteApp 中使用自訂應用程式之前，請先進行驗證。</span><span class="sxs-lookup"><span data-stu-id="ec825-117">Validate custom applications before using them in Azure RemoteApp.</span></span> <span data-ttu-id="ec825-118">這包括確認它們可在多重工作階段的平台上運作，而且不會使用不必要的資源，例如可能使同一收藏中的其他使用者缺乏的記憶體和 CPU。</span><span class="sxs-lookup"><span data-stu-id="ec825-118">This includes ensuring they work on a multi-session platform and don’t consume unnecessary resources such as memory and CPU that might starve another user in the same collection.</span></span> <span data-ttu-id="ec825-119">如需詳細資訊，請下載並檢閱 [遠端桌面服務的應用程式相容性最佳做法](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf)。</span><span class="sxs-lookup"><span data-stu-id="ec825-119">For information, download and review the [Application Compatibility Best Practices for Remote Desktop Services](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span></span>

## <a name="configuration-and-management"></a><span data-ttu-id="ec825-120">設定和管理</span><span class="sxs-lookup"><span data-stu-id="ec825-120">Configuration and management</span></span>
* <span data-ttu-id="ec825-121">隨時更新您的範本映像，視需要安裝軟體更新和其他重要的修正程式。</span><span class="sxs-lookup"><span data-stu-id="ec825-121">Keep your template images up to date, installing software updates and other critical fixes as needed.</span></span> <span data-ttu-id="ec825-122">這可確保 Azure RemoteApp 會自動調整大小以符合您的容量，而且會修補每個執行個體。</span><span class="sxs-lookup"><span data-stu-id="ec825-122">This ensures that as Azure RemoteApp auto-scales to meet your capacity, each instance is patched.</span></span>  
* <span data-ttu-id="ec825-123">請確認您有安全和可靠的 Active Directory Federation Services (AD FS) 部署。</span><span class="sxs-lookup"><span data-stu-id="ec825-123">Make sure your Active Directory Federation Services (AD FS) deployment is secure and reliable.</span></span> <span data-ttu-id="ec825-124">否則，用戶端驗證可能會失敗，導致使用者無法存取 Azure RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="ec825-124">Otherwise client authentications might fail, preventing users from accessing Azure RemoteApp.</span></span>
* <span data-ttu-id="ec825-125">使用安裝的應用程式、角色或功能設定範本映像，使它們成為無狀態。</span><span class="sxs-lookup"><span data-stu-id="ec825-125">Configure template images with installed applications, roles, or features such that they are stateless.</span></span> <span data-ttu-id="ec825-126">它們不應依賴持續性狀態之 RemoteApp 服務中的任何虛擬機器執行個體。</span><span class="sxs-lookup"><span data-stu-id="ec825-126">They should not rely on any instances of the virtual machines in a RemoteApp service being in a persistent state.</span></span>
  * <span data-ttu-id="ec825-127">將所有使用者資料儲存在使用者設定檔或服務的其他外部儲存體位置，例如內部部署的檔案共用或 OneDrive。</span><span class="sxs-lookup"><span data-stu-id="ec825-127">Store all user data in user profiles or other storage locations external to the service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="ec825-128">將共用資料儲存在服務的外部儲存體位置，例如內部部署的檔案共用或 OneDrive。</span><span class="sxs-lookup"><span data-stu-id="ec825-128">Store shared data in storage locations external to the service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="ec825-129">在範本映像中設定任何全系統的設定，而不是在服務的個別虛擬機器上設定。</span><span class="sxs-lookup"><span data-stu-id="ec825-129">Configure any system-wide settings in the template image rather than on individual virtual machines in a service.</span></span>
  * <span data-ttu-id="ec825-130">停用發佈之應用程式的自動軟體更新 - 改為手動套用至範本映像，並從範本部署之前測試它們。</span><span class="sxs-lookup"><span data-stu-id="ec825-130">Disable automatic software updates for published applications - instead apply them manually to the template image and test them before you deploy  from the template.</span></span>

