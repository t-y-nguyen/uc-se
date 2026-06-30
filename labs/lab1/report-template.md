# Lab 1 — Simple Messenger: CI/CD Cloud Deployment and Secure Implementation
# Report 

| | |
|---|---|
| **Course** | EECE/CS 3093C — Software Engineering, Summer 2026 |
| **Instructor** | Dr. Phu Phung |
| **Name** | Ty Nguyen |
| ** Email** | nguye8tl@mail.uc.edu |
| **GitHub Repository** | https://github.com/t-y-nguyen/se-nguye8tl |
| **Azure Live URL** | https://nguye8tl-messenger-lab1.azurewebsites.net/ |

---
## Overview

In this lab, I built and deployed a real-time messaging application using Node.js, Express, Socket.IO, GitHub Actions, and Azure. I implemented core messaging features, configured an automated CI/CD pipeline, and applied basic security measures to protect the application from XSS attacks. This lab helped me gain practical experience with web development, cloud deployment, and secure coding practices.

## Task 1 — Git Branch, Node.js Web Application Setup and Testing

### Screenshot 1a — Local app running
*Caption:* Terminal showing npm start output (Server running on port 8080) and the Web Preview in the browser confirming the UI with my name loads

<img width="2061" height="1068" alt="image" src="https://github.com/user-attachments/assets/533a887f-e04d-4ce8-a60a-b3c5505e65df" />


### Commit Link
https://github.com/t-y-nguyen/se-nguye8tl/commit/b8c083b19cf2287b90af777ff674223e53f9870f

---

## Task 2 — CI/CD Pipeline and Azure Deployment

### Screenshot 2a — Azure App Service Overview
*Caption:* Azure App Service Overview page showing the app name, status Running, and the default domain URL

<img width="2010" height="1013" alt="image" src="https://github.com/user-attachments/assets/43510c40-c4b1-4c4f-867e-ab42a93044fc" />

### Screenshot 2b — GitHub Actions green run
*Caption:* GitHub Actions run (green checkmark) showing the workflow steps completed successfully

<img width="1290" height="1246" alt="image" src="https://github.com/user-attachments/assets/7f7c7c2a-0ed0-44f5-a437-ae2b0e90b507" />

### Screenshot 2c — Live app on Azure
*Caption:* Browser showing the Messenger UI with my name at the Azure URL, with browser console debug information visible

<img width="2037" height="1107" alt="image" src="https://github.com/user-attachments/assets/76cef52d-d754-49b4-baac-0f48f01b5b06" />

---

## Task 3 — Use Case Realization: "Send Message"

### Analysis and Design

## Brief Use Case Description
Connected User types a message and clicks Send; system delivers it in real time to all connected users.

## User Stories
- [x] As a connected user, I want to type a text message and click Send so that all users in the chat can read it in real time. (AC-01.1, AC-01.2, AC-01.3, AC-01.4)
- [x] As a connected user, I want to press Enter to send a message so that I do not need to use the mouse. (AC-01.1, AC-01.3)
- [x] As a connected user, I want the input field to be cleared after I send a message so that I can type the next message immediately. (AC-01.5)

## Acceptance Criteria
- [x] AC-01.1: a message input field and a Send button are present and usable on the chat screen.
- [x] AC-01.2: when the input field is empty and Send is clicked or Enter is pressed, no message appears in the chat.
- [x] AC-01.3: when a non-empty message is sent, it appears in the chat window of all connected users immediately.
- [x] AC-01.4: each message displayed in the chat shows the sender's username alongside the message text.
- [x] AC-01.5: after a message is sent, the input field is cleared and ready for the next message.

## Interaction/Sequence Diagram

<img width="941" height="444" alt="Image" src="https://github.com/user-attachments/assets/0688c5d6-725c-418e-9b49-b3e6172b8f2a" />

### Screenshot 3a — `client.js` sendMessage() code
*Caption:* client.js code showing the implemented sendMessage() function with AC code comments

<img width="1687" height="838" alt="image" src="https://github.com/user-attachments/assets/4a64ff82-45a1-4cb2-ba5f-eb8ca2852615" />

### Screenshot 3b — `server.js` chat message handler
*Caption:* server.js code showing the chat message event handler with AC code comments

<img width="1887" height="588" alt="image" src="https://github.com/user-attachments/assets/bfc16928-9e33-40fe-889b-2c7c35b9faf1" />

### Screenshot 3c — Two-tab live demo
*Caption:* live app (Azure URL) with two browser windows open, showing a message sent from one window appearing in both (Same image for Task 5b, but you can see the chat messages still showing on both screens under the alert message)

<img width="1390" height="732" alt="image" src="https://github.com/user-attachments/assets/6a7edcb7-ec3d-440e-97e8-5c97260bae0a" />

---

## Task 4 — Use Case Realization: "Receive Message"

### Analysis and Design

## Brief Use Case Description
System notifies Connected User of incoming message and displays it in the conversation view without page refresh.

## User Stories
- [x] As a connected user, I want incoming messages to appear automatically so that I can follow the conversation without refreshing the page. (AC-02.1)
- [x] As a connected user, I want each message to show a timestamp so that I can see when it was received. (AC-02.2)
- [x] As a connected user, I want system notifications (join/leave) to appear in a separate area and look different from chat messages so that I can distinguish them at a glance. (AC-02.3, AC-02.4)
- [x] As a connected user, I want the application to prevent injected scripts
in chat messages from executing in my browser, so that my session and data cannot be
stolen by other users. (AC-02.5, AC-02.6)

