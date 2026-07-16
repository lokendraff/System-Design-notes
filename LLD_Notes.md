# UML Diagrams for LLD: Quick Revision & Interview Notes 🚀

## 1. Introduction to UML Diagrams
UML (Unified Modeling Language) use karte hain apne application ka idea, structure, aur flow diagrammatically samjhane ke liye. LLD interviews mein code likhne se pehle Class Diagram banana almost mandatory hota hai, taaki interviewer ko aapka thought process samajh aaye.

**Types of UML Diagrams (Mainly 2 types used in LLD):**
1. **Structural Diagrams (Static):** System ka structure kaisa hai, classes aur unke connections (e.g., **Class Diagram**).
2. **Behavioral Diagrams (Dynamic):** System ke components interact kaise karte hain over time (e.g., **Sequence Diagram**).

---

## 2. Class Diagrams (🔥 Very Important for Interviews)
Ye batata hai ki application mein kaun-kaun si classes hain, unke attributes (data) kya hain, methods (behavior) kya hain, aur classes aapas mein connected kaise hain.

### 2.1 Representing a Class
Ek class ko 3 parts (rectangles) mein divide karke represent karte hain:
1. **Top:** Class Name *(Agar abstract class hai, to naam ke upar `<<Abstract>>` likhte hain)*.
2. **Middle:** Attributes / Variables (Format: `variableName: DataType`, e.g., `brand: String`).
3. **Bottom:** Methods / Behavior (Format: `methodName(): ReturnType`, e.g., `startEngine(): void`).

### 2.2 Access Modifiers Representation
Interviewers ye zaroor check karte hain ki aap Data Encapsulation follow kar rahe ho ya nahi.
* `+` : Public (Accessible from anywhere)
* `-` : Private (Accessible only within the class - **Interview Tip: Hamesha variables/attributes ko private rakho!**)
* `#` : Protected (Accessible within class and child classes)

### 2.3 Associations & Relationships (⭐ Interview Favorite)
Classes ke beech mein connections 4 main types ke hote hain:

#### A. Inheritance (IS-A Relationship)
* **Concept:** Child class inherits Parent class. (e.g., `Car` IS-A `Vehicle`).
* **UML Representation:** Solid line with an **empty, closed arrowhead** pointing to the Parent.
* **Interview Tip:** LLD mein deep inheritance trees se bacho. 

#### B. Simple Association (HAS-A Relationship - Weakest)
* **Concept:** Two independent objects are related, but ek dusre ko own nahi karte. (e.g., `User` has an `Address`).
* **UML Representation:** Solid line with an **open arrowhead**.

#### C. Aggregation (HAS-A Relationship - Stronger)
* **Concept:** "Container and Contained" relation, but contained object **independently exist kar sakta hai**. (e.g., `Room` and `Chair`. Room toot jaye, to bhi Chair bachegi).
* **UML Representation:** Solid line with an **empty diamond** at the container side.
* **Java Code Example (Interview Add-on):** Pass the independent object via constructor.
  ```java
  class Room {
      Chair chair;
      // Chair is passed from outside, its lifecycle is independent
      public Room(Chair chair) { 
          this.chair = chair; 
      } 
  }
  ```

#### D. Composition (PART-OF Relationship - Strongest)
* **Concept:** Strict containment. Contained object **CANNOT exist** without the container. (e.g., `Car` and `Engine`. Car destroy hui to Engine bhi logically gaya).
* **UML Representation:** Solid line with a **filled (black) diamond** at the container side.
* **Java Code Example (Interview Add-on):** Instantiate object strictly inside the constructor.
  ```java
  class Car {
      Engine engine;
      public Car() { 
          // Engine's lifecycle is strictly tied to Car
          this.engine = new Engine(); 
      } 
  }
  ```

---

## 3. Sequence Diagrams
Ye batata hai ki objects ek dusre ke saath time ke hisaab se kaise interact karte hain. APIs ka flow ya specific feature ka execution (jaise "ATM Withdrawal Flow") samjhane ke liye best hota hai.

