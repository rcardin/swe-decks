---
marp: true
theme: gaia
_class: lead
paginate: true
author: Riccardo Cardin
lang: en
backgroundImage: url('../assets/background.png')
backgroundPosition: right top
backgroundSize: 150px
footer: "Software Engineering - Riccardo Cardin"
style: |
  section::after {
    content: 'Page ' attr(data-marpit-pagination) ' of ' attr(data-marpit-pagination-total);
    color:rgba(255, 246, 223, 1);
    height: 40pt;
    line-height: 30pt;
    font-size: 14pt;
  }
---

<!-- _paginate: skip -->

<style>
  section {
    font-size: 22pt;
  }
  header,footer {
    color:rgba(255, 246, 223, 1);
    background-color: rgba(169, 0, 35, 0.7);
    height: 40pt;
    line-height: 30pt;
  }
  h1, h2, h3, h4 {
    color:rgba(169, 0, 35, 1);
  }
  blockquote {
    font-size: 0.9em;
  }
  section > *  {
    font-size: 1em;
  }
</style>

# DEPENDENCY MANAGEMENT

## SOFTWARE ENGINEERING

**Università degli Studi di Padova**
**Dipartimento di Matematica**
**Corso di Laurea in Informatica**

riccardo.cardin@unipd.it

---

## DEPENDENCY

> *The quality or state of being influenced or determined by or subject to another.*

- **Changes** in a component may influence its dependencies
  - Internal changes: implementation
  - External changes: interface or extrinsic behaviour

- **Dependency** a measure of the **probability** of **changes** among dependent components
  - The stronger the dependency the higher the probability

---

## COUPLING

- A **measure** of the degree of **dependency**
  - Tightly-coupled: higher probability of changes
  - Loosely-coupled: lower probability of changes

> *Dependency between components must be minimized, making components loosely coupled.*
> — **Gang of Four**

- Free to change a component, without introducing bugs
  - Internal / external changes
  - Architecture are dynamic and evolve during time

---

## DEPENDENCY IN OOP

- Dependencies among types

<style scoped>
table {
  font-size: 0.8em;
}
</style>

| Name | Description |
|------|-------------|
| *Dependency* | When objects of one class **work briefly with** objects of another class |
| *Association* | When objects of one class **work with** objects of another class for some prolonged amount of time |
| *Aggregation* | When one class **owns but shares a reference** to objects of another class |
| *Composition* | When one class **contains** objects of another class |
| *Inheritance* | When one class **is a** type of another class |

- Lines of code and time (scope)
  - Let's analyze one by one

---

<style scoped>
pre {
  font-size: 0.9em;
}
</style>

## DEPENDENCY (RELATION)

- **Weakest** form of dependency
  - _Limited in time_: execution of one method
  - _Limited in shared code_: interface only
```java
class A {
    public A() { /* ... */ }
    public void methodA() { /* ... */}
}
class B {
    public void methodWithAParam(A param) {  // ← Dep. interval
        a.methodA();
    }
    public A methodThatReturnsA() {          // ← Dep. interval
        return new A()
    }
}
```

---

<style scoped>
pre {
  font-size: 0.9em;
}
</style>

## ASSOCIATION

- A class contains a reference to an object
    - Spans all over an object life time: permanent
        - Impacts also object construction


    - All behaviours of a class are virtually shared

```java
class A {
    private B b;
    public A(B b) { this.b = b; }  // ← Dep. interval
    // Other methods of class A
}
class B {
    public void method1() { /* ... */ }  // ← Every method
    public void method2() { /* ... */ }  //   signature of B
    public void method3() { /* ... */ }
}
```

---

<style scoped>
pre {
  font-size: 0.8em;
}
</style>

## AGGREGATION AND COMPOSITION

- One type owns the other
  - Addition of creation and deletion responsibility
  - Composition: avoid shareability of components

```java
class A {
    private B b;
    public A() {
        // A must know how to build a B 
        this.b = new B("param1","param2");  // ← Dep. interval
    }
    // Other methods of class A
    static class B {
        // Rest of the class
        public B(String param1, String param2) { /* ... */ }
        // ↑ Also the building process is shared
    }
}
```

---

<style scoped>
pre {
  font-size: 0.9em;
}
</style>

## INHERITANCE

- **Strongest** type of dependency
  - Inheritance and reuse of the not private code
  - Any change to the parent can disrupt its children

```java
class A {
    public A() { /* ... */ }           // ← Shared code
    // Other methods of class A
}
class B extends A {
    public B() {
        super();                       // ← Dep. interval
        // ...
    }
    // Other methods of class B
}
```

---

## DEPENDENCY DEGREE

- The more the **shared code**, the stronger the dependency
  - Also, the wider the scope, ...

- Can we formalize a **measure of coupling**, δ<sub>A→B</sub>?

$$\delta_{A \to B} = \frac{\varphi_{S_{A|B}}}{\varphi_{S_{tot_B}}} \varepsilon_{A \to B} \in \{x \in \mathbb{R}^+ | 0 \le x \le 1\}$$

- *φ<sub>S<sub>A|B</sub></sub>*: SLOC shared between A and B
- *φ<sub>S<sub>tot<sub>B</sub></sub></sub>*: Total SLOC of class B
- *ε<sub>A→B</sub>*: A factor [0, 1] the measures the scope

---

## DEPENDENCY DEGREE

- Coupling is proportional to the **probability** of mutual **change** between components

$$\delta_{A \to B} \propto P(B_{mod}|A_{mod})$$

- Measure of total coupling for a component

$$\delta^A_{tot} = \frac{1}{n} \sum_{C_j \in C_1,...,C_n} \delta_{A \to C_j}$$

- *C<sub>j</sub>* is the *j*th class A depends on
- The measure is the **mean** of all coupling measures

---

## INFORMATION HIDING

- Remember the `Rectangle` class?
  - What if height and width have their own types?
    - `Height`, `Width` and `Rectangle` types would always be used together
  - They are **tightly-coupled**
  - The δ<sup>C</sup><sub>tot</sub> of a client C would be very high
    - It would use always all the three types
  - δ<sup>Rectangle</sup><sub>tot</sub> would be high too

- The given solution probably obtains the **minimization** of δ<sup>C</sup><sub>tot</sub>

---

## REFERENCES

- Dependency.
  http://rcardin.github.io/programming/oop/software-engineering/2017/04/10/dependency-dot.html

- The Secret Life of Objects: Information Hiding
  http://rcardin.github.io/design/programming/oop/fp/2018/06/13/the-secret-life-of-objects.html

---

## GITHUB REPOSITORIES

https://github.com/rcardin/swe
https://github.com/rcardin/swe-decks
https://github.com/rcardin/swe-imdb

