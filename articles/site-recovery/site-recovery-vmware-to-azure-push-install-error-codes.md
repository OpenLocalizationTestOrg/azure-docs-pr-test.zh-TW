---
title: "從 VMware tooAzure 疑難排解的 aaaAzure Site Recovery |Microsoft 文件"
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
ms.openlocfilehash: 912097c8892540dd798ba025e0b10374ca51d664
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-mobility-service-push-install-issues"></a><span data-ttu-id="36d6b-103">針對行動服務推送安裝問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="36d6b-103">Troubleshooting Mobility Service push install issues</span></span>

<span data-ttu-id="36d6b-104">這篇文章說明 hello 嘗試啟用保護的 toosource 伺服器上的 tooinstall hello 行動服務時所面臨的常見問題。</span><span class="sxs-lookup"><span data-stu-id="36d6b-104">This article details hello common issues faced when trying tooinstall hello Mobility Service on toosource server for enabling protection.</span></span>

## <a name="error-code-95107-protection-could-not-be-enabled"></a><span data-ttu-id="36d6b-105">(錯誤碼 95107) 無法啟用保護。</span><span class="sxs-lookup"><span data-stu-id="36d6b-105">(Error code 95107) Protection could not be enabled.</span></span>
<span data-ttu-id="36d6b-106">**錯誤碼**</span><span class="sxs-lookup"><span data-stu-id="36d6b-106">**Error code**</span></span> | <span data-ttu-id="36d6b-107">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="36d6b-107">**Possible causes**</span></span> | <span data-ttu-id="36d6b-108">**特定錯誤的建議**</span><span class="sxs-lookup"><span data-stu-id="36d6b-108">**Error-specific Recommendations**</span></span>
--- | --- | ---
<span data-ttu-id="36d6b-109">95107</span><span class="sxs-lookup"><span data-stu-id="36d6b-109">95107</span></span> </br><span data-ttu-id="36d6b-110">***訊息-***推入安裝的 hello 行動服務 toohello 來源電腦失敗，錯誤碼***EP0858***。</span><span class="sxs-lookup"><span data-stu-id="36d6b-110">***Message -***  Push installation of hello mobility service toohello source machine failed with error code ***EP0858***.</span></span> <br> <span data-ttu-id="36d6b-111">Hello 認證提供 tooinstall 行動服務不正確或是 hello 使用者帳戶具有足夠的權限</span><span class="sxs-lookup"><span data-stu-id="36d6b-111">Either that hello credentials provided tooinstall mobility service is incorrect or hello user account has insufficient privileges</span></span> | <span data-ttu-id="36d6b-112">提供使用者認證不正確的來源電腦上的 tooinstall 行動服務</span><span class="sxs-lookup"><span data-stu-id="36d6b-112">User credentials provided tooinstall mobility service on source machine is incorrect</span></span> | <span data-ttu-id="36d6b-113">請確定 hello hello 來源機器組態伺服器上提供的使用者認證正確無誤。</span><span class="sxs-lookup"><span data-stu-id="36d6b-113">Ensure hello user credentials provided for hello source machine on configuration server are correct.</span></span> <br> <span data-ttu-id="36d6b-114">tooadd/編輯使用者認證： 移 tooconfiguration 伺服器 > Cspsconfigtool 圖示 > 管理帳戶。</span><span class="sxs-lookup"><span data-stu-id="36d6b-114">tooadd/edit user credentials: go tooconfiguration server > Cspsconfigtool icon > Manage account.</span></span> </br> <span data-ttu-id="36d6b-115">此外，請確認下列必要條件是已核取的 toosuccessfully 完成推入安裝。</span><span class="sxs-lookup"><span data-stu-id="36d6b-115">In addition, ensure below pre-requisites are checked toosuccessfully complete push install.</span></span>

