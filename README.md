# Customer-Ticketing-System
Multi agent customer support system using CrewAI and Groq api key

Building Steps

Overall System Architecture

One manager agent to oversee the process
3 Specialist agents
Classifier
Router
Responder
Sequential workflow where tickets flow through these agents
Input ticket → Supervisor
Supervisor → Classifier (get category/priority)
Supervisor → Router (get department)
Supervisor → Responder (draft response)
Supervisor reviews and outputs final result
Agent Definitions

Supervisor Agent

Role: Coordinate the workflow between agents
Skills: Process management, delegation, quality control
Tools needed: Access to all ticket information, ability to call other agents
Classifier Agent

Role: Initial ticket analysis
Skills: Categorisation, priority assessment, key info extraction
Tools needed: Classification prompt templates, category definitions
Outputs: Ticket category, priority level, key extracted information
- analyze_ticket_content() -> Extracts key information from ticket text
- determine_priority() -> Assigns priority based on content
- identify_category() -> Maps ticket to predefined categories
Router Agent

Role: Determine best department/handler
Skills: Department matching, workload assessment
Tools needed: Department rules/criteria, current workload info
Outputs: Target department, routing justification
- check_department_load() -> Checks current ticket load per department
- match_skills_required() -> Maps ticket needs to department capabilities
- get_routing_rules() -> Retrieves current routing policies
Responder Agent

Role: Draft initial responses
Skills: Response composition, template customisation
Tools needed: Response templates, knowledge base access
Outputs: Draft response, suggested knowledge base articles
- fetch_knowledge_base_articles() -> Gets relevant help articles
- generate_response() -> Creates custom response
- check_response_tone() -> Ensures appropriate tone
Assign tools to agents like so:

Copyclassifier_agent = Agent(
    role="Classifier",
    goal="Accurately categorize support tickets",
    tools=[analyze_ticket_content, determine_priority, identify_category]
)
