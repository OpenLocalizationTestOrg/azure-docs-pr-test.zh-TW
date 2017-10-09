---
title: "aaaRed Hat 更新基礎結構 (RHUI) |Microsoft 文件"
description: "了解適用於 Microsoft Azure 中隨選 Red Hat Enterprise Linux 執行個體的 Red Hat Update Infrastructure (RHUI)"
services: virtual-machines-linux
documentationcenter: 
author: BorisB2015
manager: timlt
editor: 
ms.assetid: f495f1b4-ae24-46b9-8d26-c617ce3daf3a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: borisb
ms.openlocfilehash: cc244857104b25e4e61862c518db77e915e137ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a>適用於 Azure 中隨選 Red Hat Enterprise Linux VM 的 Red Hat Update Infrastructure (RHUI)
從 hello 隨 Red Hat Enterprise Linux (RHEL) 提供的映像在 Azure Marketplace 中建立的虛擬機器都已註冊的 tooaccess hello Red Hat 更新基礎結構 (RHUI) 部署在 Azure 中。  hello 隨 RHEL 執行個體具有存取 tooa 地區 yum 儲存機制和可以 tooreceive 累加式更新。

RHEL 執行個體中設定 hello yum 儲存機制清單，由 RHUI 管理、 佈建期間。 您不需要 toodo 任何額外的設定-執行`yum update`RHEL 執行個體準備好 tooget hello 最新的更新之後。

> [!NOTE]
> 在 2016 年 9 月部署更新的 Azure RHUI，並在 2017 年 1 月我們會啟動分階段的關機 hello 的較舊的 Azure RHUI。 如果您已在使用 hello RHEL 映像 （或其快照集） 從 2016 年 9 月或更新版本-可能不不需要任何動作。 不過，您會有較舊的快照集 Vm，如果其設定都必須更新不會中斷的存取 toohello Azure RHUI toobe。
> 

## <a name="rhui-azure-infrastructure-update"></a>RHUI Azure 基礎結構更新
自 2016 年 9 月起，Azure 會有一組新的 Red Hat Update Infrastructure (RHUI) 伺服器。 這些伺服器的部署將會透過 [Azure 流量管理員](https://azure.microsoft.com/services/traffic-manager/)執行，讓任何 VM (不論是哪個區域) 都可以使用單一端點 (rhui-1.microsoft.com)。 hello hello Azure Marketplace （張貼日期為 2016 年 9 月或更高版本） 點 toohello 新 Azure RHUI 伺服器中的新 RHEL 隨用隨付 」 (PAYG) 映像，並不需要任何額外的動作。

### <a name="determine-if-action-is-required"></a>判斷是否需要採取動作
如果您遇到連接 tooAzure RHUI 來自 Azure RHEL PAYG VM 的問題，請遵循下列步驟
1. 檢查 Azure RHUI 端點的 VM 組態

    如果核取`/etc/yum.repos.d/rh-cloud.repo`檔案也包含參考`rhui-[1-3].microsoft.com`中的 baseurl `[rhui-microsoft-azure-rhel*]` hello 檔案區段。 如果它是您使用 hello 新 Azure RHUI。

    如果它指向 tooa 位置以下列模式的 hello `mirrorlist.*cds[1-4].cloudapp.net` -hello 組態更新為必要項。

    如果您使用 hello 新設定，且仍然無法連線 tooAzure RHUI-檔案與 Microsoft 或 Red Hat 支援案例。

    > [!NOTE]
    > 存取 tooAzure 裝載 RHUI 是有限的 toohello Vm 內[Microsoft Azure Datacenter IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)。
    > 

2. 如果 hello 舊 Azure RHUI 仍然可以使用當您執行這項檢查，而您想讓 tooautomatically 更新 hello 組態時，請執行下列命令的 hello:

    `sudo yum update RHEL6`或`sudo yum update RHEL7`視 hello RHEL 系列版本而定。

3. 如果您無法再連接 toohello 舊 Azure RHUI，hello 下一節中所述的後續 hello 手動步驟。

4. 請確定 hello 來源映像/快照上的 tooupdate hello 組態會影響 VM 已佈建。

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a>分階段的關機的 hello 舊 Azure RHUI
在 hello hello 關閉舊的 Azure RHUI 我們限制，如下所示存取 tooit:

1. 進一步限制存取 (ACL) tooset tooit 已連接的 IP 位址。 可能的副作用： 如果您繼續使用 hello 舊 Azure RHUI-新的 Vm 可能無法 tooconnect tooit。 瀏覽關機/取消配置/啟動程序的 RHEL Vm 與動態 Ip 可能會收到新的 IP 和因此也無法啟動失敗 tooconnect toohello 舊 Azure RHUI

2. 關閉鏡像內容傳遞伺服器。 可能的副作用： 在我們關閉詳細 CDSes 會再看見`yum update`服務時間更多的逾時為止 hello 點時，您無法再連接 toohello 舊 Azure RHUI。

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a>hello 新 RHUI 內容傳遞伺服器 hello Ip 是
如果您使用網路組態 toofurther 限制 RHEL PAYG Vm 所傳來的存取，請確定允許下列 Ip hello `yum update` toowork 視您是在 hello 環境而定。 

```
# Azure Global
13.91.47.76
40.85.190.91
52.187.75.218
52.174.163.213

# Azure US Government
13.72.186.193

# Azure Germany
51.5.243.77
51.4.228.145
```

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a>手動更新程序 toouse hello 新 Azure RHUI 伺服器
（透過 curl) 下載 hello 公用金鑰簽章

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

