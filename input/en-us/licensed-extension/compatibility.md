---
Order: 30
xref: licensed-extension-compatibility
Title: Compatibility
Description: Compatibility Information for Chocolatey Licensed Extension
---

## Summary

This covers the compatibility information for the Chocolatey Licensed Extension and associated Chocolatey CLI and other product versions.
The Chocolatey Licensed Extension is designed to work with a certain corresponding version range of the Chocolatey CLI package.
Using incompatible versions of Chocolatey CLI with the Chocolatey Licensed Extension may result in undesirable behaviour.

This page serves as a reference for troubleshooting and resolving issues that may arise from having incompatible versions of the Chocolatey Licensed Extension installed.

<?! Include "../../shared/chocolatey-component-dependencies.txt" /?>

## Troubleshooting

The above table lists the compatible product versions with the most recent version of the Chocolatey Licensed Extension.
If you are working with an earlier version of Chocolatey Licensed Extension, please consult the [Chocolatey Licensed Extension](xref:licensed-extension-release-notes) release notes to determine the recommended version(s) of Chocolatey CLI for your version of the Chocolatey Licensed Extension.

> :choco-warning: **WARNING**
>
> Chocolatey CLI v1.0.1 and up may continue to work for versions of the Chocolatey Licensed Extension older than v4.0.0, but these configurations are not supported for use in a production environment.
> We recommend all customers update to new product versions, if/when they are able to do so, in order to get the latest features and fixes.

In Chocolatey CLI versions v1.0.1 and newer, you may receive error messages regarding the currently installed Chocolatey Licensed Extension, but these will not prevent Chocolatey from functioning.
In order to resolve these messages, simply use `choco install` or `choco upgrade` to install, upgrade, or downgrade the Chocolatey CLI or Chocolatey Licensed Extension packages as appropriate to ensure you are using compatible versions of Chocolatey CLI and the Chocolatey Licensed Extension.

In Chocolatey CLI versions prior to v1.0.1, you may receive error messages similar to the following if there are incompatible versions of the Chocolatey Licensed Extension installed:

```error
The registered delegate for type IEnumerable<ICommand> threw an exception.
```

To resolve these errors, you will need to rename or move the Chocolatey Licensed Extension folder on your system in order to restore Chocolatey functionality.
From a PowerShell console, you can run the following command to back up your Chocolatey Licensed Extension and get basic Chocolatey CLI functionality back:

```powershell
Rename-Item -Path "$env:ChocolateyInstall\extensions\chocolatey" -NewName "chocolatey.old"
```

Once that's done, use `choco install` or `choco upgrade` to install, upgrade, or downgrade the Chocolatey CLI or Chocolatey Licensed Extension packages as appropriate to ensure you are using compatible versions of Chocolatey CLI and the Chocolatey Licensed Extension.
For example, the following command can be used to upgrade the Chocolatey Licensed Extension package to the latest version:

```powershell
choco upgrade chocolatey.extension -y
```

Add the `--version` parameter with the appropriate version if you need to install a specific version of the extension, possibly with the `--allow-downgrade` parameter if you are rolling back to an earlier version.

If you needed to back-up the existing Chocolatey Licensed Extension version in order to install the newer version, the following command can be used to remove the backed-up files after you have confirmed that the above steps have resolved the issue:

```powershell
Remove-Item -Path "$env:ChocolateyInstall\extensions\chocolatey.old" -Recurse -Force
```

## Compatibility Warnings

As of Chocolatey CLI v1.1.0, Chocolatey will notify you with a warning if it detects that the version of the Chocolatey Licensed Extension is not supported by the current version of Chocolatey CLI.
At runtime, with a potentially incompatible version of Chocolatey Licensed Extension installed, you will see a warning that looks like this:

```code
WARNING!

You are running a version of Chocolatey that may not be compatible with
the currently installed version of the chocolatey.extension package.
Running Chocolatey with the current version of the chocolatey.extension
package is an unsupported configuration.

See https://ch0.co/compatibility for more information.
If you are in the process of modifying the chocolatey.extension package,
you can ignore this warning.

Additionally, you can ignore these warnings by either setting the
DisableCompatibilityChecks feature:

choco feature enable --name=""'disableCompatibilityChecks'""

Or by passing the --skip-compatibility-checks option when executing a
command.
```

As the warning text notes, this feature can be disabled in one of two ways.
When running each Chocolatey CLI command, you can append the `--skip-compatibility-checks` flag, for example:

```powershell
choco list --local-only --skip-compatibility-checks
```

Alternatively, the compatibility checks can be persistently disabled by enabling the `disableCompatibilityChecks` feature:

```powershell
choco feature enable --name=""'disableCompatibilityChecks'""
```
