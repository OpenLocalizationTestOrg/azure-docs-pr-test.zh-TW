---
title: "進行從 VMware 到 Azure 的 Azure Site Recovery 疑難排解 | Microsoft Docs"
description: "針對複寫 Azure 虛擬機器時的錯誤進行疑難排解"
services: site-recovery
documentationcenter: 
author: asgang
manager: srinathv
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/24/2017
ms.author: asgang
ms.openlocfilehash: 1e2452ccc6d3f1859a39e1ee09cdde32f53767ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-mobility-service-push-install-issues"></a><span data-ttu-id="2d134-103">針對行動服務推送安裝問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="2d134-103">Troubleshooting Mobility Service push install issues</span></span>

<span data-ttu-id="2d134-104">本文詳細說明嘗試在來源伺服器上安裝行動服務以便啟用保護時所面臨的常見問題。</span><span class="sxs-lookup"><span data-stu-id="2d134-104">This article details the common issues faced when trying to install the Mobility Service on to source server for enabling protection.</span></span>

## <a name="error-code-95107-protection-could-not-be-enabled"></a><span data-ttu-id="2d134-105">(錯誤碼 95107) 無法啟用保護。</span><span class="sxs-lookup"><span data-stu-id="2d134-105">(Error code 95107) Protection could not be enabled.</span></span>
<span data-ttu-id="2d134-106">**錯誤碼**</span><span class="sxs-lookup"><span data-stu-id="2d134-106">**Error code**</span></span> | <span data-ttu-id="2d134-107">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="2d134-107">**Possible causes**</span></span> | <span data-ttu-id="2d134-108">**特定錯誤的建議**</span><span class="sxs-lookup"><span data-stu-id="2d134-108">**Error-specific Recommendations**</span></span>
--- | --- | ---
<span data-ttu-id="2d134-109">95107</span><span class="sxs-lookup"><span data-stu-id="2d134-109">95107</span></span> </br><span data-ttu-id="2d134-110">***訊息 -***  將行動服務推送安裝到來源電腦失敗，錯誤碼為 ***EP0858***。</span><span class="sxs-lookup"><span data-stu-id="2d134-110">***Message -***  Push installation of the mobility service to the source machine failed with error code ***EP0858***.</span></span> <br> <span data-ttu-id="2d134-111">可能是所提供用以安裝行動服務的認證不正確，或使用者帳戶的權限不足</span><span class="sxs-lookup"><span data-stu-id="2d134-111">Either that the credentials provided to install mobility service is incorrect or the user account has insufficient privileges</span></span> | <span data-ttu-id="2d134-112">為了在來源電腦上安裝行動服務所提供的使用者認證不正確</span><span class="sxs-lookup"><span data-stu-id="2d134-112">User credentials provided to install mobility service on source machine is incorrect</span></span> | <span data-ttu-id="2d134-113">請確定組態伺服器上針對來源電腦提供的使用者認證正確無誤。</span><span class="sxs-lookup"><span data-stu-id="2d134-113">Ensure the user credentials provided for the source machine on configuration server are correct.</span></span> <br> <span data-ttu-id="2d134-114">若要新增/編輯使用者認證：前往組態伺服器 > Cspsconfigtool 圖示 > 管理帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d134-114">To add/edit user credentials: go to configuration server > Cspsconfigtool icon > Manage account.</span></span> </br> <span data-ttu-id="2d134-115">此外，確保已檢查以下必要條件，才能成功完成推送安裝。</span><span class="sxs-lookup"><span data-stu-id="2d134-115">In addition, ensure below pre-requisites are checked to successfully complete push install.</span></span>

