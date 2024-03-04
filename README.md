# INHERITANCE

**https://www.geeksforgeeks.org/inheritance-in-c/**


Protected access modifier is similar to that of private access modifiers, the difference is that the class member declared as Protected are inaccessible outside the class but they can be accessed by any subclass(derived class) of that class.

Example 
                        
                        class A
                        {protected:
                        	int a;
                        	public:
                        		void set_A()
                        		{
                        			cout<<"Enter the Value of A=";
                        			cin>>a;	
                        		}
                        		void disp_A()
                        		{
                        			cout<<endl<<"Value of A="<<a;
                        		}
                        };
                        class B: public A
                        {int b,p;
                        	public:
                        		void set_B()
                        		{
                        			set_A();
                        			cout<<"Enter the Value of B=";
                        			cin>>b;
                        		}
                        		void disp_B()
                        		{
                        			disp_A();
                        			cout<<endl<<"Value of B="<<b;
                        		}
                        		void cal_product()
                        		{p=a*b;
                        			cout<<endl<<"Product of "<<a<<" * "<<b<<" = "<<p;
                        		}
                        		};
                        int main()
                        { B _b;
                        	_b.set_B();
                        	_b.cal_product();
                        	return 0;}


Creating object of sub class will invoke the constructor of base classes

********
1. class ABC : private XYZ              //private derivation
            {                }
2. class ABC : public XYZ              //public derivation
            {               }
3. class ABC : protected XYZ              //protected derivation
            {              }
4. class ABC: XYZ                            //private derivation by default
{            }

***********


# Modes of Inheritance: 
**There are 3 modes of inheritance**

Public Mode: If we derive a subclass from a public base class. Then the public member of the base class will become public in the derived class and protected members of the base class will become protected in the derived class.

Protected Mode: If we derive a subclass from a Protected base class. Then both public members and protected members of the base class will become protected in the derived class.

Private Mode: If we derive a subclass from a Private base class. Then both public members and protected members of the base class will become Private in the derived class.
Note: The private members in the base class cannot be directly accessed in the derived class, while protected members can be directly accessed. For example, Classes B, C, and D all contain the variables x, y, and z in the below example. It is just a question of access.  

![table-class](https://github.com/TirthGada/OOPS-notes/assets/118129263/056d499d-6fec-4abc-8690-ebe7c400aa6c)

