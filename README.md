# VRChat SDK Linux patch

## Warning: By modifying the SDK you are violating the VRChat TOS. Do it at your own risk!

A very primitive patch to add Linux support to VRChat SDK
Basically everything was working, but one line which interacted with shell32.dll was broken.

Currently only works for avatar SDK, the world SDK needs further fixes. 

1. Make a backup of your SDK
2. cd into the GUIDPatch folder
3. run ./patch.sh
4. Go to VRChat Control Panel in unity
5. Go to settings
6. Select the steamapps folder location
7. profit.

### Creating DLL mods

The entire DLL patch is:

VRCSDK3A-Editor.dll > VRC.SDK3.Builder > ExportAndTestAvatarBlueprint:11

\---
```cs
string text = VRC_SdkBuilder.GetKnownFolderPath(VRC_SdkBuilder.LocalLowGUID) + "/VRChat/vrchat/Avatars/";
```

+++
```cs
string text = EditorPrefs.GetString("VRC_steamappsPath") + "/compatdata/438100/pfx/drive_c/users/steamuser/AppData/LocalLow/VRChat/VRChat/Avatars/";
```

Edit the file in dnSpy and to generate the patch use xdelta3 like this

`xdelta3 -e -s ORIGINAL_DLL PATCHED_DLL PATCH_FILE`