### 3.1 Key Components:
* **Lifeline:** Dotted vertical line showing an object's existence over time.
* **Activation Bar:** Vertical rectangle on the lifeline showing exactly kab object "active" tha (kab code execute ho raha tha).
* **Synchronous Message:** Solid line + **Closed Arrowhead**. Sender response ka wait karta hai.
* **Asynchronous Message:** Solid line + **Open Arrowhead**. Sender wait nahi karta (e.g., sending an email notification or firing an event).
* **Return Message:** Dotted line pointing back to the sender.
* **Create/Destroy Messages:** Create message directly naye object ke box par point karta hai. Destroy hone par lifeline ke end mein 'X' mark hota hai.

### 3.2 Advanced Blocks (Alt, Opt, Loop):
* **Alt (Alternative):** Acts like `if-else` (e.g., If balance > amount, withdraw; else show 'insufficient funds' error).
* **Opt (Optional):** Acts like a simple `if` condition.
* **Loop:** Represents iterations (e.g., retrying PIN entry up to 3 times).

---

## 4. 💡 Interview Pro-Tips (Value-Adds Beyond the Video)

1. **Keep it Relevant:** Interview mein saare getters/setters ya helper methods mat draw karo class diagram mein. Sirf core domain models aur unke relationships par focus karo.
2. **"Favor Composition over Inheritance" (Crucial Design Principle):** Interviewer poochega ki "Kab Inheritance use karein aur kab Composition?".
   * *Answer:* Inheritance breaks encapsulation (child heavily depends on parent). Use Inheritance **only** when there is a strict IS-A relationship and polymorphism is required. Agar aapko bas code reuse karna hai, to **Composition (HAS-A)** use karo. Ye classes ko loosely coupled banata hai.
3. **Interface Realization:** Video mein interfaces ka representation deeply cover nahi tha, but interview mein Java interfaces pooche jaate hain. UML mein use `<<interface>>` likhte hain aur "implements" ko show karne ke liye **dashed line with a closed, empty arrowhead** use karte hain.
4. **Sequence Diagrams in Microservices/Concurrency:** Sequence diagrams are great to show race conditions, locks, ya multi-service interactions (jaise microservices mein payment gateway ka flow). Isko wahan leverage karo!

> **Best of Luck for your LLD Prep! Focus on solidifying object-oriented basics aur SOLID principles, wahi foundation banate hain.**

---


<br>
<br>

---

# SOLID Design Principles - Detailed Notes & Interview Questions

Yeh notes Coder Army ke "SOLID Design Principles" video par based hain. Isme OOPs ke problems aur S, O, L principles ko detail mein cover kiya gaya hai.

---

## 1. Introduction to SOLID Principles & Real-World Problems

### Detailed Notes :
- **Overview:** Real-world projects mein thousands of classes banti hain. Agar in classes ko theek se manage nahi kiya gaya, toh code ek "mess" ban jata hai.
- **Problems without Design Principles:**
  1. **Maintainability Issue:** Naya feature add karne par existing code break ho sakta hai aur changes karna mushkil hota hai.
  2. **Readability Issue:** Naye developers ko tightly coupled aur complex code samajhne mein bohot time lagta hai.
  3. **Bugs & Debugging:** Tightly coupled code ki wajah se bugs easily introduce hote hain aur unhe resolve karne mein bohot zyada time waste hota hai.
- **Solution:** In problems ko solve karne ke liye Robert C. Martin (2000) ne SOLID design principles introduce kiye.
- **SOLID Acronym:**
  - **S:** Single Responsibility Principle (SRP)
  - **O:** Open-Closed Principle (OCP)
  - **L:** Liskov Substitution Principle (LSP)
  - **I:** Interface Segregation Principle (ISP) - *(Next video mein covered)*
  - **D:** Dependency Inversion Principle (DIP) - *(Next video mein covered)*

### 5 Interview Questions & Answers:
**Q1. What is the main purpose of using SOLID design principles?**
*Answer:* SOLID principles ka main purpose software design ko clean, maintainable, aur scalable banana hai. Isse tight coupling avoid hoti hai aur code ko easily extend kiya ja sakta hai without introducing new bugs.

