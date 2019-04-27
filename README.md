# vagrant-red-gtk

This repo contains a Vagrantfile allowing us to test [red/red:GTK (currently rcqls/red:GTK-dev)](https://github.com/rcqls/red/tree/GTK-dev) from a VirtualBox.

## Getting started

* install [vagrant](https://www.vagrantup.com) and [VirtualBox](https://www.virtualbox.org)
* copy the Vagrantfile: as an example to do that you could clone this repo 
```
cd <somewhere>
git clone https://github.com/rcqls/vagrant-red-gtk
```
* create the red-gtk-dev VBox:
```
cd vagrant-red-gtk
vagrant up
```
* play with it
```
# to enter inside red-gtk-dev VBox
vagrant ssh
# inside the red-gtk-dev VBox
console-view
# or as an example
console-view ~/install/code/Showcase/ballots/ballots.red
```
* compile a red script
```
cd ~/bin # or any other folder where to put the newly created binary

# recompiling console-view
reds -r ~/install/red/environment/console/CLI/console-view.red

# scripts requiring compilation
reds -r ~/install/code/Scripts/mandelbrot-fast.red
./mandelbrot-fast # to compare with: console-view ~/install/code/Scripts/mandelbrot.red
reds -r ~/install/code/Scripts/perlin.red
./perlin

# script not requiring compilation but change of folder (because of assets for execution)
cd ~/install/code/Showcase/ballots/
reds -r ballots.red
./ballots
```

## the excellent [redCV](https://github.com/ldci/redCV) project (pre-cloned inside the red-gtk-dev VBox)

```
cd ~/install/redCV/samples/image_conversion
reds -r Conversion.red
./Conversion
cd ~/install/redCV/samples/voronoi
reds -r mapdiagram.red
./mapdiagram
```

## Some vagrant tasks

See `vagrant -h` for the complete help. But quickly, it is good to know:

* `vagrant halt` to stop the vbox and `vagrant up` to restart it (in fact equivalent to `vagrant reload`)
* `vagrant suspend` to suspend the vbox and `vagrant resume` to get back to the vbox.
* more carefully, `vagrant destroy` to destroy everything and `vagrant up` to rebuild it.
* `vagrant provision` if you made some changes in the install process?
* `vagrant box -h` to see all the action to manage the virtual boxes.

## Comments

### Already inside the red-gtk-dev box

Inside the red-gtk-dev vbox and inside the `install` folder, there is:


* [red](https://github.com/rcqls/red/tree/GTK-dev) required for compilation from source.
* [reds](https://github.com/rcqls/reds) allowing compilation from red source (`reds` standing for `red` from `s`ource) in a similar way than `red` binary.
* [red/code](https://github.com/red/code) and [red/community](https://github.com/red/community) for testing Red/GTK
* [redCV](https://github.com/ldci/redCV) which requires compilation


### Synced folders

The usual way is to modify the`Vagrantfile` (using `config.vm.synced_folder`) but you can also create a file `synced_folder.cfg` (in the same folder than `Vagrantfile`) with each line following the format `<full_path_host_dir>:<full_fall_guest_dir>`. This file can be updated anytime and then applied with `vagrant reload`. As an example, the following lines constitute a valid `synced_folder.cfg` (on macOS):
```
/Users/rcqls/Github:/home/vagrant/Github
/Users/rcqls/tmp/Demos:/home/vagrant/Demos
```

Note also that `/vagrant` inside the guest is by default synced with the project folder of the host where the `Vagrantfile` is. In particular, this allows us to test interesting projects by cloning or copying them here. Some further projects often tested with `red/GTK`:

* @toomasv projects:
	* [makedoc](https://github.com/toomasv/makedoc) and, in particular, `easy-VID-rt.red`
	* [learnig](https://github.com/toomasv/learning) with, in particular, the lovely styles `shrinkable.red`, `fluid.red` and `responsive.red`.
	* [ast](https://github.com/toomasv/ast)
	* ....
* TO COMPLETE....

### Other folder(s) in this repo

alternative Vagrantfiles are  proposed inside the folders of this repository.