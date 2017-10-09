您無法啟動或連接 Azure 虛擬機器 (VM) 上執行的 tooan 應用程式時，有各種原因。 原因包括 hello 應用程式未執行或接聽 hello 預期的通訊埠，hello 接聽連接埠被封鎖，或是網路不會正確傳遞流量 toohello 應用程式的規則。 本文說明有系統的方法 toofind 和正確的 hello 問題。

如果您在連接時發生問題 tooyour VM hello 下列其中一種文件第一次使用 RDP 或 SSH，請參閱：

* [疑難排解遠端桌面連線 tooa windows Azure 虛擬機器](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)
* [疑難排解安全殼層 (SSH) 連線 tooa Linux 型 Azure 虛擬機器](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)。

> [!NOTE]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../articles/resource-manager-deployment-model.md)。 本文將說明如何使用這兩個模型，但 Microsoft 建議的最新的部署使用 hello 資源管理員的模型。

如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和 hello 堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。 或者，您也可以提出 Azure 支援事件。 移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)選取**取得支援**。

## <a name="quick-start-troubleshooting-steps"></a>快速入門的疑難排解步驟
如果您有連接 tooan 應用程式的問題，請嘗試下列一般疑難排解步驟的 hello。 在每個步驟中之後, 再試一次連接 tooyour 一次應用程式：

