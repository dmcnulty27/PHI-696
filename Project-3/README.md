# Project 3

Your third project will require you to answer each of the 10 questions below.  You will be expected to open a pull request with your initial answers by the second class meeting, giving you one week to work on these problems. You and your peers will then have one week to work together to refine your respective initial answers, so they are ready for final submission. Once your pull requests have been reviewed and merged to the development branch, I will review them, then merge to the master branch. 

```
For any question involving the use of Protege, please be sure to import Basic Formal Ontology (https://raw.githubusercontent.com/BFO-ontology/BFO/v2019-08-26/bfo_classes_only.owl) and the Relations Ontology (https://raw.githubusercontent.com/oborel/obo-relations/master/ro.owl)
```

1. In BFO and RO identify at least one object property for each of a-e that _should have the listed property, but which does not_; argue for your case, using examples. 
```
  (a)  Reflexive
 Located_in should be reflexive. I am located in my self.
  (b)  Transitive 
 Occurs_in should be transitive. If a robery occurs in a building and that building is inside of a jurisdiction, then that robery happened inside of that jurisdiction.
  But also, branking should be because the inverse relation is. 
  (c)  Symmetric
  reciprocal_of seems like it should be symmetric. A reciprocal friendship is one which goes both ways. 
  (d)  Functional has relative magnitude 
  (e)  Symmetric and Reflexive
   Correlated_with should be symmetric and reflexive. If weight gain is correlated with depression, then depression is correlated with weight gain. Weight gain is also correlated with weight gain. (this sounds dumb) 
```

2. In BFO and RO identify at least one object property for each of a-e that _should not have the listed property, but which does_; argue for your case, using examples. 
```
  (a)  Irreflexive
 has_role_in_modeling seems like it could be reflexive if we are studing it. Then you would have a computational artifact about its self. This seems soft, though. Immersed_in could be another candidate, but it hinges on how you understand "physcial" in the definition. If they mean "solid", then it is irreflexive. If they mean any physical thing, it could be reflexive, since every liquid immerses its self. 
  (b)  Transitive
  Maybe aligned_with. The US can be aligned with south Korea and South Korea could be aligned with Somalia and it could be the case that the US is not aligned with Somalia. This could be cleared up with the provision of a definition. 
  has_role_in_modeling is the only asymmetric?
  (d)  Functional 
  Phenotype_of should not be functional, since its inverse function is not functional. 
  (e)  Inverse Functional
  Has_characteristic. Smile example
```

3. Model the following natural language expressions using terms from BFO and RO; you are welcome to introduce new terms where needed:  
```
 a) Sally has an arm Tuesday but does not have an arm Wednesday.
  Sally is instance_of object
Tuesday is instance_of one-dimensional temporal region 
Wednesday is an instance of one-dimensional temporal region 
Arm is an instance of fiat object part
“Sally participates in having at least one arm on Tuesday” is an instance of occurrent 
“Sally participates in having no arms on Wednesday” is an instance of occurrent
“Sally participates in having at least one arm on Tuesday precedes Sally participates in having no arms on Wednesday”

  (b) Every liver has some cell as part at all times it exists.
  Liver has_part_at_all_times Cell
  
  (c) John was a child, then an adult, then a senior. 
  John is an instance_of object
childhood is an instance_of occurrent.
adulthood is an instance_of occurrent.
seniorhood is an instance_of occurrent.
“John participates in childhood precedes John participates in adulthood which precedes John participates in seniorhood.”

  (d) Goofus and Gallant are married at each point in a three year span. 
  Goofus is an instance_of object
Gallant is an instance_of object
Marriage is an instance_of occurent
“Three years span 1” is an instance_of one-dimensional temporal region.
If zero-dimensional temporal region t1 is part_of the one-dimensional temporal region “three years span 1”, then Goofus participates in marriage at t1 and Galland participates in marriage at t1.
```

