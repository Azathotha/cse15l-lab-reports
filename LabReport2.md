# Lab Report 2
## Part 1. StringServer
```ruby
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    static int count = 0;
    String str = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("Strings: %s", str);
        }
        else {
            if (url.getPath().contains("/add-message")) {
                String[] strings = url.getQuery().split("=");
                if (strings[0].equals("s")) {
                    count++;
                    strings[1] = strings[1].replace("+"," ");
                    str += "\n" + count + ". " + strings[1];
                    return String.format("New string added: %s! The stored strings are now: %s", strings[1], str);
                }
            }
            return "404 Not Found!";
        }
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
### 1. /add-message example 1
![add-message_screenshot_1](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/use_add-message_1.png)
- Methods Called: handleRequest(URI url) in the Handler class
- Relevant Arguments: The URI object representing the URL of the request. In this case, the path is "/add-message" and the query is "s=apple".
- Relevant Fields:
  - count: It's incremented from 0 to 1.
  - str: It's updated to "1. apple".
- Changes in Relevant Fields: count is incremented, and str is updated to include the new string "1. apple".
### 2. /add-message example 2
![add-message_screenshot_2](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/use_add-message_2.png)
- Methods Called: handleRequest(URI url) in the Handler class
- Relevant Arguments: The URI object representing the URL of the request. In this case, the path is "/add-message" and the query is "s=How+am+I".
- Relevant Fields:
  - count: It's incremented from 1 to 2.
  - str: It's updated to "1. apple\n2. How am I".
- Changes in Relevant Fields: count is incremented, and str is updated to include the new string "2. How am I".

## Part 2. Key
- respond to the two feedbacks(ls using the whole path):
  ![whole_path](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/Whole_pass_SSH_keys.png)
- The path to the private and public key for my SSH key for logging into ieng6
  ![key_path](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/pri_pub_SSH_key.png)
- Log into ieng6 with course-specific account without a password
  ![login_no_pass](https://github.com/Azathotha/cse15l-lab-reports/blob/main/images/login_without_psw.png)

## Part 3. Reflection
I learned how to connect to a remote server; build, run, change and write web servers, including using url to handle the web server; different components of url; how to run web servers on my own computer; set up SSH keys.
