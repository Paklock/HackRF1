The easiest way is to use Docker.

For building:
`docker build -t portapackccache -f dockerfile-nogit .`

For running (in the root of the repo):
`docker run -it -v ${PWD}:/havoc portapackccache`