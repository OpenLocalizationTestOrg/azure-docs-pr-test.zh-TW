---
title: "IPv6-Azure 範本與 aaaDeploy 網際網路對向負載平衡器 |Microsoft 文件"
description: "如何 toodeploy IPv6 支援 Azure 負載平衡器和負載平衡的 Vm。"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
keywords: "ipv6, azure load balancer, 雙重堆疊, 公用 ip, 原生 ipv6, 行動, iot"
ms.assetid: 2998e943-13fc-4ea9-a68c-875e53a08db3
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2016
ms.author: kumud
ms.openlocfilehash: 68b9ba874a50161243577b64c4a6d9c76b39156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-internet-facing-load-balancer-solution-with-ipv6-using-a-template"></a>使用範本部署配置有 IPv6 的網際網路面向負載平衡器解決方案

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [Azure CLI](load-balancer-ipv6-internet-cli.md)
> * [範本](load-balancer-ipv6-internet-template.md)

Azure 負載平衡器是第 4 層 (TCP、UDP) 負載平衡器。 hello 負載平衡器連入流量的各項雲端服務中的狀況良好的服務執行個體或虛擬機器中負載平衡器集可提供高可用性。 Azure Load Balancer 也會在多個連接埠、多個 IP 位址或兩者上顯示這些服務。

## <a name="example-deployment-scenario"></a>範例部署案例

hello 下列圖表說明 hello 負載平衡解決方案使用本文中所述的 hello 範例範本部署。

![負載平衡器案例](./media/load-balancer-ipv6-internet-template/lb-ipv6-scenario.png)

在此案例中，您將建立下列 Azure 資源的 hello:

* 虛擬網路介面，用於每個已指派 IPv4 和 IPv6 位址的 VM
* 配置有 IPv4 和 IPv6 公用 IP 位址的網際網路面向負載平衡器
* 兩個負載平衡規則 toomap hello 公用 Vip toohello 私用端點
* 可用性設定組，其中包含 hello 兩個 Vm
* 兩部虛擬機器 (VM)

## <a name="deploying-hello-template-using-hello-azure-portal"></a>部署的 hello 範本使用 hello Azure 入口網站

這份文件參考範本發佈在 hello [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/201-load-balancer-ipv6-create/)組件庫。 您可以從 hello gallery 下載 hello 範本，或啟動直接從 hello 組件庫的 Azure 中的 hello 部署。 本文假設您已下載 hello 範本 tooyour 本機電腦。

1. 開啟 hello Azure 入口網站，並有權限 toocreate Vm 和 Azure 訂用帳戶內的網路功能資源的帳戶登入。 此外，除非您使用現有的資源，hello 帳戶需要權限 toocreate 資源群組和儲存體帳戶。
2. 按一下 [+ 新增] 從 hello 功能表，然後輸入 hello [搜尋] 方塊中，「 範本 」。 從 hello 搜尋結果中選取 「 範本部署 」。

    ![lb-ipv6-portal-step2](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step2.png)

3. 中的所有項目 hello 刀鋒視窗中，按一下 [部署範本]。

    ![lb-ipv6-portal-step3](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step3.png)

4. 按一下 [建立]。

    ![lb-ipv6-portal-step4](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step4.png)

5. 按一下 [編輯範本]。 刪除 hello 現有內容和複製/貼上在 hello hello 範本檔案的整個內容 （tooinclude hello 開始和結束 {}），然後按一下 [儲存]。

    > [!NOTE]
    > 如果您使用 Microsoft Internet Explorer 中，當您貼上您會看到對話方塊，詢問您 tooallow 存取 toohello Windows 剪貼簿。 按一下 [允許存取]。

    ![lb-ipv6-portal-step5](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step5.png)

