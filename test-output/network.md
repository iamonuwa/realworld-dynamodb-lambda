```
DELETE /__TESTUTILS__/purge
```
```
200 OK

"Purged all data!"
```
# Article
```
POST /users

{
  "user": {
    "email": "author-a890mv@email.com",
    "username": "author-a890mv",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-a890mv@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1hODkwbXYiLCJpYXQiOjE1NTczNDY3MzksImV4cCI6MTU1NzUxOTUzOX0.cLUYMAa05n5k1B1eQ7II5IFYSfiPPMrGuDPImMTVuKo",
    "username": "author-a890mv",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "authoress-jexssg@email.com",
    "username": "authoress-jexssg",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "authoress-jexssg@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvcmVzcy1qZXhzc2ciLCJpYXQiOjE1NTczNDY3MzksImV4cCI6MTU1NzUxOTUzOX0.O0odEXCK-Grad28YieUEQ1EpQkBPYov5nZ0i0gVpSFk",
    "username": "authoress-jexssg",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "non-author-sxv7my@email.com",
    "username": "non-author-sxv7my",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "non-author-sxv7my@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6Im5vbi1hdXRob3Itc3h2N215IiwiaWF0IjoxNTU3MzQ2NzM5LCJleHAiOjE1NTc1MTk1Mzl9.rofxgWUdwi_nkmHYu3ZggazKBB8CdFrNigrD9fsf41U",
    "username": "non-author-sxv7my",
    "bio": "",
    "image": ""
  }
}
```
## Create
### should create article
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-21k1mu",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346739919,
    "updatedAt": 1557346739919,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should create article with tags
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tag_a",
      "tag_b"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-8ga6ku",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346739971,
    "updatedAt": 1557346739971,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should disallow unauthenticated user
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce required fields
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "title must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "description must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "body must be specified."
    ]
  }
}
```
## Get
### should get article by slug
```
GET /articles/title-21k1mu
```
```
200 OK

{
  "article": {
    "createdAt": 1557346739919,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-21k1mu",
    "updatedAt": 1557346739919,
    "tagList": [],
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should get article with tags by slug
```
GET /articles/title-8ga6ku
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1557346739971,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-8ga6ku",
    "updatedAt": 1557346739971,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow unknown slug
```
GET /articles/2loalr
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [2loalr]"
    ]
  }
}
```
## Update
### should update article
```
PUT /articles/title-8ga6ku

{
  "article": {
    "title": "newtitle"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1557346739971,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "newtitle",
    "body": "body",
    "slug": "title-8ga6ku",
    "updatedAt": 1557346739971,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-8ga6ku

{
  "article": {
    "description": "newdescription"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1557346739971,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "body",
    "slug": "title-8ga6ku",
    "updatedAt": 1557346739971,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-8ga6ku

{
  "article": {
    "body": "newbody"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1557346739971,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "newbody",
    "slug": "title-8ga6ku",
    "updatedAt": 1557346739971,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow missing mutation
```
PUT /articles/title-8ga6ku

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article mutation must be specified."
    ]
  }
}
```
### should disallow empty mutation
```
PUT /articles/title-8ga6ku

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "At least one field must be specified: [title, description, article]."
    ]
  }
}
```
### should disallow unauthenticated update
```
PUT /articles/title-8ga6ku

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow updating non-existent article
```
PUT /articles/foo-title-8ga6ku

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foo-title-8ga6ku]"
    ]
  }
}
```
### should disallow non-author from updating
```
PUT /articles/title-8ga6ku

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be updated by author: [author-a890mv]"
    ]
  }
}
```
## Favorite
### should favorite article
```
POST /articles/title-21k1mu/favorite

{}
```
```
200 OK

{
  "article": {
    "createdAt": 1557346739919,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-21k1mu",
    "updatedAt": 1557346739919,
    "favoritedBy": [
      "non-author-sxv7my"
    ],
    "favoritesCount": 1,
    "tagList": [],
    "favorited": true
  }
}
```
```
GET /articles/title-21k1mu
```
```
200 OK

