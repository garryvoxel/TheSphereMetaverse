# The Sphere Rest API

Backend for the sphere.

## Install

Set up Node v14.13.1

You can select node version with nvm: [https://github.com/nvm-sh/nvm](https://github.com/nvm-sh/nvm)

```bash
npm install
cp env.example .env
```

### Set up wallet

Create new wallet with electron cash slp edition, edit `.env` to reflect these.

### Set up database

Install postgres, create new database and user with superuser privileges

```bash
sudo -u postgres psql
create user username with encrypted password 'password';
alter role username superuser;
create database ets_db;
grant all privileges on database ets_db to username;
```

Then once this is set up, and the modifications made to `.env` (connString) just run

```bash
npm run db:migrate
```

You can do this any time to wipe db and restart fresh:

```bash
npm run db:reset
```

You may also want to install pgadmin4 for debugging.

#### For production

Use environment variables to configure connection to postgres: 

  -  POSTGRES_USER
  -  POSTGRES_PASSWORD
  -  POSTGRES_HOST
  -  POSTGRES_DB

### Documentation

Documentation on all api routes can be found by accessing `/doc` on the http server. These are automatically detected by swagger-autogen and additional information for routes are given inside the controllers (such as in `./src/auth/controllers/forgot-password.controller.js`).

You can find documentation on how to add these tags [here](https://www.npmjs.com/package/swagger-autogen). Additionally, more datatypes and configuration can be defined inside `src/swagger.js`. To generate documentation run:

```bash
npm run swagger-autogen
```

Which will produce `src/swagger_output.json`. This may be done every time there is update to documentation or routes.

#### Deploy

To upload to staging server, make sure you have pushed to git and are on latest revision, then just type:

```bash
make deploy-staging
```

Or for production:

```bash
make deploy-prod
```

## Contributing

### Lint

Check linter doesn't have toooo many warnings :) can disable some if it isn't useful.

```bash
npm run lint
```

### Test

Run unit tests / add unit tests

```bash
npm run test
```

#### Code Coverage

To check code coverage of tests run

```bash
npm run test:coverage
```

#### Blockchain Tests

Tests using real bitcoin transactions on mainnet can be run as well. These may require some setup like populating with bch.

```bash
npm run test:bch
```