## <a name="error-code-95015-protection-could-not-be-enabled"></a><span data-ttu-id="2d134-116">(錯誤碼 95015) 無法啟用保護。</span><span class="sxs-lookup"><span data-stu-id="2d134-116">(Error code 95015) Protection could not be enabled.</span></span>
<span data-ttu-id="2d134-117">**錯誤碼**</span><span class="sxs-lookup"><span data-stu-id="2d134-117">**Error code**</span></span> | <span data-ttu-id="2d134-118">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="2d134-118">**Possible causes**</span></span> | <span data-ttu-id="2d134-119">**特定錯誤的建議**</span><span class="sxs-lookup"><span data-stu-id="2d134-119">**Error-specific Recommendations**</span></span>
--- | --- | ---
<span data-ttu-id="2d134-120">95105</span><span class="sxs-lookup"><span data-stu-id="2d134-120">95105</span></span> </br><span data-ttu-id="2d134-121">***訊息 -***  將行動服務推送安裝到來源電腦失敗，錯誤碼為 ***EP0856***。</span><span class="sxs-lookup"><span data-stu-id="2d134-121">***Message -***  Push installation of the mobility service to the source machine failed with error code ***EP0856***.</span></span> <br> <span data-ttu-id="2d134-122">不是來源電腦不允許 [檔案及印表機共用]，就是處理序伺服器與來源電腦之間有網路連線問題</span><span class="sxs-lookup"><span data-stu-id="2d134-122">Either “File and Printer Sharing” not allowed on the source machine, or there are network connectivity issues between the process server and the source machine</span></span>| <span data-ttu-id="2d134-123">未啟用檔案及印表機共用</span><span class="sxs-lookup"><span data-stu-id="2d134-123">File and print sharing is not enabled</span></span> | <span data-ttu-id="2d134-124">Windows 防火牆中的來源電腦允許 [檔案及印表機共用]，請移至來源電腦 > 在 Windows 防火牆設定之下 > [允許應用程式或功能通過防火牆] > 為所有設定檔選取 [檔案及印表機共用]。</span><span class="sxs-lookup"><span data-stu-id="2d134-124">Allow “File and Printer Sharing” on the source machine in the Windows Firewall, Go to the source machine > Under Windows Firewall settings > “Allow an app or feature through Firewall” > select “File and Printer Sharing for all profiles”.</span></span> </br> <span data-ttu-id="2d134-125">此外，確保已檢查以下必要條件，才能成功完成推送安裝。</span><span class="sxs-lookup"><span data-stu-id="2d134-125">In addition, ensure below pre-requisites are checked to successfully complete push install.</span></span>

## <a name="error-code-95117-protection-could-not-be-enabled"></a><span data-ttu-id="2d134-126">(錯誤碼 95117) 無法啟用保護。</span><span class="sxs-lookup"><span data-stu-id="2d134-126">(Error code 95117) Protection could not be enabled.</span></span>
<span data-ttu-id="2d134-127">**錯誤碼**</span><span class="sxs-lookup"><span data-stu-id="2d134-127">**Error code**</span></span> | <span data-ttu-id="2d134-128">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="2d134-128">**Possible causes**</span></span> | <span data-ttu-id="2d134-129">**特定錯誤的建議**</span><span class="sxs-lookup"><span data-stu-id="2d134-129">**Error-specific Recommendations**</span></span>
--- | --- | ---
<span data-ttu-id="2d134-130">95117</span><span class="sxs-lookup"><span data-stu-id="2d134-130">95117</span></span> </br><span data-ttu-id="2d134-131">***訊息 -***  將行動服務推送安裝到來源電腦失敗，錯誤碼為 ***EP0865***。</span><span class="sxs-lookup"><span data-stu-id="2d134-131">***Message -***  Push installation of the mobility service to the source machine failed with error code ***EP0865***.</span></span> <br> <span data-ttu-id="2d134-132">不是來源電腦不在執行中，就是處理序伺服器與來源電腦之間有網路連線問題</span><span class="sxs-lookup"><span data-stu-id="2d134-132">Either the source machine is not running, or there are network connectivity issues between the process server and the source machine</span></span> | <span data-ttu-id="2d134-133">處理序伺服器與來源伺服器之間的網路連線能力</span><span class="sxs-lookup"><span data-stu-id="2d134-133">Network connectivity between process server and source server</span></span> | <span data-ttu-id="2d134-134">檢查處理序伺服器與來源伺服器之間的連線能力。</span><span class="sxs-lookup"><span data-stu-id="2d134-134">Check connectivity between process server and source server.</span></span> </br> <span data-ttu-id="2d134-135">此外，確保已檢查以下必要條件，才能成功完成推送安裝。</span><span class="sxs-lookup"><span data-stu-id="2d134-135">In addition, ensure below pre-requisites are checked to successfully complete push install.</span></span>

