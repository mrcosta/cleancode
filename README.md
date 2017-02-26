#Clean Code 🤖

* You will not make the deadline by making the mess, but the contrary
* A programmer with code sense will take a look on a messy and know what to do to fix that
* Bad code tempt the mess to grow
* Clean Code is focused
* Clean code is code that was made by someone that cares. You can try to change and will can’t do it
* It is the programmer that make the language look simple
* Make it easier to read, to make it easier to write
* Leave the campground cleaner than you found it

#Naming 👀

* get is not different than retrieve, so stick with one and keep the pattern
* names should reveal intent
* choosing good names takes time but saves more than it takes
* change the names when you find better ones

```java
// good
setSameELigibilityStatusForAllPassengerIfNecessary
hasEligibilityStatusThatImpactsWholeReservation
```
The name of a variable, function, or class, should answer all the big questions. It should tell you why exists, what it does, and how it is used.

```java
// bad
private boolean shouldSearchByTicketNumbers(List<String> ticketNumbers) {
    return ticketNumbers != null && ticketNumbers.size() > 0 && ticketNumbers.size() <= 4;
}
// why this logic exists? 
```
```java for(Segment segment1 : pnr.getSegments())```
 
 ```java
 List<String> editList =  acsPassengerSecurityRSACS.getPassengerInfoResponseList().getPassengerInfoResponse().get(0).getEditCodeList().getEditCode();
 // bad: should be editCodes
 ```
 
#Identation 🙌
 ```java
for(Segment segment : segments) {
	if(segment.isInOperationalWindow()) {
        return segment;
    }
}
// spaces or not after 'for'??? Follow the language rules
// http://www.oracle.com/technetwork/java/codeconventions-150003.pdf 
```
