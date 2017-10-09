---
title: "範例-aaaDMZ 建置 DMZ tooprotect 防火牆與 Nsg 的應用程式 |Microsoft 文件"
description: "建置具有防火牆和網路安全性群組 (NSG) 的 DMZ"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: c78491c7-54ac-4469-851c-b35bfed0f528
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: 18f116dc3897567bff14a509ae8c13f449182bfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="example-2--build-a-dmz-tooprotect-applications-with-a-firewall-and-nsgs"></a>範例 2 – 建立 DMZ tooprotect 防火牆與 Nsg 的應用程式
[傳回 toohello 安全性界限最佳作法頁面][HOME]

此範例會建立 DMZ，其內含防火牆、四個 Windows 伺服器和網路安全性群組。 它也將會逐步每 hello 相關命令 tooprovide 更深入的了解每個步驟。 另外還有流量案例 > 一節 tooprovide 的深入了解逐步如何流量就會繼續進行 hello 層級的防禦 hello 周邊網路。 最後，在 hello references 區段中是 hello 完整程式碼和指示 toobuild 此環境 tootest 和試驗各種案例。 

![輸入 DMZ NVA 與 NSG][1]

## <a name="environment-description"></a>環境描述
在此範例中沒有包含 hello 下列訂用帳戶：

* 兩個雲端服務：“FrontEnd001” 和 “BackEnd001”
* 一個虛擬網路 “CorpNetwork”，包含兩個子網路：“FrontEnd” 和 “BackEnd”
* 套用的 tooboth 子網路的單一網路安全性群組
* 網路的虛擬設備，在此範例中 Barracuda NextGen 防火牆連線 toohello Frontend 子網路
* 一個代表應用程式 Web 伺服器的 Windows Server (“IIS01”)
* 兩個代表應用程式後端伺服器的 Windows Server (“AppVM01”、“AppVM02”)
* 一個代表 DNS 伺服器的 Windows Server ("DNS01")

> [!NOTE]
> 雖然這個範例會使用許多不同的網路虛擬裝置無法使用此範例中的 hello Barracuda NextGen 防火牆。
> 
> 

在下面 hello references 區段中沒有將建置大部分 hello 環境上面所述的 PowerShell 指令碼。 建置 hello Vm 和虛擬網路，由 hello 範例指令碼，雖然不詳述於本文件說明。

toobuild hello 環境：

1. 儲存 hello 網路組態 xml 檔案包含在 hello 參考一節 （名稱、 位置和 IP 位址 toomatch hello 指定案例與更新）
2. Hello 指令碼 toomatch hello 環境 hello 指令碼中的更新 hello 使用者變數是 toobe 執行 （訂用帳戶、 服務名稱等等）
3. 在 PowerShell 中執行 hello 指令碼

**請注意**： 表示 hello PowerShell 指令碼中的 hello 區域必須符合表示 hello 網路組態 xml 檔中的 hello 區域。

Hello 指令碼順利執行之後可能會進入 hello 後指令碼的步驟：

1. 設定 hello 防火牆規則，這會涵蓋 hello 下面的一節中： 防火牆規則。
2. （選擇性） 在 hello references 區段中是兩個指令碼 tooset hello web 伺服器和應用程式伺服器，以測試此 DMZ 設定簡單的 web 應用程式 tooallow。

hello 下一節說明大部分的 hello 指令碼陳述式相對 tooNetwork 安全性群組。

## <a name="network-security-groups-nsg"></a>網路安全性群組 (NSG)
此範例會建置 NSG 群組，然後在其中載入六個規則。 

> [!TIP]
> 一般而言，您應該先建立特定的 「 允許 」 規則，然後上次 hello 一般 「 拒絕 」 規則。 指派優先順序的 hello 規定哪些規則會先評估。 一旦流量找到 tooapply tooa 特定規則，則會不評估任何進一步的規則。 NSG 規則可套用在 hello 中輸入或輸出方向 （從 hello 觀點 hello 子網路）。
> 
> 

以宣告方式，下列規則的 hello 正在建置輸入流量：

