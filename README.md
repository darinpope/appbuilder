# appbuilder

## Installation

* `brew tap choria-io/tap`
* `brew install choria-io/tap/appbuilder`
* `appbuilder --version`

## Preparing to start command development

Instead of using the default locations for `appbuilder`, which for macOS is `$HOME/Library/Application Support`, we want to use a Git repository. Therefore, we need to set the `XDG_CONFIG_HOME` environment variable. For our installation, we are setting the environment in `$HOME/.zshrc`:

`export XDG_CONFIG_HOME=$HOME/github`

Why `XDG_CONFIG_HOME`? The only XDG value that appbuilder uses is ConfigHome in [builder.go](https://github.com/choria-io/appbuilder/blob/main/builder/builder.go#L85)

I also created an `appbuilder` Git repository because as referenced in `builder.go`, `appbuilder` is automatically appended to the Source Locations paths from `appbuilder info`:

```
appbuilder info
Choria Application Builder

        Debug Logging (BUILDER_DEBUG): false
  Configuration File (BUILDER_CONFIG): not specified
        Definition File (BUILDER_APP): not specified
                     Source Locations: /Users/dpope/github/appbuilder, /etc/appbuilder
```                     

We're also going to need to do symlinking later on. For our environment, we make sure we have a directoy on `PATH`:

`export PATH=$HOME/.local/bin`

At this point, we are ready to start command development.

## Creating a command

* In the `appbuilder` Git repository, create a `<command>-app.yaml` where `command` is the CLI you will want to call. For example, `demo-app.yaml` will translate to `demo`
* Link `appbuilder` to the command. For example, for `demo`:
  * `ln -s /usr/local/bin/appbuilder $HOME/.local/bin/demo`
* Test the command
  * `demo help`

## XDG directory locations

https://github.com/adrg/xdg#xdg-base-directory
