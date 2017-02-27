## <a name='TOC'>Table of Contents</a>

1. [Clean Code](#cleanCode)
2. [Naming](#naming)
3. [Functions](#functions)
4. [Comments](#comments)
5. [Formatting](#formatting)

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


#<a name='comments'>Comments 🗣</a>
 
#<a name='formatting'>Formatting 🙌</a>

```java
for(Segment segment : segments) {
	if(segment.isInOperationalWindow()) {
        return segment;
    }
}
// spaces or not after 'for'??? Follow the language rules
// http://www.oracle.com/technetwork/java/codeconventions-150003.pdf
```

