---
title: "aaaHow toocreate 自訂的範本映像的 Azure RemoteApp |Microsoft 文件"
description: "了解 toocreate 自訂範本的 Azure RemoteApp 的映像。 您可以使用此範本與混合式或雲端集合搭配。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: b9ec5b51-f7cd-470b-8545-d0fd714c5982
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9e3a0b2d3cc56177ea51406e6cecfe19ff235340
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-custom-template-image-for-azure-remoteapp"></a>Toocreate 自訂範本的 Azure RemoteApp 的映像
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

Azure RemoteApp 使用 Windows Server 2012 R2 範本映像 toohost 所有 hello 程式，您會想 tooshare 與您的使用者。 toocreate 自訂的 RemoteApp 範本映像，您可以開始使用現有的映像或另外新建一個。 

> [!TIP]
> 您知道您可以從 Azure VM 建立映像嗎？ True 的劇本，並減少了 hello 一段時間它採用 tooimport hello 映像。 簽出 hello 步驟[這裡](remoteapp-image-on-azurevm.md)。
> 
> 

可以上傳 Azure RemoteApp 搭配使用的 hello 映像的 hello 需求如下：

* hello 映像大小應該是 mb/s 的倍數。 如果您嘗試 tooupload 不精確的多個映像，hello 上傳將會失敗。
* hello 影像大小必須為 127 GB 或更小。
* 必須在 VHD 檔案上 (目前不支援 VHDX 檔案 [Hyper-V 虛擬硬碟])。
* hello VHD 不能在第 2 代虛擬機器。
* hello VHD 可以是固定大小或動態擴充。 因為它會採用比固定大小的 VHD 檔案的較少時間 tooupload tooAzure，建議您使用動態擴充的 VHD。
* 必須使用 hello 主開機記錄 (MBR) 磁碟分割樣式初始化磁碟 hello。 不支援 hello GUID 磁碟分割表格 (GPT) 磁碟分割樣式。
* hello VHD 必須包含單一 Windows Server 2012 R2 的安裝。 它可包含多個磁碟區，但只有其中一個包含 Windows 安裝。
* 必須安裝 hello 遠端桌面工作階段主機 (RDSH) 角色和 hello 桌面體驗功能。
* hello 遠端桌面連線代理人角色必須*不*安裝。
* 必須停用 hello 加密檔案系統 (EFS)。
* hello 映像必須使用 hello 參數 SYSPREPed **/oobe /generalize /shutdown** (請勿使用 hello **/mode: vm**參數)。
* 不支援從快照鏈結上傳您 VHD。

**開始之前**

您需要建立 hello 服務之前 toodo hello 下列：