**Q2. Real-world projects mein maintainability issue ka kya matlab hai?**
*Answer:* Maintainability ka matlab hai ki application mein naye features integrate karna aasan ho aur existing code ko kam se kam change karna pade. Tightly coupled code mein changes karne se naye bugs aate hain, jise maintainability issue kehte hain.

**Q3. Who introduced the SOLID principles?**
*Answer:* SOLID principles ko Robert C. Martin ne year 2000 ke aas-paas introduce kiya tha.

**Q4. Tight coupling kya hoti hai? Ek real-world example dein.**
*Answer:* Tight coupling tab hoti hai jab classes ek dusre par bohot zyada dependent hoti hain. Real-world example: Ek ghar mein wiring (electricity, internet, pipe) agar ek hi jagah tightly mixed ho, toh ek fault theek karne ke liye sab kuch disturb karna padta hai.

**Q5. SOLID mein ISP aur DIP ka full form kya hai?**
*Answer:* ISP stands for Interface Segregation Principle aur DIP stands for Dependency Inversion Principle.

---

## 2. Single Responsibility Principle (SRP)

### Detailed Notes (Hinglish):
- **Definition:** "A class should have only one reason to change." Yaani ek class ki sirf ek hi responsibility (ek hi kaam) honi chahiye.
- **Problem Scenario:** Ek `ShoppingCart` class hai jo teen kaam kar rahi hai: 
  1. Total price calculate karna.
  2. Invoice print karna.
  3. Database mein save karna.
  Yeh SRP ko violate karta hai kyunki agar kal ko DB storage logic change karna ho ya invoice ka format change karna ho, toh hume same `ShoppingCart` class ko change karna padega (Multiple reasons to change).
- **Solution (Using Composition):** Is monolithic class ko break karein:
  - `ShoppingCart`: Sirf items store karega aur total calculate karega.
  - `CartInvoicePrinter`: Sirf invoice print karne ka kaam karega (isme Cart ka reference hoga).
  - `CartDBStorage`: Sirf database mein save karne ka logic handle karega.
- **Misconception:** SRP ka matlab yeh nahi hai ki class mein sirf ek hi method ho. Ek class mein kitne bhi methods ho sakte hain, bas un sabka ultimate goal (responsibility) ek hi hona chahiye.


```java

// SRP: Classes handled separate responsibilities

class ShoppingCart {
    public double calculateTotal() { 
        // Logic to calculate total
        return 1500.0; 
    }
}

class CartInvoicePrinter {
    public void printInvoice(ShoppingCart cart) { 
        System.out.println("Printing Invoice for total: " + cart.calculateTotal()); 
    }
}

class CartDBStorage {
    public void saveToDB(ShoppingCart cart) { 
        System.out.println("Saving cart details to Database..."); 
    }
}

```

### 5 Interview Questions & Answers:
**Q1. Single Responsibility Principle (SRP) kya kehta hai?**
*Answer:* SRP kehta hai ki ek class ko change karne ka sirf ek hi reason hona chahiye. In simple terms, ek class ko sirf ek hi specific task ya responsibility handle karni chahiye.

**Q2. Agar ek class multiple kaam kar rahi hai toh usme kya problem aati hai?**
*Answer:* Agar ek class multiple responsibilities handle kar rahi hai, toh kisi ek feature mein change karne se dusre unrelated features break ho sakte hain. Code maintenance mushkil ho jati hai.

**Q3. Kya SRP ka matlab hai ki class mein strictly sirf ek hi method hona chahiye?**
*Answer:* Nahi, SRP ka matlab ek method hona nahi hai. Ek class mein multiple helper methods ho sakte hain, but un sabka aim ek single responsibility ko fulfill karna hona chahiye (e.g. saare methods DB connectivity ke liye ho).

**Q4. ShoppingCart example mein SRP kaise apply kiya gaya?**
*Answer:* ShoppingCart se invoice printing aur DB storage ke logic ko nikal kar do nayi classes (`CartInvoicePrinter` aur `CartDBStorage`) mein daal diya gaya. Ab ShoppingCart sirf price calculation par focus karta hai.

