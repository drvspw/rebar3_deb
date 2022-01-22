## rebar3_deb
A rebar plugin to package a release as debain package.


## Build
```
$ rebar3 compile
```

## Use
Add the plugin to your rebar config:
```erlang
{project_plugins, [
	{rebar3_deb, "0.1.0"}
]}.

%% option for rebar3_deb plugin
{deb, [
       {control_files_dir, "package/debian"}, %% directory where debian control files are present
       {source_dirs, []}, %% other source directories to package
       {install_dir, "/opt"}, %% where the release is installed
       {systemd_unit_files, ["package/systemd/sample_app.service"]} %% optionally package a systemd unit file
]}.
```

The plugin provides templates for debain control files. To generate them use
```bash
$ rebar3 new debian-control-files
```
This would create `control`, `postinst` and `prerm` files in `package/debian` directory. These files are `mustache` template files. At plugin runtime, the plugin renders the template with the appropriate values for `{{package}}`, `{{version}}` and `{{name}}`.


Then call the pluging to create a debian package
```bash
$ rebar3 debian
<Plugin Output>
```
This command accetps the same command line arguments as `rebar3 tar` command.

## Release
- Make appropriate code changes
- Update version in `src/rebar3_deb.app.src`
- Update plugin version in `examples/sample_app/rebar.config`
- Commit changes and cut a new release.
- Publish to [hex.pm](https://hex.pm)

## Use plugin from github
```erlang
{project_plugins, [
	{rebar3_deb, {git, "https://github.com/drvspw/rebar3_deb.git", {tag, "<release tag>"}}}
]}.
```
The release tag can be found in [releases](https://github.com/drvspw/rebar3_deb/releases) page.
