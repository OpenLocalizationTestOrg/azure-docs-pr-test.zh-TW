---
title: "Azure vm 的 aaaDetailed SSH 疑難排解 |Microsoft 文件"
description: "更詳細的 SSH 連接 tooan Azure 虛擬機器的問題的疑難排解步驟"
keywords: "ssh 連線被拒, ssh 錯誤, azure ssh, SSH 連線失敗"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: b8e8be5f-e8a6-489d-9922-9df8de32e839
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: support-article
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 3f711e53a8251f8c06dbb589a258222566a4ae1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-ssh-troubleshooting-steps-for-issues-connecting-tooa-linux-vm-in-azure"></a>詳細的 SSH 連接 tooa Linux VM 在 Azure 中的問題的疑難排解步驟
有許多原因會造成該 hello SSH 用戶端可能無法在 hello VM 可以 tooreach hello SSH 服務。 如果您有更遵循透過 hello[疑難排解步驟的一般 SSH](troubleshoot-ssh-connection.md)，您需要 toofurther hello 連線問題進行疑難排解。 這篇文章會引導您完成詳細的疑難排解步驟 toodetermine 其中 hello SSH 連線失敗，以及如何 tooresolve 它。

## <a name="take-preliminary-steps"></a>採取預備步驟
hello 下列圖表顯示 hello 牽涉到的元件。

![顯示 SSH 服務元件的圖表](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot1.png)

hello 下列步驟協助您找出 hello 失敗的 hello 來源，並找出因應措施或解決方案。