**Q5. SRP follow karne ke main benefits kya hain?**
*Answer:* Code highly readable aur maintainable ban jata hai. Testing easier hoti hai aur version control conflicts (merge conflicts) minimize ho jate hain.

---

## 3. Open-Closed Principle (OCP)

### Detailed Notes (Hinglish):
- **Definition:** "A class should be open for extension but closed for modification." Yaani naye features add karne ke liye class ko extend kiya jana chahiye, na ki existing (purane) code ko modify (change) kiya jaye.
- **Problem Scenario:** Hamari `CartDBStorage` class abhi SQL mein save kar rahi hai. Ab requirement aati hai ki MongoDB aur File mein bhi save karna hai. Agar hum isi class mein `saveToMongo()` aur `saveToFile()` methods add kar dein, toh humne chalte hue code ko chhed diya, jo ki OCP ka violation hai.
- **Solution (Abstraction & Polymorphism):** - Ek abstract class / interface banayein: `DBPersistence` jisme ek virtual method `save()` ho.
  - Alag-alag concrete classes banayein jo is interface ko implement karein: `SQLPersistence`, `MongoPersistence`, `FilePersistence`.
  - Ab kal ko agar Cassandra DB ka support add karna ho, toh existing classes ko change nahi karna padega, bas ek nayi class banani hogi. Code open for extension hai, but closed for modification.


```java

// OCP: Open for extension, closed for modification

interface DBPersistence {
void save(ShoppingCart cart);
}

class SQLPersistence implements DBPersistence {
@Override
public void save(ShoppingCart cart) { 
    System.out.println("Saving to SQL Database"); 
}
}

class MongoPersistence implements DBPersistence {
@Override
public void save(ShoppingCart cart) { 
    System.out.println("Saving to MongoDB"); 
}
}

```

### 5 Interview Questions & Answers:
**Q1. Open-Closed Principle (OCP) ka actual meaning kya hai?**
*Answer:* Iska matlab hai ki hume software design aisa banana chahiye ki naye functionalities add karte waqt (Open for extension) purane tested aur working code ko modify na karna pade (Closed for modification).

**Q2. "Closed for modification" rule ka benefit kya hai?**
*Answer:* Existing code modify nahi karne se hume nayi bugs introduce hone ka risk nahi hota. Purana code properly tested hota hai, uski stability maintain rehti hai.

**Q3. OCP ko achieve karne ke liye kis OOP concept ka sabse zyada use hota hai?**
*Answer:* OCP ko achieve karne ke liye hum Abstraction (Interfaces / Abstract classes) aur Polymorphism (Method overriding) ka use karte hain.

**Q4. Agar OCP follow na karein aur if-else conditions se naye features handle karein toh kya hoga?**
*Answer:* Code bohot lamba, complex aur tightly coupled ho jayega. Har naye feature ke liye if-else chain mein changes karne padenge, jisse code ko maintain karna ek nightmare ban jayega.

**Q5. OCP wale database example mein Cassandra DB add karne ka process kya hoga?**
*Answer:* OCP follow karne par, hum bas ek nayi class `CassandraPersistence` banayenge jo `DBPersistence` interface ko implement karegi aur apna `save()` logic likhegi. Existing classes ya Client ko bilkul bhi modify nahi karna padega.

---

## 4. Liskov Substitution Principle (LSP)

