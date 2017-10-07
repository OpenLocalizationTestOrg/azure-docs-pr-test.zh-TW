---
title: "aaaTroubleshoot Azure rbac 進行 |Microsoft 文件"
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
ms.openlocfilehash: 15feced32d8459d90c4c246d335932f90e1fc91f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-troubleshooting"></a><span data-ttu-id="466ed-103">角色型存取控制疑難排解</span><span class="sxs-lookup"><span data-stu-id="466ed-103">Role-Based Access Control troubleshooting</span></span>

<span data-ttu-id="466ed-104">文件本文會回答有關 hello 特定存取權限的角色，授與的常見問題，好讓您知道哪些 tooexpect 時使用 hello hello Azure 入口網站中的角色，並可以對存取問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="466ed-104">This document article answers common questions about hello specific access rights that are granted with roles, so that you know what tooexpect when using hello roles in hello Azure portal and can troubleshoot access problems.</span></span> <span data-ttu-id="466ed-105">這三種角色涵蓋了所有資源類型︰</span><span class="sxs-lookup"><span data-stu-id="466ed-105">These three roles cover all resource types:</span></span>

* <span data-ttu-id="466ed-106">擁有者</span><span class="sxs-lookup"><span data-stu-id="466ed-106">Owner</span></span>  
* <span data-ttu-id="466ed-107">參與者</span><span class="sxs-lookup"><span data-stu-id="466ed-107">Contributor</span></span>  
* <span data-ttu-id="466ed-108">讀取者</span><span class="sxs-lookup"><span data-stu-id="466ed-108">Reader</span></span>  

<span data-ttu-id="466ed-109">擁有者和參與者都具有完整存取 toohello 管理體驗，但參與者無法提供存取 tooother 使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="466ed-109">Owners and contributors both have full access toohello management experience, but a contributor can’t give access tooother users or groups.</span></span> <span data-ttu-id="466ed-110">變得更有趣 hello 讀取者角色，使用，因此我們可以在其中花一些時間。</span><span class="sxs-lookup"><span data-stu-id="466ed-110">Things get a little more interesting with hello reader role, so that’s where we'll spend some time.</span></span> <span data-ttu-id="466ed-111">請參閱 hello[角色型存取控制取得啟動文章](role-based-access-control-configure.md)如 toogrant 的存取方式的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="466ed-111">See hello [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how toogrant access.</span></span>

## <a name="app-service-workloads"></a><span data-ttu-id="466ed-112">應用程式服務工作負載</span><span class="sxs-lookup"><span data-stu-id="466ed-112">App service workloads</span></span>
### <a name="write-access-capabilities"></a><span data-ttu-id="466ed-113">寫入存取功能</span><span class="sxs-lookup"><span data-stu-id="466ed-113">Write access capabilities</span></span>
<span data-ttu-id="466ed-114">如果您授與使用者唯讀存取 tooa 單一 web 應用程式，您可能會不預期會停用某些功能。</span><span class="sxs-lookup"><span data-stu-id="466ed-114">If you grant a user read-only access tooa single web app, some features are disabled that you might not expect.</span></span> <span data-ttu-id="466ed-115">下列管理功能的 hello 需要**寫入**存取 tooa web 應用程式 （參與者或擁有者），並在任何唯讀案例中無法使用。</span><span class="sxs-lookup"><span data-stu-id="466ed-115">hello following management capabilities require **write** access tooa web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span></span>

