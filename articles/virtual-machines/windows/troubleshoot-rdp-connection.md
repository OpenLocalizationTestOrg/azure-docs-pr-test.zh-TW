---
title: "與 RDP tooa 在 Azure 中的 Windows VM 連接 aaaCannot |Microsoft 文件"
description: "當您無法連接 tooyour Windows 虛擬機器使用遠端桌面在 Azure 中疑難排解問題"
keywords: "遠端桌面的錯誤，遠端桌面連線錯誤，無法連接 tooVM，遠端桌面的疑難排解"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 0d740f8e-98b8-4e55-bb02-520f604f5b18
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: bbb36136e7a4b187fe8deea621d2b8d46d8aa102
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-remote-desktop-connections-tooan-azure-virtual-machine"></a>疑難排解遠端桌面連線 tooan Azure 虛擬機器
您的 VM 時，可以基於各種原因，讓您無法 tooaccess 失敗 hello 遠端桌面通訊協定 (RDP) 連線 tooyour windows Azure 虛擬機器 (VM)。 hello 問題可能是以 hello hello VM、 hello 網路連線或 hello 主機電腦上的遠端桌面用戶端上的遠端桌面服務。 這篇文章會引導您完成 hello 最常見的方法 tooresolve RDP 連線問題。 

如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。 或者，您可以提出 Azure 支援事件。 移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)選取**取得支援**。

<a id="quickfixrdp"></a>

## <a name="quick-troubleshooting-steps"></a>快速疑難排解步驟
每個疑難排解的步驟之後，嘗試重新連接 toohello VM:

1. 重設遠端桌面組態。
2. 檢查網路安全性群組規則 / 雲端服務端點。
3. 檢閱 VM 主控台記錄檔。
4. 重設 hello NIC hello VM。
5. 請檢查 hello VM 資源健全狀況。
6. 重設您的 VM 密碼。
7. 重新啟動您的 VM。
8. 重新部署您的 VM。

