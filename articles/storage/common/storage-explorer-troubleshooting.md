---
title: "Azure 儲存體總管疑難排解指南 | Microsoft Docs"
description: "Azure 兩個偵錯功能的概觀"
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
ms.openlocfilehash: 470b2d87ffdc4769bb2963df7dea646901469e00
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="e2129-103">Azure 儲存體總管疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="e2129-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="e2129-104">簡介</span><span class="sxs-lookup"><span data-stu-id="e2129-104">Introduction</span></span>

<span data-ttu-id="e2129-105">Microsoft Azure 儲存體總管 (預覽) 是一個獨立應用程式，可讓您在 Windows、macOS 和 Linux 上輕鬆使用 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="e2129-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you to easily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="e2129-106">應用程式可以連接 Azure、Sovereign 雲端和 Azure Stack 所裝載的 toStorage 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2129-106">The app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="e2129-107">本指南摘要說明儲存體總管中常見的問題解決方案。</span><span class="sxs-lookup"><span data-stu-id="e2129-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="e2129-108">登入問題</span><span class="sxs-lookup"><span data-stu-id="e2129-108">Sign in issues</span></span>

<span data-ttu-id="e2129-109">在繼續之前，請先嘗試重新啟動您的應用程式，查看是否能修正問題。</span><span class="sxs-lookup"><span data-stu-id="e2129-109">Before you continue, try restarting your application and see whether the problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="e2129-110">錯誤：憑證鏈結中的自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="e2129-110">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="e2129-111">發生這個錯誤的原因有好幾個，最常見的兩個原因是：</span><span class="sxs-lookup"><span data-stu-id="e2129-111">There are several reasons why you may encounter this error, and the most common two reasons are as follows:</span></span>

1. <span data-ttu-id="e2129-112">應用程式是透過「透明 proxy」連線，這表示伺服器 (例如您公司的伺服器) 是使用自我簽署憑證攔截 HTTPS 流量、解密再加密。</span><span class="sxs-lookup"><span data-stu-id="e2129-112">The app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="e2129-113">您正在執行的應用程式，例如防毒軟體，會將自我簽署的 SSL 憑證插入您收到的 HTTPS 訊息中。</span><span class="sxs-lookup"><span data-stu-id="e2129-113">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into the HTTPS messages that you receive.</span></span>

<span data-ttu-id="e2129-114">當儲存體總管發生其中一個問題時，就不會知道所接收的 HTTPS 訊息是否遭竄改。</span><span class="sxs-lookup"><span data-stu-id="e2129-114">When Storage Explorer encounters one of the issues, it can no longer know whether the received HTTPS message is tampered.</span></span> <span data-ttu-id="e2129-115">如果您有一份自我簽署憑證，您可以讓儲存體總管信任該憑證。</span><span class="sxs-lookup"><span data-stu-id="e2129-115">If you have a copy of the self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="e2129-116">如果不確定是誰插入的憑證，請依照下列步驟來尋找憑證：</span><span class="sxs-lookup"><span data-stu-id="e2129-116">If you are unsure of who is injecting the certificate, follow these steps to find it:</span></span>