4. Using the language of First-Order Logic, represent the following natural language expressions; you are welcome to introduce new terms where needed: 
``(a) Sally has an arm Tuesday but does not have an arm Wednesday.
  ∃(x)(Sx^(Tx^~Wx)) 
  S=Is Sally 
  T=Has an arm on Tuesday 
  W=Has an arm on Wednesday
  (b) Every liver has some cell as part at all times it exists.
  ∀(x)(Lx->∃(y)(Cy^Pyx))
  L=Is a liver 
  C=Is a cell 
  P=_is a part of_
  
  (c) John was a child, then an adult, then a senior.
∃t1∃t2∃t3 (C (j, t1) ∧ A (J, t2) ∧ S(J, t3) ∧ E (t1, t2) ∧ E (t1, t3))
j = John
E xy = being earlier than
C (x, t) = being a child at t
A (x, t) = being an adult at t
S (x, t) = being a senior at t

  (d) Goofus and Gallant have been married for three years; for each day of that span, it is true to assert they are married.
   
∀t(D(t) ∧ Y(t)→(M(g1,t) ∧ M(g2,t)))
M(x, t) = being married at t
Y(t) = belongs to 3 year span 1
g1 = Goofus
g2 = Gallant
D(t) = t is a day

```

5. Using BFO and RO, model the following scenario: the content of an rdf file is represented in two serializations - one in Turtle, one in XML - which are sent from one computer to two distinct computers on the same network.   

Content is an instance_of generic dependent continuant
File is an instance_of generic dependent continuant
File 1 Turtle implements content 1
File 2 XML implements content 1
Files 1 and 2 are output of Computer 1
Computer 1 is bearer of File 1 and File 2
Computer 1 is an instance_of material entity
Computer 1 sends output to Computers 2 and 3
File 1 is input of Computer 2
Computer 2 receives input from Computer 1
Computer 2 is an instance_of material entity
File 2 is input of Computer 3
Computer 3 receives input from Computer 1
Computer 3 is an instance_of material entity
Computer 1 2 and 3 are part of Network 1
Network 1 is an instance_of Network
Network is_a object aggregate



6. Using Protege, place these in the BFO hierarchy where you think they fit best:
```
  (a) Bach's Well-Tempered Clavier
 Individual,the performance is a process, the sheet is material entity that contains a relaizable entity plan and the song is a generically dependent continuant. 
  (b) Chair of the UB Philosophy Department
 class, role that has bearer independent continuant 
  (c) SARS-CoV-2
  Class, object unless we are talking about the illness, in which case it is a process. 
  (d) Mexico City
 instance of site or object aggregate 
  (e) The trunk of a minivan
 Class. Fiat object property or maybe site Idk. 
  (f) Occupation
  Class, needs to be both a process and a role. The job of CEO is a role and the fulfillment of the role is a process.
  (g) Ocean
Class or instance. It depends on what we are talking about. If we are counting the things in the ocean as part of what we mean by "ocean", then it is an object aggregate. If we mean the location, then it is a site. 
  (h) Lake 
 
```

7. True or False; explain your answers:
```
  (a) An instance of Material Entity can have an instance of Immaterial Entity as part.
  True. I am a material entity and I have a nostral hole. 
  (b) An instance of Immaterial Entity can have an instance of Material Entity as part.
  False. Neither boundaries nor sites can have material parts. 
  (c) An organization may have another organization as part.
  True. UB philosophy is an organization that is part of the UB CAS system. 
  (d) An organization may have no members as part. 
  Organizations are object aggragets and if there are not objects, then there is no organization. 
  (e) Any site is partially bounded by some instance of Material Entity.
  According to BFO, a site is bounded by a material entity. 
  (f) A book placed under the leg of a wobbly table has acquired a new function. 
  False. Functions are the reason for which something exist. The book was not created to be a anti-wobbling mechanism. 
  (g) A glass vase cushioned with packing tape for all time, has the disposition to break. 
  True. The glass has a molecular makeup such that it is breakable.
  (h) Spacetime is a class in BFO.
  False, it is spaciotemporal region. 
  (i) The continuant fiat boundary class of BFO is closed, meaning, there are no subclasses beyond those identified presently in BFO. 
