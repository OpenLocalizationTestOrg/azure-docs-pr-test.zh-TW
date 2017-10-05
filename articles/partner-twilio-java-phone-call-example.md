---
title: "如何從 Twilio 撥打電話 (Java) | Microsoft Docs"
description: "了解如何在 Azure 上的 Java 應用程式中使用 Twilio 從網頁撥打電話。"
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 0381789e-e775-41a0-a784-294275192b1d
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 04ecb80a2a9e15b549b47138caf71c7e64bda500
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-make-a-phone-call-using-twilio-in-a-java-application-on-azure"></a><span data-ttu-id="6e57e-103">如何在 Azure 上的 Java 應用程式中使用 Twilio 撥打電話</span><span class="sxs-lookup"><span data-stu-id="6e57e-103">How to Make a Phone Call Using Twilio in a Java Application on Azure</span></span>
<span data-ttu-id="6e57e-104">下列範例將說明如何從 Azure 代管的網頁上使用 Twilio 撥打電話。</span><span class="sxs-lookup"><span data-stu-id="6e57e-104">The following example shows you how you can use Twilio to make a call from a web page hosted in Azure.</span></span> <span data-ttu-id="6e57e-105">產生的應用程式會提示使用者提供電話值，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="6e57e-105">The resulting application will prompt the user for phone call values, as shown in the following screen shot.</span></span>

![Azure Call Form Using Twilio and Java][twilio_java]

