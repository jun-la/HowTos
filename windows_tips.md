Restore the “Import pictures and videos” AutoPlay Option in Windows 10/11
To add the Import pictures and videos option to the AutoPlay dialog in Windows:

Open an admin Command Prompt window.

Run the following commands:
```
cd "C:\Program Files (x86)\Windows Photo Viewer"
regsvr32 PhotoAcq.dll
regsvr32 PhotoViewer.dll
```
Note: For Windows 32-bit systems, use C:\Program Files instead of C:\Program Files (x86)
