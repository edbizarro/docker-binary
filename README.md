## Docker Binary

[GitLab](https://gitlab.com/geekpobre/docker-binary) (Source) | [GitHub](https://github.com/geekpobre/docker-binary) (Mirror)



**Docker Binary** is a tool created to help those who want to use docker containers instead of local binaries without repeating `docker run` until their fingers fall, creating a thousand aliases or having to remember which image should be used.

With the capability to use a configuration file per project or per user it can also be used to call different versions of a binary on a project without tools like `nvm` , `pyenv`,  `rvm`, etc. You can even use it to sync which image is being used for command line stuff with other developers working on the same project!



#### Installation

```bash
$ curl https://gitlab.com/geekpobre/docker-binary/raw/master/install.sh | sudo bash
```



#### Usage

```bash
$ dab [key] [command]
```

```bash
------ [terminal]
$ dab php -v

Docker Binary: using project config.
PHP 7.1.11 (cli) (built: Oct 30 2017 22:02:40) ( NTS )
Copyright (c) 1997-2017 The PHP Group
Zend Engine v3.1.0, Copyright (c) 1998-2017 Zend Technologies

------ [.dockerbinary]
php=php:7.1-cli

```

 `dab` will search the `[key]` inside a `.dockerbinary` file on your current directory with a fallback to one on your `$HOME`. For now there is no merge between the two files so if it find one on your project folder only those keys will be available.



```
key=image[=command]
```

```
node=node:latest
yarn=node:latest
npm=node:latest=yarn
```

The `.dockerbinary` file should follow the format above with one key per line. For now there is no support for comments.

If you only pass the first two parameters `dab` will assume the key is the same as the binary you want to call inside the container. If those should be different for some reason you can then use a third parameter to set what is the binary being called.



#### Extra Parameters

Behind the scenes `dab` is calling the `docker run` command. You can customize some of those values exporting some variables on your shell.

`DOCKERBINARY_DATAMOUNT` | `/app`  - Define where the current folder will be mounted inside the container.

`DOCKERBINARY_SSHMOUNT` | `/root/.ssh` - Define where your ssh folder will be mounted inside the container.

`DOCKERBINARY_PARAMS` | `-it --rm`  - Define which parameters are used on the `docker run` command.