## <a name="error-code-95015-protection-could-not-be-enabled"></a><span data-ttu-id="36d6b-116">(錯誤碼 95015) 無法啟用保護。</span><span class="sxs-lookup"><span data-stu-id="36d6b-116">(Error code 95015) Protection could not be enabled.</span></span>
<span data-ttu-id="36d6b-117">**錯誤碼**</span><span class="sxs-lookup"><span data-stu-id="36d6b-117">**Error code**</span></span> | <span data-ttu-id="36d6b-118">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="36d6b-118">**Possible causes**</span></span> | <span data-ttu-id="36d6b-119">**特定錯誤的建議**</span><span class="sxs-lookup"><span data-stu-id="36d6b-119">**Error-specific Recommendations**</span></span>
--- | --- | ---
<span data-ttu-id="36d6b-120">95105</span><span class="sxs-lookup"><span data-stu-id="36d6b-120">95105</span></span> </br><span data-ttu-id="36d6b-121">***訊息-***推入安裝的 hello 行動服務 toohello 來源電腦失敗，錯誤碼***EP0856***。</span><span class="sxs-lookup"><span data-stu-id="36d6b-121">***Message -***  Push installation of hello mobility service toohello source machine failed with error code ***EP0856***.</span></span> <br> <span data-ttu-id="36d6b-122">可能是 「 檔案及印表機共用 」 不允許在 hello 來源電腦上，或有 hello 處理序伺服器與 hello 來源電腦之間的網路連線問題</span><span class="sxs-lookup"><span data-stu-id="36d6b-122">Either “File and Printer Sharing” not allowed on hello source machine, or there are network connectivity issues between hello process server and hello source machine</span></span>| <span data-ttu-id="36d6b-123">未啟用檔案及印表機共用</span><span class="sxs-lookup"><span data-stu-id="36d6b-123">File and print sharing is not enabled</span></span> | <span data-ttu-id="36d6b-124">允許在 hello Windows 防火牆，移至 toohello 來源機器中使用 「 檔案及印表機共用 」 hello 來源電腦上 > 在 Windows 防火牆設定 > 允許的應用程式或功能通過防火牆 > 選取 「 檔案及印表機共用所有設定檔 」。</span><span class="sxs-lookup"><span data-stu-id="36d6b-124">Allow “File and Printer Sharing” on hello source machine in hello Windows Firewall, Go toohello source machine > Under Windows Firewall settings > “Allow an app or feature through Firewall” > select “File and Printer Sharing for all profiles”.</span></span> </br> <span data-ttu-id="36d6b-125">此外，請確認下列必要條件是已核取的 toosuccessfully 完成推入安裝。</span><span class="sxs-lookup"><span data-stu-id="36d6b-125">In addition, ensure below pre-requisites are checked toosuccessfully complete push install.</span></span>

## <a name="error-code-95117-protection-could-not-be-enabled"></a><span data-ttu-id="36d6b-126">(錯誤碼 95117) 無法啟用保護。</span><span class="sxs-lookup"><span data-stu-id="36d6b-126">(Error code 95117) Protection could not be enabled.</span></span>
<span data-ttu-id="36d6b-127">**錯誤碼**</span><span class="sxs-lookup"><span data-stu-id="36d6b-127">**Error code**</span></span> | <span data-ttu-id="36d6b-128">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="36d6b-128">**Possible causes**</span></span> | <span data-ttu-id="36d6b-129">**特定錯誤的建議**</span><span class="sxs-lookup"><span data-stu-id="36d6b-129">**Error-specific Recommendations**</span></span>
--- | --- | ---
<span data-ttu-id="36d6b-130">95117</span><span class="sxs-lookup"><span data-stu-id="36d6b-130">95117</span></span> </br><span data-ttu-id="36d6b-131">***訊息-***推入安裝的 hello 行動服務 toohello 來源電腦失敗，錯誤碼***EP0865***。</span><span class="sxs-lookup"><span data-stu-id="36d6b-131">***Message -***  Push installation of hello mobility service toohello source machine failed with error code ***EP0865***.</span></span> <br> <span data-ttu-id="36d6b-132">Hello 來源機器未執行，或是沒有 hello 處理序伺服器與 hello 來源電腦之間的網路連線問題</span><span class="sxs-lookup"><span data-stu-id="36d6b-132">Either hello source machine is not running, or there are network connectivity issues between hello process server and hello source machine</span></span> | <span data-ttu-id="36d6b-133">處理序伺服器與來源伺服器之間的網路連線能力</span><span class="sxs-lookup"><span data-stu-id="36d6b-133">Network connectivity between process server and source server</span></span> | <span data-ttu-id="36d6b-134">檢查處理序伺服器與來源伺服器之間的連線能力。</span><span class="sxs-lookup"><span data-stu-id="36d6b-134">Check connectivity between process server and source server.</span></span> </br> <span data-ttu-id="36d6b-135">此外，請確認下列必要條件是已核取的 toosuccessfully 完成推入安裝。</span><span class="sxs-lookup"><span data-stu-id="36d6b-135">In addition, ensure below pre-requisites are checked toosuccessfully complete push install.</span></span>

