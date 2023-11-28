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




# Practice Project 3

package Practice;

class C{
	
	void msg2() {
		
		int a = 10;
		
		int b = 20;
		
		System.out.println(" "+a+ " "+b);
	}
	
	public static void main(String args[]) {
		
		System.out.println("values of a and b are ");
		
		C value = new C(); //Here we are creating an object to class non static method of same class 
		value.msg2();
		
		D value1 = new D();// Here we are creating an Object to call non static method of other class 
		value1.msg4();
		
        A.msg();       // Here we are Calling static method of java by using its classNmae.methodName
		
	}
}



//METHOD OVERLOADING 

package Practice;

public class MethodOverloading {
	
	static int sub(int x, int y) {
		return ( x-y);
	}
	
	static int add(int x, int y,int z) // Here method name is same but different in number of parameter passed
	{
		return ( x+y+z);
	}
	
	
	
	static double sub(double x, double y) // Here we are using same method name but different in return types 
	{
		
		return (x-y);
	}
	
	static float sub(float x,float y) {
		 return (x-y);
	}

	public static void main(String args[]) {
		
		
		int a = sub(45, 23);  
		double b = sub(23.67,10.5);  
		float  c = sub(35.5f,33.3f);
		int d = add(2,4,5);
		System.out.println("subtraction of integer values: " +a);  
		System.out.println("subtraction of double values: " +b); 
		System.out.println("subtraction of float values: " +c); 
		
		System.out.println("addition of three number is :"+d);
		  
		 
	}
}


//ABSTRACT METHOD CALLING 


package Practice;

abstract class AbstractMethodExample {
	// abstract method declaration

	abstract void show();
}

public class AbstractMethodCalling extends AbstractMethodExample {
//abstract method implementation      
	void show()

	{

		System.out.println("The abstract method called.");
	}

	public static void main(String args[]) {

		AbstractMethodExample obj = new AbstractMethodCalling();
		// calling abstract method
		obj.show();

	}
}





# practice project : 4

//DEFAULT CONSTRUCTOR

package Practice;
import java.io.*;




public class alpha {
	
	alpha()
	{
		System.out.println("Default constructor");
		
	};
	
	public static void main(String args[])
	{
		
		alpha hello = new alpha();
		
	}
	
	

}

//PARAMETERIZED CONSTRUCTOR

package Practice;
import java.io.*;
import java.util.*;


class beta{
	
	String name;
	int id;
	String address;

	
	 beta(String name, int id, String address){
		
		this.name = name;
		this.id = id;
		this.address = address;
	}
	
}


public class alpha {
	
		public static void main(String args[])
	{
		
		alpha hello = new alpha();
		System.out.println("enter name, address and ID_number \n");
		Scanner sc = new Scanner(System.in);
		String name = sc.nextLine();
		String address = sc.nextLine();
		int id = sc.nextInt();
		
		
		
		
		//beta geek1 = new beta("ankush", 12, "india");
		System.out.print("name is "+name+" id_number "+id+"....address is "+address);
		//System.out.println("....address is "+address);
		
	}
	
	

}

//






#practice project5


package Practice;

import java.util.*;

public class collectionAssisted {