## Acceptance Criteria
- [x] AC-02.1: incoming chat messages are displayed in the responses area without page refresh.
- [x] AC-02.2: each message shows a timestamp alongside the message text.
- [x] AC-02.3: system status events (join/leave) are displayed in the status area, visually separate from chat messages.
- [x] AC-02.4: the status area auto-scrolls to the latest system event.
- [x] AC-02.5 (Security) Message content received from the server is rendered as plain text or HTML-escaped output — never as raw innerHTML — so that injected HTML or JavaScript in a message payload cannot execute in the recipient's browser. (OWASP A03: Injection)
- [x] AC-02.6 (Security) The server responds with a Content-Security-Policy HTTP header restricting script execution to same-origin sources (script-src 'self'), providing browser-level defence-in-depth against XSS. (SSDLC: secure HTTP headers)

## Interaction/Sequence Diagram

<img width="765" height="442" alt="Image" src="https://github.com/user-attachments/assets/9c50569d-34ec-4649-bdcd-90a334771b3c" />

### Screenshot 4a — `client.js` socket listeners
*Caption:* client.js code showing the chat message and status socket handlers with AC code comments

<img width="1896" height="916" alt="image" src="https://github.com/user-attachments/assets/159f4c6b-73d0-4e00-95ae-b9cdcff8b19f" />

### Screenshot 4b — `server.js` connect/disconnect handlers
*Caption:* server.js code showing the connect/disconnect status emission with AC code comments

<img width="1916" height="293" alt="image" src="https://github.com/user-attachments/assets/a5d4b310-5dbb-4457-a910-848b890c730a" />

### Screenshot 4c — Two-tab live demo with timestamp and status
*Caption:* live app (Azure URL) with two browser windows open, showing a chat message with a timestamp (AC-02.2) and a join/leave notification in the status area that is visually separate from chat messages (AC-02.3)

<img width="1698" height="817" alt="image" src="https://github.com/user-attachments/assets/d454b9ba-b105-4036-919f-805f827d2381" />

### Commit Link
https://github.com/t-y-nguyen/se-nguye8tl/commit/9172c293ef9ff0b70e984b61c505ffb78666e927

---


## Task 5 — Security: Input Validation, CSP, and XSS Prevention

5a. Screenshot of the GitHub Issue updated with new user stories and security ACs before implementing any security code. (SSDLC feedback loop)
5b. Screenshot of the XSS attack before the fix — show the alert dialog appearing in the victim's browser tab. The caption must identify which tab is the attacker and which is the victim.
5c. Screenshot of the XSS attack after the fix.
5d. Screenshot of the browser DevTools Network tab showing the Content-Security-Policy header in the server response.
5e. URL link to the specific commit for this task.


### Screenshot 5a — GitHub Issue (before security code)
*Caption:* GitHub Issue updated with new user stories and security ACs before implementing any security code

<img width="1177" height="1140" alt="image" src="https://github.com/user-attachments/assets/622772a1-9336-410f-a90e-a653d6fac8c4" />

### Screenshot 5b — XSS attack BEFORE the fix
*Caption:* XSS attack before the fix — show the alert dialog appearing in the victim's browser tab (Right Tab is Attacker)

<img width="1390" height="732" alt="image" src="https://github.com/user-attachments/assets/6a7edcb7-ec3d-440e-97e8-5c97260bae0a" />

### Screenshot 5c — XSS attack AFTER the fix
*Caption:* The chat window code element showing the injected payload was removed. Demonstrates DOMPurify blocking the attack.

<img width="1692" height="832" alt="image" src="https://github.com/user-attachments/assets/721566bb-e9ea-4581-80b8-93260bdcf41f" />

### Screenshot 5d — Browser DevTools CSP header
*Caption:* Browser DevTools → Network tab → document response showing the `Content-Security-Policy` header returned by the server.

<img width="1020" height="987" alt="image" src="https://github.com/user-attachments/assets/0e543263-800d-4c29-95a7-859b6ed6307e" />

### Commit Link
https://github.com/t-y-nguyen/se-nguye8tl/commit/bf25443dafabb0351b5eae2c792ac190a48f95e1

---

## Reflection Questions

**Q1.** The Secure Software Development Lifecycle (SSDLC) principle applied in Step 0 requires creating a GitHub Issue *before* writing security code. Why is this order important, and how does it reflect the "security as a cross-cutting concern" principle discussed in Lecture 11?

This documents the security requirements before you even start coding. This makes sure that security is planned from the start of the development process instead of just being integrated at the end, which makes it a cross-cutting concern

---

**Q2.** In Task 5 you used `DOMPurify.sanitize()` rather than setting `element.textContent`. What is the key advantage of DOMPurify over `textContent` for this application, and why was the server-side `xss` npm package not used?

DOMPurify removes harmful HTML and allows safe HTML content when needed. textContent only displays plaintext. So the server-side XSS package was not used bc we used a client-side output sanitization with DOMPurify

---

**Q3.** Explain why the `style-src 'unsafe-inline'` directive was needed in the CSP configuration, and what risk this introduces. How would you mitigate that risk in a future sprint?

Its needed because the app uses inline css so this puts a risk of attackers injecting malicious inline styles so to mitigate this risk we would put the styles in a external css file and remove unsafe-inline from the CSP.

---

## Summary

| Task | Description | Points Claimed |
|---|---|---|
| Task 1 | Skeleton setup, package.json, local test | /6 |
| Task 2 | CI/CD pipeline and Azure deployment | /6 |
| Task 3 | Use-Case-01: Send Message | /6 |
| Task 4 | Use-Case-02: Receive Message | /6 |
| Task 5 | Security: XSS prevention and CSP | /6 |
| Report | Screenshots, captions, commit links | /5 |
| **Total** | | **/35** |
---

*This lab report was prepared as part of EECE/CS 3093C Software Engineering, Summer 2026, University of Cincinnati.*
