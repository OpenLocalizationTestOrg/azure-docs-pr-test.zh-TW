---
title: "針對 Azure RBAC 進行疑難排解 | Microsoft Docs"
description: "取得有關角色型存取控制資源問題或疑問的協助。"
services: azure-portal
documentationcenter: na
author: andredm7
manager: femila
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 407c030ea159915d4d7ac21760a3d17ec2204372
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="role-based-access-control-troubleshooting"></a><span data-ttu-id="378f9-103">角色型存取控制疑難排解</span><span class="sxs-lookup"><span data-stu-id="378f9-103">Role-Based Access Control troubleshooting</span></span>

<span data-ttu-id="378f9-104">本文將回答關於授與角色之特定存取權限的常見問題，讓您知道在 Azure 入口網站中使用角色時預期能夠使用哪些項目，以及如何針對存取問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="378f9-104">This document article answers common questions about the specific access rights that are granted with roles, so that you know what to expect when using the roles in the Azure portal and can troubleshoot access problems.</span></span> <span data-ttu-id="378f9-105">這三種角色涵蓋了所有資源類型︰</span><span class="sxs-lookup"><span data-stu-id="378f9-105">These three roles cover all resource types:</span></span>

* <span data-ttu-id="378f9-106">擁有者</span><span class="sxs-lookup"><span data-stu-id="378f9-106">Owner</span></span>  
* <span data-ttu-id="378f9-107">參與者</span><span class="sxs-lookup"><span data-stu-id="378f9-107">Contributor</span></span>  
* <span data-ttu-id="378f9-108">讀取者</span><span class="sxs-lookup"><span data-stu-id="378f9-108">Reader</span></span>  

<span data-ttu-id="378f9-109">擁有者與參與者都可以完整存取管理經驗，但參與者無法將存取權限授予其他使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="378f9-109">Owners and contributors both have full access to the management experience, but a contributor can’t give access to other users or groups.</span></span> <span data-ttu-id="378f9-110">讀取者角色則是比較有趣，因此我們會在本文中多花點時間介紹。</span><span class="sxs-lookup"><span data-stu-id="378f9-110">Things get a little more interesting with the reader role, so that’s where we'll spend some time.</span></span> <span data-ttu-id="378f9-111">請參閱 [角色型存取控制入門文章](role-based-access-control-configure.md) ，以詳細了解如何授與存取權。</span><span class="sxs-lookup"><span data-stu-id="378f9-111">See the [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how to grant access.</span></span>

## <a name="app-service-workloads"></a><span data-ttu-id="378f9-112">應用程式服務工作負載</span><span class="sxs-lookup"><span data-stu-id="378f9-112">App service workloads</span></span>
### <a name="write-access-capabilities"></a><span data-ttu-id="378f9-113">寫入存取功能</span><span class="sxs-lookup"><span data-stu-id="378f9-113">Write access capabilities</span></span>
<span data-ttu-id="378f9-114">如果您授與對單一 Web 應用程式授與使用者唯讀存取權限，部分功能可能會在未預期的情況下停用。</span><span class="sxs-lookup"><span data-stu-id="378f9-114">If you grant a user read-only access to a single web app, some features are disabled that you might not expect.</span></span> <span data-ttu-id="378f9-115">以下管理功能需要 Web 應用程式的**寫入**存取權限 (參與者或擁有者)，而且無法在任何唯讀情況中使用。</span><span class="sxs-lookup"><span data-stu-id="378f9-115">The following management capabilities require **write** access to a web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span></span>