True and false. It depends on where the new subclass is stored. If it is in a CCO ontology, then it is not part of BFO. I see no reason that there cannot be a subclass of "two-dimensional continuant fiat boundary"
```

8. Model the following scenario in BFO, introducing whatever terms are needed to do so: John runs for 3 hours, startin slowly, speeding up during the middle, then ending the run at a slower pace.  

John is an instance_of object
John's Running is an instance_of process
John participates in John's Running
John bears running speeds of slow, normal, and fast
Slow, normal, and fast running speeds are instances_of dispositions
John’s running occurs in 3-hours, which is instance_of one-dimensional temporal region.
John's running consists of three temporal parts: Beginning, Middle, and End
Beginning realizes normal running speed
Middle realizes fast running speed
End realizes slow running speed
Beginning precedes Middle
Middle Precedes End
Speed is a quality of John's Running
Slow, Normal, and Fast are instances of speed
John's Speed at Beginning is decreased_in_magnitude_relative_to John's Speed at Middle
John's speed at Middle is increased_in_magnitude_relative_to John's Speed at End
John's speed at End is decreased_in_magnitude_relative_to John's Speed at Beginning



9. The Pellet reasoner in Protege can be used in an incremental reasoning strategy. ELI5 when and why one should use Pellet for incremental reasoning.

Pellet should be used when we don't want our work to start all over again everytime we change something. We may be trying to figure out, for example, the rules for a new game we are playing. In that situation, we probably don't want to go back to the start of the instructions every time we learn a new part of the rules. Instead, we would want to take each new rule we learn about, bring it in with the rules we already know about, think about what actions and rules the new rule would affect, and then keep going. It's very annoying to have to redo all of the work we have already done each time we learn something new, so we are better off using something that lets us combine everything as we go.

We may not want to use this, however, at the very beginning of learning this new game. When we only have a few rules we know and are trying to get a feel for everything, it helps us to keep everything in sight as we learn. In that case, starting over lets us put things in their context and bring them forward as we get a baseline for everything.

10. Protege reasoners will not allow you to combine certain properties, e.g. reflexivity and transitivity. If you attempt to assert such pairs of the same object property, then run the reasoner, nothing will happen. If you combine such properties while a reasoner is running, then ask to synchronize the reasoner, an error will be thrown. Provide a table or series of tables illustrating which pairs of properties cannot be combined in Protege, either because nothing happens when the reasoenr is run or because an error is thrown when synchronizing a reasoner after making such changes. Review the github docs on [creating tables in markdown](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/organizing-information-with-tables).
--------------------------------------------------------------------------------------------------------------
|Pairwise  | Functional | Inverse Functional | Transitive | Symmetric | Asymmetric | Reflexive | Irreflexive |
|----------|------------|--------------------|------------|-----------|------------|-----------|-------------|
|Functional| N/a        | Yes                | No         | Yes       | Yes        | Yes       | Yes         |
|----------|------------|--------------------|------------|-----------|------------|-----------|-------------|
|Inverse   | Yes        | N/a                | No         | Yes       | Yes        | Yes       | Yes         |
|Functional|            |                    |            |           |            |           |             |
|----------|------------|--------------------|------------|-----------|------------|-----------|-------------|
|Transitive| No         | No                 | N/a        | Yes       | No         | Yes       | No          |
|----------|------------|--------------------|------------|-----------|------------|-----------|-------------|
|Symmetric | Yes        | Yes                | Yes        | N/a       | No         | Yes       | Yes         |
|----------|------------|--------------------|------------|-----------|------------|-----------|-------------|
|Asymmetric| Yes        | Yes                | No         | No        | N/a        | No        | Yes         |
|----------|------------|--------------------|------------|-----------|------------|-----------|-------------|
|Reflexive | Yes        | Yes                | Yes        | Yes       | No         | N/a       | No          |
|----------|------------|--------------------|------------|-----------|------------|-----------|-------------|
|Irreflexi-| Yes        | Yes                | No         | Yes       | Yes        | No        | N/a         |
|ve        |            |                    |            |           |            |           |             |
|----------|------------|--------------------|------------|-----------|------------|-----------|-------------|
