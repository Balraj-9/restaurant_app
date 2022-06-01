# GS_PROJECT_TEMPLATE

# Setup gs-template by dev-container
 - Clone the gs_project_template.
```sh
git clone https://github.com/Mindgreppers/gs_project_template.git
cd gs_project_template
```
 - You have not in master branch, then first go to master branch 
 ```sh
 git checkout master
 ```
 - Then choose run in remote container.
 

# You have to do a one time effort to setup the database users , replicate set etc.

*****************************
# ONE TIME EFFORT
******************************
 - TO pull the latest gs_service image
```sh
docker pull docker.io/adminmindgrep/gs_service:latest
```

- Now before running the dev cotnainer, need to change permission of mongodb key file
```sh
chmod 0600 .devcontainer/mongo-keyfile
```
- Now go to the project in VSCode and start the dev container.
   - Do these two steps
1. Open in container
2. Rebuild container


- Now setup mongodb user
- Get inside the mongodb container
```sh
docker exec -it mongodb1 bash
```

- Now run the script to bootstrap the cluster

- Login to mongodb shell 
 ```sh
mongosh mongodb://admin:mindgrep@mongodb1,mongodb2,mongodb3/admin
```
## Create the user

```sh
db.createUser(
{
user: "dev",
pwd: "dev",
roles: [ { role: "readWrite", db: "test" } ]
})
```
## Prisma 
 - Prisma is an open source next-generation ORM(object Relation Mapping)

## Now setup the schema in the databases (First time, or whenever doing migration)
- For Mongodb
```sh
export MONGO_TEST_URL=mongodb://dev:dev@mongodb1,mongodb2,mongodb3:27017/test
npx prisma db push --schema=src/datasources/mongo.prisma
```


- For postgres

```sh
export POSTGRES_URL=postgresql://postgres:postgres@postgresdb:5432
npx prisma db push --schema=src/datasources/postgres.prisma
```


