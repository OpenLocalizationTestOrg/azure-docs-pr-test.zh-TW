---
title: "aaaAzure AD Java 命令列開始使用 |Microsoft 文件"
description: "如何 toobuild Java 命令列應用程式簽署 tooaccess 應用程式開發介面中的使用者。"
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
ms.openlocfilehash: 9ba1d1e794928a39ca1f091bd0e6eba57ce3d6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-java-command-line-app-tooaccess-an-api-with-azure-ad"></a><span data-ttu-id="32f1b-103">使用 Java 命令列應用程式 tooAccess API 與 Azure AD</span><span class="sxs-lookup"><span data-stu-id="32f1b-103">Using Java Command Line App tooAccess An API with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="32f1b-104">Azure AD 可讓簡單又直接 toooutsource web 應用程式的身分識別管理，提供單一登入和登出只有幾行程式碼。</span><span class="sxs-lookup"><span data-stu-id="32f1b-104">Azure AD makes it simple and straightforward toooutsource your web app's identity management, providing single sign-in and sign-out with only a few lines of code.</span></span>  <span data-ttu-id="32f1b-105">在 Java web 應用程式，您可以完成這項作業使用 Microsoft hello 社群導向 ADAL4J 實作。</span><span class="sxs-lookup"><span data-stu-id="32f1b-105">In Java web apps, you can accomplish this using Microsoft's implementation of hello community-driven ADAL4J.</span></span>

  <span data-ttu-id="32f1b-106">我們將在此處使用 ADAL4J 來執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="32f1b-106">Here we'll use ADAL4J to:</span></span>

* <span data-ttu-id="32f1b-107">登入 hello hello 身分識別提供者以使用 Azure AD 的應用程式 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="32f1b-107">Sign hello user into hello app using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="32f1b-108">顯示 hello 使用者的一些資訊。</span><span class="sxs-lookup"><span data-stu-id="32f1b-108">Display some information about hello user.</span></span>
* <span data-ttu-id="32f1b-109">符號 hello 使用者登出 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="32f1b-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="32f1b-110">在順序 toodo 這樣，您將需要：</span><span class="sxs-lookup"><span data-stu-id="32f1b-110">In order toodo this, you'll need to:</span></span>

1. <span data-ttu-id="32f1b-111">向 Azure AD 註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="32f1b-111">Register an application with Azure AD</span></span>
2. <span data-ttu-id="32f1b-112">設定您的應用程式 toouse hello ADAL4J 程式庫。</span><span class="sxs-lookup"><span data-stu-id="32f1b-112">Set up your app toouse hello ADAL4J library.</span></span>
3. <span data-ttu-id="32f1b-113">使用 hello ADAL4J 文件庫 tooissue 登入和登出要求 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="32f1b-113">Use hello ADAL4J library tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="32f1b-114">列印出 hello 使用者的相關資料。</span><span class="sxs-lookup"><span data-stu-id="32f1b-114">Print out data about hello user.</span></span>