1. 允許內部 DNS 流量 (連接埠 53)
2. 允許從 hello 網際網路 tooany VM 的 RDP 流量 （連接埠 3389）
3. 允許從 hello 網際網路 toohello NVA （防火牆） 的 HTTP 流量 （連接埠 80）
4. 允許從 IIS01 tooAppVM1 任何流量 （所有連接埠）
5. 任何流量 （所有連接埠），從 hello 網際網路 toohello 拒絕整個 VNet （這兩個子網路）
6. 拒絕任何從 hello Frontend 子網路 toohello 後端子網路的流量 （所有連接埠）

與這些規則繫結的 tooeach 子網路中，輸入 hello Internet toohello 網頁伺服器從 HTTP 要求是否兩者的規則 3 （允許） 及 5 （拒絕） 將會套用，但由於規則 3 具有較高的優先順序，只將套用的規則 5 就不會發生。 因此 hello HTTP 要求會允許 toohello 防火牆。 如果該相同流量已嘗試 tooreach hello DNS01 伺服器，hello 第一個 tooapply 和 hello 流量就不會允許 toopass toohello 伺服器是規則 5 （拒絕）。 規則 6 (Deny) 區塊 hello Frontend 子網路從交談 toohello 後端的子網路 （除了規則 1 和 4 中允許的流量），如此可保護 hello 後端 」 網路，以防 hello 攻擊者會有攻擊者竊取 hello web 應用程式在 hello 前端上，限制的存取 toohello 後端 「 受保護 」 (只公開 hello AppVM01 伺服器上的 tooresources) 網路。

沒有預設輸出的規則，可讓流量輸出 toohello 網際網路。 在此範例中，我們會允許輸出流量，並不會修改任何輸出規則。 toolock 下兩個方向的流量，使用者定義的路由時，這會探索在 hello 中可以找到不同範例[主要安全性界限文件][HOME]。

hello 上面所討論的 NSG 規則是非常類似 toohello NSG 規則中的[範例 1： 建立簡單的周邊網路與 Nsg][Example1]。 請先檢閱該文件的詳細說明每個 NSG 規則和它的屬性中的 hello NSG 描述。

## <a name="firewall-rules"></a>防火牆規則
管理用戶端將會需要 toobe PC toomanage hello 防火牆上安裝，並建立所需的 hello 組態。 Toomanage hello 裝置的方式，請參閱 hello 文件從您的防火牆 （或其他 NVA） 廠商。 hello 本節其餘部分將說明 hello 透過 hello 廠商管理用戶端 （也就不是 hello Azure 入口網站或 PowerShell） 本身，hello 防火牆設定。

