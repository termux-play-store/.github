# Termux on Google Play
This page contains information about the [Termux build on Google Play](https://play.google.com/store/apps/details?id=com.termux).

## Background
Android apps specify a [targetSdkVersion](https://developer.android.com/guide/topics/manifest/uses-sdk-element#target) property, to indicate which version of Android they are compatible with. This is for backward compatibility, as if the `targetSdkVersion` of an app specifies "Android 11", then the Android system will effectively act as if the system is running that version, allowing old behaviour, even if the system is actually running a newer Android version such as Android 14.

Almost every Android version imposes new major restrictions when it comes to security requirements, and specifically the Android 10 version update was dramatic for Termux usage, as it disallowed executing downloaded files directly.

The Termux app avoided that by using a `targetSdkVersion` of Android 9, declaring that it was not compatible with the Android 10 requirements. This meant that, due to [Google Play's API level requirements](https://developer.android.com/google/play/requirements/target-sdk), Termux was not able to be updated on Google Play starting in 2020, and new devices were not allowed to install Termux from Google Play.

This was unfortunate, as it meant that a lot of people around the world (many using Termux for real work or educational purposes, not having access to any computers and not being able to install apps from outside of Google Play due to having their phones locked down by carries) could either not install Termux at all on their new devices, or had to use old and insecure app versions on old devices.

Recently, at 2024-06-07, Termux was updated on Google Play with changes to bump the `targetSdkVersion` to latest Android, with:
- Changes to work with the updated `targetSdkVersion` required by Google Play.
- Changes to work without the [sharedUserId](https://developer.android.com/guide/topics/manifest/manifest-element#uid) manifest entry, which was not allowed by the Google Play review.
- Changes to work with less permissions, as the initial Google Play review did not approve the usage of multiple permissions.
  - Some of these (but not all) might be possible to add back in the future, if Google Play reviwers can be convinced that they are important enough for app functionality.

As the F-Droid build of the Termux app and packages is not yet compatible with the updated requirements - and before passing Google Play review it wasn't clear exactly which changes was necessary - it was done from a different code base containing changes compared to the F-Droid build:
- https://github.com/termux is the source code used in the F-Droid build of Termux.
- https://github.com/termux-play-store is the source code for the Google Play build of Termux.

This split is a temporary one as things stabilises and details are worked out.

## Current status for users
Most users who can install from [F-Droid](https://f-droid.org), should [install Termux from F-Droid](https://f-droid.org/en/packages/com.termux/) for now until the Termux build on Google Play has been stabilised more. Google Play will for now consider the Google Play build to be newer and prompt to update - this will be resolved by a Termux F-Droid update shortly, until then ignore the update prompt and/or disable automatic updates for the Google Play Termux app.

If you as a user want to help out testing or experimenting with the [Termux build on Google Play](https://play.google.com/store/apps/details?id=com.termux):
- Things can be rough - while most normal use cases should work, be ready for some issues and missing functionality.
  - Check out [Updates](#updates) below for updates, and check out and report issues at https://github.com/termux-play-store/termux-issues/issues
- Report issues at [termux-play-store/termux-issues](https://github.com/termux-play-store/termux-issues/issues/new/choose) and nowhere else, as the issues encountered can very likely be specific to the Google Play changes.
- The `Termux:API` app is not yet available (but support for the following tools are now built in: `termux-clipboard-*`, `termux-download`, `termux-saf-*`,  `termux-share`, `termux-storage-get`, `termux-usb`, `termux-vibrate` and `termux-volume`).
- The `Termux:Tasker` and `Termux:Float` apps are not yet available.
- Android version 11 is currently required, and only 64-bit devices are currently supported.
- External, non-Termux app can not yet run Termux commands (the `RUN_COMMAND` permission).
- Are you finding something that is worth pointing out here? [Create an issue about it](https://github.com/termux-play-store/termux-issues/issues/new/choose)

## Current status for developers
If you are a developer wanting to help out with contributing to Termux on Google Play:
- See [termux-play-store/termux-apps](https://github.com/termux-play-store/termux-apps) for the Android apps themselves.
- See [termux-play-store/termux-packages](https://github.com/termux-play-store/termux-packages) for packages.
- Create issues or pull requests on the above repositories, or reach out to [#termux-google-play on Matrix](https://matrix.to/#/#termux-google-play:matrix.org) to discuss!

## Updates
- `2024-09-17`: [Termux User Repository (TUR)](https://github.com/termux-user-repository/tur) is now available: `pkg install tur-repo` (after updating to latest packages with `pkg up`).
- `2024-09-16`: Usage of `/proc/self/exe` (which does not work under `termux-exec` when targetSdk is bumped) was fixed in the `zellij` package.
- `2024-09-07`: Usage of `/proc/self/exe` (which does not work under `termux-exec` when targetSdk is bumped) was fixed in the `vtm` package.
- `2024-08-29`: Version `2024.08.29` of Termux on Google Play was released, adding support for certain Termux:API tools which are now built in and work without installing Termux:API: `termux-audio-info`, `termux-battery-status`,  `termux-dialog`, `termux-keystore`, `termux-toast`.
- `2024-08-27`: Usage of `/proc/self/exe` (which does not work under `termux-exec` when targetSdk is bumped) was fixed in the `lua-language-server` package.
- `2024-07-25`: Problems with `go` packages (such as `golang`, `elvish` and `chezmoi`) was fixed.
- `2024-07-15`: Version `1.4` of the `termux-exec` package was released, fixing `system(3)` and `popen(3)` not working, shown as permission denied errors when trying to execute files using certaim programs.
- `2024-07-07`: Version `2024.07.07` of Termux on Google Play was released, fixing issues with `termux-url-opener` and `termux-file-editor`, as well as adding support for certain Termux:API tools which are now built in and work without installing Termux:API (which is not yet available on Google Play): `termux-clipboard-*`, `termux-download`, `termux-saf-*`,  `termux-share`, `termux-storage-get`, `termux-usb`, `termux-vibrate` and `termux-volume`.
- `2024-06-27`: Version `2024.06.27` of Termux on Google Play was released, restoring compatibility with a lot of X11 packages and fixing some issues.
- `2024-06-23`: Version `0.129` of Termux on Google Play was released. This version fixes GPG errors on certain devices, causing incorrect messages about "the repository .. is not signed, as well as KernelSU compatibility and configuring the extra keyboard keys using `termux.properties`.
  - If you are seeing the `the repository .. is not signed` error message from an old installation, either uninstall and install again or run `apt --allow-insecure-repositories update` and `apt upgrade` once.
- `2024-06-23`: Version `0.128` of Termux on Google Play was released. This version grants read/write access to shared storage using the `MANAGE_EXTERNAL_STORAGE` permission.
  - Run `termux-setup-storage` to get this read/write access.
- `2024-06-22`: The F-Droid build was updated with a version code bump, so Google Play will not consider its version of Termux to be newer than the F-Droid one, and will stop prompting for updating away from F-Droid.
- `2024-06-18`: Root packages (`pkg install root-repo`) were added back.
- `2024-06-16`: Version `0.127` of Termux on Google Play was released. This version adds back the Termux session notification on Android 13+ devices.
- `2024-06-14`: Version `0.126` of Termux on Google Play was released. This version fixes `proot` usage.
- `2024-06-12`: Version `0.125` of Termux on Google Play was released. This version fixes setting up access to shared storage with `termux-setup-storage`.
- `2024-06-11`: Version `0.124` of Termux on Google Play was released. This version fixes problems with updating styles.
- `2024-06-10`: Version `0.123` of Termux on Google Play was released. This version fixes a crash on `termux-setup-storage`.
- `2024-06-09`: Version `0.122` of Termux on Google Play was released, fixing some crashes and instabilities, as well as bringing full-screen support.
- `2024-06-07`: Version `0.120` of Termux on Google Play was released, the initial version being back on the Google Play.
