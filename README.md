# ⬇️ `abx-dl`

> A CLI tool to auto-detect and download *everything* available from a URL.  
> `pip install abx-dl[all]`

> [!IMPORTANT]  
> ❈ *Coming Soon...*  read the [Plugin Ecosystem Announcement (2024-10)](https://docs.sweeting.me/s/archivebox-plugin-ecosystem-announcement#%F0%9F%94%A2-For-the-minimalists-who-just-want-something-simple)  
> <sub>Release ETA: after `archivebox` `v0.9.0`</sub>

---

`abx-dl` is a CLI tool for downloading web content. It tries to be simple, quick, and powerful.

*It's inspired by great tools like `wget`, `curl`, `yt-dlp`, and `gallery-dl` that take a URL write output to the current dir.*

When passed a URL, `abx-dl` downloads content using all configured methods to the current dir:

- page HTML, JS, CSS
- images/video/audio/subs, PDF, screenshot, article text
- source code, [and much more](https://github.com/ArchiveBox/abx-dl#All-Outputs)...

> `abx-dl` abstracts away common, powerful scraping and downloading tools, including: `wget`, `wget-lua`, `curl`, `puppeteer`, `playwright`, `singlefile`, `readability`, `yt-dlp`, `forum-dl`, and many more through the [plugin library](https://docs.sweeting.me/s/archivebox-plugin-ecosystem-announcement)...  
> It replaces the old `archivebox oneshot` command and stands alone as its own tool.

---

### ~~📦 Install~~

```bash
pip install abx-dl[all]
abx-dl install   # optional: install any system packages needed
abx-dl 'https://example.com'
```

### ~~🪶 Lite Install~~

If you don't need everything in `abx-dl[all]`, you can pick and choose individual pieces:
```python
pip install abx-dl abx-plugin-wget abx-plugin-singlefile ...
abx-dl install wget,singlefile,...
abx-dl --extract=wget,singlefile 'https://example.com'
```

---

### Usage
```bash
mkdir ~/Downloads/example.com && cd ~/Downloads/example.com
abx-dl version
abx-dl help

# Basic example usage:
abx-dl --extract=title,singlefile,screenshot,media 'https://www.youtube.com/watch?v=dQw4w9WgXcQ'
```

#### Download everything

```bash
abx-dl 'https://example.com'
ls ./
# <see All Outputs below>
```

#### Download just title + screenshot

```bash
abx-dl --extract=title,screenshot 'https://example.com'
ls ./
# index.json  title.txt  screenshot.png
```

#### Download title + screenshot + html + media

```bash
abx-dl --extract=title,favicon,screenshot,singlefile,media 'https://example.com'
ls ./
# index.json  index.html  title.txt  favicon.ico  screenshot.png  singlefile.html  media/Some_video.mp4
```

#### Pass config options

Config can be persisted via file, set via env vars, or passed via CLI args.
```bash
# set per-user config in ~/.config/abx-dl/abx-dl.conf
abx-dl config --set CHECK_SSL_VALIDITY=True

# environment variables work too and are equivalent
env CHROME_USER_DATA_DIR=./personas/Default/chrome_profile

# pass per-run config as CLI args
abx-dl -c MAX_MEDIA_SIZE=250m --extract=title,singlefile,screenshot,media 'https://www.youtube.com/watch?v=dQw4w9WgXcQ'
```
---

### All Outputs

- `index.json`, `index.html`
- `title.txt`, `title.json`, `headers.json`, `favicon.ico`
- `example.com/*.{html,css,js,png...}`, `warc/`  (saved with `wget-lua`)
- `screenshot.png`, `dom.html`, `output.pdf` (rendered with `chrome`)
- `media/someVideo.mp4`, `media/subtitles`, ... (downloaded with `yt-dlp`)
- `readability/`, `mercury/`, `htmltotext.txt` (article text/markdown)
- `git/` (source code)
- ... [and more](https://github.com/ArchiveBox/ArchiveBox#output-formats) ...

---

For more advanced use with collections, parallel downloading, a Web UI + REST API, etc.  
See: [`ArchiveBox/ArchiveBox`](https://github.com/ArchiveBox/ArchiveBox)
