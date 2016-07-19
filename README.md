1.    Cocoa.
Cocoa is an application environment for both the Mac OS X operating system and iOS.  It consists of a suite of object-oriented software libraries, a runtime system, and an integrated development environment. Carbon is an alternative environment in Mac OS X, but it is a compatibility framework with procedural programmatic interfaces intended to support existing Mac OS X code bases.

2.     Frameworks that make Cocoa.
·       Appkit (Application Kit)
·       Foundation

3.     Objective-C.
Objective-C is a very dynamic language. Its dynamism frees a program from compile-time and link-time constraints and shifts much of the responsibility for symbol resolution to runtime, when the user is in control. Objective-C is more dynamic than other programming languages because its dynamism springs from three sources:
·         Dynamic typing—determining the class of an object at runtime
·         Dynamic binding—determining the method to invoke at runtime
·         Dynamic loading—adding new modules to a program at runtime

4.     Objective-C vs C/C++.
·       The Objective-C class allows a method and a variable with the exact same name. In C++, they must be different.
·       Objective-C does not have a constructor or destructor. Instead it has init and dealloc methods, which must be called explicitly.
·       Objective-C uses + and - to differentiate between class method (known as factory method in Java) and instance methods, C++ uses static to specify a factory method.
·       Multiple inheritance is not allowed in Obj-C, however we can use protocol to some extent.
·       Obj-C has runtime binding leading to dynamic linking.
·       Obj-C has categories.
·       Objective-C has a work-around for method overloading, but none for operator overloading.
·       Objective-C also does not allow stack based objects. Each object must be a pointer to a block of memory.
·       In Objective-C the message overloading is faked by naming the parameters. C++ actually does the same thing but the compiler does the name mangling for us. In Objective-C, we have to mangle the names manually. If you go in deep you will see a complete method names are as : `addA:withB:` which is a selector and `:` is used for parameter.
·       One of C++'s advantages and disadvantages is automatic type coercion.
·       Another feature C++ has that is missing in Objective-C is references. Because pointers can be used wherever a reference is used, there isn't much need for references in general.
·       Templates are another feature that C++ has that Objective-C doesn't. Templates are needed because C++ has strong typing and static binding that prevent generic classes, such as List and Array. 

5.     Appilcation Kit/App kit.
The Application Kit is a framework containing all the objects you need to implement your graphical, event-driven user interface: windows, panels, buttons, menus, scrollers, and text fields. The Application Kit handles all the details for you as it efficiently draws on the screen, communicates with hardware devices and screen buffers, clears areas of the screen before drawing, and clips views.
You also have the choice at which level you use the Application Kit:
·         Use Interface Builder to create connections from user interface objects to your application objects.
·         Control the user interface programmatically, which requires more familiarity with AppKit classes and protocols.
·         Implement your own objects by subclassing NSView or other classes.

6.   Foundation Kit.
The Foundation framework defines a base layer of Objective-C classes. In addition to providing a set of useful primitive object classes, it introduces several paradigms that define functionality not covered by the Objective-C language. The Foundation framework is designed with these goals in mind:
·         Provide a small set of basic utility classes.
·         Make software development easier by introducing consistent conventions for things such as deallocation.
·         Support Unicode strings, object persistence, and object distribution.
·         Provide a level of OS independence, to enhance portability.

7.     Dynamic and Static Typing.
Static typed languages are those in which type checking is done at compile-time, whereas dynamic typed languages are those in which type checking is done at run-time.
Objective-C is a dynamically-typed language, meaning that you don't have to tell the compiler what type of object you're working with at compile time. Declaring a type for a varible is merely a promise which can be broken at runtime if the code leaves room for such a thing. You can declare your variables as type id, which is suitable for any Objective-C object.

8.     Selectors
In Objective-C, selector has two meanings. It can be used to refer simply to the name of a method when it’s used in a source-code message to an object. It also, though, refers to the unique identifier that replaces the name when the source code is compiled. Compiled selectors are of type SEL. All methods with the same name have the same selector. You can use a selector to invoke a method on an object—this provides the basis for the implementation of the target-action design pattern in Cocoa.
[friend performSelector:@selector(gossipAbout:) withObject:aNeighbor];
is equivalent to:
[friend gossipAbout:aNeighbor];

9.     Class Introspection
·         Determine whether an objective-C object is an instance of a class
        [obj isMemberOfClass:someClass];
·         Determine whether an objective-C object is an instance of a class or its descendants
        [obj isKindOfClass:someClass];
·         The version of a class
        [MyString version]
·         Find the class of an Objective-C object
        Class c = [obj1 class]; Class c = [NSString class];
·         Verify 2 Objective-C objects are of the same class
[obj1 class] == [obj2 class]

10. Immutable vs Mutable
Immutable objects cant be changed. However they are just pointing to some location where stored values are made constant. You can change that reference to other location.  You can change the value of  mutable objects.

11. Category
In Objective-C, new functionality can be added to existing classes by adding a new category. Shared libraries that depend on a base class that has been extended will continue to work, and new classes created can call the additional methods. Category on NSString will become available on NSMutableString.
We can add new ivar to a category using these: (It is required when we have APIs of some other, don’t have code)
@interface NSFruit (Liking)
@property ( nonatomic ) BOOL liked ;
@end

@implementation NSFruit (Liking)
-(BOOL)liked{
    return [ objc_getAssociatedObject( self, "_abliked" ) boolValue ] ;
}
-(void)setLiked:(BOOL)b{
objc_setAssociatedObject(self, "_abliked",  [ NSNumber numberWithBool:b ], OBJC_ASSOCIATION_RETAIN_NONATOMIC ) ;
}
@end

12. Proxy
As long as there aren't any extra instance variables, any subclass can proxy itself as its superclass with a single call. Each class that inherits from the superclass, no matter where it comes from, will now inherit from the proxied subclass. Calling a method in the superclass will actually call the method in the subclass. For libraries where many objects inherit from a base class, proxying the superclass can be all that is needed.

13. Category vs Inheritance
Category allows adding methods only; no data members can be added as in Inheritance both data and methods can be added. Category’s scope is full application whereas inheritance’s scope that particular file. However in new compilers using associatedObjects you can add data members using category.

