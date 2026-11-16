<p align="center">
    <img alt="Repository logo, colorized Lucide 'copy' icon" src="assets/logo.png" width="300" height="300">
</p>
<h1 align="center">
    Duplicate with Dash
</h1>

First, before I criticize KDE Dolphin, let me just say I love KDE Plasma. I switched from GNOME to Plasma in 2021 after I reached my breaking point with the horrible workflow and the buggy extensions required to make it usable. 

However, I have had one major complaint with the Dolphin file manager. When duplicating files / directories, Dolphin appends the word 'copy' to the file name with a leading space _(e.g., `file-name copy.ext`)_. This is disadvantageous for obvious reasons, and it means I had to rename every duplicated file to follow proper naming best practices. 

Unfortunately, this behavior is hardcoded into KIO, meaning it cannot be changed through standard system settings or GUI menus without modifying system source code or hacking translation files. To achieve this without breaking system files, I created a custom Dolphin Service Menu. It adds a dedicated **Duplicate with Dash** option to the right-click menu that perfectly mimics a duplicate operation but formats the output properly as `file-name-copy.ext`.

## Setup

1. Open your terminal.
2. Clone the repository.

    ``` bash
    git clone https://github.com/benhaube/duplicate-with-dash.git
    ```

3. Enter the repository directory.
   
    ``` bash
    cd duplicate-with-dash
    ```

4. Create the Dolphin custom actions directory if it doesn't already exist.

    ``` bash
    mkdir -p ~/.local/share/kio/servicemenus/
    ```

> [!note] 
> If you are on an older KDE Plasma 5 release, use `~/.local/share/kservices5/ServiceMenus/` instead.

5. Create a new configuration file using a text editor like `nano`.

    ``` bash
    nano ~/.local/share/kio/servicemenus/duplicate-dash.desktop
    ```

6. Copy the file `duplicate-dash.desktop` into the `~/.local/share/kio/servicemenus` directory. This script preserves permissions and timestamps _(`cp -an`)_, avoids overwriting existing files, and intelligently handles file extensions, directories, and hidden files.

    ``` bash
    cp duplicate-dash.desktop ~/.local/share/kio/servicemenus
    ```

7. Give the file execute permission.

    ``` bash
    chmod +x ~/.local/share/kio/servicemenus/duplicate-dash.desktop
    ```

8. Close all open Dolphin windows to force it to reload its context menus, then reopen Dolphin.
9.  **Verification:** Right-click any file or directory in Dolphin. You will now see a Duplicate with Dash option in the context menu. Selecting it will generate a copy formatted as `file-name-copy.ext` without spaces.
