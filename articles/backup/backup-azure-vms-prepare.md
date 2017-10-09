---
title: "aaaPreparing 您註冊 Azure 虛擬機器的環境 tooback |Microsoft 文件"
description: "確認在 Azure 中備份虛擬機器的環境已準備就緒"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonn
editor: 
keywords: "備份；備份；"
ms.assetid: 238ab93b-8acc-4262-81b7-ce930f76a662
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/25/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 3b914c507dd6ad703ea799115ae84ac229e27787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-azure-virtual-machines"></a>準備您的環境 tooback Azure 虛擬機器
> [!div class="op_single_selector"]
> * [Resource Manager 模型](backup-azure-arm-vms-prepare.md)
> * [傳統模型](backup-azure-vms-prepare.md)
>
>

在您可以備份 Azure 虛擬機器 (VM) 之前，有三個條件必須存在。

* 您需要 toocreate 備份保存庫，或識別現有的備份保存庫*在 hello 與您的 VM 相同的區域*。
* 建立的 hello Azure 公用網際網路位址並 hello Azure 儲存體端點之間的網路連線。
* Hello VM 上安裝代理程式 hello VM。

如果您知道這些條件已存在於您的環境，然後繼續 toohello[備份您的 Vm 文章](backup-azure-vms.md)。 否則，請閱讀，本文將引導您完成 hello 步驟 tooprepare 您的環境 tooback Azure vm。

