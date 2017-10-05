---
title: "自訂應用程式的 MFA 軟體開發套件 | Microsoft Docs"
description: "本文示範如何下載和使用 Azure MFA SDK 來啟用自訂應用程式的雙步驟驗證。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 281f9c61a30a20027f69808600373aa272255ef6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a><span data-ttu-id="0079a-103">在自訂應用程式中建置 Multi-Factor Authentication (SDK)</span><span class="sxs-lookup"><span data-stu-id="0079a-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span></span>

<span data-ttu-id="0079a-104">Azure Multi-Factor Authentication 軟體開發套件 (SDK) 可讓您將雙步驟驗證直接內建到 Azure AD 租用戶中的應用程式登入或交易程序。</span><span class="sxs-lookup"><span data-stu-id="0079a-104">The Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into the sign-in or transaction processes of applications in your Azure AD tenant.</span></span>

<span data-ttu-id="0079a-105">Multi-Factor Authentication SDK 適用於 C#、Visual Basic (.NET)、Java、Perl、PHP 和 Ruby。</span><span class="sxs-lookup"><span data-stu-id="0079a-105">The Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span></span> <span data-ttu-id="0079a-106">SDK 為雙步驟驗證加上一層精簡包裝函式。</span><span class="sxs-lookup"><span data-stu-id="0079a-106">The SDK provides a thin wrapper around two-step verification.</span></span> <span data-ttu-id="0079a-107">它包含您撰寫程式碼所需要的一切，包括加註的原始程式碼檔案、範例檔案，以及詳細的 ReadMe 檔案。</span><span class="sxs-lookup"><span data-stu-id="0079a-107">It includes everything you need to write your code, including commented source code files, example files, and a detailed ReadMe file.</span></span> <span data-ttu-id="0079a-108">每套 SDK 也會包含憑證和私密金鑰，用以加密 Multi-Factor Authentication 提供者獨有的交易。</span><span class="sxs-lookup"><span data-stu-id="0079a-108">Each SDK also includes a certificate and private key for encrypting transactions that are unique to your Multi-Factor Authentication Provider.</span></span> <span data-ttu-id="0079a-109">只要您有提供者，您就可以視需要下載許多種語言和格式的 SDK。</span><span class="sxs-lookup"><span data-stu-id="0079a-109">As long as you have a provider, you can download the SDK in as many languages and formats as you need.</span></span>

<span data-ttu-id="0079a-110">Multi-Factor Authentication SDK 中的 API 結構十分簡單。</span><span class="sxs-lookup"><span data-stu-id="0079a-110">The structure of the APIs in the Multi-Factor Authentication SDK is simple.</span></span> <span data-ttu-id="0079a-111">使用多因素選項參數 (例如驗證模式) 和使用者資料 (例如要撥打的電話號碼或要驗證的 PIN 碼)，透過單一函式來呼叫 API。</span><span class="sxs-lookup"><span data-stu-id="0079a-111">Make a single function call to an API with the multi-factor option parameters (like verification mode) and user data (like the telephone number to call or the PIN number to validate).</span></span> <span data-ttu-id="0079a-112">API 會將函式呼叫轉換成 Web 服務要求，再提交到以雲端為基礎的 Azure Multi-Factor Authentication Service。</span><span class="sxs-lookup"><span data-stu-id="0079a-112">The APIs translate the function call into web services requests to the cloud-based Azure Multi-Factor Authentication Service.</span></span> <span data-ttu-id="0079a-113">所有呼叫都必須參考每個 SDK 所包含的私人憑證。</span><span class="sxs-lookup"><span data-stu-id="0079a-113">All calls must include a reference to the private certificate that is included in every SDK.</span></span>

