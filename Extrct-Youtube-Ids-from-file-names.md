# How to extrat Youtube video IDs from filenames


```
how to extravt video id from filenames below?

'/mnt/storage/gameplaycaptions/UHD-ExtensiveCaptions/E/rm_HXLZtIoA_00042.jpg.json',
 '/mnt/storage/gameplaycaptions/UHD-ExtensiveCaptions/E/rm_HXLZtIoA_00051.jpg.json',

the id is rm_HXLZtIoA

/mnt/storage/gameplaycaptions/UHD-ExtensiveCaptions/A/Z_f9JlKHAPE_00004.jpg.json',
 '/mnt/storage/gameplaycaptions/UHD-ExtensiveCaptions/A/Z_f9JlKHAPE_00055.jpg.json',

the id is Z_f9JlKHAPE
```


### GPT Answer (Wrong)

```python
import os

def extract_video_id(filename):
    # Extract the base name of the file
    base_name = os.path.basename(filename)
    # Split by underscore and take the part before the first underscore
    video_id = base_name.split("_", 1)[0]
    return video_id

# Example usage
filenames = [
    '/mnt/storage/gameplaycaptions/UHD-ExtensiveCaptions/E/rm_HXLZtIoA_00042.jpg.json',
    '/mnt/storage/gameplaycaptions/UHD-ExtensiveCaptions/E/rm_HXLZtIoA_00051.jpg.json',
    '/mnt/storage/gameplaycaptions/UHD-ExtensiveCaptions/A/Z_f9JlKHAPE_00004.jpg.json',
    '/mnt/storage/gameplaycaptions/UHD-ExtensiveCaptions/A/Z_f9JlKHAPE_00055.jpg.json',
]

for filename in filenames:
    video_id = extract_video_id(filename)
    print(video_id)
```


### Mistral-Medium (Correct)

```python
import re

# List of filenames
filenames = [
    '/mnt/storage/gameplaycaptions/UHD-ExtensiveCaptions/E/rm_HXLZtIoA_00042.jpg.json',
    '/mnt/storage/gameplaycaptions/UHD-ExtensiveCaptions/E/rm_HXLZtIoA_00051.jpg.json',
    '/mnt/storage/gameplaycaptions/UHD-ExtensiveCaptions/E/rm_HXLZtIoA_00036.jpg.json',
    '/mnt/storage/gameplaycaptions/UHD-ExtensiveCaptions/E/rm_HXLZtIoA_00045.jpg.json',
    '/mnt/storage/gameplaycaptions/UHD-ExtensiveCaptions/A/Z_f9JlKHAPE_00004.jpg.json',
    '/mnt/storage/gameplaycaptions/UHD-ExtensiveCaptions/A/Z_f9JlKHAPE_00055.jpg.json'
]

# Regular expression pattern to match the video ID
pattern = r'^(.*?)/([^/]+)_'

# Extract video IDs using regular expression <---- This is correct
video_ids = [re.match(pattern, filename).group(2) for filename in filenames]
print(video_ids)

# Extract video IDs by splitting and slicing the string <---- This is wrong
video_ids = [filename.split('/')[-2].split('_')[0] for filename in filenames]
print(video_ids)
```