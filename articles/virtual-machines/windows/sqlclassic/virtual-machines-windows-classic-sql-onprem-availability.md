---
title: "aaaExtend 內部 Alwayson 可用性群組 tooAzure |Microsoft 文件"
description: "本教學課程會使用與 hello 傳統部署模型，建立的資源，並描述如何 toouse 會 hello tooadd SQL Server Management Studio (SSMS) 中的加入複本精靈在 Azure 中的 Alwayson 可用性群組複本。"
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 7ca7c423-8342-4175-a70b-d5101dfb7f23
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: 51fe117b40d69706b35f30101538a7a36116e128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="extend-on-premises-always-on-availability-groups-tooazure"></a>擴充內部部署 Alwayson 可用性群組 tooAzure
Always On 可用性群組可透過新增次要複本，為資料庫群組提供高可用性。 如果發生故障，這些複本便可容錯移轉資料庫。 此外，它們可以是使用的 toooffload 讀取工作負載或備份工作。

您可以擴充在內部部署可用性群組 tooMicrosoft Azure 佈建 SQL server 的一或多個 Azure Vm，然後將它們加入為複本 tooyour 內部部署可用性群組。

本教學課程假設您擁有 hello 下列：

* 有效的 Azure 訂用帳戶。 您可以 [註冊免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* 現有的 Always On 可用性群組內部部署。 如需可用性群組的詳細資訊，請參閱 [Always On 可用性群組](https://msdn.microsoft.com/library/hh510230.aspx)。
* Hello 之間的連線在內部部署網路與 Azure 虛擬網路。 如需有關如何建立此虛擬網路的詳細資訊，請參閱[建立站台間連線使用 hello Azure 入口網站 （傳統）](../../../vpn-gateway/vpn-gateway-howto-site-to-site-classic-portal.md)。

> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

## <a name="add-azure-replica-wizard"></a>加入 Azure 複本精靈
這個區段會顯示如何 toouse hello**加入 Azure 複本精靈**tooextend 您 Alwayson 可用性群組解決方案 tooinclude Azure 複本。

> [!IMPORTANT]
> hello**加入 Azure 複本精靈**只支援與 hello 傳統部署模型所建立的虛擬機器。 新的 VM 部署應該使用 hello 較新的資源管理員模型。 如果您使用 Vm 與資源管理員，您必須手動加入 hello 次要的 Azure 複本使用 Transact SQL commmands （此處未顯示）。 此精靈在 hello 資源管理員狀況中無法運作。

1. 在 SQL Server Management Studio 中，依序展開 [Always On 高可用性] > [可用性群組] > [您的可用性群組名稱]。
2. 以滑鼠右鍵按一下 [可用性複本]，然後按一下 [新增複本]。
3. 根據預設，hello**將複本加入 tooAvailability 群組精靈**隨即出現。 按一下 [下一步] 。  如果您已選取 hello**不要再顯示此頁面**hello hello 頁底端期間選項先前啟動此精靈，這個畫面將不會顯示。
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742861.png)
4. 您將需要的 tooconnect tooall 現有次要複本。 您可以按一下 [連接...] 位於每個複本旁，或可以按一下 [全部連接...] 在 hello 囉 」 畫面底部。 在驗證之後，按一下 **下一步**tooadvance toohello 下一個畫面。
5. 在 [hello**指定複本**] 頁面上，多個索引標籤會列出 hello 頂端：**複本**，**端點**，**備份喜好設定**，和**接聽程式**。 從 hello**複本**索引標籤上，按一下 **加入 Azure 複本...** toolaunch hello 加入 Azure 複本精靈。
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742863.png)
6. 如果您已安裝前，請從 hello 本機 Windows 憑證存放區中選取現有的 Azure 管理憑證。 選取或輸入 hello Azure 訂用帳戶 id，如果您已使用前一個。 您可以按一下 下載 toodownload 和安裝 Azure 管理憑證，並下載 hello 使用 Azure 帳戶的訂用帳戶清單。
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742864.png)
7. 您將會填入值，將會使用的 toocreate hello Azure 虛擬機器 (VM) 將要裝載 hello 複本 hello 頁面上的每個欄位。
   
   | 設定 | 說明 |
   | --- | --- |
   | **映像** |選取所需的 hello 組合的 OS 與 SQL Server |
   | **VM 大小** |選取最適合您的業務需求的 VM 大小 hello |
   | **VM 名稱** |指定唯一的名稱，如 hello 新的 VM。 hello 名稱必須介於 3 到 15 個字元，可以包含字母、 數字和連字號，並且必須以字母開頭和結尾以字母或數字。 |
   | **VM 使用者名稱** |指定將會變成 hello hello VM 上的系統管理員帳戶的使用者名稱 |
   | **VM 系統管理員密碼** |指定 hello 新帳戶的密碼 |
   | **確認密碼** |確認 hello hello 新帳戶的密碼 |
   | **虛擬網路** |指定 Azure 虛擬網路的新 VM 應使用該 hello hello。 如需虛擬網路的詳細資訊，請參閱 [虛擬網路概觀](../../../virtual-network/virtual-networks-overview.md)。 |
   | **虛擬網路子網路** |指定新 VM 應使用該 hello hello 虛擬網路子網路 |
   | **網域** |確認 hello 預先填入的 hello 定義域值正確 |
   | **網域使用者名稱** |指定的帳戶是 hello hello 本機叢集節點上的本機 administrators 群組中。 |
   | **密碼** |指定 hello hello 網域使用者名稱的密碼 |
