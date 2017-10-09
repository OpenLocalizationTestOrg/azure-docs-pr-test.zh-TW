---
title: "SQL Server 虛擬機器 aaaProvision |Microsoft 文件"
description: "建立並使用 hello 入口網站在 Azure 中的 tooa SQL Server 虛擬機器連線。 本教學課程使用 hello Resource Manager 模式。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
editor: 
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: jroth
experimental_id: a641df96-f27d-40
ms.openlocfilehash: aaad422d6ed47f5ca00b1ef484ac270a58e24f99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-hello-azure-portal"></a>佈建 hello Azure 入口網站中的 SQL Server 虛擬機器
> [!div class="op_single_selector"]
> * [入口網站](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
> 
> 

此端對端教學課程會示範如何 toouse 會 hello Azure 入口網站 tooprovision 執行 SQL Server 的虛擬機器。

hello Azure 虛擬機器 (VM) 映像庫含有包含 Microsoft SQL Server 的數個映像。 按幾下，您可以選取其中一個 hello SQL VM 映像從 hello 組件庫，並佈建 Azure 環境中。

在本教學課程中，您將：

* [從 hello 庫中選取的 SQL VM 映像](#select-a-sql-vm-image-from-the-gallery)
* [設定並建立 hello VM](#configure-the-vm)
* [使用遠端桌面開啟 hello VM](#open-the-vm-with-remote-desktop)
* [從遠端連線 tooSQL 伺服器](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-hello-gallery"></a>從 hello 庫中選取的 SQL VM 映像
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)使用您的帳戶。

   > [!NOTE]
   > 如果您沒有 Azure 帳戶，請造訪 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。

2. 在 hello Azure 入口網站，按一下 **新增**。 hello 入口網站開啟 hello**新增**刀鋒視窗。 hello SQL Server VM 資源位於 hello**計算**hello Marketplace 的群組。
3. 在 hello**新增**刀鋒視窗中，按一下 **計算**，然後按一下**查看所有**。
4. 在 hello**篩選**文字方塊中，輸入 SQL Server，然後按下 hello ENTER 鍵。

   ![Azure 虛擬機器刀鋒視窗](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. 檢閱 hello 可用的 SQL Server 映像。 每個映像皆識別一個 SQL Server 版本和一個作業系統。 
6. 選取 SQL Server 2016 SP1 開發人員在 Windows Server 2016 上 hello 映像。

   > [!TIP]
   > hello Developer edition 會使用在本教學課程中，因為它是免費提供給開發測試用途的 SQL server 完整版本。 您需支付只執行 hello VM hello 成本。

   > [!NOTE]
   > SQL VM 映像併入 hello 授權成本 for SQL Server hello 每分鐘定價的 hello （除了 hello developer Edition 和 Express edition) 您建立的 VM。 SQL Server Developer 免費供開發/測試 (非生產環境) 使用，SQL Express 免費供輕量型工作負載 (少於 1GB 記憶體、小於 10 GB 儲存體) 使用。
   > 還有另一個選項 toobring 您-擁有的授權 (BYOL) 和 hello VM 工資。 這些映像的名稱前面會有 {BYOL}。 如需這些選項的詳細資訊，請參閱 [SQL Server Azure VM 的定價指導方針](virtual-machines-windows-sql-server-pricing-guidance.md)。

7. 在 [選取部署模型] 底下，確認已選取 [Resource Manager]。 資源管理員是 hello 建議新的虛擬機器的部署模型。 按一下 [建立] 。

    ![使用 Resource Manager 建立 SQL VM](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-hello-vm"></a>設定 hello VM
有五個刀鋒視窗可用來設定 SQL Server 虛擬機器。

| 步驟 | 說明 |
| --- | --- |
| **基本概念** |[設定基本設定](#1-configure-basic-settings) |
| **大小** |[選擇虛擬機器大小](#2-choose-virtual-machine-size) |
| **設定** |[設定選用功能](#3-configure-optional-features) |
| **SQL Server 設定** |[進行 SQL Server 設定](#4-configure-sql-server-settings) |
| **摘要** |[檢閱 hello 摘要](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a>1.設定基本設定
在 hello**基本概念**刀鋒視窗中，提供下列資訊的 hello:

* 輸入唯一的虛擬機器 [名稱] 。
* 指定**使用者名**hello hello VM 上的本機系統管理員帳戶。 此帳戶也會加入 SQL Server toohello **sysadmin**固定的伺服器角色。
* 提供強式 [密碼] 。
* 如果您有多個訂閱，請確認 hello 訂用帳戶的正確 hello 新的 VM。
* 在 hello**資源群組**方塊中，輸入新的資源群組的名稱。 或者，toouse 現有的資源群組按一下**使用現有**。 資源群組是 Azure (虛擬機器、儲存體帳戶、虛擬網路等) 中相關資源的集合。
  
  > [!NOTE]
  > 如果您只是測試或了解 Azure 中的 SQL Server 部署，使用新的資源群組很有幫助。 完成測試之後，刪除 hello 資源群組 tooautomatically 刪除 hello VM 和資源群組相關聯的所有資源。 如需有關資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../../azure-resource-manager/resource-group-overview.md)。
  > 
  > 
* 選取此部署的 [位置]  。
* 按一下**確定**toosave hello 設定。
  
    ![SQL 基本概念刀鋒視窗](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a>2.選擇虛擬機器大小
在 hello**大小**步驟中，虛擬機器大小選擇 「 hello 中**大小選擇 「**刀鋒視窗。 hello 刀鋒視窗一開始會顯示您所選取的 hello 映像為基礎的建議的機器大小。

> [!IMPORTANT]
> hello 估計 hello 上顯示的每月成本**大小選擇 「**刀鋒視窗中不包含 SQL Server 授權成本。 此預估每月成本是單獨的 VM hello hello 成本。 Hello Express 和 Developer edition 的 SQL Server，這是 hello 總估計的成本。 對於其他版本，請參閱 hello [Windows 虛擬機器定價頁面](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)並選取您目標的 SQL Server 版本。 另請參閱 hello[定價指導方針 SQL Server 的 Azure Vm](virtual-machines-windows-sql-server-pricing-guidance.md)。

![SQL VM 大小選項](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

針對生產工作負載，建議選取可支援 [進階儲存體](../../../storage/storage-premium-storage.md)的虛擬機器大小。 如果您不需要該層級的效能，使用 hello**檢視所有**按鈕，顯示所有機器的大小選項。 例如，您可能會將較小的機器使用開發或測試環境。

> [!NOTE]
> 如需關於虛擬機器大小的詳細資訊，請參閱[虛擬機器大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 如需有關 SQL Server VM 大小的考量，請參閱 [Azure 虛擬機器中的 SQL Server 效能最佳作法](virtual-machines-windows-sql-performance.md)。

選擇您的機器大小，然後按一下選取 。

## <a name="3-configure-optional-features"></a>3.設定選用功能
在 hello**設定**刀鋒視窗中，設定 Azure 儲存體、 網路功能與監視 hello 虛擬機器。

* 在 [儲存體] 底下，指定 [標準] 或 [進階 (SSD)] 的 [磁碟類型]。 針對生產環境工作負載，建議使用進階儲存體。

> [!NOTE]
> 如果您對不支援進階儲存體的機器大小選取 [進階 (SSD)]，您的機器大小會自動變更。  
> 
> 

* 在下**儲存體帳戶**，您可以接受 hello 自動佈建儲存體帳戶名稱。 您也可以按一下**儲存體帳戶**toochoose 現有帳戶並設定 hello 儲存體帳戶類型。 Azure 預設會建立具有本地備援儲存體的新儲存體帳戶。 如需儲存體選項的詳細資訊，請參閱 [Azure 儲存體複寫](../../../storage/storage-redundancy.md)。
* 在下**網路**，您可以接受 hello 自動填入值。 您也可以按一下每個功能 toomanually 設定 hello**虛擬網路**，**子網路**，**公用 IP 位址**，和**網路安全性群組**. 基於 hello 本教學課程中，保留 hello 預設值。
* Azure 可讓**監視**預設與 hello hello VM 為指定的相同儲存體帳戶。 您可以在這裡變更這些設定。
* 在 [可用性設定組] 底下，指定可用性設定組。 基於 hello 本教學課程，您可以選取**無**。 如果您計劃 tooset SQL AlwaysOn 可用性群組上的，設定 hello 可用性 tooavoid 重建 hello 虛擬機器。  如需詳細資訊，請參閱[管理 hello 虛擬機器可用性](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

完成這些設定時，請按一下 [確定] 。

## <a name="4-configure-sql-server-settings"></a>4.進行 SQL Server 設定
在 hello **SQL Server 設定**刀鋒視窗中，設定特定的設定和針對 SQL Server 最佳化。 您可以設定 SQL Server 的 hello 設定包括下列設定的 hello。

| 設定 |
| --- |
| [連線能力](#connectivity) |
| [驗證](#authentication) |
| [儲存體組態](#storage-configuration) |
| [自動修補](#automated-patching) |
| [自動備份](#automated-backup) |
| [Azure 金鑰保存庫整合](#azure-key-vault-integration) |
| [R 服務](#r-services) |

### <a name="connectivity"></a>連線能力
在下**SQL 連接性**，指定 hello 類型要 toohello 這部 vm 的 SQL Server 執行個體的存取。 基於 hello 本教學課程中，選取**公用 （網際網路）**從機器或服務上的 tooallow 連線 tooSQL 伺服器 hello 網際網路。 選取此選項，Azure 會自動設定 hello 防火牆與 hello 網路安全性的群組 tooallow 流量通訊埠 1433年。  

![SQL 連線選項](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

tooconnect tooSQL 伺服器 hello 透過網際網路，您也必須啟用 SQL Server 驗證，hello 下一節中所述。

> [!NOTE]
> 它是可能 tooadd hello 網路通訊 tooyour SQL Server VM 的更多限制。 建立 hello VM 之後，您可以加入更多的限制所編輯的 hello 網路安全性群組。 如需詳細資訊，請參閱 [什麼是網路安全性群組 (NSG)？](../../../virtual-network/virtual-networks-nsg.md)
> 
> 

如果您希望 Database Engine toonot 啟用連線 toohello 透過 hello 網際網路，選擇其中一個 hello 下列選項：

* **（在 VM 只) 內本機**tooallow 連線 tooSQL 只能從伺服器 hello VM 內。
* **（在虛擬網路） 內的私用**從機器或服務在 hello tooallow 連線 tooSQL 伺服器相同的虛擬網路。

> [!NOTE]
> 適用於 SQL Server Express edition 的 hello 虛擬機器映像不會自動啟用 hello TCP/IP 通訊協定。 這是即使的 hello 公用與私人連線，則為 true 的選項。 Express 版本中，您必須用於 SQL Server 組態管理員太[手動啟用 hello TCP/IP 通訊協定](#configure-sql-server-to-listen-on-the-tcp-protocol)之後建立 hello VM。
> 
> 

一般情況下，選擇 hello 限制最嚴格連線能力，可讓您的案例來改善安全性。 但所有 hello 選項都會透過網路安全性群組規則和 SQL/Windows 驗證安全性實體。

**連接埠**too1433 預設值。 您可以指定其他連接埠號碼。
如需詳細資訊，請參閱[連接 tooa SQL Server 虛擬機器 （資源管理員） |Microsoft Azure](virtual-machines-windows-sql-connect.md)。

### <a name="authentication"></a>驗證
如果您需要「SQL Server 驗證」，請按一下 [SQL 驗證]  under 。

![SQL Server 驗證](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> 如果您打算 tooaccess SQL Server 透過 hello 網際網路 (也就是 hello 公用連線選項)，您必須啟用 SQL 驗證這裡。 SQL Server 的公用存取 toohello 需要 hello 使用 SQL 驗證。
> 
> 

如果您啟用 [SQL Server 驗證]，請指定 [登入名稱] 和 [密碼]。 這個使用者名稱設定為 SQL Server 驗證登入和成員的 hello **sysadmin**固定的伺服器角色。 如需驗證模式的詳細資訊，請參閱[選擇驗證模式](http://msdn.microsoft.com/library/ms144284.aspx)。

如果您未啟用 SQL Server 驗證，然後您就可以使用本機系統管理員帳戶 hello hello VM tooconnect toohello SQL Server 執行個體上。

### <a name="storage-configuration"></a>儲存體組態
按一下**儲存體設定**toospecify hello 存放裝置需求。

![SQL 儲存體組態](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> 如果您選取 [標準] 儲存體，則無法使用此選項。 自動儲存體最佳化只適用於進階儲存體。
> 
> 

您可以用每秒輸入/輸出作業數 (IOPs)、輸送量 (單位為 MB/s) 及總儲存體大小來指定需求。 使用 hello 滑動縮放比例，以設定這些值。 hello 入口網站會自動計算 hello 根據這些需求的磁碟數目。

根據預設，Azure hello 儲存體最佳化 5000 IOPs、 200 Mb，和 1 TB 的儲存空間。 您可以根據工作負載變更這些儲存體設定。 在下**針對儲存體最佳化**，選取其中一個 hello 下列選項：

* **一般**hello 預設設定，並且支援大部分的工作負載。
* **交易式**傳統資料庫 OLTP 工作負載的 hello 儲存體的處理最佳化。
* **資料倉儲**hello 儲存體分析和報告工作負載最佳化。

> [!NOTE]
> hello hello 滑桿上方限制是根據您選取的虛擬機器的大小而有所不同。
> 
> 

### <a name="automated-patching"></a>自動修補
**Automated patching** 。 自動修補允許 Azure tooautomatically 修補 SQL Server 和 hello 作業系統。 指定一天的 hello 週、 時間和維護期間的持續時間。 Azure 會在此維護期間執行修補。 hello 維護窗口排程會為時間使用 hello VM 地區設定。 如果不想使用 Azure tooautomatically 修補 SQL Server 和 hello 作業系統，請按一下**停用**。  

![SQL 自動修補](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 自動修補](virtual-machines-windows-sql-automated-patching.md)。

### <a name="automated-backup"></a>自動備份
在 [自動備份] 底下，可以為所有資料庫啟用自動資料庫備份。 預設會停用自動備份。

當您啟用 SQL 自動的備份時，您可以設定下列設定的 hello:

* 備份的保留期限 (天數)
* 備份的儲存體帳戶 toouse
* 備份的加密選項和密碼
* 備份系統資料庫
* 設定備份排程

tooencrypt hello 備份、 按一下**啟用**。 然後指定 hello**密碼**。 Azure 會建立憑證 tooencrypt hello 備份，並使用 hello 指定密碼 tooprotect 該憑證。

![SQL 自動備份](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 如需詳細資訊，請參閱 [Azure 虛擬機器中 SQL Server 的自動化備份](virtual-machines-windows-sql-automated-backup.md)。

### <a name="azure-key-vault-integration"></a>Azure 金鑰保存庫整合
按一下 toostore 安全性密碼，在 Azure 中的進行加密， **Azure 金鑰保存庫整合**按一下**啟用**。

![SQL Azure 金鑰保存庫整合](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

hello 下表列出 hello 參數需要的 tooconfigure Azure 金鑰保存庫整合。

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| **金鑰保存庫 URL** |hello hello 金鑰保存庫位置。 |https://contosokeyvault.vault.azure.net/ |
| **主體名稱** |Azure Active Directory 服務主體名稱。 此名稱也是參考的 tooas hello 用戶端識別碼。 |fde2b411-33d5-4e11-af04eb07b669ccf2 |
| **主體密碼** |Azure Active Directory 服務主體密碼。 這個密碼也會參照的 tooas hello 用戶端密碼。 |9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM= |
| **認證名稱** |**認證名稱**: AKV 整合建立 SQL Server，讓 hello VM toohave 存取 toohello 金鑰保存庫中的認證。 選擇此認證的名稱。 |mycred1 |

如需詳細資訊，請參閱 [在 Azure VM 上設定 SQL Server 的 Azure 金鑰保存庫整合](virtual-machines-windows-ps-sql-keyvault.md)。

完成 SQL Server 設定之後，請按一下 [確定] 。

### <a name="r-services"></a>R 服務
您可以啟用 [SQL Server R 服務](https://msdn.microsoft.com/library/mt604845.aspx)。 SQL Server R Services 可讓您使用 SQL Server 2016 toouse 進階分析。 按一下**啟用**上 hello **SQL Server 設定**刀鋒視窗。

![啟用 SQL Server R 服務](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)


## <a name="5-review-hello-summary"></a>5.檢閱 hello 摘要
在 hello**摘要**刀鋒視窗中，檢閱 hello 摘要，並按一下**確定** toocreate SQL Server、 資源群組和資源指定此 vm。

您可以監視 hello 部署從 hello azure 入口網站。 hello**通知**在 hello 囉 」 畫面最上方的按鈕會顯示 hello 部署的基本狀態。

> [!NOTE]
> tooprovide 與了解部署時間，我以預設設定部署的 SQL VM toohello 美東地區。 此測試部署花費了 26 分鐘 toocomplete 總數。 但是根據您的區域和選取的設定，您可能會經歷較快或較慢的部署時間。
> 
> 

## <a name="open-hello-vm-with-remote-desktop"></a>使用遠端桌面開啟 hello VM
使用下列步驟 tooconnect toohello 虛擬機器使用遠端桌面的 hello:

1. 建立 Azure VM 的 hello hello hello 圖示 VM 就會出現 Azure 儀表板上。 瀏覽現有的虛擬機器，也可以找到它。 按一下新的 SQL 虛擬機器。 [虛擬機器]  刀鋒視窗會顯示您的虛擬機器詳細資料。
2. 頂端的 hello hello**虛擬機器**刀鋒視窗中，按一下 **連接**。
3. hello 瀏覽器下載 hello VM 的 RDP 檔案。 開啟 hello RDP 檔案。
    ![遠端桌面 tooSQL VM](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-remote-desktop.png)
4. hello 遠端桌面連線會通知您該 hello 無法識別此遠端連線的發行者。 按一下**連接**toocontinue。
5. 在 hello **Windows 安全性** 對話方塊中，按一下 **使用其他帳戶**。
6. 如**使用者名**類型**\<使用者名稱 >**，其中<user name>是您指定當您設定 hello VM hello 使用者名稱。 您有 tooadd hello 名稱之前初始反斜線。
7. 型別 hello**密碼**，您先前針對這個 VM，然後按一下**確定**tooconnect。
8. 如果另一個**遠端桌面連線**對話方塊詢問您是否 tooconnect，按一下 **是**。

連接 toohello SQL Server 虛擬機器之後，您可以啟動 SQL Server Management Studio，並透過使用本機系統管理員認證的 Windows 驗證進行連接。 如果您啟用 SQL Server 驗證時，您也可以連接與 hello SQL 登入和密碼在佈建您已設定使用 SQL 驗證。

存取 toohello 電腦可讓您 toodirectly 變更電腦和您的需求為基礎的 SQL Server 設定。 例如，您無法設定 hello 防火牆設定或變更 SQL Server 組態設定。

## <a name="connect-toosql-server-remotely"></a>從遠端連線 tooSQL 伺服器
在本教學課程中，我們選取 **公用**hello 虛擬機器的存取和**SQL Server 驗證**。 這些設定會自動設定的 hello 的虛擬機器 tooallow SQL Server 連線從任何用戶端透過 hello 網際網路 （假設它們擁有 hello 正確的 SQL 登入）。

> [!NOTE]
> 如果您未選取公用期間佈建，則額外的步驟，就需要的 tooaccess 您的 SQL Server 執行個體，透過 hello 網際網路。 如需詳細資訊，請參閱[連接 SQL Server 虛擬機器 tooa](virtual-machines-windows-sql-connect.md)。
> 
> 

hello 下列各節顯示如何在您從不同的電腦上的 VM 上的 tooconnect tooyour SQL Server 執行個體 hello 網際網路。

> [!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]
> 
> 

## <a name="next-steps"></a>後續步驟
如需在 Azure 中使用 SQL Server 的其他資訊，請參閱[Azure 虛擬機器上的 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)和 hello[常見問題集](virtual-machines-windows-sql-server-iaas-faq.md)。

監看的 SQL Server 在 Azure 虛擬機器的視訊概觀， [Azure VM 是 SQL Server 2016 hello 最佳平台](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016)。

[瀏覽 hello 學習路徑](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/)Azure 虛擬機器上的 SQL server。

