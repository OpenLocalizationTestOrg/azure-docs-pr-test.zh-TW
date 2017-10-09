<span data-ttu-id="0e053-101">如果您擁有授與存取儲存體帳戶中的 tooresources 共用的存取簽章 (SAS) URL，您可以使用連接字串中的 hello SAS。</span><span class="sxs-lookup"><span data-stu-id="0e053-101">If you possess a shared access signature (SAS) URL that grants you access tooresources in a storage account, you can use hello SAS in a connection string.</span></span> <span data-ttu-id="0e053-102">Hello SAS 包含 hello 資訊需要的 tooauthenticate hello 要求，因為與 SAS 連接字串提供 hello 通訊協定、 hello 服務端點和 hello 所需的認證 tooaccess hello 資源。</span><span class="sxs-lookup"><span data-stu-id="0e053-102">Because hello SAS contains hello information required tooauthenticate hello request, a connection string with a SAS provides hello protocol, hello service endpoint, and hello necessary credentials tooaccess hello resource.</span></span>

<span data-ttu-id="0e053-103">toocreate 連接字串，包含共用的存取簽章指定下列格式的 hello hello 字串：</span><span class="sxs-lookup"><span data-stu-id="0e053-103">toocreate a connection string that includes a shared access signature, specify hello string in hello following format:</span></span>

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

<span data-ttu-id="0e053-104">雖然 hello 連接字串必須至少包含一個選擇性的每個服務端點。</span><span class="sxs-lookup"><span data-stu-id="0e053-104">Each service endpoint is optional, although hello connection string must contain at least one.</span></span>

> [!NOTE]
> <span data-ttu-id="0e053-105">建議最好搭配使用 HTTPS 與 SAS。</span><span class="sxs-lookup"><span data-stu-id="0e053-105">Using HTTPS with a SAS is recommended as a best practice.</span></span>
>
> <span data-ttu-id="0e053-106">如果您指定的 SAS 連接字串中的組態檔中，您可能需要 tooencode hello URL 中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="0e053-106">If you are specifying a SAS in a connection string in a configuration file, you may need tooencode special characters in hello URL.</span></span>
>
>

### <a name="service-sas-example"></a><span data-ttu-id="0e053-107">服務 SAS 範例</span><span class="sxs-lookup"><span data-stu-id="0e053-107">Service SAS example</span></span>
<span data-ttu-id="0e053-108">以下範例是包含服務 SAS for Blob 儲存體的連接字串：</span><span class="sxs-lookup"><span data-stu-id="0e053-108">Here's an example of a connection string that includes a service SAS for Blob storage:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

<span data-ttu-id="0e053-109">以下是範例的 hello 和相同的連接字串與特殊字元編碼方式：</span><span class="sxs-lookup"><span data-stu-id="0e053-109">And here's an example of hello same connection string with encoding of special characters:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a><span data-ttu-id="0e053-110">帳戶 SAS 範例</span><span class="sxs-lookup"><span data-stu-id="0e053-110">Account SAS example</span></span>
<span data-ttu-id="0e053-111">以下範例是包含帳戶 SAS for Blob 和檔案儲存體的連接字串。</span><span class="sxs-lookup"><span data-stu-id="0e053-111">Here's an example of a connection string that includes an account SAS for Blob and File storage.</span></span> <span data-ttu-id="0e053-112">請注意，指定兩個服務的端點︰</span><span class="sxs-lookup"><span data-stu-id="0e053-112">Note that endpoints for both services are specified:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

<span data-ttu-id="0e053-113">以下是範例的 hello 和相同的連接字串，以 URL 編碼方式：</span><span class="sxs-lookup"><span data-stu-id="0e053-113">And here's an example of hello same connection string with URL encoding:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

