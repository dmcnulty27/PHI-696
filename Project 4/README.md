**The SPARQL Library of Buffalo**

[Codewars](https://www.codewars.com/dashboard) is a website designed to facilitate algorithmic training for various programming languages. Users supply problem statements and others provide coding solutions to those problems. For example, you might find a problem for Python such as: 

```
Define a function that returns the length of a given string. 
```

With a solution like: 

```
def length_of_string(s):
	return len(s)
```
	
Codewars is not limited to traditional programming languages like Python, but also facilitates training for languages like SQL. As you have learned, SQL and SPARQL are both query languages, but what might surprise you is that there is currently no option for training SPARQL in Codewars. This project will go some way to remedy that. 

For this project, you will be tasked with constructing SPARQL problems for the codewars site. 

```
Note #1: Completion of this task will not require you to actually have your SPARQL problems successfully posted to codewars. Adding problems to codewars takes more time than we have for this project. Additionally, you are only allowed to add propose problems to codewars if you have a certain amount of experience (specifically, you need 300 of what they call 'honor points', which is acquired by solving problems). At some point, assuming you permit it, I will post your problems to codewars (giving you credit of course). 
Note #2: The potential for this project to directly impact the ontology community is clear. SPARQL can be challenging, and there are few opportunities for drill practice like this. 
Note #3: You will not be required to learn a programming language, though you will likely need to expand your comfort with computer science jargon; if you hit a wall, ask your peers for help; if the wall persists, ask me. 
Note #4: Codewars provides a guidebook - https://docs.codewars.com/authoring/tutorials/create-first-kata/ - for creating problems; I strongly encourage you to read it, since the standard provided there is how I will be evaluating success. 
```
**Assignment Details**

Problems on Codewars are ranked in terms of difficulty. The lowest "kata" - 8 - indicates a rather easy problem, while the highest kata - 1 - indicates a very challenging problem. 

For our purposes, harder kata will be worth more points than easier kata, and you are required to submit enough kata to acquire 100 points according to the following point system: 

  |   **kata**    |  **points**   |
  | ------------- | ------------- |
  |       1       |      35       |
  |       2       |      25       |
  |       3       |      20       |
  |       4       |      10       |
  |       5       |       5       |
  |       6       |       3       |
  |       7       |       2       |
  |       8       |       0       |

You're probably thinking, "why would I submit a level 8 kata if they're not worth any points?" Great question. Because everyone had to submit at least one level 8 kata. Otherwise, you're permitted to submit kata in any distribution you choose. For example, you might submit 2 problems for kata one (70 points), one for kata 3 (20 points), one for kata 4 (10 points), and one for kata 8 (0 points but required). 

It is your responsibility and the responsibility of your peers reviewing your submission in PR to determine whether your submission is ranked appropriately. In the event that consensus is reached that your kata is ranked inappropriately, you must work with your peers to revise the submission so that it is either more or less challenging, accordingly. You are not permitted to submit new problems with different strengths after PRs are open, but must instead revise your PRs. So, think hard about how challenging your submission is. 

There is one other option for those desiring a different sort of challenge. If you provide alongside your SPARQL submission a translation of the same problem into SQL, complete with documentations, solution, etc. then you may receive half points extra at that kata level (rounded up). For example, if you submit a SPARQL problem that is kata rank 1 and also submit a SQL version of that same problem, you  will receive 35+18=53 points. 

My Best Attempts.....
Kata Level 6 – 3 point
All actors who have played the character of Batmen.
PREFIX dbo: http://dbpedie.org/ontology/
PREFIX dbr: http://dbpedia.org/research/
Select Distinct ?actor WHERE {
?film dbo:starring ?act .
?film dbo:wikiPageRedircts dbr:Batman_(film_series) . 
?actor dbo:wikiPageID ?id . 
FILTER (REGEX(STR(?id), “Batman_films_casts”, “I”))
} 

Kata Level 6 – 6 points
Who invented the telephone?
PREFIX dbo: http://dbpedia.org/ontology/
PREFIX foaf: http://xmlns.com/foaf/0.1/
Select ?name
?telephone a dbo:Device ; 
	Dbo:inventor ?inventor .
?inventor foaf:name ?name . 
Filter (regex(?name, “Bell”, “I”))
}