如果您需要更詳細的步驟與說明，請繼續閱讀。 請確認區域網路設備 (例如路由器和防火牆) 沒有封鎖輸出 TCP 連接埠 3389，如[詳細的 RDP 疑難排解案例](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中所述。

> [!TIP]
> 如果 hello**連接**按鈕 hello 入口網站中的 「 您的 VM 會變成灰色外，您不是透過連接的 tooAzure [Express Route](../../expressroute/expressroute-introduction.md)或[站對站 VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)連線，您需要toocreate 及指派您 VM 的公用 IP 位址之前，您可以使用 RDP。 您可以深入了解 [Azure 中的公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)。


## <a name="ways-tootroubleshoot-rdp-issues"></a>方式 tootroubleshoot RDP 問題
您可以疑難排解使用 hello Resource Manager 部署模型，使用其中一種 hello 下列方法建立的 Vm:

* [Azure 入口網站](#using-the-azure-portal)-太好了，如果您需要 tooquickly 重設 hello RDP 設定] 或 [使用者認證並不 hello Azure tools 安裝。
* [Azure PowerShell](#using-azure-powershell) -如果您想要使用 PowerShell 提示時，快速重設 hello RDP 設定] 或 [使用者認證使用 hello Azure PowerShell cmdlet。

您也可以找到疑難排解使用 hello 所建立的 Vm 上的步驟[傳統部署模型](#troubleshoot-vms-created-using-the-classic-deployment-model)。

<a id="fix-common-remote-desktop-errors"></a>

## <a name="troubleshoot-using-hello-azure-portal"></a>使用 hello Azure 入口網站的疑難排解
每個疑難排解的步驟之後，請再次嘗試連線 tooyour VM。 如果仍然無法連線，請嘗試 hello 下一個步驟。

1. **重設您的 RDP 連線**。 遠端連接已停用或 Windows 防火牆規則，例如封鎖 RDP 時，此疑難排解的步驟會重設 hello RDP 組態。
   
    選取您的 VM 中的 hello Azure 入口網站。 捲動 hello 設定窗格 toohello**支援 + 疑難排解**hello 清單的底部附近一節。 按一下 hello**重設密碼** 按鈕。 設定 hello**模式**太**只能重設組態**然後按一下hello**更新**按鈕：
   
    ![重設 hello Azure 入口網站中的 hello RDP 設定](./media/troubleshoot-rdp-connection/reset-rdp.png)
2. **確認網路安全性群組規則**。 使用[IP 流量確認](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md)tooconfirm 如果網路安全性群組中的規則會封鎖從虛擬機器的流量 tooor。 您也可以檢閱有效安全性群組規則 tooensure 輸入 「 允許 」 NSG 規則存在，而且已設定優先權的 RDP 連接埠 （預設值為 3389）。 如需詳細資訊，請參閱[使用有效的安全性規則 tootroubleshoot VM 流量流程](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow)。

3. **檢閱 VM 開機診斷**。 此步驟中疑難排解檢閱 hello VM 主控台記錄檔 toodetermine 如果 hello VM 所報告的問題。 並非所有 VM 都已啟用開機診斷，所以此疑難排解步驟可能是選擇性的。
   
    特定的疑難排解步驟已超出本文的 hello 範圍，但可能會影響 RDP 連線更多問題。 如需有關如何檢閱 hello 主控台記錄檔和 VM 螢幕擷取畫面的詳細資訊，請參閱[Vm 的開機診斷](boot-diagnostics.md)。

4. **重設 hello NIC VM hello**。 如需詳細資訊，請參閱[如何 tooreset Azure Windows vm NIC](reset-network-interface.md)。
5. **請檢查 VM 資源健全狀況 hello**。 此疑難排解步驟會確認沒有任何已知的問題與 hello 可能會影響連線 toohello VM 的 Azure 平台。
   
    選取您的 VM 中的 hello Azure 入口網站。 捲動 hello 設定窗格 toohello**支援 + 疑難排解**hello 清單的底部附近一節。 按一下 hello**資源健全狀況** 按鈕。 狀況良好的 VM 會報告為 [可用]：
   
    ![檢查 VM hello Azure 入口網站中的資源健全狀況](./media/troubleshoot-rdp-connection/check-resource-health.png)
6. **重設使用者認證**。 當您不確定或忘記 hello 認證時，此疑難排解步驟會重設 hello 上本機系統管理員帳戶的密碼。
   
    選取您的 VM 中的 hello Azure 入口網站。 捲動 hello 設定窗格 toohello**支援 + 疑難排解**hello 清單的底部附近一節。 按一下 hello**重設密碼** 按鈕。 請確定 hello**模式**設定得**重設密碼**，然後輸入您的使用者名稱和新的密碼。 最後，按一下 hello**更新**按鈕：
   
    ![重設 hello hello Azure 入口網站中的使用者認證](./media/troubleshoot-rdp-connection/reset-password.png)
7. **重新啟動您的 VM**。 此疑難排解的步驟可以更正任何基礎的問題已擁有 hello VM 本身。
   
    Hello Azure 入口網站中選取您的 VM，然後按一下 hello**概觀** 索引標籤。按一下 hello**重新啟動**按鈕：
   
    ![在 hello Azure 入口網站中重新啟動 VM hello](./media/troubleshoot-rdp-connection/restart-vm.png)
8. **重新部署您的 VM**。 此步驟中疑難排解重新部署 VM tooanother 主應用程式，Azure toocorrect 內任何基礎的平台或網路問題。
   
    選取您的 VM 中的 hello Azure 入口網站。 捲動 hello 設定窗格 toohello**支援 + 疑難排解**hello 清單的底部附近一節。 按一下 hello**重新部署**按鈕，然後再按一下**重新部署**:
   
    ![重新部署 hello Azure 入口網站中的 hello VM](./media/troubleshoot-rdp-connection/redeploy-vm.png)
   
    這項作業完成之後，暫時磁碟資料是遺失和動態 hello VM 會更新相關聯的 IP 位址。

如果您仍然遇到 RDP 問題，可以[開啟支援要求](https://azure.microsoft.com/support/options/)或閱讀[更詳細的 RDP 疑難排解概念和步驟](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

## <a name="troubleshoot-using-azure-powershell"></a>使用 Azure PowerShell 進行疑難排解
如果您還沒有這麼做，[安裝及設定 hello 最新 Azure PowerShell](/powershell/azure/overview)。

hello 下列範例會使用變數例如`myResourceGroup`， `myVM`，和`myVMAccessExtension`。 以您自己的值取代這些變數名稱和位置。

> [!NOTE]
> 您使用重設 hello 使用者認證及 hello RDP 組態 hello[組 AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet。 在下列範例中，hello`myVMAccessExtension`是您指定 hello 程序的名稱。 如果您先前已使用 hello VMAccessAgent，您可以使用來取得 hello hello 現有擴充功能名稱`Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"`hello VM toocheck hello 屬性。 hello 輸出 hello 'Extensions' 區段下的外觀 tooview hello 名稱。

每個疑難排解的步驟之後，請再次嘗試連線 tooyour VM。 如果仍然無法連線，請嘗試 hello 下一個步驟。

1. **重設您的 RDP 連線**。 遠端連接已停用或 Windows 防火牆規則，例如封鎖 RDP 時，此疑難排解的步驟會重設 hello RDP 組態。
   
    hello 下列範例會重設名為的 VM 上的 hello RDP 連線`myVM`在 hello`WestUS`位置並在 hello 資源群組中名為`myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location Westus -Name "myVMAccessExtension"
    ```
2. **確認網路安全性群組規則**。 此疑難排解步驟會確認您的網路安全性群組 toopermit RDP 流量的規則。 RDP 的 hello 預設連接埠是 TCP 連接埠 3389。 規則 toopermit RDP 流量可能不會自動建立時建立您的 VM。
   
    首先，指派所有 hello 組態資料的網路安全性群組 toohello`$rules`變數。 hello 下列範例會取得 hello 名為的網路安全性群組的相關資訊`myNetworkSecurityGroup`hello 資源群組中名為`myResourceGroup`:
   
    ```powershell
    $rules = Get-AzureRmNetworkSecurityGroup -ResourceGroupName "myResourceGroup" `
        -Name "myNetworkSecurityGroup"
    ```
   
    現在，檢視已針對此網路安全性群組的 hello 規則。 請確認的規則存在 tooallow TCP 連接埠 3389 的傳入連接，如下所示：
   
    ```powershell
    $rules.SecurityRules
    ```
   
    hello 下列範例示範有效的安全性規則，允許 RDP 流量。 您可以看到 `Protocol`、`DestinationPortRange`、`Access` 和 `Direction` 已正確設定︰
   
    ```powershell
    Name                     : default-allow-rdp
    Id                       : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/default-allow-rdp
    Etag                     : 
    ProvisioningState        : Succeeded
    Description              : 
    Protocol                 : TCP
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : *
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 1000
    Direction                : Inbound
    ```
   
    如果您沒有可允許 RDP 流量的規則，請[建立網路安全性群組規則](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 允許 TCP 連接埠 3389。
3. **重設使用者認證**。 此疑難排解的步驟會重設 hello hello 您指定當您不確定，或已忘記 hello 認證的本機系統管理員帳戶的密碼。
   
    首先，指定 hello 使用者名稱和指派新的密碼認證 toohello`$cred`變數，如下所示：
   
    ```powershell
    $cred=Get-Credential
    ```
   
    現在，更新您的 VM 上的 hello 認證。 hello 下列範例會更新名為的 VM 上的 hello 認證`myVM`在 hello`WestUS`位置並在 hello 資源群組中名為`myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location WestUS -Name "myVMAccessExtension" `
        -UserName $cred.GetNetworkCredential().Username `
        -Password $cred.GetNetworkCredential().Password
    ```
4. **重新啟動您的 VM**。 此疑難排解的步驟可以更正任何基礎的問題已擁有 hello VM 本身。
   
    下列範例會重新啟動的 hello hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`:
   
    ```powershell
    Restart-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
    ```
5. **重新部署您的 VM**。 此步驟中疑難排解重新部署 VM tooanother 主應用程式，Azure toocorrect 內任何基礎的平台或網路問題。
   
    下列範例重新部署的 hello hello 名為 VM`myVM`在 hello`WestUS`位置並在 hello 資源群組中名為`myResourceGroup`:
   
    ```powershell
    Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

如果您仍然遇到 RDP 問題，可以[開啟支援要求](https://azure.microsoft.com/support/options/)或閱讀[更詳細的 RDP 疑難排解概念和步驟](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

## <a name="troubleshoot-vms-created-using-hello-classic-deployment-model"></a>疑難排解使用 hello 傳統部署模型所建立的 Vm
每個疑難排解的步驟之後，嘗試重新連接 toohello VM。

1. **重設您的 RDP 連線**。 遠端連接已停用或 Windows 防火牆規則，例如封鎖 RDP 時，此疑難排解的步驟會重設 hello RDP 組態。
   
    選取您的 VM 中的 hello Azure 入口網站。 按一下 hello **...多個**按鈕，然後按一下**重設遠端存取**:
   
    ![重設 hello Azure 入口網站中的 hello RDP 設定](./media/troubleshoot-rdp-connection/classic-reset-rdp.png)
2. **確認雲端服務端點**。 此疑難排解步驟會確認您的雲端服務 toopermit RDP 流量的端點。 RDP 的 hello 預設連接埠是 TCP 連接埠 3389。 規則 toopermit RDP 流量可能不會自動建立時建立您的 VM。
   
   選取您的 VM 中的 hello Azure 入口網站。 按一下 hello**端點**按鈕 tooview hello 端點目前設定為您的 VM。 確認存在可允許 TCP 連接埠 3389 上 RDP 流量的端點。
   
   hello 下列範例示範有效的端點，允許 RDP 流量：
   
   ![確認 hello Azure 入口網站中的雲端服務端點](./media/troubleshoot-rdp-connection/classic-verify-cloud-services-endpoints.png)
   
   如果您沒有可允許 RDP 流量的端點，請[建立雲端服務端點](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。 允許 TCP tooprivate 連接埠 3389。
3. **檢閱 VM 開機診斷**。 此步驟中疑難排解檢閱 hello VM 主控台記錄檔 toodetermine 如果 hello VM 所報告的問題。 並非所有 VM 都已啟用開機診斷，所以此疑難排解步驟可能是選擇性的。
   
    特定的疑難排解步驟已超出本文的 hello 範圍，但可能會影響 RDP 連線更多問題。 如需有關如何檢閱 hello 主控台記錄檔和 VM 螢幕擷取畫面的詳細資訊，請參閱[Vm 的開機診斷](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/)。
4. **請檢查 VM 資源健全狀況 hello**。 此疑難排解步驟會確認沒有任何已知的問題與 hello 可能會影響連線 toohello VM 的 Azure 平台。
   
    選取您的 VM 中的 hello Azure 入口網站。 捲動 hello 設定窗格 toohello**支援 + 疑難排解**hello 清單的底部附近一節。 按一下 hello**資源健全狀況** 按鈕。 狀況良好的 VM 會報告為 [可用]：
   
    ![檢查 VM hello Azure 入口網站中的資源健全狀況](./media/troubleshoot-rdp-connection/classic-check-resource-health.png)
5. **重設使用者認證**。 此疑難排解的步驟會重設 hello hello 您指定當您不確定或忘記 hello 認證的本機系統管理員帳戶的密碼。
   
    選取您的 VM 中的 hello Azure 入口網站。 捲動 hello 設定窗格 toohello**支援 + 疑難排解**hello 清單的底部附近一節。 按一下 hello**重設密碼** 按鈕。 輸入您的使用者名稱和新密碼。 最後，按一下 hello**儲存**按鈕：
   
    ![重設 hello hello Azure 入口網站中的使用者認證](./media/troubleshoot-rdp-connection/classic-reset-password.png)
6. **重新啟動您的 VM**。 此疑難排解的步驟可以更正任何基礎的問題已擁有 hello VM 本身。
   
    Hello Azure 入口網站中選取您的 VM，然後按一下 hello**概觀** 索引標籤。按一下 hello**重新啟動**按鈕：
   
    ![在 hello Azure 入口網站中重新啟動 VM hello](./media/troubleshoot-rdp-connection/classic-restart-vm.png)

如果您仍然遇到 RDP 問題，可以[開啟支援要求](https://azure.microsoft.com/support/options/)或閱讀[更詳細的 RDP 疑難排解概念和步驟](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

## <a name="troubleshoot-specific-rdp-errors"></a>針對特定 RDP 錯誤進行疑難排解
嘗試 tooconnect tooyour 透過 RDP 的 VM 時，可能會遇到的特定錯誤訊息。 hello 下面是 hello 最常見的錯誤訊息：

* [hello 遠端工作階段中斷，因為沒有任何遠端桌面授權伺服器的可用 tooprovide 授權](troubleshoot-specific-rdp-errors.md#rdplicense)。
* [遠端桌面找不到 hello 電腦 「 名稱 」](troubleshoot-specific-rdp-errors.md#rdpname)。
* [發生驗證錯誤。hello 本機安全性授權無法連絡](troubleshoot-specific-rdp-errors.md#rdpauth)。
* [Windows 安全性錯誤：您的認證無法運作](troubleshoot-specific-rdp-errors.md#wincred)。
* [這部電腦無法連線遠端電腦的 toohello](troubleshoot-specific-rdp-errors.md#rdpconnect)。

## <a name="additional-resources"></a>其他資源
如果沒有任何這些錯誤發生，您仍然無法連線 toohello 透過遠端桌面的 VM 讀取詳細的 hello[疑難排解指南針對遠端桌面](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
* 如需疑難排解存取 VM 上執行的應用程式的步驟，請參閱[疑難排解存取 tooan 應用程式在 Azure VM 上執行](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
* 如果您有使用安全殼層 (SSH) tooconnect tooa Linux VM 在 Azure 中的問題，請參閱[疑難排解 SSH 連線 tooa 在 Azure 中的 Linux VM](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

