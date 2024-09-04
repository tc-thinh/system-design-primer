# Step-by-step

1. Requirements clarifications: Always ask questions to find the exact scope of the problem you are solving.
2. Back-of-the-envelope estimation: It’s always a good idea to estimate the scale of the system you are going to design. This will also help later, when you will be focusing on scaling, partitioning, load balancing, caching, etc.
3. System interface definition: Define what APIs are expected from the system. This will not only establish the exact contract expected from the system but also ensure that you have not gotten any requirements wrong.
4. Define data model: Defining the system data model early on will clarify how data will flow among different components of the system and later will also guide towards the data partitioning and management.
5. High-level design: Draw a block diagram with 5–6 boxes representing the core components of your system. You should identify enough components that are needed to solve the actual problem from end to end.
6. Detailed design: Dig deeper into 2–3 components; interviewer’s feedback should always guide you towards which parts of the system she wants you to explain further. You should be able to provide different options, their pros and cons, and why are you choosing them?
7. Identifying and resolving bottlenecks: Try to discuss as many bottlenecks (and different approaches to mitigate them) as possible.