## Synopsis

```
osc intercom [options] [command]
```

where available `command`s are:
 
 - `list-productions`
 - `create-production`
 - `delete-production`

## Description

Manage Intercom systems in Open Source Cloud. Create, list and delete productions.

## Usage

Find installation [instructions](usage.md) and general instructions on how to use the CLI [here](usage.md).

### List available productions

To list available productions and lines in each production for an Intercom system called `vg52` you run.

```
osc intercom list-productions vg52 
```

And it will for example output the following:

```
1: eyevinn
+-- 1: social (5)
+-- 2: dev (0)
```

This system has one production called `eyevinn` and has id `1`. It contains 2 lines and line with id `1` has currently 5 participants.

### Create production

To create a new production and lines for an Intercom system called `vg52` you run the following command.

```
osc intercom create-production vg52 myproduction line1 line2 line3
```

This will create one production called `myproduction` and that has three lines `line1`, `line2` and `line3`.

### Remove a production

To remove a production and all its lines you need the id of the production to remove. To remove production `eyevinn` in this example you would run.

```
osc intercom delete-production vg52 1
```

You will be asked to confirm the removal before it is removed.
