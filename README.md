# Wago App Flatpak

This is the Flatpak for [Wago App](https://addons.wago.io/app)

### File Access

If you store games in a non-standard location, you'll need to enable access to that location:

	flatpak override --filesystem=/path/to/game io.wago.WagoApp

### Tray

To get a working tray icon on GNOME, install the [appindicator-support](https://extensions.gnome.org/extension/615/appindicator-support/) extension.


## Development

> This whole section needs to be removed before we publish

Missing/recommended:

- [ ] get a confirmation from Wago team if the metadata looks right
- [ ] need to add an exception (see below)
- [ ] Wago team needs to add an app verification (see below)
- [ ] icons should be embedded in the AppImage
- [ ] icons missing 48x48
- [ ] desktop file keyword changes should be added to the AppImage directly
- [ ] which Wago team members wants/needs access/ownership of the GitHub repo under the flathub organization

### Exception

The flatpak needs access to `$HOME/.var/app` in order to access other programs like game launchers.  
This is not permitted for flathub flatpaks unless explicitly asked for it, so we'll have to deal with that before the PR (once created) can be merged.

This is done by forking the [flatpak-builder-link](https://github.com/flathub-infra/flatpak-builder-lint) repo and modifying/appending the following to `flatpak_builder_lint/staticfiles/exceptions.json`:

```json
"io.wago.WagoApp": {
  "finish-args-flatpak-appdata-folder-access": "This program needs to write files as game mods in various launchers."
}
```

### App verification

To get this flatpak marked as "verified" (i.e. official) the domain it is submitted with (in this case `wago.io`) needs to host a ["well-known"](https://en.wikipedia.org/wiki/Well-known_URI) file, i.e. at `https://wago.io/.well-known/org.flathub.VerifiedApps.txt`, with the following contents:

```
# io.wago.WagoApp
<APP UUID>
```

This needs to happen after it's been submitted.

Docs: <https://docs.flathub.org/docs/for-app-authors/verification>
