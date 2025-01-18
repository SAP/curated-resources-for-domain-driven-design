# **Big Picture EventStorming**

## What Is Big Picture EventStorming?

**Big Picture EventStorming** is an immersive, workshop-based method for exploring and modeling an entire business domain by focusing on **domain events**—noteworthy occurrences that change the system’s state. Conceived by **Alberto Brandolini** in the early 2010s and inspired by **Domain-Driven Design (DDD)**, it aims to:

- Foster **cross-functional collaboration** between business and technical stakeholders.
- Surface **hidden dependencies**, inefficiencies, and unexplored assumptions.
- Generate **actionable insights** for strategic and operational improvements.

Unlike traditional modeling approaches that often rely on technical diagrams, **Big Picture EventStorming** harnesses free-form exploration, inclusive participation, and visual storytelling to reveal how a domain truly operates.

## Why Use Big Picture EventStorming?

1. **Discovery of Hidden Complexity**  
   Traditional modeling can overlook tacit knowledge buried in organizational silos. By collaboratively identifying domain events, participants expose unseen processes, conflicting interpretations, and systemic constraints that might otherwise remain unnoticed.  
   *Example:* A logistics company uncovered a manual process for tracking returns—previously invisible to decision-makers—during an EventStorming session.

2. **Facilitation of Cross-Functional Collaboration**  
   **Business leaders, domain experts, technical teams, and end-users** all speak the same “event language” in EventStorming. This shared perspective bridges gaps between departments and breaks down communication barriers.  
   *Example:* A retail company used EventStorming to bring marketing and IT teams together, reducing campaign rollout time by 30%.

3. **Acceleration of Learning**  
   What typically takes weeks or months of isolated research is condensed into a **few hours** of dynamic, collaborative discovery. Teams quickly grasp complex systems and can make more informed decisions faster.

4. **Uncovering Strategic Insights**  
   By mapping an entire system visually—from events to pain points—organizations can pinpoint **bottlenecks, inefficiencies, and improvement areas**. This holistic view often sparks innovative solutions or reveals untapped opportunities.

## Key Principles

![Elements of Big Picture EventStorming](./images/BigPictureEventStorming%20Grammar.png)

1. **Domain Event Focus**  
   - **What Are Domain Events?**  
     They are significant, observable state changes in a system (e.g., “Order Created,” “Payment Approved,” “Shipment Dispatched”).  
   - **Why Focus on Events?**  
     Events form a natural, business-friendly language. They expose **causality, dependencies**, and the **sequence** of processes, bridging technical and non-technical conversations.

2. **Inclusivity and Diversity**  
   - **Who Should Participate?**  
     A broad mix of stakeholders—business analysts, developers, product managers, operations, end-users, and potentially customers.  
   - **Why Diversity Matters**  
     Each person brings a unique lens. A domain expert flags critical rules, a developer spots potential constraints, and a user highlights real-world friction.  
   - **Techniques for Engagement**  
     Use **icebreakers**, **group rotations**, and **active facilitation** to ensure every voice is heard, especially in culturally diverse or hierarchical environments.

3. **Free-Form Exploration**  
   - **Purpose of Chaotic Exploration**  
     Participants add sticky notes of events, questions, or challenges without immediate critique. This unstructured approach uncovers **tacit knowledge** and **unspoken assumptions**.  
   - **Benefits of Open Contribution**  
     The lack of rigid rules spurs creativity, revealing details that might never emerge in a more formal setting.  
   - **Handling Overlaps and Redundancies**  
     Duplicates or contradictions often signal **ambiguity** or **misalignment**, paving the way for deeper discussions.

4. **Collaborative Refinement**  
   - **From Chaos to Clarity**  
     After the initial burst of ideas, the facilitator guides the group in **organizing events** into logical timelines and clusters.  
   - **Identifying Patterns and Dependencies**  
     Visualizing the sequence reveals repeated patterns, bottlenecks, and dependencies that can hamper efficiency.  
   - **Resolving Ambiguities**  
     Group discussions during refinement clarify **edge cases** and **exceptions** that were initially overlooked.

