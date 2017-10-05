---
title: "建立 RemoteApp 混合式集合疑難排解 | Microsoft Docs"
description: "了解如何疑難排解 RemoteApp 混合式集合建立失敗"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: b32033ee-8d52-4e74-bb78-86ca873c34e2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: a486dcb3f994cd78311ee86521a6792a4d57438e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a><span data-ttu-id="68912-103">建立 Azure RemoteApp 混合式集合疑難排解</span><span class="sxs-lookup"><span data-stu-id="68912-103">Troubleshoot creating Azure RemoteApp hybrid collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="68912-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="68912-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="68912-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="68912-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="68912-106">「混合式收藏」裝載於 Azure 雲端中，並在其中儲存資料，但也會讓使用者存取儲存在您區域網路上的資料和資源。</span><span class="sxs-lookup"><span data-stu-id="68912-106">A hybrid collection is hosted in and stores data in the Azure cloud but also lets users access data and resources stored on your local network.</span></span> <span data-ttu-id="68912-107">使用者可以使用與 Azure Active Directory 同步處理或同盟的公司認證進行登入，以存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="68912-107">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span></span> <span data-ttu-id="68912-108">您可以部署使用現有 Azure 虛擬網路的混合式集合，或者可以建立新的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="68912-108">You can deploy a hybrid collection that uses an existing Azure Virtual Network, or you can create a new virtual network.</span></span> <span data-ttu-id="68912-109">建議您建立或使用虛擬網路子網路，而其預期 Azure RemoteApp 未來成長的 CIDR 範圍夠大。</span><span class="sxs-lookup"><span data-stu-id="68912-109">We recommend that you create or use a virtual network subnet with a CIDR range large enough for expected future growth for Azure RemoteApp.</span></span>

<span data-ttu-id="68912-110">是否尚未建立集合？</span><span class="sxs-lookup"><span data-stu-id="68912-110">Haven't created your collection yet?</span></span> <span data-ttu-id="68912-111">如需步驟，請參閱 [建立混合式集合](remoteapp-create-hybrid-deployment.md) 。</span><span class="sxs-lookup"><span data-stu-id="68912-111">See [Create a hybrid collection](remoteapp-create-hybrid-deployment.md) for the steps.</span></span>

<span data-ttu-id="68912-112">如果在建立集合時發生問題，或集合未如您預期地運作，請參閱下列資訊。</span><span class="sxs-lookup"><span data-stu-id="68912-112">If you are having trouble creating your collection, or if the collection isn't working the way you think it should, check out the following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="68912-113">您的映像無效</span><span class="sxs-lookup"><span data-stu-id="68912-113">Your image is invalid</span></span>
<span data-ttu-id="68912-114">如果您在等候 Azure 佈建集合時，看到如「GoldImageInvalid」的訊息，表示範本映像不符合 [已定義的映像需求](remoteapp-imagereqs.md)。</span><span class="sxs-lookup"><span data-stu-id="68912-114">If you see a message like, "GoldImageInvalid" when you are waiting for Azure to provision your collection, it means that your template image doesn't meet the [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="68912-115">因此，請閱讀 [需求](remoteapp-imagereqs.md)並修正映像，然後再嘗試重新建立集合。</span><span class="sxs-lookup"><span data-stu-id="68912-115">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try to create your collection again.</span></span>

## <a name="does-your-vnet-have-network-security-groups-defined"></a><span data-ttu-id="68912-116">VNET 是否已定義網路安全性群組？</span><span class="sxs-lookup"><span data-stu-id="68912-116">Does your VNET have network security groups defined?</span></span>
<span data-ttu-id="68912-117">如果您已在正用於您集合的子網路上定義網路安全性群組，請確定可以在子網路內存取這些 [URL 和連接埠](remoteapp-ports.md) 。</span><span class="sxs-lookup"><span data-stu-id="68912-117">If you have network security groups defined on the subnet you are using for your collection, make sure these [URLs and ports](remoteapp-ports.md) are accessible from within your subnet.</span></span>

<span data-ttu-id="68912-118">您可以將額外網路安全性群組新增至子網路中您所部署的 VM，以進行更嚴格的控制。</span><span class="sxs-lookup"><span data-stu-id="68912-118">You can add additional network security groups to the VMs deployed by you in the subnet for tighter control.</span></span>

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a><span data-ttu-id="68912-119">是否正在使用專屬 DNS 伺服器？</span><span class="sxs-lookup"><span data-stu-id="68912-119">Are you using your own DNS servers?</span></span> <span data-ttu-id="68912-120">是否可以從 VNET 子網路存取它們？</span><span class="sxs-lookup"><span data-stu-id="68912-120">And are they accessible from your VNET subnet?</span></span>
> [!NOTE]
> <span data-ttu-id="68912-121">您必須確定 VNET 中的 DNS 伺服器都已啟動，而且永遠能夠解析裝載於 VNET 中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="68912-121">You have to make sure the DNS servers in your VNET are always up and always able to resolve the virtual machines hosted in the VNET.</span></span> <span data-ttu-id="68912-122">請勿在此使用 Google DNS。</span><span class="sxs-lookup"><span data-stu-id="68912-122">Don't use Google DNS for this.</span></span>
> 
> 