### Detailed Notes (Hinglish):
- **Definition:** "Subclasses should be substitutable for their base classes." Iska matlab jahan bhi Parent class ka object use ho raha hai, wahan Child class ka object replace karne par program bina kisi error ke chalna chahiye.
- **Key Idea:** Subclass ko hamesha Parent class ke features ko **expand** karna chahiye, unhe **narrow down** (kam) nahi karna chahiye.
- **Problem Scenario:** - `Account` ek base class hai jisme `deposit()` aur `withdraw()` functions hain.
- `SavingsAccount` aur `CurrentAccount` dono ise properly implement karte hain.
- Ab ek `FixedDepositAccount` aata hai, jo `Account` ko inherit karta hai. Par FD mein `withdraw` allowed nahi hota. 
- Toh developer ne `FixedDepositAccount` ke `withdraw()` method mein Exception throw karwa di.
- Ab client jisko lagta hai ki saare accounts mein deposit/withdraw chalega, wo FD par withdraw call karke crash ho jayega. LSP violate ho gaya!
- **Bad Fix:** Client class mein `if-else` laga kar check karna ki "kya ye FixedDeposit hai? Toh withdraw mat karna". Yeh OCP ko violate kar deta hai aur client ko accounts se tightly couple kar deta hai.
- **Solution (Hierarchy Fix):**
- Ek abstract class banayein `DepositOnlyAccount` (jisme sirf deposit ho).
- Dusri abstract class banayein `WithdrawableAccount` (jo DepositOnlyAccount ko inherit kare aur withdraw add kare).
- `FixedDepositAccount` ko `DepositOnlyAccount` se inherit karwayein.
- `Savings` aur `Current` account ko `WithdrawableAccount` se inherit karwayein.
- Ab client perfectly do lists maintain kar sakta hai bina runtime exceptions/crashes ke.

```java

// LSP: Properly segregating behaviors so subclasses don't break expectations

interface DepositOnlyAccount {
    void deposit(double amount);
}

interface WithdrawableAccount extends DepositOnlyAccount {
    void withdraw(double amount);
}

class SavingsAccount implements WithdrawableAccount {
    private double balance;
    
    @Override
    public void deposit(double amount) { this.balance += amount; }
    
    @Override
    public void withdraw(double amount) { this.balance -= amount; }
}

class FixedDepositAccount implements DepositOnlyAccount {
    private double balance;

    @Override
    public void deposit(double amount) { this.balance += amount; }
    // Withdraw implement karne ki zaroorat hi nahi, so exception ka risk khatam!
}

```

### 5 Interview Questions & Answers:
**Q1. Liskov Substitution Principle (LSP) kya state karta hai?**
*Answer:* LSP state karta hai ki ek Child class (subclass) hamesha aisi honi chahiye ki agar use Parent (base) class ki jagah program mein use kiya jaye, toh application ka behavior change ya break nahi hona chahiye.

**Q2. Fixed Deposit example mein LSP kaise violate hua?**
*Answer:* `Account` class mein `withdraw()` method tha. `FixedDepositAccount` ne `Account` ko inherit toh kar liya par `withdraw()` function mein Exception throw kar di kyunki wo actually support nahi karta. Jab parent ka function child mein fail ho raha hai, tab wahan substitution fail hua aur LSP violate hua.

**Q3. Subclass mein `UnsupportedOperationException` throw karna kya indicate karta hai?**
*Answer:* Yeh strong indicator hai ki Liskov Substitution Principle (LSP) violate ho raha hai, aur child class ne aisi parent class ko inherit kiya hai jiske saare behaviors child par suit nahi karte.

**Q4. LSP violation ko solve karne ka sahi tarika kya hota hai?**
*Answer:* Sahi tarika yeh hai ki Object Hierarchy aur Abstractions ko refactor kiya jaye. Jaise common behaviors (deposit) ko ek base interface mein daal diya gaya aur specialized behaviors (withdraw) ko ek derived interface mein. 

**Q5. Agar Client class mein `instanceof` (type checking) use karke objects handle karein, toh kaunse principles break hote hain?**
*Answer:* Type checking se OCP (Open-Closed Principle) break hota hai (kyunki naye type ke liye code modify karna padega) aur yeh LSP violation ko patch karne ka galat tarika (code smell) hai kyunki polymophism theek se use nahi ho raha.

---
<br>
<br>

---

# SOLID Design Principles (Part 2) - Advanced Notes & Scenarios

Yeh notes Coder Army ke "SOLID Design Principles | part 2" video par based hain. Isme LSP ke advanced guidelines, ISP, aur DIP ko depth mein cover kiya gaya hai. 

---

## 1. Liskov Substitution Principle (LSP) - Advanced Guidelines

### Detailed Notes:
Sirf inheritance follow karna LSP ko guarantee nahi karta. Child class ko parent class ki tarah behave karna chahiye. Iske liye 3 main guidelines hain:

