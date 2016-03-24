# Docker CentOS rbenv image

A [Docker](https://docs.docker.com/introduction/understanding-docker/) image for configuring Ruby on [CentOS](http://www.centos.org/) 7. Uses [ruby-build](https://github.com/sstephenson/ruby-build) and [rbenv](https://github.com/sstephenson/rbenv) to build/switch Ruby versions based on your project's configuration.

### Image usage

Create a `Dockerfile` in your Ruby project that uses `docker-centos-rbenv` as its base image. Switch to the unprivileged application user before running application-specific commands. For example, to run a Rails server:

```Dockerfile
FROM toastercup/docker-centos-rbenv

ENV PORT 8080

COPY . $APP_PATH
RUN chown $APP_USER -R $APP_PATH

USER $APP_USER
WORKDIR $APP_PATH
RUN bundle install

EXPOSE $PORT
CMD bundle exec rails s -p $PORT
```

### Specifying a Ruby version

Your project must specify a local Ruby version via the `.ruby-version` file, which should be placed in the same directory as your project's `Dockerfile`. The contents of the file are simply the desired Ruby version, i.e. `2.3.0`.

### Why, though?

With this script, you are not dependent on the Docker image maintainer to tag a new Ruby release for you, nor do you have to fork the base image to update Ruby!

![Great Job!](http://www.whump.net/files/images/GreatJob.jpg)
