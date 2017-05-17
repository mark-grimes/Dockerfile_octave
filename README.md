By default starts qtoctave, so you need to set up X11 forwarding in some manner.  E.g. from Mac OS X

    docker run --rm -e DISPLAY=192.168.99.1:0 markgrimes/octave

where the IP address is the virtual box bridge (e.g. type `ifconfig vboxnet0` on the **Mac** host).  This will require Xquartz installed and the Preferences->Security->"Allow connections from network clients" option checked.  You'll probably also require ``xhost +`docker-machine ip default` `` in a command prompt to allow connections from the docker VM.

On linux it's much easier to just share the X11 socket:

    docker run --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix markgrimes/octave

On windows it's the same command as for Mac. You need Xming installed and "No Access Control" selected.  There are detailed instructions on https://github.com/moby/moby/issues/8710#issuecomment-135109677.