## <a name="error-code-95103-protection-could-not-be-enabled"></a><span data-ttu-id="36d6b-136">(錯誤碼 95103) 無法啟用保護。</span><span class="sxs-lookup"><span data-stu-id="36d6b-136">(Error code 95103) Protection could not be enabled.</span></span>
<span data-ttu-id="36d6b-137">**錯誤碼**</span><span class="sxs-lookup"><span data-stu-id="36d6b-137">**Error code**</span></span> | <span data-ttu-id="36d6b-138">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="36d6b-138">**Possible causes**</span></span> | <span data-ttu-id="36d6b-139">**特定錯誤的建議**</span><span class="sxs-lookup"><span data-stu-id="36d6b-139">**Error-specific Recommendations**</span></span>
--- | --- | ---
<span data-ttu-id="36d6b-140">95103</span><span class="sxs-lookup"><span data-stu-id="36d6b-140">95103</span></span> </br><span data-ttu-id="36d6b-141">***訊息-***推入安裝的 hello 行動服務 toohello 來源電腦失敗，錯誤碼***EP0854***。</span><span class="sxs-lookup"><span data-stu-id="36d6b-141">***Message -***  Push installation of hello mobility service toohello source machine failed with error code ***EP0854***.</span></span> <br> <span data-ttu-id="36d6b-142">可能是"Windows Management Instrumentation (WMI) 」 不允許在 hello 來源電腦上，或有 hello 處理序伺服器與 hello 來源電腦之間的網路連線問題</span><span class="sxs-lookup"><span data-stu-id="36d6b-142">Either “Windows Management Instrumentation (WMI)”is not allowed on hello source machine, or there are network connectivity issues between hello process server and hello source machine</span></span>| <span data-ttu-id="36d6b-143">在 hello Windows 防火牆封鎖 Windows Management Instrumentation (WMI)</span><span class="sxs-lookup"><span data-stu-id="36d6b-143">Windows Management Instrumentation (WMI) blocked in hello Windows Firewall</span></span> | <span data-ttu-id="36d6b-144">允許 Windows Management Instrumentation (WMI) 中的 hello Windows 防火牆。</span><span class="sxs-lookup"><span data-stu-id="36d6b-144">Allow Windows Management Instrumentation (WMI) in hello Windows Firewall.</span></span> <span data-ttu-id="36d6b-145">在 Windows 防火牆設定之下 > [允許應用程式或功能通過防火牆] > [為所有設定檔選取 WMI]。</span><span class="sxs-lookup"><span data-stu-id="36d6b-145">Under Windows Firewall settings > “Allow an app or feature through Firewall” > “select WMI for all profiles”.</span></span> </br> <span data-ttu-id="36d6b-146">此外，請確認下列必要條件是已核取的 toosuccessfully 完成推入安裝。</span><span class="sxs-lookup"><span data-stu-id="36d6b-146">In addition, ensure below pre-requisites are checked toosuccessfully complete push install.</span></span>

## <a name="check-push-install-logs-for-errors"></a><span data-ttu-id="36d6b-147">檢查推送安裝記錄中的錯誤</span><span class="sxs-lookup"><span data-stu-id="36d6b-147">Check Push Install Logs for errors</span></span>

<span data-ttu-id="36d6b-148">Hello 設定/程序在伺服器上，瀏覽的 toofile 'PushinstallService' 位於<Microsoft Azure Site Recovery Install Location>\home\svsystems\pushinstallsvc\ toounderstand hello 來源 hello 問題和使用下列疑難排解步驟 tooresolve hello 問題。</span><span class="sxs-lookup"><span data-stu-id="36d6b-148">On hello Configuration/Process server, Navigate toofile 'PushinstallService' located at <Microsoft Azure Site Recovery Install Location>\home\svsystems\pushinstallsvc\ toounderstand hello source of hello problem and use below troubleshooting steps tooresolve hello issue.</span></span></br><span data-ttu-id="36d6b-149">
![pushiinstalllogs](./media/site-recovery-protection-common-errors/pushinstalllogs.png)</span><span class="sxs-lookup"><span data-stu-id="36d6b-149">
![pushiinstalllogs](./media/site-recovery-protection-common-errors/pushinstalllogs.png)</span></span>

