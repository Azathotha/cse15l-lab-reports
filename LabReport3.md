# Lab Report 3

## Part 1. Bugs
Choose a bug from ArrayExamples.java reverseInPlace method
- A failure-inducing input:
  ```ruby
  @Test 
	public void testReverseInPlace() {
    int[] input1 = { 3, 8, 2, 9, 4 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 4, 9, 2, 8, 3 }, input1);
	}
  ```
- An input doesn’t induce failure:
  ```ruby
  @Test 
	public void testReverseInPlace() {
    int[] input1 = { 1, 2, 3, 2, 1 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 1, 2, 3, 2, 1 }, input1);
	}
  ```
- Symptom
  - Running with failure-inducing input:
    ![image](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/3/sym_run_fail.png)
  - Running with input doesn’t induce failure:
    ![image](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/3/sym_run_success.png)
- Bug
  - Before change:
  ```ruby
  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
  ```
  - After change:
  ```ruby
  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    int[] newArray = arr.clone();
    for (int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
  }
  ```
  Before fixing the bug, the code works well for the first half of the array; it is overwritten by the reversed second half of the array.
  But for the second half of the array, it was not correctly replaced with the reversed first half of the array, because the first half was
  already overwritten. By creating a new copy of the original array and write it reversly to the original array, the array is correctly reversed.
## Part 2. Researching Commands
I choose the "find" command for this task. 
- -type
  - Find all directories:
  ```ruby
  $ find -type d
  
  .
  ./even-more-files
  ./more-files
  ./more-files/some-more-files
  ./b.txt
  ```
  Source: [Linux Find Command Examples](https://www.binarytides.com/linux-find-command-examples/)
  - Find all executable files:
  ```ruby
  $ find -type f -executable
  
  ./.git/hooks/sendemail-validate.sample
  ./.git/hooks/prepare-commit-msg.sample
  ./.git/hooks/pre-push.sample
  ./.git/hooks/pre-rebase.sample
  ...
  ```
  Source: [Linux Find Command Examples](https://www.binarytides.com/linux-find-command-examples/)
- -name
  - Find all files named "b.txt":
  ```ruby
  $ find -type f -name "b.txt"
  
  ./some-files/even-more-files/b.txt
  ./some-files/more-files/b.txt
  ```
  Source: [Linux Find Command Examples](https://www.binarytides.com/linux-find-command-examples/)
  - Find all java files:
  ```ruby
  $ find -type f -name "*.java"
  
  ./quiz-layout/classes/cse/ExampleClass.java
  ./some-files/even-more-files/d.java
  ./some-files/more-files/c.java
  ./Read.java
  ```
  Source: [Linux Find Command Examples](https://www.binarytides.com/linux-find-command-examples/)
- -mtime
  - Find files modified in the last 7 days:
  ```ruby
  $ find -type f -mtime -7
  
  ./a.txt
  ./even-more-files/a.txt
  ./even-more-files/d.java
  ./even-more-files/b.txt
  ./more-files/b.txt
  ./more-files/c.java
  ./files.txt
  ```
  Source: [Linux Find Command Examples](https://www.binarytides.com/linux-find-command-examples/)
  - Find files accessed in the last 50 days:
  ```ruby
  $ find -type f -atime -7
  
  ./a.txt
  ./even-more-files/a.txt
  ./even-more-files/d.java
  ./even-more-files/b.txt
  ./more-files/b.txt
  ./more-files/c.java
  ./files.txt
  ```
  Source: [Linux Find Command Examples](https://www.binarytides.com/linux-find-command-examples/)
- -size
  - Find all files larger than 2KB:
  ```ruby
  $ find -type f -size 2k
  
  ./.git/objects/pack/pack-a98a6300614eec431298fd6769ceb9c56831aea0.idx
  ./.git/objects/pack/pack-a98a6300614eec431298fd6769ceb9c56831aea0.pack
  ./.git/hooks/prepare-commit-msg.sample
  ./.git/hooks/pre-push.sample
  ./.git/hooks/pre-commit.sample
  ```
  Source: [Linux Find Command Examples](https://www.binarytides.com/linux-find-command-examples/)
  - Find all files smaller than 1KB:
  ```ruby
  find -type f -size -1k
  
  ./quiz-layout/classes/history/turing.txt
  ./quiz-layout/classes/history/liskov.txt
  ./quiz-layout/classes/history/lovelace.txt
  ./quiz-layout/classes/history/history-of-computing.pdf
  ...
  ```
  Source: [Linux Find Command Examples](https://www.binarytides.com/linux-find-command-examples/)
