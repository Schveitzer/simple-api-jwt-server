# Simple Api with jwt authentication for test automation practice

Simple api for  test automation practice using [HAI Server](https://github.com/sumn2u/hai-server) Inspired from [JSON Server](https://github.com/typicode/json-server)

## Requirements
- Node >= 10.0 [How install Node](https://nodejs.org/en/download/)
- yarn >= 10.22 [How install Yarn](https://yarnpkg.com/getting-started/install)

## Getting started

Install dependencies

```
yarn install
```

Start Api server

```
yarn init:server
```

## How to login?

```
POST http://localhost:3000/auth/login
```
with the following data.

> Note: We can pick any user data from the list of users of the auth.json file.
```json
{
  "email": "nilson@email.com",
  "password":"nilson"
}
```

You should receive an access token with the following format

```json
{
   "access_token": "<ACCESS_TOKEN>"
}
```

You should send this authorization with any request to the protected endpoints

```
Authorization: Bearer <ACCESS_TOKEN>
```
## Routes

Based on the previous `db.json` file, here are all the default routes. You can also add [other routes](#add-custom-routes) using `--routes`.

### Routes
    /users
    /articles
    /authors
    /comments

```
GET    /users
GET    /users/1
POST   /users
PUT    /users/1
PATCH  /users/1
DELETE /users/1
```

### Filter

Use `.` to access deep properties

```
GET /users?age=35&gender=female
GET /users?id=1&id=2
```

### Paginate

Use `_page` and optionally `_limit` to paginate returned data.

In the `Link` header you'll get `first`, `prev`, `next` and `last` links.


```
GET /users?_page=7
GET /users?_page=7&_limit=20
```

_10 items are returned by default_

### Sort

Add `_sort` and `_order` (ascending order by default)

```
GET /users?_sort=age&_order=asc
```

For multiple fields, use the following format:

```
GET /users?_sort=age,gender&_order=desc,asc
```

### Slice

Add `_start` and `_end` or `_limit` (an `X-Total-Count` header is included in the response)

```
GET /users?_start=20&_end=30
```

_Works exactly as [Array.slice](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) (i.e. `_start` is inclusive and `_end` exclusive)_

### Operators

Add `_ne` to exclude a value

```
GET /users?id_ne=1
```

Add `_like` to filter (RegExp supported)

```
GET /users?name_like=Taylor
```

### Full-text search

Add `q`

```
GET /users?q=SILODYNE
```