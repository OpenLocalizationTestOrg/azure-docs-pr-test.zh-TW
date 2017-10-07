---
title: "aaaExample Azure 基礎結構的逐步解說 |Microsoft 文件"
description: "深入了解 hello 金鑰設計和實作部署的指導方針在 Azure 中的範例基礎結構。"
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 281fc2c0-b533-45fa-81a3-728c0049c73d
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6b307c0112203aa83e1fada81966fc265397a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-linux-vms"></a>適用於 Linux VM 的範例 Azure 基礎結構逐步解說

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

本文將逐步解說建置範例應用程式基礎結構的方法。 我們將詳細說明設計簡單的線上存放區的結合所有 hello 指導方針和命名慣例、 可用性設定組中，虛擬網路和負載平衡器、 周圍的決策基礎結構與實際部署您的虛擬機器 (Vm)。

## <a name="example-workload"></a>範例工作負載
Adventure Works Cycles 想 toobuild 線上存放區中的應用程式所組成的 Azure:

* 執行用戶端 hello 前端 web 層中的兩個 nginx 伺服器
* 兩個在應用程式層級中處理資料和訂單的 nginx 伺服器
* 兩個做為在資料庫層級中儲存產品資料及訂單的共用叢集一部分的 MongoDB 伺服器
* 兩個在驗證層級中針對客戶帳戶及供應商的 Active Directory 網域控制站
* 所有的 hello 伺服器位於兩個子網路：
  * hello web 伺服器前端的子網路 
  * 後端子 hello 應用程式伺服器、 MongoDB 叢集和網域控制站

![不同應用程式基礎結構層級的圖表](./media/infrastructure-example/example-tiers.png)

安全的連入網路流量必須在 hello web 伺服器之間進行負載平衡與客戶瀏覽 hello 線上存放區。 從伺服器必須是負載平衡 hello 應用程式伺服器之間的 hello web 要求訂單處理 hello 表單送出的 HTTP 流量。 此外，您必須針對高可用性設計 hello 基礎結構。

必須納入 hello 產生設計：

* Azure 訂用帳戶和帳戶
* 單一資源群組
* Azure 受控磁碟
* 具有兩個子網路的虛擬網路
* Hello Vm 與角色類似的可用性設定組
* 虛擬機器

上述所有 hello，請都遵循下列命名慣例：

* Adventure Works Cycles 使用 **[IT workload]-[location]-[Azure resource]** 做為首碼
  * 例如，"**azos**"（Azure 線上存放區） 是 hello IT 工作負載名稱和"**使用**"（美國東部 2） 是 hello 位置
* 虛擬網路會使用 AZOS-USE-VN**[number]**
* 可用性設定組會使用 azos-use-as-**[role]**
* 虛擬機器名稱會使用 azos-use-vm-**[vmname]**

## <a name="azure-subscriptions-and-accounts"></a>Azure 訂用帳戶與帳戶
Adventure Works Cycles 使用其企業訂用帳戶，名為 Adventure Works 企業訂用帳戶，tooprovide 計費這樣的 IT 工作負載。

## <a name="storage"></a>儲存體
Adventure Works Cycles 決定他們應該使用 Azure 受控磁碟。 建立 VM 時，會使用這兩個可用儲存體的儲存層：

* **標準儲存體**hello 網頁伺服器、 應用程式伺服器和網域控制站和其資料磁碟。
* **高階儲存體**hello MongoDB 分區化的叢集伺服器和其資料磁碟。

## <a name="virtual-network-and-subnets"></a>虛擬網路和子網路
Hello 虛擬網路不需要持續連線 toohello Adventure 工作週期在內部部署網路，因為它們會決定在僅限雲端的虛擬網路上。

它們可以建立僅限雲端的虛擬網路以下列設定使用 hello Azure 入口網站的 hello:

* 名稱：AZOS-USE-VN01
* 位置：East US 2
* 虛擬網路位址空間：10.0.0.0/8
* 第一個子網路：
  * 名稱：FrontEnd
  * 位址空間：10.0.1.0/24
* 第二個子網路：
  * 名稱：BackEnd
  * 位址空間：10.0.2.0/24

## <a name="availability-sets"></a>可用性集合
所有的四個層，其線上存放區決定上四個可用性設定組的 Adventure Works Cycles 的 toomaintain 高可用性：

* **azos-使用-做為 web** hello 網頁伺服器
* **azos 使用-做為應用程式**hello 應用程式伺服器
* **azos-使用-為-db** hello 叢集中的伺服器 hello MongoDB 分區化
* **azos-使用-做為 dc** hello 網域控制站

## <a name="virtual-machines"></a>虛擬機器
Adventure Works Cycles 決定 hello 下列其 Azure Vm 的名稱：

* **azos 使用 vm-web01** hello 第一個網頁伺服器
* **azos 使用 vm-web02** hello 第二部 web 伺服器
* **azos 使用 vm-app01** hello 第一個應用程式伺服器
* **azos 使用 vm-app02** hello 第二個應用程式伺服器
* **azos 使用 vm-db01** hello 第一台 hello 叢集中的 MongoDB 伺服器
* **azos 使用 vm-db02** hello 第二部 MongoDB 伺服器 hello 叢集中
* **azos 使用 vm-dc01** hello 第一個網域控制站
* **azos 使用 vm-dc02** hello 第二個網域控制站

以下是 hello 產生的設定。

![在 Azure 中部署的最終應用程式基礎結構](./media/infrastructure-example/example-config.png)

這個設定包含下列各項：

* 含有兩個子網路 (前端和後端) 且僅限雲端的虛擬網路
* 使用標準和進階磁碟的 Azure 受控磁碟
* 四個可用性設定組，一個用於 hello 線上存放區的每一層
* hello hello 四層的虛擬機器
* 從 hello 網際網路 toohello 的 web 伺服器的 HTTPS 為基礎的 web 流量的外部負載平衡集
* 內部負載平衡集從 hello web 伺服器 toohello 應用程式伺服器的加密的 web 流量
* 單一資源群組
