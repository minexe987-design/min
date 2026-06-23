MINEXE  —  Roblox game utility (UI + ESP overlay)
==================================================

FILES
-----
  main.cpp      Entry point. Attaches to RobloxPlayerBeta.exe, walks the
                DataModel, scans the Workspace for kit objects, and gathers
                players for ESP. Spawns the UI and overlay threads.
  UI.h / UI.cpp The MINEXE control-panel window (Win32 + GDI+): splash screen,
                checkbox panel, and the shared g_UIState that the toggles drive.
  Overlay.h /   The transparent click-through ESP overlay drawn on top of the
  Overlay.cpp   game: kit text labels + player boxes / skeleton / names / health.
  Memory.h      Process memory helpers (attach, Read<T>, ReadString) and the
                Offsets namespace (all the Roblox struct offsets).
  preview.cpp   Tiny standalone program that opens ONLY the UI (no game needed),
                handy for tweaking the look.

  AntiExploit.exe   The real app (build from main + UI + Overlay).
  preview.exe       UI-only preview.
  build.bat         Builds both. Run from the x64 Native Tools prompt.

BUILDING
--------
  1. Open "x64 Native Tools Command Prompt for VS".
  2. cd /d C:\Users\min\Desktop\AntiExploitRoblox
  3. build
     (or manually:
        cl /EHsc /std:c++17 main.cpp UI.cpp Overlay.cpp /link gdiplus.lib user32.lib gdi32.lib winmm.lib /OUT:AntiExploit.exe )

RUNNING
-------
  - Start Roblox and fully join a game FIRST.
  - Then run AntiExploit.exe. The console shows attach progress; the MINEXE
    window appears and the status dot turns green ("Connected").
  - Toggle the checkboxes. Changes take effect on the next scan (<=1.5s).
  - To preview just the UI without the game: run preview.exe.

NOTES
-----
  - Kit ESP keywords must match the in-game instance Name exactly. Watch the
    console "Found:" lines; adjust the keywords in UI.cpp if a toggle finds 0.
  - Player ESP needs the console "[Players] gathered N" count > 0 to draw.
  - The PVP "Aim Assist" checkbox is a UI placeholder only; no aiming logic
    is wired to it.
