---
title: "aaaCreate，變更或刪除的 Azure 網路介面 |Microsoft 文件"
description: "了解什麼是網路介面和 toocreate，如何變更設定，及刪除其中一個。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: dcb6cdbd73bc0d0ca4efb9d972d370cf2d54abb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-network-interface"></a>建立、變更或刪除網路介面

了解如何 toocreate，變更設定，以及刪除網路介面。 網路介面可讓您的 Azure 虛擬機器 toocommunicate 與網際網路、 Azure 和內部部署資源。 建立虛擬機器使用 hello Azure 入口網站時，hello 入口網站會建立一個網路介面以供您的預設設定。 您可以改為選擇 toocreate 利用自訂設定的網路介面，並新增一或多個網路介面 tooa 虛擬機器，您在建立時。 您也可以針對現有的網路介面 toochange 預設網路介面設定。 本文說明如何變更現有的設定，例如指派網路篩選條件 （網路安全性群組）、 子網路指派、 DNS 伺服器設定及 IP 轉寄 toocreate 自訂設定的網路介面，並刪除網路介面。

如果您需要 tooadd，變更或移除網路介面的 IP 位址讀取 hello[管理 IP 位址](virtual-network-network-interface-addresses.md)發行項。 如果您需要 tooadd 網路介面，或從虛擬機器移除網路介面，讀取 hello[新增或移除網路介面](virtual-network-network-interface-vm.md)發行項。


## <a name="before-you-begin"></a>開始之前

這份文件的任何部分中的步驟完成 hello 之前完成任何下列工作：

