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

Using dbpedia here is a SPARQL query that CONSTRUCTS a new data set of all books that have been written by authors who have written at least one book in the “Science Fiction” genre. The new data set should include the title, author, and genre of each book, as well as the name and birth year if each author.

PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbp: <http://dbpedia.org/property/>

CONSTRUCT {

?book dbo:author ?author ;

dbp:title ?title ;

dbp:genre ?genre .

?author dbo:birthYear ?birthYear ;

dbp:name ?name .

}

WHERE {

?book dbo:genre dbr:Science_fiction ;

dbp:title ?title ;

dbo:author ?author .

?author a dbo:Writer ;

dbp:name ?name .

OPTIONAL {

?author dbo:birthYear ?birthYear .

}

FILTER EXISTS {

?book2 dbo:genre dbr:Science_fiction ;

dbo:author ?author .

FILTER(?book != ?book2)

}

}





Kata level 5? – 16 points 

Using dbpedia write a SPARQL query that CONSTRUCTS a new graph of all horror movies that have been released after January 1st, 2015 along with their titles, directors, 
and ratings. The WHERE clause is used to select the horror movies that meet the criteria, and the FILTER clause is used to filter the results by release date.

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
This is a sparql query using dbpedia that constructs a graph for Stephen King book sales that are the horror genre since 1984 

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


A SPARQL query to generate a graph of all platninum selling alumbs of the punk genre from 1990-1998
Kata level 6? -- 24 points

PREFIX dbo: <http://dbpedia.org/ontology/>

PREFIX dbr: <http://dbpedia.org/resource/>

SELECT DISTINCT ?album ?artist ?releaseDate ?abstract

WHERE {

?album rdf:type dbo:Album ;

dbo:artist ?artist ;

dbo:genre dbr:Punk_rock ;

dbo:abstract ?abstract ;

dbo:releaseDate ?releaseDate .

FILTER(YEAR(?releaseDate) >= 1990 && YEAR(?releaseDate) <= 1998)

FILTER(REGEX(?abstract, "platinum", "i"))

}


A multi-step spaqrl query using in order to create a graph of all new york time's best selling authors of the true crime genre from 2000-2005
Kata level 5? -- 28 points

PREFIX nyt: <http://data.nytimes.com/elements/>


SELECT DISTINCT ?book ?author ?date

WHERE {

?book nyt:bestseller_list ?list ;

nyt:bestseller_date ?date ;

nyt:book_title ?title ;

nyt:book_author ?author .

FILTER(REGEX(?list, "Crime and Punishment", "i"))

FILTER(YEAR(?date) >= 2000 && YEAR(?date) <= 2005)

}

PREFIX dbo: <http://dbpedia.org/ontology/>

PREFIX dbr: <http://dbpedia.org/resource/>


SELECT DISTINCT ?author ?abstract ?wikiPageID ?wikiPageRevisionID

WHERE {

?book dbo:author ?author .

FILTER(REGEX(?book, "nytimes.com/books", "i"))

?author rdf:type dbo:Person ;

dbo:abstract ?abstract ;

dbo:wikiPageID ?wikiPageID ;

dbo:wikiPageRevisionID ?wikiPageRevisionID .

}

PREFIX dbo: <http://dbpedia.org/ontology/>

PREFIX dbr: <http://dbpedia.org/resource/>


CONSTRUCT {

?author rdf:type dbo:Person ;

dbo:genre dbr:True_crime ;

dbo:abstract ?abstract ;

dbo:wikiPageID ?wikiPageID ;

dbo:wikiPageRevisionID ?wikiPageRevisionID .

}

WHERE {

?book dbo:author ?author ;

nyt:bestseller_date ?date ;

dbo:genre dbr:True_crime .

FILTER(REGEX(?book, "nytimes.com/books", "i"))

FILTER(YEAR(?date) >= 2000 && YEAR(?date) <= 2005)

?author rdf:type dbo:Person ;

dbo:abstract ?abstract ;

dbo:wikiPageID ?wikiPageID ;

dbo:wikiPageRevisionID ?wikiPageRevisionID .

}


