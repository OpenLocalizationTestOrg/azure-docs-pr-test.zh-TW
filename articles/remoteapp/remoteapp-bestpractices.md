---
title: "aaaAzure RemoteApp 最佳作法 |Microsoft 文件"
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
ms.openlocfilehash: f4d09ef30816eaebb74b69f26f3242c69ea27591
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a><span data-ttu-id="db15a-103">設定和使用 Azure RemoteApp 的最佳做法</span><span class="sxs-lookup"><span data-stu-id="db15a-103">Best practices for configuring and using Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="db15a-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="db15a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="db15a-105">讀取 hello[公告](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="db15a-105">Read hello [announcement](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) for details.</span></span>
> 
> 

<span data-ttu-id="db15a-106">hello 下列資訊可協助您設定及有效率地使用 Azure RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="db15a-106">hello following information can help you configure and use Azure RemoteApp productively.</span></span>

## <a name="connectivity"></a><span data-ttu-id="db15a-107">連線能力</span><span class="sxs-lookup"><span data-stu-id="db15a-107">Connectivity</span></span>
* <span data-ttu-id="db15a-108">一律使用最新用戶端版本 hello。</span><span class="sxs-lookup"><span data-stu-id="db15a-108">Always use hello latest client version.</span></span> <span data-ttu-id="db15a-109">使用舊版的用戶端可能會造成連線問題和其他降級的體驗。</span><span class="sxs-lookup"><span data-stu-id="db15a-109">Using older clients might result in connectivity issues and other degraded experiences.</span></span> <span data-ttu-id="db15a-110">啟用應用程式自動更新為您的裝置，可確保該 hello 最新的用戶端永遠都會安裝。</span><span class="sxs-lookup"><span data-stu-id="db15a-110">Enabling automatic application updates for your device will ensure that hello latest client is always installed.</span></span>
* <span data-ttu-id="db15a-111">一律使用 hello 最穩定且可靠網際網路連線可用 tooyou。</span><span class="sxs-lookup"><span data-stu-id="db15a-111">Always use hello most stable and reliable internet connection available tooyou.</span></span>  
* <span data-ttu-id="db15a-112">請使用支援的 Proxy 連線以獲得最佳連線效能。</span><span class="sxs-lookup"><span data-stu-id="db15a-112">Use only supported proxy connections for optimal connectivity performance.</span></span>  <span data-ttu-id="db15a-113">不支援 hello SOCKS proxy。</span><span class="sxs-lookup"><span data-stu-id="db15a-113">hello SOCKS proxy is not supported.</span></span>

## <a name="applications"></a><span data-ttu-id="db15a-114">應用程式</span><span class="sxs-lookup"><span data-stu-id="db15a-114">Applications</span></span>
* <span data-ttu-id="db15a-115">儲存並關閉 RemoteApp 應用程式，當您完成 hello 應用程式時。</span><span class="sxs-lookup"><span data-stu-id="db15a-115">Save and close RemoteApp applications when you are done with hello application.</span></span> <span data-ttu-id="db15a-116">未關閉 hello 應用程式可能會導致資料遺失。</span><span class="sxs-lookup"><span data-stu-id="db15a-116">Not closing hello application might result in data loss.</span></span>
* <span data-ttu-id="db15a-117">在 Azure RemoteApp 中使用自訂應用程式之前，請先進行驗證。</span><span class="sxs-lookup"><span data-stu-id="db15a-117">Validate custom applications before using them in Azure RemoteApp.</span></span> <span data-ttu-id="db15a-118">這包括確保它們有效多重工作階段的平台上並不會消耗不必要的資源，例如記憶體和 CPU 可能會佔用 hello 中的另一位使用者的相同集合。</span><span class="sxs-lookup"><span data-stu-id="db15a-118">This includes ensuring they work on a multi-session platform and don’t consume unnecessary resources such as memory and CPU that might starve another user in hello same collection.</span></span> <span data-ttu-id="db15a-119">詳細資訊，請下載並檢閱 hello[遠端桌面服務的應用程式相容性最佳作法](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf)。</span><span class="sxs-lookup"><span data-stu-id="db15a-119">For information, download and review hello [Application Compatibility Best Practices for Remote Desktop Services](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span></span>

## <a name="configuration-and-management"></a><span data-ttu-id="db15a-120">設定和管理</span><span class="sxs-lookup"><span data-stu-id="db15a-120">Configuration and management</span></span>
* <span data-ttu-id="db15a-121">將您的範本映像，向上 toodate，視需要安裝軟體更新和其他重大修正程式。</span><span class="sxs-lookup"><span data-stu-id="db15a-121">Keep your template images up toodate, installing software updates and other critical fixes as needed.</span></span> <span data-ttu-id="db15a-122">這可確保當 Azure RemoteApp 自動縮放 toomeet 已修補程式的容量，每個執行個體。</span><span class="sxs-lookup"><span data-stu-id="db15a-122">This ensures that as Azure RemoteApp auto-scales toomeet your capacity, each instance is patched.</span></span>  
* <span data-ttu-id="db15a-123">請確認您有安全和可靠的 Active Directory Federation Services (AD FS) 部署。</span><span class="sxs-lookup"><span data-stu-id="db15a-123">Make sure your Active Directory Federation Services (AD FS) deployment is secure and reliable.</span></span> <span data-ttu-id="db15a-124">否則，用戶端驗證可能會失敗，導致使用者無法存取 Azure RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="db15a-124">Otherwise client authentications might fail, preventing users from accessing Azure RemoteApp.</span></span>
* <span data-ttu-id="db15a-125">使用安裝的應用程式、角色或功能設定範本映像，使它們成為無狀態。</span><span class="sxs-lookup"><span data-stu-id="db15a-125">Configure template images with installed applications, roles, or features such that they are stateless.</span></span> <span data-ttu-id="db15a-126">它們不應該仰賴 hello 中的虛擬機器中的永續性狀態是 RemoteApp 服務的任何執行個體。</span><span class="sxs-lookup"><span data-stu-id="db15a-126">They should not rely on any instances of hello virtual machines in a RemoteApp service being in a persistent state.</span></span>
  * <span data-ttu-id="db15a-127">所有使用者資料都儲存使用者設定檔或其他儲存體位置 toohello 外部服務，例如在內部部署的檔案共用或 OneDrive。</span><span class="sxs-lookup"><span data-stu-id="db15a-127">Store all user data in user profiles or other storage locations external toohello service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="db15a-128">例如，在內部部署的檔案共用或 OneDrive 儲存體位置 toohello 外部服務，儲存共用的資料。</span><span class="sxs-lookup"><span data-stu-id="db15a-128">Store shared data in storage locations external toohello service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="db15a-129">在 hello 範本映像，而不是在服務中的個別虛擬機器上設定任何的全系統設定。</span><span class="sxs-lookup"><span data-stu-id="db15a-129">Configure any system-wide settings in hello template image rather than on individual virtual machines in a service.</span></span>
  * <span data-ttu-id="db15a-130">停用自動軟體更新已發行的應用程式-改為手動加以套用 toohello 範本映像，並測試它們，然後再從 hello 範本部署。</span><span class="sxs-lookup"><span data-stu-id="db15a-130">Disable automatic software updates for published applications - instead apply them manually toohello template image and test them before you deploy  from hello template.</span></span>

