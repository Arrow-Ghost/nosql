# Not Only SQL — Seminar Script (Team 9, BACSE202, Module 5)

This is our speaking guide for the website. For each screen it says **what the audience sees**, **what to click**, and **what to say**, in plain words. Don't read it word for word; say it in your own voice.

> Setting up the site? See **[DEPLOY.md](DEPLOY.md)**.

---

## Before we start (5 minutes before)

1. Open the Render health link (`https://<our-api>.onrender.com/health`) to wake the score server. Then open the website on the presenting laptop, in **Chrome, full screen (F11)**.
2. Hardware acceleration must be on (Chrome → Settings → System). Otherwise the 3D parts will be slow.
3. Scroll with the **mouse wheel or trackpad, slowly**. Every scene is tied to the scroll position, so if you scroll fast it all flies past.
4. **The thin dashes on the right edge are the chapter menu.** Hover over one to see its name, click to jump there. Use them if we run short on time.
5. Put the website link or QR code on the board so classmates can play the quiz on their phones.

## Who says what

| Speaker | Chapters on the page | Roughly |
|---|---|---|
| **Garapati Sai Aditya** | 1 Intro · 2 Every tap · 3 Definition · 4 Origins | 3 min |
| **Shrish Verma** | 5 The table · 6 The wall · 7 Scale lab · 8 Rows vs documents | 3 min |
| **Sreya Chandrasekharan** | 9 Schema · 10 Four families · 11 The cluster | 4 min |
| **Annette Jose** | 12 Consistency · 13 SQL vs NoSQL · 14 Advantages · 15 Limitations | 3 min |
| **Sahila Yazar Pottayil** | 16 In the wild · 17 Choose · 18 Polyglot · 19 Recap + quiz · 20 Thank you | 3 min + quiz |

Swap sections if someone is more comfortable with another part. The **handoff line** at the end of each block tells the next speaker it's their turn.

---

# Part A — Aditya: what NoSQL is and where it came from

### 1 · Intro: "Introduction to NoSQL"
**On screen:** a loading counter, then a big "NoSQL" title over a slowly turning galaxy of dots. The dots move away from your mouse.

**Do:** wave the mouse over the dots once so people see they react.

**Say:**
> "Good morning. We are Team 9, and our topic is *Introduction to NoSQL Databases*. Instead of slides, we built a website you scroll through. Every dot behind us is one piece of data, and as we scroll, the dots rearrange into each new idea. We'll cover five things from the syllabus: why NoSQL was needed, its characteristics, its advantages, its limitations, and where it's used."

### 2 · Every tap is a database call
**On screen:** a phone rises over the headline. A "query log" on the right lists real database commands.

**Do:** tap **like**, **Follow** and **+ Cart** on the phone. A new line appears in the log for each tap.

**Say:**
> "Every time you like a post, follow someone or add something to your cart, the app talks to a database. Look at the log: a like is a simple counter, `INCR` in Redis. Following someone is a relationship, stored in a graph database. Loading your feed is a document query in MongoDB. One app, many kinds of data. That's the problem NoSQL solves."

### 3 · Definition
**On screen:** the word "NoSQL" crosses itself out ("No SQL") and becomes "Not only SQL". Then a paragraph lights up word by word.

**Say:**
> "People think NoSQL means 'no SQL'. It actually means **not only SQL**. A NoSQL database stores data in a shape other than tables: key–value pairs, documents, wide columns or graphs. Most are built to spread data over many ordinary computers instead of one big one. Many of them even have SQL-like query languages, like Cassandra's CQL."

Point at the four fact boxes: **2009** (when the name caught on), **4** (the four main types), **CQL**, **Cluster**.

### 4 · Origins (sideways timeline)
**On screen:** the page scrolls sideways and each year draws a line and appears.

