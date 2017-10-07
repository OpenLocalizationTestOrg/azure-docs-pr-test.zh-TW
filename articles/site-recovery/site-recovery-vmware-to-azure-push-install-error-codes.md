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
# <a name="troubleshooting-mobility-service-push-install-issues"></a>針對行動服務推送安裝問題進行疑難排解

這篇文章說明 hello 嘗試啟用保護的 toosource 伺服器上的 tooinstall hello 行動服務時所面臨的常見問題。

## <a name="error-code-95107-protection-could-not-be-enabled"></a>(錯誤碼 95107) 無法啟用保護。
**錯誤碼** | **可能的原因** | **特定錯誤的建議**
--- | --- | ---
95107 </br>***訊息-***推入安裝的 hello 行動服務 toohello 來源電腦失敗，錯誤碼***EP0858***。 <br> Hello 認證提供 tooinstall 行動服務不正確或是 hello 使用者帳戶具有足夠的權限 | 提供使用者認證不正確的來源電腦上的 tooinstall 行動服務 | 請確定 hello hello 來源機器組態伺服器上提供的使用者認證正確無誤。 <br> tooadd/編輯使用者認證： 移 tooconfiguration 伺服器 > Cspsconfigtool 圖示 > 管理帳戶。 </br> 此外，請確認下列必要條件是已核取的 toosuccessfully 完成推入安裝。

## <a name="error-code-95015-protection-could-not-be-enabled"></a>(錯誤碼 95015) 無法啟用保護。
**錯誤碼** | **可能的原因** | **特定錯誤的建議**
--- | --- | ---
95105 </br>***訊息-***推入安裝的 hello 行動服務 toohello 來源電腦失敗，錯誤碼***EP0856***。 <br> 可能是 「 檔案及印表機共用 」 不允許在 hello 來源電腦上，或有 hello 處理序伺服器與 hello 來源電腦之間的網路連線問題| 未啟用檔案及印表機共用 | 允許在 hello Windows 防火牆，移至 toohello 來源機器中使用 「 檔案及印表機共用 」 hello 來源電腦上 > 在 Windows 防火牆設定 > 允許的應用程式或功能通過防火牆 > 選取 「 檔案及印表機共用所有設定檔 」。 </br> 此外，請確認下列必要條件是已核取的 toosuccessfully 完成推入安裝。

## <a name="error-code-95117-protection-could-not-be-enabled"></a>(錯誤碼 95117) 無法啟用保護。
**錯誤碼** | **可能的原因** | **特定錯誤的建議**
--- | --- | ---
95117 </br>***訊息-***推入安裝的 hello 行動服務 toohello 來源電腦失敗，錯誤碼***EP0865***。 <br> Hello 來源機器未執行，或是沒有 hello 處理序伺服器與 hello 來源電腦之間的網路連線問題 | 處理序伺服器與來源伺服器之間的網路連線能力 | 檢查處理序伺服器與來源伺服器之間的連線能力。 </br> 此外，請確認下列必要條件是已核取的 toosuccessfully 完成推入安裝。

## <a name="error-code-95103-protection-could-not-be-enabled"></a>(錯誤碼 95103) 無法啟用保護。
**錯誤碼** | **可能的原因** | **特定錯誤的建議**
--- | --- | ---
95103 </br>***訊息-***推入安裝的 hello 行動服務 toohello 來源電腦失敗，錯誤碼***EP0854***。 <br> 可能是"Windows Management Instrumentation (WMI) 」 不允許在 hello 來源電腦上，或有 hello 處理序伺服器與 hello 來源電腦之間的網路連線問題| 在 hello Windows 防火牆封鎖 Windows Management Instrumentation (WMI) | 允許 Windows Management Instrumentation (WMI) 中的 hello Windows 防火牆。 在 Windows 防火牆設定之下 > [允許應用程式或功能通過防火牆] > [為所有設定檔選取 WMI]。 </br> 此外，請確認下列必要條件是已核取的 toosuccessfully 完成推入安裝。

## <a name="check-push-install-logs-for-errors"></a>檢查推送安裝記錄中的錯誤

Hello 設定/程序在伺服器上，瀏覽的 toofile 'PushinstallService' 位於<Microsoft Azure Site Recovery Install Location>\home\svsystems\pushinstallsvc\ toounderstand hello 來源 hello 問題和使用下列疑難排解步驟 tooresolve hello 問題。</br>
![pushiinstalllogs](./media/site-recovery-protection-common-errors/pushinstalllogs.png)

