# Lab Report 5

## Part 1 – Debugging Scenario
- The original post from a student:
  - Subject: Bug with ListExamples filter method
  - Hi everyone, <br /> <br />
    I'm having some trouble with the filter method in the ListExamples class. I've attached my code and a screenshot of the output I'm getting. I expected the filter method to filter out the word "filter", and based on my test method, the output should be ["filter", "filter"]. However, the method fails to filter the words based on the output. I have a feeling the bug might be related to how I'm using the StringChecker. Any ideas on what might be causing this? 
  - Here's my code, test method and output:
  - Code:
  ```ruby
    static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0,s);
      }
    }
    return result;
  }
  ```
  - Test method:
  ```ruby
 	public void testFilter() {
		String word = new String("filter");
		StringChecker sc = s -> s == word; // filtering the "filter"
		List<String> l1 = new ArrayList<String>(Arrays.asList("apple", "filter", "orange", "filter", "pear")); // original string
		List<String> l2 = new ArrayList<String>(ListExamples.filter(l1, sc)); // set l2 to filtered list
		System.out.println(l2); //print l2
		assertArrayEquals(new String[]{ "filter", "filter"}, l2.toArray());
        }
  ```
  - Output: <br />
  ![error_output](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/5/LabReport5_e_output.png)
- A response from a TA:
  - Hi,  <br /> <br />
    It looks like you're using == to compare strings in your StringChecker. To better understand what might be going wrong, try printing the result of the expression "s == word" for each string in your list. This will help you see what the == operator is actually comparing. Update your filter method like this:
  ```ruby
    String word = new String("filter");
    for(String s: list) {
      System.out.println("compare with word: " + (s == "filter") + " vs. " +
                         "compare with an string object: " + (s == word));
    if(sc.checkString(s)) {
        result.add(s);
    }
  }
  ```
- Terminal Output after Trying the Suggestion:<br />
  - ![try](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/5/try_output.png)
  - Bug Description:
    After the debugging method, I saw that the == operator is not correctly comparing the strings. The comparison might be based on object references rather than the content of the strings. To fix this issue, I need to use the .equals() method for string comparison.
- Information about the Setup:
  - File & Directory Structure: <br />
    ![structure](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/5/file_structure.png)
  - Contents of Each File Before Fixing the Bug:
    - ListExamples.java
    ```ruby
    	import java.util.ArrayList;
	import java.util.List;
	
	interface StringChecker { boolean checkString(String s); }
	
	class ListExamples {
	
	  // Returns a new list that has all the elements of the input list for which
	  // the StringChecker returns true, and not the elements that return false, in
	  // the same order they appeared in the input list;
	  static List<String> filter(List<String> list, StringChecker sc) {
	    List<String> result = new ArrayList<>();
	    for(String s: list) {
	      if(sc.checkString(s)) {
	        result.add(s);
	      }
	    }
	    return result;
	  }
	
	
	  // Takes two sorted list of strings (so "a" appears before "b" and so on),
	  // and return a new list that has all the strings in both list in sorted order.
	  static List<String> merge(List<String> list1, List<String> list2) {
	    List<String> result = new ArrayList<>();
	    int index1 = 0, index2 = 0;
	    while(index1 < list1.size() && index2 < list2.size()) {
	      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
	        result.add(list1.get(index1));
	        index1 += 1;
	      }
	      else {
	        result.add(list2.get(index2));
	        index2 += 1;
	      }
	    }
	    while(index1 < list1.size()) {
	      result.add(list1.get(index1));
	      index1 += 1;
	    }
	    while(index2 < list2.size()) {
	      result.add(list2.get(index2));
	      // change index1 below to index2 to fix test
	      index2 += 1;
	    }
	    return result;
	  }
	}
    ```
    - ListExamplesTests.java
    ```ruby
    	import static org.junit.Assert.*;
	import org.junit.*;
	import java.util.*;
	import java.util.ArrayList;
	
	
	public class ListExamplesTests {
		@Test(timeout = 500)
		public void testMerge1() {
	    	List<String> l1 = new ArrayList<String>(Arrays.asList("x", "y"));
			List<String> l2 = new ArrayList<String>(Arrays.asList("a", "b"));
			assertArrayEquals(new String[]{ "a", "b", "x", "y"}, ListExamples.merge(l1, l2).toArray());
		}
		
		@Test(timeout = 500)
	        public void testMerge2() {
			List<String> l1 = new ArrayList<String>(Arrays.asList("a", "b", "c"));
			List<String> l2 = new ArrayList<String>(Arrays.asList("c", "d", "e"));
			assertArrayEquals(new String[]{ "a", "b", "c", "c", "d", "e" }, ListExamples.merge(l1, l2).toArray());
	        }
	
		//@Test(timeout = 500)
	        public static void main(String[] args){
			String word = new String("filter");
			StringChecker sc = s -> s == word; // filtering the "filter"
			List<String> l1 = new ArrayList<String>(Arrays.asList("apple", "filter", "orange", "filter", "pear")); // original string
			List<String> l2 = new ArrayList<String>(ListExamples.filter(l1, sc)); // set l2 to filtered list
			System.out.println(l2); //print l2
			assertArrayEquals(new String[]{ "filter", "filter"}, l2.toArray());
	        }
	
	}
 	```
    - test.sh
      ```ruby
      javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
      java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests
      ```
    - Full Command Line to Trigger the Bug:
      ```ruby
      bash test.sh
      ```
    - Description of What to Edit to Fix the Bug:
      In ListExamplesTests.java, update the StringChecker implementation to use .equals() instead of == for string comparison. Here's the corrected code:
      ```ruby
      StringChecker sc = s -> s.equals(word);
      ```

## Part 2 – Reflection
In the second part of the quarter, I learned how to use jdb to figure out and fix problems in Java code. It allowed me to stop the program at certain points, check what's happening, and step through the code step by step. Also, while working on creating a grader, I learned how important it is to have good test cases to properly evaluate and grade code. It was cool to see how these tools, commands and practices can make programming easier and more efficient.

