---
title: "為 IPython Notebook 伺服器的 SQL Server 虛擬機器 aaaSet |Microsoft 文件"
description: "使用 SQL Server 和 IPython Server 來設定資料科學虛擬機器。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1fd6014a-d180-4558-b4eb-d9b5a331a99f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: ee83d1d5de671d9817c1bc1abd6b4f9c256dde8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-sql-server-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>將 Azure SQL Server 虛擬機器設定為 IPython Notebook 伺服器供進階分析使用
本主題說明如何 tooprovision 及設定 SQL Server 虛擬機器 toobe，做為雲端架構資料科學環境的一部分。 hello Windows 虛擬機器設定有支援 IPython 筆記型電腦、 Azure 儲存體總管 中，和 AzCopy，以及其他公用程式可用於資料科學專案之類的工具。 Azure 儲存體總管和 AzCopy，例如，提供方便的方式 tooupload 資料 tooAzure blob 儲存體從您的本機電腦或 toodownload 它 tooyour 從 blob 儲存體的本機電腦。

hello Azure 虛擬機器資源庫含有包含 Microsoft SQL Server 的數個映像。 選取適合您資料需求的 SQL Server VM 映像。 建議的映像如下：

* SQL Server 2012 SP2 Enterprise 的小型 toomedium 資料大小
* SQL Server 2012 SP2 Enterprise 針對最佳化資料倉儲工作量的大型 toovery 大型的資料大小
  
  > [!NOTE]
  > SQL Server 2012 SP2 Enterprise 的映像 **不包含資料磁碟**。 您將需要 tooadd 及/或將一或多個虛擬硬碟 toostore 附加您的資料。 當您建立 Azure 虛擬機器時，它擁有 hello 對應的作業系統 toohello C 磁碟機的磁碟和對應的暫存磁碟 toohello D 磁碟機的支援。 請勿使用 hello D 磁碟機 toostore 資料。 正如 hello 名，它會提供暫存儲存位置。 它並不提供備援或備份，因為它不在 Azure 儲存體內。
  > 
  > 

