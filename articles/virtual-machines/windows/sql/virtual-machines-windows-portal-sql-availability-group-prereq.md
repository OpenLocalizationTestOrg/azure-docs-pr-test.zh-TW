---
title: "aaaSQL 伺服器的可用性群組-Azure 虛擬機器必要條件 |Microsoft 文件"
description: "本教學課程會示範如何 tooconfigure hello 必要條件，用於建立 SQL Server Always On 可用性群組在 Azure Vm 上。"
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: c492db4c-3faa-4645-849f-5a1a663be55a
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: eed0729ead25c7793bb17a04cd7fd996c7dc8c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="complete-hello-prerequisites-for-creating-always-on-availability-groups-on-azure-virtual-machines"></a>完成 hello 建立 Azure 虛擬機器上的 Alwayson 可用性群組的必要條件

本教學課程示範如何 toocomplete hello 建立的必要條件[SQL Server Always On 可用性群組在 Azure 虛擬機器 (Vm) 上的](virtual-machines-windows-portal-sql-availability-group-tutorial.md)。 完成 hello 必要條件後，您可以在單一資源群組中有網域控制站、 兩個 SQL Server Vm，以及將見證伺服器。

**估計時間**： 可能需要數小時 toocomplete hello 必要條件。 這個時間大部分都是花在建立虛擬機器。

hello 下列圖表說明您在 hello 教學課程中所建置。