<span data-ttu-id="32f1b-115">啟動，tooget[下載 hello 應用程式的基本架構](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip)或[下載完成的 hello 範例](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="32f1b-115">tooget started, [download hello app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) or [download hello completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>  <span data-ttu-id="32f1b-116">您還需要哪些 tooregister 中的 Azure AD 租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="32f1b-116">You'll also need an Azure AD tenant in which tooregister your application.</span></span>  <span data-ttu-id="32f1b-117">如果沒有，[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="32f1b-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1--register-an-application-with-azure-ad"></a><span data-ttu-id="32f1b-118">1.向 Azure AD 註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="32f1b-118">1.  Register an Application with Azure AD</span></span>
<span data-ttu-id="32f1b-119">tooenable 您 tooauthenticate 應用程式的使用者，您必須先 tooregister 新的應用程式在您的租用戶。</span><span class="sxs-lookup"><span data-stu-id="32f1b-119">tooenable your app tooauthenticate users, you'll first need tooregister a new application in your tenant.</span></span>

1. <span data-ttu-id="32f1b-120">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="32f1b-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="32f1b-121">Hello 頂端列上，按一下您的帳戶，並在 hello**目錄**清單中，選擇您希望 tooregister 您的應用程式的 hello Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="32f1b-121">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="32f1b-122">按一下**更服務**在 hello 左側瀏覽，然後選擇  **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="32f1b-122">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="32f1b-123">按一下 [應用程式註冊]，然後選擇 [新增]。</span><span class="sxs-lookup"><span data-stu-id="32f1b-123">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="32f1b-124">依照 hello 提示，並建立新**Web 應用程式和/或 WebAPI**。</span><span class="sxs-lookup"><span data-stu-id="32f1b-124">Follow hello prompts and create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="32f1b-125">hello**名稱**hello 的應用程式將會描述您應用程式 tooend 使用者</span><span class="sxs-lookup"><span data-stu-id="32f1b-125">hello **name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="32f1b-126">hello**登入 URL**是 hello 基底 URL 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="32f1b-126">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="32f1b-127">hello 基本架構的預設值是`http://localhost:8080/adal4jsample/`。</span><span class="sxs-lookup"><span data-stu-id="32f1b-127">hello skeleton's default is `http://localhost:8080/adal4jsample/`.</span></span>
6. <span data-ttu-id="32f1b-128">完成註冊後，AAD 會為您的應用程式指派唯一的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="32f1b-128">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="32f1b-129">您將需要此值在 hello 下一步 區段中，因此將它複製從 hello 應用程式 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="32f1b-129">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="32f1b-130">從 hello**設定** -> **屬性**應用程式頁面上，更新 hello 應用程式識別碼 URI。</span><span class="sxs-lookup"><span data-stu-id="32f1b-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="32f1b-131">hello**應用程式識別碼 URI**是您的應用程式的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="32f1b-131">hello **App ID URI** is a unique identifier for your application.</span></span>  <span data-ttu-id="32f1b-132">hello 慣例是 toouse `https://<tenant-domain>/<app-name>`，例如`http://localhost:8080/adal4jsample/`。</span><span class="sxs-lookup"><span data-stu-id="32f1b-132">hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `http://localhost:8080/adal4jsample/`.</span></span>

<span data-ttu-id="32f1b-133">一次在 hello 入口網站應用程式建立**金鑰**從 hello**設定**您的應用程式頁面，並將它複製下來。</span><span class="sxs-lookup"><span data-stu-id="32f1b-133">Once in hello portal for your app create a **Key** from hello **Settings** page for your application and copy it down.</span></span>  <span data-ttu-id="32f1b-134">稍後您將會用到此資訊。</span><span class="sxs-lookup"><span data-stu-id="32f1b-134">You will need it shortly.</span></span>

## <a name="2-set-up-your-app-toouse-adal4j-library-and-prerequisites-using-maven"></a><span data-ttu-id="32f1b-135">2.設定您的應用程式 toouse ADAL4J 程式庫和使用 Maven 的必要條件</span><span class="sxs-lookup"><span data-stu-id="32f1b-135">2. Set up your app toouse ADAL4J library and prerequisites using Maven</span></span>
<span data-ttu-id="32f1b-136">在這裡，我們會將設定 ADAL4J toouse hello OpenID Connect 驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="32f1b-136">Here, we'll configure ADAL4J toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="32f1b-137">ADAL4J 將會使用的 tooissue 登入和登出要求、 管理 hello 使用者工作階段，以及取得 hello 使用者，在其他項目之間的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="32f1b-137">ADAL4J will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

* <span data-ttu-id="32f1b-138">Hello 根目錄中您的專案，開啟/建立`pom.xml`並找出 hello`// TODO: provide dependencies for Maven`並取代 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="32f1b-138">In hello root directory of your project, open/create `pom.xml` and locate hello `// TODO: provide dependencies for Maven` and replace with hello following:</span></span>

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



## <a name="3-create-hello-java-publicclient-file"></a><span data-ttu-id="32f1b-139">3.建立 hello Java PublicClient 檔案</span><span class="sxs-lookup"><span data-stu-id="32f1b-139">3. Create hello Java PublicClient file</span></span>
<span data-ttu-id="32f1b-140">如前文所述，我們將使用 hello Graph API tooget hello 登入的使用者資料。</span><span class="sxs-lookup"><span data-stu-id="32f1b-140">As indicated above, we will be using hello Graph API tooget data about hello logged in user.</span></span> <span data-ttu-id="32f1b-141">我們應針對此 toobe 容易讓我們來建立這兩個檔案 toorepresent**目錄物件**和個別檔案 toorepresent hello**使用者**以便 hello OO 模式的 Java 可用。</span><span class="sxs-lookup"><span data-stu-id="32f1b-141">For this toobe easy for us we should create both a file toorepresent a **Directory Object** and an individual file toorepresent hello **User** so that hello OO pattern of Java can be used.</span></span>

* <span data-ttu-id="32f1b-142">建立一個叫做檔案`DirectoryObject.java`我們將會使用 toostore 有關任何 DirectoryObject （您可能感覺受到總公司可用 toouse 這稍後可能會執行任何其他圖形查詢） 的基本資料。</span><span class="sxs-lookup"><span data-stu-id="32f1b-142">Create a file called `DirectoryObject.java` which we will use toostore basic data about any DirectoryObject (you can feel free toouse this later for any other Graph Queries you may do).</span></span> <span data-ttu-id="32f1b-143">您可以從下面剪下/貼上：</span><span class="sxs-lookup"><span data-stu-id="32f1b-143">You can cut/paste this from below:</span></span>

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


## <a name="compile-and-run-hello-sample"></a><span data-ttu-id="32f1b-144">編譯並執行 hello 範例</span><span class="sxs-lookup"><span data-stu-id="32f1b-144">Compile and run hello sample</span></span>
<span data-ttu-id="32f1b-145">寫出 tooyour 根目錄變更，然後執行下列命令 toobuild hello 範例，您只要將放在一起使用的 hello `maven`。</span><span class="sxs-lookup"><span data-stu-id="32f1b-145">Change back out tooyour root directory and run hello following command toobuild hello sample you just put together using `maven`.</span></span> <span data-ttu-id="32f1b-146">此選項會使用 hello`pom.xml`您所撰寫的相依性的檔案。</span><span class="sxs-lookup"><span data-stu-id="32f1b-146">This will use hello `pom.xml` file you wrote for dependencies.</span></span>

`$ mvn package`

<span data-ttu-id="32f1b-147">您的 `/targets` 目錄中現在應包含 `adal4jsample.war` 檔案。</span><span class="sxs-lookup"><span data-stu-id="32f1b-147">You should now have a `adal4jsample.war` file in your `/targets` directory.</span></span> <span data-ttu-id="32f1b-148">您可能會部署在 Tomcat 容器中，瀏覽 hello URL</span><span class="sxs-lookup"><span data-stu-id="32f1b-148">You may deploy that in your Tomcat container and visit hello URL</span></span> 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> <span data-ttu-id="32f1b-149">它是很容易 toodeploy WAR 與 hello 最新的 Tomcat 伺服器。</span><span class="sxs-lookup"><span data-stu-id="32f1b-149">It is very easy toodeploy a WAR with hello latest Tomcat servers.</span></span> <span data-ttu-id="32f1b-150">直接瀏覽過`http://localhost:8080/manager/`並上傳遵循 hello 指示您 ' adal4jsample.war' 檔案。</span><span class="sxs-lookup"><span data-stu-id="32f1b-150">Simply navigate too`http://localhost:8080/manager/` and follow hello instructions on uploading your ``adal4jsample.war\` file.</span></span> <span data-ttu-id="32f1b-151">它會為您的 autodeploy 與 hello 正確端點。</span><span class="sxs-lookup"><span data-stu-id="32f1b-151">It will autodeploy for you with hello correct endpoint.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="32f1b-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="32f1b-152">Next Steps</span></span>
<span data-ttu-id="32f1b-153">恭喜！</span><span class="sxs-lookup"><span data-stu-id="32f1b-153">Congratulations!</span></span> <span data-ttu-id="32f1b-154">您現在擁有可運作的 Java 應用程式具有 hello 能力 tooauthenticate 使用者、 安全地呼叫 Web Api 使用 OAuth 2.0，並取得 hello 使用者的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="32f1b-154">You now have a working Java application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="32f1b-155">如果您還沒有這麼做，現在是 hello 時間 toopopulate 與某些使用者的租用戶。</span><span class="sxs-lookup"><span data-stu-id="32f1b-155">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>

<span data-ttu-id="32f1b-156">如需參考，hello 完成 （不含您的組態值） 的範例[依現狀的.zip](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip)，或您可以將其複製從 GitHub:</span><span class="sxs-lookup"><span data-stu-id="32f1b-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

