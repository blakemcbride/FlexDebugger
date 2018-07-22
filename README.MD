
# Flex Debugger

I (Blake McBride) have a very large application written in Flex 3.
When we lost browser debugging support, my app was very hard to
maintain.  A few years ago, I wrote a portable (and simple) debugger
that has served me well.  All it really does is allow you to display
messages and values to the browser console in a very controlled way.
You can easily turn on and off messages within groups of code, and you
can control what level of messages are displayed.  Because of this,
I typically sprinkle debug statements around my code as I debug something.
Later, when I am done, I just turn of debugging with one line of code.
I leave all of the (innocuous) debug statements in place for some future
debugging need.

I can not convert my app to Flex 4 because I have about 500 screens.
Although this debugger is written for Flex 3, I feel pretty confident
that it would be easy to adapt to Flex 4.  (If you do so, please let
me know so I can post any changes.)

## Usage

### Initialization

Add to code that will use the debugger:

    import com.arahant.core.util.Debugger;

and

    private static const module:String = "MyClassName";

at the appropriate places.

### Debug Levels

There are 4 debug levels as follows:

	0 = no logging
	1 = only error (default)
	2 = only error and warn
	3 = error, warn, log, info, and value

What is displayed is controlled by a combination of the specified `module`
and the debug level for that module using the following function:

    Debugger.setModuleLevel(module, level)
    
If you want to find a module's setting, use:

    Debugger.getModuleLevel(module)

### Argument Descriptions

In what follows:

level | number | an integer, 0 through 3
module | string | name of module or class
location | string | method name + optional space and position number
msg | string | a message (usually optional)
expression | string | the expression being displayed
value | any | the value of the expression

### Debug Functions

Display a location marker with an optional message at the indicated debug level.

    Debugger.info(module, location, msg=null)
    Debugger.log(module, location, msg=null)
    Debugger.warn(module, location, msg=null)
    Debugger.error(module, location, msg=null)
    
Display a value with an optional message at debug level 3 only.

    Debugger.value(module, location, expression, value)

Display an error and throw an exception.  Basically a replacement
for `throw new Error("message")`

    Debugger.throwError(module, location, msg=null)
    

## Home for this package is:  [https://github.com/blakemcbride/FlexDebugger](https://github.com/blakemcbride/FlexDebugger)
