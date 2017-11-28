---
title: "aaaAdd 憑證 toohello Java CA 存放區 |Microsoft 文件"
description: "了解如何 tooadd 憑證授權單位 (CA) 憑證 toohello Java CA (cacerts) 之憑證存放區 Twilio 服務或 Azure 服務匯流排。"
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
ms.openlocfilehash: 030e43129580023942dee662e72d2f443167f308
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-certificate-toohello-java-ca-certificates-store"></a><span data-ttu-id="c609c-103">新增憑證 toohello Java CA 的憑證存放區</span><span class="sxs-lookup"><span data-stu-id="c609c-103">Adding a Certificate toohello Java CA Certificates Store</span></span>
<span data-ttu-id="c609c-104">hello 下列步驟顯示如何 tooadd 憑證授權單位 (CA) 憑證 toohello Java CA 憑證 (cacerts) 儲存。</span><span class="sxs-lookup"><span data-stu-id="c609c-104">hello following steps show you how tooadd a certificate authority (CA) certificate toohello Java CA certificate (cacerts) store.</span></span> <span data-ttu-id="c609c-105">使用 hello 範例 hello CA 憑證必須使用 hello Twilio 服務。</span><span class="sxs-lookup"><span data-stu-id="c609c-105">hello example used is for hello CA certificate required by hello Twilio service.</span></span> <span data-ttu-id="c609c-106">Hello 主題稍後提供的資訊說明 tooinstall hello CA hello Azure 服務匯流排的憑證。</span><span class="sxs-lookup"><span data-stu-id="c609c-106">Information provided later in hello topic describes how tooinstall hello CA certificate for hello Azure Service Bus.</span></span> 

<span data-ttu-id="c609c-107">您可以使用 keytool tooadd hello CA 憑證先前 toozipping JDK，並將它加入 tooyour Azure 專案的**approot**資料夾，或者您可以執行使用 keytool tooadd hello 憑證 Azure 的啟動工作。</span><span class="sxs-lookup"><span data-stu-id="c609c-107">You can use keytool tooadd hello CA certificate prior toozipping your JDK and adding it tooyour Azure project's **approot** folder, or you could run an Azure start-up task that uses keytool tooadd hello certificate.</span></span> <span data-ttu-id="c609c-108">這個範例假設您將新增 CA 憑證先前 toohello 被壓縮的 JDK。</span><span class="sxs-lookup"><span data-stu-id="c609c-108">This example assumes you will add a CA certificate prior toohello JDK being zipped.</span></span> <span data-ttu-id="c609c-109">此外，特定的 CA 憑證將用於 hello 範例中，但取得不同的 CA 憑證的 hello 步驟中，並匯入至 hello cacerts 存放區會如下所示。</span><span class="sxs-lookup"><span data-stu-id="c609c-109">Also, a specific CA certificate will be used in hello example, but hello steps of obtaining a different CA certificate and importing it into hello cacerts store would be similar.</span></span>

## <a name="tooadd-a-certificate-toohello-cacerts-store"></a><span data-ttu-id="c609c-110">tooadd 憑證 toohello cacerts 儲存</span><span class="sxs-lookup"><span data-stu-id="c609c-110">tooadd a certificate toohello cacerts store</span></span>
1. <span data-ttu-id="c609c-111">在命令提示字元設定 tooyour JDK **jdk\jre\lib\security**資料夾中，執行下列已安裝哪些憑證 toosee hello:</span><span class="sxs-lookup"><span data-stu-id="c609c-111">At a command prompt that is set tooyour JDK's **jdk\jre\lib\security** folder, run hello following toosee what certificates are installed:</span></span>
   
    `keytool -list -keystore cacerts`
   
    <span data-ttu-id="c609c-112">將會提示您輸入 hello 存放的密碼。</span><span class="sxs-lookup"><span data-stu-id="c609c-112">You'll be prompted for hello store password.</span></span> <span data-ttu-id="c609c-113">hello 預設密碼為**變更**。</span><span class="sxs-lookup"><span data-stu-id="c609c-113">hello default password is **changeit**.</span></span> <span data-ttu-id="c609c-114">(如果您想 toochange hello 密碼，請參閱 hello keytool 文件，網址<http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>。)這個範例假設 MD5 指紋 67:CB:9 D 與該 hello 憑證： C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 未列出，而且您想 tooimport it （此特定的憑證所 hello Twilio API 服務）。</span><span class="sxs-lookup"><span data-stu-id="c609c-114">(If you want toochange hello password, see hello keytool documentation at <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) This example assumes that hello certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 is not listed, and that you want tooimport it (this particular certificate is needed by hello Twilio API service).</span></span>
