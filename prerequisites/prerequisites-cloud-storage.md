# Cloud Storage

## Provider

Cloudbox can be setup to use any cloud storage provider that [Rclone](https://rclone.org/) supports. However, Google Drive via [G-Suite Business](https://gsuite.google.com/pricing.html) is the popular choice among users.

It is **strongly** advised that you do NOT use an educational GSuite account or any GSuite account you may buy on the secondary market \[eBay and the like\].

## Basics

Out of the box, Cloudbox stores the media unencrypted in cloud storage utilizing an Rclone VFS mount to access it. If you prefer your data is stored encrypted, you will need to do some tweaking to the Rclone config.

Media will be stored in `Movies` and `TV` folders, all within a `Media` folder in root \(i.e. `/Media`\). [\[1\]](prerequisites-cloud-storage.md#note1)

## Setup <a id="note1ref"></a>

```text
Media
├── Movies
├── Music
└── TV
```

* Example from Google Drive:

  ![](https://i.imgur.com/kwnNjni.png)

If you have media in other folders, you can simply move them into these folders via the Cloud Storage Provider's web site.

Note 1: For Google Drive, you can use the [Shift-Z trick](https://www.labnol.org/internet/add-files-multiple-drive-folders/28715/) to "symlink" folders here.

Note 2: All the paths/folders mentioned here, and elsewhere, are **CASE SENSITIVE** \(see [Cloudbox Paths](../basics/basics-cloudbox-paths.md)\).

 [1](prerequisites-cloud-storage.md#note1ref) If you would like to customize your Plex libraries beyond what is listed above, see [Customizing Plex Libraries](../advanced-configuration/customizing-plex-libraries-1.md).