Here's a sparql query to list serial killers convicted from 1990-2000 using dbpedia
Kata level 2 -- 29 points

PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

PREFIX dbo: <http://dbpedia.org/ontology/>


SELECT ?killer ?convictionDate

WHERE {

?killer rdf:type dbo:SerialKiller .

?killer dbo:convictionDate ?convictionDate .

FILTER (xsd:integer(substr(str(?convictionDate), 1, 4))) >= 1990

FILTER (xsd:integer(substr(str(?convictionDate), 1, 4))) <= 2000

}

ORDER BY ?convictionDate


Here is my attepmt at Kata level 3 -- 49 points
using dbpedia here is a sparql query using the CONSTRUCT query form at least twice in order to create a new graph(s), alongside other query forms, operators, and functions about psychological thriller films released from 2000-2004



PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

PREFIX dbo: <http://dbpedia.org/ontology/>

PREFIX dbr: <http://dbpedia.org/resource/>

PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>





CONSTRUCT {

?film rdf:type dbo:PsychologicalThriller .

?film dbo:director ?director .

}

WHERE {

?film rdf:type dbo:Film .

?film rdf:type dbo:PsychologicalThriller .

?film dbo:director ?director .

?film dbo:releaseDate ?date .

FILTER (xsd:integer(substr(str(?date), 1, 4))) >= 2000

FILTER (xsd:integer(substr(str(?date), 1, 4))) <= 2004

}





INSERT {

GRAPH <http://example.com/psych-thriller-2000-2004> {

?s ?p ?o .


}

}

WHERE {

GRAPH <http://dbpedia.org> {

?s ?p ?o .

}

FILTER (?s IN (SELECT ?film WHERE {


?film rdf:type dbo:PsychologicalThriller .

}))

}


SELECT DISTINCT ?writer

WHERE {

GRAPH <http://example.com/psych-thriller-2000-2004> {

?film dbo:writer ?writer .

}

}


CONSTRUCT {

?writer rdf:type dbo:Writer .

}

WHERE {

GRAPH <http://example.com/psych-thriller-2000-2004> {

?film dbo:writer ?writer .

}

?writer rdf:type dbo:Writer .

}



SELECT DISTINCT ?director ?award
WHERE {
  GRAPH <http://example.com/psych-thriller-2000-2004> {
    ?film dbo:director ?director .
    ?director dbo:award ?award .
  }
}


CONSTRUCT {
  ?director dbo:award ?award .
}
WHERE {
  GRAPH <http://example.com/psych-thriller-2000-2004> {
    ?film dbo:director ?director .
    ?director dbo:award ?award .
  }
}


Here is a SPARQL query using the CONSTRUCT query form in order to create or transform a new data set alongside (or separate from the construct query form) a multi-layered, multi-step combination of query forms, operators, or functions about platinum selling R&B albums from 2008-2018
Kata level 2? -- 74 points

PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

PREFIX dbo: <http://dbpedia.org/ontology/>

PREFIX dbr: <http://dbpedia.org/resource/>

PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>


CONSTRUCT {

?album rdf:type dbo:Album .

?album dbo:artist ?artist .

?album dbo:producer ?producer .

}

WHERE {

?album rdf:type dbo:Album .

?album dbo:artist ?artist .

?album dbo:genre dbr:R%26B .

?album dbo:producer ?producer .

?album dbo:certification ?certification .

?certification dbo:certificationFor ?album .


?certification dbo:issued "US" .

?certification dbo:certificationLevel "Platinum" .

?album dbo:releaseDate ?date .

FILTER (xsd:integer(substr(str(?date), 1, 4))) >= 2008

FILTER (xsd:integer(substr(str(?date), 1, 4))) <= 2018

}





CREATE GRAPH <http://example.com/rb-platinum-albums-2008-2018>

INSERT {

GRAPH <http://example.com/rb-platinum-albums-2008-2018> {

?s ?p ?o .

}

}

