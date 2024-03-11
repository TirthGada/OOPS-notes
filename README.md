
Unary Operators: These are operators that work with only one operand. Examples include the unary minus (-), unary plus (+), logical NOT (!), and increment/decrement (++/--).

Binary Operatrs: These are operators that work with two operands. Examples include arithmetic operators like addition (+), subtraction (-), multiplication (*), division (/), and comparison operators like equals (==), less than (<), greater than (>), etc.

# POLYMORPHISM


**one name , multiple forms** 
i.e objects of different classe respond showing similar behaviours  

**Compile-time and Runtime are the two programming terms used in the software development. Compile-time is the time at which the source code is converted into an executable code while the run time is the time at which the executable code is started running. Both the compile-time and runtime refer to different types of error.**


## Compile time polymorphism ( Early Binding ) :  Function Overloading & Operator Overloading
                        
                        // C++ program to demonstrate
                        // function overloading or
                        class Geeks {
                        public:
                        	// Function with 1 int parameter
                        	void func(int x)
                        	{
                        		cout << "value of x is " << x << endl;
                        	}
                        
                        	// Function with same name but
                        	// 1 double parameter
                        	void func(double x)
                        	{
                        		cout << "value of x is " << x << endl;
                        	}
                        
                        	// Function with same name and
                        	// 2 int parameters
                        	void func(int x, int y)
                        	{
                        		cout << "value of x and y is " << x << ", " << y
                        			<< endl;
                        	}
                        };



**Operator overloading**

**Operator overloading is a feature in many programming languages that allows you to redefine the behavior of certain operators (such as +, -, *, /, etc.) for user-defined data types.* This means you can define how operators should work when applied to objects of your custom classes.**

For example, in a programming language that supports operator overloading, you could define how the + operator should behave when applied to two instances of a class you've created. This enables you to write code that looks more intuitive and expressive.


// C++ program to demonstrate

// Operator Overloading or

                                    **1)** Unary Operator overloading

                                    class Increase{
                                    private:
                                      int value;

                                    public:
                                      Increase()
                                      {
                                      value=10;
                                      }

                                      void operator ++()
                                      {
                                      value=value+5;
                                      }
                                      void display(){
                                      cout<<"Value is"<<value;}
                                      };  

                                      int main(){
                                      Increase inc;
                                      ++inc;
                                      inc.display();
                                      return 0;
                                      }

                                      //output 

                                      Value is 15
                                      
                                      

                                    **2)** Binary  Operator overloading
                                    class Complex {
                                    private:
                                    	int real, imag;
                                    
                                    public:
                                    	Complex(int r = 0, int i = 0)
                                    	{
                                    		real = r;
                                    		imag = i;
                                    	}
                                    
                                    	// This is automatically called
                                    	// when '+' is used with between
                                    	// two Complex objects
                                    	Complex operator+(Complex const& obj)
                                    	{
                                    		Complex res;
                                    		res.real = real + obj.real;
                                    		res.imag = imag + obj.imag;
                                    		return res;
                                    	}
                                    	void print() { cout << real << " + i" << imag << endl; }
                                    };
                                    
                                    int main()
                                    {
                                    	Complex c1(10, 5), c2(2, 4);
                                    
                                    	// An example call to "operator+"
                                    	Complex c3 = c1 + c2;
                                    	c3.print();
                                    }


## Run time polymorphism : Virtual Functions


<img width="1440" alt="Screenshot 2024-03-08 at 9 12 45 PM" src="https://github.com/TirthGada/OOPS-notes/assets/118129263/5abf11d2-25e0-4707-9b31-6b86adea944e">

The photo added above is also a example of run time polymorphism since when there 2 functions with same name , one from derived & base class , it is decided at run time to which function to use .

To overcome above issue of run time polymorphism if we want we can use virtual function shown below



***********

# Virtual Function 
        
        class BaseClass{
            public:
                int var_base=1;
                virtual void display(){
                    cout<<"1 Dispalying Base class variable var_base "<<var_base<<endl;
                }
        };
        
        class DerivedClass : public BaseClass{
            public:
                    int var_derived=2;
                    void display(){
                        cout<<"2 Dispalying Base class variable var_base "<<var_base<<endl;
                        cout<<"2 Dispalying Derived class variable var_derived "<<var_derived<<endl;
                    }
        };

        int main(){
            BaseClass * base_class_pointer;
            BaseClass obj_base;
            DerivedClass obj_derived;
        
            base_class_pointer = &obj_derived;
            base_class_pointer->display();
            return 0;
        }


**Since here the function display is made virtual , the function will be runned of base class**

*******

        
        class CWH{
            protected:
                string title;
                float rating;
            public:
                CWH(string s, float r){
                    title =  s;
                    rating = r;
                }
                virtual void display(){}
        };
        
        class CWHVideo: public CWH
        {
            float videoLength;
            public:
                CWHVideo(string s, float r, float vl): CWH(s, r){
                    videoLength = vl;
                }
                void display(){
                    cout<<"This is an amazing video with title "<<title<<endl;
                    cout<<"Ratings: "<<rating<<" out of 5 stars"<<endl;
                    cout<<"Length of this video is: "<<videoLength<<" minutes"<<endl;
                }
        };    
        
        class CWHText: public CWH
        {
            int words;
            public:
                CWHText(string s, float r, int wc): CWH(s, r){
                    words = wc;
                }
             void display(){
              cout<<"This is an amazing text tutorial with title "<<title<<endl;
              cout<<"Ratings of this text tutorial: "<<rating<<" out of 5 stars"<<endl;
              cout<<"No of words in this text tutorial is: "<<words<<" words"<<endl;
                 }
        };
        
        int main(){
            string title;
            float rating, vlen;
            int words;
        
            // for Code With Harry Video
            title = "Django tutorial";
            vlen = 4.56;
            rating = 4.89;
            CWHVideo djVideo(title, rating, vlen);
        
            // for Code With Harry Text
            title = "Django tutorial Text";
            words = 433;
            rating = 4.19;
            CWHText djText(title, rating, words);
        
            CWH* tuts[2];
            tuts[0] = &djVideo;
            tuts[1] = &djText;
        
            tuts[0]->display();
            tuts[1]->display();
        
            return 0;
        }

        // OUTPUT 
         on doing tut0 & 1 display since base class display function has been made virtual , the derived class display functions will be running

