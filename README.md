# **Find Doctor Agent Tool**

## **Project Overview**

The **Find Doctor Agent Tool** is an intelligent multi-agent system designed to help users quickly discover the most suitable doctors based on their symptoms, required specialization, and location. The system automatically interprets user input, identifies the relevant medical specialization, and retrieves the top doctors from trusted healthcare platforms such as **Practo**, **Apollo 24x7**, and **Lybrate**. It removes manual effort and provides an automated, unified doctor search experience using real-time web results.

---

## **Objective**

To build an AI-driven assistant that can:

* Understand user symptoms.
* Identify the correct medical specialization.
* Search across multiple healthcare platforms.
* Fetch and rank top doctors.
* Present results in a clean, structured format.

---

## **Key Features**

### **1. Symptom-to-Specialization Mapping**

* A dedicated agent (`find_disease_based_on_symptom_agent`) analyzes symptoms using search tools.
* Maps conditions like *chest pain → Cardiologist*, *acne → Dermatologist*, *headache → Neurologist*, etc.
* Minimizes the need for medical knowledge from the user.

### **2. Multi-Platform Doctor Search**

The core search agent integrates results from:

* **Practo**
* **Apollo 24x7**
* **Lybrate**

It retrieves:

* Doctor Name
* Specialization
* Rating
* Education / Credentials
* Consultation Fee
* Hospital / Clinic Address
* Source Website

### **3. Intelligent Ranking System**

Doctors are ranked automatically by:

1. Highest rating
2. Strong education and experience
3. Lowest consultation fees

### **4. Strict Tool-Driven Architecture**

* The doctor search agent is designed to **never provide medical advice**.
* It **must always** call the `search_agent` tool, ensuring reliable and consistent behavior.
* Safely bypasses emergency warnings and focuses strictly on data retrieval.

---

## **System Architecture**

The tool uses a **Sequential Multi-Agent Architecture**:

1. **User Input Handler**

   * Accepts symptoms + location.
   * If location missing → asks for city.

2. **Symptom Classification Agent**
   (`find_disease_based_on_symptom_agent`)

   * Identifies the required specialization using search tools.
   * Returns specialization only.

3. **Doctor Search Agent**
   (`doctor_search_agent`)

   * Calls the search_agent tool with specialization + location.
   * Collects and ranks top 3 doctors.

4. **Result Formatter**

   * Presents final results clearly to the user.

---

## **Technology Stack**

* **Gemini 2.5 Flash Lite** (LLM foundation)
* **Custom Agent Framework**
* **Tool Integrations:** Google Search, Custom search_agent
* **Python-based orchestration**
* **SequentialAgent for workflow control**

---

## **How It Works (Example Flow)**

### **User:**

“chest pain bengaluru”

### **Agent Flow:**

1. Symptom agent → returns **Cardiologist**
2. Doctor agent → calls search agent with specialization=Cardiologist, location=Bengaluru
3. Search agent → collects top 3 cardiologists from Practo, Apollo, Lybrate
4. Results printed to user

---
