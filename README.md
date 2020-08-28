An easy to use modlist installer for Minecraft Java Edition.

## Usage for users

This is a GO version of the master branch that exists in order to support FreeBSD

Usage is as simple as downloading the [latest release](https://github.com/rleathart/mcmli/releases)
for your operating system to a modpack directory and then running the executable.
The installer will ask you to specify a remote: just copy and paste a link
to a `modpack.remote` file.
For reference, after running the installer your directory structure will look like:
```
./
├── .install.remote
├── config/
├── main.modlist
├── install.exe
└── mods/
```

On macOS and Linux, you will have to set execute permissions for the file before
running:
```
cd /path/to/your/modpack/directory
chmod u+x install*
```
Now you can run the binary either by double clicking it, or in the CLI.

## Usage for authors

The installer reads modlists from all files with the `.modlist` extension in
alphabetical order. Typical use should only require one modlist which could be
called something like `main.modlist` or `<modpack-name>.modlist`.

### Modlist format

Perhaps the easiest way to understand the modlist format is to see an example:
```
[mods]
# This line is a comment and will be ignored.
https://somesite/commonmod.jar # Comments after URLs must be preceeded by whitespace.
<Client-Only>
https://somesite/client-only-mod.jar
<Server-Only>
https://somesite/server-only-mod.jar

[config] <Always-Fetch>
https://somesite/commonconfig.cfg
```
We refer to text inside square `[]` or angle `<>` brackets as control directives.
Control directives may occur on lines by themselves or on the same line as other
control directives. Text inside `[]` brackets specifies the directory (relative
to the executable) in which to download the following URLs. Text inside `<>`
brackets specify options for the current 'context' (until the next set of `[]`
brackets). Valid options are:
-  `<Always-Fetch>` Always download these files regardless of whether or not
they are present already.
-  `<Smart-Fetch>` Only download these files if they do not exist (default behaviour).
-  `<Server-Only>` Only download these files if the current instance is a server.
-  `<Client-Only>` Only download these files if the current instance is a client.
-  `<Common>` Download these files for both servers and clients (default).
