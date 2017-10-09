---
title: "aaaDeploy hello Azure 堆疊開發套件 |Microsoft 文件"
description: "了解如何在 tooprepare hello Azure 堆疊開發套件及執行的 hello PowerShell 指令碼 toodeploy 它。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 0ad02941-ed14-4888-8695-b82ad6e43c66
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/17/2017
ms.author: erikje
ms.openlocfilehash: a96879fb91000f6b3d3aac3089861e8a573ebead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-azure-stack-development-kit"></a>部署 hello Azure 堆疊開發套件
toodeploy hello 開發套件，您必須完成下列步驟的 hello:

1. [下載 hello 部署套件](https://azure.microsoft.com/overview/azure-stack/try/?v=try)tooget hello Cloudbuilder.vhdx。
2. [準備 hello cloudbuilder.vhdx](#prepare-the-development-kit-host)執行 hello asdk installer.ps1 指令碼 tooconfigure hello 電腦 （hello 開發套件主機），您會想 tooinstall 開發套件。 這個步驟之後，hello 開發套件主機將會開機 toohello Cloudbuilder.vhdx。
3. [部署 hello 開發套件](#deploy-the-development-kit)hello 開發套件主機上。

> [!NOTE]
> 獲得最佳結果，即使您希望 toouse 中斷連線的 Azure 堆疊環境，它是連接 toohello 時的最佳 toodeploy 網際網路。 這樣一來，您可以在部署期間啟動 hello Windows Server 2016 評估版。 如果在 10 天內未啟動 hello Windows Server 2016 評估版，它會關閉。
> 
> 

## <a name="download-and-extract-hello-development-kit"></a>下載並解壓縮 hello 開發套件
1. Hello 下載開始之前，請確定您的電腦符合下列必要條件 hello:

   * hello 電腦必須至少為 60 GB 的可用磁碟空間。
   * 必須安裝 [.NET framework 4.6 (或更新版本)](https://aka.ms/r6mkiy)。

2. [移 toohello 開始頁面](https://azure.microsoft.com/overview/azure-stack/try/?v=try)，提供您詳細資料，然後按一下**送出**。
3. 在下**下載 hello 軟體**，按一下  **Azure 堆疊開發套件**。
4. 執行下載的 hello AzureStackDownloader.exe 檔案。
5. 在 [hello **Azure 堆疊開發套件程式下載程式**] 視窗中，遵循步驟 1 至 5。
6. Hello 下載完成之後，請按一下**執行**toolaunch hello MicrosoftAzureStackPOC.exe。
7. 檢閱 hello 授權合約 畫面和 hello 自我解壓縮程式精靈的資訊，然後按一下**下一步**。
8. 檢閱 hello 隱私權聲明螢幕和 hello 自我解壓縮程式精靈的資訊，然後按一下**下一步**。
9. 選取 hello hello 的目的地檔案 toobe 解壓縮，請按一下**下一步**。
   * hello 預設值是： <drive letter>:\<目前資料夾 > \Microsoft Azure 堆疊
10. 檢閱 hello 目的地位置 畫面和 hello 自我解壓縮程式精靈的資訊，然後按一下**擷取**tooextract hello CloudBuilder.vhdx (~ 25 GB) 及 ThirdPartyLicenses.rtf 檔案。 此程序將需要一些時間 toocomplete。

> [!NOTE]
> Hello 檔案解壓縮之後，您可以刪除 hello 機器上的 hello exe 和分類收納檔案 toorecover 空間。 或者，您可以移動這些檔案 tooanother 位置，如果您需要 tooredeploy 您就不需要 toodownload hello 檔案一次。
> 
> 

## <a name="prepare-hello-development-kit-host"></a>準備 hello 開發套件主應用程式
1. 請確定您可以實際連接 toohello 開發套件的主機，或存取實體主控台 （例如 KVM)。 當您重新開機 hello 開發套件主應用程式在下面步驟 13，必須有這類存取。
2. 請確定 hello 開發套件主機符合 hello[最低需求](azure-stack-deploy.md)。 您可以使用 hello[部署適用於 Azure 堆疊檢查程式](https://gallery.technet.microsoft.com/Deployment-Checker-for-50e0f51b)tooconfirm 您的需求。
3. 以本機系統管理員 tooyour 開發套件主機 hello 登入。
4. 複製或移動 hello CloudBuilder.vhdx 檔案 toohello 根目錄的 hello C:\ 磁碟機 (C:\CloudBuilder.vhdx)。
5. 執行下列指令碼 toodownload hello 開發套件安裝程式檔案 (asdk installer.ps1) toohello c:\AzureStack_Installer 資料夾，您的開發套件主機上的 hello。
    ```powershell
    # Variables
    $Uri = 'https://raw.githubusercontent.com/Azure/AzureStack-Tools/master/Deployment/asdk-installer.ps1'
    $LocalPath = 'c:\AzureStack_Installer'

    # Create folder
    New-Item $LocalPath -Type directory

    # Download file
    Invoke-WebRequest $uri -OutFile ($LocalPath + '\' + 'asdk-installer.ps1')
    ```
6. 開啟提升權限的 PowerShell 主控台 > 執行 hello C:\AzureStack_Installer\asdk-installer.ps1 指令碼 > 按一下**準備 vhdx**。
7. 在 hello**選取 Cloudbuilder vhdx** hello 安裝程式中，瀏覽 tooand 選取 hello cloudbuilder.vhdx 下載檔案，在 hello 先前步驟中的頁面。
8. 選擇性： 核取 hello**新增驅動程式**方塊 toospecify 包含您想 hello 主機的其他驅動程式的資料夾。
9. 在 hello**選擇性設定**頁面上，提供 hello hello 開發套件主機的本機系統管理員帳戶。 如果您沒有提供這些認證，您將在下方的 hello 安裝程序期間需要 KVM 存取 toohello 主機。
10. 也在 hello**選擇性設定**頁面上，您可以遵循 hello 選項 tooset hello:
    - **Computername**： 這個選項會設定 hello hello 開發套件主機名稱。 hello 名稱必須符合 FQDN 需求，而且必須是 15 個字元長度等於或小於。 hello 預設是由 Windows 產生隨機的電腦名稱。
    - **時區**： 集 hello hello 開發套件主機的時區。 hello 預設值是 (UTC-8:00) 太平洋時間 （美國和加拿大）。
    - **靜態 IP 組態**： 設定部署 toouse 靜態 IP 位址。 否則，當 hello installer hello cloudbuilder.vhx 重新開機，hello 網路介面設定的 DHCP。
11. 按一下 [下一步] 。
12. 如果您選擇靜態 IP 組態 hello 上一個步驟中，您必須立即：
    - 選取網路介面卡。 請確定您可以連接 toohello 配接器，再按一下 **下一步**。
    - 請確定該 hello **IP 位址**，**閘道**，和**DNS**值正確無誤，然後按一下**下一步**。
13. 按一下**下一步**toostart hello 準備程序。
14. 當 hello 準備表示**已完成**，按一下 **下一步**。
15. 按一下**立即重新開機**到 hello cloudbuilder.vhdx tooboot 並繼續 hello 部署程序。

## <a name="deploy-hello-development-kit"></a>部署 hello 開發套件
1. 以本機系統管理員 toohello 開發套件主機 hello 登入。 使用 hello hello 先前步驟中指定的認證。

    > [!IMPORTANT]
    > Azure Active Directory 部署中，Azure 堆疊需要存取 toohello 網際網路，直接或透過 transparent proxy。 hello 部署支援只有一個 NIC 的網路功能。 如果您有多個 Nic 時，請確定只有一個已啟用 （，其他所有項目已停用） 才能執行 hello 下一節中的 hello 部署指令碼。
    
2. 開啟提升權限的 PowerShell 主控台 > 執行 hello \AzureStack_Installer\asdk-installer.ps1 指令碼 （這可能是在 hello Cloudbuilder.vhdx 中的不同磁碟機上） > 按一下**安裝**。
3. 在 hello**類型**方塊中，選取**Azure 雲端**或**ADFS**。
    - **Azure 雲端**: Azure Active Directory 是 hello 身分識別提供者。 使用此參數 toospecify 特定目錄 hello AAD 帳戶具有全域系統管理員權限的位置。 AAD 目錄租用戶中的 hello 格式的完整名稱。.onmicrosoft.com。 
    - **ADFS**: hello 預設戳記目錄服務是 hello 身分識別提供者，在與 hello 預設帳戶 toosign azurestackadmin@azurestack.local，而且 hello 密碼 toouse hello 您提供 hello 安裝程序。
4. 在下**本機系統管理員密碼**，在 hello**密碼** 方塊中，輸入 hello 本機系統管理員密碼 （它必須符合 hello 目前設定的本機系統管理員密碼），然後按一下 **下一步**。
5. 選取網路介面卡 toouse hello 開發套件，然後按一下**下一步**。
6. 選取的 DHCP 或靜態的網路組態 hello BGPNAT01 虛擬機器。
    - **DHCP** （預設值）： hello 虛擬機器從 hello DHCP 伺服器取得 hello IP 網路設定。
    - **靜態**： 只有當 DHCP 無法指定有效的 IP 位址，如 Azure 堆疊 tooaccess hello 網際網路使用此選項。 必須指定靜態 IP 位址與 hello 子網路遮罩長度 (例如，10.0.0.5/24)。
7. 選擇性地設定下列值的 hello:
    - **VLAN ID**： 集 hello VLAN id。 只有當 hello 主機以及 AzS BGPNAT01 必須設定 VLAN ID tooaccess hello 實體網路 （與網際網路） 時，才能使用此選項。 
    - **DNS 轉寄站**: hello Azure 堆疊部署的一部分建立的 DNS 伺服器。 tooallow hello 戳記 hello 方案 tooresolve 名稱內的電腦提供您現有基礎結構的 DNS 伺服器。 hello 戳記中 DNS 伺服器將轉寄無法辨識的名稱解析要求 toothis 伺服器。
    - **時間伺服器**：設定特定的時間伺服器。 
8. 按一下 [下一步] 。 
9. 在 [hello**驗證網路介面卡內容**] 頁面上，您會看到進度列。 
    - 如果，該處會指示**無法下載更新**，依照 hello 頁面上 hello 指示。
    - 顯示 [已完成] 時，按一下 [下一步]。
10. 在 [摘要] 頁面上，按一下 [部署]。
11. 如果您使用 Azure Active Directory 部署，您將會詢問 tooenter 您 Azure Active Directory 的全域管理員帳戶認證。
12. hello 部署程序可能需要幾小時，期間 hello 系統會自動重新開機一次。
   
   > [!IMPORTANT]
   > 如果您想 toomonitor hello 部署進度，azurestack\AzureStackAdmin 身分登入。 如果您登入本機系統管理員 hello 機器之後加入 toohello 網域時，就看 hello 部署進度。 請勿重新部署，而是登入為 azurestack\AzureStackAdmin toovalidate 它正在執行。
   > 
   > 
   
    Hello 部署成功時，會顯示 hello PowerShell 主控台：**完成： 動作 '部署'**。
   
如果 hello 部署失敗，您可以使用中的 hello 下列重新執行的 PowerShell 指令碼的 hello 相同提升權限的 PowerShell 視窗：

```powershell
cd c:\CloudDeployment\Setup
.\InstallAzureStackPOC.ps1 -Rerun
```

此指令碼會重新啟動 hello 成功的最後一個步驟中的 hello 部署。

或者，您可以從頭開始[重新部署](azure-stack-redeploy.md)。


## <a name="reset-hello-password-expiration-too180-days"></a>重設 hello 密碼到期 too180 天數

toomake 確定 hello 密碼到期的 hello 開發套件主應用程式不會太快，請遵循下列步驟部署之後：

1. Hello 開發套件在主機上，開啟**群組原則管理**並瀏覽過**群組原則管理**–**樹系： azurestack.local** –**網域** – **azurestack.local**。
2. 以滑鼠右鍵按一下 [MemberServer]，然後按一下 [編輯]。
3. Hello 群組原則管理編輯器，在瀏覽過**電腦設定**–**原則**– **Windows 設定**–**安全性設定**–**帳戶原則**–**密碼原則**。
4. 在 hello 右窗格中，按兩下**密碼最長有效期**。
5. 在 hello**密碼最長有效期屬性**對話方塊中，變更 hello**密碼即將於**值 too180，然後按一下 **確定**。


## <a name="next-steps"></a>後續步驟
[使用您的 Azure 訂用帳戶註冊 Azure Stack](azure-stack-register.md)

[連接 tooAzure 堆疊](azure-stack-connect-azure-stack.md)