	public static void main(String[] args) {
		//creating arraylist
		System.out.println("ArrayList");
		ArrayList<String> city=new ArrayList<String>();   
	      city.add("Bangalore");//
	      city.add("Delhi");    	   
	      System.out.println(city);  
		
		//creating vector
	      System.out.println("\n");
	      System.out.println("Vector");
	      Vector<Integer> vec = new Vector();
	      vec.addElement(15); 
	      vec.addElement(30); 
	      System.out.println(vec);
		
		//creating linkedlist
	      System.out.println("\n");
	      System.out.println("LinkedList");
	      LinkedList<String> names=new LinkedList<String>();  
	      names.add("Alex");  
	      names.add("John");  	      
	      Iterator<String> itr=names.iterator();  
	      while(itr.hasNext()){  
	       System.out.println(itr.next());  
	       
	       //creating hashset
	       System.out.println("\n");
	       System.out.println("HashSet");
	       HashSet<Integer> set=new HashSet<Integer>();  
	       set.add(101);  
	       set.add(103);  
	       set.add(102);
	       set.add(104);
	       System.out.println(set);
	       
	       //creating linkedhashset
	       System.out.println("\n");
	       System.out.println("LinkedHashSet");
	       LinkedHashSet<Integer> set2=new LinkedHashSet<Integer>();  
	       set2.add(11);  
	       set2.add(13);  
	       set2.add(12);
	       set2.add(14);	       
	       System.out.println(set2);
	      	} 
	      }  
	}



 #parctice project 6

package Practice;

import java.util.*;
public class mapDemo {

	public static void main(String[] args) {
		// map
		
		//Hashmap
		HashMap<Integer,String> hm=new HashMap<Integer,String>();      
	      hm.put(1,"Tim");    
	      hm.put(2,"Mary");    
	      hm.put(3,"Catie");   
	       
	      System.out.println("\nThe elements of Hashmap are ");  
	      for(Map.Entry m:hm.entrySet()){    
	       System.out.println(m.getKey()+" "+m.getValue());    
	      }
	      
	     //HashTable
	       
	      Hashtable<Integer,String> ht=new Hashtable<Integer,String>();  
	      
	      ht.put(4,"Ales");  
	      ht.put(5,"Rosy");  
	      ht.put(6,"Jack");  
	      ht.put(7,"John");  

	      System.out.println("\nThe elements of HashTable are ");  
	      for(Map.Entry n:ht.entrySet()){    
	       System.out.println(n.getKey()+" "+n.getValue());    
	      }
	      
	      
	      //TreeMap
	      
	      TreeMap<Integer,String> map=new TreeMap<Integer,String>();    
	      map.put(8,"Annie");    
	      map.put(9,"Carlotte");    
	      map.put(10,"Catie");       
	      
	      System.out.println("\nThe elements of TreeMap are ");  
	      for(Map.Entry l:map.entrySet()){    
	       System.out.println(l.getKey()+" "+l.getValue());    
	      }    
	      
	   }  
}



#practice project7

public class innerClassAssisted1 {

	 private String msg="Welcome to Java"; 
	 
	 class Inner{  
	  void hello(){System.out.println(msg+", Let us start learning Inner Classes");}  
	 }  


	public static void main(String[] args) {

		innerClassAssisted1 obj=new innerClassAssisted1();
		innerClassAssisted1.Inner in=obj.new Inner();  
		in.hello();  
	}
}
public class innerClassAssisted2 {

private String msg="Inner Classes";

 void display(){  
	 class Inner{  
		 void msg(){
 System.out.println(msg);
		 }  
  }  
  
  Inner l=new Inner();  
  l.msg();  
 }  
public static void main(String[] args) {
	innerClassAssisted2  ob=new innerClassAssisted2 ();  
	ob.display();  
	}
}
//anonymous inner class
abstract class AnonymousInnerClass {
	   public abstract void display();
	}

	public class innerClassAssisted3 {

	public static void main(String[] args) {
	AnonymousInnerClass i = new AnonymousInnerClass() {

	         public void display() {
	            System.out.println("Anonymous Inner Class");
	         }
	      };
	      i.display();
	   }
	}



 # practice project 8

public class stringDemo {

