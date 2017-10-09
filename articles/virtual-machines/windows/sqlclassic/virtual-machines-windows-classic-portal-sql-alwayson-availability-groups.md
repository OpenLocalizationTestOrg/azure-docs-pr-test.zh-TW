---
title: "aaaConfigure Always On 可用性群組在 Azure 虛擬機器 （傳統） |Microsoft 文件"
description: "使用 Azure 虛擬機器建立 Always On 可用性群組。 本教學課程主要是使用 hello 使用者介面和工具，而非編寫指令碼。"
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 8d48a3d2-79f8-4ab0-9327-2f30ee0b2ff1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: f428ad994a55378c281c959f4696fdcaf50632b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-virtual-machines-classic"></a>設定 Azure 虛擬機器中的 Always On 可用性群組 (傳統)
> [!div class="op_single_selector"]
> * [傳統：UI](../classic/portal-sql-alwayson-availability-groups.md)
> * [傳統：PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
<br/>

請在開始之前仔細思考一下，您現在已經可以在 Azure Resource Manager 模型中完成這項工作。 我們建議新的部署採用 Azure Resource Manager 模型。 請參閱 [Azure 虛擬機器上的 SQL Server Always On 可用性群組](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md)。

> [!IMPORTANT] 
> Microsoft 建議最新的部署使用 hello 資源管理員的模型。 Azure 有兩個不同的部署模型 toocreate 和資源的使用：[資源管理員] 和 [傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。 本文說明如何 toouse hello 傳統部署模型。 

toocomplete 這項工作使用 hello Azure Resource Manager 模型時，請參閱[SQL Server Always On 可用性群組在 Azure 虛擬機器上的](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md)。

此端對端教學課程會示範 tooimplement 可用性群組使用 SQL Server Always On Azure 虛擬機器上執行的方式。

結尾 hello hello 教學課程中，在 Azure 中的 SQL Server Alwayson 方案將會包含下列項目 hello:

* 包含多個子網路並包括前端和後端子網路的虛擬網路。
* 具有 Active Directory (Azure AD) 網域的網域控制站
* 執行 SQL Server，而且已部署的 toohello 後端子網路和網域聯結的 toohello Azure AD 的兩部虛擬機器
* Hello 節點多數 仲裁模型具有三個節點的容錯移轉叢集
* 具有兩份可用性資料庫同步認可複本的可用性群組

下列圖例 hello 是 hello 方案的圖形表示法。

![Azure 中可用性群組的測試實驗室架構](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC791912.png)

請注意以下這是一個可用的組態。 例如，您可以減少 hello 對於兩個複本的可用性群組的虛擬機器數目。 此組態為 hello 仲裁檔案共用見證雙節點叢集中使用 hello 網域控制站會將儲存在 Azure 中的計算時數。 這個方法可以減少一個從 hello 所述設定 hello 虛擬機器計數。

本教學課程假設 hello 下列：

* 您已經有 Azure 帳戶。
* 您已經知道如何 toouse hello GUI hello 虛擬機器資源庫 tooprovision 中傳統的虛擬機器以執行 SQL Server。
* 您已非常熟悉 Always On 可用性群組的功能。 如需詳細資訊，請參閱 [Always On 可用性群組 (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx)。

> [!NOTE]
> 如想將 Always On 可用性群組與 SharePoint 搭配使用，另請參閱[為 SharePoint 2013 設定 SQL Server 2012 Always On 可用性群組](https://technet.microsoft.com/library/jj715261.aspx)。
> 
> 

## <a name="create-hello-virtual-network-and-domain-controller-server"></a>建立 hello 虛擬網路和網域控制站伺服器
一開始先建立新的 Azure 試用帳戶。 設定您的帳戶之後，您應該 hello hello Azure 傳統入口網站的首頁 螢幕上。

1. 按一下 hello**新增**hello 左上角的 hello 頁面上，如下列螢幕擷取畫面的 hello 中所示的 hello 底部的按鈕。
   
    ![Hello 入口網站中，按一下 [新增]](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665511.gif)
2. 按一下**網路服務** > **虛擬網路** > **自訂建立**hello 下列螢幕擷取畫面所示。
   
    ![建立虛擬網路](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665512.gif)
3. 在 hello**建立虛擬網路**對話方塊方塊中，逐步執行 hello 頁面，並使用 hello 下表中的 hello 設定建立新的虛擬網路。 
   
   | Page | 設定 |
   | --- | --- |
   | 虛擬網路詳細資料 |**名稱 = ContosoNET**<br/>**地區 = 美國西部** |
   | DNS 伺服器和 VPN 連線能力 |None |
   | 虛擬網路位址空間 |設定以 hello 下列螢幕擷取畫面所示： ![建立虛擬網路](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784620.png) |
4. 建立 hello 做 hello 網域控制站 (DC)，您將使用的虛擬機器。 按一下**新增** > **計算** > **虛擬機器** > **從組件庫**，如下所示下列螢幕擷取畫面的 hello。
   
    ![建立虛擬機器](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784621.png)
5. 在 hello**建立虛擬機器**對話方塊方塊中，逐步執行 hello 頁面，以及使用 hello 下表中的 hello 設定來設定新的虛擬機器。 
   
   | Page | 設定 |
   | --- | --- |
   | 虛擬機器作業系統選取 hello |Windows Server 2012 R2 Datacenter |
   | 虛擬機器組態 |**版本發行日期** = (最新版本)<br/>**虛擬機器名稱** = ContosoDC<br/>**層** = 標準<br/>**大小** = A2 (2 核心)<br/>**新使用者名稱** = AzureAdmin<br/>**新密碼** = Contoso!000<br/>**確認** = Contoso!000 |
   | 虛擬機器組態 |**雲端服務** = 建立新的雲端服務<br/>**雲端服務 DNS 名稱** = 唯一的雲端服務名稱<br/>**DNS 名稱** = 唯一的名稱 (例如：ContosoDC123)<br/>**區域/同質群組/虛擬網路** = ContosoNET<br/>**虛擬網路子網路** = Back(10.10.2.0/24)<br/>**儲存體帳戶** = 使用自動產生的儲存體帳戶<br/>**可用性設定組** = (無) |
   | 虛擬機器選項 |使用預設值 |

設定 hello 新的虛擬機器之後，等候 hello 虛擬機器 toobe 完畢。 這個程序需要一些時間 toofinish。 如果您按一下 hello**虛擬機器** 索引標籤中 hello Azure 傳統入口網站中，您可以看到 ContosoDC 循環的狀態從**啟動 （正在佈建）**太**已停止**， **啟動**，**執行 （正在佈建）**，最後再**執行**。

現在已成功佈建 hello DC 伺服器。 接下來，您將在此 DC 伺服器上設定 hello Active Directory 網域。

## <a name="configure-hello-domain-controller"></a>設定 hello 網域控制站
在 hello 下列步驟，您必須 hello ContosoDC 機器設定為 corp.contoso.com 的網域控制站中。

1. 在 hello 入口網站中，選取 hello **ContosoDC**機器。 在 hello**儀表板**索引標籤上，按一下 **連接**tooopen 遠端桌面存取的遠端桌面 (RDP) 檔案。
   
    ![連接 tooVritual 機器](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784622.png)
2. 以所設定的系統管理員帳戶 (**\AzureAdmin**) 和密碼 (**Contoso!000**) 登入。
3. 根據預設，hello**伺服器管理員**應該顯示儀表板。
4. 按一下 hello**新增角色及功能**hello 儀表板上的連結。
   
    ![透過 [伺服器總管] 新增角色](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784623.png)
5. 按一下**下一步**直到 toohello**伺服器角色**> 一節。
6. 選取 hello **Active Directory 網域服務**和**DNS 伺服器**角色。 出現提示時，新增這些角色需要的更多功能。
   
   > [!NOTE]
   > 螢幕會顯示無靜態 IP 位址的驗證警告。 如果您要測試 hello 組態，按一下**繼續**。 生產案例[使用 PowerShell tooset hello 靜態 IP 位址的 hello 網域控制站機器](../../../virtual-network/virtual-networks-reserved-private-ip.md)。
   > 
   > 
   
    ![新增角色對話方塊](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784624.png)
7. 按一下**下一步**直到您到達 hello**確認**> 一節。 選取 hello**必要時自動重新啟動 hello 目的地伺服器**核取方塊。
8. 按一下 [Install] 。
9. Hello 功能的安裝之後，傳回 toohello**伺服器管理員**儀表板。
10. 選取新的 hello **AD DS** hello 左窗格上的選項。
11. 按一下 hello**詳細**hello 黃色警告列上的連結。
    
     ![DNS 伺服器虛擬機器上的 AS DS 對話方塊](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784625.png)
12. 在 hello**動作**hello 的資料行**所有伺服器工作詳細資料**對話方塊中，按一下**升級此伺服器 tooa 網域控制站**。
13. 在 hello **Active Directory 網域服務設定精靈**，使用下列值的 hello:
    
    | Page | 設定 |
    | --- | --- |
    | 部署組態 |**新增樹系** = 已選取<br/>**根網域名稱** = corp.contoso.com |
    | 網域控制站選項 |**密碼** = Contoso!000<br/>**確認密碼** = Contoso!000 |
14. 按一下**下一步**透過 toogo hello hello 精靈中的其他頁面。 在 hello**必要條件檢查**頁面上，確認您看到下列訊息的 hello:**順利通過所有先決條件檢查**。 請注意，您應該檢閱所有適用的警告訊息，但是它可能 toocontinue hello 安裝。
15. 按一下 [Install] 。 hello **ContosoDC**虛擬機器會自動重新開機。

## <a name="configure-domain-accounts"></a>設定網域帳戶
hello 接下來的步驟設定 hello Active Directory 帳戶，供日後使用。

1. 重新登入 toohello **ContosoDC**機器。
2. 在 [伺服器管理員]  中，按一下 [工具]  >  [Active Directory 管理中心] 。
   
    ![Active Directory 管理中心](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784626.png)
3. 在 hello **Active Directory 管理中心**，選取**corp （本機）** hello 左窗格中。
4. 在右邊的 hello**工作**] 窗格中，按一下 [**新增** > **使用者**。 使用下列設定的 hello:
   
   | 設定 | 值 |
   | --- | --- |
   | **名字** |Install |
   | **使用者 SamAccountName** |Install |
   | **密碼** |Contoso! 000 |
   | **確認密碼** |Contoso! 000 |
   | **其他密碼選項** |已選取 |
   | **密碼永久有效** |已檢查 |
5. 按一下**確定**toocreate hello**安裝**使用者。 此帳戶將會使用的 tooconfigure hello 容錯移轉叢集和 hello 可用性群組。
6. 建立兩個額外的使用者， **CORP\SQLSvc1**和**CORP\SQLSvc2**，hello 與相同的步驟。 這些帳戶將用於 hello SQL Server 執行個體。 接下來，您必須 toogive **CORP\Install** hello 必要的權限 tooconfigure Windows 容錯移轉叢集。
7. 在 hello **Active Directory 管理中心**，按一下  **corp （本機）** hello 左窗格中。 在 hello**工作** 窗格中，按一下 **屬性**。
   
    ![公司使用者內容](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784627.png)
8. 選取**延伸**，然後按一下hello**進階**按鈕 hello**安全性** 索引標籤。
9. 在 hello **corp 的進階安全性設定**對話方塊中，按一下 **新增**。
10. 按一下 選取主體、搜尋 **CORP\Install**，然後按一下確定。
11. 選取 hello**讀取全部內容**和**建立電腦物件**權限。
    
     ![公司使用者權限](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784628.png)
12. 按一下 [確定]，再按一下 [確定]。 關閉 hello corp 屬性 視窗。

現在，您可以設定 Active Directory 與 hello 使用者物件，您將建立三個 SQL Server 虛擬機器，並將它們 toothis 網域。

## <a name="create-hello-sql-server-virtual-machines"></a>SQL Server 虛擬機器建立 hello
建立三個虛擬機器 一個節點用於叢集節點，兩個節點用於 SQL Server。 toocreate 每個 hello 的虛擬機器移回 toohello Azure 傳統入口網站中，按一下**新增** > **計算** > **虛擬機器** > **從組件庫**。 然後，使用下列資料表 toohelp 建立 hello 虛擬機器的 hello hello 樣板。

| Page | VM1 | VM2 | VM3 |
| --- | --- | --- | --- |
| 虛擬機器作業系統選取 hello |**Windows Server 2012 R2 Datacenter** |**SQL Server 2014 RTM Enterprise** |**SQL Server 2014 RTM Enterprise** |
| 虛擬機器組態 |**版本發行日期** = (最新版本)<br/>**虛擬機器名稱** = ContosoWSFCNode<br/>**層** = 標準<br/>**大小** = A2 (2 核心)<br/>**新使用者名稱** = AzureAdmin<br/>**新密碼** = Contoso!000<br/>**確認** = Contoso!000 |**版本發行日期** = (最新版本)<br/>**虛擬機器名稱** = ContosoSQL1<br/>**層** = 標準<br/>**大小** = A3 (4 核心)<br/>**新使用者名稱** = AzureAdmin<br/>**新密碼** = Contoso!000<br/>**確認** = Contoso!000 |**版本發行日期** = (最新版本)<br/>**虛擬機器名稱** = ContosoSQL2<br/>**層** = 標準<br/>**大小** = A3 (4 核心)<br/>**新使用者名稱** = AzureAdmin<br/>**新密碼** = Contoso!000<br/>**確認** = Contoso!000 |
| 虛擬機器組態 |**雲端服務** = 先前建立的唯一雲端服務 DNS 名稱 (例如︰ContosoDC123)<br/>**區域/同質群組/虛擬網路** = ContosoNET<br/>**虛擬網路子網路** = Back(10.10.2.0/24)<br/>**儲存體帳戶** = 使用自動產生的儲存體帳戶<br/>**可用性設定組** = 建立可用性設定組<br/>**可用性設定組名稱** = SQLHADR |**雲端服務** = 先前建立的唯一雲端服務 DNS 名稱 (例如︰ContosoDC123)<br/>**區域/同質群組/虛擬網路** = ContosoNET<br/>**虛擬網路子網路** = Back(10.10.2.0/24)<br/>**儲存體帳戶** = 使用自動產生的儲存體帳戶<br/>**可用性設定組**= 的 SQLHADR （您也可以設定 hello 可用性設定組 hello 機器建立之後。 所有的三部機器都應該指派 toohello SQLHADR 可用性設定組。） |**雲端服務** = 先前建立的唯一雲端服務 DNS 名稱 (例如︰ContosoDC123)<br/>**區域/同質群組/虛擬網路** = ContosoNET<br/>**虛擬網路子網路** = Back(10.10.2.0/24)<br/>**儲存體帳戶** = 使用自動產生的儲存體帳戶<br/>**可用性設定組**= 的 SQLHADR （您也可以設定 hello 可用性設定組 hello 機器建立之後。 所有的三部機器都應該指派 toohello SQLHADR 可用性設定組。） |
| 虛擬機器選項 |使用預設值 |使用預設值 |使用預設值 |

<br/>

> [!NOTE]
> hello 先前的設定建議標準層的虛擬機器，因為基本層機器不支援負載平衡的端點。 需要負載平衡的端點稍後 toocreate 可用性群組接聽程式。 此外，我們建議的 hello 機器大小是為了測試可用性群組在 Azure 虛擬機器。 Hello 實際執行工作負載的最佳效能，請參閱 SQL Server 機器大小和組態中的 hello 建議[Azure 虛擬機器中 SQL Server 的效能最佳做法](../sql/virtual-machines-windows-sql-performance.md)。
> 
> 

Hello 三個虛擬機器完整佈建之後，您需要 toojoin 它們 toohello **corp.contoso.com**網域和授與 CORP\Install 管理權限 toohello 機器。 toodo hello 三個虛擬機器的每一個遵循步驟，使用 hello。

1. 首先，變更 hello 慣用 DNS 伺服器位址。 下載每個虛擬機器的 RDP 檔案 tooyour 本機目錄 hello 清單中選取 hello 虛擬機器，然後按一下 hello**連接** 按鈕。 tooselect 虛擬機器，但 hello 第一個資料格在 hello 列中，按一下任何位置，hello 下列螢幕擷取畫面所示。
   
    ![下載 hello RDP 檔案](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC664953.jpg)
2. 開啟 hello RDP 檔，您已下載，與使用設定的管理員帳戶登入 toohello 虛擬機器 (**BUILTIN\AzureAdmin**) 和密碼 (**Contoso ！ 000**)。
3. 登入之後，您應該會看到 hello**伺服器管理員**儀表板。 按一下**本機伺服器**hello 左窗格中。
4. 按一下 hello**啟用 IPv6 的 DHCP 所指派的 IPv4 位址**連結。
5. 在 hello**網路連線**對話方塊方塊中，按一下 hello 網路圖示。
   
    ![變更 hello 虛擬機器的慣用 DNS 伺服器](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784629.png)
6. Hello 命令列上，按一下**變更這個連線的 hello 設定**。 （根據您的視窗 hello 大小，您可能必須 tooclick hello 雙重向右鍵 toosee 這個命令）。
7. 選取 網際網路通訊協定第 4 版 (TCP/IPv4) ，然後按一下內容 。
8. 選取**下列的 DNS 伺服器位址使用 hello** ，然後指定**10.10.2.4**中**慣用 DNS 伺服器**。
9. hello **10.10.2.4**位址是 hello 位址，是指派的 tooa Azure 的虛擬網路中的 hello 10.10.2.0/24 子網路中的虛擬機器。 虛擬機器是 **ContosoDC**。 tooverify **ContosoDC**的 IP 位址，使用**nslookup contosodc** hello 命令提示字元視窗，hello 下列螢幕擷取畫面所示。
   
    ![對網域控制站使用 NSLOOKUP toofind IP 位址](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC664954.jpg)
10. 按一下**確定** > **關閉**toocommit hello 變更。 您可以現在的加入 hello 虛擬機器**corp.contoso.com**。
11. 在 hello**本機伺服器**視窗中，按一下 hello **WORKGROUP**連結。
12. 在 hello**電腦名稱**區段中，按一下**變更**。
13. 選取 hello**網域**核取方塊，輸入**corp.contoso.com**在 hello 文字方塊中，然後按一下**確定**。
14. 在 hello **Windows 安全性**對話方塊方塊中，指定 hello hello 預設網域系統管理員帳戶的認證 (**CORP\AzureAdmin**) 和 hello 密碼 (**Contoso ！ 000**).
15. 當您看見 hello 「  褖畫惎 toohello corp.contoso.com 網域 」 訊息時，按一下**確定**。
16. 按一下**關閉** > **立即重新啟動**hello 對話方塊中。

### <a name="add-hello-corpinstall-user-as-an-administrator-on-each-virtual-machine"></a>將 hello Corp\Install 使用者新增為每個虛擬機器上的系統管理員
1. 等候 hello 虛擬機器重新啟動，並開啟 hello RDP 檔案一次 toosign toohello 虛擬機器中使用 hello **BUILTIN\AzureAdmin**帳戶。
2. 在**伺服器管理員**按一下**工具** > **電腦管理**。
   
    ![電腦管理](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784630.png)
3. 在 hello**電腦管理**對話方塊方塊中，展開 **本機使用者和群組**，然後按一下**群組**。
4. 按兩下 hello**管理員**群組。
5. 在 [hello**系統管理員屬性**對話方塊方塊中，按一下 hello**新增**] 按鈕。
6. 輸入 hello 使用者**CORP\Install**，然後按一下**確定**。 當提示您輸入認證，使用 hello **AzureAdmin**帳戶以 hello **Contoso ！ 000**密碼。
7. 按一下**確定**tooclose hello**系統管理員內容** 對話方塊。

### <a name="add-hello-failover-clustering-feature-tooeach-virtual-machine"></a>新增 hello 容錯移轉叢集功能 tooeach 虛擬機器
1. 在 hello**伺服器管理員**儀表板，按一下 **新增角色及功能**。
2. 在 [hello**新增角色及功能精靈**，按一下**下一步]**直到 toohello**功能**頁面。
3. 選取 [容錯移轉叢集] 。 出現提示時，請新增其他相依功能。
   
    ![新增容錯移轉叢集功能 toovirtual 機器](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784631.png)
4. 按一下**下一步**，然後按一下**安裝**上 hello**確認**頁面。
5. 當 hello**容錯移轉叢集**功能安裝完成後，按一下 **關閉**。
6. 登出 hello 虛擬機器。
7. 重複步驟三部伺服器都本節中的 hello: **ContosoWSFCNode**， **ContosoSQL1**，和**ContosoSQL2**。

hello SQL Server 虛擬機器現在已佈建且正在執行，但其中一個 hello for SQL Server 的預設選項。

## <a name="create-hello-failover-cluster"></a>建立 hello 容錯移轉叢集
在本節中，您可以建立 hello 容錯移轉叢集來裝載您稍後建立 hello 可用性群組。 現在，您應該完成下列 tooeach hello 三個虛擬機器，您將使用 hello 容錯移轉叢集中的 hello:

* 在 Azure 中的 hello 完整佈建的虛擬機器
* 加入 hello 虛擬機器 toohello 網域
* 加入**CORP\Install** toohello 本機 Administrators 群組
* 加入的 hello 容錯移轉叢集功能

您可以將它 toohello 容錯移轉叢集之前，這些都是在每個虛擬機器上的必要條件。

此外，請注意，Azure 虛擬網路的 hello 行為 hello 相同的內部部署網路的方式。 您需要在 hello 順序 toocreate hello 叢集：

1. 在一個節點上 (**ContosoSQL1**) 建立單一節點叢集。
2. 修改 hello 叢集 IP 位址 tooan 未使用的 IP 位址 (**10.10.2.101**)。
3. 將 hello 叢集名稱上線。
4. 新增 hello 其他節點 (**ContosoSQL2**和**ContosoWSFCNode**)。

使用下列步驟，完整設定叢集 hello toocomplete hello 工作 hello。

1. 開啟 hello RDP 檔案**ContosoSQL1**，並使用 hello 網域帳戶登入**CORP\Install**。
2. 在 hello**伺服器管理員**儀表板，按一下 **工具** > **容錯移轉叢集管理員**。
3. Hello 左窗格中，以滑鼠右鍵按一下**容錯移轉叢集管理員**，然後按一下**建立叢集**hello 下列螢幕擷取畫面所示。
   
    ![建立叢集](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784632.png)
4. 在 hello 建立叢集精靈，逐步執行 hello 頁面，以及使用 hello 下表中的 hello 設定來建立單一節點叢集：
   
   | Page | 設定 |
   | --- | --- |
   | 開始之前 |使用預設值 |
   | 選取伺服器 |在 [輸入伺服器名稱] 中輸入 **ContosoSQL1**，然後按一下 [新增] |
   | 驗證警告 |選取**否。 我不需要此群集中，來自 Microsoft 的支援和不想 toorun hello 驗證測試。當我按 [下一步] 時，繼續建立 hello 叢集**。 |
   | 用於管理 hello 叢集存取點 |在 [叢集名稱] 中輸入 **Cluster1** |
   | 確認 |除非您使用的是儲存空間，否則請使用預設值。 請參閱本表格後的 hello 警告。 |
   
   > [!WARNING]
   > 如果您使用[儲存空間](https://technet.microsoft.com/library/hh831739)、 將多個磁碟組成儲存集區，則必須清除 hello**新增所有合格的存放裝置 toohello 叢集**hello 核取方塊**確認**頁面。 如果您不要清除此選項，則會卸離 hello 虛擬磁碟 hello 叢集程序期間。 如此一來，他們也不會在磁碟管理員] 或 [檔案總管之前從 hello 叢集中移除 hello 儲存空間，並使用 PowerShell 來重新附加它。
   > 
   > 
5. Hello 左窗格中，展開 **容錯移轉叢集管理員**，然後按一下 **Cluster1.corp.contoso.com**。
6. 在 hello 中央窗格中，向下捲動 toohello**叢集核心資源**區段，然後展開 hello**名稱： Clutser1**詳細資料。 您應該會看到這兩個 hello**名稱**和 hello **IP 位址**hello 中的資源**失敗**狀態。 hello IP 位址資源無法上線因為 hello 叢集指派 hello hello 機器本身，相同的 IP 位址，這是重複的位址。
7. 以滑鼠右鍵按一下失敗的 hello **IP 位址**資源，然後再按一下**屬性**。
   
    ![叢集屬性](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784633.png)
8. 選取**靜態 IP 位址**，指定**10.10.2.101**在 hello**位址**文字方塊，然後再按一下**確定**。
9. 在 hello**叢集核心資源**區段中，以滑鼠右鍵按一下**名稱： Cluster1**，然後按一下**上線**。 等待兩個資源上線。 Hello 叢集名稱資源上線時，會以新的 Active Directory 電腦帳戶更新 hello DC 伺服器。 這個 Active Directory 帳戶將用於稍後 toorun hello 可用性群組的叢集的服務。
10. 新增 hello 剩餘節點 toohello 叢集。 Hello 瀏覽器樹狀目錄中，以滑鼠右鍵按一下**Cluster1.corp.contoso.com**，然後按一下**加入節點**hello 下列螢幕擷取畫面所示。
    
     ![新增節點 toohello 叢集](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784634.png)
11. 在 [hello**新增節點精靈**，按一下**下一步]**上 hello**選取伺服器**頁面上，加入**ContosoSQL2**和**ContosoWSFCNode** toohello 清單中的 hello 伺服器名稱**輸入伺服器名稱**，然後按一下**新增**。 完成之後，按 [下一步]。
12. 在 hello**驗證警告**頁面上，按一下**否**，但是在生產案例中，您應該執行 hello 驗證測試。 然後按 [下一步] 。
13. 在 hello**確認**頁面上，按一下**下一步**tooadd hello 節點。
    
    > [!WARNING]
    > 如果您使用[儲存空間](https://technet.microsoft.com/library/hh831739)、 將多個磁碟組成儲存集區，則必須清除 hello**新增所有合格的存放裝置 toohello 叢集**核取方塊。 如果您不要清除此選項，則會卸離 hello 虛擬磁碟 hello 叢集程序期間。 如此一來，他們也不會出現在 磁碟管理員 或 檔案總管之前從叢集移除 hello 儲存空間，並使用 PowerShell 將其重新附加。
    > 
    > 
14. Hello 節點會加入 toohello 叢集之後，請按一下**完成**。 容錯移轉叢集管理員現在應該會顯示您的叢集有 3 個節點，並將其列在 hello**節點**容器。
15. 登出 hello 遠端桌面工作階段。

## <a name="prepare-hello-sql-server-instances-for-availability-groups"></a>針對可用性群組準備 hello SQL Server 執行個體
在本節中，您要執行 hello 上同時**ContosoSQL1**和**contosoSQL2**:

* 新增的登入**NT AUTHORITY\System**具備必要權限設定 toohello 預設 SQL Server 執行個體。
* 新增**CORP\Install**為 sysadmin 角色 toohello 預設 SQL Server 執行個體。
* 開啟 SQL server 的遠端存取的 hello 防火牆。
* 啟用 hello Alwayson 可用性群組功能。
* Hello SQL Server 服務帳戶變更太**CORP\SQLSvc1**和**CORP\SQLSvc2**分別。

執行這些動作沒有順序限制。 不過，遵循步驟 hello 逐步執行順序。 兩個步驟 hello **ContosoSQL1**和**ContosoSQL2**:

1. 如果您沒有已登出 hello 遠端桌面工作階段的 hello 虛擬機器，請立刻執行。
2. 開啟 hello RDP 檔案**ContosoSQL1**和**ContosoSQL2**，並以登入**BUILTIN\AzureAdmin**。
3. 新增**NT AUTHORITY\System** toohello 具備必要權限的 SQL Server 登入。 開啟 **SQL Server Management Studio**。
4. 按一下**連接**tooconnect toohello 預設 SQL Server 執行個體。
5. 在 [物件總管] 中，依序展開 [安全性]、[登入]。
6. 以滑鼠右鍵按一下 hello **NT AUTHORITY\System**登入，然後再按一下**屬性**。
7. 在 [hello**安全性實體**hello 本機伺服器，請選取] 頁面上，**授與**的 hello 下列權限，，然後按一下 **[確定]**。
   
   * 更改所有可用性群組
   * 連接 SQL
   * 檢視伺服器狀態
8. 新增**CORP\Install**為**sysadmin**角色 toohello 預設 SQL Server 執行個體。 在 [物件總管]  中，以滑鼠右鍵按一下 [登入] ，再按一下 [新增登入] 。
9. 在 [登入名稱] 中輸入 **CORP\Install**。
10. 在 hello**伺服器角色**頁面上，選取**sysadmin**，然後按一下 **確定**。 您建立 hello 登入之後，可以查看展開**登入**中**物件總管 中**。
11. SQL Server 的防火牆規則上 hello toocreate**啟動**畫面上，開啟**具有進階安全性的 Windows 防火牆**。
12. Hello 左窗格中，選取**輸入規則**。 Hello 右窗格中，按一下 **新規則**。
13. 在 hello**規則類型**頁面上，按一下**程式** > **下一步**。
14. 在 hello**程式**頁面上，選取**這個程式路徑**，型別**%ProgramFiles%\Microsoft SQL Server\MSSQL12。MSSQLSERVER\MSSQL\Binn\sqlservr.exe**在 hello 文字方塊中，然後按一下**下一步**。 如果您要遵循這些指示，但使用 SQL Server 2012，hello SQL Server 目錄是**MSSQL11。MSSQLSERVER**。
15. 在 hello**動作**頁面上，保留**允許 hello 連線**選取，然後再按一下**下一步**。
16. 在 hello**設定檔**頁面上，接受 hello 預設設定，然後按**下一步**。
17. 在 hello**名稱**頁面上，指定規則的名稱，例如**SQL Server （程式規則）**，在 hello**名稱**文字方塊，然後按一下 **完成**。
18. tooenable hello **Always On 可用性群組**功能，在 hello**啟動**畫面上，開啟**SQL Server 組態管理員**。
19. 在 hello 瀏覽器樹狀目錄中，按一下  **SQL Server 服務**，以滑鼠右鍵按一下 hello **SQL Server (MSSQLSERVER)**服務，然後再按一下**屬性**。
20. 按一下 hello **Alwayson 高可用性**索引標籤上，選取**啟用 Alwayson 可用性群組**，如下所示 hello 下列螢幕擷取畫面，然後按一下**套用**。 按一下**確定**在 hello 對話方塊中，但不要關閉 hello**屬性**尚未對話方塊。 變更 hello 服務帳戶之後，您將會重新啟動 hello SQL Server 服務。
    
     ![啟用 Always On 可用性群組](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665520.gif)
21. toochange hello SQL Server 服務帳戶，按一下 hello**登入**索引標籤上，輸入**CORP\SQLSvc1** (如**ContosoSQL1**) 或**CORP\SQLSvc2** (如**ContosoSQL2**) 中**帳戶名稱**、 填入並確認 hello 密碼，然後按一下**確定**。
22. 在 hello 開啟對話方塊，按一下 **是**toorestart hello SQL Server 服務。 Hello SQL Server 服務重新啟動之後，變更您所做 hello**屬性**對話方塊都有效。
23. 登出 hello 虛擬機器。

## <a name="create-hello-availability-group"></a>建立 hello 可用性群組
現在您已經準備就緒 tooconfigure 可用性群組。 以下列出需執行的動作：

* 在 **ContosoSQL1** 上建立新的資料庫 (**MyDB1**)。
* 利用完整備份與 hello 資料庫的交易記錄備份。
* 還原完整的 hello 和太記錄備份**ContosoSQL2**以 hello **NORECOVERY**選項。
* 建立 hello 可用性群組 (**AG1**) 同步認可、 自動容錯移轉，與可讀取次要複本。

### <a name="create-hello-mydb1-database-on-contososql1"></a>在 ContosoSQL1 上建立 hello MyDB1 資料庫
1. 如果您已不已經登出 hello 遠端桌面工作階段的**ContosoSQL1**和**ContosoSQL2**，請立刻執行。
2. 開啟 hello RDP 檔案**ContosoSQL1**，並以登入**CORP\Install**。
3. 在 [檔案總管]  中，於 **\\C:** 磁碟中，建立名為 **備份** 的目錄。 您將使用此目錄 tooback 及還原您的資料庫。
4. Hello 新目錄按一下滑鼠右鍵，指向太**分享**，然後按一下**特定人員**hello 下列螢幕擷取畫面所示。
   
    ![建立備份資料夾](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665521.gif)
5. 新增**CORP\SQLSvc1**，然後為 hello**讀/寫**權限。 新增**CORP\SQLSvc2**，然後為 hello**讀取**權限，如中所示 hello 下列螢幕擷取畫面，然後按一下**共用**。 Hello 檔案共用的程序完成之後，請按一下**完成**。
   
    ![將權限授與備份資料夾](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665522.gif)
6. 從 hello toocreate hello 資料庫**啟動**功能表中，開啟**SQL Server Management Studio**，然後按一下**連接**tooconnect toohello 預設 SQL Server 執行個體。
7. 在 物件總管 中，以滑鼠右鍵按一下 資料庫 ，然後按一下新增資料庫 。
8. 在 資料庫名稱  中，輸入 **MyDB1**，然後按一下確定 。

### <a name="make-a-full-backup-of-mydb1-and-restore-it-on-contososql2"></a>建立 MyDB1 的完整備份，然後將其還原至 ContosoSQL2
1. toomake hello 的完整備份資料庫，在**物件總管 中**，依序展開**資料庫**，以滑鼠右鍵按一下**MyDB1**，點太**工作**，和然後按一下 **Back Up**。
2. 在 hello**來源**區段中，持續**備份類型**設定得**完整**。 在 hello**目的地**區段中，按一下**移除**tooremove hello 預設 hello 備份檔案的檔案路徑。
3. 在 hello**目的地**區段中，按一下**新增**。
4. 在 hello**檔案名稱**文字方塊中，輸入 **\\ContosoSQL1\backup\MyDB1.bak**，按一下**[確定]**，然後按一下**確定**再次tooback hello 資料庫備份。 Hello 備份作業完成時，按一下**確定**再次 tooclose hello 對話方塊。
5. toomake 交易記錄的 hello 資料庫備份，**物件總管 中**，依序展開**資料庫**，以滑鼠右鍵按一下**MyDB1**，點太**工作**，然後按一下 **Back Up**。
6. 在 [備份類型]  中，選取 [交易記錄] 。 保留 hello**目的地**檔案路徑集 toohello 您稍早指定的其中一個，然後按一下**確定**。 Hello 備份作業完成之後，請按一下**確定**一次。
7. 完整的 toorestore hello 和交易記錄備份**ContosoSQL2**，開啟 hello RDP 檔，以取得**ContosoSQL2**，並以登入**CORP\Install**。 保留 hello 遠端桌面工作階段的**ContosoSQL1**開啟。
8. 從 hello**啟動**功能表中，開啟**SQL Server Management Studio**，然後按一下**連接**tooconnect toohello 預設 SQL Server 執行個體。
9. 在 [物件總管]  中，以滑鼠右鍵按一下 [資料庫] ，再按一下 [還原資料庫] 。
10. 在 hello**來源**區段中，選取**裝置**，並按一下省略符號，hello **...** 按鈕。
11. 在 [選取備份裝置] 中按一下 [新增]。
12. 在 [備份檔案位置]  中，輸入 **\\ContosoSQL1\backup**，按一下 [重新整理] **Refresh**，選取 **MyDB1.bak**，按一下 [確定] ，然後再按一次 [確定] **OK**。 您現在應該會看到完整備份的 hello 與 hello 記錄檔備份在 hello**備份組 toorestore**窗格。
13. 移 toohello**選項**頁面上，選取**RESTORE WITH NORECOVERY**中**復原狀態**，然後按一下**確定**toorestore hello 資料庫。 Hello 之後還原作業完成，請按一下**確定**。

### <a name="create-hello-availability-group"></a>建立 hello 可用性群組
1. 移回 toohello 遠端桌面工作階段的**ContosoSQL1**。 在**物件總管 中**在 SQL Server Management Studio，以滑鼠右鍵按一下**Alwayson 高可用性**，然後按一下**新增可用性群組精靈**hello 所示，下列螢幕擷取畫面。
   
    ![啟動新增可用性群組精靈](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665523.gif)
2. 在 hello**簡介**頁面上，按一下**下一步**。 在 hello**指定可用性群組名稱**頁面上，輸入**AG1**中**可用性群組名稱**，然後按一下 **下一步**一次。
   
    ![新增可用性群組精靈，指定可用性群組名稱](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665524.gif)
3. 在 [hello**選取資料庫**頁面上，選取**MyDB1**，然後按一下**下一步]**。 由於您已執行至少一個完整備份 hello 預定的主要複本上，hello 資料庫會符合可用性群組的 hello 必要條件。
   
    ![新增可用性群組精靈：選取資料庫](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665525.gif)
4. 在 hello**指定複本**頁面上，按一下**將複本加入**。
   
    ![新增可用性群組精靈：選取複本](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665526.gif)
5. 在 hello**連接 tooServer**  對話方塊中，輸入**ContosoSQL2**中**伺服器名稱**，然後按一下**連接**。
   
    ![新的可用性群組精靈 連接 tooserver](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665527.gif)
6. 在 hello**指定複本**頁面上，您現在應該會看到**ContosoSQL2**中所列**可用複本**。 Hello 複本設定 hello 下列螢幕擷取畫面所示。 完成後，請按 [下一步] 。
   
    ![新增可用性群組精靈：選取複本 (完整)](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665528.gif)
7. 在 hello**選取初始資料同步處理**頁面上，選取**僅聯結**，然後按一下**下一步**。 您已執行資料同步處理以手動方式上進行 hello 完整和交易備份時**ContosoSQL1**還原它們**ContosoSQL2**。 您可以選擇不 tooperform hello 在資料庫上的備份和還原作業，而是選取**完整**toolet hello 新增可用性群組精靈為您執行資料同步處理。 不過，我們不建議針對某些企業中的超大型資料庫採用這種選項。
   
    ![新增可用性群組精靈：選取初始資料同步處理](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665529.gif)
8. 在 hello**驗證**頁面上，按一下**下一步**。 此頁面應看起來類似 toohello 下列螢幕擷取畫面。 沒有 hello 接聽程式設定的警告，因為您尚未設定可用性群組接聽程式。 您可以忽略此警告，因為本教學課程不會示範設定接聽程式的步驟。 tooconfigure hello 接聽程式之後您完成這個教學課程，請參閱[在 Azure 中設定 Alwayson 可用性群組的 ILB 接聽程式](../classic/ps-sql-int-listener.md)。
   
    ![新增可用性群組精靈：驗證](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665530.gif)
9. 在 hello**摘要**頁面上，按一下**完成**，hello 精靈設定 hello 新可用性群組，然後等候。 在 [hello**進度**] 頁面上，您可以按一下**更多詳細資料**tooview hello 詳細進度。 Hello 精靈完成後，檢查 hello**結果**頁面 tooverify 該 hello 可用性群組建立成功時 hello 下列螢幕擷取畫面所示，然後按一下**關閉**tooexit hello精靈。
   
    ![新增可用性群組精靈：結果](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665531.gif)
10. 在 [物件總管]  中，展開 [AlwaysOn 高可用性] ，再展開 [可用性群組] 。 您現在應該會看到此容器中的 hello 新可用性群組。 以滑鼠右鍵按一下 [AG1 (主要)] ，再按一下 [顯示儀表板] 。
    
     ![顯示可用性群組儀表板](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665532.gif)
11. 您**Alwayson 儀表板**應該外觀類似 toohello 一個 hello 在下列螢幕擷取畫面。 您可以看到 hello 複本，每個複本和 hello 同步處理狀態的 hello 容錯移轉模式。
    
     ![可用性群組儀表板](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665533.gif)
12. 傳回太**伺服器管理員**，按一下 **工具**，然後開啟**容錯移轉叢集管理員**。
13. 展開 [Cluster1.corp.contoso.com]，然後展開 [服務和應用程式]。 選取**角色**並記下該 hello **AG1**已建立可用性群組的角色。 請注意，AG1 並沒有 IP 位址供資料庫用戶端可以連線 toohello 可用性群組，因為您並未設定接聽程式。 Toohello 讀取-寫入作業的主要節點和唯讀查詢的 hello 次要節點，您可以直接連接。
    
     ![容錯移轉叢集管理員中的 AG](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665534.gif)

> [!WARNING]
> 請勿嘗試 toofail 移轉 hello 從 hello 容錯移轉叢集管理員的可用性群組。 所有容錯移轉作業都應在 SQL Server Management Studio 的 [AlwaysOn 儀表板]  中執行。 如需詳細資訊，請參閱[限制使用 hello 與可用性群組容錯移轉叢集管理員](https://msdn.microsoft.com/library/ff929171.aspx)。
> 
> 

## <a name="next-steps"></a>後續步驟
現在，您已透過在 Azure 中建立可用性群組的方式，成功實作 SQL Server Always On。 tooconfigure 這個可用性群組接聽程式，請參閱[在 Azure 中設定 Alwayson 可用性群組的 ILB 接聽程式](../classic/ps-sql-int-listener.md)。

如需在 Azure 中使用 SQL Server 的其他資訊，請參閱 [Azure 虛擬機器上的 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。