2. <span data-ttu-id="c609c-115">從憑證列在 hello 清單取得 hello 憑證[GeoTrust 根憑證](http://www.geotrust.com/resources/root-certificates/)。</span><span class="sxs-lookup"><span data-stu-id="c609c-115">Obtain hello certificate from hello list of certificates listed at [GeoTrust Root Certificates](http://www.geotrust.com/resources/root-certificates/).</span></span> <span data-ttu-id="c609c-116">Hello 憑證序號 35:DE:F4:CF hello 連結上按一下滑鼠右鍵，並將它儲存 toohello **jdk\jre\lib\security**資料夾。</span><span class="sxs-lookup"><span data-stu-id="c609c-116">Right-click hello link for hello certificate with serial number 35:DE:F4:CF and save it toohello **jdk\jre\lib\security** folder.</span></span> <span data-ttu-id="c609c-117">基於此範例中，儲存名為 tooa 檔案**Equifax\_Secure\_憑證\_Authority.cer**。</span><span class="sxs-lookup"><span data-stu-id="c609c-117">For purposes of this example, it was saved tooa file named **Equifax\_Secure\_Certificate\_Authority.cer**.</span></span>
3. <span data-ttu-id="c609c-118">匯入 hello 憑證，透過 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="c609c-118">Import hello certificate via hello following command:</span></span>
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    <span data-ttu-id="c609c-119">當系統提示您 tootrust 此憑證，如果 hello 憑證 MD5 指紋 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4，回應輸入**y**。</span><span class="sxs-lookup"><span data-stu-id="c609c-119">When prompted tootrust this certificate, if hello certificate has MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, respond by typing **y**.</span></span>
4. <span data-ttu-id="c609c-120">執行下列命令 tooensure hello CA 憑證的 hello 已成功匯入：</span><span class="sxs-lookup"><span data-stu-id="c609c-120">Run hello following command tooensure hello CA certificate has been successfully imported:</span></span>
   
    `keytool -list -keystore cacerts`
5. <span data-ttu-id="c609c-121">壓縮 hello JDK，並將它加入 tooyour Azure 專案的**approot**資料夾。</span><span class="sxs-lookup"><span data-stu-id="c609c-121">Zip hello JDK and add it tooyour Azure project's **approot** folder.</span></span>

<span data-ttu-id="c609c-122">如需 keytool 的詳細資訊，請參閱 <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>。</span><span class="sxs-lookup"><span data-stu-id="c609c-122">For information about keytool, see <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>

## <a name="azure-root-certificates"></a><span data-ttu-id="c609c-123">Azure 根憑證</span><span class="sxs-lookup"><span data-stu-id="c609c-123">Azure Root Certificates</span></span>
<span data-ttu-id="c609c-124">您使用 Azure 服務 （例如 Azure Service Bus) 的應用程式需要 tootrust hello Baltimore CyberTrust 根憑證。</span><span class="sxs-lookup"><span data-stu-id="c609c-124">Your applications that use Azure services (such as Azure Service Bus) need tootrust hello Baltimore CyberTrust Root certificate.</span></span> <span data-ttu-id="c609c-125">（從 2013 年 4 月 15 日，Azure 已開始從 hello GTE CyberTrust 全域根 toohello Baltimore CyberTrust 根移轉。</span><span class="sxs-lookup"><span data-stu-id="c609c-125">(Beginning April 15, 2013, Azure began migrating from hello GTE CyberTrust Global Root toohello Baltimore CyberTrust Root.</span></span> <span data-ttu-id="c609c-126">這項移轉採取幾個月 toocomplete。）</span><span class="sxs-lookup"><span data-stu-id="c609c-126">This migration took several months toocomplete.)</span></span>

<span data-ttu-id="c609c-127">hello Baltimore 憑證可能已經安裝在您 cacerts 存放區中，因此請記住 toorun hello **keytool-清單**命令 toosee 第一次，如果已經存在。</span><span class="sxs-lookup"><span data-stu-id="c609c-127">hello Baltimore certificate might already be installed in your cacerts store, so remember toorun hello **keytool -list** command first toosee if it already exists.</span></span>

<span data-ttu-id="c609c-128">如果您需要 tooadd hello Baltimore CyberTrust 根，它有序號 02:00:00:b9 和 SHA1 指紋 d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2 c: 78:db:28:52:ca:e4:74。</span><span class="sxs-lookup"><span data-stu-id="c609c-128">If you need tooadd hello Baltimore CyberTrust Root, it has serial number 02:00:00:b9 and SHA1 fingerprint d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74.</span></span> <span data-ttu-id="c609c-129">您可以從下載<https://cacert.omniroot.com/bc2025.crt>，儲存 tooa 本機檔案具有副檔名**.cer**，然後再匯入使用**keytool**如上所示。</span><span class="sxs-lookup"><span data-stu-id="c609c-129">It can be downloaded from <https://cacert.omniroot.com/bc2025.crt>, saved tooa local file with extension **.cer**, and then imported using **keytool** as shown above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c609c-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c609c-130">Next steps</span></span>
<span data-ttu-id="c609c-131">如需使用 Azure 的 hello 的根憑證的詳細資訊，請參閱[Azure 根憑證移轉](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c609c-131">For more information about hello root certificates used by Azure, see [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).</span></span>

<span data-ttu-id="c609c-132">如需 Java 的詳細資訊，請參閱[適用於 Java 開發人員的 Azure](/java/azure)。</span><span class="sxs-lookup"><span data-stu-id="c609c-132">For more information about Java, see [Azure for Java developers](/java/azure).</span></span>