## <a name="error-code-95103-protection-could-not-be-enabled"></a><span data-ttu-id="2d134-136">(錯誤碼 95103) 無法啟用保護。</span><span class="sxs-lookup"><span data-stu-id="2d134-136">(Error code 95103) Protection could not be enabled.</span></span>
<span data-ttu-id="2d134-137">**錯誤碼**</span><span class="sxs-lookup"><span data-stu-id="2d134-137">**Error code**</span></span> | <span data-ttu-id="2d134-138">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="2d134-138">**Possible causes**</span></span> | <span data-ttu-id="2d134-139">**特定錯誤的建議**</span><span class="sxs-lookup"><span data-stu-id="2d134-139">**Error-specific Recommendations**</span></span>
--- | --- | ---
<span data-ttu-id="2d134-140">95103</span><span class="sxs-lookup"><span data-stu-id="2d134-140">95103</span></span> </br><span data-ttu-id="2d134-141">***訊息 -***  將行動服務推送安裝到來源電腦失敗，錯誤碼為 ***EP0854***。</span><span class="sxs-lookup"><span data-stu-id="2d134-141">***Message -***  Push installation of the mobility service to the source machine failed with error code ***EP0854***.</span></span> <br> <span data-ttu-id="2d134-142">不是來源電腦不允許 [Windows Management Instrumentation (WMI)]，就是處理序伺服器與來源電腦之間有網路連線問題</span><span class="sxs-lookup"><span data-stu-id="2d134-142">Either “Windows Management Instrumentation (WMI)”is not allowed on the source machine, or there are network connectivity issues between the process server and the source machine</span></span>| <span data-ttu-id="2d134-143">Windows 防火牆中封鎖的 Windows Management Instrumentation (WMI)</span><span class="sxs-lookup"><span data-stu-id="2d134-143">Windows Management Instrumentation (WMI) blocked in the Windows Firewall</span></span> | <span data-ttu-id="2d134-144">允許 Windows 防火牆中封鎖的 Windows Management Instrumentation (WMI)。</span><span class="sxs-lookup"><span data-stu-id="2d134-144">Allow Windows Management Instrumentation (WMI) in the Windows Firewall.</span></span> <span data-ttu-id="2d134-145">在 Windows 防火牆設定之下 > [允許應用程式或功能通過防火牆] > [為所有設定檔選取 WMI]。</span><span class="sxs-lookup"><span data-stu-id="2d134-145">Under Windows Firewall settings > “Allow an app or feature through Firewall” > “select WMI for all profiles”.</span></span> </br> <span data-ttu-id="2d134-146">此外，確保已檢查以下必要條件，才能成功完成推送安裝。</span><span class="sxs-lookup"><span data-stu-id="2d134-146">In addition, ensure below pre-requisites are checked to successfully complete push install.</span></span>

## <a name="check-push-install-logs-for-errors"></a><span data-ttu-id="2d134-147">檢查推送安裝記錄中的錯誤</span><span class="sxs-lookup"><span data-stu-id="2d134-147">Check Push Install Logs for errors</span></span>

<span data-ttu-id="2d134-148">在組態/處理序伺服器上，瀏覽至位於 <Microsoft Azure Site Recovery Install Location>\home\svsystems\pushinstallsvc\ 的 'PushinstallService' 檔案，以了解問題來源並使用下列疑難排解步驟來解決問題。</span><span class="sxs-lookup"><span data-stu-id="2d134-148">On the Configuration/Process server, Navigate to file 'PushinstallService' located at <Microsoft Azure Site Recovery Install Location>\home\svsystems\pushinstallsvc\ to understand the source of the problem and use below troubleshooting steps to resolve the issue.</span></span></br><span data-ttu-id="2d134-149">
![pushiinstalllogs](./media/site-recovery-protection-common-errors/pushinstalllogs.png)</span><span class="sxs-lookup"><span data-stu-id="2d134-149">
![pushiinstalllogs](./media/site-recovery-protection-common-errors/pushinstalllogs.png)</span></span>

