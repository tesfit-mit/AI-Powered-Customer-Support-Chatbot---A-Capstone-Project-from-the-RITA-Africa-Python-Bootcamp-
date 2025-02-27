AI-Powered Customer Support Chatbot - A Capstone Project from the RITA Africa Python Bootcamp!
I'm thrilled to present an AI-powered Customer Support Chatbot I built during the RITA Africa bootcamp (tag @RITA Africa). This project highlights how Python can be used to develop an interactive chatbot that efficiently handles customer inquiries through fuzzy matching and smart query recognition.

Key Features:
	AI-powered chatbot for handling customer inquiries
	 Fuzzy matching to recognize variations in user input
	 Logging unknown queries for continuous improvement

Skills Demonstrated:
 	Implementing dictionaries for structured responses
 	Using fuzzy logic to improve query recognition
 	 File handling for logging unknown queries
 	 Practical application of Python for AI-powered chatbots
 	 Problem-solving and debugging in Python
 	 Working with external libraries (fuzzywuzzy, python-Levenshtein)
 	Writing clean, modular, and reusable code
 	 Documenting code and processes for future reference
 	User interaction design for chatbots
 	Data logging and analysis for continuous improvement
 	 Version control and project management (if applicable)
 	Collaboration and communication skills (if working in a team)

Check out the project and let me know your thoughts!

----------------------------------code –goes here---------------------------------------------------------------


	# Install required libraries (run these commands in your terminal or notebook)
# !pip install fuzzywuzzy
# !pip install python-Levenshtein

from fuzzywuzzy import process
from datetime import datetime

