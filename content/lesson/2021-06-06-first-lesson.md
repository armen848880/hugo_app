---
title: First lesson
date: 2021-06-06T13:56:01.011Z
description: Some description
---
![Logo Sixense](/img/machine_icon.svg)

# Beyond monitoring backend

## Description

Beyond monitoring backend services.

## Installation

```bash
$ npm install
```

## Setting environment values

```bash
# Set a development template for .env file
cp resources/env/development.env .env
```

## Start dependencies for local development

The previous step is a mandatory to launch servers locally.

* At first start rabbitmq locally using docker

```bash
docker-compose up -d rabbitmq
```

* When rabbitmq is started you can start database locally using docker

```bash
docker-compose up -d mongodb
```

**BE CAREFUL**: Do not launch all containers at the same time (`docker-compose up`), it will cause the backend server to stop (due to connection timeout to rabbitMQ)

## Seed database

* Run seed data script `npm run db:seed`

Connection string is already set in `.env` file
Inserted data seed files can be found in `/tools/seed/**/*.ts`.
e.g: You can find users (and its unencrypted password) in `/tools/seed/2-users/users.ts`

## Running the app

```bash
# development
$ npm run start

# watch mode
$ npm run start:dev

# production mode
$ npm run start:prod
```

## Test

```bash
# unit tests
$ npm run test

# e2e tests
$ npm run test:e2e

# test coverage
$ npm run test:cov
```

## Seed database

1. Set database connection string in `.env` file
2. Run seed data script `npm run db:seed`

## Start dependencies for local development

```bash
# To start database locally using docker
docker-compose up -d mongodb
# docker-compose -f docker-compose.infra.yml  up -d mongodb

# To start rabbitmq locally using docker
docker-compose up -d rabbitmq
```

## Internationalization

### Extract translation strings from code

Following the command parse the code src folder and extract the translation string from
the code. If you have some manual translations to exact then add them in `src/i18n.ts`
file. They are extracted and merged in translation resource files stored under `locales/$lang` folder.

```bash
npm run i18n:extract
```

**Note:** Do not do any modifications (or adding new translation terms) directly in the locales/$lang/$namespace.json files. On translation extractions or synchronization from POEditor, they will be overridden.

To Know more about usage, follow the following library documentation.

* [i18next](https://www.i18next.com/translation-function/essentials)

To translate string:

```TypeScript
constructor(private readonly i18n: I18nService) {}
...

i18n.t("my string to translate", { lang: 'fr' });
```

## More information

* [Application file storage](./resources/docs/Storage.md)