## <a name="push-install-pre-requisites-for-windows"></a><span data-ttu-id="2d134-150">適用於 Windows 的推送安裝必要元件</span><span class="sxs-lookup"><span data-stu-id="2d134-150">Push Install pre-requisites for Windows</span></span>
### <a name="ensure-file-and-printer-sharing-is-enabled"></a><span data-ttu-id="2d134-151">確保已啟用 [檔案及印表機共用]</span><span class="sxs-lookup"><span data-stu-id="2d134-151">Ensure "File and Printer Sharing" is enabled</span></span>
<span data-ttu-id="2d134-152">在 Windows 防火牆中的來源電腦允許 [檔案及印表機共用] 和 [Windows Management Instrumentation]</span><span class="sxs-lookup"><span data-stu-id="2d134-152">Allow “File and Printer Sharing” and "Windows Management Instrumentation" on the source machine in the Windows Firewall</span></span> </br>
#### <a name="if-source-machine-is-domain-joined-br"></a><span data-ttu-id="2d134-153">如果來源電腦已加入網域：</span><span class="sxs-lookup"><span data-stu-id="2d134-153">If Source machine is Domain Joined:</span></span> </br>
<span data-ttu-id="2d134-154">使用群組原則管理主控台 (GPMC) 來進行防火牆設定。</span><span class="sxs-lookup"><span data-stu-id="2d134-154">Configure firewall settings using Group Policy Management Console (GPMC).</span></span>
1. <span data-ttu-id="2d134-155">以系統管理員身分登入 Active Directory 網域電腦並開啟 [群組原則管理主控台] (GPMC.MSC，從 [開始] > [執行] 來執行)。</span><span class="sxs-lookup"><span data-stu-id="2d134-155">Login to Active directory domain machine as administrator and open Group Policy Management Console (GPMC.MSC, run from a Start > Run).</span></span></br>
3. <span data-ttu-id="2d134-156">如果未安裝 GPMC，請依照下列連結來[安裝 GPMC](https://technet.microsoft.com/library/cc725932.aspx)</span><span class="sxs-lookup"><span data-stu-id="2d134-156">If GPMC is not installed, follow the link to [Install the GPMC](https://technet.microsoft.com/library/cc725932.aspx)</span></span> </br>
4. <span data-ttu-id="2d134-157">在 GPMC 主控台樹狀目錄中，連按兩下樹系和網域中的 [群組原則物件]，並瀏覽至 [預設網域原則]。</span><span class="sxs-lookup"><span data-stu-id="2d134-157">In the GPMC console tree, double-click Group Policy Objects in the forest and domain and navigate to “Default Domain Policy”.</span></span> </br><span data-ttu-id="2d134-158">
![gpmc1](./media/site-recovery-protection-common-errors/gpmc1.png)</span><span class="sxs-lookup"><span data-stu-id="2d134-158">
![gpmc1](./media/site-recovery-protection-common-errors/gpmc1.png)</span></span> </br>
</br>
5. <span data-ttu-id="2d134-159">以滑鼠右鍵按一下 [預設網域原則] > 編輯 > 將會開啟新的 [群組原則管理編輯器] 視窗。</span><span class="sxs-lookup"><span data-stu-id="2d134-159">Right-click on “Default Domain Policy” > edit > A new “Group Policy Management Editor” window will be opened.</span></span> </br><span data-ttu-id="2d134-160">
![gpmc2](./media/site-recovery-protection-common-errors/gpmc2.png)</span><span class="sxs-lookup"><span data-stu-id="2d134-160">
![gpmc2](./media/site-recovery-protection-common-errors/gpmc2.png)</span></span> </br>
</br>
6. <span data-ttu-id="2d134-161">在 [群組原則管理編輯器] 中，瀏覽至 [電腦設定] > [原則] > [系統管理範本] > [網路] > [網路連線] > [Windows 防火牆]。</span><span class="sxs-lookup"><span data-stu-id="2d134-161">In the Group Policy Management Editor navigate to Computer Configuration > Policies > Administrative Templates > Network > Network Connections > Windows Firewall.</span></span> </br><span data-ttu-id="2d134-162">
![gpmc3](./media/site-recovery-protection-common-errors/gpmc3.png)</span><span class="sxs-lookup"><span data-stu-id="2d134-162">
![gpmc3](./media/site-recovery-protection-common-errors/gpmc3.png)</span></span> </br>
</br>
7. <span data-ttu-id="2d134-163">啟用網域設定檔和標準設定檔的下列設定</span><span class="sxs-lookup"><span data-stu-id="2d134-163">Enable the following settings for Domain Profile and  Standard Profile</span></span> </br>
<span data-ttu-id="2d134-164">a)  連按兩下「Windows 防火牆：允許輸入檔案及印表機共用例外狀況」。</span><span class="sxs-lookup"><span data-stu-id="2d134-164">a)  Double-click on exception “Windows Firewall: Allow inbound file and printer sharing exception”.</span></span> <span data-ttu-id="2d134-165">選取 [已啟用] 並按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2d134-165">Select Enabled and click OK.</span></span> </br>
<span data-ttu-id="2d134-166">b)  連按兩下「Windows 防火牆：允許輸入遠端系統管理例外狀況」。</span><span class="sxs-lookup"><span data-stu-id="2d134-166">b)  Double click on exception “Windows Firewall: Allow inbound remote administration exception”.</span></span> <span data-ttu-id="2d134-167">選取 [已啟用] 並按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2d134-167">Select Enabled and click OK.</span></span> </br><span data-ttu-id="2d134-168">
![gpmc4](./media/site-recovery-protection-common-errors/gpmc4.png)</span><span class="sxs-lookup"><span data-stu-id="2d134-168">
![gpmc4](./media/site-recovery-protection-common-errors/gpmc4.png)</span></span> </br>
</br>

