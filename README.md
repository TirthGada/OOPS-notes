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





## MULTILEVEL INHERITANCE
        
        class A
        {
        			protected:
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
        {
        		protected:
        				int b;
        			
        		public:
        				void set_B()
        				{
        					cout<<"Enter the Value of B=";
        					cin>>b;
        				}
        
        		
        				void disp_B()
        				{
        					cout<<endl<<"Value of B="<<b;
        				}
        };
        
        class C: public B
        {
        	int c,p;
        	
        	public:
        		void set_C()
        		{
        				cout<<"Enter the Value of C=";
        				cin>>c;
        		}
        		
        		void disp_C()
        		{
        				cout<<endl<<"Value of C="<<c;
        		}
        	
        			void cal_product()
        			{
        				p=a*b*c;
        				cout<<endl<<"Product of "<<a<<" * "<<b<<" * "<<c<<" = "<<p;
        			}
        };
        
        main()
        {
        	
        	C _c;
        	_c.set_A();
        	_c.set_B();
        	_c.set_C();
        	_c.disp_A();
        	_c.disp_B();
        	_c.disp_C();
        	_c.cal_product();
        	
        	return 0;
        	
        }




## HIERARCHIAL INHERITANCE

Hierarchical Inheritance: In this type of inheritance, more than one subclass is inherited from a single base class. i.e. more than one derived class is created from a single base class.
        
        
## Hybrid (Virtual) Inheritance 
Hybrid Inheritance is implemented by combining more than one type of inheritance. For example: Combining Hierarchical inheritance and Multiple Inheritance. 
Below image shows the combination of hierarchical and multiple inheritances:
        
        
## MULTIPATH INHERITANCE

A derived class with two base classes and these two base classes have one common base class is called multipath inheritance. Ambiguity can arise in this type of inheritance. 
        
        class ClassA {
        public:
        	int a;
        };
        
        class ClassB : public ClassA {
        public:
        	int b;
        };
        
        class ClassC : public ClassA {
        public:
        	int c;
        };
        
        class ClassD : public ClassB, public ClassC {
        public:
        	int d;
        };
        
        int main()
        {
        	ClassD obj;
        
        	// obj.a = 10;				 // Statement 1, Error
        	// obj.a = 100;				 // Statement 2, Error
        
        	obj.ClassB::a = 10; // Statement 3
        	obj.ClassC::a = 100; // Statement 4
        
        	obj.b = 20;
        	obj.c = 30;
        	obj.d = 40;
        
        	cout << " a from ClassB : " << obj.ClassB::a;
        	cout << "\n a from ClassC : " << obj.ClassC::a;
        
        	cout << "\n b : " << obj.b;
        	cout << "\n c : " << obj.c;
        	cout << "\n d : " << obj.d << '\n';
        }
        

**Note: Still, there are two copies of ClassA in Class-D**


************

**Avoiding ambiguity using the virtual base class:**
            
            class ClassA
            {
            public:
            	int a;
            };
            
            class ClassB : virtual public ClassA
            {
            public:
            	int b;
            };
            
            class ClassC : virtual public ClassA
            {
            public:
            	int c;
            };
            
            class ClassD : public ClassB, public ClassC
            {
            public:
            	int d;
            };
            
            int main()
            {
            	ClassD obj;
            
            	obj.a = 10;	 // Statement 3
            	obj.a = 100;	 // Statement 4
            
            	obj.b = 20;
            	obj.c = 30;
            	obj.d = 40;
            
            	cout << "\n a : " << obj.a;
            	cout << "\n b : " << obj.b;
            	cout << "\n c : " << obj.c;
            	cout << "\n d : " << obj.d << '\n';
            }

            OUTPUT
            
            a : 100
            b : 20
            c : 30
            d : 40

 **According to the above example, Class-D has only one copy of ClassA, therefore, statement 4 will overwrite the value of a, given in statement 3**


                        
