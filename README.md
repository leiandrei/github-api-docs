# GitHub REST API — Get a User

Retrieve publicly available information about a GitHub user.

---

## Endpoint

```
GET https://api.github.com/users/{username}
```

---

## Path Parameters

| Parameter  | Type   | Required | Description                          |
|------------|--------|----------|--------------------------------------|
| `username` | string | ✅ Yes   | The GitHub username to look up. |

---

## Response

A successful authorized request returns HTTP `200 OK` with a JSON object. If the user is not found or access is restricted, an error status is returned.

### HTTP Status Codes

| Status Code | Description                              |
|-------------|------------------------------------------|
| `200`       | OK — Request was successful.             |
| `401`       | Unauthorized — Authentication required. |
| `403`       | Forbidden — Rate limit exceeded.         |
| `404`       | Not Found — User does not exist.         |
| `500`       | Internal Server Error.                   |

### Response Fields

| Field        | Type   | Description                          |
|--------------|--------|--------------------------------------|
| `login`      | string | GitHub username                      |
| `id`         | int    | User ID                              |
| `node_id`    | string | Global GraphQL identifier            |
| `avatar_url` | string | URL of the user's profile picture    |
| `html_url`   | string | URL of the user's GitHub profile     |
| `name`       | string | Full name listed on profile          |
| `company`    | string | Company listed on profile            |
| `blog`       | string | User's listed website or blog        |
| `location`   | string | User's listed location               |
| `email`      | string | User's public email address          |
| `followers`  | int    | Number of followers                  |
| `following`  | int    | Number of accounts the user follows  |
| `created_at` | string | Account creation date (ISO 8601)     |

---

## Example

### Request

```python
import requests

def get_github_user(username: str) -> dict:
    url = f"https://api.github.com/users/{username}"

    try:
        response = requests.get(url)
        response.raise_for_status()
        return response.json()
    except requests.exceptions.HTTPError:
        return Exception("HTTP ERROR OCCURRED.")
    except requests.exceptions.RequestException:
        return Exception("FETCH REQUEST ERROR.")

get_github_user("leiandrei")
```

### Response

```json
{
  "login": "leiandrei",
  "id": 186822292,
  "node_id": "U_kgDOCyKulA",
  "avatar_url": "https://avatars.githubusercontent.com/u/186822292?v=4",
  "html_url": "https://github.com/leiandrei",
  "name": "Lei Andrei Domaoal",
  "company": null,
  "blog": "",
  "location": null,
  "email": null,
  "followers": 0,
  "following": 0,
  "created_at": "2024-10-30T12:06:04Z",
  "updated_at": "2026-03-15T03:46:15Z"
}
```

---

## Notes

- This endpoint returns **publicly available** information only.
- Authenticated requests may return additional fields not available to unauthenticated users.
- Unauthenticated requests are subject to a lower rate limit. To avoid `403` errors, consider authenticating your requests using a [personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).

---

## References

- [GitHub REST API Docs](https://docs.github.com/en/rest/users/users)