	public static void main(String[] args) {
		//methods of strings
		System.out.println("Methods of Strings");
		
		String sl=new String("Hello World");
		System.out.println(sl.length());

		//substring
		String sub=new String("Welcome");
		System.out.println(sub.substring(2));

		//String Comparison
		String s1="Hello";
		String s2="Heldo";
		System.out.println(s1.compareTo(s2));

		//IsEmpty
		String s4="";
		System.out.println(s4.isEmpty());

		//toLowerCase
		String s5="Hello";
		System.out.println(s1.toLowerCase());
		
		//replace
		String s6="Heldo";
		String replace=s2.replace('d', 'l');
		System.out.println(replace);

		//equals
		String x="Welcome to Java";
		String y="WeLcOmE tO JaVa";
		System.out.println(x.equals(y));
 
		System.out.println("\n");
		System.out.println("Creating StringBuffer");
		//Creating StringBuffer and append method
		StringBuffer s=new StringBuffer("Welcome to Java!");
		s.append("Enjoy your learning");
		System.out.println(s);

		//insert method
		s.insert(0, 'w');
		System.out.println(s);

		//replace method
		StringBuffer sb=new StringBuffer("Hello");
		sb.replace(0, 2, "hEl");
		System.out.println(sb);

		//delete method
		sb.delete(0, 1);
		System.out.println(sb);
		
		//StringBuilder
		System.out.println("\n");
		System.out.println("Creating StringBuilder");
		StringBuilder sb1=new StringBuilder("Happy");
		sb1.append("Learning");
		System.out.println(sb1);

		System.out.println(sb1.delete(0, 1));

		System.out.println(sb1.insert(1, "Welcome"));

		System.out.println(sb1.reverse());
				
		//conversion	
		System.out.println("\n");
		System.out.println("Conversion of Strings to StringBuffer and StringBuilder");
		
		String str = "Hello"; 
        
        // conversion from String object to StringBuffer 
        StringBuffer sbr = new StringBuffer(str); 
        sbr.reverse(); 
        System.out.println("String to StringBuffer");
        System.out.println(sbr); 
          
        // conversion from String object to StringBuilder 
        StringBuilder sbl = new StringBuilder(str); 
        sbl.append("world"); 
        System.out.println("String to StringBuilder");
        System.out.println(sbl);              		
	}
}



#practice project 9

package Practice;

import java.util.Arrays;
import java.util.stream.IntStream;

public class ArrayImp {
	
	
	private static void check(int[] arr, int toCheckValue)
    {
        
		
        boolean test = false;
        for (int element : arr) {
            if (element == toCheckValue) {
                test = true;
                break;
            }
        }
 
        // Print the result
        System.out.println("Is " + toCheckValue
                           + " present in the array: " + test);
    }

	public static void main(String[] args) {
		
		// TODO Auto-generated method stub
		
		
        int arr[] = { 5, 1, 1, 9, 7, 2, 6, 10 };
 
        
        int toCheckValue = 7;
 
        
        System.out.println("Array: " + Arrays.toString(arr));
 
        
        
        check(arr, toCheckValue);


		
		
	}

}


#practice project 10

package Practice;


import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class RegexDemo {

	public static void main(String[] args) {

		String text = "I am staying at door no 34. You can call me on 900007654 before 3 pm.";

		String regex = "\\d+";

		Pattern pattern = Pattern.compile(regex);
		Matcher matcher = pattern.matcher(text);

//		boolean b = matcher.matches();
//		System.out.println(b);
//		
//		if (matcher.matches()) {
//			
//			System.out.println("Yes, there are numbers in the given text!");
//			
//		}else {
//			System.out.println("Text does not have any numbers !!");
//		}

		int counter=0;
		while(matcher.find()) {
			System.out.printf("\n Found a match at starting at %s and ending at %s ", matcher.start(), matcher.end());
			counter++;
		};

		// Email matching
		String email = "aksingh@yahoo.co.in";
		String emailRegex = "^[a-zA-Z0-9_.-]+@@(.+)$";
		Pattern emailPattern = Pattern.compile(emailRegex);
		Matcher emailMatcher = emailPattern.matcher(email);

		if(emailMatcher.matches())
		System.out.println("\n The given text is a valid email");
		else System.out.println("\n The given text is NOT a valid email");


	}

}




 


 
