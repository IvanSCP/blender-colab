# blender-colab

<a href="https://colab.research.google.com/github/IvanSCP/blender-colab/blob/master/blender_render.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

This is a Python script that allows you to render Blender 5.0+ and older version scenes using Google Colaboratory.

You can upload the blender files using direct upload, Google Drive or URL. Rendered frames can be downloaded directly or through Google Drive.

This fork introduces **EEVEE render engine support** and **embedded script automation** while maintaining full backward compatibility with the original CYCLES workflow.

## Features

* **EEVEE Rendering**: Experimental support for EEVEE/EEVEE Next engine (Blender 2.8+). Note: EEVEE in Colab typically uses CPU/software rendering due to virtual display limitations.
* **Script Automation**: Auto-run embedded Python scripts or specific text blocks via `--python-text`.
* **Multiple Blender Versions**: Supports versions from 2.79b up to 5.2.0.
* **Flexible I/O**: Upload via direct upload, Google Drive, URL, or relative Drive paths.

## Usage

### Upload type
* `direct`: Upload your blender file in the next cell.
* `google_drive`: The blender file will be downloaded directly from Google Drive. You need to specify the path to the blender/zip file at `drive_path`.
* `url`: Direct link to the blender file in `url_blend`.
* `gdrive_relative`: The Google Drive folder specified at drive_path will be copied directly (as if it's a zipped file).

### Render Settings
* `render_engine`: Choose between `CYCLES` (GPU accelerated) or `EEVEE` (CPU/software in Colab).
* `run_scripts`: Enable to auto-run Python scripts embedded in the blend file (drivers, app handlers).
* `python_text`: Specify the name of a Text block inside your blend file to execute via `--python-text` (e.g., `drivers.py`).
* `animation`: Toggle between animation sequence or still frame rendering.
* `start_frame`, `end_frame`: Specify frame range for animation.

### Download type
* `direct`: Output files will be automatically downloaded in your browser. (Probably does not work with multiple files?)
* `google_drive`: The output files will be pasted into the specified `drive_output_path` once rendering is finished.
* `gdrive_direct`: Output frames directly to Google Drive (zipping disabled).

### A few notes
1. You must own a Google account.
2. One notebook can only run for maximum time of 12 hours (24 hours for Google Colab Pro) but not guaranteed.
3. **EEVEE Limitation**: While EEVEE is now supported, it typically renders on CPU (llvmpipe) in Google Colab due to the lack of direct GPU display access. For GPU acceleration, use CYCLES.
4. This script is tested with Blender 2.79b through 5.2.0.
5. Do note that your access to GPU may be limited or blocked if you render for many hours.
6. This script is intended for those who have no access to high-end GPU for rendering. Please use them responsibly!

## FAQ

### An error occured!
Check which section of the code failed and identify the error (such as misspelled files or path). If you don't understand the error, try re-running the code with the play button at the side. If it still fails, go to `Runtime > Restart and run all` to restart the code or try `Runtime > Factory reset runtime`. If all else fails, open an issue in GitHub with the error log you encountered attached and the details of your setup.

Common errors:
* `MessageError: TypeError: Failed to fetch` while downloading: The tab must be opened so that the frames can be downloaded.
* `EGL Error (0x3009)`: When using EEVEE, this indicates software rendering fallback. This is normal in Colab environments.

## Disclaimer
Google Colab is targeted to researchers and students to run AI/ML tasks, data analysis and education, not rendering 3D scenes. Because the computing power provided are free, the usage limits, idle timeouts and speed of the rendering may varies time by time. [Colab Pro and Colab Pro+](https://colab.research.google.com/signup) are available for those who wanted to have more powerful GPU and longer runtimes for rendering. See the [FAQ](https://research.google.com/colaboratory/faq.html) for more info. In some cases, it might be faster to use an online Blender renderfarm.