## <a name="push-install-pre-requisites-for-windows"></a><span data-ttu-id="36d6b-150">適用於 Windows 的推送安裝必要元件</span><span class="sxs-lookup"><span data-stu-id="36d6b-150">Push Install pre-requisites for Windows</span></span>
### <a name="ensure-file-and-printer-sharing-is-enabled"></a><span data-ttu-id="36d6b-151">確保已啟用 [檔案及印表機共用]</span><span class="sxs-lookup"><span data-stu-id="36d6b-151">Ensure "File and Printer Sharing" is enabled</span></span>
<span data-ttu-id="36d6b-152">允許 hello Windows 防火牆中的 hello 來源電腦上的 「 檔案及印表機共用 」 及 「 Windows Management Instrumentation"</span><span class="sxs-lookup"><span data-stu-id="36d6b-152">Allow “File and Printer Sharing” and "Windows Management Instrumentation" on hello source machine in hello Windows Firewall</span></span> </br>
#### <a name="if-source-machine-is-domain-joined-br"></a><span data-ttu-id="36d6b-153">如果來源電腦已加入網域：</span><span class="sxs-lookup"><span data-stu-id="36d6b-153">If Source machine is Domain Joined:</span></span> </br>
<span data-ttu-id="36d6b-154">使用群組原則管理主控台 (GPMC) 來進行防火牆設定。</span><span class="sxs-lookup"><span data-stu-id="36d6b-154">Configure firewall settings using Group Policy Management Console (GPMC).</span></span>
1. <span data-ttu-id="36d6b-155">登入 tooActive 目錄網域電腦系統管理員身分，並開啟 群組原則管理主控台 (GPMC。MSC，從一開始執行 > 執行)。</span><span class="sxs-lookup"><span data-stu-id="36d6b-155">Login tooActive directory domain machine as administrator and open Group Policy Management Console (GPMC.MSC, run from a Start > Run).</span></span></br>
3. <span data-ttu-id="36d6b-156">如果未安裝 GPMC，請遵循 hello 連結太[安裝 hello GPMC](https://technet.microsoft.com/library/cc725932.aspx)</span><span class="sxs-lookup"><span data-stu-id="36d6b-156">If GPMC is not installed, follow hello link too[Install hello GPMC](https://technet.microsoft.com/library/cc725932.aspx)</span></span> </br>
4. <span data-ttu-id="36d6b-157">在 hello GPMC 主控台樹狀目錄中，按兩下 hello 樹系和網域群組原則物件，並瀏覽過 「 預設網域原則 」。</span><span class="sxs-lookup"><span data-stu-id="36d6b-157">In hello GPMC console tree, double-click Group Policy Objects in hello forest and domain and navigate too“Default Domain Policy”.</span></span> </br><span data-ttu-id="36d6b-158">
![gpmc1](./media/site-recovery-protection-common-errors/gpmc1.png)</span><span class="sxs-lookup"><span data-stu-id="36d6b-158">
![gpmc1](./media/site-recovery-protection-common-errors/gpmc1.png)</span></span> </br>
</br>
5. <span data-ttu-id="36d6b-159">以滑鼠右鍵按一下 [預設網域原則] > 編輯 > 將會開啟新的 [群組原則管理編輯器] 視窗。</span><span class="sxs-lookup"><span data-stu-id="36d6b-159">Right-click on “Default Domain Policy” > edit > A new “Group Policy Management Editor” window will be opened.</span></span> </br><span data-ttu-id="36d6b-160">
![gpmc2](./media/site-recovery-protection-common-errors/gpmc2.png)</span><span class="sxs-lookup"><span data-stu-id="36d6b-160">
![gpmc2](./media/site-recovery-protection-common-errors/gpmc2.png)</span></span> </br>
</br>
6. <span data-ttu-id="36d6b-161">在 [hello 群組原則管理編輯器] 瀏覽 tooComputer 組態 > 原則 > 系統管理範本 > 網路 > 網路連線 > Windows 防火牆。</span><span class="sxs-lookup"><span data-stu-id="36d6b-161">In hello Group Policy Management Editor navigate tooComputer Configuration > Policies > Administrative Templates > Network > Network Connections > Windows Firewall.</span></span> </br><span data-ttu-id="36d6b-162">
![gpmc3](./media/site-recovery-protection-common-errors/gpmc3.png)</span><span class="sxs-lookup"><span data-stu-id="36d6b-162">
![gpmc3](./media/site-recovery-protection-common-errors/gpmc3.png)</span></span> </br>
</br>
7. <span data-ttu-id="36d6b-163">啟用 hello 下列網域設定檔和標準設定檔設定</span><span class="sxs-lookup"><span data-stu-id="36d6b-163">Enable hello following settings for Domain Profile and  Standard Profile</span></span> </br>
<span data-ttu-id="36d6b-164">a)  連按兩下「Windows 防火牆：允許輸入檔案及印表機共用例外狀況」。</span><span class="sxs-lookup"><span data-stu-id="36d6b-164">a)  Double-click on exception “Windows Firewall: Allow inbound file and printer sharing exception”.</span></span> <span data-ttu-id="36d6b-165">選取 [已啟用] 並按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="36d6b-165">Select Enabled and click OK.</span></span> </br>
<span data-ttu-id="36d6b-166">b)  連按兩下「Windows 防火牆：允許輸入遠端系統管理例外狀況」。</span><span class="sxs-lookup"><span data-stu-id="36d6b-166">b)  Double click on exception “Windows Firewall: Allow inbound remote administration exception”.</span></span> <span data-ttu-id="36d6b-167">選取 [已啟用] 並按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="36d6b-167">Select Enabled and click OK.</span></span> </br><span data-ttu-id="36d6b-168">
![gpmc4](./media/site-recovery-protection-common-errors/gpmc4.png)</span><span class="sxs-lookup"><span data-stu-id="36d6b-168">
![gpmc4](./media/site-recovery-protection-common-errors/gpmc4.png)</span></span> </br>
</br>

