If you have a class or method or w/e that does the same thing in a lot of different ways, you can hide the 'same thing' part behind a common interface and swap different implementations in as-needed.

Example is a navigation app that uses different routing algorithms for walking vs driving: put the different algorithms behind a common interface.

Mostly pretty stupid because the client has to instantiate the concrete strategy anyway, and in order to work the strategies have to have a common interface, so why the fuck wouldn't the client just call the strategy directly? Stupid.