<span data-ttu-id="6e57e-107">您必須執行下列動作才能使用本主題中的程式碼：</span><span class="sxs-lookup"><span data-stu-id="6e57e-107">You'll need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="6e57e-108">取得 Twilio 帳戶和驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="6e57e-108">Acquire a Twilio account and authentication token.</span></span> <span data-ttu-id="6e57e-109">若要開始使用 Twilio，請在 [http://www.twilio.com/pricing][twilio_pricing] 上評估價格。</span><span class="sxs-lookup"><span data-stu-id="6e57e-109">To get started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="6e57e-110">您可以在註冊[https://www.twilio.com/try-twilio][try_twilio]。</span><span class="sxs-lookup"><span data-stu-id="6e57e-110">You can sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="6e57e-111">Twilio 提供的 API 的相關資訊，請參閱[http://www.twilio.com/api][twilio_api]。</span><span class="sxs-lookup"><span data-stu-id="6e57e-111">For information about the API provided by Twilio, see [http://www.twilio.com/api][twilio_api].</span></span>
2. <span data-ttu-id="6e57e-112">取得 Twilio JAR。</span><span class="sxs-lookup"><span data-stu-id="6e57e-112">Obtain the Twilio JAR.</span></span> <span data-ttu-id="6e57e-113">在 [https://github.com/twilio/twilio-java][twilio_java_github] 上，您可以下載 GitHub 來源及建立自己的 JAR，或下載預先建置的 JAR (可能有相依性)。</span><span class="sxs-lookup"><span data-stu-id="6e57e-113">At [https://github.com/twilio/twilio-java][twilio_java_github], you can download the GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
   <span data-ttu-id="6e57e-114">本主題中的程式碼是以預先建置的 TwilioJava-3.3.8-with-dependencies JAR 撰寫的。</span><span class="sxs-lookup"><span data-stu-id="6e57e-114">The code in this topic was written using the pre-built TwilioJava-3.3.8-with-dependencies JAR.</span></span>
3. <span data-ttu-id="6e57e-115">將 JAR 新增至您的 Java 建置路徑。</span><span class="sxs-lookup"><span data-stu-id="6e57e-115">Add the JAR to your Java build path.</span></span>
4. <span data-ttu-id="6e57e-116">如果您使用 Eclipse 建立此 Java 應用程式，請使用 Eclipse 的部署組件功能在應用程式部署檔案 (WAR) 中加入 Twilio JAR。</span><span class="sxs-lookup"><span data-stu-id="6e57e-116">If you are using Eclipse to create this Java application, include the Twilio JAR in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="6e57e-117">如果您並非使用 Eclipse 建立此 Java 應用程式，請確定 Twilio JAR 與您的 Java 應用程式包含在相同的 Azure 角色內，且已新增至應用程式的類別路徑。</span><span class="sxs-lookup"><span data-stu-id="6e57e-117">If you are not using Eclipse to create this Java application, ensure the Twilio JAR is included within the same Azure role as your Java application, and added to the class path of your application.</span></span>
5. <span data-ttu-id="6e57e-118">確定您的 cacerts 金鑰存放區包含 Equifax Secure Certificate Authority 憑證，且具有 MD5 指模 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (序號為 35:DE:F4:CF，SHA1 指模為 D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A)。</span><span class="sxs-lookup"><span data-stu-id="6e57e-118">Ensure your cacerts keystore contains the Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (the serial number is 35:DE:F4:CF and the SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="6e57e-119">這是 [https://api.twilio.com][twilio_api_service] 服務的憑證授權單位 (CA) 憑證，會在您使用 Twilio API 時受到呼叫。</span><span class="sxs-lookup"><span data-stu-id="6e57e-119">This is the certificate authority (CA) certificate for the [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="6e57e-120">此 CA 憑證新增至您的 JDK cacert 存放區的相關資訊，請參閱[新增憑證至 Java CA 憑證存放區][add_ca_cert]。</span><span class="sxs-lookup"><span data-stu-id="6e57e-120">For information about adding this CA certificate to your JDK's cacert store, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="6e57e-121">此外，熟悉的資訊[建立 Hello World 應用程式使用 Azure Toolkit for Eclipse][azure_java_eclipse_hello_world]，或與其他技術在裝載 Java 應用程式在 Azure 中的，如果您是強烈建議不要使用 Eclipse。</span><span class="sxs-lookup"><span data-stu-id="6e57e-121">Additionally, familiarity with the information at [Creating a Hello World Application Using the Azure Toolkit for Eclipse][azure_java_eclipse_hello_world], or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="6e57e-122">建立用以撥打電話的 Web 表單</span><span class="sxs-lookup"><span data-stu-id="6e57e-122">Create a web form for making a call</span></span>
<span data-ttu-id="6e57e-123">下列程式碼將說明如何建立 Web 表單，以擷取撥打電話所需的使用者資料。</span><span class="sxs-lookup"><span data-stu-id="6e57e-123">The following code shows how to create a web form to retrieve user data for making a call.</span></span> <span data-ttu-id="6e57e-124">在此範例中，我們新建立了名為 **TwilioCloud** 的動態 Web 專案，並將 **callform.jsp** 新增為 JSP 檔案。</span><span class="sxs-lookup"><span data-stu-id="6e57e-124">For purposes of this example, a new dynamic web project, named **TwilioCloud**, was created, and **callform.jsp** was added as a JSP file.</span></span>

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Automated call form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Make this call</b>.</p>
     <br/>
      <form action="makecall.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="callTo" value="" />
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="callFrom" value="" />
           </td>
         </tr>
         <tr>
           <td>Call message:</td>
           <td><input type="text" size=400 name="callText" value="Hello. This is the call text. Good bye." />
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Make this call" />
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-the-code-to-make-the-call"></a><span data-ttu-id="6e57e-125">建立用以撥打電話的程式碼</span><span class="sxs-lookup"><span data-stu-id="6e57e-125">Create the code to make the call</span></span>
<span data-ttu-id="6e57e-126">下列程式碼會在使用者完成 callform.jsp 所顯示的表單時受到呼叫，可用來建立通話訊息及產生通話。</span><span class="sxs-lookup"><span data-stu-id="6e57e-126">The following code, which is called when the user completes the form displayed by callform.jsp, creates the call message and generates the call.</span></span> <span data-ttu-id="6e57e-127">在此範例中，我們將名為 **makecall.jsp** 的 JSP 檔案新增至 **TwilioCloud** 專案。</span><span class="sxs-lookup"><span data-stu-id="6e57e-127">For purposes of this example, the JSP file is named **makecall.jsp** and was added to the **TwilioCloud** project.</span></span> <span data-ttu-id="6e57e-128">(在下方的程式碼中，請使用您的 Twilio 帳戶和驗證權杖，而不要使用指派給 **accountSID** 和 **authToken** 的預留位置值。)</span><span class="sxs-lookup"><span data-stu-id="6e57e-128">(Use your Twilio account and authentication token instead of the placeholder values assigned to **accountSID** and **authToken** in the code below.)</span></span>

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    import="java.util.*"
    import="com.twilio.*"
    import="com.twilio.sdk.*"
    import="com.twilio.sdk.resource.factory.*"
    import="com.twilio.sdk.resource.instance.*"
    pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Call processing happens here</title>
    </head>
    <body>
        <b>This is my make call page.</b><p/>
     <%
    try 
    {
         // Use your account SID and authentication token instead
         // of the placeholders shown here.
         String accountSID = "your_twilio_account";
         String authToken = "your_twilio_authentication_token";

         // Instantiate an instance of the Twilio client.     
         TwilioRestClient client;
         client = new TwilioRestClient(accountSID, authToken);

         // Retrieve the account, used later to retrieve the CallFactory.
         Account account = client.getAccount();

         // Display the client endpoint. 
         out.println("<p>Using Twilio endpoint " + client.getEndpoint() + ".</p>");

         // Display the API version.
         String APIVERSION = TwilioRestClient.DEFAULT_VERSION;
         out.println("<p>Twilio client API version is " + APIVERSION + ".</p>");

         // Retrieve the values entered by the user.
         String callTo = request.getParameter("callTo");  
         // The Outgoing Caller ID, used for the From parameter,
         // must have previously been verified with Twilio.
         String callFrom = request.getParameter("callFrom");
         String userText = request.getParameter("callText");

         // Replace spaces in the user's text with '%20', 
         // to make the text suitable for a URL.
         userText = userText.replace(" ", "%20");

         // Create a URL using the Twilio message and the user-entered text.
         String Url="http://twimlets.com/message";
         Url = Url + "?Message%5B0%5D=" + userText;

         // Display the message URL.
         out.println("<p>");
         out.println("The URL is " + Url);
         out.println("</p>");

         // Place the call From, To and URL values into a hash map. 
         HashMap<String, String> params = new HashMap<String, String>();
         params.put("From", callFrom);
         params.put("To", callTo);
         params.put("Url", Url);

         CallFactory callFactory = account.getCallFactory();
         Call call = callFactory.create(params);
         out.println("<p>Call status: " + call.getStatus()  + "</p>"); 
    } 
    catch (TwilioRestException e) 
    {
        out.println("<p>TwilioRestException encountered: " + e.getMessage() + "</p>");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    catch (Exception e) 
    {
        out.println("<p>Exception encountered: " + e.getMessage() + "");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    %>
    </body>
    </html>

<span data-ttu-id="6e57e-129">除了撥打電話以外，makecall.jsp 也會顯示 Twilio 端點、API 版本和通話狀態。</span><span class="sxs-lookup"><span data-stu-id="6e57e-129">In addition to making the call, makecall.jsp displays the Twilio endpoint, API version, and the call status.</span></span> <span data-ttu-id="6e57e-130">下列螢幕擷取畫面顯示其範例：</span><span class="sxs-lookup"><span data-stu-id="6e57e-130">An example is the following screen shot:</span></span>

![Azure Call Response Using Twilio and Java][twilio_java_response]

## <a name="run-the-application"></a><span data-ttu-id="6e57e-132">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="6e57e-132">Run the application</span></span>
<span data-ttu-id="6e57e-133">以下是執行應用程式; 的概要步驟詳細說明這些步驟可以找到在[建立 Hello World 應用程式使用 Azure Toolkit for Eclipse][azure_java_eclipse_hello_world]。</span><span class="sxs-lookup"><span data-stu-id="6e57e-133">Following are the high-level steps to run your application; details for these steps can be found at [Creating a Hello World Application Using the Azure Toolkit for Eclipse][azure_java_eclipse_hello_world].</span></span>

1. <span data-ttu-id="6e57e-134">將您的 TwilioCloud WAR 匯出至 Azure **approot** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="6e57e-134">Export your TwilioCloud WAR to the Azure **approot** folder.</span></span> 
2. <span data-ttu-id="6e57e-135">修改 **startup.cmd** ，以將 TwilioCloud WAR 解壓縮。</span><span class="sxs-lookup"><span data-stu-id="6e57e-135">Modify **startup.cmd** to unzip your TwilioCloud WAR.</span></span>
3. <span data-ttu-id="6e57e-136">針對計算模擬器編譯您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e57e-136">Compile your application for the compute emulator.</span></span>
4. <span data-ttu-id="6e57e-137">在計算模擬器中開始進行部署。</span><span class="sxs-lookup"><span data-stu-id="6e57e-137">Start your deployment in the compute emulator.</span></span>
5. <span data-ttu-id="6e57e-138">開啟瀏覽器，然後執行 **http://localhost:8080/TwilioCloud/callform.jsp**。</span><span class="sxs-lookup"><span data-stu-id="6e57e-138">Open a browser, and run **http://localhost:8080/TwilioCloud/callform.jsp**.</span></span>
6. <span data-ttu-id="6e57e-139">輸入表單中的值，按一下 [Make this call] ，然後在 makecall.jsp 中檢視結果。</span><span class="sxs-lookup"><span data-stu-id="6e57e-139">Enter values in the form, click **Make this call**, and then see the results in makecall.jsp.</span></span>

<span data-ttu-id="6e57e-140">當您做好部署至 Azure 的準備後，您可以針對雲端環境重新編譯部署、部署至 Azure，以及在瀏覽器中執行 http://your_hosted_name.cloudapp.net/TwilioCloud/callform.jsp (請將 your_hosted_name 取代為您的值)。</span><span class="sxs-lookup"><span data-stu-id="6e57e-140">When you are ready to deploy to Azure, recompile for deployment to the cloud, deploy to Azure, and run http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp in the browser (substitute your value for *your_hosted_name*).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e57e-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6e57e-141">Next steps</span></span>
<span data-ttu-id="6e57e-142">此程式可說明在 Azure 上的 Java 中使用 Twilio 的基本功能。</span><span class="sxs-lookup"><span data-stu-id="6e57e-142">This code was provided to show you basic functionality using Twilio in Java on Azure.</span></span> <span data-ttu-id="6e57e-143">在部署至生產環境中的 Azure 之前，您可以新增更多錯誤處理或其他功能。</span><span class="sxs-lookup"><span data-stu-id="6e57e-143">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="6e57e-144">例如：</span><span class="sxs-lookup"><span data-stu-id="6e57e-144">For example:</span></span>

* <span data-ttu-id="6e57e-145">除了使用 Web 表單以外，您也可以使用 Azure 儲存體 Blob 或 SQL Database 來儲存電話號碼和通話文字。</span><span class="sxs-lookup"><span data-stu-id="6e57e-145">Instead of using a web form, you could use Azure storage blobs or SQL Database to store phone numbers and call text.</span></span> <span data-ttu-id="6e57e-146">使用 java 的 Azure 儲存體 blob 的相關資訊，請參閱[如何使用 Blob 儲存體服務，將來自 Java][howto_blob_storage_java]。</span><span class="sxs-lookup"><span data-stu-id="6e57e-146">For information about using Azure storage blobs in Java, see [How to Use the Blob Storage Service from Java][howto_blob_storage_java].</span></span> <span data-ttu-id="6e57e-147">使用 java 的 SQL 資料庫的相關資訊，請參閱[在 Java 中使用 SQL Database][howto_sql_azure_java]。</span><span class="sxs-lookup"><span data-stu-id="6e57e-147">For information about using SQL Database in Java, see [Using SQL Database in Java][howto_sql_azure_java].</span></span>
* <span data-ttu-id="6e57e-148">您可以使用 **RoleEnvironment.getConfigurationSettings** ，從部署的組態設定中擷取 Twilio 帳戶 ID 和驗證權杖，而不要在 makecall.jsp 中進行值的硬式編碼。</span><span class="sxs-lookup"><span data-stu-id="6e57e-148">You could use **RoleEnvironment.getConfigurationSettings** to retrieve the Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding the values in makecall.jsp.</span></span> <span data-ttu-id="6e57e-149">如需有關資訊**RoleEnvironment**類別，請參閱[使用 Azure 服務執行階段程式庫之 JSP 中][ azure_runtime_jsp]和的Azure服務執行階段封裝文件[http://dl.windowsazure.com/javadoc][azure_javadoc]。</span><span class="sxs-lookup"><span data-stu-id="6e57e-149">For information about the **RoleEnvironment** class, see [Using the Azure Service Runtime Library in JSP][azure_runtime_jsp] and the Azure Service Runtime package documentation at [http://dl.windowsazure.com/javadoc][azure_javadoc].</span></span>
* <span data-ttu-id="6e57e-150">Makecall.jsp 程式碼會將 Twilio 提供的 URL，指派[http://twimlets.com/message][twimlet_message_url]至**Url**變數。</span><span class="sxs-lookup"><span data-stu-id="6e57e-150">The makecall.jsp code assigns a Twilio-provided URL, [http://twimlets.com/message][twimlet_message_url], to the **Url** variable.</span></span> <span data-ttu-id="6e57e-151">此 URL 會提供 Twilio 標記語言 (TwiML) 回應，告知 Twilio 應如何執行通話。</span><span class="sxs-lookup"><span data-stu-id="6e57e-151">This URL provides a Twilio Markup Language (TwiML) response that informs Twilio how to proceed with the call.</span></span> <span data-ttu-id="6e57e-152">例如，傳回的 TwiML 可能會包含 **&lt;Say&gt;** 動詞，而產生要傳達給受話方的文字。</span><span class="sxs-lookup"><span data-stu-id="6e57e-152">For example, the TwiML that is returned can contain a **&lt;Say&gt;** verb that results in text being spoken to the call recipient.</span></span> <span data-ttu-id="6e57e-153">而不是使用 Twilio 提供 URL，您可以建置自己的服務回應 Twilio 的要求。如需詳細資訊，請參閱[如何為語音和簡訊功能，在 Java 中使用 Twilio][howto_twilio_voice_sms_java]。</span><span class="sxs-lookup"><span data-stu-id="6e57e-153">Instead of using the Twilio-provided URL, you could build your own service to respond to Twilio's request; for more information, see [How to Use Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java].</span></span> <span data-ttu-id="6e57e-154">可以找到 TwiML 的詳細資訊，在[http://www.twilio.com/docs/api/twiml][twiml]，和其他相關資訊**&lt;說&gt;**和其他 Twilio 動詞命令，請參閱[http://www.twilio.com/docs/api/twiml/say][twilio_say]。</span><span class="sxs-lookup"><span data-stu-id="6e57e-154">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about **&lt;Say&gt;** and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="6e57e-155">閱讀 [https://www.twilio.com/docs/security][twilio_docs_security] 上的 Twilio 安全性指引。</span><span class="sxs-lookup"><span data-stu-id="6e57e-155">Read the Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="6e57e-156">如需 Twilio 的其他資訊，請參閱 [https://www.twilio.com/docs][twilio_docs]。</span><span class="sxs-lookup"><span data-stu-id="6e57e-156">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="6e57e-157">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6e57e-157">See Also</span></span>
* <span data-ttu-id="6e57e-158">[如何為語音和簡訊功能，在 Java 中的使用 Twilio][howto_twilio_voice_sms_java]</span><span class="sxs-lookup"><span data-stu-id="6e57e-158">[How to Use Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java]</span></span>
* <span data-ttu-id="6e57e-159">[新增憑證至 Java CA 憑證存放區][add_ca_cert]</span><span class="sxs-lookup"><span data-stu-id="6e57e-159">[Adding a Certificate to the Java CA Certificate Store][add_ca_cert]</span></span>

[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/api
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_java_github]: http://github.com/twilio/twilio-java
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[azure_java_eclipse_hello_world]: http://msdn.microsoft.com/library/windowsazure/hh690944.aspx
[howto_twilio_voice_sms_java]: partner-twilio-java-how-to-use-voice-sms.md
[howto_blob_storage_java]: http://www.windowsazure.com/develop/java/how-to-guides/blob-storage/
[howto_sql_azure_java]: http://msdn.microsoft.com/library/windowsazure/hh749029.aspx
[azure_runtime_jsp]: http://msdn.microsoft.com/library/windowsazure/hh690948.aspx
[azure_javadoc]: http://dl.windowsazure.com/javadoc
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[twilio_java]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaCallForm.jpg
[twilio_java_response]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaMakeCall.jpg