* <span data-ttu-id="466ed-116">命令 (像是開始、停止等)</span><span class="sxs-lookup"><span data-stu-id="466ed-116">Commands (like start, stop, etc.)</span></span>
* <span data-ttu-id="466ed-117">變更像是一般組態的設定、調整設定、備份設定與監視設定</span><span class="sxs-lookup"><span data-stu-id="466ed-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span></span>
* <span data-ttu-id="466ed-118">存取發佈認證與其他機密，像是應用程式設定與連接字串</span><span class="sxs-lookup"><span data-stu-id="466ed-118">Accessing publishing credentials and other secrets like app settings and connection strings</span></span>
* <span data-ttu-id="466ed-119">串流記錄</span><span class="sxs-lookup"><span data-stu-id="466ed-119">Streaming logs</span></span>
* <span data-ttu-id="466ed-120">診斷記錄組態</span><span class="sxs-lookup"><span data-stu-id="466ed-120">Diagnostic logs configuration</span></span>
* <span data-ttu-id="466ed-121">主控台 (命令提示字元)</span><span class="sxs-lookup"><span data-stu-id="466ed-121">Console (command prompt)</span></span>
* <span data-ttu-id="466ed-122">有效的近期部署項目 (以便本機 git 持續部署)</span><span class="sxs-lookup"><span data-stu-id="466ed-122">Active and recent deployments (for local git continuous deployment)</span></span>
* <span data-ttu-id="466ed-123">預估的花費</span><span class="sxs-lookup"><span data-stu-id="466ed-123">Estimated spend</span></span>
* <span data-ttu-id="466ed-124">Web 測試</span><span class="sxs-lookup"><span data-stu-id="466ed-124">Web tests</span></span>
* <span data-ttu-id="466ed-125">虛擬網路 （只顯示 tooa 讀取器如果先前已由具有寫入權限的使用者設定的虛擬網路）。</span><span class="sxs-lookup"><span data-stu-id="466ed-125">Virtual network (only visible tooa reader if a virtual network has previously been configured by a user with write access).</span></span>

<span data-ttu-id="466ed-126">如果您無法存取任何這些圖格，您需要 tooask 您的系統管理員參與者存取 toohello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="466ed-126">If you can't access any of these tiles, you need tooask your administrator for Contributor access toohello web app.</span></span>

### <a name="dealing-with-related-resources"></a><span data-ttu-id="466ed-127">處理相關資源</span><span class="sxs-lookup"><span data-stu-id="466ed-127">Dealing with related resources</span></span>
<span data-ttu-id="466ed-128">Web 應用程式被複雜的幾個不同的資源，相互作用 hello 存在。</span><span class="sxs-lookup"><span data-stu-id="466ed-128">Web apps are complicated by hello presence of a few different resources that interplay.</span></span> <span data-ttu-id="466ed-129">以下是具有多個網站的典型資源群組：</span><span class="sxs-lookup"><span data-stu-id="466ed-129">Here is a typical resource group with a couple websites:</span></span>

![Web 應用程式資源群組](./media/role-based-access-control-troubleshooting/website-resource-model.png)

<span data-ttu-id="466ed-131">如此一來，如果您授與其他人存取 toojust hello web 應用程式，大部分的 hello hello hello Azure 入口網站中的網站] 刀鋒視窗的功能已停用。</span><span class="sxs-lookup"><span data-stu-id="466ed-131">As a result, if you grant someone access toojust hello web app, much of hello functionality on hello website blade in hello Azure portal is disabled.</span></span>

<span data-ttu-id="466ed-132">這些項目需要**寫入**存取 toohello **App Service 方案**對應 tooyour 網站：</span><span class="sxs-lookup"><span data-stu-id="466ed-132">These items require **write** access toohello **App Service plan** that corresponds tooyour website:</span></span>  

* <span data-ttu-id="466ed-133">檢視 hello web 應用程式的定價層 （免費或標準）</span><span class="sxs-lookup"><span data-stu-id="466ed-133">Viewing hello web app’s pricing tier (Free or Standard)</span></span>  
* <span data-ttu-id="466ed-134">調整組態 (執行個體數量、虛擬機器大小、自動調整設定)</span><span class="sxs-lookup"><span data-stu-id="466ed-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span></span>  
* <span data-ttu-id="466ed-135">配額 (儲存容量、頻寬、CPU)</span><span class="sxs-lookup"><span data-stu-id="466ed-135">Quotas (storage, bandwidth, CPU)</span></span>  

<span data-ttu-id="466ed-136">這些項目需要**寫入**存取 toohello 整個**資源群組**，其中包含您的網站：</span><span class="sxs-lookup"><span data-stu-id="466ed-136">These items require **write** access toohello whole **Resource group** that contains your website:</span></span>  

* <span data-ttu-id="466ed-137">SSL 憑證和繫結 (可以在 hello 的站台間共用的 SSL 憑證相同的資源群組和地理位置)</span><span class="sxs-lookup"><span data-stu-id="466ed-137">SSL Certificates and bindings (SSL certificates can be shared between sites in hello same resource group and geo-location)</span></span>  
* <span data-ttu-id="466ed-138">警示規則</span><span class="sxs-lookup"><span data-stu-id="466ed-138">Alert rules</span></span>  
* <span data-ttu-id="466ed-139">自動調整設定</span><span class="sxs-lookup"><span data-stu-id="466ed-139">Autoscale settings</span></span>  
* <span data-ttu-id="466ed-140">應用程式見解元件</span><span class="sxs-lookup"><span data-stu-id="466ed-140">Application insights components</span></span>  
* <span data-ttu-id="466ed-141">Web 測試</span><span class="sxs-lookup"><span data-stu-id="466ed-141">Web tests</span></span>  

