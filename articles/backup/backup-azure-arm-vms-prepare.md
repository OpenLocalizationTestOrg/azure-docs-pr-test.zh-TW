---
title: "Azure 備份： 準備虛擬機器 tooback |Microsoft 文件"
description: "確認在 Azure 中備份虛擬機器的環境已準備就緒。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "備份；備份；"
ms.assetid: e87e8db2-b4d9-40e1-a481-1aa560c03395
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 5c3a41b5d3bd56e62ca5f207442867913aa99816
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-resource-manager-deployed-virtual-machines"></a>準備您的環境 tooback 資源管理員部署虛擬機器
> [!div class="op_single_selector"]
> * [Resource Manager 模型](backup-azure-arm-vms-prepare.md)
> * [傳統模型](backup-azure-vms-prepare.md)
>
>

本文提供準備您的資源管理員部署虛擬機器 (VM) 的環境 tooback hello 步驟。 hello hello 程序所示的步驟使用 hello Azure 入口網站。  

hello Azure 備份服務有兩種類型的保存庫 （備份保存庫與復原服務保存庫） 來保護您的 Vm。 備份保存庫保護使用 hello 傳統部署模型部署的 Vm。 **不論是傳統部署還是 Resource Manager 部署的 VM**，復原服務保存庫都可給予保護。 您必須使用 復原服務保存庫 tooprotect 資源管理員部署的 VM。

> [!NOTE]
> Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。 請參閱[準備 Azure 虛擬機器註冊您的環境 tooback](backup-azure-vms-prepare.md)如需詳細資訊，使用傳統部署模型的 Vm。
>
>

在保護或備份 Resource Manager 部署的虛擬機器 (VM) 之前，請確認以下必要條件是否存在：

* 建立復原服務保存庫 （或識別現有的復原服務保存庫）*在 hello 與您的 VM 相同的位置*。
* 選取的案例、 定義 hello 備份原則，以及定義項目 tooprotect。
* 檢查 hello 安裝 VM 代理程式的虛擬機器上。
* 檢查網路連線
* 適用於 Linux Vm，如果您想 toocustomize 您備份的環境進行應用程式一致備份請遵循 hello[步驟 tooconfigure 前快照集與後快照集指令碼](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)

如果您知道這些條件已存在於您的環境，然後繼續 toohello[備份您的 Vm 文章](backup-azure-vms.md)。 如果您需要 tooset，或檢查任何這些必要條件，本文將引導您完成 hello 步驟 tooprepare 上述必要條件。