1. 檢查 hello hello 入口網站中的 hello VM 狀態。
   在 hello [Azure 入口網站](https://portal.azure.com)，選取**虛擬機器** > *VM 名稱*。

   hello hello VM 的狀態 窗格應該會顯示**執行**。 捲動 tooshow 計算、 儲存體和網路資源的最近活動。

2. 選取**設定**tooexamine 端點、 IP 位址、 網路安全性群組和其他設定。

   hello VM 應該擁有端點，可定義您可以檢視中的 SSH 流量**端點**或**[網路安全性群組](../../virtual-network/virtual-networks-nsg.md)**。 使用 Resource Manager 來建立之 VM 中的端點會儲存在網路安全性群組中。 此外，請確認 hello 規則已套用的 toohello 網路安全性群組，和它們所參考 hello 子網路中。

tooverify 網路連線，請檢查 hello 設定端點，並請參閱可連線到另一個通訊協定，例如 HTTP 或其他服務的 hello VM。

完成這些步驟之後, 再試一次 hello SSH 連線一次。

## <a name="find-hello-source-of-hello-issue"></a>找出 hello hello 問題來源
hello SSH 用戶端電腦上的可能會因為 tooissues 或 hello 下列區域中的錯誤設定 hello Azure VM 上 tooreach hello SSH 服務失敗：

* [SSH 用戶端電腦](#source-1-ssh-client-computer)
* [組織邊緣裝置](#source-2-organization-edge-device)
* [雲端服務端點和存取控制清單 (ACL)](#source-3-cloud-service-endpoint-and-acl)
* [網路安全性群組](#source-4-network-security-groups)
* [以 Linux 為基礎的 Azure VM](#source-5-linux-based-azure-virtual-machine)

## <a name="source-1-ssh-client-computer"></a>來源 1：SSH 用戶端電腦
tooeliminate 為 hello 來源 hello 失敗的電腦驗證，它可以進行 SSH 連線 tooanother 內部，以 Linux 為基礎的電腦。

![強調 SSH 用戶端電腦元件的圖表](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot2.png)

如果 hello 連線失敗，請檢查您的電腦上下列問題的 hello:

* 正封鎖輸入或輸出 SSH 流量的本機防火牆設定 (TCP 22)
* 正阻止 SSH 連線的本機安裝用戶端 Proxy 軟體
* 正阻止 SSH 連線的本機安裝網路監視軟體
* 其他類型的安全性軟體，這會監視流量或允許/不允許特定類型的流量。

如果其中一種情形適用，暫時停用 hello 軟體，然後再次嘗試 SSH 連線 tooan 在內部部署電腦 toofind 出 hello hello 連接您的電腦已封鎖的原因。 然後使用您的網路系統管理員 toocorrect hello 軟體設定 tooallow SSH 連線。

如果您使用憑證驗證，確認您擁有這些權限 toohello.ssh 資料夾主目錄中：

* Chmod 700 ~/.ssh
* Chmod 644 ~/.ssh/\*.pub
* Chmod 600 ~/.ssh/id_rsa (或您儲存私密金鑰的任何其他檔案)
* Chmod 644 ~/.ssh/known_hosts （包含您已連接 toovia SSH 主機）

## <a name="source-2-organization-edge-device"></a>來源 2：組織邊緣裝置
tooeliminate hello 失敗的來源 hello，為您的組織邊緣裝置會確認是否有直接連線 toohello 網際網路的電腦可以建立 SSH 連線 tooyour Azure VM。 如果您要存取 hello VM 透過站對站 VPN、 Azure ExpressRoute 連線，請略過太[來源 4： 網路安全性群組](#nsg)。

![強調組織邊緣裝置的圖表](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot3.png)

如果您沒有直接連接的 toohello 網際網路的電腦，在它自己的資源群組或雲端服務中建立新的 Azure VM，並使用它。 如需詳細資訊，請參閱 [在 Azure 中建立執行 Linux 的虛擬機器](quick-create-cli.md)。 當您完成與您的測試，請刪除 hello 資源的群組或 VM 和雲端服務。

如果已直接連接 toohello 網際網路的電腦，您可以建立 SSH 連線，請檢查您組織的邊緣裝置進行：

* 內部防火牆封鎖 SSH hello 網際網路流量
* Proxy 伺服器是否阻止 SSH 進行連線
* 在邊緣網路裝置上執行的入侵偵測或網路監視軟體是否阻止 SSH 進行連線

使用您的組織邊緣裝置 tooallow SSH 的流量以 hello 網際網路的網路系統管理員 toocorrect hello 設定。

## <a name="source-3-cloud-service-endpoint-and-acl"></a>來源 3：雲端服務端點和 ACL
> [!NOTE]
> 此來源適用於使用 hello 傳統部署模型所建立的 tooVMs。 對於使用資源管理員所建立的 Vm，請跳過[來源 4： 網路安全性群組](#nsg)。

tooeliminate hello 雲端服務端點和為 hello hello 失敗來源的 ACL，請確認在另一個 Azure VM hello 相同虛擬網路可讓 SSH 連線 tooyour VM。

![強調雲端服務端點和 ACL 的圖表](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot4.png)

如果您沒有在 hello 另一個 VM 相同的虛擬網路，您可以輕鬆地建立一個。 如需詳細資訊，請參閱[使用 hello CLI 在 Azure 上建立 Linux VM](quick-create-cli.md)。 刪除 hello 額外的 VM，當您在與您的測試。

如果您可以使用中的 VM 建立 SSH 連線 hello 相同虛擬網路，請檢查下列區域的 hello:

* **hello hello 目標 VM 上的 SSH 流量的端點組態。** hello 私人 TCP 連接埠的 hello 端點應該符合 hello 的 hello SSH hello VM 上的服務所接聽的 TCP 連接埠。 （hello 預設連接埠為 22）。 確認選取的 hello Azure 入口網站中的 hello SSH TCP 通訊埠編號**虛擬機器** > *VM 名稱* > **設定** > **端點**。
* **hello hello 目標虛擬機器上的 hello SSH 流量端點 ACL。** ACL 可讓您 toospecify 允許或拒絕連入流量從 hello 網際網路，根據其來源 IP 位址。 設定不正確的 Acl 可以防止傳入 SSH 流量 toohello 端點。 請檢查您允許您的 proxy 或其他的邊緣伺服器 hello 公用 IP 位址的連入流量的 Acl tooensure。 如需詳細資訊，請參閱 [關於網路存取控制清單 (ACL)](../../virtual-network/virtual-networks-acl.md)。

tooeliminate hello 端點做為來源的 hello 問題，請移除 hello 目前端點、 建立另一個端點，並指定 hello SSH 名稱 （TCP 連接埠 22 hello 公用和私用連接埠號碼）。 如需詳細資訊，請參閱 [在 Azure 中設定虛擬機器的端點](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

<a id="nsg"></a>

## <a name="source-4-network-security-groups"></a>來源 4：網路安全性群組
網路安全性群組可讓您 toohave 允許輸入和輸出流量的更細微的控制。 您可以在 Azure 虛擬網路中建立跨越子網路和雲端服務的規則。 請檢查網路安全性群組規則 tooensure hello 允許網際網路從該 SSH 流量 tooand。
如需詳細資訊，請參閱 [關於網路安全性群組](../../virtual-network/virtual-networks-nsg.md)。

您也可以使用 IP 確認 toovalidate hello NSG 組態。 如需詳細資訊，請參閱 [Azure 網路監視概觀](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)。 

## <a name="source-5-linux-based-azure-virtual-machine"></a>來源 5：以 Linux 為基礎的 Azure 虛擬機器
hello 最後一個可能發生的問題來源是 hello Azure 虛擬機器本身。

![強調以 Linux 為基礎的 Azure 虛擬機器的圖表](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot5.png)

如果還沒有這麼做，請依照 hello 指示[tooreset 密碼或 SSH Linux 型虛擬機器](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。

再次嘗試從您的電腦連線。 如果仍然失敗，則會 hello 以下是一些 hello 可能的問題：

* hello SSH 服務未執行 hello 目標虛擬機器上。
* hello SSH 服務不會接聽 TCP 通訊埠 22。 tootest，在本機電腦上安裝 telnet 用戶端，並執行 「 telnet *cloudServiceName*。.cloudapp.net 22"。 此步驟決定 hello 虛擬機器時可允許傳入和傳出通訊 toohello SSH 的端點。
* hello hello 目標虛擬機器上的本機防火牆有使輸入或輸出 SSH 流量的規則。
* 入侵偵測或網路監視 hello Azure 虛擬機器執行的軟體防止 SSH 連接。

## <a name="additional-resources"></a>其他資源
如需疑難排解應用程式存取的詳細資訊，請參閱[疑難排解存取 tooan 應用程式在 Azure 虛擬機器上執行](troubleshoot-app-connection.md)
