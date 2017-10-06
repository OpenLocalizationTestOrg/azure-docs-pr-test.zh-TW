---
title: "aaaUse PowerShell tooCreate VM 具有原生模式報表伺服器 |Microsoft 文件"
description: "本主題說明並引導您完成 hello 部署和 SQL Server Reporting Services 原生模式報表伺服器在 Azure 虛擬機器的組態。 "
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: e7791199c87dff106132f1535da12de40a8dbc9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-vm-with-a-native-mode-report-server"></a>使用 PowerShell tooCreate Azure VM 具有原生模式報表伺服器
> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

本主題說明並引導您完成 hello 部署和 SQL Server Reporting Services 原生模式報表伺服器在 Azure 虛擬機器的組態。 步驟在此文件使用的手動步驟 toocreate hello 虛擬機器和 Windows PowerShell 指令碼組合 hello hello VM 上 tooconfigure Reporting Services。 hello 組態指令碼包含開啟 HTTP 或 HTTPs 的防火牆連接埠。

> [!NOTE]
> 如果您不需要**HTTPS** hello 報表伺服器上，**略過步驟 2**。
> 
> 之後在步驟 1 中建立 hello VM，請前往 toohello 區段使用指令碼 tooconfigure hello 報表伺服器 HTTP。 執行 hello 指令碼之後，hello 報表伺服器是準備 toouse。