## <a name="virtual-machine-workloads"></a><span data-ttu-id="466ed-142">虛擬機器工作負載</span><span class="sxs-lookup"><span data-stu-id="466ed-142">Virtual machine workloads</span></span>
<span data-ttu-id="466ed-143">更像透過 web 應用程式，hello 虛擬機器刀鋒視窗上的某些功能需要寫入權限 toohello 虛擬機器或 tooother hello 資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="466ed-143">Much like with web apps, some features on hello virtual machine blade require write access toohello virtual machine, or tooother resources in hello resource group.</span></span>

<span data-ttu-id="466ed-144">虛擬機器是相關的 tooDomain 名稱、 虛擬網路、 儲存體帳戶和警示規則。</span><span class="sxs-lookup"><span data-stu-id="466ed-144">Virtual machines are related tooDomain names, virtual networks, storage accounts, and alert rules.</span></span>

<span data-ttu-id="466ed-145">這些項目需要**寫入**存取 toohello**虛擬機器**:</span><span class="sxs-lookup"><span data-stu-id="466ed-145">These items require **write** access toohello **Virtual machine**:</span></span>

* <span data-ttu-id="466ed-146">端點</span><span class="sxs-lookup"><span data-stu-id="466ed-146">Endpoints</span></span>  
* <span data-ttu-id="466ed-147">IP 位址</span><span class="sxs-lookup"><span data-stu-id="466ed-147">IP addresses</span></span>  
* <span data-ttu-id="466ed-148">磁碟</span><span class="sxs-lookup"><span data-stu-id="466ed-148">Disks</span></span>  
* <span data-ttu-id="466ed-149">擴充功能</span><span class="sxs-lookup"><span data-stu-id="466ed-149">Extensions</span></span>  

<span data-ttu-id="466ed-150">這些都需要**寫入**存取 tooboth hello**虛擬機器**，和 hello**資源群組**（hello 網域名稱），就會在：</span><span class="sxs-lookup"><span data-stu-id="466ed-150">These require **write** access tooboth hello **Virtual machine**, and hello **Resource group** (along with hello Domain name) that it is in:</span></span>  

* <span data-ttu-id="466ed-151">可用性集合</span><span class="sxs-lookup"><span data-stu-id="466ed-151">Availability set</span></span>  
* <span data-ttu-id="466ed-152">負載平衡集合</span><span class="sxs-lookup"><span data-stu-id="466ed-152">Load balanced set</span></span>  
* <span data-ttu-id="466ed-153">警示規則</span><span class="sxs-lookup"><span data-stu-id="466ed-153">Alert rules</span></span>  

<span data-ttu-id="466ed-154">如果您無法存取任何這些圖格，詢問您的參與者存取 toohello 資源群組系統管理員。</span><span class="sxs-lookup"><span data-stu-id="466ed-154">If you can't access any of these tiles, ask your administrator for Contributor access toohello Resource group.</span></span>

## <a name="see-more"></a><span data-ttu-id="466ed-155">更多資訊</span><span class="sxs-lookup"><span data-stu-id="466ed-155">See more</span></span>
* <span data-ttu-id="466ed-156">[Role Based Access Control](role-based-access-control-configure.md)： 開始使用 RBAC hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="466ed-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="466ed-157">[內建角色](role-based-access-built-in-roles.md)： 取得標準中 RBAC 的 hello 角色的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="466ed-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about hello roles that come standard in RBAC.</span></span>
* <span data-ttu-id="466ed-158">[在 Azure rbac 進行的自訂角色](role-based-access-control-custom-roles.md)： 了解 toocreate 自訂角色 toofit 您存取需要的方式。</span><span class="sxs-lookup"><span data-stu-id="466ed-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how toocreate custom roles toofit your access needs.</span></span>
* <span data-ttu-id="466ed-159">[建立存取權變更歷程記錄報告](role-based-access-control-access-change-history-report.md)︰追蹤 RBAC 中的角色指派變更。</span><span class="sxs-lookup"><span data-stu-id="466ed-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span></span>