<span data-ttu-id="0079a-114">因為 API 無權存取 Azure Active Directory 中註冊的使用者，所以您必須在檔案或資料庫中提供使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="0079a-114">Because the APIs do not have access to users registered in Azure Active Directory, you must provide user information in a file or database.</span></span> <span data-ttu-id="0079a-115">API 也沒有提供註冊或使用者管理功能，所以您需要將這些程序內建到您的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="0079a-115">Also, the APIs do not provide enrollment or user management features, so you need to build these processes into your application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0079a-116">若要下載 SDK，即使您有 Azure MFA、AAD Premium 或 EMS 授權，還是需要建立 Azure 多因素驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="0079a-116">To download the SDK, you need to create an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span> <span data-ttu-id="0079a-117">如果您針對此用途建立 Azure 多因素驗證提供者，且已有授權，請務必使用**每個啟用的使用者**模型建立提供者。</span><span class="sxs-lookup"><span data-stu-id="0079a-117">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure to create the Provider with the **Per Enabled User** model.</span></span> <span data-ttu-id="0079a-118">然後，將提供者連結至包含 Azure MFA、Azure AD Premium 或 EMS 授權的目錄。</span><span class="sxs-lookup"><span data-stu-id="0079a-118">Then, link the Provider to the directory that contains the Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="0079a-119">這個組態可確保您只會在使用 SDK 的唯一使用者超過您所擁有的授權數目時收到帳單。</span><span class="sxs-lookup"><span data-stu-id="0079a-119">This configuration ensures that you are only billed if you have more unique users using the SDK than the number of licenses you own.</span></span>


## <a name="download-the-sdk"></a><span data-ttu-id="0079a-120">下載 SDK</span><span class="sxs-lookup"><span data-stu-id="0079a-120">Download the SDK</span></span>
<span data-ttu-id="0079a-121">下載 Azure Multi-factor SDK 需要 [Azure Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="0079a-121">Downloading the Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md).</span></span>  <span data-ttu-id="0079a-122">即使您擁有 Azure MFA、Azure AD Premium 或 Enterprise Mobility Suite 授權，這還是需要完整的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0079a-122">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span></span>  <span data-ttu-id="0079a-123">若要下載 SDK，請瀏覽至 Multi-Factor 管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="0079a-123">To download the SDK, navigate to the Multi-Factor Management Portal.</span></span> <span data-ttu-id="0079a-124">連接入口網站的方式是直接管理多因素驗證提供者，或按一下 MFA 服務設定頁面上的 [移至入口網站] 連結。</span><span class="sxs-lookup"><span data-stu-id="0079a-124">You can reach the portal either by managing the Multi-Factor Auth Provider directly, or by clicking the **"Go to the portal"** link on the MFA service settings page.</span></span>

### <a name="download-from-the-azure-classic-portal"></a><span data-ttu-id="0079a-125">從 Azure 傳統入口網站下載</span><span class="sxs-lookup"><span data-stu-id="0079a-125">Download from the Azure classic portal</span></span>
1. <span data-ttu-id="0079a-126">以系統管理員身分登入 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="0079a-126">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="0079a-127">選取左邊的 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="0079a-127">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="0079a-128">在 [Active Directory] 頁面頂端，選取 [多因素驗證提供者]</span><span class="sxs-lookup"><span data-stu-id="0079a-128">On the Active Directory page, at the top select **Multi-Factor Auth Providers**</span></span>
4. <span data-ttu-id="0079a-129">選取底部的 [管理]。</span><span class="sxs-lookup"><span data-stu-id="0079a-129">At the bottom select **Manage**.</span></span> <span data-ttu-id="0079a-130">新的頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="0079a-130">A new page opens.</span></span>
5. <span data-ttu-id="0079a-131">在左下方按一下 [SDK]。</span><span class="sxs-lookup"><span data-stu-id="0079a-131">On the left, at the bottom, click **SDK**.</span></span>
   <span data-ttu-id="0079a-132"><center>![下載](./media/multi-factor-authentication-sdk/download.png)</center></span><span class="sxs-lookup"><span data-stu-id="0079a-132"><center>![Download](./media/multi-factor-authentication-sdk/download.png)</center></span></span>
6. <span data-ttu-id="0079a-133">選取您想要的語言，然後按一下其中一個相關聯的下載連結。</span><span class="sxs-lookup"><span data-stu-id="0079a-133">Select the language you want and click one the associated download links.</span></span>
7. <span data-ttu-id="0079a-134">儲存下載內容。</span><span class="sxs-lookup"><span data-stu-id="0079a-134">Save the download.</span></span>

