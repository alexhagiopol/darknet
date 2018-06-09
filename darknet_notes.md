# YOLO Notes

The author documents quite well how to use YOLOv3 here https://pjreddie.com/darknet/yolo/.

Darknet is his own equivalent to TensorFlow or Pytorch written completely
in C with no dependencies (CUDA is optional). I’m amazed that (1) one
person was able to do this and (2) the code is as simple as it is. Some
of the code is difficult to read, but the structure is clear and the
function names all very obviously map to mathematical operations.
1. The `main()` method for Darknet is in `examples/darknet.c` [link](https://github.com/pjreddie/darknet/blob/f6d861736038da22c9eb0739dca84003c5a5e275/examples/darknet.c#L403)

	a. `main()` contains the functions calls for each of the command
	line options explained in the YOLO website: *detect*, *detector test*,
	*detector demo*, and *detector train*.

	b. We will pursue *detector train* because it should execute the meat of
	the YOLO paper. If the `main()` function is passed the word *detector*
	it calls the `run_detector(int argc, char **argv)` function.

	c. `run_detector(int argc, char **argv)` is defined in `examples/detector.c` [link](https://github.com/pjreddie/darknet/blob/f6d861736038da22c9eb0739dca84003c5a5e275/examples/detector.c#L794)
    This function calls many instances of `find_char_arg(int argc, char **argv, char *arg, char *def)`
    defined in `src/utils.c`. `find_char_arg()` searches command line arguments
    for expected char sequences such as *-prefix* and returns the argument values.

    d. After parsing command line arguments, `run_detector()` will call
    `train_detector()` if the *train* argument is given. The important
    arguments for this function are (1) the location of the data configuration
    file e.g. *cfg/voc.data* which contains training and validation labels
    and (2) the network configuration file e.g *cfg/yolov3-voc.cfg* which
    contains the definition of the network architecture.

2. The training operation for YOLOv3 is in `train_detector(char *datacfg, char *cfgfile, char *weightfile, int *gpus, int ngpus, int clear)`
   [link](https://github.com/pjreddie/darknet/blob/f6d861736038da22c9eb0739dca84003c5a5e275/examples/detector.c#L6)

   a.




	

2. The training operation for YOLOv3 is here [link](https://github.com/pjreddie/darknet/blob/f6d861736038da22c9eb0739dca84003c5a5e275/examples/detector.c#L6)

What’s nice is that the common neural network operations each have their own .c file in the /src directory. E.g. connected_layer.c and convolutional_layer.c. The general structure of the codebase is that the “library” part of Darknet that contains common neural network operations is in /src and the “applications” part of Darknet that contains different specific uses of the core library is in /examples. The different applications are the YOLO detector and the author’s other neural network projects.