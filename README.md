# Sketch Framer 3
[![Gitter](https://badges.gitter.im/Join Chat.svg)](https://gitter.im/bomberstudios/sketch-framer-3?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

**BEWARE: The plugin is not yet ready for human consumption. Also: it requires Sketch 3.0.3 7882 or better, and Framer Generator Version 3.0.26 (30) or better**

This is the home of version 3 of the Sketch Framer plugin, for Sketch 3, to export to Framer 3. Yes, 3.0 is the new black.

## Known Issues

- **Complex documents will crash Sketch on export**. We're working to get that fixed, but meanwhile you can try these workarounds:
  - Flatten complex layers, either by adding a `*` to the end of the layer name, or by converting them to bitmaps
  - Split your document in multiple documents
  - Delete layers you don't plan to use (or mark them as "Please ignore" by adding a `-` to the layer name)

## How-to

Run this on the project folder to concatenate the multiple parts of the plugin into a single .sketchplugin file and install it into all known destinations (Sketch Release, Sketch Beta, Framer Generator):

    rake

Please note:

- This script assumes that **Framer Generator.app** lives in /Applications/. Please move it there if it isn't installed already.
- Right now the plugin only generates the view information of a Framer project if you run it from Sketch. This is because the plugin is intended to be run from Framer Generator, which takes care of generating the whole project skeleton.
- The `Export to Framer.sketchplugin` file won't be stored in the repo until we get all the issues fixed :)


## Development

If you'll be working on the plugin's code, you'll probably want to get the build system working. For that, you need to run this once, after cloning the repo:

    $ sudo gem install bundler
    $ bundle install --path vendor/bundle

and then, when you want to work on the code, run this:

    $ bundle exec guard -i

This will watch the repo folder, compile and install the plugin everytime a .js file on the 'src' folder is updated. It'll also announce the fact with a nice voice message.

When you're done, just hit `Ctrl + C` on the Terminal window to stop guard.


## TODO

- [x] hidden layers should remain hidden after export
- [x] hidden layers should have metadata visibility set to none
- [x] hide artboards others than the first
- [x] fix position for nested layers
- [x] fix position for layers with shadows
- [x] fix random crashes
- [x] backport Cemre's mask support
  - I think this is done, but I need testers to confirm it...
- [x] Optimization: export all assets in the same sandbox operation?
- [x] Export in a tmp folder, and pass it to Framer Generator so it moves the files to the right place
- [x] Layer stacking is wrong? Check align.sketch #7
- [x] Add back keywords #10
  - [x] **Flatten** To have a group flattened so its child groups don't export individually, append `*` to its name. Example: `Card*`. Flattening complex groups will improve performance.
  - [x] **Shape/text layers** To export a shape or a text layer as a view, put it in a group, or append `+` to its name. Otherwise they will export as a background image.
  - [x] **Ignore** To ignore a layer, append `-` to its name. Example: `Ignored-`
  - [x] **Hidden layers** Hidden layers in Sketch will be exported as hidden layers in Framer. To show the layer in Framer, try `layer.visible = true`
- [x] **Masks** Native masks now work! You can also use Scroll in the name of a group that includes a mask to make that group scrollable. To scroll the layer in Framer, do `layer.scroll = true`
- [ ] Fix artboard positions
- [ ] Symbol support?
- [ ] Issue #12 seems to be related with layer complexity
- [x] Also, layers named just '+' are exported when they shouldn't (also, they seem to crash the script?)
- [x] #15 Remove keywords (*/+) from layer name for easier access
- [ ] #16 document crashes.
   - I thought this was related to elapsed running time (timeouts, maybe?), but a basic, long running script works without a hitch.
   - Maybe we could move back to export assets one by one?
- [ ] #17 document crashes
- [ ] #10 + keyword not working in bitmap layers
- [ ] #10 * keyword not removed from JS name

## Ideas / Future

- [ ] Maybe add a preference panel where you can setup export options (specially if we end up flattening complex layers to avoid crashes)