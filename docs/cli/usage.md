Open Source Cloud provides a command line tool for communicating with Open Source Cloud services.

## Installation

### Node

Ensure you have Node and NPM installed first.

```
% npm --version
10.5.0
% node --version
v21.7.1
```

Install using NPM

```
% npm install -g @osaas/cli
```

This will install the CLI tool `osc` and to verify that it is installed correctly:

```
% osc -h
```

This should output a reference to all available commands.

### Public Docker Image

You must have Docker installed and for instructions on how to install Docker see the [Docker website](https://docs.docker.com/install/).

```
% docker --version
Docker version 24.0.7, build afdd53b
```

The official OSC CLI version Docker image is hosted on Docker Hub in the `eyevinntechnology/osccli` repository.

```
% docker run --rm -it eyevinntechnology/osccli help
Usage: osc [options] [command]

Options:
  --env <environment>                                       Environment to use
  -h, --help                                                display help for command

Commands:
...
```

For more information about the docker run command, see the [Docker reference guide](https://docs.docker.com/engine/reference/run/).

Providing environment variables using the `-e` flag. In this example we are using this flag to provide the `OSC_ACCESS_TOKEN` environment variable that contains your personal access token and list the Encore instances running.

```
% docker run --rm -it -e OSC_ACCESS_TOKEN=<pat> eyevinntechnology/osccli list encore
```

## Usage

The CLI requires the OSC credentials (Personal Access Token) is found in the environment variable `OSC_ACCESS_TOKEN`. To list all running Test Adserver instances you run:

```
% export OSC_ACCESS_TOKEN=<your-secret-pat>
% osc list eyevinn-test-adserver
boris
website
```

The general structure of the commands are:

```
osc [options] [command]
```

To display help for a command you run

```bash
% osc help [command]
```

A `[command]` can have sub commands:

```
osc <command> [options] [subcommand]
```

Some options, e.g. `--env` is global and applies to all command and subcommands, for example:

```bash
% osc --env stage admin list-instances eyevinn eyevinn-test-adserver
```