### <a name="download-from-the-service-settings"></a><span data-ttu-id="0079a-135">從服務設定下載</span><span class="sxs-lookup"><span data-stu-id="0079a-135">Download from the service settings</span></span>
1. <span data-ttu-id="0079a-136">以系統管理員身分登入 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="0079a-136">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="0079a-137">選取左邊的 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="0079a-137">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="0079a-138">按兩下您的 Azure AD 執行個體。</span><span class="sxs-lookup"><span data-stu-id="0079a-138">Double-click your instance of Azure AD.</span></span>
4. <span data-ttu-id="0079a-139">在頂端按一下  **設定**</span><span class="sxs-lookup"><span data-stu-id="0079a-139">At the top click **Configure**</span></span>
5. <span data-ttu-id="0079a-140">在多因素驗證底下選取 **管理服務設定**
   ![下載](./media/multi-factor-authentication-sdk/download2.png)</span><span class="sxs-lookup"><span data-stu-id="0079a-140">Under multi-factor authentication, select **Manage service settings**
![Download](./media/multi-factor-authentication-sdk/download2.png)</span></span>
6. <span data-ttu-id="0079a-141">在 [服務設定] 頁面上，於畫面底部按一下 [ **移至入口網站**]。</span><span class="sxs-lookup"><span data-stu-id="0079a-141">On the services settings page, at the bottom of the screen click **Go to the portal**.</span></span> <span data-ttu-id="0079a-142">新的頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="0079a-142">A new page opens.</span></span>
   <span data-ttu-id="0079a-143">![下載](./media/multi-factor-authentication-sdk/download3a.png)</span><span class="sxs-lookup"><span data-stu-id="0079a-143">![Download](./media/multi-factor-authentication-sdk/download3a.png)</span></span>
7. <span data-ttu-id="0079a-144">在左下方按一下 [SDK]。</span><span class="sxs-lookup"><span data-stu-id="0079a-144">On the left, at the bottom, click **SDK**.</span></span>
8. <span data-ttu-id="0079a-145">選取您想要的語言，然後按一下其中一個相關聯的下載連結。</span><span class="sxs-lookup"><span data-stu-id="0079a-145">Select the language you want and click one the associated download links.</span></span>
9. <span data-ttu-id="0079a-146">儲存下載內容。</span><span class="sxs-lookup"><span data-stu-id="0079a-146">Save the download.</span></span>

## <a name="whats-in-the-sdk"></a><span data-ttu-id="0079a-147">SDK 的內容</span><span class="sxs-lookup"><span data-stu-id="0079a-147">What's in the SDK</span></span>
<span data-ttu-id="0079a-148">SDK 包含下列各項：</span><span class="sxs-lookup"><span data-stu-id="0079a-148">The SDK includes the following items:</span></span>

* <span data-ttu-id="0079a-149">**讀我檔案**。</span><span class="sxs-lookup"><span data-stu-id="0079a-149">**README**.</span></span> <span data-ttu-id="0079a-150">說明如何在新的或現有的應用程式中使用 Multi-Factor Authentication API。</span><span class="sxs-lookup"><span data-stu-id="0079a-150">Explains how to use the Multi-Factor Authentication APIs in a new or existing application.</span></span>
* <span data-ttu-id="0079a-151">**原始程式檔**，用於 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="0079a-151">**Source files** for Multi-Factor Authentication</span></span>
* <span data-ttu-id="0079a-152">**用戶端憑證** </span><span class="sxs-lookup"><span data-stu-id="0079a-152">**Client certificate** that you use to communicate with the Multi-Factor Authentication service</span></span>
* <span data-ttu-id="0079a-153">**私密金鑰** </span><span class="sxs-lookup"><span data-stu-id="0079a-153">**Private key** for the certificate</span></span>
* <span data-ttu-id="0079a-154">**呼叫結果。**</span><span class="sxs-lookup"><span data-stu-id="0079a-154">**Call results.**</span></span> <span data-ttu-id="0079a-155">呼叫結果碼的清單。</span><span class="sxs-lookup"><span data-stu-id="0079a-155">A list of call result codes.</span></span> <span data-ttu-id="0079a-156">若要開啟此檔案，請使用可設定文字格式的應用程式，例如 WordPad。</span><span class="sxs-lookup"><span data-stu-id="0079a-156">To open this file, use an application with text formatting, such as WordPad.</span></span> <span data-ttu-id="0079a-157">使用呼叫結果碼來測試及疑難排解您在應用程式中的 Multi-Factor Authentication 實作。</span><span class="sxs-lookup"><span data-stu-id="0079a-157">Use the call result codes to test and troubleshoot the implementation of Multi-Factor Authentication in your application.</span></span> <span data-ttu-id="0079a-158">它們不是驗證狀態碼。</span><span class="sxs-lookup"><span data-stu-id="0079a-158">They are not authentication status codes.</span></span>
* <span data-ttu-id="0079a-159">**範例。**</span><span class="sxs-lookup"><span data-stu-id="0079a-159">**Examples.**</span></span> <span data-ttu-id="0079a-160">Multi-Factor Authentication 基本工作實作的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="0079a-160">Sample code for a basic working implementation of Multi-Factor Authentication.</span></span>