###### <a name="if-source-machine-is-not-domain-joined-and-part-of-workgroup-br"></a><span data-ttu-id="2d134-169">如果來源電腦未加入網域並屬於工作群組的一部分</span><span class="sxs-lookup"><span data-stu-id="2d134-169">If Source machine is not domain joined and part of workgroup</span></span> </br>
<span data-ttu-id="2d134-170">在遠端電腦上設定防火牆設定 (適用於工作群組)：</span><span class="sxs-lookup"><span data-stu-id="2d134-170">Configure firewall settings on remote machine (for workgroup):</span></span>
1. <span data-ttu-id="2d134-171">請移至來源電腦上，</span><span class="sxs-lookup"><span data-stu-id="2d134-171">Go to the source machine,</span></span></br>
2. <span data-ttu-id="2d134-172">在 Windows 防火牆設定之下 > [允許應用程式或功能通過防火牆] > 為所有設定檔選取 [檔案及印表機共用]。</span><span class="sxs-lookup"><span data-stu-id="2d134-172">Under Windows Firewall settings > “Allow an app or feature through Firewall” > select “File and Printer Sharing for all profiles”.</span></span> </br>
3. <span data-ttu-id="2d134-173">在 Windows 防火牆設定之下 > [允許應用程式或功能通過防火牆] > [為所有設定檔選取 WMI]。</span><span class="sxs-lookup"><span data-stu-id="2d134-173">Under Windows Firewall settings > “Allow an app or feature through Firewall” > “select WMI for all profiles”.</span></span> </br>

#### <a name="disable-remote-user-account-control-uac"></a><span data-ttu-id="2d134-174">停用遠端使用者帳戶控制 (UAC)</span><span class="sxs-lookup"><span data-stu-id="2d134-174">Disable remote User Account Control (UAC)</span></span>
<span data-ttu-id="2d134-175">使用登錄機碼來停用 UAC 以推送行動服務。</span><span class="sxs-lookup"><span data-stu-id="2d134-175">Disable UAC using registry key to push the mobility service.</span></span>
1. <span data-ttu-id="2d134-176">按一下 [開始] > [執行] > 鍵入 regedit > ENTER</span><span class="sxs-lookup"><span data-stu-id="2d134-176">Click Start > Run > type regedit > ENTER</span></span>
2. <span data-ttu-id="2d134-177">尋找而後按一下下列登錄子機碼：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System</span><span class="sxs-lookup"><span data-stu-id="2d134-177">Locate and then click the following registry subkey: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System</span></span>
3. <span data-ttu-id="2d134-178">如果 LocalAccountTokenFilterPolicy 登錄項目不存在，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2d134-178">If the LocalAccountTokenFilterPolicy registry entry does not exist, follow these steps:</span></span>
4. <span data-ttu-id="2d134-179">在 [編輯] 功能表上 > [新增] > 按一下 [DWORD 值]。</span><span class="sxs-lookup"><span data-stu-id="2d134-179">On the Edit menu > New > click DWORD Value.</span></span>
5. <span data-ttu-id="2d134-180">鍵入 LocalAccountTokenFilterPolicy，然後按 ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="2d134-180">Type LocalAccountTokenFilterPolicy and then press ENTER.</span></span>
6. <span data-ttu-id="2d134-181">在 LocalAccountTokenFilterPolicy 上按一下滑鼠右鍵，然後按一下 [修改]。</span><span class="sxs-lookup"><span data-stu-id="2d134-181">Right-click LocalAccountTokenFilterPolicy and then click Modify.</span></span>
7. <span data-ttu-id="2d134-182">在 [值] 資料方塊中鍵入 1，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2d134-182">In the Value data box, type 1, and then click OK.</span></span>
8. <span data-ttu-id="2d134-183">結束 [登錄編輯器]。</span><span class="sxs-lookup"><span data-stu-id="2d134-183">Exit Registry Editor.</span></span>


## <a name="push-install-pre-requisites-for-linux"></a><span data-ttu-id="2d134-184">適用於 Linux 的推送安裝必要元件：</span><span class="sxs-lookup"><span data-stu-id="2d134-184">Push Install pre-requisites for Linux:</span></span>

1. <span data-ttu-id="2d134-185">在來源 Linux 伺服器上建立 root 使用者。</span><span class="sxs-lookup"><span data-stu-id="2d134-185">Create a root user on the source Linux server.</span></span> <span data-ttu-id="2d134-186">(此帳戶僅適用於推送安裝和更新)</span><span class="sxs-lookup"><span data-stu-id="2d134-186">(Use this account only for the push installation and updates)</span></span></br>
2. <span data-ttu-id="2d134-187">檢查來源 Linux 伺服器上的 /etc/hosts 檔案，該檔案具有將本機主機名稱對應到所有網路介面卡相關聯之 IP 位址的項目。</span><span class="sxs-lookup"><span data-stu-id="2d134-187">Check that the /etc/hosts file on the source Linux server has entries that map the local hostname to IP addresses associated with all network adapters.</span></span> </br>
3. <span data-ttu-id="2d134-188">確定來源 Linux 伺服器上已安裝最新的 openssh、openssh-server 和 openssl 套件。</span><span class="sxs-lookup"><span data-stu-id="2d134-188">Make sure the latest openssh, openssh-server, and openssl packages are installed on source Linux server.</span></span> </br>
<span data-ttu-id="2d134-189">檢查 ssh 連接埠 22 已啟用並在執行中。</span><span class="sxs-lookup"><span data-stu-id="2d134-189">Check if ssh port 22 is enabled and running.</span></span> </br>
4. <span data-ttu-id="2d134-190">檢查代理程式的過時項目是否已存在於來源伺服器上，將舊版的代理程式解除安裝，並重新啟動伺服器、重新安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="2d134-190">Check if stale entries of agents are already present on the source server, uninstall the older agents and reboot the server, reinstall agent.</span></span> </br>

