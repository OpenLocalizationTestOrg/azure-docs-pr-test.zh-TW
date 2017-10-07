---
title: "快速入門：在 Azure 虛擬機器上手動安裝單一執行個體 SAP HANA | Microsoft Docs"
description: "在 Azure 虛擬機器上手動安裝單一執行個體 SAP HANA 的快速入門指南"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: c51a2a06-6e97-429b-a346-b433a785c9f0
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 57b58b8e07379eed5641f5f89d55b38f52c69e44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-manual-installation-of-single-instance-sap-hana-on-azure-vms"></a>快速入門：在 Azure VM 上手動安裝單一執行個體 SAP HANA
## <a name="introduction"></a>簡介
當您手動安裝 SAP NetWeaver 7.5 和 SAP HANA 1.0 SP12 時，本指南可協助您在 Azure 虛擬機器 (VM) 上設定單一執行個體的 SAP HANA。 本指南的 hello 重點是在部署在 Azure 上 SAP HANA。 它不會取代 SAP 文件。 

>[!Note]
>本指南說明如何將 SAP HANA 部署到 Azure VM。 如需將 SAP HANA 部署至 HANA 大型執行個體上的資訊，請參閱[在 Azure 虛擬機器 (VM) 上使用 SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/get-started)。
 
## <a name="prerequisites"></a>必要條件
本指南假設您已熟悉如下的這類基礎結構即服務 (IaaS) 基本知識：
 * 如何 toodeploy 虛擬機器或虛擬網路透過 hello Azure 入口網站或 PowerShell。
 * hello Azure 跨平台命令列介面 (CLI)，包括 hello 選項 toouse JavaScript Object Notation (JSON) 範本。

本指南也假設您已熟悉：
* SAP HANA 及 SAP NetWeaver 和如何 tooinstall 它們在內部部署。
* 安裝和操作 SAP HANA，以及在 Azure 上的 SAP 應用程式執行個體。
* hello 下列概念和程序：
   * 在 Azure 上規劃 SAP 部署，包括 Azure 虛擬網路規劃和 Azure 儲存體使用方式。 請參閱 [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide)。
   * 部署原則和方式 toodeploy Azure 中的 Vm。 請參閱[適用於 SAP 的 Azure 虛擬機器部署](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/deployment-guide)。
   * Azure 上的 SAP NetWeaver ASCS (ABAP SAP 中央服務)、SCS (SAP 中央服務)，以及 ERS (評估的收貨結算) 高可用性。 請參閱 [Azure VM 上的 SAP NetWeaver 高可用性](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide)。
   * 有關如何運用 ASCS/SCS 在 Azure 上的多重 SID 安裝 tooimprove 效率。 請參閱[建立 SAP NetWeaver 多 SID 組態](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-multi-sid)。 
   * Azure 中以 Linux 驅動的 VM 作為基礎執行 SAP NetWeaver 的準則。 請參閱[在 Microsoft Azure SUSE Linux VM 上執行 SAP NetWeaver](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/suse-quickstart)。 本指南提供在 Azure Vm 和詳細資料中的 Linux 特定設定 tooproperly 將 Azure 儲存體磁碟 tooLinux Vm 的連接。

此時，SAP 僅認證 Azure VM 適用於 SAP HANA 相應增加設定。 尚未支援適合 SAP HANA 工作負載的相應放大設定。 針對相應增加組態案例中的 SAP HANA 高可用性，請參閱 [Azure 虛擬機器 (VM) 上 SAP HANA 的高可用性](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability)。