## <a name="Provision"></a>連接 toohello Azure 傳統入口網站並佈建 SQL Server 虛擬機器
1. 登入 toohello [Azure 傳統入口網站](http://manage.windowsazure.com/)使用您的帳戶。
   如果您沒有 Azure 帳戶，請造訪 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
2. 在 hello Azure 傳統入口網站，在 hello 左下方 hello 網頁上，按一下  **+ 新增**，按一下 **計算**，按一下 **虛擬機器**，然後按一下 **FROM組件庫**。
3. 在 hello**建立虛擬機器**頁面上，選取包含您資料的需求，為基礎的 SQL Server 的虛擬機器映像，然後按一下hello 右下方的 hello 頁面下一步箭頭。 Hello hello 上最新的資訊在 Azure 上支援 SQL Server 映像，請參閱[開始使用 Azure 虛擬機器中 SQL Server](http://go.microsoft.com/fwlink/p/?LinkId=294720)主題 hello [Azure 虛擬機器中 SQL Server](http://go.microsoft.com/fwlink/p/?LinkId=294719)文件集。
   
   ![選取 SQL Server VM][1]
4. 在 hello 上第一個**虛擬機器組態**頁面上，提供下列資訊：
   
   * 提供 [虛擬機器名稱] 。
   * 在 [hello**新的使用者名稱**] 方塊中，輸入唯一的使用者名稱 hello VM 本機系統管理員帳戶。
   * 在 hello**新密碼**方塊中，輸入強式密碼。 如需詳細資訊，請參閱 [增強式密碼](http://msdn.microsoft.com/library/ms161962.aspx)。
   * 在 hello**確認密碼**方塊中，重新輸入 hello 密碼。
   * 選取適當的 hello**大小**hello 從下拉式清單。
     
     > [!NOTE]
     > 在佈建期間指定 hello hello 虛擬機器大小： A2 是 hello 生產工作負載的建議的最小大小。 使用 SQL Server Enterprise Edition 時，虛擬機器的最小建議大小為 A3。 當您使用 SQL Server Enterprise Edition 時，請選取 A3 或以上的大小。 使用 SQL Server 2012 或 2014 Enterprise Optimized for Transactional Workloads 映像時，請選取 A4。
     > 使用 SQL Server 2012 或 2014 Enterprise Optimized for Data Warehousing Workloads 映像時，請選取 A7。 選取的 hello 大小限制您可以設定的資料磁碟數目。 最新，您可以連接 tooa 虛擬機器上可用的虛擬機器大小和資料磁碟數目 hello 資訊，請參閱[的 Azure 虛擬機器大小](http://msdn.microsoft.com/library/azure/dn197896.aspx)。 如需定價資訊，請參閱「 [虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/)」。
     > 
     > 
   
   按一下 下一步 hello hello 底部右 toocontinue 箭號。
   
   ![VM 組態][2]
5. 在 hello 第二個**虛擬機器組態**頁面上，設定網路功能、 儲存體和可用性的資源：
   
   * 在 hello**雲端服務**方塊中，選擇**建立新的雲端服務**。
   * 在 hello**雲端服務 DNS 名稱**方塊中，提供您選擇的 DNS 名稱的 hello 第一個部分，以便完成格式名稱**TESTNAME.cloudapp.net**
   * 在 hello**區域/同質群組/虛擬網路**方塊中，選取將託管這個虛擬映像的區域。
   * 在 hello**儲存體帳戶**，選取現有的儲存體帳戶，或選取 自動產生的一個。
   * 在 hello**可用性設定組**方塊中，選取**（無）**。
   * 閱讀並接受 hello 定價資訊。
6. 在 hello**端點**區段中，在 hello 底下的空白下拉式清單中按一下**名稱**，並選取**MSSQL**然後輸入 hello hello (的DatabaseEngine執行個體的連接埠號碼**1433年**hello 預設執行個體)。
7. 您的 SQL Server VM 也可以用來做為 IPython Notebook 伺服器 (將在稍後步驟中設定)。
   加入新端點 toospecify hello 連接埠 toouse 您 IPython 筆記型電腦的伺服器。 輸入的名稱在 hello**名稱**資料行中，選取您所選擇的 hello 公用連接埠的連接埠號碼並 9999 hello 私用連接埠。
   
   按一下 下一步 hello hello 底部右 toocontinue 箭號。
   
   ![選取 MSSQL 和 IPython 連接埠][3]
8. 接受預設值 hello**安裝 VM 代理程式**選取，然後按一下 hello 右下角的 hello 精靈 toocomplete hello VM 佈建程序中的 hello hello 核取記號。
   
   `![VM 的最後選項][4]
9. 等待 Azure 準備好您的虛擬機器。 預期 hello 虛擬機器狀態 tooproceed 透過：
   
   * 啟動中 (佈建中)
   * 已停止
   * 啟動中 (佈建中)
   * 執行中 (佈建中)
   * 執行中

## <a name="RemoteDesktop"></a>開啟 hello 虛擬機器使用遠端桌面並完成安裝
1. 佈建完成時，按一下您的虛擬機器 toogo toohello 儀表板頁面的 hello 名稱。 在 hello hello 頁面底部，按一下**連接**。
2. 選擇使用 hello Windows 遠端桌面程式 tooopen hello rpd 檔案 (`%windir%\system32\mstsc.exe`)。
3. 在 hello **Windows 安全性**對話方塊方塊中，您在前述步驟中指定的本機系統管理員帳戶提供 hello 的密碼。
   （您可能會要求 hello 虛擬機器的 tooverify hello 認證。）
4. hello 第一次登入 toothis 虛擬機器，數個程序可能需要 toocomplete，包括桌面、 Windows 更新和已完成的 hello Windows 初始設定工作 (sysprep) 的安裝程式。 待 Windows sysprep 完成後，SQL Server 安裝程式會完成組態工作。 在完成這些工作的期間，可能會造成幾分鐘的時間延遲。 `SELECT @@SERVERNAME`除非 SQL Server 安裝程式完成，且 SQL Server Management Studio 可能無法在 hello 開始頁面上可見，可能傳回 hello 正確的名稱。

當您使用 Windows 遠端桌面連線的 toohello 虛擬機器，hello 虛擬機器的運作方式就像是任何其他電腦。 連接 toohello 預設執行個體的 SQL Server 與 SQL Server Management Studio （hello 虛擬機器上執行） 在 hello 一般的方式。

## <a name="InstallIPython"></a>安裝 IPython Notebook 和其他支援工具
tooconfigure 您新的 SQL Server VM tooserve 做為 IPython Notebook 伺服器，並安裝其他支援工具這類 AzCopy、 Azure 儲存體總管、 有用的資料科學 Python 封裝和其他人、 tooyou 提供特殊的自訂指令碼。 tooinstall:

1. 以滑鼠右鍵按一下 hello **Windows 啟動**圖示，然後按一下**命令提示字元 （管理員）**
2. 複製下列命令的 hello 並貼在 hello 命令提示字元。
  
        set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'
        @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"
3. 出現提示時，輸入 hello IPython Notebook 伺服器您選擇的密碼。
4. hello 自訂指令碼會自動執行數個後續安裝程序，包括：
    * 安裝和設定 IPython Notebook 伺服器
    * Hello hello 端點稍早建立的 Windows 防火牆中開啟 TCP 連接埠：
    * 適用於 SQL Server 遠端連線
    * 適用於 IPython Notebook 伺服器遠端連線
    * 擷取 IPython Notebook 範例和 SQL 指令碼
    * 下載並安裝實用的資料科學 Python 封裝
    * 下載並安裝 Azure 工具，例如 AzCopy 和 Azure 儲存體總管  
    <br>
5. 您可能會存取，並從使用 URL hello 表單的任何本機或遠端瀏覽器執行 IPython 筆記型電腦`https://<virtual_machine_DNS_name>:<port>`，其中連接埠是 hello IPython 公用連接埠選取佈建 hello 虛擬機器時。
6. IPython 筆記型電腦伺服器做為背景服務正在執行，並重新啟動 hello 虛擬機器時自動啟動。

## <a name="Optional"></a>視需要連接資料磁碟
如果您的 VM 映像不包含資料磁碟，亦即，不是 C 磁碟機 （作業系統磁碟） 和 D 磁碟機 （暫存磁碟），磁碟需要 tooadd 其中一個或多個資料磁碟 toostore 您的資料。 針對 SQL Server 2012 SP2 Enterprise 針對最佳化資料倉儲工作量 hello VM 映像隨附預先設定的 SQL Server 資料和記錄檔的其他磁碟。

> [!NOTE]
> 請勿使用 hello D 磁碟機 toostore 資料。 正如 hello 名，它會提供暫存儲存位置。 它並不提供備援或備份，因為它不在 Azure 儲存體內。
> 
> 

tooattach 額外資料磁碟，請依照下列中所述的 hello 步驟[如何 tooAttach Windows 虛擬機器的資料磁碟 tooa](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)，它將引導您完成：

1. 附加空磁碟 toohello 虛擬機器在先前步驟中佈建
2. Hello hello 虛擬機器中的新磁碟的初始化

## <a name="SSMS"></a>連接 tooSQL Server Management Studio 並啟用混合的模式驗證
hello SQL Server Database Engine 無法使用 Windows 驗證，若沒有網域環境。 tooconnect toohello Database Engine 從另一部電腦，設定 SQL Server 混合的模式驗證。 混合模式驗證可允許 SQL Server 驗證和 Windows 驗證。 SQL 驗證模式需要直接從您的 SQL Server VM 的資料庫中的訂單 tooingest 資料[Azure Machine Learning Studio](https://studio.azureml.net)使用 hello 資料匯入模組。

1. 使用遠端桌面連線的 toohello 虛擬機器，同時使用 hello Windows**搜尋**窗格和型別**SQL Server Management Studio** (SMSS)。 按一下 toostart hello SQL Server Management Studio (SSMS)。 您可能想在桌面上的捷徑 tooSSMS tooadd 供未來使用。
   
   ![啟動 SSMS][5]
   
   hello 第一次開啟 Management Studio，就必須建立 hello 使用者 Management Studio 環境。 這可能需要花費幾分鐘的時間。
2. Management Studio 開啟時，顯示 hello**連接 tooServer**  對話方塊。 在 hello**伺服器名稱** 方塊中，輸入 hello 名稱的 hello 虛擬機器 tooconnect toohello hello 物件總管 中使用 Database Engine。
   (而不是 hello 虛擬機器名稱您也可以使用**（本機）**或單一句號當做 hello**伺服器名稱**。 選取**Windows 驗證**，並將保留***您\_VM\_名稱*\\您\_本機\_系統管理員**在 hello**使用者名**方塊。 按一下 [ **連接**]。
   
   ![連接 tooServer][6]
   
   <br>
   
   > [!TIP]
   > 您可以變更 hello 的 SQL Server 驗證模式使用 Windows 登錄機碼變更，或使用 SQL Server Management Studio hello。 toochange 驗證模式使用 hello 登錄機碼變更，開始**新查詢**並執行下列指令碼的 hello:
   > 
   > 
   
       USE master
       go
   
       EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', N'Software\Microsoft\MSSQLServer\MSSQLServer', N'LoginMode', REG_DWORD, 2
       go

    使用 SQL Server management Studio toochange hello 驗證模式：

1. 在**SQL Server Management Studio 物件總管**hello 的 SQL Server （hello 虛擬機器名稱） 的執行個體名稱上按一下滑鼠右鍵，然後按**屬性**。
   
   ![伺服器屬性][7]
2. Hello 上**安全性**頁面的 **伺服器驗證**，選取**SQL Server 及 Windows 驗證模式**，然後按一下**確定**.
   
   ![選取驗證模式][8]
3. 在 hello **SQL Server Management Studio**對話方塊中，按一下 **確定**確認 hello 需求 toorestart SQL Server。
4. 在 物件總管 中，以滑鼠右鍵按一下伺服器，然後按一下重新啟動。 (如果 SQL Server Agent 處於執行狀態，您也必須將其重新啟動。)
   
   ![重新啟動][9]
5. 在 hello **SQL Server Management Studio**對話方塊中，按一下**是**同意要 toorestart SQL Server。

## <a name="Logins"></a>建立 SQL Server 驗證登入
tooconnect toohello Database Engine 從另一部電腦，您必須建立至少一個 SQL Server 驗證登入。  

您也可以透過程式設計方式建立新的 SQL Server 登入，或使用 hello SQL Server Management Studio。 以程式設計的方式，開始使用 SQL 驗證新的系統管理員使用者 toocreate**新查詢**並執行下列指令碼的 hello。 使用您選擇的「使用者名稱」和「密碼」取代 <新使用者名稱\> 和 <新密碼\>。 

    USE master
    go

    CREATE LOGIN <new user name> WITH PASSWORD = N'<new password>',
        CHECK_POLICY = OFF,
        CHECK_EXPIRATION = OFF;

    EXEC sp_addsrvrolemember @loginame = N'<new user name>', @rolename = N'sysadmin';


視需要調整 hello 密碼原則 （hello 範例程式碼會關閉原則檢查和密碼到期日）。 如需 SQL Server 登入的詳細資訊，請參閱 [建立登入](http://msdn.microsoft.com/library/aa337562.aspx)。  

toocreate 新 SQL Server 登入使用 SQL Server Management Studio hello:

1. 在**SQL Server Management Studio 物件總管**，展開您想在其中 toocreate hello 新登入的 hello 伺服器執行個體的 hello 資料夾。
2. 以滑鼠右鍵按一下 hello**安全性**資料夾中，點太**新增**，然後選取**登入...**.
   
   ![新增登入][10]
3. 在 hello**登入-新增** 對話方塊上 hello**一般**頁面上，輸入 hello hello 新使用者名稱中 hello**登入名稱**方塊。
4. 選取 [SQL Server 驗證] 。
5. 在 hello**密碼**方塊中，輸入 hello 新使用者的密碼。 該密碼一次輸入 hello**確認密碼**方塊。
6. 選取的複雜性和強制，tooenforce 密碼原則選項**強制執行密碼原則**（建議選項）。 此為選取 SQL Server 驗證時的預設選項。
7. 選取的到期日 tooenforce 密碼原則選項**強制執行密碼逾期**（建議選項）。 強制執行密碼原則必須 tooenable 選取此核取方塊。 此為選取 SQL Server 驗證時的預設選項。
8. 選取 使用新密碼 hello 第一次登入之後，tooforce hello 使用者 toocreate**使用者必須變更密碼，在下次登入時**（建議使用此登入是否有人 else toouse。 如果 hello 登入是供自己使用，請勿選取此選項。）強制執行密碼逾期必須 tooenable 選取此核取方塊。 此為選取 SQL Server 驗證時的預設選項。
9. 從 hello**預設資料庫**清單中，選取 hello 登入的預設資料庫。 **主要**hello 預設值，這個選項。 如果您尚未建立使用者資料庫，將這個資料集太**主要**。
10. 在 hello**預設語言**清單中，保留**預設**hello 值。
    
    ![登入屬性][11]
11. 如果這是您要建立 hello 第一個登入，您可能想要將此登入指定為 SQL Server 系統管理員。 如果是的話，請在 [伺服器角色] 頁面中勾選 [系統管理員 (sysadmin)]。
    
    > [!IMPORTANT]
    > Hello sysadmin 固定伺服器角色的成員擁有 hello Database Engine 的完整控制權。 基於安全性理由，請謹慎限制此角色的成員資格。
    > 
    > 
    
    ![系統管理員 (sysadmin)][12]
12. 按一下 [確定]。

## <a name="DNS"></a>判斷 hello hello 虛擬機器的 DNS 名稱
tooconnect toohello SQL Server Database Engine 從另一部電腦，您必須知道 hello 網域名稱系統 (DNS) hello 虛擬機器的名稱。

（這是 hello 名稱 hello 網際網路使用 tooidentify hello 虛擬機器。 您可以使用 hello IP 位址，但當 Azure 基於冗餘或維護移動資源時，可能會變更 hello IP 位址。 hello DNS 名稱將會是穩定，因為它可能會重新導向 tooa 新的 IP 位址。)

1. 在 hello Azure 傳統入口網站 （或從 hello 上一個步驟），選取**虛擬機器**。
2. 在 [hello**虛擬機器執行個體**] 頁面的 hello **DNS 名稱**hello 虛擬機器會出現的資料行中，尋找並複製 hello DNS 名稱前面加上**http://**。 （hello 使用者介面可能不會顯示 hello 完整名稱，但您可以以滑鼠右鍵按一下它，然後選取 複製）。

## <a name="cde"></a>從另一部電腦連接 toohello Database Engine
1. 在電腦上連接 toohello 網際網路上，開啟 SQL Server Management Studio。
2. 在 hello**連接 tooServer**或**連接 tooDatabase 引擎**對話方塊中的，在 hello**伺服器名稱**方塊中，輸入虛擬機器 （決定 hello hello DNS 名稱前一項工作） 和公用端點連接埠號碼格式的 hello *DNSName，portnumber*例如**tutorialtestVM.cloudapp.net,57500**。
3. 在 hello**驗證**方塊中，選取**SQL Server 驗證**。
4. 在 hello**登入**中，輸入您在稍早的工作中建立登入的 hello 名稱。
5. 在 [hello**密碼**] 方塊中，輸入 hello 密碼 hello 登入您在稍早的工作中建立。
6. 按一下 [ **連接**]。

## <a name="amlconnect"></a>從 Azure Machine Learning 連接 toohello Database Engine
在稍後階段 hello 小組資料科學程序，您將使用 hello [Azure Machine Learning Studio](https://studio.azureml.net) toobuild 和部署的機器學習模型。 從您的 SQL Server VM 的資料庫直接在 Azure Machine Learning 定型或計分，tooingest 資料使用 hello**匯入資料**模組中新[Azure Machine Learning Studio](https://studio.azureml.net)實驗。 本主題涵蓋更多詳細資料，透過 hello 小組資料科學程序指南的連結。 如需簡介，請參閱「 [什麼是 Azure Machine Learning Studio？」](machine-learning-what-is-ml-studio.md)。

1. 在 hello**屬性**窗格中的 hello[資料匯入模組](https://msdn.microsoft.com/library/azure/dn905997.aspx)，選取**Azure SQL Database**從 hello**資料來源**下拉式清單中。
2. 在 hello**資料庫伺服器名稱**文字方塊中，輸入`tcp:<DNS name of your virtual machine>,1433`
3. 輸入 hello SQL 使用者名稱中 hello**伺服器使用者帳戶名稱**文字方塊。
4. 輸入 hello sql 使用者密碼在 hello**伺服器使用者帳戶密碼**文字方塊。
   
   ![Azure Machine Learning 匯入資料][13]

## <a name="shutdown"></a>關閉並解除配置非使用中的虛擬機器
Azure 虛擬機器的定價策略是「 **只針對您使用的項目進行付費**」。 不會的 tooensure 時不使用虛擬機器，則需要付費，它具有 toobe 中的 hello**已停止 （取消配置）**狀態。

> [!NOTE]
> 正在關閉 hello 虛擬機器從位於內部 （使用 Windows 電源選項），hello VM 已停止，但會維持配置。 您不收費，tooensure 一律停止虛擬機器從 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)。 您也可以停止 hello VM 透過 Powershell 太"PostShutdownAction 」 等呼叫 ShutdownRoleOperation"StoppedDeallocated"。
> 
> 

tooshutdown 及取消配置 hello 虛擬機器：

1. 登入 toohello [Azure 傳統入口網站](http://manage.windowsazure.com/)使用您的帳戶。  
2. 選取**虛擬機器**從 hello 左側的導覽列。
3. 在 hello 清單中的虛擬機器，按一下您的虛擬機器，然後移 toohello hello 名稱**儀表板**頁面。
4. 在 hello hello 頁面底部，按一下**關機**。

![VM 關閉][15]

hello 虛擬機器將會取消配置，但是不會刪除。 您可以隨時從 hello Azure 傳統入口網站，以重新啟動您的虛擬機器。

## <a name="your-azure-sql-server-vm-is-ready-toouse-whats-next"></a>Azure SQL Server VM 已準備好 toouse： 後續步驟？
您的虛擬機器就準備好在您的資料科學練習 toouse。 也可以使用 IPython Notebook 伺服器 hello 瀏覽和處理的資料，以及其他工作搭配使用 Azure 機器學習和 hello 小組資料科學程序 (TDSP) hello 虛擬機器。

hello hello 資料科學程序中的下一個步驟中的對應 hello[資料科學的小組流程](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)，而且可能包括將資料移入 HDInsight，程序、 範例它那里與 Azure 機器學習 hello 資料的準備步驟了解。

[1]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/selectsqlvmimg.png
[2]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/4vm-config.png
[3]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/sqlvmports.png
[4]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmpostopts.png
[5]:./media/machine-learning-data-science-setup-sql-server-virtual-machine/searchssms.png
[6]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/19connect-to-server.png
[7]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/20server-properties.png
[8]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/21mixed-mode.png
[9]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/22restart2.png
[10]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/23new-login.png
[11]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/24test-login.png
[12]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/25sysadmin.png
[13]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/amlreader.png
[15]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmshutdown.png

