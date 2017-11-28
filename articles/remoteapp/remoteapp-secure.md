---
title: "保護 Azure RemoteApp 中的應用程式和資源 | Microsoft Docs"
description: "了解如何鎖定 Azure RemoteApp 中的應用程式和資源"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7fbade87-a453-426d-bfa5-c72227ea83cd
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 1c052906788f0f4fe4ca9fd6d3af63336245174a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="secure-apps-and-resources-in-azure-remoteapp"></a><span data-ttu-id="98363-103">保護 Azure RemoteApp 中的應用程式和資源</span><span class="sxs-lookup"><span data-stu-id="98363-103">Secure apps and resources in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="98363-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="98363-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="98363-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="98363-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="98363-106">Azure RemoteApp 可讓使用者存取集中管理的 Windows 應用程式，這樣可讓您控制使用者可以或不可以執行的動作。</span><span class="sxs-lookup"><span data-stu-id="98363-106">Azure RemoteApp provides users access to centrally-managed Windows apps, which lets you control what your users can and can't do.</span></span>  <span data-ttu-id="98363-107">當使用者從未受管理的裝置連接 (例如其個人 Macbook)，而且您想要控制使用者存取權或體驗時，這特別有用。</span><span class="sxs-lookup"><span data-stu-id="98363-107">This is particularly useful when the user is connecting from an unmanaged device (like their personal Macbook) and you want to control the user access or experience.</span></span>

<span data-ttu-id="98363-108">例如，如果您使用 Active Directory 進行使用者驗證，而且您想要防止使用者複製應用程式的資料，您可以設定遠端桌面群組原則來禁止使用者複製資料。</span><span class="sxs-lookup"><span data-stu-id="98363-108">For example, if you are using Active Directory for user authentication and you want to prevent your users from copying data out of an app, you can configure a Remote Desktop Group Policy to block users from copying data.</span></span>

<span data-ttu-id="98363-109">另一個例子是您想要對集合中的特定應用程式，封鎖網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="98363-109">Another example is if you want to block internet access for a particular app in your collection.</span></span> <span data-ttu-id="98363-110">當您建立集合的映像時，您可以建立 Windows 防火牆規則來封鎖存取。</span><span class="sxs-lookup"><span data-stu-id="98363-110">You can create a Windows Firewall rule that blocks the access when you create the image for your collection.</span></span>

## <a name="implementation-options"></a><span data-ttu-id="98363-111">實作選項</span><span class="sxs-lookup"><span data-stu-id="98363-111">Implementation options</span></span>
  <span data-ttu-id="98363-112">以下是重要的實作選項，可以視需要個別使用或一起使用：</span><span class="sxs-lookup"><span data-stu-id="98363-112">Here are the key implementation options, which can be used individually or in tandem as needed:</span></span>

