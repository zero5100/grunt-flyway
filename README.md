# grunt-flyway

> Run Flyway database migration tool with Grunt.

## WARNING
This Grunt plugin and has not been tested thoroughly yet so use it at your own risk!

The plugin supports all Flyway configuration options for `clean`, `baseline`, `migrate`, `repair`, `validate` and `info` commands.

## Getting Started

### Installing the plugin
This plugin requires Grunt `~0.4.2`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-flyway --save-dev
```

One the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-flyway');
```

### Installing Java
The plugin uses [Flyway](http://flywaydb.org) "The Agile Database Migration Framework" which is developed in Java.

So, you have to install Java and have the `java` executable available in your PATH.

## Flyway version
The plugin uses [Flyway](http://flywaydb.org) 4.1.

## The "flyway" task

### Overview
In your project's Gruntfile, add a section named `flyway` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  flyway: {
    options: {
      driver: 'com.mysql.jdbc.Driver',
      url: 'jdbc:mysql://localhost/flyway',
      user: 'flyway',
      password: 'flyway'
    },
    clean: {
      command: 'clean'
    },
    baseline: {
      options: {
        baselineDescription: 'Sample database created using Flyway:-)',
        baselineVersion: '1.0'
      },
      command: 'baseline'
    },
    migrate: {
      options: {
        locations: 'filesystem:src/main/resources/sql/migration'
      },
      command: 'migrate'
    }
  }
})
```

The name of the Grunt targets to use inside the `flyway` task configuration are not pre-defined, you can choose what you want to name those targets.

Any number of targets can be defined and you can have multiple targets with different configurations, for example:

```js
grunt.initConfig({
  flyway: {
    options: {
      driver: 'com.mysql.jdbc.Driver',
      url: 'jdbc:mysql://localhost/db1',
      user: 'flyway',
      password: 'flyway'
    },
    clean_db1: {
      command: 'clean'
    },
    clean_db2: {
      options {
        url: 'jdbc:mysql://localhost/db2'
      },
      command: 'clean',
    },
    baseline_db1: {
      options: {
        baselineDescription: 'Sample database created using Flyway:-)',
        baselineVersion: '1.0'
      },
      command: 'baseline'
    },
    baseline_db2: {
      options {
        url: 'jdbc:mysql://localhost/db2',
        baselineDescription: 'Sample database created using Flyway:-)',
        baselineVersion: '1.0'
      },
      command: 'baseline'
    },
    migrate_db1: {
      options: {
        locations: 'filesystem:src/main/resources/sql/migration'
      },
      command: 'migrate'
    },
    migrate_db2: {
      options {
        url: 'jdbc:mysql://localhost/db2',
        locations: 'filesystem:src/main/resources/sql/migration',
        placeholders: {
          name: 'Tom'
        }
      },
      command: 'migrate'
    }
  }
})
```

The only commands which are supported for the moment are `clean`, `baseline`, `migrate`, `repair`, `validate` and `info`.

### Options

Options' descriptions come from [Flyway's documentation](https://flywaydb.org/documentation/commandline/).

#### clean

See [clean command on flyway's documentation](https://flywaydb.org/documentation/commandline/clean)

#### baseline

See [baseline command on flyway's documentation](https://flywaydb.org/documentation/commandline/baseline)

#### migrate

See [migrate command on flyway's documentation](https://flywaydb.org/documentation/commandline/migrate)

#### repair

See [repair command on flyway's documentation](https://flywaydb.org/documentation/commandline/repair)

#### validate

See [validate command on flyway's documentation](https://flywaydb.org/documentation/commandline/validate)

#### info

See [info command on flyway's documentation](https://flywaydb.org/documentation/commandline/info)


### Usage Examples

Simply call the [Flyway](http://flywaydb.org) targets you've defined inside your Gruntfile:

`grunt flyway:clean`

`grunt flyway:baseline`

`grunt flyway:migrate`

`grunt flyway:repair`

`grunt flyway:validate`

`grunt flyway:info`

## Release History

### 0.4.1
  * Upgrade to Flyway 4.1.2

### 0.3.2
  * Upgrade to Flyway 3.2

### 0.3.0
  * Upgrade to Flyway 3.0

### 0.2.1

  * Add `develop` branch has been created, pull request have to be performed on this branch now
  * Upgrade to Flyway 2.3
  * **WARNING** : The plugin requires requires Grunt `~0.4.2` now

### 0.2.0

  * Added support for `validate` command
  * Added support for all options for each supported command
  * Added configuration validation
    * Required options cause an error when not present
    * Any extra option that is not available for selected command also causes an error
  * Fix JSHint Lint errors

### 0.1.1
  * Fix a Flyway classpath build problem under UNIX. The ';' character was used instead ':'.