**1. Signature Rule:**
*   **Method Argument Rule:** Child class overridden method mein same argument type ya uska broader type (parent class of the argument) accept karni chahiye. C++ / Java strict signature match force karte hain [00:04:32].
*   **Return Type Rule (Covariance):** Child class overridden method se ya toh same type return kare ya uska narrower type (subclass) return kare. Lekin broader type return nahi kar sakti [00:12:12].
*   **Exception Rule:** Child class sirf wahi exceptions throw kar sakti hai jo parent throw karta hai, ya uski sub-exceptions (narrower). Broader exceptions throw karna mana hai [00:17:42].

**2. Property Rule:**
*   **Class Invariant:** Wo rules jo ek class ke liye hamesha true hote hain (e.g., account balance >= 0). Child class ko in invariants ko ya toh same rakhna hota hai ya aur strict karna hota hai, par weak nahi kar sakti [00:29:18].
*   **History Constraint:** Ek baar parent class ne jo property/state fix kar di (e.g., `withdrawal_allowed = true`), child class use dynamically change ya revoke nahi kar sakti. Immutable properties immutable hi rehni chahiye [00:34:09].

**3. Method Rule:**
*   **Pre-conditions:** Method execute hone se pehle ki conditions. Child class pre-conditions ko weak (loose) kar sakti hai, par strong (strict) nahi kar sakti [00:40:02].
*   **Post-conditions:** Method execute hone ke baad ki conditions. Child class post-conditions ko strong kar sakti hai (extra positive results de sakti hai), par weak nahi kar sakti [00:47:34].

### 5 Advanced Interview Questions (Real-World & Implementation):

**Q1. Suppose aap ek 5-tier Role-Based Access Control (RBAC) system design kar rahe ho. `BaseUser` ek exception `AccessDeniedException` throw karta hai `performAction()` mein. Agar `AdminUser` use override karke `RuntimeException` throw kare, toh konsa rule break hoga?**
*Answer:* LSP ka **Exception Rule** break hoga. `RuntimeException` ek broader exception hai. Client code jo sirf `AccessDeniedException` catch karne ke liye likha gaya hai, wo `RuntimeException` aate hi crash ho jayega. Child class (AdminUser) ko ya toh same ya narrower exception throw karni chahiye.

**Q2. Graph algorithms implement karte waqt Covariant Return Types ka use karke ek LSP-compliant Java snippet likho.**
*Answer:* Covariant return types allow subclass to return a more specific type.
```java
class GraphNode {}
class DirectedGraphNode extends GraphNode {}

abstract class GraphPathFinder {
    abstract GraphNode findPath(); // Returns base type
}

class DirectedPathFinder extends GraphPathFinder {
    @Override
    DirectedGraphNode findPath() { // Returns subclass type (Narrower) -> Allowed!
        return new DirectedGraphNode();
    }
}
```

**Q3. ATS (Applicant Tracking System) mein resume process karte waqt humara class invariant hai "resumeSize <= 5MB". Naya AI-parser is constraint ko 10MB kar deta hai. Kya ye LSP violation hai?**
*Answer:* Haan, ye **Class Invariant Rule** ka violation hai. Invariants ko child class mein ya toh intact rakhna chahiye ya strictly aur narrow (e.g., 2MB) karna chahiye. Agar base class ki guarantee thi ki >5MB fail hoga, aur child ne 10MB allow kar diya, toh base class ki guarantee toot gayi.

**Q4. (Implementation) Pre-conditions and Post-conditions in Java. Ek AI Resume scorer ka function likho jo Pre-condition ko weak aur post-condition ko strong karta ho.**
```java
import java.util.Scanner;

class ResumeScorer {
    // Pre: wordCount > 100
    // Post: Returns score between 0 and 100
    public int calculateScore(int wordCount) {
        if (wordCount <= 100) throw new IllegalArgumentException("Too short");
        return 50; 
    }
}

class AIResumeScorer extends ResumeScorer {
    @Override
    public int calculateScore(int wordCount) {
        // Pre-condition weakened: Now accepts wordCount > 50
        if (wordCount <= 50) throw new IllegalArgumentException("Too short for AI");
        
        int score = 85;
        // Post-condition strengthened: Score > 80 guarenteed for valid AI parse
        return score; 
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter word count:");
        int count = sc.nextInt();
        System.out.println("Score: " + new AIResumeScorer().calculateScore(count));
        sc.close();
    }
}
```