> [!WARNING]
> <span data-ttu-id="0079a-161">用戶端憑證是特別為您產生的唯一私人憑證。</span><span class="sxs-lookup"><span data-stu-id="0079a-161">The client certificate is a unique private certificate that was generated especially for you.</span></span> <span data-ttu-id="0079a-162">請勿分享或遺失此檔案。</span><span class="sxs-lookup"><span data-stu-id="0079a-162">Do not share or lose this file.</span></span> <span data-ttu-id="0079a-163">它是您與 Multi-Factor Authentication 通訊時確保安全性的關鍵。</span><span class="sxs-lookup"><span data-stu-id="0079a-163">It’s your key to ensuring the security of your communications with the Multi-Factor Authentication service.</span></span>

## <a name="code-sample"></a><span data-ttu-id="0079a-164">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="0079a-164">Code sample</span></span>
<span data-ttu-id="0079a-165">此程式碼範例示範如何使用 Azure Multi-Factor Authentication SDK 中的 API，將標準模式語音通話驗證加入至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0079a-165">This code sample shows you how to use the APIs in the Azure Multi-Factor Authentication SDK to add standard mode voice call verification to your application.</span></span> <span data-ttu-id="0079a-166">標準模式是指使用者按下 # 鍵來回應通話。</span><span class="sxs-lookup"><span data-stu-id="0079a-166">Standard mode is a telephone call that the user responds to by pressing the # key.</span></span>

<span data-ttu-id="0079a-167">此範例在含有 C# 伺服器端邏輯的基本 ASP.NET 應用程式中使用 C# .NET 2.0 Multi-Factor Authentication SDK，但程序與其他語言類似。</span><span class="sxs-lookup"><span data-stu-id="0079a-167">This example uses the C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but the process is similar in other languages.</span></span> <span data-ttu-id="0079a-168">因為 SDK 包含原始程式檔，而不是可執行檔，您可以建置檔案並參考它們，或直接將它們包含在您的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="0079a-168">Because the SDK includes source files, not executable files, you can build the files and reference them or include them directly in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="0079a-169">實作 Multi-Factor Authentication 時，請使用其他方法 (通話或簡訊) 做為第二或第三驗證，以補充您的主要驗證方法 (使用者名稱和密碼)。</span><span class="sxs-lookup"><span data-stu-id="0079a-169">When implementing Multi-Factor Authentication, use the additional methods (phone call or text message) as secondary or tertiary verification to supplement your primary authentication method (username and password).</span></span> <span data-ttu-id="0079a-170">這些方法並非設計為主要驗證方法。</span><span class="sxs-lookup"><span data-stu-id="0079a-170">These methods are not designed as primary authentication methods.</span></span>

### <a name="code-sample-overview"></a><span data-ttu-id="0079a-171">程式碼範例概觀</span><span class="sxs-lookup"><span data-stu-id="0079a-171">Code Sample Overview</span></span>
<span data-ttu-id="0079a-172">這是簡單 Web 示範應用程式的範例程式碼，使用 # 鍵回應通話來驗證使用者驗證。</span><span class="sxs-lookup"><span data-stu-id="0079a-172">This sample code for a simple web demo application uses a telephone call with a # key response to verify the user's authentication.</span></span> <span data-ttu-id="0079a-173">此通話因素在 Multi-Factor Authentication 中稱為標準模式。</span><span class="sxs-lookup"><span data-stu-id="0079a-173">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span></span>