14. Why category is better than inheritance?
       If category is used, you can use same class, no need to remember a new class-name. Category created on a base class is available on sub classes.

15. Fast enumeration
Fast enumeration is a language feature that allows you to enumerate over the contents of a collection. (Your code will also run faster because the internal implementation reduces message send overhead and increases pipelining potential.)
Enum is preferred over loop for the same reason.

16. Protocol
·  A Protocol in Objective-C is identical in functionality to an interface in Java, or a purely virtual class in C++.
·  A protocol is means to define a list of required and/or optional methods that a class implements. If a class adopts a protocol, it must implement all required methods in the protocols it adopts.
·  Cocoa uses protocols to support interprocess communication through Objective-C messages. In addition, since Objective-C does not support multiple inheritance, you can achieve similar functionality with protocols, as a class can adopt more than one protocol.
·  A good example of a protocol is NSCoding, which has two required methods that a class must implement. This protocol is used to enable classes to be encoded and decoded, that is, archiving of objects by writing to permanent storage.

17. Formal Protocols
Formal Protocols allow us to define the interface for a set of methods, but implementation is not done. Formal Protocols are useful when you are using DistributedObjects, because they allow you to define a protocol for communication between objects, so that the DO system doesn't have to constantly check whether or not a certain method is implemented by the distant object.

18. Formal vs informal protocol.
In addition to formal protocols, you can also define an informal protocol by grouping the methods in a category declaration:
@interface NSObject (MyProtocol)
        //someMethod();
@end
Informal protocols are typically declared as categories of the NSObject class, because that broadly associates the method names with any class that inherits from NSObject. Because all classes inherit from the root class, the methods aren’t restricted to any part of the inheritance hierarchy. (It is also possible to declare an informal protocol as a category of another class to limit it to a certain branch of the inheritance hierarchy, but there is little reason to do so.)
When used to declare a protocol, a category interface doesn’t have a corresponding implementation. Instead, classes that implement the protocol declare the methods again in their own interface files and define them along with other methods in their implementation files.
An informal protocol bends the rules of category declarations to list a group of methods but not associate them with any particular class or implementation.
Being informal, protocols declared in categories don’t receive much language support. There’s no type checking at compile time nor a check at runtime to see whether an object conforms to the protocol. To get these benefits, you must use a formal protocol. An informal protocol may be useful when all the methods are optional, such as for a delegate, but (in Mac OS X v10.5 and later) it is typically better to use a formal protocol with optional methods.
19. Protocol's two types : @optional vs @required
Protocol methods can be marked as optional using the @optional keyword. Corresponding to the @optional modal keyword, there is a @required keyword to formally denote the semantics of the default behavior. You can use @optional and @required to partition your protocol into sections as you see fit. If you do not specify any keyword, the default is @required.
                @protocol MyProtocol
                                @optional
                                                -(void) optionalMethod;
                                @required
                                                -(void) requiredMethod;
                @end

20. Memory Management
      In MRC or for Foundation variables like CG... , CF...:
If you alloc, retain, or copy/mutablecopy it, it's your job to release/autorelease it. Otherwise it isn't.
In ARC, for Foundation varialbes you need to release/autoreleast it. For others(NS... or subclass from NS...) no need to release/autorelease.

21. Retain Counting
Every object has a RetainCount that goes up by one when the object gets a retain message. It goes down by one when the object gets a release message. When the RetainCount reaches 0, the object will call [self dealloc], thereby releasing the object's memory.

22. Copy vs assign vs retain
·         Assign is for primitive values like BOOL, NSInteger or double. For objects use retain or copy, depending on if you want to keep a reference to the original object or make a copy of it.
·         assign: In your setter method for the property, there is a simple assignment of your instance variable to the new value, eg:
(void)setString:(NSString*)newString{  
        string = newString;
 }
This can cause problems since Objective-C objects use reference counting, and therefore by not retaining the object, there is a chance that the string could be deallocated whilst you are still using it.
·         retain: this retains the new value in your setter method. For example:
This is safer, since you explicitly state that you want to maintain a reference of the object, and you must release it before it will be deallocated.
(void)setString:(NSString*)newString{  
        [newString retain];  
          [string release];    
 string = newString; 
}
·         copy: this makes a copy of the string in your setter method:
This is often used with strings, since making a copy of the original object ensures that it is not changed whilst you are using it.
(void)setString:(NSString*)newString{    
         if(string!=newString){      
                        [string release];      
                        string = [newString copy];    
         }
 }

23. alloc vs new
“alloc” creates a new memory location but doesn’t initializes it as compared to “new”.

24. release vs pool drain
“release” frees a memory. “drain” releases the NSAutoreleasePool itself.

25. NSAutoReleasePool : release vs drain
Strictly speaking, from the big picture perspective drain is not equivalent to release:
In a reference-counted environment, drain does perform the same operations as release, so the two are in that sense equivalent. To emphasise, this means you do not leak a pool if you use drain rather than release.
In a garbage-collected environment, release is a no-op. Thus it has no effect. drain, on the other hand, contains a hint to the collector that it should "collect if needed". Thus in a garbage-collected environment, using drain helps the system balance collection sweeps.

26. autorelease vs release
Autorelase: By sending an object an autorelease message, it is added to the local AutoReleasePool, and you no longer have to worry about it, because when the AutoReleasePool is destroyed (as happens in the course of event processing by the system) the object will receive a release message, its RetainCount will be decremented, and the GarbageCollection system will destroy the object if the RetainCount is zero.
Release: retain count is decremented at this point.

27. Autorelease Pool
Autorelease pools provide a mechanism whereby you can send an object a “deferred” release message. This is useful in situations where you want to relinquish ownership of an object, but want to avoid the possibility of it being deallocated immediately (such as when you return an object from a method). Typically, you don’t need to create your own autorelease pools, but there are some situations in which either you must or it is beneficial to do so.

