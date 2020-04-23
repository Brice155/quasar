---
title: Icon Genie CLI Command List
desc: Command list for Icon Genie CLI.
---

Familiarize yourself with the list of Icon Genie CLI available commands inside a Quasar project folder:

```bash
$ icongenie

  Example usage
    $ icongenie <command> <options>

  Help for a command
    $ icongenie <command> --help
    $ icongenie <command> -h

  Options
    --version, -v Print Quasar Icon Genie CLI version

  Commands
    generate, g   Generate App icons & splashscreens
    verify, v     Verifies your Quasar App's icons &
                    splashscreens
    profile, p    Creates Icon Genie profile files
    help, h       Displays this message
```

See help for any command:

```bash
$ icongenie [command name] --help
```

## Generate

The `generate` command is used for generating App icons and splashscreens. It's at the heart of Icon Genie as it does the heavy lifting.

Please take a look below at the usage and some examples. The most important parameter that you will want to notice is the `--icon` (or short `-i`) one, which takes a transparent png (with min size 64x64, but highly recommending to go over 1024x1024px) as input for your App's icons and splashscreens.

When it comes to splashscreens, you might also want to combine it with the `--background` (or short `-b`) if you want your icon to be placed on top of a background.

You might also want to take note of the `--profile` (or short `-p`) parameter which can run one or more Icon Genie [profile files](/icongenie/profile-files).

```bash
$ icongenie generate -h

  Description
    Generate App icons & splashscreens

  Usage
    $ icongenie generate [options]

    # generate icons for all installed Quasar modes
    $ icongenie generate -i /path/to/icon.png
    $ icongenie g -i /path/to/icon.png

    # generate for (as example) PWA mode only
    $ icongenie generate -m pwa --icon /path/to/icon.png

    # generate for (as example) Cordova & Capacitor mode only
    $ icongenie g -m cordova,capacitor -i
         /path/to/icon.png -b /path/to/background.png

    # generate by using a profile file
    $ icongenie generate -p ./icongenie-profile.json

    # generate by using batch of profile files
    $ icongenie generate -p ./folder-containing-profile-files

  Options
    --icon, -i            Required;
                          Path to source file for icon; must be:
                            - a .png file
                            - min resolution: 64x64 px (the higher the better!!)
                            - with transparency
                          Path can be absolute, or relative to the root of the
                            Quasar project folder
                          Recommended min size: 1024x1024 px

    --background, -b      Path to optional background source file (for splashscreens);
                          must be:
                            - a .png file
                            - min resolution: 128x128 px (the higher the better!!)
                            - transparency is optional
                          Path can be absolute, or relative to the root of the
                            Quasar project folder
                          Recommended min size: 1024x1024 px

    --mode, -m            For which Quasar mode(s) to generate the assets;
                          Default: all
                            [all|spa|pwa|ssr|bex|cordova|capacitor|electron]
                          Multiple can be specified, separated by ",":
                            spa,cordova

    --filter, -f          Filter the available generators; when used, it can
                          generate only one type of asset instead of all
                            [png|ico|icns|splashscreen|svg]

    --quality             Quality of the files [1 - 12] (default: 5)
                            - higher quality --> bigger filesize, slower
                            - lower quality  --> smaller filesize, faster

    --theme-color         Theme color to use for all generators requiring a color;
                          It gets overriden if any generator color is also specified;
                          The color must be in hex format (NOT hexa) without the leading
                          '#' character. Transparency not allowed.
                          Examples: 1976D2, eee

    --svg-color           Color to use for the generated monochrome svgs
                          Default (if no theme-color is specified): 1976D2
                          The color must be in hex format (NOT hexa) without the leading
                          '#' character. Transparency not allowed.
                          Examples: 1976D2, eee

    --png-color           Background color to use for the png generator, when
                          "background: true" in the asset definition (like for
                          the cordova/capacitor iOS icons);
                          Default (if no theme-color is specified): fff
                          The color must be in hex format (NOT hexa) without the leading
                          '#' character. Transparency not allowed.
                          Examples: 1976D2, eee

    --splashscreen-color  Background color to use for the splashscreen generator;
                          Default (if no theme-color is specified): fff
                          The color must be in hex format (NOT hexa) without the leading
                          '#' character. Transparency not allowed.
                          Examples: 1976D2, eee

    --splashscreen-icon-ratio  Ratio of icon size in respect to the width or height
                               (whichever is smaller) of the resulting splashscreen;
                               Represents percentages; Valid values: 0 - 100
                               If 0 then it doesn't adds any icon of top of background
                               Default: 40

    --profile, -p         Use JSON profile file(s):
                            - path to folder (absolute or relative to current folder)
                              that contains JSON profile files (icongenie-*.json)
                            - path to a single *.json profile file (absolute or relative
                              to current folder)
                          Structure of a JSON profile file:
                            {
                              "params": {
                                "include": [ ... ], /* optional */
                                ...
                              },
                              "assets": [ /* list of custom assets */ ]
                            }

    --help, -h            Displays this message
```

## Verify

The `verify` command is useful to verify that you have all your necessary app icons and splashscreens in the right place and that each file has the right resolution in pixels.