<span data-ttu-id="68912-123">對於混合式集合，您使用專屬 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="68912-123">For hybrid collections you use your own DNS servers.</span></span> <span data-ttu-id="68912-124">您可以在網路組態結構描述中或在建立虛擬網路時透過管理入口網站來指定它們。</span><span class="sxs-lookup"><span data-stu-id="68912-124">You specify them in your network configuration schema or through the management portal when you create your virtual network.</span></span> <span data-ttu-id="68912-125">DNS 伺服器的使用順序就是針對進行容錯移轉所指定的順序 (而非循環配置資源)。</span><span class="sxs-lookup"><span data-stu-id="68912-125">DNS servers are used in the order that they are specified in a failover manner (as opposed to round robin).</span></span>  
<span data-ttu-id="68912-126">請參閱 [VM 與角色執行個體的名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) ，以確定您的 DNS 伺服器已正確設定。</span><span class="sxs-lookup"><span data-stu-id="68912-126">Please refer to [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) to make sure your DNS servers are configured correcly.</span></span>

<span data-ttu-id="68912-127">請確定可以從針對這個集合所指定的 VNET 子網路中存取和使用您集合的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="68912-127">Make sure the DNS servers for your collection are accessible and available from the VNET subnet you specified for this collection.</span></span>

<span data-ttu-id="68912-128">例如：</span><span class="sxs-lookup"><span data-stu-id="68912-128">For example:</span></span>

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![定義 DNS](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a><span data-ttu-id="68912-130">是否在您的集合中使用 Active Directory 網域控制站？</span><span class="sxs-lookup"><span data-stu-id="68912-130">Are you using an Active Directory domain controller in your collection?</span></span>
<span data-ttu-id="68912-131">目前只有一個 Active Directory 網域才能與 Azure RemoteApp 相關聯。</span><span class="sxs-lookup"><span data-stu-id="68912-131">Currently only one Active Directory domain can be associated with Azure RemoteApp.</span></span> <span data-ttu-id="68912-132">混合式集合僅支援已使用 Windows Server Active Directory 部署之 DirSync 工具同步的 Azure Active Directory 帳戶；更具體而言，就是已同步「密碼同步化」選項，或已同步設定 Active Directory Federation Services (AD FS) 同盟。</span><span class="sxs-lookup"><span data-stu-id="68912-132">The hybrid collection supports only Azure Active Directory accounts that have been synced using DirSync tool from a Windows Server Active Directory deployment; specifically, either synced with the Password Synchronization option or synced with Active Directory Federation Services (AD FS) federation configured.</span></span> <span data-ttu-id="68912-133">您必須建立一個自訂網域，以符合內部部署之網域的 UPN 網域尾碼，並設定目錄整合。</span><span class="sxs-lookup"><span data-stu-id="68912-133">You need to create a custom domain that matches the UPN domain suffix for your on-premises domain and set up directory integration.</span></span>

<span data-ttu-id="68912-134">如需詳細資訊，請參閱 [設定 Azure RemoteApp 的 Active Directory](remoteapp-ad.md) 。</span><span class="sxs-lookup"><span data-stu-id="68912-134">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for more information.</span></span>

<span data-ttu-id="68912-135">請確定提供的網域詳細資料有效，而且可以從用於 Azure 遠端應用程式的子網路中所建立的 VM 連線網域控制站。</span><span class="sxs-lookup"><span data-stu-id="68912-135">Make sure the domain details provided are valid and the domain controller is reachable from the VM created in the subnet used for Azure Remote App.</span></span> <span data-ttu-id="68912-136">也請確定提供的服務帳戶認證具有將電腦新增至所提供網域的權限，而且可以從 VNET 中所提供的 DNS 解析提供的 AD 名稱。</span><span class="sxs-lookup"><span data-stu-id="68912-136">Also make sure the service account credentials supplied have permissions to add computers to the provided domain and that the AD name provided can be resolved from the DNS provided in the VNET.</span></span>

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a><span data-ttu-id="68912-137">在您建立集合時指定哪個網域名稱？</span><span class="sxs-lookup"><span data-stu-id="68912-137">What domain name did you specify when you created your collection?</span></span>
<span data-ttu-id="68912-138">建立或新增的網域名稱必須是內部網域名稱 (非 Azure AD 網域名稱)，而且必須是可解析的 DNS 格式 (contoso.local)。</span><span class="sxs-lookup"><span data-stu-id="68912-138">The domain name you created or added must be an internal domain name (not your Azure AD domain name) and must be in resolvable DNS format (contoso.local).</span></span> <span data-ttu-id="68912-139">例如，您有 Active Directory 內部名稱 (contoso.local) 和 Active Directory UPN (contoso.com) - 您必須在建立集合時使用內部名稱。</span><span class="sxs-lookup"><span data-stu-id="68912-139">For example, you have an Active Directory internal name (contoso.local) and an Active Directory UPN (contoso.com) - you have to use the internal name when you create your collection.</span></span>