<span data-ttu-id="0079a-174">用戶端程式碼不包含任何 Multi-Factor Authentication 特定項目。</span><span class="sxs-lookup"><span data-stu-id="0079a-174">The client-side code does not include any Multi-Factor Authentication-specific elements.</span></span> <span data-ttu-id="0079a-175">因為其他驗證因素與主要驗證無關，您可以新增它們而不必變更現有登入介面。</span><span class="sxs-lookup"><span data-stu-id="0079a-175">Because the additional authentication factors are independent of the primary authentication, you can add them without changing the existing sign-on interface.</span></span> <span data-ttu-id="0079a-176">Multi-Factor SDK 中的 API 可讓您自訂使用者經驗，但您可能完全不需要變更任何項目。</span><span class="sxs-lookup"><span data-stu-id="0079a-176">The APIs in the Multi-Factor SDK let you customize the user experience, but you might not need to change anything at all.</span></span>

<span data-ttu-id="0079a-177">伺服器端程式碼在步驟 2 新增標準模式驗證。</span><span class="sxs-lookup"><span data-stu-id="0079a-177">The server-side code adds standard-mode authentication in Step 2.</span></span> <span data-ttu-id="0079a-178">它使用標準模式驗證所需的參數建立 PfAuthParams 物件：使用者名稱、電話號碼、模式，以及每個呼叫都需要的用戶端憑證的路徑 (CertFilePath)。</span><span class="sxs-lookup"><span data-stu-id="0079a-178">It creates a PfAuthParams object with the parameters that are required for standard-mode verification: username, telephone number, and mode, and the path to the client certificate (CertFilePath), which is required in each call.</span></span> <span data-ttu-id="0079a-179">如需 PfAuthParams 中的所有參數的示範，請參閱 SDK 中的範例檔案。</span><span class="sxs-lookup"><span data-stu-id="0079a-179">For a demonstration of all parameters in PfAuthParams, see the Example file in the SDK.</span></span>

<span data-ttu-id="0079a-180">接下來，程式碼將 PfAuthParams 物件傳遞至 pf_authenticate() 函式。</span><span class="sxs-lookup"><span data-stu-id="0079a-180">Next, the code passes the PfAuthParams object to the pf_authenticate() function.</span></span> <span data-ttu-id="0079a-181">傳回值指出驗證成功或失敗。</span><span class="sxs-lookup"><span data-stu-id="0079a-181">The return value indicates the success or failure of the authentication.</span></span> <span data-ttu-id="0079a-182">Out 參數 callStatus 和 errorID 包含其他通話結果資訊。</span><span class="sxs-lookup"><span data-stu-id="0079a-182">The out parameters, callStatus, and errorID, contain additional call result information.</span></span> <span data-ttu-id="0079a-183">通話結果碼會記錄在 SDK 中的通話結果檔案。</span><span class="sxs-lookup"><span data-stu-id="0079a-183">The call result codes are documented in the call results file in the SDK.</span></span>

<span data-ttu-id="0079a-184">只需要幾行就能撰寫這個最小實作。</span><span class="sxs-lookup"><span data-stu-id="0079a-184">This minimal implementation can be written in a few lines.</span></span> <span data-ttu-id="0079a-185">不過，在實際執行的程式碼中，將會包含更複雜的錯誤處理、其他資料庫程式碼和強化的使用者經驗。</span><span class="sxs-lookup"><span data-stu-id="0079a-185">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span></span>

### <a name="web-client-code"></a><span data-ttu-id="0079a-186">Web 用戶端程式碼</span><span class="sxs-lookup"><span data-stu-id="0079a-186">Web Client Code</span></span>
<span data-ttu-id="0079a-187">以下是示範頁面的 Web 用戶端程式碼。</span><span class="sxs-lookup"><span data-stu-id="0079a-187">The following is web client code for a demo page.</span></span>

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a><span data-ttu-id="0079a-188">伺服器端程式碼</span><span class="sxs-lookup"><span data-stu-id="0079a-188">Server-Side Code</span></span>
<span data-ttu-id="0079a-189">在下列伺服器端程式碼中，步驟 2 中設定並執行 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="0079a-189">In the following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span></span> <span data-ttu-id="0079a-190">標準模式 (MODE_STANDARD) 是指使用者按下 # 鍵來回應通話。</span><span class="sxs-lookup"><span data-stu-id="0079a-190">Standard mode (MODE_STANDARD) is a telephone call to which the user responds by pressing the # key.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate the username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from the user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains the private key for the client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
