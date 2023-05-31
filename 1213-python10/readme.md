# Pytube Fix
For pytune==12.1.3 and python 3.10 on GoogleColab


## innertube.py
Getting an error on __main__.py
```
File "/Users/bennicholl/opt/anaconda3/lib/python3.8/site-packages/pytube/__main__.py", line 346, in title
    raise exceptions.PytubeError(

PytubeError: Exception while accessing title of https://youtube.com/watch?v=JxnIkZU-oFE. Please file a bug report at https://github.com/pytube/pytube
```
Change innertube.py
Line 78<br>
from     `def __init__(self, client='ANDROID', use_oauth=False, allow_cache=True):`
to     `def __init__(self, client='WEB', use_oauth=False, allow_cache=True):`
> Pytube/innertube.py in line 78 change client = 'ANDRIOD' to client = 'WEB'

## Captions.py
/usr/local/lib/python3.10/dist-packages/pytube/captions.py

in line 85
```
replace 
for i, child in enumerate(list(root)):
to 
for i, child in enumerate(list(root.findall('body/p'))):
```

in line 89
```
replace 
duration = float(child.attrib["dur"])
to:
duration = float(child.attrib["d"])
```

Then on line 92, 
```
replace:
start = float(child.attrib["start"])
to:
start = float(child.attrib["t"])
```

If only the number of lines and time will be displayed but no subtitle text, replace line 86:
```
text = child.text or ""
to:
text = ''.join(child.itertext()).strip()
if not text:
    continue
```

## cipher.py
modify /usr/local/lib/python3.10/dist-packages/pytube/cipher.py

look for the answer of dark9ive. i cite here to the team to close the duplicated issue.

Solution that worked for me:

simply modifying /usr/local/lib/python3.10/dist-packages/pytube/cipher.py
Line 411
```
transform_plan_raw = find_object_from_startpoint(raw_code, match.span()[1] - 1)
to
transform_plan_raw = js
```
then restart the runtime