* [註冊](https://azure.microsoft.com/services/remoteapp/) RemoteApp。
* 建立使用者帳戶在 Active Directory toouse，為 hello RemoteApp 服務帳戶。 限制此帳戶的 「 hello 」 權限，讓它只會將機器 toohello 網域。 如需詳細資訊，請參閱 [設定 RemoteApp 的 Azure Active Directory](remoteapp-ad.md) 。
* 收集內部部署網路的相關資訊：IP 位址資訊和 VPN 裝置詳細資料。
* 安裝 hello [Azure PowerShell](/powershell/azure/overview)模組。
* 收集您想要 toogrant 存取的 hello 使用者的相關資訊。 這可以是使用者 Microsoft 帳戶資訊或 Active Directory 工作帳戶資訊。

## <a name="create-a-template-image"></a>建立範本映像
這些是 hello 高階步驟 toocreate 從頭新的範本映像：

1. 找出 Windows Server 2012 R2 Update DVD 或 ISO 映像。
2. 建立 VHD 檔案。
3. 安裝 Windows Server 2012 R2。
4. 安裝 hello 遠端桌面工作階段主機 (RDSH) 角色和 hello 桌面體驗 」 功能。
5. 安裝您的應用程式所需的其他功能。
6. 安裝及設定您的應用程式。 toomake 共用應用程式更容易，新增的任何應用程式或您想 tooshare toohello 程式**啟動**hello 映像，特別是在 **%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs 的功能表。
7. 執行您的應用程式所需的任何其他 Windows 設定。
8. 停用 hello 加密檔案系統 (EFS)。
9. **REQUIRED:** tooWindows Update 去安裝所有重要更新。
10. SYSPREP hello 映像。

hello 建立新的映像的詳細的步驟如下：

1. 找出 Windows Server 2012 R2 Update DVD 或 ISO 映像。
2. 使用「磁碟管理」建立 VHD 檔案。
   
   1. 啟動「磁碟管理」(diskmgmt.msc)。
   2. 建立會動態擴充、大小 40 GB 或更大的 VHD。 （評估 hello 工作量用於 Windows、 應用程式，以及自訂所需的空間。 Windows Server 與 hello RDSH 角色和已安裝桌面體驗功能將需要大約 10 GB 的空間）。
      
      1. 按一下 [動作 > 建立 VHD]。
      2. 指定 hello 位置、 大小和 VHD 格式。 選取 動態擴充，然後按一下確定。
      
      此作業會執行數秒。 Hello VHD 建立完成時，您應該會看到新的磁碟不含任何磁碟機代號，並在 hello 磁碟管理 主控台中，「 未初始化 」 狀態。
      
      * Hello 磁碟 （不 hello 未配置的空間） 上按一下滑鼠右鍵，然後按一下**初始化磁碟**。 選取**MBR** （主開機記錄） 作為 hello 磁碟分割樣式，然後按一下**確定**。
      * 建立新的磁碟區： hello 未配置空間，以滑鼠右鍵按一下，然後按一下**新增簡單磁碟區**。 您可以接受 hello hello 精靈中的預設值，但請確定當您上傳 hello 範本映像時，指派磁碟機代號 tooavoid 潛在問題。
      * Hello 磁碟上按一下滑鼠右鍵，然後按一下**中斷連結 VHD**。
3. 安裝 Windows Server 2012 R2：
   
   1. 建立新的虛擬機器。 使用新的虛擬機器精靈，在 HYPER-V 管理員] 或 [用戶端 HYPER-V hello。
      1. 在 hello 指定世代 頁面上，選擇 **第 1 代**。
      2. 在 hello 連接虛擬硬碟 頁面上，選取 **使用現有的虛擬硬碟**，並瀏覽 toohello hello 先前步驟中所建立的 VHD。
      3. 在 hello 安裝選項 頁面上，選取 **安裝作業系統從開機 CD/DVD_ROM**，然後選取 Windows Server 2012 R2 安裝媒體的 hello 位置。
      4. 選擇 hello 精靈需要 tooinstall Windows 中的其他選項和您的應用程式。 完成 hello 精靈。
   2. Hello 精靈完成後，編輯 hello hello 虛擬機器設定，並變更任何其他必要 tooinstall Windows 與程式，例如 hello 虛擬處理器數目，，然後按一下**確定**。
   3. Toohello 虛擬機器連線，並安裝 Windows Server 2012 R2。
4. 安裝 hello 遠端桌面工作階段主機 (RDSH) 角色和 hello 桌面體驗功能：
   1. 啟動伺服器管理員。
   2. 按一下**新增角色及功能**hello 歡迎畫面上，或從 hello**管理**功能表。
   3. 按一下**下一步**hello 在您開始前 頁面上。
   4. 選取 角色型或功能型安裝，然後按一下下一步。
   5. 從 [hello] 清單中，選取 hello 本機電腦，然後按一下**下一步**。
   6. 選取 [遠端桌面服務]，然後按 [下一步]。
   7. 展開 [使用者介面與基礎結構]，然後選取 [桌面體驗]。
   8. 按一下 [新增功能]，然後按 [下一步]。
   9. 在 hello 遠端桌面服務 頁面上，按一下 **下一步**。
   10. 按一下 [遠端桌面工作階段主機] 。
   11. 按一下 [新增功能]，然後按 [下一步]。
   12. Hello 確認安裝選項 頁面上，選取**必要時自動重新啟動 hello 目的地伺服器**，然後按一下**是**hello 上重新啟動的警告。
   13. 按一下 [Install] 。 hello 電腦將重新啟動。
5. 安裝您的應用程式，例如 hello.NET Framework 3.5 所需的其他功能。 tooinstall hello 功能，執行 hello 新增角色及功能精靈。
6. 安裝和設定 hello 程式以及您想要透過 RemoteApp toopublish 應用程式。

> [!IMPORTANT]
> 安裝 hello RDSH 角色之前安裝的應用程式 tooensure hello 映像之前，會發現任何問題的應用程式相容性上傳 tooRemoteApp。
> 
> 請確定快顯 tooyour 應用程式 (**.lnk**檔案) 會出現在 hello**啟動**(%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs) 的所有使用者的功能表。 此外也請確認您在 hello 中看到該 hello 圖示**啟動**功能表是您想要使用者 toosee。 如果不是，請變更圖示。 (不這麼做*有*tooadd hello 應用程式 toohello 開始功能表上，但它讓它更容易 toopublish hello 應用程式中的 RemoteApp。 否則，您必須 tooprovide hello 安裝路徑 hello 應用程式發行 hello 應用程式時。）
> 
> 

1. 執行您的應用程式所需的任何其他 Windows 設定。
2. 停用 hello 加密檔案系統 (EFS)。 執行下列命令，在提升權限的命令視窗中的 hello:
   
     Fsutil 行為集 disableencryption 1
   
   或者，您可以設定，或新增下列 DWORD 值 hello 登錄中的 hello:
   
     HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableEncryption = 1
3. 如果您要建置您的映像，在 Azure 虛擬機器內，重新命名 hello  **\%windir%\Panther\Unattend.xml**檔案，這樣將會封鎖 hello 上傳用指令碼，稍後無法運作。 變更這個檔案 tooUnattend.old hello 名稱，使您仍會有 hello 檔案，以防您需要 toorevert 您的部署。
4. TooWindows Update 去安裝所有重要更新。 您可能需要 toorun Windows Update 多次 tooget 所有更新。 (有時候您安裝更新，而該更新本身又需要另外的更新。)
5. SYSPREP hello 映像。 在提升權限的命令提示字元執行下列命令的 hello:
   
   **C:\Windows\System32\sysprep\sysprep.exe /generalize /oobe /shutdown**
   
   **注意：**不使用 hello **/mode: vm** hello SYSPREP 命令，即使這是虛擬機器的參數。

## <a name="next-steps"></a>後續步驟
既然您已自訂的範本映像，您需要 tooupload 該映像 tooyour RemoteApp 集合。 請使用您的集合在下列文章 toocreate hello hello 資訊：

* [如何 toocreate RemoteApp 的混合式集合](remoteapp-create-hybrid-deployment.md)
* [如何 toocreate 的 RemoteApp 雲端集合](remoteapp-create-cloud-deployment.md)

