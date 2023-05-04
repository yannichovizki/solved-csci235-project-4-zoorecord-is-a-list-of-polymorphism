Download Link: https://assignmentchef.com/product/solved-csci235-project-4-zoorecord-is-a-list-of-polymorphism
<br>
<strong> </strong>In Project3 we stored Animal objects into an ArrayBag. However, each entry in our data file is a different Animal-class. In Project4 we will use Polymorphism to store (via pointers) different Animal-derived objects into a List. Thus, Project4 will continue to build on the previous projects to work with <strong>Lists </strong>and <strong>Polymorphism.  </strong>

We will work with the <strong>List</strong> class (doubly-linked List) discussed during lecture. This project will also be subdivided in <strong>two parts</strong>:

<ol>

 <li>Modify the Animal, Mammal, Bird and Fish classes to support <strong>Polymorphism</strong>.</li>

 <li>Modify ZooRecord to <u>inherit from List </u>and store <strong><u>pointers</u></strong><u> to </u><u>Animal</u>, where the pointers will <u>actually point to either </u><u>Mammal, </u><u>Bird or </u><u>Fish dynamic objects</u>.</li>

</ol>

<strong> </strong>

<strong>Implementation – 2 parts:  </strong>

<strong> </strong>

<strong>Part1:  Modify Animal and derived classes </strong>

<strong>           </strong>

Modify the Animal class by modifying display() to be a <strong>pure virtual function</strong>. Each derived class can then <strong>override</strong> display() to display data specific to the derived object as follows:

<ul>

 <li>Mammal::display()</li>

</ul>

Sample output:

<strong>“animal_name is [not] domestic and [it is / is not] a predator,
    it is [not] airborne and it is [not] aquatic,
</strong>

<strong>   it has [no] hair, [no] teeth, [no] fins, [no] tail and legs_ legs.

”</strong>

<strong> </strong>

<strong> </strong>

<strong>Note:</strong> in the sample output above, <strong>[text]  </strong>(text in square brackets) may or may not appear in the output, depending on the specific animal data.

<ul>

 <li>Bird::display()</li>

</ul>

Sample output:

<strong>“animal_name is [not] domestic and [it is / is not] a predator,
 </strong><strong>    </strong><strong>it is [not] airborne and it is [not] aquatic.

<em>”</em></strong>




<ul>

 <li>Fish::display()</li>

</ul>

Sample output:

“<strong>animal_name is [not] domestic, [it is / is not] a predator
 </strong><strong>    </strong><strong>and it is [not] venomous.

</strong>”

<strong>Note:</strong> The formatting must match <strong>EXACTLY</strong>, please pay special attention to  spacing, punctuation and capitalization<strong> </strong>

<strong>Part2:  Modify the ZooRecord class </strong>

Modify the ZooRecord class to <strong>inherit from List </strong>and store <strong>pointers to Animal </strong>(You will find List, Node and Exception class files on Blackboard under Course Materials/ Project4 Files). ZooRecord must have at least (but is not limited to) the following methods:

/**parameterized constructor

<strong>@pre</strong> the input file is expected to be in CSV (comma separated value) format as:

“animal_name,hair,feathers,eggs,milk,airborne,aquatic,predator,toothed,backbo ne,breathes,venomous,fins,legs,tail,domestic,catsize,class_type<strong>
</strong>”

<strong>@param</strong> input_file_name the name of  the input file

<strong>@post</strong> adds Animal pointers to Animal-derived dynamic objects to record as per the data in the input file

**/

ZooRecord(std::string input_file_name);

<strong>Note:</strong> our data file for this project has been modified to contain only class-types ‘1’ (Mammal), ‘2’ (Bird) and ‘4’ (Fish).

/**<strong>@post</strong> displays all animals in record, one per line by calling appropriate object’s display method” **/  <strong>void</strong> display();

You must also <strong>provide or allow for a default constructor</strong> (e.g. explicitly tell compiler to provide one with keyword default in interface)

<strong>Extra Credit (10 points): </strong>

If you’ve been paying attention, you should be very bothered by the way we implemented ZooRecord thus far. ZooRecord stores pointers to dynamically allocated Animal-derived objects, but the base class (List) does not know about this.




This means that if the ZooRecord is cleared or when a node is deleted or the ZooRecord object goes out of scope (the destructor is invoked), the List-derived remove() and clear() methods will only delete the dynamic nodes leaking the dynamic Animal-derived objects pointed to at each node.




To take care of this (for extra credit) do the following:

<ul>

 <li>Provide a destructor for ZooRecord that will take care of deleting the dynamic Animal-derived objects pointed to by the pointers stored in the ZooRecord nodes (you don’t need to delete the nodes because ~List() will be invoked anyways. If you wish to delete the nodes as well for efficiency, when ~List() is invoked it will already be empty). You can do so by overriding clear() to delete all dynamic Animal-derived objects and then explicitly calling List::clear() to delete the nodes. You can call clear() from ~ZooRecord().</li>

 <li>Override remove() to delete the dynamic Animal-derived objects as well as the nodes. Don’t forget to set the pointers stored in the nodes to nullptr.</li>

</ul>

<strong>Note: </strong>analogously, attention should be paid to copies as well <u>but to contain the size</u> <u>of the project we will not worry about that here.</u> Just keep in mind that copy constructors and assignment operators should both be taken care of to be used in ZooRecord in order to make “deep copies” of the Animal-derived dynamic objects.

<strong>Testing: </strong>

You must always test your implementation <strong>INCREMENTALLY</strong>!!!

In main() (not for submission) first test your modifications from Part 1. Instantiate objects of type Mammal, Bird and Fish and make calls to each object’s display() to check that data is displayed correctly.

When Part 1 is implemented and tested then move on to Part 2, instantiate in main() a ZooRecord object, and call dIsplay() on it. Make sure that Polymorphism is correctly implemented (each different object type is correctly calling its own version of

display()).