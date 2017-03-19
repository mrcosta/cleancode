## <a name='TOC'>Table of Contents</a>

1. [Clean Code](#cleanCode)
2. [Naming](#naming)
3. [Functions](#functions)
4. [Comments](#comments)
5. [Formatting](#formatting)
6. [Objects and Data Structures](#objectsAndDataStructures)
7. [Error Handling](#errorHandling)
8. [Unit Tests](#unitTests)
9. [Classes](#classes)
10. [Systems](#systems)

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

Don't use noisy words. What is the difference between and **ProductInfo** and **ProductData**? You have made the names different without making them mean anything different.

How is _NameString_ better than name? Would a _name_ ever be a floating point number? If so, it breaks an earlier rule about disinformation.

```java
 List<String> editList =  acsPassengerSecurityRSACS.getPassengerInfoResponseList().
 getPassengerInfoResponse().get(0).getEditCodeList().
 getEditCode();
 // bad: should be editCodes
```

### Class Names

Classes and objects should have nour or noun phrase names like _Customer_, _WikiPage_, _Account_ or _AdressParser_. Avoid words like _Manager_, _Processor_ or _Data_.

```java
ValidatorOfParameters // bad
ParametersValidator // good
```

### Method Names
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

# <a name='functions'>Functions ⚒</a>

Functions should be **small** and then, they should be **smaller** than that.

 > _Every function in this program was just two, or three, or four lines long. Each was transparently obvious. Each told a story. And each led you to the next in a compelling order._ 

That's how short your functions should be!

### Blocks and Identing

A long condition or the block of code that it's been executed inside a *for* block should be a function call. You keep the function small and also documents and facilitate the reading making a descriptive name.

```java
// BAD
if (!new File(files.getPath() + File.separator + GET_RESERVATION_PATH_PREFIX + identificator + 
".xml").exists()) {

// GOOD
if (recordLocatorFileExists(recordLocator)) {}
```
### Do one thing

And this thing should be in the same level of abstraction. One way to know if a function is doing more than one thing, is if you can extract another function from it with a name that is not merely a restatement of its implementations.

### Common monadic forms

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

### Number of arguments

Avoid methods with too many parameters. Sometimes is easy to mistaken using `assertEquals(expected, actua)`, so imagine methods with a big number of arguments...

### Argument objects

If you have a method that the parameters could be extract in a new object, don't be afraid to do it. Like

```java
private void buildRequestParameters(String applicationId, String flowId, String trackId)
```
### Verbs and keywords

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

### Have no side effects. A function should do only one thing!
### Prefer exceptions to returning error codes
Is easy to just catch an exception than verify a lot of conditions.


# <a name='comments'>Comments 🗣</a>
Explain yourself in code:

```java
// Check to see if the employee is eligible for full benefits
if ((employee.flags & HOURLY_FLAG) && employee.age > 65))

if (employee.isEligibleFOrFullBenefits())
```
 
# <a name='formatting'>Formatting 🙌</a>

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

# <a name='objectsAndDataStructures'>Objects and Data Structures 🔝</a>

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

## Data/Object Anti-Symmetry

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

### Train Wrecks

```java
// GOOD
Options opts = ctxt.getOptions();
File scratchDir = opts.getScratchDir();
final String outputDir = scratchDir.getAbsolutePath();
```

If Options and File are objects, then is obviously they are violating the Law of Demeter. If they are just data structure, then this doesn't apply.

### DON'T DO HYBRID STRUCTURE BETWEEN OBJECTS AND DATA STRUCTURES! 🚨

### Hiding Structure

Why did we want the absolute path of the scratch directory?? What were we going to do with it? **Probably to create a scratch file.**

So we should be telling **ctxt** to do something. We should not be asking it about its internals.

```java
BufferedOutputStream bos = ctxt.createScratchFileStream(classFileName);
```

This alows **ctxt** to hide its internals and prevents the current function from having to violate the Law of Demeter by navigating throught objects it shouldn't know about.

### Data Transfer Objects (DTO)

Class with public variables (or getters) and no functions. Is the first stage of translation stage that convert raw data into objects (responses from databases, apis, soaps).

### Conclusion

Objects expose behavior and hide data. This makes it easy to add new kinds of objects without changing existing behaviors. It also makes hard to add new behaviors to existing objects.

Data structures expose data and have no significant behavior. This makes easy to add new behavior to existing data structures but makes it hard to add new data structures to existing functions.

# <a name='errorHandling'> Error Handling ❌</a>

### Use Exceptions rather than return codes

### Create specific exceptions

### Don't return null

When we do this, we are essentially creating work for ourselves and foisting problems upon our callers. All it takes is one missing *null* check to send an application spinning out of control.

What to do?

* Throw an exception
* return a Special Case object

Always return an empty list instead of null.

# <a name='boundaries'> Boundaries 🚷</a>

Nothing to add

# <a name='unitTests'> Unit Tests 〒</a>

The Three Laws of TDD

* You may not write production code until you have a failing test
* You may not write more of a unit test than is sufficient to fail, and not compiling is failing
* You may not write more production code than is sufficient to pass the currently failing test

>Test code is just as important as production code

Tests enable change!

If your tests are dirty, then your ability to change your code is hampered, and you begin to lose the ability to improve the structure of that code. The dirtier your tests, the dirtier your code becomes.

READABILITY, READABILITY AND READABILITY!

Create a test API. Something that makes easier to read your tests. Builders and custom asserts are very specific for this.

Assert one concept per test

### FIRST

* **F**ast: Tests should be fast.
* **I**ndependent: Tests should not depend on each other. One test should not set up the conditions for the next other. And them should run in any order you prefer.
* **R**epeatable: They should run in any environment whithout failing
* **S**elf-Validating: they should have an boolean output. To make sure that a test was succesful should be not necessary to look a log file or compare two files.
* **T**imely: tests should be write just before production code. Will be hard to test after that you are in production.

# <a name='classes'>Classes 👯</a>

* We count responsibilities to check if a class is too big
* The name of a class should describe what responsibilities if fulfills
* If we cannot derive a concise name for a class, then it's likely too large
* The more ambiguous the class name, the more likely it has too many responsibilities
* *Processor, Manager or Super* often hint at unfortunate aggregation of responsibilities

We should also be able to write a brief description of the class in about 25 words without using the words *if*, *and*, *or* or *but*.

**Classes should have one responsibility. One reason to change.**

Maintaning a separation of concerns is just as important in our programming activities as it is in our programs.

Many developers fear that a large number of small, single-purpose classes make it more difficult to understand the bigger picture. They are concerned that they must navigate from class to class in order to figure out how a larger piece of work gets accomplished.

However, a system with many small classes has no more moving parts than a system with a few large classes. There is just as much to learn in the system with a few large classes. So the question is: *Do you want your tools organized into toolboxes with many small drawers each containing well-defined and well-labeled components? Or do you want a few drawers that you just toss everything into?*

## Cohesion

* Classes should have a small number of instance variables
* In general, the more instance variables a method manipulates the more cohesive that method is to its class. 
* A class in which each variable is used by each method is maximally cohesive
* We would like to cohesion to be high
* When cohesion is high, it means that the methods and variables of the class are co-dependent and hang together as a logical whole

Example of a cohesive class:

```java
public class Stack {    private int topOfStack = 0;    List<Integer> elements = new LinkedList<Integer>();    
    public int size() {        return topOfStack;    }    
    public void push(int element) {        topOfStack++;        elements.add(element);    }    
    public int pop() throws PoppedWhenEmpty {        if (topOfStack == 0)            throw new PoppedWhenEmpty();        int element = elements.get(--topOfStack);        elements.remove(topOfStack);        return element;    }}
```

When some instance variables are been used just for some methods in the class, that means that there is another class trying to get out of the larger class.

You should try to separate the variables and methods into more classes such the new classes are more cohesive.

## Organizing for Change

Change is continual.

```java
public class Sql {    public Sql(String table, Column[] columns)    public String create()    public String insert(Object[] fields)    public String selectAll()    public String findByKey(String keyColumn, String keyValue)    public String select(Column column, String pattern)    public String select(Criteria criteria)    public String preparedInsert()    private String columnList(Column[] columns)    private String valuesList(Object[] fields, final Column[] columns)    private String selectWithCriteria(String criteria)    private String placeholderList(Column[] columns)}
```
The Sql class must change when we add a new type of statement. It also must change when we alter the details of a single statement type—for example, if we need to modify the select functionality to support subselects. These two reasons to change mean that theSql class violates the SRP.

We can spot this SRP violation from a simple organizational standpoint.

Private methods that are used only to a few public methods is a sympthom that this public method could be extracted to a new class.

Should be better this way:

```java
abstract public class Sql {    public Sql(String table, Column[] columns)    abstract public String generate();}public class CreateSql extends Sql {    public CreateSql(String table, Column[] columns)    @Override public String generate()}public class SelectSql extends Sql {    public SelectSql(String table, Column[] columns)    @Override public String generate()}public class InsertSql extends Sql {    public InsertSql(String table, Column[] columns, Object[] fields)    @Override public String generate()    private String valuesList(Object[] fields, final Column[] columns)}
```

**Open Closed Principle**: Classes should be open for extension but closed for modification. The last example is open to allow new functionality via subclassing, but we can make this change while keeping every other class closed. In a ideal system, we incorporate new features by extending the system, not by making modifications to existing code.

# <a name='systems'>Systems 💻</a>










