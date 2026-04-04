Algorithms and business processes are the same idea wearing different clothes. An algorithm is a finite sequence of well-defined steps that transforms an input into an output. A business process is a finite sequence of activities that transforms resources into value. Strip away the domain-specific language and they are structurally identical. This is not a metaphor — it is a precise observation, and it is the foundation of everything in this note.

As someone studying both computer science and business, I find myself returning to this connection constantly. Operations research — the discipline that applies mathematical methods to decision-making in organizations — has known this for decades. Linear programming, network flow, scheduling theory, and queueing models are all algorithmic tools that have been applied to business problems since the 1940s. What has changed is that the cost of computing has dropped to near zero, which means the algorithmic lens is now accessible to anyone willing to apply it.

Algorithms is like a business process synonymous with step-by-step instructions. The former often refers to computational algorithms while the latter refers to step-by-step activities inside businesses. Both can be studied and are extremely useful disciplines and areas of study each for their purpose. In fact I believe this is a skill for life because as the saying goes, how we live our days is how we live our lives — and how we live our days is essentially step-by-step activities that we are more or less aware of.

# Algorithms outside programming
One of the pleasures of studying algorithms is that the ideas transfer far beyond code. Cormen et al bring an example in their chapter on probabilistic analysis — a hiring manager interviewing candidates sent by an employment agency.

1) The employment agency sends you one candidate each day
2) You interview that person and if they are better than your current best, you hire them (and fire the previous hire)

The surrounding problem is that the hiring manager pays a fee for every applicant interviewed, and a larger fee each time they hire. There is a greedy rule embedded here: hire if and only if the new candidate is strictly better than the current one. In pseudocode:

Code example 1.1 pseudocode for hiring procedure
```
hiring_procedure():
	current = 0
	for i in 1 to n:
		interview candidate i
		if candidate i > current
			current = i
			hire candidate i
```

What makes this interesting algorithmically is the question of cost. How many times do we expect to hire? If candidates arrive in the worst possible order (sorted ascending by quality), we hire every single one — $n$ times. If they arrive in random order, the expected number of hires is $H_n = \ln n$ — the $n$-th harmonic number. This is a significant difference. An organization that interviews 100 candidates in random order expects to hire roughly $\ln(100) \approx 4.6$ times. The algorithmic analysis tells us something non-obvious about the expected behavior of the process.

This is a simple example but it illustrates a deeper point: **once you write down a business process as an algorithm, you can analyze it**. You can ask about worst-case behavior, average-case behavior, and where the cost concentrates. Most organizations never do this. They just run the process and wonder why it's expensive. 

We could also make a flowchart and since this is an actual physical activity and related to business, this starts to become a business process. We can think of business processes as the algorithms that make businesses go around and the building blocks inside the value chain of businesses. Therefore we can benefit from the same sort of thinking whether we design business behaviors or computational algorithms.

Every business can be drawn as one big workflow and once we realize this we might start looking at these workflows and applying ideas on how to improve or design them. With new technologies we might instead of thinking of roles consider how AI agents can produce the steps that ultimately is what businesses are made up of. The problem is most businesses have never looked at their processes the way a software engineer looks at slow code. They just run them. And some of those processes are quietly costing serious time and money — not because people aren't working hard, but because the process itself is inefficient by design.

## Diving deeper into algorithmic analysis of business processes
From computer science we understand terms such as the **critical path** which is the longest path from start to finish. It determines the minimum time to complete the entire process — no amount of parallelism can compress it further. This is the domain of Critical Path Method (CPM), a technique from operations research developed in the 1950s that is directly equivalent to finding the longest path in a weighted DAG. If you want to speed up a business process, you focus on the critical path. Optimizing tasks that are not on the critical path produces no improvement in total duration — a direct analogue of Amdahl's law in parallel computing.

In a directed graph, a vertex with very high **in-degree** — many edges pointing into it — is a convergence point. Everything must pass through it. In a business process, this is a **bottleneck**: a single person, team, or system that all work must flow through before it can continue. The Theory of Constraints, developed by Eliyahu Goldratt, is essentially a framework for identifying and eliminating bottlenecks in production systems. It maps directly onto graph theory: find the vertex with the highest in-degree relative to its throughput capacity, and that is your constraint. Improve throughput anywhere else and the system does not improve. Improve the constraint and the whole system improves.

Not all business processes are DAGs. Many contain **cycles** — feedback loops, approval rounds, revision processes, recurring operations. An invoice that gets rejected and returned for correction, a product that goes back to design after a failed review, a support ticket that escalates and de-escalates — these are cycles in the process graph. Cycles are not inherently bad, but they are expensive. Each time a task traverses a cycle it consumes time and resources. DFS can detect cycles in $O(V+E)$. In business terms, detecting a cycle means identifying a structural rework loop — a sign that a process has no clear exit condition, or that its quality criteria are ambiguous.

