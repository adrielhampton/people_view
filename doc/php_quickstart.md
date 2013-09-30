PHP Quickstart
==============

This quickstart uses an OAuth2 library which can be found here:

[https://github.com/adoy/PHP-OAuth2](https://github.com/adoy/PHP-OAuth2)

To install the library first download the archive: [https://github.com/adoy/PHP-OAuth2/archive/master.zip](https://github.com/adoy/PHP-OAuth2/archive/master.zip).  Unzip the contents into a directory that your PHP script can access.


Include the following files from the library in your script:

```php
<?php
require('path/to/client.php');
require('path/to/GrantType/IGrantType.php');
require('path/to/GrantType/AuthorizationCode.php');
?>
```

Create a client with your client id and secret:

```php
<?php
$clientId = 'yourClientId';
$clientSecret = 'yourClientSecret';
$client = new OAuth2\Client($clientId, $clientSecret);
?>
```

Now use the client to generate the authorization url.

```php
<?php
$redirectUrl    = 'http://www.myapp.com/oauth_callback';
$authorizeUrl   = 'https://foobar.nationbuilder.com/oauth/authorize';
$authUrl = $client->getAuthenticationUrl($authorizeUrl, $redirectUrl);
echo $authUrl;
?>
```

The above will output:

```
https://foobar.nationbuilder.com/oauth/authorize?response_type=code&client_id=yourClientId&redirect_uri=http%3A%2F%2Fwww.myapp.com%2Foauth_callback
```

Someone with access to the Nation's resources will have to visit that url in a browser, accept the application and retrive the authorization code form the page url. That page url will look something like:

```
http://foobar.nationbuilder.com/?code=123456abcdef
```

Use the code to generate an access token:

```php
<?php
$code = '123456abcdef';

$accessTokenUrl = 'https://foobar.nationbuilder.com/oauth/token';
$params = array('code' => $code, 'redirect_uri' => $redirectUrl);
$response = $client->getAccessToken($accessTokenUrl, 'authorization_code', $params);

$token = $response['result']['access_token'];
?>
```

Set the client's token

```php
<?php
$client->setAccessToken($token);
?>
```

The client is now ready to make resource requests

```php
<?php
$baseApiUrl = 'https://foobar.nationbuilder.com';
$client->setAccessToken($token);
$response = $client->fetch($baseApiUrl . '/api/v1/people');
print_r($response);
?>
```


The above will output something like:

```
Array
(
    [result] => Array
        (
            [page] => 1
            [total_pages] => 1
            [per_page] => 10
            [total] => 9
            [results] => Array
                (
                    [0] => Array
                        (
                            [id] => 10
                            ...

                        )
                    ...

                    [8] => Array
                        (
                            [id] => 19
                            ...
                        )


                )

        )

    [code] => 200
    [content_type] => application/json
)

```
