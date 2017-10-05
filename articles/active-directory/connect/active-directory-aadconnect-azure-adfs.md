---
title: "Azure 中的 Active Directory Federation Services | Microsoft Docs"
description: "在本文件中，您將了解如何在 Azure 中部署 AD FS 以獲得高可用性。"
keywords: "在 azure 中部署 AD FS, 部署 azure adfs, azure adfs, azure ad fs, 部署 adfs, 部署 ad fs, azure 中的 adfs, 在 azure 中部署 adfs, 在 azure 中部署 AD FS, adfs azure, AD FS 簡介, Azure, Azure 中的 AD FS, iaas, ADFS, 將 adfs 移至 azure"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 692a188c-badc-44aa-ba86-71c0e8074510
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ddd29a1230286de8999175498ee793f3b3ea24e2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="deploying-active-directory-federation-services-in-azure"></a><span data-ttu-id="89ec4-104">在 Azure 中部署 Active Directory 同盟服務</span><span class="sxs-lookup"><span data-stu-id="89ec4-104">Deploying Active Directory Federation Services in Azure</span></span>
<span data-ttu-id="89ec4-105">AD FS 提供簡化、安全的身分識別同盟和 Web 單一登入 (SSO) 功能。</span><span class="sxs-lookup"><span data-stu-id="89ec4-105">AD FS provides simplified, secured identity federation and Web single sign-on (SSO) capabilities.</span></span> <span data-ttu-id="89ec4-106">與 Azure AD 或 O365 同盟可讓使用者使用內部部署認證進行驗證，並存取雲端中的所有資源。</span><span class="sxs-lookup"><span data-stu-id="89ec4-106">Federation with Azure AD or O365 enables users to authenticate using on-premises credentials and access all resources in cloud.</span></span> <span data-ttu-id="89ec4-107">如此一來，就一定要有高可用性的 AD FS 基礎結構，以確保能夠存取內部部署和雲端中的資源。</span><span class="sxs-lookup"><span data-stu-id="89ec4-107">As a result, it becomes important to have a highly available AD FS infrastructure to ensure access to resources both on-premises and in the cloud.</span></span> <span data-ttu-id="89ec4-108">在 Azure 中部署 AD FS 有助於達成執行最低限度的工作所需要的高可用性。</span><span class="sxs-lookup"><span data-stu-id="89ec4-108">Deploying AD FS in Azure can help achieve the high availability required with minimal efforts.</span></span>
<span data-ttu-id="89ec4-109">在 Azure 中部署 AD FS 有幾項優點，以下列出其中幾點︰</span><span class="sxs-lookup"><span data-stu-id="89ec4-109">There are several advantages of deploying AD FS in Azure, a few of them are listed below:</span></span>

* <span data-ttu-id="89ec4-110">**高可用性** – 憑借 Azure 可用性設定組的能力，您可以確保高可用性的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="89ec4-110">**High Availability** - With the power of Azure Availability Sets, you ensure a highly available infrastructure.</span></span>
* <span data-ttu-id="89ec4-111">**容易調整** – 需要更多效能？</span><span class="sxs-lookup"><span data-stu-id="89ec4-111">**Easy to Scale** – Need more performance?</span></span> <span data-ttu-id="89ec4-112">只要在 Azure 中按幾下，就能輕鬆地移轉至更強大的機器</span><span class="sxs-lookup"><span data-stu-id="89ec4-112">Easily migrate to more powerful machines by just a few clicks in Azure</span></span>
* <span data-ttu-id="89ec4-113">**跨異地備援** – 使用 Azure 異地備援，您可以確保基礎結構在全球各地均具有高可用性</span><span class="sxs-lookup"><span data-stu-id="89ec4-113">**Cross-Geo Redundancy** – With Azure Geo Redundancy you can be assured that your infrastructure is highly available across the globe</span></span>
* <span data-ttu-id="89ec4-114">**容易管理** – 透過 Azure 入口網站中極簡化的管理選項，基礎結構管理起來既容易又省事</span><span class="sxs-lookup"><span data-stu-id="89ec4-114">**Easy to Manage** – With highly simplified management options in Azure portal, managing your infrastructure is very easy and hassle-free</span></span> 

## <a name="design-principles"></a><span data-ttu-id="89ec4-115">設計原則</span><span class="sxs-lookup"><span data-stu-id="89ec4-115">Design principles</span></span>
![部署設計](./media/active-directory-aadconnect-azure-adfs/deployment.png)

<span data-ttu-id="89ec4-117">上圖顯示建議用來在 Azure 中部署 AD FS 基礎結構的基本拓撲。</span><span class="sxs-lookup"><span data-stu-id="89ec4-117">The diagram above shows the recommended basic topology to start deploying your AD FS infrastructure in Azure.</span></span> <span data-ttu-id="89ec4-118">以下列出拓撲的各個元件背後的原理︰</span><span class="sxs-lookup"><span data-stu-id="89ec4-118">The principles behind the various components of the topology are listed below:</span></span>

* <span data-ttu-id="89ec4-119">**DC/ADFS 伺服器**︰如果您的使用者人數少於 1,000 名，可以直接在網域控制站上安裝 AD FS 角色。</span><span class="sxs-lookup"><span data-stu-id="89ec4-119">**DC / ADFS Servers**: If you have fewer than 1,000 users you can simply install AD FS role on your domain controllers.</span></span> <span data-ttu-id="89ec4-120">如果不想影響網域控制站的效能，或者使用者人數超過 1,000 名，則請在不同伺服器部署 AD FS。</span><span class="sxs-lookup"><span data-stu-id="89ec4-120">If you do not want any performance impact on the domain controllers or if you have more than 1,000 users, then deploy AD FS on separate servers.</span></span>
* <span data-ttu-id="89ec4-121">**WAP 伺服器** ︰一定要部署 Web 應用程式 Proxy 伺服器，才能讓不在公司網路內的使用者也可以連線到 AD FS。</span><span class="sxs-lookup"><span data-stu-id="89ec4-121">**WAP Server** – it is necessary to deploy Web Application Proxy servers, so that users can reach the AD FS when they are not on the company network also.</span></span>
* <span data-ttu-id="89ec4-122">**DMZ**︰Web 應用程式 Proxy 伺服器將會置於 DMZ，而且 DMZ 與內部子網路之間只允許進行 TCP/443 存取。</span><span class="sxs-lookup"><span data-stu-id="89ec4-122">**DMZ**: The Web Application Proxy servers will be placed in the DMZ and ONLY TCP/443 access is allowed between the DMZ and the internal subnet.</span></span>
* <span data-ttu-id="89ec4-123">**負載平衡器**︰為了確保 AD FS 和 Web 應用程式 Proxy 伺服器具有高可用性，建議您針對 AD FS 伺服器使用內部負載平衡器，針對 Web 應用程式 Proxy 伺服器使用 Azure Load Balancer。</span><span class="sxs-lookup"><span data-stu-id="89ec4-123">**Load Balancers**: To ensure high availability of AD FS and Web Application Proxy servers, we recommend using an internal load balancer for AD FS servers and Azure Load Balancer for Web Application Proxy servers.</span></span>
* <span data-ttu-id="89ec4-124">**可用性設定組**︰為了提供 AD FS 部署備援，建議您將工作負載類似的兩個以上的虛擬機器分在同一個可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="89ec4-124">**Availability Sets**: To provide redundancy to your AD FS deployment, it is recommended that you group two or more virtual machines in an Availability Set for similar workloads.</span></span> <span data-ttu-id="89ec4-125">這項組態可以確保在規劃或未規劃的維護事件發生期間，至少有一部虛擬機器可以使用。</span><span class="sxs-lookup"><span data-stu-id="89ec4-125">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine will be available</span></span>
* <span data-ttu-id="89ec4-126">**儲存體帳戶**︰建議您擁有兩個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="89ec4-126">**Storage Accounts**: It is recommended to have two storage accounts.</span></span> <span data-ttu-id="89ec4-127">只擁有一個儲存體帳戶可能會產生單一失敗點，而且如果儲存體帳戶失效 (雖然不太可能發生)，則會無法使用部署。</span><span class="sxs-lookup"><span data-stu-id="89ec4-127">Having a single storage account can lead to creation of a single point of failure and can cause the deployment to become unavailable in an unlikely scenario where the storage account goes down.</span></span> <span data-ttu-id="89ec4-128">兩個儲存體帳戶則有助於讓每條故障路線有一個相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="89ec4-128">Two storage accounts will help associate one storage account for each fault line.</span></span>
* <span data-ttu-id="89ec4-129">**網路隔離**︰請將 Web 應用程式 Proxy 伺服器部署在不同的 DMZ 網路。</span><span class="sxs-lookup"><span data-stu-id="89ec4-129">**Network segregation**:  Web Application Proxy servers should be deployed in a separate DMZ network.</span></span> <span data-ttu-id="89ec4-130">您可以將一個虛擬網路分割成兩個子網路，然後在隔離的子網路部署 Web 應用程式 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="89ec4-130">You can divide one virtual network into two subnets and then deploy the Web Application Proxy server(s) in an isolated subnet.</span></span> <span data-ttu-id="89ec4-131">您可以簡單地設定每個子網路的網路安全性群組設定，並只允許兩個子網路之間進行必要的通訊。</span><span class="sxs-lookup"><span data-stu-id="89ec4-131">You can simply configure the network security group settings for each subnet and allow only required communication between the two subnets.</span></span> <span data-ttu-id="89ec4-132">下面會提供每種部署案例的其他詳細資料</span><span class="sxs-lookup"><span data-stu-id="89ec4-132">More details are given per deployment scenario below</span></span>

## <a name="steps-to-deploy-ad-fs-in-azure"></a><span data-ttu-id="89ec4-133">在 Azure 中部署 AD FS 的步驟</span><span class="sxs-lookup"><span data-stu-id="89ec4-133">Steps to deploy AD FS in Azure</span></span>
<span data-ttu-id="89ec4-134">本節所述步驟會概述在 Azure 中部署如下所示的 AD FS 基礎結構的指南。</span><span class="sxs-lookup"><span data-stu-id="89ec4-134">The steps mentioned in this section outline the guide to deploy the below depicted AD FS infrastructure in Azure.</span></span>