1. <span data-ttu-id="e2129-117">安裝 Open SSL</span><span class="sxs-lookup"><span data-stu-id="e2129-117">Install Open SSL</span></span>

    - <span data-ttu-id="e2129-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (任一輕裝版足可應對)</span><span class="sxs-lookup"><span data-stu-id="e2129-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of the light versions should be sufficient)</span></span>

    - <span data-ttu-id="e2129-119">Mac 和 Linux：應該包含在作業系統中</span><span class="sxs-lookup"><span data-stu-id="e2129-119">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="e2129-120">執行 Open SSL</span><span class="sxs-lookup"><span data-stu-id="e2129-120">Run Open SSL</span></span>

    - <span data-ttu-id="e2129-121">Windows：開啟安裝目錄，按一下 **/bin/**，再按兩下 **openssl.exe**。</span><span class="sxs-lookup"><span data-stu-id="e2129-121">Windows: open the installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="e2129-122">Mac 和 Linux：從終端機執行 **openssl**。</span><span class="sxs-lookup"><span data-stu-id="e2129-122">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="e2129-123">執行 s_client -showcerts -connect microsoft.com:443</span><span class="sxs-lookup"><span data-stu-id="e2129-123">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="e2129-124">尋找自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="e2129-124">Look for self-signed certificates.</span></span> <span data-ttu-id="e2129-125">如果不確定哪些是自我簽署的憑證，請尋找主旨 ("s:") 和簽發者 ("i:") 相同的所有位置。</span><span class="sxs-lookup"><span data-stu-id="e2129-125">If you are unsure which are self-signed, look for anywhere the subject ("s:") and issuer ("i:") are the same.</span></span>

5. <span data-ttu-id="e2129-126">發現任何自我簽署的憑證時，請將每個憑證從 **-----BEGIN CERTIFICATE-----** 到 **-----END CERTIFICATE-----** (含) 的所有內容，複製並貼到新的 .cer 檔案。</span><span class="sxs-lookup"><span data-stu-id="e2129-126">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** to a new .cer file.</span></span>

6. <span data-ttu-id="e2129-127">開啟儲存體總管，按一下 [編輯] > [SSL 憑證] > [匯入憑證]，然後使用檔案選擇器來尋找、選取及開啟您所建立的 .cer 檔案。</span><span class="sxs-lookup"><span data-stu-id="e2129-127">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use the file picker to find, select, and open the .cer files that you created.</span></span>

<span data-ttu-id="e2129-128">如果使用上述步驟找不到任何自我簽署的憑證，請透過意見反應工具與我們連絡，以取得更多協助。</span><span class="sxs-lookup"><span data-stu-id="e2129-128">If you cannot find any self-signed certificates using the above steps, contact us through the feedback tool for more help.</span></span>

### <a name="unable-to-retrieve-subscriptions"></a><span data-ttu-id="e2129-129">無法擷取訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e2129-129">Unable to retrieve subscriptions</span></span>

<span data-ttu-id="e2129-130">如果成功登入後無法擷取您的訂用帳戶，請依照下列步驟對此問題進行疑難排解：</span><span class="sxs-lookup"><span data-stu-id="e2129-130">If you are unable to retrieve your subscriptions after you successfully sign in, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="e2129-131">確認帳戶可以登入 Azure 入口網站存取訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2129-131">Verify that your account has access to the subscriptions by signing into the Azure Portal.</span></span>

- <span data-ttu-id="e2129-132">確定已使用正確的環境登入 (Azure、Azure 中國、Azure 德國、Azure 美國政府或自訂環境/Azure Stack)。</span><span class="sxs-lookup"><span data-stu-id="e2129-132">Make sure that you have signed in using the correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="e2129-133">如果您是在 proxy 背景，請確定已正確設定儲存體總管的 proxy。</span><span class="sxs-lookup"><span data-stu-id="e2129-133">If you are behind a proxy, make sure that you have configured the Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="e2129-134">嘗試移除再重新新增帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2129-134">Try removing and readding the account.</span></span>

- <span data-ttu-id="e2129-135">嘗試從根目錄 (亦即 C:\Users\ContosoUser) 刪除下列檔案，再重新新增帳戶：</span><span class="sxs-lookup"><span data-stu-id="e2129-135">Try deleting the following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding the account:</span></span>

    - <span data-ttu-id="e2129-136">.adalcache</span><span class="sxs-lookup"><span data-stu-id="e2129-136">.adalcache</span></span>

    - <span data-ttu-id="e2129-137">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="e2129-137">.devaccounts</span></span>

    - <span data-ttu-id="e2129-138">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="e2129-138">.extaccounts</span></span>

- <span data-ttu-id="e2129-139">登入出現任何錯誤訊息時，查看開發人員工具主控台 (按 F12)：</span><span class="sxs-lookup"><span data-stu-id="e2129-139">Watch the developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![開發人員工具](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-to-see-the-authentication-page"></a><span data-ttu-id="e2129-141">看不到驗證頁面</span><span class="sxs-lookup"><span data-stu-id="e2129-141">Unable to see the authentication page</span></span>

<span data-ttu-id="e2129-142">如果看不到驗證頁面，請依照下列步驟對此問題進行疑難排解：</span><span class="sxs-lookup"><span data-stu-id="e2129-142">If you are unable to see the authentication page, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="e2129-143">載入登入頁面可能需要一些時間，視連線速度而定，請等待至少一分鐘再關閉 [驗證] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="e2129-143">Depending on the speed of your connection, it may take a while for the sign-in page to load, wait at least one minute before closing the authentication dialog box.</span></span>

- <span data-ttu-id="e2129-144">如果您是在 proxy 背景，請確定已正確設定儲存體總管的 proxy。</span><span class="sxs-lookup"><span data-stu-id="e2129-144">If you are behind a proxy, make sure that you have configured the Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="e2129-145">按下 F12 鍵，檢視開發人員主控台。</span><span class="sxs-lookup"><span data-stu-id="e2129-145">View the developer console by pressing the F12 key.</span></span> <span data-ttu-id="e2129-146">查看開發人員主控台的回應，看看能否找到任何驗證無法運作的線索。</span><span class="sxs-lookup"><span data-stu-id="e2129-146">Watch the responses from the developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="e2129-147">無法移除帳戶</span><span class="sxs-lookup"><span data-stu-id="e2129-147">Cannot remove account</span></span>

<span data-ttu-id="e2129-148">如果無法移除帳戶，或重新驗證連結不執行任何動作，請依照下列步驟對此問題進行疑難排解：</span><span class="sxs-lookup"><span data-stu-id="e2129-148">If you are unable to remove an account, or if the reauthenticate link does not do anything, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="e2129-149">嘗試從根目錄刪除下列檔案，再重新新增帳戶：</span><span class="sxs-lookup"><span data-stu-id="e2129-149">Try deleting the following files from your root directory, and then readding the account:</span></span>

    - <span data-ttu-id="e2129-150">.adalcache</span><span class="sxs-lookup"><span data-stu-id="e2129-150">.adalcache</span></span>

    - <span data-ttu-id="e2129-151">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="e2129-151">.devaccounts</span></span>

    - <span data-ttu-id="e2129-152">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="e2129-152">.extaccounts</span></span>

- <span data-ttu-id="e2129-153">如果您想要移除 SAS 連接的儲存體資源，請刪除下列檔案：</span><span class="sxs-lookup"><span data-stu-id="e2129-153">If you want to remove SAS attached Storage resources, delete the following files:</span></span>

    - <span data-ttu-id="e2129-154">Windows 是 %AppData%/StorageExplorer 資料夾</span><span class="sxs-lookup"><span data-stu-id="e2129-154">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="e2129-155">Mac 是 /Users/<您的名稱>/Library/Applicaiton SUpport/StorageExplorer</span><span class="sxs-lookup"><span data-stu-id="e2129-155">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="e2129-156">Linux 是 ~/.config/StorageExplorer</span><span class="sxs-lookup"><span data-stu-id="e2129-156">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="e2129-157">如果刪除這些檔案，您必須重新輸入所有認證。</span><span class="sxs-lookup"><span data-stu-id="e2129-157">You will have to reenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="e2129-158">Proxy 問題</span><span class="sxs-lookup"><span data-stu-id="e2129-158">Proxy issues</span></span>

<span data-ttu-id="e2129-159">首先，確定您輸入的下列資訊都正確：</span><span class="sxs-lookup"><span data-stu-id="e2129-159">First, make sure that the following information you entered are all correct:</span></span>

- <span data-ttu-id="e2129-160">Proxy URL 和連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="e2129-160">The proxy URL and port number</span></span>

- <span data-ttu-id="e2129-161">使用者名稱和密碼 (如果 proxy 要求)</span><span class="sxs-lookup"><span data-stu-id="e2129-161">Username and password if required by the proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="e2129-162">常見的解決方案</span><span class="sxs-lookup"><span data-stu-id="e2129-162">Common solutions</span></span>

<span data-ttu-id="e2129-163">如果問題持續發生，請依照下列步驟進行疑難排解：</span><span class="sxs-lookup"><span data-stu-id="e2129-163">If you are still experiencing issues, follow these steps to troubleshoot them:</span></span>

- <span data-ttu-id="e2129-164">如果可以不使用 proxy 連接到網際網路，請確認儲存體總管不啟用 proxy 設定也能運作。</span><span class="sxs-lookup"><span data-stu-id="e2129-164">If you can connect to the Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="e2129-165">如果是這種情況，可能是 proxy 設定發生問題。</span><span class="sxs-lookup"><span data-stu-id="e2129-165">If this is the case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="e2129-166">請和您的 proxy 系統管理員合作找出問題。</span><span class="sxs-lookup"><span data-stu-id="e2129-166">Work with your proxy administrator to identify the problems.</span></span>

- <span data-ttu-id="e2129-167">確認使用 proxy 伺服器的其他應用程式是否如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="e2129-167">Verify that other applications using the proxy server work as expected.</span></span>

- <span data-ttu-id="e2129-168">確認可以使用網頁瀏覽器連接到 Microsoft Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e2129-168">Verify that you can connect to the Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="e2129-169">確認您可以收到服務端點的回應。</span><span class="sxs-lookup"><span data-stu-id="e2129-169">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="e2129-170">在瀏覽器中輸入其中一個端點 URL。</span><span class="sxs-lookup"><span data-stu-id="e2129-170">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="e2129-171">如果可以連線，您應該會收到 InvalidQueryParameterValue 或類似的 XML 回應。</span><span class="sxs-lookup"><span data-stu-id="e2129-171">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="e2129-172">如果有其他人也用您的 proxy 伺服器使用儲存體總管，請確認他們可以連線。</span><span class="sxs-lookup"><span data-stu-id="e2129-172">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="e2129-173">如果他們可以連線，您可能必須連絡您的 proxy 伺服器管理員。</span><span class="sxs-lookup"><span data-stu-id="e2129-173">If they can connect, you may have to contact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="e2129-174">診斷問題的工具</span><span class="sxs-lookup"><span data-stu-id="e2129-174">Tools for diagnosing issues</span></span>

<span data-ttu-id="e2129-175">如果您有網路工具，例如 Fiddler for Windows，您可以診斷問題，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e2129-175">If you have networking tools, such as Fiddler for Windows, you may be able to diagnose the problems as follows:</span></span>

- <span data-ttu-id="e2129-176">如果必須透過 proxy 工作，您可能必須設定網路工具透過 proxy 連線。</span><span class="sxs-lookup"><span data-stu-id="e2129-176">If you have to work through your proxy, you may have to configure your networking tool to connect through the proxy.</span></span>

- <span data-ttu-id="e2129-177">檢查網路工具使用的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="e2129-177">Check the port number used by your networking tool.</span></span>

- <span data-ttu-id="e2129-178">輸入本機主機 URL 和網路工具的連接埠號碼，當做儲存體總管的 proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="e2129-178">Enter the local host URL and the networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="e2129-179">如果作業正確，您的網路工具就會開始記錄儲存體總管向管理和服務端點提出的網路要求。</span><span class="sxs-lookup"><span data-stu-id="e2129-179">If this isdone correctly, your networking tool starts logging network requests made by Storage Explorer to management and service endpoints.</span></span> <span data-ttu-id="e2129-180">例如，在瀏覽器中輸入 blob 端點 https://cawablobgrs.blob.core.windows.net/，您會收到類似下面的回應，這表示雖然您無法存取，但資源確實存在。</span><span class="sxs-lookup"><span data-stu-id="e2129-180">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles the following, which suggests the resource exists, although you cannot access it.</span></span>

![程式碼範例](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="e2129-182">連絡 proxy 伺服器管理員</span><span class="sxs-lookup"><span data-stu-id="e2129-182">Contact proxy server admin</span></span>

<span data-ttu-id="e2129-183">如果 proxy 設定正確，您可能要連絡您的 proxy 伺服器管理員，並</span><span class="sxs-lookup"><span data-stu-id="e2129-183">If your proxy settings are correct, you may have to contact your proxy server admin, and</span></span>

- <span data-ttu-id="e2129-184">確定 proxy 不會封鎖 Azure 管理或資源端點的流量。</span><span class="sxs-lookup"><span data-stu-id="e2129-184">Make sure that your proxy does not block traffic to Azure management or resource endpoints.</span></span>

- <span data-ttu-id="e2129-185">確認 proxy 伺服器使用的驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="e2129-185">Verify the authentication protocol used by your proxy server.</span></span> <span data-ttu-id="e2129-186">儲存體總管目前不支援 NTLM proxy。</span><span class="sxs-lookup"><span data-stu-id="e2129-186">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-to-retrieve-children-error-message"></a><span data-ttu-id="e2129-187">「無法擷取子系」錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="e2129-187">"Unable to Retrieve Children" error message</span></span>

<span data-ttu-id="e2129-188">如果透過 proxy 連線至 Azure，請確認您的 proxy 設定正確無誤。</span><span class="sxs-lookup"><span data-stu-id="e2129-188">If you are connected to Azure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="e2129-189">如已獲授權可存取訂用帳戶或帳戶擁有者的資源，請確認您已閱讀或列出該資源的權限。</span><span class="sxs-lookup"><span data-stu-id="e2129-189">If you were granted access to a resource from the owner of the subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="e2129-190">SAS URL 問題</span><span class="sxs-lookup"><span data-stu-id="e2129-190">Issues with SAS URL</span></span>
<span data-ttu-id="e2129-191">如果要連線到使用 SAS URL 的服務，但發生此錯誤：</span><span class="sxs-lookup"><span data-stu-id="e2129-191">If you are connecting to a service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="e2129-192">請確認 URL 提供讀取或列出資源的必要權限。</span><span class="sxs-lookup"><span data-stu-id="e2129-192">Verify that the URL provides the necessary permissions to read or list resources.</span></span>

- <span data-ttu-id="e2129-193">請確認 URL 尚未過期。</span><span class="sxs-lookup"><span data-stu-id="e2129-193">Verify that the URL has not expired.</span></span>

- <span data-ttu-id="e2129-194">如果 SAS URL 是以存取原則為基礎，請確認尚未撤銷存取原則。</span><span class="sxs-lookup"><span data-stu-id="e2129-194">If the SAS URL is based on an access policy, verify that the access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2129-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e2129-195">Next steps</span></span>

<span data-ttu-id="e2129-196">如果這些解決方案都不能解決您的問題，請使用電子郵件透過意見反應工具提交您的問題，盡可能附上問題的詳細資料，以便我們與您連絡修正問題。</span><span class="sxs-lookup"><span data-stu-id="e2129-196">If none of the solutions work for you, submit your issue through the feedback tool with your email and as many details about the issue included as you can, so that we can contact you for fixing the issue.</span></span>

<span data-ttu-id="e2129-197">若要這樣做，請按一下 [說明] 功能表，再按一下 [傳送意見反應]**傳送回函**。</span><span class="sxs-lookup"><span data-stu-id="e2129-197">To do this, click **Help** menu, and then click **Send Feedback**.</span></span>

![意見反應](./media/storage-explorer-troubleshooting/4022503_en_1.png)
