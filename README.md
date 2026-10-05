# CodeAlpha_PhishingSimulation (Bonus Project)

Phishing attack simulation and analysis built with the **GoPhish** framework, as a bonus deliverable alongside my CodeAlpha Cyber Security Internship tasks.

> ⚠️ **Ethical disclosure:** This was a controlled, educational simulation run against my own consenting test accounts only. No real users were targeted without knowledge or consent. No real credentials were stored or misused.

## Overview

This project simulates a realistic phishing campaign — scenario design, a cloned landing page, a personalized phishing email, campaign execution, and data analysis — to understand how social engineering attacks succeed and how to defend against them.

## 1. Campaign Design

A **university Registrar's Office** scenario was chosen as the pretext: a fake notice claiming course registration was opening and students needed to re-verify their portal login.

This scenario works because it combines three classic social-engineering triggers:
- **Urgency** — registration deadlines create time pressure
- **Authority** — the Registrar's Office is a trusted source
- **Familiarity** — students already expect these emails

**Setup:** GoPhish v0.12.1 on Windows 11, admin panel at `https://127.0.0.1:3333`, phishing server on port 80, Gmail SMTP (`smtp.gmail.com:587`) as the sending profile.

## 2. Landing Page

A manual HTML clone of a university student portal login was built (cloning real sites directly often breaks due to JS/anti-phishing protections). Key techniques:
- `Capture Submitted Data` + `Capture Passwords` enabled in GoPhish
- Form `action=""` + `method="POST"` routes submissions back to GoPhish
- Victims redirected to the **real** university site post-submission, to avoid suspicion
- A visible disclosure banner was included for ethical transparency

See [`landing_page.html`](landing_page.html) for the full page.

## 3. Email Engineering

The phishing email used GoPhish templating (`{{.FirstName}}`, `{{.LastName}}`) for personalization, and leaned on the same urgency/authority/familiarity triggers. See [`email_template.html`](email_template.html).

In a real attack, the sender domain would also be spoofed or typo-squatted (e.g. `univeristy.edu`); this simulation used a plain Gmail address for transparency.

## 4. Campaign Execution

| Event | Time |
|---|---|
| Email opened | 4:32:00 |
| Link clicked | 4:32:30 |
| Credentials submitted | 4:33:00 |

Single-stage attack: one email, direct link to the fake login page. (A multi-stage attack would follow up only with users who clicked, using a stronger second lure.)

## 5. Results & Analysis

| Metric | Value |
|---|---|
| Open rate | 50% (1/2) |
| Click-through rate (of opens) | 100% (1/1) |
| Submission rate (of clicks) | 100% (1/1) |
| Overall success rate | 50% (1/2) |
| Time from click → credential submission | 30 seconds |

**Takeaway:** once a target clicked, they submitted credentials without hesitation — the landing page was convincing enough that no one paused to check the URL.

## Defensive Recommendations

1. **Security awareness training** — teach users to check sender addresses and hover over links before clicking
2. **Multi-Factor Authentication (MFA)** — stolen credentials alone shouldn't be enough to log in
3. **Email authentication** — SPF, DKIM, DMARC to catch spoofed senders
4. **Regular phishing simulations** — measure and improve awareness over time

## Tools Used
- [GoPhish](https://getgophish.com/) — open-source phishing framework
- Gmail SMTP (test sending profile)

## Related Work

📘 This simulation was used as a case study in my official Task 2 submission: [CodeAlpha_PhishingAwareness](https://github.com/bruktawitmulat56-cmd/CodeAlpha_PhishingAwareness) — a phishing awareness training deck for end users.

## References
- GoPhish Documentation — https://docs.gophish.io/
- Google — Report phishing emails — https://support.google.com/mail/answer/8253
- NIST Cybersecurity Framework — https://www.nist.gov/cyberframework