**Strongly connected components (SCCs)** — sets of vertices where every vertex can reach every other — represent subsystems that are tightly coupled and internally self-reinforcing. In an organization this might be a team or department that rarely produces external output and mostly processes work internally. Identifying SCCs in a process graph can reveal organizational silos.

When you change a step in a business process, which other steps are affected? This is an **impact analysis** question — and it is precisely what BFS solves. Starting from the changed vertex, BFS explores outward layer by layer, discovering all dependent tasks in order of their distance from the change. The BFS tree tells you the propagation structure of any change or failure. This is directly analogous to how dependency managers in software (npm, pip, cargo) compute what needs to be recompiled or retested when a package changes.

A powerful framing that comes from computer science is **complexity analysis**. We ask not just whether a process works, but how its cost scales with input size. Consider an approval process where every decision must be reviewed by every other decision-maker — this is $O(n^2)$ in the number of people involved. A hiring committee of 5 requires 10 pairwise reviews; a committee of 20 requires 190. The process becomes prohibitively expensive not because anything went wrong, but because it was designed with quadratic complexity. Many bureaucratic processes have this character — they were designed for small teams and become unworkable at scale not because of poor execution but because of poor algorithmic design.

The goal of process optimization is not just to eliminate waste in the current process — it is to redesign processes so their complexity class is appropriate for their scale. A process that must handle 10x more volume should ideally scale linearly, not quadratically.
# Operations research as applied algorithmic thinking
Operations research (OR) is the oldest formalization of this idea. Since the 1940s, OR has applied mathematical and algorithmic methods to decision-making in organizations:

- **Linear programming** — allocate resources optimally subject to constraints (simplex algorithm, $O(m \cdot n)$ in practice)
- **Network flow** — model supply chains, logistics, and resource routing as flow problems on graphs (max-flow min-cut theorem)
- **Scheduling theory** — assign jobs to machines to minimize makespan or lateness (related to topological sort and critical path)
- **Queueing theory** — model waiting lines, service systems, and throughput (relevant to any process with arrivals and service times)

What is new today is not the mathematics — it is the availability of data and computing power to apply it at scale, and the emergence of AI systems that can execute steps of a process autonomously once they are formally defined.
# Toward automated business processes
Once a business process is mapped as a graph and its algorithmic properties are understood, it becomes a specification for automation. Each vertex is a task that can be assigned to a human, a software system, or an AI agent. Each edge is a handoff that can be made explicit and monitored. The discipline of business process management (BPM) has worked toward this for decades. What AI changes is the set of tasks that can be automated — tasks that previously required human judgment (reading a document, drafting a response, classifying a request) can now be handled by language models. The bottleneck shifts from execution to design: the hard part is no longer running the process, it is mapping it correctly and defining the quality criteria at each step.

This is where the combination of computer science and business becomes genuinely powerful. A person who can both map a process as a graph, analyze its complexity, and implement or configure the agents that execute it — is working at a level most organizations have not yet reached.

The goal of the business is to deliver something which is valued by the consumer and that is going to take some work 

# Mapping business processes and workflows
One of the first steps — also acknowledged by Jan Stentoft and Anders Haug in their book *Business Process Optimization* — is to map or diagram business processes, which is to lay out the algorithm of the business. By doing this mapping we can begin to see where we might optimize and change behaviors towards more productive ones, perhaps with the use of data to measure effectiveness.

Perhaps even more potent is that once we understand that any business is at its core a sequence of activities, we are in a good position to apply algorithmic thinking. With technologies like artificial intelligence this further means we might make workflows that are augmented or fully automated. That is where we can begin to define agents, skills and tools which are capable of running business processes that we have mapped and defined.

> "I map your business workflows, identify where time and money is being wasted due to inefficient process design, and build software or AI systems that fix it — the same way a computer scientist optimizes a slow algorithm."

Mapping business processes can be done using BPMN a universal set of symbols that can describe any process and subprocess. The interesting thing about a business process diagram is that it can be considered a graph. Graphs useful for many applications in computer science and m any real-world problems now also gives us a business process representation. 

![[business process as a graph|center]]

The key insight is that a business process is not merely a linear sequence of steps. It is a **directed graph** where:
- **Vertices** represent tasks, decisions, roles, or states
- **Edges** represent dependencies, handoffs, information flows, or transitions

Once you see it this way, a rich set of algorithmic tools becomes available. When we map a business process or workflow we get a sense of what is actually happening, although many such work systems can be very complex — particularly as knowledge work becomes a bigger part of the organizational supply chain.

Many business processes are **directed acyclic graphs (DAGs)** — there are dependencies between tasks, but no circular dependencies. A product launch, an onboarding process, a software release pipeline — all of these are DAGs. Task B cannot begin until task A is complete.

Topological sort, which runs in $O(V+E)$, gives you a valid execution order for a DAG. This is exactly what project management tools like Jira, Asana, or Make/Gradle build systems compute implicitly. Understanding this means you can reason formally about whether a set of tasks is even schedulable — if the dependency graph contains a cycle, the process is deadlocked by design.


