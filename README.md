## [70 days left](https://yourcountdown.to/main-en-lair-pa-1554481335) !!!!!!!!!!

## Run project

### Start App, DB & Adminer

`docker-compose up`

See credentials in docker-compose.yml

Access GraphQL Playground here : http://localhost:4000/graphql

Access React app here : http://localhost:3000/

### .env

Copy both `web/.env.dist` and `server/.env.dist` to `web/.env` and `server/.env`

Setup a Stripe account and get your Stripe publishable key and secret key in your .env files

Create a Stripe plan on Stripe website : Billing > Products (example: create a "Dreamteam Solo" product, with a plan called "Standard")  
Insert the Plan id (something like `plan_AFCHJhjjgvhcf`) in your `server/.env`

### Basic commands

`yarn gen:types` : update GraphQL schemas if you added a new query / mutation in your React components

`yarn trans:update` : update the JSON files in web/src/translations/locales after you add a new `<FormattedMessage />` tag (see **How to manage texts and translations**) in your React components

### How to manage texts and translations

Where you want to insert text, place a `<FormattedMessage />` tag (from react-intl package) with an **id** and **defaultMessage**

Then run `yarn trans:update` to update the JSON translation files

### How to send an email

Create in `services/mail.ts` a new function that you export where you need it (most probably in resolver).

Since we are using [email-template](https://github.com/niftylettuce/email-templates) you need to create a template for your mail in `pug` into the folder emails.
`template` option match the name of the folder.
