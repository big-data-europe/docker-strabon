# Strabon's Docker image

[Strabon](http://www.strabon.di.uoa.gr)'s Docker image.

## How to...
 
### Build it

This Docker image is parameterized by the desired version of Strabon to build, represented by the `STRABON_VERSION` Docker argument.

Example:

```bash
$ docker build -t bde2020/strabon:3.3.1 --build-arg STRABON_VERSION=3.3.1 .
```

### Run it

This Docker image allows you to configure the connection and credentials properties used by Strabon, which are typically located in respectively `/WEB-INF/connection.properties` and `/WEB-INF/credentials.properties` Strabon's WAR files.
To do so, simply define an environment variable named as follow:

```
STRABON_[CONNECTION | CREDENTIALS]_<property name>
```

Where:
- `<property name>` is the name of the property to override in its associated `connection.properties` (`CONNECTION`) or `credentials.properties` (`CREDENTIALS`) file.

Example:

```bash
$ docker run -e 'STRABON_CONNECTION_hostname=postgis' -e 'STRABON_CONNECTION_port=6789' bde2020/strabon:3.3.1
```

Or:

```bash
$ docker run --env-file 'secret-conf.env' bde2020/strabon:3.3.1
```

Where `secret-conf.env` could be:

```
STRABON_CONNECTION_hostname=postgis
STRABON_CONNECTION_port=6789
STRABON_CREDENTIALS_username=foo
STRABON_CREDENTIALS_password=bar
```