# Set Password and Token Based Authentication

Once you have <a href="http://eepurl.com/gfLTuH" target="_blank">requested an account</a> and received your username and temporary password, you will be able to set your password for making additional requests. This requires the use of the `authToken` endpoint which accepts a JSON payload with your username, temporary password, and new password. The new password field is not required on subsequent `authToken` requests but if populated your password will update. Below is a full example of a curl request of this method. The values within double brackets (`{{ value }}`) are variables where you would provide your information:

```
curl -X POST \
  'https://{{ domain }}/authToken' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
    "username" : "{{ username }}",
    "password": "{{ temporary password }}",
    "newPassword": "{{ new password }}"
  }'
```

## Response

A successful request will return a `token` in the response which means your password has been set. 

```
{
  "type": "SUCCESS",
  "token": "{{ your new token will here }}"
}
```

## Tokens

Once you have a token, you can use it along with your username to make requests to other endpoints. Tokens are set to expire every hour (or `3600` seconds) so you will need to keep track of the expiration to regenerate your token. Retrieving a new token can be done using the same `authToken` endpoint. All that’s needed is your username and password.

```
curl -X POST \
  'https://{{ domain }}/authToken' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
    "username" : "{{ username }}",
    "password": "{{ temporary password }}"
  }'
```

## Forgot Password

If you forget your password, you can reset it with the `/forgotPassword` and `/confirmPassword` endpoints. Curl `/forgotPassword` to receive an email with a verification code. Then curl `/confirmPassword` with your username, verification code, and new password.  You will receive the email at the address you provided to us when setting up your account.

### forgotPassword

```
curl -X POST \
  'https://{{ domain }}/forgotPassword' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
    "username" : "{{ username }}",
  }'
```

### confirmPassword

```
curl -X POST \
  'https://{{ domain }}/confirmPassword' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
    "username" : "{{ username }}",
  }'
```

## Summary

* Contact us through [Support](mailto:eligibilityapi@nycopportunity.nyc.gov) if you need to update your account information.
* The `authToken` endpoint is used to set your new password using your username and temporary password.
* The `authToken` endpoint responds with a token that expires after 1 hour (`3600` seconds).
* The `authToken` endpoint is also used to retrieve new tokens.

## Next

[Making a Request](/making-a-request)

<br>
<br>