Kata level 8 – 0 points
Return all classes  -- (A is shorthand for rdfs; type)
SELECT DISTINCT ?class
WHERE {
	?s a ?class .
FILTER (strstarts(str(?class), http://dbpedia.org/ontology/))
}
Kata level 5 – 11 points
Write a SPARQL query that CONSTRUCTS a new graph of all books that have been written by authors who have also written books in the “Science Fiction” genre. The new graph should include the title, author, and genre of each book, as well as the name and birth year if each author.
PREFIX rdf: http://www.w3.org/1999/02/22-rdf-syntax-ns#
PREFIX dc: http://purl.org/dc/terms/
PREFIX foaf: http://xmlns.com/foaf/0.1/
PREFIX genre http://example.com/genre#

CONSTRUCT {
 ?book rdf:type dc:Book ;
dc:title >?title ;
dc:creator ?author ;
genre:ScienceFiction ?genre . 
?author rdf: type foaf:Person ;
	foaf:name ?name ;
	foaf:birthyear ?birthYear . 
}
WHERE{
?book rdf:type dc:Book ;
	dc:title ?title
	dc:creator ?author ;
	genre:Sciencefiction ?genre . 
?author rdf:type foaf:Person ;
	foaf:name ?name ; 
	foaf:birthyear ?birthYear . 
FILTER EXISTS {
?otherBook rdf:type dc:Book ;
	dc:creator ?author ; 
genre:ScienceFicton ?genre . 
Filter (?otherBook !=?book)
}
}

Kata level 5? – 16 points 
Using dbpedia write a SPARQL query that CONSTRUCTS a new graph of all horror movies that have been released after January 1st, 2015 along with their titles, directors, and ratings. The WHERE clause is used to select the horror movies that meet the criteria, and the FILTER clause is used to filter the results by release date.
CONSTRUCT { 
?movie a 
<http://schema.org/Movie> ; 
<http://schema.org/name> ?title ; 
<http://schema.org/director> ?director ; 
<http://schema.org/contentRating> ?rating .
 } 
WHERE { 
?movie a <http://schema.org/Movie> ;
<http://schema.org/name> ?title ; 
<http://schema.org/director> ?director ; 
http://schema.org/genre
 <http://schema.org/Horror> ; 
<http://schema.org/contentRating> ?rating ; 
<http://schema.org/datePublished> ?date . 
FILTER(?date > "2015-01-01"
^^<http://www.w3.org/2001/XMLSchema#date>)
 }

Kata level 6? -- 19 points
This query searches for 10 books in DBpedia that are considered cosmic horror and were published after January 1st, 1900. It returns the author, book title, book description, publisher, genre, and publication date for each book
PREFIX dbpedia-owl: <http://dbpedia.org/ontology/>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX dbp: <http://dbpedia.org/property/>

SELECT ?author ?book ?description ?publisher ?genre ?publicationDate
WHERE {
  ?book a dbo:Book ;
        dcterms:description ?description ;
        dbp:genre "Cosmic horror"@en ;
        dbo:author ?author ;
        dbo:publisher ?publisher ;
        dbo:literaryGenre ?genre ;
        dbo:publicationDate ?publicationDate .
  FILTER regex(?description, "cosmic horror", "i")
  FILTER regex(?genre, "horror", "i")
  FILTER (?publicationDate >= "1900-01-01"^^xsd:date)
}
ORDER BY DESC(?publicationDate)
LIMIT 10

Level 5? -- 21 points
Return a sparql query using dbpedia that constructs a graph for Stephen King book sales that are the horror genre since 1984 
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX dc: <http://purl.org/dc/elements/1.1/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

CONSTRUCT {
  ?book dbo:author ?author ;
        foaf:name ?name ;
        dc:date ?date ;
        dbo:sales ?sales ;
        dbo:literaryGenre ?genre .
}
WHERE {
  ?book dbo:author <http://dbpedia.org/resource/Stephen_King> ;
        foaf:name ?name ;
        dc:date ?date ;
        dbo:sales ?sales ;
        dbo:literaryGenre <http://dbpedia.org/resource/Horror_fiction> .
  FILTER (?date >= "1984-01-01"^^xsd:date)
}
