# OOPS-notes


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
                    
