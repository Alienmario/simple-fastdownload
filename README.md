[![CI](https://github.com/Alienmario/simple-fastdownload-redux/actions/workflows/plugin.yml/badge.svg)](https://github.com/Alienmario/simple-fastdownload-redux/actions/workflows/plugin.yml)

# simple-fastdownload

Provides fastdownload support for srcds without the need for webhosting. By default, it will automatically change the value of `sv_downloadurl` and serve files that are either in the downloadables stringtable or the mapcycle.

- For usage on a local server, you should be all set.  
If you have already specified a local ip in launch parameters, then you may need to set `sv_downloadurl_hostname` to `localhost`.
- For usage on a live server, edit `sv_downloadurl_hostname` to match your server's public ip or hostname, or use `+ip x.x.x.x` launch paramer.
- It's recommended to also use `-strictportbind` launch parameter. Otherwise the hostport convar used to construct the url may turn incorrect.


> If all of above fails, disable auto-setting the url with `sv_downloadurl_autoupdate 0` and add it manually in server.cfg: `sv_downloadurl http://<hostname>:<serverport>/fastdl`.
#
### Good to know
Configuration file is automatically created at **cfg\sourcemod\plugin.simple-fastdownload-redux.cfg**.

Files are preprocessed (added to whitelist and compressed) on every mapchange. If you don't change downloads at runtime, you can save some time by setting `sv_downloadurl_autoreload` to 0.

Files inside the custom folder are fully supported.

#
### Compressor
By default, if `System2` extension is installed, this will also automatically compress missing .bz2 archives to speed up the downloads further.
If `sv_downloadurl_bz2folder` is not empty, such folder will be added as a search path for bz2 files, as well as used by the compressor.
Otherwise, the compressed files are placed in same folder as the source file.
#
### Dependencies
* [Conplex & Webcon](https://forums.alliedmods.net/showthread.php?t=270962)
* [(Optional) System2](https://forums.alliedmods.net/showthread.php?t=146019)
#
### ConVars
ConVar | Default Value | Description 
------ | ------- | --------- 
sv_downloadurl_urlpath | "fastdl" | path for fastdownload url eg: `fastdl`
sv_downloadurl_autoupdate | 1 | should sv_downloadurl be set automatically
sv_downloadurl_hostname | "" | either an empty string, or hostname to use in downloadurl with no trailing slash eg: `fastdownload.example.com`
sv_downloadurl_add_mapcycle | 1 | should all maps in the mapcycle be added to the download whitelist, *recommended value: 1*
sv_downloadurl_add_downloadables | 1 | should all files in the downloads table be added to the download whitelist, *recommended value: 1*
sv_downloadurl_autoreload | 1 | should reload (and compress) files in the download whitelist on each mapchange
sv_downloadurl_bz2folder | bz2 | either an empty string, or base folder for .bz2 files in game root folder eg: bz2
sv_downloadurl_compress | 1 | should files in the download whitelist get automatically compressed as bz2 archives; requires System2 extension
sv_downloadurl_compress_max_concurrent | 2 | maximum concurrently compressed files; increasing this value should speed up processing at the cost of higher resource usage (primarily CPU)
sv_downloadurl_log_access | 1 | should all fastDL requests get logged
sv_downloadurl_log_general | 1 | should general info get logged via Sourcemod logging

### Commands
Command | Description
------ | ------
sm_fastdownload_list_files | prints a list of all files that are currently in the download whitelist, *note: for server console only*