#### <a name="enable-sftp-subsystem-and-password-authentication-in-the-sshdconfig-file"></a><span data-ttu-id="2d134-191">在 sshd_config 檔案中啟用 SFTP 子系統與密碼驗證</span><span class="sxs-lookup"><span data-stu-id="2d134-191">Enable SFTP subsystem and password authentication in the sshd_config file</span></span>
1. <span data-ttu-id="2d134-192">在來源伺服器上，以 root 的身分登入。</span><span class="sxs-lookup"><span data-stu-id="2d134-192">On source server, sign in as root.</span></span> </br>
2. <span data-ttu-id="2d134-193">在 /etc/ssh/sshd_config 檔案中，</span><span class="sxs-lookup"><span data-stu-id="2d134-193">In the file /etc/ssh/sshd_config file,</span></span></br> <span data-ttu-id="2d134-194">尋找以 PasswordAuthentication 開頭的行。</span><span class="sxs-lookup"><span data-stu-id="2d134-194">find the line that begins with PasswordAuthentication.</span></span> </br>
3. <span data-ttu-id="2d134-195">d.</span><span class="sxs-lookup"><span data-stu-id="2d134-195">d.</span></span>   <span data-ttu-id="2d134-196">取消該行的註解並將值從 “no” 變更為 “yes”。</span><span class="sxs-lookup"><span data-stu-id="2d134-196">Uncomment the line and change the value from “no” to “yes”.</span></span> </br><span data-ttu-id="2d134-197">
![Linux1](./media/site-recovery-protection-common-errors/linux1.png)</span><span class="sxs-lookup"><span data-stu-id="2d134-197">
![Linux1](./media/site-recovery-protection-common-errors/linux1.png)</span></span>
4. <span data-ttu-id="2d134-198">尋找以 “Subsystem” 為開頭的行並取消其註解。</span><span class="sxs-lookup"><span data-stu-id="2d134-198">Find the line that begins with “Subsystem” and uncomment the line.</span></span> </br><span data-ttu-id="2d134-199">
![Linux2](./media/site-recovery-protection-common-errors/linux2.png)</span><span class="sxs-lookup"><span data-stu-id="2d134-199">
![Linux2](./media/site-recovery-protection-common-errors/linux2.png)</span></span>
5. <span data-ttu-id="2d134-200">儲存變更並重新啟動 sshd 服務。</span><span class="sxs-lookup"><span data-stu-id="2d134-200">Save the changes and restart the sshd service.</span></span> </br>

## <a name="push-installation-checks-on-configurationprocess-server"></a><span data-ttu-id="2d134-201">在組態/處理序伺服器上檢查推送安裝。</span><span class="sxs-lookup"><span data-stu-id="2d134-201">Push Installation checks on Configuration/Process server.</span></span>
#### <a name="validate-credentials-for-discovery-and-installation"></a><span data-ttu-id="2d134-202">驗證認證以供探索和安裝</span><span class="sxs-lookup"><span data-stu-id="2d134-202">Validate credentials for discovery and installation</span></span>

1. <span data-ttu-id="2d134-203">從組態伺服器啟動 Cspsconfigtool</span><span class="sxs-lookup"><span data-stu-id="2d134-203">From Configuration Server, launch Cspsconfigtool</span></span></br><span data-ttu-id="2d134-204">
![WMItestConnect5](./media/site-recovery-protection-common-errors/wmitestconnect5.png)</span><span class="sxs-lookup"><span data-stu-id="2d134-204">
![WMItestConnect5](./media/site-recovery-protection-common-errors/wmitestconnect5.png)</span></span> </br>

2. <span data-ttu-id="2d134-205">確定用於保護的帳戶具有來源電腦的系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="2d134-205">Make sure that the account used for protection has administrator rights on the source machine.</span></span> </br>

