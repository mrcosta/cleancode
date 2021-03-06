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
11. [Emergence](#emergence)
12. [Concurrency](#concurrency)
13. [Successive Refinement](#successiveRefinement)
14. [JUnit Internals](#junitInternals)
15. [Smells and Heuristics](#smellsAndHeuristics)

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

Separe the system construction from the objects constructions (Dependency Injection)

> Software systems are unique compared to physical systems. Their architectures can grow incrementaly, if we maintain the proper separation of concerns.

Is best to postpone decisions until the last possible moment. This isn't lazy or irresponsible; it let's us make informed choices with the best possible information. A premature decision is a decision made with suboptimal knowledge. We will have that much less customer feedback, mental reflection on the project, and experience with our implementation choices if we decide to soon.

> Standards make it easier to reuse ideas and components. However, creating standards can sometimes take too long for the industry to wait, and some standards lose touch with the real needs of the adopters they are intended to serve.

### System need Domain-Specific Languages

A good DSL minimizes the "communication gap" between a domain concept and the code that implements and also between the developers team and it's stakeholders.

### Use the simplest thing that can possibly work.

# <a name="emergence">Emergence </a> 

Simple design

* Runs all the tests
* Contains no duplication
* Expresses the intent of the programmer
* Minimize the number of classes and methods

## Run all the tests

Systems that aren't testable aren't verifiable. Arguably, a system that cannot be verified should never be deployed.
The more tests we write, the more we'll continue to push toward things that are simpler to test. The more tests we write, more we use principles like DIP or SRP.

## Refactoring

The fact that we have tests eliminates the fear that cleaning up the code will break it!

## No duplication

Because...reasons

## Expressive
It's use to write code that we understand, because at the time we write it we're deep in an understanding of the problem we're trying to solve. Other maintainers of the code are'nt going to have so deep an understanding. The clearer we write our code, the less time others will have to spend understanding it.

### Keep your functions and classes small.

All too often we get our code working and then move on to the next problem without giving sufficient thought to making that code easy for the next person to read. Remember, the most likely next person to read the code will be you. Care is a precious resource.

# <a name="successiveRefinement">Successive Refinement</a>

First write dirty code and then clean it.

Programmers who satisfy themselves with merely working code are behaving unprofessionally. They may fear that they don't have time to improve the structure and design of their code, but I disagree. 
Bad schedules can be redone, bad requirements can be redefined. Bad team dynamics can be repaired. But bad code rots and ferments.

# <a name="junitInternals"> JUnit Internals </a>

Often one refactoring leads to another that leads to the undoing of the first. Refactoring is an interative process full of trial and error, inevitably converging on something that we feel is worthy of a professional.

No module is immune from improvement, and each of us has the responsibility to leave the code a litte better than we found it.

# <a name="smellsAndHeuristics"> Smells and Heuristics </a> 

F1: *Too Many Arguments*: Functions should have a small number of arguments
F2: *Output Arguments*: Readers expect arguments to be inputs, not outputs. If a function must change the state of something, have it change the state of the object its called on.
F3: *Flag Arguments*: Boolean arguments loudly declare that the function does more than one thing.

G3: *Incorrect Behavior at the Boundaries*: Don't rely on your intuition. Look for every boundary condition and write a test for it.

G5: *Duplication*: If you have a lot of if/elses and switchs, these should be replaced with polymorphism.

G6: *Code at wrong level of abstraction*: Isolating abstractions is one of the hardest things that software developers do, and there is no quick fix when you get it wrong.
Try to separate higher level general concepts from lower level detailed concepts.

G8: *Too much information*: Well-defined modules have very small interfaces that allow you to do a lot with a little. Poorly defined modules have wide and deep interfaces that force you to use many different gestures to get simple things done. A well-defined interface does not offer very many functions to depend upon, so coupling is low. A poorly defined interface provides lots of functions that you must call, so coupling is high.
* The fewer methods a class has, the better
* The fewer variables a function knows about, the better. 
* The fewer instance variables a class has, the better.
Be SMALL 

G9: *Dead Code*: Is code that is never executed. Can be found in conditions or try catchs that will never occur.

G10: *Vertical Separation*: variables should be declared near where they are used. The same principle apply to private methods (near its public methods).

G11: *Inconsistency*: if you use some pattern (example: for variables names), stick with it.

G13: *Artificial Coupling*: don't force things to be connected withou specific purposes. Example: enum inside a object and another object using this enum knowing about the object that holds the enum.

G14: *Feature Envy*: one object uses more another object than itself. Probably that method would be better if placed in this another object.

G15: *Selector Arguments*: In general its better to have many functions than to pass some code into a function to select the behavior (avoid boolean params).

avoid things like:

```java
double overtimeRate = overtime ? 1.5 :1.0 * tenthRate;
```

instead, try to create more functions that will split the behavior. And often is possible to use another type (int, enuns) to apply the same intent as the boolean would (sometimes boolean intents something mathematical)

G17: *Misplaced Responsibility*: could should be when makes sense to be (domain driven design) and the same apply for enums, constants...

G18: *Inapropriate Static*: make sure that there is no chance that you'll want the static method to behave polymorphically.

G19: *Use explanatory variables*: use intermediary variables to expose the intent of the calculation or logic that you are implementing.

G20: *Function names should say what they do*

G21: *Understand the algorithm*: before you consider yourself done with a function, make sure you understand how it works (refactoring is also a good approach to reinforce what it does).

G22: *Make logical dependencies physical*: if you are doing some condition to avoid call another object function, is possible that condition (or what you use) should be placed in the object that you would call (if the condition pass) rather than the current object.

```java
if (page.size() == PAGE_SIZE) {
   report.print()
}
```

instead, use:

```java
if (page.size() == report.getMaxPageSize()) {
   report.print()
}
```

G23: *Prefer Polymorphism to if/else or switch/case*

G24: *Follow standard conventions*: talk to your team about the way to indent, to declara variables, to naming functions...

G25: *Replace magic numbers with named constants* 

G26: *Be precise*: do what you need to do given the behavior of the code that you created.

G28: *Encapsulate Conditionals*

G29: *Avoid negative conditionals* 

G30: *Functions should do one thing*

G31: *Hidden Temporal Coupling*: implement in a way that each function produces a result that the next function needs, so there is no reasonable way to call them out of order.

Example:

```java
gradient = saturateGradient()
splines = calculateSplines(gradient)
```

is better than:

```java
gradient = saturateGradient()
splines = calculateSplines() // because in this way is not clear what order you can call the methods
```

G33: *Encapsulate boundary conditions*: to a variable, function...make it clearer

G34: *Functions should descend only one level of abstraction*: separate things better and don't mess code with code that should be in another place.

G36: *Avoind transitive navigation*: we don't want something like 'a.getB().getC().doSomething()' instead, we ant 'myCollaborator.doSomething()'

##JAVA

J2: *Don't hide constants*: always make explicit where they come from

J3: *Use Enums*: they are more powerful than constants alone

##NAMES

N1: *use descriptive names*

N2: *choose names at the Appropriate Level of Abstraction*

N3: *use standard nomenclature where possible* 

N7: *names should describe side-effects* 