**Q5. History constraint kya hai? Ek immutability ka example do jo history constraint break karta ho.**
*Answer:* History constraint kehta hai ki state mutable se immutable ya vice versa dynamically switch nahi honi chahiye subclasses mein. Agar parent class ne fields ko `final` (immutable) rakha hai, but subclass internal state ko setters ke through change karne ka hack introduce kar de, toh wo parent ki historical guarantee ko break kar deta hai.

---

## 2. Interface Segregation Principle (ISP)

### Detailed Notes:
*   "Clients should not be forced to depend upon interfaces that they do not use" [00:56:51].
*   Ek bada (fat) general-purpose interface banane se better hai chhote, specific interfaces banana [00:53:18].
*   Agar ek interface mein bahut saare unrelated methods hain, toh implement karne wali classes ko dummy/empty methods banane padte hain ya `UnsupportedOperationException` throw karni padti hai, jo LSP ko bhi violate kar sakta hai [00:55:54].
*   *Solution:* 2D aur 3D shapes ke interfaces alag kar do taaki Square ko Volume ka function implement na karna pade [00:57:12].

### 5 Advanced Interview Questions (Real-World & Implementation):

**Q1. 5-tier RBAC system mein `SystemAdmin`, `ContentManager`, aur `Viewer` roles hain. Ek single interface `IUserActions` (create, edit, delete, view) use karne mein kya problem hai? Use ISP se kaise theek karenge?**
*Answer:* Single `IUserActions` interface force karega `Viewer` class ko `create()`, `edit()`, aur `delete()` implement karne ke liye, jo wo support nahi karta (throw errors). 
*Fix:* Use ISP by creating segregated interfaces: `IViewable`, `ICreatable`, `IEditable`.
```java
interface IViewable { void view(); }
interface ICreatable { void create(); }

class ViewerRole implements IViewable {
    public void view() { System.out.println("Viewing..."); }
}

class ContentManagerRole implements IViewable, ICreatable {
    public void view() { System.out.println("Viewing..."); }
    public void create() { System.out.println("Creating..."); }
}
```

**Q2. Competitive programming platforms (like Codeforces/LeetCode) ke API client mein ISP kaise apply karenge?**
*Answer:* Ek giant `PlatformAPI` interface banane ke bajaye, use `ISubmissionAPI`, `IProblemAPI`, `IUserStatsAPI` mein break karenge. Aise ek analytics dashboard module ko sirf `IUserStatsAPI` ko implement karna padega, baaki sab overhead avoid hoga.

**Q3. ISP aur Single Responsibility Principle (SRP) mein fundamental difference kya hai?**
*Answer:* SRP classes ke internal logic aur responsibility se deal karta hai ("one reason to change"). ISP interface ke design aur client ke point of view se deal karta hai ("don't force clients to see methods they don't use"). SRP class focus karta hai, ISP contract focus karta hai.

**Q4. MERN stack backend (Node.js/Express) likhte waqt Controller layer mein ISP kaise reflect hota hai?**
*Answer:* Ek massive `UserController` interface banane ke bajaye (jisme login, updateProfile, deleteUser, assignRole sab ho), hum segregation karte hain jaise `AuthInterface` aur `UserProfileInterface`. Aise routes decouple hote hain.

**Q5. (Implementation) Dynamic Programming problems (e.g., Segment Trees) build karte waqt lazy propagation aur basic point updates dono hote hain. ISP apply karke interfaces likhiye.**
```java
interface IPointUpdatable {
    void pointUpdate(int index, int val);
}
interface ILazyUpdatable {
    void rangeUpdate(int l, int r, int val);
}

// Basic Segment Tree only implements PointUpdatable
class BasicSegmentTree implements IPointUpdatable {
    public void pointUpdate(int index, int val) { /* logic */ }
}

// Advanced Segment Tree implements both
class LazySegmentTree implements IPointUpdatable, ILazyUpdatable {
    public void pointUpdate(int index, int val) { /* logic */ }
    public void rangeUpdate(int l, int r, int val) { /* logic */ }
}
```

