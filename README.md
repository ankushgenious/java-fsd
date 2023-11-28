# java-fsd
This repository contains PracticeProjects
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