# Define the FAQ and responses dictionary
faq_and_responses = {
    "Hello": "Hi there! Welcome to RITA AFRICA Chatbot. How can I assist you today?",
    "What is RITA Africa?": """
RISE IN TECH AFRICA, popularly known as RITA Africa, is a leading provider of online tech training and certification programs designed to empower individuals with the skills they need to succeed in the digital economy. Our platform offers a range of courses in areas such as data analytics, cloud computing, software development, cybersecurity, and more.
""",
    "what is your name": "I am a Chatbot, you can call me Rita-Chatbot.",
    "how are you": "I’m just a bot, but I’m doing great! How about you?",
    "what do you know about RITA Africa":"""RITA Africa is a premier tech training and job placement institution dedicated to empowering African youth with cutting-edge technology skills through sponsored training. Our goal is to bridge the tech skills
    gap and provide global job opportunities for talented individuals, regardless of their financial background.
    
    RITA Africa, officially registered as RISE IN TECH AFRICA, operates as a not-for-profit organization with its headquarters in Accra, Ghana,
    West Africa.
    """,
    "what are the programs in Rita-Africa?": """
The programs given in Rita Africa are:
- Data Analytics
- Data Science & AI/ML
- Cybersecurity
- Cloud Computing
- DevOps
- Software Engineering
- Fullstack Web Development""",
    "What are Eligibility Requirements for  Rita-Africa": """
At RITA Africa, we prioritize inclusivity and excellence in our student body. To ensure a conducive learning environment and optimal outcomes for all learners, we have established the following eligibility criteria:
1. Residency: Applicants must be African citizens residing in Africa.
2. Assessment: Complete the one-month Python Developer Bootcamp with InfoSorse, designed as our approved assessment program. Earn the certificate to qualify for RITA Africa’s main training.
3. Identity Verification: Applicants are required to upload a valid proof of identity document (e.g., national ID card, passport) during the application process.

4. Language Proficiency: Proficiency in English language is essential, including reading, writing, and comprehension skills.

5. Educational Background: While there may not be strict academic requirements, applicants should have a basic educational background.

6. Technology Access: Access to a reliable internet connection and necessary technology devices (e.g., computer, smartphone) for online learning.

7. Commitment: Demonstrated commitment to learning and dedication to completing the program successfully.

8. Age Requirement: Minimum age requirement may apply, typically 18 years or older.

9. Compliance: Compliance with all RITA Africa policies and procedures throughout the admission process and program duration.

10. Motivation: A genuine interest in pursuing a career in the technology industry and willingness to engage actively in the learning process.
""",
    "What are the Admission and Selection Criteria?": """
There are 4-steps to get selected and admitted into Rita-Africa program. The 4-Steps for Admission & Selection Process are:

➢ Step 1: Submit Your Application
Start by selecting the RITA Africa tech program that best aligns with your career goals. Once you’ve chosen your desired program, submit your application for review. If your application meets our criteria, you will receive an invitation email with the next steps to join the program.

➢ Step 2: Join the Bootcamp
Upon receiving your invitation, participate in a free two-week bootcamp designed to lay a strong foundation for your advanced training. The bootcamp will also assess your readiness for the year-long career program. This is an excellent opportunity to familiarize yourself with the training environment and ensure that you are prepared for the next phase.

What you will receive:
- Training: Top-notch instruction by experienced industry professionals.
- Career Readiness Assessment: Personalized assessments to assess your ability and readiness for industry-standard career training.
- Hands-on Projects: Hands-on, practical projects aligned with real-world demands.
- Certificate of Completion: A recognized certificate upon successful completion.

➢ Step 3: Acceptance and One-Time Admission Fee
After successfully completing the bootcamp with a passing score, you will be notified of your acceptance into the program. To secure your place, a one-time admission fee of $150 is required. This fee guarantees your entry into the full program and ensures that you are ready to embark on your journey toward becoming a tech professional.

➢ Step 4: Start Your Journey
Once your spot is confirmed, you’ll begin your fully-funded 9–12-month tech career program. Throughout this phase, you’ll gain in-depth training, participate in hands-on projects, and earn industry-recognized certifications. This program will open doors to exciting career opportunities in the tech industry and equip you with the skills needed to succeed.
""",
    "How long are the programs?": """
Program durations vary depending on the specific course. Some programs may be completed in 9 months, while others may span 12 months. Visit our website or check the program page for information on the duration of your chosen program.
""",
    "What types of certifications do you offer?": """
RITA Africa offers industry-recognized certifications in various tech-related fields, including data analytics, cloud computing, software engineering, cybersecurity, and more. Our certifications are designed to equip you with the skills and credentials you need to succeed in your chosen career path.
""",
    "Can I apply if I'm not based in Africa?": """
Given the stated requirement that applicants must be both African citizens and residents in Africa, if you are not currently residing in Africa, you would not meet the eligibility criteria for the application, even if you hold African citizenship.
""",
    "How do I apply for a program at RITA Africa?": """
To apply for a program at RITA Africa, simply visit our website and join the next Python Developer Bootcamp organized by InfoSorse. Upon successful completion of the bootcamp, use your certificate to apply for any RITA Africa program. Complete the online application form, ensuring you provide accurate information and upload required documents, such as proof of identity. Once your application is submitted, our admissions team will review it and notify you of the next steps.
""",
    "bye": "It was nice chatting with you, have a nice day!",
    "thank you": "You're very welcome! 😊 I'm glad I could help. If you have any more questions or need further assistance, feel free to ask.",
    "What is the purpose of Bootcamp program in Rita-Africa?": """
The bootcamp is designed to mirror the structure of the main program, providing participants with an opportunity to assess their abilities and readiness. This two-week intensive program ensures that you have the right foundation to excel in our year-long, fully funded training.
""",
    "Why we pay an Admission Fee": """
While RITA Africa’s training and certification programs are fully funded through sponsorship, the sponsorship covers only the educational and certification aspects of the program. Several essential operational costs remain uncovered, making the one-time admission fee of $150 a necessary contribution. Here’s why this fee is important:

=> Administrative Costs: Managing applications, coordinating bootcamps, and processing enrollments involve significant administrative efforts. The admission fee helps offset these operational costs, ensuring a smooth and professional experience for all participants.

=> Program Logistics: From maintaining our learning management systems to providing technical support during your training journey, the fee helps us sustain these critical components that enable effective learning.

This small investment from students not only secures a place in our comprehensive training program but also fosters a sense of commitment and responsibility toward their educational journey. With this approach, we aim to empower aspiring tech professionals across Africa, enabling them to kickstart their careers without financial burden. This model ensures that students who enter the main program are well-prepared and committed to completing it successfully.
""",
    "do you have success stories Excellent testimonial  from previous batch?": """
Yes, there are many young African talents graduated so far like:
- Nyenpandi Josephine from Liberia,
- Banedine Okeke from Nigeria,
- Ashenafi Mekonnen from Ethiopia,
- Jael Y. Ofari from Ghana,
- Emmanuel Angeyo from Uganda,
- Carl A. Tetteh from Ghana, and so many others.
"""
}
# Function to save unknown user input in a text file for future training
def log_unknown_query(query):
    with open("unknown_queries.txt", "a") as file:
        timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        file.write(f"[{timestamp}] {query}\n")

# Function to find the best match for user input using fuzzy matching
def get_best_match(user_input):
    best_match, score = process.extractOne(user_input, faq_and_responses.keys())
    return best_match if score > 80 else None  # Adjust threshold as needed

# Main chatbot function
def chatbot():
    print("Welcome to the customer support chatbot!")
    print("Type 'exit' to end the chat.\n ")

    while True:
        user_input = input("You: ").lower()

        if user_input == "exit":
            print("Bot: Thank you for using our chatbot. Goodbye!")
            break

        best_match = get_best_match(user_input)
        if best_match:
            print("Bot:", faq_and_responses[best_match])
        else:
            print("Bot: Sorry, I don't understand that. Can you try re-phrasing?")
            log_unknown_query(user_input)
# Run the chatbot
chatbot()


Welcome to the customer support chatbot!
Type 'exit' to end the chat.
 
You:  

******************************************************************************#RiseInTechAfrica #RITAAfricaBootcamp #RITAAfrica #Python

