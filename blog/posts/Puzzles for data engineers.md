# Puzzles for data engineers, part 1

I have worked professionally as a data engineer for the past three years. Before that, I studied business intelligence at university. One of the subjects in that program was data management, and it turned out to be one of those courses I only fully appreciated once I started working.

At university, data modeling felt abstract. We studied ER diagrams, normal forms, cardinality, and keys such as primary and foreign keys. At the time, those ideas mostly lived on whiteboards and exam papers. In practice, they became much more concrete.

If you design an application for bike rentals, food delivery, or a sports league, you are also designing a model of the world. Bikes, users, payments, deliveries, teams, and matches all become entities. Their connections become relationships. The application stores those entities and relationships in a way that lets the business operate.

The relational data model is one of the most common ways to do this. Data is separated into tables so it can be stored efficiently and updated consistently. Instead of repeating everything in one large table, we split the structure into tables such as customers, products, rentals, or sales.

![Logical model of a bank application](<Logical model bank application.jpeg>)

For a data engineer, understanding that source model matters. We usually work with systems built by application teams, and our job is not just to move data around. We need to understand what the data represents, how the tables relate, and which parts of the operational model matter for analytical use cases.

That is where the work starts to become interesting. The language is familiar, but the constraints are different.

## Puzzle 1: Full or incremental ingestion?

One of the first recurring decisions in data engineering is how to ingest data from a source system.

Sometimes the only realistic option is a full load. We extract every row every time because the source does not provide timestamps, change tracking, or reliable keys for detecting updates. In other systems, incremental ingestion is possible, and often necessary, because a full extraction would be too slow, too expensive, or too disruptive to the transactional system.

This is a technical choice, but it is also a modeling choice. To ingest data incrementally, we need to know what counts as a new row, an updated row, or a deleted row. That depends on understanding the source model well enough to define change over time.

This is the first puzzle: data engineers constantly choose between full and incremental ingestion, and the right answer depends on both system constraints and data semantics.

## Puzzle 2: What should happen in each layer?

Once data has been ingested into the warehouse, the next puzzle appears: how should the pipeline be structured?

Many modern teams use some version of a medallion architecture with bronze, silver, and gold layers. The idea is simple, but the decisions inside each layer are not. Where should you deduplicate? When should you standardize naming? At what stage should business logic be introduced? Which transformations should be reversible, and which should be opinionated?

I like Piethein Strengholt's book *Designing Medallion Architectures* because it makes this point well: the architecture is not valuable because it gives you three nice labels. It is valuable because it helps you separate concerns.

In a typical setup, the bronze layer keeps raw data with minimal transformation. The silver layer refines that data through steps such as renaming columns, trimming payloads, applying light standardization, and removing duplicates. The gold layer is where data is shaped for consumption and connected into business-facing models.

Even here, the same question keeps returning: should each step run as a full refresh or incrementally? The puzzle from ingestion does not disappear once data lands in the warehouse. It follows the data through the rest of the pipeline.

## From ER diagrams to dimensional models

When data reaches the point where it should support reporting, analysis, or decision-making, we often move from the vocabulary of ER diagrams to the vocabulary of dimensional modeling.

Dimensional modeling is still about entities and relationships, but it is optimized for analytical use rather than transactional correctness. Instead of focusing on update efficiency for an application, it focuses on making questions easy to ask and answer.

That usually means organizing data into facts and dimensions. Facts capture measurable events or states such as sales, inventory, revenue, or customer satisfaction. Dimensions provide the context for analyzing those facts, such as customer, country, date, or product.

This structure produces what is often called a star schema. It is not the same as an ER diagram, but it serves a similar purpose: it gives us a model of how the data fits together. The difference is that the model is designed for analytical navigation rather than operational execution.

![Dimensional cube of data](<DImensional cube of data.png>)

The cube above is a simple sketch of that idea. We can look at one measure and slice it by different dimensions to answer business questions from multiple angles.

## Why surrogate keys show up

One concept that often surprises people the first time they work with a warehouse is the surrogate key.

Source systems usually come with their own business keys or primary keys, but those are not always ideal in an analytical model. A key may be textual, composite, unstable, or expensive to join on repeatedly. In a warehouse, we often introduce surrogate keys so dimension rows can be identified with simple internal integers.

That makes joins more efficient and gives us more control over how records evolve over time. It is one of those small design choices that looks artificial at first and then becomes obvious once you have worked with larger analytical models.

## Closing thought

This is what I find interesting about data engineering: it is full of decisions that look mechanical from a distance but turn out to be modeling decisions in disguise. Ingestion strategy, layer design, and dimensional structure are not just implementation details. They shape what questions the business can answer and how reliable those answers will be.

In part 2, I want to continue with some of the later puzzles in the pipeline, especially around change handling, historical modeling, and how analytical tables evolve over time.