###### <a name="if-source-machine-is-not-domain-joined-and-part-of-workgroup-br"></a><span data-ttu-id="36d6b-169">如果來源電腦未加入網域並屬於工作群組的一部分</span><span class="sxs-lookup"><span data-stu-id="36d6b-169">If Source machine is not domain joined and part of workgroup</span></span> </br>
<span data-ttu-id="36d6b-170">在遠端電腦上設定防火牆設定 (適用於工作群組)：</span><span class="sxs-lookup"><span data-stu-id="36d6b-170">Configure firewall settings on remote machine (for workgroup):</span></span>
1. <span data-ttu-id="36d6b-171">移 toohello 來源電腦上，</span><span class="sxs-lookup"><span data-stu-id="36d6b-171">Go toohello source machine,</span></span></br>
2. <span data-ttu-id="36d6b-172">在 Windows 防火牆設定之下 > [允許應用程式或功能通過防火牆] > 為所有設定檔選取 [檔案及印表機共用]。</span><span class="sxs-lookup"><span data-stu-id="36d6b-172">Under Windows Firewall settings > “Allow an app or feature through Firewall” > select “File and Printer Sharing for all profiles”.</span></span> </br>
3. <span data-ttu-id="36d6b-173">在 Windows 防火牆設定之下 > [允許應用程式或功能通過防火牆] > [為所有設定檔選取 WMI]。</span><span class="sxs-lookup"><span data-stu-id="36d6b-173">Under Windows Firewall settings > “Allow an app or feature through Firewall” > “select WMI for all profiles”.</span></span> </br>

#### <a name="disable-remote-user-account-control-uac"></a><span data-ttu-id="36d6b-174">停用遠端使用者帳戶控制 (UAC)</span><span class="sxs-lookup"><span data-stu-id="36d6b-174">Disable remote User Account Control (UAC)</span></span>
<span data-ttu-id="36d6b-175">停用 UAC 使用登錄金鑰 toopush hello 行動服務。</span><span class="sxs-lookup"><span data-stu-id="36d6b-175">Disable UAC using registry key toopush hello mobility service.</span></span>
1. <span data-ttu-id="36d6b-176">按一下 [開始] > [執行] > 鍵入 regedit > ENTER</span><span class="sxs-lookup"><span data-stu-id="36d6b-176">Click Start > Run > type regedit > ENTER</span></span>
2. <span data-ttu-id="36d6b-177">尋找並按一下下列登錄子機碼的 hello: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System</span><span class="sxs-lookup"><span data-stu-id="36d6b-177">Locate and then click hello following registry subkey: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System</span></span>
3. <span data-ttu-id="36d6b-178">如果 hello LocalAccountTokenFilterPolicy 登錄項目不存在，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="36d6b-178">If hello LocalAccountTokenFilterPolicy registry entry does not exist, follow these steps:</span></span>
4. <span data-ttu-id="36d6b-179">Hello 編輯 功能表上 > 新增 > 按一下 DWORD 值。</span><span class="sxs-lookup"><span data-stu-id="36d6b-179">On hello Edit menu > New > click DWORD Value.</span></span>
5. <span data-ttu-id="36d6b-180">鍵入 LocalAccountTokenFilterPolicy，然後按 ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="36d6b-180">Type LocalAccountTokenFilterPolicy and then press ENTER.</span></span>
6. <span data-ttu-id="36d6b-181">在 LocalAccountTokenFilterPolicy 上按一下滑鼠右鍵，然後按一下修改。</span><span class="sxs-lookup"><span data-stu-id="36d6b-181">Right-click LocalAccountTokenFilterPolicy and then click Modify.</span></span>
7. <span data-ttu-id="36d6b-182">在 hello 值資料 方塊中輸入 1，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="36d6b-182">In hello Value data box, type 1, and then click OK.</span></span>
8. <span data-ttu-id="36d6b-183">結束 [登錄編輯器]。</span><span class="sxs-lookup"><span data-stu-id="36d6b-183">Exit Registry Editor.</span></span>


## <a name="push-install-pre-requisites-for-linux"></a><span data-ttu-id="36d6b-184">適用於 Linux 的推送安裝必要元件：</span><span class="sxs-lookup"><span data-stu-id="36d6b-184">Push Install pre-requisites for Linux:</span></span>

1. <span data-ttu-id="36d6b-185">建立 hello 來源 Linux 伺服器上的根使用者。</span><span class="sxs-lookup"><span data-stu-id="36d6b-185">Create a root user on hello source Linux server.</span></span> <span data-ttu-id="36d6b-186">（使用此帳戶僅適用於 hello 推入安裝和更新）</span><span class="sxs-lookup"><span data-stu-id="36d6b-186">(Use this account only for hello push installation and updates)</span></span></br>
2. <span data-ttu-id="36d6b-187">請檢查該 hello 來源伺服器具有與所有網路介面卡相關聯的 hello 本機主機名稱 tooIP 位址對應的項目 Linux 上的 hello /etc/hosts 檔案。</span><span class="sxs-lookup"><span data-stu-id="36d6b-187">Check that hello /etc/hosts file on hello source Linux server has entries that map hello local hostname tooIP addresses associated with all network adapters.</span></span> </br>
3. <span data-ttu-id="36d6b-188">請確定來源 Linux 伺服器上所安裝的 hello 最新的 openssh、 openssh 伺服器和 openssl 封裝。</span><span class="sxs-lookup"><span data-stu-id="36d6b-188">Make sure hello latest openssh, openssh-server, and openssl packages are installed on source Linux server.</span></span> </br>
<span data-ttu-id="36d6b-189">檢查 ssh 連接埠 22 已啟用並在執行中。</span><span class="sxs-lookup"><span data-stu-id="36d6b-189">Check if ssh port 22 is enabled and running.</span></span> </br>
4. <span data-ttu-id="36d6b-190">檢查是否代理程式的過時的項目已經存在於 hello 來源伺服器上，解除安裝 hello 較舊的代理程式和伺服器 hello 重新開機，重新安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="36d6b-190">Check if stale entries of agents are already present on hello source server, uninstall hello older agents and reboot hello server, reinstall agent.</span></span> </br>

