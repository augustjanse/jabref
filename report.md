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

Optional (point 1): Architectural overview.

Optional (point 2): relation to design pattern(s).

## Selected issue(s)

**Title**: [Wishes for new fetchers](https://github.com/JabRef/jabref/issues/2581)

**Description**: The issue is a collection of requests for the implementation of fetchers for different platforms. 
Two of these platforms are American Physical Society (APS) and Worldcat.org. The implemented fetchers should allow for generation of BibTex/Biblatex citations and references.

### Requirements affected by functionality being refactored

Optional (point 3): trace tests to requirements.

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
| August          | - | - | - | - | - | - | - | - | - |
| Glenn        	  | - | - | - | - | - | - | - | - | - |
| Roger 		  | - | - | - | - | - | - | - | - | - |

For setting up tools and libraries (step 4), enumerate all dependencies
you took care of and where you spent your time, if that time exceeds
30 minutes.

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
