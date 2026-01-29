# Update NFT Information

## NFT API&#x20;

### update NFT metadata

&#x20;<mark style="background-color:orange;">**put**</mark>   https://api.dappportal.io/api/b2b-v1/nfts/{chain}/{contract\_address}/{token\_id}/metadata\
\
<mark style="color:red;">**To ensure the security of your secret key, this API should be called from a secure server environment rather than directly than from webpage(FrontEnd).**</mark>

#### Parameters

| Name                                                                                                               | Description                                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <p><strong>chain</strong> <mark style="color:red;">*required</mark><br>string <br><em>(path)</em></p>              | chain name : "kairos", "kaia"                                                                                                                                |
| <p><strong>contract_address</strong> <mark style="color:red;">*required</mark><br>string <br><em>(path)</em></p>   | contract address of NFT                                                                                                                                      |
| <p><strong>token_id</strong> <mark style="color:red;">*required</mark><br>string <br><em>(path)</em></p>           | token id of NFT                                                                                                                                              |
| <p><strong>X-Auth-Signature</strong> <mark style="color:red;">*required</mark><br>string <br><em>(header)</em></p> | <p>HMAC (clientId + method + path + timestamp + salt) key={secret}<br><br>You can find the code example below.</p>                                           |
| <p><strong>X-Auth-ClientId</strong> <mark style="color:red;">*required</mark><br>string <br><em>(header)</em></p>  | client id obtained from support team                                                                                                                         |
| <p><strong>X-Auth-Timestamp</strong> <mark style="color:red;">*required</mark><br>string <br><em>(header)</em></p> | <p>Timestamp used in the X-Auth-Signature (request time)<br><br>This parameter is included to protect against replay attacks.</p>                            |
| <p><strong>X-Auth-Salt</strong> <mark style="color:red;">*required</mark><br>string <br><em>(header)</em></p>      | <p>Salt used in the X-Auth-Signature (a unique random value provided by the client for each request)<br><em>(Length: 36 characters, UUID v4 format)</em></p> |

\
**HMAC Signature Generation Example (Node.js)**

Example code to generate `X-Auth-Signature` header for secure API calls.

```javascript
const crypto = require('crypto');
/**
 * Generates an HMAC signature for API authentication.
 * @param {string} secret - Shared secret key used for HMAC.
 * @param {string} clientId - Public client identifier.
 * @param {string} method - HTTP method (e.g., GET, POST).
 * @param {string} path - Request path (e.g., /api/v1/resource).
 * @param {string} timestamp - UNIX timestamp (in seconds).
 * @param {string} salt - Random value (e.g., UUID or random bytes).
 * @returns {string} - Base64-encoded HMAC signature.
 */
function generateHmacSignature(secret, clientId, method, path, timestamp, salt) {
  const message = `${clientId}|${method.toUpperCase()}|${path}|${timestamp}|${salt}`;
  const hmac = crypto.createHmac('sha256', secret);
  hmac.update(message);
  return hmac.digest('base64');
}
 
const secret = 'your-secret-key';
const clientId = 'client-abc-123';
const method = 'POST';
const path = '/api/v1/order';
const timestamp = Math.floor(Date.now() / 1000).toString();
const salt = crypto.randomUUID(); 
const signature = generateHmacSignature(secret, clientId, method, path, timestamp, salt);
 
// debug code
console.log('X-Client-Id:', clientId);
console.log('X-Timestamp:', timestamp);
console.log('X-Salt:', salt);
console.log('X-Auth-Signature:', signature);
```



#### Request Body