5. **Actionable Outcomes**  
   - **Translating Insights into Action**  
     The ultimate goal is producing deliverables—like a prioritized list of improvements or a clarified project scope—that can be acted upon immediately.  
   - **Linking to Strategy**  
     Align recognized challenges and opportunities with overarching business goals for better **executive buy-in**.  
   - **Deliverables and Artifacts**  
     Provide **visual summaries**, documentation of insights, and a definitive list of next steps to sustain momentum post-workshop.

## Steps to Facilitate a Big Picture EventStorming Workshop

1. **Preparation**  
   - **Define Objectives (30 min)**  
     Clarify the workshop’s purpose (e.g., discovering operational bottlenecks, scoping a new project).  
   - **Invite the Right Participants (15 min)**  
     Ensure all relevant roles are represented: business stakeholders, domain experts, tech leads, product managers, and end-users.  
   - **Set Up the Space (45 min)**  
     Secure a large open wall (or use a virtual whiteboard like Miro or MURAL). Provide sticky notes, markers, and color codes for events, systems, or challenges.

2. **Kick-Off (20 min)**  
   - Introduce the **purpose, structure, and desired outcomes** of the workshop.  
   - Establish **ground rules** of collaboration and respect.  
   - Use a simple **icebreaker** or warm-up activity to set a welcoming, open tone.

3. **Chaotic Exploration (60–90 min)**  
   - Participants freely add sticky notes representing **domain events, observations, or questions**.  
   - Encourage an **open, non-judgmental atmosphere** where all ideas are valid.  
   - The facilitator observes and gently guides, ensuring quieter participants are included.

4. **Organization and Categorization (60 min)**  
   - Cluster related events to form **logical workflows**. Create timelines and group similar items.  
   - Identify **key actors** (e.g., customer, system admin) and their interactions.  
   - Use distinct colors or symbols to highlight **bottlenecks, open questions, and critical systems**.

5. **Analysis of Hotspots (45–60 min)**  
   - Zoom in on areas with dense notes or **frequent debate**—these “hotspots” often reveal underlying issues or key opportunities.  
   - Facilitate discussions to determine **root causes** and brainstorm solutions collectively.

6. **Prioritization and Next Steps (30 min)**  
   - Summarize **key findings** and highlight areas needing further investigation or immediate action.  
   - Assign **ownership** for follow-up (e.g., “Product team will investigate payment failures”).  
   - Document the workshop outcomes—visual artifacts, notes, and next steps—to maintain shared understanding.

## Ideal Use Cases

1. **Discovery Initiatives**  
   - **Understanding Complex Domains**: Before launching a project, reveal hidden intricacies in business processes.  
   - **Mapping Business Processes**: Identify inefficiencies during digital transformations (e.g., in legacy approval systems).  
   - **Cross-Functional Collaboration**: Unite siloed departments under one cohesive view.

2. **Strategic Alignment**  
   - **Synchronizing Business and IT**: Ensure proposed solutions align with **business goals** and **KPIs** (e.g., time to market, customer satisfaction).  
   - **Evaluating Opportunities**: Spot areas for innovation or new services based on domain insights.

3. **Legacy System Analysis**  
   - **Deconstructing Legacy Systems**: Understand the structure and dependencies of monolithic architectures to plan modernization.  
   - **Identifying Technical Debt**: Pinpoint outdated components or convoluted workflows that slow progress.  
   - **System Documentation**: Generate a **visual roadmap** of current-state processes for reference and future planning.

4. **Problem Exploration**  
   - **Addressing Recurring Issues**: Investigate systemic problems, such as misaligned handoffs or frequent process errors.  
   - **Root Cause Analysis**: Delve deeper into hotspots to uncover underlying issues.  
   - **Testing Hypotheses**: Safely explore “what-if” scenarios before committing resources.

## Tangible Outcomes