如果您搜尋 tooget SAP HANA 執行個體或 S/4HANA 或 BW/4HANA 系統部署在非常快速的時間，您應該考慮的 hello 使用量[SAP 雲端應用裝置程式庫](http://cal.sap.com)。 例如，您可以在[本指南](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h)中找到在 Azure 上透過 SAP CAL 部署 S/4HANA 系統的相關文件。 您只需要 toohave 是 Azure 訂用帳戶和 SAP 使用者可以向 SAP 雲端應用裝置程式庫。

## <a name="additional-resources"></a>其他資源
### <a name="sap-hana-backup"></a>SAP HANA 備份
如需在 Azure VM 上備份 SAP HANA 資料庫的資訊，請參閱：
* [Azure 虛擬機器上的 SAP HANA 備份指南](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-guide)
* [檔案層級的 SAP HANA Azure 備份](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-file-level)
* [以儲存體快照集為基礎的 SAP HANA 備份](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-storage-snapshots)

### <a name="sap-cloud-appliance-library"></a>SAP 雲端應用裝置程式庫
如需使用 SAP 雲端應用裝置程式庫 toodeploy S/4HANA 或 BW/4HANA 資訊，請參閱[部署 SAP S/4HANA 或 Microsoft Azure 上的 BW/4HANA](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h)。

### <a name="sap-hana-supported-operating-systems"></a>SAP HANA 支援的作業系統
如需 SAP HANA 支援作業系統的資訊，請參閱 [SAP 支援附註 #2235581 - SAP HANA︰支援的作業系統](https://launchpad.support.sap.com/#/notes/2235581/E)。 Azure VM 僅支援這些作業系統的其中一部份。 hello 下列作業系統都支援的 toodeploy 在 Azure 上 SAP HANA: 

* SUSE Linux Enterprise Server 12.x
* Red Hat Enterprise Linux 7.2

如需關於 SAP HANA 和不同 Linux 作業系統的其他 SAP 文件，請參閱：

* [SAP 支援附註 #171356 - 在 Linux 上的 SAP 軟體︰一般資訊](https://launchpad.support.sap.com/#/notes/1984787)
* [SAP 支援附註 #1944799 - SLES 作業系統安裝的 SAP HANA 指南](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html)
* [SAP 支援附註 #2205917 - 針對 SLES 12 for SAP 應用程式的 SAP HANA DB 建議作業系統設定](https://launchpad.support.sap.com/#/notes/2205917/E)
* [SAP 支援附註 #1984787 - SUSE Linux Enterprise Server 12：安裝注意事項](https://launchpad.support.sap.com/#/notes/1984787)
* [SAP 支援附註 #1391070 - Linux UUID 解決方案](https://launchpad.support.sap.com/#/notes/1391070)
* [SAP 支援附註 #2009879 - 適用於 Red Hat Enterprise Linux (RHEL) 作業系統的 SAP HANA 指南](https://launchpad.support.sap.com/#/notes/2009879)
* [2292690 - SAP HANA DB：適用於 RHEL 7 的建議作業系統設定](https://launchpad.support.sap.com/#/notes/2292690/E)

### <a name="sap-monitoring-in-azure"></a>Azure 中的 SAP 監視
如需 Azure 中之 SAP 監視的相關資訊，請參閱：

* [SAP 附註 2191498](https://launchpad.support.sap.com/#/notes/2191498/E)。 本附註討論對 Azure 上的 Linux VM 進行 SAP「增強型監視」。 
* [SAP 附註 1102124](https://launchpad.support.sap.com/#/notes/1102124/E)。 本附註討論 Linux 上之 SAPOSCOL 的相關資訊。 
* [SAP 附註 2178632](https://launchpad.support.sap.com/#/notes/2178632/E)。 本附註討論 Microsoft Azure 上的 SAP 主要監視計量。

### <a name="azure-vm-types"></a>Azure VM 類型
與 SAP HANA 搭配使用的 Azure VM 類型與SAP 支援的工作負載情節，都記載於 [SAP 認證的 IaaS 平台](https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/iaas.html)。 

Azure VM 類型經過驗證的 SAP 適用於 SAP NetWeaver 或 hello S/4HANA 應用程式層會記載於[SAP 附註 1928533 Azure 上的 SAP 應用程式： 支援產品與 Azure VM 類型](https://launchpad.support.sap.com/#/notes/1928533/E)。

>[!Note]
>Azure 資源管理員，且 hello 傳統部署模型上才支援 SAP Linux Azure 整合。 

## <a name="manual-installation-of-sap-hana"></a>手動安裝 SAP HANA
本指南說明如何 toomanually SAP HANA 上安裝 Azure Vm 中兩個不同的方式：

* 使用分散式 NetWeaver 安裝在 hello 安裝資料庫執行個體 」 的步驟一部分的 SAP 軟體佈建 Manager (SWPM)
* 使用 hello SAP HANA 資料庫生命週期管理員工具 HDBLCM，，然後安裝 NetWeaver

您也可以使用 SWPM tooinstall 一個的單一 VM 中的所有元件 （SAP HANA、 hello SAP 應用程式伺服器和 hello ASCS 執行個體） 中所述[SAP HANA 部落格通知](https://blogs.saphana.com/2013/12/31/announcement-sap-hana-and-sap-netweaver-as-abap-deployed-on-one-server-is-generally-available/)。 這個選項不說明本快速入門指南中，但必須納入考量的問題是的 hello hello 相同。

開始安裝之前，我們建議您先閱讀 hello"準備 Azure Vm 的 SAP HANA 的手動安裝 」 一節稍後在本指南。 當您只使用預設的 Azure VM 設定時，這樣做有助於避免數個可能發生的基本錯誤。

## <a name="key-steps-for-sap-hana-installation-when-you-use-sap-swpm"></a>當您使用 SAP SWPM 時，SAP HANA 安裝的主要步驟
當您使用 SAP SWPM tooperform 分散式的 SAP NetWeaver 7.5 安裝時，此區段會列出 hello 手動、 單一執行個體的 SAP HANA 安裝的主要步驟。 hello 個別步驟的更多詳細資料螢幕擷取畫面，稍後在本指南中說明。

1. 建立包含這兩個測試 VM 的 Azure 虛擬網路。
2. 部署 hello 兩個 Azure Vm 的作業系統 （在本例中，SUSE Linux Enterprise Server (SLES) 和 SAP 應用程式 12 sp1 SLES），根據 toohello Azure 資源管理員的模型。
3. 附加兩個 Azure 標準或高階儲存體磁碟 （例如，75 GB 或 500 GB 磁碟） toohello 應用程式伺服器 VM。
4. 附加 premium 儲存體磁碟 toohello HANA DB 伺服器 VM。 如需詳細資訊，請參閱本指南稍後的 hello 磁碟 < 安裝 > 一節。
5. 根據大小或輸送量需求，附加多個磁碟，然後再建立等量磁碟區在 hello 作業系統層級 hello VM 內使用邏輯磁碟區管理或多個裝置管理工具 (MDADM)。
6. Hello 附加磁碟或邏輯磁碟區上建立 XFS 檔案系統。
7. 掛接 hello 新 XFS 檔案系統 hello 作業系統層級。 使用所有的 hello SAP 軟體的一個檔案系統。 使用例如 hello hello /sapmnt 目錄和備份，其他檔案系統。 Hello SAP HANA 資料庫在伺服器上，將 hello XFS 檔案系統掛接 /hana 以及 /usr/sap hello 高階儲存體磁碟。 此程序是必要的 tooprevent hello 根檔案系統，這並不是大型 Linux 的 Azure Vm 上填滿。
8. 輸入 hello /etc/hosts hosts 檔案中的 hello 測試 Vm 的 hello 本機 IP 位址。
9. 輸入 hello **nofail** hello /etc/hosts fstab 檔案中的參數。
10. 設定 Linux 核心參數，根據您使用 toohello Linux 作業系統版本。 如需詳細資訊，請參閱 hello 適當 SAP 附註會討論 HANA hello 本指南的 < 核心參數 > 一節。
11. 新增交換空間。
12. （選擇性） 在 hello 測試 Vm 上安裝圖形化的桌面。 否則，請使用遠端 SAPinst 安裝。
13. 從 hello SAP 服務 Marketplace 下載 hello SAP 軟體。
14. Hello 應用程式伺服器 VM 上安裝 hello SAP ASCS 執行個體。
15. Hello 之間共用 hello /sapmnt 目錄使用 NFS 測試 Vm。 hello NFS 伺服器 hello 應用程式伺服器 VM。
16. 安裝 hello 資料庫執行個體，包括 HANA、 使用 SWPM hello DB 伺服器 VM 上。
17. Hello 應用程式伺服器 VM 上安裝 hello 主應用程式伺服器 (PAS)。
18. 啟動 SAP 管理主控台 (SAP MC)。 例如，連線到 SAP GUI 或 HANA Studio。

## <a name="key-steps-for-sap-hana-installation-when-you-use-hdblcm"></a>當您使用 HDBLCM 時，SAP HANA 安裝的主要步驟
當您使用 SAP HDBLCM tooperform 分散式的 SAP NetWeaver 7.5 安裝時，此區段會列出 hello 手動、 單一執行個體的 SAP HANA 安裝的主要步驟。 hello 個別步驟的更多詳細資料螢幕擷取畫面，本指南中說明。

1. 建立包含這兩個測試 VM 的 Azure 虛擬網路。
2. 將兩個 Azure Vm （在本例中，SLES 和 SLES SAP 應用程式 12 sp1） 作業系統部署，根據 toohello Azure 資源管理員的模型。
3. 附加兩個 Azure 標準或高階儲存體磁碟 （例如，75 GB 或 500 GB 磁碟） toohello 應用程式伺服器 VM。
4. 附加 premium 儲存體磁碟 toohello HANA DB 伺服器 VM。 如需詳細資訊，請參閱本指南稍後的 hello 磁碟 < 安裝 > 一節。
5. 根據大小或輸送量需求，附加多個磁碟，並使用在 hello OS hello VM 內的層級的邏輯磁碟區管理或多個裝置管理工具 (MDADM) 來建立等量磁碟區。
6. Hello 附加磁碟或邏輯磁碟區上建立 XFS 檔案系統。
7. 掛接 hello 新 XFS 檔案系統 hello 作業系統層級。 使用一個檔案系統的所有 hello SAP 軟體，並使用 hello 另一個則用於 hello /sapmnt 目錄和備份，例如。 Hello SAP HANA 資料庫在伺服器上，將 hello XFS 檔案系統掛接 /hana 以及 /usr/sap hello 高階儲存體磁碟。 此程序是必要 toohelp 防止 hello 根檔案系統，它不是大型 Linux 的 Azure Vm 上，填滿。
8. 輸入 hello /etc/hosts hosts 檔案中的 hello 測試 Vm 的 hello 本機 IP 位址。
9. 輸入 hello **nofail** hello /etc/hosts fstab 檔案中的參數。
10. 設定核心參數，根據您使用 toohello Linux 作業系統版本。 如需詳細資訊，請參閱 hello 適當 SAP 附註會討論 HANA hello 本指南的 < 核心參數 > 一節。
11. 新增交換空間。
12. （選擇性） 在 hello 測試 Vm 上安裝圖形化的桌面。 否則，請使用遠端 SAPinst 安裝。
13. 從 hello SAP 服務 Marketplace 下載 hello SAP 軟體。
14. 建立群組，sapsys，與群組識別碼 1001 hello HANA 資料庫伺服器 VM 上。
15. 使用 HANA 資料庫生命週期管理員 (HDBLCM) hello DB 伺服器 VM 上安裝 SAP HANA。
16. Hello 應用程式伺服器 VM 上安裝 hello SAP ASCS 執行個體。
17. Hello 之間共用 hello /sapmnt 目錄使用 NFS 測試 Vm。 hello NFS 伺服器 hello 應用程式伺服器 VM。
18. 安裝 hello 資料庫執行個體，包括 HANA、 使用 SWPM hello HANA 資料庫伺服器 VM 上。
19. Hello 應用程式伺服器 VM 上安裝 hello 主應用程式伺服器 (PAS)。
20. 啟動 SAP MC。 透過 SAP GUI 或 HANA Studio 連線。

## <a name="preparing-azure-vms-for-a-manual-installation-of-sap-hana"></a>準備 Azure VM 以便手動安裝 SAP HANA
本章節涵蓋下列主題中的 hello:

* OS 更新
* 磁碟設定
* 核心參數
* 檔案系統
* hello /etc/hosts 主機檔案
* hello /etc/hosts fstab 檔案

### <a name="os-updates"></a>OS 更新
請先檢查 Linux 作業系統更新和修正程式，然後再安裝其他軟體。 藉由安裝修補程式時，您可能會無法 tooavoid 呼叫 toohello 的技術支援。

請確定您是使用︰
* 適用於 SAP 應用程式的 SUSE Linux Enterprise Server。
* 適用於 SAP 應用程式的 Red Hat Enterprise Linux 或適用於 SAP HANA 的 Red Hat Enterprise Linux。 

如果您還沒有這麼做，您的 Linux 訂閱 hello Linux 廠商登錄 hello 作業系統部署。 請注意，SUSE 具有適用於 SAP 應用程式的 OS 映像，已經包含服務且會自動註冊。

以下是檢查 for SUSE Linux 使用 hello 可用的修補程式的範例**zypper**命令：

 `sudo zypper list-patches`

Hello 問題類型而定，依類別和嚴重性分類修補程式。 常用的分類值為：**security (安全性)**、**recommended (建議)**、**optional (選用)**、**feature (功能)**、**document (文件)** 或 **yast**。
常用的嚴重性值為：**critical (嚴重)**、**important (重要)**、**moderate (中)**、**low (低)** 或 **unspecified (未指定)**。

hello **zypper**命令看起來只 hello 更新，您已安裝的封裝需要。 例如，您可以使用此命令：

`sudo zypper patch  --category=security,recommended --severity=critical,important`

您可以加入 hello 參數`--dry-run`tootest hello 更新，而不需實際更新 hello 系統。


### <a name="disk-setup"></a>磁碟設定
在 Azure 上的 Linux VM 中的 hello 根檔案系統有大小限制。 因此，它是必要的 tooattach 額外的磁碟空間 tooan Azure VM 執行 SAP。 Azure Vm SAP 應用程式伺服器，可能就已經夠用 hello 使用標準的 Azure 儲存體磁碟。 不過，對於 SAP HANA DBMS 的 Azure Vm，hello 使用 Azure 高階儲存體磁碟，生產環境和非生產實作是必要的。

根據 hello [SAP HANA TDI 存放裝置需求](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html)，建議 hello 下列 Azure 高階儲存體組態： 

| VM SKU | RAM |  /hana/data 和 /hana/log <br /> 與 LVM 或 MDADM 等量 | HANA/shared | /root volume | /usr/sap |
| --- | --- | --- | --- | --- | --- |
| GS5 | 448 GB | 2 x P30 | 1 x P20 | 1 x P10 | 1 x P10 | 

在 hello 建議的磁碟組態中，hello HANA 資料磁碟區與記錄檔磁碟區會放在相同設定的 Azure 高階儲存體磁碟會等量散佈 LVM 或 MDADM hello。 不需要 toodefine 任何 RAID 備援層級，因為 Azure 高階儲存體保持 hello 磁碟備援的三個映像。 toomake 確定您已設定足夠的儲存空間，請參閱 hello [SAP HANA TDI 存放裝置需求](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html)和[SAP HANA 伺服器安裝及更新指南](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm)。 也請考慮 hello hello 的其他虛擬硬碟 (VHD) 輸送量磁碟區不同的 Azure 高階儲存體磁碟中所述[高效能高階儲存體和受管理的 Vm 磁碟](https://docs.microsoft.com/azure/storage/storage-premium-storage)。 

您可以加入更多的進階儲存體磁碟 toohello HANA DBMS Vm 來儲存資料庫或交易記錄備份。

如需 hello 兩個主要工具 tooconfigure 等量的詳細資訊，請參閱下列發行項的 hello:

* [在 Linux 上設定軟體 RAID](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [設定 Azure 中 Linux VM 的 LVM](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

如需有關附加磁碟 tooAzure Vm 執行 Linux 作為客體作業系統、 請參閱 <<c0> [ 新增磁碟 tooa Linux VM](../../linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

Azure 高階儲存體可讓您 toodefine 磁碟快取模式。 持有 /hana/data 和 /hana/log hello 等量集，磁碟快取應該停用。 應該設定太的 hello 其他磁碟區 （磁碟），hello 快取模式**ReadOnly**。

如需詳細資訊，請參閱[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../../../storage/common/storage-premium-storage.md)。

toofind 範例 JSON 範本建立的 Vm，跳過[Azure 快速入門範本](https://github.com/Azure/azure-quickstart-templates)。
hello vm-簡單-sles 範本是基本的範本。 它包含儲存體區段與其他 100 GB 的資料磁碟。 此範本可用來當做基底。 您可以調整 hello 範本 tooyour 特定設定。

>[!Note]
>如中所述，使用 UUID 是重要的 tooattach hello Azure 儲存體磁碟[執行 SAP NetWeaver on Microsoft Azure SUSE Linux Vm](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

在 hello 測試環境中，兩個標準的 Azure 儲存體中的磁碟附加的 toohello SAP 應用程式伺服器 VM，hello 下列螢幕擷取畫面所示。 一個磁碟儲存所有 hello SAP 軟體 （包括 NetWeaver 7.5，SAP GUI 與 SAP HANA） 安裝。 足夠的可用空間會是可用的其他需求 （例如，備份和測試資料），和相同的 SAP 版圖的 hello /sapmnt 目錄 （也就是 SAP 設定檔） toobe 隸屬 toohello 的所有 Vm 之間共用，同時能確保 hello 第二個磁碟。

![SAP HANA 應用程式伺服器的 [磁碟] 視窗，其中顯示兩個資料磁碟及其大小](./media/hana-get-started/image003.jpg)


### <a name="kernel-parameters"></a>核心參數
SAP HANA 需要特定 Linux 核心設定，這不是 hello 標準 Azure 資源庫映像的一部分，而且必須手動設定。 根據您是否使用 SUSE 或 Red Hat，hello 參數可能不同。 稍早所列的 hello SAP 附註會提供這些參數的相關資訊。 在 hello 螢幕擷取畫面所示，已用 SUSE Linux 12 SP1。 

SLES SAP 應用程式 12 GA 如和 SLES SAP 應用程式 12 sp1 有全新的工具、**微調 adm**，取代 hello 舊**sapconf**工具。 **tuned-adm** 有特別的 SAP HANA 設定檔可供其使用。 SAP hana tootune hello 系統以根使用者身分輸入 hello 下列：

   `tuned-adm profile sap-hana`

如需有關**微調 adm**，請參閱 hello [SUSE 文件中的有關微調 adm](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip)。

在下列螢幕擷取畫面的 hello，您可以查看如何**微調 adm**變更的 hello`transparent_hugepage`和`numa_balancing`值，根據 toohello 必要 SAP HANA 設定。

![hello 微調 adm 工具根據 toorequired SAP HANA 設定的值變更。](./media/hana-get-started/image005.jpg)

toomake hello SAP HANA 核心設定永久性的會使用**grub2** SLES 12 上。 如需有關**grub2**，go toohello[組態檔結構](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip)hello SUSE 文件的區段。

hello 下列螢幕擷取畫面顯示如何 hello 核心設定已變更 hello 組態檔中，以及接著編譯使用**grub2 mkconfig**:

![Hello 組態檔中變更，並且使用 grub2 mkconfig 編譯的核心設定](./media/hana-get-started/image006.jpg)

另一個選項是使用 YaST 和 hello toochange hello 設定**開機載入器** > **核心參數**設定：

![hello 核心參數設定 索引標籤中 YaST 開機載入器](./media/hana-get-started/image007.jpg)

### <a name="file-systems"></a>檔案系統
hello 下列螢幕擷取畫面顯示 hello SAP 應用程式伺服器 VM 之上 hello 兩個連接標準的 Azure 儲存體磁碟所建立的兩個檔案系統。 這兩個檔案系統的型別 XFS 且已掛接太/sapdata 和 /sapsoftware。

它是不必要的 toostructure 以這種方式在檔案系統。 您必須建構 hello 磁碟空間的其他選項。 hello 最重要的考量是 tooprevent hello 根檔案系統的可用空間不足。

![Hello SAP 應用程式伺服器 VM 上建立兩個檔案系統](./media/hana-get-started/image008.jpg)

關於 hello SAP HANA 資料庫 VM，資料庫在安裝期間，當您使用 SAPinst (SWPM) 和 hello**一般**安裝選項時，一切都已安裝 /hana 和 /usr/sap 底下。 hello hello SAP HANA 記錄備份的預設位置是在 /usr/sap 之下。 同樣地，因為它是重要的 tooprevent hello 根檔案系統的儲存空間不足，請確定有足夠的可用空間 /hana 和 /usr/sap 下再使用 SWPM 安裝 SAP HANA。

如需 hello 標準檔案系統配置的 SAP HANA 的說明，請參閱 hello [SAP HANA 伺服器安裝及更新指南](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm)。

![建立 hello SAP 應用程式伺服器 VM 上的其他檔案系統](./media/hana-get-started/image009.jpg)

當您在標準 SLES/SLES 的 SAP 應用程式 12 Azure 資源庫映像上安裝 SAP NetWeaver 時，會顯示訊息，指出沒有交換空間，如下列螢幕擷取畫面的 hello 中所示。 toodismiss 這個訊息，您可以使用，以手動新增分頁檔**dd**， **mkswap**，和**swapon**。 toolearn 作法，請搜尋 「 交換檔手動新增 「 在 hello[使用 hello YaST Partitioner](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) hello SUSE 文件的區段。

另一個選項是使用 hello Linux VM 代理程式 tooconfigure 交換空間。 如需詳細資訊，請參閱 hello [Azure Linux 代理程式使用者指南](../../linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

![指出沒有足夠交換空間的快顯訊息](./media/hana-get-started/image010.jpg)


### <a name="hello-etchosts-file"></a>hello /etc/hosts 主機檔案
啟動 tooinstall SAP 之前，請確定您包含 hello 主機名稱和 IP 位址的 hello SAP Vm hello /etc/hosts 檔案中。 將一個 Azure 虛擬網路內的所有 hello SAP Vm 都部署，然後使用 hello 內部 IP 位址，如下所示：

![Hello /etc/hosts 檔案中列出的主機名稱和 IP 位址的 hello SAP Vm](./media/hana-get-started/image011.jpg)

### <a name="hello-etcfstab-file"></a>hello /etc/hosts fstab 檔案

它是很有幫助 tooadd hello **nofail**參數 toohello fstab 檔案。 如此一來，如果出錯 hello 磁碟 hello VM 不會不停止回應 hello 開機程序。 但是請記住，額外的磁碟空間可能無法使用，而且處理程序可能會填滿 hello 根檔案系統。 如果遺失 /hana，SAP HANA 將無法啟動。

![新增 hello nofail 參數 toohello fstab 檔案](./media/hana-get-started/image000c.jpg)

## <a name="graphical-gnome-desktop-on-sles-12sles-for-sap-applications-12"></a>SLES 12/SLES for SAP Applications 12 上的圖形化 GNOME 桌面
本章節涵蓋下列主題中的 hello:

* Hello GNOME 桌面和 xrdp 上安裝 SLES 12/SLES SAP 應用程式 12
* 在 SLES 12/SLES for SAP Applications 12 上使用 Firefox 來執行以 Java 為基礎的 SAP MC

您也可以使用替代項目，例如 Xterminal 或 VNC (不在本指南中說明)。

### <a name="installing-hello-gnome-desktop-and-xrdp-on-sles-12sles-for-sap-applications-12"></a>Hello GNOME 桌面和 xrdp 上安裝 SLES 12/SLES SAP 應用程式 12
如果您有 Windows 背景時，可以輕鬆地使用直接在 hello SAP Linux Vm toorun Firefox、 SAPinst、 SAP GUI、 SAP MC 或 HANA Studio 中的圖形化桌面，並透過從 Windows 電腦的 hello 遠端桌面通訊協定 (RDP) 連線 toohello VM。 取決於您的公司原則，關於新增圖形化使用者介面 tooproduction 和非實際執行的 Linux 系統，您可能想 tooinstall GNOME 您伺服器上。 在 SAP 應用程式 12 VM Azure SLES 12/SLES tooinstall hello GNOME 桌面：

1. 輸入下列命令 （例如，在 PuTTY 視窗） 中的 hello 安裝 hello GNOME 桌面：

   `zypper in -t pattern gnome-basic`

2. 安裝 xrdp tooallow 連接 toohello 透過 RDP 的 VM:

   `zypper in xrdp`

3. 編輯 /etc/sysconfig/windowmanager，並設定 hello 預設視窗管理員 tooGNOME︰

   `DEFAULT_WM="gnome"`

4. 執行**chkconfig** toomake 確定該 xrdp 重新開機後自動啟動：

   `chkconfig -level 3 xrdp on`

5. 如果您擁有 hello RDP 連線的問題，請再試一次 toorestart （從 PuTTY 視窗，例如）：

   `/etc/xrdp/xrdp.sh restart`

6. 如果 xrdp 重新啟動中所述 hello 上一個步驟無效，檢查.pid 檔案：

   `check /var/run` 

   尋找 `xrdp.pid`。 如果找到的話，移除它，然後再試一次 toorestart。

### <a name="starting-sap-mc"></a>啟動 SAP MC
安裝 hello GNOME 桌面之後，開始圖形 hello Firefox Azure SLES 12/SLES 中執行的 SAP 應用程式 12 VM 時從 Java 為基礎 SAP MC 可能會顯示錯誤因為 hello 遺漏 Java 瀏覽器外掛程式。

SAP MC 是 hello URL toostart hello `<server>:5<instance_number>13`。

如需詳細資訊，請參閱[起始 hello SAP 網頁型管理主控台](https://help.sap.com/saphelp_nwce10/helpdata/en/48/6b7c6178dc4f93e10000000a42189d/frameset.htm)。

hello 下列螢幕擷取畫面顯示 hello hello Java 瀏覽器外掛程式遺漏時所顯示的錯誤訊息：

![指出遺失 Java 瀏覽器外掛程式的錯誤訊息](./media/hana-get-started/image013.jpg)

其中一種方式 toosolve hello 問題是 tooinstall hello 缺少外掛程式使用 YaST，hello 下列螢幕擷取畫面所示：

![使用 YaST tooinstall 缺少外掛程式](./media/hana-get-started/image014.jpg)

當您重新輸入 hello SAP 管理主控台 URL 時，出現下列訊息詢問您 tooactivate hello 外掛程式：

![要求啟用外掛程式的對話方塊](./media/hana-get-started/image015.jpg)

您可能也會收到關於遺失檔案 (javafx.properties) 的錯誤訊息。 這是 Oracle Java 1.8 的 SAP GUI 7.4 相關的 toohello 需求。 (請參閱 [SAP 附註 2059429](https://launchpad.support.sap.com/#/notes/2059424)。)Hello IBM Java 版本都具有 SLES/SLES 所傳送的 SAP 應用程式 12 hello openjdk 封裝包括 hello 需要的 javafx.properties 檔案。 hello 方案是 toodownload，然後安裝 Oracle Java SE 8。

OpenSUSE openjdk 類似問題的相關資訊，請參閱 hello 討論[openSUSE 42.1 的 SAPGui 7.4 Java Leap](https://scn.sap.com/thread/3908306)。

## <a name="manual-installation-of-sap-hana-swpm"></a>手動安裝 SAP HANA：SWPM
本節中的螢幕擷取畫面的 hello 數列會顯示 hello 安裝 SAP NetWeaver 7.5 和 SAP HANA SP12，當您使用 SWPM (SAPinst) 的關鍵步驟。 NetWeaver 7.5 安裝的一部分，SWPM 也可以安裝 hello HANA 資料庫的單一執行個體。

在範例測試環境中，我們只安裝了一部進階商業應用程式程式設計 (ABAP) 應用程式伺服器。 Hello 下列螢幕擷取畫面所示，我們使用 hello**分散式系統**選項 tooinstall hello ASCS 和一個 Azure VM 與 SAP HANA 中的主要應用程式伺服器執行個體做為另一個 Azure VM 中的 hello 資料庫系統。

![ASCS 和使用 hello 分散式系統選項來安裝主要應用程式伺服器執行個體](./media/hana-get-started/image012.jpg)

Hello ASCS 執行個體安裝在 hello 應用程式伺服器 VM 上，而之後設定太 「 綠色 」 hello SAP 管理主控台 （如 hello 下列螢幕擷取畫面所示），在 hello /sapmnt 目錄 （包括 hello SAP 設定檔的目錄） 必須與共用 hello SAP HANA 資料庫伺服器 VM。 hello DB 安裝步驟需要存取 toothis 資訊。 toouse NFS 可設定使用 YaST hello 最佳方式 tooprovide 存取。

![SAP 管理主控台顯示 hello ASCS 執行個體 hello 應用程式伺服器 VM 上安裝和設定太 「 綠色的"](./media/hana-get-started/image016.jpg)

在應用程式伺服器 VM hello、 hello/sapmnt 目錄應該透過 NFS 共用，使用 hello **rw**和**no_root_squash**選項。 hello 的預設值為**ro**和**root_squash**，這可能會導致 tooproblems，當您安裝 hello 資料庫執行個體。

![透過使用 hello rw 和 no_root_squash 選項共用透過 NFS hello /sapmnt 目錄](./media/hana-get-started/image017b.jpg)

如 hello 的下一個螢幕擷取畫面所示，從 hello 應用程式伺服器 VM 的 hello /sapmnt 共用必須設定 hello SAP HANA 資料庫伺服器 VM 上使用**NFS 用戶端**（和 YaST）。

![設定使用 NFS 用戶端 hello /sapmnt 共用](./media/hana-get-started/image018b.jpg)

分散式的 NetWeaver 7.5 tooperform 安裝 (**資料庫執行個體**)，下列螢幕擷取畫面所示的 hello，為登入 toohello SAP HANA 資料庫伺服器 VM 並啟動 SWPM。

![安裝的資料庫執行個體，登入 toohello SAP HANA 資料庫伺服器 VM，然後啟動 SWPM](./media/hana-get-started/image019.jpg)

選取後**一般**安裝與 hello 路徑 toohello 安裝媒體上，輸入 DB SID、 hello 主機名稱、 hello 執行個體數目和 hello DB 系統管理員密碼。

![hello SAP HANA 資料庫系統管理員登入頁面](./media/hana-get-started/image035b.jpg)

Hello DBACOCKPIT 結構描述，請輸入 hello 密碼：

![hello DBACOCKPIT 結構描述的 hello 密碼項目方塊](./media/hana-get-started/image036b.jpg)

輸入 hello SAPABAP1 結構描述密碼問題：

![輸入 hello SAPABAP1 結構描述密碼問題](./media/hana-get-started/image037b.jpg)

每個工作完成後，綠色的核取記號會顯示 hello DB 安裝程序的下一個 tooeach 階段。 hello 訊息 」 執行的...資料庫執行個體已完成。」隨即顯示。

![含有確認訊息的完成工作視窗](./media/hana-get-started/image023.jpg)

安裝成功後，hello SAP 管理主控台應該也會顯示 hello 與 「 綠色 」 的資料庫執行個體，並顯示 hello 的 SAP HANA 處理程序 （hdbindexserver、 hdbcompileserver，等等） 的完整清單。

![含有 SAP HANA 程序清單的 SAP 管理主控台視窗](./media/hana-get-started/image024.jpg)

hello 下列螢幕擷取畫面顯示 hello 部分 hello SWPM hello HANA 安裝期間所建立的 hello /hana/shared 目錄下的檔案結構。 沒有任何選項 toospecify 不同的路徑，因為它是重要 toomount hello SAP HANA 安裝之前的 hello /hana 目錄下的額外磁碟空間使用 SWPM。 這樣可避免 hello 根檔案系統用完可用空間。

![HANA 安裝期間建立的 hello /hana/shared 目錄檔案結構](./media/hana-get-started/image025.jpg)

這個螢幕擷取畫面顯示 hello 檔案 hello /usr/sap 目錄結構：

![hello /usr/sap 目錄檔案結構](./media/hana-get-started/image026.jpg)

hello hello 分散式 ABAP 安裝最後一個步驟是 tooinstall hello 主要應用程式伺服器執行個體：

![ABAP 安裝顯示主要的應用程式伺服器執行個體 hello 最後一個步驟](./media/hana-get-started/image027b.jpg)

Hello 主要應用程式伺服器執行個體和 SAP GUI 安裝之後，請使用 hello **DBA Cockpit** hello SAP HANA 安裝的交易 tooconfirm 已正確完成：

![確認安裝成功的 DBA Cockpit 視窗](./media/hana-get-started/image028b.jpg)

最後一個步驟中，您可能會想 toofirst 安裝 HANA Studio hello SAP 應用程式伺服器 VM，並再連線 toohello hello DB 伺服器 VM 執行的 SAP HANA 執行個體：

![在 hello SAP 應用程式伺服器 VM 中安裝 SAP HANA Studio](./media/hana-get-started/image038b.jpg)

## <a name="manual-installation-of-sap-hana-hdblcm"></a>手動安裝 SAP HANA：HDBLCM
在加法 tooinstalling 分散式安裝中使用 SWPM 一部分的 SAP HANA，您可以安裝 hello HANA 獨立首先，使用 HDBLCM。 例如，您接著可以安裝 SAP NetWeaver 7.5。 本節中的 hello 螢幕擷取畫面顯示此程序的運作方式。

如需 hello HANA HDBLCM 工具的詳細資訊，請參閱：

* [選擇 hello 更正您工作的 SAP HANA HDBLCM](https://help.sap.com/saphelp_hanaplatform/helpdata/en/68/5cff570bb745d48c0ab6d50123ca60/content.htm)
* [SAP HANA 生命週期管理工具](http://saphanatutorial.com/sap-hana-lifecycle-management-tools/)
* [SAP HANA 伺服器安裝與更新指南](http://help.sap.com/hana/SAP_HANA_Server_Installation_Guide_en.pdf)

tooavoid 問題，預設值群組識別碼設定 hello `\<HANA SID\>adm user` （hello HDBLCM 工具所建立），定義新的群組稱為`sapsys`使用群組識別碼`1001`安裝 SAP HANA 透過 HDBLCM 之前：

![使用群組識別碼 1001 定義的新群組 "sapsys"](./media/hana-get-started/image030.jpg)

當您第一次啟動 HDBLCM hello 時，會顯示簡單 [開始] 功能表。 選取的項目 1，**安裝新的系統**hello 下列螢幕擷取畫面所示：

![Hello HDBLCM 開始視窗中的 [安裝新的系統] 選項](./media/hana-get-started/image031.jpg)

hello 下列螢幕擷取畫面會顯示您先前選取所有 hello 金鑰選項。

> [!IMPORTANT]
> 目錄會在名為 HANA 記錄檔和資料磁碟區，以及 hello 安裝路徑 （hana/這個範例中為 shared） 和 /usr/sap，不應該 hello 根檔案系統的一部分。 這些目錄屬於 toohello Azure 資料磁碟所連接的 toohello VM （hello 磁碟 < 安裝 > 一節所述）。 這種方法可避免用完空間 hello 根檔案系統。 在下列螢幕擷取畫面的 hello，您可以看到該 hello HANA 系統管理員具有使用者 ID`1005`屬於 hello`sapsys`群組 (識別碼`1001`)，定義 hello 安裝之前。

![先前選取的所有重要 SAP HANA 元件清單](./media/hana-get-started/image032.jpg)

您可以檢查 hello `\<HANA SID\>adm user` (`azdadm` hello 下列螢幕擷取畫面中) 中目錄 hello /etc/hosts passwd 詳細資料：

![HANA \<HANA SID\>adm 使用者詳細資料列在 hello /etc/hosts passwd 目錄](./media/hana-get-started/image033.jpg)

使用 HDBLCM 安裝 SAP HANA 之後，您可以看到在 SAP HANA Studio 中的 hello 檔案結構，hello 下列螢幕擷取畫面所示。 hello SAPABAP1 結構描述，其中包含所有 hello SAP NetWeaver 資料表，尚無法使用。

![SAP HANA Studio 中的 SAP HANA 檔案結構](./media/hana-get-started/image034.jpg)

安裝 SAP HANA 之後，就能在其上安裝 SAP NetWeaver。 下列螢幕擷取畫面所示的 hello，為已做為分散式安裝使用 SWPM （如 hello 前一節中所述） 執行 hello 安裝。 當您使用 SWPM 安裝 hello 資料庫執行個體時，您會輸入 hello 使用 HDBLCM （例如，主機名稱、 HANA SID 和執行個體號碼） 相同的資料。 SWPM 然後使用 hello 現有 HANA 安裝，並加入更多結構描述。

![使用 SWPM 執行分散式安裝](./media/hana-get-started/image035b.jpg)

hello 下列螢幕擷取畫面顯示 hello SWPM 安裝步驟，您輸入 hello DBACOCKPIT 結構描述相關的資料：

![其中輸入 DBACOCKPIT 結構描述資料 hello SWPM 安裝步驟](./media/hana-get-started/image036b.jpg)

輸入 hello SAPABAP1 結構描述相關的資料：

![輸入 hello SAPABAP1 結構描述相關的資料](./media/hana-get-started/image037b.jpg)

Hello SWPM 資料庫執行個體安裝完成之後，您可以看到在 SAP HANA Studio 中的 hello SAPABAP1 結構描述：

![SAP HANA Studio 中的 hello SAPABAP1 結構描述](./media/hana-get-started/image038b.jpg)

最後，hello SAP 應用程式伺服器和 SAP GUI 安裝完成之後，您可以確認 hello HANA 資料庫執行個體使用 hello **DBA Cockpit**交易：

![DBA Cockpit 交易 hello hello HANA 資料庫執行個體驗證](./media/hana-get-started/image039b.jpg)


## <a name="sap-software-downloads"></a>SAP 軟體下載
您可以從 hello SAP 服務商場，下載軟體，hello 下列螢幕擷取畫面所示。

下載適用於 Linux/HANA 的 NetWeaver 7.5：

 ![用於下載 NetWeaver 7.5 的 SAP 服務安裝和升級視窗](./media/hana-get-started/image001.jpg)

下載 HANA SP12 平台版本：

 ![用於下載 HANA SP12 平台版本的 SAP 服務安裝和升級視窗](./media/hana-get-started/image002.jpg)

