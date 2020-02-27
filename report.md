# Report for assignment 4

## Project

**Name**: [JabRef Bibliography Management](https://github.com/JabRef/jabref)

**Description**: JabRef is an open-source, cross-platform citation and reference management tool.

## Onboarding experience

Did it build and run as documented?
    
See the assignment for details; if everything works out of the box,
there is no need to write much here. If the first project(s) you picked
ended up being unsuitable, you can describe the "onboarding experience"
for each project, along with reason(s) why you changed to a different one.

## UML class diagram and its description

![alt text](https://github.com/augustjanse/jabref/blob/report/Untitled%20Diagram.png)

Optional (point 1): Architectural overview.

Optional (point 2): relation to design pattern(s).

## Selected issue(s)

**Title**: [Wishes for new fetchers](https://github.com/JabRef/jabref/issues/2581)

**Description**: The issue is a collection of requests for the implementation of fetchers for different platforms. 
Two of these platforms are American Physical Society (APS) and Worldcat.org. The implemented fetchers should allow for generation of BibTex/Biblatex citations and references.

### Requirements affected by functionality being refactored
Our changes are purely expanding existing functionality. Therefore, no API changes are made. Our new classes override existing interfaces. Because of that, the requirements of the public methods are the same as documented for the methods they override. Some high-level requirements on our classes are as following:

1. Finds PDF: The APS fetcher finds a PDF when selecting "Search full text documents online" on an APS entry
2. Updates entry: The Worldcat fetcher successfully updates an entry with missing info when selecting "Update with bibliographic information from the web"
3. Fails gracefully: When no info is found, fetchers report so in the appropriate way without failing.

The requirements on the environment that the GUI is properly connected to the logic that calls our classes the proper way. This is assumed to be correctly implemented already.

Optional (point 3): trace tests to requirements.
The APS fetcher was unit tested to see that it behaves as expected both when finding PDFs and when not (1, 3): https://github.com/JabRef/jabref/pull/6026/files#diff-05a59d2bfd3fd710df528c3327a23e03
It was then manually tested in the GUI to ensure that it causes no unexpected problems (3).

### Existing test cases relating to refactored code

### Test results

Overall results with link to a copy or excerpt of the logs (before/after
refactoring).

### Patch/fix

The fix can be copied or linked to (git diff).

Optional (point 4): the patch is clean.

Optional (point 5): considered for acceptance (passes all automated checks).

## Effort spent

|                 | Disc/Meeting | Disc/Meeting within parts of group| Reading documentation | Config/Setup | Analyzing |Writing doc | Coding| Running code | Total |
|-----------------|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| Adam  		  | - | - | - | - | - | - | - | - | - |
| August          | 1 | 1 | 1 | 4 | 1 | 4 | 16 | 1 | 28 |
| Glenn        	  | - | - | - | - | - | - | - | - | - |
| Roger 		  | - | - | - | - | - | - | - | - | - |

For setting up tools and libraries (step 4), enumerate all dependencies
you took care of and where you spent your time, if that time exceeds
30 minutes.

In hours:
August:
1: Trying to get GitHub Actions working for the repo
1: Look into keys. Realized the way they're doing it is probably breaking terms.
1: Start looking at APS since Worldcat is being handled. Realized we cannot use any private keys, so implement what can be done without. Tried to find an APS article that cannot be found already, but failed.
1: Looking at other FulltextFetchers for APS.

After that I started writing actual code. Organizational and team activities not included.

## the benefits, drawbacks, and limitations of our work carried out


## Some problems we have encountered
1. The problem with storing the API
2. When requesting the key from Worldcat, the authority is not instantly delivered/denied.
3. When we first run the original project using ./gradlew test, the build fails and 9 test cases failed.


Problems with Worldcat-fetcher:

We had trouble obtaining a key for the Worldcat Search API. Keys can only be obtained by libraries that maintain Worldcat discovery and/or OCLC Cataloging subscriptions. One of these libraries are the KTH-library, but unfortunetly when we contacted them they couldnt help us with our issue. KTH IT-support was also contacted but couldnt provide any help.

In the comment section of the issue we made a request to the admins to check if they could provide a sandbox-key for testing, their response was to obtain one by ourselves.

## Overall experience

What are your main take-aways from this project? What did you learn?

Optional (point 6): How would you put your work in context with best software engineering practice?

Optional (point 7): Is there something special you want to mention here?
