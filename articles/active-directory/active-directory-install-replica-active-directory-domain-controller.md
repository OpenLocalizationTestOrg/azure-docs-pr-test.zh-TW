---
title: "在 Azure 中複本 Active Directory 網域控制站 aaaInstall |Microsoft 文件"
description: "此教學課程說明 Azure 的虛擬機器的 如何 tooinstall 網域控制站從內部部署 Active Directory 樹系。"
services: virtual-network
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8c9ebf1b-289a-4dd6-9567-a946450005c0
ms.service: virtual-network
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 74876fce2ca2a29f02c2828f9b3a21227248233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-replica-active-directory-domain-controller-in-an-azure-virtual-network"></a>在 Azure 虛擬網路中安裝複本 Active Directory 網域控制台
本主題說明如何為 Azure 虛擬機器 (Vm) 中的 Azure 虛擬網路上的內部部署 Active Directory 網域 tooinstall 其他網域控制站 （也就是複本 Dc）。

> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。

您也可能對以下相關主題有興趣：

* 您可以在 Azure 虛擬網路上選擇性安裝新的 Active Directory 樹系。 如需這些步驟，請參閱[在 Azure 虛擬網路上安裝新的 Active Directory 樹系](active-directory-new-forest-virtual-machine.md)。
* 如需在 Azure 虛擬網路上安裝 Active Directory 網域服務 (AD DS) 的概念指引，請參閱 [在 Azure 虛擬機器上部署 Windows Server Active Directory 的方針](https://msdn.microsoft.com/library/azure/jj156090.aspx)(英文)。

## <a name="scenario-diagram"></a>案例圖表
在此案例中，外部使用者會需要加入網域的伺服器執行的 tooaccess 應用程式。 hello 執行 hello 應用程式伺服器和 hello 複本 Dc 的 Vm 會安裝在 Azure 虛擬網路。 hello 虛擬網路可以在內部部署網路連線的 toohello[站對站 VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md) hello 下列所示的連接圖表中，或者您可以使用[ExpressRoute](../expressroute/expressroute-locations-providers.md)更快的連接。

hello 應用程式伺服器和 hello Dc 部署在個別的雲端服務 toodistribute 計算處理，會在[可用性設定組](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)改善容錯。
hello Dc 會複寫藉由使用 Active Directory 複寫與彼此、 與內部部署網域控制站。 不需要任何同步處理工具。

![Active Directory 網域控制器 Azure vnet 複本][1]

## <a name="create-an-active-directory-site-for-hello-azure-virtual-network"></a>建立 hello Azure 虛擬網路的 Active Directory 站台
它是個不錯的主意 toocreate 代表 hello 網路區域對應 toohello 虛擬網路的 Active Directory 中的站台。 這樣有助於最佳化驗證、複寫及其他 DC 位置的作業。 hello 下列步驟說明如何 toocreate 站台，以及更多背景，請參閱[新增網站](https://technet.microsoft.com/library/cc781496.aspx)。

1. 開啟 [Active Directory 站台及服務]：[伺服器管理員] > [工具] > [Active Directory 站台及服務]。
2. 建立您在建立 Azure 虛擬網路所在的站台 toorepresent hello 區域： 按一下**網站** > **動作** > **新站台**> 類型hello hello 新站台的名稱，例如 Azure 美國西部 > 選取站台連結 >**確定**。
3. 建立子網路，將與 hello 新網站關聯： 按兩下**網站**> 以滑鼠右鍵按一下**子網路** > **新的子網路**> 輸入 hello IP 位址範圍hello 虛擬網路 （例如在 hello 案例概略圖表 10.1.0.0/16) > 選取 hello 新的 Azure 網站 >**確定**。

## <a name="create-an-azure-virtual-network"></a>建立 Azure 虛擬網路
1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，按一下 **新增** > **網路服務** > **虛擬網路** > **自訂建立**和使用 hello 下列值 toocomplete hello 精靈。

   | 在此精靈頁面上… | 指定這些值 |
   | --- | --- |
   |  **虛擬網路詳細資料** |<p>名稱： 輸入 hello 虛擬網路，例如 WestUSVNet 的名稱。</p><p>區域： 選擇 hello 最接近的區域。</p> |
   |  **DNS 和 VPN 連線能力** |<p>DNS 伺服器： 指定 hello 名稱和 IP 位址的一個或多個內部部署 DNS 伺服器。</p><p>連線能力：選取 [設定網站間 VPN]。</p><p>區域網路： 指定新的區域網路。</p><p>如果您使用的是 ExpressRoute 而不是 VPN，請參閱[透過 Exchange 提供者設定 ExpressRoute 連線](../expressroute/expressroute-locations-providers.md)。</p> |
   |  **站對站連線能力** |<p>名稱： 輸入 hello 與內部網路的名稱。</p><p>VPN 裝置 IP 位址： 指定 hello 裝置將連線 toohello 虛擬網路的 hello 公用 IP 位址。 hello VPN 裝置不得位於 NAT 後方。</p><p>位址： 指定 hello 位址範圍，為您的內部部署網路 （例如 192.168.0.0/16 hello 案例概略圖表中)。</p> |
   |  **虛擬網路位址空間** |<p>位址空間： 指定您想 toorun hello （例如 10.1.0.0/16 hello 案例概略圖表中) 的 Azure 虛擬網路中的 Vm hello IP 位址範圍。 這個位址範圍不能與 hello 的 hello 與內部網路的位址範圍重疊。</p><p>子網路： 指定的名稱和 hello 應用程式伺服器的子網路的位址 (例如前端 10.1.1.0/24) 和 hello Dc (後端、 10.1.2.0/24)。</p><p>按一下 [加入閘道子網路] 。</p> |