* <span data-ttu-id="378f9-116">命令 (像是開始、停止等)</span><span class="sxs-lookup"><span data-stu-id="378f9-116">Commands (like start, stop, etc.)</span></span>
* <span data-ttu-id="378f9-117">變更像是一般組態的設定、調整設定、備份設定與監視設定</span><span class="sxs-lookup"><span data-stu-id="378f9-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span></span>
* <span data-ttu-id="378f9-118">存取發佈認證與其他機密，像是應用程式設定與連接字串</span><span class="sxs-lookup"><span data-stu-id="378f9-118">Accessing publishing credentials and other secrets like app settings and connection strings</span></span>
* <span data-ttu-id="378f9-119">串流記錄</span><span class="sxs-lookup"><span data-stu-id="378f9-119">Streaming logs</span></span>
* <span data-ttu-id="378f9-120">診斷記錄組態</span><span class="sxs-lookup"><span data-stu-id="378f9-120">Diagnostic logs configuration</span></span>
* <span data-ttu-id="378f9-121">主控台 (命令提示字元)</span><span class="sxs-lookup"><span data-stu-id="378f9-121">Console (command prompt)</span></span>
* <span data-ttu-id="378f9-122">有效的近期部署項目 (以便本機 git 持續部署)</span><span class="sxs-lookup"><span data-stu-id="378f9-122">Active and recent deployments (for local git continuous deployment)</span></span>
* <span data-ttu-id="378f9-123">預估的花費</span><span class="sxs-lookup"><span data-stu-id="378f9-123">Estimated spend</span></span>
* <span data-ttu-id="378f9-124">Web 測試</span><span class="sxs-lookup"><span data-stu-id="378f9-124">Web tests</span></span>
* <span data-ttu-id="378f9-125">虛擬網路 (只有當虛擬網路先前是由具備寫入存取權限的使用者所設定，才會顯示出來)。</span><span class="sxs-lookup"><span data-stu-id="378f9-125">Virtual network (only visible to a reader if a virtual network has previously been configured by a user with write access).</span></span>

<span data-ttu-id="378f9-126">如果您無法存取上述任何一個磚，請洽詢您的系統管理員，取得 Web 應用程式的參與者存取權限。</span><span class="sxs-lookup"><span data-stu-id="378f9-126">If you can't access any of these tiles, you need to ask your administrator for Contributor access to the web app.</span></span>

### <a name="dealing-with-related-resources"></a><span data-ttu-id="378f9-127">處理相關資源</span><span class="sxs-lookup"><span data-stu-id="378f9-127">Dealing with related resources</span></span>
<span data-ttu-id="378f9-128">Web 應用程式因為幾個互有關聯的資源而顯得複雜。</span><span class="sxs-lookup"><span data-stu-id="378f9-128">Web apps are complicated by the presence of a few different resources that interplay.</span></span> <span data-ttu-id="378f9-129">以下是具有多個網站的典型資源群組：</span><span class="sxs-lookup"><span data-stu-id="378f9-129">Here is a typical resource group with a couple websites:</span></span>

![Web 應用程式資源群組](./media/role-based-access-control-troubleshooting/website-resource-model.png)

<span data-ttu-id="378f9-131">如此一來，如果您只授予某人 Web 應用程式存取權限，Azure 入口網站的網站刀鋒視窗上的諸多功能即會停用。</span><span class="sxs-lookup"><span data-stu-id="378f9-131">As a result, if you grant someone access to just the web app, much of the functionality on the website blade in the Azure portal is disabled.</span></span>

<span data-ttu-id="378f9-132">這些項目需要對應至您網站的「應用程式服務方案」的**寫入**權：</span><span class="sxs-lookup"><span data-stu-id="378f9-132">These items require **write** access to the **App Service plan** that corresponds to your website:</span></span>  

* <span data-ttu-id="378f9-133">檢視 Web 應用程式的定價層 (免費或標準)</span><span class="sxs-lookup"><span data-stu-id="378f9-133">Viewing the web app’s pricing tier (Free or Standard)</span></span>  
* <span data-ttu-id="378f9-134">調整組態 (執行個體數量、虛擬機器大小、自動調整設定)</span><span class="sxs-lookup"><span data-stu-id="378f9-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span></span>  
* <span data-ttu-id="378f9-135">配額 (儲存容量、頻寬、CPU)</span><span class="sxs-lookup"><span data-stu-id="378f9-135">Quotas (storage, bandwidth, CPU)</span></span>  

<span data-ttu-id="378f9-136">這些項目都需要包含您網站的整個「資源群組」的**寫入**權：</span><span class="sxs-lookup"><span data-stu-id="378f9-136">These items require **write** access to the whole **Resource group** that contains your website:</span></span>  

* <span data-ttu-id="378f9-137">SSL 憑證與繫結 (相同資源群組與地理位置中的各個網站之間，可共用 SSL 憑證)</span><span class="sxs-lookup"><span data-stu-id="378f9-137">SSL Certificates and bindings (SSL certificates can be shared between sites in the same resource group and geo-location)</span></span>  
* <span data-ttu-id="378f9-138">警示規則</span><span class="sxs-lookup"><span data-stu-id="378f9-138">Alert rules</span></span>  
* <span data-ttu-id="378f9-139">自動調整設定</span><span class="sxs-lookup"><span data-stu-id="378f9-139">Autoscale settings</span></span>  
* <span data-ttu-id="378f9-140">應用程式見解元件</span><span class="sxs-lookup"><span data-stu-id="378f9-140">Application insights components</span></span>  
* <span data-ttu-id="378f9-141">Web 測試</span><span class="sxs-lookup"><span data-stu-id="378f9-141">Web tests</span></span>  