## <a name="prerequisites-and-assumptions"></a>必要條件與假設
* **Azure 訂用帳戶**： 驗證您的 Azure 訂閱中可用的核心 hello 號碼。 如果您建立建議的 VM 大小的 hello **A3**，您需要**4**可用的核心。 若您採用 **A2** 的 VM 大小，則需要 **2** 個可用的核心。
  
  * tooverify hello 核心限制 hello Azure 傳統入口網站，在您訂用帳戶，按一下 hello 上方功能表中 hello 左的窗格，然後按一下 使用方式的設定。
  * tooincrease hello 核心配額，請連絡[Azure 支援](https://azure.microsoft.com/support/options/)。 如需 VM 大小的資訊，請參閱 [Azure 的虛擬機器大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
* **Windows PowerShell 指令碼**: hello 主題假設您有基本的 Windows PowerShell 的實用知識。 如需有關如何使用 Windows PowerShell 的詳細資訊，請參閱 hello 下列：
  
  * [在 Windows Server 上啟動 Windows PowerShell (英文)](https://technet.microsoft.com/library/hh847814.aspx)
  * [開始使用 Windows PowerShell (英文)](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a>步驟 1：佈建 Azure 虛擬機器
1. 瀏覽 toohello Azure 傳統入口網站。
2. 按一下**虛擬機器**hello 左窗格中。
   
    ![Microsoft Azure 虛擬機器](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. 按一下 [新增] 。
   
    ![新增按鈕](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. 按一下 [從資源庫] 。
   
    ![從資源庫新增 VM](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. 按一下**SQL Server 2014 RTM Standard – Windows Server 2012 R2**然後按一下hello 箭號 toocontinue。
   
    ![下一步](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    如果您需要 hello Reporting Services 資料驅動訂閱功能，請選擇**SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**。 如需有關 SQL Server 版本及支援功能的詳細資訊，請參閱[hello SQL Server 2012 版本所支援的功能](https://msdn.microsoft.com/library/cc645993.aspx#Reporting)。
6. 在 hello**虛擬機器組態**頁面上，編輯下列欄位的 hello:
   
   * 如果有一個以上**版本發行日期**，選取 hello 最新版本。
   * **虛擬機器名稱**: hello 機器的名稱也會 hello 下一個組態頁面與 hello 預設雲端服務 DNS 名稱。 跨 hello Azure 服務，hello DNS 名稱必須是唯一的。 請考慮使用描述哪些 hello 用於 VM 的電腦名稱設定 hello VM。 例如 ssrsnativecloud。
   * [層]：標準
   * **大小： A3** hello 建議用於 SQL Server 工作負載的 VM 大小。 若 VM 只當做報表伺服器，則 A2 的 VM 大小已足夠，除非 hello 報表伺服器會面臨大量的工作負載。 如需 VM 的價格資訊，請參閱 [虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/)。
   * **新的使用者名稱**: hello 您所提供的名稱會建立為 hello VM 上的系統管理員。
   * [新增密碼] 並**確認**。 此密碼用於 hello 新系統管理員帳戶，並建議使用強式密碼。
   * 按一下 [下一步] 。 ![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
7. 在 hello 下一個頁面上，編輯下列欄位的 hello:
   
   * [雲端服務]：選取 [建立新的雲端服務]。
   * **雲端服務 DNS 名稱**： 這是 hello 與 hello VM 相關聯的雲端服務的 hello 公開 DNS 名稱。 hello 預設名稱是您在輸入中的 hello VM 名稱的 hello 名稱。 如果您於稍後步驟中的 hello 主題，您可以建立受信任的 SSL 憑證並再 hello DNS 名稱 hello hello 值"**發給**"hello 憑證。
   * **區域/同質群組/虛擬網路**： 選擇 hello 區域最接近 tooyour 終端使用者。
   * [儲存體帳戶]：使用自動產生的儲存體帳戶。
   * [可用性設定組]：無。
   * **端點**保持 hello**遠端桌面**和**PowerShell**端點然後再加入 HTTP 或 HTTPS 端點，根據您的環境。
     
     * **HTTP**: hello 公用及私用通訊埠為的預設**80**。 請注意，如果您使用 80 以外的私用連接埠修改**$HTTPport = 80** hello http 指令碼中。
     * **HTTPS**: hello 公用及私用通訊埠為的預設**443**。 安全性最佳作法是 toochange hello 私用連接埠，並設定防火牆與 hello 報表伺服器 toouse hello 私用連接埠。 如需有關端點的詳細資訊，請參閱[如何 tooSet 與虛擬機器的通訊](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。 請注意，如果您使用 443 以外的連接埠變更 hello 參數**$HTTPsport = 443** hello HTTPS 指令碼中。
   * 按 [下一步]。 ![下一步](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. 在 hello hello 精靈的最後一個頁面上，保留 hello 預設**安裝 hello VM 代理程式**選取。 hello 本主題中的步驟不會使用 hello VM 代理程式，但如果您計劃 tookeep 此 VM，hello VM 代理程式和擴充功能可讓您 tooenhance 他 CM。  如需有關 hello VM 代理程式的詳細資訊，請參閱[VM 代理程式和延伸模組 – 第 1 部分](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/)。 其中一個執行 hello 預設安裝的擴充功能 ad hello VM 桌面上會顯示 hello"BGINFO"延伸模組，系統資訊，例如內部 IP 和可用磁碟空間。
9. 按一下 [完成]。 ![Ok](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. hello**狀態**的 VM 會顯示為 hello**啟動 （正在佈建）**期間 hello 佈建程序，則將顯示為**執行**當 hello VM 已佈建並就緒toouse。

## <a name="step-2-create-a-server-certificate"></a>步驟 2：建立伺服器憑證
> [!NOTE]
> 如果您不需要 HTTPS hello 報表伺服器上，您可以**略過步驟 2**並移 toohello 區段**使用指令碼 tooconfigure hello 報表伺服器和 HTTP**。 使用 hello HTTP 指令碼 tooquickly 設定 hello 報表伺服器和伺服器會準備 toouse hello 報表。

在訂單 toouse HTTPS hello VM 上，您會需要受信任的 SSL 憑證。 根據您的案例中，您可以使用下列兩種方法的 hello 的其中一個：

* 由憑證授權單位 (CA) 核發，且受到 Microsoft 信任的有效 SSL 憑證。 hello CA 根憑證會經由 Microsoft 根憑證計劃 hello 散發的必要的 toobe。 如需此計劃的詳細資訊，請參閱[Windows 和 Windows Phone 8 SSL 根憑證計劃 (成員 Ca)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx)和[簡介 toohello Microsoft 根憑證計劃](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx)。
* 自我簽署憑證。 不建議將自我簽署憑證用於生產環境。

### <a name="toouse-a-certificate-created-by-a-trusted-certificate-authority-ca"></a>toouse 由受信任憑證授權單位 (CA) 所建立的憑證
1. **要求 hello 網站的伺服器憑證的憑證授權單位**。 
   
    您可以使用任一 toogenerate 憑證要求檔案 (Certreq.txt) 的線上憑證授權單位的要求時，都需要傳送 tooa 憑證授權單位或 toogenerate hello Web 伺服器憑證精靈。 例如 Windows Server 2012 中的 Microsoft Certificate Services。 根據您的伺服器憑證所提供的識別保證 hello 等級，hello 憑證授權單位 tooapprove 數天 tooseveral 月您的要求，並將憑證檔案。 
   
    如需有關申請伺服器憑證的詳細資訊，請參閱 hello 下列： 
   
   * 使用 [Certreq](https://technet.microsoft.com/library/cc725793.aspx)、[Certreq](https://technet.microsoft.com/library/cc725793.aspx)。
   * 安全性工具 tooAdminister Windows Server 2012。
     
     [安全性工具 tooAdminister Windows Server 2012](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > hello**發給**欄位 hello 信任 SSL 憑證應該是 hello 相同為 hello**雲端服務 DNS 名稱**的 hello 新的 VM。

2. **Hello 網頁伺服器上安裝 hello 伺服器憑證**。 在此情況下則 hello VM 主機 hello 報表伺服器，並在稍後步驟中建立 hello 網站時設定 Reporting Services hello 網頁伺服器。 如需 hello 伺服器憑證安裝在 hello Web 伺服器上，使用 hello 憑證 MMC 嵌入式管理單元的詳細資訊，請參閱[安裝伺服器憑證](https://technet.microsoft.com/library/cc740068)。
   
    如果您想 toouse hello 指令碼包含本主題中，tooconfigure hello 報表伺服器，hello hello 憑證值**指紋**無須為 hello 指令碼的參數。 上如何 tooobtain hello hello 憑證的指紋，請參閱 hello 下一節，如需詳細資訊。
3. 指派 hello 伺服器憑證 toohello 報表伺服器。 當您設定 hello 報表伺服器 hello 分派完成 hello 下一節。

### <a name="toouse-hello-virtual-machines-self-signed-certificate"></a>toouse hello 虛擬機器自我簽署憑證
Hello VM 佈建時 hello VM 上建立自我簽署的憑證。 hello 憑證具有名稱為 hello VM DNS 名稱相同的 hello。 在訂單 tooavoid 憑證錯誤，就需要該 hello 憑證受到信任 hello VM 本身，還要受到 hello 站台的所有使用者。

1. hello 本機的 VM 上的 hello 憑證 tootrust hello 根 CA 加入 hello 憑證 toohello**受信任的根憑證授權單位**。 hello 以下是摘要 hello 所需的步驟。 如需如何 tootrust hello CA 的詳細步驟，請參閱[安裝伺服器憑證](https://technet.microsoft.com/library/cc740068)。
   
   1. 從 hello Azure 傳統入口網站，選取 hello VM，然後按一下 連線。 根據瀏覽器的設定，您可能會提示的 toosave.rdp 檔案，以連接 toohello VM。
      
       ![tooazure 虛擬機器連線](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) 使用 hello 使用者 VM 名稱、 使用者名稱和密碼建立 hello VM 時設定。 
      
       例如，在下列映像的 hello，hello VM 名稱是**ssrsnativecloud**而 hello 使用者名稱為**testuser**。
      
       ![登入包括 VM 名稱](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. 執行 mmc.exe。 如需詳細資訊，請參閱[How to： 使用 hello MMC 嵌入式管理單元檢視憑證](https://msdn.microsoft.com/library/ms788967.aspx)。
   3. Hello 主控台應用程式中**檔案**功能表上，新增 hello**憑證**嵌入式管理單元中，選取**電腦帳戶**當出現提示，然後按一下**下一步**.
   4. 選取**本機電腦**toomanage，然後按一下**完成**。
   5. 按一下**確定**然後展開 hello**憑證-個人**節點，然後按一下**憑證**。 hello 憑證 hello 的 hello VM 的 DNS 名稱來命名，並結束**.cloudapp.net**。 以滑鼠右鍵按一下 hello 憑證名稱，然後按一下**複製**。
   6. 展開 hello**受信任的根憑證授權單位**節點，然後以滑鼠右鍵按一下**憑證**，然後按一下**貼上**。
   7. hello 下的憑證名稱按一下雙 toovalidate**受信任的根憑證授權單位**，並確定沒有任何錯誤，而且您會看到您的憑證。 如果您想 toouse hello HTTPS 指令碼包含本主題中，tooconfigure hello 報表伺服器，hello hello 憑證值**指紋**無須為 hello 指令碼的參數。 **tooget hello 指紋值**，完成下列 hello。 區段中還有 PowerShell 範例 tooretrieve hello 指紋[使用指令碼 tooconfigure hello 報表伺服器和 HTTPS](#use-script-to-configure-the-report-server-and-HTTPS)。
      
      1. 按兩下 hello 憑證，例如 ssrsnativecloud.cloudapp.net hello 名稱。
      2. 按一下 hello**詳細資料** 索引標籤。
      3. 按一下 [指紋] 。 hello hello 指紋值欄位中所顯示 hello 詳細資料，例如 a6 08 3c df f9 0b f7 e3 7 c 25 ed a4 ed 7e ac 91 9 c 2c fb 2f。
      4. 複製 hello 指紋並儲存供稍後 hello 值或現在編輯 hello 指令碼。
      5. (*)執行 hello 指令碼之前，請移除 hello 配對值中間的 hello 空格。 例如 hello 前述的憑證指紋現在會是 a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f。
      6. 指派 hello 伺服器憑證 toohello 報表伺服器。 當您設定 hello 報表伺服器 hello 分派完成 hello 下一節。

如果您使用自我簽署的 SSL 憑證，hello hello 憑證名稱就會與 hello hello VM 主機名稱。 因此，hello hello 機器的 DNS 已向全球註冊，而且可以從任何用戶端存取。

## <a name="step-3-configure-hello-report-server"></a>步驟 3： 設定報表伺服器 hello
本節將引導您完成設定 hello VM 做為 Reporting Services 原生模式報表伺服器。 您可以使用下列方法 tooconfigure hello 報表伺服器的 hello 的其中一個：

* 使用 hello 指令碼 tooconfigure hello 報表伺服器
* 使用 Configuration Manager tooConfigure hello 報表伺服器。

如需詳細步驟，請參閱 hello 節[連接 toohello 虛擬機器並啟動 hello Reporting Services 組態管理員](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager)。

**驗證注意事項：** Windows 驗證是建議使用的驗證方法的 hello，而且它是 hello 預設 Reporting Services 的驗證。 Hello VM 所設定的使用者可以存取 Reporting Services，並且指派 tooReporting Services 角色。

### <a name="use-script-tooconfigure-hello-report-server-and-http"></a>使用指令碼 tooconfigure hello 報表伺服器和 HTTP
toouse hello Windows PowerShell 指令碼 tooconfigure hello 報表伺服器時，完成下列步驟的 hello。 hello 組態包含 HTTP，而不是 HTTPS:

1. 從 hello Azure 傳統入口網站，選取 hello VM，然後按一下 連線。 根據瀏覽器的設定，您可能會提示的 toosave.rdp 檔案，以連接 toohello VM。
   
    ![tooazure 虛擬機器連線](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) 使用 hello 使用者 VM 名稱、 使用者名稱和密碼建立 hello VM 時設定。 
   
    例如，在下列映像的 hello，hello VM 名稱是**ssrsnativecloud**而 hello 使用者名稱為**testuser**。
   
    ![登入包括 VM 名稱](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. 開啟 hello VM， **Windows PowerShell ISE**具有系統管理權限。 在 Windows server 2012 預設會安裝 PowerShell ISE hello。 建議您將使用 hello ISE 代替標準 Windows PowerShell 視窗，以便您可以將 hello 指令碼貼到 hello ISE，修改 hello 指令碼，然後再執行 hello 指令碼。
3. 在 Windows PowerShell ISE 中，按一下 hello**檢視**功能表，然後按一下**顯示指令碼窗格**。
4. 複製下列指令碼，hello hello 指令碼並貼到 hello Windows PowerShell ISE 指令碼窗格。
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change hello value if you used a different port for hello private HTTP endpoint when hello VM was created.
   
        ## Set PowerShell execution policy toobe able toorun scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. 如果您使用 80 以外的 HTTP 連接埠建立 hello VM，修改 hello 參數 $HTTPport = 80。
6. Reporting Services 目前是設定成 hello 指令碼。 如果您想 toorun hello 指令碼適用於 Reporting Services 時，修改 hello 路徑 toohello 命名空間的 hello 版本部分太"v11"，hello Get-wmiobject 陳述式。
7. 執行 hello 指令碼。

**驗證**: tooverify 正在 hello 報表伺服器基本功能，請參閱 hello[確認 hello 組態](#verify-the-configuration)本主題稍後的章節。

### <a name="use-script-tooconfigure-hello-report-server-and-https"></a>使用指令碼 tooconfigure hello 報表伺服器和 HTTPS
toouse Windows PowerShell tooconfigure hello 報表伺服器時，完成下列步驟的 hello。 hello 組態包含 HTTPS，而不是 HTTP。

1. 從 hello Azure 傳統入口網站，選取 hello VM，然後按一下 連線。 根據瀏覽器的設定，您可能會提示的 toosave.rdp 檔案，以連接 toohello VM。
   
    ![tooazure 虛擬機器連線](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) 使用 hello 使用者 VM 名稱、 使用者名稱和密碼建立 hello VM 時設定。 
   
    例如，在下列映像的 hello，hello VM 名稱是**ssrsnativecloud**而 hello 使用者名稱為**testuser**。
   
    ![登入包括 VM 名稱](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. 開啟 hello VM， **Windows PowerShell ISE**具有系統管理權限。 在 Windows server 2012 預設會安裝 PowerShell ISE hello。 建議您將使用 hello ISE 代替標準 Windows PowerShell 視窗，以便您可以將 hello 指令碼貼到 hello ISE，修改 hello 指令碼，然後再執行 hello 指令碼。
3. 執行指令碼，執行下列 Windows PowerShell 命令的 hello tooenable:
   
        Set-ExecutionPolicy RemoteSigned
   
    然後，您可以執行下列 tooverify hello 原則 hello:
   
        Get-ExecutionPolicy
4. 在**Windows PowerShell ISE**，按一下 hello**檢視**功能表，然後按一下**顯示指令碼窗格**。
5. 複製下列指令碼，並將它貼到 hello Windows PowerShell ISE 指令碼窗格中的 hello。
   
        ## This script configures hello report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when hello HTTPS endpoint was created.
   
        # You can run hello following command tooget (.cloudapp.net certificates) so you can copy hello thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # hello certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # hello certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If hello certificate is not a wildcard certificate, comment out hello following line, and enable hello full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "hello script will use $DNSNameAndPort as hello DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. 修改 hello **$certificatehash** hello 指令碼中的參數：
   
   * 這是 **必要** 參數。 如果您沒有儲存 hello 憑證值 hello 先前步驟中，使用其中一個 hello hello 憑證指紋的下列方法 toocopy hello 憑證雜湊值。:
     
       上 hello VM，開啟 Windows PowerShell ISE 並執行下列命令的 hello:
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       hello 輸出看起來類似 toohello 下列。 如果 hello 指令碼傳回空白行，hello VM 沒有憑證，例如設定，請參閱 hello 節[toouse hello 虛擬機器自我簽署憑證](#to-use-the-virtual-machines-self-signed-certificate)。
     
     或
   * 在 hello VM 執行 mmc.exe，然後再加入 hello**憑證**嵌入式管理單元。
   * 在 hello**受信任的根憑證授權單位**節點按兩下憑證名稱。 如果您使用 hello 的 hello VM 的自我簽署的憑證，hello 憑證 hello 的 hello VM 的 DNS 名稱來命名，並以結束**.cloudapp.net**。
   * 按一下 hello**詳細資料** 索引標籤。
   * 按一下 [指紋] 。 hello hello 指紋值欄位中所顯示 hello 詳細資料，例如 af 11 60 b6 4b 28 8 d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48
   * **Hello 指令碼執行之前**，移除 hello 配對值中間的 hello 空格。 例如 af1160b64b288d890a8212ff6ba9c3664f319048
7. 修改 hello **$httpsport**參數： 
   
   * 如果您使用連接埠 443 hello HTTPS 端點，然後您不需要 tooupdate hello 指令碼中的這個參數。 否則使用 hello hello VM 上設定 hello HTTPS 私用端點時，您選取的連接埠值。
8. 修改 hello **$DNSName**參數： 
   
   * hello 指令碼已針對萬用字元憑證 $DNSName ="+"。 如果您不想 tooconfigure 萬用字元憑證繫結，標記為註解 $DNSName ="+"和啟用下列行，hello $DNSNAme 完整參考，# # $DNSName="$server.cloudapp.net hello"。
     
       如果不想讓 Reporting Services 的 toouse hello 虛擬機器的 DNS 名稱，請變更 hello $DNSName 值。 如果您使用 hello 參數，hello 憑證也必須使用此名稱，並註冊的 DNS 伺服器上的全域 hello 名稱。
9. Reporting Services 目前是設定成 hello 指令碼。 如果您想 toorun hello 指令碼適用於 Reporting Services 時，修改 hello 路徑 toohello 命名空間的 hello 版本部分太"v11"，hello Get-wmiobject 陳述式。
10. 執行 hello 指令碼。

**驗證**: tooverify 正在 hello 報表伺服器基本功能，請參閱 hello[確認 hello 組態](#verify-the-connection)本主題稍後的章節。 tooverify hello 憑證繫結使用系統管理權限開啟命令提示字元並執行下列命令的 hello:

    netsh http show sslcert

hello 結果將包含 hello 下列：

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-tooconfigure-hello-report-server"></a>使用 Configuration Manager tooConfigure hello 報表伺服器
若不想使用 toorun hello PowerShell 指令碼 tooconfigure hello 報表伺服器，請遵循此節 toouse hello Reporting Services 原生模式組態管理員 tooconfigure hello 報表伺服器中的 hello 步驟。

1. 從 hello Azure 傳統入口網站，選取 hello VM，然後按一下 連線。 使用 hello 使用者名稱和密碼建立 hello VM 時設定。
   
    ![tooazure 虛擬機器連線](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. 執行 Windows update 並安裝更新 toohello VM。 如果需要 hello VM 重新啟動，重新啟動 hello VM，然後重新連線 toohello VM 從 hello Azure 傳統入口網站。
3. 從在 hello VM hello 開始功能表中，輸入**Reporting Services**並開啟**Reporting Services 組態管理員**。
4. 保留預設值 hello**伺服器名稱**和**報表伺服器執行個體**。 按一下 [ **連接**]。
5. 在 hello 左窗格中，按一下  **Web 服務 URL**。
6. 根據預設，RS 會設定為 HTTP 連接埠 80，而 IP 為全部指派。 tooadd HTTPS:
   
   1. 在**SSL 憑證**： 您想 toouse，例如 [VM 名稱] 選取 hello 憑證。.cloudapp.net。 如果未列出憑證，請參閱 hello 節**步驟 2： 建立伺服器憑證**如需有關如何 tooinstall 和信任 hello hello VM 上的憑證資訊。
   2. 在 [SSL 連接埠：] 下選擇 443。 如果您在 hello VM 不同的私用通訊埠設定 HTTPS 私用端點時，hello，此處使用該值。
   3. 按一下**套用**並等候 hello 作業 toocomplete。
7. 在 hello 左窗格中，按一下 **資料庫**。
   
   1. 按一下 [變更資料庫] 。
   2. 按一下 [建立新的報告伺服器資料庫]，然後按 [下一步]。
   3. 保留預設值，hello**伺服器名稱**: hello VM 名稱，並保留預設值，hello**驗證類型**為**目前使用者**–**整合式安全性**. 按一下 [下一步] 。
   4. 保留預設值，hello**資料庫名稱**為**ReportServer**按一下**下一步**。
   5. 保留預設值，hello**驗證類型**為**服務認證**按一下**下一步**。
   6. 按一下**下一步**上 hello**摘要**頁面。
   7. Hello 組態完成時，按一下**完成**。
8. 在 hello 左窗格中，按一下 **報表管理員 URL**。 保留預設值，hello**虛擬目錄**為**報表**按一下**套用**。
9. 按一下**結束**tooclose hello Reporting Services 組態管理員。

## <a name="step-4-open-windows-firewall-port"></a>步驟 4：開啟 Windows 防火牆連接埠
> [!NOTE]
> 如果您使用其中一個 hello 指令碼 tooconfigure hello 報表伺服器，您可以略過本節。 hello 指令碼包含的步驟 tooopen hello 防火牆連接埠。 hello 預設是連接埠 80 用於 HTTP 和 https 連接埠 443。
> 
> 

tooconnect 遠端 tooReport 管理員或 hello 報告上 hello VM 需要 hello 虛擬機器上的伺服器、 TCP 端點。 它是必要的 tooopen hello 相同的 hello VM 防火牆連接埠。 hello VM 佈建時，已建立 hello 端點。

本節提供如何 tooopen hello 防火牆連接埠上的基本資訊。 如需詳細資訊，請參閱 [為報告伺服器存取設定防火牆](https://technet.microsoft.com/library/bb934283.aspx)

> [!NOTE]
> 如果您使用 hello 指令碼 tooconfigure hello 報表伺服器，您可以略過本節。 hello 指令碼包含的步驟 tooopen hello 防火牆連接埠。
> 
> 

如果您針對 HTTPS 設定私用連接埠 443 以外時，修改下列指令碼適當的 hello。 tooopen 連接埠**443** hello Windows 防火牆，在完成 hello 下列：

1. 以系統管理權限開啟 Windows PowerShell 視窗。
2. 如果您使用 443 以外的通訊埠 hello VM 上設定 hello HTTPS 端點時，更新 hello hello 下列命令中的連接埠，然後執行 hello 命令：
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. Hello 命令完成時，**確定**hello 命令提示字元中顯示。

tooverify，hello 通訊埠已開啟，開啟 Windows PowerShell 視窗並執行下列命令的 hello:

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-hello-configuration"></a>確認 hello 組態
tooverify 現在使用 hello 報表伺服器基本功能，以系統管理權限開啟瀏覽器，然後瀏覽 toohello 下列報表伺服器和報表管理員 URL:

* 在 hello VM，瀏覽 toohello 報表伺服器 URL:
  
        http://localhost/reportserver
* 在 hello VM，瀏覽 toohello 報表管理員 URL:
  
        http://localhost/Reports
* 從本機電腦，瀏覽 toohello**遠端**hello VM 在報表管理員。 更新 hello hello 下列適當的範例中的 DNS 名稱。 出現提示時輸入密碼，請使用 hello hello VM 已佈建時所建立的系統管理員認證。 hello [Domain] 中的 hello 使用者名稱為\[使用者名稱] 格式，其中 hello 網域是 hello VM 電腦名稱，例如 ssrsnativecloud\testuser。 如果您不想要使用 HTTP**S**，移除 hello **s** hello URL 中。 在 VM 上建立額外的使用者，請參閱 hello 下一節的資訊。
  
        https://ssrsnativecloud.cloudapp.net/Reports
* 從本機電腦，瀏覽 toohello 遠端報表伺服器 URL。 更新 hello hello 下列適當的範例中的 DNS 名稱。 如果您未使用 HTTPS，移除 hello s hello URL 中。
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a>建立使用者和指派角色
設定和驗證 hello 報表伺服器之後，一般的管理工作是 toocreate 一或多個使用者，並將使用者指派 tooReporting Services 角色。 如需詳細資訊，請參閱 hello 下列：

* [建立本機使用者帳戶](https://technet.microsoft.com/library/cc770642.aspx)
* [授與使用者存取權 tooa 報表伺服器 （報表管理員）](https://msdn.microsoft.com/library/ms156034.aspx))
* [建立和管理角色指派](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate 和發行報表 toohello Azure 虛擬機器
hello 下表將摘要列出一些 hello Microsoft Azure 虛擬機器上裝載在內部部署電腦 toohello 報表伺服器中的 hello 選項可用 toopublish 現有報表：

* **RS.exe 指令碼**： 使用 RS.exe 指令碼 toocopy 報表項目從和現有的報表伺服器 tooyour Microsoft Azure 虛擬機器。 如需詳細資訊，請參閱 hello 節 「 原生模式 tooNative 模式 – Microsoft Azure 虛擬機器 」 中[Sample Reporting Services rs.exe 指令碼 tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx)。
* **報表產生器**: hello 虛擬機器包含 hello 按一下-click-once 版本的 Microsoft SQL Server 報表產生器。 toostart 報表產生器 hello hello 虛擬機器上的第一次：
  
  1. 以管理權限啟動瀏覽器。
  2. 瀏覽 tooreport 管理員 hello 虛擬機器上的，按一下**報表產生器**hello 功能區中。
     
     如需詳細資訊，請參閱 [安裝、解除安裝和支援報告產生器](https://technet.microsoft.com/library/dd207038.aspx)。
* **SQL Server Data Tools: VM**： 如果您建立 hello VM 與 SQL Server 2012，則 SQL Server Data Tools 安裝在 hello 虛擬機器上，而且可以是使用的 toocreate**報表伺服器專案**與 hello 虛擬報表機器。 SQL Server Data Tools 可以發佈 hello 報表 toohello hello 虛擬機器上的報表伺服器。
  
    如果您使用 SQL server 2014 建立 hello VM，您可以安裝 SQL Server Data Tools-BI for visual Studio。 如需詳細資訊，請參閱 hello 下列：
  
  * [Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=42313)
  * [Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843)
  * [SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* **SQL Server Data Tools：遠端**：在本機電腦上，以 SQL Server Data Tools 建立含有 Reporting Services 報告的 Reporting Services 專案。 設定 hello 專案 tooconnect toohello web 服務 URL。
  
    ![SSRS 專案的 ssdt 專案屬性](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* **使用指令碼**： 使用指令碼 toocopy 報表伺服器內容。 如需詳細資訊，請參閱[Sample Reporting Services rs.exe 指令碼 tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx)。

## <a name="minimize-cost-if-you-are-not-using-hello-vm"></a>如果您不想要使用 hello VM，將成本降至最低
> [!NOTE]
> toominimize 費用的 Azure 虛擬機器不在使用中，當關閉 hello VM 從 hello Azure 傳統入口網站。 如果您使用內部 hello VM 關閉 VM tooshut hello Windows 電源選項時，您仍會收取的 hello 相同數量的 hello VM。 tooreduce 費用，您需要 tooshut hello Azure 傳統入口網站中的 hello VM 關閉。 如果您不再需要 hello VM，請記住 toodelete hello VM 和 hello 相關聯的.vhd 檔案 tooavoid 儲存體費用。如需詳細資訊，請參閱 hello 常見問題集 > 一節[虛擬機器定價詳細資料](https://azure.microsoft.com/pricing/details/virtual-machines/)。

## <a name="more-information"></a>相關資訊
### <a name="resources"></a>資源
* 如需類似內容相關 tooa 單一伺服器部署的 SQL Server Business Intelligence 及 SharePoint 2013，請參閱[使用 Windows PowerShell tooCreate Azure VM 與 SQL Server BI 和 SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx)。
* 類似的內容相關 tooa 多重伺服器部署的 SQL Server Business Intelligence 及 SharePoint 2013，請參閱[部署 SQL Server Business Intelligence Azure 虛擬機器中](https://msdn.microsoft.com/library/dn321998.aspx)。
* 如需一般資訊相關的 toodeployments 的 SQL Server Business Intelligence Azure 虛擬機器中，請參閱[Azure 虛擬機器中 SQL Server Business Intelligence](virtual-machines-windows-classic-ps-sql-bi.md)。
* 如需 hello 成本的 Azure 計算費用，請參閱 hello 虛擬機器 索引標籤的[Azure 定價計算機](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines)。

### <a name="community-content"></a>社群內容
* 如需 toocreate Reporting Services 原生模式報表伺服器不使用指令碼的方式的逐步指示，請參閱[託管 SQL Reporting 服務在 Azure 虛擬機器](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html)。

### <a name="links-tooother-resources-for-sql-server-in-azure-vms"></a>在 Azure Vm 中的 SQL Server 的連結 tooother 資源
[Azure 虛擬機器上的 SQL Server 概觀](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