**Say** (one line per stop, keep moving):
> "1970: Edgar Codd at IBM invents the relational model, data in tables. 1974: SQL is designed at IBM. For about thirty years tables ruled. 1998: the word 'NoSQL' is first used. 2006 and 2007 are the big ones. Google publishes **Bigtable** and Amazon publishes **Dynamo**, because their data had become too big for one database server. 2008: Facebook open-sources Cassandra. 2009: MongoDB and Redis arrive, and the name NoSQL becomes popular. Today the two worlds are mixing: MongoDB has transactions, and SQL databases store JSON."

**Handoff:** "So why did companies like Google and Amazon need something new? Shrish will explain."

---

# Part B — Shrish: the need for NoSQL

### 5 · The table (relational recap)
**On screen:** two small tables, *students* and *enrolments*, and an SQL query.

**Do:** hover over a student row. Their matching enrolments light up and the query changes.

**Say:**
> "First, a quick reminder of what we already study in this course. A relational database keeps data in tables with fixed columns. A **primary key** identifies a row, a **foreign key** points to another table, and a **JOIN** puts them back together. Changes follow **ACID**: all or nothing, always valid, isolated, and permanent once saved. This design is excellent, and banks still run on it."

### 6 · The wall (Part 01: The need)
**On screen:** "Then the web happened" and three cards: Volume, Velocity, Variety.

**Say:**
> "Then the internet grew to billions of users. In 2001 an analyst named Doug Laney described the problem as three Vs. **Volume**: too much data for one machine. **Velocity**: data arrives every second, and people expect answers in milliseconds. **Variety**: profiles, photos, sensor readings, friend lists. They don't fit one fixed table design."

### 7 · Scale lab: bigger box or more boxes?
**On screen:** scrolling raises the traffic. On the left, one server grows and turns red. On the right, small servers keep getting added.

**Do:** drag the slider back and forth once.

**Say:**
> "There are two ways to handle more traffic. **Scale up**: buy a bigger server. It's simple, but the price climbs very fast, and there's always a biggest machine you can buy. See how it goes red and starts dropping requests. **Scale out**: add more cheap servers and split the data between them. The cost grows in small, steady steps. These numbers are only a model, not a benchmark, but the idea is real. NoSQL databases were designed to scale out from day one."

### 8 · Rows vs documents (the tilting screen)
**On screen:** a big screen tilts up. On the left, one order split across four tables. On the right, the same order as one document.

**Do:** click **Fetch order**, then **Asha moves city**.

**Say:**
> "Here's one customer order. In SQL it's spread over four tables, so reading it needs **three joins**. Watch the counters. In a document database the whole order sits in **one document**: one read, zero joins. That's why reads are fast. But now click 'Asha moves city'. SQL updates **one row**. The document model copied Asha's city into every order, so it has to update **three documents**. That's the trade-off: faster reads, but copied data."

**Handoff:** "So what makes a database 'NoSQL'? Sreya will walk us through the characteristics."

---

# Part C — Sreya: characteristics

### 9 · Schema on write vs schema on read (Part 02: Characteristics)
**On screen:** two panels: a SQL users table and a document collection.

**Do:** click **+ phone**, then **+ tags**.

**Say:**
> "Characteristic one: **flexible schema**. A new feature needs a phone number. In SQL we must run `ALTER TABLE` first, in every environment, and the old rows get **NULL**. In a document database we just save the new field on the one user who has it. The other documents don't change. That doesn't mean there are no rules: MongoDB, for example, can still validate documents. The rules just move closer to your app."

### 10 · Four families
**On screen:** as you scroll, the dots turn into each family, and a working demo appears on the right.

**Do and say for each one (about 30 seconds each):**

1. **Key-value.** Click **INCR likes**, then **GET session**.
   > "The simplest type: a giant dictionary. You give a key and get a value back. It's very fast, but you can only search by the key. Used for sessions, carts and counters. Example: Redis."
