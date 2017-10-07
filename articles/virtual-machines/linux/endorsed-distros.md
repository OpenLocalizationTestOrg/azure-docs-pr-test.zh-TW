---
title: "Linux 散發 aaaEndorsed |Microsoft 文件"
description: "了解在 Azure 背書散發套件上的 Linux，包括 Ubuntu、CentOS、Oracle 和 SUSE 的準則。"
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: 2777a526-c260-4cb9-a31a-bdfe1a55fffc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: f006972d4611434c62b72a1d8df60caf753e15f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="linux-on-distributions-endorsed-by-azure"></a>經 Azure 背書的 Linux 發佈
合作夥伴提供 hello Azure Marketplace 中的 Linux 映像。 我們使用的各種 Linux 社群 tooadd 更多類別 toohello 背書通訊群組清單。 在 hello 同時，不是發佈可從 hello Marketplace，您可以一律會將您自己的 Linux 按照 hello 指導方針，在[建立和上傳的虛擬硬碟包含 hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="supported-distributions-and-versions"></a>支援的發佈和版本
hello 下表列出 hello Linux 散發套件和支援 Azure 的版本。 請參閱太[支援適用於 Linux 映像在 Microsoft Azure 中](https://support.microsoft.com/en-us/kb/2941892)如需詳細資訊。

HYPER-V 和 Azure 的 hello Linux Integration Services (LIS) 驅動程式是 Microsoft 提供直接 toohello 上游 Linux 核心的核心模組。  根據預設，有些 LIS 驅動程式會建置到 hello 散發的核心。 以 Red Hat Enterprise (RHEL)/CentOS 作為基礎的較舊分佈可用在[適用於 Hyper-V 的 Linux 整合服務 4.1 版](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409)作為個別下載。 請參閱[Linux 核心需求](create-upload-generic.md#linux-kernel-requirements)hello LIS 驅動程式的相關詳細資訊。

hello Azure Linux 代理程式上 hello Azure Marketplace 映像已預先安裝，而且通常可從 hello 發佈封裝儲存機制。 您可以在 [GitHub](https://github.com/azure/walinuxagent)上找到原始程式碼。

| 配送映像 | 版本 | 驅動程式 | 代理程式 |
| --- | --- | --- | --- |
| CentOS |CentOS 6.3+、7.0+ |CentOS 6.3：[LIS 下載](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409)<p>CentOS 6.4 +：在核心中 |封裝：在 [repo](http://olcentgbl.trafficmanager.net/openlogic/6/openlogic/x86_64/RPMS/) 中，"WALinuxAgent" 的下方 <br/>原始程式碼：[GitHub](https://github.com/Azure/WALinuxAgent) |
| [CoreOS](https://coreos.com/docs/running-coreos/cloud-providers/azure/) |494.4.0+ |在核心中 |原始程式碼：[GitHub](https://github.com/coreos/coreos-overlay/tree/master/app-emulation/wa-linux-agent) |
| Debian |Debian 7.9+、8.2+ |在核心中 |套件：在「waagent」下的儲存機制中  <br/>原始程式碼：[GitHub](https://github.com/Azure/WALinuxAgent) |
| Oracle Linux |6.4+、7.0+ |在核心中 |套件：在「WALinuxAgent」下的儲存機制中  <br/>原始程式碼：[GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| Red Hat Enterprise Linux |RHEL 6.7+、7.1+ |在核心中 |套件：在「WALinuxAgent」下的儲存機制中  <br/>原始程式碼：[GitHub](https://github.com/Azure/WALinuxAgent) |
| SUSE Linux Enterprise |SLES/SLES for SAP<br>11 SP4<br>12 SP1+|在核心中 |套件：<p> 適用於 11：在 [Cloud:Tools](https://build.opensuse.org/project/show/Cloud:Tools) 儲存機制中<br>適用於 12：包含在 "Public Cloud" 模組中的 "python-azure-agent" 底下<br/>原始程式碼：[GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| openSUSE |openSUSE Leap 42.1+ |在核心中 |封裝：在 "python-azure-agent" 下的[雲端：工具](https://build.opensuse.org/project/show/Cloud:Tools)儲存機制中 <br/>原始程式碼：[GitHub](https://github.com/Azure/WALinuxAgent) |
| Ubuntu |Ubuntu 12.04、14.04、16.04、16.10 |在核心中 |套件：在「WALinuxAgent」下的儲存機制中  <br/>原始程式碼：[GitHub](https://github.com/Azure/WALinuxAgent) |

## <a name="partners"></a>合作夥伴

### <a name="coreos"></a>CoreOS
[https://coreos.com/docs/running-coreos/cloud-providers/azure/](https://coreos.com/docs/running-coreos/cloud-providers/azure/)

從 hello CoreOS 網站：

*CoreOS 是專為安全性、一致性和可靠性所設計。而不是安裝封裝，透過 yum 或 apt，CoreOS Linux 容器 toomanage 您的服務會在使用較高的層級的抽象概念。單一服務的程式碼和所有相依性都封裝於容器內，可在一或多部 CoreOS 機器上執行。*

### <a name="credativ"></a>Credativ
[http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure](http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure)

Credativ 是獨立諮詢和服務公司，專門用來 hello 開發和實作的專業解決方案使用免費軟體。 作為業界領先的開放原始碼專家，Credativ 的支援受到許多 IT 部門所採用，從而在國際上享有認可。 Credativ 目前與 Microsoft 合作，正準備適用於 Debian 8 (Jessie) 與 7 之前的 Debian (Wheezy) 的 Debian 映像。 這兩個影像都是在 Azure 上的特殊設計的 toorun，而且可以輕鬆管理透過 hello 平台。 Credativ hello 長期維護和更新的 hello Debian 映像透過其開啟來源支援中心的 azure 也支援。

### <a name="oracle"></a>Oracle
[http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html)

Oracle 的策略是 toooffer 廣泛的公用和私人雲端的解決方案組合。 選擇與如何部署 Oracle 雲端中的 Oracle 軟體和其他雲端的彈性，hello 策略可讓客戶。 Microsoft 與 oracle 的合作關係，讓 hello 信賴度的認證，並從 Oracle 支援客戶 toodeploy Oracle 軟體，Microsoft 公用和私人雲端中。  Oracle 對 Oracle 公用與私人雲端解決方案的承諾與投資沒有改變。

### <a name="red-hat"></a>Red Hat
[http://www.redhat.com/en/partners/strategic-alliance/microsoft](http://www.redhat.com/en/partners/strategic-alliance/microsoft)

hello 世界前置提供者的開放原始碼解決方案、 Red Hat 有助於超過 90%的全球 500 強公司解決的商業挑戰、 對齊其 IT 和商務策略，並做好準備 hello 未來的技術。 Red Hat 藉由透過開放的商務模型及可預測且價格實惠的訂閱模型，提供安全的解決方案來做到這點。

### <a name="suse"></a>SUSE
[http://www.suse.com/suse-linux-enterprise-server-on-azure](http://www.suse.com/suse-linux-enterprise-server-on-azure)

Azure 上的 SUSE Linux Enterprise Server 是一個經證實可為雲端運算提供優異可靠性與安全性的平台。 多用途的 SUSE Linux 平台緊密整合，使用 Azure 雲端服務 toodeliver 可輕鬆地管理雲端環境。 藉由多個 9,200 認證的應用程式的 SUSE Linux Enterprise Server 超過 1,800 個獨立軟體廠商，SUSE 可確保 hello 資料中心內執行支援的工作負載可以有信心地部署在 Azure 上。

### <a name="canonical"></a>Canonical
[http://www.ubuntu.com/cloud/azure](http://www.ubuntu.com/cloud/azure)

Canonical 對工程與開放社群的治理，促使 Ubuntu 在用戶端、伺服器和雲端運算 (包括消費者的個人雲端服務) 方面獲致成功。 統一且可用平台的 Ubuntu，從電話 toocloud Canonical 的願景提供一系列的一致介面 hello 電話、 平板電腦、 電視或桌面。 這個願景可讓各種機構從公用雲端提供者 toohello 決策者的消費性電子產品的 Ubuntu hello 第一個選擇，而且在個別的措辭之間的我的最愛。

與開發人員和 hello 世界各地的工程中心，Canonical 是唯一定位的 toopartner 硬體製造商、 內容提供者，與軟體開發人員 toobring Ubuntu 解決方案 toomarket 電腦、 伺服器及手持式裝置。