8. 按一下**確定**toovalidate hello 部署設定。
9. 接著會顯示法律條款。 閱讀，然後按一下**確定**如果您同意 toothese 條款。
10. hello**指定複本**頁面會再次顯示。 確認 hello 新的 Azure 複本上 hello hello 設定**複本**，**端點**，和**備份喜好設定**索引標籤。 修改設定 toomeet 您的業務需求。  如需有關這些索引標籤上所含的 hello 參數的詳細資訊，請參閱[指定複本頁面 （新增可用性群組精靈/加入複本精靈）](https://msdn.microsoft.com/library/hh213088.aspx)。請注意，無法使用 hello 接聽程式索引標籤包含 Azure 複本的可用性群組建立接聽程式。 此外，如果接聽程式已建立先前 toolaunching hello 精靈，您會收到指出它不支援在 Azure 中的訊息。 我們將探討如何 toocreate 接聽程式在 hello**建立可用性群組接聽程式**> 一節。
    
     ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742865.png)
11. 按一下 [下一步] 。
12. 選取您想要在 hello toouse hello 資料同步處理方法**選取初始資料同步處理**頁面上，按一下 **下一步**。 在大部分的情況下，請選取 [完整資料同步處理] 。 如需資料同步處理方法的詳細資訊，請參閱 [選取初始資料同步處理頁面 (Always On 可用性群組精靈)](https://msdn.microsoft.com/library/hh231021.aspx)。
13. 檢閱上 hello hello 結果**驗證**頁面。 更正未處理的問題，然後再視需要重新執行 hello 驗證。 按一下 [下一步] 。
    
     ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742866.png)
14. 檢閱上 hello 的 hello 設定**摘要**頁面上，然後按一下 **完成**。
15. hello 佈建程序開始。 Hello 精靈成功完成時，按一下**關閉**tooexit 超出 hello 精靈。

> [!NOTE]
> hello 加入 Azure 複本精靈會建立記錄檔中 Users\User Name\AppData\Local\SQL Server\AddReplicaWizard。 此記錄檔可以是無法使用的 tootroubleshoot Azure 複本部署。 如果 hello 精靈無法執行任何動作，會回復所有先前的作業，包括刪除 hello 佈建 VM。
> 
> 

## <a name="create-an-availability-group-listener"></a>建立可用性群組接聽程式
建立 hello 可用性群組之後，您應該建立的接聽程式的用戶端 tooconnect toohello 複本。 接聽項直接連入連線 tooeither hello 主要或唯讀次要複本。 如需接聽程式的詳細資訊，請參閱 [在 Azure 中設定 Always On 可用性群組的 ILB 接聽程式](../classic/ps-sql-int-listener.md)。

## <a name="next-steps"></a>後續步驟
在加法 toousing hello**加入 Azure 複本精靈**tooextend 您 Alwayson 可用性群組 tooAzure，您可能也會移動某些 SQL Server 工作負載完全 tooAzure。 tooget 啟動，請參閱[佈建在 Azure 上的 SQL Server 虛擬機器](../sql/virtual-machines-windows-portal-sql-server-provision.md)。

如 toorunning Azure Vm 中的 SQL Server 相關的其他主題，請參閱 < [Azure 虛擬機器上的 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。

