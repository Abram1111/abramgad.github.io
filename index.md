# Const uses

## 1 Binding some temporary to reference-to-const, to lengthen its lifetime. 

## EX

   -> ScopeGuard const& guard = MakeGuard(&cleanUpFunction);

## 2 Use const to tell others methods won't change the logical state of this object.
## EX

   -> struct SmartPtr {
   
    int getCopies() const { return mCopiesMade; }
    
};

## 3 Use const for copy-on-write classes, to make the compiler help you to decide when and when not you need to copy.
## EX


->  struct MyString {

    char * getData() { /* copy: caller might write */ return mData; }
    char const* getData() const { return mData; }
    
};

## 4 For the copy-constructor to make copies from const objects and temporaries
## EX

->   struct MyClass {

    MyClass(MyClass const& that) { /* make copy of that */ }
    
};

## 5 For making constants that trivially can't change

## EX

->   double const PI = 3.1415;

## 6 For passing arbitrary objects by reference instead of by value - to prevent possibly expensive or impossible by-value passing
## EX

->    void PrintIt(Object const& obj) {

    // ...
    
}
_______________________________________________________________________________________________________________________________________________________
# The use of & in C
## •	Logical-and
 if ( ( a>1 ) && (b<0) ) 
## •	Bitwise-and
 x = a&b; Corresponding bits are and'ed (e.g. 0&1 -> 0)
## •	Bitwise-and-assign
x &= y; Means the same as: x = x&y;
## •	Address-of operator
p = &x; Read: Assign to p (a pointer) the address of x.
## •	The additional use of & (in parameters) in C++
C++ uses a type of variable called a "reference" variable (or simply a "reference") which is not available in C (although the same effect can be achieved using pointers). References, pointers and addresses are closely related concepts. Addresses are addresses in computer memory (typically the address in memory where the value of some variable is stored), e.g. (in hexadecimal) 0xAB32C2. Pointers are variables which hold addresses, and so "point to" memory locations (and thus to the values of variables). Conceptually, reference variables are basically pointers by another name (but may not be instantiated as such by the compiler).

It is possible to declare a reference within a function, like other variables, e.g.

void main(void) 
{ 

 int i; 
 int& r = i; 
 ...
 
}

but this is pointless, since the use of the reference is equivalent to the use of the variable it references.
References are designed to be used as parameters (arguments) to functions, e.g.

void f(int& r);


void main(void) 
{

  int i=3;
  f(i); 
  printf("%d",i); 
  
}


void f(int& r) 

{ 

  r = 2*r; 

}

This program prints "6" (2*r doubles the value of the variable referenced by r, namely, i).
We could do the same in C by declaring f() as void f(int *r), in which case r is a pointer to an int, then calling f() with argument &i (address-of i), and using de-referencing of r within f(), but clearly C++ provides a more elegant way of passing values to functions (by reference) and returning (perhaps multiple) values from functions (without use of a return statement).


