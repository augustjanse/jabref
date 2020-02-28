# Report for assignment 4

## Project

**Name**: [JabRef Bibliography Management](https://github.com/JabRef/jabref)

**Description**: JabRef is an open-source, cross-platform citation and reference management tool.

## Onboarding experience
August had no problem at all building on his machine. The build does produce a lot of frightening warnings, though.

**Did it build and run as documented?**

The application did run correctly without any problems. However there was one test case that failed for the members in our group who were using Mac OS Catalina as their operating system. This issue was resolved by ignoring to run the specific test case causing the failure. We did find some documentation regarding the same issue from other contributors to the project, so it does not seem to be unique for our situation.

## UML class diagram and its description

![alt text](https://github.com/augustjanse/jabref/blob/report/Untitled%20Diagram.png)

Optional (point 1): Architectural overview.
We compiled an overview available [here](https://github.com/augustjanse/jabref/blob/report/architecture%20documentation.md).

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


### Implemented test cases and results
We found that the current test suite is kind of volatile.
The following tests are run on a clean (`git clean -xfd`) repo on the last commit before branching:
https://github.com/augustjanse/jabref/blob/report/cleaned

They all succeed. When trying the first time on the last commit of the branch, an unrelated test failed:
https://github.com/augustjanse/jabref/blob/report/aps-cleaned

However, cleaning and running again gave no errors:
https://github.com/augustjanse/jabref/blob/report/aps-cleaned2
### Test case commits
All the implemented test cases for the functions are available in the following commits:  

APS: [`5ba23c7`](https://github.com/augustjanse/jabref/commit/5ba23c741ce1eecad7690a69de1c8c99fefd5206)  
Worldcat: [`649b26e`](https://github.com/augustjanse/jabref/commit/649b26ee289ee4d197541ebe5a4aa139fbdb49cd)  
Worldcat: [`961a20e`](https://github.com/augustjanse/jabref/commit/961a20ec6f15a9d3cf91e1b2e0b09bb244ef6caa)  

To execute the test cases, use the following command: `./gradlew run`.

### Patch/fix/pull request

The the pull request are available at the following links:  
[`APS-fetcher`](https://github.com/JabRef/jabref/pull/6026)  
[`Worldcat-fetcher`](https://github.com/JabRef/jabref/pull/6035)

The pull request for APS-fetcher have already received feedback, for which actions have been taken to enable the pull request to get accepted.

Unfortunately feedback has not yet been received regarding the pull request for the Worldcat-fetcher.

We believe that it is likely for the fetchers to be merged into the master branch.


## Effort spent

|                 | Disc/Meeting | Disc/Meeting within parts of group| Reading documentation | Config/Setup | Analyzing |Writing doc | Coding| Running code | Total |
|-----------------|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| Adam  		  | 3 | 2 | 4 | 2 | 5 | 6 | 5 | 0.5 | 26.5 |
| August          | 3 | 1 | 1 | 4 | 1 | 4 | 16 | 1 | 31 |
| Glenn        	  | 3 | 2 | 3 | 2 | 1 | 1 | 16 | 1 | 30 |
| Roger 		  | 3 | 1 | 6 | 4 | 3 | 8 | 0 | 0 | 25 |

<!-- (For setting up tools and libraries (step 4), enumerate all dependencies you took care of and where you spent your time, if that time exceeds 30 minutes.) -->
### Description of time distribution, in hours:
`August`:

1: Trying to get GitHub Actions working for the repo  
1: Look into keys. Realized the way they're doing it is probably breaking terms.  
1: Start looking at APS since Worldcat is being handled. Realized we cannot use any private keys, so implement what can be done without. Tried to find an APS article that cannot be found already, but failed.  
1: Looking at other FulltextFetchers for APS.  

After that I started writing actual code. Organizational and team activities not included.

`Glenn`:

1: Installing JDK13 and running tests
1: Looking at Worldcat keys and keys in project

Other than that I spent most time understanding what to write and writing that. A lot of was spent on understanding the system, how everything was connected

`Roger`:

1:Look into the worldcat fetcher and and attempt to get the keys.  
3:Read the code written by teammates to prepare for the documentation and UML diagram drawing  
4:Learning th new knowledge that is unfamiliar to me, such as how to draw the UML diagram, SEMAT kernel and different layers and methods used in developing the fetchers.  

I use other time to read the documentation of whole project and tried to undeerstand their approach.Also, I tries to draw a graph for the architecture to make the whole structure of this project more clear and visible. 

`Adam`:

Before I could start contributing by coding I had to analyze the existing fetchers and overall code to get an understanding on how it should be implemented and this took quite the time. I found that the project in terms of coding was complex, and therefor it was difficult for me to make any progress. Since the coding was less of an issue for other group members I could distribute my time to other tasks such as documentation and analyzing. 

### The benefits, drawbacks, and limitations of our work carried out

### Limitations
The limitation we experienced was that we all have different educational background and therefor not equally prepared when it comes to working on larger open source project. However, this was converted into an advantage for this assignment.

Also One of the fetchers we implement, the Worldcat requires the authorized key to access the document.We failed to get the key unfortunately. It might not be free for users and may incur costs.

### Drawback
The APS fetcher we implement could only find PDFs that are only available elsewhere. It increases the maintenance cost without good reason. 

Also one of the fetchers we implement, the Worldcat, requires the authorized key to access the document. We failed to get the key unfortunately. It might not be free for users and may incur costs.

### Benefit
We believe that the distribution of our time was well organized for this assignment. The advantage of having members in the group with broader experience when it comes to working on larger open-source projects was utilized well. Every member had a part in making this assignment successfull. We believe that the learning experience of working in a group with different backgrounds have prepared us well for future group assignments, both as students and later as professionals.

Our work also maintains the current software system and did not change the current architecture but enrich the content and increase the fetchers to allow the system have access to more fetchers like Worldcat and APS, providing the users more options for their research. It should be easy to maintain.  

## Some problems we have encountered
**Problems with Worldcat-fetcher:**

We had trouble obtaining a key for the Worldcat Search API. Keys can only be obtained by libraries that maintain Worldcat discovery and/or OCLC Cataloging subscriptions. One of these libraries are the KTH-library, but unfortunetly when we contacted them they couldnt help us with our issue. KTH IT-support was also contacted but couldnt provide any help.

In the comment section of the issue we made a request to the admins to check if they could provide a sandbox-key for testing, their response was to obtain one by ourselves.

**Other problems**:  
One test case failed for some of the group members. However this did now effect our workflow.

## Overall experience
August found an assignment that seemed appropriate. Our issue was a composite issue of many fetcher issues. We aimed to fix both remaining.
We had no problems with the tool framework, as it was deliberately selected to use Gradle and JUnit as we were used to.

The project seemed welcoming and was well documented. We found, however, that they stored API keys in the code, which was a conundrum for us, wanting to do it the right way.
Because it was difficult to divide work on one fetcher, we decided to work separately. August did the APS fetcher. He looked at similar classes and wrote together something quickly. Thought it was almost ready. Fixed problems found by tests. Tried to get running in GUI. Didn't work as expected. Found that API doesn't work for these purposes, tried workaround. Found that workaround was case sensitive. Found API is case sensitive as well. Tried to redirect through doi.org. Tried to find redirect link with Unirest. Decided to go with other solution. Tidied up code.

After all that struggle, August sent a pull request which he thought looked pretty good. The maintainer replied with a ton of problems, that were fixed. That was an interesting experience.

Glenn has some trouble understanding the purpose of the importers and what was ment to be implemented in them versus the fetchers. He could not find any clear information about the importance of the importer, and when looking at the only other fetcher that only implements the same interface, MrDLibFetcher, its importer parsed the result (as JSON), which is now what WorldcatImporter does. However, he also needed to do make more HTTP request for each result from the main http result (to get more information about the entry, like year and publication) which he was unsure where to place, in the fethcer or the importer. The fetcher felt better because it did HTTP requests to OpenSearch alredy, but the result needed to be parsed first, because each entry in the result XML had a special ID that was needed. Therefor, a design decision was made, and the other requests were done in the importer. As no description was made of the importer, he assumes that is okay.


## What are your main take-aways from this project? What did you learn?
The biggest take-away is how hard it can be to familiarize oneself with a big project like this, and how important documentation really is. It is basically impossible to understand how everything in the project is connected in such a small amount of time, and tough to know what to look at.

However we all feel that it was a really good experience, reading other peoples code and trying to understand what they want with an issue. 

### Work in context with best software engineering practice
If we put some context to the software engineering practice of [SEMAT kernel](http://semat.org/quick-reference-guide) and the essence of that practice, we would state the following:

`Stakeholders: The people, groups, or organizations who affect or are affected by a software system.`  
This would be the owners of the JabRef repository. The software is under the MIT License which is a permissive free software license. Having that kind of license facilitates the way contribution to the project can be performed.

`Opportunity: The set of circumstances that makes it appropriate to develop or change a software system.`  
The issues posted in the github repository would be the circumstances that makes it appropriate to change/develop a software system. In this case the circumstances can be generated by the stakeholders or requested by users of the product. By having the product on a platform such as Github with the MIT license, the issues (thus the opportunities) will be available to a large crowd of potential contributers.

`Work: Activity involving mental or physical effort done in order to achieve a result.`
In our case it is the effort put into solving the issues. This has been thoroughly documented in previous section, in which each member describes their time distribution throughout the assignment.

`Team: A group of people actively engaged in the development, maintenance, delivery or support of a specific software system.` 
This would be the members in our dynamic quartet, working on the development of this assignment.

`Way-of-Working: The tailored set of practices and tools used by a team to guide and support their work.`  
We tailored the difference within our group regarding software development in such sense that every member worked on parts were their qualities were utilized to the fullest. During the development process we continued to communicate within the group to make sure that we had a common goal and way to achieve it.

### Optional (point 7): Is there something special you want to mention here?