- 檢閱 hello [Azure 限制](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits)文章 toolearn 有關限制的網路介面。
- 登入 toohello Azure[入口網站](https://portal.azure.com)，Azure 命令列介面 (CLI) 或 Azure PowerShell 的 Azure 帳戶。 如果您還沒有 Azure 帳戶，請註冊[免費試用帳戶](https://azure.microsoft.com/free)。
- 如果使用 PowerShell 命令在本文中 toocomplete 工作[安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json)。 確定您擁有 hello hello Azure PowerShell 指令程式，安裝最新版本。 tooget 說明的 PowerShell 命令，與範例中，輸入`get-help <command> -full`。
- 如果使用 Azure 命令列介面 (CLI) 命令 toocomplete 工作，在本文中[安裝及設定 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)。 確定您擁有 hello hello Azure CLI 安裝最新版本。 CLI 命令的 tooget 說明輸入`az <command> --help`。 而不是安裝 hello CLI 和其必要元件，您可以使用 hello Azure 雲端殼層。 hello Azure 雲端殼層是免費的 Bash 殼層，您可以直接在 hello Azure 入口網站中執行。 它有的 hello Azure CLI 預先安裝和設定 toouse 與您的帳戶。 toouse hello 雲端 Shell 中，按一下 hello 雲端殼層**> _**按鈕上方的 hello hello[入口網站](https://portal.azure.com)。

## <a name="create-a-network-interface"></a>建立網路介面

建立虛擬機器使用 hello Azure 入口網站時，hello 入口網站會建立使用預設設定為您的網路介面。 如果您而是會指定所有網路介面設定，您可以使用自訂設定建立網路介面，並附加 hello 網路介面 tooa 虛擬機器，建立 hello 虛擬機器 （使用 PowerShell 或 hello Azure CLI） 時。 您也可以建立網路介面，並將它加入 tooan 現有的虛擬機器 （使用 PowerShell 或 Azure CLI hello）。 toolearn toocreate 與現有的虛擬機器網路介面或 tooadd，或從現有的虛擬機器移除網路介面如何讀取 hello[新增或移除網路介面](virtual-network-network-interface-vm.md)發行項。 之前建立的網路介面，您必須擁有現有[虛擬網路](virtual-networks-create-vnet-arm-pportal.md)在 hello 相同位置和訂用帳戶建立中的網路介面。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)帳戶也就是指派 （至少） 角色的權限 hello 網路參與者訂用帳戶。 讀取 hello [Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)文章 toolearn 更多關於指派 tooaccounts 角色和權限。
2. 在 hello 方塊包含的 hello 文字*搜尋資源*hello hello Azure 入口網站頂端，在輸入*網路介面*。 當**網路介面**會出現在 hello 搜尋結果中，按一下它。
3. 在 hello**網路介面**刀鋒視窗中，按一下**+ 加**。
4. 在 hello**建立網路介面**刀鋒視窗中，輸入，或 hello 下列設定，針對選取的值，然後按一下**建立**:

    |設定|必要？|詳細資料|
    |---|---|---|
    |名稱|是|hello 名稱必須是唯一您選取的 hello 資源群組中。 在經過一段時間後，您的 Azure 訂用帳戶中可能會有好幾個網路介面。 讀取 hello[命名慣例](/azure/architecture/best-practices/naming-conventions?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions)發行項建立數個管理的命名慣例 toomake 時建議的網路介面更容易。 建立 hello 網路介面後，就無法變更 hello 名稱。|
    |虛擬網路|是|選取 hello hello 網路介面的虛擬網路。 您只能指派網路介面 tooa 虛擬網路中已有 hello 相同訂用帳戶和與 hello 網路介面的位置。 網路介面建立之後，您無法變更指派給 hello 虛擬網路。 hello 新增 hello 網路介面 toomust 虛擬機器也存在於 hello 相同位置和訂用帳戶為 hello 網路介面。|
    |子網路|是|選取您所選取的 hello 虛擬網路中的子網路。 您可以變更 hello 子網路指派給的 tooafter 建立 hello 網路介面。|
    |私人 IP 位址指派|是| 在此設定中，您選擇 hello IPv4 位址的 hello 分派方法。 選擇下列指派方法 hello:**動態：**選取此選項時，Azure 會自動將可用的位址指派從 hello hello 您選取的子網路位址空間。 Hello 虛擬機器仍在啟動之後機組 hello 停止 （取消配置） 的狀態時，azure 可能會指派不同的位址 tooa 網路介面。 如果沒有已經在 hello 停止 （取消配置） 的狀態，重新啟動 hello 虛擬機器 hello 位址會維持 hello 相同。 **靜態：**選取此選項時，您必須手動指派可用的 IP 位址從 hello hello 您選取的子網路位址空間中。 請勿變更靜態位址，直到您變更或刪除 hello 網路介面。 建立 hello 網路介面後，您可以變更 hello 分派方法。 hello Azure DHCP 伺服器會將此位址 toohello 網路介面的 hello 虛擬機器 hello 作業系統內。|
    |網路安全性群組|否| 保持設太**無**，選取現有[網路安全性群組](virtual-networks-nsg.md)，或[建立網路安全性群組](virtual-networks-create-nsg-arm-pportal.md)。 網路安全性群組可讓您 toofilter 網路流量進出網路介面。 您可以套用零個或一個網路安全性群組 tooa 網路介面。 也可以套用零個或一個網路安全性群組指派給 toohello 子網路 hello 網路介面。 網路安全性群組時套用的 tooa 網路介面和 hello 子網路 hello 網路介面被指派給，有時非預期的結果發生。 tootroubleshoot 網路安全性群組套用的 toonetwork 介面和子網路，讀取 hello[疑難排解網路安全性群組](virtual-network-nsg-troubleshoot-portal.md#nsg)發行項。|
    |訂用帳戶|是|選取其中一個 Azure [訂用帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription)。 hello 附加網路介面 tooand hello 虛擬網路連接的虛擬機器 toomust 存在於 hello 相同訂用帳戶。|
    |私人 IP 位址 (IPv6)|否| 如果您選取此核取方塊，IPv6 位址會指派的 toohello 網路介面，此外 toohello IPv4 位址指派 toohello 網路介面。 請參閱 hello [IPv6](#IPv6)本文的重要資訊使用的 IPv6 網路介面具有一節。 您無法選取 hello IPv6 位址的工作分派方法。 如果您選擇 tooassign IPv6 位址時，會將它指派與 hello 動態方法。
    |IPv6 名稱 (只有當 hello 會顯示**私人 IP 位址 (IPv6)**核取方塊) |是，如果 hello**私人 IP 位址 (IPv6)**核取方塊。| 這個名稱會指派 tooa hello 網路介面的次要 IP 設定。 深入了解 IP 組態中 hello[檢視網路介面設定](#view-network-interface-settings)本文一節。|
    |資源群組|是|選取現有的[資源群組](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group)，或建立一個群組。 網路介面可以存在於 hello 相同，或不同的資源群組，比 hello 虛擬機器，您將其附加至或使用 hello 虛擬網路連接它。|
    |位置|是|hello 附加網路介面 tooand hello 虛擬網路連接的虛擬機器 toomust 存在於 hello 相同[位置](https://azure.microsoft.com/regions)，也稱為 tooas 區域。|

hello 入口網站不會提供 hello 選項 tooassign 公用 IP 位址 toohello 網路介面建立時，雖然 hello 入口網站未建立公用 IP 位址，並將它指派 tooa 網路介面，當您建立虛擬機器使用 hello 入口網站。 toolearn tooadd 公用 IP 位址 toohello 網路介面，建立之後，如何讀取 hello[管理 IP 位址](virtual-network-network-interface-addresses.md)發行項。 如果您想 toocreate 公用 IP 位址的網路介面，您必須使用 hello CLI 或 PowerShell toocreate hello 網路的介面。

>[!Note]
> Azure 會指派 MAC 位址 toohello 網路介面 hello 網路介面是附加的 tooa 虛擬機器和 hello 虛擬機器時，才會啟動 hello 第一次。 您無法指定 hello Azure 將指派 toohello 網路介面的 MAC 位址。 hello MAC 位址會維持指派 toohello 網路介面，直到刪除為止 hello 網路介面或 hello 分派 toohello 主要 IP 設定 hello 主要網路介面的私用 IP 位址變更。 深入了解 IP 位址和 IP 設定，讀取 hello toolearn[管理 IP 位址](virtual-network-network-interface-addresses.md)發行項。

**命令**

|工具|命令|
|---|---|
|CLI|[az network nic create](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|

## <a name="view-network-interface-settings"></a>檢視網路介面設定

您可以在網路介面建立後變更其大部分的設定。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)帳戶也就是指派 （至少） 角色的權限 hello 網路參與者訂用帳戶。 讀取 hello [Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)文章 toolearn 更多關於指派 tooaccounts 角色和權限。
2. 在 hello 方塊包含的 hello 文字*搜尋資源*hello hello Azure 入口網站頂端，在輸入*網路介面*。 當**網路介面**會出現在 hello 搜尋結果中，按一下它。
3. 在 hello**網路介面**刀鋒視窗中，按一下您想要 tooview 或變更設定的 hello 的網路介面。
4. hello 下列設定詳列於 hello 刀鋒視窗，其中會顯示您選取的 hello 網路介面：
    - **概觀：**提供 hello 網路介面的相關資訊，例如 hello IP 位址指派 tooit、 hello 虛擬網路/子網路 hello 網路介面已指派給，並且附加太 hello 虛擬機器 hello 網路介面 （如果它是 tooone)。 hello 下圖顯示名為網路介面的 hello 概觀設定**mywebserver256**:![網路介面概觀](./media/virtual-network-network-interface/nic-overview.png)可以移動的網路介面 tooa 不同資源群組或按一下訂用帳戶 (**變更**) 下一步 toohello**資源群組**或**訂用帳戶名稱**。 如果您移動 hello 網路介面，您必須移動所有資源相關的 toohello 網路的介面。 如果 hello 網路介面附加的 tooa 虛擬機器，例如，您也必須移動 hello 虛擬機器和虛擬機器相關的其他資源。 toomove 網路介面，讀取 hello [tooa 新資源群組或訂用帳戶移動](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json#use-portal)發行項。 hello 文章列出先決條件及如何使用 toomove 資源 hello Azure 網站、 PowerShell 和 hello Azure CLI。
    - **IP 組態：**此處的公用和私用 IPv4 和 IPv6 位址指派 tooIP 組態。 如果 IPv6 位址被指派 tooan IP 組態，不會顯示 hello 位址。 深入了解 IP 組態以及如何 tooadd 並移除 IP 位址在 hello[設定 IP 位址的 Azure 網路介面](virtual-network-network-interface-addresses.md)發行項。 IP 轉送和子網路指派也會在這一節設定。 深入了解這些設定，讀取 hello toolearn[啟用或停用 IP 轉送](#enable-or-disable-ip-forwarding)和[變更子網路指派](#change-subnet-assignment)本文的小節。
    - **DNS 伺服器：**您可以指定哪一個 DNS 伺服器的網路介面由指派 hello Azure DHCP 伺服器。 hello 網路介面可以繼承 hello 設定 hello 從虛擬網路 hello 網路介面已指派給，或具有自訂設定，會覆寫指派給 hello 虛擬網路的 hello 設定。 toomodify 顯示的內容，完成 hello 步驟 hello[變更 DNS 伺服器](#change-dns-servers)本文一節。
    - **網路安全性群組 (NSG):** NSG 即會顯示相關聯 toohello 網路介面 （如果有的話）。 NSG 包含 hello 網路介面的輸入和輸出規則 toofilter 網路流量。 如果 NSG 相關聯的 toohello 網路介面，hello 的 hello 關聯的 NSG 會顯示的名稱。 toomodify 顯示的內容，完成 hello 步驟 hello[管理網路安全性的群組關聯](virtual-network-manage-nsg-arm-portal.md#manage-associations)發行項。
    - **屬性：**會顯示索引鍵相關 hello 網路介面，包括其 MAC 位址 （如果空白 hello 網路介面並非附加的 tooa 虛擬機器），設定及 hello 它存在於訂用帳戶。
    - **有效的安全性規則：**如果 hello 網路介面附加的 tooa 執行虛擬機器，而 NSG 相關聯的 toohello 網路介面、 hello 子網路指派，或兩者都列出安全性規則。 進一步了解顯示的內容，toolearn 讀取 hello[疑難排解網路安全性群組](virtual-network-nsg-troubleshoot-portal.md#nsg)發行項。 深入了解 Nsg，讀取 hello toolearn[網路安全性群組](virtual-networks-nsg.md)發行項。
    - **有效路由：**如果 hello 網路介面，則虛擬機器中執行的附加的 tooa 列出路由。 hello Azure 的預設路由，任何使用者定義的路由 (UDR)，以及可能存在 hello 子網路 hello 網路介面指派給任何 BGP 路由的組合為 hello 路由。 進一步了解顯示的內容，toolearn 讀取 hello[疑難排解路由](virtual-network-routes-troubleshoot-portal.md#view-effective-routes-for-a-network-interface)發行項。 深入了解 Azure 的預設值而且 UDRs，讀取 hello toolearn[使用者定義的路由](virtual-networks-udr-overview.md)發行項。
    - **一般的 Azure 資源管理員設定：** toolearn 深入了解一般 Azure 資源管理員設定，讀取 hello[活動記錄檔](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs)，[存取控制 (IAM)](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control)，[標記](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags)，[鎖定](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json)，和[自動化指令碼](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group)文件。

**命令**

如果 IPv6 位址被指派 tooa 網路介面，hello PowerShell 輸出會傳回 hello 事實 hello 位址指派，但是它不會傳回 hello 指派位址。 同樣地，CLI 會傳回 hello 事實的 hello 位址指派，但傳回的 hello *null*其輸出中的 hello 位址。

|工具|命令|
|---|---|
|CLI|[az 網路 nic 清單](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#list)tooview hello 訂用帳戶; 中的網路介面[az 網路 nic 顯示](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#show)tooview 設定網路介面|
|PowerShell|[Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) tooview hello 訂用帳戶或檢視設定的網路介面的網路介面|

## <a name="change-dns-servers"></a>變更 DNS 伺服器

hello DNS 伺服器是由 hello Azure DHCP server toohello 網路介面 hello 虛擬機器作業系統內指派。 指派的 hello DNS 伺服器是任何 hello DNS 伺服器設定網路介面。 請參閱深入了解網路介面，名稱解析設定 toolearn[虛擬機器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md)。 hello 網路介面可以繼承 hello 虛擬網路中的 hello 設定，或使用覆寫 hello hello 虛擬網路設定它自己唯一設定。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)帳戶也就是指派 （至少） 角色的權限 hello 網路參與者訂用帳戶。 讀取 hello [Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)文章 toolearn 更多關於指派 tooaccounts 角色和權限。
2. 在 hello 方塊包含的 hello 文字*搜尋資源*hello hello Azure 入口網站頂端，在輸入*網路介面*。 當**網路介面**會出現在 hello 搜尋結果中，按一下它。
3. 在 hello**網路介面**刀鋒視窗中，按一下您想要 tooview 或變更設定的 hello 的網路介面。
4. 在您選取的 hello 網路介面的 hello 刀鋒視窗，按一下**DNS 伺服器**下**設定**。
5. 按一下：
    - **虛擬網路 （預設值） 會繼承**： 選擇這個選項 tooinherit hello DNS 伺服器設定中定義的指派給 hello 虛擬網路 hello 網路介面。 在 hello 虛擬網路層級，被定義的自訂 DNS 伺服器 」 或 「 hello Azure 提供的 DNS 伺服器。 hello Azure 提供的 DNS 伺服器可解析主機名稱指派資源 toohello 相同虛擬網路。 FQDN 必須是使用的 tooresolve 指派 toodifferent 虛擬網路的資源。
    - **自訂**： 您可以為遍及多個虛擬網路設定您自己的 DNS 伺服器 tooresolve 名稱。 輸入 hello IP 位址的 hello server 想 toouse 做為 DNS 伺服器。 只有 toothis 網路介面和覆寫 hello 虛擬網路 hello 網路介面的任何 DNS 設定指派給指派 hello 您指定的 DNS 伺服器位址。
6. 按一下 [儲存] 。

**命令**

|工具|命令|
|---|---|
|CLI|[az network nic update](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="enable-or-disable-ip-forwarding"></a>啟用或停用 IP 轉送

IP 轉送可讓 hello 虛擬機器網路介面連接到：
- 收到不針對其中一個 hello IP 位址指派 tooany hello 分派 toohello 網路介面的 IP 組態的網路流量。
- 傳送使用不同的來源 IP 位址，比 hello 一個指派的 tooone 的網路介面的 IP 組態的網路流量。

必須對每個附加的 toohello 收到 hello 虛擬機器需求 tooforward 的流量的虛擬機器的網路介面啟用 hello 設定。 不論有多個網路介面或單一網路介面附加 tooit，虛擬機器可以轉送流量。 Azure 設定 IP 轉送時，hello 虛擬機器也必須執行的應用程式可以 tooforward hello 流量，例如防火牆、 WAN 最佳化，以及負載平衡應用程式。 當網路應用程式時，會執行虛擬機器時，hello 虛擬機器通常會參考的 tooas 網路的虛擬設備。 您可以檢視準備 toodeploy 網路虛擬裝置的清單中 hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances)。 IP 轉送通常使用於使用者定義的路由。 更多關於使用者定義的路由，讀取 hello toolearn[使用者定義的路由](virtual-networks-udr-overview.md)發行項。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)帳戶也就是指派 （至少） 角色的權限 hello 網路參與者訂用帳戶。 讀取 hello [Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)文章 toolearn 更多關於指派 tooaccounts 角色和權限。
2. 在 hello 方塊包含的 hello 文字*搜尋資源*hello hello Azure 入口網站頂端，在輸入*網路介面*。 當**網路介面**會出現在 hello 搜尋結果中，按一下它。
3. 在 hello**網路介面**刀鋒視窗中，按一下您想要 tooenable 或停用的轉送 IP，hello 網路介面。
4. 在您選取的 hello 網路介面的 hello 刀鋒視窗，按一下**IP 組態**在 hello**設定**> 一節。
5. 按一下**啟用**或**已停用**（預設值） toochange hello 設定。
6. 按一下 [儲存] 。

**命令**

|工具|命令|
|---|---|
|CLI|[az network nic update](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet-assignment"></a>變更子網路指派

您可以變更 hello 的子網路，但不要 hello 虛擬網路中，指派給網路介面。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)帳戶也就是指派 （至少） 角色的權限 hello 網路參與者訂用帳戶。 讀取 hello [Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)文章 toolearn 更多關於指派 tooaccounts 角色和權限。
2. 在 hello 方塊包含的 hello 文字*搜尋資源*hello hello Azure 入口網站頂端，在輸入*網路介面*。 當**網路介面**會出現在 hello 搜尋結果中，按一下它。
3. 在 hello**網路介面**刀鋒視窗中，按一下您想要 tooview 或變更設定的 hello 的網路介面。
4. 按一下**IP 組態**下**設定**hello 您選取的網路介面的 hello 刀鋒視窗中。 如果有任何 IP 組態的任何私用 IP 位址列**（靜態）**下一步 toothem，您必須變更 hello IP 位址指派方法 toodynamic 完成 hello 遵循的步驟。 必須將所有私人 IP 位址指派 hello 動態指派方法 toochange hello 子網路指派 hello 網路介面。 如果 hello 位址指派與 hello 動態方法時，繼續 toostep 五個。 如果任何 IPv4 位址指派與 hello 靜態指派方法，完成下列步驟 toochange hello 分派方法 toodynamic hello:
    - 按一下您想 toochange hello IPv4 位址指派方法 hello 清單中的 IP 組態的 hello IP 設定。
    - 在 hello 刀鋒視窗中顯示 hello IP 組態，按一下 **動態**hello**指派**方法。 您無法指定 IPv6 位址與 hello 靜態指派方法。
    - 按一下 [儲存] 。
5. 選取您想要 tooconnect hello 網路介面 toofrom hello hello 子網路**子網路**下拉式清單。
6. 按一下 [儲存] 。 新的動態位址會指派 hello hello 新子網路的子網路位址範圍內。 指派之後 hello 介面 tooa 新子網路，您可以從 hello 新的子網路位址範圍指派靜態 IPv4 位址，如果您選擇。 更多關於加入、 變更和移除 IP 位址的網路介面，讀取 hello toolearn[管理 IP 位址](virtual-network-network-interface-addresses.md)發行項。

**命令**

|工具|命令|
|---|---|
|CLI|[az network nic ip-config update](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-a-network-interface"></a>刪除網路介面

只要不是附加的 tooa 虛擬機器，您可以刪除網路介面。 如果是附加的 tooa 虛擬機器，都必須第一個位置 hello 虛擬機器在 hello 停止 （取消配置） 狀態，再卸離 hello hello 虛擬機器的網路介面，才能刪除 hello 網路介面。 toodetach 從虛擬機器的網路介面，hello 步驟完成 hello[卸離虛擬機器從一個網路介面](virtual-network-network-interface-vm.md#vm-remove-nic)區段 hello[新增或移除網路介面](virtual-network-network-interface-vm.md)發行項。 正在刪除虛擬機器卸離所有網路介面附加的 tooit，但不會刪除 hello 網路介面。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)帳戶也就是指派 （至少） 角色的權限 hello 網路參與者訂用帳戶。 讀取 hello [Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)文章 toolearn 更多關於指派 tooaccounts 角色和權限。
2. 在 hello 方塊包含的 hello 文字*搜尋資源*hello hello Azure 入口網站頂端，在輸入*網路介面*。 當**網路介面**會出現在 hello 搜尋結果中，按一下它。
3. 以滑鼠右鍵按一下 hello 網路介面要 toodelete**刪除**。
4. 按一下**是**tooconfirm 刪除 hello 網路介面。

當您刪除的網路介面，任何 MAC 或 IP 位址指派 tooit 會發行。

**命令**

|工具|命令|
|---|---|
|CLI|[az network nic delete](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmNetworkInterface](/powershell/module/azurerm.network/remove-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>後續步驟
toocreate 虛擬機器具有多個網路介面或 IP 位址，請閱讀下列發行項的 hello:

**命令**

|Task|工具|
|---|---|
|建立具有多個 NIC 的 VM|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)、[PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|建立具有多個 IPv4 位址的單一 NIC VM|[CLI](virtual-network-multiple-ip-addresses-cli.md)、[PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|建立具有私人 IPv6 位址的單一 NIC VM (在 Azure Load Balancer 後端)|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json)、[PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json)、[Azure Resource Manager 範本](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