### <a name="1-deploying-the-network"></a><span data-ttu-id="89ec4-135">1.部署網路</span><span class="sxs-lookup"><span data-stu-id="89ec4-135">1. Deploying the network</span></span>
<span data-ttu-id="89ec4-136">如上所述，您可以在單一虛擬網路中建立兩個子網路，或是建立兩個完全不同的虛擬網路 (VNet)。</span><span class="sxs-lookup"><span data-stu-id="89ec4-136">As outlined above, you can either create two subnets in a single virtual network or else create two completely different virtual networks (VNet).</span></span> <span data-ttu-id="89ec4-137">本文內容著重於部署單一虛擬網路，再將它分成兩個子網路。</span><span class="sxs-lookup"><span data-stu-id="89ec4-137">This article will focus on deploying a single virtual network and divide it into two subnets.</span></span> <span data-ttu-id="89ec4-138">就目前來說，這個方法較為簡單，因為如果是兩個不同的 VNet，就必須要有 VNet 對 VNet 閘道才能進行通訊。</span><span class="sxs-lookup"><span data-stu-id="89ec4-138">This is currently an easier approach as two separate VNets would require a VNet to VNet gateway for communications.</span></span>

<span data-ttu-id="89ec4-139">**1.1 建立虛擬網路**</span><span class="sxs-lookup"><span data-stu-id="89ec4-139">**1.1 Create virtual network**</span></span>

![建立虛擬網路](./media/active-directory-aadconnect-azure-adfs/deploynetwork1.png)

<span data-ttu-id="89ec4-141">在 Azure 入口網站中選取虛擬網路，然後只需要按一下就可以立即部署虛擬網路和一個子網路。</span><span class="sxs-lookup"><span data-stu-id="89ec4-141">In the Azure portal, select virtual network and you can deploy the virtual network and one subnet immediately with just one click.</span></span> <span data-ttu-id="89ec4-142">INT 子網路也會定義好，立即可供要新增的 VM 使用。</span><span class="sxs-lookup"><span data-stu-id="89ec4-142">INT subnet is also defined and is ready now for VMs to be added.</span></span>
<span data-ttu-id="89ec4-143">下一個步驟是在網路中新增另一個子網路，也就是 DMZ 子網路。</span><span class="sxs-lookup"><span data-stu-id="89ec4-143">The next step is to add another subnet to the network, i.e. the DMZ subnet.</span></span> <span data-ttu-id="89ec4-144">為了建立 DMS 子網路，請直接</span><span class="sxs-lookup"><span data-stu-id="89ec4-144">To create the DMZ subnet, simply</span></span>

* <span data-ttu-id="89ec4-145">選取新建立的網路</span><span class="sxs-lookup"><span data-stu-id="89ec4-145">Select the newly created network</span></span>
* <span data-ttu-id="89ec4-146">在屬性中選取子網路</span><span class="sxs-lookup"><span data-stu-id="89ec4-146">In the properties select subnet</span></span>
* <span data-ttu-id="89ec4-147">在子網路面板中，按一下新增按鈕</span><span class="sxs-lookup"><span data-stu-id="89ec4-147">In the subnet panel click on the add button</span></span>
* <span data-ttu-id="89ec4-148">提供用來建立子網路的子網路名稱和位址空間資訊</span><span class="sxs-lookup"><span data-stu-id="89ec4-148">Provide the subnet name and address space information to create the subnet</span></span>

![子網路](./media/active-directory-aadconnect-azure-adfs/deploynetwork2.png)

![子網路 DMZ](./media/active-directory-aadconnect-azure-adfs/deploynetwork3.png)

<span data-ttu-id="89ec4-151">**1.2.建立網路安全性群組**</span><span class="sxs-lookup"><span data-stu-id="89ec4-151">**1.2. Creating the network security groups**</span></span>

<span data-ttu-id="89ec4-152">網路安全性群組 (NSG) 包含存取控制清單 (ACL) 規則的清單，可允許或拒絕虛擬網路中 VM 執行個體的網路流量。</span><span class="sxs-lookup"><span data-stu-id="89ec4-152">A Network security group (NSG) contains a list of Access Control List (ACL) rules that allow or deny network traffic to your VM instances in a Virtual Network.</span></span> <span data-ttu-id="89ec4-153">NSG 可與子網路或該子網路內的個別 VM 執行個體相關聯。</span><span class="sxs-lookup"><span data-stu-id="89ec4-153">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="89ec4-154">當 NSG 與子網路相關聯時，ACL 規則便會套用至該子網路中的所有 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="89ec4-154">When an NSG is associated with a subnet, the ACL rules apply to all the VM instances in that subnet.</span></span>
<span data-ttu-id="89ec4-155">為了進行本指南，我們會建立兩個 NSG︰分別提供給內部網路和 DMZ 使用。</span><span class="sxs-lookup"><span data-stu-id="89ec4-155">For the purpose of this guidance, we will create two NSGs: one each for an internal network and a DMZ.</span></span> <span data-ttu-id="89ec4-156">其各自的標籤為 NSG_INT 和 NSG_DMZ。</span><span class="sxs-lookup"><span data-stu-id="89ec4-156">They will be labeled NSG_INT and NSG_DMZ respectively.</span></span>

![建立 NSG](./media/active-directory-aadconnect-azure-adfs/creatensg1.png)

<span data-ttu-id="89ec4-158">建立好 NSG 之後，其輸入和輸出規則皆為 0。</span><span class="sxs-lookup"><span data-stu-id="89ec4-158">After the NSG is created, there will be 0 inbound and 0 outbound rules.</span></span> <span data-ttu-id="89ec4-159">一旦各自伺服器上的角色安裝好並正常運作，就可以根據所需的安全性層級建立輸入和輸出規則。</span><span class="sxs-lookup"><span data-stu-id="89ec4-159">Once the roles on the respective servers are installed and functional, then the inbound and outbound rules can be made according to the desired level of security.</span></span>

![初始化 NSG](./media/active-directory-aadconnect-azure-adfs/nsgint1.png)

<span data-ttu-id="89ec4-161">建立好所有 NSG 之後，請建立 NSG_INT 與子網路 INT 的關聯，以及 NSG_DMZ 與子網路 DMS 的關聯。</span><span class="sxs-lookup"><span data-stu-id="89ec4-161">After the NSGs are created, associate NSG_INT with subnet INT and NSG_DMZ with subnet DMZ.</span></span> <span data-ttu-id="89ec4-162">下面提供了範例螢幕擷取畫面︰</span><span class="sxs-lookup"><span data-stu-id="89ec4-162">An example screenshot is given below:</span></span>

![NSG 設定](./media/active-directory-aadconnect-azure-adfs/nsgconfigure1.png)

* <span data-ttu-id="89ec4-164">按一下 [子網路] 以開啟子網路的面板</span><span class="sxs-lookup"><span data-stu-id="89ec4-164">Click on Subnets to open the panel for subnets</span></span>
* <span data-ttu-id="89ec4-165">選取要與 NSG 關聯的子網路</span><span class="sxs-lookup"><span data-stu-id="89ec4-165">Select the subnet to associate with the NSG</span></span> 

<span data-ttu-id="89ec4-166">完成設定後，[子網路] 面板看起來應該會像下圖︰</span><span class="sxs-lookup"><span data-stu-id="89ec4-166">After configuration, the panel for Subnets should look like below:</span></span>

![NSG 之後的子網路](./media/active-directory-aadconnect-azure-adfs/nsgconfigure2.png)

<span data-ttu-id="89ec4-168">**1.3.建立與內部部署的連線**</span><span class="sxs-lookup"><span data-stu-id="89ec4-168">**1.3. Create Connection to on-premises**</span></span>

<span data-ttu-id="89ec4-169">我們必須要連線至內部部署，才能在 Azure 中部署網域控制站 (DC)。</span><span class="sxs-lookup"><span data-stu-id="89ec4-169">We will need a connection to on-premises in order to deploy the domain controller (DC) in azure.</span></span> <span data-ttu-id="89ec4-170">Azure 提供了各種連線選項，供您將內部部署基礎結構連接到 Azure 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="89ec4-170">Azure offers various connectivity options to connect your on-premises infrastructure to your Azure infrastructure.</span></span>

* <span data-ttu-id="89ec4-171">點對站</span><span class="sxs-lookup"><span data-stu-id="89ec4-171">Point-to-site</span></span>
* <span data-ttu-id="89ec4-172">虛擬網路站對站</span><span class="sxs-lookup"><span data-stu-id="89ec4-172">Virtual Network Site-to-site</span></span>
* <span data-ttu-id="89ec4-173">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="89ec4-173">ExpressRoute</span></span>

