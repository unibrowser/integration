# Unibrowser Integration

**NOTE**: Requires `docker` to be installed

## Building Unibrowser
The Dockerfiles contains in this repository will test and build the three parts of Unibrowser: the scraper, the backend server, and the frontend web application. To test and build each component, run the following commands:

```text
> docker run --rm -d -p 27017:27017 mongo
> docker build . -t unibrowser/scraper -f Dockerfile.scraper
> docker build . -t unibrowser/backend -f Dockerfile.backend
> docker build . -t unibrowser/frontend -f Dockerfile.frontend
```

# Running Unibrowser
Once the components have been built, you can run Unibrowser by issues the following commands.

```text
> docker run --rm -d --network host unibrowser/frontend
> docker run --rm -d --network host unibrowser/backend
> docker run --rm -d --network host unibrowser/scraper
```

The `--network host` option tells the container to run on the same localhost network your computer is using. This is required to allow the containers to connect to MongoDB. The frontend binds to port 80 on your localhost, ad the backend binds to port 8080 on your localhost.

The first time you run the `mongo` image, Docker will "pull" the image from the remote repository and install it locally. Subsequent calls to `docker run` with the `mongo` image will use your local image to start the MongoDB container.
