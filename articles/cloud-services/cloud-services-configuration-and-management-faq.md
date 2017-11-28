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
# <a name="configuration-and-management-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a><span data-ttu-id="5673b-103">Azure 雲端服務之設定和管理問題：常見問題集 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="5673b-103">Configuration and management issues for Azure Cloud Services: Frequently asked questions (FAQs)</span></span>

<span data-ttu-id="5673b-104">本文包含 [Microsoft Azure 雲端服務](https://azure.microsoft.com/services/cloud-services)之設定和管理問題的相關常見問題集。</span><span class="sxs-lookup"><span data-stu-id="5673b-104">This article includes frequently asked questions about configuration and management issues for [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services).</span></span> <span data-ttu-id="5673b-105">此外，您也可以參考 hello[雲端服務 VM 大小頁面](cloud-services-sizes-specs.md)大小資訊。</span><span class="sxs-lookup"><span data-stu-id="5673b-105">You can also consult hello [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="how-do-i-add-nosniff-toomy-website"></a><span data-ttu-id="5673b-106">如何新增 「 nosniff"toomy 網站？</span><span class="sxs-lookup"><span data-stu-id="5673b-106">How do I add "nosniff" toomy website?</span></span>
<span data-ttu-id="5673b-107">tooprevent 用戶端從探測 hello MIME 類型，新增設定，在您*web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="5673b-107">tooprevent clients from sniffing hello MIME types, add a setting in your *web.config* file.</span></span>

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

<span data-ttu-id="5673b-108">您也可以在 IIS 中將此加入為設定。</span><span class="sxs-lookup"><span data-stu-id="5673b-108">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="5673b-109">使用 hello 下列命令以 hello[常見的啟動工作](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe)發行項。</span><span class="sxs-lookup"><span data-stu-id="5673b-109">Use hello following command with hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

## <a name="how-do-i-customize-iis-for-a-web-role"></a><span data-ttu-id="5673b-110">如何自訂 Web 角色的 IIS？</span><span class="sxs-lookup"><span data-stu-id="5673b-110">How do I customize IIS for a web role?</span></span>
<span data-ttu-id="5673b-111">使用 hello IIS 啟動指令碼從 hello[常見的啟動工作](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe)發行項。</span><span class="sxs-lookup"><span data-stu-id="5673b-111">Use hello IIS startup script from hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="5673b-112">我不能調整超過 X 個執行個體</span><span class="sxs-lookup"><span data-stu-id="5673b-112">I cannot scale beyond X instances</span></span>
<span data-ttu-id="5673b-113">您的 Azure 訂閱 hello 您可以使用的核心數目的上限。</span><span class="sxs-lookup"><span data-stu-id="5673b-113">Your Azure Subscription has a limit on hello number of cores you can use.</span></span> <span data-ttu-id="5673b-114">調整將無法運作如果您已使用所有可用的 hello 核心。</span><span class="sxs-lookup"><span data-stu-id="5673b-114">Scaling will not work if you have used all hello cores available.</span></span> <span data-ttu-id="5673b-115">例如，如果您有 100 個核心的限制，這表示您的雲端服務可以有 100 個 A1 大小的虛擬機器執行個體，或 50 個 A2 大小的虛擬機器執行個體。</span><span class="sxs-lookup"><span data-stu-id="5673b-115">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="how-can-i-implement-role-based-access-for-cloud-services"></a><span data-ttu-id="5673b-116">如何實作雲端服務的角色型存取？</span><span class="sxs-lookup"><span data-stu-id="5673b-116">How can I implement Role-Based Access for Cloud Services?</span></span>
<span data-ttu-id="5673b-117">雲端服務不支援 hello 角色型存取控制 (RBAC) 模型，因為它不是以基礎的 Azure 資源管理員服務。</span><span class="sxs-lookup"><span data-stu-id="5673b-117">Cloud Services doesn't support hello Role-Based Access Control (RBAC) model, as it's not an Azure Resource Manager based service.</span></span>

<span data-ttu-id="5673b-118">請參閱 [Azure RBAC 與傳統訂用帳戶系統管理員](../active-directory/role-based-access-control-what-is.md#azure-rbac-vs-classic-subscription-administrators)。</span><span class="sxs-lookup"><span data-stu-id="5673b-118">See [Azure RBAC vs. classic subscription administrators](../active-directory/role-based-access-control-what-is.md#azure-rbac-vs-classic-subscription-administrators).</span></span>

## <a name="how-do-i-set-hello-idle-timeout-for-azure-load-balancer"></a><span data-ttu-id="5673b-119">如何設定 Azure 負載平衡器的 hello 閒置逾時？</span><span class="sxs-lookup"><span data-stu-id="5673b-119">How do I set hello idle timeout for Azure load balancer?</span></span>
<span data-ttu-id="5673b-120">您可以指定 hello 逾時，在您的服務定義 (csdef) 檔，就像這樣：</span><span class="sxs-lookup"><span data-stu-id="5673b-120">You can specify hello timeout in your service definition (csdef) file like this:</span></span>

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
<span data-ttu-id="5673b-121">如需詳細資訊，請參閱[新增：Azure Load Balancer 的可設定閒置逾時](https://azure.microsoft.com/blog/new-configurable-idle-timeout-for-azure-load-balancer/)。</span><span class="sxs-lookup"><span data-stu-id="5673b-121">See [New: Configurable Idle Timeout for Azure Load Balancer](https://azure.microsoft.com/blog/new-configurable-idle-timeout-for-azure-load-balancer/) for more information.</span></span>

## <a name="can-microsoft-internal-engineers-rdp-toocloud-service-instances-without-permission"></a><span data-ttu-id="5673b-122">可以在 Microsoft 內部工程師 RDP toocloud 服務執行個體沒有權限嗎？</span><span class="sxs-lookup"><span data-stu-id="5673b-122">Can Microsoft internal engineers RDP toocloud service instances without permission?</span></span>
<span data-ttu-id="5673b-123">Microsoft 如下所示嚴格的程序，將不允許內部工程師 tooRDP 到您的雲端服務，而不會從 hello 擁有者或其被指派寫入權限 （電子郵件或其他撰寫的通訊）。</span><span class="sxs-lookup"><span data-stu-id="5673b-123">Microsoft follows a strict process that will not allow internal engineers tooRDP into your cloud service without written permission (email or other written communication) from hello owner or their designee.</span></span>

## <a name="why-is-hello-certificate-chain-of-my-cloud-service-ssl-certificate-incomplete"></a><span data-ttu-id="5673b-124">為什麼我雲端服務的 SSL 憑證的 hello 憑證鏈結不完整的？</span><span class="sxs-lookup"><span data-stu-id="5673b-124">Why is hello certificate chain of my cloud service SSL certificate incomplete?</span></span>
<span data-ttu-id="5673b-125">我們建議客戶安裝 hello 整個憑證鏈結 （分葉憑證、 中繼憑證，包含憑證和根憑證） 而非只 hello 分葉憑證。</span><span class="sxs-lookup"><span data-stu-id="5673b-125">We recommend that customers install hello full certificate chain (leaf cert, intermediate certs, and root cert) instead of just hello leaf certificate.</span></span> <span data-ttu-id="5673b-126">當您安裝只 hello 分葉憑證時，您依賴 Windows toobuild hello 憑證鏈結查核 hello CTL。</span><span class="sxs-lookup"><span data-stu-id="5673b-126">When you install just hello leaf certificate, you rely on Windows toobuild hello certificate chain by walking hello CTL.</span></span> <span data-ttu-id="5673b-127">如果間歇性的網路或 DNS 問題發生在 Azure 或 Windows Update 時，Windows 會嘗試 toovalidate hello 憑證，hello 憑證可能會視為無效。</span><span class="sxs-lookup"><span data-stu-id="5673b-127">If intermittent network or DNS issues occur in Azure or Windows Update when Windows is trying toovalidate hello certificate, hello certificate may be considered invalid.</span></span> <span data-ttu-id="5673b-128">藉由安裝 hello 整個憑證鏈結，可以避免這個問題。</span><span class="sxs-lookup"><span data-stu-id="5673b-128">By installing hello full certificate chain, this problem can be avoided.</span></span> <span data-ttu-id="5673b-129">hello 在部落格[如何 tooinstall 鏈結的 SSL 憑證](https://blogs.msdn.microsoft.com/azuredevsupport/2010/02/24/how-to-install-a-chained-ssl-certificate/)示範如何 toodo 這。</span><span class="sxs-lookup"><span data-stu-id="5673b-129">hello blog at [How tooinstall a chained SSL certificate](https://blogs.msdn.microsoft.com/azuredevsupport/2010/02/24/how-to-install-a-chained-ssl-certificate/) shows how toodo this.</span></span>

## <a name="how-do-i-associate-a-static-ip-address-toomy-cloud-service"></a><span data-ttu-id="5673b-130">如何將關聯的靜態 IP 位址 toomy 雲端服務？</span><span class="sxs-lookup"><span data-stu-id="5673b-130">How do I associate a static IP address toomy cloud service?</span></span>
<span data-ttu-id="5673b-131">tooset 的靜態 IP 位址，您需要 toocreate 保留 IP。</span><span class="sxs-lookup"><span data-stu-id="5673b-131">tooset up a static IP address, you need toocreate a reserved IP.</span></span> <span data-ttu-id="5673b-132">這個保留的 IP 可以是相關聯的 tooa 新雲端服務或 tooan 現有部署。</span><span class="sxs-lookup"><span data-stu-id="5673b-132">This reserved IP can be associated tooa new cloud service or tooan existing deployment.</span></span> <span data-ttu-id="5673b-133">請參閱下列文件以取得詳細資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="5673b-133">See hello following documents for details:</span></span>
* [<span data-ttu-id="5673b-134">如何 toocreate 保留的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5673b-134">How toocreate a reserved IP address</span></span>](../virtual-network/virtual-networks-reserved-public-ip.md#manage-reserved-vips)
* [<span data-ttu-id="5673b-135">保留現有的雲端服務的 hello IP 位址</span><span class="sxs-lookup"><span data-stu-id="5673b-135">Reserve hello IP address of an existing cloud service</span></span>](../virtual-network/virtual-networks-reserved-public-ip.md#reserve-the-ip-address-of-an-existing-cloud-service)
* [<span data-ttu-id="5673b-136">關聯保留的 IP tooa 新的雲端服務</span><span class="sxs-lookup"><span data-stu-id="5673b-136">Associate a reserved IP tooa new cloud service</span></span>](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-new-cloud-service)
* [<span data-ttu-id="5673b-137">執行部署的保留的 IP tooa 產生關聯</span><span class="sxs-lookup"><span data-stu-id="5673b-137">Associate a reserved IP tooa running deployment</span></span>](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-running-deployment)
* [<span data-ttu-id="5673b-138">使用服務組態檔相關聯的保留的 IP tooa 雲端服務</span><span class="sxs-lookup"><span data-stu-id="5673b-138">Associate a reserved IP tooa cloud service by using a service configuration file</span></span>](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file)

## <a name="what-is-hello-quota-limit-for-my-cloud-service"></a><span data-ttu-id="5673b-139">什麼是我的雲端服務的 hello 配額限制？</span><span class="sxs-lookup"><span data-stu-id="5673b-139">What is hello quota limit for my cloud service?</span></span>
<span data-ttu-id="5673b-140">請參閱[特定服務的限制](../azure-subscription-service-limits.md#subscription-limits)。</span><span class="sxs-lookup"><span data-stu-id="5673b-140">See [Service-specific limits](../azure-subscription-service-limits.md#subscription-limits).</span></span>

## <a name="why-does-hello-drive-on-my-cloud-service-vm-show-very-little-free-disk-space"></a><span data-ttu-id="5673b-141">為什麼 hello 我 VM 的雲端服務上的磁碟機顯示非常小的可用磁碟空間？</span><span class="sxs-lookup"><span data-stu-id="5673b-141">Why does hello drive on my cloud service VM show very little free disk space?</span></span>
<span data-ttu-id="5673b-142">這是預期的行為，而不造成任何問題 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5673b-142">This is expected behavior, and it shouldn't cause any issue tooyour application.</span></span> <span data-ttu-id="5673b-143">日誌記錄已開啟的 hello %uproot%Azure PaaS Vm 基本上會消耗 double hello 數量的檔案通常會佔用的空間中的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="5673b-143">Journaling is turned on for hello %uproot% drive in Azure PaaS VMs, which essentially consumes double hello amount of space that files normally take up.</span></span> <span data-ttu-id="5673b-144">不過有幾件事 toobe 留意，基本上是將這變成非問題。</span><span class="sxs-lookup"><span data-stu-id="5673b-144">However there are several things toobe aware of that essentially turn this into a non-issue.</span></span>

<span data-ttu-id="5673b-145">hello %approot%磁碟機大小計算為 <.cspkg + 最大日誌大小的大小 > + 邊界的可用空間，或 1.5 GB，兩者取其較大。</span><span class="sxs-lookup"><span data-stu-id="5673b-145">hello %approot% drive size is calculated as <size of .cspkg + max journal size + a margin of free space>, or 1.5 GB, whichever is larger.</span></span> <span data-ttu-id="5673b-146">hello VM 大小並無任何影響這個計算方式。</span><span class="sxs-lookup"><span data-stu-id="5673b-146">hello size of your VM has no bearing on this calculation.</span></span> <span data-ttu-id="5673b-147">（hello VM 大小只影響 hello hello 暫存 c： 磁碟機大小）。</span><span class="sxs-lookup"><span data-stu-id="5673b-147">(hello VM size only affects hello size of hello temporary C: drive.)</span></span> 

<span data-ttu-id="5673b-148">它是不支援的 toowrite toohello %approot%磁碟機。</span><span class="sxs-lookup"><span data-stu-id="5673b-148">It is unsupported toowrite toohello %approot% drive.</span></span> <span data-ttu-id="5673b-149">如果您正在撰寫 toohello Azure VM，您必須這樣暫存 LocalStorage 資源中 (或其他選項，例如 Blob 儲存體，Azure 檔案等。)。</span><span class="sxs-lookup"><span data-stu-id="5673b-149">If you are writing toohello Azure VM, you must do so in a temporary LocalStorage resource (or other option, such as Blob storage, Azure Files, etc.).</span></span> <span data-ttu-id="5673b-150">因此 hello hello %approot%資料夾上的可用空間數量沒有任何意義。</span><span class="sxs-lookup"><span data-stu-id="5673b-150">So hello amount of free space on hello %approot% folder is not meaningful.</span></span> <span data-ttu-id="5673b-151">如果您不確定，如果您的應用程式正在寫入 toohello %approot%磁碟機，您一律可以讓您的服務為幾天執行，而且 「 之前 」 和 「 之後 」 大小，然後比較 hello。</span><span class="sxs-lookup"><span data-stu-id="5673b-151">If you are not sure if your application is writing toohello %approot% drive, you can always let your service run for a few days and then compare hello "before" and "after" sizes.</span></span> 

<span data-ttu-id="5673b-152">Azure 不會寫入任何項目 toohello %approot%磁碟機。</span><span class="sxs-lookup"><span data-stu-id="5673b-152">Azure will not write anything toohello %approot% drive.</span></span> <span data-ttu-id="5673b-153">一旦 hello VHD 建立從.cspkg 並掛接至 hello Azure VM，hello 唯一可能會撰寫 toothis 磁碟機是您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5673b-153">Once hello VHD is created from your .cspkg and mounted into hello Azure VM, hello only thing that might write toothis drive is your application.</span></span> 

<span data-ttu-id="5673b-154">hello 筆記本設定是不可設定的因此您無法將它關閉。</span><span class="sxs-lookup"><span data-stu-id="5673b-154">hello journal settings are non-configurable, so you can't turn it off.</span></span>

## <a name="what-are-hello-features-and-capabilities-that-azure-basic-ipsids-and-ddos-provides"></a><span data-ttu-id="5673b-155">Hello 特色與功能，提供 Azure 的基本 IP/識別碼和 DDOS 為何？</span><span class="sxs-lookup"><span data-stu-id="5673b-155">What are hello features and capabilities that Azure basic IPS/IDS and DDOS provides?</span></span>
<span data-ttu-id="5673b-156">Azure 擁有 IP/ID 中的資料中心實體伺服器 toodefend 面臨的威脅。</span><span class="sxs-lookup"><span data-stu-id="5673b-156">Azure has IPS/IDS in datacenter physical servers toodefend against threats.</span></span> <span data-ttu-id="5673b-157">此外，客戶可以部署第三方安全性解決方案，例如 Web 應用程式防火牆、網路防火牆、反惡意程式碼軟體、入侵偵測、預防系統 (IDS/IPS) 等等。</span><span class="sxs-lookup"><span data-stu-id="5673b-157">In addition, customers can deploy third-party security solutions, such as web application firewalls, network firewalls, antimalware, intrusion detection, prevention systems (IDS/IPS), and more.</span></span> <span data-ttu-id="5673b-158">如需詳細資訊，請參閱[保護您的資料和資產，以及符合全域安全性標準](https://www.microsoft.com/en-us/trustcenter/Security/AzureSecurity)。</span><span class="sxs-lookup"><span data-stu-id="5673b-158">For more information, see [Protect your data and assets and comply with global security standards](https://www.microsoft.com/en-us/trustcenter/Security/AzureSecurity).</span></span>

<span data-ttu-id="5673b-159">Microsoft 會持續監視伺服器、 網路和應用程式 toodetect 威脅。</span><span class="sxs-lookup"><span data-stu-id="5673b-159">Microsoft continuously monitors servers, networks, and applications toodetect threats.</span></span> <span data-ttu-id="5673b-160">Azure 的 multipronged 的威脅管理方法就是使用入侵偵測，分散式的阻絕服務 (DDoS) 攻擊的防護，徹底測試、 行為分析，異常偵測和機器學習 tooconstantly 加強其防禦並降低風險。</span><span class="sxs-lookup"><span data-stu-id="5673b-160">Azure's multipronged threat-management approach uses intrusion detection, distributed denial-of-service (DDoS) attack prevention, penetration testing, behavioral analytics, anomaly detection, and machine learning tooconstantly strengthen its defense and reduce risks.</span></span> <span data-ttu-id="5673b-161">適用於 Azure 保護的 Azure 雲端服務和虛擬機器的 Microsoft Antimalware。</span><span class="sxs-lookup"><span data-stu-id="5673b-161">Microsoft Antimalware for Azure protects Azure cloud services and virtual machines.</span></span> <span data-ttu-id="5673b-162">您有 hello 選項 toodeploy 協力廠商的安全性解決方案此外，例如 web 應用程式防火牆、 網路防火牆、 反惡意程式碼、 入侵偵測與預防系統 (識別碼/IP) 等等。</span><span class="sxs-lookup"><span data-stu-id="5673b-162">You have hello option toodeploy third-party security solutions in addition, such as web application fire walls, network firewalls, antimalware, intrusion detection and prevention systems (IDS/IPS), and more.</span></span>

## <a name="why-does-iis-stop-writing-toohello-log-directory"></a><span data-ttu-id="5673b-163">IIS 為何停止寫入 toohello 記錄檔目錄？</span><span class="sxs-lookup"><span data-stu-id="5673b-163">Why does IIS stop writing toohello log directory?</span></span>
<span data-ttu-id="5673b-164">您已耗盡 hello 撰寫 toohello 記錄檔目錄的本機儲存體配額。</span><span class="sxs-lookup"><span data-stu-id="5673b-164">You have exhausted hello local storage quota for writing toohello log directory.</span></span><span data-ttu-id="5673b-165"> 若要修正此問題，您可以執行下列三個項目的其中一項：</span><span class="sxs-lookup"><span data-stu-id="5673b-165"> To correct this, you can do one of three things:</span></span>
* <span data-ttu-id="5673b-166">Iis 中啟用診斷，診斷 hello 定期移 tooblob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5673b-166">Enable diagnostics for IIS and have hello diagnostics periodically moved tooblob storage.</span></span>
* <span data-ttu-id="5673b-167">手動移除 hello 記錄目錄的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5673b-167">Manually remove log files from hello logging directory.</span></span>
* <span data-ttu-id="5673b-168">增加本機資源的配額限制。</span><span class="sxs-lookup"><span data-stu-id="5673b-168">Increase quota limit for local resources.</span></span>

<span data-ttu-id="5673b-169">如需詳細資訊，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="5673b-169">For more information, see hello following documents:</span></span>
* [<span data-ttu-id="5673b-170">在 Azure 儲存體中儲存和檢視診斷資料</span><span class="sxs-lookup"><span data-stu-id="5673b-170">Store and view diagnostic data in Azure Storage</span></span>](cloud-services-dotnet-diagnostics-storage.md)
* [<span data-ttu-id="5673b-171">IIS 記錄會停止在雲端服務中寫入</span><span class="sxs-lookup"><span data-stu-id="5673b-171">IIS Logs stops writing in cloud service</span></span>](https://blogs.msdn.microsoft.com/cie/2013/12/21/iis-logs-stops-writing-in-cloud-service/)

## <a name="what-is-hello-purpose-of-hello-windows-azure-tools-encryption-certificate-for-extensions"></a><span data-ttu-id="5673b-172">Hello"Windows Azure Tools 加密憑證的延伸模組 」 的目的是 hello 的什麼？</span><span class="sxs-lookup"><span data-stu-id="5673b-172">What is hello purpose of hello "Windows Azure Tools Encryption Certificate for Extensions"?</span></span>
<span data-ttu-id="5673b-173">擴充功能加入 toohello 雲端服務時，會自動建立這些憑證。</span><span class="sxs-lookup"><span data-stu-id="5673b-173">These certificates are automatically created whenever an extension is added toohello cloud service.</span></span> <span data-ttu-id="5673b-174">大多數情況下，這是 hello wad 的資料延伸模組或 hello RDP 延伸模組，但它可能是其他人，例如 hello 反惡意程式碼或記錄檔收集器延伸模組。</span><span class="sxs-lookup"><span data-stu-id="5673b-174">Most commonly, this is hello WAD extension or hello RDP extension, but it could be others, such as hello Antimalware or Log Collector extension.</span></span> <span data-ttu-id="5673b-175">這些憑證只用於加密和解密 hello hello 擴充功能私用組態。</span><span class="sxs-lookup"><span data-stu-id="5673b-175">These certificates are only used for encrypting and decrypting hello private configuration for hello extension.</span></span> <span data-ttu-id="5673b-176">永遠不會檢查 hello 到期日，因此並不重要 hello 憑證已過期。</span><span class="sxs-lookup"><span data-stu-id="5673b-176">hello expiration date is never checked, so it doesn’t matter if hello certificate is expired.</span></span> 

<span data-ttu-id="5673b-177">您可以忽略這些憑證。</span><span class="sxs-lookup"><span data-stu-id="5673b-177">You can ignore these certificates.</span></span> <span data-ttu-id="5673b-178">如果您想要清除 hello 憑證，您可以嘗試刪除全部。</span><span class="sxs-lookup"><span data-stu-id="5673b-178">If you want to clean up hello certificates, you can try deleting them all.</span></span> <span data-ttu-id="5673b-179">Azure 將會擲回錯誤 toodelete 再試一次，如果正在使用中的憑證。</span><span class="sxs-lookup"><span data-stu-id="5673b-179">Azure will throw an error if you try toodelete a certificate that is in use.</span></span>

## <a name="how-can-i-generate-a-certificate-signing-request-csr-without-rdp-ing-in-toohello-instance"></a><span data-ttu-id="5673b-180">如何產生憑證簽署要求 (CSR) 沒有"RDP ing"toohello 執行個體中？</span><span class="sxs-lookup"><span data-stu-id="5673b-180">How can I generate a Certificate Signing Request (CSR) without "RDP-ing" in toohello instance?</span></span>
<span data-ttu-id="5673b-181">請參閱下列指引文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="5673b-181">See hello following guidance document:</span></span>

>[<span data-ttu-id="5673b-182">使用 Windows Azure 網站 (WAWS) 取得要使用的憑證</span><span class="sxs-lookup"><span data-stu-id="5673b-182">Obtaining a certificate for use with Windows Azure Web Sites (WAWS)</span></span>](https://azure.microsoft.com/blog/obtaining-a-certificate-for-use-with-windows-azure-web-sites-waws/)

<span data-ttu-id="5673b-183">請注意，CSR 只是一個文字檔。</span><span class="sxs-lookup"><span data-stu-id="5673b-183">Please note that a CSR is just a text file.</span></span> <span data-ttu-id="5673b-184">它沒有從 hello 機器建立 toobe 其中 hello 將最終會使用憑證。</span><span class="sxs-lookup"><span data-stu-id="5673b-184">It does NOT have toobe created from hello machine where hello certificate will ultimately be used.</span></span><span data-ttu-id="5673b-185"> 雖然這份文件會寫入應用程式服務，hello CSR 建立為泛型，也適用於雲端服務。</span><span class="sxs-lookup"><span data-stu-id="5673b-185"> Although this document is written for an App Service, hello CSR creation is generic and applies also for Cloud Services.</span></span>