*********

# PURE VIRTUAL FUNCTION

        
        class CWH{
            protected:
                string title;
                float rating;
            public:
                CWH(string s, float r){
                    title =  s;
                    rating = r;
                }
                virtual void display()=0
        };
        
        class CWHVideo: public CWH
        {
            float videoLength;
            public:
                CWHVideo(string s, float r, float vl): CWH(s, r){
                    videoLength = vl;
                }
              
        };    
        
        class CWHText: public CWH
        {
            int words;
            public:
                CWHText(string s, float r, int wc): CWH(s, r){
                    words = wc;
                }
             void display(){
              cout<<"This is an amazing text tutorial with title "<<title<<endl;
              cout<<"Ratings of this text tutorial: "<<rating<<" out of 5 stars"<<endl;
              cout<<"No of words in this text tutorial is: "<<words<<" words"<<endl;
                 }
        };
        
        int main(){
            string title;
            float rating, vlen;
            int words;
        
            // for Code With Harry Video
            title = "Django tutorial";
            vlen = 4.56;
            rating = 4.89;
            CWHVideo djVideo(title, rating, vlen);
        
            // for Code With Harry Text
            title = "Django tutorial Text";
            words = 433;
            rating = 4.19;
            CWHText djText(title, rating, words);
        
            CWH* tuts[2];
            tuts[0] = &djVideo;
            tuts[1] = &djText;
        
            tuts[0]->display();
            tuts[1]->display();
        
            return 0;
        }

the code modification done in base class display function makes it pure virtual function which says u have to define the same name waala function in the derived class 

this code will give error as i had made base class function **pure virtual** but removed one of the derived class's function


**********
# Encapsulation
Encapsulation in C++ is defined as the wrapping up of data and information in a single unit. In Object Oriented Programming, Encapsulation is defined as binding together the data and the functions that manipulate them.

Consider a real-life example of encapsulation, in a company, there are different sections like the accounts section, finance section, sales section, etc. Now,

The finance section handles all the financial transactions and keeps records of all the data related to finance.
Similarly, the sales section handles all the sales-related activities and keeps records of all the sales.
Now there may arise a situation when for some reason an official from the finance section needs all the data about sales in a particular month.

In this case, he is not allowed to directly access the data of the sales section. He will first have to contact some other officer in the sales section and then request him to give the particular data.


            Encapsulation code

            class car {
            int speed;
            char color;
            int fuel;
            int xyz;
            } 
            
 **Encapsulation mainly refers to the property of wrapping up all info like spped , color , fuel capacity and many more inside the the class car**


Two Important  property of Encapsulation 

Data Protection: Encapsulation protects the internal state of an object by keeping its data members private. Access to and modification of these data members is restricted to the class’s public methods, ensuring controlled and secure data manipulation.

Information Hiding: Encapsulation hides the internal implementation details of a class from external code. Only the public interface of the class is accessible, providing abstraction and simplifying the usage of the class while allowing the internal implementation to be modified without impacting external code.
                
                
                class temp{
                	int a;
                int b;
                public:
                int solve(int input){
                	a=input;
                	b=a/2;
                	return b;
                }
                };
                
                int main() {
                int n;
                cin>>n;
                temp half;
                int ans=half.solve(n);
                cout<<ans<<endl;
                	
                }


Features of Encapsulation
Below are the features of encapsulation:

We can not access any function from the class directly. We need an object to access that function that is using the member variables of that class. 

The function which we are making inside the class must use only member variables, only then it is called encapsulation.

If we don’t make a function inside the class which is using the member variable of the class then we don’t call it encapsulation.

Encapsulation improves readability, maintainability, and security by grouping data and methods together.

It helps to control the modification of our data members.


// C++ program to demonstrate
                // Encapsulation
                class Encapsulation {
                private:
                	// Data hidden from outside world
                	int x;
                
                public:
                	// Function to set value of
                	// variable x
                	void set(int a) { x = a; }
                
                	// Function to return value of
                	// variable x
                	int get() { return x; }
                };
                
                // Driver code
                int main()
                {
                	Encapsulation obj;
                	obj.set(5);
                	cout << obj.get();
                	return 0;
                }


# ABSTRACTION

Data abstraction is one of the most essential and important features of object-oriented programming in C++. Abstraction means displaying only essential information and hiding the details. Data abstraction refers to providing only essential information about the data to the outside world, hiding the background details or implementation. 

Consider a real-life example of a man driving a car. The man only knows that pressing the accelerator will increase the speed of the car or applying brakes will stop the car but he does not know how on pressing the accelerator the speed is actually increasing, he does not know about the inner mechanism of the car or the implementation of the accelerator, brakes, etc in the car. This is what abstraction is.
                
You can see in the above program we are not allowed to access the variables a and b directly, however, one can call the function set() to set the values in a and b and the function display() to display the values of a and b. 

<img width="1440" alt="Screenshot 2024-03-07 at 12 10 06 AM" src="https://github.com/TirthGada/OOPS-notes/assets/118129263/5b0749a1-8478-4569-a3c9-cc7f3523b159">
