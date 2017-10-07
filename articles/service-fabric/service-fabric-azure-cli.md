---
title: "開始使用 Azure Service Fabric XPlat CLI aaaGetting"
description: "開始使用 Azure Service Fabric XPlat CLI"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: c3ec8ff3-3b78-420c-a7ea-0c5e443fb10e
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e4baa30536b4d8668d8efad301ed8210eb9c0335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-xplat-cli-toointeract-with-a-service-fabric-cluster"></a>Hello XPlat CLI toointeract 使用 Service Fabric 叢集

您可以互動 Linux 機器，在 Linux 上使用 hello XPlat CLI 從 Service Fabric 叢集。

hello 第一個步驟是取得 hello CLI hello 最新版本，從 hello git rep 並設定它在路徑中使用 hello 下列命令：

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

每個命令，它支援，您可以輸入 hello 名稱 hello 命令 tooobtain hello 說明該命令。
Hello 命令支援自動完成。 例如，hello 下列命令可讓您所有的 hello 應用程式命令的說明。 

```sh
 azure servicefabric application 
```

您可以為下列範例所示的 hello 進一步篩選 hello 說明 tooa 特定命令：

```sh
 azure servicefabric application  create
```

tooenable 的自動完成 hello CLI，執行下列命令的 hello:

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

下列命令的 hello 連接 toohello 叢集並顯示 hello hello 叢集中的節點：

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

toouse 具名參數，而且找出它們的是，您可以輸入-說明命令之後。 例如：

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

從機器連接 tooa 多電腦叢集時**也就是未叢集的一部分 hello**，使用下列命令的 hello:

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

取代為 hello PublicIPorFQDN 標記 hello 實際 IP 或 FQDN 適當。 從機器連接 tooa 多電腦叢集時**也就是叢集一部分的 hello**，使用下列命令的 hello:

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

您可以使用 PowerShell 或 CLI toointeract 與您的 Linux Service Fabric 叢集建立透過 hello Azure 入口網站。

> [!WARNING]
> 這些叢集不安全，因此，您可能會開啟一個方塊在 hello 叢集資訊清單中加入 hello 公用 IP 位址。

## <a name="using-hello-xplat-cli-tooconnect-tooa-service-fabric-cluster"></a>使用 hello XPlat CLI tooconnect tooa Service Fabric 叢集

下列 Azure CLI 命令的 hello 說明 tooconnect tooa 如何保護叢集。 hello 憑證詳細資料必須符合 hello 叢集節點上的憑證。

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

如果您的憑證的憑證授權單位 (Ca)，您會需要 tooadd hello-ca 憑證路徑參數，如下列範例中的 hello: 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

如果您有多個 Ca，請使用逗號做為 hello 分隔符號。

如果您在 hello 憑證的一般名稱不符合 hello 連接端點，您可以使用 hello 參數`--strict-ssl-false`toobypass hello 驗證，下列命令的 hello 中所示：

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

如果您想要 tooskip hello CA 驗證，您可以加入 hello-拒絕未經授權的 false 參數 hello 下列命令所示： 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

您連接之後，您應該能夠 toorun 與其他 CLI 命令 toointeract hello 叢集。

## <a name="deploying-your-service-fabric-application"></a>部署 Service Fabric 應用程式

執行下列命令 toocopy，註冊，並啟動 hello service fabric 應用程式的 hello:

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a>升級您的應用程式

hello 程序是類似 toohello [windows 處理序](service-fabric-application-upgrade-tutorial-powershell.md))。

從專案根目錄中建置、複製、註冊和建立您的應用程式。 如果您的應用程式執行個體的名稱為`fabric:/MySFApp`，hello 類型和 MySFApp，hello 命令應如下：

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

請變更 tooyour 應用程式，並重建 hello 修改服務的 hello。  更新 hello 修改服務的資訊清單檔案 (ServiceManifest.xml) 與 hello 更新版本的 hello 服務 （和程式碼或組態或視需要的資料）。 也具有 hello 更新的版本號碼 hello 應用程式中，修改 hello 應用程式資訊清單 (ApplicationManifest.xml) 和 hello 已修改的服務。  現在，複製並註冊您更新的應用程式，使用下列命令的 hello:

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

現在，您可以使用下列命令的 hello 啟動 hello 應用程式升級：

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

您現在可以監視使用 SFX hello 應用程式升級。 在幾分鐘的時間，hello 應用程式會有更新。 您也可以再試一次更新應用程式，但發生錯誤，並檢查服務網狀架構中的 hello 自動回復功能。

## <a name="converting-from-pfx-toopem-and-vice-versa"></a>轉換從 PFX tooPEM 反之亦然

您本機電腦 （具有 Windows 或 Linux） tooaccess 安全叢集中可能在不同的環境中，您可能需要 tooinstall 憑證。 例如，存取受保護的 Linux 叢集從 Windows 電腦，反之亦然時您可能需要 tooconvert 憑證從 PFX tooPEM，反之亦然。 

從 PEM 檔案 tooa PFX 檔案，下列命令使用 hello tooconvert:

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

從 PFX 檔案 tooa PEM 檔案，下列命令使用 hello tooconvert:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

請參閱太[OpenSSL 文件](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html)如需詳細資訊。

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a>疑難排解


### <a name="copying-of-hello-application-package-does-not-succeed"></a>未成功複製的 hello 應用程式套件

檢查是否已安裝 `openssh` 。 根據預設，Ubuntu 桌面不會安裝此軟體。 使用安裝 hello 下列命令：

```sh
sudo apt-get install openssh-server openssh-client**
```

如果 hello 問題持續發生，請嘗試停用的 PAM ssh 藉由變更 hello`sshd_config`檔案使用下列命令的 hello:

```sh
sudo vi /etc/ssh/sshd_config
#Change hello line with UsePAM toohello following: UsePAM no
sudo service sshd reload
```

如果 hello 問題持續發生，請嘗試 hello 日益增加的 ssh 工作階段藉由執行下列命令的 hello:

```sh
sudo vi /etc/ssh/sshd\_config
# Add hello following toolines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

使用金鑰的 ssh 驗證 （做為相對於 toopasswords) 尚不支援 （因為 hello 平台會使用 ssh toocopy 封裝），因此改為使用密碼驗證。

## <a name="next-steps"></a>後續步驟

[設定 hello 開發環境和部署 Service Fabric 應用程式 tooa Linux 叢集。](service-fabric-get-started-linux.md)

## <a name="related-articles"></a>相關文章

* [開始使用 Service Fabric 和 Azure CLI 2.0](service-fabric-azure-cli-2-0.md)
