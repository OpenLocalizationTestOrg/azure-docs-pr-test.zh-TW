---
title: "aaaAzure 存放裝置總管疑難排解指南 |Microsoft 文件"
description: "Hello 兩個 Azure 偵錯功能的概觀"
services: virtual-machines
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: delhan
ms.openlocfilehash: 5152f70418707d65c0a4bce9a916336829956219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="cbd63-103">Azure 儲存體總管疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="cbd63-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="cbd63-104">簡介</span><span class="sxs-lookup"><span data-stu-id="cbd63-104">Introduction</span></span>

<span data-ttu-id="cbd63-105">Microsoft Azure 儲存體總管 （預覽） 是一個獨立應用程式，可讓您 tooeasily 使用在 Windows、 macOS 和 Linux 的 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="cbd63-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you tooeasily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="cbd63-106">hello 應用程式可以連接 toStorage Sovereign 雲端 Azure Azure 堆疊上裝載的帳戶。</span><span class="sxs-lookup"><span data-stu-id="cbd63-106">hello app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="cbd63-107">本指南摘要說明儲存體總管中常見的問題解決方案。</span><span class="sxs-lookup"><span data-stu-id="cbd63-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="cbd63-108">登入問題</span><span class="sxs-lookup"><span data-stu-id="cbd63-108">Sign in issues</span></span>

<span data-ttu-id="cbd63-109">在繼續之前，請嘗試重新啟動您的應用程式，並查看是否可以固定 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="cbd63-109">Before you continue, try restarting your application and see whether hello problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="cbd63-110">錯誤：憑證鏈結中的自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="cbd63-110">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="cbd63-111">有數個原因，您可能會遇到這個錯誤，並且 hello 最常見的兩個原因如下：</span><span class="sxs-lookup"><span data-stu-id="cbd63-111">There are several reasons why you may encounter this error, and hello most common two reasons are as follows:</span></span>

1. <span data-ttu-id="cbd63-112">hello 應用程式是透過"transparent proxy"，這表示攔截 HTTPS 流量，解密，而且再加密使用自我簽署的憑證 （例如您公司的伺服器） 的伺服器連接。</span><span class="sxs-lookup"><span data-stu-id="cbd63-112">hello app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="cbd63-113">您正在執行的應用程式，例如防毒軟體，注入 hello HTTPS 訊息，您會收到自我簽署的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="cbd63-113">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into hello HTTPS messages that you receive.</span></span>

<span data-ttu-id="cbd63-114">當儲存體總管遇到的其中一個 hello 問題時，它不再可以知道收到 hello HTTPS 訊息是否遭竄改。</span><span class="sxs-lookup"><span data-stu-id="cbd63-114">When Storage Explorer encounters one of hello issues, it can no longer know whether hello received HTTPS message is tampered.</span></span> <span data-ttu-id="cbd63-115">如果您有一份 hello 自我簽署憑證，您可以讓信任它的儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="cbd63-115">If you have a copy of hello self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="cbd63-116">如果您不清楚誰正在插入 hello 憑證，請遵循這些步驟 toofind 它：</span><span class="sxs-lookup"><span data-stu-id="cbd63-116">If you are unsure of who is injecting hello certificate, follow these steps toofind it:</span></span>

