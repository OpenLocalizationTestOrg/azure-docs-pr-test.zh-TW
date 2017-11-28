---
title: "aaaHow tooConfigure TLS 相互驗證 Web 應用程式"
description: "了解如何 tooconfigure web 應用程式 toouse 用戶端憑證驗證在 TLS。"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: cd1d15d3-2d9e-4502-9f11-a306dac4453a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2016
ms.author: naziml
ms.openlocfilehash: 8aeb9b35058fac50b8b38f6428207ad4a82d8637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-tls-mutual-authentication-for-web-app"></a><span data-ttu-id="35492-103">如何 tooConfigure TLS 相互驗證 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="35492-103">How tooConfigure TLS Mutual Authentication for Web App</span></span>
## <a name="overview"></a><span data-ttu-id="35492-104">概觀</span><span class="sxs-lookup"><span data-stu-id="35492-104">Overview</span></span>
<span data-ttu-id="35492-105">您可以藉由啟用不同類型的驗證，來限制存取 tooyour Azure web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="35492-105">You can restrict access tooyour Azure web app by enabling different types of authentication for it.</span></span> <span data-ttu-id="35492-106">其中一種方式 toodo 是 tooauthenticate hello 要求是透過 TLS/SSL 時，使用用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="35492-106">One way toodo so is tooauthenticate using a client certificate when hello request is over TLS/SSL.</span></span> <span data-ttu-id="35492-107">這項機制稱為 TLS 相互驗證或用戶端憑證驗證，本文會詳細說明如何 toosetup 您 web 應用程式 toouse 用戶端憑證驗證。</span><span class="sxs-lookup"><span data-stu-id="35492-107">This mechanism is called TLS mutual authentication or client certificate authentication and this article will detail how toosetup your web app toouse client certificate authentication.</span></span>

> <span data-ttu-id="35492-108">**附註：** 如果您透過 HTTP 存取您的網站，而非 HTTPS，將不會收到任何用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="35492-108">**Note:** If you access your site over HTTP and not HTTPS, you will not receive any client certificate.</span></span> <span data-ttu-id="35492-109">因此您的應用程式需要用戶端憑證，如果您不應該允許要求 tooyour 應用程式透過 HTTP。</span><span class="sxs-lookup"><span data-stu-id="35492-109">So if your application requires client certificates you should not allow requests tooyour application over HTTP.</span></span>
> 
> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="configure-web-app-for-client-certificate-authentication"></a><span data-ttu-id="35492-110">設定 Web 應用程式進行用戶端憑證驗證</span><span class="sxs-lookup"><span data-stu-id="35492-110">Configure Web App for Client Certificate Authentication</span></span>
<span data-ttu-id="35492-111">您 web 應用程式 toorequire 用戶端的憑證需要 tooadd hello clientCertEnabled 站台設定您的 web 應用程式，並將它設定 tootrue toosetup。</span><span class="sxs-lookup"><span data-stu-id="35492-111">toosetup your web app toorequire client certificates you need tooadd hello clientCertEnabled site setting for your web app and set it tootrue.</span></span> <span data-ttu-id="35492-112">此設定不是目前可透過 hello 入口網站中的 hello 管理體驗和 hello REST API 需要使用 toobe tooaccomplish 此。</span><span class="sxs-lookup"><span data-stu-id="35492-112">This setting is not currently available through hello management experience in hello Portal, and hello REST API will need toobe used tooaccomplish this.</span></span>