##<a name="supported-operating-system-for-backup"></a>支援的備份作業系統
 * **Linux**：Azure 備份支援 [Azure 所背書的散發套件清單](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ，但核心作業系統 Linux 除外。 _其他提到-您-擁有-Linux 散發套件也可能會運作，只要 hello VM 代理程式位於 hello 虛擬機器和 Python 存在的支援。不過，我們並不為這些備份散發套件背書。_
 * **Windows Server**：不支援比 Windows Server 2008 R2 更舊的版本。

## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>備份和還原 VM 時的限制
準備您的環境之前，請了解 hello 限制。

* 不支援備份具有 16 個以上資料磁碟的虛擬機器。
* 不支援備份資料磁碟大小超過 1023 GB 的虛擬機器。
* 不支援備份具有保留的 IP 且沒有已定義之端點的虛擬機器。
* 不支援備份只使用 BEK 加密的 VM。 不支援備份使用 LUKS 加密的 Linux VM。
* 不建議備份相應放大檔案伺服器設定上的 VM。
* 備份資料不包含掛接的網路磁碟機附加 tooVM。
* 不支援在還原期間取代現有的虛擬機器。 如果您嘗試 toorestore hello VM hello VM 存在時，hello 還原作業將會失敗。
* 不支援跨區域備份和還原。
* 您可以備份所有公用 Azure 的區域中的虛擬機器 (請參閱 hello[檢查清單](https://azure.microsoft.com/regions/#services)支援的地區)。 如果您要尋找的 hello 地區不支援目前，它不會出現在 hello 下拉式清單中保存庫建立期間。
* 只有透過 PowerShell 才支援還原屬於多網域控制站 (DC) 組態的 DC VM。 進一步了解 [還原多 DC 網域控制站](backup-azure-restore-vms.md#restoring-domain-controller-vms)。
* 還原虛擬機器具有特殊的網路設定的 hello 只可透過 PowerShell 支援。 建立使用 hello 還原工作流程中 hello Vm UI 不會有這些網路組態 hello 還原操作完成後。 詳細資訊，請參閱 toolearn[還原特殊的網路組態的 Vm](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations)。
  * 負載平衡器組態下的虛擬機器 (內部與外部)
  * 具有多個保留的 IP 位址的虛擬機器
  * 具有多個網路介面卡的虛擬機器

## <a name="create-a-recovery-services-vault-for-a-vm"></a>建立 VM 的復原服務保存庫。
復原服務保存庫是儲存 hello 備份和復原點已建立一段時間的實體。 hello 復原服務保存庫也包含 hello 與 hello 受保護的虛擬機器相關聯的備份原則。

toocreate 復原服務保存庫：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 在 hello 中樞功能表中，按一下 **瀏覽**hello 清單中的資源，在輸入**復原服務**。 當您開始輸入 hello 清單會篩選器根據您的輸入。 按一下 [復原服務保存庫] 。

    ![按一下 hello 瀏覽按鈕並輸入 復原服務。 當您看見 hello 復原服務保存庫選項，請按一下此 tooopen hello 復原服務保存庫刀鋒視窗。](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

    復原服務保存庫的 hello 清單隨即顯示。
3. 在 hello**復原服務保存庫**功能表上，按一下 **新增**。

    ![建立復原服務保存庫的步驟 2](./media/backup-azure-arm-vms-prepare/rs-vault-menu.png)

    hello 復原服務保存庫刀鋒視窗隨即開啟，提示您 tooprovide**名稱**，**訂用帳戶**，**資源群組**，和**位置**。

    ![建立復原服務保存庫的步驟 5](./media/backup-azure-arm-vms-prepare/rs-vault-attributes.png)
4. 如**名稱**，輸入好記名稱 tooidentify hello 保存庫。 hello 名稱必須 toobe 唯一 hello Azure 訂用帳戶。 輸入包含 2 到 50 個字元的名稱。 該名稱必須以字母開頭，而且只可以包含字母、數字和連字號。
5. 按一下**訂用帳戶**toosee hello 可用訂閱清單。 如果您不確定哪一個訂用帳戶 toouse，使用預設的 hello （或建議） 訂用帳戶。 只有在您的組織帳戶與多個 Azure 訂用帳戶相關聯時，才會有多個選擇。
6. 按一下**資源群組**toosee hello 可用的資源群組的清單，或按一下**新增**toocreate 新的資源群組。 如需資源群組的完整資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)
7. 按一下**位置**hello 保存庫的 tooselect hello 地理區域。 hello 保存庫**必須**處於 hello 與您想 tooprotect hello 虛擬機器相同的區域。

   > [!IMPORTANT]
   > 如果您不確定的 hello 您 VM 所在的位置，退出 hello 保存庫建立對話方塊，並移 hello 入口網站中的虛擬機器 toohello 清單。 如果您有多個區域中的虛擬機器，您將需要 toocreate 復原服務保存庫中每個區域。 建立 hello 第一個位置中的 hello 保存庫，再繼續 toohello 下一個位置。 沒有任何需要 toospecify 儲存體帳戶 toostore hello 備份資料--hello 復原服務保存庫，而且 hello Azure 備份服務會自動處理。
   >
   >

8. 按一下 [建立] 。 它可能需要一段復原服務保存庫建立 toobe hello。 監視 hello 上方右側的區域在 hello 入口網站中的 hello 狀態通知。 一旦建立您的保存庫，它會出現在 hello 清單復原服務保存庫。 如果您沒有看到保存庫，請按一下 [重新整理] 以

    ![備份保存庫的清單](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    既然您已建立您的保存庫，了解如何 tooset hello 儲存體複寫。

## <a name="set-storage-replication"></a>設定儲存體複寫
hello 儲存體複寫選項可讓您 toochoose 地理備援儲存體和本機備援儲存體之間。 根據預設，保存庫具有異地備援儲存體。 如果這是您主要的備份，請保留 hello 選項集 toogeo 備援儲存體。 如果您想要更便宜但不持久的選項，請選擇本地備援儲存體。

tooedit hello 儲存體複寫設定：

1. 在 hello**復原服務保存庫**刀鋒視窗中，選取您的保存庫。
    當您按一下您的保存庫時，hello 設定 刀鋒視窗 (*hello 頂端具有 hello hello 保存庫名稱*) 和 hello 保存庫詳細資料 刀鋒視窗隨即開啟。

    ![從備份保存庫的 hello 清單中選擇您的保存庫](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. 在 hello**設定**刀鋒視窗中，使用 hello 垂直滑桿 tooscroll 向 toohello**管理**> 一節。 按一下**備份基礎結構**tooopen 其刀鋒視窗。 在 hello**一般**區段中，按一下**備份設定**tooopen 其刀鋒視窗。 在 hello**備份設定**刀鋒視窗中，選擇您的保存庫的 hello 存放裝置複寫選項。 根據預設，保存庫具有異地備援儲存體。 如果您變更 hello 儲存體複寫類型，請按一下**儲存**。

    ![備份保存庫的清單](./media/backup-azure-arm-vms-prepare/full-blade.png)

     如果您使用 Azure 做為主要的備份儲存體端點，請繼續使用異地備援儲存體。 如果您要使用 Azure 做為非主要備份儲存體端點，則請選擇本地備援儲存體。 深入了解[異地備援](../storage/common/storage-redundancy.md#geo-redundant-storage)和[本機備援](../storage/common/storage-redundancy.md#locally-redundant-storage)儲存選項的 hello [Azure 儲存體複寫概觀](../storage/common/storage-redundancy.md)。
    選擇您的保存庫的 hello 儲存體選項之後，您就準備好 tooassociate hello VM 與 hello 保存庫。 toobegin hello 關聯，您應該探索及註冊 hello Azure 虛擬機器。

## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>選取備份目標、 設定原則，並定義項目 tooprotect
向保存庫註冊的 VM，之前請先執行 hello 探索程序 tooensure toohello 訂用帳戶已加入任何新虛擬機器所識別。 hello 處理序會查詢 Azure hello hello 訂用帳戶，以及其他資訊中的虛擬機器清單，例如 hello 雲端服務名稱與 hello 區域。 在 hello Azure 入口網站，案例是指 toowhat 要 tooput 到 hello 復原服務保存庫。 原則是 hello 排程的頻率如何及何時建立復原點。 原則也包括 hello hello 的復原點的保留範圍。

1. 如果您已經開啟的復原服務保存庫，繼續 toostep 2。 如果您沒有開啟復原服務保存庫，然後開啟 hello [Azure 入口網站](https://portal.azure.com/)hello 中樞功能表中，按一下 **更多服務**。

   * 在 [hello] 清單中的資源，輸入**復原服務**。
   * 當您開始輸入 hello 清單會篩選器根據您的輸入。 當您看到 [復原服務保存庫] 時，請按一下它。

     ![建立復原服務保存庫的步驟 1](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

     復原服務保存庫 hello 清單隨即出現。 如果訂用帳戶中沒有保存庫，此清單將會空白。

    ![檢視的 hello 復原服務保存庫清單](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

   * 從 hello 清單中的 復原服務保存庫，請選取保存庫 tooopen 其儀表板。

     hello 設定 刀鋒視窗和 hello 保存庫 hello 選擇保存庫中，開啟儀表的板。

     ![開啟 [保存庫] 刀鋒視窗](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)
2. 在 hello 保存庫儀表板功能表上按一下**備份**tooopen hello 備份刀鋒視窗。

    ![開啟 [備份] 刀鋒視窗](./media/backup-azure-arm-vms-prepare/backup-button.png)

    hello 備份及備份目標刀鋒視窗開啟。

    ![開啟 [案例] 刀鋒視窗](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)

3. 在 hello 備份目標刀鋒視窗中，設定**您的工作負載執行**tooAzure 和**怎麼辦想 toobackup** tooVirtual 機器，然後按一下  **確定**。

    這與 hello 保存庫註冊 hello VM 延伸模組。 hello 關閉刀鋒視窗中的備份目標和 hello**備份原則**刀鋒視窗隨即開啟。

    ![開啟 [案例] 刀鋒視窗](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)
4. 在 hello 備份原則 刀鋒視窗，選取您想 tooapply toohello 保存庫的 hello 備份原則。

    ![選取備份原則](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    hello 的 hello 預設原則的詳細資料列在 hello 下拉式選單。 如果您想 toocreate 新的原則，請選取**新建**從 hello 下拉式選單。 如需定義備份原則的指示，請參閱 [定義備份原則](backup-azure-vms-first-look-arm.md#defining-a-backup-policy)。
    按一下**確定**tooassociate hello 備份原則與 hello 保存庫。

    備份原則 刀鋒視窗關閉和 hello hello**選取虛擬機器**刀鋒視窗隨即開啟。
5. 在 hello**選取虛擬機器**刀鋒視窗中，選擇將虛擬機器 tooassociate hello 以 hello 指定原則，然後按一下**確定**。

    ![選取工作負載](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    hello 選取虛擬機器會進行驗證。 如果看不到預期 toosee hello 虛擬機器，請核取，存在於同一 Azure 位置 hello 復原服務保存庫並不是受保護的另一個保存庫中的 hello。 hello 保存庫儀表板上顯示的 復原服務保存庫的 hello 的 hello 位置。

6. 既然您已經定義 hello 保存庫的所有設定，在 hello 備份刀鋒視窗中按一下**啟用備份**。 這會將部署 hello 原則 toohello 保存庫和 hello Vm。 這不會建立 hello hello 虛擬機器的初始的復原點。

    ![啟用備份](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

已成功啟用 hello 備份之後，您的備份原則也會執行排程。 如果您想要 toogenerate hello 虛擬機器上指定備份工作 tooback 現在，請參閱[Triggering hello 備份工作](./backup-azure-arm-vms.md#triggering-the-backup-job)。

如果您有登錄 hello 虛擬機器時遇到問題，請參閱下列資訊和網路連線上安裝 VM 代理程式 hello hello。 您可能不需要下列資訊，如果您要保護在 Azure 中建立的虛擬機器的 hello。 不過如果您移轉至 Azure 的虛擬機器，則是確定您已正確安裝 hello VM 代理程式和虛擬機器，可以與 hello 虛擬網路進行通訊。

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Hello 虛擬機器上安裝 VM 代理程式 hello
hello Azure VM 代理程式必須安裝在 Azure 虛擬機器以 hello 備份副檔名 toowork hello。 如果您的 VM 建立從 hello Azure 組件庫，然後 hello VM 代理程式已經存在於 hello 虛擬機器。 此資訊提供給您的 hello 情況下*不*從 hello Azure 組件庫使用的 VM 建立-例如從內部部署資料中心移轉 VM。 在這種情況下，hello VM 代理程式需要 toobe 順序 tooprotect hello 虛擬機器中安裝。 深入了解 hello [VM 代理程式](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux)。

如果您有備份 hello Azure VM 的問題，確認 hello Azure VM 代理程式已正確安裝 hello 虛擬機器上 （請參閱下表 hello）。 下表中的 hello 提供 hello VM 代理程式用於 Windows 及 Linux Vm 的其他資訊。

| **作業** | **Windows** | **Linux** |
| --- | --- | --- |
| 安裝 VM 代理程式 hello |下載並安裝 hello[代理程式 MSI 以](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。 您需要系統管理員權限 toocomplete hello 安裝。 |<li> 安裝最新的 hello [Linux 代理程式](../virtual-machines/linux/agent-user-guide.md)。 您需要系統管理員權限 toocomplete hello 安裝。 我們建議您從散發機制安裝代理程式。 我們「不」建議您直接從 github 安裝 Linux VM 代理程式。  |
| 更新 hello VM 代理程式 |更新 hello VM 代理程式的很簡單，重新安裝 hello [VM 代理程式二進位檔](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。 <br>請確認在 hello VM 代理程式在更新時，執行任何備份作業。 |依 hello 指示[更新 hello Linux VM 代理程式](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 我們建議您從散發機制更新代理程式。 我們「不」建議您直接從 github 更新 Linux VM 代理程式。<br>確定沒有備份作業正在執行時 hello VM 代理程式正在更新。 |
| 正在驗證 hello VM 代理程式安裝 |<li>瀏覽 toohello *C:\WindowsAzure\Packages* hello Azure VM 中的資料夾。 <li>您應該尋找 hello WaAppAgent.exe 檔案存在。<li> 以滑鼠右鍵按一下 hello 檔案，請移過**屬性**，然後選取 hello**詳細資料**hello 產品版本 索引標籤 欄位應該是 2.6.1198.718 或更高版本。 |N/A |

### <a name="backup-extension"></a>備份擴充功能
一次 hello hello Azure 備份服務 hello 虛擬機器安裝 VM 代理程式會安裝 hello 備用分機號碼 toohello VM 代理程式。 hello Azure 備份服務順暢地升級和修補程式 hello 備用分機號碼。

不論是否正在執行 hello VM hello 備份服務會安裝 hello 備用分機號碼。 執行中的 VM 提供 hello 取得應用程式一致復原點的最大的機會。 不過，hello Azure 備份服務會繼續向上 hello VM tooback 即使它已關閉，而且 hello 擴充功能無法安裝。 這稱為離線 VM。 Hello 復原點將會在此情況下，*絕對一致*。

## <a name="network-connectivity"></a>網路連線
在訂單 toomanage hello VM 快照，hello 備用分機號碼需要連線 toohello Azure 公用 IP 位址。 未 hello 正確連線到網際網路，hello 虛擬機器的 HTTP 要求逾時以及 hello 備份作業失敗。 如果您的部署有存取限制 (如透過網路安全性群組 (NSG))，請選擇其中一個選項來為備份流量提供明確的路徑︰

* [白名單 hello Azure 資料中心 IP 範圍](http://www.microsoft.com/en-us/download/details.aspx?id=41653)-請參閱 hello 文件，指示如何 toowhitelist hello IP 位址。
* 部署 HTTP Proxy 伺服器來路由傳送流量。

當決定哪些選項 toouse，hello 取捨是管理能力、 細微的控制與成本之間。

| 選項 | 優點 | 缺點 |
| --- | --- | --- |
| 將 IP 範圍列入允許清單 |沒有額外的成本。<br><br>存取在中開啟的 NSG，使用 hello<i>組 AzureNetworkSecurityRule</i> cmdlet。 |經過一段時間的影響 hello IP 範圍變更成的複雜 toomanage。<br><br>提供存取 toohello 整個 Azure 中，並不只是儲存體。 |
| HTTP Proxy |允許更精確地控制在 hello proxy hello 儲存體 Url。<br>單一點的網際網路存取 tooVMs。<br>不遵守 tooAzure IP 位址變更。 |Hello proxy 軟體中執行 VM 的額外成本。 |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>白名單 hello Azure 資料中心 IP 範圍
toowhitelist hello Azure 資料中心 IP 範圍，請參閱 hello [Azure 網站](http://www.microsoft.com/en-us/download/details.aspx?id=41653)如 hello IP 範圍和指示的詳細資訊。

### <a name="using-an-http-proxy-for-vm-backups"></a>使用 HTTP Proxy 進行 VM 備份
當備份 VM，hello hello VM 上的備份延伸模組會傳送 hello 快照集管理命令 tooAzure 使用 HTTPS API 的儲存體。 這些 hello 備用分機號碼流量透過 hello HTTP proxy 路由傳送，因為它是設定為存取 toohello hello 唯一元件公用網際網路。

> [!NOTE]
> 沒有建議應該使用的 hello proxy 軟體。 請確定您挑選與 hello 組態步驟的 proxy。
>
>

下面的 hello 範例影像會顯示 hello 三個設定步驟必要 toouse HTTP proxy:

* 針對繫結的所有 HTTP 流量的應用程式 VM 路由 hello Proxy VM 透過公用網際網路。
* Proxy VM 會允許 hello 虛擬網路中的 Vm 所傳來的連入流量。
* 網路安全性群組 (NSG) 名為 NSF 鎖定 hello 需要安全性規則允許連出網際網路流量從 Proxy VM。

![包含 HTTP Proxy 部署圖表的 NSG](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

toouse HTTP proxy toocommunicating toohello 公用網際網路，請遵循下列步驟：

#### <a name="step-1-configure-outgoing-network-connections"></a>步驟 1. 設定連出網路連線
###### <a name="for-windows-machines"></a>Windows 電腦
這會設定本機系統帳戶的 Proxy 伺服器組態。

1. 下載 [PsExec](https://technet.microsoft.com/sysinternals/bb897553)
2. 從提升權限的提示字元執行下列命令。

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     它會開啟 Internet Explorer 視窗。
3. 移 tooTools]-> [網際網路選項]-> [連接]-> [LAN 設定。
4. 確認系統帳戶的 Proxy 設定。 設定 Proxy IP 和連接埠。
5. 關閉 Internet Explorer。

這會設定一個整部機器的 Proxy 設定，並用於任何連出 HTTP/HTTPS 流量。

如果您設定 proxy 伺服器上目前的使用者帳戶 （不是本機系統帳戶），請使用 hello 下列指令碼 tooapply 它們 tooSYSTEMACCOUNT:

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> 如果您在 Proxy 伺服器記錄檔中發現「(407) 需要 Proxy 驗證」，請檢查驗證設定是否正確。
>
>

###### <a name="for-linux-machines"></a>Linux 電腦
加入下列行 toohello hello```/etc/environment```檔案：

```
http_proxy=http://<proxy IP>:<proxy port>
```

新增下列幾行 toohello hello```/etc/waagent.conf```檔案：

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-hello-proxy-server"></a>步驟 2. Hello proxy 伺服器上允許連入連線：
1. Hello proxy 伺服器上，開啟 Windows 防火牆。 hello 最簡單方式 tooaccess hello 防火牆是 toosearch 具有進階安全性的 Windows 防火牆。

    ![開啟防火牆 hello](./media/backup-azure-vms-prepare/firewall-01.png)
2. 在 hello Windows 防火牆對話方塊中，以滑鼠右鍵按一下**輸入規則**按一下**新增規則...**.

    ![建立新的規則](./media/backup-azure-vms-prepare/firewall-02.png)
3. 在 [hello**新增輸入規則精靈**，選擇 hello**自訂**hello 選項**規則類型**按一下**下一步]**。
4. 在 [hello 頁面 tooselect hello**程式**，選擇**所有程式**按一下**下一步]**。
5. 在 hello**通訊協定和連接埠**頁面上，輸入下列資訊的 hello，按一下 **下一步**:

    ![建立新的規則](./media/backup-azure-vms-prepare/firewall-03.png)

   * 針對 [通訊協定類型]，請選擇 [TCP]
   * 如*本機連接埠*選擇*特定連接埠*，底下的 hello 欄位中指定 hello```<Proxy Port>```已經設定。
   * 針對 [遠端連接埠]，請選取 [所有連接埠]

     Hello 精靈 hello 其餘部分，按一下 所有 hello 方式 toohello 結束，並指定此規則的名稱。

#### <a name="step-3-add-an-exception-rule-toohello-nsg"></a>步驟 3. 新增例外狀況規則 toohello NSG:
在使用 Azure PowerShell 命令提示字元中，輸入下列命令的 hello:

hello，下列命令會將例外狀況 toohello NSG。 這個例外狀況允許從 10.0.0.5 上任何連接埠 TCP 流量 tooany 通訊埠 80 (HTTP) 或 443 (HTTPS) 的網際網路位址。 如果您需要在特定的連接埠 hello 公用網際網路，可確定 tooadd 該通訊埠 toohello```-DestinationPortRange```以及。

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```


這些步驟使用範例中的特定名稱和值。*請使用您輸入時，部署或剪下和貼到您的程式碼的詳細資料的 hello 名稱和值。*

現在，您知道您的網路連線，您都已準備好 tooback 啟動您的 VM。 請參閱 [備份 Resource Manager 部署的 VM](backup-azure-arm-vms.md)。

## <a name="questions"></a>有疑問嗎？
如果您有任何問題，或如果沒有任何功能，您想要納入，toosee[傳送意見反應](http://aka.ms/azurebackup_feedback)。

## <a name="next-steps"></a>後續步驟
既然您已經備妥您的環境來備份您的 VM，您下一步是 toocreate 備份。 規劃發行項的 hello 提供備份 Vm 的詳細的資訊。

* [備份虛擬機器](backup-azure-vms.md)
* [規劃 VM 備份基礎結構](backup-azure-vms-introduction.md)
* [管理虛擬機器備份](backup-azure-manage-vms.md)