##<a name="supported-operating-system-for-backup"></a>支援的備份作業系統
 * **Linux**：Azure 備份支援 [Azure 所背書的散發套件清單](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ，但核心作業系統 Linux 除外。 _其他提到-您-擁有-Linux 散發套件也可能會運作，只要 hello VM 代理程式位於 hello 虛擬機器和 Python 存在的支援。不過，我們並不為這些備份散發套件背書。_
 * **Windows Server**：不支援比 Windows Server 2008 R2 更舊的版本。


## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>備份和還原 VM 時的限制
> [!NOTE]
> Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。 hello 下列清單提供 hello 限制 hello 傳統模式中部署時。
>
>

* 不支援備份具有 16 個以上資料磁碟的虛擬機器。
* 不支援備份具有保留的 IP 且沒有已定義之端點的虛擬機器。
* 備份資料不包含掛接的網路磁碟機附加 tooVM。
* 不支援在還原期間取代現有的虛擬機器。 第一次刪除 hello 現有的虛擬機器和任何相關聯的磁碟，然後再從備份還原 hello 資料。
* 不支援跨區域備份和還原。
* 在 Azure 的所有公用區域使用 hello Azure 備份服務來備份虛擬機器支援 (請參閱 hello[檢查清單](https://azure.microsoft.com/regions/#services)支援的地區)。 如果您要尋找的 hello 地區不支援目前，它不會出現在 hello 下拉式清單中保存庫建立期間。
* 使用 hello Azure 備份服務來備份虛擬機器僅支援選取的作業系統版本：
* 只有透過 PowerShell 才支援還原屬於多網域控制站 (DC) 組態的 DC VM。 進一步了解 [還原多 DC 網域控制站](backup-azure-restore-vms.md#restoring-domain-controller-vms)。
* 還原虛擬機器具有特殊的網路設定的 hello 只可透過 PowerShell 支援。 您使用在 hello hello 還原工作流程建立的 Vm UI 不會有這些網路組態 hello 還原操作完成後。 詳細資訊，請參閱 toolearn[還原特殊的網路組態的 Vm](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations)。
  * 負載平衡器組態下的虛擬機器 (內部與外部)
  * 具有多個保留的 IP 位址的虛擬機器
  * 具有多個網路介面卡的虛擬機器

## <a name="create-a-backup-vault-for-a-vm"></a>為 VM 建立備份保存庫
備份保存庫是儲存所有的 hello 備份和復原點已建立一段時間的實體。 hello 備份保存庫也包含 hello 將會套用的 toohello 虛擬機器進行備份的備份原則。

> [!IMPORTANT]
> 從開始 2017 年 3 月，您無法再使用 hello 傳統入口網站 toocreate 備份保存庫。 仍然支援現有的備份保存庫，且可能會太[使用 Azure PowerShell toocreate 備份保存庫](./backup-client-automation-classic.md#create-a-backup-vault)。 不過，Microsoft 建議您建立的所有部署的復原服務保存庫，因為未來的增強功能套用 tooRecovery 服務保存庫，僅。


下圖顯示 hello hello 之間的關聯性各種 Azure 備份實體： ![Azure 備份實體和關聯性](./media/backup-azure-vms-prepare/vault-policy-vm.png)



## <a name="network-connectivity"></a>網路連線
在訂單 toomanage hello VM 快照，hello 備用分機號碼需要連線 toohello Azure 公用 IP 位址。 未 hello 正確連線到網際網路，hello 虛擬機器的 HTTP 要求逾時以及 hello 備份作業失敗。 如果您的部署有存取限制 (如透過網路安全性群組 (NSG))，請選擇其中一個選項來為備份流量提供明確的路徑︰

* [白名單 hello Azure 資料中心 IP 範圍](http://www.microsoft.com/en-us/download/details.aspx?id=41653)-請參閱 hello 文件，指示如何 toowhitelist hello IP 位址。
* 部署 HTTP Proxy 伺服器來路由傳送流量。

當決定哪些選項 toouse，hello 取捨是管理能力、 細微的控制與成本之間。

| 選項 | 優點 | 缺點 |
| --- | --- | --- |
| 將 IP 範圍列入允許清單 |沒有額外的成本。<br><br>存取在中開啟的 NSG，使用 hello<i>組 AzureNetworkSecurityRule</i> cmdlet。 |經過一段時間的影響 hello IP 範圍變更成的複雜 toomanage。<br><br>提供存取 toohello 整個 Azure 中，並不只是儲存體。 |
| HTTP Proxy |允許更精確地控制在 hello proxy hello 儲存體 Url。 toosetup hello proxy 中的細微控制 https://\*.blob.core.windows.net/\* URL 模式需要 toobe 白名單。 toowhitelist 只 hello hello VM 所使用的儲存體帳戶 https://\<storageAccount\>.blob.core.windows.net/\* URL 模式需要 toobe 白名單。 <br>單一點的網際網路存取 tooVMs。<br>不遵守 tooAzure IP 位址變更。 |Hello proxy 軟體中執行 VM 的額外成本。 |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>白名單 hello Azure 資料中心 IP 範圍
toowhitelist hello Azure 資料中心 IP 範圍，請參閱 hello [Azure 網站](http://www.microsoft.com/en-us/download/details.aspx?id=41653)如 hello IP 範圍和指示的詳細資訊。

### <a name="using-an-http-proxy-for-vm-backups"></a>使用 HTTP Proxy 進行 VM 備份
當備份 VM，hello hello VM 上的備份延伸模組會傳送 hello 快照集管理命令 tooAzure 使用 HTTPS API 的儲存體。 這些 hello 備用分機號碼流量透過 hello HTTP proxy 路由傳送，因為它是設定為存取 toohello hello 唯一元件公用網際網路。

> [!NOTE]
> 沒有建議應該使用的 hello proxy 軟體。 請確認您挑選具有輸出神奇結果的 proxy，而是與 hello 組態步驟。 請確定第三方廠商軟體不會修改 hello proxy 設定
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

*請確定 hello 範例中的 hello 名稱取代 hello 詳細資料的適當 tooyour 部署。*

## <a name="vm-agent"></a>VM 代理程式
您可以備份 hello Azure 虛擬機器之前，您應該確定該 hello Azure VM 代理程式已正確安裝 hello 虛擬機器上。 由於 hello VM 代理程式是選用的元件在 hello 建立 hello 虛擬機器的時間，確定 hello VM 代理程式會選取前 hello 虛擬機器已佈建該 hello 核取方塊。

### <a name="manual-installation-and-update"></a>手動安裝和更新
hello VM 代理程式已經在 Vm 中建立的 hello Azure 圖庫中。 不過，從內部部署資料中心移轉的虛擬機器沒有 hello 安裝 VM 代理程式。 對於這類的 Vm，必須明確安裝 toobe hello VM 代理程式。 深入了解[現有的 VM 上安裝 hello VM 代理程式](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)。

| **作業** | **Windows** | **Linux** |
| --- | --- | --- |
| Hello VM 代理程式安裝 |<li>下載並安裝 hello[代理程式 MSI 以](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。 您需要系統管理員權限 toocomplete hello 安裝。 <li>[更新 hello VM 屬性](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)tooindicate hello 代理程式的安裝。 |<li> 安裝最新的 hello [Linux 代理程式](https://github.com/Azure/WALinuxAgent)從 GitHub。 您需要系統管理員權限 toocomplete hello 安裝。 <li> [更新 hello VM 屬性](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)tooindicate hello 代理程式的安裝。 |
| 更新 hello VM 代理程式 |更新 hello VM 代理程式的很簡單，重新安裝 hello [VM 代理程式二進位檔](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。 <br><br>請確認在 hello VM 代理程式在更新時，執行任何備份作業。 |依 hello 指示[更新 hello Linux VM 代理程式](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 <br><br>請確認在 hello VM 代理程式在更新時，執行任何備份作業。 |
| 正在驗證 hello VM 代理程式安裝 |<li>瀏覽 toohello *C:\WindowsAzure\Packages* hello Azure VM 中的資料夾。 <li>您應該尋找 hello WaAppAgent.exe 檔案存在。<li> 以滑鼠右鍵按一下 hello 檔案，請移過**屬性**，然後選取 hello**詳細資料**hello 產品版本 索引標籤 欄位應該是 2.6.1198.718 或更高版本。 |N/A |

深入了解 hello [VM 代理程式](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409)和[如何 tooinstall 它](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/)。

### <a name="backup-extension"></a>備份擴充功能
tooback hello 虛擬機器，hello Azure 備份服務會安裝延伸 toohello VM 代理程式。 hello Azure 備份服務順暢地升級和修補程式不需要額外的使用者介入的 hello 備用分機號碼。

如果 hello VM 正在執行，就會安裝 hello 備用分機號碼。 執行中的 VM 也提供 hello 取得應用程式一致復原點的最大的機會。 不過，hello Azure 備份服務將會繼續向上 hello VM-tooback，即使它已關閉，而且找不到 hello 擴充功能安裝 (也稱為離線 VM)。 Hello 復原點將會在此情況下，*絕對一致*如同上面所討論。

## <a name="questions"></a>有疑問嗎？
如果您有任何問題，或如果沒有任何功能，您想要納入，toosee[傳送意見反應](http://aka.ms/azurebackup_feedback)。

## <a name="next-steps"></a>後續步驟
既然您已經備妥您的環境來備份您的 VM，您下一步是 toocreate 備份。 規劃發行項的 hello 提供備份 Vm 的詳細的資訊。

* [備份虛擬機器](backup-azure-vms.md)
* [規劃 VM 備份基礎結構](backup-azure-vms-introduction.md)
* [管理虛擬機器備份](backup-azure-manage-vms.md)
