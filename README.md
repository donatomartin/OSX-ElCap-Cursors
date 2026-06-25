<img width="640" height="400" alt="image" src="https://github.com/user-attachments/assets/cc29ee70-3d11-4758-8845-f642d6825c30" />


Obtained from:
https://www.opendesktop.org/p/1084939/

How to Enable this cursor theme on Nix Home-Manager:

```nix
{ pkgs, ... }:
let
  cursorTheme = pkgs.stdenvNoCC.mkDerivation {
    pname = "el-capitan-cursor";
    version = "unstable";

    src = fetchGit {
      url = "https://github.com/donatomartin/OSX-ElCap-Cursors.git";
      rev = "3eef2baa4533336114e0f302a56c0b8d2e1a8154";
    };

    dontBuild = true;

    installPhase = ''
      mkdir -p "$out/share/icons/El-Capitan"
      cp -r cursors "$out/share/icons/El-Capitan/"

      cat > "$out/share/icons/El-Capitan/index.theme" <<EOF
      [Icon Theme]
      Name=El Capitan - Cursor
        Comment=El Capitan cursor theme
        EOF
    '';
  };
in
{
  home.pointerCursor = {
    gtk.enable = true;
    name = "El-Capitan";
    size = 12;
    package = cursorTheme;
  };

}
```