```bash
$ icongenie -h

  Description
    Verifies your Quasar App's icons and splashscreens
    for all installed modes.

  Usage
    $ icongenie verify [options]

    # verify all Quasar modes
    $ icongenie verify

    # verify specific mode
    $ icongenie verify -m spa

    # verify with specific filter
    $ icongenie verify -f ico

    # verify by using a profile file
    $ icongenie verify -p ./icongenie-profile.json

    # verify by using batch of profile files
    $ icongenie verify -p ./folder-containing-profile-files

  Options
    --mode, -m      For which Quasar mode(s) to verify the assets;
                    Default: all
                      [all|spa|pwa|ssr|bex|cordova|capacitor|electron]
                    Multiple can be specified, separated by ",":
                      spa,cordova,capacitor

    --filter, -f    Filter the available generators; when used, it verifies
                    only one type of asset instead of all
                      [png|ico|icns|splashscreen|svg]

    --profile       Use JSON profile file(s) to extract the asset list to verify:
                      - path to folder (absolute or relative to current folder)
                        that contains JSON profile files (icongenie-*.json)
                      - path to a single *.json profile file (absolute or relative
                        to current folder)
                    Structure of a JSON profile file:
                      {
                        "params": {
                          "include": [ ... ], /* optional */
                          ...
                        },
                        "assets": [ /* list of custom assets */ ]
                      }

    --help, -h      Displays this message
```

## Profile

Icon Genie also supports profile files. These files are in JSON format and tell Icon Genie how to generate the images and which ones. So the `profile` command is a helper to scaffold such types of files. They are very useful for automation, if needed.

The generic form of a JSON profile file is:

```json
{
  "params": { },
  "assets": [ ]
}
```

You can also generate multiple profile files (with different params/settings). For more information please head on to the [Profile files](/icongenie/profile-files) page.

```bash
$ icongenie profile -h

  Description
    Helper command to easily bootstrap Icon Genie profile files.

  Usage
    $ icongenie profile -o <filename> [options]

    # supplying params list
    $ icongenie profile -o <filename> --include pwa,spa --quality 7

    # supplying assets based on Icon Genie's internal list
    $ icongenie profile -o <filename> --assets spa,bex

  Options
    --output, -o          Name of the new Icon Genie profile file

    --assets, -a          Prefill the assets Array with Icon Genie's
                          internal list, based on the modes that you indicate;
                            [all|spa|pwa|ssr|bex|cordova|capacitor|electron]
                          Multiple can be specified, separated by ",":
                            spa,cordova

    --icon, -i            Path to source file for icons; must be:
                            - a .png file
                            - min resolution: 64x64 px (the higher the better!!)
                            - with transparency
                          Path can be absolute, or relative to the root of the
                            Quasar project folder
                          Recommended min size: 1024x1024 px

    --background, -b      Path to optional background source file (for splashscreens);
                          must be:
                            - a .png file
                            - min resolution: 128x128 px (the higher the better!!)
                            - transparency is optional
                          Path can be absolute, or relative to the root of the
                            Quasar project folder
                          Recommended min size: 1024x1024 px

    --include             Prefill the params.include property;
                            [all|spa|pwa|ssr|bex|cordova|capacitor|electron]
                          Multiple can be specified, separated by ",":
                            spa,cordova

    --filter, -f          Prefill the params.filter property;
                            [png|ico|icns|splashscreen|svg]

    --quality             Prefill in the params.quality property;
                          Quality of the files [1 - 12] (default: 5)
                            - higher quality --> bigger filesize, slower
                            - lower quality  --> smaller filesize, faster

    --theme-color         Prefill the params.themeColor property;
                          Theme color to use for all generators requiring a color;
                          It gets overriden if any generator color is also specified;
                          The color must be in hex format (NOT hexa) without the leading
                          '#' character. Transparency not allowed.
                          Examples: 1976D2, eee

    --svg-color           Prefill the params.svgColor property;
                          Color to use for the generated monochrome svgs
                          Default (if no theme-color is specified): 1976D2
                          The color must be in hex format (NOT hexa) without the leading
                          '#' character. Transparency not allowed.
                          Examples: 1976D2, eee

    --png-color           Prefill the params.pngColor property;
                          Background color to use for the png generator, when
                          "background: true" in the asset definition (like for
                          the cordova/capacitor iOS icons);
                          Default (if no theme-color is specified): fff
                          The color must be in hex format (NOT hexa) without the leading
                          '#' character. Transparency not allowed.
                          Examples: 1976D2, eee

    --splashscreen-color  Prefill the params.splashscreenColor property;
                          Background color to use for the splashscreen generator;
                          Default (if no theme-color is specified): fff
                          The color must be in hex format (NOT hexa) without the leading
                          '#' character. Transparency not allowed.
                          Examples: 1976D2, eee

    --splashscreen-icon-ratio  Prefill the params.splashscreenIconRatio property;
                               Ratio of icon size in respect to the width or height
                               (whichever is smaller) of the resulting splashscreen;
                               Represents percentages; Valid values: 0 - 100
                               If 0 then it doesn't adds any icon of top of background
                               Default: 40
```