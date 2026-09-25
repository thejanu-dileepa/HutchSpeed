# HutchSpeed

<img width="512" height="512" alt="unnamed" src="https://github.com/user-attachments/assets/43fcd6f3-f6e5-4af6-9e0b-e566339b1c3e" />




## How it works

- A background thread performs the HTTPS check with **WinHTTP**
  (any HTTP response counts as "good" — exactly like `main.py`, which only
  treats an exception as an error) and posts the result to the UI thread.
- The popup is a layered window (fade/pulse via `SetLayeredWindowAttributes`),
  drawn with the **GDI+ flat API** called directly from C.
- Images are loaded from embedded `RCDATA` resources through
  `CreateStreamOnHGlobal` + `GdipLoadImageFromStream`, pre-scaled once to
  300×300 for cheap animation frames.
- The process is per-monitor DPI aware, so the popup stays crisp on
  high-DPI displays.
