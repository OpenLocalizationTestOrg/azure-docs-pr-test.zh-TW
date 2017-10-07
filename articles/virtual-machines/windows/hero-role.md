---
title: "第一個 Windows VM 上的 IIS aaaInstall |Microsoft 文件"
description: "試驗您第一次安裝 IIS，並開啟連接埠 80 使用的 Windows 虛擬機器 hello Azure 入口網站。"
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6334ea45-db6b-4e08-abb5-1f98927ebc34
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cynthn
ms.openlocfilehash: 7cfed6197df058c4569d111ee88961da7c6fe0b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a>試驗在 Windows VM 上安裝角色
一旦第一個虛擬機器 (VM) 設定和執行，您可以移動 tooinstalling 的軟體和服務。 此教學課程中，我們 toouse 伺服器管理員在 hello Windows Server VM tooinstall IIS。 然後，我們會建立網路安全性群組 (NSG) 使用 hello Azure 入口網站 tooopen 連接埠 80 tooIIS 流量。 

如果您尚未建立您的第一個 VM，您應該移回太[hello Azure 入口網站中建立第一個 Windows 虛擬機器](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)再繼續進行本教學課程。

## <a name="make-sure-hello-vm-is-running"></a>請確認 VM 正在執行中的 hello
1. 開啟 hello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 中樞功能表中，按一下 **虛擬機器**。 從 [hello] 清單中選取 hello 虛擬機器。
3. 如果 hello 狀態是**已停止 （取消配置）**，按一下 hello**啟動**按鈕 hello **Essentials**刀鋒視窗中的 hello VM。 如果 hello 狀態是**執行**，您可以移 toohello 下一個步驟。

## <a name="connect-toohello-virtual-machine-and-sign-in"></a>連接 toohello 虛擬機器並登入
1. 在 hello 中樞功能表中，按一下 **虛擬機器**。 從 [hello] 清單中選取 hello 虛擬機器。
2. 在 hello 刀鋒視窗中的 hello 虛擬機器，按一下 **連接**。 這會建立並下載遠端桌面通訊協定檔案 （.rdp 檔案），就像是快顯 tooconnect tooyour 機器。 您可能想 toosave hello 檔案 tooyour 桌面，以方便存取。 **開啟**此檔案 tooconnect tooyour VM。
   
    ![螢幕擷取畫面的 hello Azure 入口網站的顯示方式 tooconnect tooyour VM](./media/hero-role/connect.png)
3. 您會收到警告該 hello.rdp 取自未知的發行者。 這是正常現象。 在 hello 遠端桌面視窗中，按一下 **連接**toocontinue。
   
    ![未知發行者相關警告的螢幕擷取畫面](./media/hero-role/rdp-warn.png)
4. 在 [hello Windows 安全性] 視窗中，型別 hello 使用者名稱和密碼 hello 建立時，您所建立的本機帳戶的 hello VM。 hello 使用者名稱輸入為*vmname*&#92;*使用者名稱*，然後按一下 **確定**。
   
    ![輸入 hello VM 名稱、 使用者名稱和密碼的螢幕擷取畫面](./media/hero-role/credentials.png)
5. 您會收到警告無法驗證該 hello 憑證。 這是正常現象。 按一下**是**tooverify hello hello 虛擬機器的身分識別，並完成登入。
   
   ![螢幕擷取畫面顯示一則訊息 trap 驗證 hello 識別 hello VM](./media/hero-role/cert-warning.png)

