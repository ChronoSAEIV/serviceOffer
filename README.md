# ServiceOffer

Retrieve GTFS data with a GraphQL query (nodejs graphql-yoga) from a database (npm gtfs + mongoose + MongoDB)

Use case is made with Montreal public transit agencies: exo, RTL and STM

## Required
1. Docker
2. Docker Compose

## Run serviceoffer

`docker-compose up -d`

### Rebuild and up only serviceoffer container

`docker-compose up -d --build serviceoffer`

### Test app

GraphQL query console: <http://localhost:4000>

MongoDB admin: <http://localhost:8082/>

Connection URI: mongodb://mongo:27017/gtfs

Query available agencies
```
query {
  agencies {
    agency_key
  }
}
```

Query RTL specific data
```
query {
  agencies(agency_key: "rtl_gtfs") {
    routes(route_id: "889") {
      route_long_name
      trips(direction_id: "1") {
        trip_id
      }
    }
  }
}
```
#### Query from HTTP request (curl)

```
curl --request POST \
  --url http://localhost:4000/ \
  --header 'content-type: application/json' \
  --data '{"query":"{\n  agencies {\n    agency_key\n  }\n}\n"}'
```
# Contribute

You are welcome to contribute either directly via GitHub Pull Request or via Gerrit:
<https://review.gerrithub.io/q/project:transitco/serviceOffer+status:open>

1. ```git clone "ssh://username@review.gerrithub.io:29418/transitco/serviceOffer" serviceOffer && scp -p -P 29418 username@review.gerrithub.io:hooks/commit-msg "serviceOffer/.git/hooks/" ```
2. Modify your files
3. git add .
4. git commit -m "message"
5. git push ssh://username@review.gerrithub.io:29418/transitco/serviceOffer HEAD:refs/for/master%topic=whatever

Then use git commit --amend to modify the proposed change.