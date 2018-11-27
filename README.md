# WindowsProject1
Example Win32 Desktop Project to test MUI

Visual Studio 2017 - UTF-8 Encoding Problems

WindowsProject1: 
----------------
Created from scratch, using menu 
   File->New->Project... Visul C++/Windows Desktop -> Windows-Desktop-Application
   
Changes:
--------
+ WindowsProject1.rc:
  - Converting to UTF-8 encoded File
  - splitting and including:
     commonres.rc (exclude from build, but included in WindowsProject1.rc)
     menu.rc      (exclude from build, but included in WindowsProject1.rc)
     dialogs.rc   (exclude from build, but included in WindowsProject1.rc)
     strings.rc   (exclude from build, but included in WindowsProject1.rc)

+ replacing LTEXT in Aboutbox dialog by readonly EDITTEXT control 
  to show text of foreign languages (dialogs.rc)
  
  
Problems:
---------

1.) If all .rc files are UTF-8 encoded, the project compiles fine, but:
   the text of Aboutbox (Belarusian) shows "diamond questionmarks",
   which are not in the UTF-8 resource files (see screenshot)
   
2.) Converting all .rc files to UTF-8-Sig 
   (some say UTF-8-BOM, but it is no "Byte-Order-Mark, UTF-8 has no byte ordering)
   the project does not compile anymore
   
3.) Using UTF-8 for WindowsProject1.rc and
         UTF-8-Sig/BOM for included .rc files (commonres.rc, menu.rc, ..., strings.rc)
   the project compiles fine AND(!) the foreign language text displays correct,
   but:
     the included .rc files (UTF-8-Sig/BOM) cannot be edited by the VS Resource-Editor anymore.

4.) Using UTF-8 (no Sig/BOM) for all .rc files:
    (despite of the "diamond questionmarks" display problem (1.)))
    The .rc files can be edited by the Resource-Editor (they are displayed fine),
    UTF-8 decoding seems to work fine for the Resource-Editor,
    but on saving changes, the file is converted to an ANSI encoding for the desired
    language (ANSI Code-Page 1251 for Belarusian , CP-936 for Japanese, etc.),
    and the "#pragma code_page(65001) is changed accordingly.
    THIS IS NOT WANTED: Why not keeping UTF-8 encoding ???
    