## <a name="push-install-pre-requisites-for-windows"></a>適用於 Windows 的推送安裝必要元件
### <a name="ensure-file-and-printer-sharing-is-enabled"></a>確保已啟用 [檔案及印表機共用]
允許 hello Windows 防火牆中的 hello 來源電腦上的 「 檔案及印表機共用 」 及 「 Windows Management Instrumentation" </br>
#### <a name="if-source-machine-is-domain-joined-br"></a>如果來源電腦已加入網域： </br>
使用群組原則管理主控台 (GPMC) 來進行防火牆設定。
1. 登入 tooActive 目錄網域電腦系統管理員身分，並開啟 群組原則管理主控台 (GPMC。MSC，從一開始執行 > 執行)。</br>
3. 如果未安裝 GPMC，請遵循 hello 連結太[安裝 hello GPMC](https://technet.microsoft.com/library/cc725932.aspx) </br>
4. 在 hello GPMC 主控台樹狀目錄中，按兩下 hello 樹系和網域群組原則物件，並瀏覽過 「 預設網域原則 」。 </br>
![gpmc1](./media/site-recovery-protection-common-errors/gpmc1.png) </br>
</br>
5. 以滑鼠右鍵按一下 [預設網域原則] > 編輯 > 將會開啟新的 [群組原則管理編輯器] 視窗。 </br>
![gpmc2](./media/site-recovery-protection-common-errors/gpmc2.png) </br>
</br>
6. 在 [hello 群組原則管理編輯器] 瀏覽 tooComputer 組態 > 原則 > 系統管理範本 > 網路 > 網路連線 > Windows 防火牆。 </br>
![gpmc3](./media/site-recovery-protection-common-errors/gpmc3.png) </br>
</br>
7. 啟用 hello 下列網域設定檔和標準設定檔設定 </br>
a)  連按兩下「Windows 防火牆：允許輸入檔案及印表機共用例外狀況」。 選取 [已啟用] 並按一下 [確定]。 </br>
b)  連按兩下「Windows 防火牆：允許輸入遠端系統管理例外狀況」。 選取 [已啟用] 並按一下 [確定]。 </br>
![gpmc4](./media/site-recovery-protection-common-errors/gpmc4.png) </br>
</br>

###### <a name="if-source-machine-is-not-domain-joined-and-part-of-workgroup-br"></a>如果來源電腦未加入網域並屬於工作群組的一部分 </br>
在遠端電腦上設定防火牆設定 (適用於工作群組)：
1. 移 toohello 來源電腦上，</br>
2. 在 Windows 防火牆設定之下 > [允許應用程式或功能通過防火牆] > 為所有設定檔選取 [檔案及印表機共用]。 </br>
3. 在 Windows 防火牆設定之下 > [允許應用程式或功能通過防火牆] > [為所有設定檔選取 WMI]。 </br>

#### <a name="disable-remote-user-account-control-uac"></a>停用遠端使用者帳戶控制 (UAC)
停用 UAC 使用登錄金鑰 toopush hello 行動服務。
1. 按一下 [開始] > [執行] > 鍵入 regedit > ENTER
2. 尋找並按一下下列登錄子機碼的 hello: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
3. 如果 hello LocalAccountTokenFilterPolicy 登錄項目不存在，請遵循下列步驟：
4. Hello 編輯 功能表上 > 新增 > 按一下 DWORD 值。
5. 鍵入 LocalAccountTokenFilterPolicy，然後按 ENTER 鍵。
6. 在 LocalAccountTokenFilterPolicy 上按一下滑鼠右鍵，然後按一下修改。
7. 在 hello 值資料 方塊中輸入 1，然後按一下確定。
8. 結束 [登錄編輯器]。


## <a name="push-install-pre-requisites-for-linux"></a>適用於 Linux 的推送安裝必要元件：

1. 建立 hello 來源 Linux 伺服器上的根使用者。 （使用此帳戶僅適用於 hello 推入安裝和更新）</br>
2. 請檢查該 hello 來源伺服器具有與所有網路介面卡相關聯的 hello 本機主機名稱 tooIP 位址對應的項目 Linux 上的 hello /etc/hosts 檔案。 </br>
3. 請確定來源 Linux 伺服器上所安裝的 hello 最新的 openssh、 openssh 伺服器和 openssl 封裝。 </br>
檢查 ssh 連接埠 22 已啟用並在執行中。 </br>
4. 檢查是否代理程式的過時的項目已經存在於 hello 來源伺服器上，解除安裝 hello 較舊的代理程式和伺服器 hello 重新開機，重新安裝代理程式。 </br>

#### <a name="enable-sftp-subsystem-and-password-authentication-in-hello-sshdconfig-file"></a>啟用 hello sshd_config 檔案中的 SFTP 子系統和密碼驗證
1. 在來源伺服器上，以 root 的身分登入。 </br>
2. 在 hello /etc/ssh/sshd_config 檔案，</br> 尋找開頭為 PasswordAuthentication hello 一行。 </br>
3. d.   Hello 行取消註解再變更 hello 值從 「 否 」 太"yes"。 </br>
![Linux1](./media/site-recovery-protection-common-errors/linux1.png)
4. 尋找開頭為"Subsystem"hello 一行和 hello 行取消註解。 </br>
![Linux2](./media/site-recovery-protection-common-errors/linux2.png)
5. 儲存 hello 變更，並重新啟動 hello sshd 服務。 </br>