<span data-ttu-id="35492-113">您可以使用 hello [ARMClient 工具](https://github.com/projectkudu/ARMClient)toomake 它輕鬆 toocraft hello REST API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="35492-113">You can use hello [ARMClient tool](https://github.com/projectkudu/ARMClient) toomake it easy toocraft hello REST API call.</span></span> <span data-ttu-id="35492-114">您登入 hello 工具之後您將需要 tooissue hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="35492-114">After you log in with hello tool you will need tooissue hello following command:</span></span>

    ARMClient PUT subscriptions/{Subscription Id}/resourcegroups/{Resource Group Name}/providers/Microsoft.Web/sites/{Website Name}?api-version=2015-04-01 @enableclientcert.json -verbose

<span data-ttu-id="35492-115">{} 中的所有項目取代為您的 web 應用程式的資訊，以及建立檔名為 enableclientcert.json 以 hello 下列 JSON 內容：</span><span class="sxs-lookup"><span data-stu-id="35492-115">replacing everything in {} with information for your web app and creating a file called enableclientcert.json with hello following JSON content:</span></span>

    {
        "location": "My Web App Location",
        "properties": {
            "clientCertEnabled": true
        }
    }

<span data-ttu-id="35492-116">請確定您的 web 應用程式是 「 位置 」 toowherever toochange hello 值位於例如美國中北部或美國西部美國等。</span><span class="sxs-lookup"><span data-stu-id="35492-116">Make sure toochange hello value of "location" toowherever your web app is located e.g. North Central US or West US etc.</span></span>

<span data-ttu-id="35492-117">您也可以使用 https://resources.azure.com tooflip hello`clientCertEnabled`屬性太`true`。</span><span class="sxs-lookup"><span data-stu-id="35492-117">You can also use https://resources.azure.com tooflip hello `clientCertEnabled` property too`true`.</span></span>

> <span data-ttu-id="35492-118">**注意：**如果您從 Powershell 執行 ARMClient，您將需要 tooescape hello @ 符號 hello JSON 檔案使用反勾號 '。</span><span class="sxs-lookup"><span data-stu-id="35492-118">**Note:** If you run ARMClient from Powershell, you will need tooescape hello @ symbol for hello JSON file with a back tick \`.</span></span>
> 
> 

## <a name="accessing-hello-client-certificate-from-your-web-app"></a><span data-ttu-id="35492-119">存取 hello 用戶端憑證從 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="35492-119">Accessing hello Client Certificate From Your Web App</span></span>
<span data-ttu-id="35492-120">如果您使用 ASP.NET，並設定您的應用程式 toouse 用戶端憑證驗證，hello 憑證才會在 hello **HttpRequest.ClientCertificate**屬性。</span><span class="sxs-lookup"><span data-stu-id="35492-120">If you are using ASP.NET and configure your app toouse client certificate authentication, hello certificate will be available through hello **HttpRequest.ClientCertificate** property.</span></span> <span data-ttu-id="35492-121">其他應用程式的堆疊，如 hello 用戶端憑證將可透過 base64 編碼值 hello 「 X-ARR ClientCert 的 「 要求標頭中的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="35492-121">For other application stacks, hello client cert will be available in your app through a base64 encoded value in hello "X-ARR-ClientCert" request header.</span></span> <span data-ttu-id="35492-122">您的應用程式可以從這個值建立憑證，然後將它用於您應用程式中的驗證和授權用途。</span><span class="sxs-lookup"><span data-stu-id="35492-122">Your application can create a certificate from this value and then use it for authentication and authorization purposes in your application.</span></span>

## <a name="special-considerations-for-certificate-validation"></a><span data-ttu-id="35492-123">憑證驗證的特殊考量</span><span class="sxs-lookup"><span data-stu-id="35492-123">Special Considerations for Certificate Validation</span></span>
<span data-ttu-id="35492-124">hello 傳送 toohello 應用程式的用戶端憑證不會進出任何驗證 hello Azure Web 應用程式平台。</span><span class="sxs-lookup"><span data-stu-id="35492-124">hello client certificate that is sent toohello application does not go through any validation by hello Azure Web Apps platform.</span></span> <span data-ttu-id="35492-125">驗證這個憑證是 hello 責任 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="35492-125">Validating this certificate is hello responsibility of hello web app.</span></span> <span data-ttu-id="35492-126">以下是基於驗證而驗證憑證內容的範例 ASP.NET 程式碼。</span><span class="sxs-lookup"><span data-stu-id="35492-126">Here is sample ASP.NET code that validates certificate properties for authentication purposes.</span></span>

    using System;
    using System.Collections.Specialized;
    using System.Security.Cryptography.X509Certificates;
    using System.Web;

    namespace ClientCertificateUsageSample
    {
        public partial class cert : System.Web.UI.Page
        {
            public string certHeader = "";
            public string errorString = "";
            private X509Certificate2 certificate = null;
            public string certThumbprint = "";
            public string certSubject = "";
            public string certIssuer = "";
            public string certSignatureAlg = "";
            public string certIssueDate = "";
            public string certExpiryDate = "";
            public bool isValidCert = false;

            //
            // Read hello certificate from hello header into an X509Certificate2 object
            // Display properties of hello certificate on hello page
            //
            protected void Page_Load(object sender, EventArgs e)
            {
                NameValueCollection headers = base.Request.Headers;
                certHeader = headers["X-ARR-ClientCert"];
                if (!String.IsNullOrEmpty(certHeader))
                {
                    try
                    {
                        byte[] clientCertBytes = Convert.FromBase64String(certHeader);
                        certificate = new X509Certificate2(clientCertBytes);
                        certSubject = certificate.Subject;
                        certIssuer = certificate.Issuer;
                        certThumbprint = certificate.Thumbprint;
                        certSignatureAlg = certificate.SignatureAlgorithm.FriendlyName;
                        certIssueDate = certificate.NotBefore.ToShortDateString() + " " + certificate.NotBefore.ToShortTimeString();
                        certExpiryDate = certificate.NotAfter.ToShortDateString() + " " + certificate.NotAfter.ToShortTimeString();
                    }
                    catch (Exception ex)
                    {
                        errorString = ex.ToString();
                    }
                    finally 
                    {
                        isValidCert = IsValidClientCertificate();
                        if (!isValidCert) Response.StatusCode = 403;
                        else Response.StatusCode = 200;
                    }
                }
                else
                {
                    certHeader = "";
                }
            }

            //
            // This is a SAMPLE verification routine. Depending on your application logic and security requirements, 
            // you should modify this method
            //
            private bool IsValidClientCertificate()
            {
                // In this example we will only accept hello certificate as a valid certificate if all hello conditions below are met:
                // 1. hello certificate is not expired and is active for hello current time on server.
                // 2. hello subject name of hello certificate has hello common name nildevecc
                // 3. hello issuer name of hello certificate has hello common name nildevecc and organization name Microsoft Corp
                // 4. hello thumbprint of hello certificate is 30757A2E831977D8BD9C8496E4C99AB26CB9622B
                //
                // This example does NOT test that this certificate is chained tooa Trusted Root Authority (or revoked) on hello server 
                // and it allows for self signed certificates
                //

                if (certificate == null || !String.IsNullOrEmpty(errorString)) return false;

                // 1. Check time validity of certificate
                if (DateTime.Compare(DateTime.Now, certificate.NotBefore) < 0 || DateTime.Compare(DateTime.Now, certificate.NotAfter) > 0) return false;

                // 2. Check subject name of certificate
                bool foundSubject = false;
                string[] certSubjectData = certificate.Subject.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certSubjectData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundSubject = true;
                        break;
                    }
                }
                if (!foundSubject) return false;

                // 3. Check issuer name of certificate
                bool foundIssuerCN = false, foundIssuerO = false;
                string[] certIssuerData = certificate.Issuer.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certIssuerData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundIssuerCN = true;
                        if (foundIssuerO) break;
                    }

                    if (String.Compare(s.Trim(), "O=Microsoft Corp") == 0)
                    {
                        foundIssuerO = true;
                        if (foundIssuerCN) break;
                    }
                }

                if (!foundIssuerCN || !foundIssuerO) return false;

                // 4. Check thumprint of certificate
                if (String.Compare(certificate.Thumbprint.Trim().ToUpper(), "30757A2E831977D8BD9C8496E4C99AB26CB9622B") != 0) return false;

                // If you also want tootest if hello certificate chains tooa Trusted Root Authority you can uncomment hello code below
                //
                //X509Chain certChain = new X509Chain();
                //certChain.Build(certificate);
                //bool isValidCertChain = true;
                //foreach (X509ChainElement chElement in certChain.ChainElements)
                //{
                //    if (!chElement.Certificate.Verify())
                //    {
                //        isValidCertChain = false;
                //        break;
                //    }
                //}
                //if (!isValidCertChain) return false;

                return true;
            }
        }
    }
