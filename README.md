# Boilr
[![Get Boilr on F-Droid](https://github.com/drpout/boilr/raw/master/src/main/img/get_it_on_f-droid.png)](https://f-droid.org/repository/browse/?fdid=mobi.boilr.boilr)  [![Get Boilr on Google Play](https://developer.android.com/images/brand/en_generic_rgb_wo_60.png)](https://play.google.com/store/apps/details?id=mobi.boilr.boilr)  [![Translation status](https://hosted.weblate.org/widgets/boilr/-/svg-badge.svg)](https://hosted.weblate.org/engage/boilr/?utm_source=widget)

Android application which monitors Bitcoin, cryptocurrencies, cryptoassets and derivatives, triggering alarms according to user settings.

![hit alarm creation](https://github.com/drpout/boilr/raw/master/src/main/img/screenshots/hit_creation.png) ![alarm list](https://github.com/drpout/boilr/raw/master/src/main/img/screenshots/alarm_list.png) ![hit alarm firing](https://github.com/drpout/boilr/raw/master/src/main/img/screenshots/hit_firing.png)

Supports 2 alarm types:

* Price Hit - Triggered when price crosses the alarm's upper or lower limit. One limit may be left empty to create an alarm with a single trigger.
* Price Change - Triggered when price changes more than X amount (in currency or percentage) in a specified time frame (e.g. 15 min). It uses a rolling time frame: price is fetched with a given update interval (e.g. 30 s) and compared with the price fetched one time frame ago (e.g. 15 min ago).

Sound and vibration are configurable globally, and individually for each alarm. Lists of exchanges, pairs and alarms are fully searchable, allowing quick setup and configuration. The alarm list behaves as your ticker, where you can reorder your alarms and directly change their limits. Triggered alarms ring, displaying their status, until you turn them off. Just like an alarm clock.

Market data is retrieved directly from the exchanges via Wi-Fi or Mobile Data (if allowed). [libdynticker](https://github.com/drpout/libdynticker) is used to interface with the exchanges. Thus, Boilr supports all [exchanges available on libdynticker](https://github.com/drpout/libdynticker/#supported-exchanges), as all their pairs.

To create alarms Boilr uses [libpricealarm](https://github.com/drpout/libpricealarm).

Other libraries we use: [changeloglib](https://github.com/gabrielemariotti/changeloglib) and [UndoBar](https://github.com/soarcn/UndoBar).

Check Boilr's website to see it in action: http://boilr.mobi Website source-code is available at [boilr-site](https://github.com/drpout/boilr-site).

## Getting help
Bug reports, feature requests and general help questions should be submitted on [Boilr's GitHub issues](https://github.com/drpout/boilr/issues). Try being specific when choosing the right title and label for your issue.

You can browse through a FAQ by checking all [issues labeled as questions](https://github.com/drpout/boilr/issues?q=label%3Aquestion).

## Troubleshooting

Trouble | Solution
------- | --------
Alarm not updating when phone is sleeping. | Set `Settings > Wi-Fi > Advanced > Keep Wi-Fi on during sleep` to `Always`

## Reasons for permissions

Permission | Reason
---------- | ------
Read the contents of your SD card | Used to fetch your custom ringtones.
Disable your screen lock | So you can turn off a ringing alarm without unlocking your device.
Full network access | To fetch data from the exchanges.
View network connections | To know whether you're using Wi-Fi or Mobile Data, allowing Mobile Data restriction. 
Run at startup | To grab your active alarms and start updating them. 
Control vibration | Allows vibration when an alarm is triggered. 
Prevent phone from sleeping | Used to keep showing the alarm triggered activity until you press the turn off button.

## Contributing

### Translating
New translations and reviews are much appreciated. If you have 10 minutes to spare just open [Boilr @ Hosted Weblate](https://hosted.weblate.org/projects/boilr/) and start editing. More info at [CONTRIBUTING.md](/CONTRIBUTING.md).

### Coding
If you know how to program take a look at the [open issues](https://github.com/drpout/boilr/issues). Check for bugs or features you find interesting and feel free to take them into your hands. If you have any doubt just post your questions on the issue's comments. When done, open a pull request. We promise to review it quickly.

If you would like to add more exchanges to Boilr check [libdynticker's contributing guide](https://github.com/drpout/libdynticker/blob/master/CONTRIBUTING.md).

## Building
1. Fill out the [prerequisites for Android Maven Plugin](https://code.google.com/p/maven-android-plugin/wiki/GettingStarted#Prerequisites).
2. Install Android API 21 SDK and Android Support Library. 
3. `mvn install:install-file -DgroupId=android -DartifactId=android -Dversion=5.1_r1 -Dpackaging=jar -Dfile=$ANDROID_HOME/platforms/android-22/android.jar`
4. `mvn install:install-file -DgroupId=com.android.support -DartifactId=support-annotations -Dversion=21.0.0 -Dpackaging=jar -Dfile=$ANDROID_HOME/extras/android/support/annotations/android-support-annotations.jar`
5. Run `mvn validate` to make Maven aware of the plugins used to download and install dependencies which are not in Maven repositories.

For now on you can use:

* `mvn package -P debug` to build an apk in debug mode.
* `mvn package -P release` to build an apk in release mode, which will be optimized, signed and aligned.
* `mvn android:deploy` to install the generated apk in any connected phones or emulators.

Note: `mvn package` with no profile associated builds an unsigned release mode apk, unsuitable for deploy. It is meant for further processing by downstream projects like F-Droid.

## Debuging
On your shell you can use `export ANDROID_LOG_TAGS="ActivityManager:I Boilr:D *:S"` to filter logcat, then run `adb logcat` as usual.

## Importing into Eclipse
If you are no vi or emacs ninja you can use Eclipse to ease your work in Boilr.

1. Install and configure the [ADT plugin](https://developer.android.com/sdk/installing/installing-adt.html).
2. Install [m2e-android](https://rgladwell.github.io/m2e-android).
3. Clone [changeloglib](https://github.com/gabrielemariotti/changeloglib/). Go to `File->Import->Existing Android Code Into Workspace`, import just what's in the `ChangeLogLibrary` directory and name the new project as `ChangeLogLibrary`.
4. Clone [UndoBar](https://github.com/soarcn/UndoBar). Go to `File->Import->Existing Android Code Into Workspace`, import just what's in the `library` directory and name the new project as `UndoBar`.   
5. Go to `File->Import->Existing Projects into Workspace` and select Boilr's git root directory.

Use Eclipse only for writing code. Always compile in the shell using Maven.

Note: we do plan to migrate to a Gradle build system and Android Studio IDE in the near future.

## Versioning
Boilr follows [Semantic Versioning](http://semver.org) with the API being the user-interface.

## License and authorship
Boilr code licensed under [GNU GPL v3](/LICENSE) or later. Copyright belongs to [André Filipe Santos](https://github.com/andrefbsantos), [David Ludovino](https://github.com/dllud) and other [contributors listed on GitHub](https://github.com/drpout/boilr/graphs/contributors), unless otherwise stated.

Concept, design, [icon](src/main/img/icons/ic_boilr.ai) and [artwork](src/main/img) by [Algazarra](http://cargocollective.com/algazarra/index). Icon and artwork dual licensed under [CC-BY-SA 4.0 International](https://creativecommons.org/licenses/by-sa/4.0) or [GPLv3+](/LICENSE). Third-party graphics' authorship and license information in [AUTHORS.md](src/main/img/AUTHORS.md).

Translators:

* Chinese: [Jan Xie](https://github.com/janx) and Song
* Czech: [Jaroslav Lichtblau](https://github.com/svetlemodry) and [Michal Čihař](https://github.com/nijel)
* French: [Tuux](http://www.rtnp.org) and [M for Momo](http://www.rtnp.org)
* German: Luca Rui
* Italian: Francesca Mautone and [Mario Frasca](https://hosted.weblate.org/user/mfrasca)
* Polish: [Michal Pleban](https://pl.linkedin.com/in/michalpleban)
* Spanish: Mariona Martinez

## Donations and tips
In case you wanna pay us a beer ;)

* BTC: 1PHuSWfuAwR6oz9qV93rTdMVozfM85Qqxx
* XMR: 43KcTwXw5D43YRE8MSG4D7X3S2kjU6ehBABucyKAVNYnKbNxpGWZ8zGbEhCq79N4ZGDtefU5w4AGoeR6eNB5yMbEPhAw3FT
* DOGE: DSSJyAtJy9xokkbfTUQ5NQov8M1WQ8FaYg
* NXT: NXT-PMQL-5RXJ-QE46-2L4SQ