1. **Comprehensive Domain Maps**  
   - A **visual blueprint** of the system’s events, actors, and interactions.

2. **Shared Understanding**  
   - Unified perspectives across **technical and non-technical** stakeholders.

3. **Clear Action Items**  
   - Identified **areas for further exploration**, immediate fixes, or strategic initiatives.

4. **Improved Collaboration**  
   - Better teamwork and communication through a **common language** of events.

5. **Strategic Insights**  
   - Understanding of **bottlenecks, innovation possibilities**, and system-wide improvements.

## Summary

**Big Picture EventStorming** is far more than a simple workshop—it’s a **transformative methodology**. By zeroing in on domain events and nurturing open dialogue, EventStorming helps organizations:

- **Expose hidden complexities** and insights.  
- **Break down siloed thinking** and encourage collaboration.  
- **Drive continuous improvement** and strategic alignment.

## Example Procurement Process

![Big Picture EventStorming Procurement Process](./images/BigPicture%20EventStorming%20Example.png)

### 1. Identify Key Players (Stakeholders)

- **Requestor/Employee**: Person who needs to purchase goods/services.  
- **Manager**: Approves the request from a budget or need perspective.  
- **Procurement Officer**: Oversees sourcing, vendor selection, and contract management.  
- **Finance**: Manages budgeting, invoices, payments, and financial reporting.  
- **Supplier/Vendor**: Provides goods/services and invoices.  
- **Legal**: Contract Negotiations with Suppliers

### 2. Major Domain Events

Below are typical events along the procurement journey:

1. **Purchase Requisition Created** : Triggered when an employee identifies a need and submits a requisition form or request in a system.
2. **Purchase Requisition Approved**: Manager or budget owner reviews and approves (or rejects) the request based on need, budget availability, etc.
3. **Request for Quotation (RFQ) Sent**: Procurement officer solicits quotes from multiple suppliers, ensuring competitive pricing or favorable terms.
4. **Suppliers Respond to RFQ**: Suppliers provide pricing, timelines, and other details. Procurement compiles responses for comparison.
5. **Supplier Shortlisted & Selected**: Procurement and stakeholders evaluate responses, select a preferred vendor, and possibly hold negotiations.
6. **Contract Finalized (If Needed)**: Formal agreement covering pricing, deliverables, timelines, and legal terms is drafted and signed.
7. **Purchase Order (PO) Created**: Official PO is issued to the chosen supplier, outlining order details and referencing contract terms.
8. **Goods/Services Delivered**: The supplier delivers goods or services to the requesting department, completing or partially completing the order.
9. **Goods/Services Inspected & Received**: Requestor confirms the delivery matches specifications, quality standards, or SLAs.
10. **Invoice Received**: Supplier sends an invoice referencing the PO, detailing payment terms.
11. **Invoice Approved**: Accounts (Finance) payable validates invoice details against the PO, resolves discrepancies, and approves for payment.
12. **Payment Released**:Finance processes the payment, finalizing the transaction and updating financial records.
13. **Procurement Review & Reporting (Read Model)**: Periodic or ad hoc review of spend, supplier performance, and process metrics to identify improvements.

### 3. Possible Pain Points (Hotspots)

1. **Manual, Paper-Driven Requisitions**
   - **Issue**: Paper forms or outdated software can slow approvals and create confusion about requisition status.  
   - **Impact**: Delays, errors in data entry, lack of transparency.

2. **Approvals Bottleneck**
   - **Issue**: Approvals pile up with a single manager or a specific department.  
   - **Impact**: Slow progress, tension between departments, and last-minute escalations.

3. **Inefficient RFQ & Supplier Selection**
   - **Issue**: Manually emailing or calling multiple suppliers leads to long turnaround times.  
   - **Impact**: Potential missed cost savings, disorganized documentation, and extended procurement cycles.

4. **Contract Negotiation Delays**
   - **Issue**: Legal or management back-and-forth can be protracted if contract processes aren’t streamlined.  
   - **Impact**: Missed deadlines, lost discounts, potential friction with suppliers.