#### <a name="enable-sftp-subsystem-and-password-authentication-in-hello-sshdconfig-file"></a><span data-ttu-id="36d6b-191">啟用 hello sshd_config 檔案中的 SFTP 子系統和密碼驗證</span><span class="sxs-lookup"><span data-stu-id="36d6b-191">Enable SFTP subsystem and password authentication in hello sshd_config file</span></span>
1. <span data-ttu-id="36d6b-192">在來源伺服器上，以 root 的身分登入。</span><span class="sxs-lookup"><span data-stu-id="36d6b-192">On source server, sign in as root.</span></span> </br>
2. <span data-ttu-id="36d6b-193">在 hello /etc/ssh/sshd_config 檔案，</span><span class="sxs-lookup"><span data-stu-id="36d6b-193">In hello file /etc/ssh/sshd_config file,</span></span></br> <span data-ttu-id="36d6b-194">尋找開頭為 PasswordAuthentication hello 一行。</span><span class="sxs-lookup"><span data-stu-id="36d6b-194">find hello line that begins with PasswordAuthentication.</span></span> </br>
3. <span data-ttu-id="36d6b-195">d.</span><span class="sxs-lookup"><span data-stu-id="36d6b-195">d.</span></span>   <span data-ttu-id="36d6b-196">Hello 行取消註解再變更 hello 值從 「 否 」 太"yes"。</span><span class="sxs-lookup"><span data-stu-id="36d6b-196">Uncomment hello line and change hello value from “no” too“yes”.</span></span> </br><span data-ttu-id="36d6b-197">
![Linux1](./media/site-recovery-protection-common-errors/linux1.png)</span><span class="sxs-lookup"><span data-stu-id="36d6b-197">
![Linux1](./media/site-recovery-protection-common-errors/linux1.png)</span></span>
4. <span data-ttu-id="36d6b-198">尋找開頭為"Subsystem"hello 一行和 hello 行取消註解。</span><span class="sxs-lookup"><span data-stu-id="36d6b-198">Find hello line that begins with “Subsystem” and uncomment hello line.</span></span> </br><span data-ttu-id="36d6b-199">
![Linux2](./media/site-recovery-protection-common-errors/linux2.png)</span><span class="sxs-lookup"><span data-stu-id="36d6b-199">
![Linux2](./media/site-recovery-protection-common-errors/linux2.png)</span></span>
5. <span data-ttu-id="36d6b-200">儲存 hello 變更，並重新啟動 hello sshd 服務。</span><span class="sxs-lookup"><span data-stu-id="36d6b-200">Save hello changes and restart hello sshd service.</span></span> </br>

## <a name="push-installation-checks-on-configurationprocess-server"></a><span data-ttu-id="36d6b-201">在組態/處理序伺服器上檢查推送安裝。</span><span class="sxs-lookup"><span data-stu-id="36d6b-201">Push Installation checks on Configuration/Process server.</span></span>
#### <a name="validate-credentials-for-discovery-and-installation"></a><span data-ttu-id="36d6b-202">驗證認證以供探索和安裝</span><span class="sxs-lookup"><span data-stu-id="36d6b-202">Validate credentials for discovery and installation</span></span>

1. <span data-ttu-id="36d6b-203">從組態伺服器啟動 Cspsconfigtool</span><span class="sxs-lookup"><span data-stu-id="36d6b-203">From Configuration Server, launch Cspsconfigtool</span></span></br><span data-ttu-id="36d6b-204">
![WMItestConnect5](./media/site-recovery-protection-common-errors/wmitestconnect5.png)</span><span class="sxs-lookup"><span data-stu-id="36d6b-204">
![WMItestConnect5](./media/site-recovery-protection-common-errors/wmitestconnect5.png)</span></span> </br>

2. <span data-ttu-id="36d6b-205">請確定用於保護 hello 帳戶 hello 來源電腦上具有系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="36d6b-205">Make sure that hello account used for protection has administrator rights on hello source machine.</span></span> </br>