<table><thead><tr><th>Example Value</th><th>Schema</th></tr></thead><tbody><tr><td><pre class="language-json"><code class="lang-json">{
  "name": "title1",
  "image": "https://data.dappportal.io/nft/N6788dcf821089d16387aac02/e9856c3c-7a74-4545-b75b-2df5b49fd41f/image/1.png",
  "cached_image": "https://obs.line-scdn.net:443/0h5TZGDWSkantnPnuVeJwVLD1rZAoLT3NuHgh4Axp7YBdUXHYsHiRMeh9sQg4BXltRECdTXBxsViABb0tsHSd9dkNfUkoWW0gsEjN6fhxtfxZKZUskEApubQRFaBFCcl0",
  "description": "description1",
  "attributes": [
    {
      "trait_type": "Color",
      "value": "Green"
    },
    {
      "trait_type": "Level",
      "value": "5 level"
    },
    {
      "trait_type": "Birthday",
      "value": "2024.12.5"
    }
  ]
}
</code></pre></td><td><pre class="language-javascript"><code class="lang-javascript">{
  name: string,
  description: string,
  image: string,
  attributes: [Atribute {
              trait_type: string,
              value: string
              }]
}
</code></pre></td></tr></tbody></table>

#### Responses

<table><thead><tr><th>HTTP Status Code </th><th>description</th></tr></thead><tbody><tr><td>200</td><td>null</td></tr><tr><td>400</td><td><pre class="language-json"><code class="lang-json">{
    "code": "UNAUTHENTICATED"
}
</code></pre></td></tr><tr><td>400</td><td><pre class="language-json"><code class="lang-json">{
    "code": "INVALID_PARAMS"
}
</code></pre></td></tr><tr><td>400</td><td><pre class="language-json"><code class="lang-json">{
    "code": "NOT_MODIFIABLE_COLLECTION"
}
</code></pre></td></tr><tr><td>429</td><td><pre class="language-json"><code class="lang-json">{
    "code": "TOO_MANY_REQUESTS"
}
</code></pre></td></tr><tr><td>500</td><td><pre class="language-json"><code class="lang-json">{
    "code": "LOCK_ACQUISITION_FAILED"
}
</code></pre></td></tr><tr><td>500</td><td><pre class="language-json"><code class="lang-json">{
    "code": "UNKNOWN_ERROR"
}
</code></pre></td></tr></tbody></table>

#### Code Example (python)

```python
import datetime
import hmac
import uuid
import base64
import json
 
import requests
 
secret_key = "your-secret-key"
client_id = "your-client-id"
method = "PUT"
chain = "kairos" //test chain
contract_address = "contract-address"
token_id = "1"
path = f"/api/b2b-v1/nfts/{chain}/{contract_address}/{token_id}/metadata"
timestamp = str(int(datetime.datetime.now().timestamp()))
salt = str(uuid.uuid4())
plain_text = f"{client_id}|{method.upper()}|{path}|{timestamp}|{salt}"
print(f"plain_text: {plain_text}")
 
# Generate HMAC SHA256 Signature
hmac_obj = hmac.new(secret_key.encode('utf-8'), plain_text.encode('utf-8'), digestmod='sha256')
signature = base64.b64encode(hmac_obj.digest()).decode('utf-8')
 
host="https://api-dapp-portal.line-apps-beta.com"
url = f"{host}{path}"
headers = {
    "Content-Type": "application/json",
    "X-Auth-Client-Id": client_id,
    "X-Auth-Signature": f"{signature}",
    "X-Auth-Timestamp": timestamp,
    "X-Auth-Salt": f"{salt}",
}
body = {
    "name": "Hello",
    "uploadImageUrl": "https://line-objects-dev.com/dapp-portal-item/nft/N687e0c575d1ae92019138c5f/5734cbaa-5d49-4702-abaa-a3074808373f/image/9.jpg",
    "attributes": [
        {
            "trait_type": "color",
            "value": "red"
        },
        {
            "trait_type": "level",
            "value": "11 level"
        }
    ],
}
 
print("=====[request]=====")
print(f"request_url: {url}")
print(f"request_header: {headers}")
print(f"request_body: {body}")
response = requests.put(url, headers=headers, data=json.dumps(body))
print(f"HTTP Status: {response.status_code}")
print(f"Response Body: {response.text}")
```

#### Request Timeout

Read Timeout: Must be **at least 10 seconds**

* The server may take several seconds to respond depending on load and metadata processing time.
* Please ensure your HTTP client is configured to wait at least 10 seconds for a response.
