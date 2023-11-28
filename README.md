# java-fsd
This repository contains PracticeProjects


# Practice-Project 1

package Practice;

public class TypeCasting {
	
	public static void main(String args[]) {
		
		int a = 10;
		
		
		long l = a;  //implicit TypeCasting 
		
		float f = l;
		
		System.out.println("Implicit TypeCasting values are");
		
		//print all the values 
		
		System.out.println("int value " +a);
		
		System.out.println("int value " +l);
		
		System.out.println("int value " +f);
		
		System.out.println("\n");
		
		
		//program for explicit TypeCating
		
		System.out.println("Explicit TypeCasting values are");
		
		double d = 10.55;
		
		long l2 = (long) d;
		
		int i  = (int)l2;
		
		System.out.println("double value "+ d);
		
		System.out.println("long value will be "+l2);
		
		System.out.println("integer value will be "+i);
		
		
		
		
	}

}





#  Practice-Project 2
// Implimentation of Private Access Modifiers 

package Practice;

class Print {

	int value1 = 100;
	private int value2 = 400;

	private void msg() {

		System.out.println("Hello java");
	}
}

public class A {

	public static void main(String args[]) {

		Print obj = new Print();
		System.out.println(obj.value2);// Compile Time error because of value declared as private and cannot be fetched
										// outside of class

		System.out.println(obj.value1); // since here value1 is accessible because of its declaration is default

		obj.msg();// Here we cannot access the content inside the msg class since it is declared
					// as private
	}
}



//Default Accesss Modifiers 

package Practice;

 class A{
	 
	  static void  msg() {
		 
		 System.out.println("hello");
	 }
	
	public static void main(String args[]) {
		
		System.out.println(" we are going to call msg method Let's see");
		
		msg();
		
		C value = new C();  // here by creating an object we can call values outside classA but within same package Practice
		value.msg2();
		
	}
}

package Practice;

class C{
	
	void msg2() {
		
		int a = 10;
		
		int b = 20;
		
		System.out.println(" "+a+ " "+b);
	}
	
	public static void main(String args[]) {
		
		System.out.println("values of a and b are ");
		
		C value = new C();
		value.msg2();
        
		
	}
}



// PROTECTED ACCESS MODIFIERS 

package Practice;

import Practice2.B;

 class A extends B{
	 
	  static void  msg() {
		 
		 System.out.println("hello");
	 }
	
	public static void main(String args[]) {
		
		System.out.println(" we are going to call msg3 method Let's see");
		
		
		B val = new B();
		//Here we are creating an object to call method outside the package with help of inherit classB(of other package Practice2 inside our class A 
		val.msg3();
		
	}
}

package Practice2;


public class B {
	
	protected static void msg3() {
		
		int x = 20;
		int y =35;
		
		System.out.println("values of X and Y are "+x +"and  "+y );
		
	}

	public static void main(String args[]) {
		
		msg3();
	}
}



//PUBLIC ACCESS MODIFIERS

package Practice;

import  Practice2.*;

 public class A{
	 
	  public static void  msg() {
		 
		 System.out.println("hello");
	 }
	
	public static void main(String args[]) {
		
		System.out.println(" we are going to call msg3 method Let's see");
		
		msg();
		
		B val = new B();
		val.msg3();       // here we can call the method of other package without extending class B of pratice2 package
		
		
				
		
	}
}




