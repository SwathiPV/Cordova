## Post request converting to get request.

This might be happening if you are using `http` to access a server which supports `https`. In this case, the http request
is automatically redirected to the `https` version, but instead of post, it will be a get request and the data is lost.

**Solution:**

Use `https` in all your requests.

## Request with query parameters redirect to GET Request

This happens when Append slash set to `true` in backend settings - so that slash will be appended at the end of the url (if the slash is not appended from the front-end). In that case, making an API call which has query parameter will be appended by the slash - which causes to redirection to the GET API.

Ex: `POST /aggregation_units?action=create` will be redirected to `GET /aggregation_units/?action=create`, Which results in Response of GET API.

This happens because, since the resource of the url i.e `/aggregation_units` doesn't have trailing slash and the `Append slash` is set to true, trailing slash will be appended at the end and leads to GET Request.

**Solution**

Append the trailing slash before the query paramters from the front-end

## Forbidden 403 error

If you try to make an API call directly to host instead of API, then Forbidded 403 error will be thrown.

Ex: `POST https://accounts.infratab.xyz/` will result in Forbidded error.

**Solution**

Please make sure, url of the API is all correct