#### <a name="check-connectivity-between-process-server-and-source-server"></a><span data-ttu-id="36d6b-206">檢查處理序伺服器與來源伺服器之間的連線能力</span><span class="sxs-lookup"><span data-stu-id="36d6b-206">Check connectivity between process server and source server</span></span>
1. <span data-ttu-id="36d6b-207">確定處理序伺服器有網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="36d6b-207">Ensure Process Server has internet connection.</span></span>
2. <span data-ttu-id="36d6b-208">使用 wbemtest.exe 驗證 WMI 連線。</span><span class="sxs-lookup"><span data-stu-id="36d6b-208">Verify WMI connection using wbemtest.exe.</span></span> </br>
<span data-ttu-id="36d6b-209">Hello 程序在伺服器上，按一下 [開始 > 執行 > wbemtest.exe > 所示，將會開啟 Windows Management Instrumentation 測試器] 視窗。</span><span class="sxs-lookup"><span data-stu-id="36d6b-209">On hello Process server, Click Start > Run > wbemtest.exe > Windows Management Instrumentation Tester window will be opened as shown.</span></span></br><span data-ttu-id="36d6b-210">
   ![WMItestConnect1](./media/site-recovery-protection-common-errors/wmitestconnect1.png)</span><span class="sxs-lookup"><span data-stu-id="36d6b-210">
   ![WMItestConnect1](./media/site-recovery-protection-common-errors/wmitestconnect1.png)</span></span> </br>
</br>
<span data-ttu-id="36d6b-211">按一下 連線 > 輸入 hello 來源伺服器 IP hello 命名空間輸入使用者名稱和密碼 （如果來源機器已加入網域，提供 hello 網域名稱，以及為"domainName\username"的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="36d6b-211">Click on Connect > Enter hello source server IP in hello Namespace Input User name and Password (If source machine is domain joined, provide hello domain name along with user name as “domainName\username”.</span></span> <span data-ttu-id="36d6b-212">如果來源電腦是工作群組中，提供 hello 使用者名稱。）選取 hello 驗證層級做為封包私密性。</span><span class="sxs-lookup"><span data-stu-id="36d6b-212">If source machine is in workgroup, provide only hello user name.) Select hello Authentication level as Packet privacy.</span></span> </br><span data-ttu-id="36d6b-213">
   ![WMItestConnect2](./media/site-recovery-protection-common-errors/wmitestconnect2.png)</span><span class="sxs-lookup"><span data-stu-id="36d6b-213">
   ![WMItestConnect2](./media/site-recovery-protection-common-errors/wmitestconnect2.png)</span></span> </br>
   </br>
<span data-ttu-id="36d6b-214">按一下 [連線]。</span><span class="sxs-lookup"><span data-stu-id="36d6b-214">Click on Connect.</span></span> <span data-ttu-id="36d6b-215">現在以提供資料的 hello hello WMI 連接應該會成功，而且應該顯示 hello Windows Management Instrumentation 測試器 視窗，如下所示：</span><span class="sxs-lookup"><span data-stu-id="36d6b-215">Now hello WMI connection should be successful with hello provided data and hello Windows Management Instrumentation Tester window should be displayed as shown below:</span></span> </br><span data-ttu-id="36d6b-216">
   ![WMItestConnect3](./media/site-recovery-protection-common-errors/wmitestconnect3.png)</span><span class="sxs-lookup"><span data-stu-id="36d6b-216">
   ![WMItestConnect3](./media/site-recovery-protection-common-errors/wmitestconnect3.png)</span></span> </br>
</br>
   <span data-ttu-id="36d6b-217">如果 WMI 連線不成功，將有出現錯誤訊息快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="36d6b-217">If WMI connection is not successful there will be an error message pop-up.</span></span> <span data-ttu-id="36d6b-218">hello，下列螢幕擷取畫面顯示嘗試失敗允許應用程式的 Windows 防火牆中是否未啟用遠端 WMI/系統管理。</span><span class="sxs-lookup"><span data-stu-id="36d6b-218">hello below screenshot shows an unsuccessful attempt if WMI/Remote Administration is not enabled in Windows firewall allowed app.</span></span> </br><span data-ttu-id="36d6b-219">
   ![WMItestConnect4](./media/site-recovery-protection-common-errors/wmitestconnect4.png)</span><span class="sxs-lookup"><span data-stu-id="36d6b-219">
![WMItestConnect4](./media/site-recovery-protection-common-errors/wmitestconnect4.png)</span></span> </br>
</br>

3. <span data-ttu-id="36d6b-220">請檢查 hello WMI 狀態和連線。</span><span class="sxs-lookup"><span data-stu-id="36d6b-220">Check for hello WMI status and connectivity.</span></span></br>
<span data-ttu-id="36d6b-221">Hello 設定/程序在伺服器上，</span><span class="sxs-lookup"><span data-stu-id="36d6b-221">On hello configuration/Process server,</span></span> </br>
<span data-ttu-id="36d6b-222">按一下 [開始] > 執行 > wmimgmt.msc > 動作 > 其他動作 > tooanother 電腦 （來源電腦） 連線。</span><span class="sxs-lookup"><span data-stu-id="36d6b-222">Click start > run > wmimgmt.msc > Actions > More Actions > connect tooanother computer (source machine).</span></span> </br>
<span data-ttu-id="36d6b-223">輸入 hello hello 如果連線是正常的用於保護和核取的帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="36d6b-223">Input hello credentials of hello account used for protection and check if connectivity is fine.</span></span> </br>

