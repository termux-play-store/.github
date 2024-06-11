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
  - Some of these might be possible to add back in the future, if Google Play reviwers can be convinced that they are important enough for app functionality.

As the main Termux app and packages is not yet compatible with the updated requirements - and before passing Google Play review it wasn't clear exactly which changes was necessary - it was done from a different code base containing changes compared to the F-Droid build:
- https://github.com/termux is the source code used in the F-Droid build of Termux.
- https://github.com/termux-play-store is the source code for the Google Play build of Termux.

This split is a temporary one as things stabilises and details are worked out.

## Current status for users
Most users who can install from [F-Droid](https://f-droid.org), should [install Termux from F-Droid](https://f-droid.org/en/packages/com.termux/) for now until the Termux build on Google Play has been stabilised more. Google Play will for now consider the Google Play build to be newer and prompt to update - this will be resolved by a Termux F-Droid update shortly, until then ignore the update prompt and/or disable automatic updates for the Google Play Termux app.

If you as a user want to help out testing or experimenting with the [Termux build on Google Play](https://play.google.com/store/apps/details?id=com.termux):
- Things can be rough - while most normal use cases should work, be ready for some issues and missing functionality.
  - Check out [Updates](#updates) below for updates.
- Report issues at [termux-play-store/termux-issues](https://github.com/termux-play-store/termux-issues/issues/new/choose) and nowhere else, as the issues encountered can very likely be specific to the Google Play changes.
- The X11 graphical system packages are not yet available, nor root functionality.
- [proot](https://wiki.termux.com/wiki/PRoot) does not yet work.
- External storage is not yet accessible.
- The `Termux:Api`, `Termux:Tasker` and `Termux:Float` apps are not yet available.
- Android version 11 is currently required, and only 64-bit devices are currently supported.
- External, non-Termux app can not yet run Termux commands (the `RUN_COMMAND` permission).
- Are you finding something that is worth pointing out here? [Create an issue about it](https://github.com/termux-play-store/termux-issues/issues/new/choose)

## Current status for developers
If you are a developer wanting to help out with contributing to Termux on Google Play:
- See [termux-play-store/termux-apps](https://github.com/termux-play-store/termux-apps) for the Android apps themselves.
- See [termux-play-store/termux-packages](https://github.com/termux-play-store/termux-packages) for packages.
- Create issues or pull requests on the above repositories, or reach out to [#termux-google-play on Matrix](https://matrix.to/#/#termux-google-play:matrix.org) to discuss!

## Updates
- `2024-06-XX` (shortly): The F-Droid build will be updated with a version code bump, so Google Play will not consider its version of Termux to be newer than the F-Droid one, and avoid prompting for updating away from F-Droid.
- `2024-06-12`: Version `0.125` of Termux on Google Play was released, setting up access to shared storage with `termux-setup-storage`.
- `2024-06-11`: Version `0.124` of Termux on Google Play was released, fixing problems with updating styles.
- `2024-06-10`: Version `0.123` of Termux on Google Play was released, fixing a crash on `termux-setup-storage`.
- `2024-06-09`: Version `0.122` of Termux on Google Play was released, fixing some crashes and instabilities, as well as bringing full-screen support.
- `2024-06-07`: Version `0.120` of Termux on Google Play was released, the initial version being back on the Google Play.

