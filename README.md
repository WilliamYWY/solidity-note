# Solidity Note
## Introduction
Soilidity is a programing language that aim to build smart contract or DeFi application which based on eth net.  
This note hope to provide some basic knowledge of this new programing language.  
Let's start!

## Require
* VScode or other IDE that support .sol file
* REMIX (It's a online solidity IDE that can help interact with your contract more conveniently)

## Content
First for all solidity code, they have to start with the version of solidity you want to work with.
```solidity
pragma solidity >= 0.7.0 < 0.9.0;

```

Then we can define a contract by using the code below, and write all our function, variables or stuff you want within the bracket.
```solidity
contract MyContract{
// function, variables, ...
}

```
- ### Variables  
Like some other programing languages, you need to define the Var first before you use them the format will be like this.
```solidity
// Var-type Scope Var-name = Value;
bool public canVote = true;
int private myAge = 21;
uint internal favNum = 18;
string myName = "William";

```
About the variable's scope, there are three common type:
- public:  
Var can be called by sending message to the contract, called within the contract and the contract derived form it.
- private:  
Var can be called only by the contract that defined it.
- internal:  
var can be called within the contract and the contract derived form it.  

You can also create mapping (dictionary) and array.
```solidity
// array
uint[] public array1; // unlimited size, no default value
uint[10] private array2; //restricted size 10, no default value
uint[] internal array3 = [1,2,3,4,5]; //with default value

//mapping
mapping(string => uint) public mapping1; // (key => value)
```
>Note: There is no float or double in solidity.

- ### Constructor
Like classes in other programing language, you can initialize the value of the contract when you deploy it.  
```solidity
contract MyContract{
    bool public canVote;
    int private myAge;
    
    constructor(bool _canVote, uint _age){
    canVote = _canVote;
    myAge = _age;
    }
}
```
>Note: You need to define the Var type for the parameters.
- ### Function
Solidity also allow you to define functions for interacting within or outside the contract.
```solidity
function doMath(int _num1, int _num2) public pure returns(int, int, int, int){
    int _sum = _num1 + _num2;
    int _sub = _num1 - _num2;
    int _mul = _num1 * _num2;
    int _div = _num1 / _num2;
    // other operation
    
    return (sum, sub, mul, div);
}
```
To define a function, you'll start with the function word and then the function's name, after that are the input parameters.  
>Note: Convertionally we name the local variable by starting with a underscore.  
  
Then we define the scope of the function like the variable, it has public, private, internal and external. 
  
Following is the kind of this function:
- pure: Means that you'll not change any global variables but doing simple calculation or return.
- view: You might will access and return the global variables without changing it.
- payable: Allow transactions.
- BLANK: Not using any decorator here means no previous restriction.

Use returns to define the returned data type and amount.  

>Note: When you use parameters tpye like string, bytes, array and mapping, solidity will ask you to use decorator "**memory**"  
>to store those value in memory space.  
>(string memory _string1)

- ### Logic and Loop
You can also define logic operation and loop in solidity.
- Logic
```solidity
function whatschool(uint _myAge) public view returns(string memory){
    if (_myAge < 20){
        return "stay home";
    } else if (_myAge >= 20 && _myAge < 50){  // &&=and, ||=or
        return "go work!";
    }  
}
```
- Loop
```solidity
function sumNums(uint[] memory _numL) public view returns(uint){
    uint _sum = 0;
    for(uint i = 0; i < _numL.length; i++){ //.length can get the length of a array
        _sum += _numL[i];
    }
    return _sum;
}
```
- ### Error handling 
In solidity there are three functions that can stop the transaction or interaction with the contract.
- require  
Using require the state will return to the state before the transaction and stop the operation below the require function, and the Gas fee won't be taken.
```solidity
// this require myAge bigger than 20 else the error message  "Your age is too small" will raise.
require(myAge >= 20, "Your age is too small");
```
- revert  
Using revert you can stop the process from keep on running, it's working alike require but the requirement is defined by logic.  
Gas fee won't be taken.
```solidity
if (myAge <= 20){
    revert("Your age is too small");
}
```

- assert  
This function usually is used when the problem is fatal, the Gas fee will be taken!
```solidity
assert(myAge <= 20)
```

When the requirement need to be frequently called, you can use "**modifier**".
```solidity
bool canVote = False
modifier available(){
    require(canVote == True, "cannot vote yet");
    _;
}

function vote() public available returns(string memory){
    return "Voted"
}
```
First define the requirement and then add the modifier when you need some functions to follow that requirement.  

- ### Struct, enum
In solidity you can also create struct to store data.
```solidity
struct customer{
    string name;
    string Add;
    uint Age;
}

customer cust1 = customer("William", "Taiwan", 0);
customer[] custL; // a list storing customer struct

function getInfo() public view returns(string memory, string memory, uint){
    return (cust1.name, cust1.Add, cust1.Age)
}
```
Also if you want your variable have restricted option, you can use enum to define the set of option.
```solidity
enum shirtsize{SMALL, MEDIUM, LARAGE}
shirtsize constant defaultSize = shirtsize.MEDIUM;
shirtsize public custsize = defaultSize;
  
function pickShirtSmall() public{
    custsize = shirtsize.SMALL;
}
```

##To do List
- inheritance 
- example
- transaction
- event







