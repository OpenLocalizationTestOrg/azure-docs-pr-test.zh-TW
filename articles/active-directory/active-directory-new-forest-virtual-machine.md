---
title: "在 Azure 虛擬網路上的 Active Directory 樹系 aaaInstall |Microsoft 文件"
description: "此教學課程說明 Azure 虛擬網路上的虛擬機器 (VM) 的 toocreate 新的 Active Directory 的樹系。"
services: active-directory, virtual-network
keywords: "active directory 虛擬機器, 安裝 active directory 樹系, azure active directory 影片  "
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
tags: 
ms.assetid: eb7170d0-266a-4caa-adce-1855589d65d1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/06/2017
ms.author: joflore
ms.openlocfilehash: 08121130777cc3c206d7b5b38974982884dca1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-new-active-directory-forest-on-an-azure-virtual-network"></a>在 Azure 虛擬網路上安裝新的 Active Directory 樹系
本主題說明如何 toocreate 新 Windows Server Active Directory 環境的虛擬機器 (VM) 上的 Azure 虛擬網路上[Azure 虛擬網路](../virtual-network/virtual-networks-overview.md)。 在此情況下，hello Azure 虛擬網路不是連接的 tooan 在內部部署網路。

您也可能對以下相關主題有興趣：

* 如需示範這些步驟的影片，請參閱[tooinstall 新的 Active Directory 在 Azure 虛擬網路上的樹系](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* 您可以選擇[設定站對站 VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md)然後安裝新樹系或擴充內部部署樹系 tooan Azure 虛擬網路。 如需相關步驟，請參閱 [在 Azure 虛擬網路中安裝複本 Active Directory 網域控制台](active-directory-install-replica-active-directory-domain-controller.md)。
* 如需在 Azure 虛擬網路上安裝 Active Directory 網域服務 (AD DS) 的概念指引，請參閱 [在 Azure 虛擬機器上部署 Windows Server Active Directory 的指導方針](https://msdn.microsoft.com/library/azure/jj156090.aspx)。

## <a name="scenario-diagram"></a>案例圖表
在此案例中，外部使用者會需要加入網域的伺服器執行的 tooaccess 應用程式。 安裝在他們自己在 Azure 虛擬網路中的雲端服務會安裝執行 hello 應用程式伺服器的 hello Vm 和執行網域控制站的 hello Vm。 它們也會包含在可用性設定檔內，以改進容錯能力。

![Azure 虛擬網路中虛擬機器上的 Active Directory 樹系][1] 7

## <a name="how-does-this-differ-from-on-premises"></a>這與內部部署有何不同？
在 Azure 或在內部部署上安裝網域控制台，差異並不會很多。 hello 下表列出 hello 主要差異。

| tooconfigure... | 內部部署 | Azure 虛擬網路 |
| --- | --- | --- |
| **Hello 網域控制站的 IP 位址** |指派靜態 IP 位址上 hello 網路介面卡內容 |執行 hello Set-azurestaticvnetip cmdlet tooassign 靜態 IP 位址 |
| **DNS 用戶端解析程式** |網路介面卡內容的網域成員上 hello 設定慣用和替代 DNS 伺服器位址 |在 hello hello 虛擬網路屬性上設定 DNS 伺服器位址 |
| **Active Directory 資料庫儲存體** |選擇性地從 C:\ 變更 hello 預設儲存位置 |您需要從 C:\ toochange 預設儲存位置 |

## <a name="create-an-azure-virtual-network"></a>建立 Azure 虛擬網路
1. 登入 toohello Azure 傳統入口網站。
2. 建立虛擬網路。 按一下 [網路]  >  [建立虛擬網路]。 以下列資料表 toocomplete hello 精靈 hello hello 值。

   | 在此精靈頁面上… | 指定這些值 |
   | --- | --- |
   |  **虛擬網路詳細資料** |<p>名稱：輸入虛擬網路的名稱</p><p>區域： 選擇 hello 最接近的區域</p> |
   |  **DNS 與 VPN** |<p>將 DNS 伺服器留空</p><p>不要選取任何 VPN 選項</p> |
   |  **虛擬網路位址空間** |<p>子網路名稱：輸入子網路的名稱</p><p>起始 IP：<b>10.0.0.0</b></p><p>CIDR：<b>/24 (256)</b></p> |

## <a name="create-vms-toorun-hello-domain-controller-and-dns-server-roles"></a>建立 Vm toorun hello 網域控制站和 DNS 伺服器角色
請重複下列步驟 toocreate Vm toohost hello DC 角色所需的 hello。 您應該部署至少兩個虛擬網域控制站 tooprovide 容錯和備援。 如果 hello Azure 虛擬網路會包含類似設定的至少兩個網域控制站 （也就是它們是兩個 Gc，執行 DNS 伺服器，和不保留任何 FSMO 角色等等） 則放入 hello Vm 執行的網域控制站的可用性設定組的改善的容錯功能。

toocreate hello Vm 使用 Windows PowerShell，而不是 hello UI，請參閱[使用 Azure PowerShell toocreate 並預先設定 Windows 型虛擬機器](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

1. 在 hello 傳統入口網站，按一下 **新增** > **計算** > **虛擬機器** > **從組件庫**. 使用下列值 toocomplete hello 精靈 hello。 除非另一個值是建議，或需要接受 hello 設定的預設值。

   | 在此精靈頁面上… | 指定這些值 |
   | --- | --- |
   |  **選擇映像** |Windows Server 2012 R2 Datacenter |
   |  **虛擬機器組態** |<p>虛擬機器名稱：輸入單一標籤名稱 (例如 AzureDC1)。</p><p>新的使用者名稱： 輸入 hello 的使用者名稱。 此使用者將會為 hello VM 上 hello 本機 Administrators 群組的成員。 您必須在 toohello VM 這個名稱 toosign hello 第一次。 名為 Administrator 的 hello 內建帳戶將無法運作。</p><p>新密碼/確認：輸入密碼</p> |
   |  **虛擬機器組態** |<p>雲端服務： 選擇 <b>建立新的雲端服務</b>hello 第一個 VM，然後選取的相同雲端服務名稱，當您建立將裝載的多個 Vm hello DC 角色。</p><p>雲端服務 DNS 名稱：指定全域唯一名稱</p><p>區域/同質群組/虛擬網路： 指定 hello 虛擬網路名稱 （例如 WestUSVNet)。</p><p>儲存體帳戶： 選擇 <b>使用自動產生的儲存體帳戶</b>hello 第一個 VM，然後選取該相同儲存體帳戶名稱，當您建立將裝載的多個 Vm hello DC 角色。</p><p>可用性設定組：選擇 [建立可用性設定組]<b></b>。</p><p>可用性集合名稱： hello 可用性設定組，當您建立的名稱 hello 第一個 VM，然後選取 相同名稱建立 Vm 時的型別。</p> |
   |  **虛擬機器組態** |<p>選取<b>安裝 hello VM 代理程式</b>和您需要的其他擴充功能。</p> |
2. 附加磁碟 tooeach 要執行 hello DC 伺服器角色的 VM。 hello 額外的磁碟是需要的 toostore hello AD 資料庫、 記錄檔和 SYSVOL。 指定的大小 （例如 10 GB) 的 hello 磁碟並將保留 hello**主機快取喜好設定**設定得**無**。 Hello 步驟，請參閱[如何 tooAttach Windows 虛擬機器的資料磁碟 tooa](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。
3. 您第一次登入 toohello VM 之後，請開啟**伺服器管理員** > **檔案和存放服務**toocreate 此使用 NTFS 的磁碟上的磁碟區。
4. 對於要執行 hello DC 角色的 Vm 保留靜態 IP 位址。 tooreserve 靜態的 IP 位址，下載 Microsoft Web Platform Installer hello 和[安裝 Azure PowerShell](/powershell/azure/overview)並執行 hello Set-azurestaticvnetip 指令程式。 例如：

    `Get-AzureVM -ServiceName AzureDC1 -Name AzureDC1 | Set-AzureStaticVNetIP -IPAddress 10.0.0.4 | Update-AzureVM`

如需如何設定靜態 IP 位址的詳細資訊，請參閱 [設定 VM 的靜態內部 IP 位址](../virtual-network/virtual-networks-reserved-private-ip.md)。

## <a name="install-windows-server-active-directory"></a>安裝 Windows Server Active Directory
使用太 hello 相同常式[安裝 AD DS](https://technet.microsoft.com/library/jj574166.aspx)您使用內部部署 （也就是您可以使用 hello UI、 回應檔案中或 Windows PowerShell）。 您需要 tooprovide 系統管理員認證 tooinstall 新樹系。 toospecify hello 位置 hello Active Directory 資料庫、 記錄以及 SYSVOL，請從 hello 作業系統磁碟機 toohello 額外資料磁碟附加 toohello VM 變更 hello 預設儲存位置。

Hello DC 安裝完成之後，再次連接 toohello VM，並登入 toohello DC。 請記住 toospecify 網域認證。

## <a name="reset-hello-dns-server-for-hello-azure-virtual-network"></a>重設 hello hello Azure 虛擬網路的 DNS 伺服器
1. 重設 hello 新的 DC/DNS 伺服器上的 hello DNS 轉寄站設定。
   1. 在 [伺服器管理員] 中，按一下 [工具]  >  [DNS]。
   2. 在**DNS 管理員**，hello hello DNS 伺服器名稱上按一下滑鼠右鍵，然後按一下**屬性**。
   3. 在 hello**轉寄站**索引標籤上，按一下 hello hello 轉寄站的 IP 位址，然後按一下**編輯**。  選取 hello IP 位址，然後按一下**刪除**。
   4. 按一下**確定**tooclose hello 編輯器和**確定**再次 tooclose hello DNS 伺服器屬性。
2. 更新 hello hello 虛擬網路的 DNS 伺服器設定。
   1. 按一下**虛擬網路**> 按兩下 hello 您所建立的虛擬網路 >**設定** > **DNS 伺服器**，並輸入 hello 名稱 hello DIP 的其中一個hello Vm 執行 hello DC/DNS 伺服器角色，然後按一下**儲存**。
   2. 選取 hello VM，然後按一下**重新啟動**tootrigger hello VM tooconfigure DNS 解讀器設定 hello hello 新的 DNS 伺服器 IP 位址。

## <a name="create-vms-for-domain-members"></a>建立網域成員的 VM
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

## <a name="see-also"></a>另請參閱
* [新的 Active Directory tooinstall Azure 的虛擬網路上的樹系](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* [在 Azure 虛擬機器上部署 Windows Server Active Directory 的指導方針](https://msdn.microsoft.com/library/azure/jj156090.aspx)
* [設定站台對站台 VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md)
* [在 Azure 虛擬網路中安裝複本 Active Directory 網域控制台](active-directory-install-replica-active-directory-domain-controller.md)
* [Microsoft Azure IT Pro IaaS：(01) 虛擬機器基本概念](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IT Pro IaaS：(05) 建立虛擬網路和跨單位連線](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)
* [虛擬網路概觀](../virtual-network/virtual-networks-overview.md)
* [如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure Cmdlet 參考](/powershell/azure/get-started-azureps)
* [設定 Azure VM 靜態 IP 位址](http://windowsitpro.com/windows-azure/set-azure-vm-static-ip-address)
* [如何 tooassign 靜態 IP tooAzure VM](http://www.bhargavs.com/index.php/2014/03/13/how-to-assign-static-ip-to-azure-vm/)
* [安裝新的 Active Directory 樹系](https://technet.microsoft.com/library/jj574166.aspx)
* [簡介 tooActive Directory 網域服務 (AD DS) Virtualization (Level 100)](https://technet.microsoft.com/library/hh831734.aspx)

<!--Image references-->
[1]: ./media/active-directory-new-forest-virtual-machine/AD_Forest.png
