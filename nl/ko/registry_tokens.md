---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-20"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# {{site.data.keyword.registrylong_notm}}에 대한 액세스 자동화
{: #registry_access}

이미지를 푸시하고 가져올 수 있도록 레지스트리 토큰 또는 {{site.data.keyword.iamlong}}(IAM) API를 사용하여 {{site.data.keyword.registrylong_notm}} 네임스페이스에 대한 액세스를 자동화할 수 있습니다.
{:shortdesc}

Kubernetes 배치에서 레지스트리 이미지를 사용하시겠습니까? [기타 Kubernetes 네임스페이스, {{site.data.keyword.Bluemix_notm}} 지역 및 계정의 이미지에 액세스](/docs/containers/cs_images.html#other)를 체크아웃하십시오.
{: tip}

API 키가 계정에 연결되고 {{site.data.keyword.Bluemix_notm}}에서 사용할 수 있으므로 각 서비스에 대해 다른 신임 정보가 필요하지 않습니다. CLI에서 API 키를 사용하거나 사용자 ID로 로그인하기 위한 자동화의 일부로 API 키를 사용할 수 있습니다.

레지스트리 토큰의 범위는 {{site.data.keyword.registrylong_notm}}용으로만 지정됩니다. 레지스트리 토큰을 읽기 전용 액세스로 제한할 수 있으며 만료되는지 또는 만료되지 않는지 선택할 수 있습니다.

{{site.data.keyword.registrylong_notm}} API 키에 대한 자세한 정보는 [API 키로 작업](/docs/iam/apikeys.html#manapikey)을 참조하십시오.

시작하기 전에 [{{site.data.keyword.registrylong_notm}} 및 Docker CLI를 설치](registry_setup_cli_namespace.html#registry_cli_install)하십시오.


## API 키를 사용하여 네임스페이스에 대한 액세스 자동화
{: #registry_api_key}

API 키를 사용하여 네임스페이스에 대한 Docker 이미지의 푸시 및 가져오기를 자동화할 수 있습니다.
{:shortdesc}

### API 키 작성
{: #registry_api_key_create}

API 키를 작성한 후 레지스트리에 로그인하는 데 사용할 수 있습니다.
{:shortdesc}

IAM API 키를 작성하려면 [API 키 작성](/docs/iam/userid_keys.html#creating-an-api-key)을 참조하십시오.

### API 키를 사용하여 액세스 자동화
{: #registry_api_key_use}

API 키를 사용하여 {{site.data.keyword.registrylong_notm}}의 네임스페이스에 액세스할 수 있습니다.
{:shortdesc}

다음 Docker 명령을 실행하여 API 키로 레지스트리에 로그인하십시오. &lt;your_apikey&gt;를 API 키로 대체하고 &lt;registry_url&gt;을 네임스페이스가 설정된 레지스트리의 URL로 대체하십시오.

```
docker login -u iamapikey -p <your_apikey> <registry_url>
```
{: pre}

명령에 대한 참조 정보는 [새 {{site.data.keyword.Bluemix_notm}} 플랫폼 API 키 작성](/docs/cli/reference/ibmcloud/cli_api_policy.html#ibmcloud_iam_api_key_create)을 참조하십시오.


## 토큰을 사용하여 네임스페이스에 대한 액세스 자동화
{: #registry_tokens}

토큰을 사용하여 {{site.data.keyword.registrylong_notm}} 네임스페이스에 대한 Docker 이미지의 푸시 및 가져오기를 자동화할 수 있습니다.
{:shortdesc}

레지스트리 토큰을 보유한 모든 사용자는 보안 정보에 액세스할 수 있습니다. {{site.data.keyword.Bluemix_notm}} 계정에 대한 토큰을 작성하여 지역에서 설정한 모든 네임스페이스에 대한 액세스 권한을 {{site.data.keyword.Bluemix_notm}} 계정 외부의 사용자에게 부여할 수 있습니다. 이 토큰을 소유하고 있는 모든 사용자 또는 앱은 container-registry 플러그인을 설치하지 않고 이미지를 네임스페이스에 푸시하고 네임스페이스에서 이미지를 가져올 수 있습니다.

{{site.data.keyword.Bluemix_notm}} 계정에 대한 토큰을 작성할 때 해당 토큰이 레지스트리에 대한 읽기 전용(가져오기) 권한을 부여하는지 또는 쓰기(푸시 및 가져오기) 권한을 부여하는지 결정할 수 있습니다. 토큰이 영구적인지 또는 24시간 후에 만료되는지 여부를 지정할 수도 있습니다. 여러 토큰을 작성하고 사용하여 다양한 유형의 액세스를 제어할 수 있습니다.

토큰을 관리하려면 다음 태스크를 사용하십시오.

-  [{{site.data.keyword.Bluemix_notm}} 계정에 대한 토큰 작성](#registry_tokens_create)
-  [토큰을 사용하여 네임스페이스에 대한 액세스 자동화](#registry_tokens_use)
-  [{{site.data.keyword.Bluemix_notm}} 계정에서 토큰 제거](#registry_tokens_remove)


### {{site.data.keyword.Bluemix_notm}} 계정의 토큰 작성
{: #registry_tokens_create}

지역의 모든 {{site.data.keyword.registrylong_notm}} 네임스페이스에 액세스 권한을 부여하기 위한 토큰을 작성할 수 있습니다.
{:shortdesc}

1.  토큰을 작성하십시오. 다음 예는 지역에 설정된 모든 네임스페이스에 읽기 및 쓰기 액세스 권한이 있는 만료되지 않는 토큰을 작성합니다.

    ```
    ibmcloud cr token-add --description "This is a token" --non-expiring --readwrite
    ```
    {: pre}

    <table>
        <thead>
        <th colspan=2><img src="images/idea.png" alt="전구 아이콘"/> 이 명령의 컴포넌트 이해</th>
        </thead>
        <tbody>
        <tr>
        <td>`--description`</td>
        <td>선택사항. 이 옵션을 사용하여 토큰을 이후에 더 쉽게 식별할 수 있도록 설명합니다.</td>
        </tr>
        <tr>
        <td>`--non-expiring`</td>
        <td>선택사항. 이 옵션을 사용하여 만료되지 않는 토큰을 작성합니다. 이 옵션을 지정하지 않으면 토큰이 24시간 후에 유효하지 않게 됩니다. <br> **팁:** 네임스페이스에 대한 액세스를 차단하는 데 만료되지 않는 토큰이 더 이상 필요하지 않은 경우에는 반드시 토큰을 제거하십시오.</td>
        </tr>
        <tr>
        <td>`--readwrite`</td>
        <td>선택사항. 이 옵션을 사용하여 사용자가 이미지를 네임스페이스에 푸시하거나 이미지를 네임스페이스에서 가져오도록 허용하는 토큰을 작성합니다. 이 옵션을 지정하지 않는 경우, 이미지를 가져오기 위해서만 토큰을 사용할 수 있습니다.</td>
        </tr>
        </tbody>
        </table>

    CLI 출력은 다음 출력과 유사합니다.

    ```
Token identifier   58669dd6-3ddd-5c78-99f9-ad0a5aabd9ad   
Token              <token_value>
    ```
    {: screen}

2.  토큰이 작성되었는지 확인하십시오.

    ```
    ibmcloud cr token-list
    ```
    {: pre}


### 토큰을 사용하여 네임스페이스에 대한 액세스 자동화
{: #registry_tokens_use}

`docker login` 명령에서 토큰을 사용하여 {{site.data.keyword.registrylong_notm}}의 네임스페이스에 대한 액세스를 자동화할 수 있습니다. 토큰에 대한 읽기 전용 또는 읽기/쓰기 액세스 권한 설정 여부에 따라, 사용자는 이미지를 네임스페이스에서 가져오고 이미지를 네임스페이스로 푸시할 수 있습니다.
{:shortdesc}

1.  {{site.data.keyword.Bluemix_notm}}에 로그인하십시오.

    ```
    ibmcloud login
    ```
    {: pre}

2.  {{site.data.keyword.Bluemix_notm}} 계정의 모든 토큰을 나열하고 사용하려는 토큰 ID를 기록해 놓으십시오.

    ```
    ibmcloud cr token-list
    ```
    {: pre}

3.  토큰에 대한 토큰 값을 검색하십시오. &lt;token_id&gt;를 토큰의 ID로 대체하십시오.

    ```
    ibmcloud cr token-get <token_id>
    ```
    {: pre}

    사용자의 토큰 값이 CLI 출력의 **토큰**에 표시됩니다.

4.  `docker login` 명령의 일부로 토큰을 사용하십시오. &lt;token_value&gt;는 이전 단계에서 검색한 토큰 값으로 대체하고 &lt;registry_url&gt;은 네임스페이스가 설정된 레지스트리에 대한 URL로 대체하십시오.

    -   미국 남부의 네임스페이스 설정의 경우: `registry.ng.bluemix.net`
    -   영국 남부의 네임스페이스 설정의 경우: `registry.eu-gb.bluemix.net`
    -   유럽 연합 중부의 네임스페이스 설정의 경우: `registry.eu-de.bluemix.net`
    -   아시아/태평양 남부의 네임스페이스 설정의 경우: `registry.au-syd.bluemix.net`

    ```
    docker login -u token -p <token_value> <registry_url>
    ```
    {: pre}
    
    `-u` 매개변수의 경우에는 토큰 ID가 아니라 문자열 `token`을 입력했는지 확인하십시오.
    {: tip}

    토큰을 사용하여 Docker에 로그인한 후에 이미지를 네임스페이스로 푸시하거나 이미지를 네임스페이스에서 가져올 수 있습니다.


### {{site.data.keyword.Bluemix_notm}} 계정에서 토큰 제거
{: #registry_tokens_remove}

토큰이 더 이상 필요하지 않은 경우 {{site.data.keyword.registrylong_notm}}를 제거합니다.
{:shortdesc}

만료된 {{site.data.keyword.registrylong_notm}} 토큰은 {{site.data.keyword.Bluemix_notm}} 계정에서 자동으로 제거되며 수동으로 제거할 필요가 없습니다.
{:tip}

1.  {{site.data.keyword.Bluemix_notm}}에 로그인하십시오.

    ```
    ibmcloud login
    ```
    {: pre}

2.  {{site.data.keyword.Bluemix_notm}} 계정의 모든 토큰을 나열하고 제거하려는 토큰 ID를 기록해 놓으십시오.

    ```
    ibmcloud cr token-list
    ```
    {: pre}

3.  토큰을 제거하십시오.

    ```
    ibmcloud cr token-rm <token_id>
    ```
    {: pre}
