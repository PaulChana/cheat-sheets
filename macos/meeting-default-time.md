# Set default meeting time for calendar

```sh
defaults write com.apple.iCal "Default duration in minutes for new event" -int <TIME IN MINUTES>
```

# Reset meeting time to default for calendar

```sh
defaults delete com.apple.iCal "Default duration in minutes for new event"
```

#macos #shell #preferences 