# Safe Opener 2 – picoCTF 2023 Writeup

<img width="886" height="494" alt="image" src="https://github.com/user-attachments/assets/75667028-4245-4686-9a1b-a26ed36dd31a" />

---

## Challenge Description

The challenge provides us with:

- A compiled Java file: `SafeOpener.class`
- A hint suggesting to "Download and try to decompile the file"

The scenario states that the author forgot the key to their safe, but the file is supposed to help retrieve the lost key.

---

## Solution

### Step 1: Decompiling the Java Class File

Java `.class` files are compiled bytecode that can be decompiled back to readable source code. I used **JD-GUI** (Java Decompiler) to open and analyze the file.


# Opening the file with JD-GUI
jd-gui SafeOpener.class
### Step 2: Analyzing the Decompiled Source Code
After decompiling, the following Java source code was revealed:

package defpackage;
```bash
import java.io.BufferedReader;
import java.io.IOException;
import java.util.Base64;
import java.io.InputStreamReader;

/* Loaded from SafeOpener.class */
public class SafeOpener {
    public static void main(String[] args) throws IOException {
        BufferedReader keyboard = new BufferedReader(new InputStreamReader(System.in));
        Base64.Encoder encoder = Base64.getEncoder();
        
        for (int i = 0; i < 3; i++) {
            System.out.print("Enter password for the safe: ");
            String key = keyboard.readLine();
            String encodedKey = encoder.encodeToString(key.getBytes());
            System.out.println(encodedKey);
            
            boolean isOpen = openSafe(encodedKey);
            if (isOpen) {
                System.out.println("You have " + (2 - i) + " attempt(s) left");
            } else {
                return;
            }
        }
    }
    
    public static boolean openSafe(String password) {
        if (password.equals("picoCTF{SAf3_0p3n3r_y0u_solv3d_it_3daf5617}")) {
            System.out.println("Sesame open!");
            return true;
        }
        
        System.out.println("Password is incorrect");
        return false;
    }
}
```
### Step 3: Identifying the Flag
Looking at the openSafe() method, the password comparison reveals the flag in plain text:

if (password.equals("picoCTF{SAf3_0p3n3r_y0u_solv3d_it_3daf5617}")) {
The flag is hardcoded directly in the source code as the expected password value.

## Flag
picoCTF{SAf3_0p3n3r_y0u_solv3d_it_3daf5617}