#### <a name="check-connectivity-between-process-server-and-source-server"></a><span data-ttu-id="2d134-206">檢查處理序伺服器與來源伺服器之間的連線能力</span><span class="sxs-lookup"><span data-stu-id="2d134-206">Check connectivity between process server and source server</span></span>
1. <span data-ttu-id="2d134-207">確定處理序伺服器有網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="2d134-207">Ensure Process Server has internet connection.</span></span>
2. <span data-ttu-id="2d134-208">使用 wbemtest.exe 驗證 WMI 連線。</span><span class="sxs-lookup"><span data-stu-id="2d134-208">Verify WMI connection using wbemtest.exe.</span></span> </br>
<span data-ttu-id="2d134-209">在處理序伺服器上，按一下 [開始] > [執行] > wbemtest.exe > [Windows Management Instrumentation 測試器] 視窗將會開啟 (如下所示)。</span><span class="sxs-lookup"><span data-stu-id="2d134-209">On the Process server, Click Start > Run > wbemtest.exe > Windows Management Instrumentation Tester window will be opened as shown.</span></span></br><span data-ttu-id="2d134-210">
   ![WMItestConnect1](./media/site-recovery-protection-common-errors/wmitestconnect1.png)</span><span class="sxs-lookup"><span data-stu-id="2d134-210">
   ![WMItestConnect1](./media/site-recovery-protection-common-errors/wmitestconnect1.png)</span></span> </br>
</br>
<span data-ttu-id="2d134-211">按一下 [連線] > 在 [命名空間輸入使用者名稱和密碼] 中輸入來源伺服器 IP (如果來源電腦已加入網域，請以 "domainName\username" 形式提供網域名稱及使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="2d134-211">Click on Connect > Enter the source server IP in the Namespace Input User name and Password (If source machine is domain joined, provide the domain name along with user name as “domainName\username”.</span></span> <span data-ttu-id="2d134-212">如果來源電腦在工作群組中，僅提供使用者名稱。)將 [驗證層級] 選取為 [封包私密性]。</span><span class="sxs-lookup"><span data-stu-id="2d134-212">If source machine is in workgroup, provide only the user name.) Select the Authentication level as Packet privacy.</span></span> </br><span data-ttu-id="2d134-213">
   ![WMItestConnect2](./media/site-recovery-protection-common-errors/wmitestconnect2.png)</span><span class="sxs-lookup"><span data-stu-id="2d134-213">
   ![WMItestConnect2](./media/site-recovery-protection-common-errors/wmitestconnect2.png)</span></span> </br>
   </br>
<span data-ttu-id="2d134-214">按一下 [連線]。</span><span class="sxs-lookup"><span data-stu-id="2d134-214">Click on Connect.</span></span> <span data-ttu-id="2d134-215">使用所提供資料進行的 WMI 連線現在應會成功，而 [Windows Management Instrumentation 測試器] 視窗應如下所示：</span><span class="sxs-lookup"><span data-stu-id="2d134-215">Now the WMI connection should be successful with the provided data and the Windows Management Instrumentation Tester window should be displayed as shown below:</span></span> </br><span data-ttu-id="2d134-216">
   ![WMItestConnect3](./media/site-recovery-protection-common-errors/wmitestconnect3.png)</span><span class="sxs-lookup"><span data-stu-id="2d134-216">
   ![WMItestConnect3](./media/site-recovery-protection-common-errors/wmitestconnect3.png)</span></span> </br>
</br>
   <span data-ttu-id="2d134-217">如果 WMI 連線不成功，將有出現錯誤訊息快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="2d134-217">If WMI connection is not successful there will be an error message pop-up.</span></span> <span data-ttu-id="2d134-218">如果未在 Windows 防火牆允許的應用程式中啟用 [WMI/遠端系統管理]，則下列螢幕擷取畫面會顯示失敗的嘗試。</span><span class="sxs-lookup"><span data-stu-id="2d134-218">The below screenshot shows an unsuccessful attempt if WMI/Remote Administration is not enabled in Windows firewall allowed app.</span></span> </br><span data-ttu-id="2d134-219">
   ![WMItestConnect4](./media/site-recovery-protection-common-errors/wmitestconnect4.png)</span><span class="sxs-lookup"><span data-stu-id="2d134-219">
![WMItestConnect4](./media/site-recovery-protection-common-errors/wmitestconnect4.png)</span></span> </br>
</br>

3. <span data-ttu-id="2d134-220">檢查 WMI 狀態和連線能力。</span><span class="sxs-lookup"><span data-stu-id="2d134-220">Check for the WMI status and connectivity.</span></span></br>
<span data-ttu-id="2d134-221">在組態/處理序伺服器上，</span><span class="sxs-lookup"><span data-stu-id="2d134-221">On the configuration/Process server,</span></span> </br>
<span data-ttu-id="2d134-222">按一下 [開始] > [執行] > wmimgmt.msc > [動作] > [其他動作] > 連線到另一部電腦 (來源電腦)。</span><span class="sxs-lookup"><span data-stu-id="2d134-222">Click start > run > wmimgmt.msc > Actions > More Actions > connect to another computer (source machine).</span></span> </br>
<span data-ttu-id="2d134-223">輸入用於防護之帳戶的認證，並檢查連線是否正常。</span><span class="sxs-lookup"><span data-stu-id="2d134-223">Input the credentials of the account used for protection and check if connectivity is fine.</span></span> </br>