1. <span data-ttu-id="98363-113">如果您的 RemoteApp 集合已加入網域，您可以強制執行任何[群組原則](https://technet.microsoft.com/library/cc725828.aspx) ([這裡](../azure-subscription-service-limits.md)所述的閒置和中斷連線逾時原則除外)。</span><span class="sxs-lookup"><span data-stu-id="98363-113">If your RemoteApp collection is domain joined you can enforce any [Group Policy](https://technet.microsoft.com/library/cc725828.aspx) (with the exception of the Idle and Disconnect timeout policies described [here](../azure-subscription-service-limits.md)).</span></span>
2. <span data-ttu-id="98363-114">除了群組原則 (如果您的集合未加入網域，或您在 AD 中沒有正確的權限)，您也可以在範本映像中設定 [本機原則](https://technet.microsoft.com/library/cc775702.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="98363-114">As an alternative to Group Policy (if your collection is not domain joined or you don't have the right privileges in AD), you can configure [Local Polices](https://technet.microsoft.com/library/cc775702.aspx) into your template image.</span></span>  <span data-ttu-id="98363-115">請注意，當群組原則與本機原則發生衝突時，以群組原則為準。</span><span class="sxs-lookup"><span data-stu-id="98363-115">Note that group polices trump local policies when there is a conflict.</span></span>
3. <span data-ttu-id="98363-116">某些 OS/應用程式設定無法透過原則設定，但可以在設定範本映像時，使用 [RegEdit 工具](remoteapp-hybridtrouble.md)透過登錄機碼來設定。</span><span class="sxs-lookup"><span data-stu-id="98363-116">Some OS/app settings are not configurable via policy, but can be via registry key using the [RegEdit tool](remoteapp-hybridtrouble.md) while configuring your template image.</span></span>
4. <span data-ttu-id="98363-117">您可以使用 [Windows 防火牆](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) 來控制從網路進出執行應用程式的電腦。</span><span class="sxs-lookup"><span data-stu-id="98363-117">You can use [Windows Firewall](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) to control network access to and from the machine where the app is running.</span></span> <span data-ttu-id="98363-118">只要確定沒有封鎖這裡所定義的 URL 和連接埠即可。</span><span class="sxs-lookup"><span data-stu-id="98363-118">Just make sure you don't block the URLs and ports defined here.</span></span>
5. <span data-ttu-id="98363-119">您可以使用 [AppLocker](https://technet.microsoft.com/library/hh831440.aspx) 來控制使用者可以執行的應用程式和檔案。</span><span class="sxs-lookup"><span data-stu-id="98363-119">You can use [AppLocker](https://technet.microsoft.com/library/hh831440.aspx) to control which applications and files users can run.</span></span> <span data-ttu-id="98363-120">比方說，聰明的使用者可能在您用來建立集合的映像中，想出方法來執行您未發佈的應用程式 - AppLocker 可以排除這種情況。</span><span class="sxs-lookup"><span data-stu-id="98363-120">For example, savvy users can figure out how to run applications that you did not publish but that are available in the image you used to create the collection - AppLocker can block this.</span></span>

## <a name="detailed-information"></a><span data-ttu-id="98363-121">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="98363-121">Detailed information</span></span>
* <span data-ttu-id="98363-122">下列 RDS 原則可能最有用：</span><span class="sxs-lookup"><span data-stu-id="98363-122">The following RDS policies are likely to be most useful:</span></span>
  * [<span data-ttu-id="98363-123">裝置及資源重新導向</span><span class="sxs-lookup"><span data-stu-id="98363-123">Device and Resource Redirection</span></span>](https://technet.microsoft.com/library/ee791794.aspx)
  * [<span data-ttu-id="98363-124">印表機重新導向</span><span class="sxs-lookup"><span data-stu-id="98363-124">Printer Redirection</span></span>](https://technet.microsoft.com/library/ee791784.aspx)
  * <span data-ttu-id="98363-125">[設定檔](https://technet.microsoft.com/library/ee791865.aspx)。</span><span class="sxs-lookup"><span data-stu-id="98363-125">[Profiles](https://technet.microsoft.com/library/ee791865.aspx).</span></span>
* <span data-ttu-id="98363-126">請注意，透過 RemoteApp PowerShell 模組設定重新導向 (如[這裡](remoteapp-redirection.md)所示) 需要依賴用戶端機器強制執行原則，因此，如果安全性是主要目標，則您會想透過範本映像本機原則或群組原則來強制執行原則。</span><span class="sxs-lookup"><span data-stu-id="98363-126">Note that configuring redirections via the RemoteApp PowerShell module (as seen [here](remoteapp-redirection.md)) relies on the client machine to enforce the policy, so if security is the primary objective you'll want to enforce the policy via the template image local policy or via group policy.</span></span>
* <span data-ttu-id="98363-127">[Windows Server 2012 R2 原則](https://technet.microsoft.com/library/hh831791.aspx)。</span><span class="sxs-lookup"><span data-stu-id="98363-127">[Windows Server 2012 R2 policies](https://technet.microsoft.com/library/hh831791.aspx).</span></span>
* <span data-ttu-id="98363-128">[Office 2013 原則](https://technet.microsoft.com/library/cc178969.aspx) (包括[如何自訂 Office 工具列](https://technet.microsoft.com/library/cc179143.aspx))。</span><span class="sxs-lookup"><span data-stu-id="98363-128">[Office 2013 polices](https://technet.microsoft.com/library/cc178969.aspx) (including [how to customize the Office toolbar](https://technet.microsoft.com/library/cc179143.aspx)).</span></span>

