# BepInEx for Valheim, Full Pack

This pack is for Valheim modding. It includes

* the unstripped Unity libraries,
* Mono libraries from Unity for .NET 4.5,
* the System.Buffers library,
* Windows and Unix versions of BepInEx and UnityDoorstop,
* a BepInEx config with the console enabled by default,
* and a bash script to start the server on Linux via cli.

It runs both on clients and servers.

## Table of Contents

* [Table of Contents](#table-of-contents)
* [Links](#links)
* [Building the pack yourself](#building-the-pack-yourself)
    + [Requirements](#requirements)
    + [DLLs](#dlls)
    + [Extras](#extras)
* [FAQ](#faq)
    + [Are you open to pull requests?](#are-you-open-to-pull-requests-)
    + [Will this package be maintained?](#will-this-package-be-maintained-)
    + [Can I submit <some-random-name>.dll to the pack?](#can-i-submit--some-random-name-dll-to-the-pack-)
    + [I'm getting a weird audio-related error when I start Valheim.](#i-m-getting-a-weird-audio-related-error-when-i-start-valheim)
    + [How do I configure my server on Linux with the bash script?](#how-do-i-configure-my-server-on-linux-with-the-bash-script-)
    + [What's my Linux server's password if I use the bash script?](#what-s-my-linux-server-s-password-if-i-use-the-bash-script-)
    + [UNSAFE_ROOT_EXECUTION](#unsafe-root-execution)
    + [There are DLLs that aren't really necessary in the pack](#there-are-dlls-that-aren-t-really-necessary-in-the-pack)
    + [There's a .NET/mono/Unity DLL missing from the pack](#there-s-a-net-mono-unity-dll-missing-from-the-pack)
* [SHA-256 File Checkums](#sha-256-file-checkums)

## Links

* [GitHub](https://github.com/U-1F31A/BepInEx_Valheim_Full)
* [Thunderstore](https://valheim.thunderstore.io/package/1F31A/BepInEx_Valheim_Full)

## Building the pack yourself

Notes:

* Before you start, create an empty folder to put everything in. Start clean and don't mix.
* We use `C:\` with the standard Unity install directory as an example. Replace it with your own paths.

### Requirements

* Get [Mono 6.12.0 Stable (6.12.0.122) 64-bit](https://www.mono-project.com/download/stable/)
* Get [Unity 2019.4.20f1](https://unity3d.com/get-unity/download/archive)
	* *Note:* You can extract the installer to get access to the DLLs if you don't want to install Unity
* Get [BepInEx for Windows x64 5.4.8](https://github.com/BepInEx/BepInEx/releases/tag/v5.4.8)
* Get [BepInEx for Unix 5.4.8](https://github.com/BepInEx/BepInEx/releases/tag/v5.4.8)
* Get [UnityDoorstop for Windows x64 3.3.0.0](https://github.com/NeighTools/UnityDoorstop/releases/tag/v3.3.0.0)
* Get [UnityDoorstop.Unix for Linux 1.5.0.0](https://github.com/NeighTools/UnityDoorstop.Unix/releases/tag/v1.5.0.0)

### DLLs

1. From `C:\Program Files\Mono\lib\mono\4.5`
	* Copy all DLLs
2. Copy the whole folder `C:\Program Files\Mono\lib\mono\4.5\Facades` (not just the DLLs inside, the folder `Facades`)
	* Keep the DLLs in that subfolder
3. From `C:\Program Files\Unity\Hub\Editor\2019.4.20f1\Editor\Data\MonoBleedingEdge\lib\mono\4.5`
	* Copy all DLLs (overwrite when prompted)
4. Copy the whole folder `C:\Program Files\Unity\Hub\Editor\2019.4.20f1\Editor\Data\MonoBleedingEdge\lib\mono\4.5\Facades` (not just the DLLs inside, the folder `Facades`)
	* Keep the DLLs in that folder, overwrite when prompted
5. From `C:\Program Files\Unity\Hub\Editor\2019.4.20f1\Editor\Data\Managed\UnityEngine`
	* Copy all DLLs (overwrite when prompted)
6. From `C:\Program Files\Unity\Hub\Editor\2019.4.20f1\Editor\Data\PlaybackEngines\windowsstandalonesupport\Variations\mono\Managed`
	* Copy all DLLs (overwrite when prompted)
7. Get a copy of System.Buffers (target .NET 4.5) and add the DLL: https://www.nuget.org/packages/System.Buffers/
8. From the DLLs you've collected, delete `UnityEngine.AudioModule.dll`

### Extras

* Copy our `doorstop_config.ini`
* Copy our custom `valheim.sh` bash script for Linux servers
* Put the pack into your Valheim client or server, run it once to generate the `config/` directory with default `BepInEx/config/BepInEx.cfg`. Then set `Enabled = true` in the category `[Logging.Console]` of `BepInEx/config/BepInEx.cfg` to enable the console, and copy the config folder to your pack
* Run the checksums (bash command): `find . -type f -exec sha256sum {} \;`

## FAQ

### Are you open to pull requests?

Yes.

### Will this package be maintained?

Yes. Both the GitHub and the packages on the mod websites are maintained by a team. If any one person becomes unavailable, the others can continue to maintain it. Should the whole team want to stop, we're open to considering new volunteers.

### Can I submit <some-random-name>.dll to the pack?

This pack is only meant for .NET/Mono/Unity DLLs. If it's part of that, sure. Make sure to include where you got it from and why you need it.

### I'm getting a weird audio-related error when I start Valheim.

Did you remove `UnityEngine.AudioModule.dll` (see [Building the pack yourself](#building-the-pack-yourself)) when building the pack yourself?

### How do I configure my server on Linux with the bash script?

Open the bash script in your favorite text editor, look at the very top.

### What's my Linux server's password if I use the bash script?

If you didn't configure the bash script to set your own password, it'll autogenerate a random password and show it in your terminal on startup.

### UNSAFE_ROOT_EXECUTION

When you try to run the Linux server via the bash script, you may encounter a similar error:

> ERROR: Running as root exposes your machine to malware and is unnecessary in a large majority of cases.

For environments that require running the bash script as root, you can start it with:

```sh
./valheim.sh UNSAFE_ROOT_EXECUTION
```

or with the environment variable

```sh
UNSAFE_ROOT_EXECUTION=true ./valheim.sh
```

### There are DLLs that aren't really necessary in the pack

We're aware. If you've got a good reason to delete them (e.g. some are already loaded by the game or by BepInEx) and you want to improve the pack, submit a pull request with the change.

### There's a .NET/mono/Unity DLL missing from the pack

Submit a pull request with the details and we'll get it added.

## SHA-256 File Checkums

Checksums are in the file `checksums.sha256`.

Checksums are sorted alphabetically so they can easily be compared even in simple text editors.