#### <a name="verify-network-shared-folders-of-source-machine-is-accessible-from-process-server-ps-remotely-using-specified-credentials"></a><span data-ttu-id="36d6b-224">確認可使用指定的認證從處理序伺服器 (PS) 遠端存取來源電腦的網路共用資料夾。</span><span class="sxs-lookup"><span data-stu-id="36d6b-224">Verify network shared folders of source machine is accessible from Process Server (PS) remotely using specified credentials.</span></span>
  1. <span data-ttu-id="36d6b-225">登入 tooProcess 伺服器 (PS) 的電腦，開啟檔案總管 > hello 位址列型別中 >"\\\source-machine-ip\C$"> 按一下 enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="36d6b-225">Logon tooProcess Server (PS) machine, Open File Explorer > In hello address bar type > "\\\source-machine-ip\C$" > click Enter.</span></span> </br><span data-ttu-id="36d6b-226">
  ![Fileshare1](./media/site-recovery-protection-common-errors/fileshare1.png)</span><span class="sxs-lookup"><span data-stu-id="36d6b-226">
![Fileshare1](./media/site-recovery-protection-common-errors/fileshare1.png)</span></span> </br>
  2. <span data-ttu-id="36d6b-227">檔案總管會提示輸入認證。</span><span class="sxs-lookup"><span data-stu-id="36d6b-227">File explorer will prompt for credentials.</span></span> <span data-ttu-id="36d6b-228">輸入 hello 使用者名稱和密碼 > 按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="36d6b-228">Enter hello username and password > click OK.</span></span></br>
   <span data-ttu-id="36d6b-229">如果來源機器已加入網域，提供 hello 網域名稱，以及使用者名稱做為"domainName\username"。</span><span class="sxs-lookup"><span data-stu-id="36d6b-229">If source machine is domain joined, provide hello domain name along with user name as "domainName\username".</span></span></br>
   <span data-ttu-id="36d6b-230">如果來源電腦是工作群組中，提供僅 hello"username"。</span><span class="sxs-lookup"><span data-stu-id="36d6b-230">If source machine is in workgroup, provide only hello "username".</span></span> </br><span data-ttu-id="36d6b-231">
  ![Fileshare2](./media/site-recovery-protection-common-errors/fileshare2.png)</span><span class="sxs-lookup"><span data-stu-id="36d6b-231">
![Fileshare2](./media/site-recovery-protection-common-errors/fileshare2.png)</span></span> </br>
  3. <span data-ttu-id="36d6b-232">如果連線成功時，您可以檢視 hello 資料夾的來源電腦遠端從處理序伺服器 (PS)</span><span class="sxs-lookup"><span data-stu-id="36d6b-232">If connection is successful, you can view hello folders of source machine remotely from Process Server (PS)</span></span> </br><span data-ttu-id="36d6b-233">
  ![Fileshare3](./media/site-recovery-protection-common-errors/fileshare3.png)</span><span class="sxs-lookup"><span data-stu-id="36d6b-233">
![Fileshare3](./media/site-recovery-protection-common-errors/fileshare3.png)</span></span> </br>

> [!NOTE] 
> <span data-ttu-id="36d6b-234">如果連線不成功，請檢查是否符合所有必要條件。</span><span class="sxs-lookup"><span data-stu-id="36d6b-234">If connection is unsuccessful, please check whether all pre-requisites are met.</span></span>
>

<span data-ttu-id="36d6b-235">如果您不想 tooopen"Windows Management Instrumentation 」，您也可以安裝行動服務手動 hello 來源電腦上。</span><span class="sxs-lookup"><span data-stu-id="36d6b-235">If you don’t want tooopen “Windows Management Instrumentation”, you can also install mobility service manually on hello source machine.</span></span></br> [<span data-ttu-id="36d6b-236">透過 GUI 手動安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="36d6b-236">Install Mobility Service manually through GUI</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) </br><span data-ttu-id="36d6b-237">
[透過組態管理員指引進行安裝](site-recovery-install-mobility-service-using-sccm.md)</span><span class="sxs-lookup"><span data-stu-id="36d6b-237">
[Installation through configuration manager guidance](site-recovery-install-mobility-service-using-sccm.md)</span></span> </br>

## <a name="next-steps"></a><span data-ttu-id="36d6b-238">後續步驟</span><span class="sxs-lookup"><span data-stu-id="36d6b-238">Next steps</span></span>
- [<span data-ttu-id="36d6b-239">啟用 VMware 虛擬機器的複寫</span><span class="sxs-lookup"><span data-stu-id="36d6b-239">Enable replication for VMware virtual machines</span></span>](vmware-walkthrough-enable-replication.md)
