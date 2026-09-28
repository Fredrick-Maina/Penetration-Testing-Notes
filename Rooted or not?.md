https://dojo.africahackon.com/challenges link to the challenge

Download the zip file.

file vaultapp.apk 
vaultapp.apk: Android package (APK), with AndroidManifest.xml, with APK Signing Block

it's an apk file

jadx-gui vaultapp.apk

if you don have jadx-gui: install ==> ```bash
sudo apt install jadx

analysing the source code:

package com.example.vaultapp;  
  
import java.io.File;  
  
/* JADX INFO: loaded from: classes.dex */  
public class RootCheck {  
    private static final byte[] ENCODED_FLAG = {40, 81, 88, 27, 13, 14, -16, -65, -26, -88, -61, -8, -102, -37, -120, -81, -77, -94, -23, -84, -71, -113, -115, -117, 54, 122, 99, 36, 109, 122, 88, 91, 9, 30, 43, 39, 101, 62, 15, 22};  
    private static final int SEED = 90;  
  
    private static byte[] deriveKey(int length) {  
        byte[] bArr = new byte[length];  
        for (int i = 0; i < length; i++) {  
            bArr[i] = (byte) (SEED + (i * 7));  
        }  
        return bArr;  
    }  
  
    public static boolean isDeviceRooted() {  
        return new File("/system/bin/su").exists();  
    }  
  
    public static String unlockDebugFlag() {  
        byte[] bArr = ENCODED_FLAG;  
        int length = bArr.length;  
        byte[] bArrDeriveKey = deriveKey(length);  
        byte[] bArr2 = new byte[length];  
        for (int i = 0; i < length; i++) {  
            bArr2[i] = (byte) (bArr[i] ^ bArrDeriveKey[i]);  
        }  
        return new String(bArr2);  
    }  
}

this is everything:

using a simple python script:

encoded = [
    40, 81, 88, 27, 13, 14, -16, -65, -26, -88,
    -61, -8, -102, -37, -120, -81, -77, -94, -23, -84,
    -71, -113, -115, -117, 54, 122, 99, 36, 109, 122,
    88, 91, 9, 30, 43, 39, 101, 62, 15, 22
]

seed = 90

decoded = bytes(
    (x & 0xff) ^ ((seed + i * 7) & 0xff)
    for i, x in enumerate(encoded)
)

print(decoded)
print(decoded.decode())


voila!!!