1. <span data-ttu-id="cbd63-117">安裝 Open SSL</span><span class="sxs-lookup"><span data-stu-id="cbd63-117">Install Open SSL</span></span>

    - <span data-ttu-id="cbd63-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) （任一 hello 淺色版本應已足夠）</span><span class="sxs-lookup"><span data-stu-id="cbd63-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of hello light versions should be sufficient)</span></span>

    - <span data-ttu-id="cbd63-119">Mac 和 Linux：應該包含在作業系統中</span><span class="sxs-lookup"><span data-stu-id="cbd63-119">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="cbd63-120">執行 Open SSL</span><span class="sxs-lookup"><span data-stu-id="cbd63-120">Run Open SSL</span></span>

    - <span data-ttu-id="cbd63-121">Windows： 開啟 hello 安裝目錄中，按一下**/bin/**，然後按兩下**openssl.exe**。</span><span class="sxs-lookup"><span data-stu-id="cbd63-121">Windows: open hello installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="cbd63-122">Mac 和 Linux：從終端機執行 **openssl**。</span><span class="sxs-lookup"><span data-stu-id="cbd63-122">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="cbd63-123">執行 s_client -showcerts -connect microsoft.com:443</span><span class="sxs-lookup"><span data-stu-id="cbd63-123">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="cbd63-124">尋找自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="cbd63-124">Look for self-signed certificates.</span></span> <span data-ttu-id="cbd63-125">如果您不確定哪些是自我簽署，請尋找任何位置 hello 主旨 ("s") 及簽發者 （「 i:"） 是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="cbd63-125">If you are unsure which are self-signed, look for anywhere hello subject ("s:") and issuer ("i:") are hello same.</span></span>

5. <span data-ttu-id="cbd63-126">當您找到任何自我簽署的憑證時，每個複製和貼上的所有項目從和包括**---BEGIN CERTIFICATE---**太**---憑證結尾---** tooa 新.cer 檔案。</span><span class="sxs-lookup"><span data-stu-id="cbd63-126">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** tooa new .cer file.</span></span>

6. <span data-ttu-id="cbd63-127">開啟 [儲存體總管] 中，按一下**編輯** > **SSL 憑證** > **匯入憑證**，，然後使用 hello 檔案選擇器 toofind，選取，然後開啟您建立的 hello.cer 檔案。</span><span class="sxs-lookup"><span data-stu-id="cbd63-127">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use hello file picker toofind, select, and open hello .cer files that you created.</span></span>

<span data-ttu-id="cbd63-128">如果找不到任何使用上述步驟 hello 的自我簽署的憑證，請與我們連絡透過 hello 意見工具，如需詳細說明。</span><span class="sxs-lookup"><span data-stu-id="cbd63-128">If you cannot find any self-signed certificates using hello above steps, contact us through hello feedback tool for more help.</span></span>

### <a name="unable-tooretrieve-subscriptions"></a><span data-ttu-id="cbd63-129">無法 tooretrieve 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cbd63-129">Unable tooretrieve subscriptions</span></span>

<span data-ttu-id="cbd63-130">如果您無法 tooretrieve 之後您訂用帳戶已成功登入，請遵循這些步驟 tootroubleshoot 此問題：</span><span class="sxs-lookup"><span data-stu-id="cbd63-130">If you are unable tooretrieve your subscriptions after you successfully sign in, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="cbd63-131">請確認您的帳戶具有存取 toohello 訂用帳戶，登入 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="cbd63-131">Verify that your account has access toohello subscriptions by signing into hello Azure Portal.</span></span>

- <span data-ttu-id="cbd63-132">請確定您已登入使用 hello 正確環境 （Azure、 Azure China、 Azure 德國、 Azure 美國政府或自訂 Azure 環境/堆疊）。</span><span class="sxs-lookup"><span data-stu-id="cbd63-132">Make sure that you have signed in using hello correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="cbd63-133">如果您在 proxy 背景，請確定您已正確設定 hello 存放裝置總管 proxy。</span><span class="sxs-lookup"><span data-stu-id="cbd63-133">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="cbd63-134">請嘗試移除並 hello 帳戶正在重新加入。</span><span class="sxs-lookup"><span data-stu-id="cbd63-134">Try removing and readding hello account.</span></span>

- <span data-ttu-id="cbd63-135">試著刪除下列檔案從根目錄 (亦即 C:\Users\ContosoUser)，然後再重新新增 hello 帳戶 hello:</span><span class="sxs-lookup"><span data-stu-id="cbd63-135">Try deleting hello following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding hello account:</span></span>

    - <span data-ttu-id="cbd63-136">.adalcache</span><span class="sxs-lookup"><span data-stu-id="cbd63-136">.adalcache</span></span>

    - <span data-ttu-id="cbd63-137">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="cbd63-137">.devaccounts</span></span>

    - <span data-ttu-id="cbd63-138">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="cbd63-138">.extaccounts</span></span>

- <span data-ttu-id="cbd63-139">監看式 hello 開發人員工具主控台 （藉由按 F12） 當您要登入的任何錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="cbd63-139">Watch hello developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![開發人員工具](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a><span data-ttu-id="cbd63-141">無法 toosee hello 驗證頁面</span><span class="sxs-lookup"><span data-stu-id="cbd63-141">Unable toosee hello authentication page</span></span>

<span data-ttu-id="cbd63-142">如果您無法 toosee hello 驗證 頁面上，請遵循這些步驟 tootroubleshoot 此問題：</span><span class="sxs-lookup"><span data-stu-id="cbd63-142">If you are unable toosee hello authentication page, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="cbd63-143">根據您的連線 hello 速度，它可能需要一些時間，hello 登入頁面 tooload、 等待至少一分鐘，再關閉 hello [驗證] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="cbd63-143">Depending on hello speed of your connection, it may take a while for hello sign-in page tooload, wait at least one minute before closing hello authentication dialog box.</span></span>

- <span data-ttu-id="cbd63-144">如果您在 proxy 背景，請確定您已正確設定 hello 存放裝置總管 proxy。</span><span class="sxs-lookup"><span data-stu-id="cbd63-144">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="cbd63-145">按 hello F12 鍵 hello 開發人員主控台檢視。</span><span class="sxs-lookup"><span data-stu-id="cbd63-145">View hello developer console by pressing hello F12 key.</span></span> <span data-ttu-id="cbd63-146">觀看 hello 回應 hello 開發人員主控台，並查看是否都可以找到任何線索為何無法運作的驗證。</span><span class="sxs-lookup"><span data-stu-id="cbd63-146">Watch hello responses from hello developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="cbd63-147">無法移除帳戶</span><span class="sxs-lookup"><span data-stu-id="cbd63-147">Cannot remove account</span></span>

<span data-ttu-id="cbd63-148">如果您無法 tooremove 帳戶，或是 hello 重新驗證連結不會執行任何動作，請遵循這些步驟 tootroubleshoot 此問題：</span><span class="sxs-lookup"><span data-stu-id="cbd63-148">If you are unable tooremove an account, or if hello reauthenticate link does not do anything, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="cbd63-149">試著刪除下列檔案從您的根目錄，並再正在重新加入 hello 帳戶 hello:</span><span class="sxs-lookup"><span data-stu-id="cbd63-149">Try deleting hello following files from your root directory, and then readding hello account:</span></span>

    - <span data-ttu-id="cbd63-150">.adalcache</span><span class="sxs-lookup"><span data-stu-id="cbd63-150">.adalcache</span></span>

    - <span data-ttu-id="cbd63-151">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="cbd63-151">.devaccounts</span></span>

    - <span data-ttu-id="cbd63-152">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="cbd63-152">.extaccounts</span></span>

- <span data-ttu-id="cbd63-153">如果您想 tooremove SAS 附加儲存體資源，請刪除下列檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbd63-153">If you want tooremove SAS attached Storage resources, delete hello following files:</span></span>

    - <span data-ttu-id="cbd63-154">Windows 是 %AppData%/StorageExplorer 資料夾</span><span class="sxs-lookup"><span data-stu-id="cbd63-154">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="cbd63-155">Mac 是 /Users/<您的名稱>/Library/Applicaiton SUpport/StorageExplorer</span><span class="sxs-lookup"><span data-stu-id="cbd63-155">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="cbd63-156">Linux 是 ~/.config/StorageExplorer</span><span class="sxs-lookup"><span data-stu-id="cbd63-156">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="cbd63-157">如果您刪除這些檔案您將有指定 tooreenter 您的認證。</span><span class="sxs-lookup"><span data-stu-id="cbd63-157">You will have tooreenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="cbd63-158">Proxy 問題</span><span class="sxs-lookup"><span data-stu-id="cbd63-158">Proxy issues</span></span>

<span data-ttu-id="cbd63-159">首先，請確定該 hello 遵循您所輸入的資訊都正確：</span><span class="sxs-lookup"><span data-stu-id="cbd63-159">First, make sure that hello following information you entered are all correct:</span></span>

- <span data-ttu-id="cbd63-160">hello proxy URL 和連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="cbd63-160">hello proxy URL and port number</span></span>

- <span data-ttu-id="cbd63-161">使用者名稱和密碼，如果所需的 hello proxy</span><span class="sxs-lookup"><span data-stu-id="cbd63-161">Username and password if required by hello proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="cbd63-162">常見的解決方案</span><span class="sxs-lookup"><span data-stu-id="cbd63-162">Common solutions</span></span>

<span data-ttu-id="cbd63-163">如果您仍然遇到問題，請遵循這些步驟 tootroubleshoot 它們：</span><span class="sxs-lookup"><span data-stu-id="cbd63-163">If you are still experiencing issues, follow these steps tootroubleshoot them:</span></span>

- <span data-ttu-id="cbd63-164">如果您可以連接 toohello 網際網路，而不使用 proxy，請確認儲存體總管就不會啟用 proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="cbd63-164">If you can connect toohello Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="cbd63-165">在 hello 情況下，可能是您的 proxy 設定發生問題。</span><span class="sxs-lookup"><span data-stu-id="cbd63-165">If this is hello case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="cbd63-166">使用 proxy 系統管理員 tooidentify hello 問題。</span><span class="sxs-lookup"><span data-stu-id="cbd63-166">Work with your proxy administrator tooidentify hello problems.</span></span>

- <span data-ttu-id="cbd63-167">請確認其他應用程式使用 hello proxy 伺服器會在如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="cbd63-167">Verify that other applications using hello proxy server work as expected.</span></span>

- <span data-ttu-id="cbd63-168">確認您能夠連線使用網頁瀏覽器 toohello Microsoft Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="cbd63-168">Verify that you can connect toohello Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="cbd63-169">確認您可以收到服務端點的回應。</span><span class="sxs-lookup"><span data-stu-id="cbd63-169">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="cbd63-170">在瀏覽器中輸入其中一個端點 URL。</span><span class="sxs-lookup"><span data-stu-id="cbd63-170">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="cbd63-171">如果可以連線，您應該會收到 InvalidQueryParameterValue 或類似的 XML 回應。</span><span class="sxs-lookup"><span data-stu-id="cbd63-171">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="cbd63-172">如果有其他人也用您的 proxy 伺服器使用儲存體總管，請確認他們可以連線。</span><span class="sxs-lookup"><span data-stu-id="cbd63-172">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="cbd63-173">如果它們可以連接，您可能必須 toocontact proxy 的伺服器管理員。</span><span class="sxs-lookup"><span data-stu-id="cbd63-173">If they can connect, you may have toocontact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="cbd63-174">診斷問題的工具</span><span class="sxs-lookup"><span data-stu-id="cbd63-174">Tools for diagnosing issues</span></span>

<span data-ttu-id="cbd63-175">如果您有網路的工具，例如 Fiddler 適用於 Windows，您可能無法 toodiagnose hello 問題，如下所示：</span><span class="sxs-lookup"><span data-stu-id="cbd63-175">If you have networking tools, such as Fiddler for Windows, you may be able toodiagnose hello problems as follows:</span></span>

- <span data-ttu-id="cbd63-176">如果您有 toowork 透過您的 proxy 時，您可能必須 tooconfigure 您網路的工具 tooconnect 透過 hello proxy。</span><span class="sxs-lookup"><span data-stu-id="cbd63-176">If you have toowork through your proxy, you may have tooconfigure your networking tool tooconnect through hello proxy.</span></span>

- <span data-ttu-id="cbd63-177">請檢查您的網路工具所使用的 hello 連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="cbd63-177">Check hello port number used by your networking tool.</span></span>

- <span data-ttu-id="cbd63-178">輸入 hello 本機主機 URL 和 hello 網路工具的連接埠號碼為儲存體總管 中的 proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="cbd63-178">Enter hello local host URL and hello networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="cbd63-179">如果此 isdone 正確，您的網路工具會啟動記錄提出儲存體總管 toomanagement 與服務端點的網路要求。</span><span class="sxs-lookup"><span data-stu-id="cbd63-179">If this isdone correctly, your networking tool starts logging network requests made by Storage Explorer toomanagement and service endpoints.</span></span> <span data-ttu-id="cbd63-180">例如，輸入您在瀏覽器中的 blob 端點 https://cawablobgrs.blob.core.windows.net/，而且您會收到回應類似於 hello 下列，建議 hello 資源存在，雖然您無法存取它。</span><span class="sxs-lookup"><span data-stu-id="cbd63-180">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles hello following, which suggests hello resource exists, although you cannot access it.</span></span>

![程式碼範例](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="cbd63-182">連絡 proxy 伺服器管理員</span><span class="sxs-lookup"><span data-stu-id="cbd63-182">Contact proxy server admin</span></span>

<span data-ttu-id="cbd63-183">如果您的 proxy 設定正確無誤，您可能必須 toocontact 您的 proxy 伺服器系統管理員，並</span><span class="sxs-lookup"><span data-stu-id="cbd63-183">If your proxy settings are correct, you may have toocontact your proxy server admin, and</span></span>

- <span data-ttu-id="cbd63-184">請確定您的 proxy 不會封鎖流量 tooAzure 管理或資源的端點。</span><span class="sxs-lookup"><span data-stu-id="cbd63-184">Make sure that your proxy does not block traffic tooAzure management or resource endpoints.</span></span>

- <span data-ttu-id="cbd63-185">請確認您的 proxy 伺服器所使用的 hello 驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="cbd63-185">Verify hello authentication protocol used by your proxy server.</span></span> <span data-ttu-id="cbd63-186">儲存體總管目前不支援 NTLM proxy。</span><span class="sxs-lookup"><span data-stu-id="cbd63-186">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-tooretrieve-children-error-message"></a><span data-ttu-id="cbd63-187">「 無法 tooRetrieve 子系 」 錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="cbd63-187">"Unable tooRetrieve Children" error message</span></span>

<span data-ttu-id="cbd63-188">如果您是透過 proxy 連線的 tooAzure，請確認您的 proxy 設定正確。</span><span class="sxs-lookup"><span data-stu-id="cbd63-188">If you are connected tooAzure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="cbd63-189">如果您已從 hello hello 訂用帳戶或帳戶的擁有者授與存取 tooa 資源，請確認您具有讀取或列出該資源的權限。</span><span class="sxs-lookup"><span data-stu-id="cbd63-189">If you were granted access tooa resource from hello owner of hello subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="cbd63-190">SAS URL 問題</span><span class="sxs-lookup"><span data-stu-id="cbd63-190">Issues with SAS URL</span></span>
<span data-ttu-id="cbd63-191">如果您要連接 tooa 服務使用 SAS URL，以及發生此錯誤：</span><span class="sxs-lookup"><span data-stu-id="cbd63-191">If you are connecting tooa service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="cbd63-192">確認 hello URL 提供 hello 必要的權限 tooread 或清單的資源。</span><span class="sxs-lookup"><span data-stu-id="cbd63-192">Verify that hello URL provides hello necessary permissions tooread or list resources.</span></span>

- <span data-ttu-id="cbd63-193">請確認該 hello URL 尚未過期。</span><span class="sxs-lookup"><span data-stu-id="cbd63-193">Verify that hello URL has not expired.</span></span>

- <span data-ttu-id="cbd63-194">如果 hello SAS URL 根據存取原則，請確認尚未撤銷 hello 存取原則。</span><span class="sxs-lookup"><span data-stu-id="cbd63-194">If hello SAS URL is based on an access policy, verify that hello access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbd63-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cbd63-195">Next steps</span></span>

<span data-ttu-id="cbd63-196">如果無 hello 方案為您的工作，送出 hello 與您的電子郵件的意見反應工具透過您的問題，而且可以包含做為您的 hello 問題的相關詳細資料，以便我們可以與您連絡以修正問題，hello。</span><span class="sxs-lookup"><span data-stu-id="cbd63-196">If none of hello solutions work for you, submit your issue through hello feedback tool with your email and as many details about hello issue included as you can, so that we can contact you for fixing hello issue.</span></span>

<span data-ttu-id="cbd63-197">toodo 此，依序按一下**協助**功能表，然後再按一下**傳送意見反應**。</span><span class="sxs-lookup"><span data-stu-id="cbd63-197">toodo this, click **Help** menu, and then click **Send Feedback**.</span></span>

![意見反應](./media/storage-explorer-troubleshooting/4022503_en_1.png)
