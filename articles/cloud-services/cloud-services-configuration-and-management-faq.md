---
title: "Microsoft Azure 雲端服務之設定和管理問題的常見問題集 | Microsoft Docs"
description: "本文列出 Microsoft Azure 雲端服務之設定和管理的相關常見問題集。"
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
ms.openlocfilehash: 42b5d2947df92b4486fe149d046168208083dde2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="configuration-and-management-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a><span data-ttu-id="ffaf1-103">Azure 雲端服務之設定和管理問題：常見問題集 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="ffaf1-103">Configuration and management issues for Azure Cloud Services: Frequently asked questions (FAQs)</span></span>

<span data-ttu-id="ffaf1-104">本文包含 [Microsoft Azure 雲端服務](https://azure.microsoft.com/services/cloud-services)之設定和管理問題的相關常見問題集。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-104">This article includes frequently asked questions about configuration and management issues for [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services).</span></span> <span data-ttu-id="ffaf1-105">您也可以參閱 [雲端服務 VM 大小頁面](cloud-services-sizes-specs.md) 以取得大小資訊。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-105">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="how-do-i-add-nosniff-to-my-website"></a><span data-ttu-id="ffaf1-106">如何將 "nosniff" 新增至我的網站？</span><span class="sxs-lookup"><span data-stu-id="ffaf1-106">How do I add "nosniff" to my website?</span></span>
<span data-ttu-id="ffaf1-107">若要防止用戶端探查 MIME 類型，請在您的 *web.config* 檔案中加入一項設定。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-107">To prevent clients from sniffing the MIME types, add a setting in your *web.config* file.</span></span>

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

<span data-ttu-id="ffaf1-108">您也可以在 IIS 中將此加入為設定。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-108">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="ffaf1-109">請參考[常見的啟動工作](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe)一文來使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-109">Use the following command with the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

## <a name="how-do-i-customize-iis-for-a-web-role"></a><span data-ttu-id="ffaf1-110">如何自訂 Web 角色的 IIS？</span><span class="sxs-lookup"><span data-stu-id="ffaf1-110">How do I customize IIS for a web role?</span></span>
<span data-ttu-id="ffaf1-111">請從[常見的啟動工作](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe)一文使用 IIS 啟動指令碼。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-111">Use the IIS startup script from the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="ffaf1-112">我不能調整超過 X 個執行個體</span><span class="sxs-lookup"><span data-stu-id="ffaf1-112">I cannot scale beyond X instances</span></span>
<span data-ttu-id="ffaf1-113">您的 Azure 訂用帳戶對於您可以使用的核心數目有限制。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-113">Your Azure Subscription has a limit on the number of cores you can use.</span></span> <span data-ttu-id="ffaf1-114">如果您已使用所有可用的核心，調整將無法運作。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-114">Scaling will not work if you have used all the cores available.</span></span> <span data-ttu-id="ffaf1-115">例如，如果您有 100 個核心的限制，這表示您的雲端服務可以有 100 個 A1 大小的虛擬機器執行個體，或 50 個 A2 大小的虛擬機器執行個體。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-115">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="how-can-i-implement-role-based-access-for-cloud-services"></a><span data-ttu-id="ffaf1-116">如何實作雲端服務的角色型存取？</span><span class="sxs-lookup"><span data-stu-id="ffaf1-116">How can I implement Role-Based Access for Cloud Services?</span></span>
<span data-ttu-id="ffaf1-117">雲端服務不支援角色型存取控制 (RBAC) 模型，因為它不是以 Azure Resource Manager 為基礎的服務。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-117">Cloud Services doesn't support the Role-Based Access Control (RBAC) model, as it's not an Azure Resource Manager based service.</span></span>

<span data-ttu-id="ffaf1-118">請參閱 [Azure RBAC 與傳統訂用帳戶系統管理員](../active-directory/role-based-access-control-what-is.md#azure-rbac-vs-classic-subscription-administrators)。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-118">See [Azure RBAC vs. classic subscription administrators](../active-directory/role-based-access-control-what-is.md#azure-rbac-vs-classic-subscription-administrators).</span></span>

## <a name="how-do-i-set-the-idle-timeout-for-azure-load-balancer"></a><span data-ttu-id="ffaf1-119">如何設定 Azure Load Balancer 的閒置逾時？</span><span class="sxs-lookup"><span data-stu-id="ffaf1-119">How do I set the idle timeout for Azure load balancer?</span></span>
<span data-ttu-id="ffaf1-120">您可以在服務定義 (csdef) 檔中指定逾時，就像這樣：</span><span class="sxs-lookup"><span data-stu-id="ffaf1-120">You can specify the timeout in your service definition (csdef) file like this:</span></span>

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
<span data-ttu-id="ffaf1-121">如需詳細資訊，請參閱[新增：Azure Load Balancer 的可設定閒置逾時](https://azure.microsoft.com/blog/new-configurable-idle-timeout-for-azure-load-balancer/)。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-121">See [New: Configurable Idle Timeout for Azure Load Balancer](https://azure.microsoft.com/blog/new-configurable-idle-timeout-for-azure-load-balancer/) for more information.</span></span>

## <a name="can-microsoft-internal-engineers-rdp-to-cloud-service-instances-without-permission"></a><span data-ttu-id="ffaf1-122">Microsoft 內部工程師是否可在沒有權限的情況下，RDP 到雲端服務執行個體？</span><span class="sxs-lookup"><span data-stu-id="ffaf1-122">Can Microsoft internal engineers RDP to cloud service instances without permission?</span></span>
<span data-ttu-id="ffaf1-123">Microsoft 會遵循嚴格的程序，不允許內部工程師在沒有擁有者或其受指派者寫入權限的情況下，RDP 到您的雲端服務 (電子郵件或其他撰寫的通訊) 中。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-123">Microsoft follows a strict process that will not allow internal engineers to RDP into your cloud service without written permission (email or other written communication) from the owner or their designee.</span></span>

## <a name="why-is-the-certificate-chain-of-my-cloud-service-ssl-certificate-incomplete"></a><span data-ttu-id="ffaf1-124">為什麼我雲端服務 SSL 憑證的憑證鏈結是不完整的？</span><span class="sxs-lookup"><span data-stu-id="ffaf1-124">Why is the certificate chain of my cloud service SSL certificate incomplete?</span></span>
<span data-ttu-id="ffaf1-125">我們建議客戶安裝完整的憑證鏈結而不是分葉憑證 (分葉憑證、中繼憑證、和根憑證)。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-125">We recommend that customers install the full certificate chain (leaf cert, intermediate certs, and root cert) instead of just the leaf certificate.</span></span> <span data-ttu-id="ffaf1-126">當您安裝分葉憑證時，會依賴 Windows 透過查核 CTL 來建置憑證鏈結。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-126">When you install just the leaf certificate, you rely on Windows to build the certificate chain by walking the CTL.</span></span> <span data-ttu-id="ffaf1-127">如果當 Windows 嘗試驗證憑證時，在 Azure 或 Windows Update 中發生間歇性網路或 DNS 問題，就可能會將憑證視為無效。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-127">If intermittent network or DNS issues occur in Azure or Windows Update when Windows is trying to validate the certificate, the certificate may be considered invalid.</span></span> <span data-ttu-id="ffaf1-128">藉由安裝完整的憑證鏈結，就可以避免這個問題。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-128">By installing the full certificate chain, this problem can be avoided.</span></span> <span data-ttu-id="ffaf1-129">[如何安裝鏈結的 SSL 憑證](https://blogs.msdn.microsoft.com/azuredevsupport/2010/02/24/how-to-install-a-chained-ssl-certificate/)中的部落格會示範如何執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-129">The blog at [How to install a chained SSL certificate](https://blogs.msdn.microsoft.com/azuredevsupport/2010/02/24/how-to-install-a-chained-ssl-certificate/) shows how to do this.</span></span>

## <a name="how-do-i-associate-a-static-ip-address-to-my-cloud-service"></a><span data-ttu-id="ffaf1-130">如何將靜態 IP 位址關聯到我的雲端服務？</span><span class="sxs-lookup"><span data-stu-id="ffaf1-130">How do I associate a static IP address to my cloud service?</span></span>
<span data-ttu-id="ffaf1-131">若要設定靜態 IP 位址，您必須建立保留的 IP。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-131">To set up a static IP address, you need to create a reserved IP.</span></span> <span data-ttu-id="ffaf1-132">這個保留的 IP 可以關聯到新的雲端服務或現有的部署。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-132">This reserved IP can be associated to a new cloud service or to an existing deployment.</span></span> <span data-ttu-id="ffaf1-133">請參閱以下文件了解詳細資料：</span><span class="sxs-lookup"><span data-stu-id="ffaf1-133">See the following documents for details:</span></span>
* [<span data-ttu-id="ffaf1-134">如何建立保留的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="ffaf1-134">How to create a reserved IP address</span></span>](../virtual-network/virtual-networks-reserved-public-ip.md#manage-reserved-vips)
* [<span data-ttu-id="ffaf1-135">保留現有雲端服務的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="ffaf1-135">Reserve the IP address of an existing cloud service</span></span>](../virtual-network/virtual-networks-reserved-public-ip.md#reserve-the-ip-address-of-an-existing-cloud-service)
* [<span data-ttu-id="ffaf1-136">建立保留的 IP 至新雲端服務的關聯</span><span class="sxs-lookup"><span data-stu-id="ffaf1-136">Associate a reserved IP to a new cloud service</span></span>](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-new-cloud-service)
* [<span data-ttu-id="ffaf1-137">建立保留的 IP 至執行中部署的關聯</span><span class="sxs-lookup"><span data-stu-id="ffaf1-137">Associate a reserved IP to a running deployment</span></span>](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-running-deployment)
* [<span data-ttu-id="ffaf1-138">使用服務組態檔建立保留的 IP 至雲端服務的關聯</span><span class="sxs-lookup"><span data-stu-id="ffaf1-138">Associate a reserved IP to a cloud service by using a service configuration file</span></span>](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file)

## <a name="what-is-the-quota-limit-for-my-cloud-service"></a><span data-ttu-id="ffaf1-139">什麼是我的雲端服務配額限制？</span><span class="sxs-lookup"><span data-stu-id="ffaf1-139">What is the quota limit for my cloud service?</span></span>
<span data-ttu-id="ffaf1-140">請參閱[特定服務的限制](../azure-subscription-service-limits.md#subscription-limits)。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-140">See [Service-specific limits](../azure-subscription-service-limits.md#subscription-limits).</span></span>

## <a name="why-does-the-drive-on-my-cloud-service-vm-show-very-little-free-disk-space"></a><span data-ttu-id="ffaf1-141">為什麼我雲端服務 VM 上的磁碟機顯示幾乎沒有可用的磁碟空間？</span><span class="sxs-lookup"><span data-stu-id="ffaf1-141">Why does the drive on my cloud service VM show very little free disk space?</span></span>
<span data-ttu-id="ffaf1-142">這是預期的行為，並不會對您的應用程式造成任何問題。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-142">This is expected behavior, and it shouldn't cause any issue to your application.</span></span> <span data-ttu-id="ffaf1-143">在 Azure PaaS VM 中會開啟 %uproot% 磁碟機的日誌記錄，基本上會消耗兩倍檔案通常所佔用的空間數量。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-143">Journaling is turned on for the %uproot% drive in Azure PaaS VMs, which essentially consumes double the amount of space that files normally take up.</span></span> <span data-ttu-id="ffaf1-144">不過，要留意幾件事，基本上這就會變得沒有問題。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-144">However there are several things to be aware of that essentially turn this into a non-issue.</span></span>

<span data-ttu-id="ffaf1-145">%approot% 磁碟機大小會以 <.cspkg 的大小 + 最大的日誌大小 + 可用空間的邊界> 來計算，或 1.5 GB，兩者取其較大。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-145">The %approot% drive size is calculated as <size of .cspkg + max journal size + a margin of free space>, or 1.5 GB, whichever is larger.</span></span> <span data-ttu-id="ffaf1-146">您 VM 的大小對這個計算方式並無任何影響。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-146">The size of your VM has no bearing on this calculation.</span></span> <span data-ttu-id="ffaf1-147">(VM 大小只會影響暫存 C: 磁碟機的大小。)</span><span class="sxs-lookup"><span data-stu-id="ffaf1-147">(The VM size only affects the size of the temporary C: drive.)</span></span> 

<span data-ttu-id="ffaf1-148">它不支援寫入 %approot% 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-148">It is unsupported to write to the %approot% drive.</span></span> <span data-ttu-id="ffaf1-149">如果您要寫入 Azure VM 中，必須在暫存 LocalStorage 資源中進行 (或其他選項，例如 Blob 儲存體、Azure 檔案等)。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-149">If you are writing to the Azure VM, you must do so in a temporary LocalStorage resource (or other option, such as Blob storage, Azure Files, etc.).</span></span> <span data-ttu-id="ffaf1-150">因此在 %approot% 資料夾上的可用空間數量沒有任何意義。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-150">So the amount of free space on the %approot% folder is not meaningful.</span></span> <span data-ttu-id="ffaf1-151">如果您不確定應用程式是否要寫入 %approot% 磁碟機中，一律可以讓您的服務執行幾天，然後比較「之前」和「之後」的大小。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-151">If you are not sure if your application is writing to the %approot% drive, you can always let your service run for a few days and then compare the "before" and "after" sizes.</span></span> 

<span data-ttu-id="ffaf1-152">Azure 不會將任何內容寫入 %approot% 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-152">Azure will not write anything to the %approot% drive.</span></span> <span data-ttu-id="ffaf1-153">一旦從 .cspkg 建立 VHD 並將其掛接至 Azure VM 後，唯一可能會寫入此磁碟機的就是您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-153">Once the VHD is created from your .cspkg and mounted into the Azure VM, the only thing that might write to this drive is your application.</span></span> 

<span data-ttu-id="ffaf1-154">日誌設定是不可設定的，因此您無法將它關閉。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-154">The journal settings are non-configurable, so you can't turn it off.</span></span>

## <a name="what-are-the-features-and-capabilities-that-azure-basic-ipsids-and-ddos-provides"></a><span data-ttu-id="ffaf1-155">Azure 的基本 IPS/IDS 和 DDOS 提供的特性和功能是什麼？</span><span class="sxs-lookup"><span data-stu-id="ffaf1-155">What are the features and capabilities that Azure basic IPS/IDS and DDOS provides?</span></span>
<span data-ttu-id="ffaf1-156">Azure 在資料中心實體伺服器中擁有 IP/ID 可以防範潛威脅。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-156">Azure has IPS/IDS in datacenter physical servers to defend against threats.</span></span> <span data-ttu-id="ffaf1-157">此外，客戶可以部署第三方安全性解決方案，例如 Web 應用程式防火牆、網路防火牆、反惡意程式碼軟體、入侵偵測、預防系統 (IDS/IPS) 等等。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-157">In addition, customers can deploy third-party security solutions, such as web application firewalls, network firewalls, antimalware, intrusion detection, prevention systems (IDS/IPS), and more.</span></span> <span data-ttu-id="ffaf1-158">如需詳細資訊，請參閱[保護您的資料和資產，以及符合全域安全性標準](https://www.microsoft.com/en-us/trustcenter/Security/AzureSecurity)。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-158">For more information, see [Protect your data and assets and comply with global security standards](https://www.microsoft.com/en-us/trustcenter/Security/AzureSecurity).</span></span>

<span data-ttu-id="ffaf1-159">Microsoft 會持續監視伺服器、網路和應用程式來偵測威脅。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-159">Microsoft continuously monitors servers, networks, and applications to detect threats.</span></span> <span data-ttu-id="ffaf1-160">Azure 的多元化威脅管理方法會使用入侵偵測、分散式阻斷服務 (DDoS) 攻擊防護、滲透測試、行為分析、異常偵測和機器學習，不斷地加強其防禦並降低風險。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-160">Azure's multipronged threat-management approach uses intrusion detection, distributed denial-of-service (DDoS) attack prevention, penetration testing, behavioral analytics, anomaly detection, and machine learning to constantly strengthen its defense and reduce risks.</span></span> <span data-ttu-id="ffaf1-161">適用於 Azure 保護的 Azure 雲端服務和虛擬機器的 Microsoft Antimalware。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-161">Microsoft Antimalware for Azure protects Azure cloud services and virtual machines.</span></span> <span data-ttu-id="ffaf1-162">您可以選擇額外部署第三方安全性解決方案，例如 Web 應用程式防火牆、網路防火牆、反惡意程式碼軟體、入侵偵測以及預防系統 (IDS/IPS) 等等。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-162">You have the option to deploy third-party security solutions in addition, such as web application fire walls, network firewalls, antimalware, intrusion detection and prevention systems (IDS/IPS), and more.</span></span>

## <a name="why-does-iis-stop-writing-to-the-log-directory"></a><span data-ttu-id="ffaf1-163">為什麼 IIS 會停止寫入記錄目錄？</span><span class="sxs-lookup"><span data-stu-id="ffaf1-163">Why does IIS stop writing to the log directory?</span></span>
<span data-ttu-id="ffaf1-164">您已耗盡寫入記錄目錄的本機儲存體配額。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-164">You have exhausted the local storage quota for writing to the log directory.</span></span><span data-ttu-id="ffaf1-165"> 若要修正此問題，您可以執行下列三個項目的其中一項：</span><span class="sxs-lookup"><span data-stu-id="ffaf1-165"> To correct this, you can do one of three things:</span></span>
* <span data-ttu-id="ffaf1-166">啟用 IIS 的診斷，並定期將診斷移至 blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-166">Enable diagnostics for IIS and have the diagnostics periodically moved to blob storage.</span></span>
* <span data-ttu-id="ffaf1-167">從記錄目錄中手動移除記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-167">Manually remove log files from the logging directory.</span></span>
* <span data-ttu-id="ffaf1-168">增加本機資源的配額限制。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-168">Increase quota limit for local resources.</span></span>

<span data-ttu-id="ffaf1-169">如需詳細資訊，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="ffaf1-169">For more information, see the following documents:</span></span>
* [<span data-ttu-id="ffaf1-170">在 Azure 儲存體中儲存和檢視診斷資料</span><span class="sxs-lookup"><span data-stu-id="ffaf1-170">Store and view diagnostic data in Azure Storage</span></span>](cloud-services-dotnet-diagnostics-storage.md)
* [<span data-ttu-id="ffaf1-171">IIS 記錄會停止在雲端服務中寫入</span><span class="sxs-lookup"><span data-stu-id="ffaf1-171">IIS Logs stops writing in cloud service</span></span>](https://blogs.msdn.microsoft.com/cie/2013/12/21/iis-logs-stops-writing-in-cloud-service/)

## <a name="what-is-the-purpose-of-the-windows-azure-tools-encryption-certificate-for-extensions"></a><span data-ttu-id="ffaf1-172">「Windows Azure Tools 擴充功能的加密憑證」用途為何？</span><span class="sxs-lookup"><span data-stu-id="ffaf1-172">What is the purpose of the "Windows Azure Tools Encryption Certificate for Extensions"?</span></span>
<span data-ttu-id="ffaf1-173">每當有擴充功能新增至雲端服務時，就會自動建立這些憑證。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-173">These certificates are automatically created whenever an extension is added to the cloud service.</span></span> <span data-ttu-id="ffaf1-174">大多數情況下，這是 WAD 擴充功能或 RDP 擴充功能，但也可能是其他的，例如反惡意程式碼軟體或記錄收集器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-174">Most commonly, this is the WAD extension or the RDP extension, but it could be others, such as the Antimalware or Log Collector extension.</span></span> <span data-ttu-id="ffaf1-175">這些憑證僅用於將擴充功能的私用組態進行加密和解密。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-175">These certificates are only used for encrypting and decrypting the private configuration for the extension.</span></span> <span data-ttu-id="ffaf1-176">永遠不會檢查到期日，因此憑證是否過期並不重要。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-176">The expiration date is never checked, so it doesn’t matter if the certificate is expired.</span></span> 

<span data-ttu-id="ffaf1-177">您可以忽略這些憑證。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-177">You can ignore these certificates.</span></span> <span data-ttu-id="ffaf1-178">如果您想要清除憑證，可以嘗試將它們全部刪除。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-178">If you want to clean up the certificates, you can try deleting them all.</span></span> <span data-ttu-id="ffaf1-179">如果您嘗試刪除的憑證正在使用中，Azure 就會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-179">Azure will throw an error if you try to delete a certificate that is in use.</span></span>

## <a name="how-can-i-generate-a-certificate-signing-request-csr-without-rdp-ing-in-to-the-instance"></a><span data-ttu-id="ffaf1-180">如何能夠產生憑證簽署要求 (CSR)，而不 "RDP" 到執行個體中？</span><span class="sxs-lookup"><span data-stu-id="ffaf1-180">How can I generate a Certificate Signing Request (CSR) without "RDP-ing" in to the instance?</span></span>
<span data-ttu-id="ffaf1-181">請參閱下列指導方針文件：</span><span class="sxs-lookup"><span data-stu-id="ffaf1-181">See the following guidance document:</span></span>

>[<span data-ttu-id="ffaf1-182">使用 Windows Azure 網站 (WAWS) 取得要使用的憑證</span><span class="sxs-lookup"><span data-stu-id="ffaf1-182">Obtaining a certificate for use with Windows Azure Web Sites (WAWS)</span></span>](https://azure.microsoft.com/blog/obtaining-a-certificate-for-use-with-windows-azure-web-sites-waws/)

<span data-ttu-id="ffaf1-183">請注意，CSR 只是一個文字檔。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-183">Please note that a CSR is just a text file.</span></span> <span data-ttu-id="ffaf1-184">不必從最終會使用憑證的電腦建立它。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-184">It does NOT have to be created from the machine where the certificate will ultimately be used.</span></span><span data-ttu-id="ffaf1-185"> 雖然是針對 App Service 寫入這份文件，但 CSR 建立為泛型，且也適用於雲端服務。</span><span class="sxs-lookup"><span data-stu-id="ffaf1-185"> Although this document is written for an App Service, the CSR creation is generic and applies also for Cloud Services.</span></span>
