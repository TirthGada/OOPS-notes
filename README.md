**Inheritance notes in other branch**
# DESTRUCTOR 
Destructor is an instance member function that is invoked automatically whenever an object is going to be destroyed. Meaning, a destructor is the last function that is going to be called before an object is destroyed.

** Objects are destroyed in the reverse order of their creation. In this case, t3 is the first to be destroyed, while t is the last. Destructor runs first for object created at last **

A destructor is also a special member function like a constructor. Destructor destroys the class objects created by the constructor. 

Destructor has the same name as their class name preceded by a tilde (~) symbol.

It is not possible to define more than one destructor. 

The destructor is only one way to destroy the object created by the constructor. Hence destructor can-not be overloaded.

Destructor neither requires any argument nor returns any value.

It is automatically called when an object goes out of scope. 

Destructor release memory space occupied by the objects created by the constructor.

In destructor, objects are destroyed in the reverse of an object creation.



# VIRTUAL DESTRUCTOR


Deleting a derived class object using a pointer of base class type that has a non-virtual destructor results in undefined behavior. To correct this situation, the base class should be defined with a virtual destructor. 
For example, the following program results in undefined behavior. 

        
        class base {
        public:
        	base()	 
        	{ cout << "Constructing base\n"; }
        	~base()
        	{ cout<< "Destructing base\n"; }	 
        };
        
        class derived: public base {
        public:
        	derived()	 
        	{ cout << "Constructing derived\n"; }
        	~derived()
        	{ cout << "Destructing derived\n"; }
        };
        
        int main()
        {
        derived *d = new derived(); 
        base *b = d;
        delete b;
        getchar();
        return 0;
        }

        ## 
        Constructing base
        Constructing derived
        Destructing base


CORRECTED CODE
          
          class base {
          public:
          	base()	 
          	{ cout << "Constructing base\n"; }
          	virtual ~base()
          	{ cout << "Destructing base\n"; }	 
          };
          
          class derived : public base {
          public:
          	derived()	 
          	{ cout << "Constructing derived\n"; }
          	~derived()
          	{ cout << "Destructing derived\n"; }
          };
          
          int main()
          {
          derived *d = new derived(); 
          base *b = d;
          delete b;
          getchar();
          return 0;
          }

          ## OUTPUT 
          Constructing base
          Constructing derived
          Destructing derived
          Destructing base


# Static Data Members

Static data members are class members that are declared using static keywords. A static member has certain special characteristics which are as follows:


Only one copy of that member is created for the entire class and is shared by all the objects of that class, no matter how many objects are created.

It is initialized before any object of this class is created, even before the main starts.

It is visible only within the class, but its lifetime is the entire program.


                class A {
                public:
                	A() 
                	{ 
                	cout << "A's Constructor Called " << 
                			endl; 
                	}
                };
                
                class B {
                	static A a;
                
                public:
                	B() 
                	{ 
                	cout << "B's Constructor Called " << 
                			endl; 
                	}
                };
                
                // Driver code
                int main()
                {
                	B b;
                	return 0;
                }

                # OUTPUT 
                B's Constructor Called 



***********

// C++ Program to demonstrate 
// the Compilation Error occurred
// due to violation of Static
                        
                        class A {
                        	int x;
                        
                        public:
                        	A() 
                        	{ 
                        	cout << "A's constructor called " << 
                        			endl; 
                        	}
                        };
                        
                        class B {
                        	static A a;
                        
                        public:
                        	B() 
                        	{ 
                        	cout << "B's constructor called " << 
                        			endl; 
                        	}
                        	static A getA() 
                        	{ 
                        	return a; 
                        	}
                        };
                        
                        // Driver code
                        int main()
                        {
                        	B b;
                        	A a = b.getA();
                        	return 0;
                        }


CORRECTED CODE


// C++ program to access static data
// member with explicit definition
                        
                        class A {
                        	int x;
                        
                        public:
                        	A() 
                        	{ 
                        	cout << "A's constructor called " << 
                        			endl; 
                        	}
                        };
                        
                        class B {
                        	static A a;
                        
                        public:
                        	B() 
                        	{ 
                        	cout << "B's constructor called " << 
                        			endl; 
                        	}
                        	static A getA() 
                        	{ 
                        	return a; 
                        	}
                        };
                        
                        // Definition of a
                        A B::a; 
                        
                        // Driver code
                        int main()
                        {
                        B b1, b2, b3;
                        A a = b1.getA();
                        
                        return 0;
                        }
                        
                        OUTPUT

                        A's constructor called 
                        B's constructor called 
                        B's constructor called 
                        B's constructor called 

                        ## The above program calls B’s constructor 3 times for 3 objects (b1, b2, and b3), but calls A’s constructor only once. The reason is that the static                                 members are shared among all objects. That is why they are also known as class members or class fields.
                                                                        




# STATIC MEMBER FUNCTION

Static members of a class are not associated with the objects of the class. Just like a static variable once declared is allocated with memory that can’t be changed every object points to the same memory. 

                
                
                class Student {
                public:
                	// static member
                	static int total;
                
                	// Constructor called
                	Student() { total += 1; }
                };
                
                int Student::total = 0;
                
                int main()
                {
                	// Student 1 declared
                	Student s1;
                	cout << "Number of students:" << s1.total << endl;
                
                	// Student 2 declared
                	Student s2;
                	cout << "Number of students:" << s2.total << endl;
                
                	// Student 3 declared
                	Student s3;
                	cout << "Number of students:" << s3.total << endl;
                	return 0;
                }

                # Output
                Number of students:1
                Number of students:2
                Number of students:3
