# SuperCollider for Atom

A SuperCollider development environment for Atom.io

---

SuperCollider is a programming language for real time audio synthesis and algorithmic composition.

https://supercollider.github.io

---

1. SuperCollider comes with a cross platform **IDE** (OS X/Linux/Windows) which communicates with the language interpreter.

2. The language interpreter runs in a separate process (**sclang**) and includes comprehensive bindings for making Qt based GUIs. sclang compiles and executes SuperCollider code, manages event schedulers (for making music) and creates GUIs. It can also send and receive OSC (Open Sound Control) and MIDI.

3. The SuperCollider synthesis server (**scsynth**) runs in a separate process or even on a separate machine so it is ideal for realtime networked music. It just makes music, its quite efficient and the audio quality is very high. Communication between sclang and scsynth is via OSC (Open Sound Control).

SuperCollider Atom is an alternative to the IDE. Atom is free, open source and very hackable.


---


### Installation

##### 1. Install this package:

using Atom's 'Install Packages', search for "supercollider"

##### 2. Download and install SuperCollider:

https://supercollider.github.io

##### 3. It should work

If you've installed SuperCollider in a non-standard place or have a development build, then create a .supercollider.yaml file to specify the path

See "Preferences" below.

##### 4. Open an .scd file in an Atom project, and then open a post window (shift-cmd-k)

---

### REPL

| key              | command                                         |
| ---------------- | ----------------------------------------------- |
| `shift-cmd-K`    | Compile library (open window if needed)         |
| `shift-enter`    | Evaluate selection or current line              |
| `shift-cmd-C`    | Clear post window                               |
| `cmd-.`          | Panic ! Stop all music                          |


You may customize these in your own Keymap file.


### Lookup classes and methods with `shift-cmd-r`

Lookup is done using Atom's Symbol View which is powered by the venerable ctags.
Its quite fast and uses fuzzy finder. All sc classes and methods are tagged.

Install ctags if you need to:

os x

    brew install ctags

ubuntu

    sudo apt-get install exuberant-ctags

windows

    http://ctags.sourceforge.net/


Add support for the supercollider language by making a file called ~/.ctags

    --langdef=supercollider
    --langmap=supercollider:.sc
    --regex-supercollider=/^([A-Z]{1}[a-zA-Z0-9_]*) /\1/c,class/
    --regex-supercollider=/^[[:space:]]*(\*[a-z]{1}[a-zA-Z0-9_]*) \{/\1/m,method/
    --regex-supercollider=/^[[:space:]]*([a-z]{1}[a-zA-Z0-9_]*) \{/\1/m,method/

- Symlink quarks and the SCClassLibrary into your project directory
- Install `symbol-gen` package
- Regenerate tags with `cmd-alt-g` or "Symbol Gen: Generate"
- `shift-cmd-r` will now be able to find all classes and methods
- Select a classname, `alt-cmd-down_arrow` to go to the definition

Best practice is to symlink the Extensions and SCClassLibrary into your current project directory. Then all Classes will be indexed and easy to look up.
I might find a way to pass the class paths to ctags later.

There is also a package called 'goto' that uses the language grammar to generate symbols rather than ctags.  If you do a lot of non-class development then this might be a useful approach. I find it tags too much junk, and I like having just classes and methods in my tags file.

### GUI

SuperCollider has a comprehensive Qt based gui toolkit.  GUIs in SuperCollider Atom work just as they do with the SCIDE, they run in the separate language process:

    Server.default.makeWindow

### Help files:

cmd-shift-p  and type "open help file..."

Or use the context menu (right-click) on the class name or method name to lookup.

The help browser will open in a new window.


(TODO: open help files directly in Atom)

## Preferences

Configuration files are managed by supercollider.js and are documented here:

http://supercolliderjs.readthedocs.org/en/latest/configuration.html

tldr: You create a .supercollider.yaml in your working directory or your home directory
and specify paths to sclang and scsynth

##### Default paths:

**OS X**

`"/Applications/SuperCollider/SuperCollider.app/Contents/Resources/sclang"`

**Linux**

`"/usr/local/bin/sclang"`

**Windows**

`"C:\Program Files\SuperCollider\sclang.exe"`


## Missing Features

#### Built in server window

    s = Server.default;

    // but its easy to make a server window
    s.makeWindow


#### Native Auto-complete

There are many Atom packages for auto-complete. However they use text matching and not direct introspection.
It would be possible to dump the class/method interface to a JSON file and then load that into auto-complete-plus.
This would provide pretty good auto-complete with argument names and everything.