WHERE {

GRAPH <http://dbpedia.org> {

?s ?p ?o .

}

FILTER (?s IN (SELECT ?album WHERE {

?album rdf:type dbo:Album .

?album dbo:genre dbr:R%26B .

?album dbo:certification ?certification .

?certification dbo:certificationFor ?album .

?certification dbo:issued "US" .

?certification dbo:certificationLevel "Platinum" .

?album dbo:releaseDate ?date .

FILTER (xsd:integer(substr(str(?date), 1, 4))) >= 2008

FILTER (xsd:integer(substr(str(?date), 1, 4))) <= 2018

})))
}

SELECT ?album ?sales

WHERE {

GRAPH <http://example.com/rb-platinum-albums-2008-2018> {

?album dbo:releaseDate ?date .

?album dbo:sales ?sales .

}

}


CREATE GRAPH <http://example.com/rb-album-sales-2008-2018>

INSERT {

GRAPH <http://example.com/rb-album-sales-2008-2018> {

?s ?p ?o .

}

}

WHERE {

GRAPH <http://example.com/rb-platinum-albums-2008-2018> {

?album dbo:releaseDate ?date .

?album dbo:sales ?sales .

}

BIND(uri(concat("http://example.com/rb-album-sales-2008-2018/", encode_for_uri(str(?album)),"/", str


Using dbpedia generate A simple multi-step SPARQL query, using a combination of at least two query forms, operators, and fucntions about FKA twigs
Kata level 7? -- 76 points


PREFIX dbo: <http://dbpedia.org/ontology/>

PREFIX dbr: <http://dbpedia.org/resource/>

PREFIX foaf: <http://xmlns.com/foaf/0.1/>





SELECT ?name ?birthDate ?birthPlace ?abstract

WHERE {

dbr:FKA_Twigs foaf:name ?name .

dbr:FKA_Twigs dbo:birthDate ?birthDate .

dbr:FKA_Twigs dbo:birthPlace ?birthPlace .

dbr:FKA_Twigs dbo:abstract ?abstract .

FILTER (LANGMATCHES(LANG(?abstract), "en"))

}


SELECT ?genre

WHERE {

dbr:FKA_Twigs dbo:genre ?genre .

}




SELECT ?album ?releaseDate

WHERE {

?album dbo:artist dbr:FKA_Twigs .

?album dbo:releaseDate ?releaseDate .

}


ORDER BY DESC(?releaseDate)

LIMIT 10


Here is a multi-step sprql query that uses a combination of at least 4 queries to retrieve information about Miley Cyrus
Kata level 6? -- 77 points

PREFIX dbo: <http://dbpedia.org/ontology/>

PREFIX dbr: <http://dbpedia.org/resource/>

PREFIX foaf: <http://xmlns.com/foaf/0.1/>

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>



SELECT ?name ?birthDate ?birthPlace ?occupation ?abstract

WHERE {

dbr:Miley_Cyrus foaf:name ?name .

dbr:Miley_Cyrus dbo:birthDate ?birthDate .

dbr:Miley_Cyrus dbo:birthPlace ?birthPlace .

dbr:Miley_Cyrus dbo:occupation ?occupation .

dbr:Miley_Cyrus dbo:abstract ?abstract .

FILTER (LANGMATCHES(LANG(?abstract), "en"))

}



SELECT ?album ?releaseDate

WHERE {

?album dbo:artist dbr:Miley_Cyrus .

?album dbo:releaseDate ?releaseDate .

}

ORDER BY DESC(?releaseDate)


SELECT ?film ?releaseDate

WHERE {

?film dbo:starring dbr:Miley_Cyrus .

?film dbo:releaseDate ?releaseDate .

}

ORDER BY DESC(?releaseDate)



SELECT DISTINCT ?language

WHERE {

?album dbo:artist dbr:Miley_Cyrus .

?album dbo:language ?language .

}



Here is spaqrl query that uses construct query to create a graph about Edgar Wright Films released from 2000-2015
Kata level 5? -- 82 points

PREFIX dbo: <http://dbpedia.org/ontology/>

PREFIX dbr: <http://dbpedia.org/resource/>

PREFIX foaf: <http://xmlns.com/foaf/0.1/>

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

PREFIX dbp: <http://dbpedia.org/property/>


CONSTRUCT {

?film a dbo:Film ;

foaf:name ?name ;

dbp:released ?released ;

dbo:director ?director .

}

WHERE {

?film a dbo:Film ;

foaf:name ?name ;

dbp:released ?released ;

dbo:director ?director .

FILTER (?director = dbr:Edgar_Wright)

FILTER (xsd:date(?released) >= "2000-01-01"^^xsd:date && xsd:date(?released) <= "2015-12-31"^^xsd:date)

}


using dbpedia generate a sparql query using constructs query to create a graph about films featuring Sacha Baron Cohen
Kata level 5 -- 87 points

PREFIX dbo: <http://dbpedia.org/ontology/>

PREFIX dbr: <http://dbpedia.org/resource/>

PREFIX foaf: <http://xmlns.com/foaf/0.1/>

PREFIX dbp: <http://dbpedia.org/property/>


CONSTRUCT {

?film a dbo:Film ;

foaf:name ?name ;

dbo:starring dbr:Sacha_Baron_Cohen ;

dbp:released ?released .

}

WHERE {

?film a dbo:Film ;

foaf:name ?name ;

dbo:starring dbr:Sacha_Baron_Cohen ;

dbp:released ?released .

}


using dbpedia generate a sparql query using constructs query to create a graph about cartoons featuring Lauren Tom (she is one of the most prolific voice actors of our time) 
Kata level 5? -- 92 points 

PREFIX dbo: <http://dbpedia.org/ontology/>

PREFIX dbr: <http://dbpedia.org/resource/>

PREFIX foaf: <http://xmlns.com/foaf/0.1/>

PREFIX dbp: <http://dbpedia.org/property/>



CONSTRUCT {

?cartoon a dbo:Cartoon ;

foaf:name ?name ;

dbo:voiceActor dbr:Lauren_Tom ;

dbp:released ?released .

}

WHERE {

?cartoon a dbo:Cartoon ;

foaf:name ?name ;

dbo:voiceActor dbr:Lauren_Tom ;

dbp:released ?released .

}


using dbpedia here is a sparql query using constructs query to create a graph about Disney Channel movies filmed in Utah
Kata level 5? -- 97 points

PREFIX dbo: <http://dbpedia.org/ontology/>

PREFIX dbr: <http://dbpedia.org/resource/>

PREFIX dbp: <http://dbpedia.org/property/>

PREFIX dct: <http://purl.org/dc/terms/>


CONSTRUCT {

?movie a dbo:Film ;

dct:title ?title ;

dbp:country ?country ;

dbo:location dbr:Utah .

}

WHERE {

?movie a dbo:Film ;

dct:title ?title ;

dbp:country ?country ;

dbo:location ?location .

FILTER regex(str(?location), "Utah") .

FILTER regex(str(?country), "United States") .

FILTER regex(str(?movie), "Disney_Channel") .

}

using dbpedia here is a complex multi-step SPARQL query, using a combination of at least four query operators about Tim Curry 
Kata level 6? -- 100 points

PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX dbr: <http://dbpedia.org/resource/>


SELECT ?movie ?title ?year ?character

WHERE {

# Get Tim Curry's information

dbr:Tim_Curry dbo:occupation dbo:Actor ;

dbo:birthPlace ?birthPlace ;

dbo:wikiPageID ?wikiPageID .

 ?movie dbo:starring dbr:Tim_Curry ;

dbo:starring ?actor ;

dbo:workLocation ?workLocation ;

dbo:releaseDate ?releaseDate ;

dbo:runtime ?runtime ;

dbo:work ?work .

  ?work foaf:name ?title ;

dbp:released ?year .


  ?work dbo:character ?character .

}

ORDER BY DESC(?year)