<span data-ttu-id="89ec4-174">建議您使用 ExpressRoute。</span><span class="sxs-lookup"><span data-stu-id="89ec4-174">It is recommended to use ExpressRoute.</span></span> <span data-ttu-id="89ec4-175">ExpressRoute 可讓您在 Azure 資料中心和內部部署或共置環境中的基礎結構之間建立私人連接。</span><span class="sxs-lookup"><span data-stu-id="89ec4-175">ExpressRoute lets you create private connections between Azure datacenters and infrastructure that’s on your premises or in a co-location environment.</span></span> <span data-ttu-id="89ec4-176">ExpressRoute 連線不會經過公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="89ec4-176">ExpressRoute connections do not go over the public Internet.</span></span> <span data-ttu-id="89ec4-177">相較於透過網際網路的一般連線，其可提供更為可靠、速度更快、延遲更低且安全性更高的網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="89ec4-177">They offer more reliability, faster speeds, lower latencies and higher security than typical connections over the Internet.</span></span>
<span data-ttu-id="89ec4-178">雖然建議的是使用 ExpressRoute，您也可以選擇任何最適合貴組織的連線方法。</span><span class="sxs-lookup"><span data-stu-id="89ec4-178">While it is recommended to use ExpressRoute, you may choose any connection method best suited for your organization.</span></span> <span data-ttu-id="89ec4-179">若要深入了解 ExpressRoute 以及使用 ExpressRoute 的各種連線選項，請閱讀 [ExpressRoute 技術概觀](https://aka.ms/Azure/ExpressRoute)。</span><span class="sxs-lookup"><span data-stu-id="89ec4-179">To learn more about ExpressRoute and the various connectivity options using ExpressRoute, read [ExpressRoute technical overview](https://aka.ms/Azure/ExpressRoute).</span></span>

### <a name="2-create-storage-accounts"></a><span data-ttu-id="89ec4-180">2.建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="89ec4-180">2. Create storage accounts</span></span>
<span data-ttu-id="89ec4-181">為了維持高可用性，並避免依賴單一儲存體帳戶，您可以建立兩個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="89ec4-181">In order to maintain high availability and avoid dependence on a single storage account, you can create two storage accounts.</span></span> <span data-ttu-id="89ec4-182">將每個可用性設定組中的機器分成兩個群組，然後為每個群組指派不同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="89ec4-182">Divide the machines in each availability set into two groups and then assign each group a separate storage account.</span></span>

![建立儲存體帳戶](./media/active-directory-aadconnect-azure-adfs/storageaccount1.png)

### <a name="3-create-availability-sets"></a><span data-ttu-id="89ec4-184">3.建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="89ec4-184">3. Create availability sets</span></span>
<span data-ttu-id="89ec4-185">針對每個角色 (DC/AD FS 和 WAP) 建立可用性設定組，讓每個可用性設定組至少包含 2 部機器。</span><span class="sxs-lookup"><span data-stu-id="89ec4-185">For each role (DC/AD FS and WAP), create availability sets that will contain 2 machines each at the minimum.</span></span> <span data-ttu-id="89ec4-186">這有助於讓每個角色達到更高的可用性。</span><span class="sxs-lookup"><span data-stu-id="89ec4-186">This will help achieve higher availability for each role.</span></span> <span data-ttu-id="89ec4-187">在建立可用性設定組時，必須要決定下列項目︰</span><span class="sxs-lookup"><span data-stu-id="89ec4-187">While creating the availability sets, it is essential to decide on the following:</span></span>

* <span data-ttu-id="89ec4-188">**容錯網域**︰相同容錯網域中的虛擬機器會共用相同的電源和實體網路交換器。</span><span class="sxs-lookup"><span data-stu-id="89ec4-188">**Fault Domains**: Virtual machines in the same fault domain share the same power source and physical network switch.</span></span> <span data-ttu-id="89ec4-189">建議最少準備 2 個容錯網域。</span><span class="sxs-lookup"><span data-stu-id="89ec4-189">A minimum of 2 fault domains are recommended.</span></span> <span data-ttu-id="89ec4-190">預設值為 3 個，在進行此部署時，您可以讓此設定保持原本的預設值。</span><span class="sxs-lookup"><span data-stu-id="89ec4-190">The default value is 3 and you can leave it as is for the purpose of this deployment</span></span>
* <span data-ttu-id="89ec4-191">**更新網域**︰在更新期間，屬於相同更新網域的機器會一起重新啟動。</span><span class="sxs-lookup"><span data-stu-id="89ec4-191">**Update domains**: Machines belonging to the same update domain are restarted together during an update.</span></span> <span data-ttu-id="89ec4-192">您至少需要 2 個更新網域。</span><span class="sxs-lookup"><span data-stu-id="89ec4-192">You want to have minimum of 2 update domains.</span></span> <span data-ttu-id="89ec4-193">預設值為 5 個，在進行此部署時，您可以讓此設定保持原本的預設值。</span><span class="sxs-lookup"><span data-stu-id="89ec4-193">The default value is 5 and you can leave it as is for the purpose of this deployment</span></span>

![可用性設定組](./media/active-directory-aadconnect-azure-adfs/availabilityset1.png)

<span data-ttu-id="89ec4-195">建立下列可用性設定組</span><span class="sxs-lookup"><span data-stu-id="89ec4-195">Create the following availability sets</span></span>

| <span data-ttu-id="89ec4-196">可用性設定組</span><span class="sxs-lookup"><span data-stu-id="89ec4-196">Availability Set</span></span> | <span data-ttu-id="89ec4-197">角色</span><span class="sxs-lookup"><span data-stu-id="89ec4-197">Role</span></span> | <span data-ttu-id="89ec4-198">容錯網域</span><span class="sxs-lookup"><span data-stu-id="89ec4-198">Fault domains</span></span> | <span data-ttu-id="89ec4-199">更新網域</span><span class="sxs-lookup"><span data-stu-id="89ec4-199">Update domains</span></span> |
|:---:|:---:|:---:|:--- |
| <span data-ttu-id="89ec4-200">contosodcset</span><span class="sxs-lookup"><span data-stu-id="89ec4-200">contosodcset</span></span> |<span data-ttu-id="89ec4-201">DC/ADFS</span><span class="sxs-lookup"><span data-stu-id="89ec4-201">DC/ADFS</span></span> |<span data-ttu-id="89ec4-202">3</span><span class="sxs-lookup"><span data-stu-id="89ec4-202">3</span></span> |<span data-ttu-id="89ec4-203">5</span><span class="sxs-lookup"><span data-stu-id="89ec4-203">5</span></span> |
| <span data-ttu-id="89ec4-204">contosowapset</span><span class="sxs-lookup"><span data-stu-id="89ec4-204">contosowapset</span></span> |<span data-ttu-id="89ec4-205">WAP</span><span class="sxs-lookup"><span data-stu-id="89ec4-205">WAP</span></span> |<span data-ttu-id="89ec4-206">3</span><span class="sxs-lookup"><span data-stu-id="89ec4-206">3</span></span> |<span data-ttu-id="89ec4-207">5</span><span class="sxs-lookup"><span data-stu-id="89ec4-207">5</span></span> |

### <a name="4-deploy-virtual-machines"></a><span data-ttu-id="89ec4-208">4.部署虛擬機器</span><span class="sxs-lookup"><span data-stu-id="89ec4-208">4. Deploy virtual machines</span></span>
<span data-ttu-id="89ec4-209">下一個步驟是部署虛擬機器，在基礎結構中裝載不同角色。</span><span class="sxs-lookup"><span data-stu-id="89ec4-209">The next step is to deploy virtual machines that will host the different roles in your infrastructure.</span></span> <span data-ttu-id="89ec4-210">每個可用性設定組中建議至少要有兩部機器。</span><span class="sxs-lookup"><span data-stu-id="89ec4-210">A minimum of two machines are recommended in each availability set.</span></span> <span data-ttu-id="89ec4-211">基本部署需要建立四部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="89ec4-211">Create four virtual machines for the basic deployment.</span></span>

| <span data-ttu-id="89ec4-212">機器</span><span class="sxs-lookup"><span data-stu-id="89ec4-212">Machine</span></span> | <span data-ttu-id="89ec4-213">角色</span><span class="sxs-lookup"><span data-stu-id="89ec4-213">Role</span></span> | <span data-ttu-id="89ec4-214">子網路</span><span class="sxs-lookup"><span data-stu-id="89ec4-214">Subnet</span></span> | <span data-ttu-id="89ec4-215">可用性設定組</span><span class="sxs-lookup"><span data-stu-id="89ec4-215">Availability set</span></span> | <span data-ttu-id="89ec4-216">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="89ec4-216">Storage account</span></span> | <span data-ttu-id="89ec4-217">IP 位址</span><span class="sxs-lookup"><span data-stu-id="89ec4-217">IP Address</span></span> |
|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="89ec4-218">contosodc1</span><span class="sxs-lookup"><span data-stu-id="89ec4-218">contosodc1</span></span> |<span data-ttu-id="89ec4-219">DC/ADFS</span><span class="sxs-lookup"><span data-stu-id="89ec4-219">DC/ADFS</span></span> |<span data-ttu-id="89ec4-220">INT</span><span class="sxs-lookup"><span data-stu-id="89ec4-220">INT</span></span> |<span data-ttu-id="89ec4-221">contosodcset</span><span class="sxs-lookup"><span data-stu-id="89ec4-221">contosodcset</span></span> |<span data-ttu-id="89ec4-222">contososac1</span><span class="sxs-lookup"><span data-stu-id="89ec4-222">contososac1</span></span> |<span data-ttu-id="89ec4-223">靜態</span><span class="sxs-lookup"><span data-stu-id="89ec4-223">Static</span></span> |
| <span data-ttu-id="89ec4-224">contosodc2</span><span class="sxs-lookup"><span data-stu-id="89ec4-224">contosodc2</span></span> |<span data-ttu-id="89ec4-225">DC/ADFS</span><span class="sxs-lookup"><span data-stu-id="89ec4-225">DC/ADFS</span></span> |<span data-ttu-id="89ec4-226">INT</span><span class="sxs-lookup"><span data-stu-id="89ec4-226">INT</span></span> |<span data-ttu-id="89ec4-227">contosodcset</span><span class="sxs-lookup"><span data-stu-id="89ec4-227">contosodcset</span></span> |<span data-ttu-id="89ec4-228">contososac2</span><span class="sxs-lookup"><span data-stu-id="89ec4-228">contososac2</span></span> |<span data-ttu-id="89ec4-229">靜態</span><span class="sxs-lookup"><span data-stu-id="89ec4-229">Static</span></span> |
| <span data-ttu-id="89ec4-230">contosowap1</span><span class="sxs-lookup"><span data-stu-id="89ec4-230">contosowap1</span></span> |<span data-ttu-id="89ec4-231">WAP</span><span class="sxs-lookup"><span data-stu-id="89ec4-231">WAP</span></span> |<span data-ttu-id="89ec4-232">DMZ</span><span class="sxs-lookup"><span data-stu-id="89ec4-232">DMZ</span></span> |<span data-ttu-id="89ec4-233">contosowapset</span><span class="sxs-lookup"><span data-stu-id="89ec4-233">contosowapset</span></span> |<span data-ttu-id="89ec4-234">contososac1</span><span class="sxs-lookup"><span data-stu-id="89ec4-234">contososac1</span></span> |<span data-ttu-id="89ec4-235">靜態</span><span class="sxs-lookup"><span data-stu-id="89ec4-235">Static</span></span> |
| <span data-ttu-id="89ec4-236">contosowap2</span><span class="sxs-lookup"><span data-stu-id="89ec4-236">contosowap2</span></span> |<span data-ttu-id="89ec4-237">WAP</span><span class="sxs-lookup"><span data-stu-id="89ec4-237">WAP</span></span> |<span data-ttu-id="89ec4-238">DMZ</span><span class="sxs-lookup"><span data-stu-id="89ec4-238">DMZ</span></span> |<span data-ttu-id="89ec4-239">contosowapset</span><span class="sxs-lookup"><span data-stu-id="89ec4-239">contosowapset</span></span> |<span data-ttu-id="89ec4-240">contososac2</span><span class="sxs-lookup"><span data-stu-id="89ec4-240">contososac2</span></span> |<span data-ttu-id="89ec4-241">靜態</span><span class="sxs-lookup"><span data-stu-id="89ec4-241">Static</span></span> |

<span data-ttu-id="89ec4-242">您可能已注意到我們還未指定 NSG。</span><span class="sxs-lookup"><span data-stu-id="89ec4-242">As you might have noticed, no NSG has been specified.</span></span> <span data-ttu-id="89ec4-243">這是因為 Azure 可讓您在子網路層級使用 NSG。</span><span class="sxs-lookup"><span data-stu-id="89ec4-243">This is because azure lets you use NSG at the subnet level.</span></span> <span data-ttu-id="89ec4-244">然後，您可以使用與子網路或 NIC 物件相關聯的個別 NSG 來控制機器的網路流量。</span><span class="sxs-lookup"><span data-stu-id="89ec4-244">Then, you can control machine network traffic by using the individual NSG associated with either the subnet or else the NIC object.</span></span> <span data-ttu-id="89ec4-245">如需詳細資訊，請閱讀 [什麼是網路安全性群組 (NSG)](https://aka.ms/Azure/NSG)。</span><span class="sxs-lookup"><span data-stu-id="89ec4-245">Read more on [What is a Network Security Group (NSG)](https://aka.ms/Azure/NSG).</span></span>
<span data-ttu-id="89ec4-246">如果您要管理 DNS，建議使用靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="89ec4-246">Static IP address is recommended if you are managing the DNS.</span></span> <span data-ttu-id="89ec4-247">您可以使用 Azure DNS，並改為在網域的 DNS 記錄中依機器的 Azure FQDN 查閱新的機器。</span><span class="sxs-lookup"><span data-stu-id="89ec4-247">You can use Azure DNS and instead in the DNS records for your domain, refer to the new machines by their Azure FQDNs.</span></span>
<span data-ttu-id="89ec4-248">部署完成之後，虛擬機器的窗格看起來應該會像下圖︰</span><span class="sxs-lookup"><span data-stu-id="89ec4-248">Your virtual machine pane should look like below after the deployment is completed:</span></span>

![虛擬機器已部署](./media/active-directory-aadconnect-azure-adfs/virtualmachinesdeployed_noadfs.png)

### <a name="5-configuring-the-domain-controller--ad-fs-servers"></a><span data-ttu-id="89ec4-250">5.設定網域控制站/AD FS 伺服器</span><span class="sxs-lookup"><span data-stu-id="89ec4-250">5. Configuring the domain controller / AD FS servers</span></span>
 <span data-ttu-id="89ec4-251">為了驗證連入要求，AD FS 必須連絡網域控制站。</span><span class="sxs-lookup"><span data-stu-id="89ec4-251">In order to authenticate any incoming request, AD FS will need to contact the domain controller.</span></span> <span data-ttu-id="89ec4-252">為了節省進行驗證時從 Azure 連線到內部部署 DC 的昂貴成本，建議您在 Azure 中部署網域控制站的複本。</span><span class="sxs-lookup"><span data-stu-id="89ec4-252">To save the costly trip from Azure to on-premises DC for authentication, it is recommended to deploy a replica of the domain controller in Azure.</span></span> <span data-ttu-id="89ec4-253">為了達到高可用性，建議您建立至少包含 2 個網域控制站的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="89ec4-253">In order to attain high availability, it is recommended to create an availability set of at-least 2 domain controllers.</span></span>

| <span data-ttu-id="89ec4-254">網域控制站</span><span class="sxs-lookup"><span data-stu-id="89ec4-254">Domain controller</span></span> | <span data-ttu-id="89ec4-255">角色</span><span class="sxs-lookup"><span data-stu-id="89ec4-255">Role</span></span> | <span data-ttu-id="89ec4-256">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="89ec4-256">Storage account</span></span> |
|:---:|:---:|:---:|
| <span data-ttu-id="89ec4-257">contosodc1</span><span class="sxs-lookup"><span data-stu-id="89ec4-257">contosodc1</span></span> |<span data-ttu-id="89ec4-258">複本</span><span class="sxs-lookup"><span data-stu-id="89ec4-258">Replica</span></span> |<span data-ttu-id="89ec4-259">contososac1</span><span class="sxs-lookup"><span data-stu-id="89ec4-259">contososac1</span></span> |
| <span data-ttu-id="89ec4-260">contosodc2</span><span class="sxs-lookup"><span data-stu-id="89ec4-260">contosodc2</span></span> |<span data-ttu-id="89ec4-261">複本</span><span class="sxs-lookup"><span data-stu-id="89ec4-261">Replica</span></span> |<span data-ttu-id="89ec4-262">contososac2</span><span class="sxs-lookup"><span data-stu-id="89ec4-262">contososac2</span></span> |

* <span data-ttu-id="89ec4-263">使用 DNS 將兩部伺服器升階為複本網域控制站</span><span class="sxs-lookup"><span data-stu-id="89ec4-263">Promote the two servers as replica domain controllers with DNS</span></span>
* <span data-ttu-id="89ec4-264">使用伺服器管理員安裝 AD FS 角色來設定 AD FS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="89ec4-264">Configure the AD FS servers by installing the AD FS role using the server manager.</span></span>

### <a name="6-deploying-internal-load-balancer-ilb"></a><span data-ttu-id="89ec4-265">6.部署內部負載平衡器 (ILB)</span><span class="sxs-lookup"><span data-stu-id="89ec4-265">6. Deploying Internal Load Balancer (ILB)</span></span>
<span data-ttu-id="89ec4-266">**6.1.建立 ILB**</span><span class="sxs-lookup"><span data-stu-id="89ec4-266">**6.1. Create the ILB**</span></span>

<span data-ttu-id="89ec4-267">若要部署 ILB，請在 Azure 入口網站選取負載平衡器，然後按一下新增 (+)。</span><span class="sxs-lookup"><span data-stu-id="89ec4-267">To deploy an ILB, select Load Balancers in the Azure portal and click on add (+).</span></span>

> [!NOTE]
> <span data-ttu-id="89ec4-268">如果在功能表中看不到 [負載平衡器]，請按一下入口網站左下角的 [瀏覽]，並向下捲動到看到 [負載平衡器] 為止。</span><span class="sxs-lookup"><span data-stu-id="89ec4-268">if you do not see **Load Balancers** in your menu, click **Browse** in the lower left of the portal and scroll until you see **Load Balancers**.</span></span>  <span data-ttu-id="89ec4-269">接著，按一下黃色星號即可將它新增至功能表。</span><span class="sxs-lookup"><span data-stu-id="89ec4-269">Then click the yellow star to add it to your menu.</span></span> <span data-ttu-id="89ec4-270">現在，請選取新的負載平衡器圖示以開啟面板，開始設定負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="89ec4-270">Now select the new load balancer icon to open the panel to begin configuration of the load balancer.</span></span>
> 
> 

![瀏覽負載平衡器](./media/active-directory-aadconnect-azure-adfs/browseloadbalancer.png)

* <span data-ttu-id="89ec4-272">**名稱**︰將負載平衡器命名為適合的名稱</span><span class="sxs-lookup"><span data-stu-id="89ec4-272">**Name**: Give any suitable name to the load balancer</span></span>
* <span data-ttu-id="89ec4-273">**配置**︰由於此負載平衡器將放置在 AD FS 伺服器前面，目的是用來進行內部網路連線，因此請選取 [內部]</span><span class="sxs-lookup"><span data-stu-id="89ec4-273">**Scheme**: Since this load balancer will be placed in front of the AD FS servers and is meant for internal network connections ONLY, select “Internal”</span></span>
* <span data-ttu-id="89ec4-274">**虛擬網路**︰選擇要在其中部署 AD FS 的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="89ec4-274">**Virtual Network**: Choose the virtual network where you are deploying your AD FS</span></span>
* <span data-ttu-id="89ec4-275">**子網路**︰在此選擇內部子網路</span><span class="sxs-lookup"><span data-stu-id="89ec4-275">**Subnet**: Choose the internal subnet here</span></span>
* <span data-ttu-id="89ec4-276">**IP 位址指派**：靜態</span><span class="sxs-lookup"><span data-stu-id="89ec4-276">**IP Address assignment**: Static</span></span>

![內部負載平衡器](./media/active-directory-aadconnect-azure-adfs/ilbdeployment1.png)

<span data-ttu-id="89ec4-278">按一下建立並部署 ILB 之後，您應該就會在負載平衡器清單中看到它︰</span><span class="sxs-lookup"><span data-stu-id="89ec4-278">After you click create and the ILB is deployed, you should see it in the list of load balancers:</span></span>

![ILB 之後的負載平衡器](./media/active-directory-aadconnect-azure-adfs/ilbdeployment2.png)

<span data-ttu-id="89ec4-280">下一個步驟是設定後端集區和後端探查。</span><span class="sxs-lookup"><span data-stu-id="89ec4-280">Next step is to configure the backend pool and the backend probe.</span></span>

<span data-ttu-id="89ec4-281">**6.2.設定 ILB 後端集區**</span><span class="sxs-lookup"><span data-stu-id="89ec4-281">**6.2. Configure ILB backend pool**</span></span>

<span data-ttu-id="89ec4-282">在 [負載平衡器] 面板中選取新建立的 ILB。</span><span class="sxs-lookup"><span data-stu-id="89ec4-282">Select the newly created ILB in the Load Balancers panel.</span></span> <span data-ttu-id="89ec4-283">這會開啟 [設定] 面板。</span><span class="sxs-lookup"><span data-stu-id="89ec4-283">It will open the settings panel.</span></span> 

1. <span data-ttu-id="89ec4-284">在 [設定] 面板中選取後端集區</span><span class="sxs-lookup"><span data-stu-id="89ec4-284">Select backend pools from the settings panel</span></span>
2. <span data-ttu-id="89ec4-285">在 [新增後端集區] 面板中，按一下 [新增虛擬機器]</span><span class="sxs-lookup"><span data-stu-id="89ec4-285">In the add backend pool panel, click on add virtual machine</span></span>
3. <span data-ttu-id="89ec4-286">此時您會看到一個面板供您選擇可用性設定組</span><span class="sxs-lookup"><span data-stu-id="89ec4-286">You will be presented with a panel where you can choose availability set</span></span>
4. <span data-ttu-id="89ec4-287">選擇 AD FS 可用性設定組</span><span class="sxs-lookup"><span data-stu-id="89ec4-287">Choose the AD FS availability set</span></span>

![設定 ILB 後端集區](./media/active-directory-aadconnect-azure-adfs/ilbdeployment3.png)

<span data-ttu-id="89ec4-289">**6.3.設定探查**</span><span class="sxs-lookup"><span data-stu-id="89ec4-289">**6.3. Configuring probe**</span></span>

<span data-ttu-id="89ec4-290">在 ILB 的 [設定] 面板中，選取 [探查]。</span><span class="sxs-lookup"><span data-stu-id="89ec4-290">In the ILB settings panel, select Probes.</span></span>

1. <span data-ttu-id="89ec4-291">按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="89ec4-291">Click on add</span></span>
2. <span data-ttu-id="89ec4-292">提供探查的詳細資料 a.</span><span class="sxs-lookup"><span data-stu-id="89ec4-292">Provide details for probe a.</span></span> <span data-ttu-id="89ec4-293">**名稱**︰探查名稱 b.</span><span class="sxs-lookup"><span data-stu-id="89ec4-293">**Name**: Probe name b.</span></span> <span data-ttu-id="89ec4-294">**通訊協定**：TCP c.</span><span class="sxs-lookup"><span data-stu-id="89ec4-294">**Protocol**: TCP c.</span></span> <span data-ttu-id="89ec4-295">**連接埠**：443 (HTTPS) d.</span><span class="sxs-lookup"><span data-stu-id="89ec4-295">**Port**: 443 (HTTPS) d.</span></span> <span data-ttu-id="89ec4-296">**間隔**：5 (預設值) – 這是 ILB 在後端集區中探查機器的間隔 e.</span><span class="sxs-lookup"><span data-stu-id="89ec4-296">**Interval**: 5 (default value) – this is the interval at which ILB will probe the machines in the backend pool e.</span></span> <span data-ttu-id="89ec4-297">**狀況不良臨界值限制**：2 (預設值) – 這是連續探查失敗臨界值，達到此臨界值之後，ILB 就會將後端集區中的機器宣告為沒有回應，並停止對它傳送流量。</span><span class="sxs-lookup"><span data-stu-id="89ec4-297">**Unhealthy threshold limit**: 2 (default val ue) – this is the threshold of consecutive probe failures after which ILB will declare a machine in the backend pool non-responsive and stop sending traffic to it.</span></span>

![設定 ILB 探查](./media/active-directory-aadconnect-azure-adfs/ilbdeployment4.png)

<span data-ttu-id="89ec4-299">**6.4.建立負載平衡規則**</span><span class="sxs-lookup"><span data-stu-id="89ec4-299">**6.4. Create load balancing rules**</span></span>

<span data-ttu-id="89ec4-300">為了有效平衡流量，應該為 ILB 設定負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="89ec4-300">In order to effectively balance the traffic, the ILB should be configured with load balancing rules.</span></span> <span data-ttu-id="89ec4-301">若要建立負載平衡規則，</span><span class="sxs-lookup"><span data-stu-id="89ec4-301">In order to create a load balancing rule,</span></span> 

1. <span data-ttu-id="89ec4-302">在 ILB 的 [設定] 面板中選取 [負載平衡規則]</span><span class="sxs-lookup"><span data-stu-id="89ec4-302">Select Load balancing rule from the settings panel of the ILB</span></span>
2. <span data-ttu-id="89ec4-303">按一下 [負載平衡規則] 面板中的 [新增]</span><span class="sxs-lookup"><span data-stu-id="89ec4-303">Click on Add in the Load balancing rule panel</span></span>
3. <span data-ttu-id="89ec4-304">在 [新增負載平衡規則] 面板中 a.</span><span class="sxs-lookup"><span data-stu-id="89ec4-304">In the Add load balancing rule panel a.</span></span> <span data-ttu-id="89ec4-305">**名稱**︰提供規則名稱 b.</span><span class="sxs-lookup"><span data-stu-id="89ec4-305">**Name**: Provide a name for the rule b.</span></span> <span data-ttu-id="89ec4-306">**通訊協定**︰選取 [TCP] c.</span><span class="sxs-lookup"><span data-stu-id="89ec4-306">**Protocol**: Select TCP c.</span></span> <span data-ttu-id="89ec4-307">**連接埠**：443 d.</span><span class="sxs-lookup"><span data-stu-id="89ec4-307">**Port**: 443 d.</span></span> <span data-ttu-id="89ec4-308">**後端連接埠**：443 e.</span><span class="sxs-lookup"><span data-stu-id="89ec4-308">**Backend port**: 443 e.</span></span> <span data-ttu-id="89ec4-309">**後端集區**︰選取稍早為 AD FS 叢集建立的集區 f.</span><span class="sxs-lookup"><span data-stu-id="89ec4-309">**Backend pool**: Select the pool you created for the AD FS cluster earlier f.</span></span> <span data-ttu-id="89ec4-310">**探查**︰選取稍早為 AD FS 伺服器建立的探查</span><span class="sxs-lookup"><span data-stu-id="89ec4-310">**Probe**: Select the probe created for AD FS servers earlier</span></span>

![設定 ILB 平衡規則](./media/active-directory-aadconnect-azure-adfs/ilbdeployment5.png)

<span data-ttu-id="89ec4-312">**6.5.更新 ILB 的 DNS**</span><span class="sxs-lookup"><span data-stu-id="89ec4-312">**6.5. Update DNS with ILB**</span></span>

<span data-ttu-id="89ec4-313">移至 DNS 伺服器，為 ILB 建立 CNAME。</span><span class="sxs-lookup"><span data-stu-id="89ec4-313">Go to your DNS server and create a CNAME for the ILB.</span></span> <span data-ttu-id="89ec4-314">CNAME 應適用於 IP 位址指向 ILB 的 IP 位址的同盟服務。</span><span class="sxs-lookup"><span data-stu-id="89ec4-314">The CNAME should be for the federation service with the IP address pointing to the IP address of the ILB.</span></span> <span data-ttu-id="89ec4-315">例如，如果 ILB DIP 位址是 10.3.0.8，而所安裝的同盟服務是 fs.contoso.com，則請為指向 10.3.0.8 的 fs.contoso.com 建立 CNAME。</span><span class="sxs-lookup"><span data-stu-id="89ec4-315">For example if the ILB DIP address is 10.3.0.8, and the federation service installed is fs.contoso.com, then create a CNAME for fs.contoso.com pointing to 10.3.0.8.</span></span>
<span data-ttu-id="89ec4-316">這可確保所有與 fs.contoso.com 有關的通訊都在 ILB 結束，並且會受到適當路由處理。</span><span class="sxs-lookup"><span data-stu-id="89ec4-316">This will ensure that all communication regarding fs.contoso.com end up at the ILB and are appropriately routed.</span></span>

### <a name="7-configuring-the-web-application-proxy-server"></a><span data-ttu-id="89ec4-317">7.設定 Web 應用程式 Proxy 伺服器</span><span class="sxs-lookup"><span data-stu-id="89ec4-317">7. Configuring the Web Application Proxy server</span></span>
<span data-ttu-id="89ec4-318">**7.1.設定 Web 應用程式 Proxy 伺服器以連線到 AD FS 伺服器**</span><span class="sxs-lookup"><span data-stu-id="89ec4-318">**7.1. Configuring the Web Application Proxy servers to reach AD FS servers**</span></span>

<span data-ttu-id="89ec4-319">為了確保 Web 應用程式 Proxy 伺服器能夠連線到 ILB 背後的 AD FS 伺服器，請在 %systemroot%\system32\drivers\etc\hosts 建立 ILB 的記錄。</span><span class="sxs-lookup"><span data-stu-id="89ec4-319">In order to ensure that Web Application Proxy servers are able to reach the AD FS servers behind the ILB, create a record in the %systemroot%\system32\drivers\etc\hosts for the ILB.</span></span> <span data-ttu-id="89ec4-320">請注意，辨別名稱 (DN) 應該是同盟服務名稱，例如 fs.contoso.com。</span><span class="sxs-lookup"><span data-stu-id="89ec4-320">Note that the distinguished name (DN) should be the federation service name, for example fs.contoso.com.</span></span> <span data-ttu-id="89ec4-321">而且 IP 項目應該是 ILB 的 IP 位址 (如範例中的 10.3.0.8) 的項目。</span><span class="sxs-lookup"><span data-stu-id="89ec4-321">And the IP entry should be that of the ILB’s IP address (10.3.0.8 as in the example).</span></span>

<span data-ttu-id="89ec4-322">**7.2.安裝 Web 應用程式 Proxy 角色**</span><span class="sxs-lookup"><span data-stu-id="89ec4-322">**7.2. Installing the Web Application Proxy role**</span></span>

<span data-ttu-id="89ec4-323">在確定 Web 應用程式 Proxy 伺服器能夠連線到 ILB 背後的 AD FS 伺服器之後，您可以接著安裝 Web 應用程式 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="89ec4-323">After you ensure that Web Application Proxy servers are able to reach the AD FS servers behind ILB, you can next install the Web Application Proxy servers.</span></span> <span data-ttu-id="89ec4-324">Web 應用程式 Proxy 伺服器不可加入網域。</span><span class="sxs-lookup"><span data-stu-id="89ec4-324">Web Application Proxy servers do not be joined to the domain.</span></span> <span data-ttu-id="89ec4-325">請選取「遠端存取」角色，將 Web 應用程式 Proxy 角色安裝在兩個 Web 應用程式 Proxy 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="89ec4-325">Install the Web Application Proxy roles on the two Web Application Proxy servers by selecting the Remote Access role.</span></span> <span data-ttu-id="89ec4-326">伺服器管理員會引導您完成 WAP 安裝。</span><span class="sxs-lookup"><span data-stu-id="89ec4-326">The server manager will guide you to complete the WAP installation.</span></span>
<span data-ttu-id="89ec4-327">如需如何部署 WAP 的詳細資訊，請閱讀 [安裝和設定 Web 應用程式 Proxy 伺服器](https://technet.microsoft.com/library/dn383662.aspx)。</span><span class="sxs-lookup"><span data-stu-id="89ec4-327">For more information on how to deploy WAP, read [Install and Configure the Web Application Proxy Server](https://technet.microsoft.com/library/dn383662.aspx).</span></span>

### <a name="8--deploying-the-internet-facing-public-load-balancer"></a><span data-ttu-id="89ec4-328">8.部署網際網路對向 (公用) 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="89ec4-328">8.  Deploying the Internet Facing (Public) Load Balancer</span></span>
<span data-ttu-id="89ec4-329">**8.1.建立網際網路對向 (公用) 負載平衡器**</span><span class="sxs-lookup"><span data-stu-id="89ec4-329">**8.1.  Create Internet Facing (Public) Load Balancer**</span></span>

<span data-ttu-id="89ec4-330">在 Azure 入口網站中選取 [負載平衡器]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="89ec4-330">In the Azure portal, select Load balancers and then click on Add.</span></span> <span data-ttu-id="89ec4-331">在 [建立負載平衡器] 面板中，輸入下列資訊</span><span class="sxs-lookup"><span data-stu-id="89ec4-331">In the Create load balancer panel, enter the following information</span></span>

1. <span data-ttu-id="89ec4-332">**名稱**︰負載平衡器的名稱</span><span class="sxs-lookup"><span data-stu-id="89ec4-332">**Name**: Name for the load balancer</span></span>
2. <span data-ttu-id="89ec4-333">**配置**︰公用 – 此選項會告知 Azure，此負載平衡器需要公用位址。</span><span class="sxs-lookup"><span data-stu-id="89ec4-333">**Scheme**: Public – this option tells Azure that this load balancer will need a public address.</span></span>
3. <span data-ttu-id="89ec4-334">**IP 位址**︰建立新的 IP 位址 (動態)</span><span class="sxs-lookup"><span data-stu-id="89ec4-334">**IP Address**: Create a new IP address (dynamic)</span></span>

![網際網路對向負載平衡器](./media/active-directory-aadconnect-azure-adfs/elbdeployment1.png)

<span data-ttu-id="89ec4-336">部署之後，負載平衡器就會出現在 [負載平衡器] 清單中。</span><span class="sxs-lookup"><span data-stu-id="89ec4-336">After deployment, the load balancer will appear in the Load balancers list.</span></span>

![負載平衡器清單](./media/active-directory-aadconnect-azure-adfs/elbdeployment2.png)

<span data-ttu-id="89ec4-338">**8.2.對公用 IP 指派 DNS 標籤**</span><span class="sxs-lookup"><span data-stu-id="89ec4-338">**8.2. Assign a DNS label to the public IP**</span></span>

<span data-ttu-id="89ec4-339">在 [負載平衡器] 面板中按一下新建立的負載平衡器項目，以顯示組態的面板。</span><span class="sxs-lookup"><span data-stu-id="89ec4-339">Click on the newly created load balancer entry in the Load balancers panel to bring up the panel for configuration.</span></span> <span data-ttu-id="89ec4-340">遵循下列步驟來設定公用 IP 的 DNS 標籤︰</span><span class="sxs-lookup"><span data-stu-id="89ec4-340">Follow below steps to configure the DNS label for the public IP:</span></span>

1. <span data-ttu-id="89ec4-341">按一下 [公用 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="89ec4-341">Click on the public IP address.</span></span> <span data-ttu-id="89ec4-342">這會開啟公用 IP 與其設定的面板</span><span class="sxs-lookup"><span data-stu-id="89ec4-342">This will open the panel for the public IP and its settings</span></span>
2. <span data-ttu-id="89ec4-343">按一下 [組態]</span><span class="sxs-lookup"><span data-stu-id="89ec4-343">Click on Configuration</span></span>
3. <span data-ttu-id="89ec4-344">提供 DNS 標籤。</span><span class="sxs-lookup"><span data-stu-id="89ec4-344">Provide a DNS label.</span></span> <span data-ttu-id="89ec4-345">這會成為您可以從任何地方存取的公用 DNS 標籤，例如 contosofs.westus.cloudapp.azure.com。</span><span class="sxs-lookup"><span data-stu-id="89ec4-345">This will become the public DNS label that you can access from anywhere, for example contosofs.westus.cloudapp.azure.com.</span></span> <span data-ttu-id="89ec4-346">您可以在外部 DNS 中新增用於同盟服務的項目 (例如 fs.contoso.com)，以解析為外部負載平衡器的 DNS 標籤 (contosofs.westus.cloudapp.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="89ec4-346">You can add an entry in the external DNS for the federation service (like fs.contoso.com) that resolves to the DNS label of the external load balancer (contosofs.westus.cloudapp.azure.com).</span></span>

![設定網際網路對向負載平衡器](./media/active-directory-aadconnect-azure-adfs/elbdeployment3.png) 

![設定網際網路對向負載平衡器 (DNS)](./media/active-directory-aadconnect-azure-adfs/elbdeployment4.png)

<span data-ttu-id="89ec4-349">**8.3.設定網際網路對向 (公用) 負載平衡器的後端集區**</span><span class="sxs-lookup"><span data-stu-id="89ec4-349">**8.3. Configure backend pool for Internet Facing (Public) Load Balancer**</span></span> 

<span data-ttu-id="89ec4-350">遵循和建立內部負載平衡器相同的步驟，將網際網路對向 (公用) 負載平衡器的後端集區設定為 WAP 伺服器的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="89ec4-350">Follow the same steps as in creating the internal load balancer, to configure the backend pool for Internet Facing (Public) Load Balancer as the availability set for the WAP servers.</span></span> <span data-ttu-id="89ec4-351">例如，contosowapset。</span><span class="sxs-lookup"><span data-stu-id="89ec4-351">For example, contosowapset.</span></span>

![設定網際網路對向負載平衡器的後端集區](./media/active-directory-aadconnect-azure-adfs/elbdeployment5.png)

<span data-ttu-id="89ec4-353">**8.4.設定探查**</span><span class="sxs-lookup"><span data-stu-id="89ec4-353">**8.4. Configure probe**</span></span>

<span data-ttu-id="89ec4-354">遵循和設定內部負載平衡器相同的步驟來設定 WAP 伺服器後端集區的探查。</span><span class="sxs-lookup"><span data-stu-id="89ec4-354">Follow the same steps as in configuring the internal load balancer  to configure the probe for the backend pool of WAP servers.</span></span>

![設定網際網路對向負載平衡器的探查](./media/active-directory-aadconnect-azure-adfs/elbdeployment6.png)

<span data-ttu-id="89ec4-356">**8.5.建立負載平衡規則**</span><span class="sxs-lookup"><span data-stu-id="89ec4-356">**8.5. Create load balancing rule(s)**</span></span>

<span data-ttu-id="89ec4-357">遵循和 ILB 中相同的步驟來設定 TCP 443 的負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="89ec4-357">Follow the same steps as in ILB to configure the load balancing rule for TCP 443.</span></span>

![設定網際網路對向負載平衡器的平衡規則](./media/active-directory-aadconnect-azure-adfs/elbdeployment7.png)

### <a name="9-securing-the-network"></a><span data-ttu-id="89ec4-359">9.保護網路</span><span class="sxs-lookup"><span data-stu-id="89ec4-359">9. Securing the network</span></span>
<span data-ttu-id="89ec4-360">**9.1.保護內部子網路**</span><span class="sxs-lookup"><span data-stu-id="89ec4-360">**9.1. Securing the internal subnet**</span></span>

<span data-ttu-id="89ec4-361">整體來說，您需要下列規則來有效率地保護內部子網路 (依如下所示順序)</span><span class="sxs-lookup"><span data-stu-id="89ec4-361">Overall, you need the following rules to efficiently secure your internal subnet (in the order as listed below)</span></span>

| <span data-ttu-id="89ec4-362">規則</span><span class="sxs-lookup"><span data-stu-id="89ec4-362">Rule</span></span> | <span data-ttu-id="89ec4-363">說明</span><span class="sxs-lookup"><span data-stu-id="89ec4-363">Description</span></span> | <span data-ttu-id="89ec4-364">Flow</span><span class="sxs-lookup"><span data-stu-id="89ec4-364">Flow</span></span> |
|:--- |:--- |:---:|
| <span data-ttu-id="89ec4-365">AllowHTTPSFromDMZ</span><span class="sxs-lookup"><span data-stu-id="89ec4-365">AllowHTTPSFromDMZ</span></span> |<span data-ttu-id="89ec4-366">允許來自 DMZ 的 HTTPS 通訊</span><span class="sxs-lookup"><span data-stu-id="89ec4-366">Allow the HTTPS communication from DMZ</span></span> |<span data-ttu-id="89ec4-367">輸入</span><span class="sxs-lookup"><span data-stu-id="89ec4-367">Inbound</span></span> |
| <span data-ttu-id="89ec4-368">DenyInternetOutbound</span><span class="sxs-lookup"><span data-stu-id="89ec4-368">DenyInternetOutbound</span></span> |<span data-ttu-id="89ec4-369">不得存取網際網路</span><span class="sxs-lookup"><span data-stu-id="89ec4-369">No access to internet</span></span> |<span data-ttu-id="89ec4-370">輸出</span><span class="sxs-lookup"><span data-stu-id="89ec4-370">Outbound</span></span> |

![INT 存取規則 (輸入)](./media/active-directory-aadconnect-azure-adfs/nsg_int.png)

<span data-ttu-id="89ec4-372">[註解]: <> (![INT 存取規則 (輸入)](./media/active-directory-aadconnect-azure-adfs/nsgintinbound.png)) [註解]: <> (![INT 存取規則 (輸出)](./media/active-directory-aadconnect-azure-adfs/nsgintoutbound.png))</span><span class="sxs-lookup"><span data-stu-id="89ec4-372">[comment]: <> (![INT access rules (inbound)](./media/active-directory-aadconnect-azure-adfs/nsgintinbound.png)) [comment]: <> (![INT access rules (outbound)](./media/active-directory-aadconnect-azure-adfs/nsgintoutbound.png))</span></span>

<span data-ttu-id="89ec4-373">**9.2.保護 DMZ 子網路**</span><span class="sxs-lookup"><span data-stu-id="89ec4-373">**9.2. Securing the DMZ subnet**</span></span>

| <span data-ttu-id="89ec4-374">規則</span><span class="sxs-lookup"><span data-stu-id="89ec4-374">Rule</span></span> | <span data-ttu-id="89ec4-375">說明</span><span class="sxs-lookup"><span data-stu-id="89ec4-375">Description</span></span> | <span data-ttu-id="89ec4-376">Flow</span><span class="sxs-lookup"><span data-stu-id="89ec4-376">Flow</span></span> |
|:--- |:--- |:---:|
| <span data-ttu-id="89ec4-377">AllowHTTPSFromInternet</span><span class="sxs-lookup"><span data-stu-id="89ec4-377">AllowHTTPSFromInternet</span></span> |<span data-ttu-id="89ec4-378">允許從網際網路到 DMZ 的 HTTPS</span><span class="sxs-lookup"><span data-stu-id="89ec4-378">Allow HTTPS from internet to the DMZ</span></span> |<span data-ttu-id="89ec4-379">輸入</span><span class="sxs-lookup"><span data-stu-id="89ec4-379">Inbound</span></span> |
| <span data-ttu-id="89ec4-380">DenyInternetOutbound</span><span class="sxs-lookup"><span data-stu-id="89ec4-380">DenyInternetOutbound</span></span> |<span data-ttu-id="89ec4-381">HTTPS 以外流向網際網路的任何流量都會遭到封鎖</span><span class="sxs-lookup"><span data-stu-id="89ec4-381">Anything except HTTPS to internet is blocked</span></span> |<span data-ttu-id="89ec4-382">輸出</span><span class="sxs-lookup"><span data-stu-id="89ec4-382">Outbound</span></span> |

![EXT 存取規則 (輸入)](./media/active-directory-aadconnect-azure-adfs/nsg_dmz.png)

<span data-ttu-id="89ec4-384">[註解]: <> (![EXT 存取規則 (輸入)](./media/active-directory-aadconnect-azure-adfs/nsgdmzinbound.png)) [註解]: <> (![EXT 存取規則 (輸出)](./media/active-directory-aadconnect-azure-adfs/nsgdmzoutbound.png))</span><span class="sxs-lookup"><span data-stu-id="89ec4-384">[comment]: <> (![EXT access rules (inbound)](./media/active-directory-aadconnect-azure-adfs/nsgdmzinbound.png)) [comment]: <> (![EXT access rules (outbound)](./media/active-directory-aadconnect-azure-adfs/nsgdmzoutbound.png))</span></span>

> [!NOTE]
> <span data-ttu-id="89ec4-385">如果需要用戶端使用者憑證驗證 (使用 X509 使用者憑證的 clientTLS 驗證)，則 AD FS 需要啟用 TCP 連接埠 49443 以供輸入存取。</span><span class="sxs-lookup"><span data-stu-id="89ec4-385">If client user certificate authentication (clientTLS authentication using X509 user certificates) is required, then AD FS requires TCP port 49443 be enabled for inbound access.</span></span>
> 
> 

### <a name="10-test-the-ad-fs-sign-in"></a><span data-ttu-id="89ec4-386">10.測試 AD FS 登入</span><span class="sxs-lookup"><span data-stu-id="89ec4-386">10. Test the AD FS sign-in</span></span>
<span data-ttu-id="89ec4-387">要測試 AD FS，最簡單的方法是使用 IdpInitiatedSignon.aspx 網頁。</span><span class="sxs-lookup"><span data-stu-id="89ec4-387">The easiest way is to test AD FS is by using the IdpInitiatedSignon.aspx page.</span></span> <span data-ttu-id="89ec4-388">為了能夠執行此作業，必須在 AD FS 屬性上啟用 IdpInitiatedSignOn。</span><span class="sxs-lookup"><span data-stu-id="89ec4-388">In order to be able to do that, it is required to enable the IdpInitiatedSignOn on the AD FS properties.</span></span> <span data-ttu-id="89ec4-389">請遵循下列步驟來確認 AD FS 設定</span><span class="sxs-lookup"><span data-stu-id="89ec4-389">Follow the steps below to verify your AD FS setup</span></span>

1. <span data-ttu-id="89ec4-390">使用 PowerShell 在 AD FS 伺服器上執行以下 Cmdlet，將它設定為啟用。</span><span class="sxs-lookup"><span data-stu-id="89ec4-390">Run the below cmdlet on the AD FS server, using PowerShell, to set it to enabled.</span></span>
   <span data-ttu-id="89ec4-391">Set-AdfsProperties -EnableIdPInitiatedSignonPage $true</span><span class="sxs-lookup"><span data-stu-id="89ec4-391">Set-AdfsProperties -EnableIdPInitiatedSignonPage $true</span></span> 
2. <span data-ttu-id="89ec4-392">從任何外部電腦存取 https://adfs.thecloudadvocate.com/adfs/ls/IdpInitiatedSignon.aspx</span><span class="sxs-lookup"><span data-stu-id="89ec4-392">From any external machine access https://adfs.thecloudadvocate.com/adfs/ls/IdpInitiatedSignon.aspx</span></span>  
3. <span data-ttu-id="89ec4-393">您應該會看到如下圖的 AD FS 網頁︰</span><span class="sxs-lookup"><span data-stu-id="89ec4-393">You should see the AD FS page like below:</span></span>

![測試登入網頁](./media/active-directory-aadconnect-azure-adfs/test1.png)

<span data-ttu-id="89ec4-395">成功登入時，它會提供您如下所示的成功訊息︰</span><span class="sxs-lookup"><span data-stu-id="89ec4-395">On successful sign-in, it will provide you with a success message as shown below:</span></span>

![測試成功](./media/active-directory-aadconnect-azure-adfs/test2.png)

## <a name="template-for-deploying-ad-fs-in-azure"></a><span data-ttu-id="89ec4-397">在 Azure 中部署 AD FS 的範本</span><span class="sxs-lookup"><span data-stu-id="89ec4-397">Template for deploying AD FS in Azure</span></span>
<span data-ttu-id="89ec4-398">此範本回部署含 6 部電腦的安裝，其中 2 部分別用於網域控制站 (AD FS 和 WAP)。</span><span class="sxs-lookup"><span data-stu-id="89ec4-398">The template deploys a 6 machine setup, 2 each for Domain Controllers, AD FS and WAP.</span></span>

[<span data-ttu-id="89ec4-399">Azure 部署範本中的 AD FS</span><span class="sxs-lookup"><span data-stu-id="89ec4-399">AD FS in Azure Deployment Template</span></span>](https://github.com/paulomarquesc/adfs-6vms-regular-template-based)

<span data-ttu-id="89ec4-400">您可以使用現有的虛擬網路，或在部署此範本時建立新的 VNET。</span><span class="sxs-lookup"><span data-stu-id="89ec4-400">You can use an existing virtual network or create a new VNET while deploying this template.</span></span> <span data-ttu-id="89ec4-401">可用於自訂部署的各種參數如下所列 (包含在部署過程中使用的參數說明)。</span><span class="sxs-lookup"><span data-stu-id="89ec4-401">The various parameters available for customizing the deployment are listed below with the description of usage of the parameter in the deployment process.</span></span> 

| <span data-ttu-id="89ec4-402">參數</span><span class="sxs-lookup"><span data-stu-id="89ec4-402">Parameter</span></span> | <span data-ttu-id="89ec4-403">說明</span><span class="sxs-lookup"><span data-stu-id="89ec4-403">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="89ec4-404">位置</span><span class="sxs-lookup"><span data-stu-id="89ec4-404">Location</span></span> |<span data-ttu-id="89ec4-405">要部署資源的區域，例如美國東部。</span><span class="sxs-lookup"><span data-stu-id="89ec4-405">The region to deploy the resources into, e.g. East US.</span></span> |
| <span data-ttu-id="89ec4-406">StorageAccountType</span><span class="sxs-lookup"><span data-stu-id="89ec4-406">StorageAccountType</span></span> |<span data-ttu-id="89ec4-407">建立的儲存體帳戶類型</span><span class="sxs-lookup"><span data-stu-id="89ec4-407">The type of the Storage Account created</span></span> |
| <span data-ttu-id="89ec4-408">VirtualNetworkUsage</span><span class="sxs-lookup"><span data-stu-id="89ec4-408">VirtualNetworkUsage</span></span> |<span data-ttu-id="89ec4-409">指出將建立新的虛擬網路，或使用現有的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="89ec4-409">Indicates if a new virtual network will be created or use an existing one</span></span> |
| <span data-ttu-id="89ec4-410">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="89ec4-410">VirtualNetworkName</span></span> |<span data-ttu-id="89ec4-411">要建立的虛擬網路名稱 (使用現有或新的虛擬網路時的必要參數)</span><span class="sxs-lookup"><span data-stu-id="89ec4-411">The name of the Virtual Network to Create, mandatory on both existing or new virtual network usage</span></span> |
| <span data-ttu-id="89ec4-412">VirtualNetworkResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="89ec4-412">VirtualNetworkResourceGroupName</span></span> |<span data-ttu-id="89ec4-413">指定現有虛擬網路所在的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="89ec4-413">Specifies the name of the resource group where the existing virtual network resides.</span></span> <span data-ttu-id="89ec4-414">使用現有虛擬網路時，這會變成必要參數，以便部署找到現有虛擬網路的識別碼</span><span class="sxs-lookup"><span data-stu-id="89ec4-414">When using an existing virtual network, this becomes a mandatory parameter so the deployment can find the ID of the existing virtual network</span></span> |
| <span data-ttu-id="89ec4-415">VirtualNetworkAddressRange</span><span class="sxs-lookup"><span data-stu-id="89ec4-415">VirtualNetworkAddressRange</span></span> |<span data-ttu-id="89ec4-416">新 VNET 的位址範圍 (如果建立新的虛擬網路，則為必要參數)</span><span class="sxs-lookup"><span data-stu-id="89ec4-416">The address range of the new VNET, mandatory if creating a new virtual network</span></span> |
| <span data-ttu-id="89ec4-417">InternalSubnetName</span><span class="sxs-lookup"><span data-stu-id="89ec4-417">InternalSubnetName</span></span> |<span data-ttu-id="89ec4-418">內部子網路的名稱 (使用現有或新的虛擬網路時的必要參數)</span><span class="sxs-lookup"><span data-stu-id="89ec4-418">The name of the internal subnet, mandatory on both virtual network usage options (new or existing)</span></span> |
| <span data-ttu-id="89ec4-419">InternalSubnetAddressRange</span><span class="sxs-lookup"><span data-stu-id="89ec4-419">InternalSubnetAddressRange</span></span> |<span data-ttu-id="89ec4-420">內部子網路的位址範圍，其包含網域控制站和 ADFS 伺服器 (如果建立新的虛擬網路，則為必要參數)</span><span class="sxs-lookup"><span data-stu-id="89ec4-420">The address range of the internal subnet, which contains the Domain Controllers and ADFS servers, mandatory if creating a new virtual network.</span></span> |
| <span data-ttu-id="89ec4-421">DMZSubnetAddressRange</span><span class="sxs-lookup"><span data-stu-id="89ec4-421">DMZSubnetAddressRange</span></span> |<span data-ttu-id="89ec4-422">dmz 子網路的位址範圍，其包含 Windows 應用程式 Proxy 伺服器 (如果建立新的虛擬網路，則為必要參數)</span><span class="sxs-lookup"><span data-stu-id="89ec4-422">The address range of the dmz subnet, which contains the Windows application proxy servers, mandatory if creating a new virtual network.</span></span> |
| <span data-ttu-id="89ec4-423">DMZSubnetName</span><span class="sxs-lookup"><span data-stu-id="89ec4-423">DMZSubnetName</span></span> |<span data-ttu-id="89ec4-424">內部子網路的名稱 (使用現有或新的虛擬網路時的必要參數)。</span><span class="sxs-lookup"><span data-stu-id="89ec4-424">The name of the internal subnet, mandatory on both virtual network usage options (new or existing).</span></span> |
| <span data-ttu-id="89ec4-425">ADDC01NICIPAddress</span><span class="sxs-lookup"><span data-stu-id="89ec4-425">ADDC01NICIPAddress</span></span> |<span data-ttu-id="89ec4-426">第一個網域控制站的內部 IP 位址，此 IP 位址會以靜態方式指派給 DC，而且必須是內部子網路內的有效 ip 位址</span><span class="sxs-lookup"><span data-stu-id="89ec4-426">The internal IP address of the first Domain Controller, this IP address will be statically assigned to the DC and must be a valid ip address within the Internal subnet</span></span> |
| <span data-ttu-id="89ec4-427">ADDC02NICIPAddress</span><span class="sxs-lookup"><span data-stu-id="89ec4-427">ADDC02NICIPAddress</span></span> |<span data-ttu-id="89ec4-428">第二個網域控制站的內部 IP 位址，此 IP 位址會以靜態方式指派給 DC，而且必須是內部子網路內的有效 ip 位址</span><span class="sxs-lookup"><span data-stu-id="89ec4-428">The internal IP address of the second Domain Controller, this IP address will be statically assigned to the DC and must be a valid ip address within the Internal subnet</span></span> |
| <span data-ttu-id="89ec4-429">ADFS01NICIPAddress</span><span class="sxs-lookup"><span data-stu-id="89ec4-429">ADFS01NICIPAddress</span></span> |<span data-ttu-id="89ec4-430">第一個 ADFS 伺服器的內部 IP 位址，此 IP 位址會以靜態方式指派給 ADFS 伺服器，而且必須是內部子網路內的有效 ip 位址</span><span class="sxs-lookup"><span data-stu-id="89ec4-430">The internal IP address of the first ADFS server, this IP address will be statically assigned to the ADFS server and must be a valid ip address within the Internal subnet</span></span> |
| <span data-ttu-id="89ec4-431">ADFS02NICIPAddress</span><span class="sxs-lookup"><span data-stu-id="89ec4-431">ADFS02NICIPAddress</span></span> |<span data-ttu-id="89ec4-432">第二個 ADFS 伺服器的內部 IP 位址，此 IP 位址會以靜態方式指派給 ADFS 伺服器，而且必須是內部子網路內的有效 ip 位址</span><span class="sxs-lookup"><span data-stu-id="89ec4-432">The internal IP address of the second ADFS server, this IP address will be statically assigned to the ADFS server and must be a valid ip address within the Internal subnet</span></span> |
| <span data-ttu-id="89ec4-433">WAP01NICIPAddress</span><span class="sxs-lookup"><span data-stu-id="89ec4-433">WAP01NICIPAddress</span></span> |<span data-ttu-id="89ec4-434">第一個 WAP 伺服器的內部 IP 位址，此 IP 位址會以靜態方式指派給 WAP 伺服器，而且必須是 WAP 子網路內的有效 ip 位址</span><span class="sxs-lookup"><span data-stu-id="89ec4-434">The internal IP address of the first WAP server, this IP address will be statically assigned to the WAP server and must be a valid ip address within the DMZ subnet</span></span> |
| <span data-ttu-id="89ec4-435">WAP02NICIPAddress</span><span class="sxs-lookup"><span data-stu-id="89ec4-435">WAP02NICIPAddress</span></span> |<span data-ttu-id="89ec4-436">第二個 WAP 伺服器的內部 IP 位址，此 IP 位址會以靜態方式指派給 WAP 伺服器，而且必須是 WAP 子網路內的有效 ip 位址</span><span class="sxs-lookup"><span data-stu-id="89ec4-436">The internal IP address of the second WAP server, this IP address will be statically assigned to the WAP server and must be a valid ip address within the DMZ subnet</span></span> |
| <span data-ttu-id="89ec4-437">ADFSLoadBalancerPrivateIPAddress</span><span class="sxs-lookup"><span data-stu-id="89ec4-437">ADFSLoadBalancerPrivateIPAddress</span></span> |<span data-ttu-id="89ec4-438">ADFS 負載平衡器的內部 IP 位址，此 IP 位址會以靜態方式指派給負載平衡器，而且必須是 WAP 子網路內的有效 ip 位址</span><span class="sxs-lookup"><span data-stu-id="89ec4-438">The internal IP address of the ADFS load balancer, this IP address will be statically assigned to the load balancer and must be a valid ip address within the Internal subnet</span></span> |
| <span data-ttu-id="89ec4-439">ADDCVMNamePrefix</span><span class="sxs-lookup"><span data-stu-id="89ec4-439">ADDCVMNamePrefix</span></span> |<span data-ttu-id="89ec4-440">網域控制站的虛擬機器名稱前置詞</span><span class="sxs-lookup"><span data-stu-id="89ec4-440">Virtual Machine name prefix for Domain Controllers</span></span> |
| <span data-ttu-id="89ec4-441">ADFSVMNamePrefix</span><span class="sxs-lookup"><span data-stu-id="89ec4-441">ADFSVMNamePrefix</span></span> |<span data-ttu-id="89ec4-442">ADFS 伺服器的虛擬機器名稱前置詞</span><span class="sxs-lookup"><span data-stu-id="89ec4-442">Virtual Machine name prefix for ADFS servers</span></span> |
| <span data-ttu-id="89ec4-443">WAPVMNamePrefix</span><span class="sxs-lookup"><span data-stu-id="89ec4-443">WAPVMNamePrefix</span></span> |<span data-ttu-id="89ec4-444">WAP 伺服器的虛擬機器名稱前置詞</span><span class="sxs-lookup"><span data-stu-id="89ec4-444">Virtual Machine name prefix for WAP servers</span></span> |
| <span data-ttu-id="89ec4-445">ADDCVMSize</span><span class="sxs-lookup"><span data-stu-id="89ec4-445">ADDCVMSize</span></span> |<span data-ttu-id="89ec4-446">網域控制站的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="89ec4-446">The vm size of the Domain Controllers</span></span> |
| <span data-ttu-id="89ec4-447">ADFSVMSize</span><span class="sxs-lookup"><span data-stu-id="89ec4-447">ADFSVMSize</span></span> |<span data-ttu-id="89ec4-448">ADFS 伺服器的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="89ec4-448">The vm size of the ADFS servers</span></span> |
| <span data-ttu-id="89ec4-449">WAPVMSize</span><span class="sxs-lookup"><span data-stu-id="89ec4-449">WAPVMSize</span></span> |<span data-ttu-id="89ec4-450">WAP 伺服器的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="89ec4-450">The vm size of the WAP servers</span></span> |
| <span data-ttu-id="89ec4-451">AdminUserName</span><span class="sxs-lookup"><span data-stu-id="89ec4-451">AdminUserName</span></span> |<span data-ttu-id="89ec4-452">虛擬機器的本機系統管理員名稱</span><span class="sxs-lookup"><span data-stu-id="89ec4-452">The name of the local Administrator of the virtual machines</span></span> |
| <span data-ttu-id="89ec4-453">AdminPassword</span><span class="sxs-lookup"><span data-stu-id="89ec4-453">AdminPassword</span></span> |<span data-ttu-id="89ec4-454">虛擬機器的本機系統管理員帳戶密碼</span><span class="sxs-lookup"><span data-stu-id="89ec4-454">The password for the local Administrator account of the virtual machines</span></span> |

## <a name="additional-resources"></a><span data-ttu-id="89ec4-455">其他資源</span><span class="sxs-lookup"><span data-stu-id="89ec4-455">Additional resources</span></span>
* [<span data-ttu-id="89ec4-456">可用性設定組</span><span class="sxs-lookup"><span data-stu-id="89ec4-456">Availability Sets</span></span>](https://aka.ms/Azure/Availability) 
* [<span data-ttu-id="89ec4-457">Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="89ec4-457">Azure Load Balancer</span></span>](https://aka.ms/Azure/ILB)
* [<span data-ttu-id="89ec4-458">內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="89ec4-458">Internal Load Balancer</span></span>](https://aka.ms/Azure/ILB/Internal)
* [<span data-ttu-id="89ec4-459">網際網路對向負載平衡器</span><span class="sxs-lookup"><span data-stu-id="89ec4-459">Internet Facing Load Balancer</span></span>](https://aka.ms/Azure/ILB/Internet)
* [<span data-ttu-id="89ec4-460">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="89ec4-460">Storage Accounts</span></span>](https://aka.ms/Azure/Storage)
* [<span data-ttu-id="89ec4-461">Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="89ec4-461">Azure Virtual Networks</span></span>](https://aka.ms/Azure/VNet)
* [<span data-ttu-id="89ec4-462">AD FS 和 Web 應用程式 Proxy 連結</span><span class="sxs-lookup"><span data-stu-id="89ec4-462">AD FS and Web Application Proxy Links</span></span>](http://aka.ms/ADFSLinks) 

## <a name="next-steps"></a><span data-ttu-id="89ec4-463">後續步驟</span><span class="sxs-lookup"><span data-stu-id="89ec4-463">Next steps</span></span>
* [<span data-ttu-id="89ec4-464">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89ec4-464">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
* [<span data-ttu-id="89ec4-465">使用 Azure AD Connect 設定和管理 AD FS</span><span class="sxs-lookup"><span data-stu-id="89ec4-465">Configuring and managing your AD FS using Azure AD Connect</span></span>](active-directory-aadconnectfed-whatis.md)
* [<span data-ttu-id="89ec4-466">使用 Azure 流量管理員在 Azure 中部署高可用性跨地區 AD FS</span><span class="sxs-lookup"><span data-stu-id="89ec4-466">High availability cross-geographic AD FS deployment in Azure with Azure Traffic Manager</span></span>](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)

