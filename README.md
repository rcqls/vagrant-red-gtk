# vagrant-red-gtk

This repo contains a Vagrantfile allowing us to test [red/red:GTK (currently rcqls/red:GTK-dev)](https://github.com/rcqls/red:GTK-dev) from a VirtualBox.

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

