# Lab Report 5

## Part 1 – Debugging Scenario
- The original post from a student:
  - Subject: Bug with ListExamples filter method
  - Hi everyone, <br /> <br />
    I'm having some trouble with the filter method in the ListExamples class. I've attached a screenshot of the code and the output I'm getting. I expected the output to be ["banana", "orange", "pear"] since these are the even-length strings in the original list. However, the filtered list's order seems incorrect. Any ideas on what might be causing this? 
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
		StringChecker sc = s -> s.length() % 2 == 0; // filtering even-length strings
		List<String> l1 = new ArrayList<String>(Arrays.asList("apple", "banana", "orange", "grape", "pear")); // original string
		List<String> l2 = new ArrayList<String>(ListExamples.filter(l1, sc)); // set l2 to filtered list
		System.out.println(Arrays.toString(l2.toArray())); //print l2
		assertArrayEquals(new String[]{ "banana", "orange", "pear"}, l2.toArray());
  }
  ```
  - Output:
  ![error_output](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/5/LabReport5_error_output.png)
- 

## Part 2 – Reflection
using jdb, writting grader

