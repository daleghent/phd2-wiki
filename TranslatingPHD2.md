# Translating the PHD2 User Interface

Translating PHD2 into different languages is a simple process.

First you will need a translation editor. [Poedit](http://poedit.net/) is an excellent free tool, and there are [several other choices](https://www.google.com/webhp?q=gettext+translations+editor) available too.

## Starting a new translation

To translate PHD2 into a new language:

  1. Download the messages template file from the phd2 source repository: [messages.pot](https://raw.githubusercontent.com/OpenPHDGuiding/phd2/master/locale/messages.pot).
  1. In Poedit, select "Start a new translation", and open the `messages.pot` file you just downloaded.
  1. Save your work as `messages.po`.

## Updating an existing translation

  1. Get the `messages.po` file for your language from the phd2 source repository in the [locale folder](https://github.com/OpenPHDGuiding/phd2/tree/master/locale). Browse to the language sub-folder for your language and click on `messages.po`. Use the Raw button on the top right side of the page to save `messages.po` to your computer.
  1. Open the `messages.po` file in Poedit

## Viewing the translation in PHD2

When you save `messages.po`, Poedit will create `messages.mo` in the same folder. Copy `messages.mo` to your phd2 install folder

```
    <PHD2_Install_Folder>/locale/<YOUR_LANGUAGE_ABBREV>/messages.mo
```

Then, restart phd2 to see the updated translation.

## Publishing the translation

Email the `messages.po` file to `andy.galasso@gmail.com`, or post a message on the [google group](https://groups.google.com/forum/?fromgroups=#!forum/open-phd-guiding) with `messages.po` as an attachment. We will commit the file to the PHD2 source repository, and the updated translation will become available in the next [development build](http://openphdguiding.org/snapshots.html) of PHD2.

---

# Translating the PHD2 User Manual

The PHD2 User Manual is available from the Help menu in PHD2. The User Manual is also rendered as a PDF file, and as HTML pages on the PHD2 web site.  All three of these formats are derived (generated) from a collection of HTML files and images in the the [PHD2 github code repository](/OpenPHDGuiding/phd2).

## Starting a new User Manual translation

Start by downloading the English user manual files to your PC. The English files are in the [help folder](/OpenPHDGuiding/phd2/tree/master/help) of the PHD2 source code repository.  There are various ways to get the help files onto your PC.  Probably the easiest way is to download the full github repo source tree - [Download ZIP](/OpenPHDGuiding/phd2/archive/master.zip), then extract just the help folder from the ZIP file.

Once you have a copy of the help files, you can make the necessary modifications to the html files using a text editor. .png images can be replaced with versions more suitable to the translation language.

There are two configuration files required for the help generator
 - PHD2GuideHelp.hhp is the main configuration file. Be sure to update the list of html files if you add, remove, or rename any of the files.
 - PHD2GuideHelp.hhc defines the Table of Contents. Edit this file as necessary to define the Table of Contents.

Help Files Format details: [wxHTML](https://docs.wxwidgets.org/trunk/overview_html.html)

Once the translation is ready, zip the help folder and send it to the PHD2 developers as described [above](#publishing-the-translation).

## Updating an existing User Manual translation

User Manual translations are located in the PHD2 repository under the locale/<language_abbreviation>/help folder. For example, the French User manual is at [locale/fr_FR/help](/OpenPHDGuiding/phd2/tree/master/locale/fr_FR/help)

To update existing User Manual help files, you can download the PHD2 repository [ZIP](/OpenPHDGuiding/phd2/archive/master.zip), make the modifications, then send the updated files [to the developers](#publishing-the-translation). Or, if you are familiar with github, you can make changes directly in the github UI, or you can [fork the repository](https://docs.github.com/en/github/getting-started-with-github/fork-a-repo) and send a [Pull Request](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests).

---


## Notes for developers ##

If you make a change that affects translatable strings (strings added, removed, or modified), please run `build/locales_update.sh` to update the `messages.po` files for translators.

After receiving an updated `messages.po` file from translators, run `build/locales_compile.sh` to update the `messages.mo` files.