{
  "article": {
    "createdAt": 1557346739919,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 1,
    "slug": "title-21k1mu",
    "updatedAt": 1557346739919,
    "tagList": [],
    "favorited": true
  }
}
```
### should disallow favoriting by unauthenticated user
```
POST /articles/title-21k1mu/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow favoriting unknown article
```
POST /articles/title-21k1mu_foo/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-21k1mu_foo]"
    ]
  }
}
```
### should unfavorite article
```
DELETE /articles/title-21k1mu/favorite
```
```
200 OK

{
  "article": {
    "createdAt": 1557346739919,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 0,
    "slug": "title-21k1mu",
    "updatedAt": 1557346739919,
    "tagList": [],
    "favorited": false
  }
}
```
## Delete
### should delete article
```
DELETE /articles/title-21k1mu
```
```
200 OK

{}
```
```
GET /articles/title-21k1mu
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-21k1mu]"
    ]
  }
}
```
### should disallow deleting by unauthenticated user
```
DELETE /articles/foo
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown article
```
DELETE /articles/foobar
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
### should disallow deleting article by non-author
```
DELETE /articles/title-8ga6ku
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be deleted by author: [author-a890mv]"
    ]
  }
}
```
## List
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "t5lifb",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-eruvga",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741061,
    "updatedAt": 1557346741061,
    "author": {
      "username": "authoress-jexssg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "t5lifb",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "1c1gm5",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title--z9uywm",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741101,
    "updatedAt": 1557346741101,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "1c1gm5",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "nimdte",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-fgbp18",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741132,
    "updatedAt": 1557346741132,
    "author": {
      "username": "authoress-jexssg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "nimdte",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "605lf4",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-26wf80",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741166,
    "updatedAt": 1557346741166,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "605lf4",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "4j7bmu",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-xyhklt",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741197,
    "updatedAt": 1557346741197,
    "author": {
      "username": "authoress-jexssg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "4j7bmu",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "uyjlb",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-rn6q19",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741225,
    "updatedAt": 1557346741225,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "uyjlb",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "jpalgd",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-uai5cm",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741265,
    "updatedAt": 1557346741265,
    "author": {
      "username": "authoress-jexssg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "jpalgd",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "1sj4fa",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-l8appk",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741297,
    "updatedAt": 1557346741297,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "1sj4fa",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "lsi2qj",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-7r2obw",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741323,
    "updatedAt": 1557346741323,
    "author": {
      "username": "authoress-jexssg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "lsi2qj",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "g84bem",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-9xjamu",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741358,
    "updatedAt": 1557346741358,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "g84bem",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "zf66qe",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-mznqkh",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741386,
    "updatedAt": 1557346741386,
    "author": {
      "username": "authoress-jexssg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "zf66qe",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "2ovmpt",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-4u9umf",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741413,
    "updatedAt": 1557346741413,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "2ovmpt",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "7plgqq",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-hg36m8",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741439,
    "updatedAt": 1557346741439,
    "author": {
      "username": "authoress-jexssg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "7plgqq",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "ikmzfy",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-wq6sk6",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741466,
    "updatedAt": 1557346741466,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "ikmzfy",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "7zpid4",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-bev3hm",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741502,
    "updatedAt": 1557346741502,
    "author": {
      "username": "authoress-jexssg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "7zpid4",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "cpn7f7",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-5sknaw",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741547,
    "updatedAt": 1557346741547,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "cpn7f7",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "wjbkav",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-wzw1no",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741601,
    "updatedAt": 1557346741601,
    "author": {
      "username": "authoress-jexssg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "wjbkav",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "uu7cuu",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-563vz7",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741652,
    "updatedAt": 1557346741652,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "uu7cuu",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "npu80s",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-3u1s1e",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741707,
    "updatedAt": 1557346741707,
    "author": {
      "username": "authoress-jexssg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "npu80s",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "u5op6m",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-mezd99",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346741754,
    "updatedAt": 1557346741754,
    "author": {
      "username": "author-a890mv",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "u5op6m",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should list articles
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "u5op6m"
      ],
      "createdAt": 1557346741754,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mezd99",
      "updatedAt": 1557346741754,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "npu80s",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741707,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3u1s1e",
      "updatedAt": 1557346741707,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "uu7cuu"
      ],
      "createdAt": 1557346741652,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-563vz7",
      "updatedAt": 1557346741652,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "wjbkav"
      ],
      "createdAt": 1557346741601,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wzw1no",
      "updatedAt": 1557346741601,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cpn7f7",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741547,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5sknaw",
      "updatedAt": 1557346741547,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7zpid4",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741502,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-bev3hm",
      "updatedAt": 1557346741502,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ikmzfy",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1557346741466,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wq6sk6",
      "updatedAt": 1557346741466,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7plgqq",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741439,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hg36m8",
      "updatedAt": 1557346741439,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2ovmpt",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741413,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4u9umf",
      "updatedAt": 1557346741413,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "zf66qe"
      ],
      "createdAt": 1557346741386,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mznqkh",
      "updatedAt": 1557346741386,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g84bem",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741358,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9xjamu",
      "updatedAt": 1557346741358,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lsi2qj",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741323,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7r2obw",
      "updatedAt": 1557346741323,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "1sj4fa",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1557346741297,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-l8appk",
      "updatedAt": 1557346741297,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jpalgd",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741265,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uai5cm",
      "updatedAt": 1557346741265,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "uyjlb"
      ],
      "createdAt": 1557346741225,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-rn6q19",
      "updatedAt": 1557346741225,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4j7bmu",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1557346741197,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xyhklt",
      "updatedAt": 1557346741197,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "605lf4",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741166,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-26wf80",
      "updatedAt": 1557346741166,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nimdte",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741132,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fgbp18",
      "updatedAt": 1557346741132,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "1c1gm5",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1557346741101,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title--z9uywm",
      "updatedAt": 1557346741101,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "t5lifb",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741061,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eruvga",
      "updatedAt": 1557346741061,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles with tag
```
GET /articles?tag=tag_7
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "1sj4fa",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1557346741297,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-l8appk",
      "updatedAt": 1557346741297,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?tag=tag_mod_3_2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "uu7cuu"
      ],
      "createdAt": 1557346741652,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-563vz7",
      "updatedAt": 1557346741652,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7zpid4",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741502,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-bev3hm",
      "updatedAt": 1557346741502,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2ovmpt",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741413,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4u9umf",
      "updatedAt": 1557346741413,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lsi2qj",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741323,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7r2obw",
      "updatedAt": 1557346741323,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "uyjlb"
      ],
      "createdAt": 1557346741225,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-rn6q19",
      "updatedAt": 1557346741225,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nimdte",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741132,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fgbp18",
      "updatedAt": 1557346741132,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles by author
```
GET /articles?author=authoress-jexssg
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "npu80s",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741707,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3u1s1e",
      "updatedAt": 1557346741707,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "wjbkav"
      ],
      "createdAt": 1557346741601,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wzw1no",
      "updatedAt": 1557346741601,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7zpid4",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741502,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-bev3hm",
      "updatedAt": 1557346741502,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7plgqq",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741439,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hg36m8",
      "updatedAt": 1557346741439,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "zf66qe"
      ],
      "createdAt": 1557346741386,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mznqkh",
      "updatedAt": 1557346741386,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lsi2qj",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741323,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7r2obw",
      "updatedAt": 1557346741323,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jpalgd",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741265,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uai5cm",
      "updatedAt": 1557346741265,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4j7bmu",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1557346741197,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xyhklt",
      "updatedAt": 1557346741197,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nimdte",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741132,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fgbp18",
      "updatedAt": 1557346741132,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "t5lifb",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741061,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eruvga",
      "updatedAt": 1557346741061,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles favorited by user
```
GET /articles?favorited=non-author-sxv7my
```
```
200 OK

{
  "articles": []
}
```
### should list articles by limit/offset
```
GET /articles?author=author-a890mv&limit=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "u5op6m"
      ],
      "createdAt": 1557346741754,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mezd99",
      "updatedAt": 1557346741754,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "uu7cuu"
      ],
      "createdAt": 1557346741652,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-563vz7",
      "updatedAt": 1557346741652,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?author=author-a890mv&limit=2&offset=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "cpn7f7",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741547,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5sknaw",
      "updatedAt": 1557346741547,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ikmzfy",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1557346741466,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wq6sk6",
      "updatedAt": 1557346741466,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles when authenticated
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "u5op6m"
      ],
      "createdAt": 1557346741754,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mezd99",
      "updatedAt": 1557346741754,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "npu80s",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741707,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3u1s1e",
      "updatedAt": 1557346741707,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "uu7cuu"
      ],
      "createdAt": 1557346741652,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-563vz7",
      "updatedAt": 1557346741652,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "wjbkav"
      ],
      "createdAt": 1557346741601,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wzw1no",
      "updatedAt": 1557346741601,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cpn7f7",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741547,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5sknaw",
      "updatedAt": 1557346741547,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7zpid4",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741502,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-bev3hm",
      "updatedAt": 1557346741502,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ikmzfy",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1557346741466,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wq6sk6",
      "updatedAt": 1557346741466,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7plgqq",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741439,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hg36m8",
      "updatedAt": 1557346741439,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2ovmpt",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741413,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4u9umf",
      "updatedAt": 1557346741413,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "zf66qe"
      ],
      "createdAt": 1557346741386,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mznqkh",
      "updatedAt": 1557346741386,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g84bem",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741358,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9xjamu",
      "updatedAt": 1557346741358,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lsi2qj",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741323,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7r2obw",
      "updatedAt": 1557346741323,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "1sj4fa",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1557346741297,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-l8appk",
      "updatedAt": 1557346741297,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jpalgd",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741265,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uai5cm",
      "updatedAt": 1557346741265,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "uyjlb"
      ],
      "createdAt": 1557346741225,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-rn6q19",
      "updatedAt": 1557346741225,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4j7bmu",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1557346741197,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xyhklt",
      "updatedAt": 1557346741197,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "605lf4",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741166,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-26wf80",
      "updatedAt": 1557346741166,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nimdte",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741132,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fgbp18",
      "updatedAt": 1557346741132,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "1c1gm5",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1557346741101,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title--z9uywm",
      "updatedAt": 1557346741101,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "t5lifb",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741061,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eruvga",
      "updatedAt": 1557346741061,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow multiple of author/tag/favorited
```
GET /articles?tag=foo&author=bar
```
```
GET /articles?author=foo&favorited=bar
```
```
GET /articles?favorited=foo&tag=bar
```
## Feed
### should get feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
200 OK

{
  "articles": []
}
```
```
POST /profiles/authoress-jexssg/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "authoress-jexssg",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "npu80s",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741707,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3u1s1e",
      "updatedAt": 1557346741707,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "wjbkav"
      ],
      "createdAt": 1557346741601,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wzw1no",
      "updatedAt": 1557346741601,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7zpid4",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741502,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-bev3hm",
      "updatedAt": 1557346741502,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7plgqq",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741439,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hg36m8",
      "updatedAt": 1557346741439,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "zf66qe"
      ],
      "createdAt": 1557346741386,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mznqkh",
      "updatedAt": 1557346741386,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lsi2qj",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741323,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7r2obw",
      "updatedAt": 1557346741323,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jpalgd",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741265,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uai5cm",
      "updatedAt": 1557346741265,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4j7bmu",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1557346741197,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xyhklt",
      "updatedAt": 1557346741197,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nimdte",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741132,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fgbp18",
      "updatedAt": 1557346741132,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "t5lifb",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741061,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eruvga",
      "updatedAt": 1557346741061,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
POST /profiles/author-a890mv/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "author-a890mv",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "u5op6m"
      ],
      "createdAt": 1557346741754,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mezd99",
      "updatedAt": 1557346741754,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "npu80s",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741707,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3u1s1e",
      "updatedAt": 1557346741707,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "uu7cuu"
      ],
      "createdAt": 1557346741652,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-563vz7",
      "updatedAt": 1557346741652,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "wjbkav"
      ],
      "createdAt": 1557346741601,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wzw1no",
      "updatedAt": 1557346741601,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cpn7f7",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741547,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5sknaw",
      "updatedAt": 1557346741547,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7zpid4",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741502,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-bev3hm",
      "updatedAt": 1557346741502,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ikmzfy",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1557346741466,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wq6sk6",
      "updatedAt": 1557346741466,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7plgqq",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741439,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hg36m8",
      "updatedAt": 1557346741439,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2ovmpt",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741413,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4u9umf",
      "updatedAt": 1557346741413,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "zf66qe"
      ],
      "createdAt": 1557346741386,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mznqkh",
      "updatedAt": 1557346741386,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g84bem",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741358,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9xjamu",
      "updatedAt": 1557346741358,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lsi2qj",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741323,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7r2obw",
      "updatedAt": 1557346741323,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "1sj4fa",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1557346741297,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-l8appk",
      "updatedAt": 1557346741297,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jpalgd",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741265,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uai5cm",
      "updatedAt": 1557346741265,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "uyjlb"
      ],
      "createdAt": 1557346741225,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-rn6q19",
      "updatedAt": 1557346741225,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4j7bmu",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1557346741197,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xyhklt",
      "updatedAt": 1557346741197,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "605lf4",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741166,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-26wf80",
      "updatedAt": 1557346741166,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nimdte",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557346741132,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fgbp18",
      "updatedAt": 1557346741132,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "1c1gm5",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1557346741101,
      "author": {
        "username": "author-a890mv",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title--z9uywm",
      "updatedAt": 1557346741101,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "t5lifb",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557346741061,
      "author": {
        "username": "authoress-jexssg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eruvga",
      "updatedAt": 1557346741061,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow unauthenticated feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
## Tags
### should get tags
```
GET /tags
```
```
200 OK

{
  "tags": [
    "jpalgd",
    "tag_6",
    "tag_mod_2_0",
    "tag_mod_3_0",
    "1c1gm5",
    "tag_1",
    "tag_mod_2_1",
    "tag_mod_3_1",
    "4j7bmu",
    "tag_4",
    "g84bem",
    "tag_9",
    "cpn7f7",
    "tag_15",
    "tag_10",
    "zf66qe",
    "1sj4fa",
    "tag_7",
    "tag_19",
    "u5op6m",
    "nimdte",
    "tag_2",
    "tag_mod_3_2",
    "ikmzfy",
    "tag_13",
    "7plgqq",
    "tag_12",
    "t5lifb",
    "tag_0",
    "2ovmpt",
    "tag_11",
    "605lf4",
    "tag_3",
    "tag_16",
    "wjbkav",
    "npu80s",
    "tag_18",
    "lsi2qj",
    "tag_8",
    "tag_a",
    "tag_b",
    "tag_5",
    "uyjlb",
    "tag_17",
    "uu7cuu",
    "7zpid4",
    "tag_14"
  ]
}
```
# Comment
```
POST /users

{
  "user": {
    "email": "author-4pw6ix@email.com",
    "username": "author-4pw6ix",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-4pw6ix@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci00cHc2aXgiLCJpYXQiOjE1NTczNDY3NDMsImV4cCI6MTU1NzUxOTU0M30.pv0SfSjOBzUzEWhGqFEWCv1urhiIMvWd3LG23FyPEsY",
    "username": "author-4pw6ix",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "commenter-uxi1km@email.com",
    "username": "commenter-uxi1km",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "commenter-uxi1km@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImNvbW1lbnRlci11eGkxa20iLCJpYXQiOjE1NTczNDY3NDMsImV4cCI6MTU1NzUxOTU0M30.LBeM5ew-y_kWBTdIeIZG8yjsN4p33z8wRKAH1X8gJq8",
    "username": "commenter-uxi1km",
    "bio": "",
    "image": ""
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-acv9i6",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557346743240,
    "updatedAt": 1557346743240,
    "author": {
      "username": "author-4pw6ix",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
## Create
### should create comment
```
POST /articles/title-acv9i6/comments

{
  "comment": {
    "body": "test comment 8y3tc4"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "048fc596-1cbf-4b6c-840f-fe709c4add6a",
    "slug": "title-acv9i6",
    "body": "test comment 8y3tc4",
    "createdAt": 1557346743281,
    "updatedAt": 1557346743281,
    "author": {
      "username": "commenter-uxi1km",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-acv9i6/comments

{
  "comment": {
    "body": "test comment p81cc9"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "15f9377d-8389-40fc-ba51-cc678613eb6f",
    "slug": "title-acv9i6",
    "body": "test comment p81cc9",
    "createdAt": 1557346743321,
    "updatedAt": 1557346743321,
    "author": {
      "username": "commenter-uxi1km",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-acv9i6/comments

{
  "comment": {
    "body": "test comment wi7l0o"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "07ac3fb5-08dd-447f-b2f7-ba42362a921a",
    "slug": "title-acv9i6",
    "body": "test comment wi7l0o",
    "createdAt": 1557346743356,
    "updatedAt": 1557346743356,
    "author": {
      "username": "commenter-uxi1km",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-acv9i6/comments

{
  "comment": {
    "body": "test comment xndjng"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "9e01cfdf-51dd-418a-b0dd-d3b794f58ea0",
    "slug": "title-acv9i6",
    "body": "test comment xndjng",
    "createdAt": 1557346743394,
    "updatedAt": 1557346743394,
    "author": {
      "username": "commenter-uxi1km",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-acv9i6/comments

{
  "comment": {
    "body": "test comment f8yljv"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "e3f005d0-47b4-40b2-9cc2-7d177addc64f",
    "slug": "title-acv9i6",
    "body": "test comment f8yljv",
    "createdAt": 1557346743431,
    "updatedAt": 1557346743431,
    "author": {
      "username": "commenter-uxi1km",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-acv9i6/comments

{
  "comment": {
    "body": "test comment vwq6un"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "2f4f02ea-b2f0-4ae3-8f63-e7f2e25614ef",
    "slug": "title-acv9i6",
    "body": "test comment vwq6un",
    "createdAt": 1557346743481,
    "updatedAt": 1557346743481,
    "author": {
      "username": "commenter-uxi1km",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-acv9i6/comments

{
  "comment": {
    "body": "test comment oct4at"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "64849d64-a053-443d-9f05-9a9a9fb4bb20",
    "slug": "title-acv9i6",
    "body": "test comment oct4at",
    "createdAt": 1557346743523,
    "updatedAt": 1557346743523,
    "author": {
      "username": "commenter-uxi1km",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-acv9i6/comments

{
  "comment": {
    "body": "test comment 3kzzx9"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "47474730-3f35-45ed-b947-f7e45c062479",
    "slug": "title-acv9i6",
    "body": "test comment 3kzzx9",
    "createdAt": 1557346743556,
    "updatedAt": 1557346743556,
    "author": {
      "username": "commenter-uxi1km",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-acv9i6/comments

{
  "comment": {
    "body": "test comment 3542gc"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "27d49475-ad2d-48ee-be6e-b72ce7b9869f",
    "slug": "title-acv9i6",
    "body": "test comment 3542gc",
    "createdAt": 1557346743604,
    "updatedAt": 1557346743604,
    "author": {
      "username": "commenter-uxi1km",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-acv9i6/comments

{
  "comment": {
    "body": "test comment raw5ye"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "2011fcae-5b40-4dec-8583-0e368b9511db",
    "slug": "title-acv9i6",
    "body": "test comment raw5ye",
    "createdAt": 1557346743647,
    "updatedAt": 1557346743647,
    "author": {
      "username": "commenter-uxi1km",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
### should disallow unauthenticated user
```
POST /articles/title-acv9i6/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce comment body
```
POST /articles/title-acv9i6/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment must be specified."
    ]
  }
}
```
### should disallow non-existent article
```
POST /articles/foobar/comments

{
  "comment": {
    "body": "test comment 7wmqwx"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
## Get
### should get all comments for article
```
GET /articles/title-acv9i6/comments
```
```
200 OK

{
  "comments": [
    {
      "createdAt": 1557346743431,
      "id": "e3f005d0-47b4-40b2-9cc2-7d177addc64f",
      "body": "test comment f8yljv",
      "slug": "title-acv9i6",
      "author": {
        "username": "commenter-uxi1km",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557346743431
    },
    {
      "createdAt": 1557346743604,
      "id": "27d49475-ad2d-48ee-be6e-b72ce7b9869f",
      "body": "test comment 3542gc",
      "slug": "title-acv9i6",
      "author": {
        "username": "commenter-uxi1km",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557346743604
    },
    {
      "createdAt": 1557346743356,
      "id": "07ac3fb5-08dd-447f-b2f7-ba42362a921a",
      "body": "test comment wi7l0o",
      "slug": "title-acv9i6",
      "author": {
        "username": "commenter-uxi1km",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557346743356
    },
    {
      "createdAt": 1557346743523,
      "id": "64849d64-a053-443d-9f05-9a9a9fb4bb20",
      "body": "test comment oct4at",
      "slug": "title-acv9i6",
      "author": {
        "username": "commenter-uxi1km",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557346743523
    },
    {
      "createdAt": 1557346743556,
      "id": "47474730-3f35-45ed-b947-f7e45c062479",
      "body": "test comment 3kzzx9",
      "slug": "title-acv9i6",
      "author": {
        "username": "commenter-uxi1km",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557346743556
    },
    {
      "createdAt": 1557346743281,
      "id": "048fc596-1cbf-4b6c-840f-fe709c4add6a",
      "body": "test comment 8y3tc4",
      "slug": "title-acv9i6",
      "author": {
        "username": "commenter-uxi1km",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557346743281
    },
    {
      "createdAt": 1557346743321,
      "id": "15f9377d-8389-40fc-ba51-cc678613eb6f",
      "body": "test comment p81cc9",
      "slug": "title-acv9i6",
      "author": {
        "username": "commenter-uxi1km",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557346743321
    },
    {
      "createdAt": 1557346743647,
      "id": "2011fcae-5b40-4dec-8583-0e368b9511db",
      "body": "test comment raw5ye",
      "slug": "title-acv9i6",
      "author": {
        "username": "commenter-uxi1km",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557346743647
    },
    {
      "createdAt": 1557346743481,
      "id": "2f4f02ea-b2f0-4ae3-8f63-e7f2e25614ef",
      "body": "test comment vwq6un",
      "slug": "title-acv9i6",
      "author": {
        "username": "commenter-uxi1km",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557346743481
    },
    {
      "createdAt": 1557346743394,
      "id": "9e01cfdf-51dd-418a-b0dd-d3b794f58ea0",
      "body": "test comment xndjng",
      "slug": "title-acv9i6",
      "author": {
        "username": "commenter-uxi1km",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557346743394
    }
  ]
}
```
## Delete
### should delete comment
```
DELETE /articles/title-acv9i6/comments/048fc596-1cbf-4b6c-840f-fe709c4add6a
```
```
200 OK

{}
```
### only comment author should be able to delete comment
```
DELETE /articles/title-acv9i6/comments/15f9377d-8389-40fc-ba51-cc678613eb6f
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only comment author can delete: [commenter-uxi1km]"
    ]
  }
}
```
### should disallow unauthenticated user
```
DELETE /articles/title-acv9i6/comments/15f9377d-8389-40fc-ba51-cc678613eb6f
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown comment
```
DELETE /articles/title-acv9i6/comments/foobar_id
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment ID not found: [foobar_id]"
    ]
  }
}
```
# User
## Create
### should create user
```
POST /users

{
  "user": {
    "email": "user1-0.uediv7953jl@email.com",
    "username": "user1-0.uediv7953jl",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.uediv7953jl@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudWVkaXY3OTUzamwiLCJpYXQiOjE1NTczNDY3NDMsImV4cCI6MTU1NzUxOTU0M30.agvyQUW6Kogh91P5KhY32iSqkW0U4L7B4bottYBvslY",
    "username": "user1-0.uediv7953jl",
    "bio": "",
    "image": ""
  }
}
```
### should disallow same username
```
POST /users

{
  "user": {
    "email": "user1-0.uediv7953jl@email.com",
    "username": "user1-0.uediv7953jl",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username already taken: [user1-0.uediv7953jl]"
    ]
  }
}
```
### should disallow same email
```
POST /users

{
  "user": {
    "username": "user2",
    "email": "user1-0.uediv7953jl@email.com",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user1-0.uediv7953jl@email.com]"
    ]
  }
}
```
### should enforce required fields
```
POST /users

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "foo": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1,
    "email": 2
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Login
### should login
```
POST /users/login

{
  "user": {
    "email": "user1-0.uediv7953jl@email.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.uediv7953jl@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudWVkaXY3OTUzamwiLCJpYXQiOjE1NTczNDY3NDQsImV4cCI6MTU1NzUxOTU0NH0.kfUg0PfD0myT_yGqaJAJCKYCIlZtwjSuFiDjzD-qTe8",
    "username": "user1-0.uediv7953jl",
    "bio": "",
    "image": ""
  }
}
```
### should disallow unknown email
```
POST /users/login

{
  "user": {
    "email": "0.kd5919jc9ze",
    "password": "somepassword"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email not found: [0.kd5919jc9ze]"
    ]
  }
}
```
### should disallow wrong password
```
POST /users/login

{
  "user": {
    "email": "user1-0.uediv7953jl@email.com",
    "password": "0.d2kguzhoy4"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Wrong password."
    ]
  }
}
```
### should enforce required fields
```
POST /users/login

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {
    "email": "someemail"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Get
### should get current user
```
GET /user
```
```
200 OK

{
  "user": {
    "email": "user1-0.uediv7953jl@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudWVkaXY3OTUzamwiLCJpYXQiOjE1NTczNDY3NDQsImV4cCI6MTU1NzUxOTU0NH0.kfUg0PfD0myT_yGqaJAJCKYCIlZtwjSuFiDjzD-qTe8",
    "username": "user1-0.uediv7953jl",
    "bio": "",
    "image": ""
  }
}
```
### should disallow bad tokens
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Profile
### should get profile
```
GET /profiles/user1-0.uediv7953jl
```
```
200 OK

{
  "profile": {
    "username": "user1-0.uediv7953jl",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow unknown username
```
GET /profiles/foo_0.5g8sjachk4c
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User not found: [foo_0.5g8sjachk4c]"
    ]
  }
}
```
### should follow/unfollow user
```
POST /users

{
  "user": {
    "username": "followed_user",
    "email": "followed_user@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "followed_user@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImZvbGxvd2VkX3VzZXIiLCJpYXQiOjE1NTczNDY3NDQsImV4cCI6MTU1NzUxOTU0NH0.3IQkP5N_AVYs-RwACSuir2c3DK7DKZNESUbiCJX4eEE",
    "username": "followed_user",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
POST /users

{
  "user": {
    "username": "user2-0.ymn5l3zrxbs",
    "email": "user2-0.ymn5l3zrxbs@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.ymn5l3zrxbs@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAueW1uNWwzenJ4YnMiLCJpYXQiOjE1NTczNDY3NDQsImV4cCI6MTU1NzUxOTU0NH0.qbQHG7ow1X_hWHn5X9dQ6DC5k2EX-S4Jeaynzta_Jd0",
    "username": "user2-0.ymn5l3zrxbs",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow following with bad token
```
POST /profiles/followed_user/follow
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Update
### should update user
```
PUT /user

{
  "user": {
    "email": "updated-user1-0.uediv7953jl@email.com"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.uediv7953jl",
    "email": "updated-user1-0.uediv7953jl@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudWVkaXY3OTUzamwiLCJpYXQiOjE1NTczNDY3NDQsImV4cCI6MTU1NzUxOTU0NH0.kfUg0PfD0myT_yGqaJAJCKYCIlZtwjSuFiDjzD-qTe8"
  }
}
```
```
PUT /user

{
  "user": {
    "password": "newpassword"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.uediv7953jl",
    "email": "updated-user1-0.uediv7953jl@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudWVkaXY3OTUzamwiLCJpYXQiOjE1NTczNDY3NDQsImV4cCI6MTU1NzUxOTU0NH0.kfUg0PfD0myT_yGqaJAJCKYCIlZtwjSuFiDjzD-qTe8"
  }
}
```
```
PUT /user

{
  "user": {
    "bio": "newbio"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.uediv7953jl",
    "bio": "newbio",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudWVkaXY3OTUzamwiLCJpYXQiOjE1NTczNDY3NDQsImV4cCI6MTU1NzUxOTU0NH0.kfUg0PfD0myT_yGqaJAJCKYCIlZtwjSuFiDjzD-qTe8"
  }
}
```
```
PUT /user

{
  "user": {
    "image": "newimage"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.uediv7953jl",
    "image": "newimage",
    "bio": "newbio",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudWVkaXY3OTUzamwiLCJpYXQiOjE1NTczNDY3NDQsImV4cCI6MTU1NzUxOTU0NH0.kfUg0PfD0myT_yGqaJAJCKYCIlZtwjSuFiDjzD-qTe8"
  }
}
```
### should disallow missing token/email in update
```
PUT /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
PUT /user

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
### should disallow reusing email
```
POST /users

{
  "user": {
    "email": "user2-0.xfgtbefcvbh@email.com",
    "username": "user2-0.xfgtbefcvbh",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.xfgtbefcvbh@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAueGZndGJlZmN2YmgiLCJpYXQiOjE1NTczNDY3NDQsImV4cCI6MTU1NzUxOTU0NH0.w6to8HGclH3_NH67D69Wvxa9I5nAqlhDmTHc4LYpM4c",
    "username": "user2-0.xfgtbefcvbh",
    "bio": "",
    "image": ""
  }
}
```
```
PUT /user

{
  "user": {
    "email": "user2-0.xfgtbefcvbh@email.com"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user2-0.xfgtbefcvbh@email.com]"
    ]
  }
}
```
# Util
## Ping
### should ping
```
GET /ping
```
```
200 OK

{
  "pong": "2019-05-08T20:19:04.887Z",
  "AWS_REGION": "us-east-1",
  "DYNAMODB_NAMESPACE": "dev"
}
```
