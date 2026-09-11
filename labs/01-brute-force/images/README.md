# DVWA Brute Force Attack Lab

## Overview

This lab documents a brute-force authentication exercise performed against **Damn Vulnerable Web Application (DVWA)** in a controlled local environment.

The purpose of this exercise was to understand how weak authentication mechanisms can be targeted using automated credential guessing and how **Burp Suite Intruder** can be used to test combinations of usernames and passwords.

All testing was performed against DVWA, an intentionally vulnerable web application running locally for cybersecurity training.

---

## Objectives

The objectives of this lab were to:

- Configure a local DVWA testing environment.
- Set DVWA to the **Low** security level.
- Route browser traffic through Burp Suite.
- Intercept an authentication request.
- Send the captured request to Burp Suite Intruder.
- Configure username and password payload positions.
- Perform automated credential testing.
- Analyse server responses to distinguish failed and successful authentication attempts.
- Understand security controls that can mitigate brute-force attacks.

# DVWA Brute Force Attack Lab

## Overview

This lab documents...

...

## Objectives

The objectives of this lab were to:
...

---

## Lab Environment

| Component | Purpose |
|---|---|
| DVWA | Intentionally vulnerable web application used as the testing target |
| XAMPP | Provides the local Apache web server and MySQL database |
| Burp Suite | Used to intercept, inspect, and automate HTTP requests |
| Firefox | Browser used to access DVWA |
| Windows | Host operating system |
| Localhost | Local isolated testing environment |

**DVWA Security Level:** Low

> **Scope:** All testing in this lab was performed against my own local DVWA environment for educational purposes.

---

# Testing Procedure

## 1. Start the DVWA Environment

The first step was to start the services required for the DVWA environment.

XAMPP was used to run the **Apache web server** and **MySQL database** required by DVWA.

![Apache and MySQL running in XAMPP](images/01-xampp-apache-mysql-running.png)

With the required services running, DVWA could be accessed through the local web server.

## 2. Access DVWA

DVWA was accessed through the local web server using Firefox.

The DVWA login page provided access to the intentionally vulnerable application used throughout the lab.

![DVWA login page](images/02-dvwa-login-page.png)

After logging in, the application's security configuration could be changed for the exercise.

## 3. Configure the DVWA Security Level

The DVWA security level was configured to **Low** before performing the brute-force exercise.

![DVWA security level configured to Low](images/03-dvwa-security-level-low.png)

DVWA intentionally provides different security levels for learning purposes. The Low setting provides minimal protection, making it possible to observe how vulnerable authentication mechanisms behave.

## 4. Configure the Browser Proxy

Firefox was configured to route its web traffic through **Burp Suite**.

This allowed Burp Suite to operate as an intercepting proxy between the browser and the DVWA application.

![Browser proxy configuration for Burp Suite](images/04-browser-burp-proxy-configuration.png)

Routing traffic through Burp Suite made it possible to inspect and manipulate HTTP requests generated while interacting with DVWA.

---

## 5. Open the DVWA Brute Force Module

The **Brute Force** vulnerability module was selected from the DVWA navigation menu.

![DVWA Brute Force module](images/05-dvwa-brute-force-page.png)

The module contains a basic username and password authentication form. This provided the authentication endpoint used for the exercise.

---

## 6. Intercept the Authentication Request

Burp Suite Proxy interception was enabled before submitting credentials through the DVWA authentication form.

![Burp Suite interception enabled](images/06-burp-suite-intercept-enabled.png)

When the login attempt was submitted, Burp Suite intercepted the HTTP request before it reached the DVWA server.

Capturing the request allowed the authentication parameters to be inspected and provided a request that could be reused for automated testing.

---

## 7. Send the Request to Burp Suite Intruder

The captured authentication request was sent from **Proxy** to **Burp Suite Intruder**.

![Sending the authentication request to Intruder](images/07-send-login-request-to-intruder.png)

Intruder can repeatedly send modified versions of an HTTP request while replacing selected parameters with values from predefined payload lists.

This makes it useful for demonstrating automated credential testing in a controlled environment.

---

## 8. Configure the Attack Positions

Within Intruder, the username and password parameters were selected as payload positions.

A **Cluster Bomb** attack configuration was used because two independent payload sets were being tested.

![Burp Intruder Cluster Bomb payload positions](images/08-intruder-cluster-bomb-positions.png)

With this configuration, Burp Suite can test combinations between the username and password payload sets.

Conceptually, combinations are generated in the following way:

```text
username1 : password1
username1 : password2
username2 : password1
username2 : password2