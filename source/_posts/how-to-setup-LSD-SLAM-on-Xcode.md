title: How to setup LSD-SLAM on Xcode
date: 2016-03-21 23:34:26
tags: [slam, xcode]
categories: slam
---

The original project uses ROS (Robot Operating System) for visualization which is not very compatible with Mac. So ROS is replaced with an open source visualization framework [Pangolin](https://github.com/stevenlovegrove/Pangolin), and I also made some changes to Apple compiler. Here are the steps to setup LSD-SLAM on your Xcode (I am using Mac OSX 10.11 with Xcode 7.2.1).

##### Clone the Repo
The Pangolin version LSD-SLAM is hosted under my github, [https://github.com/ningt/lsd_slam_xcode](https://github.com/ningt/lsd_slam_xcode).

<!--more-->

##### Install Homebrew
I am using [brew](http://brew.sh) to install dependencies.

##### Install Dependencies
Use `brew` to install `boost, glew, glm, libqglviewer, suite-sparse, eigen, cmake, opencv, qt`. 

##### Build Pangolin and g2o
Clone and build [Pangolin](https://github.com/stevenlovegrove/Pangolin) and [g2o](https://github.com/RainerKuemmerle/g2o). For g2o, you need to add one line to its `CMakeLists.txt` in order to find `libqglviewer`. 

```
#CMakeLists.txt

SET(QGLVIEWER_INCLUDE_DIR "/usr/local/Cellar/libqglviewer/2.6.1/lib/QGLViewer.framework/Headers")
```

```
$ mkdir build
$ cd build
$ cmake ..
$ make
$ make install # remember to run this
```


##### Change Xcode Settings
Open the project with Xcode, under `build settings -> header search path`:

```
/usr/include
/usr/local/include
/usr/local/Cellar/eigen/3.2.8/include/eigen3
/PATH/TO/THE/PROJECT/lsd-slam-pangolin
/PATH/TO/THE/PROJECT/lsd-slam-pangolin/thirdparty/Sophus/
```

under `build settings -> library search path`:

```
/usr/lib
/usr/local/lib
```

under `build phases -> link binary with libraries`, add the following libs (by default, `brew` will install packages to `/usr/local/Cellar/`):

```
libg2o_stuff.dylib
libg2o_solver_csparse.dylib
libg2o_csparse_extension.dylib
libg2o_types_sba.dylib
libg2o_core.dylib
libz.tbd
OpenGL.framework
libopencv_calib3d.2.4.12.dylib
libopencv_imgproc.2.4.12.dylib
libGLEW.1.13.0.dylib
libboost_filesystem.dylib
libboost_system.dylib
libboost_thread-mt.dylib
libopencv_highgui.2.4.12.dylib
libopencv_core.2.4.12.dylib
libpangolin.dylib
GLUT.framework
```

##### Pass Input Argument
At top navbar, under `Profuct -> Scheme -> Edit Scheme -> Arguments`:

```
-f /PATH/TO/images/
-c /PATH/TO/calibration.cfg
```

##### Trouble Shooting
- If you get error: `dyld: library not loaded. Reason: image not found`
	
	go to the directory where the output executable is generated, and follow the solution here. [http://stackoverflow.com/questions/17703510/dyld-library-not-loaded-reason-image-not-loaded](http://stackoverflow.com/questions/17703510/dyld-library-not-loaded-reason-image-not-loaded)
