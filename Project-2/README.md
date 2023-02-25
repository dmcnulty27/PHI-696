# Project 2

Your first project will require you to answer each of the 10 questions below.  You will be expected to open a pull request with your initial answers by the second class meeting, giving you one week to work on these problems. You and your peers will then have one week to work together to refine your respective initial answers, so they are ready for final submission. Once your pull requests have been reviewed and merged to the development branch, I will review them, then merge to the master branch. 

```Tip #1: Carefully study the Baader, et. al. selections assigned on bisimulation; it is deceptively subtle, and quite powerful. 
Tip #2: Google is still your friend. So is stackexchange...
Tip #3: Work _together_ to solve these problems, even for initial submissions and when you do, document this in github. 
Tip #4: Work together _as a team_. 
```

1. Let V be a vocabulary of ALCI consisting of a role name "P". Interpret part_of as "x is a part of y". Using this role name, define the following formulas in this language:

⊔ ⊓ ⊧ ⊭ ⊦ ⊬ ⊏ ⊐ ⊑ ⊒ C ¬ ≡ ≠ ≥ ≤ ∃ ∀

  (a)  PP that says that x is a part of y and the inverse (y is a part of x) is not true 
  (a)  I am not sure is this is doable because you cannot make an identity claim 
  (a)  PP ≡ P ⊓ ¬P- 
  
  (b) iPP that says that it is not the case the x is a part of y and the inverse (y is a part of x) is true
  (b) I am not sure is this is doable because you cannot make an identity claim
  (b) iPP ≡ ¬P ⊓ P-
  
  (c) iP that says x iP y means that y is a part of x
  (c) iP ≡ ∀part_of-.C
  (c) iP ≡ P-
   
  (d)  O that says that x overlaps y -- x is a whole including such a thing that it is a part of another thing y, so x and y has the same part
  (d)  I am not sure if you can do this becuase you cannot make an identity claim. This is a psapaital relation not sure how to manage that gap. It could be that they share a part? You would need 3 parts and that does not seem plausible. 
  (d)  O ≡ ∃P-.(∃P)
  
  (e)  D that says that x and y are disjoint --x has no part of y and y has no part of x
  (e)  I am not sure if you can do this becuase you cannot make an indentity claim 
  (e)  D ≡ ¬O 
  
2. Use your axioms from question 1 as the basis of an ALCI T-Box. Supplement this T-box with whatever other axioms you like, as well as an A-box, so that you ultimately construct a knowledge base K = (T,A). Provide a model of K. This may be graphical or symbolic or both.

TBox:{
PP ⊑ P 

P ⊑ O 

O ⊑ O¯

O¯ ⊑ O

D ⊑ ¬O}

ABox:{

(Utah, USA):P,

(Bryce Canyon, Utah):PP, 

(Bryce Canyon, USA):PP, 

(USA, Utah):iPP, 

(Utah, USA):O, 

(Oregon, Utah):D,

}


ΔI = {Bryce Canyon, Utah, Oregon, USA}

Named Individuals:

Bryce Canyon = NP

Utah = U

USA = A

Oregon = O

