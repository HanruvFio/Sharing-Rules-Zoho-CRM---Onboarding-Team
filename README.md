# Zoho CRM Account Onboarding & Sharing Rule Setup

This document outlines the process for configuring Zoho CRM to handle two distinct types of accounts:
1.  **Internal Portfolio Businesses:** Require a private onboarding process before being made visible to management.
2.  **External Clients:** Should be immediately visible to management upon creation.

The goal is to automate account visibility based on an `Onboarding Status` field.

## Prerequisite: Custom Field

Before starting, ensure a **mandatory** Pick List field has been created in the **Accounts** module.

-   **Field Name:** `Onboarding Status`
-   **Values:**
    -   `In Progress`
    -   `Completed`
    -   `External Client`
-   **Default Value:** Should be set to `-None-`.

---

## Step 1: Create the "Onboarding Team" Group

First, create a dedicated group for the two-person onboarding team.

1.  Navigate to **Setup > Users and Control > Groups**.
2.  Click the **New Group** button.
3.  Fill in the details:
    -   **Group Name:** `Onboarding Team`
    -   **Description:** `A 2-person team responsible for onboarding new portfolio businesses.`
4.  Under **Group Members**, add the two specific users who are on this team.
5.  Click **Save**.

---

## Step 2: Create the NEW Sharing Rule for Onboarding

This rule handles accounts that are `In Progress`, making them visible *only* to the Onboarding Team and the CEO.

1.  Navigate to **Setup > Security Control > Roles and Sharing**.
2.  Select the **Sharing Rules** tab.
3.  Click the **Create Sharing Rule** button.
4.  Configure the rule as follows:
    -   **Module:** `Accounts`
    -   **Rule Name:** `Share Onboarding Accounts`
    -   **Which records to be shared?:** Select **Based on criteria**.
    -   **Criteria:**
        ```
        Onboarding Status | is | In Progress
        ```
    -   **Who the records should be shared with?:**
        > Note: You will add two separate shares to the same rule.
        -   **Share 1:**
            -   **Share with:** `Groups`
            -   **Select:** `Onboarding Team`
        -   **Share 2 (Click `+ Add`):**
            -   **Share with:** `Roles`
            -   **Select:** `CEO`
    -   **What type of access to be provided?:**
        -   Set the permission to `Read/Write` for both shares.
5.  Click **Save**.

---

## Step 3: Update the EXISTING Management Sharing Rule

This step modifies the main management rule to grant access to accounts that are either completed or are external clients.

1.  Navigate to **Setup > Security Control > Roles and Sharing** and go to the **Sharing Rules** tab.
2.  Find your existing rule for the management team (e.g., `Share All Accounts with Management`).
3.  Click **Edit** for that rule.
4.  **Change the Criteria** to include two conditions:
    ```
    1. Onboarding Status | is | Completed
    2. Onboarding Status | is | External Client
    ```
5.  **Specify the
