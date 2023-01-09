# Preferences (plist)

## Disable dark mode for an app

```sh
defaults write BundleIdentifier NSRequiresAquaSystemAppearance -bool yes
```

## Set default meeting time for calendar

```sh
defaults write com.apple.iCal "Default duration in minutes for new event" -int <TIME IN MINUTES>
```

## Reset meeting time to default for calendar

```sh
defaults delete com.apple.iCal "Default duration in minutes for new event"
```

## Restart plist manager

```sh
killall cfprefsd
```

#macos #shell #preferences