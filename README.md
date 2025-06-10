# Wago App Flatpak

This is the Flatpak for [Wago App](https://addons.wago.io/app)

### File Access

If you store games in a non-standard location, you'll need to enable access to that location:

	flatpak override --filesystem=/path/to/game io.wago.WagoApp

### Tray

To get a working tray icon on GNOME, install the [appindicator-support](https://extensions.gnome.org/extension/615/appindicator-support/) extension.