## <a name="push-installation-checks-on-configurationprocess-server"></a>在組態/處理序伺服器上檢查推送安裝。
#### <a name="validate-credentials-for-discovery-and-installation"></a>驗證認證以供探索和安裝

1. 從組態伺服器啟動 Cspsconfigtool</br>
![WMItestConnect5](./media/site-recovery-protection-common-errors/wmitestconnect5.png) </br>

2. 請確定用於保護 hello 帳戶 hello 來源電腦上具有系統管理員權限。 </br>

#### <a name="check-connectivity-between-process-server-and-source-server"></a>檢查處理序伺服器與來源伺服器之間的連線能力
1. 確定處理序伺服器有網際網路連線。
2. 使用 wbemtest.exe 驗證 WMI 連線。 </br>
Hello 程序在伺服器上，按一下 [開始 > 執行 > wbemtest.exe > 所示，將會開啟 Windows Management Instrumentation 測試器] 視窗。</br>
   ![WMItestConnect1](./media/site-recovery-protection-common-errors/wmitestconnect1.png) </br>
   </br>
按一下 連線 > 輸入 hello 來源伺服器 IP hello 命名空間輸入使用者名稱和密碼 （如果來源機器已加入網域，提供 hello 網域名稱，以及為"domainName\username"的使用者名稱。 如果來源電腦是工作群組中，提供 hello 使用者名稱。）選取 hello 驗證層級做為封包私密性。 </br>
![WMItestConnect2](./media/site-recovery-protection-common-errors/wmitestconnect2.png) </br>
   </br>
   按一下 [連線]。 現在以提供資料的 hello hello WMI 連接應該會成功，而且應該顯示 hello Windows Management Instrumentation 測試器 視窗，如下所示： </br>
   ![WMItestConnect3](./media/site-recovery-protection-common-errors/wmitestconnect3.png) </br>
</br>
   如果 WMI 連線不成功，將有出現錯誤訊息快顯視窗。 hello，下列螢幕擷取畫面顯示嘗試失敗允許應用程式的 Windows 防火牆中是否未啟用遠端 WMI/系統管理。 </br>
   ![WMItestConnect4](./media/site-recovery-protection-common-errors/wmitestconnect4.png) </br>
</br>

3. 請檢查 hello WMI 狀態和連線。</br>
Hello 設定/程序在伺服器上， </br>
按一下 [開始] > 執行 > wmimgmt.msc > 動作 > 其他動作 > tooanother 電腦 （來源電腦） 連線。 </br>
輸入 hello hello 如果連線是正常的用於保護和核取的帳戶認證。 </br>

#### <a name="verify-network-shared-folders-of-source-machine-is-accessible-from-process-server-ps-remotely-using-specified-credentials"></a>確認可使用指定的認證從處理序伺服器 (PS) 遠端存取來源電腦的網路共用資料夾。
  1. 登入 tooProcess 伺服器 (PS) 的電腦，開啟檔案總管 > hello 位址列型別中 >"\\\source-machine-ip\C$"> 按一下 enter 鍵。 </br>
  ![Fileshare1](./media/site-recovery-protection-common-errors/fileshare1.png) </br>
  2. 檔案總管會提示輸入認證。 輸入 hello 使用者名稱和密碼 > 按一下 [確定]。</br>
   如果來源機器已加入網域，提供 hello 網域名稱，以及使用者名稱做為"domainName\username"。</br>
   如果來源電腦是工作群組中，提供僅 hello"username"。 </br>
  ![Fileshare2](./media/site-recovery-protection-common-errors/fileshare2.png) </br>
  3. 如果連線成功時，您可以檢視 hello 資料夾的來源電腦遠端從處理序伺服器 (PS) </br>
  ![Fileshare3](./media/site-recovery-protection-common-errors/fileshare3.png) </br>

> [!NOTE] 
> 如果連線不成功，請檢查是否符合所有必要條件。
>

如果您不想 tooopen"Windows Management Instrumentation 」，您也可以安裝行動服務手動 hello 來源電腦上。</br> [透過 GUI 手動安裝行動服務](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) </br>
[透過組態管理員指引進行安裝](site-recovery-install-mobility-service-using-sccm.md) </br>

## <a name="next-steps"></a>後續步驟
- [啟用 VMware 虛擬機器的複寫](vmware-walkthrough-enable-replication.md)