* 重新啟動 hello 虛擬機器
* 重新建立 hello 端點 / 防火牆規則/網路安全性群組 (NSG) 規則
  * [資源管理員模型 - 管理網路安全性群組](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
  * [傳統模型 - 管理雲端服務端點](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
* 從不同的位置 (例如不同的 Azure 虛擬網路) 進行連線
* 重新部署 hello 虛擬機器
  * [重新部署 Windows VM](../articles/virtual-machines/windows/redeploy-to-new-node.md)
  * [重新部署 Linux VM](../articles/virtual-machines/linux/redeploy-to-new-node.md)
* 重新建立 hello 虛擬機器

如需詳細資訊，請參閱 [疑難排解端點連接能力 (RDP/SSH/HTTP 等失敗問題)](https://social.msdn.microsoft.com/Forums/azure/en-US/538a8f18-7c1f-4d6e-b81c-70c00e25c93d/troubleshooting-endpoint-connectivity-rdpsshhttp-etc-failures?forum=WAVirtualMachinesforWindows)。

## <a name="detailed-troubleshooting-overview"></a>詳細疑難排解概觀
有四個主要區域 tootroubleshoot hello 存取 Azure 虛擬機器上執行的應用程式。

![疑難排解無法啟動應用程式](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access1.png)

1. hello hello Azure 虛擬機器上執行應用程式。
   * Hello 應用程式本身已正確執行？
2. hello Azure 虛擬機器。
   * 是 hello VM 本身正確執行，而且回應 toorequests 嗎？
3. Azure 網路端點。
   * Hello 傳統部署模型中的虛擬機器的雲端服務端點。
   * 資源管理員部署模型中虛擬機器的網路安全性群組和輸入 NAT 規則。
   * 可以將流量從使用者 toohello hello 預期的連接埠上的 VM/應用程式的流程嗎？
4. 您的網際網路邊緣裝置。
   * 是否已經有防火牆規則會防止流量正確地流動？

透過站對站 VPN 或 ExpressRoute 連線存取 hello 應用程式的用戶端電腦，可能會造成問題的 hello 主要區域 hello 應用程式和 hello Azure 虛擬機器。

toodetermine hello 來源 hello 問題和更正，請遵循下列步驟。

## <a name="step-1-access-application-from-target-vm"></a>步驟 1︰從目標 VM 存取應用程式
請嘗試 tooaccess hello 應用程式與 hello 適當的用戶端程式從執行所在的 hello VM。 使用 hello 本機主機名稱、 hello 本機 IP 位址或 hello 回送位址 (127.0.0.1)。

![直接從 hello VM 啟動應用程式](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access2.png)

例如，如果 hello 應用程式是 web 伺服器，開啟 hello VM 上的瀏覽器，然後再次嘗試 tooaccess hello VM 上裝載的網頁。

如果您可以存取 hello 應用程式，請移至太[步驟 2](#step2)。

如果您無法存取 hello 應用程式，請確認下列設定的 hello:

* hello 應用程式正在 hello 目標虛擬機器上執行。
* hello 應用程式正在接聽 hello 必須是 TCP 和 UDP 通訊埠。

在 Windows 和 Linux 型虛擬機器上使用 hello **netstat-a** tooshow hello 作用中的接聽連接埠的命令。 檢查您的應用程式應接聽的 hello 預期通訊埠的 hello 輸出。 重新啟動 hello 應用程式或視需要將它設定 toouse hello 預期的連接埠並再試一次本機 tooaccess hello 應用程式。

## <a id="step2"></a>步驟 2： 從另一個 VM hello 中存取應用程式相同的虛擬網路
嘗試從不同的 VM tooaccess hello 應用程式，但在 hello 相同虛擬網路上使用 hello VM 的主機名稱或其 Azure 指派公用、 私用或提供者 IP 位址。 針對使用 hello 傳統部署模型所建立的虛擬機器，請勿 hello 雲端服務的 hello 公用 IP 位址。

![從其他 VM 啟動應用程式](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access3.png)

例如，如果 hello 應用程式是 web 伺服器，再試一次 tooaccess 網頁中的不同 VM 上的瀏覽器從 hello 相同虛擬網路。

如果您可以存取 hello 應用程式，請移至太[步驟 3](#step3)。

如果您無法存取 hello 應用程式，請確認下列設定的 hello:

* hello hello 目標 VM 上的主機防火牆允許 hello 輸入的要求和回應的輸出流量。
* 入侵偵測或監視 hello 目標 VM 上執行的軟體的網路允許 hello 流量。
* 雲端服務端點或網路安全性群組允許 hello 流量：
  * [傳統模型 - 管理雲端服務端點](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
  * [資源管理員模型 - 管理網路安全性群組](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
* VM 和 VM，例如負載平衡器或防火牆，hello 測試之間執行 hello 路徑中在 VM 中的個別元件允許 hello 流量。

Windows 型虛擬機器上，使用 Windows 防火牆具有進階安全性 toodetermine 是否 hello 防火牆規則中排除應用程式的輸入和輸出流量。

## <a id="step3"></a>步驟 3： 從外部 hello 虛擬網路中存取應用程式
請嘗試 tooaccess hello 應用程式從 hello 虛擬網路外的電腦作為 hello 應用程式執行所在的 hello VM。 使用與您的原始用戶端電腦不同的網路。

![從 hello 虛擬網路外的電腦啟動應用程式](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access4.png)

例如，如果 hello 應用程式是 web 伺服器，請嘗試 tooaccess hello 網頁，從瀏覽器不在 hello 虛擬網路的電腦上執行。

如果您無法存取 hello 應用程式，請確認下列設定的 hello:

* 針對 Vm 建立使用 hello 傳統部署模型：
  
  * 請確認 VM 允許 hello 連入流量，特別是 「 hello 通訊協定 （TCP 或 UDP） 」 和 「 hello 公用和私用連接埠號碼的 hello 該 hello 端點組態。
  * 請確認 hello 端點上的存取控制清單 (Acl)，不會阻礙 hello 網際網路的連入流量。
  * 如需詳細資訊，請參閱[如何 tooSet 端點 tooa 虛擬機器](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。
* 若是使用 hello Resource Manager 部署模型所建立的 Vm:
  
  * 請確認的 hello 的 hello VM 允許 hello 連入流量，特別是 「 hello 通訊協定 （TCP 或 UDP） 」 和 「 hello 公用和私用連接埠號碼的輸入的 NAT 規則組態。
  * 請確認網路安全性群組允許 hello 輸入的要求和回應的輸出流量。
  * 如需詳細資訊，請參閱 [什麼是網路安全性群組 (NSG)？](../articles/virtual-network/virtual-networks-nsg.md)

如果 hello 虛擬機器或端點是一組負載平衡的成員：

* 請確認 hello 探查通訊協定 （TCP 或 UDP） 和連接埠號碼正確。
* 如果 hello 探查通訊協定和連接埠是不同於 hello 負載平衡集的通訊協定和連接埠：
  * 確認 hello 應用程式正在接聽 hello 探查通訊協定 （TCP 或 UDP） 和通訊埠編號 (使用**netstat – a** hello 上目標 VM)。
  * 請確認該 VM 允許 hello 輸入的探查要求，而輸出探查回應流量 hello 目標上的 hello 主機防火牆。

如果您可以存取 hello 應用程式，確認您的網際網路邊緣裝置會允許：

* hello 輸出應用程式要求流量從您的用戶端電腦 toohello Azure 虛擬機器。
* hello 輸入應用程式回應 hello Azure 虛擬機器流量。

## <a name="step-4-if-you-cannot-access-hello-application-use-ip-verify-toocheck-hello-settings"></a>步驟 4，如果您無法存取 hello 應用程式，使用 IP 確認 toocheck hello 設定。 

如需詳細資訊，請參閱 [Azure 網路監視概觀](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)。 

## <a name="additional-resources"></a>其他資源
[疑難排解遠端桌面連線 tooa windows Azure 虛擬機器](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)

[疑難排解安全殼層 (SSH) 連線 tooa Linux 型 Azure 虛擬機器](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)

