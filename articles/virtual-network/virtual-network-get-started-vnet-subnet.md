---
title: "您的第一個 Azure 虛擬網路的 aaaCreate |Microsoft 文件"
description: "了解如何 toocreate Azure 虛擬網路 (VNet)，連接兩個虛擬機器 (VM) toohello VNet，以及連接 toohello Vm。"
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2016
ms.author: jdial
ms.openlocfilehash: 1981524cf706d5ebc83b1ff77735617550ff058a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-virtual-network"></a>建立您的第一個虛擬網路

深入了解如何 toocreate 兩個子網路，虛擬網路 (VNet) 中建立兩個虛擬機器 (VM)，並連接的 hello 子網路，每個 VM tooone hello 下列圖片所示：

![虛擬網路圖表](./media/virtual-network-get-started-vnet-subnet/vnet-diagram.png)

Azure 虛擬網路 (VNet) 是網路的您自己 hello 雲端中的表示法。 您可以控制 Azure 網路設定，以及定義 DHCP 位址區塊、DNS 設定、安全性原則和路由。 深入了解 VNet 概念，讀取 hello toolearn[虛擬網路概觀](virtual-networks-overview.md)發行項。 完成下列步驟 toocreate hello 資源 hello 圖片所示的 hello:

1. [建立具有兩個子網路的 VNet](#create-vnet)
2. [建立兩個 Vm，各有一個網路介面 (NIC)](#create-vms)，並將相關聯的網路安全性 (nsg) tooeach NIC
3. [從 hello Vm 連接 tooand](#connect-to-from-vms)
4. [刪除所有資源](#delete-resources)。 您會產生費用，某些 hello 它們正在佈建時，在此練習中建立的資源。 toominimize hello 費用之後完成 hello 練習，請, 務必 toocomplete hello 步驟中所建立的這個區段 toodelete hello 資源。

您必須完成的 hello 本文章中的步驟之後，如何使用 VNet 的基本知識。 接下來的步驟會提供，因此您可以進一步了解如何 toouse 更深層級的 Vnet。

## <a name="create-vnet"></a>建立具有兩個子網路的虛擬網路

toocreate 兩個子網路，完成 hello 遵照的步驟，與虛擬網路。 不同的子網路通常是使用 toocontrol hello 流量子網路之間的流量。

1. 登入 toohello [Azure 入口網站](<https://portal.azure.com>)。 如果您沒有帳戶，您可以註冊[免費試用一個月](https://azure.microsoft.com/free)。 
2. 在 hello**我的最愛**窗格，hello 入口網站中，按一下**新增**。
3. 在 hello**新增**刀鋒視窗中，按一下 **網路**。 在 hello**網路**刀鋒視窗中，按一下 **虛擬網路**hello 下列圖片所示：

    ![虛擬網路圖表](./media/virtual-network-get-started-vnet-subnet/virtual-network.png)

4.  在 hello**虛擬網路**刀鋒視窗中，保留*資源管理員*hello 部署模型，然後按一下以選取**建立**。
5.  在 hello**刀鋒視窗中建立虛擬網路**出現，輸入 hello 下列值，然後按一下 **建立**:

    |**設定**|**值**|**詳細資料**|
    |---|---|---|
    |**名稱**|*MyVNet*|hello 名稱必須是唯一 hello 的資源群組中。|
    |**位址空間**|*10.0.0.0/16*|您可以使用 CIDR 標記法指定您想要的任何位址空間。|
    |**子網路名稱**|前端|hello 子網路名稱必須是唯一 hello 虛擬網路內。|
    |**子網路位址範圍**|*10.0.0.0/24*| 您指定的 hello 範圍必須存在於 hello 您定義 hello 虛擬網路的位址空間。|
    |**訂用帳戶**|*[您的訂用帳戶]*|選取的訂用帳戶 toocreate hello VNet 中。 VNet 存在於單一訂用帳戶中。|
    |**資源群組**|**建立新的：**MyRG|建立資源群組。 hello 資源群組名稱必須是唯一 hello 您選取的訂用帳戶內。 深入了解資源群組，請閱讀 hello toolearn[資源管理員](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-groups)概觀文件。|
    |**位置**|美國西部| 通常會選取 hello 位置，這是最接近 tooyour 實體位置。|

    hello VNet 花幾秒 toocreate。 一旦建立之後，您會看到 hello Azure 入口網站儀表板。

6. Hello，hello Azure 入口網站中建立的虛擬網路與**我的最愛**] 窗格中，按一下 [**所有資源**。 按一下 hello **MyVNet**虛擬網路中 hello**所有資源**刀鋒視窗。 如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入*MyVNet*在 hello**依名稱篩選...** 方塊 tooeasily 存取 hello VNet。
7. hello **MyVNet**刀鋒視窗會開啟並顯示 hello VNet 的相關資訊，hello 下列圖片所示：

    ![虛擬網路圖表](./media/virtual-network-get-started-vnet-subnet/myvnet.png)

8. Hello 上一張圖片所示，按一下**子網路**toodisplay hello hello VNet 內的子網路的清單。 hello 存在的子網路是**前端**，hello 您在步驟 5 中建立的子網路。
9. 在 hello MyVNet-子網路刀鋒視窗中，按一下  **+ 子網路**toocreate hello 與子網路下列資訊，然後按一下**確定**toocreate hello 子網路：

    |**設定**|**值**|**詳細資料**|
    |---|---|---|
    |**名稱**|後端|hello 名稱必須是唯一 hello 虛擬網路內。|
    |**位址範圍**|*10.0.1.0/24*|您指定的 hello 範圍必須存在於 hello 您定義 hello 虛擬網路的位址空間。|
    |**網路安全性群組**和**路由表**|「無」(預設值)|網路安全性群組 (NSG) 涵蓋於本文章稍後部分。 更多關於使用者定義的路由，讀取 hello toolearn[使用者定義的路由](virtual-networks-udr-overview.md)發行項。|

10. Hello 新的子網路加入 toohello VNet 之後，您可以關閉 hello **MyVNet – 子網路**刀鋒視窗中，然後關閉 hello**所有資源**刀鋒視窗。

## <a name="create-vms"></a>建立虛擬機器

與 hello VNet 子網路建立，您可以建立 hello Vm。 針對此練習中，這兩個 Vm 執行 Windows Server 作業系統 hello，不過可以執行任何 Azure，包括數個不同的 Linux 發行版本所支援的作業系統。

### <a name="create-web-server-vm"></a>建立 VM 的 hello web 伺服器

toocreate hello web 伺服器 VM，完成下列步驟的 hello:

1. 在 hello Azure 入口網站的 我的最愛 窗格中，按一下 **新增**，**計算**，然後**Windows Server 2016 Datacenter**。
2. 在 hello **Windows Server 2016 Datacenter**刀鋒視窗中，按一下 **建立**。
3. 在 hello**基本概念**刀鋒視窗中，輸入或選取下列值的 hello，然後按一下**確定**:

    |**設定**| **值**|**詳細資料**|
    |---|---|---|
    |**名稱**|*MyWebServer*|此 VM 伺服器做為網際網路資源連線的網頁伺服器。|
    |**VM 磁碟類型**|SSD|
    |**使用者名稱**|您的選擇|
    |**密碼和確認密碼**|您的選擇|
    | **訂用帳戶**|*<Your subscription>*|hello 訂用帳戶必須是 hello 相同訂用帳戶，您選取在步驟 5 中的 hello[建立具有兩個子網路的虛擬網路](#create-vnet)本文一節。 hello VNet 連接 VM toomust 存在於 hello 相同訂用帳戶為 hello VM。|
    |**資源群組**|**使用現有︰**選取 MyRG|雖然我們會使用相同的資源群組，如同 hello VNet，hello 的 hello 資源沒有 tooexist hello 中相同的資源群組。|
    |**位置**|美國西部|hello 位置必須是 hello hello 的步驟 5 中指定的相同位置[建立具有兩個子網路的虛擬網路](#create-vnet)本文一節。 Vm 和 hello Vnet 連線 toomust 存在於 hello 相同位置。|

4. 在 hello**大小選擇 「**刀鋒視窗中，按一下  *DS1_V2 標準*，然後按一下 **選取**。 讀取 hello [Windows VM 大小](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json)Azure 所支援的所有 Windows VM 大小的清單的發行項。
5. 在 hello**設定**刀鋒視窗中，輸入或選取下列值的 hello，然後按一下**確定**:

    |**設定**|**值**|**詳細資料**|
    |---|---|---|
    |**儲存體：使用受控磁碟**|*是*||
    |**虛擬網路**| 選取 MyVNet|您可以選取任何存在於 hello 相同的 VNet 位置 hello 您要建立的 VM。 深入了解 Vnet 和子網路，讀取 hello toolearn[虛擬網路](virtual-networks-overview.md)發行項。|
    |**子網路**|選取 [前端]|您可以選取存在於 hello VNet 內的任何子網路。|
    |**公用 IP 位址**|接受預設值 hello|公用 IP 位址可讓您 tooconnect toohello VM 從 hello 網際網路。 更多關於公用 IP 位址，讀取 hello toolearn [IP 位址](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses)發行項。|
    |**網路安全性群組 (防火牆)**|接受預設值 hello|按一下 hello **（新） MyWebServer nsg**預設 NSG hello 入口網站建立 tooview 其設定。 在 hello**建立網路安全性群組**刀鋒視窗中開啟，請注意，它擁有一個輸入規則，允許從任何來源 IP 位址的 TCP/3389 (RDP) 流量。|
    |**所有其他值**|接受 hello 預設值|深入了解剩餘讀取 hello 設定 hello toolearn[有關 Vm](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json)發行項。|

    網路安全性群組 (NSG) 可讓您可以傳送 hello VM 從 tooand 的網路流量 hello 類型 toocreate 輸入/輸出規則。 根據預設，所有的輸入的流量 toohello VM 遭到拒絕。 您可以為實際執行網頁伺服器針對 TCP/80 (HTTP) 和 TCP/443 (HTTPS) 新增額外的輸入規則。 因為根據預設沒有輸出流量的規則，所以允許所有輸出流量。 您可以新增/移除規則 toocontrol 流量根據您的原則。 讀取 hello[網路安全性群組](virtual-networks-nsg.md)文章 toolearn 更多關於 Nsg。

6.  在 hello**摘要**刀鋒視窗中，檢閱 hello 設定，然後按一下**確定**toocreate hello VM。 狀態磚會顯示 hello 入口網站儀表板上，為 VM 建立的 hello。 可能需要幾分鐘的時間 toocreate。 您不需要 toowait 它 toocomplete。 您可以繼續 toohello hello 建立 VM 時的下一個步驟。

### <a name="create-database-server-vm"></a>建立 hello 資料庫伺服器 VM

toocreate hello 資料庫伺服器 VM，完成下列步驟的 hello:

1.  在 hello 我的最愛 窗格中，按一下 **新增**，**計算**，然後**Windows Server 2016 Datacenter**。
2.  在 hello **Windows Server 2016 Datacenter**刀鋒視窗中，按一下 **建立**。
3.  在 hello**刀鋒視窗中的基本概念**、 輸入或選取 hello 下列值，然後按一下**確定**:

    |**設定**|**值**|**詳細資料**|
    |---|---|---|
    |**名稱**|MyDBServer|此 VM 做為資料庫伺服器 hello web 伺服器連接的但該 hello 無法連接網際網路。|
    |**VM 磁碟類型**|SSD||
    |**使用者名稱**|您的選擇||
    |**密碼和確認密碼**|您的選擇||
    |**訂用帳戶**|<Your subscription>|hello 訂用帳戶必須是 hello 相同的 hello 步驟 5 中選取的訂用帳戶[建立具有兩個子網路的虛擬網路](#create-vnet)本文一節。|
    |**資源群組**|**使用現有︰**選取 MyRG|雖然我們會使用相同的資源群組，如同 hello VNet，hello 的 hello 資源沒有 tooexist hello 中相同的資源群組。|
    |**位置**|美國西部|hello 位置必須是 hello hello 的步驟 5 中指定的相同位置[建立具有兩個子網路的虛擬網路](#create-vnet)本文一節。|

4.  在 hello**大小選擇 「**刀鋒視窗中，按一下  *DS1_V2 標準*，然後按一下 **選取**。
5.  在 hello**設定**刀鋒視窗中，輸入或選取下列值的 hello，然後按一下**確定**:

    |**設定**|**值**|**詳細資料**|
    |----|----|---|
    |**儲存體：使用受控磁碟**|*是*||
    |**虛擬網路**|選取 MyVNet|您可以選取任何存在於 hello 相同的 VNet 位置 hello 您要建立的 VM。|
    |**子網路**|選取*後端*按一下 hello**子網路**方塊，然後選取**後端**從 hello**選擇子網路**刀鋒視窗|您可以選取存在於 hello VNet 內的任何子網路。|
    |**公用 IP 位址**|None – 按一下 hello 預設位址，然後按一下 **無**從 hello**選擇公用 IP 位址**刀鋒視窗|沒有公用 IP 位址，您僅能連線 toohello VM 從另一個 VM 連接 toohello 相同的 VNet。 您無法直接從 hello 網際網路連線 tooit。|
    |**網路安全性群組 (防火牆)**|接受預設值 hello| NSG 也建立 hello MyWebServer VM 此 NSG hello 預設具有 hello 像相同的預設輸入的規則。 您可以為資料庫伺服器針對 TCP 1433 (MS SQL) 新增額外的輸入規則。 因為根據預設沒有輸出流量的規則，所以允許所有輸出流量。 您可以新增/移除規則 toocontrol 流量根據您的原則。|
    |**所有其他值**|接受 hello 預設值||

6.  在 hello**摘要**刀鋒視窗中，檢閱 hello 設定，然後按一下**確定**toocreate hello VM。 狀態磚會顯示 hello 入口網站儀表板上，為 VM 建立的 hello。 可能需要幾分鐘的時間 toocreate。 您不需要 toowait 它 toocomplete。 您可以繼續 toohello hello 建立 VM 時的下一個步驟。

## <a name="review"></a>檢閱資源

雖然您可以建立一個 VNet 和兩個 Vm，hello hello MyRG 資源群組中，為您建立數個其他資源的 Azure 入口網站。 藉由完成下列步驟的 hello 檢閱 hello hello MyRG 資源群組的內容：

1. 在 hello**我的最愛** 窗格中，按一下 **更多服務**。
2. 在 hello**更多服務**窗格中，輸入*資源群組*具有 hello word hello 方塊中*篩選*中。 按一下**資源群組**當您看到它在 hello 篩選清單。
3. 在 [hello**資源群組**] 窗格中，按一下 hello *MyRG*資源群組。 如果您有許多現有的資源群組訂閱中，您可以輸入*MyRG*中包含的 hello 文字的 hello 方塊*依名稱篩選...* tooquickly 存取 hello MyRG 資源群組。
4.  在 hello **MyRG**刀鋒視窗中，您會看到 hello 資源群組包含 12 種資源，hello 下列圖片所示：

    ![資源群組內容](./media/virtual-network-get-started-vnet-subnet/resource-group-contents.png)

深入了解 Vm、 磁碟和儲存體帳戶讀取 hello toolearn[虛擬機器](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json)，[磁碟](../virtual-machines/windows/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-network%2ftoc.json)，和[儲存體帳戶](../storage/common/storage-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json)概觀文件。 您可以看到 hello 兩個預設 Nsg hello 入口網站為您建立。 您也可以查看該 hello 入口網站建立兩個網路介面 (NIC) 的資源。 一個 NIC 透過 hello VNet 啟用 VM tooconnect tooother 資源。 讀取 hello [NIC](virtual-network-network-interface.md)文章 toolearn 更多關於 Nic。 hello 入口網站也會建立一個公用 IP 位址資源。 公用 IP 位址是公用 IP 位址資源的一項設定。 更多關於公用 IP 位址，讀取 hello toolearn [IP 位址](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses)發行項。

## <a name="connect-to-from-vms"></a>Toohello Vm 連線

使用您的 VNet 和兩個所建立的 Vm，您現在可以 hello hello 下列各節中的步驟，以連接 toohello Vm:

### <a name="connect-from-internet"></a>從 hello 網際網路連線 toohello web server VM

tooconnect toohello web 伺服器 VM 從 hello 網際網路，完成下列步驟的 hello:

1. 在 hello 入口網站開啟 hello MyRG 資源群組，藉由完成 hello 步驟 hello[檢閱資源](#review)本文一節。
2. 在 hello **MyRG**刀鋒視窗中，按一下 hello **MyWebServer** VM。
3. 在 hello **MyWebServer**刀鋒視窗中，按一下**連接**hello 下列圖片所示：

    ![連接 tooweb server VM](./media/virtual-network-get-started-vnet-subnet/webserver.png)

4. 允許您的瀏覽器 toodownload hello *MyWebServer.rdp*檔案，然後將它開啟。
5. 如果您收到對話方塊方塊中，通知您該 hello hello 遠端連線的發行者無法驗證，請按一下**連接**。
6. 當輸入您的認證，請確定您與您指定在步驟 3 中的 hello hello 使用者名稱和密碼登入[建立 hello web 伺服器 VM](#create-web-server-vm)本文一節。 如果 hello **Windows 安全性**出現方塊不會列出 hello 正確的認證，您可能需要 tooclick**更多途徑**，然後**使用不同的帳戶**，因此您可以指定 hello 正確的使用者名稱和密碼）。 按一下**確定**tooconnect toohello VM。
7. 如果您收到**遠端桌面連線**方塊通知您 hello hello 遠端電腦的身分識別無法驗證，按一下**是**。
8. 現在您已經從 hello 網際網路連線的 toohello MyWebServer VM。 將保留在 hello 遠端桌面連線開啟 toocomplete hello 步驟 hello 下一節。

hello 遠端連線是 toohello 指派 toohello 公用 IP 位址資源 hello 入口網站的 hello 的步驟 5 中建立公用 IP 位址[建立具有兩個子網路的虛擬網路](#create-vnet)本文一節。 因為在 hello 建立 hello 預設規則，便會允許 hello 連接**MyWebServer nsg** NSG 允許 TCP/3389 (RDP) 輸入 toohello VM 從任何來源 IP 位址。 如果您嘗試透過任何其他連接埠 tooconnect toohello VM，hello 連線會失敗，除非您新增其他的輸入的規則 toohello NSG 允許 hello 其他連接埠。

>[!NOTE]
>如果您新增其他的輸入的規則 toohello NSG，請確定該 hello hello 的 Windows 防火牆上開啟相同的連接埠，或 hello 連接會失敗。
>

### <a name="connect-to-internet"></a>從 hello web 伺服器 VM 連線 toohello 網際網路

tooconnect 輸出 toohello 網際網路從 hello web 伺服器 VM，完成下列步驟的 hello:

1. 如果您還沒有開啟 MyWebServerVM 遠端連線 toohello，讓遠端連線 toohello VM hello 中的 hello 步驟[連接 toohello 網頁伺服器從 hello 網際網路 VM](#connect-from-internet)本文一節。
2. 從 hello Windows 桌面上，開啟 Internet Explorer。 在 hello**安裝 Internet Explorer 11**對話方塊中，按一下**不使用建議的設定**，然後按一下 **確定**。 它是建議的 tooaccept hello 建議實際執行伺服器的設定。
3. 在 hello Internet Explorer 網址列中輸入[bing.com](http:www.bing.com)。如果您收到的 Internet Explorer 對話方塊中，按一下**新增**，然後**新增**在 hello**信任的網站**對話方塊，按一下**關閉**。 對於任何其他 Internet Explorer 對話方塊重複此程序。
4. 在 hello Bing 搜尋頁面中，輸入*whatsmyipaddress*，然後按一下 hello 放大鏡按鈕。 Bing 傳回 hello 公用 IP 位址指派 toohello 公用 IP 位址資源建立 hello 入口網站，當您建立 hello VM。 如果您檢查 hello hello 設定**MyWebServer ip**資源，您看到 hello 分派 toohello 公用 IP 位址資源，相同的 IP 位址中遵循的 hello 圖片所示。 hello IP 位址指派 tooyour VM 不過這會不同。

    ![連接 tooweb server VM](./media/virtual-network-get-started-vnet-subnet/webserver-pip.png)

5.  將保留在 hello 遠端桌面連線開啟 toocomplete hello 步驟 hello 下一節。

因為預設會允許所有從 hello VM 的輸出連線，您就可以 tooconnect toohello 網際網路從 hello VM。 您可以限制的傳出連線，藉由新增加入規則 toohello NSG 套用 toohello NIC，toohello 子網路 hello NIC 連線到，或兩者。

如果 hello VM 放置於 hello 停止 （取消配置） 的狀態是使用 hello 入口網站，可以變更 hello 公用 IP 位址。 如果您需要 hello 公用 IP 位址永遠不會變更，您可以使用 hello 靜態配置方法 hello IP 位址，而不是 hello 動態配置方法 （即 hello 預設值）。 深入了解 toolearn hello 分派方法之間的差異讀取 hello [IP 位址類型和配置方法](virtual-network-ip-addresses-overview-arm.md)發行項。

### <a name="webserver-to-dbserver"></a>從 hello web 伺服器 VM 連線 toohello 資料庫伺服器 VM

tooconnect toohello 資料庫伺服器 VM 從 hello web 伺服器 VM，完成下列步驟的 hello:

1. 如果您還沒有開啟 MyWebServer VM 遠端連線 toohello，讓遠端連線 toohello VM hello 中的 hello 步驟[連接 toohello 網頁伺服器從 hello 網際網路 VM](#connect-from-internet)本文一節。
2. 按一下 hello 左下角的 hello Windows 桌面上，hello [開始] 按鈕，然後開始輸入*遠端桌面*。 當顯示 hello 開始 功能表清單**遠端桌面連線**，按一下它。
3. 在 hello**遠端桌面連線**對話方塊方塊中，輸入*MyDBServer* hello 電腦名稱，然後按一下**連接**。
4. 輸入 hello 使用者名稱和密碼，您輸入在步驟 3 中的 hello[建立 hello 資料庫伺服器 VM](#create-database-server-vm) > 一節的本文中，然後按一下 **確定**。
5. 如果您收到對話方塊方塊中，通知您該 hello 的身分識別 hello 遠端電腦無法驗證，請按一下**是**。
6. 保留 hello 遠端桌面連線 tooboth 伺服器開啟 toocomplete hello hello 下一節中的步驟。

您即可以 toomake hello 連接 toohello 資料庫伺服器 VM 從 hello 下列原因，hello web 伺服器 VM:

- Hello 預設的 hello 的步驟 5 中建立的 NSG 中的任何來源 IP 已啟用的輸入的連線 TCP/3389[建立 hello 資料庫伺服器 VM](#create-database-server-vm)本文一節。
- 起始從 hello web 伺服器 VM，也就是連接的 toohello hello 連接做為 hello 資料庫伺服器 VM 的同一個 VNet。 tooconnect tooa 沒有公用的 IP 位址指派 tooit 的 VM，您必須從連接另一個 VM 連接 toohello 相同 VNet，即使 hello VM 是已連線的 tooa 不同的子網路。
- 即使 hello Vm 連接的 toodifferent 子網路，Azure 會建立啟用子網路之間連線的預設路由。 您可以建立您自己的不過，覆寫 hello 預設路由。 讀取 hello[使用者定義的路由](virtual-networks-udr-overview.md)文章 toolearn 深入了解 Azure 中的路由。

如果您嘗試 tooinitiate hello 網際網路遠端連線 toohello 資料庫伺服器 VM，您可以如同在 hello[連接 toohello 網頁伺服器從 hello 網際網路 VM](#connect-from-internet) > 一節的本文中，您會看到該 hello**連接**選項呈現灰色。連接灰色，因為沒有任何公用 IP 位址指派 toohello VM，所以不可能從 hello 網際網路的傳入的連接 tooit。

### <a name="connect-toohello-internet-from-hello-database-server-vm"></a>從 hello 資料庫伺服器 VM 連線 toohello 網際網路

從 hello 資料庫伺服器 VM，輸出 toohello 網際網路連線藉由完成下列步驟的 hello:

1. 如果您還沒有從 hello MyWebServer VM 開啟 MyDBServer VM 遠端連線 toohello，完成 hello 步驟 hello[連接 toohello 資料庫伺服器 VM 從 hello web 伺服器 VM](#webserver-to-dbserver)本文一節。
2. 從 hello hello MyDBServer VM 上的 Windows 桌面上，開啟 Internet Explorer 並回應 toohello 對話方塊，如同在步驟 2 和 3 的 hello [toohello 網際網路連線從 hello web 伺服器 VM](#connect-to-internet)本文一節。
3. 在 hello 網址列中輸入[bing.com](http:www.bing.com)。
4. 按一下**新增**hello Internet Explorer 出現對話方塊，然後在**新增**，然後**關閉**在 hello**信任**網站 對話方塊。 在顯示的任何其他對話方塊中完成這些步驟。
5. 在 hello Bing 搜尋頁面中，輸入*whatsmyipaddress*，然後按一下 hello 放大鏡按鈕。 Bing hello Azure 基礎結構所傳回公用 IP 位址目前已指派 toohello hello VM。 6. 關閉 hello 遠端桌面 toohello MyDBServer VM 從 hello MyWebServer VM，然後關閉 hello 遠端連線 toohello MyWebServer VM。

hello 輸出連線 toohello 網際網路允許，因為根據預設，允許所有輸出流量即使公用 IP 位址資源未指派 toohello MyDBServer VM。 所有的 Vm，根據預設，會無法 tooconnect 輸出 toohello 網際網路，不論公用 IP 位址指派的資源 toohello VM。 您不能 tooconnect toohello 公用 IP 位址從 hello 網際網路不過，像是已能 toofor hello MyWebServer VM 具有公用 IP 位址指派的資源。

## <a name="delete-resources"></a>刪除所有資源

在本文中完成下列步驟的 hello 建立 toodelete 所有資源：

1. 在本文中，完成建立 tooview hello MyRG 資源群組的步驟 1-3 中的 hello[檢閱資源](#review)本文一節。 同樣地，檢閱 hello 資源群組中的 hello 資源。 如果您建立 hello MyRG 資源群組、 每個先前步驟中，您會看到在步驟 4 中的 hello 圖片所示 hello 12 種資源。
2. 在 hello MyRG 刀鋒視窗中，按一下 hello**刪除** 按鈕。
3. hello 入口網站需要您想要 toodelete hello 資源群組 tooconfirm tootype hello 名稱它。 如果您看到資源以外的 hello 步驟 4 中所示的 hello 資源[檢閱資源](#review)> 一節的本文中，按一下 **取消**。 如果您看到只有 hello 12 資源建立為這份文件的一部分時，輸入*MyRG* hello 資源群組名稱，然後按一下**刪除**。 刪除資源群組會刪除 hello 資源群組中的所有資源，所以一定會確定 tooconfirm hello 內容的資源群組然後再刪除。 hello 入口網站刪除 hello 的資源群組中包含的所有資源，然後都刪除本身 hello 資源群組。 這個程序需要幾分鐘的時間。

## <a name="next-steps"></a>接續步驟

在本練習中，您會建立 VNet 和兩個 VM。 在建立 VM 期間，指定一些自訂設定，並且接受數個預設設定。 我們建議您先閱讀下列文章，生產環境的 Vnet 和 tooensure 您了解所有可用設定的 Vm，在部署之前的 hello:

- [虛擬網路](virtual-networks-overview.md)
- [公用 IP 位址](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses)
- [網路介面](virtual-network-network-interface.md)
- [網路安全性群組](virtual-networks-nsg.md)
- [虛擬機器](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