2. **Document.** Click the filter chips (price, wireless).
   > "Each record is a JSON document, and you can search on any field. Notice the products have different fields: the book has an author, the speaker has a battery life. One collection holds them all. Example: MongoDB."
3. **Wide-column.** Click **Ingest reading**, then **Last 3 for s-17**.
   > "Data is grouped by a partition key. Here that's the sensor ID, and each partition is kept sorted by time. Asking 'the last three readings of sensor 17' is one quick read. Great for IoT and logs. Example: Cassandra."
4. **Graph.** Click a different person.
   > "Here the relationships are the data. Click Asha: orange is who she follows, blue is friends-of-friends, which gives us 'people you may know'. Example: Neo4j."

### 11 · The cluster (3D machine)
**On screen:** a 3D model with a router at the front and three shards, each with three servers. You can drag to rotate it.

**Do:** type a key like `user:42`, click **Write**, then **Read**. Then click **Fail shard B primary** (or click a glowing server).

**Say:**
> "This is how NoSQL scales out. **Sharding**: the router takes the key, turns it into a number called a hash, and that number decides which shard stores it. Three shards each hold a third of the data. **Replication**: every shard keeps **three copies** on different servers, so one broken disk loses nothing. **Failover**: watch. I'll kill the main server, the primary, of shard B. The other copies notice, hold an election, and a new primary takes over within seconds. Writes keep working. MongoDB works like this. Cassandra goes further: it has no primary at all."

**Handoff:** "With three copies on three machines, which copy is correct? Annette will explain."

---

# Part D — Annette: consistency, comparison, advantages, limitations

### 12 · Consistency lab
**On screen:** three copies (replicas) of a product's price and two controls, **W** and **R**.

**Do:**
1. With W = 1 and R = 1, click **Write new price**, then quickly click **Read price**. Sometimes you get the old price.
2. Set W = 2 and R = 2 and do it again. Now you always get the newest acknowledged price.
3. Set W = 3, click **Cut off** on one replica, then write. The write is rejected.

**Say:**
> "A write takes time to reach every copy. **W** is how many copies must confirm a write, and **R** is how many copies we ask when reading. If R plus W is greater than the number of copies (3 here), the read always overlaps the latest write. With 1 and 1 it's faster, but you might read an old value for a moment. That's called **eventual consistency**. Last demo: I cut off one copy and demand all three confirm. The system refuses the write. It chose being correct over being available. That's the **CAP theorem**, which Team 10 covers in detail. Relational databases follow **ACID**. Many NoSQL systems follow **BASE**: Basically Available, Soft state, Eventually consistent."

### 13 · SQL vs NoSQL
**On screen:** a comparison table.

**Do:** click **Show where the line blurs**.

**Say:**
> "Side by side: tables against four models, fixed schema against flexible, mostly scale-up against scale-out, ACID against tunable consistency. Neither one is better; they solve different problems. And the line is blurring: MongoDB now supports ACID transactions, and PostgreSQL can store JSON."

### 14 · Advantages (Part 03, the cards stack up)
**Say** (one sentence per card as it slides in):
> "Advantages. **Scalability**: add machines as you grow. **Flexibility**: change the data shape without migrations. **Performance**: data you read together is stored together. **Availability**: copies keep the service up when a machine dies. **Cost**: ordinary servers or pay-as-you-go cloud. **Developer speed**: a document looks just like the object in your code."

### 15 · Limitations (Part 04, flip cards)
**Do:** hover over or tap two or three cards to flip them.

**Say:**
> "Every advantage has a price. You can get **old data for a moment**. **Joins** are weak, so you design data around your queries. There's **no single standard** language. **Copied data** can go out of sync. Many stores only guarantee **one record at a time** in a transaction. And the **tools** are younger than SQL's. The back of each card shows how real teams handle it."

**Handoff:** "So where do companies actually use it? Sahila will take us out into the real world."

---

# Part E — Sahila: applications, choosing, wrap-up, quiz

