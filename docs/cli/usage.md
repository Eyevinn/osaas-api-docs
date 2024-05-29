Open Source Cloud provides a command line tool for communicating with Open Source Cloud services.

## Installation

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
