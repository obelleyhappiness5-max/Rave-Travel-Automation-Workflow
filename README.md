Rave Travel Lead Automation Documentation
The Rave Travel lead automation is a WhatsApp lead acquisition and conversion system built for a travel destination company.

Project Overview

This project automates the entire lead management process for a travel company using artificial intelligence and workflow automation. When a potential customer sends a WhatsApp message, the system engages them intelligently, collects their study and destination details, qualifies their intent, and stores everything in a spreadsheet.
The system is capable of holding a full multi-turn conversation with a lead, matching their budget to suitable travel destinations.

Tools and Technologies

1.N8n: For workflow automation 
2.Twilio: Whatsapp communication
3.Google Gemini: Conversational AI and lead processing
4.Google Sheets: Lead database 
5.Ngrok: Https access

Automation Flow

WhatsApp Trigger
A customer sends a message to the company's WhatsApp number powered by Twilio. This instantly fires a webhook to n8n, waking up the automation pipeline.
AI Agent Processing
The message is passed to a Google Gemini AI Agent node in n8n. The agent is configured with a system prompt that defines its role as a travel assistant for Rave Travel & Tours. It collects the following details from the customer one question at a time:

1.Destination interest (UK, Canada, Australia, Ireland, Austria)
2.Tuition fees budget
3.Course option being considered
4.Intended payment method

Conversation Memory
A memory node is attached to the AI Agent, using the customer's WhatsApp number as a unique session key. This ensures Gemini remembers the full conversation history across multiple messages, enabling a natural back-and-forth exchange.
Lead Qualification (IF Node)
Once Gemini has collected all required details, it appends a tag to its response:
[Alright] — all details collected successfully
[Hello?] — customer is vague, unresponsive or uninterested

Lead Classification
An IF node checks for the tag
Serious Lead (Hot) → A WhatsApp notification with the lead's full details is sent directly to the company owner, and the lead is saved to Google Sheets with status Hot Lead
Unserious Lead (Cold) → The lead is saved to Google Sheets with status Cold Lead for future follow-up

Google Sheets Database Structure
Field	Description
Customer Phone	WhatsApp number of the lead
Destination Interest	Country or region of interest
Budget	Stated tuition fees budget
Course Option	Programme the customer is considering
Payment Method	How they intend to pay fees
Lead Status	Hot Lead / Cold Lead
Date Captured	Timestamp of first contact
Conversion Summary	AI-generated summary of the chat