![可用性群組](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="review-availability-group-documentation"></a>檢閱可用性群組文件

本教學課程假設您對 SQL Server Always On 可用性群組有基本的了解。 如果您不熟悉這項技術，請參閱 [Always On 可用性群組概觀 (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx)。


## <a name="create-an-azure-account"></a>建立 Azure 帳戶
您需要 Azure 帳戶。 您可以[申請免費 Azure 帳戶](/pricing/free-trial/?WT.mc_id=A261C142F)或[啟用 Visual Studio 訂閱者權益](/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。

## <a name="create-a-resource-group"></a>建立資源群組
1. 登入 toohello [Azure 入口網站](http://portal.azure.com)。
2. 按一下 **+**  toocreate hello 入口網站中的新物件。

   ![新增物件](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-portalplus.png)

3. 型別**資源群組**在 hello **Marketplace**搜尋 視窗。

   ![資源群組](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-resourcegroupsymbol.png)
4. 按一下 [資源群組]。
5. 按一下 [建立] 。
6. 在 hello**資源群組**刀鋒視窗底下**資源群組名稱**，輸入 hello 資源群組的名稱。 例如，輸入 **sql-ha-rg**。
7. 如果您有多個 Azure 訂用帳戶，請確認 hello 訂閱 hello 想 toocreate hello 可用性群組中的 Azure 訂用帳戶。
8. 選取位置。 hello 位置為 hello 想 toocreate hello 可用性群組的 Azure 區域。 此教學課程中，我們 toobuild 一個 Azure 位置中的所有資源。
9. 確認**Pin toodashboard**已核取。 這個選擇性的設定放 hello Azure 入口網站的儀表板中的 hello 資源群組的捷徑。

   ![資源群組](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-resourcegroup.png)

10. 按一下**建立**toocreate hello 資源群組。

Azure 會建立 hello 資源群組] 和 [pin 捷徑 toohello 資源群組 hello 入口網站中。

## <a name="create-hello-network-and-subnets"></a>建立 hello 網路和子網路
hello 下一個步驟是 toocreate hello 網路與 hello Azure 資源群組中的子網路。

hello 方案會使用兩個子網路中的一個虛擬網路。 hello[虛擬網路概觀](../../../virtual-network/virtual-networks-overview.md)提供在 Azure 中網路的詳細資訊。

toocreate hello 虛擬網路：

1. 在 hello Azure 入口網站，在資源群組中，按一下  **+ 加**。 Azure 會開啟 hello**一切**刀鋒視窗。

   ![新增項目](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/02-newiteminrg.png)
2. 搜尋 **虛擬網路**。

     ![搜尋虛擬網路](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/04-findvirtualnetwork.png)
3. 按一下 [虛擬網路] 。
4. 在 hello**虛擬網路**刀鋒視窗中，按一下 hello**資源管理員**部署模型，然後再按一下**建立**。

    hello 下表顯示 hello 虛擬網路的 hello 設定：

   | **欄位** | 值 |
   | --- | --- |
   | **名稱** |autoHAVNET |
   | **位址空間** |10.33.0.0/24 |
   | **子網路名稱** |Admin |
   | **子網路位址範圍** |10.33.0.0/29 |
   | **訂用帳戶** |指定您想 toouse hello 訂用帳戶。 如果您只有一個訂用帳戶，則**訂用帳戶**為留白。 |
   | **資源群組** |選擇**使用現有**並挑選 hello hello 資源群組名稱。 |
   | **位置** |指定 hello Azure 位置。 |

   位址空間和子網路位址範圍可能從 hello 資料表不同。 根據您的訂閱，hello 入口網站會建議可用的位址空間和對應的子網路位址範圍。 如果沒有足夠的位址空間可供使用，請使用不同的訂用帳戶。

   使用 hello 子網路名稱的 hello 範例**Admin**。此子網路是 hello 網域控制站。

5. 按一下 [建立] 。

   ![設定虛擬網路，hello](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/06-configurevirtualnetwork.png)

Azure 會讓您返回 toohello 入口網站儀表板，並建立 hello 新網路時通知您。

### <a name="create-a-second-subnet"></a>建立第二個子網路
hello 新的虛擬網路有一個子網路，名為**Admin**。 hello 網域控制站會使用此子網路。 SQL Server Vm hello 使用第二個名為的子網路**SQL**。 tooconfigure 此子網路：

1. 按一下 儀表板，您所建立的 hello 資源群組**SQL-HA-RG**。 找出 hello 下的資源群組中的 hello 網路**資源**。

    如果**SQL-HA-RG**看不到，尋找按一下**資源群組**與篩選的 hello 資源群組名稱。
2. 按一下**autoHAVNET**上 hello 的資源清單。 Azure 開啟 hello 網路組態刀鋒視窗。
3. 在 [hello **autoHAVNET**虛擬網路] 刀鋒視窗底下**設定**，按一下**子網路**。

    請注意，您已經建立 hello 子網路。

   ![設定虛擬網路，hello](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/07-addsubnet.png)
5. 建立第二個子網路。 按一下 [+ 子網路] 。
6. 在 hello**加入子網路**刀鋒視窗中，輸入設定 hello 子網路**sqlsubnet**下**名稱**。 Azure 會自動指定有效的 [位址範圍] 。 確認此位址範圍中至少有 10 個位址。 在生產環境中，您可能需要更多位址。
7. 按一下 [確定] 。

    ![設定虛擬網路，hello](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/08-configuresubnet.png)

hello 下表摘要說明 hello 網路組態設定：

| **欄位** | 值 |
| --- | --- |
| **名稱** |**autoHAVNET** |
| **位址空間** |這個值取決於您的訂用帳戶中的 hello 可用的位址空間。 一般的值是 10.0.0.0/16。 |
| **子網路名稱** |**admin** |
| **子網路位址範圍** |這個值取決於您的訂用帳戶中的 hello 可用的位址範圍。 一般的值是 10.0.0.0/24。 |
| **子網路名稱** |**sqlsubnet** |
| **子網路位址範圍** |這個值取決於您的訂用帳戶中的 hello 可用的位址範圍。 一般的值是 10.0.1.0/24。 |
| **訂用帳戶** |指定您想 toouse hello 訂用帳戶。 |
| **資源群組** |**SQL-HA-RG** |
| **位置** |指定 hello 您選擇 hello 資源群組的相同位置。 |

## <a name="create-availability-sets"></a>建立可用性設定組

建立虛擬機器之前，您會需要 toocreate 可用性設定組。 可用性設定組的規劃或未規劃的維護事件 hello 停機時間減少。 Azure 可用性設定組是 Azure 置於實體容錯網域和更新網域上的邏輯資源群組。 「 故障 」 網域可確保 hello 可用性設定組的 hello 成員有不同的電源和網路資源。 更新網域可確保，hello 可用性設定組的成員不會導致在 hello 維護相同的時間。 如需詳細資訊，請參閱[管理虛擬機器可用性 hello](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

您需要兩個可用性設定組。 其中一個是 hello 網域控制站。 hello 第二個是 hello SQL Server Vm。

可用性設定 toohello 資源群組，請按一下的 toocreate**新增**。 輸入篩選 hello 結果**可用性設定組**。 按一下**可用性設定組**在 hello 結果，然後按一下**建立**。

設定根據 toohello 參數 hello 下表中的兩個可用性設定組：

| **欄位** | 網域控制站可用性設定組 | SQL Server 可用性設定組 |
| --- | --- | --- |
| **名稱** |adavailabilityset |sqlavailabilityset |
| **資源群組** |SQL-HA-RG |SQL-HA-RG |
| **容錯網域** |3 |3 |
| **更新網域** |5 |3 |

建立 hello 可用性設定組之後，傳回 toohello 資源群組中 hello Azure 入口網站。

## <a name="create-domain-controllers"></a>建立網域控制站
在您建立 hello 網路、 子網路，可用性設定組及使用網際網路對向負載平衡器後，您準備 toocreate hello hello 網域控制站的虛擬機器。

### <a name="create-virtual-machines-for-hello-domain-controllers"></a>建立虛擬機器的 hello 網域控制站
toocreate 而且設定 hello 網域控制站，則傳回 toohello **SQL-HA-RG**資源群組。

1. 按一下 [新增] 。 hello**一切**刀鋒視窗隨即開啟。
2. 輸入 **Windows Server 2016 資料中心**。
3. 按一下 **Windows Server 2016 資料中心**。 在 hello **Windows Server 2016 Datacenter**刀鋒視窗中，確認該 hello 部署模型**資源管理員**，然後按一下**建立**。 Azure 會開啟 hello**建立虛擬機器**刀鋒視窗。

重複上述步驟 toocreate 兩部虛擬機器的 hello。 Hello 兩部虛擬機器的名稱：

* ad-primary-dc
* ad-secondary-dc

  > [!NOTE]
  > hello **ad 次要 dc**虛擬機器是選擇性的 tooprovide 的 Active Directory 網域服務的高可用性。
  >
  >

hello 下表顯示這兩個機器 hello 設定：

| **欄位** | 值 |
| --- | --- |
| **名稱** |第一網域控制站：ad-primary-dc。</br>第二網域控制站：ad-secondary-dc。 |
| **VM 磁碟類型** |SSD |
| **使用者名稱** |DomainAdmin |
| **密碼** |Contoso!0000 |
| **訂用帳戶** |*您的訂用帳戶* |
| **資源群組** |SQL-HA-RG |
| **位置** |*您的位置* |
| **大小** |DS1_V2 |
| **儲存體** | [使用受控磁碟] - [是] |
| **虛擬網路** |autoHAVNET |
| **子網路** |admin |
| **公用 IP 位址** |*Hello VM 相同的名稱* |
| **網路安全性群組** |*Hello VM 相同的名稱* |
| **可用性設定組** |adavailabilityset </br>**容錯網域**：2</br>**更新網域**：2|
| **診斷** |已啟用 |
| **診斷儲存體帳戶** |*自動建立* |

   >[!IMPORTANT]
   >您只可以在建立 VM 時才可將 VM 置於可用性設定組。 您無法變更 hello 可用性設定組之後建立的 VM。 請參閱[管理虛擬機器可用性 hello](../manage-availability.md)。

Azure 會建立 hello 虛擬機器。

建立 hello 虛擬機器之後，設定 hello 網域控制站。

### <a name="configure-hello-domain-controller"></a>設定 hello 網域控制站
在 hello 下列步驟中，設定 hello **ad 主要 dc**為 corp.contoso.com 的網域控制站電腦。

1. 在 hello 入口網站中，開啟 hello **SQL-HA-RG**資源群組和選取 hello **ad 主要 dc**機器。 在 hello **ad 主要 dc**刀鋒視窗中，按一下**連接**tooopen RDP 檔，以取得遠端桌面的存取。

    ![Tooa 虛擬機器連線](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/20-connectrdp.png)
2. 使用所設定的系統管理員帳戶 (**\DomainAdmin**) 和密碼 (**Contoso!0000**) 來登入。
3. 根據預設，hello**伺服器管理員**應該顯示儀表板。
4. 按一下 hello**新增角色及功能**hello 儀表板上的連結。

    ![伺服器總管 - 新增角色](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
5. 選取**下一步**直到 toohello**伺服器角色**> 一節。
6. 選取 hello **Active Directory 網域服務**和**DNS 伺服器**角色。 出現提示時，請新增這些角色所需的任何其他功能。

   > [!NOTE]
   > Windows 會顯示無靜態 IP 位址的警告。 如果您要測試 hello 組態，按一下**繼續**。 生產案例，請在 hello Azure 入口網站中設定 hello IP 位址 toostatic 或[使用 PowerShell tooset hello 靜態 IP 位址的 hello 網域控制站機器](../../../virtual-network/virtual-networks-reserved-private-ip.md)。
   >
   >

    ![[新增角色] 對話方塊](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/23-addroles.png)
7. 按一下**下一步**直到您到達 hello**確認**> 一節。 選取 hello**必要時自動重新啟動 hello 目的地伺服器**核取方塊。
8. 按一下 [Install] 。
9. Hello 功能完成安裝，則傳回 toohello 之後**伺服器管理員**儀表板。
10. 選取新的 hello **AD DS** hello 左側窗格上的選項。
11. 按一下 hello**詳細**hello 黃色警告列上的連結。

    ![在 hello DNS 伺服器 VM 上的 AD DS 對話方塊](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/24-addsmore.png)
12. 在 [hello**動作**hello 的資料行**所有伺服器工作詳細資料**] 對話方塊中，按一下**升級此伺服器 tooa 網域控制站**。
13. 在 hello **Active Directory 網域服務設定精靈**，使用下列值的 hello:

    | **Page** | 設定 |
    | --- | --- |
    | **部署組態** |**新增樹系**<br/> **根網域名稱** = corp.contoso.com |
    | **網域控制站選項** |**DSRM 密碼** = Contoso!0000<br/>**確認密碼** = Contoso!0000 |
14. 按一下**下一步**透過 toogo hello hello 精靈中的其他頁面。 在 hello**必要條件檢查**頁面上，確認您看到下列訊息的 hello:**順利通過所有先決條件檢查**。 您可以檢閱任何適用的警告訊息，但可能 toocontinue hello 安裝。
15. 按一下 [Install] 。 hello **ad 主要 dc**自動重新啟動虛擬機器。

### <a name="note-hello-ip-address-of-hello-primary-domain-controller"></a>請注意 hello hello 主要網域控制站的 IP 位址

使用 hello 主要網域控制站的 DNS。 請注意 hello 主要網域控制站 IP 位址。

其中一種方式 tooget hello 主要網域控制站 IP 位址是透過 hello Azure 入口網站。

1. 在 hello Azure 入口網站，開啟 hello 資源群組。

2. 按一下 hello 主要網域控制站。

3. 在 hello 主要網域控制站刀鋒視窗中，按一下 **網路介面**。

![網路介面](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/25-primarydcip.png)

請注意此伺服器 hello 私人 IP 位址。

### <a name="configure-hello-virtual-network-dns"></a>設定虛擬網路 DNS hello
在建立 hello 第一個網域控制站，並啟用 DNS hello 第一部伺服器之後，設定 hello 虛擬網路 toouse 此伺服器的 DNS。

1. 在 hello Azure 入口網站，按一下 hello 虛擬網路。

2. 在 [設定] 下方，按一下 [DNS 伺服器]。

3. 按一下**自訂**，然後輸入 hello 主要網域控制站的 hello 私人 IP 位址。

4. 按一下 [儲存] 。

### <a name="configure-hello-second-domain-controller"></a>設定 hello 第二個網域控制站
Hello 主要網域控制站重新開機之後，您可以設定 hello 第二個網域控制站。 這個選擇性步驟適用於高可用性。 請遵循這些步驟 tooconfigure hello 第二個網域控制站：

1. 在 hello 入口網站中，開啟 hello **SQL-HA-RG**資源群組和選取 hello **ad 次要 dc**機器。 在 hello **ad 次要 dc**刀鋒視窗中，按一下 **連接**tooopen RDP 檔，以取得遠端桌面存取。
2. 使用設定的管理員帳戶登入 toohello VM (**BUILTIN\DomainAdmin**) 和密碼 (**Contoso ！ 0000**)。
3. 變更 hello 慣用 DNS 伺服器位址 toohello 位址 hello 網域控制站。
4. 在**網路和共用中心**，按一下 hello 網路介面。
   ![網路介面](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/26-networkinterface.png)

5. 按一下 [內容] 。
6. 選取 [網際網路通訊協定第 4 版 (TCP/IPv4)]，然後按一下 [內容]。
7. 選取**下列的 DNS 伺服器位址使用 hello**及指定位址中的 hello 主要網域控制站，hello**慣用 DNS 伺服器**。
8. 按一下**確定**，然後**關閉**toocommit hello 變更。 現在您已經準備可以 toojoin hello VM 太**corp.contoso.com**。

   >[!IMPORTANT]
   >如果您遺失 hello 連接 tooyour 遠端桌面變更 hello DNS 設定之後，請移 toohello Azure 入口網站並重新啟動 hello 虛擬機器。

9. 從 hello 遠端桌面 toohello 次要網域控制站，開啟**伺服器管理員儀表板**。
10. 按一下 hello**新增角色及功能**hello 儀表板上的連結。

    ![伺服器總管 - 新增角色](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
11. 選取**下一步**直到 toohello**伺服器角色**> 一節。
12. 選取 hello **Active Directory 網域服務**和**DNS 伺服器**角色。 出現提示時，請新增這些角色所需的任何其他功能。
13. Hello 功能完成安裝，則傳回 toohello 之後**伺服器管理員**儀表板。
14. 選取新的 hello **AD DS** hello 左側窗格上的選項。
15. 按一下 hello**詳細**hello 黃色警告列上的連結。
16. 在 [hello**動作**hello 的資料行**所有伺服器工作詳細資料**] 對話方塊中，按一下**升級此伺服器 tooa 網域控制站**。
17. 在下**部署組態**，選取**新增網域控制站 tooan 現有網域**。
   ![部署組態](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/28-deploymentconfig.png)
18. 按一下 [選取] 。
19. 連接使用 hello 系統管理員帳戶 (**CORP.CONTOSO.COM\domainadmin**) 和密碼 (**Contoso ！ 0000**)。
20. 在**從 hello 樹系中選取網域**，按一下您的網域，然後按一下**確定**。
21. 在**網域控制站選項**、 使用 hello 預設值，以及設定 DSRM 密碼。

   >[!NOTE]
   >hello **DNS 選項**頁面可能會警告您，無法建立此 DNS 伺服器的委派。 您在非生產環境中可以忽略這個警告。
22. 按一下**下一步**直到 hello 對話方塊達到 hello**必要條件**檢查。 然後按一下 [安裝] 。

Hello 伺服器完成 hello 組態變更之後，重新啟動伺服器 hello。

### <a name="add-hello-private-ip-address-toohello-second-domain-controller-toohello-vpn-dns-server"></a>新增 hello 私用 IP 位址 toohello 第二個網域控制站 toohello VPN DNS 伺服器

在 hello Azure 入口網站，在 虛擬網路，變更 hello DNS 伺服器 tooinclude hello hello 次要網域控制站 IP 位址。 這可讓 hello DNS 服務備援性。

### <a name=DomainAccounts></a>設定 hello 的網域帳戶

在 hello 下一個步驟中，您可以設定 hello Active Directory 帳戶。 hello 下表顯示 hello 帳戶：

| |安裝帳戶<br/> |sqlserver-0 <br/>SQL Server 和 SQL Agent 服務帳戶 |sqlserver-1<br/>SQL Server 和 SQL Agent 服務帳戶
| --- | --- | --- | ---
|**名字** |Install |SQLSvc1 | SQLSvc2
|**使用者 SamAccountName** |Install |SQLSvc1 | SQLSvc2

使用下列步驟 toocreate hello 每個帳戶。

1. 登入 toohello **ad 主要 dc**機器。
2. 在 伺服器管理員 中，選取 工具，然後按一下Active Directory 管理中心。   
3. 選取**corp （本機）** hello 左窗格中。
4. 在右邊的 hello**工作**窗格中，選取**新增**，然後按一下**使用者**。
   ![Active Directory 管理中心](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/29-addcnewuser.png)

   >[!TIP]
   >設定每個帳戶的複雜密碼。<br/> 對於非生產環境中，設定 hello 使用者帳戶 toonever 過期。

5. 按一下**確定**toocreate hello 使用者。
6. 重複先前 hello 三個帳戶的每個步驟的 hello。

### <a name="grant-hello-required-permissions-toohello-installation-account"></a>Hello 所需的權限授與 toohello 安裝帳戶
1. 在 hello **Active Directory 管理中心**，選取**corp （本機）** hello 左窗格中。 接著在右手邊的 hello**工作**] 窗格中，按一下 [**屬性**。

    ![公司使用者內容](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/31-addcproperties.png)
2. 選取**延伸**，然後按一下hello**進階**按鈕 hello**安全性** 索引標籤。
3. 在 hello **corp 的進階安全性設定** 對話方塊中，按一下 **新增**。
4. 按一下 選取主體、搜尋 **CORP\Install**，然後按一下確定。
5. 選取 hello**讀取全部內容**核取方塊。

6. 選取 hello**建立電腦物件**核取方塊。

     ![公司使用者權限](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/33-addpermissions.png)
7. 按一下 [確定]，再按一下 [確定]。 關閉 hello **corp**屬性 視窗。

現在您已完成設定 Active Directory 與 hello 使用者物件，建立兩個 SQL Server Vm 以及將見證伺服器 VM。 然後聯結所有的三個 toohello 網域。

## <a name="create-sql-server-vms"></a>建立 SQL Server VM

建立第三部額外的虛擬機器。 hello 解決方案需要兩部虛擬機器與 SQL Server 執行個體。 第三虛擬機器的功能為見證。 Windows Server 2016 會使用[雲端見證](http://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness)，但為了與舊版作業系統一致，本文件使用虛擬機器作為見證。  

在繼續之前，請考慮下列 deisign 決策的 hello。

* **儲存體 - Azure 受控磁碟**

   Hello 虛擬機器存放裝置，使用 Azure 受管理的磁碟。 Microsoft 為 SQL Server 虛擬機器建議受控磁碟。 管理磁碟 hello 幕後的控制代碼儲存體。 此外，當與受管理磁碟的虛擬機器都處於 hello 相同可用性設定組，Azure 會發佈 hello 存放裝置資源 tooprovide 適當備援。 如需其他資訊，請參閱 [Azure 受控磁碟概觀 (英文)](../managed-disks-overview.md)。 如需可用性設定組中受控磁碟的具體資訊，請參閱[在可用性設定組中使用 VM 的受控磁碟 (英文)](../manage-availability.md#use-managed-disks-for-vms-in-an-availability-set)。

* **網路 - 生產環境中的私人 IP 位址**

   Hello 虛擬機器，本教學課程會使用公用 IP 位址。 這可讓遠端連線，直接 toohello 虛擬機器 hello 網際網路-它容易設定步驟。 在實際執行環境中，Microsoft 建議僅私人 IP 位址順序 tooreduce hello 弱點使用量 hello SQL Server 執行個體 VM 資源。

### <a name="create-and-configure-hello-sql-server-vms"></a>建立及設定 hello SQL Server Vm
接下來，建立三個 VM，亦即兩個 SQL Server VM 和一個適用於其他叢集節點的 VM。 toocreate 每個 hello Vm，請返回 toohello **SQL-HA-RG**資源群組中，按一下 **新增**、 hello 適當的主機庫項目的搜尋中，按一下**虛擬機器**，然後按一下**從組件庫**。 在下列資料表 toohelp 建立 hello Vm hello 使用 hello 資訊：


| Page | VM1 | VM2 | VM3 |
| --- | --- | --- | --- |
| 選取 hello 適當的主機庫項目 |**Windows Server 2016 Datacenter** |**SQL Server 2016 SP1 Enterprise on Windows Server 2016** |**SQL Server 2016 SP1 Enterprise on Windows Server 2016** |
| 虛擬機器組態 **基本** |**名稱** = cluster-fsw<br/>**使用者名稱** = DomainAdmin<br/>**密碼** = Contoso!0000<br/>**訂用帳戶** = 您的訂用帳戶<br/>**資源群組** = SQL-HA-RG<br/>**位置** = 您的 Azure 位置 |**名稱** = sqlserver-0<br/>**使用者名稱** = DomainAdmin<br/>**密碼** = Contoso!0000<br/>**訂用帳戶** = 您的訂用帳戶<br/>**資源群組** = SQL-HA-RG<br/>**位置** = 您的 Azure 位置 |**名稱** = sqlserver-1<br/>**使用者名稱** = DomainAdmin<br/>**密碼** = Contoso!0000<br/>**訂用帳戶** = 您的訂用帳戶<br/>**資源群組** = SQL-HA-RG<br/>**位置** = 您的 Azure 位置 |
| 虛擬機器組態 **大小** |**大小** = DS1\_V2 (1 個核心，3.5 GB) |**大小** = DS2\_V2 (2 個核心，7 GB)</br>hello 大小必須支援 SSD 儲存裝置 （Premium 磁碟支援。 )) |**大小** = DS2\_V2 (2 個核心，7 GB) |
| 虛擬機器組態 **設定** |**儲存體**：使用受控磁碟。<br/>**虛擬網路** = autoHAVNET<br/>**子網路** = sqlsubnet(10.1.1.0/24)<br/>**公用 IP 位址**自動產生。<br/>**網路安全性群組** = 無<br/>**監視診斷** = 啟用<br/>**診斷儲存體帳戶** = 使用自動產生的儲存體帳戶<br/>**可用性設定組** = sqlAvailabilitySet<br/> |**儲存體**：使用受控磁碟。<br/>**虛擬網路** = autoHAVNET<br/>**子網路** = sqlsubnet(10.1.1.0/24)<br/>**公用 IP 位址**自動產生。<br/>**網路安全性群組** = 無<br/>**監視診斷** = 啟用<br/>**診斷儲存體帳戶** = 使用自動產生的儲存體帳戶<br/>**可用性設定組** = sqlAvailabilitySet<br/> |**儲存體**：使用受控磁碟。<br/>**虛擬網路** = autoHAVNET<br/>**子網路** = sqlsubnet(10.1.1.0/24)<br/>**公用 IP 位址**自動產生。<br/>**網路安全性群組** = 無<br/>**監視診斷** = 啟用<br/>**診斷儲存體帳戶** = 使用自動產生的儲存體帳戶<br/>**可用性設定組** = sqlAvailabilitySet<br/> |
| 虛擬機器組態 **SQL Server 設定** |不適用 |**SQL 連線** = 私用 (在虛擬網路內)<br/>**連接埠** = 1433<br/>**SQL 驗證** = 停用<br/>**儲存體組態** = 一般<br/>**自動修補** = 星期日 2:00<br/>**自動備份** = 停用</br>**Azure 金鑰保存庫整合** = 已停用 |**SQL 連線** = 私用 (在虛擬網路內)<br/>**連接埠** = 1433<br/>**SQL 驗證** = 停用<br/>**儲存體組態** = 一般<br/>**自動修補** = 星期日 2:00<br/>**自動備份** = 停用</br>**Azure 金鑰保存庫整合** = 已停用 |

<br/>

> [!NOTE]
> hello 機器大小，我們建議是為了在 Azure Vm 中測試可用性群組。 Hello 實際執行工作負載的最佳效能，請參閱 SQL Server 機器大小和組態中的 hello 建議[效能最佳做法適用於 SQL Server 在 Azure 虛擬機器](virtual-machines-windows-sql-performance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
>
>

Hello 三個 Vm 完整佈建之後，您需要 toojoin 它們 toohello **corp.contoso.com**網域和授與 CORP\Install 管理權限 toohello 機器。

### <a name="joinDomain"></a>加入 hello 伺服器 toohello 網域

您現在可以 toojoin 太 hello Vm**corp.contoso.com**。請勿 hello 下列 hello SQL Server Vm 和 hello 檔案共用見證伺服器：

1. 從遠端連線的虛擬機器 toohello **BUILTIN\DomainAdmin**。
2. 在 [伺服器管理員] 中，按一下 [本機伺服器]。
3. 按一下 hello **WORKGROUP**連結。
4. 在 hello**電腦名稱**區段中，按一下**變更**。
5. 選取 hello**網域**核取方塊，然後輸入**corp.contoso.com** hello 文字方塊中。 按一下 [確定] 。
6. 在 hello **Windows 安全性**快顯對話方塊中，指定 hello hello 預設網域系統管理員帳戶的認證 (**CORP\DomainAdmin**) 和 hello 密碼 (**Contoso ！ 0000**).
7. 當您看見 hello 「  褖畫惎 toohello corp.contoso.com 網域 」 訊息時，按一下**確定**。
8. 按一下**關閉**，然後按一下**立即重新啟動**hello 快顯對話方塊中。

### <a name="add-hello-corpinstall-user-as-an-administrator-on-each-cluster-vm"></a>將 hello Corp\Install 使用者新增為每個叢集 VM 的系統管理員

Hello 網域的成員身分的每個虛擬機器重新啟動之後，新增**CORP\Install** hello 本機 administrators 群組的成員身分。

1. 等候 hello VM 重新啟動，然後太啟動 hello RDP 檔案中的 hello 主要網域控制站 toosign 再次從**sqlserver 0**使用 hello **CORP\DomainAdmin**帳戶。
   >[!TIP]
   >請確定登入 hello 網域系統管理員帳戶。 在 hello 先前步驟中，您已使用 hello 內建在系統管理員帳戶。 現在已 hello 伺服器 hello 網域中，使用 hello 網域帳戶。 在您的 RDP 工作階段中，指定 *DOMAIN*\\*username*。

2. 在 伺服器管理員 中選取 工具，然後按一下電腦管理。
3. 在 hello**電腦管理**視窗中，展開**本機使用者和群組**，然後選取**群組**。
4. 按兩下 hello**管理員**群組。
5. 在 hello**系統管理員屬性** 對話方塊中，按一下 hello**新增** 按鈕。
6. 輸入 hello 使用者**CORP\Install**，然後按一下**確定**。
7. 按一下**確定**tooclose hello**系統管理員內容**對話方塊。
8. 對於重複 hello 上一個步驟**sqlserver 1**和**叢集 fsw**。

### <a name="setServiceAccount"></a>設定 hello SQL Server 服務帳戶

在每個 SQL Server VM，設定 hello SQL Server 服務帳戶。 使用 hello 帳戶時建立您[hello 網域帳戶設定](#DomainAccounts)。

1. 啟動 **SQL Server 組態管理員**。
2. Hello SQL Server 服務，以滑鼠右鍵按一下，然後按一下**屬性**。
3. 設定 hello 帳戶和密碼。
4. 上重複這些步驟 hello 其他 SQL Server VM。  

SQL Server 可用性群組，每個 SQL Server VM 會需要 toorun 以網域帳戶。

### <a name="create-a-sign-in-on-each-sql-server-vm-for-hello-installation-account"></a>在 hello 安裝帳戶的每個 SQL Server VM 上建立登入

使用 hello 安裝帳戶 (CORP\install) tooconfigure hello 可用性群組。 此帳戶必須隸屬 hello toobe **sysadmin**每個 SQL Server VM 上的固定的伺服器角色。 hello 下列步驟建立的登入 hello 安裝帳戶：

1. 透過 hello 遠端桌面通訊協定 (RDP) 連線 toohello 伺服器，使用 hello  *\<MachineName\>\DomainAdmin*帳戶。

1. 開啟 SQL Server Management Studio 並連接 toohello 本機 SQL Server 執行個體。

1. 在 [物件總管] **中**，按一下 [安全性]。

1. 以滑鼠右鍵按一下 [登入]。 按一下 [新增登入]。

1. 在 [登入 - 新增] 中，按一下 [搜尋]。

1. 按一下 [位置]。

1. 輸入 hello 網域系統管理員的 網路認證。

1. 使用 hello 安裝帳戶。

1. 設定登入 toobe hello 的 hello 成員**sysadmin**固定的伺服器角色。

1. 按一下 [確定] 。

重複上述步驟 hello 其他 SQL Server VM 的 hello。

## <a name="add-failover-clustering-features-tooboth-sql-server-vms"></a>新增容錯移轉叢集功能 tooboth SQL Server Vm

請勿 hello tooadd 容錯移轉叢集功能，這兩個 SQL Server Vm 上：

1. 透過 hello 遠端桌面通訊協定 (RDP) 連線 toohello SQL Server 虛擬機器，使用 hello *CORP\install*帳戶。 開啟 [伺服器管理員儀表板] 。
2. 按一下 hello**新增角色及功能**hello 儀表板上的連結。

    ![伺服器總管 - 新增角色](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
3. 選取**下一步**直到 toohello**伺服器功能**> 一節。
4. 在 [功能] 中，選取 [容錯移轉叢集]。
5. 新增任何其他必要的功能。
6. 按一下**安裝**tooadd hello 功能。

Hello 上重複步驟 hello 其他 SQL Server VM。

## <a name="a-nameendpoint-firewall-configure-hello-firewall-on-each-sql-server-vm"></a><a name="endpoint-firewall">每個 SQL Server VM 上 hello 防火牆設定

hello 方案需要下列 toobe hello 防火牆中開啟的 TCP 連接埠的 hello:

- **SQL Server VM：**<br/>
   SQL Server 預設執行個體的連接埠 1433。
- **Azure Load Balancer 探查：**<br/>
   任何可用的連接埠。 範例會經常使用 59999。
- **資料庫鏡像端點：** <br/>
   任何可用的連接埠。 範例會經常使用 5022。

hello 防火牆連接埠需要 toobe 在這兩個 SQL Server Vm 上開啟。

開啟 hello 連接埠的 hello 方法取決於您所使用的 hello 防火牆解決方案。 hello 下一節說明 tooopen hello Windows 防火牆中的連接埠。 開啟 hello 需要在每個 SQL Server Vm 上的連接埠。

### <a name="open-a-tcp-port-in-hello-firewall"></a>在 hello 防火牆中開啟 TCP 連接埠

1. 在 hello 第一個 SQL Server**啟動**畫面上，啟動**具有進階安全性的 Windows 防火牆**。
2. 在 hello 左窗格中，選取 **輸入規則**。 在 hello 右窗格中，按一下 **新規則**。
3. 針對 [規則類型]，選擇 [連接埠]。
4. Hello 埠指定**TCP**和型別 hello 適當的連接埠號碼。 請參閱下列範例中的 hello:

   ![SQL 防火牆](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/35-tcpports.png)

5. 按一下 [下一步] 。
6. 在 hello**動作**頁面上，保留**允許 hello 連線**選取，然後再按一下**下一步**。
7. 在 hello**設定檔**頁面上，接受 hello 預設設定，然後按**下一步**。
8. 在 hello**名稱**頁面上，指定規則的名稱 (例如**Azure LB 探查**) 在 hello**名稱**文字方塊，然後再按一下**完成**。

重複這些步驟在 hello 第二個 SQL Server VM。

## <a name="next-steps"></a>後續步驟

* [在 Azure 虛擬機器上建立 SQL Server Always On 可用性群組](virtual-machines-windows-portal-sql-availability-group-tutorial.md)