28. How autorelease pool is managed.
Every time -autorelease is sent to an object, it is added to the inner-most autorelease pool. When the pool is drained, it simply sends -release to all the objects in the pool.
Autorelease pools are simply a convenience that allows you to defer sending -release until "later". That "later" can happen in several places, but the most common in Cocoa GUI apps is at the end of the current run loop cycle.

29.  Memory Leak
If RetainingAndReleasing are not properly used then RetainCount for AnObject doesn’t reach 0. It doesn’t crash the application.

30. Event Loop
In a Cocoa application, user activities result in events. These might be mouse clicks or drags, typing on the keyboard, choosing a menu item, and so on. Other events can be generated automatically, for example a timer firing periodically, or something coming in over the network. For each event, Cocoa expects there to be an object or group of objects ready to handle that event appropriately. The event loop is where such events are detected and routed off to the appropriate place. Whenever Cocoa is not doing anything else, it is sitting in the event loop waiting for an event to arrive. (In fact, Cocoa doesn't poll for events as suggested, but instead its main thread goes to sleep. When an event arrives, the OS wakes up the thread and event processing resumes. This is much more efficient than polling and allows other applications to run more smoothly).
Each event is handled as an individual thing, then the event loop gets the next event, and so on. If an event causes an update to be required, this is checked at the end of the event and if needed, and window refreshes are carried out.

31. @property  @synthesize @dyanamic
·       Properties are a feature in Objective-C that allow us to automatically generate accessors
·       The @synthesize directive automatically generates the setters and getters for us, so all we have to implement for this class is the dealloc method. 
·       @synthesize will generate getter and setter methods for your property. @dynamic just tells the compiler that the getter and setter methods are implemented not by the class itself but somewhere else (like the superclass)
·       Uses for @dynamic are e.g. with subclasses of NSManagedObject (CoreData) or when you want to create an outlet for a property defined by a superclass that was not defined as an outlet:

32. @property vs @synthesize
@property - declares a property.
@synthesize - creates getter and setter methods for a property
Example:
       @property float value;
 is equivalent to:
        -(float)value;
        - (void)setValue:(float)newValue;
@synthesize defines the properties.


33. Relation between iVar and @property.
iVar are just instance variables. It cant be accessed unless we create accessors, which are generated by @property. iVar and its counterpart @property can be of different names.
@interface Box : NSObject{
    NSString *boxName;
}
@property (strong) NSString *boxDescription;//this will become another ivar
-(void)aMethod;
@end
@implementation Box
@synthesize boxDescription=boxName;//now boxDescription is accessor for name
-(void)aMethod {
    NSLog(@"name=%@", boxName);
     NSLog(@"boxDescription=%@",self.boxDescription);
    NSLog(@"boxDescription=%@",boxDescription); //throw an error
}
@end

34. Differnce between boxName and self.boxName.
boxName: Accessing directly.
self. boxName: Accessing boxName through accessors. If property/synthesize is not there it will throw error.

35. What it does “@synthesize boxDescription=boxName;”  ?
Here you can use boxName or self.boxName. We cant use boxDescription.

36. atomic vs nonatomic
@property(atomic, retain)……. 
@property(retain)…….
@property(nonatomic, retain)…….
atomic is the default behavior, so first and second are same.
Assuming that you are @synthesizing the method implementations, atomic vs. non-atomic changes the generated code. If you are writing your own setter/getters, atomic/nonatomic/retain/assign/copy are merely advisory.
With atomic, the synthesized setter/getter will ensure that a whole value is always returned from the getter or set by the setter, regardless of setter activity on any other thread. That is, if thread A is in the middle of the getter while thread B calls the setter, an actual viable value -- an autoreleased object, most likely -- will be returned to the caller in A.
In nonatomic, no such guarantees are made. Thus, nonatomic is considerably faster than atomic.
What atomic does not do is make any guarantees about thread safety. If thread A is calling the getter simultaneously with thread B and C calling the setter with different values, thread A may get any one of the three values returned -- the one prior to any setters being called or either of the values passed into the setters in B and C. Likewise, the object may end up with the value from B or C, no way to tell.
Ensuring data integrity -- one of the primary challenges of multi-threaded programming -- is achieved by other means.

37. Collection
In Cocoa and Cocoa Touch, a collection is a Foundation framework class used for storing and managing groups of objects. Its primary role is to store objects in the form of either an array, a dictionary, or a set.

38. Threads and how to use
Use this class when you want to have an Objective-C method run in its own thread of execution. Threads are especially useful when you need to perform a lengthy task, but don’t want it to block the execution of the rest of the application. In particular, you can use threads to avoid blocking the main thread of the application, which handles user interface and event-related actions. Threads can also be used to divide a large job into several smaller jobs, which can lead to performance increases on multi-core computers.
Two ways to create threads…
·         detachNewThreadSelector:toTarget:withObject:
·         Create instances of NSThread and start them at a later time using the “start” method.
NSThread is not as capable as Java’s Thread class, it lacks
·         Built-in communication system.
·         An equivalent of “join()”

39.Threadsafe
When it comes to threaded applications, nothing causes more fear or confusion than the issue of handling signals. Signals are a low-level BSD mechanism that can be used to deliver information to a process or manipulate it in some way. Some programs use signals to detect certain events, such as the death of a child process. The system uses signals to terminate runaway processes and communicate other types of information.
The problem with signals is not what they do, but their behavior when your application has multiple threads. In a single-threaded application, all signal handlers run on the main thread. In a multithreaded application, signals that are not tied to a specific hardware error (such as an illegal instruction) are delivered to whichever thread happens to be running at the time. If multiple threads are running simultaneously, the signal is delivered to whichever one the system happens to pick. In other words, signals can be delivered to any thread of your application.
The first rule for implementing signal handlers in applications is to avoid assumptions about which thread is handling the signal. If a specific thread wants to handle a given signal, you need to work out some way of notifying that thread when the signal arrives. You cannot just assume that installation of a signal handler from that thread will result in the signal being delivered to the same thread.

40. Which one is thread-safe-atomic or non-atomic?
Immutable objects are generally threadsafe. E.g, NSString
None are threadsafe.
atomic guarantees atomic access to the variable but it DOESN'T make your code thread safe. Neither does non-atomic.
With "atomic", the synthesized setter/getter methods will ensure that a whole value is always returned from the getter or set by the setter, regardless of setter activity on any other thread. So if thread A is in the middle of the getter while thread B calls the setter, an actual viable value will be returned to the caller in A. For nonatomic, you have no such guarantees.

41. @synchronized
Objective-C supports multithreading in applications. Therefore, two threads can try to modify the same object at the same time, a situation that can cause serious problems in a program. To protect sections of code from being executed by more than one thread at a time, Objective-C provides the @synchronized() directive.
The @synchronized()directive locks a section of code for use by a single thread. Other threads are blocked until the thread exits the protected code—that is, when execution continues past the last statement in the @synchronized() block.
The @synchronized() directive takes as its only argument any Objective-C object, including self. This object is known as a mutual exclusion semaphore or mutex. It allows a thread to lock a section of code to prevent its use by other threads. You should use separate semaphores to protect different critical sections of a program. It’s safest to create all the mutual exclusion objects before the application becomes multithreaded, to avoid race conditions.
 (void)criticalMethod{
                          @synchronized(self) {
                                              // Critical code.
         }
}

42. MVC
It is useful to divide the complex task of computer application design into domains in order to simplify the process. Object oriented approaches are modular in philosophy, so the Model View Controller design pattern is a popular way to make logical divisions among class responsibilities.
Each object oriented programming environment/language has a slightly different definition/convention of MVC.
The main advantage of adopting a design pattern like MVC is that it allows the code in each unit to be decoupled from the others, making it more robust and immune to changes in other code.
Within the scope of Cocoa, MVC is an extremely important pattern. The major enhancements that Apple have made to Cocoa, namely Bindings and Core Data, are manifestly based on the MVC pattern.
Model: A Model object:
·         is usually a simple subclass of NSObject (or an instance of NSManagedObject for CoreData)
·         has a set of instance variables in which to store its data
·         has a series of accessor methods for those ivars
·         has one or more init: methods to return new instances to other classes
·         has a dealloc method
·         may have custom methods to manipulate the model objects internal data
·         is frequently reusable
View: A View object:
·         is some subclass of NSView
·         contains a drawRect: method which is the basis of all drawing
·         is rarely subclassed or modified
·         makes extensive use of delegates for customisation
·         is generally reusable
Controller: A Controller object:
·         mediates between model and view
·         is usually a subclass of NSObject
·         contains the outlets and actions for IB
·         contains ivars and collections to own and hold model objects
·         has methods for manipulating and composing model objects
·         contains the main awakeFromNib method
·         is instantiated in the nib file/s
·         contains the business logic of the program
·         is rarely reusable

43. Application lifecycle
Chronology of an application: When the process is started, it runs the NSApplicationMain function, which creates an instance of NSApplication. The application object reads the main nib file and unarchives the objects inside. The objects are all sent the message awakeFromNib. Then the application object checks for events.
This lifecylce of a typical cocoa application is depicted in the below diagram.

44. NSBundle
An NSBundle object represents a location in the file system that groups code and resources that can be used in a program. NSBundle objects locate program resources, dynamically load and unload executable code, and assist in localization. You build a bundle in Xcode using one of these project types: Application, Framework, plug-ins.

45. Delegate
The delegation is a commonly used pattern in object-oriented programming. It is a situation where an object, instead of performing a tasks itself, delegates that task to another, helper object. The helper object is called the delegate.
A delegate allows one object to send messages to another object when an event happens.
A delegate is just an object that another object sends messages to when certain things happen, so that the delegate can handle app-specific details the original object wasn't designed for. It's a way of customizing behavior without subclassing.
They are never retained.

46. Notification and Observers
A notification is a message sent to one or more observing objects to inform them of an event in a program. The notification mechanism of Cocoa follows a broadcast model. It is a way for an object that initiates or handles a program event to communicate with any number of objects that want to know about that event. These recipients of the notification, known as observers, can adjust their own appearance, behavior, and state in response to the event. The object sending (or posting) the notification doesn’t have to know what those observers are. Notification is thus a powerful mechanism for attaining coordination and cohesion in a program. It reduces the need for strong dependencies between objects in a program (such dependencies would reduce the reusability of those objects). Many classes of the Foundation, AppKit, and other Objective-C frameworks define notifications that your program can register to observe.
The centerpiece of the notification mechanism is a per-process singleton object known as the notification center (NSNotificationCenter). When an object posts a notification, it goes to the notification center, which acts as a kind of clearing house and broadcast center for notifications. Objects that need to know about an event elsewhere in the application register with the notification center to let it know they want to be notified when that event happens. Although the notification center delivers a notification to its observers synchronously, you can post notifications asynchronously using a notification queue (NSNotificationQueue).

47. Delegate vs Notification
·       The concept of notification differs from delegation in that it allows a message to be sent to more than one object. It is more like a broadcast rather than a straight communication between two objects. It removes dependencies between the sending and receiving object(s) by using a notification center to manage the sending and receiving of notifications. The sender does not need to know if there are any receivers registered with the notification center. There can be one, many or even no receivers of the notification registered with the notification center. Simply, Delegate is 1-to-1 object and Notification can be *-to-* objects.
·       The other difference between notifications and delegates is that there is no possibility for the receiver of a notification to return a value to the sender.
·       Typical uses of notifications might be to allow different objects with an application to be informed of an event such as a file download completing or a user changing an application preference. The receiver of the notification might then perform additional actions such as processing the downloaded file or updating the display.

48. Plist
Property lists organize data into named values and lists of values using several object types. These types give you the means to produce data that is meaningfully structured, transportable, storable, and accessible, but still as efficient as possible. Property lists are frequently used by applications running on both Mac OS X and iOS. The property-list programming interfaces for Cocoa and Core Foundation allow you to convert hierarchically structured combinations of these basic types of objects to and from standard XML. You can save the XML data to disk and later use it to reconstruct the original objects.
The user defaults system, which you programmatically access through the NSUserDefaults class, uses property lists to store objects representing user preferences. This limitation would seem to exclude many kinds of objects, such as NSColor and NSFont objects, from the user default system. But if objects conform to the NSCoding protocol they can be archived to NSData objects, which are property list–compatible objects

49. Responder Chain and First Responder
A ResponderChain is a hierarchy of objects that have the opportunity to respond to events received.
The first object in the ResponderChain is called the FirstResponder.

50. Helper Objects
Helper Objects are used throughout Cocoa and CocoaTouch, and usually take the form of a delegate or dataSource. They are commonly used to add functionality to an existing class without having to subclass it.

51. TableView’s delegate, datasource
“delegate” methods control tableview behavior.
“datasource methods focus on providing and effecting data.
Delegate of NSTableView
·         (void)tableViewSelectionDidChange:(NSNotification *)aNotification
·         NSTableViewSelectionDidChangeNotification
To be a data source for an NSTableView, you just have to implement three methods:
·         (int)numberOfRowsInTableView:(NSTableView *)aTableView                 - Returns the number of rows to display
·         (id)tableView:(NSTableView*)aTableView
 objectValueForTableColumn:(NSTableColumn *)aTableColumn
 row:(int)rowIndex - Returns data for a given row in a given column. This data is fed into the NSCell set up for that column.
·         (void)tableView:(NSTableView*)aTableView
 setObjectValue:(id)anObject
forTableColumn:(NSTableColumn *)aTableColumn
row:(int)rowIndex - Called when the user changes the value of a given data cell. Don't implement this if you want a read only NSTableView.

52. KVC
Key-value coding is a mechanism for accessing an object’s properties indirectly, using strings to identify properties, rather than through invocation of an accessor method or accessing them directly through instance variables. E.g. NSDictionary and NSMutableDictionary
 "Keys" are just strings, and "values" can be any type of object.

53. Key value path
Cocoa makes a distinction between "keys" and "key paths". A "key" allows you to get a value on an object. A "key path" allows you to chain multiple keys together, separated by dots.
For example :
      [p valueForKeyPath:@"spouse.name"];
      … is exactly the same as this…
      [[p valueForKey:@"spouse"] valueForKey:@"name"];

54. KVO
Key-value observing is a mechanism that allows objects to be notified of changes to specified properties of other objects. Key-value observing is a mechanism that allows objects to be notified of changes to specified properties of other objects.

55. KVB or Binding
In simple terms KVB=KVC + KVO
A binding is an attribute of one object that may be bound to a property in another such that a change in either one is reflected in the other. For example, the “value” binding of a text field might be bound to the temperature attribute of a particular model object. More typically, one binding might specify that a controller object “presents” a model object and another binding might specify that the value of a text field be tied to the temperature property of the object presented by the controller.
 Cocoa bindings reduces the code dependencies between models, views and controllers, supports multiple ways of viewing your data, and automatically synchronizes views when models change. Cocoa bindings provides extensible controllers, protocols for models and views to adopt, and additions to classes in Foundation and the Application Kit. You can eliminate most of your glue code by using bindings available in Interface Builder to connect controllers with models and views.

56. #import and @class filename
#import brings the entire header file in question into the current file; any files that THAT file #imports are also included. @class, on the other hand (when used on a line by itself with some class names), just tells the compiler "Hey, you're going to see a new token soon; it's a class, so treat it that way).

57. Singleton class
Only one instance of that class is created in the application.
@interface SomeManager : NSObject
             + (id)singleton;
 @end
 @implementation SomeManager
            + (id)singleton {    
                                 static id sharedMyManager = nil; 
                                 @synchronized([MyObject class]){ 
                                                     if (sharedMyManager == nil) { 
                                                                         sharedMyManager = [[self alloc] init]; 
                                                      } 
                                 }
                                return sharedMyManager;
            }
 @end

//using block
+ (id) singleton {
    static SomeManager *sharedMyManager = nil;
    static dispatch_once_t  onceToken;
    dispatch_once(&onceToken, ^{
        sharedMyManager = [[self alloc] init];
    });
    return sharedMyManager;
}

58. File’s owner
The File's Owner of your primary nib file is, by default, the NSApplication class and this comes ready-made for you when you create your Cocoa application. If your application has just the one nib file, you really don't need to worry about File's Owner. But if that's true, your application is probably really trivial or not well written.
The File's Owner of the nib is the object that makes communication possible between this new nib and other parts of the application. 

59. Whats the difference between frame and bounds?
The frame of a view is the rectangle, expressed as a location (x,y) and size (width,height) relative to the superview it is contained within. The bounds of a view is the rectangle, expressed as a location (x,y) and size (width,height) relative to its own coordinate system (0,0).

60. What’s the NSCoder class used for?  
NSCoder is an abstractClass which represents a stream of data. They are used in Archiving and Unarchiving objects. NSCoder objects are usually used in a method that is being implemented so that the class conforms to the protocol. (which has something like encodeObject and decodeObject methods in them).

61. Implement the following methods: retain, release, autorelease. 
-(id) retain{
                NSIncrementExtraRefCount(self);
                return self;
}

-(id) release{
                if(NSDecrementExtraRefCountWasZero(self)){
                                NSDeallocObject(self);
                }
}

-(id) autorelease{
                //add the object to the autorelease pool
                [NSAutoreleasePool addObject:self];
                return self;
}
62. Implement your own synthesized methods for the property NSString *title.
-(NSString*) title {
                return title;
}

-(void) setTitle: (NSString *) newTitle{
                if(newTitle != title){
                                [title release];
                                title=[newTitle retain]; // or copy as per your need
                }
}

63.  Cluster Class
Class clusters are a design pattern that the Foundation framework makes extensive use of. Class clusters group a number of private concrete subclasses under a public abstract superclass. The grouping of classes in this way simplifies the publicly visible architecture of an object-oriented framework without reducing its functional richness.

64. Shallow copying vs deep copy.
Copies of objects can be shallow or deep. Both shallow- and deep-copy approaches directly duplicate scalar properties but differ on how they handle pointer references, particularly references to objects (for example, NSString *str). A deep copy duplicates the objects referenced while a shallow copy duplicates only the references to those objects. So if object A is shallow-copied to object B, object B refers to the same instance variable (or property) that object A refers to. Deep-copying objects is preferred to shallow-copying, especially with value objects.
Shallow is “by Reference”, Deep is “by Value”




65. Differentiate Foundation vs Core Foundation
CoreFoundation is a general-purpose C framework whereas Foundation is a general-purpose Objective-C framework. Both provide collection classes, run loops, etc, and many of the Foundation classes are wrappers around the CF equivalents. CF is mostly open-source , and Foundation is closed-source.
Core Foundation is the C-level API, which provides CFString, CFDictionary and the like. Foundation is Objective-C, which provides NSString, NSDictionary, etc. CoreFoundation is written in C while Foundation is written in Objective-C. Foundation has a lot more classes CoreFoundation is the common base of Foundation and Carbon.
66. Difference between coreData and Database

Database
	
Core Data
Primary function is storing and fetching data
	
Primary function is graph management (although reading and writing to disk is an important supporting feature)
Operates on data stored on disk (or minimally and incrementally loaded)
	
Operates on objects stored in memory (although they can be lazily loaded from disk)
Stores "dumb" data
	
Works with fully-fledged objects that self-manage a lot of their behavior and can be subclassed and customized for further behaviors
Can be transactional, thread-safe, multi-user
	
Non-transactional, single threaded, single user (unless you create an entire abstraction around Core Data which provides these things)
Can drop tables and edit data without loading into memory
	
Only operates in memory
Perpetually saved to disk (and often crash resilient)
	
Requires a save process
Can be slow to create millions of new rows
	
Can create millions of new objects in-memory very quickly (although saving these objects will be slow)
Offers data constraints like "unique" keys
	
Leaves data constraints to the business logic side of the program

67. Core data vs sqlite.
Core data is an object graph management framework. It manages a potentially very large graph of object instances, allowing an app to work with a graph that would not entirely fit into memory by faulting objects in and out of memory as necessary. Core Data also manages constraints on properties and relationships and maintains reference integrity (e.g. keeping forward and backwards links consistent when objects are added/removed to/from a relationship). Core Data is thus an ideal framework for building the "model" component of an MVC architecture.
To implement its graph management, Core Data happens to use sqlite as a disk store. It could have been implemented using a different relational database or even a non-relational database such as CouchDB. As others have pointed out, Core Data can also use XML or a binary format or a user-written atomic format as a backend (though these options require that the entire object graph fit into memory).

68. Retain cycle or Retain loop.
When object A retains object B, and object B retains A. Then Retain cycle happens. To overcome this use “close” method.
Objective-C's garbage collector (when enabled) can also delete retain-loop groups  but this is not relevant on the iPhone, where Objective-C garbage collection is not supported.

69. What is unnamed category.
A named category -- @interface Foo(FooCategory) -- is generally used to:
    i. Extend an existing class by adding functionality.
  ii. Declare a set of methods that might or might not be implemented by a delegate.

Unnamed Categories has fallen out of favor now that @protocol has been extended to support @optional methods.
A class extension -- @interface Foo() -- is designed to allow you to declare additional private API -- SPI or System Programming Interface -- that is used to implement the class innards. This typically appears at the top of the .m file. Any methods / properties declared in the class extension must be implemented in the @implementation, just like the methods/properties found in the public @interface.
Class extensions can also be used to redeclare a publicly readonly @property as readwrite prior to @synthesize'ing the accessors.
Example:
     Foo.h
@interface Foo:NSObject
     @property(readonly, copy) NSString *bar;
    -(void) publicSaucing;
@end
     Foo.m
@interface Foo()
     @property(readwrite, copy) NSString *bar;
     - (void) superSecretInternalSaucing;
@end
@implementation Foo
     @synthesize bar;
.... must implement the two methods or compiler will warn ....
@end

70. Copy vs mutableCopy.
copy always creates an immutable copy.
mutableCopy always creates a mutable copy.

71. Strong vs Weak
The strong and weak are new ARC types replacing retain and assign respectively.
Delegates and outlets should be weak.
A strong reference is a reference to an object that stops it from being deallocated. In other words it creates a owner relationship.
A weak reference is a reference to an object that does not stop it from being deallocated. In other words, it does not create an owner relationship.

72. __strong, __weak, __unsafe_unretained, __autoreleasing.
Generally speaking, these extra qualifiers don’t need to be used very often. You might first encounter these qualifiers and others when using the migration tool. For new projects however, you generally you won’t need them and will mostly use strong/weak with your declared properties.
__strong – is the default so you don’t need to type it. This means any object created using alloc/init is retained for the lifetime of its current scope. The “current scope” usually means the braces in which the variable is declared
__weak – means the object can be destroyed at anytime. This is only useful if the object is somehow strongly referenced somewhere else. When destroyed, a variable with __weak is set to nil.
__unsafe_unretained – is just like __weak but the pointer is not set to nil when the object is deallocated. Instead the pointer is left dangling.
__autoreleasing, not to be confused with calling autorelease on an object before returning it from a method, this is used for passing objects by reference, for example when passing NSError objects by reference such as [myObject performOperationWithError:&tmp];

73. Types of NSTableView
      Cell based and View based. In view based we can put multiple objects.

74. When to use Bindings.

75. Software Design Pattern.
Creational Patterns
Factory - The Factory Method defines an interface for creating objects, but lets subclasses decide which classes to instantiate.

e.g.: SuperClass:Employee.
SubClasses as:FullTimeEmployee and PartTimeEmployee.
Cluster Class
Abstract Factory
Singleton - The Singleton pattern ensures that a class has only one instance and provides a global point of access to that instance.

e.g.: LoggerClass
Builder
Prototype
Structural Patterns
Adapter - The Adapter pattern allows otherwise incompatible classes to work together by converting the interface of one class into an interface expected by the clients.

Bridge
Composite
Decorator
Façade - The Façade defines a unified, higher level interface that makes it easier to use.

Eg: A Customer Care Person has access to Customer + Order Detail + Dispatch, they can talk to all of them, while Customer has only access to CCP. Here CCP acts as Façade.
Flyweight
Proxy
Behaviour Patterns
Chain of responsibilty
 Command
 Interpreter
 Iterator
 Momentro
 State
 Observer
 Strategey
 Template Visitor
               
76. Mac OS Releases.
Version 10.0: "Cheetah"
Version 10.1: "Puma"
Version 10.2: "Jaguar"
Version 10.3: "Panther"
Version 10.4: "Tiger"
Version 10.5: "Leopard"
Version 10.6: "Snow Leopard"
Version 10.7: "Lion"
Version 10.8: "Mountain Lion"
Version 10.9: "Mavericks"
Version 10.10: "Yosemite".

77. Structure of MacOS.







78. Web Services
What are Web Services?
·         Web services are application components
·         Web services communicate using open protocols
·         Web services are self-contained and self-describing
·         Web services can be discovered using UDDI
·         Web services can be used by other applications
·         XML is the basis for Web services

How Does it Work?
The basic Web services platform is XML + HTTP.
XML provides a language which can be used between different platforms and programming languages and still express complex messages and functions.
The HTTP protocol is the most used Internet protocol.
Web services platform elements:
·         SOAP (Simple Object Access Protocol)
·         UDDI (Universal Description, Discovery and Integration)
·         WSDL (Web Services Description Language)
In cocoa, NSURLConnection and NSURLRequest are used for this.

79. Abstract class in cocoa.
Cocoa doesn’t provide anything called abstract.  We can create a class abstract which gets check only at runtime, compile time this is not checked.
@interface AbstractClass : NSObject
@end
@implementation AbstractClass
+ (id)alloc{
    if (self == [AbstractClass class]) {
        NSLog(@"Abstract Class cant be used");
    }
    return [super alloc];
@end

80. xml parsers.
NSXML is SAX parser.
SAX parser is one where your code is notified as the parser walks through the XML tree, and you are responsible for keeping track of state and constructing any objects you might want to keep track of the data as the parser marches through.
A DOM parser reads the entire document and builds up an in-memory representation that you can query for different elements. Often, you can even construct XPath queries to pull out particular pieces.

SAX parser is advantageous than using DOM parser.
-The input document is too big for available memory (actually in this case SAX is your only choice)
-You can process the document in small contiguous chunks of input. You do not need the entire document before you can do useful work
-You just want to use the parser to extract the information of interest, and all your computation will be completely based on the data structures created by yourself. Actually in most of our applications, we create data structures of our own which are usually not as complicated as the DOM tree. From this sense, I think, the chance of using a DOM parser is less than that of using a SAX parser.

 DOM parser is advantageous than using SAX parser.
-Your application needs to access widely separately parts of the document at the same time.
-Your application may probably use a internal data structure which is almost as complicated as the document itself.
-Your application has to modify the document repeatedly.

-Your application has to store the document for a significant amount of time through many method calls.

81. What is syncronous and asynchronous call?
A synchronous process is invoked by a request/response operation, and the result of the process is returned to the caller immediately via this operation.
An asynchronous process is invoked by a one-way operation and the result and any faults are returned by invoking other one-way operations. The process result is returned to the caller via a callback operation.
For example, you can think of a synchronous process as a telephone, and an asynchronous process as the postal system. When you are having a conversation on the phone, you send and receive messages instantaneously using the same connection. If you were to send the same message in a letter via the postal service, it would be delivered in one manner, and its response returned in another.

82.  How you send notification to other applications / observe them?
        [[NSWorkspace shardWorkspace] notificationCenter].
        Distributed Objects.
        NSInvocation.

83. How u decide background or foreground application?

84. How u do unit testing for your code and gui.

85. Where are objects and variables stored in Objective-C (Heap or Stack)?

In Objective-C, objects are usually created on the heap:

    NSObject *obj = [[NSObject alloc] init];



The storage for the obj variable itself is on the stack, but the object it points to is in the heap. The [NSObject alloc] call allocates a chunk of heap memory, and fills it out to match the layout needed for an NSObject.



A stack object is just an object where the memory for that object is allocated on the stack. Objective-C doesn't have any support for this directly



Objective-C supports stack objects only for Blocks.

86. Sandboxing

87. NSURLConnection class, types and how to use.

There are two ways of using the NSURLConnection class. One is asynchronous, and the other is synchronous. An asynchronous connection will create a new thread and does its downloading process on the new thread. A synchronous connection will block the calling thread while downloading content and doing its communication.
Many developers think that a synchronous connection blocks the main thread, but that is incorrect. A synchronous connection will always block the thread from which it is fired. If you fire a synchronous connection from the main thread, yes, the main thread will be blocked. But if you fire a synchronous connection from a thread other than the main thread, it will be like an asynchronous connection in that it won’t block your main thread. In fact, the only difference between a synchronous and an asynchronous con‐ nection is that the runtime will create a thread for the asynchronous connection, while it won’t do the same for a synchronous connection.
In order to create an asynchronous connection, we need to do the following:

       Have our URL in an instance of NSString.
       Convert our string to an instance of NSURL.
      Place our URL in a URL Request of type NSURLRequest, or in the case of mutable URLs, in an instance of NSMutableURLRequest.
       Create an instance of NSURLConnection and pass the URL request to it. 


88. Cocoa class naming conventions.

89. Difference between HTTP and HTTPS.
·         HTTP stands for HyperText Transfer Protocol, whereas, HTTPS is HyperText Transfer Protocol Secure.
·         HTTP transmits everything as plan text, while HTTPS provides encrypted communication, so that only the recipient can decrypt and read the information.  Basically, HTTPS is a combination of HTTP and SSL (Secure Sockets Layer). This SSL is that protocol which encrypts the data.
·         HTTP is fast and cheap, where HTTPS is slow and expensive.
As, HTTPS is safe it’s widely used during payment transactions or any sensitive transactions over the internet. On the other hand, HTTP is used most of the sites over the net, even this blogspot sites also use HTTP.
·         HTTP URLs starts with “http:// “ and use port 80 by default, while HTTPS URLs stars with “https:// “ and use port 443.
·         HTTP is unsafe from attacks like man-in-the-middle and eavesdropping, but HTTPS is secure from these sorts of attacks.

90.GCD
Grand Central Dispatch is not just a new abstraction around what we've already been using, it's an entire new underlying mechanism that makes multithreading easier and makes it easy to be as concurrent as your code can be without worrying about the variables like how much work your CPU cores are doing, how many CPU cores you have and how much threads you should spawn in response. You just use the Grand Central Dispatch API's and it handles the work of doing the appropriate amount of work. This is also not just in Cocoa, anything running on Mac OS X 10.6 Snow Leopard can take advantage of Grand Central Dispatch ( libdispatch ) because it's included in libSystem.dylib and all you need to do is include #import <dispatch/dispatch.h> in your app and you'll be able to take advantage of Grand Central Dispatch.

91.  How you attain the backward compatibility?

    Set the Base SDK to Current version of Mac (ex. 10.8)
    Set the Deployment SDK to older version (ex.1.6)

92. Call Back.

Synchronous operations are ones that happen in step with your calling code. Most of Cocoa works this way: you send a message to an object, say to format a string, etc, and by the time that line of code is "done", the operation is complete.

But in the real world, some operations take longer than "instantaneous" (some intensive graphics work, but mainly high or variably latency things like disk I/O or worse, network connectivity). These operations are unpredictable, and if the code were to block until finish, it might block indefinitely or forever, and that's no good.

So the way we handle this is to set up "callbacks"-- you say "go off and do this operation, and when you're done, call this other function". Then inside that "callback" function, you start the second operation that depends on the first. In this way, you're not spinning in circles waiting, you just get called "asynchronously" when each task is done.

93. When to use Blocks?
Blocks are first-class functions, which is a fancy way of saying that Blocks are regular Objective-C objects. Since they’re objects, they can be passed as parameters, returned from methods and functions, and assigned to variables. Blocks are called closures in other languages such as Python, Ruby and Lisp, because they encapsulate state when they are declared. A block creates a const copy of any local variable that is referenced inside of its scope. Before blocks, whenever you wanted to call some code and have it call you back later, you would typically use delegates or NSNotificationCenter. That worked fine, except it spreads your code all over – you start a task in one spot, and handle the result in another.

94.    Does Objective-C contain private methods?
NO.
There is nothing called a private method in Obj-C. If a method is defined in .m only then it becomes protected. If in .h it is public.
If you really want a private method then you need to add a local category/ unnamed category/ class extension on the class and add the method in the category and define the method in the class.m

95. What is new with XCode4.4+
The compiler LLVM/clang 3.2
literals for arrays, dictionary.
auto-synthesize for @property. @synthisize prop=_prop;

96. NSThread vs GCD

Migrating Away from Threads
The idea is that you eliminate work on your part, since the paradigm fits MOST code more easily.

        It reduces the memory penalty your application pays for storing thread stacks in the application’s memory space.
        It eliminates the code needed to create and configure your threads.
        It eliminates the code needed to manage and schedule work on threads.
        It simplifies the code you have to write.

Empirically, using GCD-type locking instead of @synchronized is about 80% faster or more, though micro-benchmarks may be deceiving. Read more here, though I think the advice to go async with writes does not apply in many cases, and it's slower (but it's asynchronous).
Advantages of Threads
Why would you continue to use Threads? From the same document:

    It is important to remember that queues are not a panacea for replacing threads. The asynchronous programming model offered by queues is appropriate in situations where latency is not an issue. Even though queues offer ways to configure the execution priority of tasks in the queue, higher execution priorities do not guarantee the execution of tasks at specific times. Therefore, threads are still a more appropriate choice in cases where you need minimal latency, such as in audio and video playback.

Another place where I haven't personally found an ideal solution using queues is daemon processes that need to be constantly rescheduled. Not that you cannot reschedule them, but looping within a NSThread method is simpler (I think). Edit: Now I'm convinced that even in this context, GCD-style locking would be faster, and you could also do a loop within a GCD-dispatched operation.
97. What is Bundle Identifiers.

A bundle ID precisely identifies a single app. A bundle ID is used during the development process to provision devices and by the operating system when the app is distributed to customers. For example, Game Center and In-App Purchase use a bundle ID to identify your app when using these services. The preferences system uses this string to identify the app for which a given preference applies. Similarly, Launch Services uses the bundle ID to locate an app capable of opening a particular file, using the first app it finds with the given identifier. The bundle ID is also used to validate an app’s signature.
The bundle ID string must be a uniform type identifier (UTI) that contains only alphanumeric characters (A-Z,a-z,0-9), hyphen (-), and period (.). The string should be in reverse-DNS format. For example, if your company’s domain is Ajax.com and you create an app named Hello, you could assign the string com.Ajax.Hello as your app’s bundle ID.


98. What are differences between Library and Frameworks.
A static library is actually compiled as part of your app, whereas a framework is distributed with your app. 

Basically, frameworks ARE libraries and provide a handy mechanism for working with them. If you look "inside" a framework, it's just a directory containing a static library and header files (in some folder structure with metadata).
If you want to create your own framework, you have to create a "static library" and pack it in a specific way.
---

Static library - a unit of code linked at compile time, which does not change.
However, iOS static libraries are not allowed to contain images/assets (only code). You can get around this challenge by using a media bundle though. 
Dynamic library - a unit of code and/or assets linked at runtime that may change.
However, only Apple is allowed to create dynamic libraries for iOS , for OSX you can create your own. 
Software Framework - a compiled set of code that accomplishes a task... hence, you can actually have a static framework or a dynamic framework, which are typically just the compiled versions of the above.


99. Difference between JSON and XML.
JSON is so much more lightweight and less verbose.

100. When to use Delegates, Notifications, KVO and blocks.
As all the four severs almost similar functions, as these are used to get and send values (callbacks).

Block: 1 to 3 callbacks and 1 observer.

Delegate: Many callbacks and single observer.

KVO: Any number of Observers. Just want to be notified of changes to state of an object. Simplistic update (UI update), unrelated to behaviour.

Notification: Multiple observers. Observer “far away” from Observee(Poster).

