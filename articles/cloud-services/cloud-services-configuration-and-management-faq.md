---
title: "aaaConfiguration 與管理的問題，Microsoft Azure 雲端服務的常見問題集 |Microsoft 文件"
description: "本文列出 hello 設定及管理 Microsoft Azure 雲端服務的相關常見問題集。"
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 62ece142ac0ef5d45081cab333375b1a0a8f0ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Azure 雲端服務之設定和管理問題：常見問題集 (FAQ)

本文包含 [Microsoft Azure 雲端服務](https://azure.microsoft.com/services/cloud-services)之設定和管理問題的相關常見問題集。 此外，您也可以參考 hello[雲端服務 VM 大小頁面](cloud-services-sizes-specs.md)大小資訊。

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="how-do-i-add-nosniff-toomy-website"></a>如何新增 「 nosniff"toomy 網站？
tooprevent 用戶端從探測 hello MIME 類型，新增設定，在您*web.config*檔案。

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

您也可以在 IIS 中將此加入為設定。 使用 hello 下列命令以 hello[常見的啟動工作](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe)發行項。

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

## <a name="how-do-i-customize-iis-for-a-web-role"></a>如何自訂 Web 角色的 IIS？
使用 hello IIS 啟動指令碼從 hello[常見的啟動工作](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe)發行項。

## <a name="i-cannot-scale-beyond-x-instances"></a>我不能調整超過 X 個執行個體
您的 Azure 訂閱 hello 您可以使用的核心數目的上限。 調整將無法運作如果您已使用所有可用的 hello 核心。 例如，如果您有 100 個核心的限制，這表示您的雲端服務可以有 100 個 A1 大小的虛擬機器執行個體，或 50 個 A2 大小的虛擬機器執行個體。

## <a name="how-can-i-implement-role-based-access-for-cloud-services"></a>如何實作雲端服務的角色型存取？
雲端服務不支援 hello 角色型存取控制 (RBAC) 模型，因為它不是以基礎的 Azure 資源管理員服務。

請參閱 [Azure RBAC 與傳統訂用帳戶系統管理員](../active-directory/role-based-access-control-what-is.md#azure-rbac-vs-classic-subscription-administrators)。

## <a name="how-do-i-set-hello-idle-timeout-for-azure-load-balancer"></a>如何設定 Azure 負載平衡器的 hello 閒置逾時？
您可以指定 hello 逾時，在您的服務定義 (csdef) 檔，就像這樣：

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="mgVS2015Worker" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10100"   idleTimeoutInMinutes="30" />
    </Endpoints>
  </WorkerRole>
```
如需詳細資訊，請參閱[新增：Azure Load Balancer 的可設定閒置逾時](https://azure.microsoft.com/blog/new-configurable-idle-timeout-for-azure-load-balancer/)。

## <a name="can-microsoft-internal-engineers-rdp-toocloud-service-instances-without-permission"></a>可以在 Microsoft 內部工程師 RDP toocloud 服務執行個體沒有權限嗎？
Microsoft 如下所示嚴格的程序，將不允許內部工程師 tooRDP 到您的雲端服務，而不會從 hello 擁有者或其被指派寫入權限 （電子郵件或其他撰寫的通訊）。

## <a name="why-is-hello-certificate-chain-of-my-cloud-service-ssl-certificate-incomplete"></a>為什麼我雲端服務的 SSL 憑證的 hello 憑證鏈結不完整的？
我們建議客戶安裝 hello 整個憑證鏈結 （分葉憑證、 中繼憑證，包含憑證和根憑證） 而非只 hello 分葉憑證。 當您安裝只 hello 分葉憑證時，您依賴 Windows toobuild hello 憑證鏈結查核 hello CTL。 如果間歇性的網路或 DNS 問題發生在 Azure 或 Windows Update 時，Windows 會嘗試 toovalidate hello 憑證，hello 憑證可能會視為無效。 藉由安裝 hello 整個憑證鏈結，可以避免這個問題。 hello 在部落格[如何 tooinstall 鏈結的 SSL 憑證](https://blogs.msdn.microsoft.com/azuredevsupport/2010/02/24/how-to-install-a-chained-ssl-certificate/)示範如何 toodo 這。

## <a name="how-do-i-associate-a-static-ip-address-toomy-cloud-service"></a>如何將關聯的靜態 IP 位址 toomy 雲端服務？
tooset 的靜態 IP 位址，您需要 toocreate 保留 IP。 這個保留的 IP 可以是相關聯的 tooa 新雲端服務或 tooan 現有部署。 請參閱下列文件以取得詳細資料的 hello:
* [如何 toocreate 保留的 IP 位址](../virtual-network/virtual-networks-reserved-public-ip.md#manage-reserved-vips)
* [保留現有的雲端服務的 hello IP 位址](../virtual-network/virtual-networks-reserved-public-ip.md#reserve-the-ip-address-of-an-existing-cloud-service)
* [關聯保留的 IP tooa 新的雲端服務](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-new-cloud-service)
* [執行部署的保留的 IP tooa 產生關聯](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-running-deployment)
* [使用服務組態檔相關聯的保留的 IP tooa 雲端服務](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file)

## <a name="what-is-hello-quota-limit-for-my-cloud-service"></a>什麼是我的雲端服務的 hello 配額限制？
請參閱[特定服務的限制](../azure-subscription-service-limits.md#subscription-limits)。

## <a name="why-does-hello-drive-on-my-cloud-service-vm-show-very-little-free-disk-space"></a>為什麼 hello 我 VM 的雲端服務上的磁碟機顯示非常小的可用磁碟空間？
這是預期的行為，而不造成任何問題 tooyour 應用程式。 日誌記錄已開啟的 hello %uproot%Azure PaaS Vm 基本上會消耗 double hello 數量的檔案通常會佔用的空間中的磁碟機。 不過有幾件事 toobe 留意，基本上是將這變成非問題。

hello %approot%磁碟機大小計算為 <.cspkg + 最大日誌大小的大小 > + 邊界的可用空間，或 1.5 GB，兩者取其較大。 hello VM 大小並無任何影響這個計算方式。 （hello VM 大小只影響 hello hello 暫存 c： 磁碟機大小）。 

它是不支援的 toowrite toohello %approot%磁碟機。 如果您正在撰寫 toohello Azure VM，您必須這樣暫存 LocalStorage 資源中 (或其他選項，例如 Blob 儲存體，Azure 檔案等。)。 因此 hello hello %approot%資料夾上的可用空間數量沒有任何意義。 如果您不確定，如果您的應用程式正在寫入 toohello %approot%磁碟機，您一律可以讓您的服務為幾天執行，而且 「 之前 」 和 「 之後 」 大小，然後比較 hello。 

Azure 不會寫入任何項目 toohello %approot%磁碟機。 一旦 hello VHD 建立從.cspkg 並掛接至 hello Azure VM，hello 唯一可能會撰寫 toothis 磁碟機是您的應用程式。 

hello 筆記本設定是不可設定的因此您無法將它關閉。

## <a name="what-are-hello-features-and-capabilities-that-azure-basic-ipsids-and-ddos-provides"></a>Hello 特色與功能，提供 Azure 的基本 IP/識別碼和 DDOS 為何？
Azure 擁有 IP/ID 中的資料中心實體伺服器 toodefend 面臨的威脅。 此外，客戶可以部署第三方安全性解決方案，例如 Web 應用程式防火牆、網路防火牆、反惡意程式碼軟體、入侵偵測、預防系統 (IDS/IPS) 等等。 如需詳細資訊，請參閱[保護您的資料和資產，以及符合全域安全性標準](https://www.microsoft.com/en-us/trustcenter/Security/AzureSecurity)。

Microsoft 會持續監視伺服器、 網路和應用程式 toodetect 威脅。 Azure 的 multipronged 的威脅管理方法就是使用入侵偵測，分散式的阻絕服務 (DDoS) 攻擊的防護，徹底測試、 行為分析，異常偵測和機器學習 tooconstantly 加強其防禦並降低風險。 適用於 Azure 保護的 Azure 雲端服務和虛擬機器的 Microsoft Antimalware。 您有 hello 選項 toodeploy 協力廠商的安全性解決方案此外，例如 web 應用程式防火牆、 網路防火牆、 反惡意程式碼、 入侵偵測與預防系統 (識別碼/IP) 等等。

## <a name="why-does-iis-stop-writing-toohello-log-directory"></a>IIS 為何停止寫入 toohello 記錄檔目錄？
您已耗盡 hello 撰寫 toohello 記錄檔目錄的本機儲存體配額。 若要修正此問題，您可以執行下列三個項目的其中一項：
* Iis 中啟用診斷，診斷 hello 定期移 tooblob 儲存體。
* 手動移除 hello 記錄目錄的記錄檔。
* 增加本機資源的配額限制。

如需詳細資訊，請參閱下列文件的 hello:
* [在 Azure 儲存體中儲存和檢視診斷資料](cloud-services-dotnet-diagnostics-storage.md)
* [IIS 記錄會停止在雲端服務中寫入](https://blogs.msdn.microsoft.com/cie/2013/12/21/iis-logs-stops-writing-in-cloud-service/)

## <a name="what-is-hello-purpose-of-hello-windows-azure-tools-encryption-certificate-for-extensions"></a>Hello"Windows Azure Tools 加密憑證的延伸模組 」 的目的是 hello 的什麼？
擴充功能加入 toohello 雲端服務時，會自動建立這些憑證。 大多數情況下，這是 hello wad 的資料延伸模組或 hello RDP 延伸模組，但它可能是其他人，例如 hello 反惡意程式碼或記錄檔收集器延伸模組。 這些憑證只用於加密和解密 hello hello 擴充功能私用組態。 永遠不會檢查 hello 到期日，因此並不重要 hello 憑證已過期。 

您可以忽略這些憑證。 如果您想要清除 hello 憑證，您可以嘗試刪除全部。 Azure 將會擲回錯誤 toodelete 再試一次，如果正在使用中的憑證。

## <a name="how-can-i-generate-a-certificate-signing-request-csr-without-rdp-ing-in-toohello-instance"></a>如何產生憑證簽署要求 (CSR) 沒有"RDP ing"toohello 執行個體中？
請參閱下列指引文件的 hello:

>[使用 Windows Azure 網站 (WAWS) 取得要使用的憑證](https://azure.microsoft.com/blog/obtaining-a-certificate-for-use-with-windows-azure-web-sites-waws/)

請注意，CSR 只是一個文字檔。 它沒有從 hello 機器建立 toobe 其中 hello 將最終會使用憑證。 雖然這份文件會寫入應用程式服務，hello CSR 建立為泛型，也適用於雲端服務。