5. **Invoice Matching Errors**
   - **Issue**: If invoice details don’t match the PO or receiving records, manual reconciliation is time-consuming.  
   - **Impact**: Delayed payments, frustration for suppliers, and potential financial penalties.

6. **Lack of Spend Analytics**
   - **Issue**: Without proper analytics, organizations can’t identify overspending, vendor performance issues, or cost-saving opportunities.  
   - **Impact**: Reactive decision-making, missed negotiating power, hidden inefficiencies.

### 4. Potential Opportunities & Improvements

- **Automated Procurement Platform**
  - **Opportunity**: Implement an integrated digital system or e-procurement suite (e.g., Coupa, SAP Ariba, or a custom solution).  
  - **Value**:
    - Speeds up requisition and approval flows.  
    - Consolidates vendor data, quotes, and PO information in one place.  
    - Enables real-time status tracking.

- **Streamlined Approval Workflow**
  - **Opportunity**: Introduce dynamic routing rules for approvals (e.g., up to a certain dollar amount only a single manager is needed).  
  - **Value**:  
    - Reduced bottlenecks and waiting times.  
    - Clear visibility of who’s holding up an approval.

- **Supplier Portal & Self-Service**
  - **Opportunity**: Provide suppliers with a portal to upload quotations, invoices, and track payment status.  
  - **Value**:  
    - Eliminates back-and-forth emails.  
    - Minimizes data entry errors and shortens response times.

- **Contract Templates & E-Signatures**
  - **Opportunity**: Use standard contract templates and digital signatures to expedite negotiations.  
  - **Value**:  
    - Shortens legal reviews with pre-approved terms and conditions.  
    - Offers clarity and reduces version-control chaos.

- **Real-Time Delivery Tracking & Quality Checks**
  - **Opportunity**: Integrate supplier logistics data into the procurement system for real-time shipment tracking.  
  - **Value**:  
    - Immediate alerts on delivery issues or delays.  
    - Automated checklists for inspection and acceptance of goods.

- **Automated Invoice Matching**
  - **Opportunity**: Deploy OCR (Optical Character Recognition) or AI-enabled invoice processing to match invoices with POs.  
  - **Value**:  
    - Reduces manual data entry and reconciliation errors.  
    - Quicker turnaround for vendor payments.

- **Centralized Data & Analytics**
  - **Opportunity**: Implement a robust data warehouse or analytics tool.  
  - **Value**:  
    - Gain visibility into total spend, supplier performance, cost savings opportunities.  
    - Informed, proactive decision-making on strategic sourcing.

- **Continuous Improvement & Supplier Relationship Management**
  - **Opportunity**: Create periodic review sessions to measure supplier performance (on-time deliveries, quality, compliance).  
  - **Value**:  
    - Foster stronger partnerships with top-performing suppliers.  
    - Uncover improvement areas and renegotiate better terms.

### 5. Next Steps for Transformation

- **Run a Focused Workshop**: Gather procurement stakeholders, finance, operations, IT, and major suppliers to validate these findings.  
- **Prioritize Issues & Opportunities**: Use a matrix to rank potential improvements by impact and feasibility.  
- **Develop a Roadmap**: Outline quick-win implementations (e.g., e-signatures, automated workflows) before tackling bigger changes (e.g., full e-procurement solution).  
- **Assign Ownership**: Clearly designate teams or individuals responsible for each improvement.  
- **Monitor & Evolve**: Use periodic metrics (cost savings, lead times, supplier satisfaction) to gauge success and refine the process.

## Conclusion

By mapping out the entire procurement journey through **Big Picture EventStorming**, organizations can visualize both friction points and opportunities. A clear, shared understanding of the **procurement process** paves the way for strategic changes—from **automation** and **data integration** to **better supplier relationships**—that deliver tangible benefits in cost savings, efficiency, and stakeholder satisfaction.
