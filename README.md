## <a name='TOC'>Table of Contents</a>

1. [Clean Code](#cleanCode)
2. [Naming](#naming)
3. [Functions](#functions)
4. [Comments](#comments)
5. [Formatting](#formatting)
6. [Objects and Data Structures](#objectsAndDataStructures)
7. [Error Handling](#errorHandling)

# <a name='introduction'>Clean Code 🤖</a>

* You will not make the deadline by making the mess, but the contrary
* A programmer with code sense will take a look on a messy and know what to do to fix that
* Bad code tempt the mess to grow
* Clean Code is focused
* Clean code is code that was made by someone that cares. You can try to change and will can’t do it
* It is the programmer that make the language look simple
* Make it easier to read, to make it easier to write
* Leave the campground cleaner than you found it

# <a name='naming'>Naming 👀</a>

* get is not different than retrieve, so stick with one and keep the pattern
* names should reveal intent
* choosing good names takes time but saves more than it takes
* change the names when you find better ones

```java
// good
setSameELigibilityStatusForAllPassengerIfNecessary()
hasEligibilityStatusThatImpactsWholeReservation()
```
The name of a variable, function, or class, should answer all the big questions. It should tell you why exists, what it does, and how it is used.

```java
// bad
private boolean shouldSearchByTicketNumbers(List<String> ticketNumbers) {
    return ticketNumbers != null && ticketNumbers.size() > 0 && ticketNumbers.size() <= 4;
}
// why this logic exists? 
```

```java 
for(Segment segment1 : pnr.getSegments())
```
 
 ___
Don't use noisy words. What is the difference between and __ProductInfo__ and __ProductData__? You have made the names different without making them mean anything different.

How is _NameString_ better than name? Would a _name_ ever be a floating point number? If so, it breaks an earlier rule about disinformation.

```java
 List<String> editList =  acsPassengerSecurityRSACS.getPassengerInfoResponseList().
 getPassengerInfoResponse().get(0).getEditCodeList().
 getEditCode();
 // bad: should be editCodes
```
***
###Class Names
Classes and objects should have nour or noun phrase names like _Customer_, _WikiPage_, _Account_ or _AdressParser_. Avoid words like _Manager_, _Processor_ or _Data_.

```java
ValidatorOfParameters // bad
ParametersValidator // good
```

###Method Names
Methods should have verb or verb phrase names like _postPayment_, _deletePage_, or _save_. 

Accessors, mutators and predicates should be named for their value and prefixed with _get_, _set_ and _is_.

When constructor are overloaded, use static factory methods with names that describe the arguments and hide (make private the constructors). For example,

```java
Complex fulcrumPoint = Complex.FromRealNumber(23.0)` 
// is better than 
Complex fulcrumPoint = new Complex(23.0)
```
Example:

```java
private Complex(Double realNumber) {
    this.fulcrumPoint = realNumber;
}
static Complex FromRealNumber(Double realNumber) {
    return new Complex(realNumber);
}
```

###Pick one word per concept
What is the difference between *fetch*, *retrieve* and *get*? What is the difference between a *DeviceManager* and a *ProtocolController*? The name leads you to expect two objects that have very different type as well as having different classes.

If I need to differentiate between *MacAdress*, *PortAdress* and *WebAdress* I might consider using MAC and URI for names.

#<a name='functions'>Functions ⚒</a>

Functions should be **small** and then, they should be **smaller** than that.

>*Every function in this program was just two, or three, or four lines long. Each was transparently obvious. Each told a story. And each led you to the next in a compelling order.*

That's how short your functions should be!

###Blocks and Identing

A long condition or the block of code that it's been executed inside a *for* block should be a function call. You keep the function small and also documents and facilitate the reading making a descriptive name.

```java
// BAD
if (!new File(files.getPath() + File.separator + GET_RESERVATION_PATH_PREFIX + identificator + 
".xml").exists()) {

// GOOD
if (recordLocatorFileExists(recordLocator)) {}
```
###Do one thing

And this thing should be in the same level of abstraction. One way to know if a function is doing more than one thing, is if you can extract another function from it with a name that is not merely a restatement of its implementations.

###Common monadic forms

They are the forms to call a method. 

* **Asking** a question:

```java
boolean fileExists("myFile.txt");
```

* Or you may be operating on that argument, **tranforming** it into something else and returning it:

```java
InputStream fileOpen("myFile.txt");
```

* A less common is an **event**. In this form there is an input argument but no output argument. The argument is used to alter the state of the system:

```java
void passwordAttemptFailedNTimex(int attempt)
```

* If a function is going to transform its input argument, the transformation should appear as the return value because will follow the rule of the transformation:

```java
// BAD
void transform(StringBuffer out)

//GOOD
StringBuffer transform(StringBuffer in)
```

###Number of arguments

Avoid methods with too many parameters. Sometimes is easy to mistaken using `assertEquals(expected, actua)`, so imagine methods with a big number of arguments...

###Argument objects

If you have a method that the parameters could be extract in a new object, don't be afraid to do it. Like

```java
private void buildRequestParameters(String applicationId, String flowId, String trackId)
```
###Verbs and keywords

`write(name)` is very evocative. Always try to link the name of the function with the parameter's name.

```java
// BAD
assertEquals(expected, actual);
// GOOD
assertExpectedEqualsActual(expected, actual);

// BAD
private boolean isNotInfantPassenger(Passenger passenger)
// GOOD
private boolean isNotInfant(Passenger passenger)
```

###Have no side effects. A function should do only one thing!
###Prefer exceptions to returning error codes
Is easy to just catch an exception than verify a lot of conditions.


#<a name='comments'>Comments 🗣</a>
Explain yourself in code:

```java
// Check to see if the employee is eligible for full benefits
if ((employee.flags & HOURLY_FLAG) && employee.age > 65))

if (employee.isEligibleFOrFullBenefits())
```
 
#<a name='formatting'>Formatting 🙌</a>

* variables should be declared in the begin of the method or in the begin of a block
* caller’s method should be above called methods
* first, group the methods by affinity (do similar things) and then use the order of the calls (if it is what is happening to reorder then)
* team rules (talk to your team to know the better patterns that fits with you)

```java
for(Segment segment : segments) {
	if(segment.isInOperationalWindow()) {
        return segment;
    }
}
// spaces or not after 'for'??? Follow the language rules
// http://www.oracle.com/technetwork/java/codeconventions-150003.pdf
```

#<a name='objectsAndDataStructures'>Objects and Data Structures 🔝</a>

```java
public class Point {
    public double x;
    public double y;
}
```
```java
public interface Point {
    double getX();
    double getY();
    void setCartesian(double x, double y);
    double getR();
    double getTheta();
    void setPolar(double r, double theta);
}
```

In the second one is necessary to set the coordinates together as an atomic operation. For the first one you can manipulate the data independently, this exposes implementation.

We want to express our data in abstract terms.

Objects hide their data behind abstractions and expose functions that operate on that data. Data structure expose their data and have no meaningful functions.

##Data/Object Anti-Symmetry

```java
public class Square {    public Point topLeft;    public double side;}
public class Rectangle {    public Point topLeft;    public double height;    public double width;}public class Circle {    public Point center;    public double radius;}public class Geometry {    public final double PI = 3.141592653589793;    public double area(Object shape) throws NoSuchShapeException {        if (shape instanceof Square) {            Square s = (Square)shape;            return s.side * s.side;        } else if (shape instanceof Rectangle) {            Rectangle r = (Rectangle)shape;            return r.height * r.width;        } else if (shape instanceof Circle) {            Circle c = (Circle)shape;            return PI * c.radius * c.radius;        }        throw new NoSuchShapeException();    }
}     
```

If I add a new method, *perimeter()*, in *Geometry*, all the classes would be unnafected. But if I add a new shape, all the methods in *Geometry* would be necessary to changed.

```java
public class Square implements Shape {    private Point topLeft;    private double side;    public double area() {        return side*side;    }}public class Rectangle implements Shape {    private Point topLeft;    private double height;    private double width;    public double area() {        return height * width;    }}
```

If I do this, when a new method is add in *Shape*, all the other classes also need to be changed.

>Procedural code (code using data structure) makes it easy to add new functions without changing the existing data structure. OO code, on the other hand, makes it easy to add new classes without changing existing functions.

The complement is also true:

>Procedural code makes it hard to add new data structures because all the functions must change. OO code makes it hard to add new functions because all the classes must change.

## Law of Demeter 👴🏿

Objects should hide their data and expose operations. The Law of demeter says that **a method f, inside a class C should only call the methods of these**:

* C
* An object created inside the method f
* An object passed as an argument to f
* An object held in a instance variable of C

*Talk to friends, not to strangers.*

```java
// BAD
final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();
```

###Train Wrecks

```java
// GOOD
Options opts = ctxt.getOptions();
File scratchDir = opts.getScratchDir();
final String outputDir = scratchDir.getAbsolutePath();
```

If Options and File are objects, then is obviously they are violating the Law of Demeter. If they are just data structure, then this doesn't apply.

###DON'T DO HYBRID STRUCTURE BETWEEN OBJECTS AND DATA STRUCTURES! 🚨

###Hiding Structure

Why did we want the absolute path of the scratch directory?? What were we going to do with it? **Probably to create a scratch file.**

So we should be telling **ctxt** to do something. We should not be asking it about its internals.

```java
BufferedOutputStream bos = ctxt.createScratchFileStream(classFileName);
```

This alows **ctxt** to hide its internals and prevents the current function from having to violate the Law of Demeter by navigating throught objects it shouldn't know about.

###Data Transfer Objects (DTO)

Class with public variables (or getters) and no functions. Is the first stage of translation stage that convert raw data into objects (responses from databases, apis, soaps).

###Conclusion

Objects expose behavior and hide data. This makes it easy to add new kinds of objects without changing existing behaviors. It also makes hard to add new behaviors to existing objects.

Data structures expose data and have no significant behavior. This makes easy to add new behavior to existing data structures but makes it hard to add new data structures to existing functions.

#<a name='errorHandling'> Error Handling</a>





