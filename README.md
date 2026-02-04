# copy_models.sh

Copy Hugging Face model folders from a USB drive (or any directory) into your local Hugging Face cache.

## What it does

- Lists top-level directories in the **current directory** (e.g. your USB mount point).
- Lets you pick one by number.
- Copies that folder into `~/.cache/huggingface/hub/` so Navigator can use it.

Folder names are shown without the `models--` prefix for readability; the actual directory names on disk are unchanged.

## Requirements

- Bash
- Write access to `~/.cache/huggingface/hub/`

## Usage

1. **Mount your USB drive** (if using one).

2. **Go to the folder that contains the model directories:**
   ```bash
   cd /path/to/usb/or/folder/with/models
   ```

3. **Run the script:**
   ```bash
   ./copy_models.sh
   ```
   Or with `bash`:
   ```bash
   bash copy_models.sh
   ```

4. **Follow the prompts:**
   - The script lists numbered model folders.
   - Enter the number of the model you want, or `q` to quit.
   - It copies the chosen folder into your cache and reports success or failure.

## Cache location

Models are copied to:

```text
/Users/<your-username>/.cache/huggingface/hub/<model-folder-name>/
```

This is the default Hugging Face Hub cache directory, so models will be found by `transformers`, `diffusers`, and other HF tools without extra config.

## Example

```text
Hello yourname!
Using folders from: /Volumes/MODELS

Models available:
     1  some-org/some-model
     2  another-org/another-model

Enter the number of the model you want to copy to your .cache folder (or 'q' to quit):
 1

Selected model: models--some-org--some-model
Copying folder models--some-org--some-model to /Users/yourname/.cache/huggingface/hub/...
...
Folder successfully copied to /Users/yourname/.cache/huggingface/hub/models--some-org--some-model
```

## Notes

- Only **top-level** directories are listed; hidden directories (names starting with `.`) are skipped.
- If the target folder already exists in the cache, the script overwrites/merges with `cp -Rv`.
- The script uses your current working directory as the source; run it from the USB path (or the folder that contains the model dirs).