請確認下載的 hello 金鑰

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

檢查 hello 輸出，確認`keyid`和`user ID packet`:

```bash
Version: GnuPG v1.4.7 (GNU/Linux)
:public key packet:
        version 4, algo 1, created 1446074508, expires 0
        pkey[0]: [2048 bits]
        pkey[1]: [17 bits]
        keyid: EB3E94ADBE1229CF
:user ID packet: "Microsoft (Release signing) <gpgsecurity@microsoft.com>"
:signature packet: algo 1, keyid EB3E94ADBE1229CF
        version 4, created 1446074508, md5len 0, sigclass 0x13
        digest algo 2, begin of digest 1a 9b
        hashed subpkt 2 len 4 (sig created 2015-10-28)
        hashed subpkt 27 len 1 (key flags: 03)
        hashed subpkt 11 len 5 (pref-sym-algos: 9 8 7 3 2)
        hashed subpkt 21 len 3 (pref-hash-algos: 2 8 3)
        hashed subpkt 22 len 2 (pref-zip-algos: 2 1)
        hashed subpkt 30 len 1 (features: 01)
        hashed subpkt 23 len 1 (key server preferences: 80)
        subpkt 16 len 8 (issuer key ID EB3E94ADBE1229CF)
        data: [2047 bits]
```

安裝 hello 公開金鑰

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

下載、驗證及安裝用戶端 RPM

下載：適用於 RHEL 6

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

適用於 RHEL 7

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

驗證：

```bash
rpm -Kv azureclient.rpm
```

檢查輸出中的簽章的 hello 封裝是 [確定]

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

安裝 hello RPM

```bash
sudo rpm -U azureclient.rpm
```

完成時，請確認您可以存取 Azure RHUI 表單 hello VM

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a>全部的一個指令碼自動化 hello 前工作
使用下列指令碼以更新受影響的 Vm toohello 新 Azure RHUI 伺服器的所需的 tooautomate hello 工作 hello。

```sh
# Download key
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 

# Validate key
if ! gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release | grep -q "keyid: EB3E94ADBE1229CF"; then
    echo "Keyfile azure.asc NOT valid. Exiting."
    exit 1
fi

# Install Key
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release

# Download RPM package
if grep -q "release 7" /etc/redhat-release; then
    ver=7
elif  grep -q "release 6" /etc/redhat-release; then
    ver=6
else
    echo "Version not supported, exiting"
    exit 1
fi

url=https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel$ver/rhui-azure-rhel$ver-2.0-2.noarch.rpm
curl -o azureclient.rpm "$url"

# Verify package
if ! rpm -Kv azureclient.rpm | grep -q "key ID be1229cf: OK"; then
    echo "RPM failed validation ($url)"
    exit 1
fi

# Install package
sudo rpm -U azureclient.rpm
```