### 16 · In the wild (Part 05: Applications)
**On screen:** the dots form a globe. Use cases on the left, real companies on the right.

**Say:**
> "NoSQL runs social feeds, shopping carts, IoT sensors, live leaderboards, games, fraud detection and caches. These examples come from the companies' own papers and blogs, linked on the page. **Amazon** built Dynamo so the shopping cart never refuses an 'add to cart'. **Google** used Bigtable for more than sixty products. **Facebook** stored Messages in HBase. **Netflix** keeps viewing history in Cassandra. **Discord** moved trillions of messages from Cassandra to ScyllaDB."

### 17 · Which database fits?
**Do:** click the example buttons: **bank ledger**, then **smart meters**, then **social network**.

**Say:**
> "Here's a simple way to choose. A bank ledger needs strict transactions, so it's **relational**. Smart meters send endless time-stamped readings, so **wide-column**. A social network is about connections, so **graph**. Notice that relational is always an option. NoSQL doesn't replace SQL."

### 18 · Better together (polyglot persistence)
**Do:** hover over each box in the online store diagram.

**Say:**
> "Real apps mix databases. In one online store: the product catalogue in MongoDB, carts in Redis, **payments in PostgreSQL** because money needs ACID, recommendations in Neo4j, click history in Cassandra. Martin Fowler calls this **polyglot persistence**: use the right tool for each job."

### 19 · Recap + live quiz
**Do:** read the five recap rows quickly, then invite the class.

**Say:**
> "To sum up: the **need** was big, fast, varied data. Its **characteristics** are flexible schema, sharding, replication and relaxed consistency. The **advantages** are scale, speed, uptime and flexibility. The **limitations** are weaker consistency, fewer joins and copied data. And the **applications** are everywhere around us. Now it's your turn. Open the link on your phone, type your name and take the seven-question quiz. The leaderboard updates live, and ties go to whoever answered faster."

(Fun detail if someone asks: **the leaderboard itself is stored in MongoDB**, a NoSQL database, behind a small API. And the server works out the score from your answers, so you can't fake a 7/7.)

### 20 · Thank you
**On screen:** the dots spell **NOT ONLY SQL** behind "Thank you. Questions?"

**Say:**
> "Thank you. Our main message: NoSQL is not a replacement for SQL. It's a set of tools for scale, variety and speed. Next, Team 10 goes deeper into CAP and ACID versus BASE, and Team 11 into NoSQL data modelling. We're happy to take questions."

---

## Likely questions (short answers)

| Question | Simple answer |
|---|---|
| Is NoSQL faster than SQL? | For simple lookups at huge scale, often yes, because data is stored the way it's read. For complex joins and reports, SQL is usually better. |
| Does NoSQL have transactions? | Many have them per record. Some, like MongoDB since 4.0, also support multi-document ACID transactions. |
| When should I NOT use NoSQL? | When data is very structured, you need many joins or reports, or money must stay exactly consistent (banking, billing). |
| What is sharding vs replication? | Sharding **splits** the data across machines to grow. Replication **copies** the data to survive failures. Real clusters do both. |
| What is eventual consistency? | Copies may differ for a moment after a write, but if no new writes come in, they all end up the same. |
| What does R + W > N mean? | If the copies you write to and the copies you read from overlap, you always see the newest acknowledged value. |
| Is MongoDB the same as NoSQL? | No. MongoDB is one document database. NoSQL is the whole family: key-value, document, wide-column and graph. |
| Can you scale SQL horizontally? | Yes, by sharding or with distributed SQL databases like Google Spanner or CockroachDB, but joins and transactions across machines are harder. |

## If something goes wrong on stage

- **Leaderboard says "Waking the score server…":** keep talking. It usually connects within a minute, and any scores already played upload automatically.
- **The 3D cluster is slow:** skip it with the chapter dashes on the right and explain it in words.
- **Lost your place:** hover over the dashes on the right edge to see chapter names and click to jump.
