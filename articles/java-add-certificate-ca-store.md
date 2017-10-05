---
title: "新增憑證至 Java CA 存放區 | Microsoft Docs"
description: "了解如何將憑證授權單位 (CA) 憑證新增至 Twilio 服務或 Azure 服務匯流排的 Java CA 憑證 (cacerts) 存放區。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4f3ec837588c6e959e82108ca25ab4289e40d3f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="adding-a-certificate-to-the-java-ca-certificates-store"></a><span data-ttu-id="9e9ad-103">新增憑證至 Java CA 憑證存放區</span><span class="sxs-lookup"><span data-stu-id="9e9ad-103">Adding a Certificate to the Java CA Certificates Store</span></span>
<span data-ttu-id="9e9ad-104">下列步驟顯示如何新增憑證授權單位 (CA) 憑證到 Java CA 憑證 (cacerts) 存放區。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-104">The following steps show you how to add a certificate authority (CA) certificate to the Java CA certificate (cacerts) store.</span></span> <span data-ttu-id="9e9ad-105">使用的範例是針對 Twilio 服務所要求的 CA 憑證。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-105">The example used is for the CA certificate required by the Twilio service.</span></span> <span data-ttu-id="9e9ad-106">本主題稍後提供的資訊將說明如何安裝 Azure 服務匯流排的 CA 憑證。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-106">Information provided later in the topic describes how to install the CA certificate for the Azure Service Bus.</span></span> 

<span data-ttu-id="9e9ad-107">您可以先使用 keytool 新增 CA 憑證，再將 JDK 壓縮並新增到 Azure 專案的 **approot** 資料夾，或者也可以執行使用了 keytool 來新增憑證的 Azure 啟動工作。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-107">You can use keytool to add the CA certificate prior to zipping your JDK and adding it to your Azure project's **approot** folder, or you could run an Azure start-up task that uses keytool to add the certificate.</span></span> <span data-ttu-id="9e9ad-108">這個範例假設您會先新增 CA 憑證再將 JDK 壓縮。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-108">This example assumes you will add a CA certificate prior to the JDK being zipped.</span></span> <span data-ttu-id="9e9ad-109">另外，範例中將使用特定 CA 憑證，但是若要取得不同的 CA 憑證並將之儲存到 cacerts 存放區，步驟會很類似。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-109">Also, a specific CA certificate will be used in the example, but the steps of obtaining a different CA certificate and importing it into the cacerts store would be similar.</span></span>

## <a name="to-add-a-certificate-to-the-cacerts-store"></a><span data-ttu-id="9e9ad-110">新增憑證至 cacerts 存放區</span><span class="sxs-lookup"><span data-stu-id="9e9ad-110">To add a certificate to the cacerts store</span></span>
1. <span data-ttu-id="9e9ad-111">在設定為 JDK **jdk\jre\lib\security** 資料夾的命令提示字元下，執行下列命令來查看已安裝哪些憑證：</span><span class="sxs-lookup"><span data-stu-id="9e9ad-111">At a command prompt that is set to your JDK's **jdk\jre\lib\security** folder, run the following to see what certificates are installed:</span></span>
   
    `keytool -list -keystore cacerts`
   
    <span data-ttu-id="9e9ad-112">系統會提示您輸入存放區密碼。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-112">You'll be prompted for the store password.</span></span> <span data-ttu-id="9e9ad-113">預設密碼為 **changeit**。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-113">The default password is **changeit**.</span></span> <span data-ttu-id="9e9ad-114">(若要變更密碼，請參閱 keytool 文件，網址為 <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>。)這個範例假設 MD5 指紋為 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 的憑證未列在其中，而您想要將它匯入 (Twilio API service 需要這個特定的憑證)。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-114">(If you want to change the password, see the keytool documentation at <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) This example assumes that the certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 is not listed, and that you want to import it (this particular certificate is needed by the Twilio API service).</span></span>