## <a name="rhui-overview"></a>RHUI 概觀
[Red Hat 更新基礎結構](https://access.redhat.com/products/red-hat-update-infrastructure)提供 Red Hat 認證雲端提供者所裝載的 Red Hat Enterprise Linux 雲端執行個體可高度擴充的方案 toomanage yum 儲存機制內容。 依據 hello 上游 Pulp 專案 RHUI 允許雲端提供者 toolocally 鏡像 Red Hat 裝載的儲存機制內容，其本身的內容，以建立自訂儲存機制，並進行這些儲存機制可用 tooa 大群使用者透過負載平衡內容傳遞系統。

## <a name="regions-where-rhui-is-available"></a>可以使用 RHUI 的區域
在所有可使用 RHEL 隨選映像的地區，皆可使用 RHUI。 它目前包含在 hello 上所列的所有公用區域[Azure 狀態儀表板](https://azure.microsoft.com/status/)頁面上，Azure 美國政府和 Azure 德國區域。 從 RHEL 隨選映像佈建之 VM 的 RHUI 存取包含在其價格中。 我們展開 RHEL 隨可用性 hello 未來在其他地區/國家雲端可用性將會更新。

> [!NOTE]
> 存取 tooAzure 裝載 RHUI 是有限的 toohello Vm 內[Microsoft Azure Datacenter IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)。
> 
> 

## <a name="get-updates-from-another-update-repository"></a>從其他更新儲存機制取得更新
如果您需要從不同的更新儲存機制 （而不是 Azure 託管 RHUI) tooget 更新時，首先您需要 toounregister RHUI 從您的執行個體。 則您需要 toore 登錄其與 hello 所需的更新基礎結構 （例如 Red Hat 附屬或 Red Hat 客戶入口網站 CDN）。 您將需要這些服務的適當 Red Hat 訂用帳戶，而且必須註冊 [Azure 中的 Red Hat 雲端存取](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure)。

toounregister RHUI 和重新登錄 tooyour 更新基礎結構，請遵循下列步驟：

1. 編輯 /etc/yum.repos.d/rh-cloud.repo 並變更所有`enabled=1`太`enabled=0`。 例如：
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. 編輯 /etc/yum/pluginconf.d/rhnplugin.conf 並變更`enabled=0`太`enabled=1`。
3. 然後向 hello 所需的基礎結構，例如 Red Hat 客戶入口網站。 請遵循解決方案指南 Red Hat[如何 tooregister 和訂閱系統 toohello Red Hat 客戶入口網站](https://access.redhat.com/solutions/253273)。

> [!NOTE]
> 存取 toohello Azure 託管 RHUI 隨附於 hello RHEL 隨用隨付 」 (PAYG) 映像的價格。 取消登錄從 hello Azure 託管 RHUI PAYG RHEL VM 不會轉換成提到您-擁有的授權 (BYOL) 型別 VM hello 虛擬機器。 如果您註冊 hello 相同的 VM 與其他來源的更新您可能會產生 double 費用： 第一次 Azure RHEL 軟體費用，和 hello Red Hat 訂閱的第二次。 
> 
> 建立及部署您自己 （BYOL 型別） 映像中所述，如果您以一致的方式需要 toouse 要考慮 Azure 託管 RHUI 以外的更新基礎結構[建立及上傳 Red Hat 基礎 Azure 的虛擬機器](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)發行項。
> 

## <a name="next-steps"></a>後續步驟
從 Azure Marketplace 隨用隨付映像和運用 Azure 託管 RHUI Red Hat Enterprise Linux VM toocreate 太移[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/)。 您將會無法 toouse `yum update` RHEL 執行個體沒有任何額外的設定中。