2. 接下來，您需要設定 hello 虛擬網路閘道 toocreate 安全的站對站 VPN 連線。 請參閱[設定虛擬網路閘道](../vpn-gateway/vpn-gateway-configure-vpn-gateway-mp.md)hello 的指示。
3. 建立 hello 新的虛擬網路與內部部署 VPN 裝置之間的 hello 站對站 VPN 連線。 請參閱[設定虛擬網路閘道](../vpn-gateway/vpn-gateway-configure-vpn-gateway-mp.md)hello 的指示。

## <a name="create-azure-vms-for-hello-dc-roles"></a>建立 Azure Vm 的 hello DC 角色
請重複下列步驟 toocreate Vm toohost hello DC 角色所需的 hello。 您應該部署至少兩個虛擬網域控制站 tooprovide 容錯和備援。 如果 hello Azure 虛擬網路會包含類似設定的至少兩個網域控制站 （也就是它們是兩個 Gc，執行 DNS 伺服器，和不保留任何 FSMO 角色等等） 則放入 hello Vm 執行的網域控制站的可用性設定組的改善的容錯功能。
toocreate hello Vm 使用 Windows PowerShell，而不是 hello UI，請參閱[使用 Azure PowerShell toocreate 並預先設定 Windows 型虛擬機器](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，按一下 **新增** > **計算** > **虛擬機器** > **從組件庫**。 使用下列值 toocomplete hello 精靈 hello。 除非另一個值是建議，或需要接受 hello 設定的預設值。

   | 在此精靈頁面上… | 指定這些值 |
   | --- | --- |
   |  **選擇映像** |Windows Server 2012 R2 Datacenter |
   |  **虛擬機器組態** |<p>虛擬機器名稱：輸入單一標籤名稱 (例如 AzureDC1)。</p><p>新的使用者名稱： 輸入 hello 的使用者名稱。 此使用者將會為 hello VM 上 hello 本機 Administrators 群組的成員。 您必須在 toohello VM 這個名稱 toosign hello 第一次。 名為 Administrator 的 hello 內建帳戶將無法運作。</p><p>新密碼/確認：輸入密碼</p> |
   |  **虛擬機器組態** |<p>雲端服務： 選擇 <b>建立新的雲端服務</b>hello 第一個 VM，然後選取的相同雲端服務名稱，當您建立將裝載的多個 Vm hello DC 角色。</p><p>雲端服務 DNS 名稱：指定全域唯一名稱</p><p>區域/同質群組/虛擬網路： 指定 hello 虛擬網路名稱 （例如 WestUSVNet)。</p><p>儲存體帳戶： 選擇 <b>使用自動產生的儲存體帳戶</b>hello 第一個 VM，然後選取該相同儲存體帳戶名稱，當您建立將裝載的多個 Vm hello DC 角色。</p><p>可用性設定組：選擇 [建立可用性設定組]<b></b>。</p><p>可用性集合名稱： hello 可用性設定組，當您建立的名稱 hello 第一個 VM，然後選取 相同名稱建立 Vm 時的型別。</p> |
   |  **虛擬機器組態** |<p>選取<b>安裝 hello VM 代理程式</b>和您需要的其他擴充功能。</p> |