---

## 3. Dependency Inversion Principle (DIP)

### Detailed Notes:
*   "High-level modules should not depend on low-level modules. Both should depend on abstractions." [01:00:08]
*   High-level modules (business logic) ko databases, API calls, ya specific framework implementations (low-level modules) par directly dependent nahi hona chahiye [01:01:22].
*   *Solution:* Ek abstraction (Interface/Abstract class) layer beech mein daalna chahiye [01:05:41].
*   DIP ko hum **Dependency Injection (DI)** ke through achieve karte hain, jisme required objects (dependencies) constructor ya setter ke through pass kiye jaate hain [01:10:22].
*   Golden Rule: "If Open-Closed Principle is the target, then Dependency Inversion Principle is the solution." [01:11:30]

### 5 Advanced Interview Questions (Real-World & Implementation):

**Q1. Project InternEase (AI-driven EdTech platform) mein Gemini AI APIs aur Tesseract.js (OCR) use hote hain resume parse karne ke liye. Core scoring logic directly Tesseract wrapper se baat kar raha hai. DIP apply karke iska Java code likhiye.**
*Answer:* Core scoring logic ko OCR implementaion se decouple karna hoga using an interface `DocumentParser`.
```java
import java.util.Scanner;

interface DocumentParser {
    String extractText(String filePath);
}

class TesseractOCR implements DocumentParser {
    public String extractText(String filePath) { return "Text from Tesseract"; }
}

class GeminiAIParser implements DocumentParser {
    public String extractText(String filePath) { return "Text from Gemini AI"; }
}

// High Level Module
class ATSEngine {
    private DocumentParser parser; // Abstraction
    
    // Dependency Injection
    public ATSEngine(DocumentParser parser) {
        this.parser = parser;
    }
    
    public void scoreResume(String filePath) {
        String text = parser.extractText(filePath);
        System.out.println("Scoring: " + text);
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("Press 1 for Tesseract, 2 for Gemini AI:");
        int choice = sc.nextInt();
        
        DocumentParser selectedParser = (choice == 1) ? new TesseractOCR() : new GeminiAIParser();
        ATSEngine engine = new ATSEngine(selectedParser);
        engine.scoreResume("resume.pdf");
        sc.close();
    }
}
```

**Q2. DIP ke context mein "Inversion of Control (IoC)" ka kya role hota hai?**
*Answer:* Normal flow mein High-Level module khud Low-Level module ka object create karta hai (`new LowLevel()`). IoC framework (jaise Spring Boot) control "invert" kar deta hai. Ab container objects create karta hai aur High-level modules ke constructor mein automatically inject kar deta hai (Dependency Injection), validating DIP completely.

**Q3. Ek monolithic app ko Microservices mein migrate karte waqt DIP kaise madad karta hai?**
*Answer:* Agar backend strongly coupled hai (jaise local DB queries), migrate karna nightmare hoga. Agar business logic sirf `IRepository` abstraction par depend karta hai, toh monolith DB repository ko easily Microservice HTTP Client repository se swap kiya jaa sakta hai without changing core business logic.

**Q4. FleetMaster project (Fleet management system) mein real-time GPS tracking hai. UDP protocol implementation directly business layer mein embedded hai. Dangers batao aur DIP se resolve karo.**
*Answer:* Danger ye hai ki agar kal ko UDP ki jagah WebSockets ya MQTT API use karni padhi, toh saari core logic modify karni padegi (Violates OCP). 
*Fix:* Ek interface `ILocationProvider` banao. `UDPLocationTracker` aur `MQTTLocationTracker` use implement karein. Core logic me `ILocationProvider` inject karo.

**Q5. DIP aur Strategy Design Pattern mein kya connection hai?**
*Answer:* DIP architectural guideline hai, jabki Strategy pattern uska ek runtime implementation technique hai. Strategy pattern interface ke multiple implementations banata hai aur high-level module ko interface de deta hai, jisse algorithms dynamically runtime pe switch ho sakte hain—exactly what DIP preaches.