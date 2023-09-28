# Make a disk image auto open

```sh
dmg_vol_name="name"

# Final DMG that you will be shipping
dmg_path="/path/to/final/dmg/$dmg_vol_name.dmg"  

# Temporary DMG that will be worked on and then deleted
dmg_build_path="/path/to/temp/dmg/$dmg_vol_name.dmg"    

# Should match the mounted name of your DMG
dmg_volume="/Volumes/$dmg_vol_name"                         

hdiutil attach -owners on "dmg_build_path" -shadow

# This actually makes the change to auto open the DMG in finder
bless "$dmg_volume/" --openfolder "$dmg_volume"  

hdiutil detach "$dmg_volume"
hdiutil convert -format UDZO -o "$dmg_path" "$dmg_build_path" -shadow
```

#shell #dmg