2. 附加磁碟 tooeach 要執行 hello DC 伺服器角色的 VM。 hello 額外的磁碟是需要的 toostore hello AD 資料庫、 記錄檔和 SYSVOL。 指定的大小 （例如 10 GB) 的 hello 磁碟並將保留 hello**主機快取喜好設定**設定得**無**。 Hello 步驟，請參閱[如何 tooAttach Windows 虛擬機器的資料磁碟 tooa](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。
3. 您第一次登入 toohello VM 之後，請開啟**伺服器管理員** > **檔案和存放服務**toocreate 此使用 NTFS 的磁碟上的磁碟區。
4. 對於要執行 hello DC 角色的 Vm 保留靜態 IP 位址。 tooreserve 靜態的 IP 位址，下載 Microsoft Web Platform Installer hello 和[安裝 Azure PowerShell](/powershell/azure/overview)並執行 hello Set-azurestaticvnetip 指令程式。 例如：

    'Get-AzureVM -ServiceName AzureDC1 -Name AzureDC1 | Set-AzureStaticVNetIP -IPAddress 10.0.0.4 | Update-AzureVM

如需如何設定靜態 IP 位址的詳細資訊，請參閱 [設定 VM 的靜態內部 IP 位址](../virtual-network/virtual-networks-reserved-private-ip.md)。

## <a name="install-ad-ds-on-azure-vms"></a>在 Azure VM 上安裝 AD DS
登入 tooa VM，並確認您擁有連線 hello 站對站 VPN 或 ExpressRoute 連線 tooresources 跨內部部署網路上。 然後在 hello Azure Vm 上安裝 AD DS。 您可以使用您在內部部署網路 （UI、 Windows PowerShell 或回應檔案） 上使用 tooinstall 其他 DC 的相同程序。 當您安裝 AD DS 時，請務必指定新的磁碟區 hello hello 的 hello AD 資料庫記錄檔及 SYSVOL 的位置。 如果您需要複習一下 AD DS 安裝，請參閱[安裝 Active Directory Domain Services (等級 100)](https://technet.microsoft.com/library/hh472162.aspx) 或[在現有網域中安裝複本 Windows Server 2012 網域控制站 (等級 200)](https://technet.microsoft.com/library/jj574134.aspx)。

## <a name="reconfigure-dns-server-for-hello-virtual-network"></a>重新設定 hello 虛擬網路 DNS 伺服器
1. 在 hello [Azure 入口網站](https://portal.azure.com)，在 hello**搜尋資源**方塊中，輸入*虛擬網路*，然後按一下 **虛擬網路 （傳統）**中hello 搜尋結果。 按一下 hello hello 虛擬網路名稱，然後[重新設定 hello DNS 伺服器 IP 位址在虛擬網路](../virtual-network/virtual-network-manage-network.md#dns-servers)toouse hello 靜態 IP 位址指派 toohello 複本網域控制站，而不是在內部部署 DNS hello IP 位址伺服器。
2. tooensure hello 虛擬網路上所有的 hello 複本 DC Vm 設定 toouse DNS 伺服器在 hello 虛擬網路上，按一下**虛擬機器**，針對每個 VM 中，按一下 hello 狀態 資料行，然後按一下**重新啟動**. 等待 hello VM 顯示**執行**狀態再 toosign 到其中。

## <a name="create-vms-for-application-servers"></a>建立應用程式伺服器的 VM
1. 重複下列步驟 toocreate Vm toorun 做為應用程式伺服器 hello。 除非另一個值是建議，或需要接受 hello 設定的預設值。

   | 在此精靈頁面上… | 指定這些值 |
   | --- | --- |
   |  **選擇映像** |Windows Server 2012 R2 Datacenter |
   |  **虛擬機器組態** |<p>虛擬機器名稱：輸入單一標籤名稱 (例如 AppServer1)。</p><p>新的使用者名稱： 輸入 hello 的使用者名稱。 此使用者將會為 hello VM 上 hello 本機 Administrators 群組的成員。 您必須在 toohello VM 這個名稱 toosign hello 第一次。 名為 Administrator 的 hello 內建帳戶將無法運作。</p><p>新密碼/確認：輸入密碼</p> |
   |  **虛擬機器組態** |<p>雲端服務： 選擇 **建立新的雲端服務**hello 第一個 VM，並選取相同雲端服務名稱，當您建立多個 Vm，將裝載 hello 應用程式。</p><p>雲端服務 DNS 名稱：指定全域唯一名稱</p><p>區域/同質群組/虛擬網路： 指定 hello 虛擬網路名稱 （例如 WestUSVNet)。</p><p>儲存體帳戶： 選擇 **使用自動產生的儲存體帳戶**hello 第一個 VM，該相同儲存體帳戶名稱，當您建立多個 Vm，然後選取將裝載 hello 應用程式。</p><p>可用性設定組：選擇 [建立可用性設定組]。</p><p>可用性集合名稱： hello 可用性設定組，當您建立的名稱 hello 第一個 VM，然後選取 相同名稱建立 Vm 時的型別。</p> |
   |  **虛擬機器組態** |<p>選取<b>安裝 hello VM 代理程式</b>和您需要的其他擴充功能。</p> |
2. 每個 VM 已佈建之後，登入，並將其聯結 toohello 網域。 在 [伺服器管理員] 中，按一下 [本機伺服器]  >  [WORKGROUP]  >  [變更…] 然後選取**網域**和型別 hello 您的內部網域名稱。 提供認證的網域使用者，然後再重新啟動 hello VM toocomplete hello 網域加入。

toocreate hello Vm 使用 Windows PowerShell，而不是 hello UI，請參閱[使用 Azure PowerShell toocreate 並預先設定 Windows 型虛擬機器](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

如需有關使用 Windows PowerShell 的詳細資訊，請參閱[開始使用 Azure Cmdlet](/powershell/azure/overview) 和 [Azure Cmdlet 參考](/powershell/azure/get-started-azureps)。

## <a name="additional-resources"></a>其他資源
* [在 Azure 虛擬機器上部署 Windows Server Active Directory 的指導方針](https://msdn.microsoft.com/library/azure/jj156090.aspx)
* [如何 tooupload 現有內部部署 HYPER-V 網域控制站 tooAzure 使用 Azure PowerShell](http://support.microsoft.com/kb/2904015)
* [在 Azure 虛擬網路上安裝新的 Active Directory 樹系](active-directory-new-forest-virtual-machine.md)
* [Azure 虛擬網路](../virtual-network/virtual-networks-overview.md)
* [Microsoft Azure IT Pro IaaS：(01) 虛擬機器基本概念](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IT Pro IaaS：(05) 建立虛擬網路和跨單位連線](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure 管理 Cmdlet](/powershell/module/azurerm.compute/#virtual_machines)

<!--Image references-->
[1]: ./media/active-directory-install-replica-active-directory-domain-controller/ReplicaDCsOnAzureVNet.png
