# API Design

For all future API's I'm going to start using the Heroku API spec [found
here](https://www.gitbook.com/book/geemus/http-api-design/details).


The book goes into detail about the 'why's but below I'm going to summarize the
'what' since after reading the book I believe strongly in most of their
decisions.

## Heroku API Spec Decisions

* Always require TLS.  Any http traffic should just be rejected.  
* Always use API version, and use in a header:  

```sh
Accept: application/vnd.<my-api>+json; version=3
```

* Use an `ETag` header so users can cache responses  
* Always provide a `Request-Id` header (with UUID) for better debugging/tracing  
* Divide large requests into smaller pieces using the `Range` header. [More information on that here](https://devcenter.heroku.com/articles/platform-api-reference#ranges)  

### Requests

* Accept JSON request bodies 
* Use plural names for all resources unless it is a singleton (`/status` may be example of singleton)
* Prefer RESTFul endpoints that don't need special actions.  When special action is needed:

```sh
/resources/:resource/actions/:action
```
Ex:
```sh
/runs/{run_id}/actions/stop
```

* Downcase attributes/pathes. Use dash separation except in attributes to make JS easier
```
service-api.com/users
service-api.com/app-setups
service_class: "first"
```

* Except ID's and entities identified names.  Always **at least** ID's.

```sh
$ curl https://service.com/apps/{app_id_or_name}
$ curl https://service.com /apps/97addcf0-c182
$ curl https://service.com/apps/www-prod
```

* Minimize path nesting:

```sh
/orgs/{org_id}/apps/{app_id}/dynos/{dyno_id}
```
Should be:  
```
/orgs/{org_id}
/orgs/{org_id}/apps
/apps/{app_id}
/apps/{app_id}/dynos
/dynos/{dyno_id}
```

### Responses

* Use correct response codes
    + `200` for GET/POST/DELETE/PATCH that succeeds sync  
    + `201` for call that creates new resource.  Add a `Location` header of where new resource lives.  
    + `202` for POST/PUT/DELETE/PATCH that will occur async  
    + `206` request succeed for GET but only partial response (i.e. is a range request)  
    + `401` Unauthorized - request failed b/c user is not authenticated  
    + `403` Forbidden - request failed b/c user is not authorized for specific resource  
    + `422` Unprocessable Entity - request contained invalid parameters  
    + `429` Too Many Requests - client has been rate-limited, retry later  
    + `500` Internal Server Error - something went wrong on server
