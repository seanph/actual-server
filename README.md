# Actual Server

This is the main project to run my fork of [Actual](https://github.com/seanph/actual), a local-first personal finance tool. It provides a server to persist changes and make data available across all devices.

See the original repo [here](https://github.com/actualbudget/actual).

## Running

It's very easy to get started. Clone this repo, install deps, and start it:

```
git clone https://github.com/seanph/actual-server.git
cd actual-server
yarn install
yarn start
```

Go to <https://localhost:5006> in your browser and you'll see Actual.

## Running via Docker
To run using a Docker container you can use following commands;

```
git clone https://github.com/seanph/actual-server.git
cd actual-server
docker build -t actual-server .
docker run -p 5006:5006 actual-server
```

## Deploying

Whenever you want to update Actual, update the versions of `@actual-app/api` and `@actual-app/web` in `package.json`.

Alternatively `yarn link` any changes from the main repo, see `README.md` in [the main repo](https://github.com/seanph/actual) for more info.

### Persisting server data

One problem with the above setup is every time you deploy, it will wipe away all the data on the server. You'll need to bootstrap the instance again and upload your files.

Let's move the data somewhere that persists. Create a Docker volume that mounts at `/data`: Actual will automatically check if the `/data` directory exists and use it automatically.

_You can also configure the data dir with the `ACTUAL_USER_FILES` environment variable._

## Configuring the server URL

The Actual app is totally separate from the server. In this project, they happen to both be served by the same server, but the app doesn't know where the server lives.

The server could live on a completely different domain. You might setup Actual so that the app and server are running in completely separate places.

Since Actual doesn't know what server to use, the first thing it does is asks you for the server URL. If you are running this project, simply click "Use this domain" and it will automatically fill it in with the current domain. This works because we are serving the app and server in the same place.
