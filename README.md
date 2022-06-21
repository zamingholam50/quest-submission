## Chapter 1 day 1

1. Explain what the Blockchain is in your own words. You can read this to help you, but you don't have to: https://www.investopedia.com/terms/b/blockchain.asp
A blockchain is a decentralized mechanism to store data.

2. Explain what a Smart Contract is. You can read this to help you, but you don't have to: https://www.ibm.com/topics/smart-contracts
A smart contract is the program that defines functionality that a user can interact with.Smart contracts are deployed to the blockchain to enable others to interact with it.

3. Explain the difference between a script and a transaction.
A script allows you to read data from the blockchain and does not cost any money. A transaction allows you to modify data on the blockchain and incurs a cost.

## Chapter 1 day 2


1. What are the 5 Cadence Programming Language Pillars?
Safety and Security, Clarity, Approachability, Developer Experience, and Resource Oriented Programming.

2. In your opinion, even without knowing anything about the Blockchain or coding, why could the 5 Pillars be useful (you don't have to answer this for #5)?
Safety and Security - ensure that users and developers can not perform malicious actions
Clarity - easier for users to understand what the smart contract is doing
Approachability - easy for new developers to get started
Developer Experience - allows developers to be more productive

## day1

deploy the contract

```cadence

pub contract JacobTucker {
    pub let is: String

    init() {
        self.is = "The best"
    }
}

```


heck that your variable is actually equals "the best" by executing a script to read that variable. Include a screenshot of the output.


import JacobTucker from 0x01

pub fun main(): String {
  return JacobTucker.is
  }
  
 
 
 ## day2
 
Explain why we wouldn't call changeGreeting in a script.

  Only  reads the data, but does not change it in any way. For the purpose of depositing funds

What does the AuthAccount mean in the prepare phase of the transaction?

  acquiring access to the user's log information in the preparatory stage

What is the difference between the prepare phase and the execute phase in the transaction?

  in preparation if you have access to the information/data in your assessment book. not in progress with us

Add two new things inside your contract: A variable named myNumber that has type Int (set it to 0 when the contract is deployed) A function named updateMyNumber that takes in a new number named newNumber as a parameter that has type Int and updates myNumber to be newNumber


```cadence
pub contract HelloWorld {

    pub var greeting: String
    pub var mypoint : Int

    init() {
        self.greeting = "Hello, World!"
        self.mypoint = 0
    }

    pub fun changeGreeting(newGreeting: String) {
        self.greeting = newGreeting
    }

    pub fun updateMypoint(newpoint : Int) {
        self.mypoint = newpoint
    }
}

```



Add a script that reads myNumber from the contract


```cadence
Add a script that reads mypoint from the contract

import HelloWorld from 0x01

pub fun main(): String {
    log(HelloWorld.greeting)
    log(HelloWorld.mypoint)

    return HelloWorld.greeting
}

```


Add a transaction that takes in a parameter named myNewNumber and passes it into the updateMyNumber function. Verify that your number changed by running the script again.

```cadence
import HelloWorld from 0x01

transaction(myNewGreeting: String, myNewpoint: Int) {

  prepare(signer: AuthAccount) {}

  execute {
    HelloWorld.changeGreeting(newGreeting: myNewGreeting)
    HelloWorld.updateMypoint(newpoint: myNewpoint)
  }
}

```


### day3


```cadence

In a script, initialize an array (that has length == 3) of your favourite people, represented as Strings, and log it.

pub fun main() {
    var favPpl: [String] = ["Duke", "Sara", "Fable"]
    log(favPpl)
}

```



In a script, initialize a dictionary that maps the Strings Facebook, Instagram, Twitter, YouTube, Reddit, and LinkedIn to a UInt64 that represents the order in which you use them from most to least. For example, YouTube --> 1, Reddit --> 2, etc. If you've never used one before, map it to 0!

```cadence
pub fun main() {
    var socialMedias: {String: UInt64} = {"Facebook": 1, "Instagram": 2, "Twitter": 1, "YouTube": 3, "Reddit": 1, "LinkedIn" : 1}
    log(socialMedias)
}

```


Explain what the force unwrap operator ! does, with an example different from the one I showed you (you can just change the type).

Dictionaries give an optional role, in this case it means the absence of any role. Force deployment informs about an error code in case the role is also equal to zero instead of the predicted kind. In the case of public music thrown earlier, in case I try to read the role with the target, it returns zero, the probability that the lexicographic mark is not available at all, and also, for the purpose of the design error, a forced sweep manager is needed.

Using this picture below, explain...

What the error message means

I strive to return the line, but in the very process we give away an optional line. Why do I get this error
because of this, the fact that dictionaries give optional characteristics to the presence of access. This is coupled with the fact that the mark you are looking for can not work in any way. How to correct this
Perfectly return the optional role "String?" and also let the method of tolerance cultivate all sorts of errors. In the options property, use Force Unwrap "thing[0x03]!" dispatcher in error return statement if null


### DAY4


Deploy a new contract that has a Struct of your choosing inside of it (must be different than Profile). Create a dictionary or array that contains the Struct you defined. Create a function to add to that array/dictionary.

Create a dictionary or array that contains the Struct you defined

Create a function to add to that array/dictionary.





```cadence

pub contract Login {

    pub var profiles: {Address: Profile}
    
    pub struct Profile {
        pub let rowNext: String
        pub let account: Address

        init(_rowNext: String, _account: Address) {
            self.rowNext = _rowNext
            self.account = _account
        }
    }

    pub fun addProfile(rowNext: String, account: Address) {
        let newProfile = Profile(_rowNext: rowNext, _account: account)
        self.profiles[account] = newProfile
    }

    init() {
        self.profiles = {}
    }

}

```

Add a transaction to call that function in step 3.

```cadence

import Login from 0x01

transaction(rowNext: String, account: Address) {

    prepare(signer: LoginAccount) {}

    execute {
        Login.addProfile(rowNext: rowNext, account: account)
        log("Done.")
    }
}

```


Add a script to read the Struct you defined.

```cadence

import Login from 0x01

pub fun main(account: Address): Login.Profile {
    return Login.people[account]!
}

```



## day1

In words, list 3 reasons why structs are different from resources

Able to act only in 1 resource variant
messages are necessarily "moved" among locations, and also do not have
Resources must be intentionally generated, as well as liquidated


Describe a situation where a resource might be better to use than a struct

I think it can be used in ntf, because it is ideal for these purposes.

What is the keyword to make a new resource

create

Can a resource be created in a script or transaction (assuming there isn't a public function to create one)?

The main word to form can be applied only within the boundaries of the contract.

What is the type of the resource below?


Jacob type resource

Let's play the "I Spy" game from when we were kids. I Spy 4 things wrong with this code. Please fix them.\


```cadence

pub contract Test {

    // Hint: There's nothing wrong here ;)
    pub resource Jacob {
        pub let rocks: Bool
        init() {
            self.rocks = true
        }
    }

    pub fun createJacob(): @Jacob { 
        let myJacob <- create Jacob() 
        return <- myJacob 
    }
}

```


## Day2


```Cadence

pub contract SmartContract {

    pub var myArray: @[char]
    pub var myDictionary: @{String: char}

    pub resource char {
        pub let message: String

        init() {
            self.message = "i'm message for array"
        }
    }


    pub fun array(char: @char) {
        self.myArray.append(<- char)
    }

    pub fun dicrionary(char: @char) {
        let key = char.message

        let oldchar <- self.myDictionary[key] <- char
        destroy oldchar
    }


    pub fun removeFromMyArray(index: Int): @char {
        return <- self.myArray.remove(at: index)

    }

    pub fun removeFromDictionary(key: String): @char {
        let char <- self.myDictionary.remove(key: key) ?? panic("Could not find CHAR")
        return <- char
    }




    init() {
        self.myArray <- []
        self.myDictionary <- {}
    }

}

```


## Day3

Define your own contract that stores a dictionary of resources. Add a function to get a reference to one of the resources in the dictionary.

```cadence

pub contract NFTs {

    pub var NFTset: @{UInt64: toolsNFT}

    pub fun dogReference(key: UInt64): &toolsNFT {
        return &self.NFTset[key] as &toolsNFT
    }

    pub fun addNFT(id: UInt64, toolsName: String, gender: String, color: String) {
        let toolsNFTdetail <- create toolsNFT(_id: id, _toolsName: toolsName, _color: color)
        self.NFTset[toolsNFTdetail.id] <-! toolsNFTdetail
    }

    pub resource toolsNFT {
        pub var id: UInt64
        pub var toolsName: String
        pub var color: String

        init(_id: UInt64, _toolsName: String, _color: String, _age: UInt64) {
            self.id = _id
            self.toolsName = _toolsName
            self.color = _color
        }
    }

    init(){
        self.NFTset <- {}
    }
}
```


```cadence
import NFTs from 0x01

pub fun main(key: UInt64): &toolsNFTs.toolsNFT {
  
  return toolsNFTs.toolsReference(key: key)
}

```

## Day4

Explain, in your own words, the 2 things resource interfaces can be used for (we went over both in today's content)


Limitation of access to data regarding the stay or functions. If the source contains a method interconnected with it, the brewer must be able to notice it, but the graphic artist may not need to
The formation of various sets of laws for the purpose of various additions, together with the use of the 1st and also this resource. The source is able to be used by a merchant or a buyer, and also anyone with them is able to have different abilities or data, but both have every chance to use the only one, and also this material source.

Define your own contract. Make your own resource interface and a resource that implements the interface. Create 2 functions. In the 1st function, show an example of not restricting the type of the resource and accessing its content. In the 2nd function, show an example of restricting the type of the resource and NOT being able to access its content./

```cadence
pub resource interface CAR {
        pub var name: String
        pub var retailPrice : UFix64
    }

    pub resource carelem : CAR {
        pub var retailPrice : UFix64
        pub var name: String
        pub var style: String


        init(_CARName: String, _style: String, _abv : UFix64, _ibu : UFix64){
            self.name = _carName
            self.style = _style

            self.retailPrice = 200000.0

        }
    }
    
```
    
    
How would we fix this code?


```cadence

pub contract Stuff {

    pub struct interface ITest {
      pub var greeting: String
      pub var favouriteFruit: String
      pub fun changeGreeting(newGreeting: String): String //i add this
    }

    pub struct Test: ITest {
      pub var greeting: String
      pub var favouriteFruit: String //and this added

      pub fun changeGreeting(newGreeting: String): String {
        self.greeting = newGreeting
        return self.greeting // returns the new greeting
      }

      init() {
        self.greeting = "Hello!"
        self.favouriteFruit = "Apple" //and 3
      }
    }

    pub fun fixThis() {
      let test: Test{ITest} = Test()
      let newGreeting = test.changeGreeting(newGreeting: "Bonjour!")
      log(newGreeting)
    }
}

```
## Day5

For today's quest, you will be looking at a contract and a script. You will be looking at 4 variables (a, b, c, d) and 3 functions (publicFunc, contractFunc, privateFunc) defined in SomeContract. In each AREA (1, 2, 3, and 4), I want you to do the following: for each variable (a, b, c, and d), tell me in which areas they can be read (read scope) and which areas they can be modified (write scope). For each function (publicFunc, contractFunc, and privateFunc), simply tell me where they can be called.

access(all) contract SomeContract {
    pub var testStruct: SomeStruct

    pub struct SomeStruct {

        //
        // 4 Variables
        //

        pub(set) var a: String

        pub var b: String

        access(contract) var c: String

        access(self) var d: String

        //
        // 3 Functions
        //

        pub fun publicFunc() {}

        access(contract) fun contractFunc() {}

        access(self) fun privateFunc() {}


        pub fun structFunc() {
            /****************/
            /**** AREA 1 ****/
            /* a R/W        */
            /* b R/W        */
            /* c R/W        */
            /* d R/W        */
            /* publicFunc   */
            /* contractFunc */
            /* privateFunc  */
            /****************/
        }

        init() {
            self.a = "a"
            self.b = "b"
            self.c = "c"
            self.d = "d"
        }
    }

    pub resource SomeResource {
        pub var e: Int

        pub fun resourceFunc() {
            /****************/
            /**** AREA 2 ****/
            /* a R/W        */
            /* b R          */
            /* c R          */
            /* d            */
            /* publicFunc   */
            /* contractFunc */
            /****************/
        }

        init() {
            self.e = 17
        }
    }

    pub fun createSomeResource(): @SomeResource {
        return <- create SomeResource()
    }

    pub fun questsAreFun() {
        /****************/
        /**** AREA 3 ****/
        /* a R/W        */
        /* b R          */
        /* c R          */
        /* d            */
        /* publicFunc   */
        /* contractFunc */
        /****************/
    }

    init() {
        self.testStruct = SomeStruct()
    }
}
This is a script that imports the contract above:

import SomeContract from 0x01

pub fun main() {
  /****************/
  /**** AREA 3 ****/
  /* a R/W        */
  /* b R          */
  /* c            */
  /* d            */
  /* publicFunc   */
  /****************/
}


## day1

Explain, in your own words, the 2 things resource interfaces can be used for (we went over both in today's content)
1. Interfaces can be used to define requirements that must be implemented.
2. Interfaces can be used to restrict access to certain things.

3. How would we fix this code?

pub contract Stuff {

    pub struct interface ITest {
      pub var greeting: String
      pub var favouriteFruit: String
      pub fun changeGreeting(newGreeting: String): String // Added
    }

    // ERROR:
    // `structure Stuff.Test does not conform 
    // to structure interface Stuff.ITest`
    pub struct Test: ITest {
      pub var greeting: String
      pub var favouriteFruit: String // Added

      pub fun changeGreeting(newGreeting: String): String {
        self.greeting = newGreeting
        return self.greeting // returns the new greeting
      }

      init() {
        self.greeting = "Hello!"
      }
    }

    pub fun fixThis() {
      let test: Test{ITest} = Test()
      let newGreeting = test.changeGreeting(newGreeting: "Bonjour!") // ERROR HERE: `member of restricted type is not accessible: changeGreeting`
      log(newGreeting)
    }
}

## DAY2

111 What does .link() do?
.link() creates a link for the purpose of allowing traffic where the /public/private facilities make it easily accessible

222 In your own words (no code), explain how we can use resource interfaces to only expose certain things to the /public/ path.

Having defined unstable functions along with the target, as well as it would be desirable to apply as well as a public access method to the resource interface, we began to use them together with the target of granting to the resource, accessing the resource in accordance with the /public/ direction.


pub contract Store  {
    pub resource interface Iproducts {
        pub let item: String 
    }
    pub resource products: Iproducts {
        pub let item: String
        init() {
        self.item = "hp omen 15"
        } 
    }
    pub fun createproducts(): @products {
        return <- create  products()
    }
}


import Store from 0x01
transaction() {
  prepare(signer: AuthAccount) {
    signer.save(<- Store.createproducts(), to:/storage/MyStore)
  }
  execute {}
} 


import Store from 0x01
transaction() {
  prepare(signer: AuthAccount) {
    let myproducts <- signer.load<@Store.products>(from: /storage/MyStore)
                    ?? panic("No products")
    log(myproducts.item)
    destroy myproducts;
  }
  execute {}
} 



import Store from 0x01
transaction() {
  prepare(signer: AuthAccount) {
    let myproducts = signer.borrow<&Store.products>(from: /storage/MyStore)
                    ?? panic("No products")
    log(myproducts.item)
  }
  execute {}
}



## day3

. Why did we add a Collection to this contract? List the two main reasons.
Collection was used to reduce the number of storage paths for multiple items and to enable others to put things in the Collection.  

2. What do you have to do if you have resources "nested" inside of another resource? ("Nested resources")
You must have a destroy function that destroys the nested resources.

3. Brainstorm some extra things we may want to add to this contract. Think about what might be problematic with this contract and how we could fix it.

Idea #1: Do we really want everyone to be able to mint an NFT? 🤔.
Change access of createNFT() to access(account).

Idea #2: If we want to read information about our NFTs inside our Collection, right now we have to take it out of the Collection to do so. Is this good?
We could add a function to return a reference to an NFT in the collection or iterates over references to the NFTs.


## DAY4


Because we had a LOT to talk about during this Chapter, I want you to do the following:
Take our NFT contract so far and add comments to every single resource or function explaining what it's doing in your own words. Something like this:





```cadence

pub contract CryptoPoops {
pub var totalSupply: UInt64

// This NFT source includes an area as well as a personal number as well as a number of empty metadata.

pub resource NFT {
    pub let id: UInt64

    pub let name: String
    pub let favouriteFood: String
    pub let luckyNumber: Int

    init(_name: String, _favouriteFood: String, _luckyNumber: Int) {
    self.id = self.uuid

    self.name = _name
    self.favouriteFood = _favouriteFood
    self.luckyNumber = _luckyNumber
    }
}

// This resource socket sets the available methods for our NFT collection target.

pub resource interface CollectionPublic {
    pub fun deposit(token: @NFT)
    pub fun getIDs(): [UInt64]
    pub fun borrowNFT(id: UInt64): &NFT
}

// This is our selection of NFTs, it is she who will carry out the socket of the available meeting and also saves our NFTs, allowing you to enter, remove and also borrow NFTs.

pub resource Collection: CollectionPublic {
    pub var ownedNFTs: @{UInt64: NFT}

    // This role is used to add NFTs to the collection.

    pub fun deposit(token: @NFT) {
    self.ownedNFTs[token.id] <-! token
    }

    //This role is used for the purpose of concluding an NFT with a meeting.

    pub fun withdraw(withdrawID: UInt64): @NFT {
    let nft <- self.ownedNFTs.remove(key: withdrawID) 
            ?? panic("This NFT does not exist in this Collection.")
    return <- nft
    }

    //Gives all, without exception, personal NFT numbers that belong to NFT.

    pub fun getIDs(): [UInt64] {
    return self.ownedNFTs.keys
    }

    //It is used to borrow NFT and also read its metadata in the absence of pulling out from the meeting.

    pub fun borrowNFT(id: UInt64): &NFT {
    return &self.ownedNFTs[id] as &NFT
    }

    // excited by the presence of the formation of the assembly and also forms a useless lexicon that belong to the NFT.

    init() {
    self.ownedNFTs <- {}
    }
    
    // obviously destroys the invested lexicon of resources by the presence of the liquidation of the meeting.

    destroy() {
    destroy self.ownedNFTs
    }
}

//Forms an empty collection and also gives it to the transaction that generates it.

pub fun createEmptyCollection(): @Collection {
    return <- create Collection()
}

// this is the source of the Minter, which is considered to be a single section along with the code for the purpose of forming NFTs or additional minters.

pub resource Minter {
    // Forms an NFT and also gives it to the transaction that activates the function.

    pub fun createNFT(name: String, favouriteFood: String, luckyNumber: Int): @NFT {
    return <- create NFT(_name: name, _favouriteFood: favouriteFood, _luckyNumber: luckyNumber)
    }

    // generates another source of Minter, giving someone else to mint NFT.

    pub fun createMinter(): @Minter {
    return <- create Minter()
    }

}

// the presence of the contract deployment is invoked by assigning the unstable Supply the role 0 and also keeping the Minter source in the account base.

init() {
    self.totalSupply = 0
    self.account.save(<- create Minter(), to: /storage/Minter)
}
}

```

1. Describe what an event is, and why it might be useful to a client.
An event allows a contract to inform clients of actions that took place under the contract.

4. For each of the functions below (numberOne, numberTwo, numberThree), follow the instructions.

pub contract Test {

  // TODO
  // Tell me whether or not this function will log the name.
  // name: 'Jacob'
  // Yes
  pub fun numberOne(name: String) {
    pre {
      name.length == 5: "This name is not cool enough."
    }
    log(name)
  }

  // TODO
  // Tell me whether or not this function will return a value.
  // name: 'Jacob'
  // Yes
  pub fun numberTwo(name: String): String {
    pre {
      name.length >= 0: "You must input a valid name."
    }
    post {
      result == "Jacob Tucker"
    }
    return name.concat(" Tucker")
  }

  pub resource TestResource {
    pub var number: Int

    // TODO
    // Tell me whether or not this function will log the updated number.
    // Also, tell me the value of `self.number` after it's run.
    // No. Self.number will equal 0 after it's run
    pub fun numberThree(): Int {
      post {
        before(self.number) == result + 1
      }
      self.number = self.number + 1
      return self.number
    }

    init() {
      self.number = 0
    }

  }


}



1. Explain why standards can be beneficial to the Flow ecosystem.
Standards are beneficial because it allow interoperability between contracts.				
2. What is YOUR favourite food?
Red oil wontons

3. Please fix this code (Hint: There are two things wrong):

The contract interface:

pub contract interface ITest {
  pub var number: Int
  
  pub fun updateNumber(newNumber: Int) {
    pre {
      newNumber >= 0: "We don't like negative numbers for some reason. We're mean."
    }
    post {
      self.number == newNumber: "Didn't update the number to be the new number."
    }
  }

  pub resource interface IStuff {
    pub var favouriteActivity: String
  }

  pub resource Stuff {
    pub var favouriteActivity: String
  }
}
The implementing contract:

pub contract Test: ITest { // Add contract interface
  pub var number: Int
  
  pub fun updateNumber(newNumber: Int) {
    self.number = 5
  }

  /* This can be deleted since we should be using resource interface defined in contract interface
  pub resource interface IStuff {
    pub var favouriteActivity: String
  }
  */

  pub resource Stuff: ITest.IStuff { // Use resource interface from contract interface
    pub var favouriteActivity: String

    init() {
      self.favouriteActivity = "Playing League of Legends."
    }
  }

  init() {
    self.number = 0
  }
}


/**
## The Flow Non-Fungible Token standard
*/

// The main NFT contract interface. Other NFT contracts will
// import and implement this interface
//
pub contract interface NonFungibleToken {

    pub var totalSupply: UInt64

    pub event ContractInitialized()

    pub event Withdraw(id: UInt64, from: Address?)

    pub event Deposit(id: UInt64, to: Address?)

    pub resource interface INFT {
        // The unique ID that each NFT has
        pub let id: UInt64
    }

    pub resource NFT: INFT {
        pub let id: UInt64
    }

    pub resource interface Provider {
        pub fun withdraw(withdrawID: UInt64): @NFT {
            post {
                result.id == withdrawID: "The ID of the withdrawn token must be the same as the requested ID"
            }
        }
    }

    pub resource interface Receiver {
        pub fun deposit(token: @NFT)
    }

    pub resource interface CollectionPublic {
        pub fun deposit(token: @NFT)
        pub fun getIDs(): [UInt64]
        pub fun borrowNFT(id: UInt64): &NFT
    }

    pub resource Collection: Provider, Receiver, CollectionPublic {

        // Dictionary to hold the NFTs in the Collection
        pub var ownedNFTs: @{UInt64: NFT}

        // withdraw removes an NFT from the collection and moves it to the caller
        pub fun withdraw(withdrawID: UInt64): @NFT

        // deposit takes a NFT and adds it to the collections dictionary
        // and adds the ID to the id array
        pub fun deposit(token: @NFT)

        // getIDs returns an array of the IDs that are in the collection
        pub fun getIDs(): [UInt64]

        // Returns a borrowed reference to an NFT in the collection
        // so that the caller can read data and call methods from it
        pub fun borrowNFT(id: UInt64): &NFT {
            pre {
                self.ownedNFTs[id] != nil: "NFT does not exist in the collection!"
            }
        }
    }

    pub fun createEmptyCollection(): @Collection {
        post {
            result.getIDs().length == 0: "The created collection must be empty!"
        }
    }
}
