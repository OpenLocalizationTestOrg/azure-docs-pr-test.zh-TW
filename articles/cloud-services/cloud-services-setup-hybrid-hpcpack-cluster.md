---
title: "aaaSet 組成的混合式 HPC Pack 叢集在 Azure 中 |Microsoft 文件"
description: "了解 Microsoft HPC Pack toouse 和 Azure tooset 向上很小，混合式高效能運算 (HPC) 叢集"
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: 5ad30d78dcd0c6a95d2a61f25015232edab3563c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a>使用 Microsoft HPC Pack 和隨選 Azure 計算節點設定混合式高效能計算 (HPC) 叢集
使用 Microsoft HPC Pack 2012 R2 和 Azure tooset 很小，混合式高效能運算 (HPC) 叢集上。 本文中所顯示的 hello 叢集包含一個在內部部署 HPC Pack 前端節點和某些計算節點部署視在 Azure 中雲端服務。 然後，您就可以 hello 混合式叢集上執行運算作業。

![Hybrid HPC cluster][Overview] 

此教學課程會示範一個方法，有時也稱為叢集 「 高載 toohello 雲端，」 toouse 可擴充、 隨 Azure 資源 toorun 需要大量計算的應用程式。

本教學課程假設您先前沒有使用計算叢集或 HPC Pack 的經驗。 您部署快速供示範之用的混合式計算叢集的預期只有 toohelp 它。 如需考量和步驟 toodeploy HPC Pack 在混合式叢集更大規模生產環境中，或 toouse HPC Pack 2016，請參閱 hello[詳細指引](http://go.microsoft.com/fwlink/p/?LinkID=200493)。 如需使用 HPC Pack 的其他案例，包括 Azure 虛擬機器中的自動化叢集部署，請參閱[使用 HPC Pack 在 Azure 中建立及管理 Windows HPC 叢集的選項](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

## <a name="prerequisites"></a>必要條件
* **Azure 訂用帳戶** - 如果您沒有 Azure 訂用帳戶，只需要幾分鐘就可以建立 [免費帳戶](https://azure.microsoft.com/free/) 。
* **執行 Windows Server 2012 R2 或 Windows Server 2012 在內部部署電腦**-使用這個電腦作為 hello hello HPC 叢集前端節點。 如果您目前執行的不是 Windows Server，可以下載並安裝 [評估版](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2)。
  
  * hello 電腦必須是聯結的 tooan Active Directory 網域。 基於測試目的，您可以設定 hello 前端節點電腦做為網域控制站。 tooadd hello Active Directory 網域服務伺服器角色和升級為網域控制站的 hello 前端節點電腦，請參閱 Windows Server hello 文件集。
  * toosupport HPC Pack，hello 作業系統必須安裝的其中一種語言： 英文、 日文或中文 （簡體）。
  * 確認已安裝重要及重大更新。
* **HPC Pack 2012 R2** - [下載](http://go.microsoft.com/fwlink/p/?linkid=328024)hello hello 電量與複製 hello 檔案 toohello 前端節點電腦的可用的最新版本的安裝套件。 選擇安裝檔案 hello 中相同的 Windows Server 安裝的語言。

    >[!NOTE]
    > 如果您想 toouse HPC Pack 2016，而不是 HPC Pack 2012 R2，需要進行其他設定。 請參閱 hello[詳細指引](http://go.microsoft.com/fwlink/p/?LinkID=200493)。
    > 
* **網域帳戶**-此帳戶必須具有本機系統管理員權限 hello 前端節點 tooinstall HPC Pack 設定。
* **連接埠 443 上的 TCP 連線**從 hello 前端節點 tooAzure。

## <a name="install-hpc-pack-on-hello-head-node"></a>Hello 前端節點上安裝 HPC Pack
您必須先在執行 Windows Server 的內部部署電腦上安裝 Microsoft HPC Pack。 此電腦會成為 hello hello 叢集前端節點。

1. 使用具有本機系統管理員權限的網域帳戶登入 toohello 前端節點。

2. 從 hello HPC Pack 安裝檔案執行 Setup.exe，以啟動 hello HPC Pack 安裝精靈。

3. 在 hello **HPC Pack 2012 R2 安裝程式**畫面上，按一下**新安裝或加入新功能 tooan 現有安裝**。

    ![HPC Pack 2012 Setup][install_hpc1]

4. 在 hello **Microsoft 軟體使用者協議頁面**，按一下**下一步**。

5. 在 hello**選取安裝類型**頁面上，按一下**透過建立前端節點建立新的 HPC 叢集**，然後按一下**下一步**。

6. hello 精靈會執行數個預先安裝的測試。 按一下**下一步**上 hello**安裝規則**頁面上，如果所有測試都成功。 否則，請檢閱 hello 所提供的資訊，並在您的環境中進行任何必要的變更。 Hello 測試一次，或如果必要開始可再次 hello 安裝精靈，然後執行。
7. 在 hello **HPC 資料庫組態**頁面上，確定**前端節點**選取所有的 HPC 資料庫，然後按一下**下一步**。 

    ![DB Configuration][install_hpc4]

8. 接受預設選取項目 hello hello 精靈的其餘的頁面。 在 hello**安裝所需的元件**頁面上，按一下**安裝**。
   
    ![Install][install_hpc6]

9. Hello 安裝完成之後，取消核取**啟動 HPC 叢集管理員**，然後按一下**完成**。 (您將在稍後的步驟中啟動 HPC 叢集管理員)。
   
    ![完成][install_hpc7]

## <a name="prepare-hello-azure-subscription"></a>準備 hello Azure 訂用帳戶
執行下列步驟在 hello hello [Azure 入口網站](https://portal.azure.com)您 Azure 訂用帳戶。 完成這些步驟之後，您可以部署 Azure 節點從 hello 在內部部署前端節點。 
  
  > [!NOTE]
  > 請一併記下您的 Azure 訂用帳戶識別碼，稍後需要用到。 Hello 中找到識別碼**訂閱**hello 入口網站中。
  > 

### <a name="upload-hello-default-management-certificate"></a>上傳 hello 預設管理憑證
HPC Pack 安裝 hello 前端節點，稱為 hello Microsoft HPC Azure 管理憑證，您可以上傳做為 Azure 管理憑證上的自我簽署的憑證。 此憑證供測試和之間的概念證明部署 toosecure hello 連線 hello 前端節點和 Azure。

1. 從 hello 前端節點的電腦 中，登入 toohello [Azure 入口網站](https://portal.azure.com)。

2. 按一下 [訂用帳戶] > 您的訂用帳戶名稱。

3. 按一下 [管理憑證] > [上傳]。4. 瀏覽的 hello 檔案 C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer hello 前端節點上。 然後，按一下 [上傳]。

   
hello**預設 HPC Azure 管理**憑證出現在 hello 管理憑證的清單。

### <a name="create-an-azure-cloud-service"></a>建立 Azure 雲端服務
> [!NOTE]
> 為了達到最佳效能，建立 hello 雲端服務和 hello （在後續步驟中） 的儲存體帳戶中 hello 相同地理區域。
> 
> 

1. 在 hello 入口網站中，按一下 **雲端服務 （傳統）** > **+ 加**。

2.  輸入 hello 服務的 DNS 名稱，選擇資源群組和位置，然後按**建立**。


### <a name="create-an-azure-storage-account"></a>建立 Azure 儲存體帳戶
1. 在 hello 入口網站中，按一下 **儲存體帳戶 （傳統）** > **+ 加**。

2. 輸入 hello 帳戶的名稱，然後選取 hello**傳統**部署模型。

3. 選擇資源群組和位置，並保留其他設定的預設值。 然後按一下 [ **建立**]。

## <a name="configure-hello-head-node"></a>設定 hello 前端節點
toouse HPC 叢集管理員 toodeploy Azure 節點和 toosubmit 作業先執行一些必要的叢集設定步驟。

1. Hello 前端節點上，啟動 HPC 叢集管理員。 如果 hello**選取前端節點**對話方塊出現時，按一下**本機電腦**。 hello**部署待辦事項清單**隨即出現。

2. 在 [必要部署工作] 底下，按一下 [設定您的網路]。
   
    ![Configure Network][config_hpc2]

3. 在 hello 網路設定精靈 中，選取 **只在企業網路上的所有節點**(拓樸 5)。 此網路設定為 hello 簡單供示範之用。
   
    ![Topology 5][config_hpc3]
   
4. 按一下**下一步**tooaccept hello 剩餘 hello 精靈頁面上的預設值。 然後，在 hello**檢閱**索引標籤上，按一下 **設定**toocomplete hello 網路組態。

5. 在 hello**部署待辦事項清單**，按一下 **提供安裝認證**。

6. 在 hello**安裝認證**對話方塊中，輸入 hello 使用 HPC Pack tooinstall hello 網域帳戶認證。 然後按一下 [確定] 。 
   
    ![Installation Credentials][config_hpc6]
   
7. 在 hello**部署待辦事項清單**，按一下 **設定新節點的命名 hello**。

8. 在 hello**指定節點命名序列**對話方塊方塊中，接受 hello 預設命名數列，然後按一下**確定**。 即使 hello 您在本教學課程中加入 Azure 節點會自動命名，請完成這個步驟。
   
    ![Node Naming][config_hpc8]
   
9. 在 hello**部署待辦事項清單**，按一下 **建立節點範本**。 稍後在 hello 教學課程中，您可以使用 hello 節點範本 tooadd Azure 節點 toohello 叢集。

10. 在 hello 建立節點範本精靈，請執行下列的 hello:
    
    a. 在 hello**選擇節點範本類型**頁面上，按一下**Windows Azure 節點範本**，然後按一下**下一步**。
    
    ![Node Template][config_hpc10]
    
    b. 按一下**下一步**tooaccept hello 預設範本的名稱。
    
    c. 在 hello**提供訂用帳戶資訊**頁面上，輸入您的 Azure 訂用帳戶 ID （適用於您的 Azure 帳戶資訊）。 然後，在 [管理憑證] 中，瀏覽 [預設 Microsoft HPC Azure 管理]。 然後按 [下一步] 。
    
    ![Node Template][config_hpc12]
    
    d. 在 hello**提供服務資訊**頁面、 選取 hello 雲端服務和您在上一個步驟中建立的 hello 儲存體帳戶。 然後按 [下一步] 。
    
    ![Node Template][config_hpc13]
    
    e. 按一下**下一步**tooaccept hello 剩餘 hello 精靈頁面上的預設值。 然後，在 hello**檢閱**索引標籤上，按一下 **建立**toocreate hello 節點範本。
    
    > [!NOTE]
    > 根據預設，hello Azure 節點範本包含設定 toostart （佈建） 和停止 hello 節點以手動方式，使用 HPC 叢集管理員。 您可以選擇性地設定排程 toostart 和停止自動 hello Azure 節點。
    > 
    > 

## <a name="add-azure-nodes-toohello-cluster"></a>新增 Azure 節點 toohello 叢集
現在使用 hello 節點範本 tooadd Azure 節點 toohello 叢集。 加入 hello 節點 toohello 叢集會儲存其組態資訊，讓您可以啟動 （佈建） 這些隨時 hello 雲端服務中。 您的訂用帳戶只取得支付 Azure 節點之後 hello 雲端服務中執行 hello 執行個體。

請遵循這些步驟 tooadd 兩個小節點。

1. 在 HPC 叢集管理員中，按一下 [節點管理] \(在最新版本的 HPC Pack 中稱為 [資源管理]) > [新增節點]。
   
    ![Add Node][add_node1]

2. 在新增節點精靈 的上 hello hello**選擇部署方法**頁面上，按一下**新增 Windows Azure 節點**，然後按一下**下一步**。
   
    ![Add Azure Node][add_node1_1]

3. 在 hello**指定新的節點**頁面上，選取 hello 您先前建立的 Azure 節點範本 (預設會呼叫**預設 AzureNode 範本**)。 接著，指定 **2** 個大小為 [小型] 的節點，然後按 [下一步]。
   
    ![Specify Nodes][add_node2]
   
4. 在 hello**完成 hello 新增節點精靈**頁面上，按一下**完成**。
    
     HPC 叢集管理員中現在會出現兩個 Azure 節點，名為 **AzureCN-0001** 和 **AzureCN-0002**。 兩者都是在 hello**未部署**狀態。
   
    ![Added Nodes][add_node3]

## <a name="start-hello-azure-nodes"></a>啟動 hello Azure 節點
當您想要在 Azure 中，使用 HPC 叢集管理員 toostart （佈建） toouse hello 叢集資源 hello Azure 節點，並且使其連線。

1. HPC 叢集管理員中，按一下**節點管理**(稱為**資源管理**在目前版本的 HPC Pack)，並選取 hello Azure 節點。

2. 按一下 開始，然後按一下確定。
   
   ![Start Nodes][add_node4]
   
    hello 節點轉換 toohello**佈建**狀態。 檢視 hello 佈建記錄 tootrack hello 佈建進行中。
   
    ![Provision Nodes][add_node6]

3. 請稍候幾分鐘 hello Azure 節點完成佈建到且處於 hello**離線**狀態。 處於此狀態，hello 角色執行個體正在執行，但尚無法接受叢集作業。

4. 執行 hello 角色執行個體的 tooconfirm，hello Azure 入口網站中，按一下**雲端服務 （傳統）** > *your_cloud_service_name*。
   
   您應該會看到兩個**HpcWorkerRole** hello 服務中執行執行個體 （節點）。 HPC Pack 也會自動部署兩個**HpcProxy**執行個體 （中型大小） toohandle hello 前端節點與 Azure 之間的通訊。

   ![Running Instances][view_instances1]

5. toobring hello Azure 節點線上 toorun 叢集作業，選取 hello 節點、 按一下滑鼠右鍵，然後按一下**上線**。
   
    ![Offline Nodes][add_node7]
   
    HPC 叢集管理員表示 hello 節點在 hello**線上**狀態。

## <a name="run-a-command-across-hello-cluster"></a>Hello 叢集中執行的命令
toocheck hello 安裝中，使用 hello HPC Pack **clusrun**命令 toorun 命令或一個或多個叢集節點上的應用程式。 簡單舉例如下，使用**clusrun** tooget hello IP 組態 hello Azure 節點。

1. Hello 前端節點上，系統管理員身分開啟命令提示字元。

2. 輸入下列命令的 hello:
   
    `clusrun /nodes:azurecn* ipconfig`

3. 出現提示時，輸入您的叢集系統管理員密碼。 您應該會看到命令的輸出類似 toohello 下列。
   
    ![clusrun][clusrun1]

## <a name="run-a-test-job"></a>執行測試工作
現在您可以送出 hello 混合式叢集執行的測試工作。 這個範例是簡單的參數式掃掠作業 (一種本質平行計算)。 這個範例會執行子工作使用 hello 新增整數 tooitself**設定/a**命令。 Hello 叢集中的所有 hello 節點 1 too100 從都參與 toofinishing hello 子任務的整數。

1. 在 HPC 叢集管理員中，按一下 [作業管理] > [New Parametric Sweep Job] \(新增參數式掃掠作業)。
   
    ![New Job][test_job1]

2. 在 hello**新參數掃掠工作**對話方塊中，於**命令列**，型別`set /a *+*`（覆寫 hello 預設命令列顯示）。 保留的 hello 剩餘的設定，預設值，然後按**送出**toosubmit hello 作業。
   
    ![Parametric Sweep][param_sweep1]

3. Hello 作業完成時，連按兩下 hello**我掃掠工作**作業。

4. 按一下**檢視工作**，然後按一下任務的子工作 tooview hello 計算輸出。
   
    ![Task Results][view_job361]

5. 按一下的 toosee 哪一個節點的子工作中，執行 hello 計算**配置節點**。 (您的叢集可能會顯示不同的節點名稱。)
   
    ![Task Results][view_job362]

## <a name="stop-hello-azure-nodes"></a>停止 hello Azure 節點
您嘗試 hello 叢集之後，停止 hello Azure 節點 tooavoid 不必要的費用 tooyour 帳戶。 這個步驟會停止 hello 雲端服務，並移除 hello Azure 角色執行個體。

1. 在 HPC 叢集管理員中，於 [節點管理] \(在舊版的 HPC Pack 中稱為 [資源管理]) 中，選取這兩個 Azure 節點。 然後，按一下 [停止]。
   
    ![Stop Nodes][stop_node1]

2. 在 hello**停止 Windows Azure 節點**對話方塊中，按一下 **停止**。 
   
3. hello 節點轉換 toohello**停止**狀態。 請稍候幾分鐘 HPC 叢集管理員會顯示 hello 節點都是**未部署**。
   
    ![Not Deployed Nodes][stop_node4]

4. hello 角色執行個體在 Azure 中，不會再執行中的 tooconfirm hello Azure 入口網站中，按一下**雲端服務 （傳統）** > *your_cloud_service_name*。 Hello 的實際執行環境中部署沒有任何執行個體。 
   
    如此即完成 hello 教學課程。

## <a name="next-steps"></a>後續步驟
* 瀏覽 hello 文件[HPC Pack](https://technet.microsoft.com/library/cc514029)。
* tooset 組成的混合式部署 HPC Pack 叢集在更大的小數位數，請參閱[tooAzure 背景工作角色執行個體，使用 Microsoft HPC Pack 高載](http://go.microsoft.com/fwlink/p/?LinkID=200493)。
* 針對其他方式 toocreate 在 Azure 中的 HPC Pack 叢集，包括使用 Azure 資源管理員範本，請參閱[HPC 叢集的選項以在 Azure 中的 Microsoft HPC Pack](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
