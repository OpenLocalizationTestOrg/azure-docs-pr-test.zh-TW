---
title: "Azure AD Java 命令列入門 | Microsoft Docs"
description: "如何建立一個將使用者登入以存取 API 的Java 命令列應用程式。"
services: active-directory
documentationcenter: java
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 51e1a8f9-6ff0-4643-a350-0ba794e26fd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 91e4a7b2ac454465d5cce4948a4d5f0b542d2b55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-java-command-line-app-to-access-an-api-with-azure-ad"></a><span data-ttu-id="493fa-103">使用 Java 命令列應用程式存取具有 Azure AD 的 API</span><span class="sxs-lookup"><span data-stu-id="493fa-103">Using Java Command Line App To Access An API with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="493fa-104">Azure AD 讓您外包 Web 應用程式的身分識別管理變得既簡單又直接，只需幾行的程式碼便可提供單一登入和登出。</span><span class="sxs-lookup"><span data-stu-id="493fa-104">Azure AD makes it simple and straightforward to outsource your web app's identity management, providing single sign-in and sign-out with only a few lines of code.</span></span>  <span data-ttu-id="493fa-105">在 Java Web 應用程式中，您可以使用 Microsoft 的 ADAL4J 社群導向實作來完成這項作業。</span><span class="sxs-lookup"><span data-stu-id="493fa-105">In Java web apps, you can accomplish this using Microsoft's implementation of the community-driven ADAL4J.</span></span>

  <span data-ttu-id="493fa-106">我們將在此處使用 ADAL4J 來執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="493fa-106">Here we'll use ADAL4J to:</span></span>

* <span data-ttu-id="493fa-107">使用 Azure AD 做為身分識別提供者，將使用者登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="493fa-107">Sign the user into the app using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="493fa-108">顯示使用者的一些相關資訊。</span><span class="sxs-lookup"><span data-stu-id="493fa-108">Display some information about the user.</span></span>
* <span data-ttu-id="493fa-109">讓使用者登出 App。</span><span class="sxs-lookup"><span data-stu-id="493fa-109">Sign the user out of the app.</span></span>

<span data-ttu-id="493fa-110">為執行此作業，您必須執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="493fa-110">In order to do this, you'll need to:</span></span>

1. <span data-ttu-id="493fa-111">向 Azure AD 註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="493fa-111">Register an application with Azure AD</span></span>
2. <span data-ttu-id="493fa-112">設定您的應用程式以使用 ADAL4J 程式庫。</span><span class="sxs-lookup"><span data-stu-id="493fa-112">Set up your app to use the ADAL4J library.</span></span>
3. <span data-ttu-id="493fa-113">使用 ADAL4J 程式庫向 Azure AD 發出登入和登出要求。</span><span class="sxs-lookup"><span data-stu-id="493fa-113">Use the ADAL4J library to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="493fa-114">列印出使用者的相關資料。</span><span class="sxs-lookup"><span data-stu-id="493fa-114">Print out data about the user.</span></span>