如果您在執行 tootrouble tooconnect 再試一次時，請參閱[疑難排解遠端桌面連線 tooa windows Azure 虛擬機器](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

## <a name="install-iis-on-your-vm"></a>在您的 VM 上安裝 IIS
既然您已登入 toohello VM，我們會安裝伺服器角色，以便您可以試驗更多。

1. 開啟 [伺服器管理員]  \(如果尚未開啟)。 按一下 hello**啟動**功能表，然後再按一下**伺服器管理員**。
2. 在**伺服器管理員**，選取**本機伺服器**hello 左窗格中。 
3. 在 hello 功能表中，選取 **管理** > **新增角色及功能**。
4. 在 [hello 新增角色及功能精靈] 的 hello**安裝類型**頁面上，選擇**角色型或功能型安裝**，然後按一下**下一步**。
   
    ![螢幕擷取畫面顯示 hello 新增角色及功能精靈] 索引標籤的 [安裝類型](./media/hero-role/role-wizard.png)
5. 選取 hello VM 從 hello 伺服器集區，然後按一下**下一步**。
6. 在 hello**伺服器角色**頁面上，選取**網頁伺服器 (IIS)**。
   
    ![螢幕擷取畫面顯示 hello 新增角色及功能精靈] 索引標籤的 [伺服器角色](./media/hero-role/add-iis.png)
7. 在 新增所需的 IIS 功能的相關快顯 hello，請確定**包含管理工具**已選取，然後按一下**新增功能**。 當快顯 hello 關閉時，按一下**下一步**hello 精靈中。
   
    ![顯示快顯 tooconfirm 新增 hello IIS 角色螢幕擷取畫面](./media/hero-role/confirm-add-feature.png)
8. 在 hello 功能頁面上，按一下 **下一步**。
9. 在 hello**網頁伺服器 (IIS)**頁面上，按一下**下一步**。 
10. 在 hello**角色服務**頁面上，按一下**下一步**。 
11. 在 hello**確認**頁面上，按一下**安裝**。 
12. Hello 安裝完成時，按一下**關閉**hello 精靈。

## <a name="open-port-80"></a>開啟連接埠 80
為了讓 VM tooaccept 輸入流量透過連接埠 80，您需要 tooadd 輸入的規則 toohello 網路安全性群組。 

1. 開啟 hello [Azure 入口網站](https://portal.azure.com)。
2. 在**虛擬機器**選取 hello 您所建立的 VM。
3. 在 hello 虛擬機器設定中，選取**網路介面**，然後選取 hello 現有網路介面。
   
    ![顯示 hello 的 hello 虛擬機器設定網路介面螢幕擷取畫面](./media/hero-role/network-interface.png)
4. 在**Essentials** hello 網路介面，按一下 hello**網路安全性群組**。
   
    ![顯示 hello Essentials > 一節 hello 網路介面的螢幕擷取畫面](./media/hero-role/select-nsg.png)
5. 在 hello **Essentials** hello NSG 刀鋒視窗中的，您應該有一個現有的預設輸入規則**預設允許 rdp**它可讓您 toolog toohello VM 中。 您會加入另一個輸入的規則 tooallow IIS 流量。 按一下 [輸入安全性規則] 。
   
    ![顯示 hello hello NSG 的 Essentials > 一節螢幕擷取畫面](./media/hero-role/inbound.png)
6. 在 [輸入安全性規則] 中，按一下 [新增]。
   
    ![安全性規則顯示 hello 按鈕 tooadd 螢幕擷取畫面](./media/hero-role/add-rule.png)
7. 在 [輸入安全性規則] 中，按一下 [新增]。 型別**80**在 hello 連接埠範圍，並確定**允許**已選取。 完成時按一下 [確定]。
   
    ![安全性規則顯示 hello 按鈕 tooadd 螢幕擷取畫面](./media/hero-role/port-80.png)

如需有關 Nsg，輸入和輸出規則，請參閱[允許外部存取 tooyour VM 使用 hello Azure 入口網站](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="connect-toohello-default-iis-website"></a>連接 toohello 預設 IIS 網站
1. 在 hello Azure 入口網站，按一下 **虛擬機器**，然後選取您的 VM。
2. 在 hello **Essentials**刀鋒視窗，複製您**公用 IP 位址**。
   
    ![螢幕擷取畫面顯示其中 toofind hello VM 的公用 IP 位址](./media/hero-role/ipaddress.png)
3. 開啟瀏覽器，並在 hello 網址列中輸入公用 IP 位址如下： http://<publicIPaddress>按一下**Enter** toogo toothat 位址。
4. 您的瀏覽器應該開啟 hello 預設 IIS web 網頁。 它看起來會像這樣：
   
    ![在瀏覽器中顯示哪些 hello 預設 IIS 頁面螢幕擷取畫面看起來像](./media/hero-role/iis-default.png)

## <a name="next-steps"></a>後續步驟
* 您也可以試驗[連接資料磁碟](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)tooyour 虛擬機器。 資料磁碟可為虛擬機器提供更多的儲存空間。

