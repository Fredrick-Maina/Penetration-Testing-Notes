file-name.apk
     ↓
JADX → source code
     ↓
apktool → Manifest + Smali + resources
     ↓
Search for → passwords / secrets / API keys / URLs / crypto
     ↓
Run app → observe behavior
     ↓
ADB + Frida → investigate runtime behavior


jadx-gui vaultapp.apk
apktool d vaultapp.apk -o vaultapp

adb install vaultapp.apk
adb logcat