<span data-ttu-id="493fa-115">若要開始使用，請[下載應用程式基本架構](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip)或[下載完整的範例](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="493fa-115">To get started, [download the app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) or [download the completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>  <span data-ttu-id="493fa-116">您還需要一個可以註冊應用程式的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="493fa-116">You'll also need an Azure AD tenant in which to register your application.</span></span>  <span data-ttu-id="493fa-117">如果您還沒有租用戶， [了解如何取得租用戶](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="493fa-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1--register-an-application-with-azure-ad"></a><span data-ttu-id="493fa-118">1.向 Azure AD 註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="493fa-118">1.  Register an Application with Azure AD</span></span>
<span data-ttu-id="493fa-119">若要啟用應用程式來驗證使用者，您必須先要在您的租用戶中註冊這個新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="493fa-119">To enable your app to authenticate users, you'll first need to register a new application in your tenant.</span></span>

1. <span data-ttu-id="493fa-120">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="493fa-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="493fa-121">在頂端列上按一下您的帳戶，然後在 [目錄] 清單底下，選擇您要註冊應用程式的 Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="493fa-121">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="493fa-122">按一下左側瀏覽區中的 [更多服務]，然後選擇 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="493fa-122">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="493fa-123">按一下 [應用程式註冊]，然後選擇 [新增]。</span><span class="sxs-lookup"><span data-stu-id="493fa-123">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="493fa-124">遵照提示進行，並建立新的 **Web 應用程式和/或 WebAPI**。</span><span class="sxs-lookup"><span data-stu-id="493fa-124">Follow the prompts and create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="493fa-125">應用程式的 [ **名稱** ] 將對使用者說明您的應用程式</span><span class="sxs-lookup"><span data-stu-id="493fa-125">The **name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="493fa-126">[ **登入 URL** ] 是指應用程式的基底 URL。</span><span class="sxs-lookup"><span data-stu-id="493fa-126">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="493fa-127">基本架構的預設值是 `http://localhost:8080/adal4jsample/`。</span><span class="sxs-lookup"><span data-stu-id="493fa-127">The skeleton's default is `http://localhost:8080/adal4jsample/`.</span></span>
6. <span data-ttu-id="493fa-128">完成註冊後，AAD 會為您的應用程式指派唯一的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="493fa-128">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="493fa-129">您會在後續小節中用到這個值，所以請從應用程式索引標籤中複製此值。</span><span class="sxs-lookup"><span data-stu-id="493fa-129">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="493fa-130">從應用程式的 [設定]  ->  [屬性] 頁面，更新應用程式識別碼 URI。</span><span class="sxs-lookup"><span data-stu-id="493fa-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="493fa-131">[ **應用程式識別碼 URI** ] 是指應用程式的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="493fa-131">The **App ID URI** is a unique identifier for your application.</span></span>  <span data-ttu-id="493fa-132">慣例會使用 `https://<tenant-domain>/<app-name>`，例如：`http://localhost:8080/adal4jsample/`。</span><span class="sxs-lookup"><span data-stu-id="493fa-132">The convention is to use `https://<tenant-domain>/<app-name>`, e.g. `http://localhost:8080/adal4jsample/`.</span></span>

<span data-ttu-id="493fa-133">進入應用程式的入口網站後，從應用程式的 [設定] 頁面建立 [金鑰]，然後複製下來。</span><span class="sxs-lookup"><span data-stu-id="493fa-133">Once in the portal for your app create a **Key** from the **Settings** page for your application and copy it down.</span></span>  <span data-ttu-id="493fa-134">稍後您將會用到此資訊。</span><span class="sxs-lookup"><span data-stu-id="493fa-134">You will need it shortly.</span></span>

## <a name="2-set-up-your-app-to-use-adal4j-library-and-prerequisites-using-maven"></a><span data-ttu-id="493fa-135">2.使用 Maven 設定您的應用程式以使用 ADAL4J 程式庫和必要條件</span><span class="sxs-lookup"><span data-stu-id="493fa-135">2. Set up your app to use ADAL4J library and prerequisites using Maven</span></span>
<span data-ttu-id="493fa-136">在這裡，我們將設定 ADAL4J 以使用 OpenID Connect 驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="493fa-136">Here, we'll configure ADAL4J to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="493fa-137">ADAL4J 將用來發出登入和登出要求、管理使用者的工作階段，以及取得使用者相關資訊等其他作業。</span><span class="sxs-lookup"><span data-stu-id="493fa-137">ADAL4J will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

* <span data-ttu-id="493fa-138">在您的專案根目錄中，開啟/建立 `pom.xml` 並找到 `// TODO: provide dependencies for Maven`，然後以下列取代：</span><span class="sxs-lookup"><span data-stu-id="493fa-138">In the root directory of your project, open/create `pom.xml` and locate the `// TODO: provide dependencies for Maven` and replace with the following:</span></span>

```Java
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>public-client-adal4j-sample</artifactId>
    <packaging>jar</packaging>
    <version>0.0.1-SNAPSHOT</version>
    <name>public-client-adal4j-sample</name>
    <url>http://maven.apache.org</url>
    <properties>
        <spring.version>3.0.5.RELEASE</spring.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>adal4j</artifactId>
            <version>1.1.2</version>
        </dependency>
        <dependency>
            <groupId>com.nimbusds</groupId>
            <artifactId>oauth2-oidc-sdk</artifactId>
            <version>4.5</version>
        </dependency>
        <dependency>
            <groupId>org.json</groupId>
            <artifactId>json</artifactId>
            <version>20090211</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.0.1</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.7.5</version>
        </dependency>
</dependencies>
    <build>
        <finalName>public-client-adal4j-sample</finalName>
        <plugins>
                <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <version>1.2.1</version>
            <configuration>
                <mainClass>PublicClient</mainClass>
            </configuration>
        </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <executions>
                    <execution>
                        <id>install</id>
                        <phase>install</phase>
                        <goals>
                            <goal>sources</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</artifactId>
                <version>2.5</version>
                <configuration>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
        <artifactId>maven-assembly-plugin</artifactId>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>single</goal>
            </goals>
          </execution>
        </executions>
        <configuration>
          <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
          </descriptorRefs>
        </configuration>
      </plugin>
      <plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-assembly-plugin</artifactId>
  <configuration>
    <archive>
      <manifest>
        <mainClass>PublicClient</mainClass>
      </manifest>
    </archive>
  </configuration>
</plugin>
        </plugins>
    </build>

</project>


```



## <a name="3-create-the-java-publicclient-file"></a><span data-ttu-id="493fa-139">3.建立 Java PublicClient 檔案</span><span class="sxs-lookup"><span data-stu-id="493fa-139">3. Create the Java PublicClient file</span></span>
<span data-ttu-id="493fa-140">如以上所述，我們將使用圖形 API 來取得有關所登入使用者的資料。</span><span class="sxs-lookup"><span data-stu-id="493fa-140">As indicated above, we will be using the Graph API to get data about the logged in user.</span></span> <span data-ttu-id="493fa-141">為了讓我們順利進行，我們應該建立一個代表**目錄物件**的檔案以及一個代表**使用者**的個別檔案，如此便可以使用 Java 的 OO 模式。</span><span class="sxs-lookup"><span data-stu-id="493fa-141">For this to be easy for us we should create both a file to represent a **Directory Object** and an individual file to represent the **User** so that the OO pattern of Java can be used.</span></span>

* <span data-ttu-id="493fa-142">建立名為 `DirectoryObject.java` 的檔案，我們將用它來儲存有關任何 DirectoryObject 的基本資料 (您稍後可以隨意使用它執行任何其他圖形查詢)。</span><span class="sxs-lookup"><span data-stu-id="493fa-142">Create a file called `DirectoryObject.java` which we will use to store basic data about any DirectoryObject (you can feel free to use this later for any other Graph Queries you may do).</span></span> <span data-ttu-id="493fa-143">您可以從下面剪下/貼上：</span><span class="sxs-lookup"><span data-stu-id="493fa-143">You can cut/paste this from below:</span></span>

```Java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

import javax.naming.ServiceUnavailableException;

import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;

public class PublicClient {

    private final static String AUTHORITY = "https://login.microsoftonline.com/common/";
    private final static String CLIENT_ID = "2a4da06c-ff07-410d-af8a-542a512f5092";

    public static void main(String args[]) throws Exception {

        try (BufferedReader br = new BufferedReader(new InputStreamReader(
                System.in))) {
            System.out.print("Enter username: ");
            String username = br.readLine();
            System.out.print("Enter password: ");
            String password = br.readLine();

            AuthenticationResult result = getAccessTokenFromUserCredentials(
                    username, password);
            System.out.println("Access Token - " + result.getAccessToken());
            System.out.println("Refresh Token - " + result.getRefreshToken());
            System.out.println("ID Token - " + result.getIdToken());
        }
    }

    private static AuthenticationResult getAccessTokenFromUserCredentials(
            String username, String password) throws Exception {
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(AUTHORITY, false, service);
            Future<AuthenticationResult> future = context.acquireToken(
                    "https://graph.windows.net", CLIENT_ID, username, password,
                    null);
            result = future.get();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;
    }
}


```


## <a name="compile-and-run-the-sample"></a><span data-ttu-id="493fa-144">編譯並執行範例</span><span class="sxs-lookup"><span data-stu-id="493fa-144">Compile and run the sample</span></span>
<span data-ttu-id="493fa-145">變更回根目錄，並執行下列命令來建置您剛剛使用 `maven`組成的範例。</span><span class="sxs-lookup"><span data-stu-id="493fa-145">Change back out to your root directory and run the following command to build the sample you just put together using `maven`.</span></span> <span data-ttu-id="493fa-146">這將會使用您針對相依性所撰寫的 `pom.xml` 檔案。</span><span class="sxs-lookup"><span data-stu-id="493fa-146">This will use the `pom.xml` file you wrote for dependencies.</span></span>

`$ mvn package`

<span data-ttu-id="493fa-147">您的 `/targets` 目錄中現在應包含 `adal4jsample.war` 檔案。</span><span class="sxs-lookup"><span data-stu-id="493fa-147">You should now have a `adal4jsample.war` file in your `/targets` directory.</span></span> <span data-ttu-id="493fa-148">您可以在 Tomcat 容器中部署該檔案並造訪 URL</span><span class="sxs-lookup"><span data-stu-id="493fa-148">You may deploy that in your Tomcat container and visit the URL</span></span> 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> <span data-ttu-id="493fa-149">使用最新的 Tomcat 伺服器部署 WAR 非常容易。</span><span class="sxs-lookup"><span data-stu-id="493fa-149">It is very easy to deploy a WAR with the latest Tomcat servers.</span></span> <span data-ttu-id="493fa-150">只要瀏覽至 `http://localhost:8080/manager/` 並遵循上傳您的 adal4jsample.war 檔案的指示即可。</span><span class="sxs-lookup"><span data-stu-id="493fa-150">Simply navigate to `http://localhost:8080/manager/` and follow the instructions on uploading your ``adal4jsample.war\` file.</span></span> <span data-ttu-id="493fa-151">它會為您自動部署正確的端點。</span><span class="sxs-lookup"><span data-stu-id="493fa-151">It will autodeploy for you with the correct endpoint.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="493fa-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="493fa-152">Next Steps</span></span>
<span data-ttu-id="493fa-153">恭喜！</span><span class="sxs-lookup"><span data-stu-id="493fa-153">Congratulations!</span></span> <span data-ttu-id="493fa-154">您現在有一個可運作的 Java 應用程式，能夠驗證使用者、使用 OAuth 2.0 安全地呼叫 Web API，以及取得使用者的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="493fa-154">You now have a working Java application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="493fa-155">如果您還沒有這麼做，現在是將一些使用者植入租用戶的時候。</span><span class="sxs-lookup"><span data-stu-id="493fa-155">If you haven't already, now is the time to populate your tenant with some users.</span></span>

<span data-ttu-id="493fa-156">如需參考， [此處以 .zip 格式提供](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip)完整範例 (不含您的組態值)，您也可以從 GitHub 將其複製：</span><span class="sxs-lookup"><span data-stu-id="493fa-156">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