用戶端下載及連接 toohello Barracuda 用在此範例中的指示可在這裡找到： [Barracuda NG 系統管理員](https://techlib.barracuda.com/NG61/NGAdmin)

Hello 防火牆上轉送規則需要 toobe 建立。 由於這個範例只會在繫結 toohello 防火牆的網際網路流量，然後 toohello web 伺服器，因此也需要只能有一個轉送 NAT 規則。 在 hello 用於此範例 hello Barracuda NextGen 防火牆規則，是目的地 NAT 規則 (「 Dst NAT 」) toopass 這個流量。

toocreate hello 下列規則 （或確認現有的預設規則），從 hello Barracuda NG 管理用戶端儀表板開始，瀏覽 toohello 設定 索引標籤、 在 hello 操作設定 區段按一下 規則集。 方格呼叫時，「 主要規則 」 會顯示 hello 現有 hello 防火牆上的作用中和已停用規則。 Hello 右上角的此方格是很小，綠色"+"按鈕，再按一下這個 toocreate 新的規則 (請注意： 您的防火牆可能 「 鎖定 」 的變更，如果您看到按鈕標示 「 鎖定 」，而且您會無法 toocreate 或編輯規則，請按一下此按鈕太 「 解除鎖定 」 hello規則集，並允許編輯)。 如果您想 tooedit 現有的規則，就會選取該規則、 以滑鼠右鍵按一下並選取 編輯規則。

建立新規則並提供名稱，例如 "WebTraffic"。 

hello 目的地 NAT 規則的圖示看起來像這樣：![目的地 NAT 圖示][2]

hello 規則本身看起來可能像這樣：

![防火牆規則][3]

以下任何輸入的位址，叫用 hello 防火牆嘗試 tooreach HTTP （連接埠 80 或 443 用於 HTTPS） 傳送 hello 防火牆的 [DHCP1 本機 IP] 介面和重新導向的 toohello hello 10.0.1.5 IP 位址與 Web 伺服器。 因為 hello 流量的未來動態連接埠 80 和連接埠 80 上的持續 toohello web 伺服器上所不需進行任何連接埠變更。 不過，目標清單中可能有 10.0.1.5:8080 如果我們的 Web 伺服器會接聽連接埠 8080 因此轉譯的 hello hello 輸入連接埠 80 上 hello 防火牆 tooinbound 連接埠 8080 hello web 伺服器上。

連線方法應該也被表示，hello 目的地規則 hello 網際網路，從 「 動態 SNAT"，則最適合。 

雖然只建立了一個規則，但請務必正確設定其優先順序。 如果在 hello 方格 hello 防火牆上的所有規則的這個新規則 hello 下方 （如下 hello"BLOCKALL 」 規則） 它將永遠不會進入播放。 確定網路流量的 hello 新建立的規則值高於 hello BLOCKALL 規則。

一旦建立 hello 規則之後，就必須進行推入 toohello 防火牆，然後啟動，如果這不是 hello 規則變更不會生效。 hello 推播和啟動處理程序是 hello 下一節中所述。

## <a name="rule-activation"></a>啟用規則
以 hello ruleset 修改 tooadd 這項規則，hello ruleset 必須上傳 toohello 防火牆並啟動。

![防火牆規則啟用][4]

在 hello 右上角的 hello 管理用戶端都是叢集的按鈕。 按一下 hello 傳送變更 按鈕 toosend hello 修改規則 toohello 防火牆，然後按一下 hello 「 啟用 」 按鈕。

與 hello 啟用 hello 防火牆規則集的範例環境的這個組建已完成。 （選擇性） hello post 組建指令碼在 hello 參考區段可以是執行 tooadd 應用程式 toothis 環境 tootest hello 下方流量的情況。

> [!IMPORTANT]
> 您不會直接達到 hello web 伺服器的重要 toorealize 它。 當瀏覽器要求 HTTP 頁面從 FrontEnd001.CloudApp.Net 時，此防火牆的流量 toohello 不 hello hello HTTP 端點 （連接埠 80） 傳遞網頁伺服器。 hello 防火牆，然後根據 toohello 規則建立要求 toohello Web 伺服器的 Nat 上方。
> 
> 

## <a name="traffic-scenarios"></a>流量案例
#### <a name="allowed-web-tooweb-server-through-firewall"></a>（允許）Web tooWeb 通過防火牆的伺服器
1. 網際網路使用者從 FrontEnd001.CloudApp.Net (網際網路面向雲端服務) 要求 HTTP 頁面
2. 雲端服務將流量透過開啟連接埠 80 上 10.0.1.4:80 toofirewall 本機介面上的端點
3. Frontend 子網路開始處理輸入規則：
   1. NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則
   2. NSG 規則 2 」 (RDP) 不會套用移動 toonext 規則
   3. NSG 規則 3 (網際網路 tooFirewall) 會套用，流量會允許中停止的規則處理
4. 流量達到 hello 防火牆 (10.0.1.4) 的內部 IP 位址
5. 這是連接埠 80 的流量，請將其重新導向 toohello IIS01 的 web 伺服器，請參閱 < 防火牆轉寄規則
6. IIS01 接聽 web 流量、 收到此要求，並開始處理 hello 要求
7. IIS01 詢問 hello SQL Server 上 AppVM01 資訊
8. Frontend 子網路上沒有輸出規則，允許流量
9. hello 後端子網路會開始處理輸入的規則：
   1. NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則
   2. NSG 規則 2 」 (RDP) 不會套用移動 toonext 規則
   3. NSG 規則 3 (網際網路 tooFirewall) 不會套用移動 toonext 規則
   4. NSG 規則 4 (IIS01 tooAppVM01) 會套用，流量會允許中停止的規則處理
10. AppVM01 收到 hello SQL 查詢並予以回應
11. 因為允許在後端子網路 hello 回應 hello 沒有輸出規則
12. Frontend 子網路開始處理輸入規則：
    1. 套用 tooInbound 流量 hello 後端子網路 toohello Frontend 子網路，因此沒有任何 hello NSG 規則適用於沒有 NSG 規則
    2. hello 允許子網路之間流量的預設系統規則會允許這個流量，因此允許 hello 流量。
13. hello IIS 伺服器收到 hello SQL 回應，並完成 hello HTTP 回應，並將傳送 toohello 要求者
14. 由於這是 hello 防火牆 NAT 工作階段，hello 回應目的地 （一開始） 為 hello 防火牆
15. hello 防火牆收到 hello 回應 hello Web 伺服器，並將轉送後 toohello 網際網路使用者
16. 由於有前端子網路 hello 回應 hello 上的沒有輸出規則，而且 hello 網際網路使用者會收到要求的 hello 網頁。

#### <a name="allowed-rdp-toobackend"></a>（允許）RDP tooBackend
1. 網際網路上的伺服器系統管理員要求的 BackEnd001.CloudApp.Net:xxxxx 其中 xxxxx 是 RDP tooAppVM01 hello 隨機指派通訊埠編號上的 RDP 工作階段 tooAppVM01 （hello Azure 入口網站上或透過 PowerShell，可以找到 hello 指派連接埠）
2. Hello 防火牆只接聽 hello FrontEnd001.CloudApp.Net 位址，因為它並未包含與此流量
3. Backend 子網路開始處理輸入規則：
   1. NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則
   2. NSG 規則 2 (RDP) 適用，允許流量，停止處理規則
4. 由於沒有輸出規則，會套用預設規則並允許傳回的流量
5. 已啟用 RDP 工作階段
6. AppVM01 會提示輸入使用者名稱和密碼

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a>(允許) DNS 伺服器上的 Web 伺服器 DNS 查閱
1. Web 伺服器，IIS01，需要的資料摘要在 www.data.gov，但需要 tooresolve hello 位址。
2. hello 的網路組態 hello VNet 清單 DNS01 (10.0.2.4 hello 後端子網路上) 做為主要 DNS 伺服器 hello，IIS01 傳送 hello DNS 要求 tooDNS01
3. Frontend 子網路上沒有輸出規則，允許流量
4. Backend 子網路開始處理輸入規則：
   1. NSG 規則 1 (DNS) 適用，允許流量，停止處理規則
5. DNS 伺服器收到 hello 要求
6. DNS 伺服器沒有快取的 hello 位址和要求的根 DNS 伺服器上 hello 網際網路
7. Backend 子網路上沒有輸出規則，允許流量
8. 網際網路 DNS 伺服器回應，因為此工作階段已在內部起始，hello 允許回應
9. DNS 伺服器快取 hello 回應及回應 toohello 初始要求後 tooIIS01
10. Backend 子網路上沒有輸出規則，允許流量
11. Frontend 子網路開始處理輸入規則：
    1. 套用 tooInbound 流量 hello 後端子網路 toohello Frontend 子網路，因此沒有任何 hello NSG 規則適用於沒有 NSG 規則
    2. hello 允許子網路之間流量的預設系統規則會允許這個流量，因此允許 hello 流量
12. IIS01 DNS01 收到 hello 回應

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(允許) Web 伺服器存取 AppVM01 上的檔案
1. IIS01 要求 AppVM01 上的檔案
2. Frontend 子網路上沒有輸出規則，允許流量
3. hello 後端子網路會開始處理輸入的規則：
   1. NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則
   2. NSG 規則 2 」 (RDP) 不會套用移動 toonext 規則
   3. NSG 規則 3 (網際網路 tooFirewall) 不會套用移動 toonext 規則
   4. NSG 規則 4 (IIS01 tooAppVM01) 會套用，流量會允許中停止的規則處理
4. AppVM01 收到 hello 要求和回應檔案 （假設已獲授權存取）
5. 因為允許在後端子網路 hello 回應 hello 沒有輸出規則
6. Frontend 子網路開始處理輸入規則：
   1. 套用 tooInbound 流量 hello 後端子網路 toohello Frontend 子網路，因此沒有任何 hello NSG 規則適用於沒有 NSG 規則
   2. hello 允許子網路之間流量的預設系統規則會允許這個流量，因此允許 hello 流量。
7. hello IIS 伺服器收到 hello 檔案

#### <a name="denied-web-direct-tooweb-server"></a>（拒絕）Web 直接 tooWeb 伺服器
因為網頁伺服器 hello、 IIS01 和 hello 防火牆會在 hello 它們共用相同的雲端服務 hello 相同公開 IP 位址。 因此任何 HTTP 流量會被導向 toohello 防火牆。 雖然會成功處理 hello 要求，它不能移直接 toohello Web 伺服器，它通過，依照設計，透過 hello 防火牆第一次。 請參閱 hello hello 流量本節中的第一個案例。

#### <a name="denied-web-toobackend-server"></a>（拒絕）Web tooBackend 伺服器
1. 網際網路的使用者嘗試 tooaccess AppVM01 上的檔案，即可透過 hello BackEnd001.CloudApp.Net 服務
2. 因為不有開啟的檔案共用的任何端點，這不會傳送 hello 雲端服務，並不會連線到 hello 伺服器
3. 如果基於某些原因，hello 端點處於開啟狀態，NSG 規則 5 (網際網路 tooVNet) 會封鎖此流量

#### <a name="denied-web-dns-lookup-on-dns-server"></a>(拒絕) DNS 伺服器上的 Web DNS 查閱
1. 網際網路的使用者嘗試 toolookup DNS01 內部 DNS 記錄透過 hello BackEnd001.CloudApp.Net 服務
2. 因為沒有開啟以供 DNS 的端點，這不會傳送 hello 雲端服務，並不會連線到 hello 伺服器
3. 如果基於某些原因，hello 端點處於開啟狀態，NSG 規則 5 (網際網路 tooVNet) 會封鎖此流量 (注意： 不原因有兩個適用於該規則 1 」 (DNS)、 第一個 hello 來源位址是 hello 網際網路，此規則只適用於 toohello 也為 hello 本機 VNet 來源這是允許規則，讓它永遠不會拒絕的流量）

#### <a name="denied-web-toosql-access-through-firewall"></a>（拒絕）透過防火牆 web tooSQL 存取
1. 網際網路使用者從 FrontEnd001.CloudApp.Net (網際網路面向雲端服務) 要求 SQL 資料
2. 因為沒有開啟以供 SQL 的端點，這不會傳送 hello 雲端服務，並不會到達 hello 防火牆
3. 如果端點處於開啟狀態的因為某些原因，hello Frontend 子網路會開始處理輸入的規則：
   1. NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則
   2. NSG 規則 2 」 (RDP) 不會套用移動 toonext 規則
   3. NSG 規則 2 (網際網路 tooFirewall) 會套用，流量會允許中停止的規則處理
4. 流量達到 hello 防火牆 (10.0.1.4) 的內部 IP 位址
5. 防火牆具有任何轉送規則的 SQL，並卸除 hello 流量

## <a name="conclusion"></a>結論
這是相當直接的方式，保護您的應用程式的防火牆和隔離 hello 後端的輸入流量子網路。

您可以在[這裡][HOME]找到更多範例和網路安全性界限的概觀。

## <a name="references"></a>參考
### <a name="main-script-and-network-config"></a>主要的指令碼和網路組態
在 PowerShell 指令碼檔案中儲存 hello 完整的指令碼。 將儲存到檔案中名為"NetworkConf2.xml"hello 網路組態。
視需要修改 hello 使用者定義的變數。 執行 hello 指令碼，然後遵循 hello 防火牆規則設定指示上述。

#### <a name="full-script"></a>完整指令碼
此指令碼，會根據 hello 使用者定義的變數：

1. 連接 tooan Azure 訂用帳戶
2. 建立新的儲存體帳戶
3. 建立新的 VNet 和 hello 網路組態檔中所定義的兩個子網路
4. 建置 4 個 Windows Server VM
5. 設定 NSG，包括：
   * 建立 NSG
   * 在其中填入規則
   * 繫結 hello NSG toohello 適當的子網路

此 PowerShell 指令碼應該在連線到網際網路的電腦或伺服器上本機執行。

> [!IMPORTANT]
> 此指令碼在執行時，PowerShell 中可能會跳出警告或其他參考訊息。 只有紅色字體的錯誤訊息才需要擔心。
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and Network Security Groups in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Two new cloud services
       - Two Subnets (FrontEnd and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet (plus hello NVA on hello FrontEnd subnet)
       - Three Servers on hello BackEnd Subnet
       - Network Security Groups tooallow/deny traffic patterns as declared

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Security requirements are different for each use case and can be addressed in a
      myriad of ways. Please be sure that any sensitive data or applications are behind
      hello appropriate layer(s) of protection. This script serves as an example of some
      of hello techniques that can be used, but should not be used for all scenarios. You
      are responsible tooassess your security needs and hello appropriate protections
      needed, and then effectively implement those protections.

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       myFirewall - 10.0.1.4
       IIS01      - 10.0.1.5

      BackEnd Service (BackEnd subnet 10.0.2.0/24)
       DNS01      - 10.0.2.4
       AppVM01    - 10.0.2.5
       AppVM02    - 10.0.2.6

    #>

    # Fixed Variables
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf2.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure proper NSG Rule creation later in this script:
        #       - hello Web Server must be VM 1
        #       - hello AppVM1 Server must be VM 2
        #       - hello DNS server must be VM 4
        #
        #       Otherwise hello NSG rules in hello last section of this
        #       script will need toobe changed toomatch hello modified
        #       VM array numbers ($i) so hello NSG Rule IP addresses
        #       are aligned toohello associated VM IP addresses.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
            Return}
        Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
              New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

      # Update Subscription Pointer tooNew Storage Account
        Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: Web traffic goes through hello firewall, so we'll need tooset up a HTTP endpoint.
                #       Also, hello firewall will be redirecting web traffic tooa new IP and Port in a
                #       forwarding rule, so hello HTTP endpoint here will have hello same public and local
                #       port and hello firewall will do hello NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                    # Note: A Remote Desktop endpoint is automatically created when each VM is created.
                }
            $i++
        }

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) too$($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
            -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
            -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
            -Protocol *

        # Assign hello NSG toohello Subnets
            Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
            Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
            Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a>網路組態檔
儲存此 xml 檔，以更新的位置，並新增 hello 連結 toothis 檔案 toohello $NetworkConfigFile 變數上述 hello 指令碼中。

    <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
      <VirtualNetworkConfiguration>
        <Dns>
          <DnsServers>
            <DnsServer name="DNS01" IPAddress="10.0.2.4" />
            <DnsServer name="Level3" IPAddress="209.244.0.3" />
          </DnsServers>
        </Dns>
        <VirtualNetworkSites>
          <VirtualNetworkSite name="CorpNetwork" Location="Central US">
            <AddressSpace>
              <AddressPrefix>10.0.0.0/16</AddressPrefix>
            </AddressSpace>
            <Subnets>
              <Subnet name="FrontEnd">
                <AddressPrefix>10.0.1.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="BackEnd">
                <AddressPrefix>10.0.2.0/24</AddressPrefix>
              </Subnet>
            </Subnets>
            <DnsServersRef>
              <DnsServerRef name="DNS01" />
              <DnsServerRef name="Level3" />
            </DnsServersRef>
          </VirtualNetworkSite>
        </VirtualNetworkSites>
      </VirtualNetworkConfiguration>
    </NetworkConfiguration>

#### <a name="sample-application-scripts"></a>範例應用程式指令碼
如果您想 tooinstall 範例應用程式，和其他周邊網路的範例，其中一個已提供在 hello 下列連結：[範例應用程式指令碼][SampleApp]

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "具有 NSG 的輸入 DMZ"
[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "目的地 NAT 圖示"
[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "防火牆規則"
[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "防火牆規則啟用"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