#### <a name="verify-network-shared-folders-of-source-machine-is-accessible-from-process-server-ps-remotely-using-specified-credentials"></a><span data-ttu-id="2d134-224">確認可使用指定的認證從處理序伺服器 (PS) 遠端存取來源電腦的網路共用資料夾。</span><span class="sxs-lookup"><span data-stu-id="2d134-224">Verify network shared folders of source machine is accessible from Process Server (PS) remotely using specified credentials.</span></span>
  1. <span data-ttu-id="2d134-225">登入處理序伺服器 (PS) 電腦，開啟 [檔案總管] > 在位址列類型中 > "\\\source-machine-ip\C$" > 按一下 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="2d134-225">Logon to Process Server (PS) machine, Open File Explorer > In the address bar type > "\\\source-machine-ip\C$" > click Enter.</span></span> </br><span data-ttu-id="2d134-226">
  ![Fileshare1](./media/site-recovery-protection-common-errors/fileshare1.png)</span><span class="sxs-lookup"><span data-stu-id="2d134-226">
![Fileshare1](./media/site-recovery-protection-common-errors/fileshare1.png)</span></span> </br>
  2. <span data-ttu-id="2d134-227">檔案總管會提示輸入認證。</span><span class="sxs-lookup"><span data-stu-id="2d134-227">File explorer will prompt for credentials.</span></span> <span data-ttu-id="2d134-228">輸入使用者名稱和密碼，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2d134-228">Enter the username and password > click OK.</span></span></br>
   <span data-ttu-id="2d134-229">如果來源電腦已加入網域，請以 "domainName\username" 形式提供網域名稱及使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="2d134-229">If source machine is domain joined, provide the domain name along with user name as "domainName\username".</span></span></br>
   <span data-ttu-id="2d134-230">如果來源電腦在工作群組中，僅提供使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="2d134-230">If source machine is in workgroup, provide only the "username".</span></span> </br><span data-ttu-id="2d134-231">
  ![Fileshare2](./media/site-recovery-protection-common-errors/fileshare2.png)</span><span class="sxs-lookup"><span data-stu-id="2d134-231">
![Fileshare2](./media/site-recovery-protection-common-errors/fileshare2.png)</span></span> </br>
  3. <span data-ttu-id="2d134-232">如果連線成功，您可以從處理序伺服器 (PS) 遠端檢視來源電腦的資料夾</span><span class="sxs-lookup"><span data-stu-id="2d134-232">If connection is successful, you can view the folders of source machine remotely from Process Server (PS)</span></span> </br><span data-ttu-id="2d134-233">
  ![Fileshare3](./media/site-recovery-protection-common-errors/fileshare3.png)</span><span class="sxs-lookup"><span data-stu-id="2d134-233">
![Fileshare3](./media/site-recovery-protection-common-errors/fileshare3.png)</span></span> </br>

> [!NOTE] 
> <span data-ttu-id="2d134-234">如果連線不成功，請檢查是否符合所有必要條件。</span><span class="sxs-lookup"><span data-stu-id="2d134-234">If connection is unsuccessful, please check whether all pre-requisites are met.</span></span>
>

<span data-ttu-id="2d134-235">如果您不想開啟 "Windows Management Instrumentation"，您也可以在來源電腦上手動安裝行動服務。</span><span class="sxs-lookup"><span data-stu-id="2d134-235">If you don’t want to open “Windows Management Instrumentation”, you can also install mobility service manually on the source machine.</span></span></br> [<span data-ttu-id="2d134-236">透過 GUI 手動安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="2d134-236">Install Mobility Service manually through GUI</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) </br><span data-ttu-id="2d134-237">
[透過組態管理員指引進行安裝](site-recovery-install-mobility-service-using-sccm.md)</span><span class="sxs-lookup"><span data-stu-id="2d134-237">
[Installation through configuration manager guidance](site-recovery-install-mobility-service-using-sccm.md)</span></span> </br>

## <a name="next-steps"></a><span data-ttu-id="2d134-238">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2d134-238">Next steps</span></span>
- [<span data-ttu-id="2d134-239">啟用 VMware 虛擬機器的複寫</span><span class="sxs-lookup"><span data-stu-id="2d134-239">Enable replication for VMware virtual machines</span></span>](vmware-walkthrough-enable-replication.md)
