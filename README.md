# Photo Metadata Extractor (Local) — v1

A small **offline** Windows-friendly tool that extracts **file + EXIF metadata** from photos in a folder and exports it to **CSV** (optionally JSONL).

- Local-first / no uploads
- Simple GUI (like your PDF2Text tool) + CLI mode
- Works best for JPEG/JPG; also supports PNG/TIFF/WEBP (EXIF availability depends on format)

## Install

```powershell
pip install pillow
```

## Run (GUI)

```powershell
python .\photo_metadata_extractor_local.py
```

## Run (CLI)

```powershell
python .\photo_metadata_extractor_local.py --folder "C:\Photos"
python .\photo_metadata_extractor_local.py --folder "C:\Photos" --out "C:\Photos\meta.csv"
python .\photo_metadata_extractor_local.py --folder "C:\Photos" --recursive
python .\photo_metadata_extractor_local.py --folder "C:\Photos" --jsonl
```

## Output fields

The CSV includes:

- filepath, filename, ext
- file_size_bytes, created_time, modified_time
- width, height
- date_time_original, date_time_digitized, date_time
- camera_make, camera_model, software, orientation
- gps_lat, gps_lon, gps_alt_m (if present)
- has_exif, exif_error

## Notes / limitations (v1)

- Extraction-only. (We can add **strip metadata** and **edit metadata** as v2/v3.)
- Some images have no EXIF; those rows will still include file metadata.
- GPS is only present if it was recorded and not stripped.

## Packaging (optional)

```powershell
pip install pyinstaller
pyinstaller --noconfirm --clean --onefile --windowed --name "photo-meta-extractor" .\photo_metadata_extractor_local.py
```

EXE output: `dist\photo-meta-extractor.exe`
