# muse
A simple real time music generator based on Markov Chain.   
Initially designed for Python, but if you want, you can easily use it in cpp files.

## How it may help you
- __A real time pure music player.__  
  It will never create .mid files, which means you can play your music ceaselessly.
- __A music generator based on Markov Chain.__  
  You can create random music with given models.
- __A model builder.__  
  You can easily train your own models.

If you want something above, try `muse`! Actually, I haven't found one can play music without created midi files.

### Something you need to know
- __The program hardly check whether input is 'good'.__  
  I test it can do well in normal conditions. But what will happen when you send 'bad' models? The god knows.
- __Poor algorithm.__  
  The program may be useful but can't be powerful. I'm sorry.

## Install muse
First, download `muse.h`. Now you can use it in your cpp files. Easily. `#include "muse.h"`
Next, download `setup.py` and `muse.i`. Then use SWIG (for example) to build Python module.
### Use swig to build muse
Firstly, make sure your swig is OK.
```
swig -c++ -python muse.i
python setup.py build_ext --inplace
```
If everything goes well, you will get many files. Cut `muse.py` and `_muse.xxxxxx.pyd` to your py dir, then `import muse`.

#### i will write all, maybe tomorrow