6. 按一下 [編輯參數]。 Hello 參數刀鋒視窗中，在指定 hello 指引 hello 值在 hello 範本參數 區段中，然後按一下 儲存 tooclose hello 參數刀鋒視窗。 在 hello 自訂部署刀鋒視窗中，選取您的訂用帳戶中，而現有的資源群組，或建立一個。 如果您要建立資源群組，然後選取 hello 資源群組的位置。 接下來，按一下**法律條款**，然後按一下 **購買**hello 法律條款。 Azure 會開始部署 hello 資源。 花幾分鐘的時間 toodeploy hello 的所有資源。

    ![lb-ipv6-portal-step6](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step6.png)

    如需有關這些參數的詳細資訊，請參閱 hello[範本參數和變數](#template-parameters-and-variables)本文中稍後的章節。

7. hello 範本所建立的 toosee hello 資源按一下 瀏覽、 hello 清單中向下捲動，直到您看到 「 資源群組 」，然後按一下它。

    ![lb-ipv6-portal-step7](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step7.png)

8. 在 hello 資源群組刀鋒視窗中，按一下 hello hello 您在步驟 6 中指定的資源群組名稱。 您會看到所有已部署的 hello 資源的清單。 如果一切順利，[上次部署] 下應該會顯示 [成功]。 如果沒有，請確定您使用的 hello 帳戶具有權限 toocreate hello 所需的資源。

    ![lb-ipv6-portal-step8](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step8.png)

    > [!NOTE]
    > 完成步驟 6 之後立即瀏覽您的資源群組，如果 「 最後一個部署 」 會顯示 hello 「 部署 」 狀態，而部署 hello 資源時。

9. 按一下 「 myIPv6PublicIP"hello 資源清單中。 您會看到確認它有下 IP 位址，IPv6 位址，且其 DNS 名稱是您在步驟 6 中的 hello dnsNameforIPv6LbIP 參數所指定的 hello 值。 此資源是 hello 公用 IPv6 位址和主機名稱是可存取的 tooInternet 用戶端。

    ![lb-ipv6-portal-step9](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step9.png)

## <a name="validate-connectivity"></a>驗證連線能力

已成功部署 hello 範本，您可以藉由完成下列工作的 hello 驗證連線：

1. 登入 toohello Azure 入口網站，並連接 tooeach 的 hello hello 範本部署所建立的 Vm。 如果您部署的是 Windows Server VM，請從命令提示字元執行 ipconfig /all。 您會看到 hello Vm 有 IPv4 和 IPv6 位址。 如果您已部署 Linux Vm，您需要 tooconfigure hello Linux 作業系統 tooreceive 動態 IPv6 位址使用 hello 指示提供給您的 Linux 散發套件。
2. 從連線到 IPv6 網際網路的用戶端起始連線 toohello 公用 IPv6 位址的 hello 負載平衡器。 hello 負載平衡器的 tooconfirm hello 兩個 Vm 間的負載平衡，您可以在每個 hello Vm 上安裝網頁伺服器像 Microsoft 網際網路資訊服務 (IIS)。 每部伺服器上的 hello 預設 web 網頁可能包含 hello 文字"Server0"或者"Server1"toouniquely 識別。 然後，開啟網際網路瀏覽器上 IPv6 網際網路連線的用戶端，並瀏覽 toohello 您 hello 負載平衡器 tooconfirm 端對端 IPv6 連線能力 tooeach VM hello dnsNameforIPv6LbIP 參數所指定的主機名稱。 如果您只看到 hello 網頁，只有一部伺服器時，您可能需要 tooclear 您的瀏覽器快取。 開啟多個私人瀏覽工作階段。 您應該會看來自每部伺服器的回應。
3. 從連線到 IPv4 網際網路的用戶端起始連線 toohello 公用 IPv4 位址的 hello 負載平衡器。 hello 負載平衡器的 tooconfirm 是負載平衡 hello 兩個 Vm，您可以測試使用 IIS，步驟 2 中所述。
4. 從每個 VM，起始的輸出連線 tooan IPv6 或 IPv4 連線網際網路的裝置。 在這兩種情況下，看到 hello 目的地裝置 hello 來源 IP 是 hello 公用 IPv4 或 IPv6 位址 hello 負載平衡器。

> [!NOTE]
> IPv4 和 IPv6 的 ICMP 已封鎖在 hello Azure 網路。 因此，像 ping 這類的 ICMP 工具一定會失敗。 tootest 連線使用的 TCP 替代方案，例如 TCPing 或 hello PowerShell 測試 NetConnection cmdlet。 請注意，hello hello 圖表中顯示的 IP 位址的值，您可能會看到的範例。 由於 hello IPv6 位址動態指派，您收到 hello 位址會略有不同，而且可能會因區域。 此外，很常見的 hello 公用 IPv6 位址上與不同的前置詞的 hello 負載平衡器 toostart 比 hello hello 後端集區中的私用 IPv6 位址。

## <a name="template-parameters-and-variables"></a>範本參數和變數

Azure Resource Manager 範本包含多個變數和參數，您可以自訂 tooyour 需求。 您不想使用者 toochange 固定的值會使用變數。 參數值會使用部署 hello 範本時，想要使用者 tooprovide。 這篇文章中所述的 hello 案例設定 hello 範例範本。 您可以自訂此 tooneeds 您的環境。

在本文中使用的範本包含下列 hello hello 範例變數和參數：

| 參數 / 變數 | 注意事項 |
| --- | --- |
| adminUsername |指定使用 toosign toohello 搭配虛擬機器 hello hello 系統管理員帳戶名稱。 |
| adminPassword |指定 hello hello 系統管理員帳戶的密碼使用 toosign toohello 搭配虛擬機器。 |
| dnsNameforIPv4LbIP |指定要作為 hello 公用 hello 負載平衡器名稱 tooassign hello DNS 主機名稱。 這個名稱會解析 toohello 負載平衡器的公用 IPv4 位址。 hello 名稱必須是小寫，並且與 hello regex: ^ [a-z][a-z0-9-]{1,61}[a-z0-9]$。 |
| dnsNameforIPv6LbIP |指定要作為 hello 公用 hello 負載平衡器名稱 tooassign hello DNS 主機名稱。 這個名稱會解析 toohello 負載平衡器的公用 IPv6 位址。 hello 名稱必須是小寫，並且與 hello regex: ^ [a-z][a-z0-9-]{1,61}[a-z0-9]$。 這可以是 hello 相同的名稱，如 hello IPv4 位址。 當用戶端傳送 Azure 此名稱的 DNS 查詢將會退回 hello A 和 AAAA 記錄會共用 hello 名稱。 |
| vmNamePrefix |指定 hello VM 名稱前置詞。 hello 範本會附加一個數字 (0、 1、 等等) 建立 Vm 時 hello toohello 名稱。 |
| nicNamePrefix |指定 hello 網路介面名稱前置詞。 hello 範本會附加一個數字 (0、 1、 等等) toohello hello 網路介面建立時的名稱。 |
| storageAccountName |輸入 hello 現有的儲存體帳戶名稱，或指定 hello 範本所建立的新一個 toobe hello 名稱。 |
| availabilitySetName |輸入然後之 hello 可用性集合名稱 toobe hello Vm 搭配使用 |
| addressPrefix |使用虛擬網路 hello toodefine hello 位址範圍 hello 位址前置詞。 |
| subnetName |hello VNet 建立 hello 子網路中的 hello 名稱 |
| subnetPrefix |使用 toodefine hello 位址範圍 hello 子網路的 hello 位址前置詞。 |
| vnetName |指定 hello hello VNet hello Vm 所使用的名稱。 |
| ipv4PrivateIPAddressType |hello 配置方法，用於 hello 私用 IP 位址 （靜態或動態） |
| ipv6PrivateIPAddressType |hello 分派方法用於 hello 私用 IP 位址 （動態）。 IPv6 只支援 Dynamic (動態) 配置。 |
| numberOfInstances |hello 數目負載平衡 hello 範本所部署的執行個體 |
| ipv4PublicIPAddressName |指定您想要利用 hello 公用 IPv4 位址 hello 負載平衡器 toouse toocommunicate hello DNS 名稱。 |
| ipv4PublicIPAddressType |hello 配置方法，用於 hello 公用 IP 位址 （靜態或動態） |
| Ipv6PublicIPAddressName |指定您想要的 hello 負載平衡器 hello 公用 IPv6 位址 toouse toocommunicate hello DNS 名稱。 |
| ipv6PublicIPAddressType |hello hello 公用 IP 位址 （動態） 所使用的配置方法。 IPv6 只支援 Dynamic (動態) 配置。 |
| lbName |指定 hello hello 負載平衡器名稱。 這個名稱是顯示在 hello 入口網站，或使用參考 tooit 使用 CLI 或 PowerShell 命令時。 |

hello 範本中的 hello 剩餘變數包含 Azure 建立 hello 資源時指派的衍生的值。 請勿變更這些變數。