Role Assignments:
P (Part_of) = {(NP, U), (U,A), (O,A), (U,U), (O,O), (A,A)

PP (ProperPart_of) = {(NP,U), (NP,A), (U,A), (O,A)}

iP (inverse Part_of) = {(U,NP), (A,U), (A,O), (A,NP)}

iPP (inverse ProperPart_of) = {(U,NP), (A,NP), (A,U), (A,O)}

O (overlaps) = {(NP,U), (NP,A), (U,A), (O,A), (NP, NP), (U,U), (A,A), (O,O)}

D (disjoint) = {(O,U), (NP, O)}


![Protege2a](https://user-images.githubusercontent.com/123985147/221180906-722d91a8-0186-4906-83d5-af76193f531f.png)


As a Bonus here is my favorite picture I've taken at Bryce Canyon, it is at Sunrise (My favorite National Park in Utah). As well as my favorite picture I've taken in Oregon at Crater Lake (The only National Park in Oregon) simply becuase I miss the West. 

![Bryce Canyon Sunrise](https://user-images.githubusercontent.com/123985147/221182562-89053251-07f0-4fa1-a50f-29f9cf168bad.jpg)

![Crater Lake Wizard Island](https://user-images.githubusercontent.com/123985147/221182582-a440f7bb-c20a-4de5-b50e-8c33abafdac5.jpg)


3. Translate the following first-order logic axioms into ALCI:

⊔ ⊓ ⊧ ⊭ ⊦ ⊬ ⊏ ⊐ ⊑ ⊒ C ¬ ≡ ≠ ≥ ≤ ∃ ∀
Note that we can drop the first universal quantifiers :)


(a) ∀x∃y∀z(R(x,y) ∧ R(x,z) ∧ R(y,z)) - For all cases of x there is some y such that for all cases of z it is the case that all instances of x Rs some instance of y and all instances of x Rs all instances of z and some y Rs all instances z
 
∃R.(∀R.T)⊓∃R.T

(b) ∃x∀y∃z(R(x,y) ∧ R(x,z) ∧ R(y,z)) - There is some x such that for all y there is some z such that it is the case that some instance of x Rs all instances of y and x Rs some instance of z and all instances of y Rs some z

∃R-.(∃R.(∃R-.T))

∃R-.∃R¯(∃R).∃R(T)

(c) ∀y(R(x, y) → ∃x(R(y, x) ∧ ∀y(R(x, y) → A(y)))) - For all y if there is some x thats Rs all instances of y then there is some x such that all instances of y Rs some x and for all y if x Rs y then y As

Is this well-formed? I think not. If the implicit universal is there then why would we introduce the extistential x....

(d) (∀y)(R(x, y) → A(y)) ∧ (∃y)(R(x, y) ∧ B(y)) - For all y if x Rs y then y As and some instances of y x Rs y and y Bs

I am not sure about this but assuming the implicit universal x....

 (∀R.A) ⊓ (∃R.B)

4. Provide an interpretation I1 for ALC and an interpretation I2 for ALCN - each distinct from any interpretation covered in class so far - and construct a bisimulation that demonstrates ALCN is more expressive than ALC. Use the mermaid syntax of markdown to provide a graphical representation of your work. Feel free to use the mermaid live editor when diagramming.

![Protege5](https://user-images.githubusercontent.com/123985147/221069424-1023a268-b07b-42b1-8a29-61ba9ae02ccf.png)

D=Delaney


ΔI1 = {Delaney, Perci, Moia, Theia}

Named IndividualsI: 
DelaneyI = D
PerciI = Perci 
MoiraI = Moira
TheiaI = Theia


Role Assignments: t = {(D, Perci), (D, Moira), (B, Theia)}

ΔI2 = {Delaney, Perci, Moira}

Named IndividualsI: 
DelaneyI2 = D2 
PerciI2 = Perci2 
MoiraI2 = Moira2

Role Assignments: t2 = {(D2, Perci2), (D, Moira2)}

Bisimulation:

ρ = {(D, D2), (Perci, Perci2), (Moira, Moira2), (Theia,Moira2)}

So B is bisimilar to B2. By defining the role t as ≥2 ∃t.⊤ in I1 ≥1 ∃t2.⊤ in I2" -- You should intead say, "I1 there is an element with 3 successors but in I2 there is an element with 2 elements

5. Provide an interpretation I1 for ALC and an interpretation I2 for ALCN - each distinct from any interpretation covered in class so far - and construct a bisimulation that does not demonstrate ALCN is more expressive than ALC. Use the mermaid syntax of markdown to provide a graphical representation of your work. Feel free to use the mermaid live editor when diagramming.

![Protegestuff](https://user-images.githubusercontent.com/123985147/221281070-59576dac-6df4-4b28-b250-3ec77d46630b.png)

Named IndividualsI: 
DelaneyI=D
PerciI=Perci
MoiraI=Moira 


Role Assignments t={(D, Perci), (D,Moira)}

ΔI2= {Delaney, Perci, Moira}

Named IndividualsI: 
DelaneyI2=D2
PerciI2=Perci2
MoiraI2=Moira2

Role Assignments: t2 ={(D2,Percival), (D2, Moira Lee)}

Bisimulation:

ρ = {(D, D2), (Moira, Moira2), (Perci, Perci2)}

So B is bisimilar to B2. But we cannot distinguish formula X in ALC and ALCN

6. Explain the difference - using natural language - between the description logic expressions:

⊔ ⊓ ⊧ ⊭ ⊦ ⊬ ⊏ ⊐ ⊑ ⊒ C ¬ ≡ ≠ ≥ ≤ ∃ ∀

(a) ∃r.C and ∀r.C

(a) Corresponds to all instances that relates to some instances of C

(a) Corresponds to all instances that relates to only instances of C

(b) ∃r-.C and ∀r-.C

(b) The first refers to all instances which have some instance C as a r-predecessor.

(b) The second refers to all instances which have only instances of C as r-predecessors

(c) <=nr and <=nr.C

(c) The first one refers to all instances which have no more than n r-fillers.

(c) Corresponds to restrictions that r is realted to no more than n instances of C

(d) ∃r-.C and ∃r-.{a} 

(d) The first one should mean all instances which has some instance of C as r-predecessor

(d) The second one refers to all instances which have some r-predecessor which is just a.

7. There is a delightfully helpful subreddit called "ELI5" which stands for something like "explain it like I'm 5" where users post conceptually challenging questions and other users attempt to provide explanations in simple, jargon-free, terms that presumably a 5 year-old could understand. Using this as a model, explain the finite model property. Be sure to provide a simple example and explain when the property might be important, and when it is not so important.

Answer to 7. Consider a puzzle. A puzzle has a finite number of pieces and can be solved in a finite number of moves. This is to say a finite model property describes something that is true in a system and can be proven to be true within a finite number of moves, with a finite number of pieces. Importance? The finite model property is useful in that it creates a domain (edge pieces) around a concept (the whole puzzle) so that there are not infite numbers of possible pieces to the concept or puzzle. Unimportance? If we are talking about infite possibilties it is not useful to have a strict domain as the domain is never-ending in such a case, imagine a puzzle that continues to generate a new piece everytime one is put into place. This is to say a Finite model property can be used to design a procedure used for solving a problem or performing a computation for its satisfiable concepts.

![puzzles](https://user-images.githubusercontent.com/123985147/221069880-c9c63073-958e-4b3f-b024-d4a33a0cb7b1.jpg)

8. Following up on the preceding , explain the tree model property. Be sure to provide a simple example and explain when the property might be important, and when it is not so important.

Answer to 8. It is like playing Guess Who? such that we start with knowing one descriptor of the person pictured (the root). Depending on the how you guess and question the Guess Who? board will start to show patterns into different (or branches) possibilties. If you guess males you go through one pattern if you guess females you go through another pattern and if you guess gender non-conforming you will be lead down yet another pattern. Once you guess the right person (the leaf) you have reached the end of the model. Importance? The important aspect of this model is that you can see the different possible pattern the game takes and how each guess or question gets you closer to the answer! Unimportance? If you know who to guess there is no reason to go through the garden of forking paths. You can use a tree model property to check for and adhere to consistencies is a visual anaylsis platform.

![guess-who-board-game-hand](https://user-images.githubusercontent.com/123985147/221070772-8118287d-9ed2-44b0-a4d0-d8b6f6fa4f80.png)

9. Open the Protege editor and create object properties for each of the role names that you constructed in question 1. You should have at least 6 object properties. Assert in the editor that P is a sub-property of O, that P is transitive, and that O is symmetric. Next, add individuals - a, b, c - to the file and assert that c is part of a and that c overlaps b. Running the reasoner should reveal - highlighted in yellow if you select the individual c - that c overlaps a. Using the discussion in the selections from chapter 4 of the Baader, et. al. text as a guide, explain how the tableau algorithm is generating this inference. Also, provide a screenshot of the results of your reasoner run with c highlighted.

![Protege](https://user-images.githubusercontent.com/123985147/221044462-590df2a7-230f-438d-863d-0da5b661fbeb.png)


10. Following up on your work in question 9, adjust/add/remove/etc. object properties and individuals in your Protege file so that when you run a reasoner in Protege, you return the following consequences:

  (a) a is a proper part of b and disjoint from e
  
  (b) a overlaps c
  
  (c) a is part of b, b is part of f, and a is part of f 
  
  (e) There are no parts between a and g in common
  
Provide a screenshot of your results here.

As it states post a screen shot I will only one post a screenshot :)

![PROTEGE2](https://user-images.githubusercontent.com/123985147/221046071-9b2c21be-4508-47d3-813b-93b5838a0414.png)
