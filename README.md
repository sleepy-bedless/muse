# muse
A simple real time music generator based on Markov Chain.   
Initially designed for Python, but if you want, you can easily use it in cpp files.
> [How it may help you](https://github.com/sleepy-bedless/muse/blob/main/README.md#how-it-may-help-you)
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
Next, download `setup.py` and `muse.i`. Then use [SWIG](https://github.com/swig/swig) (for example) to build Python module.
### Use swig to build muse
Firstly, make sure your swig is OK.
```
swig -c++ -python muse.i
python setup.py build_ext --inplace
```
If everything goes well, you will get many files. Cut `muse.py` and `_muse.xxxxxx.pyd` to your py dir, then `import muse`.

## Create brand-new music
Now your `muse` module should be accessible.

### Use class Note to play note
```c++
// example.cpp
// ...
void main()
{
    Note midi_note;    // first, we get a Note object
    midi_note.open();  // this will get your midi handle so that you can play note
    midi_note.play_note(75, 100, 1, 0);
      // to play a note, you should send note(0-127), velocity(0-127), instrument(0-127, default 0), channel(0-15, default 0)
    Sleep(500);        // pause it, then you hearing sound.
    midi_note.close()  // if everything done, don't forget to close it
}
```
### Use class MarkovGenerator to play music
If you have your models, you can easily create music with MarkovGenerator.  
You need 3 model, for note, velocity and time. If one of witch has no model, it will use default const.
```c++
// example.cpp
// ...
void main()
{
    Note midi_note;
    MarkovGenerater MC;

    MC.set_module_note("output_note.model");   // load model for note
    MC.set_module_time("output_time.model");
    MC.set_fixed_velocity(100);                // if no loaded model, you can change the used default const
    MC.set_seed(time(0));                      // you can set random seed with, such as, fortune number

    midi_note.open();                          // certainly you need to open Note
    for (int i = 0; i < 100; i++) {
        std::cout << i << std::endl;
        Sleep(0.5 * MC.play_note(midi_note));  // MarkovGenerater.play_note will return the time of note
          // you should send a Note object, and you can change instrument(0-127, default 0) and channel(0-15, default 0)
    }
    midi_note.close();
}
```
#### i will write all, maybe tomorrow
