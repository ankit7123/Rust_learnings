# Rust_learnings
cargo build - rust-> binary at compile time 
#Immutability 

By default everything is immutable in rust. Need to define if a variable is mutable & we need to change the values. for Ex - 

        fn main() {
            println!("Hello, world!");
            //arrays, maps ,strings 
            //have to mention mutable to change values 
            let mut var : i32 = 344555;
            print!(" {}",var);
            var = 4567;
            print!(" changed values {}", var);
        }
Pros - Avoid memory issues , thread safe :) which leads to optmization from complier's prospective.
Cons - values can be changed , if multiple threads are operating over it :(

Key Learning - Const (jsp)  != immutable (in rust) 

#Memory Management - 

Heap vs Stack 

if variable type is pre-defined then it is stored in stack format for quicker access except string since the data can grow with string ; below is the example - 

      fn main(){ 
      let s1: String = String::from("hello");
      print!("{}",s1)
      }
      
      Stack - predictable compile data   
      fn main() {
          stack_fn();
          heap_fn();
          update_sting_fn();
          
      }
      fn stack_fn(){
      
          let a = 10;
          let b: i32 = 20;
          let c: i32 = a + b ;
          print!("{}",c);
      }
      //declare a string and append with another string 
      fn heap_fn() {
          let s1 = String :: from ("hello");
          let s2 = String :: from ("world");
          let combined = format!("{} {}",s1, s2);
           print!("combined string : {}",combined);
      }
      fn update_sting_fn(){
      // start with base string 
      let mut s = String::from("Initial string");
      print!("before update {}",s);
      println!("Capacity: {},length: {},pointer: {:p}",s.capacity(),s.len(),s.as_ptr());
      
      //appending some string at the end
      s.push_str("some additional text");
      println!("After update: {}",s);
      println!("Capacity: {},length: {},pointer: {:p}",s.capacity(),s.len(),s.as_ptr());
      
      }

#Ownership 
Rust follows some rules on how to govern system memory, where compiler performs some checks. If any one of those rules are voilated the code won't compile. since compile check it doesn't slow down while running.

For the same heap there can not be two pointers from stack. either one of them has to be invalid. the error code is "borrow of moved value: variable "
The solution to above stat. is to clone, which is essentially copying the entire heap.

        fn main() {
            let s1:String = String::from("Hi There");
            print!("{}",s1);
            let s2:String = s1;
            print!("{}",s2);
            print!("{}",s1);//this throws error due to ownership moved from s1 to s2
        }


#Borrowing 
Similar to references , using the reference : below is the example - 
        fn main() {
        
        let mut s1:String = String::from("Hi There");
        print!("{}",s1);
        let s2:&String = &s1;
        print!("{}",s2);
        
        }






      
