---
title: "aaaHow tooMake 來電 Twilio (Java) |Microsoft 文件"
description: "了解 toomake 電話如何從網頁上，在 Azure 上的 Java 應用程式中使用 Twilio 呼叫。"
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
ms.openlocfilehash: 04fe5a78d431a79790dee3ca75c2b004aea4345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-java-application-on-azure"></a><span data-ttu-id="f987e-103">如何在 Java 應用程式在 Azure 上的電話使用 Twilio tooMake</span><span class="sxs-lookup"><span data-stu-id="f987e-103">How tooMake a Phone Call Using Twilio in a Java Application on Azure</span></span>
<span data-ttu-id="f987e-104">hello 下列範例示範您如何使用 Twilio toomake 呼叫，以從 Azure 中裝載的網頁。</span><span class="sxs-lookup"><span data-stu-id="f987e-104">hello following example shows you how you can use Twilio toomake a call from a web page hosted in Azure.</span></span> <span data-ttu-id="f987e-105">hello 產生應用程式會提示 hello 使用者通話值 hello 下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="f987e-105">hello resulting application will prompt hello user for phone call values, as shown in hello following screen shot.</span></span>

![Azure Call Form Using Twilio and Java][twilio_java]

<span data-ttu-id="f987e-107">您將需要 toodo hello 下列 toouse 本主題中的 hello 程式碼：</span><span class="sxs-lookup"><span data-stu-id="f987e-107">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="f987e-108">取得 Twilio 帳戶和驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="f987e-108">Acquire a Twilio account and authentication token.</span></span> <span data-ttu-id="f987e-109">開始使用 Twilio，tooget 評估在定價[http://www.twilio.com/pricing][twilio_pricing]。</span><span class="sxs-lookup"><span data-stu-id="f987e-109">tooget started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="f987e-110">您可以在註冊[https://www.twilio.com/try-twilio][try_twilio]。</span><span class="sxs-lookup"><span data-stu-id="f987e-110">You can sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="f987e-111">Hello Twilio 所提供的 API 的相關資訊，請參閱[http://www.twilio.com/api][twilio_api]。</span><span class="sxs-lookup"><span data-stu-id="f987e-111">For information about hello API provided by Twilio, see [http://www.twilio.com/api][twilio_api].</span></span>
2. <span data-ttu-id="f987e-112">取得 hello Twilio JAR。</span><span class="sxs-lookup"><span data-stu-id="f987e-112">Obtain hello Twilio JAR.</span></span> <span data-ttu-id="f987e-113">在[https://github.com/twilio/twilio-java][twilio_java_github]，您可以下載 hello GitHub 來源並建立您自己的 JAR，或下載預先建立的 JAR （不論有無相依性）。</span><span class="sxs-lookup"><span data-stu-id="f987e-113">At [https://github.com/twilio/twilio-java][twilio_java_github], you can download hello GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
   <span data-ttu-id="f987e-114">使用預先建置 TwilioJava 3.3.8-與-相依性 JAR hello 寫入 hello 本主題中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f987e-114">hello code in this topic was written using hello pre-built TwilioJava-3.3.8-with-dependencies JAR.</span></span>
3. <span data-ttu-id="f987e-115">新增 hello JAR tooyour Java 建置路徑。</span><span class="sxs-lookup"><span data-stu-id="f987e-115">Add hello JAR tooyour Java build path.</span></span>
4. <span data-ttu-id="f987e-116">如果您使用 Eclipse toocreate 此 Java 應用程式，包括 hello Twilio JAR 應用程式部署檔案中 (WAR) 使用 Eclipse 的部署組件功能。</span><span class="sxs-lookup"><span data-stu-id="f987e-116">If you are using Eclipse toocreate this Java application, include hello Twilio JAR in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="f987e-117">如果您未使用 Eclipse toocreate 此 Java 應用程式，請確定 hello Twilio JAR 內含 hello 做為您的 Java 應用程式，並將它們加入 toohello 類別路徑，您的應用程式的 Azure 角色相同。</span><span class="sxs-lookup"><span data-stu-id="f987e-117">If you are not using Eclipse toocreate this Java application, ensure hello Twilio JAR is included within hello same Azure role as your Java application, and added toohello class path of your application.</span></span>
5. <span data-ttu-id="f987e-118">確定您 cacerts 金鑰存放區包含 hello Equifax 安全憑證授權單位憑證的 MD5 指紋 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello 序列值為 35:DE:F4:CF，hello SHA1 指紋為 D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A)。</span><span class="sxs-lookup"><span data-stu-id="f987e-118">Ensure your cacerts keystore contains hello Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello serial number is 35:DE:F4:CF and hello SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="f987e-119">這是 hello hello 憑證授權單位 (CA) 憑證[https://api.twilio.com] [ twilio_api_service]服務，當您使用 Twilio Api 時呼叫。</span><span class="sxs-lookup"><span data-stu-id="f987e-119">This is hello certificate authority (CA) certificate for hello [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="f987e-120">新增此 CA 憑證 tooyour JDK cacert 存放區的相關資訊，請參閱[加入 Java CA 憑證存放區的憑證 toohello][add_ca_cert]。</span><span class="sxs-lookup"><span data-stu-id="f987e-120">For information about adding this CA certificate tooyour JDK's cacert store, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="f987e-121">此外，在 hello 資訊的熟悉度[建立 Hello World 應用程式使用 hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world]，或與其他技術在裝載 Java 應用程式在 Azure 如果您不使用 Eclipse，強烈建議。</span><span class="sxs-lookup"><span data-stu-id="f987e-121">Additionally, familiarity with hello information at [Creating a Hello World Application Using hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world], or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="f987e-122">建立用以撥打電話的 Web 表單</span><span class="sxs-lookup"><span data-stu-id="f987e-122">Create a web form for making a call</span></span>
<span data-ttu-id="f987e-123">下列程式碼的 hello 顯示 toocreate web 表單 tooretrieve 進行呼叫的使用者資料的方式。</span><span class="sxs-lookup"><span data-stu-id="f987e-123">hello following code shows how toocreate a web form tooretrieve user data for making a call.</span></span> <span data-ttu-id="f987e-124">在此範例中，我們新建立了名為 **TwilioCloud** 的動態 Web 專案，並將 **callform.jsp** 新增為 JSP 檔案。</span><span class="sxs-lookup"><span data-stu-id="f987e-124">For purposes of this example, a new dynamic web project, named **TwilioCloud**, was created, and **callform.jsp** was added as a JSP file.</span></span>

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
           <td><input type="text" size=400 name="callText" value="Hello. This is hello call text. Good bye." />
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

## <a name="create-hello-code-toomake-hello-call"></a><span data-ttu-id="f987e-125">建立 hello 程式碼 toomake hello 呼叫</span><span class="sxs-lookup"><span data-stu-id="f987e-125">Create hello code toomake hello call</span></span>
<span data-ttu-id="f987e-126">hello 下列程式碼會呼叫 hello 使用者完成 hello callform.jsp 所顯示的表單時，會建立 hello 呼叫訊息並產生 hello 呼叫。</span><span class="sxs-lookup"><span data-stu-id="f987e-126">hello following code, which is called when hello user completes hello form displayed by callform.jsp, creates hello call message and generates hello call.</span></span> <span data-ttu-id="f987e-127">基於此範例中，名為 hello JSP 檔案**makecall.jsp** ，並且加入 toohello **TwilioCloud**專案。</span><span class="sxs-lookup"><span data-stu-id="f987e-127">For purposes of this example, hello JSP file is named **makecall.jsp** and was added toohello **TwilioCloud** project.</span></span> <span data-ttu-id="f987e-128">(使用您的 Twilio 帳戶和驗證語彙基元而非 hello 預留位置值太指派**accountSID**和**authToken** hello 的下列程式碼。)</span><span class="sxs-lookup"><span data-stu-id="f987e-128">(Use your Twilio account and authentication token instead of hello placeholder values assigned too**accountSID** and **authToken** in hello code below.)</span></span>

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
         // of hello placeholders shown here.
         String accountSID = "your_twilio_account";
         String authToken = "your_twilio_authentication_token";

         // Instantiate an instance of hello Twilio client.     
         TwilioRestClient client;
         client = new TwilioRestClient(accountSID, authToken);

         // Retrieve hello account, used later tooretrieve hello CallFactory.
         Account account = client.getAccount();

         // Display hello client endpoint. 
         out.println("<p>Using Twilio endpoint " + client.getEndpoint() + ".</p>");

         // Display hello API version.
         String APIVERSION = TwilioRestClient.DEFAULT_VERSION;
         out.println("<p>Twilio client API version is " + APIVERSION + ".</p>");

         // Retrieve hello values entered by hello user.
         String callTo = request.getParameter("callTo");  
         // hello Outgoing Caller ID, used for hello From parameter,
         // must have previously been verified with Twilio.
         String callFrom = request.getParameter("callFrom");
         String userText = request.getParameter("callText");

         // Replace spaces in hello user's text with '%20', 
         // toomake hello text suitable for a URL.
         userText = userText.replace(" ", "%20");

         // Create a URL using hello Twilio message and hello user-entered text.
         String Url="http://twimlets.com/message";
         Url = Url + "?Message%5B0%5D=" + userText;

         // Display hello message URL.
         out.println("<p>");
         out.println("hello URL is " + Url);
         out.println("</p>");

         // Place hello call From, tooand URL values into a hash map. 
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

<span data-ttu-id="f987e-129">此外 toomaking hello 呼叫、 makecall.jsp 顯示 hello Twilio 端點、 應用程式開發介面版本，以及 hello 呼叫狀態。</span><span class="sxs-lookup"><span data-stu-id="f987e-129">In addition toomaking hello call, makecall.jsp displays hello Twilio endpoint, API version, and hello call status.</span></span> <span data-ttu-id="f987e-130">下列螢幕擷取畫面的 hello 是範例：</span><span class="sxs-lookup"><span data-stu-id="f987e-130">An example is hello following screen shot:</span></span>

![Azure Call Response Using Twilio and Java][twilio_java_response]

## <a name="run-hello-application"></a><span data-ttu-id="f987e-132">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="f987e-132">Run hello application</span></span>
<span data-ttu-id="f987e-133">下列是 hello 高階步驟 toorun 您的應用程式。詳細說明這些步驟可以找到在[建立 Hello World 應用程式使用 hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world]。</span><span class="sxs-lookup"><span data-stu-id="f987e-133">Following are hello high-level steps toorun your application; details for these steps can be found at [Creating a Hello World Application Using hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world].</span></span>

1. <span data-ttu-id="f987e-134">匯出您 TwilioCloud WAR toohello Azure **approot**資料夾。</span><span class="sxs-lookup"><span data-stu-id="f987e-134">Export your TwilioCloud WAR toohello Azure **approot** folder.</span></span> 
2. <span data-ttu-id="f987e-135">修改**startup.cmd** toounzip TwilioCloud WAR。</span><span class="sxs-lookup"><span data-stu-id="f987e-135">Modify **startup.cmd** toounzip your TwilioCloud WAR.</span></span>
3. <span data-ttu-id="f987e-136">編譯您的應用程式的 hello 計算模擬器。</span><span class="sxs-lookup"><span data-stu-id="f987e-136">Compile your application for hello compute emulator.</span></span>
4. <span data-ttu-id="f987e-137">Hello 計算模擬器中啟動您的部署。</span><span class="sxs-lookup"><span data-stu-id="f987e-137">Start your deployment in hello compute emulator.</span></span>
5. <span data-ttu-id="f987e-138">開啟瀏覽器，然後執行 **http://localhost:8080/TwilioCloud/callform.jsp**。</span><span class="sxs-lookup"><span data-stu-id="f987e-138">Open a browser, and run **http://localhost:8080/TwilioCloud/callform.jsp**.</span></span>
6. <span data-ttu-id="f987e-139">在 hello 表單中輸入值，請按一下**進行這個呼叫**，然後查看 makecall.jsp hello 結果。</span><span class="sxs-lookup"><span data-stu-id="f987e-139">Enter values in hello form, click **Make this call**, and then see hello results in makecall.jsp.</span></span>

<span data-ttu-id="f987e-140">當您準備好 toodeploy tooAzure，部署 toohello 雲端重新編譯、 部署 tooAzure，以及執行 http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp hello 瀏覽器中的 (您值取代為*your_hosted_name*)。</span><span class="sxs-lookup"><span data-stu-id="f987e-140">When you are ready toodeploy tooAzure, recompile for deployment toohello cloud, deploy tooAzure, and run http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp in hello browser (substitute your value for *your_hosted_name*).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f987e-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f987e-141">Next steps</span></span>
<span data-ttu-id="f987e-142">此程式碼提供 tooshow 您基本的功能在 Azure 上使用 Twilio 在 Java 中的。</span><span class="sxs-lookup"><span data-stu-id="f987e-142">This code was provided tooshow you basic functionality using Twilio in Java on Azure.</span></span> <span data-ttu-id="f987e-143">在部署之前 tooAzure 在生產環境中的，您可能想要 tooadd 詳細的錯誤處理或其他功能。</span><span class="sxs-lookup"><span data-stu-id="f987e-143">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="f987e-144">例如：</span><span class="sxs-lookup"><span data-stu-id="f987e-144">For example:</span></span>

* <span data-ttu-id="f987e-145">而不是使用網頁表單，也可以使用 Azure 儲存體 blob 或 SQL Database toostore 電話號碼，並呼叫的文字。</span><span class="sxs-lookup"><span data-stu-id="f987e-145">Instead of using a web form, you could use Azure storage blobs or SQL Database toostore phone numbers and call text.</span></span> <span data-ttu-id="f987e-146">使用 java 的 Azure 儲存體 blob 的相關資訊，請參閱[tooUse hello 來自 Java 的 Blob 儲存體服務的方式][howto_blob_storage_java]。</span><span class="sxs-lookup"><span data-stu-id="f987e-146">For information about using Azure storage blobs in Java, see [How tooUse hello Blob Storage Service from Java][howto_blob_storage_java].</span></span> <span data-ttu-id="f987e-147">使用 java 的 SQL 資料庫的相關資訊，請參閱[在 Java 中使用 SQL Database][howto_sql_azure_java]。</span><span class="sxs-lookup"><span data-stu-id="f987e-147">For information about using SQL Database in Java, see [Using SQL Database in Java][howto_sql_azure_java].</span></span>
* <span data-ttu-id="f987e-148">您可以使用**RoleEnvironment.getConfigurationSettings** tooretrieve hello Twilio 帳戶識別碼和驗證語彙基元從您的部署組態設定，而不是硬式編碼 makecall.jsp 中的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="f987e-148">You could use **RoleEnvironment.getConfigurationSettings** tooretrieve hello Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding hello values in makecall.jsp.</span></span> <span data-ttu-id="f987e-149">如需 hello **RoleEnvironment**類別，請參閱[使用 hello Azure 之 JSP 中服務執行階段程式庫][ azure_runtime_jsp]和 hello Azure 服務執行階段封裝文件，網址[http://dl.windowsazure.com/javadoc][azure_javadoc]。</span><span class="sxs-lookup"><span data-stu-id="f987e-149">For information about hello **RoleEnvironment** class, see [Using hello Azure Service Runtime Library in JSP][azure_runtime_jsp] and hello Azure Service Runtime package documentation at [http://dl.windowsazure.com/javadoc][azure_javadoc].</span></span>
* <span data-ttu-id="f987e-150">hello makecall.jsp 程式碼會將 Twilio 提供的 URL，指派[http://twimlets.com/message][twimlet_message_url]，toohello **Url**變數。</span><span class="sxs-lookup"><span data-stu-id="f987e-150">hello makecall.jsp code assigns a Twilio-provided URL, [http://twimlets.com/message][twimlet_message_url], toohello **Url** variable.</span></span> <span data-ttu-id="f987e-151">此 URL 提供通知以 hello tooproceed 如何呼叫的 Twilio Twilio 標記語言 (TwiML) 回應。</span><span class="sxs-lookup"><span data-stu-id="f987e-151">This URL provides a Twilio Markup Language (TwiML) response that informs Twilio how tooproceed with hello call.</span></span> <span data-ttu-id="f987e-152">例如，可以包含 hello TwiML 傳回**&lt;說&gt;**正在口語的 toohello 呼叫收件者的文字會產生的指令動詞。</span><span class="sxs-lookup"><span data-stu-id="f987e-152">For example, hello TwiML that is returned can contain a **&lt;Say&gt;** verb that results in text being spoken toohello call recipient.</span></span> <span data-ttu-id="f987e-153">而不是使用 hello Twilio 提供 URL，您可以建置自己服務 toorespond tooTwilio 要求。如需詳細資訊，請參閱[如何 tooUse 語音和簡訊功能，在 Java 中 Twilio][howto_twilio_voice_sms_java]。</span><span class="sxs-lookup"><span data-stu-id="f987e-153">Instead of using hello Twilio-provided URL, you could build your own service toorespond tooTwilio's request; for more information, see [How tooUse Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java].</span></span> <span data-ttu-id="f987e-154">可以找到 TwiML 的詳細資訊，在[http://www.twilio.com/docs/api/twiml][twiml]，和其他相關資訊**&lt;說&gt;**和其他 Twilio 動詞命令，請參閱[http://www.twilio.com/docs/api/twiml/say][twilio_say]。</span><span class="sxs-lookup"><span data-stu-id="f987e-154">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about **&lt;Say&gt;** and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="f987e-155">讀取 hello Twilio 安全性指導方針，在[https://www.twilio.com/docs/security][twilio_docs_security]。</span><span class="sxs-lookup"><span data-stu-id="f987e-155">Read hello Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="f987e-156">如需 Twilio 的其他資訊，請參閱 [https://www.twilio.com/docs][twilio_docs]。</span><span class="sxs-lookup"><span data-stu-id="f987e-156">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="f987e-157">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f987e-157">See Also</span></span>
* <span data-ttu-id="f987e-158">[如何 tooUse Twilio 語音和簡訊功能，在 Java 中][howto_twilio_voice_sms_java]</span><span class="sxs-lookup"><span data-stu-id="f987e-158">[How tooUse Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java]</span></span>
* <span data-ttu-id="f987e-159">[新增憑證 toohello Java CA 憑證存放區][add_ca_cert]</span><span class="sxs-lookup"><span data-stu-id="f987e-159">[Adding a Certificate toohello Java CA Certificate Store][add_ca_cert]</span></span>

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