2. <span data-ttu-id="9e9ad-115">從 [GeoTrust 根憑證](http://www.geotrust.com/resources/root-certificates/)(英文)列出的憑證清單取得憑證。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-115">Obtain the certificate from the list of certificates listed at [GeoTrust Root Certificates](http://www.geotrust.com/resources/root-certificates/).</span></span> <span data-ttu-id="9e9ad-116">以滑鼠右鍵按一下序號為 35:DE:F4:CF 之憑證的連結，將它儲存到 **jdk\jre\lib\security** 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-116">Right-click the link for the certificate with serial number 35:DE:F4:CF and save it to the **jdk\jre\lib\security** folder.</span></span> <span data-ttu-id="9e9ad-117">基於本範例的目的，它是儲存成名為 **Equifax\_Secure\_Certificate\_Authority.cer** 的檔案。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-117">For purposes of this example, it was saved to a file named **Equifax\_Secure\_Certificate\_Authority.cer**.</span></span>
3. <span data-ttu-id="9e9ad-118">透過下列命令匯入憑證：</span><span class="sxs-lookup"><span data-stu-id="9e9ad-118">Import the certificate via the following command:</span></span>
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    <span data-ttu-id="9e9ad-119">當系統提示您信任這個憑證，如果憑證有 MD5 指紋 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4，請輸入 **y**回應。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-119">When prompted to trust this certificate, if the certificate has MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, respond by typing **y**.</span></span>
4. <span data-ttu-id="9e9ad-120">執行下列命令確定成功匯入 CA 憑證：</span><span class="sxs-lookup"><span data-stu-id="9e9ad-120">Run the following command to ensure the CA certificate has been successfully imported:</span></span>
   
    `keytool -list -keystore cacerts`
5. <span data-ttu-id="9e9ad-121">將 JDK 壓縮並新增到 Azure 專案的 **approot** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-121">Zip the JDK and add it to your Azure project's **approot** folder.</span></span>

<span data-ttu-id="9e9ad-122">如需 keytool 的詳細資訊，請參閱 <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-122">For information about keytool, see <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>

## <a name="azure-root-certificates"></a><span data-ttu-id="9e9ad-123">Azure 根憑證</span><span class="sxs-lookup"><span data-stu-id="9e9ad-123">Azure Root Certificates</span></span>
<span data-ttu-id="9e9ad-124">使用 Azure 服務 (例如 Azure 服務匯流排) 的應用程式需要信任 Baltimore CyberTrust 根憑證。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-124">Your applications that use Azure services (such as Azure Service Bus) need to trust the Baltimore CyberTrust Root certificate.</span></span> <span data-ttu-id="9e9ad-125">(自 2013 年 4 月 15 日起，Azure 就已開始從 GTE CyberTrust 全域根憑證移轉到 Baltimore CyberTrust 根憑證。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-125">(Beginning April 15, 2013, Azure began migrating from the GTE CyberTrust Global Root to the Baltimore CyberTrust Root.</span></span> <span data-ttu-id="9e9ad-126">此次移轉花費了幾個月的時間完成。)</span><span class="sxs-lookup"><span data-stu-id="9e9ad-126">This migration took several months to complete.)</span></span>

<span data-ttu-id="9e9ad-127">Baltimore 憑證可能已經安裝於您的 cacerts 存放區，因此請記得先執行 **keytool -list** 命令看看它是否已經存在。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-127">The Baltimore certificate might already be installed in your cacerts store, so remember to run the **keytool -list** command first to see if it already exists.</span></span>

<span data-ttu-id="9e9ad-128">如果您需要新增 Baltimore CyberTrust 根憑證，它的序號是 02:00:00:b9、SHA1 指紋是 d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-128">If you need to add the Baltimore CyberTrust Root, it has serial number 02:00:00:b9 and SHA1 fingerprint d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74.</span></span> <span data-ttu-id="9e9ad-129">從 <https://cacert.omniroot.com/bc2025.crt> 下載它並儲存到副檔名為 **.cer** 的本機檔案，然後使用 **keytool** 匯入，如上文所述。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-129">It can be downloaded from <https://cacert.omniroot.com/bc2025.crt>, saved to a local file with extension **.cer**, and then imported using **keytool** as shown above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e9ad-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9e9ad-130">Next steps</span></span>
<span data-ttu-id="9e9ad-131">如需 Azure 所用根憑證的詳細資訊，請參閱 [Azure 根憑證移轉](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-131">For more information about the root certificates used by Azure, see [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).</span></span>

<span data-ttu-id="9e9ad-132">如需 Java 的詳細資訊，請參閱[適用於 Java 開發人員的 Azure](/java/azure)。</span><span class="sxs-lookup"><span data-stu-id="9e9ad-132">For more information about Java, see [Azure for Java developers](/java/azure).</span></span>

