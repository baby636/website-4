---
layout: docs
title: AppVeyor Enterprise Maintenance Guide
---

<!-- markdownlint-disable MD022 MD032 -->
# AppVeyor Enterprise Maintenance Guide
{:.no_toc}

* Comment to trigger ToC generation
{:toc}
<!-- markdownlint-enable MD022 MD032 -->

## Updating AppVeyor installation

RDP into AppVeyor server and open PowerShell console.

To update AppVeyor Installation PowerShell module (AppVeyor Installer) run the following command:

```posh
iex ((New-Object Net.WebClient).DownloadString('https://www.appveyor.com/downloads/enterprise/install.ps1'))
```

To update AppVeyor installation (Web and Worker roles) to the latest available version run:

```posh
Update-AppVeyor
```


## Backup

[TBD]

* Registry settings
* Databases
* Artifacts

# Troubleshooting and support

During installation AppVeyor uses randomly-generated values for security keys, account passwords and other sensitive values. All these values as well as other installer data such as AppVeyor roles and versions installed can be found under this registry key:

    HKEY_LOCAL_MACHINE\SOFTWARE\Appveyor\Install

When something goes wrong:

* If build real-time log stops working there might be a transient issue with SignalR. Do F5 in browser to restart SignalR connection.
* Restart IIS and/or `Appveyor.Worker` and/or `Appveyor.BuildAgent` services.
* Nothing helps - [report the issue](/support/) to AppVeyor team. While reporting the issue look into these places for possible errors/warning:
    * Web browser's "Developer tools" - for any JavaScript-related errors.
    * `AppVeyor` event log in Event Viewer under `Applications and Services Logs\AppVeyor`. Web, Worker and Build Agent roles write logs there.