## <a name="virtual-machine-workloads"></a><span data-ttu-id="378f9-142">虛擬機器工作負載</span><span class="sxs-lookup"><span data-stu-id="378f9-142">Virtual machine workloads</span></span>
<span data-ttu-id="378f9-143">差不多與 Web 應用程式相同的是，虛擬機器分頁上的某些功能需要具備虛擬機器 (或是資源群組中的其他資源) 的寫入存取權限。</span><span class="sxs-lookup"><span data-stu-id="378f9-143">Much like with web apps, some features on the virtual machine blade require write access to the virtual machine, or to other resources in the resource group.</span></span>

<span data-ttu-id="378f9-144">虛擬機器與網域名稱、虛擬網路、儲存體帳戶及警示規則相關。</span><span class="sxs-lookup"><span data-stu-id="378f9-144">Virtual machines are related to Domain names, virtual networks, storage accounts, and alert rules.</span></span>

<span data-ttu-id="378f9-145">這些項目都需要具備「虛擬機器」的**寫入**權：</span><span class="sxs-lookup"><span data-stu-id="378f9-145">These items require **write** access to the **Virtual machine**:</span></span>

* <span data-ttu-id="378f9-146">端點</span><span class="sxs-lookup"><span data-stu-id="378f9-146">Endpoints</span></span>  
* <span data-ttu-id="378f9-147">IP 位址</span><span class="sxs-lookup"><span data-stu-id="378f9-147">IP addresses</span></span>  
* <span data-ttu-id="378f9-148">磁碟</span><span class="sxs-lookup"><span data-stu-id="378f9-148">Disks</span></span>  
* <span data-ttu-id="378f9-149">擴充功能</span><span class="sxs-lookup"><span data-stu-id="378f9-149">Extensions</span></span>  

<span data-ttu-id="378f9-150">這些項目都需要同時具備「虛擬機器」與所屬之「資源群組」(連同網域名稱) 的**寫入**權：</span><span class="sxs-lookup"><span data-stu-id="378f9-150">These require **write** access to both the **Virtual machine**, and the **Resource group** (along with the Domain name) that it is in:</span></span>  

* <span data-ttu-id="378f9-151">可用性設定組</span><span class="sxs-lookup"><span data-stu-id="378f9-151">Availability set</span></span>  
* <span data-ttu-id="378f9-152">負載平衡集合</span><span class="sxs-lookup"><span data-stu-id="378f9-152">Load balanced set</span></span>  
* <span data-ttu-id="378f9-153">警示規則</span><span class="sxs-lookup"><span data-stu-id="378f9-153">Alert rules</span></span>  

<span data-ttu-id="378f9-154">如果您無法存取上述任何一個磚，請洽詢您的系統管理員，以取得資源群組的參與者存取權限。</span><span class="sxs-lookup"><span data-stu-id="378f9-154">If you can't access any of these tiles, ask your administrator for Contributor access to the Resource group.</span></span>

## <a name="see-more"></a><span data-ttu-id="378f9-155">更多資訊</span><span class="sxs-lookup"><span data-stu-id="378f9-155">See more</span></span>
* <span data-ttu-id="378f9-156">[角色型存取控制](role-based-access-control-configure.md)：開始在 Azure 入口網站中使用 RBAC。</span><span class="sxs-lookup"><span data-stu-id="378f9-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="378f9-157">[內建角色](role-based-access-built-in-roles.md)︰取得有關 RBAC 中標準角色的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="378f9-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about the roles that come standard in RBAC.</span></span>
* <span data-ttu-id="378f9-158">[Azure RBAC 中的自訂角色](role-based-access-control-custom-roles.md)︰了解如何建立自訂角色，以符合您的存取需求。</span><span class="sxs-lookup"><span data-stu-id="378f9-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how to create custom roles to fit your access needs.</span></span>
* <span data-ttu-id="378f9-159">[建立存取權變更歷程記錄報告](role-based-access-control-access-change-history-report.md)︰追蹤 RBAC 中的角色指派變更。</span><span class="sxs-lookup"><span data-stu-id="378f9-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span></span>

