### GSoC 24 - ALTQ refactoring and NPF integration

September 12, 2024. posted by Emmanuel Nyarko.

Alternate Queuing has been of great need in the high Performance Computing space since the continuous records of unfair disruption in network quality due to the buffer bloat problem. the buffer bloat problem still persists and not completely gone. but mordern active queue managements have been introduced to improve the performance of networks.

altq was refactored to basically improve maintainability. duplicates were handled, some compile time errors were fixed, and also performance has been improved too.

this improves the quality of developer experience on maintaining the atq codebase.

The controlled delay (CoDel) active queue management has also been integrated into the netbsd codebase. This introduces improvements made in the area of quality of service in the netbsd operating system. CoDel was a research led collaborative work by Van Jacobness and Kathleen Nichols which was developed to manage queues under control of the minimum delay experienced by packets in the running buffer window.

As it stands now, ALTQ in netbsd is integrated in PF packet filter. I am currently working to integrate it in the NPF packet filter. and the code in netbsd is on the constant pursuit to produce clean and maintainable code.

I'll also be working to improve quality of service in netbsd through quality and collaborative research driven by randomness in results. As a research computer scientist, I will be working to propose new active queue managements for the netbsd operating system to completely defeat the long lasting buffer bloat problem.

more details to work is [here](https://github.com/Emmankoko/Open_source_reports/blob/main/GSOC/gsoc24.md)

