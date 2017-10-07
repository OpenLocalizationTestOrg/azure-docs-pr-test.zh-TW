---
title: "aaaViewing 及修改主機名稱 |Microsoft 文件"
description: "Azure 虛擬機器，tooview 及變更主機名稱的 web 和背景工作角色的名稱解析"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c668cd8e-4e43-4d05-acc3-db64fa78d828
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 17d0dd7911754a94db3f37b924b4687da1c70aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="viewing-and-modifying-hostnames"></a>檢視與修改主機名稱
tooallow 您角色執行個體 toobe 參考依主機名稱，則必須將 hello hello 主機名稱的值為每個角色的 hello 服務組態檔中。 您執行此作業，加入所需的 hello 主機名稱 toohello **vmName**屬性 hello**角色**項目。 hello 值 hello **vmName**屬性用於做為基底 hello 的每個角色執行個體的主機名稱。 例如，如果**vmName**是*webrole*有三個該角色執行個體，hello hello 執行個體的主機名稱將是*webrole0*， *webrole1*，和*webrole2*。 因為根據 hello 虛擬機器名稱填入 hello 虛擬機器的主機名稱不需要 toospecify hello 組態檔中，虛擬機器的主機名稱。 如需設定 Microsoft Azure 服務的詳細資訊，請參閱 [Azure 服務組態結構描述 (.cscfg 檔)](https://msdn.microsoft.com/library/azure/ee758710.aspx)

## <a name="viewing-hostnames"></a>檢視主機名稱
您可以使用任何下列的 hello 工具，在雲端服務中檢視 hello 的虛擬機器和角色執行個體的主機名稱。

### <a name="azure-portal"></a>Azure 入口網站
您可以使用 hello [Azure 入口網站](http://portal.azure.com)tooview hello 的主機名稱的虛擬機器的 hello 概觀刀鋒視窗上的虛擬機器。 請記住，hello 刀鋒視窗中顯示的值**名稱**和**主機名稱**。 雖然它們一開始 hello 相同變更 hello 主機名稱不會變更 hello hello 虛擬機器或角色執行個體的名稱。

角色執行個體也可以檢視在 hello Azure 入口網站，但如果您列出雲端服務中的 hello 執行個體時，不會顯示 hello 主機名稱。 您會看到每個執行個體名稱，但該名稱不能代表 hello 主機名稱。

### <a name="service-configuration-file"></a>服務組態檔
您可以部署之服務的 hello 服務組態檔從 hello**設定**hello Azure 入口網站中的 hello 服務刀鋒視窗。 然後您可以查看 hello **vmName**屬性 hello**角色名稱**元素 toosee hello 主機名稱。 請注意，這個主機名稱用於做為基底 hello 的每個角色執行個體的主機名稱。 例如，如果**vmName**是*webrole*有三個該角色執行個體，hello hello 執行個體的主機名稱將是*webrole0*， *webrole1*，和*webrole2*。

### <a name="remote-desktop"></a>遠端桌面
啟用遠端桌面 (Windows)、 Windows PowerShell 遠端執行功能 (Windows) 或 SSH （Linux 和 Windows） 連線 tooyour 虛擬機器或角色執行個體之後，您可以透過各種方式檢視 hello 作用中的遠端桌面連線的主機名稱：

* 輸入主機名稱在 hello 命令提示字元或 SSH 終端機。
* 輸入 ipconfig/所有 hello 命令提示 (僅限 Windows)。
* Hello 系統檢視 hello 電腦名稱設定 (僅限 Windows)。

### <a name="azure-service-management-rest-api"></a>Azure 服務管理 REST API
從 REST 用戶端，請遵循下列指示：

1. 確定您擁有用戶端憑證 tooconnect toohello Azure 入口網站。 tooobtain 用戶端憑證，請依照下列中的 hello 步驟[How to： 下載和匯入發佈設定及訂用帳戶資訊](https://msdn.microsoft.com/library/dn385850.aspx)。 
2. 設定名稱為 x-ms-version，值為 2013-11-01 的標頭項目。
3. 以下列格式的 hello 傳送要求： https://management.core.windows.net/\<subscrition 識別碼\>/services/hostedservices/\<服務名稱\>？ 內嵌詳細資料 = true
4. 尋找 hello **HostName**每個項目**RoleInstance**項目。

> [!WARNING]
> 您也可以檢視雲端服務從 hello REST 呼叫回應 hello 內部網域尾碼，藉由檢查 hello **InternalDnsSuffix**項目，或藉由執行 ipconfig/全部從命令提示字元中的遠端桌面工作階段 (Windows)或從 SSH 終端機 (Linux) 執行 cat /etc/resolv.conf。
> 
> 

## <a name="modifying-a-hostname"></a>修改主機名稱
上傳已修改的服務組態檔，或從遠端桌面工作階段的 hello 電腦重新命名，您可以修改 hello 任何虛擬機器或角色執行個體的主機名稱。

## <a name="next-steps"></a>後續步驟
[名稱解析 (DNS)](virtual-networks-name-resolution-for-vms-and-role-instances.md)

[Azure 服務組態結構描述 (.cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710.aspx)

[Azure 虛擬網路組態結構描述](http://go.microsoft.com/fwlink/?LinkId=248093)

[使用網路組態檔指定 DNS 設定](virtual-networks-specifying-a-dns-settings-in-a-virtual-network-configuration-file.md)

